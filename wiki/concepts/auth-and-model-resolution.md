---
title: Auth and Model Resolution
created: 2026-04-08
updated: 2026-04-08
type: concept
tags: [auth, provider, models, cli, gateway, architecture]
sources: [raw/articles/hermes-cli-gateway-config-deep-dive-2026-04-08.md]
---

# Auth and Model Resolution

Hermes separates authentication state, provider selection, runtime credential resolution, model normalization, and API-mode selection.

## Main pieces
- `hermes_cli/auth.py` manages provider auth state and locking around `auth.json`
- `hermes_cli/model_switch.py` centralizes model/provider switching logic
- runtime code resolves credentials and model metadata before applying a switch

## Key point

Switching models is a pipeline, not a string substitution. It may involve provider detection, alias resolution, credential lookup, normalization, metadata lookup, and API-mode derivation.

## Related pages
- [[configuration-architecture]]
- [[cli-and-gateway]]
- [[profiles]]
- [[hermes-agent]]
