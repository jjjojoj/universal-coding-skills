---
name: grill-with-docs
description: Stress-test a plan against the codebase's domain language and update glossary or ADR documentation as decisions become clear. Use when a user wants design grilling that stays grounded in existing docs, terminology, and implementation reality.
---

# Grill with Docs

Grilling session that challenges your plan against the existing domain model, sharpens terminology, and updates documentation inline as decisions crystallise.

## Instructions

Interview me relentlessly about every aspect of this plan until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one. For each question, provide your recommended answer.

Ask the questions one at a time, waiting for feedback on each question before continuing.

If a question can be answered by exploring the codebase, explore the codebase instead.

## Domain awareness

During codebase exploration, also look for existing documentation:

- root project instructions and README files
- `CONTEXT.md` or `CONTEXT-MAP.md`
- `docs/adr/` or similar decision records
- domain glossaries, architecture docs, issue templates, and product specs

Prefer existing project conventions over this skill's default filenames. Only create the default files below when the repo has no established convention.

### File structure

Most repos have a single context:

```
/
├── CONTEXT.md
├── docs/
│   └── adr/
│       ├── 0001-event-sourced-orders.md
│       └── 0002-postgres-for-write-model.md
└── src/
```

If a `CONTEXT-MAP.md` exists at the root, the repo has multiple contexts. See [CONTEXT-FORMAT.md](CONTEXT-FORMAT.md) for details.

Create files lazily — only when you have a resolved term, relationship, ambiguity, or decision to write. Do not create empty documentation scaffolding.

## During the session

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in the project glossary, call it out immediately. "Your glossary defines 'cancellation' as X, but you seem to mean Y — which is it?"

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term.

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with specific scenarios. Invent scenarios that probe edge cases and force precision about boundaries between concepts.

### Cross-reference with code

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it.

If code and docs disagree, record the conflict as unresolved unless the user explicitly confirms which source is authoritative.

### Update documentation inline

When a term is resolved, update the project glossary right there. Don't batch these up — capture them as they happen. See [CONTEXT-FORMAT.md](CONTEXT-FORMAT.md).

Do not write speculative terminology into durable docs. If a question remains open, capture it under "Flagged ambiguities" with the decision needed.

### Offer ADRs sparingly

Only offer to create an ADR when all three are true:

1. **Hard to reverse** — the cost of changing your mind later is meaningful
2. **Surprising without context** — a future reader will wonder "why did they do it this way?"
3. **The result of a real trade-off** — there were genuine alternatives and you picked one for specific reasons

See [ADR-FORMAT.md](ADR-FORMAT.md) for the format.

## Common errors

- Asking abstract questions when the code can answer them.
- Creating an ADR for a routine implementation detail.
- Treating the glossary as a dictionary of every noun in the repo. It should contain project-specific domain terms.
- Updating docs after the session instead of while decisions are fresh.
