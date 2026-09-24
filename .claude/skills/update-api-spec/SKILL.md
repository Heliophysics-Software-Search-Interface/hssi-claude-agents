---
name: update-api-spec
description: >
  Sync the submitter's and updater's API reference skills with the hssi-website
  source code, and reconcile the documented controlled-value lists against the
  live HSSI vocabularies. Use when the HSSI API has changed, when allowed-value
  lists may have drifted, or before trusting a value snapshot. Clones or pulls
  the hssi-website repo, reads the relevant source files, and updates
  submission-payload, submission-verification, update-payload, and the
  hssi-field-definitions field files (their fenced vocab blocks and their
  statements about how the website renders, filters and searches each field).
---

# Update API Spec

Sync the reference files with the latest HSSI API source **and** the live controlled vocabularies.

**When to use:**
- The HSSI API has changed (new fields, renamed keys, changed shapes, new quirks) and the `submission-payload`, `submission-verification`, or `update-payload` skills need updating. → Steps 1–5.
- A controlled-value list may have drifted, or you want to re-date a snapshot before trusting it. → **Step A** (independent; needs no repo clone).
- The website may have changed how a field renders, filters or searches, or the form's text and requirement levels — the field files state these as facts. → **Step B** (needs the repo clone; run it whenever `hssi-website` has new commits).

**How often:** The API itself is relatively stable — run Steps 1–5 on failures or announced changes. **Vocabulary drift is different**: rows get added and edited through normal operation, so **run Step A before any batch of submissions or updates that leans on the documented value lists**, and whenever a submission fails with `Unknown value`.

---

## Step A: Reconcile controlled vocabularies against live

> **Verify assumptions before trusting them.** The **Possible Values** lists in the
> `hssi-field-definitions/fields/*.md` files — each fenced between `<!-- vocab:<Model> begin -->` and
> `<!-- vocab:<Model> end -->` — and the taxonomy counts at the top of `fields/04-software-functionality.md`
> are **dated snapshots of an external system**, not invariants. Nothing in this repo detects drift on
> its own. Start this step by re-checking, not by assuming the last audit still holds.

### A1. Fetch every vocabulary from **both** targets

Prod and localhost can and do diverge — at the 2026-08-06 audit the closed vocabularies differed in
`License` and `DataInput`. Always check both; the authority for any given operation is the target
actually in play.

```bash
OUT=$(mktemp -d)
for ENV in "prod https://hssi.hsdcloud.org" "local http://localhost"; do
  set -- $ENV
  mkdir -p "$OUT/$1"
  for M in FunctionCategory Region ProgrammingLanguage FileFormat OperatingSystem \
           CpuArchitecture RepoStatus DataInput Phenomena License Keyword; do
    curl -s -m 60 -o "$OUT/$1/$M.json" "$2/api/models/$M/rows/all/"
  done
  # InstrumentObservatory is ~7,700 rows; fetch the columns needed for the Field 31/32 vocabulary-state check only
  curl -s -m 120 -o "$OUT/$1/InstrumentObservatory.json" "$2/api/models/InstrumentObservatory/rows/all/?columns=id,name,identifier,type"
done
echo "$OUT"
```

Notes: model names resolve case-insensitively (`CpuArchitecture` is the canonical Django class; `CPUArchitecture` also works). There is **no** `/api/models/` index endpoint — it 404s, so the model list above is maintained by hand; cross-check it against `django/website/models/vocab.py` when you have the source checked out.

### A2. Diff each vocabulary against the documented list

For each model, set-compare the live `name` values against the corresponding **Possible Values** list inside the `<!-- vocab:<Model> begin -->` … `<!-- vocab:<Model> end -->` block of the field file that owns it (the `Vocabulary:` header line of each `fields/NN-*.md` names its model; `FileFormat` is owned by `fields/18` and mirrored in `fields/19`), and report three classes separately:

| Class | Meaning | Severity |
|---|---|---|
| **doc-only** | In the document, absent from live | **Breaking** — `serializers/submission.py` matches with `name__iexact` after a bare `.strip()`, so these raise `ValidationError: Unknown value` and fail the whole submission |
| **live-only** | In live, missing from the document | Agents can't pick a valid value they can't see |
| **target-divergent** | Present on one target only | Value works against one instance, 400s against the other |

