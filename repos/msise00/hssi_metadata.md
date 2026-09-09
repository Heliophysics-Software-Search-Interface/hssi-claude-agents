# HSSI Metadata Extraction Results

**HSSI Software ID:** 2bccae2a-78df-4ce5-b6b3-40afea73fe4d
**Repository:** https://github.com/space-physics/msise00
**Source Revision:** e4ab457c4e3f252c7ce748826d1e137ec9c563c0
**Extraction Date:** 2026-09-08
**Validation Date:** 2026-09-08
**Validation Status:** PASS

---

**Scope note — where the software actually lives.** This repository holds two independent user-facing
paths onto one compiled Fortran core, and several fields only make sense once that is clear. The core
is the NRL MSISE-00 Fortran in `src/msise00/fortran/`, compiled to a standalone executable
(`msise00_driver`) by `src/msise00/CMakeLists.txt`. The Python package (`src/msise00/`) and the MATLAB
package (`+msise00/`) each shell out to that executable and parse its stdout; neither links it as a
library. A third tree, `reference/`, holds the unmodified NRL originals and a hand-written `Makefile`
that the package's own CMake project never reaches — the root `CMakeLists.txt` contains only
`add_subdirectory(src/msise00)`. A fourth, `.archive/`, holds the retired f2py-based implementation and
is excluded from the project's own type checking. Evidence drawn from `reference/` or `.archive/` is
therefore evidence about heritage or history, not about what a user runs, and is labelled as such below.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.595393
- **Source:** DataCite, which mirrors the Zenodo deposit metadata.
- This is the Zenodo **concept** DOI, and the DOI record proves it rather than assuming it: the record
  carries twenty-four `HasVersion` relations to per-release DOIs (among them
  `10.5281/zenodo.14532758`, the v1.11.1 release DOI recorded in Field 12), which is the shape only a
  concept record has. A concept DOI is the right value for this field because it resolves to whichever
  release is current, so the citation a visitor copies does not silently pin them to v1.11.1 forever.
- The same record also carries `IsSupplementTo https://github.com/space-physics/msise00/tree/v1.11.1`,
  the signature of Zenodo's GitHub release integration. That matters for a future refresh: because the
  deposit is integration-generated rather than hand-uploaded, its creator list and title are derived
  from the GitHub release, which is why Field 6 and Field 12 below trace back to GitHub rather than to
  a hand-curated citation file.
- Registered 2017-05-30; the record's own `version` field reads `v1.11.1` and its title is
  `space-physics/msise00: Python bugfix for Python 3.9`.

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/space-physics/msise00
- **Source:** the repository itself, corroborated by the DOI record's `IsSupplementTo` target and by
  the PyHC registry's `code:` value for this package.
- **This URL is load-bearing beyond this entry.** Four other HSSI entries — GLOW, HWM-93, ReesAurora
  and ScienceDates — name this exact URL as their own related software, stored as literal URLs rather
  than as references to this entry. Changing it here would strand those pointers silently. If the
  repository is ever moved or renamed, those four entries must be updated in the same pass.

### 4. Software Functionality (RECOMMENDED — treated as critical)
- **Values:**
  - Data Processing and Analysis
  - Data Processing and Analysis: Data Access and Retrieval
  - Data Visualization
  - Data Visualization: 2D Graphics
  - Data Visualization: Line Plots
  - Models and Simulations
  - Models and Simulations: Empirical

**Why each value is here.**
- *Models and Simulations* / *Empirical* — this is the whole point of the package. The NRL source it
  wraps documents itself in `src/msise00/fortran/msise00_sub.f` as a "Neutral Atmosphere Empirical
  Model" reaching from the surface to the lower exosphere (that phrase runs across two comment lines
  in the source, so only the quoted fragment is verbatim), and the model is a fit to satellite drag,
  mass spectrometer and incoherent scatter data rather than a solution of the governing equations.
- *Data Processing and Analysis: Data Access and Retrieval* — a default run reaches out to the network
  before it can compute anything. `src/msise00/base.py` calls `gi.get_indices(time, smoothdays=81)`
  whenever the caller does not supply indices, and the test suite's own skip message —
  `pytest.skip("unable to download RecentIndices.txt")` in `src/msise00/tests/test_module.py` — names
  the file being fetched. A user who selects this facet and finds MSISE-00 gets a true answer: they can
  call one function and have the driving indices retrieved for them.
- *Data Visualization* / *Line Plots* / *2D Graphics* — plotting is a first-class, dual-language
  feature, not a demo. In Python, `src/msise00/plots.py` provides `plot1dalt` and `plot1dtime`
  (`semilogx`/`plot` altitude and time profiles → Line Plots) and `plot2dlatlon` (`imshow` of eight
  species over a lat/lon grid → 2D Graphics), reachable from the `msise00` command line unless `-q` is
  passed. In MATLAB, `+msise00/plotalt.m` and `+msise00/plottime.m` provide the same two profile plots
  and are exercised by `+msise00/TestUnit.m`'s `test_plot_alt` and `test_plot_time`.

**Considered and rejected — with the reason, so these are not re-proposed.** Every branch of the
functionality taxonomy was considered, not only the ones adopted. The following came closest and
still fail:

- *Coordinate Transforms* (and its `Solar` child). `src/msise00/plots.py` genuinely performs one: it
  takes the Sun's apparent position from `astropy.coordinates.get_sun`/`AltAz` and converts it to a
  geodetic footprint with `pymap3d.aer2geodetic`, and `Examples/suntest.py` demonstrates that
  conversion on its own. It is rejected because no public function exposes it — its only effect is a
  white marker drawn on a density map, and a user who selected this facet expecting a coordinate
  utility would have been misled.
- *Data Visualization: Movies*. The README's caption "MSIS global time animation" and the checked-in
  `src/msise00/tests/msise00_demo.gif` suggest animation, but the package cannot produce one. A
  case-insensitive search of every tracked file at this revision for
  `animation|FuncAnimation|imageio|ffmpeg` matched only that README caption and nothing in any source
  file, against a control search for `matplotlib` that matched seven files. `plot4d` writes one PNG per
  time step; assembling them into the GIF was done outside the repository.
- *Data Visualization: 2D Slices*. The README says the hero plot "shows a slice at 200km on a
  world-wide grid", which is tempting. It is rejected because the plotting code never extracts a plane
  from a stored volume: `run` computes the field at the requested altitude and `plot2dlatlon` displays
  exactly what was computed, calling `atmos.alt_km.item()` — a call that presumes a single altitude.
  There is no volume to slice.
- *Models and Simulations: Data Guided*. The model is driven by observed F10.7 and Ap. Rejected because
  those are two scalar activity indices feeding an empirical fit, not a data-driven boundary or state;
  a visitor filtering this facet is looking for assimilative models and would not want a climatology.
  The retrieval half of that idea is already carried by *Data Access and Retrieval*.
- *Models and Simulations: Forecasting*. `src/msise00/tests/test_module.py` contains a `test_forecast`
  that runs the model at `datetime(2029, 3, 31, 12)` and asserts concrete temperatures, so future-dated
  runs do work (the index dependency supplies predicted values). Rejected because the forecast skill
  lives in the index provider, not here; MSISE-00 itself is a climatology evaluated at whatever indices
  it is handed.
- *Models and Simulations: Physics-Based* and *First Principles*. Rejected in favour of the precise
  label. The model's altitude profiles have physical form, but its coefficients are fitted; *Empirical*
  is the term the model's own documentation uses.
- *Data Processing and Analysis: Analysis*, *Processing*, *File Format Conversion*. Rejected. Marshalling
  the driver's stdout into a dataset, merging grid points with `xarray.merge` and writing netCDF is
  plumbing around a model evaluation, not scientific analysis of data the user brought. Converting an
  xarray object to a MATLAB matrix (`+msise00/python-matlab/xarray2mat.m`) is an in-memory data-model
  conversion, not a file format conversion.
- *Servers and Environments* (any child). Rejected: no server, no HPC parallelism, and the same
  case-insensitive whole-tree search found no `docker`, `singularity`, `apptainer` or `mpi4py`. The
  build is CMake driven from Python or MATLAB.

### 5. Related Region (RECOMMENDED — treated as critical)
- **Values:**
  - Earth Atmosphere
  - Earth Lower and Middle Atmosphere
  - Earth Thermosphere

**Why the two additions.** The `Region` vocabulary is flat: no value implies any other, so the coarse
`Earth Atmosphere` that the record already carried does not make the software discoverable to anyone
filtering for the specific layers it covers. The software covers them explicitly. `README.md` line 10
states "Valid from altitude z = 0..1000 km.", and the NRL header in
`src/msise00/fortran/msise00_sub.f` documents a "Neutral Atmosphere Empirical Model" spanning the
surface to the lower exosphere. Ground to
1000 km spans the troposphere, stratosphere and mesosphere (Earth Lower and Middle Atmosphere) and the
thermosphere, and the model's principal outputs are thermospheric: `Texo` is the exospheric
temperature, and the anomalous-oxygen term the NRL source documents exists specifically to serve
satellite drag calculations above 500 km. A visitor filtering on `Earth Thermosphere` who did not get
MSISE-00 back would be right to consider the catalogue broken.

