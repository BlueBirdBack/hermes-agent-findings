# Raw Source: Hermes repository inventory and cloc snapshot

Date captured: 2026-04-08
Repository path: `/root/.hermes/hermes-agent/hermes-agent`

## cloc snapshot

- 1427 text files
- 1409 unique files
- 60 files ignored
- 444,594 lines of code

### Largest language buckets
- Python: 700 files, 231,626 code lines
- Markdown: 536 files, 145,300 code lines
- JSON: 23 files, 25,806 code lines
- XSD: 39 files, 19,654 code lines
- TeX: 30 files, 12,200 code lines

## Top-level file-count buckets
- tests: 444 files
- skills: 402 files
- website: 131 files
- optional-skills: 130 files
- tools: 68 files
- environments: 43 files
- hermes_cli: 41 files
- gateway: 33 files
- plugins: 32 files
- agent: 24 files

## Implication for wiki ingestion
A file-per-page wiki would be the wrong shape. The repo should be ingested by subsystem and architectural centrality, not by mirroring all 1409 files into wiki pages.

## Proposed ingestion priority buckets
1. Core architecture and entrypoints
2. Runtime internals
3. Tool system
4. Memory and persistence
5. CLI and gateway
6. Plugins and MCP
7. Cron and environments
8. Tests and docs as validation/context
9. Skills and optional-skills as catalog/reference material rather than page-per-skill ingestion
