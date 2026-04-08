---
title: Terminal and Background Processes
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [tools, background-process, persistence, architecture]
sources: [raw/articles/hermes-tools-and-memory-deep-dive-2026-04-08.md]
---

# Terminal and Background Processes

Hermes treats terminal execution as managed environment interaction rather than raw shelling out.

## Main features
- multiple terminal backends
- per-task environment/session management
- approval checks for dangerous commands
- output sanitization and redaction
- explicit background process registry
- polling, logs, stdin writing, kill, and recovery metadata

## Why it matters

This subsystem is part of Hermes' continuity story: work can continue across turns, and process state is modeled rather than forgotten.

## Related pages
- [[tool-system]]
- [[persistence-and-sessions]]
- [[cli-and-gateway]]
- [[hermes-agent]]
