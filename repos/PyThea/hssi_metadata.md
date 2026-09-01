# HSSI Metadata — PyThea

**HSSI Software ID:** 9de35b9b-704e-4cf3-b580-fff54b9ede15
**Repository:** https://github.com/AthKouloumvakos/PyThea
**Source Revision:** f5bc63e11335b2fdaa0d49bc482083c65c8875bb
**Source Revision Date:** 2026-06-11 (tag `v1.3.0`)
**Extraction Date:** 2026-07-29
**Validation Date:** 2026-07-30
**Validation Status:** PASS

This is the canonical metadata record for PyThea, reconciled against the live HSSI entry and the
source repository at the revision above. Every controlled-vocabulary value was confirmed against the
live HSSI vocabularies; Fields 31–32 carry SPASE identifiers throughout.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)

Not applicable — PyThea was already present in HSSI and its original submitter is not part of the
public record. Submitter details are set at initial submission and are not part of this metadata.

---

### 2. Persistent Identifier (RECOMMENDED)

`https://doi.org/10.5281/zenodo.5713659`

*Source / evidence:* this is PyThea's active Zenodo concept DOI — the one the project itself tells
users to cite (`README.md:105,107`, `docs/source/acknowledge.rst:16,24`, `docs/source/index.rst:62,64`,
`PyThea/PyThea_app.py:107`). It is fed by the GitHub–Zenodo integration and spans v0.5.2 (2021-11-19)
through v1.3.0 (2026-06-11), resolving to version record `10.5281/zenodo.20648868`.

*Corrected from* `https://doi.org/10.5281/zenodo.5683556`. That is a genuine but abandoned first
PyThea deposit: it carries a single version record (v0.4.0, issued 2021-11-17) and was never updated
after 2021-11-18, so it does not track the software. Field 10 still records its 2021-11-17 date as
PyThea's first publication.

---

### 3. Code Repository (MANDATORY)

`https://github.com/AthKouloumvakos/PyThea`

*Source:* stored HSSI value; `git remote -v`; `pyproject.toml:48` `"Source Code" =
"https://github.com/AthKouloumvakos/PyThea"`. GitHub API confirms `default_branch = master`,
`archived = false`.

---

### 4. Software Functionality (MANDATORY)

All 22 values below were confirmed against the live `FunctionCategory` vocabulary, and every
subcategory's parent is present in the list.

- **Coordinate Transforms**
- **Coordinate Transforms: Solar** — model parameters are reported in *both* Heliographic Stonyhurst
  and Heliographic Carrington (`PyThea/geometrical_models.py:376-395`, `:496-520`, `:764-784`
  `to_dataframe()` → `transform_to(frames.HeliographicCarrington(observer='Earth', …))`); model point
  clouds are built as `SkyCoord` in `frames.HeliographicStonyhurst` and projected through each map's
  WCS (`geometrical_models.py:111-131`, `:479-495`, `:660-671`); Stonyhurst/Carrington grids, limbs,
  prime meridian and solar equator overlays (`PyThea/utils.py:208-268`); Helioprojective visibility
  tests (`PyThea/extensions/Parker_spirals/utils.py:33-35`); solar differential rotation of HEK
  coronal-hole boundaries via `solar_rotate_coordinate` (`PyThea/extensions/hek/utils.py:8,129`).
- **Coordinate Transforms: Heliospheric** — Parker spiral coordinates computed in heliographic
  Carrington out to the observer's heliocentric distance and mapped back to a 1 R_sun footpoint
  (`PyThea/extensions/Parker_spirals/__init__.py:6-63`, tested in
  `PyThea/test/test_extension_utils.py:15,39`); Heliocentric Earth Ecliptic (HEE) conversions for the
  ecliptic-plane view (`docs/source/examples/Basic_Plots/plot_ellipsod_on_ecliptic_view.py:41-45`).
- **Coordinate Transforms: Mission-Specific** — spacecraft-specific pointing/observer corrections:
  AIA pointing update from JSOC (`PyThea/sunpy_dev/extern/sunkit_instruments/aia/utils.py:3,10`),
  SOHO observer location rewritten from JPL Horizons ephemeris into `HGLN_OBS`/`HGLT_OBS`/`DSUN_OBS`
  (`.../lasco/utils.py:12-19`), STEREO/EUVI image dejitter from FPS offsets updating
  `CRPIX1/2`/`CRPIX1A/2A`/`XCEN`/`YCEN` (`.../stereo/utils.py:120-152`).
- **Data Processing and Analysis**
- **Data Processing and Analysis: Data Access and Retrieval** — `download_fits()` runs
  `Fido.search`/`Fido.fetch` (`PyThea/utils.py:271-329`); HEK event queries (`PyThea/utils.py:60-91`,
  `PyThea/extensions/hek/utils.py:11-70`); two bundled `sunpy` Fido clients for NASCOM archives
  (`PyThea/sunpy_dev/net/dataretriever/sources/lasco.py`, `.../stereo.py`); SOAR access via
  `sunpy_soar` (`PyThea/config/selected_imagers.py:8,77-90`); `pooch`-managed sample data
  (`PyThea/data/sample_data.py`); local FITS-database manager (`PyThea/utils_database.py:57-95`).
- **Data Processing and Analysis: Calibration** — CHANGELOG v0.9.0 "Adds calibration for AIA, LASCO,
  and STEREO EUVI"; EUVI bias subtraction, filter-throughput normalisation and dejitter
  (`.../stereo/utils.py:107-155`); COR1 three-angle polarisation inversion to total brightness via a
  Mueller matrix (`.../stereo/utils.py:11-104`); exposure-time normalisation
  (`PyThea/sunpy_dev/map/maputils.py:104-128`); AIA `aiapy.calibrate.update_pointing` prep
  (`.../aia/utils.py:3,10`).
- **Data Processing and Analysis: Image Processing** — running-difference and base-difference image
  sequences (`maputils.py:31-78`, `:231-259`), coronagraph occulter masking with per-detector inner/outer
  radii (`maputils.py:262-309`), median filtering (`PyThea/utils.py:127-129`), superpixel rebinning
  (`maputils.py:221-224`), colour-limit determination (`maputils.py:312-325`).
- **Data Processing and Analysis: Processing** — the per-imager processing pipeline
  `maps_process()` / `single_imager_maps_process()` (`PyThea/utils.py:369-447`) chaining
  `filter_maps` → `prepare_maps` → `maps_sequence_processing`.
- **Data Processing and Analysis: Data Reduction** — `filter_maps()` discards duplicates and maps with
  non-nominal exposure, dimensions or polarisation state (`maputils.py:131-174`); superpixel
  downsampling reduces 4096² AIA / 2048² SECCHI frames (`maputils.py:221-224`, factors declared per
  imager in `PyThea/config/selected_imagers.py:13-90`).
- **Data Processing and Analysis: Analysis** — CME/shock kinematics: apex height, flank lengths, speed
  and acceleration derived from the fitted parameters with 1-sigma uncertainty bands
  (`PyThea/utils.py:645-850`), polynomial / smoothing-spline / user-supplied-expression fits with
  covariance-derived sigma (`PyThea/utils.py:853-970`), analytic model-parameter conversions
  (`geometrical_models.py:167-243`, `:522-563`).
- **Data Processing and Analysis: Time Series Analysis** — the fits operate on a `pandas.DatetimeIndex`
  of fitting times resampled to a one-minute grid, and speed/acceleration are numerical time
  derivatives of the fitted height-time curve (`PyThea/utils.py:735-791`, `:884-888`).
- **Data Visualization**
- **Data Visualization: 2D Graphics** — `make_figure()` renders each `sunpy.map` on a WCS axis with
  colour limits, limb, grid and inverted-axis handling (`PyThea/utils.py:94-170`); geometrical-model
  overlays (`geometrical_models.py:310-374`, `:758-762`, `:805-811`); HEK event annotations
  (`PyThea/extensions/hek/utils.py:71-160`).
- **Data Visualization: Line Plots** — height-time, speed-time, acceleration-time, longitude-time and
  latitude-time plots with shaded uncertainty bands (`PyThea/utils.py:645-850`; figure test
  `PyThea/test/test_figures.py:176`).
