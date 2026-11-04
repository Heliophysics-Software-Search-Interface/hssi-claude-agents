# HSSI Metadata Extraction Results

**HSSI Software ID:** 57de45be-d089-435e-a4d1-5ba361fda1a2
**Repository:** https://github.com/space-physics/iri2016
**Source Revision:** ca523ad80d22c25e95ecb2f95d37094cb7adb035
**Extraction Date:** 2026-11-03
**Validation Date:** 2026-11-03
**Validation Status:** PASS

---

## Scope notes — read these before the fields

**Two IRI-2016 Python packages, kept apart.** This record is `space-physics/iri2016`, Michael Hirsch's
Python and MATLAB interface to the IRI-2016 model. It is not `rilma/pyIRI2016` (Ronald Ilma's Python
wrapper), which HSSI catalogues separately as `pyIRI2016`. The two share early history: this
repository began as Hirsch's fork of `rilma/pyIRI2016`, and its git history still starts with Ilma's
2016–2017 commits. Until hssi-website issue #81 (August 2026) HSSI also held a row named `IRI-2016`,
but that row's repository, DOI (`10.5281/zenodo.240895`) and dates were all `rilma/pyIRI2016`'s, and it
was retired as a duplicate of `pyIRI2016`. Before this submission HSSI had never catalogued
`space-physics/iri2016`; this record now uses the name `IRI-2016` for it (Field 7), and nothing from the
retired row carries over. Every identifier in this dossier was checked to belong to this repository's
lineage rather than to `rilma/pyIRI2016`; Fields 2, 3, 6, 7, 10, 29 and 33 say how.

**The lineage, as far as the evidence reaches.**
- 2016-12-09 → 2017-05: `rilma/pyIRI2016` (Ronald Ilma, `rri5@cornell.edu`). Its v1.1.0 release
  (2017-01-12) is Zenodo record 240895.
- 2017-04-13 onward: Hirsch's fork, published as `scivision/pyIRI2016`. Its GitHub releases v1.2.0,
  v1.2.1 and v1.2.1_1 (all 2017-04-24) were archived by the GitHub–Zenodo integration under concept
  DOI `10.5281/zenodo.591802`. Hirsch's 2017 work was also merged back upstream (rilma PR #4,
  2017-04-28), so both repositories contain those commits.
- 2018-02-27: the present GitHub repository object (id 123071113) was created and the history pushed
  into it; tags start at v1.3.0 the same day. The v1.2.x tags are not present in this repository.
- v1.5.1 (2018-07-30): release titled "Rename, increase test coverage, add Matlab example" with body
  `PyIRI2016=>IRI2016`; the first PyPI upload under the `iri2016` name is the same day.
- Today the repository is `space-physics/iri2016`. The GitHub API answers both `scivision/pyIRI2016`
  and `scivision/iri2016` with a permanent redirect to repository id 123071113, which is this one.

**The pinned revision is 24 commits past the last release.** The last release is v1.11.1 (2020-11-04).
`pyproject.toml` at the pin declares `version = "1.12.0"`, but no tag, GitHub release or PyPI upload of
1.12.0 exists, so 1.12.0 is a declared-but-unreleased version (Field 12). Evidence for the other fields
is read at the pin. Differences from the release that matter to a reader: the vendored IRI Fortran was
refreshed from upstream on 2023-06-29 (the `irisub.for` change list runs to `2020.09 01/03/21` at the
pin against `2020.05 01/16/20` at v1.11.1), `igrf2020s.dat` was added, the Meson build was removed,
packaging moved from `setup.cfg`/`setup.py` to `pyproject.toml` (Python ≥3.9 at the pin, ≥3.7 at the
release), and a Windows CI job was added.

**Vendored model code versus this package's own code.** `src/iri2016/src/*.for` is the IRI-2016 Fortran
distributed at irimodel.org, patched by Hirsch for the command-line interface (`.gitattributes` marks
`src/iri2016/src/*` `linguist-vendored`). This package's own code is the Python package
(`src/iri2016/*.py`), the free-form driver `src/iri2016/src/iri_driver.f90`, the CMake build, and the
MATLAB package `+iri2016/`. Several fields turn on that split: model-provenance comments in the vendored
Fortran (authors of routines, the missions whose data fitted the coefficients) describe the IRI model,
not this software.

**How the package runs the model.** `iri2016.IRI()` builds the Fortran on first call with CMake ("build
on run", `src/iri2016/build.py`), then runs the compiled `iri2016_driver` executable as a subprocess for
each evaluation and parses its text output into an `xarray.Dataset` (`src/iri2016/base.py`). The driver
fixes the IRI option switches (`jf`) itself; the README tells users to edit the driver and rebuild to
change them. `.archive/` holds retired code from the older f2py design and is not part of the package.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** Shawn Polson
- **Submitter Email:** shawn.polson@lasp.colorado.edu

**Source:** Supplied by the user for this submission. The catalogue already holds a Person row
`Shawn` / `Polson` (with an ORCID), so the name is written in exactly that split. Nothing in the
repository identifies a submitter; the authors' addresses in the git history (`rri5@cornell.edu`,
the `scivision` GitHub noreply addresses) are correspondence context only and are not this field's
value.

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.591802

**What it is.** The Zenodo concept DOI for `scivision/pyIRI2016`, this repository under its former
name. DataCite types it `Software`; its `HasVersion` list is four version records — 556838 and 556839
(both v1.2.0, byte-identical files), 556841 (v1.2.1, titled "scivision/pyIRI2016: prereqs") and 556843
(v1.2.1_1). Every version carries `IsSupplementTo https://github.com/scivision/pyIRI2016/tree/<tag>`,
the GitHub–Zenodo integration's signature. Creators: `Ronald I.` and `Michael Hirsch, Ph.D.`
(affiliation `SciVision, Inc.`).

**How the deposit was tied to this repository.** Three independent checks:
1. GitHub redirects `scivision/pyIRI2016` (the `IsSupplementTo` owner/name) to repository id 123071113,
   which is `space-physics/iri2016`.
2. The v1.2.1_1 deposit's zip unpacks to a directory named `scivision-pyIRI2016-8c5db0e`. Commit
   `8c5db0e` ("userreq", 2017-04-24) is an ancestor of the pinned revision, and all 91 files in the zip
   hash (git blob hash) identically to that commit's tree; the only tree entry absent from the zip is
   the `pyiri2016/data` symlink, which a zip does not carry as a file.
3. The v1.2.0 deposit's zip root is `scivision-pyIRI2016-89bc356`; commit `89bc356` ("release",
   2017-04-24) is also an ancestor of the pin.

Rule 5 of the Field 2 rubric therefore fires: it is the concept DOI of a software deposit of this
software.

**Known costs, recorded and accepted (rule 5).** The concept presents its newest deposit, v1.2.1_1 of
2017-04-24, far older than Field 12's v1.11.1, and under the old name. The "Software" citation the
site generates from it by doi.org content negotiation reads, in APA style: `Ronald, I., & Michael
Hirsch, P. D. (2017). scivision/pyIRI2016 v1.2.1_1 (Version v1.2.1_1) [Computer software]. Zenodo.`
The creator strings are Zenodo's GitHub-integration renderings, not the authors' names (Field 6 has
those). No deposit was made after April 2017, so the concept will keep presenting that version. None of
this is a reason to clear or move the value under the rubric; it is the only DOI that identifies this
software.

