# HSSI Metadata Extraction Results

**HSSI Software ID:** b677d3e7-9934-4e08-b823-8809798f2028
**Repository:** https://github.com/space-physics/hwm93
**Source Revision:** 5575db756404ae9de34d396835f54c28479f332b
**Extraction Date:** 2026-08-30
**Validation Date:** 2026-09-01
**Validation Status:** PASS

---

## Scope note — read this before the evidence

`space-physics/hwm93` is a thin Python (and MATLAB) interface around A. E. Hedin's original HWM93
Fortran source, which the repository carries in-tree at `src/hwm93_sub.f` (2,727 lines) and
`src/hwm93_driver.f` (79 lines). The vendored copy keeps Hedin's 1993 header and comments, but its
declarations have been modernised to Fortran 90 syntax, so it is not a byte-for-byte copy of the 1993
original — see Field 13 for the specific syntax, and note that the upstream original can no longer be
retrieved for comparison because its host no longer resolves (see the dead-link note at the end of
this file). `.gitattributes:1` marks `src/* linguist-vendored`, which is why
GitHub's language statistics report Python/Shell/MATLAB/Meson/CMake and **no Fortran at all** — a
false signal a future agent should not trust. Almost all of the scientific content of this package is
the vendored Fortran; the Python layer is `hwm93/__init__.py` (32 lines), `hwm93/plots.py` (14 lines)
and the `RunHWM93.py` CLI demo (47 lines).

**The repository is archived on GitHub and read-only.** Its last commit is the pinned revision above
(2021-03-22) and its last release is v0.9.1 (2018-08-16). Nothing about this software is expected to
change; a future refresh should expect the same evidence at the same pin.

**No component of this package reads any data file.** There is no `OPEN`/`READ`/`CLOSE` statement
anywhere in `src/hwm93_sub.f` or `src/hwm93_driver.f`; the model's spherical-harmonic coefficients
are compiled in by `subroutine GWSBK5()` (`src/hwm93_sub.f:1539`–`2727`). No Python file in the
package opens, reads, downloads, or requests anything. That single fact is the reason Fields 17, 18,
28, 31 and 32 are legitimately empty, and it should be re-checked before any of them is ever filled.

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
**Value:** https://doi.org/10.5281/zenodo.1311461

HSSI held no value for this field before this refresh, and the 2025-12 extraction recorded Field 2
as `Not found`, with the note `No DOI found in repository files, README, or metadata files.` That
negative conclusion is correct about the *repository* and wrong about the *software*: the repository
genuinely carries no DOI badge, no
`CITATION.cff`, no `codemeta.json` and no `.zenodo.json` — a case-insensitive grep for
`doi|zenodo|orcid|citat|cite` across every tracked file at the pin returns no matches at all. But a
Zenodo GitHub-integration archive of this project exists and was simply never linked back into the
repository.

**Evidence.** A Zenodo search for `hwm93` returns record 1311481, whose API response gives
`conceptdoi: 10.5281/zenodo.1311461` and `conceptrecid: 1311461`. DataCite resolves
`10.5281/zenodo.1311461` with `publisher: "Zenodo"`, `resourceTypeGeneral: "Software"`, creator
`Michael Hirsch, Ph.D.` (affiliation `SciVision, Inc.`), description `NASA Horizontal Wind Model
HWM93 in Python`, and three `HasVersion` relations — `10.5281/zenodo.1311462` (v0.8.0),
`10.5281/zenodo.1311467` (v0.8.1) and `10.5281/zenodo.1311481` (v0.9.0). `https://doi.org/10.5281/
zenodo.1311461` resolves (200). The deposits are titled `scivision/pyhwm93: …` because the repository
was still named `scivision/pyhwm93` in July 2018; that older path now redirects to
`https://github.com/space-physics/hwm93`, so the identity chain is unbroken.

**An independent check that does not key on the repository name.** Everything above keys on the
string `hwm93` or on a repository path, so those checks share a single failure mode: a manually
uploaded, descriptively titled deposit would be invisible to all of them at once. A DataCite query
keyed on title and creator instead fails differently and finds nothing —
`titles.title:"horizontal wind" AND creators.name:"Hirsch"` restricted to
`resource-type-id=software` returns 0, as does `titles.title:(HWM93 OR "horizontal wind model")`
under the same restriction, while the control `creators.name:"Hirsch, Michael"` under that
restriction returns a large body of this author's software deposits, so the query form works and the
empty results are real absence rather than a broken query. The absence of any further software DOI
for this package therefore rests on two checks that fail in different ways, not on repetitions of one
name-keyed check.

**Why the concept DOI and not a version DOI.** Field 2 asks for "the concept DOI for all versions".
`10.5281/zenodo.1311461` is exactly that. The version DOIs belong in Field 12's Version PID, and none
exists for the version this record stores — see Field 12.

**Traps recorded so a later refresh does not repeat them.** The Zenodo/DataCite metadata for this
concept DOI is *wrong* in two places and must not be used to autofill anything: (a) DataCite splits
the creator name into `givenName: "Ph.D."` / `familyName: "Michael Hirsch"`, a Zenodo name-parsing
artifact — Field 6 is derived from the repository and ORCID instead; (b) the Zenodo record declares
`license: {"id": "other-open"}`, which contradicts the repository's own `LICENSE.txt` and the
`setup.cfg` classifier — Field 15 is derived from the repository, never from the DOI record.

**Coupling with Field 11.** The form ties Publisher to whether a Zenodo DOI has been obtained, so
this identifier and Field 11's `Zenodo` stand or fall together. A future refresh that withdrew this
DOI would have to return Publisher to the repository host in the same move.

---

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/space-physics/hwm93

**Source:** The git remote at the pinned revision, `setup.cfg:7`
(`url = https://github.com/space-physics/hwm93`), and the GitHub API (`html_url`).

**Rename history, recorded because two authoritative external sources still point at the old names.**
PyPI's `home_page` for the `hwm93` package is `https://github.com/scivision/hwm93`, and the Zenodo
deposits reference `https://github.com/scivision/pyhwm93/tree/v0.9.0`. Both of those URLs redirect
(200) into `https://github.com/space-physics/hwm93`, the second preserving its `/tree/v0.9.0` path.
The chain is `scivision/pyhwm93` →
`scivision/hwm93` → `space-physics/hwm93`. The current value is correct; the stale upstream pointers
are not drift in this record and must not be "corrected" into it.

---

### 4. Software Functionality (RECOMMENDED)
**Values:**
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Physics-Based
- Data Visualization
- Data Visualization: Line Plots

HSSI stored a sixth value, `Data Visualization: 2D Graphics`, before this refresh. It was removed,
for the reason given below.

