# HSSI Metadata Extraction Results

**HSSI Software ID:** 063b5195-7e46-4b16-a45c-25393fb8675f
**Repository:** https://github.com/fmihpc/rhybrid
**Source Revision:** 2df55d510629504a7c654d189031c6f9d598fda6
**Extraction Date:** 2026-08-10
**Validation Date:** 2026-08-22
**Validation Status:** PASS

---

## Scope note — read this before the evidence

RHybrid is **not a standalone program**. Its `src/` tree is copied into the Corsair parallel
simulation platform's user tree (`corsair/src/user/rhybrid/`) and compiled into a `corsair_rhybrid`
executable (`INSTALL`, `src/Makefile`). Nothing in this repository builds or runs on its own, and
none of Corsair, ParGrid, VLSV or Zoltan is vendored here; the one vendored third-party file is
`tools/vlsvparticles.py`, a copied Analysator module that still carries its Analysator / University
of Helsinki copyright header. The primary evidence below is therefore this repository's own source,
configuration files, tooling and `pubs.txt`, together with the developers' own project site
`https://planets.fmi.fi` — the repository's declared GitHub `homepage` and the developers' only
narrative description of the model outside the README. External registries (Crossref, ORCID, ROR,
Zenodo, DataCite, ASCL, the GitHub API) are used where the notes say so.

A second consequence: the repository publishes **no release, no tag, and no version string of any
kind**. Several fields below are correctly empty for that reason, and the negative research that
establishes it is recorded so a later refresh does not repeat it.

Field numbering below follows the HSSI Resource Submission Form (Fields 1–33), which does not
correspond to the ordering of the API keys: Authors is Field 6 here, Related Region is Field 5, and
Interoperable Software is Field 30.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*No submitter is recorded for this software, and none is derivable from the repository. RHybrid was
not submitted by this project, and the original submission was repository-scraped rather than
maintainer-supplied: its four author rows were exactly the four GitHub contributor accounts of
`fmihpc/rhybrid`, carrying those accounts' GitHub display names. That origin explains several of the
corrections documented in Field 6.*

### 2. Persistent Identifier (RECOMMENDED)
**Not found.**

RHybrid has no concept DOI. Negative research, so this is not re-investigated later:

- The repository contains no `CITATION.cff`, `codemeta.json`, `.zenodo.json`, DOI badge, or DOI
  string of any kind. The README's "Main reference" is a journal-article DOI, which belongs in
  Field 14, not here.
- Zenodo search for `rhybrid` returns five records, **none** of which is an authoritative archive of
  `fmihpc/rhybrid`:
  - `10.5281/zenodo.10836240` (concept `10.5281/zenodo.10836239`), *"parkusa/rhybrid_vc: RHybrid"* —
    a GitHub–Zenodo snapshot of the third-party **fork** `parkusa/rhybrid_vc`, not of the FMI
    repository. Creators are "Riku Jarvinen (Finnish Meteorological Institute)" and "eganhila", i.e.
    GitHub-scraped contributor names, and its licence is recorded as CC-BY-4.0, which contradicts the
    code's actual GPL v3 licensing. Using it as RHybrid's persistent identifier would point HSSI at a
    fork and import a licence error.
  - `10.5281/zenodo.13706293` and `10.5281/zenodo.20344860`, *"Rhybrid Code and Parameter Table"* /
    *"… (2026GRL)"* — paper-supplement deposits by a third-party user group (Zhou & Jarvinen)
    accompanying their own publications. Their descriptions quote the RHybrid README, but they
    archive a snapshot plus a run-parameter table for one study, not the software as a maintained
    product. One is licensed CC-BY-4.0 and one GPL-3.0-or-later, which is itself a sign these are
    ad-hoc deposits.
  - `10.5281/zenodo.11403027` and `10.5281/zenodo.19247602` — datasets, not software (see Field 28).
- DataCite search for `rhybrid` surfaces the same Zenodo deposits and no FMI-issued software DOI.
- ASCL has no RHybrid code entry.
- `https://planets.fmi.fi/modeling.html`, the developers' own description of the model, gives no DOI.

If FMI later mints a concept DOI for the code, that becomes the correct value; until then this field
is properly empty rather than filled with a fork's or a supplement's DOI.

### 3. Code Repository (MANDATORY)
`https://github.com/fmihpc/rhybrid`

Carried over from the existing HSSI record and independently confirmed: this is the URL the README
itself gives ("The latest version of RHybrid can be downloaded at: https://github.com/fmihpc/rhybrid"),
the URL `INSTALL` clones, and the URL the developers' project page links to. The local clone's git
remote resolves to it, the GitHub API reports `full_name = fmihpc/rhybrid` with `default_branch =
master`, and the repository is not archived or moved.

### 4. Software Functionality (MANDATORY)
The record previously carried a single value, `Models and Simulations`. That value was correct but
materially incomplete: RHybrid also computes plasma moments from macroparticles, performs output data
reduction, converts file formats, extracts and plots 2D slices, makes movies and 3D trajectory
figures, traces test particles, and is an MPI/HPC application. The twenty values below replaced it,
each carrying its own code evidence, and every selected subcategory's parent is listed as the
taxonomy requires. All twenty were matched against the live `FunctionCategory` vocabulary.

**Models and Simulations**
The core of the repository is a simulation model. `src/hybrid_propagator.cpp` (2,094 lines) advances the
electromagnetic fields, `src/particle_propagator_boris_buneman.h` pushes ions with a Boris–Buneman
integrator, `src/particle_injector.cpp` (1,840 lines) injects populations, and
`src/particle_boundary_cond_hybrid.h` applies boundaries.

**Models and Simulations: First Principles**
The quasi-neutral hybrid formulation is solved from fundamental physics, not from fitted
relationships: ions move under the Lorentz force as kinetic macroparticles, electrons form a
charge-neutralising fluid, and the field solve combines the electron momentum equation (including the
Hall term, `Hybrid.use_hall_term`, and an electron pressure term, `cellEp`) with Faraday's law.
`src/magnetic_field.h` builds the intrinsic field from dipole/quadrupole/line-dipole analytic
profiles; `src/resistivity.h` supplies resistivity profiles.

**Models and Simulations: Physics-Based**
Selected in addition to First Principles because parts of the model are semi-empirical physics rather
than ab initio: `src/neutral_profiles.h` implements Chamberlain exospheres, exponential and power-law
neutral profiles, and three body-specific profiles — `neutralDensityVenusHydrogen`,
`neutralDensityVenusOxygen` and `neutralDensityMercurySodiumExner20`, of which only the last carries
a published citation in a source comment (Exner et al. 2020, doi:10.1029/2019JA027691). Ionospheric emission profiles such as
`ionoCosSzaDayConstantNight` (`examples/venus.cfg`) are likewise parameterised physics.

**Data Processing and Analysis**
Parent for the moment computation, reduction, conversion, slicing and time-series work below.

**Data Processing and Analysis: Plasma Moments**
`src/particle_accumulator.cpp` accumulates macroparticle weight and velocity onto the grid, and
`src/operator_userdata.cpp` writes per-population number density (`n_*`), bulk velocity (`v_*`) and
temperature (`T_*`), plus ion charge density (`cellRhoQi`, `nodeRhoQi`), ion current (`cellJi`) and
electron velocity (`cellUe`). Deriving bulk quantities from a particle distribution is exactly this
subcategory.

