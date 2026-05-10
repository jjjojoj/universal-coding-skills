---
name: grill-me
description: Stress-test a plan through one-question-at-a-time grilling, resolving assumptions, dependencies, risks, and edge cases before implementation. Use when the user asks for critique, design pressure, devil's advocate, or help finding gaps in a plan.
---

# Grill Me

Interview me relentlessly about every aspect of this plan until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one. For each question, provide your recommended answer.

Ask the questions one at a time, waiting for feedback on each question before continuing.

If a question can be answered by exploring the codebase, explore the codebase instead.

Stop grilling when the remaining uncertainty is low enough to act, or when the next question would not change the plan.

---

**When to use:**

- You have a plan or design and want to stress-test it
- You want to find gaps in your thinking before committing
- You're about to start implementation and want to make sure the design is solid
- You need someone to play devil's advocate

**What makes a good grilling:**

- Questions are specific, not vague ("What happens when the payment fails after the order is confirmed?" not "What about error handling?")
- Each question resolves one decision branch
- The assistant offers its recommended answer for each question
- Code exploration replaces hypothetical questions when possible
- Open assumptions are summarized before implementation starts

**Common errors:**

- Asking multiple questions at once.
- Asking questions the codebase can answer.
- Challenging style preferences while missing behavioral edge cases.
- Continuing after the plan is clear enough to execute.
