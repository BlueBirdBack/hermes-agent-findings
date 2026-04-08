# Raw Source: Hermes CLI, gateway, config, and profiles deep dive

Date captured: 2026-04-08
Source files:
- cli.py
- hermes_cli/main.py
- hermes_cli/config.py
- hermes_cli/auth.py
- hermes_cli/model_switch.py
- hermes_cli/commands.py
- gateway/run.py
- gateway/session.py
- gateway/config.py
- hermes_constants.py
- hermes_cli/profiles.py

Key extracted findings:
- `hermes_cli/config.py` is the canonical config system, but CLI and gateway still bridge many values into environment variables for runtime compatibility.
- `HERMES_HOME` is the core invariant; profiles are alternate `HERMES_HOME` roots selected very early at startup.
- Slash commands are centralized in one command registry consumed by CLI, gateway, Telegram menus, Slack routing, and autocomplete.
- Gateway session identity is deterministic and policy-driven, with DM/group/thread distinctions and configurable reset behavior.
- Gateway runtime includes explicit concurrency guards to avoid duplicate agents per session.
- Auth is provider-aware and stored in `auth.json` under file locking.
- Model switching is a full resolution pipeline, not just string replacement.
