---
title: CLI and Gateway
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [cli, gateway, platform, sessions, auth, models, architecture]
sources: [raw/articles/hermes-code-reading-notes-2026-04-08.md]
---

# CLI and Gateway

Hermes has two main user-facing entry modes: the interactive CLI and the messaging gateway.

## CLI side

The CLI has two layers:
- `hermes_cli/main.py` as the shell entrypoint and command tree
- `cli.py` as the live interactive chat experience

## Gateway side

The gateway is handled primarily by `gateway/run.py` and `gateway/session.py`. It is responsible for platform adapter lifecycle, session routing, and background-process notifications.

## Why this split matters

These are not separate products. Both ultimately drive the same runtime and the same durable session model.

## Related pages
- [[hermes-agent]]
- [[agent-runtime]]
- [[persistence-and-sessions]]
- [[profiles]]
- [[tool-system]]
