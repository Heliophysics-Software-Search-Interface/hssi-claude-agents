# HSSI Metadata Extraction Results

**HSSI Software ID:** 855aa42c-15e8-4b99-be89-3986ccb8254c
**Repository:** https://github.com/gemini3d/gemini3d
**Source Revision:** aa50fa1a34c374edaf7e1c79e6d330e4025f777c
**Extraction Date:** 2026-09-11
**Validation Date:** 2026-09-12
**Validation Status:** PASS

---

**Scope note — read this before using the evidence below.** Two facts change how the repository
should be read at this revision.

*First*, the source revision `aa50fa1a` post-dates a submodule experiment that was started and then
abandoned. `.gitmodules` was added on 2024-01-17 (commit `cb6503c5`, "Git Submodule:
fortran-filesystem") and deleted on 2026-03-23 (commit `df72b933`, "ffilesystem via FetchContent").
At the pinned revision there is no `.gitmodules` and no gitlink entry: the six external components
(ffilesystem, glow, h5fortran, hwm14, msis, mumps) are pulled in at configure time by CMake
`FetchContent` from the pinned tarballs listed in `cmake/libraries.json`. `Readme.md` at this
revision has not caught up — it still instructs `git clone --recurse-submodules` and
`git submodule update --init --recursive`. Evidence drawn from the repository is therefore top-level
only; the components' own sources are not part of this tree.

*Second*, the **software name in the repository is not the name on this HSSI entry.** `Readme.md`
line 1 is `# GEMINI`; `CITATION.cff` and `codemeta.json` both say `Gemini3D`; the CMake project is
`gemini3d`. The name "PyGemini" on this entry comes from the PyHC registry, which pairs that name
with this repository. The repository does mention PyGemini — 21 times across 8 files at this
revision — but always as an external component it detects and calls out to, never as its own name
(the measured sweep is under Field 7). There is also a separate live repository,
`https://github.com/gemini3d/pygemini`, that *is* PyGemini. That divergence was examined and settled
in favour of the stored pairing; Field 7 carries the full reasoning, including the evidence that
pointed the other way.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Note:** Placeholder by design. HSSI's public read APIs do not expose submitter identity, so no
value can be recovered from the catalogue; the submitter is named by whoever submits the entry.

---

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.3647579

**Why this DOI.** The form asks for "the concept DOI for all versions". At DataCite,
`10.5281/zenodo.3647579` carries 57 `HasVersion` relations and no `IsVersionOf` — it is the Zenodo
concept record for the GitHub-Zenodo deposit series, titled `Gemini3D`. Its
`IsSupplementTo` target is `https://github.com/gemini3d/gemini3d/tree/v1.7.0`, confirming it belongs
to this repository. The README carries the matching concept badge,
`https://zenodo.org/badge/latestdoi/146920930`.

**Rejected: `10.5281/zenodo.3813224` — and this rejection must not be reversed.** Both of the
repository's own machine-readable metadata files declare that DOI:

- `CITATION.cff` at this revision: `doi: 10.5281/zenodo.3813224`
- `codemeta.json` at this revision: `"identifier": "10.5281/zenodo.3813224"`

It is nevertheless the wrong value. DataCite resolves `10.5281/zenodo.3813224` to the title
`gemini3d/gemini: robus`, version `v0.5.6`, issued 2020-05-07, with
`IsVersionOf 10.5281/zenodo.3647579`. It is a **version** DOI for a 2020 release — one of the 57
versions the concept DOI aggregates — and its title is a truncated GitHub release headline. A future
refresh that "corrects" Field 2 to match `CITATION.cff` would replace a correct concept DOI with a
stale version DOI, and would also pull in that record's degraded creator list (see Field 6). The
divergence between HSSI and the repository is HSSI being right; this is a repository metadata bug,
not an HSSI one.

**Rejected: `10.5281/zenodo.10475267`.** That is the current *version* DOI (v1.7.0) and belongs in
Field 12, where it is recorded. Confirmed newest: it is the highest-numbered of the 57 `HasVersion`
records (next highest `10.5281/zenodo.6812158`), and the concept record's own `version` field reads
`v1.7.0` with issue date 2024-01-09.

**Rejected: `10.5281/zenodo.3910038`.** That is the concept DOI of `gemini3d/pygemini`, a different
deposit series with a different creator list. It is the DOI this field would carry had the entry been
repointed at the Python repository; it was not, for the reasons set out in Field 7, so the concept
DOI of the Fortran repository is the correct value here.

---

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/gemini3d/gemini3d

**Note:** This is the stored value and the repository this extraction was performed against. It
resolves to a live, non-archived GitHub repository (`gemini3d/gemini3d`, description "Ionospheric
fluid electrodynamic model", primary language Fortran, created 2018-08-31) whose default branch
`main` contains the pinned revision. It is also the value the PyHC registry gives for its `PyGemini`
entry.

**The alternative was examined and not taken.** Because the entry is named "PyGemini", a case exists
that this field should instead point at `https://github.com/gemini3d/pygemini`. It was considered in
full under Field 7 and rejected: the literature, the DOI series, the licence history and the release
record all belong to the Fortran repository, and the PyHC registry — the entry's provenance — is what
pairs the name with this repository. The Python repository is recorded instead in Field 30, as
interoperable software.

**Note on `codemeta.json`.** It declares `"codeRepository": "https://github.com/gemini3d/gemini"`
(no "3d"). GitHub answers that path with a 301 to repository id `146920930`, whose canonical name is
`gemini3d/gemini3d`; the codemeta string is the repository's former name, preserved only by GitHub's
rename redirect. That same repository id appears in the README's Zenodo badge
(`https://zenodo.org/badge/146920930.svg`), which independently ties the concept DOI in Field 2 to
this repository. The stored value is the better one — do not "correct" it back to the codemeta
string.

---
### 4. Software Functionality (RECOMMENDED — treated as critical)
**Values:**
- Coordinate Transforms
- Coordinate Transforms: Ionospheric
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Processing
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: First Principles
- Models and Simulations: Physics-Based
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Line Plots
- Servers and Environments
- Servers and Environments: High Performance Computing

Every value above is written in the canonical `Parent: Child` form. Thirteen child names in the
`FunctionCategory` vocabulary sit on more than one row (`2D Slices`, `Analysis`, `Calibration`,
`Distribution/Access`, `Field-line Tracing`, `Infrastructure as Code`, `Instrument Response`,
`ML/AI`, `Mission-Specific`, `Observatory/Instrument Models`, `Packet Decommutation`, `Processing`,
`Spectrogram`), so an unqualified child can bind the wrong twin; three of those ambiguous names
(`2D Slices`, `Analysis`, `Processing`) are in use here. Each parent whose children appear is also
listed in its own right.

The order of this list is data, not presentation: `softwareFunctionality` is a sorted field whose
stored sequence carries a sort value and is the order a visitor reads on the entry page. The
sequence above is HSSI's existing stored order — Coordinate Transforms, then Data Processing and
Analysis, then Models and Simulations, then Data Visualization, then Servers and Environments —
with `Models and Simulations: Data Guided`, the one value added at this refresh, placed in its
alphabetical slot inside its own parent block. Appending that value at the end of the list was
rejected because it would strand a Models and Simulations child below the Servers and Environments
block; regrouping the whole list into alphabetical parent order was rejected because it would
resequence eight already-stored values for no gain in accuracy. This list is therefore not in
alphabetical parent order by oversight, and tidying it into that order would silently rewrite
stored data.

**Evidence for each value.**

- **Models and Simulations / First Principles / Physics-Based** — `Readme.md` line 9: "The GEMINI
  model (*G*eospace *E*nvironment *M*odel of *I*on-*N*eutral *I*nteractions) is a three-dimensional
  ionospheric fluid-electrodynamic model". The tree solves the multifluid transport equations
  (`src/multifluid/`), advection (`src/numerical/advection/advec.f90`), diffusion
  (`src/numerical/diffusion/PDEparabolic.f90`), and an elliptic electrostatic-potential problem
  (`src/numerical/potential/PDEelliptic.f90`, `elliptic2d.f90`, `elliptic3d.f90`) from the governing
  physics rather than from a fit.
- **Models and Simulations: Empirical** — the model's background state comes from empirical
  climatologies: MSIS00/MSIS 2.1 (`src/neutral/atmos.f90`, `config.nml` key `msis_version = 0` or
  `21`), HWM14 horizontal winds (`src/neutral/wind.f90`, `options.cmake` line 27
  `option(gemini3d_hwm14 "use HWM14 neutral winds model")`), the Fang 2008/2010 impact-ionization
  parameterizations (`src/ionization/fang.f90`, `fang_run.f90`), and NCAR GLOW
  (`options.cmake` line 25: `option(gemini3d_glow "use NCAR GLOW airglow / aurora model" on)`).
- **Models and Simulations: Data Guided** — *added at this refresh.* GEMINI is routinely driven by
  externally supplied, data-derived boundary conditions rather than run closed. `src/inputdata/`
  contains first-class reader objects for each driver: `efielddataobj.f90` (electric field /
  field-aligned current top boundary), `precipdataobj.f90` (particle precipitation),
  `solfluxdataobj.f90` (solar flux), and twelve `src/inputdata/neutraldata*obj*.f90` classes (the
  count is the pinned tree's, matched on that path pattern) for externally computed neutral
  perturbations and neutral background. `docs/Readme_input.md` documents the matching namelist groups
  `&precip` (`flagprecfile`), `&efield`, `&solflux`, and the top-boundary arrays `Vmaxx1it` /
  `Vminx1it` with `flagdirich` selecting whether the supplied data are potential or FAC. This is
  exactly the "data-driven boundaries, observational inputs" case; it was missing before this
  refresh.
- **Coordinate Transforms / Coordinate Transforms: Ionospheric** — `src/numerical/coord/geomagnetic.f90`
  exports a user-facing transform API — its `public ::` statement spans lines 14-15 and names
  `geomag2geog`, `geog2geomag`, `r2alt`, `alt2r`, `rotgg2gm`, `rotgm2gg`, `ECEFspher2ENU`,
  `ENU2ECEFspher` and the epoch-aware `set_magnetic_pole`. Companion
  modules `dipole.f90`, `spherical.f90` and `meshobj_dipole.f90` build dipole/curvilinear
  ionospheric grids, and `test/coord/geomag2geog_testdriver.f90` is a dedicated round-trip test.
  These are geographic↔geomagnetic/dipole conversions used for ionospheric grids, which is the
  "Ionospheric" child.
- **Data Processing and Analysis / Analysis / Processing** — `src/utils/magcalc.f90` is a separate
  post-processing program that reads a completed simulation's current densities and evaluates the
  Biot-Savart integral to produce magnetic perturbations at user-specified field points
  (`docs/Readme_magcalc.md`). `src/numerical/interpolation/`, `src/numerical/calculus/` (`div.f90`,
  `gradient.f90`, `integral.f90`) and `test/compare/` (frame-by-frame comparison of outputs) are
  further processing/analysis capabilities exposed to users.
- **Data Processing and Analysis: 2D Slices** — `test/interpolation/testinterp3.py` takes three
  orthogonal 2-D cuts out of a 3-D array (`fx1x2x3[ix3, :, :]`, `fx1x2x3[:, ix2, :]`,
  `fx1x2x3[:, :, ix1]`) before display; `src/numerical/interpolation/interp2d.f90` provides the 2-D
  interpolation used on such planes.
- **Data Visualization / 2D Graphics / 2D Slices / Line Plots** — these are evidenced *inside this
  repository*, not only by the Python front end. `test/potential/test_potential2d.py`,
  `test_potential2d_auroral.py`, `test/diffusion/test_diffusion1D.py`,
  `test/interpolation/testinterp.py` and `testinterp3.py` build Matplotlib figures with
  `pcolormesh` (2-D graphics), slice-plane displays (2-D slices) and `ax.plot(x1, fx1x2)` (line
  plots). `docs/Readme_output.md` additionally documents `gemini3d.plot.plot_all` and the MATLAB
  `plotall` as the project's standard output-viewing path.
- **Servers and Environments / High Performance Computing** — `src/mpimod/` (`mpihalo.f90`,
  `mpisend.f90`, `mpirecv.f90`, `autogrid.f90`) implements the domain decomposition; `Readme.md`
  line 44: "For example we have found that a 20M grid point simulations takes about  4 hours on 72
  Xeon E5 cores.  200M grid point simulations can take up to a week on 256 cores."; `docs/Readme_VEGA.md`, `docs/Readme_pleiades.md` and `docs/Readme_Dardel.md` are per-cluster
  deployment guides; `docs/Readme_mpi.md` covers MPI troubleshooting; and `test/mpi_launcher.cmake`
  plus the `download`/`offline` CTest presets exist specifically for batch nodes without internet.

**Considered and rejected — with the reasons, so a later refresh does not re-propose them.**

- **Models and Simulations: MHD.** `src/numerical/advection/` contains `MHD1D_SAW.f90`,
  `MHD1D_SND.f90` and `MHD1D_shock.f90`, whose two-line header comment reads (lines 3-4 of
  `MHD1D_SAW.f90`) `!A 'CLASSICAL HYDRODYNAMIC' SOLVER (WAVES PROPAGATED THRU SOURCE TERMS)` then
  `!FOR THE IDEAL MHD EQUATIONS IN 1.66 DIMENSIONS.  M. ZETTERGREN, T. SYMONS`. They look like an MHD capability and they are not. Each is a standalone `program`, each writes its own
  `MHD1D.dat`, and a whole-tree sweep for `MHD1D` at this revision finds 9 occurrences, all inside
  those same three files — the same 9 whether the search is case-sensitive or case-insensitive.
  `src/numerical/advection/CMakeLists.txt` builds only `advec.f90` and
  `advec_mpi.f90`, so the MHD drivers are never compiled or installed. GEMINI is a multifluid
  transport model, not an MHD code.
- **Coordinate Transforms: Magnetospheric.** That child covers GSE/GSM/SM/GEO/MAG conversions.
  GEMINI's `geomagnetic.f90` is a centered-dipole geographic↔geomagnetic transform built for
  ionospheric grids; there is no GSE/GSM/SM machinery. A user filtering on the magnetospheric child
  would not want this back.
- **Servers and Environments: Software or Environment Container.** No Dockerfile, Singularity or
  Apptainer definition exists at this revision (searched the whole pinned tree for `docker`,
  `singularity`, `apptainer` and `.def`; no file matched).
- **Models and Simulations: Observatory/Instrument Models.** `magcalc.bin` produces a synthetic
  observable (ground magnetic perturbation) at arbitrary user-supplied field points — "a list of
  ground stations (irregular mesh), a regular mesh, or a set of satellite tracks (irregular mesh)"
  (`docs/Readme_magcalc.md`). It models no named instrument's response, geometry or sampling; the
  points are whatever the user writes into `magfieldpoints.{h5,dat}`.
- **Data Processing and Analysis: Data Assimilation.** No assimilation scheme exists. GEMINI accepts
  prescribed boundary data (captured by "Data Guided"), which is forcing, not assimilation.
- **Data Processing and Analysis: Data Access and Retrieval.** Sweeping every `http(s)://` URL in
  the build and test machinery at this revision (`CMakeLists.txt`, `options.cmake`, `cmake/`,
  `scripts/`, `test/`), the URLs actually *fetched* rather than cited in a comment are the six
  dependency tarball stems in `cmake/libraries.json` and the reference-data archive in
  `test/test_urls.json`; the rest are documentation links inside comments. So the network activity
  is CMake `FetchContent` pulling dependency sources and CTest pulling reference *test fixtures*.
  Neither is a science-data retrieval API offered to users.
- **Data Processing and Analysis: File Format Conversion.** The `{raw, Matlab, NetCDF4} → HDF5`
  converters (`scripts/convert_data.py`, `scripts/convert_grid.py`) live in the *pygemini*
  repository, not in this one. It is the value this field would have gained had the entry been
  repointed at `gemini3d/pygemini`; it was not (Field 7), so the converters stay out of scope here.
- **Data Processing and Analysis: Time Series Analysis.** `src/temporal/` is simulation time-stepping
  and calendar utilities (`timeutils.f90`, `dateinc`, solar zenith angle), not analysis of
  time-ordered observations.

---
### 5. Related Region (RECOMMENDED — treated as critical)
**Values:**
- Earth Atmosphere
- Earth Auroral Subregion
- Earth Ionosphere
- Earth Thermosphere

**Order matters here.** `relatedRegion` is an ordered field — the rows carry a sort value — so the
four values above are intended in exactly the sequence listed: `Earth Atmosphere`,
`Earth Auroral Subregion`, `Earth Ionosphere`, `Earth Thermosphere`. That is alphabetical, which is
also the order the two previously stored values were held in, so nothing about the existing
convention changes.

The `Region` vocabulary is **flat**: every row is a top-level value, and no parent-child implication
exists between them. `Earth Ionosphere` therefore does not follow from `Earth Atmosphere`, and vice
versa — each coarse and each fine value has to be chosen on its own merits. Before this refresh the
record carried two coarse values and nothing finer — `Earth Atmosphere` and `Earth Magnetosphere` —
which left the model's actual domain unsearchable. Three fine values are added here and
`Earth Magnetosphere` is removed; the reasoning for the removal is below.

**Earth Ionosphere** — *added.* The single most obvious value and the one whose absence mattered
most. `Readme.md` line 9 calls GEMINI "a three-dimensional ionospheric fluid-electrodynamic model";
the GitHub repository description is "Ionospheric fluid electrodynamic model"; `codemeta.json`'s
`"description"` is the same string. A user browsing HSSI's Earth Ionosphere region and not finding
GEMINI is the clearest possible miss.

**Earth Thermosphere** — *added.* The model's vertical domain is the thermosphere:
`src/collisions/collisions.f90` line 543 notes "the grid extends from ~90-1000 km in altitude
approx.", and `src/multifluid/multifluid.f90` line 49 refers to "closed field-line grids extending
to high altitudes" versus "cartesian simulations not exceed altitudes of 1500 km". The model's own
name is "Model of Ion-Neutral Interactions", and the neutral partner is the thermosphere: MSIS
densities and temperature (`src/neutral/atmos.f90`) and HWM14 winds (`src/neutral/wind.f90`).
*The counter-argument, recorded so the next refresh can weigh it rather than rediscover it:* GEMINI
does not solve thermospheric dynamics. The neutral state is always prescribed — either from the
MSIS/HWM empirical background (`src/neutral/neutral_background_mod.f90`) or from an external model's
output read through `src/neutral/neutral_perturbations_mod.f90`. On balance the value is kept,
because the searcher's question is "is this software about that region", and a model of ion-neutral
interaction across 90-1000 km is.

**Earth Auroral Subregion** — *added.* Aurora is the first use case `Readme.md` lists (line 11,
"effects of auroras on the terrestrial ionosphere"). NCAR GLOW is built in **by default**
(`options.cmake` line 25: `option(gemini3d_glow "use NCAR GLOW airglow / aurora model" on)`), the
tree carries `src/io/aurora.f90` and `src/io/aurora_hdf5.f90` for auroral emission output, and
`test/potential/test_potential2d_auroral.f90` plus its Python plotter are auroral test cases. The
a case-insensitive whole-tree search for `auroral` at this revision matches 14 files.

**Earth Atmosphere** — *kept.* A coarse but true browse path: this is an atmospheric-region model,
and because the vocabulary is flat, dropping it would remove the entry from that browse entirely
without the finer values compensating.

**Earth Magnetosphere** — *HSSI carried this value before this refresh; it is removed at this
refresh.* It is recorded here at length because the evidence that once supported it is real and a
future refresh will meet the same evidence again.

What is true: GEMINI implements the magnetosphere-ionosphere coupling *interface*.
`docs/Readme_input.md` documents the top-boundary arrays `Vmaxx1it` and `Vminx1it` with
`"flagdirich"    ! (1) whether to treat the data in Vmax{min}x1 arrays as potential (1 value) or FAC
(0 value)"`, and `flagcap = 2` / `magcap` add "ionospheric+magnetospheric parts" of the inertial
capacitance (`src/io/config.f90` lines 84-85; `src/collisions/collisions.f90` line 540). The
published work the repository lists is squarely M-I coupling science (cusp flow channels, RENU2,
MICA). None of that is withdrawn.

Why it is nevertheless not a Region value: GEMINI's domain stops at the top of the ionosphere. The
magnetosphere enters only as a boundary condition and a lumped capacitance — a *driver* of the
modelled region, not a region the software models. A Region value asserts where the software works,
and on that test the magnetosphere fails. The counter-argument that once carried it — that a
searcher browsing Earth Magnetosphere for the ionospheric end of an M-I coupling problem would be
glad to find GEMINI — was considered and not accepted: it would equally admit every ionospheric
model with a magnetospheric boundary condition, which is most of them, and it is not a ground the
field's rule offers. The M-I coupling literature remains discoverable through Field 27, where those
publications are recorded.

**Considered and not selected.**

- **Earth Lower and Middle Atmosphere** — the grid bottom sits at the mesopause, not below it.
  `src/collisions/collisions.f90` line 543 assumes "~90-1000 km", and the shipped
  `test/config/config_example.nml` sets `alt_min = 80e3` / `alt_max = 1000e3`; 80 km is the upper
  mesosphere, and nothing in the troposphere, stratosphere or lower mesosphere is modelled. A
  case-insensitive whole-tree search for `mesospher` at this revision matches zero files (control:
  `ionospher`, same query shape, matches 21). The stored keyword
  `ionosphere_thermosphere_mesosphere` is a PyHC registry token (see Field 16), not evidence of a
  mesospheric domain.
- **Earth Inner Magnetosphere / Earth Outer Magnetosphere / Earth Magnetotail / Earth Magnetosheath**
  — no part of the model is in any of these. They fail for the same reason the coarse
  `Earth Magnetosphere` fails above, only more sharply: naming a *specific* magnetospheric region
  would be a stronger claim still than the boundary-condition evidence supports.
- **Solar Wind, Solar Environment, Corona, Chromosphere, Photosphere, Solar Interior, Heliosheath,
  Interplanetary Space, Planetary Magnetospheres and the four named planetary magnetospheres** —
  out of domain. GEMINI is terrestrial, and solar conditions enter it as scalar drivers — the
  `activ` triple of `f107a,f107,Ap` in `&base`, and the optional `&solflux` time series — not as a
  modelled region.

---

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Matthew Zettergren
- **Author Identifier:** https://orcid.org/0000-0002-9837-059X
- **Affiliation:** Not recorded

**Author 2:**
- **Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation:** Boston University (https://ror.org/05qwgg493); Scivision, Inc.

**Why these two, and only these two.** Four independent sources agree on exactly this pair with
exactly these ORCIDs:

- `CITATION.cff` at this revision — `family-names: Zettergren` / `given-names: Matthew` /
  `orcid: 0000-0002-9837-059X`, and `family-names: Hirsch` / `given-names: Michael` /
  `orcid: 0000-0002-1637-6526`.
- `codemeta.json` at this revision — two `"@type": "Person"` entries with `"@id"` set to the same
  two ORCID URLs and matching `givenName`/`familyName`.
- The concept DOI record `10.5281/zenodo.3647579` — creators `Zettergren, Matthew` and
  `Hirsch, Michael`, each with an ORCID `nameIdentifier`.
- The current version DOI record `10.5281/zenodo.10475267` — the same two creators with the same
  ORCIDs.

Both display names match the primary name on the corresponding ORCID `/person` record exactly
(`given-names` "Matthew" / `family-name` "Zettergren"; "Michael" / "Hirsch"). Neither ORCID record
has a credit name or any `other-names` entry, so there is no alternative display form to prefer.

**Zenodo `contributors` were checked and are empty.** Both the 3813224 and 10475267 Zenodo records
return `"contributors": null`; neither adds anyone beyond the creators. Neither record's creators
carry an `affiliation` value, so Zenodo supplies no affiliation for either author (and no packed
`1 - … 2 - …` affiliation string exists to unpack).

**No `.mailmap`, `.zenodo.json`, `AUTHORS` or `CONTRIBUTORS` file exists** — not at this revision,
and none was ever added anywhere in the history reachable from it (searched the full add-history for
those names). Besides the four sources above, the only other files at this revision that name a
person are `ford.md` (its `author:` block, discussed below) and `.github/CODEOWNERS`, which lists
the GitHub handles `@mattzett` and `@scivision` — Zettergren and Hirsch again.

**Considered and not added: Guy Grubbs.** Real evidence exists for him and it is worth recording so
the question is settled rather than reopened every refresh:

- `ford.md` lists three names under `author:` — `Matthew Zettergren`, `Guy Grubbs`,
  `Michael Hirsch`. That block configures the FORD documentation generator's author credit.
- The superseded version record `10.5281/zenodo.3813224` (v0.5.6, 2020) lists three creators:
  `Michael Hirsch, Ph.D.`, `Zettergren, Matthew D.` and `Guygrubbs` (Zenodo's own JSON renders the
  third as `guygrubbs`).
- The commit history reachable from this revision contains five commits from him, under two
  identities: `Grubbs <ggrubbs1@gs673-guydt.ndc.nasa.gov>` (4) and
  `guygrubbs <guygrubbs@gmail.com>` (1).

He is nevertheless **not** added, because every *current* authorship declaration the project
maintains — `CITATION.cff`, `codemeta.json`, and both live Zenodo records for the concept DOI and the
current version — names two authors. The 3813224 record is the same one rejected in Field 2 as stale,
and it is stale in its creator list too: the names there are degraded (`Michael Hirsch, Ph.D.` is
parsed by DataCite into `givenName: "Ph.D."` / `familyName: "Michael Hirsch"`, and none of the three
carries an ORCID). Importing authorship from that record would make the entry worse, not better.

**Considered and not added: other frequent committers.** Counting commits reachable from this
revision and grouping each person's several author identities: Joaquín Díaz 32 (4 identities),
Pavel Inchin 25 (4), Pralay Vaggu 16 (2), Jules van Irsel 7 (2), Lehar Joshi 3, Scott Aiton 2 and
Jeff Klenzing 1. None is named in any of the project's authorship declarations. Field 6 records
declared authorship, not contribution volume.

**Affiliations.**

- Hirsch's two stored affiliations are corroborated. His ORCID employments record a single entry:
  **Boston University**, role "Research Scientist", Boston MA US, start 2018-08, no end date — and
  ROR `https://ror.org/05qwgg493` has `ror_display` exactly `Boston University` (status active).
  Note the ORCID record disambiguates Boston University by RINGGOLD id 1846, not by ROR, so the ROR
  was matched on name rather than carried across from ORCID. **Scivision, Inc.** is stored without an
  identifier; it is Hirsch's own consultancy and the source of his `scivision` commit identity, and
  it does not appear in his ORCID employments.
- Zettergren has no affiliation recorded, and this refresh does not propose one. His ORCID record
  lists **no employments at all**, so the authoritative source is silent. Circumstantial evidence
  points to Embry-Riddle Aeronautical University — `docs/Readme_VEGA.md` is titled for "ERAU's VEGA
  HPC system", several of his commits carry hostnames under `…erau.edu`, and all six theses listed
  in `docs/Readme_references.md` are Embry-Riddle Aeronautical University or Dartmouth College
  dissertations — but a build-machine
  hostname is not an authorship affiliation statement, and inventing one from inference would be
  worse than leaving the field honestly empty. If a maintainer confirms it, ERAU's ROR is the value
  to look up at that point.

---
### 7. Software Name (MANDATORY)
**Value:** PyGemini

**The entry keeps the PyHC registry's name and the registry's pairing of that name with the Fortran
repository.** The question of whether it should was asked seriously — the name on this entry is not
the name the repository gives itself, and a separate repository genuinely called PyGemini exists —
and it was settled in favour of the stored pairing. The whole of that inquiry is recorded below,
including the evidence that pointed the other way, so that a future refresh can see the question was
examined rather than overlooked, and need not reopen it from scratch.

#### The mismatch that prompted the question

The form says Field 7 is "The name of the software package as listed on the code repository." At the
repository recorded in Field 3 (`https://github.com/gemini3d/gemini3d`), at the pinned revision, the
package is **not** listed as PyGemini:

| Source at `aa50fa1a` | Name it gives |
|---|---|
| `Readme.md` line 1 | `# GEMINI` |
| `Readme.md` line 9 | "The GEMINI model (*G*eospace *E*nvironment *M*odel of *I*on-*N*eutral *I*nteractions)" |
| `CITATION.cff` | `title: Gemini3D` |
| `codemeta.json` | `"name": "Gemini3D"` |
| `CMakeLists.txt` | `project(gemini3d … DESCRIPTION "3-D ionospheric model" … VERSION 2.0.0)` |
| `ford.md` | `project: GEMINI3D` |
| GitHub repository metadata | `gemini3d/gemini3d`, description "Ionospheric fluid electrodynamic model" |
| DOI record `10.5281/zenodo.3647579` | title `Gemini3D` |

The name "PyGemini" *does* occur in the repository — and every occurrence treats it as a **different,
externally installed package** rather than as this repository's own name. That is a stronger
statement than mere absence would be, so it is measured rather than asserted. Sweeping the whole
pinned tree at revision `aa50fa1a` with `git grep`:

- case-**sensitive** `PyGemini`: **5 occurrences in 4 files** — `Readme.md` (1),
  `cmake/python.cmake` (1), `cmake/summary.cmake` (1), `test/compare/compare.f90` (2).
- case-**insensitive** `pygemini`: **21 occurrences in 8 files**, adding `docs/Readme_Dardel.md` (6),
  `docs/Readme_VEGA_updated2.md` (3), `test/config.cmake` (2) and `test/compare/CMakeLists.txt` (1).
  The tree spells it five different ways: `pygemini` (6), `PyGemini` (5), `PYGEMINI` (4),
  `PyGEMINI` (4), `Pygemini` (2). Every matching line contains exactly one occurrence, so the line
  and occurrence counts coincide here.
- Controls under the identical query shape and scope: case-insensitive `gemini` returns 1,755
  occurrences (exit 0); a nonsense token returns 0 (exit 1). The instrument can see both a positive
  and a true negative.

**What those 21 occurrences do.** They divide into four groups, and none of them is the repository
naming itself:

1. **The build system probes for it as an external dependency.** `cmake/python.cmake` defines
   `function(check_pygemini)`, which runs the ambient interpreter as a subprocess —
   `execute_process(COMMAND ${Python_EXECUTABLE} -c "import gemini3d;
   print(gemini3d.__version__)")` — and aborts with `message(FATAL_ERROR "Failed to get PyGemini
   version: …")` if that import fails. This is the shape of a find-module for a third-party package:
   it asks whether a *separately installed distribution* is importable, and treats its absence as
   fatal rather than trying to supply it. It cannot build PyGemini, because PyGemini is not in this
   tree. Note what the function does **not** do: `PYGEMINI_FOUND` occurs exactly once in the whole
   tree, in the call guard at `cmake/python.cmake` line 64
   (`if(Python_FOUND AND NOT DEFINED PYGEMINI_FOUND)`), and nothing anywhere `set()`s it — the only
   cache variable the function writes is `set(H5PY_FOUND true CACHE BOOL "Python h5py Found")` at
   line 28. So the guard is a caller-overridable escape hatch that this repository never defines, and
   the probe runs whenever Python is found.
2. **The build summary lists it as an optional feature.** `cmake/summary.cmake` line 9:
   `add_feature_info(PyGemini gemini3d_python "simulation generation, HPC script generator and
   plotting")` — PyGemini is an optional capability of the build, gated on `gemini3d_python`, and the
   description is of what the *other* package supplies.
3. **The test suite invokes it by subprocess and skips when it is absent.**
   `test/compare/compare.f90` builds `cmd = "python -m gemini3d.compare " // new_file // " " //
   ref_file // " -plot"` and runs it through `execute_command_line`, reporting on failure
   `"ERROR: failed to plot diff using PyGemini: "`. The `elseif(P%matlab)` branch of the same
   subroutine shells out to `gemini3d.plot.plotdiff` and reports `"ERROR: failed to plot diff using
   MatGemini: "` — the code treats PyGemini and MatGemini as two interchangeable **external** front
   ends. `test/compare/CMakeLists.txt` line 57 and `test/config.cmake` lines 274 and 283 carry
   `DISABLED $<NOT:$<BOOL:${PYGEMINI_DIR}>>`, disabling those tests when the external component is
   not pointed at.
4. **The HPC documentation tells users to install it from its own repository.**
   `docs/Readme_Dardel.md` line 71 is titled "## Installing PyGEMINI on KTH's Dardel with Bash" and
   lines 81 and 89 point at `https://github.com/gemini3d/pygemini`; line 83 states "Pygemini plotting
   is independent of the gemini3d build. One can directly clone it and plot outputs from simulation
   files." `docs/Readme_VEGA_updated2.md` lines 78, 91 and 106 do the same for ERAU's VEGA.

The single `Readme.md` occurrence in the case-sensitive set says the same thing in prose — line 149:
"GEMINI can also be run via scripting frontend of PyGemini `python -m gemini3d.run -np`, or the
executable `gemini3d.run`." — and the second, lower-case `Readme.md` occurrence at line 189 is
"there are python and MATLAB scripts available in the mat_gemini and pygemini repositories", naming
pygemini as one of two sibling **repositories**.

So the Fortran repository does not merely decline to call itself PyGemini; its CMake, its CTest
gating and its Fortran test harness **integrate PyGemini as a separate component they detect and
call out to**. The mismatch in this field is therefore not a naming preference — the software this
entry points at demonstrates, in executable form, that PyGemini is a different piece of software.

#### Where the name came from

From the PyHC registry. `_data/projects_unevaluated.yml` carries this entry verbatim:

```yaml
- name: PyGemini
  description: Python frontend for Gemini3D ionospheric kintic + fluid dynamics models
  code: https://github.com/gemini3d/gemini3d
  contact: Michael Hirsch
  keywords: ["ionosphere_thermosphere_mesosphere","specific"]
```

(The `kintic` typo is the registry's.) The registry itself pairs the Python-frontend *name* with the
Fortran-core *repository*, and HSSI inherited that pairing. PyGemini appears in neither of the other
two registry files: searching `projects.yml` (58 `- name:` entries) and `projects_core.yml` (7)
case-insensitively for `pygemini` returns 0 in each, and for `gemini` returns 0 in each as well.

#### The two candidate repositories, characterised

| | `gemini3d/gemini3d` (stored in Field 3) | `gemini3d/pygemini` |
|---|---|---|
| GitHub description | "Ionospheric fluid electrodynamic model" | "Python interface for Gemini3D" |
| Primary language | Fortran | Python |
| Created | 2018-08-31 | 2020-06-17 |
| Last push observed | 2026-09-11 | 2026-08-12 |
| Licence | Apache-2.0 (`LICENSE`) | Apache-2.0 (`LICENSE.txt`) |
| `CITATION.cff` / `codemeta.json` | both present | neither present |
| Concept DOI | `10.5281/zenodo.3647579` (57 versions) | `10.5281/zenodo.3910038` (20 versions) |
| Latest version DOI | `10.5281/zenodo.10475267`, v1.7.0, 2024-01-09 | `10.5281/zenodo.7675594`, v1.7.1, 2023-02-24 |
| DOI creators | Zettergren, Hirsch (both with ORCIDs) | Scivision; Zettergren, Matthew D.; Wright, Isaac; Hatch, Spencer (Birkeland Centre for Space Science) — none with an ORCID |
| Distribution | source build via CMake; no PyPI package | PyPI `gemini3d`, latest 1.7.0 uploaded 2023-02-19 |
| Documentation | FORD site `https://gemini3d.github.io/gemini3d/` (live) | `Readme.md` only; no Pages site |
| Wiki | separate wiki repo exists, last edited 2020-03-09 | separate wiki repo exists, last edited 2020-10-14 |
| What it contains | 163 Fortran sources: multifluid solver, elliptic/parabolic solvers, MPI decomposition, MSIS/HWM/GLOW/Fang coupling, `magcalc` | `src/gemini3d/`: `config.py`, `read.py`, `write.py`, `plot/`, `coord.py`, `grid/`, `efield/`, `particles/`, `magcalc.py`, `msis.py`, `run.py`, `model.py`, `hpc.py`, `web.py`, raw/MATLAB/NetCDF4 → HDF5 converters |
| Its own name for itself | `# GEMINI` | `# PyGemini` |

The Python package's PyPI distribution name is `gemini3d` and its summary is "3-D ionospheric model
plotting suite"; the PyPI long description is the pygemini `Readme.md`, which opens `# PyGemini` and
links `https://github.com/gemini3d/pygemini`, confirming the PyPI name belongs to that repository and
not to the Fortran one.

#### The evidence pointing the other way — considered, and not determinative

This is the case against the stored pairing. It is genuine, it is not refuted below, and it is
recorded in full because a future refresh will meet it again and should know it was weighed rather
than missed.

A visitor who searches HSSI for "PyGemini" may well be looking for the Python package they
`pip install` or `import gemini3d` — the thing whose own README is titled `# PyGemini`. Under the
stored pairing they land on an entry named PyGemini whose repository link takes them to a Fortran
codebase titled `# GEMINI`, and whose Field 12 version (v1.7.0, 2024-01-09) is the *Fortran*
release, not the Python one (v1.7.1, 2023-02-24). Conversely, a visitor searching for "GEMINI" or
"Gemini3D" — the name used in the publications of Field 27 — finds an entry called PyGemini.

There is also a corroborating outside signal: the HSSI entry `amisrsynthdata` lists
`https://github.com/gemini3d/pygemini` in its own interoperable software, so the catalogue contains a
pointer to the *Python* repository that resolves to no HSSI entry of its own, while the entry
actually named PyGemini points elsewhere.

What blunts this, and is why it did not carry: both halves of the confusion are addressed inside the
entry rather than by moving it. Field 8's description names the pairing in its first clause, and
Field 30 lists `https://github.com/gemini3d/pygemini` as interoperable software, so a visitor who
arrives looking for the Python package is told immediately what they have found and is given the
link to it. The `amisrsynthdata` pointer is likewise reciprocated from Field 30 rather than left
dangling.

#### Why the stored pairing stands

The name and the repository are kept together as they are, for four reasons that hold at this
revision:

- **This entry is the PyHC registry's entry, under the registry's own name and pairing.** The
  registry is what brought the software into the catalogue, and it is the registry that pairs the
  name "PyGemini" with `gemini3d/gemini3d`. Renaming the entry or repointing it would make the
  catalogue disagree with its own upstream source about which record this is.
- **The two repositories are one stack, and the Fortran core says so itself.** `Readme.md` line 149
  documents the Python frontend as a standard way to run the model, and the CMake and CTest
  integration catalogued above is the core project treating PyGemini as a component it expects its
  users to have. A user who reaches this entry reaches the whole stack.
- **The publications describe the model this entry points at.** Every paper in Field 27 is about
  GEMINI the model, not about the Python wrapper. Repointing the entry at `gemini3d/pygemini` would
  leave the catalogue holding the wrapper while the literature, the DOI series with the ORCID-bearing
  creators, the licence history and the release record all belong to the Fortran repository.
- **The entry already discloses the pairing to its readers.** Field 8's description opens "PyGemini
  is the PyHC registry name for the Gemini3D/GEMINI software stack", so a visitor is told in the
  first clause what the name refers to. The disclosure is deliberate and is retained.

The acknowledged cost is that Field 7 does not reproduce the name the repository gives itself, which
is what the form's wording asks for. That cost is accepted: the form's instruction serves the goal of
making an entry findable and unambiguous to a reader, and here the registry name plus the
first-clause disclosure achieves that better than a rename would.

#### The alternatives, and why they were not taken

- **Renaming the entry to GEMINI or Gemini3D while keeping the repository.** The smallest change that
  would make name and repository agree, and the closest call. Fields 2, 6, 10, 12, 13, 15, 23 and 24
  all already describe the Fortran repository, so only Field 7 and the leading clause of Fields 8 and
  9 would have moved. It was not taken because it would sever the entry from the PyHC registry
  record that is its provenance, and because a reader searching the registry's name would then find
  nothing.
- **Repointing the entry at `gemini3d/pygemini` while keeping the name.** The largest change, and it
  would have touched most of the record: Field 2 → `10.5281/zenodo.3910038`; Field 3 →
  `https://github.com/gemini3d/pygemini`; Field 6 → a four-person creator list with no ORCIDs
  (Scivision, Zettergren, Isaac Wright, Spencer Hatch); Field 10 → 2020-06-17; Field 12 → v1.7.1 /
  2023-02-24 / `10.5281/zenodo.7675594`; Field 13 → Python 3.x only; Field 24 → no Pages site;
  Field 4 would gain `Data Processing and Analysis: File Format Conversion` and lose the
  first-principles and HPC values; Fields 29 and 30 would invert, the Fortran core becoming the
  related software. It was not taken because it would leave HSSI carrying the Python wrapper instead
  of the model the literature describes.
- **Splitting into two entries, one per repository.** The most faithful representation of what the
  two repositories actually are, and the most work. Creating a second catalogue entry is beyond what
  a metadata refresh does, so it was not pursued here; it remains the option a future curator would
  reach for if the two repositories diverge further.

---

### 8. Description (MANDATORY)
**Value:** PyGemini is the PyHC registry name for the Gemini3D/GEMINI software stack, a three-dimensional ionospheric fluid-electrodynamic model written primarily in object-oriented Fortran 2008. GEMINI is used for studies of auroral effects on the terrestrial ionosphere, natural hazard effects on the space environment, and ionospheric fluid instabilities that affect radio propagation. The model uses generalized orthogonal curvilinear coordinates, has been tested with dipole and Cartesian coordinates, supports MPI/HPC execution, and includes Python/MATLAB-facing workflows for running simulations and loading, plotting, and analyzing HDF5 output.

**Kept unchanged, and it holds up against the source.** Clause by clause, the description tracks
`Readme.md` at this revision:

- "three-dimensional ionospheric fluid-electrodynamic model written primarily in object-oriented
  Fortran 2008" ← line 9, "a three-dimensional ionospheric fluid-electrodynamic model written
  (mostly) in object-oriented fortran (2008+ standard)".
- the three use cases ← lines 11-13, "effects of auroras on the terrestrial ionosphere" /
  "natural hazard effects on the space environment" / "effects of ionospheric fluid instabilities on
  radio propagation".
- "generalized orthogonal curvilinear coordinates, has been tested with dipole and Cartesian
  coordinates" ← line 21, "GEMINI uses generalized orthogonal curvilinear coordinates and has been
  tested with dipole and Cartesian coordinates."
- "supports MPI/HPC execution" ← the Platforms section and `src/mpimod/`.
- "Python/MATLAB-facing workflows for running simulations and loading, plotting, and analyzing HDF5
  output" ← lines 149 and 189, the "Loading and plotting output" section at lines 191-195, and
  `docs/Readme_output.md`.

The opening clause — "PyGemini is the PyHC registry name for the Gemini3D/GEMINI software stack" — is
an honest disclosure of the naming question examined under Field 7 rather than an error, and it is
verifiably true: the registry entry quoted there is exactly that. It is deliberately retained — with
the pairing settled as it stands, that clause is what tells a visitor who arrived looking for the
Python package what they have actually found.

**Not replaced.** This wording is a prior curator's, it is accurate, and it is well above the form's
bar ("sufficiently detailed to provide the potential user with information to determine if the
software is useful"). Rewriting it for style would discard editorial intent for nothing.

---

### 9. Concise Description (OPTIONAL)
**Value:** PyHC entry for the Gemini3D ionospheric fluid-electrodynamic model and scripting workflows for simulations, HDF5 output, plotting, and analysis.

**Kept unchanged.** 144 characters — just under the form's 150-200 character preview window, close
enough that no reworking is warranted — and it says
what the software is rather than repeating the first sentence of Field 8. No change proposed.

---
### 10. Publication Date (RECOMMENDED)
**Value:** 2018-08-31

**Unchanged, and the stored value already follows a defensible rule — first public availability of
the source.** Two independent measurements land on the same instant: the first commit reachable from
this revision is `c136f342095715f4768c6adf5ec6b5dd81304487`, "Initial commit", authored
`2018-08-31T13:07:22-04:00`; GitHub reports the repository's `created_at` as
`2018-08-31T17:07:22Z`. Those are the same moment in two time zones. The form's wording — "Date of
first broadcast/publication ... Used for the initial version of the software" — is satisfied by the
date the code first became public.

**Considered and rejected: 2020-02-05.** That is the issue date of `10.5281/zenodo.3647580`
(v0.2.0, titled `gemini3d/GEMINI: KHI JGR version of code`), the lowest-numbered and therefore
earliest of the 57 versions under the concept DOI — i.e. the date the software was first *published
with a DOI*. It is a coherent alternative reading of "publication", but it would post-date the
software's actual public availability by seventeen months and would mislead a user trying to place
the model in time relative to the 2012-2019 publications in Field 27. The earlier, source-based rule
is kept.

**What the rejected alternative would have implied.** Had the entry been repointed at
`gemini3d/pygemini` (Field 7), this date would have become 2020-06-17, that repository's
`created_at`. It was not, so the Fortran repository's first-availability date stands.

---

### 11. Publisher (RECOMMENDED)

**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Unchanged.** The form says that where a DOI was obtained through Zenodo, Zenodo is the correct
entry. The Field 2 concept DOI and the Field 12 version DOI are both `10.5281/zenodo.*` and both
DataCite records give `"publisher": {"name": "Zenodo"}`. `https://zenodo.org` is the appropriate
identifier: Zenodo is not an organisation with a ROR of its own in the sense the form's ROR example
intends, and the URL is what the form prescribes as the fallback.

**Considered and rejected: GitHub.** The form directs to the repository host *only* if no DOI has
been obtained. A DOI has been obtained.

---

### 12. Version (RECOMMENDED)

**Version Number:** v1.7.0

**Version Date:** 2024-01-09

**Version Description:** Working release wrapping up late 2022 and all 2023 changes, before implementing Git Submodules in Gemini3D. CI passes: Linux (GCC 9,10,11,12,13, Intel oneAPI 2024.0), macOS (GCC 13).

**Version PID:** https://doi.org/10.5281/zenodo.10475267

**All four sub-fields unchanged. The reason this needs explaining is that the repository looks like
it has moved on, and in the sense that matters for this field it has not.**

**v1.7.0 is still the latest release.** The newest tag reachable from the pinned revision is
`v1.7.0`, on commit `169ca673a574db990d8366b45016a9b22fc04590`, dated 2024-01-09; 58 tags are
reachable from the pin and none sorts later. GitHub lists 56 releases, the most recent being
`v1.7.0`, published 2024-01-09, release name "release before Git submodule". The Zenodo concept
record's own `version` field reads `v1.7.0`.

**The 2.0.0 in `CMakeLists.txt` is not a release, and a future refresh must not treat it as one.**
At the pinned revision `CMakeLists.txt` declares `VERSION 2.0.0` inside its `project(gemini3d …)`
call. At the `v1.7.0` tag the same line reads `VERSION 1.7.0`. The bump to `2.0.0` was made in
commit `62f8ea9e18fc72512f74b7455055e421db197f6b` ("eliminate C_BOOL", 2026-03-30) and no tag, no
GitHub release and no Zenodo deposit corresponds to it — searching every tag in the clone for one
beginning `v2` or `2` returns nothing. It is an in-development version number on the `main` line.
Field 12 asks for a released, citable version, and `Version PID` in particular requires a DOI that
2.0.0 does not have.

**There is a large amount of unreleased work, and that is a fact about the project, not about this
field.** 641 commits separate `v1.7.0` from the pinned revision, and the most recent of them is
dated the same day as the pin. A user reading Field 12 should understand that v1.7.0 is the latest
*release* and that `main` is considerably ahead of it — which is exactly what `Readme.md` line 23
tells them: "Generally, the Git `main` branch has the current development version and is the best
place to start, while more thoroughly-tested releases happen regularly."

**The stored Version Description is wholly attributable upstream — no clause is invented.** There is
no `CHANGELOG`, `NEWS`, `HISTORY` or release-notes file anywhere at this revision (searched the
pinned tree for those names, case-insensitively; nothing matched), so the only release notes are the
GitHub release body, which reads:

> making a working release wrapping up late 2022 and all 2023 changes, before implementing Git
> Submodules in Gemini3D.
>
> CI passes:
>
> * Linux: GCC 9,10,11,12,13, Intel oneAPI 2024.0
> * macOS: GCC 13

Taking the stored description clause by clause:

- "Working release wrapping up late 2022 and all 2023 changes, before implementing Git Submodules in
  Gemini3D." — **inherited**, verbatim in substance; the edit drops the leading "making a" and
  capitalises. Tested against the release's actual range: `v1.6.1..v1.7.0` is 366 commits whose
  author dates run from 2022-07 to 2024-01, covering every month of 2023. The author's own phrase
  "late 2022" understates the 95 commits dated 2022-07 and 2022-08 at the start of the range, but
  this is the upstream wording and it is substantially right.
- "CI passes: Linux (GCC 9,10,11,12,13, Intel oneAPI 2024.0), macOS (GCC 13)." — **inherited**;
  the only change is bullets reflowed into parentheses.
- Nothing in the stored text is **unattributable**. The release *name* ("release before Git
  submodule") adds no information the body does not already carry, so its omission costs nothing.

**A note the description turns out to have got right, and then history overtook.** The release
announced itself as coming "before implementing Git Submodules in Gemini3D". Submodules were indeed
implemented eight days later (`.gitmodules` added 2024-01-17) — and then removed again on 2026-03-23
in favour of CMake `FetchContent`. The pinned tree has no submodules. This does not affect the field;
it is recorded because `Readme.md` still instructs `git clone --recurse-submodules`, and a future
reader comparing the release note, the README and the tree will otherwise think one of them is wrong.

**Version PID.** `10.5281/zenodo.10475267` is the version DOI for v1.7.0 (DataCite: version `v1.7.0`,
issued 2024-01-09, `IsVersionOf 10.5281/zenodo.3647579`, `IsSupplementTo
https://github.com/gemini3d/gemini3d/tree/v1.7.0`). It is the newest of the 57 versions under the
concept DOI — the next-highest record number is `10.5281/zenodo.6812158`.

**What the rejected alternative would have implied, and a trap it leaves behind.** Had the entry
been repointed at `gemini3d/pygemini` (Field 7), all four sub-fields would have become the Python
package's v1.7.1 / 2023-02-24 / `https://doi.org/10.5281/zenodo.7675594`. It was not. The trap
survives the decision and is worth carrying forward: both repositories use a `v1.7.x` series, so a
future refresh must take care not to conflate them.

---

### 13. Programming Language (RECOMMENDED)
**Values:**
- C
- C++
- Fortran 2008
- Python 3.x

**Unchanged. The criterion is the form's own: "Select the most important languages (e.g., Python,
Fortran, C). This is not meant to be an exhaustive list."** So the test is importance to the
software, not presence in the tree — which decides the inclusions and, more usefully, the
exclusions.

**Included.**

- **Fortran 2008** — the model itself. `Readme.md` line 9: "written (mostly) in object-oriented
  fortran (2008+ standard)". 163 of the 290 files at this revision are `.f90`. The vocabulary offers
  `Fortran 2003`, `Fortran 2008`, `Fortran 2023`, `Fortran77` and `Fortran90`; `Fortran 2008` is the
  standard the README names, and the code's `implicit none (type, external)` and submodule usage are
  2008-and-later features.
- **C** and **C++** — not incidental. `CMakeLists.txt` declares `project(gemini3d LANGUAGES C CXX
  Fortran …)` with the comment "Gemini3D is Fortran, but external libraries use C, and some
  find_package need C." More decisively, `AGENTS.md` at this revision opens: "the `bind(C)` interface
  is a vital capability that couples to external programs written in C and C++." The tree carries
  `include/gemini3d.h` (the public C header), `app/main.cpp` (a C++ entry point beside the Fortran
  `app/main.f90`), `src/libgemini_c.f90` and `src/libgemini_mpi_c.f90` (the `bind(C)` layer),
  `src/utils/cpu_count.cpp`, and `test/test_hdf5.c`. `Readme.md` line 55 lists "C, C++ and Fortran compiler"
  as a build requirement. A C/C++ program embedding GEMINI is a supported use.
- **Python 3.x** — the project's stated interface language. `docs/Readme_output.md` documents
  `import gemini3d.plot` (line 10) and `import gemini3d.read` (line 35) as *the* way to plot and load
  output, and line 193 of `Readme.md` states "GEMINI uses Python for essential interfaces, plotting
  and analysis."
  `Readme.md` line 60 lists "Python and/or MATLAB for scripting front- and back-ends". Eight `.py`
  files are in the pinned tree itself (six test drivers/plotters, `test/temporal/PlotSZA.py`, and
  `scripts/check_subprojects.py`), and `options.cmake` line 29 exposes
  `option(gemini3d_python "Python-based self-checks")`.

**Excluded, with reasons.**

- **CMake** — the build system is written in CMake (at this revision, 32 `CMakeLists.txt` files and
  24 `.cmake` files, plus `CMakePresets.json`), and CMake has no row in the 19-row
  `ProgrammingLanguage` vocabulary. Even if it were, a
  build language is not one of "the languages most important for the software" in the sense a user
  filtering by language means.
- **MATLAB** — `MATLAB` *is* a vocabulary row, and `Readme.md` line 60 names MATLAB alongside Python
  as a scripting front/back-end, with `options.cmake` line 31 offering
  `option(gemini3d_matlab "Matlab-based self-checks")`. It is excluded because no MATLAB source
  exists in this repository: the MATLAB side lives entirely in `gemini3d/mat_gemini`, which is
  recorded in Field 29 and Field 30. Including it here would attribute another repository's language
  to this one. *This is the exclusion most likely to be re-proposed; the reason is the repository
  boundary, not a judgement that MATLAB is unimportant.*
- **Fortran 2023, Fortran 2003, Fortran90, Fortran77** — the README names the 2008+ standard, and
  listing several Fortran rows for one body of code would dilute rather than inform.
- **Other** — a catch-all adds nothing when four precise rows already cover the code.
- **Shell / PowerShell** — three `.sh` and one `.ps1` file exist (`scripts/hwm14_debug.sh`,
  `scripts/hwm14_oneapi_windows.ps1`, and two CI helper scripts). They are build/CI glue; neither has
  a vocabulary row and neither is important to the software.

**Note on `pyproject.toml`.** The top-level `pyproject.toml` at this revision configures only
`[tool.black]` and `[tool.mypy]`. It declares no package, no build backend and no dependencies — it
is linting configuration, not evidence of a Python distribution in this repository. (The Python
*distribution* named `gemini3d` on PyPI is built from `gemini3d/pygemini`; see Field 7.)

---
### 14. Reference Publication (OPTIONAL)
**Value:** Not found

**This is a researched negative, not an unexamined blank.** The form wants "the DOI for the
publication describing the software, sometimes used as the preferred citation for the software in
addition to the version-specific citation to the code itself (e.g., a JOSS paper)."

**What the project itself says.** `CITATION.cff` at this revision has no `preferred-citation` block
at all — the whole file is ten lines: `cff-version`, an `authors:` list of two people,
`title: Gemini3D`, and a `doi:`. The project
therefore directs citation to the software DOI and designates no paper. `codemeta.json` likewise
carries no `referencePublication`.

**Where one was looked for and not found.** Searched ADS/Sci-X for a model-description paper:
`title:"Geospace Environment Model of Ion-Neutral Interactions"` returns 0; `bibstem:JOSS
full:"gemini3d"` returns 0 — there is no JOSS paper. A nonsense-title control query returned 0 and
an unrestricted `full:"gemini3d"` query returned 28 records, so the instrument was capable of both
a true negative and a true positive. The 28 hits are science applications and conference abstracts,
not software descriptions.

**Considered and rejected: `https://doi.org/10.1029/2012JA017637`** (Zettergren & Semeter 2012,
"Ionospheric plasma transport and loss in auroral downward current regions"). It is the model's
first appearance — `docs/Readme_references.md` line 3 opens "Since its first appearance in 2012,
GEMINI has been used in over 15 publications, and 6 theses focusing on local-scale ionospheric
dynamics" — and it is the strongest candidate. It is rejected because it is a science-results paper,
not a description of the software, and because the project has not designated it. It is already
recorded in Field 27, where a paper that uses the software belongs.

---

### 15. License (RECOMMENDED)
**Value:** Apache License 2.0

**Newly filled — HSSI held no licence value for this entry before this refresh.** That gap was the
single most consequential omission in the record: a user cannot tell whether they may use the
software.

**The licence at the pinned revision is unambiguous.** `LICENSE` is 9,558 bytes of the canonical
Apache License 2.0 text, opening

> Apache License
> Version 2.0, January 2004
> http://www.apache.org/licenses/

and closing with clause 9, "Accepting Warranty or Additional Liability". `codemeta.json` declares
`"license": "https://spdx.org/licenses/Apache-2.0"`. GitHub's licence endpoint reports
`spdx_id: Apache-2.0`, `name: Apache License 2.0`, `path: LICENSE`. The live `License` vocabulary row
named exactly `Apache License 2.0` carries `url` `https://spdx.org/licenses/Apache-2.0` — the same
URI `codemeta.json` uses.

**Read by content, the licence changed once, and a future refresh should know that.** Following the
licence text through history rather than following the filename (the file was renamed
`LICENSE`→`LICENSE.txt`→`LICENSE` along the way, which a filename-based reading would mistake for
churn):

| Commit | Date | Path | Bytes | Text it actually contains |
|---|---|---|---|---|
| `c136f342` "Initial commit" | 2018-08-31 | `LICENSE` | 34,520 | **GNU Affero General Public License v3** |
| `47aed9cf` | 2019-07-16 | `LICENSE.txt` | 34,520 | unchanged AGPL-3.0 (rename only) |
| `49201ba9` "doi badge" | 2020-02-06 | `LICENSE.txt` | 10,762 | **Apache License 2.0**, with a "Copyright 2020 Matthew Zettergren" header |
| `6173a021` | 2021-05-25 | `LICENSE` | 10,081 | Apache-2.0 (rename back, header trimmed) |
| `d34cf69c` "format" | 2021-05-25 | `LICENSE` | 9,558 | Apache-2.0, canonical text |
| `aa50fa1a` (pin) | 2026-09-11 | `LICENSE` | 9,558 | identical to `d34cf69c` |

So the project relicensed from AGPL-3.0 to Apache-2.0 on 2020-02-06 and has not changed since. Any
version of the software before that date — including the earliest Zenodo deposits under the concept
DOI — was AGPL-3.0. Field 15 describes the software's current licence terms, so Apache-2.0 is the
value; the history is recorded so nobody is surprised by an old tarball.

**The near-match rows, ruled out by name.** Every other row in the `License` vocabulary was weighed
against the repository's licence text and rejected, for these reasons:

- `Creative Commons Attribution 4.0 International` — **this is the trap.** Both live Zenodo records
  (`10.5281/zenodo.3647579` and `10.5281/zenodo.10475267`) declare `cc-by-4.0`, and DataCite echoes
  "Creative Commons Attribution 4.0 International". That is the licence Zenodo applies to the
  *deposit* — the archived snapshot and its metadata — chosen in the Zenodo web form. It is not the
  licence on the code, which is what Field 15 is about and what `LICENSE` and `codemeta.json` state.
  A DOI-autofill path would import CC-BY-4.0 here; it must not. (For completeness: the superseded
  record `10.5281/zenodo.3813224` declares Zenodo licence id `other-open`, i.e. a third answer again,
  which is itself a sign of how little the deposit licence tracks the code.)
- `GNU General Public License v3.0 or later`, `GNU General Public Licenses (GPL version 2)`,
  `GNU Lesser General Public License v3.0 only`,
  `GNU Library or ‘Lesser’ General Public Licenses (LGPL version 2)` — the historical licence was
  AGPL-3.0, which is a *different* licence from any of these four and has no row in the vocabulary
  at all. None is the current licence either.
- `MIT License`, `BSD 2-Clause "Simplified" License`, `BSD 3-Clause "New" or "Revised" License` —
  different licences; no evidence for any of them at any revision.
- `Other`, `Restricted` — a catch-all is only defensible when no exact row exists. An exact row does.

**Note for the submitter/updater.** `Software.license` is a foreign key to a shared `License` row
that carries the URL; there is no per-software licence URI to set, so `https://spdx.org/licenses/
Apache-2.0` is a property of the row, not a value for this entry.

---
## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- aurora
- electrodynamics
- electron precipitation
- field-aligned currents
- fluid dynamics
- geospace
- gravity waves
- ionosphere
- ionosphere_thermosphere_mesosphere
- ionospheric fluid electrodynamics
- plasma instabilities
- plasma physics
- space physics
- space weather
- thermosphere
- total electron content

All sixteen are written in the lower-case form the `Keyword` rows actually store. The catalogue's
read API title-cases keywords for display (`Aurora`, `Fluid Dynamics`,
`Ionosphere_Thermosphere_Mesosphere`), so a rendered value must never be copied back as a stored
value. Keyword is the form's one genuinely open vocabulary — a missing keyword is created rather
than rejected — which makes reusing an existing row, not minting a near-duplicate, the discipline
that matters here. Each of the six added values below was checked against the live vocabulary and
exists there verbatim.

**Ten kept.** `aurora`, `electrodynamics`, `fluid dynamics`, `geospace`, `ionosphere`,
`ionosphere_thermosphere_mesosphere`, `ionospheric fluid electrodynamics`, `plasma physics`,
`space physics`, `space weather`. Provenance and standing:

- `aurora` and `ionosphere` are the repository's own GitHub topics
  (`"topics": ["aurora", "ionosphere"]`) and `codemeta.json`'s `"keywords": ["ionosphere",
  "aurora"]` — the only keywords the project itself declares.
- `ionosphere_thermosphere_mesosphere` is inherited verbatim from the PyHC registry entry quoted in
  Field 7. It is a PyHC taxonomy token rather than a phrase a person would type, and the "mesosphere"
  third of it overstates the model's domain (see Field 5). It is kept because it is the token PyHC
  users search with and because it costs nothing; the plain `thermosphere` row added below is the
  value that actually makes the domain findable. (The registry's other keyword for this entry,
  `specific`, is a PyHC general/specific classifier, not a science keyword, and is rightly absent.)
- `ionospheric fluid electrodynamics`, `fluid dynamics`, `electrodynamics`, `plasma physics`,
  `space physics`, `geospace`, `space weather` are restatements of `Readme.md` line 9's
  "three-dimensional ionospheric fluid-electrodynamic model" at varying levels of generality. They
  are kept: a searcher arriving from any of those terms should find a model that is literally
  described by them.
**One stored keyword removed.** `magnetosphere` — HSSI carried this keyword before this refresh and
it is removed at this refresh. Its recorded justification was that the magnetosphere enters GEMINI
as a top-boundary potential/FAC condition and a lumped capacitance, and that the value was kept "on
the same reasoning that keeps the region value". That reasoning was not accepted for the region (see
`Earth Magnetosphere` under Field 5), and the keyword had no independent support to fall back on:
it came from a prior curator's domain reading, not from any upstream source. The repository declares
only two keywords of its own — `aurora` and `ionosphere`, in its GitHub topics and `codemeta.json` —
and PyHC's keyword list for this entry is `["ionosphere_thermosphere_mesosphere","specific"]`.
Neither names the magnetosphere. A future refresh that wants to re-add it needs a ground the region
argument did not supply.

**Six added, each evidenced at this revision.**

- **`thermosphere`** — the model's vertical domain and the neutral half of "Ion-Neutral
  Interactions": MSIS densities and temperature (`src/neutral/atmos.f90`), HWM14 winds
  (`src/neutral/wind.f90`), domain ~80-1000 km (Field 5). Without it the entry is unfindable from
  the single most natural one-word query for its region.
- **`field-aligned currents`** — a first-class capability, not an incidental one.
  `docs/Readme_input.md` documents the `&Jpar` namelist group with `flagJpar` ("estimate parallel
  currents or not?"), and `"flagdirich"` selecting whether the top-boundary arrays are potential or
  FAC; `docs/Readme_magcalc.md` explains that `magcalc.bin` wants `flagJpar=.true.` because
  "Parallel Currents are (likely) Required".
- **`electron precipitation`** — `src/inputdata/precipdataobj.f90` and
  `src/ionization/boundary_conditions/precipBCs_mod.f90` implement file-driven precipitation input;
  the `&precip` namelist group carries `flagprecfile`, `dtprec` and `prec_dir`; and the impact
  ionization is computed by the Fang 2008/2010 electron parameterizations
  (`src/ionization/fang.f90`) or by GLOW.
- **`total electron content`** — `docs/Readme_output.md` line 144 is the section heading
  "## Computing total electron content (TEC)", and line 146 describes the calculation. Chosen over
  the bare acronym because the row exists in the long form.
- **`plasma instabilities`** — `Readme.md` line 13 names "effects of ionospheric fluid instabilities
  on radio propagation" as one of the model's three headline use cases.
- **`gravity waves`** — the model's other headline use case, `Readme.md` line 12, "natural hazard
  effects on the space environment", is realised through acoustic-gravity-wave neutral perturbation
  input: the twelve `src/inputdata/neutraldata*obj*.f90` classes exist to ingest an external neutral
  model's wave field, and `docs/Readme_input.md` documents `interptype` for 2-D Cartesian,
  2-D axisymmetric and 3-D geomagnetic/geographic neutral inputs with a source epicentre
  (`sourcemlat`, `sourcemlon`).

**Considered and not added.** Each of these exists as a live row, so the reason is relevance, not
availability:

- `neutral winds` — genuinely evidenced (HWM14, `src/neutral/wind.f90`), but it describes an input
  GEMINI consumes rather than a subject it addresses; `thermosphere` already carries the neutral
  domain.
- `particle precipitation` — a near-synonym of the `electron precipitation` row that was added.
  Adding both would be the near-duplication this field is supposed to avoid; GEMINI's precipitation
  is specifically electron precipitation, so the narrower row is the right one.
- `magnetosphere-ionosphere coupling` — considered while `magnetosphere` was still stored, as a more
  precise replacement for it. Rejected on its own merits and still rejected now that `magnetosphere`
  is gone: the repository never uses the phrase, and adding it would assert a framing the source
  does not.
- `ionosphere modeling`, `physics-based model`, `empirical model`, `simulation`, `modeling` — all
  true and all so generic that they would return this entry alongside most of the catalogue.
- `fortran`, `plasma` — `fortran` duplicates Field 13, and `plasma` is subsumed by the kept
  `plasma physics`.
- `airglow` — GLOW is an "airglow / aurora model" in its own option text, and `src/io/aurora.f90`
  writes emission output, but the aurora side is what GEMINI actually uses it for; `aurora` is
  already present.

---

### 17. Data Sources (OPTIONAL)
**Value:** Other

**Unchanged.** The field asks which data *input sources* the software supports, from a list of
archives and access protocols. GEMINI supports none of them: it reads HDF5 files that the user has
already prepared (`indat_size`, `indat_grid`, `indat_file` in `&files`), plus directories of
precipitation, electric-field and solar-flux inputs the user generates with PyGemini or mat_gemini.
`Readme.md` line 189 is explicit that input preparation happens outside this program: "Generally
speaking there are python and MATLAB scripts available in the mat_gemini and pygemini repositories
that will save data in the appropriate format once generated". `Other` is the
list's prescribed answer when no listed source applies.

**Considered and rejected, row by row.**

- `HTTP/HTTPS Directories` and `FTP/FTPS Directories` — the build and tests do fetch over HTTPS (see
  the URL sweep under Field 4), but what they fetch is dependency source tarballs and CTest
  reference fixtures, not science data. A user filtering on this row wants a tool that retrieves
  data for them; GEMINI does not.
- `Observatory/Mission-specific` — this row pairs with Fields 31/32, which are empty for the reasons
  set out there. Selecting it would assert an observatory association the software does not have.
- `CDAWeb`, `HAPI`, `Madrigal`, `SSCWeb`, `OMNIWeb`, `AMDA`, `das2`, `GFZ`, `VirES`, `WDC`, `TAP`,
  `The Virtual Solar Observatory.`, `S3/Cloud-aware` — no client, URL, or documentation for any of
  these exists at this revision. The empirical inputs GEMINI *does* use (MSIS, HWM14, GLOW) are
  compiled-in model codes fetched as source at build time, not data services.

---

### 18. Input File Formats (RECOMMENDED)
**Values:**
- ascii
- HDF5
- Other

**Unchanged; all three still hold at this revision.**

- **HDF5** — the primary scientific input format. `&files` in `docs/Readme_input.md` points at
  `simsize.h5`, `simgrid.h5` and `initial_conditions.h5`; `src/io/reader_hdf5.f90`,
  `src/numerical/grid/readgrid_hdf5.f90` and `src/io/plasma_input_hdf5.f90` are the readers.
  `config_nml.f90` derives the format from the input file's suffix when `file_format` is not set.
- **ascii** — the simulation configuration is text. `docs/Readme_input.md`: "Gemini uses Fortran 95
  standard NAMELIST files for the input configuration files." (`docs/Readme_input.md` line 14),
  read by `src/io/config_nml.f90`; the
  older `.ini` form is still readable via `src/io/config_ini.f90`.
- **Other** — the raw binary field-point file for `magcalc`. `docs/Readme_magcalc.md` documents
  `magfieldpoints.{h5,dat}` and the `.dat` layout (`integer(4) :: lpoints`, then
  `real(8), dimension(lpoints) :: r,theta,phi`), and `src/utils/magcalc.f90` still implements it —
  `case ('.dat')` at line 175, opening the file `form='unformatted',access='stream'`. **It is
  deprecated but not removed**, and the code says so itself at line 176:
  `print '(a)', "WARNING: Magcalc .dat input format is long-deprecated and may not work."` If a
  future revision deletes that branch, `Other` should go with it.

**Considered and rejected: `netCDF3/4`.** GEMINI *used* to read and write netCDF — the v1.6.1 release
note says the point release was made "_before_ removing raw and netcdf file i/o", and
`src/io/reader.f90` still carries the fossil comment `interface !< reader_{raw,hdf5,nc4}.f90`. At
this revision the capability is gone: a case-insensitive whole-tree search for `netcdf`,
`nc4fortran` or `.nc` matches 0 files, against 59 files for `hdf5` under the same query shape. Do
not re-add it from the old release notes. (The *pygemini* repository does still ship a
NetCDF4→HDF5 converter; that belongs to its record, not this one.)

**Considered and rejected: `csv`, `JSON`, `CDF`, `FITS`, `IDL.sav`, `ISTP-Compliant`, `Zarr`.** Four
`.json` files exist at this revision and none is scientific input: `cmake/libraries.json` and
`test/test_urls.json` are build/test configuration the tooling reads, `CMakePresets.json` is CMake
configuration, and `codemeta.json` is this repository's own metadata record. For the other six
formats, no reader exists anywhere in the tree.

---

### 19. Output File Formats (RECOMMENDED)
**Values:**
- HDF5

**Unchanged.** `docs/Readme_output.md` line 3 states it flatly: "The file format for Gemini is
HDF5." The writers are `src/io/plasma_output_hdf5.f90`, `src/io/aurora_hdf5.f90`,
`src/io/cond_hdf5.f90` and `src/io/mag_hdf5.f90`; `src/io/debug_dump.f90` dumps via `h5fortran`'s
`h5write`; and `magcalc` writes HDF5 too ("`magcalc` uses hdf5 output files containing the following
variables: `real(wp), dimension(lpoints) :: Br, Btheta, Bphi.`").

**Considered and rejected: `ascii`.** `src/io/logging.f90` opens a text file
(`form='formatted'`, default name `debug.log`) and appends values line by line. That is a debug log,
not a data product, and listing `ascii` here would tell a user they can get their simulation results
as text, which they cannot. The three `flagoutput` modes described in `docs/Readme_output.md` — full
state, averaged parameters, density only — are all HDF5.

**Considered and rejected: `Other` for plot images.** `gemini3d.plot.plot_all(direc,
saveplot_fmt="png")` writes PNG or EPS, but that is the Python front end rendering figures, not this
program writing a data format.

---
### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

**Unchanged, and stated outright by the source.** `Readme.md` lines 36-37: "Gemini is intended to be
OS / CPU arch / platform / compiler agnostic. / Operating system support includes: Linux, MacOS, and
Windows." All three are exercised in CI at this revision: `.github/workflows/ci.yml` runs on
`ubuntu-latest` and `ubuntu-24.04`, `ci_macos.yml` on `macos-latest`, `ci_windows.yml` on
`windows-latest`, and `oneapi-linux.yml` on `ubuntu-latest`. `docs/` carries per-platform build
guides for each: `Linux_gcc.md`, `Linux_intel_oneapi.md`, `MacOS_gcc.md`, `Windows_gcc.md`,
`Windows_intel_oneapi.md`.

**Considered and rejected: `Operating System Independent`.** The README's word "agnostic" invites it,
but this is compiled Fortran/C/C++ with platform-specific build documentation and a
Windows-specific known issue (`Readme.md`: "Occasionally on Windows you may get a system error code
`0xc0000005`"). The row is for software that genuinely does not care — interpreted code, typically.
Naming the three supported platforms is both more accurate and more useful to someone filtering.

**Considered and rejected: `Solaris`, `MobilePlatform`, `Other`.** No evidence at this revision.

---

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- Apple Silicon arm64
- HPC or HEC
- Linux aarch64 or arm64
- ppc64le
- x86-64

**Unchanged.** These five are the vocabulary's rendering of one sentence, `Readme.md` line 38: "CPU
arch support includes: Intel, AMD, ARM, IBM POWER, Cray and more." Mapping each clause:

- "Intel, AMD" → **x86-64**.
- "ARM" → both ARM rows. The distinction the vocabulary draws is macOS-on-ARM versus Linux-on-ARM,
  and the repository evidences both: `ci_macos.yml` runs on `macos-latest` (**Apple Silicon
  arm64**), and `cmake/cpu_count.cmake` line 3 handles **Linux aarch64 or arm64** explicitly —
  "on ARM e.g. Raspberry Pi, the usually reliable cmake_host_system_info gives 1 instead of true
  count" — matching `Readme.md` line 39, "GEMINI can run on hardware ranging from a Raspberry Pi to
  laptop to a high-performance computing (HPC) cluster."
- "IBM POWER" → **ppc64le**, the only POWER row available.
- "Cray" plus the HPC framing → **HPC or HEC**. Backed by `cmake/cray.cmake` ("toolchain for Intel
  oneAPI and/or GCC compilers on Cray system"), `Readme.md` line 59 ("Cray with GCC or Intel oneAPI
  backend"), the three cluster guides `docs/Readme_VEGA.md`, `docs/Readme_pleiades.md` and
  `docs/Readme_Dardel.md`, and the offline-batch CTest presets.

**Considered and rejected: `GPU`.** There is no GPU offload at this revision. Searching the whole
tree case-insensitively for `cuda`, `openacc`, `\bhip\b`, `sycl`, `target teams` and `gpu` returns
zero files for each; a sixth pattern, `rocm`, appears to match one file but the hit is the substring
inside `ProcMask` in `src/utils/cpu_count.cpp`, not a ROCm reference. Control under the same query
shape: `mpi` matches 146 files. Parallelism here is MPI domain decomposition only.

**Considered and rejected: `CPU Independent`.** Same reasoning as `Operating System Independent`
above — this is compiled code with architecture-specific build handling.

**Considered and rejected: `Sun (SPARC)`, `Other`.** No evidence at this revision.

---

### 22. Related Phenomena (OPTIONAL)
**Value:** None — deliberately empty

**This is an examined empty, not a blank.** The field is a **closed** vocabulary of exactly seven
rows: `Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`,
`Solar Flares`, `Solar Wind`, `X-ray emission`. Every one of the seven is a solar or heliospheric
phenomenon. GEMINI is a terrestrial ionospheric model. The vocabulary simply has no row for what
this software is about.

**Measured, not assumed.** Sweeping the whole pinned tree case-insensitively for each row's term and
for its obvious synonyms:

| Pattern | Files matched at `aa50fa1a` |
|---|---|
| `coronal heating` | 0 |
| `coronal mass ejection` | 0 |
| `CME` | 0 |
| `solar corona`, `corona` | 0 |
| `geomagnetic storm` | 0 |
| `storm`, `substorm` | 0 |
| `solar wind` | 0 |
| `X-ray`, `xray` | 0 |
| `solar flare` | 0 |
| `flare` | 1 |

Control under the identical query shape and scope: `aurora` matches 23 files, so the instrument can
see a positive.

Two of those results need explaining rather than just reporting:

- **The single `flare` hit does not support `Solar Flares`.** It is a source comment in
  `src/libgemini.f90` line 151, where the `solflux` pointer declaration carries the trailing comment
  `! perturbations to solar flux, e.g., from a flare or eclipse`. GEMINI does not model, detect or
  analyse flares; it accepts a user-supplied solar-flux time series that *could* represent one. That
  is a "configurable for" mention, which the relevance bar excludes, and the same sentence offers
  "eclipse" as an equally valid interpretation of the same input.
- **`geomagnetic` matches 53 lines across 26 files, and reading all 53 finds no storm among them.**
  They are of two kinds only: geomagnetic *coordinates* (the `src/numerical/coord/geomagnetic.f90`
  module and its build target, "INTERPOLATION BASED ON GEOMAGNETIC COORDINATES", the `Bincl`
  namelist key commented `! geomagnetic inclination`, `interptype` option "3 - 3D Cartesian
  geomagnetic"), and geomagnetic *activity indices* (`src/ionization/glow_run.in.f90` line 41,
  `! ap      Ap index of geomagnetic activity`, and the `activ` triple). An activity index is a
  driver the user supplies, not a phenomenon the software addresses. The zero result for
  `geomagnetic storm` is what settles it.

**Why the five values a prior extraction proposed could not be used.** An earlier extraction
proposed `Auroral emissions`, `Ionospheric disturbances`, `Ionospheric instabilities`, `Natural
hazard effects on the space environment` and `Space weather events`. All five are accurate
descriptions of GEMINI and all five are free text: **none of them is one of the seven rows**, and
the API path for this field rejects anything not in the vocabulary rather than creating it. That is
why none reached the catalogue. The right destination for phenomena with no row is Field 16, the
open vocabulary — and that is where the substance of three of them now lives, as the added keywords
`plasma instabilities`, `gravity waves` and `electron precipitation`, alongside the existing
`aurora` and `space weather`.

**Conclusion for a future refresh:** do not re-propose free text here, and do not stretch one of the
seven solar rows to cover an ionospheric model. If the vocabulary ever gains an ionospheric or
auroral row, this entry is a strong candidate for it.

---

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Newly filled — HSSI held no development status for this entry before this refresh.**

**Chosen from the row definitions, not from impression.** The vocabulary is the eight repostatus.org
states, and each carries its definition. `Active` reads: "The project has reached a stable, usable
state and is being actively developed." Both halves are satisfied:

- *stable, usable state* — 58 tags reachable from the pin, 56 published GitHub releases, the most
  recent `v1.7.0` on 2024-01-09, and a versioned Zenodo deposit series with 57 versions.
- *being actively developed* — commits reachable from the pin, counted by author-date year: 144 in
  2018, 694 in 2019, 932 in 2020, 1,100 in 2021, 583 in 2022, 221 in 2023, 277 in 2024, 160 in 2025,
  174 in 2026 up to the pin. The pinned commit itself is dated 2026-09-11. GitHub reports
  `archived: false`.

`codemeta.json` independently declares `"developmentStatus": "active"`.

**The seven rejected rows, each against its own definition.**

- `Inactive` — "no longer being actively developed". Contradicted by 174 commits in 2026 up to the
  pin, the last of them on the pin date.
- `Unsupported` — "the author(s) have ceased all work on it". Same contradiction.
- `Abandoned`, `Suspended`, `WIP`, `Concept` — all four require that "there has not yet been a
  stable, usable release" (or, for `Concept`, minimal implementation). 56 releases falsify the
  premise for all four before their differentiating clauses even matter.
- `Moved` — "The project has been moved to a new location, and the version at that location should
  be considered authoritative." The opposite is true: `gemini3d/gemini` is the *old* name and 301s
  *to* this repository (see Field 3).

**The one fact that could mislead a future refresh, recorded so it does not.** There has been no
tagged release since 2024-01-09, and 641 commits have accumulated on `main` since. A release-cadence
reading would suggest `Inactive`. It would be wrong: repostatus.org's `Active` turns on *development*
activity, not release frequency, and `Readme.md` line 23 states the project's own model — "Generally,
the Git `main` branch has the current development version and is the best place to start, while more
thoroughly-tested releases happen regularly."

Also note that GitHub's `updated_at` field is not a commit-activity signal (it moves for stars,
description edits and similar); the year-by-year commit counts above are, and they are what this
value rests on.

---
### 24. Documentation (RECOMMENDED)
**Value:** https://gemini3d.github.io/gemini3d/

**Unchanged — and it is important that it *stayed* unchanged, because the repository's own
documentation links at this revision are broken and a naive refresh would "correct" this field into
a 404.**

The stored URL is the canonical GitHub Pages site for the repository — it is the `homepage` GitHub
records for `gemini3d/gemini3d`, and the repository publishes Pages. The site serves the
FORD-generated subroutine-level reference described in `docs/Readme_docs.md`, and it served that
documentation when it was checked for this dossier.

**The repository's own documentation links point somewhere else, and that somewhere did not
resolve.** At this revision `Readme.md` links the generated documentation as
`[rendered as webpages](https://gemini3d.github.io/GEMINI/)`, `docs/Readme_docs.md` links "the
[GEMINI docs website](https://gemini3d.github.io/gemini/index.html)", and `ford.md` declares
`project_website: https://gemini3d.github.io/gemini`. None of those three paths served the
documentation when they were checked for this dossier. They are stale links left behind by the
`gemini` → `gemini3d` repository rename: GitHub Pages, unlike the repository API, does not redirect
the old project path, so the rename broke them silently and the repository has not caught up.
**Do not replace the stored value with any of these** — the rule holds regardless of what those
paths happen to serve later, because the stored URL is the one GitHub itself names as the
repository's homepage.

**Neither wiki belongs here, and this is worth recording because `has_wiki` is a misleading signal.**
GitHub reports `has_wiki: false` for `gemini3d/gemini3d` — yet a wiki repository does exist and is
reachable. A repository's wiki is a *separate* git repository at `<repo>.wiki.git`, so `has_wiki`
proves nothing either way and must be probed directly. Probing both:

- `https://github.com/gemini3d/gemini3d.wiki.git` — reachable, with five pages: `Home.md`,
  `compiler-speed-comparison.md`, `tests:-GCC-Linux.md`, `tests:-GCC-MSYS2-Windows.md`,
  `tests:-Intel-compiler.md`. Last edited 2020-03-09.
- `https://github.com/gemini3d/pygemini.wiki.git` — reachable, with two pages: `Home.md` and
  `PyGemini-packaging-approach.md`. Last edited 2020-10-14. (Its repository reports
  `has_wiki: true`, the reverse of the core repository's — a further reason to treat the flag as
  uninformative.)

Control for the probe: the same `git ls-remote` against a deliberately nonexistent
`gemini3d/<nonexistent>.wiki.git` returns "Repository not found", so a reachable result means real
content. Both wikis are dormant developer notes — compiler benchmark tables and a packaging
discussion — not the installation-and-usage documentation this field asks for. Recorded so a future
refresh does not re-discover them and mistake them for a better value.

**Considered and rejected: `https://github.com/gemini3d/gemini3d/tree/main/docs`.** The `docs/`
directory holds the substantive prose — 22 files including `Readme_input.md`, `Readme_output.md`,
`Readme_magcalc.md`, `Readme_cmake.md`, `Readme_compilers.md`, `Readme_mpi.md`, `Readme_prereqs.md`
and the per-platform and per-cluster guides — and it is arguably more useful to a new user than the
FORD API reference. It is rejected only because this field takes a single URL and the Pages site is
the project's own declared homepage; the `docs/` tree is reachable from `Readme.md`'s "List of other
associated Readmes" section in any case. If a future refresh wants to prefer it, the branch-name
fragility of a `tree/main/` URL is the counter-argument.

**A further reason the rejected alternative was unattractive.** Had the entry been repointed at
`gemini3d/pygemini` (Field 7), this field would have had no good value at all: that repository has no
Pages site, and its documentation is its `Readme.md` plus the dormant wiki above.

---

### 25. Funder (OPTIONAL)

**Funder 1:**
- **Organization:** Defense Advanced Research Projects Agency
- **Funder Identifier:** https://ror.org/02caytj08

**Funder 2:**
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

**Funder 3:**
- **Organization:** U.S. National Science Foundation
- **Funder Identifier:** https://ror.org/021nxhr62

**Unchanged. All three names are the ROR record's own `ror_display`, verified against the ROR v2
API** (which returns names as a `names[{value, types}]` array and has no top-level `name` field, so
a lookup that reads `name` gets nothing):

| Identifier | `ror_display` | acronyms | status |
|---|---|---|---|
| `https://ror.org/02caytj08` | Defense Advanced Research Projects Agency | ARPA, DARPA | active |
| `https://ror.org/027ka1x80` | National Aeronautics and Space Administration | NASA, NASA HQ | active |
| `https://ror.org/021nxhr62` | U.S. National Science Foundation | NSF | active |

Note the third: the canonical ROR display name is **"U.S. National Science Foundation"**, with the
"U.S." prefix. A refresh that "expands the acronym" to "National Science Foundation" would diverge
from ROR. The form's instruction to avoid acronyms is satisfied by all three.

**Where the three come from, and how thin the evidence actually is.** The only funder statement in
the repository is `codemeta.json`'s

```json
"funder": {
    "@type": "Organization",
    "name": "NSF, NASA, DARPA"
}
```

— three agencies packed into a single `name` string on one `Organization` object. A prior curator
correctly unpacked it into three funder entries and resolved each to a ROR. That unpacking is kept.

**Corroboration found at this revision for two of the three.**

- **NASA** is independently evidenced twice in `Readme.md`: line 132, "[h5fortran](https://github.com/
  geospace-code/h5fortran) funded in part by NASA [NNH19ZDA001N-HDEE grant 80NSSC20K0176](https://
  hdrl.gsfc.nasa.gov/HDEE19_Abstracts.pdf)", and lines 150-151, "Development of `gemini3d.run` was
  funded by NASA / [NNH19ZDA001N-HDEE grant 80NSSC20K0176]". `docs/Readme_pleiades.md` additionally
  documents running GEMINI on NASA's Pleiades system, which is compute support rather than funding.
- **DARPA** is corroborated by the shipped example batch script `myrun`, whose line 4 is
  `#SBATCH --account=DARPA4763B987` — a DARPA-charged allocation on a Navy DSRC machine (the script
  runs from `/p/work1/inchinp/...`).
- **NSF** has no corroboration anywhere at this revision beyond the packed `codemeta.json` string.
  A whole-tree, case-insensitive, word-boundary search for `NSF` matches exactly that one line and
  nothing else. (The word boundary is load-bearing: an unanchored `nsf` also matches "transfer" and
  "transform" across two dozen files, which is how a careless sweep manufactures corroboration.
  Controls under the same anchored query shape: `NASA` matches 4 files, a nonsense token 0.) It is
  kept
  because `codemeta.json` is the project's own declaration and there is no reason to doubt it — GEMINI
  is a long-running academic model and NSF support is entirely ordinary — but a future refresh should
  know the evidence is a single word in a comma-separated string, not an acknowledgement.

**Considered and rejected: funders named in the publications of Field 27.** Those papers' funding
acknowledgements fund *the science done with* GEMINI, and in several cases fund the observing
campaigns (MICA, RENU2) rather than the software. A citing paper's funder is not the software's
funder, and importing them would silently widen this field with agencies the project never claimed.

---

### 26. Award Title (OPTIONAL)

**Award 1:**
- **Award Title:** NASA Heliophysics Data Environment Enhancements
- **Award Number:** 80NSSC20K0176

**Unchanged, and the stored split is better than the repository's raw string.** `Readme.md` writes
the award twice as the single phrase "NNH19ZDA001N-HDEE grant 80NSSC20K0176", hyperlinked to
`https://hdrl.gsfc.nasa.gov/HDEE19_Abstracts.pdf`. That phrase concatenates three different things:

- `NNH19ZDA001N` — the NASA ROSES-2019 NRA solicitation number,
- `HDEE` — the program element within it, Heliophysics Data Environment Enhancements,
- `80NSSC20K0176` — the grant number itself.

The form wants the award's **full title** in one sub-field and its **identifier** in the other. The
stored values do exactly that: the program element expanded to its full name as the title, and the
grant number alone as the number. An earlier extraction recorded the award *number* as the whole
string "NNH19ZDA001N-HDEE grant 80NSSC20K0176", which is not an identifier a funder could track. The
stored form is kept.

**What this award actually funded, stated precisely.** `Readme.md` attributes it to two specific
things, neither of which is the GEMINI Fortran solver: h5fortran (line 132) and the `gemini3d.run`
frontend (lines 150-151), the latter being part of PyGemini. It is nonetheless the right award for
this entry, which covers the whole stack: the entry's own description frames itself as the
"Gemini3D/GEMINI software stack", and `gemini3d.run` is squarely inside it.

**Considered and not recorded as a second award: `DARPA4763B987`.** It appears in `myrun` line 4 as
`#SBATCH --account=DARPA4763B987`. It is an HPC *allocation account code* on a DoD supercomputing
system, not a grant identifier, and no award title exists for it anywhere at this revision. Recording
an award number with no title would be both unfounded and, in HSSI's data model, unusable. It is
cited under Field 25 as corroboration that DARPA support is real, which is all the evidence supports.

**Considered and rejected: awards from the Field 27 publications.** Same reasoning as Field 25 — a
citing paper's grant is not this software's grant.

**Note on scope.** Award rows are shared across HSSI entries, so any change to the title or number of
`NASA Heliophysics Data Environment Enhancements` would alter every entry that references it. No such
change is proposed; this entry's recorded values are already correct.

---
## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Values:**
- https://doi.org/10.1002/2013GL058018
- https://doi.org/10.1002/2013JA019583
- https://doi.org/10.1002/2014JA020860
- https://doi.org/10.1002/2015GL066806
- https://doi.org/10.1002/2015JA021116
- https://doi.org/10.1002/2015JA021536
- https://doi.org/10.1002/2015JA021790
- https://doi.org/10.1002/2016JA023159
- https://doi.org/10.1002/2016JA023329
- https://doi.org/10.1002/2016RS006182
- https://doi.org/10.1029/2008JA013384
- https://doi.org/10.1029/2010GL045406
- https://doi.org/10.1029/2011JA016649
- https://doi.org/10.1029/2012JA017637
- https://doi.org/10.1029/2018GL081569
- https://doi.org/10.1029/2018GL081886
- https://doi.org/10.1029/2018JA025721
- https://doi.org/10.1029/2019GL082576
- https://doi.org/10.1029/2019JA027200
- https://doi.org/10.1029/2019JA027734

**Nineteen kept, one added.** Sweeping the whole pinned tree for DOI-shaped strings
(`10.\d{4,9}/[-._;()/:A-Za-z0-9]+`) returns matches in exactly seven files: `CITATION.cff` and
`codemeta.json` (the Zenodo DOIs handled in Field 2, plus codemeta's own schema DOI),
`docs/Readme_references.md`, and four source and test files —
`src/collisions/collisions.f90`, `src/ionization/fang.f90`, `src/sources/sources.f90` and
`test/ionization/test_fang.f90`. Every publication DOI found in those seven is accounted for below,
and each of the twenty values corresponds to one of them.

**Sixteen from `docs/Readme_references.md`**, the project's own "Publications Using GEMINI" list. Its
opening line sets the field's scope precisely: "Since its first appearance in 2012, GEMINI has been
used in over 15 publications, and 6 theses focusing on local-scale ionospheric dynamics." These are
papers that *use* the software, which is exactly what Field 27 is for.

**Four from source-code comments**, which is why they are not in the references file and why a
references-file-only sweep would have missed them:

- `https://doi.org/10.1029/2008JA013384` — cited in `src/ionization/fang.f90` and again in
  `test/ionization/test_fang.f90`. This is Fang et al. (2008), the electron impact-ionization
  parameterization the module implements.
- `https://doi.org/10.1029/2010GL045406` — cited in `src/ionization/fang.f90`. Fang et al. (2010),
  the successor parameterization; `src/ionization/fang_run.f90` exposes both as
  `ionization_fang2008` and `ionization_fang2010`.
- `https://doi.org/10.1029/2011JA016649` — cited in both `src/collisions/collisions.f90` and
  `src/sources/sources.f90`, the collision-frequency and source-term modules.
- `https://doi.org/10.1029/2012JA017637` — Zettergren & Semeter (2012), which is also the first
  entry in `docs/Readme_references.md`. See Field 14 for why it is here rather than as the reference
  publication.

**Added at this refresh: `https://doi.org/10.1002/2016JA023329`.** Burleigh & Zettergren (2017),
"Anisotropic fluid modeling of ionospheric upflow: Effects of low-altitude anisotropy and
thermospheric winds", *Journal of Geophysical Research: Space Physics* — confirmed at Crossref. It
is listed in `docs/Readme_references.md` alongside the other fifteen journal articles but was the
one paper from that file missing from the record. It was almost certainly missed because its link in
the references file is not a plain DOI URL: it is
`https://agupubs.onlinelibrary.wiley.com/doi/pdf/10.1002/2016JA023329%4010.1002/%28ISSN%292169-9402.IMC15`,
where the `%40` is an encoded `@` introducing a Wiley virtual-issue suffix. The DOI is the part
before the `@`. **A future sweep must strip that suffix rather than treat the whole string as the
identifier.**

**Deliberately omitted: the six theses.** `docs/Readme_references.md` lists MS and PhD theses by Lee
(2013), Burleigh (2013, 2018), Fernandes (2015), Clayton (2019) and Gutow (2020), from Embry-Riddle
Aeronautical University and Dartmouth College. None has a DOI, and their links are ProQuest
`openview` URLs, a `commons.erau.edu` CGI `viewcontent.cgi?article=…` URL, and — for Gutow — no link
at all. Field 27 accepts only a URL per entry and prefers a DOI; a ProQuest session-style URL is not
a permanent link, and the one durable-looking candidate (`https://commons.erau.edu/edt/408/`, for
Burleigh 2018) would leave the other five unrepresented. Recording a partial, format-inconsistent
subset would be worse than the documented omission. If a future refresh wants them, ADS abstract
pages are the route the form suggests.

**Deliberately omitted: the papers that cite GEMINI but which the project does not list.** An ADS
full-text search for `gemini3d`, excluding the Zenodo deposit records themselves
(`full:"gemini3d" -bibstem:zndo`), returns 28 records — mostly AGU meeting abstracts and recent JGR
papers not in the references file. Field 27 is for publications "the
software developer prioritizes"; the references file *is* that prioritisation, and widening the field
to the whole citation graph would replace the developers' selection with an automated one.

---

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Researched, not assumed.** The DOI sweep described under Field 27 found no dataset DOI anywhere at
this revision — every `10.x/...` match is either a Zenodo software DOI or a journal article. The
whole-tree URL sweep described under Field 4 found exactly one data-bearing URL:
`test/test_urls.json`, whose entire content is

```json
{
"ref_data": {
  "url": "https://www.dropbox.com/s/ratmyk4f8lb1u6t/ref_data.json?dl=1"
}
}
```

That is a Dropbox-hosted archive of CTest reference outputs — regression fixtures for
`test/compare/`, downloaded by `test/download.cmake`. It is neither a scientific dataset nor a
persistent identifier, and a Dropbox share link is the opposite of what this field asks for.

**Considered and rejected: the empirical model data GEMINI consumes.** MSIS, HWM14 and GLOW ship
coefficient and parameter files (e.g. `msis21.parm`, referenced from `CMakeLists.txt`), but those
arrive as *source* through CMake `FetchContent` from the repositories recorded in Field 29. They are
model coefficients compiled into the executable, not datasets the software supports analysis of.

---

### 29. Related Software (OPTIONAL)
**Values:**
- https://github.com/gemini3d/GEMINI-docs
- https://github.com/gemini3d/GEMINI-examples
- https://github.com/gemini3d/glow
- https://github.com/gemini3d/hwm14
- https://github.com/gemini3d/mat_gemini
- https://github.com/gemini3d/msis

**Changed: six of the eight stored values are kept and two are removed.** The governing test is the
form's: an entry belongs here if it is *distinguishing* — a similar-purpose tool, a predecessor, a
companion, or a **domain-specific** dependency whose presence characterises this software — and the
rule extends Field 30's generic-infrastructure exclusion into this field, so infrastructure is
excluded here on the same terms. Each of the eight is given its own verdict below rather than
inherited.

| Stored value | Verdict | Reason |
|---|---|---|
| `https://github.com/gemini3d/GEMINI-docs` | **keep** | The mathematical formulation of the model. `Readme.md` lines 15-17: "The detailed mathematical formulation of GEMINI is included in [GEMINI-docs]". A reader who wants to know what equations this code solves goes here and nowhere else. |
| `https://github.com/gemini3d/GEMINI-examples` | **keep** | The project's own example simulations. `docs/Readme_input.md`: "A large number of examples (in addition to those included in the main repo) are included in the [GEMINI-examples] repository." A companion, and the practical entry point for a new user. |
| `https://github.com/gemini3d/glow` | **keep** | NCAR GLOW, the airglow/aurora model, built in **by default** (`options.cmake` line 25) and fetched from this exact URL by `cmake/libraries.json`. A heliophysics model, not infrastructure. |
| `https://github.com/gemini3d/hwm14` | **keep** | HWM14 horizontal neutral wind model, same fetch mechanism, same reasoning. |
| `https://github.com/gemini3d/msis` | **keep** | MSIS neutral atmosphere (MSIS00 / MSIS 2.1, selected by `msis_version` in `&neutral_BG`), same fetch mechanism, same reasoning. |
| `https://github.com/gemini3d/mat_gemini` | **keep** | The MATLAB front/back end. `Readme.md` lines 194-195 and `docs/Readme_output.md` throughout. Also in Field 30, correctly — it is both a companion package and a demonstrated exchange partner. |
| `https://github.com/geospace-code/h5fortran` | **remove** | HSSI carried this value before this refresh; it is removed at this refresh. h5fortran is an HDF5 wrapper — I/O plumbing, the category the generic-infrastructure exclusion names, and that exclusion applies to this field as well as to Field 30. It was previously kept on the ground that `Readme.md` line 132 singles it out by name under "For file input/output we also use" and attaches the NASA HDEE funding attribution to it; that is a true observation about the README but it is not one of the rule's stated grounds for inclusion, and being named in a dependency list does not make a library distinguishing. Its funding role survives intact in Field 26, and HDF5 itself is already visible to a reader through Fields 18 and 19. |
| `https://mumps-solver.org/` | **remove** | HSSI carried this value before this refresh; it is removed at this refresh. MUMPS is a general sparse direct solver, not heliophysics, and it fails the same generic-infrastructure test. The ground it was previously kept on — that it is unusually user-visible, because `Readme.md`'s "Known limitations and issues of GEMINI" devotes item 3 to MUMPS underestimating the memory a solve needs and tells the user to add `mumps_par%ICNTL(14)=50` to the potential solver — is a real and still-useful fact about running GEMINI, but user-visibility is not among the rule's grounds for listing software here. The limitation itself is not lost: it is recorded in this row, and it remains in `Readme.md` for anyone who builds the code. |

**Two URL findings recorded so a future refresh does not "fix" them wrongly.** The first concerns
a value removed above; it is kept because the discrepancy outlives the value.

- **If h5fortran is ever reconsidered, `geospace-code/h5fortran` is the URL — not the fork the build
  actually fetches.** The value is removed above, but the URL finding is recorded because anyone
  revisiting it will hit the discrepancy. `cmake/libraries.json` at this revision fetches h5fortran
  from `https://github.com/ECLAIRWaveS/h5fortran/archive/...`, not from `geospace-code`. Checked at
  GitHub: `ECLAIRWaveS/h5fortran` is a fork (`fork: true`, parent `geospace-code/h5fortran`) created
  2023-10-29 with 0 stars; `geospace-code/h5fortran` is the upstream project, created 2018-04-09, and
  is the URL `Readme.md` line 132 gives. Both resolved independently when they were checked for this
  dossier, neither redirecting to the other — the fork is a pinned build source, not the project. (`cmake/libraries.json` likewise fetches `ffilesystem`
  from `ECLAIRWaveS`; ffilesystem is listed in neither field — see the exclusions below.)
- **`GEMINI-docs` and `GEMINI-examples` resolve, though GitHub's canonical names are now lower-case**
  (`gemini3d/gemini-docs`, `gemini3d/gemini-examples`). GitHub repository paths are
  case-insensitive, both stored URLs work, and `Readme.md` itself uses the mixed-case forms. No
  change; noted so the lower-case canonical form is not mistaken for a broken stored value.

**Considered and not added.**

- **`https://github.com/gemini3d/mat_gemini-scripts`** — the repository `Readme.md` lines 197-201
  points at "[Gemini-scripts](https://github.com/gemini3d/GEMINI-scripts)" for "scripts used for
  various published and ongoing analyses", and `docs/Readme_input.md` points at
  `https://github.com/gemini3d/gemini-scripts/tree/master/magic/` for neutral-input preparation
  examples. Both of those URLs now 301 to `gemini3d/mat_gemini-scripts`. It is a genuine companion
  and a reasonable addition; it is not added because it is an auxiliary MATLAB script collection
  whose parent `mat_gemini` is already listed, and adding it would push the field toward
  enumerating the whole GitHub organisation. Recorded as a live candidate a future refresh may take.
- **`https://github.com/gemini3d/gemci`** — "Long-running CI cases", cited by `docs/Readme_magcalc.md`
  and `docs/Readme_input.md` as the source of example configurations. Not added: a CI-fixture
  repository tells a prospective user nothing about what the software does.
- **`https://github.com/ECLAIRWaveS/ffilesystem`** — a Fortran filesystem-path library fetched by
  `CMakeLists.txt`. This is generic infrastructure by the form's own test: path manipulation would be
  equally at home in a web app, a finance model or a biology pipeline. Excluded from both fields.
- **HDF5, LAPACK, ScaLAPACK and MPI** — see Field 30, from which they are removed. They are not
  relocated here: Field 29 applies the same exclusion to the generic stack, and the usual correct
  destination for a rejected Field 30 entry is neither field.
- **`https://github.com/space-physics/NCAR-GLOW`, `https://github.com/space-physics/msise00`,
  `https://github.com/space-physics/hwm93`** — these are HSSI entries in their own right (GLOW,
  MSISE-00, HWM-93), so cross-linking to them is tempting. They are *different software* from what
  GEMINI builds: they are Python wrappers around those models, whereas GEMINI fetches and compiles
  the `gemini3d/*` Fortran adaptations. HWM-93 is also a different model generation from the HWM14
  GEMINI uses. The stored `gemini3d/*` URLs name what the build actually consumes, which is what a
  reader needs.

---

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://github.com/amisr/amisrsynthdata
- https://github.com/gemini3d/mat_gemini
- https://github.com/gemini3d/pygemini

**Changed: one value added and six removed.** This is the largest change in this refresh, so the
reasoning is set out per value. The form's bar for this field is a *demonstrated exchange* between
peer tools — shared or converted data models, one's output imported into the other, an adapter API,
a plugin relationship, a companion package, or a cross-language bridge — and it states outright that
**being a dependency is not interoperability**.

**Kept, with the evidence.**

| Value | Why it passes |
|---|---|
| `https://github.com/gemini3d/pygemini` | The strongest entry in the field, and demonstrated in executable form. This repository's CMake probes for it as an external package (`cmake/python.cmake`'s `check_pygemini()` runs `import gemini3d`), its build summary lists it as an optional feature, its CTest cases are `DISABLED` without `PYGEMINI_DIR`, and `test/compare/compare.f90` shells out to `python -m gemini3d.compare … -plot`. `Readme.md` line 149 documents running the model through it. The full sweep is under Field 7. |
| `https://github.com/gemini3d/mat_gemini` | The same relationship in MATLAB. `test/compare/compare.f90`'s `elseif(P%matlab)` branch invokes `gemini3d.plot.plotdiff(...)` by `execute_command_line`, symmetric with the PyGemini branch; `docs/Readme_output.md` documents `gemini3d.loadframe` / `gemini3d.read.grid` for reading GEMINI's HDF5 output into MATLAB; `docs/Readme_magcalc.md` notes magcalc output "can be read using the mat_gemini interfact `gemini3d.read.magdata`". A cross-language bridge to a named tool, which the form lists explicitly. |

**Added: `https://github.com/amisr/amisrsynthdata`.** An HSSI entry in its own right, and the
exchange is concrete and one function deep: `src/amisrsynthdata/state_functions/gemini_utils.py`
imports `from gemini3d.grid.gridmodeldata import model2pointsgeogcoords` and `import gemini3d.read
as read`, and `state_functions/density.py` defines a `gemini()` state function documented as
"Electron density output from GEMINI model." with a `gemini_output_dir` parameter. Its
`docs/source/installation.rst` states that "Utilizing output from the GEMINI non-linear ionospheric
dynamics model to specify the ionospheric state requires `pygemini` … to be installed." So
amisrsynthdata reads GEMINI simulation output and turns it into synthetic AMISR data — GEMINI's
output imported into another tool, which is the paradigm case for this field. It is also
**reciprocal**: amisrsynthdata already lists `https://github.com/gemini3d/pygemini` in its own
interoperable software, so this addition makes an existing one-way link in the catalogue point both
ways. A user who arrives at either entry should be able to find the other.

**Six values removed.** HSSI carried all six before this refresh and they are removed at this
refresh: each is a dependency GEMINI links or calls, and none is a peer tool a user would
deliberately combine with it.

| Value | Why it fails |
|---|---|
| `https://github.com/HDFGroup/hdf5` | The HDF5 library. Pure I/O plumbing — equally at home in a web app, a finance model or a biology pipeline, which is the form's own test for generic infrastructure. A reader learns nothing from "interoperates with HDF5" that Fields 18 and 19 do not already tell them by listing HDF5 as the input and output format. |
| `https://github.com/geospace-code/h5fortran` | A Fortran HDF5 wrapper. Same category. GEMINI *links* it; there is no exchange between two tools. It is removed from Field 29 as well, on the same generic-infrastructure ground — see the verdict there. |
| `https://mumps-solver.org/` | A general sparse direct solver called from inside the potential solve. Not a peer tool; the user never combines GEMINI with MUMPS, they build GEMINI against it. It is removed from Field 29 as well — see the verdict there. |
| `https://netlib.org/lapack/` | Dense linear algebra. Generic numerical infrastructure; true of an enormous fraction of compiled scientific software. Not relocated to Field 29. |
| `https://www.netlib.org/scalapack/` | Distributed linear algebra, pulled in via MUMPS (`CMakeLists.txt`: "we'll get LAPACK and SCALAPACK from MUMPS to avoid duplication of CMake script in this project"). Same reasoning, and it is not even a direct dependency. |
| `https://www.mcs.anl.gov/research/projects/mpi/` | MPI. A parallel-programming standard, not a software package this one interoperates with; "uses MPI" is true of most HPC codes. The HPC capability it represents is already recorded as `Servers and Environments: High Performance Computing` in Field 4 and `HPC or HEC` in Field 21. |

Applying the same bar to what is left produces a field that says something specific and true: GEMINI
exchanges data with its Python front end, its MATLAB front end, and one downstream synthetic-data
tool. Compare the removed set, which would read identically for a great many compiled scientific
codes.

**Considered and not added.**

- **ForestClaw.** This is the most interesting near-miss and it deserves recording, because the
  evidence looks stronger than it is. `src/inputdata/` contains `neutraldata3Dobj_fclaw.f90`,
  `neutraldata3Dobj_fclaw_axisymm.f90` and `neutraldata3Dobj_fclaw_3Dx.f90`, and these are **built**
  — `src/inputdata/CMakeLists.txt` lines 67, 74 and 81 declare them as libraries and `src/CMakeLists.txt`
  links them into the main targets. The class comment reads "type definition for 3D neutral data that
  will be provided from a parallel model (i.e. one that runs with GEMINI)", and `include/gemini3d.h`
  line 125 says "some of these will very likely need to be rewritten when used with forestclaw". It
  The word "forestclaw" itself occurs four times in three files: the `include/gemini3d.h` comment
  above, `TODO.md` line 27 listing "p4est based; ForestClaw?" as an open question, and — the
  strongest of the four — `src/libgemini.f90` lines 1603 and 1631, where the public subroutines
  `interp3_in` and `interp2_in` declare their point arguments `! single points based on forestclaw
  organization`.

  **Those last two also show that ForestClaw and MAGIC are one coupling, not two.** Both subroutines
  carry the doc comment "Interface to access trilinear interpolation routines in gemini and
  interpolate MAGIC data", and `interp3_in` notes inline "note that the MAGIC coordinatees are
  permuted x,y,z". So the ForestClaw-organised entry points exist in order to receive MAGIC's field
  data. ForestClaw is nonetheless not added, for two reasons that are independent of the MAGIC
  question: no ForestClaw URL, dependency, build target or test exists anywhere in the tree, and
  ForestClaw is a general adaptive-mesh PDE framework — generic infrastructure by the form's own
  test, not a heliophysics peer tool. If a future revision adds a real ForestClaw dependency or a
  working coupled example, revisit this.
- **MAGIC** (the acoustic-gravity wave model GEMINI takes neutral perturbations from).
  `src/inputdata/neuslab_mpi.f90` line 3 states its submodule "contains utility procedures
  specifically for computing overlaps between GEMINI and MAGIC grids", and `docs/Readme_input.md`
  points at a `magic/` directory of input-preparation examples — this is a real, working exchange and
  it would pass the relevance bar comfortably. It is not added because **Field 30 requires a URL and
  MAGIC has no public repository or landing page** that this revision names. `TODO.md` line 28's
  "Two way coupling with MAGIC" shows the relationship was still being developed at this revision.
  This is the one genuine interoperation the field cannot express for want of a URL rather than for
  want of evidence; if MAGIC acquires a public repository or landing page, it should be added.
- **`https://github.com/gemini3d/gemci`** — CI fixtures, not a peer tool. See Field 29.
- **The generic scientific-Python stack.** `numpy`, `h5py` and `matplotlib` are imported by the
  Python test drivers in `test/`, and `astropy.coordinates` by `test/temporal/PlotSZA.py`. All are
  Tier A or unevidenced Tier B: importing a library in a test script is not an exchange with a peer
  tool.

---
### 31. Related Instruments (OPTIONAL)
**Value:** None — deliberately empty

### 32. Related Observatories (OPTIONAL)
**Value:** None — deliberately empty

**Fields 31 and 32 are argued together, because the same evidence settles both.** An earlier
extraction recorded "Not found" on the general theory that "the software is a modeling tool and not
tied to specific instruments". That conclusion is right, but the theory is not a substitute for
evidence — a model *can* be instrument-specific, and plenty of models in this catalogue are. So the
question was re-derived from the pinned tree rather than inherited.

**The relevance test.** An instrument or observatory belongs here only if the software is *designed
to support* it: reads, writes, parses, calibrates or processes that specific instrument's data;
implements a format or convention specific to it; is purpose-built or an instrument-team tool for
it; or models or visualises its measurements as a primary function. GEMINI satisfies none of these
for any instrument or observatory.

**Three independent sweeps of the pinned tree, all negative.**

1. **By concept.** Searched case-insensitively, with word boundaries, for twenty-six instrument,
   observatory and platform terms — `Arecibo`, `PFISR`, `RISR`, `EISCAT`, `Millstone`, `Sondrestrom`, `Jicamarca`,
   `AMISR`, `SuperDARN`, `DMSP`, `Swarm`, `CHAMP`, `GOLD`, `ICON`, `incoherent scatter`, `radar`,
   `magnetometer`, `ionosonde`, `riometer`, `photometer`, `all-sky`, `imager`, `Fabry`, `FPI`,
   `Poker` and `Svalbard`. Searching each with word boundaries, **exactly one of those 26 terms
   matched anything: `Arecibo`, in 1 file** — and it is not an association, but an invented
   output-directory name in a `Readme.md` usage example
   (`mpiexec -np 4 build/gemini.bin ~/mysim3d/arecibo`). The other 25 matched 0 files. Control under
   the identical query shape: `ionosphere` matches 8 files. Separately, the bare acronym `ISR`
   appears as the adjective in
   `src/io/io_nompi.f90` and `src/io/plasma_output_hdf5.f90`, "output ISR-like average parameters",
   describing an output *mode* that emits the quantities an incoherent-scatter radar measures
   (`ne,Ti,Te,v1`) without reference to any particular radar.
2. **By naming authority.** Searched for `spase-metadata.org`, `hpde.io`, `nssdc` and `SMWG`: zero
   files matched.
3. **Mechanically, against the whole controlled vocabulary.** This is the sweep that makes the empty
   defensible rather than merely unrefuted, so its denominator matters. Every `name` and
   `abbreviation` of six characters or more in the `InstrumentObservatory` vocabulary — 5,446
   distinct terms — was matched, with word boundaries and case-insensitively, against the
   concatenated non-empty text lines of every text file in the pinned tree (41,049 lines). Controls
   under the identical matcher: `ionosphere` found, a nonsense token not found. Worth recording
   alongside it: at the time of this sweep every row in that vocabulary carried an
   `https://spase-metadata.org/` identifier, with none failing the guard — the guard is nonetheless
   a real one and a future refresh must keep applying it, because a row without a SPASE identifier
   means upstream drift or a row wrongly created, and must be reported rather than used.

   **Eight of the 5,446 terms matched, and all eight are false positives.** Each is resolved
   individually below rather than dismissed as a group:

   | Vocabulary term | Row it belongs to | Where it actually occurs in the tree |
   |---|---|---|
   | `Cluster` | observatory `SMWG/Observatory/Cluster` | ordinary English: "high-performance computing (HPC) cluster", "a cluster environment", "Dartmouth Polaris cluster" |
   | `Darwin` | observatory `ASWS/Observatory/Ground/Darwin` | `darwin*)` in a shell `case` statement in `scripts/hwm14_debug.sh` — the macOS kernel name |
   | `ELECTRON` | abbreviation of instrument `Interball-1/ELECTRON` | the word "ELECTRON" in Fortran comments, e.g. "DISTURBANCE ELECTRON PRECIPITATION PATTERN" |
   | `Legacy` | abbreviation of instrument `HamSCI/.../Grape1Legacy` | "legacy coding style", "legacy rates", "the legacy GEMINI value" |
   | `Magnetic Field` | name of instrument `SMWG/Instrument/Ulysses/FGM` | the `magcalc` documentation: "## Computing Magnetic Field Perturbations" |
   | `Geomagnetic Indices` | observatory `CNES/Observatory/CDPP-AMDA/Indices` | one console message, `src/gemini_init.f90` line 56: `print*, 'F10.7 and geomagnetic indices:  ',cfg%activ` — printing the user's own `activ` configuration values, not reading an index service |
   | `Resolute Bay` | observatory `SMWG/Observatory/IAGA/Resolute.Bay` | a **publication title** in `docs/Readme_references.md` line 17 (Perry et al. 2015) |
   | `Rocket Experiment for Neutral Upwelling 2` | observatory `SMWG/Observatory/RENU2` | a **publication title** in `docs/Readme_references.md` line 33 (Burleigh et al. 2019) |

**The last two deserve a direct answer, because they are the strongest case anyone will make for
filling this field.** Resolute Bay and RENU2 are real heliophysics observatories with real SPASE
rows, and GEMINI genuinely was used in studies of both. But the software does not read RISR data,
does not parse RENU2 telemetry, ships no configuration for either, and names them nowhere outside
the bibliography. A user searching HSSI for `observatory:"RENU2"` wants tools for working with
RENU2 data; GEMINI would be noise in that result. The right home for those campaigns is Field 27,
where both papers already are.

**Other candidates considered and rejected.**

- **`magcalc`'s "ground stations" and "satellite tracks".** `docs/Readme_magcalc.md` says the field
  points "could be a list of ground stations (irregular mesh), a regular mesh, or a set of satellite
  tracks (irregular mesh)". These are whatever coordinates the user writes into
  `magfieldpoints.{h5,dat}`; no station list, magnetometer network or spacecraft is named or shipped.
- **The example simulation location.** `test/config/config_example.nml` sets `glat = 67.11` /
  `glon = 212.95` — a bare coordinate pair in the Alaskan sector with no site name attached anywhere
  in the tree. A latitude and longitude in a demo configuration is not an observatory association.
  Searching the tree for `observatory` or `station` returns only "ground stations", "stationary
  grid" and "workstation" (control: `glat` matches 38 files).
- **The "ISR-like" output mode** (see sweep 1). This is a *phenomenon of the output format*, not
  instrument support. If anything it argues the opposite: GEMINI emits quantities comparable to what
  ISRs measure precisely so that it is *not* tied to any one radar.
- **AMISR, via `amisrsynthdata`.** The tool recorded in Field 30 turns GEMINI output into synthetic
  AMISR data files and is correctly associated with the AMISR observatory — on *its* record. The
  instrument-specific work happens there, not here; GEMINI has no AMISR-specific code.

**A note on procedure, because it constrains any future addition.** These fields are SPASE-only:
there is no free-type path, and a bare name either binds to an arbitrary same-name row or creates a
new identifier-less one. Any value added in a later refresh must carry an
`https://spase-metadata.org/` identifier resolved against the live vocabulary — never completed from
a pattern.

---

### 33. Logo (OPTIONAL)
**Value:** Not found

**Searched thoroughly; the project has no logo, and this is a documented omission rather than a
gap.**

- **No image file exists in the pinned tree.** Listing every path at this revision and filtering for
  `.png`, `.jpg`, `.jpeg`, `.svg`, `.gif`, `.ico`, `.webp`, `.bmp` and `.pdf` returns nothing (the
  filter's exit status confirms an empty result, not a failed command).
- **Nor did one ever exist that could serve.** Searching the entire add-history reachable from this
  revision for image files finds three that were added and later removed: `doc/figure1.png`,
  `doc/figure2.png` and `tests/data/CDash.png`. A pair of numbered figures and a CI-dashboard
  screenshot; none is a logo, and none is present at the pin.
- **The word "logo" does not appear in any meaningful sense.** Searching the tree case-insensitively
  for `logo`, `favicon` or `banner` returns four hits, all of them the substring inside the word
  "analogous" in the four `app/main*.f90` files.
- **The documentation site offers only FORD's own favicon.** `https://gemini3d.github.io/gemini3d/`
  references exactly two images: `./favicon.png` and a Creative Commons licence badge served from
  `i.creativecommons.org`. The favicon fetches as `image/png`, 803 bytes, 32×32 — and looking at it,
  it is a serif italic "f" on a dark navy square: the FORD documentation generator's own mark, not
  GEMINI's. Recording it would put another project's logo on this entry.
- **The PyHC registry supplies none.** Several entries in `projects_unevaluated.yml` carry a `logo:`
  key (DASCutils, GOESutils, GLOW, HWM-93, IGRF-13, IRI-2016, IRI-90, LOWTRAN, THEMISasi). The
  `PyGemini` entry, quoted in full under Field 7, has no `logo:` key.
- **The Python repository has none either**, which is worth recording because it closes the question
  from the other side too: `gemini3d/pygemini` contains no image file of any kind, and a
  case-insensitive search of it for `logo` returns no match (control: `gemini` matches 66 files).
  Neither repository in the stack has a logo, so no naming outcome would have supplied one.
- **The DOI records carry no image.** Neither the concept record nor the current version record
  exposes a logo or thumbnail.

**Do not invent one.** A screenshot of model output, an example plot, or an institutional mark would
all be wrong here: the field asks for "the logo for the software", and this software does not have
one. If the project adopts one, the value must be a fetched, verified `image/*` URL — and if it is
git-hosted, pinned to a 40-character commit SHA on `raw.githubusercontent.com`, never a branch name
and never a `blob/` page URL.

---
