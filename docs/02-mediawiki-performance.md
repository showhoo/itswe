# 02 · MediaWiki 性能调优实录（MediaWiki 1.46）

> [itswe.com](https://www.itswe.com) 建站文档 · 性能篇。三个真实生产事故的定位与修复，含可复现的数据与配置。环境：MediaWiki 1.46 + PHP-FPM 8.4 + MySQL 8（Docker）。

## 结论先行

| 优化项 | 措施 | 实测效果 |
|---|---|---|
| 页面渲染 | 对象缓存 `CACHE_DB` → APCu（`CACHE_ACCEL`） | 匿名文章页 **0.429s → 0.193s（2.2×）** |
| 全文搜索 | `OPTIMIZE TABLE searchindex` 重建 FTS | 初始化 5-15s → **1.8-2.2s** |
| 搜索索引膨胀 | 识别批量编辑追加增量段 | 104MB → 22MB |
| 渲染与缓存联动 | fastcgi_cache 手动失效机制 | 词条更新 ≤10 分钟可见 |

## 事故一：匿名搜索 4-10 秒

**现象**：未登录状态搜索极慢，登录后正常。

**定位**：`$wgDebugLogFile` + 数据库 PROCESSLIST 显示单次搜索产生 **13,356 次 objectcache SQL**——MediaWiki 把系统消息包、LinkCache、中文变体（zh/zh-hant/zh-cn/en）逐条回源，全砸在 `objectcache` 表上。

**根因**：`$wgMainCacheType = CACHE_DB`。DB 对象缓存比无缓存强不了多少：它仍是 SQL，且行级读写放大严重。

**修复**：PHP 容器内安装 APCu 并切缓存类型：

```bash
# 容器内
pecl install apcu
docker-php-ext-enable apcu
# php.ini
apc.shm_size=256M
apc.enable_cli=1
```

```php
$wgMainCacheType    = CACHE_ACCEL;
$wgMessageCacheType = CACHE_ACCEL;
$wgSessionCacheType = CACHE_ACCEL;   // 见下文"会话坑"
```

**A/B 实测**（同机新旧镜像互切）：匿名文章页渲染 **0.429s → 0.193s**。

### ⚠️ 会话缓存的坑

切 `SessionCacheType = CACHE_ACCEL` 后，**机器人登录全面失效**（"Unable to continue login"）。根因：MediaWiki 对未 persist 的会话用 `WRITE_CACHE_ONLY` 写进程内缓存，跨 worker 即丢失；GET 方式获取 login token 的会话永不落库。

**修复**：会话走 `CACHE_DB`（跨重启稳健），机器人取 token 改用 **POST**（POST 触发会话持久化）：

```python
# meta=tokens 必须用 POST，GET 获取的 token 跨请求即失效
api.post(action='query', meta='tokens', type='login')
```

## 事故二：全文搜索越来越慢（FTS 膨胀）

**现象**：跨配置、跨通道（TCP/socket）恒定慢，FT 初始化（PROCESSLIST `State=FULLTEXT initialization`）5-15 秒。

**定位三板斧**：PHP 分段 error_log 打点 → PROCESSLIST 抓现场 → **看 FTS `.ibd` 文件大小**。结果：1489 行的 `searchindex` 表，FTS 增量段膨胀到 **104MB**。

**根因**：当天 100+ 次批量编辑，每次编辑对 si_text 是 DELETE+INSERT，InnoDB FTS 增量段只增不减。

**修复与运维约定**：

```sql
OPTIMIZE TABLE searchindex;   -- 104MB → 22MB，初始化回到 1.8-2.2s
```

> **批量导入/大量编辑后必须跑一次 `OPTIMIZE TABLE searchindex`**——这不是可选优化，是 FT 膨胀复发的确定性事件。

## 事故三：缓存层静默消失

**现象**：搜索优化成果一夜回退，无人改动配置。

**根因**：为加 MySQL socket 挂载 `docker compose up -d` 重建了 PHP 容器——前一天 pecl 装的 APCu 随容器消失。**容器重建 = 运行时状态清零。**

**修复**：派生镜像固化扩展（不再依赖运行时安装）：

```dockerfile
FROM 1panel-php:8.4.6
RUN install-php-extensions apcu && docker-php-ext-enable apcu
```

配套每日存活探针 cron，`apcu_fetch` 失败即写告警日志——别让缓存层再静默消失一天。

## 分层缓存全景

| 层 | 机制 | 失效方式 | 谁能清 |
|---|---|---|---|
| PHP 进程内 | APCu（MainCache/MessageCache） | 重启 fpm（模板改动需 `kill -USR2 1`，进程内有记忆化） | 运维 |
| 页面 | nginx fastcgi_cache（TTL 10min） | 删缓存目录；MW 的 purge **不会**联动 | 运维 |
| 边缘 | CDN（TTL 5min，遵循源站 Cache-Control） | CDN 控制台 Purge | 运维 |

经验：**改词条 → 清 fastcgi → 带随机参数验证渲染**；改 mustache 模板 → 还要 reload fpm；改 CDN 生效策略 → 控制台提交刷新。

---

- 上一篇：[01 · 整体架构](01-architecture.md) · 下一篇：[03 · nginx SNI 分流](03-nginx-sni-stream.md)
- 站点入口：<https://www.itswe.com>
