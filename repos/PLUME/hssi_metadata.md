# HSSI Metadata Extraction Results

**HSSI Software ID:** 59c24c09-5ecd-44c8-a324-5a7da62c634b
**Repository:** https://github.com/kgklein/PLUME
**Source Revision:** 21a3711745d5fb6d8f147d4ca773a9db7508924d
**Extraction Date:** 2026-08-10
**Validation Date:** 2026-11-21
**Validation Status:** PASS
**Release v.2.0.0 evidence:** read at `46864a43a466458f881624af03a0cd251ef169f4` (the `v.2.0.0` tag,
2026-11-20) and cited as `46864a4`; the fields the release could change were re-read there. Evidence
not marked `46864a4` was read at the Source Revision above. Root-level files cited without a revision
(`INSTALL.md`, `input.md`, `output.md`, `tutorial.md`, `README-JETPLUME.md`) and the README's former
numbered sections (§1–§6) are those of `21a3711`; v.2.0.0 moved or rewrote them under `docs/`.

---

**Scope note — read this before the field evidence.** PLUME is a single-executable, serial Fortran
dispersion-relation solver (with a small bundled C99 component for the plasma dispersion function
since v.2.0.0), not a data-analysis package. Three consequences shape almost every field below:

1. It consumes only its own Fortran namelist input files and emits only its own ASCII tables. It
   reads no archive, no mission product, and no instrument data, so Data Sources, Related
   Instruments and Related Observatories are legitimately empty rather than unfilled, and Related
   Datasets holds only the input deposit of the developers' own JET-PLUME paper (Field 28).
2. The repository bundles three satellite components beyond the dispersion solver: **JET-PLUME** (a
   field–particle-correlation extension merged into `main` at v.1.1.0, `src/fpc.f90` +
   `docs/README-JETPLUME.md`, which v.2.0.0 documents as the all-kinetic historical pathway),
   **`linfpclib`** (a Python wrapper that writes inputs, runs the executable, and loads results), and
   **`SWIFT`** (a PyVista 3D/animated eigenmode visualizer). Much of the Software Functionality and
   Programming Language evidence lives in those components, not in the dispersion solver.
3. The physics is region-agnostic by construction — a uniform magnetized plasma with arbitrary
   bi-Maxwellian components and, since v.2.0.0, cold-fluid components. Region and Phenomena values
   therefore rest on the specific applications the repository and its code paper actually name, not
   on the full set of places a plasma dispersion solver could be pointed.

**Release v.2.0.0 (2026-11-20, tag at `46864a43a466458f881624af03a0cd251ef169f4`).** The fields this
release could change were re-read at that revision, which is cited as `46864a4` beside the evidence it
supplied; evidence not so marked was read at the Source Revision above. The release added cold-fluid
and mixed kinetic/cold populations, a choice of `rho_ref` or `d_ref` normalization, a bundled
Faddeeva implementation of the plasma dispersion function, adaptive Bessel-function caching, and
extended eigenfunction, wave-energy and heating diagnostics. It also reorganized the user manual
under `docs/`: the root `INSTALL.md`, `input.md`, `output.md`, `tutorial.md` and `README-JETPLUME.md`
moved there or were rewritten there, the README lost its former numbered sections (authors,
citation instructions, license copy), and the repository images moved to `docs/assets/`. A
reference below to one of those root files or README sections is to the Source Revision unless
`46864a4` is named.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Source:* Not derivable. The repository names authors but no metadata submitter, and the published
HSSI record does not expose who submitted it. A real name and work email must be supplied by whoever
submits or updates this record.

---

### 2. Persistent Identifier (RECOMMENDED)
`https://doi.org/10.5281/zenodo.15215513`

*Source:* The value published in HSSI, independently confirmed against Zenodo and DataCite.

**Why this DOI rather than the one in the README.** `10.5281/zenodo.15215513` is the Zenodo *concept*
DOI: every version record reports `conceptrecid: 15215513` and `conceptdoi:
10.5281/zenodo.15215513`, and DataCite lists four `HasVersion` relations from it
(`10.5281/zenodo.15215514`, `10.5281/zenodo.16904910`, `10.5281/zenodo.17148711`, and, since the
v.2.0.0 release, `10.5281/zenodo.24407914`). The concept now presents v.2.0.0 (DataCite `version:
v.2.0.0`, title "kgklein/PLUME: PLUME 2.0.0"), matching Field 12. Field 2 asks for "the concept DOI
for all versions," so the stored value is the correct one.

**Rejected alternative:** `10.5281/zenodo.15215514`. This is what the repository itself advertises —
before v.2.0.0 the README badge (`README.md` line 1), the FORD landing page (`ford_project.md` line
28), and the BibTeX blocks in both files all cited it; at `46864a4` the badges are gone but the
manual's BibTeX block (`docs/index.md`) still cites it. It is the **v.1.0.1 version DOI**, not the
concept DOI, so using it would pin the record to the April 2025 release and silently exclude every
later one. A version DOI belongs in Field 12 (Version PID), where the current release's DOI is
recorded. This is an upstream inconsistency in the repository, not an error in the HSSI record — a
future agent should not "correct" Field 2 to match the repository's BibTeX.

---

### 3. Code Repository (MANDATORY)
`https://github.com/kgklein/PLUME`

*Source:* The repository's own canonical URL, corroborated by `git remote`, `ford_project.md`
(`project_github`), the clone instruction in `INSTALL.md`, and the acknowledgement request in
`README.md` §2. Default branch `main`. Unchanged at `46864a4`: the clone instruction is now in
`docs/INSTALL.md`, the README's "Citation and license" section asks users to acknowledge
`https://github.com/kgklein/PLUME`, and the v.2.0.0 Zenodo deposit links `IsSupplementTo
https://github.com/kgklein/PLUME/tree/v.2.0.0`.

---

### 4. Software Functionality (MANDATORY)

- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Wave Polarization Analysis
- Data Processing and Analysis: 3D Particle Distribution Processing
- Data Processing and Analysis: Plasma Moments
- Data Processing and Analysis: 2D Slices
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Data Visualization: 3D Graphics
- Data Visualization: Movies
- Data Visualization: 2D Slices
- Models and Simulations
- Models and Simulations: First Principles
- Models and Simulations: Theory
- Models and Simulations: Physics-Based

*Source:* Code analysis of `src/*.f90`, `linfpclib/`, `SWIFT/SWIFT.py`, `plotter/example/*.plt`, and
the repository documentation (`README.md`, `README-JETPLUME.md`, `input.md`, `output.md`,
`tutorial.md`).

**Re-checked for release v.2.0.0 at `46864a4`; the set is unchanged.** Every routine cited below
still exists and is still built (the `Makefile` `LFMOD` list links `disprels`, `fpc` and the new
modules into `plume.e`); line numbers below are those of `46864a4`. The release's new capabilities —
cold-fluid and mixed kinetic/cold populations, the `d_ref` normalization, the Faddeeva evaluation of
the plasma dispersion function, adaptive Bessel caching, and wave-energy and corrected heating
diagnostics (`docs/models.md`, `docs/heating.md`, `docs/eigenfunctions.md`) — are further
linear-theory calculations of the same kind and are carried by the existing *Models and Simulations:
First Principles* / *Theory* and *Data Processing and Analysis: Analysis* / *Plasma Moments* values;
the vocabulary has no fluid-model or cold-plasma value that would add anything. The new
`contours/plot_plume_resonances.py` plots dispersion, polarization, resonance-velocity contours and
heating channels with `matplotlib` (line plots and 2D contour maps), which the existing *Line Plots*
and *2D Graphics* values already cover.

**A parent category belongs in the list alongside each of its children, and the earlier published
set omitted one.** The value set previously published in HSSI held
`Data Processing and Analysis: Wave Polarization Analysis` and `Data Processing and Analysis:
Analysis` without their parent `Data Processing and Analysis`. HSSI does not add a parent implicitly
when a child is selected, so the parent is a value in its own right; its earlier absence made the
published set incomplete rather than differently classified. Both of those leaf values are correct and
are retained.

**Evidence for each value.**

