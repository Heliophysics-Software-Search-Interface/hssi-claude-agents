# HSSI Metadata Extraction Results

**HSSI Software ID:** 9c1d2774-3eeb-4b72-bd48-fa7eb5c5e39e
**Repository:** https://github.com/space-physics/WMM2020
**Source Revision:** db7be2cd4a84dc55e66e3bbf1523a62f25ec8ad3
**Extraction Date:** 2026-09-06
**Validation Date:** 2026-09-07
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

WMM2020 is a **thin Python wrapper around NOAA's World Magnetic Model C reference implementation**,
which the repository vendors under `src/wmm2020/src/`. Every claim below comes from one of two
distinct classes of evidence, and they must not be conflated:

- **Wrapper-authored material** — `setup.cfg`, `pyproject.toml`, `setup.py`, `README.md`,
  `MANIFEST.in`, the CMake and Meson build definitions, `.github/workflows/ci.yml`, and the seven
  tracked `.py` files. This is Michael Hirsch's work and describes *this package*.
- **Vendored upstream material** — four of the five `.c` files, the two `.h` files, `src/Makefile`
  and `WMM.COF` under `src/wmm2020/`. This is NOAA's code and documentation. It is authoritative
  about **the WMM model** — its physics, its validity limits, what it does and does not include, and
  who wrote it — and it is the best source in the repository for Fields 5, 6, 22, 27 and 28. It is
  *not* evidence about the Python package's design, licensing intent or maintenance. The one
  exception is `src/wmm2020/src/wmm_point_sub.c`, Hirsch's adaptation of NOAA's `wmm_point.c` into
  the callable `wmmsub` entry point that the Python layer calls through `ctypes`; that file belongs
  to the first class.

The distinction matters most for Field 15 (the vendored notice licenses NOAA's code, and the tree
says nothing about the wrapper), Field 5 and Field 22 (the vendored text states plainly which
physical regions and phenomena the model does *not* describe), and Field 6 (the vendored code
carries its own authorship credits).

A second scope fact: the repository has never carried a `CITATION.cff`, `codemeta.json` or
`.zenodo.json` — not at the pinned revision and not anywhere in its 28-commit ancestry. The tracked
tree at the pin holds 32 files in total. Structured-metadata files that normally supply authors,
identifiers and licence simply do not exist here, so most fields are established from package
metadata, the vendored C, and external authorities.

A third: this record is one of a pair. `space-physics/WMM2015` is the same author's previous-epoch
package with near-identical architecture, and it has its own HSSI entry. Shared architecture is a
reason to check the sibling's reasoning, never a reason to inherit its conclusions — where this file
reaches a different answer, it says why on this tree's evidence.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Note:** This placeholder is the catalogue convention for a record whose HSSI submitter is supplied
at submission time rather than derived from the repository. It is not a gap in the extraction.

### 2. Persistent Identifier (RECOMMENDED)
Not found

**No DOI exists for this software.** HSSI held no value for this field before this refresh, and the
research below supports leaving it empty rather than treating it as unexamined.

The repository contains no DOI: no `CITATION.cff`, no `codemeta.json`, no `.zenodo.json`, and the
four README badges (lines 3–6) are a GitHub Actions status badge, an LGTM Python language grade, a
PyPI supported-Python-versions badge and a pepy download counter — none is a DOI badge. Absence in
the tree cannot by itself rule out a deposit made outside the repository, so three independent,
structurally different searches were run, each paired with a control proving the search could see a
deposit that *does* exist. Every count below is what those searches returned on 2026-09-06.

1. **Repository-slug search.** Zenodo returns 0 records for the quoted phrase
   `"space-physics/wmm2020"`. The differential control is the decisive part: the identically shaped
   query `"space-physics/lowtran"` returns 1 record (`space-physics/lowtran: New f2py build using
   CMake`), so the instrument is live for deposits made under this exact owner and slug convention.
   DataCite returns 0 for the same literal string and 0 for `titles.title:"wmm2020"`; Zenodo returns
   0 for `title:wmm2020`.
2. **Old-repository-name redirect test — here there is nothing to redirect.** A slug-keyed search is
   blind to a deposit made under a former repository name, so the rename history must be checked.
   This repository shows no sign of ever having been renamed. Across all 28 commits in the pin's
   ancestry, `setup.cfg` has declared `url = https://github.com/space-physics/wmm2020` and `name = wmm2020` from the
   initial commit onward, and every one of the **88** `github.com/<owner>/<repo>` self-references
   found anywhere in that history is that same lowercase string. (Pattern
   `github\.com/[A-Za-z0-9_.-]+/[A-Za-z0-9_.-]+` run with `git grep -ohP` over all tracked files at
   every commit reachable from the pin; the only other matches are `David-OConnor/pyflow`, 28, and
   `space-physics/wmm2015`, 6.) So unlike its sibling package, this repository has no former name
   under which a deposit could hide.
3. **Creator-keyed search — the only class that can find a manual upload,** which carries no
   repository name at all. Every record was enumerated, not just the first page. Zenodo
   `metadata.creators.person_or_org.name:` returns 48 records for `"Hirsch, Michael"` (47 unique
   titles), 34 for `"Michael Hirsch"`, 28 for `"SciVision"`, 3 for `"Tavant, Antoine"` (1 unique
   title), and 0 for both `"Nielsen, Aaron"` and `"Korzh, Andrey"`. None of those titles matches the
   case-insensitive regex `wmm|world magnetic|magnetic model|geomagnet`. DataCite keyed on the ORCID
   recorded in Field 6 (`creators.nameIdentifiers.nameIdentifier:"https://orcid.org/0000-0002-1637-6526"`)
   returns 166 records spanning 26 distinct titles, none matching that regex. These result sets are
   their own controls: they are large and they contain this author's genuine deposits, including
   geomagnetism-adjacent ones — `GIMA Magnetometer tools` and `Auroral Electrojet Tools` both appear
   — so the instruments demonstrably see this creator's work in this subject area.

Two further controls. A Zenodo search for `title:"World Magnetic Model"` returns 1 record — a
model-based error-grid deposit by other authors — showing the title index is live and does surface
WMM-subject material when it exists. And the creator-name variants must be unioned rather than
treated as one query, because Zenodo does not normalise creator names: `"Hirsch, Michael"`,
`"Michael Hirsch"` and `"SciVision"` return three different-sized result sets for the same person.

**A method trap that mints false negatives.** As of 2026-09-06 an **unquoted** `owner/repo` slash
makes the Zenodo API return **HTTP 500 with a JSON error body**, which a naive reader parses as an
empty result set. Every zero above was recorded only after confirming the response shape was a real
`hits` object with `total: 0`. Quote the phrase, and check the shape before recording any zero.

**Do not re-run a repository-name-keyed check alone and conclude from it.** It is structurally
incapable of detecting the manual-deposit case, which is the case that would apply here. The sibling
package WMM2015 likewise carries no persistent identifier, so the absence is a property of this
author's WMM packages rather than an oversight specific to this record.

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/WMM2020

**A capitalisation divergence exists, and it is settled: the capitalised form is retained.** This is
recorded in full so a later refresh understands why the lowercase spelling was considered and not
taken, and does not rediscover it as a defect.

*What the repository itself says — lowercase, always.* `setup.cfg` declares
`url = https://github.com/space-physics/wmm2020` and `name = wmm2020`, and has since the initial
commit with no rename ever. All 88 `github.com/...` self-references across the whole history use that
lowercase string (pattern and scope in Field 2). GitHub's API reports the canonical name in lowercase
too: `full_name`, `name` and `html_url` all read `space-physics/wmm2020`. PyPI's `home_page` for the
`wmm2020` distribution is likewise the lowercase URL.

*What the capitalised form has behind it.* The PyHC registry uses it —
`_data/projects_unevaluated.yml` line 155 reads `code: https://github.com/space-physics/WMM2020` —
and it is the spelling HSSI stores in both this field and Field 24, and the spelling the registry
also uses for the sibling WMM2015 entry.

*Why the capitalised form is kept.*

1. **A case change would break a live in-catalogue relation.** The HSSI entry for WMM2015 points at
   this entry through its related-software field using this exact capitalised URL string, and those
   relations resolve on the exact string rather than case-insensitively. Lowercasing here would leave
   a published sibling entry pointing at a URL this entry no longer carries — a user-facing breakage
   bought for a cosmetic gain. **This reason carries the retention on its own**: it turns on how the
   catalogue stores and resolves the relation, not on GitHub's behaviour, so it holds whether or not
   reason 2 remains true.
2. **There is no user-facing benefit on the other side.** As of 2026-09-06 both spellings return
   HTTP 200 with no redirect at all (`redirect_url` empty, the effective URL preserving whichever case
   was requested), so the link works identically either way and no reader is ever sent astray. GitHub's
   case handling is GitHub's to change, so treat this reason as dated rather than durable — and check
   it before relying on it.
3. **The capitalised form is not unsupported.** It is the registry's own spelling for this project and
   its sibling, and it is HSSI's existing convention across both records.

A future refresh should not "correct" this field or Field 24 to lowercase. The lowercase evidence is
recorded here precisely so that it stops being rediscovered as a problem.

### 4. Software Functionality (RECOMMENDED)
- Models and Simulations
- Models and Simulations: Empirical
- Data Visualization
- Data Visualization: 2D Graphics

Every value is a live `FunctionCategory` row, and each subcategory's parent is present, so the
selection is structurally complete. `FunctionCategory` rows carry empty definitions throughout — not
one of the 83 rows has a definition — so the category wording used below comes from the project's
software-functionality classification guidance, never from the vocabulary itself.

**Models and Simulations: Empirical.** WMM2020 evaluates a spherical-harmonic geomagnetic model whose
Gauss coefficients are fitted to observations and shipped as a data table, `src/wmm2020/WMM.COF`
(93 lines, first line `    2020.0            WMM-2020        12/10/2019`). The vendored library's own
abstract describes it as built for spherical-harmonic models of the Earth's magnetic field generally
(`GeomagnetismLibrary.c:15`: ` * It however is built to be used for spherical harmonic models of the Earth's magnetic field`),
and `GeomagnetismHeader.h:131` declares `    int nMax; /* Maximum degree of spherical harmonic model */`.
This is precisely the class of empirical geomagnetic reference model the category exists for: it is
not derived from first principles, and it runs no solver.

**Data Visualization: 2D Graphics.** `src/wmm2020/plots.py` defines
`def plotwmm(mag: xarray.Dataset):`, which draws two labelled contour panels —
`    ax[0].set_title("Magnetic Declination [degrees]")` and
`    ax[1].set_title("Magnetic Inclination [degrees]")` — over a geographic longitude/latitude grid,
via `    h = ax[0].contour(mag.glon, mag.glat, mag.decl, range(-90, 90 + 20, 20))`. Contour plots on
a 2-D grid are 2D Graphics. `RunWMM2020.py` exercises this as the package's worked example.

#### The two `Data Processing and Analysis` rows were stored on this record and have been removed

The record previously carried `Data Processing and Analysis` and `Data Processing and Analysis: Analysis`.
Both are gone, and the reasoning is set down in full so a later refresh does not restore them as an
obvious omission.

*The category is gated on scientific data, and this package analyses none.* The parent means reading,
transforming or analysing scientific data. WMM2020's three computational entry points — `wmm`,
`transect` and `wmm_point` in `src/wmm2020/base.py` — all do the same thing: evaluate a fitted global
coefficient table at coordinates the caller supplies, through the `libwmm.wmmsub` C call. Nothing
measured is ingested, filtered, calibrated, fitted or reduced. The coefficient table
`src/wmm2020/WMM.COF` is not data being analysed — it *is* the model, shipped as its parameters.

*The searcher's side gives the same answer.* A user filtering HSSI on
`Data Processing and Analysis: Analysis` is looking for tools that do something to *their* data, and
would find a pure forward model out of place among them.

*What was argued for keeping them, and why it does not carry.* Three points had real force and are
recorded rather than dismissed. `transect()` computes field values along an arbitrary caller-supplied
path, which is closer to producing a derived series than a single lookup — but the series is still
evaluated from the model, not derived from anything measured. The CMake build registers a genuine
file-in/file-out batch job as a test, `add_test(NAME WMM20file` running
`COMMAND $<TARGET_FILE:wmm20_file> f ${CMAKE_CURRENT_SOURCE_DIR}/test_input.asc  ${CMAKE_CURRENT_BINARY_DIR}/test_output.asc`,
which has the shape of a processing step — but its input is a coordinate list rather than a
measurement, and Field 19 records how narrowly that program is exposed to a user. And the values were
stored and a curator selected them, so they are broad rather than false — which is a reason to record
why they came off, not a reason to leave them on.

*The question that settled it* was whether "Analysis" in this catalogue means anything a user
computes, or specifically analysis performed on observational data. The second reading is the one the
vocabulary's own gating on scientific data supports, and under it both rows come off.

**A consequence outside this entry, disclosed rather than relied on.** The sibling WMM2015 entry
carried neither row when the two were compared during this refresh. Removal therefore brought the two
entries into agreement, where keeping the rows would have left them disagreeing. That is a consequence
of this choice and never a reason for it: the argument above rests on this tree's entry points and on
the category's own gating, and would stand unchanged had the sibling been classified the other way.

**Categories considered against the live 83-row vocabulary and rejected, with reasons.** Recorded so
a later refresh does not re-litigate them.

- **Models and Simulations: Forecasting.** Genuinely arguable and therefore settled in writing.
  `WMM.COF` carries secular-variation coefficients — `GeomagnetismHeader.h:129` declares
  `    double *Secular_Var_Coeff_G; /* CD - Gauss coefficients of secular geomagnetic model (nT/yr) */`
  — and the library extrapolates the field forward from the 2020.0 epoch, so the software really does
  predict a future field state. Rejected all the same: in this catalogue "Forecasting" means
  space-weather prediction, and a user filtering on it wants nowcasts and event forecasts, not a
  five-year secular drift term.
- **Models and Simulations: Physics-Based / First Principles / Theory / Data Guided.** The
  spherical-harmonic expansion is a physically motivated basis, but the software solves nothing — it
  evaluates a fitted coefficient table shipped inside the package. `Empirical` already carries the
  correct meaning, and a physics label would overstate what runs. `Data Guided` is the near-miss
  worth naming: the coefficients were fitted to data, but they were fitted upstream by NOAA and BGS
  and arrive here as a frozen table, so no observation guides anything at run time.
- **Coordinate Transforms** and its Heliospheric / Ionospheric / Magnetospheric / Mission-Specific /
  Planetary / Solar children. The vendored C contains real coordinate machinery, including geodetic
  and spherical conversions and a Transverse Mercator projection. None of it is reachable from this
  package: `src/wmm2020/__init__.py` is the single line `from .base import wmm, wmm_point`, and the
  geodetic-to-spherical step happens inside `wmmsub` as an internal utility. Classifying an internal
  utility as a user-facing capability is the specific error this category is prone to.
