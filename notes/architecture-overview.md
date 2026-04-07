# Hermes Agent Architecture Overview

## What this repository is
Hermes Agent is a multi-interface, tool-using AI agent that can run in a terminal UI or behind a messaging gateway. The repo is built around one core synchronous conversation loop (`AIAgent` in `run_agent.py`) and a large surrounding ecosystem for tools, memory, skills, sessions, auth, models, background processes, and platform adapters.

## Big picture mental model
At a high level, the system looks like this:

1. `hermes_cli/main.py` is the top-level command entrypoint for the `hermes` command.
2. `cli.py` runs the interactive terminal chat UX.
3. `gateway/run.py` runs the messaging gateway for Telegram/Discord/Slack/etc.
4. Both paths eventually create and drive an `AIAgent` from `run_agent.py`.
5. `AIAgent` builds prompts, calls the model API, executes tool calls, stores transcript state, and loops until a final assistant response is produced.

## Main architectural layers

### 1) Agent runtime
Core files:
- `run_agent.py`
- `agent/prompt_builder.py`
- `agent/context_compressor.py`
- `agent/prompt_caching.py`
- `agent/models_dev.py`

Responsibilities:
- Build the system prompt from identity, skills, memory, context files, and platform metadata.
- Prepare conversation history for the target provider/API mode.
- Run the main conversation loop.
- Normalize model responses from multiple providers into a common internal format.
- Execute tool calls and append tool results back into the transcript.
- Compress old context when token usage grows too large.

### 2) Tool system
Core files:
- `model_tools.py`
- `tools/registry.py`
- `tools/*.py`
- `toolsets.py`

Responsibilities:
- Discover tools by importing tool modules.
- Register tool schemas and handlers in the central registry.
- Filter tools by enabled/disabled toolsets.
- Dispatch tool calls from the model into Python handlers.
- Support dynamic MCP tools and plugin-provided tools.

### 3) CLI and configuration
Core files:
- `hermes_cli/main.py`
- `cli.py`
- `hermes_cli/config.py`
- `hermes_cli/commands.py`
- `hermes_cli/model_switch.py`
- `hermes_cli/skin_engine.py`
- `hermes_cli/auth.py`

Responsibilities:
- Parse shell subcommands like `hermes model`, `hermes gateway`, `hermes doctor`, etc.
- Run the interactive terminal interface.
- Load and save `~/.hermes/config.yaml` and `~/.hermes/.env`.
- Provide slash command definitions shared between CLI and messaging gateways.
- Resolve providers, models, aliases, and credentials.
- Apply visual skins/themes to the CLI.

### 4) Gateway and session routing
Core files:
- `gateway/run.py`
- `gateway/session.py`
- `gateway/platforms/*`
- `gateway/config.py`

Responsibilities:
- Connect to Telegram, Discord, Slack, WhatsApp, Signal, and other platforms.
- Build per-chat/per-thread/per-user session identities.
- Route inbound messages to the right running agent session.
- Preserve continuity across platforms.
- Deliver cron and background-process updates back to users.

### 5) Persistence and memory-like systems
Core files:
- `hermes_state.py`
- `tools/*` for memory/todo/session search behavior
- `cron/*`
- `agent/trajectory.py`

Responsibilities:
- Store transcripts and metadata in SQLite (`~/.hermes/state.db`).
- Support FTS5 search over message history.
- Track session lineage, system prompt snapshots, tool calls, token counters, and costs.
- Maintain task lists, memory entries, skills, and scheduled jobs.

## The most important design pattern
The repo uses a strongly centralized orchestration pattern:
- One main runtime loop (`AIAgent`) owns conversation flow.
- One tool registry owns tool definitions and dispatch.
- One config/auth layer owns provider/model resolution.
- One gateway runner owns messaging-platform lifecycle.
- One SQLite store owns durable transcript/search state.

That makes the codebase broad, but conceptually it is not many unrelated apps — it is one agent engine with several interfaces and support systems around it.
