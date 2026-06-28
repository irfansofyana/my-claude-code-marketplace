---
name: shared-understanding
description: Use when a development request is vague, exploratory, conflicted, under-specified, or the user says they are unsure, wants to be grilled, wants assumptions challenged, or needs goal, scope, constraints, and success criteria clarified before planning or implementation.
---

# Shared Understanding

Reach alignment before planning or building. The discipline is one question at a time.

## Loop

1. Inspect the repo instead of asking anything local files can answer.
2. State your current understanding in one short sentence when it helps frame the next branch.
3. Ask exactly one question.
4. Include `My recommendation:` with the answer you would choose and why.
5. Wait for the user's reply before asking the next question.

## What To Resolve

Resolve only branches that materially affect the work:

- goal and non-goals;
- user value or success criteria;
- scope boundaries and constraints;
- risky assumptions;
- sequencing and rollback needs;
- verification expectations.

Challenge assumptions when they affect correctness, cost, maintainability, scope, or user value. Do not challenge harmless preferences.

## Completion Criterion

Shared understanding is reached only when every material branch in What To Resolve is answered by repo evidence or the user, explicitly accepted as an assumption with risk, or deliberately deferred. Then state:

- goal;
- scope and out of scope;
- key constraints;
- success criteria;
- next action.

Ask for confirmation if the next step would change files or commit to a plan.
