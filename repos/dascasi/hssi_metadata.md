# HSSI Metadata Extraction Results

**HSSI Software ID:** abb7adf0-cc3e-4734-ac67-20a562f83c33
**Repository:** https://github.com/space-physics/dascasi
**Source Revision:** 18a3b4b0e025bface5385cd0f68f07aaea66c4d7
**Extraction Date:** 2026-08-29
**Validation Date:** 2026-08-30
**Validation Status:** PASS

**Scope note on the pinned revision.** `18a3b4b0` ("case insensitive exclude", 2026-03-26, branch
`main`) is one commit *after* tag `v3.0.0`, which points at
`a0f874a190ffb1afa1a4fe5a915ef13d5eca575d`. `git diff v3.0.0..18a3b4b0` is a single line in
`.pre-commit-config.yaml` (the FITS `exclude` regex gains a `(?i)` flag). For every purpose in this
dossier the pinned tree is the released v3.0.0 tree, so evidence cited from the pinned working tree
also describes the artifact behind the v3.0.0 release and the v3.0.0 Zenodo deposit.

**Scope note on the software's two names.** The GitHub repository, the Python package, and the PyPI
distribution are all named `dascasi` at this revision; the distribution was named `dascutils` through
v2.3.0. HSSI's software name is `DASCutils`. Field 7 explains why that is correct rather than stale.
Throughout this dossier "DASCutils" means the HSSI record and "dascasi" means the package/repository
as it exists at the pinned revision.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Source:** Not derivable from the repository or from the published HSSI record. The placeholder is
the catalogue convention for entries whose submitter identity is not part of the public metadata; it
is deliberate, not an unfilled gap.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.595465

