---
title: Persistence and Sessions
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [persistence, sqlite, sessions, gateway, background-process, architecture]
sources: [raw/articles/hermes-code-reading-notes-2026-04-08.md]
---

# Persistence and Sessions

Hermes uses a durable persistence layer rather than ephemeral chat history.

## Core storage

`hermes_state.py` stores sessions and messages in SQLite with FTS5 search. It also keeps metadata such as model, costs, token counts, parent session lineage, and system prompt snapshots.

## Session routing

`gateway/session.py` manages active chat identity for messaging platforms. This is distinct from the SQLite database: it is the routing layer for active conversations, not the only source of truth.

## Continuity focus

The persistence architecture supports:
- searchable history
- long-running agent workflows
- background process continuity
- cross-interface continuity
- session lineage across compression or resets

## Related pages
- [[memory-system]]
- [[cli-and-gateway]]
- [[agent-runtime]]
- [[hermes-agent]]
