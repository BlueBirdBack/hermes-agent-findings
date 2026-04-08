---
title: Prompt Caching
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [prompt, prompt-caching, architecture, runtime]
sources: [raw/articles/hermes-readme-and-agents-2026-04-08.md]
---

# Prompt Caching

Prompt caching is a major implementation constraint in Hermes rather than a small optimization.

## Core rule

The AGENTS guide explicitly warns against changes that would alter past context or rebuild the system prompt mid-conversation except in controlled compression flows.

## Why it matters

Hermes keeps a stable prompt prefix so repeated turns can benefit from cache hits. This shapes how memory, skill injection, and context assembly are implemented.

## Design implications

- built-in memory is injected as a frozen snapshot at session start
- ephemeral context is often injected later rather than rebuilding the prompt core
- prompt-stability concerns affect runtime architecture decisions

## Related pages
- [[agent-runtime]]
- [[memory-system]]
- [[hermes-agent]]
