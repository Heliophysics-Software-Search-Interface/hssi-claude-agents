# Controlled vocabularies — the live API is authoritative

Every **Possible Values** block in the `fields/*.md` files is a **dated snapshot**, not the source of
truth. The live vocabulary on the target you are working against is authoritative and wins on any
conflict:

```
GET <target>/api/models/<Model>/rows/all/
```

**Use the snapshot to pick candidates; use the API to confirm they exist.** Confirm every
controlled-list value against the live endpoint for the target you are working with before writing it
into a payload or an `hssi_metadata.md`. In extract-only mode, with no target given, resolve against
production `https://hssi.hsdcloud.org`. If a value you want has no live row, record what the source
actually says and flag it rather than substituting a near-miss.

**Why exactness matters.** `serializers/submission.py` resolves controlled lists with
`Model.objects.filter(name__iexact=value)` after nothing more than `.strip()`. There is no alias
table and no fuzzy matching. A value that is one character off — a missing trailing period, a
straight quote where the row has a curly one — raises `ValidationError: Unknown value` and fails the
entire submission. Case is the only difference that is forgiven. So: match case-insensitively after
trimming (that is exactly what the backend does), and treat any other difference as a real submission
failure, not a nitpick.

**Vocabularies can differ between targets.** As of the 2026-08-06 audit, the closed vocabularies are
identical between `https://hssi.hsdcloud.org` and `http://localhost` except `License` and `DataInput`:
production still carries three legacy duplicate License rows and one junk DataInput row that
localhost has retired (see `fields/15` and `fields/17`). Never assume a value that worked on one target
exists on the other — and never treat an extra row on one side as automatically the correct value.
Validate against the target actually in play.

**Only Keywords (Field 16) is an open vocabulary** — `_get_or_create_keyword` creates missing rows,
so it can never fail this check. The simple closed lists (Fields 4, 5, 13, 15, 17–23) reject unknown
values. Fields 31–32 are structured records whose backend **creates** an `InstrumentObservatory` row for
an unknown identifier or an unmatched bare name, so nothing rejects a bad entry there — enforce Field 31's
SPASE resolution and payload gate yourself.

## How each agent applies this

- **Extractor:** confirm each candidate against the live endpoint before writing it into the dossier
  (Fields 4, 5, 13, 15, 17, 18/19, 20, 21, 22, 23 and 31/32).
- **Validator:** a value's presence in a snapshot is not evidence it is valid, and its absence is not
  evidence it is invalid. **Only raise an ERROR when the live endpoint has no matching row.**
- **Submitter / Updater:** for each controlled-list field (`softwareFunctionality`, `relatedRegion`,
  `programmingLanguage`, `inputFormats`, `outputFormats`, `operatingSystem`, `cpuArchitecture`,
  `developmentStatus`, `dataSources`, `relatedPhenomena`, `license`) fetch the endpoint on the target
  URL and normalize each value to an exact match from the endpoint's `name` field. If no exact match
  exists, flag it for review — do not silently drop or approximate.

## Field → model endpoint

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
| 31/32 Related Instruments & Observatories | `/api/models/InstrumentObservatory/rows/all/` (`type` 1 = instrument, 2 = observatory — **SPASE-only**; see the resolution ladder in `fields/31`) |

Notes:

- **Model names resolve case-insensitively.** `CpuArchitecture` is the canonical Django class name;
  `CPUArchitecture` also works. There is no `/api/models/` index endpoint — it 404s.
- **`FunctionCategory`, `Region`, and `Phenomena` are graph lists.** `FunctionCategory` is
  hierarchical, so values are written `Parent: Child` (space after the colon is canonical; the
  serializer strips whitespace around it). `Region` and `Phenomena` are currently flat — every row is
  a top-level value.
- **Large lists:** `InstrumentObservatory` is ~7,700 rows. Fetch once to a file with
  `?columns=id,name,identifier,type,abbreviation` (keep `id`, or the API returns an empty `data[]`)
  and filter locally; never load every row into context.
- **Keywords are the only open vocabulary.** `_get_or_create_keyword` creates missing rows; the simple
  closed lists raise on an unknown value; Fields 31–32 silently create rows (see above).

To re-verify the snapshots against live and refresh them, use the `update-api-spec` skill (Step A);
it rewrites the fenced `vocab:` blocks in the field files plus the supporting items its Step A4 lists
(provenance lines, counts, trap notes), nothing else.
