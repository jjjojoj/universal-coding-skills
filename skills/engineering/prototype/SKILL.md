---
name: prototype
description: Build throwaway code that answers a specific design question. Use when you need to validate a UI concept, logic approach, or integration pattern before committing to production implementation.
---

# Prototype

A prototype is **throwaway code that answers a question**. The question decides the shape.

## Pick a branch

Identify which question is being answered:

- **"Does this logic / state model feel right?"** → [LOGIC.md](LOGIC.md). Build a tiny interactive terminal app that pushes the state machine through cases that are hard to reason about on paper.
- **"What should this look like?"** → [UI.md](UI.md). Generate several radically different UI variations on a single route, switchable via a URL search param and a floating bottom bar.

The two branches produce very different artifacts — getting this wrong wastes the whole prototype. If the question is genuinely ambiguous, default to whichever branch better matches the surrounding code (a backend module → logic; a page or component → UI) and state the assumption.

## Rules that apply to both

1. **Throwaway from day one, and clearly marked as such.** Locate the prototype code close to where it will actually be used so context is obvious — but name it so a casual reader can see it's a prototype, not production.
2. **One command to run.** Whatever the project's existing task runner supports — `npm run <name>`, `python <path>`, `bun <path>`, etc. The user must be able to start it without thinking.
3. **No persistence by default.** State lives in memory. Persistence is the thing the prototype is _checking_, not something it should depend on.
4. **Skip the polish.** No tests, no error handling beyond what makes the prototype _runnable_, no abstractions. The point is to learn something fast and then delete it.
5. **Surface the state.** After every action (logic) or on every variant switch (UI), print or render the full relevant state so the user can see what changed.
6. **Delete or absorb when done.** When the prototype has answered its question, either delete it or fold the validated decision into the real code — don't leave it rotting in the repo.

## When done

The _answer_ is the only thing worth keeping from a prototype. Capture it somewhere durable (commit message, ADR, issue, or a `NOTES.md` next to the prototype) along with the question it was answering.

## Common Mistakes

- **Picking the wrong branch.** Building a UI prototype for a logic question (or vice versa) wastes the entire effort. If the user says "I'm not sure how this state machine handles X," that's LOGIC, not UI — no matter how visual the end product will be.
- **Prototype becoming production.** The most dangerous outcome. If the prototype feels solid, delete the prototype files and rewrite the validated logic/design into the real codebase from scratch. Prototypes skip error handling, tests, and architectural discipline — carrying those shortcuts into production creates technical debt.
- **Over-engineering the prototype itself.** Adding configuration, multiple environments, or abstraction layers to throwaway code. Every minute spent on prototype infrastructure is a minute not spent answering the question.
- **Not stating the question first.** A prototype that answers a vague or wrong question is noise, not signal. Write the question down before writing any code.
- **Leaving the prototype in the repo after answering the question.** "I'll clean it up later" means it rots. The cleanup step (delete or absorb) must happen before the task is done.
