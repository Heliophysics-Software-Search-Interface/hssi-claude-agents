# hssi-claude-agents

Claude Code agents for managing [HSSI](https://hssi.hsdcloud.org) software metadata — extraction, validation, submission, and updates.

## Agents

- **Orchestrator** (CLAUDE.md) — Routes requests, manages pipelines, handles approval gates
- **Extractor** (.claude/agents/hssi-metadata-extractor.md) — Extracts metadata from repos into hssi_metadata.md
- **Validator** (.claude/agents/hssi-metadata-validator.md) — Independently validates extracted metadata
- **Submitter** (.claude/agents/hssi-metadata-submitter.md) — Builds API payloads and submits to HSSI
- **Updater** (.claude/agents/hssi-metadata-updater.md) — Updates existing HSSI entries with fresh metadata

## Steps to Use

1. Get [Claude Code](https://www.claude.com/product/claude-code)
2. Clone this repo
3. Run `claude` from the root dir
4. Point it to a software repo (e.g. local folder path, GitHub URL, DOI)
5. Metadata gets extracted into `repos/<repo>/hssi_metadata.md`
6. Optionally: ask Claude to submit the metadata to HSSI
7. To update existing entries: ask Claude to "update sunpy on HSSI"

## Codex
See the [Codex version of this repo](https://github.com/Heliophysics-Software-Search-Interface/hssi-codex-agents).
