# HSSI Metadata Extraction Results

**HSSI Software ID:** 54e3e7bc-9a9b-472f-a469-79f493328672
**Repository:** https://github.com/lkilcommons/igrfpy
**Source Revision:** f904a66956532c2ec3c27f96c98b83dd7537b112
**Extraction Date:** 2026-08-05
**Validation Date:** 2026-08-06
**Validation Status:** PASS

---

## Scope note — read before interpreting the evidence

Two properties of this repository change how its evidence should be read.

1. **It vendors upstream code, and not all of it is built.** The repository contains four Fortran
   sources but `setup.py` compiles only two of them:
   `ext_modules = [igrf11, igrf12]` with `sources=["igrfpy/igrf11.f"]` and
   `sources=["igrfpy/igrf12.f"]` (`setup.py` lines 12-13, 28). `igrfpy/igrf11_cli.f` and
   `igrfpy/igrf12_cli.f` are present but appear in no `Extension`, and nothing in
   `igrfpy/__init__.py` or `igrfpy/test_igrfpy.py` imports them. Their grid, yearly-time-series
   and declination/inclination/horizontal-intensity capabilities are therefore **unreachable dead
   code at this revision** and are deliberately not credited in Field 4. They *were* reachable in
   version 0.1, whose single extension was built from `igrfpy/igrf11.f90` plus the f2py signature
   file `igrfpy/igrf11.pyf` and exposed the `IGRF11(ITYPE,DATE,ALT,IFL,XLTI,...)` grid routine.
   Commit `5226bde` (2020-01-07) split that file and dropped the `.pyf`, and the CLI routines lost
   their build. A future refresh must re-read `ext_modules` before crediting grid or time-series
   functionality.

2. **It is dormant, not archived.** The newest commit is `f904a669` (2020-07-27); the GitHub API
   reports `archived: false`, `pushed_at: 2020-07-27T22:48:36Z`, 0 releases, 0 tags,
   `open_issues_count: 0`, no topics and no homepage. Any classifier or comment in the tree is the
   author's 2020 statement, not a current one, and must be labelled as such rather than read as a
   present-tense fact.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

No submitter identity is recorded. This field names the person who submits metadata through the HSSI
form, and no such person is on record for this entry.

### 2. Persistent Identifier (RECOMMENDED)
**Not found.**

Negative research, so a future agent need not repeat it: the repository has 12 tracked files and
none of them is a `CITATION.cff`, `codemeta.json`, `.zenodo.json` or `CITATION` file. A
case-insensitive sweep of the whole tree for `doi`, `zenodo`, `badge`, `shields.io` and `citation`
returns exactly one hit, and it is spurious: the letters "doi" inside the English word "doing" in
the comment at `igrfpy/__init__.py:137`. `zenodo`, `badge`, `shields.io` and `citation` appear
nowhere in the tree at all, `LICENSE` included. Searching DataCite for `igrfpy` returns 0 records and
searching Zenodo for `igrfpy` returns 0 hits. There is no `igrfpy` project on PyPI, so no packaging
index record exists that might carry a DOI either. The software has never been
archived to a DOI-minting repository. The field is correctly empty.

### 3. Code Repository (MANDATORY)
`https://github.com/lkilcommons/igrfpy`

This is the canonical location, and the URL is live. Confirmed by the git remote
(`origin https://github.com/lkilcommons/igrfpy.git`), by `setup.py`'s
`download_url = "https://github.com/lkilcommons/igrfpy"` (line 23), and by the GitHub API's
`full_name: lkilcommons/igrfpy` with `fork: false`. Default branch is `master`.

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Models and Simulations
- Models and Simulations: Empirical

**`Models and Simulations: Empirical`** is the core classification. igrfpy
evaluates the IGRF, a spherical-harmonic empirical model of Earth's main field whose Gauss
coefficients are determined by fitting observations rather than by solving the physics of the
geodynamo. `igrfpy/igrf12.f:4-6` describes itself as "a synthesis routine for the 12th generation
IGRF as agreed in December 2014 by IAGA Working Group V-MOD... valid 1900.0 to 2020.0 inclusive",
and `igrfpy/igrf11.f` carries the equivalent 11th-generation statement (December 2009, valid 1900.0
to 2015.0).

**`Models and Simulations`** — the parent — is listed because every subcategory requires its parent
alongside it. Earlier metadata for this record carried the `Empirical` leaf with no parent category;
supplying the parent is a structural correction, not a new claim about the software.

**`Coordinate Transforms`** is listed as a user-facing capability, on this evidence:

- `getmainfield`'s `geocentric` keyword (`igrfpy/__init__.py:40`, documented at lines 58-60) lets
  the caller supply either geodetic or geocentric latitudes; it selects `itype` (line 125), and the
  `itype = 1` branch of the Fortran performs the WGS84 spheroid-to-sphere conversion
  (`igrfpy/igrf12.f:31-33` documents the WGS84 change).
- The `altisradius` keyword converts between height above the surface and distance from Earth's
  centre in both directions (`igrfpy/__init__.py:133-140`, using the 6371.2 km IGRF reference
  radius), and validates the result against the model's inner limit (lines 144-146).
- The wrapper converts the Fortran's native north-east-down output into east-north-up
  (`igrfpy/__init__.py:183-185`, `BU.append(-1*bd)`), and the docstring specifies the returned
  frame (lines 74-79). This convention is maintained deliberately, not incidentally: commit
  `07273b2` is "fixed ENU / NEU coordinate system confusion" and `b28cd4c` is "Fixed sign of upward
  component".

**No subcategory is selected under Coordinate Transforms, deliberately.** The six available
children are Heliospheric, Ionospheric, Magnetospheric, Mission-Specific, Planetary and Solar. None
describes a terrestrial geodetic-to-geocentric conversion or a local NED-to-ENU component
reordering, and the top-level category is selectable on its own. `Coordinate Transforms:
Magnetospheric` was the nearest candidate (it covers GEO among GSE/GSM/SM/MAG) and was rejected:
igrfpy never converts between magnetospheric frames; it converts between two geodetic
representations of the same near-ground location.

Considered and rejected, with reasons — recorded so a future agent does not re-propose them:

- **`Models and Simulations: Physics-Based`** — the spherical-harmonic expansion is a solution of
  Laplace's equation, which is a physics argument, but the coefficients come from fitting
  observations and nothing physical is solved at run time. IGRF is a canonical example of the
  `Empirical` category, alongside IRI, MSIS and HWM.
- **`Models and Simulations: Data Guided`** — no observational data drives the model at run time;
  the coefficients are frozen into the compiled extension.
- **`Models and Simulations: Forecasting`** — the routines emit a warning rather than a forecast
  beyond their validity window (`igrfpy/igrf11.f:471`, `if (date.gt.2015.0) write (6,960) date`).
  The secular-variation option is an interpolation coefficient set, not a prediction product.
- **`Data Visualization`** and any of its children — the package contains no plotting code. The only
  plotting in the repository is in the demonstration notebook `igrftest.ipynb`, which calls
  `matplotlib` directly on `getmainfield`'s return values. The library itself has four imports
  (`igrfpy/__init__.py:15-18`) — `numpy`, `datetime`, and the `igrf11` and `igrf12` extension
  modules, i.e. array support, time handling and the model itself — and no plotting dependency among
  them. Note the trap here: `igrfpy/__init__.py:9` contains the line "Basic plotting
  tools" inside the module docstring. That is a stale leftover from DavitPy's `models.igrf`
  docstring (the whole header block is inherited — lines 1-14 also still say
  "**Module**: models.igrf"), and it describes no code in this package. Do not classify from it.
