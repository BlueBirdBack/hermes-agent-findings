---
title: Plugin System
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [plugin, architecture, tools, codebase]
sources: [raw/articles/hermes-plugins-docs-and-product-surface-2026-04-08.md]
---

# Plugin System

Hermes has a general plugin system plus a specialized memory-provider plugin layer.

## General plugins
General plugins can provide tools, hooks, CLI commands, injected content, bundled data, and bundled skills.

## Specialized memory providers
Memory providers are a constrained plugin tier with a dedicated lifecycle and a one-active-provider model layered on top of built-in memory.

## Why it matters

The plugin system is one of the main ways Hermes expands capability without forcing every feature into the runtime core.

## Related pages
- [[tool-system]]
- [[memory-provider-architecture]]
- [[repo-ecosystem]]
- [[skills-ecosystem]]
