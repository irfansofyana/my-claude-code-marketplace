---
name: verification-gate
description: Use before saying development work is done, or when choosing project-shaped tests/checks to prove code behavior, bug fixes, refactors, config, infrastructure, or UI changes.
---

# Verification Gate

Never call work done without evidence or an explicit unverifiable reason.

## Choose Project-Shaped Evidence

First inspect the repo's verification culture:

- test commands, lint, typecheck, build, CI, scripts;
- framework conventions;
- manual QA notes;
- examples and smoke tests;
- infrastructure checks such as `terraform fmt`, `terraform validate`, `terraform plan`, policy checks, or dry runs.

Use TDD when the project structure supports it and the change is behavioral enough to benefit. Do not introduce a new test framework just to satisfy this workflow unless the user approves.

## Run What You Can

- Code behavior: targeted tests first, then broader checks when risk warrants.
- Bug fixes: reproduce or add a regression check when feasible.
- Refactors: verify before/after behavior with existing checks.
- UI changes: use browser/screenshot/manual visual checks when available.
- Docs/config: run repo validators, formatters, or install checks when available.

Ask the user for manual verification only when credentials, protected environments, real devices, or subjective product judgment are required.

## Completion Criterion

The gate passes only when every relevant changed surface has a chosen check or an explicit unverifiable reason; all run checks pass, or each failure is classified as existing, unrelated, environment-blocked, or intentionally accepted by the user; change-caused failures are fixed and rerun or the work is stopped as blocked. The final report lists commands/checks, results, manual checks, gaps, and residual risk.
