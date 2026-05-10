---
name: triage
description: Move issues through a small state machine of triage roles, distinguishing issues ready for agent work from those needing human judgment. Use when processing a project issue tracker backlog.
---

# Triage

Move issues on the project issue tracker through a small state machine of triage roles.

## Roles

Two **category** roles:

- `bug` — something is broken
- `enhancement` — new feature or improvement

Five **state** roles:

- `needs-triage` — maintainer needs to evaluate
- `needs-info` — waiting on reporter for more information
- `ready-for-agent` — fully specified, ready for an AI agent
- `ready-for-human` — needs human implementation
- `wontfix` — will not be actioned

Every triaged issue should carry exactly one category role and one state role.

State transitions: an unlabeled issue normally goes to `needs-triage` first; from there it moves to `needs-info`, `ready-for-agent`, `ready-for-human`, or `wontfix`. `needs-info` returns to `needs-triage` once the reporter replies.

## Show what needs attention

Query the issue tracker and present three buckets, oldest first:

1. **Unlabeled** — never triaged.
2. **`needs-triage`** — evaluation in progress.
3. **`needs-info` with reporter activity since the last triage notes** — needs re-evaluation.

Show counts and a one-line summary per issue. Let the maintainer pick.

## Triage a specific issue

1. **Gather context.** Read the full issue (body, comments, labels, reporter, dates). Parse any prior triage notes so you don't re-ask resolved questions. Explore the codebase.
2. **Recommend.** Tell the maintainer your category and state recommendation with reasoning, plus a brief codebase summary relevant to the issue. Wait for direction.
3. **Reproduce (bugs only).** Before any grilling, attempt reproduction: read the reporter's steps, trace the relevant code, run tests or commands.
4. **Grill (if needed).** If the issue needs fleshing out, run a grilling session.
5. **Apply the outcome:**
   - `ready-for-agent` — post an agent brief comment (see [AGENT-BRIEF.md](AGENT-BRIEF.md)).
   - `ready-for-human` — same structure, but note why it can't be delegated.
   - `needs-info` — post triage notes with specific, actionable questions.
   - `wontfix` — polite explanation, then close.

## Needs-info template

```markdown
## Triage Notes

**What we've established so far:**

- point 1
- point 2

**What we still need from you (@reporter):**

- question 1
- question 2
```

## Resuming a previous session

If prior triage notes exist on the issue, read them, check whether the reporter has answered any outstanding questions, and present an updated picture before continuing. Don't re-ask resolved questions.

## Choosing ready-for-agent vs ready-for-human

Mark as `ready-for-agent` when:
- The issue is fully specified with concrete acceptance criteria.
- The change is bounded and unlikely to require architectural judgment.
- The work is primarily implementation (wire up existing patterns) rather than design.
- The codebase has enough existing patterns that an agent can follow conventions.

Mark as `ready-for-human` when:
- The issue requires design decisions that can't be specified in advance.
- The work touches security, auth, billing, or data integrity in non-trivial ways.
- The change requires deep domain knowledge that isn't captured in codebase documentation.
- The issue is ambiguous and needs iteration (treat iteration as a human task, then triage the clarified result again).

When uncertain, default to `ready-for-human`. A miscategorized `ready-for-agent` issue wastes agent cycles and produces a PR that needs rewriting. A miscategorized `ready-for-human` issue just takes a few extra minutes of a human's time.

## Common Pitfalls

- **Triaging without exploring the codebase.** An issue that says "the login page is broken" could be a 5-minute CSS fix or a week-long auth refactor. You can't recommend a state without understanding the code.
- **Re-asking resolved questions.** If prior triage notes exist and the reporter already answered a question, asking it again signals you didn't read the issue. Always parse existing triage notes first.
- **Marking bugs as `ready-for-agent` without reproducing.** If you haven't confirmed the bug exists, you're asking an agent to debug an unconfirmed report. That's the hardest possible task for an agent.
- **Over-grilling simple issues.** Not every issue needs a grilling session. If the issue body is already clear and specific, triage it directly.
- **Writing agent briefs with file paths.** File paths go stale. Write about types, interfaces, and behavioral contracts instead. See [AGENT-BRIEF.md](AGENT-BRIEF.md).
