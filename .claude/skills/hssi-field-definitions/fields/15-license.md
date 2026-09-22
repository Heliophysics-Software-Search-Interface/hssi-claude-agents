# Field 15 — License

**Level:** RECOMMENDED · **API:** `license` · **Change class:** dynamic
**Vocabulary:** `/api/models/License/rows/all/`
**Filter tab:** none · **Free-text search tier:** T4.7 · **Field-search code:** `license`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 347-395; other sections are authored in Phase 2. -->

## What it is

**Type:** Nested group

**What it is:** The full name of the license assigned to this software. Licenses supported by SPDX are preferred. If the software is restricted, enter 'Restricted'.

**How to fill it:** Choose from a list of licenses with proper grammar and punctuation. If the license is listed on https://spdx.org/licenses/, copy the entire license title.

**Sub-fields:**
- **License** (RECOMMENDED): License name
- **License URI** (RECOMMENDED): URI of the license (auto-populated for SPDX licenses)

This is a **closed** list despite the "copy the SPDX title" instruction above: the serializer does
`License.objects.filter(name__iexact=<value>)` and raises `Unknown license` on no match. An SPDX
title that is not a row below will be rejected — use `Other` instead.

<!-- vocab:License begin -->
**Possible Values** — *11 canonical values, snapshot 2026-08-06. Live `/api/models/License/rows/all/` is authoritative. **Row counts differ by target**: `http://localhost` has these 11; `https://hssi.hsdcloud.org` additionally carries 3 legacy duplicate rows (see below) — use the canonical name on either target.*

- Apache License 2.0
- BSD 2-Clause "Simplified" License
- BSD 3-Clause "New" or "Revised" License
- Creative Commons Attribution 4.0 International
- GNU General Public Licenses (GPL version 2)
- GNU General Public License v3.0 or later
- GNU Lesser General Public License v3.0 only
- GNU Library or ‘Lesser’ General Public Licenses (LGPL version 2)
- MIT License
- Other
- Restricted
<!-- vocab:License end -->

**Traps in this list:**

- **Curly quotes.** The LGPL version 2 row uses typographic quotes — `‘Lesser’` (U+2018/U+2019),
  *not* `'Lesser'`. A straight-quote copy will not match.
- **Three legacy duplicate rows exist on production and must not be used.** They are *not* extra
  licences; each is a second name for a row already listed above, and localhost has already retired
  them. Always emit the canonical name on the left:

  | Canonical (use this) | Legacy duplicate on prod (never emit) | Why it is a duplicate |
  |---|---|---|
  | `GNU Lesser General Public License v3.0 only` | `GNU Library or ‘Lesser’ General Public Licenses (LGPL version 3)` | identical URL `https://spdx.org/licenses/LGPL-3.0-only.html` |
  | `BSD 3-Clause "New" or "Revised" License` | `New BSD license` | same SPDX identifier `BSD-3-Clause`; unused by any software on either target |
  | `Other` | a second url-empty `Other` row | `License.get_other_licence()` resolves them with `.first()`, so binding is arbitrary |

  Sending a legacy name to localhost returns a 400 — correctly, because the canonical row is the one
  to use. When diffing a production record, a stored legacy value is **drift to correct**, not a
  value to preserve.

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- phase2 -->

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- moved from RSFF "Notes for AI Agents" -->
5. **License** information is typically in:
   - LICENSE or LICENSE.txt file
   - Package metadata files
   - Repository settings

<!-- moved from .claude/agents/hssi-metadata-validator.md:79-79 -->
- **Data Sources**, **File Formats**, **Operating System**, **CPU Architecture**, **Related Phenomena**, **License** values must be rows of their respective live vocabularies (Fields 15, 17–22) — see rule 3 under Important Rules, and the endpoint table in `hssi-field-definitions`. Watch the byte-level traps: `The Virtual Solar Observatory.` carries a trailing period, the LGPL license names use curly `‘Lesser’`, and `Operating System Independent` is spelled out in full (there is no `OS Independent`).

<!-- moved from .claude/agents/hssi-metadata-validator.md:139-142 -->
**Field 15 (License):**
- Read the actual LICENSE/LICENSE.txt file
- Compare license name against what's in the metadata
- Check if SPDX identifier is correct

## Payload and roundtrip notes

<!-- moved from .claude/skills/submission-payload/SKILL.md:241-247 -->
### License is a plain string

The `license` field is a **plain string** containing the license name — not an object. The serializer looks up `License.objects.filter(name__iexact=<value>)` against the controlled list, so the value must match an entry from `/api/models/License/rows/all/` exactly (case-insensitive).

```json
"license": "BSD 3-Clause \"New\" or \"Revised\" License"
```

## Worked examples

<!-- phase2 -->

## Provenance

- Vocabulary block `vocab:License` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 347-395 on 2026-09-22.
