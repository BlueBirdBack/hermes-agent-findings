---
title: Testing and Invariants
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [testing, architecture, docs, codebase]
sources: [raw/articles/hermes-repo-inventory-and-cloc-2026-04-08.md]
---

# Testing and Invariants

Hermes has an unusually large test surface, and that test surface is one of the clearest signals of what the maintainers consider non-negotiable.

## What the tests are useful for
- discovering architectural invariants
- finding safety boundaries
- understanding provider quirks
- understanding profile, memory, process, and gateway edge cases

## Why it matters

In a large repo like Hermes, tests are not just verification; they are part of the architecture documentation.

## Related pages
- [[hermes-agent]]
- [[profiles]]
- [[prompt-caching]]
- [[tool-system]]
