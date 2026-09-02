# HSSI Metadata Extraction Results

**HSSI Software ID:** 4aa97b85-e71d-4584-a971-8b307e0a0e82
**Repository:** https://github.com/geospace-code/georinex
**Source Revision:** 8d1210a0f1ada71ff7b8d0484cfaf22ff154a38e
**Extraction Date:** 2026-09-01
**Validation Date:** 2026-09-02
**Validation Status:** PASS

---

## Scope note — read this before the evidence

GEOrinex is a pure-Python reader and batch converter for GNSS exchange formats: RINEX 2.x and 3.x
navigation and observation files (plain, gzip, bzip2, zip, LZW `.Z`, and Hatanaka-compressed CRINEX),
`io.StringIO` text streams, SP3-a/c/d ephemeris and clock files, and the NetCDF4 files it writes
itself. Everything it produces is either an `xarray.Dataset` in memory or a NetCDF4 (HDF5-container)
file on disk. There is a thin MATLAB entry point (`ReadRinex.m`) that calls the Python package.

Two structural facts drive several fields and should be re-checked before any of them is ever
changed:

**Nothing in the package retrieves data over a network.** No tracked Python file at the pin imports
`requests`, `urllib`, `ftplib`, or any HTTP or FTP client, and no file performs a download. A
case-insensitive grep across the package's Python sources (excluding the test-fixture directory) for
`requests|urllib|urlopen|ftplib|wget|curl|download|https?://|ftp://` matches **fifteen** lines across
those 25 files, and every one of them is a URL sitting in a docstring or a comment. The pattern is
scoped to two things — the `http`, `https` and `ftp` URL schemes, and the import names of the clients
a Python package would actually fetch with — so that a reader re-running it reconciles against the
same boundary. Note the trap it is built to avoid: `ftplib` matches an *import name*, not a URL
scheme, so a pattern that lists `ftplib` while omitting `ftp://` silently misses the three `igs.org`
citations below. The complete set, so that reconciliation is line for line:

| Location | What it is |
|---|---|
| `src/georinex/keplerian.py:16`, `:19`, `:21` | orbital-mechanics references in the `keplerian2ecef` docstring |
| `src/georinex/nav2.py:25`, `:26` | the pair of RINEX 2.11 format references in the `rinexnav2` docstring — a gLAB page, and `ftp://igs.org/pub/data/format/rinex211.txt` |
| `src/georinex/nav2.py:139` | `# %% format I2 …` — the same gLAB reference, in an inline comment |
| `src/georinex/nav3.py:247` | `ftp://igs.org/pub/data/format/rinex303.pdf` in a bare docstring inside the `case "G":` branch of `_fields`, followed by the page numbers of the tables it cites |
| `src/georinex/obs3.py:18` | a bare docstring at module level holding the NMEA satellite-ID table, `"""https://github.com/mvglasow/satstat/wiki/NMEA-IDs"""` |
| `src/georinex/obs3.py:316` | RINEX 3.05 observation format reference in an inline comment |
| `src/georinex/plots_geo.py:30`, `:97` | the same cartopy issue link, twice |
| `src/georinex/rio.py:46` | a bare string expression inside `opener()`, `"""https://en.wikipedia.org/wiki/List_of_file_signatures"""`, documenting the magic-number check on the lines below it |
| `src/georinex/sp3.py:3` | the IGS SP3 formats page, in the module docstring |
| `src/georinex/sp3.py:27` | `http://epncb.oma.be/ftp/data/format/sp3_docu.txt  (sp3a)` in the `load_sp3` docstring — an `http` URL with `ftp` in its *path*, which is why it turns up in a scheme search and why it should not be read as a transfer |
| `src/georinex/sp3.py:48` | `# (see ftp://igs.org/pub/data/format/sp3d.pdf)` — an inline comment explaining the SP3-d satellite-count field width |

Every one of the fifteen is a format specification, a reference document, or an upstream issue link:
this package cites the standards it implements and fetches none of them. That is why Field 17 is
legitimately empty and why `Data Processing and Analysis: Data Access and Retrieval` is not in
Field 4.

**RINEX 4 is advertised but not implemented at the pin.** `README.md:7` opens
`RINEX 4, RINEX 3 and RINEX 2 reader and batch conversion to NetCDF4 / HDF5 in Python or Matlab.` and
`README.md:26` lists `* RINEX 4.x, RINEX 3.x, or RINEX 2.x` as an input data type. The dispatch code
does not agree: `src/georinex/base.py:212` reads `if int(info["version"]) in {1, 2}:` and
`:223` reads `elif int(info["version"]) == 3:`, with `:235` falling through to
`raise ValueError(f"unknown RINEX {info}  {fn}")`; the navigation path at `:160`, `:162` and `:165`
has the same shape, ending in `raise LookupError(f"unknown RINEX  {info}  {fn}")`. A file whose
header version parses to 4 therefore raises rather than loading. The repository ships a RINEX 4
fixture, `src/georinex/tests/obs4.00gage.19o`, whose first line is
`     4.0            OBSERVATION DATA    M (MIXED)           RINEX VERSION / TYPE`, and no test file
at the pin references it. The README claim and the fixture were both added by commit
`178036320627be5f99dc318d80476eeb1db367a8` (2025-01-21, "add RINEX 3.05 OBS test file, allow SBAS
header flexibility"), whose only source change was to `src/georinex/obs3.py`'s header parser. The
standing feature request, GitHub issue #83 "Rinex 4" (opened 2022-01-12), is still open and notes
that "4.0 observations files are compatible with 3.0, but navigation files are not." This is why
Fields 8 and 9 deliberately do **not** repeat the project's RINEX 4 claim — see the reasoning
there.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Note:** Placeholder by catalogue convention. This record was not submitted by its maintainer, and
the HSSI data API does not expose submitter identity, so no name can be recovered from the record
itself.

---

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.595473

**This is the concept DOI, and the stored value is correct.** DataCite resolves
`10.5281/zenodo.595473` with `publisher: "Zenodo"`, `resourceTypeGeneral: "Software"`, and **48**
`HasVersion` relations pointing at the individual release deposits. It also carries
`IsSupplementTo https://github.com/geospace-code/georinex/tree/v1.16.2`, the signature of a Zenodo
GitHub-integration deposit rather than a manual upload — which is what ties the DOI to this
repository and to Field 11's publisher.

**The repository's own two DOI citations are stale version DOIs, and this is the durable finding of
this field.** Neither should ever be promoted into Field 2.

- `CITATION` (the file has no `.cff` extension and contains exactly one line) reads
  `https://doi.org/10.5281/zenodo.3401498`. DataCite gives that DOI
  `version: v1.13.0`, `Issued 2019-09-06`, title
  `scivision/georinex: NAV: allow same-time entries, fix pandas &gt;= 0.25, OBS2 wrong obs num OK`,
  and `IsVersionOf 10.5281/zenodo.595473`.
- `README.md:3` carries the badge
  `[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.2580306.svg)](https://doi.org/10.5281/zenodo.2580306)`.
  DataCite gives `10.5281/zenodo.2580306` `version: v1.8.0`, `Issued 2019-02-28`, title
  `scivision/georinex: File extension agnostic`, and `IsVersionOf 10.5281/zenodo.595473`.

Both are therefore individual-release identifiers frozen in 2019 — at v1.13.0 and v1.8.0, while the
concept's newest deposit is v1.16.2. From the searcher's side that matters concretely: a user who follows the repository's badge
lands on a 2019 snapshot, whereas the concept DOI always resolves to the newest deposit. The
consequence is downstream and visible — the peer-reviewed `gnss_lib_py` paper recorded in Field 27
cites georinex in its bibliography as `[30] georinex (2022). URL https://doi.org/10.5281/zenodo.3401498`,
i.e. it inherited the stale CITATION DOI verbatim.

**Negative research: there is no second, independent DOI for this software.** Three checks that fail
in different ways all come back empty, so the absence is real rather than an artifact of one query
shape.

- *Repository-name keyed.* A DataCite search restricted to `resource-type-id=software` for
  `titles.title:"georinex"` returns 38 deposits; every one inspected is a Zenodo release under this
  concept.
- *Old-name keyed.* This project has been renamed twice, so name-keyed checks need the old names.
  `https://github.com/scivision/pyrinex` and `https://github.com/scivision/georinex` both redirect
  (200) to `https://github.com/geospace-code/georinex`; `https://github.com/geospace-code/pyrinex`
  is 404, so the chain is `scivision/pyrinex` -> `scivision/georinex` -> `geospace-code/georinex`.
  The early deposits are titled accordingly — `10.5281/zenodo.213688` is
  `scienceopen/pyrinex: Initial release` (v0.1, issued 2016-12-20) — and each carries
  `IsVersionOf 10.5281/zenodo.595473`.
- *Creator keyed, which is the only check blind neither to renames nor to a descriptively titled
  manual upload.* Zenodo record searches on `metadata.creators.person_or_org.name` for
  `"Michael Hirsch"`, `"Hirsch, Michael"` and `"scivision"` return 34, 48 and 28 records
  respectively, so the query form works; the newest results in each — `themisasi`, `NEXRAD`,
  `isr-raw`, `LAPACK95`, `mat_gemini-scripts`, `MatGemini`, `Fortran filesystem`, `h5fortran` and
  others — are unrelated projects, and no georinex deposit outside this concept surfaced in any of
  the three.
  A DataCite software search for `creators.name:"Hirsch" AND titles.title:"rinex"` returns 4, all of
  them `scivision/georinex` or `scivision/pyrinex` release deposits under this same concept, while
  the control `creators.name:"Hirsch, Michael"` under the same software restriction returns 519 —
  so the empty result is real absence, not a broken query.

**A trap recorded so DOI autofill is never trusted here.** The Zenodo/DataCite record for this
concept declares
`rightsList: [{"rights": "Creative Commons Attribution 4.0 International", "rightsIdentifier": "cc-by-4.0"}]`.
That is **not** this software's licence — see Field 15, which is derived from `LICENSE.txt`. The same
record also splits creator names badly (see Field 6). Autofill from this DOI would import both
errors.

---

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/geospace-code/georinex

**Source:** The git remote at the pinned revision, and the GitHub API, which gives
`full_name: geospace-code/georinex` and `default_branch: main`. `README.md:61` documents the
development install as `git clone https://github.com/geospace-code/georinex`.

**Rename history, recorded because external sources still point at the old paths.** The Zenodo
deposits from 2016–2019 reference `https://github.com/scivision/pyrinex/tree/…` and
`https://github.com/scivision/georinex/tree/…`, and the README's own PyMap3d link
(`README.md:175`) still uses the retired `scivision/` path. All of those redirect into
`geospace-code/georinex`. The stored value is the canonical current one; the stale upstream pointers
are not drift in this record and must not be "corrected" into it.

---

### 4. Software Functionality (RECOMMENDED)
**Values:**
- Coordinate Transforms
- Data Processing and Analysis
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Data Visualization: Orbit Plots

All nine were carried over from the existing HSSI record. Each was re-tested against the
`software-functionality` skill's category wording and against the code at the pin, and each holds.
No further value in the vocabulary applies; the ones that came closest are listed as rejected
alternatives below, so this is a settled result rather than an inherited one.

**A durable caution about the vocabulary.** Every `FunctionCategory` row carries an empty
`definition` — not some of them, all of them. Category wording therefore has to come from the
`software-functionality` skill's table; "the vocabulary's own description" does not exist and must
never be cited as an authority here.

**Coordinate Transforms — kept, as the bare parent.** Two user-facing conversions exist.
`keplerian2ecef` is exported from the package's public API (`src/georinex/__init__.py` imports it
from `.keplerian` and lists it in `__all__`) and converts GPS or Galileo broadcast Keplerian elements
into ECEF X/Y/Z; its docstring header at `src/georinex/keplerian.py:2` is
`GPS Keplerian elements => ECEF`. Separately, `src/georinex/obs2.py:405` and
`src/georinex/obs3.py:336` both execute `hdr["position_geodetic"] = ecef2geodetic(*hdr["position"])`,
attaching a geodetic latitude/longitude/altitude attribute to an observation dataset whose header
carries an approximate position, whenever the optional `pymap3d` dependency is installed (both call
sites are guarded on that import, sharing a prefix but not identical: `obs2.py:404` is exactly
`if ecef2geodetic is not None:`, while `obs3.py:335` extends it to
`if ecef2geodetic is not None and len(hdr["position"]) == 3:`); `README.md:174`–`:175` documents
this as a capability
(`To convert ECEF to Latitude, Longitude, Altitude or other coordinate systems, use` /
`[PyMap3d](https://github.com/scivision/pymap3d).`), and `src/georinex/tests/test_obs2.py:208` and
`test_obs3.py:162` assert the resulting values.

*No subcategory is selected, and that is deliberate.* The six children are `Heliospheric`,
`Ionospheric`, `Magnetospheric`, `Mission-Specific`, `Planetary` and `Solar`. The transforms here are
terrestrial and geodetic — Earth-centred inertial-to-fixed and ECEF-to-geodetic — and the vocabulary
has no terrestrial or geodetic child. `Ionospheric` covers AACGM, MLT and apex coordinates, none of
which this package computes; `Planetary` covers non-Earth bodies. Recording the bare parent is the
accurate answer, not an omission to be filled later.

**Data Processing and Analysis — kept** as the parent of the three children below.

**Data Processing and Analysis: File Format Conversion — kept.** This is the package's headline
capability. `README.md:7` describes it as `batch conversion to NetCDF4 / HDF5`;
`src/georinex/base.py` exports `batch_convert`; and `src/georinex/rinex2hdf5/__main__.py` is a
dedicated CLI whose docstring at `:2` is `Converts RINEX 2/3 NAV/OBS to NetCDF4 / HDF5`.

