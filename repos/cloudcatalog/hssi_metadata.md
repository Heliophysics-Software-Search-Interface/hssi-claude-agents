# HSSI Metadata — CloudCatalog

**HSSI Software ID:** a7f6fd15-9b3c-4cae-a029-0da92222f465
**Repository:** https://github.com/heliocloud-data/cloudcatalog
**Source Revision:** 1c7b8dbbd150b6148ee683484c69d46e5b44f76d (branch `develop`, 2026-07-21)
**Metadata Date:** 2026-07-31
**Validation Date:** 2026-07-31
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [supplied at submission time]
- **Submitter Email:** [supplied at submission time]

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

### 4. Software Functionality (MANDATORY)
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
| ...: Data Access and Retrieval | `CatalogRegistry`, `CloudCatalog.request_cloud_catalog()`, `get_entry()`, `sample_file()`, `stream()`, `stream_uri()`, `EntireCatalogSearch.search_by_id/title/keywords()` in `src/cloudcatalog/main.py`. |
| ...: File Format Conversion | `update_catalog_from_csv()` ingests `cat.csv` and writes `catalog.json` (`src/cloudcatalog/updater/catalog_updater.py`); `cloudcat_indexer.write_indexes()` converts `catalog.json` into per-id HTML index pages (`src/cloudcatalog/generators/cloudcat_indexer.py`). Both present at the source revision. *(A third converter, `cloudcatalog-manifest2indices`, ships in the released 1.2.1 package but was removed from this repository by the source-revision merge itself — PR #39, "Moved ops tools to heliocloud_tools repo", deleted `generators/manifest2indices.py`. `pyproject.toml:50` still declares the now-dangling console script. Not relied on as evidence here.)* |
| ...: Processing | Index post-processing in `request_cloud_catalog()`: spec-version-dependent fixups (synthesises a `stop` column for pre-0.5 indices), `#`-prefixed header stripping, positional column normalisation, multi-year frame concatenation, ISO-8601 parsing and time-range filtering; `validate_and_fix_timestamp()` repairs malformed timestamps. |
| Servers and Environments | Parent category of the two subcategories below. |
| ...: Distribution/Access | The package *is* the access layer for a decentralised, serverless data-distribution standard: "RESTful & serverless (indices are flat files alongside their datasets)" (`README.md`); `docs/cloudcatalog-spec.md` section 2 defines the global `HelioDataRegistry.json` bucket registry; `src/cloudcatalog/validators/validate_cloudcatalog_api.py` exercises the public service endpoint `https://api.heliocloud.org/cloudcatalog?id=`. |
| ...: Data servers processing and handling | Server-side catalog maintenance tooling: `updater/catalog_updater.py` (safe merge/update of `catalog.json`), `updater/recatalog.py` (bulk relocation of holdings, rewriting both `catalog.json` and every index CSV, with backups), `updater/version_file.py` (versioned backups), `validators/validation.py` (`Validator` — JSON-Schema validation of global/local catalogs, ID-uniqueness checks, index-file reachability), `validators/validator.py` (spec compliance of new entries). |

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

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere
- Interplanetary Space
- Planetary Magnetospheres
- Solar Environment

None of these five is wrong for a general heliophysics data-indexing tool.

**`Corona` was considered and rejected.** The only evidence for it is that the datasets the client
is *tested against* happen to be coronal EUV imaging — `aia_0094` (SDO/AIA 94 Å, `README.md`),
`euvml_stereoa_171` (STEREO EUVI 171 Å, `tests/test_hdrl.py::test_hdrl_euv`),
`PARKERSOLARPROBE_WISPR_FITS_LEVEL2_PT30M` (`tests/test_reverse_lookup.py`). That is the **same
evidence class rejected in Fields 31–32**, where every instrument and observatory name in the
repository is a test fixture or tutorial example; admitting `Corona` on test-fixture evidence while
refusing SDO/AIA on identical evidence would be internally inconsistent. Two further reasons:
`Solar Environment` is already present and is the coarser solar region that subsumes the corona;
and CloudCatalog indexes files for whatever region a data owner chooses to publish, so no specific
region is distinguishing.

**Also considered and not added:** `Solar Wind`, `Photosphere`, `Earth Magnetotail`,
`Earth Inner Magnetosphere` — each supportable only by inferring instrument coverage from example
dataset IDs.

---

### 6. Authors (MANDATORY)

Author order is significant and is: Antunes, Jeschke, Shumate, Knowles.

**1. Alex Antunes**
- Author Identifier: https://orcid.org/0000-0002-3098-2602
- Affiliation: Johns Hopkins University Applied Physics Laboratory — https://ror.org/029pp9z10
- Evidence: ORCID 0000-0002-3098-2602 resolves to "Alex Antunes", employment
  "Johns Hopkins University Applied Physics Laboratory" (ROR `029pp9z10`), dept SES/SRN.
  Commits as `Sandy Antunes <sandy.antunes@jhuapl.edu>` (72 commits) and `antunak1` (30);
  named contact in the PyHC registry and in `docs/CloudCatalog-Demo.ipynb`.

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
- **Completed correction:** this record previously held the misspelling **`Schumate`** with no
  identifier. Corrected to `Shumate` with the ORCID above, preserving the author's existing
  identity and position in the author order. The ORCID for Jeschke was added in the same
  correction, also to a pre-existing identity that carried none.

**4. Lisa Knowles**
- Author Identifier: Not found
- Affiliation: Johns Hopkins University Applied Physics Laboratory — https://ror.org/029pp9z10
- Evidence: primary author of `src/cloudcatalog/validators/validator.py`
  (`git blame`: 201 of 305 current lines), whose module docstring reads
  *"Contact Lisa Knowles lisa.knowles@jhuapl.edu"*. 5 commits as
  `Knowles, Lisa A <Lisa.Knowles@jhuapl.edu>` / `Lisa Knowles <lisa.knowles@jhuapl.edu>`
  (+467 / −204 lines) — a larger code contribution than Peter Shumate's (+58 / −21).
  Affiliation from the `@jhuapl.edu` address and the repository copyright holder.
- No ORCID recorded: the only public ORCID named "Lisa Knowles" (0000-0001-8181-0475) has no
  employments and no works, so identity cannot be confirmed. Left empty rather than guessed.

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
We also include command-line tools for creating and viewing the networked catalogs: cloudcatalog-tree lists all toplevel datasets and the number of dataIDs available; cloudcatalog-spider adds valid years and the number of files; cloudcatalog-update-json updates catalog.json using metadata from catalog_stub.json; cloudcatalog-update-csv updates catalog.json using metadata from cat.csv; cloudcatalog-gui provides a GUI for selecting files for cloudcatalog-update-json; and cloudcatalog-manifest2indices converts an AWS Manifest.csv to individual [dataID]_[YYYY].csv indices. The package also includes validators that check catalog.json files and dataset indices against the CloudCatalog specification.
```

The block above is the exact value, including the curly quotes U+2018/U+2019 in the bullets.

**Completed correction — the first line.** This record previously opened with "Shared Cloud
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
verbatim, which is also the verbatim abstract of the lead author's DASH 2025 record
(Zenodo 10.5281/zenodo.17398630) — the project's canonical present-day summary. It sits third so
the opening, and therefore the search-result preview, is unchanged. The final paragraph covers the
command-line tooling and validators, from `README.md` section "Command-line tools" (lines 30–44)
and `pyproject.toml` `[project.scripts]`; without it the description covered only the read API and
omitted roughly half the shipped software.

*Scope note:* the final paragraph describes the software **as released at the version this record
carries (1.2.1)**, which is what `pip install cloudcatalog` delivers and in which all six console
scripts work. One of the six, `cloudcatalog-manifest2indices`, was moved out to the
`heliocloud_tools` repository *after* the 1.2.1 release, by the source-revision merge itself
(PR #39, 2026-07-21), so it is absent from the current `develop` tree while remaining present in
the released package. It should be dropped from this paragraph whenever a future refresh advances
Field 12 past 1.2.1.

---

### 9. Concise Description (OPTIONAL, max 200 chars)
A Python package for retrieving cloud data file catalogs/indices

64 characters. Verbatim from the PyHC community registry (`_data/projects.yml`), the
highest-priority curated source.

*A fuller alternative, if a longer preview is ever wanted (166 chars):* "A specification, Python
API, and command-line toolset for serverless, decentralized indexing and retrieval of file
catalogs for massive cloud-stored science datasets."

---

### 10. Publication Date (RECOMMENDED)
2023-05-31

Corroborated: GitHub reports `created_at: 2023-05-31T15:15:55Z` for
`heliocloud-data/cloudcatalog`, an exact match. The first commit is later — `2738665` on
2023-09-13 — because the code was migrated in from `heliocloud/platform`, and the first PyPI
release (0.4) is 2023-10-26. The repository-creation date is the defensible "date of first
publication".

---

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

Per the Field 11 guidance — if no DOI has been obtained, indicate the repository host — and no
software DOI exists (Field 2).

---

### 12. Version (RECOMMENDED)
- **Version Number:** 1.2.1
- **Version Date:** 2026-03-31
- **Version Description:** the exact value is the single paragraph in the literal block below —
  plain text, no markup, no backtick characters:

```
Package reorganized into cloudcatalog.generators, cloudcatalog.updater and cloudcatalog.validators submodules; added the cloudcatalog-tree, cloudcatalog-spider and cloudcatalog-gui command-line tools; added catalog merge/update tools with JSON and CSV ingest, catalog validators, reverse lookup of dataset IDs by index path, alternate-catalog support, HTML index generation from catalog.json, and a sample-file helper; expanded the test suite and added black/pylint/pre-commit checks in CI.
```

- **Version PID:** Not found

Evidence, and the traps avoided:

- **PyPI is authoritative.** `https://pypi.org/pypi/cloudcatalog/json` gives
  `info.version` = **1.2.1**, sdist and wheel uploaded **2026-03-31T11:35:19Z**, not yanked.
  Full release history: 0.4 (2023-10-26), 0.5 (2024-03-12), 0.6.1 (2024-08-21), 1.0.0
  (2024-09-04), 1.0.2 (2025-02-19), 1.1.0 (2025-06-02), **1.2.1 (2026-03-31)**.
- **Not 1.2.3.** `pyproject.toml` on `develop` says `version = "1.2.3"` (set by commit `a3ab434`,
  2026-07-07). It is unreleased: no PyPI release, no git tag, no GitHub release. Automated
  metadata extractors report 1.2.3 with high confidence — that is the trap.
- **Not 1.1.01.** `pyproject.toml` on `origin/main` says `1.1.01`, a malformed and stale value;
  `main`'s HEAD (`db81e173`, 2026-03-31) predates the version bump commit `a50a73f`.
- **The 1.2.1 bump was never committed.** No commit on any branch sets `version = "1.2.1"`; the
  in-repo sequence runs 1.1.0 (`9d74d3c`) → 1.1.01 (`594947d`) → 1.2.2 (`a50a73f`) → 1.2.3
  (`a3ab434`), skipping 1.2.1 entirely, so the published sdist was evidently built from an
  uncommitted local edit. This *corroborates* rather than undermines the value: the 1.2.1 sdist and
  wheel were uploaded at 2026-03-31T11:35:19Z, and `a50a73f` bumps the repository to 1.2.2 at
  2026-03-31T12:25:33−04:00 (= 2026-03-31T16:25:33Z), four hours fifty minutes later the same day —
  the ordinary shape of a release followed by a post-release bump. PyPI, not git, is authoritative.
- **The Version Description is derived**, not quoted: there is no `CHANGELOG.md`, no release notes
  and no tags, so it summarises the 32 non-merge commits in `9d74d3c..db81e173` — from the 1.1.0
  version bump to the repository state contemporaneous with the 1.2.1 upload. It is plain text:
  module and command names appear bare, and any inline code formatting in this file's explanatory
  prose is presentation only and forms no part of the value.
- **Version PID:** no per-version DOI exists (see Field 2).

**Completed correction:** this record previously held version `1.1.0` dated 2025-09-04. That date
also disagreed with PyPI, which published 1.1.0 on 2025-06-02.

---

### 13. Programming Language (RECOMMENDED)
- Python 3.x

GitHub language statistics are 100% Python (121,256 bytes); `requires-python = ">=3.9"`; the CI
matrix pins `python-version: ["3.11"]`.

---

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.5281/zenodo.17398630

"CloudCatalog: an API plus Tools for Lazy Indexing of Millions of Cloud-Stored Data Files",
Alex Antunes (ORCID 0000-0002-3098-2602, JHUAPL), DASH 2025, published 2025-10-20, CC-BY-4.0.
It is the publication *describing this software*:

- its abstract is **verbatim** the current `README.md` lead paragraph;
- its Zenodo custom metadata declares
  `code:codeRepository = https://github.com/heliocloud-data/cloudcatalog`,
  `code:programmingLanguage = [Python, JSON]` and `code:developmentStatus = active` — the author
  explicitly bound the record to this repository.

The authors never designated a preferred citation: there is no `CITATION.cff` and no "how to cite"
section, so this assignment rests on authorship plus content rather than on a stated preference.

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
  catalog `index` entries "MUST start with s3:// or https://" (spec section 3);
  `docs/CloudCatalog-Demo.ipynb` — "works for AWS S3 or conventional hosting (HTTP or HTTPS
  URLs)"; `validators/validate_cloudcatalog_api.py` queries `https://api.heliocloud.org/...`.

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

