# HSSI Metadata Extraction Results

**HSSI Software ID:** 2979f7e7-b34d-4f16-8c96-966d7a2a1f01
**Repository:** https://github.com/space-physics/astrometry_geomap
**Source Revision:** cbe04e58bdd267cdb03517c480e9cfcb3011aef8
**Extraction Date:** 2026-08-29
**Validation Date:** 2026-08-29
**Validation Status:** PASS

---

**Scope note.** All in-repository evidence below is drawn from the pinned revision
`cbe04e58bdd267cdb03517c480e9cfcb3011aef8` (tag `v1.4.1`, 2026-07-09, branch `main`). This matters
because the July 2026 release reworked the package substantially: it dropped `python-dateutil`,
raised the Python floor to 3.10, added a `python -m astrometry_azel` entry point, and widened
continuous integration to macOS. An earlier dossier for this software described the 2024-02-05 tree
and several of its statements no longer hold; where a value here supersedes that earlier reading, the
reason is recorded with the field.

Two naming facts recur throughout and are stated once here. The GitHub repository is
`astrometry_geomap`; the installable Python package inside it is `astrometry_azel`
(`pyproject.toml` `name`); the registry and HSSI name is `AstrometryAzEl`. The repository was renamed
from `astrometry_azel`, and `https://github.com/space-physics/astrometry_azel` still redirects to the
current location.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This placeholder is the catalogue convention for a record whose HSSI metadata was contributed
without an identified individual submitter. It is not a missing value to be repaired by guessing.

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.595450

Zenodo concept DOI, covering all versions. Confirmed against the Zenodo REST API
(`https://zenodo.org/api/records/595450`), which reports `conceptdoi: 10.5281/zenodo.595450`,
`conceptrecid: 595450`, and as of 2026-08-29 resolved the concept record to version `v1.4.1`
(record 21280344). DataCite carries the same DOI with `relationType: IsVersionOf`.

**Trap for a future refresh.** The README's DOI badge points at
`https://doi.org/10.5281/zenodo.4527817`, which is the *version* DOI for v1.3.0, not the concept DOI.
A badge-driven extraction would record the wrong identifier here. The concept DOI is the correct
Field 2 value; the current version DOI belongs in Field 12.

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/space-physics/astrometry_geomap

The repository root. Confirmed live via the GitHub API (`full_name: space-physics/astrometry_geomap`,
`default_branch: main`, `archived: false`).

The PyHC registry entry still lists the pre-rename URL
`https://github.com/space-physics/astrometry_azel`
(`https://github.com/heliophysicsPy/heliophysicsPy.github.io/blob/main/_data/projects_unevaluated.yml`).
That URL redirects, but the post-rename URL above is the durable one and is what belongs here.

### 4. Software Functionality (RECOMMENDED)
- **Values:**
  - Coordinate Transforms
  - Data Processing and Analysis
  - Data Processing and Analysis: Calibration
  - Data Processing and Analysis: Data Access and Retrieval
  - Data Processing and Analysis: Data Reduction
  - Data Processing and Analysis: File Format Conversion
  - Data Processing and Analysis: Image Processing
  - Data Visualization
  - Data Visualization: 2D Graphics

These nine values carry over from the existing HSSI record; the evidence below confirms each of them
against the pinned revision. A tenth, `Data Processing and Analysis: Analysis`, was considered and
declined; see *Considered and rejected*.

**Evidence per value.**

- **Coordinate Transforms** — the package's central purpose. `radec2azel()` and the helper
  `pymap3d_radec2azel()` in `src/astrometry_azel/__init__.py` convert celestial right
  ascension/declination to local horizon azimuth/elevation for every pixel, using an
  `astropy.coordinates.AltAz` frame anchored to an `EarthLocation` and an observation `Time`.
  `project.image_altitude()` performs a second transform, azimuth/elevation plus slant range to
  WGS-84 geodetic latitude/longitude, via `pymap3d.aer2geodetic()`.
- **Data Processing and Analysis: Calibration** — astrometric plate-scale calibration is the
  headline capability. `doSolve()` invokes Astrometry.net's `solve-field` to fit a WCS solution to a
  star field; the GitHub repository description reads "FITS to Azimuth/Elevation using
  Astrometry.net--calibrate and plate scale images".
- **Data Processing and Analysis: Data Access and Retrieval** — `src/astrometry_azel/download/__main__.py`
  is a user-facing downloader (`python -m astrometry_azel.download`) that retrieves Astrometry.net
  star index files over HTTP from `https://data.astrometry.net/4200/` (2MASS) and
  `https://data.astrometry.net/4100/` (Tycho) via `urllib.request.urlretrieve`.
- **Data Processing and Analysis: Data Reduction** — `io.meanstack()` and `io.collapsestack()`
  collapse multi-frame image stacks by mean or median; the module docstring states the purpose
  explicitly ("Averaging a selected stack of images improves SNR for astrometry.net").
  `scripts/AverageImageStack.py` is the CLI wrapper.
- **Data Processing and Analysis: File Format Conversion** — `project.plate_scale()` converts an
  arbitrary input image to FITS (`io.load_image()` then `io.write_fits()`) so that `solve-field` can
  consume it, and writes the result as netCDF4 (`io.write_netcdf()`).
- **Data Processing and Analysis: Image Processing** — `io.rgb2grey()` performs luminance conversion
  including RGBA alpha handling; `plot.wcs_image()` warps an image into sky coordinates through its
  WCS solution using `pcolormesh`; `scripts/LocateCrop.py` uses `skimage.feature.match_template`.
- **Data Visualization** and **Data Visualization: 2D Graphics** — `plot/__init__.py` produces
  contour overlays of azimuth/elevation and RA/declination on the image
  (`az_el()`, `ra_dec()`), grayscale/RGB image displays with colorbars (`image_stack()`), and
  WCS-warped `pcolormesh` renderings (`wcs_image()`, `xy_image()`).
  `plot/project.py geomap()` draws a Cartopy `PlateCarree` geographic map with coastlines, borders,
  state/province lines and place annotations. All output is two-dimensional raster and contour
  graphics.

**Considered and rejected.**

- **Every `Coordinate Transforms` subcategory.** The six available children are Heliospheric,
  Ionospheric, Magnetospheric, Mission-Specific, Planetary and Solar. All six name space-physics
  magnetic, solar or spacecraft reference frames. This software transforms between celestial
  (RA/Dec), local horizon (Az/El) and terrestrial geodetic (WGS-84 lat/lon) frames, none of which any
  child covers — in particular, `Ionospheric` covers magnetic coordinate systems such as AACGM,
  magnetic local time and apex coordinates, which the package does not compute. The bare parent
  standing alone is therefore the correct and complete classification, not an oversight.
