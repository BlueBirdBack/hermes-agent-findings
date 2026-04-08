---
title: Delegation and Subagents
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [tools, runtime, architecture, research]
sources: [raw/articles/hermes-tools-and-memory-deep-dive-2026-04-08.md]
---

# Delegation and Subagents

Hermes delegation creates isolated child agents rather than merely splitting prompts.

## Main properties
- fresh child sessions
- restricted tool access
- blocked sensitive/meta tools
- limited depth and parallelism
- parent-only visibility of final summaries
- child sessions usually skip memory and context files

## Why it matters

Delegation is one of the repo's most important scalability features for reasoning-heavy work without flooding the parent context.

## Related pages
- [[tool-system]]
- [[agent-runtime]]
- [[memory-system]]
- [[programmatic-tool-calling]]
