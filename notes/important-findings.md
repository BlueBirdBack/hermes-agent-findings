# Important Findings After Reading the Full Repository

## 1) The real center of the system is still `AIAgent`
Even though the repo has a lot of surface area, the architectural center is still the synchronous message/tool loop in `run_agent.py`.

What matters most:
- nearly every interface eventually funnels into `AIAgent`
- the main abstraction is a normalized conversation transcript, not a one-off prompt
- tool calling is part of the default control flow, not a side feature
- session continuity, context compression, and persistence are built around keeping that loop alive for long-running work

Practical takeaway: when trying to understand or change Hermes safely, start from the agent loop and work outward.

## 2) Hermes is designed around one normalized internal format
A recurring pattern across the repo is:
- normalize messages internally
- adapt only at provider or platform boundaries
- keep durable state richer than any single provider API requires

This shows up in:
- OpenAI-style internal messages with extra reasoning/tool metadata
- provider-specific adapters layered on top of the shared transcript format
- gateway session routing that preserves chat continuity while letting storage remain provider-agnostic

Practical takeaway: the project prefers translation layers over provider-specific forks of the core runtime.

## 3) The tool registry is the main extensibility spine
`tools/registry.py` plus `model_tools.py` forms one of the strongest architectural seams in the project.

Key patterns:
- tool modules self-register on import
- discovery is import-driven
- toolsets are the primary capability boundary
- registry metadata carries schemas, handlers, requirements, emojis, and availability checks
- dispatch is centralized, including type coercion and error wrapping
- MCP discovery and plugin discovery extend the same general tool surface

Practical takeaway: if you want to add major capability, the least disruptive path is usually fit into the existing registry and toolset model rather than adding a parallel execution path.

## 4) Sync runtime + async tools is a deliberate design constraint
The top-level agent loop is synchronous, but the repo contains a lot of async-capable integrations.

Important finding:
- the repo has explicit event-loop bridging logic to avoid the classic `Event loop is closed` failures that happen when cached async clients outlive short-lived loops
- this is not accidental glue; it is a recurring engineering concern and is handled centrally

Practical takeaway: sync/async boundary bugs are a first-class maintenance risk in this codebase. Any new async integration should follow the existing bridging patterns rather than inventing a new lifecycle.

## 5) Persistence is much deeper than just chat history
`hermes_state.py` is not a simple transcript logger.

Important properties:
- SQLite with WAL mode
- FTS5 search over messages
- session lineage via parent session chains
- stored token/cost metadata
- system prompt snapshots
- reasoning/tool metadata retention
- retry logic with jitter to reduce SQLite lock convoy problems under contention

Practical takeaway: state storage is part of the product, not just an implementation detail. Changes here affect search, recovery, cost accounting, and session continuity.

## 6) The gateway is a real orchestration layer, not a thin wrapper
`gateway/run.py` is huge because the gateway is doing real work:
- env/config bootstrapping
- platform adapter lifecycle
- session routing
- agent caching
- command dispatch
- background-process update delivery
- recovery and cleanup
- platform-specific behavior smoothing

Practical takeaway: messaging support is not bolted on. Hermes is effectively a multi-interface agent platform where CLI and gateway are peer entry points into the same runtime.

## 7) Profiles are one of the repo’s most important invariants
The AGENTS guide is very explicit here, and the codebase backs that up.

Critical rule:
- code must use `get_hermes_home()` for state paths
- user-facing strings should use `display_hermes_home()`
- hardcoding `~/.hermes` is considered a known historical source of bugs

Practical takeaway: profile-safety is a repo-wide invariant. A seemingly harmless path literal can create real multi-profile bugs.

## 8) Prompt caching stability strongly shapes implementation choices
The repo repeatedly protects prompt-cache friendliness.

Observed philosophy:
- keep the stable system prompt stable
- avoid mid-conversation prompt rebuilding except for explicit compression flows
- inject ephemeral additions in ways that preserve cache hits when possible

Practical takeaway: some code may look more indirect than necessary because cache preservation is a product requirement, not a micro-optimization.

## 9) Skills and memory are product-defining, not decorative
The README promise is reflected in the implementation.

Important finding:
- the system treats memory, user profile, skills, session search, and self-improvement workflows as core features
- there are dedicated tools, storage paths, commands, and docs for them
- skill loading and memory injection are part of normal prompt assembly

Practical takeaway: Hermes is built for longitudinal use. Features that help the agent remember, retrieve, and refine behavior are central to its identity.

## 10) The repo is unusually committed to operational continuity
A lot of components point to the same design goal: keep work alive across time and interfaces.

Examples:
- background process registry with recovery metadata
- gateway session stores and reset policies
- cron jobs with delivery targets
- durable SQLite state
- context compression for long conversations
- profile isolation
- multiple terminal backends including remote/serverless ones

Practical takeaway: Hermes is architected less like a chatbot and more like a durable operator that users return to.

## 11) Testing is not an afterthought; it is part of the architecture
The repository has a very large test suite and many tests target subtle architectural edges, including:
- prompt caching
- tool arg coercion
- browser security boundaries
- process recovery
- profile behavior
- plugin behavior
- provider-specific quirks
- async bridging
- compression correctness

Practical takeaway: tests are one of the best ways to infer which invariants the maintainers consider non-negotiable.

## 12) The docs and code are unusually aligned
In many repos, docs are aspirational. Here, a lot of the architecture docs, AGENTS guidance, README claims, and implementation patterns line up closely.

Practical takeaway: for this codebase, reading docs is genuinely high leverage, especially:
- `AGENTS.md`
- `README.md`
- website developer-guide docs
- tests around the subsystem you want to change

## 13) The codebase is broad, but not conceptually fragmented
After reading the full repo, the best mental model is:
- one agent runtime
- one tool spine
- one persistent state layer
- two main user-facing entry modes (CLI and gateway)
- several extension systems layered around them (skills, plugins, MCP, cron, terminal backends, memory providers)

This is much easier to reason about than treating every directory as a separate mini-application.

## 14) Best fast relearn path after the full read
If I needed to get productive again quickly, I would re-open files in roughly this order:

1. `README.md`
2. `AGENTS.md`
3. `run_agent.py`
4. `model_tools.py`
5. `tools/registry.py`
6. `hermes_state.py`
7. `cli.py`
8. `hermes_cli/main.py`
9. `hermes_cli/config.py`
10. `gateway/run.py`
11. `gateway/session.py`
12. the relevant tool file or platform adapter for the feature being changed

## 15) Highest-risk areas for future changes
Based on the repo structure and tests, the most delicate areas appear to be:
- provider/runtime compatibility layers
- prompt caching and context compression
- profile-safe path handling
- gateway session continuity
- background process recovery
- async tool lifecycle management
- tool schema/dispatch changes that could break existing prompts or skills

Practical takeaway: these areas deserve verification with targeted tests before and after changes.
