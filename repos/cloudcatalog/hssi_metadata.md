# HSSI Metadata — CloudCatalog

**HSSI Software ID:** a7f6fd15-9b3c-4cae-a029-0da92222f465
**Repository:** https://github.com/heliocloud-data/cloudcatalog
**Source Revision:** 1c7b8dbbd150b6148ee683484c69d46e5b44f76d (branch `develop`, 2026-07-21)
**Extraction Date:** 2026-07-31
**Validation Date:** 2026-10-29
**Validation Status:** PASS
---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

Not part of the stored metadata record.

---

### 2. Persistent Identifier (RECOMMENDED)
Not found

No software DOI exists. There is no Zenodo software record, no `CITATION.cff`, no
`codemeta.json`, no `.zenodo.json`, and no DOI badge in `README.md`. A DataCite search for
`cloudcatalog` returns only Zenodo *publications* and *datasets* from the HelioCloud team, not
software records (see Fields 14, 27, 28). The repository has **zero tags and zero releases**, so
there is no GitHub–Zenodo archive from which a concept DOI could have been minted.

---

### 3. Code Repository (MANDATORY)
https://github.com/heliocloud-data/cloudcatalog

Confirmed live: GitHub reports `full_name` `heliocloud-data/cloudcatalog`, default branch
`develop`, not archived. Matches `pyproject.toml` `[project.urls] Repository`. The PyHC registry
records the same repository with a trailing slash; the slash-free form is used here.

---

### 4. Software Functionality (RECOMMENDED)
- Data Processing and Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing
- Servers and Environments
- Servers and Environments: Distribution/Access
- Servers and Environments: Data servers processing and handling

Both parent categories are included alongside their subcategories. Note that `Processing` and
`Distribution/Access` each exist twice in the vocabulary; the values here are the ones under
`Data Processing and Analysis` and `Servers and Environments` respectively, **not** the
same-named children of `Mission-related`.

Per-value evidence:

| Value | Evidence |
|---|---|
| Data Processing and Analysis | Parent category of the three subcategories below. |
| ...: Data Access and Retrieval | `CatalogRegistry`, `CloudCatalog.request_cloud_catalog()`, `get_entry()`, `sample_file()`, `stream()`, `stream_uri()`, `EntireCatalogSearch.search_by_id/title/keywords()` in `src/cloudcatalog/main.py`; release 1.3.1 adds `CloudCatalog.ls_wildcard()`, which selects the file keys of a returned index that match a filename wildcard (PR #46; all read at `a3c2509`). |
| ...: File Format Conversion | `update_catalog_from_csv()` ingests `cat.csv` and writes `catalog.json` (`src/cloudcatalog/updater/catalog_updater.py`); `cloudcat_indexer.write_indexes()` converts `catalog.json` into per-id HTML index pages (`src/cloudcatalog/generators/cloudcat_indexer.py`). Both present at the source revision and at `a3c2509`. *(A third converter, `cloudcatalog-manifest2indices`, shipped in the 1.2.1 package. PR #39, "Moved ops tools to heliocloud_tools repo", deleted `generators/manifest2indices.py` in the source-revision merge, and release 1.3.1, whose package contents equal `a3c2509`, does not contain it; `pyproject.toml` still declares the console script, which therefore fails. Never relied on as evidence here.)* |
| ...: Processing | Index post-processing in `request_cloud_catalog()`: spec-version-dependent fixups (synthesises a `stop` column for pre-0.5 indices), `#`-prefixed header stripping, positional column normalisation, multi-year frame concatenation, ISO-8601 parsing and time-range filtering; `validate_and_fix_timestamp()` repairs malformed timestamps. |
| Servers and Environments | Parent category of the two subcategories below. |
| ...: Distribution/Access | The package *is* the access layer for a decentralised, serverless data-distribution standard: "RESTful & serverless (indices are flat files alongside their datasets)" (`README.md`); `docs/cloudcatalog-spec.md` section 2 defines the global `HelioDataRegistry.json` bucket registry; `src/cloudcatalog/validators/validate_cloudcatalog_api.py` (renamed `validate_apiheliocloud.py` by PR #43 with its content unchanged; read at `a3c2509`) exercises the public service endpoint `https://api.heliocloud.org/cloudcatalog?id=`. |
| ...: Data servers processing and handling | Server-side catalog maintenance tooling: `updater/catalog_updater.py` (safe merge/update of `catalog.json`), `updater/recatalog.py` (bulk relocation of holdings, rewriting both `catalog.json` and every index CSV, with backups), `updater/version_file.py` (versioned backups), `validators/validation.py` (`Validator` — JSON-Schema validation of global/local catalogs, ID-uniqueness checks, index-file reachability), `validators/validator.py` (spec compliance of new entries). PR #43 renamed these two `validation_class.py` and `validate_json.py` respectively, with their content unchanged, deleted the overlapping `validate_cloudcatalog.py` script, and added a verbose option to `catalog_updater.py` (read at `a3c2509`). |

**At release 1.3.1** (`1c7b8db..a3c2509`, the code PyPI 1.3.1 ships): besides the wildcard filter and
the renames above, PR #44 makes lookups that find nothing log the miss and return `None` or an empty
result instead of raising. Neither the filter, which is retrieval, nor the error handling adds a
category, and every value above keeps its evidence.

**Considered and excluded:**
- `Data Processing and Analysis: Time Series Analysis` — the temporal filtering in
  `request_cloud_catalog()` operates on *file-index metadata*, not on science measurements.
- `Data Visualization` (and `: Web-Based`) — `cloudcatalog-gui` is a Tkinter form for editing
  catalog metadata, and `cloudcat_indexer.py` emits static HTML link pages; neither renders data.
- `Mission-related` (`: Archive`, `: Inventory`, `: Ingest`) — the package is deliberately
  mission-agnostic infrastructure, not part of any single mission's ground system.
- `Servers and Environments: Infrastructure as Code` — the CDK/IaC code lives in the separate
  `heliocloud-data/platform` repository, not here.

---

### 5. Related Region (RECOMMENDED)
Not found — deliberately empty

CloudCatalog is domain-independent software (Field 5 rule 2). It indexes, finds and retrieves files
for whatever datasets a data owner chooses to publish, and it behaves identically whatever physical
region the data describe; it computes, models and analyses no physics, so no region passes rule 4.

**Sweep at `a3c2509`** (`src/`, `README.md`, every `.md` file under `docs/`, and `pyproject.toml`):
case-insensitive searches for magnetospher, ionospher, thermospher, atmospher, aurora, corona,
photospher, chromospher, "solar wind", heliospher, magnetotail, magnetosheath, plasmasphere,
"radiation belt", interplanetary, heliosheath, "solar interior", Mars, Jupiter, Saturn, Uranus and
Neptune each return no match, while a `catalog` control on the same scope matches. Word-anchored
searches on the same scope find no `solar` and no `earth`, and find `sun` only in example metadata
for a solar-image dataset: the example Info file in section 6.2 of `docs/cloudcatalog-spec.md`
(`"Size of sun in pizels"`, `"x coord of sun center"`), repeated in the five earlier specification
versions under `docs/`. The example file catalog in section 4.6 of the same specification carries
that quantity as an `RSUN` column. Example data is not scope (rule 3). The project's own
descriptions (the README, the `pyproject.toml` description and the DASH 2025 poster abstract) name
no region; the PyHC registry entry carries no Science Area tag.

**Superseded values.** The record previously carried `Earth Atmosphere`, `Earth Magnetosphere`,
`Interplanetary Space`, `Planetary Magnetospheres` and `Solar Environment` — the five rows of the
legacy dropdown, kept with only the note that none of them was wrong for a general heliophysics
data-indexing tool and with no code evidence. Rule 8 re-derives incumbents, and a legacy-five
default that no evidence supports is cleared, so none of the five is kept, and the field is
evidenced-empty under rules 2 and 9.

**Considered and rejected** (test fixtures and example data are not scope, rule 3):
- `Corona` and `Solar Environment` — the datasets the client is *tested against* happen to be coronal
  EUV imaging: `aia_0094` (SDO/AIA 94 Å, `README.md`), `euvml_stereoa_171` (STEREO EUVI 171 Å,
  `tests/test_hdrl.py::test_hdrl_euv`) and `PARKERSOLARPROBE_WISPR_FITS_LEVEL2_PT30M`
  (`tests/test_reverse_lookup.py`). That is the same evidence class rejected in Fields 31–32, where
  every instrument and observatory name in the repository is a test fixture or tutorial example.
- `Earth Magnetosphere`, `Earth Inner Magnetosphere` and `Earth Magnetotail` — the MMS and LANL
  `A1_K0_MPA` fixture ids (Field 31) and the THEMIS `THA_L2_FFT` id in `tests/test_wildcard.py`;
  fixtures again.
- `Solar Wind` and `Photosphere` — supportable only by inferring instrument coverage from example
  dataset ids.
- The `heliophysics` keyword and HelioCloud's heliophysics holdings — a discipline, not a region; the
  specification itself is for "sharing datasets across cloud frameworks" (`README.md`).

---

### 6. Authors (MANDATORY)

Author order is significant and is: Antunes, Jeschke, Shumate, Knowles.

**1. Alex Antunes**
- Author Identifier: https://orcid.org/0000-0002-3098-2602
- Affiliation: Johns Hopkins University Applied Physics Laboratory — https://ror.org/029pp9z10
- Affiliation: Project Calliope — identifier not found. The ROR v2 query `query=Calliope`
  (2026-10-28) returns a single organization, the unrelated Calliope Film Resources, while the same
  query form for Johns Hopkins University Applied Physics Laboratory returns `029pp9z10` first.
- Evidence: ORCID 0000-0002-3098-2602 resolves to "Alex Antunes", employment
  "Johns Hopkins University Applied Physics Laboratory" (ROR `029pp9z10`), dept SES/SRN.
  Commits as `Sandy Antunes <sandy.antunes@jhuapl.edu>` (82 commits at `a3c2509`) and `antunak1` (30);
  named contact in the PyHC registry and in `docs/CloudCatalog-Demo.ipynb`.
- **Both affiliations, and why.** This author's record carries JHU/APL and Project Calliope together.
  Two other catalogued packages credit the same person as "Antunes, Sandy": CDFlib's DataCite record
  (10.5281/zenodo.1481144) with the affiliation Project Calliope and no identifier, and PySPEDAS's
  `CITATION.cff` (`spedas/pyspedas`) with "Johns Hopkins University Applied Physics Laboratory", this
  ORCID's own employment. That is the same human, so the catalogue holds one record for him carrying
  the union of the institutions its sources attribute to him; an affiliation is never dropped in
  favour of a newer one. On 2026-10-29 HSSI held that one record, "Alex Antunes" with this ORCID and
  both affiliations, on CloudCatalog, CDFlib and PySPEDAS. The identification rests on the commit
  chain recorded above plus the PySPEDAS `CITATION.cff` entry. It does **not** rest on the ORCID name:
  that record publishes no "Sandy" alias, so a name-only inference would not have been sufficient.

**2. Chris Jeschke**
- Author Identifier: https://orcid.org/0009-0008-8557-6709
- Affiliation: Johns Hopkins University Applied Physics Laboratory — https://ror.org/029pp9z10
- Evidence: 8 commits as `Chris Jeschke <chris.jeschke@jhuapl.edu>`, including the repository's
  initial check-in (`2738665`, `04e4b23` "Initial check in of scregistry"); +5,402 lines, the
  second-largest contribution. An ORCID public search returns exactly one JHUAPL Jeschke:
  0009-0008-8557-6709 ("Chris, Christopher Jeschke", employment *Johns Hopkins University Applied
  Physics Laboratory*, **Space Exploration Sector**, from 2023-01, ROR `029pp9z10`) — name,
  institution, sector and timeframe all agree. The ORCID is **not stated in the repository**; it
  rests on that external identity match.

**3. Peter Shumate**
- Author Identifier: https://orcid.org/0009-0003-6088-5437
- Affiliation: Johns Hopkins University Applied Physics Laboratory — https://ror.org/029pp9z10
- Evidence for the spelling **Shumate** (three independent primary sources):
  1. Git history — 6 commits authored as `Peter Shumate <peter.shumate@jhuapl.edu>` /
     `peter.shumate <peter.shumate@jhuapl.edu>` (`8c00867` "#6: Update MIT License",
     `66337eb` "#10: Add GitHub issue templates", plus merges).
  2. ORCID 0009-0003-6088-5437 — "Peter **Shumate**", Research Software Engineer at Johns
     Hopkins University Applied Physics Laboratory from 2023-08 (ROR `029pp9z10`).
  3. Zenodo 10.5281/zenodo.13887203 ("HelioCloud as a replicable open science architecture",
     Gateways 2024) lists creator "**Shumate**, Peter" alongside Antunes and Jeschke.
  No source anywhere spells it "Schumate".
- **Previous incorrect value:** this record previously held the misspelling **`Schumate`** with no
  identifier. Corrected to `Shumate` with the ORCID above, preserving the author's existing
  identity and position in the author order. The ORCID for Jeschke was added in the same
  correction, also to a pre-existing identity that carried none.

**4. Lisa Knowles**
- Author Identifier: https://orcid.org/0000-0001-8181-0475
- Affiliation: Johns Hopkins University Applied Physics Laboratory — https://ror.org/029pp9z10
- Evidence: primary author of `src/cloudcatalog/validators/validator.py` at the source revision
  (`git blame`: 201 of 305 current lines; PR #43 later renamed the file `validate_json.py` with its
  content unchanged), whose module docstring reads
  *"Contact Lisa Knowles lisa.knowles@jhuapl.edu"*. 5 commits as
  `Knowles, Lisa A <Lisa.Knowles@jhuapl.edu>` / `Lisa Knowles <lisa.knowles@jhuapl.edu>`
  (+467 / −204 lines) — a larger code contribution than Peter Shumate's (+58 / −21).
  Affiliation from the `@jhuapl.edu` address and the repository copyright holder. She is also named
  on the DASH 2025 poster byline (Field 14).
- **Identity linkage for the ORCID (Field 6 rule 14).** 0000-0001-8181-0475 is the only public ORCID
  record named "Lisa Knowles" (fielded given-name and family-name search, 2026-10-28), and it lists no
  employments and no works, so the ORCID record alone cannot confirm identity. DOI records supply the
  linkage: six Zenodo deposits carry this ORCID beside "Knowles, Lisa", all co-authored with Alex
  Antunes and Peter Shumate, five of them giving her affiliation as Johns Hopkins University Applied
  Physics Laboratory — 10.5281/zenodo.17392903 and 10.5281/zenodo.23211648, on which she is first
  author, and 10.5281/zenodo.17426660, 10.5281/zenodo.17435199, 10.5281/zenodo.23069202 and
  10.5281/zenodo.23186292. A DOI record carrying the ORCID beside this name is the linkage rule 14
  accepts.
- **Superseded value (rule 15).** This record previously left her identifier empty, because the ORCID
  record alone confirms nothing; the DOI records above supply the linkage it lacked. The record HSSI
  held for her had no identifier before this ORCID was added, and it holds the ORCID on that existing
  record rather than on a second one. A read on 2026-10-29 found that record crediting her on no
  other catalogue entry.

**Considered and excluded:**
- **Johns Hopkins University Applied Physics Laboratory as an organization author.**
  `pyproject.toml` declares exactly one author —
  `authors = [ {name = "Johns Hopkins University Applied Physics Laboratory LLC", email = "sandy.antunes@jhuapl.edu"} ]`
  — and PyPI carries the same `author_email` for every release; `LICENSE.MD` reads
  "Copyright © 2023 The Johns Hopkins University Applied Physics Laboratory LLC". That line is
  packaging / rights-holder boilerplate rather than an authorship claim, and the institution is
  already fully represented as the affiliation of all four person-authors. Listing it separately
  would read as though JHUAPL wrote the software in addition to, and apart from, its four named
  employees. The rights-holder fact is recorded in Field 15. (Had it been listed, the canonical
  ROR name "Johns Hopkins University Applied Physics Laboratory" would be used, dropping the
  "LLC" suffix.)
- `Nicholas Lenzi` (1 merge commit, 0 lines) and GitHub user `oms9` (2 merge commits, 0 lines) —
  merge-only, no authored content.
- **Co-authors of publications about the software who appear in no software-metadata source** (Field 6
  rule 7): Omar Shalaby, Brian Thomas, Jon Vandegriff, Sarah Rourke and Jeffery Bradford, named beside
  the authors on the DASH 2025 poster byline (Field 14); Brian Thomas, Jeffery Bradford, Sarah Rourke,
  Nicholas Lenzi and Jon Vandegriff among the creators of the Gateways 2024 demo record (weighed in
  Field 27); and Brian Thomas on the AGU 2024 abstract (weighed in Field 27). None of them appears in
  `pyproject.toml` or in an in-source contact string, and none has a non-merge commit: Nicholas
  Lenzi's one commit, `d3bbd0d`, is a merge (above).

No `CITATION.cff`, `AUTHORS`, `CONTRIBUTORS`, `codemeta.json` or `.zenodo.json` exists in the
repository. The author list is a union of the previously recorded authors, `pyproject.toml`,
in-source contact strings, and git history; nobody was dropped.

---

### 7. Software Name (MANDATORY)
CloudCatalog

See "Software name evidence" near the end of this file.

---

### 8. Description (MANDATORY)

```
CloudCatalog specification and API for providing and accessing cloud data
API for accessing the generalized CloudCatalog (cloudcatalog) specification for sharing data in and across clouds
Indexing millions of files for easy, searchable yet serverless and decentralized access is hard.  CloudCatalog is a lightweight CSV- and JSON-based indexing schema enabling HAPI-like "data ID + time range" queries on massive cloud datasets, and includes an implementation of the API and support tools in Python. Key goals include that (1) data owners control their own indices, (2) indices are static files to avoid incurring server costs, (3) searching is efficient and (4) indices are easily constructable and maintainable by the scientists/data-owners (the 'lazy' part). In addition to the FAIR principles of findability, accessibility, interoperability, and reusability, it is serverless and decentralized so that contributors can publish and update their open science data without the worries of external gatekeeping or server maintenance.
CloudCatalog is a generalized indexing specification for large cloud datasets.
The push to open science means many more published datasets, and finding and accessing is important to solve. CloudCatalog is an indexing method for sharing big datasets in cloud systems. It is scientist-friendly and it is easy to generate a set of indices. It uses static index files in time-ordered CSV format that are easy to fetch, easy to access via an API, and very low cost in both money and bandwidth needed to support. Metadata is kept in a simple JSON schema. We also provide a Python client toolset for scientists to access datasets that use CloudCatalog.
The CloudCatalog specification and tools are open source, created by the HelioCloud project, and already used for 2 Petabytes of publicly available NASA and scientist-contributed data. We hope the community continues to adopt this CloudCatalog standard (in github, linked off heliocloud.org).
* For sharing datasets across cloud frameworks
* Decentralized: data owners control their own data and access
* RESTful & serverless (indices are flat files alongside their datasets)
* Removes need for doing slow/expensive disk ‘ls’ on large holdings
* Global registry JSON points to owner-controlled ‘buckets’
* Uses minimal JSON to list metadata, CSV files for indices
* Searchable
* Public specification here on GitHub.
The API is designed for retrieving file catalog (index) files from a specific ID entry in a catalog within a bucket. It also includes search functionality for searching through all data index catalogs found in the bucket list.
We also include command-line tools for creating and viewing the networked catalogs: cloudcatalog-tree lists all toplevel datasets and the number of dataIDs available; cloudcatalog-spider adds valid years and the number of files; cloudcatalog-update-json updates catalog.json using metadata from catalog_stub.json; cloudcatalog-update-csv updates catalog.json using metadata from cat.csv; and cloudcatalog-gui provides a GUI for selecting files for cloudcatalog-update-json. The package also includes validators that check catalog.json files and dataset indices against the CloudCatalog specification.
```

The block above is the exact value, including the curly quotes U+2018/U+2019 in the bullets.

**Previous incorrect first line.** This record previously opened with "Shared Cloud
Registry specification and API for providing and accessing cloud data", the *old* GitHub About
text using the project's abandoned name. The current GitHub About wording is
"CloudCatalog specification and API for providing and accessing cloud data". The rename is
documented in the repository's own history: commit `f2fb4fa` (2023-10-18)
*"Changed scregistry.py to cloudcatalog.py ... FileRegistry to CloudCatalog ... scregistry to
cloudcatalog"*, and commit `11a7cfa` (2024-09-04) *"fixed inconsisent naming of CloudCatalog in
docs. Added .coveragerc file."* (quoted verbatim; the misspelling of "inconsistent" is the
author's). Residue of the old name survives only as `docs/scr_logo.png` (a "SHARED CLOUD REGISTRY"
logo) and the phrase "SCR Time format" in `docs/cloudcatalog-spec.md` section 5.

**Provenance of the two later paragraphs.** Paragraph 3 is the current `README.md` lead paragraph
verbatim. The same paragraph, up to whitespace, opens the two-paragraph abstract of the lead author's
DASH 2025 record (Zenodo 10.5281/zenodo.17398630), whose second paragraph, on reaching HelioCloud's
holdings with CloudCatalog and on performance and extensibility, is not in the README; the shared
paragraph is the project's canonical present-day summary. It sits third so
the opening, and therefore the search-result preview, is unchanged. The final paragraph covers the
command-line tooling and validators, from `README.md` section "Command-line tools" (lines 30–44)
and `pyproject.toml` `[project.scripts]`; without it the description covered only the read API and
omitted roughly half the shipped software.

*Scope note:* the final paragraph describes the software as released at the version this record
carries, 1.3.1, whose package contents equal `a3c2509`, and it does not name
`cloudcatalog-manifest2indices`. While the record carried 1.2.1, the paragraph ended with the clause
"; and cloudcatalog-manifest2indices converts an AWS Manifest.csv to individual [dataID]_[YYYY].csv
indices", which was true of the 1.2.1 package. PR #39 (2026-07-21) moved the converter to the
`heliocloud_tools` repository, and 1.3.1 contains no `generators/manifest2indices.py`, so the console
script that `pyproject.toml` and the README still list fails. Field 8 rule 2 drops a claim whose
module does not exist at the pin, even when the README makes it; removing the clause moved the final
"and" onto the `cloudcatalog-gui` item and changed no other word. Restore the clause only if the
converter returns to this package.

*Why the `cloudcatalog-gui` clause is kept.* The `cloudcatalog-gui` entry point targets
`cloudcatalog.catalogtools.catalog_updater:updater_gui`, and no `catalogtools` module exists in the
1.2.1 or 1.3.1 wheel or in any commit, so the command fails in both releases. The GUI itself ships
intact as `cloudcatalog.updater.updater_gui.updater_gui()`, a Tkinter form that drives
`update_catalog_from_json()`: the capability the clause describes is in the code, and only the
console-script wiring is broken. Drop the clause under rule 2 only if a release removes that module.

---

### 9. Concise Description (OPTIONAL, max 200 chars)
A Python package for retrieving cloud data file catalogs/indices

64 characters. Verbatim from the PyHC community registry (`_data/projects.yml`), the
highest-priority curated source.

**Considered and not selected** (166 chars): "A specification, Python API, and command-line toolset
for serverless, decentralized indexing and retrieval of file catalogs for massive cloud-stored
science datasets." It is composed rather than taken from a project source, and the registry's
curated summary is kept.

---

### 10. Publication Date (RECOMMENDED)
2023-10-26

The first release (Field 10 rule 4, anchor (a)): `cloudcatalog` 0.4 on PyPI, whose wheel and sdist
were uploaded at 2023-10-26T20:11:53Z and 20:11:55Z (PyPI JSON API, read 2026-10-28). It is the
earliest release of any kind: the project has no git tags, no GitHub releases and no Zenodo software
deposit (Fields 2 and 12). No release appeared under the pre-rename name either: PyPI has no
`scregistry` project, and the rename commit `f2fb4fa` (2023-10-18) precedes 0.4.

**Superseded value.** The record previously held 2023-05-31, GitHub's `created_at` for the
repository (2023-05-31T15:15:55Z). Anchor (b) accepts a creation date only when a first commit on
the pinned ancestry carries the same date, and the repository's single root commit, `2738665`
"Initial commit", is dated 2023-09-13: the repository was created empty and filled later, the trap
the Field 10 file calls "Repository created empty." The date follows neither anchor, so rule 3 does
not keep it and rule 4 replaces it.

**Not used:** the dates of the HelioCloud platform repository, from which code was moved into this
one (commits `019fa8a` and `5c1ef04`, Field 29). It is a separate project, and its dates do not
date this software (rule 2).

---

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

Per the Field 11 guidance — if no DOI has been obtained, indicate the repository host — and no
software DOI exists (Field 2).

---

### 12. Version (RECOMMENDED)
- **Version Number:** 1.3.1
- **Version Date:** 2026-09-23
- **Version Description:** Not found
- **Version PID:** Not found

Evidence, and the traps avoided:

- **PyPI is the release list.** The project has no git tags, no GitHub releases and no changelog.
  `https://pypi.org/pypi/cloudcatalog/json` (read 2026-10-28) lists 0.4 (2023-10-26), 0.5
  (2024-03-12), 0.6.1 (2024-08-21), 1.0.0 (2024-09-04), 1.0.2 (2025-02-19), 1.1.0 (2025-06-02), 1.2.1
  (2026-03-31), 1.3.0 (2026-09-21), 1.3.1 (2026-09-23) and 1.3.3 (2026-10-21), none yanked. For a
  project that does not tag, Field 12 rule 3 counts a PyPI upload of a version declared at a commit on
  the default branch's lineage or on a release branch cut from it.
- **1.3.1 is that release.** Commit `fe916cb` (2026-09-21, merged by PR #46) sets
  `version = "1.3.1"` on `develop`, and the 1.3.1 sdist, uploaded 2026-09-23T20:58:58Z (the wheel at
  20:58:57Z), matches the tree of `develop` at `a3c2509` (merged 2026-09-23T19:31:20Z) file for file
  in `src/`, `tests/` and `pyproject.toml`. The date is that upload's UTC day (rule 7).
- **Not 1.3.3.** PyPI's newest release, 1.3.3 (wheel 2026-10-21T18:29:02Z, sdist 18:29:04Z), was
  built from `59142c7`
  ("new module with HAPI-style returns", 2026-10-21T18:26:20Z), the one commit on the branch
  `48-hapi`, which is the only place 1.3.3 is declared; its sdist matches that commit file for file.
  The branch is a feature branch, not a release branch: it is named for the open issue #48 ("convert
  CC to HAPI format"), follows the project's issue-numbered branch convention (`5-test_cascade`,
  `21-err2warn` and `45-wildcards` were each merged into `develop` by pull request), has no pull
  request, and is one commit ahead of `develop`. A PyPI file built from code on neither the default
  branch's lineage nor a release branch is unreleased code for this field (rule 2). No 1.3.2 was
  declared or uploaded. **For a later update:** record the newest PyPI version declared at a
  `develop` commit; when the HAPI-style module reaches `develop`, check Fields 4, 8, 17, 29 and 30
  against it.
- **Not 1.3.0.** The source tree of the 1.3.0 sdist (wheel 2026-09-21T17:02:39Z, sdist 17:02:41Z)
  matches `762e019`, the merge of PR #44 three minutes earlier, apart from an extra `_hapitime.py`,
  and no commit declares its version string; `fe916cb` sets 1.3.1 about 42 minutes later. 1.3.1
  supersedes it in any case.
- **Version Description empty.** Rule 10 derives a new release's description afresh, and rules
  13–16 take it only from a GitHub release title or body or a changelog entry, of which CloudCatalog
  has none. The pull-request descriptions in the range (PR #44 explains the switch from raised errors
  to logged `None` results) are not release notes, and a summary composed from them or from commit
  subjects is never recorded (rule 15).
- **Version PID:** no per-version DOI exists (see Field 2).
- **Declared but never released, settled.** `develop` declared 1.2.2 (`a50a73f`, 2026-03-31) and then
  1.2.3 (`a3ab434`, 2026-07-07); neither was uploaded, tagged or released. Automated metadata
  extractors reported 1.2.3 with high confidence; that was the trap. `origin/main` still declares the
  malformed `1.1.01` at `db81e17` (2026-03-31), behind `develop`. The 1.2.1 release was itself never
  declared in any commit (the sequence runs 1.1.0 `9d74d3c` → 1.1.01 `594947d` → 1.2.2 `a50a73f`):
  its wheel and sdist were uploaded at 2026-03-31T11:35:19Z and 11:35:20Z from an uncommitted edit,
  about four hours fifty minutes before `a50a73f` bumped `develop` to 1.2.2 (2026-03-31T16:25:33Z),
  the same shape 1.3.0 shows.

**Previous values.** Before 1.3.1, HSSI held version 1.2.1 (2026-03-31) with a description
summarising the 32 non-merge commits `9d74d3c..db81e17`. That summary was composed from commit
subjects, which Field 12 never records (rule 15), and it is not carried onto 1.3.1 (rule 10). Before
1.2.1 the record held 1.1.0 dated 2025-09-04, a date PyPI contradicts: 1.1.0 was published
2025-06-02.

---

### 13. Programming Language (RECOMMENDED)
- Python 3.x

GitHub reports Python only; `requires-python = ">=3.9"`; the CI matrix pins
`python-version: ["3.11"]`.

---

### 14. Reference Publication (OPTIONAL)
https://doi.org/10.5281/zenodo.17398630

"CloudCatalog: an API plus Tools for Lazy Indexing of Millions of Cloud-Stored Data Files",
Alex Antunes (ORCID 0000-0002-3098-2602, JHUAPL), DASH 2025, published 2025-10-20, CC-BY-4.0.
It is the publication *describing this software*:

- the first paragraph of its two-paragraph abstract is, up to whitespace, the current `README.md`
  lead paragraph; the second, on reaching HelioCloud's holdings with CloudCatalog and on performance
  and extensibility, is not in the README;
- its Zenodo custom metadata declares
  `code:codeRepository = https://github.com/heliocloud-data/cloudcatalog`,
  `code:programmingLanguage = [Python, JSON]` and `code:developmentStatus = active` — the author
  explicitly bound the record to this repository.

The authors never designated a preferred citation: there is no `CITATION.cff` and no "how to cite"
section, so this assignment rests on authorship plus content rather than on a stated preference.

**A poster as the Reference Publication, settled.** The record is a conference poster, a form Field 14
rule 2 ordinarily sends to Field 27. It is kept here deliberately: no paper describing CloudCatalog
has been found (the ADS/SciX, Zenodo and DataCite searches recorded in Field 27), and this poster is
the only publication with a DOI whose subject is the software, written by its lead author, opening
with the README's lead paragraph and bound by its metadata to this repository. Keeping it is not an open
question. Revisit Field 14 only if a paper describing the software appears, and then move this poster
to Field 27.

Concept DOI (all versions): https://doi.org/10.5281/zenodo.17398629. Recorded as context; the
versioned record DOI above is the citable one.

---

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

`LICENSE.MD` — "The MIT License (MIT) / Copyright © 2023 The Johns Hopkins University Applied
Physics Laboratory LLC"; `pyproject.toml` `license = {text = "MIT License"}`; PyPI classifier
`License :: OSI Approved :: MIT License`; GitHub reports `license.spdx_id = MIT`.

---
## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- api
- aws
- catalogs
- cloud
- cloud computing
- csv
- data access
- data management
- data retrieval
- heliophysics
- indexing
- json
- metadata
- open science
- pyhc package
- python
- s3
- serverless

Sources: `pyproject.toml` `keywords = ["cloud","index","catalog","AWS"]`; PyHC registry
`keywords: ["data_retrieval","general","csv","remote","data_access"]`; the Zenodo DASH 2025 record
`keywords: ["heliophysics","cloud computing"]`; and `README.md` ("The push to open science…",
"RESTful & serverless", S3 buckets throughout).

**Deliberate deviation:** `pyproject` says `index`; this record uses **`indexing`**. A bare `index`
keyword would sit among the existing geomagnetic-index keywords (`ae index`, `dst index`,
`kp index`, `geomagnetic index`) and read as an entirely different concept.

Dropped as low-value or ambiguous: `general`, `remote`, `fair`, `big data`, `specification`.

**`pyhc package`** is the PyHC package marker, which Field 16 rule 15 requires on every package listed
in the PyHC registry; CloudCatalog's entry is in `_data/projects.yml`. It binds the existing
`pyhc package` keyword row.

The sources above are those of release 1.3.1 (`a3c2509`), read 2026-10-28; on that date the
repository had no GitHub topics.

---

### 17. Data Sources (OPTIONAL)
- S3/Cloud-aware
- HTTP/HTTPS Directories

- **S3/Cloud-aware** — `fetch_S3()` / `fetch_S3_n_lines()` in `src/cloudcatalog/main.py` use
  `boto3` S3 clients (anonymous/`UNSIGNED`, signed, and region-pinned variants, with ranged
  `GET`s); the whole specification is built on `s3://` bucket endpoints
  (`docs/cloudcatalog-spec.md` sections 2–3); `boto3` is a declared runtime dependency.
- **HTTP/HTTPS Directories** — `fetch_url()` + `s3url_to_https()` provide an HTTPS fallback;
  `CatalogRegistry` fetches `http://heliocloud.org/catalog/HelioDataRegistry.json` over HTTP;
  the specification says a catalog `index` entry
  `MUST start with s3:// or "https://" (or equivalent) end in a terminating '/'.`
  (`docs/cloudcatalog-spec.md` section 3);
  `docs/CloudCatalog-Demo.ipynb` — "works for AWS S3 or conventional hosting (HTTP or HTTPS
  URLs)"; `validators/validate_cloudcatalog_api.py` (renamed `validate_apiheliocloud.py` by PR #43)
  queries `https://api.heliocloud.org/...`.

At `a3c2509` (release 1.3.1) the fetch cascade in `main.py`, which PR #44 restructured to return
`None` instead of raising, reaches the same S3 (unsigned, signed, region-pinned), HTTP(S) and
local-file sources.

**Considered and excluded:**
- `CDAWeb` — the repository's CDAWeb references (`generators/find_in_catalog.py`,
  `validators/find_collection.py`) filter CloudCatalog's *own* `collections` tag for the string
  "CDAWeb"; the mirrored CDAWeb data is reached as ordinary S3 objects, never through CDAWeb's
  services.
