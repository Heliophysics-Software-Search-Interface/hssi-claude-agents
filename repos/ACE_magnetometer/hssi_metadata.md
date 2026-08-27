# HSSI Metadata Extraction Results

**HSSI Software ID:** 6cd949ce-78fd-4c77-ae81-4812f02b02e0
**Repository:** https://github.com/space-physics/ACE_magnetometer
**Source Revision:** 1656d1c2ab5efaa04de1c8137e1a3a304e4d356d
**Extraction Date:** 2026-08-27
**Validation Date:** 2026-08-27
**Validation Status:** PASS

---

## Scope note

Three things change how the evidence below should be read.

**The upstream repository is archived on GitHub and read-only.** The pinned revision above is the last
upstream commit (2021-04-27, "Delete FUNDING.yml"). Barring an un-archive by the owner, the repository
evidence in this dossier is terminal: a future refresh should expect the same tree, the same sole
release, and the same author. What can still change is external context — a DOI minted later, a SPASE
record added for the data product, or HSSI's own controlled vocabularies.

**The software handles the ACE Science Center *browse* product, not ACE Level 2 data.** Every value
below that concerns data — data sources, input formats, instruments, datasets — turns on this. On its
browse-parameter information page, https://izw1.caltech.edu/ACE/ASC/browse/browse_info.html, the ACE
Science Center states that browse parameters "are not suitable for serious scientific work, and should
not be cited without first consulting the appropriate ACE instrument team", and are produced
automatically during level-one processing without science-team verification. The header of the sample
file shipped in `tests/` repeats the caveat. This is a property of the upstream data product, not a
defect in the software, but it is why the Level 2 dataset DOI is deliberately *not* recorded in Field 28.

That page is the source of the ACE Science Center quotations below, except where a passage attributes
one to the header of the sample browse file in `tests/`, which is resolvable inside the repository at
the pinned revision. Anyone verifying a quotation should fetch `browse_info.html` itself: the archive
directory one level up (https://izw1.caltech.edu/ACE/ASC/browse/, cited in Field 28 for a different
purpose) is a bare file listing carrying none of this prose, so a quotation checked against it will
appear — wrongly — to be unsupported.

A third, purely local point: a working copy of this repository may carry untracked files left by
earlier tooling — an automated repository-metadata scan and copies of the PyHC registry YAMLs, dated
2025-12. They are not part of the repository at the pinned revision and are stale relative to their
own upstream sources. They are not evidence for anything in this dossier.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The bracketed placeholder is the catalogue convention for a record whose submitter is supplied at
submission time. It is not a missing value.

### 2. Persistent Identifier (RECOMMENDED)
Not found.

The repository at the pinned revision contains no `CITATION.cff`, no `.zenodo.json`, no
`codemeta.json`, and no DOI badge — the README's only badges are the GitHub Actions CI badge and two
PyPI badges. A Zenodo record search for `ACE_magnetometer` returns no hits; a DataCite DOI query for
`ACE_magnetometer` returns zero results, as does one for creator "Hirsch, Michael" restricted to ACE
titles. Worth noting for context: the author maintains his own Zenodo API client (`pyzenodo3`), so
unfamiliarity with DOI minting is not the explanation — this software simply has no DOI.

This agrees with the empty value already stored in HSSI. If a DOI is ever minted for the archived
repository, it would also supply Field 12's Version PID.

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/ACE_magnetometer

This is the canonical `full_name` GitHub reports for the repository, and the URL recorded in the PyHC
project registry — whose ACEmag entry sits in the unevaluated-packages list,
https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects_unevaluated.yml,
rather than the core or community lists a reader would check first. `setup.cfg` and the README badges
spell it lowercase (`https://github.com/space-physics/ace_magnetometer`); GitHub resolves that
spelling to the same repository, but the mixed-case form is the canonical one and is what is recorded.

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: Line Plots

**Evidence for each retained value.**

- *Data Access and Retrieval* — `ace_magnetometer.download()` opens an anonymous FTP session to
  `mussel.srl.caltech.edu`, changes to `/pub/ace/browse/MAG16sec/<year>`, and retrieves
  `ACE_MAG16_<year>-<doy>_V3-3.zip` by binary transfer, skipping files already present. `DownloadACE.py`
  exposes this as a date-and-path command line.
- *Processing* — `ace_magnetometer.load()` opens the retrieved ZIP, parses the whitespace-delimited
  ASCII table inside with a comment-stripping reader, selects nine of its columns, converts the ACE
  epoch column (seconds since 1996-01-01) into a datetime index, and drops the raw time column,
  returning a time-indexed table. The MATLAB `loadACEhdf.m` performs the analogous job for HDF browse
  files: it reads the `fp_year` vector, finds the record range covering the requested interval, and
  reads only those records for the requested fields.
- *Line Plots* — `PlotACE.py` draws three stacked shared-x line panels (RTN components; GSE
  components; total field and `dBrms`) with a UTC time axis; `matlab/PlotACE.m` draws one line panel
  per requested MAG field over a MATLAB date axis.
