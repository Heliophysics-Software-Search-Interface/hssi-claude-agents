# HSSI Metadata Extraction Results

**HSSI Software ID:** c0c97c0f-c50b-44b5-9b95-c599e99004fa
**Repository:** https://github.com/space-physics/GOESplot
**Source Revision:** fa4e4d378b50f422450c1c936e2aa770525de18d
**Extraction Date:** 2026-08-30
**Validation Date:** 2026-08-31
**Validation Status:** PASS

---

## Scope note — read this before interpreting any field below

Two facts about this software change how all the evidence should be read, and they recur in almost
every field note:

1. **The project has been renamed twice and its HSSI name is not its repository name.** The
   repository is `space-physics/GOESplot`, the packaging name at the pinned revision is `goesplot`,
   and the name this record carries is `GOESutils` — the name under which the Python in Heliophysics
   Community registry lists it and the name of the only artifact this project ever published to
   PyPI. Field 7 records the full name history and the reasoning; other fields refer back to it
   rather than repeating it.
2. **The repository is archived on GitHub (verified 2026-08-30) and its last push is the pinned
   revision, 2022-08-11.** Barring an unarchive, the source tree is closed, and quotations of it
   below are pinned to commit `fa4e4d378b50f422450c1c936e2aa770525de18d`, which is immutable. A few
   quotations are deliberately *not* from the pinned tree — the PyPI and GitHub API metadata, the
   PyHC registry entry, and the pre-rename `setup.cfg` cited in Field 12 — and each says so where it
   appears. It also means the repository's
   own self-descriptions (a `Development Status :: 4 - Beta` classifier from 2018, a PyPI download
   badge pointing at a project name that was never published) are frozen author statements, not
   current signals — several fields below correct values that were previously derived from them.

The tree at the pin is small enough to enumerate: `README.md`, `LICENSE.txt`, `MANIFEST.in`,
`setup.py`, `setup.cfg`, `pyproject.toml`, three top-level driver scripts (`get-goes-preview.py`,
`get-goes-hires.py`, `plot-goes.py`), the installed package `src/goesplot/` (`__init__.py`, `io.py`,
`plots.py`, three `data/*.wld` world files, and `tests/` holding `test_all.py` plus two GOES-13 data
fixtures), and CI/lint configuration. There is no documentation site, no `CITATION.cff`, no
`codemeta.json`, and no `.zenodo.json`.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

Placeholder by catalogue convention — the submitter identity is supplied at submission time and is
not a property of the software.

### 2. Persistent Identifier (RECOMMENDED)
Not found.

No DOI exists for this software. Because the project was renamed twice (Field 7), searching only the
current-era names would prove nothing — a deposition made under an earlier name would sit outside
that search entirely. The sweep below therefore covers the whole name chain and then the author, and
it is recorded in full so a later refresh can rely on it instead of repeating it.

**In the repository.** The pinned tree contains no `CITATION.cff`, `codemeta.json` or `.zenodo.json`,
and a grep of every text file at the pin for `doi`, `cite`, `citation` and `orcid` returns zero
matches, `LICENSE.txt` included. Note the deliberate contrast with Field 25, whose *funder* search
does match inside `LICENSE.txt`, on "grant"/"granted": the Apache text carries no citation or
identifier vocabulary at all, so no "outside the licence boilerplate" qualifier belongs here and the
two fields are not describing the same result.

**DataCite.** Zero results for `goesplot OR goesutils`, searched 2026-08-30.

**Zenodo, by name.** Searched 2026-08-30 for each name this project has carried. `goesplot`,
`GOESplot`, `goesutils`, `goes_quickplot` and `GOES_quickplot` each return zero hits. The two
hyphenated names behave differently, and the difference is worth writing down so that nobody re-runs
them, sees a large result count, and concludes a hit was overlooked: `goes-satellite` and
`goes-quick-plot` return thousands of hits purely because Zenodo tokenises on the hyphen and matches
`goes` as a bare word. Those results are unrelated GOES science datasets and works by authors whose
surname is "Goes". None of them is this software, and none lists Hirsch among its creators. Those two
queries returned noise, not evidence.

**Zenodo, by author — the stronger negative.** A creator-level search on 2026-08-30 for
`creators.name:"Hirsch, Michael"` returns 48 depositions; paged through in full, not one has "goes"
anywhere in its title. Narrowing to `creators.orcid:"0000-0002-1637-6526"` returns 20, with the same
result.

What makes that absence informative rather than merely unproven is that this author does deposit
space-physics tooling of exactly this kind on Zenodo — for instance
`https://doi.org/10.5281/zenodo.376876` (GIMA Magnetometer tools) and
`https://doi.org/10.5281/zenodo.376875` (Auroral Electrojet Tools). So the conclusion is not "this
author never used Zenodo", which would leave the question open; it is a specific gap for this
specific package, observed at author level on 2026-08-30.

**No stale repository is carrying its own deposition hook.** Of the historical GitHub paths,
`scivision/goesutils`, `scivision/goes-quick-plot` and `space-physics/goesutils` all 301-redirect to
repository id 122528719 — the one repository now named `space-physics/GOESplot` — while
`scivision/GOESplot` and `scivision/goesplot` return 404 on the GitHub API. There is a single
repository behind every one of these names, not a family of them, and it is archived, so a
Zenodo–GitHub release hook can no longer mint a DOI for it.

Recorded as an evidenced absence rather than an unexamined blank. A future refresh needs to revisit
this only if the code is deposited independently of the repository.

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/GOESplot

Verified live on 2026-08-30 (GitHub repository id 122528719, default branch `main`). The two earlier
URLs the project used — `scivision/goes-quick-plot` and `scivision/goesutils` — are historical names
of this same repository and redirect to it; see Field 7. Do not substitute either of them, and do not
substitute the PyPI project page: the published PyPI artifact is a 2018 snapshot under a different
name and is not the code repository.

### 4. Software Functionality (RECOMMENDED)
- **Data Processing and Analysis**
- **Data Processing and Analysis: Data Access and Retrieval**
- **Data Processing and Analysis: Data Reduction**
- **Data Processing and Analysis: Image Processing**
- **Data Processing and Analysis: Processing**
- **Data Visualization**
- **Data Visualization: 2D Graphics**

Evidence, per value:

- **Data Access and Retrieval** — the package's headline capability. `get_preview()` in
  `src/goesplot/io.py` drives a `concurrent.futures.ThreadPoolExecutor` pool of HTTP downloads
  against NOAA's GIBBS browse-image service, building each URL from
  `STEM = "https://www.ncdc.noaa.gov/gibbs/image/GOE-"`; `get_hires()` opens an anonymous FTP session
  (`with ftplib.FTP(host, "anonymous", "guest", timeout=15) as F:`) and retrieves a file list parsed
  out of a NOAA CLASS order email by `parse_email()`. Both are exported from the package root
  (`from .io import load, get_hires, get_preview`) and both have a dedicated CLI driver.
- **Processing** — the general load-and-prepare pipeline. `load()` dispatches on file suffix to
  `loadpreview()` or `loadhires()`, each of which assembles an `xarray.DataArray` with named
  dimensions and coordinates; `load()` then stamps provenance onto whichever object came back
  (`img.attrs["filename"] = fn.name`) before returning it. That attribute is set in the dispatcher,
  after the loader returns — not inside either loader.
- **Data Reduction** — `loadhires()` decimates on read,
  `lon = np.flipud(f["lon"][::downsample, ::downsample])` and likewise for latitude and the data
  array, driven by a user-facing option:
  `p.add_argument("-d", "--downsample", help="downsample factor", type=int, default=8)` in
  `plot-goes.py`. Strided subsampling that reduces volume while preserving the field is exactly this
  category, and the default of 8 means the reduction is on by default rather than an edge case.
