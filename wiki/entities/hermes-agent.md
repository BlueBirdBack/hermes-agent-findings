---
title: Hermes Agent
created: 2026-04-08
updated: 2026-04-08
type: entity
tags: [architecture, codebase, runtime, cli, gateway, tools, persistence, research]
sources: [raw/articles/hermes-code-reading-notes-2026-04-08.md]
---

# Hermes Agent

Hermes Agent is a multi-interface AI agent system centered on a synchronous conversation and tool-calling loop. It can run through a terminal UI or through messaging platforms such as Telegram, Discord, Slack, and others.

## Overview

The best top-level mental model is:
- one main runtime loop in [[agent-runtime]]
- one extensibility spine in [[tool-system]]
- one durable transcript and search layer in [[persistence-and-sessions]]
- two main user-facing entry modes in [[cli-and-gateway]]
- a layered memory model described in [[memory-system]]

## Key properties

- The architectural center is `AIAgent` in `run_agent.py`
- Tool execution is first-class, not bolted on later
- Prompt stability and prompt caching shape implementation choices
- The system is optimized for continuity across long-lived sessions
- The codebase is broad, but conceptually unified

## Related pages
- [[agent-runtime]]
- [[tool-system]]
- [[memory-system]]
- [[prompt-caching]]
- [[profiles]]
- [[cli-and-gateway]]
- [[persistence-and-sessions]]