**The README's DOI badge is a trap — do not adopt it.** `README.md` line 3 carries a Zenodo badge for
`10.5281/zenodo.240895`. That record is `rilma/pyIRI2016: Official release of the IRI2016 wrapper in
Python`, v1.1.0, 2017-01-12, sole creator Ronald Ilma (Cornell University), `IsSupplementTo
https://github.com/rilma/pyIRI2016/tree/v1.1.0`. It archives the other repository, which still exists
and which HSSI catalogues as `pyIRI2016` with this same DOI as its Field 2. Rule 2 ("Software record of
a different product") fires. Shared history does not change that: rilma's `v1.1.0` commit (`8f25250`)
is an ancestor of this repository's pin only because Hirsch forked that code, while the deposit
archives the separate, still-active repository `rilma/pyIRI2016` (GitHub repository id 72548874; this
repository is 123071113), and this project has its own concept deposit (above). The badge's history:
Ilma added it on 2017-01-12; Hirsch removed it on 2018-02-27 (`a9198a2`, when the present repository
was created) and put it back on 2018-07-12
(`5519943`, "modernize, pep8, mypy"), still pointing at Ilma's v1.1.0 deposit, and his later
`space-physics/iri2020` README carries the same badge. Read it as the maintainer's credit to the original
wrapper, not as a DOI for this code: the deposit's files are `rilma/pyIRI2016` v1.1.0. Adopting it would
give two catalogue entries one DOI and cite Ilma's 2017 release as this software.

**Negative research — no other software DOI for this software (searched 2026-11-03).** Run on the
descriptive title, the old and new repository names, and the creators, each with a control:
- DataCite `descriptions.description:"International Reference Ionosphere 2016"` restricted to software
  returns exactly the five `scivision/pyIRI2016` DOIs and rilma's 240895; DataCite
  `relatedIdentifiers.relatedIdentifier:*scivision/pyIRI2016*` returns the five `scivision` DOIs (the
  positive control), while the same query on `*space-physics/iri2016*` and `*scivision/iri2016*`
  returns nothing.
- Zenodo free text `"scivision/pyIRI2016"` returns the v1.2.1_1 record; `"space-physics/iri2016"` and
  `"scivision/iri2016"` return nothing; free text `iri2016` returns rilma's record plus unrelated
  datasets, papers and one unrelated software deposit.
- Zenodo creator-keyed search over `Hirsch, Michael`, `Michael Hirsch` and `Michael Hirsch, Ph.D.`
  surfaces, among IRI-related titles, only `scivision/pyIRI2016 v1.2.1_1` and `scivision/pyiri90`
  (IRI-90's deposit). Hirsch's later PyHC packages (for example `space-physics/msise00`) have deposits,
  but none was made for this repository after 2017.
- `README.md`'s other DOI, `10.5281/zenodo.1493021`, is a Presentation (Field 27), not software.

**Coupled fields.** Field 11 follows this DOI (Zenodo). Fields 10, 12 and 15 were re-derived from the
repository rather than from the deposit: the deposit's licence id is Zenodo's `other-open` placeholder
and its dates are 2017.

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/iri2016

**Source:** `git remote -v` of the clone; the GitHub API's `full_name` `space-physics/iri2016` (not a
fork, not archived, default branch `main`); the CMake project's `HOMEPAGE_URL`
(`src/iri2016/CMakeLists.txt`) and the v1.11.1 `setup.cfg` `url`; the README's clone instruction; the
PyPI `home_page`; the PyHC registry `code:` for the `IRI-2016` entry. Recorded as the bare repository
root.

**Former names, recorded as history (rule 3).** `https://github.com/scivision/pyIRI2016` and
`https://github.com/scivision/iri2016` both redirect to this repository. They appear in the Zenodo
deposit's `IsSupplementTo` links, which keep the name the repository had in 2017. Neither is the value.

**Not this field's value.** `https://github.com/rilma/pyIRI2016` is the fork parent, a separate and
still-active repository with its own HSSI entry (Field 29). The MATLAB File Exchange listing
`https://www.mathworks.com/matlabcentral/fileexchange/81056-iri2016` is a distribution page that links
back to this repository. `http://irimodel.org/` (the repository's GitHub homepage field) is the IRI
model's site, not this software's source.

### 4. Software Functionality (RECOMMENDED)
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Physics-Based
- Data Visualization
- Data Visualization: Line Plots
- Data Visualization: 2D Graphics

Every child is listed with its parent, in fully qualified `Parent: Child` form.

**Evidence per value.**
- *Models and Simulations* / *Models and Simulations: Empirical* — the package exists to evaluate the
  IRI-2016 empirical climatology. `iri2016.IRI()` (`src/iri2016/base.py`) runs the compiled model for a
  time, location and altitude range and returns electron density, neutral, ion and electron
  temperatures, ion densities, the F2/F1/E peak densities and heights, TEC, equatorial vertical ion
  drift and foF2. The model is driven by tabulated CCIR/URSI coefficient maps and index files shipped
  under `src/iri2016/data/`. `timeprofile()` and `geoprofile()` (`src/iri2016/profile.py`) evaluate it
  over a time range or a latitude range; the same capability is exposed as the CLI modules
  `python -m iri2016.altitude|latitude|time` and to MATLAB as `iri2016.iri2016()`.
- *Models and Simulations: Physics-Based* — the bottomside ion composition the package returns comes
  from a photochemical model, not a statistical fit. The driver (`src/iri2016/src/iri_driver.f90`)
  sets `jf(4:6) = .false.`, so `jf(6)` selects "Ni - RBV-2010 & TBT-2015" (`irisub.for:603`
  `RBTT=(.not.jf(6))`). Below 300 km that branch calls `CHEMION` (`irisub.for:2155`), the
  Richards–Bilitza–Voglozin (2010) Ion Density Calculator in `iriflip.for`, which computes O+, O2+, NO+
  and N+ from chemical-equilibrium reaction rates with an NRLMSISE-00 neutral atmosphere (`GTD7`). Those
  densities reach the user as `nO+`, `nO2+`, `nNO+` and `nN+` in the returned dataset (`base.py`
  `SIMOUT`) and as `iono.nO`, `iono.nO2`, `iono.nNO`, `iono.nN` in MATLAB. The same value was settled
  for `pyIRI2016` on the same component.
- *Data Visualization* / *Data Visualization: Line Plots* — `src/iri2016/plots.py` is part of the
  installed package: `altprofile()` plots Ne and Ti/Te against altitude, `latprofile()` plots NmF2,
  NmF1, NmE and hmF2, hmF1, hmE against latitude, and `timeprofile()` plots the peak densities and
  heights, foF2 and TEC against time. The CLI modules call them when matplotlib is installed. MATLAB's
  `iri2016.plotiono()` and `iri2016.plottime()` draw the same kinds of line plots.
- *Data Visualization: 2D Graphics* — `plots.timeprofile()` also draws `pcolormesh` of electron density
  against altitude and time with a colour bar.

**Considered and not selected.**
- *Coordinate Transforms* (any child) — the vendored `igrf.for` contains geomagnetic, CGM, MLT and
  magnetospheric coordinate machinery, and the driver leaves CGM computation on (`jf(47)` stays at the
  `.true.` default). But the driver hard-codes geographic input (`jmag = 0`), and none of the dip,
  modip, CGM or MLT outputs reaches the user: `base.py` reads only oarr entries for NmF2, hmF2, NmF1,
  hmF1, NmE, hmE, TEC, the equatorial vertical ion drift, foF2, F10.7 and Ap, and the MATLAB wrapper
  only the peak values and TEC. No transform is user-facing (rule 3).
- *Models and Simulations: Forecasting* — IRI is a climatology. The foF2 storm model (Field 22)
  corrects foF2 from past 3-hour ap values in the bundled index file; nothing predicts a future state.
- *Models and Simulations: Field-line Tracing* / *Data Processing and Analysis: Field-line Tracing* —
  `igrf.for` holds field-line integrators (`SHELLG`, `STOER`), but the package exposes no tracing.
- *Data Processing and Analysis* (any child) — the package takes no data in. Its Python layer parses the
  driver's text output and assembles model output into labelled `xarray` datasets; the TEC it returns
  is computed inside the model run (`iri_tec`, called by the driver). *Time Series Analysis* is the
  closest call and fails because `timeprofile()` generates a series by repeated model evaluation and
  performs no temporal analysis of one. For comparison, the sibling IRI-90 package converts ion
  percentages to densities in its own Python code, which is the step its record's *Data Processing and
  Analysis: Analysis* rests on; here the driver asks IRI for densities directly (`jf(22) = .false.`), so
  there is no comparable step.
- *Data Visualization: Movies* — the README's animated `figures/iri2DExample02.gif` is a pre-rendered
  figure inherited from `rilma/pyIRI2016` (added 2016-12-09); the package has no animation or map code.
- *Servers and Environments*, *Mission-related* — no evidence.

### 5. Related Region (RECOMMENDED)
- Earth Atmosphere
- Earth Ionosphere
- Earth Thermosphere

**Evidence per row** (the Region vocabulary is flat, so each row is earned separately):
- *Earth Ionosphere* — the software's subject: README "Python and Matlab interfaces to the International
  Reference Ionosphere (IRI) 2016 model"; every headline output is ionospheric (electron density, ion
  composition, electron and ion temperatures, F2/F1/E peak parameters, TEC).
- *Earth Thermosphere* — the returned dataset includes `Tn`, the neutral temperature IRI computes from
  NRLMSISE-00 (`cira.for` `GTD7`), returned in Python as `Tn` and in MATLAB as `iono.Tn`; the ionosphere
  the model describes is embedded in the thermosphere, and `pyproject.toml` declares the keyword
  `thermosphere`.
- *Earth Atmosphere* — the coarse row containing both fine rows (rubric rule 5); without it the entry is
  invisible to a visitor filtering at the coarse level.

**Considered and not selected.** *Earth Lower and Middle Atmosphere* — IRI's D-region models reach down
to about 60 km, but that is ionospheric physics in the mesosphere, and the package's defaults start at
80 km (altitude CLI) or higher. *Earth Auroral Subregion* — the driver turns the auroral-boundary model
off (`jf(33:35) = .false.`). *Earth Magnetosphere* and its children — no magnetospheric output reaches
the user. A registry science-area tag (`ionosphere_thermosphere_mesosphere`) and the PyPI topic
`Atmospheric Science` were not used as evidence.

### 6. Authors (MANDATORY)

#### Author 1
- **Author Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation 1:** Boston University — https://ror.org/05qwgg493
- **Affiliation 2:** Scivision, Inc. — no identifier (see below)

#### Author 2
- **Author Name:** Ronald Ilma
- **Author Identifier:** Not found (searched; see below)
- **Affiliation:** Cornell University — https://ror.org/05bnh6r87

**Why these two.** The candidate pool is every author source the project has. At the pin there is no
`CITATION.cff`, `codemeta.json`, `.zenodo.json`, `AUTHORS` or contributors file, and none ever existed
in the history; `pyproject.toml` declares no `authors`. The sources that do name authors all name these
two people and no one else:
- `LICENSE.txt`: `Copyright (c) 2018 Michael Hirsch, Ph.D.` and `Copyright (c) 2017 Ronald Ilma`.
- `setup.cfg` at the last release tag v1.11.1: `author = Michael Hirsch, Ph.D.; Ronald Ilma`; PyPI's
  `iri2016` 1.11.1 metadata repeats it.
- The software's own Zenodo deposits (concept 591802): creators `Ronald I.` and `Michael Hirsch, Ph.D.`.
- The PyHC registry contact: `Michael Hirsch`.

**Order.** Hirsch, then Ilma, following the most recent package metadata (`setup.cfg` at v1.11.1, PyPI)
and the licence. The 2017 deposits list Ilma first; they predate everything after the v1.2.x releases.

**Michael Hirsch.** All of `Michael Hirsch, Ph.D`, `Michael Hirsch` and `scivision` at
`scivision@users.noreply.github.com`, and `Michael Hirsch, Ph.D` at
`10931741+scivision@users.noreply.github.com`, are one person: the GitHub account `scivision`, which
GitHub's contributor list credits with all 211 of those commits. The name drops the `Ph.D.` suffix
(rule 12). The ORCID is the record for a Research Scientist in Electrical and Computer Engineering at
Boston University from 2018-08 (no end date), whose works include *PyMap3D* and *h5fortran* (JOSS) and
auroral and ionospheric papers. A fielded ORCID search on given-names `Michael` and family-name `Hirsch`
returns seven records; identity rests on the employment and works, not the name. Do not use
`https://orcid.org/0000-0001-6183-6256`, a different Michael Hirsch (STFC/Leipzig, microscopy) that the
same search returns. The catalogue already holds this person's row (`Michael` / `Hirsch`, carrying this
ORCID, with Boston University and Scivision, Inc. affiliations), so the ORCID binds it.

