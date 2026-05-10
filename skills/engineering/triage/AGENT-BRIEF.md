# Writing Agent Briefs

An agent brief is a structured comment posted on an issue tracker item when it moves to `ready-for-agent`. It is the authoritative specification that a coding agent or implementer will work from. The original issue body and discussion are context — the agent brief is the contract.

## Principles

### Durability over precision

The issue may sit in `ready-for-agent` for days or weeks. The codebase will change. Write the brief so it stays useful even as files are renamed, moved, or refactored.

- **Do** describe interfaces, types, and behavioral contracts
- **Do** name specific types, function signatures, or config shapes that the implementer should look for or modify
- **Don't** reference file paths — they go stale
- **Don't** reference line numbers
- **Don't** assume the current implementation structure will remain the same

### Behavioral, not procedural

Describe **what** the system should do, not **how** to implement it. The implementer will explore the codebase fresh and make its own implementation decisions.

- **Good:** "The `SkillConfig` type should accept an optional `schedule` field of type `CronExpression`"
- **Bad:** "Open src/types/skill.ts and add a schedule field on line 42"

### Complete acceptance criteria

The implementer needs to know when it's done. Every agent brief must have concrete, testable acceptance criteria.

- **Good:** "Running the test suite with the new config should pass all existing tests plus 3 new tests"
- **Bad:** "Triage should work correctly"

### Explicit scope boundaries

State what is out of scope. This prevents the implementer from gold-plating or making assumptions about adjacent features.

## Template

```markdown
## Agent Brief

**Category:** bug / enhancement
**Summary:** one-line description of what needs to happen

**Current behavior:**
Describe what happens now. For bugs, this is the broken behavior.
For enhancements, this is the status quo.

**Desired behavior:**
Describe what should happen instead. Be specific about inputs, outputs,
and edge cases.

**Acceptance criteria:**
- [ ] Concrete, testable criterion 1
- [ ] Concrete, testable criterion 2
- [ ] Concrete, testable criterion 3

**Scope:**
In scope: ...
Out of scope: ...

**Hints:**
- Any useful types, interfaces, or patterns to look for
- Related code areas that might need changes
- Any gotchas or non-obvious dependencies
```

## Handoff checks

- The brief is understandable without reading every previous comment.
- Acceptance criteria can be verified with product behavior, API behavior, or named commands.
- Scope boundaries mention adjacent work that should not be included.
- Hints accelerate exploration but do not dictate a brittle file-by-file implementation.
