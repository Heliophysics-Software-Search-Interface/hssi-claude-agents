# Field 11 — Publisher

**Level:** RECOMMENDED · **API:** `publisher` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.1 (name, abbreviation) · **Field-search code:** `publisher`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 277-289; other sections are authored in Phase 2. -->

## What it is

**Type:** Nested group

**What it is:** The publisher (entity) of the creative work.

**How to fill it:** For software where a DOI has been obtained through Zenodo (e.g., GitHub-Zenodo workflow), Zenodo is the correct entry. If no DOI has been obtained, indicate the repository host, such as GitHub or GitLab.

**Sub-fields:**
- **Organization** (RECOMMENDED): Publisher name
- **Publisher Identifier** (RECOMMENDED): ROR identifier when available (e.g., https://ror.org/03c3r2d17) or URL otherwise (e.g., https://zenodo.org)

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- phase2 -->

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- moved from .claude/agents/hssi-metadata-validator.md:74-74 -->
- **ROR identifiers** must be full URLs: `https://ror.org/XXXXXXXXX` (Fields 6, 11, 25)

## Payload and roundtrip notes

<!-- moved from .claude/skills/submission-payload/SKILL.md:249-258 -->
### Publisher has no `publisherIdentifier` key

The publisher object uses `{name, identifier}` only. There is no `publisherIdentifier` key — use `identifier` for the ROR or other organizational ID.

```json
"publisher": {
  "name": "Zenodo",
  "identifier": "https://zenodo.org"
}
```

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 277-289 on 2026-09-22.