Compare **case-insensitively after trimming** — that is exactly what the backend does — but report every other difference as breaking. Real examples caught this way: `The Virtual Solar Observatory` missing the stored trailing period, and straight `'Lesser'` where the License rows use curly `‘Lesser’`.

Structural cases:
- **`FunctionCategory`** is hierarchical. Build full names as `Parent: Child` (space after the colon — the canonical form the API returns; compare after normalizing colon spacing) from each row's `parents` before comparing; comparing bare names produces false duplicates. Also re-derive the counts quoted at the top of `fields/04-software-functionality.md` (rows, top-level, distinct names, recurring names).
- **`InstrumentObservatory`** is not listed in any field file (too large); instead re-verify the vocabulary-state sentence in `fields/31-related-instruments.md`: the row count and that every row's `identifier` starts with `https://spase-metadata.org/`. Report any row that fails that guard; re-date the sentence.
- **`Region`** and **`Phenomena`** are graph lists that are currently *flat*. If a future refresh gives them parents, they'd need `Parent:Child` handling too — check before assuming.
- **`Keyword`** is an **open** vocabulary (`_get_or_create_keyword` creates missing rows), so live-only keywords are expected and are not drift. Only refresh the sample count and date in `fields/16`.

### A3. Flag likely data-entry junk — **report, never delete**

Some rows are artifacts of free-text values leaking into controlled lists rather than real vocabulary. **This skill never deletes or edits a live row**; it reports them so a human can decide. Signals:

- an embedded URL in the `name` (`Other - https://xrt.cfa.harvard.edu/level1/`; an Organization named `https://zenodo.org/records/18494048`)
- a `name` prefixed with another valid value plus free text (`Other - …`)
- trailing punctuation where siblings have none (`The Virtual Solar Observatory.`)
- an empty `identifier` where every sibling row has one (`AMDA`, `GFZ`, `Madrigal`, `WDC` in `DataInput`)
- duplicate names within a *flat* list (prod carries two url-empty `License` rows named `Other`; `get_other_licence()` resolves them with `.first()`, so binding is arbitrary)
- a single row holding a comma-delimited list (a `Keyword` row containing seven comma-separated terms)

**Repeated names in `FunctionCategory` are not junk** — 13 subcategory names legitimately recur under different parents and are disambiguated by the parent prefix.

If a junk row is the *only* row for a real concept, say so explicitly: `The Virtual Solar Observatory.` carries the canonical `…#VSO` identifier, so the typo'd name is the value that must be used, not avoided.

### A4. Apply the reconciliation

- Correct each drifted list **inside its `vocab:` fence** in the owning field file. Outside the fences, this step edits only the items named below — the provenance lines, the **Traps** notes and `> **Trap.**` callouts that belong to a list, the Field 4 counts, the Field 16 sample count and date, the Field 31 vocabulary-state sentence and the `## Provenance` dates; every other sentence is hand-written guidance and is left alone.
- Refresh that list's provenance line to the run date and the targets actually checked:
  `*N values, snapshot YYYY-MM-DD, verified identical on https://hssi.hsdcloud.org and http://localhost. Live /api/models/<Model>/rows/all/ is authoritative.*`
- Keep a short **Traps** note under any list with a byte-level hazard or a target divergence, and a `> **Trap.**` callout for any value removed as never-valid — the removal is the fix, but the note is what stops it being re-added.
- Update the counts and date at the top of `fields/04-software-functionality.md` if the taxonomy changed.
- Add the run date to the owning field file's `## Provenance` section ("Vocabulary block re-verified YYYY-MM-DD").
- Never edit `repos/*/hssi_metadata.md` from this skill. If reconciliation invalidates a value already recorded in canonical metadata files, **report the affected files and values** and let the orchestrator route the fix through the normal Updater pipeline.

### A5. Verify

Re-run the A2 diff against the edited field files and confirm zero doc-only and zero live-only entries for every list, except deliberately annotated target-divergent rows. Byte-check the known traps explicitly rather than eyeballing them.

---

## Step B: Re-verify the field files' site facts against hssi-website

> The field files describe the website as it was on a recorded commit. The router
> `hssi-field-definitions/SKILL.md` carries that commit in an HTML comment:
> `<!-- site-facts: verified against hssi-website <sha> (<commit date>) on <run date> -->`.
> Nothing detects website drift on its own; this step does.

### B1. Get the source and the recorded commit

Clone or pull `hssi-website` as in Step 1. Read the `site-facts:` line from the router and note its sha.

