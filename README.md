# hssi-claude-agents
Claude Code agents for extracting HSSI metadata from any repo and submitting it to the HSSI API.

## Agents

- **Extractor** (CLAUDE.md) — Extracts metadata from software repositories into `hssi_metadata.md`
- **Validator** (.claude/agents/hssi-metadata-validator.md) — Independently validates extracted metadata
- **Submitter** (.claude/agents/hssi-metadata-submitter.md) — Converts metadata to API JSON and submits to HSSI
- **Updater** (.claude/agents/hssi-metadata-updater.md) — Updates existing HSSI entries with fresh metadata from repos

## Steps to Use:
1. Get [Claude Code](https://www.claude.com/product/claude-code)
2. Clone this repo
3. Run `claude` from the root dir
4. Point it to a software repo (e.g. local folder path, GitHub URL, DOI)
5. Metadata gets extracted into `repos/<repo>/hssi_metadata.md`
6. Optionally: ask Claude to submit the metadata to HSSI (production or localhost)
7. To update existing entries: ask Claude to "update sunpy on HSSI" or "enrich sunpy's metadata"
