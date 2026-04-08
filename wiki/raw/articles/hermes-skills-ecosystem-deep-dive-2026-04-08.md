# Raw Source: Hermes skills ecosystem deep dive

Date captured: 2026-04-08
Source files:
- skills/* category DESCRIPTION.md and representative SKILL.md files
- optional-skills/* category DESCRIPTION.md and representative SKILL.md files
- agent/skill_utils.py
- agent/skill_commands.py
- tools/skills_tool.py
- tools/skills_hub.py
- hermes_cli/skills_hub.py

Key extracted findings:
- Built-in skills are a curated workflow knowledge layer seeded into user installs.
- Optional skills are official but dormant extensions, used for niche, experimental, or setup-heavy capabilities.
- Skills are metadata-driven prompt modules with progressive disclosure and on-demand supporting files.
- The Skills Hub suggests a marketplace-like distribution model with official, optional, and community skill sources.
- Skills are one of Hermes' main product-scaling mechanisms because they expand capability without bloating the core runtime.
