---
name: to-issues
description: Break an approved plan or PRD into independently deliverable vertical-slice issues with clear dependencies and acceptance criteria. Use when turning product or engineering plans into issue tracker work items for humans or coding agents.
---

# To Issues

Break a plan into independently-grabbable issues using vertical slices (tracer bullets).

## Process

### 1. Gather context

Work from whatever is already in the conversation context. If the user passes an issue reference (issue number, URL, or path), fetch it from the issue tracker and read its full body and comments.

If no issue tracker is configured or accessible, produce issue drafts in the same template and say they are ready to paste.

### 2. Explore the codebase (optional)

If you haven't explored the codebase, do so to understand the current state. Issue titles and descriptions should use the project's domain vocabulary.

### 3. Draft vertical slices

Break the plan into **tracer bullet** issues. Each issue is a thin vertical slice that cuts through ALL integration layers end-to-end, NOT a horizontal slice of one layer.

Slices may be 'HITL' (requires human interaction) or 'AFK' (can be implemented without human interaction). Prefer AFK over HITL where possible.

Rules:

- Each slice delivers a narrow but COMPLETE path through every layer (schema, API, UI, tests)
- A completed slice is demoable or verifiable on its own
- Prefer many thin slices over few thick ones
- Each slice has one primary user-visible behavior or operational outcome
- Dependencies are explicit; avoid hidden sequencing in prose

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

After publishing, verify that every issue exists, links to its blockers, and can be understood without reading the whole conversation.

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

Each criterion should be observable through product behavior, API behavior, logs/metrics, or a named command. Avoid "implementation completed" as a criterion.

## Blocked by

- A reference to the blocking ticket (if any)
- Or "None - can start immediately" if no blockers
```

## Common errors

- Creating horizontal issues like "add schema", "add API", "add UI" when none are useful alone.
- Writing acceptance criteria that require knowing the implementation.
- Omitting test or verification expectations from AFK issues.
- Publishing issues before the user has approved the dependency graph.
