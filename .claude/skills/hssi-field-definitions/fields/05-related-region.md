# Field 5 — Related Region

**Level:** RECOMMENDED · **API:** `relatedRegion[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/Region/rows/all/`
**Filter tab:** Region · **Free-text search tier:** T3 · **Field-search code:** `region`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 180-224; other sections are authored in Phase 2. -->

## What it is

**Type:** Multi-select dropdown

**What it is:** The physical region the software supports science functionality for.

**How to fill it:** Select all physical regions the software's functionality is commonly used or intended for.

The vocabulary is currently flat — every row is a top-level value, no `Parent:Child` form.

<!-- vocab:Region begin -->
**Possible Values** — *24 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/Region/rows/all/` is authoritative.*

- Chromosphere
- Corona
- Earth Atmosphere
- Earth Auroral Subregion
- Earth Inner Magnetosphere
- Earth Ionosphere
- Earth Lower and Middle Atmosphere
- Earth Magnetosheath
- Earth Magnetosphere
- Earth Magnetotail
- Earth Outer Magnetosphere
- Earth Thermosphere
- Heliosheath
- Interplanetary Space
- Jupiter Magnetosphere
- Mars Magnetosphere
- Neptune Magnetosphere
- Photosphere
- Planetary Magnetospheres
- Saturn Magnetosphere
- Solar Environment
- Solar Interior
- Solar Wind
- Uranus Magnetosphere
<!-- vocab:Region end -->

> **Historical note.** Until the 2026-07-29 audit this field listed only 5 values (Earth Atmosphere,
> Earth Magnetosphere, Interplanetary Space, Planetary Magnetospheres, Solar Environment). Those are
> the keys of `REGION_MAPPING_TTL` in `models/vocab.py` — a mapping used for TTL export, **not** the
> selectable vocabulary. All 24 rows above are offered by `/api/models/Region/choices/`. Prefer the
> most specific applicable region (e.g. `Earth Ionosphere` over `Earth Atmosphere`) rather than
> defaulting to the old five.

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- moved from .claude/agents/hssi-metadata-extractor.md:242-246 -->
**Related Region (RECOMMENDED on the form; treat as critical):**
- Also critically important
- Requires understanding the physical regions the software is commonly used for
- **Fetch the options from `/api/models/Region/rows/all/`** — there are 24, and they are finer-grained than the five broad regions this file used to list (`Earth Ionosphere`, `Earth Thermosphere`, `Earth Magnetotail`, `Corona`, `Photosphere`, per-planet magnetospheres, …). Prefer the most specific applicable region over a broad one.
- Select ALL that apply

<!-- moved from .claude/agents/hssi-metadata-extractor.md:369-373 -->
Strongly prioritize **RECOMMENDED** fields, as they greatly improve submission quality — above all
Software Functionality and Related Region, which this workflow treats as critically important even
though the live form marks them RECOMMENDED. For those two, an empty value is legitimate only when
the evidence genuinely supports no value (e.g. domain-independent tooling with no Region), never as
an unexamined gap.

<!-- moved from .claude/agents/hssi-metadata-validator.md:61-61 -->
- [ ] Fields 4 (Software Functionality) and 5 (Related Region) are RECOMMENDED on the live form, not MANDATORY. This workflow still treats them as critically important: an empty value is acceptable only when the dossier carries durable evidence that no value applies (domain-independent tooling can legitimately have no Region — e.g. the settled sammi/cdflib decisions); an unexamined blank is still an ERROR.

<!-- moved from .claude/agents/hssi-metadata-validator.md:76-76 -->
- **Related Region** values must be rows of the live `/api/models/Region/rows/all/` vocabulary (Field 5). There are **24**, not the five broad regions older instructions listed — `Earth Ionosphere`, `Earth Thermosphere`, `Earth Magnetotail`, `Corona`, `Photosphere`, the per-planet magnetospheres and so on are all valid. **Never flag a specific region as invalid just because it isn't one of the old five.**

<!-- moved from .claude/agents/hssi-metadata-validator.md:100-103 -->
**Field 5 (Related Region):**
- Verify against the scientific description, README, and papers
- Check: Does the software actually operate in all listed regions?
- Check: Are there regions it supports that aren't listed?

<!-- moved from .claude/agents/hssi-metadata-validator.md:386-386 -->
4. **Be thorough on Software Functionality and Related Region.** These are the two most important fields. Spend extra time verifying them. Read the code, not just the README.

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- moved from RSFF "Notes for AI Agents" -->
16. **Related Region** is also important and requires a deep understanding of the physical regions the software is commonly used for.

## Payload and roundtrip notes

<!-- phase2 -->

## Worked examples

<!-- phase2 -->

## Provenance

- Vocabulary block `vocab:Region` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 180-224 on 2026-09-22.
