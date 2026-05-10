---
name: tdd
description: Practice behavior-first test-driven development with vertical red-green-refactor slices through public interfaces. Use when implementing features or fixes where tests should drive design, protect behavior, or expose better module boundaries.
---

# Test-Driven Development

## Philosophy

**Core principle**: Tests should verify behavior through public interfaces, not implementation details. Code can change entirely; tests shouldn't.

**Good tests** are integration-style: they exercise real code paths through public APIs. They describe _what_ the system does, not _how_ it does it. A good test reads like a specification — "user can checkout with valid cart" tells you exactly what capability exists. These tests survive refactors because they don't care about internal structure.

**Bad tests** are coupled to implementation. They mock internal collaborators, test private methods, or verify through external means (like querying a database directly instead of using the interface). The warning sign: your test breaks when you refactor, but behavior hasn't changed. If you rename an internal function and tests fail, those tests were testing implementation, not behavior.

See [tests.md](tests.md) for examples and [mocking.md](mocking.md) for mocking guidelines.

## Anti-Pattern: Horizontal Slices

**DO NOT write all tests first, then all implementation.** This is "horizontal slicing" — treating RED as "write all tests" and GREEN as "write all code."

This produces **crap tests**:

- Tests written in bulk test _imagined_ behavior, not _actual_ behavior
- You end up testing the _shape_ of things (data structures, function signatures) rather than user-facing behavior
- Tests become insensitive to real changes — they pass when behavior breaks, fail when behavior is fine
- You outrun your headlights, committing to test structure before understanding the implementation

**Correct approach**: Vertical slices via tracer bullets. One test → one implementation → repeat. Each test responds to what you learned from the previous cycle.

```
WRONG (horizontal):
  RED:   test1, test2, test3, test4, test5
  GREEN: impl1, impl2, impl3, impl4, impl5

RIGHT (vertical):
  RED→GREEN: test1→impl1
  RED→GREEN: test2→impl2
  RED→GREEN: test3→impl3
  ...
```

## Workflow

### 1. Planning

Before writing any code:

- [ ] Confirm with user what interface changes are needed
- [ ] Confirm with user which behaviors to test (prioritize)
- [ ] Identify opportunities for [deep modules](deep-modules.md) (small interface, deep implementation)
- [ ] Design interfaces for [testability](interface-design.md)
- [ ] List the behaviors to test (not implementation steps)
- [ ] Get user approval on the plan

Ask: "What should the public interface look like? Which behaviors are most important to test?"

**You can't test everything.** Confirm with the user exactly which behaviors matter most. Focus testing effort on critical paths and complex logic, not every possible edge case.

### 2. Tracer Bullet

Write ONE test that confirms ONE thing about the system:

```
RED:   Write test for first behavior → test fails
GREEN: Write minimal code to pass → test passes
```

This is your tracer bullet — proves the path works end-to-end.

### 3. Incremental Loop

For each remaining behavior:

```
RED:   Write next test → fails
GREEN: Minimal code to pass → passes
```

Rules:

- One test at a time
- Only enough code to pass current test
- Don't anticipate future tests
- Keep tests focused on observable behavior

### 4. Refactor

After all tests pass, look for [refactor candidates](refactoring.md):

- [ ] Extract duplication
- [ ] Deepen modules (move complexity behind simple interfaces)
- [ ] Apply SOLID principles where natural
- [ ] Consider what new code reveals about existing code
- [ ] Run tests after each refactor step

**Never refactor while RED.** Get to GREEN first.

## Checklist Per Cycle

```
[ ] Test describes behavior, not implementation
[ ] Test uses public interface only
[ ] Test would survive internal refactor
[ ] Code is minimal for this test
[ ] No speculative features added
```

## When to Deviate from Strict TDD

TDD is a tool, not a religion. Deviate deliberately when:

- **Exploratory coding on unfamiliar terrain.** When you don't yet know what the interface should look like, writing tests first is guessing. Prototype the implementation, discover the shape, then extract tests from what you learned.
- **Writing tests for existing untested code (characterization tests).** You're documenting current behavior, not designing new behavior. Write the test to capture what the code actually does before refactoring.
- **Trivial glue code.** Boilerplate that wires together already-tested modules doesn't benefit from test-first. Write it, then verify integration at a higher level.
- **The test framework makes incremental testing impractical.** Some domains (GPU shaders, embedded firmware, complex visual output) have feedback loops measured in minutes. Batch written tests may be pragmatically necessary — but acknowledge you're deviating and why.

When deviating, state the reason explicitly in a code comment or commit message. "Skipped TDD here because <reason>" is enough to prevent future maintainers from thinking it was carelessness.

## Common Mistakes

- **Testing implementation details instead of behavior.** If renaming an internal function breaks tests, those tests are wrong. The test should care about what the system produces, not which internal steps it took.
- **Mocking internal collaborators.** Mocking your own classes/modules couples tests to the current structure. Only mock at true system boundaries (external APIs, time, randomness).
- **Over-testing simple getters, constructors, and delegation.** A test that asserts `new User("Alice").name` equals `"Alice"` tests the language runtime, not your code.
- **Writing tests that never fail.** If you write the implementation first and then a test that passes on the first run, you haven't tested anything — you've written a duplicate of the implementation. Delete the test or invert it temporarily to verify it can fail.
- **Horizontal slicing.** Writing all tests before any implementation. This anchors on imagined behavior and produces brittle tests that don't survive implementation reality.
- **Refactoring while RED.** Don't clean up code structure while tests are failing. Get to GREEN first, then refactor with the safety net of passing tests.
