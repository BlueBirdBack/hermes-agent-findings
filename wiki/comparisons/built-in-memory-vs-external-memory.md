---
title: Built-in Memory vs External Memory Providers
created: 2026-04-08
updated: 2026-04-08
type: comparison
tags: [memory, memory-provider, comparison, architecture]
sources: [raw/articles/hermes-code-reading-notes-2026-04-08.md]
---

# Built-in Memory vs External Memory Providers

## Comparison table

| Dimension | Built-in memory | External memory provider |
| --- | --- | --- |
| Storage | `MEMORY.md` and `USER.md` | Provider-specific backend |
| Scope | Small curated facts | Richer recall and modeling |
| Prompt behavior | Injected as frozen snapshot | Can add prompt blocks and prefetch recall |
| Write timing | Immediate file persistence | Provider-defined sync strategy |
| Availability | Always on | Optional, one external provider at a time |
| Tooling | Agent-level memory tool | Provider-specific tools |

## Synthesis

Built-in memory gives Hermes a compact always-available memory layer. External providers extend that with richer retrieval, semantic recall, or user modeling. The repo deliberately keeps built-in memory always active and limits external provider count to one active non-builtin provider.

## Related pages
- [[memory-system]]
- [[persistence-and-sessions]]
- [[hermes-agent]]
