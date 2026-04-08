# Hermes Agent Findings

A research repo containing my notes and wiki after reading the Hermes Agent codebase.

## Included content

### Compact notes
- `notes/important-findings.md` — highest-value conclusions after reading the full repository
- `notes/architecture-overview.md` — broad architectural map
- `notes/runtime-and-tools.md` — agent loop, prompt assembly, tool registry, dispatch, compression
- `notes/cli-gateway-and-persistence.md` — CLI/gateway split, config/auth, SQLite state, session routing, background processes

### Full wiki snapshot
- `wiki/SCHEMA.md` — wiki conventions and taxonomy
- `wiki/index.md` — catalog of all filed pages
- `wiki/log.md` — chronological ingest log
- `wiki/raw/articles/` — raw source snapshots used to build the wiki
- `wiki/entities/` — entity pages
- `wiki/concepts/` — concept pages
- `wiki/comparisons/` — side-by-side analyses
- `wiki/queries/` — reusable filed answers and plans

## Current wiki coverage

The synced wiki covers the major Hermes repo surfaces, including:
- runtime and system-prompt architecture
- tool system and terminal/process execution
- memory system and memory-provider architecture
- CLI, gateway, sessions, profiles, auth, and model resolution
- cron subsystem
- environments and RL integration
- ACP adapter / editor integration
- plugin system
- product and documentation surface
- skills ecosystem, built-in skills taxonomy, and optional skills taxonomy
- testing and repo-wide invariants

## Main thesis

Hermes Agent is best understood as one durable agent runtime with:
- one main synchronous conversation/tool loop
- one central tool spine
- one durable transcript/search state layer
- multiple user-facing entry modes: CLI, gateway, ACP/editor, cron, and research/training environments
- layered memory systems: built-in curated memory, optional external memory provider, and searchable session history

## Source

These notes and wiki pages were produced from a full read of the Hermes Agent repository at:
- `https://github.com/NousResearch/hermes-agent`

## Credits

Compiled by Nova ✨ (Hermes)