- **Data Visualization: Orbit Plots** — ecliptic-plane view drawing planet and spacecraft orbits
  (Mercury, Venus, Earth, STEREO-A, Parker Solar Probe, Solar Orbiter, BepiColombo) with Parker
  spirals (`docs/source/examples/Basic_Plots/plot_ellipsod_on_ecliptic_view.py:50-160`); spacecraft and
  planet positions marked on the images themselves (`PyThea/utils.py:173-205`,
  `PyThea/config/selected_bodies.py`).
- **Data Visualization: Web-Based** — the whole user interface is a Streamlit browser application
  (`PyThea/PyThea_app.py`, launched by `pythea streamlit` → `PyThea/pythea_cli.py:25-49`;
  `docs/source/application.rst:7` "Its user-friendly GUI, built on Streamlit…").
- **Models and Simulations**
- **Models and Simulations: Forward-Fitting** — the core capability: three geometrical models (GCS
  flux rope, spheroid, ellipsoid) are forward-projected onto multi-viewpoint imagery and their
  positional/geometrical parameters adjusted until the projection matches the observed front
  (`PyThea/geometrical_models.py`, `PyThea/modules.py:130-290` fitting sliders,
  `PyThea/PyThea_app.py:192-560`).
- **Models and Simulations: Empirical** — `docs/source/geometrical_models.rst:45`: "The Graduated
  Cylindrical Shell (GCS) model is an **empirical geometrical model** of a flux rope defined by
  Thernisien et al. (2006, 2011)."
- **Models and Simulations: Physics-Based** — the Parker spiral interplanetary-magnetic-field model,
  parameterised by solar rotation rate and solar wind speed
  (`PyThea/extensions/Parker_spirals/__init__.py:6-63`; app feature added in CHANGELOG v0.13.0
  "Implements new feature of Parker spiral and HEK events visualization on the images").
- **Models and Simulations: Field-line Tracing** — the same module traces the spiral field line from
  an observer's position back to the Sun and returns its solar footpoint at r = 1 R_sun
  (`Parker_spirals/__init__.py:36-63` `footpoint()`; tested at
  `PyThea/test/test_extension_utils.py:39`).

*Deliberately excluded, with reasons (audit trail):*
- `Data Visualization: 3D Graphics` — **the extraction brief's premise that PyThea renders 3D
  visualizations with `pyvista` does not hold.** `pyvista` appears only at
  `PyThea/geometrical_models.py:26,463-470`, where `pv.ParametricEllipsoid` and `pv.Sphere` are
  intersected to *compute* the ellipsoid∩photosphere curve; there is no `pv.Plotter`, no `mplot3d`,
  no VTK render window anywhere in the repo (CHANGELOG v0.7.4 confirms the switch from Vedo to
  PyVista was made "to reduce rendering time" of that geometric calculation). All rendering is
  matplotlib onto 2D WCS axes.
- `Data Processing and Analysis: 2D Slices` / `Data Visualization: 2D Slices` — the intersection above
  is a surface∩surface curve, not a cut through a 3D data volume.
- `Data Visualization: Mission-Specific` — per-instrument title and colour-limit special cases exist
  (`PyThea/utils.py:131-164`, `maputils.py:312-325`) but they are cosmetic formatting, not a distinct
  mission-specific visualization type.
- `Data Visualization: Movies` — no animation code.
- `Models and Simulations: Data Guided` — would add nothing beyond `Forward-Fitting`.
- `Models and Simulations: Theory` — the models are analytic *geometry*, not theoretical physics.
- `Mission-related: *` — PyThea is an independent analysis tool, not part of any mission ground system.
- `Servers and Environments: *` — the Streamlit app runs locally for a single user; there is no
  Dockerfile, server deployment or HPC component. `Data Visualization: Web-Based` already captures the
  browser UI.

---

### 5. Related Region (MANDATORY)

- **Solar Environment** — the package's overall domain.
- **Corona** — the reconstruction target is CMEs and CME-driven shocks in the corona, fitted to
  coronagraph and EUV coronal imagery: LASCO C2 (2-6 R_sun) and C3, SECCHI COR1/COR2, Metis, and
  AIA 193 Å / 211 Å and EUVI 195 Å coronal channels (`PyThea/config/selected_imagers.py:13-83`);
  `docs/source/geometrical_models.rst:9,45` describes fronts observed "in white-light and extreme
  ultraviolet" and GCS reproducing flux-rope CMEs "in the solar corona".
- **Interplanetary Space** — the supported imager set extends well past the corona: STEREO/SECCHI
  HI1 and HI2 heliospheric imagers (`selected_imagers.py:53-67`), PSP/WISPR inner and outer telescopes
  (`:69-75`), Solar Orbiter SoloHI (`:85-90`); the Parker spiral / footpoint model and the ecliptic
  orbit view operate out to ~1 AU
  (`docs/source/examples/Basic_Plots/plot_ellipsod_on_ecliptic_view.py:88-92`, axis limits ±1.15 AU).

*Considered and excluded:* `Chromosphere` and `Photosphere` — the configured channels are coronal;
the only 1600 Å AIA data in the repo is a figure-test fixture (`PyThea/data/sample_data.py:9-16`).
`Solar Wind` — solar wind speed is an *input parameter* to the Parker spiral (default 350 km/s), but
PyThea neither reads nor analyses solar wind measurements.

---

### 6. Authors (MANDATORY)

**Author 1**
- **Name:** Athanasios Kouloumvakos (givenName `Athanasios`, familyName `Kouloumvakos`)
- **Author Identifier:** `https://orcid.org/0000-0001-6589-4509`
- **Affiliation:**
  - Organization: `Johns Hopkins University Applied Physics Laboratory`
  - Affiliation Identifier: `https://ror.org/029pp9z10`

*Source / evidence for the author:* `pyproject.toml:26-28` (sole `authors` entry); `.zenodo.json:6-12`
(sole creator, with ORCID); the Zenodo v1.3.0 record and DataCite `10.5281/zenodo.5713659` (single
creator, `nameType Personal`, ORCID `0000-0001-6589-4509`); ORCID confirms the given/family name
spelling; `README.md:115` "The lead author of this software package Athanasios Kouloumvakos".

*Source / evidence for the affiliation:* three independent current sources agree —
1. ORCID employments for `0000-0001-6589-4509`: exactly one employment, "Johns Hopkins University
   Applied Physics Laboratory" (North Laurel, Maryland, US), disambiguated to ROR
   `https://ror.org/029pp9z10`. No IRAP employment is listed.
2. `.zenodo.json:10` — `"affiliation": "The Johns Hopkins University Applied Physics Laboratory,
   Maryland, USA"`, in-repo at the extracted revision.
3. The Zenodo v1.3.0 record and DataCite `10.5281/zenodo.5713659` creators carry the same JHU/APL
   affiliation.

ROR `https://ror.org/029pp9z10` resolves to display name `Johns Hopkins University Applied Physics
Laboratory`, matching the recorded organization name exactly.

**Completed correction (2026-07-30).** The affiliation previously read `Institut de Recherche en
Astrophysique et Planétologie` (ROR `https://ror.org/05hm2ja81`), a value that traced only to the 2021
v0.4.0 Zenodo/DataCite record and that no current source supports. It was replaced — not
supplemented — because this field records where an author *is*, not an affiliation history. Verified
live afterwards: the author resolves to Johns Hopkins University Applied Physics Laboratory / ROR
`https://ror.org/029pp9z10` and to no other organization.

*Additional authors — considered, not added:* `git shortlog -sne --all` shows one non-Kouloumvakos
committer, Jan Gieseler (1 commit, `2bd71771`, 2022-11-28, "replace os.environ['HOME'] with
Path.home()"), and the reference publication (Field 14) has six authors (Kouloumvakos,
Rodríguez-García, Gieseler, Price, Vourlidas, Vainio). No software-authorship source —
`pyproject.toml`, `.zenodo.json`, or the Zenodo/DataCite creator lists — credits anyone but
Kouloumvakos, so the paper's co-author list is publication authorship rather than software
authorship. Kouloumvakos is the sole author; nobody was dropped.

