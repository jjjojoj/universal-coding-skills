# Logic Prototype

A tiny interactive terminal app that lets the user drive a state model by hand. Use this when the question is about **business logic, state transitions, or data shape**.

## When this is the right shape

- "I'm not sure if this state machine handles the edge case where X then Y."
- "Does this data model actually let me represent the case where..."
- "I want to feel out what the API should look like before writing it."

If the question is "what should this look like" — wrong branch. Use [UI.md](UI.md).

## Process

### 1. State the question

Before writing code, write down what state model and what question you're prototyping. One paragraph. A logic prototype that answers the wrong question is pure waste.

Also name the non-goals. If persistence, auth, concurrency, or real integrations are out of scope, say so before building.

### 2. Pick the language

Use whatever the host project uses. Match existing conventions for tooling — don't add a new package manager or runtime just for the prototype.

### 3. Isolate the logic in a portable module

Put the actual logic behind a small, pure interface that could be lifted out and dropped into the real codebase later. The TUI around it is throwaway; the logic module shouldn't be.

The right shape depends on the question:

- **A pure reducer** — `(state, action) => state`. Good when actions are discrete events.
- **A state machine** — explicit states and transitions. Good when "which actions are legal" is part of the question.
- **A small set of pure functions** over a plain data type. Good when there's no implicit current state.
- **A class or module with a clear method surface** when the logic genuinely owns ongoing internal state.

Keep it pure: no I/O, no terminal code, no `console.log` for control flow. The TUI imports it and calls into it; nothing flows the other direction.

### 4. Build the smallest TUI that exposes the state

On every tick, clear the screen and re-render the whole frame. The user should always see one stable view, not an ever-growing scrollback.

Each frame has two parts:

1. **Current state**, pretty-printed and diff-friendly (one field per line, or formatted JSON).
2. **Keyboard shortcuts**, listed at the bottom: `[a] add user  [d] delete user  [t] tick clock  [q] quit`.

Behaviour:

1. **Initialise state** — a single in-memory object/struct. Render the first frame on start.
2. **Read one keystroke (or one line)** at a time, dispatch to a handler that mutates state.
3. **Re-render** the full frame after every action — don't append, replace.
4. **Loop until quit.**

### 5. Make it runnable in one command

Add a script to the project's existing task runner. The user should run one command — never need to remember a path.

Exit semantics:

- `0`: user quit normally after exploring the model.
- Non-zero: startup failed, required fixture/env was missing, or the prototype hit an unhandled state. Print the current action and state snapshot before exiting when possible.

### 6. Hand it over

Give the user the run command. They'll drive it themselves. If they want new actions added, add them. Prototypes evolve.

### 7. Capture the answer

When the prototype has done its job, the answer to the question is the only thing worth keeping. Leave a `NOTES.md` next to the prototype if the user is AFK.

## Anti-patterns

- **Don't add tests.** A prototype that needs tests is no longer a prototype.
- **Don't wire it to the real database.** Use an in-memory store.
- **Don't generalise.** No "what if we wanted to support X later."
- **Don't blur the logic and the TUI together.** Keep the TUI as a thin shell over a pure module.
- **Don't ship the TUI shell into production.**
- **Don't hide state transitions.** If the user cannot see what changed after an action, the prototype is not answering the question.