**Source:** Carried over from the existing HSSI record; independently confirmed against the DataCite
record for `10.5281/zenodo.595465` (https://api.datacite.org/dois/10.5281/zenodo.595465).

**Why this DOI and not another.** `10.5281/zenodo.595465` is the Zenodo *concept* DOI — the
software-level identifier that resolves to whichever version is latest. Its DataCite record carries
seventeen `HasVersion` relations, among them `10.5281/zenodo.19229352` (v3.0.0) and
`10.5281/zenodo.3471731`. That relation set is what proves it is the concept record rather than one
more version record. Field 2 asks for the identifier of the software; the version-specific DOI
belongs in Field 12 and is recorded there.

**Do not "correct" this to the DOI in the `CITATION` file.** The repository's `CITATION` file
contains exactly one line, `https://doi.org/10.5281/zenodo.3471731`, and has carried that value
since 2021-10-13; the one later commit touching the file, in March 2026, added a trailing newline
and left the DOI unchanged.
DataCite resolves `10.5281/zenodo.3471731` to "space-physics/dascutils: refactor for efficiency with
dict of xarray.DataArray", version `v2.0.0`, issued 2019-10-03. It is a superseded *version* DOI, not
the software's persistent identifier, and it names the software by its former distribution name. A
future agent reading `CITATION` in isolation will be tempted to promote it; that would replace a
stable concept DOI with a six-year-old snapshot.

**Also rejected:** the README's Zenodo badge target `https://zenodo.org/badge/latestdoi/51016067`.
It is a redirect service keyed on the GitHub repository id, not a DOI, and resolves to a moving
target.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/space-physics/dascasi

**Source:** Carried over from the existing HSSI record; confirmed as the `origin` of the pinned local
clone and against the GitHub API record at `https://api.github.com/repos/space-physics/dascasi`
(default branch `main`, not archived, last push 2026-03-26). Every later GitHub API claim in this
dossier about this repository — repository creation date, topics, licence, language byte counts, and
the release metadata — comes from that endpoint and its `/languages` and `/releases/latest`
sub-resources.

**Durable note on the former path.** `https://github.com/space-physics/dascutils` still resolves —
the GitHub API returns `Moved Permanently` for it — because GitHub keeps a redirect after a
repository rename. The canonical path is `space-physics/dascasi`, and that is what is recorded here.
The PyPI page for the retired `dascutils` distribution still lists `https://github.com/space-physics/dascasi`
as its home page, which independently confirms the rename rather than a fork.

### 4. Software Functionality (RECOMMENDED — treated as critical)
**Values:**
- Coordinate Transforms
- Data Processing and Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Movies

**Source:** Ten of these eleven were carried over from the existing HSSI record, which held no
`Data Processing and Analysis: Data Reduction` value before this refresh; that eleventh value is
derived from the pinned source (see below). All eleven exist as rows in the live `FunctionCategory`
vocabulary, and each subcategory's parent was resolved from the row's own `parents` link rather than
assumed.

**Evidence for each retained value.**

- **Coordinate Transforms** — `src/dascasi/dio.py::_project` calls `pymap3d`'s `pm.aer2geodetic` to
  convert per-pixel azimuth/elevation plus a slant range derived from an assumed emission altitude
  (`mapalt_km * 1e3 / np.sin(np.radians(eli))`) into geodetic latitude/longitude about the camera's
  geodetic origin. It is user-facing: `du.load(..., wavelength_altitude_km=...)` triggers it, README
  devotes its "Map Projection" section to it, and `src/dascasi/tests/test_projection.py` asserts
  specific reference lat/lon values for the 428/558/630 nm channels.
- **Data Processing and Analysis** — parent of the five subcategories below.
- **… : Calibration** — `loadcal` is one of four names exported from `src/dascasi/__init__.py`. It
  reads the DASC azimuth/elevation plate-scale FITS pair, masks the zero-valued off-sky pixels to
  NaN, and range-checks the result (0–360° azimuth, 0–90° elevation). `_azel` applies the calibration
  to the loaded stack. README's "Spatial registration (plate scale)" section documents it, including
  the caveat that the end user must verify the calibration against sky features.
- **… : Data Access and Retrieval** — `download` is exported from `__init__.py`; `src/dascasi/web.py`
  walks the remote archive tree and retrieves the matching files; `src/dascasi/download.py` exposes
  it as the `python -m dascasi.download SITE START END OUTDIR` command documented in the README.
- **… : File Format Conversion** — `save_hdf5` (exported) writes a FITS-derived image stack to HDF5,
  and `scripts/ConvertDASC_FITS_to_HDF5.py` is a dedicated FITS-stack → HDF5 converter with its own
  README section.
- **… : Image Processing** — `dio.py::_loadimg` implements DASC-specific pixel handling: unpacking
  unsigned 14-bit data written into signed 16-bit integers, rotating by `k=-1` for pre-2012 frames
  and `k=+1` otherwise, and zeroing/clipping values above 16384 left by the 2013 RAID corruption.
  `src/dascasi/projection.py::interpSpeedUp` re-grids the image stack onto a regular geographic mesh
  via Delaunay triangulation and barycentric interpolation.
- **… : Processing** — the pipeline `_slicereq → _sift → _camloc → _azel → _project` inside a single
  `load()` call is a processing chain rather than any one of the specific subcategories.
- **Data Visualization** — parent of the two subcategories below; `src/dascasi/plots.py` is a
  dedicated plotting module.
- **… : 2D Graphics** — `pcolormesh` and `contour`/`clabel` across `image_azel`, `pcolor_azel`,
  `contour_azel` and `plot_projected_image`; `imshow` in `moviedasc`; and a bar histogram in
  `histogram_dasc`, whose only plotting call is `a.hist(imgs[i].values.ravel(), bins=128)`.
- **… : Movies** — `moviedasc` steps a fixed cadence through the time axis, updates the image handles
  in place, and writes one PNG per timestep; `python -m dascasi.movie` is the documented entry point
  and the README has a "Make movies from DASC raw data files" section.

**Why `Data Processing and Analysis: Data Reduction` is recorded.** `dio.py::_azel` computes an
integer downscale factor when the calibration grid is coarser than the image grid and applies
`skimage.transform.downscale_local_mean` to the image stack, logging
`downsizing images by factors of ... to match calibration data`. That is local-mean binning to reduce
array size while preserving the signal, which is what the taxonomy's `Data Reduction` subcategory
covers — reducing data volume while preserving information (averaging, binning, downsampling). The
`FunctionCategory` rows themselves carry no definition text, so that characterization comes from the
classification guidance rather than from the vocabulary. It is
not incidental: `scikit-image` is declared in the `full` extra of `pyproject.toml`, and `dio.py`
raises `ImportError("pip install scikit-image")` when the downscale path is needed and the package is
missing. The reduction is visible to the caller, since `du.load()` returns the downscaled stack.
`_slicereq`'s time-window and wavelength subsetting reduces the returned stack further.

**Considered and not selected, with reasons.**

- **`Coordinate Transforms: Ionospheric`** — the taxonomy scopes this subcategory to conversions
  between *ionospheric coordinate systems* (AACGM, MLT, magnetic latitude, apex coordinates); the
  `FunctionCategory` row carries no definition text of its own, so that scope comes from the
  classification guidance. DASCutils performs a *geometric* AER →
  geodetic projection and never computes a magnetic coordinate. The README makes the boundary
  explicit: "Be sure you know if you're using magnetic north or geographic north" — the software
  leaves magnetic-frame handling to the user. One artifact will mislead a grep: `dio.py::load`'s
  docstring line "Bdecl is in degrees, from IGRF model" is stale — `load()` has no `Bdecl` parameter
  and no IGRF or magnetic-field code exists in the pinned tree. A case-insensitive search of the
  tracked source for `IGRF`, `AACGM`, `magnetic` and `Bdecl` returns only that docstring line and the
  README caveat quoted above. Re-add only if a magnetic-coordinate transform is actually
  implemented.
- **`Data Processing and Analysis: Analysis`** — the package derives no physical quantity. `pyproject.toml`
  describes it as "UAF Digital All-Sky Camera: reading and plotting", and the nearest thing to an
  analysis product, `plots.py::histogram_dasc`, is a per-wavelength intensity histogram that exists
  as a diagnostic figure and is already covered by Data Visualization: 2D Graphics.
- **`Data Processing and Analysis: Time Series Analysis`** — `utils.py::get_time_slice` and
  `DataArray.sel(time=..., method="nearest")` are time *indexing*, not temporal analysis. No
  filtering, detrending, or autocorrelation exists in the pinned tree.
- **`Data Visualization: Line Plots`** — no line plotting. The contour overlays are 2D contours and
  `histogram_dasc` draws bars.
- **`Data Processing and Analysis: 2D Slices` / `Data Visualization: 2D Slices`** — the stack's third
  axis is time, not a spatial dimension, so extracting a frame is not a slice through a data volume.
- **The whole `Mission-related` branch** — DASCutils is a third-party user tool for a ground-based
  observatory instrument, not part of an instrument team's ground system or a mission pipeline.
- **The whole `Models and Simulations` branch** — the projection assumes a per-wavelength emission
  altitude supplied by the caller; it does not model emission physics.
- **The whole `Servers and Environments` branch** — no container, server, or HPC tooling in the tree.

### 5. Related Region (RECOMMENDED — treated as critical)
**Values:**
- Earth Atmosphere
- Earth Auroral Subregion
- Earth Ionosphere
- Earth Thermosphere

**Source:** `Earth Atmosphere` is carried over from the existing HSSI record, which held that value
alone before this refresh. The other three are derived from the repository evidence below. All four
exist as rows in the live 24-row `Region` vocabulary.

**The vocabulary is flat.** Every `Region` row is top-level; there is no parent/child relation among
them. Consequently a coarse value never implies a fine one and a fine value never implies its coarse
neighbour — each of the four below is justified on its own evidence, and no "X encompasses Y"
argument is used or accepted here.

- **Earth Atmosphere** — the DASC images optical emission from Earth's upper atmosphere.
  `pyproject.toml` carries the classifier `Topic :: Scientific/Engineering :: Atmospheric Science`,
  and the PyHC registry entry tags the project `ionosphere_thermosphere_mesosphere`. That entry lives
  in `_data/projects_unevaluated.yml`
  (https://github.com/heliophysicsPy/heliophysicsPy.github.io/blob/main/_data/projects_unevaluated.yml);
  every later reference in this dossier to "the PyHC registry entry" means that record.
- **Earth Auroral Subregion** — auroral imaging is the software's central scientific use. README:
  "A common task in auroral and airglow analysis is to project the image to an imaginary alttiude"
  (the typo is the README's). `scripts/dasc_hist.py` is documented as projecting "HiST auroral
  tomography system FOV onto PFRR DASC". The Poker Flat site record in SPASE,
  https://spase-metadata.org/IUGONET/Observatory/NICT/SALMON/PF, declares
  `ObservatoryRegion: Earth.NearSurface.AuroralRegion`.
- **Earth Ionosphere** — the per-wavelength projection altitudes hard-coded in
  `scripts/PlotProjectedImage.py` and asserted in `src/dascasi/tests/test_projection.py` are
  428 nm → 110 km, 558 nm → 150 km, 630 nm → 200 km: E- and F-region ionospheric altitudes, with the
  630.0 nm OI line placed in the F region. The HSSI record has carried the keyword `ionosphere` since
  before this refresh.
- **Earth Thermosphere** — those same 110–200 km altitudes are thermospheric, and the 557.7 nm and
  630.0 nm auroral emissions originate from atomic oxygen in the thermosphere. The record has carried
  the keyword `thermosphere`, and the PyHC tag names the thermosphere explicitly.

**`Earth Lower and Middle Atmosphere` is deliberately not recorded.** It is the one Region candidate
whose evidence cuts both ways, so the case on each side is kept here rather than left to be
re-litigated blindly.

- *The argument for it, weighed and not decisive:* the record's stored keyword set includes
  `mesosphere`; the PyHC tag is `ionosphere_thermosphere_mesosphere`; the SPASE Poker Flat record
  cited above declares `Earth.NearSurface.Mesosphere` alongside the auroral region; the README names
  airglow as a primary use, and the 557.7 nm airglow layer sits near the mesopause; and
  `wavelength_altitude_km` accepts an arbitrary altitude, so a user can project to mesopause heights.
- *What decided it:* every projection altitude named anywhere in the pinned tree — code, scripts,
  tests, README and notebook — lies between 110 and 200 km.
  `scripts/PlotProjectedImage.py` maps 428 nm to 110 km, 558 nm to 150 km and 630 nm to 200 km (with
  150 km for the unfiltered `0000` channel), `src/dascasi/tests/test_projection.py` asserts the same
  three, and `scripts/dasc_hist.py` defaults `--projalt` to 110 km; the README discusses projection
  altitude without naming a number. The one other altitude in the source, `imgs["alt0"] = 0.0` in
  `dio.py::_camloc`, is the camera's assumed height above the ellipsoid, not an emission altitude.
  The 428/558/630 nm filter set is the standard *auroral* triplet. Decisively, the vocabulary row
  bundles the lower atmosphere — troposphere and stratosphere — with the middle atmosphere, so
  selecting it would assert support for regions the software does not address.
- *Why no narrower value was chosen instead:* the vocabulary as read on 2026-08-29 has no
  `Earth Mesosphere` row, so nothing available captures the mesospheric airglow case without also
  claiming the lower atmosphere. If such a row is added, the argument above becomes live again and
  this field should be revisited.

**Considered and not selected:** every magnetospheric row (`Earth Inner/Outer Magnetosphere`,
`Earth Magnetosheath`, `Earth Magnetosphere`, `Earth Magnetotail`), every solar and heliospheric row
(`Chromosphere`, `Corona`, `Photosphere`, `Solar Environment`, `Solar Interior`, `Solar Wind`,
`Heliosheath`, `Interplanetary Space`), and every planetary row. DASCutils is a ground-based optical
imaging tool pointed at Earth's upper atmosphere; it reads no field, particle, or solar data, and it
supports no non-terrestrial body.

### 6. Authors (MANDATORY)

**Author 1:**
- **Authors:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation 1:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** https://ror.org/05qwgg493
- **Affiliation 2:**
  - **Organization:** Scivision, Inc.
  - **Affiliation Identifier:** Not found

**Source:** Carried over from the existing HSSI record. The ORCID was confirmed against
https://pub.orcid.org/v3.0/0000-0002-1637-6526/person, which returns given name "Michael", family
name "Hirsch". The Boston University ROR was confirmed against
https://api.ror.org/v2/organizations/05qwgg493, whose `ror_display` name is exactly "Boston
University". Hirsch is the author of the overwhelming majority of commits in the pinned clone under
a set of GitHub noreply and personal addresses, is the PyHC registry `contact`, and is the
`author` of record on the retired `dascutils` PyPI distribution ("Michael Hirsch, Ph.D.", from
`https://pypi.org/pypi/dascutils/json`). Every PyPI claim in this dossier comes from that JSON API,
`https://pypi.org/pypi/<distribution>/json` — the HTML project page is bot-gated and cannot be used
to establish either presence or absence.

**Why "Scivision, Inc." carries no identifier, and should not be given one.** The ROR API returns
exactly one organization for the query "Scivision": https://ror.org/011qev639, "SciVision Biotech
Inc. (Taiwan)", a Kaohsiung biotechnology company with no connection to Michael Hirsch's US
consultancy. Attaching that ROR would be a factual error. The affiliation is genuine — the Apache
header at the top of `src/dascasi/__init__.py` reads "Copyright 2023 SciVision, Inc." — so the
identifier-less form is the correct representation, not an omission to be repaired. The stored
casing "Scivision, Inc." differs from the company's own "SciVision, Inc."; that is a stored-value
detail, not evidence of a different organization.

**Author 2:**
- **Authors:** Sebastijan Mrak
- **Author Identifier:** https://orcid.org/0000-0002-3925-760X
- **Affiliation 1:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** https://ror.org/05qwgg493

**Source:** Carried over from the existing HSSI record; corroborated by `contributors.md`, which
credits "Sebastijan Mrak  @aldebaran1: mapping projection", and by the pinned clone's single
non-Hirsch commit, authored by `aldebaran1 <smrak@bu.edu>`. His authorship is also visible in the
source: `src/dascasi/projection.py` and `src/dascasi/utils.py` both open with the docstring
"Created on Fri Sep 28 11:43:24 2018 / @author: smrak". `projection.py` supplies
`interpolateCoordinate` and `interpSpeedUp`, the interpolation machinery behind the map projection.

**How Sebastijan Mrak's ORCID was established.** The evidence for the identity is strong and
specific, not merely a name match: the ORCID expanded-search endpoint,
`https://pub.orcid.org/v3.0/expanded-search/`, returns exactly one record for given name
"Sebastijan" and family name "Mrak", and that record lists `smrak@bu.edu` among its emails — the
exact address on the single non-Hirsch commit in this repository. Its employment history includes
Boston University (department "ECE", role "PhD student", from 2016-09-01), which brackets the
2018-09-28 date in the contributed files' own docstrings, and later Boston University Center for
Space Physics, University of Colorado Boulder, and Johns Hopkins University Applied Physics
Laboratory.

**Why the identifier could not be applied as ordinary software metadata.** HSSI held no ORCID for
this author before this refresh, and that gap could not be closed by editing this software's author
list. Supplying an identifier for an author whose stored person record carries none does not annotate
that record — it creates a second person record and leaves the original orphaned and still attached
to the software. The identifier was therefore deliberately kept out of this software's metadata
update, and the correction was directed at the person record itself. The limitation is durable and
general: an identifier-less person record is repaired at the person record, never by adding the
identifier to a software entry that references it. A person record can also be shared with other
software, which is a second reason such a change does not belong in one software entry's update.

**The correction was applied on 2026-08-30, and the divergence recorded here is closed.** The ORCID
was written to Sebastijan Mrak's existing person record, which kept its identity and its Boston
University affiliation, so no duplicate record was created for this author and none was left
orphaned. The identifier accordingly appears in the value line above, and nothing about this author
remains to be reconciled.

**Boston University is recorded as Sebastijan Mrak's affiliation.** The record carried no affiliation
for this author before this refresh. An affiliation, unlike an identifier, can be attached to an
existing identifier-less person record without minting a duplicate, because the author is matched by
name when no identifier is sent. That asymmetry is why the affiliation could be carried by this
software's metadata update at a point when the ORCID could not, and it is worth remembering: for an
author whose person record has no identifier, affiliations are safe to add from a software entry and
identifiers are not. The evidence is his `smrak@bu.edu` commit address in this repository together
with the ORCID employment recorded above: Boston University, department "ECE", from 2016-09-01,
which brackets the 2018 dates in the files he contributed. The organization is the same Boston
University row, ROR `https://ror.org/05qwgg493`, already carried by Michael Hirsch's affiliation.

**"Samuel" is a misattribution and must not be added as a third author.** Zenodo's creator list for
this software — from the deposit record at `https://zenodo.org/api/records/19229352`, the source of
every Zenodo API claim in this dossier — reads `["scivision", "Samuel", "Sebastijan Mrak"]`, and
DataCite mirrors it verbatim,
with `nameType: "Personal"` and no name identifiers. Zenodo derives that list from GitHub's
contributors API, which credits the account `sam8979` (display name "Samuel") with 10 contributions.
Those 10 commits are Michael Hirsch's. GitHub's commit API returns them with commit-author fields
reading `scienceopen <nobody@github.com>` and `Michael H <nobody@github.com>` — Hirsch's own
identities under the generic placeholder address `nobody@github.com`, which the `sam8979` account has
since claimed. In the pinned clone, `git log --all` finds exactly ten commits with that address, all
authored under Hirsch's names, dated 2016-06-26 to 2016-08-04, with subjects including "FTP download
DASC FITS in time range", "improve reading of corrupt FITS files, use non-visible plots for
robustness of output", and "suppress flood of VerifyWarning Astropy messages for corrupt FITS" — core
Hirsch work on this package. No author resembling "Samuel" appears anywhere in the repository's
history or in `contributors.md`. Packaging metadata is silent rather than corroborating, and the
distinction matters: `pyproject.toml` at the pinned revision declares no `authors` field at all, and
PyPI reports a null `author` for `dascasi` 3.0.0, so only the retired `dascutils` distribution names
anyone ("Michael Hirsch, Ph.D."). That silence is not evidence against a third author — the repository
history and `contributors.md` are what carry the case. Field 6 correctly holds two authors.

The same Zenodo creator list also explains why `scivision` must not be recorded as an author name:
it is Hirsch's GitHub login, not a person's name, and DataCite has parsed it as a family name.

### 7. Software Name (MANDATORY)
**Value:** DASCutils

**Alternate names in circulation:** `dascasi` (the Python package, the PyPI distribution since
v3.0.0, and the GitHub repository name), `dascutils` (the PyPI distribution through v2.3.0),
`space-physics/dascasi` (the repository path).

**Source:** Carried over from the existing HSSI record; matches the PyHC registry entry, which reads
`name: DASCutils` with `code: https://github.com/space-physics/dascasi`.

**Why DASCutils is right even though the package is now `dascasi`.** The project renamed its
internals in 2023 ("pyproject only, rename internals dascasi") and its PyPI distribution at v3.0.0:
the JSON API shows `dascasi` with a single release, 3.0.0, uploaded 2026-03-26, alongside the
predecessor distribution `dascutils` with 13 releases from 1.2.1 (2018-05-23) to 2.3.0 (2022-04-06).
The PyHC registry entry, however, pairs `code: https://github.com/space-physics/dascasi` with
`name: DASCutils`, so the community registry catalogues the project under the older name while
pointing at the renamed repository, and HSSI's name matches that catalogued name. Changing HSSI's
name to `dascasi` would break that correspondence and orphan the historical distribution name that
1.2.1–2.3.0 users know. The alternate names above are recorded so a search for either form has a
path back to this record.

### 8. Description (MANDATORY)
**Value:** Digital All Sky Camera utilities for the University of Alaska Geophysical Institute cameras. This software provides utilities for plotting, saving, and analyzing data from the Poker Flat Research Range Digital All Sky Camera and other locations. It reads FITS format all-sky camera images, performs spatial calibration using azimuth/elevation plate scale data, supports map projection to specified altitudes for auroral and airglow analysis, converts FITS image stacks to HDF5 format with lossless compression, and creates visualizations including movies and projected images. The software handles corrupted FITS files from the 2013 RAID array failure and supports multi-wavelength image analysis for scientific studies of aurora and airglow phenomena.

**Source:** Reproduced byte-for-byte from the existing HSSI record.

**Retained unchanged, and checked for factual drift against the pinned source.** Every claim in it
holds at revision `18a3b4b0`: the FITS reading is `astropy.io.fits` in `dio.py`; the plate-scale
calibration is `loadcal`/`_azel`; the map projection to a specified altitude is `_project` driven by
`wavelength_altitude_km`; the HDF5 conversion is `save_hdf5`, and its compression is genuinely
lossless (`compression="gzip", compression_opts=1, shuffle=True, fletcher32=True`); the RAID
workaround is the clip-and-zero logic in `_loadimg`, whose docstring names the failure; and
multi-wavelength handling runs through the `wavelengths` key and the 428/558/630 nm channels. The
upstream one-line descriptions (GitHub's and Zenodo's "Digital All Sky Camera utilities, for U.
Alaska Geophysical Institute cameras", PyHC's "Digital All Sky Camera utilities, for camera at Poker
Flat Research Range and elsewhere", and `pyproject.toml`'s "UAF Digital All-Sky Camera: reading and
plotting") are all shorter and less informative than the stored text; none of them is a reason to
replace it.

### 9. Concise Description (OPTIONAL)
**Value:** Digital All Sky Camera utilities for U. Alaska Geophysical Institute cameras, supporting image reading, calibration, projection, format conversion, and visualization.

**Source:** Reproduced byte-for-byte from the existing HSSI record.

**Retained unchanged.** It fits the field's preview role, it is accurate against the pinned source,
and its wording deliberately echoes the upstream GitHub/Zenodo one-liner while naming the five
capabilities. Rewording it would be a stylistic preference, not a correction.

### 10. Publication Date (RECOMMENDED)
**Value:** 2016-02-03

**Source:** Carried over from the existing HSSI record; confirmed twice over. The GitHub API reports
`created_at: 2016-02-03T17:10:31Z` for `space-physics/dascasi`, and the first commit in the pinned
clone, `adc6a644dc48359d9076d6678fb399fd69e801c0` "Initial commit", is dated `2016-02-03 12:10:31
-0500` — the same instant expressed in local time.

**Why this date rather than a Zenodo date.** Zenodo's `publication_date` for this software is
2026-03-26, because it tracks the most recent deposit; the concept DOI's DataCite record likewise
reports `publicationYear: 2026` and a single `Issued` date of 2026-03-26. Each individual version DOI
carries its own deposit date. None of those is the date the software was first made public. Field 10
is a software-level first-publication date, so the repository's creation is the right answer and the
Zenodo dates belong to Field 12.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** Carried over from the existing HSSI record; DataCite reports `publisher: "Zenodo"` for
both the concept DOI and the v3.0.0 version DOI.

**Note.** Zenodo is the publisher of the archived software deposits that give this record its DOIs.
It is not the developing institution — that is Michael Hirsch working through SciVision, Inc., with a
Boston University affiliation, and those belong to Field 6.

### 12. Version (RECOMMENDED)
- **Version Number:** v3.0.0
- **Version Date:** 2026-03-26
- **Version Description:** dascasi name, modernize
- **Version PID:** https://doi.org/10.5281/zenodo.19229352

**Source:** Carried over from the existing HSSI record; each sub-field independently confirmed.

- The version string matches git tag `v3.0.0` (pointing at `a0f874a1`), the Zenodo record's
  `version: "v3.0.0"`, and DataCite's `version: "v3.0.0"`. The package's own
  `src/dascasi/__init__.py` sets `__version__ = "3.0.0"` without the leading `v`; the stored value
  follows the tag and the DOI record, which are the citable forms, and this discrepancy is a normal
  Python packaging convention rather than a conflict to resolve.
- The date matches the GitHub release (`published_at: 2026-03-26T04:31:02Z`), the PyPI upload of
  `dascasi` 3.0.0 (2026-03-26T04:31:32), the Zenodo `publication_date`, and the pinned HEAD commit
  date.
- The description reproduces the GitHub release name, "dascasi name, modernize", which Zenodo also
  used in its deposit title "space-physics/dascasi: dascasi name, modernize". The GitHub release body
  is empty and `v3.0.0` is a lightweight tag carrying no annotation message, so the release name is
  the only human-written description of the release.
- The version PID is the version-specific Zenodo DOI. Its DataCite record carries
  `IsVersionOf: 10.5281/zenodo.595465`, confirming the concept/version pairing recorded in Field 2.

**Note on what "v3.0.0" changed.** Reading the six 2026 commits, the release is a packaging and
tooling modernization — `use importlib.resources`, `pre-commit`, `ruff format`, `test: catch
ConnectionRefusedError too` — completing the `dascutils` → `dascasi` rename that began with the
2023-03-20 commit "pyproject only, rename internals dascasi". No scientific behaviour changed. This
matters for a later refresh: a large version-number jump here does not imply a change in
functionality, region, or format support.

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** Carried over from the existing HSSI record; confirmed present in the live
`ProgrammingLanguage` vocabulary.

**Evidence:** `pyproject.toml` sets `requires-python = ">=3.11"` and classifies
`Programming Language :: Python :: 3`; `.github/workflows/ci.yml` builds a single Python `3.11`
matrix entry across three operating systems; the entire `src/dascasi/` tree is Python, using
3.10-and-later syntax (`X | None` annotations, `match`/`case` in `utils.py::getDASCimage`).

**Why nothing else is listed.** GitHub's language breakdown for the repository reports Python 44222
bytes, Jupyter Notebook 2038 bytes, and Shell 496 bytes. The notebook bytes are the single example
`Notebooks/Azimuth Elevation Plot.ipynb`, whose code cells are Python calls into this package; the
shell bytes are `reference/downloadDASC.sh`, a deprecated `wget` helper whose own first comment says
"use DownloadDASC.py instead of this script." and whose 496-byte size accounts for GitHub's Shell
count exactly. Neither is an implementation language of the software,
and neither has a row in the vocabulary in any case. `Python 2.x` was rejected outright: the
`requires-python` floor and the 3.10+ syntax make Python 2 impossible.

### 14. Reference Publication (OPTIONAL)
**Value:** Not found

**Source:** Evidenced absence. This is negative research, not an unattempted lookup.

- No CITATION.cff exists at any revision in the pinned clone, so there is no `preferred-citation`
  block. The one-line `CITATION` file holds a Zenodo *software* DOI, not a paper.
- DataCite's `relatedIdentifiers` for both the concept DOI and the v3.0.0 version DOI contain only
  `IsSupplementTo` the GitHub tree at `https://github.com/space-physics/dascasi/tree/v3.0.0` plus
  `HasVersion`/`IsVersionOf` links among the Zenodo siblings. There is no `IsDescribedBy`,
  `IsSupplementedBy`, or `IsCitedBy` relation to any journal DOI.
- ADS full-text search returns zero documents for `full:"dascasi"` and one for `full:"DASCutils"`,
  and that one document is a user paper rather than a software paper (see Field 27). Every ADS result
  cited in this dossier comes from `https://api.adsabs.harvard.edu/v1/search/query`, reached with an
  anonymous token from `https://scixplorer.org/v1/accounts/bootstrap`; no personal API key is needed
  to reproduce them.
- There is no `paper/` directory, no JOSS badge, and no manuscript source anywhere in the tracked
  tree.

DASCutils has code DOIs and no describing publication. A future agent should not expect one to
surface without an explicit announcement from the maintainer.

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** https://spdx.org/licenses/Apache-2.0

**Source:** Re-derived from the repository, then matched to the live `License` vocabulary. HSSI held
no license value for this record before this refresh, so this is a newly filled gap rather than a
change.

**Evidence, in order of authority.**
- `LICENSE.txt` in the pinned tree is the full 176-line Apache License text, opening
  "Apache License / Version 2.0, January 2004 / http://www.apache.org/licenses/".
- `src/dascasi/__init__.py` opens with "Copyright 2023 SciVision, Inc." followed by the standard
  Apache 2.0 boilerplate paragraph.
- The GitHub API reports `license.spdx_id: "Apache-2.0"`, `license.name: "Apache License 2.0"`.
- Zenodo records `license: {"id": "apache2.0"}` and DataCite's `rightsList` gives
  `rightsIdentifier: "apache-2.0"`, `rightsIdentifierScheme: "SPDX"`.

**On the value written here.** `Apache License 2.0` is copied verbatim from the live vocabulary row,
which is what the backend matches on. The URI recorded is that row's own SPDX URL,
`https://spdx.org/licenses/Apache-2.0`. The repository's own pointer is the Apache Foundation URL
`http://www.apache.org/licenses/LICENSE-2.0` (as it appears in `__init__.py` and, over `https`, in a
prior extraction of this record) — both identify the same license, and the SPDX form is preferred
here because it is what HSSI stores for the row. DataCite's `rightsUri` is the same Apache Foundation
URL. Recording the SPDX URI is not a rejection of the Apache URL; it is a choice to match the
catalogue's canonical form.

The license was re-derived from the repository rather than taken from DOI autofill on purpose: Zenodo
metadata for this project has demonstrably propagated upstream errors into other fields (its creator
list is GitHub-handle-derived, as Field 6 documents), so its license claim is treated as
corroboration rather than as the source.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values (as stored, lowercase):**
- airglow
- all-sky-camera
- atmospheric science
- aurora
- calibration
- camera
- fits
- image processing
- ionosphere
- mesosphere
- thermosphere

**Source:** Carried over from the existing HSSI record. Each of the eleven was confirmed to exist as
a row in the live `Keyword` vocabulary in exactly this lowercase form, with no title-cased duplicate
row for any of them.

**Do not "fix" the casing.** The stored rows are lowercase; HSSI's view rendering title-cases
keywords for display (so a reader sees "Airglow", "All-Sky-Camera", "Fits"). Copying a rendered
title-cased string back into a patch would either fail to match or create a duplicate row. The value
list above is the stored form.

**Reconciliation of every upstream keyword source — nothing is dropped and nothing is missing.**
- GitHub topics for the repository are `all-sky-camera`, `aurora`, `camera` — all three already
  stored.
- `pyproject.toml` declares `keywords = ["aurora", "camera"]` — both stored.
- PyPI reports `aurora, camera` for `dascasi` and `aurora,scientific camera` for the retired
  `dascutils` distribution; "scientific camera" adds nothing over `camera`.
- The PyHC registry entry lists `["ionosphere_thermosphere_mesosphere", "specific"]`. The compound
  first tag is already covered by the three separate stored keywords `ionosphere`, `thermosphere`,
  `mesosphere`. The second tag, `specific`, is a PyHC taxonomy marker denoting a narrow-scope
  project, not a science keyword, and is deliberately not carried across.
- `airglow`, `calibration` and `fits` come from the README's own vocabulary, where each appears
  literally. `atmospheric science` comes from `pyproject.toml`'s
  `Topic :: Scientific/Engineering :: Atmospheric Science` classifier. `image processing` comes from
  none of those — the string appears in neither the README nor `pyproject.toml` — but from the
  software's actual behaviour: the DASC pixel handling and geographic re-gridding recorded under
  Field 4. It is a correct descriptive keyword and is kept; it simply has no upstream keyword list
  behind it. All five remain accurate at the pinned revision.

**Nothing is added to the stored set.** `Keyword` is HSSI's only open vocabulary, so any string can
be added and a
row minted for it. Candidates such as "Poker Flat", "all-sky imager", "HDF5" or "optical" were
considered and rejected: the first two are better served by Fields 31/32, the third by Field 19, and
none of them appears as a keyword in any upstream source. Minting rows adds catalogue noise without
improving discovery here.

### 17. Data Sources (OPTIONAL)
**Values:**
- FTP/FTPS Directories
- Observatory/Mission-specific

**Source:** Carried over from the existing HSSI record; both confirmed present in the live
`DataInput` vocabulary.

**Evidence.** `src/dascasi/web.py` builds its client on Python's standard `ftplib`
(`with ftplib.FTP(ftop, "anonymous", "guest", timeout=15) as F:`) against
`HOST = "ftp://optics.gi.alaska.edu"`, walks `<site>/DASC/RAW/<year>/<yyyymmdd>/`, and retrieves
files with `F.retrbinary`. The archive is the University of Alaska Fairbanks Geophysical Institute's
own optical data server, and `src/dascasi/download.py` restricts retrieval to six UAF-GI site codes
(`choices=["EAA", "FYU", "KAK", "PKR", "TOO", "VEE"]`), which is what makes the source
observatory-specific rather than a general archive. Per the Field 17 guidance, selecting
`Observatory/Mission-specific` pairs with naming the observatory in Field 32, which records the
Poker Flat Geophysical Observatory row and the reasoning behind that choice.

**`HTTP/HTTPS Directories` is explicitly rejected.** There is no HTTP or HTTPS retrieval path in the
pinned source. `web.py` is the only download implementation and it is FTP-only; the sole remaining
HTTP-adjacent artifact, `reference/downloadDASC.sh`, is a `wget` script that also targets
`ftp://optics.gi.alaska.edu/...` and is marked deprecated in its own first comment. The README points
at data exactly once, and that link — `ftp://optics.gi.alaska.edu/Cal_data/`, at README line 96 — is
FTP. Its three `http://` URLs carry no data: a PyPI download-stats badge and its target (line 5) and
an xarray documentation page (line 39). Re-add only if a genuine HTTP client appears.

**Also considered and rejected:** `CDAWeb`, `HAPI`, `Madrigal`, `S3/Cloud-aware`, `SSCWeb`, `AMDA`,
`OMNIWeb`, `das2`, `GFZ`, `TAP`, `VirES`, `WDC`, `The Virtual Solar Observatory.` and `Other`. A
word-boundary search of the pinned tree for the thirteen service and protocol names in their full
vocabulary form — `S3/Cloud-aware` and `The Virtual Solar Observatory.` included — returns no match
at all, in no tracked file, text or binary. The full form matters: a shortened fragment matches
unrelated text — `das` sits inside every `dasc` in this repository — so a search on fragments says
nothing about whether a service is referenced.

Two tokens do produce stray hits against the binary test data, by two different routes, and both are
recorded so a future agent recognises them rather than re-investigating. `S3`, shortened from
`S3/Cloud-aware`, occurs case-sensitively inside the two `.FIT` calibration files and all three
example PNGs, and in none of the four `.FITS` image files; some of the PNG occurrences are flanked by
non-word bytes, so a case-sensitive word-boundary search for that bare fragment finds it there too —
and only there, since no case-sensitive `.FIT` occurrence clears the word-boundary test. `TAP` is
the opposite case: it is a full vocabulary name rather than a shortening, and it matches nothing
until the search mode is relaxed. A case-sensitive substring search finds it nowhere, and no
word-boundary search finds it in either case; only a case-insensitive substring search matches,
returning exactly one occurrence, the bytes `TAp`, inside `dasc_projection_plot.png`. Both tokens
fall inside binary array or image payload rather than in any reference to cloud storage or to a TAP
service, so every one of these hits is incidental to the question of whether a data-source service
is referenced.

`Other`, the fourteenth rejected value, is deliberately excluded from that search: it is an ordinary
English word, and it does occur in the tracked tree — README line 7 reads "(Other locations, too)",
which is prose about camera sites rather than a data source. It is rejected on the substantive
ground instead: the two stored values together describe the retrieval path completely, leaving
nothing for `Other` to cover.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- FITS
- HDF5

**Source:** Carried over from the existing HSSI record; both confirmed present in the live
`FileFormat` vocabulary.

**Evidence.** `src/dascasi/dio.py` reads images with `astropy.io.fits.open` and globs both `*.FITS`
and `*.fits`; the plate-scale calibration files it reads via `loadcal` are `_Az.FIT`/`_El.FIT`, the
same format under a truncated extension. `dio.py::load` dispatches on suffix — `if fin.is_file() and
fin.suffix in (".h5", ".hdf5"): return load_hdf5(fin, treq, wavelenreq)` — and
`src/dascasi/hdf5.py::load_hdf5` reads previously converted stacks with `h5py`. The round trip is
exercised by `src/dascasi/tests/test_mod.py::test_read_write_hdf5`.

**Rejected:** `Other`. Nothing else is read. The `.mp4`/`.png` artifacts that appear in adjacent
discussions of DASC data are outputs or third-party derivatives, not inputs.

### 19. Output File Formats (RECOMMENDED)
**Values:**
- HDF5
- Other

**Source:** Carried over from the existing HSSI record; both confirmed present in the live
`FileFormat` vocabulary.

**Evidence.** `src/dascasi/hdf5.py::save_hdf5` writes an HDF5 file with per-wavelength datasets under
`/<wavelength>/imgs`, gzip compression with shuffle and Fletcher-32 checksums, and HDF5 image
attributes (`CLASS=IMAGE`, `IMAGE_VERSION=1.2`, `IMAGE_SUBCLASS=IMAGE_GRAYSCALE`,
`DISPLAY_ORIGIN=LL`) that make the file readable as an image stack by generic HDF5 tooling.

`Other` covers PNG, which has no row in the `FileFormat` vocabulary. PNG output is real and
user-facing: `plots.py::histogram_dasc` writes `DASChistogram.png` to a caller-supplied directory,
and `plots.py::moviedasc` writes one `<timestamp>.png` per frame with
`fg.savefig(ofn, bbox_inches="tight", facecolor="k")` when an output directory is given. Recording
`Other` rather than omitting it preserves the fact that the movie workflow produces files on disk.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

**Source:** Carried over from the existing HSSI record; all three confirmed present in the live
`OperatingSystem` vocabulary.

**Evidence.** `.github/workflows/ci.yml` runs the full install-and-test job
(`pip install .[tests]`, `mypy`, `pytest`) on a matrix of `[windows-latest, macos-latest,
ubuntu-latest]`. That is direct evidence of successful installation on each, which is what the field
asks for. `dio.py` carries a Windows-specific branch (`if os.name != "nt"` guards the lower-case
`*.fits` glob, avoiding duplicate matches on case-insensitive filesystems), showing Windows support
is maintained deliberately rather than incidentally.

**`Operating System Independent` was considered and not selected.** `pyproject.toml` does carry the
classifier `Operating System :: OS Independent`, and the vocabulary does have a matching row. The
classifier is the packager's assertion; the CI matrix is the evidence. Enumerating the three tested
platforms is both better supported and more useful to a user filtering HSSI by operating system,
since the independent value would not surface the record for a "Windows" filter. `Solaris`,
`MobilePlatform` and `Other` are rejected — nothing tests or claims them.

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- CPU Independent

**Source:** Carried over from the existing HSSI record; confirmed present in the live
`CpuArchitecture` vocabulary.

**Evidence.** The package is pure Python: the pinned tree contains no C, Cython, Fortran or Rust
sources, no compiled extension modules, and no build backend beyond `setuptools`/`wheel`. PyPI's
single `dascasi` 3.0.0 release is a platform-independent distribution. The claim rests on the
package itself rather than on its dependency tree: `pymap3d` is likewise pure Python, while `numpy`,
`scipy` and `h5py` carry compiled cores whose architecture coverage is their own maintainers' concern
and is not asserted here.

**Rejected:** `Apple Silicon arm64`, `x86-64`, `Linux aarch64 or arm64` and the other specific rows
would each understate portability by implying the others are unsupported; `GPU` and `HPC or HEC` are
false — there is no CUDA, MPI, or job-scheduler code in the tree.

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found — the phenomena this software addresses have no row in the vocabulary.

**Source:** Carried over from the existing HSSI record (the field was empty before this refresh) and
re-confirmed against the live `Phenomena` vocabulary.

**This is an evidenced-empty field, not an unexamined gap.** The complete vocabulary as read on
2026-08-29 is: Coronal Heating; Coronal Mass Ejections; Geomagnetic Storms; Solar Corona; Solar
Flares; Solar Wind; X-ray emission. Every row carries an empty `definition` and an empty
`identifier`, so the vocabulary itself defines none of them and each has to be read from its name
alone. Five of the seven — Coronal Heating, Coronal Mass Ejections, Solar Corona, Solar Flares and
Solar Wind — name a solar feature explicitly. `Geomagnetic Storms` is terrestrial and is rejected on
its own grounds below. `X-ray emission` is unqualified: the row says nothing about whether it denotes
solar X-rays, auroral X-ray bremsstrahlung from precipitating electrons, or something else, so it
must not be read as implicitly solar. It is rejected for a reason that holds under any of those
readings — DASCutils handles the 428, 558 and 630 nm optical channels, and a case-insensitive search
of the pinned tree for "x-ray" and "xray" returns nothing. The phenomena
DASCutils actually addresses — **aurora** and **airglow**, named in the README ("A common task in
auroral and airglow analysis"), in `pyproject.toml`'s `keywords`, and in the GitHub topics — have no
row. Enumerating the vocabulary here *is* the reason the field is correctly empty, and it saves a
future agent the lookup.

**`Geomagnetic Storms` is explicitly rejected.** It is the tempting near-miss, being the one row that
plainly names a terrestrial phenomenon, but aurora is not a geomagnetic storm: auroral displays occur
routinely under
quiet and substorm conditions, and DASCutils computes no geomagnetic index, ingests no magnetometer
data, and has no storm-selection functionality. Selecting it would make the record surface for storm
queries it cannot serve.

**When to revisit:** if `Aurora`, `Airglow`, `Auroral Precipitation` or a similar row is added to the
`Phenomena` vocabulary, this field should be filled immediately — the evidence for it already exists
and is recorded above.

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** Derived from the pinned repository's own activity and confirmed present in the live
`RepoStatus` vocabulary. HSSI held no development-status value for this record before this refresh,
so this is a newly filled gap.

**Evidence.**
- Release `v3.0.0` was published 2026-03-26, five months before this extraction, with a matching PyPI
  upload the same day and a matching Zenodo deposit.
- Six commits in March 2026 modernize the project: `use importlib.resources`, `pre-commit`,
  `pre-commit don't edit data files`, `test: catch ConnectionRefusedError too`, `ruff format`, and
  the pinned HEAD's `case insensitive exclude`.
- The toolchain is current at the pinned revision: `.github/workflows/ci.yml` uses
  `actions/checkout@v6` and `actions/setup-python@v6`; `.pre-commit-config.yaml` pins
  `pre-commit-hooks` v6.0.0, `ruff-pre-commit` v0.15.5, and `mirrors-mypy` v1.19.1.
- The GitHub repository is not archived and not disabled, and `pyproject.toml` classifies the project
  `Development Status :: 5 - Production/Stable`.

**Alternatives considered and rejected.**
- **`Inactive`** — the honest counter-argument, because commit activity between 2023-03-20 and
  2026-03-25 was a single commit and the repository was effectively dormant for three years. It is
  rejected because that dormancy *ended*: the current state, as of the pinned revision, is a freshly
  released and freshly re-tooled project. A future refresh should re-examine this if another
  multi-year gap opens without a release.
- **`Unsupported` / `Abandoned`** — the repository is not archived, carries no deprecation notice,
  and shipped a release in 2026.
- **`Moved`** — tempting because both the distribution name (`dascutils` → `dascasi`) and, earlier,
  the repository path changed. But the project did not move to a different home; it renamed in place,
  and `github.com/space-physics/dascutils` redirects to the current repository rather than pointing
  elsewhere. `Moved` would signal to users that development continues somewhere else, which is false.
- **`WIP`** — contradicted by the Production/Stable classifier and a tagged, published, PyPI-released
  version.
- **`Concept` / `Suspended`** — neither describes a decade-old package with sixteen tags and a
  current release.

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/space-physics/dascasi

**Source:** Carried over from the existing HSSI record; the absence of any alternative was verified
against the pinned tree and the GitHub API.

**Why the repository URL is the right value here.** The README is the documentation. It covers
installation (`git clone` plus `pip install -e`), the direct API (`du.load`, `du.save_hdf5`), the
`python -m dascasi.download` and `python -m dascasi.movie` command lines with their flags, spatial
registration with plate-scale calibration files including the caveats about camera moves and
magnetic-versus-geographic north, and map projection to per-wavelength altitudes. It embeds two
example figures rendered from the repository's own test data.

**No separate documentation site exists.** The pinned tree contains no `docs/` directory, no
`.readthedocs.yaml`/`.readthedocs.yml`, no Sphinx or MkDocs configuration, and no documentation
badge — the three README badges point at Zenodo, the CI workflow, and PyPI download statistics. The
GitHub API reports an empty `homepage` field. Supplementary usage examples live in `scripts/` — five
Python example scripts — and in `Notebooks/Azimuth Elevation Plot.ipynb`, all inside the repository
this URL already points at. Two of the five carry documented caveats a reader should know about.
`dasc_hist.py` cannot run as committed at all: it calls `plothstfovondasc` with six arguments against
a five-parameter definition (see Field 29 for which call site raises what). `PlotImageAzEl.py`
hard-codes `data_file = Path("~/data/dasc/PKR_DASC_0428_20151027_122319.645.FITS")` at line 21, a path
that is not in the repository, so on a clean checkout it fails on a missing input rather than on a
code defect; the commented `dascasi_download.exe` invocation just above it is the intended way to
obtain that file. The other three carry neither defect: `PlotAzimuthElevation.py` and
`PlotProjectedImage.py` resolve their inputs from the packaged test data under
`src/dascasi/tests/data/`, and `ConvertDASC_FITS_to_HDF5.py` is argparse-driven and takes the user's
own input and output paths. Field 24's own instruction — "If this is
the same as the access URL, then enter that link here" — is exactly this case.

### 25. Funder (OPTIONAL)
**Value:** Not found

**Source:** Evidenced absence. This is negative research, not an unattempted lookup.

- DataCite's `fundingReferences` array is **empty** for both the concept DOI `10.5281/zenodo.595465`
  and the v3.0.0 version DOI `10.5281/zenodo.19229352`.
- A `git grep` across every tracked file at the pinned revision for `fund`, `grant`, `NSF`, `NASA`,
  `award`, `sponsor` and `acknowledg` returns no funding statement. The only hits are incidental
  substrings — `skimage.transform` in `dio.py` and `tri.transform` in `projection.py`, each caught by
  the case-insensitive `NSF` pattern matching the letters n-s-f inside the word "tra**nsf**orm", plus
  a binary match inside an example PNG. `LICENSE.txt` was excluded from that sweep as boilerplate.
- The repository has no CITATION.cff, no codemeta.json, and no `.zenodo.json` — the three files that
  would ordinarily carry structured funding metadata — at the pinned revision or at any revision in
  its history.
- The only copyright attribution in the source, `src/dascasi/__init__.py`'s "Copyright 2023
  SciVision, Inc.", names Michael Hirsch's own company, not a sponsor.

**The one paper that acknowledges DASCutils does not supply a funder for it, and its awards must not
be read as evidence here.** Ozturk et al. (2020), recorded in Field 27, acknowledges support through
a NASA contract with the Jet Propulsion Laboratory, NSF award AGS-1821135 to J. L. Semeter, and NSF
award AGS-1840962 to SRI International for the Poker Flat Incoherent Scatter Radar. Every one of
those supports the *paper's* authors and instrumentation — a study of mesoscale electrodynamics using
PFISR and GITM — and none of them is attached to DASCutils, whose acknowledgement in that paper is a
bare thank-you to the library's developers with no funding statement. Per the Field 25/26 guidance,
funding tiers must not be conflated: an award that supported a study which used this software did not
fund this software. Recording any of those three here would be wrong, and a future agent encountering
them should not do it. The named awards are written out above precisely so that finding them again in
Crossref or in the article text is not mistaken for a new discovery.

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Source:** Evidenced absence, on the same research as Field 25 — no award title or number appears in
DataCite's funding block, in any tracked repository file, or in any packaging or archival metadata
for this software. With no funder established, there is no award to attach.

The three award identifiers recorded under Field 25 (a NASA/JPL contract, NSF AGS-1821135, NSF
AGS-1840962) belong to Ozturk et al. (2020) and to the PFISR facility, not to DASCutils. They are
listed there as a rejected inference, not as candidates for this field.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** https://doi.org/10.1029/2019JA027562

**Why this publication is recorded.** HSSI held no related publications for this record before this
refresh. Across the searches enumerated under "Negative research" below, one publication was found
that credits DASCutils, and its acknowledgement states outright that the library "was used in this
study" — verified use rather than an incidental mention.

**The counter-argument, weighed and rejected.** The field's definition scopes it to publications
"the software developer prioritizes", and no signal of this maintainer's preference exists: the
repository carries no publication list, and the paper credits the developers without citing a code
DOI. That silence was judged too weak a reason to suppress a documented use. With no maintainer
signal either way, a reader of this record is better served by the one paper known to have used the
software than by an empty field.

**The publication:** https://doi.org/10.1029/2019JA027562

> Ozturk, D. S., Meng, X., Verkhoglyadova, O. P., Varney, R. H., Reimer, A. S., & Semeter, J. L.
> (2020). A New Framework to Incorporate High-Latitude Input for Mesoscale Electrodynamics.
> *Journal of Geophysical Research: Space Physics*, 125. ADS bibcode `2020JGRA..12527562O`.

**What the acknowledgement says, verbatim.** From the Acknowledgements section of
<https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2019JA027562>:

> "We thank the developers of Spacepy (https://pypi.org/project/spacepy/), AACGMV2
> (https://pypi.org/project/aacgmv2/), and Dascutils (https://pypi.org/project/dascutils/)
> libraries, which were used in this study."

This is an explicit statement of use, not a passing mention, which is what makes the paper a
defensible Field 27 entry rather than a coincidence of vocabulary. Two details in it are worth
keeping. The paper names the software **`Dascutils`** and links the **`dascutils`** PyPI
distribution — the pre-v3.0.0 distribution name — which independently corroborates the rename
recorded in Field 7 and shows the software was in use under that name. And it credits the library's
*developers* without citing a code DOI, so it establishes use without establishing a preferred
citation.

**Why the credit sits in the acknowledgements rather than the methods.** ADS's acknowledgements index
matches this paper for `ack:"DASCutils"` while `body:"DASCutils"` returns zero, which locates the
credit precisely: the software is thanked as a tool used, and is not discussed as a method in the
main text. Probes against the same bibcode confirm the acknowledgements also mention "Poker Flat" and
"NSF" but not "Hirsch" and not "Zenodo", consistent with the verbatim text above. The author list
places the work at JPL, SRI International, and Boston University's Center for Space Physics — the
last being the institution of DASCutils' own two authors — and the study uses Poker Flat
instrumentation.

**A third-party tie between the DASC data host and Donald Hampton.** The same acknowledgement thanks
"Mark Conde and Don Hampton for the SDI data ... and ASI data (at http://optics.gi.alaska.edu/optics/)".
That is independent, non-repository evidence that the all-sky-imager data served from
`optics.gi.alaska.edu` — the host `src/dascasi/web.py` downloads from — is associated with Don
Hampton at UAF-GI. It is part of the evidence behind the observatory recorded in Field 32 and is
cited there.

**On reading the article.** The publisher's page is marked Free Access and renders normally in a
browser; a plain HTTP client is turned away by a Cloudflare interstitial, as is the author-manuscript
copy at `https://rss.onlinelibrary.wiley.com/doi/am-pdf/10.1029/2019ja027562`, and Europe PMC holds
no record for this DOI. The barrier is bot-gating, not entitlement — worth knowing if the text ever
needs re-checking, but the wording itself is recorded above and does not need recovering again.

**Negative research on other publications — do not re-run these searches without new information.**
ADS full-text search
returns zero documents for `full:"dascasi"`, `full:"space-physics/dascasi"`,
`full:"space-physics/dascutils"`, `full:"zenodo.595465"`, and `ack:"dascasi"`; `full:"dascutils"`
returns only the paper above. The searches were validated with controls: a nonsense token returns
zero, and `full:"themisasi"` — the sibling package recorded in Fields 29 and 30 — returns 46
documents, proving the index reaches this literature and that the DASCutils result is a real scarcity
rather than a tokenization artifact. DataCite reports `citationCount: 0` for the v3.0.0 version DOI.

**Nothing in this paper bears on Fields 25 and 26.** Its acknowledgement of DASCutils carries no
funding statement for the software; the awards it does acknowledge fund the paper's authors and the
PFISR facility, and are recorded as a rejected inference under Field 25. Fields 25 and 26 remain
evidenced-empty.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Source:** Evidenced absence with two specifically rejected candidates.

**The data this software reads has no persistent identifier.** DASCutils operates on the DASC raw
FITS archive at `ftp://optics.gi.alaska.edu/<site>/DASC/RAW/<year>/<yyyymmdd>/` — an anonymous FTP
tree. It has no DOI, and searches of the instrument/observatory vocabulary and of SPASE turned up no
data-product record for the DASC to cite as a permanent landing page. Field 28 requires a URL; there
is no permanent one to give.

**Rejected candidate 1 — https://doi.org/10.5281/zenodo.6878145 (concept 10.5281/zenodo.6878144),
"PFRR ASC Image Dataset for Troyer et al. 2022 (Substorm Activity as a Driver of Energetic Pulsating
Aurora)", Troyer, Jaynes, Jones, Kaeppler, Varney & Reimer, 2022-07-21.** This is the closest match
found: its own `related_identifiers` block declares
`isDerivedFrom: ftp://optics.gi.alaska.edu/PKR/DASC/RAW/`, the exact archive DASCutils downloads
from. It is rejected because the archived artifacts are compiled MP4 movies — the record's
description states "File names looking like 428-YYYY-MM-DD.mp4 are movies compiled from the 428 nm
images" — and DASCutils neither reads nor writes MP4. The software supports no functionality for the
deposited files, only for their unarchived source. Re-add only if the raw FITS themselves are
deposited under a DOI.

**Rejected candidate 2 — https://doi.org/10.5281/zenodo.8329371, stored title `Dataset for
"Data-driven empirical conductance relations during auroral precipitation using incoherent scatter
radar and all sky imagers" JGR-Space Physics`.** It surfaces on a DataCite full-text search for `optics.gi.alaska.edu`, but its files are
per-year Excel spreadsheets and a single HDF5 file of PFISR conductance inversions — derived analysis
products, not DASC imagery in any format DASCutils reads.

**Also searched and empty:** DataCite queries for UAF/Geophysical Institute all-sky camera datasets
returned only unrelated deposits (atmospheric heat emission, thermospheric weather).

### 29. Related Software (OPTIONAL)

**Value 1:** https://github.com/geospace-code/pymap3d

**Source:** Carried over from the existing HSSI record, and retained under the relevance gate on
specific evidence: `src/dascasi/dio.py::_project` calls `pm.aer2geodetic(azi, eli, slant_range, lat0,
lon0, alt0)` to perform the auroral altitude projection, which is the capability the README dedicates
its "Map Projection" section to and which `src/dascasi/tests/test_projection.py` verifies against
reference latitudes and longitudes. `pymap3d` is declared in `pyproject.toml`'s core `dependencies`.

**Why it passes the gate where the generic stack does not.** It is a domain-specific geodetic
library, from the `geospace-code` organization, whose presence characterizes what this software does:
without it there is no projection, and the projection is the scientific core of the package. It is
not part of the generic scientific-Python stack — a web app, a finance model, or a biology pipeline
would have no use for AER-to-geodetic conversion.

**Value 2:** https://github.com/space-physics/themisasi

**Source:** Carried over from the existing HSSI record, and retained on two independent grounds.

- *Distinguishing companion.* THEMIS ASI utilities are the sibling tool for the other major
  ground-based all-sky-imager network in Alaska ("Read & Plot THEMIS ASI 256x256 'high resolution'
  GBO ground-based imager data"). Knowing that DASCutils is the DASC analogue of themisasi, from the
  same `space-physics` organization, tells a reader something specific about DASCutils that is not
  true of most packages. This is Field 29's "performs similar tasks but does not necessarily link
  together" prong, and what it asks for is a same-task-shape relationship on different
  instrumentation, not a code reference — the same standard under which the Digital Meridian
  Spectrometer is recorded below. The concrete integration in the next bullet is additional evidence,
  not the basis of this prong.
- *Concrete integration.* `src/dascasi/plots.py` imports `themisasi.plots as themisplot` (line 19,
  guarded by `try/except ImportError`) and calls `themisplot.overlayrowcol(ax, rows, cols)` inside
  `moviedasc` at lines 187 and 204 — the executable half of the integration.
  `scripts/dasc_hist.py` imports `from themisasi.fov import mergefov` (line 12) and calls
  `mergefov(..., site="DASC")` (line 71) to merge a narrow field-of-view camera's FOV onto DASC
  frames; that script documents the *intended* integration rather than a working invocation, because
  it cannot run as committed (see the call-signature note below). `themisasi` is declared in
  `pyproject.toml`'s `full` extra. This same evidence also supports the Field 30 entry below.

  **`scripts/dasc_hist.py` does not execute as committed.** `plothstfovondasc` is defined with five
  parameters at line 15 and called with six arguments at both line 68 and line 73 — but the two calls
  fail differently, and the distinction matters to anyone tracing the script. The line-68 call sits
  inside a `try:` and evaluates the undefined name `img` while building its arguments, so it raises
  `NameError`, which is the caught control-flow path (`except NameError:` at line 69) and is
  evidently how the script was meant to fall through. It is the line-73 call, in the `except`
  handler, that actually reaches the six-against-five arity mismatch and raises `TypeError` before
  `moviedasc` is ever entered. The import and the `mergefov` call are real source-level
  evidence of the intended design, but they are not a demonstration that the combined workflow runs.
  Nothing about the themisasi relationship depends on this script alone — `plots.py` carries the
  working integration — and the defect is recorded so a future agent citing the script knows its
  limits, and so it is not mistaken for evidence that the integration is broken.

**themisasi is recorded in both Field 29 and Field 30, deliberately.** The two fields make
different claims and both are independently true: Field 29 says themisasi is the similar-purpose
sibling tool that helps a reader place DASCutils, and Field 30 says the two exchange concrete objects
in code. Dropping the Field 29 entry would lose the "similar tasks" signal that a user browsing
all-sky-imager software needs. The reading that would have removed it — the field definition's
phrasing, "does not necessarily link together (which would be 'interoperable software')" — was
considered and rejected: that phrasing describes what Field 29 tolerates, not what it excludes.

**Value 3:** https://github.com/space-physics/digital-meridian-spectrometer

**Source:** The two projects' own package and repository descriptions, their shared GitHub
organization and author, and the PyHC registry. The record carried no entry for the Digital Meridian
Spectrometer before this refresh.

**Why it passes the "performs similar tasks" prong.** `space-physics/digital-meridian-spectrometer`
declares `name = "dmsp"` and `description = "Load and plot UAF Geophysical Institute Digital Meridian
Spectrometer data"` in its `pyproject.toml`, and its GitHub repository description — from
`https://api.github.com/repos/space-physics/digital-meridian-spectrometer`, a second endpoint outside
the dascasi pin recorded under Field 3 — reads "for Poker Flat Digital Meridian Spectrometer, which
uses netCDF". That is the same task shape as DASCutils: a
load-and-plot reader that turns a UAF Geophysical Institute optical auroral instrument's native files
into arrays and figures. The instrument differs — a meridian spectrometer rather than an all-sky
camera — and that difference is what makes the entry informative rather than redundant, since a user
holding data from one of the two co-located Poker Flat instruments has a natural next tool for the
other. Both projects are by Michael Hirsch, in the same `space-physics` GitHub organization, under
the same Apache-2.0 licence. The PyHC registry file already cited in this dossier,
`_data/projects_unevaluated.yml`, carries them as adjacent entries — DASCutils immediately preceding
"Digital Meridian Spectrometer" — with identical `contact: Michael Hirsch` and an identical keyword
list `["ionosphere_thermosphere_mesosphere","specific"]`.

**The evidence is external to both repositories, and a future reader should not expect otherwise.**
Neither repository references the other: a case-insensitive search of the pinned dascasi tree for
"meridian", "dmsp" and "spectromet" returns nothing, and a search of the DMS repository's text files
on its default branch for "dasc" and "all sky" returns nothing either. There is no import, no
dependency declaration and no shared code path between the two, and none is claimed here. The
association rests instead on the two projects' own descriptions, the shared organization and author,
and the PyHC registry — public, checkable and durable sources, none of them inside a source tree.
That is what Field 29's "does not necessarily link together" prong is for; requiring a code reference
here while accepting themisasi partly on the same prong would apply two different bars to one
question, which is why the earlier rejection of this entry was reversed.

**https://github.com/astropy/astropy is not recorded; the record carried it until this refresh.**
Under the relevance gate astropy is a domain-adjacent foundational package that qualifies only on a
cited, specific exchange, and there is none. `src/dascasi/dio.py` uses `astropy.io.fits` purely
internally: `_loadimg` opens the file, immediately unwraps to NumPy with `h[0].data.squeeze()`, and
closes the context; `load()` returns `xarray.DataArray` objects. No astropy object crosses the public
API boundary, astropy appears nowhere in the README's API description, and no test asserts an astropy
type. What the record actually gains from astropy — the ability to read FITS — is already carried by
Field 18. **What would justify re-adding it:** a public API that accepts or returns astropy objects
(an `HDUList`, a `Quantity`, an `astropy.time.Time`), or documented astropy-based interchange.

**https://github.com/pydata/xarray is not recorded; the record carried it until this refresh.**
xarray is generic labeled-array infrastructure — equally at home in a finance model or a biology
pipeline — so under Field 29's exclusion of the generic stack it distinguishes nothing about
DASCutils. The same verdict follows from the searcher's side: someone browsing DASCutils' related
software and finding `xarray` learns nothing that sets this package apart, since any Python package
that returns labeled arrays could carry the same line, whereas `themisasi` and the Digital Meridian
Spectrometer send that person to a genuinely useful next tool. It was not dismissed out of hand,
because a real, documented exchange with xarray exists; that exchange was examined against Field 30's
narrower interoperability test instead, and the evidence and the reason it still did not earn an
entry there are set out under Field 30.

**Considered and not selected.**
- **https://github.com/space-physics/histutils** — a genuine near-miss. `scripts/dasc_hist.py`
  defaults its `--ncal` argument to `../histutils/cal/hst0cal.h5` and `../histutils/cal/hst1cal.h5`,
  and its docstring says the script "projects HiST auroral tomography system FOV onto PFRR DASC".
  Rejected because the pinned source never imports `histutils` and does not declare it in any
  dependency group; the two paths are the default value of a user-overridable `--ncal` argument and
  are passed straight through to `themisasi.fov.mergefov`, so nothing in this repository ties them to
  `histutils` beyond the directory name. The association is a default filesystem path, not a software
  relationship. **Re-add if** an actual import or a declared dependency appears.
- **Other `space-physics` instrument tools** beyond the two recorded above. Rejected for want of any
  relationship at all: no reference in the pinned tree, no shared task shape, and no registry pairing
  of the kind that supports the Digital Meridian Spectrometer entry. "Same author, same institution"
  on its own is not a software relationship.
- **numpy, scipy, matplotlib, cartopy, scikit-image, h5py, pytest, mypy, setuptools** — the generic
  scientific-Python and tooling stack, excluded by the gate regardless of how central they are to the
  implementation. Listing them would read identically for most packages in the catalogue. `h5py`
  deserves a specific note because it is domain-adjacent Tier B rather than plainly generic: it is
  rejected because the relationship DASCutils has is with the HDF5 *format*, already recorded in
  Fields 18 and 19, not with h5py as a peer tool.

**Note on display names.** The related-item rows this field has referenced carried display names
that merely repeat their own URLs, rather than human-readable labels. Those names are placeholders
carrying no information beyond the URL, and must not be used as evidence for or against including an
entry.

### 30. Interoperable Software (OPTIONAL)

**Value:** https://github.com/space-physics/themisasi

**Source:** Derived from the pinned source. HSSI held no interoperable-software entries for this
record before this refresh.

**The demonstrated exchange.** This is a code-level, bidirectional-in-effect integration, not a
dependency listing.

- `src/dascasi/plots.py` does `import themisasi.plots as themisplot` and, inside `moviedasc`, calls
  `themisplot.overlayrowcol(ax, rows, cols)` on the very matplotlib axes holding the DASC frame — so
  themisasi's overlay routine draws directly onto DASCutils' figure.
- `scripts/dasc_hist.py` does `from themisasi.fov import mergefov` (line 12) and calls
  `mergefov(ocalfn, None, None, p.ncal, p.projalt, site="DASC")` (line 71) — note the explicit
  `site="DASC"` argument, which is themisasi's own API accepting a DASC target. The returned
  `rows, cols` are then intended to pass straight back into DASCutils' `moviedasc`. Weigh this
  example as *documented intent*, not as a working invocation: the script cannot run as committed,
  for the call-signature reason recorded under Field 29. The executable evidence for this field is
  the `plots.py` call above.
- `themisasi` is declared in `pyproject.toml`'s `full` optional-dependency group, and the import in
  `plots.py` is wrapped in `try/except ImportError` with a `themisplot = None` fallback, which is the
  structure of an optional peer integration rather than a hard dependency.

Both packages are all-sky-imager tools, and their station sets overlap in Alaska — Poker Flat, Fort
Yukon, Eagle and Kaktovik each appear both among the DASC site codes and among the THEMIS ground
stations in the SPASE vocabulary. A user combining them is therefore doing exactly what the field
describes: running peer domain tools together on the same science problem.

**xarray is deliberately not recorded here.** https://github.com/pydata/xarray meets the letter of
the Tier B test, and the evidence is kept in full so a future agent can see that it was rejected on
principle rather than for want of evidence.

- *The evidence that qualifies it.* xarray sits in the guidance's Tier B — foundational-but-domain-adjacent
  packages that qualify on a specific documented exchange — and the qualifying example given there is
  a public API whose documented return type is an xarray object. DASCutils meets that test literally.
  The README states that `du.load()` "returns a dictionary of
  [xarray.DataArray](http://xarray.pydata.org/en/stable/generated/xarray.DataArray.html), which is
  like a 'smart' Numpy array", and describes the returned structure ("The images are in a 3-D stack:
  (time, x, y). `data.time` is the time of each image"). All three supports hold at the
  pinned revision: `README.md` lines 38–43 state the return type, `src/dascasi/tests/test_mod.py`
  line 27 asserts `isinstance(imgs[wavelength], xarray.DataArray)`, and `src/dascasi/plots.py` lines
  88–89 raise `TypeError` on a non-`DataArray` argument, making the type part of the contract. So
  DASCutils' documented output *is* an xarray object, which xarray-aware tooling can consume
  directly.
- *Why it is nonetheless not recorded.* The governing principle behind the relevance gate asks
  whether a package would be equally at home in a web app, a finance model, or a biology pipeline.
  xarray plainly would be. It is generic scientific-Python infrastructure rather than a high-level
  heliophysics or science peer tool, and the field's stated purpose is which such tools this software
  interoperates with. That principle governs however well the specific exchange is evidenced —
  recording xarray would read as a dependency listing dressed up in evidence. It was removed from
  Field 29 on the same principle, and it belongs in neither field. Re-open this only if the
  governing gate itself changes, not on the strength of the code evidence above, which was already
  weighed.
- *The same conclusion from the user's side.* A person browsing DASCutils' interoperable software is
  looking for the next tool to reach for. `xarray` does not answer that: it tells them how the data
  is shaped once they already have it, and any Python package that returns labeled arrays could list
  it, so it distinguishes nothing about DASCutils. `themisasi` does answer it, sending someone
  holding DASC imagery to the sibling tool for the co-located THEMIS all-sky imager at Fort Yukon.
  That is the difference the field exists to record, and it is why the verdict here is not a close
  call despite the strength of the code evidence above.

**Considered and not selected.**
- **astropy** — no astropy object crosses the API boundary; see Field 29.
- **h5py / the HDF5 format** — the HDF5 files DASCutils writes are self-describing image stacks
  readable by generic HDF5 tools, which is a *format* property already recorded in Fields 18 and 19.
  Interoperability with a file format is not interoperability with a package. From the searcher's
  side the entry would actively mislead: someone scanning this field for a peer tool to combine with
  DASCutils would find a storage library, and would learn only what the input and output format
  fields already tell them on the same page.
- **pymap3d** — a library DASCutils calls, with no exchange in the other direction and no shared data
  model. It belongs in Field 29 as a domain-specific dependency, and is recorded there.
- **numpy, scipy, matplotlib, cartopy, scikit-image** — Tier A generic infrastructure, excluded
  without exception.
- **"Part of the scientific Python ecosystem" and "a PyHC-listed package, so it interoperates with
  PyHC packages"** — neither is ever sufficient on its own, and neither is used here. DASCutils'
  PyHC listing is in `projects_unevaluated.yml`, which carries no interoperability assessment at all.

### 31. Related Instruments (OPTIONAL)

**Value:**
- **Instrument Name:** The all-sky imager at Poker Flat Research Range, Alaska.
- **Instrument Identifier:** https://spase-metadata.org/IUGONET/Instrument/NICT/SALMON/PF/asi

**Source:** Carried over from the existing HSSI record. The name above reproduces the vocabulary
row's stored `name` verbatim, including its trailing period; the identifier is a bare
`https://spase-metadata.org/` URL, so the entry binds to an existing row rather than creating one.

**What the software actually targets, and why the field is non-empty.** DASCutils is purpose-built
for the University of Alaska Fairbanks Geophysical Institute **Digital All-Sky Camera (DASC)**. It
clears the "designed to support" bar decisively and specifically:

- It parses DASC FITS header conventions by name — `OBSDATE`, `OBSSTART`, `FRAME`, `FILTWAV`, `GLAT`,
  `GLON` in `dio.py::gettime`, `getwavelength` and `getcoords`.
- It hard-codes the Poker Flat camera position, `{"lat0": 65.126, "lon0": -147.479}`, as the fallback
  for files whose headers lack `GLAT`/`GLON`, keyed on the `PKR` filename prefix.
- It implements DASC-specific detector handling: unsigned 14-bit data written into signed 16-bit
  integers ("DASC iKon cameras are/were 14-bit at least through 2015"), and an image rotation whose
  direction flips for pre-2012 frames.
- It works around a DASC-specific data incident, the 2013 RAID array failure, citing the instrument's
  own operator in a code comment: "Don Hampton says about 90% of data OK, but 10% NOK."
- It parses DASC filename conventions (`PKR_DASC_0428_20170102_030405.678.FITS`,
  `VEE_DASC_0000_20170102_030405.FIT`) and restricts downloads to six DASC site codes.

**The DASC has no record of its own in the vocabulary.** Searching the full
`InstrumentObservatory` list as read on 2026-08-29 for `DASC`, for `digital all[- ]sky`, for
`Venetie`/`VEE`, and for each of the six site codes returns no row for the UAF-GI Digital All-Sky
Camera. Restricting to *instrument* rows (`type == 1`), the four non-Poker sites that appear at all —
Eagle, Fort Yukon, Kaktovik and Toolik — carry only magnetometer instruments plus, at Fort Yukon, a
THEMIS ground all-sky imager; none has a DASC instrument row, and Venetie has no row of either type.
Those four sites *do* have site-level observatory rows, which is a Field 32 matter and is set out
there. Every identifier
returned by that read began with `https://spase-metadata.org/`, so the absence is an absence in
SPASE rather than a vocabulary defect. This is a documented omission at the level of the instrument itself, and it is the
reason the stored value is a proxy rather than a match.

**What the stored row actually is.** `https://spase-metadata.org/IUGONET/Instrument/NICT/SALMON/PF/asi`
is the **NICT** all-sky imager at Poker Flat Research Range. Its SPASE record names Minoru Kubota
(NICT) as Principal Investigator and describes the experiment as NICT's, "conducted as part of Alaska
Project, which is operated jointly by NICT and Gephysical Intitute of University of Alaska,
Fairbanks" (the misspellings are the record's own). It is an imager of "airglows and/or auroras" at
the same range, and in the vocabulary as read on 2026-08-29 it was the sole row whose name contains
"Research Range". It is therefore the closest available all-sky imager at the DASC's primary site — but it is a different
instrument, operated by a different institution.

**Alternatives examined and rejected as the instrument value.**
- `https://spase-metadata.org/IUGONET/Instrument/TohokuU/opt_obs/pok/ac` — "Aurora Camera at Poker
  Flat", Tohoku University, SPASE `InstrumentType: Imager`, `ObservatoryID:
  spase://IUGONET/Observatory/TohokuU/opt_obs/pokopt`. Another optical instrument at Poker Flat, also
  not the DASC. It is worth knowing about because it is the instrument that belongs to the Tohoku
  observatory row that Field 32 held before this refresh (see there).
- `https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/FYKN/ASI` — "THEMIS Ground Fort
  Yukon All Sky Imager". A THEMIS GBO camera co-located with a DASC site, operated for THEMIS. It is
  the instrument `themisasi` supports, not the one DASCutils supports, and belongs on that package's
  record.
- The Poker Flat magnetometer rows (`SMWG/Instrument/Ground/Poker.Flat/Magnetometer`,
  `IUGONET/Instrument/WDC_Kyoto/WDC/POK/Magnetometer`,
  `IUGONET/Instrument/TohokuU/mag_obs/pok/sm`, `SMWG/Instrument/THEMIS/Ground/UCLA-GBO/POKR/MAG`) and
  `IUGONET/Instrument/NICT/SALMON/PF/MFradar` — wrong instrument class entirely.

**Why the proxy is kept rather than the field emptied.** The alternative was to drop the entry
under the resolution ladder's "nothing defensible resolves" rule, on the ground that the DASC is a
specific instrument with no SPASE record and that a proxy names an instrument the software does not
read, leaving Field 32 to carry the site association alone. That was weighed and not chosen. The
NICT row is the closest available all-sky imager at the DASC's primary site, and keeping it surfaces
this record where DASCutils users would look — among Poker Flat optical instrumentation — which an
empty field would not.

The caveat stands and is why this note is kept: the recorded row names a different operator's
camera, so the entry should be read as a site-level proxy for the DASC, not as a claim that
DASCutils reads NICT data. What must never happen — however a future agent revisits this — is
inventing a DASC row, since a name without an identifier creates a new identifier-less vocabulary
row.

**When to revisit:** if SPASE registers the UAF-GI Digital All-Sky Camera, that row supersedes the
proxy recorded here.

### 32. Related Observatories (OPTIONAL)

**Value:**
- **Observatory Name:** Poker Flat Geophysical Observatory
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Ground/Poker.Flat

**Source:** Selected from the live `InstrumentObservatory` vocabulary, replacing the row this record
carried before this refresh (see "The previous value and why it was wrong" below). The name above
reproduces that vocabulary row's stored `name` character for character, and the identifier is a bare
`https://spase-metadata.org/` URL, so the entry binds to an existing row rather than creating one.

**Why this row.** `SMWG/Observatory/Ground/Poker.Flat` is the University of Alaska record: SPASE
AlternateName "Observatory Station Code: POKR", Acknowledgement "Please acknowledge: University of
Alaska", and Principal Investigator **Donald Hampton**. Two independent lines of evidence tie that
record to the data this software reads. First, DASCutils' own `src/dascasi/dio.py` cites him on the
RAID-corrupted DASC data: "Don Hampton says about 90% of data OK, but 10% NOK." Second — and from
outside the project — the Ozturk et al. (2020) acknowledgement quoted under Field 27 thanks "Mark
Conde and Don Hampton for the SDI data ... and ASI data (at http://optics.gi.alaska.edu/optics/)",
naming Hampton as a source of all-sky-imager data served from the same host `src/dascasi/web.py`
downloads from. Together those connect this SPASE record to the people operating the camera whose
data the software reads.

**The standard that decided it.** This field is read as an association a user would also follow in
the opposite direction: on a page listing the software related to an observatory, a visitor to the
UAF record should be unsurprised to find DASCutils there, and a visitor to a record belonging to a
different operator should find it out of place. The UAF site record passes that test plainly. The
alternatives below either fail it or pass it only for a reason such a visitor cannot see.

**A caveat carried by the chosen row, recorded so it is not mistaken for an error.** The record's
`ObservatoryGroupID`s are `Ground/GMAG` and `Ground/GIMA`, and two of its three `InformationURL`
entries describe the ground **magnetometer** array — the THEMIS GMAG site and an ASF/GI
magnetometer-array overview. The third is instrument-agnostic: a "HelioData" link to
`https://helio.data.nasa.gov/mission/Ground_Poker.Flat`, added 2026-07-20 according to the record's
own `RevisionHistory`. So although the record is site-level and its Principal Investigator is the
DASC's operator, SPASE's own descriptive links register it predominantly in a magnetometer context
rather than an optical one. That is a property of the SPASE record, not an argument against the
association.

**The previous value and why it was wrong.** This record carried
`https://spase-metadata.org/IUGONET/Observatory/TohokuU/opt_obs/pokopt`, vocabulary name "Poker Flat
aurora observatory", until this refresh. That row is **Tohoku University's** optical site at Poker
Flat: SPASE Principal Investigator Takeshi Sakanoi, metadata contact Manabu Yagi, description "Poker
Flat aurora observatory", location 65.119 N / 212.567 E. It shares the location with the DASC and
little else. It is a different operator's observatory; DASCutils cannot read its data, since the
software downloads from `ftp://optics.gi.alaska.edu` and parses DASC filename and header conventions
that do not apply to the Tohoku instrument; and it was not even the parent of the instrument recorded
in Field 31, which declares `ObservatoryID: spase://IUGONET/Observatory/NICT/SALMON/PF`. A visitor
arriving from Tohoku University's optical site would find DASCutils out of place there.

**Rejected — `https://spase-metadata.org/IUGONET/Observatory/NICT/SALMON/PF`, vocabulary name "Poker
Flat".** This is the declared parent of the instrument recorded in Field 31, so choosing it would
have made Fields 31 and 32 an internally consistent SPASE instrument/observatory pair. Its SPASE
record describes "Poker Flat Research Range of Geophysical Instititute, University of Alaksa
Fairbanks (GI/UAF)" with NICT experiments "operated as joint middle and upper atmosphere observations
beween NICT and GI/UAF" (the typos are the record's own), places it at 65.1 N / -147.5 E — matching,
to the record's precision, the DASC position hard-coded in `dio.py` — and declares
`ObservatoryRegion: ["Earth.NearSurface.Mesosphere", "Earth.NearSurface.AuroralRegion"]`, the same
evidence cited under Field 5. Finding DASCutils under it would not be surprising, so it comes
close to the deciding standard; what it lacks is that the record frames the site as NICT's joint
programme rather than as the UAF observatory that operates the DASC. Its one real advantage — SPASE-internal consistency with
Field 31 — is invisible to the person following an observatory-to-software link, and so carried no
weight against the operator match. Its vocabulary name, the bare string "Poker Flat", is also less
informative in a catalogue listing.

**Rejected — recording the DASC site network.** `src/dascasi/download.py` declares
`choices=["EAA", "FYU", "KAK", "PKR", "TOO", "VEE"]`, the kind of concrete supported-site list that
can justify recording several evidenced rows. Five of the six have SMWG ground observatory rows, all
carrying Principal Investigator Donald Hampton and the "Please acknowledge: University of Alaska"
statement:

| Site code | Vocabulary `name` (as stored) | Identifier |
|---|---|---|
| PKR | Poker Flat Geophysical Observatory | https://spase-metadata.org/SMWG/Observatory/Ground/Poker.Flat |
| FYU | Fort Yukon Geophysical Observatory | https://spase-metadata.org/SMWG/Observatory/Ground/Fort.Yukon |
| EAA | Eagle Geophysical Observatory | https://spase-metadata.org/SMWG/Observatory/Ground/Eagle |
| KAK | Observatory Station Code: KAKO | https://spase-metadata.org/SMWG/Observatory/Ground/Kaktovik |
| TOO | Toolik Lake Geophysical Observatory | https://spase-metadata.org/SMWG/Observatory/Ground/Toolik.Lake |

The option was not taken, for four reasons that compound.

1. *SPASE registers no optical instrument the software could serve at the other sites.* Restricting
   the vocabulary read of 2026-08-29 to instrument rows, Eagle, Kaktovik and Toolik Lake carry only
   magnetometers, and the one all-sky imager at Fort Yukon is
   `SMWG/Instrument/THEMIS/Ground/UCLA-GBO/FYKN/ASI`, a THEMIS GBO camera that belongs to
   `themisasi`'s record rather than this one. Associating DASCutils with those sites would point a
   user at instrumentation this software does not read.
2. *The in-repository evidence for the non-PKR sites is thin.* The `choices` list is the only place
   the six are enumerated as a set. Outside it, the tracked tree mentions a non-PKR site only in a
   `VEE` usage example in `download.py`'s own module docstring (lines 10 and 12), a
   `VEE_DASC_0000_20170102_030405.FIT` filename-convention comment at `src/dascasi/web.py` line 124,
   and the `KAK` and `TOO` case arms of the deprecated `reference/downloadDASC.sh`. There is no test
   data, no calibration file and no hard-coded position for any site but Poker Flat: `dio.py` lines
   353–354 fall back to `{"lat0": 65.126, "lon0": -147.479}` for the `PKR` filename prefix and to
   NaN for every other prefix, and the FITS sample images and the azimuth/elevation calibration pair
   packaged under `src/dascasi/tests/data/` are `PKR_DASC_*` files.
3. *At least one site code looks vestigial.* `src/dascasi/web.py` line 45 builds the archive path as
   `<site>/DASC/RAW/` for every site, while `reference/downloadDASC.sh` maps `TOO` to `CASC` rather
   than `DASC`. The package would therefore look under `TOO/DASC/RAW/` where the reference script
   expects `TOO/CASC/RAW/`, which suggests the site list outran the download code.
4. *The network could never be recorded completely.* `VEE` (Venetie) has no SPASE row of either type,
   so the association would always be five-sixths of the declared site list.

Two details about those rows are worth keeping even though the option was not taken. The Kaktovik
row's stored `name` in the vocabulary is the SPASE *AlternateName* form "Observatory Station Code:
KAKO" rather than the ResourceName "Kaktovik Geophysical Observatory"; if that row is ever used, the
name in the table above is what must be written, character for character. And the magnetometer-context
caveat noted for the chosen row applies unevenly across the five: all five carry three
`InformationURL` entries of the same three kinds — the THEMIS GMAG site, an ASF/GI magnetometer-array
overview (whose target URL differs for Toolik Lake), and the generic HelioData mission page — and all
five name Donald Hampton as Principal Investigator with the acknowledgement "Please acknowledge:
University of Alaska", but their `ObservatoryGroupID`s differ: Poker Flat, Fort Yukon and Kaktovik
carry both `Ground/GMAG` and `Ground/GIMA`; Eagle carries only `Ground/GIMA`; and Toolik Lake carries
neither.

**A trap to avoid — do not resolve `TOO` by name.**
`https://spase-metadata.org/SMWG/Observatory/Ground/Toolangi`, whose vocabulary name is "Observatory
Station Code: TOO", is **Toolangi, Australia**, and matches the DASC's `TOO` site code purely by
coincidence. The correct Alaskan row is `Ground/Toolik.Lake`. A future agent matching site codes
against abbreviations will hit this.

**Rejected outright:** `SMWG/Observatory/IAGA/Poker.Flat` (vocabulary name "Poker.Flat"),
`IUGONET/Observatory/WDC_Kyoto/WDC/POK` ("Poker Flat Geomagnetic Observatory"), and
`IUGONET/Observatory/TohokuU/mag_obs/pokmag` ("Poker Flat geomagnetic observatory") — all geomagnetic
observatory records for an optical instrument's software. Also rejected:
`SMWG/Observatory/THEMIS/Ground/GIMA` ("NASA THEMIS Ground Stations in Alaska") and
`SMWG/Observatory/Ground/GIMA` ("GIMA") — network-level magnetometer groupings, and in the THEMIS
case belonging to `themisasi`'s record rather than this one.

**Fields 31 and 32 are deliberately not a SPASE parent/child pair.** The instrument recorded in
Field 31 declares its parent as `spase://IUGONET/Observatory/NICT/SALMON/PF`, not the UAF row
recorded here, so the two entries come from different SPASE record families that share the Poker Flat
location. Both are proxies for one UAF-GI instrument that SPASE does not register: Field 31 names the
nearest all-sky imager at the site, and Field 32 names the site as UAF operates it. Pairing them for
SPASE-internal tidiness would have meant choosing the observatory by the instrument proxy's lineage
instead of by the operator of the data DASCutils actually reads. If SPASE ever registers the UAF-GI
Digital All-Sky Camera, both fields should be revisited together: that row would supersede the
Field 31 proxy, and it would most likely declare this observatory as its parent.

### 33. Logo (OPTIONAL)
**Value:** Not found

**Source:** Evidenced absence with a specifically rejected alternative. HSSI held an empty string
for this field before this refresh, which is correct.

**Rejected alternative — https://i.ibb.co/JKLF4FB/logo.jpg.** This is the `logo:` URL in the PyHC
registry entry for DASCutils, and it is the value a future agent is most likely to reach for.
It resolves to a real, live JPEG — 10136 bytes, 598 × 141 pixels, served as `image/jpeg` — so it is
not rejected as a broken link or as an HTML placeholder. Two other things disqualify it:

1. **It is not a logo.** The image is a cropped photograph of a green auroral arc against a dark sky.
   It contains no wordmark, no lettering, and no graphic identity — it is a decorative banner, at a
   4.2:1 aspect ratio suited to a page header rather than an identifying mark.
2. **It is not durably hosted.** `i.ibb.co` is ImgBB, a free third-party image host. The URL is not
   commit-pinned, not repository-hosted, and carries no version or retention guarantee, so it cannot
   satisfy the field's requirement that the logo "be stored online in a permanent place."

**No repository-hosted candidate exists.** The pinned tree contains three images, all under
`src/dascasi/tests/data/`: `dasc_azel.png`, `dasc_projection_plot.png` and
`dasc_projection_plot_pc.png`. All three are example scientific output — an azimuth/elevation contour
plot and two projected-image plots. The README embeds two of them, `dasc_projection_plot_pc.png` and
`dasc_azel.png`, to illustrate `scripts/PlotProjectedImage.py` and `scripts/PlotAzimuthElevation.py`;
`dasc_projection_plot.png` is not referenced outside the test-data directory. None is a logo, and
pointing Field 33 at a test-data figure would misrepresent them.

**When to revisit:** if the project adds a genuine logo asset to the repository, a raw URL pinned to
a specific commit and verified to serve `image/*` content would be the value to record.
