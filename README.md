# socratic-coach

[![License: MIT](https://img.shields.io/github/license/SherryLi-vc/socratic-coach)](./LICENSE)

**English** · [简体中文](./README.zh-CN.md)

> Turn a muddled question into the right question — before anyone jumps to a solution.

A general-purpose Agent Skills skill for any agent that can load a `SKILL.md`. When a goal is vague, thinking is tangled, or an XY problem appears, it uses Socratic questioning and the 5 Whys to clarify context, goals, attempts, and blockers (the four-part frame). The outcome is a clear, high-quality problem statement, ready for the next step, not a premature solution. It is designed to run before grill-me.

- **No answers before the need is locked**: No tools, code, solution recommendations, or partial pros-and-cons of a proposed Y, even when asked.
- **1–2 load-bearing questions per turn**: Each question must be able to change the Goal or Blocker; self-checkable facts are looked up, not asked.
- **XY stripping and 5 Whys**: Names the means (Y), asks for the real goal (X), and points out logic jumps.
- **Four-part frame, draft first**: Context / Goal / Attempts / Blocker → a draft, not yet locked → the final version only after you confirm.
- **Progress line and a clear ending**: Every turn shows what is still missing; the final ends with "Round complete" and recommends grill-me by default, without launching it.
- **Follows your language**: Matches the conversation language (falls back to the agent's default, then Chinese); Chinese conversations use Chinese labels only.

## Quick start / Install

The repository root is the skill folder. Clone or copy it into a skills directory and keep the folder name equal to the skill `name` (`socratic-coach`). It contains one `SKILL.md` and no scripts.

Shared user-level path read by Codex, Cursor, Gemini CLI, and OpenCode:

```sh
git clone https://github.com/SherryLi-vc/socratic-coach.git ~/.agents/skills/socratic-coach
```

Claude Code (also read by Cursor and OpenCode):

```sh
git clone https://github.com/SherryLi-vc/socratic-coach.git ~/.claude/skills/socratic-coach
```

Gemini CLI alternative:

```sh
gemini skills install https://github.com/SherryLi-vc/socratic-coach.git
```

Project-level: put the folder under `.agents/skills/socratic-coach/` (or `.claude/skills/socratic-coach/`) in your repository. Other hosts that load `SKILL.md` folders can use a copy of the whole folder, keeping sibling files.

### How to invoke

| Host | Invocation |
|---|---|
| All hosts | Auto-load when the description matches |
| Claude Code | `/socratic-coach` |
| Codex | `$socratic-coach` |
| Cursor | `/` menu |
| Gemini CLI | Loads via its activate_skill flow |

Chinese trigger phrases such as `/苏格拉底` and `/问清楚` are phrases matched by the description; they are not guaranteed slash commands in every host.

**Compatibility:** [Agent Skills specification](https://agentskills.io/specification); [Claude Code](https://code.claude.com/docs/en/skills); [OpenAI Codex](https://developers.openai.com/codex/skills); [Cursor](https://cursor.com/docs/context/skills); [Gemini CLI](https://geminicli.com/docs/cli/skills/); [OpenCode](https://opencode.ai/docs/skills/).

## How it differs from grill-me

| | **socratic-coach** | **grill-me / grilling** |
|---|---|---|
| What the user brings | A vague goal, a means-focused question, or a stream of thoughts | A plan or design that needs to be made concrete |
| Questions per turn | 1–2 high-leverage questions, without solution recommendations | Can explore the full decision frontier and often recommend options |
| Success looks like | Four-part frame clarified → a precise problem statement | Design decisions resolved and shared understanding reached → an actionable plan |
| Before confirmation | No tools, code, solutions, or partial pros-and-cons of a proposed Y | No implementation before confirmation, though options may be discussed during discovery |
| Handoff | Names a next skill such as grill-me, brainstorming, requirements, or coding; does not launch it | Often continues into specification, implementation, or grill-with-docs |

In short: **grill-me turns an idea into an actionable plan; socratic-coach turns a muddled question into the right question.** When design choices need to be made, socratic-coach recommends switching to grill-me instead of making those choices itself.

## Use socratic-coach before grill-me

The recommended flow is **Socratic clarification first, grill-me second**:

1. If the idea is still unclear—or the conversation starts with “recommend a tool”—use socratic-coach to distill the real problem into one sentence.
2. The final response ends with a clear “Round complete” notice and recommends grill-me as the default next step.
3. Take that clarified problem to grill-me to make design decisions and shape an actionable plan.

Skipping the first step can produce a very detailed answer to the wrong question. If the problem is already clear, you can go straight to grill-me.

## Triggers

- **Automatic:** An agent may load the skill when the `SKILL.md` frontmatter description matches signals such as confusion, tool recommendations, XY problems, or “my thoughts are a mess.”
- **Optional commands:** `/苏格拉底` and `/问清楚`.

## Language

The skill follows the language used in the current conversation. If that is unclear, it uses the agent’s configured default language, falling back to Chinese. Language changes only the wording, not the underlying rules.

## Repository structure

| Path | Description |
|---|---|
| [`SKILL.md`](./SKILL.md) | Loadable skill instructions, including rules, workflow, templates, and self-checks |
| [`docs/examples/`](./docs/examples/) | Example conversations: follow-up questions, drafts, and final versions |
| [`docs/uat-summary.md`](./docs/uat-summary.md) | UAT summary placeholder; the full report is not public |
| [`CHANGELOG.md`](./CHANGELOG.md) | Version and rename history |
| [`LICENSE`](./LICENSE) | MIT License |

## Core behavior at a glance

1. Before the core need is confirmed: no tools, code, solution recommendations, or partial pros-and-cons of a proposed Y—even if asked.
2. Ask 1–2 high-leverage questions per turn: each must be able to change the Goal or Blocker. Self-checkable facts do not count toward the limit.
3. Clarify four elements—Context, Goal, Attempts, and Blocker. Present a **draft, not yet locked** first; provide the final version after the user confirms it.
4. End each turn with a progress line so the user can see what remains.
5. End the final response with **Round complete**: state that clarification is done, recommend grill-me by default, and mention other downstream skills as alternatives. Never launch another skill or load it automatically.
6. Match user-facing labels and terminology to the conversation language. In Chinese conversations, do not mix in English labels.

## License

MIT © 2026 SherryLi-vc

The complete rules and U1–U12 acceptance checklist are in [`SKILL.md`](./SKILL.md).