- **Image Processing** — `wld2mesh()` is documented as
  `"""converts .wld to lat/lon mesh for Cartopy/Matplotlib plots` /
  `    assumes the .wld file is EPSG:4326 coordinates (WGS84)` and turns a six-parameter world file
  into the latitude/longitude grid for the image pixels; `loadpreview()` validates the raster shape
  (`assert img.ndim == 3 and img.shape[2] == 3, "unexpected GOES image format"`) and labels the
  channel axis (`coords={"lon": lon, "lat": lat, "color": ["R", "G", "B"]}`); `loadhires()` corrects
  raster orientation with `np.flipud` and carries a validity mask (`mask = lon > 180`). This is
  georeferencing and conditioning of 2-D raster imagery, which is what the category covers. It is
  included deliberately and on the modest end of the category — there is no deconvolution, feature
  detection or morphology here — but the software's entire subject matter is satellite imagery, and a
  user filtering HSSI for image-processing tools would not be surprised to find a package whose
  public API turns a GOES image file into a georegistered array.
- **2D Graphics** — `plots.py` renders with `h = ax.pcolor(lon, lat, im, transform=PC)` onto a
  Cartopy `Geostationary` axes with coastline and state-boundary features, and `plotlatlon()` draws
  labelled contour fields (`h = ax[0].contour(lat)`).

Considered and rejected, with reasons — recorded so a later refresh does not re-litigate them:

- **Coordinate Transforms** (and every subcategory of it). `wld2mesh()` maps world-file affine
  parameters to a WGS84 grid and `plots.py` reprojects PlateCarree data onto a geostationary view via
  Cartopy. Both are cartographic map projection, not transformation between the heliophysics
  reference frames this category exists to describe — its subcategories are Heliospheric,
  Ionospheric, Magnetospheric, Mission-Specific, Planetary and Solar, and none of them fits a
  geographic raster. Selecting the bare parent would put this package in front of users searching for
  GSE/GSM/AACGM-style frame conversion, which it does not do.
- **Data Processing and Analysis: Analysis.** The package computes no derived physical quantity and
  performs no statistical analysis; it downloads, loads, georeferences and draws. The catch-all is
  easy to over-apply and is left off on that basis.
- **Data Processing and Analysis: File Format Conversion.** Files are read into memory
  (`xarray.DataArray`) but never written out in a different format; the only files the package writes
  are the bytes it downloaded, unchanged. See Field 19.
- **Mission-related** (all subcategories). This is a third-party user-side utility for downloading
  and looking at public NOAA products. It is not part of any NOAA ground system, pipeline, or
  instrument team's toolchain — the distinction the category exists to draw.
- **Models and Simulations**, **Servers and Environments** (all subcategories). No model, solver,
  synthetic data generation, server, container or parallel-computing facility exists in the tree.
- **Data Visualization: Line Plots** and **Movies.** `plotlatlon()` produces contour panels, not line
  plots; there is no animation code and no frame-sequence export.

Two of these values — Data Reduction and Image Processing — were absent from the classification HSSI
held before this refresh, which listed the other five. They were added because the evidence for each
is a specific, user-facing code path, not because the vocabulary happens to contain them.

### 5. Related Region (RECOMMENDED)
- **Earth Atmosphere**
- **Earth Lower and Middle Atmosphere**

`Earth Atmosphere` was the sole region HSSI held before this refresh, and it is retained as the
broad, safe characterisation; it is supported directly by `setup.cfg`'s classifier
`Topic :: Scientific/Engineering :: Atmospheric Science`.

`Earth Lower and Middle Atmosphere` was added alongside it because it is the region the data
actually sample. The package ships world files for exactly three GOES imager bands —
`GOES_EAST_IR.wld`, `GOES_EAST_VIS.wld`, `GOES_EAST_WV.wld` — and the preview downloader advertises
the same set: `p.add_argument("goesmode", help="instrument [IR,WV,VS]")`. Longwave infrared, visible
and water-vapour imagery sense clouds, surface and tropospheric moisture; that is the lower and
middle atmosphere, not an upper-atmosphere or space-plasma region. A user browsing HSSI for lower and
middle atmosphere software would be glad to find a GOES imagery download-and-plot tool.

The Region vocabulary is flat: no row implies any other, so the broad and the specific value are each
recorded on their own evidence rather than one being inferred from the other.

Considered and rejected: **Earth Ionosphere**, **Earth Thermosphere** and the magnetospheric regions.
The PyHC registry entry for this package (see Field 16) carries the topical tags
`ionosphere_thermosphere_mesosphere`, `solar` and `magnetosphere`, and those tags are the reason
someone might reach for these rows. But the software handles GOES *imager* products only. GOES's
space-environment instruments — the magnetometer, the energetic-particle sensors and the X-ray
sensor, which are what would justify an ionospheric, magnetospheric or solar region — are not read,
parsed, downloaded or plotted anywhere in the tree. Selecting those regions would send space-physics
searchers to a meteorological-imagery utility.

### 6. Authors (MANDATORY)
- **Name:** Michael Hirsch
  - **Author Identifier:** https://orcid.org/0000-0002-1637-6526
  - **Affiliation:** Boston University — https://ror.org/05qwgg493
  - **Affiliation:** Scivision, Inc.

Michael Hirsch is the sole author. He is the only committer on the pinned lineage (33 commits,
2018-02-22 through 2022-08-11, all authored by `Michael Hirsch` / `Michael Hirsch, Ph.D` under
`scivision@users.noreply.github.com`), and the only name in the packaging metadata:
`author = Michael Hirsch, Ph.D.` with `author_email = scivision@users.noreply.github.com` in
`setup.cfg`. The Apache header in `src/goesplot/__init__.py` reads
`Copyright 2020 Michael Hirsch, Ph.D.`, and the PyHC registry entry gives
`contact: Michael Hirsch`. There is no `AUTHORS`, `CONTRIBUTORS` or `CITATION.cff` file to
corroborate or extend this, and no second contributor to add.

The ORCID and both affiliations are carried over from the existing HSSI record — the repository
itself carries no ORCID and no institutional affiliation, so they cannot be re-derived from the
source. The ORCID was independently confirmed on 2026-08-30 against the public ORCID API, which
resolves `0000-0002-1637-6526` to given name `Michael`, family name `Hirsch`.

The name recorded here is `Michael Hirsch` rather than the `Michael Hirsch, Ph.D.` form used in
`setup.cfg`; the plain form is the correct one for a person record and matches ORCID, and the
post-nominal is a packaging-metadata style choice rather than part of the name.

`Scivision, Inc.` is recorded without a ROR, deliberately. A ROR search for "Scivision" on
2026-08-30 returns a single organisation, `https://ror.org/011qev639` — **SciVision Biotech Inc.
(Taiwan)**, a Kaohsiung biotechnology company at `https://www.scivision.com.tw`. That is a different
entity entirely from the scientific-software consultancy this author works through, and attaching its
ROR would silently misattribute the affiliation. Recorded so the near-miss is not mistaken for a
match in a later refresh; the affiliation stands correctly as a name-only entry.

### 7. Software Name (MANDATORY)
**GOESutils**

This name needs its history on the record, because three different names are all currently live and
each is correct for something different:

| Where | Name | Status |
|---|---|---|
| HSSI record | `GOESutils` | the recorded value |
| PyHC registry (`_data/projects_unevaluated.yml`) | `GOESutils` | curated heliophysics listing |
| PyPI | `goesutils` 1.0.8, uploaded 2018-09-02 | the only artifact this project ever published |
| GitHub repository | `space-physics/GOESplot` | current, archived |
| README title | `# GOES Plot` | current |
| `setup.cfg` at the pin | `name = goesplot`, `version = 1.1.0` | current packaging name |

The packaging name changed repeatedly. Reading `setup.py`/`setup.cfg` at each renaming commit on the
pinned lineage: `GOES_quickplot` (2018-03-06) → `goes-satellite` (2018-08-18) → `goes_quickplot`
(2018-08-19) → `goesutils` at commit d34614d, 2018-09-01, whose subject is `rename` → `goesplot` at
commit f84ca53, 2020-05-04, subject `rename, refactor`. The repository URL moved alongside:
`scivision/goes-quick-plot` → `scivision/goesutils` → `space-physics/GOESplot`. These are all the
same repository — `https://api.github.com/repos/scivision/goesutils` redirects to repository id
122528719, which is `space-physics/GOESplot`.

**The name is `GOESutils`, and that is settled.** It is the name in the curated PyHC registry, which
is the source this HSSI entry's name and logo candidate came from, and which also supplied the three
domain keywords that this refresh removed as unsupported (Field 16). It is likewise the name of the
only installable artifact that exists. A heliophysics user who has encountered this package at all
has most likely met it as GOESutils, so that is the name they arrive with and the name that should
greet them.

The repository name is not thereby hidden, though the routes to it are narrower than they might be.
`GOESplot` reaches a repo-side searcher through Field 3's repository URL and through the name table
above, which is where the rename is explained. Adding it to Field 16 as an alias keyword was
considered and declined — that field holds subject keywords, and the software's own former name is
not a topic it is about; Field 16 records the reasoning. The residual limitation is therefore
deliberate and worth stating plainly: someone searching the bare string `GOESplot` matches this
record through the repository URL and the name history, not through its keywords.

**The caveat that travels with the decision, documented rather than resolved.** This record carries version
1.1.0 in Field 12, and 1.1.0 exists only under the packaging name `goesplot`: commit `f84ca53` changed
the name and the version in a single edit. `pip install goesutils` gets 1.0.8 from 2018. So
"GOESutils 1.1.0" is a name/version pair that never shipped together. That oddity is recorded so a
later reader does not take it for a data-entry slip and "fix" one half of it. It is the price of
naming the entry for the artifact users know while versioning it from the current packaging metadata;
naming it `GOESplot` would trade this oddity for a different one, since that name has no released
artifact at all.

On which names were ever published: `goesplot` was never on PyPI. Checked 2026-08-30 against the
PyPI JSON API for every name this project has used — `GOES_quickplot`, `goes_quickplot`,
`goes-quickplot`, `goes-quick-plot`, `goes-satellite`, `goesutils`, `goesplot` — only `goesutils`
returns 200; the rest, `goesplot` included, return 404. (Only the JSON and Simple APIs prove absence;
PyPI's HTML project page returns 200 behind a bot gate even for packages that do not exist, so a page
that loads is not evidence a package exists.)

### 8. Description (MANDATORY)
Download and plot GOES satellite JPEGs and high-resolution NetCDF4 by date/time. This Python package
provides tools to download GOES (Geostationary Operational Environmental Satellite) preview images at
3-hour cadence and full-fidelity NetCDF4 data at 1-minute cadence from NOAA repositories. The
software includes functionality to plot GOES infrared and other data georegistered on map coordinates
using Cartopy. The preview downloader takes the GOES spacecraft number as a command-line argument,
while georegistration is fixed to the GOES-East longitude slot and the packaged world files and
bundled example data are GOES-13. It can access data from the NOAA NCDC GIBBS service for preview
images and NOAA CLASS for high-resolution data.

The body of this description is the text HSSI held before this refresh, changed only by the two
corrections set out below. Its shape and most of its wording come from the author's own repository
description on GitHub, which is also the `description` field of the PyHC registry entry, so it is the
blurb a user is most likely to recognise; that is why it was edited surgically rather than rewritten.

**The first correction: the GOES-16 clause was replaced.** The text HSSI held before this refresh
asserted "It supports both GOES-13 and GOES-16 satellites." Nothing in the source supports the GOES-16 half of that claim: a pickaxe search over the
whole pinned lineage for the string (`git log -S'goes.?16' --pickaxe-regex -i` against the pin)
returns no commit that ever added or removed it, and a grep of every text file at the pin for a GOES
spacecraft number returns only GOES-13 — the README's worked example, `plot-goes.py`'s docstring,
the GIBBS example URL in `io.py` (`https://www.ncdc.noaa.gov/gibbs/image/GOE-13/IR/2017-08-21-06`),
and both test fixtures (`goes13-IR-2017-07-13-12.jpg`, `goes13.2017.233.080017.BAND_02.nc`). GOES-16
exists for this project as a GitHub repository topic — a label attached to the repository, not a
fact about the code — and, downstream of that, as a keyword. The replacement clause states what the
code actually does: the spacecraft number is a plain integer argument
(`p.add_argument("goessat", help="number of GOES satellite e.g. 13", type=int)`), while the plotting
side is pinned to one orbital slot (`GS = cartopy.crs.Geostationary(-75.0)`) and the packaged world
files are `GOES_EAST_*` with `STEM = "GOES_EAST_"  # FIXME: make auto per satellite` in `io.py`. This
is a correction of a factually unsupported statement, not a stylistic rewrite. See Field 32, where
the same evidence bears on the observatory associations.

**The second correction: "PNGs" became "JPEGs".** The opening sentence previously said PNG, and the
preview files this software downloads are JPEG. The evidence is unambiguous and sits in three places
at the pin: the README lists
`* [preview .jpg](https://www.ncdc.noaa.gov/gibbs/), 3 hour cadence`; `get-goes-preview.py`'s
docstring says `* 3-hour JPG low-resolution previews`; and `dl_goes()` writes
`fn = outdir / f"goes{goes:d}-{mode}-{dgoes}.jpg"`. Accuracy was chosen over fidelity to inherited
wording, on the same principle that decided the keyword removals in Field 16: a description that
misstates the delivered format misleads the reader it is written for.

**That correction creates a divergence from upstream, and the divergence is deliberate.** The word
"PNG" is the author's own, and it is what both the GitHub repository description and the PyHC
registry entry display. HSSI's description now differs from both by that one token, on purpose. Two
consequences a later agent needs: first, do **not** "resynchronise" this sentence to the upstream
blurb — the divergence is the correction, not drift. Second, do **not** adjust Fields 18/19 toward
PNG on the strength of any wording; the delivered preview format is JPEG, recorded there as `Other`
because the FileFormat vocabulary has no JPEG row.

### 9. Concise Description (OPTIONAL)
Quick Python script to download and plot GOES satellite preview and hi-resolution data by date/time.

This is the README's own one-line summary at the pin, quoted exactly. Kept unchanged: it is 100
characters, well inside the 200-character limit, it is the author's phrasing, and it previews the
software accurately.

### 10. Publication Date (RECOMMENDED)
**2018-02-22**

The repository's creation date (`created_at` = `2018-02-22T20:01:47Z`, GitHub API, verified
2026-08-30) and the date of the first commit on the pinned lineage, `a88a7f8` "Initial commit". These
agree, so the date is firm. It is not a release date — the first PyPI upload was 2018-09-02 and the
only GitHub release, `v1.0.8` "Initial Release", was published 2018-08-19 — but Field 10 asks for
first publication of the software, and public availability began when the repository did.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