---

### 7. Software Name (MANDATORY)

`PyThea`

*Source / evidence:* the concise product name, distinguished upstream from the longer citation title
`PyThea: A software package to reconstruct the 3D structure of CMEs and shock waves` (which is a
Zenodo/DataCite title and is carried by Fields 8/9 as descriptive metadata, not by this field):
- `pyproject.toml:10-11` — `name = "PyThea"` and `description = "PyThea: A software package to
  reconstruct the 3D structure of CMEs and shock waves"`. The long string is the *description* field.
- PyPI `https://pypi.org/pypi/PyThea/json` — `info.name = "PyThea"`,
  `info.summary =` the long string.
- Repository name `AthKouloumvakos/PyThea`; console entry point `pythea`
  (`pyproject.toml:86-87`); documentation site `https://www.pythea.org`; in-app title
  `st.set_page_config(page_title='PyThea')` (`PyThea/PyThea_app.py:132`);
  `docs/source/index.rst:9` "PyThea's Documentation".
- SoMEF 0.9.11 on the repository: `name = "PyThea"` (confidence 1.0), `full_title =` the long string.
No source was found that contradicts `PyThea` as the canonical product name.

*Corrected 2026-07-30* from the long citation title to the concise product name.

---

### 8. Description (MANDATORY)

> PyThea is an open-source software package that can be used to reconstruct the 3D structure of
> Coronal Mass Ejections (CMEs) and shock waves and determine their kinematics using remote-sensing
> observations. The tool implements the Graduated Cylindrical Shell (GCS) model that can be used to
> reconstruct CMEs and two geometrical models, namely a spheroid and ellipsoid model to reconstruct
> shock waves. It also implements remote-sensing observations from multiple viewpoints such as the
> Solar and Heliospheric Observatory (SoHO), Solar Terrestrial Relations Observatory (STEREO), and
> Parker Solar Probe. Imaging data from the Solar Dynamics Observatory (SDO) and Solar Orbiter are
> also supported.

*Source / evidence:* the first three sentences are the current upstream `README.md:13` text, verbatim,
at revision `f5bc63e1`. They differ from the stored HSSI description in exactly one respect — the
clause now reads "…(STEREO), **and Parker Solar Probe**". The stored text matches the older
`.zenodo.json:3` abstract, which the author has not refreshed. Using the README wording keeps the
author's own phrasing while removing a factual staleness: PSP/WISPR support was added in CHANGELOG
v0.13.0.

*Final sentence.* The upstream README text, even at v1.3.0, omits two observatories the package
demonstrably supports, so the author's wording alone would leave the description factually incomplete.
That sentence is therefore editorial rather than quoted. Evidence for the claim it makes:
- **SDO** — `PyThea/config/selected_imagers.py:21-27` configures `AIA-193` and `AIA-211`
  (`'source': 'SDO'`); AIA calibration via `aiapy` at
  `PyThea/sunpy_dev/extern/sunkit_instruments/aia/utils.py:3,10`; CHANGELOG v0.12.0 "Adds more imaging
  data from SDO/AIA".
- **Solar Orbiter** — `selected_imagers.py:77-90` configures EUI (`EUI-FSI174-IMAGE`), Metis
  (`METIS-VL-TB`) and SoloHI tiles T1–T4 (`'source': 'SOLO'`), fetched from the Solar Orbiter Archive
  via `sunpy_soar`; CHANGELOG v0.14.0 "Adds imaging data from Solar Orbiter EUI and METIS" and v1.0.0
  "Adds imaging data from Solar Orbiter's SOLOHi".

Both observatories are correspondingly recorded in Field 32, and their instruments in Field 31.

---

### 9. Concise Description (OPTIONAL)

> PyThea is an open-source Python package that reconstructs the 3D structure of coronal mass ejections
> and shock waves and determines their kinematics from multi-viewpoint remote-sensing observations.

198 characters, within the 200-character limit.

*Source / evidence:* this replaced a mechanical 200-character truncation of the description that broke
mid-word ("…using remote-sensing **observat**") — a defect rather than editorial intent. The
replacement keeps the author's own sentence and vocabulary and completes it.

*Third variant considered, not adopted:* the GitHub repository `description` field reads "PyThea is an
open-source software package to perform coronal mass ejection (CME) and shock wave 3D reconstruction
using multi-viewpoint remote-sensing observations." It contradicts neither Field 8 nor Field 9; the
README wording is preferred for Field 8 as the author's fullest statement, and the concise text above
for Field 9 because it completes the stored sentence rather than substituting a different one.

---

### 10. Publication Date (RECOMMENDED)

`2021-11-17`

*Source / evidence:* this is the `Issued` date of the first PyThea Zenodo record
(`10.5281/zenodo.5683556`, v0.4.0) — DataCite `dates = [{"date": "2021-11-17", "dateType":
"Issued"}]`. Field 10 asks for the date of first publication of the initial version, so the stored
value is correct and should not be moved to the newer concept DOI's date (2021-11-19 for v0.5.2 /
2026-06-11 for v1.3.0). Recommend keeping it unchanged even though Field 2 is being repointed.

---

### 11. Publisher (RECOMMENDED)

- **Organization:** `Zenodo`
- **Publisher Identifier:** `https://zenodo.org`

*Source:* stored HSSI value; DataCite `10.5281/zenodo.5713659` → `publisher = "Zenodo"`; releases are
minted through the GitHub–Zenodo integration (`.zenodo.json` present in the repo root).

---

### 12. Version (RECOMMENDED)

- **Version Number:** `v1.3.0`
- **Version Date:** `2026-06-11`
- **Version PID:** `https://doi.org/10.5281/zenodo.20648868`
- **Version Description:**

> Features: extends the network data sources available for selected imagers, and adds a method to
> manually import FITS files from a folder. Minor changes: updates the dependency to sunpy>=7.1.2.
> Bug fixes: fixes a bug in figure creation, fixes a bug in the kinematic plots, and guards against
> uninitialized variables.

*Refreshed from* `v0.4.0`, which had been current since 2021.

*Source / evidence:*
- Version number and date: git tag `v1.3.0` → commit `f5bc63e11335b2fdaa0d49bc482083c65c8875bb`,
  authored 2026-06-11; PyPI `1.3.0` sdist/wheel `upload_time_iso_8601 = 2026-06-11T19:40:58.827624Z`;
  Zenodo record `20648868` `metadata.version = "v1.3.0"`, `publication_date = 2026-06-11`.
- Version PID: `GET https://zenodo.org/api/records/20648868` → `doi = 10.5281/zenodo.20648868`,
  `conceptdoi = 10.5281/zenodo.5713659`.
- Version description: summarised from `CHANGELOG.md:1-12` (the `# v1.3.0` section), cross-checked
  against the GitHub release body for tag `v1.3.0` (release `338192231`, identical bullet list).
- **Upstream date error, not propagated:** `CHANGELOG.md` dates v1.3.0, v1.2.0 and v1.1.0 all as
  "12-Feb-2025" — a copy-paste error. The authoritative per-release dates are the git tags / PyPI
  uploads / Zenodo records: v1.3.0 = 2026-06-11, v1.2.0 = 2025-10-21, v1.1.0 = 2025-02-12.
- Store the bare `v1.3.0`; do **not** store the view API's rendered `<name> - <version>` string.

---

### 13. Programming Language (RECOMMENDED)

- `Python 3.x`

*Source:* stored HSSI value; `pyproject.toml:12` `requires-python = ">=3.12"` and
`:17-18` classifiers `Programming Language :: Python :: 3` / `:: 3.12`; SoMEF reports Python as the
only language (215,140 bytes). `find . -name '*.py'` accounts for every source file in the repo —
no C/Fortran/IDL/JavaScript sources exist. The only non-Python languages present are reStructuredText
docs and a small CSS file (`docs/source/_static/css/custom.css`), neither of which is a significant
implementation language.

---

### 14. Reference Publication (RECOMMENDED)

`https://doi.org/10.3389/fspas.2022.974137`