- **Data Processing and Analysis: File Format Conversion, Data Access and Retrieval, Data Reduction,
  Calibration, Time Series Analysis, Processing.** No format is converted; nothing is retrieved (see
  Field 17); nothing is reduced or calibrated; no time-ordered measurement is analysed. `transect`
  produces an ordered series but the ordering is the caller's, not time's.
- **Data Visualization: Line Plots** — `plotwmm` calls `ax.contour`, not a line plot.
- **Data Visualization: 2D Slices** — tempting, because `wmm()` is documented to work "for a single
  altitude value" and so returns a constant-altitude cut through a 3-D field. Rejected: the values
  are computed directly at that altitude; nothing is sliced out of a stored 3-D volume, which is what
  the category describes.
- **Data Visualization: 3D Graphics, Movies, Web-Based, Orbit Plots, Spectrogram, Hodograms,
  Mission-Specific, Spacecraft Formation Plots, ML/AI** — no such code exists; `plots.py` is 20 lines
  and contains only the two contour panels.
- **Mission-related** and all its children — this is not part of any mission's ground system. See
  Fields 31 and 32.
- **Servers and Environments** and its children — no server, no container definition, no HPC or
  parallel code. The build's `--parallel` flag in `src/wmm2020/build.py` parallelises *compilation*,
  not computation.

### 5. Related Region (RECOMMENDED)
- Earth Atmosphere

**The previously recorded rationale for this value was unusable and has been replaced.** An earlier
revision of this file argued from a PyHC registry keyword — that
`ionosphere_thermosphere_mesosphere` "confirms applicability to Earth's upper atmosphere". That is
the propagated-registry-tag pattern: the tag is a facet label attached to many registry entries, not
a statement this software makes about itself, and the model's own scope statement cuts directly
against it. The value survives; the reasoning is re-derived below from this tree.

**What the software's own artifacts establish.** The public entry points take geographic coordinates
and an altitude in kilometres:
`def wmm(glats: np.ndarray, glons: np.ndarray, alt_km: float, yeardec: float) -> xarray.Dataset:` and
`def wmm_point(glat: float, glon: float, alt_km: float, yeardec: float) -> dict[str, float]:`.
`RunWMM2020.py` declares `p.add_argument("alt_km", help="altitude (km) default: 0.", type=float, default=0.0)`
and grids the whole globe; both tests evaluate at `alt_km=0`. So the documented and exercised regime
is the Earth's surface and the altitudes above it.

**The altitude envelope the bundled C states.** `GeomagnetismLibrary.c:1021` warns only below a floor,
with the fragment ` Elevations above -10.0 km are recommended for accurate results. ` inside its
`printf` — a lower bound with no upper bound given. The file-processing program is the only place a
ceiling is written down, at `src/wmm2020/src/wmm_file.c:512–513` as
`        minalt = -10; /* To be defined */` and `        maxalt = 1000;` in kilometres. The model's
working envelope is therefore roughly 10 km below the ellipsoid to 1000 km above it.

**What the bundled C says the model does and does not include — the decisive evidence.** NOAA's help
text in `src/wmm2020/src/wmm_point.c` is a multi-line `printf` block; each string is a separate source
line and they are quoted individually rather than spliced. Line 133:
`            printf("\n is a model of Earth's main magnetic field. The WMM");`. Then lines 159–162
state that a degree and order 12 model
`            printf("\n such as WMM, describes only the long wavelength spatial Magnetic ");`,
`            printf("\n fluctuations due to Earth's core. Not included in the WMM series");`,
`            printf("\n models are intermediate and short wavelength spatial fluctuations ");`,
`            printf("\n that originate in Earth's mantle and crust. Consequently, isolated");`.
Lines 165–167 continue:
`            printf("\n trenches) of several degrees may be expected. Also not included in");`,
`            printf("\n the model are temporal fluctuations of magnetospheric and ionospheric");`,
`            printf("\n origin. On the days during and immediately following magnetic storms,");`.

Unlike the sibling package's tree, this repository carries **no** Enhanced Magnetic Model help block
alongside the WMM one — a word-bounded search of the whole tracked tree at the pin for
`is a model of Earth's main` returns exactly one line, `wmm_point.c:133` above. There is therefore no
near-identical sibling sentence here to mistake for the WMM statement.

**Earth Atmosphere — kept, and why it is the right row rather than a finer one.** The region a user
cares about is where the software's outputs apply: the near-Earth volume from the surface upward that
the API accepts and the model's envelope covers. `Earth Atmosphere` is the row that spans that
volume. The `Region` vocabulary has 24 rows and is **flat** — every row is top-level, no row implies
any other — so each value below is judged on its own merits and no "X encompasses Y" argument is
available or used.

**Which new values now apply — asked, and answered no.** The question is not merely whether the
stored value is still valid but whether the vocabulary offers anything better or additional.

- `Earth Lower and Middle Atmosphere` — correct for the worked example and both tests, all at the
  surface, but it silently discards the model's stated reach to 1000 km. Choosing it would understate
  the envelope.
- `Earth Ionosphere` and `Earth Thermosphere` — these altitudes lie inside the model's envelope, but
  the software computes no ionospheric or thermospheric quantity, performs no magnetic-coordinate
  transform, and the vendored text at `wmm_point.c:166` explicitly disclaims ionospheric field
  contributions. Selecting either would put this record in front of a searcher looking for ITM tools,
  who would find a main-field model out of place. This is the same evidence on which Field 16
  removes the `ionosphere` and `upper atmosphere` keywords; the two outcomes agree.
- `Earth Magnetosphere`, `Earth Inner Magnetosphere`, `Earth Outer Magnetosphere`,
  `Earth Magnetosheath`, `Earth Magnetotail`, `Earth Auroral Subregion` — all name magnetospheric
  structures whose fields `wmm_point.c:166` says the model excludes.
- `Chromosphere`, `Corona`, `Photosphere`, `Solar Interior`, `Solar Environment`, `Solar Wind`,
  `Interplanetary Space`, `Heliosheath`, `Planetary Magnetospheres` and the five per-planet
  magnetosphere rows (Jupiter, Mars, Neptune, Saturn, Uranus) — all outside an Earth-only model's
  scope.

That accounts for all 24 rows.

**Worth recording for a future refresh: the vocabulary offers nothing for the field's source region.**
The physical region that actually *generates* what this software computes is the Earth's core —
`wmm_point.c:160` says so in as many words. There is no `Earth Core`, `Earth Interior` or
`Earth Surface` row; `Solar Interior` is the only interior row in the vocabulary and it is solar. So
there is no way to name the source region, and `Earth Atmosphere` naming the *application* region is
the best available truth rather than a compromise anyone should try to improve on without a
vocabulary change.

### 6. Authors (MANDATORY)
- **Author: Michael Hirsch**
  - **Identifier:** https://orcid.org/0000-0002-1637-6526
  - **Affiliation:** Boston University — https://ror.org/05qwgg493
  - **Affiliation:** Scivision, Inc.
- **Author: Manoj C. Nair**
  - **Identifier:** https://orcid.org/0000-0002-0541-0127
  - **Affiliation:** Not recorded — see the affiliation note below
- **Author: Adam Woods**
  - **Identifier:** Not recorded
  - **Affiliation:** Not recorded — see the affiliation note below

Authors are identified by name, not by position. The order this file lists them in is a presentation
choice and is not evidence of HSSI's stored ordering, so any later correction must be made by name
rather than by index.

#### The inclusion criterion, settled: authors of a whole component this package ships

The field is derived from **one** criterion, applied to produce every inclusion and every exclusion.
Ruling person by person produces a list nobody can defend later, so the criterion is stated here and
the list above follows from it without exception.

**The criterion.** Credit the people the sources name as authors of a *complete component that this
package ships*. Do not credit support contacts, authors of individual routines inside a component,
authors of a prior-language original a routine was adapted from, or acknowledgements.

**Applied.** Two components ship here: the Python wrapper and NOAA's Geomagnetism Library. The
wrapper's author is Michael Hirsch — `setup.cfg:4` declares `author = Michael Hirsch, Ph.D.`, and he
authored `wmm_point_sub.c`, both build definitions and every Python file. The library's authorship
line is `GeomagnetismLibrary.c:75`, ` *  Written by Manoj C Nair and Adam Woods`. That yields the
three names above.

**Aaron Nielsen, Andrey Korzh and Antoine Tavant were stored as authors and have been removed.** Each
contributed one or two commits implementing an individual feature rather than a whole component; what
each of them actually did is set out below, and the criterion excludes all three on that basis. The
removal of those three previously stored values is recorded here in full so a later refresh understands
it was deliberate and does not restore them from the commit history as an apparent omission.

**Criteria considered and rejected, with what each would have yielded.**

- *Everyone the version-control history records as a commit author of this repository.* This is the
  criterion the previously stored list embodied. It yields Hirsch, Nielsen, Korzh and Tavant, and
  excludes every NOAA author on the ground that the vendored library is a dependency this repository
  redistributes rather than authors. Rejected because it credits as full authors of the software three
  people who each added one feature, while denying credit to the two people who wrote the code
  performing every physical calculation the software exists to perform. The imbalance runs the wrong
  way.
- *The union of both — six names.* It omits nobody, which is its whole appeal. Rejected because a
  six-name list in which the person who made the Python package is one voice among six misdescribes
  the package as much as either narrower list does, and because "credit everyone who might qualify" is
  not a criterion that can be reapplied consistently at a later refresh.

**The effect on a person using the site, stated because it is real either way.** The same vendored
NOAA Geomagnetism Library is shipped by a second piece of software in this catalogue, the WMM2015
wrapper, which as observed during this refresh credits Michael Hirsch, Manoj C. Nair and Adam Woods.
Under the criterion settled here a visitor comparing the two wrappers sees the component attributed
the same way on both, and someone searching the catalogue for **Manoj Nair** finds both packages that
ship his code rather than one of them. That is a consequence of applying this criterion to this
tree's evidence, **not a reason for choosing it** — the criterion rests on what the sources here say
about components and their authors, and would stand unchanged had the sibling been settled the other
way. Inheriting a criterion from a neighbouring entry is exactly how a list becomes indefensible.

**Two practical constraints follow from crediting the NOAA authors.** First, `Person` rows for both
Manoj C. Nair and Adam Woods already existed at the time of this refresh, each with an empty
identifier and each matching byte-exactly on given and family name, so crediting them attaches
**existing** rows rather than minting new ones — the addition costs no new person records. Second, and
against that: an ORCID for either must **not** be sent in a routine metadata update. A person row
created without an identifier is found by name, whereas an update carrying an identifier is matched on
that identifier instead — so sending one matches nothing, mints a duplicate row and orphans the
original. Nair's verified ORCID was therefore **not** sent in this entry's PATCH; it was applied on
2026-09-07 by a database-side correction to the existing row, which preserves that row's identity and
every other entry referencing it. No ORCID is asserted for Woods at all, and none should be — see the
Woods note below.

**The commit-authorship evidence, exactly.** Five distinct author forms appear across all 28 commits
in the pin's ancestry, and they sum to 28, so this is the whole history rather than a sample:
`Michael Hirsch <scivision@users.noreply.github.com>` (20),
`Michael Hirsch <10931741+scivision@users.noreply.github.com>` (4),
`Aaron Nielsen <apn@apnielsen.com>` (2),
`Antoine T <antoine.tavant@lpp.polytechnique.fr>` (1) and
`Andrey Korzh <ao.korzh@gmail.com>` (1). The committer field additionally carries
`GitHub <noreply@github.com>` on four commits, which is GitHub's own service identity committing on a
user's behalf — a committer string is not a person and must not be read as a fifth contributor. There
is no `.mailmap` at the pin or anywhere in the ancestry, so these are simply the strings the commits
were authored under. **Do not fabricate a combined author string**: quote one of the five forms
exactly or paraphrase without quotation marks.

**`Michael Hirsch <10931741+scivision@users.noreply.github.com>` is genuine here, and a reader may
arrive expecting otherwise.** This exact string has been mis-transcribed in the catalogue before — it
was fabricated as a composite elsewhere, and the lesson attached to it is "a plausible-looking
numeric-prefixed no-reply author form is a warning sign". That lesson is about a different matter and
is not evidence against this value. The hazard here runs the opposite way from the usual one: a
reviewer who recognises the string may flag a correct value as a defect. So the evidence is recorded
in full.

*The structural argument.* At this pin the set of commits **authored** by
`Michael Hirsch <10931741+scivision@users.noreply.github.com>` and the set **committed** by
`GitHub <noreply@github.com>` are **the same four commits, exactly** — neither set contains a member
outside the other. That is a biconditional, not a resemblance, and it is what makes the string
genuine rather than merely plausible: GitHub sets that committer identity when it creates a commit on
a user's behalf through the web interface, and the numeric no-reply author address is the other half
of the same mechanism. GitHub writes both halves; an ordinary local commit carries neither, and it is
the exact coincidence of the two sets — not the look of the address — that identifies the mechanism.
It is re-derivable in one command:
`git log --format='%h|%s|%an <%ae>|%cn <%ce>' --committer='GitHub <noreply@github.com>' db7be2cd4a84dc55e66e3bbf1523a62f25ec8ad3`

*Corroboration, not the argument.* Those four commits are `2213067` (2020-06-10, `Initial commit`),
`ae6e1fa` (2020-07-15, `Create codeql-analysis.yml`), `3ebbbc6` (2020-07-15, `Update README.md`) and
`b41d78c` (2020-09-08, `Delete codeql-analysis.yml`) — a repository creation and three single-file
create/update/delete actions, which is the shape of work done through the web interface. This
supports the structural fact; on its own it would only be a resemblance.

*The same address occurs in a second role, and any count must state which role it means.* Besides
authoring those four commits, `10931741+scivision@users.noreply.github.com` is the **committer** on
three further commits authored by other people — `1a9ebdf` and `7744e61` (Aaron Nielsen) and
`dc44618` (Andrey Korzh) — Hirsch applying contributors' work through the same interface. So the
string occurs on **7 of the 28 commits** across both roles, while an author-only sweep
(`git log --format='%an <%ae>'`) sees **4**. Both figures are correct; stated without their roles they
look like a contradiction, and a later agent re-deriving one of them may conclude the other is wrong.

