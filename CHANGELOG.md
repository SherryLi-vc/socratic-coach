# Changelog

## [0.2.0] — 2026-10-30

### Changed（真人测试反馈）

- 终稿新增【本轮结束】收尾：明说「问清楚这一步已完成」，默认推荐 grill-me 并说明接法，其余下游列为备选。
- 追问轮与草案末尾新增【进度】行，用户能看到还差几段、大约几轮。
- 对用户可见的段名与术语跟随当轮语言：中文会话用 背景 / 目标 / 已尝试 / 卡点，不再出现 Context、Blocker 等英文标签。
- README 写明本 skill 是 grill-me 的前置。
- 验收自检新增 U10–U12。

## [0.1.0] — 2026-10-29

### Renamed

- Skill id：`socratic-question-coach` → **`socratic-coach`**
- 本地路径：`/home/box/agent-data/workflows/socratic-coach/SKILL.md`
- 历史方案 / UAT 仍归档在 `/workspace/socratic-question-coach/`（见该目录 `INDEX.md`，索引已改指新 id）

### Added

- 公开仓最小骨架：README（vs grill-me）、MIT、示例对话、触发说明、UAT 摘要占位
- 硬规则加固：P0-1 可自查不占问名额；P0-2 只问承重问 / 早停；P0-3 锁死前禁半评 Y
- 验收自检扩至 U1–U9
- 语言：跟随用户当轮语言；不明则品牌默认语（未设置则中文）——已去掉五语种对照表

### Notes

- 内部 UAT（旧 id）：U1–U6 Go（角色扮演）；开源对照 B1–B5 Pass。公开仓仅嵌摘要占位，完整报告不随仓发布。
