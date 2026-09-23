# HSSI Metadata Extraction Results

**HSSI Software ID:** 62ac1496-2c4b-4d93-95f0-7ee39deeb0ea
**Repository:** https://github.com/space-physics/WMM2015
**Source Revision:** fb4e06f5f66ac707f1799aa12ef1687904926d56
**Extraction Date:** 2026-09-05
**Validation Date:** 2026-09-07
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

WMM2015 is a **thin Python wrapper around NOAA's World Magnetic Model C reference implementation**,
which the repository vendors under `src/wmm2015/src/`. Every claim below therefore comes from one of
two distinct classes of evidence, and they must not be conflated:

- **Wrapper-authored material** — `setup.cfg`, `pyproject.toml`, `setup.py`, `README.md`,
  `MANIFEST.in`, the CMake and Meson build definitions, and the seven tracked `.py` files. This is
  Michael Hirsch's work and describes *this package*.
- **Vendored upstream material** — four of the five `.c` files, the two `.h` files and `WMM.COF`
  under `src/wmm2015/`. This is NOAA's code and documentation. It is authoritative about **the WMM
  model** (its physics, its validity limits, what it does and does not include, and who wrote it),
  and it is the best source in the repository for Fields 5, 6, 22, 27 and 28. It is *not* evidence
  about the Python package's own design, licensing intent or maintenance. The one exception is
  `src/wmm2015/src/wmm_point_sub.c`, which is Hirsch's adaptation of NOAA's `wmm_point.c` into the
  callable `wmmsub` entry point, and which therefore belongs to the first class above.

The distinction matters most for Field 15 (the vendored notice licenses NOAA's code, and the tree
states nothing about the wrapper) and Field 5 (the vendored text states plainly which physical
regions the model does *not* describe).

A second scope fact: the repository's `LICENSE.txt` is a NOAA notice rather than a software licence,
and the repository has never carried a `CITATION.cff`, `codemeta.json` or `.zenodo.json` — neither at
the pinned revision nor anywhere in its ancestry. Structured-metadata files that normally carry
authors, identifiers and licence simply do not exist here, so most fields are established from
package metadata, the vendored C, and external authorities.

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
four README badges are GitHub Actions, LGTM, PyPI supported-Python-versions, and a pepy download
counter — none is a DOI badge. Absence in the tree, however, cannot rule out a deposit made outside
the repository, so three independent, structurally different searches were run, each paired with a
positive control proving the search could see a deposit that *does* exist:

1. **Title/subject search.** Zenodo returned nothing for `title:wmm2015` or `metadata.title:"WMM2015"`.
   DataCite returned nothing for `titles.title:"wmm2015"`, `titles.title:"WMM2015"`, or the literal
   string `"space-physics/WMM2015"`. A Zenodo search for `title:"World Magnetic Model"` returned a
   single 2025 error-grid record by other authors, unrelated to this package — the control showing
   the title index is live and does surface WMM-subject material when it exists.
2. **Old-repository-name redirect test.** This repository has been renamed twice; a repo-name-keyed
   search under the current name is blind to a deposit made under a former one. Both historical names
   redirect (HTTP 301) to `https://github.com/space-physics/WMM2015`: `scivision/wmm2015` and
   `scivision/pywmm2015`. The second is corroborated inside the repository itself — a `pywmm2015/`
   package directory exists in the ancestry and not at the pin. A control request for a deliberately
   nonexistent repository under the same organization returned 404, so the 301s are real redirects
   rather than a permissive default.
3. **Creator-keyed search (name-independent).** This is the only class of search that can find a
   *manual* upload, which carries no repository name at all. Zenodo's
   `metadata.creators.person_or_org.name:"Hirsch, Michael"` returns 48 deposits; all were enumerated
   and none is WMM-related. DataCite keyed on the ORCID recorded in Field 6
   (`creators.nameIdentifiers.nameIdentifier:"https://orcid.org/0000-0002-1637-6526"`) returns 166
   records spanning 26 distinct titles; all were enumerated and none matches `wmm`, `magnetic model`
   or `geomag` by case-insensitive regex. Both result sets are their own positive controls: they are
   large, they contain this author's genuine software deposits (h5fortran, Gemini3D, PyGemini,
   nc4fortran, findssh, Fortran filesystem), and they prove the instruments see this creator's work.

**Do not re-run a repository-name-keyed check alone and conclude from it.** It is structurally
incapable of detecting the manual-deposit case, which is exactly the case that would apply here.

The sibling package WMM2020 likewise carries no persistent identifier in the catalogue, so the
absence is a property of this author's WMM packages, not an oversight specific to this record.

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/WMM2015

**Source:** The repository itself. GitHub's canonical `full_name` for the project is
`space-physics/WMM2015` with that exact capitalisation, and the stored value matches it.

Note the deliberate case difference from `setup.cfg`, whose `url = https://github.com/space-physics/wmm2015`
is all-lowercase. GitHub resolves both, but only the capitalised form is the canonical one the
platform itself reports, and it is the form the catalogue's WMM2020 entry uses when it points back at
this repository. Field 24 below turns on the same distinction.

### 4. Software Functionality (RECOMMENDED)
- Models and Simulations
- Models and Simulations: Empirical
- Data Visualization
- Data Visualization: 2D Graphics

Every value is a live `FunctionCategory` row, and each subcategory's parent is present, so the
selection is structurally complete.

**Models and Simulations: Empirical.** WMM2015 evaluates a spherical-harmonic geomagnetic model whose
Gauss coefficients are fitted to observations and shipped as a data table, `src/wmm2015/WMM.COF`. The
vendored library's own abstract describes it as built "to be used for spherical harmonic models of
the Earth's magnetic field" generally. This is precisely the class of empirical/climatological
geomagnetic reference model the category exists for; it is not derived from first principles, and it
runs no solver.

**Data Visualization: 2D Graphics.** `src/wmm2015/plots.py` defines `def plotwmm(mag: xarray.Dataset):`,
which draws two labelled contour panels — `ax[0].set_title("Magnetic Declination [degrees]")` and
`ax[1].set_title("Magnetic Inclination [degrees]")` — over a geographic longitude/latitude grid.
Contour plots on a 2-D grid are 2D Graphics. `RunWMM2015.py` exercises this as the package's worked
example.

**Categories considered against the current 83-row vocabulary and rejected, with reasons.** These are
recorded so a later refresh does not re-litigate them:

- **Models and Simulations: Forecasting.** Genuinely arguable and therefore worth settling in writing.
  `WMM.COF` carries secular-variation coefficients — `GeomagnetismHeader.h` declares
  `double *Secular_Var_Coeff_G; /* CD - Gauss coefficients of secular geomagnetic model (nT/yr) */` —
  and `MAG_TimelyModifyMagneticModel` extrapolates the field forward from the 2015.0 epoch, so the
  software really does predict a future field state. Rejected all the same: in this catalogue
  "Forecasting" means space-weather prediction, and a user filtering on it wants nowcasts and event
  forecasts, not a five-year secular drift term. Returning a main-field model there would be out of
  place for that searcher.
- **Models and Simulations: Physics-Based / First Principles / Theory.** The spherical-harmonic
  expansion is a physically motivated basis, but the software solves nothing — it evaluates a fitted
  coefficient table. `Empirical` already carries the correct meaning and adding a physics label would
  overstate what runs.
- **Coordinate Transforms** (and its Ionospheric/Magnetospheric/Planetary children). The vendored C
  contains real coordinate machinery — `MAG_GeodeticToSpherical`, `MAG_SphericalToGeodetic`,
  `MAG_GetUTMParameters`, `MAG_TMfwd4`, `MAG_ConvertGeoidToEllipsoidHeight`. None of it is reachable
  from this package: `src/wmm2015/__init__.py` is the single line `from .base import wmm`, and the
  geodetic-to-spherical step happens inside `wmmsub` as an internal utility. Classifying an internal
  utility as a user-facing capability is the specific error this category is prone to.
- **Data Processing and Analysis** (and its children). The CMake build produces a `wmm_file`
  executable that reads a coordinate list and writes results, but that is forward model evaluation
  over a list of points, not analysis of measured data, and it is not exposed through the Python API.
  A user filtering for data-processing tools would not expect a pure forward model.
- **Data Visualization: Line Plots** — `plotwmm` calls `ax.contour`, not a line plot.
- **Data Visualization: 2D Slices** — tempting, because `wmm()` is documented to work "for a single
  altitude value" and so returns a constant-altitude cut through a 3-D field. Rejected: the values
  are computed directly at that altitude; nothing is sliced out of a stored 3-D volume, which is what
  the category describes.
- **Data Visualization: 3D Graphics, Movies, Web-Based, Orbit Plots** — no such code exists.

`FunctionCategory` rows carry empty definitions throughout, so the category wording used above comes
from the project's software-functionality classification guidance, not from the vocabulary itself.

### 5. Related Region (RECOMMENDED)
- Earth Atmosphere

**What the software's own artifacts establish.** The public entry point is
`def wmm(glats: np.ndarray, glons: np.ndarray, alt_km: float, yeardec: float) -> xarray.Dataset:` —
geographic latitude, geographic longitude, an altitude in kilometres, and a decimal year. The worked
example `RunWMM2015.py` declares
`p.add_argument("alt_km", help="altitude (km) default: 0.", type=float, default=0.0)` and grids the
whole globe; the only test evaluates `mag = wmm.wmm(65, 85, alt_km=0, yeardec=2012.52868852459)`. So
the package's documented and exercised regime is the Earth's surface and the altitudes above it.

