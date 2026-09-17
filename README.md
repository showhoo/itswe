# itswe · 思维接触网百科 — 铁路接触网（OCS）开放知识库 & 开源建站文档

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](./LICENSE)
![Status](https://img.shields.io/badge/%E7%8A%B6%E6%80%81-%E6%8C%81%E7%BB%AD%E6%9B%B4%E6%96%B0-brightgreen)

**[www.itswe.com](https://www.itswe.com)** 是面向铁路接触网（Overhead Contact System，OCS）工程师、院校师生与铁路爱好者的中文开放知识库：

- 📖 **639 篇系统化词条（全站 709 页）** —— 接触网悬挂、张力、吊弦、风偏、磨耗、覆冰、波速传播等主题，按 12 大栏目分类体系组织，数值全部溯源到标准条文
- 📝 **在线题库 9,166 题** —— 电气化铁路（5,542）与城轨（3,624）两大板块：知识点刷题、错题本、9 套模拟卷（标准卷 120 题 / 快练卷 50 题）与铁路、城轨试题答案精选页（各 50 道高频题，免登录查阅），服务端自动评分
- 🧮 **20 个在线工程计算器** —— 张力/弛度、吊弦、风偏、磨耗、载流量、覆冰、波速、电压降等，浏览器直接计算、无需登录
- 📜 **标准规范速查** —— GB/T、TB/T 系列接触网标准的关键数值速查卡，随新标准发布同步更新
- 📱 **PWA 支持** —— 计算器与术语可安装到手机离线使用

> **English**: [itswe.com](https://www.itswe.com) is a Chinese open knowledge base for railway **overhead contact line (OCL / OCS)** engineering — 639 structured articles (709 pages), a 9,166-question online exam bank for railway & metro OCS, 20 interactive calculators, and quick-reference cards for Chinese national (GB/T) and railway industry (TB/T) standards. Free, no login required, installable as a PWA.

## 在线计算器

全部计算器见 [itswe.com/Category:tools](https://www.itswe.com/Category:tools)，包括：

| 计算器 | 链接 |
|---|---|
| 张力-温度安装曲线生成器 | [calculator/tension](https://www.itswe.com/calculator/tension/) |
| 弓网接触力统计评价 | [calculator/force](https://www.itswe.com/calculator/force/) |
| 载流量修正与短路热稳定 | [calculator/ampacity](https://www.itswe.com/calculator/ampacity/) |
| 吊弦长度计算 | [calculator/dropper](https://www.itswe.com/calculator/dropper/) |
| 风偏限界校验 | [calculator/wind](https://www.itswe.com/calculator/wind/) |
| 接触线磨耗率计算 | [calculator/wear](https://www.itswe.com/calculator/wear/) |
| 接触线参数速查 | [calculator/copper](https://www.itswe.com/calculator/copper/) |
| 补偿行程计算 | [calculator/stroke](https://www.itswe.com/calculator/stroke/) |
| 波速利用率计算 | [calculator/wavespeed](https://www.itswe.com/calculator/wavespeed/) |
| 电压降校核 | [calculator/voltage-drop](https://www.itswe.com/calculator/voltage-drop/) |
| 曲线拉出值综合偏移校核 | [calculator/curve-stagger](https://www.itswe.com/calculator/curve-stagger/) |
| 覆冰荷载校核 | [calculator/icing](https://www.itswe.com/calculator/icing/) |
| 锚段长度计算 | [calculator/anchor-length](https://www.itswe.com/calculator/anchor-length/) |
| b 值计算 | [calculator/bvalue](https://www.itswe.com/calculator/bvalue/) |
| 腕臂预配计算 | [calculator/cantilever](https://www.itswe.com/calculator/cantilever/) |
| 爬电距离校核 | [calculator/creepage](https://www.itswe.com/calculator/creepage/) |
| 软横跨负载计算 | [calculator/cross-span](https://www.itswe.com/calculator/cross-span/) |
| 支柱容量选型 | [calculator/pole-capacity](https://www.itswe.com/calculator/pole-capacity/) |
| 弛度-张力互算 | [calculator/sag](https://www.itswe.com/calculator/sag/) |
| 定位器坡度计算 | [calculator/steady-arm](https://www.itswe.com/calculator/steady-arm/) |

计算器公式库的 TypeScript 测试套件见姊妹仓库 [showhoo/ocs-calculators](https://github.com/showhoo/ocs-calculators)（零依赖纯函数 + 218 项单元测试，npm 包 ocs-calculators v0.3.0）。

## 站点结构与栏目

内容按 **12 大栏目**组织（条目数与站内 [llms.txt](https://www.itswe.com/llms.txt) 同源，2026-09-17）：

| 栏目 | 条目 | 栏目 | 条目 |
|---|---|---|---|
| [零部件库](https://www.itswe.com/Category:parts) | 107 | [常见故障与案例库](https://www.itswe.com/Category:cases) | 42 |
| [基础理论](https://www.itswe.com/Category:theory) | 46 | [标准规范库](https://www.itswe.com/Category:standards) | 137 |
| [设计与计算](https://www.itswe.com/Category:design) | 24 | [术语库](https://www.itswe.com/Category:glossary) | 58 |
| [施工与验收](https://www.itswe.com/Category:construction) | 21 | [城轨供电与受流](https://www.itswe.com/Category:metro) | 49 |
| [运维与检测](https://www.itswe.com/Category:operation) | 35 | [在线题库](https://www.itswe.com/exam/) | 9,166 题 |
| [6C 检测体系](https://www.itswe.com/Category:6c) | 33 | [工具与计算器](https://www.itswe.com/Category:tools) | 20 |

完整分类树与各栏目内容说明见 **[docs/07 · 站点结构与内容地图](docs/07-site-structure.md)**。

## 开源建站文档

本仓库同时开源 itswe.com 的**完整建站实践**——单服务器承载 MediaWiki 知识库的高性能、低成本方案，全部数据来自真实生产环境实测：

| 文档 | 内容 |
|---|---|
| [01 · 整体架构](docs/01-architecture.md) | 单 VPS 多站点共存：入口分流、容器拓扑、备份策略 |
| [02 · MediaWiki 性能调优](docs/02-mediawiki-performance.md) | 缓存分层实录：页面渲染 **2.2×** 提速、FTS 索引膨胀治理 |
| [03 · nginx SNI 分流](docs/03-nginx-sni-stream.md) | 一个 443 端口服务多个 HTTPS 站点（`ssl_preread` 实战） |
| [04 · 国内 CDN 接入](docs/04-cdn-edgeone.md) | EdgeOne 接入与回源策略，首屏 **0.97s → 0.12s（8×）** 实测 |
| [05 · Wiki SEO 工程实践](docs/05-wiki-seo-practices.md) | sitemap / llms.txt / OG 图自动生成 / 百度收录通道 |
| [06 · 内容生产流水线](docs/06-content-pipeline.md) | 百科词条的工业化生产、质检与发布纪律 |
| [07 · 站点结构与内容地图](docs/07-site-structure.md) | 12 大栏目、两级分类树与在线题库：写什么、在哪、有多少 |

## 内容规范

itswe.com 的词条执行严格的内容纪律，这也是本知识库区别于一般百科的价值所在：

- **数值溯源**：所有关键数值必须落到标准条文（如 GB/T 12971.1、TB/T 2809、EN 50149），并经人工白名单校验
- **参考资料只写可核验来源**（来源名 + 访问日期），拒绝不可回溯的"网上说的"
- **原创撰写**：拒绝搬运百科内容，词条按统一骨架生成、逐页机检 + 人工复核

## 版权与引用

词条与文档内容以 **CC BY-SA 4.0** 授权发布：转载请注明出处并以相同方式共享。工程数据请以现行有效标准原文为准。

## 赞助

本知识库的建设与维护感谢以下赞助者的支持：

**[河南创为铁路器材有限公司](https://www.chuangwit.com)**

## 相关项目

- [showhoo/ocs-calculators](https://github.com/showhoo/ocs-calculators) —— 计算器公式 TypeScript 库（npm: `ocs-calculators`）
- 官网：<https://www.itswe.com>
