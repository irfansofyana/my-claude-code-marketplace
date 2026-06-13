---
name: 9router-web-researcher
description: >-
  Pi-only web research workflow for environments that have pi-9router-ext and a subagent extension such as @tintinweb/pi-subagents configured. Use this skill when the user explicitly asks to use 9router, pi-9router-ext, ninerouter tools, or a 9router route/combo for web research, or when project/user instructions state that 9router-web-researcher is the preferred research stack. Do NOT use for ordinary web research in standard shared-mcp-only or non-Pi clients; use web-researcher instead. This skill always delegates research lanes to subagents and then synthesizes compact cited findings.
---

# 9router Web Researcher

You are conducting real research, not recalling training data. Use `pi-9router-ext` web tools as the primary research path, and keep bulky search/fetch output out of the main context by delegating every research lane to subagents.

Expected client: Pi Coding Agent with both `pi-9router-ext` and subagent orchestration installed. This skill can fall back to direct web tools inside subagents when 9router tools are unavailable.

## Prerequisites

Pi core intentionally does not include built-in subagents. Install a subagent package before relying on this skill:

```bash
pi install npm:@tintinweb/pi-subagents
pi install npm:pi-9router-ext
```

Then configure 9router with `/9router-config` and verify it with `/9router-status`. `@tintinweb/pi-subagents` provides subagent orchestration; other Pi subagent extensions are acceptable if they can run parallel research children with isolated context.

If no subagent tool is available, do not run direct web research in the main context. Stop and tell the user to install/configure `@tintinweb/pi-subagents` or another subagent extension, because the main goal of this skill is context isolation.

## Core Rules

1. **Always spawn subagents.** For every web research task, launch 2–4 research-capable subagents in one tool turn. With `@tintinweb/pi-subagents`, use its available research-capable/general subagent configuration. In other harnesses, use an equivalent general-purpose research subagent. Main agent plans lanes and synthesizes; subagents search/fetch.
2. **Keep main context lean.** Do not paste raw search pages, long excerpts, or broad result dumps into main context. Require compact lane reports.
3. **Use exact 9router tool names.** The Pi tools are `ninerouter_status`, `ninerouter_web_search`, and `ninerouter_web_fetch`. Never invent `9router_*` tool names.
4. **9router first.** Each subagent should call `ninerouter_status`, then `ninerouter_web_search`, then `ninerouter_web_fetch` for top URLs that support important claims.
5. **Retry before fallback.** If 9router results are weak, retry 2–3 sharper query variants through 9router before switching tools.
6. **Fallback directly if needed.** If 9router tools fail or are absent, use direct tools similar to `web-researcher`: Brave for discovery, Tavily for extraction/deepening, Exa for semantic/technical/entity-heavy precision.
7. **Cite claims inline.** Every factual claim, code recommendation, date, pricing statement, or comparison point needs `(source: URL)`.

## Step 1: Classify Intent

Classify the request before choosing lanes.

| Intent | Signals | Useful lanes |
|---|---|---|
| News/current | latest, recent, today, this week, 2025/2026, changed, still true | Freshness/news, official/source-of-truth |
| Technical/docs | library, API, SDK, error message, framework, package, release notes | Official/source-of-truth, community/issues, comparison when alternatives exist |
| Debugging | exact error, stack trace, broken install, runtime failure | Community/issues, official/source-of-truth, version-specific lane |
| Comparison | X vs Y, alternatives, tradeoffs, benchmarks, production fit | Comparison/alternatives, community/evidence, official/source-of-truth |
| Entity/company | company, product, pricing, funding, customers, roadmap | Entity/company, freshness/news, official/source-of-truth |
| Known URLs | user provides URLs to read/summarize | URL extraction plus verification lane if claims need checking |
| General research | best practices, how to, background, broad topic | General discovery, official/source-of-truth, community/evidence |

## Step 2: Build Query Plan

Infer constraints from the user before searching: freshness window, preferred/excluded domains, exact URLs, product versions, geography, language, or requested 9router route/combo. Only ask a follow-up if a missing constraint would change the research materially.

Generate lane-specific queries before spawning subagents. Prefer precise query families:

- **Exact error**: quote the distinctive error, e.g. `"ECONNREFUSED 127.0.0.1:5432"`.
- **Official docs**: `site:docs.vendor.com feature name`, `site:github.com/vendor/repo release notes`, product docs URL when known.
- **Version/runtime**: include language, framework, package version, OS, database, cloud provider, or year.
- **Freshness**: add `latest`, `2026`, `this week`, `release notes`, `changelog`, or `announced`.
- **Community evidence**: add `GitHub issue`, `Stack Overflow`, `Reddit`, `forum`, `HN`, `discussion`.
- **Comparison**: `X vs Y production tradeoffs`, `X limitations`, `Y alternatives`, `benchmark`, `case study`.
- **Contradiction/risks**: `X problem`, `X known issue`, `X migration risk`, `X deprecated`, `X security advisory`.
- **Entity/pricing**: `official pricing`, `status page`, `docs limits`, `terms`, `customers`, `funding`, `acquisition`.

