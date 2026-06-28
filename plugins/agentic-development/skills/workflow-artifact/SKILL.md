---
name: workflow-artifact
description: Use when development work is large, risky, multi-session, multi-agent, interrupted, or needs durable plan/handoff memory for continuity across coding agents.
---

# Workflow Artifact

Create durable task memory when chat context is not enough.

## Path

Default path:

```text
docs/ai-workflow/YYYY-MM-DD-<task-slug>.md
```

Use an existing repo convention instead when one is obvious.

If the path already exists, update it when it is the same task. For a different task on the same day, append a short distinguishing suffix such as `-2` or a more specific slug.

## Lifecycle

Default to a repository document that is eligible for version control, not a gitignored scratch file, when the artifact is meant to survive agent sessions. Do not commit it unless the user asks or the repo workflow explicitly requires it.

Use a repo-ignored scratch location only when the artifact is local-only or disposable. Mark scratch artifacts clearly and delete them before finishing unless they are still needed for handoff.

When the task completes, set Current Status to `Done`, `Blocked`, or `Handoff`, refresh Verification and Handoff, and either keep the artifact as useful project memory or remove/archive it if it was only live working state.

## When To Create Or Update

Create before implementation for large/risky, multi-agent, interrupted, multi-session, or continuity-heavy medium work. Update after meaningful plan changes, consequential decisions, research findings, verification, interruption, or handoff.

Do not create artifacts for tiny work unless the user asks.

## Template

```markdown
# <Task Title>

## Goal

## Mode

Tiny | Small | Medium | Large/Risky

## Current Status

## Local Instructions

Project instruction files consulted and notable constraints.

## Decisions

Consequential decisions only. Include rejected approaches when useful.

## Research

Source links, date-sensitive findings, and implementation impact.

## Plan

Checklist of current work slices.

## Key Areas

Important files, modules, tests, config, or docs. Not a full changelog.

## Verification

Commands, checks, results, manual steps, and gaps.

## Open Questions And Risks

## Handoff

What the next agent should do first.
```

## Completion Criterion

The artifact is complete only when every template section is present and non-empty or marked `N/A` with a reason; Current Status, Plan, Verification, Open Questions And Risks, and Handoff match the latest work; and Handoff names the exact next action a fresh agent should take first.
