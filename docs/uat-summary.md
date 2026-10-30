# UAT 摘要（占位）

> 完整 UAT / 开源对照报告归档在内部路径 `/workspace/socratic-question-coach/`（见该目录 `INDEX.md`）。本文件仅公开摘要，不含自演全文。

| 项 | 内容 |
|---|---|
| Skill id（现行） | `socratic-coach`（曾用 `socratic-question-coach`） |
| 内部 UAT 日期 | 2026-10-29（Asia/Shanghai） |
| 剧本 U1–U6 | **6/6 Pass**（角色扮演） |
| 开源对照 B1–B5 | **5/5 Pass**（相对「炼问题、禁抢答」产品线更贴） |
| Go / No-Go | **Go**（有条件备注，非 Blocker） |
| 主要局限 | 自演非真人压力测；description 自动路由层未在无关会话实测 |

### 拍板要点（静态对照均落实）

- description 可命中自动触发；口令备选
- 锁死前禁工具/代码/方案/半评 Y
- 每轮 1–2 承重问；指出逻辑跳跃
- 终稿黄金四段；Attempts 可空标「尚未尝试」
- 锁死后可半评 Y；设计拍板只建议 grill-me；不自动派下游

### 待补（公开仓占位）

- [ ] 链到公开发布后的 commit / tag
- [ ] （可选）真人短测 U1+U5 摘要
- [ ] （可选）无口令自动触发抽测关闭 R4