Correct by the field's own rule: no DOI has been obtained (Field 2), so the publisher is the
repository host. Zenodo would be wrong here — there is no Zenodo deposit.

### 12. Version (RECOMMENDED)
- **Version Number:** 1.1.0
- **Version Date:** 2020-05-04
- **Version Description:** rename, refactor
- **Version PID:** Not found

`setup.cfg` at the pin declares `version = 1.1.0`, and that value was introduced by commit `f84ca53`
on 2020-05-04, whose subject line is `rename, refactor` — the source of the version description. The
same commit renamed the package: immediately before it, `setup.cfg` read `name = goesutils` with
`version = 1.0.8`, and f84ca53 changed both lines together — which is why version 1.1.0 has only ever
existed under the name `goesplot` (Field 7). The version has not changed since; the three later
commits on the lineage (`5a7e601` and `7ae4b0a`, both 2021-04-27, the `src/` layout move and numpy
type annotations, and `fa4e4d3`, 2022-08-11, the pin) left it alone.

**Do not "reconcile" this down to the git tag.** The repository carries exactly one tag, `v1.0.8`
pointing at `22b7940` (2018-08-19), which is an ancestor of the pin — verified with
`git merge-base --is-ancestor`, so it sits on the real lineage and is not an orphan. That tag is
*older* than the declared version, and it matches the single PyPI release (`goesutils` 1.0.8, sdist
uploaded 2018-09-02T01:46:57Z). The declared 1.1.0 was simply never tagged or published; the
packaging metadata is nevertheless the software's own statement of its version and is the right value
for this field. A future agent seeing "latest tag v1.0.8" should not treat it as newer information.

No version PID: there is no DOI of any kind for this software (Field 2), so there is nothing
version-specific to record.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x**

`setup.cfg` declares `python_requires = >= 3.7` and the classifier
`Programming Language :: Python :: 3`; all source code in the tree is Python. `Python 2.x` does not
apply — the pin's final commit is titled "python >= 3.7 type annotation" and `io.py` opens with
`from __future__ import annotations`, using PEP 585 built-in generics (`list[datetime]`,
`tuple[str, list[str]]`) that Python 2 cannot parse. No other language appears in the tree.

### 14. Reference Publication (OPTIONAL)
Not found.

There is no paper describing this software. No JOSS submission, no `paper.md`, and no citation
instruction anywhere in the pinned tree. Searched 2026-08-30: DataCite returns 0 results for
`goesplot OR goesutils`; OpenAlex finds the package name in exactly one work, and only via full-text
match, never in a title or abstract — see Field 27, where that work is assessed and rejected.

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** https://spdx.org/licenses/Apache-2.0

Four independent sources agree and none dissents. `LICENSE.txt` at the pin is the full, unmodified
Apache License 2.0 text. `src/goesplot/__init__.py` carries the standard Apache header —
`Licensed under the Apache License, Version 2.0 (the "License");` — above
`Copyright 2020 Michael Hirsch, Ph.D.`. `setup.cfg` points at the file with
`license_files =` / `  LICENSE.txt`. GitHub's licence detection reports SPDX `Apache-2.0`
(verified 2026-08-30).

`Apache License 2.0` is the exact spelling of the HSSI vocabulary row, whose identifier is
`https://spdx.org/licenses/Apache-2.0`; that identifier is recorded rather than
`https://www.apache.org/licenses/LICENSE-2.0`, which a previous extraction used — both name the same
licence, but the SPDX URL is the one the controlled list carries.

Two traps worth leaving on the record. `setup.cfg` has **no** `License ::` classifier, so a
classifier-driven extractor will report no licence for this package; that is an absence of metadata,
not an absence of licensing. And PyPI's metadata for `goesutils` 1.0.8 has an **empty** `license`
field — again a packaging gap, not a licensing fact. HSSI held no licence value for this software
before this refresh, which is consistent with an earlier pass having trusted one of those two empty
fields.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- atmospheric science
- goes
- goes13
- goes16
- noaa
- satellite
- space weather

