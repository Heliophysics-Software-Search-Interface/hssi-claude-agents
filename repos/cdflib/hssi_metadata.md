# HSSI Metadata Extraction Results

**HSSI Software ID:** 11cb7b68-cfe7-4d6c-84ed-af5ab071e74c
**Repository:** https://github.com/lasp/cdflib
**Source Revision:** a5362441980ad8d740c647a77527b05c41195eed
**Extraction Date:** 2026-07-29
**Validation Date:** 2026-07-30
**Validation Status:** PASS
**Final HSSI state:** Fields 2–33 match the validated values in this file.

**Seed:** The existing HSSI record. No prior canonical `hssi_metadata.md` existed. Every field below
is either a preserved submitted value or an evidence-backed correction. Controlled-list values were
confirmed against the live HSSI vocabularies.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Note: Submitter details are not exposed in the public software view.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.1481144

*Source: preserved from existing HSSI record. Verified via DataCite: this is the Zenodo **concept
(all-versions) DOI** — `versionOfCount` is 0, it carries only `HasVersion` relations to the ten
version DOIs, and Zenodo reports `conceptrecid = 1481144`. The correct value for this field; no change.*

*Note (upstream, not an HSSI error): the GitHub-Zenodo archiving hook stopped producing deposits
after version 0.4.7 (2022-08-19), so the concept DOI's landing page still shows title
`MAVENSDC/cdflib:` and version 0.4.7, and `https://zenodo.org/badge/latestdoi/102912691` still
resolves to `10.5281/zenodo.7011489` (0.4.7). Consequently no version-specific DOI exists for 1.3.12
— see Field 12. Worth reporting to the maintainers; nothing to fix in HSSI.*

### 3. Code Repository (MANDATORY)
https://github.com/lasp/cdflib

*CHANGED. Old: `https://github.com/MAVENSDC/cdflib`. Evidence: the old URL permanently redirects
to `https://github.com/lasp/cdflib`; the GitHub API reports `full_name = lasp/cdflib`,
`fork = false`, `archived = false`, default branch `main`; `pyproject.toml` declares
`[project.urls] Homepage = "https://github.com/lasp/cdflib"`; `mkdocs.yml` declares
`repo_url: https://github.com/lasp/cdflib`; every README badge targets `lasp/cdflib`; and the local
clone's `origin` is `https://github.com/lasp/cdflib.git`. The repository moved GitHub organizations
from MAVENSDC to lasp; the stored URL is the pre-move location.*

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing

*CHANGED (replacement). Old: `Servers and Environments: Distribution/Access` only. Every value above
was confirmed byte-for-byte against the live `FunctionCategory` vocabulary, and every
`Parent: Child` value has its bare parent top-level category present as its own separate entry.*

*The former value was removed because no repository evidence supported it:
cdflib is a client-side file-format library with no server, service, or distribution component. Its
only remotely related capability — remote/cloud-aware reading — is captured far more precisely by
`Data Processing and Analysis: Data Access and Retrieval`. Its bare parent `Servers and Environments`
was removed with it, since it existed solely to satisfy the parent-inclusion rule for that child.*

Per-value evidence:
- **Data Processing and Analysis** — required bare parent for the three children below.
- **Data Processing and Analysis: File Format Conversion** — the library's central capability.
  `cdflib/cdfread.py` (`CDF` class) parses the CDF binary format directly and `cdflib/cdfwrite.py`
  writes CDF version 3 files; `cdflib/xarray/cdf_to_xarray.py` and `cdflib/xarray/xarray_to_cdf.py`
  provide public `cdf_to_xarray()` / `xarray_to_cdf()` converters (documented in `docs/xarray.md`),
  and `xarray_to_cdf`'s docstring documents an explicit "netCDF -> CDF conversion" workflow.
  `cdflib/epochs.py` (`CDFepoch`) and `cdflib/epochs_astropy.py` (`CDFAstropy`) convert between the
  CDF time types (CDF_EPOCH, CDF_EPOCH16, CDF_TT2000) and ISO 8601, `numpy.datetime64`, Unix
  timestamps, broken-down date components and `astropy.time.Time`.
- **Data Processing and Analysis: Data Access and Retrieval** — `CDF.__init__` in
  `cdflib/cdfread.py` dispatches on the path scheme: `s3://` paths are read through `boto3` and
  `cdflib/s3.py`'s `S3object` (three selectable read strategies, including chunked HTTP byte-range
  reads), and `http://`/`https://` paths are fetched with `urllib.request`. Users retrieve remote
  CDFs by passing a URL, and `varget(..., startrec=, endrec=)` plus `CDFepoch.findepochrange()`
  retrieve selected record ranges rather than whole files.
- **Data Processing and Analysis: Processing** — the core read/write path performs a real
  transformation chain rather than raw byte handoff. In `cdflib/cdfread.py`: whole-file and
  per-variable GZIP decompression (`_uncompress_file`, `cdflib/_gzip_wrapper.py`) and RLE
  decompression (`_uncompress_rle`), optional MD5 checksum validation (`_md5_validation`,
  `CDF(validate=True)`), endianness/encoding conversion (`_endian`, `_convert_option`), CDF-type to
  NumPy dtype mapping, and record/dimension reconstruction. `cdflib/cdfwrite.py` performs the inverse
  encoding/endianness conversion and NumPy-dtype to CDF-type mapping on write (`_datatype_size`, the
  `value.dtype.type` dispatch, its own `_convert_option`, and inline endianness selection). Separately, the optional xarray adapter adds FILLVAL
  substitution and dtype negotiation of its own — `_convert_fillvals_to_nan` (the `fillval_to_nan`
  option) in `cdflib/xarray/cdf_to_xarray.py`, and `_dtype_to_cdf_type`, `_convert_nans_to_fillval`
  and `_variable_compression` in `cdflib/xarray/xarray_to_cdf.py`. Note these four are
  adapter-only: the core `cdfread.py`/`cdfwrite.py` modules contain no FILLVAL handling at all.