**Consequence worth stating.** HWM-93 — the companion NRL empirical model in the same wrapper family,
with the same ground-to-exosphere validity range — carried `Earth Atmosphere`,
`Earth Lower and Middle Atmosphere`, `Earth Thermosphere` and `Earth Ionosphere` when this dossier was
written, and LOWTRAN carried the lower-and-middle-atmosphere value. On the two layer values recorded
above, a user comparing MSISE-00 against its own siblings would have found it the thinnest of the group
on a facet where it is no narrower in fact. (It remains one value short of HWM-93 on this facet, and
deliberately so — see the ionosphere decision below.) This is stated as a consequence, not as a
precedent: the argument above rests on the model's own stated validity range and stands with no sibling
in view.

**`Earth Ionosphere` was considered and deliberately not added.** The case for it is real, was
weighed, and is recorded here so that a later refresh recognises this as a judgement already made
rather than a value someone missed. That case: the model's 0–1000 km validity range is precisely the
ionospheric altitude range; MSIS neutral densities are the standard input to ionospheric conductivity,
collision-frequency and ionization-rate calculations, which is exactly why GLOW and ReesAurora in this
catalogue depend on this package; and every close neighbour carried the value — HWM-93, IRI-90, GLOW
and ReesAurora all did when this dossier was written. None of that is refuted by the decision.

It was decided from the searcher's side. MSISE-00 is a **neutral** atmosphere model: it returns He, O,
N2, O2, Ar, H, N, anomalous O, total mass density and two temperatures, and no electron density, no ion
composition, no plasma quantity of any kind. Someone filtering `Earth Ionosphere` is looking for
software about the ionosphere and would get a model that computes nothing ionospheric — so the value
costs that searcher more than it gains this entry. Being an *input to* ionospheric work is not the same
as modelling the ionosphere, and the Region facet records the latter. If the question is ever reopened,
it should be reopened on what the Region facet is for, not on the evidence above, which is already
here and was not found wanting.

### 6. Authors (MANDATORY)

#### Author 1:
- **Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** https://ror.org/05qwgg493
  - **Organization:** Scivision, Inc.
  - **Affiliation Identifier:** Not found — see the note below; none exists.

#### Author 2:
- **Name:** Daniel Kastinen
- **Author Identifier:** https://orcid.org/0000-0002-6371-1016 — correct value established here; must
  be applied database-side, see the note below.
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11

#### Primary Contact:
- **Name:** Michael Hirsch
- The PyHC registry entry for this package gives `contact: Michael Hirsch`. Same person as Author 1.

**Why exactly these two, and why no more.** The author set is the union of every source that credits
anyone: the two names the record already held, the two Zenodo creators on the concept DOI (`scivision`
and `Daniel Kastinen`, the latter with affiliation `Institutet för rymdfysik`), and the commit history.
Nobody is dropped. The repository has no machine-readable citation metadata to reconcile against — and
this is a historical claim, not a claim about the current tree: searching every path ever added on this
revision's ancestry for `citation|zenodo|codemeta|mailmap|funding|contribut|author` matched exactly one
file, `.github/FUNDING`, out of 131 distinct added paths, with a control search for `readme` matching
three. There has never been a `CITATION.cff`, `.zenodo.json`, `codemeta.json` or `.mailmap` here, and
`pyproject.toml` declares no `authors` table. So GitHub and Zenodo are the only author evidence there is.

**Michael Hirsch — one person behind six git identities.** `git shortlog -sne` at this revision lists
six author identities, and all but one are him: `scivision`, `Michael Hirsch, Ph.D` and
`Michael Hirsch` at `scivision@users.noreply.github.com`, plus `Michael Hirsch, Ph.D` and `Michael` at
`10931741+scivision@users.noreply.github.com`. Both addresses are GitHub noreply forms of the login
`scivision` (the numeric prefix is that account's id), which is also the Zenodo creator name, since the
deposit is integration-generated and inherits the GitHub handle rather than a personal name.

**Michael Hirsch — why this ORCID.** `https://orcid.org/0000-0002-1637-6526` is a Research Scientist in
Electrical and Computer Engineering at Boston University (from 2018), whose eighteen public works are
auroral, ionospheric and scientific-software papers, including *PyMap3D: 3-D coordinate conversions for
terrestrial and geospace environments* (10.21105/joss.00580) and *h5fortran* (10.21105/joss.02842) —
both packages by this author and both in the same geospace-code/space-physics family as MSISE-00. A
fielded ORCID search on the name returns seven records, so a bare-name match would not be safe; the
identification rests on the works and the Boston University employment, not on the name.

*Rejected alternative — do not reintroduce it.* `https://orcid.org/0000-0001-6183-6256` was recorded
for this author in an earlier revision of this dossier and is **wrong**. It belongs to a different
Michael Hirsch: Science and Technology Facilities Council and Leipzig University, whose published work
is single-molecule fluorescence microscopy, receptor biophysics and EMCCD detector physics — no
heliophysics, no geospace, no software. It appears in the same seven-record name search as the correct
ORCID, which is exactly why the name alone cannot settle this field.

**Daniel Kastinen — identifier newly established, and how it must be applied.** No identifier was
recorded on HSSI for this author before this refresh, and this refresh does not add one, for the reason
set out at the end of this paragraph. The correct value is `https://orcid.org/0000-0002-6371-1016`. A
fielded search on `given-names:Daniel AND family-name:Kastinen` returns exactly one record (the same
search shape returns seven for Michael Hirsch, so it is discriminating rather than merely lucky), and
three independent things bind that record to this contributor: its employment is Scientist at
`Institutet för rymdfysik` in the department "Solar Terrestrial and Atmospheric Research", disambiguated
to `https://ror.org/043kppn11` — the identical ROR already stored for his affiliation here; his single
commit to this repository is authored as `danielk <daniel.kastinen@irf.se>`, and `irf.se` is that
institute's domain; and his publications include *Monitoring of lower thermospheric neutral density
variations using meteor head echoes*, which is the very quantity this package computes.
**This value must not be sent through a routine metadata update.** The stored person record for him
already exists without an identifier, and supplying one that way mints a second person record and
orphans the first, splitting his authorship across two entities. It has to be written directly to the
existing record. Until that happens the divergence persists, and a future refresh should treat this
paragraph as the pending item rather than re-deriving the ORCID.

**A one-commit author is still an author.** His contribution at this revision is a single commit
(`c89d8d9`, 2021-06-24, "update example to conform to wrapper API", modifying
`Examples/AltitudeProfile.m`). Commit volume is not the test: he is a named creator on the software's
own DOI record, which is the project's own act of credit, and a low commit count is not grounds to drop
a credited author.

**Affiliations — why two for Hirsch, and why one of them has no identifier.** Boston University comes
from his ORCID employment record and carries the ROR above. `Scivision, Inc.` is his company, evidenced
in-repository by `LICENSE.txt`, whose copyright line reads `Copyright (c) 2015-2025 SciVision, Inc.`,
and by the GitHub login the commits and the Zenodo creator name both use. **No ROR record for this
company was discoverable, and a future agent should not attach the near-match.** As of 2026-09-08 a ROR
search for SciVision returned a single organization, `https://ror.org/011qev639` — *SciVision Biotech
Inc. (Taiwan)*, a Kaohsiung company at `scivision.com.tw`. The durable point does not depend on what
the registry holds later: that record is a different entity, so attaching it would be a factual error
rather than a harmless approximation, and it stays the wrong answer however the registry changes.
Separately, the organization name stored here is `Scivision, Inc.` while the company's own spelling, in
the repository's `LICENSE.txt` at this revision, is `SciVision, Inc.` with a capital V. **This is a
known and parked divergence: it is not to be fixed, and it blocks nothing.** The name lives on an
organization record shared with other entries rather than on this one, and such names are not
rewritable through a metadata update in any case. It is recorded here only so that a future refresh
recognises it as already known, and does not reopen it as a finding, a correction task, or a reason to
hold this entry.

### 7. Software Name (MANDATORY)
- **Name:** MSISE-00
- **Full Title:** MSISE-00 in Python and Matlab
- **Alternate Name:** msise00
- The short form is the PyHC registry's `name:` for this package and the form a heliophysicist
  recognizes; the full title is the README's own heading (`README.md` line 1,
  `# MSISE-00 in Python and Matlab`); the lower-case form is the repository, PyPI and Python import
  name. The hyphenated `MSISE-00` is the deliberate choice: it distinguishes the catalogue entry
  from the bare model name while remaining what a searcher types.