- **Two `Data Processing and Analysis` children are declined for one shared reason: each would
  restate a capability the selected values already carry.** A subcategory earns its place by naming
  something no other selected value asserts; one that only re-labels an already-asserted capability
  widens search matches without adding information about the software. The same double-counting test
  decides both of the following.

  - **Data Processing and Analysis: Analysis.** The two functions that make the case for this row are
    each already asserted elsewhere in the field. `project.image_altitude()` does derive a geophysical
    quantity rather than reformatting one — the geodetic ground footprint of each image pixel under an
    assumed single emission altitude, computed with a secant slant-range approximation
    (`slant_range_m = projection_altitude_km * 1e3 / sin(radians(elevation))`), which is the aeronomy
    technique the README's "PlotGeomap.py" section and the `PlotGeomap.py` docstring describe. But the
    derivation it performs is a frame conversion — azimuth/elevation plus slant range to WGS-84
    geodetic latitude/longitude via `pymap3d.aer2geodetic()` — and `Coordinate Transforms` already
    asserts precisely that. `scripts/LocateCrop.py` likewise produces an analytic result, the pixel
    offset of a cropped image within its original by normalized cross-correlation
    (`skimage.feature.match_template`), and `Data Processing and Analysis: Image Processing` already
    asserts that. The supporting evidence is preserved here rather than discarded, so a future agent
    can see what was weighed; what it does not show is a capability the selected values leave
    unstated.

  - **Data Processing and Analysis: Processing.** The processing this package performs is covered by
    the more specific siblings already selected — Calibration, Data Reduction, Image Processing and
    File Format Conversion. The generic child would likewise broaden search matches without naming a
    capability those siblings leave unasserted.
- **Models and Simulations** and its children. The single-emission-altitude assumption is a
  geometric approximation applied to observed imagery, not a model of a physical system: the altitude
  is a required user-supplied CLI argument (`PlotGeomap.py projection_altitude_km`), and no physics is
  solved or simulated. `Empirical` and `Physics-Based` are the plausible-looking traps here; both
  would misrepresent the package.
- **Data Visualization: Line Plots, Movies, 3D Graphics.** No one-dimensional line plot, animation
  export or three-dimensional rendering exists in `plot/__init__.py` or `plot/project.py`.
  `scripts/AverageImageStack.py` *reads* animated GIF and multi-page TIFF stacks but writes still
  PNG frames, so it is frame reduction rather than movie generation.
- **Mission-related** and **Servers and Environments** in all forms. The package is not part of any
  mission ground system and provides no server, container or deployment functionality.

### 5. Related Region (RECOMMENDED)
- **Values:**
  - Earth Atmosphere
  - Earth Auroral Subregion

The Region vocabulary is flat: no row implies any other, so each row has to earn its place on
independent evidence rather than inherit it from a broader or narrower neighbour. That principle
selects the two values above, and it is also what excludes the neighbouring atmospheric rows
discussed under *Considered and rejected*.

- **Earth Atmosphere** — the projection altitude is a free user parameter
  (`PlotGeomap.py projection_altitude_km`), so the software's geographic mapping is not confined to
  one atmospheric layer. The generic row is accurate for that reason.
- **Earth Auroral Subregion** — aurora is the software's named science application. `pyproject.toml`
  lists `aurora` among its keywords; the README's "PlotGeomap.py" section describes the technique as
  used "in aeronomy assuming a certain altitude of auroral or airglow emissions"; the PyHC registry
  description is "plate scale / calibrate star imagery to use multiple auroral/airglow cameras
  together"; and `download/__main__.py` describes its index-file defaults as tuned for "auroral
  imagers".

**How the PyHC bucket is read.** PyHC classifies this entry under the compound label
`ionosphere_thermosphere_mesosphere`, recorded at
`https://github.com/heliophysicsPy/heliophysicsPy.github.io/blob/main/_data/projects_unevaluated.yml`
under the `AstrometryAzEl` entry (`keywords: ["ionosphere_thermosphere_mesosphere","specific"]`).
That label is a single atomic term in PyHC's own taxonomy, not three independent regional assertions,
and it is read that way consistently throughout this record. It corroborates the general
upper-atmosphere domain of the software; it does not select any individual Region row, and it is not
cited below as support for the ionosphere, the thermosphere or the mesosphere.

**Considered and rejected.**

- **Earth Ionosphere and Earth Thermosphere.** Both rows were argued in detail and both are declined,
  for one reason that applies equally to each. The case for them rested on a single shared anchor: the
  README's one worked altitude, "if a short wavelength filter (blue) was applied to the auroral image,
  one might assume the emissions were at about 100 km altitude". That figure genuinely admits both
  readings — 100 km lies in the lower thermosphere, and it is also the ionospheric E region where the
  auroral emissions this software geolocates are excited — but that is the difficulty rather than the
  justification. Because the vocabulary is flat, each row needs evidence of its own, and one
  documentation sentence cannot supply independent support for two separate regional assertions.
  The code settles it: the package computes no ionospheric or thermospheric quantity. It geolocates
  image pixels under a projection altitude the user is required to supply
  (`PlotGeomap.py` takes `projection_altitude_km` as a positional argument, passed straight into
  `project.image_altitude()`), so the ~100 km figure illustrates how to use that parameter rather than
  describing a region the software works in. Consistent with this, neither "ionosphere" nor
  "thermosphere" appears anywhere in the repository's own files at the pinned revision; both terms
  reach this record only through the external PyHC bucket, which is read atomically above.
  The evidence is preserved here rather than discarded so a future agent can see exactly what was
  weighed and can revisit it on new grounds: should the upstream documentation ever state a worked
  case that anchors one of these regions on its own — an ionospheric or thermospheric quantity
  actually computed, or a specified emission layer rather than a user-chosen altitude — that row
  becomes a defensible addition on its own merits.
- **Earth Lower and Middle Atmosphere.** The mesosphere is named in none of the repository's files at
  this revision; it reaches this record only through the PyHC compound label, which for the reason
  given above corroborates the general upper-atmosphere domain without selecting this row. The
  repository's single altitude example (~100 km) sits above the mesopause. A user projecting an
  OH-layer airglow image near 87 km would make this row applicable, and if the documentation ever
  states such a case the row becomes a defensible addition; as of this revision it is not evidenced.
- **The magnetospheric, solar, heliospheric and planetary rows.** The software operates on
  ground-based optical imagery of Earth's upper atmosphere. No file in the repository at this revision
  refers to magnetospheric, solar or interplanetary regions.

### 6. Authors (MANDATORY)
- **Author:** Michael Hirsch
  - **Author Identifier:** https://orcid.org/0000-0002-1637-6526
  - **Affiliations:**
    - Boston University — https://ror.org/05qwgg493
    - Scivision, Inc. — no ROR

Sole author. Across the 177 commits in the pinned revision's ancestry, the commit-author names vary
between `scivision`, `Michael Hirsch, Ph.D`, `Michael Hirsch` and `irs4`, but only two author email
addresses appear, and both are GitHub noreply forms for the single account `scivision`:
`scivision@users.noreply.github.com` (176 commits) and its ID-prefixed form
`10931741+scivision@users.noreply.github.com` (1 commit).
The PyHC registry gives `contact: Michael Hirsch`.

