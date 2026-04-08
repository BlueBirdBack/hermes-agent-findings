---
title: Memory Provider Architecture
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [memory, memory-provider, plugin, architecture]
sources: [raw/articles/hermes-tools-and-memory-deep-dive-2026-04-08.md]
---

# Memory Provider Architecture

Hermes supports external memory providers through a plugin interface layered on top of built-in file-backed memory.

## Main roles
- provider discovery and loading
- optional provider prompt blocks
- prefetch before turns
- post-turn sync
- provider-specific tools
- lifecycle hooks for compression, delegation, shutdown, and mirrored memory writes

## Key point

External providers are additive to built-in memory, and the runtime intends to keep only one active non-builtin provider at a time.

## Related pages
- [[memory-system]]
- [[built-in-memory-vs-external-memory]]
- [[tool-system]]
- [[hermes-agent]]
