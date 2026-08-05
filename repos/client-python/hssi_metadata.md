# HSSI Metadata Extraction Results

**HSSI Software ID:** f6e3429d-e80e-4cf6-889e-44af1e93f87d
**Repository:** https://github.com/hapi-server/client-python
**Source Revision:** aafecdb33f528c45304d8f1a33f405893f6dc842
**Extraction Date:** 2026-08-04
**Validation Date:** 2026-08-04
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
has moved to `.github/workflows/pyhc-actions.yml`, and `misc/` now holds the release tooling. Six
releases shipped between 2026-05-02 and 2026-07-22.

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
`conceptdoi` by every Zenodo version record in the series, and currently resolves to the 0.3.2
version record.

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
  and writes `.npy`/`.pkl` cache files (`hapiclient/util.py::write_atomic`), but that is an internal
  caching mechanism, not a user-facing conversion feature: there is no API by which a user asks
  hapiclient to convert file A into file B. The formats involved are recorded in Fields 18 and 19
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

- **Version Number:** 0.3.2
- **Version Date:** 2026-07-22
- **Version PID:** https://doi.org/10.5281/zenodo.21496990
- **Version Description:** Suppresses the spurious pandas "Could not infer format" warning raised when parsing HAPI timestamps (issue #103, PR #104); adopts standard-library logging practice, with a NullHandler and application-controlled propagation, in place of unconditionally disabled propagation; and migrates packaging from setup.py to pyproject.toml.

**Previous value:** `v0.2.9` (released 2026-06-08). Superseded — six releases have shipped since,
ending at 0.3.2.

**Why 0.3.2 and not 0.3.3b0.** Both tags exist, both have GitHub releases, and — confusingly — the
`0.3.3b0` GitHub release was published thirty seconds *before* the `0.3.2` release, with its
`prerelease` flag set to false. None of that makes it the current release:

1. **The project's own release process says `b` versions are not releases.** The `Makefile` header
   documents two separate procedures. Under "Beta versions" it states in the heading:
   *"Beta versions (not released to pypi.org)."* Under "Releases" step 1 is *"Remove the 'b' in the
   version in CHANGES.txt"*, and step 4 is to create the **next** `b0` version and commit it, which
   "will update the version information in the repository to indicate it is now in a pre-release
   state." `0.3.3b0` at `HEAD` is precisely that post-release development marker — set by commit
   `fbcfe2f`, "Update version for next release", made two minutes after the 0.3.2 release commit.
2. **`0.3.3b0` was never published to PyPI.** The PyPI project's newest release is `0.3.2`
   (sdist uploaded 2026-07-22T16:06:10Z); there is no `0.3.3b0` file at all.
3. **The `prerelease=false` flag is a tooling artifact, not a statement.** The `gh-release` target
   is `gh release create $(VERSION) --target master --notes "Release $(VERSION)" --title "Release
   $(VERSION)"` — it never passes `--prerelease`, so *every* GitHub release this project has ever
   made reports `prerelease=false`, betas included. The flag carries no information here.
4. **Zenodo's concept DOI resolves to 0.3.2.** Zenodo minted version DOIs for both
   (`10.5281/zenodo.21496985` for 0.3.3b0, `10.5281/zenodo.21496990` for 0.3.2), and the concept DOI
   `10.5281/zenodo.5553155` currently resolves to the 0.3.2 record.

**`0.3.2`, bare, is the exact version string.** It is `__version__` in `hapiclient/__init__.py` at
the release commit, the PyPI release name, the GitHub release tag, and DataCite's `version`
attribute. The version is that number alone — never `v`-prefixed, and never combined with the
software name.

**Tag-naming inconsistency, for future reference.** Each release produces **two** git tags, because
`make version-tag` runs `git tag -a v$(VERSION)` while `make gh-release` runs
`gh release create $(VERSION)` with the bare number. Both `v0.3.2` and `0.3.2` therefore point at
commit `ff91cda93e578bffa996ea827d781d6de4d86d7f`. Older releases (through `v0.3.0`) have only the
`v`-prefixed tag because the GitHub releases for them were made by hand. Do not read the duplication
as two different releases.

**Version Date — 2026-07-22, corroborated four ways.** The `0.3.2` tag commit `ff91cda` is dated
2026-07-22 12:05:38 -0400 (16:05:38 UTC); the GitHub release was published 2026-07-22T16:05:41Z; the
Zenodo version record was created 2026-07-22T16:05:46Z; the PyPI sdist was uploaded
2026-07-22T16:06:10Z. All four fall within 35 seconds of one another on the same UTC day.

**Version PID — verified, and Zenodo's own metadata for it is partly wrong.** The Zenodo version
record 21496990 carries `version: "0.3.2"` and `conceptdoi: 10.5281/zenodo.5553155`, which fixes the
mapping unambiguously. But that same record reports `publication_date: 2021-10-06` and
`license: other-open`, and DataCite mirrors both (`publicationYear: 2021`, `dates: [{2021-10-06,
Issued}]`, `rightsList: [Other (Open)]`). **Both are Zenodo-side errors inherited verbatim from the
repository's hand-maintained `.zenodo.json`, which hard-codes a 2021 publication date and
`"license": "other-open"` for every deposit in the series.** The Version Date above and the License
in Field 15 are therefore derived from the repository and the release artifacts, not copied from the
DOI record. Anything auto-filled from this DOI must be re-checked against the repository.

**Version Description sourcing.** `CHANGES.txt` gives a single line for v0.3.2
("Date parsing warning https://github.com/hapi-server/client-python/pull/104") and the GitHub release
body is the auto-generated "Release 0.3.2", so neither alone is a usable summary. The description
above is that line expanded with the verifiable `0.3.1..0.3.2` source diff: the
`warnings.catch_warnings()` filter added in `hapiclient/hapitime.py::hapitime2datetime`, the
NullHandler/propagation rework in `hapiclient/log.py`, and the deletion of `setup.py` in favour of
`pyproject.toml`.

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
3. **No supported Python floor admits Python 2.** `pyproject.toml` at `HEAD` declares
   `requires-python = ">=3.8"`; the released 0.3.2 declared `>=3.5`. Neither permits 2.x. (The
   `>=3.5` visible on PyPI is the 0.3.2 sdist's metadata, not stale data — the bump to `>=3.8`
   landed after that release and will first appear on PyPI with 0.3.3.)
4. **No test target is Python 2.** `tox.ini` `envlist = py38,py39,py310,py311,py312,py313,py314`;
   the `py27` environment that once justified this value is gone. `.travis.yml` runs Python 3.8
   only, and `.github/workflows/pyhc-actions.yml` runs the PyHC PHEP 3 and environment-compatibility
   checks.
5. **Python-3-only syntax makes the package uncompilable under Python 2.** `hapiclient/util.py`
   uses f-strings at lines 478, 515, 518 and 522 (in `write_atomic`), and `hapiclient/data.py`
   uses one at line 25 (`log(f'Using STOP = {STOP}')`). f-strings are a **parse**-time construct,
   so either module alone is a `SyntaxError` under Python 2 regardless of whether the enclosing
   function is ever called. `hapiclient/data.py` is reached from the public `hapi()` entry point,
   so the package cannot even be imported under Python 2.

**The counter-evidence, and why it does not save the value.** Four `sys.version_info` guards
survive in the source: `hapiclient/__init__.py` (`if sys.version_info[0] < 3: reload(sys)`),
`hapiclient/get.py` line 148, `hapiclient/data.py` line 239 (`if sys.version_info < (3, ):`), and a
`<= (3, 5)` branch in `hapiclient/util.py::unicode_error_message`. The first three are **unreachable
dead code** — they can never execute, because the module graph fails to compile under Python 2 — and
the fourth is a Python 3.5 check, not a Python 2 one. Vestigial compatibility branches are evidence
of history, not of support.

**Not selected:** any other programming language. `Python 3.x` is the only applicable value — the
package is pure Python; there are no compiled extensions, no bundled C/Fortran, and no other
language in the source tree.

---

### 14. Reference Publication (RECOMMENDED)
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

**Considered and rejected:** `cdaweb`, `omniweb`, `sscweb` (duplicate Field 17);
`csv`, `json` (duplicate Fields 18/19); `data access` (a synonym of the recorded `data_retrieval` —
note that `data_retrieval` and `data retrieval` are two distinct terms in the keyword vocabulary, and
the underscore form recorded here, which is the form PyHC uses, is the correct one for this record);
`space physics` (a synonym of the recorded `heliophysics`).

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
- **JSON**
- **Other**

**Evidence.** With the default `cache=True`, a HAPI response is written to disk and then parsed from
that file, so these are genuinely files the software reads, not only wire formats.
- `csv` — `hapiclient/get.py::get_csv` retrieves the response to `<root>.csv`
  (`data_cache_paths(...)['csv']`) and `_parse_csv` / `_parse_csv_missing_length` read it with
  `pandas.read_csv`, falling back to `np.genfromtxt`.
- `JSON` — HAPI `/catalog`, `/info` and `/capabilities` responses are parsed as JSON
  (`util.py::urlopen(..., parse_json=True)`, `util.py::jsonparse`), and the cached `.json` metadata
  file written by `cache.py::meta_cache_write` is read back on a later run.
- `Other` — covers the **HAPI binary transport format**, which is the package's *default*
  (`hapiopts()` sets `'format': 'binary'`) and for which the format vocabulary offers no more
  specific value. `get_binary` retrieves it to `<root>.bin` and `_parse_binary` reads it with
  `np.fromfile`/`np.frombuffer` against a dtype derived from the parameter metadata. `Other` also
  covers the NumPy `.npy` and pickle `.pkl` cache artifacts read back by
  `cache.py::data_cache_read_npy` and `meta_cache_read`.

**Why the previous "Not applicable" was wrong.** This field was once recorded as "Not applicable —
data is retrieved from servers, not read from files". That is only true when caching is disabled;
caching is on by default, and even with it off the package still parses CSV, JSON and binary
payloads.

**Rejected:** `ascii` (`csv` is the precise term for what is parsed), and `CDF`, `FITS`, `HDF5`,
`netCDF3/4`, `IDL.sav`, `ISTP-Compliant`, `Zarr` — the package reads none of them.

---

### 19. Output File Formats (RECOMMENDED)

**Values:**
- **csv**
- **JSON**
- **Other**

**Evidence.** Every generated file goes through `hapiclient/util.py::write_atomic`, which dispatches
on suffix and writes to a temporary path before `os.replace`:
- `csv` — the retrieved CSV response is written to `<root>.csv` by `util.py::urlretrieve`.
- `JSON` — `cache.py::meta_cache_write` writes the dataset metadata to `<root>.json` with
  `json.dump(data, f, indent=2)`.
- `Other` — the NumPy `.npy` data cache (`numpy.save`, via `cache.py::data_cache_write`), the
  pickle `.pkl` metadata caches (`pickle.dump(..., protocol=2)`), and the raw `.bin` HAPI binary
  response, none of which has a more specific value in the format vocabulary.

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

**Evidence from release and commit cadence.** Six releases in under three months —
v0.2.7 (2026-05-02), v0.2.8 (2026-06-04), v0.2.9 (2026-06-08), v0.3.0 (2026-07-08),
0.3.1 (2026-07-09), 0.3.2 (2026-07-22) — each with a corresponding PyPI upload and Zenodo deposit.
The most recent commit on `master` is 2026-07-22. Substantive work in that window includes a
packaging migration to `pyproject.toml`, a logging rework, atomic cache writes fixing corruption
from interrupted downloads (issue #94), a NumPy fallback for failed pandas CSV reads (PR #98), and
the addition of PyHC compliance workflows. The PyHC registry rates the project "Good" on all six
axes (community, documentation, testing, software maturity, Python 3, license).

`Active` — "reached a stable, usable state and being actively developed" — is exactly right.

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
- **Not found**

**Negative research.** The repository cites no publications. The only publication tied to this
software is the JGR HAPI standard paper, and it is already recorded in Field 14 (Reference
Publication), so listing it again here would duplicate it.

One candidate was investigated and rejected: the 2019 ESSOAr item "Interoperability for Heliophysics
and Planetary Time Series Data via HAPI" (10.1002/essoar.10501378.1), found via the ORCID record of
author Jon Vandegriff. It is not cited anywhere in this repository, its DOI no longer resolves in
DataCite, and its subject is the HAPI standard rather than this client — the same ground the Field 14
paper covers authoritatively.

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
