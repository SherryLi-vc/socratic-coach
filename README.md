# socratic-coach（苏格拉底提问教练） / Socratic Coach

**中文｜**面向 Grok Bot 与 Cursor 的 AI Agent Skill。当目标模糊、思路混乱或出现 XY 问题时，通过苏格拉底式追问、5 Whys 与黄金圈，逐步澄清背景、目标、已尝试和卡点。它每轮只问 1–2 个承重问题，在核心需求确认前不抢答、不推荐工具或方案，最终帮助用户形成一句高质量的问题定义。

**English｜**An AI agent skill for Grok Bot and Cursor. When a goal is vague, thinking is tangled, or an XY problem appears, it uses Socratic questioning, the 5 Whys, and the Golden Circle to clarify context, goals, attempts, and blockers. It asks only 1–2 high-leverage questions per turn and avoids jumping to tools or solutions before the core need is confirmed. The outcome is a clear, high-quality problem statement—ready for the next step, not a premature solution.

**终点是高水平问题，不是可动手方案。** 核心需求锁死前禁止抢答与半评手段 Y。

曾用 id：`socratic-question-coach`（已 rename，见 [CHANGELOG](./CHANGELOG.md)）。

## 与 grill-me 的定位

| | **socratic-coach** | **grill-me / grilling** |
|---|---|---|
| 用户带来的是 | 模糊意图 / 手段提问 / 意识流 | 一个要压实的计划或设计 |
| 每轮问题 | 1–2 个**承重问**，不带方案推荐 | 可问满 frontier，且常带 ➡️ 推荐答案 |
| 成功标准 | 黄金四段锁死 → **高水平问题句** | 设计树走完 + 共享理解 → **可动手方案** |
| 锁死前 | 禁工具 / 代码 / 方案 / 半评 Y | 确认前不实现，但访谈中可推荐选项 |
| 下游 | 只**点名** grill-me / brainstorming / Requirement / Coding | 常接 to-spec / 实现 / grill-with-docs |

一句话：**grill-me 把「想法」烤成「可动手的方案」；本 skill 把「乱问」炼成「该问的那一句」。**

需要拍板设计树时，本 skill **只建议切换 grill-me**，不在内部完成选型。

### 本 skill 是 grill-me 的前置

推荐的用法是**先苏格拉底、后 grill-me**：

1. 想法还乱，或一开口就是「推荐个工具」时，先用本 skill，把真正要解决的问题锁成一句话。
2. 终稿最后会出现【本轮结束】，明确告诉用户「问清楚这一步已完成」，并默认推荐 grill-me 作为下一步。
3. 用户把这句问题交给 grill-me，逐个拍板设计选择，烤成可动手方案。

跳过第 1 步直接 grill，常会把一个问错了的问题定得很细。想法本来就清楚时，可以直接用 grill-me。

## 触发

- **自动**：`SKILL.md` frontmatter `description` 命中后可由 agent 加载（混乱 / 推荐工具 / XY /「脑子乱了」等）。
- **口令（备选）**：`/苏格拉底`、`/问清楚`。

语言：跟随用户当轮语言；不明确时用品牌 agent 默认语（未设置则中文）。语言只改表达，不改硬规则。

## Install

将本仓 `SKILL.md` 拷入 agent 的 skills/workflows 为 `socratic-coach/SKILL.md`，或通过 bot 的 skill 安装器导入。

```text
workflows/
  socratic-coach/
    SKILL.md
```

## 仓库结构

| 路径 | 说明 |
|---|---|
| [`SKILL.md`](./SKILL.md) | 可加载 skill 正文（硬规则、流程、模板、验收自检） |
| [`docs/examples/`](./docs/examples/) | 示例对话（追问 / 草案 / 终稿） |
| [`docs/uat-summary.md`](./docs/uat-summary.md) | UAT 摘要占位（完整报告见内部归档） |
| [`CHANGELOG.md`](./CHANGELOG.md) | 版本与 rename 记录 |
| [`LICENSE`](./LICENSE) | MIT |

## 核心约定（摘要）

1. 锁死前：禁工具/代码/方案推荐；禁半评 Y 利弊（即使用户追问）。
2. 每轮 1–2 个承重问（会改变 Goal 或 Blocker）；可自查事实不占名额。
3. 黄金四段：背景 / 目标 / 已尝试 / 卡点（英文会话用 Context / Goal / Attempts / Blocker）→ 先【草案·未锁死】，用户确认后终稿。
4. 每轮末尾有【进度】行，用户随时知道还差几段。
5. 终稿以【本轮结束】收尾：明说已完成，默认推荐 grill-me，其余下游作为备选；不自动派下游、不自动加载下游 skill。
6. 对用户可见的段名与术语跟随当轮语言，中文会话不夹英文标签。

完整规则与验收表 U1–U12 见 `SKILL.md`。

## License

MIT © 2026 SherryLi-vc
