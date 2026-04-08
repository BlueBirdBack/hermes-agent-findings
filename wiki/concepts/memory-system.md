---
title: Memory System
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [memory, memory-provider, sessions, sqlite, architecture, research]
sources: [raw/articles/hermes-code-reading-notes-2026-04-08.md]
---

# Memory System

Hermes has a layered memory model rather than a single memory feature.

## Layers

### Built-in curated memory
Two small file-backed stores hold durable compact memory:
- `MEMORY.md` for environment and project facts
- `USER.md` for user preferences and profile information

This memory is injected as a frozen snapshot at session start. Mid-session writes persist immediately to disk but do not alter the current system prompt.

### External memory provider
Hermes supports one active non-builtin memory provider at a time, alongside the built-in memory. These providers can prefetch recall, sync turns, expose tools, and add richer cross-session modeling.

### Session search
Hermes also keeps full session history in SQLite with FTS5. This is broad searchable history rather than small always-in-context memory.

## Why it matters

The layered design gives Hermes:
- small always-available memory
- richer optional provider memory
- large cold searchable history

## Related pages
- [[persistence-and-sessions]]
- [[agent-runtime]]
- [[prompt-caching]]
- [[cli-and-gateway]]
- [[hermes-agent]]