**Data Processing and Analysis: Data Reduction — kept.** The skill defines this as reducing data
volume while preserving information, by averaging, binning, downsampling or filtering. All four
reduction axes are exposed on the public API and the CLI: time bounds (`tlim`), constellation subset
(`read/__main__.py:37`–`:39`, `"--use"` with `choices=["G", "C", "E", "S", "J", "R", "I"]`),
measurement subset (`"--meas"`, `:44`), and explicit temporal decimation
(`read/__main__.py:59`, `p.add_argument("-interval", help="read the rinex file only every N seconds", type=float)`).
The decimation is real, not nominal: `src/georinex/obs2.py:91` documents
`t_interval: allows decimating file read by time e.g. every 5 seconds.` and `:156`–`:164` skips
epochs closer together than the requested interval.

**Data Processing and Analysis: Processing — kept** as the general pipeline value: header parsing,
epoch-block ingestion, unit normalisation and dataset assembly across `obs2.py`, `obs3.py`,
`nav2.py`, `nav3.py` and `sp3.py`.

**Data Visualization — kept**, with all three children below.

**Data Visualization: Line Plots — kept.** `src/georinex/plots.py:27` defines
`obstimeseries(obs: xarray.Dataset)`, which draws `ax.plot(time, dat)` (`:43`) for the `L1`/`L1C`
carrier-phase observables against time, labelled `"time [UTC]"`.
`src/georinex/plot/__main__.py` is a four-panel time-series CLI over pseudorange, carrier phase,
Doppler and signal strength.

**Data Visualization: 2D Graphics — kept, and the map evidence is what keeps it.** The skill scopes
this subcategory to static 2D plots of the contour/heatmap/image/2D-map family. This package draws
genuine geographic maps: `src/georinex/plots_geo.py:29` and `:96` both create axes with
`projection=cartopy.crs.PlateCarree()` and add `cpf.LAND`, `cpf.OCEAN`, `cpf.COASTLINE` and
`cpf.BORDERS` features, and `:116`/`:118` scatter receiver positions onto that map with marker size
scaled by measurement interval. `python -m georinex.loc` (`README.md:179`) is the user-facing entry
point. A user filtering HSSI for 2D-graphics software and finding a package that plots GNSS receiver
networks on a coastline map is not surprised.

**Data Visualization: Orbit Plots — kept.** `src/georinex/plots_geo.py:21`
`navtimeseries(nav: xarray.Dataset)` computes each satellite's ground track — via `keplerian2ecef`
for GPS (`:66`) and Galileo (`:75`), and directly from the broadcast X/Y/Z for SBAS (`:40`) and
GLONASS (`:53`) — converts to geodetic with `pm.ecef2geodetic` and plots `ax.plot(lon, lat, label=sv)`
(`:87`) over the same map. It also range-checks the results against each constellation's expected
altitude and inclination (`:46`–`:82`), which is orbit-aware behaviour rather than generic plotting.

**Considered and rejected — do not re-propose without new evidence:**

- *Data Processing and Analysis: Data Access and Retrieval.* No network retrieval exists anywhere in
  the package; see the scope note. The UNAVCO FTP paths at `README.md:276`–`:286` are places a user
  can go and get files by hand, not a supported access backend.
- *Data Processing and Analysis: Time Series Analysis.* Tempting, because the output is a
  time-indexed `xarray.Dataset`, `tlim` filters by time, `gettime` and the `georinex.gtime` CLI
  extract and audit epoch vectors, and `README.md:48` advertises
  `In-memory: Xarray.Dataset. This allows all the database-like indexing power of Pandas to be unleashed.`
  It was rejected because none of that is *analysis* in the skill's sense — no temporal filtering of
  signal content, no trend estimation, no autocorrelation, no resampling beyond epoch decimation.
  The package hands a user a time series; the analysis is theirs. `Data Visualization: Line Plots`
  already records the time-series display, and `Data Reduction` records the temporal subsetting.
- *Data Processing and Analysis: Analysis.* `README.md:141` does carry a section literally headed
  `## Analysis`, but its content (`:143`) is a statement that the package *enables* analysis, not
  that it performs any — the sentence is quoted in full in Field 30. The one derived physical
  quantity it computes, satellite ECEF position from broadcast elements, is already recorded under
  Coordinate Transforms.
- *Data Processing and Analysis: Calibration.* RINEX observables arrive already in physical units.
  The package does perform unit and encoding normalisation — kilometres to metres for GLONASS NAV2
  ephemerides, and Fortran `D`-exponent handling in `rinex_string_to_float`
  (`src/georinex/common.py`) — but calibration in the skill's sense means converting raw instrument
  counts to physical units using calibration files or response functions, and none of that exists
  here.
- *Data Processing and Analysis: Packet Decommutation.* RINEX and SP3 are line-oriented ASCII
  formats, not binary telemetry streams. There is no CCSDS or packet handling.
- *Servers and Environments: High Performance Computing.* `README.md:15` claims the package
  `allows for HPC / out-of-core operations on massive amounts of GNSS data`, and `README.md:47` adds
  that the converted output `allows filtering/processing of gigantic files too large to fit into RAM.` This is the most quotable near-miss in the README and is recorded so
  it is not mistaken for evidence. The package provides no HPC infrastructure: no MPI, no job
  scripts, no scheduler integration, no container. What it provides is a NetCDF4 output that
  *other* tools can process out-of-core. A user filtering HSSI for HPC software would find a
  single-process file reader out of place.
- *Servers and Environments: Software or Environment Container.* No Dockerfile or container
  definition exists in the tree at the pin.
- *Mission-related, and every child.* This is a general-purpose format reader, not part of any
  mission's ground system.
- *Models and Simulations, and every child.* Nothing here models a physical system. `keplerian2ecef`
  evaluates the broadcast ephemeris the satellites themselves transmit; it does not model orbits.
- *Data Visualization: Spacecraft Formation Plots.* `navtimeseries` draws several satellites on one
  map, which is a constellation of independent ground tracks, not a formation-geometry plot.
- *Data Visualization: 3D Graphics, Movies, Spectrogram, Web-Based, Mission-Specific, ML/AI.* No
  three-dimensional rendering, animation, time-frequency display, browser output, mission-specific
  plot type, or machine learning appears anywhere in the package.

---

### 5. Related Region (RECOMMENDED)
**Values:**
- Earth Atmosphere
- Earth Ionosphere

`Earth Atmosphere` was carried over from the existing HSSI record, which held it alone.
`Earth Ionosphere` was added in this refresh.

**The Region vocabulary is flat** — every one of the 24 rows has empty `parents` and `children` — so
neither value implies the other and each has to stand on its own evidence. A coverage argument of the
form "Earth Atmosphere already encompasses the ionosphere" is not available and would be a defect.

**Earth Atmosphere.** The package's own metadata places it in atmospheric science: `pyproject.toml`
declares the classifier `"Topic :: Scientific/Engineering :: Atmospheric Science"`. GNSS
observations recorded in RINEX are atmospheric-sounding data in the general case — the signal's
delay through the neutral atmosphere and the ionised atmosphere is what makes the observables
scientifically interesting beyond positioning. The coarse value is the one a user filtering broadly
for atmospheric software will use, and this record belongs in that result set.

**Earth Ionosphere — added, and this is the substantive change in this field.** Two independent
lines of evidence support it.

*In the code.* The package parses and exposes the broadcast ionospheric correction coefficients from
RINEX NAV headers as first-class dataset attributes. `src/georinex/nav2.py:205`–`:209` reads the
RINEX 2 `ION ALPHA` and `ION BETA` header records and sets
`nav.attrs["ionospheric_corr_GPS"] = np.hstack((alpha, beta))`. `src/georinex/nav3.py:143`–`:155`
does the same for RINEX 3's `IONOSPHERIC CORR` block across five constellations, setting
`ionospheric_corr_GPS`, `ionospheric_corr_GAL`, `ionospheric_corr_QZS`, `ionospheric_corr_BDS` and
`ionospheric_corr_IRN`. These are the Klobuchar (and Galileo NeQuick) model parameters that
single-frequency receivers use to correct for ionospheric delay, and the package treats them as
output worth surfacing rather than header noise: `src/georinex/tests/test_nav2.py:197` and
`test_nav3.py:239` are dedicated `test_ionospheric_correction` tests, and
`src/georinex/tests/test_rinex.py:75` asserts `nav.ionospheric_corr_GAL` values.

*In the literature.* Ionospheric researchers build on this package directly. Reid et al. (2026),
"The Real-Time Advanced Ionospheric Data Assimilation (AIDA) Model", *Space Weather* **24**,
`https://doi.org/10.1029/2025SW004712`, names georinex in its acknowledgements, and
Ventriglia et al. (2026), "PyTECGg: total electron content calibration with GNSS data", *SoftwareX*
**34**, 102737, `https://doi.org/10.1016/j.softx.2026.102737`, references it in its full text. Both
are total-electron-content / ionospheric-specification work. Note that only the first of the two is
recorded in Field 27, and the difference is not an inconsistency: the question here is whether
ionospheric researchers use this software, which a full-text reference answers, while Field 27 asks
the narrower question of which publications credit it deliberately enough to belong on the record.

*The searcher's-side test.* Dual-frequency GNSS carrier-phase and pseudorange observations are the
primary ground-based measurement of ionospheric total electron content, RINEX is the format they are
distributed in, and the network that distributes most of them is the one Field 32 records. Someone filtering HSSI for Earth Ionosphere software is, in practice, looking for
tools that let them work with ionospheric observations; a Python reader that turns RINEX into
analysis-ready arrays is exactly what they will reach for, and its absence from that result set would
make the catalogue look incomplete. They would be glad to find it.

**Considered and rejected — `Earth Thermosphere`.** The obvious argument for it is the PyHC registry
entry, whose keyword list for this package is `["ionosphere_thermosphere_mesosphere","specific"]`
(`_data/projects_unevaluated.yml`), and that keyword is already stored in Field 16. It was rejected
because the keyword is a broad PyHC domain bucket that propagates across many entries and is not
evidence about this software. Nothing in the repository supports it: a case-insensitive grep of
**every tracked file** at the pin for
`thermospher|mesospher|tropo|water vapou?r|electron content|\bTEC\b|scintillat` returns **no
matches at all** — not in the code, not in any of the six tracked Markdown files, not even in the
RINEX test
fixtures. GNSS TEC is an integrated ionospheric measurement; the thermosphere is not
something this package touches, names, or lets a user compute.

**Considered and rejected — `Earth Lower and Middle Atmosphere`.** GNSS meteorology (tropospheric
zenith delay, precipitable water vapour) is a genuine and major use of RINEX data, and it would be a
defensible value for some GNSS software. It is not defensible for this one: the same grep above finds
no mention of the troposphere or water vapour anywhere in the repository, and the package computes no
delay quantity of any kind. Recorded so the general truth about RINEX is not mistaken for a fact
about GEOrinex.

**Considered and rejected — the remaining 20 rows.** `Chromosphere`, `Corona`, `Photosphere`,
`Solar Interior`, `Solar Environment`, `Solar Wind`, `Heliosheath`, `Interplanetary Space`,
`Earth Auroral Subregion`, `Earth Inner Magnetosphere`, `Earth Outer Magnetosphere`,
`Earth Magnetosheath`, `Earth Magnetosphere`, `Earth Magnetotail`, `Planetary Magnetospheres` and the
Jupiter, Saturn, Mars, Uranus and Neptune magnetosphere rows all describe regions this package
computes nothing in and reads no data from. GNSS satellites fly in medium Earth orbit at roughly
20,000 km — with the geostationary and inclined-geosynchronous members higher still — and so are
inside the magnetosphere, but the package handles their signals as measured at the ground, not the
plasma environment they fly through; `Earth Inner Magnetosphere` on the strength of the orbit
altitude would be a category error a user would find out of place.

---

### 6. Authors (MANDATORY)

**Author 1:**
- **Author Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation 1:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** https://ror.org/05qwgg493
- **Affiliation 2:**
  - **Organization:** Scivision, Inc.
  - **Affiliation Identifier:** Not found

**Author 2:**
- **Author Name:** Nikolay Mayorov
- **Author Identifier:** Not found — see the ORCID note below
- **Affiliation:** Not found

**Author 3:**
- **Author Name:** Joakim Strandberg
- **Author Identifier:** https://orcid.org/0000-0002-1564-2976
- **Affiliation:**
  - **Organization:** Chalmers University of Technology
  - **Affiliation Identifier:** https://ror.org/040wg7k59

**Author 4:**
- **Author Name:** Martin Valgur
- **Author Identifier:** Not found — see the ORCID note below
- **Affiliation:**
  - **Organization:** Milrem Robotics
  - **Affiliation Identifier:** Not found

**Author 5:**
- **Author Name:** Snehil Saluja
- **Author Identifier:** Not found — see the ORCID note below
- **Affiliation:**
  - **Organization:** Indian Institute of Technology Kanpur
  - **Affiliation Identifier:** https://ror.org/05pjsgx75

**Author 6:**
- **Author Name:** Daniel Estévez
- **Author Identifier:** Not found — see the ORCID note below
- **Affiliation:** Not found

**Author 7:**
- **Author Name:** Elias Kunnas
- **Author Identifier:** Not found — see the ORCID note below
- **Affiliation:** Not found

**Author 8:**
- **Author Name:** Frédéric Meynadier
- **Author Identifier:** https://orcid.org/0000-0003-2719-5592
- **Affiliation:**
  - **Organization:** Bureau international des poids et mesures
  - **Affiliation Identifier:** https://ror.org/055vkyj43

**Author 9:**
- **Author Name:** Volker Mayer
- **Author Identifier:** https://orcid.org/0000-0001-8771-3254
- **Affiliation:**
  - **Organization:** European Space Agency
  - **Affiliation Identifier:** https://ror.org/03wd9za21
  - **Note:** Selected over the two institutions his ORCID names. `European Space Operations Centre`
    was recorded first, on evidence that turned out to be misattributed; the reasoning and the
    rejected alternatives are under "Volker Mayer's affiliation" below.

