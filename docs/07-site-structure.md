# 07 · 站点结构与内容地图

> [itswe.com](https://www.itswe.com) 建站文档 · 内容篇。这份地图回答三个问题：站上有什么栏目、每个栏目放什么、各有多少内容。计数与站内 [llms.txt](https://www.itswe.com/llms.txt) 同源（2026-09-17），随内容发布滚动更新。

itswe.com 是面向铁路接触网（OCS）从业者的中文专业知识库与线上工具平台，内容按 **12 大栏目** 组织，词条之间通过分类目录与内链形成网状知识结构。

## 栏目总览

| 栏目 | 公开条目 | 一句话说明 |
|---|---|---|
| [零部件库](https://www.itswe.com/Category:parts) | 107 | 按系统组成梳理零部件："装在哪里、起什么作用、如何选型" |
| [基础理论](https://www.itswe.com/Category:theory) | 46 | 讲清"为什么"：弓网耦合、受流质量、绝缘与附加导线原理 |
| [设计与计算](https://www.itswe.com/Category:design) | 24 | 张力弛度、锚段长度、跨距布置、限界校验等设计口径 |
| [施工与验收](https://www.itswe.com/Category:construction) | 21 | 施工工艺、安装精度控制、验收标准与常见质量问题 |
| [运维与检测](https://www.itswe.com/Category:operation) | 35 | 巡检项点、检测方法与周期、缺陷分级与处置流程 |
| [6C 检测体系](https://www.itswe.com/Category:6c) | 33 | 接触网运行检测监测体系各子系统的解读与数据应用 |
| [常见故障与案例库](https://www.itswe.com/Category:cases) | 42 | 脱敏处理后的典型故障分析与处置复盘 |
| [标准规范库](https://www.itswe.com/Category:standards) | 137 | 标准要点速查卡：国家/行业/国际/认证四子类，新旧对照 |
| [术语库](https://www.itswe.com/Category:glossary) | 58 | 易混淆专业名词的统一解释，消除"一名多说法" |
| [城轨供电与受流](https://www.itswe.com/Category:metro) | 49 | 城市轨道交通接触网专题，总览页 /metro/index + 7 个主题子分类（柔性/刚性/第三轨） |
| [在线题库](https://www.itswe.com/exam/) | 9,166 题 | 刷题、错题本、模拟卷与答案精选，服务端自动评分 |
| [工具与计算器](https://www.itswe.com/Category:tools) | 20 | 在线工程计算器，另有 20 个交互应用本体直接可用 |

全站合计 **709 页**（内容条目 639 + 分类页 49 + 计算器 20 + 首页 1，与 [/resources/counts.json](https://www.itswe.com/resources/counts.json) 同源；wiki sitemap 子图 689 条 = 内容条目 + 分类页 + 首页）。

## 分类树

分类采用两级结构：一级栏目（L1）→ 主题子类（L2）。中文名以站内分类导航为准。

### 零部件库（parts，107 篇 / 13 子类）

接触网系统的物理构成，按部件功能归位：

| 子类 | 主题 |
|---|---|
| [接触线](https://www.itswe.com/Category:parts/contact-wire) | 各型号接触线（CTAH/CTMH/CTS 系列等）的结构与参数 |
| [承力索](https://www.itswe.com/Category:parts/messenger-wire) | 承力索与绞线载体的选型与性能 |
| [吊弦](https://www.itswe.com/Category:parts/dropper) | 载流型/整体吊弦的规格与安装 |
| [定位装置](https://www.itswe.com/Category:parts/registration) | 定位器、定位管与拉出值体系 |
| [张力补偿装置](https://www.itswe.com/Category:parts/tensioning) | 棘轮、弹簧等补偿装置的形式与补偿行程 |
| [绝缘子](https://www.itswe.com/Category:parts/insulator) | 棒式、悬式与复合绝缘子的爬距与污秽等级 |
| [分段绝缘器](https://www.itswe.com/Category:parts/section-insulator) | 分段、分相绝缘器与锚段关节配合 |
| [线岔](https://www.itswe.com/Category:parts/crossing) | 线岔交叉与无交叉转换 |
| [刚性悬挂](https://www.itswe.com/Category:parts/rigid) | 城轨刚性悬挂的汇流排与附件 |
| [支持结构](https://www.itswe.com/Category:parts/structure) | 腕臂、横梁与支柱支持体系 |
| [基础](https://www.itswe.com/Category:parts/foundation) | 支柱基础与地脚螺栓 |
| [开关设备](https://www.itswe.com/Category:parts/switch) | 隔离开关与负荷开关 |
| [辅助部件](https://www.itswe.com/Category:parts/auxiliary) | 电连接等辅助连接件 |

### 基础理论（theory，46 篇 / 4 子类）

- [弓网关系](https://www.itswe.com/Category:theory/pantograph-ocs)：受电弓与接触网的动态耦合、离线率与受流质量
- [附加导线理论](https://www.itswe.com/Category:theory/auxiliary)：正馈线、保护线、回流线的电气原理
- [复合绝缘子理论](https://www.itswe.com/Category:theory/insulator)：伞裙体系与污闪机理
- [国际系统谱系](https://www.itswe.com/Category:theory/systems)：接触网制式的国际谱系对照

### 运维与检测（operation，35 篇 / 3 子类）

- [病害管理](https://www.itswe.com/Category:operation/defects)：缺陷分级、整治流程
- [应急管理](https://www.itswe.com/Category:operation/emergency)：故障抢修与应急响应
- [季节性整治](https://www.itswe.com/Category:operation/seasonal)：覆冰、大风、鸟害等季节项点

### 术语库（glossary，58 篇 / 6 子类）

几何参数 / 悬挂与补偿 / 磨耗与材料 / 受电弓与受流 / 供电方式与回流 / 运维检测——六个主题子类各司其职，词条给出定义、中英对照与上下文用法。

### 标准规范库（standards，137 篇 / 4 子类）

[国家标准](https://www.itswe.com/Category:standards/national)（GB/G B/T）/ [行业标准](https://www.itswe.com/Category:standards/industry)（TB/T 等）/ [国际标准](https://www.itswe.com/Category:standards/international)（IEC/EN）/ [认证与体系](https://www.itswe.com/Category:standards/certification)。标准卡片提炼适用条款与关键数值，数值逐条溯源到标准条文。

### 城轨供电与受流（metro，49 篇 / 7 子类）

城轨直流牵引供电与受流专题，入口为分类总览页 [/metro/index](https://www.itswe.com/metro/index)：

- [设计与几何](https://www.itswe.com/Category:metro/design)：刚性/柔性悬挂型式、刚柔过渡与城轨几何参数
- [第三轨与受流](https://www.itswe.com/Category:metro/third-rail)：接触轨体制、四轨回流与集电靴受流界面
- [供电与回流](https://www.itswe.com/Category:metro/power)：直流供电制式、回流回路、杂散电流防护与接地防雷
- [装置与部件](https://www.itswe.com/Category:metro/parts)：汇流排组件、城轨绝缘子、电分段与城轨受电弓
- [建设与调试](https://www.itswe.com/Category:metro/construction)：冷滑试验、送电验收、夜间天窗作业与车辆段接触网
- [运维与检修](https://www.itswe.com/Category:metro/operation)：巡检检测、运维制度、应急抢修与覆冰处置
- [新制式与趋势](https://www.itswe.com/Category:metro/trends)：无接触网供电、有轨电车接触网等演进方向

## 在线题库与模拟考试（/exam/）

题库是独立于 MediaWiki 的自研 PHP + MySQL 判分系统，与词条体系互为印证：

| 板块 | 题量 |
|---|---|
| 电气化铁路接触网 | 5,542 |
| 城轨接触网 | 3,624 |
| **合计** | **9,166** |

- **题型**：单选 / 多选 / 判断，逐题附解析与标准依据
- **功能**：知识点刷题、只刷错题（错题本）、9 套模拟卷（5 套职业技能等级卷 + 铁路/城轨标准卷与快练卷，标准卷 120 题 / 快练卷 50 题）
- **答案精选**：[/exam/answers](https://www.itswe.com/exam/answers)（铁路）与 [/exam/answers/metro](https://www.itswe.com/exam/answers/metro)（城轨）各 50 道高频题的答案与解析，逐题标注依据标准，免登录在线查阅
- **判分**：服务端自动评分、即时出成绩单，登录后进度与错题本留存
- **定位**：对标接触网工职业技能鉴定理论机考的日常自测与培训工具

## 计算器的双形态

每台计算器有两处入口，互为补充：

- **原理说明页**：`/tools/calculator-<slug>`（词条型文档，讲公式来源与适用条件，归入 [Category:tools](https://www.itswe.com/Category:tools)）
- **交互应用本体**：`/calculator/<slug>/`（纯前端实时计算，无需登录，支持 PWA 安装）

公式库的 TypeScript 测试套件开源在 [showhoo/ocs-calculators](https://github.com/showhoo/ocs-calculators)（npm 同名包）。

## 说明页群与发现层

说明页：关于本站 / 免责声明 / 隐私政策 / 联系我们 / 版权与引用 / 社区规范 / 投稿规范 / ExamReturn（题库成绩认证说明）。

面向搜索引擎与 AI 的机器发现层（详见 [05 · Wiki SEO 工程实践](05-wiki-seo-practices.md)）：

- `sitemap.xml`：wiki + calculator + exam 三子图，另附百度扁平版
- `llms.txt` / `llms-full-*.txt`（26 个全文分卷）/ `llms-changes.json` 增量清单
- REST API：`/rest.php/v1/page/<slug>` 恒返回 JSON；对短链 URL 发送 `Accept: text/markdown` 返回 wikitext 源（兼容保留）
- wikitext 直出端点：`GET /md/<slug>` 恒返回 `text/x-wiki`——为每个 slug 提供独立 URL，使 wikitext 响应拥有独立的 EdgeOne 缓存键（内容协商与 HTML 共享缓存键，命中缓存可能返回 HTML）；机器抓取以 `/md/<slug>` 或 `?action=raw` 为准

## 规划中

- **FAQ 问答栏目**：已上线 58 页高频问答（llms.txt 同源，2026-09-17），后续持续扩容
- **题库扩容**：两板块题量与模拟卷持续补充
- 内容季度刷新：数据与栏目计数随发布滚动更新
