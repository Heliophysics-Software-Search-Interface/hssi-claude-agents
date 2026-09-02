# HSSI Metadata Extraction Results

**HSSI Software ID:** 30f42aa0-cca9-4cb7-8479-7149e5f20112
**Repository:** https://github.com/space-physics/igrf
**Source Revision:** c418dd6940560d158568ebf35243266b92d09bf9
**Extraction Date:** 2026-09-01
**Validation Date:** 2026-09-02
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

**This entry is a third-party Python/Matlab *implementation* of the IGRF-13 generation, not the model
itself.** The three catalogue records tabulated below all carry names built on "IGRF" and are three
different kinds of thing. Confusing them is the easiest mistake to make here:

| Record | What it actually is |
|---|---|
| **IGRF-13** (this entry) | `space-physics/igrf` — Michael Hirsch's MIT-licensed Python package with a Matlab interface, wrapping the IAGA V-MOD Fortran synthesis routine for the 13th generation of the model. Source code, PyPI package, Zenodo software DOI. |
| **IGRF-14** | The IAGA-published **model coefficient release** on Zenodo, landing at `https://www.ncei.noaa.gov/products/international-geomagnetic-reference-field`. Data files, no source code, no build system. Not a software project. |
| **igrfpy** | `lkilcommons/igrfpy` — a separate, unrelated third-party Python wrapper around the IGRF-11 and IGRF-12 Fortran routines. |

Two consequences run through this file. First, evidence about *the model* — its application domains,
its coefficient releases, its defining papers — is not automatically evidence about *this software*,
and each field below says which of the two it rests on. Second, a relation to one of the sibling
records is not automatically symmetric; see Field 29.

**Only IGRF-13 is on this package's build path.** `src/igrf/CMakeLists.txt` at the pinned revision
builds exactly one target, `add_executable(igrf13_driver fortran/igrf13_driver.f90 fortran/igrf13.f)`,
and `MANIFEST.in` ships only `src/igrf/fortran/igrf13_driver.f90`, `src/igrf/fortran/igrf13.f` and
`src/igrf/CMakeLists.txt`. The repository also carries `igrf11.f`, `igrf11_driver.f`, `igrf12.f`,
`igrf12_driver.f`, `igrf13_legacy.f`, `IGRF12.COF` and `WMM2015.COF`, none of which the current Python
or Matlab API can reach; the `model=11` and `model=12` tests in `src/igrf/tests/test_mod.py` are
commented out, and the keyword they exercised no longer exists. Several fields below turn on this
distinction between *present in the tree* and *reachable by a user*.

**Durable upstream limitation — the console script is misnamed, and it is a regression.**
`pyproject.toml` declares `[project.scripts]` as `findssh = "igrf.__main__:cli"`, the name of a
different package by the same author. The README tells the reader to run `igrf` to reproduce its
example plots, but the packaging metadata installs that entry point as `findssh`; `python -m igrf`
works regardless. The history shows how it happened: the same 2024-08-23 commit that migrated the
project from `setup.cfg` to `pyproject.toml` introduced the `findssh` line, while the `setup.cfg` it
deleted had carried the correct `console_scripts` entry `igrf = igrf.__main__:cli` — and that commit
also commented out `test_cli`, the one test that would have caught the breakage. This is an upstream
defect at the pinned revision, recorded once here so that no field's prose claims a working `igrf`
command. It is not a metadata error to correct on our side.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

Not part of the software's descriptive metadata; supplied by whoever transmits the record. The
placeholder is this catalogue's convention for the field, not an unfilled gap.

### 2. Persistent Identifier (RECOMMENDED)
`https://doi.org/10.5281/zenodo.1184871`

This is the Zenodo **concept** DOI, which is what this field asks for — the concept DOI for all
versions. Its correctness is established by the Zenodo record itself: the record reached through this
DOI is version record `5560949`, whose `conceptrecid` is `1184871` and whose `conceptdoi` is
`10.5281/zenodo.1184871`, with the version DOI `10.5281/zenodo.5560949` recorded separately in
Field 12. Concept and version DOIs are both kept in this file so a future agent does not mistake one
for the other.

**The README badge is not the source, and reading it as one is a trap.** The badge is
`[![DOI](https://zenodo.org/badge/33064474.svg)](https://zenodo.org/badge/latestdoi/33064474)`, keyed
on the GitHub repository's numeric id (33064474, confirmed as this repository's `id`). That badge
target redirects to `https://doi.org/10.5281/zenodo.5560949` — the **latest version** DOI, not the
concept DOI. A refresh that harvests the badge will therefore produce the wrong kind of DOI for this
field. The concept DOI has to come from the Zenodo record's `conceptdoi`.

**The deposit is automated, which is also why Field 11 is Zenodo.** The version record carries
`related_identifiers: [{"identifier": "https://github.com/space-physics/igrf/tree/v13.0.2",
"relation": "isSupplementTo", "scheme": "url"}]`. An `isSupplementTo` pointing at a `/tree/<tag>` URL
is the signature of the GitHub–Zenodo release integration rather than of a manual upload.

**Negative research worth keeping: a creator-keyed DOI search cannot find this record.** The Zenodo
record's sole creator is the bare string `Michael`, with `affiliation: null` — no surname at all. A
sweep keyed on any spelling of "Hirsch" misses it entirely. Anyone re-testing a "does this software
have a DOI?" question on this or another `space-physics` package must search by title or by repository
path, not by creator name.

**Zenodo's own licence value must not be copied.** The record reports `license: {"id": "other-open"}`,
a Zenodo generic. The licence in Field 15 is re-derived from `LICENSE.txt` at the pinned revision.

### 3. Code Repository (MANDATORY)
`https://github.com/space-physics/igrf`

The canonical location, and the URL is live. Confirmed by the local clone's `origin` remote, by
`pyproject.toml`'s package name `igrf`, and by the GitHub API's `full_name: space-physics/igrf` with
`fork: false` and `archived: false`. The default branch is `main`, and the pinned revision
`c418dd6940560d158568ebf35243266b92d09bf9` is that branch's tip. The same URL is the PyHC registry's
`code:` value and PyPI's `Homepage`.

### 4. Software Functionality (RECOMMENDED)
- Coordinate Transforms
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Models and Simulations
- Models and Simulations: Empirical

**`Models and Simulations: Empirical`** is the core classification, and `Models and Simulations` is
listed alongside it because a subcategory never implies its parent in this field. IGRF is a
spherical-harmonic representation of Earth's main field whose coefficients are fitted to observations
rather than derived from the physics of the geodynamo. `src/igrf/fortran/igrf13.f` describes itself as
a synthesis routine for the 13th generation IGRF as agreed in December 2019 by IAGA Working Group
V-MOD, valid from 1900.0 to 2025.0 inclusive, with values from 1945.0 to 2015.0 inclusive definitive
and others non-definitive. The coefficients are compiled in as Fortran `data` tables (`gh(3645)` and
the twenty-six `g0`-through-`gs` blocks that are equivalenced onto it), so nothing is fitted or
ingested at run time.

**`Data Processing and Analysis: Analysis`**, with its parent, covers the derived quantities the
package computes on top of raw model output. `src/igrf/utils.py`'s `mag_vector2incl_decl` derives
magnetic declination and inclination from the north/east/down vector (`arctan2(y, x)` and
`arctan2(z, hypot(x, y))`, converted to degrees), and it is one of the three utility functions
`src/igrf/__init__.py` exports publicly. Both `igrf()` and `grid()` add `incl` and `decl` to every
returned dataset, so the derivation is not optional.

**`Data Visualization: 2D Graphics`**, with its parent, is earned by `src/igrf/plots.py`. `plotigrf`
draws contour maps of the north, east and down components and of total intensity over a
latitude/longitude grid, plus a second figure of "Magnetic Declination [degrees]" and
"Magnetic Inclination [degrees]" contours; `src/igrf/__main__.py` calls it and then `show()`. The two
images the README embeds, `src/igrf/tests/incldecl.png` and `src/igrf/tests/vectors.png`, are output
of exactly this code path — they are example plots, not logos (see Field 33).

