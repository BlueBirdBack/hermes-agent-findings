# Wiki Index

> Content catalog for the Hermes Agent codebase wiki.
> Last updated: 2026-04-08 | Total pages: 29

## Entities
- [[hermes-agent]] — Top-level page for the Hermes Agent system and its major subsystems.

## Concepts
- [[acp-adapter]] — ACP-based editor integration for VS Code, Zed, JetBrains, and other ACP clients.
- [[agent-runtime]] — The central `AIAgent` loop and its role in conversation orchestration.
- [[auth-and-model-resolution]] — Authentication state, provider resolution, model normalization, and switching pipeline.
- [[built-in-skills-taxonomy]] — Summary of the built-in curated skills corpus.
- [[cli-and-gateway]] — The two primary user-facing entry modes and how they connect to the shared runtime.
- [[configuration-architecture]] — Canonical config plus runtime env-bridging compatibility layers.
- [[cron-subsystem]] — File-backed scheduling and autonomous recurring/one-shot job execution.
- [[delegation-and-subagents]] — Isolated child-agent execution for delegated tasks.
- [[environments-and-rl]] — Atropos-style evaluation and RL integration layer.
- [[gateway-session-model]] — Stable session-key and reset-policy model for messaging platforms.
- [[memory-provider-architecture]] — Plugin model for additive external memory providers.
- [[memory-system]] — Hermes' layered memory design: built-in curated memory, external providers, and session search.
- [[optional-skills-taxonomy]] — Summary of official in-repo but non-default skills.
- [[persistence-and-sessions]] — Durable SQLite state, session routing, and continuity-oriented storage design.
- [[plugin-system]] — General plugins plus specialized memory-provider plugins.
- [[product-and-documentation-surface]] — Hermes as a documented platform product across user, developer, and integration docs.
- [[profiles]] — Multi-instance isolation through `HERMES_HOME` and profile-safe path handling.
- [[programmatic-tool-calling]] — `execute_code` as constrained multi-step tool orchestration.
- [[prompt-caching]] — Prompt stability as a core architectural constraint affecting runtime design.
- [[repo-ecosystem]] — The wider repo surface: tests, skills, docs, plugins, environments, and more.
- [[skills-ecosystem]] — Skills as a major capability-scaling layer across built-in, optional, and external sources.
- [[system-prompt-architecture]] — How Hermes layers and stabilizes system-prompt construction.
- [[terminal-and-processes]] — Managed terminal execution and background process tracking.
- [[testing-and-invariants]] — Tests as a map of repo invariants and safety boundaries.
- [[tool-system]] — The registry-driven tool architecture and main extensibility seam.

## Comparisons
- [[built-in-memory-vs-external-memory]] — Side-by-side comparison of Hermes' built-in memory and optional external providers.

## Queries
- [[exhaustive-hermes-repo-ingestion-plan]] — Structured plan for exhaustive repo research without creating one page per file.
- [[what-is-hermes-agent]] — Reusable orientation answer describing Hermes at a high level.