**Models and Simulations / Models and Simulations: Empirical.** HWM93 is an empirical model, stated
as such by its own reference publication title — "Empirical wind model for the upper, middle and
lower atmosphere" — and by `src/hwm93_sub.f:2`, `C      Horizontal wind model HWM93 covering all
altitude regions`. Uncontroversial.

**Models and Simulations: Physics-Based — kept, with the evidence that settles it.** This value could
look like over-classification on an empirical model, so the reason is recorded here to stop it being
re-litigated. HWM93 is not a curve fit over arbitrary basis functions: it represents the horizontal
wind field as *vector spherical harmonics* separated into divergent and rotational parts.
`src/hwm93_sub.f:1381`–`1382` declares `SUBROUTINE VSPHR1(C,S,L,M,BT,BP,LMAX)` with the header
comment `C      CALCULATE VECTOR SPHERICAL HARMONIC B FIELD THETA AND PHI`, and the model's switch
table at `src/hwm93_sub.f:38` reads
`C              24 - ALL B FIELDS (DIV)   25 - ALL C FIELDS (CURL)`. A divergence/curl decomposition
of a vector wind field is a physically motivated representation, which is what "Physics-Based
(broader than first principles) — semi-empirical physics" describes. From a searcher's side: someone
filtering for physics-based models and getting a semi-empirical harmonic wind model is not surprised;
someone who *excluded* it would be missing the standard semi-empirical wind field.

**Data Visualization / Data Visualization: Line Plots.** `hwm93/plots.py:5` defines
`plothwm(winds: xarray.Dataset)`, which calls `ax.plot(...)` twice to draw meridional and zonal wind
against altitude, labels the axes `"altitude [km]"` and `"winds [m/s]"`, and titles the figure.
`RunHWM93.py:41` calls it from the CLI. `hwm93.m:24`–`38` reimplements the same altitude-profile plot
in MATLAB. Line plotting is a real, user-facing capability of this package, not an internal step.

**Why `Data Visualization: 2D Graphics` does not belong.** That subcategory covers static 2D
plots of the contour/heatmap/image family — `pcolormesh`, `imshow`, contour plots, 2D maps. This
package produces none of those. `hwm93/plots.py` uses only `ax.plot`, and the MATLAB path uses only
`plot`. `Line Plots` already captures precisely what the software draws. A user filtering HSSI for
2D-graphics software expects images and fields, and would find a two-line altitude profile out of
place; nothing is lost to them, because that same user reaching for line plots still finds this
record.

**Considered and not selected, with reasons — do not re-propose without new evidence:**
- *Data Processing and Analysis* and every child of it. The package processes no input data. It
  evaluates a model from scalar arguments and assembles the result into an `xarray.Dataset`
  (`hwm93/__init__.py:26`–`30`). There is nothing read, filtered, calibrated, reduced or converted.
- *Data Processing and Analysis: File Format Conversion.* `RunHWM93.py:39` writes NetCDF via
  `winds.to_netcdf(outfn)`, but there is no input format to convert *from*. Writing model output is
  covered by Field 19, not by a conversion capability.
- *Coordinate Transforms* (and `Coordinate Transforms: Ionospheric`). `hwm93/__init__.py:15` calls
  `datetime2gtd(time, glon)` to derive year-day, UT seconds and local apparent solar time. Local
  solar time is arguably a coordinate, but the conversion is an internal argument-marshalling step
  performed by the `sciencedates` dependency, is not exposed as a capability of this package, and is
  not something a user would come to HWM93 for.
- *Models and Simulations: Forecasting.* HWM93 is a climatology evaluated at a requested time from
  user-supplied F10.7 and ap values. It predicts nothing forward.
- *Models and Simulations: Data Guided.* The F10.7 and ap arguments are user-typed scalars
  (`RunHWM93.py:22`–`24` defaults them to 150, 150 and 4). No observational data stream drives the
  model, so a user filtering for data-guided/assimilative models would find this out of place.
- *Servers and Environments* and *Mission-related*: nothing in the package is server, container,
  pipeline or mission-operations software.

**A durable caution about the vocabulary.** All 83 `FunctionCategory` rows carry an empty
`definition`. Category wording therefore has to come from the `software-functionality` skill's table;
"the vocabulary's own description" does not exist and must never be cited as an authority here.

---

### 5. Related Region (RECOMMENDED)
**Values:**
- Earth Atmosphere
- Earth Lower and Middle Atmosphere
- Earth Thermosphere
- Earth Ionosphere

`Earth Atmosphere` is carried over from the existing HSSI record, which held it alone;
`Earth Lower and Middle Atmosphere`, `Earth Thermosphere` and `Earth Ionosphere` were added in this
refresh. The Region vocabulary is **flat** — every row has empty `parents` and `children` — so none
of these four values implies any other, and each has to stand on its own evidence. That is why a
coverage argument of the form "Earth Atmosphere already encompasses the thermosphere" is not
available and would be a defect.

**Earth Atmosphere.** HWM93 is a whole-neutral-atmosphere model; the coarse value is the one a
user filtering broadly for atmospheric software will use, and this record belongs in that result set.

**Earth Lower and Middle Atmosphere.** The model genuinely reaches the ground. Its lower
altitude node table at `src/hwm93_sub.f:72`–`73` is
`      data ZN2/100.,90.,82.5,75.,67.5,60.,52.5,` / `     & 45.,37.5,30.,22.5, 15.,7.5, 0./` — nodes
at 100 and 90 km, then every 7.5 km from 90 km down to 0 km. The bundled test driver exercises 80,
60, 40, 20 and 0 km (`src/hwm93_driver.f:10`). `setup.cfg:9`–`11` lists `mesosphere`,
`stratosphere` and `thermosphere` as the package's own keywords, and the reference publication is
titled "Empirical wind model for the **upper, middle and lower** atmosphere". A user filtering HSSI
for lower- and middle-atmosphere software will be glad to find a wind model that actually covers the
stratosphere and mesosphere — that reach is unusual for software catalogued as heliophysics, and it
is the single most under-advertised property of this package.

**Earth Thermosphere.** `setup.cfg:11` and the GitHub topic list both carry `thermosphere`.
The upper node table is `      DATA ZN1/200.,150.,130.,115.,100./` (`src/hwm93_sub.f:71`), the CLI
default altitude sweep is 60 to 1000 km in 5 km steps (`RunHWM93.py:20`), the README example
evaluates 150 km, and `src/hwm93_sub.f:92` has an explicit `C       EXOSPHERE WIND` branch above
200 km. Thermospheric winds are the model's best-known application; a user filtering for thermosphere
software and *not* finding HWM93 would consider the catalogue broken.

**Earth Ionosphere — the reasoning in the searcher's terms.** HWM93 outputs
*neutral* winds, not plasma parameters, so on a literal "what does it compute" reading this value
looks wrong. Decide it instead from the side of the person browsing: someone filtering HSSI for
ionosphere software is, in practice, an ionospheric modeller, and a neutral wind model is a required
input to that work — neutral winds drive the F-region vertical drift and the ionospheric dynamo, and
HWM is the standard source for them. CCMC's own catalogue page for SAMI3
(`https://ccmc.gsfc.nasa.gov/models/SAMI3~1.0/`) describes it as a model in which "the neutral winds
are obtained from the HWM models", which is exactly the workflow such a user is in. The repository
agrees: `ionosphere` is one of the ten GitHub topics, the PyHC registry entry
keys this package as `ionosphere_thermosphere_mesosphere`, and `ionosphere` was already among the
record's keywords before this refresh. Would that user be annoyed to find HWM93 under Earth
Ionosphere? No — they would reach for it. That is the test, and it is passed.

**Considered and rejected — `Earth Auroral Subregion`.** Every Python and MATLAB worked example is
sited in the auroral zone: `RunHWM93.py:21` defaults to `(65, -148)`, the README example uses
`glat=65., glon=-148.`, and `hwm93.m:7`–`8` uses `65.1, -147.5` — Poker Flat, Alaska, the author's
home observatory. That is a demo location, not a scope, and the bundled Fortran driver makes the
point: its own 20-case sweep at `src/hwm93_driver.f:11`–`12` is
`      DATA XLAT/4*60.,0.,5*60.,4*45.,0,45.,45.,-45.,45.,45./` /
`      DATA XLONG/5*-70.,0.,4*-70.,5*0,90.,90.,0,-90.,-90./` — latitudes of 0°, ±45° and 60° at
longitudes of 0°, ±90° and −70°, nowhere near Poker Flat. HWM93 is a global model with no
auroral-specific treatment; a user filtering for auroral-region software would find a global wind
climatology out of place. Recorded so the Poker Flat coordinates are not mistaken for evidence again.

**Considered and rejected — solar and magnetospheric regions.** `F107A`, `F107` and `AP`
(`src/hwm93_sub.f:1`) are solar and geomagnetic *drivers* supplied as scalar inputs; they do not make
this software support science in the corona, solar wind, or magnetosphere. Aside from
`Earth Auroral Subregion`, rejected just above on its own grounds, the unselected rows of the Region
vocabulary are all solar, heliospheric, magnetospheric or planetary — `Chromosphere`, `Corona`,
`Photosphere`, `Solar Interior`, `Solar Environment`, `Solar Wind`, `Heliosheath`,
`Interplanetary Space`, `Earth Inner Magnetosphere`, `Earth Outer Magnetosphere`,
`Earth Magnetosheath`, `Earth Magnetosphere`, `Earth Magnetotail`, `Planetary Magnetospheres` and the
Jupiter, Saturn, Mars, Uranus and Neptune magnetosphere rows — and HWM93 computes nothing in any of
them.

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
- **Author Name:** A. E. Hedin
- **Author Identifier:** Not found — see the ORCID note below, which is a deliberate omission
- **Affiliation:** Not found — see the affiliation note below, which is a deliberate omission

Both authors are carried over from the existing HSSI record. Michael Hirsch is independently
confirmed as the author of the Python/MATLAB implementation by `setup.cfg:4`
(`author = Michael Hirsch, Ph.D.`), by `RunHWM93.py:3` (the module docstring names him), by
`LICENSE.txt:3` (`Copyright (c) 2015-2018 Michael Hirsch`), by PyPI (`author: Michael Hirsch, Ph.D.`)
and by being the sole GitHub contributor to the repository. ORCID `0000-0002-1637-6526` resolves to
Michael Hirsch with a Boston University employment (department ECE, Research Scientist, from
2018-08), which corroborates the stored identifier and the Boston University affiliation.

**Why A. E. Hedin belongs on this record.** This is the substantive judgement in this entry, so the
reasoning is recorded in full.

The case against is that the HSSI record describes the *software package* `space-physics/hwm93`, and
Hedin neither wrote nor released it. He wrote the model in 1993; the repository begins in 2015; he is
not named in `setup.cfg`, on PyPI, or on the Zenodo deposits, all of which credit Hirsch alone.

The case for is stronger, and it is a searcher's-side case. Someone who finds this record in HSSI has
searched for HWM-93. The record's own name is `HWM-93` and its description opens "NASA Horizontal
Wind Model HWM93 in Python and Matlab" — the thing being catalogued, from the user's point of view,
is Hedin's model, delivered through a Python interface. The package ships and executes Hedin's
Fortran: `src/hwm93_sub.f:3` reads `C      A. E. HEDIN  (1/25/93) (4/9/93)`, and that file is
essentially the whole scientific content of the download. The software's own documentation credits
him twice more — `README.md:112`,
`Original A. E. Hedin Fortran 77 HWM93 [code](ftp://hanna.ccmc.gsfc.nasa.gov/pub/modelweb/atmospheric/hwm93/)`,
and `RunHWM93.py:5`, `Original fortran code by A. E. Hedin`. Hedin is also first author of the
reference publication in Field 14. A user browsing HSSI by author for Hedin — the author of the HWM
and MSIS empirical model families — would expect this record back and would be right to. A record
that credited only the author of a 32-line wrapper, for a package named after and consisting mostly
of Hedin's model, would misattribute the science to a reader who cannot see the source tree.

Listing him is not an inference from domain knowledge; it is what the software itself says about its
own authorship. Keeping him also matches the repository's evident intent, which is to credit the
model's originator prominently in the README's Reference section.