**The altitude guidance the bundled C actually states.** `MAG_Warnings` warns only below a floor:
" Elevations above -10.0 km are recommended for accurate results. " — a lower bound, with no upper
bound given. The file-processing program is the only place a ceiling is written down, as
`        minalt = -10; /* To be defined */` and `        maxalt = 1000;` in kilometres. The model's
own working envelope is therefore roughly 10 km below the ellipsoid to 1000 km above it.

**What the bundled C says the model does and does not include.** This is the decisive evidence, and
it comes from NOAA's own help text in `src/wmm2015/src/GeomagnetismLibrary.c`, in the WMM help block
running from line 808 to line 852. Line 809 describes the model as
`is a model of Earth's main Magnetic field.`

**That line number is load-bearing, not decoration.** The same file carries a near-identical sibling at
line 733, `is a model of Earth's main Magnetic and crustal field.`, which belongs to the Enhanced
Magnetic Model help block rather than the WMM one. The two lines share their opening words and diverge
on exactly the crustal-field point the Region argument below turns on, so a quotation truncated before
that divergence would not say which model it describes. The WMM line — the one that applies to this
software — excludes the crustal field.

Within the same WMM block, lines 834–838 say a degree and order 12 model such as WMM describes only
the long wavelength spatial fluctuations due to Earth's core, and that the intermediate and short
wavelength spatial fluctuations originating in Earth's mantle and crust are
`Not included in the WMM series` of models — that phrase falling on line 836. Line 842 then states
that also not included in `the model are temporal fluctuations of Magnetospheric and ionospheric`
origin, naming magnetic storms as the case where the model deviates most.

**Earth Atmosphere — kept, and why it is the right row rather than a finer one.** The region a user
cares about here is where the software's outputs apply: the near-Earth volume from the surface upward
that the API accepts and the model's envelope covers. `Earth Atmosphere` is the row that spans that
volume. Two finer rows were considered and rejected:

- `Earth Lower and Middle Atmosphere` — correct for the worked example and the test, both at the
  surface, but it silently discards the model's stated reach to 1000 km. Choosing it would understate
  the envelope.
- `Earth Ionosphere` and `Earth Thermosphere` — these altitudes are inside the model's envelope, but
  the software computes no ionospheric or thermospheric quantity, performs no magnetic-coordinate
  transform, and the vendored text explicitly disclaims ionospheric field contributions. Selecting
  them would put this record in front of a searcher looking for ITM tools, who would find a
  main-field model out of place.

Worth recording for a future refresh: the physical region that actually *sources* this field — Earth's
core and interior — has no row in the 24-row `Region` vocabulary at all. `Solar Interior` is the only
interior row and is solar. So there is no way to name the source region, and `Earth Atmosphere` naming
the application region is the best available truth.

**Rows rejected outright.** `Earth Auroral Subregion`, `Earth Inner Magnetosphere`,
`Earth Magnetosheath`, `Earth Magnetotail` and `Earth Outer Magnetosphere` all name magnetospheric
structures whose fields the model explicitly excludes. `Chromosphere`, `Corona`, `Photosphere`,
`Solar Interior`, `Solar Environment`, `Solar Wind`, `Interplanetary Space`, `Heliosheath`,
`Planetary Magnetospheres` and the per-planet magnetosphere rows (Jupiter, Mars, Neptune, Saturn,
Uranus) are all outside an Earth-only model's scope. That accounts for every row in the vocabulary.

**Settled: `Earth Magnetosphere` is removed from this field.** Both cases are kept below; the one not
taken was weighed and found not determinative, not refuted.

*The case for removing it.* The vendored NOAA text states that the model does not include temporal
fluctuations of magnetospheric origin, and its stated ceiling of 1000 km sits well below the
magnetosphere proper. On the searcher's side, a user browsing HSSI for software related to the Earth
Magnetosphere is looking for magnetospheric field models, magnetopause and magnetotail tools, or
storm-time analysis; a wrapper around a core-field reference model is not what they came for, and its
presence would read as a mis-tag.

*The case for keeping it.* The main field is the internal field that defines magnetospheric geometry
in the first place, and geomagnetic-field software is often filed under this row by convention. A
user who reached WMM2015 from a magnetosphere listing would not be misled about what it computes,
because the description says plainly that it is a World Magnetic Model wrapper.

*Why it went that way.* The removal case rests on the model's own words about itself, which is the
strongest evidence available; the retention case rests on cataloguing convention. The removal was
taken, and `Earth Atmosphere` is now this field's only value.

### 6. Authors (MANDATORY)
- **Author: Michael Hirsch**
  - **Identifier:** https://orcid.org/0000-0002-1637-6526
  - **Affiliation:** Boston University — https://ror.org/05qwgg493
  - **Affiliation:** Scivision, Inc.
- **Author: Manoj C. Nair**
  - **Identifier:** https://orcid.org/0000-0002-0541-0127
  - **Affiliation:** Not recorded (see below)
- **Author: Adam Woods**
  - **Identifier:** Not recorded (see below)
  - **Affiliation:** Not recorded (see below)

Authors are identified by name, not by position. The order this file lists them in is a presentation
choice and is not evidence of HSSI's stored ordering, so any later correction must be made by name
rather than by index.

**The criterion, stated so the rest of the cohort can inherit it.** Field 6 asks for the authors of
*this software*. For a wrapper package that ships a third party's library largely unmodified, the
defensible line is: **credit the people the sources name as authors of a whole component this
package ships**,
and do not credit (i) support and correspondence contacts, (ii) authors of individual routines inside
a component, (iii) authors of a prior-language original that a routine was adapted from, or
(iv) acknowledgements. Two components ship here — the Python wrapper and NOAA's Geomagnetism Library —
and the criterion yields exactly three names.

**The full candidate class in the vendored C, each line attributed to its role.** A surname count is
not a count of people, and these roles are not uniform:

- *Component authorship (included).* `GeomagnetismLibrary.c` carries the line
  ` *  Written by Manoj C Nair and Adam Woods`. This is the authorship statement for the library that
  performs all the physics — the whole scientific content of the package. Michael Hirsch is the
  wrapper's author: `setup.cfg` declares `author = Michael Hirsch, Ph.D.`, and he authored
  `wmm_point_sub.c` (the `wmmsub` entry point the Python layer calls through `ctypes`), the build
  system and every Python file.
- *Support and correspondence contacts (excluded).* ` *  Attn: Susan McLean` heads the National
  Geophysical Data Center address block, and ` *  Attn: Manoj Nair or Arnaud Chulliat` heads the
  "Software and Model Support" block; the same two names recur in runtime `printf` contact banners
  and in the date-out-of-range warning. These say whom to write to, not who wrote the code. Arnaud
  Chulliat appears in the repository **only** in that contact role, which is why he is not an author
  here even though he leads the WMM Technical Report (see Field 27).
- *Routine-level authorship inside a component (excluded).* `MAG_TMfwd4`, the Transverse Mercator
  forward projection, credits `       Algorithm developed by: C. Rollins   August 7, 2006` and
  `       C software written by:  K. Robins`. The `julday` subroutine in `wmm_file.c` credits its C
  implementation to `C. H. Shaffer` of Lockheed Missiles and Space Company. Five further routine
  headers in `GeomagnetismLibrary.c` carry Manoj Nair's name and NOAA address at routine level rather
  than component level, and they are enumerated here because this paragraph claims a full candidate
  class: `MAG_RotateMagneticVector` at line 3147 (`Manoj Nair, June, 2009 Manoj.C.Nair@Noaa.Gov`),
  `MAG_PcupHigh` at 3686 (`  Manoj Nair, Nov, 2009 Manoj.C.Nair@Noaa.Gov`), `MAG_PcupLow` at 3848
  (`   Written by Manoj Nair, June, 2009 . Manoj.C.Nair@Noaa.Gov.`), `MAG_Summation` at 4095
  (`    Manoj Nair, June, 2009 Manoj.C.Nair@Noaa.Gov`) and `MAG_SummationSpecial` at 4158
  (`Manoj Nair, June, 2009 manoj.c.nair@noaa.gov`, lowercased in that one). Those five change no
  outcome — Nair is already credited at component level by the library's own authorship line, so they
  add no person and remove none — but a completeness claim that is not complete is worse than no claim,
  and a later agent counting Nair mentions should find the count already accounted for. All of these
  routines sit inside a library that already has a named authorship line, and none of them is reachable
  from this package's Python API.
- *Authors of an original in another language (excluded).*
  `  Adopted from the FORTRAN code written by Mark Wieczorek September 25, 2005.` credits the Fortran
  original of the high-degree Legendre routine. The `julday` block likewise credits the FORTRAN
  version to `S. McLean` of NGDC. Adapting someone's algorithm from another language is a citation,
  not co-authorship of this package.
- *Acknowledgement (excluded).* The `julday` block closes with a thanks to Rob Raper for a bug fix.
- *Version-control keyword (excluded as a distinct person).* `$Author: awoods $` appears in every
  vendored file in `src/wmm2015/src/` except the coefficient header `EGM9615.h` — six of the seven.
  It is NOAA's Subversion keyword recording the last committer of their revision, and it resolves to
  Adam Woods, who is already credited.

**Why the criterion is right on the searcher's side.** A reader of this HSSI page wants to know whose
work this is and whom to cite. Three names — the wrapper's author and the two named authors of the
model code — answer that directly. Admitting the full candidate class would produce a list of ten in
which the person who actually made this Python package is one voice among many, and would credit
people for routines this package never executes. The union rule against dropping a credited
contributor is satisfied: nobody named as an author of a shipped component has been omitted, and
every excluded name is recorded above with the role that excludes it.