**What each minor contributor actually did.** Aaron Nielsen's two commits are corroborated
independently: the GitHub release body for `v1.1.0` credits `@anielsen001` for adding "transect
function that computes and returns arbitrary paths through the wmm" and for "error checking for input
of two 1-D arrays" — both visible in `src/wmm2020/base.py` today as `transect()` and the
`np.allclose(np.diff(...))` assertions in `wmm()`. Antoine Tavant's single commit `1408f65` is
"add wmm_point", which added the `wmm_point()` function and put it in the package's exported surface;
it is the commit `v1.1.1` points at. Andrey Korzh's single commit `dc44618` is "Prevent rebuilding on
each import". Each is a real, identifiable feature; none is a whole component.

**The NOAA credits in the vendored C, by role.** A surname count is not a count of people, and these
roles are not uniform. This enumeration comes from a case-insensitive `git grep -P` over **all
tracked files at the pin** using the alternation
`written by|adopted from|algorithm developed by|developed by|author[s]?\s*[:=]|\$Author|attn:|credit|created by|contributed by|courtesy of|modified by|maintainer|acknowledg|thanks|thank |copyright|prepared by|provided by|originally|based on|derived from|adapted|contact|revision|programmed by|coded by|implemented by|Nair|Woods|Chulliat|McLean|Shaffer|Rollins|Robins|Wieczorek|Raper|Hirsch`,
which returns 40 lines. **26 of those 40 lines name a person**, and every one of the 26 falls into
one of the four classes below or into the separate non-credit class described after them. The other
14 name nobody: they are the six NOAA public-domain licence sentences (`LICENSE.txt:1`, `:3` and `:5`,
and `GeomagnetismLibrary.c:31`, `:33` and `:35`), a `.gitignore` comment about generated files, two
bare `$Revision:` lines (`GeomagnetismHeader.h:8` and `wmm_point_sub.c:26`), four contact prompts and
warning banners that give an address rather than a name, and one algorithm note at
`GeomagnetismLibrary.c:2437` reading
`/*This algorithm does not result in the difference of F being derived from `.

Two details of that 14 are easy to get wrong and are pinned down here. **There is no MIT licence text
in this tree**: `MIT License|Permission is hereby granted` matches **zero files** at the pin, because
the MIT scaffold was removed upstream before this revision — every licence sentence among the 40 is
NOAA's public-domain notice, and a later agent should not expect a second licence to turn up.
**And the version-control keyword family is larger than the nameless subset**: `$Revision:`/`$Id:`/
`$Author` together match **five** lines, of which only the two bare `$Revision:` lines above name
nobody. The other three — `GeomagnetismHeader.h:9`, `GeomagnetismLibrary.c:10` and
`wmm_point_sub.c:27` — all embed the string `awoods` and so fall on the naming side of the split;
they are *not* credits either, and the paragraph below on RCS/Subversion keyword expansions explains
why. The 26/14 split is unaffected by both points.

- *Component authorship.* `GeomagnetismLibrary.c:75` carries ` *  Written by Manoj C Nair and Adam Woods`,
  followed at lines 76–77 by ` *  Manoj.C.Nair@noaa.Gov` and ` *  Adam.Woods@noaa.gov`. This is the
  authorship statement for the library that performs all the physics. Michael Hirsch is the wrapper's
  author: `setup.cfg:4` declares `author = Michael Hirsch, Ph.D.`, `src/wmm2020/build.py` opens with a
  docstring naming him at line 4 (`Michael Hirsch, Ph.D.`) and line 5 (`https://www.scivision.dev`),
  and he authored `wmm_point_sub.c`, both build definitions and every Python file.
- *Support and correspondence contacts.* `GeomagnetismLibrary.c:55` is ` *  Attn: Arnaud Chulliat`,
  heading the NCEI address block; `:64` is ` *  Attn: Adam Woods or Manoj Nair`, heading the "Software
  and Model Support" block. A similarly formed `Attn:` line recurs in two runtime banners, but naming a
  *different* pair: `GeomagnetismLibrary.c:1051` and `wmm_point.c:186` both print (tab-indented inside
  the `printf` string) `Attn: Manoj Nair or Arnaud Chulliat` — Chulliat in place of Woods. The two
  banners match each other, not the `:64` header line; only Nair is common to both forms. These say
  whom to write to, not who wrote the code. Arnaud Chulliat appears in
  this repository **only** in that contact role — which matters, because he is first author of the WMM
  Technical Report recorded in Field 27, and it would be easy to promote him on that basis rather than
  on anything this tree says.
- *Routine-level authorship inside a component.* `MAG_TMfwd4`, the Transverse Mercator forward
  projection, credits `       Algorithm developed by: C. Rollins   August 7, 2006` at
  `GeomagnetismLibrary.c:2715` and `       C software written by:  K. Robins` at `:2716` — note the
  **double space** after the colon on the second line, which must not be squeezed. Five further routine
  headers carry Manoj Nair's name and NOAA address at routine rather than component level, and they are
  enumerated here because this paragraph claims a full class: `:2643`
  (`Manoj Nair, June, 2009 Manoj.C.Nair@Noaa.Gov`), `:3182`
  (`  Manoj Nair, Nov, 2009 Manoj.C.Nair@Noaa.Gov`), `:3344`
  (`   Written by Manoj Nair, June, 2009 . Manoj.C.Nair@Noaa.Gov.`), `:3591`
  (`    Manoj Nair, June, 2009 Manoj.C.Nair@Noaa.Gov`) and `:3654`
  (`Manoj Nair, June, 2009 manoj.c.nair@noaa.gov`, lowercased in that one). Those five change no
  outcome — Nair is already named at component level — but a completeness claim that is not complete is
  worse than none, and a later agent counting Nair mentions should find the count accounted for. His
  address also heads four file-level comment blocks: `wmm_file.c:13`, `wmm_grid.c:21`, `wmm_point.c:23`
  and `wmm_point_sub.c:23`, plus `GeomagnetismHeader.h:104`.
- *Authors of an original in another language.* `GeomagnetismLibrary.c:3180` reads
  `  Adopted from the FORTRAN code written by Mark Wieczorek September 25, 2005.`, crediting the Fortran
  original of the high-degree Legendre routine. Adapting an algorithm from another language is a
  citation, not co-authorship of this package.

**A separate class that is not a credit at all, and must never be listed as one.**
`GeomagnetismHeader.h:9` and `wmm_point_sub.c:27` both carry ` *      Last changed by: $Author: awoods $`
(the second with different leading whitespace: ` *  Last changed by: $Author: awoods $`), and
`GeomagnetismLibrary.c:10` carries
`/* $Id: GeomagnetismLibrary.c 1521 2017-01-24 17:52:41Z awoods $`. These are **RCS/Subversion keyword
expansions** — an artifact of NOAA's own version-control history, recording who last committed to
*their* repository. They are not authorship credits, they are not evidence about who wrote anything,
and they say nothing whatever about authorship of this Python package. They resolve to Adam Woods, who
is separately and properly credited at `GeomagnetismLibrary.c:75`; the keyword adds no person and must
not be allowed to sit in a list of credits as though it were one.

**Names that appear in the sibling package's vendored C but NOT here — negative research, recorded so
nobody imports them.** A case-insensitive search of the whole tracked tree at the pin for
`McLean|Shaffer|Raper|Lockheed|julday` returns **zero matches** (control: `Nair` matches in 6 files —
`GeomagnetismHeader.h`, `GeomagnetismLibrary.c`, `wmm_file.c`, `wmm_grid.c`, `wmm_point.c` and
`wmm_point_sub.c`). Susan McLean, C. H. Shaffer and Rob Raper are credited in the WMM2015-era NOAA
library and are **absent from this one**, which ships a later upstream revision. Likewise the
`Attn:` contact here is Arnaud Chulliat where the earlier library named Susan McLean. Do not carry
those names across from the sibling record.

**Michael Hirsch — author identity and identifier, settled.** The identifier recorded is
`https://orcid.org/0000-0002-1637-6526`. That ORCID's public record is Michael Hirsch, Research
Scientist in Electrical and Computer Engineering at Boston University since 2018-08, with Boston
University M.Eng. and Ph.D. degrees, and works including *PyMap3D: 3-D coordinate conversions for
terrestrial and geospace environments* (10.21105/joss.00580) and *h5fortran* (10.21105/joss.02842)
alongside a series of auroral and ionospheric papers. `geospace-code/pymap3d`'s `CITATION.cff` pairs
that exact ORCID with the author name "SciVision". Four of this repository's 28 commits are
*authored* under GitHub's numeric-prefixed no-reply address
`10931741+scivision@users.noreply.github.com` (it is additionally the *committer* on three more — see
the commit-authorship evidence above), and account ID 10931741 is the login `scivision`, which binds
the account to this repository's authorship;
`setup.cfg:4` gives `author = Michael Hirsch, Ph.D.` A future person-identity resolution should expect
both `Michael Hirsch` author forms and treat them as one person.

*Rejected alternative — do not reintroduce it.* `https://orcid.org/0000-0001-6183-6256` was recorded
for this author in an earlier revision of this file and is **wrong**. That ORCID belongs to a
different person of the same name: a Senior Facility Scientist at the Science and Technology
Facilities Council's Central Laser Facility, with a Leipzig University Ph.D. and Dipl. Math. in
Mathematics, whose twenty-nine works are entirely single-molecule fluorescence microscopy, EGFR/HER3
receptor biophysics and EMCCD detector physics. That record contains no heliophysics, no geospace and
no software. A future refresh that encounters the value must reject it rather than restore it.

The `Scivision, Inc.` spelling is parked deliberately across the catalogue and must not be normalised
here.

**Antoine Tavant — name completed, identifier deliberately absent.** An earlier revision of this file
gave the family name as "T". The git author line is
`Antoine T <antoine.tavant@lpp.polytechnique.fr>`, whose address supplies the surname; "Antoine T" was
a truncated display name, not a username. An ORCID search returns exactly one "Antoine Tavant" record,
`https://orcid.org/0000-0003-0010-8073`, but nothing ties that record to this contributor, so no
identifier is recorded — the name is corrected and the identifier left absent rather than guessed.

**The two NOAA authors — identifiers researched, and neither asserted as a value.**

*Manoj C. Nair — identifier confirmed, and applied by database-side correction on 2026-09-07.*
`https://orcid.org/0000-0002-0541-0127` is this author: the record's employment is University of
Colorado Boulder and its works are geomagnetism throughout, including *International geomagnetic
reference field: the thirteenth generation* and CrowdMag work. Corroboration independent of the name:
the WMM2020 Technical Report recorded in Field 27 lists `Nair, Manoj` among its three authors. It was
**not** sent through the metadata API, for the reason above: sending an ORCID for an author whose stored
person row was created without an identifier matches on the identifier rather than the name, which mints
a duplicate row and orphans the existing one. It was applied instead on **2026-09-07 by a database-side
correction** to the existing row. A later refresh should expect the ORCID already present and must still
not send it in a PATCH — the mint-and-orphan hazard belongs to the update path, not to the value, and
storing the value does not retire it.

*Adam Woods — researched and deliberately not asserted.* `https://orcid.org/0000-0003-1831-5038` is a
plausible candidate: the name matches and the sole employment is University of Colorado Boulder. But
it lists **zero works**, so nothing ties it to geomagnetism or to the WMM. A same-name-plus-same-
institution match with no corroborating output is not sufficient to credit a named individual.
Recorded so a later agent neither re-hunts it nor adopts it uncritically.

*Affiliation for the NOAA authors — resolvable, but deliberately not asserted here.* The vendored C
names the institution directly in the same header block as the authorship line:
`GeomagnetismLibrary.c:52–54` read ` *  National Centers for Environmental Information`,
` *  NOAA E/NE42, 325 Broadway` and ` *  Boulder, CO 80305 USA`. That institution **is**
ROR-resolvable: a v2 query for the exact string `"National Centers for Environmental Information"`
returns exactly one organization, `https://ror.org/04r0wrp59`, whose `ror_display` is
`NOAA National Centers for Environmental Information` and whose alias list contains
`National Centers for Environmental Information` — the exact string the vendored C prints. This is
worth flagging because the sibling WMM2015 record hit a wall here: its older upstream library names
the *National Geophysical Data Center*, for which a ROR v2 query returns **zero** results and which is
not among NCEI's aliases, so no affiliation could be recorded there at all. That blocker does not
exist in this tree.

Even so, no affiliation is asserted for Nair or Woods **in this refresh**, and the reason is specific
rather than cautionary boilerplate: there is no existing organization for them to attach to, so
asserting one would create a new shared organization row. No organization in the catalogue carried that
ROR at this refresh, none carried either the `ror_display` form or the alias the vendored C prints, and
no NCEI-like organization existed under any other spelling. That negative is a real one rather than a
failed lookup: Boston University's ROR, recorded as Michael Hirsch's affiliation above, resolves to
exactly one existing organization, so an existing row does match when there is one to match. A name
match therefore cannot supply these two authors an affiliation; there is nothing to match.

Creating that row remains available — it is a deliberate, escalated act rather than something that
falls out of a metadata update — and its name would not be in doubt, since a new ROR-keyed organization
takes the `ror_display` form quoted above verbatim. What makes it worth deferring is permanence: an
organization's name cannot be corrected through any API path once the row exists, whereas an
affiliation can be added to these authors on any later day. The argument is recoverability rather than
availability, so the research is recorded complete — the ROR above, and the alias that confirms it is
the right organisation — and the value is left unasserted, which forecloses nothing.

*Do not propose renaming any existing person or organization row* as part of resolving this field.

### 7. Software Name (MANDATORY)
WMM2020

**Source:** The project's own capitalisation, used consistently where the project presents itself to
a reader — the README's `# WMM2020` heading, the PyHC registry entry's `name: WMM2020`, and the plot
title the software itself renders, `    fg.suptitle("WMM2020  {}".format(mag.time))` (note the two
spaces in that format string).

The distinction a previous revision of this file blurred, kept accurate here: the **distribution**
name is the lowercase `wmm2020`. `setup.cfg:2` declares `name = wmm2020`, that is the PyPI project
name, and `import wmm2020` is the import name. Lowercase is the Python packaging convention, not the
project's name. The stored value is the form a user would recognise and search for, and it is
preserved as submitted.

### 8. Description (MANDATORY)
WMM2020 is a Python wrapper providing a simple, object-oriented interface to the World Magnetic Model 2020 (WMM2020), the standard geomagnetic reference model produced by NOAA's National Centers for Environmental Information (NCEI) and the British Geological Survey (BGS). Given geographic latitude, longitude, altitude, and decimal year as inputs, the software computes the geomagnetic field elements: magnetic declination, inclination, total field intensity, and the north, east, and downward components of the magnetic field vector. The underlying WMM2020 C source code from NOAA is compiled automatically on first use via CMake. The package supports gridded computations over latitude/longitude arrays (returning xarray Datasets) as well as single-point lookups, and includes visualization of declination and inclination contour maps. WMM2020 is tested on Linux, macOS, and Windows. The model is valid for the epoch 2020.0 to 2025.0.

