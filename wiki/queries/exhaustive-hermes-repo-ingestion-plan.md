---
title: Exhaustive Hermes Repo Ingestion Plan
created: 2026-04-08
updated: 2026-04-08
type: query
tags: [query, research, codebase, architecture, docs]
sources: [raw/articles/hermes-repo-inventory-and-cloc-2026-04-08.md]
---

# Exhaustive Hermes Repo Ingestion Plan

This plan aims for exhaustive understanding without creating one wiki page per file.

## Why not one page per file?

The repository has roughly 1409 unique text files and about 444k lines of code. A file-mirror wiki would be noisy, redundant, and hard to navigate. The wiki should capture durable understanding, not reproduce the repository tree.

## Correct ingestion model

### Layer 1: raw source capture
Store grouped raw sources for important files and batches.

Examples:
- one raw source for README + AGENTS
- one raw source for runtime core files
- one raw source for memory-related files
- one raw source for gateway/session files
- one raw source for CLI/config/auth files

### Layer 2: synthesized wiki pages
Create or update pages for:
- core entities
- major concepts
- important comparisons
- reusable query answers

## Exhaustive ingestion phases

### Phase 1 — Core architectural spine
Read and synthesize these first:
- `README.md`
- `AGENTS.md`
- `run_agent.py`
- `model_tools.py`
- `tools/registry.py`
- `hermes_state.py`
- `cli.py`
- `hermes_cli/main.py`
- `gateway/run.py`
- `gateway/session.py`

Expected output:
- deepen existing pages like [[agent-runtime]], [[tool-system]], [[memory-system]], [[cli-and-gateway]], and [[persistence-and-sessions]]
- add file-centric pages only where the file is architecturally central

### Phase 2 — Runtime internals
Read and group these:
- `agent/prompt_builder.py`
- `agent/context_compressor.py`
- `agent/prompt_caching.py`
- `agent/auxiliary_client.py`
- `agent/model_metadata.py`
- `agent/models_dev.py`
- `agent/trajectory.py`

Expected output:
- strengthen [[agent-runtime]] and [[prompt-caching]]
- possibly add concept pages for prompt assembly or context compression details

### Phase 3 — Memory and persistence
Read and group these:
- `agent/memory_manager.py`
- `agent/memory_provider.py`
- `agent/builtin_memory_provider.py`
- `tools/memory_tool.py`
- `tools/session_search_tool.py`
- memory provider plugins under `plugins/memory/`

Expected output:
- deepen [[memory-system]]
- add comparison pages for built-in memory vs session search vs external providers
- possibly add a page for memory provider architecture

### Phase 4 — CLI, config, auth, model switching
Read and group these:
- `hermes_cli/config.py`
- `hermes_cli/auth.py`
- `hermes_cli/model_switch.py`
- `hermes_cli/commands.py`
- `hermes_cli/skin_engine.py`
- related CLI helpers

Expected output:
- deepen [[cli-and-gateway]] and [[profiles]]
- maybe add pages for provider resolution or config architecture

### Phase 5 — Tool architecture in depth
Read and group these:
- high-signal tools in `tools/`
- terminal/process tools
- browser tools
- delegate/code execution tools
- MCP integration tools

Expected output:
- deepen [[tool-system]]
- add pages for terminal backend architecture, delegation, MCP, and tool safety patterns

### Phase 6 — Gateway and platforms
Read and group these:
- `gateway/config.py`
- `gateway/status.py`
- `gateway/delivery.py`
- selected platform adapters

Expected output:
- deepen [[cli-and-gateway]] and [[persistence-and-sessions]]
- add comparisons or pages for gateway orchestration and platform abstractions

### Phase 7 — Tests and docs for invariant extraction
Do not create a page per test. Instead, use tests to learn invariants.

Priority:
- tests for prompt caching
- tests for profile handling
- tests for memory tools
- tests for process registry
- tests for browser/tool safety

Expected output:
- refinement of existing pages with stronger claims about repo invariants
- maybe a concept page for testing philosophy

### Phase 8 — Skills and website docs as reference layer
The repo has hundreds of skill/doc files. These should mostly be treated as catalogs, examples, and product surface area — not each turned into a wiki page.

Expected output:
- one or a few summary pages about the skills ecosystem
- one page about website/docs as documentation surface

## Batch strategy

For exhaustive ingestion, process the repo by subsystem batches, not by alphabetical file order.

Recommended batch order:
1. core files
2. agent/
3. tools/
4. hermes_cli/
5. gateway/
6. plugins/
7. cron/ + environments/
8. tests/
9. docs/ + website/
10. skills/ + optional-skills/

## Page creation rules during exhaustive ingestion

Create a new wiki page only when:
- the file or subsystem is central to architecture
- multiple sources converge on the same concept
- the knowledge will be reused repeatedly

Do not create a page when:
- the file is a thin utility
- it is a leaf implementation detail
- its content fits naturally as a section in an existing page
- it is one of many similar tests or skills with no unique architectural significance

## What exhaustive means here

Exhaustive does not mean one page per file.
It means every important subsystem is eventually represented in the wiki, with raw-source coverage broad enough that the wiki can answer architectural questions without re-reading the repo from scratch.

## Best next concrete step

Next ingest batch:
- `run_agent.py`
- `model_tools.py`
- `tools/registry.py`
- `hermes_state.py`
- `agent/memory_manager.py`
- `tools/memory_tool.py`

That batch would deepen the highest-value parts of the wiki fastest.

## Related pages
- [[hermes-agent]]
- [[agent-runtime]]
- [[tool-system]]
- [[memory-system]]
- [[persistence-and-sessions]]
- [[prompt-caching]]
- [[profiles]]
