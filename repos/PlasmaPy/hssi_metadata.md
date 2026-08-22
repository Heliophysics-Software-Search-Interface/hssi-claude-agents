# HSSI Metadata Extraction Results

**HSSI Software ID:** 4507d98e-44d1-40ea-8733-8047738b9a7a
**Repository:** https://github.com/PlasmaPy/PlasmaPy
**Source Revision:** 02d1c194a5b054516167b24503abe27b4e77825d
**Extraction Date:** 2026-08-07
**Validation Date:** 2026-08-22
**Validation Status:** PASS
**Scope note — read the evidence with this in mind.** The pinned source revision is 97 commits ahead
of the most recent release, `v2026.2.0` (2026-02-20). Some evidence cited below therefore comes from
unreleased `main`: the `plasmapy.formulary.fusion` module and six `CITATION.cff` author entries do
not exist in the `v2026.2.0` tarball. Those are recorded because they are real, merged, and
authoritative at the pinned revision, and because Field 6 and Field 4 describe the software rather
than a single release. Field 12 (Version) deliberately does **not** follow `main` — it records the
latest released version only, and must never be advanced from unreleased commits.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*PlasmaPy's HSSI record was not submitted by this project; the submitter identity is not recoverable
from the stored record, which is why the placeholder stands rather than a name.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.6774349

*This is the Zenodo **concept** DOI for the chain that tracks PlasmaPy's current releases. It resolves
to https://zenodo.org/records/18706665 — version `2026.2.0`, published 2026-02-20 — and Zenodo reports
that record's `conceptdoi` as `10.5281/zenodo.6774349` (equivalently, its `conceptrecid` is `6774349`).
It is therefore the concept parent of the version DOI recorded in Field 12
(`https://doi.org/10.5281/zenodo.18706665`), so Fields 2 and 12 describe the same Zenodo lineage:
Field 2 stays stable across releases while Field 12 stays precise. Repository evidence for this DOI:
`docs/install.rst:237` (`.. _from Zenodo: https://doi.org/10.5281/zenodo.6774349`) and
`.github/content/release-checklist.md:149`, which points a maintainer cutting a release at
`https://zenodo.org/doi/10.5281/zenodo.6774349` as "this record".*

**Correction to a previously recorded and previously stored value.** The earlier value was
`https://doi.org/10.5281/zenodo.1436011`, justified in this file as "the Zenodo **concept** DOI, which
always resolves to the newest release." That justification was factually wrong and the value is
corrected here. PlasmaPy's Zenodo integration **forked into two separate concept-DOI chains**, and
`1436011` heads the abandoned one: it resolves to https://zenodo.org/records/4037407 — version
`0.4.0`, published 2020-07-21 — and froze there when the fork happened. Its DataCite record still
reports `version: 0.4.0` with `publicationYear: 2020`, the newest release in its `HasVersion` list is
`10.5281/zenodo.4037407` (record 4037407, v0.4.0, 2020-07-21), and its `relatedIdentifiers` carry
`IsPreviousVersionOf 10.5281/zenodo.6774349`, which marks the fork point. A persistent identifier that
resolves to a 2020 v0.4.0 release does not persistently identify this software, and keeping it would
have left Fields 2 and 12 split across two unrelated chains.

*Alternative considered and not adopted: keeping `1436011` because it is the long-standing public
badge. `README.md:20` still renders `https://zenodo.org/badge/DOI/10.5281/zenodo.1436011.svg` linking
to that DOI, and `docs/conf.py:392` lists `https://doi.org/10.5281/zenodo.1436011` among the
linkcheck-ignore patterns. That is a documented inconsistency inside PlasmaPy's own repository, not
evidence that the abandoned chain is the right identifier: the two places a user or maintainer actually
follows — the installation instructions and the release checklist — both point at `6774349`. A future
agent that finds the README badge should read it as the known-stale artifact described here rather than
as a reason to revert this field. If upstream later repoints the badge, that is confirmation of this
choice, not new information.*

*Neither of the project's citation sources contradicts this choice, because neither names a concept
DOI at all: `CITATION.cff` gives `identifiers: - type: doi / value: 10.5281/zenodo.18706665` and
`docs/about/citation.rst` substitutes `https://doi.org/10.5281/zenodo.18706665`. Both are the
**version-specific** DOI, which is recorded in Field 12.*

*Do not derive Fields 10, 12, or 15 from `1436011`'s DataCite record — it is a 2020 snapshot
(`version 0.4.0`, publication year 2020, rights `Other (Open)`). The version DOI's DataCite record is
current and is the one cited in those fields.*

### 3. Code Repository (MANDATORY)
https://github.com/PlasmaPy/PlasmaPy

*Confirmed against `CITATION.cff` (`repository-code`), `pyproject.toml` (`urls.Source`), and the live
GitHub repository, which is not archived and whose default branch is `main`.*

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Magnetic Null Finding
- Data Processing and Analysis: Plasma Moments
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 3D Graphics
- Data Visualization: Line Plots
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: First Principles
- Models and Simulations: Forward-Fitting
- Models and Simulations: Instrument Response
- Models and Simulations: MHD
- Models and Simulations: Physics-Based
- Models and Simulations: Theory

**Evidence per value, from `src/plasmapy/`:**

- `plasmapy.particles` — object-oriented and functional access to particle, element, isotope, and
  ionization-state data, including `IonizationState` / `IonizationStateCollection` (Analysis).
- `plasmapy.formulary` — plasma parameter formulas drawn largely from the NRL Plasma Formulary:
  frequencies, lengths, speeds, drifts, collisions (`collisions/`), dielectric tensor, dimensionless
  parameters, distribution functions, magnetostatics, laser, quantum and relativistic quantities
  (Theory, Physics-Based, First Principles).
- `plasmapy.dispersion` — analytical (Stix cold-plasma, two-fluid, MHD waves) and numerical
  (Hollweg, kinetic Alfvén) dispersion solvers plus the plasma dispersion function (MHD, Theory,
  Physics-Based).
- `plasmapy.plasma` — `equilibria1d` (Harris sheet), `cylindrical_equilibria.ForceFreeFluxRope`
  (Lundquist force-free flux rope), generic plasma classes, structured and unstructured Cartesian
  grids, and the OpenPMD HDF5 reader (MHD, Analysis).
- `plasmapy.simulation` — `ParticleTracker` with Boris and relativistic Boris integrators, Yee CFL
  resolution constraints, and termination conditions (First Principles, Physics-Based).
- `plasmapy.diagnostics` — Thomson scattering (`spectral_density`), swept Langmuir probe analysis,
  and synthetic charged-particle (proton) radiography (Analysis, Energy Spectra, Forward-Fitting).
- `plasmapy.analysis` — fit functions, swept Langmuir analysis, time-series conditional averaging,
  excess statistics, running moments, and 3D magnetic null point finding (Analysis, Time Series
  Analysis, Magnetic Null Finding).
- **Data Access and Retrieval** — `plasmapy.utils.data` exports a public `Downloader` class that
  retrieves PlasmaPy resource and sample-data files from the `PlasmaPy/PlasmaPy-data` repository via
  the GitHub contents API (`_API_BASE_URL`) and raw HTTPS (`_RAW_BASE_URL`), with a local cache and
  SHA-based freshness validation. This is user-callable retrieval of remote data, not a build-time
  step. Recorded because the stored classification omitted it.
- **Plasma Moments** — `plasmapy.diagnostics.langmuir.swept_probe_analysis` returns electron and ion
  number densities, electron temperature, and plasma/floating potential derived from a measured
  probe I–V characteristic, and `get_EEDF` recovers the electron energy distribution function;
  `plasmapy.diagnostics.thomson.spectral_density_model` recovers electron/ion densities,
  temperatures, and drift velocities by fitting a measured Thomson scattering spectrum. These are
  bulk plasma quantities recovered from measurements, which is what this category is for, even
  though PlasmaPy reaches them by fitting rather than by moment integration of a measured velocity
  distribution.
- **Processing** — `plasmapy.analysis.swept_langmuir.helpers` conditions and sorts probe traces
  before analysis (`check_sweep`, `sort_sweep_arrays`), and `plasmapy.plasma.grids` provides
  nearest-neighbour and volume-averaged interpolators for moving quantities on and off grids. This
  row stays as the general pipeline-transform category; the volume-reducing part of the same
  subpackage's work is recorded more specifically under `Data Reduction` below. (An earlier version of
  this note also credited `helpers` with *smoothing* probe traces. It does not: at this revision
  `swept_langmuir/helpers.py` exports only `check_sweep`, `merge_voltage_clusters`, and
  `sort_sweep_arrays`, and the sole mention of smoothing in the subpackage is an error message in
  `swept_langmuir/floating_potential.py:288` advising the *user* to smooth the current.)