**Data Processing and Analysis: Data Reduction**
Explicit, configurable output reduction: `Hybrid.save_reduced_state_interval`,
`Hybrid.save_reduced_state_Nstride` ("Write every Nstride'th cell in reduced state output"),
`Hybrid.save_reduced_state_include_particles` and `Hybrid.save_particles_Nstride` ("Write particles in
every Nstride'th cell") in `src/user.cpp`, with the writer in `src/diagnostics.h`. Temporally averaged
output variables (`*_ave`, `cellBAverage`, built under `WRITE_GRID_TEMPORAL_AVERAGES` in
`src/Makefile`) are a second reduction path.

**Data Processing and Analysis: File Format Conversion**
`tools/vlsv_to_vtk.py` reads a VLSV state file and writes VTK XML — `.vti` for the grid and `.vtp`
for macroparticles. `INSTALL` documents the invocation and the resulting `state00004000.vti`.

**Data Processing and Analysis: 2D Slices**
`tools/plotter_rhybrid_2d_slice.py` (899 lines) and `tools/plotter_example_2D.py` reshape the flat
VLSV cell arrays into `(nz,ny,nx)` volumes and extract xy/xz/yz cut planes; the script's own header
documents 3D runs (three columns per figure) and 2D runs (one column). Listed under both processing
(the extraction) and visualisation (the figure).

**Data Processing and Analysis: Time Series Analysis**
`tools/create_time_series_point.py` interpolates chosen variables at a fixed point across every VLSV
file in a run directory and writes `time_series.dat`. `tools/rhb_log2pdf.sh` /
`tools/rhb_log2pdf_all.sh` plot the time-ordered `field.log` and `pop*.log` records. The in-code
diagnostics themselves emit time-ordered per-population series (escape rate, kinetic-energy escape
rate; `src/user.cpp` log-column headers, `src/diagnostics.h`).

**Data Processing and Analysis: Analysis**
`tools/create_derived_parameters.py` computes derived physical variables from a VLSV file and writes a
new VLSV file (its constants block defines proton, helium, oxygen and molecular-oxygen masses and
`mu0`); `tools/create_interpolation_along_trajectory.py` interpolates model variables along a
trajectory; `tools/rhb_check_run.py` and `tests/run_tests.py` compare modelled flow moments against
the prescribed upstream input within a statistical tolerance.

**Data Processing and Analysis: Processing**
The general pipeline step: `tools/rhb_dashboard.py` builds a run overview from the log files,
`tools/get_post_job_statistic.sh` gathers resource usage, and the shipped tools form a documented
post-processing chain (`INSTALL`, `examples/venus.txt`).

**Data Visualization**
Parent for the figure-producing tools.

**Data Visualization: 2D Graphics**
Pseudocolour slice plots with linear and logarithmic normalisation in
`tools/plotter_rhybrid_2d_slice.py`, `tools/example_venus_plotter_rhybrid_2d_slice.py` (765 lines) and
`tools/plotter_example_2D.py`, including a `matplotlib.patches.Wedge` overlay for the planetary body.

**Data Visualization: 2D Slices**
The same scripts' primary product is the displayed 2D cut plane through the 3D simulation volume.

**Data Visualization: 3D Graphics**
`tools/create_interpolation_along_trajectory.py` and `tools/trace_test_particles.py` both build a
Matplotlib 3D axes (`add_subplot(projection='3d')`), render the planetary sphere with `plot_surface`,
and draw paths inside the simulation domain.

**Data Visualization: Line Plots**
`tools/plotter_example_testrun.py`, `tools/rhb_check_run.py`, `tools/rhb_dashboard.py`,
`tools/rhb_log2pdf.sh` (gnuplot to PDF via Ghostscript) and the per-variable subplot stacks in
`tests/run_tests.py` all produce 1D line plots.

**Data Visualization: Movies**
`INSTALL` and `examples/venus.txt` document producing MP4 videos from the PNG frame series
(`ffmpeg -framerate 5 -pattern_type glob …`), and `tools/plotter_rhybrid_2d_slice_job.slrm` automates
the whole frames-then-`ffmpeg`-per-variable pipeline across SLURM nodes and writes `mp4/*.mp4`.

**Data Visualization: Orbit Plots**
`tools/create_interpolation_along_trajectory.py` constructs a spacecraft-like path — its own comment
reads "# circular orbit around the planet at r = 1.5*Rp on z = 0 plane" — and renders it in 3D against
the planetary sphere in a figure titled `trajectory`. `tools/trace_test_particles.py` similarly plots
traced ion trajectories in 3D and as component time series.

**Servers and Environments**
Parent for the HPC value.

**Servers and Environments: High Performance Computing**
RHybrid is an MPI application throughout (61 `MPI_*` call sites in `src/diagnostics.h` alone, plus
`src/user.cpp`, `src/detectors.cpp`, `src/particle_injector.cpp`,
`src/particle_boundary_cond_hybrid.h`), uses Zoltan for dynamic load balancing across MPI processing
elements (README; `INC_ZOLTAN` in `src/Makefile`; `[LoadBalance] methods = RCB` in the example
configs), and ships SLURM batch scripts for both the model run (`examples/slurm_batch_script.slrm`,
10 nodes × 20 tasks) and multi-node post-processing (`tools/plotter_rhybrid_2d_slice_job.slrm`, which
also handles Lustre file removal via `lfs find`).

**Considered and rejected — recorded so these are not re-proposed:**

- **Models and Simulations: MHD.** Explicitly wrong. RHybrid is a hybrid (quasi-neutral) code: ions
  are kinetic macroparticles, only electrons are a fluid. The developers' own model page contrasts the
  hybrid approach with fluid descriptions and states its advantage is precisely that "the ion velocity
  distributions need not be prescribed in advance as they evolve self-consistently". There is no
  magnetohydrodynamic solver in `src/`.
- **Models and Simulations: Data Guided.** Upstream solar-wind and IMF conditions are plain constants
  typed into a `.cfg` file (`[IMF] Bx/By/Bz`, the `solarwind` population parameters). Two example
  configs are matched to observed intervals (`examples/mars_agufm2015_run1.cfg` "Mars 25.01.2015 12:20
  (Run1, MAVEN inbound)"), but the code has no data ingestion or assimilation path, and by this
  standard nearly every simulation code would qualify.
- **Models and Simulations: Observatory/Instrument Models** and **Models and Simulations: Instrument
  Response.** The optional detector facility (`src/detectors.cpp`, `USE_DETECTORS` in `src/Makefile`)
  places virtual probes at arbitrary coordinates read from an ASCII file
  (`DetectorParticle.coordinate_file`, `DetectorBulkParameter.coordinate_file`) and records particles
  and bulk parameters there. It models no instrument's geometry, energy channels, or response
  function.
- **Data Processing and Analysis: 3D Particle Distribution Processing** and **Energy Spectra.** The
  only velocity-distribution/spectra accumulation code in the repository is commented out — the
  `dataSpectraID` / `spectra[species.popid].f[0] += w;` block in `src/particle_accumulator.cpp` sits
  inside `/* … */` within `#ifdef USE_DETECTORS`. Published RHybrid velocity-distribution figures
  (e.g. the Mercury foreshock VDFs on the developers' examples page) were produced outside this
  repository from the saved macroparticle data.
- **Data Processing and Analysis: Field-line Tracing** and **Models and Simulations: Field-line
  Tracing.** No field-line integrator exists in `src/` or `tools/`. The magnetic-field-draping and
  field-line figures on the developers' site were made in external tools from RHybrid output.
  `tools/trace_test_particles.py` traces *particles*, not field lines.
- **Coordinate Transforms** and all its children. RHybrid works entirely in one Cartesian simulation
  frame. The dipole orientation parameters (`IntrinsicB.theta`, `IntrinsicB.phi`) and the planet-radius
  normalisation in the plotting tools are internal geometry, not a user-facing conversion between
  named coordinate systems.
- **Data Processing and Analysis: Data Access and Retrieval.** Nothing in the repository fetches remote
  data (see Field 17).
- **Mission-related** and all its children. RHybrid is a research model, not part of any mission ground
  system, pipeline, archive or operations chain.
- **Data Visualization: Web-Based.** `tools/rhb_dashboard.py` is named "dashboard" but forces
  `matplotlib.use('Agg')` and writes static PNGs; there is no browser component.
- **Servers and Environments: Software or Environment Container.** No Dockerfile, Singularity
  definition, or environment specification exists; `INSTALL` is a manual from-source recipe.
- **Data Processing and Analysis: ML/AI**, **Calibration**, **Image Processing**, **Spectrogram**,
  **Wavelet Analysis**, **Curlometer**, **Pitch Angle Distributions**, **Packet Decommutation**,
  **Data Assimilation**, **Linear Gradient Estimation**, **Magnetic Null Finding**, **Wave
  Polarization Analysis**. None has any implementation here. Worth noting for two of them, because a
  reader might expect otherwise: the ULF-wave science RHybrid is best known for is done *on* its
  output in the papers, not by spectrogram or wavelet code in this repository; and magnetic
  reconnection/null topology is likewise studied downstream.

### 5. Related Region (MANDATORY)
- `Interplanetary Space`
- `Solar Wind`
- `Mars Magnetosphere`
- `Planetary Magnetospheres`
- `Earth Magnetosphere`

All five were matched against the live `Region` vocabulary. The record previously carried only
`Interplanetary Space`; the other four were added to it and none was removed.

- `Interplanetary Space` — every run is driven by an interplanetary magnetic field and an
  upstream flow (`[IMF]` section; `Hybrid.particle.population.solarwind`), and the ion foreshock that
  dominates the model's published science lies in the interplanetary medium upstream of the bodies.
- `Solar Wind` — the README's own first sentence scopes the model to "the solar wind and plasma
  interactions of celestial bodies"; `solarwind` is a first-class particle-population type in
  `src/user.cpp`; `examples/empty_box_flow.cfg` and `tests/test_empty_1d.cfg` are pure undisturbed
  solar-wind flow tests.
- `Mars Magnetosphere` — the most specific applicable row for the body RHybrid is most used on:
  `examples/mars.cfg`, `examples/mars_jgr_2022.cfg`, `examples/mars_agufm2015_run1.cfg`,
  `examples/mars_agufm2015_run2.cfg`, the README's designated main reference (oxygen ion energization
  at Mars), and four `pubs.txt` entries on the Martian magnetotail, ion escape and foreshock. Mars has
  an induced rather than intrinsic magnetosphere, which this row still covers as the only
  Mars-specific option.
- `Planetary Magnetospheres` — required for the bodies with no dedicated row: Mercury
  (`examples/mercury.cfg`, `examples/mercury_mnras_2020.cfg`, `neutralDensityMercurySodiumExner20`,
  two `pubs.txt` entries on the Hermean magnetosphere and foreshock), Venus (`examples/venus.cfg`,
  `examples/venus_grl_2020.cfg`, `examples/venus.txt`, `neutralDensityVenusHydrogen`/`…Oxygen`, two
  `pubs.txt` entries), comets (`examples/comet.cfg` with a power-law neutral coma and a 1 km nucleus),
  the Moon and exoplanets (`pubs.txt`: Egan et al. 2019 on unmagnetized exoplanets and on weakly
  magnetized planets; the developers' model page states the model "has also been applied beyond the
  solar system … on exoplanetary systems").
- `Earth Magnetosphere` — supported by a peer-reviewed application listed in the repository's own
  `pubs.txt`: Yang, Jarvinen, Guo et al. (2023), *Deformations at Earth's dayside magnetopause during
  quasi-radial IMF conditions: Global kinetic simulations and Soft X-ray Imaging*,
  doi:10.26464/epp2023059. The model is body-agnostic by construction (`R_object`, `M_object` and the
  magnetic-field profile are all configurable), so an Earth application is a genuine capability rather
  than a coincidence.

**Considered and not selected:**
- `Earth Magnetosheath` and `Earth Outer Magnetosphere` — the Yang et al. (2023) study is specifically
  about the dayside magnetopause and the soft X-ray emission from the magnetosheath, so either row
  could be argued as more specific. Not selected because one publication is thin ground for
  multiplying Earth sub-regions, and `Earth Magnetosphere` already makes the record discoverable. A
  later refresh with more Earth applications should promote the specific rows.
- `Earth Ionosphere` — RHybrid does have an `ionosphere` particle-population type, but it models
  *planetary* ionospheric ion outflow at Mars and Venus, not Earth's ionosphere.
- `Jupiter Magnetosphere`, `Saturn Magnetosphere`, `Uranus Magnetosphere`, `Neptune Magnetosphere` —
  no example configuration, publication, or developer statement applies RHybrid to the giant planets.
  FMI's participation in the Juice/PEP instrument package (developers' missions page) is instrument
  hardware work, unrelated to this code.
- `Corona`, `Chromosphere`, `Photosphere`, `Solar Interior`, `Solar Environment`, `Heliosheath` — the
  model does not simulate the Sun or the outer heliosphere. Its solar wind is an imposed inflow
  boundary condition, not a modelled region.

### 6. Authors (MANDATORY)
Four authors, reconciled by union with the four author rows the record already held — nobody was
dropped and nobody was added. Two of those rows carried GitHub handles rather than personal names;
their real identities are established below from the repository's own commit history plus the
publication record, and the rows were corrected in place, keeping their original identities rather
than being replaced by new ones.

They are listed in order of contribution to the default branch (`git shortlog`), principal developer
first. The record previously listed them in the order eganhila, Ilja, Riku Jarvinen, David Phillips,
which was an artifact of the original GitHub scrape rather than an authorship statement; contribution
order replaced it.

**1. Riku Jarvinen**
- Identifier: `https://orcid.org/0000-0002-4246-2954`
- Affiliations:
  - Finnish Meteorological Institute — `https://ror.org/05hppb561`
  - Aalto University — `https://ror.org/020hwjq30`

Principal developer: 305 of the 316 commits on `master`, committed under four git name/email
combinations spread across three addresses — `riku.jarvinen@fmi.fi` appears under two name spellings
(`rjarvinen`, 291 commits, and `Riku Jarvinen`, 10), alongside
`Riku Järvinen <rjarvinen@users.noreply.github.com>` (3) and
`Riku Jarvinen <rijarvin@voima-login2.(none)>` (1) — from the initial 2016-01-08 source publication to
the current HEAD (2026-06-08). The README's sole contact is "Finnish Meteorological Institute: Dr.
Riku Jarvinen (riku.jarvinen@fmi.fi)", and he is first author of the designated main reference. The
stored ORCID is confirmed by Crossref on that paper (doi:10.1002/2017JA024884) and on
doi:10.1029/2020GL087462.

Neither affiliation was on the record before. The Finnish Meteorological Institute rests on the
README contact line, his commit email `riku.jarvinen@fmi.fi`, his GitHub profile
(`company = Finnish Meteorological Institute`), and the developers' team page ("Riku Järvinen, Team
lead, PhD"). Aalto University rests on equally firm evidence: every source file in `src/` carries
"Copyright 2018- Aalto University" beside the FMI line, and Crossref records "Department of Electronics and Nanoengineering, School of Electrical
Engineering, Aalto University" as his affiliation on the main reference and on the 2019–2022 RHybrid
papers. Both affiliations are current and both belong on the record. Confidence: high.

*Name form.* The stored value `Riku Jarvinen` is the transliterated form used in the README, in
`INSTALL`-adjacent material, and in published author lists ("Jarvinen R."). His own ORCID record and
GitHub profile give the diacritic form **Riku Järvinen**, as does the developers' team page, and his
git author name appears both ways in this repository. The stored form is kept as the value because it
is the form the software's own documentation uses; the diacritic form is recorded here so a future
agent knows it is a known variant and not a discovery.

**2. Ilja Honkonen** — *corrected; the row previously held a blank given name and the family name
`Ilja`, and carried no identifier*
- Identifier: `https://orcid.org/0000-0002-9542-5866`
- Affiliation: Finnish Meteorological Institute — `https://ror.org/05hppb561`

`Ilja` is the GitHub display name of the account `iljah`, captured without a surname by the original
scrape. The real identity is unambiguous: the same person's six commits on `master` appear
under two identities in `git log`, `Ilja <2098356+iljah@users.noreply.github.com>` (4 commits,
2025-02-06 to 2026-02-27, the GitHub web-editor identity of account 2098356 = `iljah`) and
`Ilja Honkonen <ilja.honkonen@fmi.fi>` (2 commits, 2025-02-07 to 2025-03-03); the repository also
carries a remote branch named `iljah-patch-1`, merged as PR #4 (`38ef0588`, 2025-02-27) and again as
PR #17 (`a47f5d21`, 2026-03-09). The `@fmi.fi` commit email gives the affiliation directly, and the
developers' team page lists "Ilja Honkonen, Senior researcher, PhD, docent" with ORCID
`0000-0002-9542-5866` linked. That ORCID record's 44 works include the FMI
global hybrid Mercury/BepiColombo modelling papers, corroborating both the person and the group.
Confidence: high.

**3. Hilary Egan** — *corrected; the row previously held a blank given name and the family name
`eganhila`, and carried no identifier*
- Identifier: `https://orcid.org/0000-0002-8784-6724`
- Affiliation: University of Colorado Boulder — `https://ror.org/02ttsq026`

`eganhila` is a GitHub login with no display name set on the account, which is why the original
scrape captured the handle as a surname. `git log` resolves it: the three commits from that contributor (2018-04-11 to
2018-09-05) are authored by `Hilary Egan <hilaryye@gmail.com>`. `pubs.txt` independently confirms the
person and the connection to this code, listing her as lead author of two RHybrid papers — Egan,
Jarvinen, Ma & Brain (2019, doi:10.1093/mnras/stz1819) and Egan, Jarvinen & Brain (2019,
doi:10.1093/mnras/stz788) — plus Egan et al. (2018, doi:10.1029/2017JA025068). Crossref lists her
ORCID as `0000-0002-8784-6724` on both 2019 papers, which is decisive; the ORCID record itself is
sparse (no works or employments published) and was the only exact given-name/family-name match in
ORCID's public search at extraction time, so the identification rests on the Crossref registration
rather than on the ORCID profile. Confidence: high.

The affiliation recorded is the one contemporaneous with her contributions: Crossref gives
"Department of Astrophysical and Planetary Sciences, University of Colorado, Boulder" on both 2019
RHybrid papers, and her 2018 commits fall in that period. Her present-day employer is not evidenced
by any source in or reachable from this repository, so it is deliberately not asserted. Confidence in
the contribution-era affiliation: high; in it being current: not claimed.

**4. David Phillips**
- Identifier: `https://orcid.org/0009-0006-1010-6863`
- Affiliation: Finnish Meteorological Institute — `https://ror.org/05hppb561`

Two commits on `master` (2025-04-01, 2025-04-02) authored by `dphillips95 <david.phillips@fmi.fi>`;
GitHub profile name "David Phillips", `company = Finnish Meteorological Institute`. The name and the
Finnish Meteorological Institute affiliation were already on the record and were left alone; the
identifier was empty and was filled with `0009-0006-1010-6863`, "David Nicholas Huttly Phillips",
whose only published employment is the Finnish Meteorological Institute from 2024-09 with
disambiguation identifier `https://ror.org/05hppb561` — matching the affiliation already recorded —
and whose six works include RHybrid-relevant items ("Global hybrid-particle modelling of Mercury's
space plasma environment and BepiColombo observations", "On enhancing parallel global hybrid-particle
model with run-time adaptive mesh refinement and temporal substepping"). The developers' team page
lists "David Phillips, Post-doctoral researcher, PhD" with the same ORCID linked. Confidence: high.

The value keeps the short form `David Phillips` (repository and team-page form) rather than the full
ORCID legal name.

**Considered and not selected as authors:**
- **Finnish Meteorological Institute** and **Aalto University** as *organization* authors. Both are
  copyright holders — "Copyright (c) 2015- Finnish Meteorological Institute" in the README and
  "Copyright 2015- Finnish Meteorological Institute / Copyright 2018- Aalto University" in every
  `src/` header — and FMI is credited as developer and distributor. Not added as author entries
  because copyright holding and institutional attribution are not authorship, and both are already
  represented where they belong: as author affiliations, and FMI additionally as Publisher (Field 11).
  Should a later refresh revisit institutional credit, FMI's ROR is `https://ror.org/05hppb561` and
  Aalto's is `https://ror.org/020hwjq30`.
- Co-authors of the reference publication who are not contributors to this repository (D. A. Brain,
  R. Modolo, A. Fedorov, M. Holmström) and frequent scientific collaborators named in `pubs.txt`
  (E. Kallio, M. Alho, T. I. Pulkkinen, and others). They are authors of papers, not of the software;
  their contributions are represented by Fields 14 and 27.
- `tools/vlsvparticles.py` carries Analysator's own copyright ("Copyright 2013-2025 Finnish
  Meteorological Institute / Copyright 2017-2018 University of Helsinki"). That is a vendored
  third-party file, so University of Helsinki is not an author of RHybrid; the relationship is
  recorded in Field 30 instead.

**Standing platform limitation affecting this field.** HSSI's update API cannot rename an existing
person: a rename is silently accepted and discarded, and the whole `authors` field is rejected if any
row carries a blank given name. The two malformed rows here — a blank given name with the family name
`eganhila`, and a blank given name with the family name `Ilja` — were therefore unfixable through a
normal metadata update, and were corrected at the row level instead. A person row can be shared with
other software records, so any such fix has to be checked for other references first; that check was
done before these two were changed. The consequence for a future refresh is that author *names* on
this record cannot be altered by an ordinary update, only identifiers and affiliations can — if a name
here ever needs to change again, it needs the same row-level route and the same shared-reference
check.

### 7. Software Name (MANDATORY)
`RHybrid`

This corrected a previously stored `rhybrid`. The repository's own naming evidence is consistent and
points to the mixed-case form:

- The README expands the name and explains the internal capital: "RHybrid (**paR**allel **Hybrid**)".
  The capital H is meaningful — it marks the second word of the contraction — and is lost in both
  `rhybrid` and `RHYBRID`.
- README body prose uses `RHybrid` in every one of its occurrences outside the title line (ten
  times, including "The RHybrid code is originally developed at…", "The latest version of RHybrid…",
  "Main reference for RHybrid", and the example acknowledgement text).
- The GitHub repository description is "RHybrid Simulation Code".
- The developers' own model page uses `RHybrid` throughout.
- Source-file headers say "This file is part of the RHybrid simulation" / "the RHybrid simulation
  platform".
- The designated main reference and the `pubs.txt` papers refer to the model as RHybrid.

**Rejected: `rhybrid`** (the value previously stored). This is the GitHub repository slug. GitHub repository
names are conventionally lowercase and `fmihpc`'s other repositories follow the same pattern
(`corsair`, `pargrid`, `vlsv`, `hyb`); the slug is not the project's own rendering of its name. The
form definition asks for "the name of the software package as listed on the code repository", and what
the repository *says* — in its README, its description, and its source headers — is `RHybrid`.

**Rejected: `RHYBRID`** (the README's first line). That line is a section-heading style, not the name:
the same README renders each of its section headings in all caps ("SIMULATION CODE", "COMPILATION",
"ACKNOWLEDGEMENTS, CO-AUTHORSHIP AND CITING", "CONTACTS"), and the sibling files follow the same
convention (`doc/README` is "RHYBRID DOCUMENTATION", `src/README` is "RHYBRID SOURCE CODE",
`examples/README` is "EXAMPLE SIMULATION RUN CONFIGURATION FILES"). Nothing in the repository uses
`RHYBRID` in running prose. The in-code log prefix `(RHYBRID)` in `src/diagnostics.h` and
`src/detectors.cpp` is likewise a fixed-width log tag, matching Corsair's `(MAIN)` style.

Confidence: high. This is a display-form correction, not a change of identity, and the concise and
long descriptions below use the same form.

### 8. Description (MANDATORY)
```
RHybrid (paRallel Hybrid) is a parallel C++/MPI kinetic plasma simulation model platform for the solar wind and plasma interactions of celestial bodies. The RHybrid code is originally developed at the Finnish Meteorological Institute. The RHybrid code is distributed under the GPL v3 open source license by the Finnish Meteorological Institute.

RHybrid implements the quasi-neutral hybrid approach: positively charged ions are modelled explicitly as kinetic macroparticles moving under the Lorentz force, while electrons are treated as a charge-neutralizing fluid. Because the ion velocity distributions are not prescribed in advance but evolve self-consistently, and because any number of ion populations with different masses and charges can be followed at once, the model resolves the ion finite-Larmor-radius and multi-species effects that shape the plasma interactions of planets, moons, comets and exoplanets.

The code is compiled as a simulation module of the Corsair parallel simulation platform and builds on the ParGrid parallel grid, the VLSV parallel file format and the Zoltan library, which partitions the domain and balances computational load between MPI processing elements. Simulations are configured from ASCII run configuration files that define the Cartesian grid, the intrinsic magnetic field (dipole, quadrupole, line-dipole and hemispheric profiles, with optional mirror dipoles), resistivity profiles, gravity, the Hall and electron pressure terms of the electric field, and any number of uniform, solar wind, flow, ionospheric and exospheric ion populations with Chamberlain, exponential, power-law or published body-specific neutral profiles. Example configurations are provided for Mars, Venus, Mercury, a comet, a localized magnetic anomaly, and idealized 1D, 2D and periodic test setups.

Output consists of VLSV state files holding the electromagnetic fields and per-population plasma moments (number density, bulk velocity and temperature, ion charge density and current, electron velocity and pressure term), optional macroparticle data, reduced and cell-strided state files, ASCII main, field and per-population log files including particle and energy escape rates, and ASCII records from configurable virtual detectors placed at coordinates read from a file. Bundled Python and shell tools post-process this output using the Analysator library: 2D pseudocolor slices and MP4 movies, log-file plots, point time series, interpolation along a spacecraft trajectory, derived variables, test particle tracing, and conversion of VLSV files to VTK XML. SLURM batch scripts are included for running both the model and the post-processing on HPC systems.

RHybrid has been applied to the solar wind interactions of Mars, Venus, Mercury, the Moon, comets and exoplanets, and to Earth's dayside magnetopause, and is used to interpret in situ particle and magnetic field observations from missions including MAVEN, Mars Express, Venus Express, Solar Orbiter and BepiColombo.
```

The first paragraph is the maintainers' own README wording, preserved word for word. HSSI stores that
paragraph with the README's fixed-width hard-wrap newlines embedded mid-sentence; those are rewrapped
here into flowing prose, which is a formatting repair rather than a rewording — no word is changed,
added, or removed in that paragraph.

The four added paragraphs are enrichment, not replacement. The stored description says what RHybrid is
and who distributes it but nothing about the physics, the configurable inputs, the outputs, the tooling
or the bodies and missions it is used for, which leaves a prospective user unable to judge whether the
code is useful to them — the specific thing the form asks this field to support. Sources for the
additions, all authoritative:

- The quasi-neutral hybrid description and the finite-Larmor-radius / multi-species rationale are
  paraphrased from the developers' own model documentation at
  `https://planets.fmi.fi/modeling.html`, the site this repository declares as its GitHub homepage.
- The Corsair / ParGrid / VLSV / Zoltan sentence follows the README's own "SIMULATION CODE" section and
  `INSTALL`'s build recipe.
- The configuration inventory is read from `src/user.cpp` (the `cr.get(...)` parameter registrations),
  `src/magnetic_field.h`, `src/resistivity.h`, `src/neutral_profiles.h`, and the `examples/*.cfg`
  files.
- The output inventory is read from `src/operator_userdata.cpp`, `src/diagnostics.h`,
  `src/detectors.cpp` and the log-column headers in `src/user.cpp`.
- The tooling inventory is read from `tools/` and from the documented post-processing sessions in
  `INSTALL` and `examples/venus.txt`.
- The bodies-and-missions closing paragraph is drawn from the example configurations, `pubs.txt`, and
  the developers' model and examples pages (which is where the Moon application is documented).

The maintainers' paragraph is kept first and intact deliberately, so that it remains separable: if a
later refresh decides to publish only their wording, that paragraph alone is the correct value — with
the newlines rewrapped, since the embedded hard wraps are a copy artifact rather than intended
formatting.

### 9. Concise Description (OPTIONAL)
```
RHybrid (paRallel Hybrid) is a parallel C++/MPI ion-kinetic hybrid plasma simulation platform for the solar wind and plasma interactions of planets, moons, comets and exoplanets.
```
178 characters, within the field's 200-character limit.

Worth having rather than relying on the automatic preview: the first 200 characters of the description
run out at "…The RHybrid code is originally developed at the", one word short of naming the developing
institution, and never reach anything about the model's physics, its inputs, or its outputs — the
second half of the preview is spent on provenance and licensing rather than on what the software does.
This sentence keeps the README's own opening formulation and its "paRallel Hybrid" expansion while
substituting the concrete body list for the vaguer "celestial bodies" and naming the ion-kinetic
hybrid method, which is the single most distinguishing fact about the code.

### 10. Publication Date (RECOMMENDED)
`2016-01-08`

This date was already on the record, but it was worth re-deriving because it coincides with the
repository's creation timestamp, which
would ordinarily be a weak proxy. It is not a proxy here. The distinct candidate events are:

- **Development start, 2015.** The README reads "Copyright (c) 2015- Finnish
  Meteorological Institute", and every `src/` header carries the same 2015 start date (one tool,
  `tools/rhb_log2pdf.sh`, reads "Copyright 2014-"). This is when
  work began in house, not when the software was published, so it is not Field 10.
- **Repository creation, 2016-01-08.** GitHub reports `created_at = 2016-01-08T11:07:36Z`, matching the
  first commit `aaa1926` (2016-01-08 13:07:36 +0200), which added a one-line `README.md` and nothing
  else.
- **First public release of the code, 2016-01-08.** The *second* commit, `5fade43`, landed 56 seconds
  later at 2016-01-08 13:08:32 +0200 and added the complete working source tree — 35 files and 7,831
  insertions, including `src/user.cpp` (1,038 lines), `src/hybrid_propagator.cpp` (1,420 lines),
  `src/particle_injector.cpp`, `src/magnetic_field.h`, `src/neutral_profiles.h` and the Mars, Venus,
  comet and anomaly example configurations. The complete, runnable model was therefore public on
  2016-01-08, the same calendar date in both local time and UTC.
- **Reference paper publication, February 2018.** Crossref gives `issued = 2018-02` for
  doi:10.1002/2017JA024884. That is the publication date of the *paper describing* the software and
  belongs to Field 14, not here.

So `2016-01-08` is correct not because it is the repository's birthday but because the software itself
was published that day. Confidence: high. There is no earlier public release to prefer: the repository
carries no tag and no GitHub release (see Field 12), so the first source-bearing commit is the
first publication. The one thing that cannot be verified from outside is whether the repository was
public from its first day; GitHub exposes no visibility history, and `created_at` is the best available
evidence.

### 11. Publisher (RECOMMENDED)
- **Organization:** Finnish Meteorological Institute
- **Publisher Identifier:** `https://ror.org/05hppb561`

The software states its own publisher: "The RHybrid code is
**distributed** under the GPL v3 open source license **by the Finnish Meteorological Institute**"
(README), repeated in the example acknowledgement text the README asks users to reproduce. FMI is also
the copyright holder in every source header and the owner of the `fmihpc` GitHub organization.

**Rejected: `GitHub`.** The form's how-to-fill text says to indicate the repository host when no DOI
has been obtained, and no DOI has been obtained here (Field 2), so GitHub is the by-the-book fallback.
It is not used because the fallback exists for the case where nothing better is known, and here the
work itself names its publishing entity explicitly. Recording "GitHub" would replace a real
institutional publisher with a hosting provider and would lose the ROR.

**Rejected: `Zenodo`.** Would be right if FMI had archived the code through the GitHub–Zenodo
workflow. It has not; the Zenodo records that mention RHybrid are a fork snapshot and third-party
paper supplements (Field 2).

**Rejected: `Aalto University`.** A co-copyright-holder from 2018 in every source header, but the
README's distribution statement names only FMI. Aalto is recorded as an author affiliation instead
(Field 6).

### 12. Version (RECOMMENDED)
**Not found — deliberately left empty.**

RHybrid declares no version, anywhere. This is a documented omission, not a gap to be filled by
inference, and the negative research is recorded in full so it is not repeated:

- **No git tags.** `git tag` on the current clone returns nothing; the GitHub `/tags` endpoint returns
  `[]`.
- **No releases.** The GitHub `/releases` endpoint returns `[]`. SoMEF's `download_url`
  (`…/rhybrid/releases`) points at an empty releases page.
- **No version string in the source tree.** A repository-wide search for "version", excluding GPL
  boilerplate, yields only prose ("The latest version of RHybrid can be downloaded at:", "This script
  version is for multiple runs", "TBD: faster vectorized version") and one commented-out VTK XML
  attribute `version='0.1'` in `tools/vlsv_to_vtk.py`, which is the VTK file-format version, not
  RHybrid's.
- **No package or citation metadata of any kind.** There is no `CITATION.cff`, `codemeta.json`,
  `.zenodo.json`, `CHANGELOG`, `setup.py`, `pyproject.toml`, `DESCRIPTION` or `Project.toml`.
- **The build system deliberately stamps a fingerprint instead of a version.** `src/Makefile`
  assembles a `COMPILEINFO` string from `date --iso-8601=seconds`, `whoami`, `hostname`, `pwd` and the
  compiler flags, and `src/do_compile_corsair.sh` logs `git show -q`, `git status` and `git diff` for
  both `rhybrid` and `corsair`. Provenance is recorded per build by commit and compile environment —
  which is a design choice, and an explanation of why no version number exists.
- **No archival record supplies one.** Of the five Zenodo records matching "rhybrid", only the fork
  snapshot `10.5281/zenodo.10836240` carries a `version` field, and its value is the literal string
  `03182024` — the datestamp of a `parkusa/rhybrid_vc` fork tag, not an RHybrid release identifier.
  The two "Rhybrid Code and Parameter Table" supplements have no version. ASCL has no entry. The
  developers' model page publishes no version.

Explicitly **not** used as a version, because each would be fabrication: the HEAD commit SHA
`2df55d51…`; the HEAD commit date 2026-06-08; the repository creation year; the GitHub `updated_at` or
`pushed_at` timestamps; and the fork's `03182024` datestamp.

One trap worth carrying forward. The record holds a version row in which every subfield is blank —
no number, no release date, no description, no version PID. HSSI's view renders such a row by
prefixing the software name to the version number, producing a string like `"RHybrid - "`. That is a
presentation artifact, not a stored value, and it must not be mistaken for one or copied into a
future update. The field stays empty; if FMI ever tags a release, that tag becomes the value.

### 13. Programming Language (RECOMMENDED)
- `C++`
- `Python 3.x`
- `Other`

These three were already on the record and were confirmed rather than changed. GitHub's language
breakdown for the repository is C++ 551,208 bytes, Python 141,424, Shell 22,530, Makefile 3,726,
C 1,219.

- `C++` — the model itself; `src/` is 11,119 lines of C++ across 24 source files, built with `-std=c++17` (`INSTALL`).
- `Python 3.x` — the twelve Python scripts in `tools/` plus `tests/run_tests.py`; all are Python 3 (f-string-free
  but using `pathlib`, `argparse`, `subprocess.run(...).returncode` and Python-3 `print()`), and the
  HPC job script loads a `python-data/3.10` module.
- `Other` — the correct home for the Shell scripts (`tools/*.sh`, `src/do_compile_corsair.sh`, the
  `.slrm` SLURM scripts) and the Makefiles, neither of which has a row in the `ProgrammingLanguage`
  vocabulary.

`C` was considered and not added: GitHub attributes 1,219 bytes of C, but the repository contains no
`.c` file and no C source is compiled by `src/Makefile`. `Python 2.x` was considered and rejected — no
script is Python 2 compatible.

### 14. Reference Publication (RECOMMENDED)
`https://doi.org/10.1002/2017JA024884`

This is the README's own designation, under the heading
"Main reference for RHybrid": Jarvinen R., Brain D.A., Modolo R., Fedorov A., Holmström M. (2018),
*Oxygen Ion Energization at Mars: Comparison of MAVEN and Mars Express Observations to Global Hybrid
Simulation*, J. Geophys. Res. 123, 1678-1689, doi:10.1002/2017JA024884. Verified against Crossref:
title, journal, volume, page range and the 2018-02 issue date all match, and the first author's ORCID
matches the one HSSI stores for him.

The distinction between this field and Field 27 is the README's, not ours: the README names exactly one
"Main reference", and `pubs.txt` lists the other thirteen as "Peer-reviewed scientific publications
with RHybrid". This DOI appears in both places (it is the last line of `pubs.txt`) and is recorded here
only, to avoid duplicating it across the two fields.

### 15. License (RECOMMENDED)
- **License:** `GNU General Public License v3.0 or later`
- **License URI:** `https://spdx.org/licenses/GPL-3.0-or-later.html`

Matched against the live `License` vocabulary.

The GPL variant and version are consistent across every source of truth for RHybrid's own code (the
one vendored third-party file is treated separately below), and the "or later" qualifier is
explicit:

- `COPYING` is the full text of the "GNU GENERAL PUBLIC LICENSE, Version 3, 29 June 2007".
- Every one of the 24 source files in `src/`, plus `tests/run_tests.py`, `tools/rhb_dashboard.py`,
  `tools/rhb_log2pdf.sh` and `tools/rhb_log2pdf_all.sh`, carries the same header: "you can
  redistribute it and/or modify it under the terms of the GNU General Public License as published by
  the Free Software Foundation, **either version 3 of the License, or (at your option) any later
  version**". That clause is what makes this GPL-3.0-**or-later** rather than GPL-3.0-only.
- The README states the code "is distributed under the GPL v3 open source license", which agrees with
  the headers; the README simply does not repeat the "or later" qualifier. There is no disagreement
  between the two — the README is the short form and the headers are the operative grant.
- GitHub's licence detector reports `spdx_id = GPL-3.0` (its generic GPL-3.0 key), as does SoMEF, which
  reads the same GitHub field. Neither distinguishes `-only` from `-or-later`; the source headers do,
  and they are authoritative.

One genuine internal inconsistency, recorded for completeness rather than as a problem: the vendored
Analysator module `tools/vlsvparticles.py` carries a GPL "version 2 of the License, or (at your
option) any later version" header from Analysator, along with Analysator's own copyright. That is a
third-party file's licence, not RHybrid's, and GPL-2-or-later is compatible with distribution under
GPLv3. It does not change this field.

**Rejected:** `GNU General Public Licenses (GPL version 2)` (wrong version — that is only the vendored
file's own grant); `Other` (unnecessary, the exact SPDX-titled row exists); `GNU Lesser General Public
License v3.0 only` and the LGPL-2 row (wrong licence family entirely).

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
Twenty-six terms, one concept per entry, lower case. Keywords is
the only open vocabulary in the form, so the live Keyword vocabulary was checked term by term to
reuse existing rows rather than mint near-duplicates. No row count is quoted here on purpose: this
list grows whenever anyone submits a new keyword, so any number recorded would be stale by the next
check — re-derive any existing/new split against the live list rather than trusting a figure.
The terms marked *(new row)* had no row on the live list when they were resolved and were minted
for this record; the rest reuse rows that already existed.

`plasma` · `space plasma` · `plasma physics` · `space physics` · `space weather` · `solar wind` ·
`magnetosphere` · `magnetosheath` · `planetary magnetospheres` · `induced magnetosphere` *(new row)* ·
`foreshock` *(new row)* · `shock waves` · `ultralow-frequency waves` · `ion escape` *(new row)* ·
`particle distributions` · `simulation` · `hybrid simulation` *(new row)* · `physics-based model` ·
`model-data comparison` · `high performance computing` · `c++` · `planetary science` · `mars` ·
`venus` *(new row)* · `mercury` *(new row)* · `exoplanets` *(new row)*

Justification by group:

- Plasma and discipline terms (`plasma`, `space plasma`, `plasma physics`, `space physics`,
  `space weather`) — the README's own framing ("kinetic plasma simulation model platform") and the
  developers' description of the team as a "planetary space weather research team".
- Regions and structures (`solar wind`, `magnetosphere`, `magnetosheath`, `planetary magnetospheres`,
  `induced magnetosphere`) — mirror Field 5 and the physics every run produces: a bow shock,
  magnetosheath and either an intrinsic (Mercury, Earth) or induced (Mars, Venus, comet)
  magnetosphere. `induced magnetosphere` is minted because it is the class of system RHybrid is most
  used on and no existing row expresses it.
- Phenomena (`foreshock`, `shock waves`, `ultralow-frequency waves`, `ion escape`) — the dominant
  science themes in `pubs.txt`: four of the fourteen papers are on ULF foreshock waves at Mercury,
  Mars and Venus and four are on planetary ion escape, with one paper (Jarvinen et al. 2020,
  doi:10.1029/2020GL087462) belonging to both groups. `foreshock` and `ion escape` have no existing row and no
  suitable near-match, so they are minted; `ultralow-frequency waves` and `shock waves` already exist
  and are reused instead of minting `ULF waves` or `bow shock`.
- Method (`simulation`, `hybrid simulation`, `physics-based model`, `particle distributions`,
  `model-data comparison`) — the hybrid/QNH method is the code's defining property and has no existing
  row, so `hybrid simulation` is minted. `particle distributions` reflects the developers' statement
  that ion velocity distributions "evolve self-consistently"; `model-data comparison` reflects the main
  reference and the Solar Orbiter and MAVEN comparison studies.
- Implementation (`high performance computing`, `c++`) — MPI, Zoltan load balancing and the SLURM
  scripts; both rows already exist.
- Bodies (`planetary science`, `mars`, `venus`, `mercury`, `exoplanets`) — each has a dedicated example
  configuration, neutral profile, or publication. `mars` already exists; `venus`, `mercury` and
  `exoplanets` are minted for parity with it.

Considered and not selected: `bow shock` and `mpi` (would be near-duplicates of the reused
`shock waves` and `high performance computing` rows); `models` (too generic beside `simulation` and
`physics-based model`); `moon` and `comets` (the Moon application is documented only on the
developers' examples page and comets only by `examples/comet.cfg`, so both are real but thin — a
later refresh with a published comet or lunar study should add them); `crustal field` (suggested by
`examples/anomaly.cfg`, a 1 km-scale object with a 96 nT surface field in a ±206 km box, which is
almost certainly a Martian crustal magnetic anomaly setup, but the config never says so and no paper
in `pubs.txt` covers it — the inference is not strong enough to mint a row); `maven` and
`bepicolombo` (missions belong in Field 32, where they are recorded with SPASE identifiers).

### 17. Data Sources (OPTIONAL)
**Not found — deliberately left empty.**

RHybrid ingests no external data. Everything it reads is either its own prior output or a
locally-written text file:

- Run configuration: ASCII `.cfg` files parsed through Corsair's config reader (`cr.get(...)`
  throughout `src/user.cpp`).
- Optional detector coordinates: local ASCII files listing `x y z` triplets, read by
  `readRealsFromFile` in `src/user.cpp` for `DetectorParticle.coordinate_file` and
  `DetectorBulkParameter.coordinate_file`.
- Restart: its own VLSV state files (`[Restart] filename =` in every example configuration).

The post-processing tools read only VLSV files and log files produced by the run itself. There is no
HTTP, FTP, S3, archive-client, or web-service code anywhere in the repository.

The whole `DataInput` vocabulary is enumerated here as the reason this field is correctly empty: `AMDA`, `CDAWeb`, `das2`, `FTP/FTPS Directories`, `GFZ`, `HAPI`, `HTTP/HTTPS Directories`,
`Madrigal`, `Observatory/Mission-specific`, `OMNIWeb`, `Other`, `S3/Cloud-aware`, `SSCWeb`, `TAP`,
`The Virtual Solar Observatory.`, `VirES`, `WDC`. None describes a local configuration file. In
particular `Other` was considered and rejected: selecting it would tell an HSSI user that RHybrid
supports some unlisted *data source*, when in fact it supports none — an empty field is the truthful
answer. `Observatory/Mission-specific` was also considered, since Field 32 does list missions; it is
rejected because that value is for software that reads a mission's data, and RHybrid reads no mission
data (see Field 31).

### 18. Input File Formats (RECOMMENDED)
- `ascii`
- `Other`

Both were matched against the live `FileFormat` vocabulary, which Fields 18 and 19 share.

- `ascii` — the run configuration files (`examples/*.cfg`, `tests/test_empty_1d.cfg`) and the detector
  coordinate files read by `readRealsFromFile` in `src/user.cpp`, which skips blank lines and `#`
  comments and parses whitespace-separated reals.
- `Other` — **VLSV**, the FMI parallel simulation file format, used for restart input
  (`[Restart] filename =`) and as the input to each of the VLSV-reading post-processing tools
  (`alr.vlsvfile.VlsvReader(input_file)`); the log-plotting tools read the ASCII logs instead. VLSV has no row in the vocabulary, and `Other` is the
  form's instructed fallback.

Considered and rejected: `HDF5` and `netCDF3/4` (VLSV is its own binary format with an XML footer, not
built on either); `CDF`, `FITS`, `csv`, `JSON`, `IDL.sav`, `ISTP-Compliant`, `Zarr` (no reader for any
of them exists in the repository).

### 19. Output File Formats (RECOMMENDED)
- `ascii`
- `Other`

- `ascii` — `logfile.txt` (the main run log), `field.log` and per-population `pop*.log` files
  (`src/diagnostics.h`, with the column definitions written by `src/user.cpp`, e.g. "% 10. Escape rate
  [#/s]", "% 14. Kinetic energy escape rate [J/s]"), the detector particle and bulk-parameter files
  written by `src/detectors.cpp`, and `time_series.dat` from `tools/create_time_series_point.py`.
- `Other` — two formats with no vocabulary row: **VLSV** state files, reduced state files and
  macroparticle output written through `simClasses.vlsv.writeArray(...)` in
  `src/operator_userdata.cpp` and `src/diagnostics.h`; and **VTK XML** (`.vti` for the grid, `.vtp`
  for particles) written by `tools/vlsv_to_vtk.py` via PyVista.

Considered and not listed: PNG, PDF and MP4 figures and movies from the plotting tools and
`rhb_log2pdf.sh` — these are graphics, not data file formats, and the vocabulary has no row for them.

### 20. Operating System (RECOMMENDED)
- `Linux`

Evidence for Linux is direct: `INSTALL` is headed "EXAMPLE COMPILATION — Ubuntu 22.04.5 LTS (Apr 2,
2025)" and gives a complete, dated, working recipe; the SLURM batch scripts target Linux HPC clusters
with Lmod `module load` and Lustre (`/usr/bin/lfs find`).

`Mac` was considered and deliberately **not** selected, on concrete evidence rather than absence of
evidence: `src/Makefile` builds its `COMPILEINFO` string with `date --iso-8601=seconds`, a GNU
coreutils option that BSD/macOS `date` does not accept, so the shipped build would fail on macOS
without modification. `Windows`, `Solaris` and `MobilePlatform` have no supporting evidence.

`Operating System Independent` was considered and rejected: the code is a compiled MPI application
with a Linux-specific build, and claiming OS independence would mislead a user into an unsupported
build. A POSIX/Unix port is plausible — the C++17 source itself uses nothing Linux-specific — but
plausible is not supported, and this field asks which systems the software "can successfully be
installed on".

### 21. CPU Architecture (RECOMMENDED)
- `HPC or HEC`
- `x86-64`

Both were matched against the live `CpuArchitecture` vocabulary.

- `HPC or HEC` — direct evidence, and the primary target. RHybrid is MPI-parallel throughout, uses
  Zoltan for dynamic load balancing across MPI processing elements, and ships SLURM batch scripts for
  multi-node runs (`examples/slurm_batch_script.slrm`: 10 nodes × 20 tasks, 100 GB) and multi-node
  post-processing (`tools/plotter_rhybrid_2d_slice_job.slrm`: 2 nodes × 15 cores, 185 GB, `srun`,
  Lustre-aware cleanup). `INSTALL`'s smallest working example is still `mpirun -n 4`.
- `x86-64` — circumstantial rather than stated, and flagged as such. `INSTALL` targets Ubuntu 22.04.5
  LTS with a plain `../configure && make` for Zoltan and no architecture flags; the HPC job script
  loads a `StdEnv` / `gcc/11.3.0` / `boost` / `python-data/3.10-24.04` module stack characteristic of
  an x86-64 national HPC environment. No file in the repository names an architecture explicitly.

`CPU Independent` was considered and rejected: RHybrid must be compiled for a target architecture, so
the value would be inaccurate even though the C++17 source contains no architecture-specific
intrinsics or assembly. `GPU` was considered and rejected — there is no CUDA, HIP, OpenACC, OpenMP
offload or any other accelerator code path. `Apple Silicon arm64`, `Linux aarch64 or arm64`,
`ppc64le` and `Sun (SPARC)` are all plausible in principle for portable C++17 plus MPI, but nothing in
the repository or its documentation demonstrates a build on any of them.

### 22. Related Phenomena (OPTIONAL)
- `Solar Wind`

Matched against the live `Phenomena` vocabulary.

`Solar Wind` is certain: the README scopes the model to "the solar wind and plasma interactions of
celestial bodies", `solarwind` is a named particle-population type in `src/user.cpp`, and the
solar-wind interaction is the subject of essentially every entry in `pubs.txt`.

The vocabulary is the reason nothing else is selected. Its rows are `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and
`X-ray emission` — a solar- and Earth-oriented list with no row for any of the phenomena RHybrid
actually specialises in: bow shocks, ion foreshocks, ULF waves, induced magnetospheres, planetary ion
escape, magnetotail dynamics. Those are recorded in Keywords (Field 16), which is the open vocabulary
and the form's designated home for phenomena that have no row here. This field is not thin by
oversight.

Individually considered and rejected:

- `X-ray emission` — the closest genuine call. `pubs.txt` includes Yang, Jarvinen, Guo, Sun,
  Koutroumpa et al. (2023), doi:10.26464/epp2023059, which pairs RHybrid global kinetic simulations
  with Soft X-ray Imaging of Earth's dayside magnetopause. Not selected because RHybrid computes no
  X-ray emission: it outputs plasma moments and fields, and the solar-wind charge-exchange emission in
  that study was derived from its output externally. Recorded here so a future agent can weigh it
  again if emission modelling is ever added to the code.
- `Coronal Mass Ejections` — RHybrid can be driven with any upstream conditions, including
  ICME-like ones, but no example configuration or `pubs.txt` entry does so, and the model does not
  simulate CME initiation or propagation.
- `Geomagnetic Storms` — the single Earth application is a steady quasi-radial-IMF magnetopause study,
  not a storm simulation, and RHybrid produces no geomagnetic indices.
- `Coronal Heating`, `Solar Corona`, `Solar Flares` — the model does not simulate the Sun.

### 23. Development Status (RECOMMENDED)
`Active`

Matched against the live `RepoStatus` vocabulary. repostatus.org defines `Active` as "reached stable, usable state and being actively developed", and
both halves hold.

*Stable and usable:* fourteen peer-reviewed publications 2018–2024 report science done with the code
(`pubs.txt`); `INSTALL` gives a complete, dated (Apr 2025) build-and-run recipe with a success check;
`tests/run_tests.py` is a parameter-sweep regression suite that compares modelled moments against the
prescribed upstream conditions.

*Actively developed:* on the default branch `master`, 56 commits in 2026 (through the current HEAD,
2026-06-08), 77 in 2025, 68 in 2024. These are substantive, not housekeeping: a separate configuration
section for electron pressure, electron number density added as a selectable output variable,
obsolete output parameters and the unused background charge density removed, configuration variables
renamed for clarity (`minRhoQi` → `min_ion_charge_density_relative`), new SLURM job scripts and
post-processing examples. The README states the developers "are open for scientific collaborations and
further development of the model and are committed to open science", and names an active contact.

**Signals deliberately not used.** At the time of extraction the GitHub API reported
`pushed_at = 2026-08-10T12:15:10Z` and `updated_at = 2026-07-30T17:08:05Z`, both later than the
default branch's HEAD commit (2026-06-08). Those fields move on pushes to *any* ref and on
repository-metadata changes, and this repository carries nine non-`master` remote branches
(`airless_objects`, `conic_inner_boundary`, `harmonized_config_file_var_names`, `iljah-patch-1`,
`new_B_splitting`, `new_var_handling`, `shocktube`, `test_particle_mode`, `xmin_boundary`). The status above rests on the default branch's own commit history and the repository's own
statements instead.

Rejected: `WIP` — there is no "no stable, usable public release yet" here; the code is published,
documented, tested and cited, and the absence of tagged releases (Field 12) is a release-management
choice, not immaturity. `Inactive`, `Unsupported`, `Abandoned`, `Suspended` — contradicted by 2026
commit activity and a named active maintainer. `Moved` — the README points to this repository as the
canonical download location, and GitHub reports `archived = false`.

### 24. Documentation (RECOMMENDED)
`https://github.com/fmihpc/rhybrid`

This is where RHybrid's documentation actually lives, and the form explicitly permits the access URL
when they coincide. The repository root holds the `README` (overview, component libraries, citation
and contact) and `INSTALL` (the complete installation and post-processing walkthrough); `examples/`
holds sixteen annotated run configurations plus `examples/venus.txt`, a worked post-processing session;
`doc/` holds two algorithm notes (`cell_indexing.pdf`, `field_algorithm.pdf`); `tools/` scripts carry
usage headers, and `tools/plotter_rhybrid_2d_slice.py` documents its full argument grammar in a
40-line comment block.

Alternatives considered:

- `https://planets.fmi.fi/modeling.html` — the developers' scientific description of the model
  (the hybrid/QNH approach, the equations, the applications). It is authoritative and is used
  throughout this dossier as a source, but it contains no installation instructions, which this field
  asks for, and it describes two codes (RHybrid and HYB) rather than documenting this one. It is a
  reasonable secondary value if HSSI ever supports more than one documentation URL.
- `https://github.com/fmihpc/rhybrid/blob/master/INSTALL` — more precisely the installation
  instructions, but it pins a branch path and omits the README, examples and algorithm notes.
- `https://github.com/fmihpc/rhybrid/tree/master/doc` — only two algorithm PDFs behind a one-line
  `doc/README`; not the documentation a new user needs.
- A GitHub wiki — the repository has the wiki feature enabled (`has_wiki = true`), but
  `https://github.com/fmihpc/rhybrid/wiki` redirects to the repository, i.e. the wiki is empty. Worth
  recording so a future agent does not go looking for it. There is no Read the Docs site, no
  `.readthedocs.yml`, and no GitHub Pages site (`has_pages = false`).

### 25. Funder (OPTIONAL)
- **Organization:** European Research Council
- **Funder Identifier:** `https://ror.org/0472cxd90`

Confidence: moderate. The attribution is well sourced, but the source is the developers' project site
rather than the repository, which is the reason it is recorded with that qualification rather than as
a certainty.

Evidence: the repository declares `https://planets.fmi.fi` as its GitHub homepage, and that site's
Missions & Projects page states "Our team's work is mainly funded through the European Research
Council's Consolidator Grant project named Mercury in the solar wind: adaptive kinetic model for space
weather at solar system's innermost planet (MEOW). **In the project, we develop novel methods for
particle-based global space weather modeling** and include detailed electron physics description as
well as apply the model to interpret space plasma observations on the BepiColombo mission." The same
site's Modeling page identifies RHybrid as that team's model platform, and its home page repeats
"Our work is funded by the European Research Council through the Mercury in the solar wind (MEOW)
project". So the funded activity is the development of this model, stated by its developers on the
site the repository points to. The grant carries a citable identifier (`https://doi.org/10.3030/101124960`).

Caveat a later refresh should keep in mind: **the repository itself contains no funding
acknowledgement.** The README asks users to acknowledge FMI and the code, not a grant. If a maintainer
adds a funding statement, that supersedes this inference.

**Considered and not selected: Research Council of Finland** (formerly Academy of Finland),
`https://ror.org/05k73zm37`, award 310444. Crossref funding metadata credits "Academy of Finland"
award 310444 on two RHybrid modelling papers led by the code's principal developer — Jarvinen, Kallio
& Pulkkinen (2022), doi:10.1029/2021JA030078, and Kallio, Jarvinen et al. (2022),
doi:10.1029/2022GL101850. Not selected because that is funding acknowledged for *studies performed
with* the model, which is a weaker claim than funding the software; by the same standard the record
would also have to absorb the CNRS, CNES, Chinese Academy of Sciences and NSFC grants that Crossref
attaches to other `pubs.txt` papers. The identifiers are recorded so that a later refresh judging
paper-level acknowledgement sufficient can add them without repeating the research.

Also noted: the developers' missions page describes participation in NASA's Astrobiology ICAR team
"Retention of Habitable Atmospheres in Planetary Systems" (RHAPS, funded 2023–2028), which is
thematically connected to the exoplanet atmosphere-retention work RHybrid has been used for. Not
recorded as a funder because the page frames FMI as a collaborating partner rather than as a recipient
funding this software.

### 26. Award Title (OPTIONAL)
- **Award Title:** `Mercury in the solar wind: adaptive kinetic model for space weather at solar system's innermost planet`
- **Award Number:** `101124960`

Same source and same moderate confidence as Field 25: the ERC Consolidator Grant project
MEOW, named in full on `https://planets.fmi.fi/missions.html` with the grant record linked as
`https://doi.org/10.3030/101124960` (European Commission grant 101124960).

The title is recorded as the funder states it, without the "(MEOW)" acronym suffix, since the form asks
for the full award title. Its length is 102 characters, within the `Award.name` 128-character storage
limit that would otherwise fail the write.

The record previously pointed at a blank award row — no name, no identifier, no funder — which
carried no information and was not a value worth preserving. It was unlinked from this software and
the ERC/MEOW award recorded above took its place. That blank row still exists in HSSI and is still
referenced by another software record, so nothing was orphaned by unlinking it here, and it should
not be treated as deletable debris by a later cleanup. Identifying what the blank row is meant to
represent belongs to the record that still holds it, not to this one.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Thirteen DOIs, taken from `pubs.txt`, the repository's own curated
list headed "Peer-reviewed scientific publications with RHybrid". The fourteenth entry in that file is
the README's designated main reference and is recorded in Field 14 instead, so it is not duplicated
here.

1. `https://doi.org/10.3847/1538-4357/ad8159` — Zhou J., Liu K., Jarvinen R., Kallio E. et al. (2024), *Hybrid Simulations of the Martian Magnetotail Twist*, ApJ 976, 7.
2. `https://doi.org/10.1093/mnras/stae2032` — Hinton P.C., Brain D.A., Schnepf N.R., Jarvinen R., Ramstad R. (2024), *Atmospheric ion escape and solar wind deposition as a function of planetary radius*, MNRAS 533, 3999-4006.
3. `https://doi.org/10.26464/epp2023059` — Yang Z.W., Jarvinen R., Guo X.C. et al. (2023), *Deformations at Earth's dayside magnetopause during quasi-radial IMF conditions: Global kinetic simulations and Soft X-ray Imaging*, Earth Planet. Phys. 8, 1-11.
4. `https://doi.org/10.3847/1538-4357/acc655` — Wang L., Huang C., Du A. et al. (2023), *Kelvin-Helmholtz Instability at Mars: In Situ Observations and Kinetic Simulations*, ApJ 947, 51.
5. `https://doi.org/10.1029/2022JA031023` — Stergiopoulou K., Jarvinen R., Andrews D.J. et al. (2023), *Solar Orbiter Data-Model Comparison in Venus' Induced Magnetotail*, JGR 128, 2.
6. `https://doi.org/10.1029/2022GL101850` — Kallio E., Jarvinen R., Massetti S. et al. (2022), *Ultra-low frequency waves in the Hermean magnetosphere: On the role of the morphology of the magnetic field and the foreshock*, GRL 49, 24.
7. `https://doi.org/10.1029/2021JA030078` — Jarvinen R., Kallio E., Pulkkinen T.I. (2022), *Ultra-low Frequency Foreshock Waves and Ion Dynamics at Mars*, JGR 127, 5.
8. `https://doi.org/10.3847/1538-3881/abb465` — France K., Duvvuri G., Egan H. et al. (2020), *The High-energy Radiation Environment around a 10 Gyr M Dwarf: Habitable at Last?*, AJ 160, 5.
9. `https://doi.org/10.1029/2020GL087462` — Jarvinen R., Alho M., Kallio E., Pulkkinen T.I. (2020), *Oxygen Ion Escape From Venus Is Modulated by Ultra-Low Frequency Waves*, GRL 47, 11.
10. `https://doi.org/10.1093/mnras/stz3257` — Jarvinen R., Alho M., Kallio E., Pulkkinen T.I. (2020), *Ultra-low frequency waves in the ion foreshock of Mercury: A global hybrid modeling study*, MNRAS 491, 4147-4161.
11. `https://doi.org/10.1093/mnras/stz1819` — Egan H., Jarvinen R., Ma Y., Brain D.A. (2019), *Planetary magnetic field control of ion escape from weakly magnetized planets*, MNRAS 488, 2108-2120.
12. `https://doi.org/10.1093/mnras/stz788` — Egan H., Jarvinen R., Brain D.A. (2019), *Stellar influence on heavy ion escape from unmagnetized exoplanets*, MNRAS 486, 1283-1291.
13. `https://doi.org/10.1029/2017JA025068` — Egan H., Ma Y., Dong C., Modolo R., Jarvinen R. et al. (2018), *Comparison of Global Martian Plasma Models in the Context of MAVEN Observations*, JGR 123, 3714-3726.

Two of these are load-bearing elsewhere in this dossier and should not be pruned without reading the
fields that cite them: entry 3 is the sole evidence for `Earth Magnetosphere` in Field 5 and for the
`X-ray emission` rejection in Field 22; entry 5 is the sole evidence for Solar Orbiter in Field 32.

Also present in the repository but not listed here: two conference abstracts cited in configuration
file headers (Jarvinen et al., AGU Fall Meeting 2015, P21A-2092, in
`examples/mars_agufm2015_run1.cfg` and `run2.cfg`). They have no DOI and are not peer-reviewed, so they
fall outside what this field asks for; they are noted because they are the earliest recorded RHybrid
results and establish the MAVEN/Mars Express run provenance used in Field 32.

Deliberately not added: RHybrid papers published after `pubs.txt` was last updated. Riku Järvinen's
ORCID record lists further items that appear to be RHybrid work (for example "The Energetic Oxygen Ion
Beams in the Martian Magnetotail Current Sheets" and "Localized Hybrid Simulation of Martian Crustal
Magnetic Cusp Regions"), but `pubs.txt` is the maintainers' own curation of which publications belong
to the model, and extending it from an author's full bibliography would substitute our judgement for
theirs. A later refresh should re-read `pubs.txt` rather than ORCID.

### 28. Related Datasets (OPTIONAL)
**Not found.**

No dataset is referenced anywhere in the repository: no data DOI, no archive link, no downloaded input
dataset. This follows from Field 17 — RHybrid consumes no observational data, so there is no dataset
whose analysis it supports.

Considered and not selected, so the research is not repeated: two Zenodo datasets produced from
RHybrid runs by a third-party user group —
- `10.5281/zenodo.19247602`, "Magnetic field data of RHybrid simulation at the MAVEN orbital
  locations" (Zhou J., 2026-03-27), and
- `10.5281/zenodo.11403027`, "rhybrid code" (Zhou J., 2024-05-31), which is deposited as a dataset
  despite its title.

Both are *outputs* of particular RHybrid runs, not datasets the software reads or supports analysis
of, and neither is deposited by the maintainers. Listing them would invert the relationship this field
records.

### 29. Related Software (OPTIONAL)
`https://github.com/fmihpc/hyb`

**HYB** is the peer this field exists to surface. The developers' own model page presents RHybrid and
HYB side by side as the team's two planetary particle-hybrid plasma simulation codes: "HYB is a highly
efficient serial C++ code for planetary particle hybrid plasma simulations using adaptive mesh
refinement and macroparticle splitting and joining methods. It has been used to study observations on
many missions like Mars Express, Cassini-Huygens, Venus Express, MAVEN and Rosetta missions."
Same institution, same `fmihpc` GitHub organization, same scientific task, complementary
implementation (serial + AMR versus parallel + uniform grid). That is precisely "software that
performs similar tasks but does not necessarily link together", and it is the single most useful
cross-reference for someone evaluating RHybrid. Confidence: moderate-high — the relationship is stated
by the developers, though the RHybrid repository itself never mentions HYB, and no source calls RHybrid
a fork or direct successor of HYB, so no such lineage is asserted.

**Corsair, ParGrid, VLSV and Zoltan are deliberately *not* recorded here.** They are RHybrid's core
dependencies, and the form's Field 29 text does say important dependencies belong in this field — so
this is a real classification choice, not an oversight. They are kept in Field 30, where the original
submitter put them, because all four *do* link together with RHybrid at build and run time, which is
the condition Field 29's own definition excludes ("does not necessarily link together (which would be
'interoperable software')"). Duplicating them across both fields would add no information and would
make the two fields indistinguishable for this record. The reasoning per package is in Field 30.

**Excluded as generic infrastructure** — recorded so a future pass does not add them: NumPy, SciPy,
Matplotlib and PyVista (imported by `tools/*.py`), Boost (`INC_BOOST` in `src/Makefile`), Open MPI
(`mpirun`, `OMPI_MCA_io=^ompio` in `INSTALL`), SLURM, gnuplot, Ghostscript and FFmpeg (invoked by
`tools/rhb_log2pdf.sh` and the movie pipeline). Each would be equally at home in an engineering, finance
or biology pipeline, and none says anything about RHybrid that is not equally true of most simulation
codes. The asymmetry with Zoltan is intentional, and it rests on RHybrid's configuration surface
rather than on Zoltan's prominence in the README: every run configuration file selects a Zoltan
partitioning algorithm by name and sets Zoltan's load-imbalance parameters, whereas MPI and Boost are
never named or selected in an RHybrid configuration and a user cannot address them at all. Field 30
carries the full reasoning, including the case for dropping Zoltan.

### 30. Interoperable Software (OPTIONAL)
- `https://github.com/fmihpc/corsair`
- `https://github.com/fmihpc/pargrid`
- `https://github.com/fmihpc/vlsv`
- `https://sandialabs.github.io/Zoltan/`
- `https://github.com/fmihpc/analysator`

The first four were already on the record and were retained; Analysator was the addition. HSSI stores
related-item entries of this kind with the placeholder name `UNKNOWN`, identified only by URL. That
placeholder is a storage artifact and is never user-visible, so it is not drift to correct — the URL
is what identifies each entry, and the URLs are right. Per package:

- **Corsair** — RHybrid is a Corsair simulation module, which is the strongest form of the
  plugin/extension relationship this field recognises. `INSTALL` copies `rhybrid/src/*` into
  `corsair/src/user/rhybrid/`, sets `SIM=rhybrid` in Corsair's `Makefile.arch`, and builds a
  `corsair_rhybrid` executable; `src/Makefile` produces `librhybrid.a` and symlinks it into
  `../../lib`, includes `../../../Makefile.${ARCH}`, and compiles against Corsair's
  `particleinjector`, `dataoperator`, `particlepropagator` and `gridbuilder` headers.
  `src/do_compile_corsair.sh` is a helper that lives in Corsair's main folder. Every one of the
  seventeen configuration files in `examples/` and `tests/` is a Corsair run-config file
  (all seventeen declare `gridbuilder = LogicallyCartesian` and carry `[Simulation]` and
  `[LoadBalance]` sections).
- **ParGrid** — the shared parallel data model. RHybrid's fields and macroparticles live in ParGrid
  user data arrays (`simClasses.pargrid.getUserData(...)`, `getUserDataDynamic<...>`,
  `pargrid::DataWrapper` in `src/particle_accumulator.cpp` and `src/user.cpp`) and RHybrid registers
  its own ParGrid data transfers; `INC_PARGRID` is on the include path in `src/Makefile`.
- **VLSV** — the shared interchange format. RHybrid writes every state file through
  `simClasses.vlsv.writeArray("VARIABLE", ...)` (`src/operator_userdata.cpp`) and its reduced-state
  writer in `src/diagnostics.h`; `INC_VLSV` is on the include path. VLSV is the format by which
  RHybrid output reaches Analysator and the wider FMI/Vlasiator tool chain, which is what makes it an
  exchange rather than a mere dependency.
- **Zoltan** — the coupling is exposed through RHybrid's own configuration surface, which is what
  separates it from the generic build-time infrastructure excluded in Field 29. All seventeen run
  configuration files in `examples/` and `tests/` carry a `[LoadBalance]` section in which the user
  selects a Zoltan partitioning algorithm by its Zoltan name — `methods = RCB` in fourteen of them and
  `methods = RANDOM` in the other three, each file carrying the alternative as a commented line — and
  all seventeen set Zoltan's load-balancing parameters (`tolerances = 1.05`,
  `processes_per_partition = 2`, with `maximum_load_imbalance` and `repartition_check_interval` in
  `[Simulation]`). Configuring an RHybrid run therefore means choosing and tuning Zoltan's behaviour
  directly, by name. Nothing comparable exists for MPI or Boost: neither is ever named or selected in
  an RHybrid configuration file, and a user has no way to address them at all. The README additionally
  names Zoltan with its URL alongside Corsair, ParGrid and VLSV as a library the code is built on
  ("Zoltan library (https://sandialabs.github.io/Zoltan/) is used for partitioning and balacing
  computational load between MPI processing elements"), `INC_ZOLTAN` is on the include path, and
  `INSTALL` pins v3.901 with a full configure-and-build recipe, so the combined environment is
  specific and tested.
- **Analysator** — the clearest demonstrated exchange in the repository, and the one that was missing
  from the record. Nine of the twelve Python scripts in `tools/` open RHybrid output through Analysator
  (`import analysator as alr`; `alr.vlsvfile.VlsvReader`, `alr.calculations.vlsv_intpol_points`), and
  `tests/run_tests.py` does the same through Analysator's earlier module name (`import pytools as pt`).
  `INSTALL` clones `https://github.com/fmihpc/analysator` as the first step of its recipe and documents
  `export PYTHONPATH=$PYTHONPATH:~/bin/analysator/` before running the post-processing examples;
  `examples/venus.txt` repeats it; `tools/plotter_rhybrid_2d_slice_job.slrm` has a
  `folder_analysator="/PATH/TO/ANALYSATOR/"` configuration variable. `tools/vlsvparticles.py` is a
  vendored Analysator module, still carrying Analysator's own copyright header. Output of one package
  read directly by the other, with a companion-tool relationship documented in the installation
  instructions — exactly what this field is for.

**The rejected classification, stated plainly.** The alternative was to move Corsair, ParGrid, VLSV and
Zoltan to Field 29 as "important software dependencies" and leave only Analysator here. That reading is
defensible — `INSTALL` shows RHybrid's source being compiled *into* Corsair rather than two peer tools
exchanging data, and dependency presence alone is never interoperability. It was not adopted because:
the form's Field 29 definition explicitly carves out software that links together and points it here;
each of the four participates in a concrete exchange or shared data model, cited above, rather than
merely appearing in a dependency list; none is generic infrastructure (all four are HPC or space-plasma
simulation components, and three are FMI space-plasma libraries); and the classification came from the
original submitter, with no evidence that it is wrong. Nothing was removed. Should a later refresh
prefer the stricter separation, the correct change is a move of these four to Field 29, never a
deletion — and Field 29's note records the same reasoning from the other side.

**Zoltan specifically — the tension, and how it was resolved.** Zoltan is the one entry here that does
not map cleanly onto any of the exchange types this field enumerates. Corsair is a plugin/extension
relationship, ParGrid is a shared data model, and VLSV is a shared and converted interchange format.
Zoltan, by contrast, performs an internal computational subroutine — domain decomposition — which is
structurally the same kind of relationship RHybrid has with MPI and Boost, and those are excluded as
generic infrastructure in Field 29. A strict reading of the field definition would therefore drop it.
Field 29 is not an obviously better home either, because it applies the same generic-infrastructure
exclusion, so dropping Zoltan from here means removing it from HSSI's machine-readable relationships
altogether and keeping the dependency only as prose in this dossier. The judgement recorded goes the
other way, on the configuration-surface evidence above: a coupling the user selects and tunes by name
in every run configuration is a difference in kind from MPI and Boost, not merely a difference in
prominence, and the entry was a submitted value with no evidence that it is wrong. Zoltan is therefore
recorded here by deliberate decision, not by default. That decision turns on a judgement about the
field definition rather than on any disputed fact, so a later refresh could reasonably reach the other
answer; the argument on both sides is set out above precisely so that any such re-decision needs no
new research, and so that Zoltan's presence is not mistaken for an oversight and quietly removed.

**Excluded** for the same reasons given in Field 29: NumPy, SciPy, Matplotlib, PyVista, Boost, Open
MPI, SLURM, gnuplot, Ghostscript, FFmpeg. Vlasiator was considered — Analysator originated as its
analysis package, and `tools/vlsvparticles.py` still carries a URL to the Vlasiator project in its
header — and rejected: nothing in RHybrid interoperates with Vlasiator itself, and the shared ancestry
runs through VLSV and Analysator, which are both already listed.

### 31. Related Instruments (OPTIONAL)
**Not found — omitted deliberately, with the negative research below.**

RHybrid is designed to support no specific instrument, and the resolution ladder was never reached
because nothing passes the relevance gate.

- **No instrument is named anywhere in the repository.** Not in the README, `INSTALL`, `pubs.txt`, the
  sixteen example configurations, the source, or the tools. Outside the publication titles carried by
  the README's main reference and by `pubs.txt`, the one place spacecraft appear is two
  configuration-file comment headers (`examples/mars_agufm2015_run1.cfg`, "Mars 25.01.2015 12:20
  (Run1, MAVEN inbound)", and `run2.cfg`, "(Run2, Mars Express inbound)"), which identify observation
  intervals, not instruments.
- **No instrument data is read, parsed, calibrated or processed.** RHybrid ingests only configuration
  files and its own VLSV restart files (Field 17). It implements no instrument-specific format,
  convention, response function, energy-channel definition, or field of view.
- **The facilities that look instrument-adjacent are generic by construction.** The optional detectors
  (`src/detectors.cpp`, `USE_DETECTORS`) are virtual probes at arbitrary coordinates read from an
  ASCII file — no instrument geometry or response. `tools/create_interpolation_along_trajectory.py`
  interpolates along an arbitrary point list, and its shipped example builds a synthetic circular
  orbit rather than reading any real ephemeris.
- **The data–model comparisons happen in the papers, not in the code.** The main reference compares
  RHybrid to MAVEN and Mars Express observations, and `pubs.txt` includes a Solar Orbiter comparison,
  but in every case the observational side is handled outside this repository. Under the field's own
  test — would someone working with, say, MAVEN STATIC or Mars Express ASPERA-3/IMA data reach for
  *this* software to handle that data — the answer is no. The mission-level relationship those studies
  do establish is recorded in Field 32, which is the right granularity for a simulation code.
- Instruments considered and dropped at the relevance gate, for the record: MAVEN STATIC, SWIA and MAG;
  Mars Express ASPERA-3 / IMA; Venus Express ASPERA-4; Solar Orbiter MAG; BepiColombo SERENA and MPO-MAG.
  Each is plausibly the instrument whose measurements a given RHybrid study was compared against, but
  none is named in the repository and none is supported by code. FMI's own participation in Mars
  Express ASPERA-3 and Juice PEP (developers' missions page) is instrument-team work by the same
  institute, not a property of this software.

This is a documented omission, which is a correct outcome for an instrument-agnostic simulation code.
No name is recorded without a SPASE identifier under any circumstances, so there is nothing here to
resolve or to flag as ambiguous.

### 32. Related Observatories (OPTIONAL)
Four entries, each bound to a single row of the live `InstrumentObservatory` vocabulary with
`type = 2`, with that row's `name` copied character for character. No row count is quoted, because
this vocabulary can grow whenever a submission supplies an unresolved name. What matters is the
guard: every row recorded below satisfies
`identifier.startswith("https://spase-metadata.org/")`, and no row in the vocabulary failed it when
these four were resolved, consistent with the PR #54 backfill — a dated observation about a shared
vocabulary rather than a standing property of it. A row that ever fails that guard is upstream drift
or an agent-created artifact and must be reported, never used.

1. **`Mars Atmosphere and Volatile EvolutioN`**
   `https://spase-metadata.org/SMWG/Observatory/MAVEN`
   *Evidence:* the README's designated main reference is a MAVEN data–model comparison ("Comparison of
   MAVEN and Mars Express Observations to Global Hybrid Simulation"); `examples/mars_agufm2015_run1.cfg`
   is a shipped configuration whose header reads "Mars 25.01.2015 12:20 (Run1, MAVEN inbound)", i.e. a
   run set up to match a MAVEN observation interval; `pubs.txt` includes Egan et al. (2018),
   *Comparison of Global Martian Plasma Models in the Context of MAVEN Observations*; and the
   developers' model page names MAVEN among the missions whose in situ observations the model is
   applied to. Confidence: high.
   *Resolution note:* two rows match this mission —
   `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/MAVEN` ("Mars Atmosphere and Volatile
   Evolution Mission") and the SMWG row above. Same entity, so the SMWG tie-breaker applies. The
   recorded name preserves the SMWG row's capital final N.

2. **`Mars Express`**
   `https://spase-metadata.org/SMWG/Observatory/MarsExpress`
   *Evidence:* named in the main reference's title alongside MAVEN; `examples/mars_agufm2015_run2.cfg`
   is a shipped configuration headed "Mars 25.01.2015 14:30 (Run2, Mars Express inbound)"; named on
   the developers' model page. Confidence: high.
   *Resolution note:* three rows match — the SMWG row above,
   `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/MarsExpress` ("Mars Express") and
   `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/MEX` ("Mars-Express"). One entity, three
   names; SMWG tie-breaker applies.

3. **`Solar Orbiter`**
   `https://spase-metadata.org/ESA/Observatory/SolarOrbiter`
   *Evidence:* `pubs.txt` lists Stergiopoulou K., Jarvinen R., Andrews D.J. et al. (2023),
   *Solar Orbiter Data-Model Comparison in Venus' Induced Magnetotail*, JGR 128,
   doi:10.1029/2022JA031023 — a peer-reviewed RHybrid data–model comparison against Solar Orbiter
   measurements, curated by the maintainers in the repository itself; also named on the developers'
   model page. Confidence: high.
   *Resolution note:* no SMWG row exists for Solar Orbiter; the ESA row is the correct one (matching
   the field guidance's own worked example). The alternative
   `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SolO` is the same entity under an AMDA
   alias.

4. **`BepiColombo Spacecraft`**
   `https://spase-metadata.org/SMWG/Observatory/BepiColombo`
   *Evidence:* the current development line of the model exists to support this mission. The
   developers' missions page states the ERC Consolidator Grant project MEOW — which funds the team's
   model development (Fields 25 and 26) — will "develop novel methods for particle-based global space
   weather modeling and include detailed electron physics description as well as **apply the model to
   interpret space plasma observations on the BepiColombo mission**", and the model page names
   BepiColombo first among the missions RHybrid is applied to. The repository backs the Mercury
   capability directly: `examples/mercury.cfg` and `examples/mercury_mnras_2020.cfg`, the published
   sodium exosphere profile `neutralDensityMercurySodiumExner20` in `src/neutral_profiles.h`, and two
   `pubs.txt` entries on the Hermean magnetosphere and ion foreshock. Confidence: moderate-high — the
   mission link is stated by the developers rather than written into the repository, while the Mercury
   modelling capability the link depends on is fully evidenced in the repository.
   *Resolution note:* four rows match "BepiColombo". `https://spase-metadata.org/SMWG/Observatory/BepiColombo`
   and `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/BepiColombo` are the same
   mission-level entity, so the SMWG tie-breaker selects the former; its `name` is
   "BepiColombo Spacecraft", copied verbatim rather than shortened. The other two rows —
   `…/CDPP-AMDA/BepiColombo/MPO` ("Mercury Planetary Orbiter") and `…/CDPP-AMDA/BepiColombo/Mio`
   ("Mio") — are *distinct* sub-platform entities, not duplicates of the mission. They are not
   recorded because nothing in the repository or the developers' statements selects between the two
   spacecraft, and the mission-level association is the accurate one. This is not an ambiguity
   blocker: the entity "BepiColombo" resolves cleanly to one preferred row.

**Considered, resolved, and not selected.** Two further missions are named on the developers' model
page in the same sentence as MAVEN, Mars Express and Solar Orbiter, but have no supporting artifact in
the repository and no entry in `pubs.txt`. Their SPASE rows are resolved and recorded here so that
adding either later is a decision rather than new research:

- **Venus Express** — `https://spase-metadata.org/SMWG/Observatory/VenusExpress` (name "Venus
  Express"; the CNES rows `…/CDPP-Archive/VEX` and `…/CDPP-AMDA/VEX` are the same entity, so the SMWG
  tie-breaker would apply). RHybrid's Venus capability is thoroughly evidenced in the repository
  (`examples/venus.cfg`, `examples/venus_grl_2020.cfg`, `examples/venus.txt`,
  `neutralDensityVenusHydrogen`/`…Oxygen`, two `pubs.txt` Venus papers) — but that is evidence for the
  *body*, recorded in Field 5, not for the mission. The only RHybrid Venus data–model comparison in
  `pubs.txt` is against Solar Orbiter, not Venus Express. Note that Venus Express was heavily used
  with FMI's *other* hybrid code, HYB (Field 29), which the developers' page associates with Venus
  Express explicitly — so a careless reading could attach it to the wrong code.
- **Parker Solar Probe** — `https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe` (name
  "Parker Solar Probe"; the two CNES rows are the same entity). Named once on the developers' model
  page and nowhere else. PSP is a solar-wind and inner-heliosphere mission, while RHybrid models
  planetary interactions, so the connection is the least self-evident of the six and has the least
  supporting material.

Both rest on genuine developer statements, and a later refresh could reasonably judge the model page
sufficient on its own. They were left out to keep the selection internally consistent: each of the four
recorded entries has a repository artifact or a `pubs.txt` publication behind it, and these two have
neither.

**Not related, and recorded so it is not mistaken for an omission:** Cassini-Huygens and Rosetta,
which the developers' model page associates with HYB rather than RHybrid; and Juice, which appears on
the missions page as FMI instrument-hardware participation in the PEP package. The Moon appears as an
application on the developers' examples page ("Moon's solar wind interaction … in a global 3D RHybrid
simulation run") and is reflected in Field 5 and the description, but it is a body, not an
observatory, and has no `type = 2` row.

### 33. Logo (OPTIONAL)
**Not found.**

The repository contains no image file of any kind — the complete file listing is `COPYING`, `INSTALL`,
`README`, `pubs.txt`, and the `doc/`, `examples/`, `src/`, `tests/` and `tools/` directories, whose
only non-text contents are two algorithm PDFs and two OpenDocument presentation sources
(`doc/cell_indexing.odp`/`.pdf`, `doc/field_algorithm.odp`/`.pdf`). There is no logo badge in the
README, no `.github` assets directory, and no GitHub Pages site. The developers' project site carries
simulation figures and an FMI institutional identity but no RHybrid mark that would serve as a logo,
and RHybrid is not in any PyHC registry, which is the other common source of curated logo URLs.

---

## Cross-cutting negative research

Recorded once here rather than repeated per field, so a later refresh does not redo it.

**PyHC registries — not a PyHC package.** All three registry files were read in full on 2026-08-10:
`projects_core.yml`, `projects.yml` and `projects_unevaluated.yml`. RHybrid appears in none of them,
under no name, and no entry's `code` field points at `fmihpc`. This is expected and not a deficiency: PyHC curates Python packages,
and RHybrid is a C++/MPI model whose Python content is post-processing tooling. It does mean the
curated PyHC sources of logo, documentation URL and keywords are unavailable for this record, which is
why Fields 24, 33 and 16 rest on repository and developer-site evidence instead.

**SoMEF adds nothing beyond the GitHub API for this repository.** At threshold 0.7 it yields only
what the GitHub API already gives directly: the repository URL, owner `fmihpc`, `date_created`
2016-01-08T11:07:36Z, `date_updated` 2026-07-30T17:08:05Z, the GitHub licence key `GPL-3.0`, the
description "RHybrid Simulation Code", the README text, the language byte counts, and four shell
script paths. It finds no version, no DOI, no authors, no documentation URL and no logo — consistent
with those genuinely not existing rather than with a failed extraction. Two of its outputs are wrong
and should not be trusted if it is re-run here: it classifies the `application_domain` as "Semantic
web", and its `download_url` (`…/rhybrid/releases`) points at an empty releases page. Its header
extraction also errors ("list index out of range") on this README, which is named `README` with no
extension, is not Markdown, and uses bare all-caps section titles instead of Markdown headings.

**The GitHub repository has no topics.** `topics = []`, so the usual repository-topic source of
keywords is empty and Field 16 is derived from the code and publications instead.