- *Data Processing and Analysis: Wave Polarization Analysis* — `calc_eigen` (`src/disprels.f90:2580`
  at `46864a4`) returns the complex electric field components `(Ex, Ey, Ez)` that define the wave's
  polarization state, and the shipped gnuplot scripts compute and plot the degree of elliptical
  polarization of the `x` and `y` electric-field components from output columns 13–16
  (`plotter/example/example_kpar.plt`, the `#Polarization` panels, unchanged at `46864a4`; described
  in the pre-v.2.0.0 `tutorial.md` §4 as "the degree of elliptical polarization of the $x$ and $y$
  components of the electric field"). At `46864a4` the manual lists "E/B polarization" as a supported
  diagnostic for kinetic, fully cold and mixed plasmas (`docs/models.md`, capability matrix), and the
  new `contours/plot_plume_resonances.py` plots polarization against the scan parameter.
- *Data Processing and Analysis: Analysis* — the code derives physical quantities beyond the raw
  dispersion roots: growth/damping rates, power absorption or emission per species, and — with
  `low_n` true — that power decomposed into Landau, transit-time, and separated `n = +1` / `n = -1`
  cyclotron channels (`output.md` lines 115–135, `Ps_split` in `calc_eigen`). At `46864a4` the
  decomposition is the "seven selected channels" of `docs/heating.md` (`Ps_split(1:7,1:nspec)`,
  `src/disprels.f90:497`), and v.2.0.0 adds the complete formal wave energy for kinetic, cold and
  mixed plasmas (`docs/heating.md`, `src/heating_energy.f90`).
- *Data Processing and Analysis: 3D Particle Distribution Processing* — JET-PLUME `option 7`
  (`compute_fpc_cart`, `src/fpc.f90:34` at `46864a4`) computes the perturbed distribution function
  `f_s1(v_x, v_y, v_z)` (real and imaginary parts) and the field–particle correlations `C_Ei` on a
  full 3D Cartesian velocity grid; `option 6` (`compute_fpc_gyro`, `src/fpc.f90:1047`) does the
  gyrotropic `(v_perp, v_par)` equivalent. `linfpclib.loadlinfpc3d` and `loadlinfpc3d_dist` read those
  velocity-space volumes back into Python. v.2.0.0 keeps this pathway for all-kinetic plasmas only:
  "Cold/mixed FPC is not implemented" (`docs/README-JETPLUME.md`, `46864a4`).
- *Data Processing and Analysis: Plasma Moments* — `src/fpc.f90` integrates the perturbed
  distribution over velocity when `computemoment` is true, explicitly computing the "Density
  Fluctuation: Zeroth Moment of delta f"
  and the "Fluid Velocity: First Moment" (comments at lines 605 and 614 at `46864a4`), using a
  Sokhotski–Plemelj treatment of the resonant denominator. `linfpclib.loadmoms` loads the resulting
  per-species density and velocity moments. Independently, `calc_eigen` returns per-species density
  fluctuations (`ns`) and velocity fluctuations (`vmean`) derived from the susceptibility tensor; at
  `46864a4` the new `src/species_moments.f90` extends these to cold-fluid populations ("Species U and
  density" supported for kinetic, fully cold and mixed plasmas, `docs/models.md`).
  Note the documented upstream limitation: the gyrotropic routine refuses to compute moments
  ("WARNING! The gyro routine does not support computing moments at this time due to computational
  demand!", `src/fpc.f90:1223` at `46864a4`) — FPC moments come from the Cartesian routine only.
- *Data Processing and Analysis: 2D Slices* — the Cartesian JET-PLUME output file stores three 2D
  planes of each 3D velocity-space quantity — `(v_perp,1, v_perp,2)`, `(v_perp,1, v_par)`,
  `(v_perp,2, v_par)` — separated by `---` (`README-JETPLUME.md` §4, "Cartesian Ouput"; at `46864a4`
  `docs/README-JETPLUME.md`: "Projection files contain (x,y), (x,z), (z,y) array layouts separated by
  `---`"); the gyrotropic routine produces the `(v_perp, v_par)` plane described there as "equal to
  integrating out the third coorindate, $\theta$" (at `46864a4`, distributions "reduced over velocity
  gyrophase to a (vperp,vpar) grid"); and `linfpclib.reduce_3d_to_projections` reduces a 3D velocity
  array onto those same three planes. `SWIFT.build_domain` additionally samples the reconstructed 3D
  real-space fluctuation field on a **fixed-`y` plane** (`DomainSampling.y`, driven by `SWIFT_Y0`),
  which is a literal plane cut through a 3D volume. *Caveat for a future reader:* the JET-PLUME
  evidence is projection (integration over one axis) rather than cross-section, while the taxonomy
  note for this value speaks of "cross-sections … plane cuts, volumetric data sampling." The value is
  selected because "volumetric data sampling" covers the plane reductions, and SWIFT's fixed-`y` cut
  is an unambiguous plane cut that supports the value on its own even if a curator declines to treat
  projections as slices.
- *Data Visualization: 2D Slices* — the primary evidence is `plotlinfpc_gyro_dist`
  (`linfpclib/linfpcplot.py:127`), which displays the real or imaginary part of the perturbed
  distribution function on the gyrotropic velocity plane as a 2D `matplotlib` figure: it selects
  `linfpcdata['re_f']` or `['im_f']`, titles the figure `Re{$f(v_{||},v_\perp)$}` or
  `Im{$f(v_{||},v_\perp)$}`, renders it with `plt.pcolormesh(vpar, vperp, C, …)`, labels the axes
  `$v_{||}/v_{ts}$` and `$v_{\perp}/v_{ts}$`, and can overlay the resonant velocity as a vertical
  line. This citation carries the value cleanly: the function receives an already-2D velocity plane
  and displays it, performing no reduction of its own, so the projection-versus-cross-section question
  raised above does not arise for the visualization value. Supporting evidence: `plot_9pan_cart`
  (`linfpclib/linfpcplot.py:245`) lays the Cartesian velocity planes out as a 3×3 `plt.subplots` grid
  of `pcolormesh` panels — "Makes 3x3 plot of projections of FPC vel signature in cartesian
  coordinates" — `plot_fs1_re_im_cart` (`linfpclib/linfpcplot.py:336`) does the 2×3 equivalent for
  the perturbed distribution function, and `SWIFT` renders its fixed-`y` plane.
- *2D Graphics* — `plotter/example/example_map.plt` renders the dispersion tensor magnitude
  `log10|Λ(ω_r, γ)|` as a 50-level `pm3d` contour map over the complex-frequency plane with the
  identified roots overplotted; `linfpcplot.plotlinfpc_gyro` and `sweep2dplot` produce 2D
  velocity-space and two-parameter-sweep maps.
- *Line Plots* — `plotter/example/example_kpar.plt`, `example_kperp.plt`, `example_kpar-E.plt` and
  `example_double.plt` plot `ω_r/Ω_p`, `γ/Ω_p`, per-species damping ratios and polarization against
  the scan parameter; `linfpcplot.plot_disp_rel` and `plot_disp_power_2spec` are the Python
  equivalents.
- *3D Graphics* — `SWIFT/SWIFT.py` reconstructs `δB(x,t)` and `δU_ref(x,t)` in real space from a
  PLUME eigenmode row and renders them in 3D with PyVista (`create_static_plot`, `_build_glyph_mesh`,
  `_add_orientation_axes`).
- *Movies* — `SWIFT.create_animation` opens a GIF (`plotter.open_gif`) and writes one frame per step
  through a wave period (`plotter.write_frame`, `SWIFT_FRAMES_PER_PERIOD`, frames spanning
  `T = 2π/|ω_r|` so the loop closes); `SWIFT/run_swift_viz_example.sh` exercises it with
  `SWIFT_CREATE_GIF=1`.
- *First Principles* — the code solves the linearized Vlasov–Maxwell system from kinetic theory,
  following "Stix 'Waves in Plasmas' Chapter 10, Eqns. 66-73" (`README.md` §1; at `46864a4`
  `docs/index.md`: "Its kinetic equations follow Stix, *Waves in Plasmas*, Chapter 10, equations
  66–73"), with the plasma dispersion function (`zet_in`, `src/disprels.f90:4983` at `46864a4`, now
  evaluated through the bundled Faddeeva implementation, `src/plasma_z_faddeeva.f90`) and
  Bessel-function sums over cyclotron harmonics (`src/bessel.f90`, `src/bessel_cache.f90`). The
  v.2.0.0 cold-fluid response is likewise derived from the equations of motion, following "Verscharen
  & Chandran (2013), Section 2.1" (`docs/index.md`).
- *Theory* — it is a linear-theory calculation: it evaluates an analytic dispersion tensor and
  locates its roots (`map_search`, `refine_guess`, `find_minima`) rather than time-advancing a
  simulation. The RNAAS code paper frames it as an implementation of "the linear Vlasov–Maxwell
  dispersion relation."
- *Physics-Based* — the broader physics-based modelling parent value, selected alongside *First
  Principles* because the collision extension (`collision_type = 1`, a non-conservative Krook
  operator for neutral–charged collisions, `input.md`; at `46864a4` `docs/input.md`: "1
  nonconservative Krook", supported for kinetic populations only and marked "P / NV off-diagonal
  accuracy" in `docs/models.md`) is a modelled closure rather than a first-principles collision
  integral.

**Considered and rejected, with reasons** (recorded so these are not re-proposed):

- *Servers and Environments: High Performance Computing* — **rejected on direct evidence.**
  Before v.2.0.0, `ford_project.md` line 35 called PLUME "a parallelised numerical code" (and "even
  relativistic"), but a sweep of every `src/*.f90` file and the `Makefile` found no MPI call, no
  `use mpi`, no OpenMP sentinel and no `-fopenmp`/`-qopenmp` flag; the build linked a single serial
  executable `plume.e`. v.2.0.0 removed that sentence: at `46864a4` the FORD landing page reads "a
  Fortran solver for linear electromagnetic dispersion relations in homogeneous, nonrelativistic,
  magnetized plasmas", the README opens "PLUME is a serial Fortran solver", and the same sweep over
  `src/*.f90`, `src/*.c` and the `Makefile` still finds no MPI, OpenMP, CUDA or OpenACC. Do not add
  HPC.
- *Coordinate Transforms* (parent or any child) — the code does work in a wave-aligned frame
  (`k_perp,1 = k_perp`, so the `⊥,1` direction lies in the wave–magnetic-field plane) and converts
  between gyrotropic `(v_perp, v_par)` and Cartesian `(v_x, v_y, v_z)` velocity-space
  representations. Every child of this category is a *physical or spacecraft* coordinate system
  (heliospheric, ionospheric, magnetospheric, mission-specific, planetary, solar); none covers
  velocity-space representations, and the bare parent would imply a spatial-frame capability the code
  does not offer.
- *Models and Simulations: MHD* — the tutorial identifies "the Slow, Alfven, Fast, and 'entropy'
  (SAFE) modes … at MHD length scales," but the equations solved are Vlasov–Maxwell, not the MHD
  equations. Recovering MHD-scale modes from a kinetic dispersion relation is not an MHD solver.
- *Models and Simulations: Data Guided* — `option 5` follows roots "along a prescribed path … set by
  solar wind models" (`src/plume.f90:177` at `46864a4`, `read_radial_input`, `radial_scan`). Those
  paths come from *models*, not observations, and the option is explicitly unfinished: it prints
  "Option 5 is under development. Use with caution...Here be Dragons..." before running, and at
  `46864a4` `docs/input.md` adds that "No small standalone public radial model is currently
  validated".
- *Models and Simulations: Forward-Fitting* — root refinement (`refine_guess`, secant iteration in
  `rtsec`) minimizes `|Λ|` in complex-frequency space. That is root-finding on an analytic function,
  not fitting a forward model to measured data.
- *Models and Simulations: Field-line Tracing* and *Data Processing and Analysis: Field-line Tracing*
  — SWIFT draws "straight 'field lines' parallel to z (consistent with B0 || z-hat)"
  (`SWIFT.build_domain` docstring); they are pre-placed straight sampling polylines, not integrated
  field lines. Nothing in the repository traces a field line.
- *Data Visualization: Hodograms* — the polarization panels plot the derived scalar `P_E^xy` against
  the scan parameter, not one field component against another.
- *Data Processing and Analysis: Data Reduction* — `reduce_3d_to_projections` does perform
  mean/sum/max reductions, but that operation is the plane projection already credited under *2D
  Slices*; the package offers no data-volume-reduction capability in its own right.
- *Data Processing and Analysis: Processing* — a catch-all that would add nothing over *Analysis*;
  the wrapper's write-input → run → load chain is plumbing around the solver, not a user-facing
  processing capability.
- *Data Processing and Analysis: Energy Spectra* — the heating output is power per species (and per
  damping channel) as a function of the scan parameter, not flux or power versus energy.
- *Data Processing and Analysis: Pitch Angle Distributions* — the velocity grids are
  `(v_perp, v_par)` or `(v_x, v_y, v_z)`; nothing bins by pitch angle.
- *Data Processing and Analysis: Data Access and Retrieval* — the only network code in the repository
  is `.github/scripts/*.py`, which queries the NASA ADS API to maintain the project's
  citing-papers bibliography during CI. That is repository housekeeping, not a data-access capability
  offered to users.
- *Data Processing and Analysis: Spectrogram*, *Time Series Analysis*, *File Format Conversion*,
  *Calibration*, *Image Processing*, *ML/AI*, all *Mission-related* values, *Data Visualization:
  Spectrogram / Orbit Plots / Spacecraft Formation Plots / Web-Based / Mission-Specific* — no
  corresponding capability anywhere in the repository.

---

### 5. Related Region (MANDATORY)

- Earth Magnetosphere
- Interplanetary Space
- Planetary Magnetospheres
- Solar Wind

*Source:* `Earth Magnetosphere`, `Interplanetary Space` and `Planetary Magnetospheres` are the
regions already published in HSSI; `Solar Wind` rests on repository evidence set out below.

**Why `Solar Wind` belongs here.** It is the one region the repository names in its own source and
documentation: `src/vars.f90:279` heads its radial-scan block "Variables for radial scan of solar
wind models: See Option 5"; `src/disprels.f90:1577` describes `radial_scan` as running "for a
specified radial solar wind model"; `input.md` documents `option 5` as "Find roots for parameters
along a prescribed path", adding "Path is set by solar wind models, with values calculated and output
by helper function …". At `46864a4` the source comments stand
(`src/vars.f90:244` and `:307`, `src/plume.f90:177`, `src/functions.f90:473`,
`src/disprels.f90:1866`), while the rewritten manual no longer names the solar wind and keeps
`option 5` only as a kinetic-only legacy radial scan (`docs/input.md`). v.2.0.0's new examples
(`inputs/example/*.in`) name no region either, so the release neither adds nor removes regional
evidence. The code paper that the developers
designate as the prior description of PLUME (Klein & Howes 2015, Field 27) is titled "Predicted
impacts of proton temperature anisotropy on solar wind turbulence." `Solar Wind` is a distinct
vocabulary row from `Interplanetary Space`, so the two coexist — neither supersedes the other.

**Why the three broader regions belong here too.** A uniform-magnetized-plasma dispersion solver
applies wherever a hot collisionless magnetized plasma does; Earth's magnetosphere, interplanetary
space, and planetary magnetospheres are a defensible reading of that generality, and nothing in the
repository contradicts any of them.

**Considered and not selected** (no repository evidence; recorded so they are not re-proposed as
oversights): `Corona`, `Solar Environment`, `Chromosphere`, `Earth Magnetosheath`, `Earth Inner
Magnetosphere`, `Earth Magnetotail`. Each is a plausible *application* of a hot-plasma dispersion
solver, and the magnetosheath in particular is where temperature-anisotropy instabilities of the kind
PLUME finds are most studied — but the repository never names any of them, and selecting them would
be inference rather than evidence. The neutral–charged Krook collision operator
(`collision_type = 1`, `Kn`, `nunS`) does make partially ionized plasmas tractable, which would point
at `Chromosphere` or `Earth Ionosphere`; the repository never says so, so it is left out.

---

### 6. Authors (MANDATORY)

**1. Kristopher Gregory Klein**
- Identifier: `https://orcid.org/0000-0001-6038-1923`
- Affiliation: University of Arizona — `https://ror.org/03m2x1q45`

**2. Gregory Howes**
- Identifier: `https://orcid.org/0000-0003-1749-2665`
- Affiliation: University of Iowa — `https://ror.org/036jqmy94`

**3. Collin Brown**
- Identifier: `https://orcid.org/0000-0001-6113-4860`
- Affiliation: United States Naval Research Laboratory — `https://ror.org/04d23a975`
- Affiliation: University of Iowa — `https://ror.org/036jqmy94`

*Source:* `README.md` §"Authors" lists exactly Kristopher Klein (kgklein@arizona.edu), Gregory Howes
(gregory-howes@uiowa.edu), and Collin Brown (collin.crbrown@gmail.com); `ford_project.md` lists the
same three on its `author:` line; and Klein's and Howes's ORCIDs match the RNAAS code paper's author
metadata (Crossref record for `10.3847/2515-5172/add1c2`). Brown's ORCID, and each of the three
distinct organizations named above, were already published in HSSI; the one affiliation entry that was
not — Brown's University of Iowa — is evidenced below.

**Re-checked for release v.2.0.0; the list is unchanged.** At `46864a4` the README has no authors
section; the manual's "Authors, scientific references and citation" section (`docs/index.md`) states
"PLUME is maintained by Kristopher Klein (kgklein@arizona.edu), Gregory Howes
(gregory-howes@uiowa.edu), and Collin Brown (collin.crbrown@gmail.com)", the `ford_project.md`
`author:` line still names the same three, and the `LICENSE` copyright is unchanged. The JET-PLUME
paper (Brown, Howes, Klein & TenBarge 2026, Field 27) cites the software itself as "C. R. Brown,
G. G. Howes, and K. G. Klein, 'JET-PLUME: A kinetic extension to the PLUME framework'", the same
three people. The repository still has no `CITATION.cff`, `.zenodo.json` or `codemeta.json`.

**Ordering.** This dossier lists the three in the order used by the README and the code paper
(Klein, Howes, Brown), while HSSI renders them alphabetically by family name (Brown, Howes, Klein).
The two orderings describe the same set of three authors; the difference is presentational and is not
drift.

**Collin Brown's University of Iowa affiliation.** HSSI previously gave Brown only the Naval Research
Laboratory, which understates his affiliation: three primary sources give him a second, co-equal one.
The RNAAS paper lists "Department of Physics and Astronomy, University of Iowa, Iowa City, IA 52242,
USA" as his *first* affiliation and "Plasma Physics Division, Naval Research Laboratory" as his
second; `README-JETPLUME.md` line 4 reads "University of Iowa; Naval Research Lab- Plasma Physics
Division"; and the JET-PLUME block of the `src/plume.f90` header (lines 11–14) gives his institution
as "University of Iowa". At `46864a4` the `src/plume.f90` header is unchanged, the rewritten
`docs/README-JETPLUME.md` no longer carries the affiliation line, and the JET-PLUME paper (2026)
again lists the University of Iowa first and the Naval Research Laboratory's Plasma Physics Division
second. The stored `University of Iowa` identity carries the matching ROR
`https://ror.org/036jqmy94`. The NRL affiliation is correct as published — nothing contradicts it,
and his `collin.r.brown6.ctr@us.navy.mil` commits confirm it.

**Department-level affiliations deliberately not used.** The paper and the `src/plume.f90` header
place Klein at the "Lunar and Planetary Laboratory, University of Arizona" and Brown/Howes in the
"Department of Physics and Astronomy" at Iowa, and NRL's "Plasma Physics Division" has its own ROR
(`https://ror.org/01kg1t878`). Institution-level affiliations are used instead because: the Arizona
Lunar and Planetary Laboratory has **no** ROR record (a ROR search returns the unrelated Lunar and
Planetary Institute in Houston, `https://ror.org/01r4eh644`, and other non-matches), the Iowa physics
department has no ROR record, and substituting NRL's division ROR for the parent would replace a
correct, already-stored, ROR-identified value with a narrower one for no gain. This is recorded so a
later refresh does not spend the same effort.

**Considered and not recorded as an author: Rogerio Jorge.** His identity is fully resolved below so
that a later refresh presented with new evidence does not have to redo the research:

- Name: Rogerio Jorge
- Identifier: `https://orcid.org/0000-0003-2941-6571`
- Affiliation: University of Wisconsin–Madison — `https://ror.org/01y2jtd41`
  (ORCID employment: Assistant Professor, Department of Physics, University of Wisconsin-Madison,
  from 2024-01-01 with no end date — i.e. his affiliation at the time of his 2025-09-12 commit; his
  git email `rogerio.jorge@ist.utl.pt` is a stale Instituto Superior Técnico address from a post he
  left on 2023-12-31. Note the spelling trap: ORCID writes the institution with a plain hyphen,
  while ROR's display name and the organization row HSSI already carries both use an **en-dash**
  (U+2013). That row carries the ROR `https://ror.org/01y2jtd41`, so the organization is identified
  directly by that ROR rather than by matching the en-dash spelling by name.)

*Evidence that was weighed in favour.* He is a credited creator on the Zenodo records for v.1.2.0
(`10.5281/zenodo.17148711`) and v.2.0.0 (`10.5281/zenodo.24407914`, the version Field 12 records),
and he is a genuine git contributor: commit `f5225d5ec920701aa90d062a68d68fddfdd629d9`, 2025-09-12,
"Fix Makefile: correct module dependencies and moddir handling" (merged via PR #28, five days before
the v.1.2.0 release). He has no other commit through `46864a4`.

*Evidence that decided it against.* Every maintainer-authored statement of PLUME's authorship draws
only on the three people in Field 6: `README.md` §"Authors" (all three), the `author:` line in
`ford_project.md` (all three), the RNAAS code paper (all three), `INSTALL.md` §"Authors" and
`tutorial.md` §"Authors" (Klein and Howes), the `LICENSE` copyright (Klein and Howes; the copy
reproduced in `README.md` §6 adds Brown), and the `src/*.f90` file headers (Klein for PLUME, Brown for
the JET-PLUME block). Jorge appears in none of them. The one authorship statement in the repository
that names someone outside Field 6 is `README-JETPLUME.md` §"Other Contributing Authors", which names
Jason TenBarge and is addressed separately below — it does not name Jorge either. More decisively, the Zenodo creator lists
are demonstrably auto-derived from GitHub contributors rather than curated: the repository contains no
`CITATION.cff` and no `.zenodo.json` in any commit on any branch, the v.1.0.1 and v.1.1.0 creator
lists render Collin Brown as the bare GitHub handle `collinrbr`, and **Gregory Howes — an author on
every maintainer-authored list and on the code paper — is absent from the Zenodo creators of every
version** because he has no commits in the repository at all (his name appears in no commit on any
branch, though a remote branch is named `howes`). Treating the Zenodo creator list as authoritative
for Field 6 would therefore require dropping Howes, which is plainly wrong; the same reasoning that
keeps Howes in argues against reading Jorge in. The v.2.0.0 deposit changes none of this: its
creators are Collin Brown (now under his human name rather than the handle `collinrbr`, as on his
GitHub profile), Kristopher Gregory Klein and Rogerio Jorge — the repository's three GitHub
contributors — and Howes is again absent. His contribution is also a one-commit build-system
fix rather than science content. Recording a person the maintainers do not name as an author would
misattribute authorship in a public catalogue, the more consequential of the two possible errors, so
he is omitted. He should not be re-proposed on the strength of the Zenodo creator list alone; that
would take new evidence, such as the maintainers adding him to their author statement or a
`CITATION.cff`. He is not an author of the JET-PLUME paper (2026), nor named in its citation of the
software.

**Considered and not recorded as an author: Jason TenBarge.** Resolved here for the same reason:

- Name: Jason TenBarge
- Identifier: `https://orcid.org/0000-0003-0143-951X`
- Affiliation: Princeton University — `https://ror.org/00hx57361`
  (ORCID employment: Research Scholar, Department of Astrophysical Sciences, Princeton University,
  from 2020 with no end date. HSSI already carries a `Princeton University` row with this ROR.)

*Evidence that was weighed in favour.* `README-JETPLUME.md` §"Other Contributing Authors" names Greg
Howes, Kris Klein, and Jason TenBarge. That is a maintainer-authored authorship credit inside the
repository — arguably stronger evidence than Jorge's — and JET-PLUME has been part of PLUME proper
since v.1.1.0, so the component he is credited on is now shipped and installed with the code. At
`46864a4` the rewritten `docs/README-JETPLUME.md` reads "Original JET-PLUME contributions are credited
to Collin Brown, Gregory Howes, Kristopher Klein and Jason TenBarge." He is also the fourth author of
the JET-PLUME paper: Brown, Howes, Klein & TenBarge (2026), *Physics of Plasmas* 33, 072101
(`10.1063/5.0335826`, Field 27).

*Evidence that decided it against.* The credit is scoped to the JET-PLUME component and is worded as
"Other Contributing Authors," distinct from the lead-author line above it. The post-merge top-level
`README.md` — the file the merged product presents — still lists only Klein, Howes, and Brown as
PLUME's authors, as do `ford_project.md` and the code paper, while the `src/*.f90` headers and the
`LICENSE` name subsets of those same three. He has no commits in the repository and appears on no
Zenodo record, including the v.2.0.0 deposit. Omitted for the same reason as above. The JET-PLUME
paper, which an earlier revision of this record expected would settle the question, was published
in July 2026 and was weighed when v.2.0.0 was recorded. It does not change the outcome: the paper's
own citation of the software (its reference to "JET-PLUME: A kinetic extension to the PLUME
framework", https://github.com/kgklein/PLUME/) credits Brown, Howes and Klein, not TenBarge, so the
same authors draw the line between co-authoring the paper and authoring the code; the v.2.0.0 manual
credits him with "contributions" to JET-PLUME separately from the three people it names as PLUME's
maintainers; and he appears in no software-metadata source (no `CITATION.cff`, `.zenodo.json`,
`codemeta.json` or Zenodo creator list). Paper co-authorship alone does not make a person an author
of the software. A later refresh should revisit this only if the maintainers add him to their
author statement or a software-metadata file.

---

### 7. Software Name (MANDATORY)
`PLUME: Plasma in a Linear Uniform Magnetized Environment`

*Source:* The `README.md` H1 heading text (line 3), reused as the `INSTALL.md` H1 and as the RNAAS
code paper title.

**Rejected alternative: the bare `PLUME`.** That is the repository name, and SoMEF reports
`name: PLUME` with `full_title: PLUME: Plasma in a Linear Uniform Magnetized Environment`. The
expanded form is the better catalogue entry — it is what the maintainers lead with, and it makes the
acronym searchable — so the short form is not a candidate.

---

### 8. Description (MANDATORY)

```
PLUME (Plasma in a Linear Uniform Magnetized Environment).

PLUME is a serial Fortran solver for linear electromagnetic dispersion relations in homogeneous, nonrelativistic magnetized plasmas. Populations may be combinations of drifting kinetic bi-Maxwellians or cold fluids. Parallel drifts and kinetic temperature anisotropy are supported. Given a wavevector and plasma state, PLUME calculates complex mode frequencies, continues solutions through wavevector and/or parameter scans, and outputs electromagnetic polarizations, species density/velocity perturbations, and signed absorption/emission for kinetic populations.

JET-PLUME (Judging Energy Transfer in a Plasma in a Linear Uniform Magnetized Environment) is an extension that ships and installs with PLUME. It predicts wave-particle energy transfer in velocity space using the field-particle correlation technique and linear theory, producing the perturbed distribution function and the velocity-space energy transfer for each electric field component, in either gyrotropic or Cartesian velocity coordinates.

An overview of the code can be found in README.md, with details on the inputs and outputs in docs/input.md and docs/output.md files respectively.

The code is written in Fortran, with instructions for installation in the docs/INSTALL.md file.

The output data is in ASCII format, and can be plotted with gnuplot, matplotlib, or any other standard visualization methods. An optional Python wrapper (linfpclib) writes input files, calls the executable, and loads results for use in a Jupyter notebook, and the bundled SWIFT tool renders static and animated 3D views of a reconstructed eigenmode.

An example .in input file is found in the inputs/example/ subdirectory, along with a .sh file to illustrate the execution of the code.

The kinetic equations evaluated by PLUME are found in Klein, Howes, and Brown 2025 RNAAS.
```

*Source:* The project's v.2.0.0 README lead for the solver paragraph, within a corrected and extended
revision of the description originally published in HSSI, which was itself the Zenodo v.1.0.1
abstract (`10.5281/zenodo.15215514`) with its HTML stripped and its one hyperlinked sentence dropped.

**Brought forward for release v.2.0.0.** HSSI held the following text until this update. It was
correct for v.1.2.0, and is reproduced so a later reader can see exactly what changed:

```
PLUME (Plasma in a Linear Uniform Magnetized Environment).

PLUME is a numerical solver for the hot plasma dispersion relation for a plasma with an arbitrary number of drifting bi-Maxwellian components. Each component is defined by its density, its drift velocity parallel to the mean magnetic field, and its parallel and perpendicular temperatures, and the solver identifies supported waves for any direction of propagation with respect to the background magnetic field. The code then varies the wavevector or the plasma parameters to trace dispersion relations for the identified solutions, and can supplementarily calculate heating rates, eigenfunctions, and the susceptibility tensor.

JET-PLUME (Judging Energy Transfer in a Plasma in a Linear Uniform Magnetized Environment) is an extension that ships and installs with PLUME. It predicts wave-particle energy transfer in velocity space using the field-particle correlation technique and linear theory, producing the perturbed distribution function and the velocity-space energy transfer for each electric field component, in either gyrotropic or Cartesian velocity coordinates.

An overview of the code can be found in README.md, with details on the inputs and outputs in input.md and output.md files respectively.

The code is written in FORTRAN90, with instructions for installation in the INSTALL.md file.

The output data is in ASCII format, and can be plotted with gnuplot, matplotlib, or any other standard visualization methods. An optional Python wrapper (linfpclib) writes input files, calls the executable, and loads results for use in a Jupyter notebook, and the bundled SWIFT tool renders static and animated 3D views of a reconstructed eigenmode.

An example .in input file is found in the inputs/example/ subdirectory, along with a .sh file to illustrate the execution of the code.

The full equations evaluated by PLUME are found in Klein, Howes, and Brown 2025 RNAAS.
```

Four changes were made, each confined to what the release made wrong or materially incomplete; every
other word, and the paragraph order, is kept.

1. **Materially incomplete — the solver paragraph (replaced with the project's current text).** The
   superseded second paragraph was taken from the pre-v.2.0.0 `README.md` §1, which described only
   drifting bi-Maxwellian components, each "defined by its density, its drift velocity … and its
   parallel and perpendicular temperatures". v.2.0.0 added cold-fluid and mixed kinetic/cold
   populations as the release's headline capability, and cold components have no temperature, so
   that paragraph now omits and partly misdescribes what the solver does. The project rewrote the
   README lead to cover it, and that text is adopted verbatim: the first three sentences are
   `README.md` lines 7–9 at `46864a4`, the fourth is its next paragraph (lines 11–13). Only that
   paragraph's closing sentence, "Details on models and limitations are available", which exists to
   carry two hyperlinks this plain-text field cannot hold, is left out.
2. **Wrong paths.** "input.md and output.md" → "docs/input.md and docs/output.md", and "the INSTALL.md
   file" → "the docs/INSTALL.md file": v.2.0.0 moved all three files into `docs/`, so the old root
   paths no longer exist. `README.md` and `inputs/example/` (with `run_example.sh`) are still where
   the text says.
3. **"FORTRAN90" → "Fortran".** At `46864a4` the sources require Fortran 2003 and 2008 features as
   well as Fortran 90 (Field 13), so "written in FORTRAN90" is no longer accurate; the project's own
   current wording is "a serial Fortran solver".
4. **"The full equations" → "The kinetic equations".** The RNAAS code paper gives the kinetic
   (bi-Maxwellian) equations. The cold-fluid response added in v.2.0.0 is not in it: the manual cites
   Verscharen & Chandran (2013) for it and documents the full set in `docs/models.md`,
   `docs/eigenfunctions.md` and `docs/heating.md` (`46864a4`). Claiming the paper holds the full
   equations would now send a reader looking for something it does not contain.

**Considered and not changed.** The JET-PLUME paragraph stays: the extension still ships and
installs with PLUME (`src/fpc.f90` is linked into `plume.e` at `46864a4`), and the paragraph claims
nothing for cold or mixed plasmas, for which v.2.0.0 documents that FPC "is not implemented"
(`docs/README-JETPLUME.md`). The wrapper/SWIFT sentence and the gnuplot reference stay: `linfpclib/`,
`SWIFT/` and the gnuplot scripts in `plotter/example/` all still ship (the manual calls the `.plt`
scripts "historical examples", which does not make the statement that output "can be plotted with
gnuplot" untrue). Replacing the whole description with the new README lead was rejected because the
stored text's remaining paragraphs — JET-PLUME, the wrapper, SWIFT, the example files — are still
accurate and carry information the README lead does not.

The earlier history of this field, from the Zenodo abstract to the text reproduced above, follows.

**The description originally published in HSSI (the Zenodo v.1.0.1 abstract), reproduced exactly so
a future reader can see what was corrected:**

```
PLUME (Plasma in a Linear Uniform Magnetized Environment).

PLUME is a numerical solver for the hot plasma dispersion relation for a plasma with an arbitrary number of drifiting bimaxwellian components. 

An overview of the code can be found in README.md, with details on the inputs and outputs in input.md and output.md files respectively.

The code is written in FORTRAN90, with instructions for installation in the install.md file.

The output data is in ASCII format, and can be plotted with gnuplot, matplotlib, or any other standard visualization methods.

An example .in input file is found in the inputs/examples/ subdirectory, along with a .sh file is illustrate the execution of the code.

The full equations evaluated by PLUME are found in Klein, Howes, and Brown 2024 RNAAS.
```

**Why that text is superseded, item by item.** The maintainers' own sentences, paragraph order and
voice are preserved; each difference is either a demonstrable factual correction or the addition of
capability the earlier text omitted.

1. **Factual error — the code paper's year.** The stored text says "Klein, Howes, and Brown 2024
   RNAAS". The paper is 2025: *Research Notes of the AAS* **9**, 102, published 2025-04-30 (Crossref
   record for `10.3847/2515-5172/add1c2`), and every in-repository citation of it
   (`README.md` §2, `tutorial.md` §1, `input.md`, `output.md`) says 2025. The error originates in the
   Zenodo abstract, not in HSSI.
2. **Wrong filename.** "install.md" → `INSTALL.md`, the actual tracked filename.
3. **Wrong directory.** "inputs/examples/" → `inputs/example/`, the actual tracked path.
4. **Typographical and grammatical errors in the source text.** "drifiting bimaxwellian" → "drifting
   bi-Maxwellian"; "a .sh file is illustrate" → "a .sh file to illustrate".
5. **Materially incomplete — JET-PLUME.** The stored text predates v.1.1.0 (2025-08-19), whose
   entire content was "Merging of JETPLUME into PLUME". JET-PLUME is now a shipped, installed,
   separately documented capability (`src/fpc.f90`, `README-JETPLUME.md`, `README.md` §5) that a
   prospective user cannot discover from the stored description at all.
6. **Materially incomplete — the Python wrapper and SWIFT.** `README.md` §4 documents two supported
   ways to run PLUME, one of which (the `linfpclib` wrapper plus `examplelinfpc.ipynb`) the stored
   text never mentions; `SWIFT/` is likewise absent.
7. **Under-described solver.** The added detail about per-component parameters, arbitrary propagation
   direction, parameter/wavevector scans, and the optional heating/eigenfunction/tensor outputs is
   taken directly from `README.md` §1 and the `heating`/`eigen`/`tensor` flags in `input.md`.

**A minimal variant was considered and rejected.** Applying only items 1–4 — fixing the year, the
two paths and the two typos while changing nothing else — would have removed every factual error but
left the description materially incomplete on JET-PLUME, `linfpclib` and SWIFT, so the fuller
revision was preferred.

**Deliberately omitted from the Zenodo abstract:** its sentence "A library of papers citing PLUME can
be found here.", whose meaning depended on a hyperlink that this plain-text field cannot carry. The
library itself is recorded under Field 27.

---

### 9. Concise Description (OPTIONAL, max 200 characters)
`PLUME solves the Vlasov-Maxwell hot-plasma dispersion relation for any number of drifting bi-Maxwellian components, and computes heating rates, eigenfunctions and velocity-space energy transfer.`

*Source:* Written from `README.md` §1 and §5; HSSI held no concise description before. 194
characters, within the field's 200-character limit.

**Why not simply truncate Field 8.** The first 150–200 characters of the description are consumed by
the parenthetical name restatement and the opening solver sentence, so an auto-generated preview
never reaches what the code actually produces. This wording front-loads the four things a searcher needs: the equation
system solved, the plasma model, and the two headline output classes (heating rates/eigenfunctions
from PLUME, velocity-space energy transfer from JET-PLUME). It is drawn from `README.md` §1 and
§5 and uses "Vlasov-Maxwell" with a plain hyphen rather than an en-dash to avoid a non-ASCII
character in a short preview string.

**Kept unchanged for release v.2.0.0.** The value does not mention the cold-fluid populations that
v.2.0.0 added, but every claim it makes is still true at `46864a4` — PLUME still solves the
Vlasov-Maxwell dispersion relation for any number of drifting bi-Maxwellian components, and still
computes heating rates, eigenfunctions and (through JET-PLUME, for all-kinetic plasmas)
velocity-space energy transfer — and a preview is legitimately lossy; the cold-fluid capability is
stated in the description's solver paragraph (Field 8). Adding it here would mean composing a new
sentence, and no project-authored one-line summary covering it fits in 200 characters: the README's
opening sentence (`README.md` line 7) is 132 characters but omits the populations, and the first two
sentences together run to 215.

---

### 10. Publication Date (RECOMMENDED)
`2025-04-14`

*Source:* GitHub releases API for `kgklein/PLUME` and the Zenodo version records.

**Replaces the stored value `2025-09-17`, which was the wrong date for this field.** Field 10 is the
"Date of first broadcast/publication … Used for the initial version of the software," and
`2025-09-17` is the release date of v.1.2.0 — the version Field 12 then recorded. Storing it in
Field 10 as well made the software appear to have had no existence before its third release. (Field
10 is untouched by later releases: v.2.0.0, 2026-11-20, is recorded in Field 12 only.)

**Why 2025-04-14.** The initial version is `v.1.0.0`, GitHub release name "PLUME Initial Release",
published 2025-04-14T21:42:15Z. The archival publication happened the same day: `v.1.0.1` ("Zenodo
Release") was published 2025-04-14T22:00:08Z, eighteen minutes later, and its Zenodo record
(`10.5281/zenodo.15215514`, the earliest version under the concept DOI) carries
`publication_date: 2025-04-14`. Both readings of "first publication" — first public release, and
first DOI-registered deposit — give the same date, so the value is unambiguous.

**Rejected alternatives:** `2023-01-12`, the GitHub repository creation timestamp reported by SoMEF
as `date_created` — repository creation is not publication, the first commit is 2023-01-18, and the
first tagged release is two years later. `2025-04-30`, the RNAAS code paper publication date — that
is the paper's date, and the paper is recorded in Field 14.

---

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** `https://zenodo.org`

*Source:* Confirmed by DataCite (`publisher: "Zenodo"` for `10.5281/zenodo.15215513`) and by the
GitHub–Zenodo release integration that produced all three version records. Field 11's guidance names
Zenodo as the correct entry for exactly this workflow.

A URL rather than a ROR is used because Zenodo itself has no ROR record — CERN, its host, does, but
substituting CERN would misidentify the publisher — and Field 11 explicitly permits a URL where no ROR
exists. HSSI already carries a `Zenodo` organization row with this identifier.

---

### 12. Version (RECOMMENDED)
- **Version Number:** `v.2.0.0`
- **Version Date:** `2026-11-20`
- **Version PID:** `https://doi.org/10.5281/zenodo.24407914`
- **Version Description:**

```
This major release extends PLUME to support cold-fluid species alongside kinetic bi-Maxwellian populations, with corresponding updates to the numerical methods, eigenfunction calculations, and documentation.

### New capabilities
- **Cold-fluid populations:** Support for fully cold and mixed kinetic/cold plasmas, including cold reference species, parallel drifts, and oblique propagation.
- **Normalization:** Support for both reference-gyroradius (`rho_ref`) and reference-inertial-length (`d_ref`) normalization. The latter permits cold-fluid calculations without requiring a finite reference temperature.
- **Numerical methods:** Improved evaluation of the plasma dispersion function using the Faddeeva implementation and adaptive caching of Bessel functions.
- **Diagnostics:** Extended eigenfunction, wave-energy, and heating calculations to mixed kinetic/cold systems.

### Compatibility
The existing `rho_ref` normalization remains the default for input files that do not explicitly select a normalization. The `d_ref` convention is required for cold-fluid calculations.

The documentation includes guidance for reproducing calculations using the numerical conventions of earlier PLUME releases.
```

*Source:* The current release, `v.2.0.0`, corroborated by four independent sources (git tag, GitHub
release, Zenodo and DataCite — set out below). It supersedes `v.1.2.0` (2025-09-17,
`https://doi.org/10.5281/zenodo.17148711`), which HSSI held until this update.

**Release evidence, all agreeing on v.2.0.0 / 2026-11-20.** Git tag `v.2.0.0` (lightweight) →
commit `46864a43a466458f881624af03a0cd251ef169f4`, "Merge pull request #44 from kgklein/kgk-cold-v00",
2026-11-20T20:13:14Z; it descends from `v.1.2.0` and from this file's Source Revision, and is the head
of `main`. GitHub release `v.2.0.0`, titled "PLUME 2.0.0", published 2026-11-20T22:18:58Z and labelled
**Latest**, not a pre-release. Zenodo record 24407914, title "kgklein/PLUME: PLUME
2.0.0", `version: v.2.0.0`, `publication_date: 2026-11-20`, `IsSupplementTo
https://github.com/kgklein/PLUME/tree/v.2.0.0`; DataCite for `10.5281/zenodo.24407914`, `version:
v.2.0.0`, `Issued` 2026-11-20, `IsVersionOf 10.5281/zenodo.15215513`, and the concept DOI now lists
it as its fourth `HasVersion`. PLUME is not on PyPI: the `plume` project there is an unrelated
web-application package (`https://github.com/JamesRamm/plume`), and `linfpclib` is not published. The full release history is `v.1.0.0` and
`v.1.0.1` (both 2025-04-14, both tagging `1e4baab`), `v.1.1.0` (2025-08-19, `f832462`), `v.1.2.0`
(2025-09-17, `81ac15d`), `v.2.0.0` (2026-11-20, `46864a4`).

**Why each sub-value is what it is.** The number is written as the tag writes it (`v.2.0.0`, with the
`v.` the stored `v.1.2.0` used), not as the release title's `2.0.0`. The date is the release's UTC
publication day; the tagged commit falls on the same UTC day. The PID is the v.2.0.0 version DOI —
not the concept DOI, which is Field 2. The description is the GitHub release body (mirrored in the
Zenodo abstract), filtered for a site user and otherwise verbatim: its opening `PLUME 2.0.0` heading
was dropped because it only repeats the release name; the "Documentation and validation" bullet
("Reorganized user documentation, expanded examples and numerical tests, and clarified input
parameters, output conventions, and numerical limitations") was dropped as documentation and test
housekeeping; and the closing "Documentation" section, two bare links to the documentation site and
the repository, was dropped as a pointer. The opening sentence's "and documentation" stays because
only whole items are trimmed. The second Compatibility sentence is kept because it tells a user that
results differ from earlier releases and how to reproduce the old ones.

**The superseded v.1.2.0 row,** kept here for reference: number `v.1.2.0`, date `2025-09-17`, PID
`https://doi.org/10.5281/zenodo.17148711`, description "This new version splits the n = \pm 1
cyclotron resonances into separate components, rather than keeping the previous summation of the
two terms. This changes the column numbering scheme. See output.md for details." (the Zenodo v.1.2.0
abstract, with its literal `\pm`). Git tag `v.1.2.0` → `81ac15d6aa5eee43fa5fcb91df1ed9c28c4670c9`;
GitHub release "Updated Cyclotron Heating to Split positive and negative resonances", published
2025-09-17T23:40:54Z.

**The repository's own version declarations are still stale, and none of them names a release.**

- `Makefile` header comment: "VERSION 1.1 … LAST UPDATE: 2025/08/18", unchanged at `46864a4` although
  the file was rewritten for v.2.0.0. A hand-maintained comment, not a release.
- The manual's BibTeX block (`docs/index.md` at `46864a4`, formerly `ford_project.md`): `version =
  {v1.0.1}`, `doi = {10.5281/zenodo.15215514}`, with the note "The archived release predates some
  current capabilities." Stale, and spelled `v1.0.1` without the second dot.
- The README DOI badge pointing at `10.5281/zenodo.15215514` was removed in v.2.0.0.
- There is **no** `CITATION.cff`, no `.zenodo.json`, no `codemeta.json`, no `CHANGELOG.md`, and no
  version constant in `src/`, `linfpclib/` or `SWIFT/` at `46864a4`. `docs/reproducibility.md`
  refers to earlier releases as "PLUME 1.y.z" without naming a release itself.

**Commits after a release are not a release.** Before v.2.0.0, `main` carried 31 unreleased commits
after `v.1.2.0`, and this field correctly kept v.1.2.0 throughout. A future refresh should re-check
tags and releases rather than commit dates.

**Storage form — a trap for any later edit.** The version number is stored bare, as `v.2.0.0`, while
the view layer renders it as `<software name> - <number>`. The rendered string must never be written
back into this field, or the stored value is corrupted. The version description is stored as the
markdown block above; the site renders it as markdown under "Release Notes".

---

### 13. Programming Language (RECOMMENDED)

- Fortran90
- Fortran 2003
- Fortran 2008
- C
- Python 3.x

*Source:* File census of the working tree and of every branch in the repository, GitHub's language
statistics, SoMEF, and inspection of the sources themselves; re-derived at `46864a4` for release
v.2.0.0, which added the Fortran 2003, Fortran 2008 and C values and removed `Other`. HSSI held `Fortran90`,
`Python 3.x` and `Other` until this update.

**`Other` removed for v.2.0.0 (removal approved by the user on 2026-11-21).** `Other` was recorded
for three languages with no vocabulary row: gnuplot (the `plotter/example/*.plt` scripts), shell
(`run_example.sh`, `cycle.sh`, `run_swift_viz_example.sh`) and GNU make (the `Makefile`). None of the
three is a language this field records. Make and shell scripts are build and run tooling, which never
count, and `Other` is never a stand-in for a build system. The gnuplot scripts are example plotting
scripts, not the code that carries the science and not a supported front end with its own tests or
build target; at `46864a4` `docs/INSTALL.md` calls them "historical `.plt` examples" and names
Matplotlib as the plotting requirement. The software's real languages all have rows (the Fortran
standards, C, Python 3.x), so nothing is left for `Other` to represent. Do not restore it on the
strength of gnuplot, shell or make. The pre-v.2.0.0 reasoning for keeping it is preserved in the
`Other` bullet below as superseded history.

**Why v.2.0.0 adds Fortran 2003 and Fortran 2008.** The field records one row per Fortran standard
the sources actually require, taken file by file over the sources the build compiles. Before
v.2.0.0 a grep for post-1995 features returned nothing (see the Fortran90 bullet below). At
`46864a4` the release's new and rewritten modules use them throughout, and the `Makefile` `LFMOD` list
compiles every one of the files named here into `plume.e`:

- **Fortran 2003 features** — `use, intrinsic :: ieee_arithmetic` / `ieee_exceptions` /
  `iso_fortran_env` / `iso_c_binding`, `bind(C, name=…)` interfaces with `value` arguments,
  `abstract interface`, a type-bound `procedure :: export => export_scale` with a `class(...)` dummy,
  and `move_alloc`. Files whose latest feature is Fortran 2003: `auxiliary_normalization.f90`,
  `cold_reference.f90`, `cold_susceptibility.f90`, `harmonic_selection.f90`,
  `heating_response.f90`, `kinetic_core.f90`, `plasma_z_backend.f90`, `plasma_z_faddeeva.f90`,
  `species_moments.f90`.
- **Fortran 2008 features** — `error stop`, `block … end block`, and `open(newunit=…)`. Files using
  them: `adaptive_kinetic.f90`, `bessel_cache.f90`, `disprels.f90`, `electromagnetic_fields.f90`,
  `fpc.f90`, `functions.f90`, `heating_diagnostics.f90`, `heating_energy.f90`, `scan_support.f90`,
  `vars.f90` (for example `vars.f90:420` `open(newunit=warning_unit, …)` and `:481` `error stop`), and
  `kinetic_collisional_species.inc`.
- **Still Fortran 90 only** — `bessel.f90`, `nrtype.f90`, `nrutil_trim.f90`, `plasma_z_legacy.f90`,
  `plume.f90` and the other `.inc` files, so `Fortran90` stays. The field is the union over the
  compiled sources, which is why all three rows are recorded rather than only the newest.
- The `Makefile` passes no `-std=` flag, so no standard is declared beyond what the features require.
  `Fortran 2023` is not a candidate: none of its features appears. `src/gk_disp_gf.f90` is still not
  in `LFMOD` and is not counted.

**Why v.2.0.0 adds C, and not C++.** v.2.0.0 evaluates the plasma dispersion function through Steven
G. Johnson's Faddeeva implementation, vendored unmodified as `third_party/faddeeva/Faddeeva.cc` and
`Faddeeva.h` (MIT license), plus a project-written ISO_C_BINDING bridge, `src/faddeeva_bridge.c`. The
`Makefile` compiles both with the C compiler as C99 — its `faddeeva.o` rule compiles
`third_party/faddeeva/Faddeeva.cc` with `$(CC) … $(FADDEEVA_CFLAGS) -x c`, where `FADDEEVA_CFLAGS =
-O3 -std=c99 -fno-fast-math`, and its `faddeeva_bridge.o` rule compiles `src/faddeeva_bridge.c` with
`$(CC) … $(FADDEEVA_CFLAGS)` — and links them into `plume.e`; `docs/INSTALL.md` lists "an
ordinary C99 compiler" as a build requirement; `third_party/faddeeva/README.md` says "Compile
Faddeeva.cc as C99 (cc -std=c99 -x c), not C++" and that no C++ standard library is required. Vendored
code the package compiles and calls to do its science counts, and this is the routine behind every
kinetic susceptibility, so `C` is recorded. GitHub's language bar reports `C++` 1.9% because Linguist
classifies the `.cc` extension as C++; that is the file name, not how the project builds it, so
`C++` is rejected.

**`Rust` and `Typescript` were previously published for this software and no evidence supports
either.** Across every branch and the full commit history
(`git log --all --pretty=format: --name-only`, deduplicated, then filtered) there is no `.rs`, `.ts`
or `.tsx` file, no `Cargo.toml`, no `Cargo.lock`, no `tsconfig.json` and no `package.json` — the
filtered search returns nothing. The remote branches are `main`, `gh-pages`, `JETPLUME`,
`JETPLUME_collisions`, `howes`, and `kgk-interp-scan`; only `gh-pages` contains any web assets, and
those 125 `.html`/`.css`/`.js` files are the FORD-generated documentation site plus vendored
third-party theme assets (FontAwesome webfonts, `tipuesearch`, `svg-pan-zoom.min.js`) — generated
output and third-party JavaScript, neither authored by the project nor TypeScript. GitHub's own
language statistics for the repository report `Fortran`, `Python`, `Gnuplot`, `Shell`, and
`Makefile`, with no Rust or TypeScript at any size. SoMEF reports the same five. Neither value is
recoverable from any source examined, so neither should be restored. At `46864a4` the
GitHub language bar adds `C++` and `C` (the Faddeeva files, above) and still shows no Rust or
TypeScript, and no `.rs`, `.ts` or `.tsx` file exists on `main`.

**The values recorded before v.2.0.0, and why** (read at the Source Revision; the Fortran-dialect
finding in the first bullet held until v.2.0.0, and the `Other` bullet is superseded; both are
covered above).

- **`Fortran90`** — nine `.f90` free-form sources totalling ~382 KB, built by the `Makefile` with
  `gfortran` (`-O3 -DDOUBLE -fdefault-real-8 -funroll-loops -ffast-math`), with `ifort` retained as
  a commented alternative. The dialect is genuinely Fortran 90/95, not later: a grep across all
  sources for `iso_fortran_env`, `select type`, `class(`, `associate(`, deferred-length
  `character(:)`, type-bound `procedure`, `abstract interface` and `=> null()` returns zero hits in
  every file. So `Fortran 2003`, `Fortran 2008` and `Fortran 2023` are not candidates, and
  `Fortran77` is wrong (the code is free-form with modules). `INSTALL.md` requires a "Fortran 90
  compiler".
- **`Python 3.x`** — ~180 KB of Python: `linfpclib/linfpc.py` (3216 lines), `linfpclib/linfpcplot.py`
  (619), `SWIFT/SWIFT.py` (1091), and two `.github/scripts/*.py`. Python 3 specifically:
  `from __future__ import annotations`, `dataclass`, `typing` subscripts and f-strings in
  `SWIFT.py`; the CI workflows pin `python-version: '3.10'`; `examplelinfpc.ipynb` was executed
  under Python 3.12.2. `Python 2.x` is not a candidate. v.2.0.0 adds
  `contours/plot_plume_resonances.py` (948 lines, `from __future__ import annotations`, dataclasses)
  and `linfpclib/_namelist.py`, and `docs/INSTALL.md` lists "Python 3" for the wrapper and analysis
  workflows.
- **`Other`** (superseded; removed for v.2.0.0, see above) — three build- and workflow-critical languages have no row in the vocabulary: **gnuplot**
  (~39 KB across five `plotter/example/*.plt` scripts, the documented visualization path in
  `tutorial.md` §4, and identified as `Gnuplot` by GitHub), **shell/bash** (`inputs/example/run_example.sh`,
  `plotter/example/cycle.sh`, `SWIFT/run_swift_viz_example.sh`, plus the `bash` requirement the
  notebook states for `os.system` calls), and **GNU make** (the `Makefile`, which `INSTALL.md`
  lists as a hard requirement). The earlier reasoning was that `Other` is the only way to represent
  them, so it stayed; it was rejected for v.2.0.0 because none of the three counts. At `46864a4`
  the five `plotter/example/*.plt` scripts are unchanged, `docs/INSTALL.md` describes them as
  "historical `.plt` examples" that "require gnuplot" while naming Matplotlib as the plotting
  requirement, and the build and run paths still rely on GNU make and shell scripts.

---

### 14. Reference Publication (RECOMMENDED)
`https://doi.org/10.3847/2515-5172/add1c2`

*Source:* The code paper: Klein, K. G., Howes, G. G., & Brown, C. R., "PLUME: Plasma in a Linear
Uniform Magnetized Environment," *Research Notes of the AAS* **9**, 102 (2025), published 2025-04-30.
`README.md` §2 instruction 3, `tutorial.md` §1, `input.md`, and `output.md` all direct users to cite
it, and `.github/scripts/add_plume_papers_to_ads_library.py` lists its bibcode `2025RNAAS...9..102K`
as a PLUME citation to track. Unchanged at `46864a4`: the README's "Citation and license" section
and the manual (`docs/index.md`) both say "For publications, cite the PLUME code paper", linking this
article, and the tracking script still lists the bibcode. The JET-PLUME paper (Field 27) describes
one component and the project does not ask users to cite it, so it does not displace this value.

**Previous value: `https://iopscience.iop.org/article/10.3847/2515-5172/add1c2`** — the publisher
landing page, which is the exact URL the repository links and which resolves to the same article. It
was corrected to the DOI form because Field 14's declared type is a DataCite DOI, so the DOI is the
schema-correct representation of this identifier; a DOI is also the durable form, since publisher
landing-page URL schemes change and DOIs do not. Crossref confirms the two forms identify one
article: `10.3847/2515-5172/add1c2` returns the matching title, the three authors with Klein's and
Howes's ORCIDs attached, *Research Notes of the AAS* volume 9 page 102, and a 2025-04-30 publication
date.

---

### 15. License (RECOMMENDED)
- **License:** `BSD 2-Clause "Simplified" License`
- **License URI:** `https://spdx.org/licenses/BSD-2-Clause.html`

*Source:* The repository `LICENSE` file, which is the plain BSD 2-Clause text, "Copyright (c) 2025,
Kristopher G. Klein and Gregory G. Howes". The name matches the live `License` vocabulary row exactly.
GitHub's license detection independently reports `bsd-2-clause` / SPDX `BSD-2-Clause`, and SoMEF
reports the same.

**Durable warning: Zenodo's legacy license field for this record is wrong, and DOI autofill copies
it.** Zenodo's legacy records API reports `metadata.license.id` as `cc-by-4.0` for v.1.0.1
(record 15215514) and `bsd-2-clause-netbsd` for v.1.1.0 and v.1.2.0 (records 16904910, 17148711).
Neither matches the repository. Resolving the same records through Zenodo's InvenioRDM
representation shows what is actually deposited: v.1.1.0 and v.1.2.0 carry
`rights: [{id: bsd-2-clause, title: BSD 2-Clause "Simplified" License}]`, so the
`bsd-2-clause-netbsd` string is a legacy-serializer artifact rather than a depositor error — but
**v.1.0.1 genuinely carries `cc-by-4.0`** in both representations, which is a real error in the
oldest deposit. DataCite mirrors this: `10.5281/zenodo.15215514` reports "Creative Commons
Attribution 4.0 International", while the concept DOI and the two later version DOIs report
`BSD 2-Clause "Simplified" License`. Consequence for a future refresh: **derive Field 15 from the
repository `LICENSE` file only.** A DOI-autofill pass keyed on the version DOI cited in the README
badge (v.1.0.1) will produce `Creative Commons Attribution 4.0 International`, which is a valid
HSSI License row and so will not be caught by vocabulary validation.

**Discrepancy inside the repository itself, noted so it is not mistaken for a licence change.** The
`LICENSE` file's copyright line names two holders (Klein and Howes), while the licence text
reproduced in `README.md` §6 names three (Klein, Howes, and Brown). The licence *terms* are
identical BSD 2-Clause in both places, so Field 15 is unaffected; only the copyright attribution
differs. SoMEF surfaces both variants. v.2.0.0 removed the README copy: at `46864a4` the README says
only "PLUME is distributed under the BSD 2-Clause license", linking the unchanged `LICENSE` file.

**The bundled MIT component does not change this value (checked for v.2.0.0).** v.2.0.0 vendors Steven
G. Johnson's Faddeeva implementation under `third_party/faddeeva/` with its own MIT `LICENSE`. The
README and manual state that PLUME is distributed under BSD 2-Clause "with the bundled Faddeeva
implementation retaining its separate MIT license", and `third_party/faddeeva/README.md` notes that
the MIT notice is retained alongside PLUME's licence. Field 15 records the software's own licence, so
it stays `BSD 2-Clause "Simplified" License`; GitHub still detects `BSD-2-Clause` for the repository.
The v.2.0.0 Zenodo record repeats the legacy-serializer artifact `bsd-2-clause-netbsd` described
above, while its DataCite record reports `BSD 2-Clause "Simplified" License`.

**On the License URI.** `https://spdx.org/licenses/BSD-2-Clause.html` is the URL carried by the HSSI
`BSD 2-Clause "Simplified" License` vocabulary row itself, so it is auto-populated rather than
derived here. DataCite reports a different but equivalent URI for the same licence,
`https://opensource.org/licenses/BSD-2-Clause`; do not substitute it, because the field's URI is
tied to the vocabulary row.

**Rejected:** `Other` (unnecessary — the canonical row exists) and any SPDX title not present as a
row (the field is a closed list despite its "copy the SPDX title" wording).

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- astrophysics
- plasma physics
- space physics
- plasma instabilities
- dispersion relation
- plasma waves
- field-particle correlation
- temperature anisotropy
- plasma heating
- cold plasma

*Source:* `astrophysics`, `plasma physics` and `space physics` are the repository's own GitHub topics
(`astrophysics`, `plasma-physics`, `space-physics`, also reported by SoMEF as `keywords`; unchanged
when the repository page was read on 2026-11-21); the other seven rest on the repository evidence
below. `cold plasma` was added for release v.2.0.0; the other nine were held by HSSI before it.

Keywords are stored lower-case and rendered Title Case, so they are written here in lower case and
compared on the stored identity. HSSI's `Astrophysics`, `Plasma Physics`, `Space Physics` are the same
three values as the first three above, not different ones — casing alone is never drift in this field.

**Basis for the remaining keywords.** `plasma instabilities` — the solver reports growing modes
(`γ > 0`) and the publication the developers designate as PLUME's prior description is about the
four proton temperature-anisotropy instabilities.
`dispersion relation` — the code's central object (`src/disprels.f90`, `output.md`
"dispersion_*.map" / ".roots"). `plasma waves` — `README.md` §1, "identify supported waves with any
direction of propagation". `field-particle correlation` — the named technique JET-PLUME implements
(`README-JETPLUME.md`, `src/fpc.f90`). `temperature anisotropy` — `alphS` = `T_⊥/T_∥` is one of the
six per-component input parameters (`input.md`). `plasma heating` — the `heating` flag and the
per-species power absorption/emission output with its Landau, transit-time and cyclotron
decomposition (`input.md`, `output.md`).

**`cold plasma`, added for v.2.0.0.** Cold-fluid populations are the release's headline capability:
"Support for fully cold and mixed kinetic/cold plasmas" (release notes), "PLUME supports
bi-Maxwellian and cold populations in mixtures" (`docs/models.md`, `46864a4`), selected by `tauS=0`
under the `d_ref` normalization, with cold susceptibility, cold-reference and fully cold dispersion
code (`src/cold_susceptibility.f90`, `src/cold_reference.f90`) and examples such as
`inputs/example/fully_cold_scan.in`. "Cold plasma" is the term a searcher looking for a cold-plasma
dispersion solver would type, and the project uses it itself ("kinetic and cold-plasma species",
`AGENTS.md`); the manual's own phrase, "cold-fluid populations", names the same model. No other field
carries it — the functionality vocabulary has no fluid-model value, and Field 22 has no matching row.
The live vocabulary had no row for it or any case, separator or plural variant, so `cold plasma` is
a new lower-case vocabulary row. `cold fluid` was considered and not used: it is the manual's
narrower wording for the population model, whereas `cold plasma` is the domain term. `kinetic
theory`, `wave energy` and `normalization` were not added: the first two are carried by Field 4
(`Models and Simulations: First Principles`, `Data Processing and Analysis: Analysis`) and the
existing `plasma heating`, and the third is a solver setting rather than a subject a searcher looks
for.

**Deliberately excluded, so these are not re-proposed.** `solar wind`, `fortran`, `theory` and
`wave polarization` all exist as HSSI keyword rows and all describe PLUME accurately, but Field 16 is
explicitly for keywords "not supported by other metadata fields" and each of these is already carried
by Field 5/22 (Solar Wind), Field 13 (Fortran90), or Field 4 (`Models and Simulations: Theory`,
`Data Processing and Analysis: Wave Polarization Analysis`). Also skipped: a velocity-distribution
keyword — the concept is central to JET-PLUME, but the vocabulary already contains the near-duplicate
pair `velocity distribution function` and `velocity distribution functions`, and there is no
principled basis for choosing one, so `field-particle correlation` carries the meaning instead
without minting or arbitrarily picking a row. `moments` and `particle moments` exist but duplicate
Field 4's `Data Processing and Analysis: Plasma Moments`.

---

### 17. Data Sources (OPTIONAL)
None.

*Source:* Code analysis of the solver, the wrapper and SWIFT. This emptiness is a finding, not a gap:
the software supports no external data source.

PLUME's only inputs are Fortran namelist text files that the user (or the `linfpclib` wrapper)
writes: `read_in_params`, `read_map_input`, `read_scan_input`, `read_guess_input` and
`read_radial_input` in `src/functions.f90` all open the `.in` file named on the command line, and the
`option 5` radial path reads `.rad` files that a helper function generates locally. There is no HTTP,
FTP, S3, HAPI, CDAWeb, Madrigal or archive client anywhere in the solver, the wrapper, or SWIFT.
The one network client in the repository, `.github/scripts/*.py`, queries the NASA ADS API to
maintain the project's citing-papers bibliography during CI — a documentation build step, not a data
input the software supports.

The `DataInput` vocabulary offers nothing that applies: `AMDA`, `CDAWeb`, `das2`, `FTP/FTPS Directories`, `GFZ`, `HAPI`, `HTTP/HTTPS Directories`, `Madrigal`,
`Observatory/Mission-specific`, `OMNIWeb`, `Other`, `S3/Cloud-aware`, `SSCWeb`, `TAP`,
`The Virtual Solar Observatory.`, `VirES`, `WDC`. Every row names an external archive, service or
transport that PLUME does not use. `Other` is rejected specifically: it would assert that the
software supports *some* unlisted data source, when the accurate statement is that it supports none —
it reads only its own input files. Re-checked at `46864a4` for v.2.0.0: the new modules, the
`contours/` plotting script and the wrapper changes add no network or archive client.

---

### 18. Input File Formats (RECOMMENDED)
- ascii

*Source:* The input files are plain-text Fortran namelists (`inputs/example/*.in`, `tests/*.in`), read
with list-directed namelist I/O in `src/functions.f90`; the radial-scan `.rad` files and the
`linfpclib` loaders (`load_plume_sweep`, `loadlinfpc*`, `loadeigen`, `loadmoms`) are likewise plain
text. No binary, CDF, FITS, HDF5, netCDF, JSON, csv, IDL.sav or Zarr reader exists anywhere in the
repository, so `ascii` is the complete answer rather than a partial one. Unchanged at `46864a4`:
v.2.0.0's new inputs are further namelist `.in` files (`inputs/example/`), the wrapper's new
`linfpclib/_namelist.py` parses the same text namelists, and `contours/plot_plume_resonances.py`
reads a plain-text `key = value` `.resplot` configuration plus PLUME's own text outputs.

---

### 19. Output File Formats (RECOMMENDED)
- ascii

*Source:* `output.md` and `README-JETPLUME.md` §4 specify every output as whitespace-delimited text
columns or row/column grids — `dispersion_*.map`, `dispersion_*.roots`, `*.modeN`, and the JET-PLUME
`.cpar`, `.cperp`, `.cparcart`, `.cperp1`, `.cperp2`, `.df1*` files. The Zenodo abstract agrees ("The
output data is in ASCII format"). Unchanged at `46864a4`: v.2.0.0's new outputs — the named-column
`.energy` companion, `.bessel` metadata and `.warn` warnings (`docs/output.md`) — are formatted
text written with ordinary formatted `open`/`write` (no `form='unformatted'` or stream access
anywhere in `src/`); `docs/output.md` pairs `.energy` with the Python text reader `load_plume_energy`.

**`Other` considered and rejected.** SWIFT writes GIF animations and PNG screenshots, and
`plotter/example/cycle.sh` produces LaTeX and PDF via gnuplot's TeX terminal. Those are figures — the
rendered products of the visualization tooling — not data formats in which the software emits
scientific results, and adding `Other` would imply an unlisted *data* output format that does not
exist.

---

### 20. Operating System (RECOMMENDED)
- Linux
- Mac

*Source:* `INSTALL.md` §"REQUIREMENTS AND DEPENDENCIES", `examplelinfpc.ipynb` cell 0, the CI
configuration, and the shell dependencies of the documented run paths. Both values exist in the live
`OperatingSystem` vocabulary.

**`Operating System Independent` was previously published for this software and overstates its
platform support.** Two independent maintainer-authored statements exclude Windows:

1. `INSTALL.md` §"REQUIREMENTS AND DEPENDENCIES" gives as its first requirement "A UNIX, Linux, or
   macOS operating system with a working shell."
2. `examplelinfpc.ipynb` cell 0: "You will need to be able to call a Bash terminal when the library
   executes commands like `os.system('*command*')`. This is the default behavior for most Jupyter
   Notebook installations on macOS and likely on Linux as well. Windows will likely require
   additional setup." This names macOS and Linux as the platforms where the documented Python
   workflow works out of the box, and singles Windows out as needing extra work.

Neither passage is silence about Windows; both are documented exclusions, so `Operating System
Independent` overstated the supported platforms. Supporting evidence: both GitHub workflows run on
`ubuntu-latest`; the documented run paths are shell scripts with `#!/usr/bin/env bash` and
`set -euo pipefail` (`SWIFT/run_swift_viz_example.sh`) or bare POSIX shell
(`inputs/example/run_example.sh`, `plotter/example/cycle.sh`); and the `Makefile` targets shell out to
`mv`, `rm -f` and `tar`.

**Why the narrower value was chosen even though the code would probably build on Windows.** gfortran,
GNU make and a POSIX shell are all obtainable on Windows through MSYS2, MinGW or WSL, so a Windows
build is technically plausible — the maintainers simply do not claim or test it. Field 20 asks for the
operating systems the software "can successfully be installed on," and what the project documents is
the UNIX family: "A UNIX, Linux, or macOS operating system with a working shell." The vocabulary has no `UNIX` row, so
`Linux` and `Mac` are the two rows that express that requirement, and CI exercises Linux only. The
documented position was recorded in preference to the technically plausible one, and `Windows` is not
added for the same reason. If the maintainers later document or test Windows support, this is the
field to revisit.

**Re-checked for release v.2.0.0; unchanged, though the evidence for `Mac` changed.** At `46864a4`
the rewritten `docs/INSTALL.md` no longer carries the "A UNIX, Linux, or macOS operating system"
requirement. It reads instead: "GNU Fortran/C 11.4.0 and GNU make 4.3 have been exercised on Linux
… Other platforms/compilers are not certified by the presence of an alternative Makefile rule." The
only CI workflows still run on `ubuntu-latest`. `Linux` therefore rests on documentation and CI.
`Mac` stays on package-specific evidence that the release did not touch: `examplelinfpc.ipynb`
(unchanged since before v.2.0.0) names macOS as the platform where the wrapper's shell calls work
by default, and its stored outputs were produced on a maintainer's Mac — the notebook's recorded
module path is `/Users/collinbrown/Documents/PLUME/linfpclib/linfpcplot.py`, a macOS home-directory
path for Collin Brown, an author. That other platforms are "not certified" is a statement about what the maintainers test,
not a statement that the software does not run on macOS, and the maintainers have run it there.
Removing `Mac` would hide the software from `os:"Mac"` searches although a maintainer runs it on that
platform. Windows remains unsupported for the reasons above; v.2.0.0's new C99 component is built
with `cc` and adds nothing for Windows.

---

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

*Source:* Inspection of the sources and the build.

They contain no architecture-specific code: no intrinsics, no assembly, no vendor libraries
(`LIBS=` is empty in the `Makefile`), and no architecture-conditional compilation. The only build
switch is compiler choice (`SYSTEM=GFORT` versus a commented `IFORT`). `GPU` and `HPC or HEC` are
specifically rejected: there is no CUDA, OpenACC, OpenCL, MPI or OpenMP anywhere in `src/` or the
`Makefile`, and the pre-v.2.0.0 `ford_project.md` claim that PLUME is "parallelised" was contradicted
by the build itself (see the corresponding note under Field 4). `x86-64` and `Apple Silicon arm64`
are not recorded in place of `CPU Independent` because nothing restricts the code to either.

Re-checked at `46864a4` for v.2.0.0: the README now calls PLUME "a serial Fortran solver", the
`ford_project.md` "parallelised" sentence is gone, and the release's new code adds no architecture
dependence. The bundled Faddeeva C99 code is portable C linked only against `libm` (`LIBS= -lm`);
its unused `USE_OPENLIBM` hooks are not enabled (`third_party/faddeeva/README.md`). The only
build-level special handling is floating-point (`-fno-fast-math` for the IEEE-sensitive modules,
`-fdefault-real-8`), which is not architecture-specific.

---

### 22. Related Phenomena (OPTIONAL)
- Solar Wind

*Source:* The repository's own source comments and documentation, cited below. Confirmed against the
live `Phenomena` vocabulary.

**Why `Solar Wind`.** It is the only phenomenon in the vocabulary that the repository itself names.
`src/vars.f90:279` heads its radial-scan variables "Variables for radial scan of solar wind
models"; `src/disprels.f90:1577` documents `radial_scan` as running "for a specified radial solar
wind model"; `input.md` and `src/plume.f90:168` describe `option 5`'s path as "set by solar wind
models". At `46864a4` the same source comments remain (`src/vars.f90:307`, `src/disprels.f90:1866`,
`src/plume.f90:177`), and no new phenomenon is named in the v.2.0.0 code, examples or manual. The
publication the code paper identifies as describing a simplified earlier version of
PLUME is titled "Predicted impacts of proton temperature anisotropy on solar wind turbulence."

**`Coronal Heating` considered and not selected.** The physics case for it is real: PLUME computes
collisionless damping rates decomposed into exactly the Landau, transit-time and cyclotron channels
that the coronal-heating problem turns on (`low_n`, `Ps_split`, `output.md` lines 115–135). It is not
selected because the repository never mentions the corona, coronal heating, or any coronal
application — in source, documentation, or example inputs (re-checked at `46864a4`). Selecting it
would be inference from the physics rather than evidence from the software. The developers' curated
citing-papers library (`https://ui.adsabs.harvard.edu/public-libraries/RWGonkVgRpOaTizvWwsjKg`,
rebuilt weekly by `.github/workflows/update_ads_library.yml`; 90 papers when read on 2026-11-21)
shows how PLUME is applied in the literature, but how
other authors apply a general solver is not evidence that the software itself addresses a
phenomenon, so it is not a basis for this field.

The remaining rows — `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`,
`X-ray emission` — have no support anywhere in the repository. Note that `Related Phenomena` is a
closed vocabulary, so phenomena PLUME addresses that have no controlled value (wave–particle energy
transfer, Landau damping, temperature-anisotropy instabilities) are carried in Keywords instead.

---

### 23. Development Status (RECOMMENDED)
`Active`

*Source:* The release and commit history described below. Confirmed against the live `RepoStatus`
vocabulary; the bare term is the value, without the repostatus.org description.

**Evidence.** The repostatus.org definition of `Active` is "Reached stable, usable state and being
actively developed", and both halves hold. *Stable and usable:* five tagged releases, each with a
GitHub release and a Zenodo DOI, spanning 2025-04-14 to 2026-11-20, plus a peer-reviewed code paper,
a full user manual, a quick start, and worked examples. *Actively developed:* v.2.0.0, a major
release, was published on 2026-11-20 after 30 commits on `main` since this file's Source Revision
(`21a3711..46864a4`, 2026-08-14 to 2026-11-20, two of them merged pull requests, #43 and #44); the
repository page read on 2026-11-21 shows no archived banner; two GitHub Actions workflows are live,
one of them on a weekly schedule. (Before v.2.0.0 the evidence was 31 commits after `v.1.2.0`, the
latest the 2026-05-12 merge of PR #42.)

**Rejected alternatives:** `WIP` — there are stable public releases, so it does not apply, even
though individual features are unfinished (`option 5` prints "under development", `option 3` is
deprecated and halts, and at `46864a4` several cold/mixed diagnostics are marked unsupported or
"not fully validated" in the manual's capability matrix). `Inactive`
and `Unsupported` — contradicted by 2026 commits. `Abandoned`, `Suspended`, `Moved`, `Concept` — all
contradicted by the release and commit history.

---

### 24. Documentation (RECOMMENDED)
`https://kgklein.github.io/PLUME/`

*Source:* The FORD documentation site deployed by `.github/workflows/doc.yml` to the `gh-pages`
branch, and set as the GitHub repository's `homepage`.

**Re-checked for release v.2.0.0.** The site root returns `200 text/html` and now serves the v.2.0.0
manual (its landing page describes "kinetic bi-Maxwellian and cold-fluid populations" and links the
User Manual and Quick Start); it is still the repository's homepage link, and `.github/workflows/doc.yml`
still deploys `docs_out` to `gh-pages` (now built by `scripts/build_docs.sh`). The value stands.

**HSSI previously published `https://kgklein.github.io/PLUME/page/INSTALL.html`,** one interior page
of this same site. Both URLs resolve, and that one does satisfy the "installation instructions" half of
the field, but the site root is the documentation landing page: it presents the
project overview and links every other page — Install, Tutorial, Input, Output, the JET-PLUME
README, the citing-papers list, and the generated API reference for all modules and procedures.
`INSTALL.md` names it as where "the documentation is automatically built and deployed". Field 24 asks
for "the documentation and installation instructions"; the root covers both, the interior page only
one.

**Durable warning — do not use `http://www.plume.space`.** `ford_project.md` sets
`base_url: http://www.plume.space`, which looks like an official project site. It is not one: the
URL returns a Namecheap parking page headed "Domain registration has expired." The FORD `base_url`
is stale configuration, and this domain must not be recorded in Field 24 or anywhere else.

---

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** `https://ror.org/027ka1x80`

*Source:* The acknowledgements of the RNAAS code paper
(`10.3847/2515-5172/add1c2`) read: "K.G.K. was supported in part by NASA grant 80NSSC19K0912.
G.G.H. was supported in part by NASA grants 80NSSC20K1273, 80NSSC24K0260, 80NSSC24K0552, and
80NSSC24K1241. C.R.B. was supported in part by an appointment to the NRC Research Associateship
Program at Plasma Physics Division in the Naval Research Laboratory."

The acronym is expanded per HSSI convention, and the expanded name plus ROR match an organization
row HSSI already carries. The repository itself contains no funding statement — `README.md` §2 asks
only for citation, not acknowledgement of a grant — so the code paper is the authoritative source.
Crossref carries no `funder` array for the paper, and neither Zenodo (`grants: null` on all three
version records) nor DataCite (`fundingReferences: []`) records any funding, so this could not have
been obtained from the DOI metadata.

**Considered and not recorded — a second funder for C. R. Brown.** His support is an appointment to
the NRC Research Associateship Program, which the National Academies of Sciences, Engineering, and
Medicine administers (ROR `https://ror.org/02eq2w707`) while the host agency provides the funds —
here the Naval Research Laboratory (`https://ror.org/04d23a975`, already an HSSI row) or the Office
of Naval Research (`https://ror.org/00rk2pe57`, also already an HSSI row). Because the
acknowledgement does not say who funds the appointment, recording any one of the three would assert a
funding relationship the primary source does not state, so no second funder is asserted. The three
ROR candidates are resolved above so that a later refresh with better evidence — a grant number, an
award page, or a funding statement naming the sponsor — can pick one without redoing the lookup.

**The JET-PLUME paper's funding statement, weighed for v.2.0.0 and not added.** Brown, Howes, Klein &
TenBarge (2026, Field 27) state: "C.R.B. and G.G.H were supported in part by NASA grant
80NSSC20K1273. C.R.B. was supported in part by an appointment to the NRC Research Associateship
Program at the Plasma Physics Division in the Naval Research Laboratory, administered by the
Fellowships Office of the National Academies of Sciences, Engineering, and Medicine. K.G.K. was
supported in part by NASA grants 80NSSC19K0912 and 80NSSC24K0171. J.M.T. was supported by NASA Grant
80NSSC23K0099." Every sentence funds a person, not the software, so none of it is a basis for adding
a funder or award; `80NSSC24K0171` (Klein) and `80NSSC23K0099` (TenBarge) are therefore not added.
The statement does settle who administers Brown's NRC appointment (the National Academies'
Fellowships Office), but it still does not name who funds it, so the paragraph above stands.

---

### 26. Award Title (OPTIONAL)

| Award Title | Award Number |
|---|---|
| National Aeronautics and Space Administration grant | 80NSSC19K0912 |
| National Aeronautics and Space Administration grant | 80NSSC20K1273 |
| National Aeronautics and Space Administration grant | 80NSSC24K0260 |
| National Aeronautics and Space Administration grant | 80NSSC24K0552 |
| National Aeronautics and Space Administration grant | 80NSSC24K1241 |

*Source:* The five grant numbers are quoted from the RNAAS code paper's acknowledgements (see
Field 25), which attributes `80NSSC19K0912` to K. G. Klein and the other four to G. G. Howes.

**Why the titles read this way.** No award *title* is published for any of these grants — the
acknowledgement gives numbers only, and NASA grant titles for these awards are not retrievable from
Crossref, DataCite, Zenodo, or the repository. Rather than invent titles, this uses the
funder-name-plus-"grant" form together with the bare grant number as the identifier, which is the
convention HSSI already uses for NASA grants whose titles are not published. The title string is 51
characters, well inside the 128-character limit that applies to an award name, so none of these
values risks a write failure.

**Not included:** any award for C. R. Brown's NRC Research Associateship. It is a fellowship
appointment with no award number in the acknowledgement, and its funder is unresolved (Field 25).

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

1. `https://doi.org/10.1063/1.4914933` — Klein, K. G., & Howes, G. G. (2015). Predicted impacts of
   proton temperature anisotropy on solar wind turbulence. *Physics of Plasmas*, 22, 032903.
2. `https://doi.org/10.1017/S0022377824000667` — Huang, R., Howes, G. G., & McCubbin, A. J. (2024).
   The velocity-space signature of transit-time damping. *Journal of Plasma Physics*, 90, 535900401.
3. `https://doi.org/10.1063/5.0335826` — Brown, C. R., Howes, G. G., Klein, K. G., & TenBarge, J. M.
   (2026). Phase-space energy transfer of wave–particle interactions using the field–particle
   correlation technique and linear plasma theory with JET-PLUME. *Physics of Plasmas*, 33, 072101.
   (Preprint: arXiv:2606.20865.)
4. `https://doi.org/10.1086/305770` — Quataert, E. (1998). Particle Heating by Alfvénic Turbulence in
   Hot Accretion Flows. *The Astrophysical Journal*, 500, 978–991.
5. `https://doi.org/10.1088/0004-637X/764/1/88` — Verscharen, D., & Chandran, B. D. G. (2013). The
   Dispersion Relations and Instability Thresholds of Oblique Plasma Modes in the Presence of an Ion
   Beam. *The Astrophysical Journal*, 764, 88.

*Source:* All five DOIs verified through Crossref (title, authors, venue, type `journal-article`) and
each resolves at doi.org; the repository evidence for each is below. Entries 1–2 were held by HSSI
before release v.2.0.0; entries 3–5 were added for it.

**Entry 3 — the developers' own paper about JET-PLUME (added for v.2.0.0).** Its abstract
introduces "JET-PLUME (Judging Energy Transfer in a Plasma in a Linear Uniform Magnetized
Environment), an extension of the PLUME Vlasov-Maxwell dispersion solver", the component PLUME has
shipped since v.1.1.0 (`src/fpc.f90`, `docs/README-JETPLUME.md`); three of its four authors are the
three people in Field 6; and its Data Availability statement points to `https://github.com/kgklein/PLUME`.
It is the JET-PLUME paper the pre-v.2.0.0 `README.md` §5 listed as "[... Work in Progress]"; it was
published in July 2026 (ADS `2026PhPl...33g2101B`), and v.2.0.0 removed that placeholder without
citing it. A paper by the software's authors whose subject is the software is exactly what this
field is for.

**Entries 4–5 — the publications the v.2.0.0 manual presents as the solver's basis (added for
v.2.0.0).** At `46864a4` the manual's "Authors, scientific references and citation" section
(`docs/index.md`) is the project's reference list, and it names five works: "The kinetic solver
descends from Quataert (1998) and Gregory Howes's Fortran adaptation. Its kinetic equations follow
Stix, *Waves in Plasmas*, Chapter 10 … The cold drifting response follows Verscharen & Chandran
(2013), Section 2.1. The selected kinetic heating channels are discussed in the PLUME code paper and
Huang et al. (2024)." Quataert (1998) is linked to its ADS record (`1998ApJ...500..978Q`); Verscharen &
Chandran (2013) is linked to its arXiv preprint (`1212.5192`, published as ApJ 764, 88) and cited again
in `docs/numerics.md`. Quataert's paper presents the original solver PLUME's kinetic core derives
from, and Verscharen & Chandran's §2.1 is the cold-fluid response v.2.0.0 implements
(`src/cold_susceptibility.f90`). Both are method papers the code implements, presented by the project
as such, so both qualify. Judged as a list, the basis papers come to four — these two, Klein & Howes
(2015) and Huang et al. (2024); Stix is a textbook and the code paper is Field 14 — each tied to a
distinct core capability (the kinetic solver's origin, its earlier version, its heating channels, its
cold-fluid response), so the list stays short and every entry explains something a visitor would
want to know.

**Superseded rejection of Quataert (1998).** Before v.2.0.0 this field rejected Quataert (1998)
because "the repository names the person, not the paper: no DOI, no year, no link anywhere in the
tree", and because it "describes a predecessor implementation rather than PLUME". The first reason no
longer holds: the v.2.0.0 manual cites the paper by year and links its ADS record in its reference
list. The second does not exclude it: a paper the project presents as the origin of its solver is a
basis paper, which is what admits it.

**Entry 1 — designated a PLUME reference by the repository's own automation.** The repository treats
this paper as a citable PLUME reference in code, not just in prose:
`.github/scripts/print_bib_markdown.py` sets `PLUME_ADS_BIB_CODE = "2015PhPl...22c2903K"`, and
`.github/scripts/add_plume_papers_to_ads_library.py` lists that bibcode alongside the code paper's
(`2025RNAAS...9..102K`) as the two bibcodes whose citations constitute "papers citing PLUME".
`SWIFT/SWIFT.py` (lines 28–31) cites its preprint, arXiv:1503.00695, for the complex-frequency
convention and the sign interpretation of `γ`. The RNAAS code paper states that "a simplified
version of PLUME was described in" Klein & Howes — i.e. this paper describes an earlier version of
the software, which is squarely what Field 27 is for.

**Entry 2 — cited in the repository as the basis of an implemented feature.** `input.md` documents
the `low_n` flag as separating "Landau, Transit, and Cyclotron damping" and hyperlinks this paper as
what the implementation "follows", alongside §5 of the code paper. It is a developer-prioritized
citation for a specific capability, linked from the documentation rather than merely named.
At `46864a4` the manual cites it in its reference list (`docs/index.md`) and in `docs/heating.md`
for "the selected kinetic heating channels", and the repository's automation still tracks Entry 1's
bibcode (`.github/scripts/add_plume_papers_to_ads_library.py`) while `SWIFT/SWIFT.py` still cites its
preprint, so neither incumbent's basis changed.

**Considered and not included, with reasons.**

- *"Howes (2017)".* `examplelinfpc.ipynb` cell 0 says the notebook predicts "the signatures found in
  Howes (2017), a kinetic Alfvén wave experiencing Landau damping," and names the run `howes2017` —
  but gives no journal, volume or DOI, and at least three papers fit the author-year: Howes, G. G.
  (2017), "A prospectus on kinetic heliophysics," *Phys. Plasmas* 24, 055907; Howes, Klein & Li
  (2017), "Diagnosing collisionless energy transfer using field–particle correlations:
  Vlasov–Poisson plasmas," *JPP* 83, 705830102; and Howes, McCubbin & Klein (2018) on Landau damping
  in current sheets. Selecting one would be a guess. **Recorded here so a future agent does not
  re-derive this dead end** — resolving it requires asking the maintainers, not more searching.
- *Stix, T. H., "Waves in Plasmas".* The theoretical basis (`README.md` §1 cites Chapter 10,
  Eqns. 66–73) and the most-cited reference in the code paper, but a monograph rather than a
  publication with a DOI or a stable APA-plus-permalink form.
- *Fried & Conte (1961), "The Plasma Dispersion Function".* Cited by the code paper for the plasma
  dispersion function that `zet_in` evaluates; again a monograph, and one step further removed.
- *The project's ADS citing-papers library*
  (`https://ui.adsabs.harvard.edu/public-libraries/RWGonkVgRpOaTizvWwsjKg`). This is a live,
  weekly-refreshed list of third-party papers citing the two PLUME bibcodes, rendered into the
  documentation site as a "Papers citing PLUME" page. It is genuinely developer-curated, but it is a
  bibliography of citing works rather than a set of publications the developers single out, its
  membership changes without any repository change, and Field 27 expects individual DOIs. The library URL is recorded here as context for a future refresh; it
  is not a Field 27 value.
- *Papers that use PLUME* — none added, because PLUME is too widely used for a list of users to
  help a searcher. That library, which the v.2.0.0 manual presents as "Publications using PLUME", held 90 papers when
  read on 2026-11-21 (last modified 2026-08-14), spanning
  2014–2026, and v.2.0.0's manual links it and a SciX mirror
  (`https://scixplorer.org/public-libraries/LR2P1ENiTgO8Z-vBM_35DA`). A searcher is better served by
  that library than by a hand-picked subset here. The search for v.2.0.0 covered papers that entered
  ADS since this record's 2026-08-10 extraction date and cite either tracked bibcode
  (`2025RNAAS...9..102K`, `2015PhPl...22c2903K`) or mention PLUME in the full text with "dispersion"
  (controls: a nonsense token returned 0 hits; a comparable solver name returned hits). Weighed and
  not added, so a later refresh does not rediscover them as new:
  - substantive uses with methods statements naming PLUME — Martinović et al. (2026), *PRL* 136,
    255201 (`10.1103/nlq9-2g37`); Qian et al. (2026), *ApJ* 1008, 244 (`10.3847/1538-4357/ae9a74`);
    López et al. (2026), arXiv:2611.21929;
  - citations or mentions only — Klein et al. (2026), *Sol. Phys.* 301, 167 (cites the code paper among
    bi-Maxwellian solvers); Schröder et al. (2026), *JPP* 92, E130 (results "also replicated by …
    PLUME"); van der Holst et al. (2026), *ApJ* 1008, 16 (PLUME named for future work); Gaelzer et al.
    (2026), arXiv:2611.07220, and Bai & Xie (2026), *CPC* 327, 110281 (PLUME in lists of solvers);
    Dhamane et al. (2026), *A&A* 713, A126 (cites a PLUME paper; its arXiv text never names PLUME);
    Kumbhar et al. (2026), *ApJ* 1007, 166, and Guo et al. (2025), *PRL* 135, 185201 (cite Klein &
    Howes 2015; an ADS full-text query for PLUME in them returned nothing).

---

### 28. Related Datasets (OPTIONAL)
- `https://doi.org/10.5281/zenodo.19225024` — Brown, C., Howes, G., Klein, K., & TenBarge, J.
  (2026). Input files for: Phase-Space Energy Transfer of Wave-Particle Interactions using the
  Field-Particle Correlation Technique and Linear Plasma Theory with JET-PLUME. Zenodo dataset.

*Source:* The Data Availability statement of the JET-PLUME paper (Field 27): "Inputs can be found at
https://doi.org/10.5281/zenodo.19225024." Added for release v.2.0.0; HSSI held no related dataset
before it.

**Why it belongs.** It is the supplementary data of the software's own paper: the deposit's README
says it "contains input files and run configurations used to generate the results presented in the
above manuscript", namely the JET-PLUME, Gkeyll and AstroGK parameter files behind the paper's
comparisons. A user who wants to reproduce the paper's JET-PLUME results, or to see worked
field–particle-correlation inputs (which the v.2.0.0 manual says are still missing from the
repository: "A curated standalone public FPC lesson is still outstanding", `docs/README-JETPLUME.md`),
finds them there. DataCite types it `Dataset`; it resolves at doi.org.

**Why the version DOI.** `10.5281/zenodo.19225024` is the only version (2026-03-25) under concept
`10.5281/zenodo.19225023`, and it is the DOI the paper cites. A paper's supplementary data is a fixed
deposit tied to that paper, so the exact cited deposit is recorded; the concept DOI is noted here in
case a later version appears.

**Everything else is still correctly absent.** PLUME generates its own data rather than analysing
published datasets, and it reads no dataset at all (Field 17). The repository does ship output files
— `data/example/dispersion_map_par.map`, `.roots`, and `map_par_kpar_1_10000.mode1`–`mode3`, plus,
from v.2.0.0, `dispersion_map_high_beta_par.map`/`.roots` — but `data/README.data` and the tutorial
present them as example products for the shipped plotting scripts. They have no DOI, no landing page,
and no separate archival identity: they are versioned inside the code deposit, so they are covered by
the software's own DOI rather than being a related dataset. Zenodo and DataCite record no dataset
relation for any version, v.2.0.0 included (the only `relatedIdentifiers` are `IsSupplementTo` links
to the matching GitHub tag, plus the concept/version links).

---

### 29. Related Software (OPTIONAL)
None.

*Source:* Every software relationship the repository or its code paper asserts was examined; none
qualifies. This is a researched negative result, not an unfilled field.

**Predecessors — real, but with nothing citable to point at.** `README.md` §1: "This code is based
upon a F90 adaptation by Greg Howes of a solver originally by Eliot Quataert." `src/plume.f90` case 3
refers to "Gullveig (the precursor of this code)". `src/functions.f90` lines 1043–1052 record that
four namelist-reading utilities (`get_indexed_namelist_unit`, `input_unit_exist`, `get_unused_unit`,
`input_unit`) "were all adopted from the Astrophysical Gyrokinetic Code (AGK)". Field 29 wants a
software DOI or, failing that, a code repository URL. The Quataert solver and Gullveig have no public
repository or software DOI; AstroGK has a peer-reviewed paper
(*J. Comput. Phys.* 229, 9347, DOI `10.1016/j.jcp.2010.09.006`) but no locatable public code
repository or software DOI, and Field 29 explicitly redirects publication DOIs to Field 27. The AGK
borrowing is also four input-parsing helpers copied into the tree, not a dependency and not a fork.
**Recorded so a future agent does not repeat this search.**

**Similar-purpose solvers deliberately not asserted.** Other Vlasov–Maxwell dispersion solvers exist
and would be genuinely useful neighbours for a reader (ALPS, NHDS, LEOPARD, WHAMP and others). At the
Source Revision none was named anywhere in the repository: a grep across every source file,
documentation file, example and the notebook returned nothing for any of those names (v.2.0.0 adds
NHDS as a test reference only; see below). The code paper's abstract acknowledges that "many
numerical methods for solving the Vlasov–Maxwell dispersion relation … have been implemented" without
naming one, and its indexed reference list (Crossref for `10.3847/2515-5172/add1c2`, ADS
`2025RNAAS...9..102K`) has three entries — Fried & Conte (1961), Huang et al. (2024) and Stix (1992) —
none of them a comparable solver. Listing a comparable solver here would assert a relationship
neither the repository nor its code paper makes. Cross-linking PLUME to peer tools would be a
deliberate curatorial choice rather than something the available evidence supports.

**Generic infrastructure excluded** per the field's relevance gate: numpy, matplotlib, PyVista,
gnuplot, GNU make, LaTeX and ImageMagick are all present in the workflows and all fail the "would
this be equally at home in a web app, a finance model, or a biology pipeline" test.

**Candidates introduced by release v.2.0.0, weighed and not added** (read at `46864a4`):

- *Steven G. Johnson's Faddeeva Package* (original `https://ab-initio.mit.edu/Faddeeva`, vendored
  from the `JuliaMath/openspecfun` mirror, `third_party/faddeeva/README.md`). PLUME now compiles it to
  evaluate the plasma dispersion function, but it is a generic special-function library — the
  Faddeeva function serves optics, spectroscopy and statistics as much as plasma physics — so it is
  generic numerical infrastructure, excluded however prominent. It is credited in Field 13 (`C`) and
  Field 15's note instead. The mirror repository is a mirror, not the upstream project, and would not
  qualify either.
- *NHDS* (the New Hampshire Dispersion relation Solver, Verscharen & Chandran 2018). v.2.0.0's test
  suite re-implements its susceptibility formulas as an independent test oracle
  (`tests/mixed_reference.py`: "Independent test-only NHDS/Stix bi-Maxwellian harmonic sum … The
  Y-tensor formulas follow NHDS src/suscep.f90"), and `docs/development.md` lists "NHDS/Stix tensor
  references" among the tests. That is a validation reference inside the test suite, not a statement
  that NHDS is an alternative to PLUME or performs PLUME's task for a user, and nothing NHDS provides
  is built or run by PLUME. It is the first similar-purpose solver the repository names (the paragraph
  above was written when none was), but being named as a test reference does not make it related
  software. Revisit if the documentation ever presents NHDS (or ALPS, which the manual still does not
  name) as an alternative or companion. Neither NHDS nor ALPS is in the HSSI catalogue (search on
  2026-11-21).
- *Verscharen & Chandran (2013)* is the method paper for the cold-fluid response, which belongs in
  Field 27 (entry 5), not here.
- *AstroGK* is still named only for the four input-parsing helpers in `src/functions.f90` (now lines
  1140ff), and the JET-PLUME paper uses it only as a comparison simulation code; neither is a relation
  this field records.

---

### 30. Interoperable Software (OPTIONAL)
None.

*Source:* Researched and correctly empty.

PLUME is a self-contained command-line executable whose entire interface is its own Fortran namelist
input files and its own ASCII output tables. There is no adapter or converter API, no shared or
convertible data model with another domain package, no plugin or extension relationship, no
companion package, and no bridge to a named domain tool such as SPEDAS or a MATLAB interface. The
components that *do* consume PLUME's output — `linfpclib`, `plotter/`, `SWIFT/` — ship inside this
same repository and are part of this software, not separate peer tools it interoperates with.

**Candidates considered, and why each fails the gate.** numpy, matplotlib and PyVista are
generic infrastructure — arrays, plotting, 3D rendering — equally at home outside heliophysics, so
being a dependency of them says nothing about PLUME. gnuplot, LaTeX/pdflatex and ImageMagick
(`plotter/example/cycle.sh`) are likewise generic tooling. Jupyter is the closest call: `README.md`
§4 documents running the wrapper via `jupyter notebook`, `examplelinfpc.ipynb` ships as the worked
example, and `ford_project.md` links it — but "can be driven from a notebook" is true of most Python
code and identifies no exchange with a peer scientific tool, which is what this field records. The
NASA ADS API used in CI is a web service, not software this package interoperates with. There is no
Tier-B case here supported by a specific documented exchange, so the field is correctly empty.

Re-checked at `46864a4` for v.2.0.0: the bundled Faddeeva implementation is compiled into the
executable rather than exchanged with (and is generic numerical code in any case, Field 29); NHDS is
used only as a test oracle; SciPy, NumPy, Matplotlib and mpmath appear only in tests and plotting
(`docs/INSTALL.md`); and the release adds no adapter, converter or plugin interface. The field stays
empty.

---

### 31. Related Instruments (OPTIONAL)
None.

*Source:* An explicit search of the repository for instrument and mission names, detailed below. This
is a documented omission, not an unresolved lookup.

PLUME is instrument-agnostic by construction: it solves the dispersion relation for a uniform
magnetized plasma described entirely by dimensionless parameters (`betap`, `kperp`, `kpar`, `vtp`,
and six per-component ratios). It reads no instrument data, implements no instrument-specific format
or convention, and is not an instrument-team tool. A search of every `.f90`, `.md`, `.py`, `.in`,
`.plt`, `.sh`, `.yml` file and the `Makefile` for instrument and mission names — MMS, THEMIS,
Cluster, Wind, Parker Solar Probe/PSP, Solar Orbiter, ACE, Ulysses, Helios, Voyager, Juno, Cassini,
MAVEN, Van Allen Probes/RBSP, Geotail, Polar, FAST, SDO, AIA, GOES, Hinode, IRIS, STEREO, and the
instrument acronyms SWEAP, FIELDS, SPAN, FPI, FGM, MFI, SWE, 3DP, EMFISIS — returns only false
positives on ordinary English (`fields`, `fast`, `span`, `windows`, "solar wind"). Nothing is being
omitted for want of resolution — there is nothing to resolve — and no entry may be recorded in this
field without a `https://spase-metadata.org/` identifier. Re-checked at `46864a4`: v.2.0.0's new
sources, examples and manual name no instrument or mission. (Several later papers apply PLUME to
Parker Solar Probe, Wind or Solar Orbiter measurements — see Field 27 — but that is how others use a
general solver, not a capability of the software.)

---

### 32. Related Observatories (OPTIONAL)
None.

*Source:* The same search described under Field 31. No mission, observatory or spacecraft is named
anywhere in the repository.
The nearest thing to a platform association is `option 5`'s radial path through "solar wind models" —
which is a model, not an observatory, and is captured by Field 5 (`Solar Wind`) and Field 22
(`Solar Wind`) instead. No name is recorded here without a `https://spase-metadata.org/` identifier.

---

### 33. Logo (OPTIONAL)
`https://raw.githubusercontent.com/kgklein/PLUME/11da73ac1e3628ae0ec8b433ed37880207857c71/PLUME_logo.png`

*Source:* `PLUME_logo.png` at the repository root, embedded by `README.md` line 7 and copied into the
documentation site by `.github/workflows/doc.yml`.

**HSSI previously published `https://github.com/kgklein/PLUME/blob/main/PLUME_logo.png`, which does
not serve an image.** A `/blob/` URL is GitHub's HTML file-viewer page: requesting it returns
`Content-Type: text/html` and a roughly 216 KB HTML document, so anything rendering it as an image
gets nothing. The `raw.githubusercontent.com` form of the same file returns `Content-Type: image/png`
and the actual 672,580-byte asset. The recorded URL is 103 characters, well inside the 200-character
limit that applies to a URL field.

**Why the commit is pinned rather than the branch.** An earlier revision of this record used the
branch form `.../kgklein/PLUME/main/PLUME_logo.png` and reasoned that pinning would "silently freeze
the catalogue image to one revision" while the branch form keeps working if the maintainers update
the logo. That reasoning is rejected. A branch's mutability is not a feature here but the fragility
being avoided: the URL breaks silently the moment the file is renamed, moved or deleted, and Field
33's "stored online in a permanent place" wording is a requirement about the URL, not only about the
file. A logo redesign is something a metadata refresh should notice and record deliberately, not
something the catalogue inherits unannounced. Only the commit-pinned URL above is recorded, so that
no superseded candidate can later be mistaken for a live alternative.

**Re-checked for release v.2.0.0; the stored URL stands.** v.2.0.0 moved the file to
`docs/assets/PLUME_logo.png`, where the README (`46864a4`, line 5) and the manual's landing pages
embed it. The image itself is unchanged — the blob at the pinned commit and at `46864a4` is the same
object, `6310ea22c9c028c07addccf8eba9e1200240e1d2` — and the pinned URL above still returns
`image/png`, 672,580 bytes. Because the URL is pinned to a commit, the move did not break it, which
is exactly why it was pinned; repointing it at the new path would change nothing a user sees. No new
logo has been adopted.

**Not selected: `Jet-Plume_Logo.svg`.** SoMEF reports this file as the repository's `logo`, but it is
the logo of the JET-PLUME sub-component (`README.md` §5, `README-JETPLUME.md`), not of PLUME.
`PLUME_logo.png` is the image the README leads with. Also present at the repository root and not
candidates: `qrcode_plume_github.png` (a QR code pointing at the repository), `favicon.ico`, and the
`.xcf` GIMP sources for the logo and QR code. (At `46864a4` the SVG and the QR code also live under
`docs/assets/`; the `.xcf` sources and `favicon.ico` remain at the root.)

---

## Additional context not captured by any field

**v.2.0.0 adds a large test suite but still no test workflow.** At `46864a4` `tests/` holds dozens
of `unittest` modules, Fortran probes and development reports (`docs/development.md`: "Tests include
independent cold fluid/current solutions, NHDS/Stix tensor references, SciPy/Faddeeva and optional
arbitrary precision …"), run by hand with `python3 -m unittest discover -s tests`. `.github/workflows/`
still contains only `doc.yml` and `update_ads_library.yml`, so CI still runs no tests.

**Editable GIMP sources ship alongside the images.** `PLUME_logo.xcf` (1.6 MB) and
`qrcode_plume_github.xcf` are tracked in the repository, so the logo is maintainable upstream.

**A gyrokinetic dispersion module is present but not built.** `src/gk_disp_gf.f90` (1022 lines,
"Gyrokinetic Dispersion Relation Functions", "Copyright, 2005 Greg Howes") implements a separate
gyrokinetic dispersion relation with collisional, hyperviscous, Krook and bi-Maxwellian/bi-kappa
options. It is **not** in the `Makefile`'s `LFMOD` object list, so it is not compiled into `plume.e`
and none of its routines is reachable from `src/plume.f90`. It is therefore excluded from the Field 4
functionality classification — a future refresh should re-check whether it has been wired into the
build before crediting gyrokinetic or bi-kappa capability. Re-checked at `46864a4`: still present,
still absent from `LFMOD`.

**Before v.2.0.0 a test workflow was documented but did not exist.** At the Source Revision
(`21a3711`), `INSTALL.md` told contributors that "GitHub will run automatic tests (via workflows) to
ensure that the changes do not break the code", but `.github/workflows/` contained only `doc.yml` and
`update_ads_library.yml`, and `tests/` held two input files (`2D-scan-test.in`, `drift_cbe_test.in`)
and no harness. v.2.0.0 removed that promise and added the test suite described in the paragraph on
v.2.0.0 above; CI still runs no tests. None of this changes Field 23, but it is worth knowing before
citing CI as evidence of testing.

**PyHC registry: not a member.** No entry in any of the three PyHC registry files —
`projects_core.yml`, `projects.yml`, `projects_unevaluated.yml` in
`heliophysicsPy/heliophysicsPy.github.io/_data/` — matches PLUME, JET-PLUME, `linfpclib`, or the
repository URL `https://github.com/kgklein/PLUME`. No curated PyHC metadata is therefore available for
this software, and absence from those registries is expected for a Fortran-first package. PyHC
membership is not a prerequisite for anything in this record. Re-checked on 2026-11-21: still no
match in any of the three files.