**`Coordinate Transforms`** is included because what the package exposes is a genuine
geodetic/geocentric choice rather than a unit change:
`igrf13.f` documents `alt` as "height in km above sea level if itype = 1" and as
"distance from centre of Earth in km if itype = 2 (>3485 km)", with `itype` selecting
"1 if geodetic (spheroid)" or "2 if geocentric (sphere)"; the `itype = 1` branch of the routine
performs the "conversion from geodetic to geocentric coordinates" "(using the WGS84 spheroid)" and
rotates the output components back into the local geodetic frame. That choice reaches the user
directly — `igrf()` and `grid()` in `src/igrf/base.py` both take `itype` as a keyword-only argument
and pass it to the driver, and the command line exposes `--itype` with the help text
"1: geodetic. 2: geocentric". Separately, `latlon2colat`, which converts geographic latitude and
longitude to colatitude and east-longitude, is one of the publicly exported utilities.
*The counter-argument, recorded because it is respectable:* this is a mode switch and a four-line
helper, not a coordinate library, and a user filtering the catalogue for coordinate tools is looking
for something else. It is listed anyway because the classification guidance directs erring toward
inclusion where a user can access or benefit from a transform, and here the user selects it through a
documented public keyword and a documented CLI flag. **No subcategory is claimed**: the six children
are Heliospheric, Ionospheric, Magnetospheric, Mission-Specific, Planetary and Solar, and none
describes a terrestrial geodetic-to-geocentric conversion. `Coordinate Transforms: Magnetospheric`
was the nearest candidate and is rejected — the package never converts between magnetospheric frames.

**Considered and rejected**, so these are not re-proposed:

- **`Models and Simulations: Forecasting`** — the tempting evidence is real: secular variation is a
  first-class, user-selectable output (`isv` = "0 if main-field values are required" versus
  "1 if secular variation values are required", exposed as `--isv` with the help text
  "0: main field. 1: secular variation"), and the routine accepts dates to 2030.0 with a warning past
  2025.0. It is rejected because what this software emits is the model's annual rate of change of the
  *internal* field, not a space-weather prediction product. A user filtering the catalogue for
  forecasting tools wants nowcast or forecast systems, and would find a geomagnetic main-field
  calculator out of place among them.
- **`Models and Simulations: Physics-Based`** and **`: First Principles`** — the spherical-harmonic
  form is a solution of Laplace's equation, so the temptation is genuine, but the coefficients are
  empirically fitted and nothing physical is solved at run time. Adding a physics category would blur
  the distinction that `Empirical` exists to record.
- **`Models and Simulations: Data Guided`** — no observational data drives the model at run time; the
  coefficients are frozen into the compiled executable. The observational basis is already expressed
  by `Empirical`.
- **`Data Processing and Analysis: Processing`** — the package processes no input data; it synthesizes
  values from arguments. `Analysis` is the accurate leaf, and adding the vaguer `Processing` alongside
  it would assert a pipeline role that does not exist.
- **`Data Processing and Analysis: Time Series Analysis`** — `datetime2yeardec` accepts a sequence of
  times, but `igrf()` takes one scalar `time` and no code analyses a time-ordered series.
- **`Data Processing and Analysis: Data Access and Retrieval`** and **`: File Format Conversion`** —
  the package downloads nothing and converts no formats (see Fields 17–19). No Python source at the
  pinned revision imports an HTTP client.
- **`Data Visualization: Line Plots`, `: 3D Graphics`, `: Movies`, `: Web-Based`, `: 2D Slices`,
  `: Spectrogram`** — `plotigrf`, the one plotting function the package actually calls, draws contour
  maps on a latitude/longitude grid and nothing else; its `mode = "pcolor"` branches are unreachable,
  `mode` being assigned `"contour"` literally. The module's other function, `plotdiff1112`, draws
  `imshow` images rather than contours, but it is stale and uncalled: it indexes dataset variables
  `"x"`, `"y"`, `"z"` and `"Btotal"` that the current `igrf()` and `grid()` output does not contain.
  Either way the figures are flat rasters or contour maps, so `2D Graphics` covers them and no other
  visualization child applies.
- **`Mission-related`** and **`Servers and Environments`**, with all their children — there is no
  mission ground system, pipeline, server, container or HPC component in the 33-file tree.

### 5. Related Region (RECOMMENDED)
- Earth Ionosphere
- Earth Magnetosphere

`Earth Atmosphere` was recorded before this refresh and is removed. That value is one of the five
coarse regions this field wrongly offered until the vocabulary was corrected, and the vocabulary is
**flat** — a coarse row neither implies nor is implied by a specific one, so nothing is inherited
either way and "X encompasses Y" is not an available argument.

**`Earth Ionosphere`** rests on this software's own artifacts and on how it has actually been used.
The README's Python worked example evaluates the model at 100 km altitude
(`mag = igrf.igrf('2010-07-12', glat=65, glon=-148, alt_km=100)`), that is, in the E-region, and its
Matlab counterpart evaluates it at the surface — both squarely near-Earth; the PyHC
registry entry for this package tags it with an ionosphere/thermosphere/mesosphere domain keyword
(quoted in full under Field 33); and the two peer-reviewed applications that could be located are both
ionospheric — Nosikov et al. 2025 in *Radio Science*, whose title names ray tracing in the anisotropic
ionosphere with applications to the IGRF13 model and whose full text names this repository path, and
Gasque et al. 2023 in *Geophysical Research Letters*, which cites this package's version DOI in a
kinetic model of ionospheric emission (both in Field 27). From the searcher's side this is the
clearest case in the field: ionospheric calculations routinely need the main field as a background, and
a user filtering for ionospheric software would be glad to find a small, direct IGRF evaluator.

**`Earth Magnetosphere`** rests on the quantity computed and on the interface that exposes it. The
internal main field is the baseline against which magnetospheric field models are defined, and this
software can be evaluated at magnetospheric distances: in geocentric mode `alt` is the
"distance from centre of Earth in km if itype = 2 (>3485 km)" — a lower bound near the core-mantle
boundary and **no** stated upper bound — and `itype` is exposed through both the Python API and the
command line. A user filtering for magnetospheric software and looking for an internal-field baseline
would be unsurprised to find this.

This lands in the same place as the catalogue's record for the IGRF-14 coefficient release, but on
different evidence: that record reasoned from the release description's statement of the model's
application areas, whereas the two values above are argued from this package's altitude domain, its
exposed geodetic/geocentric interface, its own worked example and its citation record. The coincidence
is not deference.

**Considered and rejected**, each with its reason:

- **`Earth Atmosphere`** — the strongest argument for keeping it is authorial: `pyproject.toml`
  classifies the package `Topic :: Scientific/Engineering :: Atmospheric Science`. That lost on two
  grounds. A PyPI trove topic is a coarse distribution-metadata bucket covering a subject area at a
  granularity that maps onto three separate rows of this vocabulary, so it cannot select among them;
  and where the vocabulary offers the specific region, the guidance directs preferring it. The
  specific ionospheric evidence above is what actually supports a value here. A user filtering for
  atmospheric software is looking for neutral-atmosphere models, and the way this package genuinely
  serves atmospheric science — supplying the background field for ionospheric work — is exactly what
  `Earth Ionosphere` records.
- **`Earth Thermosphere`** and **`Earth Lower and Middle Atmosphere`** — the PyHC domain tag names the
  thermosphere and mesosphere as well as the ionosphere, and the README example at 100 km is formally
  in the lower thermosphere. Rejected because that tag is a single three-domain bucket whose
  ionospheric component is independently evidenced and whose other two components are not, and because
  one illustrative altitude argument is not a domain claim. Apart from that bundled tag, no source
  consulted — the repository, the registry entry or the located literature — ties this software to
  thermospheric or mesospheric science specifically.
- **`Earth Auroral Subregion`** — the Gasque et al. 2023 paper is about STEVE's picket fence, a
  subauroral optical phenomenon, and it cites this package. Rejected because a use-citation shows the
  field in which one group applied the model; it does not make the software auroral-specific, and
  nothing in the package addresses auroral physics. A user filtering for auroral software would find a
  general main-field calculator out of place. The same bar is applied in the other direction: the
  ionospheric value above is not carried by citations alone but by the repository's own example
  altitude and the registry tag as well.
- **`Earth Inner Magnetosphere`, `Earth Outer Magnetosphere`, `Earth Magnetotail`,
  `Earth Magnetosheath`** — the software supplies the internal main field as a baseline throughout the
  magnetosphere and distinguishes no subregion; the API, the CLI, the tests and the plotting code
  contain nothing that selects among them. Choosing all four would be padding, and choosing one would
  be a guess.
- **All non-terrestrial rows** — `Chromosphere`, `Corona`, `Heliosheath`, `Interplanetary Space`,
  `Jupiter Magnetosphere`, `Mars Magnetosphere`, `Neptune Magnetosphere`, `Photosphere`,
  `Planetary Magnetospheres`, `Saturn Magnetosphere`, `Solar Environment`, `Solar Interior`,
  `Solar Wind`, `Uranus Magnetosphere`. IGRF is a model of Earth's field only; the reference radius is
  Earth's (6371.2 km) and the spheroid is WGS84.

**The vocabulary has no term for the region the modelled field originates in** — the Earth's core,
deep interior, crust or lithosphere. Its one interior row, `Solar Interior`, is solar. That absence is
why no interior region appears above, and it should not be read as an oversight.

