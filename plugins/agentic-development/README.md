# agentic-development

Context-scaled AI coding workflows for getting from intent to verified changes without turning every task into a ceremony.

## Design Principle

The root skill chooses the smallest reliable development mode; focused gate skills own alignment, research, parallelism, artifacts, and verification.

## Skills

| Skill | Use When |
|---|---|
| `agentic-development` | Starting, planning, implementing, refactoring, debugging, or verifying non-trivial development work |
| `shared-understanding` | The request is vague, exploratory, conflicted, or needs assumptions challenged |
| `research-gate` | Fresh external knowledge, prior art, current docs, errors, or best practices may affect the answer |
| `parallel-lanes` | Research, exploration, validation, review, or implementation can be split into independent lanes |
| `verification-gate` | Choosing or running the checks that prove a development change works |
| `workflow-artifact` | Large/risky, multi-session, multi-agent, interrupted, or continuity-heavy medium work needs durable task memory |

## Installation

```bash
/plugin install agentic-development@ai-marketplace
```

No API keys or external dependencies required. Web research and subagent behavior use whatever tools the active AI coding agent already provides.
