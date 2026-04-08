---
title: Profiles
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [profiles, architecture, cli, gateway, persistence]
sources: [raw/articles/hermes-readme-and-agents-2026-04-08.md]
---

# Profiles

Hermes supports multiple isolated profiles, each with its own `HERMES_HOME` directory and associated state.

## Core invariant

Code that reads or writes Hermes state should use `get_hermes_home()` rather than hardcoded `~/.hermes` paths. User-facing messages should use `display_hermes_home()`.

## Why it matters

Profile isolation affects:
- config
- API keys
- memory
- sessions
- skills
- gateway state
- other persistent tool state

## Design significance

The AGENTS guide treats profile-safety as a repo-wide invariant and explicitly calls out hardcoded `~/.hermes` paths as a historical bug source.

## Related pages
- [[cli-and-gateway]]
- [[persistence-and-sessions]]
- [[memory-system]]
- [[hermes-agent]]