- The two parent categories are required because their subcategories are selected.

**`Data Visualization: 2D Graphics` was carried on this record earlier and has been dropped.** The
classification guidance defines *2D Graphics* as static two-dimensional plots of the contour / heatmap
/ image kind, whose indicators are `pcolormesh`, `imshow`, contour calls and 2D maps. Neither workflow
produces any of those: the Python plotter calls the pandas line-plot wrapper and MATLAB's `plot`, and
every figure the package makes is a line plot already covered by *Data Visualization: Line Plots*.
Under a looser reading — "any static 2D figure" — the value would be merely redundant rather than
wrong, so dropping it sharpens the classification rather than correcting an outright error. It should
not be re-added on the strength of "the package draws two-dimensional figures."

**Considered and not selected.**

- *Coordinate Transforms* (and its Heliospheric / Magnetospheric children) — tempting because the data
  carry both RTN and GSE components, but the transformation is done upstream. The browse file header
  reads "16-second average Interplanetary Magnetic Field in RTN and GSE Coordinates", and the software
  merely selects the already-computed columns; the MATLAB path likewise reads pre-computed
  `B_rtn_theta_MAG` / `B_rtn_phi_MAG` angles. The pinned revision's Python and MATLAB sources contain
  no coordinate-transform code.
- *Data Processing and Analysis: Time Series Analysis* — the closest near-miss, and worth recording so
  it is not re-litigated blind. The package does build a pandas time-indexed series, and the MATLAB
  path selects records by time range. But the category means analysis *of* time-ordered data — temporal
  filtering, trend estimation, autocorrelation — and the package performs none. Constructing the index
  and subsetting by date are covered by *Processing*.
- *Data Processing and Analysis: Data Reduction* — the 16-second averaging that defines this product is
  performed by the ACE Science Center during level-one processing, not by this software: the
  browse-parameter information page pinned in the Scope note records that browse parameters are "created
  at the Science Center during level one processing" and that "MAG browse data is reported with 16-second
  time resolution". The package neither averages, bins, nor downsamples.
- *Data Processing and Analysis: Analysis* — the catch-all is easy to over-apply. No derived physical
  quantity is computed here: `Btotal` and `dBrms` are columns in the source file, not calculations.
- *Data Processing and Analysis: File Format Conversion* — `download()` writes the retrieved ZIP
  byte-for-byte; `load()` returns an in-memory table and writes nothing. Nothing is converted between
  file formats.
- *Mission-related* (and *Mission-related: Monitoring*) — the browse product exists for monitoring, and
  a reader might extend that to the tool. But this category is for software that is part of a mission's
  ground system or operations pipeline. This is a third-party reader of a public archive, written by
  someone outside the ACE team.
- *Models and Simulations*, *Servers and Environments* — nothing in the package models, simulates, or
  serves anything.

### 5. Related Region (MANDATORY)
- Interplanetary Space
- Solar Wind

The Region vocabulary is flat: no row implies any other, so each value is argued on its own evidence
and neither argument below depends on the other.

**Interplanetary Space** — ACE observes from a halo orbit about the Sun–Earth L1 point, and the data
product this software handles is titled, in the file header written by the ACE Science Center,
"16-second average Interplanetary Magnetic Field in RTN and GSE Coordinates". The region the
measurements are made in is interplanetary space. This value is already stored in HSSI and is confirmed.