- **Data Reduction** — `plasmapy.analysis.time_series.running_moments` reduces a signal over a
  sliding window: `running_mean(signal, radius)` and `running_moment(signal, radius, moment, time)`.
  The moments `running_moment` returns are, per its own docstring, a running **standard deviation**
  (`moment=2`, `running_moments.py:85`), skewness (`moment=3`, `:86`), or excess kurtosis (`moment=4`,
  `:87`) — **not** variance, which an earlier version of this note wrongly recorded. The
  implementation settles it: `:144` computes `run_moment = np.sqrt(running_mean(difference**2,
  radius))`, the square root of the mean squared deviation. The classification is unaffected by that
  correction; only the description was imprecise.
  `plasmapy.analysis.swept_langmuir.helpers` reduces a Langmuir trace before analysis:
  `merge_voltage_clusters` (docstring: "merge those clusters, and associated `current` values, into a
  single point") dispatches at `helpers.py:565` to `_merge_voltage_clusters__zero_diff_neighbors`,
  which averages clusters of identical voltage points, and at `:571` to
  `_merge_voltage_clusters__within_dv`, which averages clusters of voltage points within
  `voltage_step_size` of one another — collapsing many samples into one. Windowed averaging and
  cluster-averaging cut data volume while preserving the information the downstream analysis needs,
  which is what this subcategory is for and is a more specific fit for that evidence than the generic
  `Processing` row, which also remains listed.
- **Empirical** — `plasmapy.formulary.fusion` evaluates fusion cross sections and Maxwellian-averaged
  reactivities from the Bosch–Hale Padé (rational-function) parametrization of the astrophysical
  S-function, using the published Table IV coefficients where available and coefficients fit to
  ENDF/B evaluated cross sections for the remaining reactions; `plasmapy.formulary.braginskii`
  implements tabulated/fitted transport coefficients. These are parametrized fits to measured or
  evaluated data, not first-principles derivations, so `Empirical` applies alongside
  `First Principles` rather than instead of it.
- **Instrument Response** — `plasmapy.diagnostics.charged_particle_radiography.detector_stacks`
  provides `Layer` and `Stack` with `deposition_curves` and `energy_bands`, modelling how particle
  energy is deposited through a radiochromic-film detector stack; `synthetic_radiography.Tracker`
  and `synthetic_radiograph` generate the synthetic diagnostic image itself.
- **Line Plots / 2D Graphics** — `plasmapy.diagnostics.langmuir` draws probe characteristics,
  logarithmic-current fits, and EEDF plots directly (`matplotlib.pyplot` scatter/line calls); the
  maintained example gallery renders `synthetic_radiograph` output and dispersion parameter maps
  with `pcolormesh`, `contourf`, and `imshow`.
- **3D Graphics** — five notebooks in the example gallery build a 3D axes with `projection="3d"` and
  render PlasmaPy quantities on it; they are the complete set of `projection=` matches under
  `docs/notebooks/` at this revision. What they plot is not the same thing, so it is recorded per
  notebook:
  - `docs/notebooks/simulation/particle_tracker.ipynb` — `ax.plot(*particle_trajectory.T)`: the 3D
    trajectory produced by PlasmaPy's own `ParticleTracker`. This is the strongest of the five, being
    genuine simulation output rendered in 3D.
  - `docs/notebooks/diagnostics/charged_particle_radiography_particle_tracing.ipynb`,
    `..._particle_tracing_custom_source.ipynb`, and `..._particle_tracing_wire_mesh.ipynb` — each
    renders the *setup geometry* of a synthetic-radiography run in 3D: the
    `plasmapy.plasma.grids.CartesianGrid` E-field volume, plus the `Tracker`'s source-to-detector axis
    and source/detector positions (`ax.quiver` and `ax.scatter` over `sim.source` / `sim.detector`).
    The synthetic radiograph itself is a 2D image plotted elsewhere in those notebooks, so these three
    support 3D rendering of PlasmaPy grid and geometry objects rather than of a radiography product.
  - `docs/notebooks/formulary/ExB_drift.ipynb` — plots guiding-centre drift orbits in 3D
    (`ax.plot(x, y, z)`, twice, with and without the drift term). The orbits are integrated by the
    notebook itself in an explicit time-stepping loop inside `single_particle_trajectory`,
    parameterized by PlasmaPy's `gyrofrequency` and `gyroradius`. So this is PlasmaPy quantities
    visualized in 3D rather than a PlasmaPy trajectory product.

**On the differing evidence tiers behind `2D Graphics` and `3D Graphics`.** **Both values are kept**,
and they do *not* rest on the same footing. Recorded explicitly so a future agent can see what backs
each one without re-deriving it, and so the two are not treated as a single decision:

- `2D Graphics` has **library-code** support. A search of `src/` at this revision for
  `import matplotlib` returns a single match, `src/plasmapy/diagnostics/langmuir.py:26`
  (`import matplotlib.pyplot as plt`), and it drives plotting from inside the library itself — probe
  characteristics, logarithmic-current fits, and EEDF plots, as described in the Line Plots /
  2D Graphics bullet above. The gallery's 2D rendering is corroboration on top of that rather than
  its only support, and the three calls named there sit in specific notebooks: `pcolormesh` in the
  three `charged_particle_radiography_particle_tracing*` notebooks, which is where
  `synthetic_radiograph` output is displayed; `contourf` in
  `docs/notebooks/dispersion/dispersion_function.ipynb`; and `imshow` in
  `docs/notebooks/dispersion/two_fluid_dispersion.ipynb`.
- `3D Graphics` has **no** library-code support. Searching `src/` at this revision for `mplot3d`,
  `Axes3D`, `plot_surface`, `plot_trisurf`, `plot_wireframe`, `scatter3d`, and `projection=...3d`
  returns no match, so PlasmaPy exposes no 3D plotting function of its own; the value rests entirely
  on the five gallery notebooks listed above. Their maintenance evidence is **not uniform across the
  five**, and the split is recorded here because an earlier version of this note asserted a single
  execution mechanism over the whole set and was wrong about three of them:
  - **Two are re-executed on every documentation build.** `particle_tracker.ipynb` (0 of 24 cells
    carry stored outputs) and `ExB_drift.ipynb` (0 of 17) are committed output-free. `docs/conf.py`
    sets no `nbsphinx_execute` override, so nbsphinx's default `"auto"` applies, which executes
    precisely those notebooks that have no stored outputs. `.github/workflows/ci.yml` runs the `docs`
    nox session ("Documentation, Python 3.14, Ubuntu"), so these two are genuinely exercised in CI —
    and one of them is `particle_tracker.ipynb`, the flagship `ParticleTracker` 3D example, which is
    why this value's core support is real rather than nominal.
  - **Three render from committed cached outputs and are not re-executed.**
    `charged_particle_radiography_particle_tracing.ipynb` (9 of 23 cells carry stored outputs),
    `..._custom_source.ipynb` (10 of 44), and `..._wire_mesh.ipynb` (7 of 31) each have at least one
    output cell, so nbsphinx `"auto"` skips executing them. Their standing as maintained project
    material rests on publication rather than execution: `docs/index.rst:53` and
    `docs/ad/diagnostics/charged_particle_radiography/synthetic_radiography.rst:16–18` reference them
    by path in `nbgallery` directives, and `docs/examples.rst` gathers the gallery through globbing
    `nbgallery` directives (`notebooks/simulation/*` at `:71`, with `docs/simulation/index.rst:36`
    globbing the same directory). **A future agent must not claim CI executes these three.**

  So a reviewer weighing this value is weighing executed-notebook evidence for two of the five and
  published-gallery evidence for the other three. Either way the value should not be assumed to stand
  or fall with `2D Graphics`.

**Considered and not selected** (recorded so these are not re-proposed without new evidence):

- *Coordinate Transforms* (and all six children) — the nearest thing to a coordinate transform in the
  package is `_coerce_to_cartesian_si`, a private helper in `charged_particle_radiography` that
  converts Cartesian/cylindrical/spherical *position* tuples to metres. Searching the source text
  under `src/` at this revision for `GSE`, `GSM`, `SM`, `Carrington`, `Stonyhurst`, `helioprojective`,
  `AACGM`, `MLT`, and `heliographic` returns no match (a raw byte search does hit `GSE` and `MLT`
  inside one binary HDF5 test fixture, `data00000100.h5`, which contains no transform code), so there
  is no user-facing transform between heliophysics reference frames.
- *Data Processing and Analysis: 3D Particle Distribution Processing* — `plasmapy.formulary.distribution`
  evaluates analytic Maxwellian and kappa distribution functions (including `Maxwellian_velocity_3D`
  and `kappa_velocity_3D`), which is model evaluation rather than processing of a measured 3D
  velocity distribution product; `get_EEDF` returns a 1D energy distribution. Nothing in the package
  reads or reduces an instrument VDF.
- *Data Processing and Analysis: Field-line Tracing* and *Models and Simulations: Field-line Tracing*
  — no tracing, streamline integration, or PFSS-style extrapolation exists in the source. The
  `nullpoint` module locates nulls; it does not trace the separatrices from them.
- *Data Processing and Analysis: Image Processing* — `synthetic_radiograph` produces a particle-count
  histogram; there is no deconvolution, feature detection, or image restoration.
- *Servers and Environments: Software or Environment Container* — `binder/` contains only a
  `requirements.txt`; there is no Dockerfile, Singularity definition, or served endpoint in the
  repository.
- *Models and Simulations: Forecasting*, *Data Assimilation*, *ML/AI* — no predictive, assimilative,
  or machine-learning code paths exist.

### 5. Related Region (MANDATORY)
- Solar Environment
- Corona
- Chromosphere
- Photosphere
- Solar Wind
- Interplanetary Space
- Earth Magnetosphere

*`Solar Environment`, `Interplanetary Space`, and `Earth Magnetosphere` are carried over from the
existing HSSI record. Four regions are added from repository evidence:*

- **Solar Wind** — `plasmapy.formulary.collisions.helio` exists as a dedicated subpackage whose
  module docstring states "Applications include the solar wind", and its `temp_ratio` function models
  ion thermalization for a plasma in transit between two heliocentric distances in astronomical
  units, following Maruca (2013) and Johnson (2023). This is the most specific applicable region and
  the strongest region evidence in the package.
- **Corona** — the load-bearing evidence is a docstring example inside the library itself:
  `src/plasmapy/formulary/lengths.py:222` reads "Let's estimate the proton gyroradius in the solar
  corona" and then calls `gyroradius(B=0.2 * u.T, particle="p+", T=1e6 * u.K)`. That example is an
  executed doctest, not decoration: `noxfile.py` adds `--doctest-modules` to the test session for the
  highest supported Python, and `.github/workflows/ci.yml` runs that session as
  `tests-3.14(skipslow)` with no job-level condition on it, so the corona example is exercised on every
  run of that workflow — which triggers on pull requests and on pushes to `main`, `stable`, release
  branches, and tags.
  `docs/notebooks/formulary/solar_plasma_beta.ipynb` has a "Solar corona" section that computes plasma
  β as well, and it corroborates this region — but only corroborates it: that section introduces
  `T_corona = 1 * u.MK`, `n_corona = 1e9 * u.cm**-3`, and `B_corona = 50 * u.G` as uncited illustrative
  parameters "for an active region in the solar corona", with no reference attached.
- **Chromosphere** — the "Solar chromosphere" section of
  `docs/notebooks/formulary/solar_plasma_beta.ipynb` computes plasma β from published parameters, and
  it is this section, **not** the corona section, that carries the literature citations: Bogod et al.
  (2015) for the quiet chromosphere's field range of ∼40–200 G, and model C7 of Avrett & Loeser (2007)
  for the temperature and hydrogen number density 1 Mm above the photosphere
  (`T_chromosphere = 6225 * u.K`, `n_chromosphere = 2.711e13 * u.cm**-3`,
  `B_chromosphere = [40, 200] * u.G`). An earlier version of this note attributed both citations to the
  corona *and* the chromosphere calculations; they belong to the chromosphere one alone.
- **Photosphere** — `docs/notebooks/formulary/solar_plasma_beta.ipynb` continues past its chromosphere
  section into two further sections that compute plasma β for the photosphere. "Quiet solar
  photosphere" uses `T_photosphere = 5800 * u.K`, `n_photosphere = 1e17 * u.cm**-3`, and
  `B_photosphere = 400 * u.G`, and the notebook reads off that β is an order of magnitude above 1, so
  plasma pressure-gradient forces dominate magnetic ones there. "Sunspot photosphere" then uses
  `T_sunspot = 4500 * u.K` and `B_sunspot = 2 * u.kG` with the same `n_photosphere`, on the stated
  reasoning that the photospheric field is strongest in sunspots so β should be lowest there. As in
  the corona section, these are uncited illustrative parameters rather than literature-sourced ones.

  **This value corrects a previously recorded claim that was factually wrong.** An earlier version of
  this file listed `Photosphere` among the regions having "no supporting content", grouped with
  `Solar Interior` and the planetary magnetospheres. That was incorrect. The evidence above sits in
  the same notebook, in the two sections immediately following the chromosphere section that the
  accepted `Chromosphere` value rests on, so rejecting `Photosphere` while accepting `Chromosphere`
  was arbitrary rather than evidence-based. A future agent must not re-reject this region on the "no
  supporting content" basis: the content is in `solar_plasma_beta.ipynb` and is quoted here so the
  question does not have to be re-derived. The negative half of that earlier finding does still hold,
  and bounds the case: `photospher*` matches no file under `src/` and no notebook under
  `docs/notebooks/` other than `solar_plasma_beta.ipynb`, so that one notebook is the whole of the
  evidence for this region.

Field 5 asks which physical regions the software is *commonly used for*, which a maintained worked
example answers directly — that is the basis on which the notebook evidence above is admitted.

**The three solar-atmosphere values draw on one shared artifact, but they do not all depend on it —
and the difference decides what a future reviewer may drop.** The shared artifact is
`docs/notebooks/formulary/solar_plasma_beta.ipynb`, whose title is "Plasma beta in the solar
atmosphere", whose opening cell states its purpose as "calculating plasma β in different regions of the
solar atmosphere", and whose addition `docs/changelog/0.8.1.rst:455` records in PR #1552 in those same
terms. Its four calculations are corona, chromosphere, quiet photosphere, and sunspot photosphere.
Only two of the three values rest on it:

- **`Chromosphere` and `Photosphere` are notebook-only, and stand or fall together.** Neither has any
  support in `src/`; both come from adjacent sections of that single file. This pairing is what made
  adding `Photosphere` a matter of consistency rather than a fresh judgement — the accepted
  `Chromosphere` value already admitted exactly this tier of evidence from exactly this artifact, so
  excluding `Photosphere` was arbitrary. A future agent who concludes that notebook-tier evidence is
  too weak for Field 5 must drop both of these; one who accepts either is committed to the other.
- **`Corona` is corroborated by that notebook but does not depend on it.** Its load-bearing evidence is
  the executed `src/plasmapy/formulary/lengths.py:222` doctest — library code, exercised in CI, wholly
  independent of the notebook. **A reviewer who rejects notebook-tier evidence entirely must still keep
  `Corona`.** Do not drop it alongside the other two.

Evidence *quality* differs inside the notebook-only pair as well, and a future agent should see that
rather than assume parity. `Chromosphere`'s parameters are attributed to published models — Bogod et
al. (2015) for the quiet-chromosphere field range, and Avrett & Loeser (2007) model C7 for temperature
and hydrogen density — while `Photosphere`'s values, like those in the corona section, are uncited
illustrative parameters. That is a difference in strength rather than in kind: an uncited worked
example in a maintained notebook still demonstrates a region the software is used for, which is what
Field 5 asks. It does mean `Chromosphere` is the sturdier half of the pair, and that if the pair were
ever narrowed, `Photosphere` is the one to reconsider first.

Field 4's `2D Graphics` / `3D Graphics` pair has the **same shape**, and the parallel is worth carrying
across rather than treating as a contrast: in both fields one value has executed library-code evidence
(`src/plasmapy/diagnostics/langmuir.py:26` there, the `lengths.py:222` doctest here) while the other
rests on the example gallery. Gallery support is not uniform, and Field 4 records the detail: of its
five 3D notebooks, two are re-executed on every documentation build and three render from committed
cached outputs. `solar_plasma_beta.ipynb`, the notebook behind `Chromosphere` and `Photosphere`, stores
no cell outputs, so it falls in the re-executed group. In neither field are the two values a single
decision, and in both the library-code value survives a reviewer who discounts the gallery.

**Considered and not selected:**

- *Earth Ionosphere* and *Earth Thermosphere* — PyHC's curated registry entry for PlasmaPy carries
  the facet keyword `ionosphere_thermosphere_mesosphere`, which is why these look plausible. A
  full-text search of `src/plasmapy/` and `docs/notebooks/` at this revision finds no occurrence of
  "ionosphere", "thermosphere", or "aurora" in any form. PyHC's facet tags describe community scope
  rather than implemented functionality, so without repository evidence these are left off. If a
  future release adds ionospheric functionality, this is the note to revisit.
- *Earth Auroral Subregion* — the same negative result, re-verified at this revision and with the same
  cause. Searching `src/` and `docs/` (`.py`, `.rst`, `.md`, and notebook source cells rather than raw
  `.ipynb` bytes, so base64 image payloads cannot produce false matches) for `aurora`, `auroral`, and
  `airglow` returns no match. On that evidence PlasmaPy contains no auroral, ionospheric, or
  thermospheric functionality, so no Earth upper-atmosphere row applies.
- *Earth Atmosphere* and *Earth Lower and Middle Atmosphere* — the same search over the same scope for
  `atmospher`, `stratospher`, `mesospher`, `tropospher`, `neutral density`, and `neutral wind` returns
  four matches, and each one refers to the **solar** atmosphere rather than Earth's: the title and
  opening framing of `docs/notebooks/formulary/solar_plasma_beta.ipynb` ("Plasma beta in the solar
  atmosphere", "different regions of the solar atmosphere", and the same phrase again in its
  introductory cell) and the changelog entry announcing that notebook, which begins at
  `docs/changelog/0.8.1.rst:455` and carries the matching phrase "different parts of the solar
  atmosphere" at `:457`. Those matches are already represented by `Corona`,
  `Chromosphere`, and `Photosphere`. Within that same scope there is no neutral-atmosphere physics,
  atmospheric density or composition model, and no altitude-profile code, so neither Earth-atmosphere
  row applies.
- *Earth Magnetosheath / Inner Magnetosphere / Outer Magnetosphere / Magnetotail* — the magnetosphere
  material (`docs/notebooks/formulary/magnetosphere.ipynb`) treats reconnection and plasma parameters
  generically; nothing selects a specific magnetospheric subregion, so the broader stored
  `Earth Magnetosphere` remains the right level.
- *Solar Interior* and the planetary magnetosphere rows (`Jupiter Magnetosphere`,
  `Mars Magnetosphere`, `Saturn Magnetosphere`, `Neptune Magnetosphere`, `Uranus Magnetosphere`,
  `Planetary Magnetospheres`) — no supporting content, on the same scoped search as the rows above
  (`src/` and `docs/` `.py`, `.rst`, `.md`, and notebook source cells). `solar interior`, `tachocline`,
  `convection zone`, `radiative zone`, and `helioseismolog` return no match, and neither do `Jupiter`,
  `Saturn`, `Neptune`, `Uranus`, `Mars`, `Jovian`, or `Kronian`. The solar regions PlasmaPy does
  address stop at the photosphere (see `Photosphere` above), and on that same search no planet other
  than Earth appears in the package.
- *Heliosheath* — **rejected on the physics, not merely on the absence of the word**, because the
  absence-of-the-word test would not settle it. The candidate is genuine: PlasmaPy's one radially
  extended heliospheric model, `plasmapy.formulary.collisions.helio.collisional_analysis.temp_ratio`,
  takes heliocentric positions `r_0` and `r_n` in astronomical units and imposes no upper bound on
  either, so nothing in the signature stops a user passing 90 au. What bounds it is the model. The
  function integrates the Maruca (2013) / Johnson (2023) collisional-thermalization equation while
  scaling the primary ion's density, radial velocity, and temperature by the Hellinger et al. (2011)
  power laws `n ∝ r^-1.8`, `v_r ∝ r^-0.2`, and `T ∝ r^-0.74`, which describe the freely expanding
  supersonic solar wind. Those scalings do not survive the termination shock, past which the flow is
  decelerated, compressed, heated, and deflected — so the model does not reach the heliosheath even
  though its argument range formally would. The docstring states the same limit itself, "Application is
  primarily for the solar wind", and its worked example spans 0.1 → 1.0 au. Nothing else in the
  package models shocked or subsonic heliosheath plasma, and the physics that dominates that region is
  absent: searching `src/` and `docs/` (`.py`, `.rst`, `.md`, and notebook source cells) at this
  revision for `heliosheath`, `heliopause`, `termination shock`, `pickup ion`, `outer heliosphere`, and
  `Voyager` returns no match. Two `interstellar` matches do exist, but the interstellar medium lies
  beyond the heliosheath rather than in it, and both are parameter-regime illustrations rather than
  models: `src/plasmapy/formulary/lengths.py:236` mentions the gyroradius of a cosmic ray in the
  interstellar medium, and `docs/notebooks/formulary/iter.ipynb` plots the interstellar medium beside
  the solar corona and the solar wind at 1 au on a plasma-parameter comparison. The heliocentric range
  `temp_ratio` genuinely spans is already carried by the selected `Interplanetary Space`. If a future
  release adds termination-shock or pickup-ion physics, this is the note to revisit.
- Laboratory and fusion-device applications (LAPD, tokamaks, ITER, laser-produced plasmas) are a
  large part of PlasmaPy's user base but have no corresponding HSSI region; they are represented
  through Keywords (Field 16) instead.

*Coverage of the controlled vocabulary.* Every unselected Region value is accounted for in the list
just given —
`Earth Ionosphere`, `Earth Thermosphere`, `Earth Auroral Subregion`, `Earth Atmosphere`,
`Earth Lower and Middle Atmosphere`, `Earth Magnetosheath`, `Earth Inner Magnetosphere`,
`Earth Outer Magnetosphere`, `Earth Magnetotail`, `Solar Interior`, `Heliosheath`,
`Planetary Magnetospheres`, and the five per-planet magnetosphere rows. The field's length is
therefore a conclusion about PlasmaPy rather than an unfinished search. Re-read the live controlled
vocabulary during a future refresh so newly introduced values receive the same consideration.

### 6. Authors (MANDATORY)

> **`PlasmaPy Community` identifier — intentionally retained.** The organizational author
> `PlasmaPy Community` (author 1) stores
> `https://github.com/PlasmaPy/PlasmaPy/blob/main/CITATION.cff` in its author-identifier field. That is a
> source pointer rather than an ORCID/ROR-style entity identifier, and therefore not the cleanest
> semantic use of the field. **It is deliberately kept.** It provides useful authoritative provenance for
> this community author, and preserving it under HSSI's current Person-shaped representation of
> organizational authors is the settled preference. A future audit must **not** re-propose removing it.
>
> Supporting facts for that decision: PlasmaPy is not a legal entity with a ROR, so no entity identifier
> exists to substitute; SunPy's equivalent community author is represented the same way, carrying its own
> `https://github.com/sunpy/sunpy/blob/main/CITATION.cff` in the identifier field, so this is an
> established convention for community authors rather than a one-off defect; and the rule that this
> field carries an ORCID applies to human authors, which this record is not.
>
> **Three authors here are also credited by other software under different name forms**, and this
> project's entries are the canonical form in each case: Tien Vo, Pey Lian Lim and Andrew J. Leonard.
> Recorded so a later refresh recognises the variants — "P. L. Lim" in CDFlib and
> sunkit-image, "Drew Leonard" in sunkit-instruments, `Tien 'Vo` in PySPEDAS — instead of treating them
> as separate people.

`CITATION.cff` at the pinned revision lists **163** author entries, up from 157 at the `v2026.2.0`
tag. The recommended group attribution is **PlasmaPy Community**, listed first, whose author
identifier points at the authoritative contributor roster.

> **The full roster is the chosen representation.** Reducing the author list to the single
> **PlasmaPy Community** group entry — with
> https://github.com/PlasmaPy/PlasmaPy/blob/main/CITATION.cff as its author identifier — was
> considered and **not adopted**. Doing so would discard the 152 individually attributed contributors
> listed below along with their ORCIDs and affiliations, which is exactly the comprehensiveness this
> record exists to hold, and it would erase the attribution HSSI already stores. `PlasmaPy Community`
> is kept as the first author for two reasons that do not require collapsing anything: it is the group
> attribution `CITATION.cff` itself recommends, and it is where the thirteen entries that cannot be
> represented as an HSSI Person are folded (see below). It is an addition to the roster, not a
> substitute for it.

> **Folded contributors.** Of the 163 `CITATION.cff` entries, 149 carry both a given name and a
> family name, 12 are bare GitHub handles with no personal name, and 2 are mononyms. Thirteen of
> those cannot be represented as an HSSI Person and are folded into **PlasmaPy Community**: the
> eleven handles `BH4`, `Bzero`, `CBrown345`, `cicciope`, `flaixman`, `itsraashi`, `lgoenner`,
> `nrb1234`, `Physics-is-awesome`, `seanjunheng2`, and `WineDarkMoon`, plus the mononyms `Oscar`
> (alias `0scvr`) and `Zaid` (alias `zaid646`). Mononyms are folded rather than stored because
> HSSI's author serializer rejects the entire authors field when a stored `givenName`/`familyName`
> pair is incomplete, so a single-name Person is not a safe representation.
>
> One handle that looks like it belongs on that list does **not**: `CITATION.cff`'s bare
> `- alias: sandshrew118` entry is GitHub user `sandshrew118`, whose profile name is **Andrew
> Sandeman**, and who appears in the git history as `Andrew <apsandeman@gmail.com>`. HSSI's named
> Person "Andrew Sandeman" is that contributor. Recording this here so a future agent does not
> mistake Andrew Sandeman for an unmatched legacy row and does not add `sandshrew118` a second time
> as a folded handle.

**Author list (153 entries): PlasmaPy Community + 150 `CITATION.cff` contributors (the 149 entries
carrying a given and family name, plus Andrew Sandeman, whose `CITATION.cff` entry is the bare alias
`sandshrew118`) + 2 contributors retained from the original HSSI record (Anthony Vo and Frank
Silva).**

- **Author:** PlasmaPy Community
  - *Author Identifier:* https://github.com/PlasmaPy/PlasmaPy/blob/main/CITATION.cff

- **Author:** Nicholas A. Murphy
  - *Author Identifier:* https://orcid.org/0000-0001-6628-8033
  - *Affiliation:* Center for Astrophysics Harvard & Smithsonian — https://ror.org/03c3r2d17
  - *Affiliation:* Smithsonian Astrophysical Observatory — https://ror.org/04mh52z70
  - *Affiliation:* Smithsonian Institution — https://ror.org/01pp8nd67

- **Author:** Erik Everson
  - *Author Identifier:* https://orcid.org/0000-0001-6079-8307
  - *Affiliation:* University of California, Los Angeles — https://ror.org/046rm7j60

- **Author:** Dominik Stańczak
  - *Author Identifier:* https://orcid.org/0000-0001-6291-8843
  - *Affiliation:* University of Warsaw — https://ror.org/039bjqg32

- **Author:** Peter Heuer
  - *Author Identifier:* https://orcid.org/0000-0001-5050-6606
  - *Affiliation:* University of Rochester — https://ror.org/022kthw22

- **Author:** Pawel M. Kozlowski
  - *Author Identifier:* https://orcid.org/0000-0001-6849-3612
  - *Affiliation:* West Virginia University — https://ror.org/011vxgd24
  - *Affiliation:* Los Alamos National Laboratory — https://ror.org/01e41cf67

- **Author:** Elliot Johnson
  - *Affiliation:* University of Delaware — https://ror.org/01sbq1a82

- **Author:** Ritiek Malhotra
  - *Affiliation:* Chandigarh University — https://ror.org/05t4pvx35

- **Author:** David Schaffner
  - *Author Identifier:* https://orcid.org/0000-0002-9180-6565
  - *Affiliation:* Bryn Mawr College — https://ror.org/05sjwtp51

- **Author:** Steve Vincena
  - *Author Identifier:* https://orcid.org/0000-0002-6468-5710
  - *Affiliation:* University of California, Los Angeles — https://ror.org/046rm7j60

- **Author:** Mel Abler
  - *Author Identifier:* https://orcid.org/0000-0003-2528-8752

- **Author:** James Addison

- **Author:** Paula Valentina Alarcon
  - *Author Identifier:* https://orcid.org/0000-0002-7860-9567
  - *Affiliation:* North Carolina State University — https://ror.org/04tj63d06

- **Author:** Benjamin Antognetti
  - *Author Identifier:* https://orcid.org/0000-0002-1444-9680
  - *Affiliation:* University of Wisconsin–Madison — https://ror.org/01y2jtd41

- **Author:** Ataf Fazledin Ahamed
  - *Affiliation:* OpenRefactory Inc.

- **Author:** Christoper Arran
  - *Author Identifier:* https://orcid.org/0000-0002-8644-8118
  - *Affiliation:* University of York — https://ror.org/04m01e293

- **Author:** Haman Bagherianlemraski
  - *Author Identifier:* https://orcid.org/0000-0001-7381-1996
  - *Affiliation:* University of Massachusetts Amherst — https://ror.org/0072zz521

- **Author:** Jasper P. Beckers
  - *Affiliation:* ASML (United States) — https://ror.org/00gtpjy03

- **Author:** Manas Satish Bedmutha

- **Author:** Camilo Bedoya-Lopez

- **Author:** Justin Bergeron

- **Author:** Ludovico Bessi

- **Author:** Riley Britten

- **Author:** Shane Brown
  - *Author Identifier:* https://orcid.org/0000-0003-3309-3939
  - *Affiliation:* University of Delaware — https://ror.org/01sbq1a82

- **Author:** Khalil Bryant
  - *Author Identifier:* https://orcid.org/0000-0002-2105-0280
  - *Affiliation:* University of Michigan — https://ror.org/00jmfr291

- **Author:** Sean Carroll

- **Author:** Carlos Cartagena-Sanchez
  - *Author Identifier:* https://orcid.org/0000-0002-0486-1292
  - *Affiliation:* Beloit College — https://ror.org/009yr1d55

- **Author:** Sarthak Choudhary

- **Author:** Christian Clauss

- **Author:** Sean Chambers

- **Author:** Ankur Chattopadhyay

- **Author:** Apoorv Choubey

- **Author:** Sebastian Colom
  - *Author Identifier:* https://orcid.org/0009-0006-0863-0180
  - *Affiliation:* NASA Ames Research Center

- **Author:** Chase Davies

- **Author:** Jacob Deal

- **Author:** Gregor Decristoforo
  - *Author Identifier:* https://orcid.org/0000-0002-7616-0946
  - *Affiliation:* UiT The Arctic University of Norway — https://ror.org/00wge5k78

- **Author:** Diego Diaz

- **Author:** Fionnlagh Mackenzie Dover
  - *Author Identifier:* https://orcid.org/0000-0002-1984-7303
  - *Affiliation:* SP2RC, School of Mathematics and Statistics, University of Sheffield

- **Author:** David Drozdov

- **Author:** Tiger Du
  - *Author Identifier:* https://orcid.org/0000-0002-8676-1710
  - *Affiliation:* Vanderbilt University — https://ror.org/02vm5rt34

- **Author:** Leah Einhorn

- **Author:** Tamar Ervin
  - *Author Identifier:* https://orcid.org/0000-0002-8475-8606
  - *Affiliation:* University of California, Berkeley — https://ror.org/01an7q238

- **Author:** Thomas Fan
  - *Affiliation:* Quansight (United States) — https://ror.org/00zeq0353

- **Author:** Samaiyah I. Farid
  - *Author Identifier:* https://orcid.org/0000-0003-0223-7004
  - *Affiliation:* Center for Astrophysics Harvard & Smithsonian — https://ror.org/03c3r2d17
  - *Affiliation:* Yale University — https://ror.org/03v76x132

- **Author:** Emmanuel Ferdman
  - *Author Identifier:* https://orcid.org/0009-0004-8953-0151

- **Author:** Michael Fischer

- **Author:** Bryan Foo
  - *Author Identifier:* https://orcid.org/0000-0001-5308-6870
  - *Affiliation:* Massachusetts Institute of Technology — https://ror.org/042nb2s44

- **Author:** Heinz-Alexander Fütterer
  - *Author Identifier:* https://orcid.org/0000-0003-4397-027X

- **Author:** Rajagopalan Gangadharan

- **Author:** Seth Gerow
  - *Author Identifier:* https://orcid.org/0009-0008-3588-0497
  - *Affiliation:* Embry-Riddle Aeronautical University — https://ror.org/010jskt71
    - *Note:* The identity of this affiliation is carried by the ROR, not by the spelling. The
      hyphen-minus form recorded here is the institution's own official usage: erau.edu titles
      itself `Embry-Riddle Aeronautical University` with a plain hyphen, which predominates
      across the site; the remaining occurrences there use a non-breaking hyphen (U+2011), and
      none use an en dash. ROR's display name renders the same institution with an en dash
      (`Embry–Riddle Aeronautical University`, U+2013), which is registry typography rather than
      a different name, and is deliberately not adopted here. Do not "correct" the hyphen to an
      en dash.

- **Author:** Mahlet Getahun
  - *Affiliation:* Marietta College — https://ror.org/03apb0g70

- **Author:** Jessica Gonzalez
  - *Affiliation:* California Institute of Technology — https://ror.org/05dxps055

- **Author:** Brian Goodall

- **Author:** Shauna Gordon-McKeon
  - *Author Identifier:* https://orcid.org/0000-0002-2373-8927

- **Author:** Marco Gorelli

- **Author:** Graham Goudeau

- **Author:** Silvina Guidoni
  - *Author Identifier:* https://orcid.org/0000-0003-1439-4218
  - *Affiliation:* American University — https://ror.org/052w4zt36

- **Author:** Julia Guimiot

- **Author:** Colby C. Haggerty
  - *Author Identifier:* https://orcid.org/0000-0002-2160-7288
  - *Affiliation:* University of Chicago — https://ror.org/024mw5h28
  - *Affiliation:* University of Hawaii at Manoa — https://ror.org/01wspgy28

- **Author:** Raymon Skjørten Hansen

- **Author:** Mohammed Haque
  - *Affiliation:* Columbia University — https://ror.org/00hj8s172

- **Author:** Julien Hillairet
  - *Author Identifier:* https://orcid.org/0000-0002-1073-6383
  - *Affiliation:* Commissariat à l'Énergie Atomique et aux Énergies Alternatives — https://ror.org/00jjx8s55

- **Author:** Chris Hoang

- **Author:** Poh Zi How

- **Author:** Yi-Min Huang
  - *Author Identifier:* https://orcid.org/0000-0002-4237-2211
  - *Affiliation:* Princeton University — https://ror.org/00hx57361

- **Author:** Nabil Humphrey
  - *Author Identifier:* https://orcid.org/0000-0002-4227-2544

- **Author:** Maria Isupova

- **Author:** Alexis Jeandet
  - *Author Identifier:* https://orcid.org/0000-0003-2892-6924
  - *Affiliation:* Laboratory of Plasma Physics (LPP/CNRS) — https://ror.org/05c95bg36

- **Author:** Evan Jones
  - *Author Identifier:* https://orcid.org/0009-0004-6699-4869

- **Author:** Marcin Kastek
  - *Author Identifier:* https://orcid.org/0009-0002-5918-4652
  - *Affiliation:* Institute of Plasma Physics and Laser Microfusion — https://ror.org/0452jaa17

- **Author:** James Kent

- **Author:** Dusan Klima
  - *Author Identifier:* https://orcid.org/0009-0008-5134-6171

- **Author:** Alf Köhn-Seemann
  - *Author Identifier:* https://orcid.org/0000-0002-1192-2057
  - *Affiliation:* University of Stuttgart — https://ror.org/04vnq7t77

- **Author:** Siddharth Kulshrestha

- **Author:** Sundaran Kumar

- **Author:** Piotr Kuszaj

- **Author:** Samuel J. Langendorf
  - *Author Identifier:* https://orcid.org/0000-0002-7757-5879
  - *Affiliation:* Los Alamos National Laboratory — https://ror.org/01e41cf67

- **Author:** Anna Lanteri

- **Author:** Terrance Takho Lee

- **Author:** Andrew J. Leonard
  - *Author Identifier:* https://orcid.org/0000-0001-5270-7487
  - *Affiliation:* Aperio Software Ltd.

- **Author:** Nicolas Lequette
  - *Affiliation:* Laboratory of Plasma Physics (LPP/CNRS) — https://ror.org/05c95bg36

- **Author:** Pey Lian Lim
  - *Author Identifier:* https://orcid.org/0000-0003-0079-4114
  - *Affiliation:* Space Telescope Science Institute — https://ror.org/036f5mx38

- **Author:** Aditya Magarde

- **Author:** Joao Victor Martinelli

- **Author:** Muhammad Masood
  - *Affiliation:* University of Edinburgh — https://ror.org/01nrxwf90

- **Author:** Isaias McHardy
  - *Author Identifier:* https://orcid.org/0000-0001-5394-9445

- **Author:** Dhawal Modi

- **Author:** Kevin Montes
  - *Author Identifier:* https://orcid.org/0000-0002-0762-3708
  - *Affiliation:* Massachusetts Institute of Technology — https://ror.org/042nb2s44

- **Author:** Stuart J. Mumford
  - *Author Identifier:* https://orcid.org/0000-0003-4217-4642
  - *Affiliation:* Aperio Software Ltd.
  - *Affiliation:* University of Sheffield — https://ror.org/05krs5044

- **Author:** Joshua Munn

- **Author:** Leo Murphy
  - *Affiliation:* William & Mary — https://ror.org/03hsf0573

- **Author:** Bao Nguyen
  - *Author Identifier:* https://orcid.org/0000-0002-1753-4223
  - *Affiliation:* Imperial College London — https://ror.org/041kmwe10

- **Author:** Suzanne Nie

- **Author:** Carlos Ortiz
  - *Affiliation:* University of Wisconsin–Madison — https://ror.org/01y2jtd41

- **Author:** Shivam Panda

- **Author:** Mahima Pannala

- **Author:** Tulasi Parashar
  - *Author Identifier:* https://orcid.org/0000-0003-0602-8381
  - *Affiliation:* University of Delaware — https://ror.org/01sbq1a82
  - *Affiliation:* Victoria University of Wellington — https://ror.org/0040r6f76

- **Author:** Neil Patel

- **Author:** Francisco Silva Pavon

- **Author:** Roberto Díaz Pérez

- **Author:** Preston Pitzer
  - *Author Identifier:* https://orcid.org/0009-0007-0655-1347
  - *Affiliation:* Virginia Tech — https://ror.org/02smfhw86

- **Author:** Jakub Polak

- **Author:** Ramiz Qudsi
  - *Author Identifier:* https://orcid.org/0000-0001-8358-0482
  - *Affiliation:* Boston University — https://ror.org/05qwgg493

- **Author:** Raajit Raj

- **Author:** Vishwas Rajashekar
  - *Author Identifier:* https://orcid.org/0000-0002-4914-6612
  - *Affiliation:* PES University — https://ror.org/05m169e78

- **Author:** Afzal Rao

- **Author:** Jeffrey Reep
  - *Author Identifier:* https://orcid.org/0000-0003-4739-1152
  - *Affiliation:* University of Hawaii at Manoa — https://ror.org/01wspgy28

- **Author:** Steve Richardson
  - *Author Identifier:* https://orcid.org/0000-0002-3056-6334
  - *Affiliation:* United States Naval Research Laboratory — https://ror.org/04d23a975

- **Author:** Jayden Roberts
  - *Author Identifier:* https://orcid.org/0009-0009-9490-5284

- **Author:** Shanshan Rodriguez
  - *Author Identifier:* https://orcid.org/0000-0003-2944-0424
  - *Affiliation:* Grinnell College — https://ror.org/04tmmky42

- **Author:** Reynaldo Rojas Zelaya

- **Author:** Armando Salcido

- **Author:** Andrew Sandeman

- **Author:** Antonia Savcheva
  - *Author Identifier:* https://orcid.org/0000-0002-5598-046X
  - *Affiliation:* Center for Astrophysics Harvard & Smithsonian — https://ror.org/03c3r2d17

- **Author:** Cora Schneck

- **Author:** Chengcai Shen
  - *Author Identifier:* https://orcid.org/0000-0002-9258-4490
  - *Affiliation:* Center for Astrophysics Harvard & Smithsonian — https://ror.org/03c3r2d17

- **Author:** Andrew Sheng

- **Author:** Dawa Nurbu Sherpa

- **Author:** Luciano Silvestri
  - *Author Identifier:* https://orcid.org/0000-0003-3530-7910
  - *Affiliation:* Michigan State University — https://ror.org/05hs6h993

- **Author:** Trestan F. Simon
  - *Author Identifier:* https://orcid.org/0009-0000-3029-8619

- **Author:** Angad Singh

- **Author:** Ankit Singh

- **Author:** Brigitta Sipőcz
  - *Author Identifier:* https://orcid.org/0000-0002-3713-6337
  - *Affiliation:* DIRAC Institute, University of Washington
  - *Affiliation:* Infrared Processing and Analysis Center — https://ror.org/05q79g396

- **Author:** Cody Skinner
  - *Affiliation:* Phoenix Security Labs

- **Author:** Tomasz Adam Skrzypczak

- **Author:** Nikita Smirnov

- **Author:** Joseph Smith
  - *Author Identifier:* https://orcid.org/0000-0002-5978-6840
  - *Affiliation:* Marietta College — https://ror.org/03apb0g70

- **Author:** Stuart Sobeske
  - *Affiliation:* University of Michigan — https://ror.org/00jmfr291

- **Author:** Matteo Spedicato

- **Author:** David Stansby
  - *Author Identifier:* https://orcid.org/0000-0002-1365-1908
  - *Affiliation:* Advanced Research Computing Centre, University College London, UK
  - *Affiliation:* Department of Mechanical Engineering, University College London
  - *Affiliation:* Imperial College London — https://ror.org/041kmwe10
  - *Affiliation:* Mullard Space Science Laboratory, University College London
  - *Affiliation:* University College London — https://ror.org/02jx3x895

- **Author:** Tomás Stinson

- **Author:** Shelley Sugiharto
  - *Author Identifier:* https://orcid.org/0009-0003-3159-0541
  - *Affiliation:* Texas A&M University — https://ror.org/01f5ytq51

- **Author:** Michaela Švancarová

- **Author:** Antoine Tavant
  - *Author Identifier:* https://orcid.org/0000-0003-0010-8073
  - *Affiliation:* Laboratory of Plasma Physics (LPP/CNRS) — https://ror.org/05c95bg36
  - *Affiliation:* Centre Spatial de l'École Polytechnique

- **Author:** Veronica Tranquilino
  - *Affiliation:* University of Michigan — https://ror.org/00jmfr291

- **Author:** Thomas Ulrich

- **Author:** Mychal Valle
  - *Author Identifier:* https://orcid.org/0000-0003-4230-6916
  - *Affiliation:* University of California, Los Angeles — https://ror.org/046rm7j60

- **Author:** Thomas Varnish
  - *Author Identifier:* https://orcid.org/0000-0002-8078-214X
  - *Affiliation:* Massachusetts Institute of Technology — https://ror.org/042nb2s44

- **Author:** Tien Vo
  - *Author Identifier:* https://orcid.org/0000-0002-8335-1441
  - *Affiliation:* Laboratory for Atmospheric and Space Physics — https://ror.org/01fcjzv38

- **Author:** Tingfeng Wu
  - *Author Identifier:* https://orcid.org/0000-0001-8745-204X

- **Author:** Sixue Xu
  - *Author Identifier:* https://orcid.org/0000-0001-7959-8495
  - *Affiliation:* University of California, Los Angeles — https://ror.org/046rm7j60

- **Author:** Chun Hei Yip

- **Author:** Carol Zhang

- **Author:** Clément Robert
  - *Author Identifier:* https://orcid.org/0000-0001-8629-7068

- **Author:** Shawn Polson
  - *Author Identifier:* https://orcid.org/0000-0003-0619-5745
  - *Affiliation:* Laboratory for Atmospheric and Space Physics — https://ror.org/01fcjzv38

- **Author:** Yaocheng Chen
  - *Author Identifier:* https://orcid.org/0000-0002-8967-4911
  - *Affiliation:* Korea Astronomy and Space Science Institute — https://ror.org/04g2pxh42
  - *Affiliation:* Universidade de São Paulo — https://ror.org/036rp1748
    - *Note:* Both affiliations are kept because this author's affiliation set is unioned with
      the stored shared record, which is this field's stated convention. ORCID corroborates both
      employments — Korea Astronomy and Space Science Institute through June 2026, and
      Universidade de São Paulo (which ORCID lists under its English name) from July 2026 — so
      they are consecutive and current, not a duplicate or a stale leftover. The shared Person
      record is linked to more than one software entry, so both affiliations appear wherever
      that person is credited.

- **Author:** Anthony Vo

- **Author:** Frank Silva

- **Author:** Sean Clark
  - *Author Identifier:* https://orcid.org/0009-0004-5738-5359

- **Author:** Vaibhav Mehta
  - *Author Identifier:* https://orcid.org/0000-0003-2357-3023
  - *Affiliation:* Cornell University — https://ror.org/05bnh6r87

- **Author:** John Bonner
  - *Affiliation:* Haverford College — https://ror.org/04fnrxr62

- **Author:** Mohit Arvind Khakharia

- **Author:** Mike German


*Source: the stored HSSI record reconciled by identity-aware union against `CITATION.cff` at the
pinned revision. Author identity was matched on ORCID first and normalized name second; affiliations
were unioned per author. Names appear as HSSI stores them (see the divergence note below); ROR
identifiers are shown after an em dash where one is stored or was newly resolved.*

**Corrections to previously recorded values** (what the value was, what it is now, and why):

- **Nicholas A. Murphy, Samaiyah I. Farid, Antonia Savcheva, Chengcai Shen** — the affiliation was
  previously written `Center for Astrophysics, Harvard & Smithsonian` (with a comma). The stored
  value is `Center for Astrophysics Harvard & Smithsonian` with ROR `https://ror.org/03c3r2d17`, and
  that is what is recorded now. The comma form is not the stored string; the institution's own
  styling uses a vertical bar (`Center for Astrophysics | Harvard & Smithsonian`, as `CITATION.cff`
  writes it), which the stored row renders without punctuation. Because HSSI resolves organizations
  by exact name, the comma form would have created a duplicate organization row.
- **Stuart J. Mumford** — three affiliations were previously recorded, one of which was the bare
  string `https://orcid.org/0000-0001-5270-7487`. That is an ORCID, and it belongs to **Andrew J.
  Leonard**, not to any organization. It was a data defect and has been removed. The two genuine
  affiliations are `Aperio Software Ltd.` and `University of Sheffield`
  (`https://ror.org/05krs5044`), which is exactly what HSSI stores.
- **David Stansby** — four affiliations were previously recorded; the stored record has five. The
  missing one, `Mullard Space Science Laboratory, University College London`, is restored.
- **Steve Richardson** — the affiliation was previously written `U.S. Naval Research Laboratory`. The
  stored value is `United States Naval Research Laboratory` (`https://ror.org/04d23a975`), which is
  also the acronym-expanded form this metadata calls for, and is what is recorded now.
- **Nicolas Lequette and Antoine Tavant** — Lequette's affiliation was previously written
  `Laboratoire de Physique des Plasmas`, and Tavant's `Laboratoire de Physique des Plasmas, Ecole
  Polytechnique`. Both name one and the same laboratory: LPP (UMR 7648) in Palaiseau, registered
  under `https://ror.org/05c95bg36`. That ROR record carries `Laboratoire de Physique des
  Plasmas` as its display name, `Laboratory of Plasma Physics` as its English alias, the acronyms
  `LPP` and `LPTP`, and `UMR 7648`; it lists CNRS (`https://ror.org/02feahw73`) and École
  Polytechnique (`https://ror.org/05hy3tk52`) among its parents, which is why both of the earlier
  spellings resolve to this single laboratory. Both authors are therefore recorded under the
  identifier-bearing name `Laboratory of Plasma Physics (LPP/CNRS)`, matching what this record
  already carries for Alexis Jeandet. `CITATION.cff` still writes the French display name; adopting
  it, or the `, Ecole Polytechnique` variant, would split one laboratory across identifierless
  organization rows alongside the ROR-backed one, and should not be proposed.
- **Antoine Tavant's second affiliation stands on its own.** `Centre Spatial de l'École
  Polytechnique` is a different organization from LPP — an École Polytechnique space centre
  rather than the plasma-physics laboratory — and Tavant genuinely holds both. It is recorded
  alongside LPP and must not be folded into it on the strength of the shared École Polytechnique
  parentage.

**Known divergence between HSSI and `CITATION.cff` that cannot be fixed by a metadata update.** For
four contributors, `CITATION.cff` gives a fuller or more current name than HSSI stores:

| Stored in HSSI (recorded above) | `CITATION.cff` at this revision |
|---|---|
| Erik Everson | Erik T. Everson |
| Dominik Stańczak | Dominik Stańczak-Marikin |
| Peter Heuer | Peter V. Heuer |
| Diego Diaz | Diego A. Diaz Riega |

The upstream names are the more correct ones. They are **not** recorded as the field value because
HSSI's API cannot rename an existing Person: a metadata update that supplies a different
`givenName`/`familyName` for an already-linked ORCID silently no-ops rather than renaming, so
proposing a rename would produce a diff that can never be applied. Correcting these requires a
direct database change by an HSSI administrator, outside the submission and update APIs. A future
agent should not re-propose these as achievable field changes. Note that the divergence runs both
ways — HSSI stores the fuller form for Nicholas A. Murphy, Jasper P. Beckers, Manas Satish Bedmutha,
Samuel J. Langendorf, Trestan F. Simon, and Colby C. Haggerty, where `CITATION.cff` currently gives
the shorter one — so this is a difference in vintage rather than a systematic error on either side.

Two further name divergences of the same kind: `CITATION.cff` lists **Drew Leonard** where HSSI
stores **Andrew J. Leonard** (same ORCID `0000-0001-5270-7487`), and lists **Stuart Mumford** where
HSSI stores **Stuart J. Mumford** (same ORCID `0000-0003-4217-4642`).

**Affiliations newly added from `CITATION.cff`** (union, not replacement — the previously stored
affiliation is kept alongside, because an author's earlier institution remains a true attribution for
the work already contributed):

| Author | Added affiliation | ROR |
|---|---|---|
| Pawel M. Kozlowski | Los Alamos National Laboratory | https://ror.org/01e41cf67 |
| Thomas Fan | Quansight (United States) | https://ror.org/00zeq0353 |
| Samaiyah I. Farid | Yale University | https://ror.org/03v76x132 |
| Colby C. Haggerty | University of Hawaii at Manoa | https://ror.org/01wspgy28 |
| Julien Hillairet | Commissariat à l'Énergie Atomique et aux Énergies Alternatives | https://ror.org/00jjx8s55 |
| Tulasi Parashar | Victoria University of Wellington | https://ror.org/0040r6f76 |
| Vishwas Rajashekar | PES University | https://ror.org/05m169e78 |
| Antoine Tavant | Centre Spatial de l'École Polytechnique | *(none)* |
| Thomas Varnish | Massachusetts Institute of Technology | https://ror.org/042nb2s44 |

Notes on those additions: `CITATION.cff` abbreviates several of these (`CEA`, `MIT`, `UCLA`), and the
expanded institutional names above are used because HSSI asks for full names rather than acronyms.
`Quansight Labs` is the name `CITATION.cff` uses; ROR indexes only the parent company, so the ROR
display name `Quansight (United States)` is recorded — the same convention already used for
`ASML (United States)` in this record. `Colby C. Haggerty`'s new affiliation reuses HSSI's existing
`University of Hawaii at Manoa` row (already linked to Jeffrey Reep) rather than ROR's diacritic form
`University of Hawaiʻi at Mānoa`, so the two contributors share one organization row.
`Centre Spatial de l'École Polytechnique` has no ROR record; it is stored without an identifier, as
several other rows in this record already are.

HSSI stores affiliations on shared Person identities rather than on each Person–Software
relationship. These unioned affiliations therefore appear on every software entry linked to the same
Person. That is expected shared-person behavior, not evidence that another entry independently
asserted each affiliation, and is not a reason to remove one from PlasmaPy's author metadata.

**Authors newly added** — six entries were appended to `CITATION.cff` after the `v2026.2.0` tag. Five
have usable personal names and are recorded as Persons (Sean Clark, Vaibhav Mehta, John Bonner, Mohit
Arvind Khakharia, Mike German); the sixth, `Zaid`, is a mononym and is folded into PlasmaPy Community
for the reason given above.

**Considered and not selected:**

- *An ORCID for Elliot Johnson.* `CITATION.cff` gives Elliot Johnson the ORCID
  `0000-0003-2892-6924` — but that same ORCID is also assigned to **Alexis Jeandet** two dozen
  entries later in the same file. One of the two is wrong upstream, and HSSI's stored record already
  takes the safe reading: Alexis Jeandet keeps the ORCID and Elliot Johnson has none. That is left
  unchanged. Do not "fix" Elliot Johnson by copying this ORCID in.
- *Replacing `SP2RC, School of Mathematics and Statistics, University of Sheffield` for Fionnlagh
  Mackenzie Dover with the plainer `University of Sheffield` that `CITATION.cff` now gives.* The
  stored value is the same institution at finer granularity; adding the coarser name would duplicate
  the attribution without adding information.
- *Replacing David Stansby's, Brigitta Sipőcz's, Stuart J. Mumford's, Jeffrey Reep's, or Steve
  Richardson's stored affiliations with the single shorter one `CITATION.cff` now lists.* In each
  case the stored set is a superset or an expanded form of the upstream string.

**Durable limitation worth knowing.** `Bryn Mawr College`, `North Carolina State University`,
`University of Wisconsin–Madison`, `Beloit College` and `Marietta College` were previously stored
without an identifier. Their ROR is now attached to the shared organization row and is recorded
above, so none of them is an identifierless row any longer. Other rows in this record still hold no
identifier, among them `Aperio Software Ltd.` and `Centre Spatial de l'École Polytechnique`. The
constraint behind that is unchanged and is the part worth remembering: an identifier cannot be
backfilled onto an existing Organization row through a metadata update, because organization
attributes are not editable that way — only a direct change to the shared organization catalogue can
add one. Attaching a ROR to a row that still lacks one is therefore not an achievable improvement
from this record, and should not be proposed as one.

### 7. Software Name (MANDATORY)
PlasmaPy

*The project's own capitalisation, consistent across `CITATION.cff` (`title`), `README.md`,
`pyproject.toml` (distribution name `plasmapy`, lower-cased only as a PyPI convention), and the
Zenodo record title.*

### 8. Description (MANDATORY)
PlasmaPy is an open source, community-developed Python package for plasma research and education. It is intended to contain core functionality needed by plasma scientists across disciplines — analogous to what Astropy provides for astronomy. PlasmaPy provides object-oriented and functional interfaces for representing and accessing particle data (`plasmapy.particles`); a comprehensive `plasmapy.formulary` subpackage implementing many common plasma parameter formulas drawn from the NRL Plasma Formulary (frequencies, lengths, speeds, drifts, collisions, dielectric and dimensionless quantities, distribution functions, quantum and relativistic plasma physics); and the `plasmapy.dispersion` subpackage for analytical (Stix cold-plasma, MHD wave) and numerical (Hollweg, kinetic Alfvén) plasma dispersion relations and the plasma dispersion function. The `plasmapy.diagnostics` subpackage provides analysis routines for Thomson scattering, swept Langmuir probe characteristics, and synthetic charged particle (proton) radiography, while `plasmapy.analysis` provides utilities for fit functions, conditional averaging of time series, and 3D magnetic null point finding. The `plasmapy.simulation` subpackage offers a general particle tracker with Boris and relativistic Boris integrators, and `plasmapy.plasma` defines 1D and cylindrical MHD equilibria, generic plasma classes, and structured/unstructured Cartesian grids, including a reader for OpenPMD HDF5 files. PlasmaPy uses `astropy.units` extensively to enforce physical-unit correctness on all inputs and outputs.

*Unchanged from the stored record, which is consistent with `README.md`, the `CITATION.cff` abstract,
and the DataCite abstract for the version DOI. It is deliberately not rewritten: the wording is
accurate at this revision and rephrasing submitted prose for style is not an improvement. The one
thing a future refresh could legitimately add is the `plasmapy.formulary.fusion` module (fusion cross
sections and Maxwellian-averaged reactivities), which is on `main` but not in any release; that is
left out here so the description continues to describe released functionality.*

### 9. Concise Description (OPTIONAL)
PlasmaPy is an open source, community-developed Python package for plasma research and education, providing core particle, formulary, dispersion, diagnostics, and simulation functionality.

*Unchanged. Editorial wording that accurately summarises the package; no reason to restate it
differently.*

### 10. Publication Date (RECOMMENDED)
2018-04-29

*Date of the earliest release tag in the repository, `v0.1.0` (2018-04-29), which is the first
broadcast of the software and therefore what this field asks for. Deliberately **not** taken from
DataCite: the concept DOI's record reports publication year 2020 because it is pinned to a stale
`0.4.0` snapshot, and the version DOI's record reports 2026. Neither is the initial version.*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*DataCite reports `publisher: "Zenodo"` for both the concept DOI and the version DOI, and
`docs/about/citation.rst` states that all public releases are archived in the PlasmaPy Community on
Zenodo.*

### 12. Version (RECOMMENDED)
- **Version Number:** 2026.2.0
- **Version Date:** 2026-02-20
- **Version Description:** Latest stable release as recorded in CITATION.cff. See https://docs.plasmapy.org/en/stable/whatsnew/index.html for changelog.
- **Version PID:** https://doi.org/10.5281/zenodo.18706665

*`2026.2.0` is the latest release: it is the newest tag in the repository, GitHub's latest release
(not a prerelease, the previous being `v2025.10.0`), and the current PyPI version.*

**On the version date, which has two defensible-looking answers.** The repository and Zenodo both
assert **2026-02-20**: `CITATION.cff` has `date-released: '2026-02-20'`, `docs/about/citation.rst`
substitutes DOI `10.5281/zenodo.18706665`, and DataCite's record for that DOI carries
`{"date": "2026-02-20", "dateType": "Issued"}`. The competing figure — GitHub's release
`published_at` and PyPI's upload timestamp, both `2026-02-21T02:17Z` — is the same moment expressed
in UTC; 02:17 UTC on 21 February is the evening of 20 February in the United States, where the
release was cut. **2026-02-20 is the date the project itself asserts and is the value recorded.** A
future agent seeing `2026-02-21` in a GitHub or PyPI API response should not treat it as drift.

**The recorded version number is the bare `2026.2.0`.** HSSI's read API renders versions as
`PlasmaPy - 2026.2.0`, prefixing the software name for display. That rendered string is not the
stored value and must never be written into this file or into an update payload.

*The pinned source revision is 97 commits past this tag. That does not change this field: a version
is only advanced when a release is actually cut.*

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*`pyproject.toml` declares `requires-python = ">=3.12"` and classifiers for Python 3.12, 3.13, and
3.14. The package is pure Python — there is no build step for compiled extensions in
`[build-system]`, and no C, Cython, Fortran, or Rust sources under `src/`.*

### 14. Reference Publication (RECOMMENDED)
Not found

*PlasmaPy has no journal paper describing the software. `docs/about/citation.rst` is explicit that
the citation is the version-specific Zenodo record (see Field 12), and `docs/bibliography.bib`
contains no PlasmaPy self-citation. Two Zenodo DOIs that might be mistaken for one are grant
proposals, not publications — see Field 27.*

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

*`LICENSE.md` is the 3-clause BSD text; `pyproject.toml` declares `license-files = [ "LICENSE.md" ]`;
`CITATION.cff` gives `license: BSD-3-Clause`; GitHub reports SPDX `BSD-3-Clause`; and DataCite's
record for the version DOI carries `rightsIdentifier: bsd-3-clause`. The recorded name matches
HSSI's `License` vocabulary row exactly, including the curly-free straight double quotes.*

*Related but separate: `PATENT.md` adds a patent-retaliation clause on top of the BSD licence. It is
not itself a licence and has no HSSI vocabulary row, so it is not represented in this field.*

*Do not derive this field from the **concept** DOI's DataCite record, which reports
`Other (Open)` — a stale artifact of the 2020 snapshot that record is pinned to.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- Astronomy
- Astrophysics
- Atomic Physics
- Fusion
- Heliophysics
- High-Energy-Density Physics
- Langmuir Probes
- Magnetic Flux Ropes
- Magnetic Reconnection
- Magnetohydrodynamics
- Open Source
- Open Source Software
- Particles
- Physics
- Plasma
- Plasma Astrophysics
- Plasma Diagnostics
- Plasma Parameters
- Plasma Physics
- Plasma Science
- Proton Radiography
- Python
- Science
- Solar Physics
- Space Physics
- Space Plasmas
- Thomson Scattering

*Twenty-four keywords are carried over from the stored record, corroborated by `pyproject.toml`
keywords, DataCite subjects for the version DOI, and GitHub repository topics (`astronomy`,
`astrophysics`, `atomic-physics`, `fusion`, `hedp`, `heliophysics`,
`high-energy-density-physics`, `particles`, `plasma-physics`, `plasma-science`, `python`, `science`,
`solar`, `space-physics`, `space-plasma-physics`). Keywords are stored lower-case and rendered in
title case, so casing differences between this file and an API response are display artifacts, not
drift.*

*Three additional keywords are supported by current repository evidence:*

- **Magnetohydrodynamics** — `plasmapy.dispersion.analytical.mhd_waves_`,
  `plasmapy.plasma.equilibria1d`, and `plasmapy.plasma.cylindrical_equilibria`; `README.md` itself
  invites "puns about computational magnetohydrodynamics".
- **Magnetic Reconnection** — `plasmapy.analysis.nullpoint` (3D magnetic null finding),
  `docs/notebooks/formulary/magnetosphere.ipynb` (reconnection parameters), and DOE award
  DE-SC0016363, "The Evolution of Magnetic Skeletons During 3D Magnetic Reconnection", recorded in
  Field 26.
- **Magnetic Flux Ropes** — `plasmapy.plasma.cylindrical_equilibria.ForceFreeFluxRope`, the analytic
  Lundquist force-free flux rope solution.

*Considered and not selected: `plasma instabilities` (the NSF proposal describes a solver for waves
**and instabilities**, but only the wave solvers are implemented at this revision); `particle
distributions` and `particle moments` (covered by the stored `Particles` and by Field 4); `solar
wind` (now carried more precisely by Fields 5 and 22); `fusion energy` (a DataCite subject, but the
stored `Fusion` row already covers it and a second row would be a near-duplicate).*

### 17. Data Sources (OPTIONAL)
- Other
- HTTP/HTTPS Directories

*`Other` is carried over and remains correct: PlasmaPy is not primarily a data-access tool, and in
normal use the analysis routines operate on arrays and files the user supplies.*

*`HTTP/HTTPS Directories` is added because `plasmapy.utils.data.Downloader` — public API, not a build
step — retrieves resource and sample-data files over HTTPS from
`https://raw.githubusercontent.com/PlasmaPy/PlasmaPy-data/main/`, listing the available files through
`https://api.github.com/repos/PlasmaPy/PlasmaPy-data/contents/`. That is retrieval from an
HTTPS-served file directory, which is exactly what this vocabulary row describes.*

*Considered and not selected: `Observatory/Mission-specific`, `CDAWeb`, `HAPI`, `AMDA`, `SSCWeb`,
`OMNIWeb`, `Madrigal`, `The Virtual Solar Observatory.`, `VirES`, `TAP`, `das2`, `GFZ`, `WDC`,
`FTP/FTPS Directories`, `S3/Cloud-aware` — the package contains no client for any archive, protocol,
or mission-specific source. Enumerating them here is the reason the field is correctly this short:
the emptiness is a fact about PlasmaPy, not an unfinished search.*

### 18. Input File Formats (RECOMMENDED)
- HDF5
- JSON

*HDF5 is carried over: `plasmapy.plasma.sources.openpmd_hdf5.HDF5Reader` reads HDF5 files following
the OpenPMD standard (raising a dedicated exception when a file is not OpenPMD-conformant),
`plasmapy.diagnostics.charged_particle_radiography.synthetic_radiography` reads saved radiography
runs back from HDF5, and `plasmapy.particles.atomic` reads NIST ionization-energy data from a
bundled HDF5 file.*

*JSON is added: `plasmapy.particles` publicly exports `ParticleJSONDecoder`, `json_load_particle`,
and `json_loads_particle`, which reconstruct `Particle` objects from a JSON file object or string.
This is a user-facing deserialization path, not internal configuration.*

*Considered and not selected: NumPy `.npy` — the sample Langmuir traces shipped under
`docs/notebooks/langmuir_samples/` are `.npy` files, but they are loaded by `numpy.load` in the
notebooks rather than by any PlasmaPy reader, and `.npy` has no HSSI `FileFormat` row (recording
`Other` for it would be less informative than omitting it). No CDF, FITS, netCDF, IDL save, Zarr,
CSV, or plain-ASCII reader exists in the package.*

### 19. Output File Formats (RECOMMENDED)
- HDF5
- JSON

*HDF5 is carried over: `plasmapy.simulation.particle_tracker.save_routines` and
`plasmapy.diagnostics.charged_particle_radiography.synthetic_radiography` both open output files with
`h5py.File(path, "w")`.*

*JSON is added: `Particle.json_dump(fp)` writes a particle to a file object and `Particle.json_dumps()`
returns the JSON string, the write side of the serialization round trip described in Field 18.*

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

*The GitHub Actions workflows run the test and installability matrices on `ubuntu-latest`,
`macos-latest`, and `windows-latest`. `pyproject.toml` additionally declares the classifier
`Operating System :: OS Independent`.*

*Considered and not selected: the vocabulary row `Operating System Independent`. The three specific
platforms are what CI actually exercises and are the more useful search facets; adding the
catch-all alongside them would add no information. `Solaris` and `MobilePlatform` have no supporting
evidence.*

### 21. CPU Architecture (RECOMMENDED)
- Apple Silicon arm64
- x86-64

*GitHub-hosted `macos-latest` runners are Apple Silicon arm64, and the default `ubuntu-latest` and
`windows-latest` runners are x86-64; those are the architectures the CI matrix actually exercises.*

*Considered and not selected: `CPU Independent`. PlasmaPy is pure Python and imposes no architecture
constraint of its own, which makes that row tempting — but its dependency set (NumPy, SciPy, h5py,
matplotlib) is distributed as compiled wheels, so practical availability is bounded by those
projects' wheel coverage rather than by PlasmaPy. Recording the two tested architectures is the more
defensible claim. `GPU` and `HPC or HEC` have no supporting evidence: there is no CUDA, CuPy,
`mpi4py`, or job-scheduler integration in the package.*

### 22. Related Phenomena (OPTIONAL)
- Solar Wind
- Coronal Mass Ejections

*This field was previously "Not found". Two values are added on direct repository evidence:*

- **Solar Wind** — `plasmapy.formulary.collisions.helio.collisional_analysis.temp_ratio` predicts the
  ion temperature ratio for a plasma in transit between two heliocentric distances, with the
  docstring stating "Application is primarily for the solar wind", following Maruca (2013) and
  Johnson (2023). This is a dedicated, phenomenon-specific capability rather than an application
  note.
- **Coronal Mass Ejections** — `plasmapy.plasma.cylindrical_equilibria.ForceFreeFluxRope` implements
  the Lundquist (1950) force-free solution, documented as "often used to approximate the magnetic
  structure of interplanetary coronal mass ejections (ICMEs)"; `docs/notebooks/particles/ace.ipynb`
  is a worked example of ICME ionization states.

**Considered and not selected:**

- *X-ray emission* — `plasmapy.formulary.radiation.thermal_bremsstrahlung` looks like a match, but its
  docstring restricts it to the Rayleigh–Jeans limit (ℏω ≪ k_BT_e), i.e. the low-frequency end of the
  bremsstrahlung spectrum. It does not model X-ray bremsstrahlung and should not be cited for this
  value.
- *Solar Flares*, *Coronal Heating*, *Geomagnetic Storms*, *Solar Corona* — these appear only as
  motivating prose in documentation (for example `docs/notebooks/formulary/magnetosphere.ipynb`
  noting that reconnection powers solar flares and contributes to geomagnetic storms). No code path
  is specific to any of them.

Every unselected Phenomena value is enumerated above, so this field's shortness is a conclusion about
PlasmaPy rather than an incomplete search. Re-read the live controlled vocabulary during a future
refresh so newly introduced values receive the same consideration.

### 23. Development Status (RECOMMENDED)
Active

*97 commits merged between the `v2026.2.0` tag and the pinned revision, including new functionality
(`plasmapy.formulary.fusion`); GitHub reports the repository as not archived with a push on
2026-08-06; releases are cadenced (v2025.8.0, v2025.10.0, v2026.2.0); the CI, pre-commit, and
Dependabot workflows were current and passing when this record was compiled; and PlasmaPy is a PyHC
**core** package.*

### 24. Documentation (RECOMMENDED)
https://docs.plasmapy.org/

*Declared in `pyproject.toml` (`urls.Documentation`), `CITATION.cff` (`url`), `.readthedocs.yml`, the
PyHC registry entry (`docs`), and `README.md`. Verified to resolve.*

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
  - *Funder Identifier:* https://ror.org/027ka1x80

- **Organization:** Smithsonian Institution
  - *Funder Identifier:* https://ror.org/01pp8nd67

- **Organization:** United States Department of Energy
  - *Funder Identifier:* https://ror.org/01bj3aw27

- **Organization:** U.S. National Science Foundation
  - *Funder Identifier:* https://ror.org/021nxhr62

*`README.md`'s acknowledgments name all four, and `docs/about/credits.rst` details what each funded.*

**Name correction.** This file previously wrote the NSF funder as `National Science Foundation`. The
stored value is **`U.S. National Science Foundation`** — the agency's current name, under the
unchanged ROR `https://ror.org/021nxhr62`. Independent corroboration: DataCite's record for the
version DOI (`10.5281/zenodo.18706665`) gives `funderName: "U.S. National Science Foundation"` for
all four NSF awards, and PlasmaPy's own `docs/about/credits.rst` writes "the U.S. National Science
Foundation (NSF)". The older `National Science Foundation` string survives only in DataCite's stale
concept-DOI record and in the 2019 proposal record; it should not be reintroduced from either.

*Considered and not selected: **Google**. `docs/about/credits.rst` lists Google Summer of Code among
the sources of early support. GSoC funds student stipends through a mentorship program rather than
awarding a grant to the project, it appears in no DataCite `fundingReference`, and `README.md`'s
funder list omits it. Recorded here so the omission is understood as a decision.*

### 26. Award Title (OPTIONAL)
- **Award Title:** Collaborative Research: Frameworks: An open source software ecosystem for plasma physics
  - *Award Number:* 1931388
- **Award Title:** Collaborative Research: Frameworks: An open source software ecosystem for plasma physics
  - *Award Number:* 1931393
- **Award Title:** Collaborative Research: Frameworks: An open source software ecosystem for plasma physics
  - *Award Number:* 1931429
- **Award Title:** Collaborative Research: Frameworks: An open source software ecosystem for plasma physics
  - *Award Number:* 1931435
- **Award Title:** Collaborative Research: The Evolution of Magnetic Skeletons During 3D Magnetic Reconnection
  - *Award Number:* DE-SC0016363
- **Award Title:** NASA Heliophysics Data Environment Enhancements (HDEE)
  - *Award Number:* 80NSSC20K0174
- **Award Title:** PlasmaPy Infrastructure and Maintenance
  - *Award Number:* 80NSSC25K0360

*The first six are carried over. The four NSF awards and the DOE award are each present verbatim as
DataCite `fundingReferences` on the version DOI; the HDEE award appears in DataCite's "Other"
description and in `docs/about/credits.rst`. `docs/about/credits.rst` dates the NSF CSSI support to
October 2019 – September 2025.*

**New award.** `docs/about/credits.rst` states: "PlasmaPy infrastructure and maintenance from August
2025 through July 2028 for two person-months per year is supported by NASA Heliophysics Tools and
Methods grant **80NSSC25K0360** to the Smithsonian Astrophysical Observatory." The award title is
recorded as **PlasmaPy Infrastructure and Maintenance**, matching the title of the funded proposal
deposited at https://doi.org/10.5281/zenodo.17148678 (Murphy, Nicholas, 2025, resource type
Text/Proposal). This is the currently active grant and was missing from the record; its funder is
NASA, already listed in Field 25.

