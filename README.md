# Universal Coding Skills

> Tool-agnostic coding skills adapted from [mattpocock/skills](https://github.com/mattpocock/skills).  
> Works with **any** AI coding agent — Claude Code, Codex, OpenCode, Cursor, Copilot, Windsurf, and more.

## What Is This?

A collection of battle-tested engineering workflows, originally written for Claude Code by [Matt Pocock](https://github.com/mattpocock), now adapted into a **universal format** that works with any AI-powered coding tool.

Each skill is a structured `SKILL.md` with optional reference files. They encode **disciplines, not features** — ways of working that make your AI agent more effective.

## How to Use

### Option 1: System Prompt (Universal)

Add the relevant `SKILL.md` content to your AI coding tool's system prompt or project instructions:

- **Claude Code**: Add to `CLAUDE.md` or `.claude/` project instructions
- **Codex**: Add to `codex.md` or `AGENTS.md`
- **OpenCode**: Add to project instructions or system prompt
- **Cursor**: Add to `.cursorrules` or project rules
- **Copilot**: Add to `.github/copilot-instructions.md`
- **Windsurf**: Add to `.windsurfrules`

### Option 2: Pick Individual Skills

Copy only the skills you need into your project:

```bash
# Example: add TDD skill to your project
cp -r skills/engineering/tdd ./your-project/.ai-skills/tdd
```

Then reference it in your tool's config.

### Option 3: Context on Demand

When you need a skill, paste its content into the conversation with your AI agent.

## Skills Overview

### Engineering

| Skill | Description |
|-------|-------------|
| [tdd](skills/engineering/tdd/) | Test-driven development with vertical-slice red-green-refactor |
| [diagnose](skills/engineering/diagnose/) | Disciplined debugging: feedback loop → reproduce → hypothesize → instrument → fix |
| [prototype](skills/engineering/prototype/) | Build throwaway prototypes to flush out designs (logic or UI) |
| [to-prd](skills/engineering/to-prd/) | Turn conversation context into a structured PRD |
| [to-issues](skills/engineering/to-issues/) | Break plans into vertical-slice issues |
| [improve-codebase-architecture](skills/engineering/improve-codebase-architecture/) | Find deepening opportunities using domain language |
| [grill-with-docs](skills/engineering/grill-with-docs/) | Stress-test plans against domain model and documentation |
| [triage](skills/engineering/triage/) | Issue triage through a state machine |
| [zoom-out](skills/engineering/zoom-out/) | Get broader context on unfamiliar code |

### Productivity

| Skill | Description |
|-------|-------------|
| [grill-me](skills/productivity/grill-me/) | Relentless Q&A to stress-test plans |
| [caveman](skills/productivity/caveman/) | Ultra-compressed communication (~75% token reduction) |
| [write-a-skill](skills/productivity/write-a-skill/) | Create new skills with proper structure |

## Key Concepts

### Vertical Slices > Horizontal Slices

Whether writing tests or breaking down work, prefer **vertical slices** (tracer bullets) over horizontal ones. Each slice cuts through all layers end-to-end, delivering a narrow but complete path.

### Depth Over Breadth

Design **deep modules** — small interfaces hiding complex implementations. This maximizes leverage (capability per unit of interface) and locality (change concentrated in one place).

### Behavior Over Implementation

Tests should verify **what** the system does through public interfaces, not **how** it does it. Tests coupled to implementation break on refactors without behavior changes.

## Contributing

Contributions welcome! Please:

1. Keep skills tool-agnostic (no Claude Code / Cursor / etc. specific references)
2. Follow the existing structure (SKILL.md + optional reference files)
3. Keep descriptions concise and trigger-focused

## License

MIT

## Acknowledgments

- Original skills by [Matt Pocock](https://github.com/mattpocock) — [mattpocock/skills](https://github.com/mattpocock/skills)
- Adapted to universal format for use with any AI coding agent
