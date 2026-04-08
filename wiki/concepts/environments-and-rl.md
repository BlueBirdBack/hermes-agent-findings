---
title: Environments and RL Integration
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [architecture, runtime, tools, research, codebase]
sources: [raw/articles/hermes-cron-environments-acp-deep-dive-2026-04-08.md]
---

# Environments and RL Integration

Hermes contains an Atropos-oriented environments subsystem for evaluation and RL-style tool-using rollouts.

## Main pieces
- environment base classes
- multi-turn agent loop for rollouts
- task-scoped tool continuity via task IDs
- verifier-facing ToolContext access
- benchmark-specific environment specializations

## Why it matters

This subsystem shows that Hermes is also a research/training platform, not just an interactive assistant runtime.

## Related pages
- [[agent-runtime]]
- [[terminal-and-processes]]
- [[repo-ecosystem]]
- [[testing-and-invariants]]
