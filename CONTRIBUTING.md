# 贡献指南

感谢关注本仓库！三类内容的贡献方式不同，请对号入座。

## 1. 建站文档（docs/）—— 欢迎 Issue 与 PR

- 勘误（数据、配置、结论错误）或补充实践经验，请提 Issue；能直接改的欢迎提 PR
- 文档内容必须来自**生产环境实测**，引用数据给出可复核来源
- 红线：**不得**包含密钥、密码、内部 IP、非公开架构细节
- 中文写作为主，术语首次出现附英文；提交即表示同意以 CC BY-SA 4.0 授权

## 2. 词条内容（itswe.com 本体）—— 不走 GitHub

词条由站点内容流水线管理，不接受直接 PR。发现词条错误请：

- 通过 [投稿规范 / 联系页](https://www.itswe.com/contribute) 反馈，或
- 在本仓库提 Issue 并标注 `site-content`，由维护者转交编辑复核

## 3. 计算器公式 —— 去 ocs-calculators

公式库及其 TypeScript 测试在 [showhoo/ocs-calculators](https://github.com/showhoo/ocs-calculators)，Issue / PR 请到那边提。

## 本地写作

纯 Markdown，无需构建。提交前自查：

```bash
# 链接有效性（相对路径）
grep -oE '\]\([^)]+\)' docs/*.md   # 人工核对目标存在
```