**Deliberate omission — no ORCID is recorded for A. E. Hedin, and none should ever be.** His HSSI
Person row carried no identifier before this refresh, and this refresh adds none. Negative research
supporting the omission: an ORCID public search on family name `Hedin`, against the public expanded
search index at `https://pub.orcid.org/v3.0/expanded-search/?q=family-name:Hedin`, returns no NASA
or Goddard heliophysicist, and nothing else that corresponds to A. E. Hedin; the entries whose given
name begins with A are Anders, Astrid, Allan, Asa Suzanne (ORCID's own spelling, without the
diacritic) and Anna Isabel Hedin-Urrutia. Only two of those five list any institution in the
index — Swedish universities in one case, a US hospital and university in the other — and neither is
a heliophysics employer. He was a NASA Goddard scientist who died before ORCID existed in any
practical sense, so an ORCID for him is very unlikely to exist at
all. A name match must never be used to mint one: sending an identifier for an already-stored
identifier-less author does not annotate the existing row, it creates a second Person row and orphans
the first.

**Deliberate omission — no affiliation is recorded for A. E. Hedin.** NASA Goddard Space Flight
Center (`https://ror.org/0171mag52`, whose ROR display name is the shorter
`Goddard Space Flight Center`) is the historically correct affiliation and is recorded here as
context only. It is left off the record because the Person row is shared across HSSI records:
attaching an affiliation to it would change how Hedin appears on every entry that references the
same row, which is not something a refresh scoped to one entry should do. A future effort that is
scoped to that should use that ROR.

**Deliberate omission — `A. E.` is not expanded, and the Person row is not renamed.** The stored
given name is the short form. Expanding short-form given names to full names is a catalogue-wide
question that is open and parked elsewhere; it is not settled in this entry. For the record, the
short form is also what both primary sources use — `src/hwm93_sub.f:3` writes `A. E. HEDIN` and the
reference publication bylines `A.E. Hedin` — so the stored value is faithful to the sources even if
the catalogue later standardises on full names.

**Considered and not applied — a ROR for `Scivision, Inc.`** The affiliation recorded here carries
no identifier. ROR has exactly one match for a "Scivision" query, `https://ror.org/011qev639`, and
it is **SciVision Biotech Inc. (Taiwan)**, a Kaohsiung biotechnology company with no connection to Michael
Hirsch's US consultancy. **Do not attach that ROR to this affiliation.** This is the specific trap a
future agent doing an identifier sweep will walk into, which is why the wrong candidate is named
here rather than merely excluded.

**Considered and not applied — the `Scivision, Inc.` spelling.** DataCite and Zenodo render the
company as `SciVision, Inc.` with a capital V; the HSSI organization row is `Scivision, Inc.`. The
row is shared, and renaming an organization is not something a routine metadata update can do
safely or at all. Recorded so the difference is not mistaken for drift.

**Considered and rejected — additional authors from git history.** `git shortlog` at the pin shows
eight distinct author identities, but they are all Michael Hirsch under old and new names and
addresses (`Michael Hirsch, Ph.D`, `scienceopen`, `michael`, `nucl <hirsch617@gmail.com>`,
`10931741+scivision@users.noreply.github.com`). GitHub reports exactly one contributor account,
`scivision`. There is no second human contributor to add.

---

### 7. Software Name (MANDATORY)
**Value:** HWM-93

**Source:** Carried over from the existing HSSI record, and independently corroborated by the PyHC
registry, whose entry in `_data/projects_unevaluated.yml` is `name: HWM-93` with
`code: https://github.com/space-physics/hwm93`. PyHC metadata is manually curated and takes priority
over automated extraction.

**Alternative forms, recorded so the hyphen is not "corrected" later.** The distribution name is
`hwm93` (`setup.cfg:2`, PyPI), the README heading is `# HWM93 in Python` (`README.md:8`), and the
GitHub repository is `hwm93`. `HWM-93` is the curated display form and is how the model is written in
the heliophysics literature. Preserved as editorial intent; the differences are stylistic and none of
them is a correction.

---

### 8. Description (MANDATORY)
**Value:** NASA Horizontal Wind Model HWM93 in Python and Matlab. HWM93 is an empirical model that provides horizontal wind velocities (meridional and zonal components) for Earth's atmosphere from ground level to the exosphere. The model uses inputs including date, time, altitude, geographic location, solar activity indices (F10.7 flux), and geomagnetic activity indices (AP) to compute wind vectors. This Python implementation wraps the original Fortran 77 code by A. E. Hedin using f2py, making it accessible from Python and Matlab. The software supports multiple Fortran compilers (Gfortran, Intel ifort, PGI pgf90, Nvidia flang) and can output results to NetCDF/HDF5 format for further analysis.

**Carried over unchanged from the existing HSSI record.** It is the submitted wording and is
preserved as editorial intent, but every factual claim in it was checked against the pinned source
and all of them hold:

- The opening sentence is GitHub's own repository description
  (`NASA Horizontal Wind Model HWM93 in Python and Matlab`), with a sentence-final period added.
- *Meridional and zonal components* — `src/hwm93_sub.f:22`–`23`:
  `C        W(1) = MERIDIONAL (m/sec + Northward)` and `C        W(2) = ZONAL (m/sec + Eastward)`.
- *From ground level to the exosphere* — node tables reaching 0 km (`src/hwm93_sub.f:72`–`73`) and an
  explicit `C       EXOSPHERE WIND` branch (`src/hwm93_sub.f:92`).
- *Inputs* — the `GWS5` signature and its documented argument list, `src/hwm93_sub.f:1`, `:6`–`:16`.
- *Wraps the original Fortran 77 code by A. E. Hedin using f2py* — `README.md:26`
  ("We use `f2py` (part of `numpy`) to seamlessly use Fortran libraries from Python.") and
  `setup.py:5`, which builds the extension `hwm93fort` from `src/hwm93_sub.f` with
  `f2py_options=["only:", "gws5", ":", "--quiet"]`.
- *Multiple Fortran compilers* — `README.md:15`–`20` lists Gfortran ≥ 5, Intel `ifort`, PGI `pgf90`
  and Nvidia `flang`.
- *NetCDF/HDF5 output* — `README.md:55` and `RunHWM93.py:25`, `:39`.

No correction is warranted, and none should be made on stylistic grounds.

---

### 9. Concise Description (OPTIONAL)
**Value:** Python and Matlab interface to NASA's HWM93 empirical atmospheric horizontal wind model, computing meridional and zonal wind components for altitudes from 0 to 1000+ km.

**Carried over unchanged from the existing HSSI record** (169 characters, within the 200-character
limit). The "0 to 1000+ km" range is supported: the Fortran node tables start at 0 km, the CLI's
default sweep ends at 1000 km (`RunHWM93.py:20`), the MATLAB example sweeps `100:10:1000`
(`hwm93.m:9`), and above 200 km the model uses its exosphere branch, which has no upper cut-off.
Preserved as editorial intent.

---

### 10. Publication Date (RECOMMENDED)
**Value:** 2015-03-29

**Source:** Carried over from the existing HSSI record and independently confirmed. The repository's
earliest commit `0b6aaf98f948ed96b93d033c8f9ae8475a606896` is authored 2015-03-29 02:39:46 -0400 =
2015-03-29T06:39:46Z, which matches the GitHub API's `created_at` of `2015-03-29T06:39:46Z` exactly.

**A caution about this repository's history shape.** `git rev-list --max-parents=0 HEAD` returns
**four** root commits — `0b6aaf98` (2015-03-29 02:39:46 -0400), `30fc4f00` and `dce420ba` (both
2015-03-29 02:40:41 -0400, from a merged `scienceopen/python-hwm93` line) and `bae4cd71`
(2015-11-01). Three of the four sit on the same day, and `0b6aaf98` is the earliest. Anyone
re-deriving this date should use `git rev-list <pin>` restricted to the pinned lineage; the
space-physics repositories carry pre-rewrite orphan lineages that `git log --all` will surface and
that have misled prior reviews.

**Considered and not selected — 2018-07-13.** That is the date of the first formal release (GitHub
release `v0.8.0` and the first Zenodo deposit), and is a defensible reading of "first publication."
It was not selected because the source has been publicly available since March 2015, and because the
2018 dates properly belong to the version record in Field 12 rather than to the software's first
appearance.

---

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

HSSI stored `GitHub` / `https://github.com` before this refresh, which was the correct value on the
understanding that no DOI existed. Field 11's instruction is explicit and conditional: "For software
where a DOI has been obtained through Zenodo (e.g., GitHub-Zenodo workflow), Zenodo is the correct
entry. If no DOI has been obtained, indicate the repository host, such as GitHub or GitLab." A
Zenodo DOI *has* been obtained (Field 2), and DataCite records the concept DOI's publisher as
`Zenodo`.

The searcher's-side reason, not merely a rule-following one: if the record publishes a Zenodo DOI as
its persistent identifier, a user who clicks that identifier lands on Zenodo. A Publisher of "GitHub"
alongside it would tell that user the wrong thing about who archived the software.

**This value is contingent on Field 2, and the two move together.** Were the Zenodo concept DOI ever
withdrawn from Field 2, Publisher would have to return to `GitHub` / `https://github.com`, because
the form's fallback applies whenever no DOI has been obtained. Both organization rows —
`Zenodo` / `https://zenodo.org` and `GitHub` / `https://github.com` — already exist in HSSI under
exactly those names and identifiers, so that reversal would resolve cleanly if it were ever needed.

---

### 12. Version (RECOMMENDED)

#### Latest Version:
- **Version Number:** v0.9.1
- **Version Date:** 2018-08-16
- **Version Description:** Add Matlab HWM93 demo
- **Version PID:** Not found

**All four sub-fields are carried over unchanged from the existing HSSI record, and each is right.**
The reasoning for each is below, because each has a superficially attractive alternative.