**Preserved as submitted.** The wording is a curator's, and it is accurate against the code; a
stylistic rewrite would discard deliberate phrasing for no gain. Each claim checks out: the six field
elements are exactly the six arrays `wmm()` populates in `src/wmm2020/base.py` (`north`, `east`,
`down`, `total`, `incl`, `decl`); the gridded path returns an `xarray.Dataset` and the single-point
path is `wmm_point()`; `plots.py` draws the two contour maps; `README.md:11` says
`Tested on Linux, Mac and Windows.`; and `WMM.COF`'s first line begins `    2020.0`, with
`wmm_point.c` stating the model is valid for five years after the base epoch. The attribution to NCEI
and BGS is the vendored C's own, at `wmm_point.c:175–176`:
`            printf("\n developed jointly by the National Centers for Environmental Information");`
and `            printf("\n (NCEI, Boulder CO, USA) and the British Geological Survey (BGS, ");`.

#### The CMake-versus-Meson divergence — durable rationale, do not "correct" this back to the README

The description says the C is compiled **via CMake**. `README.md:35` says something different:
`The first time you use WMM2020, you will see messages from the Meson build system and your C compiler.`
The description is right and the README line is stale text. A future refresh reading the README will
be tempted to reverse this; the evidence below is why it must not.

1. **Nothing in the tree invokes Meson at run time.** `src/wmm2020/build.py`'s `build()` docstring is
   `    attempt to build using CMake`; it resolves `    exe = shutil.which("cmake")` and raises
   `        raise FileNotFoundError("CMake not available")` if absent; and it locates
   `CMakeLists.txt`. The only three `meson` matches anywhere at the pin are
   `src/wmm2020/meson.build` itself, an include line in `MANIFEST.in`, and `README.md:35`.
2. **The Meson definition could not satisfy the loader even if it were invoked.** `base.py` resolves
   its shared library with `dllfn = get_libpath(BDIR, "wmm20")`, i.e. it looks for
   `libwmm20.{so,dylib,dll}`. `src/wmm2020/CMakeLists.txt:20` declares
   `add_library(wmm20 SHARED src/wmm_point_sub.c)` — the matching name. `src/wmm2020/meson.build:15`
   declares `wmm15_lib = shared_library('wmm15', 'src/wmm_point_sub.c',` — a **`wmm15`** name, a
   copy-paste leftover from the sibling project. A Meson build would produce a library the Python
   loader would never find, and `base.py` would raise `ModuleNotFoundError`.

So this is not merely "the README names a build system the code does not call"; it is "the README
names a build system whose output this package could not load". The stored description is correct.

### 9. Concise Description (OPTIONAL)
Python interface to the World Magnetic Model 2020 (WMM2020) for computing geomagnetic field declination, inclination, and intensity at any location and time.

**Preserved as submitted.** It is accurate and it is a curator's wording.

A near-alternative was considered and not taken: `setup.cfg:6` declares
`description = WMM2020 geomagnetic model with simple object-oriented Python interface`, which PyPI
publishes as the package summary. Adopting it would trade a sentence that tells a reader what the
software *computes* for one that tells them what it *is*. For a concise description standing beside a
full one, naming the outputs is the more useful of the two, and the stored wording already does that.
Recorded so a later refresh does not treat the `setup.cfg` string as an unexamined improvement.

### 10. Publication Date (RECOMMENDED)
2020-06-10

**Three independent artifacts agree, so no ambiguity arises here.** The `v1.0.0` tag points at commit
`018dae4`, whose author and committer dates are both 2020-06-10T03:57:27-04:00; the GitHub release
`v1.0.0` — named `initial release` — has `published_at` 2020-06-10T07:59:30Z; and the PyPI sdist
`wmm2020-1.0.0.tar.gz` was uploaded 2020-06-10T07:58:02Z. All three fall inside a single three-minute window.

**The definition's two readings do not conflict for this software.** The field is defined as "Date of
first broadcast/publication", with "Used for the initial version of the software". One reading points
at the day the repository became public, the other at the day the first version was released. Here
they are the same calendar day: GitHub reports `created_at` 2020-06-10T07:35:09Z for the repository,
and the first release followed twenty-four minutes later. This is worth stating because the sibling
WMM2015 record had to choose between those two readings — its repository predated its first release by
almost three months — and a later agent comparing the two records should know the divergence in method
there does not indicate a divergence in method here.

**A previously recorded contradiction, resolved.** An earlier revision of this file carried a summary
table marking this field "Not found | No clear date" while the field body gave 2020-06-10. The table
was wrong, is not part of the current dossier standard, and has been removed; the evidenced value
stands.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source and reasoning.** The field definition directs that when no DOI has been obtained, the
repository host is the correct entry. Field 2 establishes that no DOI exists, and the repository is
hosted on GitHub. Zenodo was considered and rejected: there is no GitHub-Zenodo integration on this
repository — no `.zenodo.json` at the pin or in the ancestry — and no Zenodo deposit exists. PyPI was
also considered: the package is distributed there, but PyPI is a package index rather than the
publisher of the source, and the field's own guidance names the repository host.

### 12. Version (RECOMMENDED)
- **Version Number:** 1.1.1
- **Version Date:** 2021-02-11
- **Version Description:** Not recorded — deliberately left empty; the reasoning is below
- **Version PID:** Not found

**`1.1.1` is the newest version any source publishes.** `setup.cfg:3` declares `version = 1.1.1`. The
repository's three tags are `v1.0.0`, `v1.1.0` and `v1.1.1`, all three verified to sit on the pinned
revision's own ancestry — checked with `git merge-base --is-ancestor` against the pin rather than
`git log --all`, because tags in this organization's repositories can sit on pre-rewrite orphan
lineages. As of 2026-09-06 GitHub publishes exactly those three releases and PyPI exactly three
sdists, `1.0.0`, `1.1.0` and `1.1.1`, with no extra release lacking a tag; PyPI's `home_page` for the
`wmm2020` distribution is this repository, confirming the distribution is this software rather than a
name collision.

**The `1.1.1` versus `v1.1.1` prefix.** Three sources, two spellings: `setup.cfg` says `1.1.1`, PyPI
publishes `1.1.1`, and the git tag is `v1.1.1`. The unprefixed form is what the software says about
itself and what a user installing it sees; the `v` is a git tagging convention. The stored `1.1.1` is
correct and should not be "corrected" to the tag spelling.

#### Version date — 2021-02-11 is right, and the reason matters more than the value

**A discrepancy will look real at the next refresh unless the mechanism is written down here.** The
`v1.1.1` tag points at commit `1408f65`, whose **author** date is 2020-11-17T14:35:00+0100 — nearly
three months before the recorded release date. That commit is Antoine Tavant's "add wmm_point", and
it was **replayed onto** `8b2324d` rather than merged, so its author date preserves when it was
originally written while its committer date records when it entered this history. The committer date
is 2021-02-11T03:20:56-05:00, i.e. 2021-02-11T08:20:56Z.

Three independent artifacts put the release within four minutes of each other on that day: the
committer date 08:20:56Z, the GitHub release `published_at` 2021-02-11T08:23:25Z, and the PyPI upload
of `wmm2020-1.1.1.tar.gz` at 2021-02-11T08:24:12Z.

**Do not repeat the earlier revision's explanation of this date.** It attributed the value to the
"lightweight tag creatordate". All three tags here *are* lightweight — `git cat-file -t` returns
`commit` for each, and `git for-each-ref` shows an empty `taggerdate` — but for a lightweight tag
`creatordate` simply *is* the pointed-at commit's committer date, so citing it names a symptom rather
than the mechanism. The mechanism is committer-versus-author date on a replayed commit, and stating
it that way is what stops the 2020-11-17 author date being read as a contradiction next time.

#### The version description is deliberately empty

**The release carries two candidate texts and neither is recorded.** The GitHub release API holds
**both** fields for `v1.1.1`, and they are different texts:

- release `name`: `enhance build. add single point and test`
- release `body`: `allow CMake >= 3.10\r\nbugfix: don't rebuild each import` (two lines, CRLF-separated)

Both are preserved here rather than in the field, so the decision is re-openable on the evidence
rather than needing the release API re-queried.

**Why neither was taken.** Read as a description of *this version of this software*, both texts are
developer-facing build notes: they speak about the minimum CMake version, about not rebuilding on each
import, and about "enhance build". A reader on this page wanting to know what version 1.1.1 offers
them learns almost nothing from either, and a changelog fragment in a description slot reads as
noise beside a full description that already says what the software computes. An empty description
loses the release's own words — which is a real cost, and is why they are quoted in full above — but
it does not mislead. Combining the two texts was also available and would have lost nothing of the
release's own account of itself; it was not taken for the same reason, since combining two
build-oriented lines yields a longer build-oriented line.

**The attribution evidence, which is what would have made any of them safe to use.** It is recorded
because it is the expensive part to re-derive and it bears on any future attempt to fill this field.
The relevant release range is `v1.1.0..v1.1.1`; `v1.1.0` is confirmed an ancestor of `v1.1.1`, and the
range contains exactly 8 commits: `1408f65` "add wmm_point", `8b2324d` "cmake >= 3.10, better
feedback, Numpy 1.20 types", `77b79d8` "pep517", `f261cbe` "meta", `3483f03` "cmake template",
`dc44618` "Prevent rebuilding on each import", `b41d78c` "Delete codeql-analysis.yml" and `8f5ea52`
"cleanup unused code". Every element of both candidate texts maps into that range: "add single point
and test" to `1408f65`; "allow CMake >= 3.10" and "enhance build" to `8b2324d`; "bugfix: don't rebuild
each import" to `dc44618`. **Nothing in either text is inherited from an earlier tag**, so either
choice would have been attributable — the objection to them is editorial, not evidential.

For the record, the neighbouring releases carry their own distinct texts, which is how the inheritance
test above was made real: `v1.1.0`'s name is `enhance build, add features` with a four-bullet body
crediting `@anielsen001`, and `v1.0.0`'s name is `initial release` with an empty body. None of that
text appears in the `v1.1.1` fields.

**Version PID.** None. Field 2 establishes there is no DOI for this software at all, so no
version-specific DOI can exist.

### 13. Programming Language (RECOMMENDED)
- C
- Python 3.x

**The criterion — settled first, then applied to every inclusion and exclusion.** List a language when
the repository ships source in that language that forms part of what the software delivers to a user —
either executed by the package or compiled into the artifact the package builds — **and** the
`ProgrammingLanguage` vocabulary has a row for it. Deciding language by language invites arbitrary
calls; deciding by criterion makes the result reproducible.

**The stored pair `C` and `Python 3.x` is exactly what that criterion yields.** It is consistent with
the criterion above and *not* with the broader alternative of "every language present in the tracked
tree", which would additionally demand CMake, Meson and Make — see the exclusions below.

**The tracked tree at the pin.** Seven `.py` files (`RunWMM2020.py`, `setup.py`,
`src/wmm2020/{__init__,base,build,plots}.py`, `src/wmm2020/tests/test_all.py`), five `.c` files and
two `.h` files under `src/wmm2020/src/`, and three build definitions
(`src/wmm2020/CMakeLists.txt`, `src/wmm2020/meson.build`, `src/wmm2020/src/Makefile`).

**Python 3.x — included.** The entire public interface a user imports is Python:
`src/wmm2020/__init__.py` is the single line `from .base import wmm, wmm_point`. `setup.cfg:22`
declares `python_requires = >= 3.7`. `Python 2.x` is excluded by that same declaration, and by
`base.py:1`'s `from __future__ import annotations` and the PEP 585/604 annotation
`-> dict[str, float]` on `wmm_point`, neither of which is Python 2 syntax.

**C — included.** The vendored NOAA library and the wrapper's `ctypes` entry point are C, and the
build compiles them. **Both build definitions name every source explicitly; neither uses a glob**, so
the build graph below is complete with no directory to descend into.

- **CMake** compiles `add_library(geo src/GeomagnetismLibrary.c)`,
  `add_library(wmm20 SHARED src/wmm_point_sub.c)` and `add_executable(wmm20_file src/wmm_file.c)`.
- **Meson** compiles `geo_lib = library('geo', 'src/GeomagnetismLibrary.c',`,
  `wmm15_lib = shared_library('wmm15', 'src/wmm_point_sub.c',` and
  `wmm_exe = executable('wmm', 'src/wmm_point.c',`.
- **The vendored `src/wmm2020/src/Makefile`** builds three standalone executables, `wmm_file`, `wmm_grid` and
  `wmm_point`, each against `GeomagnetismLibrary.o`. It is NOAA's own makefile and is not invoked by
  the Python package.
- **`src/wmm2020/build.py` invokes CMake, and only CMake** — see Field 8. So the path the Python
  package actually takes compiles `GeomagnetismLibrary.c` and `wmm_point_sub.c` into `libwmm20`.
- Consequently `src/wmm2020/src/wmm_grid.c` is compiled by neither CMake nor Meson, though
  `MANIFEST.in`'s `recursive-include src/wmm2020/src *.c` still ships it in the sdist, and the
  vendored `Makefile` would build it. Recorded so its presence is not read as an incomplete survey of
  the build graph.

The two `.h` files are C headers and are covered by the same value.

**CMake, Meson and Make — excluded, and this is a vocabulary limit rather than a judgement.** The
`ProgrammingLanguage` vocabulary has 19 rows and contains no CMake, Meson or Make row, so the
criterion's practical reach here is C and Python only. This is worth stating because GitHub's own
language analysis reports five languages for this repository by byte volume — C, Python, CMake, Meson
and Makefile — and an agent seeing that report will otherwise try to add the last three and find the
submission rejected on an unknown value.

**Fortran — excluded, and this is the trap worth flagging.** The vendored C credits a Fortran
*original* it was adapted from: `GeomagnetismLibrary.c:3180` reads
`  Adopted from the FORTRAN code written by Mark Wieczorek September 25, 2005.` No Fortran source is
in the tree — that routine exists here only as C. The vocabulary's five Fortran rows (`Fortran 2003`,
`Fortran 2008`, `Fortran 2023`, `Fortran77`, `Fortran90`) are all inapplicable. The vocabulary also
carries `IDL`, `MATLAB` and `Julia` rows, none of which has any presence in this tree.

### 14. Reference Publication (OPTIONAL)
Not found

#### The WMM2020 Technical Report is not this software's reference publication

**The report stays where it is, in Field 27 as a related publication, and this field stays empty.**
The placement of that document spans Fields 14, 27 and 28 and was settled as a single question rather
than three; the companion outcomes are recorded in those fields.