### 8. Description (MANDATORY)
- **Description:** NRL MSISE-00 atmospheric model-- in Python and Matlab. Python API for Fortran MSISE-00 neutral atmosphere model. The MSISE-00 model provides atmospheric temperature and density from ground to thermospheric heights. Valid from altitude z = 0..1000 km. Outputs include temperature (Kelvin), density (particles per cubic meter), and mass density (kilograms per cubic meter).
- Every clause is traceable and every clause is true, so the wording is left alone. The opening is the
  project's own one-line description (identical in the GitHub repository description, the DOI record's
  abstract and the PyHC registry `description:`); the second sentence is `pyproject.toml`'s
  `description`; the validity range is `README.md` line 10; and the units come from the README's own
  "Units" section, which gives temperature in degrees Kelvin, density in particles per cubic meter and
  mass density in kilograms per cubic meter.
- The doubled hyphen in "model--" is the project's punctuation, reproduced from its own description
  rather than tidied. A future refresh should not "fix" it: matching the project's self-description is
  what lets a visitor recognize that this catalogue entry and that repository are the same thing.

### 9. Concise Description (OPTIONAL)
- **Concise Description:** NRL MSISE-00 atmospheric model-- in Python and Matlab
- This is the project's own single-line summary, appearing identically as the GitHub repository
  description, the DOI record's abstract, and the PyHC registry `description:`.

### 10. Publication Date (RECOMMENDED)
- **Date:** 2015-03-27
- The date the repository began: commit `8366796` ("Initial commit") is dated 2015-03-27, and the
  GitHub repository's `created_at` is the same day. Note that this is deliberately *not* the
  DOI's registration date (2017-05-30) or the current release date (2024-12-19) — the field records
  when the software was first published, and the release date is carried by Field 12.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- The DOI record's `publisher` is `Zenodo`, the deposit's publisher of record; the recorded identifier
  is Zenodo's own root URL.
- **No ROR record exists for Zenodo as named, so the root URL is the correct identifier here and a
  future refresh need not repeat the search.** A ROR query for Zenodo returned no organization at all
  when checked on 2026-09-08. The near-match to avoid is CERN, which operates Zenodo and is a distinct
  registrant with its own ROR, `https://ror.org/01ggx4157` (European Organization for Nuclear
  Research). Attaching that would name the operator rather than the publisher of record, and it stays
  the wrong answer however the registry changes.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.11.1
- **Version Date:** 2024-12-19
- **Version Description:** Python bugfix for Python 3.9
- **Version PID:** https://doi.org/10.5281/zenodo.14532758

**Why v1.11.1 is still current even though the source revision is much later.** This is the ordinary
released-then-developed-further shape, not a stale record, and each alternative was checked and ruled
out. The tag `v1.11.1` (`3659c30`, 2024-12-19) is an ancestor of the source revision, so it is not on
an orphan lineage. `src/msise00/__init__.py` at the source revision still reads
`__version__ = "1.11.1"`, so there is no declared-but-unreleased bump to catch up with. The fourteen
commits between the tag and the source revision are compiler, CI, typing and test maintenance
(gfortran 15, Python ≥ 3.11, pre-commit, test-data regeneration after a NumPy ABI change) — real work,
but no release. PyPI's latest `msise00` is 1.11.1, uploaded 2024-12-19, and GitHub's newest release is
`v1.11.1`, published the same day.

