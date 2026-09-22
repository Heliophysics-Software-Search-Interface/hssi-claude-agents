# Controlled vocabularies — the live API is authoritative

<!-- Part 1 moved verbatim from resource_submission_form_fields.md lines 14-47; Part 2 from the former SKILL.md body (2026-09-22). -->

## Part 1 — rules (from RSFF)

Every **Possible Values** list below is a **dated snapshot**, not the source of truth. The live
vocabulary on the submission target is authoritative and wins on any conflict:

```
GET <target>/api/models/<Model>/rows/all/
```

**Use the snapshot to pick candidates; use the API to confirm they exist.** Confirm every
controlled-list value against the live endpoint for the target you are working with before writing it
into a payload or an `hssi_metadata.md`.

**Why exactness matters.** `serializers/submission.py` resolves controlled lists with
`Model.objects.filter(name__iexact=value)` after nothing more than `.strip()`. There is no alias
table and no fuzzy matching. A value that is one character off — a missing trailing period, a
straight quote where the row has a curly one — raises `ValidationError: Unknown value` and fails the
entire submission. Case is the only difference that is forgiven.

**Vocabularies can differ between targets.** As of the 2026-08-06 audit, the closed vocabularies are
identical between `https://hssi.hsdcloud.org` and `http://localhost` except `License` and `DataInput`:
production still carries three legacy duplicate License rows and one junk DataInput row that
localhost has retired (see Fields 15 and 17). Never assume a value that worked on one target exists
on the other — and never treat an extra row on one side as automatically the correct value.

**Only Keywords (Field 16) is an open vocabulary** — `_get_or_create_keyword` creates missing rows.
Every other list rejects unknown values.

The field-to-endpoint mapping is in `.claude/skills/hssi-field-definitions/SKILL.md`, which wraps this
document. To re-verify these snapshots against live and refresh them, run **Step A** of the
`update-api-spec` skill.

## Part 2 — field → model endpoint and matching notes (from the former SKILL.md body)

## Controlled vocabularies: the live API is authoritative

The **Possible Values** lists in that document are a **dated snapshot**, not the source of truth. The
live endpoint on the submission target always wins:

```
GET <target>/api/models/<Model>/rows/all/
```

**Before writing any controlled-list value into a payload or an `hssi_metadata.md`, confirm it
against the live endpoint for the target you are working with.** Use the snapshot to pick
*candidates*; use the API to confirm they *exist*.

This is not a formality. `serializers/submission.py` resolves controlled lists with
`Model.objects.filter(name__iexact=value)` after nothing more than `.strip()`. There is no alias
table and no fuzzy matching, so a value that is one character off — a missing trailing period, a
straight quote where the row has a curly one — raises `ValidationError: Unknown value` and fails the
whole submission.

**Vocabularies can differ between targets.** As of 2026-08-06 the closed vocabularies were identical
between `https://hssi.hsdcloud.org` and `http://localhost` except `License` and `DataInput`, where
production still carries three legacy duplicate License rows and one junk DataInput row that localhost
has retired. Never assume a value that worked on one target exists on the other — and never treat an
extra row on one side as automatically correct. See Fields 15 and 17 for the durable traps.

### Field → model endpoint

| Field | Model endpoint |
|-------|----------------|
| 4 Software Functionality | `/api/models/FunctionCategory/rows/all/` |
| 5 Related Region | `/api/models/Region/rows/all/` |
| 13 Programming Language | `/api/models/ProgrammingLanguage/rows/all/` |
| 15 License | `/api/models/License/rows/all/` |
| 16 Keywords | `/api/models/Keyword/rows/all/` (**open vocabulary** — missing values are created) |
| 17 Data Sources | `/api/models/DataInput/rows/all/` |
| 18/19 Input & Output File Formats | `/api/models/FileFormat/rows/all/` |
| 20 Operating System | `/api/models/OperatingSystem/rows/all/` |
| 21 CPU Architecture | `/api/models/CpuArchitecture/rows/all/` |
| 22 Related Phenomena | `/api/models/Phenomena/rows/all/` |
| 23 Development Status | `/api/models/RepoStatus/rows/all/` |
| 31/32 Related Instruments & Observatories | `/api/models/InstrumentObservatory/rows/all/` (`type` 1 = instrument, 2 = observatory — **SPASE-only**; see the Field 31 resolution ladder) |