**Version Number — keep `v0.9.1`; do not normalise away the `v`.** All sources agree on the number
and disagree only on the prefix: `setup.cfg:3` says `version = 0.9.1` and PyPI's single release is
`0.9.1`, while the git tag and the GitHub release are both `v0.9.1`. `v0.9.1` is the newest tag and
is a genuine ancestor of the pinned revision — verified with `git rev-list -n1 v0.9.1` →
`eee67c7d501cd3fea31b3bc0f493588c1dffb31e` plus `git merge-base --is-ancestor`, which is the check
that matters in these repositories because `git log --all` also surfaces orphan pre-rewrite lineages.
All four tags (v0.8.0, v0.8.1, v0.9.0, v0.9.1) pass the same ancestry check.

Decided from the searcher's side: `v0.9.1` and `0.9.1` are equally legible, a user filtering or
reading either one is neither confused nor annoyed, and `v0.9.1` is what the repository page itself
shows and what Field 12's own guidance uses as its example ("e.g., v1.0.0"). There is no user-visible
benefit to changing it. Replacing a version also orphans the previous `SoftwareVersion` row — settled
accepted HSSI behaviour, and never on its own a reason to avoid a *needed* correction, but here there
is no correction to make.

**Version Date — keep 2018-08-16.** The `v0.9.1` tagged commit is authored 2018-08-16, the GitHub
release for that tag was published 2018-08-16T19:02:54Z, and the PyPI sdist `hwm93-0.9.1.tar.gz` was
uploaded 2018-08-16T19:00:00. Three independent sources, one date.

**Version Description — keep `Add Matlab HWM93 demo`, and here is why it is not a quotation.** No
source carries that exact string. The GitHub release title is `add matlab HWM93 demo` (lower-case
"add" and "matlab"), and the tagged commit subject is `add matlab hwm93 example`. The stored value is
a sentence-cased rendering of the release title. That is the right thing for a field a user reads as
a change note, and it is recorded here explicitly so a future refresh does not flag the capitalisation
difference as drift and "fix" it back to the author's lower-case release title.

**Version PID — genuinely does not exist, and this is the negative research that should stop it being
re-proposed.** Zenodo's GitHub integration deposited exactly three releases of this project —
`10.5281/zenodo.1311462` (v0.8.0), `10.5281/zenodo.1311467` (v0.8.1) and `10.5281/zenodo.1311481`
(v0.9.0), all on 2018-07-13 — and then stopped. The v0.9.1 release of 2018-08-16 was never archived,
so there is no version DOI for the version this record stores. Substituting the v0.9.0 DOI would
attach the wrong version's identifier; substituting the concept DOI would duplicate Field 2. Leave
empty.

**No newer version exists.** The repository is archived, its last commit is the pinned revision
(2021-03-22), and there is no tag or release after v0.9.1.

---

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x
- Fortran77
- MATLAB

**Carried over unchanged from the existing HSSI record.** `setup.cfg:19` declares
`Programming Language :: Python :: 3` and `:27` requires `python_requires = >= 3.6`; `setup.cfg:18`
declares `Programming Language :: Fortran`; `hwm93.m` is a MATLAB entry point and `README.md:88`–`90`
documents it ("You can import this Python module from Matlab as in `hwm93.m`.").

**Considered and not selected — adding `Fortran90`.** The vendored source is *not* pure Fortran 77
despite the README calling it that. It is fixed-form (`.f`, `C` comment column, continuation in
column 6) but uses Fortran 90 declaration syntax throughout: `src/hwm93_sub.f:46`–`49` reads
`      integer, intent(in) :: IYD` / `      real, intent(in) :: SEC,ALT,GLAT,GLONG,STL,F107A,F107` /
`      real, intent(in) :: AP(2)` / `      real,intent(OUT) :: W(2)`, with `CHARACTER(len=4) ::`
declarations, `enddo`, `END SUBROUTINE`/`END FUNCTION` and `END program` — none of which a
strict-F77 compiler accepts. `Fortran77` was nonetheless kept as the single Fortran value because
Field 13 asks for "the most important languages... not meant to be an exhaustive list", because the
model's provenance is F77 and the repository says so itself — `README.md:112` describes the upstream
source as `Original A. E. Hedin Fortran 77 HWM93`, while `RunHWM93.py:5` carries the attribution
`Original fortran code by A. E. Hedin` without naming a dialect — and because a user filtering
`Fortran77` is looking for exactly this kind of legacy geophysical model wrapper. Recorded so that
neither the F90 syntax is mistaken for an error in the stored value, nor `Fortran90` re-proposed
without a fresh reason.

**Considered and rejected — Shell.** `tests/test_compilers.sh` is a developer convenience script for
sweeping compilers; it is not a language of the software. `Other` would be the only available row and
would tell a user nothing.

**A false signal to ignore.** GitHub's language statistics for this repository are Python, Shell,
MATLAB, Meson and CMake — Fortran is absent because `.gitattributes:1` marks `src/*
linguist-vendored`. Do not derive Field 13 from GitHub's language breakdown here.

---

### 14. Reference Publication (RECOMMENDED)
**Value:** https://doi.org/10.1016/0021-9169(95)00122-0

**Carried over from the existing HSSI record and verified.** Crossref and NASA ADS agree on the
bibliographic record: *Empirical wind model for the upper, middle and lower atmosphere*, A. E. Hedin,
E. L. Fleming, A. H. Manson, F. J. Schmidlin, S. K. Avery, R. R. Clark, S. J. Franke, G. J. Fraser,
T. Tsuda, F. Vial and R. A. Vincent — eleven authors — *Journal of Atmospheric and Terrestrial
Physics* **58**(13), 1421–1447, issued 1996-09, ADS bibcode `1996JATP...58.1421H`. The DOI resolves.

**Journal name correction.** The 2025-12 extraction described this as "Hedin et al., 1996" without a
journal; anyone filling that gap should note the journal for volume 58 is the *Journal of Atmospheric
and **Terrestrial** Physics*, not the *Journal of Atmospheric and **Solar-Terrestrial** Physics* —
the title change came after this volume. Both Crossref (`container-title`) and ADS (`pub`) give the
former.

**Why this DOI and not a software paper.** There is no JOSS or other software paper for the Python
implementation. This publication describes the model the software implements, which is what Field 14
asks for. The Fortran header dates the code to `A. E. HEDIN  (1/25/93) (4/9/93)`
(`src/hwm93_sub.f:3`), three years before the paper — the paper is the model's formal description,
which is the standard relationship for the HWM family.

**Full text is not retrievable by ordinary fetch.** The publisher returns 403 to non-browser clients,
Unpaywall reports `is_oa: false` / `oa_status: closed`, OpenAlex finds no open location, and Europe
PMC has no record (`hitCount 0`). The bibliographic facts above are all from Crossref and ADS
metadata, which is sufficient for this field.

---

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

HSSI held no license value before this refresh. The value is derived from the repository, never from
DOI autofill.

**Evidence.** `LICENSE.txt:1` is `The MIT License (MIT)` and `LICENSE.txt:3` is
`Copyright (c) 2015-2018 Michael Hirsch`; the file continues with the standard MIT permission and
warranty-disclaimer paragraphs. `setup.cfg:16` declares the classifier
`License :: OSI Approved :: MIT License`, and `setup.cfg:21`–`22` sets `license_files =` /
`  LICENSE.txt`. GitHub's own license detection reports `key: mit`, `spdx_id: MIT` and
`name: MIT License` for this repository.

`MIT License` is the exact stored name of the controlled-vocabulary row, and that row carries
`url: https://spdx.org/licenses/MIT`, which is the URI recorded above.

**Why not the Zenodo value.** The Zenodo deposit declares `license: {"id": "other-open"}`, which
would map to `Other`. That is Zenodo's own error, contradicted by three repository-internal sources
and by GitHub's detection. DOI autofill copies such errors verbatim; the repository is authoritative
for this field.

**Why not `https://opensource.org/licenses/MIT`.** The 2025-12 extraction used that URI. It is a
valid MIT landing page, but the License vocabulary row itself carries the SPDX URL, and Field 15 says
the URI is auto-populated for SPDX licenses. The SPDX form is the one to store.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- atmospheric science
- empirical model
- f2py
- fortran
- geoscience
- horizontal wind model
- hwm93
- ionosphere
- matlab
- matlab-python-interface
- mesosphere
- middle atmosphere
- neutral winds
- python
- stratosphere
- thermosphere
- upper atmosphere

**Fourteen values are carried over from the existing HSSI record; three were added in this
refresh** — `neutral winds`, `upper atmosphere` and `middle atmosphere`.

**Provenance of the carried-over fourteen.** The GitHub topic list supplies ten of them exactly:
`f2py`, `fortran`, `geoscience`, `hwm93`, `ionosphere`, `matlab`, `matlab-python-interface`,
`mesosphere`, `python`, `thermosphere`. `setup.cfg:9`–`11` supplies `mesosphere`, `stratosphere` and
`thermosphere`. The remaining three — `atmospheric science`, `empirical model`, `horizontal wind
model` — are derived terms: the first from the `setup.cfg:20` classifier
`Topic :: Scientific/Engineering :: Atmospheric Science`, the other two from the reference
publication's title and the model's own name.