**Where the description comes from.** `Python bugfix for Python 3.9` is byte-for-byte the GitHub
release's own `name` for `v1.11.1`, and that release's `body` is empty — so the title is the whole of
the maintainer's release note, and the stored description is authoritative on that basis alone. It is
not inherited from the previous tag: `v1.11.0`'s release name is the visibly different `return empty
Dataset on error rather than ValueError`. Two further points are recorded so they are not later
mistaken for errors. First, the release title is independently corroborated from inside the correct
range. Of the seven commits in `v1.11.0..v1.11.1` — a range whose endpoints are ancestry-checked,
`v1.11.0` being an ancestor of `v1.11.1` and `v1.11.1` an ancestor of the source revision — six are
MATLAB and CI work, and the remaining one, `2119b52c`, is the Python fix the title names. Its subject
line reads `ci: add windows`, but its message body opens `fix annotations for Python 3.9`, and its diff
adds `from __future__ import annotations` to `src/msise00/plots.py` while bumping
`src/msise00/__init__.py` from `__version__ = "1.11.0"` to `"1.11.1"` — so it is both a genuine Python
3.9 compatibility fix and the commit that produces this release. Read the subject lines alone and the
title looks unsupported; read the bodies and it is exact. Second, "Python 3.9" looks wrong against the
source revision's
`requires-python = ">=3.11"`, but at both `v1.11.0` and `v1.11.1` `pyproject.toml` declared
`requires-python = ">=3.9"`, and the published PyPI release still reports `>=3.9`. The floor was raised
later, in the post-release maintenance described above. The title was accurate when written.

**PyPI identification.** The package name is genuinely this software's, established without relying on
the name alone: `home_page` and `project_urls` are both absent from the PyPI record, so the binding is
the `summary`, `Python API for Fortran MSISE-00 neutral atmosphere model.`, which is byte-identical to
`pyproject.toml`'s `description` at this revision, together with a latest version and upload timestamp
that match the GitHub release.

### 13. Programming Language (RECOMMENDED)
- **Languages:**
  - Fortran77
  - Fortran90
  - Fortran 2003
  - Fortran 2008
  - MATLAB
  - Python 3.x

**The criterion, stated once and applied to everything.** This field records the language editions
someone must be able to compile or run in order to use this software. Everything below follows from
that single test, applied over a closed candidate set (the tracked source files at this revision:
17 `.py`, 14 `.m`, 6 `.f90`, 3 `.for`, 3 `.f`, plus the MATLAB package directory `+msise00` and the
root `buildfile.m`).

It is worth saying plainly that the competing criterion — *catalogue every language edition present
anywhere in the tracked tree*, a paraphrase rather than a quotation — yields the **same six values
here**, because the newest constructs in the tree all appear among the three files the package actually
compiles. The two criteria differ only in whether the reasoning is recorded, not in the outcome, so
this is not an open question; it is written down so a future refresh does not reopen it.

**Why each edition.**
- *Python 3.x* — the package under `src/msise00/`, with `requires-python = ">=3.11"`.
- *MATLAB* — not incidental. `+msise00/` is a full MATLAB package (`msise00.m`, `plotalt.m`,
  `plottime.m`, a `private/` build helper), `buildfile.m` defines MATLAB build and test tasks,
  `+msise00/TestUnit.m` is a `matlab.unittest.TestCase` suite, and a dedicated CI workflow runs MATLAB
  R2024b on Linux, macOS and Windows. A MATLAB user can use this software without touching Python.
- *Fortran77* — the compiled core `src/msise00/fortran/msise00_sub.f` and `msise00_data.f` are
  fixed-form NRL source, and the build compiles them with `-std=legacy` under GNU
  (`src/msise00/CMakeLists.txt`), which is exactly the accommodation legacy fixed-form code needs.
- *Fortran90* — those same fixed-form files are wrapped in a Fortran 90 `module` with
  `private`/`public`/`contains`, and `msise00_driver.f90` is free-form.
- *Fortran 2003* — `msise00_driver.f90` uses `use, intrinsic:: iso_fortran_env`,
  `command_argument_count()`, ten `get_command_argument` calls and a square-bracket array constructor;
  `msise00_sub.f` also uses `use, intrinsic :: iso_fortran_env`.
- *Fortran 2008* — `msise00_sub.f` uses the `error stop` statement, at lines 1233 and 1596. Both are
  executable statements inside `IF` blocks, not comments (fixed-form comments here begin with `C` in
  column one). This is the newest edition required, so a Fortran 95 compiler cannot build this
  software — which is precisely the fact this field exists to tell a user.
- *To be exact about the distribution across the compiled files,* because the build fact and the
  construct fact are easy to misread as contradicting each other: the build compiles **three** files —
  `msise00_sub.f` and `msise00_data.f` into an object library, `msise00_driver.f90` into the
  executable. All three are Fortran 90 or later in form (the two fixed-form `.f` files are wrapped in
  modules; the `.f90` is free-form), and the 2003 and 2008 constructs sit in **two of the three**.
  `msise00_data.f` is a module-wrapped table of model coefficients and carries none of them: a search
  of that file for `error stop`, `iso_fortran_env`, `get_command_argument` and
  `command_argument_count` returns nothing, while the same search over the other two compiled files
  matches both.

**Why the two additions rather than leaving the stored pair.** The record previously listed only
Fortran77 and Fortran90, which understates the compiler a user needs. The additions are not a
reclassification of anything: both new values are evidenced in the compiled sources themselves, so
they describe the same code more accurately.

**Confirmed absences over the same closed set, including two near-misses that look like hits.** The
twelve tracked Fortran files were searched for `do concurrent`, `submodule`, `contiguous`, coarray
syntax, `findloc`, `norm2` and the Fortran 2008 `block` construct, against a control search for
`subroutine` that matched four of them. Everything except `block` matched nothing beyond the
`error stop` pair already credited. `block` needs stating carefully, because a loose search for it does
return a line: `reference/nrlmsise00_sub_ORIGINAL.for:1652:      BLOCK DATA GTD7BK`. That is not the
construct being tested for — a `BLOCK DATA` unit is a legacy common-block initialiser, not the Fortran
2008 `BLOCK … END BLOCK` construct — and searching for the construct form itself, an `end block` or a
line containing nothing but `block`, returns nothing. The occurrence is also in `reference/`, which the
package build never compiles, so it could not affect the compiler requirement either way. So
*Fortran 2023* does not apply.
*Julia* exists in the vocabulary and appears nowhere in the tree at all. *IDL* is the same shape of
near-miss as `BLOCK DATA`: searched case-insensitively on word boundaries across the whole tracked
tree it matches exactly one path, and that path is `src/msise00/tests/msise00_demo.gif` — a byte
sequence inside a binary image fixture, not source text. Restricted to the tree's text files it matches
nothing, so there is no IDL source here. *C* and *C++* likewise: the CMake project declares
`LANGUAGES Fortran` only.

**What the `reference/` tree does and does not add.** It holds the NRL originals
(`nrlmsise00_sub_ORIGINAL.for`, `nrlmsise00_driver_ORIGINAL.for`, fixed-form) and free-form `.f90`
utilities, built only by its own hand-written `Makefile`. Its editions are a subset of the six above,
so it changes nothing here. It is mentioned because a future agent will see it and wonder: the package
build never reaches it. `src/msise00/CMakeLists.txt` names its three sources explicitly — there is no
glob, wildcard or file-set anywhere in either CMake file — so what is compiled is exactly those three
files and nothing else.

### 14. Reference Publication (RECOMMENDED)
- **DOI:** https://doi.org/10.1029/2002JA009430
- **Citation:** Picone, J. M., A. E. Hedin, D. P. Drob and A. C. Aikin (2002), NRLMSISE‐00 empirical
  model of the atmosphere: Statistical comparisons and scientific issues, *Journal of Geophysical
  Research: Space Physics*, 107(A12).
- The README points at this paper directly, at line 136:
  `* 1200+ citations 2002 [paper](http://onlinelibrary.wiley.com/doi/10.1029/2002JA009430/pdf)`. The
  authors, title, journal, volume and issue above are Crossref's metadata for that DOI, which supplied
  the two authors the earlier "et al." elided.
- The title's `NRLMSISE‐00` contains a Unicode hyphen (U+2010), reproduced as the publisher registered
  it rather than normalised to ASCII.
- **Do not report this DOI as broken.** The DOI and its metadata are intact: Crossref served the
  complete record, which is where the citation above comes from. Resolving the DOI lands on the Wiley
  platform, which as of 2026-09-08 returned HTTP 403 to a non-browser client — bot-blocking, not a dead
  DOI and not a paywall. Whatever that platform returns on a given day, a fetch failure there is not
  evidence about the DOI.
- **Why the model's paper rather than a paper about this package:** there is no paper about this
  package. See Field 27, which records that negative result and the search behind it.

### 15. License (RECOMMENDED)
- **License:** MIT License
- HSSI held no licence value for this software before this refresh; this fills that gap with the
  vocabulary's exact `MIT License` row. Three independent sources agree: `LICENSE.txt` at this revision
  opens `The MIT License (MIT)` / `Copyright (c) 2015-2025 SciVision, Inc.`; GitHub reports the
  repository's licence as SPDX `MIT`; and the DOI record's rights entry is `MIT License` with
  `rightsUri https://opensource.org/licenses/MIT` and SPDX identifier `mit`.
- **The licence has never changed, and this was checked by reading the file rather than by trusting the
  path.** `LICENSE.txt` reads as MIT at every content-changing commit in its history: at the initial
  commit (`8366796`, 2015-03-27, then named `LICENSE`), at `da3a170` (2019-06-30, where the path was
  renamed and the copyright line read `Copyright (c) 2015 Michael Hirsch`), and at `f24661c`
  (2025-06-06, the current line). Only the copyright holder changed. In particular the released
  version, v1.11.1, falls between the last two and carries MIT as well.
- **The NRL-origin Fortran carries no licence notice of its own, and this was checked before asserting
  a single licence for the tree.** A case-insensitive search of all thirteen files in `reference/` and
  `src/msise00/fortran/` for `copyright|licen[cs]|public domain|distribut|permission|proprietary|export`
  returned three matches, all of them the same NRL prose line — "subroutine is part of the distribution
  package for the" — in the body of the model's own documentation comments. Against a control search
  for `GTD7` matching nine of those thirteen files, that is a real absence: there is no NRL licence
  grant, restriction or public-domain declaration anywhere in the wrapped code. The MIT licence
  therefore covers the repository as it stands without a competing notice to reconcile.
- No licence URI is recorded as a value. This field resolves to a shared licence record that carries
  its own URL, so a per-software URI is not storable; the URIs above are cited as evidence only.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Keywords:**
  - atmosphere
  - build-on-run
  - empirical model
  - geospace
  - ionosphere_thermosphere_mesosphere
  - msis
  - neutral atmosphere
  - specific
  - thermosphere

**Provenance of the retained six.** `atmosphere` and `geospace` are `pyproject.toml`'s own
`keywords = ["atmosphere", "geospace"]`. `build-on-run` and `msis` are the repository's GitHub topics
and also the project's own vocabulary — `README.md` line 57 reads "This Python module uses our
build-on-run technique.", which is what that unusual tag means and why it is worth keeping: it tells a
prospective user that the Fortran is compiled on first use rather than shipped as a binary wheel.
`ionosphere_thermosphere_mesosphere` and `specific` come from the PyHC registry entry for this package.
All six are stored in lower case; the spellings above are the stored ones and should be sent verbatim
even though the lookup is case-insensitive, and even though the site renders them title-cased.

**The PyHC domain tag was checked rather than inherited.** PyHC's domain keywords propagate across its
registry and are frequently unsupported by the software that carries them, so
`ionosphere_thermosphere_mesosphere` was tested against this package rather than accepted. It survives
on the thermosphere and mesosphere halves: the model's validity range covers both, and thermospheric
temperature and composition are its primary outputs.

**This keyword is retained even though Field 5 does not carry `Earth Ionosphere`, and the two positions
are compatible rather than in tension.** They answer different questions, so a future refresh should
not "correct" either one into the other on the grounds that they differ. Region is a physical-domain
facet recording what the software *models*, and MSISE-00 models no ionospheric quantity — which is why
that value was declined there. This keyword is the ITM research community's own label for the domain a
tool *serves*, carried verbatim from the registry that assigned it, and MSIS is a canonical member of
the ITM toolset precisely as the neutral-atmosphere input that ionospheric calculations require.
Someone browsing the ITM tag is looking for that toolset and should find this entry; someone filtering
the ionosphere region is looking for ionospheric models and should not.

**`specific` is a registry taxonomy label, not a scientific keyword.** In the PyHC registry it
distinguishes special-purpose packages from general-purpose ones (a sibling entry in the same file
carries `general` in the same position). It conveys nothing to a visitor browsing this catalogue's
keywords, so it is a reasonable candidate for removal on a later pass; it is retained here because it
is a faithful record of the registry's own classification and removing it would lose that, which is
the weaker of two small losses.

**Why the three additions.** Each is a term a searcher would plausibly type, and each is evidenced in
the software's own words rather than inferred. `thermosphere` and `empirical model` already exist in the
keyword vocabulary, so they bind existing rows and immediately connect this entry to others tagged the
same way — the first because thermospheric density and temperature are the model's headline outputs,
the second because it is the category MSIS belongs to and the word the wrapped NRL source itself uses.
`neutral atmosphere` had no row in the keyword vocabulary before this refresh and enters it as a new
one; it earns that because it is the single most distinguishing phrase for this software, appearing
verbatim in `pyproject.toml`'s description
("Python API for Fortran MSISE-00 neutral atmosphere model.") and in the NRL header. It is also the
discriminator a visitor needs: it is what separates MSISE-00 from the ionospheric and wind models it
sits beside in this catalogue.

**Considered and not added.** `f10.7`, `geomagnetic index` and `geophysical indices` all exist in the
vocabulary and were rejected: MSISE-00 consumes those indices, it does not provide them, and a visitor
searching for index software wants the package named in Field 29 instead. `mesosphere`,
`middle atmosphere` and `upper atmosphere` were rejected as redundant with the Field 5 regions, which
express altitude coverage in the facet built for it.

### 17. Data Sources (OPTIONAL)
- **Values:**
  - HTTP/HTTPS Directories
  - Other

**`HTTP/HTTPS Directories` is recorded alongside `Other`, and the pair is deliberate.** Every default
run of this software fetches solar and geomagnetic indices over the network before it can compute
anything: `src/msise00/base.py`
calls `gi.get_indices(time, smoothdays=81)` whenever the caller passes no `indices` argument, and the
test suite names the artifact being downloaded in its own skip message,
`pytest.skip("unable to download RecentIndices.txt")`. The provider is named once in the project's
release history — the first of the v1.9.0 release note's two bullets reads "SWPC obsolesced their prior
data source, this used geomagindices >= 1.3.0 to use the new recent data source to provide Ap and f10.7
to MSIS", the second being about the Python version floor — but the
`DataInput` vocabulary has no SWPC or NOAA row, and nothing at this source revision names an archive.

The retrieval is real, mandatory in the default path, and of a named file over HTTP, so a visitor
filtering for software that pulls its inputs from web directories is right to expect MSISE-00 back —
and `Other` on its own tells that visitor nothing. That is what the added value buys.

`Other` is kept beside it rather than replaced, and the argument for keeping `Other` alone was weighed
rather than dismissed: this software names no archive in its own code or documentation, the retrieval
is delegated entirely to a separate package, and that package's endpoint has already changed once, so
`Other` alone claims nothing that could go stale. The pair is the more informative resolution — it
records both what is certain, that inputs arrive by HTTP fetch, and what is genuinely not determined at
this source revision, which archive they come from.
- Also considered and rejected outright: `GFZ`, `WDC`, `OMNIWeb`, `CDAWeb`, `HAPI` and
  `Observatory/Mission-specific`. Attributing a specific archive on the strength of a dependency's
  behaviour would be a claim this repository does not make and that nothing here would re-check.

### 18. Input File Formats (RECOMMENDED)
- **Formats:** None — this software reads no data files, and that is a property of the design rather
  than a gap in the research.

The model's inputs are arguments, not files: the public `msise00.run` takes a time, an altitude, a
latitude, a longitude and an optional dictionary of indices, and the command line takes the same as
flags. There is no reader, parser or loader in the public API.

**Two near-misses, both correctly excluded.** The test suite calls `xarray.open_dataset` on checked-in
`ref*.nc` files and `np.loadtxt` on `ccmc.log`, so netCDF and ASCII are read *by the tests* — but
as fixtures for comparing against reference output, not as user inputs; no code path lets a user hand
the package a file. Recording `netCDF3/4` here would send a visitor looking for a netCDF reader to a
model that has none.

### 19. Output File Formats (RECOMMENDED)
- **Formats:**
  - HDF5
  - netCDF3/4
- Both are one capability, stated in the software's own terms. `README.md` line 80 reads "Write NetCDF4
  output (HDF5 compatible) with command line argument `-w filename.nc`.", and the implementation is
  `atmos.squeeze().to_netcdf(ncfn)` in `src/msise00/__main__.py`. NetCDF4 is an HDF5 container, so both
  facets are true of the same file, so a visitor filtering either one is right to find this.
- **Considered and rejected:** `Other` for the PNG figures that `writeplot` saves via
  `fg.savefig(ofn, dpi=100, bbox_inches="tight")`. Plot images are not a scientific data format, the
  vocabulary has no image row, and `Other` would tell a visitor nothing while making the entry look
  like it emits an unspecified data product.

### 20. Operating System (RECOMMENDED)
- **Systems:**
  - Linux
  - Mac
  - Operating System Independent
  - Windows
- All four are directly evidenced and the combination is deliberate, not redundant.
  `Operating System Independent` is the project's own claim, via the `pyproject.toml` classifier
  `Operating System :: OS Independent`. The three named systems are what continuous integration
  actually exercises: `.github/workflows/ci.yml` runs a `unix` job over `ubuntu-latest` and
  `macos-latest` for Python 3.11 and 3.14, plus an `msys2` job on `windows-latest`, and
  `.github/workflows/ci-matlab.yml` covers the same three systems for MATLAB R2024b (its Linux runner
  is pinned to `ubuntu-24.04`).
- One caveat a future refresh should not mistake for an error: the classifier's `OS Independent` is
  the project's portability claim about its Python code, but using it does require a Fortran compiler on
  the host (`README.md` gives per-platform instructions for obtaining one). Both facts are recorded —
  the classifier as the project's claim, the three named systems as tested reality.

### 21. CPU Architecture (RECOMMENDED)
- **Architectures:**
  - Apple Silicon arm64
  - CPU Independent
  - x86-64
- `CPU Independent` is the primary and correct characterization: the code is Fortran and Python with no
  architecture-specific intrinsics, assembly or binary artifacts — it is compiled from source on the
  user's machine, which is the whole point of the build-on-run design.
- `x86-64` is directly evidenced: the Windows CI job installs the MSYS2 package
  `mingw-w64-ucrt-x86_64-gcc-fortran`, naming the architecture explicitly.
- **`Apple Silicon arm64` is recorded, and the argument against recording it is kept because it was
  weighed rather than dismissed.** The evidence for it: the MATLAB build helper
  `+msise00/private/fix_macos.m` prepends both Homebrew locations to `PATH` —
  `needed_paths = ["/opt/homebrew/bin", "/usr/local/bin"]` — and `/opt/homebrew` is the Apple Silicon
  prefix while `/usr/local` is the Intel one, so the project handles both Mac architectures
  deliberately, and macOS CI exercises the Mac path on every relevant push. The argument against it:
  `CPU Independent` is already recorded and already covers every architecture, so naming individual
  ones adds discoverability rather than information, and a minimal facet would keep only `x86-64`, the
  value with the most explicit in-repository evidence. What decided it was asymmetry rather than
  coverage. Because `x86-64` is recorded, omitting arm64 would not have left this facet minimal — it
  would have left it lopsided, telling a searcher who filters for Apple Silicon that this software is
  unavailable there while telling one who filters for x86-64 that it is available, when the software
  demonstrably builds and is CI-tested on both. That actively misleads, where a facet carrying neither
  value would merely have omitted.
- Considered and rejected: `GPU` and `HPC or HEC` — there is no GPU code and no parallelism beyond
  CMake's `--parallel` build flag; `ppc64le`, `Sun (SPARC)` and `Linux aarch64 or arm64` — nothing in
  the repository or its CI addresses them.

### 22. Related Phenomena (OPTIONAL)
- **Values:** None — and this is an evidenced conclusion about the vocabulary, not an unexamined blank.

The `Phenomena` vocabulary offers exactly seven values: `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and
`X-ray emission`. Six are solar or heliospheric and have nothing to do with a terrestrial neutral
atmosphere model. The seventh, `Geomagnetic Storms`, is the only real candidate and is rejected: the
model takes the Ap index as a parameter and so responds to storm-time conditions, but it does not
study, detect, characterize or predict storms, and a visitor filtering for storm software would find a
climatology with a magnetic-activity knob. The vocabulary simply contains no term for what this
software is about — neutral density, thermospheric composition, satellite drag — so the correct value
is none. If a term of that kind is ever added, this field should be revisited.

### 23. Development Status (RECOMMENDED)
- **Status:** Active

HSSI held no development status for this software before this refresh, so this is a first assignment
rather than a correction, and it is a trust signal a visitor reads directly.

**The deciding test is the vocabulary row's own definition, not the release history.** The `Active`
row reads "The project has reached a stable, usable state and is being actively developed." Its first
clause is satisfied on any reading: `pyproject.toml` carries the classifier
`Development Status :: 5 - Production/Stable`, there are 28 released versions on PyPI, and the
repository is neither archived nor carrying open issues. The second clause is what decides, and it asks
about development, not about releases.

**Development evidence at the pinned revision, re-derivable by anyone holding the pin.** Counted over
the pinned lineage — `git rev-list` on the source revision, not across all refs — there are 17 commits
in 2024, 8 in 2025 and 6 in 2026, the most recent being `e4ab457` on 2026-03-17, subject
`CI: universal gfortran 15`. That recent work is compiler and language-floor modernization: universal
gfortran 15 support, Python ≥ 3.11, pre-commit, an API update, and regenerated test data after a NumPy
ABI change. Someone is keeping this working against a moving ecosystem. These counts are fixed by the
revision rather than by the calendar, which is what makes them safe to rely on later.

**Release cadence is not the test this definition sets, so the newest release date does not weigh
against `Active`.** The hazard here is specific and foreseeable: the newest release is `v1.11.1` from
2024-12-19, so a future agent glancing only at release history would read `Active` as unsupported and
be tempted to "correct" it to `Inactive`. The definition says the project is being actively developed,
and commits landing in three successive years on an unarchived repository satisfy that. **Do not revert
this value on release-date evidence alone.**

**The `Inactive` reading was considered and is not determinative.** Its definition is "The project has
reached a stable, usable state but is no longer being actively developed; support/maintenance will be
provided as time allows." The strongest points on that side are genuine and are kept here: there has
been no release since 2024-12-19; the pinned lineage carries no commits at all in either 2022 or 2023;
and the recent commits are upkeep rather than new capability, which reads close to that definition's
own "support/maintenance will be provided as time allows". What rules it out is its own operative
clause — "no longer being actively developed" is falsified by the 2024, 2025 and 2026 commits above on
a repository that is not archived. A project maintained sporadically is still being maintained.

The remaining values are ruled out on their own definitions.
`Unsupported` ("the author(s) have ceased all work on it") is contradicted by the 2026 commits.
`Abandoned`, `Suspended` and `WIP` share the requirement that there has "not yet been a stable, usable
release", which is false here. `Concept` does **not** carry that phrase and has to be excluded on its
own terms instead: its definition is "Minimal or no implementation has been done yet, or the repository
is only intended to be a limited example, demo, or proof-of-concept.", and a package with 28 released
versions on PyPI declaring `Development Status :: 5 - Production/Stable` is neither minimal nor a demo.
`Moved` would require an authoritative version elsewhere; there is none.

For context: among the sibling wrappers in this catalogue, GLOW and LOWTRAN carried
`Inactive` and HWM-93 and IRI-90 carried `Unsupported` when this dossier was written. MSISE-00 is the
most recently touched of that family, which is a reason its value should not be inherited from theirs.

### 24. Documentation (RECOMMENDED)
- **URL:** https://ccmc.gsfc.nasa.gov/models/NRLMSIS~00/
- This is the CCMC model page for NRLMSIS-00, and it is the PyHC registry's own curated documentation
  target for this package, arrived at by following the registry's stored value
  (`https://ccmc.gsfc.nasa.gov/modelweb/models/nrlmsise00.php`), which redirects here. The current URL
  is recorded rather than the redirecting one so that the stored value does not depend on a redirect
  continuing to exist.
- **Why an upstream model page rather than the project's own README.** The two do different jobs and
  only one of them is otherwise unreachable from this record. The README documents installation and
  API usage, and a visitor already has it: Field 3 links the repository, whose front page *is* the
  README. The CCMC page documents the model itself — its physics, inputs, validity and provenance —
  which nothing else in this record supplies. Sending a visitor there adds information; sending them to
  the README again would not.
- **Two related absences, both checked so they are not rechecked.** There is no wiki:
  `git ls-remote https://github.com/space-physics/msise00.wiki.git` reports the repository as not
  found, and GitHub reports `has_wiki: false` — so no wiki page carries release policy or other
  documentation. And the link the README itself offers for the original Fortran,
  `https://ccmc.gsfc.nasa.gov/pub/modelweb/atmospheric/msis/` (README line 135, also the repository's
  GitHub `homepage` field) did not resolve when checked on 2026-09-08, returning HTTP 404. The durable
  point is independent of CCMC's server: the model's current CCMC location is the page recorded above
  as this field's value, so that older path is not a candidate here even if it is restored. It is
  recorded so nobody adopts it.

### 25. Funder (OPTIONAL)
- **Values:** None found — an evidenced absence, with the routes recorded so they are not re-run.
- The DOI record's `fundingReferences` list is empty, as are its `subjects` and `contributors`.
- No funding metadata has ever existed in this repository. Searching every path added anywhere on this
  source revision's ancestry for `citation|zenodo|codemeta|mailmap|funding|contribut|author` matched
  exactly one file out of 131 distinct added paths — `.github/FUNDING` — and that file is not a
  research funder record: its entire content is `github: [scivision]` and `ko_fi: scivision`, a
  personal donation configuration, and it was renamed away the same day it was created (2019-11-05).
- Crossref carries no funder metadata for the reference publication either. That would not have helped
  in any case: the 2002 NRLMSISE-00 paper's funding is the Naval Research Laboratory's, for building
  the model — not funding for this Python and MATLAB wrapper, which is what this field records.

### 26. Award Title (OPTIONAL)
- **Values:** None found — for the same reasons as Field 25, and with no separate award identifier
  anywhere in the DOI record, the repository or its history.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Publications:** None — and this is a researched negative, not an unsearched field.
- There is no publication about this software. The DOI record's twenty-five related identifiers are
  twenty-four `HasVersion` links to its own release DOIs plus the one `IsSupplementTo` link to the
  GitHub tag; not one is a publication relation of any kind. `README.md`'s "Reference" section cites
  exactly one paper, the 2002 model paper already recorded in Field 14.
- **A literature search confirms it, and the control makes that falsifiable.** Searching the
  astronomy/heliophysics literature index for `msise00` and `msise-00` in the title, and for
  `space-physics/msise00` in full text, returns two records — and both are this package's own Zenodo
  software deposits (*space-physics/msise00: Auto-build for Python and Matlab, increase test coverage*,
  2019, and *space-physics/msise00: Matlab tests, enhance build*, 2021), i.e. release records of the
  DOI already held in Field 2, not publications about the software. No journal or conference article
  exists. The control that makes this a real absence rather than a search artifact: the same query
  shape on `pymap3d` — another package by the same author — returns three records including a genuine
  journal article (*PyMap3D: 3-D coordinate conversions for terrestrial and geospace environments*,
  2018, 10.21105/joss.00580). The index does surface this author's software papers when they exist.
- **The most likely wrong guess, closed off.** This author does write software papers: his ORCID record
  lists that PyMap3D article and *h5fortran: object-oriented polymorphic Fortran interface for HDF5
  file IO* (10.21105/joss.02842), both for packages in the same family as this one. None of his
  eighteen listed works concerns MSISE-00. A future agent should not spend effort looking for a JOSS
  paper for this package; there is none, and its absence is not an oversight in this record.
- Deliberately *not* placed here: the 2002 model paper, which belongs in Field 14 as the reference
  publication and would be redundant duplicated here.

### 28. Related Datasets (OPTIONAL)
- **Datasets:** None.
- This software produces data rather than consuming a published dataset. Its only external inputs are
  two scalar activity indices, and those arrive through a software package (Field 29) rather than from
  a citable dataset. The DOI record carries no dataset relation.
- Considered and rejected: the in-repository comparison fixtures. `src/msise00/tests/ccmc.log` is
  saved CCMC web-service output and `src/msise00/tests/ref1.nc`–`ref6.nc` are regenerated by the
  package itself (each test file documents the exact command, e.g. `python -m msise00 -w
  src/msise00/tests/ref3.nc -a 200 -gs 30 60 -t 2017-03-01T12`). They are test fixtures with no
  identifier and no publication, not related datasets.

### 29. Related Software (OPTIONAL)
- **Software:**
  - https://github.com/space-physics/geomagindices
  - https://github.com/space-physics/hwm93
  - https://github.com/space-physics/iri90
  - https://github.com/timduly4/pyglow

Every entry — retained, added or removed — gets a reason; an incumbent kept without an argument would
be the same defect as a candidate rejected without one. Each URL above is under 128 characters, and
each is the exact repository URL the corresponding catalogue entry stores, so a visitor sees a legible
repository address as the link text rather than an opaque identifier. (If the site ever renders
resolved titles instead of raw URLs, a DOI would become the better choice on persistence grounds.)

- **`geomagindices` — re-derived against the field's own criteria, and retained.** Field 29 admits
  software by several distinct routes, so it is worth naming which one this is rather than asserting
  that it belongs. It is not a similar-purpose tool, not a predecessor, and not a fork parent. It
  qualifies as the field's domain-specific dependency case, whose test is
  "a heliophysics/science library whose presence characterizes the software" — and both halves hold.
  *A heliophysics/science library:* it retrieves F10.7 solar radio flux and Ap geomagnetic indices,
  quantities with no meaning outside this field. Put through the test the field directs at any package
  it does not name — would it be equally at home in a web app, a finance model or a biology pipeline —
  it fails immediately, so it is not generic infrastructure.
  *Its presence characterizes the software:* MSISE-00 cannot answer a default call without it.
  `src/msise00/base.py` imports it as `import geomagindices as gi` and calls it inside `rungtd1d`, the
  model's innermost function, and the project treats it as a first-order concern: `pyproject.toml`
  pins `geomagindices>=1.4.0`, and the release history turns on this dependency repeatedly — v1.3.0
  adopted it ("use `geomagindices` package to get Geomagnetic indices"), v1.9.0 followed it to a new
  upstream data source, and v1.10.0 raised the floor to `>=1.4.0` for an index computation that, in
  the maintainer's words, "makes MSISe00 here nearly exactly match CCMC". It also passes the
  information test that disqualified numpy
  below: a statement that this software depends on geomagindices is true of almost nothing else in the
  catalogue, so it tells a reader something about *this* software rather than about the ecosystem.
  From the searcher's side, a visitor who wants to reproduce a run needs to know where the driving
  indices come from, and this is the only field that tells them.
- **`hwm93` — added.** The companion model. HWM-93 is the NRL horizontal wind model wrapped by the same
  author in the same build-on-run pattern over the same altitude range; MSIS gives the neutral
  composition and temperature, HWM gives the winds, and upper-atmosphere work routinely uses them
  together. HWM-93's own catalogue entry already names this repository as related software, so the
  relationship was recorded in one direction only, leaving a visitor who arrived at MSISE-00 first with
  no way to discover it.
- **`iri90` — added.** The ionospheric counterpart, again by the same author in the same wrapper family.
  It is the natural partner and the natural contrast: where MSISE-00 gives neutral species, IRI-90
  gives electron and ion parameters. A visitor holding MSISE-00 and needing the plasma side of the same
  altitude range should be shown it.
- **`pyglow` — added.** A directly competing route to the same model. pyglow is an independent Python
  wrapper around several upper-atmosphere climatologies including MSIS 2000, which is this same
  NRLMSISE-00. This is the paradigm case the field's own definition describes: software performing
  similar tasks under different design choices. A visitor evaluating how to call MSIS from Python is
  materially better off knowing both exist.

**`numpy` — removed as a matter of policy, not as a judgement call.** The submission form names numpy
first among the packages that must never be listed (Field 30, line 690), and line 698 states that
Field 29 applies the same exclusion to the generic stack, so a rejected generic package is not to be
relocated here. This is not a preference a later reviewer can approve away, and the form gives the
reason in general terms at line 690: "It directly depends on numpy" is true of nearly every package in
HSSI, so it distinguishes nothing. The dependency itself is real and unchanged — `pyproject.toml`
lists `numpy` — it simply is not related software.

**`xarray` — moved to Field 30, not removed.** It was recorded here, but it belongs one field over: the
relationship is a demonstrated data exchange, not a similar-purpose or characterizing dependency. The
evidence is set out under Field 30. The same URL is used there, so nothing is lost by the move.

**Considered and rejected, so they are not re-proposed.**
- *pymap3d* (`https://github.com/geospace-code/pymap3d`) and *astropy*. Both are optional
  `[project.optional-dependencies] plot` extras used only inside `src/msise00/plots.py` to place a sun
  marker on a density map, and `plots.py` guards both imports with `try`/`except ImportError` so the
  package works without them. astropy also sits in the tier that requires a specific documented
  exchange, and decorating a figure is not one. Neither characterizes what this software is.
- *matplotlib*, *netCDF4*, *pytest*, *mypy*, *setuptools*, *wheel*. Generic infrastructure — plotting,
  I/O plumbing, testing, packaging — each equally at home in a web application or a finance model.
- *ScienceDates* (`https://github.com/geospace-code/sciencedates`). Worth recording because its own
  catalogue entry names this repository, and because a predecessor of it, `fortrandates.py`, really was
  vendored here once (it appears among the paths added on this revision's ancestry). At this source
  revision neither name appears anywhere in the tree — a case-insensitive search for
  `sciencedates|fortrandates` over all tracked files returns nothing — and the date handling now lives
  in `src/msise00/timeutils.py` using only the standard library and NumPy. It is a former dependency,
  not a current one.
- *GLOW*, *ReesAurora*. Both depend on this package and both name it in their own entries. Rejected
  because this field is for software that tells a reader something about *this* software: that an
  auroral model chooses MSIS for its neutral background characterizes the auroral model's design, not
  the atmosphere model's.
- *TIEGCM* and *LOWTRAN*. Both are Earth-atmosphere models in this catalogue, and TIEGCM in particular
  is the first-principles alternative to an empirical climatology, which fits the field's "different
  assumptions" example. Rejected on the field's own information test: being another model of Earth's
  upper atmosphere would hold for a large and growing share of this catalogue, so listing them
  would dilute the four entries above, each of which is specifically about MSIS access or its immediate
  model companions. This is the weakest of the rejections and a later refresh may reasonably revisit
  TIEGCM; the four retained entries should not be diluted casually.
- *`https://github.com/gemini3d/msis`*. Another MSIS interface exists under the gemini3d organization
  and is named as related software by PyGemini's catalogue entry. Rejected here because nothing in this
  repository references it, so any statement about its relationship to this package would be an
  inference about a third-party repository that nothing in this record would ever re-check.

### 30. Interoperable Software (OPTIONAL)
- **Software:**
  - https://github.com/pydata/xarray
  - https://www.mathworks.com/products/matlab.html

HSSI held no interoperable software for this entry before this refresh. Both additions clear the
tier that demands a specific exchange documented in the public API, docs, examples or tests — not
merely a dependency, and not an ecosystem-membership claim.

**`xarray` — the documented public interchange format.** The evidence was established with an explicit
pattern over an explicit scope: `git grep -n -P 'xarray'` at this source revision, over the whole
tracked tree, matches eleven files. What the matches actually are, resolved individually rather than
counted:

- *Public return value.* `src/msise00/base.py` builds and returns `xarray.Dataset` objects from
  `rungtd1d` and `run` — the package's two exported model functions — and merges grid points with
  `xarray.merge`. The dataset is the API's output type, not an internal intermediate.
- *Documented as such.* `README.md` tells the user so directly at lines 73–75: "atmos is an" /
  "[xarray.Dataset](http://xarray.pydata.org/en/stable/generated/xarray.Dataset.html)" /
  "containing all the simulation output values." — a labelled link to xarray's own documentation for
  the returned type.
- *Exercised in tests as an exchange.* `src/msise00/tests/test_point.py`, `test_grid.py` and
  `test_time_grid.py` each import `xarray` and `xarray.testing`, reopen written output with
  `xarray.open_dataset`, and compare with `xarray.testing.assert_allclose`. The round trip
  model → netCDF → xarray object is asserted, not assumed.
- *Adapted for another language.* `+msise00/python-matlab/xarray2mat.m` and `xarrayind2vector.m` are
  converters whose entire purpose is translating xarray objects into MATLAB values, reaching into
  `V.indexes{key}.values.tolist` and `double(py.numpy.asfortranarray(V))`.
- *Not evidence, and excluded as such:* the `xarray` entry in `pyproject.toml`'s `dependencies`, which
  would prove only presence; and the matches in `.archive/f2py.py` and `.archive/msise00.m`, which are
  the retired f2py implementation kept for history and excluded from the project's own type checking.

**`MATLAB` — a genuine cross-language bridge, which the field names as qualifying.** MATLAB support
here is not a mention in a README; it is a parallel implementation with its own test suite and CI.
`+msise00/msise00.m` runs the compiled model directly from MATLAB, returning a MATLAB struct;
`+msise00/python-matlab/msise00.m` bridges the other way with `atmos = py.msise00.run(time, alt_km,
glat, glon);`, handing MATLAB the Python object that the adapters above then convert;
`+msise00/TestUnit.m` is a `matlab.unittest.TestCase` suite that validates both the numerical results
and the plots; and `.github/workflows/ci-matlab.yml` runs all of it on Linux, macOS and Windows against
MATLAB R2024b. The URL recorded is the same MathWorks product URL that GLOW and LOWTRAN use for this
relationship, which keeps this entry pointing at the same catalogue item rather than creating a
near-duplicate.

**Consequence worth stating plainly.** When this dossier was written, `https://github.com/pydata/xarray`
sat in the interoperable-software field of GLOW, HWM-93 and ReesAurora, and the MathWorks URL sat in
GLOW's and LOWTRAN's. A user comparing MSISE-00 against those siblings would have seen the same
xarray-and-MATLAB architecture described as interoperability everywhere except here. That is a
consequence, not the argument: the argument is the evidence above, which stands on its own.

**Rejected for this field.** *numpy* and *matplotlib* — the never-list tier, no exceptions. *netCDF4* —
a test-only extra; the netCDF write goes through xarray, so the exchange that exists is xarray's.
*astropy* — used internally to compute a sun position for a plot decoration, which is not an exchange
of data models. *geomagindices* — a genuine exchange in the sense that it hands over an index
dictionary, but it is a mandatory upstream dependency that characterizes the software, which is what
Field 29 is for; recording it in both fields would say the same thing twice.

### 31. Related Instruments (OPTIONAL)
- **Instruments:** None — the correct value for an instrument-agnostic model, established by search
  rather than assumed.

**The relevance gate is what decides this, and the model fails it on purpose.** MSISE-00 reads no
instrument's data, writes no instrument's format, calibrates nothing and is not a mission or
instrument team tool. It takes a time, a place, an altitude and two activity indices, and returns
climatological neutral densities and temperatures. A visitor on any instrument's page would be
puzzled to find it there.

**The interesting part, and the reason this is worth reading before proposing anything.** The
instruments in the model's *heritage* do have vocabulary rows, so a future agent will find them and be
tempted. A case-insensitive search over the whole controlled vocabulary — across the row name,
abbreviation, SPASE identifier and definition, so all four text columns — finds real entries for the
measurement techniques the acronym MSIS stands for: neutral mass spectrometers and atmospheric density
accelerometers on the Atmosphere Explorer satellites (for example
`https://spase-metadata.org/SMWG/Instrument/AE-C/NACE` and
`https://spase-metadata.org/SMWG/Instrument/AE-C/MESA`) and incoherent scatter radars including EISCAT
and `https://spase-metadata.org/SMWG/Observatory/AMISR`. **They are still correctly excluded.** The
model was *derived* from decades of such measurements; this software *supports* none of them. Heritage
is not support, and recording those rows would make MSISE-00 appear in searches for AE-C or EISCAT
data tooling, which it is not.

**Also considered and excluded:** the Poker Flat Research Range. It appears in this repository only as
a demonstration coordinate — `src/msise00/__main__.py`'s docstring says "Poker Flat Research Range
altitude profile" and `Examples/AltitudeProfile.py` uses `glat = 65.1`, `glon = -147.5`. Poker Flat
observatories do have vocabulary rows, but an example location in a docstring is a tutorial mention,
not a designed-to-support relationship.

**The model's own name has no vocabulary row.** Searching the same four columns of the vocabulary,
case-insensitively, for `MSIS` on a word boundary and for `NRLMSIS` returns nothing at all, against a
control search for `SuperDARN` on the same columns that returns ten rows and concept searches that
returned dozens. So there is no missing-instrument substitution to make either. Every naming authority
present in the vocabulary was covered by that search, not just the SPASE working group's.

**A hard constraint for any future addition.** Nothing may be recorded in this field without an
`https://spase-metadata.org/` identifier. A bare name does not free-type; it creates a new
identifier-less vocabulary row, which is the defect a past vocabulary clean-up removed. If a genuine
instrument association is ever found, it must resolve to a real row or be omitted.

### 32. Related Observatories (OPTIONAL)
- **Observatories:** None — for the same reason and by the same search as Field 31, which covered
  observatory rows (the vocabulary's observatory-typed rows were in scope throughout) alongside
  instrument rows.
- The model is not a mission product and supports no platform specifically. There is no spacecraft,
  facility, ground station, sounding rocket or mission label whose data this software reads or whose
  measurements it is built to serve; it serves any location and time on Earth.
- One asymmetry worth recording so it is not read as an omission: the CCMC runs NRLMSIS-00 as a
  hosted model and this package's `src/msise00/tests/ccmc.log` is saved CCMC output used as a
  regression reference. The CCMC is a modelling facility, not an observatory, and it has no
  observatory row; the comparison is a test fixture. It is noted under Field 28.

### 33. Logo (OPTIONAL)
- **URL:** None — deliberately empty, and the emptiness is evidenced rather than merely unfilled.

HSSI held no logo for this entry before this refresh, and none is being added. The project has never
had a logo: the only two images tracked at
this source revision are model-output figures under `src/msise00/tests/`, and the PyHC registry entry
for this package has no `logo:` key — an absence that is real rather than a gap in that file, since the
same registry file carries nine `logo:` lines for other entries.

**Both candidates were fetched, inspected, and are recorded here because they are the evidence for the
emptiness** — not as fallbacks awaiting promotion. Their URLs are pinned to this dossier's source
revision, so a future agent can re-check them without re-deriving anything:

- `https://raw.githubusercontent.com/space-physics/msise00/e4ab457c4e3f252c7ce748826d1e137ec9c563c0/src/msise00/tests/msis_matlab.png`
  — 200, `image/png`, 20513 bytes, URL 130 characters. Looked at: a MATLAB line plot of N2 number
  density against time, with labelled axes and a single trace over one day. The README presents it at
  line 17 with
  the caption "This plot is from [Matlab](./src/msise00/tests/test_msise00_matlab.m) calling MSISE00:".
- `https://raw.githubusercontent.com/space-physics/msise00/e4ab457c4e3f252c7ce748826d1e137ec9c563c0/src/msise00/tests/msise00_demo.gif`
  — 200, `image/gif`, 3942343 bytes, URL 131 characters. This is the README's hero image at line 15,
  captioned "MSIS global time animation": the global density panels described at README line 12 as "The
  plot immediately below shows a slice at 200km on a world-wide grid." At nearly 4 MB it is a heavy
  asset for a catalogue thumbnail.

**Why neither was chosen.** Neither image is a logo. Both are data products — a demonstration plot and
an output animation — and neither is a wordmark, emblem or identifying graphic. A visitor scanning a
list of catalogue entries gains nothing from a thumbnail of an arbitrary N2 density profile, and the
GIF at nearly 4 MB would be a poor page asset besides.

**The argument the other way was real and is kept.** The project does present both images at the top of
its README, which is the closest thing it has to a visual identity, and a page with an image reads as
more complete than one without. There is also a consequence in the world: when this dossier was
written, WMM2020 — the same author, the same wrapper family — carried as its logo a commit-pinned raw
URL to a demonstration plot inside its own `tests/` directory, and LOWTRAN carried a pinned raw URL to
a demonstration figure too. So this entry is visibly imageless beside siblings whose images are of
exactly this kind. That was weighed and did not carry the decision: matching a sibling's practice is
not a reason to put a data product in a field meant for an identifying mark. The question turned on
what a logo field is for on the site, and it is settled — a future refresh should not read the empty
field as an unfinished one.

**If a logo is ever added, it must be commit-pinned.** A branch-based URL would break silently the
moment the file is renamed or moved, and pinning is what makes a later logo change a deliberate,
noticed edit rather than a silent substitution. There is no Git-LFS complication here — this revision
has no `.gitattributes`, and both fetches returned real image bytes rather than a pointer file.

---

## Durable context

Kept because it repeatedly bears on the fields above and on how a future agent should read this
repository.

**Build-on-run, and why so many fields mention it.** There is no compiled artifact in the
distribution. The first call from either language compiles the Fortran: `src/msise00/base.py`'s
`build()` locates `cmake`, configures `src/msise00/CMakeLists.txt` and builds `msise00_driver`, and
`+msise00/private/cmake.m` does the same from MATLAB. This is what the `build-on-run` keyword records,
what makes a Fortran compiler a real user prerequisite despite the "OS Independent" classifier
(Field 20), and why the Fortran editions in Field 13 are a genuine constraint on users rather than
trivia about vendored source.

**Dependencies at this source revision**, from `pyproject.toml`: required — `numpy`, `xarray`,
`geomagindices>=1.4.0`; build — `setuptools>=61.0.0`, `wheel`; `tests` extra — `pytest`, `netCDF4`,
`mypy`; `plot` extra — `matplotlib`, `astropy`, `pymap3d`. Fields 29 and 30 give the verdict on each.
An earlier revision of this dossier also listed a `lint` extra with `flake8` and
`types-python-dateutil`; that group does not exist at this source revision, so any future comparison
against the older text should expect it to be gone rather than treat its absence as an extraction miss.

**Command line.** The `msise00` entry point accepts `-t` times, `-a` altitudes (scalar, start/stop/step
or a list), `-c` a lat/lon pair or `-gs` a global grid spacing, `-w` a netCDF output filename, `-o` a
plot output directory and `-q` to suppress plotting. Single-point, altitude-profile, time-series and
global-grid runs are all reachable without writing code, which is part of why Fields 4 and 19 credit
retrieval, plotting and netCDF output as user-facing capabilities.

**Three inaccuracies in the project's own README, recorded so they are not mistaken for findings.**
Line 58 says "The first time you use this Python module, you will see messages from the Meson build
system." — the build is CMake, and no `meson.build` exists at this revision; Meson was used
historically (`matlab/setup_meson.m` and `matlab/meson.m` appear among the paths added on this
revision's ancestry). Line 135's link to the original Fortran,
`https://ccmc.gsfc.nasa.gov/pub/modelweb/atmospheric/msis/`, did not resolve when checked on
2026-09-08 (HTTP 404); the model's current CCMC location is the Field 24 URL. Line 17's relative link
to `./src/msise00/tests/test_msise00_matlab.m` points at a file that does not exist at this revision
(it existed once, as `tests/test_msise00_matlab.m`). None of these changes any field value; each is the
kind of thing that otherwise costs a future agent an hour.

**Two source trees that are not the software.** `reference/` holds the unmodified NRL originals and
free-form utilities, built only by its own hand-written `Makefile` and never reached by the package's
CMake project. `.archive/` holds the retired f2py implementation and an old MATLAB entry point, and is
excluded from the project's own `mypy` configuration. Evidence from either is heritage or history, and
this dossier labels it as such wherever it is used.