**Michael Hirsch — author identity and identifier.** The identifier recorded here is
`https://orcid.org/0000-0002-1637-6526`. That ORCID's public record is Michael Hirsch, Research
Scientist in Electrical and Computer Engineering at Boston University since 2018-08, with Boston
University M.Eng. and Ph.D. degrees, and works including *PyMap3D: 3-D coordinate conversions for
terrestrial and geospace environments* (10.21105/joss.00580) and *h5fortran* (10.21105/joss.02842)
alongside a series of auroral and ionospheric papers. `geospace-code/pymap3d`'s `CITATION.cff` pairs
that exact ORCID with the author name "SciVision". This repository's git history records the author
under three distinct name/address forms, all of them his.
`git log --format='%an <%ae>' fb4e06f5f66ac707f1799aa12ef1687904926d56 | sort | uniq -c`,
over the pin's full ancestry, returns 27 ×
`Michael Hirsch, Ph.D <scivision@users.noreply.github.com>`, 12 ×
`Michael Hirsch <scivision@users.noreply.github.com>`, and 1 ×
`Michael Hirsch, Ph.D <10931741+scivision@users.noreply.github.com>`. Those counts sum to 40,
which is `git rev-list --count` at the pin, so the three forms are the whole history rather than a
sample, and they differ only in the `, Ph.D` suffix and the numeric prefix. The variation is not a
rewriting artifact: there is no `.mailmap` at the pin and none was ever added in the ancestry, so
these are simply the strings the commits were authored under.

Only **one** of the forty commits — `7a08061`, 2019-11-11, "Update ci.yml" — carries GitHub's
numeric-prefixed no-reply address, and stating that frequency plainly matters: the history does not
generally record him that way. The conclusion is unweakened, because a single commit authored
under a numeric GitHub no-reply address is sufficient to bind that account to this repository's
authorship, and account ID 10931741 is the login `scivision`. `setup.cfg` gives the author as
`author = Michael Hirsch, Ph.D.`, and `space-physics/NEXRAD` gives
`author_email = scivision@users.noreply.github.com`. A future person-identity resolution here should
expect all three author forms and treat none of them as a second person; the committer field
additionally carries GitHub's own service identity, `GitHub <noreply@github.com>`, on two commits,
which is GitHub itself and not a fourth identity.

*Rejected alternative — do not reintroduce it.* `https://orcid.org/0000-0001-6183-6256` was recorded
for this author in an earlier revision of this file and is **wrong**. That ORCID belongs to a
different person of the same name: a Senior Facility Scientist at the Science and Technology
Facilities Council's Central Laser Facility, with a Leipzig University Ph.D. and Dipl. Math. in
Mathematics, whose twenty-nine works are entirely single-molecule fluorescence microscopy, EGFR/HER3
receptor biophysics and EMCCD detector physics. That record contains no heliophysics, no geospace and
no software. A future refresh that encounters the value must reject it rather than restore it.

The `Scivision, Inc.` spelling is parked deliberately across the catalogue and must not be
normalised here.

**Manoj C. Nair — identifier confirmed, and applied by database-side correction on 2026-09-07.**
`https://orcid.org/0000-0002-0541-0127` is this author. The record's employment is University of
Colorado Boulder, and its 127 works are geomagnetism throughout — including *Evaluation of candidate
models for the 13th generation International Geomagnetic Reference Field*, *International geomagnetic
reference field: the thirteenth generation*, CrowdMag work, and *Global Geomagnetic Model Errors as a
Function of Altitude and Geomagnetic Activity*. Corroboration that this is the WMM co-author is
independent of the name: the WMM2015 Technical Report (Field 27) lists "Nair, M." among its personal
authors, and the University of Colorado Boulder is where the NOAA geomagnetism group's academic
affiliate sits, at the same Boulder address the vendored C prints.

This identifier could not be applied through the metadata API and was **not** sent in this entry's
PATCH. The author's HSSI row was created without an identifier, and attaching one through an ordinary
metadata update matches on the identifier rather than the name, which would mint a second person row
and orphan the existing one. It was therefore applied on **2026-09-07 by a database-side correction**
to the existing person row, leaving that row's identity — and every other entry referencing it —
intact. A later refresh should expect to find the ORCID already present on the row and must still not
send it in a PATCH: the mint-and-orphan hazard is a property of the update path, not of the value, and
it does not go away now that the value is stored.

**Adam Woods — researched, and deliberately not asserted.** `https://orcid.org/0000-0003-1831-5038`
is a plausible candidate: the name matches, the sole employment is University of Colorado Boulder,
and the record has the same shape as Manoj Nair's confirmed record (all-caps name, one undated
institutional employment). But it lists **zero works**, so there is nothing tying it to geomagnetism
or to the WMM. A same-name-plus-same-institution match with no corroborating output is not sufficient
to credit a named individual, and asserting it risks attaching this software to the wrong person.
Recorded so a later agent neither re-hunts it from scratch nor adopts it uncritically; it needs
independent corroboration before use.

**Affiliations for Nair and Woods — researched, and correctly left empty.** The sources that name
both men as WMM authors also name their institution, and they agree.

*What the vendored C says.* `src/wmm2015/src/GeomagnetismLibrary.c` carries the authorship line
` *  Written by Manoj C Nair and Adam Woods` at line 77, inside the same file-header comment block
that gives an address at lines 52–55 — four separate comment lines carrying, in order, `National
Geophysical Data Center`, `NOAA EGC/2`, `325 Broadway` and `Boulder, CO 80303 USA` after each line's
` *  ` comment marker. They are not one run-on string and there is no separator between them; the only
`/` in the block is inside `EGC/2`.
The authorship line is not adjacent to that address either: two contact blocks and a documentation
pointer sit between them at lines 56–74. The header is one block naming both the institution and the
authors, which is what makes it evidence of affiliation, but nothing tighter than that.

*What the WMM2015 Technical Report says, and the conflict a future agent will hit.* The NOAA
repository landing page for `10.7289/V5TB14V7` (`.../view/noaa/48055`) lists, under the label
`Corporate Authors(s)`, a semicolon-delimited list rendered
`National Geophysical Data Center;British Geological Survey;` — no space after either semicolon, and a
trailing one closing the list, exactly as the page's `Personal Author(s)` list is punctuated. That is
the rendering quoted here. **Resolving the same DOI gives a different and shorter institution string:**
DataCite's record for `10.7289/V5TB14V7` gives `publisher` as `National Geophysical Data Center` with
the British Geological Survey absent entirely, and CSL via doi.org content negotiation gives both
`publisher` and `container-title` as `National Geophysical Data Center`, likewise without BGS. This is
recorded so a future agent who resolves the DOI, sees only NGDC, and takes it as a contradiction does
not "correct" the landing-page rendering away. Both renderings are of the same report; the DOI
metadata simply carries one corporate author where the catalogue page carries two.

*Why the affiliations are nonetheless left empty.* The blocker is identification, not evidence:
**the ROR registry has no record for the National Geophysical Data Center** — a v2 query for that
exact organization name returns zero results. NGDC was folded into NOAA's National Centers for
Environmental Information, whose ROR is `https://ror.org/04r0wrp59` with `ror_display`
"NOAA National Centers for Environmental Information", but that record's aliases include the National
Climatic Data Center and do **not** include the National Geophysical Data Center. Recording NCEI would
therefore assert an institution neither source names, and recording NGDC would mean an
identifier-less organization row. A third option exists and is weaker still: Manoj Nair's ORCID
attests University of Colorado Boulder, which is an ORCID-attested present-day affiliation rather
than the institution the software's own sources credit. The affiliations are left unfilled with the
mapping problem documented, so a later refresh can settle the policy question rather than rediscover
the obstacle.

### 7. Software Name (MANDATORY)
WMM2015

**Source:** The project's own capitalisation, used consistently — the README's `# WMM2015` heading,
GitHub's repository name, and the plot title the software itself renders,
`    fg.suptitle("WMM2015  {}".format(mag.time))`. The PyPI distribution name is the lowercase
`wmm2015`, which is the packaging convention rather than the project's name. The stored value is the
form a user would recognise and search for; it is preserved as submitted.

### 8. Description (MANDATORY)
WMM2015 World Magnetic Model...in simple, object-oriented Python. WMM2015 is a Python wrapper for the World Magnetic Model 2015, providing a simple interface to compute geomagnetic field components (north, east, down, total intensity, declination, and inclination) at specified geographic coordinates and altitudes. The package uses a build-on-run technique, compiling the C library on first use. Tested on Linux, Mac and Windows. Most C compilers work.

**Source and editorial status.** The opening and closing sentences are the README verbatim —
`WMM2015 World Magnetic Model...in simple, object-oriented Python.`, `Tested on Linux, Mac and Windows.`
and `Most C compilers work.` The middle is a faithful expansion: the six field components it names
are exactly the six arrays `wmm()` populates in `src/wmm2015/base.py` (`north`, `east`, `down`,
`total`, `incl`, `decl`), and the build-on-run sentence restates the README's
`This Python wrapper of WMM2015 uses our build-on-run technique.` The wording is preserved as
submitted; it is accurate against the code, and a stylistic rewrite would discard a curator's
deliberate phrasing for no gain.

### 9. Concise Description (OPTIONAL)
WMM2015 geomagnetic model with simple object-oriented Python interface

**Source:** `setup.cfg`, byte-for-byte:
`description = WMM2015 geomagnetic model with simple object-oriented Python interface`. It is also
what PyPI publishes as the package summary. Preserved as submitted.

### 10. Publication Date (RECOMMENDED)
2018-08-15

