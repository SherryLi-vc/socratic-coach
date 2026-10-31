# socratic-coach（苏格拉底提问教练）

[![License: MIT](https://img.shields.io/github/license/SherryLi-vc/socratic-coach)](./LICENSE)

[English](./README.md) · **简体中文**

> 把「乱问」炼成「该问的那一句」：先问清，再动手。

通用的 Agent Skills skill，适用于任何能加载 `SKILL.md` 的 AI agent。当目标模糊、思路混乱或出现 XY 问题时，通过苏格拉底式追问与 5 Whys，按黄金四段逐步澄清背景、目标、已尝试和卡点，最终帮你形成一句高质量的问题定义，而不是过早给出方案。它是 grill-me 的前置。

- **需求锁死前不抢答**：即使被追问，也不推荐工具、代码或方案，也不提前半评手段 Y 的利弊。
- **每轮 1–2 个承重问题**：每个问题都能改变目标或卡点；能自行查明的事实自己查，不问用户。
- **剥离 XY 并追问 5 Whys**：指出手段（Y），追问真实目标（X），并指出逻辑跳跃。
- **黄金四段，先草案后终稿**：背景 / 目标 / 已尝试 / 卡点 → 先给未锁死的草案 → 用户确认后再给终稿。
- **进度提示与明确收尾**：每轮说明还缺什么；终稿以“本轮结束”收尾，默认推荐 grill-me，但不自动启动。
- **跟随你的语言**：跟随对话语言（未明确时使用 agent 默认语言，再回退到中文）；中文对话只使用中文标签。

## 快速开始 / 安装

仓库根目录本身就是 skill 文件夹。将其克隆或复制到 skills 目录，并确保文件夹名与 skill 的 `name` 一致（`socratic-coach`）。仓库包含一个 `SKILL.md`，没有脚本。

Codex、Cursor、Gemini CLI 和 OpenCode 都会读取的用户级共享目录：

```sh
git clone https://github.com/SherryLi-vc/socratic-coach.git ~/.agents/skills/socratic-coach
```

Claude Code（Cursor 和 OpenCode 也会读取）：

```sh
git clone https://github.com/SherryLi-vc/socratic-coach.git ~/.claude/skills/socratic-coach
```

Gemini CLI 的另一种安装方式：

```sh
gemini skills install https://github.com/SherryLi-vc/socratic-coach.git
```

项目级安装：将文件夹放在项目内的 `.agents/skills/socratic-coach/`（或 `.claude/skills/socratic-coach/`）下。其他能加载 `SKILL.md` 文件夹的宿主可复制整个文件夹，并保留同级文件。

### 调用方式

| 宿主 | 调用方式 |
|---|---|
| 所有宿主 | 描述匹配时自动加载 |
| Claude Code | `/socratic-coach` |
| Codex | `$socratic-coach` |
| Cursor | `/` 菜单 |
| Gemini CLI | 通过 activate_skill 流程加载 |

`/苏格拉底`、`/问清楚` 等中文触发词是由描述匹配的短语，并非每个宿主都保证支持的斜杠命令。

**兼容性：** [Agent Skills 规范](https://agentskills.io/specification)；[Claude Code](https://code.claude.com/docs/en/skills)；[OpenAI Codex](https://developers.openai.com/codex/skills)；[Cursor](https://cursor.com/docs/context/skills)；[Gemini CLI](https://geminicli.com/docs/cli/skills/)；[OpenCode](https://opencode.ai/docs/skills/)。

## 与 grill-me 的区别

| | **socratic-coach** | **grill-me / grilling** |
|---|---|---|
| 用户带来的是 | 模糊目标、手段导向的问题或一段意识流 | 需要具体化的计划或设计 |
| 每轮问题 | 1–2 个承重问题，不推荐方案 | 可探索完整决策空间，通常会推荐选项 |
| 成功标准 | 黄金四段澄清 → 精确的问题定义 | 设计决策达成、形成共同理解 → 可执行计划 |
| 确认前 | 不推荐工具、代码或方案，不提前半评 Y 的利弊 | 确认前不实现，但访谈时可以讨论选项 |
| 后续衔接 | 只指出 grill-me、brainstorming、需求或编码等后续 skill，不自动启动 | 通常继续进入规格、实现或 grill-with-docs |

一句话：**grill-me 把想法变成可执行计划；socratic-coach 把混乱的问题炼成正确的问题。** 需要拍板设计选择时，socratic-coach 会建议切换到 grill-me，而不会自行决策。

## 先用 socratic-coach，再用 grill-me

推荐流程是**先苏格拉底式澄清，再使用 grill-me**：

1. 想法仍不清楚，或一开始就在问“推荐个工具”时，先用 socratic-coach 把真实问题提炼成一句话。
2. 终稿会明确显示“本轮结束”，并默认推荐 grill-me 作为下一步。
3. 将澄清后的问题交给 grill-me，逐项确定设计选择并形成可执行计划。

跳过第一步，可能会把一个问错的问题回答得十分详细。如果问题本来就很清楚，可以直接使用 grill-me。

## 触发方式

- **自动触发：** `SKILL.md` 的 frontmatter 描述与困惑、工具推荐、XY 问题或“脑子乱了”等信号匹配时，agent 可以加载本 skill。
- **备选口令：** `/苏格拉底`、`/问清楚`。

## 语言

Skill 跟随当前对话语言。语言不明确时，使用 agent 配置的默认语言，未设置则回退到中文。语言只改变表达，不改变底层规则。

## 仓库结构

| 路径 | 说明 |
|---|---|
| [`SKILL.md`](./SKILL.md) | 可加载的 skill 指引，包含规则、流程、模板和自检 |
| [`docs/examples/`](./docs/examples/) | 示例对话：追问、草案和终稿 |
| [`docs/uat-summary.md`](./docs/uat-summary.md) | UAT 摘要占位；完整报告未公开 |
| [`CHANGELOG.md`](./CHANGELOG.md) | 版本与更名记录 |
| [`LICENSE`](./LICENSE) | MIT 许可证 |

## 核心行为速览

1. 核心需求确认前：不推荐工具、代码或方案，也不提前半评手段 Y 的利弊，即使被追问。
2. 每轮提出 1–2 个承重问题：每个问题都能改变目标或卡点。可自行查明的事实不占问题名额。
3. 澄清背景、目标、已尝试和卡点。先给出**未锁死的草案**，用户确认后再给终稿。
4. 每轮结束都显示进度，让用户知道还缺什么。
5. 终稿以**本轮结束**收尾：说明问清楚已完成，默认推荐 grill-me，并列出其他后续 skill 作为备选；不自动启动或加载其他 skill。
6. 面向用户的标签和术语跟随对话语言；中文对话不混用英文标签。

## 许可证

MIT © 2026 SherryLi-vc

完整规则和 U1–U12 验收清单见 [`SKILL.md`](./SKILL.md)。