- `HAPI` — the package is only "HAPI-like" in query shape and borrows HAPI's time format
  (spec section 5). `tests/test_hapi.py` is an explicit stub whose converter body is commented out
  and whose `CloudCatalogToHAPIConverter` returns its input unchanged. No HAPI client exists.
- `Observatory/Mission-specific` — the software is dataset- and mission-agnostic (Fields 31–32).

---

### 18. Input File Formats (RECOMMENDED)
- csv
- JSON

- **csv** — index files `[index]/[id]_[YYYY].csv` read with `pd.read_csv()`
  (`request_cloud_catalog()`, `sample_file()`); `update_catalog_from_csv()` reads `cat.csv`.
- **JSON** — `catalog.json`, the global `HelioDataRegistry.json`, `catalog_stub.json` and the
  optional `<id>.info` metadata file.

**Not claimed:** `csv-zip` and `parquet` appear in the *specification* (section 4) but the client
hard-codes `ndxformat = "csv"` in `main.py`, so they are not implemented. `FITS`, `CDF`, `netCDF`
and `HDF5` are the formats of the *indexed data files*, which the package streams as opaque bytes
(`stream()` hands a `BytesIO` to a user callback) and never parses — they belong to the user's
downstream reader, not to this package.

---

### 19. Output File Formats (RECOMMENDED)
- csv
- JSON
- Other

