# Raw Source: Hermes runtime and persistence deep dive

Date captured: 2026-04-08
Source files:
- run_agent.py
- agent/prompt_builder.py
- agent/context_compressor.py
- agent/prompt_caching.py
- hermes_state.py
- agent/trajectory.py

Key extracted findings:
- `AIAgent` is the orchestration hub and separates stable persisted session state from ephemeral API-call-time context injection.
- System prompt assembly is layered and intentionally stable across a session.
- Continuing sessions try to reuse stored system-prompt snapshots from SQLite for cache friendliness.
- Context compression is a structured feature with tool-pair preservation, not simple truncation.
- SQLite persistence is dual-path with session JSON logs plus `state.db` as the durable searchable store.
- `state.db` uses WAL mode, FTS5, rich token/cost columns, parent session lineage, and reasoning persistence.
- Compression creates child sessions linked via `parent_session_id` and rebuilds the system prompt for the new lineage branch.
- Prompt caching is implemented as a narrow API-boundary concern rather than as a mutation of canonical transcript state.