### 6. Authors (MANDATORY)
- **Author:** Michael Hirsch
  - **Author Identifier:** `https://orcid.org/0000-0002-1637-6526`
  - **Affiliation:** Boston University — `https://ror.org/05qwgg493`
  - **Affiliation:** Scivision, Inc.

**Sole authorship is a finding, not an omission.** At the pinned revision the repository has no
`CITATION.cff`, no `AUTHORS` or contributors file, no `.mailmap` and no `codemeta.json`; the committer
set resolves to nine identity lines that are all one person — `Michael Hirsch, Ph.D`,
`Michael Hirsch`, `scivision`, `scienceopen`, `michael` and `nucl`, across
`scivision@users.noreply.github.com`, `scienceopen@users.noreply.github.com`,
`10931741+scivision@users.noreply.github.com` and `hirsch617@gmail.com`. The two GitHub noreply
handles are tied to the same name by commits authored as `Michael Hirsch, Ph.D` under each, and the two
`hirsch617@gmail.com` aliases share an address. PyPI records the author as `Michael Hirsch, Ph.D.`,
the PyHC registry gives the contact as `Michael Hirsch`, and Zenodo carries only the bare given name
`Michael`. `Michael Hirsch` is the form used here because it is the name under which the person is
identified by ORCID and by the curated registry entry.

The ORCID is corroborated independently: the public record for `0000-0002-1637-6526` is
`Michael Hirsch`, with a Boston University employment (department ECE, Research Scientist, from August
2018, no end date) and Master's and Ph.D. degrees from the same department. That employment is what
supports the `Boston University` affiliation and its ROR. The second affiliation, `Scivision, Inc.`,
is the author's own company, named in the copyright line of `LICENSE.txt`
(`Copyright (c) 2015 Scivision, Inc.`).

**Susan Macmillan and William Brown are deliberately not listed, and only new evidence about *this
package's* authorship would change that.** The comment block of `igrf13syn` in
`src/igrf/fortran/igrf13.f`
credits adaptations of the synthesis routine to Susan Macmillan (August 2003, December 2004,
December 2009 and December 2014) and to William Brown (December 2019, February 2020), and
`src/igrf/fortran/igrf13_legacy.f` names both alongside the British Geological Survey and IAGA Working
Group V-MOD. They are authors of the **upstream IAGA routine that this package vendors**, not of this
package: neither has any commit in the repository's history, and the credit a user of *this* page needs
is for the Python and Matlab wrapper, the packaging, the CMake build and the xarray output design —
all of which are one person's work. Their scientific credit reaches the record through the model's
defining publication in Field 27 and through the upstream reference implementation in Field 29, which
is where it belongs.

**Do not send an ORCID for an author whose stored record lacks one.** No such case arose here — this
record's one author already carried the correct ORCID before this refresh, and it is unchanged — but the
constraint is recorded because it is the kind of thing a later refresh could get wrong. Person and organization records are shared
across the catalogue and are not this entry's to alter.

### 7. Software Name (MANDATORY)
`IGRF-13`

**The name is `IGRF-13`, and the alternatives weighed against it are recorded below with the reason
each lost.** What the sources say: the PyHC registry entry is
`name: IGRF-13`; the repository, the importable module and the PyPI distribution are all `igrf`; the
README's title is `# IGRF 13 in Python`; `pyproject.toml`'s description is
`IGRF13, IGRF12, IGRF11 models with simple object-oriented Python interface.`; and GitHub's repository
description is `International Geomagnetic Reference Field IGRF13 in Python and Matlab`.

`IGRF-13` is retained for three reasons. It is the name used by the one curated external registry that
lists this package, so keeping it means the catalogue and that registry agree. It names the model
generation, which is this package's single most important distinguishing property — the coefficients
are frozen at generation 13 and the synthesis routine is valid only to 2025.0 — and it is what a user
actually types. And the implementation-versus-model distinction, which is the real risk, is already
carried where a searcher reads it: the concise description in Field 9 opens "International Geomagnetic
Reference Field (IGRF13) model with object-oriented Python and Matlab interfaces", which appears next
to the name in results.

**The alternatives weighed and not chosen, with the argument for each:**

- **`igrf`** — this field's own guidance asks for the name of the software package as listed on the
  code repository, and that name is `igrf`. It would also make the catalogue's three IGRF records
  visibly different in kind (`igrf`, `IGRF-14`, `igrfpy`), where today two of the three read like
  successive model generations when only one of those two is software. Against it: lower-case `igrf`
  beside `IGRF-14` can read as a typo or a duplicate rather than a distinction, it discards the
  generation information, and it diverges from the registry.
- **`IGRF-13 in Python`** or a similar constructed form — closest to the README title, and it states
  implementation-not-model immediately. Against it: it is not a name any source actually uses, it
  omits the Matlab interface that is a genuine feature of the package, and inventing a display name is
  a larger step than a metadata refresh should take on its own.

### 8. Description (MANDATORY)
International Geomagnetic Reference Field: IGRF13 in object-oriented Python or Matlab. The current
public Python API and build path target IGRF13; IGRF11 and IGRF12 source files are retained in the
repository but are not exposed by the current driver. The software provides calculations of Earth's
main magnetic field components (north, east, down, total intensity) as well as magnetic inclination
and declination at specified geographic coordinates and altitudes. Secular variation, the annual rate
of change of each component in nT/year, can be requested instead of main-field values, and coordinates
may be supplied as either geodetic (WGS84 spheroid) or geocentric. It uses a Fortran backend with
Python and Matlab interfaces, and outputs results as xarray Datasets for easy integration with other
geoscience tools. The included IGRF13 synthesis routine is valid through 2025.0, with reduced-accuracy
warnings for later dates.

The description's factual claims are verified against the pinned revision. The opening sentence is the
README's own summary
line, `International Geomagnetic Reference Field: IGRF13 in object-oriented Python or Matlab.` The
build-path clause is confirmed by `CMakeLists.txt` and `MANIFEST.in` (see the scope note). The
component list matches the returned dataset's data variables — `north`, `east`, `down`, `total`,
`incl`, `decl` — as printed in the README and assembled in `src/igrf/base.py`. The validity statement
matches `igrf13.f`, which is valid from 1900.0 to 2025.0 inclusive and warns for dates past 2025.0
while computing to 2030.0.

**One sentence was added by this refresh**, on secular variation and the geodetic/geocentric choice.
Both are user-facing capabilities the description had omitted entirely: `isv` and `itype` are keyword
arguments of `igrf()` and `grid()` and flags of the command line, `igrf13.f` documents the `isv = 1`
outputs in nT/year ("north component (nT) if isv = 0, nT/year if isv = 1"), and the `itype = 1` branch
performs the "conversion from geodetic to geocentric coordinates" "(using the WGS84 spheroid)". This
is a material omission repaired, not a rewording; the surrounding text is unchanged.

**Considered and rejected: naming IGRF-14 here as the successor generation.** A reader in 2026 is
using a model whose validity ended at 2025.0, so the temptation is real. It is rejected because a
description's job is to describe this software, the validity limit is already stated plainly, and
naming a successor product would require an edit at every five-year model generation. Where a reader's
"what should I use for later dates?" question is actually answered is Field 29's ppigrf entry —
maintained, compiler-free and covering generation 14.

### 9. Concise Description (OPTIONAL)
International Geomagnetic Reference Field (IGRF13) model with object-oriented Python and Matlab
interfaces for calculating Earth's magnetic field components.

This wording stands as the maintainer-facing preview: it is within the field's 200-character limit, it
is accurate, and it does the implementation-versus-model disambiguation that Field 7 relies on, by
naming the Python and Matlab interfaces in the preview a searcher sees. No stylistic alternative was
substituted for it.

### 10. Publication Date (RECOMMENDED)
`2015-03-29`

**What this value represents:** the date the repository began. The first commit on the pinned lineage
is `1ea75cd8fafa548806dcc0c964c6c8571ee0bf38`, 2015-03-29 02:55:18 -0400, by Michael Hirsch, and
GitHub's `created_at` for the repository is `2015-03-29T06:55:18Z` — the same instant expressed in
UTC. Two independent sources agree exactly, so the value is not an artifact of either.

**A tension worth keeping, because it will look like an error to someone who does not know it.** This
package's *IGRF-13* identity begins much later: release v13.0.0 is dated 2020-08-24 (git tag
`daaa7698b3b1c45cff69ea1581f1062e1c43bf4a`, with a PyPI upload the same day), and the eight releases
before it — v1.2.0 through v1.3.6, 2018-02-27 to 2019-11-11 — were an IGRF-11/IGRF-12 wrapper. The
field asks for the date of first publication, used for the initial version of the software, so the
repository's origin is the right answer; 2020-08-24 is recorded here as the date the current model
generation arrived.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** `https://zenodo.org`

