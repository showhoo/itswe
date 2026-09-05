# itswe · 思维接触网百科 — 铁路接触网（OCS）开放知识库 & 开源建站文档

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](./LICENSE)
![Status](https://img.shields.io/badge/%E7%8A%B6%E6%80%81-%E6%8C%81%E7%BB%AD%E6%9B%B4%E6%96%B0-brightgreen)

**[www.itswe.com](https://www.itswe.com)** 是面向铁路接触网（Overhead Contact System，OCS）工程师、院校师生与铁路爱好者的中文开放知识库：

- 📖 **512+ 系统化词条** —— 接触网悬挂、张力、吊弦、风偏、磨耗、覆冰、波速传播等主题，按分类体系组织，数值全部溯源到标准条文
- 🧮 **12 个在线工程计算器** —— 张力/弛度、吊弦、风偏、磨耗、载流量、覆冰、波速、电压降等，浏览器直接计算、无需登录
- 📜 **标准规范速查** —— GB/T、TB/T 系列接触网标准的关键数值速查卡，随新标准发布同步更新
- 📱 **PWA 支持** —— 计算器与术语可安装到手机离线使用

> **English**: [itswe.com](https://www.itswe.com) is a Chinese open knowledge base for railway **overhead contact line (OCL / OCS)** engineering — 512+ structured articles, 12 interactive calculators, and quick-reference cards for Chinese national (GB/T) and railway industry (TB/T) standards. Free, no login required, installable as a PWA.

## 在线计算器

全部计算器见 [itswe.com/Category:tools](https://www.itswe.com/Category:tools)，包括：

| 计算器 | 链接 |
|---|---|
| 张力与弛度 | [calculator/tension](https://www.itswe.com/calculator/tension/) |
| 吊弦 | [calculator/dropper](https://www.itswe.com/calculator/dropper/) |
| 风偏与绝缘间隙 | [calculator/wind](https://www.itswe.com/calculator/wind/) |
| 接触线磨耗 | [calculator/wear](https://www.itswe.com/calculator/wear/) |
| 覆冰 | [calculator/icing](https://www.itswe.com/calculator/icing/) |
| 载流量 | [calculator/ampacity](https://www.itswe.com/calculator/ampacity/) |
| 波速传播 | [calculator/wavespeed](https://www.itswe.com/calculator/wavespeed/) |
| 电压降 | [calculator/voltage-drop](https://www.itswe.com/calculator/voltage-drop/) |
| 悬挂受力 | [calculator/force](https://www.itswe.com/calculator/force/) |
| 曲线区段拉出值 | [calculator/curve-stagger](https://www.itswe.com/calculator/curve-stagger/) |

计算器公式库的 TypeScript 测试套件见姊妹仓库 [showhoo/ocs-calculators](https://github.com/showhoo/ocs-calculators)（零依赖纯函数 + 152 项单元测试）。

## 开源建站文档

本仓库同时开源 itswe.com 的**完整建站实践**——单服务器承载 MediaWiki 知识库的高性能、低成本方案，全部数据来自真实生产环境实测：

| 文档 | 内容 |
|---|---|
| [01 · 整体架构](docs/01-architecture.md) | 单 VPS 多站点共存：入口分流、容器拓扑、备份策略 |
| [02 · MediaWiki 性能调优](docs/02-mediawiki-performance.md) | 缓存分层实录：页面渲染 **2.2×** 提速、FTS 索引膨胀治理 |
| [03 · nginx SNI 分流](docs/03-nginx-sni-stream.md) | 一个 443 端口服务多个 HTTPS 站点（`ssl_preread` 实战） |
| [04 · 国内 CDN 接入](docs/04-cdn-edgeone.md) | EdgeOne 接入与回源策略，首屏 **0.97s → 0.12s（8×）** 实测 |
| [05 · Wiki SEO 工程实践](docs/05-wiki-seo-practices.md) | sitemap / llms.txt / OG 图自动生成 / 百度收录通道 |
| [06 · 内容生产流水线](docs/06-content-pipeline.md) | 512 词条的工业化生产、质检与发布纪律 |

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