- **csv** — `cloudcatalog-manifest2indices` writes `[dataID]_[YYYY].csv` indices;
  `spider(create_manifest=True)` writes `manifest_spider.txt` via `DataFrame.to_csv()`.
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

- `pyproject.toml` classifier `Development Status :: 4 - Beta` (stable, usable, still evolving).
- The Zenodo DASH 2025 record's custom field `code:developmentStatus = {"id": "active"}` — the
  author's own declaration.
- Currently developed: 32 non-merge commits between 1.1.0 and 1.2.1, with further work since
  (`a3ab434` 2026-07-07; PR #39 merged 2026-07-21); GitHub `pushed_at` 2026-07-21, 18 open issues,
  not archived.
- In production: "already used for 2 Petabytes of publicly available NASA and
  scientist-contributed data" (`README.md`).
- Not `WIP` — there are seven published PyPI releases and a stable public API. The "beta, use at
  risk for now" caveat in the README applies only to the generator/updater tools.

---

### 24. Documentation (RECOMMENDED)
https://github.com/heliocloud-data/cloudcatalog

The authors' own declared documentation location — `pyproject.toml`
`[project.urls] Documentation = "https://github.com/heliocloud-data/cloudcatalog"`, also carried on
PyPI. There is no documentation site: `docs/conf.py` and `docs/index.rst` exist (Sphinx,
`project = "cloudcatalog"`, title "cloudcatalog Documentation") but there is no `.readthedocs.yml`,
and `https://cloudcatalog.readthedocs.io/en/latest/` returns 404. The repository root carries the
README with usage and installation guidance, plus `docs/` (specification, contributing guide, demo
notebook, developer notes).

**Considered and excluded:** the PyHC-curated docs link
`https://github.com/heliocloud-data/cloudcatalog/blob/main/docs/cloudcatalog-spec.md` — reachable,
but it is the specification document alone, with no installation or usage content; and the `docs/`
tree `https://github.com/heliocloud-data/cloudcatalog/tree/develop/docs`, which is branch-pinned
and fragile.

---

### 25. Funder (OPTIONAL)
Not found

No funding statement, acknowledgement or grant number appears anywhere in the repository, on PyPI,
or in any of the four related Zenodo records (none has a `grants` entry). The only
funding-adjacent evidence is `docs/CONTRIBUTING.md` — "HelioCloud originated at NASA/GSFC from the
Heliophysics Data Research Library" — plus the NASA-owned `s3://gov-nasa-hdrl-data1/` bucket.

**Considered and excluded:** "National Aeronautics and Space Administration",
`https://ror.org/027ka1x80`. Institutional origin at NASA/GSFC and a NASA-owned S3 bucket do not
establish NASA as a *funder* of this software, and no grant or funding statement exists in any
source.

---

### 26. Award Title (OPTIONAL)
Not found

No award title or award number appears in the repository, in PyPI metadata, or in any related
Zenodo record.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.5281/zenodo.13887203

"HelioCloud as a replicable open science architecture", Gateways 2024, published 2024-10-03,
CC-BY-4.0. Creators: Antunes, Alex; **Shumate, Peter**; Thomas, Brian; Bradford, Jeffery;
Rourke, Sarah; Lenzi, Nicholas; **Jeschke, Chris**; Vandegriff, Jon — three of this software's four
person-authors. Its abstract names the software directly: "By separating our open source releases
as platform, heliophysics-specific container, **CloudCatalog indexing standard**, and
tutorials…". Concept DOI: 10.5281/zenodo.13887202.

**Considered and excluded:**
- 10.5281/zenodo.17398940 ("Contributing to the HelioCloud Open Science Cloud Computing
  Community", DASH 2025) — about HelioCloud community governance, with no substantive CloudCatalog
  content.
- 10.5281/zenodo.18749496 ("HDRL Show and Tell: Current Infrastructure", 2026-02-23, creators
  include "Antunes, Sandy") — its only CloudCatalog content is a single agenda line, "Sandy
  Antunes: HelioCloud development and the CloudCatalog", inside a twelve-topic internal
  show-and-tell deck. A mention, not a publication about this software.
- 10.5281/zenodo.17398630 — used as the Reference Publication (Field 14) rather than duplicated
  here.

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
2. **heliocloud_tools** — companion repository that now hosts the CloudCatalog web service and
   operations tooling moved out of this one: commits `19ecbdd` "moved cloudcatalog web service to
   heliocloud_tools instead", `d2c926a` / `dc03e16` / `89a5127` "Moved ops tools to
   heliocloud_tools repo". The service it hosts is the one exercised by
   `validators/validate_cloudcatalog_api.py` at `https://api.heliocloud.org/cloudcatalog?id=`.
3. **HAPI data specification** — the similar-purpose standard CloudCatalog explicitly models
   itself on and borrows from. `README.md`: enabling "HAPI-like" data ID + time range queries;
   `docs/CloudCatalog-Demo.ipynb`: "like HAPI, it is both a specification and an accompanying
   Python API"; `docs/cloudcatalog-spec.md` section 5: "the SCR Time format (**taken from the HAPI
   Time format**) is a subset of the ISO 8601 standard".

---

### 30. Interoperable Software (OPTIONAL)
- https://github.com/lasp/cdflib

**Canonical URL.** cdflib's repository moved from `MAVENSDC/cdflib` to `lasp/cdflib`:
`https://github.com/MAVENSDC/cdflib` returns HTTP 301 redirecting to
`https://github.com/lasp/cdflib`, and cdflib's PyPI metadata declares
`Homepage: https://github.com/lasp/cdflib` as its only project URL. The current canonical location
is recorded; a redirecting URL is deliberately not used.

**cdflib** is admitted on a concrete demonstrated exchange: the shipped demo notebook
`docs/CloudCatalog-Demo.ipynb` defines `plot_cdf(s3_uri, d, e, f)` whose body is
`cdf = cdflib.CDF(s3_uri)` then `plt.plot(cdf.varget(1))`, and drives it with
`fr.stream_uri(file_registry1[:3], lambda s3_uri, d, e, f: plot_cdf(s3_uri, d, e, f))`
(cells 41 and 43). The package's documented output — the S3 URIs emitted by `stream_uri()` — is
consumed directly by cdflib in the project's own worked example.

**Considered and excluded:**
- `pandas` — not listed even though the public API returns `DataFrame`s. Being a dependency is not
  interoperability.
- `boto3` / `botocore`, `requests`, `smart_open`, `python-dateutil`, `jsonschema`, `aiohttp`,
  `filelock`, `matplotlib`, `pytest` — generic infrastructure (cloud SDK, HTTP, I/O plumbing,
  schema validation, plotting, testing); each would be equally at home in a web app or a finance
  model.
- `astropy` — imported in `docs/CloudCatalog-Demo.ipynb` cell 1 (`import astropy.io.fits`) but
  never used in any cell. An unused import is not a demonstrated exchange.
- `PySPEDAS` and a HAPI client — explicitly future work, not implemented.
  `docs/CloudCatalog-Demo.ipynb` lists "add hooks to PySpedas & HAPI?" among future items and
  states: "Future: We'd love to work hook for CloudCatalog calls into other packages (esp.
  PySpedas and HAPI) so the cloud-stored data is fetchable within user's preferred toolsets."
  `tests/test_hapi.py` is a stub with its converter body commented out.
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

**This software has no logo of its own.**

**Considered and excluded:** the HelioCloud project logo. The PyHC registry curates
`logo: https://heliocloud.org/static/img/logo.jpg` for this package (that URL now 404s; the same
asset is served at `https://heliocloud.org/logo.png`), but it is the generic **HelioCloud project
wordmark**, not a CloudCatalog mark, and attaching a parent-project logo to one of its components
misrepresents the entry. Left empty until CloudCatalog has a logo of its own.

**Also not usable: `docs/scr_logo.png`.** It is the retired "SHARED CLOUD REGISTRY" mark from
before the 2023 rename and would republish the abandoned project name.

---

## Software name evidence (Field 7)

The software's name is **`CloudCatalog`**. This record previously held `CloudCatalog API`, which no
source supports.

1. **PyHC community registry** (`heliophysicsPy.github.io/_data/projects.yml`, entry at line 122)
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
5. **The specification names itself** "CloudCatalog" / "the generalized Cloud Catalog
   specification" throughout `docs/cloudcatalog-spec.md`, and the primary API class is
   `class CloudCatalog`.
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

---

## Completed corrections

Five values in this record were wrong or stale and have been corrected against the evidence cited
in their fields:

| Field | Was | Now |
|---|---|---|
| 7 Software Name | `CloudCatalog API` | `CloudCatalog` |
| 6 Authors | `Peter Schumate`, no identifier | `Peter Shumate`, ORCID `0009-0003-6088-5437` |
| 6 Authors | `Chris Jeschke`, no identifier | ORCID `0009-0008-8557-6709` added |
| 12 Version | `1.1.0`, dated 2025-09-04 | `1.2.1`, dated 2026-03-31 |
| 8 Description | opened with the abandoned "Shared Cloud Registry" name | opens with the current wording |

Both author corrections preserved the existing author identities and their positions in the author
order. Lisa Knowles was added as a fourth author, and JHUAPL affiliations were added to Jeschke,
Shumate and Knowles. Sixteen fields that were previously empty are now populated: 9, 11, 14, 15,
16, 17, 18, 19, 20, 21, 23, 24, 27, 28, 29 and 30, plus the version date and description in 12.

Fields deliberately left empty, each with its reasoning recorded in the field: 2 (no software DOI
exists), 22, 25, 26, 31, 32, 33.