**Author 10:**
- **Author Name:** Derek Knowles
- **Author Identifier:** https://orcid.org/0000-0001-7362-2327
- **Affiliation:**
  - **Organization:** Stanford University
  - **Affiliation Identifier:** https://ror.org/00f54p054

---

**Where the ten authors come from, and why the list is what it is.** All ten were carried over from
the existing HSSI record, which took them from the Zenodo deposit. The DataCite record for the
concept DOI lists **eleven** creators, in this order: `scivision`, `Nikolay Mayorov`,
`Joakim Strandberg`, `Martin Valgur`, `Snehil Saluja`, `Daniel Estévez`, `Elias Kunnas`,
`fmeynadier`, `VOMAY`, `Derek Knowles`, `izzydrewlynn`. Four of those are GitHub handles rather than
personal names; three were resolved to people and are stored as such, and the fourth is a documented
omission below. Nobody stored has been dropped.

**Michael Hirsch is the principal author.** `LICENSE.txt:3` is `Copyright (c) 2015 Michael Hirsch`;
`src/georinex/keplerian.py:3` carries `Michael Hirsch, Ph.D.` in the module docstring; and he is the
overwhelming majority of the commit history — `git shortlog -sne` restricted to the pinned lineage
attributes 427 of 458 commits to his three name spellings under the `scivision` GitHub account. The
stored ORCID `0000-0002-1637-6526` and the Boston University affiliation are unchanged and are
corroborated by his ORCID record.

**The handle-to-person mappings, and the single standard applied to all four.** Each accepted mapping
rests on the same class of evidence: a primary artifact in which the contribution is git-authored
under a personal name. This is stated explicitly because applying the standard unevenly is exactly
how a wrong author name gets minted.

- `scivision` -> **Michael Hirsch**. Commits under
  `scivision@users.noreply.github.com` and `10931741+scivision@users.noreply.github.com` are
  git-authored `Michael Hirsch` and `Michael Hirsch, Ph.D`, and `LICENSE.txt:3` names him.
- `fmeynadier` -> **Frédéric Meynadier**. Commit `2acbb6b1083cf1e5e8a876b745e507a7ded6d9ec`
  (2020-02-21, "Added support for sp3 version d") is git-authored
  `Frédéric Meynadier <frederic.meynadier@bipm.org>`, and GitHub attributes that commit to the
  `fmeynadier` account.
- `VOMAY` -> **Volker Mayer**. The merged commit `60f13a2f844341bd5009139d9dd90a799ae04775`
  (2019-11-01, "Derive interval attribute from data if missing (#53)") is git-authored under the bare
  handle, but the three branch commits of pull request #53 — `0fa0057865`, `edac87b2c8` and
  `d6a705ed2c`, all 2019-10-15 — are git-authored `Volker Mayer <volker.mayer@esa.int>`. The personal
  name is therefore in a primary artifact, not inferred from the handle's spelling.
- `izzydrewlynn` -> **unresolved**, and left off. See the documented omission below.

**Documented omission — the eleventh creator, `izzydrewlynn`, is not added.** The evidence that
supports the omission, so it is not re-litigated:

- The account's single contribution is commit `86b957588bcf8aec56d4016351d707d2d8d4ce1c`
  (2020-10-13, "Update obs2.py"), merged as pull request #69 on 2020-11-11. Both the merged commit
  and the PR branch commit are git-authored
  `izzydrewlynn <38845559+izzydrewlynn@users.noreply.github.com>` — the handle itself, with GitHub's
  noreply address. There is no personal name in any artifact.
- The GitHub account (user id 38845559, created 2018-04-30) has `name`, `company`, `location`, `bio`
  and `blog` all empty, no public events, and one public repository, which is a fork of georinex.
- Applying the standard used for the other three handles therefore yields nothing. Recording the bare
  handle as an author name would mint an HSSI Person row that cannot be attributed to anyone and
  would tell a reader nothing. Note also that the ORCID rule below cuts the other way here: an
  author added by mistake cannot be quietly withdrawn later without leaving an orphan row.

If a personal name for this account is ever established from a primary source, adding an eleventh
author is the right correction.

**Three further named contributors are in git history but not in the Zenodo creator list, and are
deliberately not added.** Zenodo's GitHub integration snapshots the contributor list at deposit time,
and its snapshot for v1.16.2 is demonstrably not a complete list of named contributors. Three people
with commits on the pinned lineage are absent from it:

| Contributor | Commit(s) on the pinned lineage |
|---|---|
| Greg Starr (`gregstarr`) | `5bac6525d09373f4004d1e924162d8c6b672a72f`, 2016-08-24, "update" |
| Nikos Kanistras (`loctio`) | `d5de43c21f915230c6d09f43da1acc2e9a7cd1f6`, 2021-11-11, "Retrieve time-system corrections from RINEX 3" |
| Jan Bolting (`jtec`, `janbolting`) | `10e2358e5518dc2a67ca605c16edfa5cdc06ae2d`, 2024-01-09; `95ef1d8e7150f998a1b5a429090cadb429128648`, 2024-01-28 |

All three appear in GitHub's contributor list for the repository. **Jan Bolting's commits post-date
the v1.16.2 release, which explains his absence; Greg Starr's and Nikos Kanistras's do not.** That
asymmetry is the fact a later refresh needs: the omission of those two is a gap in Zenodo's snapshot
rather than a consequence of timing, whereas Bolting would be expected to appear in any deposit cut
after January 2024.

**Why the ten stand.** The Zenodo creator list is the only authorship statement this project has ever
published. Expanding it unilaterally would make the HSSI record disagree with its own DOI — the DOI
Field 2 records, and the one downstream papers cite — and a one-commit contributor is not what a
reader of a citation-style author list expects to find there. The catalogue's job here is to reflect
the published authorship, not to reconstruct a better one from the commit graph.

**The case that was weighed and not taken is kept, because it is not a bad argument.** These are
named contributors of substantive code, identified by exactly the class of evidence that resolved
three of the handles already on the list, and the Zenodo list is a mechanical snapshot rather than a
curated statement. The right trigger for revisiting this is upstream, not editorial: if a later
deposit ever changes the creator list — a release after January 2024 that sweeps Bolting in, say —
this record should follow that new list, rather than re-opening the question from the commit graph.

**ORCIDs — five of the ten authors carry one.** Michael Hirsch's identifier was already on the
record; the four established below were added by a correction applied directly to the authors'
existing Person rows. The remaining five are documented absences, set out after the evidence.

**Why those four could not arrive through the ordinary update path — the general rule, because it
will come up again.** Sending an identifier for an author whose Person row already exists *without*
one does not annotate that row: it creates a second Person row and orphans the first. A metadata
update that tries to "fill in" a missing ORCID that way makes the catalogue worse rather than
better, so the identifier has to be written to the existing row instead. That is why these four were
recorded here with their evidence before they could be stored, and it is the first thing to check
before proposing an identifier for any author who still has none — the five below, and any author on
any other record whose Person row is bare.

- **Joakim Strandberg -> `https://orcid.org/0000-0002-1564-2976`.** The mapping is clinched by the
  contributor's own homepage. ORCID `0000-0002-1564-2976` (Joakim Strandberg, Chalmers University of
  Technology, department "Space, Earth and Environment", graduate student from 2015-10) lists the
  researcher URL `http://jstrandberg.se/`, and that page links to `github.com/Ydmir` — `Ydmir` is the
  GitHub login under which four of this contributor's five georinex commits were made
  (`Ydmir <joakim.u.strandberg@gmail.com>`, 2017-01-05 to 2017-01-10; the fifth, `53221a3d`, is
  git-authored `Joakim Strandberg` under the same address). His registered works are
  GNSS-reflectometry papers, which is the same domain.
- **Frédéric Meynadier -> `https://orcid.org/0000-0003-2719-5592`.** His georinex commit is authored
  from `frederic.meynadier@bipm.org`, and this ORCID's ongoing employment (from 2018-07-01) is
  Bureau International des Poids et Mesures, department "Temps", with GNSS time-transfer
  publications among its 55 works. An ORCID surname search for `Meynadier` returns five people, and
  he is the only Frédéric.
- **Volker Mayer -> `https://orcid.org/0000-0001-8771-3254`.** His pull-request commits are authored
  from `volker.mayer@esa.int`, and this ORCID's ongoing employment (from 2016) is LSE Space GmbH,
  Darmstadt, with the department recorded as "Provision of Engineering Services to ESA/ESOC
  Navigation Support Office" and the role "Navigation Engineer"; its works include
  "Bye-bye, bias! The ESA Multi-GNSS Bias Reference Frame". An ORCID search for `Volker Mayer`
  returns two people; the other, `0000-0003-3217-9394`, lists no institution in the search index.
- **Derek Knowles -> `https://orcid.org/0000-0001-7362-2327`.** His georinex commits are authored
  `betaBison <knowles.derek@gmail.com>`; PyPI records the author of `gnss-lib-py` as Derek Knowles
  and its homepage as `https://github.com/Stanford-NavLab/gnss_lib_py`; and this ORCID's single
  registered work is "gnss_lib_py: Analyzing GNSS data with Python", with a Stanford University
  Mechanical Engineering education entry. An ORCID search for family name `Knowles` with given name
  `Derek` returns exactly this one record.

**Where these four identifiers do and do not yet appear.** They sit on the authors' Person rows and
are served as part of this record's authorship. Production still carries those same four rows
without them, and will until the next seed-CSV promotion propagates the correction. A production
check made before that happens will find the four fields empty; that is a known lag between
environments, not drift in this dossier, and it needs no further research — the identifiers and the
evidence for them are above.

**No ORCID could be established for five authors, and this negative research should stop the search
being repeated.**

- *Nikolay Mayorov* — three ORCID records match the name: `0000-0001-6866-504X` (Moscow State
  University of Culture and Arts and a film archive — a film historian), `0000-0002-9003-1841` (no
  institution, no works) and `0009-0001-2677-881X` (four computer-graphics papers on differentiable
  rendering and 3D reconstruction). None corresponds to the numerical-Python contributor.
- *Martin Valgur* — an ORCID surname search for `Valgur` returns **0** records.
- *Snehil Saluja* — an ORCID given-name search for `Snehil` returns 78 people and a surname search
  for `Saluja` returns 216; no record combines the two, and none is at IIT Kanpur or in GNSS.
- *Elias Kunnas* — an ORCID surname search for `Kunnas` returns 16 people, none named Elias.
- *Daniel Estévez* — an ORCID search returns eleven near matches; the two spelled exactly
  `DANIEL ESTEVEZ` (`0000-0002-7289-7959`, `0000-0002-1644-8112`) each have no institution and no
  registered works, so neither can be tied to this contributor, and the rest are different people
  (Max Planck / Havana, Basque Country, and several compound surnames).

**Volker Mayer's affiliation — `European Space Agency`, and why not either institution his ORCID
actually names.** His ORCID record carries exactly two employment entries, and neither is the
recorded value. Read whole, they are:

| Organization | Department | Role | Period | Identifier |
|---|---|---|---|---|
| `LSE Space GmbH` | `Provision of Engineering Services to ESA/ESOC Navigation Support Office` | `Navigation Engineer` | 2016 – ongoing, no end date | none |
| `European Space Operations Centre` | `Navigation Support Office` | `German Trainee Programm` | 2016 – 2016 | `https://ror.org/0541jr710`, with `disambiguation-source: ROR` |

**Reading the whole entry matters here, and getting it wrong once already skewed this decision.** The
department string naming ESA/ESOC belongs to the **LSE Space GmbH** entry, not to the ESOC one. ESOC's
own department is the plain `Navigation Support Office` and its role is a `German Trainee Programm`
that started and ended in 2016. An earlier draft of this dossier attached the engineering-services
department to ESOC, which made that entry read as a substantive post held at the time of the
contribution. It was not, and repairing the attribution is what moved this record off ESOC.

**What the evidence establishes.** The contribution is pull request #53, whose branch commits are
dated 2019-10-15 and authored from `volker.mayer@esa.int`. In October 2019 the only employment his
own profile records is **LSE Space GmbH**, whose department field says in terms that the work is
provision of engineering services *to* ESA/ESOC. The ESOC traineeship had closed three years earlier.
So the substantive, ongoing, engineering relationship is with LSE Space GmbH; the ROR-keyed,
ORCID-disambiguated relationship is with ESOC but is expired; and the `@esa.int` address is the only
one of the three artifacts that comes from the contribution itself.

**Why `European Space Agency` is the recorded value.**

- It is true across the whole period on either reading of his position — ESOC trainee in 2016, or LSE
  Space engineer embedded in ESA/ESOC's Navigation Support Office from 2016 onward. The agency is ESA
  in both.
- It is what the contribution's own artifact supports. `volker.mayer@esa.int` is an ESA address in
  use in 2019, three years after the traineeship closed, which is what an embedded contractor holds.
- An HSSI organization row with exactly that name and ROR already existed before this refresh, so
  recording it mints neither an identifier-less row (the LSE Space cost) nor a second new one (the
  ESOC cost).
- On the searcher's side it is the only one of the three a heliophysics reader can place without
  looking anything up, and it does not mislead them about the institutional context of the work.

**The honest cost of the value, recorded rather than buried.** `European Space Agency` is an
**inference** — from ESOC being an ESA establishment and from the address domain — not a
transcription of any employment entry on his ORCID, which names ESA nowhere. `LSE Space GmbH` is the
transcription. A future refresh that concluded strict fidelity to the person's own profile outranks
legibility would be making a coherent argument rather than correcting an error, and should say so
explicitly instead of treating this value as a defect.

**Considered and rejected — `LSE Space GmbH`, no identifier.** The literal answer, and the only
institution his profile says he was employed by in 2019. Rejected on two costs: it has no ROR, so it
mints an identifier-less HSSI organization row that nothing later can match on; and to a reader it
names an engineering-services contractor rather than the agency the work served.