A caution for anyone re-deriving this. The clone also contains commits that are *not* ancestors of
the pinned revision, reachable only through tags left on lineages predating a history rewrite.
`git log --all` therefore reports a wider set of author addresses than the released history has —
among them an older `scienceopen@users.noreply.github.com` form, consistent with a GitHub account
rename, and a few generic `nobody@` addresses. Those commits are not part of the history this record
describes, and the wider address list is not evidence of additional authors. Scope the check to the
revision (`git log <revision>` or `git rev-list <revision>`) rather than to every ref in the clone.

The ORCID record `0000-0002-1637-6526` names Michael Hirsch and lists a Boston University employment
(Research Scientist, department "ECE", from 2018-08) plus Boston University degrees, corroborating the
Boston University affiliation. `LICENSE.txt` reads "Copyright 2020 SciVision, Inc.", which is the
in-repository evidence for the Scivision affiliation.

**Do not take the author name from the DOI metadata.** Both Zenodo and DataCite record the creator of
this software as `scivision` with `familyName: "scivision"` — the GitHub username, not a personal
name. An extraction that trusts DataCite here will corrupt the author record.

**Negative research on the Scivision ROR.** A ROR API query for "Scivision"
(`https://api.ror.org/organizations?query=Scivision`) returns a single unrelated organization,
`SciVision Biotech Inc. (Taiwan)`, `https://ror.org/011qev639`, a Kaohsiung company. That ROR must not
be attached to this affiliation. Michael Hirsch's Scivision, Inc. has no ROR record; the affiliation
is correctly stored without an identifier.

**Department not used.** The ORCID employment names the department "ECE". No Boston University
department row existed in HSSI's organization table when this record was compiled, and the
institution-level name "Boston University" carries the ROR, so the institution name is the right
value.

An earlier dossier for this software recorded "Author Identifier: Not found" and "Affiliation: Not
found". Both were wrong: the ORCID and both affiliations are recoverable from the sources above.

### 7. Software Name (MANDATORY)
- **Value:** AstrometryAzEl

This is the registry name (`name: AstrometryAzEl` in PyHC's `projects_unevaluated.yml`) and the name
under which the software is known in HSSI. Alternative forms in circulation are the Python package
name `astrometry_azel` (`pyproject.toml`) and the repository name `astrometry_geomap`.

**Corrected claim.** An earlier dossier described `astrometry_azel` as the "package and PyPI name".
There is no PyPI distribution. `astrometry-azel`, `astrometry_azel`, `astrometry-geomap` and
`astrometry_geomap` each return HTTP 404 from both authoritative PyPI endpoints,
`https://pypi.org/pypi/<name>/json` and `https://pypi.org/simple/<name>/` (a `numpy` control on the
same endpoint returns 200, confirming the probe works). The README's only installation route is
`pip install -e ./astrometry_geomap` from a git clone, and the revision pinned here removed the
README's PyPI version and downloads badges. Do not reintroduce a PyPI reference for this software
without re-checking those two endpoints — the rendered HTML project page on pypi.org returns 200 even
for names that do not exist and cannot be used to establish existence.

### 8. Description (MANDATORY)
- **Value:** Register images to geographic maps using the astrometry.net program. This software performs plate scale calibration of star imagery to enable use of multiple auroral and airglow cameras together. It converts FITS images to azimuth/elevation coordinates using Astrometry.net, with applications in aeronomy for studying aurora and airglow emissions. The software assumes emissions occur at a specified altitude, typically about 100 km for auroral observations, and projects images onto geographic coordinates.

Composed from `pyproject.toml`'s `description` ("Register images to geographic maps using the
astrometry.net program", still verbatim at this revision), the PyHC registry description, and the
README. Its claims hold at the pinned revision: FITS-to-azimuth/elevation conversion
(`fits2azel()`), the assumed single emission altitude with ~100 km as the auroral example (README,
"PlotGeomap.py" section), and geographic projection (`project.image_altitude()` plus
`plot/project.py geomap()`).

**Deliberately not rewritten.** The description understates the accepted input range — the package
also ingests JPEG, PNG, TIFF, GIF, HDF5 and MATLAB `.mat` imagery through `io.load_image()` and
`io.meanstack()`, not only FITS. The wording nevertheless stands: it is not wrong (FITS is what the
Astrometry.net step consumes, and non-FITS input is converted to FITS first), and rephrasing curated
prose for style is not an improvement. The understatement is recorded so a future agent reads it as a
noticed and accepted limit of the wording rather than an oversight, and knows the full accepted input
range is carried by Field 18.

### 9. Concise Description (OPTIONAL)
- **Value:** Plate scale and calibrate star imagery to azimuth/elevation coordinates for auroral and airglow camera observations using Astrometry.net.

137 characters, within the field's 200-character limit. Derived from the PyHC registry description
("plate scale / calibrate star imagery to use multiple auroral/airglow cameras together") rendered as
a sentence. Accurate at this revision; the curated wording is kept rather than restyled.

### 10. Publication Date (RECOMMENDED)
- **Value:** 2016-02-13

The date of the earliest commit in the published history, `45c3c972d9500f93f3679a161f3ec5925dbb6e2b`,
2016-02-13 22:28:18 -0500.

**Alternative considered and not selected.** The GitHub API reports the repository's `created_at` as
2014-05-02T05:14:44Z, nearly two years earlier. The two cannot be reconciled from available evidence:
the earliest commit's message is "rebase", so the history was rewritten and any pre-2016 commit dates
were destroyed. There is no Zenodo deposit or release older than the 2016 history to arbitrate
(the earliest GitHub release is `v1.0`, 2016-09-29). 2016-02-13 is the earliest date that is
verifiable from a primary artifact, so it stands. A future agent should not silently flip this to the
repository creation date; doing so would require evidence that the pre-rebase content was the same
software.

Note that DataCite reports `publicationYear: 2026` for the concept DOI. That is an artifact of the
concept DOI resolving to the newest version and must not be used for this field.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

The software's DOIs are minted through the GitHub-Zenodo integration, which makes Zenodo the
publisher; DataCite records `publisher: "Zenodo"` for the concept DOI.

A ROR would be preferred to a bare URL, but a ROR API query for "Zenodo" returns zero results, so
`https://zenodo.org` is the correct fallback the field allows. Do not substitute CERN's ROR: CERN
operates Zenodo but is not the publisher named in the DOI metadata.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.4.1
- **Version Date:** 2026-07-09
- **Version Description:** overhaul to be package based
- **Version PID:** https://doi.org/10.5281/zenodo.21280344

Each part derived independently:

- **Number** — git tag `v1.4.1` resolves to the pinned commit `cbe04e5`; Zenodo's record 21280344
  reports `version: "v1.4.1"`; the GitHub release is tagged `v1.4.1`. The `v` prefix follows both the
  tag and Zenodo, and matches the convention already used for the previous version record. Note that
  `src/astrometry_azel/__init__.py` declares `__version__ = "1.4.1"` without the prefix; the prefixed
  form is the one carried by the release artifacts.
- **Date** — three independent sources agree on 2026-07-09: the git tag's creation date, the GitHub
  release `published_at` 2026-07-09T13:20:15Z, and Zenodo's `publication_date` 2026-07-09.
- **Description** — the GitHub release name, "overhaul to be package based", which Zenodo mirrors as
  the suffix of its record title ("space-physics/astrometry_geomap: overhaul to be package based").
  The release body is empty, so the release name is the only maintainer-authored summary available.
  For context, this release closes a long gap: 66 commits separate the `v1.3.0` and `v1.4.1` tags,
  the bulk of them a 2023 refactor and a 2024-02-05 plotting batch that were never tagged. The five
  commits immediately preceding the tag are the July 2026 modernization burst that gives the release
  its name: `46c8418` "modernize package" (dropped the `python-dateutil` dependency, raised
  `requires-python` to >=3.10, removed the flake8 lint extra), `5bd7ca2` "update
  URLs", `dd50a41` "use main entry point" (added `src/astrometry_azel/__main__.py`, removed the
  top-level `PlateScale.py`), `ab587e5` "unambiguous index_data reference" (added the `packaging`
  dependency, which supports its Astrometry.net <0.95 / >=0.95 accommodation), and `cbe04e5` "badge".
  That detail is recorded here rather than in the field value, so the stored description stays
  faithful to the maintainer's own release note.