**What the previously stored 2018-05-23 is.** It is the GitHub repository creation date and the
date of the first commit (`f004b3d`, "Initial commit"), which fall on the same day. Seven commits land on 2018-05-23 in all,
including the one whose message is "initial working, API could use some streamlining" — so 2018-05-23
is when the repository and a working prototype came into existence.

**Settled: the first published release, 2018-08-15, is the recorded value.** Both readings are kept
below; Reading A was weighed and found not determinative, not refuted.

*Reading A — keep 2018-05-23.* The date the code first became publicly available. The repository has
been public from that day, and the code was already functional.

*Reading B — change to 2018-08-15.* The field definition reads "Date of first broadcast/publication"
and "Used for the initial version of the software." The first *version* is `0.9.1`, whose GitHub
release is named "initial release" and was published 2018-08-15T04:02:18Z; the matching PyPI sdist
`wmm2015-0.9.1.tar.gz` was uploaded 2018-08-15T04:03:00, forty-two seconds later. Under a reading that
ties the field to "the initial version," this is the date the software was published as a version
rather than merely pushed to a repository.

*Deciding considerations.* The definition's two sentences pull in different directions: "first
broadcast/publication" fits a public repository, while "Used for the initial version" fits the tagged
release. From the searcher's side, a publication date of 2018-05-23 tells a reader when the project
started; 2018-08-15 tells them when they could first install it. Both are defensible and both are
verifiable. Reading B was taken, on the definition's second sentence — "Used for the initial version
of the software" — so the field records the day the software first existed as an installable version
rather than the day the repository appeared.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source and reasoning.** The field definition directs that when no DOI has been obtained, the
repository host is the correct entry. Field 2 establishes that no DOI exists, and the repository is
hosted on GitHub, so GitHub is correct. Zenodo was considered and rejected: there is no
GitHub-Zenodo integration on this repository and no Zenodo deposit exists.

### 12. Version (RECOMMENDED)
- **Version Number:** 1.1.1
- **Version Date:** 2021-02-11
- **Version Description:** cleanup, CMake >= 3.10, better feedback, Numpy 1.20 types. Changes include: cmake >= 3.10, pep517 compliance, improved documentation, cmake template updates
- **Version PID:** Not found

**`1.1.1` is the newest version any source publishes.** The repository's five tags are `v0.9.1`,
`v1.0.0`, `v1.0.1`, `v1.1.0` and `v1.1.1`, and all five are verified to sit on the pinned revision's
own ancestry — checked against `git rev-list` from the pin rather than `git log --all`, because tags
in this organization's repositories can sit on pre-rewrite orphan lineages. GitHub publishes exactly
those five releases, the newest being `v1.1.1` on 2021-02-11. PyPI's newest `wmm2015` release is
`1.1.1`, sdist uploaded 2021-02-11T08:25:47, and its `home_page` is this repository, confirming the
distribution is this software rather than a name collision. `setup.cfg` declares `version = 1.1.1`.

**The `1.1.1` versus `v1.1.1` prefix.** Three sources, two spellings: `setup.cfg` says
`version = 1.1.1`, PyPI publishes `1.1.1`, and the git tag is `v1.1.1`. The unprefixed form is what
the software says about itself and what a user installing it sees; the `v` is a git tagging
convention. The stored `1.1.1` is correct and should not be "corrected" to the tag spelling.

**Version date.** 2021-02-11 is consistent across all three independent sources — the tagged commit
`2d0d219`, the GitHub release publication timestamp, and the PyPI upload — so no ambiguity arises.

**The version description is attributable to the right release range, clause by clause.** The range is
`v1.1.0..v1.1.1`, and `v1.1.0` is confirmed an ancestor of `v1.1.1`. It contains exactly four commits:
"cmake >= 3.10, better feedback, Numpy 1.20 types", "pep517", "doc" and "cmake template". Checking
each clause of the stored text against that range, reading both the release `name` and `body` of all
five releases:

- "cleanup," — from the `v1.1.1` release **name**, which is "cleanup, CMake >= 3.10". Not inherited;
  this is why reading the release name and not only the body matters, since the `v1.1.1` body is empty.
- "CMake >= 3.10, better feedback, Numpy 1.20 types" — the tagged commit's own subject, differing only
  in capitalising "cmake".
- "cmake >= 3.10" (the repetition) — the same commit, restated.
- "pep517 compliance" — the "pep517" commit.
- "improved documentation" — the "doc" commit.
- "cmake template updates" — the "cmake template" commit.

**No clause is inherited from an earlier tag**, and none is unattributable. The description is
redundant — it names the CMake version bump twice — but redundancy is a style matter, not a defect,
and rewriting it would discard the submitter's wording for no factual gain. Checked against the
neighbouring releases so the inheritance test is real: `v1.1.0`'s name and body are about applying
WMM2020's Python and CMake updates, `v1.0.1`'s is "keep build within package dir", `v1.0.0`'s is about
the build-on-run install method and moving CI to GitHub Actions, and `v0.9.1`'s is "initial release" /
"CI on Mac, Linux, Windows". None of that text appears in the stored description.

**Version PID.** None. Field 2 establishes there is no DOI for the software at all, so no
version-specific DOI can exist.

*Aside worth knowing for a later refresh:* PyPI carries a `1.0.2` sdist (2019-11-12) that has no
corresponding git tag or GitHub release. It does not affect the current version, but it explains any
apparent mismatch between the tag list and the PyPI release list.

### 13. Programming Language (RECOMMENDED)
- C
- Python 3.x

**The criterion — settled first, then applied to every inclusion and exclusion.** List a language when
the repository ships source in that language that forms part of what the software delivers to a user —
either executed by the package or compiled into the artifact the package builds — **and** the
`ProgrammingLanguage` vocabulary has a row for it. Deciding language by language invites arbitrary
calls; deciding by criterion makes the result reproducible, and the rest of this cohort can inherit it.

**The tracked tree at the pin.** Seven `.py` files, five `.c` files, two `.h` files, plus CMake and
Meson build definitions.

**Python 3.x — included.** All seven `.py` files are the package's own code, and the entire public
interface a user imports is Python. `setup.cfg` declares `python_requires = >= 3.7`. `Python 2.x` is excluded by that
same declaration.

**C — included.** The vendored NOAA library and the wrapper's `ctypes` entry point are C, and both
build systems compile it. **Both build definitions name every source explicitly; neither uses a glob.**
A search of `src/wmm2015/CMakeLists.txt` and `src/wmm2015/meson.build` for `glob`, `*.c`, `fileset`,
`add_subdirectory` or `subdir` returns no matches, with a control confirming the same search does
match `add_library`/`library(` in those files — so the build graph below is complete, with no
subdirectory to descend into.

- **CMake** compiles `add_library(geo src/GeomagnetismLibrary.c)`,
  `add_library(wmm15 SHARED src/wmm_point_sub.c)` and `add_executable(wmm_file src/wmm_file.c)`.
- **Meson** compiles `geo_lib = library('geo', 'src/GeomagnetismLibrary.c',`,
  `wmm15_lib = shared_library('wmm15', 'src/wmm_point_sub.c',` and
  `wmm_exe = executable('wmm', 'src/wmm_point.c',`.
- **`src/wmm2015/build.py` invokes CMake, and only CMake**: it resolves `    exe = shutil.which("cmake")`
  and raises `        raise FileNotFoundError("CMake not available")` if absent. Meson is present in
  the tree but is not on the path the Python package takes.
- Consequently `src/wmm2015/src/wmm_grid.c` is compiled by **neither** build system, though
  `MANIFEST.in`'s `recursive-include src/wmm2015/src *.c` still ships it in the sdist. Recorded so a
  later reader does not mistake its presence for an incomplete reading of the build graph.

The two `.h` files are C headers and are covered by the same value.

**CMake and Meson — excluded, and this is a vocabulary limit rather than a judgement.** The
`ProgrammingLanguage` vocabulary has 19 rows and contains no CMake row and no Meson row, so the
criterion's practical reach here is C and Python only. This is worth stating because automated
repository analysis reports both as languages — they are counted by byte volume alongside C and
Python — and a future agent seeing that report will otherwise try to add them and find the submission
rejected on an unknown value.

**Fortran — excluded, and this is the trap worth flagging.** The vendored C credits Fortran
*originals* it was adapted from:
`  Adopted from the FORTRAN code written by Mark Wieczorek September 25, 2005.` for the high-degree
Legendre routine, and a FORTRAN `julday` in `wmm_file.c`. No Fortran source is in the tree — those
routines exist here only as C. The vocabulary's five Fortran rows — `Fortran 2003`,
`Fortran 2008`, `Fortran 2023`, `Fortran77` and `Fortran90` — are all inapplicable.

### 14. Reference Publication (OPTIONAL)
Not found

**No publication describes this software.** The field asks for the DOI of the publication describing
the software, typically a software paper such as a JOSS submission. This package has none: there is no
paper about the Python wrapper, and the README's only `## Reference` section links two NOAA WMM map
PDFs rather than a publication about the code.

**Explicitly not the WMM Technical Report.** `https://doi.org/10.7289/V5TB14V7` describes the WMM2015
*model*, was published in 2015 before this wrapper existed, and never mentions it. It belongs in
Field 27 and is recorded there. A future refresh should not promote it here.

### 15. License (RECOMMENDED)
Other

**`Other` is the only truthful value the vocabulary permits, and this note exists so that is not read
as an unexplained fallback.**

**What the repository actually states.** `LICENSE.txt` at the pin is NOAA's World Magnetic Model
notice, not a software licence. Its operative sentence is
`The WMM source code is in the public domain and not licensed or under copyright.` It goes on to
record the 17 U.S.C. 403 notice obligation for third parties producing copyrighted works predominantly
from U.S. Government material, and it cites `https://www.ngdc.noaa.gov/geomag/WMM/license.shtml` as
its source. `setup.cfg` points `license_files` at that file and declares no licence name; PyPI's
`license` field for the distribution is empty; GitHub's licence detection returns `NOASSERTION`.

