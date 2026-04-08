# Raw Source: Hermes tools and memory deep dive

Date captured: 2026-04-08
Source files:
- model_tools.py
- tools/registry.py
- tools/terminal_tool.py
- tools/process_registry.py
- tools/delegate_tool.py
- tools/code_execution_tool.py
- agent/memory_manager.py
- agent/memory_provider.py
- agent/builtin_memory_provider.py
- tools/memory_tool.py
- plugins/memory/*

Key extracted findings:
- The real center of the tool system is `tools/registry.py`; `model_tools.py` is now a thin orchestration layer.
- Tool schemas are dynamically shaped in important cases such as `execute_code`.
- Some tools are intentionally intercepted at the agent layer instead of executed through normal registry dispatch.
- The terminal tool is a sessioned environment manager across multiple backends, not just subprocess execution.
- Background process handling is a dedicated subsystem via `process_registry`.
- Delegation uses isolated child agents with explicit limits and blocked tools.
- `execute_code` is controlled programmatic tool calling, not unrestricted code execution.
- Built-in memory is bounded, file-backed, injection-scanned, and frozen into the system prompt as a session-start snapshot.
- External memory providers are plugin-based, additive, and intended to be one-at-a-time.