- **csv** — `updater/recatalog.py` `update_index()` rewrites the `[id]_[YYYY].csv` index files when
  holdings are relocated, and `cloudspider.spider(create_manifest=True)` writes `manifest_spider.txt`
  via `DataFrame.to_csv()` (both read at `a3c2509`). The `cloudcatalog-manifest2indices` converter,
  which wrote `[dataID]_[YYYY].csv` indices in 1.2.1, is absent from 1.3.1 (Field 8) and is not part of
  this evidence.
- **JSON** — `update_catalog_from_json()` / `update_catalog_from_csv()` write `catalog.json`
  (`json.dump(..., indent=4)`); `generators/catalog_editor.write_catalog()` does the same under a
  file lock; `CloudCatalog(cache=True)` writes a cached `catalog.json`.
- **Other** — `generators/cloudcat_indexer.write_indexes()` generates per-dataset
  `[id]_index.html` pages; HTML is not in the format vocabulary, which is what `Other` covers.
  Not claimed: the plain-text `spiderout.txt` report, which is a log rather than a data file.

---

### 20. Operating System (RECOMMENDED)
- Operating System Independent

Pure Python with no compiled extensions, no OS-specific code paths and no platform markers in
`pyproject.toml`; the dependencies (`boto3`, `pandas`, `requests`, `smart_open`, `jsonschema`,
`aiohttp`) are all cross-platform. Note that `OS Independent` is **not** a valid value; the exact
value is `Operating System Independent`.