**`neutral winds` — the highest-value addition here.** HWM93 computes *neutral* winds,
and that is precisely what distinguishes it from the plasma-drift and convection models a user might
otherwise confuse it with. A heliophysicist searching HSSI for "neutral wind" should get HWM93 back;
before this refresh no stored keyword on this record named the *neutral* wind specifically. The
closest value then stored, `horizontal wind model`, was the model's name rather than the quantity,
and it did not distinguish neutral winds from the plasma drifts and convection velocities that other
records describe. No row for this value existed in the keyword vocabulary before this refresh, so
recording it created one. That is legitimate — Keywords is the only open vocabulary — and it is not
a near-duplicate: the existing `wind` and `winds` rows are too generic to discriminate, and before
this refresh no row anywhere in the keyword vocabulary contained the string `neutral` at all.

**`upper atmosphere` and `middle atmosphere` — both reuse existing vocabulary rows.**
They come straight from the reference publication's title, "Empirical wind model for the upper,
middle and lower atmosphere", and they are how atmospheric scientists name the altitude bands this
model spans. A user searching either phrase would be glad to find a wind model that actually covers
both. Reusing the existing rows avoids minting near-duplicates.

**Considered and not selected.** `hwm` exists as a keyword row and would broaden matching to the
model family, but `hwm93` is already stored and the shorter form adds little beyond it.
`atmospheric modelling` and `atmospheric-modelling` both exist as rows and are near-duplicates of
each other and of `atmospheric science`; adding either would deepen an existing vocabulary mess
without helping a searcher. `ionosphere_thermosphere_mesosphere` is the PyHC registry's raw
underscore key and reads as machine output, not as a keyword a person would type.

---

### 17. Data Sources (OPTIONAL)
**Value:** Not applicable — no data source

**Carried over as empty from the existing HSSI record, and this is an evidenced-empty rather than an
unexamined gap.** The software reads nothing. There is no `OPEN`, `READ`, `CLOSE` or `INQUIRE`
statement anywhere in `src/hwm93_sub.f` or `src/hwm93_driver.f`; the model's coefficients are
compiled in by `subroutine GWSBK5()` (`src/hwm93_sub.f:1539`–`2727`). No Python file in the package
opens a file, downloads anything, or imports an HTTP client — `hwm93/__init__.py`, `hwm93/plots.py`
and `RunHWM93.py` contain no `open(`, `requests`, `urlopen`, or download call. F10.7 and ap arrive as
scalar function arguments (`RunHWM93.py:22`–`24`, defaulting to 150, 150 and 4).

The seventeen values in this vocabulary are all remote archives, services and access protocols —
AMDA, CDAWeb, das2, FTP/FTPS Directories, GFZ, HAPI, HTTP/HTTPS Directories, Madrigal,
Observatory/Mission-specific, OMNIWeb, Other, S3/Cloud-aware, SSCWeb, TAP, The Virtual Solar
Observatory., VirES and WDC. This package uses none of them, and that is why the field is correctly
empty rather than a candidate for `Other`.

---

### 18. Input File Formats (RECOMMENDED)
**Value:** Not applicable — no file input

**Carried over as empty.** For the same reason as Field 17: nothing is read. The public entry point
`hwm93.run(time, altkm, glat, glon, f107a, f107, ap)` (`hwm93/__init__.py:9`) takes only scalars and
an array of altitudes, and the CLI passes command-line arguments straight through
(`RunHWM93.py:19`–`34`).

---

### 19. Output File Formats (RECOMMENDED)
**Values:**
- HDF5
- netCDF3/4

**Carried over unchanged from the existing HSSI record.** `RunHWM93.py:25` adds the option
`-o`, `--outfn` with help text `write NetCDF (HDF5) of data`, and `RunHWM93.py:39` writes it with
`winds.to_netcdf(outfn)`. `README.md:55` states "Write data to NetCDF (HDF5) with `-o` option." Both
rows are justified because the repository itself names both, and because netCDF-4 is an HDF5
container — the software's own wording, "NetCDF (HDF5)", is the reason both are listed rather than a
guess about which engine xarray selects at runtime.

**Considered and rejected — `ascii`.** The Fortran test driver writes formatted text to unit 6
(`src/hwm93_driver.f:20`, `:66`–`:77`), and `CMakeLists.txt:13`–`14` diffs that stdout against the
fixture `tests/test.log`. That is a build-time regression check, not a user-facing output format; a
user filtering HSSI for software that writes ASCII data products would find nothing usable here.

---

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

**Carried over unchanged from the existing HSSI record and confirmed against CI.**
`.github/workflows/ci.yml` defines three jobs — `linux` on `ubuntu-latest` (`:14`), `macos` on
`macos-latest` (`:28`) and `windows` on `windows-latest` (`:40`) — each installing the package and
running pytest, with the Windows job configuring mingw32 and `FC: gfortran` (`:46`, `:52`). The
archived `archive/.appveyor.yml` additionally targeted Visual Studio 2017 and Ubuntu 1804.

**Considered and not selected — `Operating System Independent`.** `setup.cfg:17` declares the
classifier `Operating System :: OS Independent`, which is a claim of portability rather than of
tested support. Listing three specifically tested platforms is more informative to a user deciding
whether the package will build for them, and mixing the blanket value in beside them would be
contradictory. Note also that `OS Independent` is *not* a value in the HSSI vocabulary — the only
cross-platform row is `Operating System Independent`, spelled out — so the classifier string could
never have been used verbatim.

---

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Carried over unchanged from the existing HSSI record.** Nothing in the package is
architecture-specific: it is portable Fortran plus Python. `meson.build:5` and `CMakeLists.txt:6` add
`-march=native` for GCC, which tunes for whatever host is compiling and is therefore
architecture-agnostic rather than architecture-restricting.

**Considered and not selected — enumerating `x86-64` and `Apple Silicon arm64`.** The CI runners of
2021 were x86-64 in all three jobs, so that enumeration would record where it happened to be tested
rather than what it requires, and would narrow the record misleadingly for a user on arm64. The
practical requirement is a Fortran compiler, not an architecture.

---

### 22. Related Phenomena (OPTIONAL)
**Value:** Not applicable — no phenomenon in the vocabulary applies

