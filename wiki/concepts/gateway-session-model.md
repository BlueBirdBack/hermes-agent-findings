---
title: Gateway Session Model
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [gateway, sessions, platform, persistence, architecture]
sources: [raw/articles/hermes-cli-gateway-config-deep-dive-2026-04-08.md]
---

# Gateway Session Model

Hermes has a deterministic gateway session model built around stable session keys and explicit reset policy.

## Main responsibilities
- map platform/chat/thread/user context to stable session keys
- decide when to reset by idle, daily, both, or never
- keep gateway-facing routing state aligned with durable transcript storage
- avoid duplicate running agents for the same session

## Key point

The gateway is not just transport glue. It is a real orchestration layer over active multi-platform conversations.

## Related pages
- [[cli-and-gateway]]
- [[persistence-and-sessions]]
- [[configuration-architecture]]
- [[profiles]]