**Considered and rejected — `European Space Operations Centre`, `https://ror.org/0541jr710`.**
Recorded first, on the misattributed department, and the weakest of the three once that was repaired.
It carries the same loss of precision as ESA **plus** a defect neither other option has: his profile
scopes that relationship to a traineeship that ended in 2016, so recording it bare would assert a
2019 institutional tie the evidence does not support. It would also mint a new row. Its one
advantage — ORCID disambiguated that entry to a ROR — attaches to the traineeship, not to the work in
question.

**Considered and rejected — recording both `LSE Space GmbH` and `European Space Agency`.** HSSI
supports multiple affiliations, so this was the most complete option available: employer of record
plus agency context. Rejected because it still mints the identifier-less LSE Space row while adding
nothing a reader needs. Recording no affiliation at all was rejected on the same page: it would
discard a relationship that the commit address, the ORCID department text and the ROR disambiguation
all independently support.

**The BIPM spelling, and the rule that settles it.** Three forms of this institution's name are in
play, and the recorded value is ROR's: `Bureau international des poids et mesures`, the
`ror_display` name on `https://ror.org/055vkyj43`. Considered and not selected: the title-cased
French `Bureau International des Poids et Mesures`, which is how the author's own ORCID employment
entry renders it, and ROR's English label `International Bureau of Weights and Measures`. Recording
an organization under its ROR display name is not a blanket catalogue convention, but its reasoning
governs this case: no row for this institution existed before this refresh, so the row is created
from this affiliation entry and keyed by a ROR identifier — the ROR record *is* the thing being
pointed at, and its display name is the authoritative form for it. Where a row already exists, or
where no ROR is being attached, that argument does not apply and the question is open again. Note
also that this is a routine call rather than a user-facing one: the capitalisation of a French
institutional name reads the same to a site visitor either way, which is why it is decided by rule
rather than by the searcher's-side test. What
is *not* open is the acronym: Field 25's "Avoid acronyms and enter one organization per field"
instruction, which the affiliation sub-field follows in practice, rules out `BIPM`.

**Considered and not applied — a ROR for `Scivision, Inc.`** ROR's only "Scivision" match is
`https://ror.org/011qev639`, **SciVision Biotech Inc. (Taiwan)**, a Kaohsiung biotechnology company
with no connection to Michael Hirsch's US consultancy. Do not attach it. The wrong candidate is named
here rather than merely excluded, because it is the trap an identifier sweep walks into.

**Considered and not applied — the `Scivision, Inc.` versus `SciVision, Inc.` spelling.** DataCite
and Zenodo render the company with a capital V; the HSSI organization row is `Scivision, Inc.`. The
row is shared across records and this difference is parked catalogue-wide. It is not drift in this
record and must not be "fixed" here.

**A DataCite artifact to ignore.** For the two 2019 deposits, DataCite renders the principal author
as `{"name": "Michael Hirsch, Ph.D.", "givenName": "Ph.D.", "familyName": "Michael Hirsch"}` — a
Zenodo name-parsing failure that puts the honorific in the given-name slot. For the current deposits
it renders every creator with `familyName` set to the whole name and no `givenName` at all. Neither
shape should ever be imported; Field 6's name splits come from the repository and from each person's
own profile.

---

### 7. Software Name (MANDATORY)
**Value:** GEOrinex

**Carried over from the existing HSSI record and independently corroborated.** The PyHC registry
entry in `_data/projects_unevaluated.yml` reads
`- name: GEOrinex` / `  code: https://github.com/geospace-code/georinex`, which is the same string
HSSI stores. PyHC metadata is manually curated and takes priority over automated extraction.

**The other renderings, recorded so none of them is later mistaken for a correction.** This project
spells its own name at least five ways:

| Form | Where it appears |
|---|---|
| `georinex` | the GitHub repository name, the PyPI distribution (`name = "georinex"` in `pyproject.toml`), the Python import name, and 17 occurrences in `README.md` — mostly code blocks and CLI invocations |
| `GeoRinex` | the README's own title line (`README.md:1`, `# GeoRinex`) and two body sentences (`README.md:16`, `:143`) |
| `GeoRINEX` | `README.md:38` (`is also support by GeoRINEX:`) and `ReadRinex.m:2` (`%% ReadRinex  GeoRINEX Python toolbox from Matlab`) |
| `Georinex` | `src/georinex/versions.py`, `print("Georinex", __version__)` |
| `GEOrinex` | the PyHC registry, and this record |

Decided from what a user would search for: all five forms differ only in capitalisation, and
`GEOrinex` is the curated display form that a heliophysics user arriving from the PyHC project list
will already have seen. There is no user-visible benefit to changing it, and the repository itself
offers no single authoritative alternative — it disagrees with itself across three files.

---

### 8. Description (MANDATORY)
**Value:** RINEX 2, RINEX 3, and SP3 reader with batch conversion to NetCDF4 / HDF5 in Python or Matlab. GEOrinex reads plain, compressed, and Hatanaka-compressed GNSS navigation and observation files into xarray datasets for filtering, plotting, and offline analysis, and can write converted NetCDF4 outputs for faster reuse on large datasets.

**A value change in this refresh: the RINEX 4 term was removed from the stored description.** HSSI
stored `RINEX 2, RINEX 3, RINEX 4, and SP3 reader …`; the recorded value drops that one term and is
otherwise the submitted wording, word for word. Everything else in it is preserved as editorial
intent. The reason for the departure is set out below, because this record now deliberately says
something narrower than the software's own front page.

Every other factual claim in the value was checked against the pinned source, and all of them hold:

- *RINEX 2, RINEX 3, and SP3 reader with batch conversion to NetCDF4 / HDF5 in Python or Matlab* —
  `README.md:7`, and `src/georinex/base.py` dispatching to `rinexobs2`/`rinexobs3`,
  `rinexnav2`/`rinexnav3` and `load_sp3`. The MATLAB path is `ReadRinex.m`, whose body calls
  `dat = py.georinex.load(fn);`.
- *plain, compressed, and Hatanaka-compressed* — `src/georinex/rio.py`'s `opener()` handles gzip
  (`:52`), bzip2 (`:65`), zip (`:79`), LZW `.Z` (`:88`) and plain text (`:103`), invoking
  `crx2rnx` on Hatanaka content in each branch; `README.md:29`–`:34`.
- *navigation and observation files* — `README.md:27`–`:28` lists `NAV` and `OBS`.
- *into xarray datasets* — the readers return `xarray.Dataset` objects (`load` returns a dict of two
  of them when a `.nc` file holds both a NAV and an OBS group, `base.py:93`–`:94`); `README.md:13`
  links `[xarray.Dataset]`.
- *for filtering, plotting, and offline analysis* — `tlim`/`use`/`meas`/`interval` filtering,
  `src/georinex/plots.py` and `plots_geo.py`, and `README.md:19`, which describes the project's
  initial goal as `one-time offline conversion of ASCII (and compressed ASCII) RINEX to HDF5/NetCDF4,`.
- *can write converted NetCDF4 outputs for faster reuse on large datasets* — `README.md:46` and
  `:109`–`:110`; `base.py` writes with `to_netcdf(..., format="NETCDF4")`.

**Why this record does not repeat the project's RINEX 4 claim.** The README asserts RINEX 4 support
in three places — `README.md:7`, `:26` and `:83` — and the code at the pin does not implement it.
`src/georinex/base.py:212` reads `if int(info["version"]) in {1, 2}:` and `:223` reads
`elif int(info["version"]) == 3:`, with `:235` falling through to
`raise ValueError(f"unknown RINEX {info}  {fn}")`; the navigation path at `:160`, `:162` and `:165`
has the same shape, ending in `raise LookupError(f"unknown RINEX  {info}  {fn}")`. A file whose
header version parses to 4 therefore raises rather than loading. The repository ships a RINEX 4
fixture, `src/georinex/tests/obs4.00gage.19o`, that no test at the pin references, and GitHub issue
number 83, "Rinex 4" — the standing feature request, opened 2022-01-12 — is still open.

The decision turns on the governing test, whose subject is the person using the HSSI website: a user
who finds this record by filtering for RINEX 4 support, installs the package and gets a `ValueError`
has been misled by the catalogue. A description that repeats an upstream claim the software cannot
honour transfers that defect to every searcher who trusts the catalogue, and a searcher has no way to
discover the gap short of reading `base.py`. So the record states what the software does.

**If RINEX 4 support ever lands upstream, restore the term.** The removal is a statement about the
code at this pinned revision, not a judgement that the project will never support RINEX 4 — its
maintainer evidently intends to, having added the claim and a fixture in 2025. A future refresh that
finds version 4 in the `base.py` dispatch, or issue 83 closed by an implementation rather than by
abandonment, should put RINEX 4 back into Fields 8 and 9 and delete this paragraph.

**Considered and rejected — keeping the project's own wording.** The argument for it is real, and it
is the stronger case for the other side: a catalogue entry is normally supposed to
reflect the software's self-description, the README is the authoritative statement of what the
project says it is, and the mismatch is an upstream defect for the maintainer to resolve rather than
a metadata error. It was rejected because the catalogue's obligation runs to its own users before it
runs to fidelity with an upstream page, and because nothing is lost by stating the narrower truth: a
reader who wants the project's own claim can follow Field 3 to the README, which still makes it.

---

### 9. Concise Description (OPTIONAL)
**Value:** Python RINEX 2/3 and SP3 reader with batch conversion to NetCDF4/HDF5 for GNSS processing, plotting, and scalable offline analysis of large local datasets.

**The RINEX 4 term was removed here too, for the reasons under Field 8; the value is otherwise the
submitted wording unchanged.** `2/3/4` became `2/3`, taking the string from 157 to **155
characters** — still inside the 200-character cap and still inside the 150–200 band the form asks
for, so nothing had to be reworded to keep it in range. "local datasets" is accurate and is worth
keeping: it is the one phrase in either description that tells a user this package does not fetch
data (Field 17).

---

### 10. Publication Date (RECOMMENDED)
**Value:** 2015-04-21

**Carried over from the existing HSSI record and independently confirmed by two sources that agree to
the second.** The earliest commit on the pinned lineage is
`b08f716986205c86d8192c9e555f386a9dbf1d72`, "Initial commit", authored 2015-04-20 19:19:29 −0600 =
**2015-04-21T01:19:29Z**, and the GitHub API reports this repository's `created_at` as
`2015-04-21T01:19:29Z`. The stored value is the UTC date; a reader who checks `git log` with local
formatting will see 2015-04-20 and should not treat that as drift.

**A caution about this repository's history shape.** `git rev-list --max-parents=0` restricted to the
pin returns exactly one root commit, `b08f7169`. Anyone re-deriving this date must scope the walk to
the pinned lineage (`git rev-list <pin>`), not `git log --all`: the geospace-code and space-physics
repositories carry tags on pre-rewrite orphan lineages, and `--all` has produced confidently wrong
corrections elsewhere in this catalogue.

**Considered and not selected — 2016-12-20.** That is the date of the first Zenodo deposit,
`10.5281/zenodo.213688` (`scienceopen/pyrinex: Initial release`, v0.1), and is a defensible reading
of Field 10's "Date of first broadcast/publication." It was not selected because the source has been
public
since April 2015 and the deposit dates properly belong to Field 12's version record. Recorded also
because the previous extraction's note on this point was wrong in three ways — it gave the first
release as "v0.5.0 (2017-05-30, DOI: 10.5281/zenodo.569328)", whereas `10.5281/zenodo.569328` is
`scienceopen/pyrinex v1.0.0`, issued 2017-04-26, and is not the earliest of the 48 deposits.

---

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Carried over unchanged.** Field 11's instruction is conditional: "For software where a DOI has been
obtained through Zenodo (e.g., GitHub-Zenodo workflow), Zenodo is the correct entry. If no DOI has
been obtained, indicate the repository host, such as GitHub or GitLab." A Zenodo DOI has been
obtained through exactly that workflow — the concept record's
`IsSupplementTo https://github.com/geospace-code/georinex/tree/v1.16.2` relation is the GitHub
integration's signature — and DataCite records the publisher as `Zenodo`.

**This value is contingent on Field 2 and the two move together.** If the Zenodo DOI were ever
withdrawn from Field 2, Publisher would have to return to the repository host.

---

### 12. Version (RECOMMENDED)

#### Latest Version:
- **Version Number:** v1.16.2
- **Version Date:** 2023-11-15
- **Version Description:** Fixed numerous bugs, including xarray API update. Requires Python 3.8+ as Python 3.7 library support and wheel availability is dwindling.
- **Version PID:** https://doi.org/10.5281/zenodo.10130117

**All four sub-fields are carried over unchanged, and each is confirmed.**

**Version Number — `v1.16.2` is the latest release, and it must not be bumped.** Four sources agree:
`src/georinex/__init__.py` at the pin sets `__version__ = "1.16.2"`; the newest git tag is `v1.16.2`;
the newest GitHub release is `v1.16.2`; and the **PyPI JSON API** (`https://pypi.org/pypi/georinex/json`)
reports `info.version: 1.16.2` across 34 releases. The JSON API is the authoritative check here
because PyPI's HTML project page returns 200 even for packages that do not exist.

The tag resolves to `da3eb3e5af30d38e1c865854682447800503bfc8` (authored 2023-11-15 01:40:03 −0500 =
2023-11-15T06:40:03Z) and `git merge-base --is-ancestor` confirms it is a genuine ancestor of the
pinned revision. **Twenty commits sit between the tag and the pin** — Python ≥ 3.10, the
`importlib.resources` migration, the `georinex.gtime` module rename, RINEX 3.05 header handling, type
hints and documentation. That is ordinary unreleased development, not a new version, and no version
number should be invented for it.