Correct per this field's guidance, which names Zenodo for software whose DOI was obtained through the
GitHub-Zenodo workflow. That is demonstrably this case: the version record's `isSupplementTo` relation
points at `https://github.com/space-physics/igrf/tree/v13.0.2`, the integration's signature (Field 2).
GitHub is not the right answer here precisely because a DOI was obtained; that alternative is rejected
for that reason.

### 12. Version (RECOMMENDED)
- **Version Number:** `v13.0.2`
- **Version Date:** `2021-10-11`
- **Version Description:** Use Matlab test unit class. Attempt to make CMake build more robust from
  Python.
- **Version PID:** `https://doi.org/10.5281/zenodo.5560949`

**This is a confirmation from four independent sources, not an anomaly to investigate.** The git tag
`v13.0.2` is `5d01a902977bb0927f157eca18073cad30a1a4b0`, dated 2021-10-11, and is an ancestor of the
pinned revision; `src/igrf/__init__.py` at the pin declares `__version__ = "13.0.2"`; PyPI's latest
release is `13.0.2`, with the sdist `igrf-13.0.2.tar.gz` uploaded 2021-10-11; and the Zenodo version
record `5560949` gives `version: v13.0.2` and `publication_date: 2021-10-11`. The `v`-prefixed form is
used because it is the form the git tag and Zenodo both use.

The version description is the Zenodo record's own release notes, whose two paragraphs are "Use Matlab
test unit class" and "Attempt to make CMake build more robust from Python" — matching the two commits
the tag actually contains (`7114538`, "build more robust", and `5d01a90`, "Matlab use test class").
The version DOI and the concept DOI in Field 2 are a pair; neither substitutes for the other.

**The repository has moved on without releasing.** Two commits sit between the v13.0.2 tag and the
pinned revision: a one-line README edit (2023-08-17), and a 2024-08-23 commit whose "update metadata"
subject understates it — it migrated the project from `setup.py`/`setup.cfg` to `pyproject.toml`,
rewrote the CI workflow, deleted five legacy config files, and touched `src/igrf/__init__.py` and the
test module. So the newest release is nearly three years older than the newest commit. That gap is what Field 23 turns on. Only
three releases have ever reached PyPI: 13.0.0 (2020-08-24), 13.0.1 and 13.0.2 (both 2021-10-11).

**A trap for a later refresh: PyPI's frozen metadata contradicts the repository.** PyPI reports
`requires_python: >=3.7`, because that metadata was written at the 2021 release; `pyproject.toml` at
the pin says `requires-python = ">=3.9"`. For any claim about the repository, the pin wins.

### 13. Programming Language (RECOMMENDED)
- Fortran77
- Fortran90
- Fortran 2008
- MATLAB
- Python 3.x

**The rule applied:** a row earns its place when it names a dialect that characterizes a distinct body
of the shipped source, or when it raises the toolchain requirement a reader must satisfy. That rule
keeps three Fortran rows and excludes two.

- **`Fortran77`** — the numerical kernels are fixed-form legacy Fortran: `igrf13.f` uses
  `implicit double precision (a-h,o-z)`, `dimension`, `equivalence` and `data` blocks with column-6
  continuation, and `igrf11.f`, `igrf12.f`, `igrf11_driver.f`, `igrf12_driver.f` and
  `igrf13_legacy.f` are of the same era and form.
- **`Fortran90`** — `igrf13.f` has been modernized by the packager while staying fixed-form: it is
  wrapped in `module igrf` / `contains` / `end module igrf` and uses standalone `intent(in)` and
  `intent(out)` attribute statements. `igrf13_driver.f90` is free-form, uses a module and calls
  `igrf13syn` with keyword arguments.
- **`Fortran 2008`** — added by this refresh, and the reason the two rows held before it were
  insufficient. Of the two Fortran files actually built, `igrf13_driver.f90` takes its kinds from
  `use, intrinsic:: iso_fortran_env, only: stderr=>error_unit, dp=>real64`, and the named kind constant
  `real64` is a Fortran 2008 addition. This package therefore cannot be compiled by a Fortran 77 or
  Fortran 90 compiler, which `Fortran77` and `Fortran90` on their own implied it could.

**`Fortran 2003` considered and rejected.** Its features are genuinely present — the `intrinsic` module
nature on the `use` statements in both `igrf13.f` and `igrf13_driver.f90`, `error_unit`, and
`command_argument_count()` and `get_command_argument()` in the driver. It is excluded because every one
of those is also required of any Fortran 2008 compiler, so the row would neither characterize a
distinct body of source nor change what a reader concludes about the toolchain, while pushing this
field to four Fortran rows on the strength of two `use` statements. **`Fortran 2023` rejected** — no
Fortran 2023 feature appears.

**A documented gap in the vocabulary.** The true compiler floor is one standard higher than any
available row: `igrf13_driver.f90` uses `implicit none (type, external)`, and the
implicit-none-spec-list form is a **Fortran 2018** addition, for which there is no row.
`Fortran 2008` is the closest available value. If a `Fortran 2018` row is ever added, that is the
value to record here.

**`MATLAB`** is a first-class interface, not an afterthought: `+igrf/igrf.m`,
`+igrf/private/xarray2mat.m`, `+igrf/TestUnit.m` and `setup.m` form a Matlab package with its own unit
test, `igrf.m` uses an `arguments` validation block, and the README documents the call. See Field 30.

**`Python 3.x`** — `pyproject.toml` sets `requires-python = ">=3.9"`, and CI pins
`python-version: '3.9'`. `Python 2.x` is rejected: `src/igrf/utils.py` opens with
`from __future__ import annotations` and uses PEP 585 generics (`tuple[float, float]`), and
`src/igrf/base.py` uses f-strings and `importlib.resources`.

### 14. Reference Publication (OPTIONAL)
Not found. Documented omission — **no publication describes this software.**

This field wants the DOI of a publication describing *the software*, a JOSS paper or its equivalent,
which is a different thing from the model's defining paper. The negative research is thorough enough
that it should not be repeated: a title search for IGRF papers naming Python or Matlab returns
nothing; an author search combining this author with IGRF in title or abstract returns nothing; and a
full-text search for the repository path `space-physics/igrf` returned, as of this extraction, exactly
two records — the Zenodo software deposit itself (indexed as `doctype: software`, with the bare-given-name creator noted in
Field 2) and one article that *uses* the package, recorded in Field 27 rather than here. A
nonsense-token control on the same full-text index returned zero, so the index was genuinely queried.
The searches were keyed on title, author and full text, not merely on the repository name.

**The IGRF-13 model paper is deliberately in Field 27, not here.** Alken et al. 2021 describes the
model, and this software is one third-party implementation of it. Recording it as this software's
reference publication would tell a user that citing that paper credits this wrapper, which it does
not; it would also make several catalogue records that implement or publish IGRF appear to share a
software paper.

### 15. License (RECOMMENDED)
- **License:** `MIT License`
- **License URI:** `https://spdx.org/licenses/MIT`

HSSI held no licence value for this field before this refresh; this fills it. `LICENSE.txt` at the
pinned revision is the MIT licence text under the heading `The MIT License (MIT)`, with the line
`Copyright (c) 2015 Scivision, Inc.` — and GitHub's own licence detection reports
`spdx_id: MIT`. `MIT License` is the controlled vocabulary's row name, copied exactly; that vocabulary
is closed and matched without aliasing, so a variant such as "MIT" would be rejected.

**Zenodo's `other-open` was rejected**, per settled practice for this catalogue: it is Zenodo's own
generic placeholder and does not describe the licence in the repository. `pyproject.toml` declares no
`license` field at all, and PyPI's `license` string is empty, so `LICENSE.txt` is where the licence is
actually stated — and it is unambiguous.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- geomagnetic
- igrf
- igrf13
- main field
- secular variation
- declination
- inclination
- spherical harmonics

**The standard applied**, drawn from the field's own definition — general science keywords not
supported by other metadata fields — and from the searcher's side: a keyword earns its place if a user
would plausibly type it and no other field already delivers it. Seven of the ten stored terms fail
that test, and five science terms were missing.

**Kept, with their evidence:**

- `geomagnetic` and `igrf` — the author's own two keywords, `keywords = ["geomagnetic", "igrf"]` in
  `pyproject.toml`. `igrf` reaches anyone looking for the model family.
- `igrf13` — kept although it looks like a version number, because it is not one: the software version
  is 13.0.2, while "IGRF13" names the *model generation*, whose coefficients and 1900.0-2025.0
  validity window are specific to it. Generations are not interchangeable, and this is the term that
  separates this package from the catalogue's other IGRF records.

**Added, each on its own evidence at the pinned revision:**

- `main field` and `secular variation` — the two things the software can compute, selected by one
  argument. `igrf13.f` documents `isv` as "0 if main-field values are required" and
  "1 if secular variation values are required", and describes the `isv = 1` outputs in nT/year; the
  command line exposes the choice with the help text "0: main field. 1: secular variation". Secular
  variation appeared nowhere in this record before this refresh, and it is half of what the software
  does.
