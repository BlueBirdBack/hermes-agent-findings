# Raw Source: Hermes code reading notes

Date captured: 2026-04-08
Source type: internal research notes

This raw source captures the current synthesized understanding gathered from reading the Hermes Agent repository in full.

Key observations:
- Hermes is centered on `AIAgent` in `run_agent.py`
- The tool registry and toolset system form the main extensibility spine
- The gateway is a major orchestration layer, not a thin wrapper
- Built-in memory is small, curated, and injected as a frozen system-prompt snapshot
- External memory providers are additive and constrained to one active non-builtin provider at a time
- SQLite persistence with FTS5 search and session lineage is a core subsystem
- Prompt caching and profile-safe path handling are repo-wide invariants
- Hermes is designed for continuity across sessions, interfaces, and long-running tasks
