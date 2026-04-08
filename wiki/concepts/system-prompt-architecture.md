---
title: System Prompt Architecture
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [prompt, prompt-caching, runtime, architecture]
sources: [raw/articles/hermes-runtime-and-persistence-deep-dive-2026-04-08.md, raw/articles/hermes-readme-and-agents-2026-04-08.md]
---

# System Prompt Architecture

Hermes treats system-prompt construction as a stable layered artifact rather than a string rebuilt casually every turn.

## Main layers

The prompt is assembled from:
- identity material such as `SOUL.md`
- explicit system instructions
- built-in memory and user profile blocks
- optional external memory provider prompt blocks
- skills prompt/index material
- project context files such as `AGENTS.md`
- session, provider, model, and platform metadata

## Important design choice

Hermes prefers to keep the core system prompt stable across a session. Ephemeral context is often injected only at API-call time rather than persisted into canonical history.

## Why it matters

This architecture supports [[prompt-caching]] and reduces accidental mid-session drift in agent behavior.

## Related pages
- [[prompt-caching]]
- [[agent-runtime]]
- [[memory-system]]
- [[hermes-agent]]