**Scope of the notice.** The notice covers **the NOAA model code**. Nothing anywhere in the tree
states a licence for the Python wrapper. A case-insensitive search of the whole tracked tree for
`licence`/`license` matches only four files: `LICENSE.txt` itself, `setup.cfg` (which merely points
`license_files` at it), `GeomagnetismLibrary.c` (which repeats the same NOAA notice in its LICENSES
block), and `.gitattributes` (a line-ending rule). Neither `pyproject.toml` nor the README says
anything about licensing. A user's rights over the wrapper are therefore undefined by the
repository, which is a real and durable property of this software rather than a gap in the
extraction.

**Licence history, established by file content across the ancestry.** The notice has been present and
substantively unchanged since the repository's first day. Commit `f11f382` (2018-05-23) added a file
named `LICENSE` carrying blob `2cf3fea62556e4042e0547d29c7fda7e591125eb`; commit `c286989`
(2019-08-18) renamed it to `LICENSE.txt` carrying blob `41fa030dd8600e90ac7eff1dfc2e0c21d64e065f`,
which is the blob at the pin. Diffing the two blobs shows the only differences are removed trailing
whitespace — the wording is identical. There is no earlier or intervening licence of any kind. This
was checked by comparing file content at each content-changing commit rather than by an
addition-filtered log, which would have reported the rename as a fresh addition and hidden the
continuity.

**Why no other row fits.** The `License` vocabulary has 11 rows: `Apache License 2.0`,
`BSD 2-Clause "Simplified" License`, `BSD 3-Clause "New" or "Revised" License`,
`Creative Commons Attribution 4.0 International`, `GNU General Public Licenses (GPL version 2)`,
`GNU General Public License v3.0 or later`, `GNU Lesser General Public License v3.0 only`, the
LGPL version 2 row, `MIT License`, `Other` and `Restricted`. **There is no public-domain row and no
U.S.-Government-work row.** `Restricted` would be actively wrong — the notice says the software may be
used freely by the public. So `Other` is not a default; it is the only row that does not misstate the
position, and this note is the record of what `Other` means for this software.

**There is no per-software License URI, and an earlier revision's was unwritable.** An earlier
revision of this file carried a `License URI:` sub-value of
`https://www.ngdc.noaa.gov/geomag/WMM/license.shtml`. HSSI has no per-software licence URI: the
software's licence is a foreign key to a shared licence row that carries its own URL, so a
software-specific URI cannot be stored at all. That URL is cited above as **evidence** for what the
notice says, and must not be reintroduced as a storable value.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- build-on-run
- declination
- geomagnetic
- geomagnetism
- inclination
- magnetic field
- main field
- secular variation
- spherical harmonics
- World Magnetic Model

Keywords are the one open vocabulary in this record, so the stored spellings above are what matter;
the site renders them title-cased, and that rendering must never be mistaken for the stored value.

**Carried forward from the existing record:** `build-on-run`, `geomagnetic`, `geomagnetism`,
`magnetic field` and `World Magnetic Model`. The two other keywords the record carried,
`ionosphere_thermosphere_mesosphere` and `specific`, are removed — see below. `geomagnetic` is
`setup.cfg`'s only declared keyword and, with `build-on-run`, one of the repository's two GitHub
topics.

**Added in this refresh, each with in-repository evidence and each reusing an existing vocabulary row
so no near-duplicate is minted:**

- **`declination`** — one of the two quantities the software plots and one of the six it returns:
  `    ax[0].set_title("Magnetic Declination [degrees]")`, the `decl` array in `base.py`, and the
  README's link to the WMM2015 declination map.
- **`inclination`** — the other: `    ax[1].set_title("Magnetic Inclination [degrees]")`, the `incl`
  array, and the README's inclination map link.
- **`main field`** — the precise term the vendored C uses for what the model represents. This is the
  keyword that most efficiently distinguishes this software from external-field and
  magnetospheric-field models, which is the confusion most likely to send a searcher here by mistake.
- **`secular variation`** — the mechanism that makes the model valid across its five-year epoch:
  `WMM.COF` ships secular-variation coefficients, declared in `GeomagnetismHeader.h` as
  `double *Secular_Var_Coeff_G; /* CD - Gauss coefficients of secular geomagnetic model (nT/yr) */`.
- **`spherical harmonics`** — the model's method. The vendored library's abstract states
  `It however is built to be used for spherical harmonic models of the Earth's magnetic field`
  (`src/wmm2015/src/GeomagnetismLibrary.c:15`), and the program's help text describes WMM as a degree
  and order 12 model.

**Considered and not added.** `WGS84` — the model is referenced to the WGS-84 ellipsoid, but that is a
reference-frame detail a user is unlikely to search on. `navigation` — the vendored C discusses
compass readings and grid variation, but the repository never uses the word, and adding it would
assert an application the software does not claim. `noaa` — true and evidenced, but an institution tag
rather than a subject term. `empirical model` — already carried by Field 4's
`Models and Simulations: Empirical`. `geomagnetic field` — a near-duplicate of the stored
`geomagnetic` and `magnetic field`. `WMM` — would mint a new row, and the software's own name already
carries the token while the expanded form is already stored.

**Settled: both PyHC facet tags are removed.** The cases on each side are kept below, because the
retention case was weighed and found not determinative rather than disproved.

Both `specific` and `ionosphere_thermosphere_mesosphere` entered this record from the PyHC registry
entry reproduced near the end of this file, not from anything the software says about itself.

*`specific`.* This is not a subject keyword at all. PyHC's `_data/taxonomy.yml` defines a facet
`category: "Span"` with `description: "The user scope of a project"` and
`keywords: ["general", "specific"]`. The value means "this project's user scope is narrow" — a
statement about the registry's classification scheme, not about geomagnetism. Rendered on the HSSI
page as "Specific", it is uninterpretable, and a user who clicks it gets an arbitrary cross-section of
the catalogue. The case for removal rests on that evidence. The case for keeping it — that
it is a faithful copy of PyHC's data — was weighed and found not determinative.

*`ionosphere_thermosphere_mesosphere`.* A PyHC "Science Area" facet tag, and one that propagates
across many registry entries. The test is whether this software touches that domain rather than
inheriting the label. *Against keeping:* the vendored C states that temporal fluctuations of
magnetospheric and ionospheric origin are not included in the model, and the software computes no
ionospheric, thermospheric or mesospheric quantity. A user searching HSSI for ITM software wants
models of that region's physics and would find a core-field model out of place. *For keeping:* the
model's stated envelope reaches 1000 km, which spans the ITM altitudes, and the main-field vector is a
routine input to ITM work — magnetic coordinates, conductivity tensors, field-aligned geometry — so an
ITM researcher might well be glad to find it. Note that a searcher who wants the field for that
purpose would more naturally reach it through `geomagnetic`, `magnetic field` or the newly added
`main field`, all of which are stored.

*Consistency with Field 5.* This removal and the `Earth Magnetosphere` removal in Field 5 rest on the
same evidence — the model's own statement about what it excludes — and were settled together, so the
record does not claim a region it disclaims while denying a keyword on the same ground, or the
reverse.

### 17. Data Sources (OPTIONAL)
Not found — and correctly so.

The software reads no remote data source. Its coefficients are bundled in the repository as
`src/wmm2015/WMM.COF`, and the Python API takes numbers as arguments rather than fetching anything.
The one file the software can read is a local ASCII coordinate list the user writes, consumed by the
`wmm_file` program.

The `DataInput` vocabulary's 17 rows are `AMDA`, `CDAWeb`, `das2`, `FTP/FTPS Directories`, `GFZ`,
`HAPI`, `HTTP/HTTPS Directories`, `Madrigal`, `Observatory/Mission-specific`, `OMNIWeb`, `Other`,
`S3/Cloud-aware`, `SSCWeb`, `TAP`, `The Virtual Solar Observatory.`, `VirES` and `WDC`. Every one names
an archive, service or transport this software does not use. `Other` was considered for the local-file
case and rejected: there is no local-file row, and selecting `Other` would tell a searcher nothing
while implying the software has an external data-access capability it does not have. Enumerating the
vocabulary is the reason this field is correctly empty, not merely the record that it was checked.

### 18. Input File Formats (RECOMMENDED)
- ascii

The primary Python API takes numeric arguments programmatically and reads no user file. Two ASCII
inputs exist nonetheless: the bundled coefficient table `src/wmm2015/WMM.COF`, which the C reads at
every call, and the coordinate list consumed by the `wmm_file` program, of which the repository ships
an example at `src/wmm2015/test_input.asc`. Both are plain text.

No other row in the 11-row `FileFormat` vocabulary applies: `CDF`, `csv`, `FITS`, `HDF5`, `IDL.sav`,
`ISTP-Compliant`, `JSON`, `netCDF3/4`, `Zarr` and `Other` all name formats the software neither reads
nor recognises. The `wmm_file` output is space-aligned columns rather than delimited fields, so `csv`
would be wrong.

### 19. Output File Formats (RECOMMENDED)
- ascii

The Python API returns an in-memory `xarray.Dataset` and writes no file — an in-memory object is not a
file format, and recording one here would misdescribe the API. The `wmm_file` program writes an ASCII
results file, which is the only data file this software writes. The same rejection of the remaining ten
`FileFormat` rows applies as in Field 18.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Directly evidenced, and the complement is evidenced too.** The README states
`Tested on Linux, Mac and Windows.` The CI workflow runs the test suite on `ubuntu-latest`,
`macos-latest` and `windows-latest`.

