# Field 6 — Authors

**Level:** MANDATORY · **API:** `authors[]` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.1 (given, family, identifier) · **Field-search code:** `author`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 225-240; other sections are authored in Phase 2. -->

## What it is

**Type:** Multi-entry nested group

**What it is:** The author(s) of this software.

**How to fill it:** Multiple authors should be included in separate author fields.

**Sub-fields:**
- **Authors** (MANDATORY): Author name
- **Author Identifier** (RECOMMENDED): The identifier of the author. For a person author, this is the ORCiD (e.g., https://orcid.org/0000-0003-0875-2023). For an author that is an **organization** (a lab, consortium, or institution credited as an author), use its ROR instead (e.g., https://ror.org/03c3r2d17) — HSSI recognizes a ror.org identifier and treats that author as an organization. Enter the complete identifier URL.
- **Affiliation** (RECOMMENDED, multi-entry):
  - **Organization**: Complete name without acronyms (e.g., Center for Astrophysics Harvard & Smithsonian)
  - **Affiliation Identifier**: ROR identifier if one exists (e.g., https://ror.org/03c3r2d17)

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- moved from .claude/agents/hssi-metadata-extractor.md:46-46 -->
- **Pre-populate** every field from the seed first. If both a prior `hssi_metadata.md` and live HSSI metadata are provided, live HSSI is the authoritative baseline for what is currently published. For scalar fields, keep a populated live HSSI value when the sources disagree and retain the prior-file value only as a documented candidate. For multi-valued fields, take the identity-aware union of values that either source has; do not concatenate conflicting scalar values. Match authors by ORCID and then normalized name, and for each matched author union affiliations by ROR and then normalized organization name so choosing one author object never discards affiliations from the other seed. Match other structured entries by stable identifier before normalized name.

<!-- moved from .claude/agents/hssi-metadata-extractor.md:273-273 -->
**Organization names (Author Affiliation, Funder) — expand acronyms.** When you encounter an acronym for an affiliation (Field 6) or funder (Field 25), record the full institutional name instead. Example: `NASA` → `National Aeronautics and Space Administration`. If the source only contains an ambiguous acronym you can't confidently expand, leave it as-is and note it so the validator/user can resolve it.

<!-- moved from .claude/agents/hssi-metadata-extractor.md:275-275 -->
**Organization authors (Field 6) — detect and record a ROR.** An *author* can be an organization (a lab, consortium, or institution credited as an author), not just a person. Recognize these signals: a CITATION.cff author entry with a single `name:` key and no `given-names`/`family-names`; a codemeta.json / JSON-LD author with `"@type": "Organization"`; a DataCite or Zenodo creator whose `nameType` is `"Organizational"`; or a name that is clearly a group (`… Team`, `… Community`, `… Consortium`, `… Collaboration`). For such an author, look up its **ROR** via the ror.org API (`https://api.ror.org/organizations?query=<name>`) and record that ROR as the author's identifier — no separate "organization" marker is needed, since HSSI infers org-ness from the `ror.org` identifier. Keep the person-vs-organization distinction: use an ORCID for people and a ROR for organization authors.

<!-- moved from .claude/agents/hssi-metadata-updater.md:409-413 -->
When extracting fresh values for **Author Affiliation (Field 6)** or **Funder (Field 25)**, record the full institutional name instead of an acronym (example: `NASA` → `National Aeronautics and Space Administration`). When diffing against HSSI, do not flag an existing full name as STALE just because the fresh source uses an acronym — prefer the full-name form. For Funder, also keep one organization per entry rather than combining multiple into a single value.

When an author is itself an **organization** (a lab, consortium, or institution credited as an author), its identifier is a **ROR** (`https://ror.org/…`) rather than an ORCID, and HSSI treats such an author as an organization. During refresh/enrich, match and dedupe these authors by that ROR identifier (exactly as ORCID is used for people), and don't flag a `ror.org` author identifier as invalid.

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- moved from RSFF "Notes for AI Agents" -->
4. **Authors** can be extracted from:
   - CITATION.cff file
   - codemeta.json file
   - AUTHORS file
   - CONTRIBUTORS file
   - Git commit history (with caution)
   - Package metadata (setup.py, package.json, etc.)

<!-- moved from .claude/agents/hssi-metadata-validator.md:72-74 -->
- **Author names** should follow "Given Name, Initials, Surname" convention (Field 6)
- **Author identifiers** must be full URLs (Field 6): an **ORCID** (`https://orcid.org/XXXX-XXXX-XXXX-XXXX`) for a person author, or a **ROR** (`https://ror.org/XXXXXXXXX`) for an author that is an organization. Do **not** flag a `ror.org` author identifier as an error — HSSI treats such an author as an organization.
- **ROR identifiers** must be full URLs: `https://ror.org/XXXXXXXXX` (Fields 6, 11, 25)

<!-- moved from .claude/agents/hssi-metadata-validator.md:105-114 -->
**Field 6 (Authors):**
- Cross-check against ALL of these sources (if they exist):
  - CITATION.cff
  - codemeta.json
  - AUTHORS or CONTRIBUTORS files
  - .zenodo.json
  - Package metadata (setup.py, pyproject.toml, setup.cfg, package.json)
- Flag authors present in sources but missing from metadata
- Verify author identifiers resolve and match the right entity: an **ORCID** should match the right person; a **ROR** identifies an *organization* author (a lab/consortium/institution credited as an author) — check the ROR resolves to that organization, and do not flag it as a malformed person ORCID
- **Affiliation organization names should be the full institutional name, not acronyms.** Flag any affiliation that is a bare acronym (e.g., `ESA` instead of `European Space Agency`) as a WARNING with `Suggested fix: expand to the full institutional name`. Do not flag values that include an acronym alongside the full name (e.g., "European Space Agency (ESA)").

<!-- moved from .claude/agents/hssi-metadata-validator.md:183-185 -->
2. **Search for unlisted authors:**
   - Compare every source of author info against the metadata
   - Look for CONTRIBUTORS files, git shortlog patterns

## Payload and roundtrip notes

<!-- moved from .claude/skills/submission-payload/SKILL.md:108-108 -->
**Organization authors.** An author may be an organization (a lab, consortium, or institution credited as an author) rather than a person. To submit one, put its **ROR URL** in `identifier` (e.g., `https://ror.org/03c3r2d17`). HSSI derives org-ness server-side purely from the `ror.org` identifier — there is no separate flag — and renders the author as a schema.org `Organization`, with its affiliations as `parentOrganization`. `givenName` and `familyName` are still both required and non-empty, and the stored name is `givenName + " " + familyName`, so **split the org name on the first whitespace**: first token → `givenName`, the remainder → `familyName` (e.g., "The SunPy Community" → `givenName: "The"`, `familyName: "SunPy Community"`). A single-token org name (e.g., "NASA") can't satisfy the non-empty `familyName` rule — flag it to the user rather than guessing a split. This applies to **authors only**; contributors remain person/ORCID-only.

<!-- moved from .claude/agents/hssi-metadata-submitter.md:113-113 -->
**D. Organization-name sanity** — For `affiliation[].name` (Field 6) and `funder[].name` (Field 25), if a value is a bare acronym (e.g., `ESA` rather than `European Space Agency`), surface it in the verification report and ask the user before submitting. Do not auto-expand — the value should already be expanded upstream by the extractor. Also flag funder entries that combine multiple organizations into one value (the form expects one organization per entry).

<!-- moved from .claude/agents/hssi-metadata-updater.md:217-218 -->
- **Identity matching does not erase attribute differences.** Match authors by ORCID and then normalized name; for each matched author, union affiliations by ROR and then normalized organization name. Match organizations, awards, instruments, and observatories by their stable identifier before normalized/canonical name, then separately compare their labels and nested values. Do not mark two objects fully MATCH merely because their identifiers match.
- **Respect PATCH capability limits.** The endpoint reuses existing people, organizations, awards, instruments, and observatories and does not overwrite their nonblank names. It can add author affiliations but cannot remove an existing affiliation. Classify a desired shared-entity rename or nested affiliation removal as NON-PATCHABLE, omit it from `patch`, and make it a hard blocker for canonical completion until the user routes it through the CSV/manual database workflow. Top-level relationship removals remain possible through a complete approved replacement list.

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 225-240 on 2026-09-22.