**Carried over as empty, but re-examined against the live seven-value vocabulary rather than
inherited as a blank.** The seven rows are `Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic
Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and `X-ray emission`. The vocabulary is flat,
so no value implies another.

Six of the seven are solar or heliospheric phenomena and have no bearing on a model of Earth's
neutral horizontal winds.

**`Geomagnetic Storms` — considered seriously, and rejected.** There is a real argument for it: ap is
one of the model's inputs (`src/hwm93_sub.f:1`), the documented switch table includes
`9 - DAILY AP` and `13 - MIXED AP/UT/LONG` (`src/hwm93_sub.f:33`, `:35`), the second element of the
AP array is documented as `C             AP(2)=CURRENT 3HR ap INDEX (used only when SW(9)=-1.)`
(`src/hwm93_sub.f:16`), and storm-time thermospheric winds are a genuine research topic. It was
rejected on the searcher's-side test: HWM93 is a quiet-time climatology with a weak magnetic-activity
correction, not storm software. A user filtering HSSI for geomagnetic-storm software is looking for
storm indices, ring-current models, or storm forecasting; a general wind climatology in that result
set is out of place and dilutes it. The ap dependence is an input parameter, not a phenomenon the
software supports science functionality *for*.

An evidenced-empty value is a legitimate outcome for this OPTIONAL field, and this is one.

---

### 23. Development Status (RECOMMENDED)
**Value:** Unsupported

HSSI held no development status before this refresh.

**The signals, and which one was weighted.** The repository is `archived: true` on GitHub, its last
commit is the pinned revision of 2021-03-22, its last release is v0.9.1 of 2018-08-16, and
`setup.cfg:13` declares `Development Status :: 4 - Beta`.

The `setup.cfg` classifier was **not** weighted. It is a PyPI packaging-maturity label, frozen at the
2018 release, drawn from a different vocabulary than repostatus.org's; "4 - Beta" describes API
stability at packaging time, not whether the project is still developed. Reading it as a repostatus
term would produce a nonsense answer.

**The archived flag is the decisive signal, and it has to be tested against every row, not just
against the row one is trying to exclude.** An archived GitHub repository is read-only: it accepts no
commit, no issue and no pull request. That is a statement about what can happen to this project from
here on, not merely a measure of how long it has been quiet.

**Clause by clause against the vocabulary's own definitions.** Unlike `FunctionCategory`, whose rows
carry no definition at all, the `RepoStatus` rows do carry one, and it is the repostatus.org
wording — so this choice is decidable from the text of the rows rather than from intuition about what
the terms feel like.

- **`Unsupported` — selected.** "The project has reached a stable, usable state but the author(s)
  have ceased all work on it. A new maintainer may be desired." Both clauses hold. *Stable, usable
  state*: the final release was published to PyPI as a working distribution (`0.9.1` there, tagged
  `v0.9.1` in the repository — see Field 12), `.github/workflows/ci.yml` builds and tests it on
  Linux, macOS and Windows, and `tests/test_all.py:19`–`20` asserts reference wind values to a
  relative tolerance. Schumm et al. (2020), recorded in Field 27, used the package in a published
  study, which is independent confirmation that a usable release existed and is immune to toolchain
  drift. That last point matters, because installability itself has decayed: `setup.py:3` is
  `from numpy.distutils.core import setup, Extension`, and `numpy.distutils` is gone for
  Python ≥ 3.12 / numpy ≥ 1.26, so `pip install hwm93` fails on a current default toolchain even
  though the sdist installed cleanly in its era. Nothing about the value turns on that. The choice
  between `Unsupported` and `Inactive` cannot turn on it either: "stable, usable state" is wording
  those two rows share. The release condition is load-bearing only against `WIP`, `Suspended` and
  `Abandoned` below, and what those rows ask is whether a stable, usable release was ever made — not
  whether it still installs on a current toolchain.
  *Ceased all work*: no commit since 2021-03-22, no release since 2018-08-16, and the repository has
  been put into an archived, read-only state, which is the author's own act of closing it. The
  second sentence is permissive — "may be desired", not "is desired" — so it offers a possibility
  rather than imposing a requirement, and nothing has to be shown about a wanted maintainer for the
  row to fit.
- **The permissive maintainer clause is durable negative research, and it points *toward* this
  value.** Reading "A new maintainer may be desired." as though it required evidence that a
  maintainer *is* wanted is a misquotation of the source, and that misreading is what previously
  argued against `Unsupported` here. With the real wording restored, no clause of this row is unmet.
  A future refresh that finds no maintainer solicitation in the repository, the README or the archive
  notice has found nothing that counts against this value.
- **`Inactive` — considered and rejected on its final clause.** "The project has reached a stable,
  usable state but is no longer being actively developed; support/maintenance will be provided as
  time allows." Its first two clauses fit this project exactly as well as `Unsupported`'s first
  sentence does; the third does not. An archived repository cannot receive an issue or a pull
  request, so support "as time allows" is structurally impossible rather than merely slow, and
  storing it would promise a visitor something this project cannot deliver. Note that the two rows
  are *contrary* claims about the author's posture rather than nested ones — `Inactive` affirms
  continuing support, `Unsupported` denies it — so neither is the weaker or safer choice, and the
  archived flag is what decides between them. Recorded so `Inactive` is not re-proposed from the
  commit and release dates alone, which is how it would look right.
- **`Active` — excluded.** "The project has reached a stable, usable state and is being actively
  developed." No commits for five years, no releases for eight, repository read-only.
- **`WIP`, `Suspended` and `Abandoned` — excluded on the opening condition all three share**, that
  "there has not yet been a stable, usable release": a stable, usable release of this package was
  made and published to PyPI, so none of them can apply. `Suspended` fails twice over, because it
  also requires that "the author(s) intend on resuming work" and archiving is the opposite of
  intending to resume. `Abandoned`'s second clause — "the project has been abandoned and the
  author(s) do not intend on continuing development" — does describe this project, which is
  precisely why its release condition has to be read as the discriminator.
- **`Concept` — excluded.** "Minimal or no implementation has been done yet, or the repository is
  only intended to be a limited example, demo, or proof-of-concept." This is a working model wrapper
  published on PyPI, not a demonstration.
- **`Moved` — excluded.** "The project has been moved to a new location, and the version at that
  location should be considered authoritative." The repository was renamed twice, but nothing was
  relocated to a new authoritative project, and the old URLs redirect here rather than away.

**What the value tells a user.** The software reached a working state, it is finished, and no one is
maintaining it — so it can be relied on to behave exactly as it does today, and no bug report will be
answered. That is the operative fact for anyone deciding whether to build on this package.

---

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/space-physics/hwm93

**Carried over unchanged from the existing HSSI record.** There is no documentation site, no `docs/`
directory and no Read the Docs configuration in the repository at the pin. `README.md` is the
documentation: it covers installation including compiler prerequisites for all three platforms
(`:23`–`:44`), command-line use (`:51`–`:55`), module use with a worked example and the shape of the
returned object (`:57`–`:86`), MATLAB use (`:88`–`:90`), and Fortran-only use via Meson or a direct
f2py invocation (`:94`–`:107`). Field 24 explicitly allows the access URL when documentation is not
separately hosted.

---

### 25. Funder (OPTIONAL)
**Value:** Not found

**Negative research, so this is not re-searched from scratch each refresh.** No tracked file at the
pin contains any funding, grant, award or acknowledgement statement. A case-insensitive grep across
every tracked file for `fund|acknowledg|grant|NSF|NASA|award` matches four lines, and none of them is
a funding statement: `LICENSE.txt:5` (`Permission is hereby granted, free of charge, to any person
obtaining a copy` — the MIT boilerplate), `README.md:10`
(`NASA Horizontal Wind Model HWM93 in Python &ge; 3.6`, which names the model's origin rather than a
funder of this software), and the `nasa.gov` hostname inside the dead upstream FTP URL at
`README.md:112` and `RunHWM93.py:6`. The Zenodo deposit carries no grants and
DataCite records no `fundingReferences` for the concept DOI. Crossref returns `funder: None` for the
reference publication.

**Considered and rejected — NASA as funder.** The model HWM93 was developed at NASA Goddard; the
Python interface in this repository was not, and Field 25 asks what funded *this software*. Recording
NASA here would tell a user that this package was NASA-funded work, which is not evidenced. The NASA
relationship is already visible where it belongs: in the software name, the description, the
reference publication and the Hedin authorship.

---

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Same negative research as Field 25.** No award title or number appears anywhere in the repository,
in the Zenodo/DataCite records, or in Crossref's metadata for the reference publication.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** https://doi.org/10.1029/2020JA027944

HSSI held no related publications before this refresh, and the 2025-12 extraction recorded Field 27
as `Not found`, with the note `No publications citing or using this specific Python implementation
were found in the repository`. That is true of the
repository and false of the literature; the citation is in a paper, not in the repo.

**The publication.** Schumm, G.; Bonnell, J. W.; Wygant, J. R.; Mozer, F. S. (2020), *Calculation of
the Atomic Oxygen Fluence on the Van Allen Probes*, **Journal of Geophysical Research: Space
Physics**, ADS bibcode `2020JGRA..12527944S`, DOI `10.1029/2020JA027944`. The study models atomic
oxygen exposure to the Van Allen Probes spacecraft over the mission, for which a neutral-atmosphere
wind and density specification is required.

**Why it qualifies as a use of *this* software rather than of the model.** NASA ADS full-text search
places the literal string `github.com/space-physics/hwm93` in this paper's text, and the paper's
**acknowledgements section** contains both `Hirsch` and `space-physics`. The queries are recorded
here in their scoped form, because the bare predicates are a different claim entirely:
`doi:10.1029/2020JA027944 ack:"Hirsch"` → 1 and `doi:10.1029/2020JA027944 ack:"space-physics"` → 1
(equivalently `bibcode:2020JGRA..12527944S`), whereas an unscoped `ack:"Hirsch"` or
`ack:"space-physics"` matches a large slice of the ADS corpus through tokenisation and says nothing
about this paper. A refresh that re-derives the claim from the bare predicate will get a very
different result and could wrongly conclude this record is false. That acknowledgement is a credit to
this specific Python implementation by its repository URL and its author, not a citation of Hedin's
1996 paper. In the full-text index,
`full:"space-physics/hwm93"` and `full:"github.com/space-physics/hwm93"` each return this paper and
no other, while `full:"pyhwm93"`, `full:"scivision/hwm93"` and `full:"zenodo.1311461"` each return
nothing.

**Verification method and its limits, recorded because the source cannot be re-read directly.** The
publisher returns 403 to non-browser clients and the paper is not open access (Unpaywall
`is_oa: false`; OpenAlex reports no open location; Europe PMC has no record), so the exact
acknowledgement sentence could not be retrieved. The findings above come from targeted membership
queries against ADS's indexes, run with negative controls that behaved correctly: scoped to this
paper, a nonsense token and a fabricated grant number each returned nothing under `ack:`, while
`ack:"Hirsch"`, `ack:"space-physics"` and `ack:"NRLMSISE"` each returned it, as did
`full:"github.com/space-physics/hwm93"`, `full:"horizontal wind model"` and `full:"NRLMSISE"`. The
two indexes are not interchangeable — `horizontal wind model` is present in the full text but not
under `ack:` — so any re-derivation has to state which index it queried. **If the exact
acknowledgement wording is ever needed, a browser can render the article page where a plain fetch
cannot.**

**Considered and rejected — the other papers that mention HWM93.** ADS full-text and
acknowledgement searches for `HWM93`, alone and alongside `Python`, return a further handful of
papers, but those cite the *model* — its 1996 paper or its Fortran — and not this package. Only one
paper in ADS names this repository, and it is the one recorded above (`full:"space-physics/hwm93"`).
Field 27 is for publications that describe, cite or use *the software*, so the rest do
not belong, and this note exists so they are not swept in wholesale on a later pass.

---

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Evidenced absence, not an unexamined blank.** The software neither reads nor produces a dataset
that is published anywhere. F10.7 and ap enter as user-typed scalars, and the model's coefficients
are compiled into the Fortran (`src/hwm93_sub.f:1539`–`2727`) rather than distributed as data. The
one data-like artifact in the repository, `tests/test.log`, is a regression fixture of the Fortran
driver's stdout, not a scientific dataset.

---

### 29. Related Software (OPTIONAL)
**Values:**
- https://github.com/geospace-code/sciencedates
- https://github.com/space-physics/msise00

Before this refresh HSSI stored three further entries here — `https://github.com/numpy/numpy`,
`https://github.com/pydata/xarray` and `https://github.com/dateutil/dateutil`. All three were
removed, and `msise00` was added. The reasoning for each is below.

**One bar, applied to every candidate.** A package earns a place in Field 29 or 30 only if it is
**(a) informative to a heliophysics searcher** — it tells them something true of *this* software and
not of most Python packages — **and (b) actually connected**, by a specific artifact in the code,
docs, examples or tests. Both conditions, for every candidate, in both directions. In particular,
code evidence alone does not admit a package, and domain similarity alone does not either. This
matters here because the list HSSI stored before this refresh mixed the two standards.

