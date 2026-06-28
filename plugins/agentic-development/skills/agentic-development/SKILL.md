---
name: agentic-development
description: Use when a development task is unclear, multi-step, risky, or needs coordinated gates for shared understanding, research, parallel lanes, workflow artifacts, and verification. For a single concern, invoke the specific gate; for tiny mechanical changes, skip unless the user asks.
---

# Agentic Development

Use the smallest reliable development loop. Expand only when ambiguity, risk, external facts, or coordination demand it.

## First Pass

1. Read and follow applicable local instruction files: `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `.cursor/rules`, `.github/copilot-instructions.md`, or equivalents. Complete when you can name which files existed and which constraints affect the task.
2. Inspect the repo area likely touched by the request, including related tests/config when present. Complete when you can name the involved files/components and which questions the codebase answered.
3. Choose a mode using the table. Complete when you have stated the mode and the trigger(s) that justify it.

| Mode | Use When | Loop |
|---|---|---|
| Tiny | Mechanical, obvious, low-risk | Inspect -> change -> verify -> summarize |
| Small | Clear goal, limited files | Inspect -> short plan -> change -> verify -> summarize |
| Medium | Some ambiguity, behavior change, several files | Clarify if needed -> plan checklist -> implement slices -> verify |
| Large/Risky | Broad scope, migration, architecture, security, production risk, multi-session | Artifact -> shared understanding -> research/parallel lanes -> plan -> slices -> verify -> handoff |

## Gates

- **Shared understanding:** If intent is vague, conflicted, or underspecified, invoke `shared-understanding`.
- **Research:** If current or external knowledge could change the answer, invoke `research-gate`.
- **Parallel lanes:** For medium/large work with independent research, exploration, validation, or review, invoke `parallel-lanes`.
- **Artifact:** For large/risky, multi-agent, interrupted, multi-session, or continuity-heavy medium work, invoke `workflow-artifact`.
- **Verification:** Before saying done, invoke `verification-gate`.

## Scope Control

Classify discovered adjacent work:

- **Blocking:** required for the requested work to be correct; fix now.
- **Related:** useful but not required; ask before doing.
- **Parking lot:** document only.

Do not commit by default. Commit only when the user asks or the repo workflow explicitly requires it.

## Completion Criterion

Stop only when the requested change is implemented or deliberately deferred, every triggered gate has passed or is explicitly blocked, verification evidence is available, and the final response names what changed, what was verified, and any remaining risk.