- `declination` and `inclination` — `mag_vector2incl_decl` is a publicly exported function, `decl` and
  `incl` are variables of every returned dataset, `plots.py` titles two panels
  "Magnetic Declination [degrees]" and "Magnetic Inclination [degrees]", and the README embeds the
  resulting figure. These are also the field elements under which non-specialists look for a
  geomagnetic model at all.
- `spherical harmonics` — the mathematical form of the model, and visible in the implementation rather
  than merely assumed: `igrf13.f` performs the "computation of Schmidt quasi-normal coefficients p and
  x(=q)" with degree-13 truncation (`cl(13)`, `sl(13)`, `p(105)`, `q(105)`), and the comment block
  refers to the model's maximum degree.

**Removed, with reasons, so they are not restored:**

- `specific` — PyHC registry scaffolding. It classifies a registry entry as domain-specific rather than
  general-purpose, and means nothing to a person browsing this catalogue.
- `fortran`, `python`, `matlab` — all three are Field 13 values. The field's definition excludes
  keywords that other fields support, and the language facet gives a searcher strictly more than these
  strings do.
- `matlab-python-interface` — the capability is real and distinctive, but it falls to exactly the same
  rule, applied consistently: the bilingual nature of the package is expressed by `MATLAB` and
  `Python 3.x` together in Field 13 and by the Matlab bridge in Field 30, and the hyphenated slug is a
  repository-topic string rather than a science keyword.
- `igrf12` — the package cannot compute IGRF-12. `igrf12.f` and `IGRF12.COF` are in the tree but off
  the build path, and the test that exercised them is commented out. A user searching for igrf12 who
  landed here would find a capability that does not exist.
- `ionosphere_thermosphere_mesosphere` — a PyHC domain tag in underscored slug form. Nobody types it;
  its ionospheric component is now carried properly by `Earth Ionosphere` in Field 5, which the field's
  own definition makes grounds for exclusion; and its thermospheric and mesospheric components are not
  supported by this software (see Field 5).

**Considered and not added:** `geomagnetism`, `geomagnetic field` and `earth magnetic field`, as
near-duplicates of the author's own `geomagnetic`; `empirical model`, already carried by
`Models and Simulations: Empirical` in Field 4; `gauss coefficients`, a term of art the sources here do
not use, and one whose searcher is looking for a coefficient release rather than an evaluator of one;
`core field` and `crustal field`, which describe the model's origin and applications rather than
anything this package does; and `world magnetic model` or `wmm2015`, which would mislead —
`WMM2015.COF` is vendored but unbuilt and unreachable, so this package cannot compute WMM (see
Field 27 on the WMM2015 map PDFs).

**Provenance of what was stored.** Eight of the ten stored keywords are this repository's GitHub topics
(`fortran`, `geomagnetic`, `igrf`, `igrf12`, `igrf13`, `matlab`, `matlab-python-interface`, `python`,
retrieved 2026-09-01 — repository settings, not tracked content), and the remaining two are the PyHC
registry entry's `keywords:` list.

### 17. Data Sources (OPTIONAL)
Not applicable. Documented omission.

**The software retrieves nothing.** Its coefficients are compiled into the executable as Fortran `data`
tables, and its inputs are function arguments or command-line arguments. No Python source at the pinned
revision imports `requests`, `urllib` or any HTTP client; the declared dependencies are
`dependencies = ["xarray", "numpy"]`; and the four subprocess calls in `src/igrf/base.py` invoke only
two local programs, CMake (to configure and build) and the locally built `igrf13_driver` executable.

Every row this field offers names a remote archive or an access protocol — `AMDA`, `CDAWeb`, `das2`,
`FTP/FTPS Directories`, `GFZ`, `HAPI`, `HTTP/HTTPS Directories`, `Madrigal`,
`Observatory/Mission-specific`, `OMNIWeb`, `S3/Cloud-aware`, `SSCWeb`, `TAP`,
`The Virtual Solar Observatory.`, `VirES`, `WDC` — and none of them is contacted. `Other` was
considered and rejected: selecting it would assert that some unlisted data source exists, when the
correct statement is that there is none. That is why this field is empty, and empty is the right value
rather than a gap.

### 18. Input File Formats (RECOMMENDED)
Not applicable. Documented omission.

**Nothing on the build path or in either public API reads a data file.** `igrf()` and `grid()` take a
time and scalar or array coordinates; the command line takes a date and numeric flags; the coefficients
are compiled in.

**The one piece of evidence that looks like a counter-example, examined.** The repository ships
`reference/sample_coords.txt`, `reference/sample_out_IGRF12.txt` and `reference/sample_out_WMM2015.txt`,
which are plain ASCII tables — `sample_coords.txt` in the
date/coordinate-system/altitude/latitude/longitude form the NOAA and BGS command-line synthesis programs
prompt for, and the two `sample_out_*` files carrying that program's output header
(`Date Coord-System Altitude Latitude Longitude D_deg D_min I_deg I_min H_nT X_nT Y_nT Z_nT F_nT dD_min
dI_min dH_nT dX_nT dY_nT dZ_nT dF_nT`). They are **not read by anything**: no Python, Matlab or built
Fortran source references them, and `src/igrf/tests/test_mod.py` compares against hard-coded numbers
rather than these fixtures. The ASCII I/O they belong to lives in the *unbuilt* legacy programs —
`igrf11_driver.f`, `igrf12_driver.f` and `igrf13_legacy.f` each prompt interactively and `OPEN` an
output file — and none of those is in `CMakeLists.txt` or `MANIFEST.in`.

`ascii` is therefore rejected as an input format: it describes upstream programs bundled as provenance,
not a capability of the software as built and installed. If a future revision ever puts one of those
programs on the build path, this is the field to revisit.

### 19. Output File Formats (RECOMMENDED)
Not applicable. Documented omission.

**The software writes no files.** `igrf()` and `grid()` return `xarray.Dataset` objects in memory — both
are annotated `-> xarray.Dataset` in `src/igrf/base.py` — and the command line either prints the dataset
or renders figures with `show()`. There is no `savefig`, no `to_netcdf`, no `to_csv` and no `open(...)`
for writing anywhere in the Python sources at the pinned revision.

`netCDF3/4` and `Zarr` were considered and rejected. A user *can* serialize the returned dataset through
xarray, but the field asks for formats the software supports for generated files, and this software
implements no writer for any of them; claiming those formats would credit it with xarray's capabilities.
`ascii` is rejected for the reason given in Field 18. The interchange relationship with xarray that this
return type does establish is recorded where it belongs, in Field 30.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

`Operating System Independent` was stored alongside these three and is removed. **The rule applied:**
where a package's own sources and instructions name specific platforms and branch on them, list those
platforms; reserve `Operating System Independent` for software with no platform-specific installation
step and no platform-specific code path. This package has both.

- It cannot be installed without a platform-appropriate Fortran toolchain. The README states that "A
  Fortran compiler is required, such as `gfortran`" and then gives three different instructions —
  `apt install gfortran` for Linux, `brew install gcc` for Mac, and a link to MinGW gfortran for
  Windows — and `src/igrf/base.py`'s `build()` raises
  `FileNotFoundError("CMake not available")` when CMake is absent.
- It branches on the platform in code: `src/igrf/base.py` appends `.exe` to the driver name when
  `os.name == "nt"`, and selects `g = ["-G", "MinGW Makefiles"]` on the same test when
  `CMAKE_GENERATOR` is unset.

`pyproject.toml`'s `Operating System :: OS Independent` classifier is the argument on the other side,
and it is why the value was there. It loses because it is a distribution-metadata assertion about
pure-Python portability that this package's own build requirements contradict — and because the more
useful signal to a reader is precisely that installation is platform-dependent.

**Evidence per platform, stated precisely because the previous record overstated it.** `Linux` and
`Mac` are exercised by continuous integration: `.github/workflows/ci.yml` runs the matrix
`os: [ubuntu-24.04, macos-latest]` with `FC: gfortran-14`, installing the package and running `pytest`,
which compiles the Fortran through `build()` on first use. **`Windows` is not in the CI matrix.** It
rests entirely on the README's MinGW gfortran instruction and the two `os.name == "nt"` branches above —
deliberate support code, but untested here. Note also that the workflow triggers only on pushes touching
`**.py` or the workflow file, so a change to the Fortran alone does not exercise the build.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Confirmed, and this is a positive finding about the source rather than a default. Nothing in the tree is
architecture-specific: no SIMD intrinsics, no assembly, no architecture test in `CMakeLists.txt` or in
`build()`, no compiled artifact in the repository, and no GPU or MPI code. Portability rests on the
compiler, and both CI platforms build from the same source with the same `gfortran-14`.