**Considered and excluded:** the explicit `Linux` / `Mac` / `Windows` triple. CI exercises
`ubuntu-latest` only, so Linux is the only *tested* platform, but the recorded value describes the
software's actual portability rather than its CI coverage.

---

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Pure Python, no architecture-specific code, and PyPI ships `py3-none-any` wheels.

---

### 22. Related Phenomena (OPTIONAL)
Not found

Deliberately empty. The package is phenomenon-agnostic: it indexes and retrieves *files*, and
supports no phenomenon specifically. **`Solar Corona` was considered and rejected** for the same
reason `Corona` was rejected in Field 5 — the supporting evidence is coronal test fixtures, the
identical evidence class rejected in Fields 31–32.

---

### 23. Development Status (RECOMMENDED)
Active

- `pyproject.toml` classifier `Development Status :: 4 - Beta` — a packaging maturity label, which
  corroborates that releases exist and nothing more.
- The Zenodo DASH 2025 record's custom field `code:developmentStatus = {"id": "active"}` — the
  author's own declaration.
- Dated anchors (read 2026-10-28): the last commit on the default branch `develop` is `a3c2509`,
  2026-09-23T19:31:20Z, less than six months before that reading, so rule 6 gives `Active`; the
  newest release is 1.3.1 of 2026-09-23 (Field 12), followed by a PyPI upload from a feature branch
  on 2026-10-21; the repository is not archived and has 19 open issues.
- In production: "already used for 2 Petabytes of publicly available NASA and
  scientist-contributed data" (`README.md`).
- Not `WIP` — there are ten published PyPI releases and a stable public API. The "beta, use at
  risk for now" caveat in the README applies only to the generator/updater tools.

---

### 24. Documentation (RECOMMENDED)
https://github.com/heliocloud-data/cloudcatalog

The authors' own declared documentation location — `pyproject.toml`
`[project.urls] Documentation = "https://github.com/heliocloud-data/cloudcatalog"`, also carried on
PyPI. There is no documentation site: `docs/conf.py` and `docs/index.rst` exist (Sphinx,
`project = "cloudcatalog"`, title "cloudcatalog Documentation") but there is no `.readthedocs.yml`,
and `https://cloudcatalog.readthedocs.io/en/latest/` returned 404 on 2026-10-28. The repository
root carries the README with usage and installation guidance, plus `docs/` (specification,
contributing guide, demo notebook, developer notes). There is no wiki either:
`git ls-remote https://github.com/heliocloud-data/cloudcatalog.wiki.git` returned "Repository not
found." on 2026-10-29, although GitHub reports `has_wiki: true`; the same command lists the PySPEDAS
wiki, the positive control.

**Considered and excluded:** the PyHC-curated docs link
`https://github.com/heliocloud-data/cloudcatalog/blob/main/docs/cloudcatalog-spec.md` — reachable,
but it is the specification document alone, with no installation or usage content; and the `docs/`
tree `https://github.com/heliocloud-data/cloudcatalog/tree/develop/docs`, which is branch-pinned
and fragile.

---

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

NASA is recorded as the funder of the project whose product this software is (Field 25 rule 8). The
two links:

1. **The software is HelioCloud's product.** The README says "The CloudCatalog specification and
   tools are open source, created by the HelioCloud project" (`README.md` at `a3c2509`), and
   `docs/CONTRIBUTING.md` is titled "Contributing to HelioCloud and CloudCatalog".
2. **HelioCloud is supported by NASA.** The description of the lead author's DASH 2025 poster record,
   10.5281/zenodo.17419850 ("The Jupyter Cloud Ecosystem for Science: Featuring HelioCloud", Antunes
   and Snow), says "HelioCloud, a NASA-supported initiative, exemplifies this transformation." NASA's
   HDRL Program Review Report (10.5281/zenodo.22131847, Field 27) corroborates it: HDRL's Data
   Integration Services for Heliophysics "also supports the development of the HelioCloud platform".

This is the third clause of rule 8: a statement that supports the platform whose product the software
is (link 2), with a source attesting that the software is that platform's product (link 1). The poster
record does not name CloudCatalog; the README supplies that link. The support statement names no award
(Field 26). The identifier is NASA's ROR, whose display name is the name above.

**Superseded value.** HSSI held no funder until this update. This record previously excluded NASA,
reasoning that institutional origin at NASA/GSFC and a NASA-owned S3 bucket do not establish a funder;
that still holds for those two facts, which are not the basis of the value above.

**Searched for further funders and awards:** the repository at `a3c2509`, with a case-insensitive
sweep of the whole tree for fund, grant, acknowledg, award and 80NSSC (its one match is the word
"granted" in the MIT licence text of `LICENSE.MD`, which also serves as the positive control); the
PyPI metadata; the DataCite `fundingReferences` and Zenodo `grants` of the Field 14, 27 and 28 records
and of 10.5281/zenodo.17419850; and the text of the Field 14 poster abstract and of the Field 27 and
28 records. The repository names no funder; its only funding-adjacent evidence is
`docs/CONTRIBUTING.md` — "HelioCloud originated at NASA/GSFC from the Heliophysics Data Research
Library" — plus the NASA-owned `s3://gov-nasa-hdrl-data1/` bucket.

