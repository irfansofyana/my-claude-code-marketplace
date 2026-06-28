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
