---
name: parallel-lanes
description: Use when development work has independent lanes for research, codebase exploration, inventory, validation, review, or non-overlapping implementation that can run in subagents, parallel tool calls, or separately owned workstreams.
---

# Parallel Lanes

Use parallelism when independence is real.

## When To Use

- Tiny work: skip.
- Small work: use opportunistically for independent reads/searches.
- Medium/large work: use when available for research, codebase exploration, migration inventory, validation, review, UI checks, or security passes.

## Lane Hierarchy

1. Subagents for independent reasoning or fresh-eye review.
2. Parallel tool calls for independent file reads, searches, metadata checks, or commands.
3. Sequential fallback when neither is available.

## Lane Contract

Define each lane with:

- question or task;
- allowed scope;
- files or systems to avoid;
- expected output;
- stop condition.

The main agent owns synthesis, decisions, and final user communication.

## Edit Safety

Default lanes are research, exploration, and validation. Editing lanes are allowed only when file ownership is clearly non-overlapping. If ownership is unclear, lanes report findings and the main agent applies edits.

## Completion Criterion

Every lane has a result, gap, or blocked reason. Before leaving the gate, each gap or blocker is resolved by the main agent, marked non-blocking with reason, added to the plan/artifact as follow-up, or escalated to the user. The main agent has synthesized how the lane output changes the plan.
