# HSSI Metadata Extraction Results

**HSSI Software ID:** 59c24c09-5ecd-44c8-a324-5a7da62c634b
**Repository:** https://github.com/kgklein/PLUME
**Source Revision:** 21a3711745d5fb6d8f147d4ca773a9db7508924d
**Extraction Date:** 2026-08-10
**Validation Date:** 2026-08-10
**Validation Status:** PASS

---

**Scope note — read this before the field evidence.** PLUME is a single-executable Fortran 90
dispersion-relation solver, not a data-analysis package. Three consequences shape almost every field
below:

1. It consumes only its own Fortran namelist input files and emits only its own ASCII tables. It
   reads no archive, no mission product, and no instrument data, so Data Sources, Related
   Instruments, Related Observatories, and Related Datasets are legitimately empty rather than
   unfilled.
2. The repository bundles three satellite components that the previously published description does
   not mention: **JET-PLUME** (a field–particle-correlation extension merged into `main` at v.1.1.0,
   `src/fpc.f90` + `README-JETPLUME.md`), **`linfpclib`** (a Python wrapper that writes inputs, runs
   the executable, and loads results), and **`SWIFT`** (a PyVista 3D/animated eigenmode visualizer).
   Much of the Software Functionality and Programming Language evidence lives in those components,
   not in the dispersion solver.
3. The physics is region-agnostic by construction — a uniform magnetized plasma with arbitrary
   bi-Maxwellian components. Region and Phenomena values therefore rest on the specific applications
   the repository and its code paper actually name, not on the full set of places a hot-plasma
   dispersion solver could be pointed.

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
10.5281/zenodo.15215513`, and DataCite lists three `HasVersion` relations from it
(`10.5281/zenodo.15215514`, `10.5281/zenodo.16904910`, `10.5281/zenodo.17148711`). Field 2 asks for
"the concept DOI for all versions," so the stored value is the correct one.

**Rejected alternative:** `10.5281/zenodo.15215514`. This is what the repository itself advertises —
the README badge (`README.md` line 1), the FORD landing page (`ford_project.md` line 28), and the
BibTeX blocks in both files all cite it. It is the **v.1.0.1 version DOI**, not the concept DOI, so
using it would pin the record to the April 2025 release and silently exclude v.1.1.0 and v.1.2.0.
The version DOI belongs in Field 12 (Version PID), where the current release's DOI is already
recorded. This is an upstream inconsistency in the repository, not an error in the HSSI record — a
future agent should not "correct" Field 2 to match the README badge.

---

### 3. Code Repository (MANDATORY)
`https://github.com/kgklein/PLUME`

*Source:* The repository's own canonical URL, corroborated by `git remote`, `ford_project.md`
(`project_github`), the clone instruction in `INSTALL.md`, and the acknowledgement request in
`README.md` §2. Default branch `main`.

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
`tutorial.md`). All sixteen values were confirmed against the live `FunctionCategory` vocabulary.

**A parent category belongs in the list alongside each of its children, and the earlier published
set omitted one.** The value set previously published in HSSI held
`Data Processing and Analysis: Wave Polarization Analysis` and `Data Processing and Analysis:
Analysis` without their parent `Data Processing and Analysis`. HSSI does not add a parent implicitly
when a child is selected, so the parent is a value in its own right; its earlier absence made the
published set incomplete rather than differently classified. Both of those leaf values are correct and
are retained.

**Evidence for each value.**