- **PID** — the version DOI `10.5281/zenodo.21280344`, confirmed by the Zenodo API record whose
  `conceptdoi` is `10.5281/zenodo.595450` and by DataCite's `IsVersionOf` relation.

**Superseded value.** Until this record was brought up to date on 2026-08-29, HSSI carried
v1.3.0 / 2021-02-10 / "python >= 3.7, to keep up with NEP29 stack, src/ layout" /
`https://doi.org/10.5281/zenodo.4527817`. That was correct when it was recorded, and is superseded by
the 2026-07-09 release rather than corrected.

**Also superseded.** An earlier dossier noted that the repository declared an unreleased development
version v1.4.0 with no Zenodo DOI. That development state was released as v1.4.1 with a DOI, so the
reason for withholding it no longer applies.

### 13. Programming Language (RECOMMENDED)
- **Values:**
  - Python 3.x
  - MATLAB

**Python 3.x** — the entire installable package is Python. `pyproject.toml` sets
`requires-python = ">=3.10"` and the CI matrix exercises Python 3.10 and 3.14. GitHub's language
statistics for the repository report 41,665 bytes of Python.

**MATLAB** — rests entirely on one file, `archive/modifyFITSheaderAstrometry.m` (89 lines), which is
present at the pinned revision and has been unchanged since the first commit. GitHub's language
statistics count it (2,514 bytes of MATLAB). It is a genuine part of the distributed repository, and
it is the historical MATLAB implementation of the same FITS/WCS-to-RA-Dec step the Python package
performs, so it is not unrelated scaffolding. It is, however, archived and not exercised by the
package or its tests. If a future revision deletes `archive/`, this value should be dropped.

Note for Field 15: that MATLAB file carries its own header comment "GPL v3+ license", which differs
from the repository's ISC `LICENSE.txt`.

### 14. Reference Publication (OPTIONAL)
- **Value:** Not found

No publication describes this software. There is no JOSS paper, no `CITATION.cff`, no `codemeta.json`
and no paper reference in the README, `pyproject.toml` or the Zenodo/DataCite records.

**Considered and rejected.** The README links a PDF, Schindler et al. 2016
(`https://www.dsi.uni-stuttgart.de/institut/mitarbeiter/schindler/Schindler_et_al._2016.pdf`),
described in the README as an "article on good robustness of Astrometry.net to shaky, streaked
images". That paper is about Astrometry.net, the external solver, not about this package, and
predates most of it. It is neither a reference publication (Field 14) nor a related publication
(Field 27), because it neither describes nor uses this software.

The publication recorded in Field 27 *uses* this software rather than describing it, which is why it
belongs there and not here. The citable artifact for this software is its Zenodo DOI (Field 2).

### 15. License (RECOMMENDED)
- **License:** Other
- **License URI:** https://spdx.org/licenses/ISC.html