More decisively, `src/wmm2015/build.py` enumerates the supported platforms in code: `get_libpath`
branches on `win32`/`cygwin`, `linux` and `darwin`, and for anything else raises
`        raise ValueError(f"Unsupported platform: {sys.platform}")`. That explicit failure is why
`Operating System Independent` — otherwise tempting, since `setup.cfg` declares the classifier
`Operating System :: OS Independent` — would be **false**. The classifier overstates what the code does.

`Solaris` was considered and rejected: the vendored `GeomagnetismHeader.h` names Sun Solaris with GCC
among the environments NOAA's subroutine library was tested in, but that is upstream's testing of
upstream's code, and this Python package would refuse to build there. `MobilePlatform` and `Other`
have no supporting evidence. Note that `cygwin` is handled in the code but has no vocabulary row of
its own; it is covered in practice by `Windows`.

A separate and important constraint that is not an operating-system value: the README states that
Visual Studio is not supported, because MSVC does not export function symbols without additional
headers. That restricts the *compiler*, not the platform — the package works on Windows through MinGW,
which `build.py` selects by default.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

The package compiles portable C from source on the host at first use, and contains no
architecture-specific code: a case-insensitive search of `src/wmm2015/src/` for `__x86`, `__SSE`,
`__AVX`, `asm volatile`, `_mm_` intrinsics, `__aarch64` or the word `intrinsic` returns zero matches,
while a control search of the same directory for `sqrt` matches 28 lines in `GeomagnetismLibrary.c` —
so the negative is real and not a broken pattern. Nothing in the build definitions, the packaging
metadata or the documentation pins an architecture.

The remaining `CpuArchitecture` rows were considered and rejected. `x86-64`, `Apple Silicon arm64`,
`Linux aarch64 or arm64`, `ppc64le` and `Sun (SPARC)` would each *narrow* a package that is not narrow
— the CI runners happen to be one architecture, but that is a property of the CI configuration, not a
limit on the software. `GPU` and `HPC or HEC` describe capabilities this single-threaded scalar code
does not have. `Other` would be less informative than the correct row.

### 22. Related Phenomena (OPTIONAL)
Not found — and the vocabulary is the reason.

The `Phenomena` vocabulary has 7 rows: `Coronal Heating`, `Coronal Mass Ejections`,
`Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and `X-ray emission`. Six are solar
or heliospheric and plainly inapplicable to an Earth main-field model.

The seventh, `Geomagnetic Storms`, is the near-miss and is **explicitly excluded by the model itself**.
The vendored C states that temporal fluctuations of magnetospheric and ionospheric origin are not
included, and names magnetic storms as the case where the model deviates most from reality. Selecting
it would attach this software to precisely the phenomenon its own documentation warns it does not
represent. A searcher looking for storm-time tools would be actively misled.

The phenomenon this software *does* support — the Earth's main geomagnetic field and its secular
variation — has no row in this closed vocabulary. Per the field's own guidance, a supported phenomenon
with no row belongs in Keywords instead, which is where `main field` and `secular variation` have been
recorded in Field 16.

### 23. Development Status (RECOMMENDED)
Inactive

**HSSI held no value for this field before this refresh.** `Inactive` is derived from the
repostatus.org definitions carried by the vocabulary itself, not assumed.

The vocabulary's `Inactive` row is defined as: "The project has reached a stable, usable state but is
no longer being actively developed; support/maintenance will be provided as time allows." Both halves
hold.

*Stable and usable.* The PyPI classifier is `  Development Status :: 5 - Production/Stable`, five
tagged releases exist, and the CI suite passes across three operating systems.

*No longer actively developed, but not closed.* The last push to the repository was 2021-10-11 and the
last release 2021-02-11. The repository is **not archived** and not disabled, and it carries one open
issue — so the project remains open to contact rather than shut. Note that GitHub's `updated_at`
timestamp of 2024-10-14 is **not** commit activity; it moves on metadata events such as starring, and
must not be read as evidence of development. The project has never received a pull request: a GitHub
issue-search restricted to this repository with `is:pr` returns zero, and the same query against the
sibling `space-physics/wmm2020` returns six, confirming the query works.

**Alternatives considered and rejected.**

- `Unsupported` — "The project has reached a stable, usable state but the author(s) have ceased all
  work on it. A new maintainer may be desired." Rejected on the two clauses of that definition rather
  than on any archiving test: the definitions distinguish `Unsupported` from `Inactive` by whether the
  author has ceased *all* work and a new maintainer is wanted, not by a repository flag. Neither clause
  holds here. The project remains open to contact — not archived, not disabled, carrying one open issue
  — and nothing in the repository, its packaging or its README seeks a new maintainer. `Inactive`'s
  weaker claim, that "support/maintenance will be provided as time allows", is what the evidence
  supports. The unarchived state is one observation among that evidence, not the criterion.
- `Moved` — "The project has been moved to a new location, and the version at that location should be
  considered authoritative." This is the trap here, and it is worth writing down: the repository's
  GitHub *homepage* field points at `https://github.com/space-physics/wmm2020`, which reads like a
  redirection. It is not one. WMM2020 implements a **different model epoch** and is a separate package
  with its own coefficients; it does not supersede this software as an implementation of WMM2015, and
  a user who needs the 2015 model must still use this one. The pointer is a signpost to the newer
  epoch, not a relocation.
- `Active`, `Concept`, `WIP`, `Suspended`, `Abandoned` — all excluded by the combination of five
  releases, a production classifier, and no commit since October 2021.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/WMM2015

**Changed from the previously stored `https://github.com/space-physics/wmm2015` — a case correction,
not a new destination.**

**Why this URL is right at all.** The documentation is the README, and there is nowhere else for it to
point. There is no `docs/` directory in the tree, no ReadTheDocs configuration, and GitHub Pages is
not enabled. The repository wiki has no content: requesting `/wiki` redirects to the repository root,
while the same request against a repository that does have a populated wiki stays on the wiki page —
and in any case a wiki lives in a separate repository invisible from this code pin, so its being
enabled proves nothing. The field definition explicitly sanctions this case: "If this is the same as
the access URL, then enter that link here." The README does carry installation instructions, under
`## Install`, with both the PyPI and editable-checkout paths.

**Why the case matters, decided from the searcher's side.** The previously stored value was lowercase
because it was copied from `setup.cfg`'s `url = https://github.com/space-physics/wmm2015`. GitHub
resolves both spellings, so nothing breaks — but HSSI renders each field as a visible link, and a
reader of this page would have seen a Code Repository ending in `WMM2015` beside a Documentation link
ending in `wmm2015`, and had to work out whether those are two different places. They are not.
Matching Field 3 exactly removes a distinction that carries no information and reads as an
inconsistency.

### 25. Funder (OPTIONAL)
Not found

**Nothing in the repository names a funder.** A case-insensitive search of the entire tracked tree at
the pin for `fund`, `funding`, `funder`, `grant`, `award`, `sponsor`, `NSF`, `NASA` or `contract` as
word-initial tokens returns zero files. Two controls show that negative is a real absence rather than
a failed pattern, and each is stated with the scope it was counted over, so both numbers are
reproducible as written. Over that same whole tracked tree, word-initial `Boulder` matches two files.
Restricted to the vendored C and headers — pathspec `src/wmm2015/src/*.c` and `src/wmm2015/src/*.h` —
the case-insensitive alternation `\b(NOAA|fund)` matches six: `GeomagnetismHeader.h`,
`GeomagnetismLibrary.c`, `wmm_file.c`, `wmm_grid.c`, `wmm_point.c` and `wmm_point_sub.c`. Over the
whole tree that same alternation matches nine files case-insensitively and two case-sensitively.
`fund` matches nothing anywhere in the tree at any case, which is why every hit under either scope is
a spelling of NOAA.

**Two near-misses, recorded so they are not mistaken for funding.**

- `.github/FUNDING.yml` existed in this repository's history and was deleted at commit `25791ce`
  (2021-01-02). Its entire content was `github: [scivision]` and `ko_fi: scivision` — personal
  donation links for the maintainer, not a research funding acknowledgement. It is absent at the pin.
- The vendored C's help text names the model's sponsoring and developing bodies: the model is a joint
  product of the United States' National Geospatial-Intelligence Agency and the United Kingdom's
  Defence Geographic Centre, developed jointly by the National Geophysical Data Center and the British
  Geological Survey. Those bodies sponsor **the WMM model**, not this Python wrapper, and none of them
  is described as funding software development. Recording any of them here would attribute this
  package's creation to institutions that had nothing to do with it.

### 26. Award Title (OPTIONAL)
Not found

Follows directly from Field 25: with no funder named anywhere in the repository, there is no award to
name. No grant or contract number appears in the tree.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.7289/V5TB14V7

**Resolved through doi.org content negotiation.** The record returns title
"The US/UK World Magnetic Model for 2015-2020", publisher "National Geophysical Data Center", issued
2015, first author "Chulliat, A.". The NOAA repository landing page for the same DOI lists the
personal authors as Chulliat, A.; Macmillan, S.; Alken, P.; Beggan, C.; Nair, M.; Hamilton, B.;
Woods, A.; Ridley, V.; Maus, S.; Thomson, A., and the corporate authors as National Geophysical Data
Center and British Geological Survey. This is the WMM2015 Technical Report.

