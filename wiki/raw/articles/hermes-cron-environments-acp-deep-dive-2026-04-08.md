# Raw Source: Hermes cron, environments, and ACP deep dive

Date captured: 2026-04-08
Source files:
- cron/jobs.py
- cron/scheduler.py
- environments/README.md
- environments/hermes_base_env.py
- environments/agent_loop.py
- environments/tool_context.py
- environments/patches.py
- representative benchmark environment files
- acp_adapter/server.py
- acp_adapter/session.py
- acp_adapter/tools.py
- acp_adapter/auth.py
- acp_adapter/entry.py

Key extracted findings:
- Cron is a file-backed scheduler with structured job models, persistent output, delivery routing, and at-most-once recurring execution semantics.
- Cron runs AIAgent in a constrained `platform="cron"` context with disabled memory and some toolsets.
- The environments subsystem is an Atropos integration layer for evaluation and RL workflows built around task-scoped tool continuity.
- `HermesAgentLoop` is the environment-side multi-turn tool-calling engine.
- `ToolContext` exposes the same rollout task state to reward/verifier code.
- ACP exposes Hermes as an Agent Client Protocol server for editor integrations.
- ACP sessions are persisted and restorable, with shared Hermes runtime semantics and curated tool exposure.