**`x86-64`, `Apple Silicon arm64` and `Linux aarch64 or arm64` considered and rejected.** They are
empirically satisfied — GitHub's macOS runners are Apple Silicon and its Ubuntu runners x86-64 — but
listing them would narrow a claim the source does not narrow, and would misrepresent
architecture-neutral source as architecture-targeted. **`GPU`, `HPC or HEC`, `ppc64le`, `Sun (SPARC)`
and `Other` rejected** — no evidence of any.

**Why this field prefers "Independent" while Field 20 prefers the specific platforms**, since the two
choices look opposite: the operating-system claim of independence is falsified by the package's own code
and instructions, whereas here there is nothing architecture-specific to falsify it. The rule is the
same in both fields — follow what the source actually distinguishes.

### 22. Related Phenomena (OPTIONAL)
Not found. Documented omission.

The vocabulary is **closed** and offers seven rows: `Coronal Heating`, `Coronal Mass Ejections`,
`Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and `X-ray emission`. Six are solar
or heliospheric and have no bearing on a model of Earth's internal field.

**`Geomagnetic Storms` is the only candidate, and it is wrong.** IGRF models the *quiet internal main
field* — the part generated in the Earth's core, fitted to observations with disturbance fields
removed. Storm-time variation is produced by external magnetospheric and ionospheric current systems
that this model does not represent at all, and nothing in the repository mentions storms, indices or
disturbance. A user filtering the catalogue for storm-related software would find a main-field
calculator actively misleading.

The concepts this software *does* relate to — the main field, secular variation, declination and
inclination — have no row here. They are carried by Field 16, which is this field's stated remedy for a
phenomenon the controlled list cannot express. This field is correctly empty.

### 23. Development Status (RECOMMENDED)
`Inactive`

HSSI held no value for this field before this refresh; this fills it. The definition `Inactive` carries
is "The project has reached a stable, usable state but is no longer being actively developed;
support/maintenance will be provided as time allows." Both halves of it are evidenced.

- *Stable and usable:* `pyproject.toml` classifies the package
  `Development Status :: 5 - Production/Stable`; three releases have reached PyPI, the newest being
  13.0.2; there is a working public API, a pytest test that checks the computed field components and the
  derived inclination and declination against fixed reference values, a CMake test
  (`add_test(NAME igrf13 COMMAND $<TARGET_FILE:igrf13_driver> 2015.1 0 0 0 0 1)`), and a Matlab unit
  test class.
- *No longer actively developed:* the newest commit at the pinned revision is 2024-08-23, and what it
  changed is packaging and infrastructure rather than the software — a migration to `pyproject.toml`, a
  CI rewrite, and edits to `src/igrf/__init__.py` and the test module (see Field 12). **The science
  code has not changed since 2021-10-11**, the day v13.0.2 was released: that is the newest commit
  touching the Fortran kernels, `base.py`, `utils.py`, `plots.py` or the coefficient files.
- *Support as time allows:* the repository is not archived, and the author was still doing housekeeping
  on it in 2024, which is maintenance as time allows rather than feature development.

**Every alternative, with its reason:**

- **`Active`** — "The project has reached a stable, usable state and is being actively developed." The
  first half holds, the second does not: the science code was untouched for the two years and ten
  months between 2021-10-11 and the pinned revision, and the one commit that broke that silence was
  packaging housekeeping. An unarchived repository is one nobody closed, which is not evidence of
  active development.
- **`Unsupported`** — "The project has reached a stable, usable state but the author(s) have ceased all
  work on it. A new maintainer may be desired." Rejected on the settled position that this value belongs
  to an **archived** repository and not to a quiet but open one: work has not ceased (a 2024 commit) and
  the repository is not archived. Note that the definition says a new maintainer *may* be desired — a
  permission, not a requirement — so the absence of any such request is not by itself what excludes this
  value; the 2024 commit and the unarchived state are.
- **`Abandoned`, `Suspended`, `WIP`, `Concept`** — each requires either that there has not yet been a
  stable, usable release, or that implementation is minimal or demonstration-only. Three PyPI releases
  and a Production/Stable classifier rule all four out.
- **`Moved`** — nothing indicates relocation; this remains the canonical location (Field 3).

### 24. Documentation (RECOMMENDED)
`https://github.com/space-physics/igrf`

This field explicitly permits the access URL when the documentation lives there, and it does: `README.md` is the whole of the documentation, covering installation (including the
per-platform compiler instructions), the one-time `igrf.build()` step, a Python usage example with its
printed output, a Matlab section, and a references list.

**Confirmed absent at the pinned revision:** no `docs/` directory, no `.readthedocs.yml`, no Sphinx or
MkDocs configuration, and no `.rst` file among the 33 tracked files. GitHub reports `has_pages: false`
and `has_wiki: false`.

**A caveat a reader following this documentation will hit.** The README's example section instructs the
reader to run `igrf` on the command line to reproduce the figures, but the packaging metadata installs
that entry point under a different name (see the scope note); `python -m igrf` is the working
equivalent. Relatedly, at the pinned revision `src/igrf/__init__.py`'s docstring reads
"use IGRF via f2py from Python", which no longer describes the implementation — `src/igrf/base.py` runs a CMake-built standalone
executable through `subprocess`, with no f2py extension module anywhere. Both are upstream inaccuracies
to be aware of, not values to correct here.

### 25. Funder (OPTIONAL)
Not found. Documented omission.

No funding statement exists to record. At the pinned revision no file in the repository contains any
funding, grant, sponsorship, award or acknowledgement language. The one match anywhere in the tree is a
false positive: the "grant" inside "granted", in `LICENSE.txt`'s "Permission is hereby granted, free of
charge, to any person obtaining a copy". The Zenodo record's `grants`
field is `null`. An acknowledgements-section search naming this repository returns nothing.

**Considered and rejected: the funders named in the IGRF-13 model paper's acknowledgements.** They
supported the *model* and the institutions that produce it, not this third-party wrapper. Recording them
here would attribute funding to work they did not fund, which is the specific error this field's
guidance warns against.

### 26. Award Title (OPTIONAL)
Not found. Documented omission. Same evidence as Field 25 — there is no award to record, and an award
entry without a title cannot be recorded in any case.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- `https://doi.org/10.1186/s40623-020-01288-x` — Alken, P., Thébault, E., Beggan, C. D., et al.,
  "International Geomagnetic Reference Field: the thirteenth generation", *Earth, Planets and Space* 73,
  49 (2021). Open access.
- `https://doi.org/10.1029/2024RS008092` — Nosikov, I. A., Klimenko, M. V., Padokhin, A. M.,
  Nosikova, V. V., Bessarab, P. F., "Generalized Force Method for Point‐To‐Point Ray Tracing in
  Anisotropic Ionosphere: Implementation and Applications to NeQuick2 and IGRF13 Models",
  *Radio Science* (2025).
- `https://doi.org/10.1029/2023GL106073` — Gasque, L. C., Janalizadeh, R., Harding, B. J.,
  Yonker, J. D., Gillies, D. M., "It's Not Easy Being Green: Kinetic Modeling of the Emission
  Spectrum Observed in STEVE's Picket Fence", *Geophysical Research Letters* (2023).
- `https://doi.org/10.3389/fspas.2022.1023163` — Cai, L., Aikio, A., Kullen, A., Deng, Y., Zhang, Y.,
  et al., "GeospaceLAB: Python package for managing and visualizing data in space physics",
  *Frontiers in Astronomy and Space Sciences* (2022).

**Alken et al. 2021 was stored before this refresh and is kept.** It is the paper that defines the model
generation this software implements, so a user of this page needs it — but it describes the model, not
the wrapper, which is why it sits here and not in Field 14 (see that field for the full reason).

**The other three are added by this refresh, and they are the field's own subject matter**: publications
that cite or use the software. Each was verified individually.

- Nosikov et al. 2025 names this repository path in its indexed full text, and its title names the
  IGRF13 model as one of the two models it implements against — ionospheric ray tracing.
- Gasque et al. 2023 and Cai et al. 2022 each cite this package's version DOI
  (`10.5281/zenodo.5560949`) — the first in a kinetic model of STEVE's picket-fence emission, the second
  in a space-physics data-management package.

**The basis and the boundary of that set, so a later refresh can extend it rather than redo it.** These
are the publications located, as of this extraction, by a citation search on the version DOI and a
full-text search for the repository path; the *concept* DOI has no indexed citations, so a search keyed on it alone would find
none of them. A nonsense-token control on the same index returned zero, confirming the index was really
queried. Coverage of any citation index is partial, so this is what was found rather than a proof of what
exists. The set matters more than usual here because Field 14 is empty: these three papers are the only
published evidence a reader has that this small tool is used in real science.