The `v` prefix is kept. `pyproject.toml` derives the version from `georinex.__version__`, so PyPI
shows the bare `1.16.2`, while the tag and the GitHub release both carry the `v`. Field 12's own
guidance uses `v1.0.0` as its example, and a user reading either form is neither confused nor
annoyed. Replacing a version value also orphans the previous `SoftwareVersion` row — accepted HSSI
behaviour, never a reason to avoid a needed correction, but here there is no correction to make.

**Version Date — 2023-11-15, from four independent sources.** The tagged commit's author date
(2023-11-15T06:40:03Z), the GitHub release `published_at` (2023-11-15T06:50:17Z), Zenodo's
`Issued 2023-11-15` for the version DOI, and the PyPI upload times for
`georinex-1.16.2-py3-none-any.whl` (2023-11-15T06:54:24) and `georinex-1.16.2.tar.gz`
(2023-11-15T06:54:26).

**Version Description — kept, and here is why it is not a quotation.** No source carries the stored
string exactly. The GitHub release title is `numerous bugfixes. Requires Python >= 3.8` and its body
is two paragraphs beginning `FIxed numerous bugs, including xarray API update` — with a capital "I"
in "FIxed" — followed by
`Requires Python 3.8+ as Python 3.7 library support and wheel availability is dwindling.` The stored
value is that body with the typo corrected and the paragraph break flattened into a sentence break.
That is the right rendering for a field a user reads as a change note, and it is recorded here
explicitly so a later refresh does not flag the difference as drift and "fix" it back to the typo.

The "Requires Python 3.8+" claim is historically accurate and should not be updated to match the pin:
`git show v1.16.2:pyproject.toml` gives `requires-python = ">=3.8"`, whereas the pin now declares
`requires-python = ">=3.10"`. The version description describes the version, not the current tree.

**Version PID — `https://doi.org/10.5281/zenodo.10130117`, established independently.** DataCite
gives that DOI `version: v1.16.2`, `Issued 2023-11-15`, title
`geospace-code/georinex: numerous bugfixes. Requires Python >= 3.8`, and
`IsVersionOf 10.5281/zenodo.595473`. It is a version DOI, distinct from Field 2's concept DOI, which
is what this sub-field asks for.

---

### 13. Programming Language (RECOMMENDED)
**Values:**
- MATLAB
- Python 3.x

