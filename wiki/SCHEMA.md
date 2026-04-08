# Wiki Schema

## Domain
Hermes Agent codebase research. This wiki covers the architecture, runtime, memory system, tool system, CLI, gateway, persistence layer, and notable implementation patterns of the Hermes Agent repository.

## Conventions
- File names: lowercase, hyphens, no spaces (e.g., `agent-runtime.md`)
- Every wiki page starts with YAML frontmatter
- Use `[[wikilinks]]` between pages; aim for at least 2 outbound links per page
- When updating a page, always bump the `updated` date
- Every new wiki page must be added to `index.md`
- Every material action must be appended to `log.md`
- Raw sources under `raw/` are immutable snapshots
- Prefer synthesis over duplication; update existing pages before creating new ones

## Frontmatter
```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | query | summary
tags: [from taxonomy below]
sources: [raw/articles/source-name.md]
---
```

## Tag Taxonomy
- runtime
- agent-loop
- prompt
- prompt-caching
- context-compression
- memory
- memory-provider
- tools
- tool-registry
- mcp
- plugin
- cli
- gateway
- platform
- persistence
- sqlite
- sessions
- auth
- models
- provider
- profiles
- background-process
- architecture
- testing
- docs
- research
- codebase

Rule: every tag on a page must appear in this taxonomy. Add new tags here before using them.

## Page Thresholds
- Create a page when an entity or concept is central to the codebase or appears repeatedly across sources
- Add to an existing page when the topic is already covered
- Do not create pages for passing mentions or low-signal details
- Split a page when it exceeds ~200 lines
- Archive a page when it is superseded

## Entity Pages
For concrete subsystems, files, or named components. Include:
- what it is
- its responsibilities
- important relationships to other components
- relevant source references

## Concept Pages
For cross-cutting ideas and design patterns. Include:
- definition
- how it appears in Hermes
- why it matters
- related concepts

## Comparison Pages
For side-by-side analyses, such as CLI vs gateway or built-in memory vs external memory providers.

## Update Policy
When new information conflicts with existing content:
1. Check dates and source proximity to implementation
2. If still contradictory, note both positions with sources
3. Mark contradictions in the page body and flag in future lint passes