Considered and deliberately excluded (audit trail):
- `Servers and Environments: Distribution/Access` and its bare parent `Servers and Environments` —
  the previously stored value, removed as described above.
- `Data Processing and Analysis: Analysis` — cdflib computes no derived physical or statistical
  quantities; it is I/O and representation only.
- `Data Processing and Analysis: Time Series Analysis` — `findepochrange` / `epochrange_*` locate the
  record index range covering a time window, which is time-based subsetting, not temporal analysis.
  A user searching HSSI for time-series analysis tools would not want cdflib.
- `Data Processing and Analysis: Data Reduction` — GZIP/RLE are lossless container compression, not
  averaging, binning or downsampling.
- `Data Processing and Analysis: Packet Decommutation` — the binary parsing is of on-disk CDF
  internal records (CDR/GDR/VDR/VXR/VVR/ADR/AEDR), not spacecraft telemetry packets.
- `Data Processing and Analysis: Calibration` — no calibration, response or unit conversion.
- `Data Visualization` and children — no plotting API. `_find_xarray_plotting_values` only copies
  ISTP attributes into the xarray attribute names that *xarray's own* plotting routines read;
  `matplotlib` appears solely in the `dev` extra.
- `Coordinate Transforms` and children — none. Coordinate-system names (GSE/GSM/RTN) appear only
  inside test-fixture variable names; the library performs no transforms.
- `Mission-related` and children — cdflib is a general-purpose format library, not part of any
  mission ground system, despite its MAVEN SDC / LASP heritage.
- `Servers and Environments: Software or Environment Container` — `.devcontainer/Dockerfile` is a
  contributor development environment, not a distributed container product.

### 5. Related Region (MANDATORY)
Not found

*The former values `Earth Magnetosphere`, `Interplanetary Space` and `Planetary Magnetospheres` were
removed because none describes cdflib's functionality. This is not an extraction gap; the field is
intentionally empty.*

*Rationale. Field 5 asks for "the physical region the software supports **science functionality**
for." cdflib has no science functionality tied to any region — it reads and writes a file format.
Every region value is therefore a false membership in a browse facet: a user filtering for
`Earth Magnetosphere` wants magnetosphere science tools, and a byte-level format library appearing
there costs trust in the filter. That is the same standard applied to Fields 18/19, where `netCDF3/4`
was declined because cdflib cannot open a netCDF file.*

*The three former values are all members of the legacy five-item Region list
(`Earth Atmosphere`, `Earth Magnetosphere`, `Interplanetary Space`, `Planetary Magnetospheres`,
`Solar Environment`) that once comprised the selectable vocabulary. The stored trio reflected that
old coarse dropdown rather than documented region-specific functionality.*

*Although the field is labelled mandatory, no region applies to a format library. An empty Region is
also established practice for format and infrastructure tooling — the closest analog in HSSI,
`sammi-cdf` (a Python package for CDF/ISTP metadata management, with the same `CDF` +
`ISTP-Compliant` input and output formats as cdflib), carries no region at all.*

*Also excluded for the same reason: `Earth Atmosphere` (suggested by the PyHC
`ionosphere_thermosphere_mesosphere` tag and the DE-2 RPA / FAST / SABER-TIMED / M-GITM test
fixtures), plus `Earth Ionosphere`, `Earth Thermosphere`,
`Earth Lower and Middle Atmosphere`, `Solar Wind`, `Solar Environment` and `Mars Magnetosphere`. The
mission files under `tests/testfiles/` and the remote-data test corpus were chosen to exercise
structural variety in CDF files; they are not regions the software supports science functionality for.*

*Note for HSSI maintainers (not actionable in this record): a MANDATORY Region field is a poor fit
for format and infrastructure libraries, which have no region by construction and no `Not
applicable` row to select.*

### 6. Authors (MANDATORY)
The complete stored 15-author set is retained in its established order.

