# 05 · Wiki 站 SEO 工程实践（含 AI 搜索引擎适配）

> [itswe.com](https://www.itswe.com) 建站文档 · SEO 篇。中文新站冷启动的完整收录通道建设：从"上线 10 天 Google 只抓了 35 次"到多引擎稳定收录，每个通道都给出自动化实现。

## 收录通道全景

| 通道 | 实现 | 频率 |
|---|---|---|
| Google | GSC 提交 sitemap + 高价值页"请求编入索引" | 上线时 + 重大更新 |
| 百度 | 普通收录 API 每日推送（配额 10 条/天，优先级队列轮换） | 每日 cron |
| 通用 | sitemap.xml 每小时增量生成 | 每小时 cron |
| AI 搜索 | llms.txt（全文索引）+ robots 声明 | 随内容更新 |
| 社交/IM | OG 图自动生成（每页一张品牌卡） | 随内容更新 |

## sitemap：每小时增量

脚本化生成 sitemapindex + 子表（单表 ≤5 万 URL），每小时 cron 增量比对，新增页自动进入。GSC 报"无法抓取 sitemap"多为报表延迟——用日志验证真实抓取再下结论。

## 百度：配额敏感的每日推送

百度普通收录配额极小（新站 10 条/天）。策略：

1. **优先级队列**：首页/顶级栏目页（P0）> 一级分类（P1）> 内容页（P2），新页优先
2. **配额用尽按最久未推轮换**，474 条存量约 53 天推完
3. 状态文件记录已推 URL 防重复；配额超限报错（over quota）要识别，避免浪费当日配额

```python
# 推送接口：token 按站点独立，同一 token 服务不同站点配额分开
requests.post(f'http://data.zz.baidu.com/urls?site={site}&token={token}',
              data=urls, headers={'Content-Type': 'text/plain'})
```

## llms.txt：面向 AI 搜索的站点声明

传统 SEO 之外，AI 搜索引擎（ChatGPT/Perplexity 等）正在成为内容入口。itswe.com 的做法：

- 维护 `llms.txt`：站点简介 + 全部内容页的标题/摘要索引（500+ 页）
- robots.txt 里声明内容使用偏好（AIPREF 信号行）：允许抓取引用、要求署名

> 注意：robots.txt 中非标准指令（如 `Content-Usage:`）对 Google 无害——解析器跳过未知行，Allow/Disallow/Sitemap 照常生效。

## OG 图自动生成

每篇词条自动生成一张 1200×630 品牌分享卡（标题 + 分类 + 品牌视觉），分享到社交/IM 的点击率显著高于无图链接。实现：内容发布流水线的后置步骤，模板渲染 + 批量出图，新页自动补产。

## 技术层规范

- **canonical** 每页自指，变体 URL 收敛
- **title 后缀守卫**：工具层追加站点名后缀时判重，防"标题双拼"
- **面包屑**与分类体系一致（注意 wiki 直连计数与页面列表计数是两个口径，别混用）
- **短描述**：description 从正文摘要提取，80+ 字符保证搜索结果摘要完整

## 内容层规范（比技术层更重要）

- **数值溯源**：关键数值必须落到标准条文，站外标准号先过人工白名单再引用
- **参考资料只写可核验来源**：来源名 + 访问日期，不挂不可回溯的超链
- **禁词机检**：拒绝"全文如下/摘自百度百科"式内容，逐页 lint 不过不发布
- 冷启动耐心：新站前 10 天 Google 只抓 35 次是正常的；sitemap + GSC + 少量外链后，2-4 周内进入稳定抓取

## 效果度量

- 日志按 UA 分类统计爬虫构成（Googlebot / Baiduspider / 必应 / 社交爬虫各占多少）
- GSC 展示/点击按页面聚合，找"有展示无点击"的页面改 title/description
- 品牌 SERP 监控：官网 + GitHub 仓库多占位（见本仓库的存在意义）

---

- 上一篇：[04 · 国内 CDN 接入](04-cdn-edgeone.md) · 下一篇：[06 · 内容生产流水线](06-content-pipeline.md)
- 站点入口：<https://www.itswe.com>