**Considered and excluded:**
- **NASA award 80NSSC22K0643.** The Field 28 dataset record, 10.5281/zenodo.13972479, ends "Work was
  funded under NASA Heliophysics 21-LWSTM21_2-0018, award number 80NSSC22K0643." USAspending lists
  the award to The Johns Hopkins University (2022-03-01 to 2024-07-31), and its description is the
  creation of the full ML-ready EUV dataset from 1995 to the present, accessible via the cloud. It
  funded the dataset, a work this software serves, not the software: a record that names the
  software counts only through a sentence attributing funding to the software or its producing
  project (rules 4 and 8), and an input's own funding is excluded (rule 5).
- **Heliophysics Science Division** (Crossref Funder ID 10.13039/100020016) — the DataCite
  `fundingReferences` of the Field 27 HDRL Program Review Report, 10.5281/zenodo.22131847: the
  report's own funding, not the software's (rule 4).

---

### 26. Award Title (OPTIONAL)
Not found

No award is attributed to CloudCatalog or to HelioCloud, the project whose product it is (Field 26
rule 8): the statement that HelioCloud is NASA-supported (Field 25) names no award, and the searches
recorded in Field 25 find none. A funder recorded without an award is legitimate (rule 8).

**Considered and excluded:** NASA award 80NSSC22K0643 (to The Johns Hopkins University, 2022-03-01
to 2024-07-31), which funded the EUV-ML dataset of Field 28, a work this software serves, rather
than the software (rule 3; the evidence is in Field 25). The `21-LWSTM21_2-0018` beside it in the
dataset record is not the award number; the record names 80NSSC22K0643 as that.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.5281/zenodo.22131847