- **`Data Processing and Analysis`** and its children, including `Analysis`,
  `Time Series Analysis`, `Data Access and Retrieval` and `File Format Conversion` — the package
  reads no scientific data. `invartolist` (`igrfpy/__init__.py:20-37`) marshals caller-supplied
  scalars, lists and arrays into flat lists; accepting an array of times produces a time series
  rather than analysing one; and there is no download, query or file-conversion path anywhere (see
  Fields 17-19).
- **`Mission-related`** and **`Servers and Environments`** and their children — no mission ground
  system, pipeline, server, container or HPC component exists in the 12-file tree.

### 5. Related Region (MANDATORY)
- Earth Ionosphere
- Earth Magnetosphere

`Earth Magnetosphere` is listed because the IGRF is the standard internal-field
term in magnetospheric field models and in the field-line mapping and magnetic-coordinate
calculations built on them, so a magnetospheric user is a genuine consumer of this functionality.

`Earth Ionosphere` is listed because evaluating the main field at ionospheric altitudes is what this
particular wrapper exists for: the code was extracted from the Virginia Tech SuperDARN DavitPy
project (`README.md:4`, `igrfpy/__init__.py:1-4`), an ionospheric HF-radar toolkit, and the main
field is the input to the magnetic-coordinate, conjugate-mapping, conductivity and radar-geometry
calculations that community performs. The model imposes no altitude ceiling — the only altitude
constraint in the code is the geocentric lower limit of 3485 km (`igrfpy/__init__.py:145-146`) — so
ionospheric altitudes are fully inside its domain.

Considered and rejected:

- **`Earth Inner Magnetosphere`, `Earth Outer Magnetosphere`, `Earth Magnetotail`,
  `Earth Magnetosheath`** — the field-definition guidance prefers the most specific applicable
  region, but igrfpy implements only the internal field and contains no external-field or
  magnetopause module, so it supports no magnetospheric subregion in particular. The broad
  `Earth Magnetosphere` is the honest scope.
- **`Earth Atmosphere`, `Earth Lower and Middle Atmosphere`, `Earth Thermosphere`** — the model is
  evaluated at 1.6 km elevation in the unit test and at 1 km in the notebook, so the neutral
  atmosphere is inside the valid domain, but the software provides no atmospheric science
  functionality distinct from the same main-field evaluation. Selecting them would describe the
  coordinate domain rather than the supported science. (`Earth Thermosphere` is a plausible future
  addition given the maintainer's ionosphere-thermosphere research area, but nothing in this
  repository supports it.)
- **`Earth Auroral Subregion`** — no auroral-specific capability; the repository contains no
  auroral-zone, boundary or oval logic.

### 6. Authors (MANDATORY)
1. **Liam Kilcommons**
   - Identifier: `https://orcid.org/0000-0002-4980-3045`
   - Affiliation: University of Colorado Boulder — `https://ror.org/02ttsq026`

The ORCID resolves to given name "LIAM", family name "KILCOMMONS". The affiliation ROR resolves to
"University of Colorado Boulder". Kilcommons is the author of all 16 commits (three git identities —
`liam.kilcommons27@gmail.com`, `lkilcommons@users.noreply.github.com`, `liamk@nut.colorado.edu` —
all his), and `setup.py:21` gives `author_email = "liam.kilcommons@colorado.edu"`.

Organizational authors considered and **not** applied. Recorded in full, with the identifier lookups
already done, so a curator who judges the vendored-code authorship worth crediting can act without
repeating the research — and so an agent that meets the same attribution language does not
re-propose it as a discovery:

- **CU SEDA Group** — `setup.py:20` declares `author = "CU SEDA Group"`, i.e. the University of
  Colorado Space Environment Data Analysis group. Not applied because the individual person author
  with a verified ORCID is the more precise and more citable representation of the same
  contribution, and because no ROR record for the group was found — queries for "SEDA" and for
  "Space Environment Data Analysis" return only unrelated organizations. HSSI infers
  organization-ness from a `ror.org` identifier, so an identifierless entry would be stored as a
  person with a blank given name.
- **Virginia Tech SuperDARN Lab / the DavitPy Project** — `README.md:4` states "This code is mostly
  the work of VT SuperDARN's DavitPy Project" and `igrfpy/__init__.py:1` carries
  "Copyright (C) 2012 VT SuperDARN Lab". Not applied as an author because that provenance is
  recorded more precisely as the fork parent in Field 29 and in the description, and because there
  is **no ROR for the lab or for SuperDARN** (a ROR query for "SuperDARN" returns 0 results).
  Virginia Tech's institutional ROR is `https://ror.org/02smfhw86`, but it identifies the
  university, not the lab, so using it would misidentify the contributor.
- **International Association of Geomagnetism and Aeronomy** — ROR `https://ror.org/013ym9476`
  (ROR display name "Association Internationale de Géomagnétisme et d’Aéronomie", with
  "International Association of Geomagnetism and Aeronomy" as an English label and "IAGA" as a
  registered acronym). IAGA authored and maintains the IGRF synthesis Fortran that makes up most of
  this distribution — GitHub's language byte counts on 2026-08-05 were Fortran 119,605,
  Python 13,074, Jupyter Notebook 1,679 — and `igrfpy/README.md:5` (a file vendored from upstream)
  states "This software is maintained by the International Association of Geomagnetism and Aeronomy
  (IAGA)". Not applied because that sentence is about the IGRF model software, not about the igrfpy
  package, and the model's provenance is already carried by Field 29 (the NCEI IGRF distribution)
  and Field 27 (the IGRF-11 and IGRF-12 description papers).

### 7. Software Name (MANDATORY)
`igrfpy`

Confirmed by `setup.py:15` (`name='igrfpy'`), the repository name, the package directory
`igrfpy/`, and SoMEF's `name` / `full_title` / `package_id` results. The all-lower-case spelling is
the maintainer's own and is preserved as written.

### 8. Description (MANDATORY)

> igrfpy provides Python wrappers around the Fortran synthesis routines of the 11th and 12th
> generation International Geomagnetic Reference Field (IGRF), the IAGA standard empirical model of
> Earth's main (internal, core-generated) magnetic field. Its getmainfield function accepts times,
> geographic latitudes, longitudes and altitudes as single values, Python lists, or NumPy arrays,
> and returns the eastward, northward and upward magnetic field components in nanotesla, handling
> the geodetic/geocentric and altitude/radius conversions and the north-east-down to east-north-up
> convention on the caller's behalf. IGRF-12 (valid 1900.0 to 2020.0) is used by default; the 11th
> generation routine (valid 1900.0 to 2015.0) remains available through the igrf11 keyword, and the
> underlying igrf11syn and igrf12syn Fortran routines are also exposed directly for main-field or
> secular-variation output. The spherical harmonic coefficients are compiled into the Fortran
> extension modules, so no coefficient files or network access are required at run time, but
> installation does require a Fortran compiler. This code is mostly the work of VT SuperDARN's
> DavitPy Project and, of course, the original IGRF authors; the contributions here are the
> simplified getmainfield interface, a standalone install script, and pytest unit tests validated
> against the NOAA National Centers for Environmental Information geomagnetic field calculator.

