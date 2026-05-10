---
name: zoom-out
description: Build a higher-level map of an unfamiliar code area by identifying relevant modules, callers, dependencies, domain concepts, and change risks. Use when the user needs orientation before modifying or reviewing code.
---

<!-- REVIEW: Original skill was too thin: it described the desired output but did not give a repeatable exploration workflow or quality bar. -->

# Zoom Out

Go up a layer of abstraction. Produce a map of the relevant modules and callers using the project's domain vocabulary.

---

**When to use this skill:**

- You're unfamiliar with a section of code
- You need to understand how a module fits into the bigger picture
- You want a high-level map before diving into details
- You need to know what callers depend on a module before making changes

## Process

1. Identify the entry point from the user's prompt: file, symbol, feature, route, command, issue, or error.
2. Read nearby project docs and glossary terms first if they exist.
3. Trace outward from the entry point:
   - direct callers and callees
   - shared data types, events, schemas, commands, routes, jobs, or configuration
   - tests that describe expected behavior
4. Stop when additional files no longer change the mental model or risk picture.
5. Present a map, not a patch plan, unless the user asks for changes.

## Output

Provide:

1. Relevant modules in the area, with brief descriptions.
2. How they relate to each other: callers, callees, shared dependencies, and runtime flow.
3. Which domain concepts each module maps to.
4. Important seams, extension points, and state ownership.
5. A mental model of the architecture at this level of abstraction.
6. Change risks: callers likely to break, tests to run, and unknowns that need confirmation.

## Common errors

- Listing files without explaining relationships.
- Diving into line-by-line implementation before naming the higher-level concepts.
- Ignoring tests, routes, jobs, or config that reveal real entry points.
- Treating the first found caller as the whole system.
