# HSSI Metadata Extraction Results

**HSSI Software ID:** f6e3429d-e80e-4cf6-889e-44af1e93f87d
**Repository:** https://github.com/hapi-server/client-python
**Source Revision:** aafecdb33f528c45304d8f1a33f405893f6dc842
**Extraction Date:** 2026-08-04
**Validation Date:** 2026-10-29
**Validation Status:** PASS

**Scope note.** `hapiclient` is a *protocol-generic* client: it implements the HAPI (Heliophysics
Application Programmer's Interface) specification and talks to any HAPI-compliant server. There is
no instrument-, mission-, or archive-specific code anywhere in the package. That single fact governs
several fields below — it is why Related Instruments, Related Observatories, and Related Phenomena
are correctly empty, why Related Region is deliberately broad, and why the server URLs and dataset
IDs appearing in `hapi_demo.py` are demonstrations rather than declarations of support. A future
agent tempted to add specific instruments or missions from the demo file should read Fields 31 and
32 first.

The repository at this revision differs structurally from its 0.2.x layout, which matters when
following file references in older notes: `setup.py` no longer exists (replaced by
`pyproject.toml`), the test suite lives in a top-level `test/` rather than `hapiclient/test/`, CI
has moved to `.github/workflows/pyhc-actions.yml`, and `misc/` now holds the release tooling. By this
revision six releases had shipped, between 2026-05-02 and 2026-07-22.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Placeholder — the submitter fields are not part of the software's metadata.*

---

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.5553155

**Evidence.** This is the Zenodo *concept* DOI — the all-versions identifier. It is declared in the
repository's own `.zenodo.json` (`related_identifiers`, `relation: isVersionOf`), is returned as
`conceptdoi` by every Zenodo version record in the series, the 0.3.3 record included. A concept DOI
presents the newest deposit, so what it shows moves with each release: on 2026-10-28 it resolved to
the 0.3.3 version record (`10.5281/zenodo.21892809`) and DataCite's concept record gave `version`
0.3.3, where at this dossier's extraction it presented 0.3.2.

**Why the concept DOI and not a version DOI.** Field 2 asks for the identifier of the software as a
whole; the version-specific DOI belongs in Field 12 (Version PID), where it is recorded.

---

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/hapi-server/client-python

**Evidence.** The repository's git remote, the PyHC registry `code` field, and the README's install
instructions (`pip install 'git+https://github.com/hapi-server/client-python'`) all agree. Verified
to resolve.

---

### 4. Software Functionality (MANDATORY)

**Values:**
- **Data Processing and Analysis**
- **Data Processing and Analysis: Data Access and Retrieval**
- **Data Processing and Analysis: Processing**

**Evidence for each value.**

- *Data Access and Retrieval* — the package's raison d'être. `hapiclient/get.py` (`get_binary`,
  `get_csv`) downloads HAPI `/data` responses; `hapiclient/catalog.py`, `hapiclient/info.py` and
  `hapiclient/capabilities.py` retrieve the `/catalog`, `/info` and `/capabilities` endpoints;
  `hapiclient/servers.py` fetches the master list of public HAPI servers. `hapiclient/util.py`
  wraps `urllib3` with HAPI-aware error handling. The single public entry point `hapi()`
  (`hapiclient/hapi.py`) dispatches on argument count to all of these.

- *Processing* — `hapiclient/get.py::_compute_dt` builds a NumPy structured dtype from the HAPI
  parameter metadata (sizes, types, string lengths, column offsets); `_parse_binary` reads the
  little-endian binary stream with `np.fromfile`/`np.frombuffer` and decodes Unicode string columns;
  `_parse_csv` and `_parse_csv_missing_length` parse CSV via `pandas.read_csv` with an
  `np.genfromtxt` fallback, then reshape columns into the structured array. `hapiclient/util.py::
  subset_meta` subsets and validates the parameter metadata.

**Considered and rejected, with reasons** (recorded so a future refresh does not re-litigate them):

- *Data Visualization* and any of its subcategories — **hapiclient plots nothing.** All plotting
  lives in the separate optional `hapiplot` package (https://github.com/hapi-server/plot-python).
  `hapiclient/__init__.py` exports only `hapi`, `request2path`, `hapitime2datetime`,
  `datetime2hapitime` and `HAPIError`; `matplotlib` is not a dependency in `pyproject.toml`. The
  README's example imports `hapiplot` separately.
- *Servers and Environments* (and *Data servers processing and handling*, *Distribution/Access*) —
  the closest tempting match, because the package's whole subject matter is data servers. Rejected:
  the parent category covers infrastructure, deployment and runtime-environment software (server
  implementations, containers, HPC, orchestration). `hapiclient` is strictly the client side; it
  contains no server, no Dockerfile, and no deployment artifacts.
- *Servers and Environments: High Performance Computing* — `hapiclient/data.py` uses
  `joblib.Parallel` with a threading backend, but only to issue at most five concurrent HTTP
  requests (`n_parallel` default 5, asserted `> 1`), and the code comment itself notes it "does not
  often lead to significant speed-up". Concurrent HTTP fetching is not high-performance computing.
- *Data Processing and Analysis: File Format Conversion* — literally the package reads CSV/binary
  and writes `.npy`/`.pkl` cache files (`hapiclient/util.py::write_atomic`), but that is the
  response cache, not a conversion feature: there is no API by which a user asks hapiclient to
  convert file A into file B. The formats involved are recorded in Fields 18 and 19
  instead.
- *Data Processing and Analysis: Data Reduction* — parameter selection (`subset_meta`) and time-range
  trimming do reduce data volume, but the category means averaging/binning/downsampling, none of
  which the package performs.
- *Data Processing and Analysis: Analysis* — the catch-all. Rejected: no derived physical quantities
  are computed anywhere in the package.
- *Data Processing and Analysis: Time Series Analysis* — **considered at length and rejected.** The
  case for it is real: `hapiclient/hapitime.py` is a 356-line module devoted entirely to HAPI time
  handling, two of its functions (`hapitime2datetime`, `datetime2hapitime`) are among the five names
  exported from `hapiclient/__init__.py` and so are user-facing rather than internal, and
  `hapiclient/data.py::_get_chunks` splits a request at cadence-derived hour/day/month/year
  boundaries, trims the first and last chunk to the requested range, and `np.concatenate`s the
  results into one time-ordered array. That is nonetheless **time-*format* conversion and
  time-*range* request partitioning, not analysis of time-ordered data**: the package performs no
  filtering, detrending, autocorrelation or resampling, derives no new quantity from the time
  series, and the retained *Processing* subcategory already covers the parsing that turns a response
  into arrays. Selecting this value would surface `hapiclient` for a user searching for software
  that analyses time series, which it does not do. Recorded in full so a future refresh does not
  re-propose it.
- *Coordinate Transforms* (any subcategory) — `hapi_demo.py` requests parameters named `X_GSE`,
  `Y_GSE`, `Z_GSE` and `BGSEc`, which is a coordinate-system *name* appearing in a dataset's
  parameter list, not a transform. The package performs no coordinate conversion.
- *Mission-related* (any subcategory) — the package is protocol-generic and belongs to no mission's
  ground system.

**0.3.3 changes no value here** (read at `e990889180a80ecfb277271bff6cdb1e088521c0`). PR #108
extends the response cache to the `/catalog` and `/capabilities` endpoints (`hapiclient/catalog.py`
and `hapiclient/capabilities.py` now go through `cache.meta_cache_read` and `meta_cache_write`), and
PR #107 removes a warning from the fallback to CSV when a server does not offer binary. Both refine
how the package retrieves data, which *Data Access and Retrieval* already records; neither adds a
capability that another category describes.

**Parent-present invariant.** Both selected subcategories — *Data Access and Retrieval* and
*Processing* — sit under `Data Processing and Analysis`, which is itself selected, so the
invariant holds. (The subcategory names appearing in the rejected list above are not selected
values and impose no parent requirement.)

---

### 5. Related Region (MANDATORY)

**Values:**
- **Earth Atmosphere**
- **Earth Magnetosphere**
- **Interplanetary Space**
- **Planetary Magnetospheres**
- **Solar Environment**
- **Solar Wind**

**Reasoning.** A protocol-generic client supports whichever regions the queried server serves, so the
correct shape for this field is a broad set rather than a precise one. All six selected values are
regions HAPI servers serve time series for, and none is contradicted by anything in the repository.
An earlier extraction argued for a narrower set — only Earth Magnetosphere, Interplanetary Space and
Solar Environment. Earth Atmosphere and Planetary Magnetospheres are nonetheless correct and are
deliberately retained: there is no evidence they are wrong, and HAPI servers do serve atmospheric
and planetary-magnetospheric time series.

**`Solar Wind` rests on the same basis as the other five**, not on any narrower one. The reasoning
that justifies a broad region set justifies this value too: a protocol-generic client supports
whichever regions the queried server serves. The one server-specific fact it rests on is definitional
rather than demonstrated — `OMNIWeb`, a Data Source on this record (Field 17), *is* an archive of
near-Earth solar-wind plasma and interplanetary magnetic field data; that is what OMNI is,
independent of any file in this repository. `Solar Wind` is a controlled value distinct from
`Interplanetary Space`, so selecting one does not imply the other; a user filtering on solar-wind
software would otherwise not reach this record despite the data it is used to retrieve.

**No demonstration file is cited as evidence in this field, and the argument does not depend on one
indirectly either.** The server URLs and dataset identifiers in `hapi_demo.py` exist to exercise the
client against several servers and are rejected as evidence in Fields 22, 31 and 32; treating them
as evidence here — directly, or by leaning on Field 17 entries that were themselves selected from
those demonstrations — would be inconsistent. `OMNIWeb` is cited above because its subject matter is
a matter of definition — what OMNI *is* — not because `hapi_demo.py` happens to call it.

**Negative research — `SSCWeb` does not support the `Solar Wind` selection, and a future refresh
should not enlist it.** An earlier draft of this rationale grouped CDAWeb, OMNIWeb and SSCWeb
together as servers on which solar-wind data is well represented. That is wrong for SSCWeb: the
Satellite Situation Center
is a spacecraft **ephemeris** service, serving orbital position, magnetic-field-line traces and
geophysical-region mapping rather than plasma or field measurements. The repository's own
demonstration bears this out — `hapi_demo.py::sscweb()` requests `dataset='ace'` with
`parameters='X_GSE,Y_GSE,Z_GSE'`, which is the ACE spacecraft's position, not anything ACE measured.
`SSCWeb` remains a correct Field 17 Data Source; it is simply not evidence for a region.

**Not selected.** The remaining region values (`Chromosphere`, `Corona`, `Earth Ionosphere`,
`Earth Magnetotail`, `Heliosheath`, the per-planet magnetospheres, etc.) were considered and
rejected: there is nothing in the repository that distinguishes them from one another for a generic
client, and selecting them all would make the field meaningless.

---

### 6. Authors (MANDATORY)

Four authors. The set rests on the citation-bearing sources taken together — `CITATION.cff`,
`.zenodo.json`, `pyproject.toml`, the Zenodo v0.2.1 deposit (record 5553156) and its DataCite record,
and the authors' ORCID records — with the specific support for each author given under that author.
Everyone named as a creator in those sources is an author here; contributors named in none of them
are not (see the rejected list at the end of this field).

**Author 1 — Robert S. Weigel**
- **Author Identifier:** https://orcid.org/0000-0002-9521-5228
- **Affiliation — Organization:** George Mason University
- **Affiliation Identifier:** https://ror.org/02jqj7156
- **Sources:** the byline form used on publications indexed under this ORCID (e.g. the JGR paper in
  Field 14, which carries "Robert S. Weigel" with this exact ORCID attached) — note that ORCID's own
  structured profile fields are the barer `given-names: Robert` / `family-name: Weigel`, with no
  middle initial and no `other-names`, so the fuller form comes from the publication byline rather
  than from the ORCID name record itself; `LICENSE.txt` ("Copyright 2019- R.S. Weigel");
  `pyproject.toml` `authors = [{ name = "Bob Weigel", email = "rweigel@gmu.edu" }]`; `.zenodo.json`
  creators; the PyHC registry `contact` field ("Bob Weigel").
- **Note — do not "fix" this name from the repository.** Three upstream sources give a non-canonical
  form and all three are wrong in different ways: `pyproject.toml` and `.zenodo.json` give the
  informal "Bob Weigel"; `CITATION.cff` has the name components **swapped**
  (`family-names: Robert S.` / `given-names: Weigel`); and the DataCite record for the version DOI
  carries `familyName: "Bob Weigel"` with an empty given name, a Zenodo-side artifact of the
  single-string `name` in `.zenodo.json`. The ORCID-canonical form "Robert S. Weigel" recorded
  above is correct and should not be replaced from any of them.

**Author 2 — Hari Narayana Batta**
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Sources:** Zenodo deposit 5553156 (v0.2.1) creators; git history
  (`Hari Narayana Batta <harinarayanabatta1997@gmail.com>`, 6 commits).
- **Negative research (do not repeat).** An ORCID search on the family name Batta returns no record
  whose name, works or affiliations connect to heliophysics or to this project. No affiliation is
  discoverable from the commit email (a personal address). Leave both sub-fields empty.

**Author 3 — Jeremy Faden**
- **Author Identifier:** https://orcid.org/0000-0003-2397-488X
- **Affiliation — Organization:** Cottage Systems — https://ror.org/01sqsqt89
- **Affiliation — Organization:** University of Iowa — https://ror.org/036jqmy94
- **Sources:** The ORCID and both affiliations were supplied by the maintainer in the original
  submission; Zenodo deposit 5553156 creators; git history
  (`Jeremy Faden <faden@cottagesystems.com>`, which independently corroborates the Cottage Systems
  affiliation). Both ROR records are Iowa City, Iowa, consistent with each other.

**Author 4 — Jon Vandegriff**
- **Author Identifier:** https://orcid.org/0000-0002-0781-1565
- **Affiliation — Organization:** Johns Hopkins University Applied Physics Laboratory
- **Affiliation Identifier:** https://ror.org/029pp9z10
- **Evidence.** The ORCID record 0000-0002-0781-1565 gives the name "Jon Vandegriff", carries the
  **verified public primary email `jon.vandegriff@jhuapl.edu`**, which is byte-identical to the
  commit author email in this repository (`jvandegriff <jon.vandegriff@jhuapl.edu>`); lists
  employment at Johns Hopkins University Applied Physics Laboratory, Space Exploration Sector; and
  includes among its works "Interoperability for Heliophysics and Planetary Time Series Data via
  HAPI". Five other ORCID records share the surname and none has any heliophysics connection, so the
  match is unambiguous. The affiliation is recorded under the institution's full name rather than
  the "JHU APL" acronym.
- **Name provenance.** Zenodo recorded this creator only as the GitHub handle "jvandegriff"; the
  full name "Jon Vandegriff" comes from the original submitter and is confirmed by the ORCID record.
- **Completed correction.** This author was previously carried by name alone, with neither an
  identifier nor an affiliation. The ORCID, affiliation and ROR above are the correct values on the
  evidence given; they are settled and should not be re-derived on a later pass.

**Considered and rejected as authors.** The git history also contains commits from Sandy Antunes
(`sandy@rpg.net`), Srikar Reddy Karemma, David Stansby and `sapols` (a PyHC-actions workflow
contribution). None of them appears in any citation-bearing source — not `CITATION.cff`, not
`.zenodo.json`, not any Zenodo deposit's creator list, not `pyproject.toml`. They are contributors,
not authors, and are deliberately excluded.

**Documented upstream defects in the repository** (worth reporting to the maintainer, but not
grounds for changing HSSI): `CITATION.cff` has `family-names` and `given-names` reversed, declares
`cff-version: 0.2.1` (not a valid CFF schema version — it appears to be the software version pasted
into the wrong key), and pins `version: v0.2.1` / `date-released: 2021-10-06`, both years out of
date. `pyproject.toml` lists only one of the four authors.

---

### 7. Software Name (MANDATORY)
- **Value:** HAPI Client

**Evidence.** This is the display name in the PyHC core-packages registry (`name: "HAPI Client"`),
which is the manually curated and therefore highest-priority source for a name. Alternative forms
deliberately not used: `hapiclient` (the PyPI/import identifier), `hapi-server/client-python` (the
repository path), and `hapi-server/client-python:` (the Zenodo/DataCite title, which is malformed —
it ends in a bare colon because `.zenodo.json` sets `"title": "hapi-server/client-python:"`).

---

### 8. Description (MANDATORY)

- **Value:** A Python client for the Heliophysics Application Programmer's Interface (HAPI). This package provides functions to access time series data from HAPI-compliant servers, which serve data from various heliophysics missions and instruments. The client handles data retrieval, caching, and provides utilities for time format conversions. An optional hapiplot package provides basic visualization capabilities including line plots and spectrograms. The HAPI data model is intentionally minimal and follows the HAPI metadata specification closely.

**Verified against the current README.** Every claim still holds at this revision: retrieval
(`hapiclient/get.py`), caching (`hapiclient/cache.py` plus `hapiclient/util.py::write_atomic`),
time-format utilities (`hapiclient/hapitime.py`), the optional `hapiplot` companion (README
installation section), and the deliberately minimal metadata model (the README's "Metadata Model"
section states it "is intentionally minimal and closely follows that of the HAPI metadata model").
The large restructuring between 0.2.9 and 0.3.2 was packaging and internal refactoring; it changed
nothing this description asserts.

**Deliberately not extended, despite being incomplete.** The description does not mention
chunked/parallel requests or catalog/info metadata browsing. That is an omission, not an error, and
the wording is the submitter's editorial choice; it is not rewritten merely because a longer version
could be written.

---

### 9. Concise Description (OPTIONAL)

- **Value (196 characters):** Python client for accessing time series data from HAPI-compliant servers, with response parsing, caching, chunked and parallel requests, and time-format conversion utilities for heliophysics data.

**Previous value and why it was corrected.** The previous text read "Python client for
accessing time series data from HAPI servers, providing data retrieval and **basic plotting
capabilities** for heliophysics data." That attributes plotting to `hapiclient`, which is factually
wrong and is contradicted by the record's own Description field one line above it (which correctly
assigns plotting to the separate optional `hapiplot` package) and by the package's public API, which
exports no plotting function and does not depend on `matplotlib`. Because the concise description
is the short summary a user reads before opening the record, the error is user-visible. The
replacement keeps the original sentence shape and register and substitutes capabilities the package
actually has, each backed by code cited in Field 4.

**This is a correction of a submitted value, not a stylistic preference** — it was made only because
the previous text makes a false capability claim, and would not have been made otherwise.

---

### 10. Publication Date (RECOMMENDED)

- **Value:** 2018-09-19

**Governing reading of the field.** Field 10 is defined as the "date of first broadcast/publication
… used for the initial version of the software". It asks when the software was *first published*,
not when it first acquired a DOI.

**Evidence.** `CHANGES.txt` opens with four entries — `v0.0.1`, `v0.0.2`, `v0.0.3` and `v0.0.4` —
each reading "2018-09-19 -- Initial package release." The earliest surviving `hapiclient` release
file on PyPI is 0.0.3, uploaded 2018-09-19T16:11:15Z, the same day. (Files for 0.0.1 and 0.0.2 no
longer exist on PyPI, which is why 0.0.3 is the earliest *surviving* upload rather than the earliest
release.) Repository and package index agree: `hapiclient` was first published on 2018-09-19.

**Rejected alternative — 2018-09-19 supersedes 2021-10-06, which was the previously recorded
value.** `2021-10-06` is the date of the **first Zenodo deposit** (record 5553156, software version
v0.2.1). Three artifacts carry it and agree with one another: `.zenodo.json`
(`"publication_date": "2021-10-06"`), `CITATION.cff` (`date-released: 2021-10-06`), and the Zenodo
and DataCite records for the concept DOI and for every version DOI in the series. It is nonetheless
a **deposit date, not a first-publication date** — the software had been publicly released for three
years before that deposit existed. This is a settled decision, taken in full knowledge that it
leaves HSSI's Publication Date disagreeing with the `publicationYear` of the DOI this record links
to; that disagreement is accepted because the two fields are answering different questions.
**Do not revert to 2021-10-06.** Re-encountering the DOI's 2021 date is expected, not a discovery.

**Previously rejected alternative.** An early extraction proposed 2017-06-02 (the GitHub repository
creation date, via SoMEF). Rejected then and still rejected: repository creation is not publication,
and the first release post-dates it by fifteen months.

---

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Evidence.** DataCite reports `publisher: "Zenodo"` for the version DOI, and the DOIs are minted
through the GitHub–Zenodo integration, which is exactly the case the form's guidance names.

**Previous incorrect value, corrected.** The Publisher Identifier was once recorded as
`https://ror.org/01ggx4157`. That ROR resolves to **CERN** (European Organization for Nuclear
Research), not to Zenodo — CERN hosts Zenodo, but the two are not the same entity, and no ROR record
exists for Zenodo itself. `https://zenodo.org` is both authoritative and precisely the example the
submission form gives for a publisher with no ROR. Do not reintroduce the CERN ROR.

---

### 12. Version (RECOMMENDED)

- **Version Number:** 0.3.3
- **Version Date:** 2026-08-11
- **Version PID:** https://doi.org/10.5281/zenodo.21892809
- **Version Description:**
  - Don't warn if binary not available
  - Cache catalog and capabilities

**Previous values.** HSSI held 0.3.2 (released 2026-07-22, Version PID
https://doi.org/10.5281/zenodo.21496990) until the 0.3.3 update, and v0.2.9 (released 2026-06-08)
before that. Each was superseded by a newer release (Field 12 rule 3).

**Why 0.3.3** (read at `e990889180a80ecfb277271bff6cdb1e088521c0`, the head of `master`, and at the
tagged commit `c40f02afb02cff6fdbf4c99ed0dcc8fd11ac578f`). The tags `v0.3.3` and `0.3.3` both point
at `c40f02a` ("Last 0.3.3 commit", 2026-08-11), which lies on `master`'s own lineage:
`git merge-base --is-ancestor 0.3.3 e990889` holds, and so does `0.3.2` → `0.3.3`. At that commit
`hapiclient/__init__.py` sets `__version__ = '0.3.3'` and `pyproject.toml` sets `version = "0.3.3"`.
The GitHub release `0.3.3` ("Release 0.3.3") is neither a draft nor marked as a pre-release, and
PyPI's JSON API gives `0.3.3` as `info.version`, with a sdist that is not yanked. The remote's other
branches are issue branches (`105-catch-json-error-response`, `94-cache-files-can-be-corrupted-…`
and the like) and a Copilot branch; none is a release branch.

**Nothing newer had been released on 2026-10-28.** PyPI's newest upload is `0.3.3`, and no later
tag exists. The four commits after the tag (`3d164af` through `e990889`, 2026-08-11 to 2026-08-12)
are unreleased: `pyproject.toml` and `__version__` still say `0.3.3` at `e990889`, while
`CHANGES.txt` has opened a `v0.3.4b0` heading holding "Set Accept-Encoding headers in request." A
later refresh should look for a 0.3.4 release.

**`b` versions are pre-releases and are never recorded.** The project tags its betas and publishes
them on GitHub and Zenodo, so they look like releases. `0.3.3b0` was the case in point: its GitHub
release was published 2026-07-22T16:05:11Z, thirty seconds *before* the `0.3.2` release, with its
`prerelease` flag set to false, and Zenodo minted a version DOI for it (`10.5281/zenodo.21496985`).
The 0.3.3 release of 2026-08-11 superseded it, which settles that tag; the reasoning holds for every
later `b` tag:

1. **The project's own release process says `b` versions are not releases.** The `Makefile` header
   documents two separate procedures. Under "Beta versions" it states in the heading:
   *"Beta versions (not released to pypi.org)."* Under "Releases" step 1 is *"Remove the 'b' in the
   version in CHANGES.txt"*, and step 4 is to create the **next** `b0` version and commit it, which
   "will update the version information in the repository to indicate it is now in a pre-release
   state." `0.3.3b0` was that post-release development marker, set by commit `fbcfe2f`, "Update
   version for next release", two minutes after the 0.3.2 release commit. The `0.3.3b0` tag itself
   points at `944374b`, the commit just before the 0.3.2 release commit.
2. **`0.3.3b0` was never published to PyPI.** PyPI has no `0.3.3b0` file. (Some much older betas
   were uploaded — `0.0.9b0`, `0.1.5b4`, `0.1.9b2`, `0.1.9b3` — and are pre-releases all the same.)
3. **The `prerelease=false` flag is a tooling artifact, not a statement.** The `gh-release` target
   is `gh release create $(VERSION) --target master --notes "Release $(VERSION)" --title "Release
   $(VERSION)"` — it never passes `--prerelease`, so *every* GitHub release this project has ever
   made reports `prerelease=false`, betas included. The flag carries no information here.
4. **Zenodo's concept DOI presented 0.3.2, not 0.3.3b0, while those were the two newest deposits**
   (`10.5281/zenodo.21496985` for 0.3.3b0, `10.5281/zenodo.21496990` for 0.3.2). That corroborates
   rather than decides: a concept presents the most recently created deposit, and the 0.3.2 deposit
   was created thirty seconds later.

**`0.3.3`, bare, is the exact version string.** It is `__version__` in `hapiclient/__init__.py` at
the tagged commit, the PyPI release name, the GitHub release tag, and DataCite's `version`
attribute for the Version PID, and it keeps the bare form the superseded `0.3.2` was stored in. The
version is that number alone — never `v`-prefixed, and never combined with the software name.

**Tag-naming inconsistency, for future reference.** Each release produces **two** git tags, because
`make version-tag` runs `git tag -a v$(VERSION)` while `make gh-release` runs
`gh release create $(VERSION)` with the bare number. Both `v0.3.2` and `0.3.2` therefore point at
commit `ff91cda93e578bffa996ea827d781d6de4d86d7f`, and both `v0.3.3` (annotated) and `0.3.3`
(lightweight) at `c40f02afb02cff6fdbf4c99ed0dcc8fd11ac578f`. Older releases (through `v0.3.0`) have
only the `v`-prefixed tag because the GitHub releases for them were made by hand. Do not read the
duplication as two different releases.

**Version Date — 2026-08-11, the release event's UTC day.** The GitHub release `0.3.3` was published
2026-08-11T18:01:01Z. The tagged commit `c40f02a` is dated 2026-08-11 14:00:58 -0400 (18:00:58 UTC),
the annotated tag `v0.3.3` one second later; the Zenodo version record was created
2026-08-11T18:01:06Z and the PyPI sdist was uploaded 2026-08-11T18:03:34Z. All fall on the same UTC
day.

**Version PID — verified, and Zenodo's own metadata for it is partly wrong.** The Zenodo version
record 21892809 carries `version: "0.3.3"`, `conceptdoi: 10.5281/zenodo.5553155` and the file
`hapi-server/client-python-0.3.3.zip`; DataCite gives the DOI `version` 0.3.3 and an `IsVersionOf`
relation to the concept, and the concept's `HasVersion` list includes it. That fixes the mapping
unambiguously. But the same record reports `publication_date: 2021-10-06` and `license:
other-open`, and DataCite mirrors both (`publicationYear: 2021`, `dates: [{2021-10-06, Issued}]`,
`rightsList: [Other (Open)]`). **Both are Zenodo-side errors inherited verbatim from the
repository's hand-maintained `.zenodo.json`, which hard-codes a 2021 publication date and
`"license": "other-open"` for every deposit in the series.** The Version Date above and the License
in Field 15 are therefore derived from the repository and the release artifacts, not copied from the
DOI record. Anything auto-filled from this DOI must be re-checked against the repository.

**Version Description — the release's own words.** The GitHub release's name and body are both the
auto-generated "Release 0.3.3", and the Zenodo deposit's description is the package description
"Python client for HAPI", so neither carries release notes (Field 12 rule 16). The text therefore
comes from `CHANGES.txt` at the tagged commit (rule 13), which ends:

```
v0.3.3b0:
	2026-07-22 -- Makefile and related updates
	2026-08-10 -- Don't warn if binary not available
v0.3.3:
	2026-08-11 -- Cache catalog and capabilities https://github.com/hapi-server/client-python/pull/108
```

Both headings belong to 0.3.3. `v0.3.3b0` is the development heading that the `Makefile`'s release
step 4 opens after each release; step 1 says to remove its "b" at release time, and for 0.3.3 the
maintainer instead added a separate `v0.3.3` heading below it. The `0.3.3b0` tag (`944374b`) carries
the heading empty, `fbcfe2f` reopened it empty after the 0.3.2 release, and both entries under it
were committed inside the `0.3.2..0.3.3` range (`aafecdb`, 2026-07-22; `646a99e`, "do not warn
(#107)", 2026-08-10). Filtered for the site user (rule 14):

- "Makefile and related updates" is a build chore and is dropped.
- "Don't warn if binary not available" is kept: when a server's `/capabilities` response does not
  offer the binary transport format, the client now falls back to CSV without the warning it used to
  print (`hapiclient/data.py::_get_format`, where the warning call is commented out).
- "Cache catalog and capabilities" is kept: `/catalog` and `/capabilities` responses are now cached
  as `/info` responses already were (PR #108).

The two kept items are recorded verbatim, as markdown bullets in the changelog's order, without their
date prefixes and with the #108 item's trailing pull-request link dropped (rule 15).

**Superseded description, not repeated.** The 0.3.2 row's description was a summary composed from
that release's `CHANGES.txt` line and the `0.3.1..0.3.2` source diff. A composed summary is never
recorded (rule 15), and one release's description is never carried onto a newer number (rule 10).

---

### 13. Programming Language (RECOMMENDED)

- **Python 3.x**

**Previously recorded value, corrected.** `Python 2.x` was listed alongside `Python 3.x` in this
record; the entry is incorrect. It entered the record from the Python 2 dependency branch in the old
`setup.py`; both that branch and the file itself are gone, upstream dropped Python 2.7 support in
v0.2.7, and nothing at this revision can even be imported under Python 2. `Python 3.x` alone is
correct, and `Python 2.x` should not be restored.

**Evidence that Python 2 support is gone.**

1. **The project says so explicitly.** `CHANGES.txt`, entry `v0.2.7` (2026-05-02):
   *"Support for Python 2.7 dropped."* That release predates the version recorded in Field 12.
2. **The file that carried the Python 2 support was deleted.** `setup.py` — which held the Python 2
   dependency branch cited as the original justification for this value — was removed in the
   `0.3.1..0.3.2` diff and replaced by `pyproject.toml`.
3. **No supported Python floor admits Python 2.** `pyproject.toml` declares
   `requires-python = ">=3.8"` at the 0.3.3 tag and at `e990889`, and PyPI's metadata for 0.3.3
   carries the same floor; the 0.3.2 release had declared `>=3.5`. Neither permits 2.x.
4. **No test target is Python 2.** `tox.ini` `envlist = py38,py39,py310,py311,py312,py313,py314`;
   the `py27` environment that once justified this value is gone. `.travis.yml` runs Python 3.8
   only, and `.github/workflows/pyhc-actions.yml` runs the PyHC PHEP 3 and environment-compatibility
   checks.
5. **Python-3-only syntax makes the package uncompilable under Python 2.** At `e990889`,
   `hapiclient/util.py` uses f-strings at lines 482, 519, 522 and 526 (in `write_atomic`),
   `hapiclient/data.py` uses one at line 26 (`log(f'Using STOP = {stop}')`), and
   `hapiclient/cache.py`, since 0.3.3, two more at lines 131 and 133. f-strings are a
   **parse**-time construct, so any one of these modules alone is a `SyntaxError` under Python 2
   regardless of whether the enclosing function is ever called. `hapiclient/data.py` is reached
   from the public `hapi()` entry point, so the package cannot even be imported under Python 2.

**The counter-evidence, and why it does not save the value.** Two `sys.version_info` branches that
could be read as Python 2 support survive at `e990889`: `hapiclient/get.py` line 148
(`if sys.version_info[0] < 3:`), which is **unreachable dead code** — it can never execute, because
the module graph fails to compile under Python 2 — and a `<= (3, 5)` branch in
`hapiclient/util.py::unicode_error_message` (line 101), which is a Python 3.5 check, not a Python 2
one. (`hapiclient/__init__.py` line 21, `sys.version_info < (3, 10)`, is a macOS warning filter for
Python 3.) Two more that this section once listed were deleted in 0.3.3: the `reload(sys)` /
`setdefaultencoding` block in `hapiclient/__init__.py` and the `sys.version_info < (3, )` trimming
branch in `hapiclient/data.py::_get_chunks`. Vestigial compatibility branches are evidence of
history, not of support.

**Not selected:** any other programming language. `Python 3.x` is the only applicable value — the
package is pure Python; there are no compiled extensions, no bundled C/Fortran, and no other
language in the source tree.

---

### 14. Reference Publication (OPTIONAL)
- **Value:** https://doi.org/10.1029/2021JA029534

**Verified.** The DOI resolves to Weigel, R. S., Vandegriff, J., Faden, J., King, T., Roberts, D. A.,
Harris, B., Candey, R., et al. (2021), *"HAPI: An API Standard for Accessing Heliophysics Time Series
Data"*, **Journal of Geophysical Research: Space Physics**, December 2021. It is the paper describing
the HAPI standard this package implements, and its first three authors are three of this record's
four authors. It is the correct reference publication.

**Provenance.** The value was supplied by the submitter; no reference publication is cited anywhere
in the repository, so a from-scratch extraction would not have found it. Do not remove it on the
grounds that the repository does not mention it.

---

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html
- **SPDX identifier:** BSD-3-Clause

**Evidence.** `LICENSE.txt` contains the verbatim three-clause BSD text — copyright notice
("Copyright 2019- R.S. Weigel"), the binary-redistribution clause, and the no-endorsement clause —
followed by the standard BSD warranty disclaimer. `pyproject.toml` references it with
`license = { file = "LICENSE.txt" }`. PyPI carries the same text. The exact applicable value is
`BSD 3-Clause "New" or "Revised" License`, with straight double quotes around *New* and *Revised*,
not curly ones.

**Do not copy the DOI record's licence.** `.zenodo.json` declares `"license": "other-open"`, and
Zenodo and DataCite therefore both report "Other (Open)" for every version DOI in this series. That
is an upstream error in the repository's Zenodo configuration, not a different licence — the actual
`LICENSE.txt` is unambiguous BSD-3-Clause. Any DOI-driven autofill will get this wrong.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values** (stored lower-case):
- data_retrieval
- hapi
- heliophysics
- metadata
- pyhc package
- python
- time series
- web service

**Evidence for `data_retrieval`, `hapi`, `heliophysics` and `time series`.** `data_retrieval` is the
term the PyHC core-packages registry uses for this project, and it names the package's primary
capability (Field 4). `hapi` is the protocol the package implements and the name it is published
under. `heliophysics` is the domain the protocol and its servers serve. `time series` is the only
kind of data HAPI transports — the standard is an API for heliophysics time series (Field 14), and
`hapi()` returns time-ordered arrays.

**Evidence for `metadata`, `python` and `web service`.** `web service` — the package is a client for
a web-service API; it issues HTTP GETs against the HAPI `/catalog`, `/info`, `/data` and
`/capabilities` endpoints (`hapiclient/catalog.py`, `info.py`, `get.py`, `capabilities.py`).
`metadata` — HAPI metadata access is a first-class, separately documented capability, not a side
effect: `hapi(server)` and `hapi(server, dataset)` return catalog and info metadata, `subset_meta`
subsets it, it is cached independently of the data, and the README devotes a "Metadata Model"
section to it. `python` — the package is pure Python (`pyproject.toml`, an all-`.py` source tree, no
compiled extensions).

**`pyhc package` is the PyHC package marker (Field 16 rule 15).** HAPI Client is listed in the PyHC
registry's `_data/projects_core.yml` (read 2026-10-28), so the record carries `pyhc package`, written
exactly so, which lets a searcher find every PyHC package with `keyword:"pyhc package"`. It rests on
that rule rather than on any term the project declares, and the rule overrides the keyword
exclusions that would otherwise apply to it.

**`line_plots`, `plotting` and `spectra` were once recorded here, and are deliberately not keywords
of this record.** They describe capabilities that live entirely in the separate `hapiplot` package,
not in `hapiclient`, which is the same fact Fields 4, 8 and 9 all rest on: `hapiclient/__init__.py`
exports no plotting function, `matplotlib` is not a dependency, and the README installs `hapiplot`
separately to plot anything.

The three keywords originate in the PyHC core-packages registry, which lists exactly
`["data_retrieval","line_plots","plotting","spectra"]` for the "HAPI Client" project. PyHC is the
manually curated, highest-priority source for keywords, and that is why they survived earlier
passes — but PyHC is scoping the *project*, which it treats as including the plotting companion,
whereas this HSSI record is for `hapiclient` specifically. Within that scope the three keywords
assert a capability the software does not have, so they are correctly absent here. A future refresh
will meet them again in the PyHC registry; that is expected and is not grounds to restore them.

**The hapiclient ↔ hapiplot relationship is not lost by their absence.** It remains asserted where
it belongs: Field 29 (Related Software) and Field 30 (Interoperable Software) both carry
`https://github.com/hapi-server/plot-python`, and Field 8's Description names the optional hapiplot
package explicitly.

**Considered and rejected:** `cdaweb`, `omniweb`, `sscweb` (duplicate Field 17); `csv` (duplicates
Fields 18/19) and `json` (duplicates Field 19); `data access` (a synonym of the recorded
`data_retrieval` — note that `data_retrieval` and `data retrieval` are two distinct terms in the
keyword vocabulary, and the underscore form recorded here, which is the form PyHC uses, is the
correct one for this record); `space physics` (a synonym of the recorded `heliophysics`).

---

### 17. Data Sources (OPTIONAL)

**Values:**
- **CDAWeb**
- **HAPI**
- **Observatory/Mission-specific**
- **OMNIWeb**
- **SSCWeb**

**Evidence.** `HAPI` is the defining source type — the package speaks only this protocol, and
`hapiclient/servers.py` fetches the master list of public HAPI servers from
https://github.com/hapi-server/servers/raw/master/all.txt. `CDAWeb` and `OMNIWeb`: the README's
headline example and `hapi_demo.py::cdaweb()` / `omniweb()` query
`https://cdaweb.gsfc.nasa.gov/hapi`, including the OMNI2 hourly merged dataset. `SSCWeb`:
`hapi_demo.py::sscweb()` queries `http://hapi-server.org/servers/SSCWeb/hapi`.
`Observatory/Mission-specific`: a substantial share of public HAPI servers are single-mission or
single-observatory endpoints, so the client routinely reaches mission-specific sources.

**Considered and rejected.** `Other` for LISIRD — `hapi_demo.py::lisird()` queries
`http://lasp.colorado.edu/lisird/hapi`, and the data-source vocabulary offers no value for LISIRD.
`Other` was rejected as carrying no information the already-selected `HAPI` value does not: `HAPI`
asserts that *any* HAPI server is supported, which is the accurate statement about this package.
`HTTP/HTTPS Directories` was rejected: the client fetches over HTTP but from a structured API, never
from directory listings. `FTP/FTPS Directories`, `S3/Cloud-aware`, `das2`, `AMDA`, `Madrigal`,
`TAP`, `VirES`, `GFZ`, `WDC` and `The Virtual Solar Observatory.` were rejected — no code path in
the package reaches any of them.

*Reference for future refreshes:* the authoritative, changing list of public HAPI servers is at
http://hapi-server.org/servers/.

---

### 18. Input File Formats (RECOMMENDED)

**Values:**
- **csv**
- **Other**

**Evidence** (read at `e990889`; `hapiclient/get.py` is unchanged since this dossier's source
revision). With the default `cache=True`, a HAPI **data** response is written to disk and then
parsed from that file, so CSV and binary are genuinely files the software reads, not only wire
formats. Since 0.3.3 those files sit in a `data/` subdirectory of the server's cache directory
(`cache.py::data_cache_paths`, which passes `endpoint='data'` to `request2path`).
- `csv` — `hapiclient/get.py::get_csv` retrieves the response to `<root>.csv`
  (`data_cache_paths(...)['csv']`) and `_parse_csv` / `_parse_csv_missing_length` read it with
  `pandas.read_csv`, falling back to `np.genfromtxt`.
- `Other` — covers the **HAPI binary transport format**, which is the package's *default*
  (`hapiopts()` sets `'format': 'binary'`) and for which the format vocabulary offers no more
  specific value. `get_binary` retrieves it to `<root>.bin` and `_parse_binary` reads it with
  `np.fromfile`/`np.frombuffer` against a dtype derived from the parameter metadata.

**`JSON` removed.** HSSI held `csv`, `JSON` and `Other` until the 0.3.3 update. `JSON` is not an
input file format of this package: JSON reaches it only as the bodies of HAPI `/catalog`, `/info`
and `/capabilities` responses, which `util.py::urlopen(..., parse_json=True)` decodes in memory with
`json.loads`; the package has no `json.load` call, so it never reads a JSON file. The `.json` copies
that `cache.py::meta_cache_write` saves are never read back — `meta_cache_read` opens only the
`.pkl` copy, at this dossier's source revision as at `e990889` — so an earlier version of this
section was wrong to rest `JSON` partly on them. Fetching data over a network API into memory is the
shape Field 18 rule 9 names as having no input file format, and rule 5's evidence is a reader that
opens the format, which this package has for CSV and binary files but not for JSON. The JSON the
package *writes* is recorded in Field 19.

**Cache files read back are not inputs either.** `Other` once also rested on the NumPy `.npy` and
pickle `.pkl` cache files that `cache.py::data_cache_read_npy` and `meta_cache_read` read back when
`usecache=True`. Those are the package reading its own saved files back, which Field 18 rule 4
excludes; they are outputs (Field 19), not input formats. Rule 4 turns on the re-reading, not on
the file: the `.npy` and `.pkl` files hold results the package already produced, whereas the `.csv`
and `.bin` files are read because they hold the server's data response, parsed there for the first
time. `Other` stands on the HAPI binary format alone.

**Why the previous "Not applicable" was wrong.** This field was once recorded as "Not applicable —
data is retrieved from servers, not read from files". That holds only when caching is disabled
(then the CSV and binary responses are parsed from in-memory buffers); caching is on by default, and
then they are read from the files they are saved to.

**Rejected:** `JSON` (above); `ascii` (`csv` is the precise term for what is parsed); and `CDF`,
`FITS`, `HDF5`, `netCDF3/4`, `IDL.sav`, `ISTP-Compliant`, `Zarr` — the package reads none of them.

---

### 19. Output File Formats (RECOMMENDED)

**Values:**
- **csv**
- **JSON**
- **Other**

**Evidence** (read at `e990889`). Every generated file goes through
`hapiclient/util.py::write_atomic`, which dispatches on suffix and writes to a temporary path before
`os.replace`. Since 0.3.3 the cache directory is laid out by endpoint (`cache.py::request2path`):
data files under `<server>/data/`, `/info` metadata under `<server>/info/`, and — new in 0.3.3 (PR
#108) — the `/catalog` and `/capabilities` responses under `<server>/catalog/` and
`<server>/capabilities/`.
- `csv` — the retrieved CSV response is written to `<root>.csv` by `util.py::urlretrieve`.
- `JSON` — `cache.py::meta_cache_write` writes the dataset metadata to `<root>.json` with
  `json.dump(data, f, indent=2)`, and since 0.3.3 the `/catalog` and `/capabilities` responses
  too.
- `Other` — the NumPy `.npy` data cache (`numpy.save`, via `cache.py::data_cache_write`), the
  pickle `.pkl` metadata caches (`pickle.dump(..., protocol=2)`), and the raw `.bin` HAPI binary
  response, none of which has a more specific value in the format vocabulary.

**Why saved responses are outputs here, not bookkeeping.** Every file above is written to the
response cache, and Field 19 rule 3 excludes internal bookkeeping — files that are not a data
product a user asks for. These are. The cache is a public, documented option: `hapi()`'s docstring
gives "`cache` (``True``) - Save responses and processed responses in cachedir", and `cachedir`
is the user's to set (by default a `hapi-data` directory under the system temporary directory,
`cache.py::cachedir`). The metadata `hapi()` returns names the saved files
for the user: `cache.py::data_cache_write` adds `x_dataFile` (the `.csv` or `.bin` response),
`x_dataFileParsed` (the `.npy` array), `x_metaFile` (the `.json` metadata) and `x_metaFileParsed`
(the `.pkl` metadata) to it. Rule 6 therefore admits them, as writes to user-facing files. Field 18
reaches the opposite verdict on the `.npy` and `.pkl` files only as *inputs*, where reading them
back is the package reading its own cache (Field 18 rule 4).

**Why the previous "Not applicable" was wrong.** This field was once recorded as no more than the
package "returns in-memory data structures". It does return NumPy arrays and dicts, but it also
writes five kinds of file to the cache directory by default.

**Rejected:** the same seven scientific formats as Field 18 — the package writes none of them, and
the earlier note that a *user* could convert the returned arrays to CDF or HDF5 with another library
describes the user's other tools, not this package's output.

---

### 20. Operating System (RECOMMENDED)
- **Operating System Independent**

**Evidence.** Pure Python with no compiled extensions and no OS-specific dependency
(`pyproject.toml`: `joblib`, `urllib3`, `numpy`, `pandas`, `isodate`). The historical Travis matrix
in `.travis.yml` exercised Linux, macOS and Windows; the code contains explicit accommodations for
all three (`cache.py::request2path` substitutes Windows-forbidden filename characters;
`util.py::warning` and `error` drop ANSI colour codes on Windows shells; `__init__.py` suppresses a
Darwin-specific urllib3/OpenSSL warning) — accommodations, not restrictions.

**Considered and rejected: additionally listing `Linux`, `Mac` and `Windows`.** Those three would be
individually defensible on the CI evidence, but `Operating System Independent` already asserts them
and mixing the two styles in one field is redundant.

---

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Evidence.** Pure Python; no architecture-specific code, no compiled extensions, no SIMD or GPU
paths. `joblib` is used only for thread-based concurrency of HTTP requests.

---

### 22. Related Phenomena (OPTIONAL)
- **Not found** — correctly empty.

**Negative research (do not re-propose).** The available phenomena values are Coronal Heating,
Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind and X-ray
emission. None applies, because `hapiclient` implements no phenomenon-specific science — it
transports and parses whatever a server returns.

The tempting entries and why they are wrong: the README's headline example retrieves the **Dst
index** (`OMNI2_H0_MRG1HR`, parameter `DST1800`), the canonical geomagnetic-storm index, which
invites `Geomagnetic Storms`; and `hapi_demo.py::cdaweb()` retrieves ACE interplanetary magnetic
field data, which invites `Solar Wind`. Both are **demonstration datasets chosen to exercise the
client**, not phenomena the software is built to study. Adding them would tell a user searching for
geomagnetic-storm software that this package does something it does not.

**Why Field 5 selects `Solar Wind` as a Region while this field rejects it as a Phenomenon — the
divergence is intentional, not an oversight.** The two fields ask different questions: Related Region
asks which regions the data a client retrieves can pertain to, and Related Phenomena asks what the
software is purpose-built to study. They also rest on different evidence here. Field 5's selection
does not depend on the demonstration data rejected above; it rests on `OMNIWeb` — a Data Source on
this record (Field 17) — being by definition an archive of near-Earth solar-wind and
interplanetary-magnetic-field data. No analogous independent argument exists for the phenomenon
reading: nothing in the package studies the solar wind, and the only evidence that would suggest
otherwise is the demonstration data already rejected. A future refresh should not treat the two
outcomes as inconsistent, nor "correct" one to match the other.

---

### 23. Development Status (RECOMMENDED)
- **Active**

**Evidence from release and commit cadence** (read 2026-10-28). Seven releases between 2026-05-02
and 2026-08-11 — v0.2.7 (2026-05-02), v0.2.8 (2026-06-04), v0.2.9 (2026-06-08), v0.3.0
(2026-07-08), 0.3.1 (2026-07-09), 0.3.2 (2026-07-22), 0.3.3 (2026-08-11) — each with a
corresponding PyPI upload and Zenodo deposit. The most recent commit on `master` is
`e990889180a80ecfb277271bff6cdb1e088521c0`, dated 2026-08-12 (21:37:09 UTC). The repository is not
archived, and the README carries no repostatus badge or status statement. Substantive work in that
window includes a packaging migration to `pyproject.toml`, a logging rework, atomic cache writes
fixing corruption from interrupted downloads (issue #94), a NumPy fallback for failed pandas CSV
reads (PR #98), caching of the `/catalog` and `/capabilities` responses (PR #108), and the addition
of PyHC compliance workflows. The PyHC registry rates the project "Good" on all six axes (community,
documentation, testing, software maturity, Python 3, license).

`Active` — "The project has reached a stable, usable state and is being actively developed." — is
exactly right: with a
last default-branch commit on 2026-08-12 and a last release on 2026-08-11, the project sits inside
Field 23 rule 6's six-month window.

---

### 24. Documentation (RECOMMENDED)
- **Value:** https://github.com/hapi-server/client-python/blob/master/README.md

**Evidence.** Verified to resolve. It is also the `docs` value in the PyHC core-packages registry,
which is the curated source for this field.

**Considered and rejected as replacements.** There is no hosted documentation site: no `docs/`
directory, no Sphinx configuration, no Read the Docs setup — API documentation exists only as
docstrings (`hapi()`'s is extensive). The three genuine supplementary resources are the Colab
notebook (https://colab.research.google.com/github/hapi-server/client-python-notebooks/blob/master/hapi_demo.ipynb),
the in-repo example script `hapi_demo.py`, and the PyHC Summer School tutorials
(https://github.com/hapi-server/tutorial-python, newly linked from the README at this revision). All
three resolve, but none is a better single documentation entry point than the README, which links to
all of them and additionally carries installation and development instructions. Field 24 accepts one
URL, so they are recorded here rather than substituted.

---

### 25. Funder (OPTIONAL)
- **Not found**

**Negative research.** No funding statement, acknowledgements section, grant number or sponsor
appears anywhere in the repository — not in `README.md`, `LICENSE.txt`, `CHANGES.txt`,
`CITATION.cff`, `.zenodo.json`, `pyproject.toml`, or any source file. DataCite returns an empty
`fundingReferences` for every DOI in the series.

**Explicitly not inferred.** The reference publication in Field 14 (the JGR HAPI standard paper) has
its own acknowledgements, but that funding supported the *standard and the collaboration*, not this
Python client, and attributing it here would be a fabrication.

---

### 26. Award Title (OPTIONAL)
- **Not found**

Follows from Field 25 — with no funder identified there is no award to record. Same negative
research applies.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Value:** https://doi.org/10.1029/2024EA003937

**Included — a third-party paper that uses this package.** Majirský, A., Mackovjak, Š., Kostárová,
S., and Amrich, S. (2025), *"Extreme Space Weather Events of the Past 30 Years: Preparation for Data
From Mission Vigil"*, **Earth and Space Science**, February 2025 (10.1029/2024EA003937). None of its
four authors is an author of this software. Describing a script the paper uses, it states: "It also
utilizes the hapiclient Python package (B. Weigel, Vandegriff, et al., 2021)." The sentence before
it credits HAPI itself, and the next one continues with what else the script employs. The paper also
says that the data its pipeline obtained for the four most extreme events it identifies are
published on Zenodo. Its reference list carries the `hapi-server/client-python` software beside the
HAPI standard paper. That is a deliberate, cited statement, in a sentence of its own, that the
paper's own software is built on this package, so Field 27 rule 5 includes it. The rule's condition
that such uses still be news holds: the works found that name the package are few, and each is
recorded in this section. The quoted sentence was confirmed in Semantic Scholar's citation context
for the paper; the surrounding text was read only in the ADS full-text index, which drops
punctuation, because the publisher's site blocks automated reading, so the section that holds the
passage was not seen there.

**The developers' HAPI-platform publications are not added — a settled decision.** Field 27 rule 3
admits, beside the developers' own publications about this software, "one by an author about the
platform the software serves". The user settled on 2026-10-29 that for this record that one is the
Field 14 reference publication, the JGR paper describing the HAPI standard, which rule 2 keeps out
of this field. The developers' other publications about HAPI are therefore not added; they belong to
the HAPI standard rather than to this client, and a Python client's record listing them would put a
platform's whole output in front of a searcher looking for the client. Weighed and excluded on that
ground (found by a creator-keyed Zenodo search for Weigel, Vandegriff and Faden on 2026-10-28):

- Posters: 10.5281/zenodo.14270996 (2024, "The HAPI Protocol: A Standard Access Mechanism for Time
  Series Data"); 10.5281/zenodo.14527276 (2024, "Impacting Open Science via Interoperable Data Access
  with the Heliophysics Application Programmer's Interface (HAPI)"); 10.5281/zenodo.15042846 (2025,
  "Simplifying Access to Space Weather Data using the HAPI Data Access Standard");
  10.5281/zenodo.21245292 (2026, GEM, "Easy Access to Heliophysics Data with HAPI" — the one that
  shows this package itself, in an example prompt asking for a script that uses `hapiclient`).
- The ESSOAr preprint 10.1002/essoar.10501378.1 (Vandegriff, Weigel, Faden et al., posted
  2019-12-12, "Interoperability for Heliophysics and Planetary Time Series Data via HAPI"), which
  also appears among Jon Vandegriff's ORCID works.
- The working paper 10.5281/zenodo.4752107 (2021, "A Plan for Further Promulgation and Development of
  the Heliophysics Application Programmer's Interface (HAPI)") and the HAPI 3.3.1 specification
  deposit 10.5281/zenodo.17516129 (2025).
- Talk decks: 10.5281/zenodo.8422472 (2023, "HAPI - A Standard Time Series Data Access API for
  Heliophysics and Planetary Data"), 10.5281/zenodo.11114385 (2024, "HAPI: The story of a uniform
  data access mechanism built in Heliophysics …"), 10.5281/zenodo.17387480 (DASH 2025,
  "Interoperable Heliophysics Data Access via HAPI"), 10.5281/zenodo.17421195 (2025, "Issues Related
  to Metadata and Metadata Standards Identified while Developing the HAPI Specification and Using
  HAPI Data"), 10.5281/zenodo.21793481 (COSPAR 2026, "Efficient Space Weather Data Access Using
  HAPI"), 10.5281/zenodo.23088029 (2026, "Making Ground Data Discoverable: Mapping from HAPI to
  SPASE 2") and 10.5281/zenodo.23144432 (DASH 2026, "Future Directions for the HAPI
  Specification").

The same search found deposits that mention HAPI but are about other subjects, so they are neither
about this software nor about its platform: 10.5281/zenodo.15632921 and 10.5281/zenodo.17457042
("A Standard for Units in Heliophysics", a units recommendation drawn up by the HAPI, SPASE and ISTP
metadata groups) and 10.5281/zenodo.18749828 ("HDRL Show and Tell: Community Connections and
Operations", a set of short talks of which one covers HAPI).

**Corrected negative research — the ESSOAr preprint.** An earlier version of this section rejected
the ESSOAr item partly because "its DOI no longer resolves in DataCite". That was wrong: it is a
Crossref DOI, for a posted-content preprint, and it resolves (to essopenarchive.org). It is excluded
on the platform ground above instead.

**Also weighed and not added.**
- Grimes, E. W., et al. (2022), "The Space Physics Environment Data Analysis System in Python",
  *Frontiers in Astronomy and Space Sciences* (10.3389/fspas.2022.1020815). Its abstract names
  `hapiclient` in a list of the open-source projects PySPEDAS is built from ("PyTplot, cdflib,
  hapiclient, etc.") — a dependency mention, which rule 6 excludes.
- MacDonald, E., et al. (2026), "Crowdsourced aurora observations during geomagnetic superstorms:
  the Aurorasaurus open science database", *Frontiers in Astronomy and Space Sciences*, 2026-10-09
  (10.3389/fspas.2026.1883317). Its methods state that "The entire workflow was implemented in
  Python using supporting scientific libraries", then list seven — pandas, matplotlib, aacgmv2,
  hapiclient, cartopy, seaborn and spacy — citing the v0.2.7 software deposit
  (10.5281/zenodo.19980024) for hapiclient. That is a list of tools, which rule 6 excludes. Unlike
  the Vigil paper, it never says what hapiclient does in the workflow.
- The 2022 *Frontiers* paper on VirES for Swarm (10.3389/fspas.2022.1002697, "Python tools for
  ESA’s Swarm mission: VirES for Swarm and surrounding ecosystem") says its own client is "very
  similar in usage pattern and ethos to broader data access libraries such as hapiclient" and cites
  the concept DOI. A comparison in background text is a mention (rule 6).
- Barnum, J., et al. (2023), "Python in Heliophysics Community (PyHC): Current status and future
  outlook", *Advances in Space Research* (10.1016/j.asr.2022.10.006). An ecosystem review whose
  reference list cites the v0.2.1 software deposit; none of its authors is an author of this
  software, and it reports no results built with the package (rule 6).
- The COSPAR 2026 meeting abstract "Efficient Space Weather Data Access Using HAPI" (ADS
  2026cosp...46.3461V). A meeting abstract is never an eligible publication (rule 1); its talk deck is
  the 10.5281/zenodo.21793481 entry above.

**Search recorded (2026-10-28).** ADS full-text searches for `hapiclient`, for `"HAPI client"`, and
for `client-python` with `hapi`, restricted to records entered since 2026-08-04, returned nothing;
the controls `sunpy` and `pyspedas` over the same window returned hits, and a nonsense token
returned none. Over all records, the `hapiclient` full-text search returned the Vigil and PySPEDAS
papers, and an acknowledgements search for `hapiclient` and a full-text search for the concept DOI
returned nothing. An OpenAlex full-text search (`fulltext.search:hapiclient`, 2026-10-29) returned
four works: the Vigil, PySPEDAS, Aurorasaurus and VirES papers; the controls `sunpy` and `pyspedas`
returned hits the same day, and a nonsense token returned none. The PyHC review was found through
its citation of the v0.2.1 deposit. DataCite reports no citations of the concept DOI. The repository
cites no publications, and the JGR HAPI standard paper is recorded in Field 14, not here. This field
was recorded as empty before the 0.3.3 update.

---

### 28. Related Datasets (OPTIONAL)
- **Not found**

**Negative research.** The package supports no particular dataset; it retrieves whatever a HAPI
server offers. The dataset identifiers appearing in `hapi_demo.py` (`OMNI2_H0_MRG1HR`, `AC_H0_MFI`,
`ace`, `sme_ssi`, `dataset1`) are demonstrations spread deliberately across four different servers to
exercise the client, not datasets it is built for, and none has a DOI cited in the repository.
Listing any of them would misrepresent a generic client as dataset-specific.

---

### 29. Related Software (OPTIONAL)
- **hapiplot** — https://github.com/hapi-server/plot-python

**Evidence.** The companion visualization package, written and maintained by the same project. The
README documents installing it (`pip install hapiplot --upgrade`) and every plotting example in
`hapi_demo.py` calls `hapiplot(data, meta)` on this package's output. `hapiclient/data.py` even
annotates its returned metadata with `x_server` and `x_dataset` keys whose in-code comment says they
"will also be used for labeling plots by hapiplot()" — a deliberate accommodation of the companion.

**Considered and rejected.**
- The HAPI **data specification** (https://github.com/hapi-server/data-specification), referenced
  throughout `hapiclient/hapi.py`'s docstring and the README. It is a specification document, not
  software.
- The HAPI **server list** repository (https://github.com/hapi-server/servers), fetched at runtime by
  `servers.py`. It is a text file of URLs, not software.
- `numpy`, `pandas`, `isodate`, `joblib`, `urllib3` — runtime dependencies from `pyproject.toml`, all
  generic scientific-Python or HTTP/concurrency infrastructure. Being a dependency is not being
  related software, and each would read identically for most of the Python ecosystem.

---

### 30. Interoperable Software (OPTIONAL)
- **hapiplot** — https://github.com/hapi-server/plot-python

**Evidence of a demonstrated exchange.** `hapiplot(data, meta)` consumes this package's exact return
pair — the NumPy structured array and the metadata dict — unmodified. The exchange runs in both
directions in the source: `hapiclient/hapi.py::hapiopts` documents itself as "Used by hapiplot() and
hapi()", and `hapiclient/data.py` injects `x_server` / `x_dataset` into the metadata specifically for
hapiplot's plot labelling. This is a companion package with a shared data model, which is the
paradigm case for this field.

**Considered and rejected.**
- `astropy` — the README's "Data Model and Time Format" section lists "Creating an Astropy NDArray"
  among the notebook's examples. Rejected: astropy is not a dependency, `hapiclient` exposes no
  astropy adapter, and the "exchange" amounts to constructing an astropy object from a plain NumPy
  array, which is true of anything that returns NumPy arrays.
- `pandas` — used internally for fast CSV parsing and `to_datetime` conversion, and the README notes
  the returned data can be put in a `DataFrame`. Excluded: generic infrastructure, and a dependency
  rather than a peer tool.
- `numpy`, `isodate`, `joblib`, `urllib3` — same reason; all would be equally at home in a web
  application or a finance model.
- PyHC membership on its own — this package is a PyHC core package, but ecosystem membership is not
  a demonstrated interoperation with any particular package.

---

### 31. Related Instruments (OPTIONAL)
- **None** — correctly empty, by design.

**This is a deliberate, evidence-backed omission, not a gap.** `hapiclient` is instrument-agnostic in
the strongest sense: the package contains **no instrument-specific code of any kind**. Its data
handling is driven entirely by the `parameters` array in whatever metadata the server returns —
`get.py::_compute_dt` builds the NumPy dtype from the server-declared `type`, `size` and `length`
fields, and nothing anywhere branches on an instrument, a mission or a dataset identifier. The
relevance test fails at the first stage: a user searching HSSI for a specific instrument would not
expect a generic protocol client back, and nothing in the package helps with one instrument more than
another. Because no candidate passes the relevance gate, no SPASE resolution is required, and there
is no ambiguity to escalate.

**Specifically rejected, so a future agent does not mine them out of the demo file.**
`hapi_demo.py::cdaweb()` requests `AC_H0_MFI` parameters `Magnitude,BGSEc` — ACE/MAG level-2
data — and `hapi_demo.py::lisird()` requests `sme_ssi` (Solar Mesosphere Explorer solar spectral
irradiance). Both are **demonstration name-drops**, exactly the category the relevance gate
excludes: they exist to show that the client works against four different servers, and swapping them
for any other dataset would require no code change.

**This field records only instruments carrying a canonical `https://spase-metadata.org/`
identifier.** No candidate here has one that is uniquely justified, and none needs one, because none
passes the relevance gate. The field is therefore correctly empty; an instrument name without a
canonical SPASE identifier is never recorded.

---

### 32. Related Observatories (OPTIONAL)
- **None** — correctly empty, by design.

**Same reasoning as Field 31.** The package supports no mission or observatory in particular; it
supports the HAPI protocol, and therefore every server that speaks it equally.

**Previous incorrect entries, corrected.** "OMNI" and "CDAWeb" were once listed here as bare prose
names. Both were wrong on two independent counts:
1. **Neither is an observatory.** CDAWeb is NASA's multi-mission data archive and belongs in Field 17
   (Data Sources), where it is recorded. OMNI is a merged multi-spacecraft solar-wind dataset, not a
   platform; its archive, OMNIWeb, is likewise recorded in Field 17.
2. **Neither had a SPASE identifier.** This field records only entries carrying a canonical
   `https://spase-metadata.org/` identifier; a bare name is never recorded. Do not reintroduce
   either entry in any form.

The `hapi_demo.py::sscweb()` demo requests the SSCWeb dataset named `ace`, which superficially names
a mission. That is a demonstration name-drop and is rejected for the same reason as the instruments
in Field 31; SSCWeb itself is recorded as a Data Source in Field 17.

---

### 33. Logo (OPTIONAL)
- **Value:** https://hapi-server.org/logos/HAPI-large.png

**Evidence.** The HAPI project logo, served from the project's own site; verified to resolve.

**Previous value and why it was replaced.** The record originally carried the PyHC registry's SVG,
`https://raw.githubusercontent.com/hapi-server/hapi-server.github.io/master/logos/HAPI.svg` (which
also still resolves). It was replaced with the PNG by a deliberate curator decision. The PyHC
registry still lists the SVG, so a naive PyHC-priority refresh would revert this — **do not.**

---

## Cross-Cutting Notes

**PyHC registry.** This package is listed in the PyHC **core** packages registry
(`_data/projects_core.yml`) as `name: "HAPI Client"`, with `contact: "Bob Weigel"`,
`keywords: ["data_retrieval","line_plots","plotting","spectra"]`, `docs` and `code` both pointing at
this repository, `logo` pointing at the SVG, and "Good" ratings on all six quality axes. PyHC is the
highest-priority source for the software name, documentation URL and keywords — with two documented
exceptions above, in both of which HSSI deliberately departs from PyHC: the logo (Field 33, replaced
with the PNG) and PyHC's three plotting keywords `line_plots`, `plotting` and `spectra` (Field 16,
absent because they describe the companion `hapiplot` package rather than `hapiclient`). Meeting
either in the registry on a later pass is expected and is not grounds to adopt it.

**Sources that are known to be wrong, collected in one place.** A future agent re-deriving this
record will meet all of these and should not "fix" HSSI from them:
- `.zenodo.json` — hard-codes `publication_date: 2021-10-06` and `license: "other-open"` for every
  deposit, and titles the software `"hapi-server/client-python:"` with a trailing colon. Zenodo and
  DataCite reproduce all three verbatim.
- `CITATION.cff` — `family-names`/`given-names` swapped, `cff-version: 0.2.1` (not a CFF schema
  version), `version: v0.2.1` and `date-released: 2021-10-06`, both long superseded.
- DataCite creator record for the version DOI — `familyName: "Bob Weigel"` with no given name.
- GitHub release `prerelease` flags — always `false`, including for betas, because the `Makefile`'s
  `gh release create` never passes `--prerelease`.
- `.travis.yml` — still present and still referenced by the README's build badge, but it invokes
  `tox -e short-test`, an environment that no longer exists in `tox.ini`. The live CI is
  `.github/workflows/pyhc-actions.yml`.

**ORCID coverage.** Three of the four authors have ORCIDs (Weigel, Faden, Vandegriff). Only Hari
Narayana Batta remains without one, and searching has established that no matching public record
exists.

**Reference publication.** The project has a genuine standard-describing paper (Field 14) but no
software paper (JOSS or equivalent). That is a fact about the project, not a gap in this record.