- *Data Processing and Analysis: Wave Polarization Analysis* — `calc_eigen` (`src/disprels.f90:2290`) returns the complex electric
  field components `(Ex, Ey, Ez)` that define the wave's polarization state, and the shipped gnuplot
  scripts compute and plot the degree of elliptical polarization of the `x` and `y` electric-field
  components from output columns 13–16 (`plotter/example/example_kpar.plt`, the `#Polarization`
  panels; described in `tutorial.md` §4 as "the degree of elliptical polarization of the $x$ and $y$
  components of the electric field").
- *Data Processing and Analysis: Analysis* — the code derives physical quantities beyond the raw
  dispersion roots: growth/damping rates, power absorption or emission per species, and — with
  `low_n` true — that power decomposed into Landau, transit-time, and separated `n = +1` / `n = -1`
  cyclotron channels (`output.md` lines 115–135, `Ps_split` in `calc_eigen`).
- *Data Processing and Analysis: 3D Particle Distribution Processing* — JET-PLUME `option 7` (`compute_fpc_cart`,
  `src/fpc.f90:33`) computes the perturbed distribution function `f_s1(v_x, v_y, v_z)` (real and
  imaginary parts) and the field–particle correlations `C_Ei` on a full 3D Cartesian velocity grid;
  `option 6` (`compute_fpc_gyro`, `src/fpc.f90:1020`) does the gyrotropic `(v_perp, v_par)`
  equivalent. `linfpclib.loadlinfpc3d` and `loadlinfpc3d_dist` read those velocity-space volumes back
  into Python.
- *Data Processing and Analysis: Plasma Moments* — `src/fpc.f90` integrates the perturbed
  distribution over velocity when `computemoment` is true, explicitly computing the "Density
  Fluctuation: Zeroth Moment of delta f"
  and the "Fluid Velocity: First Moment" (comments at lines 578 and 587), using a
  Sokhotski–Plemelj treatment of the resonant denominator. `linfpclib.loadmoms` loads the resulting
  per-species density and velocity moments. Independently, `calc_eigen` returns per-species density
  fluctuations (`ns`) and velocity fluctuations (`vmean`) derived from the susceptibility tensor.
  Note the documented upstream limitation: the gyrotropic routine refuses to compute moments
  ("WARNING! The gyro routine does not support computing moments at this time due to computational
  demand!", `src/fpc.f90:1191`) — moments come from the Cartesian routine only.
- *Data Processing and Analysis: 2D Slices* — the Cartesian JET-PLUME output file stores three 2D
  planes of each 3D velocity-space quantity — `(v_perp,1, v_perp,2)`, `(v_perp,1, v_par)`,
  `(v_perp,2, v_par)` — separated by `---` (`README-JETPLUME.md` §4, "Cartesian Ouput"); the
  gyrotropic routine produces the `(v_perp, v_par)` plane described there as "equal to integrating
  out the third coorindate, $\theta$"; and `linfpclib.reduce_3d_to_projections` reduces a 3D velocity
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
  following "Stix 'Waves in Plasmas' Chapter 10, Eqns. 66-73" (`README.md` §1), with the plasma
  dispersion function (`zet_in`, `src/disprels.f90:5104`) and Bessel-function sums over cyclotron
  harmonics (`src/bessel.f90`).
- *Theory* — it is a linear-theory calculation: it evaluates an analytic dispersion tensor and
  locates its roots (`map_search`, `refine_guess`, `find_minima`) rather than time-advancing a
  simulation. The RNAAS code paper frames it as an implementation of "the linear Vlasov–Maxwell
  dispersion relation."
- *Physics-Based* — the broader physics-based modelling parent value, selected alongside *First
  Principles* because the collision extension (`collision_type = 1`, a non-conservative Krook
  operator for neutral–charged collisions, `input.md`) is a modelled closure rather than a
  first-principles collision integral.

**Considered and rejected, with reasons** (recorded so these are not re-proposed):

- *Servers and Environments: High Performance Computing* — **rejected on direct evidence.**
  `ford_project.md` line 35 calls PLUME "a parallelised numerical code," but a sweep of every
  `src/*.f90` file and the `Makefile` finds no MPI call, no `use mpi`, no OpenMP sentinel and no
  `-fopenmp`/`-qopenmp` flag; the build links a single serial executable `plume.e` from
  `nrtype/nrutil_trim/vars/functions/bessel/disprels/fpc` plus `plume.o`. The FORD page's wording
  (which also claims "even relativistic," a capability the README does not describe) does not reflect
  this build. Do not add HPC on the strength of that sentence.
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
  solar wind models" (`src/plume.f90:168`, `read_radial_input`, `radial_scan`). Those paths come from
  *models*, not observations, and the option is explicitly unfinished: it prints "Option 5 is under
  development. Use with caution...Here be Dragons..." before running.
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
regions already published in HSSI; `Solar Wind` rests on repository evidence set out below. All four
were confirmed against the live `Region` vocabulary.

**Why `Solar Wind` belongs here.** It is the one region the repository names in its own source and
documentation: `src/vars.f90:279` heads its radial-scan block "Variables for radial scan of solar
wind models: See Option 5"; `src/disprels.f90:1577` describes `radial_scan` as running "for a
specified radial solar wind model"; `input.md` documents `option 5` as "Find roots for parameters
along a prescribed path. Path is set by solar wind models." The code paper that the developers
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
as "University of Iowa". The stored `University of Iowa` identity carries the matching ROR
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

*Evidence that was weighed in favour.* He is a credited creator on the Zenodo record for v.1.2.0
(`10.5281/zenodo.17148711`), the version HSSI currently stores in Field 12, and he is a genuine git
contributor: commit `f5225d5ec920701aa90d062a68d68fddfdd629d9`, 2025-09-12, "Fix Makefile: correct
module dependencies and moddir handling" (merged via PR #28, five days before the v.1.2.0 release).

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
keeps Howes in argues against reading Jorge in. His contribution is also a one-commit build-system
fix rather than science content. Recording a person the maintainers do not name as an author would
misattribute authorship in a public catalogue, the more consequential of the two possible errors, so
he is omitted. He should not be re-proposed on the strength of the Zenodo creator list alone; that
would take new evidence, such as the maintainers adding him to the README or a `CITATION.cff`, or his
appearing as an author of a JET-PLUME paper.

**Considered and not recorded as an author: Jason TenBarge.** Resolved here for the same reason:

- Name: Jason TenBarge
- Identifier: `https://orcid.org/0000-0003-0143-951X`
- Affiliation: Princeton University — `https://ror.org/00hx57361`
  (ORCID employment: Research Scholar, Department of Astrophysical Sciences, Princeton University,
  from 2020 with no end date. HSSI already carries a `Princeton University` row with this ROR.)

*Evidence that was weighed in favour.* `README-JETPLUME.md` §"Other Contributing Authors" names Greg
Howes, Kris Klein, and Jason TenBarge. That is a maintainer-authored authorship credit inside the
repository — arguably stronger evidence than Jorge's — and JET-PLUME has been part of PLUME proper
since v.1.1.0, so the component he is credited on is now shipped and installed with the code.

*Evidence that decided it against.* The credit is scoped to the JET-PLUME component and is worded as
"Other Contributing Authors," distinct from the lead-author line above it. The post-merge top-level
`README.md` — the file the merged product presents — still lists only Klein, Howes, and Brown as
PLUME's authors, as do `ford_project.md` and the code paper, while the `src/*.f90` headers and the
`LICENSE` name subsets of those same three. He has no commits in the repository and appears on no
Zenodo record. Omitted for the same reason as above. The JET-PLUME code paper is still unwritten —
`README.md` §5 marks its citation "[... Work in Progress]" — so its eventual author list is the
evidence that would justify revisiting this.

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

PLUME is a numerical solver for the hot plasma dispersion relation for a plasma with an arbitrary number of drifting bi-Maxwellian components. Each component is defined by its density, its drift velocity parallel to the mean magnetic field, and its parallel and perpendicular temperatures, and the solver identifies supported waves for any direction of propagation with respect to the background magnetic field. The code then varies the wavevector or the plasma parameters to trace dispersion relations for the identified solutions, and can supplementarily calculate heating rates, eigenfunctions, and the susceptibility tensor.

JET-PLUME (Judging Energy Transfer in a Plasma in a Linear Uniform Magnetized Environment) is an extension that ships and installs with PLUME. It predicts wave-particle energy transfer in velocity space using the field-particle correlation technique and linear theory, producing the perturbed distribution function and the velocity-space energy transfer for each electric field component, in either gyrotropic or Cartesian velocity coordinates.

An overview of the code can be found in README.md, with details on the inputs and outputs in input.md and output.md files respectively.

The code is written in FORTRAN90, with instructions for installation in the INSTALL.md file.

The output data is in ASCII format, and can be plotted with gnuplot, matplotlib, or any other standard visualization methods. An optional Python wrapper (linfpclib) writes input files, calls the executable, and loads results for use in a Jupyter notebook, and the bundled SWIFT tool renders static and animated 3D views of a reconstructed eigenmode.

An example .in input file is found in the inputs/example/ subdirectory, along with a .sh file to illustrate the execution of the code.

The full equations evaluated by PLUME are found in Klein, Howes, and Brown 2025 RNAAS.
```

*Source:* A corrected and extended revision of the description previously published in HSSI, which
was itself the Zenodo v.1.0.1 abstract (`10.5281/zenodo.15215514`) with its HTML stripped and its one
hyperlinked sentence dropped.

**The previously published description, reproduced exactly so a future reader can see what was
corrected:**

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

---

### 10. Publication Date (RECOMMENDED)
`2025-04-14`

*Source:* GitHub releases API for `kgklein/PLUME` and the Zenodo version records.

**Replaces the stored value `2025-09-17`, which was the wrong date for this field.** Field 10 is the
"Date of first broadcast/publication … Used for the initial version of the software," and
`2025-09-17` is the release date of v.1.2.0 — the *current* version, already recorded in Field 12.
Storing it in Field 10 as well made the software appear to have had no existence before its third
release.

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
- **Version Number:** `v.1.2.0`
- **Version Date:** `2025-09-17`
- **Version PID:** `https://doi.org/10.5281/zenodo.17148711`
- **Version Description:** `This new version splits the n = \pm 1 cyclotron resonances into separate components, rather than keeping the previous summation of the two terms. This changes the column numbering scheme. See output.md for details.`

*Source:* The current release, corroborated by four independent sources (git tag, GitHub release,
Zenodo and DataCite — set out below).

**Why HEAD activity does not change this field.** `main` carries 31 commits after the `v.1.2.0` tag
(`git rev-list v.1.2.0..main`), the latest dated 2026-05-12, and the extraction revision
`21a3711745d5fb6d8f147d4ca773a9db7508924d` is one of them. None of that is a release: there is no
tag, no GitHub release, and no Zenodo deposit after v.1.2.0. Field 12 records a released version, so
unreleased development on `main` is correctly invisible here. A future refresh should re-check tags
and releases rather than commit dates.

**The repository's own version declarations are all stale, and none of them names a newer release.**

- `Makefile` header comment: "VERSION 1.1 … LAST UPDATE: 2025/08/18". A hand-maintained comment
  matching the v.1.1.0 era (released 2025-08-19); the file has since been modified by the
  2025-09-12 module-dependency fix without the comment being updated.
- `ford_project.md` BibTeX block: `version = {v1.0.1}` — stale, and also note the form `v1.0.1`
  without the second dot, which is not how the tags are spelled.
- `README.md` DOI badge: `10.5281/zenodo.15215514`, the v.1.0.1 version DOI — stale.
- There is **no** `CITATION.cff`, no `.zenodo.json`, no `codemeta.json`, no `CHANGELOG.md`, and no
  version constant, parameter or string in any `src/*.f90` file, in `linfpclib/`, or in `SWIFT/`.
  The three machine-readable metadata files are absent from every commit on every branch, not just
  from `main`, which is why Zenodo derives its creator lists from GitHub contributors (see Field 6).
  Grepping the sources for `version` yields only dated code comments and a wrapper warning about
  "the most current version of PLUME".

**Authoritative release evidence, all agreeing on v.1.2.0 / 2025-09-17.** Git tag `v.1.2.0` →
commit `81ac15d6aa5eee43fa5fcb91df1ed9c28c4670c9`, 2025-09-17; GitHub release `v.1.2.0` "Updated
Cyclotron Heating to Split positive and negative resonances", published 2025-09-17T23:40:54Z,
neither draft nor prerelease; Zenodo record 17148711, `version: v.1.2.0`,
`publication_date: 2025-09-17`; DataCite for `10.5281/zenodo.17148711`, `version: v.1.2.0`, `Issued`
2025-09-17. The full release history is `v.1.0.0` and `v.1.0.1` (both 2025-04-14, both tagging
`1e4baab`), `v.1.1.0` (2025-08-19, `f832462`), `v.1.2.0` (2025-09-17, `81ac15d`).

**Storage form — a trap for any later edit.** The version number is stored bare, as `v.1.2.0`, while
the view layer renders it as `<software name> - <number>`. The rendered string must never be written
back into this field, or the stored value is corrupted. The version description above is the release note as stored, matching
the Zenodo v.1.2.0 abstract including its literal `\pm`.

---

### 13. Programming Language (RECOMMENDED)

- Fortran90
- Python 3.x
- Other

*Source:* File census of the working tree and of every branch in the repository, GitHub's language
statistics, SoMEF, and inspection of the sources themselves. All three values confirmed against the
live `ProgrammingLanguage` vocabulary.

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
recoverable from any source examined, so neither should be restored.

**Why each recorded value is correct.**

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
  under Python 3.12.2. `Python 2.x` is not a candidate.
- **`Other`** — three build- and workflow-critical languages have no row in the vocabulary: **gnuplot**
  (~39 KB across five `plotter/example/*.plt` scripts, the documented visualization path in
  `tutorial.md` §4, and identified as `Gnuplot` by GitHub), **shell/bash** (`inputs/example/run_example.sh`,
  `plotter/example/cycle.sh`, `SWIFT/run_swift_viz_example.sh`, plus the `bash` requirement the
  notebook states for `os.system` calls), and **GNU make** (the `Makefile`, which `INSTALL.md`
  lists as a hard requirement). `Other` is the only way to represent them, so it stays.

---

### 14. Reference Publication (RECOMMENDED)
`https://doi.org/10.3847/2515-5172/add1c2`

*Source:* The code paper: Klein, K. G., Howes, G. G., & Brown, C. R., "PLUME: Plasma in a Linear
Uniform Magnetized Environment," *Research Notes of the AAS* **9**, 102 (2025), published 2025-04-30.
`README.md` §2 instruction 3, `tutorial.md` §1, `input.md`, and `output.md` all direct users to cite
it, and `.github/scripts/add_plume_papers_to_ads_library.py` lists its bibcode `2025RNAAS...9..102K`
as a PLUME citation to track.

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
differs. SoMEF surfaces both variants.

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

*Source:* `astrophysics`, `plasma physics` and `space physics` are the repository's own GitHub topics
(`astrophysics`, `plasma-physics`, `space-physics`, also reported by SoMEF as `keywords`); the other
six rest on the repository evidence below.

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
it reads only its own input files.

---

### 18. Input File Formats (RECOMMENDED)
- ascii

*Source:* The input files are plain-text Fortran namelists (`inputs/example/*.in`, `tests/*.in`), read
with list-directed namelist I/O in `src/functions.f90`; the radial-scan `.rad` files and the
`linfpclib` loaders (`load_plume_sweep`, `loadlinfpc*`, `loadeigen`, `loadmoms`) are likewise plain
text. No binary, CDF, FITS, HDF5, netCDF, JSON, csv, IDL.sav or Zarr reader exists anywhere in the
repository, so `ascii` is the complete answer rather than a partial one.

---

### 19. Output File Formats (RECOMMENDED)
- ascii

*Source:* `output.md` and `README-JETPLUME.md` §4 specify every output as whitespace-delimited text
columns or row/column grids — `dispersion_*.map`, `dispersion_*.roots`, `*.modeN`, and the JET-PLUME
`.cpar`, `.cperp`, `.cparcart`, `.cperp1`, `.cperp2`, `.df1*` files. The Zenodo abstract agrees ("The
output data is in ASCII format").

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
the UNIX family: "A UNIX, Linux, or macOS operating system." The vocabulary has no `UNIX` row, so
`Linux` and `Mac` are the two rows that express that requirement, and CI exercises Linux only. The
documented position was recorded in preference to the technically plausible one, and `Windows` is not
added for the same reason. If the maintainers later document or test Windows support, this is the
field to revisit.

---

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

*Source:* Inspection of the sources and the build.

They contain no architecture-specific code: no intrinsics, no assembly, no vendor libraries
(`LIBS=` is empty in the `Makefile`), and no architecture-conditional compilation. The only build
switch is compiler choice (`SYSTEM=GFORT` versus a commented `IFORT`). `GPU` and `HPC or HEC` are
specifically rejected: there is no CUDA, OpenACC, OpenCL, MPI or OpenMP anywhere in `src/` or the
`Makefile`, and the `ford_project.md` claim that PLUME is "parallelised" is contradicted by the build
itself (see the corresponding note under Field 4). `x86-64` and `Apple Silicon arm64` are not
recorded in place of `CPU Independent` because nothing restricts the code to either.

---

### 22. Related Phenomena (OPTIONAL)
- Solar Wind

*Source:* The repository's own source comments and documentation, cited below. Confirmed against the
live `Phenomena` vocabulary.

**Why `Solar Wind`.** It is the only phenomenon in the vocabulary that the repository itself names.
`src/vars.f90:279` heads its radial-scan variables "Variables for radial scan of solar wind
models"; `src/disprels.f90:1577` documents `radial_scan` as running "for a specified radial solar
wind model"; `input.md` and `src/plume.f90:168` describe `option 5`'s path as "set by solar wind
models". The publication the code paper identifies as describing a simplified earlier version of
PLUME is titled "Predicted impacts of proton temperature anisotropy on solar wind turbulence."

**`Coronal Heating` considered and not selected.** The physics case for it is real: PLUME computes
collisionless damping rates decomposed into exactly the Landau, transit-time and cyclotron channels
that the coronal-heating problem turns on (`low_n`, `Ps_split`, `output.md` lines 115–135). It is not
selected because the repository never mentions the corona, coronal heating, or any coronal
application — in source, documentation, or example inputs. Selecting it would be inference from the
physics rather than evidence from the software. A future refresh that gains access to the
developers' curated citing-papers library
(`https://ui.adsabs.harvard.edu/public-libraries/RWGonkVgRpOaTizvWwsjKg`, rebuilt weekly by
`.github/workflows/update_ads_library.yml`; reading it requires an ADS API token) could revisit this on
the strength of how PLUME is actually applied in the literature.

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
actively developed", and both halves hold. *Stable and usable:* four tagged releases, each with a
GitHub release and a Zenodo DOI, spanning 2025-04-14 to 2025-09-17, plus a peer-reviewed code paper,
a full documentation site, a tutorial, and worked examples. *Actively developed:* commits continue
past the latest release — 31 commits on `main` after the `v.1.2.0` tag, the most recent 2026-05-12,
which is the merge of PR #42 recorded as this file's source revision; GitHub reports `pushed_at`
2026-05-12 and `archived: false`; two GitHub Actions workflows are live, one of them on a weekly
schedule.

**Rejected alternatives:** `WIP` — there are stable public releases, so it does not apply, even
though individual features are unfinished (`option 5` prints "under development", `option 3` is
deprecated and halts, and JET-PLUME's own citation is marked "[... Work in Progress]"). `Inactive`
and `Unsupported` — contradicted by 2026 commits. `Abandoned`, `Suspended`, `Moved`, `Concept` — all
contradicted by the release and commit history.

---

### 24. Documentation (RECOMMENDED)
`https://kgklein.github.io/PLUME/`

*Source:* The FORD documentation site deployed by `.github/workflows/doc.yml` to the `gh-pages`
branch, and set as the GitHub repository's `homepage`.

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

*Source:* Both DOIs verified through Crossref; the repository evidence for each is below.

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

**Considered and not included, with reasons.**

- *Quataert (1998), ApJ 500, 978.* `README.md` §1 says PLUME "is based upon a F90 adaptation by Greg
  Howes of a solver originally by Eliot Quataert," and the code paper says PLUME "is built on an
  implementation first presented in E. Quataert." The repository names the person, not the paper: no
  DOI, no year, no link anywhere in the tree. Including it would require supplying a citation the
  developers did not, and it describes a predecessor implementation rather than PLUME.
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
  membership changes without any repository change, and Field 27 expects individual DOIs. Reading it
  also requires an ADS API token. The library URL is recorded here as context for a future refresh; it
  is not a Field 27 value.

---

### 28. Related Datasets (OPTIONAL)
None.

*Source:* Researched and correctly empty.

PLUME generates its own data rather than analysing published datasets, and it reads no dataset at
all (Field 17). The repository does ship output files — `data/example/dispersion_map_par.map`,
`.roots`, and `map_par_kpar_1_10000.mode1`–`mode3` — but `data/README.data` and `tutorial.md` §4
present them as example products for the shipped gnuplot scripts to plot. They have no DOI, no
landing page, and no separate archival identity: they are versioned inside the code deposit, so they
are covered by the software's own DOI rather than being a related dataset. Zenodo and DataCite record
no dataset relation for any version (the only `relatedIdentifiers` are `IsSupplementTo` links to the
matching GitHub tag, plus the concept/version `HasVersion` links).

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
and would be genuinely useful neighbours for a reader (ALPS, NHDS, LEOPARD, WHAMP and others). None is
named anywhere in the repository: a grep across every source file, documentation file, example and the
notebook returns nothing for any of those names. The code paper's abstract acknowledges that "many
numerical methods for solving the Vlasov–Maxwell dispersion relation … have been implemented" without
naming one, and the references identifiable from it are Stix, Quataert, Klein & Howes, Fried & Conte
and Huang et al. — *but the paper's full reference list could not be retrieved*, so absence from the
paper is weaker evidence than absence from the repository, and a future agent with the full
bibliography may find a comparable code cited there. Even so, listing a comparable solver here would
assert a relationship the repository does not make. Cross-linking PLUME to peer tools would be a
deliberate curatorial choice rather than something the available evidence supports.

**Generic infrastructure excluded** per the field's relevance gate: numpy, matplotlib, PyVista,
gnuplot, GNU make, LaTeX and ImageMagick are all present in the workflows and all fail the "would
this be equally at home in a web app, a finance model, or a biology pipeline" test.

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
field without a `https://spase-metadata.org/` identifier.

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
`https://raw.githubusercontent.com/kgklein/PLUME/main/PLUME_logo.png`

*Source:* `PLUME_logo.png` at the repository root, embedded by `README.md` line 7 and copied into the
documentation site by `.github/workflows/doc.yml`.

**HSSI previously published `https://github.com/kgklein/PLUME/blob/main/PLUME_logo.png`, which does
not serve an image.** A `/blob/` URL is GitHub's HTML file-viewer page: requesting it returns
`Content-Type: text/html` and a roughly 216 KB HTML document, so anything rendering it as an image
gets nothing. The `raw.githubusercontent.com` form of the same file returns `Content-Type: image/png`
and the actual 672,580-byte asset. The recorded URL is 67 characters, well inside the 200-character
limit that applies to a URL field.

**Alternative considered.** Pinning the commit instead of the branch —
`https://raw.githubusercontent.com/kgklein/PLUME/81ac15d6aa5eee43fa5fcb91df1ed9c28c4670c9/PLUME_logo.png`
(103 characters) — would be immutable, which Field 33's "stored online in a permanent place" wording
mildly favours. The branch form is chosen because it keeps working if the maintainers update the
logo, and because a commit-pinned asset URL would silently freeze the catalogue image to one 2025
revision. Both forms are recorded so the choice can be revisited.

**Not selected: `Jet-Plume_Logo.svg`.** SoMEF reports this file as the repository's `logo`, but it is
the logo of the JET-PLUME sub-component (`README.md` §5, `README-JETPLUME.md`), not of PLUME.
`PLUME_logo.png` is the image the README leads with. Also present at the repository root and not
candidates: `qrcode_plume_github.png` (a QR code pointing at the repository), `favicon.ico`, and the
`.xcf` GIMP sources for the logo and QR code.

---

## Additional context not captured by any field

**Editable GIMP sources ship alongside the images.** `PLUME_logo.xcf` (1.6 MB) and
`qrcode_plume_github.xcf` are tracked in the repository, so the logo is maintainable upstream.

**A gyrokinetic dispersion module is present but not built.** `src/gk_disp_gf.f90` (1022 lines,
"Gyrokinetic Dispersion Relation Functions", "Copyright, 2005 Greg Howes") implements a separate
gyrokinetic dispersion relation with collisional, hyperviscous, Krook and bi-Maxwellian/bi-kappa
options. It is **not** in the `Makefile`'s `LFMOD` object list, so it is not compiled into `plume.e`
and none of its routines is reachable from `src/plume.f90`. It is therefore excluded from the Field 4
functionality classification — a future refresh should re-check whether it has been wired into the
build before crediting gyrokinetic or bi-kappa capability.

**A test workflow is documented but does not exist.** `INSTALL.md` tells contributors that "GitHub
will run automatic tests (via workflows) to ensure that the changes do not break the code", but
`.github/workflows/` contains only `doc.yml` (documentation build and deploy) and
`update_ads_library.yml` (weekly bibliography refresh). The `tests/` directory holds two input files
(`2D-scan-test.in`, `drift_cbe_test.in`) and no harness. This does not change Field 23 — there are
stable releases and active development — but it is worth knowing before citing CI as evidence of
testing.

**PyHC registry: not a member.** No entry in any of the three PyHC registry files —
`projects_core.yml`, `projects.yml`, `projects_unevaluated.yml` in
`heliophysicsPy/heliophysicsPy.github.io/_data/` — matches PLUME, JET-PLUME, `linfpclib`, or the
repository URL `https://github.com/kgklein/PLUME`. No curated PyHC metadata is therefore available for
this software, and absence from those registries is expected for a Fortran-first package. PyHC
membership is not a prerequisite for anything in this record.