Give each subagent 3–6 concrete queries and tell it to add variants only when results are weak.

## Step 3: Spawn Parallel Subagents

Launch 2–4 research-capable subagents in the same turn. With `@tintinweb/pi-subagents`, use the available subagent tool in parallel mode and pick a research-capable/general child agent for each lane. Use adaptive lanes:

- **Official/source-of-truth lane**: official docs, specs, release notes, vendor blog, status/pricing pages.
- **Freshness/news lane**: recent announcements, news, dated changes, current status.
- **Community/issues lane**: GitHub issues, Stack Overflow, forums, Reddit, field reports.
- **Comparison/alternatives lane**: tradeoffs, benchmarks, alternatives, migration stories.
- **Entity/company lane**: company/product/pricing/funding/customer research.
- **URL extraction lane**: exact URLs provided by user, with focused extraction and verification.

Minimum 2 lanes. Use 3 lanes for technical/debug/comparison. Use 4 lanes for high-stakes, ambiguous, or broad research.

### Subagent Prompt Template

Use a compact prompt like this for each lane:

```text
You are one lane in a parallel web research task for 9router-web-researcher.

Lane: <lane name>
User question: <original user question>
Your search intent: <what this lane should prove/disprove>
Queries to try first:
- <query 1>
- <query 2>
- <query 3>

Tool policy:
1. Call ninerouter_status first.
2. Use ninerouter_web_search for discovery. Omit route unless user requested a route/combo.
3. Use ninerouter_web_fetch on top URLs needed to verify key claims.
4. If 9router tools are unavailable or fail after useful retries, fall back to direct tools: Brave for discovery, Tavily for extraction, Exa for semantic/technical/entity precision.
5. Do not return raw page dumps.

Return under 900 words using this exact schema:
## Lane
<lane name>

## Search intent
<one sentence>

## Queries tried
- <query>

## Evidence
- Claim: <short answer fragment>
  Source: <URL>
  Source type/date: <official docs|news|issue|forum|paper|pricing|unknown>, <date if available>
  Support: <short quote or page detail that proves the claim>
  Confidence: high|medium|low

## Conflicts
- <conflict or "None found"> with source URLs and dates when relevant

## Gaps
- <unverified area or "None material">

## Lane recommendation
<one short recommendation from this lane only>
```

If a subagent cannot access 9router and no fallback web tools are available, it should report the missing tools and the install/config action instead of hallucinating.

## Step 4: Synthesize Across Lanes

Read only subagent reports. Merge, deduplicate, and resolve conflicts. Prefer claims supported by official or multiple independent sources. Mark uncertainty when sources disagree or evidence is thin.

Use confidence labels consistently:
- **High**: multiple independent strong sources agree, or one authoritative primary source directly answers.
- **Medium**: one strong source, partial agreement, or current but incomplete evidence.
- **Low**: stale, indirect, anecdotal, or conflicting evidence.

For high-stakes or contradiction-heavy answers, run a final citation-audit subagent if needed. Ask it to check whether key claims have source URLs and supporting evidence, then drop or downgrade unsupported claims.

Do not bury citations in a reference list. Attach sources to claims inline:

> PostgreSQL refuses local TCP connections when the server is not listening on `127.0.0.1:5432`; verify with `pg_isready -h 127.0.0.1 -p 5432` (source: https://www.postgresql.org/docs/current/app-pg-isready.html)

## Output Structure

### Summary
2–3 sentences with the main answer and most important caveat.

### Findings
Organize by relevance. Each finding includes:
- what was found
- why it matters
- inline `(source: URL)` citations
- version/date context when recency matters
- code/config snippets when useful

### Recommendations
When there is a clear best path, state it directly and explain tradeoffs. For comparisons, include a small decision framework.

### Gaps
List what could not be verified, stale/conflicting evidence, missing official documentation, or assumptions.

### Research coverage
Briefly list:
- lanes run
- whether 9router was used or direct fallback was needed
- source types covered (official docs, news, issues, forums, etc.)

Keep this section short; it exists for transparency, not audit verbosity.

## Failure Handling

If the subagent tool is unavailable:

1. Do not perform direct research in the main context.
2. Answer with setup guidance:
   - install subagents: `pi install npm:@tintinweb/pi-subagents`
   - restart/reload Pi if needed
   - ask Pi to "Check whether subagents are configured correctly" or run `/subagents-doctor` when available

If `ninerouter_status` or both search/fetch tools are unavailable inside subagents:

1. Ask subagents to try direct fallback tools.
2. If direct tools also unavailable, answer with setup guidance only:
   - install `pi-9router-ext`: `pi install npm:pi-9router-ext`
   - configure `/9router-config`
   - verify `/9router-status`
   - ensure 9router exposes web routes from `GET /v1/models/web`

Never fabricate current facts when tools are unavailable.
