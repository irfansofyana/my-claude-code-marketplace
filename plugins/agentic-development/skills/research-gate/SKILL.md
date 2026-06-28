---
name: research-gate
description: "Use when development work depends on current or external facts: latest docs/APIs, library or platform behavior, security guidance, unfamiliar errors, migrations, comparisons, best practices, prior art, or known fixes."
---

# Research Gate

Research is for reducing uncertainty, not for delaying local work.

## Decide

Inspect local docs and code first when the answer may be repo-defined.

Use external research when:

- facts may have changed recently;
- external APIs, frameworks, providers, models, packages, deployment, CI, browsers, platforms, or security guidance matter;
- the user asks for latest, recommended, compare, best practice, known fix, or prior art;
- an error message or failing tool output is unfamiliar;
- guessing would shape the implementation;
- repeated attempts failed.

Skip research when the answer is clearly local, mechanical, or already covered by authoritative repo docs/tests. If skipped, say why briefly.

## Source Order

Prefer sources in this order:

1. Official docs, specs, release notes, changelogs.
2. Maintainer issues, discussions, migration guides.
3. Reputable engineering writeups, incident reports, benchmarks.
4. Community posts only when they explain a reproducible symptom or workaround.

## Citation Rule

When research is used, cite source links in the answer. For medium/large work, also record important links and date-sensitive findings in the live workflow artifact.

## Completion Criterion

End the gate only after local docs/code have been inspected or explicitly ruled out. If research is used, record each implementation-shaping finding, its authoritative source link, version/date constraints, conflicts or unavailable authoritative sources, and implementation impact. If research is skipped, state the repo-local evidence that makes it unnecessary.