**Frame it by what each field renders, not by "is it a DOI?".** A contested publication has exactly
three possible placements on this software's page, and they look different to a visitor:

- **Field 27, Related Publications** — the document appears in a list of related publications. This is
  where it is, and where it stays.
- **Field 14, Reference Publication** — the page renders a *Reference Publication* citation block,
  presenting the document as the citation for this software.
- **Field 2, Persistent Identifier** — drives a "Cite Me" block headed *Software* via doi.org content
  negotiation. **This is wrong here regardless of the other two**, because the tech report is not this
  software; recording its DOI in Field 2 would tell the catalogue that a NOAA report *is* the Python
  package.

**The argument that carried it.** `https://doi.org/10.25923/ytk1-yx35` resolves to *The US/UK World
Magnetic Model for 2020-2025: Technical Report* — authors Chulliat, Arnaud; Alken, Patrick; Nair,
Manoj — publisher "National Centers for Environmental Information (U.S.); British Geological Survey",
issued 2020. It describes **the model**. It does not describe, mention or cite this Python wrapper,
which did not exist when it was written. Field 14 asks for "the publication describing the software",
typically a software paper such as a JOSS submission, and no such paper exists for this package: the
README's `## Reference` section links two NOAA WMM2020 chart PDFs (an inclination map and a
declination map), not a publication about the code. Promoting the report here would render a citation
block telling a visitor to cite a NOAA report when citing this software, which is a
misattribution the page would state in its most prominent form.

**The argument on the other side, recorded because it is not weak.** The report is the specification
of exactly what this software computes, and the vendored C repeatedly directs the user to it —
`wmm_point.c:155–156` tell the reader that for more information they should see the WMM Technical
Report. A reader who wants to use this software correctly needs that document. What that establishes
is that the document belongs *on the page*, which Field 27 accomplishes; it does not establish that
the document is the software's reference publication. "Needed in order to use the software" and "the
publication describing the software" are different relations, and only the second is this field.

### 15. License (RECOMMENDED)
Other

**`Other` is the only truthful value the vocabulary permits, and this note exists so that is not read
as an unexplained fallback.**

**What the repository actually states.** `LICENSE.txt` at the pin is NOAA's World Magnetic Model
notice, not a software licence. Line 1 is
`The World Magnetic Model - License and copyright information`; the operative sentences are line 3,
`The WMM source code is in the public domain and not licensed or under copyright.`, and line 4,
`The information and software may be used freely by the public.` Line 5 records the 17 U.S.C. 403
notice obligation for third parties producing copyrighted works predominantly from U.S. Government
material, and line 7 cites ` https://www.ngdc.noaa.gov/geomag/WMM/license.shtml` as its source.
`setup.cfg` points `license_files` at that file and declares no licence name; PyPI's `license` field
for the distribution is the empty string; GitHub's licence detection returns `NOASSERTION` with a
`null` URL.

**Scope of the notice.** It covers **the NOAA model code**. Nothing anywhere in the tree states a
licence for the Python wrapper. `GeomagnetismLibrary.c:31–35` simply repeats the same NOAA notice in
its `LICENSES` block. Neither `pyproject.toml` nor the README says anything about licensing. A user's
rights over the wrapper are therefore undefined by the repository — a real and durable property of
this software, not a gap in the extraction.

**Licence history, established by file content and not by a path filter.** Two commits touch a licence
file, both on 2020-06-10, and the content check gives a clearer answer than the path history does.

- `2213067` (2020-06-10T03:35:10-04:00, "Initial commit") is GitHub's repository-creation scaffold. Its
  entire tree is three files: `.gitignore`, `LICENSE` and `README.md`. That `LICENSE`, blob
  `d5fc9f4a3a88b3416edf6277cb106410330abefb`, is GitHub's **MIT License** template with
  `Copyright (c) 2020 Space Physics`.
- `883676f` (2020-06-10T03:54:57-04:00, "initial commit"), nineteen minutes later, is the commit that
  first populated the repository with actual code. It deletes `LICENSE` and adds `LICENSE.txt` carrying
  the NOAA notice, blob `41fa030dd8600e90ac7eff1dfc2e0c21d64e065f` — the blob still present at the pin.

No commit has touched either path since. **This corrects a claim worth being precise about:** the two
files do *not* carry the same text, so this is not a rename with continuous content. But neither is it
a relicensing of released software — the MIT template existed for nineteen minutes, alongside no code
at all, and was gone before the first line of the package was committed. A future agent that diffs the
paths will see MIT→NOAA and should read it as the scaffold being replaced, not as a licence change.

**Why no other row fits.** The `License` vocabulary has 11 rows: `Apache License 2.0`,
`BSD 2-Clause "Simplified" License`, `BSD 3-Clause "New" or "Revised" License`,
`Creative Commons Attribution 4.0 International`, `GNU General Public Licenses (GPL version 2)`,
`GNU General Public License v3.0 or later`, `GNU Lesser General Public License v3.0 only`,
`GNU Library or ‘Lesser’ General Public Licenses (LGPL version 2)`, `MIT License`, `Other` and
`Restricted`. **There is no public-domain row and no U.S.-Government-work row.** `MIT License` would
be actively wrong — that template was deleted before any code existed and describes nothing that
ships. `Restricted` would also be wrong: the notice says the software may be used freely by the
public. So `Other` is not a default; it is the only row that does not misstate the position, and this
note is the record of what `Other` means for this software.

**There is no per-software License URI, and an earlier revision's was unwritable.** An earlier revision
of this file carried a `License URI:` sub-value of
`https://www.ngdc.noaa.gov/geomag/WMM/license.shtml`. HSSI has no per-software licence URI: a
software's licence is a foreign key to a **shared** licence row that carries its own URL, so a
software-specific URI cannot be stored at all, and the shared `Other` row's own URL is empty. That NOAA
URL is cited above as **evidence** for what the notice says, and must not be reintroduced as a storable
value.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- build-on-run
- declination
- geomagnetic
- geophysics
- inclination
- magnetism
- main field
- secular variation
- space physics
- space weather
- spherical harmonics
- World Magnetic Model

Keywords are the one **open** vocabulary in this record, so the stored spellings above are what
matter; the site renders them title-cased ("Declination", "Space Physics"), and that rendering must
never be mistaken for the stored value. Every term above already existed as a `Keyword` row at this
refresh, so none of them mints a near-duplicate.

**Carried forward unchanged from the existing record:** `declination`, `geomagnetic`, `geophysics`,
`inclination`, `magnetism`, `space physics`, `space weather` and `World Magnetic Model`. `geomagnetic`
is `setup.cfg`'s sole declared keyword (lines 7–8, `keywords =` / `  geomagnetic`) and one of the
repository's two GitHub topics.

**Added in this refresh, each with in-repository evidence:**

- **`build-on-run`** — the repository's other GitHub topic (`topics: ["build-on-run", "geomagnetic"]`)
  and the project's own name for its defining architectural choice: `README.md:34` reads
  `This Python wrapper of WMM2020 uses our build-on-run technique.` It is the single most
  distinguishing practical fact about installing this package.
- **`main field`** — the precise term the vendored C uses for what the model represents
  (`wmm_point.c:133`). This is the keyword that most efficiently separates this software from
  external-field and magnetospheric-field models, which is the confusion most likely to send a
  searcher here by mistake.
- **`secular variation`** — the mechanism that makes the model valid across its five-year epoch.
  `WMM.COF` ships secular-variation coefficients, declared at `GeomagnetismHeader.h:129` as
  `    double *Secular_Var_Coeff_G; /* CD - Gauss coefficients of secular geomagnetic model (nT/yr) */`.
- **`spherical harmonics`** — the model's method. `GeomagnetismLibrary.c:15` states
  ` * It however is built to be used for spherical harmonic models of the Earth's magnetic field`, and
  `wmm_point.c:158` describes WMM as a degree and order 12 model.

**Considered and not added.** `geomagnetism` — a near-duplicate of the stored `geomagnetic`, though it
does exist as a row. `magnetic field` and `geomagnetic field` — likewise near-duplicates of the stored
`geomagnetic` and `magnetism`. `core field` — accurate to `wmm_point.c:160`, but `main field` is the
term the source itself uses and the one a geomagnetism user searches. `WGS84` — the model is referenced
to the WGS-84 ellipsoid per `wmm_point.c:150`, but that is a reference-frame detail a user is unlikely
to search on. `navigation` — the vendored C discusses compass readings and grid variation, but the
repository never uses the word, and adding it would assert an application the software does not claim.
`noaa` — true and evidenced, but an institution tag rather than a subject term. `empirical model` —
already carried by Field 4's `Models and Simulations: Empirical`. `WMM` — the expanded form is already
stored and the software's own name carries the token.

#### `ionosphere` and `upper atmosphere` removed; the two PyHC facet tags not added

Two questions were settled here, together with each other and with Field 5, because the same evidence
bears on all three and an inconsistent answer would have been incoherent.

**`ionosphere` and `upper atmosphere` were stored and have been removed.** Both were ordinary subject
keywords rather than propagated facet labels, so neither came off for being a tag; each was judged on
the model's own scope statement. `wmm_point.c:166` states that temporal fluctuations of magnetospheric
and **ionospheric** origin are not included in the model. The software computes no ionospheric,
thermospheric or mesospheric quantity, reads no ionospheric data, and performs no magnetic-coordinate
transform. A user searching HSSI for ionospheric or upper-atmosphere software wants models of that
region's physics and would find a core-field model out of place.

*The case for keeping them, which is why this needed deciding rather than assuming.* The model's
stated envelope reaches 1000 km (`wmm_file.c:513`), which spans upper-atmosphere altitudes, and the
main-field vector is a routine *input* to ITM work — magnetic coordinates, conductivity tensors,
field-aligned geometry — so an ITM researcher might genuinely be glad to find this package. What
defeats it is that such a searcher is already served: they would more naturally arrive through
`geomagnetic`, `magnetism` or the newly added `main field`, all of which are stored. The two keywords
bought no reachability that the record does not already have, at the cost of advertising a regime the
model explicitly disclaims.

**The two PyHC facet tags were not added.** The PyHC registry entry
(`_data/projects_unevaluated.yml` lines 154–158) carries
`keywords: ["ionosphere_thermosphere_mesosphere","specific"]`, and neither is recorded as a keyword
for this software. Both rows already existed in the vocabulary, so adding them was available and was
declined on what they are.
`specific` is not a subject keyword at all: PyHC's `_data/taxonomy.yml` defines a facet
`category: "Span"` with `description: "The user scope of a project"` and
`keywords: ["general", "specific"]`, so the value means "this project's user scope is narrow" — a
statement about the registry's classification scheme, not about geomagnetism. Rendered on an HSSI page
as "Specific" it is uninterpretable, and a user clicking it gets an arbitrary cross-section of the
catalogue. `ionosphere_thermosphere_mesosphere` is a PyHC "Science Area" facet tag that propagates
across many registry entries; the same scope evidence above applies to it, and it is the tag that an
earlier revision of this file wrongly cited as *confirming* the Field 5 value.

**The three outcomes agree, which was the requirement.** Field 5 declines `Earth Ionosphere` and
`Earth Thermosphere` on `wmm_point.c:166`; this field removes `ionosphere` and `upper atmosphere` on
the same evidence; and no ITM facet tag is added from the registry. It would have been incoherent to
deny the region while adding an ITM keyword on the strength of a registry tag, or to keep the keyword
while rejecting the region for the opposite reason.

### 17. Data Sources (OPTIONAL)
Not found — and correctly so.

**The software reads no remote data source, and this is evidenced rather than assumed.** Its
coefficients ship inside the repository as `src/wmm2020/WMM.COF` (93 lines, first line
`    2020.0            WMM-2020        12/10/2019`), and the Python API takes numbers as arguments
rather than fetching anything.

**The searches, with their patterns and scope.** A case-insensitive `git grep -P` over the seven
tracked `.py` files at the pin for `urllib|requests|http|ftp|socket|urlopen|download` matches exactly
**one line**, and it is not network code: `src/wmm2020/build.py:5` is the author's website
`https://www.scivision.dev` inside the module docstring. The control for that sweep is
`numpy|xarray`, which matches 4 of the 7 files. **The `http` alternative above is deliberately
unanchored, and must stay that way.** A word-bounded `\bhttp\b` does **not** match `https`, and over
these seven files it returns **zero** — a clean-looking negative that is an artifact of the anchor
rather than a fact about the code. `\bhttps?\b` over the same scope returns the one docstring line.
Any later re-derivation should use `https?` or leave the alternative unanchored; a bare `\bhttp\b`
sweep will silently miss every `https` URL in a tree. Over the **whole** tracked tree, the word-bounded
alternation `\b(urllib|requests|socket|urlopen|download)\b` matches exactly **one line**, also not
network code: `GeomagnetismLibrary.c:428` is
`            printf("Please download this file from http://www.ngdc.noaa.gov/geomag/WMM/DoDWMM.shtml.  \n");`
— a message telling a *human* where to obtain a coefficient file if it is missing, in a program that
never fetches one. Stated in the terms the searches actually support: **the package performs no
runtime data retrieval.** URLs do occur throughout the tree — in `README.md`, `setup.cfg`, the
`CMakeLists.txt`, the NOAA C headers and banners — but the two the retrieval sweeps surfaced are a
module docstring pointing at the author's website and a `printf` telling a user where to download
coefficients by hand. A URL in a comment, a docstring or a printed message is text, not network code;
no client, socket, archive query or download path runs in this software.

The one file the software can read at a user's direction is a local ASCII coordinate list consumed by
the `wmm20_file` program; the repository ships an example at `src/wmm2020/test_input.asc`, whose entire
content is the single line `2020.5 E F30000 70.3 30.8`.

**Enumerating the vocabulary is the reason this field is correctly empty, not merely the record that it
was checked.** The `DataInput` vocabulary's 17 rows are `AMDA`, `CDAWeb`, `das2`,
`FTP/FTPS Directories`, `GFZ`, `HAPI`, `HTTP/HTTPS Directories`, `Madrigal`,
`Observatory/Mission-specific`, `OMNIWeb`, `Other`, `S3/Cloud-aware`, `SSCWeb`, `TAP`,
`The Virtual Solar Observatory.`, `VirES` and `WDC`. Every one names an archive, service or transport
this software does not use. `Other` was considered for the local-file case and rejected: there is no
local-file row, and selecting `Other` would tell a searcher nothing while implying an external
data-access capability the software does not have. `Observatory/Mission-specific` is likewise excluded,
consistently with Fields 31 and 32.

### 18. Input File Formats (RECOMMENDED)
- ascii

