---
title: Tool System
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [tools, tool-registry, mcp, plugin, architecture, runtime]
sources: [raw/articles/hermes-code-reading-notes-2026-04-08.md]
---

# Tool System

Hermes uses a centralized registry-driven tool architecture.

## Main pattern

Tool modules register themselves through the central registry when imported. The runtime then filters and exposes available tools by toolset, and dispatches model tool calls through a common handler.

## Important characteristics

- registration is import-driven
- toolsets are the main capability boundary
- schema, handler, requirements, and metadata live together
- dispatch includes argument coercion and error normalization
- MCP and plugin-discovered tools extend the same general surface

## Why it matters

This is the most important extensibility seam in the repo. New capability usually fits best by integrating with the existing registry and toolset model.

## Related pages
- [[agent-runtime]]
- [[cli-and-gateway]]
- [[memory-system]]
- [[hermes-agent]]