*Affiliations.* Boston University comes from the ORCID employment, which covers 2018 onward — the
period of nearly all of this repository's development. `Scivision, Inc.` is the affiliation the
software's own Zenodo deposit gives (`SciVision, Inc.`). ROR has no record for this company: the only
"Scivision" match, `https://ror.org/011qev639`, is SciVision Biotech Inc. (Taiwan), an unrelated
company, and must not be attached. The catalogue's existing organization row is spelled
`Scivision, Inc.`, and that spelling is used so the name binds it; the company's own spelling
`SciVision, Inc.` is a known, parked divergence on a shared row, not something to correct here.

**Ronald Ilma.** Author of the code this repository was forked from, and still credited by this
software's own licence, package metadata and deposits. His commits here are `rilma`, `Ronald Ilma` and
`Ronald I` at `rri5@cornell.edu` (31 commits, 2016-12-09 to 2017-05-02). Name form: `Ronald Ilma`, as in
`LICENSE.txt` and `setup.cfg`. Rejected forms: DataCite's `Ronald, I.` (which reads as family name
`Ronald` — never imported, rule 12), Zenodo's truncated `Ronald I.`, and `Ronald R. Ilma
Campana`, which only `rilma/pyIRI2016`'s `pyproject.toml` uses. The catalogue holds two
identifier-less rows carrying his names: `Ronald` / `Ilma` (the row `pyIRI2016` lists) and a separate
`Ronald R. Ilma` / `Campana`. This entry's author is the `Ronald` / `Ilma` row. With no identifier, a name
binds only on its exact given/family split, so he is always written `Ronald` / `Ilma`; the `Campana` row
must not be used.

*ORCID — negative research (2026-11-03).* Fielded ORCID searches for given-names `Ronald` with
family-name `Ilma`, `Campana` or `Ilma Campana` return no records; family-name `Ilma` alone returns 73
records, none with a given name beginning `Ron`. The same search shape finds Michael Hirsch's known
record, so the empty result is real. No identifier is recorded, and none should be inferred from a name match.

*Affiliation.* Cornell University (`https://ror.org/05bnh6r87`): his commits to the code this
repository inherits were made from `rri5@cornell.edu` in 2016–2017, and the original code's own Zenodo
deposit (240895) gives `Cornell University` as his affiliation. The catalogue's `Ronald` / `Ilma` row
already carries that affiliation, so recording it here changes nothing on the shared row.

**Considered and not listed as authors.**
- *The IRI model's developers* — Dieter Bilitza and the COSPAR/URSI IRI Working Group originated the
  model this package runs (rule 3); their work is credited through Field 29 (`https://irimodel.org/`).
- *Authors of individual routines inside the vendored Fortran* — the source credits, among others,
  V. Truhlik, D. Bilitza and L. Triskova (Te and ion-composition models), P. Richards (the IDC
  photochemistry, `iriflip.for`), K. Torkar (FIRI, `iridreg.for`), N. A. Tsyganenko, V. Papitashvili,
  V. Popov and T. Moretto (geomagnetic and CGM routines, `igrf.for`), and Picone, Hedin, Drob and Aikin
  (NRLMSISE-00, `cira.for`). Rule 4 excludes routine-level credits, and the IRI distribution names no
  author for the component as a whole.
- `w2naf` — thanked in the v1.4.1 release notes for feedback; acknowledged, with no commits and no
  presence in any author source.
- No other committer exists: `git shortlog` at the pin and GitHub's contributor list resolve every
  commit to Hirsch or Ilma.

### 7. Software Name (MANDATORY)
IRI-2016

**Why `IRI-2016`.** It is the name the curated PyHC registry gives this repository: `name: IRI-2016` on
the entry whose `code:` is `https://github.com/space-physics/iri2016`, in `_data/projects_unevaluated.yml`
(registry commit `b1e3c973`). It is also the standard written form of the model generation, the one a
searcher types (as with `IRI-90` for the earlier generation), and it follows the way this author's other
model interfaces are named in the catalogue after their registry entries (`IRI-90`, `HWM-93`, `IGRF-13`,
`MSISE-00`, as of 2026-11-03). The choice was deliberate: Field 7's rule 8 would otherwise
take the project's own spelling, so a later refresh should keep `IRI-2016` as a registry-held name
(rule 3) rather than "correct" it to `IRI2016`.