**The actual licence is ISC.** `LICENSE.txt` contains the ISC permission text ("Permission to use,
copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted
..."), copyright "2020 SciVision, Inc."; the GitHub API reports `spdx_id: ISC`; and DataCite records
`rightsIdentifier: isc` with `rights: "ISC License"`.

**`Other` is nevertheless the correct stored value**, because HSSI's License field is a closed
vocabulary and it contains no ISC row. The complete vocabulary is: Apache License 2.0;
BSD 2-Clause "Simplified" License; BSD 3-Clause "New" or "Revised" License; Creative Commons
Attribution 4.0 International; GNU General Public Licenses (GPL version 2); GNU General Public
License v3.0 or later; GNU Lesser General Public License v3.0 only; GNU Library or ‘Lesser’ General
Public Licenses (LGPL version 2); MIT License; Other; Restricted. None of the permissive rows is
ISC, and none is close enough to substitute — ISC is not MIT and not a BSD variant, so selecting one
of those would misstate the licence. The submission serializer matches licence names exactly
(case-insensitively) and rejects anything else, so an SPDX title such as "ISC License" would be
refused outright.

The License URI carries the real information: `https://spdx.org/licenses/ISC.html` identifies the
actual licence even though the name field must read `Other`.

**Corrected claim.** An earlier dossier recorded the licence name as "ISC License". That is the right
licence but not a submittable value; recording it would fail on submission.

**Durable caveat.** `archive/modifyFITSheaderAstrometry.m` declares "GPL v3+ license" in its own
header comment, which conflicts with the repository-level ISC `LICENSE.txt`. This is an upstream
inconsistency in a single archived file, not something HSSI metadata can resolve; the
repository-level licence governs the field value. It is noted so a future agent who finds the GPL
string does not conclude the ISC reading is wrong.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Values:**
  - aeronomy
  - airglow
  - astrometry
  - astronomy
  - astropy
  - aurora
  - citizen-science
  - ionosphere_thermosphere_mesosphere
  - plate-scale

Sources: `pyproject.toml` `keywords = ["astrometry", "plate-scale", "astronomy", "aurora"]`; GitHub
repository topics `astrometry`, `astropy`, `citizen-science`; PyHC registry keyword
`ionosphere_thermosphere_mesosphere`.

**Why `airglow` and `aeronomy` belong here.** Both are existing rows in HSSI's keyword vocabulary and
both are directly evidenced. Airglow is named in the README's "PlotGeomap.py" section, in
`PlotGeomap.py`'s module docstring ("This technique is used in aeronomy for aurora and airglow"), in
the PyHC description, and in this record's own Field 8 description; aeronomy is named in the first two
of those, which are the only two files in the repository that use either word. Until this record was
brought up to date on 2026-08-29, HSSI's stored keyword set omitted both while carrying airglow's
companion term `aurora` — an asymmetry nothing in the evidence supported.

**Considered and rejected.**

- **`specific`** — the second PyHC keyword on this entry. It is a marker in PyHC's own
  general-versus-specific taxonomy, not a science term, and carries no meaning outside that registry.
- **`all-sky-camera` / `all-sky-imager`** — both exist in the vocabulary and would be plausible for an
  auroral imaging tool, but the repository evidence points the other way:
  `download/__main__.py` describes its index-file defaults as chosen for "non-all-sky auroral
  imagagers in the 5 to 50 degree FOV range" [sic], and the README says `solve-field` "is designed for
  professional science-grade imagery from telescopes and narrow to medium field of view imagers (at
  least to 50 degree FOV)". An earlier dossier asserted the README mentions all-sky cameras; it does
  not at this revision. Do not add these rows without new evidence.
- **`photometry`** — the README's "Related" section points users to a *different* package for
  photometry, which is evidence that this one does not do it.
- **`fits`, `netcdf`, `image processing`, `calibration`** — all true of the software, but the field's
  own guidance is for keywords "not supported by other metadata fields". These are already carried by
  Fields 18/19 (file formats) and Field 4 (functionality).
- **`citizen science`** (space-separated) — a near-duplicate of the stored hyphenated
  `citizen-science`, which matches the GitHub topic exactly. Adding both would mint a redundant
  association.

### 17. Data Sources (OPTIONAL)
- **Value:** HTTP/HTTPS Directories

`src/astrometry_azel/download/__main__.py` retrieves Astrometry.net star index files by plain HTTPS
directory listing from `https://data.astrometry.net/4200/` (2MASS) and `https://data.astrometry.net/4100/`
(Tycho), with `urllib.request.urlretrieve`. The CI workflow exercises this path directly
(`python -m astrometry_azel.download -source https://data.astrometry.net/4100/ -i 10 15`).

**Considered and rejected.** No other row in the vocabulary applies. In particular
`Observatory/Mission-specific` does not: the retrieved files are all-sky star catalogue indices used
by the solver, not any observatory's or mission's data holdings — which is also why Fields 31 and 32
are empty. There is no FTP path, no HAPI/CDAWeb/SSCWeb/OMNIWeb/VirES/Madrigal/AMDA/das2/TAP/WDC/GFZ
client, no cloud or S3 access, and no VSO usage anywhere in the package.

### 18. Input File Formats (RECOMMENDED)
- **Values:**
  - FITS
  - HDF5
  - netCDF3/4
  - Other

- **FITS** — `fits2radec()` opens the image and its `.wcs`/`.new` sidecar with `astropy.io.fits`;
  `io.get_sources()` reads Astrometry.net's `.rdls` and `-indx.xyls` FITS binary tables;
  `io.meanstack()` handles `.fits` and `.new`.
- **HDF5** — `io.meanstack()` dispatches `.h5` to `io._h5mean()`, which reads `/rawimg`, `/ut1_unix`
  and `/params` through `h5py`; `io.readh5coord()` reads observer coordinates from `/sensorloc` or
  `/lla`. The `python -m astrometry_azel` CLI help states "image data file name (HDF5 or FITS)".
- **netCDF3/4** — `io.read_data()` opens a netCDF file with `xarray.open_dataset()`, and
  `PlotGeomap.py` takes exactly that as its input argument: "netCDF file from python -m
  astrometry_azel". netCDF is therefore a genuine *input* format for the second stage of the
  workflow, not only an output. Until this record was brought up to date on 2026-08-29, HSSI carried
  netCDF for this software as an output format only; the code never supported that asymmetry.
- **Other** — formats with no row in the vocabulary: JPEG, PNG, TIFF and animated GIF via
  `imageio.v3.imread()` in `io.load_image()` and `io.meanstack()`, and MATLAB `.mat` via
  `scipy.io.loadmat()` in `io.meanstack()`. The README's worked example passes a `.jpg`.

### 19. Output File Formats (RECOMMENDED)
- **Values:**
  - FITS
  - netCDF3/4
  - Other

- **FITS** — `io.write_fits()` writes a `PrimaryHDU` with checksum; `project.plate_scale()` uses it to
  produce the `_new.fits` file handed to `solve-field`.
- **netCDF3/4** — `io.write_netcdf()` writes `format="NETCDF4"` with zlib compression, Fletcher32
  checksums and per-variable chunking. The README states the primary output plainly: "gives netCDF
  .nc with az/el ra/dec and PNG plots of the data".
- **Other** — PNG figures. `src/astrometry_azel/__main__.py` writes `*_radec.png` and `*_azel.png`;
  `PlotGeomap.py` writes `*_proj.png`; `plot.image_stack()` writes `*_picture.png`;
  `scripts/AverageImageStack.py` writes PNG frames via `imageio.imwrite()`.

### 20. Operating System (RECOMMENDED)
- **Values:**
  - Linux
  - Mac

The README states it directly: "The supported operating systems are Linux, macOS, or Windows
Subsystem for Linux", with per-platform install lines `apt install astrometry.net` and
`brew install astrometry-net`. The CI matrix in `.github/workflows/ci.yml` builds and tests on
`ubuntu-26.04` and `macos-latest`, with a matching conditional step that installs Astrometry.net by
apt on Linux and by Homebrew on macOS.

**Why Mac is listed.** An earlier dossier recorded Linux only, on the then-accurate observation that
CI ran `ubuntu-latest` alone. The July 2026 CI rework added macOS as a first-class tested platform,
so the basis for excluding it no longer holds.

**Considered and rejected.**

- **Windows** — the README's only Windows route is Windows Subsystem for Linux, which runs the Linux
  build; there is no native Windows support, and the required external Astrometry.net program is
  installed there through Ubuntu inside WSL. Recording `Windows` would tell a user the package
  installs natively on Windows, which it does not.
- **Operating System Independent** — `pyproject.toml` carries the classifier
  `"Operating System :: OS Independent"`, which is a packaging default rather than a tested claim. It
  is contradicted by the README's explicit three-environment statement and by the hard external
  dependency on Astrometry.net's `solve-field` binary, which the repository only shows being obtained
  for Linux and macOS. The Python code alone would be OS-independent; the software as documented is
  not.

### 21. CPU Architecture (RECOMMENDED)
- **Value:** CPU Independent

The package is pure Python with no compiled extensions of its own and no architecture-specific code
paths; `pyproject.toml` declares no platform or architecture constraint.

**Considered and rejected.** `x86-64` and `Apple Silicon arm64` are both exercised in practice (the
GitHub-hosted `ubuntu-26.04` and `macos-latest` runners respectively), but listing them would narrow
a true claim into a false one — nothing in the package prevents it running on other architectures
where its dependencies build. `GPU` and `HPC or HEC` are not applicable; there is no accelerated or
parallel code.

### 22. Related Phenomena (OPTIONAL)
- **Value:** Not found — no applicable row exists in the vocabulary

This is an evidenced empty value, not an unexamined gap. The software's phenomena are unambiguous —
aurora and airglow, named throughout the README, the PyHC description and the Field 8 description —
but HSSI's Related Phenomena vocabulary is a closed list whose complete contents are: Coronal
Heating; Coronal Mass Ejections; Geomagnetic Storms; Solar Corona; Solar Flares; Solar Wind; X-ray
emission. None of the seven names an optical upper-atmosphere emission: there is no aurora row and
no airglow row, and nothing else in the list is something an auroral imaging tool could honestly
claim.

**Corrected claim.** An earlier dossier recorded "Aurora" and "Airglow" here with a note that they
"may not be in the controlled vocabulary". They are not, and the field rejects unknown values
outright — those entries were unsubmittable. Per the field's own guidance, a phenomenon with no row
belongs in Keywords instead, which is where `aurora` and `airglow` are recorded (Field 16).

`Geomagnetic Storms` is the trap to avoid here: aurora is a storm-time manifestation, but this
software supports no science functionality for geomagnetic storms as such — it geolocates optical
imagery and computes no geomagnetic quantity. Do not select it as a proxy for aurora.

### 23. Development Status (RECOMMENDED)
- **Value:** Active

Evidence at and around the pinned revision: version v1.4.1 was tagged and released 2026-07-09, with a
matching Zenodo deposit the same day; the GitHub API reports `archived: false` and `pushed_at`
2026-07-09T13:20:15Z; the CI matrix tests against Python 3.14, i.e. it tracks current interpreter
releases; and `pyproject.toml` classifies the package `"5 - Production/Stable"`. Under the
repostatus.org definitions HSSI uses, that is `Active` — reached a stable, usable state and being
actively developed.

**Corrected claim.** An earlier dossier recorded `Inactive` on the evidence available to it: the
newest commit was then 2024-02-05 and the newest release v1.3.0 from 2021-02-10. The July 2026
release supersedes that reading. HSSI held no development-status value at all until this record was
brought up to date on 2026-08-29.

**Durable caveat for the next refresh.** Development is episodic rather than continuous — releases
cluster in 2016-2021, then 2024 commits with no release, then the 2026-07 release. `Active` is
correct as of this revision, but a future agent should re-derive it from the newest release and push
dates rather than assuming it persists.

### 24. Documentation (RECOMMENDED)
- **Value:** https://github.com/space-physics/astrometry_geomap

The README is the documentation. It carries the installation instructions the field asks for
(operating system prerequisites, `apt`/`brew` install of Astrometry.net, virtual environment setup,
`pip install -e`, star index download, and how to run the self-tests) plus usage examples for both
the local-solver and the nova.astrometry.net web-service workflows. There is no Read the Docs site,
no `docs/` directory, and GitHub Pages is not enabled (`has_pages: false`, `has_wiki: false`).

**Considered and rejected.** `https://www.scivision.dev/astrometry-tips-techniques` is the
repository's GitHub `homepage` field and is linked from the README as a "Tips and techniques article,
especially for DSLR citizen science data". Reading it, it is a general article about tuning
Astrometry.net's `solve-field` — source-count targets, `--sigma`, `--downsample`, `-L`, cropping
strategies, verification against Stellarium. It mentions this package in passing and links its
repository, but documents neither its installation nor its API. It is a useful companion read, not
this software's documentation.

### 25. Funder (OPTIONAL)
- **Value:** Not found

### 26. Award Title (OPTIONAL)
- **Value:** Not found

Negative research covering both fields: DataCite returns an empty `fundingReferences` array for the
concept DOI; the Zenodo record carries no grant metadata; the repository contains no acknowledgments,
funding file, `CITATION.cff` or `codemeta.json`; the README and `Readme_build.md` name no sponsor;
and the author's tips-and-techniques article carries no acknowledgment section.

**Trap to avoid.** The publication recorded in Field 27 (Nanjo et al. 2026) is funded by the Japan
Society for the Promotion of Science, and Crossref exposes those awards on that DOI. That funding
supports the *citing* study — a camera calibration campaign that used this software — not the
development of this software. It must not be copied into these fields.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Value:** https://doi.org/10.1186/s40623-026-02451-6

Nanjo, S., Brändström, U., Nozawa, S., Kawabata, T., and Hosokawa, K. (2026), "Calibration and
observations of an AI-triggered commercial digital camera for auroral studies", *Earth, Planets and
Space*, 78:112. Open access under CC BY 4.0; published 2026-05-29. Bibliographic details confirmed
against the Crossref API for that DOI.

This is a publication that *uses* the software, which is exactly what Field 27 is for. Its
geometrical-calibration section states that the Astrometry.net calibration parameters "were then
input into the Python package astrometry-azel (Hirsch 2021) to compute the azimuth and zenith angle
for each pixel in the image", and its reference list carries "Hirsch M (2021)
space-physics/astrometry_azel." — a substantive methodological use, not a passing mention. The
paper's own subject, an AI-triggered commercial digital camera used for auroral observation, is
precisely the citizen-science-grade auroral imaging this package is built for.

**Independent verification of the quoted use.** The publisher's site blocks non-browser fetches, so
the citation was confirmed through ADS/SciX full-text search against the paper's bibcode
`2026EP&S...78..112N`: the queries `full:"astrometry-azel"` and `full:"astrometry_azel"` restricted
to that bibcode each match, while a nonsense-token control query against the same bibcode returns
nothing, ruling out a false positive from the search backend. Europe PMC has no record of this DOI,
and Semantic Scholar has no paper node for either Zenodo DOI, so the citation-graph route is
unavailable for this software — ADS full text is the working route and should be the first stop for a
future refresh.

**Considered and rejected.** The Schindler et al. 2016 PDF linked from the README is about
Astrometry.net's robustness to shaky and streaked images. It neither cites nor uses this package, and
predates most of it; see Field 14.

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found

**Considered and not selected.** The software downloads Astrometry.net's pre-built star index files —
the 2MASS index at `https://data.astrometry.net/4200/` and the Tycho index at
`https://data.astrometry.net/4100/`. These are reference catalogues consumed by the external
`solve-field` solver to recognize star patterns; they are not observational datasets the software
analyses, which is what Field 28 asks for ("datasets the software supports functionality for"). Their
role — an HTTP-retrieved input source — is already recorded in Field 17.

Recorded so a future agent can see they were weighed rather than missed. If HSSI's reading of Field 28
were ever broadened to include reference catalogues, these two URLs would be the ones to record.

### 29. Related Software (OPTIONAL)
- **Values:**
  - https://github.com/dstndstn/astrometry.net
  - https://github.com/astropy/astropy
  - https://github.com/geospace-code/pymap3d
  - https://github.com/space-physics/dascasi
  - https://github.com/scivision/starscale

**The case for each.**

- **astrometry.net** (`dstndstn/astrometry.net`) — the defining dependency. It is not a Python
  package but an external C program that this software wraps: `doSolve()` locates the `solve-field`
  executable with `shutil.which()`, checks its version for `--index-dir` support, and runs it as a
  subprocess; the README's installation section is largely about obtaining it, `Readme_build.md`
  documents building it from source, and both CI jobs install it before the tests. The package has no
  purpose without it. This is the clearest possible domain-specific dependency.
- **astropy** — a domain-specific (astronomy) dependency whose presence characterizes the software
  rather than merely being present. The RA/Dec-to-Az/El transform is performed by
  `astropy.coordinates` (`SkyCoord.transform_to(AltAz(location=EarthLocation(...), obstime=Time(...)))`),
  the WCS pixel-to-world evaluation by `astropy.wcs.WCS.all_pix2world()`, and all FITS I/O by
  `astropy.io.fits`. It fails the generic-infrastructure test decisively: astropy would be absurd in a
  web app, a finance model or a biology pipeline.
- **pymap3d** — a domain-specific geodetic coordinate-conversion library, hard-imported at
  module scope in `src/astrometry_azel/project.py` and called as
  `pymap3d.aer2geodetic(az=..., el=..., srange=..., lat0=..., lon0=..., h0=...)` to turn the computed
  azimuth/elevation plus slant range into WGS-84 latitude/longitude. Without it the geographic
  projection — the capability the repository is now named for — does not run.
  `src/astrometry_azel/tests/test_all.py` guards `test_fits2azel` with
  `pytest.importorskip("pymap3d")`. Recorded under its canonical repository
  `https://github.com/geospace-code/pymap3d`; `https://github.com/scivision/pymap3d` is the former
  URL and redirects there.

  **Durable upstream limitation.** `pymap3d` is a hard import but is *not* declared in
  `pyproject.toml`'s `dependencies = ["packaging", "numpy", "astropy", "xarray", "netcdf4"]`, so a
  clean `pip install` of this package leaves `project.py` unimportable. The test suite tolerates this
  via `importorskip`, which is why CI stays green. Worth knowing for anyone reasoning about the
  package's real dependency set; it is an upstream packaging bug, not a metadata error.

  A naming quirk that can mislead: `src/astrometry_azel/__init__.py` defines a function named
  `pymap3d_radec2azel()` which is implemented entirely with astropy. The name is a historical
  artifact of an earlier implementation and is not evidence of a pymap3d call in that module — the
  real call is the one in `project.py`.
- **dascasi** (`space-physics/dascasi`) — named in the source as the origin of an algorithm.
  `project.image_altitude()` carries the docstring line "adapted from
  https://github.com/space-physics/dascasi". Its GitHub description is "Digital All Sky Camera
  utilities, for U. Alaska Geophysical Institute cameras"; PyHC registers it as "DASCutils", "Digital
  All Sky Camera utilities, for camera at Poker Flat Research Range and elsewhere". It is a companion
  package by the same author that performs the same single-altitude geographic projection, but bound
  to specific all-sky cameras. It is distinguishing in exactly the way Field 29 intends: a reader
  learns where this software's projection method came from and what the instrument-specific sibling
  is.
- **starscale** — the README's "Related" section: "For source extraction or photometry, see my
  AstroPy-based [examples](https://github.com/scivision/starscale)." An author-declared companion for
  adjacent functionality this package deliberately does not provide.

  **Two facts about this URL, neither of which unsettles it.** First, the recorded
  `https://github.com/scivision/starscale` is the pre-rename URL and redirects to
  `https://github.com/space-physics/starscale`. The pre-rename form is the recorded value because
  this entry exists only by virtue of the README citing it, so the URL here is the one the README
  actually links, and it resolves. The redirect is documented so a future agent reads the older URL
  as a faithful reflection of the source rather than as an error to correct; substituting the
  canonical post-rename target would silently detach the entry from the evidence that justifies it.
  Second, the target repository is archived (last push 2021-12-29), which does not disqualify it —
  the README still points readers there, and Field 29 exists to tell a reader what related software
  exists, including software that is no longer developed.

**Considered and rejected.** The generic stack was evaluated against the same gate applied in
Field 30 and is excluded here too: numpy, scipy, matplotlib, cartopy, imageio, scikit-image,
packaging and pytest are generic infrastructure (arrays, plotting, mapping, image and archive I/O,
packaging, testing) that would be equally at home outside heliophysics, and saying this software
depends on them distinguishes it from nothing. A package rejected from Field 30 does not thereby
belong here.

### 30. Interoperable Software (OPTIONAL)
- **Values:**
  - https://github.com/astropy/astropy
  - https://github.com/pydata/xarray

**The demonstrated exchange for each.**

- **xarray** — `xarray.Dataset` is the package's documented public interchange format, not an
  internal convenience. `fits2radec()` is annotated `-> xarray.Dataset`; `fits2azel()` returns the
  same object; `radec2azel(scale: xarray.Dataset, ...)`, `project.image_altitude(img: xarray.Dataset, ...)`
  and `io.write_netcdf(ds: xarray.Dataset, ...)` all take one; `io.read_data()` returns one. The
  returned Datasets carry labelled coordinates, named data variables (`ra`, `dec`, `azimuth`,
  `elevation`, `latitude_proj`, `longitude_proj`) and per-variable `units` attributes, so any
  xarray-speaking tool can consume this software's output directly with no conversion step.
- **astropy** — the public API exchanges astropy objects, not merely uses the library.
  `io.get_sources()` returns an `astropy.io.fits.fitsrec.FITS_rec` (its docstring names the return
  type as `astropy.fits.fitsrec.FITS_rec`, an upstream typo for the same class; the value is consumed
  by `scripts/PrintSourceRaDec.py` and `scripts/OverlayStars.py`), and the FITS artefacts the
  package reads and writes (`.new`, `.wcs`, `.rdls`, `-indx.xyls`) round-trip through astropy's FITS
  and WCS machinery. astropy is a peer science tool a user would deliberately combine with this
  package.

**Three values retired.** Until this record was brought up to date on 2026-08-29, HSSI carried three
further entries here, each of which fails the relevance gate: the gate asks for a demonstrated
exchange with another high-level science tool, not for a dependency listing. The reasoning that
retired each one is recorded below so a future agent does not restore it from the dependency list
alone.

- **python-dateutil** (`https://github.com/dateutil/dateutil`) — retired on two independent grounds.
  It is not in the repository at all at this revision: commit `46c8418` ("modernize package",
  2026-07-08) dropped `python-dateutil` from `dependencies` and `types-python-dateutil` from the lint
  extra, and a full-tree search for "dateutil" at the pinned revision returns nothing. Date parsing is
  now done with `datetime.fromisoformat()` and `numpy.datetime64`. Independently, `python-dateutil` is
  named in Tier A of the exclusion list — generic date plumbing, true of a large share of the Python
  ecosystem, and not by itself evidence of interoperability.
- **numpy** (`https://github.com/numpy/numpy`) — retired. Tier A. It is a real dependency and is used
  throughout, but "depends on numpy" is true of a large share of the scientific Python ecosystem and
  therefore says nothing about this software in particular.
- **netcdf4-python** (`https://github.com/Unidata/netcdf4-python`) — retired, and the closest call of
  the three, because it is the one the source names explicitly by library rather than merely
  importing, so both sides of the reasoning are recorded in full against a future agent who finds that
  name and reads it as a declared integration. In its favour: `io.write_netcdf()` hard-codes
  `ds.to_netcdf(out_file, format="NETCDF4", engine="netcdf4", encoding=enc)`, naming the library
  explicitly, `scripts/PlateScaleFITS.py` selects the same engine, and netCDF is the on-disk handoff
  between `python -m astrometry_azel` and `PlotGeomap.py`. Against it, decisively: the library is
  never imported and is surfaced in no signature, return type or other user-facing API at this
  revision — outside the `dependencies` list in `pyproject.toml` and one passing code comment, those
  two `engine=` strings are its whole presence in the source, so it sits underneath xarray's writer,
  which is "uses internally", the exact case Tier B excludes. The only "exchange" is this software
  reading back its own output file. And what the user actually needs to know — that the software reads and
  writes netCDF3/4 — is a *format* fact already recorded in Fields 18 and 19, which is where it
  belongs. Dropping it loses no information.

**Considered and not added.** cartopy, matplotlib, imageio, scikit-image, scipy, h5py and packaging
were each evaluated. All are generic infrastructure by the "web app, finance model, or biology
pipeline" test — mapping, plotting, image I/O, image algorithms, scientific utilities, array-file
I/O, packaging. h5py is Tier B rather than Tier A, so it was checked specifically: it appears only
inside `io._h5mean()` and `io.readh5coord()`, returns plain numpy arrays, and is never exposed in the
public API, so it fails the cited-exchange requirement. HDF5 support is recorded in Field 18 where it
belongs. Astrometry.net is a genuine peer tool but is an external C program invoked as a subprocess
rather than a package this one exchanges data models with, so it is recorded in Field 29.

### 31. Related Instruments (OPTIONAL)
- **Value:** Not found — documented omission

The software is instrument-agnostic by design. It plate-scales and geolocates any star-field image
for which the user supplies an observer location and a UTC timestamp; nothing in the package reads,
parses, calibrates or models any specific instrument's data, and no instrument-specific format or
convention is implemented.

The instrument-adjacent mentions at the pinned revision are the following, and none clears the
designed-to-support bar:

- `src/astrometry_azel/download/__main__.py` describes its index-file defaults as useful for "a
  variety of non-all-sky auroral imagagers in the 5 to 50 degree FOV range" [sic] — a field-of-view
  class of cameras, not a named instrument.
- The README describes `solve-field` as designed for imagery "from telescopes and narrow to medium
  field of view imagers" — a generic class label.
- `archive/modifyFITSheaderAstrometry.m` name-drops `HST1` and `HST2` inside an example comment
  (`modifyFITSheaderAstrometry('../Meteor/HST1_1secNoEM.wcs',512,512)`). This is a filename in a
  usage example in an archived, unexercised MATLAB helper (HST here is the author's own HiST
  high-speed auroral imager). It is the kind of demonstration mention the relevance gate explicitly
  excludes, and a search of HSSI's SPASE-backed instrument vocabulary for HiST/HST returns only
  THEMIS rows matching on the substring in "History", so there is no row to bind to in any case.
- `src/astrometry_azel/plot/project.py` hard-codes Thunder Mountain, Calgary, Banff and Edmonton as
  map annotations. These are cartographic reference points for human orientation, not observing
  sites.
- `src/astrometry_azel/tests/apod4.*` is an Astrometry.net demonstration image, credited in
  `src/astrometry_azel/tests/credits.txt` to
  `https://github.com/dstndstn/astrometry.net/blob/master/demo/apod4.jpg`. A test fixture, not an
  instrument association.

**Corrected claim.** An earlier dossier recorded "Digital All Sky Cameras (general category)" with
"Instrument Identifier: Not found". That entry was wrong twice over. It is a generic class label
rather than a resolvable instrument, and Fields 31/32 accept only SPASE-identified rows — a name
without a `https://spase-metadata.org/` identifier either binds arbitrarily to a same-named row or
creates a new identifierless row, which is precisely what the vocabulary backfill removed. It was
also contradicted by the repository, which at this revision documents *non*-all-sky imagers. The
same dossier attributed a Poker Flat DASC association to this package; that association belongs to
the separate `dascasi` package (Field 29), and no Poker Flat or DASC reference exists in this
repository at the pinned revision.

The instrument vocabulary was searched for rows that might have applied despite the agnosticism —
Poker Flat sites, all-sky imagers, auroral imagers, airglow instruments — and rows do exist for many
of them (for example
`https://spase-metadata.org/IUGONET/Instrument/NICT/SALMON/PF/asi`). None was selected, because the
software supports none of them specifically. A user searching HSSI for any of those instruments would
not expect this tool back, and someone working with that instrument's data would not reach for it. An
empty Field 31 is the correct outcome here, not a gap.

### 32. Related Observatories (OPTIONAL)
- **Value:** Not found — documented omission

Same reasoning as Field 31. The software is not tied to any observatory: observer latitude, longitude
and time are mandatory command-line arguments supplied per image, which is the structural expression
of its site-agnosticism. The README's worked examples use an arbitrary coordinate pair
(`61.2 -149.9`, near Anchorage) purely to demonstrate the CLI.

No observatory-level substitution is available or appropriate, because there is no
designed-to-support instrument whose platform could stand in for it — the omission is of the
"nothing applies" kind (Field 17's `Observatory/Mission-specific` is correspondingly unselected), not
the "instrument missing from the vocabulary" kind.

### 33. Logo (OPTIONAL)
- **Value:** Not found

Evidenced absence. The repository tree at the pinned revision contains exactly one image file in a
web-displayable format, `src/astrometry_azel/tests/apod4.jpg` (JPEG, 719x507, 65,564 bytes); there is
no PNG, GIF, SVG or other such file anywhere in the tree. That JPEG is the Astrometry.net
demonstration photograph used as a test fixture and is credited as such in
`src/astrometry_azel/tests/credits.txt`. Using it as a logo would misrepresent both this software and
Astrometry.net's demo asset.

There is no logo elsewhere either: the README contains two badges (a Zenodo DOI badge and a CI status
badge, neither a logo), and the PyHC registry entry for `AstrometryAzEl` in `projects_unevaluated.yml`
has no `logo:` key — notable because the neighbouring `DASCutils` entry in the same file does have
one, so the absence reflects the registry's actual content rather than a registry that never carries
logos.

Any logo recorded here in future must be a commit-pinned raw URL that fetch-verifies as `image/*`
with plausible image bytes and fits within 200 characters. Nothing at this revision qualifies.

---

## Metadata Agreement (MANDATORY)

By submitting this form, you acknowledge and agree that any metadata you provide is submitted
voluntarily and becomes part of the public domain. You waive all rights, claims, and interests to the
submitted metadata, and grant unrestricted use, reproduction, modification, and distribution rights to
the receiving party or its designees.