**Solar Wind** — the quantity delivered is the magnetic field carried by the solar wind
plasma streaming past L1; ACE's magnetometer is one of the standard upstream solar wind monitors, and
the ACE Science Center names the solar wind first when it states, on its browse-parameter information
page (https://izw1.caltech.edu/ACE/ASC/browse/browse_info.html), what the browse parameters are for:
"Their purpose is to allow monitoring of the solar wind and large-scale particle and magnetic field
behavior, and selection of interesting time periods for more intensive study." A researcher filtering
HSSI by the Solar Wind region would expect an ACE MAG reader to come back. The argument is independent
of the Interplanetary Space argument: that one is about where the spacecraft sits, this one is about
which medium is being sampled.

The case against it is narrow, and is recorded so it is not re-raised as though it were new: the
software itself contains no solar-wind-specific processing. But Field 5 asks which regions the
functionality is used for, not which regions the code names.

That purpose sentence is reproduced above in full because a composite paraphrase of it — solar wind
behavior, particle fluxes, and magnetic fields — was previously presented in quotation marks as if it
were the source's wording. That continuous phrase does not occur on the browse-parameter information
page cited above. "particle fluxes" does occur there, but in two unrelated sentences: one listing the
charged particle fluxes the browse data contain, and one advising caution during periods of intense
particle fluxes. Neither concerns the purpose of the browse parameters. The Solar Wind argument never
depended on the paraphrase, and the paraphrase must not be reintroduced as a quotation.

**Considered and rejected.**

- *Earth Magnetosphere*, *Earth Inner Magnetosphere*, *Earth Outer Magnetosphere*, *Earth Magnetosheath*,
  *Earth Magnetotail* — L1 is roughly 1.5 million km sunward of Earth, far upstream of the bow shock;
  none of these regions is sampled. Note for future refreshes: the PyHC registry entry for ACEmag carries
  the keywords `magnetosphere`, `ionosphere_thermosphere_mesosphere` and `specific`. Those are a coarse
  topical tagging rather than a region assignment: `magnetosphere` there records that ACE data feed
  magnetospheric research, which is not evidence for an HSSI Earth-magnetosphere region and must not be
  re-imported as one. The same entry's `ionosphere_thermosphere_mesosphere` keyword, applied to a
  spacecraft at L1, shows how coarse the tagging is.
- *Heliosheath*, *Solar Environment*, *Corona*, *Photosphere*, *Chromosphere*, *Solar Interior* — remote
  or distant regions the instrument does not observe.
- The planetary magnetosphere rows — no planetary data path exists in the package.

### 6. Authors (MANDATORY)
- **Author:** Michael Hirsch
  - **Author Identifier:** https://orcid.org/0000-0002-1637-6526
  - **Affiliations:**
    - **Organization:** Boston University — **Affiliation Identifier:** https://ror.org/05qwgg493
    - **Organization:** Scivision, Inc. — **Affiliation Identifier:** Not found

`setup.cfg` names "Michael Hirsch, Ph.D." as the sole author, and he is the only contributor to the
code: at the pinned revision every commit is his, under two GitHub-noreply addresses
(`scivision@users.noreply.github.com` and `10931741+scivision@users.noreply.github.com`), and GitHub's
contributor list for the repository shows only `scivision`. The single-author list is therefore
complete rather than merely unchallenged. (The one later commit in this working copy is a local
metadata commit by the HSSI cataloguing effort, not upstream authorship.)

The ORCID and both affiliations come from the existing HSSI record and are retained in full. An earlier
extraction of this repository recorded the author identifier and affiliation as "Not found", because
no tracked file at the pinned revision mentions an ORCID, a ROR, Boston University or Scivision — HSSI
is the richer source here, and its values supersede that verdict rather than the other way round.

The ORCID is corroborated rather than taken on trust: 0000-0002-1637-6526 belongs to a Michael Hirsch
whose public record lists a Boston University Ph.D. and M.E. in Electrical Engineering, a Boston
University research scientist post in the ECE department from 2018-08, and works including *PyMap3D:
3-D coordinate conversions for terrestrial and geospace environments* and a series of auroral and
ionospheric papers. PyMap3D is a package in the same author's GitHub organizations, so the identity
match is on published software as well as on name and field. The Boston University ROR
https://ror.org/05qwgg493 resolves to Boston University.

**Scivision, Inc. deliberately carries no identifier.** A ROR API query for `Scivision`
(`https://api.ror.org/organizations?query=Scivision`) returns a single organization: SciVision Biotech
Inc., a biotechnology company in Kaohsiung, Taiwan, https://ror.org/011qev639. It is unrelated to this
author, and that ROR must not be attached to him. Scivision, Inc. is the author's own consultancy (the
GitHub handle `scivision`); no ROR record for it surfaced under that query, so the affiliation is
recorded without an identifier — the correct representation on the available evidence, not an
incomplete one.

### 7. Software Name (MANDATORY)
ACEmag

The PyHC project registry lists this software as `ACEmag` with `code:
https://github.com/space-physics/ACE_magnetometer`, and that curated name is what HSSI stores. Two
alternatives exist and were not chosen: the Python distribution name `ace_magnetometer` (`setup.cfg`)
and the GitHub repository name `ACE_magnetometer`. Both are machine identifiers rather than a display
name, and switching to either would break continuity with the PyHC listing for no gain.

### 8. Description (MANDATORY)
ACE_magnetometer provides Python and MATLAB tools for working with 16-second ACE satellite magnetometer
data. The Python workflow downloads and loads ACE archive files and plots IMF components including Br,
Bt, Bn, Bx, By, Bz, Btotal, and dBrms, while the MATLAB workflow reads local ACE HDF files and plots the
RTN field components and direction angles over a requested time range.

**This text is a factual correction of an earlier description, not a rewrite.** The superseded wording
was:

> ACE_magnetometer provides Python and MATLAB tools for working with 16-second ACE satellite
> magnetometer data. The Python workflow downloads and loads ACE archive files, while the MATLAB
> workflow reads local ACE HDF files and plots IMF components including Br, Bt, Bn, Bx, By, Bz, Btotal,
> and dBrms.

In that sentence the component list attaches to the MATLAB clause, which misstates the code in two ways.
The eight named components — Br, Bt, Bn, Bx, By, Bz, Btotal, dBrms — are precisely the columns
`load()` extracts and `PlotACE.py` plots, i.e. the *Python* path. The MATLAB path requests a different
field set from the HDF file (`B_rtn_r_MAG`, `B_rtn_t_MAG`, `B_rtn_n_MAG`, `B_rtn_theta_MAG`,
`B_rtn_phi_MAG`) and plots the three RTN components in nT plus two direction angles in degrees; it never
touches Bx/By/Bz, Btotal, or dBrms. The stored sentence also leaves the Python workflow appearing not
to plot at all, which is the package's headline capability.

