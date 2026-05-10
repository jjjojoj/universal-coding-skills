---
name: to-prd
description: Synthesize existing conversation and codebase context into a concise PRD with user stories, implementation decisions, testing decisions, scope, risks, and open questions. Use when the user asks to turn current understanding into a product requirements document.
---

# To PRD

Turn the current conversation context and codebase understanding into a PRD. Do NOT interview the user — just synthesize what you already know.

If a missing fact blocks a truthful PRD, ask the smallest possible blocking question. Otherwise mark assumptions and open questions explicitly instead of inventing certainty.

## Process

1. Explore the repo to understand the current state of the codebase, if you haven't already.

2. Sketch out the major modules you will need to build or modify to complete the implementation. Actively look for opportunities to extract deep modules that can be tested in isolation.

   Check with the user that these modules match their expectations. Check which modules they want tests written for.

3. Write the PRD using the template below, then publish it to the project issue tracker if configured. If no tracker is configured, produce the PRD as a draft artifact in the conversation.

## PRD Template

```markdown
## Problem Statement

The problem that the user is facing, from the user's perspective.

## Solution

The solution to the problem, from the user's perspective.

## Goals and Success Metrics

- Goal 1
- Metric or observable signal 1
- Metric or observable signal 2

## User Stories

A LONG, numbered list of user stories. Each in the format:

1. As an <actor>, I want a <feature>, so that <benefit>

This list should be extremely extensive and cover all aspects of the feature.

## Implementation Decisions

- The modules that will be built/modified
- The interfaces of those modules
- Technical clarifications
- Architectural decisions
- Schema changes
- API contracts
- Specific interactions

Do NOT include specific file paths or code snippets — they go stale fast.

Exception: if a prototype produced a snippet that encodes a decision more precisely than prose can (state machine, reducer, schema, type shape), inline it and note briefly that it came from a prototype.

## Testing Decisions

- What makes a good test (only test external behavior, not implementation details)
- Which modules will be tested
- Prior art for the tests (similar types of tests in the codebase)
- Commands or checks that should pass when implementation is complete, if known

## Out of Scope

Things that are out of scope for this PRD.

## Risks and Open Questions

- Risk or unresolved question 1
- Risk or unresolved question 2

## Rollout and Compatibility

How this ships, any migration/backfill needed, and compatibility constraints.

## Further Notes

Any additional notes about the feature.
```

## Common errors

- Turning implementation guesses into requirements.
- Including file paths that will go stale before work starts.
- Writing user stories that are really engineering tasks.
- Omitting explicit out-of-scope items, causing issue breakdown to grow later.