The primary Python API takes numeric arguments programmatically and reads no user file. Two ASCII
inputs exist nonetheless: the bundled coefficient table `src/wmm2020/WMM.COF`, which the C reads on
every call, and the coordinate list consumed by the `wmm20_file` program, of which the repository
ships an example at `src/wmm2020/test_input.asc`. Both are plain text.

No other row in the 11-row `FileFormat` vocabulary applies: `CDF`, `csv`, `FITS`, `HDF5`, `IDL.sav`,
`ISTP-Compliant`, `JSON`, `netCDF3/4`, `Zarr` and `Other` all name formats the software neither reads
nor recognises. `csv` in particular would be wrong — `WMM.COF` is fixed-width space-aligned columns
and `test_input.asc` is space-separated tokens, neither of them delimited fields.

### 19. Output File Formats (RECOMMENDED)
- ascii

**HSSI held no value for this field before this refresh.** It is filled here from the build's own test
rather than from inference, and the limits on the capability are recorded beside it, because those
limits are what a reader needs in order to judge the value rather than over-read it.

The Python API returns in-memory objects and writes no file — `wmm()` returns an `xarray.Dataset`,
`transect()` and `wmm_point()` return plain `dict`s. An in-memory object is not a file format, and
recording one here would misdescribe the API.

But this package does ship a program that writes a data file, and the CMake build **runs it**.
`src/wmm2020/CMakeLists.txt:24` declares `add_executable(wmm20_file src/wmm_file.c)`, and lines 27–30
register it as a test:

```
add_test(NAME WMM20file
COMMAND $<TARGET_FILE:wmm20_file> f ${CMAKE_CURRENT_SOURCE_DIR}/test_input.asc  ${CMAKE_CURRENT_BINARY_DIR}/test_output.asc
WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)
```

(Note the genuine double space before `${CMAKE_CURRENT_BINARY_DIR}` — do not squeeze it when quoting.)
That reads an ASCII coordinate list and writes an ASCII results file, and it is the only data file this
software writes. The same rejection of the remaining ten `FileFormat` rows applies as in Field 18.

**The capability reaches every install and is nevertheless unexposed — both halves are true.** On the
reaching side: `src/wmm2020/build.py` invokes `cmake --build` over the whole build directory with no
target restriction, so `wmm20_file` is compiled on every install alongside the shared library the
Python layer loads, and its example input ships in the source distribution as
`src/wmm2020/test_input.asc`. On the unexposed side: `CMakeLists.txt` declares **no `install()` rule**
for it — nor does `meson.build` — neither `setup.cfg` nor `pyproject.toml` nor `setup.py` declares any
`console_scripts` or `entry_points`, and **no Python source references it**. A case-insensitive search
of the whole tracked tree at the pin for `wmm20_file|wmm_file` matches only `CMakeLists.txt` (four
lines), NOAA's vendored `src/Makefile` and `wmm_file.c` itself. A user therefore reaches this program
only by locating the compiled binary inside the installed package's build directory. So `ascii` is
correct — this software does write an ASCII data file — while describing a capability that is absent
from the documented API rather than one the package offers a user.

**Its one registered use is platform-limited.** `CMakeLists.txt:31–32` disable the test on macOS with
`set_tests_properties(WMM20file PROPERTIES` / `DISABLED $<BOOL:${APPLE}>`, and line 34 explains why —
`# wmm_file.c has bug from original authors on MacOS`. Strictly, what is platform-limited is the
automated verification rather than the output capability. But the practical consequence is worth
stating plainly: on macOS the single place in this project where the file-writing path is exercised
does not run, so nothing in the tree demonstrates the capability there.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Directly evidenced three ways.** `README.md:11` states `Tested on Linux, Mac and Windows.` —
verified including the trailing period, and note the immediately following line 12,
`Most C compilers work.`, which is about compilers rather than platforms and must not be conflated
with it. `.github/workflows/ci.yml` defines three jobs whose runners are `    runs-on: ubuntu-latest`
(line 17), `    runs-on: macos-latest` (line 33) and `    runs-on: windows-latest` (line 46), each
running `pytest` on `        python-version: '3.7'`.

More decisively, `src/wmm2020/build.py` enumerates the supported platforms in code: `get_libpath`
branches on `    if sys.platform in ("win32", "cygwin"):`, `    elif sys.platform == "linux":` and
`    elif sys.platform == "darwin":`, and for anything else raises
`        raise ValueError(f"Unsupported platform: {sys.platform}")`.

**`Operating System Independent` — considered and rejected as false.** `setup.cfg:13` declares the
classifier `  Operating System :: OS Independent`, which is tempting and which an automated extractor
will surface. The explicit `ValueError` above contradicts it: the package refuses to run on any
platform outside those three. The classifier overstates what the code does.

`Solaris` was considered and rejected. `GeomagnetismLibrary.c:47` names `Sun Solaris with GCC Compiler`
among the environments NOAA tested *their* subroutine library in, but that is upstream's testing of
upstream's code; this Python package would hit the `ValueError` there. `MobilePlatform` and `Other`
have no supporting evidence. Note that `cygwin` is handled in the code but has no vocabulary row of its
own; it is covered in practice by `Windows`.

A separate and important constraint that is **not** an operating-system value: `README.md:13–14` state
`At this time Visual Studio is not supported since MSVC doesn't export function symbols without additional headers,`
/ `which is typically done with something like SWIG.` That restricts the *compiler*, not the platform —
the package works on Windows through MinGW, which `build.py` selects by default when
`CMAKE_GENERATOR` is unset.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Changed from the previously stored `x86-64`, because that value asserts a limit this software does
not have.**

*Why `x86-64` was recorded, and why the reasoning does not hold.* An earlier revision of this file
justified it as "CI runs on GitHub Actions standard runners which are x86-64". That is a claim about a
third party's infrastructure at a past moment, not about this repository. `.github/workflows/ci.yml`
names **no** architecture at all — only `ubuntu-latest`, `macos-latest` and `windows-latest`, whose
underlying hardware GitHub changes at will and has changed since — as of 2026-09-06 the `macos-latest`
fleet has moved to ARM. A CI runner's architecture is a property of the CI configuration, not a limit
on the software, and resting a stored value on it means the value silently becomes wrong when someone
else re-provisions their fleet.

*The durable evidence for `CPU Independent`.* The package compiles portable C from source on the host
at first use, and contains no architecture-specific code. A case-insensitive `git grep -P` over
`src/wmm2020/src/` at the pin for
`__x86|__SSE|__AVX|asm volatile|_mm_|__aarch64|intrinsic|-march|-mtune|x86|amd64|arm64` returns
**zero files**, and the same alternation extended with `architecture` over the **whole** tracked tree
also returns zero files. The control for that sweep is `sqrt`, which matches 28 lines in
`GeomagnetismLibrary.c` — so the negative is a real absence and not a broken pattern. Neither
`CMakeLists.txt` nor `meson.build` nor the vendored `Makefile` declares an architecture constraint; the
`Makefile`'s flags are `CFLAGS = -g -O2 -Wall -W`, none of them architectural. Nothing in the packaging
metadata or the documentation pins an architecture either, and as of 2026-09-06 every PyPI release is an
sdist — not one wheel — so nothing is even distributed per-architecture.

**The remaining `CpuArchitecture` rows, considered and rejected.** `x86-64`, `Apple Silicon arm64`,
`Linux aarch64 or arm64`, `ppc64le` and `Sun (SPARC)` would each *narrow* a package that is not narrow.
`GPU` and `HPC or HEC` describe capabilities this single-threaded scalar code does not have — the
`--parallel` flag in `build.py` parallelises compilation, not computation. `Other` would be less
informative than the correct row.

### 22. Related Phenomena (OPTIONAL)
Not found — and the vocabulary is the reason.

**The previously recorded rationale for this emptiness was factually wrong about the vocabulary and has
been replaced.** An earlier revision of this file justified the empty value by listing "Coronal Heating,
Coronal Holes, CMEs, Solar Corona, Solar Flares, X-ray emission". `Coronal Holes` is **not** a row —
listing it would be rejected on submission — and that list omitted two rows that do exist and that
actually bear on this software, `Geomagnetic Storms` and `Solar Wind`. The value stands; the reasoning
is re-derived below against the live vocabulary.

The `Phenomena` vocabulary has 7 rows: `Coronal Heating`, `Coronal Mass Ejections`,
`Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and `X-ray emission`. Six are solar
or heliospheric and plainly inapplicable to an Earth main-field model.

The seventh, `Geomagnetic Storms`, is the near-miss, and it is **explicitly excluded by the model
itself**. It is the only phenomenon in the vocabulary this software's own documentation mentions, and
it mentions it as a source of error. `wmm_point.c:166–169` read, line by line:
`            printf("\n the model are temporal fluctuations of magnetospheric and ionospheric");`,
`            printf("\n origin. On the days during and immediately following magnetic storms,");`,
`            printf("\n temporal fluctuations can cause substantial deviations of the Geomagnetic");`,
`            printf("\n field from model values. If the required declination accuracy is");`.
Selecting it would attach this software to precisely the phenomenon its own documentation warns it does
not represent, and a searcher looking for storm-time tools would be actively misled.

The phenomenon this software *does* support — the Earth's main geomagnetic field and its secular
variation — has no row in this closed vocabulary. Per the field's own guidance, a supported phenomenon
with no row belongs in Keywords instead, which is where `main field` and `secular variation` are
recorded in Field 16.

### 23. Development Status (RECOMMENDED)
Inactive

**HSSI held no value for this field before this refresh** — it was unset rather than wrong, so this is
a fill. `Inactive` is derived from the `RepoStatus` row definitions carried by the vocabulary itself,
quoted byte-exact from the rows, not assumed.

The `Inactive` row is defined as: "The project has reached a stable, usable state but is no longer
being actively developed; support/maintenance will be provided as time allows." Both halves hold.

*Stable and usable.* `setup.cfg:10` declares `  Development Status :: 5 - Production/Stable`, three
tagged releases exist with matching PyPI sdists, and the CI suite runs across three operating systems.

*No longer actively developed, but not closed.* The last commit is the pin itself, `db7be2c`
"simplify build", 2021-10-10; GitHub reports `pushed_at` 2021-10-11 and the last release was
2021-02-11. As of 2026-09-06 the repository is **not archived** (`archived: false`), not
disabled (`disabled: false`), and carries three open issues — so the project remains open to contact
rather than shut.

Two observations that must **not** be read as activity. GitHub's `updated_at` timestamp of 2025-06-11
is not commit activity; it moves on metadata events such as starring. And `has_wiki: true` proves
nothing here: the wiki repository does not exist — as of 2026-09-06 `git ls-remote` against
`https://github.com/space-physics/wmm2020.wiki.git` returned `Repository not found` — so there is no
wiki content, and none is available to Fields 12 or 24 either. A repository wiki lives in a separate
git repository that is unreachable from a code pin, so the flag can never substitute for checking.

**Alternatives considered and rejected.**

- `Unsupported` — "The project has reached a stable, usable state but the author(s) have ceased all
  work on it. A new maintainer may be desired." Rejected on the two clauses of that definition rather
  than on any archiving test. Note the definition says a new maintainer **may** be desired; that exact
  phrase has been misquoted elsewhere as "is desired" and used to justify this row wrongly. Neither
  clause holds here: the project is not archived, not disabled and carries open issues, and nothing in
  the repository, its packaging or its README seeks a new maintainer. `Inactive`'s weaker claim — that
  "support/maintenance will be provided as time allows" — is what the evidence supports.
- `Moved` — "The project has been moved to a new location, and the version at that location should be
  considered authoritative." Worth ruling out explicitly, because this repository's GitHub *homepage*
  field points away from itself — as of 2026-09-06 at
  `https://www.ngdc.noaa.gov/geomag/WMM/soft.shtml#downloads`. That is NOAA's own WMM software
  download page — a pointer to the upstream model's distribution, not a
  relocation of this Python package, which exists nowhere else. There is also a real successor model
  epoch (WMM2025) that this package does not implement, but a superseding *model* is not a moved
  *project*: a user who needs the 2020 model must still use this software.
- `Active`, `Concept`, `WIP`, `Suspended`, `Abandoned` — all excluded by the combination of three
  releases, a production/stable classifier, and no commit since October 2021.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/WMM2020

**Why this URL is right at all.** The documentation is the README, and there is nowhere else for it to
point. There is no `docs/` directory in the tracked tree, no ReadTheDocs configuration, no GitHub Pages
setup, and no wiki content (see Field 23). The field definition explicitly sanctions this case: "If
this is the same as the access URL, then enter that link here." The README does carry installation
instructions under `## Install`, with both the PyPI path (`python -m pip install wmm2020`) and the
editable-checkout path, plus a `## Usage` section with a worked example.

**The capitalisation matches Field 3 deliberately.** The same settled reasoning applies here — see
Field 3. Both fields render as visible links on the page, and a reader seeing a Code Repository ending
in `WMM2020` beside a Documentation link ending in `wmm2020` would have to work out whether those are
two different places. They are not. Do not lowercase this field.

### 25. Funder (OPTIONAL)
Not found

**Nothing in the repository names a funder.** A case-insensitive `git grep -P` over the entire tracked
tree at the pin for the word-initial alternation `\b(fund|funding|funder|grant|award|sponsor|NSF|NASA|contract)`
returns **zero files**. The control for that sweep is `NOAA`, which matches 9 files at the pin —
`LICENSE.txt`, `README.md`, `src/wmm2020/CMakeLists.txt`, and the six vendored C/H sources — so the
negative is a real absence rather than a failed pattern.

**Two near-misses, recorded so they are not mistaken for funding.**

- `.github/FUNDING.yml` existed in this repository's history and is **absent at the pin**. It was added
  at `883676f` (2020-06-10) with the entire content `github: [scivision]` / `ko_fi: scivision`, and
  deleted at `77b79d8` (2021-01-02, "pep517"). Those are personal donation links for the maintainer,
  not a research funding acknowledgement.
- The vendored C names the model's sponsoring and developing bodies, at `wmm_point.c:172–177`: the WMM
  is `            printf("\n and models prepared. The World Magnetic Model is a joint product of");`
  `            printf("\n the United States' National Geospatial-Intelligence Agency (NGA) and");`
  `            printf("\n the United Kingdom's Defence Geographic Centre (DGC). The WMM was");`
  `            printf("\n developed jointly by the National Centers for Environmental Information");`
  `            printf("\n (NCEI, Boulder CO, USA) and the British Geological Survey (BGS, ");`
  `            printf("\n Edinburgh, Scotland).");`. Those four bodies sponsor and develop **the WMM
  model**, not this Python wrapper, and none of them is described as funding software development.
  Recording any of them here would attribute this package's creation to institutions that had nothing to
  do with it.