**Considered and rejected: the two WMM2015 map PDFs in the README's references list**
(`WMM2015_I_MERC.pdf` and `WMM2015_D_MERC.pdf` on the NOAA geomag site). They belong in no field. They
are reference *figures* — inclination and declination charts — for the World Magnetic Model, a
*different* model whose coefficient file `WMM2015.COF` is vendored in this repository but is off the
build path and unreachable from either public API. They are not publications describing or using this
software, they are not datasets it reads, and listing them would suggest a WMM capability the package
does not have.

### 28. Related Datasets (OPTIONAL)
Not found. Documented omission.

The software reads no external dataset. Its IGRF-13 coefficients are Fortran `data` statements compiled
into the executable, and the two coefficient files that *are* present as separate artifacts
(`src/igrf/IGRF12.COF` and `src/igrf/WMM2015.COF`) are off the build path and unreachable from the Python
or Matlab API.

**Negative research, recorded because a future agent will find the near-miss.** Zenodo carries an archive
of IGRF-13 coefficients under the concept DOI `10.5281/zenodo.11269409`. It should not be added here: it
is a third-party archive created to serve as a data source for a different software project, this package
has no relation to it, and — decisively — this package cannot load external coefficient files at all.

### 29. Related Software (OPTIONAL)
- `https://doi.org/10.5281/zenodo.5962660` — ppigrf, the pure-Python IGRF implementation published by
  IAGA V-MOD
- `https://www.ngdc.noaa.gov/IAGA/vmod/igrf13.f` — the upstream IAGA reference implementation this
  package compiles

**The rule applied, and it is one rule for every candidate:** an entry earns a place only if it tells a
reader something about *this* software that no other field delivers and that would not be equally true of
any other IGRF wrapper. That test admits two entries and excludes everything else, including six of the
seven values Field 29 held before this refresh; the seventh, `igrf13.f`, is kept with its URL scheme
corrected.

**`igrf13.f`** is the strongest relation this field can express. It is not merely a reference: this exact
file is compiled into the shipped executable
(`add_executable(igrf13_driver fortran/igrf13_driver.f90 fortran/igrf13.f)`) and is one of the three
files `MANIFEST.in` distributes. The package is a wrapper around it, so the entry tells a reader what the
software *is* — the case this field names explicitly when it says "Important software dependencies and
software this work was forked from should also be included." The URL is recorded in its `https://` form; the `http://` form stored before
this refresh answers with a permanent redirect to it.

**`ppigrf`** is the paradigm case for this field's primary subject, "Software that performs similar
tasks but does not necessarily link together (which would be 'interoperable software')." It also passes
the field's separate requirement that an entry be *distinguishing*, in a way that arbitrary third-party
implementations do not: it is published by **IAGA V-MOD itself**, the working group that maintains the
model this package implements, which bounds the relation to one identifiable publisher instead of an
open-ended list of reimplementations. Verified independently — the
repository `https://github.com/IAGA-VMOD/ppigrf` is MIT-licensed, not archived, and last pushed
2026-02-20; its description is "Pure Python IGRF (International Geomagnetic Reference Field)"; its only
dependencies are numpy and pandas, so unlike this package it needs no Fortran compiler and no CMake; and
it ships both `IGRF13.shc` and `IGRF14.shc`, its README stating "Note that this code now defaults to use
IGRF-14". That combination is what makes the entry informative: it is the alternative a reader of *this*
page would actually switch to, whether because they cannot install a compiler or because they need dates
past this package's 2025.0 limit. The concept DOI is used rather than a version DOI, per this field's
preference for the all-versions identifier. ppigrf is not itself a catalogue entry, so this is an
external reference, not an in-catalogue link.

**Removed by this refresh, as the rule applied rather than as a discretionary trim:**

- **`https://github.com/numpy/numpy`** and **`https://github.com/matplotlib/matplotlib`** — the generic
  scientific-Python stack is excluded from this field with no exceptions. Being a dependency is not a
  relation that distinguishes anything, and a numpy dependency is true of most of the
  scientific-Python ecosystem. matplotlib is not even a declared dependency here: `dependencies = ["xarray", "numpy"]`, and
  `src/igrf/__main__.py` imports it inside a `try`/`except ImportError`, so plotting is optional.
- **`https://github.com/Kitware/CMake`** — build tooling, and generic infrastructure by any test:
  equally at home in a web application or a finance model. That the package invokes CMake at install
  time is a real fact about it, and it is recorded where a reader needs it, in Fields 20 and 23.
- **`https://github.com/pydata/xarray`** — not removed from the record but **reclassified to Field 30**.
  Its genuine relation to this software is a documented data-model exchange, which is Field 30's
  subject; listed here it read as a bare dependency, which this field excludes.
- **`http://www.ngdc.noaa.gov/IAGA/vmod/igrf11.f`** and **`.../igrf12.f`** — the same bar that admits
  `igrf13.f` excludes these, and the bar has to cut both ways: if being on the build path is what earns
  `igrf13.f` its place, then not being on the build path must count against these two. Neither is in
  `CMakeLists.txt` or `MANIFEST.in`, neither is reachable from the Python or Matlab API, and the tests
  that once exercised generations 11 and 12 are commented out. Retaining them implied a multi-generation
  capability the package does not have — the same overstatement `pyproject.toml`'s own description
  (`IGRF13, IGRF12, IGRF11 models with simple object-oriented Python interface.`) makes and that Field 8
  corrects.

**Considered and rejected**, so the reasoning is not repeated:

- **`https://www.ngdc.noaa.gov/IAGA/vmod/igrf.html`, the IAGA V-MOD IGRF landing page** — it resolves,
  and it would be a friendlier click than 60 kB of raw Fortran served as plain text. It loses because it
  is a page about the *model*, hosting several generations, whereas the point of the entry is to identify
  the one file this package actually compiles. Precision about what this software is beats click comfort
  here.
- **The IGRF-14 catalogue entry**
  (`https://www.ncei.noaa.gov/products/international-geomagnetic-reference-field`). This deserves its
  argument in full, because the case for it is genuine: this package is frozen at generation 13, whose
  synthesis routine is valid only to 2025.0, so a reader arriving in 2026 has a real need the successor
  generation would answer. The catalogue's IGRF-14 record separately considered and rejected a link *to*
  this package, reasoning that third-party IGRF implementations have no principled stopping point — and
  that objection would **not** block the reverse direction, because "the successor of the generation I
  implement" is a single bounded relation while "one of my many implementations" is unbounded. So the
  asymmetry argument survives. What defeats the entry is what the IGRF-14 record actually *is*: a
  coefficient release, not a software project (see the scope note). It performs no task similar to this
  one, it is not a dependency, and it is not what this work was forked from — so it fails this field's
  subject matter on every clause. It also fails the rule above: "generation 14 exists" is a fact about
  the model that is equally true of every IGRF wrapper, and this record already states its own validity
  limit in Field 8. The catalogue's convention is that accuracy about what a software actually relates to
  takes precedence over the discoverability benefit of linking to an existing entry, and a reader's
  genuine need for a later-generation option is met by the ppigrf entry, which does qualify. For the same
  reason `igrf14.f` on the IAGA page is rejected: it is the successor of the file this package wraps,
  which is a relation of the *model*, not of this software.
- **`igrfpy`** (`https://github.com/lkilcommons/igrfpy`), another Python IGRF wrapper and itself a
  catalogue entry. Rejected because admitting it has no principled stopping point: IGRF has many
  independent implementations across several languages, and once the "published by the model's own
  maintaining body" criterion that admits ppigrf is dropped, there is no line that admits igrfpy and
  excludes pyIGRF, ChaosMagPy, Harmonica, MATLAB's Aerospace Toolbox and the rest. Being a catalogue
  sibling is a discoverability bonus, not a qualification. A user comparing Python IGRF options is better
  served by searching the catalogue for the model than by an arbitrary subset of links here.
- **GeospaceLAB** (`https://github.com/JouleCai/geospacelab`). Its 2022 paper cites this package's
  version DOI (Field 27), which makes it a downstream consumer rather than a peer or a dependency — and
  the relation is not durable: release 0.14.15 does not list `igrf` among its declared dependencies at
  all. A citation in a four-year-old paper with no current declared dependency is not a relation to
  record.
- **The author's sibling model wrappers** in the same GitHub organization — `iri2016`, `iri90`,
  `lowtran`, `msise00`, `hwm93` and others. They share an author, a packaging pattern and a
  Fortran-wrapping approach, and nothing else: they model different physical quantities, they exchange no
  data with this package, and neither depends on the other. "Same author, same pattern" would be equally
  true of a dozen packages, so it carries no information about this one.

### 30. Interoperable Software (OPTIONAL)
- `https://github.com/pydata/xarray`
- `https://www.mathworks.com/products/matlab.html`

