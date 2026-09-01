# HSSI Metadata Extraction Results

**HSSI Software ID:** 7bd65217-fdbe-4945-a657-496a494fff48
**Repository:** https://github.com/spacepy/spacepy
**Source Revision:** cb983af96e06265dc35463e0d725a11eaf0682a6
**Extraction Date:** 2026-08-12
**Validation Date:** 2026-08-22
**Validation Status:** PASS

**Scope note.** Evidence below is drawn from the pinned source revision (authored 2026-03-15, the
newest commit on the repository's default branch), from the two reference publications, and from
external authorities (Zenodo, ORCID, ROR). SpacePy's most recent public release remains **0.7.0**
(2024-11-08); `pyproject.toml` at this revision declares `version = "0.8.0a0"`, which is an
in-development marker and not a released version. Three questions were settled earlier and remain
settled: how the license is represented (Field 15), the author-name form for Brian Larsen (Field 6),
and the exclusion of generic dependencies from Interoperable Software (Field 30). The reasoning for
each is recorded in its own field.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.3252523

Zenodo **concept** DOI, which always resolves to the newest release. It is the identifier the
README badge and `CITATION.cff` both point at, and Zenodo's record for the 0.7.0 release
(10.5281/zenodo.14057789) names it as its `conceptdoi`. The version-specific DOI is deliberately
kept in Field 12 rather than here, so that this field does not go stale on each release.

### 3. Code Repository (MANDATORY)
https://github.com/spacepy/spacepy

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms: Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Field-line Tracing
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Pitch Angle Distributions
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Spectrogram
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Line Plots
- Data Visualization: Orbit Plots
- Data Visualization: Spectrogram
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing
- Models and Simulations: ML/AI

Every subcategory above is accompanied by its required parent category (Coordinate Transforms,
Data Processing and Analysis, Data Visualization, Models and Simulations). SpacePy claims no
subcategory under Mission-related or Servers and Environments, and neither parent is claimed.

**Evidence for each claim.**

- *Coordinate Transforms / Magnetospheric* — `spacepy.coordinates` and `spacepy.ctrans` convert among
  GDZ, GEO, GSM, GSE, SM, GEI, CDMAG/MAG, SPH, RLL, TOD/ECITOD, J2000/ECI2000, TEME and ECIMOD
  (`SYSAXES_TYPES` in `spacepy/coordinates.py`), plus generalized transforms via quaternions.
- *Data Processing and Analysis* — file I/O (`spacepy.pycdf` for NASA CDF, `spacepy.datamodel` for
  HDF5, netCDF3 and JSON-headed ASCII); OMNI/Qin-Denton retrieval (`spacepy.omni.get_omni`);
  superposed epoch analysis (`spacepy.seapy`); bootstrap confidence intervals and association
  analysis (`spacepy.poppy`); AE9/AP9 output handling (`spacepy.ae9ap9`); SWMF/BATS-R-US/RAM-SCB
  output processing and derived-quantity calculation (`spacepy.pybats.bats` `calc_temp`, `calc_b`,
  `calc_j`, `calc_E`, `calc_ndens`, `calc_beta`, `calc_jxb`, `calc_alfven`, `calc_vort`,
  `calc_gradP`); IRBEM-based field-line tracing and L* (`spacepy.irbempy`); binning/rebinning and
  resampling (`spacepy.datamanager.rebin`, `spacepy.datamodel.resample`); generic spectrogram
  binning (`spacepy.plot.spectrogram`); pitch-angle distribution conversion
  (`spacepy.empiricals.vampolaPA`, `getVampolaOrder`, `omniFromDirectionalFlux`); energy/fluence
  spectra (`spacepy.empiricals.getSolarProtonSpectra`, `spacepy.ae9ap9.plotSpectrogram`).
- *Data Visualization* — `spacepy.plot` supplies publication-quality 2D graphics, line plots,
  spectrogram display, `levelPlot`, and smart time-tick helpers; `spacepy.pybats` plots 2D cut
  planes and spherical shells through a 3D simulation domain (`Bats2d`, `ShellSlice.add_cont_shell`);
  orbit and trajectory plots come from `spacepy.ae9ap9.Ae9Data.plotOrbit` and pybats'
  `add_orbit_plot` in the `bats` and `ram` submodules.
- *Models and Simulations: Empirical* — `spacepy.empiricals` implements plasmapause location,
  the Shue magnetopause, Lmax, Dst*, and expected solar wind temperature; `spacepy.igrf` implements
  IGRF (coefficients shipped as `spacepy/data/igrf14coeffs.txt`).
- *Models and Simulations: Field-line Tracing* — IRBEM-backed tracing through the Tsyganenko
  external field models (`find_footpoint`, `find_magequator`, `get_Lstar`, `find_LCDS`), and
  streamline tracing through model fields (`spacepy.pybats.trace2d`, `bats.Stream`).
- *Models and Simulations: ML/AI* — `spacepy.LANLstar` provides artificial-neural-network models
  for L* (`LANLstar`) and Lmax (`LANLmax`), with the trained networks shipped in
  `spacepy/data/LANLstar/`.
- *Models and Simulations: Data Guided* — SpacePy's model entry points retrieve observational
  driver data automatically rather than requiring the user to supply it. `spacepy.empiricals`
  functions take a `Ticktock` plus a `dbase`/`omnivals` argument and call `spacepy.omni.get_omni`
  to obtain the Qin-Denton/OMNI solar-wind and geomagnetic-index values that drive the model
  (`getLmax`, `getPlasmaPause`, `getMagnetopause`, `getMPstandoff`, `getDststar`). The same pattern
  drives the Tsyganenko external fields used by `spacepy.irbempy` — `get_Bfield`, `find_Bmirror`,
  `find_magequator` and `find_LCDS` all accept `omnivals` and fall back to `spacepy.omni.get_omni`
  when it is not supplied. This is a model driven by observational data, which is what the
  subcategory denotes.

**Considered and not selected.**

- *Data Processing and Analysis: Data Assimilation* — the `data_assimilation`, `radbelt` and
  `spacepy_EnKF` modules were moved to the sandbox in the 0.7.0 release (release notes: "These
  modules were undertested and minimally documented. They may be restored in the future with
  appropriate testing and docs."). `spacepy/sandbox/` is not listed in `pyproject.toml`'s
  `[tool.setuptools] packages`, so the sandbox is not installed with the package and the capability
  is not available to a user of a release. If a future release restores those modules to the
  installed package, this subcategory should be revisited.
- *Data Processing and Analysis: ML/AI* — the only machine-learning component is LANLstar's neural
  network, which produces a model result (L*/Lmax) rather than analysing data, so it is classified
  under Models and Simulations: ML/AI. No ML is applied to observational data analysis.
- *Data Processing and Analysis: 2D Slices* — SpacePy does not cut 2D planes out of 3D volumes; it
  reads output that the simulation has already written as a 2D cut plane (`Bats2d`) or a spherical
  shell (`ShellSlice`). The `Extraction` class states it "only works with
  `spacepy.pybats.bats.Bats2d` objects", so extraction is along lines within an existing 2D plane.
  The visualization counterpart (Data Visualization: 2D Slices) is claimed, because those planes
  and shells are slices through a 3D simulation domain and SpacePy renders them.
- *Data Processing and Analysis: Wavelet Analysis* — no wavelet transform, scalogram or wavelet
  coherence code was found in the shipped package or in `Doc/source` at this revision.
- *Data Visualization: 3D Graphics* — no use of `mplot3d`, `Axes3D`, `projection='3d'`,
  `plot_surface`, VTK, Mayavi or PyVista was found in the shipped package or docs. The SciPy 2010
  paper described `Bats3d` objects as "being developed"; they are still not present.
- *Data Visualization: Movies* — no `matplotlib.animation`, `FuncAnimation`, `ArtistAnimation` or
  frame/movie export was found in the shipped package or docs.
- *Data Visualization: Web-Based* — `spacepy.pybats.interact.ClickTracer` is a Matplotlib mouse
  event handler for adding streamlines to an existing axes, not a browser-based visualization.
- *Coordinate Transforms: Ionospheric* — SpacePy implements no AACGM, apex, or magnetic-local-time
  coordinate conversion. `spacepy.coordinates` offers CDMAG/MAG (centered geomagnetic dipole), which
  belongs to the Magnetospheric subcategory, and GDZ (geodetic). Occurrences of "MLT" in the
  codebase are axis labels and column names in pybats readers for DGCPM, RAM and BATS-R-US model
  output, not coordinate conversions. Note that `Doc/source/capabilities.rst` describes
  `spacepy.coordinates` as covering "Earth magnetospheric and ionospheric physics" — that phrasing
  refers to the physics domains served, not to an ionospheric coordinate transform, and is not by
  itself grounds to claim this subcategory.
- *Coordinate Transforms: Heliospheric / Solar* — `spacepy.empiricals.getSolarRotation` and
  `spacepy.plot.carrington.solarRotationPlot` compute and plot by Carrington or Bartels rotation
  **number**. A rotation number is a time index, not a coordinate frame, and SpacePy converts to no
  heliographic or heliocentric system.
- *Data Processing and Analysis: Curlometer* and *Linear Gradient Estimation* — `bats.calc_j` and
  `bats.calc_gradP` compute a curl and a gradient by finite differences on a simulation grid. Both
  subcategories denote multi-spacecraft in-situ estimation from a small number of measurement
  points, which SpacePy does not perform.
- *Data Processing and Analysis: Plasma Moments* — `bats.calc_temp` and `bats.calc_ndens` convert
  MHD state variables (pressure, mass density) into temperature and number density using an
  equation of state. They do not integrate a velocity distribution function, which is what this
  subcategory denotes. SpacePy contains no distribution-function moment integration.
- *Models and Simulations: Forecasting* — `spacepy.realtime` retrieves an externally produced
  forecast over HTTP; it does not generate one. That is data retrieval, already claimed.
- *Models and Simulations: Theory* — `spacepy.pybats.dipole` supplies a closed-form dipole field
  (`b_mag`, `b_hat`, `b_line`), but it is a small plotting aid hard-coded to Earth's dipole moment
  (30400 nT) rather than an analytical modelling capability offered to users.
- *Models and Simulations: MHD* and *Physics-Based* / *First Principles* — SpacePy runs no MHD or
  first-principles simulation. `spacepy.pybats` reads, analyses and visualizes output produced by
  external codes (BATS-R-US, RAM-SCB, RIM, GITM, PWOM, DGCPM); the simulation itself is SWMF's.
  This is recorded instead as interoperability with SWMF in Field 30.

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Earth Inner Magnetosphere
- Earth Outer Magnetosphere
- Earth Auroral Subregion
- Earth Ionosphere
- Earth Thermosphere
- Earth Atmosphere
- Interplanetary Space
- Solar Wind
- Planetary Magnetospheres

**Evidence, region by region.** An earlier version of this field carried only the four coarse terms
(Earth Magnetosphere, Earth Atmosphere, Interplanetary Space, Planetary Magnetospheres) while its own
prose already asserted ionosphere, thermosphere and solar-wind coverage. That inconsistency was
resolved in favour of the code: each finer region below is claimed because a named module supports
it.

- **Earth Magnetosphere** — the package's central domain: coordinate systems, radiation belts,
  ring current, magnetopause, and geomagnetic field models.
- **Earth Inner Magnetosphere** — radiation-belt drift shells and L* (`spacepy.irbempy.get_Lstar`,
  `find_LCDS`), the AE9/AP9 empirical radiation-belt environment (`spacepy.ae9ap9`), the LANLstar
  neural-network L* model, ring current via RAM-SCB output (`spacepy.pybats.ram`), plasmasphere via
  DGCPM output (`spacepy.pybats.dgcpm`), and the plasmapause model
  (`spacepy.empiricals.getPlasmaPause`).
- **Earth Outer Magnetosphere** — the Shue magnetopause model (`spacepy.empiricals.getMagnetopause`,
  `getMPstandoff`), the last closed drift shell (`spacepy.irbempy.find_LCDS`), and the last closed
  field line at Earth in global MHD output
  (`spacepy.pybats.bats.Bats2d.find_earth_lastclosed`).
- **Earth Auroral Subregion** — the Ridley Ionosphere Model reader exposes RIM's auroral-oval
  calculation (`spacepy.pybats.rim.OvalDebugFile`, `add_oval_line`, which interpolates and plots the
  oval location), and `spacepy.pybats.kyoto` retrieves the AE/AL/AU auroral electrojet indices.
- **Earth Ionosphere** — `spacepy.pybats.rim` (Ridley Ionosphere Model and Ridley Serial output),
  `spacepy.pybats.gitm` (Global Ionosphere-Thermosphere Model), `spacepy.pybats.pwom` (Polar Wind
  Outflow Model — ionospheric outflow), and `spacepy.pybats.dgcpm`. The PyHC registry entry for
  SpacePy carries the keyword `ionosphere_thermosphere_mesosphere`.
- **Earth Thermosphere** — `spacepy.pybats.gitm` handles input/output for the Global
  Ionosphere-**Thermosphere** Model, the SWMF's Upper Atmosphere module.
- **Earth Atmosphere** — retained as the broader upper-atmosphere term covering the same GITM/PWOM
  capability; the SciPy 2010 paper frames SpacePy's scope as "atmospheres and above" including
  "the deposition of energy into the upper atmosphere".
- **Interplanetary Space** — OMNI near-Earth interplanetary data are propagated from upstream
  monitors; the PyHC registry entry carries the keyword `heliosphere`.
- **Solar Wind** — `spacepy.omni.get_omni` retrieves the OMNI and Qin-Denton near-Earth solar wind
  parameters; `spacepy.empiricals.getExpectedSWTemp` models solar-wind temperature; the Shue
  magnetopause is driven by solar-wind dynamic pressure and IMF Bz; and
  `spacepy.pybats.ImfInput` reads and writes SWMF's upstream solar-wind input files.
- **Planetary Magnetospheres** — retained. The supporting capability is generic rather than
  body-specific: `spacepy.pybats.dipole` is documented in units of "planetary radius" and pybats
  plotting places a "planetary body" in the figure, so pybats can handle a BATS-R-US run configured
  for another body. There is no per-planet model, coordinate frame, or data reader in the package,
  so this value is the weakest in the list; it is kept because it is a supported, if general,
  capability and no evidence contradicts it.

**Considered and not selected.**

- *Earth Magnetotail* — the TS07D coefficient files shipped in `spacepy/data/TS07D/TAIL_PAR/` are
  inputs to the Tsyganenko-Sitnov external field model as a whole, not a tail-specific analysis
  capability, and the package has no magnetotail-specific module or diagnostic.
- *Earth Magnetosheath* — the only sheath-adjacent reference is `Doc/source/omni.rst` explaining
  that OMNI data are "propagated to Earth's bow shock nose", which describes the provenance of an
  input dataset rather than a magnetosheath capability.
- *Corona, Chromosphere, Photosphere, Solar Interior, Solar Environment, Heliosheath, and the
  per-planet magnetosphere terms (Jupiter, Saturn, Mars, Uranus, Neptune)* — no supporting code.
  `getSolarProtonSpectra` models the fluence spectrum of a solar particle event at 1 AU, not the
  solar atmosphere where such events originate.

### 6. Authors (MANDATORY)

- **Author:** Steven K. Morley
  - **Author Identifier:** https://orcid.org/0000-0001-8520-0199
  - **Affiliation:** Los Alamos National Laboratory
    - Affiliation Identifier: https://ror.org/01e41cf67

- **Author:** Jonathan T. Niehof
  - **Author Identifier:** https://orcid.org/0000-0001-6286-5809
  - **Affiliation:** University of New Hampshire
    - Affiliation Identifier: https://ror.org/01rmh9n78

- **Author:** Daniel T. Welling
  - **Author Identifier:** https://orcid.org/0000-0002-0590-1022
  - **Affiliation:** University of Michigan
    - Affiliation Identifier: https://ror.org/00jmfr291

- **Author:** Brian Larsen
  - **Author Identifier:** https://orcid.org/0000-0003-4515-0208
  - **Affiliation:** Los Alamos National Laboratory
    - Affiliation Identifier: https://ror.org/01e41cf67

- **Author:** Antoine Brunet
  - **Author Identifier:** https://orcid.org/0000-0003-2666-3227
  - **Affiliation:** Office National d'Études et de Recherches Aérospatiales
    - Affiliation Identifier: https://ror.org/005y2ap84

- **Author:** Miles A. Engel
  - **Author Identifier:** https://orcid.org/0000-0003-4248-9636
  - **Affiliation:** Los Alamos National Laboratory
    - Affiliation Identifier: https://ror.org/01e41cf67

- **Author:** Jan Gieseler
  - **Author Identifier:** https://orcid.org/0000-0003-1848-7067
  - **Affiliation:** University of Turku
    - Affiliation Identifier: https://ror.org/05vghhr25

- **Author:** John Haiducek
  - **Author Identifier:** https://orcid.org/0000-0002-4027-8475
  - **Affiliation:** Not found

- **Author:** Michael Henderson
  - **Author Identifier:** https://orcid.org/0000-0003-4975-9029
  - **Affiliation:** Los Alamos National Laboratory
    - Affiliation Identifier: https://ror.org/01e41cf67

- **Author:** Aaron Hendry
  - **Author Identifier:** https://orcid.org/0000-0002-9130-3781
  - **Affiliation:** British Antarctic Survey
    - Affiliation Identifier: https://ror.org/01rhff309

- **Author:** Michael Hirsch
  - **Author Identifier:** https://orcid.org/0000-0002-1637-6526
  - **Affiliation:** Boston University
    - Affiliation Identifier: https://ror.org/05qwgg493
  - **Affiliation:** Scivision, Inc.
    - Affiliation Identifier: Not found

- **Author:** Peter Killick
  - **Author Identifier:** Not found
  - **Affiliation:** Met Office
    - Affiliation Identifier: https://ror.org/01ch2yn61

- **Author:** Josef Koller
  - **Author Identifier:** Not found
  - **Affiliation:** Los Alamos National Laboratory
    - Affiliation Identifier: https://ror.org/01e41cf67

- **Author:** Asher Merrill
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

- **Author:** Lutz Rastaetter
  - **Author Identifier:** https://orcid.org/0000-0002-7343-4147
  - **Affiliation:** Community Coordinated Modeling Center
    - Affiliation Identifier: https://ror.org/01dy3j343
  - **Affiliation:** National Aeronautics and Space Administration
    - Affiliation Identifier: https://ror.org/027ka1x80

- **Author:** Ashton Reimer
  - **Author Identifier:** https://orcid.org/0000-0002-4621-3453
  - **Affiliation:** SRI International
    - Affiliation Identifier: https://ror.org/05s570m15

- **Author:** Albert Y. Shih
  - **Author Identifier:** https://orcid.org/0000-0001-6874-2594
  - **Affiliation:** Goddard Space Flight Center
    - Affiliation Identifier: https://ror.org/0171mag52

- **Author:** Amanda Stricklan
  - **Author Identifier:** https://orcid.org/0000-0001-7751-8885
  - **Affiliation:** Los Alamos National Laboratory
    - Affiliation Identifier: https://ror.org/01e41cf67

**Composition.** Eighteen authors, matching `CITATION.cff`, Zenodo's 18 creators for the 0.7.0
release, and the citation block in `Doc/source/index.rst`. No author in those authoritative lists
has been dropped.

**Name preservation (settled).** The middle-initial form **Brian A. Larsen** appears in Zenodo's
creator list and in two places in the repository — `CITATION.cff:25-26` and the "To cite the code
itself" BibTeX block at `Doc/source/index.rst:47` — while the stored HSSI record is **Brian Larsen**.
The stored form was deliberately preserved, so **Brian Larsen** stands. That is not merely a
preference for the stored value: the no-initial form is also what SpacePy's own package metadata and
module headers use, including `pyproject.toml`'s `maintainers`, `setup.py`, `spacepy.__team__` in
`spacepy/__init__.py`, and the author lines of `spacepy/time.py`, `spacepy/datamodel.py`,
`spacepy/ae9ap9.py`, `spacepy/plot/__init__.py` and `spacepy/toolbox/__init__.py`. Both are correct
renderings of the same name, so this is a formatting choice rather than an error to fix. It is
settled and should not be re-raised. The
one author name that *was* changed away from its stored HSSI value is Lutz Rastaetter; the reasoning
for treating that case differently is recorded with his entry below.

**Affiliations and identifiers established from primary sources, with their evidence.**

- **Michael Hirsch — Boston University and Scivision, Inc.** His commit in this repository is authored under the
  GitHub account `scivision`, which independently corroborates the association. Scivision, Inc. has
  no ROR identifier, and a ROR search does not produce a confident match for a small company
  of that name, so the identifier is left empty rather than guessed.
- **Josef Koller — Los Alamos National Laboratory.** The SciPy 2010 proceedings paper marks all six
  authors, Koller among them, with "‡ Los Alamos National Laboratory"; he has commits in this
  repository authored as `jkoller@lanl.gov`, alongside a larger set of early commits under a bare
  `jkoller` identity carrying no address; and `spacepy/realtime.py` names him as its sole author and
  carries "Institution: Los Alamos National Laboratory" with contact `jkoller@lanl.gov` (lines 6-10).
  Note for any later check: `spacepy/LANLstar.py` also lists him among its authors, but it carries no
  `Institution:` line at all and its contact line is `smorley@lanl.gov, yiqunyu17@gmail.com`, so it
  is not evidence of his affiliation and should not be cited as such.
- **Michael Henderson — Los Alamos National Laboratory.** Same SciPy 2010 affiliation marker
  (as Michael G. Henderson), and a commit authored as `mghenderson@lanl.gov`.
- **Antoine Brunet — ORCID `0000-0003-2666-3227` and ONERA.** His commits in this repository are
  authored as `antoine.brunet@onera.fr`, and the 0.2.3 release notes credit "Thanks Antoine
  Brunet" for the `pycdf.Var.pad` work. That ORCID record is Antoine Brunet, Research Fellow in
  ONERA's DPHY department, with a publication record in Earth radiation-belt modelling — the same
  laboratory that develops IRBEM, which SpacePy bundles and wraps. The organization is recorded at
  the parent-institution level (ONERA, ROR `005y2ap84`) rather than the DPHY department
  (ROR `00nf91p74`), because the parent is the recognizable and reusable entity. The name is written
  in expanded form per the guidance to avoid acronyms.
- **Peter Killick — Met Office.** His commits are authored as `peter.killick@metoffice.gov.uk`.
  This rests on the work-email domain alone, which is direct evidence of employment but a single
  source; no ORCID could be matched to him.
- **Aaron Hendry — ORCID `0000-0002-9130-3781` and British Antarctic Survey.** `spacepy/LANLstar.py`
  credits "Aaron Hendry" in its author line, and the 0.4.0 release notes record that
  `spacepy.LANLstar` "now uses a numpy-based implementation (based on contributions from Aaron
  Hendry)". He has a commit in this repository under the personal address `aaron@hendry.co.nz`. That
  ORCID is Aaron Hendry, Space Weather Scientist in the Space Weather and Atmosphere group at the
  British Antarctic Survey in Cambridge, GB, with a publication record in radiation-belt dynamics and
  EMIC-wave-driven electron precipitation — the subject matter of his LANLstar contribution. The
  employment entry disambiguates itself with ROR `https://ror.org/01rhff309`, so name, department,
  city, country and identifier all agree. The affiliation is a current one; SpacePy's own sources supply none, so no
  contribution-era alternative was available to weigh against it.
- **Lutz Rastaetter — ORCID `0000-0002-7343-4147`, Community Coordinated Modeling Center and
  National Aeronautics and Space Administration.** He has two commits in this repository, both on the
  code the 0.5.0 release notes credit to him: "Added sort_unstructured_data keyword" (2022-03-09,
  `lutz.rastaetter@nasa.gov`) and "Added test for IdlFile ascii and binary reader" (2022-03-16,
  `lutz.rastaetter@gmial.com` — a mistyped `gmail` domain). Those release notes read
  "`~.pybats.IdlFile` no longer sorts unstructured data from binary files… Thanks Lutz Rastaetter",
  which is that same change. His ORCID employment record gives NASA Goddard Space Flight Center,
  department "Space Weather Laboratory, Code 674", role Aerospace Technologist / Fields and
  Particles, Greenbelt, MD, US, from 2010-08-30 and current.

  **Spelling — settled, and a deliberate exception.** The name is recorded as **Rastaetter**, not the
  "Rastatter" that HSSI previously stored. Four sources support "Rastaetter": the registered name on
  his ORCID record (which carries "Lutz Rastatter" only as an other-name); the author name on each of
  his two commits here, one as `Lutz Rastaetter` from a `@nasa.gov` address and one as `RASTAETTER`;
  and the spelling SpacePy's own documentation uses at `Doc/source/release_notes.rst:254`.

  The repository spells it "Rastatter" in **two** places, and a future refresh will meet both:
  `CITATION.cff:55` (`family-names: Rastatter`) and `Doc/source/index.rst:53`
  (`Rastatter, Lutz and Reimer, Ashton and`), the latter inside the 18-name author list at
  `Doc/source/index.rst:46-54`, part of the "To cite the code itself" BibTeX block beginning at line
  44. Neither should be used to re-propose the "Rastatter" spelling. They are not two independent
  confirmations: that BibTeX author list carries the same eighteen family names in the same order as
  `CITATION.cff`'s own author block, so it is the one list restated in another format. This is a deliberate departure from
  the precedent set for **Brian Larsen**, where the stored HSSI name was preserved: that case is a
  formatting preference between two correct renderings of a name, whereas this one is a
  source-supported spelling correction.

  **Why the affiliations are CCMC and NASA rather than Goddard.** The canonical ORCID identity
  carries established Community Coordinated Modeling Center and NASA affiliations, which are
  retained here. No SpacePy source document independently connects him to CCMC. The string "CCMC"
  does occur in the repository — at
  `tests/test_igrf.py:82-85`, where an IGRF unit test is validated against the CCMC Vitmo ModelWeb
  calculator — but that is an external validation reference, not an authorship or affiliation
  statement, so a reviewer who greps for "CCMC" and finds it has not found a defect. **Goddard Space Flight Center (`https://ror.org/0171mag52`) was
  considered and rejected**, even though his ORCID employment names it, for two reasons that both
  point the same way. Descriptively it would be redundant: ROR records the Community Coordinated
  Modeling Center as a child of Goddard Space Flight Center, so the CCMC affiliation already places
  him there. Recording Goddard separately would therefore duplicate the same institutional context
  rather than add a distinct affiliation.
- **Amanda Stricklan — ORCID `0000-0001-7751-8885` and Los Alamos National Laboratory.** This is the
  best-evidenced of these, because it is self-asserted: her public ORCID record lists "SpacePy"
  under DOI `10.5281/zenodo.3252523` — the exact concept DOI in Field 2 — together with
  "spacepy/spacepy: 0.3.0" (`10.5281/zenodo.6499545`), and her employment history includes LANL
  ISR-1 (Space Science and Applications), the group that produces SpacePy.

**Contributors considered for the author list and deliberately not added.** The author list is the
identity-aware union of the three authoritative sources — the stored HSSI author set,
`CITATION.cff`, and Zenodo's creators for the release. Commit history alone does not add an author,
because the project curates its own credit list. The contributors below are recorded so a later
refresh does not re-derive the question from the commit log. Together with the eighteen credited
authors, they account for every distinct **commit-author** identity in the repository's history at
this revision; the remaining identities all resolve to credited authors committing under more than
one name or address.

- **Yiqun Yu — not added.** She has seven commits in this repository (five as `yiqun@lanl.gov`, two
  as `yiqun@dipole.lanl.gov`); `spacepy/LANLstar.py` credits "Yiqun Yu" in its author line and
  carries `yiqunyu17@gmail.com` in its contact line; she is a co-author of the 2012 AGU abstract
  "Space Science with the SpacePy Toolkit" listed in `Doc/source/publications.rst`; and she is the
  second author of Jordanova et al. (2014), also listed there. The decisive reason not to add her is
  that she appears in none of the three authoritative author lists, so the union does not reach her.
  This is what distinguishes her from Aaron Hendry, whose contribution is comparable in kind but who
  **is** named in `CITATION.cff`.
- **James Westbrook — not added.** The address `jamesmw732@gmail.com` authored 115 commits in 2024
  (78 of them under the name string "James Westbrook", 37 under "James"), a volume exceeded only by
  the four core maintainers — Niehof, Morley, Larsen and Welling. He is nonetheless named in none of
  the three authoritative author lists, and unlike Hendry and Brunet he receives no "Thanks" credit
  line in `Doc/source/release_notes.rst`; the address is personal rather than institutional, so no
  affiliation could be derived either.
- **Jonathan George — not added.** `jongeorge1999@gmail.com` authored 35 commits between 2024-06-12
  and 2024-09-08 (32 under the handle `jongeorge1999`, 3 under "Jonathan George"), mostly
  documentation cleanup and docstring work. Same disposition and same reasons as Westbrook: absent
  from all three authoritative author lists, no "Thanks" credit line, and a personal address that
  yields no affiliation.
- **Minor contributors — not added, listed so the next refresh need not re-derive them.** Each of
  these authored one or two commits, appears in none of the three authoritative author lists, and is
  named nowhere in `CITATION.cff`, `Doc/source/release_notes.rst`, `Doc/source/index.rst` or
  `Doc/source/publications.rst`: **Qusai Al Shidi** (`me@qalshidi.science`, one commit
  `455629088076fe65dee41618f1e55110cbae10c0`, 2025-08-22, "Fix `make install` line for cdf");
  **Macdara Ó Murchú** (`m4cd4r4@gmail.com`, two commits in March 2026 fixing a
  `parse_filename_time` crash — one of which is the pinned source revision of this dossier);
  **Jaap Vermeulen** (`jaap@lanl.gov`, two build-system commits in 2017); **Scott E Lasley**
  (`slasley@umd.edu`, one 2016 commit removing a non-ASCII character that broke f2py); and
  **u117089** (an opaque identity with no email address, one 2011 commit whose message is signed
  "[SKM]", indicating Steve Morley applied it on their behalf).

  Note that the GitHub handle `spacecataz` (`dantwelling@gmail.com`) is **not** an uncredited
  contributor — it is one of Daniel T. Welling's several commit identities, and he is already a
  credited author.

**Credited in module docstrings, but not commit authors.** Sweeping every `Authors:` and
`Additional Contributors:` line in the package and its documentation turns up three people who have
no commit at all — under any name or address, on any ref — and who are not credited authors of
SpacePy. They are named here with their citations so a reader who greps those docstrings and finds
one does not read it as a gap in the author list:

- **Charles Kiyanda** — `spacepy/datamodel.py:10`, "Additional Contributors: Charles Kiyanda and
  Miles Engel", mirrored at `Doc/source/datamodel.rst:24`.
- **Lorna Ellis** — `spacepy/pycdf/istp.py:13`, "Additional Contributors: Lorna Ellis, Asher
  Merrill".
- **Humberto Godinez** — `spacepy/sandbox/data_assimilation.py:6`, "Authors: Josef Koller, Humberto
  Godinez". This is one of the sandbox modules that 0.7.0 stopped shipping, for the reason Field 4
  gives when it rejects `Data Processing and Analysis: Data Assimilation`, so the credit is to a
  module that is no longer installed with the package.

None of the three is named in `CITATION.cff`, `Doc/source/index.rst`, Zenodo's creator list, or the
stored HSSI author list, so the identity-aware union does not reach them, and a docstring credit
alone does not add an author. The names credited alongside them — Miles Engel, Asher Merrill and
Josef Koller — are already credited authors. A comparable non-commit credit sits at
`developer/scripts/net2txt.py:2`, which attributes a gist to Aaron Hendry; he is himself a credited
author, so it raises no question.

**Author details researched and deliberately left unresolved.**

- **John Haiducek — affiliation genuinely ambiguous, left empty on purpose.** His commits are
  authored as `jhaiduce@umich.edu` and his ORCID record shows University of Michigan from 2013-09 to
  2018-08, which is the contribution-era affiliation, then United States Naval Research Laboratory
  from 2018-11 to the present. Both organizations already exist in HSSI
  (`https://ror.org/00jmfr291` and `https://ror.org/04d23a975`). Because HSSI does not distinguish
  contribution-time from current affiliation, and `CITATION.cff` and Zenodo supply neither, the field
  is empty by decision rather than for want of research. Both readings are recorded above so that the
  question does not have to be reopened from scratch; neither should be adopted silently on the
  strength of the commit address or the ORCID record alone.
- **Josef Koller — ORCID `0000-0002-6770-4980` rejected.** An ORCID record exists under that exact
  name, but it lists no employment and no works, so there is nothing to tie it to this person.
  His affiliation was established independently (above) and does not depend on it.
- **Asher Merrill — no affiliation available.** His commits use a personal address
  (`asher.s.merrill@gmail.com`) and no other source in the repository, `CITATION.cff` or Zenodo
  supplies an institution.

### 7. Software Name (MANDATORY)
SpacePy

### 8. Description (MANDATORY)
SpacePy is a Python package for the space sciences that makes data analysis, modeling, and visualization easier. It supports obtaining OMNI and Qin-Denton data; reading and writing NASA CDF, HDF5, and JSON-headed ASCII; publication-quality plotting; superposed epoch, association, and bootstrap analyses; empirical plasmapause, magnetopause, Lmax, and radiation-belt models; coordinate and time conversion; IRBEM magnetic-field tracing and L-star calculations; IGRF; the LANLstar neural-network model; AE9/AP9 output; and PyBats analysis and visualization of SWMF, BATS-R-US, RAM-SCB, and GITM output.

This wording is an accurate summary of the package at 0.7.0 and at the pinned revision; each
capability it names is served by a module that ships in the release. One phrase deserves a note, so
it is not later read as a claim about a module that no longer ships: "radiation-belt models" is
served by `spacepy.ae9ap9` — which `Doc/source/capabilities.rst` describes as supporting "the AE9/AP9
empirical radiation belt model" — together with the LANLstar neural-network L* model, both named
separately in the same sentence. It does **not** refer to the former `spacepy.radbelt` module, which
0.7.0 moved to the sandbox and which is therefore no longer installed (see Field 4, where
`Data Processing and Analysis: Data Assimilation` is rejected for the same reason).

### 9. Concise Description (OPTIONAL)
Python tools for space-science data analysis, coordinate and time conversion, empirical modeling, scientific file I/O, and publication-quality visualization.

### 10. Publication Date (RECOMMENDED)
2010-05-20

Date of the first commit in the public repository ("Initial revision"), confirmed from the git
history at this revision. Alternatives considered and not used: the first Zenodo release with the
concept DOI, 2019-06-19, which post-dates public availability by nine years; the first scholarly
publication (SciPy 2010 Proceedings, published 2011); and GitHub's repository-creation date of
2012-10-28, which reflects the migration to GitHub rather than the software's public availability.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

### 12. Version (RECOMMENDED)
- **Version Number:** 0.7.0
- **Version Date:** 2024-11-08
- **Version PID:** https://doi.org/10.5281/zenodo.14057789
- **Version Description:**

```
Please see the full release notes at https://spacepy.github.io/release_notes.html

Binary wheels are now provided for Linux on 64-bit ARM, intended for Raspberry Pi.

There are no changes to dependencies, minimum versions, or installation process with this release.

## New Features
`help` now supports searching the documentation.

## Dependency requirements
Numpy 2.0 is now fully supported. 

Numpy and f2py are no longer required to build SpacePy.  Binary wheels are no longer tied to numpy or Python version.

Sphinx 4.0 is now required to build the documentation; this is not a concern for most users.

Support for Python 3.6 has been removed due to inability to test. Python 3.7 is the oldest supported Python; as a result, Astropy 2.0 is the oldest supported Astropy (if using Astropy).

## Deprecations and removals
`toolbox.timeout_check_call` is deprecated as redundant to using `subprocess.check_call` with the `timeout` argument.

The `irbempy.irbempylib` module has been removed. This was the old internal interface to the IRBEM library and was not intended for public use.

The `data_assimilation`, `radbelt`, and `spacepy_EnKF` modules have been moved to the "sandbox". These modules were undertested and minimally documented.

## Major bugfixes
`irbempy.find_Bmirror` now correctly returns one `Bmirr` per input pitch angle instead of ignoring all but the first.

## Other changes
Operations on `dmarray` which return a scalar value will now return a numpy array scalar rather than the base Python type. This is consistent with the behavior of `numpy.ndarray`. `dmarray` also supports assigning to its `dtype` and `shape`. Together these changes should make `dmarray` a much closer drop-in replacement for `numpy.ndarray`.

Warnings issued by SpacePy are now associated with the line of the calling code, not with the SpacePy code itself.
```

The description above is the full 0.7.0 release-notes text. An earlier version of this file carried a
condensed paraphrase instead, which dropped the deprecations, the bugfix and the `dmarray` changes;
the full text supersedes it and should be preserved intact rather than re-summarised.

**Version number form.** The number is `0.7.0`. The catalogue display `SpacePy - 0.7.0` prefixes
the software name for presentation; the canonical version value remains the bare number.

0.7.0 is the newest GitHub release (published 2024-11-08), the newest git tag (`release-0.7.0`), and
the newest PyPI version. `pyproject.toml` declares `0.8.0a0`, an in-development marker, not a
release.

### 13. Programming Language (RECOMMENDED)
- C
- Fortran77
- Fortran90
- Python 3.x

Python is the primary language. C sources live in `spacepy/libspacepy`. The bundled, modified
IRBEMlib (`spacepy/irbempy/irbem-lib-20241214-8279aa9`) is predominantly fixed-format Fortran 77 but
uses Fortran 90 features such as `!`-prefixed line comments, so both dialects are listed. The
project classifiers list "Programming Language :: C" and "Programming Language :: Fortran"; SoMEF's
language detection likewise reports Python, C and Fortran. The later Fortran standards available in
the controlled list (Fortran 2003, 2008, 2023) are not claimed — no evidence of those language
levels was found in the bundled sources.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.3389/fspas.2022.1023612

Niehof, J. T., Morley, S. K., Welling, D. T., & Larsen, B. A. (2022). The SpacePy space science
package at 12 years. *Frontiers in Astronomy and Space Sciences*, 9. This is the preferred package
reference in both the README's BibTeX block and `CITATION.cff`, which scopes it as the reference for
"package scope and specific details of datamodel and coordinates". The older SciPy 2010 paper is
recorded in Field 27 rather than here, because `CITATION.cff` scopes it to "the package and its
history" and the 2022 article is the current description.

### 15. License (RECOMMENDED)
- **Repository License:** Python Software Foundation License 2.0
- **License URI:** https://spdx.org/licenses/PSF-2.0.html

**HSSI leaves this field empty, deliberately.** `LICENSE.md` is a license modeled on the Python
Software Foundation License, granted by Triad National Security, LLC (which operates Los Alamos
National Laboratory), and `pyproject.toml` classifies it as
"License :: OSI Approved :: Python Software Foundation License". HSSI's controlled license
vocabulary contains no Python Software Foundation entry — its rows are Apache License 2.0, the two
BSD variants, Creative Commons Attribution 4.0 International, the GPL v2 and v3-or-later entries,
the LGPL v2 and v3.0-only entries, MIT License, Other, and Restricted. Mapping SpacePy to the
generic `Other` row would be less accurate than recording the true license here and leaving HSSI's
field empty, so the field is empty by decision, not by omission.

**Standing recommendation:** add Python Software Foundation License 2.0 to HSSI's controlled license
vocabulary; this field can then be populated correctly.

**Do not adopt Zenodo's license value.** Zenodo's record for the 0.7.0 release states
`{"id": "cc-by-4.0"}`. That is wrong for SpacePy — `LICENSE.md` is the PSF-derived Triad license —
and it is a particularly easy error to import, because *Creative Commons Attribution 4.0
International* does exist in HSSI's vocabulary and would be accepted without complaint. Any future
DOI-driven autofill must be overridden here.

The bundled modified IRBEMlib is separately covered by the LGPL; that applies to the vendored
component, not to SpacePy as a whole.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- Ascii
- Batsrus
- Cdf
- Coordinates
- Csv
- Data Access
- Data Analysis
- Data Container
- Hdf5
- Heliophysics
- Heliosphere
- Igrf
- Ionosphere
- Magnetohydrodynamics
- Magnetosphere
- Omni
- Physics
- Plasma
- Plotting
- Python
- Radiation Belts
- Reference Data
- Shue
- Simulation
- Solar Wind
- Space
- Space Weather
- Swmf
- Time
- Tsyganenko

Sources: the PyHC registry entry (which supplies most of these, including `csv`, `data_container`
and `reference_data`), `pyproject.toml`'s `keywords`, the README, and
`Doc/source/capabilities.rst`. Canonical keyword terms are lowercase; the catalogue presents the
same terms in Title Case, so the difference is presentation rather than content.

**Where the source terms actually come from.** The repository's GitHub topics are exactly seven:
`python`, `python3`, `space`, `coordinates`, `batsrus`, `swmf`, `cdf`. `magnetosphere` and `plasma`
are **not** GitHub topics — they come from `pyproject.toml`'s `keywords`
(`magnetosphere`, `plasma`, `physics`, `space`, `solar.wind`, `space.weather`,
`magnetohydrodynamics`). All of these are already covered by the list above; `python3` was not
added separately as a near-duplicate of `Python`.

**`Heliosphere` is included** because it is PyHC's own literal term for this package, it exists as a
row in the live Keyword vocabulary, it expresses a concept none of the other keywords carries, and
it matches the Solar Wind and Interplanetary Space regions in Field 5.

**`ionosphere_thermosphere_mesosphere` is deliberately excluded**, even though it is PyHC's literal
term and SpacePy genuinely covers that domain. HSSI's live Keyword table carries two near-duplicate
rows for the concept — `ionosphere_thermosphere_mesosphere` and
`ionosphere thermosphere mesosphere` — so selecting either one entrenches a duplicate rather than
resolving it. Keywords are an open vocabulary, so a new spelling would only add a third. The concept
is already carried by the existing `Ionosphere` keyword together with the Earth Ionosphere and Earth
Thermosphere regions in Field 5. If the duplicate rows are ever merged upstream, this exclusion can
be revisited.

### 17. Data Sources (OPTIONAL)
- FTP/FTPS Directories
- HTTP/HTTPS Directories
- Observatory/Mission-specific
- OMNIWeb
- WDC
- Other

- **OMNIWeb** — `spacepy.omni.get_omni` serves the OMNI and Qin-Denton near-Earth solar wind
  databases, and `spacepy.toolbox.update` maintains the local copies.
- **HTTP/HTTPS Directories** — `spacepy.toolbox._crawl_yearly` walks year-partitioned HTTP directory
  listings to fetch data; the shipped defaults include the OMNI2 hourly CDF tree at SPDF
  (`https://spdf.gsfc.nasa.gov/pub/data/omni/omni_cdaweb/hourly/`), the Qin-Denton daily files, the
  leap-second table at `https://maia.usno.navy.mil/ser7/tai-utc.dat`, and the PSD database at
  `http://spacepy.lanl.gov/repository/psd_dat.sqlite`.
- **Observatory/Mission-specific** — the default `qd_daily_url` is the Van Allen Probes ECT science
  operations centre's public data server, `https://rbsp-ect.newmexicoconsortium.org/data_pub/QinDenton/`.
- **WDC** — `spacepy.pybats.kyoto` is documented as "a tool set for obtaining and handling
  geomagnetic indices stored at the Kyoto World Data Center (WDC) website", and fetches Dst, Kp and
  AE/AL/AU directly from `wdc.kugi.kyoto-u.ac.jp` CGI endpoints. That is a direct World Data Center
  retrieval capability, distinct from the generic HTTP directory crawling above.
- **Other** — model and mission output formats that no listed source covers: SWMF/BATS-R-US,
  RAM-SCB, GITM and AE9/AP9 output files read from local storage.

**FTP/FTPS Directories is kept, with a caveat.** At this revision SpacePy configures no FTP endpoint.
Every default URL in `_read_config` is `http://` or `https://`. The `ftp://` strings that survive in
the shipped Python are two commented-out legacy defaults in `spacepy/toolbox/__init__.py`
(`#leapsec_url ='ftp://maia.usno.navy.mil/...'`, `#omni_url = 'ftp://virbo.org/QinDenton/...'`), and
the `/ftp/` in the default `qindenton_url` is a path segment on an HTTP server, not a protocol.
`spacepy.toolbox.get_url` is documented as opening "an HTTP URL" and is HTTP-specific in behaviour:
it inspects `Last-Modified` headers, tests `getcode() >= 400` as an HTTP status, and in keep-alive
mode selects `http.client.HTTPConnection`/`HTTPSConnection` explicitly.

The value is nonetheless kept, and that is the settled outcome rather than an oversight. One live
documentation reference still presents FTP as the source of the leap-second table —
`Doc/source/quickstart.rst` cites `ftp://maia.usno.navy.mil/ser7/tai-utc.dat` — even though the code
now fetches it over HTTPS. Dropping a stored value on evidence this mixed was judged worse than
recording it with the caveat. Read the value as a capability SpacePy had historically and no longer
exercises in code; if the documentation reference is ever updated, removal becomes clean-cut.

**Considered and not selected.**

- *CDAWeb* — the OMNI2 hourly product SpacePy downloads lives under an SPDF path whose name contains
  `omni_cdaweb`, but SpacePy crawls that HTTP directory tree directly rather than using CDAWeb's
  service or API, and offers no general CDAWeb dataset access. HTTP/HTTPS Directories plus OMNIWeb
  describe what SpacePy actually does. Recorded here so this near-miss is not re-proposed from the
  URL alone.
- *HAPI, SSCWeb, Madrigal, AMDA, VirES, TAP, das2, GFZ, The Virtual Solar Observatory., S3/Cloud-aware*
  — no client for any of these exists in the package.

### 18. Input File Formats (RECOMMENDED)
- ascii
- CDF
- csv
- HDF5
- IDL.sav
- ISTP-Compliant
- JSON
- netCDF3/4
- Other

- **CDF** and **ISTP-Compliant** — `spacepy.pycdf` reads NASA CDF, with `spacepy.pycdf.istp`
  providing ISTP metadata checking and tooling; `spacepy.datamodel.ISTPArray`/`ISTPContainer` carry
  the same conventions into the data model.
- **HDF5** and **netCDF3/4** — `spacepy.datamodel.fromHDF5` and `fromNC3`; netCDF4 files are read
  through the HDF5 path.
- **ascii** and **JSON** — `readJSONheadedASCII` and `readJSONMetadata` read SpacePy's JSON-headed
  ASCII format; plain ASCII model output is read throughout pybats and `spacepy.ae9ap9`.
- **csv** — `spacepy.ae9ap9` parses the AE9/AP9 output header's
  "Data Delimiter:" line and sets a comma delimiter when the file declares one
  (`ans['delimiter'] = ','`), then reads the body with that delimiter. Comma-separated input is
  therefore an explicitly handled case, not an incidental one. The PyHC registry entry also carries
  the `csv` keyword.
- **Other** — SWMF/BATS-R-US binary and ASCII `*.out`/`*.outs` output, RAM-SCB output, DGCPM, RIM,
  PWOM and GITM files, and the AE9/AP9 text products.

**IDL.sav is kept, on the second of two readings.** SpacePy itself never calls `scipy.io.readsav`,
and no `.sav` handling exists in the package. The earlier basis for this value — a mention of `scipy.io.readsav`
in `Doc/source/capabilities.rst` — is not sound, because that page's opening sentence says it lists
capabilities "and, in some cases, of other packages that might be of interest to SpacePy users", and
the `readsav`, `numpy.loadtxt` and `astropy.io.fits` entries all sit in that third-party category.
The value is nonetheless **retained**, because there is a second and better reading: `spacepy.pybats`
reads SWMF's *IDL-formatted* output files (`IdlFile`: "reads/parses an IDL-formatted output file
from the SWMF", accepting `*.out`/`*.outs`), and `IDL.sav` is the nearest term the controlled
vocabulary offers for IDL-origin binary data. Both readings are recorded because the value rests on
the second one; the stricter reading, under which `IDL.sav` means only the IDL save-file format and
the value would be dropped, was considered and not adopted.

**Considered and not selected.** *FITS* — `astropy.io.fits` is named in the same third-party section
of `capabilities.rst`; SpacePy has no FITS reader of its own. *Zarr* — no support.

### 19. Output File Formats (RECOMMENDED)
- ascii
- CDF
- HDF5
- ISTP-Compliant
- JSON
- Other

`spacepy.datamodel` writes via `toCDF`, `toHDF5`, `toJSONheadedASCII` and `writeJSONMetadata`, with
`createISTPattrs` producing ISTP-compliant attributes; `spacepy.pycdf` writes CDF directly, including
creation from a master/skeleton CDF. `Other` covers `toHTML` and the SWMF input files SpacePy can
write (see `ImfInput` in Field 30).

**netCDF3/4 is intentionally absent here.** `spacepy.datamodel` provides `fromNC3` for reading but
no netCDF writer, so netCDF is an input-only format.

**csv is intentionally absent here.** `toJSONheadedASCII` accepts a `delimiter` keyword and can
therefore emit comma-separated data rows, but the product is a JSON-headed ASCII file already
covered by `ascii` and `JSON`; SpacePy has no plain-CSV writer. This asymmetry with Field 18 is
deliberate.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

`pyproject.toml` classifiers list MacOS X, Microsoft Windows, POSIX and POSIX :: Linux, and CI runs
on all three platforms. `Solaris` and `Other` are not claimed despite the generic POSIX classifier,
as no evidence of testing or support on those platforms exists.
`Operating System Independent` is inapplicable — SpacePy ships compiled C and Fortran components and
platform-specific binary wheels.

### 21. CPU Architecture (RECOMMENDED)
- Apple Silicon arm64
- Linux aarch64 or arm64
- x86-64

The 0.7.0 release notes lead with "Binary wheels are now provided for Linux on 64-bit ARM, intended
for Raspberry Pi"; macOS wheels cover Apple Silicon; x86-64 is supported across all three operating
systems. `ppc64le`, `GPU`, `HPC or HEC`, `Sun (SPARC)`, `Other` and `CPU Independent` are not
claimed — no wheels, CI targets or documentation support them.

### 22. Related Phenomena (OPTIONAL)
- Geomagnetic Storms
- Solar Wind

An earlier version of this field was empty. That was an under-claim rather than a correct emptiness:
both terms below are supported by named modules, as set out here.

- **Geomagnetic Storms** — `spacepy.empiricals.getDststar` implements pressure-corrected Dst
  (O'Brien and Burton formulations), the standard storm index; `getLmax` implements an empirical
  last-closed-drift-shell model for storm conditions; `spacepy.pybats.kyoto` retrieves Kyoto WDC Dst
  and AE indices; `spacepy.pybats.ram` handles output from the RAM-SCB ring-current model; and the
  default external field throughout `spacepy.irbempy` is `T01STORM`, the storm-time Tsyganenko model.
- **Solar Wind** — `spacepy.omni.get_omni` retrieves OMNI and Qin-Denton solar-wind parameters;
  `spacepy.empiricals.getExpectedSWTemp` models the expected solar-wind temperature; the Shue
  magnetopause functions are driven by solar-wind dynamic pressure and IMF Bz; and
  `spacepy.pybats.ImfInput` reads and writes SWMF's upstream solar-wind input files. The term is
  also already an HSSI keyword for this software.

**Considered and not selected.** The remaining terms in the controlled vocabulary are Coronal
Heating, Coronal Mass Ejections, Solar Corona, Solar Flares, and X-ray emission. A search of
the shipped package and the documentation sources found no mention of coronal mass ejections,
solar flares, coronal heating or X-ray emission. The nearest candidate,
`spacepy.empiricals.getSolarProtonSpectra`, computes the fluence spectrum of a solar energetic
particle event using the Ellison and Ramaty (1985) form; solar energetic particles have no term in
this vocabulary, and the function models the particle spectrum rather than the flare or CME that
produced it. Radiation belts, substorms, ring current, plasmapause and magnetopause — all genuinely
supported by SpacePy — likewise have no term in this vocabulary; their absence from this field
reflects the vocabulary's coverage, not a gap in the software.

### 23. Development Status (RECOMMENDED)
Active

Commits continue through March 2026 on the default branch; releases are ongoing; the PyHC registry
rates SpacePy's Software Maturity as "Good". The `pyproject.toml` classifier
"Development Status :: 4 - Beta" describes API maturity rather than project activity and is not the
basis for this value.

### 24. Documentation (RECOMMENDED)
https://spacepy.github.io/

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
  - **Funder Identifier:** https://ror.org/027ka1x80
- **Organization:** United States Department of Energy
  - **Funder Identifier:** https://ror.org/01bj3aw27
- **Organization:** Johns Hopkins University Applied Physics Laboratory
  - **Funder Identifier:** https://ror.org/029pp9z10

**Authoritative source.** The Funding section of the reference publication (Niehof et al. 2022,
*Frontiers in Astronomy and Space Sciences* 9, `10.3389/fspas.2022.1023612`, open access) states:

> SpacePy development has been supported by several missions, including the Van Allen Probes
> Radiation Belt Storm Probe, Energetic particle, Composition, and Thermal plasma suite, JHU/APL
> contract 967399 under NASA prime contract NAS5-01072; and the Parker Solar Probe Integrated
> Science Investigation of the Sun, JHU/APL contract 136435 under NASA prime contract NNN06AA01C.
> Further support was provided by United States Government contract 89233218CNA000001 for Los Alamos
> National Laboratory (LANL), which is operated by Triad National Security, LLC for the United States
> Department of Energy; and NASA Grant 80NSSC21K0304 "Enhancing Heliophysics Python Library
> Interoperability by Adapting Common Data Models".

This is the authoritative basis for **NASA**, which supported the work through two prime contracts
and a grant, and for the **United States Department of Energy**, through the LANL contract. Both
organizations were recorded here before this evidence was located; the funding statement is what now
substantiates them, and it should be the citation of record rather than the earlier bare assertion.

**Johns Hopkins University Applied Physics Laboratory is included (settled).** Both mission-derived
support paths reached the SpacePy developers as JHU/APL contracts (967399 and 136435). APL is the
organization that issued those contracts, which meets the field's definition of an organization
supporting the work through a financial contribution, and the paper names those contracts explicitly
as the instruments of support. The considered alternative — that APL is merely a pass-through of the
NASA prime contracts, so NASA alone is the funder — is a reasonable reading and is recorded here as
the rejected one, so a later refresh does not reopen it.

**Considered and not selected.**

- *Triad National Security, LLC* — the paper identifies Triad as the entity that **operates** LANL
  for the Department of Energy. It is the management contractor and recipient, not the funder; DOE
  is the funder, and is recorded.
- *Los Alamos National Laboratory* — repository copyright notices (`LICENSE.md`, module headers)
  document LANL as the developing institution, and the paper shows it as the recipient of DOE
  contract 89233218CNA000001. It is the performing organization, not a funder, and is recorded
  instead as an author affiliation in Field 6.
- The Acknowledgments section of the same paper thanks contributors ("everybody who has contributed
  to SpacePy via pull requests, discussions, and well-formed issues") and names no funder, so it
  adds nothing here. The Data Availability Statement points only to the article's supplementary
  material.
- The older SciPy 2010 proceedings paper (`10.25080/Majora-92bf1922-012`) has **no** acknowledgments
  or funding section at all — its text runs from the closing "SpacePy in action" section straight
  into the reference list. It is therefore not a source of funder or award information, and a future
  refresh need not re-read it for that purpose.

### 26. Award Title (OPTIONAL)
- **Award Title:** Enhancing Heliophysics Python Library Interoperability by Adapting Common Data Models
  - **Award Number:** 80NSSC21K0304
  - **Funder:** National Aeronautics and Space Administration

This field was previously empty on the basis that no award was documented; the reference
publication's Funding section (quoted in full in Field 25) supplies one. It is the only support
instrument in that statement for which the paper gives an actual award **title**, quoted there in
full. The title is 85 characters, within HSSI's 128-character limit for an award name.

**Other support instruments named in the same statement, deliberately not entered as awards
(settled).** The paper names each of these by the mission or investigation it funded rather than by
an award title, so entering them would require inventing titles the source does not provide, and
that was decided against. Their numbers are preserved here as durable evidence of how SpacePy was
funded, and so the decision does not have to be re-derived:

- Van Allen Probes RBSP Energetic particle, Composition, and Thermal plasma (ECT) suite —
  JHU/APL contract **967399**, under NASA prime contract **NAS5-01072**.
- Parker Solar Probe Integrated Science Investigation of the Sun —
  JHU/APL contract **136435**, under NASA prime contract **NNN06AA01C**.
- Los Alamos National Laboratory — United States Government contract **89233218CNA000001**
  (DOE; LANL operated by Triad National Security, LLC).

Note that two of these carry nested numbers (a JHU/APL contract under a NASA prime contract), so
even the choice of which number represents "the award" is not determined by the source.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Papers describing SpacePy.**

- https://doi.org/10.25080/Majora-92bf1922-012 — Morley, S. K., Koller, J., Welling, D. T.,
  Larsen, B. A., Henderson, M. G., & Niehof, J. T. (2011). SpacePy — A Python-based library of tools
  for the space sciences. *Proceedings of the 9th Python in Science Conference (SciPy 2010)*, 67–72.
- https://doi.org/10.3389/fspas.2022.1023612 — Niehof, J. T., Morley, S. K., Welling, D. T., &
  Larsen, B. A. (2022). The SpacePy space science package at 12 years. *Frontiers in Astronomy and
  Space Sciences*, 9.

**Papers that use SpacePy, from the developers' own curated list.**

- https://doi.org/10.1016/j.asr.2019.11.023 — Gieseler, J., Oleynik, P., Hietala, H., Vainio, R.,
  Hedman, H.-P., Peltonen, J., Punkkinen, A., Punkkinen, R., Säntti, T., Hæggström, E., Praks, J.,
  Niemelä, P., Riwanto, B., Jovanovic, N., & Mughal, M. R. (2020). Radiation monitor RADMON aboard
  Aalto-1 CubeSat: First results. *Advances in Space Research*, 66(1), 52-65.
- https://doi.org/10.1002/2014GL059533 — Jordanova, V. K., Yu, Y., Niehof, J. T., Skoug, R. M.,
  Reeves, G. D., Kletzing, C. A., Fennell, J. F., & Spence, H. E. (2014). Simulations of inner
  magnetosphere dynamics with an expanded RAM-SCB model and comparisons with Van Allen Probes
  observations. *Geophysical Research Letters*, 41(8), 2687-2694.
- https://doi.org/10.5194/angeo-30-1633-2012 — Niehof, J. T., Morley, S. K., & Friedel, R. H. W.
  (2012). Association of cusp energetic ions with geomagnetic storms and substorms.
  *Annales Geophysicae*, 30(12), 1633-1643.
- https://doi.org/10.1029/2012GL051722 — Turner, D. L., Angelopoulos, V., Shprits, Y., Kellerman, A.,
  Cruce, P., & Larson, D. (2012). Radial distributions of equatorial phase space density for outer
  radiation belt electrons. *Geophysical Research Letters*, 39, L09101.
- https://doi.org/10.1029/2009JA014596 — Welling, D. T., & Ridley, A. J. (2010). Exploring sources of
  magnetospheric plasma using multispecies MHD. *Journal of Geophysical Research: Space Physics*,
  115, A04201.
- https://doi.org/10.1098/rspa.2010.0078 — Morley, S. K., Friedel, R. H. W., Spanswick, E. L.,
  Reeves, G. D., Steinberg, J. T., Koller, J., Cayton, T., & Noveroske, E. (2010). Dropouts of the
  outer electron radiation belt in response to solar wind stream interfaces: Global Positioning
  System observations. *Proceedings of the Royal Society A*, 466(2123), 3329-3350.
- https://doi.org/10.2172/1035497 — Niehof, J. T., & Morley, S. K. (2012). Determining the
  significance of associations between two series of discrete events: bootstrap methods.
  Technical Report LA-14453, Los Alamos National Laboratory.

**Sources for this field.** `Doc/source/publications.rst` is the developers' own curated publication
list and is authoritative for this field alongside `CITATION.cff`. Its opening states "The following
publications have been prepared using SpacePy. If you have published a paper using SpacePy, contact
the SpacePy team to be added to this list", which is exactly the curation this field's definition
asks for — publications that "describe, cite, or use the software that the software developer
prioritizes". The first six entries above are the whole of its "Papers using SpacePy →
Peer-reviewed papers" section; the seventh is the sole DOI-bearing entry in its "Papers using
SpacePy → Other publications and presentations" section.

Author, title, year and journal agree between each DOI's registered metadata and the docs page. Two
harmless discrepancies are worth recording so they are not mistaken for errors later: the docs page
gives the Jordanova et al. page range as 2687-2695 where the publisher registers 2687-2694, and the
OSTI record for the technical report lists two organizational "authors" (USDOE NNSA and Los Alamos
National Laboratory) alongside the two human authors, Niehof and Morley, whom the docs page names.

**The "Papers about SpacePy" section contributes nothing further, and that is a finding rather than
an omission.** Its peer-reviewed subsection contains only the SciPy 2010 paper, already recorded
above, and links to it by PDF rather than by DOI. Its "Other publications and presentations"
subsection holds three items — the 2012 AGU abstract "Space Science with the SpacePy Toolkit", a 2010
tri-fold, and a 2010 GEM Summer Workshop poster — none of which carries a DOI, so none is recordable
in this field.

The two package papers listed first are general references in `CITATION.cff` and in the README's
BibTeX block. The 2022 article is additionally recorded as the Reference Publication (Field 14); it
appears in both fields because it is both the preferred citation and a publication describing the
software.

**Reaching the 2011 article text.** The DOI recorded above, `10.25080/Majora-92bf1922-012`, is the
one `CITATION.cff` publishes and is retained as the value; note, though, that it resolves to the
volume index `https://proceedings.scipy.org/articles/proceedings-2010` rather than to the article.
The legacy `conference.scipy.org/proceedings/scipy2010/morley.html` URL is still served, as a small
stub reading "This content has moved" that carries a `meta http-equiv="refresh"` to a **different**
DOI suffix, `https://doi.org/10.25080/Majora-92bf1922-00c`. That one lands on the specific article
page `https://proceedings.scipy.org/articles/Majora-92bf1922-00c`, titled "SpacePy - A Python-based
Library of Tools for the Space Sciences", with a per-article PDF at
`https://proceedings.scipy.org/articles/Majora-92bf1922-00c.pdf`. Use that per-article PDF rather
than the collected-volume PDF (`https://proceedings.scipy.org/articles/proceedings-2010.pdf`,
article at pages 67–72) when the text is needed.

### 28. Related Datasets (OPTIONAL)
Not found

SpacePy consumes data from several external sources — the OMNI2 hourly database at SPDF, the
Qin-Denton derived solar-wind database served by the Van Allen Probes ECT science operations centre,
the USNO leap-second table, AE9/AP9 model output, and SWMF-family simulation output — but none of
these is published with a dataset DOI that the repository cites, and the repository nowhere
identifies a dataset as related to the software in the sense this field intends. The reference
publication's Data Availability Statement points only to the article's supplementary material and
names no dataset.

### 29. Related Software (OPTIONAL)
- https://github.com/MAVENSDC/cdflib — pure-Python NASA CDF library; a same-purpose alternative to
  `spacepy.pycdf`, useful for distinguishing the two.
- https://github.com/PRBEM/IRBEM — the IRBEM library, bundled in modified form under
  `spacepy/irbempy/` and wrapped by `spacepy.irbempy`; a domain-specific dependency.
- https://github.com/spacepy/dbprocessing — companion data-processing framework from the same
  SpacePy organization.
- https://github.com/sunpy/sunpy — sister heliophysics Python package; like SpacePy, a PyHC core
  package, and the closest same-ecosystem comparison for a user choosing between them.

These four are settled. Generic scientific-Python dependencies (NumPy, SciPy, Matplotlib, h5py,
python-dateutil) are excluded here for the same reason they are excluded from Field 30: being a
dependency is not, by itself, a relationship worth recording.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/SWMFsoftware/SWMF — Space Weather Modeling Framework
- https://github.com/lanl/RAM-SCB — Ring current-Atmosphere interactions Model with Self-Consistent
  magnetic field
- https://autoplot.org/ — Autoplot

This field once held Matplotlib, pandas, SciPy, Astropy, h5py and NumPy. Those were removed on the
grounds that they are generic runtime dependencies rather than software SpacePy exchanges data with,
and **that decision stands and must not be reversed** — being a dependency is not interoperability.
The three entries above are of a different kind, each backed by a specific, named exchange:

- **SWMF** — `spacepy.pybats` exists to exchange data with the Space Weather Modeling Framework, in
  both directions. Its module docstring reads "Module for reading, manipulating, and visualizing
  BATS-R-US and SWMF output", and `Doc/source/pybats.rst` states that "PyBats provides access to
  output files written by the Space Weather Modeling Framework and the codes contained within".
  `IdlFile` parses SWMF `*.out`/`*.outs` files, and dedicated readers cover the framework's
  components — `bats` (BATS-R-US), `rim` (Ridley Ionosphere Model), `gitm` (Global
  Ionosphere-Thermosphere Model, the SWMF's UA module), `pwom` (Polar Wind Outflow Model, the PW
  module) and `dgcpm` (Dynamic Global Core Plasma Model, the plasmasphere module). The reverse
  direction is explicit too: `spacepy.pybats.ImfInput` is "A class to read, write, manipulate, and
  visualize solar wind upstream input files for SWMF simulations", so SpacePy can generate the
  driving input a SWMF run consumes.
- **RAM-SCB** — `spacepy.pybats.ram` is "A module for reading, handling, and plotting RAM-SCB
  output". RAM-SCB is listed separately from SWMF because it is also distributed standalone by Los
  Alamos National Laboratory, and SpacePy provides a dedicated reader for it rather than reaching it
  only through the framework.
- **Autoplot** — `spacepy.datamodel`'s JSON-headed ASCII format is an interchange format shared with
  Autoplot, not merely a SpacePy-internal one. `Doc/source/capabilities.rst` describes it as
  "ASCII-based data files with rich JSON metadata, supported by tools such as Autoplot", and
  `Doc/source/quickstart.rst` calls the format "RBSP/AutoPlot-compatible". SpacePy's output is
  therefore directly loadable by Autoplot. This is the weakest of the three entries, resting on two
  documentation statements rather than on code, and is recorded with that qualification.

*The trailing slash on the Autoplot URL is deliberate and must be preserved.* Related-item
identifiers are matched as exact strings, so `https://autoplot.org` and `https://autoplot.org/`
resolve to the same page but occupy two separate catalogue entries. The slashed form is the one this
record holds; rewriting it without the slash on a later refresh re-splits the entry rather than
correcting it.

**Considered and not selected.** AE9/AP9 — `spacepy.ae9ap9` reads its output, which would qualify,
but AE9/AP9 is distributed through a restricted United States Air Force channel with no public
repository or DOI to record, and this field requires an identifier. IRBEM is bundled and wrapped
rather than exchanged with, so it belongs in Field 29 and is recorded there.

### 31. Related Instruments (OPTIONAL)
Not found

**This emptiness is a finding, not a gap.** SpacePy is an instrument-agnostic toolkit. A search of
the shipped package modules at this revision for instrument and mission names found no
instrument-specific reader, parser, calibration routine, or format implementation. The capabilities
that touch instrument data do so through generic, multi-mission formats — NASA CDF with ISTP
conventions, HDF5, netCDF, JSON-headed ASCII — which belong in Fields 18 and 19, or through generic
archives and services, which belong in Field 17.

No instrument clears the "designed to support" bar, so this field stays empty. The one entity that
does clear it, OMNI, resolves to an observatory and is recorded in Field 32; an `OMNI Instrument`
row exists in the vocabulary (`https://spase-metadata.org/SMWG/Instrument/OMNI`) and was
deliberately not used here, because SpacePy consumes the OMNI data product rather than supporting an
instrument. Since this field admits only entries carrying an `https://spase-metadata.org/`
identifier, no name may be recorded speculatively in any case.

**Association considered and rejected: Van Allen Probes / RBSP-ECT.** This is the association most
likely to be proposed again, so the reasoning is recorded. Three real links exist: the reference
publication's Funding section shows SpacePy development supported by the Van Allen Probes ECT suite
contract; the SciPy 2010 paper reports that "The Science Operations Center for the RBSP mission is
also incorporating SpacePy into its processing stream" and that `pycdf` development was "targeted
towards the generation of ISTP-compliant CDF files for the upcoming Radiation Belt Storm Probes
(RBSP) mission"; and the default Qin-Denton data URL is hosted by the RBSP-ECT science operations
centre. None of these makes SpacePy designed to support the instrument. The funding and deployment
links are provenance, recorded in Fields 25 and 26; the ISTP CDF work produced a *generic*
multi-mission capability, not an RBSP reader; and the Qin-Denton database, although hosted by
RBSP-ECT, contains OMNI-derived interplanetary parameters rather than Van Allen Probes measurements,
so the link is a hosting location and is recorded in Field 17 as an observatory/mission-specific
data source.

### 32. Related Observatories (OPTIONAL)
- **OMNI** — `https://spase-metadata.org/SMWG/Observatory/OMNI`

**Why OMNI meets the designed-to-support bar.** `spacepy.omni.get_omni` is a purpose-built core
capability, not an incidental one: it is cited elsewhere in this dossier as the evidence for the
`Models and Simulations: Data Guided` functionality (Field 4), the Solar Wind and Interplanetary
Space regions (Field 5), the `OMNIWeb` data source (Field 17), and the Solar Wind phenomenon
(Field 22). `spacepy.toolbox` maintains the local OMNI and Qin-Denton databases, and SpacePy's
empirical and Tsyganenko-field entry points consume those values as their driving inputs. A user
searching HSSI for software that works with OMNI should get SpacePy back. SPASE describes
`SMWG/Observatory/OMNI` as a virtual observatory over ACE, Wind, IMP 8, Geotail, GOES and others,
so the observatory type fits what OMNI is.

**Resolution.** Two observatory rows (`type` 2) carry the exact name `OMNI`:
`https://spase-metadata.org/SMWG/Observatory/OMNI` and
`https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/OMNI`. This is one entity with two candidate
rows, so the documented tie-break applies — prefer the `SMWG/...` row among same-name duplicates —
and the CNES/CDPP-AMDA row is rejected as a national data-centre mirror of the same virtual
observatory. Because the tie-break resolves it, this is a settled selection and not an unresolved
ambiguity.

**Considered counter-view, rejected.** OMNI can be read as a multi-mission *derived data product*
already captured by Field 17's `OMNIWeb` value, in which case listing it here would be duplication.
That reading was weighed and rejected: Field 17 records *where SpacePy fetches data from*, whereas
this field records *what SpacePy is designed to support*, and HSSI's own vocabulary classifies OMNI
as an observatory. Recorded so a later refresh does not relitigate it.

**Negative research — do not re-propose these.** The other candidates that surface from the
repository are SWMF/BATS-R-US, RAM-SCB, GITM, DGCPM, RIM, PWOM and AE9/AP9. HSSI's SPASE-backed
vocabulary holds **no row for any of them**, nor for Qin-Denton. They are modelling frameworks and derived products, and they are already represented
correctly elsewhere: as interoperable software (Field 30), as data sources (Field 17), and as file
formats (Fields 18 and 19).

**Kyoto ground observatories, rejected.** `spacepy.pybats.kyoto` fetches *derived indices* — Dst, Kp
and AE/AL/AU — from the World Data Center at Kyoto, not any individual station's magnetometer data.
The vocabulary does contain a large family of individual ground geomagnetic observatory rows under
`https://spase-metadata.org/IUGONET/Observatory/WDC_Kyoto/...`, but SpacePy is designed to support
none of them specifically, so they are omitted. Field 17's `WDC` value already captures that source.

**On the instrument side.** An `OMNI Instrument` row also exists
(`https://spase-metadata.org/SMWG/Instrument/OMNI`, `type` 1). It is deliberately not used: SpacePy
consumes the OMNI *data product* rather than supporting an instrument, so the association belongs at
the observatory level. Field 31 stays empty.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/spacepy/spacepy/cb983af96e06265dc35463e0d725a11eaf0682a6/Doc/source/_static/spacepy_logo.jpg

The canonical logo asset in the repository, recorded as a raw URL pinned to the commit above rather
than tracking the default branch — a branch reference breaks silently on any upstream rename, move or
deletion, and a redesign should be recorded by a refresh rather than inherited unannounced. The PyHC registry points at
the rendered documentation copy (`https://spacepy.github.io/_static/spacepy_logo.jpg`), which is the
same image; the repository-hosted URL is preferred because it is the source of record.
