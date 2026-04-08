---
title: Agent Runtime
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [runtime, agent-loop, prompt, prompt-caching, context-compression, architecture]
sources: [raw/articles/hermes-code-reading-notes-2026-04-08.md]
---

# Agent Runtime

The runtime core of Hermes is the `AIAgent` loop in `run_agent.py`.

## What it does

The agent runtime:
- builds or restores the system prompt
- appends user messages to transcript state
- prepares provider-facing payloads
- calls the model
- normalizes model responses into a common internal format
- executes tool calls and appends tool results
- repeats until a final non-tool response is produced

## Why it matters

This is the control center of the entire repo. Nearly every other major subsystem exists to support, constrain, or extend this loop.

## Important implementation ideas

- Hermes keeps a normalized internal message format and translates at provider boundaries
- Prompt assembly is layered rather than monolithic
- [[prompt-caching]] is treated as an important product constraint
- [[context-compression]] preserves long-running conversations without throwing away core context

## Related pages
- [[hermes-agent]]
- [[tool-system]]
- [[memory-system]]
- [[prompt-caching]]
- [[persistence-and-sessions]]
