# Raw Source: Hermes plugins, docs, and product/documentation surface

Date captured: 2026-04-08
Source files:
- plugins/memory/*
- docs/acp-setup.md
- docs/honcho-integration-spec.md
- docs/migration/openclaw.md
- website/README.md
- website/docs/* structure and selected feature/developer pages
- packaging/homebrew/README.md
- CONTRIBUTING.md
- README.md

Key extracted findings:
- Hermes is documented as a broad agent platform, not just a terminal coding assistant.
- There are two extension models: general plugins and specialized memory-provider plugins.
- Memory providers are first-party curated plugins layered on top of built-in memory.
- Honcho is the most strategically elaborated memory-provider integration in the repo.
- ACP/editor support and OpenClaw migration are first-class product surfaces.
- The website docs are mature and split into getting-started, user-guide, developer-guide, guides, integrations, and reference.
- Distribution and packaging are treated as part of the product surface, including Homebrew-specific runtime packaging choices.