Both entries rest on a *documented exchange* at the pinned revision, which is the only thing that
qualifies a foundational-but-domain-adjacent package for this field. Neither is here on dependency
presence, and neither is here as a member of any ecosystem.

**xarray — the identifier is repaired, the entry is kept.** Before this refresh this field held
`https://docs.xarray.dev/`, a **documentation site**; the field asks for a DOI or a code repository, so
the identifier is replaced with xarray's repository. The relation itself is exactly the exchange this
field's guidance offers as its worked example of a qualifying claim — the public API returns
`xarray.Dataset` objects as its documented interchange format. Here that is literal:
`src/igrf/base.py` annotates both public entry points `-> xarray.Dataset`, `src/igrf/__init__.py`
exports both, and `README.md` documents the return type explicitly ("returns an `xarray.Dataset`") and
prints the resulting dataset with its `north`, `east`, `down`, `total`, `incl` and `decl` variables. This
is not "uses xarray internally": the dataset *is* the software's output contract, and the Matlab bridge
below is built by converting it.

**MATLAB — kept, and the earlier grounds for removing it do not survive the evidence.** The
interoperation is documented, adapted and tested, which is the pattern this field names as a qualifying
cross-language bridge:

- `+igrf/igrf.m` calls the Python package directly —
  `dat = py.igrf.igrf(datestr(time), glat, glon, alt_km);` — behind a MATLAB `arguments` block that
  validates the four inputs.
- `+igrf/private/xarray2mat.m` is an explicit adapter, not incidental glue: it takes the returned xarray
  variable, reads `V = V.values;`, and reshapes it into a MATLAB array. `igrf.m` calls it six times, once
  per output component.
- `+igrf/TestUnit.m` is a MATLAB unit-test class asserting the six values, `setup.m` puts the Python
  library on MATLAB's path, `README.md` has a `### Matlab` section documenting the call, and the v13.0.2
  Zenodo release is titled `space-physics/igrf: Robust build, matlab unit test`.
- The README states the point of the bridge in the author's own terms: "Instead of the $1000 Aerospace
  Toolbox, use this free IGRF for Matlab". That is a genuinely distinguishing fact about this package,
  and this field is where a reader learns it.

**On the MathWorks URL, since it is the obvious objection.** MATLAB has no public code repository and no
DOI, and this field's guidance provides for exactly that case: where there is no repository, link where
users can find more information. The MathWorks product page is that page for MATLAB. Rejecting it as "a
marketing page for a commercial runtime" would delete a real, tested, documented capability over the
absence of an identifier its subject does not have, and recording the capability nowhere serves no
reader. Note that admitting this URL is about *identifier* admissibility for a relation that already
qualifies; it is not a precedent for admitting a landing page whose underlying *relation* fails the test
(see the IGRF-14 entry in Field 29).

**Considered and rejected:** numpy, the other declared dependency, and matplotlib, an undeclared optional
plotting import — generic stack, excluded here with no exceptions, and no exchange is documented for
either. Blanket claims of the "part of the standard scientific Python ecosystem" kind were not used and
should not be introduced.

### 31. Related Instruments (OPTIONAL)
Not applicable. Documented omission.

**IGRF is a global model, and this software is instrument-agnostic** — which under this field's relevance
test means it supports no instrument specifically. It reads no instrument's data, parses no
instrument-specific format, calibrates nothing, and is not an instrument-team tool. Its inputs are a date
and a position; its coefficients are compiled in. No instrument name appears anywhere in the 33 tracked
files at the pinned revision.

The model's *coefficients* are of course derived upstream from ground observatory and satellite
magnetometer measurements, but that is a fact about how IAGA produced the model rather than about what
this software supports, and it would be equally true of every IGRF implementation.

This field is SPASE-only in practice: an entry without an `https://spase-metadata.org/` identifier is not
submittable, and a bare name creates a new identifier-less vocabulary row. Nothing here needs resolving,
because there is no candidate to resolve.

### 32. Related Observatories (OPTIONAL)
Not applicable. Documented omission. Same reasoning as Field 31: the software is observatory- and
mission-agnostic, works with no mission's data products, implements no mission's conventions, and names
no observatory or mission anywhere in the tree.

### 33. Logo (OPTIONAL)
`https://www.ngdc.noaa.gov/IAGA/vmod/img/vmod_header.gif`

**What the asset is, established by fetching and looking at it.** The URL serves real image bytes —
`content-type: image/gif`, 18,445 of them, decoding as a GIF89a image of 550x70 pixels — rather than the
HTML page or the text pointer that a bad logo URL returns. The image is a wide web banner: a blue
gradient panel on the left carrying the two lines "IAGA Division V-MOD" and
"Geomagnetic Field Modeling", with a magnetic-field contour map filling the right two-thirds. It is the
**IAGA V-MOD website's header graphic**, not a mark designed for this Python package. The asset is not hosted in a git repository, so
there is no commit to pin; reachability is the only URL requirement in that case, and this URL is not a
branch reference that could silently break.

**The evidence that this is a deliberate choice rather than a stray, gathered so the question can be
settled once.** The value did not come from a guess: it is the `logo:` field of this package's entry in
the PyHC registry's unevaluated-projects list, whose entry reads in full

```yaml
- name: IGRF-13
  code: https://github.com/space-physics/igrf
  description: International Geomagnetic Reference Field IGRF -- in Python and Matlab
  logo: https://www.ngdc.noaa.gov/IAGA/vmod/img/vmod_header.gif
  contact: Michael Hirsch
  keywords: ["ionosphere_thermosphere_mesosphere","specific"]
```

at lines 65-70 of `_data/projects_unevaluated.yml` in `heliophysicsPy/heliophysicsPy.github.io` at commit
`fec609689cf7bbeffbc71d732bbe49fe3b7baa34` — a file byte-identical to the current `main`. The registry's
`contact:` for the entry is the package's own author.

Three further pieces of corroboration point the same way. First, it is a repeated practice rather than
a one-off, and the whole comparison set is small enough to state exactly. That file holds 28 entries,
every one of which gives Michael Hirsch as its contact, so it is one author's curation throughout. Nine
of the 28 carry a `logo:` at all; the other 19 carry none. Of those nine, five point at a graphic hosted
on the site of the institution behind the model or observatory the package serves — `GLOW` at
`www2.hao.ucar.edu`, `HWM-93` at `ccmc.gsfc.nasa.gov`, this entry at `www.ngdc.noaa.gov`, and `IRI-2016`
and `IRI-90` at `iri.gsfc.nasa.gov`. Of the remaining four, two are images from the package's own
repository (`LOWTRAN` and `GOESutils`, both on `raw.githubusercontent.com`) and two are re-hosted on a
generic image host (`DASCutils` and `THEMISasi`, both on `i.ibb.co`). Pointing at the model institution's
own site is therefore the largest single pattern among the entries that carry a logo, and — since most
entries carry no logo at all — supplying one is a choice made entry by entry rather than a default, which
is what makes it evidence of intent here. Second, this repository's own GitHub `homepage` field is set to `https://www.ngdc.noaa.gov/IAGA/vmod/` —
the very site whose header this image is. Third, the package's identity genuinely is "the IAGA V-MOD
IGRF-13 routine, made usable from Python", so the V-MOD banner is not an unrelated graphic.

**Rejected as alternatives:** `src/igrf/tests/incldecl.png` and `src/igrf/tests/vectors.png`, the two
images the README embeds. They are example output plots produced by `src/igrf/plots.py` — a
declination/inclination contour pair and a field-component pair — not logos, and substituting one would
misrepresent a figure as a mark. No other image exists in the repository.

**The value is a website banner rather than a conventional wordmark, and it is kept as it stands.** For
a third-party wrapper of an institutional model that is the apt choice: it is the value the package's own
author supplied to the registry, it is reachable and it is a real image, and it names the working group
whose routine the package compiles. No substitution was made — the only other images available are the
example plots rejected above.

---

## Sources

Repository evidence is drawn from `space-physics/igrf` at
`c418dd6940560d158568ebf35243266b92d09bf9` (2024-08-23), 33 tracked files, and every repository claim
above is true at that revision. External evidence: the Zenodo records for concept
`10.5281/zenodo.1184871` and version `10.5281/zenodo.5560949`; the PyPI JSON metadata for `igrf` (the
HTML project page is not authoritative — it answers 200 even for packages that do not exist);
`_data/projects_unevaluated.yml` in `heliophysicsPy/heliophysicsPy.github.io` at commit
`fec609689cf7bbeffbc71d732bbe49fe3b7baa34`; the GitHub API for repository metadata, topics and detected
languages; the public ORCID record `0000-0002-1637-6526`; Crossref and ADS/SciX for the publications in
Field 27 and the negative research in Field 14; and the NOAA IAGA V-MOD site for the upstream reference
implementation and the logo asset.
