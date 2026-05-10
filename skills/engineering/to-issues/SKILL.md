---
name: to-issues
description: Break a plan into independently-grabbable issues using vertical slices (tracer bullets). Use when a plan, PRD, or design needs to be converted into actionable tasks for an issue tracker.
---

# To Issues

Break a plan into independently-grabbable issues using vertical slices (tracer bullets).

## Process

### 1. Gather context

Work from whatever is already in the conversation context. If the user passes an issue reference (issue number, URL, or path), fetch it from the issue tracker and read its full body and comments.

### 2. Explore the codebase (optional)

If you haven't explored the codebase, do so to understand the current state. Issue titles and descriptions should use the project's domain vocabulary.

### 3. Draft vertical slices

Break the plan into **tracer bullet** issues. Each issue is a thin vertical slice that cuts through ALL integration layers end-to-end, NOT a horizontal slice of one layer.

Slices may be 'HITL' (requires human interaction) or 'AFK' (can be implemented without human interaction). Prefer AFK over HITL where possible.

Rules:
- Each slice delivers a narrow but COMPLETE path through every layer (schema, API, UI, tests)
- A completed slice is demoable or verifiable on its own
- Prefer many thin slices over few thick ones

### 4. Quiz the user

Present the proposed breakdown as a numbered list. For each slice, show:

- **Title**: short descriptive name
- **Type**: HITL / AFK
- **Blocked by**: which other slices (if any) must complete first
- **User stories covered**: which user stories this addresses

Ask the user:

- Does the granularity feel right?
- Are the dependency relationships correct?
- Should any slices be merged or split further?

Iterate until the user approves the breakdown.

### 5. Publish the issues

For each approved slice, publish a new issue using the template below. Publish in dependency order so you can reference real issue identifiers.

## Granularity Guidelines

A slice is too big when:
- It takes more than 1–2 days of focused work.
- It covers multiple distinct user stories.
- The acceptance criteria list exceeds 5–7 items.

A slice is too small when:
- It delivers no user-visible or testable behavior on its own.
- It's a single-file change with no integration touchpoints (that's a commit, not an issue).
- Its description is a tautology of its title.

## When Not to Use This

- **The plan is a single, small change.** Breaking a one-hour task into slices is overhead, not leverage.
- **The user is exploring, not committing.** If the user is prototyping or brainstorming, issues lock thinking too early.
- **No issue tracker is configured.** Don't publish issues to nowhere. Skip to a checklist in the conversation instead.
- **The work is firefighting.** A critical bug fix doesn't benefit from issue decomposition — fix first, document after.

## Issue Template

```markdown
## Parent

A reference to the parent issue (if applicable).

## What to build

A concise description of this vertical slice. Describe the end-to-end behavior, not layer-by-layer implementation.

Avoid specific file paths or code snippets. Exception: if a prototype produced a snippet that encodes a decision more precisely than prose can, inline it here and note briefly that it came from a prototype.

## Acceptance criteria

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Blocked by

- A reference to the blocking ticket (if any)
- Or "None - can start immediately" if no blockers
```