**Alternative weighed: `IRI2016`.** The project's own spelling, used consistently: the README H1
`IRI2016 ionosphere model from Python and Matlab`, the README prose ("A Fortran compiler is required to
build the IRI2016 code", "This Python wrapper of IRI2016", "IRI2016 is readily accessible from Matlab"),
the package description `IRI2016 International Reference Ionosphere from Python`, and the rename in
release v1.5.1, `PyIRI2016=>IRI2016`. It is the same name without the hyphen; the registry form was
preferred for the reasons above.

**The retired HSSI row of the same name was a different package.** Until hssi-website issue #81
(August 2026) HSSI held a row named `IRI-2016` whose repository, DOI (`10.5281/zenodo.240895`) and dates
were all `rilma/pyIRI2016`'s; it was retired as a duplicate of `pyIRI2016`. This record's `IRI-2016` is
`space-physics/iri2016`, and none of that row's identifiers apply to it (scope note, Field 2).

**Other forms not adopted.**
- `iri2016` — the repository, PyPI distribution, import and MATLAB package slug (rule 4).
- `IRI2016 ionosphere model from Python and Matlab` — a title line, not a name (rule 2).
- `pyIRI2016` / `scivision/pyIRI2016` — the abandoned former name, and the name of the separate
  `rilma/pyIRI2016` entry (rule 7).

**Registry link, settled.** The PyHC `IRI-2016` entry's `hssi:` link pointed at
`https://hssi.hsdcloud.org/software/pyiri2016/`, HSSI's page for the separate `rilma/pyIRI2016`, until
registry commit `08f381b1` ("Point IRI-2016's HSSI link at its own HSSI entry", 2026-11-04 UTC), which
changed it to `https://hssi.hsdcloud.org/software/iri-2016/`, this entry's page.

### 8. Description (MANDATORY)

Python and Matlab interfaces to the International Reference Ionosphere (IRI) 2016 model. A Fortran compiler is required to build the IRI2016 code.

This Python wrapper of IRI2016 uses our build-on-run technique. On the first run or `iri2016.IRI()` the Fortran code is built--we call this "build on run".

* Altitude Profile: plot density and temperatures vs altitude
* Latitude profile: plot densities and height at the peak of F2, F1, and E regions vs geographic latitude
* Time profile: plot densities and height at the peak of F2, F1, and E regions vs UTC

`iri2016/iri2016/data/index/{apf107,ig_rz}.dat` are [regularly updated](http://irimodel.org/indices/). Currently we don't auto-update those.

**Source and its exact relationship to the README (rule 7, new value).** There is no `CITATION.cff`
abstract and no docs site, so the text is the README's lead paragraph extended by whole sentences and
items from later README sections, in the README's order:
- Paragraph 1 is the README lead paragraph (lines 11–12), with its in-page link `[Matlab](#matlab)`
  reduced to the word and its line break joined.
- Paragraph 2 is the two sentences opening the Install section's build-on-run note, verbatim.
- The three bullets are the Usage section's item headings, with the commands and figures removed. One
  correction: the README writes "F2, F2, and E" in the latitude and time items; the code plots NmF2,
  NmF1, NmE and hmF2, hmF1, hmE (`plots.latprofile`, `plots.timeprofile`), so the second `F2` is the
  README's typo for `F1` and is written `F1` here.
- The last paragraph is the README's "Data files" section verbatim, including its link. The path it
  gives is the README's own, from before the `src/` layout; at the pin the files are under
  `src/iri2016/data/index/`. Kept verbatim rather than rewritten, because the sentence states a real
  assumption a user needs (see below) and rewriting the path would be composing.

**Dropped from the README on the code test (rule 2).** The fourth usage item, "Latitude vs Longitude:
plot of foF2 a function of geographic latitude and longitude", is not in the description: no code at
the pin computes or plots a latitude–longitude map (`geoprofile()` scans latitude at one longitude). The
README's map figure and animation are inherited from `rilma/pyIRI2016`. Restore the item only if a
later pin ships a map capability.

**Assumptions the README does not state, recorded for a future editor.**
- CMake is required as well as a Fortran compiler: `build.py` raises `FileNotFoundError("CMake not
  available")` when `cmake` is not on the path, and nothing installs it.
- Plotting needs matplotlib, which is not a declared dependency (the CLI modules skip plotting when the
  import fails).
- The bundled index files end early: `apf107.dat` (3-hour ap, F10.7) runs to 2019-02-15 and `ig_rz.dat`
  (IG12, Rz12) to 2020-12. The storm correction in Field 22 needs ap history in that file, and IRI needs
  the solar indices for the requested date, so dates beyond the bundled coverage need updated files from
  irimodel.org — which is what the README's "Currently we don't auto-update those" warns about. For a
  month outside `ig_rz.dat`'s range, `tcon` in `irifun.for` prints `** OUT OF RANGE **` and returns
  without the indices; for a date outside `apf107.dat` the ap lookups return `-5`.

**Preview.** The opening sentence stands alone, and Field 8's first 199 characters end inside the third
sentence, before any markdown. The result card's preview is Field 9's value.

### 9. Concise Description (OPTIONAL)
International Reference Ionosphere 2016 from Python and Matlab

**Source.** The curated PyHC registry `description:` for the entry whose `code:` is this repository
(`_data/projects_unevaluated.yml`; the same text at registry commit `b1e3c973` and at `08f381b1`), which
is also the GitHub repository description. It is the first source rule 6 names, 62 characters, and
every claim in it holds at the pin: the package runs the IRI-2016 model from Python (`iri2016.IRI()`)
and from MATLAB (the `+iri2016` package). `Matlab` is the project's own spelling throughout and is kept
(rule 4 fixes errors only).

**Why the field is filled.** By the user's decision, every new entry in this catalogue batch carries both
a description and a concise description. That overrides rule 6's default for an empty field, which
would have left it empty because Field 8's opening sentence ("Python and Matlab interfaces to the
International Reference Ionosphere (IRI) 2016 model.") already works as a preview; that empty outcome
is the alternative not taken. HSSI held no concise description for this entry before this value was
added.

**Other candidates not taken.** The package description `IRI2016 International Reference Ionosphere
from Python` omits the MATLAB interface; the README H1 `IRI2016 ionosphere model from Python and Matlab`
is a title line and does not name the model in full.

### 10. Publication Date (RECOMMENDED)
2017-04-24

**Source (rule 4, anchor a: first release).** The first public release of this software is its v1.2.0
release as `scivision/pyIRI2016`, archived by the GitHub–Zenodo integration as record 556838 (created
2017-04-24T06:18Z), whose zip root is commit `89bc356` ("release", 2017-04-24 02:17 −0400 = 06:17 UTC),
an ancestor of the pin. Records 556839 (a byte-identical v1.2.0), 556841 (v1.2.1) and 556843
(v1.2.1_1) followed within the hour.

**A rename is not a new project (rule 2).** The 2017 releases were published under the name
`scivision/pyIRI2016`; the same continuous history was renamed `IRI2016` in v1.5.1 and is this
repository. GitHub's redirect from the old name and the commit ancestry tie them.

**Alternatives considered and rejected.**
- 2017-01-12 — `rilma/pyIRI2016` v1.1.0 (Zenodo 240895), and 2016-12-09, its first commit. These are
  the fork parent's artifacts, a separate and still-existing project with its own HSSI entry, whose own
  Publication Date is 2017-01-12 (rule 2: a fork parent's dates do not date this software).
- 2018-02-27 — the present GitHub repository object's `created_at` and its first release, v1.3.0. The
  repository was re-created that day with the history pushed in, so the date is later than the first
  release.
- 2018-07-30 — the first PyPI upload under the name `iri2016` (1.5.1). Later than the Zenodo releases.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source (rule 1).** Field 2 is a Zenodo DOI; DataCite's `publisher` for it is `Zenodo`. Zenodo has no
ROR, and CERN's ROR identifies the operator, not the repository, so the URL is the identifier. The
catalogue's existing `Zenodo` organization row carries exactly this name and identifier. PyPI and the
MATLAB File Exchange are distribution channels, never the publisher (rule 6).

### 12. Version (RECOMMENDED)
- **Version Number:** v1.11.1
- **Version Date:** 2020-11-04
- **Version Description:** build on run instead of build on import
- **Version PID:** Not found

**Release history read from the pin.** Tags v1.3.0 → v1.11.1 (2018-02-27 → 2020-11-04), each with a
GitHub release, and every tag except `v1.8.0` is an ancestor of the pin. `v1.8.0` is not on the pin's
lineage; it is older than v1.11.1 either way and does not affect the choice. PyPI's `iri2016` releases
run 1.5.1 → 1.11.1, all sdists, none yanked, and include an untagged 1.7.0 (2018-11-27). The 2017
v1.2.x releases exist only as Zenodo deposits (Field 2).

**Number.** v1.11.1 is the newest release on every channel: the GitHub release `v1.11.1` (published
2020-11-04T22:46Z), the tag, `setup.cfg` at the tag (`version = 1.11.1`), and PyPI 1.11.1 (uploaded
2020-11-04T22:47Z). The tag form `v1.11.1` is used (the GitHub release and tag write it so; `setup.cfg`
and PyPI write `1.11.1`); both are correct, so a later refresh should not "fix" the prefix.

**Declared but never released — do not record.** `pyproject.toml` at the pin declares `1.12.0`. There
is no `v1.12.0` tag, no GitHub release and no PyPI upload of it (rule 2). At the next refresh, check for
a 1.12.0 tag, release or upload.

**Date.** The GitHub release's `published_at`, 2020-11-04 UTC (rule 7); the tagged commit `d73da84`
(2020-11-04 17:44 −0500 = 22:44 UTC) and the PyPI upload agree.

**Description (rules 13–16).** The release's title, verbatim: "build on run instead of build on
import". Its body reads "using best-practices for Python, build on first run instead of first import."
and "Add more tests to Matlab."; the first restates the title behind a generic clause and the second is
test housekeeping (rule 14), so the title alone is recorded. It is the user-visible change: since
v1.11.1 the Fortran is compiled on the first model call rather than at import (Field 8 describes the
technique).

**Version PID.** No Zenodo deposit exists for any release after v1.2.1_1 (April 2017), so v1.11.1 has
no version DOI (rule 18). The v1.2.x version DOIs belong to those releases only.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- MATLAB
- Fortran77
- Fortran90
- Fortran 2003
- Fortran 2008

**Which languages count (rule 4).** The user writes Python or MATLAB; the science core is the vendored
IRI Fortran that CMake compiles on first run, plus Hirsch's free-form driver. Counted Fortran sources are
exactly the ones the build compiles: `src/iri2016/src/CMakeLists.txt` builds `irisub.for irifun.for
iritec.for iridreg.for iriflip.for igrf.for cira.for`, and `src/iri2016/CMakeLists.txt` links them into
`iri2016_driver` from `src/iri_driver.f90`. Not counted: `src/test.f90` (built only with
`BUILD_TESTING`, test-only), `src/iri2016/src/reference/*` (not built), and `.archive/` (retired f2py-era
Python and MATLAB).

**Evidence per value (rule 6: one row per standard a construct requires).**
- *Python 3.x* — `pyproject.toml` `requires-python = ">=3.9"`, classifier `Programming Language ::
  Python :: 3`; CI runs Python 3.9 and 3.11.
- *MATLAB* — a supported front end: the `+iri2016` package (`iri2016.m`, `plotiono.m`, `plottime.m`,
  `private/cmake.m`) with a `matlab.unittest` suite (`+iri2016/TestUnit.m`), `TestAll.m`, a
  `buildfile.m` with `check` and `test` tasks, example scripts in `Examples/`, a README section, and a
  MATLAB File Exchange listing. Caveat recorded for a future agent: the MATLAB auto-build helper
  (`+iri2016/private/cmake.m`) runs `ctest -S setup.cmake`, but `setup.cmake` was deleted on 2021-10-11
  (commit `e545b56`) and `MANIFEST.in` still lists it. `iri2016.m` calls that helper only when no
  `iri2016_driver` executable is already present in `src/iri2016/`, so the MATLAB path depends on the
  driver having been built there by other means. That is a defect in one helper, not a stub: the
  interface, its tests and its examples are maintained (the test was modernised on 2023-06-28), so
  MATLAB stays.
- *Fortran77* — the seven compiled `.for` files are fixed-form; gfortran 14.1.0 at `-std=f2018` rejects
  `irisub.for` and `igrf.for` for Fortran-2018-deleted features (shared and non-`CONTINUE` DO
  terminations, arithmetic IF).
- *Fortran90* — attribute declarations with `INTENT` (`irisub.for:416-418`, Hirsch's interface patch;
  `iritec.for`; `igrf.for:713`) and `DO WHILE … END DO` (`iridreg.for:129`); `irisub.for` and
  `iridreg.for` compile cleanly at `-std=f95`.
- *Fortran 2003* — `iri_driver.f90` uses `use, intrinsic:: iso_fortran_env` and the deferred-length
  `character(:), allocatable :: datadir`; gfortran rejects it at `-std=f95` ("Fortran 2003: module nature
  in USE statement", "deferred type parameter") and accepts it at `-std=f2003`.
- *Fortran 2008* — `igrf.for:740` `if (mess) error stop 'Error while reading ' // …`, added in Hirsch's
  2023 patch; gfortran reports "Fortran 2008: ERROR STOP statement" at `-std=f2003`. At `-std=f2008` it
  instead reports that a STOP code must be a constant expression: the concatenated, non-constant stop
  code is a Fortran 2018 feature. The vocabulary has no Fortran 2018 row, and nothing reaches a Fortran
  2023 feature, so the `error stop` statement's own edition, Fortran 2008, is the row recorded.

**Rejected.** `Fortran 2023` (no construct needs it). `C` (none in the tree). CMake (build system, no
row). The `Fortran 2008: Pointer procedure assignment` diagnostics gfortran prints for `irifun.for` are
the known `REAL*8` cascade, not a Fortran 2008 construct. `Jupyter Notebook` (one example notebook,
Python kernel).

### 14. Reference Publication (OPTIONAL)
Not found

**Negative research.** No `CITATION.cff`, no "Citing" or "How to cite" section, no JOSS badge, and no
paper directory at the pin or anywhere in the history. ADS/SciX full-text searches for
`"space-physics/iri2016"`, `"scivision/iri2016"`, `"scivision/pyIRI2016"`, `"pip install iri2016"` and
`"iri2016 python"` (with a nonsense-token control returning zero and a `"timduly4/pyglow"` positive
control returning hits) found papers that use or name the package (Field 27) but none that describes it.

**Rejected candidates.**
- `https://doi.org/10.5281/zenodo.1493021` — the README's "2016 presentation": Dieter Bilitza's
  slides on the IRI model, typed Presentation. A presentation is never Field 14 (rule 2), and it
  describes the model, not this software (rule 5). See Field 27.
- Bilitza et al. (2017), *International Reference Ionosphere 2016: From ionospheric climate to
  real-time weather predictions*, Space Weather 15, `10.1002/2016SW001593` — the IRI-2016 model paper.
  It describes the model, not this package (rule 5), and the repository never cites it. Recorded so it
  is not proposed again.
- The two Zenodo software DOIs (Field 2) — software deposits, not publications (rule 1).

### 15. License (RECOMMENDED)
MIT License

**Source.** `LICENSE.txt` at the pin is the MIT text (`MIT License`, copyright lines for Michael Hirsch
2018 and Ronald Ilma 2017); GitHub detects SPDX `MIT`. The licence has been MIT since Ilma's
`License.txt` of 2017-01-12; the file was renamed three times (`License.txt` → `LICENSE.md` → `LICENSE`
→ `LICENSE.txt`) and gained Hirsch's copyright line in 2018, with no change of licence.
`pyproject.toml` declares no licence key and no licence classifier at the pin — a packaging gap, not a
licensing fact.
`MIT License` is the exact vocabulary row. The Zenodo deposits' licence id is `other-open`, Zenodo's
placeholder, not a licence (rule 7 trap). No licence URI is a storable value (rule 9).

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- thermosphere
- ionosphere
- build-on-run
- ionosphere-modeling
- matlab-python-interface
- International Reference Ionosphere
- electron density
- electron temperature
- ion temperature
- NmF2
- hmF2
- fof2
- total electron content
- pyhc package

**Project-declared (rule 9).** `thermosphere` and `ionosphere` are `pyproject.toml` `keywords`;
`build-on-run`, `ionosphere`, `ionosphere-modeling` and `matlab-python-interface` are the GitHub
repository topics. Each binds an existing row of the same spelling (`ionosphere-modeling` is the
hyphenated row, matching the topic; a separate `ionosphere modeling` row also exists and is not used).

**Domain terms a searcher would type (rule 10), each evidenced in the code.** The model the package runs
(`International Reference Ionosphere`, binding the existing capitalised row), and the quantities it
returns: `electron density` (`ne`), `electron temperature` and `ion temperature` (`Te`, `Ti`), `NmF2` and
`hmF2` (returned and plotted), `fof2` (`foF2`, returned and plotted since v1.8.5 "add foF2 plot"), and
`total electron content` (`TEC`). All but `fof2` bound rows the catalogue already held before this
submission; `fof2` had no row and was introduced by this record, written lower-case as the rubric
requires for a new keyword, although the quantity is conventionally written `foF2`.

**PyHC marker (rule 15).** `pyhc package` — the software is listed in the PyHC registry's
`projects_unevaluated.yml`.

**Considered and not added.** The registry tags `ionosphere_thermosphere_mesosphere` (the domain test
passes, but the underscore-joined form is never added as a new keyword, and `ionosphere` and
`thermosphere` already carry it) and `specific` (a registry scope tag, rule 2). `iri` (an existing row;
the name already carries the acronym). `fortran`, `python`, `matlab`, `cmake` (restate Field 13 or are
build tooling). `ion composition` and `neutral temperature` (true outputs, but the project never uses
the phrases and the listed terms cover the headline quantities). `storm`/`geomagnetic storm` (Field 22
carries it).

### 17. Data Sources (OPTIONAL)
Not found — evidenced empty

**Source (rule 11).** The software reaches no remote source. A sweep of the tracked tree outside the
vendored Fortran for `urlopen|urlretrieve|requests.|ftplib|wget|https?://` matches only README badges,
links and the clone command, and CMake's `HOMEPAGE_URL`; the vendored Fortran's matches are comments
naming where its inputs come from. The model reads only files shipped in the package (`src/iri2016/data/`:
CCIR and URSI coefficient maps, IGRF coefficients, `mcsat` tables and the `apf107.dat`/`ig_rz.dat`
index files), which the driver points at by passing the installed `data` directory. Bundled model tables
are not a data source (rule 5), and the README says the index files are not auto-updated. Every row
was weighed: `HTTP/HTTPS Directories` and `FTP/FTPS Directories` (no download code), `Other` (no
source to name), `Observatory/Mission-specific` (mission-agnostic, Fields 31/32), and the named
services (no client for any).

### 18. Input File Formats (RECOMMENDED)
- ascii

**Source.** The compiled model reads ASCII coefficient and index tables at run time from the package's
`data` directory: `ccir/ccir11-22.asc` and `ursi/ursi11-22.asc` (foF2 and M(3000)F2 coefficient maps),
`igrf/dgrf1945-2015.dat`, `igrf2015*.dat`, `igrf2020*.dat` (IGRF coefficients), `mcsat/mcsat11-22.dat`,
and `index/apf107.dat` and `index/ig_rz.dat` (read by `GETSHC`, `read_ig_rz`, `readapf107` and the
CCIR/URSI reader in `irisub.for`). The index files are the ones the README says users must refresh from
irimodel.org themselves, so they are a format the software genuinely accepts from the user. The Python
layer's `np.genfromtxt` reads the driver's stdout pipe, not a file, and is not counted.

### 19. Output File Formats (RECOMMENDED)
- netCDF3/4

**Source (rule 6).** `python -m iri2016.latitude … -o <file>` writes the latitude profile with
`iono.to_netcdf(outfn)` (`src/iri2016/latitude.py:16`), a public CLI option. Caveat: `to_netcdf` needs
the `netCDF4` or `scipy` backend, neither of which the package declares, so the write works only where
one of them is installed.

**Not counted.** The API's return value is an in-memory `xarray.Dataset` (rule 5); the plots are shown,
never saved (`plots.py` has no `savefig`), so no `Other`; the driver prints a numeric table to stdout,
which is console output, not a file; MATLAB returns a struct.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Source (rule 4: a native build).** The Fortran is compiled on the user's machine, so the value is the
platforms the project builds and documents for. The README gives a Fortran-compiler route for each:
`apt install gfortran` (Linux), `brew install gcc` (Mac), MSYS2 (Windows). `.github/workflows/ci.yml`
defines a `core` job on `ubuntu-latest` and `macos-latest` and a `windows` job on `windows-latest` with
MSYS2 MinGW gfortran. `build.py` has a Windows branch (`-G "MinGW Makefiles"`) and `base.py` appends
`.exe` on Windows. As of 2026-11-03 GitHub retained no run history for the
workflow, so the three values rest on the CI configuration, the per-OS install documentation and the platform-specific code, not on observed passing
runs. `Operating System :: OS Independent` is the package's classifier but is never the value for a
compiled package (rule 4).

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Source (rule 4).** Portable Fortran compiled on the user's machine at first run, with no SIMD
intrinsics, assembly, architecture-conditional code or CPU-specific flags (the CMake files set none).
PyPI carries only sdists, so no architecture-specific binary was ever published. A macOS CI runner does
not add an arm64 row.

### 22. Related Phenomena (OPTIONAL)
- Geomagnetic Storms

**Source (rule 5: a storm-time function).** The driver enables IRI's foF2 storm model: it sets
`jf(26) = .true.` and leaves `jf(8)` true, so `irisub.for:1346` sets `fstorm_on`, and line 1366 calls
`STORM`, which scales foF2 by a storm-time correction computed from the preceding 3-hour ap history and
derives the storm-time peak density `NMF2S` from it. Its whole purpose is the ionosphere's response to
geomagnetic storms, the contrast case rule 6 names, so rule 6 ("An activity index as an input is not the
phenomenon") does not apply. It is a primary function of this software rather than an optional
correction: the package's own driver switches it on explicitly
(`jf(26) = .true.  ! jf(26) == jf(8) == .true. for foF2`), the public API offers no way to turn it off
short of editing and rebuilding the driver, and so every evaluation for a date with ap history applies
it. The storm-corrected peak density is what the model returns as NmF2 (`OARR(1)=NMF2S`,
`irisub.for:2267`) and what the electron-density profile is built on, and both reach the user. (The separate `foF2` value that
Hirsch's patch adds, `oarr(100) = foF2` at `irisub.for:2346`, is the uncorrected one.) The same value
was settled for `pyIRI2016`, which enables the same switch.

**Limits worth knowing.** The foE storm model (`jf(35)`) and the auroral boundary (`jf(33)`) are off in
the driver. The ap history comes from the bundled `apf107.dat`, which ends on 2019-02-15; for a later
date with no updated index file, IRI finds no ap value and applies no storm correction.

**The other six rows** — `Coronal Heating`, `Coronal Mass Ejections`, `Solar Corona`, `Solar Flares`,
`Solar Wind`, `X-ray emission` — are solar or heliospheric and the software computes nothing about them.

### 23. Development Status (RECOMMENDED)
Inactive

**Source (rule 6).** The software has stable releases (v1.11.1 on PyPI and GitHub, 2020-11-04). The last
commit on the default branch `main` is `ca523ad` ("ci: add windows"), 2024-01-14. That is more than 24
months before 2026-11-03, so rule 6 gives `Inactive`. The repository is not archived,
the README carries no repostatus badge and no status statement, and nothing points to a new location.
Dated anchors for a later refresh: last commit 2024-01-14; last release 2020-11-04.

**Rejected.** *Active* — no commit in the last 24 months. *Unsupported* — the repository is open, and
open issues alone do not show the author has ceased all work. *Moved* — `space-physics/iri2020`, the
same author's interface to the next model generation, is a separate project, and nothing in this
repository points to it. The trove classifier `Development Status :: 5 - Production/Stable` is a
packaging label, not a repostatus term.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/iri2016

**Source (rule 5).** The README is the documentation: install routes per OS, build-on-run, usage for
each CLI profile, the JF-switch note, the MATLAB section and the data-files caveat. There is no `docs/`
directory, no Read the Docs or MkDocs configuration, no Pages site (`has_pages: false`), and no
`Documentation` URL in the package metadata.

**Rejected.** *The wiki* (`iri2016.wiki.git`, two commits on 2018-12-11): a placeholder `Home` page and
one page, "BUG: Repeated IRI2016 calls", describing NaN ion densities when the old in-process (f2py)
build was called repeatedly. The current design runs the driver as a fresh subprocess per call, so the
page documents a retired architecture; it is not documentation (rule 4). *`http://irimodel.org/`* (the
repository's GitHub homepage) documents the IRI model, not this package, and the project does not
nominate it as its documentation.

### 25. Funder (OPTIONAL)
Not found

**Negative research (rule 12).** No funding statement, acknowledgement, grant number or sponsor appears
in the README, licence, package metadata, release notes or Python/MATLAB code; the software's Zenodo
deposits have no funding references. The only funding-adjacent file the repository ever had,
`.github/FUNDING.yml` (added 2019-10-02, deleted 2021-03-22), listed Hirsch's GitHub Sponsors and Ko-fi
accounts — personal sponsorship, naming no funding organization. No paper describes this software
(Field 14), so there is no acknowledgement section to read. Excluded: NASA, which appears in the
vendored Fortran only as the institution of individual routines' authors (`igrf.for`), an input's
provenance (rule 5); the funders of Goncharenko et al. (2021), a citing paper (rule 4); Boston
University and Cornell University, which are affiliations (Field 6).

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

**Source.** The same negative research as Field 25; no source attributes an award to this software.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.5281/zenodo.1493021
- https://doi.org/10.1029/2020JA028466
- https://doi.org/10.1029/2022SW003360
- https://doi.org/10.1029/2024SW004037
- https://doi.org/10.1029/2024JA032910

**`https://doi.org/10.5281/zenodo.1493021` — the model presentation the README points to (rule 4).**
Bilitza, D. (2016), *International Reference Ionosphere 2016*, Zenodo (DataCite type Text, resource type
Presentation, issued 2016-06-20; a 13-slide PDF). The slides cover IRI's terms of reference and working
group, the parameters and ranges it describes, its data sources and model providers, how the
electron-density profile is built, its strengths and weaknesses, the IRI-2016 changes (new hmF2 options,
improved ion composition) and IRI real-time. It is the only reference in `README.md`, the item "2016
presentation" under the heading "Notes", and so the project's own pointer to a description of the model
the software runs: the rule-4 case of "A publication the project presents as the basis of the software".
A slide deck is eligible only when it reads as a substantial standalone document; this one was judged to
pass: its terms-of-reference slide is full-sentence bullets, and its other slides are parameter and
data-source lists, tables and annotated build-up figures judged followable without the talk. It is
not Field 14's value: a presentation is never the reference publication, and it describes the model
rather than this package.

**Four papers that use the software (rule 5)**, each crediting it deliberately where rule 5 looks for
the credit:
- Goncharenko, L. P., Tamburri, C. A., Tobiska, W. K., et al. (2021), *A New Model for Ionospheric Total
  Electron Content: The Impact of Solar Flux Proxies and Indices*, Journal of Geophysical Research: Space
  Physics, doi:10.1029/2020JA028466. Acknowledgments: "The authors acknowledge the MATLAB interface to
  IRI‐2016 that was used in this study and available at https://github.com/space-physics/IRI2016" — this
  software's MATLAB interface, used for the paper's results.
- Chen, Z., Wang, K., Li, H., et al. (2024), *Storm-Time Characteristics of Ionospheric Model (MSAP)
  Based on Multi-Algorithm Fusion*, Space Weather, doi:10.1029/2022SW003360. Methods (§2.2): "In this
  paper, IRI TEC maps are calculated by the IRI-2016 model in the Python environment of Linux"; Data
  Availability: "The IRI-2016 model is derived from https://github.com/space-physics/iri2016".
- Salinas, C. C. J. H., et al. (2024), *Development of the Ionospheric E-Region Prompt Radio Occultation
  Based Electron Density (E-PROBED) Model*, Space Weather, doi:10.1029/2024SW004037. The paper states
  "This work runs IRI through a python wrapper" and describes `iri2016.IRI()` building the Fortran on
  first run; Data Availability: "IRI2016 is publicly available at https://pypi.org/project/iri2016/1.5.2/"
  (release 1.5.2 of this package).
- Ellahouny, N. M., et al. (2024), *EISCAT Observations of Depleted High-Latitude F-Region During an
  HSS/SIR-Driven Magnetic Storm*, JGR Space Physics, doi:10.1029/2024JA032910. Its Data Availability
  statement credits the "IRI-16 model Python package https://pypi.org/project/iri2016/"; the body names the IRI-2016
  model but makes no further statement about the package, but a Data Availability credit is one of the deliberate forms rule 5 names.

**Not widely used, so uses are still news.** The literature searches below find about ten papers that
name the repository or the PyPI package, of which these four credit it deliberately; rule 5's limit for
widely used software (list no users) does not apply. A later refresh should revisit that judgement only
if the count of deliberate uses grows large.

**Weighed and excluded.**
- Papers that run IRI-2016 by another route, not this package (rule 6): Forsythe, V. V., et al. (2021),
  Radio Science, 10.1029/2021RS007264 (IRI-2016 source from irimodel.org; its `space-physics` link is to
  the separate POLAN package); Mackovjak, S., et al. (2021), JGR Space Physics, 10.1029/2020JA028991
  (CCMC's IRI-2016 web interface); Ssessanga, N., et al. (2023), Space Weather, 10.1029/2023SW003584
  (irimodel.org); Chen, Z., et al. (2023), JGR Space Physics, 10.1029/2023JA031930 (CCMC's IRI-2016 web
  interface); Seba, E. B., et al. (2026), Space Weather, 10.1029/2024SW004321 (PyIRI, a different
  package). Each surfaces in a full-text search for `iri2016`, which also matches the model's name.
- Zolotov, O., et al. (2021), *pyFIRI — A free and open source Python software package of the
  non-auroral Earth's lower ionosphere*, SoftwareX, 10.1016/j.softx.2021.100885. Its full text could not
  be read; its reference list cites the IRI model papers but no `iri2016` software, and its code
  repository (`ElsevierSoftwareX/SOFTX-D-21-00148`) contains no `iri2016`, so it is treated as not a use.
  Reopen only if its text shows otherwise.
- Barta, V., et al. (2022), Frontiers in Environmental Science, 10.3389/fenvs.2022.904335 — runs IRI-2016
  from irimodel.org and uses a different `space-physics` repository (LWPC); not this software (rule 6).
- Yang, T. Y., et al. (2025), Scientific Reports, 10.1038/s41598-025-93628-8 — uses
  `space-physics/iri2020`, the author's separate IRI-2020 interface, not this software.
- Bilitza et al. (2017), Space Weather, 10.1002/2016SW001593, the IRI-2016 model paper — the repository
  never cites it, so rule 4 does not admit it (Field 14).
- The papers cited in the vendored Fortran's reference blocks (for example Picone et al. 2002 for
  NRLMSISE-00 in `cira.for`, Richards et al. 2010 for the IDC in `iriflip.for`, and the Truhlik et al.
  ion-composition and electron-temperature papers in `irifun.for`) — each is behind one routine of the
  vendored model, they are numerous, and listing them would bury the publications about this software
  (rule 4's long-list judgement: list none).

**Search record (2026-11-03).** ADS/SciX full text and acknowledgements for `"space-physics/iri2016"`,
`"github.com/space-physics/IRI2016"`, `"scivision/iri2016"`, `"scivision/pyIRI2016"`,
`"10.5281/zenodo.591802"`, `"iri2016"` with `"pypi"`, `"pip install iri2016"` and `ack:"iri2016"`; a
nonsense token returned zero and `"timduly4/pyglow"` returned hits. DataCite recorded no citations of
the concept DOI.

### 28. Related Datasets (OPTIONAL)
Not found

**Rule 4 candidates — the shipped coefficient and index tables — and why none can be recorded.** The
package ships and evaluates CCIR and URSI foF2/M(3000)F2 coefficient maps, IGRF coefficients in IRI's
own file format (`dgrf1945` … `dgrf2015`, `igrf2015`/`igrf2015s`, `igrf2020`/`igrf2020s`, i.e. the
IGRF-13 generation), `mcsat` tables, and the `apf107.dat`/`ig_rz.dat` index files. None has a DOI or a
permanent landing page for the exact release shipped (rule 8):
- A DataCite search (2026-11-03) finds nothing for `apf107`, `ig_rz`, CCIR or URSI coefficients, or an
  IRI dataset; its two IGRF-13 "datasets" are supplementary files of a paper.
- `10.5281/zenodo.11269409` is a third-party Zenodo archive of IGRF-13 coefficients made for another
  project; it is not the files this package ships (the IRI-format `.dat` files), so it is not recorded.
- `http://irimodel.org/indices/`, which the README links, serves the current index files, not the
  2019/2020 releases the package ships; rule 4 wants the exact shipped release, so a page for the latest
  ones would point users at data the software does not carry.
These tables are recorded under Field 18 instead.

### 29. Related Software (OPTIONAL)
- https://github.com/rilma/pyIRI2016
- https://irimodel.org/

**`https://github.com/rilma/pyIRI2016` — the fork parent and code origin (rule 9).** Evidence in this
repository: its git history begins with Ronald Ilma's commits from 2016-12-09 ("Initial version") through
2017-05-02, including `8f25250`, the commit `rilma/pyIRI2016`'s `v1.1.0` tag points at; `LICENSE.txt` keeps `Copyright (c) 2017 Ronald Ilma`;
the README still carries `rilma/pyIRI2016`'s Zenodo badge; and this software's own deposits list Ilma as
a creator. HSSI catalogues it as `pyIRI2016`, so the URL is that entry's stored `code_repository_url`,
byte for byte (rule 11). The URL form was chosen over the DOI that entry carries
(`10.5281/zenodo.240895`, a legacy version DOI with no concept DOI) because the site shows the raw URL
as link text (rule 13).

**`https://irimodel.org/` — the upstream model this package vendors and runs (rule 9: the original code
it wraps).** The repository's GitHub homepage is `http://irimodel.org/`; the README sends users to
`http://irimodel.org/indices/` for the index files; and the 2023-06-29 commits "irisub.for: upstream and
apply our own Python interface patch", "irifun.for upstream and apply our patches for Python", "igrf.for
upstream and patch for python" and "iritest upstream" pulled the IRI-2016 Fortran from that
distribution. The IRI Fortran has no public repository and no DOI, so the model's official site is the
value (rule 12(c)); the catalogue already holds a related-software row with exactly this URL (from
`pyIRI2016`), so it binds. The site offers the IRI-2016 Fortran, the common coefficient files and the
indices files; it may refuse non-browser clients, which is not a dead link.

**Considered and not listed.**
- `https://github.com/space-physics/iri90` (HSSI's `IRI-90`) and `https://github.com/space-physics/iri2020`
  — the same author's interfaces to the IRI-90 and IRI-2020 generations, built from the same template
  (`iri2020` was created on 2023-06-29, the day of this repository's last upstream refresh, and its
  README copies this one's, the `240895` DOI badge included). Neither repository names the other, and
  nothing in this repository names either, so rule 9's similar-purpose route (the project names it as an
  alternative) and rule 4 (support from this software's sources or developers) are not met. Open lead:
  add them if the project ever links them. When this record was submitted, HSSI's `IRI-90` entry listed
  this repository in its own Field 29, so that relation runs one way only.
- `https://github.com/timduly4/pyglow` (HSSI's `pyglow`) — another Python route to IRI-2016, but this
  project never names it (rules 4 and 9). Open lead on the same terms.
- `space-physics/msise00`, `space-physics/igrf` — the NRLMSISE-00 and IGRF routines IRI uses are the
  copies vendored inside the IRI Fortran (`cira.for`, `igrf.for`), not those packages (rule 5).
- numpy, python-dateutil (Tier A); xarray (Tier B, recorded in Field 30 on its exchange, not here);
  setuptools, wheel, CMake, gfortran, pytest, flake8, mypy (generic build and test tooling); matplotlib
  (Tier A, optional).
- MATLAB — a runtime already in Field 13 (rule 5); its interface relation is in Field 30.
- The MATLAB File Exchange listing `81056-iri2016` — a distribution page for this same software.

**Inbound references in the catalogue (as of this submission, 2026-11-03).** `pyIRI2016`'s Field 29
referred to this software by the concept DOI `https://doi.org/10.5281/zenodo.591802`, and `IRI-90`'s by
`https://github.com/space-physics/iri2016` (this entry's Field 3). Under Field 29's URL rules,
`pyIRI2016`'s DOI-form reference should become this entry's repository URL at that entry's next refresh.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/pydata/xarray
- https://www.mathworks.com/products/matlab.html

**`https://github.com/pydata/xarray` — the public API's interchange type (Tier B, rule 4).** The three
exported functions return xarray objects: `IRI(...) -> xarray.Dataset` (`src/iri2016/base.py`), and
`timeprofile(...) -> xarray.Dataset` and `geoprofile(...) -> xarray.Dataset` (`src/iri2016/profile.py`).
The datasets carry named variables (`ne`, `Tn`, `Ti`, `Te`, the ion densities, `NmF2` … `foF2`, `TEC`),
coordinates (`time`, `alt_km`, `glat`, `glon`) and run attributes (`f107`, `ap`). The shipped example
notebook works with them as datasets (`sim.time`, `sim.alt_km`, `sim.ne`), `plots.py` consumes them, and
the latitude CLI writes one out with xarray's `to_netcdf`. Recorded as the upstream repository root
(rule 12(a)); xarray's concept DOI `10.5281/zenodo.598201` was passed over because the site renders the
raw URL. The catalogue holds other xarray rows (`https://xarray.dev`, `https://docs.xarray.dev/`); this
form is the prescribed one and already exists as a row.

**`https://www.mathworks.com/products/matlab.html` — a MATLAB interface (rule 7).** The `+iri2016`
MATLAB package runs the same compiled driver and returns a MATLAB struct (`iri2016.iri2016`), with
plotting (`plotiono`, `plottime`), a `matlab.unittest` suite (`TestUnit.m`, `TestAll.m`), a
`buildfile.m`, examples (`Examples/AltitudeProfile.m`, `Examples/TimeProfile.m`), a README section and a
File Exchange listing. The catalogue already holds a related-item row with exactly this URL, used by
other Python-and-MATLAB model interfaces, so it binds that row rather than minting a variant. Caveat
(Field 13): the
MATLAB auto-build helper calls a `setup.cmake` deleted in 2021, so MATLAB users need the driver built
first.

**Considered and not listed.** numpy, python-dateutil, matplotlib (Tier A). netCDF4/scipy (the
`to_netcdf` backends — not declared, generic I/O). Jupyter (one example notebook; no kernel, widget or
extension). `rilma/pyIRI2016`, `iri90`, `iri2020`, `pyglow` — no exchange with this software in either
direction.

### 31. Related Instruments (OPTIONAL)
Not found — a relevance decision, not a lookup failure

**Rule 2.** IRI is a global empirical climatology evaluated at any location; the software reads,
calibrates or processes no instrument's data and is not an instrument-team tool. A user searching for an
instrument would not expect it back.

**Where instrument and facility names occur, and why none qualifies.** Every occurrence is in the
vendored IRI Fortran comments, recording which observations an empirical sub-model was fitted to or
validated against, plus one switch label in the retired `.archive/legacy.py`
(`# 23 Te_tops (Aeros,ISIS)`). Representative lines at the pin: `irisub.for:1856` "Te-MAXIMUM based on
JICAMARCA and ARECIBO data"; `irifun.for:6492` "observations by space ionosondes ISIS 1,ISIS 2, and
IK19"; `irifun.for:4749` "(by AE-C, and AE-E)"; `irifun.for:4929` "(by IK24)"; `irifun.for:3471`
"based on C/NOFS CINDI data"; `iriflip.for:1227` "the Atmosphere Explorer-E PES fluxes". A
case-insensitive, word-anchored search finds none of these names in the Python package, the driver, the
MATLAB package, the README or the build files; the one hit outside the vendored model files is a comment
in the test-only `src/test.f90` (`!Te: Aeros/AE/ISIS model`), which echoes IRI's own label for its
electron-temperature option. Fitting heritage is not designed-to-support (rules 3–4).

**Fitting rows exist and were declined.** The vocabulary sweep (name, abbreviation, identifier and
definition; `SUVI` as the positive control, a nonsense word as the negative) finds instrument rows for
the hardware the comments name, among them `https://spase-metadata.org/SMWG/Instrument/ISIS1/SFS`
("ISIS1 Swept-Frequency Sounder"), `https://spase-metadata.org/SMWG/Instrument/ISIS2/SFS`,
`https://spase-metadata.org/SMWG/Instrument/AE-E/PES`… (the Atmosphere Explorer instrument families
under `SMWG/Instrument/AE-C/` and `AE-E/`), `https://spase-metadata.org/SMWG/Instrument/CNOFS/CINDI`
("Coupled Ion-Neutral Dynamics Investigation") and the `Aeros-A` instruments. The three `Jicamarca` rows
are a magnetometer and a GIRO ionosonde station at that site, not the radar the comment means. No row
exists for Arecibo, IK19 or IK24, or for IRI itself. None is used, for the relevance reason above.

### 32. Related Observatories (OPTIONAL)
Not found — a relevance decision, not a lookup failure

**Same examination as Field 31.** The software targets no mission, platform or facility. It is not the
"Mission observational record only" case (Field 32 rule 2) either: IRI's coefficients come from decades of
ground and space data from many networks and missions, not from one mission's record, and the package
reads none of their data.

**Fitting rows exist and were declined.** Observatory rows exist for spacecraft the vendored comments
name: `https://spase-metadata.org/SMWG/Observatory/ISIS1`, `…/ISIS2` and the programme-level `…/ISIS`
(all named "International Sats for Ionosph Studies"), `https://spase-metadata.org/SMWG/Observatory/AE-C`
and `…/AE-E` (Atmosphere Explorer-C and -E), `https://spase-metadata.org/SMWG/Observatory/Aeros-A`
("Aeros A") and `https://spase-metadata.org/SMWG/Observatory/CNOFS` ("Communication/Navigation Outage
Forecasting System"). Selecting any would assert that this software supports that mission's data, which
it does not. Field 17 carries no `Observatory/Mission-specific` value, consistent with this.

### 33. Logo (OPTIONAL)
https://spdf.gsfc.nasa.gov/research/IRI/website/doc/images/red_band-179.jpg

**What the image is.** A 179 × 134 JPEG (19,072 bytes, `image/jpeg`): a photograph from orbit of an
aurora over Earth's limb, red above green. It is a decorative image from the IRI project's website at
NASA SPDF, not a mark this repository ever published. Stated so a later refresh does not "discover" it
and reopen the question.

**Why it is the value (rule 2).** The PyHC registry entry whose `code:` is this repository
(`IRI-2016` in `_data/projects_unevaluated.yml`, registry commit `b1e3c973`) presents
`https://iri.gsfc.nasa.gov/images/red_band-179.jpg` as the project's logo. That URL redirects permanently
to the value above, which serves a byte-identical image (SHA-256
`7b000e69cefaa17e3f1415261fc117ff98fd359e8a3b815ce7a7ee4d429a34ed` for both); the redirect target is
stored because it does not depend on the redirect surviving (rule 9). It is not git-hosted, so there is
no commit to pin. The sibling `IRI-90` entry uses the companion image from the same site, chosen by its
own registry entry the same way.

**Not this logo's twin — a trap recorded elsewhere.** The `pyIRI2016` dossier records that this image
must not be used for `rilma/pyIRI2016`, because the registry entry that presents it belongs to this
repository. The two records agree.

**Rejected alternative.** The README's header image,
`https://raw.githubusercontent.com/space-physics/iri2016/ca523ad80d22c25e95ecb2f95d37094cb7adb035/figures/iri2DExample02.gif`
(`image/gif`, 683 × 319, an animated global map of foF2 for 2010-09-21), sits in the hero position but
is an example model-output figure, inherited from `rilma/pyIRI2016` (added 2016-12-09), of a capability
this package no longer has (Field 8). Nothing presents it as branding (rule 4). The other `figures/*.png`
are example plots and are excluded for the same reason. There is no logo file, docs site or `html_logo`.
