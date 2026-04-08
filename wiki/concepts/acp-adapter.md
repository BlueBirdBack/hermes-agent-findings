---
title: ACP Adapter
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [architecture, gateway, cli, tools, codebase]
sources: [raw/articles/hermes-cron-environments-acp-deep-dive-2026-04-08.md]
---

# ACP Adapter

Hermes exposes itself through Agent Client Protocol for editor integrations such as VS Code, Zed, and JetBrains.

## Main responsibilities
- manage ACP sessions mapped to Hermes sessions
- run AIAgent under ACP-facing lifecycle and callbacks
- advertise commands and curated tool surfaces to clients
- persist and restore ACP sessions through Hermes state storage

## Why it matters

ACP is a first-class interface channel alongside the CLI and messaging gateway.

## Related pages
- [[cli-and-gateway]]
- [[gateway-session-model]]
- [[tool-system]]
- [[configuration-architecture]]