Notes:

- **Model names resolve case-insensitively.** `CpuArchitecture` is the canonical Django class name;
  `CPUArchitecture` also works. There is no `/api/models/` index endpoint — it 404s.
- **`FunctionCategory`, `Region`, and `Phenomena` are graph lists.** `FunctionCategory` is
  hierarchical, so values are written `Parent:Child` and the serializer splits on `:`. `Region` and
  `Phenomena` are currently flat — every row is a top-level value.
- **Keywords are the only open vocabulary.** `_get_or_create_keyword` creates missing rows; every
  other list raises on an unknown value.

## Part 3 — how the agents apply this (extractor)

<!-- moved from .claude/agents/hssi-metadata-extractor.md:262-270 -->
**Controlled-list values — the live API is authoritative, not the skill's snapshot.** The **Possible Values** lists in `hssi-field-definitions` are a dated snapshot. Use them to *pick candidates*; use the live vocabulary to confirm those candidates *exist* before writing them into `hssi_metadata.md`:

```
GET <target>/api/models/<Model>/rows/all/
```

Applies to Fields 4, 5, 13, 15, 17, 18/19, 20, 21, 22, 23 and 31/32 — the endpoint for each is tabled in the `hssi-field-definitions` skill. In extract-only mode (no target given), resolve against production `https://hssi.hsdcloud.org`.

This matters because the backend matches with `name__iexact` after a bare `.strip()` — no aliases, no fuzzy matching. A value that is one character off (a missing trailing period, a straight quote where the row has a curly one) fails the whole submission later. Vocabularies also differ by target: as of 2026-08-06 production has legacy `License` names and a junk `DataInput` value that do not exist on localhost. If a value you want has no live row, record what the repo actually says and flag it for the user rather than substituting a near-miss.

## Part 4 — how the agents apply this (validator rule 3, first paragraph)

<!-- moved from .claude/agents/hssi-metadata-validator.md:374-374 -->
3. **Check allowed values against the live API, not the snapshot.** For controlled-list fields (Software Functionality, Related Region, Programming Language, Data Sources, File Formats, Operating System, CPU Architecture, Phenomena, Development Status, License), the authority is `GET <target>/api/models/<Model>/rows/all/` — the endpoint for each field is tabled in the `hssi-field-definitions` skill. The **Possible Values** lists in `resource_submission_form_fields.md` are a **dated snapshot** for orientation only; a value's presence there is not evidence it is valid, and its absence is not evidence it is invalid. **Only raise an ERROR when the live endpoint has no matching row.** Match case-insensitively after trimming (that is exactly what the backend's `name__iexact` does) but flag any other difference — a missing trailing period or a straight-vs-curly quote is a real submission failure, not a nitpick. Keywords (Field 16) is an open vocabulary and can never fail this check. Where prod and localhost differ (as `License` does), validate against the target actually in play.

## Part 5 — how the agents apply this (submitter check C)

<!-- moved from .claude/agents/hssi-metadata-submitter.md:108-111 -->
**C. Controlled-list normalization** — For each controlled-list field (`softwareFunctionality`, `relatedRegion`, `programmingLanguage`, `inputFormats`, `outputFormats`, `operatingSystem`, `cpuArchitecture`, `developmentStatus`, `dataSources`, `relatedPhenomena`, `license`):
  - Fetch the corresponding endpoint on the target URL (see `submission-payload` skill for endpoint list)
  - Normalize each value to an exact match from the endpoint's `name` field
  - If no exact match exists, flag for user review — do not silently drop or approximate
