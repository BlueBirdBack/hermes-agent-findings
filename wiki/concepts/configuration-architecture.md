---
title: Configuration Architecture
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [cli, gateway, auth, provider, architecture, profiles]
sources: [raw/articles/hermes-cli-gateway-config-deep-dive-2026-04-08.md]
---

# Configuration Architecture

Hermes has a canonical config system plus compatibility layers that still matter at runtime.

## Canonical configuration files
- `~/.hermes/config.yaml`
- `~/.hermes/.env`
- `~/.hermes/auth.json`

## Core pattern

`hermes_cli/config.py` is the main configuration subsystem, but both `cli.py` and `gateway/run.py` still bridge configuration into environment variables for downstream runtime compatibility.

## Why this matters

The user-facing source of truth is increasingly `config.yaml`, but a contributor still has to understand environment-bridging behavior to predict runtime results.

## Related pages
- [[profiles]]
- [[auth-and-model-resolution]]
- [[cli-and-gateway]]
- [[gateway-session-model]]
