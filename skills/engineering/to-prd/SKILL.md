---
name: to-prd
description: Turn the current conversation context and codebase understanding into a structured PRD without interviewing the user. Use when a design discussion needs to be captured as a product requirements document.
---

# To PRD

Turn the current conversation context and codebase understanding into a PRD. Do NOT interview the user — just synthesize what you already know.

Use this when the conversation has accumulated design decisions that need capturing. If the user explicitly asked for a PRD, use this. Otherwise, consider [to-issues](../to-issues/SKILL.md) if the goal is breaking work into implementable units rather than documenting design rationale.

## Relationship to to-issues

- **to-prd** captures the _what_ and _why_: problem statement, user stories, architectural decisions, testing strategy.
- **to-issues** breaks that plan into _how_: individually-grabbable vertical slices.

A PRD is upstream of issues. If you have a PRD, the next step is to use to-issues to decompose it. If you don't need the design documentation (small feature, obvious implementation), skip the PRD and go straight to to-issues.

## Process

1. Explore the repo to understand the current state of the codebase, if you haven't already.

2. Sketch out the major modules you will need to build or modify to complete the implementation. Actively look for opportunities to extract deep modules that can be tested in isolation.

   Check with the user that these modules match their expectations. Check which modules they want tests written for.

3. Write the PRD using the template below, then publish it to the project issue tracker if configured.

## PRD Template

```markdown
## Problem Statement

The problem that the user is facing, from the user's perspective.

## Solution

The solution to the problem, from the user's perspective.

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

## Out of Scope

Things that are out of scope for this PRD.

## Further Notes

Any additional notes about the feature.
```

## Common Mistakes

- **Interviewing the user.** This skill says "do NOT interview the user — synthesize what you already know." If you have gaps, list them as open questions in Further Notes and let the user fill them in. Don't turn a PRD into a grilling session.
- **Including file paths and code snippets.** They go stale before the PRD is a week old. Describe types, interfaces, and behavioral contracts instead.
- **Writing user stories as implementation tasks.** "Add a users table" is a task, not a user story. "As a new visitor, I can create an account" is a user story. Implementation details live in Implementation Decisions.
- **Skipping the module sketch step.** The module sketch (step 2) is where implementation feasibility is checked. A PRD that doesn't flag architectural friction is incomplete.
- **Treating the PRD as final.** A PRD from conversation context is a starting point, not a contract. Mark it as draft and expect iteration.
