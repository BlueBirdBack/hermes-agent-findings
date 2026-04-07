# Hermes Agent Findings

A compact repo of my notes after reading the Hermes Agent codebase in full.

## Included notes

- `notes/important-findings.md` — highest-value conclusions after reading the full repository
- `notes/architecture-overview.md` — broad architectural map
- `notes/runtime-and-tools.md` — agent loop, prompt assembly, tool registry, dispatch, compression
- `notes/cli-gateway-and-persistence.md` — CLI/gateway split, config/auth, SQLite state, session routing, background processes

## Main thesis

Hermes Agent is best understood as one durable agent runtime with:

- one main synchronous conversation/tool loop
- one central tool spine
- one durable transcript/search state layer
- two primary user-facing entry modes: CLI and gateway
- layered memory systems: built-in curated memory, optional external memory provider, and searchable session history

## Biggest takeaways

- `AIAgent` is still the architectural center.
- Tool execution is part of the core loop, not an add-on.
- Prompt-cache stability strongly shapes implementation choices.
- Profile-safe path handling is a repo-wide invariant.
- Memory is layered: small curated memory + optional external provider + large searchable history.
- The gateway is a serious orchestration layer, not a thin platform wrapper.
- Hermes is optimized for continuity across sessions, interfaces, and long-running tasks.

## Source

These notes were produced from a full read of the Hermes Agent repository.