**Why it belongs here.** The vendored C repeatedly and specifically directs its user to this document:
it cites Equations 17-18 of the WMM Technical report for the geodetic-to-spherical conversion,
Equation 19 for the time adjustment of coefficients, tells the user to see the WMM Technical Report
for more information about model uncertainties, and points at the WMM Technical Documentations for
details on the subroutines. The report is the specification of exactly what this software computes,
and its abstract states it contains the information users of WMM2015 require in order to implement the
model and software correctly. A reader on this HSSI page cannot use the software properly without it.

**The definitional caveat, recorded honestly.** Field 27 is defined as publications that "describe,
cite, or use the software". This report describes the **model**, not this Python wrapper, and predates
the wrapper by three years. It is recorded here on the searcher's-side judgement that the document a
user must read to use this software correctly is more valuable on the page than a strict reading of
the definition is protective. A future agent should not remove it as merely out of scope without
weighing that; nor should it be promoted to Field 14, which asks for a publication describing *the
software* (see Field 14).

**Rejected alternatives.** The README's `## Reference` section links two NOAA WMM2015 map PDFs — an
inclination map and a declination map. Those are chart products with no DOI and no publication record,
not publications, and they are better represented by the model and dataset entries already recorded.
The 2020-2025 and 2025-2030 Technical Reports exist and were rejected: they document later model
epochs that this software does not implement.

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.7289/V5TH8JNW

**Resolved through doi.org content negotiation.** The record returns title "World Magnetic Model 2015",
publisher "NOAA National Centers for Environmental Information", issued 2014, type `dataset`, first
author "Chulliat, A.". This is the WMM2015 coefficient release.

**Why it belongs here.** The field asks for datasets the software supports functionality for. This
software's entire function is to evaluate this coefficient set, which it ships in the repository as
`src/wmm2015/WMM.COF`. Recording it tells a reader exactly which model release is inside the package —
information that is otherwise only discoverable by opening a coefficient file.

**Rejected alternative, and the evidence that settles it.** `https://doi.org/10.25921/XHR3-0T19` —
"World Magnetic Model 2015 version 2", NOAA National Centers for Environmental Information, issued
2019 — is the *revised* 2015-epoch coefficient set, released after the original was found to be
drifting out of specification. This package does **not** ship it. The first line of
`src/wmm2015/WMM.COF` carries the tokens `2015.0`, `WMM-2015` and `12/15/2014`, identifying it as the
original December 2014 release; the v2 file identifies itself differently. Recording the v2 DOI would
misstate which coefficients a user of this package actually gets.

### 29. Related Software (OPTIONAL)
- https://github.com/space-physics/WMM2020
- https://github.com/space-physics/igrf

Both are entries in this catalogue, and each URL is that entry's exact stored repository URL, because
the page renders a related item's raw URL as its own link text.

**WMM2020 — kept, with its capitalisation corrected.** The previously stored value was
`https://github.com/space-physics/wmm2020`, all-lowercase. The WMM2020 catalogue entry's stored
repository URL is `https://github.com/space-physics/WMM2020` with capitals. What follows from the
mismatch is a rendering problem rather than a broken link: the lowercase form would display on this
page as a URL that does not match the one displayed on WMM2020's own page, making two references to
the same project look like references to two different things. The corrected form also matches the
direction the relation already runs the other way — the WMM2020 entry lists
`https://github.com/space-physics/WMM2015` as its related software, using this record's exact stored
repository URL — so the pair becomes symmetric.

WMM2020 qualifies on the merits regardless of the reciprocal link: it is the same author's next-epoch
package, built the same way, and it is the software a user should reach for if they need the current
model rather than the 2015 one. This repository's own GitHub homepage field points at it, and the
README states that WMM2020 is also available and links to it.

**IGRF-13 — added.** `https://github.com/space-physics/igrf` is the catalogue's entry for
"International Geomagnetic Reference Field: IGRF13 in object-oriented Python or Matlab". It is this
software's closest peer: the other internationally standard model of the Earth's **main** magnetic
field, wrapped by the same author with the same build-on-run architecture and the same
object-oriented Python interface. That is exactly the field's stated case of software that "performs
similar tasks but does not necessarily link together". On the searcher's side, a user who lands on
WMM2015 and wonders what the alternatives are is best served by exactly this pointer — WMM and IGRF
are the two models a geomagnetic-field user chooses between.

**Candidates considered and rejected, so this is not re-litigated.** Two mechanical slices of the
catalogue were run: an inbound slice for entries whose relation fields point at this repository, and a
by-concept slice over entry names, descriptions and keywords for geomagnetic and magnetic-field terms.
The inbound slice found only WMM2020, already covered. The by-concept slice surfaced these, all
rejected:

- **IGRF-14** (`https://www.ncei.noaa.gov/products/international-geomagnetic-reference-field`) — the
  IGRF *model product page* rather than a peer software implementation. The software peer for that
  model is already covered by IGRF-13, and adding a long NCEI product URL that renders as its own link
  text would add noise rather than information.
- **igrfpy** (`https://github.com/lkilcommons/igrfpy`) — rejected on the same test that admits
  IGRF-13, so that the bar excluding one entry is the bar admitting the other. IGRF-13 is admitted
  because four things hold at once: it implements the other internationally standard model of the
  Earth's main field, it is by this package's own author, it uses the same build-on-run architecture,
  and it presents the same object-oriented Python interface. igrfpy satisfies only the first. Its
  catalogue author is Liam Kilcommons, with no authorial relationship to this package; its `setup.py`
  builds `igrfpy/igrf11.f` and `igrfpy/igrf12.f` as `numpy.distutils` Fortran extensions rather than
  compiling C on first import, so the architectures have nothing in common; and it wraps IGRF-11 and
  12 rather than IGRF-13. It is a peer of the IGRF *model*, not of this *package*, and it is the
  package relationship that puts IGRF-13 on this page.
- **geopack** — Tsyganenko external-field models. These model the magnetospheric field, which is the
  component WMM explicitly excludes; a reader would be more likely to conflate the two than to be
  helped.
- **python-magnetosphere** — a mixed collection that happens to include an IGRF module; not a peer to
  a single-model wrapper.
- **AACGMv2, ApexPy, OCBpy, OMMBV** — magnetic *coordinate system* conversions. Different task, and
  Field 4 records that this software provides no user-facing coordinate transform.
- **pyglow** — an aggregator wrapping HWM, IRI and IGRF together; not a comparable single-model tool.
- **HWM-93, ACEmag, GIMAmag, Auroral Electrojet** — four packages this software's own author wrote or
  co-wrote in the same `space-physics` GitHub organization (`space-physics/hwm93`,
  `space-physics/ACE_magnetometer`, `space-physics/gima-magnetometer`, `space-physics/AEindex`), each
  in a different scientific domain: neutral winds, ACE magnetometer data, GIMA magnetometer data and
  the auroral electrojet index. **Shared authorship is not relatedness**, and this is the most tempting
  wrong inclusion here.
- **pyIRI2016** (`https://github.com/rilma/pyIRI2016`) — rejected because it models ionospheric
  electron density rather than the Earth's main field. It is worth recording separately that it does
  **not** belong with the four above, because the by-concept slice surfaces it alongside them and the
  grouping is easy to assume: its catalogue entry gives the repository as
  `https://github.com/rilma/pyIRI2016` — the `rilma` organization, not `space-physics` — and its
  catalogue author is Ronald Ilma, not this software's author. Sweeping it into a shared-authorship
  rejection would put a false authorship claim in this file; the domain ground alone rejects it.
- **numpy** — excluded by the standing Tier A rule, which the field's own text applies to Field 29 as
  well as Field 30. See Field 30.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/pydata/xarray

**numpy removed — the Tier A rule applied, not a reviewer's preference.**
`resource_submission_form_fields.md` lists numpy under "Never list these (Tier A), no exceptions", and
its rationale is that being a dependency is not interoperability: depending on numpy is true of nearly
every package in this catalogue and so distinguishes nothing about this one. The same text extends the
exclusion to Field 29, so numpy does not relocate there — the correct destination is neither field.

**xarray kept, on the specific exchange the public API documents.** xarray is a Tier B package, which
qualifies only when a specific exchange appears in the public API, docs, examples or tests, and never
on dependency presence alone. The exchange here is in the public API and is the strongest form the
guidance describes — the documented interchange type of the package's only public function:

- `src/wmm2015/__init__.py` is the single line `from .base import wmm`, so `wmm()` is the entire
  exported surface.
- Its signature is
  `def wmm(glats: np.ndarray, glons: np.ndarray, alt_km: float, yeardec: float) -> xarray.Dataset:`
  — the return type is declared as an `xarray.Dataset`, and the body constructs one:
  `    mag = xarray.Dataset(coords={"glat": glats[:, 0], "glon": glons[0, :]})`.
- The package's own second module consumes that object across a module boundary:
  `def plotwmm(mag: xarray.Dataset):`.

So a user does not merely run this alongside xarray — the model results are *handed to them* as an
xarray object, and any xarray-based workflow can consume them with no conversion step. That is
concrete and specific to this software, not a claim that would read the same for an arbitrary package.
Contrast the internal-use case explicitly excluded by the guidance: `transect()` returns a plain dict
and is not exported, so the xarray relationship is genuinely the public interface rather than an
implementation detail.

**The honest limitation.** The README does not mention xarray, so the evidence is the API signature
and type annotations rather than prose documentation. That is a weaker footing than a documented
adapter function would be, and is recorded here so a future refresh can weigh it rather than
rediscover it. It was judged sufficient because the annotation is on the sole public entry point and
is enforced by the package's own second module.

**Blanket justifications explicitly not relied on.** Neither "part of the standard scientific Python
ecosystem" nor PyHC membership is offered as a reason for anything in this field; the form's text
rules both out on their own, and the xarray entry stands or falls on the API evidence above.

