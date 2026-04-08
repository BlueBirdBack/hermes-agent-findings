---
title: What is Hermes Agent?
created: 2026-04-08
updated: 2026-04-08
type: query
tags: [query, architecture, runtime, cli, gateway, tools]
sources: [raw/articles/hermes-code-reading-notes-2026-04-08.md]
---

# What is Hermes Agent?

Hermes Agent is a durable, tool-using AI agent system built around one synchronous runtime loop and exposed through both a CLI and a messaging gateway.

## Short answer

It is best understood as:
- one runtime in [[agent-runtime]]
- one extensibility spine in [[tool-system]]
- one durable history layer in [[persistence-and-sessions]]
- one layered memory model in [[memory-system]]
- two main interfaces in [[cli-and-gateway]]

## Why this answer is worth filing

This summary is a reusable orientation answer that prevents re-deriving the same high-level framing repeatedly.

## Related pages
- [[hermes-agent]]
- [[agent-runtime]]
- [[tool-system]]
- [[memory-system]]