The correction above is a minimal splice: the same two-clause sentence, the same vocabulary and
punctuation, with the component list moved to the workflow that actually produces it and the MATLAB
clause described accurately. The prior submitter's phrasing and structure are otherwise preserved
deliberately — this is a factual fix, not a stylistic preference.

Two durable facts about the software that a future editor may want in the description but that are
absent from both versions: the MATLAB workflow's input file path is hard-coded inside `PlotACE.m`
(`~/data/ACE/ACE_BROWSE_2013-001_to_current.HDF`), so a user must edit the script; and the MATLAB
workflow has no download step, so the HDF file must be obtained separately.

### 9. Concise Description (OPTIONAL)
Python and MATLAB tools to retrieve, load, and plot 16-second ACE magnetometer data from the ACE archive.

Carried over from the existing HSSI record unchanged. It is accurate at the package level and well
within the 200-character preview budget. One nuance, recorded so it is not mistaken for an error later:
retrieval is a Python-only capability — the MATLAB scripts read a local file. The sentence describes
what the package as a whole offers, which is the intended reading of a preview line, so it was left
alone rather than lengthened.

### 10. Publication Date (RECOMMENDED)
2017-03-14

The repository was created 2017-03-14T21:03:44Z and its initial commit carries the same timestamp
(2017-03-14T17:03:44-04:00). Both give 2017-03-14 in UTC. This matches the stored value.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

With no DOI (Field 2), the form's instruction is to name the repository host, and GitHub is where the
software is distributed from.

**Zenodo and PyPI were both checked and neither is the publisher.** There is no Zenodo record. The
README displays two PyPI badges — a supported-Python-versions badge and a download-count badge, both
keyed to `ace_magnetometer` — but `https://pypi.org/pypi/<name>/json` returns 404 for
`ace_magnetometer`, `ace-magnetometer`, `ACEmag` and `acemag`. PyPI normalizes project names by
case-folding and collapsing runs of `-`, `_` and `.` to a single `-`, so those four probes cover every
separator and case variant of the two plausible names; the absence is not an artifact of spelling.
Those badges are aspirational, or point at a distribution that is not on PyPI; either way they render
broken. This is worth keeping on the record because the badges are the one thing in the repository that
might otherwise be read as evidence of a PyPI publication.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.9.0
- **Version Date:** 2018-07-25
- **Version Description:** Uses zip files with ascii data inside
- **Version PID:** Not found

Re-derived from the repository and its GitHub release rather than from any DOI autofill. There is a
single release: tag `v0.9.0`, titled "initial release", published 2018-07-25T02:53:18Z, with the body
"Uses zip files with ascii data inside". The tag points at commit
`7e1e3fe797e3bc9b649b2d7d2f0378f3608afa46`, dated 2018-07-24 22:52:35 -0400 — 2018-07-25 in UTC, which
is the date recorded.

**No version bump has occurred and none is expected.** `setup.cfg` gained `version = 0.9.0` in the
2018-07-24 packaging commit, and that line reaches the pinned revision unchanged even though later
commits rewrote much of the file around it. The seven commits after the `v0.9.0` tag moved the MATLAB
scripts into `matlab/`, adjusted install prerequisites, migrated CI from Travis and AppVeyor to GitHub
Actions, and finally deleted `.github/FUNDING.yml`; none of them altered the version. With the
repository archived, `v0.9.0` is final.

The version string is recorded with the `v` prefix, matching the Git tag and the GitHub release rather
than the bare `0.9.0` in `setup.cfg`; both denote the same release. Version PID is empty because no DOI
exists for any version.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- MATLAB

Python: `setup.cfg` declares `python_requires = >= 3.6.2` and classifiers for Python 3.6, 3.7 and 3.8;
the package and both entry-point scripts are Python 3. `Python 2.x` is excluded by the requirement.
MATLAB: four `.m` files under `matlab/` implement an independent load-and-plot workflow
(`PlotACE.m`, `loadACEhdf.m`, `datenum2DOY.m`, `datenum2fpYear.m`). Both values are already stored and
are confirmed.

### 14. Reference Publication (RECOMMENDED)
Not found.

No paper describes this software. The repository cites none; the author's JOSS papers are PyMap3D and
h5fortran, and a JOSS search for an ACE magnetometer paper returns only an unrelated pharmacokinetics
application; and the author's public ORCID work list — 18 entries as of this extraction, spanning
auroral, ionospheric and Fortran-tooling topics — contains no ACE magnetometer software paper. The ACE
MAG instrument paper is not a substitute: it describes the hardware, has no connection to this
package, and is not cited anywhere in the repository.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html

