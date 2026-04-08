---
title: Skills Ecosystem
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [docs, research, codebase, tools]
sources: [raw/articles/hermes-skills-ecosystem-deep-dive-2026-04-08.md]
---

# Skills Ecosystem

Hermes uses skills as a major capability-scaling layer.

## Main split
- built-in skills: curated, seeded into installs by default
- optional skills: official but dormant extensions for niche, experimental, or setup-heavy workflows
- external/community skills: distributed through Skills Hub style mechanisms

## Architectural role

Skills are metadata-driven prompt modules with progressive disclosure and supporting files loaded on demand. They are lighter-weight than plugins and let Hermes expand domains without pushing all capability into Python runtime code.

## Why it matters

The skills ecosystem is one of Hermes' main differentiators and one of the clearest signs that the product is designed for procedural self-improvement and wide domain coverage.

## Related pages
- [[plugin-system]]
- [[repo-ecosystem]]
- [[product-and-documentation-surface]]
- [[hermes-agent]]
