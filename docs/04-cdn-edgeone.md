# 04 · 国内 CDN 接入：腾讯云 EdgeOne 实测（首屏 8× 提速）

> [itswe.com](https://www.itswe.com) 建站文档 · CDN 篇。海外源站的中文站点接入国内 CDN 的完整实录：接入方式、缓存策略、实测数据、以及日志口径的变化。

## 背景

源站在海外，国内用户直连的首屏瓶颈在跨境链路。目标：国内访客就近命中，海外访客不受影响，源站配置改动最小。

## 实测数据（国内联通宽带直连）

| 场景 | TLS 握手 | 首字节 TTFB | 总耗时 |
|---|---|---|---|
| 直连海外源站（接入前） | ~0.35s | ~0.5s | **0.97s** |
| CDN 边缘命中（接入后） | **0.06s** | **0.097s** | **0.12s** |
| CDN 回源未命中 | — | ~0.8s | ~1.0s |

首屏 **8× 提速**；未命中场景与直连相当（回源海外是固有往返，由缓存 TTL 摊薄）。

## 接入方式

CNAME 接入（子域模式）：DNS 处 `www` CNAME 指向 EdgeOne 分配的接入域名，EdgeOne 回源到真实源站 IP。

缓存策略核心一条：**EdgeOne 遵循源站 Cache-Control**。

```nginx
# 站点 vhost：HTML 页面短缓存，静态资源长缓存
add_header Cache-Control "public, max-age=300";              # 页面
location ~* \.(css|js|png|svg|woff2?)$ {
    add_header Cache-Control "public, max-age=604800";       # 静态 7 天
}
```

验证是否生效：响应头出现 `EO-Cache-Status: HIT`（命中）/ `MISS`（未命中）。

## 回源与缓存失效的联动

关键认知：**源站清缓存 ≠ CDN 清缓存**。MediaWiki 词条更新后的完整失效链：

```
编辑词条 → (可选)清源站 fastcgi_cache → CDN 侧等 TTL(300s) 或控制台提交 Purge
```

工程实践：

- 页面 TTL 300s：普通更新等 5 分钟自然过期，可接受
- 急更（纠错、下线内容）：EdgeOne 控制台提交 URL 刷新，分钟级生效
- 验证渲染：带随机查询参数的 URL 会穿透 CDN 到源站，是验证"源站真实状态"的万能方法

## 日志口径的变化（容易踩的坑）

接入 CDN 后，源站日志的 `remote_addr` 变成 **EdgeOne 节点 IP**，真实访客 IP 在 `X-Forwarded-For`：

```nginx
# 只信任 CDN 官方公布的回源网段（EdgeOne 控制台「回源 IP 段」页面可查）。
# 切勿写成 0.0.0.0/0——那等于允许任意来源伪造 X-Forwarded-For，
# 会污染统计日志、绕过基于 IP 的限速与封禁。
set_real_ip_from <EdgeOne回源网段-1>;
set_real_ip_from <EdgeOne回源网段-2>;
real_ip_header X-Forwarded-For;
real_ip_recursive on;
```

对应地，日志分析脚本要改口径：

- 独立访客统计：优先取 XFF 第一段（浏览器直访场景无 XFF 时回退 remote_addr）
- UA 不变：爬虫（如 Facebook 的 meta-webindexer）经 CDN 回源时 UA 保留，可以继续按 UA 分类
- 防刷限速：按 remote_addr 限速会误伤（整个节点 IP 是一个"访客"），需按还原后的真实 IP

## 效果验证清单

1. `nslookup` 确认域名 CNAME 到 EdgeOne 节点
2. 响应头 `EO-Cache-Status: HIT`（国内访问）
3. 海外访问路径不受影响（直连或回源正常）
4. 源站日志 XFF 口径正确
5. 词条更新后 5 分钟内全网可见（或 Purge 后立即）

---

- 上一篇：[03 · nginx SNI 分流](03-nginx-sni-stream.md) · 下一篇：[05 · Wiki SEO 工程实践](05-wiki-seo-practices.md)
- 站点入口：<https://www.itswe.com>