**This description replaced an earlier stored value, and the replacement was not a stylistic
preference.** That earlier value was the following three fragments joined by newlines: "Python
wrappers on the International Geomagnetic Reference Field 11&12 Fortran code" / "International Geomagnetic
Reference Field 11&12 Wrapper" / "This code is mostly the work of VT SuperDARN's
[ DavitPy Project ](https://github.com/vtsuperdarn/davitpy) and of course the original IGRF
authors."

That string is a machine-assembled autofill artifact, not authored prose. Running SoMEF against the
repository reproduces it exactly as three separate `description` results: (1) `README.md:2` and the
GitHub repository blurb, (2) `setup.py:17`'s `description` value, and (3) `README.md:4-5`. The HSSI
autofill cascade concatenates description candidates of similar confidence, and that value was those
three glued together. Consequences that made it defective rather than merely terse:

- Fragments 1 and 2 say the same thing twice, so the 150-200 character preview is a duplicated title
  rather than a description.
- Fragment 3 contains raw Markdown link syntax, complete with the stray spaces inside the brackets,
  in a plain-text field.
- The `README.md:7-10` sentences that describe what the package actually contributes were dropped,
  and the field guidance's core requirement — "what the software does, why to use it, assumptions it
  makes" — is unmet: nothing states that it computes field components, what units or frame it
  returns, which generation is the default, what date range is valid, or that a Fortran compiler is
  needed.

The description preserves every substantive claim of that earlier text, including the DavitPy and
original-IGRF-authors attribution in the maintainer's own words. What it adds is verified either in
the source or against the external records cited elsewhere in this file — the latter covering only
the expansion of the acronym "NCEI" as it appears in `igrfpy/test_igrfpy.py:6` and the
characterisation of the IGRF as the IAGA standard main-field model, which Field 27's papers
establish. From the source: the API surface (`igrfpy/__init__.py:40-79`), the validity windows
(`igrfpy/igrf11.f:5-6`, `igrfpy/igrf12.f:4-6`), the IGRF-12 default (the `igrf11=False` keyword at
`igrfpy/__init__.py:40` with the branch at lines 175-181), the compiled-in coefficients (Field 17),
the compiler requirement (`setup.py:9-13`), and the NCEI-referenced tests
(`igrfpy/test_igrfpy.py:6-8, 99-115`). "11&12" is expanded to "11th and 12th generation" because
the ampersand-digit form is a packaging shorthand rather than prose.

### 9. Concise Description (OPTIONAL)
> Python wrapper around the IAGA Fortran routines for the 11th and 12th generation International
> Geomagnetic Reference Field (IGRF), returning main-field components at given times and locations.

192 characters, inside the field's 200-character limit. That limit is a hard cap rather than a
guideline: the stripped length is checked during validation and an over-length value is rejected
outright, with an error that says so. The contrast worth carrying forward is that this clean
failure is not how every length limit in the form behaves — the `CharField`-backed columns behind
Fields 26-30 are not length-checked during validation, so an over-length value there is not refused
up front but fails at the database write instead. The 128-character name column is the case that
matters in practice; see "Constraint on Fields 26-30" under Field 28.

The concise description exists because the first 200 characters of the earlier stored description
were a duplicated title, which is precisely the case this field is for. It remains useful alongside
the current description because it names the standards body and both model generations in one line.
Note for a future editor: at 192 characters this leaves 8 characters of headroom, so any rewording
must be re-measured rather than eyeballed.

### 10. Publication Date (RECOMMENDED)
`2015-07-10`

Confirmed twice: the GitHub API reports
`created_at: 2015-07-10T19:43:14Z`, and the initial fork commit `1f0dd18` ("Forked DavitPy IGRF") is
dated 2015-07-10 13:47:22 -0600. SoMEF independently reports `date_created 2015-07-10T19:43:14Z`.
This is the date the code was first published in this repository, which is what the field asks for.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** `https://github.com`

The field's own instruction covers this case directly: "If
no DOI has been obtained, indicate the repository host, such as GitHub or GitLab." No DOI exists
(Field 2), and GitHub is where the software is published. A URL is used rather than a ROR because
GitHub is a commercial platform with no ROR record, and the field explicitly permits a URL when no
ROR exists. "GitHub" is the company's full name, so no acronym expansion applies.

### 12. Version (RECOMMENDED)
- **Version Number:** `0.2`
- **Version Date:** deliberately absent — see below
- **Version Description:** Switched the default to the 12th generation IGRF, with IGRF-11 still
  reachable through the igrf11 keyword; split the IGRF synthesis routines into separate Fortran
  sources and replaced the hand-written f2py signature file with inline intent declarations,
  building igrf11 and igrf12 as two extension modules instead of one; and added pytest unit tests
  checked against the NOAA National Centers for Environmental Information geomagnetic field
  calculator. Later work under the same version number added docstrings and split getmainfield into
  two functions, updated the README, removed unused files, and made the Python code Python 3
  compatible.
- **Version PID:** Not found — no DOI exists for any version (Field 2).

**The version number is `0.2`, and it replaced an earlier empty value.** `setup.py:16` declares
`version = "0.2"` at this
revision. That is the only place the project declares a version for itself, and it is authoritative
in the sense that matters to a user: installing from source yields a distribution named igrfpy 0.2.
(The other `version` strings in the tree belong to other software and must not be mistaken for
igrfpy's: `igrfpy/test_igrfpy.py:52` records the NCEI calculator's `"version": "0.5.1.7"`, and
`igrftest.ipynb` records the notebook format version and the kernel's Python version.)
An empty version string carries no information, and it was the cause of the `"igrfpy - "` string the
HSSI view renders for such a record (the view composes `<software name> - <number>`). That rendered
prefix is a presentation transform and is never stored data — do not copy it into this field.

**The version description is deliberately plain text, with no markdown.**
`SoftwareVersion.description` carries no markup, so inline-code backticks would render literally as
backtick characters — the same defect that made the earlier description value in Field 8 unusable.
Identifier-like words in it (igrf11, intent, igrf12, getmainfield) therefore appear as bare words. The
same applies to Description and Concise Description. Do not add markdown to any of the three.

Negative research supporting this choice, recorded so it is not redone: `git tag -l` is empty and
the GitHub tags API reports no tags; the GitHub releases API reports no releases (SoMEF's
`download_url` points at the empty releases page); and there is no `igrfpy` project on PyPI, so no
published sdist or wheel exists. There is therefore **no release artifact** whose
version could contradict `setup.py`, and equally none that could corroborate it.

Rejected alternatives:

- **Leaving the version empty.** An empty string is not a statement that the version is unknown, it
  is missing data, and the repository does declare a version. The absence of tags means there is no
  *release*, not that there is no *version*.
- **Any semantic version derived from commit history** (e.g. "0.2.1" for the commits after the bump,
  or a date-based version). Rejected outright: inventing a version identifier the project never used
  would be fabrication.
- **Treating the repository's age or commit count as a version.** Rejected for the same reason.
- **Borrowing an IGRF generation number (11, 12, 13 or 14) as the package version.** Rejected
  emphatically. The generation numbers identify the *scientific model* this package wraps, not the
  wrapper's release. Doing so would also be self-contradictory here, since one 0.2 distribution
  ships two generations. This trap is specific to IGRF wrappers and is the most likely way for a
  future agent to corrupt this field.

**Why the version date is absent rather than guessed.** `0.2` first appears in commit `5226bde`
(2020-01-07), which changed `version = "0.1"` to `version = "0.2"` — but `0.2` is not a frozen
snapshot. Six further commits landed under the same version number — four substantive
(`70d22d6`, `8908e94`, `887e859`, `f904a669`) plus two merges — the last being `f904a669`
(2020-07-27), which changed `igrfpy/__init__.py`. So no single date identifies "when 0.2 was
released": 2020-01-07 is when the label was created, 2020-07-27 is when the code carrying that label
last changed, and neither is a release event because no release exists. Recording either would
assert a release that never happened. Both candidate dates are written down here so a future agent
can see they were considered and why neither was chosen.

The version description is drawn from `5226bde`'s own commit message and diff (it renamed
`igrfpy/igrf11.f90` to `igrfpy/igrf11.f`, deleted `igrfpy/igrf11.pyf`, added `igrfpy/igrf12.f`,
`igrfpy/igrf11_cli.f`, `igrfpy/igrf12_cli.f` and `igrfpy/test_igrfpy.py`, and rewrote `setup.py`'s
`ext_modules`), plus the messages of the four substantive commits that followed it — `70d22d6`
("Added docstrings and refactored getmainfield into two functions"), `8908e94` ("Update README.md"),
`887e859` ("Remove unnessecary files") and `f904a669` ("Python 3 compatability (print statments)").
It summarises evidenced changes; it is not a reconstruction of release notes the project never
wrote. Note for accuracy that `b09ee7d` ("Added silent option", 2017-01-06) and `b28cd4c` ("Fixed
sign of upward component, changed getmainfield to deal with multiple or single inputs", 2015-07-11)
are **0.1** work — `setup.py` still read `version = "0.1"` at both — so the `silent` keyword and the
scalar/list/array input handling must not be credited to 0.2.

### 13. Programming Language (RECOMMENDED)
- Fortran77
- Python 3.x

Note the vocabulary's exact spelling: `Fortran77`, with no space. Values are matched literally, so a
one-character variant is rejected.

**The Fortran value is `Fortran77`. It replaced `Fortran90`, which the compiled sources do not bear
out.** The evidence that the Fortran in this repository is fixed-form FORTRAN 77 rather than
Fortran 90:

- All four `.f` sources are fixed-form, and form is a separate question from dialect. The two
  compiled sources carry 394 (`igrfpy/igrf11.f`) and 426 (`igrfpy/igrf12.f`) column-6 continuation
  lines; the two uncompiled ones carry 30 and 31, with 101 and 34 column-1 `c`/`C` comment cards
  respectively. Fixed form therefore does not by itself settle the dialect — the point below about
  `::` does.
- `igrfpy/igrf12.f:42` uses the FORTRAN 77 declaration style
  `implicit double precision (a-h,o-z)`.
- `setup.py:12-13` compiles both sources with `extra_f77_compile_args=["-w"]` — the build itself
  names the dialect.
- Neither compiled source contains free-form code, a Fortran-90 module or interface block, an
  `allocatable`, or even one `::` attribute-declaration separator.

That last point is scoped to the two compiled sources deliberately, and the scoping is itself
evidence. The uncompiled files are **not** uniformly F77: `igrfpy/igrf11_cli.f:83-85` and
`igrfpy/igrf12_cli.f:85-87` use genuine Fortran-90 attribute-style declarations
(`real*8,DIMENSION(totpts) :: aLat,aLon` and its two siblings in each file), and each file also
carries two `Cf2py ... ::` directive lines. Every `::` in the Fortran sources is in those two files;
there is none in `igrfpy/igrf11.f` or `igrfpy/igrf12.f`. (The other `::` occurrences in the tree are
the Trove classifier strings at `setup.py:31-36`, an unrelated use of the token.) That strengthens
the `Fortran77` choice rather
than weakening it: the Fortran-90 syntax lives exclusively in the sources `setup.py` does not build
(Scope note), so it is further evidence that those files are unreached dead code, not evidence about
the dialect that actually ships.

The one Fortran-90-era token in the compiled sources is a single inline `!` comment,
`igrfpy/igrf12.f:43` (`real date ! LMK don't know if needed?`); the `intent(in)` / `intent(out)`
lines at `igrfpy/igrf12.f:44-45` are f2py directives, which are not standard Fortran of any
generation. Neither makes the body of the code Fortran 90.

Where `Fortran90` probably came from, since knowing this prevents the value being reinstated by
accident: before commit `5226bde` the file was named **`igrfpy/igrf11.f90`**. That
extension was a misnomer even then — the version of the file at the initial fork (`1f0dd18`) has 424
column-6 continuation lines and 174 column-1 comment cards (87 written `c`, 87 written `C`) in 1,165
lines, i.e. it was fixed-form FORTRAN 77 under a `.f90` name — and the accompanying
`igrfpy/igrf11.pyf` opened with the f2py mode line `!    -*- f90 -*-`. Anything keying off the old
filename, or a submitter picking a middle-of-the-road "Fortran" from the dropdown, would land on
`Fortran90`. SoMEF reports only the unqualified
`Fortran`, so it is not the source of the specific value.

Keeping both `Fortran77` and `Fortran90` was considered and rejected. That would have been imprecise
rather than outright false, but HSSI matches these values literally, so retaining `Fortran90` would
return this package to a user searching for a dialect it does not contain, and would leave in place a
value the compiled sources do not bear out. A user searching `Fortran77` should find
this package; a user searching `Fortran90` should not.

**The Python value is `Python 3.x`.** The final commit `f904a669` exists specifically to provide
"Python 3 compatability (print statments)". `Python 2.x` was considered and rejected: this is a
Python-2-era codebase (`igrftest.ipynb` still records `kernelspec` `display_name: Python 2`,
`name: python2` and `language_info.version: 2.7.9`) and the code at HEAD would probably still run
under Python 2, but the maintainer's
last action was to move it to Python 3, `setup.py`'s classifiers name only the unversioned
`Programming Language :: Python`, and there is no `python_requires`. Claiming Python 2 support would
assert a runtime the project deliberately moved away from.

### 14. Reference Publication (RECOMMENDED)
**Not found.**

No publication describes igrfpy: there is no JOSS paper, no `CITATION.cff`, no "how to cite"
section, and no DOI of any kind associated with the package (Field 2).

Considered and rejected: putting the IGRF-12 description paper
(`https://doi.org/10.1186/s40623-015-0228-9`) here. It describes the IAGA model that this package
wraps, not the wrapper, and this field is single-valued while the package ships two generations, so
selecting one would silently misrepresent the other. Both model papers are recorded in Field 27
instead, where multiple entries are allowed and the relationship can be stated rather than implied.

### 15. License (RECOMMENDED)
- **License:** `GNU General Public License v3.0 or later`
- **License URI:** `https://spdx.org/licenses/GPL-3.0-or-later.html`

The `LICENSE` file is the full GNU General Public License
text, "Version 3, 29 June 2007". The GitHub license API reports
`{key: gpl-3.0, spdx_id: GPL-3.0, name: GNU General Public License v3.0}`. `setup.py:34` classifies
it `License :: OSI Approved :: GNU General Public License (GPL)`, and `setup.py:3-4` explains the
provenance: "Code is still under GPLv3 as per superDARN licensing / CU SEDA has broken it out from
DavitPy for solo usage".

**Vocabulary limitation worth recording.** The repository's licence is best described by SPDX
`GPL-3.0-only` — the bare GPL-3.0 text with no source file electing the "or (at your option) any
later version" option, which is how GitHub detects it. The phrase does occur in the tree, but only
inside the GPL text itself: in its "Revised Versions of this License" section (`LICENSE:572-587`) and
in the recommended notice of its "How to Apply These Terms to Your New Programs" template
(`LICENSE:640`). Neither is an election by this project; no `.py` or `.f` file carries that notice.

The live `License` vocabulary has 11 rows and its only GPLv3 row is
`GNU General Public License v3.0 or later`; there is no `...v3.0 only` row, and the only other GPL
row is `GNU General Public Licenses (GPL version 2)`. So the selected value is the
closest available row and must **not** be read as evidence that the project elected the "or later"
option. `Other` was rejected as strictly less informative than a row that names GPL version 3. If a
`GPL-3.0-only` row is ever added to the vocabulary, this field should move to it. The URI is copied
from the selected row rather than composed, so it will match on comparison.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- igrf
- igrf11
- igrf12
- geomagnetic field
- magnetic field models
- empirical model
- secular variation
- spherical harmonics

Keywords is the one open vocabulary in the form, which means an unrecognised keyword is created
rather than rejected — so the existing vocabulary was checked first, to reuse rows rather than mint
near-duplicates. `igrf`, `igrf12`, `geomagnetic field`, `magnetic field models` and `empirical model`
already existed. `igrf11`, `secular variation` and `spherical harmonics` did not, and each is
justified individually below rather than added casually, because a new keyword row is permanent:
`igrf11` is the missing
sibling of the existing `igrf12` and `igrf13` rows and names the generation this package uniquely
offers among the three; `secular variation` is the standard term for the `isv = 1` output the
exposed Fortran routines provide (`igrfpy/__init__.py:89-91` documents "isv = 1 if secular variation
values are required"); and `spherical harmonics` names the mathematical form of the model, whose
degree-13 coefficient arrays are visible in `igrfpy/igrf12.f:47-52`.

Excluded on purpose: `fortran` and `python` (both exist as rows) — the field asks for science
keywords "not supported by other metadata fields", and the languages are Field 13. `geomagnetism`
and `earth magnetic field` (both exist as rows) — near-duplicates of the selected
`geomagnetic field`, and attaching redundant synonyms degrades the vocabulary. `main field` and
`iaga` — would be new rows; the first is ambiguous outside geomagnetism and the second is
organizational rather than scientific.

### 17. Data Sources (OPTIONAL)
**Not found — correctly empty.**

This is a substantive finding rather than a gap, and it is the key fact about how igrfpy works.
**The IGRF coefficients are compiled into the Fortran extension modules; nothing is read at run
time.** Verified directly:

- `igrfpy/igrf11.f` contains 24 `data` statements and `igrfpy/igrf12.f` contains 25, holding the
  Gauss coefficients as Fortran literals with their epochs in the line-trailing comment column
  (`data g0/ -31543.,-2298., 5922., ... 1900`).
- A grep for uncommented `OPEN`, `READ`, `INQUIRE` or `CLOSE` statements across all four Fortran
  sources returns **no matches** — every such statement in `igrfpy/igrf11_cli.f` and
  `igrfpy/igrf12_cli.f` is commented out with a leading `!` (for example `igrf11_cli.f:120`,
  `!       OPEN (UNIT = IU,FILE = FNM,STATUS = 'NEW')`, and `igrf11_cli.f:132`,
  `!      READ (5,*) ITYPE`), and those two files are not compiled at all (see the Scope note).
- Neither `igrfpy/__init__.py` nor `igrfpy/test_igrfpy.py` opens a file or performs any network
  access, and `setup.py:29` declares `install_requires=[]`. A tree-wide search for `urllib`,
  `requests`, `urlopen`, `http.client`, `socket`, `ftplib`, `wget` and `curl` returns no matches at
  all, so there is no retrieval path to overlook.
- The repository's complete tracked file list is 12 files, none of which is a coefficient table:
  `.gitignore`, `LICENSE`, `README.md`, `igrfpy/README.md`, `igrfpy/__init__.py`,
  `igrfpy/igrf11.f`, `igrfpy/igrf11_cli.f`, `igrfpy/igrf12.f`, `igrfpy/igrf12_cli.f`,
  `igrfpy/test_igrfpy.py`, `igrftest.ipynb`, `setup.py`. There is no `igrf11coeffs.txt` or
  `igrf12coeffs.txt` in the tree and no code path that would read one.

Every row in the 17-value `DataInput` vocabulary names a data archive, service or access protocol —
AMDA, CDAWeb, das2, FTP/FTPS Directories, GFZ, HAPI, HTTP/HTTPS Directories, Madrigal,
Observatory/Mission-specific, OMNIWeb, Other, S3/Cloud-aware, SSCWeb, TAP,
`The Virtual Solar Observatory.`, VirES, WDC. igrfpy consumes none of them, and even `Other` would
be false, because there is no data input at all. Empty is the correct value and should stay empty
unless the package gains a reader.

### 18. Input File Formats (RECOMMENDED)
**Not found — correctly empty.**

The package has no file input of any kind (see Field 17). `getmainfield`'s inputs are in-memory
Python scalars, lists and NumPy arrays (`igrfpy/__init__.py:40-46`), and the Fortran routines take
scalar arguments. None of the 11 `FileFormat` rows (ascii, CDF, csv, FITS, HDF5, IDL.sav,
ISTP-Compliant, JSON, netCDF3/4, Other, Zarr) applies, so the field is correctly empty.

### 19. Output File Formats (RECOMMENDED)
**Not found — correctly empty.**

`getmainfield` returns three Python lists of floats (`igrfpy/__init__.py:74-79, 187`) and the
Fortran routines return scalars through their argument list; nothing is written to disk. The only
`WRITE` statements that target a file unit are in the uncompiled `igrfpy/igrf11_cli.f` and
`igrfpy/igrf12_cli.f` (for example `igrf12_cli.f:363`, `WRITE(IU,958) DATE,ALT,TYPE`) and are
unreachable at this revision — do not classify an output format from them. Both compiled sources do
contain `WRITE` statements — four in total, at `igrfpy/igrf11.f:471` and `:615` and
`igrfpy/igrf12.f:505` and `:649` — but each writes to unit 6 (standard output) to emit a date-range
warning, and no `WRITE` in either compiled source targets any other unit. Standard output is not a
file format, so the field is correctly empty.

### 20. Operating System (RECOMMENDED)
**Not found — a deliberate omission, not an oversight.**

The project makes no platform claim and nothing in the repository establishes one: there is no CI
configuration (the 12-file tree contains no `.github/` directory and no `.travis.yml`), no
`Operating System ::` classifier in `setup.py:30-37`, no installation instructions in either README,
and no published wheel or sdist to inspect (there is no PyPI release). Because `setup.py` builds
Fortran extensions through `numpy.distutils`, what the package installs on is determined by the user's Fortran
toolchain rather than declared by the project.

The only platform-adjacent evidence is `extra_f77_compile_args=["-w"]` (`setup.py:12-13`), a
GCC-style flag that implies a GCC-family Fortran compiler — but gfortran is available on Linux,
macOS and Windows via MinGW, so this narrows the *compiler* and not the *operating system*.

Documented candidate, not applied: `Operating System Independent`. The source contains no
platform-specific code, no path handling and no conditional compilation, so a case can be made that
it is portable at source level. It is not applied because a compiled extension's portability is a
property of the toolchain the user supplies, and asserting cross-platform support that was never
tested or claimed would be fabrication. A user who judges source-level portability sufficient can
add it. A future agent should not treat this field's emptiness as an unexamined gap.

### 21. CPU Architecture (RECOMMENDED)
**Not found — a deliberate omission, on the same reasoning as Field 20.**

Nothing in the repository names an architecture: no assembly, no compiler intrinsics, no endianness
assumptions, no architecture-specific build flags, no CI matrix, and no distributed binary. The code
is compiled from portable source on the target machine.

Documented candidate, not applied: `CPU Independent`, for the source-level portability argument
above. Not applied for the same reason: the project never made the claim and it was never tested.
`x86-64` and `Apple Silicon arm64` were also considered and rejected — they are the architectures
the maintainer plausibly used, but "plausibly used" is not evidence, and the repository contains
none.

### 22. Related Phenomena (OPTIONAL)
**Not found — correctly empty.**

`Phenomena` is a closed 7-row vocabulary: Coronal Heating, Coronal Mass Ejections, Geomagnetic
Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission. **No row describes Earth's internal
or main magnetic field**, which is the phenomenon igrfpy addresses, and the API rejects anything not
in the list.

`Geomagnetic Storms` was considered and rejected, because it is the one row a future agent is likely
to reach for. igrfpy models only the quiet internal field: it has no external-field, ring-current,
disturbance-index or storm-time capability, and the main field is the *baseline* one subtracts to
study storms rather than a storm product. Selecting it would return igrfpy to users searching for
storm software, which it is not. Terms that do describe this software (`geomagnetic field`,
`secular variation`, `spherical harmonics`) are in Keywords, the open vocabulary the field guidance
directs such terms to.

### 23. Development Status (RECOMMENDED)
`Inactive`

The repostatus.org definition of `Inactive` is "reached a stable, usable state but is no longer being
actively developed; support/maintenance will be provided as time allows", and both halves are
evidenced:

- *Stable and usable:* version 0.2 with a working public API, a pytest suite that validates the
  wrapper and the Fortran against independently retrieved NOAA NCEI calculator output to 0.5 nT
  (`igrfpy/test_igrfpy.py:99-115, 138-162`), and a demonstration notebook with saved output.
- *No longer actively developed:* the newest commit is 2020-07-27, the whole history is 16 commits,
  and activity came in four short bursts (2015-07, 2017-01, 2020-01, 2020-07).

Every rejected alternative, with its reason:

- **`Active`** — there has been no commit since July 2020. Note explicitly that `archived: false` in
  the GitHub API does **not** mean active: an unarchived repository is simply one nobody closed, and
  0 open issues on a repository with 0 stars and 1 fork is an absence of traffic rather than
  evidence of responsiveness.
- **`Abandoned`** ("initial development has started, but there has not yet been a stable, usable
  release; the project has been abandoned") — rejected on its first clause. The absence of git tags
  and of a PyPI record means there is no *release artifact*, not that the software never reached a
  usable state; it demonstrably did.
- **`Unsupported`** ("reached a stable, usable state but the authors have ceased all work; a new
  maintainer is desired") — the closest rival, rejected for lack of evidence. It requires an
  authorial statement of cessation or a request for a maintainer, and there is none: no deprecation
  notice, no archive flag, no README banner, no successor pointer. `Inactive` is the value that does
  not put words in the author's mouth. If a future refresh finds such a statement, `Unsupported`
  becomes correct.
- **`Suspended`** — requires a stated intent to resume; none exists.
- **`WIP`** and **`Concept`** — contradicted by the working, tested 0.2 API.
- **`Moved`** — no successor project is named anywhere; the code has not relocated.

On the `Development Status :: 4 - Beta` classifier at `setup.py:31`: it is not the source of this
value and does not map onto one. It is the author's own maturity assessment as of 2020, whereas the
repostatus vocabulary describes *activity*, and "Beta" has no repostatus counterpart. Treating a
six-year-old Beta classifier as a current status would be a category error.

### 24. Documentation (RECOMMENDED)
`https://github.com/lkilcommons/igrfpy/blob/master/README.md`

The URL is live. There is no documentation site, no `docs/` directory, no `.readthedocs.yml`, and no
wiki content (the GitHub wiki is enabled but has none). The documentation for this package
consists of `README.md`, the vendored upstream note in `igrfpy/README.md`, the `getmainfield`
docstring (`igrfpy/__init__.py:41-123`, which reproduces the upstream Fortran's input/output
description in full), and the `igrftest.ipynb` usage example.

`README.md` is chosen as the most specific real documentation. Rejected alternative: the bare
repository URL, which the field permits when documentation and access URL coincide — it is
indistinguishable from Field 3 and points a reader at the file list rather than at the prose. A
`master`-branch blob URL is normally fragile, but this repository is dormant and `master` is its
default branch, so the risk is minimal. Known limitation to record honestly: neither README contains
installation instructions, which the field asks for; the closest thing is `README.md:8`'s mention of
"a seperate install script". No better URL exists.

### 25. Funder (OPTIONAL)
**Not found.**

The repository contains no funding statement, acknowledgement section, grant number, or
`FUNDING.yml`. `setup.py:20` names the "CU SEDA Group" as author, which is an organizational unit
rather than a funder. There is no DOI record (Field 2) whose `fundingReferences` could supply one.
Deliberately left empty rather than guessed: work of this kind at the University of Colorado is
commonly NASA- or NSF-supported, but inferring an agency with no evidence would be fabrication.

### 26. Award Title (OPTIONAL)
**Not found — correctly empty.**

There is no award to record, which is consistent with the absence of any funding information in the
repository (Field 25).

This field previously carried one entry whose name and identifier were both empty strings and whose
funder was null. That was **malformed absence, not an award title**: it conveyed nothing, and where
rendered it presented igrfpy as holding a nameless award. Dropping the association is the reason the
field now reads as genuinely empty rather than as an unnamed award.

Only the association with this record was dropped. The underlying award entry is shared with other
software entries and was deliberately left intact — a future agent should not propose deleting or
renaming it on this record's behalf, because its condition is a catalogue-wide concern outside this
record's scope.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
1. `https://doi.org/10.1186/s40623-015-0228-9` — Thebault, E., et al. (2015). International
   Geomagnetic Reference Field: the 12th generation. *Earth, Planets and Space*, 67:79.
2. `https://doi.org/10.1111/j.1365-246X.2010.04804.x` — Finlay, C. C., et al. (2010). International
   Geomagnetic Reference Field: the eleventh generation. *Geophysical Journal International*,
   183(3), 1216-1230.

Crossref confirms the titles, journals and publication dates quoted above for both DOIs.

These are the authoritative descriptions of the two model generations this package implements, and
they are what `README.md:5`'s credit to "the original IGRF authors" points at. They are the
citations a user of igrfpy's output owes: the wrapper adds an interface, but the science is the IAGA
model. The pairing is exact rather than approximate — `igrfpy/igrf12.f:4-5` cites the model "as
agreed in December 2014 by IAGA Working Group V-MOD" (the 12th generation, Thebault et al. 2015) and
`igrfpy/igrf11.f` the December 2009 agreement (the 11th generation, Finlay et al. 2010) — so both
entries correspond to compiled, reachable code.

Interpretation noted for the record: the field's wording is "publications that describe, cite, or
use the software". These papers describe the *model* rather than this Python package, so the fit is
by extension rather than literal. They are applied because most of what this distribution contains
is the IAGA synthesis code these papers document (Fortran 119,605 bytes against Python 13,074 on
2026-08-05), because no other field in the form is a better home for a model-description reference
(Field 14 was rejected above and Field 28 is for datasets), and because
a user who finds igrfpy through HSSI needs them. The alternative — leaving the field empty and losing
the references entirely — was judged worse. Field 14 was also considered and rejected for these
DOIs (see that field).

### 28. Related Datasets (OPTIONAL)
1. `https://www.ngdc.noaa.gov/IAGA/vmod/coeffs/igrf12coeffs.txt`
2. `https://www.ngdc.noaa.gov/IAGA/vmod/coeffs/igrf11coeffs.txt`

**The value of each entry is the bare URL above, byte-exact.** This field carries a URL and nothing
else: an entry is validated as a URL, and the stored human-readable name is derived from that URL
rather than supplied alongside it (see "Constraint on Fields 26-30" below). A citation string is not
a URL and cannot be stored here.

**What those two URLs identify** — recorded in the citation form the field guidance asks for when no
DOI is available, as documentation for a human reader rather than as a value to be stored:

- International Association of Geomagnetism and Aeronomy, Working Group V-MOD (2014). 12th
  Generation International Geomagnetic Reference Field Schmidt semi-normalised spherical harmonic
  coefficients, degree n=1,13 [Data set]. NOAA National Centers for Environmental Information.
  https://www.ngdc.noaa.gov/IAGA/vmod/coeffs/igrf12coeffs.txt
- International Association of Geomagnetism and Aeronomy, Working Group V-MOD (2009). 11th
  Generation International Geomagnetic Reference Field Schmidt semi-normalised spherical harmonic
  coefficients, degree n=1,13 [Data set]. NOAA National Centers for Environmental Information.
  https://www.ngdc.noaa.gov/IAGA/vmod/coeffs/igrf11coeffs.txt

How each citation element was derived, so a future agent can check it rather than trust it: the
**titles** are the first header line of each file itself (`# 12th Generation International
Geomagnetic Reference Field Schmidt semi-normalised spherical harmonic coefficients, degree n=1,13`,
and the same line with "11th" in the other file); the **years** are the adoption dates recorded in
the vendored Fortran this package compiles — December 2014 for the 12th generation
(`igrfpy/igrf12.f:4-5`) and December 2009 for the 11th (`igrfpy/igrf11.f:4-5`) — rather than the
years of the describing papers, which are 2015 and 2010 and are cited in Field 27; the **responsible
body** is IAGA Working Group V-MOD, named in those same source comments; and the **publisher** is
NOAA's National Centers for Environmental Information, the current identity of the former National
Geophysical Data Center, whose legacy `ngdc.noaa.gov` host still serves both files.

**Constraint on Fields 26-30 (durable — it shapes what these fields can ever hold).** Every entry in
Related Publications, Related Datasets, Related Software and Interoperable Software, and the
identifier side of Award Title, is stored as a URL, and the accompanying name is set from that same
URL rather than being separately settable. Two consequences that outlive this refresh: descriptive
text — a citation, a title, a short label — cannot be attached to an entry, so any such text belongs
in a dossier note like the one above and nowhere else; and because the name column is derived from
the URL and is narrower than the URL column (a 128-character ceiling against 200), an entry whose URL
exceeds 128 characters cannot be stored at all even though it would pass URL validation. No URL
proposed anywhere in this record comes close to that ceiling — the longest is the 76-character NCEI
IGRF product page in Field 29 — so nothing here needs shortening, but a future refresh that adds a
long archive or query URL should check the length before proposing it.

**These two entries belong to this field, and were previously recorded under Interoperable Software
(Field 30).** Both URLs are live and serve the coefficient tables directly, without redirect.

Why they do not belong in Field 30. That field is for other high-level heliophysics or science
**software** with which a demonstrated exchange exists — a shared data model, an adapter API, a
plugin relationship, a cross-language bridge. These two URLs are **plain-text data files, not
software**, so the field's subject matter excludes them; and there is no exchange of any kind,
because igrfpy never reads them. The coefficients in these tables are transcribed into the Fortran
`data` statements at build time (Field 17), which makes the relationship "the authoritative
published form of the numbers this package has hard-coded" — a data relationship.

Why here rather than nowhere. Field 28 is for datasets the software provides functionality for, and
evaluating these coefficient sets is the entirety of what igrfpy does. The links also answer the
question a careful user of a wrapper like this one actually asks: which coefficient set is baked in,
and where is the authoritative version to check it against. The field's fill guidance prefers a DOI
and permits a citation with a permanent link when no DOI exists; a DataCite search for
International Geomagnetic Reference Field datasets surfaced no DOI for the IGRF-11 or IGRF-12
coefficient tables, so the NOAA-hosted URLs are the authoritative form available. The publications
describing these datasets are recorded in Field 27, which satisfies the guidance's intent.

Alternative considered and rejected: omitting both entries as belonging to no field. That would have
discarded links the previous submitter deliberately recorded and that a user needs, purely because
they had been filed under the wrong field.

Not moved to Field 17 (Data Sources): that field describes sources the software **reads at run
time**, and igrfpy reads nothing (Field 17).

### 29. Related Software (OPTIONAL)
1. `https://github.com/vtsuperdarn/davitpy` — the DavitPy project, which this code was forked from.
2. `https://www.ncei.noaa.gov/products/international-geomagnetic-reference-field` — the NOAA
   National Centers for Environmental Information IGRF product page, the distribution point for the
   upstream IAGA IGRF model and its Fortran synthesis programs.
3. `https://github.com/space-physics/igrf` — a maintained, PyHC-registered Python interface to the
   IGRF Fortran, performing the same task for newer model generations.

All three URLs are live.

**DavitPy is the best-evidenced relationship in this record.** The field explicitly
asks for "software this work was forked from", and three independent places in the tree say so:
`README.md:4` ("This code is mostly the work of VT SuperDARN's DavitPy Project"),
`igrfpy/__init__.py:1-4` ("Copyright (C) 2012 VT SuperDARN Lab ... Broken out from DavitPy by
University of Colorado SEDA Group in 2014"), and `setup.py:3-4` ("CU SEDA has broken it out from
DavitPy for solo usage"). The second commit in the history, `1f0dd18`, is titled "Forked DavitPy
IGRF" — it is the commit that brought the code in, immediately after `77e424d` "Initial commit".
Note that GitHub reports
`fork: false` for this repository — the extraction was done by copying files, not by using GitHub's
fork mechanism, so repository metadata alone would miss this relationship entirely. That is worth
remembering on any future refresh.

**The NCEI IGRF product page** is listed with its justification made explicit. It is not a
similar-purpose tool; it is where the upstream IGRF model software — including
the IAGA-published `igrfXXsyn` synthesis programs that `igrfpy/igrf11.f` and `igrfpy/igrf12.f` are
copies of — is distributed. That upstream software has no code repository and no DOI, and the field
directs that when there is no public repository one should "enter link where users can find more
information", so the product page is the correct available link. `igrfpy/README.md:7` points to the
older IAGA V-MOD page `http://www.ngdc.noaa.gov/IAGA/vmod/igrf.html`, which still resolves but only
after a redirect to its HTTPS form; the NCEI product page is the current, non-redirecting entry point
and is preferred to it.

**`https://github.com/space-physics/igrf`** is listed as software performing similar tasks — the
field's primary definition. It is a Python interface to the IGRF Fortran, registered in PyHC's
unevaluated-projects list under the name "IGRF-13", and it covers generations that igrfpy does not.
A user who reaches igrfpy and needs a generation later than IGRF-12, or a maintained package, needs
exactly this pointer, and igrfpy's dormancy (Field 23) makes the pointer more valuable rather than
less.

A boundary for this list, so it does not grow without evidence: other Python IGRF implementations
exist (pyIGRF and ppigrf among them) and were considered and not applied, because they are neither
referenced by this repository nor registered in PyHC, so admitting them would start an open-ended
catalogue of every package that computes the same model. The rule applied here is that a Field 29
similar-purpose entry must be either named in this repository or PyHC-registered.

Also considered: cross-linking the separate HSSI record for the IGRF-14 model. Not applied, because
igrfpy is a distinct package with no relationship to it beyond implementing an earlier generation of
the same model, and no stable public link for that record has been verified.
**igrfpy supports IGRF-11 and IGRF-12 only**; it must never inherit metadata from an IGRF-13 or
IGRF-14 record.

Excluded dependencies, with reasons:

- **numpy** — imported by `igrfpy/__init__.py:15` and used as `numpy.distutils` in `setup.py:9`.
  Excluded: generic scientific-Python infrastructure, true of nearly every package in HSSI, and
  therefore carrying no information about this one.
- **pytest** — `igrfpy/test_igrfpy.py:1`. Excluded: generic test tooling.
- **matplotlib** — used only in the demonstration notebook, never by the package. Excluded as
  generic plotting infrastructure even setting the demo-only usage aside.
- **f2py** — part of numpy, and a build tool rather than related software.

Negative research on IGRF generation scope, recorded because it is the likeliest error a future
agent could make here: a case-insensitive sweep of the entire working tree **and** the full git
history for `igrf13`, `igrf14`, `13th`, `14th` and `thirteenth` returns **no matches**. igrfpy
implements the 11th and 12th generations only. Neither the existence of newer generations nor the
presence of a separate IGRF-14 entry in HSSI is evidence that this package supports them.

### 30. Interoperable Software (OPTIONAL)
**Not found — correctly empty.**

Two entries were previously recorded here:
`https://www.ngdc.noaa.gov/IAGA/vmod/coeffs/igrf12coeffs.txt` and
`https://www.ngdc.noaa.gov/IAGA/vmod/coeffs/igrf11coeffs.txt`. They belong to Field 28 (Related
Datasets) and are recorded there with the full reasoning — **relocated, not discarded.** They do not
belong here because they are data files rather than software, and igrfpy never reads them, so neither
the subject matter nor the demonstrated-exchange requirement of this field is met.

**The field is genuinely empty, and that is correct.** igrfpy demonstrates no interoperation with any
other package:

- `setup.py:29` declares `install_requires=[]` — it has no declared dependencies at all.
- There is no adapter or converter API, no `to_*`/`from_*` function, no plugin or entry-point
  registration, no shared data model, and no bridge to a named domain tool. The package defines
  exactly two functions, `invartolist` and `getmainfield` (`igrfpy/__init__.py:20, 40`), and
  re-exports the two f2py-generated extension modules; `invartolist` is an input-marshalling
  helper, not an exchange point.
- The return type is three plain Python lists of floats (`igrfpy/__init__.py:160, 183-185, 187`) —
  the absence of a structured interchange type (an `xarray.Dataset`, an `astropy` quantity, a tplot
  variable) is precisely what makes an interoperability claim unavailable here.
- The only external tool whose output appears anywhere in the package is the NOAA NCEI geomagnetic
  calculator, and it appears as hard-coded expected values pasted into a test file
  (`igrfpy/test_igrfpy.py:6-53`, "retrieved Jan 7, 2020"). That is a validation reference, not a
  runtime interoperation; the test performs no call to it. (The other external things the repository
  names — DavitPy and the IAGA/NOAA IGRF pages — are provenance, recorded in Field 29.)
- Sharing a Python runtime with numpy is not interoperability, and neither is membership in an
  ecosystem. igrfpy is not a PyHC package in any case: all three PyHC registry files — core,
  community and unevaluated — were read in full, and neither the name `igrfpy` nor the repository
  owner `lkilcommons` appears in any of them.

### 31. Related Instruments (OPTIONAL)
**Not found — correctly empty, on positive evidence rather than a failed lookup.**

igrfpy is instrument-agnostic, and there is nothing to resolve against the SPASE vocabulary. A sweep
of the working tree for instrument, mission and platform names — `swarm`, `champ`, `orsted`, `magsat`,
`dmsp`, `themis`, `cluster`, `goes`, `ace`, `wind`, `observator`, `magnetometer`, `satellite`,
`spacecraft`, `mission` — matched nothing relevant. The only substantive hits were the SuperDARN and
DavitPy provenance lines in `README.md:4`, `setup.py:3,18` and `igrfpy/__init__.py:1`, which name the
software this code came from (Field 29) rather than an instrument this software supports. Everything
else was an incidental English substring: "permission" in the `LICENSE` text, and "interface" and
"earth's surface" in `README.md:7` and `igrfpy/__init__.py:63`.

This is the substantive point, not a technicality: the IGRF is derived from ground observatory and
satellite magnetometer measurements, but **igrfpy reads none of that data**. It evaluates
coefficients that were already fitted upstream, so it processes, calibrates, parses and visualizes
no instrument's data and is purpose-built for no instrument. The field-definition guidance excludes
instrument-agnostic tools for exactly this reason: a user searching HSSI for a specific
magnetometer's software should not get a generic main-field model back. **No entry was omitted for
being hard to resolve** — there was no candidate entity at any point, so the SPASE resolution ladder
never applies and no ambiguity is being hidden. The field is correctly empty, and should stay empty
unless the package gains instrument-specific support.

### 32. Related Observatories (OPTIONAL)
**Not found — correctly empty**, for the same reason as Field 31: no mission, observatory or ground
network is supported, referenced or required by this software, and the name sweep above found no
candidate.

### 33. Logo (OPTIONAL)
**Not found.**

The repository contains no image file (its 12 tracked files are listed under Field 17), neither
README embeds an image, GitHub reports `has_pages: false` and an empty `homepage`, and SoMEF reports
no `logo` result. There is no logo to link.

---

## Durable limitations and follow-ups for a later refresh

- **Version 0.2 has no release date, and probably never will.** The two candidate dates and the
  reason both were rejected are in Field 12. If the project ever tags a release, that tag supersedes
  the reasoning there.
- **The licence row is a best-available match, not an exact one.** The repository's licence is SPDX
  `GPL-3.0-only` and the vocabulary offers only `GNU General Public License v3.0 or later`
  (Field 15). Move the value if a `GPL-3.0-only` row is ever added.
- **`igrfpy/igrf11_cli.f` and `igrfpy/igrf12_cli.f` are vendored but unbuilt** (Scope note). Should a
  future revision add them to `ext_modules`, the grid, yearly-time-series and
  declination/inclination/horizontal-intensity capabilities would become reachable and Field 4 would
  need revisiting. Check `setup.py`'s `ext_modules` before crediting them.
- **The module docstring at `igrfpy/__init__.py:9` says "Basic plotting tools" and is wrong** — an
  inherited DavitPy fragment describing code that is not in this package. Do not classify Data
  Visualization from it.
- **`Fortran90` was this record's earlier language value, and it traces back to the pre-2020
  `igrf11.f90` filename** — itself a misnomer for fixed-form FORTRAN 77 source (Field 13). The value
  is now `Fortran77`. If `Fortran90` reappears in this field later, it is a regression, not a
  discovery.
- **Version Description, Description and Concise Description are plain-text fields.** None renders
  markdown, so backticks, asterisks and link syntax would appear literally to a reader. The version
  description is recorded above without inline-code backticks for that reason, and the earlier
  Description value's leaked Markdown link syntax (Field 8) is what the defect looks like in
  practice. Concise Description additionally has a hard 200-character cap enforced in validation,
  unlike the length-unchecked `CharField` columns behind Fields 26-30 (Fields 9 and 28).
- **The status could legitimately move from `Inactive` to `Unsupported`** if the author ever posts a
  deprecation notice, archives the repository, or asks for a maintainer (Field 23). Absent such a
  statement, `Inactive` remains the defensible value.
- **Organizational-author candidates are pre-researched** in Field 6, including IAGA's ROR
  `https://ror.org/013ym9476` and the finding that no ROR exists for the VT SuperDARN Lab. A future
  curator can act on them without repeating the lookups.