*Considered and not selected as separate awards: the "Scholarly Studies grant awarded by the
Smithsonian Institution" and the generic "NASA Heliophysics Tools & Methods grant" phrasing in the
DataCite description. Neither carries an award number or a specific title in any source; the
Smithsonian appears as a funder in Field 25 and the Tools and Methods grant is captured concretely
as 80NSSC25K0360 above.*

**Which funder issued which award.** HSSI's award records carry their funder organization directly,
and the pairings below are the stored state. But neither Field 25 nor Field 26 expresses the
correspondence — the submission form has no per-award funder sub-field, and the view API returns
awards as titles alone — so a refresh working only from those surfaces should take the pairing from
this note rather than treating it as unrecorded. The pairings are: the four CSSI
awards `1931388`, `1931393`, `1931429` and `1931435` are U.S. National Science Foundation;
`DE-SC0016363` is the United States Department of Energy; and `80NSSC20K0174` (HDEE) and
`80NSSC25K0360` are National Aeronautics and Space Administration. For the four NSF awards and the
DOE award that attribution is carried directly in the version DOI's DataCite `fundingReferences`, so
it is verifiable rather than inferred; for the two NASA awards it comes from
`docs/about/credits.rst`, quoted above. The Smithsonian Institution is a Field 25 funder with no
award of its own, for the reason given in the preceding note.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

