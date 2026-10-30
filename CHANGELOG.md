# Changelog

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