**Carried over unchanged.** `pyproject.toml` declares `"Programming Language :: Python :: 3"` and
`requires-python = ">=3.10"`; `.github/workflows/ci.yml` tests Python 3.10, 3.11, 3.12 and 3.13. The
MATLAB layer is two tracked files, `ReadRinex.m` (a function that calls `py.georinex.load(fn)` and
plots the result) and `matlab/demo_rinex.m` (which uses MATLAB's own `rinexread`). The GitHub
language API reports `Python: 144698` and `MATLAB: 1268` bytes and nothing else, which matches the
tree.

**Considered and not selected — `Python 2.x`.** Early history supported Python 2 (commit
`946eec8ceb61acbc8d387ebea2d2a95498801c72`, 2015-04-26, "self-test for python 2, 3. Handle wider
range of defective RINEX"), but the pin requires 3.10 or newer. Field 13 describes the software as it
is, not as it was.

---

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found

**Evidenced absence, not an unexamined gap.** There is no paper describing this software. An ADS
full-text search for `full:"georinex"` returns 13 documents; two are this project's own Zenodo
deposits and the other eleven are papers that *use* the package (the notable ones are recorded in
Field 27). None of them is about georinex. There is no JOSS, SoftwareX, GPS Solutions or other
software paper for it, and none is referenced from the repository.

**Why the `CITATION` file does not supply this field.** `CITATION` contains a single line,
`https://doi.org/10.5281/zenodo.3401498`, which is a Zenodo software deposit for v1.13.0, not a
publication. Field 2 already carries the software's concept DOI, and putting a version DOI here
would duplicate that identifier while asserting it is a paper.

**Considered and rejected — Hatanaka (2008).** `README.md:295` cites
`Hatanaka, Y. (2008), A Compression Format and Tools for GNSS Observation Data, Bulletin of the Geospatioal Information Authority of Japan, 55, 21-30.`
That is the reference for the CRINEX compression format the package can decompress, not a
description of this software. Field 14 asks for the publication that describes the software. (The
misspelling "Geospatioal" is the repository's own; the line is quoted as written.)

---

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

**HSSI held no license value before this refresh.** The value is derived from the repository, never
from DOI autofill.

**Evidence.** `LICENSE.txt:1` is `The MIT License (MIT)` and `LICENSE.txt:3` is
`Copyright (c) 2015 Michael Hirsch`; the file continues with the standard MIT permission grant and
warranty disclaimer. `pyproject.toml` declares the classifier
`"License :: OSI Approved :: MIT License"`, PyPI carries that same classifier, and GitHub's licence
detection reports `key: mit`, `spdx_id: MIT`, `name: MIT License`.

**The licence file is `LICENSE.txt`, not `LICENSE`** — worth noting because a tool that looks only
for the extensionless name finds nothing here.

`MIT License` is the exact stored name of the controlled-vocabulary row, and that row carries
`url: https://spdx.org/licenses/MIT`, which is the URI recorded above.

**Why not the Zenodo value — this is the trap in this record.** The Zenodo deposit for v1.16.2, and
the concept record with it, declares
`rightsList: [{"rights": "Creative Commons Attribution 4.0 International", "rightsUri": "https://creativecommons.org/licenses/by/4.0/legalcode", "rightsIdentifier": "cc-by-4.0"}]`.
`Creative Commons Attribution 4.0 International` is a real row in HSSI's License vocabulary, so DOI
autofill would populate this field with a wrong-but-valid value and nothing would reject it. It is
the depositor's own error, contradicted by three repository-internal sources and by GitHub's
detection. The repository is authoritative for this field.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- ephemeris
- gnss
- gps
- hdf5
- ionosphere
- ionosphere_thermosphere_mesosphere
- NetCDF4
- rinex
- sp3

**Seven values were carried over from the existing HSSI record; two were added in this refresh** —
`ionosphere` and `ephemeris`. Both reuse existing vocabulary rows rather than minting
near-duplicates.

**Provenance of the carried-over seven.** GitHub's topic list for this repository is exactly
`['gnss', 'gps', 'rinex']`. `pyproject.toml` declares `keywords = ["RINEX", "sp3", "HDF5", "NetCDF4"]`.
The PyHC registry entry supplies `ionosphere_thermosphere_mesosphere`. The stored casing is mixed
(`hdf5` lower, `NetCDF4` mixed) because keyword rows are shared catalogue-wide and were created by
different records; the view API title-cases them for display in any case, so this is not drift to
fix here.

**`ionosphere` — the highest-value addition.** It is what makes this package findable by the
community most likely to want it. The justification is the same evidence that carries Field 5: the
`ionospheric_corr_*` dataset attributes parsed in `src/georinex/nav2.py:205`–`:209` and
`src/georinex/nav3.py:143`–`:155`, and the ionospheric literature built on the package, both papers
of which are cited under Field 5.
Before this refresh the only ionosphere-adjacent keyword on the record was
`ionosphere_thermosphere_mesosphere`, which is PyHC's underscore-joined domain key and reads as
machine output rather than a term a person would type into a search box.

**`ephemeris` — added because SP3 is a first-class capability that no stored keyword named in
words.** `sp3` was stored, but that is a format code; a user searching for ephemeris or orbit
products would not have found this record. The evidence is direct: `src/georinex/sp3.py` implements
`load_sp3` for SP3-a, SP3-c and SP3-d; `README.md:37` describes
`[SP3 ephemeris / clock](https://gssc.esa.int/education/library/standards-and-data-formats/file-formats/sp3/)`;
and the pinned revision is itself the commit "doc: SP3 ephemeris support details". The broadcast
ephemeris in RINEX NAV files is the other half of the same capability.

**Considered and not selected.** `orbit`, `geodesy`, `navigation`, `satellite`, `python` and `xarray`
all exist as rows and are all arguably true of this package, but each is either too generic to
discriminate (`python`, `satellite`, `orbit`) or describes the surrounding discipline rather than the
software (`geodesy`, `navigation`). `total electron content` exists as a row and was rejected
outright: the package does not compute TEC, and a user searching that term wants software that
produces the quantity. Adding `hatanaka` or `crinex` was considered — the CRINEX support is genuinely
distinctive — but neither string exists in the vocabulary, and Field 18's `Other` plus Field 29's
`hatanaka` entry already record the capability where a user will meet it.

**`ionosphere_thermosphere_mesosphere` — kept, not because it is a good keyword but because removing
it here would be the wrong scope.** It is the PyHC registry's own domain key, it appears on many
records, and normalising it is a catalogue-wide question rather than this entry's. Note the tension
with Field 5, where the thermosphere and mesosphere components of that same key were rejected for
lack of evidence: an unexamined PyHC keyword is weak evidence about a Region and adequate as a
searchable tag, and those are different bars.

---

### 17. Data Sources (OPTIONAL)
**Value:** Not applicable — no remote data source

**Carried over as empty, and this is an evidenced-empty rather than an unexamined gap.** The package
performs no remote retrieval of any kind; see the scope note for the grep that establishes it. Every
input arrives as a local `pathlib.Path`, a directory glob, or an `io.StringIO` text stream —
`src/georinex/rio.py`'s `opener()` accepts exactly those and raises
`OSError(f"Unsure what to do with input of type: {type(fn)}")` for anything else.

**The seventeen rows in this vocabulary name remote archives, services and access protocols, plus a
catch-all** — `AMDA`, `CDAWeb`, `das2`, `FTP/FTPS Directories`, `GFZ`, `HAPI`,
`HTTP/HTTPS Directories`, `Madrigal`, `Observatory/Mission-specific`, `OMNIWeb`, `Other`,
`S3/Cloud-aware`, `SSCWeb`, `TAP`, `The Virtual Solar Observatory.`, `VirES` and `WDC`. This package
reaches none of them, which is why the field is correctly empty rather than a candidate for `Other`:
`Other` would assert some data source exists, and none does.

**Considered and rejected — `FTP/FTPS Directories`.** `README.md:276`–`:286` lists UNAVCO FTP paths
(`ftp://data-out.unavco.org/pub/rinex3/obs/` and three siblings) under a "Data" heading, and
`README.md:206`–`:207` links two example files there. These are places a user is told to go and
fetch RINEX by hand; nothing in the package opens them. Selecting an access protocol the software
cannot use would tell a user it can download data, which it cannot. Those UNAVCO hostnames are also
the operator's retired branding — EarthScope now runs that archive — which is a further reason not to
encode them into a field.

---

### 18. Input File Formats (RECOMMENDED)
**Values:**
- ascii
- netCDF3/4
- Other

**Carried over unchanged.**

**`ascii`** — RINEX and SP3 are line-oriented ASCII formats, and the package reads them as text
throughout: `src/georinex/rio.py:104` opens uncompressed files with
`fn.open("r", encoding="ascii", errors="ignore")`, and the zip branch at `:85` wraps entries with
`io.TextIOWrapper(bf, encoding="ascii", errors="ignore")`. `README.md:29` heads the input list with
`* Plain ASCII or seamlessly read compressed ASCII in:`.

**`netCDF3/4`** — the package reads back the NetCDF4 files it writes. `src/georinex/base.py:81`–`:100`
handles a `.nc` input by trying `rinexnav` (`:84`) and `rinexobs` (`:89`) on it, each of which calls
`xarray.open_dataset(fn, group=group)` (`:153`, `:204`) for the `NAV` and `OBS` groups.
`README.md:96`–`:99` documents `python -m georinex.read myrinex.nc`, and the test suite ships
converted fixtures such as `src/georinex/tests/data/demo_nav3.10n.nc`.

**`Other`** — the compression wrappers, which have no rows of their own: gzip, bzip2, zip and LZW
`.Z` (`src/georinex/rio.py:52`, `:65`, `:79`, `:88`, each selected by suffix or magic number), and
Hatanaka-compressed CRINEX, decoded by `crx2rnx` in four of those branches. RINEX and SP3 themselves
also have no vocabulary row, so `Other` carries them as named formats too.

**Considered and rejected — adding `HDF5` as an input.** A NetCDF4 file is an HDF5 container, so on a
purely technical reading the package already reads HDF5. It was rejected for two reasons that a
future refresh should weigh before reopening it. First, the read path is not general: `rinexinfo`
(`src/georinex/rio.py:147`–`:156`) probes a `.nc` file only for `xarray` groups named `OBS` and
`NAV`, so an arbitrary HDF5 file yields nothing and the loader raises. Second, the project never
advertises HDF5 as an input — `README.md:24`–`:35`, the "Input data types" list, names RINEX 4/3/2
(the README's own claim, whose RINEX 4 term Fields 8 and 9 deliberately do not repeat — see there),
compressed ASCII, Hatanaka and `io.StringIO`, and nothing else. A user filtering for HDF5-input
software wants a tool that will open their HDF5 file; this one will open only its own output. The
asymmetry with Field 19, where `HDF5` **is** recorded, is deliberate and is explained there.

---

### 19. Output File Formats (RECOMMENDED)
**Values:**
- HDF5
- netCDF3/4

`netCDF3/4` was carried over from the existing HSSI record. **`HDF5` was added in this refresh.**

**`netCDF3/4`** — the only file the package writes. `src/georinex/base.py:173` and `:246` call
`to_netcdf(outfn, group=group, mode=wmode, encoding=enc, format="NETCDF4")` on the nav and obs
datasets respectively, and
`src/georinex/sp3.py` writes SP3 output the same way; the encoding constant is
`ENC = {"zlib": True, "complevel": 1, "fletcher32": True}` (`base.py:16`).

**`HDF5` — added, on the software's own wording rather than on an inference about container
formats.** The project describes its output as HDF5 in five places, and one of them is the name of a
command:

- `README.md:7` — `batch conversion to NetCDF4 / HDF5`
- `README.md:44`–`:46` — the `## Output` section, whose first bullet is
  `* File: NetCDF4 (subset of HDF5), with `zlib` compression.`
- `README.md:104` — `python -m georinex.rinex2hdf5 ~/data "*o" -o ~/data`, and the module
  `src/georinex/rinex2hdf5/` exists for exactly that purpose, its docstring reading
  `Converts RINEX 2/3 NAV/OBS to NetCDF4 / HDF5`
- `README.md:109` — `It's suggested to save the GNSS data to NetCDF4 (a subset of HDF5) with the `-o`option,`
- `README.md:173` — `If available, the `location` is written to the NetCDF4 / HDF5 output file on conversion.`

The claim is also demonstrated rather than asserted: `README.md:189`–`:193` shows the output being
read straight back with `h5py`, `with h5py.File('my.nc') as f:` followed by
`ecef = h['OBS'].attrs['position']`. A user filtering HSSI for software that produces HDF5 will get a
file they can open with h5py, which is the test that matters. Before this refresh no stored value
said so, and the CLI a user would type — `georinex.rinex2hdf5` — was undiscoverable from the
record's format fields.

**Considered and rejected — `ascii` and `csv`.** The package writes no text data product. The
`georinex.gtime` CLI prints epoch summaries to stdout for debugging
(`src/georinex/gtime/__main__.py`), which is console output, not a file format a user would filter
for.

---

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Operating System Independent
- Windows

**Carried over unchanged and confirmed against CI.** `.github/workflows/ci.yml` runs the matrix on
`ubuntu-latest` for Python 3.10–3.13, plus `windows-latest` on Python 3.12 and `macos-latest` on
Python 3.13, each installing the package with `pip install .[tests,lint,io]` and running `pytest`.

**Why all four, including the blanket value.** `pyproject.toml` declares the classifier
`"Operating System :: OS Independent"`, and here that is a substantive claim rather than boilerplate:
this is pure Python with no compiled extension and no platform-specific code path, so it genuinely
runs wherever a supported Python runs. Listing the three tested platforms tells a user where it is
verified; listing `Operating System Independent` tells a user on a fourth platform that nothing
structural stops them. Both are useful and neither contradicts the other. Note that
`Operating System Independent` is the spelled-out vocabulary row — the classifier string
`OS Independent` is not a value and could never be used verbatim.

---

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Carried over unchanged.** Nothing in the package is architecture-specific: it is pure Python with
no compiled component, no intrinsics and no architecture-conditional code. The dependency set
(`python-dateutil`, `numpy`, `xarray`, `hatanaka`, `ncompress`, `netcdf4`) ships wheels across the
common architectures.

**Considered and not selected — enumerating `x86-64` and `Apple Silicon arm64`.** That would record
where CI happens to run rather than what the software requires, and would narrow the record
misleadingly for a user on another architecture.

---

### 22. Related Phenomena (OPTIONAL)
**Value:** Not applicable — no phenomenon in the vocabulary applies

**Carried over as empty, but re-examined against the live seven-value vocabulary rather than
inherited as a blank.** The rows are `Coronal Heating`, `Coronal Mass Ejections`,
`Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and `X-ray emission`. The
vocabulary is flat, so no value implies another.

Six of the seven are solar or heliospheric phenomena with no bearing on a GNSS file reader.

**`Geomagnetic Storms` — considered, and rejected.** There is a real argument: storm-time ionospheric
disturbance is one of the main scientific reasons to process GNSS observations, and the AIDA paper in
Field 27 is space-weather work built on this package. It was rejected on the searcher's-side test.
GEOrinex parses files; it detects nothing, indexes nothing and models nothing. A user filtering HSSI
for geomagnetic-storm software wants storm indices, ring-current models or forecasting tools, and a
format reader in that result set dilutes it. The ionospheric connection is recorded where it is true
and useful — Field 5's `Earth Ionosphere` and Field 16's `ionosphere` — rather than promoted into a
phenomenon claim the software does not support.

An evidenced-empty value is a legitimate outcome for this OPTIONAL field, and this is one. Note that
the phenomenon a GNSS user would most likely search for, ionospheric scintillation, has no row in
this vocabulary; a term with no row belongs in Keywords, and it was rejected there too because the
package does not measure it.

---

### 23. Development Status (RECOMMENDED)
**Value:** Active

**HSSI held no development status before this refresh.**

**The signals.** The repository is **not** archived (`archived: false`, `disabled: false` from the
GitHub API). Its most recent commit is the pinned revision, 2026-05-27, and the GitHub API's
`pushed_at` for the repository is `2026-05-27T13:28:15Z`. Twenty commits sit after the v1.16.2 tag,
spread across 2024-01 (eight), 2025-01 (ten), 2025-03 (one) and 2026-05 (one), and they include
feature work rather than only housekeeping: RINEX 3.05 observation-header support and SBAS header
flexibility (`178036320627be5f99dc318d80476eeb1db367a8`), a Python ≥ 3.10 floor, the
`importlib.resources` migration, and the `georinex.gtime` module rename. `pyproject.toml` declares
`"Development Status :: 5 - Production/Stable"`. The last release is v1.16.2 (2023-11-15), and the
GitHub API's `open_issues_count` for the repository is 41, which counts open issues and pull
requests together.

**Clause by clause against the vocabulary's own definitions.** Unlike `FunctionCategory`, whose rows
carry no definition, the `RepoStatus` rows do carry one and it is the repostatus.org wording, so this
choice is decidable from the text of the rows.

- **`Active` — selected.** "The project has reached a stable, usable state and is being actively
  developed." *Stable, usable state*: v1.16.2 is published on PyPI as a working distribution, CI
  builds and tests it on three platforms and four Python versions, and `pyproject.toml`'s own
  classifier is Production/Stable. *Being actively developed*: commits landed in each of 2024, 2025
  and 2026, the most recent of them being the pinned revision itself, and 2025's work added format
  support rather than merely maintaining the build.
- **`Inactive` — considered and rejected on its middle clause.** "The project has reached a stable,
  usable state but is no longer being actively developed; support/maintenance will be provided as
  time allows." The first clause fits; the second does not, because development did not stop. The
  tempting evidence for `Inactive` is the release gap — nothing tagged since 2023-11-15 — and this
  note exists so that gap is not mistaken for dormancy. A project can develop on `main` without
  cutting releases, and this one demonstrably has.
- **`Unsupported` — excluded.** "The project has reached a stable, usable state but the author(s)
  have ceased all work on it. A new maintainer may be desired." Work has not ceased.
- **`WIP`, `Suspended` and `Abandoned` — excluded on the opening condition all three share**, that
  "there has not yet been a stable, usable release": 34 releases exist on PyPI and 48 deposits on
  Zenodo.
- **`Concept` — excluded.** "Minimal or no implementation has been done yet, or the repository is
  only intended to be a limited example, demo, or proof-of-concept." This is a maintained package
  whose own selftest transcript reports `158 passed, 1 skipped` (`README.md:75`).
- **`Moved` — excluded.** "The project has been moved to a new location, and the version at that
  location should be considered authoritative." The repository has been renamed twice, but the old
  paths redirect *here*; nothing was relocated away.

**What this value tells a user.** The package works, it is maintained, and a bug report has a
reasonable chance of being read — but a fix will reach them only through a git install until the
maintainer cuts a release, because PyPI has been behind `main` since November 2023.

---

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/geospace-code/georinex

**Carried over unchanged.** There is no documentation site, no `docs/` directory and no Read the Docs
configuration in the repository at the pin, and the GitHub API reports `has_pages: false` and
`has_wiki: false`. The documentation is four Markdown files in the repository root — `README.md`
(installation and selftest at `:50`–`:77`, command-line use at `:78`–`:118`, module use and worked
examples at `:119`–`:201`, benchmarks and profiling at `:202`–`:248`, and format, algorithm and data
notes at `:249`–`:296`), plus
`Readme_NAV.md`, `Readme_OBS.md` and `Readme_RINEX.md`. Field 24 explicitly allows the access URL
when documentation is not separately hosted.

---

### 25. Funder (OPTIONAL)
**Value:** Not found

**Negative research, so this is not re-searched from scratch each refresh.** No tracked file at the
pin contains a funding, grant, award or acknowledgement statement. A case-insensitive grep across
**every tracked file** at the pin for `fund|acknowledg|grant|NSF|NASA|award|sponsor` matches five
lines in five files, and none of them is a funding statement:

- `LICENSE.txt:5` — `Permission is hereby granted, free of charge, to any person obtaining a copy`,
  the MIT boilerplate.
- `src/georinex/keplerian.py:84` — `    # %% transform`, which matches only because "transform"
  contains the letters "nsf".
- Three RINEX test fixtures carrying the same antenna-model header comment,
  `G PAGES             igs05.atx @ igscb.jpl.nasa.gov          SYS / PCVS APPLIED` —
  `src/georinex/tests/data/obs3.01gage.10o:31`,
  `src/georinex/tests/data/obs3.05gage.19o:39` and `src/georinex/tests/obs4.00gage.19o:38`. A JPL
  hostname inside sample data is not a statement about this software.

DataCite records `fundingReferences: []` for the concept DOI and for the v1.16.2 version DOI.

**Considered and rejected — the funders of the papers in Field 27.** Crossref records the AIDA paper
as funded by the European Space Agency (award GT18-009EP) and the gnss_lib_py paper by the National
Science Foundation (award 2006162) and NASA's Jet Propulsion Laboratory. Those grants funded
*those* projects, which used georinex; they did not fund georinex. Recording them here would tell a
user this package was ESA- and NSF-funded work, which is not evidenced.

---

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Same negative research as Field 25.** No award title or number appears in the repository, in the
Zenodo or DataCite records, or in any source tied to this software rather than to a paper that used
it.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Values:**
- https://doi.org/10.1029/2025SW004712
- https://doi.org/10.1016/j.softx.2024.101811

**HSSI held no related publications before this refresh, and the previous extraction recorded
`Not found`.** That was true of the repository — nothing at the pin cites a paper that uses this
software — and false of the literature.

**How the candidates were found, and the pool they were drawn from.** An ADS full-text search for
`full:"georinex"` returns 13 documents: this project's own two indexed Zenodo deposits and eleven
papers that use the package. The eleven are AIDA (Space Weather 2026), PyTECGg (SoftwareX 2026), PRX
(GPS Solutions 2026), gnss_lib_py (SoftwareX 2024), GSSC Now (Advances in Space Research 2024), a
GNSS jamming-detection paper (IEEE TAES 2024), a RINEX-in-Python teaching paper (Journal of Applied
Engineering Sciences 2024), three smartphone-GNSS papers (Sensors 2023, Remote Sensing 2023 ×2) and
one unrelated engineering conference paper. Field 27 is not a citation index, so the two recorded
below were selected on a stated bar rather than by taking the whole list.

**The bar applied: an acknowledgement, not a passing mention.** ADS indexes acknowledgement sections
separately from full text, and exactly two of the eleven name this package there —
`ack:"georinex"` returns `2026SpWea..2404712R` and `2024SoftX..2701811K`. An acknowledgement is a
deliberate credit by the authors; a full-text occurrence is often a bibliography line or a
dependency roll-call. Both selected papers are peer-reviewed and CC-BY.

**Reid, B.; Themens, D. R.; Elvidge, S.; Ahmed, M. A.; Ball, W.; Hoque, M. M. (2026), "The Real-Time
Advanced Ionospheric Data Assimilation (AIDA) Model", *Space Weather* 24,
`https://doi.org/10.1029/2025SW004712`.** This is the heliophysics-relevant entry and the reason this
field is worth filling. The final sentence of its Acknowledgments section reads
`The open-source software georinex (scivision et al., 2023) was used to parsing RINEX-formatted GNSS data.`
The grammatical slip is the article's own and is quoted as published; do not silently correct it.

That sentence is a specific credit for a specific job, not a dependency roll-call, and nothing beside
it dilutes the credit — the paper's acknowledgement index carries `georinex`, `RINEX` and `software`
but no hit for `numpy` or `python`. It is the clearest vindication available of the acknowledgement
bar applied above. A user who lands on the GEOrinex record and sees that a real-time ionospheric data
assimilation model credits it learns something they cannot get from the repository.

The paper's matching reference-list entry is
`scivision, Mayorov, N., Strandberg, J., Valgur, M., Saluja, S., Estévez, D., et al. (2023). geospace-code/georinex: Numerous bugfixes. requires python >= 3.8. Zenodo.`
Two durable things follow from it. First, it cites the **v1.16.2** deposit — the title matches
`10.5281/zenodo.10130117` — so unlike the gnss_lib_py paper below, this one did **not** inherit the
stale v1.13.0 DOI that the repository's `CITATION` file publishes. Second, it prints the first
creator as the bare handle `scivision`, which is the concrete downstream cost of the Zenodo creator
list discussed in Field 6: a handle that this record resolves to Michael Hirsch reaches the published
literature unresolved, and every future citation generated from that deposit will do the same until
the deposit's creator metadata is corrected upstream.

**Knowles, D.; Kanhere, A. V.; Neamati, D.; Gao, G. (2024), "gnss_lib_py: Analyzing GNSS data with
Python", *SoftwareX* 27, 101811, `https://doi.org/10.1016/j.softx.2024.101811`.** Three independent
things make this the strongest software-side entry. Its acknowledgements read
"The authors also acknowledge the open-source code repositories on which gnss lib py was built and
depends including NumPy [25], Pandas [26], scipy [28], matplotlib [29], georinex [30], pytest [13],
unlzw3, pynmea2, plotly, and requests." (as rendered in the arXiv preprint's extracted text, where
the underscores of `gnss_lib_py` come through as spaces), and its reference [30] is
`georinex (2022).` / `URL https://doi.org/10.5281/zenodo.3401498`. The software it describes declares
`georinex<=1.16.1` in its PyPI dependencies and imports it at
`gnss_lib_py/parsers/rinex_nav.py:22` and `gnss_lib_py/parsers/rinex_obs.py:9`. And its first author,
Derek Knowles, is one of this record's own authors (Field 6). The same package is recorded in
Field 30. Note that this paper's citation of the stale v1.13.0 version DOI is the concrete downstream
cost of the `CITATION` file discussed in Field 2.

**Considered and not added — PyTECGg.** Ventriglia, V.; Guerra, M.; Okoh, D.; Vermicelli, P.;
Ciraolo, L.; Cesaroni, C. (2026), "PyTECGg: total electron content calibration with GNSS data",
*SoftwareX* 34, 102737, `https://doi.org/10.1016/j.softx.2026.102737`, is INGV work on ionospheric
TEC calibration and is the most topically aligned paper in the pool after AIDA — which is exactly why
its exclusion is written down rather than passed over. It mentions georinex in its full text but
**not** in its acknowledgements: `full:"georinex"` scoped to its bibcode returns 1, and
`ack:"georinex"` scoped the same way returns 0. It therefore fails the bar applied above, and that
bar is what keeps this field from turning into a citation index. Admitting PyTECGg would mean
widening the bar to substantive full-text use, which would also admit PRX and probably GSSC Now. The
scoped results are recorded so that a future refresh wanting to re-weigh the bar can do so without
re-running the search.

**Considered and rejected — the remaining eight.** The three smartphone-GNSS papers, the jamming
detection paper, the teaching paper and the engineering conference paper mention georinex in passing
as one tool among several; none credits it in acknowledgements, and none would tell a reader of this
record anything about the software they do not already know. Field 27 asks for publications the
developer prioritises, and with no developer prioritisation available, the acknowledgement bar is the
closest defensible proxy.

**Publisher access, recorded because it will recur for anyone re-verifying these quotations.**
AGU/Wiley article pages and ScienceDirect both return 403 to plain non-browser clients, and Europe
PMC indexes neither of these DOIs (`hitCount 0`); the Birmingham institutional repository's PDF of
the AIDA article is 403 as well, even though Unpaywall reports that article as gold open access.
**None of that is a paywall** — the AIDA article is open access and a browser renders it, which is
how the two AIDA strings above were read, from
`https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2025SW004712`. The gnss_lib_py acknowledgement
comes from the arXiv preprint, `arXiv:2404.08854`, which needs no browser. Plan for a browser rather
than treating the 403 as a dead end.

---

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Evidenced absence.** The package neither produces nor is bound to any published dataset. Its
`src/georinex/tests/data/` directory holds 72 small RINEX, CRINEX, SP3 and NetCDF
fixtures — including a genuine IGS product, `igs19362.sp3c`, and station files such as
`ab422100.18n` — but these are regression fixtures of a few kilobytes each, not a scientific dataset
with an identifier, and none carries a DOI or a landing page. The archives the README points a user
at (UNAVCO/EarthScope FTP directories, `README.md:276`–`:286`) are directory listings, not identified
datasets.

---

### 29. Related Software (OPTIONAL)
**Values:**
- https://github.com/geospace-code/pymap3d
- https://github.com/valgur/hatanaka

Before this refresh HSSI stored six entries here: `https://github.com/numpy/numpy`,
`https://github.com/pydata/xarray`, `https://github.com/scivision/pymap3d`,
`https://github.com/Unidata/netcdf4-python`, `https://github.com/valgur/hatanaka` and
`https://github.com/vapier/ncompress`. Four were removed, one was kept, and one was kept with a
corrected URL. Every decision is below.

**One bar, applied to every candidate, in both directions.** A package earns a place in Field 29 or
30 only if it is **(a) informative to a heliophysics or GNSS searcher** — it tells them something
true of *this* software and not of most Python packages — **and (b) actually connected**, by a
specific artifact in the code, docs, examples or tests. Code evidence alone does not admit a package,
and domain adjacency alone does not either. The list stored before this refresh mixed the two
standards, which is what this rework corrects.

**Tier A removals are the rule applied, not curator taste.** `resource_submission_form_fields.md`
heads its Field 30 exclusion list `**Never list these (Tier A), no exceptions:**` and enumerates
numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly, bokeh, requests, python-dateutil, pytest,
tqdm, PyYAML, click, setuptools `and the rest of the generic scientific-Python/tooling stack`. Under
Field 29 the same document states that the exclusion reaches this field too: "The generic
scientific-Python stack is excluded here too … because listing them says nothing that isn't equally
true of most of the ecosystem."

**`xarray` and `netCDF4` are not in that list, and the distinction decides two entries below.** The
same document places them in a separate **Tier B** — `astropy, xarray, cdflib, h5py, netCDF4, dask,
MATLAB, Jupyter` — which are admissible, but "**only** when a specific exchange is documented in the
public API, docs, examples, or tests — never on dependency presence alone." That is why `xarray`
survives (in Field 30, on the documented-interchange evidence recorded there) while
`netcdf4-python` does not: a Tier B package is weighed on its evidence, not excluded by name.

**`pymap3d` — kept, with its URL corrected to `https://github.com/geospace-code/pymap3d`.**
Condition (b): `src/georinex/obs2.py:13` and `src/georinex/obs3.py:11` both read
`from pymap3d import ecef2geodetic`, and `obs2.py:405` / `obs3.py:336` use it to attach
`position_geodetic` to an observation dataset whose header carries an approximate position;
`src/georinex/plots_geo.py:14` imports it as `pm` and calls `pm.ecef2geodetic` at `:40`, `:53`, `:67`
and `:76` to place satellites on the map; `src/georinex/geo.py:15` documents
`Requires pymap3d.ecef2geodetic`; `pyproject.toml` declares it in the `plot` extra;
`src/georinex/tests/test_conv.py:92` gates a test with `pytest.importorskip("pymap3d")`; and
`README.md:174`–`:175` recommends it to the user by name. Condition (a): it is a geodetic
coordinate-conversion library, not generic infrastructure — it would be absurd in a finance model —
and it is itself an HSSI entry (PyMap3D), so a user on either record is served by the link.

*The URL change, decided from what a visitor actually sees.* An HSSI page renders a `RelatedItem`'s
raw URL as the link text, so the string stored in this field is literally what a reader reads and
then clicks. The stored value was the retired `scivision/pymap3d` path — the same one `README.md:175`
still links to — which shows a visitor an owner this project left years ago. The convention for an
in-catalogue relation is to store the target entry's exact `code_repository_url`, and PyMap3D's own
HSSI record holds exactly `https://github.com/geospace-code/pymap3d`; recording that string means the
visitor reads the canonical path, follows it, and arrives at the same URL the PyMap3D entry itself
advertises. That the two paths are one resource is corroborated by the old one redirecting (200) to
the new. A `RelatedItem` row with the canonical identifier already existed, so this consolidates
rather than proliferates, and both URLs are well inside the 128-character limit that applies to these
rows.

**`hatanaka` — kept.** Condition (b): `src/georinex/rio.py:14` is `from hatanaka import crx2rnx`,
and `crx2rnx` is invoked in four of `opener()`'s branches (`:63`, `:77`, `:101`, `:109`) so that
CRINEX content is decompressed transparently regardless of the outer container; `pyproject.toml`
lists it as a required dependency; `src/georinex/tests/test_hatanaka.py` is a dedicated test module;
and `README.md:288`–`:291` credits it by name and link, reading
`Compressed Hatanaka CRINEX files are supported seamlessly via` / `[hatanaka](https://github.com/valgur/hatanaka)`.
Condition (a): Hatanaka/CRINEX compression exists only for GNSS observation data — it is a
domain-specific format library that would be meaningless outside this field — and its author,
Martin Valgur, is one of this record's own authors, having contributed the commit that adopted it
(`82b39ddc94823736aba7b21d8c7fd099d37a0e22`, 2021-04-13, "use the external hatanaka lib for
crx2rnx"). A GNSS user who sees it learns something real.

**`ncompress` — removed, and the stored URL was pointing at the wrong project anyway.** Condition (b)
is satisfied: `src/georinex/rio.py:20` is `from ncompress import decompress as unlzw`, used at `:93`
to read LZW `.Z` files, with `src/georinex/tests/test_lzw.py` covering it. It fails condition (a).
LZW decompression is I/O plumbing — the same package would be at home in any archival pipeline in any
field — and the capability it provides is already recorded where a user will meet it, in Field 18's
`Other`. Two further notes for a future refresh: the URL HSSI stored before this refresh,
`https://github.com/vapier/ncompress`, is the classic Unix `compress` C utility, whereas the Python
package this project depends on is
`https://github.com/valgur/ncompress` (PyPI `ncompress`, summary "LZW compression and decompression",
homepage `https://github.com/valgur/ncompress`), so that entry named a different project; and
if the relevance decision were ever reversed, it is the valgur URL that would be correct.

**`numpy` — removed.** Genuinely used throughout (`src/georinex/keplerian.py`, `obs2.py`, `obs3.py`,
`sp3.py`, and declared in `pyproject.toml` dependencies) and genuinely uninformative: a numpy link on
this page would be equally true of nearly every record in HSSI.

**`netcdf4-python` — removed.** This was the Tier-B case in the list HSSI held before this refresh,
so the reasoning is
recorded rather than assumed. `netcdf4` is a required dependency, `src/georinex/versions.py` prints
its version, and it is the engine behind `to_netcdf(..., format="NETCDF4")`. But it is a file-format
binding, not a peer tool: a user does not combine georinex *with* netcdf4-python, they use georinex
and get a NetCDF4 file. The output format is already recorded in Field 19, which is where a searcher
looks for it. Tier B admits a package only on a specific documented *exchange*, and writing a file in
a library's format is not one.

**`xarray` — removed from Field 29 and recorded in Field 30 instead.** Its relationship to this
package is interoperability, not similarity: it is not a competing RINEX reader, a predecessor, a
fork parent, or a domain-specific library. See Field 30 for the evidence that admits it there.

**Considered and not added — other RINEX readers.** Field 29's own definition invites
`Software that performs similar tasks but does not necessarily link together`, and the pool from
Field 27 contains two: `PRX`, a Python RINEX
pre-processing tool (GPS Solutions 2026), and MATLAB's built-in `rinexread`, which
`matlab/demo_rinex.m` actually calls. Neither was added. PRX is referenced nowhere in this repository
and the association would rest entirely on this dossier's own literature search rather than on
anything the projects say about each other; `rinexread` is a commercial toolbox function with no
repository URL to record, and the MATLAB relationship is already visible in Field 13. Recorded so a
future refresh weighs these deliberately rather than rediscovering them.

**A caution about display names.** Every `RelatedItem` row on this record carries the repository URL
in both the name and identifier positions. Such names are placeholders, are not surfaced to a user,
and must not influence which packages belong in Fields 29 and 30.

---

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://github.com/pydata/xarray
- https://github.com/Stanford-NavLab/gnss_lib_py

Before this refresh HSSI stored four entries: `https://github.com/matplotlib/matplotlib`,
`https://github.com/pandas-dev/pandas`, `https://github.com/pydata/xarray` and
`https://github.com/SciTools/cartopy`. Three were removed, one was kept, and one was added.

**`xarray` — kept, with the specific exchange cited.** xarray qualifies only on documented-exchange
evidence, never on dependency presence, and here the evidence is unusually direct: `xarray.Dataset`
is this package's **documented public interchange format**, and the README teaches the user to
operate on it with xarray's own API.

- `README.md:12`–`:14` describes the conversion target as
  `[xarray.Dataset](http://xarray.pydata.org/en/stable/api.html#dataset)` / `for easy use in analysis and plotting.`
- `README.md:143` states
  `A significant reason for using `xarray` as the base class of GeoRinex is that big data operations are fast, easy and efficient.`
- `README.md:154`–`:167`, "Join data from multiple files", instructs the user to combine outputs with
  `obs = xarray.concat((obs1, obs2), dim='time')` and `obs = xarray.merge((obs1, obs2))`.
- `README.md:180`–`:186` shows reading the converted file back with `obs = xarray.open_dataset('my.nc)`
  — the missing closing quote is the repository's own typo, reproduced here as written.
- In code, `src/georinex/base.py:153` and `:204` read groups with
  `xarray.open_dataset(fn, group=group)`, and the readers return `xarray.Dataset` objects.

A user who already works in xarray can consume this package's output and feed it onward without
writing an adapter, which is exactly what this field asks.

**`gnss_lib_py` — added, and it is the clearest demonstrated exchange this record has.** The
direction is the useful one: another domain tool imports georinex's output. Evidence — PyPI lists
`georinex<=1.16.1` among `gnss-lib-py`'s required dependencies;
`gnss_lib_py/parsers/rinex_nav.py:22` and `gnss_lib_py/parsers/rinex_obs.py:9` both read
`import georinex as gr`, and `rinex_nav.py:5` describes the arrangement as
`turn gets passed into the georinex library used to parse the rinex file.`; and the package's
peer-reviewed paper acknowledges georinex by name and cites its DOI (Field 27). It clears
condition (a) easily: `gnss-lib-py` is a GNSS analysis and state-estimation library from Stanford's
NavLab, a peer scientific tool rather than infrastructure, and its author Derek Knowles is one of
this record's authors. The URL is 46 characters, well inside the 128-character limit.

*Why Field 30 and not Field 29.* Field 29 is for software that performs *similar* tasks; gnss_lib_py
performs different tasks and *consumes* georinex's parsing. That is a demonstrated exchange, which is
Field 30's test.

**`matplotlib` — removed.** A Tier A generic plotting library, excluded without exception. It is
genuinely used (`src/georinex/plots.py:2`, `plots_geo.py:5`, `plot/__main__.py`, and the `plot` extra
in `pyproject.toml`), but "uses matplotlib for its plots" is true of most of the scientific Python
ecosystem. The plotting capability is recorded where it belongs, in Field 4.

**`cartopy` — removed.** Also Tier A by name. It is used for the map projections in
`src/georinex/plots_geo.py:29` and `:96`, and it is optional (imported in a `try`/`except` that sets
`cartopy = None`). Mapping infrastructure is generic; the map-drawing capability is recorded in
Field 4's `Data Visualization: 2D Graphics`.

**`pandas` — removed, and this one deserves its reasoning written down because the evidence looks
strong.** `README.md:196`–`:201`, "Convert to Pandas DataFrames", documents
`df = nav.to_dataframe()` and points the user at Pandas multi-indexing; `src/georinex/geo.py`
returns a `pandas.DataFrame` from `get_locations`; and `README.md:48` advertises
`In-memory: Xarray.Dataset. This allows all the database-like indexing power of Pandas to be unleashed.`
A documented `to_dataframe()` adapter is literally one of the examples Field 30's own guidance gives
for a qualifying exchange. It was removed anyway, because pandas is named in the Tier A list, which is
absolute and admits no exceptions. Recorded in full so a future refresh understands that this was a
rule applied against contrary-looking evidence, not an oversight — and so the same evidence is not
offered again as if it were new.

**Considered and not selected — MATLAB.** This is the strongest remaining Tier-B case and it was
still declined. The bridge is real: `ReadRinex.m` is a complete MATLAB entry point that calls
`dat = py.georinex.load(fn);`, converts the returned xarray variables with
`double(py.numpy.asfortranarray(V))`, and plots them; `README.md:7` advertises "in Python or Matlab";
and GitHub reports MATLAB as a language of the repository. It was not selected because Field 13
already records MATLAB as a language of this software, so the capability is discoverable, and because
Field 30 stores a URL per entry — for a commercial numerical computing environment that would be a
vendor product page rather than a repository, which reads as out of place among peer scientific
packages. The evidence is recorded rather than discarded so a later refresh that weighs the
vendor-URL awkwardness differently starts from this paragraph.

**Considered and rejected — `netCDF4` and `h5py` as interoperability partners.** `README.md:189`–`:193`
does show the output being opened with `h5py.File`, which is a genuine cross-library exchange. It was
rejected because h5py is not a dependency of this package at all — the README is telling the user
what *they* can do with an HDF5 file — and because the fact that matters to a searcher, that the
output is readable as HDF5, is recorded in Field 19 where they will look for it. Listing an I/O
library the package does not use would misdescribe the relationship.

---

### 31. Related Instruments (OPTIONAL)
**Value:** Not found

**Carried over as empty, and examined rather than left blank by default.** GEOrinex reads a data
*format*, not an instrument's data. Nothing in it is specific to any one receiver, antenna or
spacecraft: the constellation selector at `src/georinex/read/__main__.py:37`–`:39` accepts
`choices=["G", "C", "E", "S", "J", "R", "I"]` — GPS, BeiDou, Galileo, SBAS, QZSS, GLONASS and IRNSS,
i.e. every GNSS constellation RINEX 3 defines — and the parsers branch on RINEX version and record
type, never on a receiver model or a station.

**Considered and not selected — `Global Positioning Satellites for Ionosphere Monitoring`,
`https://spase-metadata.org/SMWG/Instrument/IGS/GPS_Receiver`.** Of the instrument rows examined,
this is the one with a real claim here, so the rejection is recorded rather than assumed.
Its SPASE definition begins "The GPS receiver in each tracking station within the International GNSS
Service (IGS) global network generates raw orbit" — and RINEX observation files *are* that raw
tracking data, which georinex reads. It was not selected for two reasons. First, the row is scoped by
its own name and definition to ionosphere monitoring, a science application this package does not
perform; it hands a user the observables and stops. Second, the software's relationship is to the IGS
system's *formats and products*, not to the per-station receiver, so an observatory-level association
is the accurate one, and Field 32 records it. This instrument row would become the right choice only
if that observatory-level association were ever withdrawn and an association were still wanted.

**Considered and rejected — the IUGONET per-station GPS receiver rows.** The vocabulary contains a
set of `https://spase-metadata.org/IUGONET/Instrument/RISH/HyperDenseGNSSRN/*/GPSreceiver` entries
(Uji-area schools and a police depot in Japan) and a CHAMP GPS receiver row. These are specific named
installations that this package has no relationship with; it has never read a byte of their data
specifically, and a user on any of those station pages would find a general-purpose format reader out
of place.

**A vocabulary observation, recorded so it is not re-derived.** Searching the instrument/observatory
vocabulary for the GNSS constellations themselves returns nothing usable: `GLONASS`, `BeiDou`,
`QZSS`, `IRNSS`, `NavIC`, `NAVSTAR`, `SBAS`, `WAAS` and `EGNOS` each return **0** rows, and the 16
rows matching `Galileo` are NASA's Jupiter orbiter, its instruments, and two GEOS-1/GEOS-2 ephemeris
rows whose names happen to contain the word — none of them is the European constellation. Searches for `RINEX`,
`UNAVCO` and `EarthScope` each return 0. GNSS constellations are not in SPASE as observatories, so
even a change of mind about the relevance gate could not be acted on for them until those rows exist
upstream. Nor is there an identifier-less row to worry about here: Fields 31 and 32 are
SPASE-identified by construction — a value is submittable only as a vocabulary row's canonical name
paired with its `https://spase-metadata.org/` identifier, and there is no free-type path — so the
question for this record is which rows apply, never whether a bare name could be entered.

---

### 32. Related Observatories (OPTIONAL)
**Value:** International GNSS Service — `https://spase-metadata.org/SMWG/Observatory/IGS`

**HSSI held no value here before this refresh, and the default expectation for this field was that it
should stay empty.** It is recorded because the vocabulary turns out to contain a row that fits the
relevance gate better than expected, and because the user-facing test comes out clearly in its
favour. The value is fully resolved and needs no manual disambiguation: `International GNSS Service`
is the vocabulary row's canonical `name`, copied verbatim, its `type` is 2 (observatory), and its
identifier is `https://spase-metadata.org/SMWG/Observatory/IGS`. There is one IGS observatory row and
one IGS instrument row in the vocabulary, and no other row competes for either.

**Why it is recorded.** The relevance gate admits software that implements a format or convention
specific to an observatory as a means of supporting it. The IGS is not a data archive in the excluded
sense — it is the global system whose SPASE definition begins
`The IGS global system of satellite tracking stations, Data Centers, and Analysis` /
`Centers puts high-quality GPS data and data products on line in near real time` (the stored
definition is hard-wrapped; the line break is shown as ` / `) — and the two things it publishes are
exactly the two things this package reads.

- *SP3 is an IGS product format, and the code says so.* `src/georinex/sp3.py:1`–`:4` opens with the
  docstring `SP3 format:` / `    https://kb.igs.org/hc/en-us/articles/201096516-IGS-Formats`, and
  `README.md:40`–`:42` links the three supported sub-versions to
  `https://files.igs.org/pub/data/format/sp3.txt`, `https://files.igs.org/pub/data/format/sp3c.txt`
  and `https://files.igs.org/pub/data/format/sp3d.pdf` — the IGS's own specifications. The repository
  ships a real IGS product as a fixture, `src/georinex/tests/data/igs19362.sp3c`.
- *RINEX is the IGS's exchange format*, and `Readme_RINEX.md` cites the IGS 3.05 specification and
  release notes directly.
- *The decisive consideration was the user's.* A visitor on HSSI's International GNSS Service page
  clicking through to related software is glad to find a Python reader for IGS RINEX and SP3 — it is
  among the most directly useful things that page could offer — and someone working with IGS data
  would in fact reach for this package. Both sanity checks pass, and that is what settled it.

**The case against, kept because it is genuine and a future refresh should weigh it rather than
rediscover it.** RINEX is not IGS-exclusive: it is used far beyond the IGS, by regional and national
GNSS networks and by continuously operating reference stations generally, and this repository's own
data pointers are UNAVCO archives (`README.md:276`–`:286`), not IGS ones. On that reading RINEX is a
generic multi-organisation format, which the gate sends to Fields 18/19 rather than 31/32, and the
software is format-specific rather than observatory-specific. SP3 weakens the objection without
removing it — SP3 files are produced by analysis centres that are IGS members, which is close to but
not identical with "IGS-specific". The objection did not carry, because a format-specificity argument
decides where the *format* belongs, not whether the searcher standing on the IGS page is served.

**Considered and rejected — also recording the `SMWG/Instrument/IGS/GPS_Receiver` instrument row.**
The package does read exactly what those receivers produce, which is why the option was live. It was
rejected for the reasons given under Field 31, and Field 31 is empty as a result.

**Considered and rejected — UNAVCO/EarthScope.** The README's data section points at
`ftp://data-out.unavco.org/pub/rinex3/obs/` and three sibling paths, and those archives supplied
several of the test fixtures, so they are the obvious second candidate after the IGS. Searches of the
vocabulary for `UNAVCO` and `EarthScope` return **0** rows, so there would be nothing to record even
if the gate were passed — and it would not be, since a data archive a user is told to browse by hand
is a Data Sources question (Field 17), not an observatory the software is designed to support.

---

### 33. Logo (OPTIONAL)
**Value:** Not found

**Carried over as empty, and two candidates were examined and rejected.**

**Rejected — `src/georinex/tests/example_plot.png`.** It is the only raster or vector image tracked
in the repository at the pin (a filter of `git ls-tree -r` for `.png`, `.jpg`, `.jpeg`, `.svg`,
`.gif`, `.ico` and `.webp` returns this one file, blob
`cec30dabe650f2c3ced7b417e097fe6e89ba9b38`, 84,025 bytes), and `README.md:22` embeds it as
`![RINEX plot](./src/georinex/tests/example_plot.png)`. It satisfies every mechanical requirement of
the field: pinned to the source revision at
`https://raw.githubusercontent.com/geospace-code/georinex/8d1210a0f1ada71ff7b8d0484cfaf22ff154a38e/src/georinex/tests/example_plot.png`
it serves 200 with `content-type: image/png` and 84,025 bytes, it is a real 900×900 RGBA PNG, the
repository has no `.gitattributes` so it is not LFS-tracked, and the URL is 133 characters, inside
the 200-character `URLField` limit.

It is nonetheless not a logo. Looking at it: a four-panel matplotlib figure titled
"GEOP107Q.18o  satellite G14", plotting pseudoranges, carrier phase, Doppler and signal strength
against time for a single GPS satellite on 2018-04-17. The README's own alt text calls it a "RINEX
plot". A user scanning HSSI cards would see a line chart where an identifying mark belongs.

**Rejected — a PyHC registry logo, because there isn't one.** The PyHC entry for this package in
`_data/projects_unevaluated.yml` has `name`, `code`, `description`, `contact` and `keywords`, and
**no `logo:` key**. The absence is meaningful rather than incidental: neighbouring entries in the same
file do carry one — `GOESutils` supplies a `raw.githubusercontent.com` JPEG and `DASCutils` an
`i.ibb.co` image — so the registry does record logos for this author's packages when they exist. It
simply has none for this one.

The software has no logo. That is the correct value, and an evidenced absence is a fine outcome for
this OPTIONAL field.

---

## Additional Notes

### PyHC registry status

This package appears in the PyHC registry's **unevaluated** list,
`_data/projects_unevaluated.yml`, not in `projects_core.yml` or `projects.yml`. The entry reads:

```
- name: GEOrinex
  code: https://github.com/geospace-code/georinex
  description: Python RINEX 2/3 NAV/OBS reader with speed and simplicity, handling most RINEX formats.
  contact: Michael Hirsch
  keywords: ["ionosphere_thermosphere_mesosphere","specific"]
```

Being unevaluated means PyHC has not assessed the package against its standards; it carries no
quality ratings, so nothing in that entry informs Field 23. The registry supplies the curated
software name (Field 7) and one keyword (Field 16), and its `description` is `pyproject.toml`'s own
`description = "Python RINEX 2/3 NAV/OBS reader with speed and simplicity."` with a trailing clause
added. Its keyword list is weak evidence about Region — see Field 5, where the thermosphere and
mesosphere components were rejected.

### The package's public interface, for anyone re-deriving the science fields

`src/georinex/__init__.py` exports 23 names. The ones that carry the capabilities recorded above are:

| Name | What it does |
|---|---|
| `load` | version- and type-detecting entry point for RINEX 2 and 3 OBS/NAV, SP3 and `.nc`; a version-4 header raises (Field 8) |
| `batch_convert` | glob a directory and convert each file to NetCDF4 |
| `rinexobs`, `rinexobs2`, `rinexobs3` | observation readers |
| `rinexnav`, `rinexnav2`, `rinexnav3` | navigation readers, including the `ionospheric_corr_*` attributes |
| `load_sp3` | SP3-a/c/d position, clock and velocity reader |
| `keplerian2ecef` | broadcast Keplerian elements to ECEF |
| `gettime`, `obstime2`, `obstime3`, `navtime2`, `navtime3` | epoch vectors without a full read |
| `rinexheader`, `obsheader2`, `obsheader3`, `navheader2`, `navheader3`, `rinexinfo` | header inspection |
| `globber`, `to_datetime` | path and time helpers |

Five console entry points exist as `__main__` modules: `georinex.read` (read, convert and plot),
`georinex.rinex2hdf5` (batch convert), `georinex.plot` (four-panel observable plot),
`georinex.loc` (receiver map) and `georinex.gtime` (epoch audit).

### Test-suite size — two numbers in the README, both recorded here

`README.md:16` says `GeoRinex has over 125 unit tests driven by Pytest.` while `README.md:75`, the
selftest transcript, shows `158 passed, 1 skipped`. Both are the repository's own statements at the
pin and neither is a metadata field; they are recorded together so a future reader does not treat one
as a correction of the other.
