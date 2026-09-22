# Field 15 — License

**Level:** RECOMMENDED · **API:** `license` · **Change class:** dynamic
**Vocabulary:** `/api/models/License/rows/all/`
**Filter tab:** none · **Free-text search tier:** T4.7 · **Field-search code:** `license`

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

**The License URI sub-field is not a per-software value.** `Software.license` is a foreign key to a
shared `License` row, and the URL lives on that row (`License.url`). There is no per-software licence
URI anywhere in storage: choosing a row publishes that row's URL, and a URI that differs from it is
unwritable.

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
- **The GPL v3 row has no "GPL" in its name** (`GNU General Public License v3.0 or later`). Print all
  rows before asserting that a licence has none; a substring filter on an abbreviation misses it.
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

A user deciding whether they may use, modify or redistribute a tool — or build it into their own
software — needs the licence before they invest time in it. The value tells them the terms at a glance
and links to the licence text. A wrong row is worse than none: because the row carries a shared URL, a
near-match (LGPL-2.0 for LGPL-2.1, GPL for AGPL, BSD for CeCILL-B) publishes the wrong legal terms and
points the user at the wrong text. A blank on well-licensed software hides a fact the user needed.

## How it appears on the site

- **Detail page:** "Licensing & Funding" section, "License" row. The row name is shown, linked to the
  row's `url` when it has one; `Other` and `Restricted` have no URL and render as plain text.
- **Filter tab:** none.
- **Free-text search:** tier T4.7 (`license` name).
- **Field search:** `license:"…"` matches `license__name__icontains`.
- **JSON-LD:** `license` is emitted as an object with `@id`/`url` set to the row URL and `name`, only
  when the row has a URL; the catalogue-record wrapper also carries the row URL. `Other` and
  `Restricted` therefore emit no licence.

## Rubric: include / exclude

Rule 1 fixes which licence is being mapped. Then apply rules 2–9 top to bottom and stop at the first
rule that fires.

1. **The software's CURRENT licence governs.** Determine it from the repository at the pinned revision:
   the LICENSE file's content, per-file headers, and `license` / `License ::` metadata. Not the first
   commit's licence, not the released version's, not the DOI deposit's. A licence the project has since
   replaced is history for the dossier, never a candidate value.
2. **The software itself states it is restricted** (access by agreement or request, use or
   redistribution limited by its owner) → `Restricted`. Fires on: a source stating the restriction.
   Unavailable source code with no stated terms is **not** `Restricted` (rule 7).
3. **The current licence has a row** → that row, spelled exactly (curly `‘Lesser’`, straight `"` in the
   BSD names). Decide BSD 2- versus 3-Clause by the clauses in the file (the no-endorsement clause makes
   it 3-Clause), not by the DOI deposit's label.
4. **Same licence text and version, differing only in the "only" / "or later" election the vocabulary
   cannot express** → the row for that text and version. GPL-3.0-only maps to `GNU General Public
   License v3.0 or later` (there is no GPL-3.0-only row); LGPL-3.0-or-later maps to `GNU Lesser General
   Public License v3.0 only`; GPL-2.0-or-later maps to `GNU General Public Licenses (GPL version 2)`.
   `Other` is not chosen here: it would discard an accurate licence family and version to express an
   election nobody searches for.
5. **Rule out the near-match row by name.** A different licence family or version never maps to the
   nearest-looking row: GPL-2.0 is not `GNU General Public License v3.0 or later`; LGPL-2.1 is not the
   LGPL version 2 row (its URL is SPDX `LGPL-2.0`); AGPL-3.0 is not the GPL v3 row; CeCILL-B is not a
   BSD row; the legacy `… (LGPL version 3)` duplicate is never used in place of `GNU Lesser General
   Public License v3.0 only`. Record each tempting near-match and why it fails.
6. **A real licence with no row** (an SPDX title such as LGPL-2.1, NASA-1.3, CeCILL-B, or a project's
   own licence agreement) → `Other`, with the actual licence and its SPDX identifier (if any) written in
   the dossier note. If a matching row is later added to the vocabulary, change to it.
7. **No licence anywhere** — no LICENSE file, no header, no package metadata, no statement from the
   publisher or host → leave the field **empty** and record the search. Do not select `Other` (it
   asserts a determined, unlisted licence) or `Restricted` (it asserts terms nobody set). Zenodo's
   `other-open` and "Open Access" rights strings are placeholders, not licences.
8. **Incumbent values.** Keep a stored value that rules 1–6 reproduce. Replace one that differs: a
   relicensing since the last refresh, a legacy duplicate row (drift to correct), or a DOI-autofilled
   value the repository contradicts (the autofill copies Zenodo's hand-set licence dropdown verbatim).
   Clear a stored value only when rule 7 fires. Never "correct" a value backwards to an earlier licence.
   This field is dynamic: re-derive it on every refresh.
9. **Never record a License URI** as a value, and never propose writing one; cite the LICENSE file's
   URL in the note as evidence only.

## Ask the user only when

- **The software's own licence offers a choice of licences for the software as a whole** (dual
  licensing), since the field holds one row. A different licence on a vendored component, on data, or
  on a wiki is not this shape — rule 1 decides it.

