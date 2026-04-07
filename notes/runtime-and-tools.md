# Runtime and Tooling Notes

## Main runtime loop (`run_agent.py`)
The heart of the repo is `AIAgent`.

### What `AIAgent` does
On initialization it:
- Resolves provider and API mode.
- Initializes the model client.
- Loads tool definitions from `model_tools.get_tool_definitions(...)`.
- Sets up memory/session/todo/delegation helpers.
- Configures prompt caching and context compression.

### Main loop shape
The conversation loop in `run_conversation(...)` is roughly:
1. Build/restore system prompt.
2. Add user message to conversation history.
3. Prepare provider-facing request payload.
4. Call the model.
5. Normalize the response into a stable internal assistant message.
6. If the response includes tool calls:
   - append the assistant tool-call message,
   - execute the tools,
   - append tool result messages,
   - loop again.
7. If no tool calls exist, finalize and return the assistant text.

This means Hermes is fundamentally a synchronous tool-calling loop with persistent transcript state.

## Internal message strategy
The internal transcript is mostly stored in OpenAI-style message dicts:
- `system`
- `user`
- `assistant`
- `tool`

Assistant turns may also carry extra internal metadata such as:
- reasoning text/details
- finish reasons
- tool call payloads
- Codex reasoning artifacts for replay

The repo tries hard to keep one normalized internal conversation format, then translate that format for each provider/API.

## Prompt assembly
Prompt assembly is layered, not monolithic.

Important inputs include:
- agent identity / `SOUL.md`
- tool-aware instructions
- memory and user-profile blocks
- skill system prompt
- project context files like `AGENTS.md`
- platform metadata
- current timestamp/session metadata

A key implementation detail: Hermes keeps the stable system prompt cached and injects ephemeral context later at call time. That appears intended to improve prompt-caching effectiveness, especially for Anthropic-compatible cache control.

## Context compression
`agent/context_compressor.py` handles long conversations.

Observed behavior:
- Old large tool outputs can be pruned first.
- The start of the conversation is partially preserved.
- The recent tail is protected by token budget.
- The middle gets summarized with an auxiliary LLM.
- Repeated compressions maintain a rolling summary/handoff.

The summary tries to preserve:
- goal
- constraints/preferences
- progress
- decisions
- relevant files
- next steps
- critical context

Compression is not just summarization; it also repairs tool-call/tool-result integrity so the transcript remains valid for future model turns.

## Tool architecture

### Tool registration
Tools self-register in `tools/registry.py` via `registry.register(...)` when their module is imported.

Each tool entry includes things like:
- tool name
- toolset name
- JSON schema
- Python handler
- availability check
- metadata (env requirements, emoji, async flag)

### Tool discovery
`model_tools._discover_tools()` imports tool modules to trigger registration.

That same discovery path also brings in:
- MCP tools
- plugin-discovered tools

### Tool filtering and schemas
`model_tools.get_tool_definitions(...)`:
- resolves enabled/disabled toolsets,
- requests available definitions from the registry,
- applies some dynamic schema adjustments for special tools.

### Tool dispatch
`handle_function_call(...)` in `model_tools.py` is the main bridge from model output to Python execution.

It does several useful things:
- coerces arg types against the schema,
- runs plugin hooks,
- special-cases some tool behavior,
- dispatches to the registry handler,
- returns JSON-stringified errors when something goes wrong.

Some tools are intentionally intercepted at the agent layer instead of being dispatched normally, especially tools that need direct access to session/agent state.

## Tool execution safeguards
The runtime does more than blindly execute tool calls. It appears to:
- validate or repair malformed JSON args,
- handle hallucinated tool names,
- reject unknown tools cleanly,
- deduplicate some duplicate tool calls,
- parallelize only when a batch appears safe.

That makes the agent loop more resilient to imperfect model outputs.

## Async handling detail
The repo includes a deliberate async-bridging strategy so sync code can safely call async tools and avoid event-loop lifecycle errors. This matters because the top-level agent loop is synchronous, while some tools or backends are async.

## Why this architecture matters
After reading the code, the repo’s operating model feels like:
- maintain one durable, normalized conversation state;
- translate only at the provider boundary;
- treat tools as part of the core loop;
- keep long-horizon sessions viable with compression/search/memory;
- let the same runtime power both CLI and messaging experiences.