`LICENSE.txt` at the pinned revision is the standard
MIT License text, "Copyright (c) 2017 Michael Hirsch, Ph.D."; `setup.cfg` points `license_files` at it;
and GitHub's own license detection reports MIT (`spdx_id: MIT`). `MIT License` is the exact name of the
row in HSSI's license vocabulary, so no near-miss substitution is involved.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- ace
- geoscience
- geospace
- IMF
- magnetic field
- magnetometer
- python
- satellite-magnetometer
- solar wind

Eight of the nine are exactly the repository's own declared terms, and their split is worth recording
because it explains the mixed casing: `ace`, `geoscience`, `magnetometer`, `python`,
`satellite-magnetometer` are the five GitHub repository topics (lower-case and hyphenated by GitHub's
own rules), while `IMF`, `magnetic field`, and `geospace` are the three keywords listed in `setup.cfg`,
whose capitalization of the acronym is the author's. That casing is reproduced exactly as those two
sources write it, and should not be normalized.

The ninth, `solar wind`, is the companion of the Solar Wind region (Field 5) and phenomenon (Field
22). It is the term a user is most likely to search for when looking for upstream IMF monitor data,
and it already exists in the keyword vocabulary, so recording it reuses that term rather than
minting a near-duplicate. It is deliberately not sourced from the repository: no tracked file at the
pinned revision contains the phrase, in any casing. Considered and not added: `interplanetary
magnetic field` (already represented by `IMF`) and `space weather` (the browse product is explicitly
unsuitable for the operational use that term implies).

### 17. Data Sources (OPTIONAL)
- FTP/FTPS Directories
- Observatory/Mission-specific

`ace_magnetometer/__init__.py` hard-codes
`URL = 'ftp://mussel.srl.caltech.edu/pub/ace/browse/MAG16sec/'` and retrieves files with Python's
`ftplib` over anonymous FTP — a literal FTP directory source. That host is the ACE Science Center at
Caltech's Space Radiation Laboratory, an archive serving one mission's data, which is what
`Observatory/Mission-specific` denotes; per the form's own instruction, selecting it is paired with
naming the mission in Field 32, which this record does. The source was confirmed live at this
extraction: the 2013 directory serves 365 files named exactly as `date2filename()` constructs them
(`ACE_MAG16_2013-001_V3-3.zip` and so on), so the download path still works despite the software being
archived.

Both values are already stored and are confirmed. **Considered and rejected:** `HTTP/HTTPS
Directories` (the pinned revision's Python sources reach the network through `ftplib` alone, with no
HTTP client), and `CDAWeb`, `HAPI`, `AMDA`, `OMNIWeb`, `SSCWeb` — all of which do serve ACE
magnetometer data, none of which this software touches. That last point is the durable one: a future
agent who reasons "ACE MAG is on CDAWeb" would be describing the mission, not this package.

### 18. Input File Formats (RECOMMENDED)
- ascii
- Other

*ascii* — the Python path's actual data format. The retrieved ZIP contains a single whitespace-delimited
ASCII table with `#`-prefixed header lines, read with a whitespace-separator, comment-stripping reader.
The sample file in `tests/ACE_MAG16_2013-043_V3-3.zip` shows the format directly, including the ACE
Science Center header block and columns for SCclock, ACE epoch time, RTN and GSE components.

*Other* — carries two things that have no row of their own. First, the MATLAB path's HDF input.
Second, the ZIP container itself, which the Python path opens rather than treating as an opaque
download.

**`HDF5` was considered and deliberately rejected.** `loadACEhdf.m` uses MATLAB's `hdfinfo`/`hdfread`
and addresses the file through `statHDF.Vgroup(1).Vdata` — Vgroup and Vdata are HDF4 constructs, and
MATLAB's HDF5 access goes through a different interface (`h5info`/`h5read`). The ACE Science Center's
browse HDF files are HDF4. The docstring inside `loadACEhdf.m` says "filename of HDF5 datafile to read",
which is where a future extraction is most likely to go wrong: the comment is inaccurate, and the API
calls are authoritative. Since HSSI's file-format vocabulary offers `HDF5` but no HDF4 row, recording
`HDF5` would assert a format the software cannot read. `Other` is the correct representation.

**`csv` was also rejected.** The Python loader calls a CSV-reader function, but with a whitespace
separator on a fixed-width ASCII table containing no delimiter-separated values. The format is ascii;
the reader's name is an implementation detail. `CDF`, `netCDF3/4`, `FITS`, `JSON`, `IDL.sav`,
`ISTP-Compliant` and `Zarr` have no code path.

### 19. Output File Formats (RECOMMENDED)
Not found — deliberately empty.

The package writes no data product. `PlotACE.py` ends in an interactive `show()`; nothing calls a
figure-save function, and the MATLAB script likewise draws to a figure window. The one file the package
writes is the byte-for-byte copy of the retrieved `.zip`, which is a cached input rather than an output
format. Because a displayed matplotlib or MATLAB figure can be saved by hand, one could argue for
image formats here — but the file-format vocabulary is aimed at data interchange formats and contains no
image row, and "the user could click Save" is not software functionality.

This matches the empty value stored in HSSI, and the emptiness is a finding rather than a gap.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Operating System Independent
- Windows

