---
name: agentic-development
description: Use when a development task is unclear, multi-step, risky, or needs coordinated gates for shared understanding, research, parallel lanes, workflow artifacts, and verification. For a single concern, use the matching gate skill if available; for tiny mechanical changes, skip unless the user asks.
---

# Agentic Development

Use the smallest reliable development loop. Expand only when ambiguity, risk, external facts, or coordination demand it.

## First Pass

1. Read and follow applicable local instruction files: `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `.cursor/rules`, `.github/copilot-instructions.md`, or equivalents. Complete when you can name which files existed and which constraints affect the task.
2. Inspect the repo area likely touched by the request, including related tests/config when present. Complete when you can name the involved files/components and which questions the codebase answered.
3. Choose a mode using the table. Complete when you have stated the mode and the trigger(s) that justify it.

| Mode | Use When | Example | Loop |
|---|---|---|---|
| Tiny | Mechanical, obvious, low-risk | Rename a variable, format one file, fix a typo | Inspect -> change -> verify -> summarize |
| Small | Clear goal, limited files | Add one config value, adjust a narrow helper and test | Inspect -> short plan -> change -> verify -> summarize |
| Medium | Some ambiguity, behavior change, several files | Add a field across API/schema/UI, refactor a module | Clarify if needed -> plan checklist -> implement slices -> verify |
| Large/Risky | Broad scope, migration, architecture, security, production risk, multi-session | Auth rewrite, data migration, cross-service rollout | Artifact -> alignment -> research/lanes -> plan -> slices -> verify -> handoff |

## Gates

Gate skills are portable instruction sets, not callable subroutines. When a gate applies, load and follow the named `agentic-development:<skill>` skill if the runtime exposes it. If another skill cannot be loaded directly, use the fallback behavior in that bullet.

- **Shared understanding (`agentic-development:shared-understanding`):** If intent is vague, conflicted, or underspecified, read and follow this gate; otherwise ask one question at a time until the task is clear.
- **Research (`agentic-development:research-gate`):** If current or external knowledge could change the answer, read and follow this gate; otherwise research first and verify sources before relying on the answer.
- **Parallel lanes (`agentic-development:parallel-lanes`):** For medium/large work with independent research, exploration, validation, or review, read and follow this gate; otherwise split independent work into sequential lanes and synthesize findings.
- **Artifact (`agentic-development:workflow-artifact`):** For large/risky, multi-agent, interrupted, multi-session, or continuity-heavy medium work, read and follow this gate; otherwise keep a concise written handoff in the working context.
- **Verification (`agentic-development:verification-gate`):** Before saying done, read and follow this gate; otherwise run the strongest practical verification and report evidence.

## Commit Policy

Do not commit by default. Commit only when the user asks or the repo workflow explicitly requires it.

## Scope Control

Classify discovered adjacent work:

- **Blocking:** required for the requested work to be correct; fix now.
- **Related:** useful but not required; ask before doing.
- **Parking lot:** document only.

## Completion Criterion

Stop only when the requested change is implemented or deliberately deferred, every triggered gate has passed or is explicitly blocked, verification evidence is available, and the final response names what changed, what was verified, and any remaining risk.