### B2. Diff the watched files

```bash
cd <hssi-website> && git diff --stat <recorded-sha>..HEAD -- \
  django/website/views/search.py \
  frontend/filters \
  django/website/templates/website/software_detail.html \
  django/website/models/serializers/software.py \
  django/website/forms/names.py \
  django/website/forms/submission_data.py \
  django/website/models/software.py django/website/models/vocab.py
```

If the diff is empty, move the router line forward to `HEAD` and today's date and stop. Otherwise, for
each changed file, re-read it and reconcile every statement that depends on it:

| Source file | What it decides | Where the field files state it |
|---|---|---|
| `views/search.py` | free-text tiers T1–T4 and their fields; `_FIELD_ALIAS_MAP` field-search codes and what each matches | router index **Search** and **Code** columns; each file's *Free-text search* and *Field search* bullets |
| `frontend/filters/filterMenu.ts`, `filterGroup.ts`, `filterTab/*.ts` | which fields have a sidebar tab, what the tab lists, folding (Python/Fortran rows), parent–child inclusion, disabled tabs | router **Filter tab** column; each file's *Filter* bullet (Fields 4, 5, 13, 17, 22) |
| `templates/website/software_detail.html` | detail-page sections, labels, link text and fallbacks (`UNKNOWN` → raw URL), what renders in parentheses, markdown rendering, header contents | each file's *Detail page* bullet |
| `models/serializers/software.py` | JSON-LD (`applicationCategory`, `author`, `mentions`, `keywords` …) and the `/api/view/` readback shape | each file's *JSON-LD* bullet; *Readback* lines in *Payload and roundtrip notes* |
| `forms/names.py` (`TTEXPL_*`, `TTBEST_*`) | the form's field descriptions and tooltips | each file's *What it is* / *How to fill it* text (quoted from the form) |
| `forms/submission_data.py` | requirement level per field | router **Level** column; each file's header `Level:` |
| `models/software.py`, `models/vocab.py` | field types, column caps (`URLField` 200, RelatedItem name 128), sorted M2M fields, `ControlledList` vs `ControlledGraphList` | *Payload and roundtrip notes*; Step A's model list (see Step 5b) |