### 31. Related Instruments (OPTIONAL)
Not found — the software is instrument-agnostic.

**Why no instrument qualifies.** The relevance gate asks whether the software is *designed to support*
a specific instrument. WMM2015 reads no instrument's data at all: it evaluates a fitted global
coefficient table at coordinates the user supplies. There is no instrument-specific format, parser,
calibration or archive client anywhere in the tree. A user working with any particular magnetometer's
data would not reach for this package, and a searcher browsing an instrument's page for related
software would find it out of place.

**The searches that back that up, with their patterns and column scope.** The `InstrumentObservatory`
vocabulary was swept for magnetometer and geomagnetic concepts using the case-insensitive pattern
`magnetometer|geomagnet|magnetic observ|INTERMAGNET|world magnetic|\bWMM\b|\bIGRF\b|\bSwarm\b|\bCHAMP\b|\bOersted\b|declinat`.
**Scope changes the answer materially, which is why both sweeps are published:** matching the `name`
column alone gives 2505 rows, while matching `name`, `abbreviation`, `identifier` and `definition`
gives 3517 (2454 of type instrument and 1063 of type observatory). Either way the hits are ground magnetometer stations and spacecraft magnetometers, none
of which this software touches. A targeted four-column probe for `world magnetic` or a word-bounded
`WMM` returns exactly one row — an OGO-2 Rubidium Vapor Magnetometer — which is a coincidental text
match, not a WMM record. There is no World Magnetic Model row in this vocabulary, which is correct:
the WMM is a model, not an instrument or observatory.

**A tempting association, considered and rejected.** The satellite magnetometry that the WMM2015
coefficients were *derived from* — Swarm, CHAMP and Oersted — does have rows in the vocabulary
(for example `https://spase-metadata.org/SMWG/Observatory/CHAMP`,
`https://spase-metadata.org/SMWG/Instrument/CHAMP/FGM`,
`https://spase-metadata.org/SMWG/Instrument/Oersted/OESM`, and Swarm A/B/C magnetometer rows). They
are **not** listed, and should not be added by a later refresh: this software does not read those
missions' data, does not implement their formats, and was not built by their teams. The provenance of
the coefficients belongs to the model's documentation, which Field 27 records; it is not a
designed-to-support relationship for this wrapper.

The vocabulary's SPASE-identifier guard was applied and holds: every row carries an identifier under
`https://spase-metadata.org/`, with none failing. Had a row failed it, it would have been reported
rather than used.

### 32. Related Observatories (OPTIONAL)
Not found — the software is observatory- and mission-agnostic.

The same reasoning and the same searches as Field 31 apply; the observatory-typed rows were included
in those sweeps. WMM2015 is a global model with no mission or observatory affiliation: it is not a
mission tool, it processes no observatory's data products, and it implements no observatory-specific
convention. The only near-associations are the missions whose measurements fed the model's coefficient
fit, rejected in Field 31 for the same reason.

Consistently with this, Field 17 records no `Observatory/Mission-specific` data source, since there is
no observatory-specific input to declare.

### 33. Logo (OPTIONAL)
Not found
*(stored value; erroneously left empty — see the correction below, to be applied at the next refresh)*

**Correction — queued, not yet applied to HSSI: the earlier exclusion of the README hero image was
ERRONEOUS for this software.** The general Field 33 rule is unchanged: a README hero figure with
nothing else presenting it as branding is a figure, not a logo. This package and its sister WMM2020 are
a deliberate, developer-backed exception: the developer has stated that these plot images are the ones
they want used as the packages' logos, which is presentation evidence of the kind the rule asks for,
and WMM2020 already records its nearly identical README hero plot as its logo. The two entries must
agree. **Any agent refreshing WMM2015 must add the pinned URL below as the Field 33 value in its next
update**, re-verifying the fetch and the pin at that time; if the file has moved, re-pin the same image
at its current commit. Until that update is applied, HSSI holds no logo for this software and the value
line above records that stored state. The candidate and its verification are kept in full below so the
refresh does not have to re-derive them. This exception extends to no other package.

HSSI holds no logo for this software. Exactly one image exists in the tracked tree,
and it is the README's hero image, referenced from the README as
`![image](./src/wmm2015/tests/incldecl.png)` immediately after the introductory text and before
`## Install`.

*The candidate URL, verified.*
`https://raw.githubusercontent.com/space-physics/WMM2015/fb4e06f5f66ac707f1799aa12ef1687904926d56/src/wmm2015/tests/incldecl.png`
It is pinned to a 40-hex commit SHA with no branch name and no `blob/` segment, and it is 127
characters, inside the 200-character field limit. Fetching it returns `image/png`, 160,516 bytes,
sha256 `7bd79685c9da97de7efcf9d130dee310fe9c4e46c5bec956c66fc2172b69428e`, byte-identical to the blob
tracked at the pin — so it is genuine image content rather than a Git-LFS pointer, and the repository
declares no LFS filters. The image is 1528x651, RGBA.

*What the image actually shows.* A two-panel matplotlib contour figure. The suptitle reads
"WMM2015  2015"; the left panel is titled "Magnetic Declination [degrees]" and the right "Magnetic
Inclination [degrees]"; both are plotted against "Geographic longitude (deg)" and "Geographic latitude
(deg)" with viridis-coloured labelled contours at 20-degree intervals. It is precisely
the output of `plots.plotwmm()` — it matches `    fg.suptitle("WMM2015  {}".format(mag.time))`, the
two `set_title` calls, and the `range(-90, 90 + 20, 20)` contour levels in `src/wmm2015/plots.py`.

*The case for recording it.* The project itself presents this image as its visual identity: it is the
README's only content image — the four other image references there are status badges — and it sits
in hero position immediately below them. Sample output is a common and legitimate form of identity
for a scientific model package, and on the searcher's side a thumbnail of global declination and
inclination contours conveys what this software does far better than an empty logo slot does.

*The reasoning that excluded it, now rejected.* The exclusion rested on these observations, which
remain true but do not disqualify the image under the current rule. It is not a logo in the designed
sense — no wordmark, no mark, no chosen palette; it is a figure the plotting function happens to produce. Its path is `src/wmm2015/tests/incldecl.png`,
i.e. it lives in the **test directory**, which suggests it was committed as a test fixture or
reference output and reused in the README rather than authored as a brand asset. At 1528x651 it is a
wide figure, not a shape a logo slot is designed for. And the PyHC registry entry for this software
(reproduced below) carries **no** `logo:` field, so the one external registry that could have
corroborated the project's own intent does not.

*Why that reasoning does not decide this case.* Those observations would exclude the image under the
general rule, and for another package they still would. Here the developer's stated wish that this
image serve as the package's logo supplies the presentation evidence the rule asks for, so a
sample-output figure, its location under the test directory, its wide aspect ratio, and the absence of
a `logo:` field in the PyHC registry are not grounds to exclude it. WMM2020 records its counterpart
plot as its logo on the same basis, and the two entries should agree.

*Outcome.* The sole image in the tree is this software's logo and belongs in Field 33 at the pinned URL
above; the stored value is empty only because the erroneous exclusion has not yet been reversed in
HSSI. No substitute image was sought or invented; there is no other image in the tree.

---

## PyHC Registry Information

WMM2015 appears in the PyHC registry's **unevaluated packages** list, `_data/projects_unevaluated.yml`
in `heliophysicsPy/heliophysicsPy.github.io` — not in the core or community lists. Pinning the
specific file matters, because the three lists carry different curation status. The entry is:

```yaml
- name: WMM2015
  code: https://github.com/space-physics/WMM2015
  description: World Magnetic Model 2015 from Python
  contact: Michael Hirsch
  keywords: ["ionosphere_thermosphere_mesosphere","specific"]
```

This is the origin of the two keywords Field 16 records as removed. Both are facet tags drawn from
`_data/taxonomy.yml` — `ionosphere_thermosphere_mesosphere` from the "Science Area"
facet and `specific` from the "Span" facet, whose description is "The user scope of a project" and
whose only two values are `general` and `specific`. The entry carries no `logo:` field, which bears on
Field 33. The registry's `code` URL uses the capitalised repository spelling, matching Field 3.

---

## Notes

- **What this software is.** A Python wrapper around NOAA's WMM2015 reference C implementation, using
  a build-on-run technique: the C library is compiled on first import rather than shipped as a binary
  wheel. Every release is a source distribution; there are no wheels on PyPI. This means a working C
  compiler is a runtime prerequisite, which is unusual and worth knowing before interpreting the
  operating-system and CPU-architecture fields.
- **Model epoch.** This package implements WMM2015, valid for the five years from its 2015.0 epoch.
  Its successor for the current epoch is a separate package, WMM2020, recorded in Field 29. WMM2015 is
  not superseded *as an implementation of WMM2015*, which is why Field 23 is `Inactive` rather than
  `Moved`.
- **Compiler constraint.** MSVC is not supported, because it does not export function symbols without
  additional headers; MinGW is used on Windows. This is a compiler limit, not a platform or
  architecture limit — see Fields 20 and 21.
- **A file that ships but never compiles.** `src/wmm2015/src/wmm_grid.c` is included in the source
  distribution by `MANIFEST.in`'s `recursive-include src/wmm2015/src *.c` but is named by neither the
  CMake nor the Meson build. Recorded so its presence is not read as an incomplete survey of the build
  graph.
- **Repository history.** The project has been renamed twice; `scivision/wmm2015` and
  `scivision/pywmm2015` both still redirect to the current location, and a `pywmm2015/` package
  directory survives in the ancestry. Relevant to Field 2, where a search keyed only on the current
  name would be incomplete.
