# HSSI Metadata Extraction Results

**HSSI Software ID:** 11cb7b68-cfe7-4d6c-84ed-af5ab071e74c
**Repository:** https://github.com/lasp/cdflib
**Source Revision:** a5362441980ad8d740c647a77527b05c41195eed
**Extraction Date:** 2026-07-29
**Validation Date:** 2026-10-29
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Note: Submitter details are not exposed in the public software view.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.1481144

*DataCite shows this is the Zenodo **concept (all-versions) DOI** — `versionOfCount` is 0, it carries `HasVersion` relations to eleven version DOIs
(0.3.19 was deposited twice, as `10.5281/zenodo.4013925` and `10.5281/zenodo.4746598`, although
DataCite's own `versionCount` reads 10) plus one `IsSupplementTo` link to the 0.4.7 source tree, and
Zenodo reports `conceptrecid = 1481144`. It is the correct value for this field.*

*Note (upstream, not an HSSI error): the GitHub-Zenodo archiving hook stopped producing deposits
after version 0.4.7 (2022-08-19), so on 2026-10-28 the concept DOI's record still showed title
`MAVENSDC/cdflib:` and version 0.4.7, and `https://zenodo.org/badge/latestdoi/102912691` still
resolved to `10.5281/zenodo.7011489` (0.4.7). Consequently no version-specific DOI exists for any
1.x release, 1.3.16 included — see Field 12. Worth reporting to the maintainers; nothing to fix in HSSI.*

*Not to be proposed: the "Archive" link at the top of `docs/index.md` (at `cf7553f`) points to
`https://zenodo.org/record/4746617`, which DataCite identifies as the version deposit for 0.3.20
(`10.5281/zenodo.4746617`, `IsVersionOf` this concept DOI). It is neither this field's value nor a
Version PID for any 1.x release.*

### 3. Code Repository (MANDATORY)
https://github.com/lasp/cdflib

*HSSI formerly held `https://github.com/MAVENSDC/cdflib`. Evidence that it is wrong: the old URL permanently redirects
to `https://github.com/lasp/cdflib`; the GitHub API reports `full_name = lasp/cdflib`,
`fork = false`, `archived = false`, default branch `main`; `pyproject.toml` declares
`[project.urls] Homepage = "https://github.com/lasp/cdflib"`; `mkdocs.yml` declares
`repo_url: https://github.com/lasp/cdflib`; the README's CI and codecov badges target `lasp/cdflib`; and the local
clone's `origin` is `https://github.com/lasp/cdflib.git`. The repository moved GitHub organizations
from MAVENSDC to lasp; the former URL is the pre-move location.*

### 4. Software Functionality (RECOMMENDED)
- Data Processing and Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing

*Before the first refresh of this record HSSI held `Servers and Environments: Distribution/Access`
alone. Every `Parent: Child` value above has its bare parent top-level category present as its own
separate entry.*

*That former value is rejected because no repository evidence supports it:
cdflib is a client-side file-format library with no server, service, or distribution component. Its
only remotely related capability — remote/cloud-aware reading — is captured far more precisely by
`Data Processing and Analysis: Data Access and Retrieval`. Its bare parent `Servers and Environments`
is rejected with it, since it existed solely to satisfy the parent-inclusion rule for that child.*

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
Considered and deliberately excluded:
- `Servers and Environments: Distribution/Access` and its bare parent `Servers and Environments` —
  HSSI's former value, rejected as described above.
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

### 5. Related Region (RECOMMENDED)
Not found

*HSSI formerly held `Earth Magnetosphere`, `Interplanetary Space` and `Planetary Magnetospheres`;
none describes cdflib's functionality. This is not an extraction gap; the field is intentionally
empty.*

*Rationale. Field 5 asks for "The physical region the software supports science functionality for."
cdflib has no science functionality tied to any region — it reads and writes a file format.
Every region value is therefore a false membership in a browse facet: a user filtering for
`Earth Magnetosphere` wants magnetosphere science tools, and a byte-level format library appearing
there costs trust in the filter. That is the same standard applied to Fields 18/19, where `netCDF3/4`
was declined because cdflib cannot open a netCDF file.*

*The three former values are all members of the legacy five-item Region list
(`Earth Atmosphere`, `Earth Magnetosphere`, `Interplanetary Space`, `Planetary Magnetospheres`,
`Solar Environment`) that once comprised the selectable vocabulary. That trio reflected the old
coarse dropdown rather than documented region-specific functionality.*

*Region is a RECOMMENDED field, and an evidenced-empty value is legitimate: no region applies to a
format library. An empty Region is also established practice for format and infrastructure tooling —
the closest analog in HSSI, `sammi-cdf` (a Python package for CDF/ISTP metadata management, which reads
and writes `CDF` and `ISTP-Compliant` files), carried no region on 2026-10-28.*

*Also excluded for the same reason: `Earth Atmosphere` (suggested by the PyHC
`ionosphere_thermosphere_mesosphere` tag and the DE-2 RPA / FAST / SABER-TIMED / M-GITM test
fixtures), plus `Earth Ionosphere`, `Earth Thermosphere`,
`Earth Lower and Middle Atmosphere`, `Solar Wind`, `Solar Environment` and `Mars Magnetosphere`. The
mission files under `tests/testfiles/` and the remote-data test corpus were chosen to exercise
structural variety in CDF files; they are not regions the software supports science functionality for.*

*Note for HSSI maintainers (not actionable in this record): a Region field with no `Not applicable`
row cannot say explicitly that format and infrastructure libraries have no region by construction.*

### 6. Authors (MANDATORY)
The record's 15 authors, in its established order.

1. **Alex Antunes** — https://orcid.org/0000-0002-3098-2602 — Affiliations: Johns Hopkins University Applied Physics Laboratory (https://ror.org/029pp9z10); Project Calliope (no ROR)
2. **Julie Barnum** — https://orcid.org/0000-0001-8755-0694 — Affiliation: Laboratory for Atmospheric and Space Physics (https://ror.org/01fcjzv38)
3. **Angeline Burrell** — https://orcid.org/0000-0001-8875-9326 — Affiliation: United States Naval Research Laboratory (https://ror.org/04d23a975)
4. **Bryan Harter** — https://orcid.org/0000-0002-3908-9001 — Affiliation: Laboratory for Atmospheric and Space Physics (https://ror.org/01fcjzv38)
5. **htyeim (GitHub)** *(given name `htyeim`, family name `(GitHub)`)* — Identifier: Not found — Affiliation: Not found
6. **Jack Ireland** — https://orcid.org/0000-0002-2019-8881 — Affiliation: Goddard Space Flight Center (https://ror.org/0171mag52)
7. **Alexis Jeandet** — https://orcid.org/0000-0003-2892-6924 — Affiliation: Laboratoire de Physique des Plasmas (https://ror.org/05c95bg36)
8. **Hugo van Kemenade** — https://orcid.org/0000-0001-5715-8632 — Affiliation: Nord Software (no ROR)
9. **Pey Lian Lim** — https://orcid.org/0000-0003-0079-4114 — Affiliation: Space Telescope Science Institute (https://ror.org/036f5mx38)
10. **Michael Hirsch** — https://orcid.org/0000-0002-1637-6526 — Affiliations: Boston University (https://ror.org/05qwgg493); Scivision, Inc. (no ROR)
11. **Jonathon M. Smith** — https://orcid.org/0000-0002-8191-4765 — Affiliations: Catholic University of America (https://ror.org/047yk3s18); Goddard Space Flight Center (https://ror.org/0171mag52)
12. **David Stansby** — https://orcid.org/0000-0002-1365-1908 — Affiliations: Advanced Research Computing Centre, University College London, UK (no ROR); Department of Mechanical Engineering, University College London (no ROR); Imperial College London (https://ror.org/041kmwe10); Mullard Space Science Laboratory, University College London (no ROR); University College London (https://ror.org/02jx3x895)
13. **Supervised** *(family name `Supervised`, given name empty; not a personal name)* — Identifier: Not found — Affiliation: University of California, Los Angeles (https://ror.org/046rm7j60)
14. **Jan Christoph Terasa** — Identifier: Not found — Affiliation: Institute of Experimental and Applied Physics, University of Kiel (no ROR)
15. **Andreas J. Weiss** — Identifier: Not found — Affiliation: Not found

*Creator considered and not listed:*
- **MAVEN SDC** *(organization author)* — Affiliation: Laboratory for Atmospheric and Space Physics
  (https://ror.org/01fcjzv38); no identifier, since a ROR lookup for "MAVEN Science Data Center"
  returns no matching organization. This is the one Zenodo creator not in the author list: the
  concept DOI's creator list contains 16 entries and the author list 15, the difference being this
  organizational creator. It is kept outside the numbered list, which reproduces the record's
  established author set.

**Hugo van Kemenade — verified identity.** His identifier
`https://orcid.org/0000-0001-5715-8632` is confirmed by the ORCID registry:
`pub.orcid.org/v3.0/0000-0001-5715-8632/person` returns given name "Hugo", family name
"van Kemenade", and an ORCID expanded search for that name returns exactly one record — this one. The
alternative `https://orcid.org/0000-0003-1845-9125` is **not a valid ORCID**: it fails the ORCID
ISO 7064 MOD 11-2 check digit (computed `X`, written `5`) and the ORCID registry has no such record.
His identifier is therefore `0000-0001-5715-8632`.

**Catalogue identity notes.** Several of this project's Zenodo creator strings are handles, initials or
alternate spellings of people the catalogue records under a canonical name. Each is resolved below, with
this project's own creator string recorded so a future refresh reading Zenodo recognises it instead of
creating a second record for the same person.

- **Author 1 — Alex Antunes**, credited by this project as "Sandy Antunes". ORCID
  `0000-0002-3098-2602` resolves to "Alex Antunes" at Johns Hopkins University Applied Physics
  Laboratory, and that person commits as `Sandy Antunes <sandy.antunes@jhuapl.edu>`; `spedas/pyspedas`
  independently lists `Antunes, Sandy` with the JHU/APL affiliation, matching the ORCID's employment.
  **The ORCID name alone would not have been sufficient** — that record publishes no "Sandy" alias — so a
  future refresh must not read the name mismatch there as a contradiction. His record carries both
  JHU/APL and the Project Calliope affiliation this project supplies; an affiliation is never dropped in
  favour of a newer one.
- **Author 2 — Julie Barnum.** `https://orcid.org/0000-0001-8755-0694` resolves to given name "Julie",
  family name "Barnum", institution "Laboratory for Atmospheric and Space Physics". An ORCID expanded
  search for that name returns exactly this one record, so the match is unambiguous, and the checksum is
  valid.
- **Author 5 — `htyeim (GitHub)`.** A proven platform handle with no published human name, recorded in the
  catalogue's convention of the exact handle as the given name and the platform in the family-name field.
  This repository's git author is `htyeim <17849322+htyeim@users.noreply.github.com>`, and GitHub
  attributes commit `75e8424f8c2a00c7137f2ababc8a8bab69e6a9d8` to account `htyeim`, ID 17849322. The
  exact login is lower-case `htyeim` and is not to be capitalised. **No human name is
  asserted, because none is published.**
- **Author 9 — Pey Lian Lim**, credited by this project as "P. L. Lim".
  `https://orcid.org/0000-0003-0079-4114` resolves to given name "Pey Lian", family name "Lim", with
  employment "Space Telescope Science Institute" (Baltimore, MD, since 2007-10-01) — an exact match to the
  affiliation this project already supplied. The identifier passes the ORCID ISO 7064 MOD 11-2 check
  digit. `ndcube`'s git author `2090236+pllim@users.noreply.github.com` ties the same person to GitHub
  account `pllim`.
- **Author 10 — Michael Hirsch**, credited by this project as "scivision". That is his GitHub handle
  (`scivision`, 34 commits, third-largest contributor), and this repository's own git history records the
  author as `Michael Hirsch, Ph.D <scivision@users.noreply.github.com>` — a legacy GitHub noreply address
  encoding that login — so the handle and the name are the same contributor in this project's own record.
  His ORCID is `0000-0002-1637-6526`. **The superficially similar `0000-0001-6183-6256` belongs to a
  different Michael Hirsch** — a Senior Facility Scientist at the Science and Technology Facilities
  Council's Central Laser Facility, with a Leipzig Ph.D. in Mathematics and twenty-nine works entirely in
  single-molecule microscopy and receptor biophysics — and must never be used here.
- **Author 11 — Jonathon M. Smith**, credited by this project as "Jonathon Smith". This repository's git
  author is `Jonathon Smith <36175570+JonathonMSmith@users.noreply.github.com>`, GitHub account
  `JonathonMSmith`; ORCID `0000-0002-8191-4765` resolves to "Jonathon Smith" at the Catholic University of
  America. He is also an author of pysat and sami2py.
- **Author 13 — `Supervised`** is not a personal name and no identity is asserted for it. Its affiliation
  here is UCLA and its Zenodo affiliation is "UCLA Institute of Geophysics and Planetary Physics"; the
  only UCLA IGPP committer is `egrimes@igpp.ucla.edu` (**Eric Grimes**, GitHub `ericthewizard`), so the
  row is most likely a mangled Zenodo entry for him. **Not asserted as fact.** `spedas/pyspedas` does
  carry a git author `supervised <egrimes@igpp.ucla.edu>`, which strengthens the hypothesis without
  settling it, but **this repository's git history contains no `supervised` author at all** — only
  `eric <egrimes@igpp.ucla.edu>` — so there is no repository-side evidence for this entry specifically.
  Resolving it needs the Zenodo creator record for the affected version, or the author's confirmation.

- **Affiliation naming — Jan Christoph Terasa.** The institute is recorded under its expanded name,
  `Institute of Experimental and Applied Physics, University of Kiel`. `IEAP University Kiel` is a
  superseded label for that same institute and should not be reintroduced: Kiel University's Section of
  Physics states that the section comprises "IEAP - Institut für Experimentelle und Angewandte Physik"
  and "ITAP - Institut für Theoretische Physik und Astrophysik", and the institute's own site titles
  itself "Institut für Experimentelle und Angewandte Physik der Christian-Albrechts-Universität zu
  Kiel" — so the acronym string and the expanded string denote one organization. No ROR record exists
  for the institute (a ROR v2 search for it returns nothing), so the expanded name is correctly
  identifierless and no identifier should be invented or attached to it.
- **Affiliation naming — Alexis Jeandet.** The recorded form is ROR's own display name for the
  organization, `Laboratoire de Physique des Plasmas` (`https://ror.org/05c95bg36`). HSSI formerly
  held this organization as `Laboratory of Plasma Physics (LPP/CNRS)`. The ROR identifier fixing
  identity does not make that label right: read in full, the ROR record carries `Laboratory of Plasma
  Physics` only as an English *alias* and `LPP` as an acronym, so the label corresponded to no name form
  on the record at all. It is noted here so it is not reintroduced.

*Git contributors not treated as authors:* `git shortlog -sne` and the GitHub
contributors list include Mykhaylo Shumko, David Turner, Brad Trantham, Stuart Mumford, Warrick Ball,
Ben Greiner, Maxine Hartnett, Eric Grimes, and several handle-only accounts who are not on the Zenodo
creator list and are not declared authors anywhere in the repository. `pyproject.toml` declares only
`Bryan Harter <harter@lasp.colorado.edu>`. Contributing is not authorship; the Zenodo creator list is
the project's own author statement — as a statement about *this dossier's* author list. It is not a rule
against consolidating shared `Person` records: HSSI maintains one Person per uniquely proven human, and
where this project's creator string differs from the canonical person's recorded name, the creator
string is kept in the rationale above rather than as a duplicate row.

*Also checked and excluded:* the PyHC registry lists `contact: Bryan Harter, Michael Liu, David
Stansby, Michael Hirsch`. Michael Hirsch is author 10 above (the `scivision` handle). The other two are
accounted for above, but **Michael Liu** appears in no
authoritative source — not in `git log --all` authors, not in the Zenodo concept-DOI creator list
(16 entries, none matching), and nowhere in the repository. PyHC's `contact` field lists community
points of contact, which is not an authorship claim, so he is not treated as an author.

### 7. Software Name (MANDATORY)
CDFlib

*Corroborated: `README.md` heading is `# CDFlib`, and the PyHC
community registry lists the project as `name: CDFlib`. (The distribution/import name is the lowercase
`cdflib`; the display name is `CDFlib`.)*

### 8. Description (MANDATORY)
cdflib is a pure-Python implementation of NASA's Common Data Format (CDF) for reading and writing CDF files. It is not a set of bindings around the NASA CDF C library: the core depends only on NumPy, so there is nothing to compile and no external library to install. cdflib reads variables, global attributes and variable attributes from CDF version 2 and version 3 files held on local disk, behind an HTTP/HTTPS URL, or in an S3 bucket (including chunked byte-range reads), transparently decompressing GZIP- and RLE-compressed files and optionally validating their MD5 checksums. It writes CDF version 3 files, with optional per-variable and whole-file compression and checksums. Its cdfepoch module converts between the CDF time types (CDF_EPOCH, CDF_EPOCH16 and CDF_TT2000) and ISO 8601 strings, NumPy datetime64 values, Unix timestamps and broken-down date components, using a bundled leap-second table; an optional astropy backend exposes the same conversions as astropy Time formats. Optional xarray helpers convert a CDF file into an xarray Dataset and write an xarray Dataset back out as a CDF, checking and filling in ISTP-compliant metadata in both directions, which also makes netCDF-to-CDF conversion straightforward.

*HSSI formerly held "CDFlib provides Python bindings to read and write CDF (Common Data Format)
files". Replacing it is a factual correction, not a stylistic rewrite. The phrase "Python bindings" is
contradicted by every primary source, and inverts the software's central selling point (emphasis
added in the quotations): `README.md` — "a python module to read/write CDF ... **without needing to install the
CDF NASA library**" (link markup omitted); `docs/index.md` — "cdflib is an effort to replicate the CDF
libraries using a **pure python implementation**. This means users do not need to install the CDF NASA
libraries" (link markup omitted);
`.github/copilot-instructions.md` — "a pure Python library ... **It does not rely on the NASA CDF C
library**"; PyHC registry — "Read / write NASA CDF with pure Python + Numpy, no compiling";
`pyproject.toml` declares `numpy >= 1.21` as the sole runtime dependency and PyPI ships a
`py3-none-any` wheel. The replacement keeps the old sentence's shape and subject while correcting the
error and adding the substance Field 8 asks for (what it does, why to use it, its assumptions).*

### 9. Concise Description (OPTIONAL)
Read or write CDF files in Python

*The submitter's wording, accurate and within the length limit. (A richer 200-character alternative such as "Read and write NASA CDF files in pure
Python, with no need for the NASA CDF library" is noted only as an option; it is a stylistic
preference, not a correction.)*

### 10. Publication Date (RECOMMENDED)
2017-09-11

*Corroborated: the first PyPI release
(`cdflib` 0.1.0) was uploaded 2017-09-11. (For context, the first commit is 2017-07-31 and the GitHub
repository was created 2017-09-08 — the date is the first public release, which is the correct
reading of the form's "Date of first broadcast/publication.")*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Correct per Field 11: the DOI was obtained through the
GitHub-Zenodo workflow. Zenodo has no ROR, so the service URL is the appropriate identifier.*

### 12. Version (RECOMMENDED)
- **Version Number:** 1.3.16
- **Version Date:** 2026-10-21
- **Version Description:** Handle TT2000 leap seconds and adjust unixtime mapping
- **Version PID:** Not found

*Evidence for `1.3.16`, read at `cf7553fe93c0684ae461fffb1df0a0b9daa23219` (the tagged commit, and the
head of the default branch `main`): the tags `1.3.13` (`cbb14d0`), `1.3.14` (`3f1342e`), `1.3.15`
(`e40784a`) and `1.3.16` (`cf7553f`) all lie on `main`'s own lineage (`git merge-base --is-ancestor`
holds for each against `cf7553f`); each has a GitHub release that is neither a draft nor a pre-release;
and PyPI lists each with a `py3-none-any` wheel and an sdist, with `info.version = 1.3.16`. No newer tag,
release or upload existed on 2026-10-28. The remote's other branches are `gh-pages` (the built documentation) and a
feature branch for issue 327; neither is a release branch. The number is written bare, as the tag, the
release name and PyPI write it and as the superseded numbers were stored. HSSI held `1.3.12` (released
2026-06-01) until the 1.3.16 refresh, and `1.3.6` before an earlier refresh replaced it. The view API renders
the number as `CDFlib - <number>`; that prefix is a display transform, not part of the stored value.*

*Version Date: the GitHub release `1.3.16` was published 2026-10-21T17:47:30Z; the tagged commit is
dated 2026-10-21T17:46:52Z (11:46:52-06:00), and PyPI's wheel was uploaded 2026-10-21T17:50:08Z — all
the same UTC day.*

*Version Description: the release name is the bare tag, so the text comes from the release body, whose
only item is "Handle TT2000 leap seconds and adjust unixtime mapping by @bryan-harter in
https://github.com/lasp/cdflib/pull/350", under a "What's Changed" heading. The heading, the item's
trailing contributor-and-pull-request credit and the body's "Full Changelog" compare link are dropped;
the item's own words are kept verbatim. The change it describes (`cf7553f`, PR #350) makes `CDFepoch.breakdown_tt2000` return a leap second as second 60
(`23:59:60`) instead of rolling it into the minute, and makes `unixtime()` map that second to `:59` plus
one second. `docs/changelog.md` has no entry for 1.3.14, 1.3.15 or 1.3.16; its newest heading,
`1.3.13`, carries the non-existent-path fix (#328) that the release notes and the tag place in 1.3.14
(`3f1342e`), so the changelog is not a source for this field. The superseded `1.3.12` row's description
was a summary composed from that release's commit diff, because its release body was only a compare
link; a composed summary is not recorded for any release.*

*Version PID is genuinely absent, not merely unfound: the concept DOI's newest version deposit is
`10.5281/zenodo.7011489` (version 0.4.7, 2022-08-19), so no version DOI has been minted for any 1.x
release. A Zenodo free-text search for `"lasp/cdflib"` returns no deposit (the control
`"MAVENSDC/cdflib"` returns one), and DataCite has no `cdflib`-titled record with version `1.3.16` (the
control, version `0.4.7`, returns the concept and its 0.4.7 version). See the Field 2 note.*

### 13. Programming Language (RECOMMENDED)
Python 3.x

*`Python 3.x` is correct: `requires-python = ">= 3.9"`,
classifiers `Programming Language :: Python :: 3 :: Only` and 3.9-3.13, and the GitHub language
breakdown is Python plus a 222-byte `.devcontainer/Dockerfile`.*

*HSSI formerly also held `Other`, which is rejected because the repository contains no source in any
other language — no C, Fortran, IDL, MATLAB, Java or compiled extension of any kind, which is the
project's defining design choice. The only non-Python file GitHub counts is the development-container
Dockerfile, which is contributor tooling rather than a shipped language component.*

### 14. Reference Publication (OPTIONAL)
Not found

*No JOSS or other software paper. No `CITATION.cff`, `codemeta.json` or `.zenodo.json` exists in the
repository, and neither the DataCite record nor the README names a reference publication.*

*Decided together with Field 27. The developers' AGU Fall Meeting 2019 abstract
(`2019AGUFMSH41C3312H`) is a meeting abstract, which is never Field 14 (rule 2) and never Field 27
either (Field 27 rule 1); no poster or paper of that presentation is deposited (see Field 27).
The PySPEDAS paper (Grimes et al. 2022, https://doi.org/10.3389/fspas.2022.1020815), co-authored by
Bryan Harter, describes a different product that is built on cdflib (rule 5).*

*Burrell et al. 2018, "Snakes on a Spaceship—An Overview of Python in Heliophysics"
(https://doi.org/10.1029/2018JA025877, arXiv:1901.00143), is the one peer-reviewed paper with a section
on cdflib: its appendix section A.3.1, "CDFlib". Its ten authors include two cdflib authors, Angeline
Burrell (author 3) and David Stansby (author 12). Rule 6 still does not fire. It needs a paper by the
developers that names the software in its title or presents its code in a dedicated section, and to
which the project's documentation or its authors point. This paper is a survey of some thirty
community packages by different teams, not a paper about cdflib and its sibling tools, and nothing at
`cf7553f` points to it: a sweep of the pinned tree for `burrell`, `snakes on a spaceship`,
`2018JA025877`, `1901.00143`, `doi.org` and `arxiv` finds only example dataset DOIs in the
ISTP-compliance notes under `.github/skills/` and a binary CDF test fixture, which also serve as the
sweep's positive control. The ADS/SciX search recorded under Field 27 found no other peer-reviewed
paper about cdflib.*

### 15. License (RECOMMENDED)
MIT License

*HSSI held no License before the first refresh of this record. Evidence: `LICENSE` at the repository root contains the verbatim
MIT License text, "Copyright (c) 2025 Regents of the University of Colorado"; `pyproject.toml`
declares `license = { file = "LICENSE" }`; the GitHub API reports `license.spdx_id = MIT`; and the
PyPI metadata carries the same MIT text.*

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
- pyhc package

*Before the first refresh of this record HSSI held `cdf` alone, in lower case (the view API renders
it in title case, "Cdf"). `Keyword` is the one open vocabulary, so every keyword is
written in lower case to match that row's casing and avoid near-duplicates.*

*Evidence: `maven`, `lasp`, `pds` and `gsfc` are the project's own declared package keywords
(`pyproject.toml`: `keywords = ["CDF", "maven", "lasp", "PDS", "GSFC"]`). `common data format` and
`nasa cdf` are the format's full and colloquial names, spelled out throughout `README.md` and
`docs/index.md`, and are the obvious search terms for someone who does not know the `cdf` abbreviation.
`istp` reflects a documented feature, not an aspiration: `xarray_to_cdf` validates ISTP compliance
(`_global_attribute_checker`, `_variable_attribute_checker`, `_dimension_checker`, `_epoch_checker`,
`ISTPError`), `tests/test_xarray_istp_checkers.py` covers it, and `.github/skills/istp-compliance/`
documents the conventions. `xarray` and `netcdf` reflect the public converter API and the documented
netCDF-to-CDF workflow (Fields 18/19, 30).*

*`pyhc package` is the PyHC package marker (Field 16 rule 15). CDFlib is listed in the PyHC
registry's `_data/projects.yml` (entry `name: CDFlib`, read 2026-10-28 with the file as of `7bc0bef`,
its latest change), so the entry carries the exact lower-case row `pyhc package`; it rests on that rule
alone, since no project source lists it. The registry's own tags for this entry — `magnetosphere`,
`ionosphere_thermosphere_mesosphere` and `specific` — are excluded: `specific` is a scope tag (rule 2),
and the two domain tags fail the domain test for the reasons given under Field 5 (rule 3).*

*Declined: `python` (redundant with Field 13), `heliophysics`, `data access`, `file format` — too
generic to aid discovery.*

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- S3/Cloud-aware

*HSSI held no Data Sources before the first refresh of this record.*

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

*Before the first refresh of this record HSSI held `CDF` alone.*

- *`CDF` — `cdflib/cdfread.py` parses the CDF binary format directly, accepting both version 3
  (`magic_number == "cdf30001"`) and version 2 (`"cdf26002"`) files.*
- *`ISTP-Compliant` — reading is ISTP-aware, not merely ISTP-agnostic: `cdf_to_xarray` interprets
  `DEPEND_0..N`, `LABL_PTR`, `UNIT_PTR`, `FORM_PTR`, `VAR_TYPE`, `FILLVAL` and `DELTA_*` attributes to
  reconstruct dimensions, coordinates, labels and uncertainties
  (`_discover_depend_variables`, `_discover_label_variables`, `_discover_uncertainty_variables`,
  `_determine_dimension_names`, `_convert_fillvals_to_nan`), and `docs/xarray.md` states the
  converters "attempt to determine any ISTP Compliance" (link markup omitted).*
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

*Before the first refresh of this record HSSI held `CDF` alone.*

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

*Before the first refresh of this record HSSI held `Operating System Independent` alone. That value
rests on the PyPI classifier `Operating System :: OS Independent` and the pure-Python `py3-none-any`
wheel.*

*`Linux`, `Mac` and `Windows` are backed by
`.github/workflows/ci.yml`, whose test matrix is
`os: [ubuntu-latest, windows-latest, macos-latest]` x `python-version: ["3.10", "3.11", "3.12", "3.13"]`
— all three platforms are actually exercised on every push and pull request, so the claim is tested,
not merely asserted.*

### 21. CPU Architecture (RECOMMENDED)
CPU Independent

*HSSI held no CPU Architecture before the first refresh of this record. Evidence: cdflib is pure Python with no compiled extension, no
`ext_modules`, and no build-time compiler requirement — `README.md` states "The core of this package
uses only numpy, with no complicated compiler requirements", `pyproject.toml` lists `numpy >= 1.21`
as the sole runtime dependency, and PyPI ships a single architecture-independent `py3-none-any` wheel
per release (no per-architecture wheels exist).*

### 22. Related Phenomena (OPTIONAL)
Not found

*Evidenced empty. cdflib is a file-format library; it neither models nor detects any physical
phenomenon. None of the `Phenomena` vocabulary's rows (on 2026-10-28: Coronal Heating, Coronal Mass
Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission) has any support
in the repository, and inferring phenomena from the science content of test fixtures would be fabrication.*

### 23. Development Status (RECOMMENDED)
Active

*HSSI held no Development Status before the first refresh of this record. Evidence, read at
`cf7553fe93c0684ae461fffb1df0a0b9daa23219`: `README.md` and `docs/index.md` carry no successor pointer,
no repostatus.org badge and no status statement (rules 1, 3 and 4), and the GitHub API reported
`archived = false` on 2026-10-28 (rule 2). The software reached a stable, usable state long ago — PyPI releases run from 0.1.0 (2017-09-11) to 1.3.16, and the
classifier `Development Status :: 5 - Production/Stable` corroborates only that releases exist. Rule 6
therefore decides on the last commit on the default branch `main`: `cf7553f`, committed
2026-10-21T17:46:52Z, which is also the newest release (1.3.16, published 2026-10-21). Releases
published in 2026: 1.3.8 (2026-01-09), 1.3.9 (2026-04-09), 1.3.10 (2026-04-29), 1.3.11 (2026-05-21),
1.3.12 (2026-06-01), 1.3.13 and 1.3.14 (both 2026-09-25), 1.3.15 (2026-10-20) and 1.3.16 (2026-10-21).
CI runs a 12-cell matrix on every push and pull request, and `.github/workflows/remote-tests.yaml` runs
a scheduled weekly remote-data job.*

### 24. Documentation (RECOMMENDED)
https://lasp.github.io/cdflib/

*HSSI formerly held `https://cdflib.readthedocs.io/en/latest/`. Evidence that the documentation moved:*
- *`README.md` states "The full documentation can be found here" and links only
  `https://lasp.github.io/cdflib/`.*
- *The repository has no `.readthedocs.yml`/`.readthedocs.yaml` and no `docs/conf.py`. Both were
  deleted in commit `6d3f966` "Adding Mkdocs and Simplifying Github Actions (#318)" (2025-11-21),
  which introduced `mkdocs.yml` and `.github/workflows/docs.yml`.*
- *`.github/workflows/docs.yml` runs `mkdocs gh-deploy --force` on every push to `main`, publishing to
  GitHub Pages at `https://lasp.github.io/cdflib/`. That site serves the MkDocs Material build; on
  2026-10-28 the Read the Docs site still served a Sphinx build, which this repository no longer
  contains the configuration to produce.*
- *On 2026-10-28 the Read the Docs project record still pointed at the pre-move
  `https://github.com/MAVENSDC/cdflib`; at extraction it also declared `documentation_type: sphinx`.*

*On 2026-10-28 both URLs resolved. The Read the Docs URL is not dead — it is unmaintained and served from
build configuration the project deleted, which is why it should be replaced rather than kept as an
alternative. (The PyHC registry also still lists the Read the Docs URL; PyHC's entry predates the
move and is stale in the same way, as is its `code:` URL — see Field 3.)*

### 25. Funder (OPTIONAL)
- **Funder:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

*NASA is the agency of both awards recorded in Field 26 — a grant it obligated in 2021 and the 2024
proposal NASA published an abstract for, whose selection is inferred in Field 26 — and NASA's own
record of each names cdflib as its subject, so Field 25 rule 8 qualifies NASA as their awarding agency.
Those records are the two proposal abstracts NASA published, which ADS indexes as `2020hdee.prop...14H` (NASA Proposal ID
20-HDEE20_2-0014, "Integrating the python XArray library and the CDF file format") and
`2024htm..prop...22H` (NASA Proposal ID 24-HTM24-0022), both by Bryan Harter (author 4) of the
University of Colorado Boulder. The first states "we propose that modules be added to the cdflib library
that enables the conversion of ISTP compliant CDF files to XArray DataSets objects" — the federal record
of the resulting grant names only XArray, and the link to cdflib runs through this abstract, whose first
sentence the grant's description reproduces (Field 26); the second, titled
"Sustaining and Enhancing cdflib: …", states "We are asking for support to maintain this critical tool".
The name is ROR's display name for `https://ror.org/027ka1x80` (rules 9–10), and every funder of a
recorded award appears here (rule 11): NASA is the funder of both awards in Field 26.*

*Where the evidence is, and is not. The repository contains no funding, grant, award or sponsor
statement at `cf7553f`, the DataCite record has an empty `fundingReferences` array, and the Zenodo
record has no grants. The funding was found through the literature search recorded under Field 27 and confirmed in
the federal award record (Field 26), not in the project's own files.*

*Considered and excluded:*
- *The Regents of the University of Colorado — the copyright holder named in `LICENSE` and the recipient
  of award 80NSSC21K0306; neither role makes it a funder.*
- *The NASA contracts in the PySPEDAS paper's funding statement (Grimes et al. 2022), including
  NNG17PZ01C for SPEDAS community support and NNG04EB99C for MMS SPEDAS plug-in development. They fund
  SPEDAS work described in a paper about a different product (rule 4).*
- *The MAVEN mission. Its Science Data Center produced cdflib (`2019AGUFMSH41C3312H`: "The MAVEN Science
  Data Center (SDC) has created several open-source software tools … specifically the cdflib, PyTplot,
  and PyDIVIDE libraries"), but no source states MAVEN funding for the software or names a MAVEN award
  (rule 7); the agency is already recorded.*

### 26. Award Title (OPTIONAL)
- **Award Title:** Integrating the python XArray library and the CDF file format
- **Award Number:** 80NSSC21K0306
- **Award Funder:** National Aeronautics and Space Administration (https://ror.org/027ka1x80)
- **Award Title:** Sustaining and Enhancing cdflib: A Python-First Common Data Format Library for the Heliophysics Community
- **Award Number:** 24-HTM24-0022
- **Award Funder:** National Aeronautics and Space Administration (https://ror.org/027ka1x80)

*Both awards are recorded under Field 26 rule 7: NASA's record of each names cdflib as the funded work
(quoted in Field 25). Neither is named in the repository or the DOI metadata.*

*`80NSSC21K0306`. USAspending (read 2026-10-28) records it as a NASA grant (assistance listing 43.001,
Science) to The Regents of the University of Colorado, running 2021-01-01 to 2021-12-31, with $18,485
obligated. Its description, "XARRAY IS AN OPEN SOURCE PYTHON LIBRARY THAT PROVIDES MULTI-DIMENSIONAL
DATA STORAGE WITH THEIR CUSTOM DATAARRAY AND DATASET DATA STRUCTURES.", is the first sentence of the
Background section of the 20-HDEE20_2-0014 proposal abstract, upper-cased, which ties the grant to that
proposal. The repository holds the funded work, written inside the award period: `709ae49` "First
commit of the CDF file to XArray Dataset function" (Bryan Harter, 2021-01-26) and `871d4bd` "Initial
commit of the xarray_to_cdf function" (2021-10-29), which at `cf7553f` live in `cdflib/xarray/`. Title:
the federal description is an abstract sentence, not a title, so the title is the proposal's own as
NASA's selected-proposal abstract gives it, in its own capitalisation, 61 characters (rules 9–10).
Number: the grant number as USAspending writes it; no award in HSSI carried it, in that or any
punctuation variant, before this entry (rule 13). The proposal ID is not used because the grant number
exists.*

*`24-HTM24-0022`. The record is NASA's published abstract of a selected proposal; the selection is
inferred from the ADS NASA-proposal collection. On 2026-10-28 that collection held only a subset of the
HTM-24 call's proposals, with gaps in their numbering, consistent with NASA's published abstracts of
selected proposals, and this project's HDEE-20 record in the same collection corresponds to the grant
above. No grant number was public on 2026-10-28: USAspending held no award whose
description carries `24-HTM24-0022`, `HTM24`, the title or its opening sentence, although other
ROSES-2024 awards open their descriptions with their proposal IDs (controls: `80NSSC25K7933`, opening
with `24-OSTFL24-0057`, and `80NSSC25K7754`, opening with `24-HSR24_2-0148`), and none of the NASA awards
to the University of Colorado active since 2024-10-01 has a description that mentions CDF. The proposal
ID is therefore the identifier, the form the NASA record gives (rule 13), as the catalogue already does
for another NASA award known only by its proposal ID. Title: the proposal's own, 105 characters, within
the 128-character limit. When a grant number (`80NSSC…`) is published for this award, a later refresh
should replace the identifier with it.*

*Funder. Each award's funder is the National Aeronautics and Space Administration, the agency that
made it, named as Field 25 records it — ROR's display name and `https://ror.org/027ka1x80` — so the
awards and Field 25 share one organization (rule 16). No award in the catalogue carried either number
before this entry.*

*Considered and excluded: the HDEE-20 proposal ID `20-HDEE20_2-0014` as a second identifier for the
first award (the grant number supersedes it), and the PySPEDAS paper's SPEDAS contracts (Field 25).*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.3389/fspas.2022.1020815 — Grimes, E. W., Harter, B., Hatzigeorgiu, N., et al. (2022), "The Space Physics Environment Data Analysis System in Python", Frontiers in Astronomy and Space Sciences
- https://doi.org/10.1029/2021JA029620 — Olshevsky, V., Khotyaintsev, Y. V., Lalti, A., et al. (2021), "Automated Classification of Plasma Regions Using 3D Particle Energy Distributions", Journal of Geophysical Research: Space Physics
- https://doi.org/10.3389/fspas.2022.1073578 — Palmroos, C., Gieseler, J., Dresing, N., et al. (2022), "Solar energetic particle time series analysis with Python", Frontiers in Astronomy and Space Sciences
- https://doi.org/10.1038/s41550-024-02278-9 — Yardley, S. L., Brooks, D. H., D’Amicis, R., et al. (2024), "Multi-source connectivity as the driver of solar wind variability in the heliosphere", Nature Astronomy
- https://doi.org/10.1029/2025SW004857 — Patrick, A. M., Coxon, J. C., Bentley, S. N., et al. (2026), "How Does the Definition of a Geomagnetic Storm Affect the Contents of the Resulting Storm List?", Space Weather
- https://doi.org/10.1029/2022JA031027 — Andrews, D. J., Stergiopoulou, K., Andersson, L., et al. (2023), "Electron Densities and Temperatures in the Martian Ionosphere: MAVEN LPW Observations of Control by Crustal Fields", Journal of Geophysical Research: Space Physics

*The repository, the DataCite record (empty `relatedItems`) and the Zenodo record cite no publication
beyond Zenodo's `isSupplementTo` link back to the GitHub source tree; the GSFC/SPDF URLs in the
repository are specification and user-guide documents, not publications about cdflib. Every entry above
comes from the literature. Titles and venues are as the DOI records give them.*

*Per entry. All six are peer-reviewed articles. The PySPEDAS paper enters under rule 3's platform
clause; the other five are publications about other work that is built with cdflib and that credit it
deliberately (rule 5). While cdflib's credited literature stays this small, each such use is news.
cdflib is widely used as a dependency of other software (Field 30), but few papers credit it by name,
and rule 5 turns on the credited papers.*
- *Grimes et al. 2022 (PySPEDAS), rule 3's platform clause: a paper by a cdflib developer about a
  platform cdflib serves. Bryan Harter, cdflib author 4, is the paper's second author, and its
  author-contribution statement says "BH contributed to the development of cdflib, PyTplot, as well as
  the MAVEN plug-in." It covers PySPEDAS, the Python version of the Space Physics Environment Data
  Analysis System, whose load routines are built on open-source projects including PyTplot and cdflib,
  and whose PyTplot file importers read CDF files through cdflib. Its other references to cdflib are enumerations of
  packages (the abstract's list of projects PySPEDAS builds on, the importers' list of libraries, and the
  Acknowledgments' thanks to "the developers of the PyTplot, numpy, cdflib, netCDF4, hapiclient, astropy,
  and requests packages"), which would not by themselves be a deliberate credit under rule 5.*
- *Olshevsky et al. 2021, methods: "The datasets are saved and loaded in CDF files using the
  open-source cdflib module (MAVEN SDC, 2021)" (read in the arXiv version, arXiv:1908.05715).*
- *Palmroos et al. 2022, methods: the package's multidimensional CDF loaders "exploit the Python
  package cdflib (Stansby et al., 2022)" (read in the arXiv version, arXiv:2210.10432).*
- *Yardley et al. 2024, methods: the level 3 files downloaded from SOAR, the Solar Orbiter archive,
  were "read into Python using the cdflib module", citing its Zenodo DOI.*
- *Patrick et al. 2026, Data Availability Statement: "OMNI CDF files were read in Python using cdflib
  version 1.2.3 (Stansby et al., 2022)."*
- *Andrews et al. 2023, Data Availability Statement, after the links to the LPW, MAG and SWIA data:
  "The authors thank the MAVEN Science Data Center team for provision of code in particular the cdflib
  python package." This is the paper's only mention of cdflib (read on the publisher's page); its
  Acknowledgments section funds one author and does not name the software.*

*The line drawn between rules 5 and 6: a sentence that singles cdflib out — stating what it did in
the work, or thanking its providers for it — in the methods, an acknowledgement or a data statement, is
a deliberate credit; a name in an enumeration of packages, an AAS "Software:" list included, is not.*

*Weighed and excluded, recorded so a later refresh does not rediscover them as new.*

*Not an eligible publication (rule 1):*
- *Harter, B., Jr., Barnum, J. & Ware, A. (2019), "Open Source Python Libraries for Visualization and
  Manipulation of Space Physics Data, Developed by the MAVEN Science Data Center", AGU Fall Meeting
  Abstracts, SH41C-3312 (https://ui.adsabs.harvard.edu/abs/2019AGUFMSH41C3312H/abstract). It is the
  developers' own presentation of cdflib, PyTplot and PyDIVIDE as the MAVEN SDC's libraries, describing
  cdflib as "a python-native library for reading and writing .cdf files", but it survives only as an
  ADS meeting abstract, which is never eligible. No poster or paper of the presentation is deposited:
  title searches at Zenodo, DataCite and Crossref, and Zenodo creator-keyed searches for Bryan Harter (by
  name and ORCID) and Julie Barnum, find none (controls: the Zenodo and DataCite title searches find the
  2025 poster listed below, and the Crossref search finds Burrell et al. 2018). A deposited copy of the
  poster would be a rule 3 candidate.*
- *Meeting abstracts that also name cdflib only among other tools: Hartnett & Robbertz, AGU 2024
  (`2024AGUFMSM43C2856H`, about SAMMI), and Candey et al., AGU 2018 (`2018AGUFMIN11D0651C`). A deposited
  poster of either would fail rule 6 as well.*
- *The two NASA proposal abstracts (`2020hdee.prop...14H`, `2024htm..prop...22H`): award records,
  carried by Fields 25–26, not publications.*
- *Three Zenodo records that name cdflib in passing: the data and code deposited for a substorm study
  (https://doi.org/10.5281/zenodo.18493818), whose scripts "rely on standard scientific libraries"
  including cdflib; a reproducibility package for a study of financial multifractal cascades
  (https://doi.org/10.5281/zenodo.20006731), which lists cdflib among its dependencies "for the
  solar-wind CDF reader"; and "Space Atlas: Phase I scaffold and cislunar benchmark for the Nervous
  Machine causal-learning framework" (https://doi.org/10.5281/zenodo.20563338), whose data-access notes
  say "cdflib parser used (pure-Python, pip-installable)". Zenodo types them as other material, a
  dataset and a project deliverable; none is an article, a preprint or a technical report.*
- *Zenodo software deposits that name cdflib are software, not publications: solo-epd-loader,
  mag-noise/crm and pysatNASA (ADS `full:"cdflib"`), kylermurphy/gmag
  (https://doi.org/10.5281/zenodo.10472150, "kylermurphy/gmag: Updates for Pandas 2.0.2 and cdflib
  1.0.4", found through the DataCite query `query=cdflib`), and a coincidence detector for decametric
  radio networks (https://doi.org/10.5281/zenodo.22949729, Zenodo free-text `cdflib`).*

*A section on cdflib in a paper about something broader (rule 3):*
- *Burrell et al. 2018, "Snakes on a Spaceship—An Overview of Python in Heliophysics"
  (https://doi.org/10.1029/2018JA025877). It is more than a mention: its appendix section A.3.1,
  "CDFlib", describes the package, and two cdflib authors, Angeline Burrell (author 3) and David Stansby
  (author 12), are among its ten authors. Its subject, though, is Python in heliophysics generally — a
  survey of some thirty community packages — not this software, so rule 3 does not fire, and a survey is
  not a use of the software under rule 5. It is excluded on that ground.*

*Mentions only (rule 6):*
- *Vogt et al. 2020, Earth and Space Science (https://doi.org/10.1029/2019EA000953): "CDF files are read
  using CDFlib" inside an enumeration of the tool's dependencies.*
- *Bendt et al. 2024, ApJ 971, 179 (https://doi.org/10.3847/1538-4357/ad54bc), and Bendt & Chapman 2026,
  ApJL 998, L2 (https://doi.org/10.3847/2041-8213/ae3820): AAS "Software:" lists.*
- *Agarwal et al. 2026, Space Weather (https://doi.org/10.1029/2025SW004911): "All plots in this study
  are produced using open-source Python 3.9.18 packages, including NumPy, Matplotlib, cdflib, and
  datetime." (read in the arXiv version, arXiv:2604.08842).*
- *Jebaraj et al. 2026, arXiv:2610.08034 (https://doi.org/10.48550/arXiv.2610.08034): a software list
  beside numpy, scipy, matplotlib and PyWavelets.*
- *Salemi et al. 2025, arXiv:2510.01285: cdflib appears in a list of per-format file loaders.*
- *Martinez, Hartnett & Barnum 2025, "Strengthening Open Source Practices in Heliophysics"
  (https://doi.org/10.5281/zenodo.17370636), a deposited poster, an eligible type, on open-source
  practice drawn from the IMAP science data center and PyHC tools. Julie Barnum is author 2, but its
  subject is not cdflib, and its record names cdflib only in a list: "existing PyHC open source tools
  within IMAP - such as cdflib, SAMMI, and space-packet-parser".*

*Not about this software:*
- *The developers' other deposits that the creator-keyed searches find — posters on the MAVEN SDC's
  legacy-code modernization (2024) and on science data system papers (2025), an IHDEA 2026 presentation
  on the ISTP metadata guidelines, and PyHC and HSSI talks and meeting reports — are not about cdflib,
  and their Zenodo records do not name it.*
- *The other hits are about CDFLIB, the unrelated Fortran library of cumulative distribution functions
  (Brown, Lovato and Russell): confirmed from the text for five papers in numerical methods, machine
  learning, ecology and hydrology; SciPy 1.0 bundles that library; and a GWAS paper
  (`2015trus....3...46L`) was not read.*

*Search record (ADS/SciX API, 2026-10-28, all years): `full:"cdflib"`, `abs:"cdflib" OR
title:"cdflib"`, `ack:"cdflib"` (the two Bendt papers) and `body:"cdflib"`; controls:
`full:"xyzzyqwertcdf"` returns 0, and `full:"pyspedas"` returns hits. Records entered since
2026-07-29: only Jebaraj et al. DataCite reports no citations of the concept DOI. Zenodo (2026-10-29):
free-text `cdflib` (control: `xyzzyqwertcdf` returns 0), the creator-keyed searches, and the title
searches for the 2019 presentation recorded above.*

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

*`SpacePy` and `pycdfpp` are included as same-purpose peers. Field 29 covers "[s]oftware that
performs similar tasks but does not necessarily link together", and names "a package performing
similar tasks" as its first qualifying category; unlike Field 30 it does not
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

*Considered and rejected:*
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

*Considered and excluded:*
- *`numpy` — Tier A, no exceptions.*
- *`netCDF4` / `h5netcdf` — Tier B, but the documented exchange is with xarray: the netCDF-to-CDF
  workflow reads through `xarray.load_dataset` and these are only the engines xarray selects. cdflib
  has no netCDF API of its own, so no direct exchange is demonstrated. (The workflow itself is
  recorded in Field 18.)*
- *`boto3` / `botocore`, `pooch`, `pytest`, `pytest-remotedata`, `hypothesis`, `matplotlib`,
  `mkdocs*`, `ipython`, `pre-commit` — generic infrastructure and tooling.*
- *Blanket ecosystem claims — cdflib is widely used downstream (PySPEDAS, pytplot, sunpy, pysat and
  others read CDFs through it), but "part of the standard scientific Python ecosystem" and "a PyHC member,
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

*This is an exclusion, not a resolution failure. The `InstrumentObservatory` vocabulary has
SPASE-identified rows for the missions and instruments listed above, so these entries were dropped
for irrelevance, not for want of a match. No name is emitted without a
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
`logo: https://avatars3.githubusercontent.com/u/22352442?s=460&v=4` for CDFlib, which served a PNG
on 2026-10-28. Declined on three grounds — it is the **GitHub organization avatar of MAVENSDC**, the
organization the project has since moved away from (Field 3), not a logo for cdflib itself; a GitHub
avatar URL carrying `?s=460&v=4` sizing parameters on the legacy `avatars3.` shard host is not the
"permanent place" Field 33 requires; and PyHC's entry for this project is demonstrably stale in its
other URLs too.*

## Durable catalog notes

- Field 6 keeps the record's established 15-author set. Its source-form variants and shared-identity
  evidence are recorded with the relevant authors so they are not mistaken for distinct people in later
  maintenance. Hugo van Kemenade's ORCID is verified.
- Fields 31 and 32 are empty because cdflib is mission-agnostic; mission and instrument names in tests
  and examples do not establish scientific support.
- The releases 1.3.13 through 1.3.16 (`a536244..cf7553f`) fixed bugs in existing paths: reading a
  variable with no written records, the pad-value offset of NOVARY zVariable dimensions, the `.cdf`
  fallback for a non-existent path, datetime conversion under NumPy 2.5, TT2000 leap-second breakdown
  and unix-time mapping, and the CDF type `xarray_to_cdf` gives epoch `FILLVAL`/`VALIDMIN`/`VALIDMAX`
  attributes. They added or removed no capability, format, data source, dependency, platform or
  language, and left `pyproject.toml`, `README.md`, `mkdocs.yml`, `LICENSE` and `.github/` unchanged, so
  the repository evidence the other sections cite from the Source Revision reads the same at `cf7553f`.
