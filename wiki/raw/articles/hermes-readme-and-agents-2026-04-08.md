# Raw Source: Hermes README and AGENTS guide

Date captured: 2026-04-08
Source path: /root/.hermes/hermes-agent/hermes-agent
Source files:
- README.md
- AGENTS.md

Key extracted facts:
- Hermes Agent positions itself as a self-improving AI agent with memory, skills, session search, cron scheduling, delegation, and multiple terminal backends.
- The top-level architecture centers on `AIAgent` in `run_agent.py`, with tool orchestration in `model_tools.py`, registry logic in `tools/registry.py`, interactive CLI in `cli.py`, shell entrypoint logic in `hermes_cli/main.py`, and messaging orchestration in `gateway/run.py`.
- The AGENTS guide emphasizes prompt-cache stability: the system prompt should not be rebuilt mid-session except for controlled compression flows.
- The AGENTS guide emphasizes profile-safe path handling via `get_hermes_home()` and `display_hermes_home()` rather than hardcoded `~/.hermes` paths.
- The tool system is explicitly registry-driven and toolset-scoped.
- The codebase treats CLI and gateway as two major interfaces over the same runtime.
- The persistence model includes SQLite session storage with FTS5 search and continuity-oriented session handling.
- The repository contains a large automated test suite and expects full-suite testing before pushes.