*No journal publication describes, or is designated as the preferred citation for, PlasmaPy —
`docs/about/citation.rst` directs users to the version-specific Zenodo record instead, and
`docs/bibliography.bib` (which generates the documentation bibliography) contains no PlasmaPy
self-citation.*

*Considered and not selected — two DOIs a future agent will encounter and should not add here:*

- https://doi.org/10.5281/zenodo.3406803 — "NSF CSSI proposal: An open source software ecosystem for
  plasma physics" (Murphy, Everson, Vincena, Parashar, Schaffner; 2019).
- https://doi.org/10.5281/zenodo.17148678 — "PlasmaPy Infrastructure and Maintenance" (Murphy; 2025).

*Both are DataCite resource type **Text / Proposal**: funding proposals, cited by
`docs/about/credits.rst` as funding provenance rather than as literature about the software. Their
substance is already represented — the first by NSF awards 1931388/1931393/1931429/1931435 and the
second by NASA award 80NSSC25K0360, all in Field 26.*

### 28. Related Datasets (OPTIONAL)
Not found

*PlasmaPy ships no dataset with a DOI and supports no specific published dataset. The sample data
it does distribute — the `.npy` Langmuir traces under `docs/notebooks/langmuir_samples/` and the
files in the `PlasmaPy/PlasmaPy-data` repository ("Sample data for testing and documenting
PlasmaPy") — are documentation fixtures with no persistent identifier, not research datasets.*

### 29. Related Software (OPTIONAL)
- https://github.com/astropy/astropy (Astropy — domain dependency; PlasmaPy's public API is built on `astropy.units` and `astropy.constants`)
- https://github.com/PlasmaPy/plasmapy-calculator (plasmapy-calculator — companion package extracted from PlasmaPy)

*Astropy is carried over from the stored record. `plasmapy-calculator` is added: the plasma
calculator formerly shipped inside PlasmaPy has been extracted into a standalone package, and what
remains at `plasmapy.utils.calculator` is a stub whose `main()` raises a `RuntimeError` directing
users to https://github.com/PlasmaPy/plasmapy-calculator. `pyproject.toml` still declares the
`plasma-calculator` console script with the comment "Remove references to plasma calculator after
mid-2026". A companion package split out of this software is exactly what this field is for.*

*Considered and not selected:*

- *Matplotlib, NumPy, pandas, SciPy, requests, tqdm, packaging, wrapt, mpmath, pytest* — declared
  dependencies, but generic scientific-Python and tooling infrastructure. An entry reading "depends
  on NumPy" would be equally true of most of the catalogue and so carries no information about
  PlasmaPy.
- *xarray* — see Field 30 for why it does not qualify there either.
- *plasmapy-sphinx* — a PlasmaPy-authored Sphinx extension used only to build the documentation. It
  is a companion project, but it is documentation tooling rather than software a PlasmaPy user would
  reach for, so it is left out.
- *PlasmaPy-data* — a data repository, not software; see Field 28.

**Two previously recorded values removed** — what they were, and why they are not values of this
field. Both were in the stored HSSI record; both fail the field's relevance gate as written in the
Field 30 relevance rules of `resource_submission_form_fields.md`, which Field 29 applies as well, and
the reasoning is recorded here so neither is re-proposed:

- **`https://github.com/lmfit/lmfit-py`** (lmfit — previously described as "the fitting layer behind
  `plasmapy.diagnostics.thomson.spectral_density_model`"). lmfit is named in neither the Tier A nor
  the Tier B exclusion list, so the test for a package absent from both tiers applies:
  *would it be equally at home in a web app, a finance model, or a biology pipeline?* For a
  general-purpose curve-fitting library the answer is yes, so it takes Tier A treatment — generic
  infrastructure, excluded whether or not it happens to be enumerated. Field 29 applies the same
  exclusion as Field 30, so the answer cannot legitimately differ between the two fields, and this
  record's own Field 30 note had already answered that same test in the affirmative for lmfit. The
  object-level handoff is real — `spectral_density_model` returns an `lmfit.Model` — but a real
  handoff to a generic library is still a handoff to a generic library; that evidence is recorded in
  Field 30's "considered and not selected" list, which is where it belongs.
- **`https://github.com/h5py/h5py`** (h5py — previously described as "the HDF5 layer behind the
  OpenPMD reader and the radiography/particle-tracker writers"). h5py is an explicitly enumerated
  **Tier B** package, and a Tier B package qualifies only on a documented *specific* exchange appearing
  in the public API, docs, examples, or tests. The description cited for it is internal-use language
  of exactly the form the guidance disqualifies ("uses xarray internally" is the worked
  counter-example). Reading and writing HDF5 is generic I/O plumbing that would be equally at home
  outside heliophysics. An earlier note on this record kept h5py on the grounds that it was the stored
  value and that removing it needed a curator's judgement; that reasoning is superseded. h5py is not
  a value of this field, and, as the earlier note itself observed, dropping it contradicts no evidence
  recorded here.

These two removals complete a cleanup already begun on this record, where matplotlib, NumPy, pandas,
xarray, and SciPy were removed from Field 29 earlier for the same reason. **Fields 18 and 19 are
unaffected:** HDF5 remains a genuine input and output format for PlasmaPy on its own evidence (the
OpenPMD reader, the radiography and particle-tracker writers, the bundled NIST ionization-energy file),
whether or not the library implementing it is listed as related software. Those are independent facts,
and a future agent should not "restore consistency" by dropping HDF5 from the format fields.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/astropy/astropy

*This field was previously empty. Astropy is added on cited, API-level evidence rather than on
dependency presence: PlasmaPy's public functions accept and return `astropy.units.Quantity`
throughout, and that contract is machine-enforced by the `@validate_quantities` decorator in
`plasmapy.utils.decorators.validators` and by `@particle_input` in `plasmapy.particles.decorators`;
`plasmapy.plasma.grids` stores grid quantities with their `astropy` units attached; the OpenPMD
reader converts OpenPMD dimension exponents into `astropy.units`; and
`docs/notebooks/getting_started/units.ipynb` documents `Quantity` as the expected input and output
type of `plasmapy.formulary`. That is a shared data model, and Astropy is an astronomy-domain tool
rather than generic infrastructure.*

**Considered and not selected:**

- *xarray* — `plasmapy.plasma.grids.AbstractGrid` holds an `xarray.Dataset` in its public `.ds`
  attribute and builds `xr.DataArray` objects internally. This is internal representation that
  happens to be reachable: no documentation, notebook, or docstring presents an `xarray` object as
  an interchange format, and there is no converter API in either direction. "Uses xarray internally"
  is explicitly not sufficient for this field.
- *lmfit* — `plasmapy.diagnostics.thomson.spectral_density_model` returns an `lmfit.Model`, which is
  a genuine object-level handoff. It is nevertheless a general-purpose curve-fitting library that
  would be equally at home in a finance model or a biology pipeline, so it fails this field's
  generic-infrastructure test. The same test excludes it from Field 29, where it was previously
  recorded and is now absent — see the removal rationale there. lmfit is a value of neither field;
  this bullet exists so the handoff evidence is not mistaken for new grounds to add it back.
- *SunPy and SpacePy* — removed from this field in an earlier reconciliation and still correctly
  absent. Both are fellow PyHC core packages installable alongside PlasmaPy, and PlasmaPy's
  `utils/datatype_factory_base.py` and `plasma/plasma_base.py` acknowledge SunPy/ndcube as the
  source of a design pattern. Neither is a demonstrated data exchange: PlasmaPy imports neither, and
  there is no converter, plugin, or shared data model between them. PyHC co-membership is never on
  its own sufficient here.
- *The OpenPMD standard and PIC codes that write it* (WarpX, PIConGPU, FBPIC) — `HDF5Reader` genuinely
  ingests their simulation output, which is a real interoperation, but it is with a **file standard**
  rather than with a named package: PlasmaPy reads OpenPMD files through `h5py` directly and does not
  use `openpmd-api`. That relationship is recorded where it belongs, as HDF5 in Field 18.
- *Jupyter* — the example gallery is notebooks, which is documentation format rather than a data
  exchange with Jupyter.

### 31. Related Instruments (OPTIONAL)
Not found

*PlasmaPy is instrument-agnostic infrastructure. Its diagnostics subpackage supports **classes** of
diagnostic — swept Langmuir probes, Thomson scattering systems, proton radiography with radiochromic
film stacks — generically, parameterised by the user, with no named instrument's data format,
calibration, or convention implemented in the package.*

*Negative research, recorded so it is not repeated. The named instrument-and-mission references found
in the repository are demonstration material:*

- **ACE (Advanced Composition Explorer)** — `docs/notebooks/particles/ace.ipynb` uses hourly C, O, and
  Fe ion densities during an ICME that were *estimated by eye from Figure 4 of Gilbert et al. (2012)*
  and hard-coded into the notebook. No ACE data is read, and no ACE product, format, or archive is
  supported.
- **MMS (Magnetospheric Multiscale)** — `docs/notebooks/formulary/magnetosphere.ipynb` uses MMS
  spacecraft separations as a worked example for computing magnetospheric length scales. No MMS data
  is read.

*Both are exactly the "tutorial/demo name-drop" case this field excludes. Note that both **do**
resolve in HSSI's controlled vocabulary — `https://spase-metadata.org/SMWG/Observatory/ACE` and
`https://spase-metadata.org/SMWG/Observatory/MMS`, both type 2 (observatory) — so they were excluded
on relevance, not because they could not be resolved. They are observatories in any case, so they
could never have populated Field 31.*

*Also considered: the OMEGA Laser Facility and the Basic Plasma Science Facility (LAPD), which appear
in `docs/about/credits.rst` as communities that supported the project, not as instruments the
software supports; and ITER, which appears as a parameter set in
`docs/notebooks/formulary/iter.ipynb`. Fusion devices are out of HSSI's heliophysics instrument
scope regardless.*

### 32. Related Observatories (OPTIONAL)
Not found

*Same conclusion and same evidence as Field 31: no mission or observatory is supported by
purpose-built functionality, a data format, an archive client, or a convention. ACE and MMS appear
only as worked examples, and their SPASE identifiers are recorded in Field 31 so that a future agent
can see they were evaluated and rejected on relevance rather than left unresolved.*

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/PlasmaPy/PlasmaPy-logo/main/exports/with-text-dark.png

*The image `README.md` renders at the top of the page, served from the project's own
`PlasmaPy/PlasmaPy-logo` repository. Verified to resolve.*

*Considered and not selected: the PyHC registry lists a different asset from the same repository,
`https://github.com/PlasmaPy/PlasmaPy-logo/raw/main/exports/graphic-circular.png` — a circular mark
without the wordmark. The stored `with-text-dark.png` is the project's own README choice and carries
the name, which reads better as a catalogue logo. Either is authoritative; there is no need to
change.*