Every other case is decided by the rubric.

## Where to find it, and traps

**Sources, in priority order:**
1. The LICENSE / LICENSE.txt / COPYING file at the pin, read by content (its first lines and the
   clauses that distinguish near-matches), including files outside the repository root when the
   packaging root is a subdirectory.
2. Per-file licence headers in the source.
3. Package metadata: `license` / `license-expression` / `License ::` classifiers in `pyproject.toml`,
   `setup.cfg` or `setup.py`; PyPI's JSON API.
4. Repository settings: GitHub's detected `license.spdx_id`.
5. For software without a repository: the publisher's or host's own terms page.
6. The DOI deposit (DataCite `rightsList`, Zenodo `metadata.license.id`) — corroboration only.

**Validator checks:** read the actual LICENSE/LICENSE.txt file; compare the licence name against the
metadata; check that the SPDX identifier is correct; confirm the value is a row of the live
`/api/models/License/rows/all/` (Field 15), byte-exact including the curly `‘Lesser’`.

**Licence history.** Answer a history question by reading the file's content at each commit
(`git log --format=%H -- LICENSE*` then `git show <sha>:<path> | head -3`). A rename is not a change:
`git log --diff-filter=A` reports the rename as the file's creation and hides the real relicensings.
Check the released tag too, because the released version can carry a different licence than the pin —
that difference is durable rationale (it explains why Zenodo or PyPI disagree), not a competing value.

**Traps:**
- **GitHub's detected licence only looks at the repository root.** `license: null` can mean the LICENSE
  sits under the packaging subdirectory, not that there is none; `NOASSERTION` means a licence is present
  that GitHub cannot map.
- **An absent classifier or an empty PyPI `license` field** is a packaging gap, not a licensing fact.
- **The DOI deposit's licence can be a valid, wrong row.** A Zenodo deposit declaring CC-BY-4.0 for
  MIT-licensed code, or `bsd-2-clause` for a 3-clause file, maps to a live row and is accepted without
  complaint — re-derive from the repository.
- **Zenodo `other-open`** is either the default placeholder or an accurate record of an older licence
  era; either way it is not this field's value.
- **"any later version" inside the GPL text itself** (its section 14 and its appendix) is standard
  licence wording, not the project's "or later" election.
- **Licences of other things on the same page.** A Google Code `contentLicense` governs wiki content; a
  host page's "public domain" sentence may be about a different program it distributes. Scope the
  licence to the software this entry describes.

## Payload and roundtrip notes

### License is a plain string

The `license` field is a **plain string** containing the license name — not an object. The serializer looks up `License.objects.filter(name__iexact=<value>)` against the controlled list, so the value must match an entry from `/api/models/License/rows/all/` exactly (case-insensitive).

```json
"license": "BSD 3-Clause \"New\" or \"Revised\" License"
```

- The value is stripped before the lookup, and the lookup takes `.first()`; no match raises
  `{"license": "Unknown license '<value>'."}` (400). Only case is forgiven — a straight-quote `'Lesser'`
  fails.
- `"license": null` or `""` clears the foreign key; an omitted key leaves it unchanged.
- On roundtrip the stored form may be represented as an object `{name, url, …}` looked up from the
  `License` row; compare by name.
- Two production `Other` rows bind arbitrarily through `.first()`; the canonical one is the url-empty row
  `License.get_other_licence()` returns.

## Worked examples

- **An unlisted licence with a tempting row (pyflct).** The package is LGPL-2.1-or-later on five
  sources, after relicensing from GPL-3.0-or-later a month after its first commit. Rule 1 takes the
  current LGPL; rule 5 rules out the LGPL version 2 row because its URL is SPDX `LGPL-2.0`; rule 6 gives
  `Other`, with the licence named in the note. The initial commit's GPL v3 is a live row and must not be
  "restored".
- **A distinct licence family (TomograPy).** The repository ships CeCILL-B in English and French,
  unchanged since it was added. CeCILL-B is often called "BSD-like", but it is a different licence text
  under French law, and the CeCILL family has no row; rule 5 rejects both BSD rows and rule 6 records
  `Other`.
- **Current licence over released licence (ReesAurora).** The file went GPL-3.0 → AGPL-3.0 → (a rename,
  content unchanged) → Apache-2.0, and the only release shipped under AGPL. Rule 1 gives `Apache License
  2.0`; the AGPL era explains Zenodo's `other-open` and is recorded, with `GNU General Public License
  v3.0 or later` ruled out by name because AGPL is not GPL.
- **An election the vocabulary cannot express (python-magnetosphere).** The LICENSE is the GPLv3 text
  and the README says "v.3" with no "or later" grant. Rule 4 keeps `GNU General Public License v3.0 or
  later`: same text and version, and `Other` would discard the accurate GPLv3 information.
- **A valid wrong row from the DOI (SAVIC).** The LICENSE is MIT but sits under `source/`, so GitHub
  reports no licence, and the Zenodo deposit declares CC-BY-4.0 — itself a live row. Rules 1 and 3 give
  `MIT License` from the file; the deposit's value is the trap recorded in the note.

## Provenance

- Vocabulary block `vocab:License` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 347-395 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