**`sciencedates` — kept.** Condition (b): `hwm93/__init__.py:4` is
`from sciencedates import datetime2gtd`, called at `:15` on the package's only public code path;
`setup.cfg:34` declares it in `install_requires`; `.coveragerc:7` omits `*/sciencedates/*` from
coverage measurement, which shows how closely the two were developed. Condition (a): despite its
generic tagline, `datetime2gtd` produces the `(IYD, UTSEC, STL)` triple — year-and-day as YYDDD, UT
seconds, and local apparent solar time — that geophysical Fortran models such as `GWS5` require as
their argument convention (`src/hwm93_sub.f:6`–`:11`). That convention would be absurd in a web app,
a finance model or a biology pipeline, which is the test. It is also a geospace-code sibling by the
same author and the shared time layer beneath a family of these model wrappers, so a heliophysics
user who sees it learns something real and may well need it directly.

**`numpy` — removed here, and not recorded in Field 30 either.** It satisfies condition (b)
emphatically — `README.md:26` says "We use `f2py` (part of `numpy`) to seamlessly use Fortran
libraries from Python", `setup.py:3` imports
`from numpy.distutils.core import setup, Extension`, and `setup.py:5` builds the `hwm93fort`
extension with f2py — but it fails condition (a) completely. f2py is generic Fortran-wrapping
infrastructure, used identically outside heliophysics, and numpy is at home in a web app, a finance
model and a biology pipeline alike. From a searcher's side, a numpy link on the HWM93 page conveys
nothing, because it would be equally true of nearly every record in HSSI. The wrapper mechanism is
already recorded where it is useful: in Field 8's description and in the `f2py` keyword.

Applying the bar symmetrically is the point: `sciencedates` is kept because it passes *both*
conditions, and `numpy` is dropped because it fails (a) — not because one had code evidence and the
other did not. Both have code evidence.

**`python-dateutil` — removed.** Same outcome, same reasoning. It is genuinely used
(`hwm93/__init__.py:5` and `RunHWM93.py:10`, both for `parse()` on a timestamp string) and genuinely
generic date parsing.

**`xarray` — removed from Field 29 and recorded in Field 30 instead.** Its role here is
interoperability, not similarity: it is not a competing atmospheric model, a predecessor, a fork
parent, or a domain-specific library. On a Related Software list it tells a user nothing about how
HWM93 relates to other wind models; on the Interoperable list it tells them the output plugs into the
xarray/NetCDF ecosystem, which is genuinely useful. See Field 30 for the evidence that admits it
there.

**`msise00` — added, and it is the one genuinely debatable call in these two fields.** Field 29's
own definition names the case: "[s]oftware that performs similar tasks but does not necessarily link
together... For example, two software that model the upper atmosphere of Earth
but using different assumptions." HWM93 (neutral winds) and NRLMSISE-00 (neutral density and
temperature) are the canonical paired empirical upper-atmosphere models; a user running one very
often needs the other. `https://github.com/space-physics/msise00` is the same author's Python and
MATLAB wrapper of NRLMSISE-00, built on the same architecture, and is not archived.

The in-repository evidence is real but indirect: `src/hwm93_sub.f:4`–`5` reads
`C      Calling argument list made similar to GTS5 subroutine for` /
`C       MSIS-86 density model and GWS4 for thermospheric winds.` — Hedin deliberately shaped HWM93's
interface to match the MSIS density model's. That establishes the model-family relationship at the
pin. What it does not literally name is the `space-physics/msise00` package; connecting `MSIS-86` /
`GTS5` to that repository is a short but real inferential step.

From the searcher's side the entry earns its place: someone on the HWM-93 page who is shown MSISE-00
under Related Software has been told exactly the thing they most need to know next, and would not
find it out of place. The one caveat on the entry is that the link is inferred rather than quoted;
the inference is set out above so a later refresh can weigh it rather than rediscover it.

**Considered and rejected — `gemini3d/hwm14`, the successor model.** HWM14 supersedes HWM93 and is,
in the abstract, the most useful thing one could tell a visitor to this record. It was not selected
for three reasons: nothing at the pinned revision references HWM14 at all; the candidate repository
is a CMake/Fortran build harness (GitHub reports only Fortran and CMake, with no Python interface),
so it is a different kind of artifact from this package rather than a peer implementation; and it has
moved organisations, from `space-physics/hwm14` to `gemini3d/hwm14`, which makes the URL less stable
than a Field 29 entry should be. Recorded with its context — CCMC hosts HWM14 at
`https://ccmc.gsfc.nasa.gov/models/HWM14~2014/` — so a future refresh can revisit it deliberately
rather than rediscovering it.

**Considered and rejected — `iri2016`, `igrf` and the other space-physics model wrappers.** They
share an author and an architecture with this package but model different quantities (ionospheric
plasma, the geomagnetic field) and are not paired with HWM93 by anything in the repository or by
scientific practice the way MSIS is. Listing the whole sibling org would turn Field 29 into a
directory of one developer's output, which tells a searcher nothing about HWM93 specifically.

**Considered and rejected — `hwm93fort`.** It is not separate software. It is this repository's own
f2py extension module, built from `src/hwm93_sub.f` by `setup.py:5` and imported at
`hwm93/__init__.py:2`.

**A caution about display names.** Before this refresh, every RelatedItem row on this record carried
the repository URL in both the name and identifier positions. Such names are placeholders and are
not surfaced to a user, so they must not influence which packages belong in Fields 29 and 30.

---

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://github.com/pydata/xarray

Before this refresh HSSI stored two further entries here, `https://github.com/matplotlib/matplotlib`
and `https://github.com/numpy/numpy`. Both were removed, for the reasons below.

**`xarray` — kept, with the specific exchange cited.** xarray is a package that qualifies only on
documented-exchange evidence, never on dependency presence, and here the evidence is unusually
direct: `xarray.Dataset` is this package's **documented public interchange format**. `README.md:67`
states "`winds` is an [xarray.Dataset](http://xarray.pydata.org/en/stable/generated/xarray.Dataset.html)"
and `README.md:69`–`81` prints the returned object's full repr, including its dimensions,
coordinates, data variables and attributes, as part of the usage documentation. The public function
is annotated `-> xarray.Dataset` (`hwm93/__init__.py:9`) and constructs one explicitly at `:26`–`:30`.
Downstream use is real in two directions: `RunHWM93.py:39` serialises it with `winds.to_netcdf(outfn)`,
and `hwm93.m:18`–`19` reads it from MATLAB via `winds{'meridional'}` and `winds{'zonal'}`. A user who
already works in xarray can consume this model's output without writing an adapter, which is what
this field is asking.

**`matplotlib` — removed.** It is a generic plotting library, excluded from this field
without exception. It is genuinely used — `hwm93/plots.py:1` imports
`from matplotlib.pyplot import figure`, `RunHWM93.py:13` imports `show`, and `setup.cfg:45`–`47`
declares the `plot` extra — but "uses matplotlib for its plots" is true of most of the scientific
Python ecosystem and so tells a searcher nothing about HWM93. The plotting capability itself is
recorded where it belongs, in Field 4 (`Data Visualization: Line Plots`).

**`numpy` — removed.** Same reasoning as in Field 29: real usage, zero discriminating
information. Being a dependency is not interoperability.

**Considered and rejected — `seaborn`.** `setup.cfg:45`–`47` declares
`plot =` / `  matplotlib` / `  seaborn`, so seaborn is an optional extra of this package. It was not
among the values HSSI stored in either field before this refresh, and it fails the bar twice over:
it is a generic plotting library of exactly the kind this field excludes, **and** it is not imported
anywhere in the package at the pin — `hwm93/plots.py` uses matplotlib only, and no other file
references it. The declaration is vestigial. Recorded so a future dependency sweep does not add it.

**Considered and not selected — MATLAB.** This is the strongest Tier-B case the repository offers,
and it was still declined. The evidence for a genuine cross-language bridge is real: `hwm93.m` is a
complete MATLAB entry point that calls `py.hwm93.run(...)` (`hwm93.m:16`), converts the returned
xarray variables with `double(py.numpy.asfortranarray(V))` (`hwm93.m:41`), and plots them; the README
documents it at `:88`–`:90`; and the GitHub topic list includes `matlab-python-interface`. It was not
selected because Field 13 already records MATLAB as a language of this software, so the capability is
already discoverable, and because Field 30 stores a URL per entry — for a commercial numerical
computing environment that would be a vendor product page rather than a repository. From a searcher's
side, someone reading "Interoperable Software" wants the peer scientific packages they can pair with
HWM93; a commercial IDE listed among them reads as out of place. The bridge itself is genuine, so
the evidence is recorded here rather than discarded: a later refresh that weighed it against the
vendor-URL awkwardness differently would start from this paragraph rather than from scratch.

**Considered and rejected — the blanket ecosystem claim.** The 2025-12 extraction justified this
field with the note `The software interoperates with standard scientific Python libraries; it returns
xarray datasets and optional plotting workflows use matplotlib.` A blanket ecosystem claim is never
sufficient on its own, which is why each entry above stands or falls on a named artifact instead.
What survives from that note is its xarray half, on the documented-exchange evidence given above; its
matplotlib half is precisely the generic-plotting claim this field excludes.

---

### 31. Related Instruments (OPTIONAL)
**Value:** Not applicable — the software is instrument-agnostic

**Carried over as empty, and examined rather than left blank by default.** HWM93 is a global empirical
model. It reads no instrument's data — see the scope note and Field 17 — implements no
instrument-specific format or convention, is not an instrument-team tool, and does not model or
visualise any particular instrument's measurements. It supports no instrument specifically, which is
the definition of instrument-agnostic. A user searching HSSI by instrument would not expect a global
wind climatology back, and would find it out of place among tools that actually read that
instrument's data.

