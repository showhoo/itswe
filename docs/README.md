# itswe 建站文档

[itswe.com](https://www.itswe.com)（铁路接触网知识库，MediaWiki）的完整建站实践。单 VPS、Docker 化、生产环境实测数据。

| # | 文档 | 一句话 |
|---|---|---|
| 01 | [整体架构](01-architecture.md) | 单 VPS 多站点共存：入口分流、容器拓扑、备份策略 |
| 02 | [MediaWiki 性能调优](02-mediawiki-performance.md) | 缓存分层实录：渲染 2.2×、FTS 膨胀治理 |
| 03 | [nginx SNI 分流](03-nginx-sni-stream.md) | 一个 443 端口服务多个 HTTPS 站点 |
| 04 | [国内 CDN 接入](04-cdn-edgeone.md) | EdgeOne 实测首屏 8× 提速与回源策略 |
| 05 | [Wiki SEO 工程实践](05-wiki-seo-practices.md) | 多引擎收录通道自动化 + AI 搜索适配 |
| 06 | [内容生产流水线](06-content-pipeline.md) | 512 词条的工业化生产与质检纪律 |

建议按编号顺序阅读；每篇可独立成篇。

相关仓库：[showhoo/ocs-calculators](https://github.com/showhoo/ocs-calculators)（计算器公式 TypeScript 库）。
