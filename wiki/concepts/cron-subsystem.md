---
title: Cron Subsystem
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [architecture, persistence, cli, gateway]
sources: [raw/articles/hermes-cron-environments-acp-deep-dive-2026-04-08.md]
---

# Cron Subsystem

Hermes includes a file-backed scheduler for one-shot and recurring autonomous runs.

## Main responsibilities
- parse and persist job schedules
- determine due jobs safely
- execute AIAgent runs in cron context
- persist outputs
- optionally deliver results back to chats or channels

## Notable design choice

Recurring jobs are pre-advanced before execution to favor at-most-once semantics over replaying missed runs after failure or restart.

## Related pages
- [[hermes-agent]]
- [[configuration-architecture]]
- [[persistence-and-sessions]]
- [[gateway-session-model]]
