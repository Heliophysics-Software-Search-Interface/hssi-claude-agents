---
name: hssi-field-definitions
description: >
  Complete HSSI Resource Submission form field definitions, allowed values, and extraction guidance
  for all 33 metadata fields. Use whenever working with HSSI metadata — extracting, validating,
  submitting, or reasoning about field requirements.
user-invocable: false
---

# HSSI Field Definitions

The full field reference is `resource_submission_form_fields.md` — **at the repository root, not in
this skill directory.** The `@` line at the bottom auto-loads it. If it did not resolve (no field
definitions appear after this section), **Read `<repo-root>/resource_submission_form_fields.md`
directly** — the path is relative to the repo root, not to this skill's base directory.

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

**Vocabularies can differ between targets.** As of 2026-07-29 every vocabulary was identical between
`https://hssi.hsdcloud.org` and `http://localhost` **except `License`**, where two rows exist only on
prod. Never assume a value that worked on one target exists on the other.

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

To re-verify the snapshot against live and refresh it, use the `update-api-spec` skill.

---

@resource_submission_form_fields.md