*Source / evidence:* Kouloumvakos, A., Rodríguez-García, L., Gieseler, J., Price, D. J., Vourlidas, A.,
& Vainio, R. (2022). *PyThea: An open-source software package to perform 3D reconstruction of coronal
mass ejections and shock waves.* Frontiers in Astronomy and Space Sciences, 9, 974137. Crossref
confirms the title, journal, `issued 2022-09-06`, and the six-author list. The project names it as
*the* citation: `README.md:105,107` ("please mention it in the main text and cite _PyThea_ paper"),
`docs/source/acknowledge.rst:8-12`, `docs/source/index.rst:53-58`, `PyThea/PyThea_app.py:107`.

---

### 15. License (RECOMMENDED)

- **License:** `GNU General Public License v3.0 or later`
- **License URI:** `https://spdx.org/licenses/GPL-3.0-or-later.html`

*Source:* stored HSSI value, which matches the live `License` row verbatim (row
whose stored URL is exactly the SPDX URI above).
Corroborated by `LICENSE.md` (GPL v3 full text, 33,872 bytes), `pyproject.toml:14` `license = { file
= "LICENSE.md" }` and `:20` classifier `License :: OSI Approved :: GNU General Public License v3
(GPLv3)`, every source-file header ("either version 3 of the License, or (at your option) any later
version" — e.g. `PyThea/utils.py:6-9`), `.zenodo.json:4` `"license": "GPL-3.0+"`, and DataCite
`rightsList` → `rights = "GNU General Public License v3.0 or later"`, `rightsIdentifier = "gpl-3.0+"`.
The "or later" variant is therefore correct, not the plain GPL-3.0-only that the GitHub API reports.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

All values lowercase, one keyword per entry. Every value below already exists as a row in the live
`Keyword` vocabulary, so no new rows are minted.

*Stored in HSSI (all retained):*
- `coronal mass ejections`
- `euv waves`
- `heliophysics`
- `python`
- `science`
- `shock waves`
- `solar`
- `solar physics`

*Added:*
- `coronagraph` — the majority of supported imagers are coronagraphs (LASCO C2/C3, SECCHI COR1/COR2,
  Metis) and the code models their occulters explicitly
  (`PyThea/sunpy_dev/map/maputils.py:262-309`).
- `remote sensing` — the project's own framing: "determine their kinematics using remote-sensing
  observations" (`README.md:13`, `PyThea/utils.py:2-3` module header).
- `flux rope reconstruction` — the GCS model is a flux-rope model
  (`docs/source/geometrical_models.rst:45`; `PyThea/geometrical_models.py:589` "A class of the GCS CME
  model").
- `solar imaging` — multi-viewpoint solar imaging from six observatories
  (`PyThea/config/selected_imagers.py`).

*Sources reconciled:* `pyproject.toml:25` `keywords = ['science', 'solar physics', 'solar', 'coronal
mass ejections', 'shock waves', 'EUV waves']` (all already present, lowercased); GitHub repository
topics `["heliophysics", "python", "solar-physics"]` — `solar-physics` folded into the existing
`solar physics` row rather than minting a hyphenated near-duplicate. No stored keyword was dropped.

---

### 17. Data Sources (OPTIONAL)

- `The Virtual Solar Observatory.` — *(note the trailing period; that is the live row name)*
  `PyThea/utils.py:273` "Downloads the imaging data (FITS files) from the Virtual Solar Observatory
  (VSO)"; the default provider for 16 of the configured imagers
  (`PyThea/PyThea_app.py:168` "The default providers (left) use VSO to download data."); remote test
  `PyThea/test/test_remote_clients.py:78-105` asserts `'vso' in result.keys()` for AIA, LASCO,
  COR1/COR2, EUVI, HI1/HI2 and WISPR.
- `Observatory/Mission-specific` — the Solar Orbiter Archive (SOAR) via `sunpy_soar`
  (`PyThea/config/selected_imagers.py:8,77-90`; `test_remote_clients.py:113-129` asserts
  `'soar' in result.keys()`); JSOC for AIA pointing metadata
  (`PyThea/sunpy_dev/extern/sunkit_instruments/aia/utils.py:10-14`, warning text "Check connection
  with JSOC"); the NASCOM SOHO/LASCO and STEREO/SECCHI mission archives (see next entry). Selected in
  accordance with the Field 17 instruction to cross-list observatory-specific sources with Field 32.
- `HTTP/HTTPS Directories` — two bundled `sunpy` `GenericClient` subclasses walk dated HTTPS directory
  trees and parse their plain-text indices:
  `PyThea/sunpy_dev/net/dataretriever/sources/lasco.py:24`
  (`https://sohoftp.nascom.nasa.gov/qkl/lasco/quicklook/level_05/%y%m%d/`) and
  `.../stereo.py:24,54` (`https://stereo-ssc.nascom.nasa.gov/data/ins_data/secchi/L0/…`). Sample data
  is likewise fetched over HTTPS with `pooch` (`PyThea/data/sample_data.py:7-11`).
- `Other` — two further network sources have no row in the 17-value `DataInput` vocabulary: the
  Heliophysics Event Knowledgebase (HEK) for flare, active-region and coronal-hole event lists
  (`PyThea/utils.py:60-91`, `PyThea/extensions/hek/utils.py:11-70`,
  `test_remote_clients.py:24-58`), and the JPL Horizons ephemeris service via
  `sunpy.coordinates.get_horizons_coord` (`PyThea/utils.py:202,248,263`,
  `PyThea/test/test_utils.py:100`).

*Considered and excluded:* `FTP/FTPS Directories` — despite the `sohoftp.nascom.nasa.gov` hostname the
client uses `https://` only. `CDAWeb`, `HAPI`, `SSCWeb`, `AMDA`, `OMNIWeb`, `Madrigal`, `das2`,
`VirES`, `WDC`, `GFZ`, `TAP`, `S3/Cloud-aware` — no code path touches any of them.

---

### 18. Input File Formats (RECOMMENDED)

- `FITS` — all imaging input. `load_fits()` builds `sunpy.map.Map` objects from downloaded files
  (`PyThea/utils.py:332-366`); the manual-import feature globs `*.fits` and `*.fts`
  (`PyThea/PyThea_app.py:75-81`); every sample-data fixture is a `.fits`/`.fts` file
  (`PyThea/data/sample_data.py`).
- `JSON` — fitting files are read back in via `model_fittings.load_from_json()`
  (`PyThea/utils.py:489-538`; tested at `PyThea/test/test_utils.py:58`), and the local FITS database
  index is JSON (`PyThea/utils_database.py:64-79`).
- `ascii` — the two bundled Fido clients parse plain-text fixed-width archive indices with
  `pandas.read_fwf`: LASCO `img_hdr.txt` (`.../sources/lasco.py:62-66`) and the STEREO
  `SCC<YYYYMM>.img.<detector>` monthly summaries (`.../sources/stereo.py:73-77`).

---

### 19. Output File Formats (RECOMMENDED)

- `JSON` — the only data product the application writes. `model_fittings.to_json()` serialises the
  event, model type, per-time parameter table, kinematic fit method, creation date and PyThea version
  (`PyThea/utils.py:620-642`), offered as "Download Fitting as .json file"
  (`PyThea/PyThea_app.py:638-640`); the FITS-database manager also writes JSON
  (`PyThea/utils_database.py:92-94`).

*Considered and excluded:* `csv` — `PyThea/extensions/buttons.py:44` contains a `to_csv(index=False)`
branch, but `download_button()` in that module is never called anywhere in the package (the app uses
Streamlit's own `st.sidebar.download_button` with JSON), so CSV output is not a supported feature.
Figures are rendered in the browser via `st.pyplot`, not written as data files.

---

### 20. Operating System (RECOMMENDED)

- `Operating System Independent` — `pyproject.toml:21` classifier `Operating System :: OS Independent`
  and `:63` `platforms = ["any"]`. *(Note: `OS Independent` is not a valid HSSI value; the live
  `OperatingSystem` row is `Operating System Independent`.)*
- `Linux` — both CI workflows run on `ubuntu-latest`
  (`.github/workflows/pytest.yml:16`, `.github/workflows/flake8.yml:17`); docs build on
  `ubuntu-lts-latest` (`.readthedocs.yaml:10`).
- `Windows` — explicitly supported and repeatedly fixed: CHANGELOG v0.7.2 "pip installation fails on
  Windows because of non-existing HOME (closed #17)" and v0.7.1 "Fixes a bug with windows install
  (closed #15)"; `setup.py:8-11` uses `pathlib.Path.home()` for exactly this reason.
- `Mac` — pure-Python package with no compiled extensions, covered by the `OS Independent` classifier;
  the installation docs recommend Miniconda/Anaconda and note that Conda "runs on Windows, macOS, and
  Linux" (`docs/source/installing.rst:13`). *Inferred from cross-platform status rather than from a
  macOS test run: the claim rests on the `OS Independent` classifier plus the absence of any compiled
  extension, which is sound evidence of macOS support even though CI does not exercise it.*

---

### 21. CPU Architecture (RECOMMENDED)

- `CPU Independent`

*Source / evidence:* PyThea is pure Python with no compiled extensions, no build step beyond
`setuptools`/`setuptools_scm` (`pyproject.toml:1-7`), and no architecture constraint in any classifier
or dependency pin. No GPU, MPI or HPC code exists. Concrete architectures (`x86-64`, `Apple Silicon
arm64`) are not claimed because the repository provides no per-architecture evidence beyond
`ubuntu-latest` CI runners.

---

### 22. Related Phenomena (OPTIONAL)

- `Coronal Mass Ejections` — the GCS model exists to reconstruct CMEs
  (`PyThea/geometrical_models.py:589`; `README.md:13`).
- `Solar Corona` — the fitted structures are coronal white-light and EUV fronts, imaged by the
  configured coronagraphs and EUV imagers (`docs/source/geometrical_models.rst:9,45`;
  `PyThea/config/selected_imagers.py:13-83`).
- `Solar Flares` — flares are a first-class object in the application: `get_hek_flare()` retrieves the
  GOES-classified flare list used to name and select the event
  (`PyThea/utils.py:60-91`, `PyThea/modules.py:36-129`), `get_hek_flares()` and `plot_hek(mode=
  'Flares')` overlay flare positions on the images (`PyThea/extensions/hek/utils.py:56-69,131+`), and
  fitting files are keyed by flare class (e.g. `FLX1p0D20211028T153500MEllipsoid.json`,
  `PyThea/data/sample_data.py:40-44`).

*Considered and excluded:* `Solar Wind` — an input parameter to the Parker spiral only, not analysed.
`X-ray emission` — GOES soft X-ray class is used as a text label from HEK; no X-ray data is read.
`Coronal Heating`, `Geomagnetic Storms` — unsupported. EUV waves, which PyThea does fit, has no
`Phenomena` row and is therefore carried in Keywords (Field 16) as the vocabulary instructs.

---

### 23. Development Status (RECOMMENDED)

`Active`

*Source / evidence:* `pyproject.toml:19` classifier `Development Status :: 5 - Production/Stable`
(reached a stable, usable state — v1.0.0 was released 2024-12-19 and labelled "This is the first
stable version of PyThea!"), combined with continuing development: three releases since then (v1.1.0
2025-02-12, v1.2.0 2025-10-21, v1.3.0 2026-06-11), the most recent commit 2026-06-11 (~7 weeks before
this extraction), an actively maintained CHANGELOG, and `archived = false` on the GitHub API. That
combination is `Active` (stable **and** actively developed) rather than `Inactive` or `WIP`.

*Release dates above are the authoritative git-tag / GitHub-release dates, not the CHANGELOG's.*
v1.0.0 is tag `2b547bf` dated 2024-12-19 (GitHub release `published_at 2024-12-19T19:32:26Z`);
`CHANGELOG.md:37` reads "19-Nov-2024", the same upstream month/day transposition already documented
for v1.1.0–v1.3.0 under Field 12.

---

### 24. Documentation (RECOMMENDED)

`https://www.pythea.org/en/latest/`

*Source:* byte-identical to `pyproject.toml:47` `Documentation =
"https://www.pythea.org/en/latest/"`. Verified reachable. Built from `docs/source/` by
Sphinx on Read the Docs (`.readthedocs.yaml`); `README.md:97` points users to `https://www.pythea.org/`.

---

### 25. Funder (OPTIONAL)

- **Funder 1**
  - Organization: `National Aeronautics and Space Administration`
  - Funder Identifier: `https://ror.org/027ka1x80`
- **Funder 2**
  - Organization: `European Commission`
  - Funder Identifier: `https://ror.org/00k4n6c32`

*Source / evidence:* only funding attributed to **PyThea's own development** is listed.
- NASA — `README.md:115`: "The lead author of this software package Athanasios Kouloumvakos
  acknowledges financial support from NASA Grant 80NSSC24K0071 for the further development and
  improvement of PyThea during 2024. This grant was part of the NASA Headquarters Heliophysics Tools
  and Methods Program in response to NASA ROSES–2022 (NNH22ZDA001N)." Also the reference
  publication's Funding statement: "…and from NASA NNN06AA01C (SO-SIS Phase-E) contract that allowed
  further improvements and update of the package…". ROR verified via
  `api.ror.org/v2/organizations/027ka1x80` → ror_display `National Aeronautics and Space
  Administration`.
- European Commission — reference publication Funding statement, verbatim: "This study has received
  funding from the European Union's Horizon 2020 research and innovation programme under grant
  agreement No. 101004159 (SERPENTINE). AK acknowledges financial support from the SERPENTINE project
  that allowed to initiate PyThea's development…". ROR verified via
  `api.ror.org/v2/organizations` → `https://ror.org/00k4n6c32` `European Commission`.
  The paper's wording is "the European Union's Horizon 2020 … programme", but `European Commission`
  (ROR `https://ror.org/00k4n6c32`) is the body that signs Horizon 2020 grant agreements and the
  standard funder-registry entity; the literal alternative `European Union`
  (ROR `https://ror.org/019w4f821`) was considered and not chosen.

*Considered and excluded (they fund co-authors' research, not this software):* Spanish Ministerio de
Ciencia, Innovación y Universidades (ESP2017-88436-R, PID2019-104863RB-I00 — L. Rodríguez-García);
Academy of Finland / FORESAIL (312357, 336809 — J. Gieseler, R. Vainio); NASA 80NSSC19K1261 and LWS
80NSSC19K0069 (A. Vourlidas). The same Funding statement also records that at publication time
"Currently, no funding is associated directly with the development of the package" — the NASA
80NSSC24K0071 award in the README post-dates the paper.

---

### 26. Award Title (OPTIONAL)

- **Award 1**
  - Award Title: `Solar EneRgetic ParticlE aNalysis plaTform for the INner hEliosphere (SERPENTINE)`
  - Award Number: `101004159`
- **Award 2**
  - Award Title: `National Aeronautics and Space Administration contract`
  - Award Number: `NNN06AA01C`
- **Award 3**
  - Award Title: `National Aeronautics and Space Administration grant`
  - Award Number: `80NSSC24K0071`

*Source / evidence:*
- Award 1: the SERPENTINE grant referenced in the paper's Funding statement (grant agreement
  No. 101004159); the project title comes from the CORDIS fact sheet for grant 101004159 ("Solar
  EneRgetic ParticlE aNalysis plaTform for the INner hEliosphere", H2020, 2021-01-01 to 2024-06-30).
  Credited with initiating PyThea's development. The title is recorded with its trailing
  ` (SERPENTINE)` to match HSSI's existing award record for grant `101004159` exactly.
- Award 2: reference publication Funding statement (credited with "further improvements and update of
  the package"), which names only the contract: "NASA NNN06AA01C (SO-SIS Phase-E) contract".
- Award 3: `README.md:115`, independently corroborated by the author's own research-projects page
  (`akouloumvakos.spaceweather.gr/projects/`), which records the same ROSES-2022 Heliophysics Tools
  and Methods solicitation (`NNH22ZDA001N-HTM`), PI role and ~2023–2024 duration. Only the grant
  number, the funding programme ("NASA Headquarters Heliophysics Tools and Methods Program") and the
  solicitation are published; neither source gives a distinct formal award title (the personal page
  calls it simply "NASA's Grant HTM-2022: PyThea").

*Award titles for Awards 2 and 3.* No formal title exists for either, and none was invented. Both
follow the descriptive convention HSSI already uses for title-less grants, which spells the agency out
rather than acronymising it — the same wording as HSSI's existing records for grants `80NSSC20K0195`,
`80NSSC20K1786` and `80NSSC22K0061`. Award 3 reuses that wording exactly; Award 2 says `contract`
because the source calls `NNN06AA01C` a contract rather than a grant. The award **number** remains the
identifying value in each case, and neither title is presented as a published formal award title.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- `https://doi.org/10.1086/508254` — Thernisien, A. F. R., Howard, R. A., & Vourlidas, A. (2006).
  *Modeling of Flux Rope Coronal Mass Ejections.* The Astrophysical Journal.
- `https://doi.org/10.1088/0067-0049/194/2/33` — Thernisien, A. (2011). *Implementation of the
  Graduated Cylindrical Shell Model for the Three-dimensional Reconstruction of Coronal Mass
  Ejections.* The Astrophysical Journal Supplement Series.

*Source / evidence:* these are the two publications the project itself designates as the definitive
description of the model it implements — `PyThea/geometrical_models.py:614`: "A full description of the
GCS model is given in Thernisien et al. (2006; doi:10.1086/508254) and Thernisien (2011;
doi:10.1088/0067-0049/194/2/33)", echoed in `docs/source/geometrical_models.rst:45`. Both DOIs were
verified against Crossref (titles, journals, author lists as above).

*Deliberately not padded:* `docs/source/geometrical_models.rst:45` also cites Balmaceda et al. (2020)
and Dumbović et al. (2019) as supporting literature for the model's self-similar expansion, and many
third-party papers use PyThea, but neither group is prioritised by the project as describing or
documenting the software.

---

### 28. Related Datasets (OPTIONAL)

`Not found`

*Note:* PyThea reads mission imaging products (see Fields 31-32) but the repository cites no dataset
DOI or formal dataset citation for any of them. The only dataset-like artifact is the author's
`PyThea-sample-data` GitHub repository of test FITS files
(`PyThea/data/sample_data.py:6`, `https://github.com/AthKouloumvakos/PyThea-sample-data`), which is a
test fixture, not a scientific dataset, and carries no DOI.

---

### 29. Related Software (OPTIONAL)

- `https://doi.org/10.5281/zenodo.4081425` — **GCS in Python** (`gcs_python`), Forstner, J. L.

*Source / evidence:* resolving this DOI (DataCite `10.5281/zenodo.4081425`) gives "GCS in Python" by Johan L.
Forstner — the standalone GCS fitting tool at `https://github.com/johan12345/gcs_python`. The
relationship is *derivation and similarity*, not interoperation: PyThea's GCS class incorporates code
from it under its MIT licence, with the licence vendored into this repository.
- `PyThea/geometrical_models.py:608-613`: "…this class is a reworked and adapted code to python of the
  IDL scripts cmecloud.pro and shellskeleton.pro … **with additions from the GCS in Python package
  that can be found here: https://github.com/johan12345/gcs_python/** that are implemented under the
  MIT License of that package … A copy of this license can be found in PyThea's extensions/ folder."
- `PyThea/geometrical_models.py:726,742,749` mark the specific code blocks taken from
  `gcs_python/gcs/geometry.py`.
- `PyThea/extensions/LICENSE_gcs_python.md` — the vendored MIT licence ("Copyright (c) 2020 Johan von
  Forstner"); added per CHANGELOG v0.7.1.
- `README.md:103` lists it as a "Useful Python package": "An implementation of the Graduated
  Cylindrical Shell model in python."

There is no data exchange, adapter API, plugin relationship or shared data model between the two
packages — they are alternative implementations of the same model, one partly derived from the other.
That is precisely Field 29 ("software that performs similar tasks but does not necessarily link
together … Important software dependencies and software this work was forked from should also be
included") and fails Field 30's demonstrated-exchange bar.

*Recorded here rather than in Field 30*, where it had previously been filed; Field 30 now carries four
entries that each meet the demonstrated-exchange bar.

*Considered and excluded:* other 3D CME reconstruction tools (e.g. IDL `scraytrace`) are cited only as
the origin of the algorithm, not as software the project relates itself to; the SolarSoft
`scraytrace` IDL package (`geometrical_models.py:609,613`) has no DOI or public repository URL to
record and is already accounted for by the Thernisien publications in Field 27.

---

### 30. Interoperable Software (OPTIONAL)

- `https://doi.org/10.5281/zenodo.591887` — **sunpy**
  *Evidence of exchange (plugin/extension + shared data model):* PyThea's data model **is** sunpy's —
  every image is a `sunpy.map.GenericMap` / `MapSequence` and every public utility takes and returns
  them (`PyThea/utils.py:332-366`, `PyThea/sunpy_dev/map/maputils.py` throughout). More strongly,
  PyThea *extends* sunpy: `LASCOClient` and `STEREOClient` subclass
  `sunpy.net.dataretriever.GenericClient` and register new `Instrument`/`Source`/`Provider`/`Detector`
  attribute values into sunpy's Fido registry
  (`PyThea/sunpy_dev/net/dataretriever/sources/lasco.py:1-11,80-87`, `.../stereo.py:1-11,91-100`),
  which the application activates at runtime (`PyThea/PyThea_app.py:145-148`). `README.md:107`:
  "_PyThea_ has a strong dependency on SunPy and AstroPy Python packages, consider citing these
  packages as well." Hard dependency `sunpy>=7.1.2` (`pyproject.toml:31`).
- `https://doi.org/10.5281/zenodo.4016980` — **aiapy**
  *Evidence of exchange:* PyThea hands sunpy `AIAMap` objects to `aiapy.calibrate.update_pointing` and
  consumes the corrected maps back into its own pipeline
  (`PyThea/sunpy_dev/extern/sunkit_instruments/aia/utils.py:3,10-14`, dispatched from
  `PyThea/sunpy_dev/map/maputils.py:207-208`). Declared dependency (`pyproject.toml:35`). This is a
  concrete two-way exchange over the shared sunpy data model, not incidental use.
- `https://doi.org/10.5281/zenodo.7595725` — **sunpy-soar**
  *Evidence of exchange (plugin relationship):* imported specifically to register the SOAR client and
  its `a.soar.Product` attribute into sunpy's Fido, which PyThea's Solar Orbiter imager definitions
  then query (`PyThea/config/selected_imagers.py:8` `import sunpy_soar  # noqa`, `:77-90`
  `a.soar.Product('EUI-FSI174-IMAGE')`, `a.soar.Product('METIS-VL-TB')`,
  `a.soar.Product(f'SOLOHI-{tile}F{z}')`); the remote test asserts the SOAR client actually answers
  (`PyThea/test/test_remote_clients.py:113-129`, `assert 'soar' in result.keys()`). Declared
  dependency (`pyproject.toml:40`).
- `https://doi.org/10.5281/zenodo.4670728` — **Astropy** *(Tier B — cited evidence)*
  *Evidence of exchange:* `astropy.coordinates.SkyCoord` and `astropy.units.Quantity` are the
  *documented interchange format* of PyThea's public API, not internal plumbing: the model classes take
  a `SkyCoord` centre and `u.R_sun`/`u.degree` quantities and their `coordinates`,
  `intersecting_curve`, `apex` and `base` members return `SkyCoord`
  (`PyThea/geometrical_models.py:91-131`, `:244-278`, `:450-495`, `:618-671`), enforced by
  `@u.quantity_input` annotations (`:167,205,522,543,636`). The documented usage examples build models
  from `SkyCoord`s and plot the returned `SkyCoord`s
  (`docs/source/examples/Utilites/construct_geometrical_model.py`,
  `docs/source/utilities.rst:125-144`). `README.md:102,107` names AstroPy explicitly and asks users to
  cite it.

*Tier A exclusions (dependencies, not interoperability) — recorded for the audit trail:* `numpy`,
`scipy`, `pandas`, `matplotlib`, `seaborn`, `streamlit`, `pyvista`, `numexpr`, `click`, `pooch`,
`jplephem`, `pytest` / `pytest-astropy` / `pytest-sugar` / `pytest-mpl`, `sphinx` and its extensions,
`setuptools` / `setuptools_scm`, `plotly` (docs extra only). Each is generic infrastructure that would
be equally at home in a web app, a finance model or a biology pipeline; `pyvista` in particular is
used only for a mesh-intersection calculation (`geometrical_models.py:463-470`).
*Also excluded:* `sunkit-instruments` — `PyThea/sunpy_dev/extern/sunkit_instruments/` mirrors that
package's directory layout (suggesting the code is intended for upstreaming) but the package is
neither imported nor declared as a dependency, so there is no exchange to cite.

---

### 31. Related Instruments (OPTIONAL)

Every entry below resolves to exactly one instrument row in HSSI's controlled
instrument/observatory vocabulary, and every `identifier` is a `https://spase-metadata.org/` SPASE
identifier. Names are copied verbatim from the matched rows. There are no unresolved or ambiguous
entries in this field.

The governing evidence is `PyThea/config/selected_imagers.py`, which enumerates every imager the
application can search, download, calibrate, process and fit models to, together with per-imager
detector, wavelength, dimension, polarisation and superpixel configuration.

| Instrument Name (verbatim) | Instrument Identifier | In-repo evidence |
|---|---|---|
| Large Angle Spectroscopic Coronagraph | `https://spase-metadata.org/SMWG/Instrument/SOHO/LASCO` | `selected_imagers.py:13-19` (`LC2`, `LC3`: `a.Instrument.lasco` + `a.Detector.c2`/`c3`); `maputils.py:284-291` C2/C3 occulter geometry; `.../lasco/utils.py` prep; `.../sources/lasco.py` NASCOM client |
| Atmospheric Imaging Assembly | `https://spase-metadata.org/SMWG/Instrument/SDO/AIA` | `selected_imagers.py:21-27` (`AIA-193`, `AIA-211`); `.../aia/utils.py` aiapy prep; `maputils.py:207-208`; figure tests `test_figures.py:46,71` |
| Stereo-A Sun Earth Connection Coronal and Heliospheric Investigation | `https://spase-metadata.org/SMWG/Instrument/STEREO-A/SECCHI` | `selected_imagers.py:29-67` (`'instrument': 'SECCHI'` on every STEREO-A imager); `.../sources/stereo.py:95` registers `attrs.Instrument: [('SECCHI','')]` |
| Stereo-B Sun Earth Connection Coronal and Heliospheric Investigation | `https://spase-metadata.org/SMWG/Instrument/STEREO-B/SECCHI` | same, STEREO-B side (`selected_imagers.py:33,41,49,57,65`) |
| STEREO-A SECCHI Cor1 Coronagraph | `https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/Cor1` | `selected_imagers.py:45-47`; polarisation inversion `.../stereo/utils.py:11-104`; occulter `maputils.py:278-280` |
| STEREO-B SECCHI Cor1 Coronagraph | `https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/Cor1` | `selected_imagers.py:49-51`; figure test `test_figures.py:96` |
| STEREO-A SECCHI Cor2 Coronagraph | `https://spase-metadata.org/SMWG/Instrument/STEREO-A/SECCHI/Cor2` | `selected_imagers.py:29-31`; occulter `maputils.py:281-283`; figure test `test_figures.py:136` |
| STEREO-B SECCHI Cor2 Coronagraph | `https://spase-metadata.org/SMWG/Instrument/STEREO-B/SECCHI/Cor2` | `selected_imagers.py:33-35` |
| Extreme UltraViolet Imager on the STEREO-A mission | `https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/EUVI` | `selected_imagers.py:37-39` (195 Å); calibration `.../stereo/utils.py:107-155`; `maputils.py:212-213` |
| Extreme UltraViolet Imager on the STEREO-B mission | `https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/EUVI` | `selected_imagers.py:41-43`; STEREO_B-specific dejitter sign flip `.../stereo/utils.py:143-144` |
| Heliospheric Imager-1 Telescope on the STEREO-A mission | `https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/HI-1` | `selected_imagers.py:53-55` |
| Heliospheric Imager-1 Telescope on the STEREO-B mission | `https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/HI-1` | `selected_imagers.py:57-59` |
| Heliospheric Imager-2 Telescope on the STEREO-A mission | `https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/HI-2` | `selected_imagers.py:61-63` |
| Heliospheric Imager-2 Telescope on the STEREO-B mission | `https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/HI-2` | `selected_imagers.py:65-67` |
| PSP WISPR | `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/WISPR` | `selected_imagers.py:69,73` query `a.Instrument.wispr`; instrument-specific figure handling `PyThea/utils.py:131,150`, `maputils.py:315-319` |
| Parker Solar Probe, PSP, Wide-field Imager for Solar Probe, WISPR, Suite, Inner Telescope, IT, Instrument | `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/WISPR/InnerTelescope` | `selected_imagers.py:69-71` (`a.Detector.inner`, L3, 960×1024); figure test `test_figures.py:200` |
| Parker Solar Probe, PSP, Wide-field Imager for Solar Probe, WISPR, Suite, Outer Telescope, OT, Instrument | `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/WISPR/OuterTelescope` | `selected_imagers.py:73-75` (`a.Detector.outer`); figure test `test_figures.py:235` |
| Extreme Ultraviolet Imager | `https://spase-metadata.org/ESA/Instrument/SolarOrbiter/EUI` | `selected_imagers.py:77-79` (`a.Instrument('EUI')`, `a.soar.Product('EUI-FSI174-IMAGE')`, L2); SOAR remote test `test_remote_clients.py:107-129` |
| Metis | `https://spase-metadata.org/ESA/Instrument/SolarOrbiter/Metis` | `selected_imagers.py:81-83` (`a.soar.Product('METIS-VL-TB')`); special title/clim handling `PyThea/utils.py:131,157-160`, `maputils.py:320-321` |
| The Solar Orbiter Heliospheric Imager | `https://spase-metadata.org/NASA/Instrument/SolarOrbiter/SoloHI` | `selected_imagers.py:85-90` (tiles T1-T4, `a.soar.Product('SOLOHI-{n}F{T|G}')`); title/clim handling `PyThea/utils.py:131,155-156`, `maputils.py:322-323` |

*Resolution notes (SPASE ladder):*
- **Rule 1 (single match):** LASCO, AIA, EUI, Metis, SoloHI, and each of the ten STEREO/SECCHI
  detector rows and two WISPR telescope rows matched exactly one `type = 1` row.
- **Rule 2 (evidence-backed multi-row expansion):** SECCHI and WISPR each have per-spacecraft /
  per-telescope rows, and `selected_imagers.py` enumerates precisely which ones — STEREO-**A** *and*
  STEREO-**B** for all five SECCHI telescopes (`a.Source('STEREO_A')` / `a.Source('STEREO_B')` on
  lines 29-67, confirmed by `.../sources/stereo.py:96` registering both sources), and WISPR
  **Inner** *and* **Outer** (`a.Detector.inner` / `a.Detector.outer`, lines 69-75). The suite-level
  rows are listed alongside the detector rows because the code queries the suite by name
  (`'instrument': 'SECCHI'`, `a.Instrument.wispr`, `attrs.Instrument: [('SECCHI','')]`), so a user
  searching HSSI for `instrument:"SECCHI"` or `instrument:"WISPR"` — the abbreviations carried only by
  those suite rows — should find PyThea.
- **`.html` normalisation:** `SMWG/Instrument/SDO/AIA` was preferred over the duplicate
  `SMWG/Instrument/SDO/AIA.html` ("Atmospheric Imaging Assembly (AIA)"). A third `AIA` abbreviation
  collision — `IUGONET/Instrument/WDC_Kyoto/WDC/AIA/Magnetometer`, "Magnetometers at Argentine
  Island" — was correctly rejected on type/context.
- **Not applicable:** no entry needed Rule 3 (ambiguity flag), Rule 4 (observatory fallback) or Rule 5
  (omission) — every supported imager has its own SPASE instrument row.

*Considered and excluded from Field 31 (audit trail):*
- **GOES** — `PyThea/utils.py:83` filters the HEK flare list with `a.hek.OBS.Observatory == 'GOES'`
  and displays `fl_goescls`. PyThea never reads GOES data; it consumes a multi-mission event catalogue
  that happens to report GOES flare classes. That is a Data Source / event-context use, not
  designed-to-support (see Field 17 `Other`).
- **HMI** — `a.hek.FRM.Name == 'HMI SHARP'` (`PyThea/extensions/hek/utils.py:19`) selects an HEK
  active-region *feature-recognition method* name; no HMI data is read.
- **SDO/AIA 1600 Å** — appears only as a figure-test fixture; not a configured imager, so it adds no
  instrument beyond AIA itself.

---

### 32. Related Observatories (OPTIONAL)

All seven entries resolved to `type = 2` rows carrying `https://spase-metadata.org/` identifiers.
Names are verbatim from the matched rows.

| Observatory Name (verbatim) | Observatory Identifier | Evidence |
|---|---|---|
| Solar and Heliospheric Observatory | `https://spase-metadata.org/SMWG/Observatory/SOHO` | `selected_imagers.py:15,19` `'source': 'SOHO'`; `.../lasco/utils.py:14` `get_horizons_coord('SOHO', …)`; `.../sources/lasco.py:84` registers `attrs.Source: [('SOHO','')]` |
| Solar Dynamics Observatory | `https://spase-metadata.org/SMWG/Observatory/SDO` | `selected_imagers.py:23,27` `'source': 'SDO'` (AIA 193/211); CHANGELOG v0.12.0 "Adds more imaging data from SDO/AIA" |
| Solar-Terrestrial Relations Observatory | `https://spase-metadata.org/SMWG/Observatory/STEREO` | `selected_imagers.py:92-95` `providers['STEREO']` groups all ten STEREO imagers; `README.md:13` |
| Solar Terrestrial Relations Observatory A | `https://spase-metadata.org/SMWG/Observatory/STEREO-A` | `selected_imagers.py:29,37,45,53,61` `a.Source('STEREO_A')`, `'source': 'STEREO_A'`; `.../sources/stereo.py:61-62,96` |
| Solar Terrestrial Relations Observatory B | `https://spase-metadata.org/SMWG/Observatory/STEREO-B` | `selected_imagers.py:33,41,49,57,65` `a.Source('STEREO_B')`; `.../stereo/utils.py:143` STEREO_B-specific dejitter; `.../sources/stereo.py:63-64,96` |
| Parker Solar Probe | `https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe` | `selected_imagers.py:71,75` `'source': 'PSP'`; CHANGELOG v0.13.0 "Adds imaging data from PSP/WISPR"; `README.md:13` |
| Solar Orbiter | `https://spase-metadata.org/ESA/Observatory/SolarOrbiter` | `selected_imagers.py:79,83,90` `'source': 'SOLO'`; CHANGELOG v0.14.0 "Adds imaging data from Solar Orbiter EUI and METIS", v1.0.0 "Adds imaging data from Solar Orbiter's SOLOHi" |

*Resolution notes (SPASE ladder):*
- **Two of these names are ambiguous in the vocabulary, so the identifier is what fixes the binding.**
  Three rows are named exactly `Parker Solar Probe` (`CNES/Observatory/CDPP-AMDA/PSP`,
  `CNES/Observatory/CDPP-Archive/PSP`, `SMWG/Observatory/ParkerSolarProbe`) and two exactly
  `Solar and Heliospheric Observatory` (`CNES/Observatory/CDPP-AMDA/SOHO`, `SMWG/Observatory/SOHO`);
  `Solar-Terrestrial Relations Observatory` is unique (`SMWG/Observatory/STEREO`). A name-only
  association would bind arbitrarily among same-name rows, so each entry above carries its explicit
  SPASE identifier.
- **SMWG tie-breaker** applied to SOHO, PSP and the three STEREO rows: the `CNES/Observatory/CDPP-*`
  rows are archive-scoped duplicates of the same missions (`CDPP-AMDA/STEREO`,
  `CDPP-Archive/STEREO-A`, `CDPP-AMDA/STEREO-B`, `CDPP-AMDA/SolO`, …) and are deprioritised.
- **Solar Orbiter** has two same-name rows and neither is `SMWG`: `ESA/Observatory/SolarOrbiter` and
  `CNES/Observatory/CDPP-AMDA/SolO`. `ESA/Observatory/SolarOrbiter` is selected — it is the mission's
  own authoritative record (and the identifier the field-definitions guidance names for Solar
  Orbiter), it is path-consistent with the two Solar Orbiter instrument rows also selected here
  (`ESA/Instrument/SolarOrbiter/EUI`, `ESA/Instrument/SolarOrbiter/Metis`), and the alternative is the
  same archive-scoped CNES/CDPP family already deprioritised above. The evidence supports the selected
  row without a remaining Rule 3 ambiguity.
- **Rule 2 (evidence-backed expansion):** the mission-level STEREO row is recorded alongside both
  spacecraft rows, because the code targets each spacecraft individually
  (`a.Source('STEREO_A')` / `a.Source('STEREO_B')` for all five SECCHI telescopes, plus a
  STEREO_B-specific calibration branch). Nothing was inferred.
- **No omissions and no observatory fallbacks were needed in this field.**

*Considered and excluded:* **GOES** (HEK flare-catalogue filter only — see Field 31);
**BepiColombo**, **Mercury/Venus/Earth/Mars/Jupiter** (`PyThea/config/selected_bodies.py`) — these are
JPL Horizons ephemeris targets whose *positions* are plotted for viewing geometry; PyThea reads no
BepiColombo data, so it is not designed to support that mission. Note that STEREO-A/B, Solar Orbiter
and Parker Solar Probe also appear in `selected_bodies.py`, but they are listed above on the strength
of their imager support, not their ephemeris entries.

---

### 33. Logo (OPTIONAL)

`https://raw.githubusercontent.com/AthKouloumvakos/PyThea/f5bc63e11335b2fdaa0d49bc482083c65c8875bb/docs/logo/pythea_logo.png`

*Source:* verified reachable and served as `image/png`. The file exists in the
repository at `docs/logo/pythea_logo.png` and is the logo the project itself points to
(`README.md:11,107`, `PyThea/PyThea_app.py:105`). SoMEF independently reported the same asset. The URL
is pinned to the commit above rather than to the default branch that upstream and SoMEF reference, so
no rename or move upstream can silently break it.

---

## Record notes

**Corrections applied 2026-07-30** (each documented in its field above, with evidence):

| Field | Correction |
|---|---|
| 2 Persistent Identifier | repointed from the abandoned first Zenodo deposit to PyThea's active concept DOI |
| 6 Authors | affiliation replaced with the author's current institution, Johns Hopkins University Applied Physics Laboratory |
| 7 Software Name | long citation title replaced by the concise product name `PyThea` |
| 8 Description | refreshed to current upstream wording, plus one editorial sentence recording SDO and Solar Orbiter support |
| 9 Concise Description | mid-word truncation replaced with a complete sentence |
| 12 Version | refreshed from v0.4.0 to v1.3.0 (2026-06-11) with its release DOI and change summary |
| 29 / 30 | `gcs_python` recorded as related rather than interoperable software; Field 30 rebuilt around demonstrated exchanges |

Fields 4, 5, 14, 16–23, 25–27, 31 and 32 were substantially expanded from empty or minimal values.
Fields 3, 10, 11, 13, 15 and 24 were already correct and are unchanged. Field 33 names the same logo
asset it always did, now recorded as a commit-pinned raw URL instead of a branch reference. Field 28 is empty because
PyThea cites no dataset DOI.

**Upstream data quirks worth remembering.** `CHANGELOG.md` mis-dates several releases — v1.0.0 as
"19-Nov-2024" and v1.1.0, v1.2.0 and v1.3.0 all as "12-Feb-2025"; the git tags, PyPI uploads and
Zenodo records are authoritative and were used instead. Two Zenodo concept DOIs exist for PyThea (see
Field 2). The long citation title is upstream's `description`/`summary`, not its package name (Field 7).