**`10.5281/zenodo.22131847` — a third-party report on a service built with the software (rule 5).**
"Heliophysics Digital Resource Library (HDRL) Program Review Report" (Thomas, B. A.; Ireland, J.;
Jian, L.; Candey, R.; Ringuette, R.; Zenodo, 2026-08-27), a technical report (Zenodo and DataCite type
Report); none of its authors is an author of this software. Its section 4.7, "DISH Discoverability
Mechanisms", states that HDRL's Data Integration Services for Heliophysics "supports discoverability
of cloud-based data using the “cloudcatalog” software and standard (Antunes et al. 2025)" and that
"Over 1.2 PB of cloud-hosted science data are currently discoverable using cloudcatalog"; elsewhere it
says that uploaded data "are registered using the cloudcatalog software and are thereby made
discoverable". HDRL's discovery service is built with this software, and the report says so
deliberately, citing the Field 14 record. The software's citing literature is small, so such a use is
still news. *(The report's phrase "Cloudcatalog is built on top of HAPI" is its own loose wording: the
software borrows HAPI's query shape and time format, Fields 17 and 29.)*

**Publication search, 2026-10-28** (a later update searches from this date): Zenodo creator-keyed
searches on all four person-authors by name, and on Alex Antunes by ORCID, plus free-text
`cloudcatalog`; ADS/SciX `full:"cloudcatalog"` (5 records) and `title:"cloudcatalog"`, beside a
nonsense-token control returning 0 and a `full:"pysat"` control returning hits; DataCite
`query=cloudcatalog` (10 DOIs, all weighed in this record); and the DataCite citation counts of the
Field 14 and 28 DOIs and of 10.5281/zenodo.13887203 (all zero). On 2026-10-29, for the AGU 2024
abstract below: Zenodo and DataCite title searches, with the Field 14 poster's title as the positive
control, a Crossref bibliographic search, and a Crossref listing of the records with an author
named Antunes since 2024 under the prefix that ESS Open Archive shares with Authorea (10.22541)
found no deposited poster or paper.

**Considered and excluded:**
- **https://doi.org/10.5281/zenodo.13887203 — a Gateways 2024 demo submission: a demo abstract plus
  two slides.** "HelioCloud as a replicable open science architecture", published 2024-10-03,
  CC-BY-4.0; creators Antunes, Alex; Shumate, Peter; Thomas, Brian; Bradford, Jeffery; Rourke, Sarah;
  Lenzi, Nicholas; Jeschke, Chris; Vandegriff, Jon (three of this software's four person-authors);
  concept DOI 10.5281/zenodo.13887202. Zenodo types it a conference proceeding, but the record's
  description is a demo abstract, which opens "We demo HelioCloud" and names the software once: "By
  separating our open source releases as platform, heliophysics-specific container, CloudCatalog
  indexing standard, and tutorials…". Its one file, `Gateways2024_paper_31.pdf`, is a deck of two
  slides exported from LibreOffice Impress: "HelioCloud Overview" (bullets on the shared open
  architecture, a diagram of the network of instances, screenshots of the user portal and the
  notebook environment) and "Example: 2TB of SDO EUV data" (an irradiance plot, a 27-hour laptop run
  against 25 minutes on HelioCloud, and a note that an instance will be stood up for a hands-on demo).
  CloudCatalog is named only in the abstract, not on the slides. A meeting abstract is never an
  eligible publication, and the deck was judged to fail the standalone test for slide decks: a deck of
  headings and images that a reader cannot follow without the demo (rules 1 and 7). HSSI listed it
  in this field until this update.
- **https://ui.adsabs.harvard.edu/abs/2024AGUFMIN13B2159A/abstract — the lead author's AGU 2024
  meeting abstract.** Antunes, A. K. and Thomas, B. A., "Enabling Better Cloud Dataset Sharing with
  CloudCatalog", AGU Fall Meeting 2024, abstract IN13B-2159 (December 2024). Its whole subject is this
  software: the indexing specification, the top-level `catalog.json` metadata file, the time-ordered
  CSV indices of the form "start, stop, datakey, filesize", and the "Python HAPI-like API to search on
  dataset IDs over timeranges". A meeting abstract is never an eligible publication (rule 1), and no
  deposit of the presentation it announces was found (searches above); add that deposit here if one
  appears.
- 10.5281/zenodo.17398940 ("Contributing to the HelioCloud Open Science Cloud Computing
  Community", DASH 2025) — about HelioCloud community governance, with no substantive CloudCatalog
  content.
- 10.5281/zenodo.18749496 ("HDRL Show and Tell: Current Infrastructure", 2026-02-23) — a 47-page
  deck by twelve creators, among them "Antunes, Sandy", surveying HDRL's current infrastructure in
  turn. Antunes's part, introduced by the agenda line "Sandy Antunes: HelioCloud development and the
  CloudCatalog", covers HelioCloud: a slide titled "HelioCloud: Development & the CloudCatalog" on the
  HelioCloud project, and a tools slide whose CloudCatalog item describes it as "a RESTful endpoint
  for cloud-stored data", with a current and a future note. Its subject is HDRL's infrastructure
  as a whole, not this software or the platform it serves, so rule 3 does not admit it.
- 10.5281/zenodo.17398630 — used as the Reference Publication (Field 14) rather than duplicated
  here.
- https://doi.org/10.48550/arXiv.2607.06650 ("HDRL Staff Strategy Meeting Report", Thomas et al.,
  July 2026) — its only CloudCatalog content is the agenda line "Sandy Antunes: HelioCloud development
  and the CloudCatalog"; a mention (rule 6).
- 10.5281/zenodo.23069202 ("Getting Scientists On Board with Cloud Portals", Antunes et al., DASH
  2026) — about JupyterHub cloud portals and training scientists to use them; its only CloudCatalog
  content is a list item naming `sunpy_cloudcatalog` among cloud integrations, the source of the
  Field 30 sunpy-cloudcatalog entry. A talk about the compute portal rather than the data registry
  this software serves, in the same class as 10.5281/zenodo.17398940.
- Earlier HelioCloud-team deposits by this software's authors: 10.5281/zenodo.14918634 (Shumate, IHDEA
  2025, "HelioCloud: Collaborative Computing and Cost Management via Commercial Cloud"), whose only
  CloudCatalog content is one slide sentence calling it HelioCloud's library for sharing datasets
  across HelioCloud instances, a mention (rule 6); and 10.5281/zenodo.17123082 (a HelioCloud overview
  talk at TESS 2022, before this repository's first commit), 10.5281/zenodo.13887300 (Gateways 2024, a
  two-page conference paper on spinning up short-term platforms for workshops) and
  10.5281/zenodo.17419850 (DASH 2025, the Jupyter cloud ecosystem), none of which names CloudCatalog
  in its metadata or in the text extractable from its file (the 17419850 PDF has no extractable text;
  its description is the Field 25 source for NASA's support of HelioCloud).
- https://doi.org/10.1109/JSTARS.2020.3023901 (ADS 2020IJSTA..13.6008V, a 2020 Google Earth Engine
  wetland-classification article) — the fifth ADS full-text hit, published three years before this
  repository's first commit (2023-09-13) and its adoption of the name `cloudcatalog` (2023-10-18), so
  the hit cannot refer to this software.
- The other 2026 deposits by HelioCloud-team members that include this software's authors, none of
  which names CloudCatalog in its metadata or in the text extractable from its slides or poster:
  10.5281/zenodo.23086560 and 10.5281/zenodo.23087324 ("The Hassles of Managing Big Data", data
  ingestion with AWS Lambda), 10.5281/zenodo.23086708 and 10.5281/zenodo.23086960 (cloud security),
  10.5281/zenodo.23024146 (cost monitoring), 10.5281/zenodo.23186292 (deploying a HelioCloud),
  10.5281/zenodo.23211648 (Jupyter AI in HelioCloud), and 10.5281/zenodo.21793481 and
  10.5281/zenodo.23144432 (HAPI).

---

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.5281/zenodo.13972479

"EUV-ML solar physics dataset from STEREO + SOHO, 2 solar cycles" (Antunes, Vievering, Linko;
2024-10-22). Evidence on **both** sides:

- the dataset record itself states the data is served from
  `s3://gov-nasa-hdrl-data1/contrib/euvml/` with "a sample Python Jupyter Notebook … for accessing
  them via the **'cloudcatalog' Python client**";
- this repository tests directly against it — `tests/test_hdrl.py::test_hdrl_euv` requests dataset
  id `euvml_stereoa_171`, and `test_search` asserts `search_by_id("EUVML_STEREO")` returns 10
  entries.

Concept DOI: 10.5281/zenodo.13972478. Other holdings referenced in the repository (SDO/AIA, MMS,
CDAWeb mirrors, PSP/WISPR) have no dataset DOI cited anywhere and are not listed.

---

### 29. Related Software (OPTIONAL)
- https://github.com/heliocloud-data/platform
- https://github.com/heliocloud-data/heliocloud_tools
- https://github.com/hapi-server/data-specification

Each entry is distinguishing, with a specific artifact cited:

1. **HelioCloud platform** — the parent project this software was extracted from and is deployed
   as part of. `docs/CONTRIBUTING.md` is titled "Contributing to HelioCloud and CloudCatalog";
   `docs/cloudcatalog-spec.md` section 1: "Adopted by HelioCloud, this specification creates a
   global data registry … maintained at the HDRL HelioCloud.org website"; git history shows the
   code was moved out of the platform repository — commits `019fa8a` / `5c1ef04`, "Moving over
   files from platform/tools that belong to scregistry".
2. **heliocloud_tools** — the companion repository to which the CloudCatalog web service and
   operations tooling were moved out of this one: commits `19ecbdd` ("moved cloudcatalog web service to
   heliocloud_tools instead"), `d2c926a` and `dc03e16` ("Moved ops tools to heliocloud_tools repo",
   the latter continuing ", also pulling PyHC Actions for now") and `89a5127` ("moved ops tools to
   heliocloud_tools, nerfed PyHC cicd for now"). The service it hosts is the one exercised by
   `validators/validate_cloudcatalog_api.py` (renamed `validate_apiheliocloud.py` by PR #43) at
   `https://api.heliocloud.org/cloudcatalog?id=`.
3. **HAPI data specification** — the similar-purpose standard CloudCatalog explicitly models
   itself on and borrows from. `README.md`: enabling "HAPI-like" data ID + time range queries;
   `docs/CloudCatalog-Demo.ipynb`: "like HAPI, it is both a specification and an accompanying
   Python API"; `docs/cloudcatalog-spec.md` section 5: "the SCR Time format (**taken from the HAPI
   Time format**) is a subset of the ISO 8601 standard". The specification's concept DOI,
   10.5281/zenodo.4757596 (the badge in its repository's README; DataCite lists it with `HasVersion`
   relations), is passed over for the repository URL because the site shows the raw URL as link text
   (rule 13).

**Considered and excluded:**
- https://github.com/heliocloud-data/sunpy-cloudcatalog — recorded in Field 30 only. Its relation to
  this software is the plug-in exchange itself, which belongs in Field 30 alone (rule 3).
- `hapiclient` — release 1.3.1 ships `_hapitime.txt`, a text file reproducing hapiclient's `hapitime`
  functions (its own imports and examples name `hapiclient`); as a `.txt` file it cannot be imported,
  and nothing in the package uses it. The HAPI-style returns of the unreleased `48-hapi` branch
  (Field 12) do not use it either. Functionality planned but not shipped is not a relation (rule 7).
  The HAPI specification itself is entry 3.

---

### 30. Interoperable Software (OPTIONAL)
- https://github.com/lasp/cdflib
- https://github.com/heliocloud-data/sunpy-cloudcatalog

**Canonical URL.** cdflib's repository moved from `MAVENSDC/cdflib` to `lasp/cdflib`:
`https://github.com/MAVENSDC/cdflib` returns HTTP 301 redirecting to
`https://github.com/lasp/cdflib`, and cdflib's PyPI metadata declares
`Homepage: https://github.com/lasp/cdflib` as its only project URL. The current canonical location
is recorded; a redirecting URL is deliberately not used. cdflib's concept DOI,
10.5281/zenodo.1481144 (DataCite `HasVersion`), is passed over for the repository URL because the
site shows the raw URL as link text (Field 29 rule 13).

**cdflib** is admitted on a concrete demonstrated exchange: the shipped demo notebook
`docs/CloudCatalog-Demo.ipynb` defines `plot_cdf(s3_uri, d, e, f)` whose body is
`cdf = cdflib.CDF(s3_uri)` then `plt.plot(cdf.varget(1))`, and drives it with
`fr.stream_uri(file_registry1[:3], lambda s3_uri, d, e, f: plot_cdf(s3_uri, d, e, f))`
(cells 41 and 43). The package's documented output — the S3 URIs emitted by `stream_uri()` — is
consumed directly by cdflib in the project's own worked example.

**sunpy-cloudcatalog** is a plug-in written against this package (rule 7, with the evidence on the
partner's side). Its repository, `heliocloud-data/sunpy-cloudcatalog` (`main` at `f5c6416`,
2026-02-17; PyPI `sunpy-cloudcatalog` 1.0.1, which requires `cloudcatalog` and `sunpy`), implements
`CloudCatalogClient`, a SunPy `BaseClient` whose `search()` calls
`cloudcatalog.CloudCatalog(q.bucket).request_cloud_catalog(...)`, so that CloudCatalog holdings are
searchable through `sunpy.net.Fido`, with `Fido.fetch()` writing CSV file manifests; its README
presents it as a SunPy-affiliated Fido client for CloudCatalog. The developers name it in their DASH
2026 talk (10.5281/zenodo.23069202: "integration with Fido, sunpy_cloudcatalog"). It had no HSSI entry
on 2026-10-28, so the entry is its repository root (Field 29 rule 12); if it gains an entry, use that
entry's stored `code_repository_url` (rule 11).

**Considered and excluded:**
- `pandas` — not listed even though the public API returns `DataFrame`s. Being a dependency is not
  interoperability.
- `boto3` / `botocore`, `requests`, `smart_open`, `python-dateutil`, `jsonschema`, `aiohttp`,
  `filelock`, `matplotlib`, `pytest` — generic infrastructure (cloud SDK, HTTP, I/O plumbing,
  schema validation, plotting, testing); each would be equally at home in a web app or a finance
  model.
- `astropy` — imported in `docs/CloudCatalog-Demo.ipynb` cell 1 (`import astropy.io.fits`) but
  never used in any cell. An unused import is not a demonstrated exchange.
- `SunPy` — the Fido exchange is performed by sunpy-cloudcatalog, not by this package, which never
  imports sunpy; listing SunPy would infer a pairing through a third package (rule 5).
- `PySPEDAS` and a HAPI client — explicitly future work, not implemented.
  `docs/CloudCatalog-Demo.ipynb` lists "add hooks to PySpedas & HAPI?" among future items and
  states: "Future: We'd love to work hook for CloudCatalog calls into other packages (esp.
  PySpedas and HAPI) so the cloud-stored data is fetchable within user's preferred toolsets."
  `tests/test_hapi.py` is a stub with its converter body commented out. Release 1.3.1's
  `ls_wildcard()` is called a "pyspedas-like wildcard routine" in its commit message, an idiom with no
  PySPEDAS import or exchange. The HAPI-style returns exist only on the unreleased `48-hapi` branch
  (Field 12); re-check a HAPI exchange when that branch reaches `develop`.
- `AWS Athena` — genuinely documented as a query path over the CSV indices
  (`docs/cloudcatalog-spec.md` sections 4.4 and 4.5), but it is a proprietary managed service with
  no repository or DOI to link, and it queries the index files rather than interoperating with the
  package.

---

### 31. Related Instruments (OPTIONAL)
Not found — deliberately empty

CloudCatalog is instrument-agnostic by design: it indexes and retrieves *files* for arbitrary
datasets and implements no instrument-specific parser, format, calibration or convention. It never
opens a science file — `stream()` hands raw bytes to a user callback and `stream_uri()` hands over
URIs. Every instrument name in the repository is a test fixture or tutorial example, so no
candidate is relevant enough to record:

| Mentioned | Where | Why omitted |
|---|---|---|
| SDO/AIA (`aia_0094`) | `README.md` "Specific example for an SDO fetch…", `tests/test_hdrl.py::test_hdrl_aia`, demo notebook | Example dataset id used to exercise a generic client. |
| MMS/FEEPS, MMS/ASPOC, MMS/MEC | `README.md` "Add-on example for an MMS fetch", `tests/test_mms.py`, `tests/test_hdrl.py`, `tests/test_hapi.py`, `docs/demo.py` | Integration-test fixtures against the HDRL bucket. |
| STEREO/EUVI, SOHO/EIT (`euvml_stereoa_171`) | `tests/test_hdrl.py::test_hdrl_euv`, spec section 4.6 CSV examples | Example dataset; captured instead via the EUV-ML dataset DOI in Field 28. |
| PSP/WISPR | `tests/test_reverse_lookup.py` | Example dataset id for a path-based reverse lookup. |
| LANL `A1_K0_MPA` | `tests/test_reverse_lookup.py` | Example of a CDAWeb-mirrored id. |

A user searching for `instrument:"AIA"` would not want a generic cloud file-index client, and
nobody working with AIA data reaches for this package to *read* AIA data. Related concerns are
routed to their proper fields: the multi-mission `s3://gov-nasa-hdrl-data1/` archive → Field 17
(`S3/Cloud-aware`), and the generic FITS/CDF formats of the indexed files → not claimed in
Fields 18–19 (see Field 18).

---

### 32. Related Observatories (OPTIONAL)
Not found — deliberately empty

The same reasoning as Field 31, applied to missions and observatories (SDO, MMS, STEREO, SOHO,
Parker Solar Probe): the software is mission-agnostic and supports none of them specifically — it
supports *whatever* a data owner chooses to index. `gov-nasa-hdrl-data1` is a generic multi-mission
archive, which the Field 32 guidance routes to Data Sources rather than to an observatory
association.

---

### 33. Logo (OPTIONAL)
Not found

No image is presented as CloudCatalog's logo in the repository at `a3c2509`: `docs/conf.py` sets no
`html_logo`, the README has no header image, and the only image file in the tree is
`docs/scr_logo.png` (below).

**The PyHC registry logo.** The PyHC registry entry (`_data/projects.yml`) presents
`logo: https://heliocloud.org/static/img/logo.jpg`, which is presentation evidence under Field 33
rule 2, but that URL returned 404 on 2026-10-28, and rule 10 never records a URL that does not return
an image. The Wayback Machine holds ten captures of it, from 2024-07-27 to 2025-11-22, all with one
content digest, such as
`http://web.archive.org/web/20251121131750/https://heliocloud.org/static/img/logo.jpg`: a JPEG of
8712×4643 pixels showing the HelioCloud sun-and-orbit emblem with the name set in grey italic across
it. `https://heliocloud.org/logo.png`, which served an image on 2026-10-29 (`image/png`, 1186×367), is
different artwork, the emblem beside the name in red bold type. It is the parent project's mark,
which the project does not present as this software's logo (rule 5), and it is not the registry's
image, so it does not stand in for that one (rule 10). A later update should revisit this field under
rule 2 if the registry's image is found at a live URL, or if the registry entry presents another
image.

**Also not usable: `docs/scr_logo.png`.** It is the retired "SHARED CLOUD REGISTRY" mark from before
the 2023 rename, and nothing in the repository references it, so the project does not present it as
a logo (rule 4).

---

## Software name evidence (Field 7)

The software's name is **`CloudCatalog`**. This record previously held `CloudCatalog API`, which no
source supports.

1. **PyHC community registry** (`heliophysicsPy.github.io/_data/projects.yml`, entry at line 131 on 2026-10-28)
   records `name: "CloudCatalog"`, `code: https://github.com/heliocloud-data/cloudcatalog/`.
   PyHC is a manually curated registry and the highest-priority naming source. It is unambiguous.
2. **The lead author's own publication title** — Zenodo 10.5281/zenodo.17398630,
   *"**CloudCatalog**: an API plus Tools for Lazy Indexing of Millions of Cloud-Stored Data
   Files"* (Alex Antunes, DASH 2025), whose metadata sets `code:codeRepository` to this
   repository. The author separates the proper noun (`CloudCatalog`) from the descriptor ("an API
   plus Tools") — and "plus Tools" shows the software is *not* only an API.
3. **Repository, distribution and import name** is `cloudcatalog` in every channel: the GitHub
   repository name, the PyPI distribution (`pypi.org/project/cloudcatalog`,
   `info.name = cloudcatalog`), `pyproject.toml` `name = "cloudcatalog"`, the import
   (`import cloudcatalog`), and the Sphinx project (`docs/conf.py` `project = "cloudcatalog"`,
   `docs/index.rst` "cloudcatalog Documentation").
4. **GitHub About**: "**CloudCatalog** specification and API for providing and accessing cloud
   data" — again the name followed by a descriptor.
5. **The specification's own title** is its section 1 heading, "The generalized Cloud Catalog
   specification for large cloud datasets" (`docs/cloudcatalog-spec.md`); its prose writes the name
   `CloudCatalog`, and the primary API class is `class CloudCatalog`.
6. **The string `CloudCatalog API` occurs zero times in the repository** — verified
   case-sensitively and case-insensitively across the working tree and across *every commit on
   every branch* (`git grep -i "cloudcatalog api" $(git rev-list --all)` returns no matches).
7. **The project deliberately standardised on this name.** Commit `f2fb4fa` (2023-10-18) renamed
   `scregistry` → `cloudcatalog` and `FileRegistry`/`CloudMe` → `CloudCatalog`; commit `11a7cfa`
   (2024-09-04) is titled "fixed inconsisent naming of CloudCatalog in docs. Added .coveragerc
   file." Naming consistency was an explicit maintainer goal.
8. **No disambiguation need.** No other catalogued software is named `CloudCatalog`, so an "API"
   suffix would distinguish nothing.

**The counter-argument, and why it does not survive.** The case for keeping "API" rests on one
string — the `README.md` H1, `# CloudCatalog (cloudcatalog) API` — plus the `pyproject`
description, "API for accessing the generalized CloudCatalog (cloudcatalog) specification". The
suggested reading is that "API" deliberately distinguishes the *software* (this Python API) from
the *specification* (a document). Three things defeat it:

- **It mis-scopes the record.** The Code Repository for this entry is the whole repository, which
  contains the specification documents (`docs/cloudcatalog-spec.md`, `-1.1.md`, and four earlier
  versions), the client API, generator/updater tools, validators and six console scripts. Naming
  the record "CloudCatalog API" names one component of what is catalogued. The author's own title
  makes the same point: "an API **plus Tools**".
- **Even the README H1 parses the other way.** `CloudCatalog (cloudcatalog) API` reads as
  *proper noun* + *(import name)* + *common-noun descriptor*, exactly as the GitHub About line
  does. Nowhere is "CloudCatalog API" used as a unit — hence the zero-hit search.
- **The descriptor is already where it belongs.** "API for accessing the generalized CloudCatalog
  (cloudcatalog) specification…" is the second line of the description and stays there. Nothing is
  lost by removing "API" from the name; the software/specification distinction is stated more
  precisely in prose than a two-word title could manage.