Provenance of each: `goes` and `satellite` are the author's own, from `setup.cfg`'s `keywords` block
(and they match the PyPI metadata's `keywords = 'goes,satellite'`). `goes13`, `goes16` and `noaa` are
the repository's GitHub topics, verified live on 2026-08-30 as exactly
`['goes13', 'goes16', 'noaa']`. `atmospheric science` derives from `setup.cfg`'s classifier
`Topic :: Scientific/Engineering :: Atmospheric Science`. `space weather` has no upstream source; it
was added editorially in an earlier pass and is kept, because GOES is the platform a space-weather
user expects to see named even though the imager products themselves are meteorological. Every
keyword recorded here is a subject term; none is an alias for the software's own names.

The PyHC entry, fetched 2026-08-30 from
`https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects_unevaluated.yml`,
reads in full:

```
- name: GOESutils
  code: https://github.com/space-physics/GOESplot
  description:  Download and plot GOES satellite PNGs and high-resolution NetCDF4 by date/time
  logo: https://raw.githubusercontent.com/space-physics/GOESplot/master/src/goesplot/tests/goes13-IR-2017-07-13-12.jpg
  contact: Michael Hirsch
  keywords: ["ionosphere_thermosphere_mesosphere","solar","magnetosphere","specific"]
```

Two things follow. First, the registry's fourth tag, `specific`, is deliberately **not** carried over:
it is a PyHC-internal classification marker, not a subject keyword, and it would be meaningless as an
HSSI search term. Second, this package appears only in `projects_unevaluated.yml` — checked on the
same date, it is absent from both `_data/projects_core.yml` and `_data/projects.yml`. Pin any future
registry claim to that specific file; "the PyHC registry" is three lists, not one.

**Three PyHC domain keywords were dropped in this refresh, and should not be reinstated.** HSSI held
`ionosphere_thermosphere_mesosphere`, `solar` and `magnetosphere` before this refresh; they reached
the record from the PyHC entry quoted above, alongside the name and the logo candidate. Each names a
physical domain whose data this software does not touch. The package reads GOES imager products —
infrared, visible and water vapour — while GOES's magnetometer, energetic-particle and X-ray
instruments appear nowhere in the tree; Field 22 reaches the same finding from the phenomena side,
independently. A user filtering HSSI on `magnetosphere` and being handed a weather-imagery downloader
is a false positive, and that is the test that settles it. The removal is documented here rather than
performed silently precisely because the PyHC entry remains upstream and carried those tags when it
was fetched on 2026-08-30: a later refresh that reads the registry afresh must recognise them as
known, considered and rejected, not as new evidence.

**`goes16` is kept as a keyword**, even though the GOES-16 observatory association was removed in the
same refresh (Field 32). That is a consistent reading, not an inconsistency, because the two fields
make different claims. A keyword records how the author labelled his own project — `goes16` is one of
his three GitHub topics — and a loose keyword match costs a searcher little. A Field 32 entry asserts
that the software is *designed to support* that spacecraft, which is a claim the source cannot bear.
The weaker claim survives evidence that defeats the stronger one.

Considered and not added: `geostationary`, `weather satellite`, `GIBBS`, `NOAA CLASS`. The first two
are largely covered by `goes` and `satellite`, and the two archive names are recorded properly in
Field 17 and in the surrounding prose.

`GOESplot` was considered as a keyword and rejected. The temptation is real: Field 7 settles the
software name as `GOESutils`, while the repository, the README title and the current packaging name
are all GOESplot, and that name does not appear in the Field 8 description text either — so a keyword
would have been the one place in this record where someone searching the string `GOESplot` could
match. It was declined because this field holds *subject* keywords, terms describing what the
software is about, and an alias for the project's own repository name is not a topic. Admitting it
would make the keyword set do two unrelated jobs at once and would license the same move on every
renamed package.

The navigational consequence is real and is left on the record rather than papered over: **a searcher
who knows this software only as `GOESplot` will not match it on keywords.** They reach it through
Field 3's repository URL and through the name history in Field 7, which is where the rename is
explained. A future agent noticing that gap should recognise it as a known and accepted cost of
keeping Field 16 to subject terms, not as an oversight to fix by adding the alias.

### 17. Data Sources (OPTIONAL)
- **HTTP/HTTPS Directories**
- **FTP/FTPS Directories**
- **Observatory/Mission-specific**

`HTTP/HTTPS Directories`: `dl_goes()` builds GIBBS URLs from
`STEM = "https://www.ncdc.noaa.gov/gibbs/image/GOE-"` and fetches them with `requests`
(`R = requests.head(url, allow_redirects=True, timeout=10)` then a `requests.get`).
`FTP/FTPS Directories`: `get_hires()` uses `ftplib` against a NOAA CLASS host, defaulted in
`get-goes-hires.py` as `p.add_argument("-host", help="FTP host", default="ftp.class.ngdc.noaa.gov")`,
with a deliberate `sleep(0.5)  # anti-leech` between retrievals.
`Observatory/Mission-specific`: both services are GOES-specific NOAA products rather than
general-purpose archives, which is the cross-listing Field 17 calls for when a software supports a
named mission's own data path.

None of the remaining vocabulary rows applies — the package speaks to no AMDA, CDAWeb, das2, GFZ,
HAPI, Madrigal, OMNIWeb, S3/cloud, SSCWeb, TAP, Virtual Solar Observatory, VirES or WDC endpoint, and
`Other` would add nothing on top of the three specific rows already selected.

**Durable upstream limitation, observed 2026-08-30 (not a permanent claim about NOAA).** All three
of the software's data endpoints were unreachable from this network on that date:
`ftp.class.ngdc.noaa.gov` (the default FTP host) had no DNS record via public resolver 8.8.8.8;
`www.class.ncdc.noaa.gov` (the NOAA CLASS URLs printed in the README) likewise had no DNS record; and
`https://www.ncdc.noaa.gov/gibbs/…` 301-redirects to `https://www.ncei.noaa.gov/gibbs/…`, which did
not respond within 25 seconds on repeated attempts, although `https://www.ncei.noaa.gov/` itself
answers promptly. NOAA reorganised these services after the software was archived. The Data Sources
values remain correct as a description of what the software is built to talk to; a future refresh
should not read them as a claim that those endpoints are live, and should re-test rather than assume
either state.

### 18. Input File Formats (RECOMMENDED)
- **netCDF3/4**
- **ascii**
- **Other**

`netCDF3/4`: `loadhires()` opens `with netCDF4.Dataset(fn, "r") as f:` and reads the `time`, `lon`,
`lat` and `data` variables; the bundled fixture is `goes13.2017.233.080017.BAND_02.nc` and
`test_load_hires` asserts `img.shape == (1100, 2500)` on it.
`ascii`: the three `data/*.wld` world files are six-line plain-text files parsed with
`wld = np.loadtxt(fn)`, and `parse_email()` reads a plain-text NOAA CLASS order email line by line to
recover the FTP directory and file list.
`Other`: the preview images are JPEG. `load()` dispatches on `if fn.suffix == ".jpg":`, `loadpreview()`
reads them with `imageio` (`img = iio.imread(fn)`), and `test_load_preview` asserts
`img.shape == (1200, 1200, 3)`. The FileFormat vocabulary has no JPEG row, so `Other` is the correct
representation — this is what `Other` is for, not a placeholder for something unexamined.

Considered and rejected: **HDF5**. NetCDF-4 files are physically HDF5 containers, so an automated
sniffer might propose it, but the vocabulary lists `netCDF3/4` and `HDF5` as separate rows and the
software reads these files strictly through the netCDF API. Recording HDF5 would imply a general HDF5
capability the package does not have. **csv**, **CDF**, **FITS**, **JSON**, **IDL.sav**,
**ISTP-Compliant** and **Zarr** have no basis anywhere in the tree.

### 19. Output File Formats (RECOMMENDED)
- **netCDF3/4**
- **Other**

These are the formats of the files the software writes to disk, and the nuance matters enough to
record precisely. The package does not serialise any derived product. What it writes is what it
retrieved, byte for byte: `get_hires()` streams FTP content straight to disk
(`F.retrbinary(f"RETR {rfn}", h.write)`), producing NetCDF files; `urlretrieve()` writes the fetched
GIBBS response body (`f.write(R.content)`) to a `.jpg` path, which is the JPEG covered by `Other`,
exactly as in Field 18. Figures are shown interactively — `plot-goes.py` calls
`show()` after each `plotgoes()` — and are never written to a file by any code path in the tree.

A stricter reading is possible and was considered: that a program which only mirrors downloads has no
output formats at all, and this field should be empty. It is not adopted, because the files do come
into existence through the software and a user who runs it ends up with `.nc` and `.jpg` files on
disk; a searcher filtering for netCDF output is not misled by that, only by an expectation of derived
products, which this note exists to correct.

### 20. Operating System (RECOMMENDED)
- **Operating System Independent**
- **Linux**

`Operating System Independent` is the author's own declaration —
`setup.cfg` carries the classifier `Operating System :: OS Independent` — and is consistent with the
code, which is pure Python using `pathlib` throughout and no platform-specific calls or compiled
extensions. `Linux` records where the software is actually exercised: `.github/workflows/ci.yml`
defines a single job with `runs-on: ubuntu-latest`, `python-version: '3.8'`, installing
`.[tests,lint,io]` and running flake8, mypy and pytest.

`Mac` and `Windows` are not recorded. Nothing forbids them and the OS-independent claim covers them
in principle, but no CI job or documentation demonstrates either, and the two values already recorded
say both what is claimed and what is verified.

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

Pure Python with no compiled extension modules, no architecture-specific code, and no build step
beyond `setuptools`/`wheel` (`pyproject.toml`: `requires = ["setuptools", "wheel"]`). Nothing in the
tree targets GPU, HPC, aarch64, ppc64le, SPARC or any other specific architecture.

### 22. Related Phenomena (OPTIONAL)
Not found — evidenced empty, not unexamined.

The whole Phenomena vocabulary was reviewed against this software: Coronal Heating, Coronal Mass
Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission. Every row is a
solar, heliospheric or geomagnetic phenomenon. This software downloads and plots GOES imager
products — clouds, water vapour and surface/cloud-top brightness temperature — and computes nothing
about any of those phenomena.

The near-miss worth recording, so it is not re-proposed: **X-ray emission** looks apt because GOES
carries the Solar X-ray Sensor whose flux defines the standard flare classification. This software
does not read XRS data. Its two loaders handle a GIBBS browse JPEG and a GVAR-era imager NetCDF
file, and a grep of every text file at the pin for `xrs`, `x-ray`, `magnetomet` and `particle`
matches nothing — no X-ray product is downloaded, parsed or plotted. The Phenomena vocabulary is
flat, so there is also no broader row that could be selected as an approximation. An empty value is
the correct outcome here.

### 23. Development Status (RECOMMENDED)
**Unsupported**

The repository is archived on GitHub — `archived: true`, verified 2026-08-30 — and its last push is
the pinned revision, `pushed_at` = `2022-08-11T14:02:49Z`. Archiving makes a repository read-only:
issues and pull requests can no longer be opened, so no support can be provided even in principle.
The software did reach a stable, usable, released state (a tagged `v1.0.8` GitHub release titled
"Initial Release" in August 2018 and a PyPI sdist in September 2018). Matching those two facts to
the vocabulary's own definitions, `Unsupported` is the row that fits: *"The project has reached a
stable, usable state but the author(s) have ceased all work on it. A new maintainer may be desired."*

Rejected alternatives, with reasons:

- **Inactive** — *"…no longer being actively developed; support/maintenance will be provided as time
  allows."* The first clause is true but the second is false for an archived repository, where a user
  cannot even file an issue. `Inactive` would leave a searcher with a more optimistic expectation
  than the project can meet. This is the closest alternative and a reasonable person could choose it;
  the archived state is what tips it.
- **Abandoned** — requires that there *not yet* have been a stable, usable release. There was one, so
  this row does not describe the project despite the everyday sense of the word.
- **Moved** — no successor project exists; the renames all happened within this same repository
  (Field 7), which is not what `Moved` means.
- **Active** — **wrong**, and worth pinning down whose value it was. HSSI held no development-status
  value at all for this software before this refresh; `Active` was recorded by the earlier extraction
  of 2025-12-03, never by the live record. It rested on two pieces of bad evidence:
  `setup.cfg`'s classifier `Development Status :: 4 - Beta`, which is the author's
  2018-era self-description and says nothing about current maintenance, and a "last updated
  2024-06-22" figure taken from automated tooling output. GitHub's own `pushed_at` of 2022-08-11
  contradicts that date, and the repository is archived. Recorded here so the same inference is not
  made again from the same classifier.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/GOESplot

There is no documentation site. The repository has no `docs/` directory, no Sphinx or ReadTheDocs
configuration, and GitHub Pages is not enabled (`has_pages: false`, verified 2026-08-30). All user
documentation is the README plus the module and CLI docstrings, and the two carry different
material: the README explains ordering data through the NOAA CLASS shopping cart and warns that
"It may take up to 48 hours to get access to your order.", while `get-goes-hires.py`'s docstring
gives the four numbered steps for turning the resulting CLASS email into an input file for the
downloader. The repository URL is therefore the correct and complete documentation link, and its
being identical to Field 3 is a fact about this project rather than an oversight.

Related observation for a future editor: the README's inline image reference
`![goes absorption](tests/goes13-IR-2017-07-13-12.jpg)` is **broken at the pin**. The file moved to
`src/goesplot/tests/` in the 2021-04-27 `src/` layout commit (`5a7e601`) and the README path was
never updated; the old path returns 404 on raw.githubusercontent.com. Likewise the README's download
badge, `[![PyPi Download stats](http://pepy.tech/badge/goesplot)](http://pepy.tech/project/goesplot)`,
points at a project name never published to PyPI — `https://pepy.tech/project/goesplot` returns 404.
Neither can be fixed upstream now that the repository is archived; both are recorded so they are not
mistaken for extraction errors.

### 25. Funder (OPTIONAL)
Not found.

No funding statement, acknowledgement, grant number, sponsor or agency attribution appears anywhere
in the pinned tree — a grep of every text file for `fund`, `grant`, `award`, `acknowledg`, `NSF`,
`NASA` and `sponsor` matches nothing outside the Apache licence's own use of "grant"/"granted". There
is no paper whose acknowledgements section could supply one (Field 14), and no DOI record to consult
(Field 2). This is a small personal utility, and an absent funder is the expected outcome rather than
a gap in the search.

### 26. Award Title (OPTIONAL)
Not found.

Follows directly from Field 25: with no funder identified and no publication or DOI record to draw
on, there is no award to record.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found.

Negative research, so a future refresh does not repeat it. A full-text search of OpenAlex on
2026-08-30 finds the package name in exactly one work — *Python in Heliophysics Community (PyHC):
Current status and future outlook*, https://doi.org/10.1016/j.asr.2022.10.006 — and only on full
text; a title-and-abstract search returns zero. That paper is an ecosystem survey of the PyHC project
inventory. Naming a package in a community-wide survey is a passing mention, not a publication that
describes, uses or substantively cites the software, and the same entry would be equally true of
any package in the PyHC lists, so it carries no information about *this* software. It is therefore
considered and not recorded.

The same check was run on the other current-era name, for the same completeness reason the Field 2
sweep gives. OpenAlex searched for `goesplot` on 2026-08-30 returns a single work, *Physics of the
Analytic S-Matrix* (`https://doi.org/10.48550/arxiv.2306.05395`), which is a theoretical particle
physics text and does not contain the string at all — search-relevance noise rather than a citation.
Recorded so a later agent who re-runs that query recognises the hit for what it is instead of
investigating it. DataCite and Zenodo return nothing for either project name.

### 28. Related Datasets (OPTIONAL)
Not found.

The software consumes two NOAA data services: GIBBS browse imagery and NOAA CLASS full-fidelity GOES
imager data. Neither is recorded here, and the reason is worth keeping. Field 28 takes a URL per
entry, ideally a DOI or a permanent dataset landing page. The GIBBS previews are a browse product
rather than a citable dataset, and both services' endpoints were unresolvable on 2026-08-30
(see Field 17), so no permanent landing page for the exact products this software retrieves could be
verified. NCEI does publish DOI-bearing gridded climate data records derived from the same underlying
ISCCP B1 archive, but those are different, re-gridded products that this software neither downloads
nor reads — recording one would assert a dataset relationship that does not exist. The service
relationship is captured accurately in Field 17 instead.

### 29. Related Software (OPTIONAL)
Not found — see the reasoning below, and the tier analysis at the end of Field 30.

HSSI held four entries in this field before this refresh — `matplotlib`, `xarray`, `cartopy` and
`netcdf4-python` — and all four were removed. All four are dependencies, and being a dependency is not what this field records. Field 29 is for
software that *distinguishes* this package — a tool doing a similar job, a predecessor or fork
parent, a companion package, or a domain-specific dependency whose presence characterises the
software. The generic scientific-Python stack is excluded from Field 29 on exactly the same terms as
from Field 30, and `matplotlib` and `cartopy` are named in that exclusion; `netCDF4` is generic I/O
plumbing that would be equally at home in a climate model, a biology pipeline or a web service.
`xarray` earns a place in Field 30 on specific evidence (below) but is not a similar-purpose tool, a
predecessor or a domain library, so it does not belong here.

The genuinely relevant candidates for this field would be *other GOES data-access packages* — that is
what "software that performs similar tasks" means here, and such packages do exist in the wider
Python ecosystem. None is recorded because this repository points at none: the README, the module
and CLI docstrings, and the commit subjects on the pinned lineage name no other GOES access package.
Any entry would therefore be an outside assertion that two packages are similar rather than evidence
about this software, and Field 29 entries should be traceable to the software itself. If
a curator with domain knowledge wants to name a peer package, that is a legitimate editorial addition
— it is simply not something this extraction can evidence.

Predecessor check, since Field 29 explicitly covers forks and predecessors: there is none. The
project's earlier names (`GOES_quickplot`, `goes-satellite`, `goes_quickplot`, `goesutils`) are all
prior names of *this same repository*, not separate works — see Field 7. There is nothing to link to.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/pydata/xarray

**xarray qualifies on a documented public-API exchange, not on being a dependency.** The package's
entire public surface is three functions — `src/goesplot/__init__.py` is
`from .io import load, get_hires, get_preview` — and the primary one declares an xarray return type:
`def load(fn: Path, downsample: int = None, wld: Path = None) -> xarray.DataArray:`. Both loaders
construct labelled arrays with named dimensions and coordinates
(`img = xarray.DataArray(img, dims=["lon", "lat", "color"], coords={"lon": lon, "lat": lat, "color": ["R", "G", "B"]})`),
and the plotting entry point consumes the same object:
`def plotgoes(img: xarray.DataArray, verbose: bool = False):`. An `xarray.DataArray` is therefore this
software's documented interchange format — anything a user does with the output, they do in xarray.
That is the specific, cited exchange the field requires, as distinct from internal use.

Excluded across Fields 29 and 30, one standard applied to every candidate. Note which field each was
actually stored in: `matplotlib` and `cartopy` were in both, while `netcdf4-python` was in Field 29
only and never in Field 30.

- **matplotlib** (`https://github.com/matplotlib/matplotlib`) — the rendering library `plots.py` is
  built on. "Uses matplotlib for all plotting" is the field's own canonical example of what does not
  qualify; it is true of a large share of the Python ecosystem and distinguishes nothing.
- **cartopy** (`https://github.com/SciTools/cartopy`) — the map-projection library behind
  `PC = cartopy.crs.PlateCarree()` and `GS = cartopy.crs.Geostationary(-75.0)`. It is central to what
  the plots look like, and it is nevertheless generic mapping infrastructure, named in the same
  exclusion as matplotlib. Consistency is the point: cartopy is excluded on precisely the grounds
  that would otherwise let matplotlib back in.
- **netcdf4-python** (`https://github.com/Unidata/netcdf4-python`) — held under Field 29 only before
  this refresh. It is used strictly internally: `loadhires()` opens `netCDF4.Dataset` and immediately converts
  the contents into an xarray object; no netCDF4 object crosses the public API, and the package's only
  other mention of it is a guard,
  `raise ImportError("netCDF4 needed for hires data.   pip install netcdf4")`. Internal use is
  explicitly not sufficient for this tier. It is also an *optional* extra
  — `setup.cfg`'s `[options.extras_require]` block declares it under `io =` rather than in
  `install_requires` — which makes its previous inclusion alongside four omitted hard requirements
  hard to defend on any consistent rule.

For completeness, the hard requirements that HSSI did not hold before this refresh and that are not
recorded now either, so the standard is visibly uniform: `install_requires` at the pin is `python-dateutil`, `numpy`, `imageio`, `xarray`,
`requests`. Of those, only xarray clears the bar; `numpy`, `requests` and `python-dateutil` are named
generic infrastructure, and `imageio` is generic image I/O plumbing that would be equally at home
outside science entirely. Development extras (`pytest`, `flake8`, `mypy`) are tooling and never
qualify.

**These exclusions are determined by the field definitions, not by curator preference.** Before this
refresh Fields 29 and 30 held nearly the same four packages, which made the distinction between
"related" and "interoperable" invisible to a site visitor and told them nothing they could not read
off a requirements file. Applying the fields' own tiers resolves every candidate without discretion:

- `matplotlib` and `cartopy` are **Tier A** — the "never list these, no exceptions" set. That
  exclusion is not scoped to Field 30; Field 29 applies the same test to the generic stack, so
  neither package can be relocated instead of removed. There is no reading of the rules on which they
  stay in either field.
- `netCDF4` and `xarray` are **Tier B**, admitted only on a documented public-API exchange. `xarray`
  meets that bar by the rule's own qualifying pattern — the documented public return type of
  `load()`, consumed downstream by `plotgoes()`. `netCDF4` fails it by the rule's own disqualifying
  pattern — opened inside `loadhires()`, converted immediately to an xarray object, never crossing
  the public API.

Reinstating the dependency list HSSI held before this refresh is therefore not an available
alternative, and nothing here should be read as inviting a later agent to restore it as a matter of
taste. The one genuine editorial
opening is the one recorded under Field 29: a curator with domain knowledge could add a real GOES
peer package. That is a different act from re-adding generic infrastructure.

### 31. Related Instruments (OPTIONAL)
Not found — a documented omission, reached deliberately.

This software processes GOES **imager** data: GIBBS browse imagery in the infrared, visible and
water-vapour bands, and GVAR-era full-fidelity imager NetCDF from NOAA CLASS. The natural entries
would be the GOES-13 Imager and, if GOES-16 support were real, its Advanced Baseline Imager — and
those two names were in fact proposed by an earlier extraction, without identifiers.

Neither can be represented, because **no GOES Earth-viewing imager exists in the controlled
vocabulary**. Checked upstream at SPASE on 2026-08-30, the instrument directories hold:
`https://spase-metadata.org/SMWG/Instrument/GOES/13/` → Ephemeris, EPS, MAG, SEM, XRS;
`https://spase-metadata.org/SMWG/Instrument/GOES/16/` → Ephemeris, MAG;
`https://spase-metadata.org/NOAA/Instrument/GOES/16/` → SUVI. HSSI's own instrument rows agree — the
GOES instrument rows are ephemeris, magnetometer, energetic-particle, space-environment-monitor and
X-ray sensors, with no ABI row and no Imager row for any spacecraft. That is not an oversight in
SPASE: its scope is heliophysics instrumentation, and the GOES imager is a meteorological instrument.

The two near-misses to leave on the record, since both contain the word "imager" and will attract a
future agent's attention: `https://spase-metadata.org/SMWG/Instrument/GOES/12/SXI` is the GOES-12
**Solar X-Ray Imager**, and the four `.../NOAA/Instrument/GOES/1[6-9]/SUVI` rows are the **Solar
Ultraviolet Imager**. Both are Sun-pointing instruments. Neither has anything to do with the
Earth-viewing imagery this software handles, and selecting either would be a serious mismatch.

Because no row resolves, the correct outcome is to omit the field rather than record a bare name: an
identifier-less instrument entry either binds to an arbitrary same-named row or creates a new
identifier-less row in the vocabulary. The association is not lost — it is carried at the platform
level in Field 32, which is the prescribed substitution when an instrument has no record of its own.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Geostationary Operational Environmental Satellites
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/GOES
- **Observatory Name:** Geostationary Operational Environmental Satellite 13
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/GOES/13

Both names are copied verbatim from the controlled vocabulary rows, and both identifiers are SPASE
resource IDs, as required.

**GOES-13** is the spacecraft the software demonstrably supports. It is the only numbered GOES
spacecraft appearing anywhere in the pinned tree's text files and filenames. The README's worked
example is:

```
example: download IR from GOES-13 2018-01-01 to 2018-01-02 to `~/data/goes13`:

python get-goes-preview.py 13 IR 2018-01-01T00 2018-01-03T00 ~/data/goes13
```

and the same spacecraft recurs in `plot-goes.py`'s docstring, in `io.py`'s GIBBS example URL
`https://www.ncdc.noaa.gov/gibbs/image/GOE-13/IR/2017-08-21-06`, and in both test fixtures —
`goes13-IR-2017-07-13-12.jpg` and `goes13.2017.233.080017.BAND_02.nc`, the latter a GVAR-era filename
whose `BAND_02` band label and `.2017.233.` day-of-year form follow the CLASS convention for the
legacy GOES imager. A user working with GOES-13 imagery would reach for this and be well served.

**The mission-level row is added** because the download path is genuinely fleet-generic, not
GOES-13-only. `get-goes-preview.py` takes the spacecraft as a plain integer,
`p.add_argument("goessat", help="number of GOES satellite e.g. 13", type=int)`, and `dl_goes()`
interpolates it straight into the GIBBS path, so any GOES spacecraft GIBBS serves can be fetched
without touching the code. A visitor browsing the GOES mission and asking what software relates to it
would be glad to find a GOES download-and-plot utility; recording only a single spacecraft would hide
it from exactly that visitor. Note that a second vocabulary row shares this mission-level *name* but
carries the identifier `.../SMWG/Observatory/GOES/4` — a different entity, not a competing candidate
for the same one. The identifier above disambiguates them, which is why it must travel with the name.

**GOES-16 was removed in this refresh.** HSSI held
`Geostationary Operational Environmental Satellite 16`
(`https://spase-metadata.org/SMWG/Observatory/GOES/16`) before this refresh; it is no longer
recorded. The evidence on both sides is kept below, because the association is superficially
plausible and a later agent reading the repository topics alone would be tempted to restore it.

The evidence that decided it:
- The string appears nowhere on the pinned lineage. A pickaxe search over that whole lineage
  (`git log -S'goes.?16' --pickaxe-regex -i` against the pin) returns no commit that ever added or
  removed it, and a grep of every text file at the pin for a GOES spacecraft number returns only
  GOES-13.
- The high-resolution reader is not written for GOES-16 data. `loadhires()` expects the GVAR-era CLASS
  layout — variables `time`, `lon`, `lat` and `data`, indexed as `f["data"][0, ::downsample, ::downsample]`
  — which is not the structure of GOES-16 ABI L1b files. Nothing in the tree reads an ABI product.
- The bundled world files and both fixtures are GOES-13-era, and `io.py` carries the author's own
  admission that generalisation was never done: `STEM = "GOES_EAST_"  # FIXME: make auto per satellite`.
- That value most likely descended from the earlier extraction's ungrounded "GOES-16 Advanced
  Baseline Imager (ABI)" entry in Field 31, resolved up to the observatory level by the standard
  substitution. Resolving an unsupported claim to a valid identifier makes it *postable*, not *true*.

The contrary evidence, and why it did not carry:
- `goes16` is one of the author's own three GitHub repository topics, verified live 2026-08-30 —
  authorial intent, even if aspirational.
- GOES-16 occupied the GOES-East slot from late 2017, so `GS = cartopy.crs.Geostationary(-75.0)` and
  the `GOES_EAST_*` world files are nominally its slot too, and the world files describe GIBBS's fixed
  remapped geographic grid rather than any spacecraft's optics — so the preview path is not obviously
  GOES-16-incapable. (Whether GIBBS ever served GOES-16 could not be established: the service was
  unreachable on 2026-08-30, see Field 17.)

What settled it was the searcher's side. A visitor on a GOES-16 page clicking "show software related
to this observatory" is working with ABI, GLM, SUVI, EXIS or SEISS products. This software reads none
of them; they would install it and find nothing that opens their files. That is precisely the "out of
place" result the association exists to prevent. Nor does the removal orphan the fleet-wide use case,
because the mission-level row recorded above covers it — a GOES searcher still finds this software.

The keyword `goes16` is retained in Field 16, and that is consistent rather than contradictory. A
keyword records how the author labelled his own project and costs a searcher little when the match is
loose; a Field 32 entry asserts that the software is *designed to support* that spacecraft. The
weaker claim survives evidence that defeats the stronger one.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/space-physics/GOESplot/fa4e4d378b50f422450c1c936e2aa770525de18d/src/goesplot/tests/goes13-IR-2017-07-13-12.jpg

**What this image actually is, stated plainly:** it is the package's pytest fixture — it lives in
`src/goesplot/tests/` and `test_load_preview` asserts on it — which the README also reuses as an
illustration. It is a sample GOES-13 infrared frame over North America, not a project logo or mark.
The repository has no logo.

HSSI held no logo for this software before this refresh; this URL fills a field that was empty, so
nothing was displaced by recording it.

It is recorded for reasons that hold from a site visitor's side. The PyHC registry — a curated
heliophysics index, and the same entry this record's name comes from — designates precisely this file
as the project's `logo`, so a heliophysics user has plausibly already seen this image standing for
this package. In an HSSI result list the field's
practical effect is a thumbnail, and a GOES infrared image of North America communicates at a glance
what the software is for, where the counterfactual is a blank thumbnail. Nothing about the image is
misleading — it is a GOES frame standing for a GOES tool. That is why it is recorded.

A strict reading of "logo", on which this field would be left empty because the project has no mark,
was considered and would have been defensible on the same facts; it was not chosen, because a blank
serves no one and this image serves the searcher. The file's true nature is documented above rather
than glossed so that the decision rests on what the image actually is, and so that a later refresh
inherits the reasoning instead of assuming the project has a logo.

On the URL form: the commit-pinned SHA path is used deliberately. PyHC's own URL points at a `master`
branch reference while the repository's default branch is `main`; both resolve today, but the pinned
form cannot break, because a raw URL pinned to a commit SHA resolves to immutable content by
construction. All three forms were fetch-verified on 2026-08-30 and return `content-type: image/jpeg` with
`content-length: 273702` — a real image, not an HTML error page or a Git LFS pointer served as text.
The pinned URL is 144 characters, inside the 200-character limit for a URL field.

---

## Decisions settled in this record

Each of these is argued in full under its field. They are collected here so a reader sees the whole
decision surface at once, and so that a later refresh meeting the same evidence recognises them as
closed rather than reopening them.

1. **Field 7 — the software name is `GOESutils`.** It is PyHC's name for the package and the name of
   the only distribution this project ever published to PyPI, so it is the name a heliophysics user
   arrives with. The repository name stays reachable through Field 3 and through Field 7's own name
   history; an alias keyword in Field 16 was considered and declined, because that field holds
   subject terms rather than the software's other names. The "GOESutils 1.1.0" name/version pair, which never shipped
   together, is documented under Field 7 as a known consequence of that choice rather than an error
   awaiting repair.
2. **Fields 29 and 30 — the dependency entries are excluded by the field definitions, not by
   preference.** `matplotlib` and `cartopy` are Tier A, the "never list these, no exceptions" set,
   and that exclusion covers Field 29 as well, so neither can be relocated instead of removed.
   `netCDF4` and `xarray` are Tier B: `xarray` meets the documented public-API exchange test and is
   recorded in Field 30, while `netCDF4` fails it, being converted internally and never crossing the
   public API. Reinstating the dependency list HSSI held before this refresh is not an available
   option. The one genuine
   editorial opening, recorded under Field 29, is that a curator with domain knowledge could add a
   real GOES peer package — a different act from re-adding generic infrastructure.
3. **Field 32 — GOES-16 removed, the mission-level GOES row added, GOES-13 kept.** No revision on the
   pinned lineage names GOES-16, and the high-resolution reader does not read ABI products, so the
   association would have handed GOES-16 searchers a tool that opens none of their files. The mission-level row
   keeps the fleet-wide download capability discoverable to a GOES searcher.
4. **Field 16 — the three PyHC domain keywords removed.** `ionosphere_thermosphere_mesosphere`,
   `solar` and `magnetosphere` each name a domain this software's data do not cover, so each would
   surface this entry as a false positive. `goes16` stays, because a keyword records how the author
   labelled his own project and makes a weaker claim than a Field 32 association. `GOESplot` was
   considered as an alias keyword and rejected, keeping this field to subject terms; Field 16 records
   the navigational cost that choice accepts.
5. **Field 8 — "PNGs" corrected to "JPEGs".** The delivered preview format is JPEG on the evidence of
   the README, the downloader docstring and the write path. Accuracy was chosen over fidelity to the
   inherited blurb, which leaves this description one token away from the GitHub and PyHC wording by
   design. Field 8 records why that divergence must not be resynchronised away, and why it must
   not be used to push Fields 18/19 toward PNG.