**Considered and rejected — the instruments behind the model's empirical fit.** The tempting move
here is to associate HWM93 with the observations it was fitted to. The HWM family was built from
ground-based MF and meteor radar, incoherent-scatter radar, Fabry-Perot interferometers and
satellite instruments, and CCMC's description of the successor model names the UARS WINDII and HRDI
instruments explicitly. Those are the model's *provenance*, decades upstream of this Python package,
and the package cannot read a byte of any of their data. Someone on a WINDII or HRDI page clicking
"show software related to this instrument" wants software that works with those measurements; a
Fortran wind model wrapped in Python would be a puzzling result.

**A vocabulary observation, recorded so this is not re-derived.** Several of those instruments have no
row in HSSI's controlled instrument/observatory vocabulary at all: searches for `WINDII`, `HRDI`,
`wind imaging` and `high resolution doppler` return zero rows. So even if the relevance gate were
somehow passed, there would be nothing to resolve to. The general-class labels that *do* appear —
`Incoherent Scatter Radar`, the various `Meteor radar` station rows, the three Fabry-Perot rows — are
site-specific or generic-class entries that HWM93 has no relationship to.

**A note for any future refresh that reopens this.** Fields 31 and 32 accept only entries carrying a
`https://spase-metadata.org/` identifier, and there is no free-type path: submitting a bare name
either binds to some arbitrary same-named row or mints a new identifierless one. So even a change of
mind about the relevance gate could not be acted on for WINDII or HRDI until those rows exist
upstream.

---

### 32. Related Observatories (OPTIONAL)
**Value:** Not applicable — the software is observatory-agnostic

**Carried over as empty, examined on the same basis as Field 31.** The package works with no
mission's or observatory's data, implements none of their conventions, and is not a mission-team
tool.

**Considered and rejected — the platforms behind the model's empirical fit.** Unlike the instruments,
several of these *do* exist in the vocabulary: `Upper Atmosphere Research Satellite`
(`https://spase-metadata.org/SMWG/Observatory/UARS`), `Dynamics Explorer-B`
(`https://spase-metadata.org/SMWG/Observatory/DynamicsExplorer2`), the `Atmosphere Explorer` family
and `Gravity Field and Steady-State Ocean Circulation Explorer`
(`https://spase-metadata.org/SMWG/Observatory/GOCE`). They were rejected anyway, and the resolvability
is precisely why the rejection needs writing down. Apply the governing test: a user on the UARS page
clicking "show software related to this observatory" is looking for software that reads, calibrates,
plots or otherwise handles UARS data. HWM93 does none of that; it is a 1993 empirical fit that
happens to have consumed some UARS-era measurements in its derivation, distributed here as a Python
wrapper that reads nothing. That user would find it out of place, and the association would dilute a
result set they need to be clean. Provenance of a model's coefficients is not designed-to-support.

**Considered and rejected — Van Allen Probes.** Schumm et al. (2020), recorded in Field 27, used this
software in a Van Allen Probes study. That is a paper's use of the software, not the software's
support of the mission; HWM93 knows nothing about the Van Allen Probes and reads none of their data.
Recorded because Field 27 and Field 32 sit close together and the temptation to mirror one into the
other is real.

**Considered and rejected — Poker Flat.** The repository's example coordinates (65, -148) are the
author's home observatory, used as demo defaults in `RunHWM93.py:21`, the README example and
`hwm93.m:7`–`8`. A demo location is not an observatory the software is designed to support. See also
Field 5, where the same coordinates were rejected as evidence for the auroral region.

---

### 33. Logo (OPTIONAL)
**Value:** Not found

**Carried over as empty, and two candidates were examined and rejected.**

**Rejected — `tests/example.png`.** It is a real 63,133-byte PNG (verified by its file signature) that
`README.md:13` embeds as `![image](tests/example.png)`, and it does serve as `image/png` from
`https://raw.githubusercontent.com/space-physics/hwm93/5575db756404ae9de34d396835f54c28479f332b/tests/example.png`
— so it would satisfy the mechanical requirements of the field. It is nonetheless not a logo: it is
the matplotlib output of `plothwm`, a wind-versus-altitude profile used as a README illustration and
as a visual reference for the test suite. A user scanning HSSI cards would see a line chart where an
identifying mark belongs.

**Rejected — the CCMC logo offered by the PyHC registry.** The PyHC entry in
`_data/projects_unevaluated.yml` supplies `logo: https://ccmc.gsfc.nasa.gov/images/CCMC-LOGO-2.gif`,
and that URL is live (200, `image/gif`). PyHC is normally a priority source, which is exactly why this
rejection is recorded: the image is the Community Coordinated Modeling Center's organisational logo,
not a mark for this software. CCMC does not host, maintain or distribute this Python package, and
CCMC's current model catalogue does not carry HWM93 at all (see Field 3's neighbouring note in the
Additional Notes section below). Putting CCMC's logo on this record would assert a provenance that
does not exist.

The software has no logo. That is the correct value.

---

## Additional Notes

### The dead upstream link to the original Fortran — a durable finding

Two files point at a host that no longer exists. `README.md:112` reads
`Original A. E. Hedin Fortran 77 HWM93 [code](ftp://hanna.ccmc.gsfc.nasa.gov/pub/modelweb/atmospheric/hwm93/)`
and `RunHWM93.py:6` carries the same URL as
`from ftp://hanna.ccmc.gsfc.nasa.gov/pub/modelweb/atmospheric/hwm93/`. The host
`hanna.ccmc.gsfc.nasa.gov` is **NXDOMAIN** — DNS resolution fails outright, and curl exits 6
(couldn't resolve host). The Wayback Machine has no snapshot of that FTP path either.

GitHub records this repository's `homepage` as the HTTPS form of the same path,
`https://ccmc.gsfc.nasa.gov/pub/modelweb/atmospheric/hwm93/`. That URL now returns **404**, as does
its parent `https://ccmc.gsfc.nasa.gov/pub/modelweb/`. The Wayback Machine does hold a snapshot of
the HTTPS path from 2022-01-06, so the modelweb archive was still live then and has since been
retired.

**Does CCMC host HWM93 anywhere today? Investigated: no.** `https://ccmc.gsfc.nasa.gov/` and
`https://ccmc.gsfc.nasa.gov/models/` are both live (200). The models catalogue contains exactly one
HWM entry — **HWM14**, at `https://ccmc.gsfc.nasa.gov/models/HWM14~2014/`, with an Instant Run
service at `https://kauai.ccmc.gsfc.nasa.gov/instantrun/hwm/` (live) and a public repository link to
`https://map.nrl.navy.mil/map/pub/nrl/HWM/HWM14/` (live). There is no HWM93 page:
`https://ccmc.gsfc.nasa.gov/models/HWM~93/` returns 404, and `https://map.nrl.navy.mil/map/pub/nrl/HWM/HWM93/`
redirects to the parent HWM directory, which offers no HWM93 subdirectory.

**Consequence for this record.** The repository's own reference link is permanently broken and the
software is archived, so it will never be fixed upstream. The vendored `src/hwm93_sub.f` in this
repository is now among the more accessible copies of Hedin's HWM93 Fortran, which strengthens rather
than weakens the case for this HSSI entry. No HSSI field should carry the dead `ftp://` URL or the
404-ing `ccmc.gsfc.nasa.gov/pub/modelweb/` path — in particular, GitHub's `homepage` value must not be
used for Field 24, which is why Field 24 points at the repository README instead.

### PyHC registry status

This package appears in the PyHC registry's **unevaluated** list,
`_data/projects_unevaluated.yml`, not in `projects_core.yml` or `projects.yml`. The entry is:
`name: HWM-93`, `code: https://github.com/space-physics/hwm93`,
`description: NASA Horizontal Wind Model HWM93 in Python and Matlab`,
`logo: https://ccmc.gsfc.nasa.gov/images/CCMC-LOGO-2.gif`, `contact: Michael Hirsch`,
`keywords: ["ionosphere_thermosphere_mesosphere","specific"]`. Being unevaluated means PyHC has not
assessed the package against its standards; it carries no quality ratings, so nothing in that entry
informs Field 23. The registry supplies the curated software name (Field 7) and corroborates the
description; its logo field is rejected in Field 33.

### Model interface reference, for anyone re-deriving the science fields

The single public entry point is
`SUBROUTINE GWS5(IYD,SEC,ALT,GLAT,GLONG,STL,F107A,F107,AP,W)` (`src/hwm93_sub.f:1`), exposed to
Python through f2py as `hwm93fort.gws5` (`setup.py:5`, `hwm93/__init__.py:21`). Its documented
arguments (`src/hwm93_sub.f:6`–`:16`) are year and day as YYDDD, UT seconds, altitude in km, geodetic
latitude and longitude in degrees, local apparent solar time in hours, the three-month average and
previous-day F10.7 flux, and a two-element AP array. Outputs are `C        W(1) = MERIDIONAL (m/sec +
Northward)` and `C        W(2) = ZONAL (m/sec + Eastward)` (`src/hwm93_sub.f:22`–`23`).

Internally the model is built from vector spherical harmonics (`VSPHR1`, `src/hwm93_sub.f:1381`),
associated Legendre polynomials (`LEGPL1`, `:1427`) and cubic-spline interpolation between altitude
nodes (`SPLINE`/`SPLINT`, `:1456`, `:1495`), with coefficients supplied by `GWSBK5` (`:1539`). The
altitude structure is `ZN1 = 200, 150, 130, 115, 100` km above and `ZN2 = 100 … 0` km below
(`:71`–`:73`), with a separate exosphere branch above 200 km (`:92`).