`setup.cfg` classifies the package `Operating System :: OS Independent`, and the CI workflow proves the
claim on three platforms: a `linux` job on `ubuntu-latest` running lint, type-check and tests, and an
`integration` job matrixed over `windows-latest` and `macos-latest` running the test suite. Recording
both the specific platforms and the independence claim is intentional: the specific rows are what a
user filters on, the independent row is what the author asserts. All four are already stored and are
confirmed.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Pure Python with no compiled extension: `setup.py` is a bare `setup()` call, `pyproject.toml`
requires only setuptools and wheel, and the pinned revision's tracked files contain no C or Fortran
source and no compiled-extension build step. The MATLAB scripts are interpreted likewise. Specific
architecture rows (`x86-64`, `Apple Silicon arm64`, `Linux aarch64 or arm64`) were considered and
rejected: enumerating them would imply the package is built per-architecture, which would be less
accurate than the independence claim, not more precise.

### 22. Related Phenomena (OPTIONAL)
- Solar Wind

An earlier extraction of this repository recorded "Not found", reasoning that the repository names no
phenomenon explicitly. That verdict rested on an outdated picture of the phenomena vocabulary, taken to
lack both `Solar Wind` and `Geomagnetic Storms` while carrying a `Coronal Holes` row that the live
vocabulary does not have. The field was therefore re-tested against the current vocabulary rather than
inherited, and `Solar Wind` is what that test returned.

The case for `Solar Wind`: the sole data product the software retrieves, loads and plots is the in-situ
magnetic field of the solar wind at L1. The ACE Science Center gives the purpose of the browse
parameters as allowing "monitoring of the solar wind and large-scale particle and magnetic field
behavior, and selection of interesting time periods for more intensive study", naming the solar wind
first. (Field 5 quotes that sentence in full, with the URL of the page it appears on, and records the
composite paraphrase that must not be requoted in its place.) The field components this package plots
(RTN and GSE, plus total field and its RMS fluctuation) are the standard quantities of solar wind
magnetic field study. Field 22 asks which phenomena the software supports science functionality for,
and this is the one.

The case against, recorded honestly: the package implements no phenomenon-specific capability — no
shock or discontinuity detection, no ICME or magnetic cloud identification, no derived index. A strict
reading in which Field 22 is reserved for software that *analyses* a phenomenon would leave the field
empty. The looser reading, which the field's own wording supports, is the one adopted here.

**Considered and rejected.** *Coronal Mass Ejections* — ACE MAG 16-second data are a workhorse for
identifying interplanetary CMEs, but that is what analysts do with the data, not what this software
does; it offers no CME detection, catalogue, or annotation. *Geomagnetic Storms* — the IMF Bz this
package plots is the classic storm driver, but no index, coupling function, or magnetospheric
response is computed. *Solar Corona*, *Coronal Heating*, *Solar Flares*, *X-ray emission* — remote solar
phenomena outside anything this in-situ magnetometer reader touches.

### 23. Development Status (RECOMMENDED)
- Unsupported

The reasoning matters more than the label here, because the plausible values all sound alike in casual
use.

The field's guidance points to repostatus.org for term descriptions, and the definitions quoted below
are the ones HSSI stores for these rows, so the choice is determined by which definition the evidence
satisfies:

- **Unsupported** — "The project has reached a stable, usable state but the author(s) have ceased all
  work on it. A new maintainer may be desired." Both halves hold. The stable state is asserted by the
  author in `setup.cfg` (`Development Status :: 5 - Production/Stable`) and realized by the v0.9.0
  release. The cessation of work is not inferred from silence: the owner **archived the repository on
  GitHub**, which makes it read-only — issues and pull requests are closed off, so the author has
  foreclosed even ad-hoc support through the repository. That is an owner-declared end of maintenance,
  which is stronger evidence than the 2021-04-27 last-push date alone.
- **Inactive** — "reached a stable, usable state but is no longer being actively developed;
  support/maintenance will be provided as time allows." The first clause fits; the second is
  contradicted by archiving, which removes the channel through which such support would be provided.
  This was the value an earlier extraction chose, on last-commit date alone and without weighing what
  archiving means. It is the runner-up, not an error, but `Unsupported` is the more precise claim.
- **Abandoned** — "Initial development has started, but there has not yet been a stable, usable
  release; the project has been abandoned…". Rejected on its first clause: a stable release exists.
  `Abandoned` is for projects that never shipped, and using it here would understate the software's
  usability, not just its maintenance state.
- **Suspended** — requires that the authors intend to resume. Archiving signals the opposite.
- **Moved** — requires an authoritative successor at a new location. None is declared in the README or
  the repository settings, and a survey of the author's `space-physics`, `geospace-code` and `scivision`
  GitHub accounts turned up no other ACE-named or ACE-described package.
- **Active**, **WIP**, **Concept** — excluded by the archived, released state of the repository.

A caveat that keeps this honest rather than final: `Unsupported` describes maintenance, not
functionality. The download path was confirmed working at this extraction, so the software is
unmaintained but not broken.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/ACE_magnetometer/blob/main/README.md