### 26. Award Title (OPTIONAL)
Not found

Follows directly from Field 25: with no funder named anywhere in the repository, there is no award to
name. No grant or contract number appears anywhere in the tracked tree at the pin, under the same sweep
and control recorded in Field 25.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.25923/ytk1-yx35

**What this DOI is.** The value recorded above resolves through doi.org content negotiation to
*The US/UK World Magnetic Model for 2020-2025: Technical Report*, authors **Chulliat, Arnaud; Alken,
Patrick; Nair, Manoj**, publisher `National Centers for Environmental Information (U.S.); British
Geological Survey`, issued 2020. That DOI record's own `URL` field is exactly
`https://repository.library.noaa.gov/view/noaa/24390`, the NOAA repository landing page that this
record previously stored; the DOI and that URL are the **same document**, the DOI being the persistent
form.

**A previously recorded citation for this document was wrong.** An earlier revision of this file gave
the authors as "Chulliat, A., Brown, W., Alken, P., et al." **W. Brown is not among the three authors
the DOI record carries.** The correct author list is the three names above. A future refresh should not
restore the four-name form.

**Why the document belongs on this page at all.** The vendored C repeatedly directs its user to it:
`wmm_point.c:155–156` tell the reader that for more information they should see the WMM Technical
Report, and the same document is the specification of exactly what this software computes. A reader on
this HSSI page cannot use the software properly without it.

**The definitional caveat, recorded honestly.** Field 27 is defined as publications that "describe,
cite, or use the software". This report describes the **model**, not this Python wrapper, and does not
mention it. It is recorded here on the searcher's-side judgement that the document a user must read to
use this software correctly is more valuable on the page than a strict reading of the definition is
protective. A future agent should not remove it as merely out of scope without weighing that.

#### The DOI replaces the bare landing-page URL

**The stored value was `https://repository.library.noaa.gov/view/noaa/24390`, the NOAA repository
landing page, and it is replaced by `https://doi.org/10.25923/ytk1-yx35`.** The two address the same
document — that DOI record's own `URL` field is exactly the landing-page URL — so this is a change of
form, not of referent, and nothing was mis-served before.

*Why the DOI form.* The field's own guidance says "ideally DOIs". A DOI is a persistent identifier
with a maintained resolution guarantee; a repository landing-page path is one host's URL structure and
can be reorganised without notice. The DOI also carries the structured metadata — title, three
authors, publisher, year — that the bare path does not.

*The cost, which is real and was accepted.* HSSI renders a related item's **raw URL as the visitor's
link text**, so the page changes from a recognisable `repository.library.noaa.gov` address to an
opaque DOI string. A visitor loses the at-a-glance cue that the document is a NOAA repository item.
That was judged the lesser loss against a resolution guarantee, since the DOI resolves to the same
page the old value pointed at directly.

*Worth knowing at the next refresh.* A related item is keyed by its URL, so changing one is a
detach-and-attach rather than an edit — a removal plus an addition, which should not be read as two
separate changes.

**Rejected alternatives.** `README.md:56–57` link two NOAA WMM2020 chart PDFs — an inclination map and
a declination map. Those are chart products with no DOI and no publication record, not publications;
they are better represented by the model and dataset entries already available. Both links returned
HTTP 404 as of 2026-09-06, which is worth knowing before following them but is not why they were
rejected — the rejection rests on what they are. The 2015-2020 and 2025-2030 Technical Reports exist
and are rejected: they document model epochs this software does not implement.

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.25921/11v3-da71

**HSSI held no related dataset for this software before this refresh.** The recorded value is the
WMM2020 coefficient release: `https://doi.org/10.25921/11v3-da71` resolves through doi.org content
negotiation to *World Magnetic Model 2020*, authors **NCEI Geomagnetic Modeling Team** and **British
Geological Survey** (both organizational literals), publisher `NOAA National Centers for Environmental
Information`, issued 2019.

**Why it belongs here.** The field asks for datasets the software supports functionality for. This
software's entire function is to evaluate this coefficient set, and it **ships it inside the
repository**: `src/wmm2020/WMM.COF`, whose first line reads
`    2020.0            WMM-2020        12/10/2019` — the 2020.0 epoch, the WMM-2020 label, and a
December 2019 release date consistent with the DOI record's 2019 issue year. Recording it tells a
reader exactly which model release is inside the package, information otherwise discoverable only by
opening a coefficient file. It also gives the page a precise answer to the question a visitor most
often has about an epoch-bound model — *which* coefficients — that no other field carries.

**The argument for leaving it empty, recorded because it is not a weak one.** The dataset is not
something the software *reads from elsewhere* or helps a user analyse; it is bundled and invisible at
run time. Field 17 records that this software retrieves nothing, and a reader might reasonably expect
a "related dataset" to be something they could go and get and then point this tool at. Under that
reading the coefficient table is an implementation detail rather than a related dataset. What decides
it the other way is the searcher's side: the identity of the shipped coefficient set is a fact a user
of an epoch-bound model wants, and bundling it makes that fact harder to find, not less relevant.

**Consistency with Fields 14 and 27.** All three concern how much of the NOAA model's own bibliography
this wrapper's page should carry, and they were settled together. The report is a *related
publication* and not the reference publication; the coefficient release is a *related dataset*; and
neither becomes the software's own persistent identifier. The page therefore points at the model's
specification and its coefficients without ever claiming that either one is this Python package.

### 29. Related Software (OPTIONAL)
- https://github.com/space-physics/igrf
- https://github.com/space-physics/WMM2015

Both are entries in this catalogue, and each URL is that entry's **exact stored repository URL**:
`https://github.com/space-physics/igrf` is the repository URL stored for the HSSI entry **IGRF-13**,
and `https://github.com/space-physics/WMM2015` is WMM2015's. That exactness is what the convention
requires, because the page renders a related item's raw URL as the visitor's own link text; a URL that
does not match the target entry's own would display as a reference to a different project.

**Both incumbents are judged on the merits below rather than kept by default.** Note the asymmetry that
has to be resolved with a single bar: WMM2015 is named in this repository's own README, whereas
**nothing in this tree mentions igrf at all** — the only GitHub URLs pointing anywhere other than this
repository, across the whole 28-commit history, are `space-physics/wmm2015` (6 occurrences) and
`David-OConnor/pyflow` (28). So
in-repository mention cannot be the bar, or IGRF-13 fails it; and mere shared authorship cannot be the
bar either, or a dozen unrelated packages pass it.

**The bar applied:** a package belongs here if a user who has landed on WMM2020 and is deciding what to
use would be materially better off knowing about it — because it implements the *same or the
neighbouring model* of the Earth's main field. Both incumbents clear that bar, and the rejections below
fail it.

**WMM2015 — kept.** It is the same author's previous-epoch package, built the same way, wrapping the
same NOAA library for the 2015.0 epoch. `README.md:10` names it directly:
`[WMM2015](https://github.com/space-physics/wmm2015) is also available.` It is precisely what a user
who needs a date before 2020 must switch to, and this software cannot serve them. As of this refresh the relation is
reciprocal in both directions — the WMM2015 catalogue entry lists this repository's exact stored URL in
its own related-software field.

*A note on the URL spelling.* The README's link is lowercase; the value recorded here is the
capitalised form, because that is WMM2015's exact stored repository URL and the relation resolves on
the exact string. See Field 3 for the settled reasoning on case.

**IGRF-13 — kept.** `https://github.com/space-physics/igrf` is the catalogue's entry for
"International Geomagnetic Reference Field: IGRF13 in object-oriented Python or Matlab". It is this
software's closest peer: the *other* internationally standard model of the Earth's **main** magnetic
field, wrapped by the same author with the same build-on-run architecture and the same object-oriented
Python interface. That is exactly the field's stated case of software that "performs similar tasks but
does not necessarily link together". WMM and IGRF are the two models a geomagnetic-field user chooses
between, and a user on this page who wonders what the alternatives are is best served by that pointer.
The absence of any in-repository mention does not weaken it — the relation is between what the two
packages *do*, not between their READMEs.

**Candidates considered and rejected, so this is not re-litigated.** A by-concept slice of the
catalogue on geomagnetic and magnetic-field terms surfaced these:

- **IGRF-14** — its catalogue entry's stored repository URL is
  `https://www.ncei.noaa.gov/products/international-geomagnetic-reference-field`, an NCEI *model
  product page* rather than a peer software implementation. The software peer for the IGRF model is
  already covered by IGRF-13, and adding a long product URL that renders as its own link text would add
  noise rather than information.
- **igrfpy** (`https://github.com/lkilcommons/igrfpy`) — rejected on the same bar that admits IGRF-13,
  so that the test excluding one is the test admitting the other. IGRF-13 is admitted because four
  things hold at once: it implements the other internationally standard main-field model, it is by this
  package's own author, it uses the same build-on-run architecture, and it presents the same
  object-oriented Python interface. igrfpy satisfies only the first — its catalogue author is Liam
  Kilcommons, it builds Fortran extensions rather than compiling C on first import, and it wraps IGRF-11
  and 12. It is a peer of the IGRF *model*, not of this *package*.
- **pyIGRF** (`https://github.com/rilma/pyIGRF`) — same ground as igrfpy: a different author's IGRF
  wrapper with no architectural or authorial relationship to this package.
- **geopack** — Tsyganenko external-field models. These model the magnetospheric field, which is the
  component `wmm_point.c:166` says WMM explicitly excludes; a reader would be more likely to conflate
  the two than to be helped.
- **python-magnetosphere** — a mixed collection that happens to include an IGRF module; not a peer to a
  single-model wrapper.
- **AACGMv2, ApexPy, OCBpy, OMMBV** — magnetic *coordinate system* conversions. Different task, and
  Field 4 records that this software provides no user-facing coordinate transform.
- **pyglow** — an aggregator wrapping HWM, IRI and IGRF together; not a comparable single-model tool.
- **viresclient** — a client for ESA's VirES services, including VirES for Swarm. It is a data-access
  client for the satellite magnetometry that feeds main-field models, not an implementation of one.
  Field 17 records that this software retrieves no data at all, so the two share no task.
- **Packages by this software's author in other domains** — HWM-93, ACEmag, GIMAmag and Auroral
  Electrojet all sit in the same `space-physics` GitHub organization and are the same author's work,
  in neutral winds, ACE magnetometer data, GIMA magnetometer data and the auroral electrojet index
  respectively. **Shared authorship is not relatedness**, and this is the most tempting wrong inclusion
  here; it is also why the bar above is stated in terms of what the software models rather than who
  wrote it.
- **numpy** — excluded by the standing Tier A rule, which the field's own text applies to Field 29 as
  well as Field 30. Being a dependency is not relatedness. See Field 30.
- **matplotlib** — same exclusion. `plots.py` imports it and `RunWMM2020.py` calls `show()`, but
  plotting is generic infrastructure and the claim would read identically for most of the ecosystem.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/pydata/xarray

**HSSI held no value for this field before this refresh.**

**numpy — excluded by the Tier A rule, which is policy rather than a curator's preference.**
`setup.cfg:26–28` declares `install_requires =` / `  xarray` / `  numpy`, so numpy is a genuine
dependency. The form's own text lists numpy first under "Never list these (Tier A), no exceptions",
and its rationale is that being a dependency is not interoperability: depending on numpy is true of
nearly every package in this catalogue and so distinguishes nothing about this one. The same text
extends that exclusion to Field 29, so numpy does not relocate there — the correct destination is
neither field. `matplotlib` (imported by `plots.py`) and `pytest` (the test extra) are excluded on the
same rule.

**xarray — included, on the specific exchange the public API documents and the tests enforce.** xarray
is a Tier B package, which qualifies **only** when a specific exchange appears in the public API, docs,
examples or tests, and never on dependency presence alone. The exchange here is the strongest form the
guidance describes — the guidance's own qualifying example is a public API that returns
`xarray.Dataset` as its documented interchange format, and that is literally what happens:

- `src/wmm2020/base.py` declares
  `def wmm(glats: np.ndarray, glons: np.ndarray, alt_km: float, yeardec: float) -> xarray.Dataset:`,
  and the body constructs one:
  `    mag = xarray.Dataset(coords={"glat": glats[:, 0], "glon": glons[0, :]})`.
- `wmm` is exported: `src/wmm2020/__init__.py` is `from .base import wmm, wmm_point`.
- The package's own second module consumes that object across a module boundary:
  `src/wmm2020/plots.py` declares `def plotwmm(mag: xarray.Dataset):`.
- **The contract is tested, not merely annotated.** `src/wmm2020/tests/test_all.py:10` asserts
  `    assert isinstance(mag, xarray.Dataset)`.

So a user does not merely run this alongside xarray — the model results are *handed to them* as an
xarray object, and any xarray-based workflow can consume them with no conversion step. That is concrete
and specific to this software, not a claim that would read the same for an arbitrary package.

**The honest limitation, and the part of the picture that cuts the other way.** The README never
mentions xarray, so the evidence is the API signature, the annotations and the test rather than prose
documentation. And the exchange is not uniform across the public surface: the other exported entry
point, `wmm_point`, returns a plain `dict` — `def wmm_point(glat: float, glon: float, alt_km: float, yeardec: float) -> dict[str, float]:`,
with `test_all.py:23` asserting `    assert isinstance(mag, dict)` — as does `transect`, which is
defined in `base.py` but is **not** re-exported by `__init__.py`. So xarray is the interchange type of
the package's principal gridded entry point, not of everything it offers. That was judged sufficient
because `wmm()` is the function the README's usage example calls (`mag = wmm2020.wmm(glat, glon, alt_km, yeardec)`)
and the one the package's own plotting module is built around.

**Blanket justifications explicitly not relied on.** Neither "part of the standard scientific Python
ecosystem" nor PyHC membership is offered as a reason for anything in this field; the form's text rules
both out on their own, and the xarray entry stands or falls on the API and test evidence above.

### 31. Related Instruments (OPTIONAL)
Not found — the software is instrument-agnostic. **This is an inclusion judgement against a vocabulary
that does contain plausible rows, not a report that no fitting row exists.**

**Why no instrument qualifies.** The relevance gate asks whether the software is *designed to support*
a specific instrument. WMM2020 reads no instrument's data at all: it evaluates a fitted global
coefficient table, bundled in the repository, at coordinates the user supplies. There is no
instrument-specific format, parser, calibration or archive client anywhere in the tree, and Field 17
records the sweeps establishing that it retrieves nothing over any network.

**What was found and rejected, named explicitly.** The satellite magnetometry from which WMM-series
coefficients are *derived* does have rows in this vocabulary, all of them carrying
`https://spase-metadata.org/` identifiers, and each is written out in full here so a later agent
neither elides one nor re-hunts them:

- `https://spase-metadata.org/SMWG/Instrument/CHAMP/FGM` — `CHAMP Fluxgate Magnetometer` (type 1)
- `https://spase-metadata.org/SMWG/Instrument/Oersted/OESM` — `Overhauser Effect Scalar Magnetometer on the Oersted spacecraft` (type 1)

They are **not** listed, and should not be added by a later refresh: this software does not read those
missions' data, does not implement their formats, and was not built by their teams. The provenance of
the coefficients belongs to the model's documentation, which Field 27 records; it is not a
designed-to-support relationship for this wrapper. On the searcher's side, a visitor on the CHAMP FGM
page clicking "show software related to this instrument" expects tools for working with CHAMP
measurements and would be puzzled to find a global reference-field evaluator that has never touched
them.

**The in-repository search that backs the negative, with its pattern and scope.** A case-insensitive
`git grep -P` over **all tracked files at the pin** for
`\b(swarm|champ|oersted|ørsted|intermagnet|sac-c|observatory|satellite|magnetometer|geomagnetic observator)\b`
returns **zero files**. The control is `\b(magnetic|declination)\b` over the same scope, which matches
**7** files case-sensitively (`README.md`, `src/wmm2020/base.py`, `GeomagnetismHeader.h`,
`GeomagnetismLibrary.c`, `wmm_file.c`, `wmm_grid.c`, `wmm_point.c`) and **9** case-insensitively
(those seven plus `LICENSE.txt` and `src/wmm2020/plots.py`) — so the pattern and the engine work and
the negative is a real absence. The pattern, the scope and the case-sensitivity are published together
deliberately, because all three move the number. A re-derivation that produces a different figure
should check the case flag, and check that a truncated file listing has not been read as a count,
before concluding the tree has changed.

**The precise negative, which is narrower than "nothing is named here".** The facility pattern above
returns zero files, but the tree is not silent about institutions: it names the model's **producing
and sponsoring bodies** — the National Centers for Environmental Information, the British Geological
Survey, the US National Geospatial-Intelligence Agency and the UK Defence Geographic Centre — in
attribution text the C prints to its user (see Field 32 for the artifact). What the tree names nowhere
is an observatory, spacecraft, satellite or instrument **whose data this software reads**. That is the
claim the searches support, and it is the claim Fields 31 and 32 turn on; a broader "no facility is
named anywhere" would be false, and a later agent who finds NCEI or BGS in the source should not read
it as contradicting this negative.

**Vocabulary state, checked rather than assumed.** Every row in the `InstrumentObservatory` table
carried a `https://spase-metadata.org/` identifier at this refresh, across every authority prefix
present in it — SMWG, IUGONET, CNES, HamSCI, ASWS, ISWI, NASA, NSF, ESA and NOAA — so the candidate
search above was not confined to SMWG. That prefix remains a real guard rather than an assumption: a
row failing it would indicate upstream drift or a wrongly created row, and must be reported rather
than used.

**There is no World Magnetic Model row in this vocabulary, and that is correct** — a probe of the
`name`, `abbreviation` and `identifier` columns for `world magnetic` or a word-bounded `WMM` returns
zero rows. The WMM is a model, not an instrument or an observatory, so its absence here is not a gap to
be filled.

### 32. Related Observatories (OPTIONAL)
Not found — the software is observatory- and mission-agnostic.

The same reasoning, the same searches and the same vocabulary verification as Field 31 apply;
observatory-typed rows (type 2) were included in those sweeps. WMM2020 is a global model with no
mission or observatory affiliation: it is not a mission tool, it processes no observatory's data
products, and it implements no observatory-specific convention.

**Candidates found and rejected, each written out in full.**

- `https://spase-metadata.org/SMWG/Observatory/Ground/INTERMAGNET` —
  `International Real-time Magnetic Observatory Network`. Ground magnetic observatory data of exactly
  the kind that feeds main-field models. Rejected: this software neither reads INTERMAGNET data nor
  produces anything in its formats. A visitor on the INTERMAGNET page looking for related software
  wants tools for handling observatory magnetograms and would be puzzled to find a coefficient
  evaluator.
- `https://spase-metadata.org/SMWG/Observatory/CHAMP` — `CHAMP`;
  `https://spase-metadata.org/SMWG/Observatory/SAC-C` — `SAC-C Project`;
  `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM` — `Swarm : ESA mission`; and its three
  spacecraft rows `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM-A` (`Swarm Alpha`),
  `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM-B` (`Swarm Bravo`) and
  `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM-C` (`Swarm Charlie`). All are missions
  whose measurements fed the model's coefficient fit upstream. Rejected on the same ground as Field 31:
  coefficient provenance is not a designed-to-support relationship.
- `https://spase-metadata.org/SMWG/Observatory/Ground/BGS` — `British Geological Survey`. **This one
  needs its own reasoning, because unlike every other candidate above it *is* named in the tracked
  tree.** The rejection rests on the artifact, so the artifact is quoted rather than summarised.
  `British Geological Survey` occurs **exactly once** in the whole tracked tree at the pin, at
  `src/wmm2020/src/wmm_point.c:176`, and it is **inside a `printf`**:

  ```
              printf("\n (NCEI, Boulder CO, USA) and the British Geological Survey (BGS, ");
  ```

  The surrounding lines are the same printed banner, naming NCEI, the US National
  Geospatial-Intelligence Agency and the UK Defence Geographic Centre alongside it. So BGS appears here
  as a **co-developer and co-sponsor of the WMM model**, in attribution text this software *displays to
  its user* — not as an observatory whose data this software reads. The distinction is visible in the
  artifact itself, which is what makes the rejection re-checkable rather than asserted: a single
  occurrence, in a string literal, in a help banner. The SPASE row is a *ground observatory* record.
  Selecting it would tell a searcher that this package works with BGS observatory magnetograms, which
  it does not. The institutional relationship is real and is recorded where it belongs: in Field 8's
  description, in Field 25's near-miss note, and in the Field 27 and 28 DOI records, whose publishers
  and authors include BGS.

  The same treatment settles `National Centers for Environmental Information`, whose role in this tree
  is identical to BGS's. It is not rejected as a candidate row, because it has none: a probe of the
  `InstrumentObservatory` `name`, `abbreviation` and `identifier` columns for
  `ncei|environmental information|geophysical data center|ngdc` returns **zero rows of either type**
  (control: `BGS` in an identifier returns the one ground-observatory row rejected just above). It
  occurs **7 times across 4 files** in the source:
  `GeomagnetismLibrary.c` (3), `wmm_point.c` (2), `wmm_file.c` (1) and `wmm_grid.c` (1) — a postal
  address block in the C header comments, and printed contact and attribution banners. That is the
  institution that *produced* the coefficient model, recorded as such in Field 6's affiliation
  reasoning; it is not a data source this software queries (Field 17) nor a facility whose measurements
  it handles.

**Consistently with this, Field 17 records no `Observatory/Mission-specific` data source,** since there
is no observatory-specific input to declare, and Field 4 records no `Mission-related` category.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/space-physics/WMM2020/db7be2cd4a84dc55e66e3bbf1523a62f25ec8ad3/src/wmm2020/tests/incldecl.png

#### The README hero figure is recorded as the logo

**HSSI held an empty logo before this refresh.** The recorded value is the repository's only tracked
image, which the README places in hero position.

**A previously recorded claim about this field was factually wrong.** An earlier revision of this file
stated "no logo file or URL found in repository or PyHC registry". A file *is* there. Exactly one image
is tracked at the pin, and the README puts it in hero position.

**The candidate, fully verified.**

`https://raw.githubusercontent.com/space-physics/WMM2020/db7be2cd4a84dc55e66e3bbf1523a62f25ec8ad3/src/wmm2020/tests/incldecl.png`

- It is pinned to the 40-hex commit SHA with no branch name and no `blob/` segment, and it is 127
  characters, inside the 200-character field limit.
- Fetched on 2026-09-06 it returned HTTP 200 with content-type `image/png` and 123,447 bytes — genuine
  image content, not a Git-LFS pointer. `.gitattributes` at the pin declares only `text eol=lf` rules
  and contains no `filter=lfs` entry, so the LFS case does not arise.
- The fetched bytes are sha256
  `67e316314defe8ab342c42bd3b823338390c92b7e50f06d9c667763140597d6d`, **byte-identical** to the tracked
  blob `c4b7317ff5a669b662132b0fcc4699f1dc76cc54` at the pin.
- The image is 881 × 521, 8-bit RGBA PNG.
- It is the only image of any kind in the tracked tree (no other `.png`, `.jpg`, `.jpeg`, `.svg`,
  `.gif`, `.ico` or `.webp` file exists), and `README.md:16` is its **only** reference anywhere in the
  tree: `![image](./src/wmm2020/tests/incldecl.png)`. Despite living under `tests/`, no test uses it.

**What the image actually shows — it was fetched and looked at.** A two-panel matplotlib contour
figure. The super-title reads `WMM2020  2020.0`; the left panel is titled
`Magnetic Declination [degrees]` and the right `Magnetic Inclination [degrees]`; both are plotted
against `Geographic longitude (deg)` and `Geographic latitude (deg)` with viridis-coloured labelled
contours at 20-degree intervals.

**It is generated output of this package.** Every element above traces to `src/wmm2020/plots.py`:
`    fg.suptitle("WMM2020  {}".format(mag.time))` — **note the two spaces in that format string, which
is why the rendered title reads `WMM2020  2020.0`; do not squeeze it** — plus
`    ax[0].set_title("Magnetic Declination [degrees]")`,
`    ax[1].set_title("Magnetic Inclination [degrees]")`,
`    ax[0].set_ylabel("Geographic latitude (deg)")`,
`        a.set_xlabel("Geographic longitude (deg)")` and the
`range(-90, 90 + 20, 20)` contour levels. So this is an **example figure, not a designed logo,
wordmark or icon.**

**Why it was recorded rather than left empty.** The project itself presents this image as its visual
identity: it is the README's only content image — the four other image references there are status
badges — and it sits immediately below them and above `## Install`. Sample output is a common and
legitimate form of identity for a scientific model package, and on the searcher's side a thumbnail of
global declination and inclination contours conveys what this software does far better than an empty
logo slot does. The URL is verified, commit-pinned, correctly typed and comfortably within the length
limit.

**The case for leaving it empty, recorded so the decision is legible rather than re-argued.** It is
not a logo in the designed sense — no wordmark, no mark, no chosen palette; it is a figure the
plotting function happens to produce, and its own title text is generated at run time from the model
epoch. Its path is `src/wmm2020/tests/incldecl.png`, i.e. it lives in the **test directory**, which
suggests it was committed as a reference output and reused in the README rather than authored as a
brand asset. At 881 × 521 it is a wide figure, not a shape a logo slot is designed for. And the PyHC
registry entry for this software (reproduced below) carries **no** `logo:` field, so the one external
registry that could corroborate the project's own intent does not. What outweighs all of this is that
the alternative is nothing at all: an accurate picture of the software's output serves a visitor
better than a blank slot, and no competing image exists to be displaced.

**Do not reopen this.** No substitute image was sought or invented; there is no other image in the
tree. And do not re-argue the pinning on freshness grounds — a commit-pinned URL freezing the image to
one revision is the intended behaviour, not a drawback, and repointing it at a branch would break
silently on any upstream rename or move.

---

## PyHC Registry Information

WMM2020 appears in the PyHC registry's **unevaluated packages** list, `_data/projects_unevaluated.yml`
in `heliophysicsPy/heliophysicsPy.github.io` — not in the core or community lists. Pinning the specific
file matters, because the three lists carry different curation status. The entry is at lines 154–158:

```yaml
- name: WMM2020
  code: https://github.com/space-physics/WMM2020
  description: World Magnetic Model 2020 from Python
  contact: Michael Hirsch
  keywords: ["ionosphere_thermosphere_mesosphere","specific"]
```

Both keywords are facet tags drawn from `_data/taxonomy.yml` — `ionosphere_thermosphere_mesosphere`
from the "Science Area" facet and `specific` from the "Span" facet, whose description is "The user
scope of a project" and whose only two values are `general` and `specific`. **Neither** is recorded as
a keyword for this software, and Field 16 records why neither was added. The entry carries no `logo:` field, which is weighed in
Field 33. The registry's `code` URL uses the capitalised repository spelling, which is the form
Fields 3 and 24 store and one of the grounds for keeping it. The sibling WMM2015 entry sits immediately
below at lines 160–164 with the identical keyword pair.

---

## Notes

- **What this software is.** A Python wrapper around NOAA's WMM2020 reference C implementation, using a
  build-on-run technique: the C library is compiled on first import rather than shipped as a binary
  wheel. All three PyPI releases are source distributions and there are no wheels, so a working C
  compiler is a runtime prerequisite. That is unusual and worth knowing before interpreting the
  operating-system and CPU-architecture fields.
- **Model epoch.** This package implements WMM2020, whose coefficient file declares the 2020.0 epoch and
  which the vendored C states is valid for five years after that base epoch. Its predecessor for the
  2015 epoch is a separate package, WMM2015, recorded in Field 29. A later model epoch existing does not
  make this project "Moved" — see Field 23.
- **Compiler constraint.** MSVC is not supported, because it does not export function symbols without
  additional headers; MinGW is used on Windows. This is a compiler limit, not a platform or architecture
  limit — see Fields 20 and 21.
- **The README's build-system sentence is stale and the description deliberately contradicts it.** See
  Field 8. This is the single most likely thing for a future refresh to "fix" in the wrong direction.
- **A Meson definition that could not work.** `src/wmm2020/meson.build:15` names its shared library
  `wmm15`, a copy-paste leftover from the sibling project, while `base.py` loads `wmm20`. Meson is
  present in the tree, is shipped by `MANIFEST.in`, and is never invoked.
- **A file that ships but never compiles under either build definition.** `src/wmm2020/src/wmm_grid.c`
  is included in the source distribution by `MANIFEST.in`'s `recursive-include src/wmm2020/src *.c` and
  is built by NOAA's vendored `src/Makefile`, but is named by neither `CMakeLists.txt` nor
  `meson.build`. Recorded so its presence is not read as an incomplete survey of the build graph.
- **A file that ships in the manifest but does not exist.** `MANIFEST.in:1` still includes
  `src/wmm2020/setup.cmake`, a file the pin commit `db7be2c` itself deleted. Harmless, but it will look
  like a missing file to anyone auditing the manifest against the tree.
- **Repository history.** No rename is detectable anywhere in this project's history, and no former
  GitHub name is known — relevant to Field 2, where a slug-keyed search is therefore not blind in the way it would be for the sibling
  package. All three tags are lightweight and all three are ancestors of the pin.