1. **Sandy Antunes** — Identifier: Not found — Affiliation: Project Calliope (no ROR)
2. **Julie Barnum** — Identifier: Not found — Affiliation: Not found
3. **Angeline Burrell** — https://orcid.org/0000-0001-8875-9326 — Affiliation: United States Naval Research Laboratory (https://ror.org/04d23a975)
4. **Bryan Harter** — https://orcid.org/0000-0002-3908-9001 — Affiliation: Laboratory for Atmospheric and Space Physics (https://ror.org/01fcjzv38)
5. **Htyeim** *(given name empty in HSSI)* — Identifier: Not found — Affiliation: Not found
6. **Jack Ireland** — https://orcid.org/0000-0002-2019-8881 — Affiliation: Goddard Space Flight Center (https://ror.org/0171mag52)
7. **Alexis Jeandet** — https://orcid.org/0000-0003-2892-6924 — Affiliation: Laboratory of Plasma Physics (LPP/CNRS) (https://ror.org/05c95bg36)
8. **Hugo van Kemenade** — https://orcid.org/0000-0001-5715-8632 — Affiliation: Nord Software (no ROR)
9. **P. L. Lim** — Identifier: Not found — Affiliation: Space Telescope Science Institute (https://ror.org/036f5mx38)
10. **Scivision** *(given name empty in HSSI)* — Identifier: Not found — Affiliation: Not found
11. **Jonathon Smith** — Identifier: Not found — Affiliation: Not found
12. **David Stansby** — https://orcid.org/0000-0002-1365-1908 — Affiliations: Advanced Research Computing Centre, University College London, UK (no ROR); Department of Mechanical Engineering, University College London (no ROR); Imperial College London (https://ror.org/041kmwe10); Mullard Space Science Laboratory, University College London (no ROR); University College London (https://ror.org/02jx3x895)
13. **Supervised** *(given name empty in HSSI; not a personal name)* — Identifier: Not found — Affiliation: University of California, Los Angeles (https://ror.org/046rm7j60)
14. **Jan Christoph Terasa** — Identifier: Not found — Affiliation: IEAP University Kiel (no ROR)
15. **Andreas J. Weiss** — Identifier: Not found — Affiliation: Not found

*All 15 entries preserve the stored given/family names, identifiers and affiliation organizations.*

*Creator considered but not added:*
- **MAVEN SDC** *(organization author)* — Affiliation: Laboratory for Atmospheric and Space Physics
  (https://ror.org/01fcjzv38); no identifier, since a ROR lookup for "MAVEN Science Data Center"
  returns no matching organization. This is the one Zenodo creator absent from HSSI: the concept DOI's
  creator list contains 16 entries and HSSI stores 15, the difference being this organizational
  creator. It remains outside the numbered list so that the list reflects the stored author set.

**Hugo van Kemenade — verified identity.** The stored identifier
`https://orcid.org/0000-0001-5715-8632` is confirmed by the ORCID registry:
`pub.orcid.org/v3.0/0000-0001-5715-8632/person` returns given name "Hugo", family name
"van Kemenade", and an ORCID expanded search for that name returns exactly one record — this one. The
alternative `https://orcid.org/0000-0003-1845-9125` is **not a valid ORCID**: it fails the ORCID
ISO 7064 MOD 11-2 check digit (computed `X`, stored `5`) and the ORCID registry has no such record.
The stored value is therefore retained.

**Catalog identity note.** Three stored rows have an empty given name (`Htyeim`, `Scivision`) or are
not personal names (`Supervised`). The organizational creator and identity enrichments below were
not incorporated into this record; they belong to campaign-wide shared-identity reconciliation.

*Catalog identity observations:*
- **P. L. Lim** has a discoverable ORCID that HSSI records as absent: `https://orcid.org/0000-0003-0079-4114`
  resolves to given name "Pey Lian", family name "Lim", with employment "Space Telescope Science
  Institute" (Baltimore, MD, since 2007-10-01) — an exact match to the affiliation already stored for
  this author. The identifier passes the ORCID ISO 7064 MOD 11-2 check digit.
- **Julie Barnum** likewise: `https://orcid.org/0000-0001-8755-0694` resolves to given name "Julie",
  family name "Barnum", institution "Laboratory for Atmospheric and Space Physics". An ORCID expanded
  search for that name returns exactly this one record, so the match is unambiguous. Checksum valid.
  HSSI currently stores neither an identifier nor an affiliation for her.
- `Scivision` (blank given name) is the GitHub handle of **Michael Hirsch** (`scivision`, 34 commits,
  third-largest contributor). Correct form: given "Michael", family "Hirsch".
- `Htyeim` (blank given name) is the GitHub handle `htyeim` (1 commit). No real name published.
- `Supervised` is not a name. Its HSSI affiliation is UCLA and its Zenodo affiliation is "UCLA
  Institute of Geophysics and Planetary Physics"; the only UCLA IGPP committer is
  `egrimes@igpp.ucla.edu` (**Eric Grimes**, GitHub `ericthewizard`), so this row is most likely a
  mangled Zenodo entry for him. Not asserted as fact.
- Affiliation strings that would benefit from acronym expansion if authors were ever patchable:
  `IEAP University Kiel` -> Institute of Experimental and Applied Physics, University of Kiel;
  `Laboratory of Plasma Physics (LPP/CNRS)` -> Laboratoire de Physique des Plasmas.

*Git contributors not treated as authors:* `git shortlog -sne` and the GitHub
contributors list include Mykhaylo Shumko, David Turner, Brad Trantham, Stuart Mumford, Warrick Ball,
Ben Greiner, Maxine Hartnett, Eric Grimes, and several handle-only accounts who are not on the Zenodo
creator list and are not declared authors anywhere in the repository. `pyproject.toml` declares only
`Bryan Harter <harter@lasp.colorado.edu>`. Contributing is not authorship; the Zenodo creator list is
the project's own author statement.

*Also checked and excluded:* the PyHC registry lists `contact: Bryan Harter, Michael Liu, David
Stansby, Michael Hirsch`. The other three are accounted for above, but **Michael Liu** appears in no
authoritative source — not in `git log --all` authors, not in the Zenodo concept-DOI creator list
(16 entries, none matching), and nowhere in the repository. PyHC's `contact` field lists community
points of contact, which is not an authorship claim, so he is not treated as an author.

### 7. Software Name (MANDATORY)
CDFlib

*PRESERVED from existing HSSI record. Corroborated: `README.md` heading is `# CDFlib`, and the PyHC
community registry lists the project as `name: CDFlib`. (The distribution/import name is the lowercase
`cdflib`; the display name is not changed.)*

### 8. Description (MANDATORY)
cdflib is a pure-Python implementation of NASA's Common Data Format (CDF) for reading and writing CDF files. It is not a set of bindings around the NASA CDF C library: the core depends only on NumPy, so there is nothing to compile and no external library to install. cdflib reads variables, global attributes and variable attributes from CDF version 2 and version 3 files held on local disk, behind an HTTP/HTTPS URL, or in an S3 bucket (including chunked byte-range reads), transparently decompressing GZIP- and RLE-compressed files and optionally validating their MD5 checksums. It writes CDF version 3 files, with optional per-variable and whole-file compression and checksums. Its cdfepoch module converts between the CDF time types (CDF_EPOCH, CDF_EPOCH16 and CDF_TT2000) and ISO 8601 strings, NumPy datetime64 values, Unix timestamps and broken-down date components, using a bundled leap-second table; an optional astropy backend exposes the same conversions as astropy Time formats. Optional xarray helpers convert a CDF file into an xarray Dataset and write an xarray Dataset back out as a CDF, checking and filling in ISTP-compliant metadata in both directions, which also makes netCDF-to-CDF conversion straightforward.

*CHANGED — factual correction, not a stylistic rewrite. Old: "CDFlib provides Python bindings to read
and write CDF (Common Data Format) files" (preserved here so nothing is silently discarded). The
phrase "Python bindings" is contradicted by every primary source, and inverts the software's central
selling point: `README.md` — "a python module to read/write CDF ... **without needing to install the
CDF NASA library**"; `docs/index.md` — "cdflib is an effort to replicate the CDF libraries using a
**pure python implementation**. This means users do not need to install the CDF NASA libraries";
`.github/copilot-instructions.md` — "a pure Python library ... **It does not rely on the NASA CDF C
library**"; PyHC registry — "Read / write NASA CDF with pure Python + Numpy, no compiling";
`pyproject.toml` declares `numpy >= 1.21` as the sole runtime dependency and PyPI ships a
`py3-none-any` wheel. The replacement keeps the old sentence's shape and subject while correcting the
error and adding the substance Field 8 asks for (what it does, why to use it, its assumptions).*

### 9. Concise Description (OPTIONAL)
Read or write CDF files in Python

*PRESERVED from existing HSSI record — accurate and within the length limit, so left alone as
submitter wording. (A richer 200-character alternative such as "Read and write NASA CDF files in pure
Python, with no need for the NASA CDF library" is noted only as an option; it is a stylistic
preference, not a correction.)*

### 10. Publication Date (RECOMMENDED)
2017-09-11

*PRESERVED from existing HSSI record, and independently corroborated: the first PyPI release
(`cdflib` 0.1.0) was uploaded 2017-09-11. (For context, the first commit is 2017-07-31 and the GitHub
repository was created 2017-09-08 — the stored date is the first public release, which is the correct
reading of "date of first publication.")*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*PRESERVED from existing HSSI record. Correct per Field 11: the DOI was obtained through the
GitHub-Zenodo workflow. Zenodo has no ROR, so the service URL is the appropriate identifier.*

### 12. Version (RECOMMENDED)
- **Version Number:** 1.3.12
- **Version Date:** 2026-06-01
- **Version Description:** Bug-fix release. Invalid ISTP `DEPEND_N` attribute values encountered by `xarray_to_cdf` now respect the `terminate_on_warning` flag — they are reported through `_warn_or_except` instead of unconditionally raising `ValueError` — so writing a Dataset with a malformed DEPEND attribute warns by default rather than aborting.
- **Version PID:** Not found

*CHANGED. Old version number: `1.3.6` (stored bare; the view API renders it as "CDFlib - 1.3.6" —
the rendered prefix is a display transform and is not part of the stored value). Evidence for
`1.3.12`: git tag `1.3.12` is the extracted revision `a5362441980ad8d740c647a77527b05c41195eed`
(committed 2026-06-01), the GitHub release `1.3.12` was published 2026-06-01, and PyPI reports
`info.version = 1.3.12` uploaded 2026-06-01. Nothing newer exists on either GitHub tags/releases or
PyPI as of 2026-07-29. Version description derived from the single commit in `1.3.11..1.3.12`
(`a536244`, "Fixing an issue where an error was thrown") and its diff to
`cdflib/xarray/xarray_to_cdf.py`; the GitHub release notes and `docs/changelog.md` have no 1.3.12
entry.*

*Version PID is genuinely absent, not merely unfound: Zenodo's newest deposit for this project is
`10.5281/zenodo.7011489` (version 0.4.7), so no version DOI has ever been minted for any 1.x release.
See the Field 2 note.*

### 13. Programming Language (RECOMMENDED)
Python 3.x

*`Python 3.x` PRESERVED from existing HSSI record, and correct: `requires-python = ">= 3.9"`,
classifiers `Programming Language :: Python :: 3 :: Only` and 3.9-3.13, and the GitHub language
breakdown is Python plus a 222-byte `.devcontainer/Dockerfile`.*

*`Other` was removed because the repository contains no source in any
other language — no C, Fortran, IDL, MATLAB, Java or compiled extension of any kind, which is the
project's defining design choice. The only non-Python file GitHub counts is the development-container
Dockerfile, which is contributor tooling rather than a shipped language component.*

### 14. Reference Publication (RECOMMENDED)
Not found

*No JOSS or other software paper. No `CITATION.cff`, `codemeta.json` or `.zenodo.json` exists in the
repository, and neither the DataCite record nor the README names a reference publication.*

### 15. License (RECOMMENDED)
MIT License

*CHANGED (field was empty in HSSI). Evidence: `LICENSE` at the repository root contains the verbatim
MIT License text, "Copyright (c) 2025 Regents of the University of Colorado"; `pyproject.toml`
declares `license = { file = "LICENSE" }`; the GitHub API reports `license.spdx_id = MIT`; and the
PyPI metadata carries the same MIT text. `MIT License` is a byte-identical row in the live `License`
vocabulary.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- cdf
- common data format
- nasa cdf
- istp
- xarray
- netcdf
- maven
- lasp
- pds
- gsfc

*CHANGED (additive). Old: `cdf` only (stored lowercase; the view API renders it Title Case as "Cdf").
Written lowercase to match the existing row's casing and avoid near-duplicates. `Keyword` is the one
open vocabulary — `cdf`, `nasa cdf`, `istp`, `xarray`, `netcdf` and `maven` already exist as
byte-identical live rows and are reused; `common data format`, `lasp`, `pds` and `gsfc` would be
created.*

*Evidence: `maven`, `lasp`, `pds` and `gsfc` are the project's own declared package keywords
(`pyproject.toml`: `keywords = ["CDF", "maven", "lasp", "PDS", "GSFC"]`). `common data format` and
`nasa cdf` are the format's full and colloquial names, spelled out throughout `README.md` and
`docs/index.md`, and are the obvious search terms for someone who does not know the `cdf` abbreviation.
`istp` reflects a documented feature, not an aspiration: `xarray_to_cdf` validates ISTP compliance
(`_global_attribute_checker`, `_variable_attribute_checker`, `_dimension_checker`, `_epoch_checker`,
`ISTPError`), `tests/test_xarray_istp_checkers.py` covers it, and `.github/skills/istp-compliance/`
documents the conventions. `xarray` and `netcdf` reflect the public converter API and the documented
netCDF-to-CDF workflow (Fields 18/19, 30).*

*Declined: `python` (redundant with Field 13), `heliophysics`, `data access`, `file format` — too
generic to aid discovery.*

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- S3/Cloud-aware

*CHANGED (field was empty in HSSI). Both values confirmed against the live `DataInput` vocabulary.*

*Evidence — `CDF.__init__` in `cdflib/cdfread.py` branches on the path scheme, so remote reading is a
first-class documented parameter, not an internal detail:*
- *`HTTP/HTTPS Directories`: `fname.startswith("http://") or fname.startswith("https://")` sets
  `ftype = "url"`, and `_file_or_url_or_s3_handler` fetches it with
  `urllib.request.Request`/`urlopen`.*
- *`S3/Cloud-aware`: `fname.startswith("s3://")` sets `ftype = "s3"`; the documented
  `s3_read_method` parameter selects among load-to-memory, download-to-tmp, and "reads the file in
  chunks directly from S3 over https"; `cdflib/s3.py`'s `S3object` implements ranged
  `read`/`seek`/`tell`; and `boto3`/`botocore` support unsigned anonymous access
  (`Config(signature_version=UNSIGNED)`). `docs/changelog.md` records "Updated cdfread to allow anon
  access from AWS S3" (1.3.2), and `.github/copilot-instructions.md` states the library "Supports
  reading from local files, URLs, and S3 buckets".*

*Declined: `CDAWeb`, `Observatory/Mission-specific` and the other archive-specific rows. cdflib
implements no archive client and no search/query API; it reads a URL or key you already have. CDAWeb
appears only as background prose in `.github/skills/istp-compliance/`, and the LASP MAVEN SDC URL in
`tests/test_xarray_reader_writer.py` is a test-fixture host, not a supported data source.*

### 18. Input File Formats (RECOMMENDED)
- CDF
- ISTP-Compliant

*CHANGED (additive). Old: `CDF` only — preserved. Both confirmed against the live `FileFormat`
vocabulary.*

- *`CDF` — `cdflib/cdfread.py` parses the CDF binary format directly, accepting both version 3
  (`magic_number == "cdf30001"`) and version 2 (`"cdf26002"`) files.*
- *`ISTP-Compliant` — reading is ISTP-aware, not merely ISTP-agnostic: `cdf_to_xarray` interprets
  `DEPEND_0..N`, `LABL_PTR`, `UNIT_PTR`, `FORM_PTR`, `VAR_TYPE`, `FILLVAL` and `DELTA_*` attributes to
  reconstruct dimensions, coordinates, labels and uncertainties
  (`_discover_depend_variables`, `_discover_label_variables`, `_discover_uncertainty_variables`,
  `_determine_dimension_names`, `_convert_fillvals_to_nan`), and `docs/xarray.md` states the
  converters "attempt to determine any ISTP Compliance".*
*`netCDF3/4` was considered and excluded because cdflib does not read
netCDF. The public converter signatures fix the boundary: `cdf_to_xarray(filename: str) -> xr.Dataset`
takes a **CDF** path and returns an in-memory Dataset, and
`xarray_to_cdf(xarray_dataset: xr.Dataset, file_name: str) -> None` takes an in-memory Dataset and
writes a **CDF** file. No cdflib function accepts a `.nc` path. Within the `cdflib` package itself, a
search for `load_dataset`, `open_dataset` and `to_netcdf` returns **no executable call at all** — the
single hit is a docstring line — and every `xr.*` reference is a type annotation or an in-memory
object construction. xarray is not even a runtime dependency (`numpy` is the only one). The "Example
netCDF -> CDF conversion" section of `xarray_to_cdf`'s docstring has **the user** call
`xr.load_dataset(...)` in their own script and pass the resulting Dataset in — a tutorial for
combining two libraries, not a cdflib capability. `tests/test_xarray_reader_writer.py` does call
`xr.load_dataset()` on `.nc`/`.ncdf` fixtures about ten times, but that is the test harness standing
in for the user: it loads netCDF **with xarray**, then feeds the Dataset to cdflib for comparison
against the CDF path — which demonstrates the division of labour rather than contradicting it. Because
Fields 18/19 drive browse facets, listing `netCDF3/4` would put cdflib in front of users who filter
for netCDF readers and then cannot open their file with it. The real capability is recorded where it
is accurate: keyword `netcdf` (Field 16) and `xarray` as interoperable software (Field 30).*

### 19. Output File Formats (RECOMMENDED)
- CDF
- ISTP-Compliant

*CHANGED (additive). Old: `CDF` only — preserved.*

- *`CDF` — `cdflib/cdfwrite.py` writes CDF version 3 files (`write_globalattrs`,
  `write_variableattrs`, `write_var`), with optional GZIP compression and MD5 checksums.*
- *`ISTP-Compliant` — `xarray_to_cdf(..., istp=True)` is the default and actively produces ISTP
  metadata rather than just checking it: it injects missing `DEPEND_N` attributes
  (`_add_depend_variables_to_dataset`), enforces required global and variable attributes, validates
  `LABLAXIS`/`LABL_PTR` dimensions, checks monotonically increasing epochs, and converts
  `epoch`/`epoch_N` variables to CDF_TT2000. Non-compliance surfaces as warnings or `ISTPError`.*

*`netCDF3/4` is deliberately NOT listed as an output: cdflib writes only CDF. Writing a Dataset to
netCDF would be `xarray`'s `to_netcdf`, which cdflib never calls. This matches the symmetric decision
on Field 18 — cdflib neither reads nor writes netCDF in either direction.*

### 20. Operating System (RECOMMENDED)
- Operating System Independent
- Linux
- Mac
- Windows

*CHANGED (additive). Old: `Operating System Independent` only — preserved, and confirmed by the PyPI
classifier `Operating System :: OS Independent` and the pure-Python `py3-none-any` wheel.*

*`Linux`, `Mac` and `Windows` are backed by
`.github/workflows/ci.yml`, whose test matrix is
`os: [ubuntu-latest, windows-latest, macos-latest]` x `python-version: ["3.10", "3.11", "3.12", "3.13"]`
— all three platforms are actually exercised on every push and pull request, so the claim is tested,
not merely asserted.*

### 21. CPU Architecture (RECOMMENDED)
CPU Independent

*CHANGED (field was empty in HSSI). Evidence: cdflib is pure Python with no compiled extension, no
`ext_modules`, and no build-time compiler requirement — `README.md` states "The core of this package
uses only numpy, with no complicated compiler requirements", `pyproject.toml` lists `numpy >= 1.21`
as the sole runtime dependency, and PyPI ships a single architecture-independent `py3-none-any` wheel
per release (no per-architecture wheels exist). `CPU Independent` is a byte-identical row in the live
`CPUArchitecture` vocabulary.*

### 22. Related Phenomena (OPTIONAL)
Not found

*Empty in HSSI and left empty. cdflib is a file-format library; it neither models nor detects any
physical phenomenon. None of the live `Phenomena` rows (Coronal Heating, Coronal Mass Ejections,
Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission) has any support in the
repository, and inferring phenomena from the science content of test fixtures would be fabrication.*

### 23. Development Status (RECOMMENDED)
Active

*CHANGED (field was empty in HSSI). Evidence: PyPI classifier `Development Status :: 5 -
Production/Stable`; the GitHub API reports `archived = false` with `pushed_at = 2026-06-01`, under two
months before extraction; four releases shipped in 2026 alone (1.3.9 on 2026-04-09, 1.3.10 on
2026-04-29, 1.3.11 on 2026-05-21, 1.3.12 on 2026-06-01); CI runs a 12-cell matrix on every push and
pull request; and `.github/workflows/remote-tests.yaml` runs a scheduled weekly remote-data job.
`Active` is a byte-identical row in the live `RepoStatus` vocabulary.*

### 24. Documentation (RECOMMENDED)
https://lasp.github.io/cdflib/

*CHANGED. Old: `https://cdflib.readthedocs.io/en/latest/`. Evidence that the documentation moved:*
- *`README.md` states "The full documentation can be found here" and links only
  `https://lasp.github.io/cdflib/`.*
- *The repository has no `.readthedocs.yml`/`.readthedocs.yaml` and no `docs/conf.py`. Both were
  deleted in commit `6d3f966` "Adding Mkdocs and Simplifying Github Actions (#318)" (2025-11-21),
  which introduced `mkdocs.yml` and `.github/workflows/docs.yml`.*
- *`.github/workflows/docs.yml` runs `mkdocs gh-deploy --force` on every push to `main`, publishing to
  GitHub Pages at `https://lasp.github.io/cdflib/`. That site serves the current MkDocs Material
  build; the Read the Docs site still serves a Sphinx build, which this repository no longer contains
  the configuration to produce.*
- *The Read the Docs project record still points at the pre-move `https://github.com/MAVENSDC/cdflib`
  and declares `documentation_type: sphinx`.*

*Both URLs currently resolve. The Read the Docs URL is not dead — it is unmaintained and served from
build configuration the project deleted, which is why it should be replaced rather than kept as an
alternative. (The PyHC registry also still lists the Read the Docs URL; PyHC's entry predates the
move and is stale in the same way, as is its `code:` URL — see Field 3.)*

### 25. Funder (OPTIONAL)
Not found

*Searched the full repository for funding, grant, award and sponsor statements: nothing. The DataCite
record has an empty `fundingReferences` array and the Zenodo record has no grants. `LICENSE` names
"Regents of the University of Colorado" as copyright holder, which is a rights holder, not a funder,
and would be a guess if recorded here.*

### 26. Award Title (OPTIONAL)
Not found

*No award title or number anywhere in the repository or the DOI metadata.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

*No publications are cited by the repository, the DataCite record (empty `relatedItems`), or the
Zenodo record beyond the `isSupplementTo` link back to the GitHub source tree. The GSFC/SPDF URLs in
the repository are specification and user-guide documents, not citable publications about cdflib.*

### 28. Related Datasets (OPTIONAL)
Not found

*cdflib is dataset-agnostic. The mission files under `tests/testfiles/` and the remote-data URLs in
`tests/test_xarray_reader_writer.py` are format-exercise fixtures chosen for structural variety, not
datasets the software is built to support, and none carries a dataset DOI or an hpde.io identifier.*

### 29. Related Software (OPTIONAL)
- https://cdf.gsfc.nasa.gov/ — NASA CDF library (the reference C library and toolset for the CDF format)
- https://doi.org/10.5281/zenodo.3252523 — SpacePy (its `spacepy.pycdf` module reads and writes CDF by wrapping the NASA CDF C library)
- https://github.com/SciQLop/CDFpp — pycdfpp (a header-only C++ CDF library with Python bindings)

*`NASA CDF library` — this is the software cdflib exists to replace, and it is named as such in the
repository's own framing, which makes it genuinely distinguishing. `README.md` — "read/write CDF ...
without needing to install the [CDF NASA library](https://cdf.gsfc.nasa.gov/)"; `docs/index.md` —
"cdflib is an effort to replicate the CDF libraries using a pure python implementation. This means
users do not need to install the [CDF NASA libraries](https://cdf.gsfc.nasa.gov/)";
`.github/copilot-instructions.md` — "It does not rely on the NASA CDF C library". No DOI exists for
the NASA CDF library, so the project URL is used, as Field 29 permits.*

*`SpacePy` and `pycdfpp` are included as same-purpose peers. Field 29
covers "software that performs similar tasks but does not necessarily link together," and names "a
package performing similar tasks" as its first qualifying category; unlike Field 30 it does not
require a demonstrated exchange, so the absence of an in-repo reference is not disqualifying. Both are
heliophysics/scientific CDF libraries, so neither is generic infrastructure. The distinguishing
information in each case is architectural: `spacepy.pycdf` is a Python interface **over** the NASA CDF
C library and `pycdfpp` is a C++ implementation with Python bindings, whereas cdflib's defining design
choice is a pure-Python implementation that needs no compiled CDF library at all — the contrast a
reader choosing among them most needs.*

*Resolution notes. SpacePy is recorded as its Zenodo **concept (all-versions) DOI**
`10.5281/zenodo.3252523`, which satisfies Field 29's preference for a DOI and is also the persistent
identifier on SpacePy's own HSSI record, so the entry cross-links two existing HSSI resources rather
than pointing outside the registry. pycdfpp has no DOI located, so its repository URL is used per
Field 29's documented fallback; note the PyPI distribution is `pycdfpp` while the repository is named
`CDFpp`. Its author, Alexis Jeandet, is also a listed CDFlib author (entry 7).*

*Considered and not added (audit trail):*
- *`numpy` — Tier A generic infrastructure. Excluded even though it is the sole runtime dependency;
  "depends on numpy" is true of nearly every package in HSSI and distinguishes nothing.*
- *`boto3` / `botocore` — a general-purpose cloud SDK that would be equally at home in a web app;
  Tier A treatment despite the real S3 integration (which is captured in Field 17 instead).*
- *`pooch`, `hypothesis`, `pytest`, `pytest-cov`, `pytest-remotedata`, `mkdocs`, `mkdocs-material`,
  `mkdocstrings`, `ipython`, `pre-commit`, `matplotlib` — testing, docs and development tooling.*

### 30. Interoperable Software (OPTIONAL)
- https://github.com/pydata/xarray — xarray
- https://github.com/astropy/astropy — astropy

*Both are Tier B packages admitted on specific cited evidence of a demonstrated exchange, not on
dependency presence (neither is even a runtime dependency — both are optional extras).*

- ***xarray*** *— cdflib ships a dedicated adapter subpackage. `cdflib/xarray/cdf_to_xarray.py`
  exposes `cdf_to_xarray(filename, ...) -> xr.Dataset` and `cdflib/xarray/xarray_to_cdf.py` exposes
  `xarray_to_cdf(dataset, path, ...)`, a documented round-trip converter pair between the CDF file
  format and xarray's data model. `docs/xarray.md` is a dedicated documentation page for it;
  `tests/test_xarray_reader_writer.py` and `tests/test_xarray_istp_checkers.py` test it; and the
  converters translate ISTP semantics into xarray coordinates, dimensions, labels and plotting
  attributes (`_find_xarray_plotting_values`, `ISTP_TO_XARRAY_ATTRS`). This is an explicit
  adapter/converter API, the exact bar Field 30 sets.*
- ***astropy*** *— `cdflib/epochs_astropy.py` registers three new astropy time formats by subclassing
  `astropy.time.formats.TimeFromEpoch`: `CDFEpoch`, `CDFEpoch16` and `CDFTT2000`. `CDFAstropy`
  methods (`convert_to_astropy`, `encode`, `breakdown`, `to_datetime`, `unixtime`, `compute`,
  `findepochrange`, `parse`) accept and return `astropy.time.Time` objects, so CDF time values become
  first-class astropy quantities. Covered by `tests/test_astropy_epochs.py`; `astropy` is a declared
  test extra. This extends astropy's own type system rather than merely calling it.*

*Considered and excluded (audit trail):*
- *`numpy` — Tier A, no exceptions.*
- *`netCDF4` / `h5netcdf` — Tier B, but the documented exchange is with xarray: the netCDF-to-CDF
  workflow reads through `xarray.load_dataset` and these are only the engines xarray selects. cdflib
  has no netCDF API of its own, so no direct exchange is demonstrated. (The workflow itself is
  recorded in Field 18.)*
- *`boto3` / `botocore`, `pooch`, `pytest`, `pytest-remotedata`, `hypothesis`, `matplotlib`,
  `mkdocs*`, `ipython`, `pre-commit` — generic infrastructure and tooling.*
- *Blanket ecosystem claims — cdflib is widely used downstream (PySPEDAS, pytplot, sunpy, pysat and
  others read CDFs through it), but "part of the scientific Python ecosystem" and "a PyHC member,
  so it interoperates with PyHC packages" are never sufficient, and none of those packages is
  referenced from this repository. Not listed.*

### 31. Related Instruments (OPTIONAL)
Not found

*Deliberately empty — a documented omission at the **relevance gate**, before any vocabulary
resolution was attempted. cdflib is a general-purpose, instrument-agnostic implementation of a file
format; it supports no instrument specifically, so per Field 31 it supports none. Nothing in the
repository is purpose-built for, calibrates, or models any instrument's measurements.*

*What was considered and why it was excluded:* the repository names many instruments, but only as
test fixtures and docstring examples chosen to exercise structural variety in CDF files —
`tests/testfiles/` holds PSP FIELDS, DE-2 RPA and FAST ESA files, and the remote-data tests and
`cdf_to_xarray`/`xarray_to_cdf` docstrings walk through MMS FGM/FPI/EPD-EIS, THEMIS ground
magnetometer, MAVEN LPW/SWIA/SWEA/SEP/STATIC/EUV, Van Allen Probes EMFISIS, GOES-17 magnetometer,
Wind 3DP, OMNI, SABER and TIMED-SEE products. Field 31 excludes tutorial/demo/example name-drops
outright. The two sanity checks both fail: a user searching HSSI for `instrument:"MMS FGM"` wants
MMS analysis tools, not a format library, and someone working with FGM data would reach for cdflib
only incidentally, as they would for any CDF file.

*This is an exclusion, not a resolution failure. The live `InstrumentObservatory` vocabulary is
reachable and fully SPASE-backed (every row's `identifier` is a `https://spase-metadata.org/` URL,
with no non-SPASE rows), and it contains rows for every mission and instrument listed above — so
these entries were dropped for irrelevance, not for want of a match. No name is emitted without a
SPASE identifier.*

*The MAVEN, PDS and GSFC references in `pyproject.toml`'s keywords are provenance and heritage — the
project began at the LASP MAVEN Science Data Center and targets a NASA/GSFC format — not a
designed-to-support relationship. They are recorded as keywords (Field 16), which is where they
belong.*

### 32. Related Observatories (OPTIONAL)
Not found

*Deliberately empty for the same reason and by the same reasoning as Field 31: cdflib is
mission-agnostic, and every mission mentioned in the repository (Parker Solar Probe, MMS, THEMIS,
MAVEN, Van Allen Probes, GOES, Wind, Dynamics Explorer 2, FAST, TIMED, OMNI) appears only as a test
fixture or documentation example. Excluded at the relevance gate. No observatory name is emitted
without a SPASE identifier.*

### 33. Logo (OPTIONAL)
Not found

*No logo exists in the repository: no image asset under `docs/`, no `logo` or `favicon` setting in
`mkdocs.yml`, and no logo in `README.md`.*

*Candidate considered and declined: the PyHC community registry lists
`logo: https://avatars3.githubusercontent.com/u/22352442?s=460&v=4` for CDFlib, which still serves a
PNG. Declined on three grounds — it is the **GitHub organization avatar of MAVENSDC**, the
organization the project has since moved away from (Field 3), not a logo for cdflib itself; a GitHub
avatar URL carrying `?s=460&v=4` sizing parameters on the legacy `avatars3.` shard host is not the
"permanent place" Field 33 requires; and PyHC's entry for this project is demonstrably stale in its
other URLs too.*

---

## Extraction Summary

**Changed versus the live HSSI record (all evidence-backed):**

| Field | Old (live HSSI) | New | Basis |
|---|---|---|---|
| 3 Code Repository | `https://github.com/MAVENSDC/cdflib` | `https://github.com/lasp/cdflib` | permanent redirect + `pyproject.toml` + `mkdocs.yml` + README badges + git remote |
| 4 Software Functionality | `Servers and Environments: Distribution/Access` | 4 `Data Processing and Analysis` values (bare parent included) | source-level analysis of read/write/epoch/xarray modules; old value removed as unsupported |
| 5 Related Region | 3 values | *(cleared)* | no region-specific science functionality; stored trio was a legacy-vocabulary artifact |
| 8 Description | "Python bindings" phrasing | corrected, expanded | factual error contradicted by README, docs, PyHC, packaging |
| 12 Version | `1.3.6` | `1.3.12` (+ date, description) | git tag at HEAD, GitHub release, PyPI |
| 13 Programming Language | `Python 3.x`, `Other` | `Python 3.x` | no non-Python source of any kind |
| 15 License | *(empty)* | `MIT License` | `LICENSE`, GitHub `spdx_id`, PyPI |
| 16 Keywords | `cdf` | 10 keywords | declared `pyproject.toml` keywords + documented features |
| 17 Data Sources | *(empty)* | `HTTP/HTTPS Directories`, `S3/Cloud-aware` | `cdfread.py` scheme dispatch, `s3.py`, changelog |
| 18 Input Formats | `CDF` | + `ISTP-Compliant` | ISTP-aware reader (`netCDF3/4` declined — cdflib parses no netCDF) |
| 19 Output Formats | `CDF` | + `ISTP-Compliant` | `xarray_to_cdf(istp=True)` generates ISTP metadata |
| 20 Operating System | `Operating System Independent` | + `Linux`, `Mac`, `Windows` | CI matrix tests all three |
| 21 CPU Architecture | *(empty)* | `CPU Independent` | pure Python, `py3-none-any` wheel |
| 23 Development Status | *(empty)* | `Active` | not archived, four 2026 releases, active CI |
| 24 Documentation | `https://cdflib.readthedocs.io/en/latest/` | `https://lasp.github.io/cdflib/` | RTD config deleted in `6d3f966`; MkDocs deployed by `docs.yml`; README |
| 29 Related Software | *(empty)* | NASA CDF library, SpacePy, pycdfpp | the library cdflib replaces, plus two same-purpose CDF peers |
| 30 Interoperable Software | *(empty)* | xarray, astropy | `cdflib/xarray/` converters; astropy Time format subclasses |

**Preserved unchanged:** 2 Persistent Identifier, 7 Software Name, 9 Concise Description,
10 Publication Date, 11 Publisher, 22 Related Phenomena (empty), 25/26 Funder & Award (empty),
27/28 Related Publications & Datasets (empty), 31/32 Related Instruments & Observatories (empty),
33 Logo (empty).

## Durable catalog notes

- Field 6 preserves the stored 15-author set. The MAVEN SDC organizational creator and the documented
  identity enrichments remain campaign-wide shared-identity observations rather than changes to this
  record. Hugo van Kemenade's stored ORCID is verified and correct.
- Fields 31 and 32 are empty because cdflib is mission-agnostic; mission and instrument names in tests
  and examples do not establish scientific support.
- Replacing Field 12 naturally detached the previous `1.3.6` SoftwareVersion row. HSSI retains
  unreferenced version rows as normal platform behaviour; no catalog cleanup is needed for this record.