The README is the whole of the documentation: a one-line description, a sample output figure, and two
worked command lines for the download and plot scripts. There is no docs directory, no Sphinx or
ReadTheDocs configuration, and no wiki content despite the wiki feature being enabled. The URL is
pinned to `main`, which is the repository's default branch, and resolves. Installation instructions are
implicit (`pip install .[plot]`, inferable from `setup.cfg` extras and the CI workflow) rather than
written out — a genuine documentation gap, but the README remains the correct and only target for this
field.

### 25. Funder (OPTIONAL)
Not found.

No funding statement, acknowledgement, or grant number appears in any tracked file at the pinned
revision. The sole match for "grant" in the tree is the MIT License's "Permission is hereby granted",
and there is no publication whose acknowledgements could supply one (Field 14).

One piece of negative research worth keeping, because it is the funding-shaped artifact a future
agent is most likely to encounter in the repository's history: a `.github/FUNDING.yml` existed
between 2019-10-08 and 2021-04-27, containing `github: [scivision]` and `ko_fi: scivision`. That is
a GitHub Sponsors / Ko-fi donation configuration pointing at the author personally — not a research
funder, not an award, and not eligible for Field 25 even had it survived. The pinned revision is the
commit that deleted it.

### 26. Award Title (OPTIONAL)
Not found.

No award title or number appears in the repository, and there is no reference publication whose
acknowledgements could supply one. See Field 25 for why the deleted `FUNDING.yml` is not a source.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found.

The repository cites no publications: there is no `CITATION.cff`, no references section, and no paper
DOI in the README or source comments. The author's public ORCID record contains no work that is this
software or that uses it. A citation-graph check for papers citing the package found nothing to
evaluate, which is unsurprising for an uncited, undoi'd utility.

Related to Field 28's reasoning: the ACE Science Center explicitly asks users to consult the ACE
instrument team before citing browse data — the sentence, and the page carrying it, are quoted in the
Scope note — which makes it unlikely that published work will ever cite this particular data path.

### 28. Related Datasets (OPTIONAL)
Not found — deliberately empty, with a specific DOI that should not be added.

The dataset this software consumes is identifiable and was traced: the ACE Science Center's 16-second
MAG **browse** product, served from `ftp://mussel.srl.caltech.edu/pub/ace/browse/MAG16sec/`. It has no
DOI and, at this extraction, no SPASE record — probes for browse-level or level-1 ACE MAG dataset
identifiers found none.

**The ACE Level 2 16-second dataset DOI is a trap and is deliberately not recorded.** The SPASE record
`spase://NASA/NumericalData/ACE/MAG/L2/PT16S` ("ACE Magnetic Field 16-Second Level 2 Data") carries
DOI https://doi.org/10.48322/e0dc-0h53, and its access list even includes the same FTP host this
software uses — but a *different directory*, `/pub/ace/level2/mag/`. The two products share a mission,
an instrument and a cadence, and are otherwise not the same data: Level 2 is science-quality and
science-team-verified, while browse data are automatically generated during level-one processing and,
in the ACE Science Center's own words on the browse-parameter information page pinned in the Scope note,
"are not suitable for serious scientific work, and should not be cited without first consulting the
appropriate ACE instrument team." Recording the Level 2 DOI would tell a user this software reads
verified Level 2 data, which it does not. The near-identical
`spase://NASA/NumericalData/ACE/MAG/KeyParameter/PT16S` (DOI https://doi.org/10.48322/av87-m833, the
CDAWeb `AC_K1_MFI` 16-second key parameter product) is wrong for the same reason.

