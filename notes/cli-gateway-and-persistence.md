# CLI, Gateway, and Persistence Notes

## CLI split: shell CLI vs interactive CLI
There are two important CLI layers.

### `hermes_cli/main.py`
This is the top-level command entrypoint for `hermes` subcommands.

It is responsible for:
- applying profile overrides early,
- loading env/config state,
- constructing the argparse tree,
- dispatching commands like `chat`, `model`, `gateway`, `setup`, `tools`, `memory`, `cron`, `sessions`, `doctor`, and more.

### `cli.py`
This is the interactive chat/TUI layer.

It is responsible for:
- running the live terminal chat experience,
- slash command handling,
- switching models/providers during a session,
- coordinating display/spinner behavior,
- launching the agent with the current runtime config.

## Command registry pattern
`hermes_cli/commands.py` is a central registry for slash commands.

This is a nice architectural choice because one command definition fan-outs into:
- CLI help,
- autocomplete,
- gateway help,
- Telegram bot command menus,
- Slack subcommand routing,
- alias resolution.

That makes command additions relatively centralized and low-duplication.

## Config system
The canonical persistent config appears to be:
- `~/.hermes/config.yaml`
- `~/.hermes/.env`

### `hermes_cli/config.py`
Important roles:
- create/prepare Hermes home,
- define `DEFAULT_CONFIG`,
- deep-merge user config with defaults,
- expand `${ENV_VAR}` references,
- migrate old config shapes,
- atomically save config and env values.

### `cli.py` runtime config adaptation
`cli.py` has its own config-loading path for the interactive runtime. It adapts the canonical config into a shape that the live CLI session and terminal backends can use immediately.

My takeaway: `hermes_cli/config.py` is the persistent source of truth, while `cli.py` adds runtime-friendly shaping.

## Auth and provider resolution
`hermes_cli/auth.py` is a major hub.

It handles:
- provider definitions,
- auth state storage (`~/.hermes/auth.json`),
- runtime credential resolution,
- access-token refresh flows,
- active-provider selection,
- API-key and OAuth-like provider support.

The repo is clearly designed to support many providers and to auto-resolve the best available authenticated provider when possible.

## Model switching
Model switching is shared logic rather than duplicated per interface.

`hermes_cli/model_switch.py` appears to handle:
- explicit provider selection,
- alias resolution,
- provider detection,
- runtime credential lookup,
- model validation/normalization,
- API mode detection,
- metadata lookup before applying the switch.

This is one of the cleaner cross-cutting architecture choices in the repo because both the shell CLI and interactive `/model` flows can use it.

## Skin system
`hermes_cli/skin_engine.py` is a data-driven theming system.

It supports:
- built-in skins,
- user YAML skins under `~/.hermes/skins/`,
- runtime switching,
- inheritance from default values.

This part of the codebase is mostly presentation logic, but it is implemented in a reusable way rather than being hardcoded inside the UI.

## Persistence: SQLite + gateway session map
There are two distinct persistence layers.

### 1) Durable transcript database: `hermes_state.py`
This stores the durable session history in SQLite.

Key observations:
- database path is `~/.hermes/state.db`,
- WAL is enabled,
- there is FTS5-based search,
- sessions store metadata like model, title, costs, token counts, parent session lineage, and system prompt snapshots,
- messages retain assistant reasoning/tool metadata as needed.

This is the real long-term transcript/search layer.

### 2) Gateway session routing: `gateway/session.py`
This file manages session identity for messaging platforms.

It handles:
- stable session keys for DM/group/thread contexts,
- reset policies (idle/daily/both/none),
- session-to-chat mapping,
- transcript loading/appending/rewriting,
- keeping gateway-facing state in sync with the durable transcript store.

My mental model: `SessionStore` is the routing/state layer for active chats, not the sole system of record for all conversation history.

## Gateway runner
`gateway/run.py` is the orchestration layer for messaging platforms.

It is responsible for:
- loading gateway config,
- building the `SessionStore`,
- constructing adapters per enabled platform,
- caching/running agents per session,
- handling recovery and cleanup,
- bridging background-process events back into conversations.

The gateway is not a thin wrapper; it has real orchestration responsibility.

## Background process model
Background execution is more sophisticated than a raw subprocess wrapper.

Observed design:
- `terminal(background=true)` launches managed background sessions.
- `tools/process_registry.py` tracks running/finished processes, logs, stdin, recovery metadata, and watcher settings.
- Watchers can push progress updates and completion notifications back into the gateway chat flow.
- Active background processes can prevent session auto-reset.
- Process metadata is checkpointed so recovery can happen after restarts.

That is a strong sign the repo is designed for long-running agent workflows rather than only short one-turn jobs.

## Architecture takeaway
The repo’s persistence and gateway design are built around continuity:
- continuity of session identity,
- continuity of tool/process state,
- continuity of provider/model state,
- continuity of searchable history,
- continuity across multiple user-facing interfaces.

That continuity focus seems to be one of the core design philosophies of the project.
