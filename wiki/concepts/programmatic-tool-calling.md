---
title: Programmatic Tool Calling
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [tools, runtime, architecture]
sources: [raw/articles/hermes-tools-and-memory-deep-dive-2026-04-08.md]
---

# Programmatic Tool Calling

Hermes' `execute_code` feature is best understood as programmatic tool calling, not unrestricted sandbox execution.

## Main idea

The model writes Python that can call a constrained allowlist of Hermes tools. This allows multi-step mechanical workflows to happen inside one inference turn while keeping intermediate steps out of the main context.

## Why it matters

It is a key efficiency feature and an important complement to [[delegation-and-subagents]].

## Related pages
- [[tool-system]]
- [[delegation-and-subagents]]
- [[terminal-and-processes]]
- [[agent-runtime]]