If a future curator wants a dataset association anyway, the honest form would be a citation to the ACE
Science Center browse product with its archive directory (https://izw1.caltech.edu/ACE/ASC/browse/), not
either DOI above. That directory is a bare file listing rather than a descriptive landing page; the
product's own description lives in its sibling `browse_info.html`, pinned in the Scope note. That path is
recorded for completeness rather than preferred: an empty field is more accurate than an approximate
link.

### 29. Related Software (OPTIONAL)
Not found — deliberately empty after a full pass over the candidates.

The declared dependencies are `pandas`, `numpy` and `python-dateutil`, with extras `pytest`, `flake8`,
`mypy`, `matplotlib` and `seaborn`. Every one of these is generic scientific-Python or developer
tooling: arrays, dataframes, date parsing, plotting, styling, testing, linting, type-checking. Listing
any of them would say something equally true of most of the Python ecosystem, which is the exact
condition under which this field carries no information. Being imported is not a relationship.

Two non-generic candidate classes were considered and rejected on the evidence:

- **The author's sibling packages in the `space-physics` GitHub organization** — several perform a
  visibly similar job on other data, as their GitHub repository descriptions say (`gima-magnetometer`,
  "UAF Geophysical Institute magnetometer network data read and plot"; `AEindex`, "Auroral Electrojet
  AE-index read and plot."; `GOESplot`; `themisasi`; `geomagindices`). What they share with this package
  is an author, an organization, and a house style — not a documented relationship. No tracked file at
  the pinned revision names any of them, none is imported, and no code is shared; notably, the author's
  own date-conversion package (`sciencedates`, in his `geospace-code` organization) exists, yet this
  repository reimplements day-of-year and fractional-year conversions inline in `datenum2DOY.m` and
  `datenum2fpYear.m`. "Same author, similar idiom" is not the distinguishing relation this field asks
  for.
- **Third-party tools that also load ACE MAG data** — PySPEDAS is the strongest example, and it
  genuinely does perform the similar task (`pyspedas/projects/ace/mfi.py` loads ACE magnetometer data);
  Speasy and CDAWeb-backed clients would qualify on the same grounds. They are rejected because the
  relationship would be entirely the cataloguer's assertion: this repository does not mention them, and
  they do not mention it. Recording it would also be open-ended — the same reasoning admits every
  general-purpose heliophysics data client. Named here so a future refresh can see the option was
  weighed rather than missed: PySPEDAS (https://github.com/spedas/pyspedas) is the strongest candidate
  should this field ever be read as a similar-tools pointer, and it was not selected because nothing in
  either project asserts the relationship.

An evidenced empty field is the outcome here, and it matches what HSSI stores.

### 30. Interoperable Software (OPTIONAL)
Not found — deliberately empty.

There is no demonstrated exchange with any other package: no adapter or converter API, no shared data
model, no plugin or companion relationship, no documented import of this package's output into another
tool. `load()` returns a plain pandas DataFrame, which is a language-level convenience rather than an
interchange contract with a named peer tool.

**MATLAB was considered specifically and rejected.** The repository ships MATLAB scripts, so MATLAB is
present — but it is the *runtime* for half of this codebase, not a peer tool this software exchanges
data with. The Python and MATLAB workflows in this package do not even interoperate with each other:
they read different files (ZIP-of-ASCII versus HDF), share no intermediate format, and neither calls
the other. MATLAB's correct home in this record is Field 13, where it is already recorded.

The generic exclusions from Field 29 apply here unchanged, and a package rejected there does not
migrate here.

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** ACE Magnetic Field Instrument
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ACE/MAG

The software is purpose-built for this instrument: it retrieves only MAG 16-second browse files, its
loader knows only MAG's column layout, and its plots are MAG's field components. The SPASE record for
this identifier confirms the match, naming the resource "ACE Magnetic Field Instrument" and listing
among its alternate names "ACE Magnetometer", "ACE MAG" and "ACE MFI" (the remaining one is the NSSDC
designation "1997-045A-09").

Both the name and the identifier are recorded above so the entry is defensible without re-querying the
vocabulary, and so the identifier — which is the reliable de-duplication key — travels with the name.

**Considered and not selected:** `Magnetic Field Instrument`,
https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/ACE/MAG. This is the CNES/AMDA registry's record
of the same physical instrument. It is a genuine SPASE row, not junk, but recording both would create a
duplicate association for one instrument; the SMWG record is the canonical one. A future agent should
recognize it as the same entity rather than an additional instrument.

**A matching trap worth recording:** the abbreviation `ACE` in this vocabulary also belongs to a
different instrument entirely — the TRACERS Analyzer of Cusp Electrons,
https://spase-metadata.org/NASA/Instrument/TRACERS/AnalyzerCuspElectrons. Abbreviation-only matching on
"ACE" is unsafe here; match on the mission path segment or the full name.

No other ACE instrument is supported. The mission's other instruments (SWEPAM, EPAM, CRIS, SIS, SWICS,
SWIMS, SEPICA, ULEIS) have SPASE rows of their own, and most of them contribute to the same browse
archive — the ACE Science Center's browse-parameter information page
(https://izw1.caltech.edu/ACE/ASC/browse/browse_info.html) documents browse parameters for CRIS, EPAM,
MAG, SEPICA, SIS, SWEPAM, SWICS and ULEIS, and states that "The SWIMS instrument does not contribute to
the browse parameters." None of that reaches this software, whose URL, filename pattern and column
layout are MAG-specific.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Advanced Composition Explorer
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/ACE

The software works exclusively with data from this mission, retrieved from the mission's own science
center. Field 17's `Observatory/Mission-specific` selection is the paired half of this association, as
the form's instructions require.

**Considered and not selected:** `Advanced Composition Explorer, NASA`,
https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/ACE — the CNES/AMDA registry's record of the same
mission. As with the instrument, the SMWG row is canonical and recording both would duplicate a single
association.

### 33. Logo (OPTIONAL)
Not found.

The repository contains one image, `tests/timeplot.png`, which the README embeds. It is a sample output
figure — a three-panel time series of ACE magnetometer components produced by `PlotACE.py` — not a
project logo, and recording it as one would misrepresent it. There is also negative evidence from
curation: the PyHC registry supports a `logo:` key and several of this author's other entries use it
(DASCutils, GOESutils, IGRF-13, LOWTRAN among them), while the ACEmag entry has none.