Reconcile by rewriting the statement to what the source now does; never soften a fact into "may". Where a
rule rests on the fact (Field 5's coarse-parent rule rests on the Region filter not inheriting; Fields
29/30's URL-form rule rests on the raw URL being the link text), say so in the report — the owner decides
whether the rule changes, this step changes only the facts.

### B3. Record and report

Update the router's `site-facts:` line to the `HEAD` sha, its commit date and today's date. Report every
changed file, every statement rewritten (file and line), and every rule whose premise moved.

---

## Workflow (API source sync)

Steps 1–6 below sync the **API contract** from source. They are independent of Steps A and B — run any alone.

### Step 1: Get the hssi-website Source

Clone or pull the HSSI website repository:

```bash
# Clone to a temp location if not already present
git clone https://github.com/Heliophysics-Software-Search-Interface/hssi-website.git /tmp/hssi-website

# Or pull if already cloned
cd /tmp/hssi-website && git pull
```

If the user already has a local clone (e.g., `~/git/hssi-website`), use that instead.

### Step 2: Read the Relevant Source Files

Read these specific files:

#### Shared (covers both submit and update paths)

1. **`concept/import_submission_notes.md`** — Official API documentation. Field list, required/recommended/optional classification, object schemas.

2. **`concept/import_submission.json`** — HSSI developers' curated example payload. Authoritative template for the new-format payload shape; cross-reference with the serializer source.

3. **`django/website/models/serializers/submission.py`** — The DRF `SubmissionSerializer`. Authoritative field mapping and transformation logic for both `POST /api/submission/` (full create) and `PATCH /api/data/software/<uid>/` (partial update — same serializer with `partial=True`). Pay special attention to:
   - `to_internal_value_user()` — required field validation (skipped under `partial=True`)
   - `_get_or_create_person()` — Person dedup and field names (`given_name`/`family_name`)
   - `_get_or_create_org()` — Organization dedup
   - License handling (plain string input, `License.objects.filter(name__iexact=...)`)
   - Version object handling (`number`, `release_date`, `description`, `version_pid`)
   - `update_user()` / `_apply_user_fields()` — the partial-update branch invoked by PATCH

4. **`django/hssi/camel_case_renderer.py`** — `decamelize_data()` and `CamelCaseJSONRenderer`. Explains how incoming camelCase JSON keys are auto-converted to snake_case before the serializer sees them.

5. **`django/website/models/serializers/util.py`** — `SerialView` enum and shared serializer utilities used by submission and software serializers; `HssiSerializer.update()` dispatches to `update_user()` for the USER view.

6. **`django/website/urls.py`** — URL routing. Confirms the current endpoint paths.

#### Submit path

7. **`django/website/views/api/software_api.py`** — `SubmissionAPI` (the `POST /api/submission/` view). Shows the request/response shape, status codes, and the post-commit side effects (`SoftwareEditQueue` creation, email notification) that run outside the atomic transaction.

#### Update path

8. **`django/website/views/api/software_api.py`** (also for update) — `SoftwareDetailAPI`. The `patch()` method is the canonical update endpoint. `get_permissions()` switches to `HasUpdateToken` for PATCH; `get_serializer_class()` switches to `SubmissionSerializer` for PATCH. `SoftwareListAPI.get()` implements the `?repo_url=<url>` filter used by the updater's lookup step.

9. **`django/website/views/api/permissions.py`** — `HasUpdateToken` bearer-token permission class used by `SoftwareDetailAPI.patch()`. Uses `secrets.compare_digest`; fails closed when `HSSI_UPDATE_TOKEN` is unset.

10. **`django/website/test_update_api.py`** — Regression tests for `PATCH /api/data/software/<uid>/` and the `/api/list/software/?repo_url=` lookup. Treat as the authoritative behavioral spec for the update path: response shape, error codes, M2M replacement, `null`-clears-scalar, empty-list-clears-M2M, `submitter` rejection, token unset/invalid.

### Step 3: Compare Against Current Skills

Read the current versions of:
- `.claude/skills/submission-payload/SKILL.md`
- `.claude/skills/submission-verification/SKILL.md`
- `.claude/skills/update-payload/SKILL.md`

Compare the source files against the current skill content. Look for:
- New fields added to the API
- Renamed keys (e.g., snake_case → camelCase changes)
- Changed shapes (e.g., string → object, array → single value)
- New or changed controlled-list endpoints
- New backend quirks or representation differences
- Changes to required vs optional field classification
- Endpoint route or HTTP method changes (especially in `urls.py` and the view classes)

### Step 4: Update the Skill Files

Update `submission-payload/SKILL.md`, `submission-verification/SKILL.md`, and `update-payload/SKILL.md` to reflect any changes found. Specifically:

- Update the Section-to-API-Field Mapping table
- Update Object Specifications if schemas changed
- Update Known Backend Quirks with any new findings
- Update the controlled-list endpoint table if endpoints changed
- Update the known representation differences in `submission-verification`
- Update the *Payload and roundtrip notes* section of any `hssi-field-definitions/fields/NN-*.md` whose field's key, shape or quirk changed
- For `update-payload`: keep the PATCH endpoint contract, lookup endpoint, and field-shapes table aligned with `software_api.py` + `test_update_api.py`

### Step 5: Report Changes

Produce a summary of what changed and why:
- List each change made to the skill files
- Note any discrepancies between `import_submission.json` and the actual serializer behavior
- Flag any breaking changes that might affect existing payloads
- If Step A ran, report the vocabulary diff by class (doc-only / live-only / target-divergent), the junk rows flagged, and any canonical `repos/*/hssi_metadata.md` values invalidated by the reconciliation

### Step 5b: Check whether the vocabulary contract changed

Two source-level changes silently invalidate Step A's assumptions, so check for them whenever you have the source checked out:

- **`django/website/models/vocab.py`** — a new `ControlledList`/`ControlledGraphList` model means a new vocabulary to reconcile (add it to Step A1's model list); a model switching between `ControlledList` and `ControlledGraphList` changes whether values are flat or `Parent:Child`.
- **`_normalize_term` / `_get_controlled_item` / `_get_graph_list_item` in `serializers/submission.py`** — these currently do nothing but `.strip()` plus `name__iexact`. If an alias table or fuzzy matching is ever introduced, the "one character off fails the submission" warnings throughout these skills become wrong and must be rewritten, not just re-dated.

### Step 6: Cleanup

- If you cloned to `/tmp/hssi-website`, either leave it (for future runs) or remove it based on user preference
- If using the user's local clone, leave it as-is
