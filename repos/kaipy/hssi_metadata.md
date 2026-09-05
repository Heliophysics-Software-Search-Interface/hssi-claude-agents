# HSSI Metadata Extraction Results

**HSSI Software ID:** e2069dd1-ba2f-45fa-b2b7-9052a16f74cc
**Repository:** https://github.com/JHUAPL/kaipy
**Source Revision:** 0028c69c52a91ff378a5798708daaba4cdfb5790
**Extraction Date:** 2026-09-04
**Validation Date:** 2026-09-05
**Validation Status:** PASS

---

**Scope note.** Kaipy is the Python analysis-and-visualization layer of a two-package system: the
Fortran simulation suite **Kaiju** (MAGE, GAMERA, GAMERA-helio, RAIJU, REMIX, RCM, CHIMP) produces
HDF5 output, and Kaipy reads, reduces, models against, and plots it. Almost every judgement below
turns on that division of labour — Kaipy is not the simulation, but it is not a generic plotting
library either, and several fields (Software Functionality, Related Region, Related Software) are
decided by asking which half of the pair a given capability really belongs to. The pinned revision
is tag `kaipy-1.1.4`, which is also the tip of `master`; three branches exist and one of them,
`dev_h5concat`, is unmerged, which matters for Development Status and Version. `external_contrib` is
**not** a second unmerged branch: it is an ancestor of `master`, and its tip `4e98d39` ("Merged in
external_contrib (pull request #18)") is the `kaipy-1.1.3` tag commit itself.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This entry was not submitted by this project; the placeholder is the catalogue convention for a
record maintained by curation rather than by its authors. It is not a defect and must not be
"corrected" to a curator's name — `Submitter.email` is the key that controls who can unlock the
entry for editing.

### 2. Persistent Identifier (RECOMMENDED)
**Concept DOI:** https://doi.org/10.5281/zenodo.15801040

This is the Zenodo **concept** DOI, which is the correct choice for this field because it always
resolves to the newest deposited version rather than freezing the record at one release. Fetching it
redirects to `https://zenodo.org/records/17914543`, the 1.1.4 deposit, confirming both that it
resolves and that it is genuinely a concept DOI rather than a version DOI.

The deposit is a real GitHub–Zenodo integration release, not a manual upload: the Zenodo record
carries `{"identifier": "https://github.com/JHUAPL/kaipy/tree/kaipy-1.1.4", "relation":
"isSupplementTo", "resource_type": "software", "scheme": "url"}`. The `tree/<tag>` URL is the
signature the integration writes and a hand-made deposit does not have. This matters for Field 11:
because the DOI came through the GitHub–Zenodo workflow, Zenodo is the correct Publisher.

The 1.1.4 deposit's twelve creators, with ORCIDs and affiliations, match `CITATION.cff` at the pin
exactly, which is why that deposit — not the older 1.1.3 one — is the authoritative external source
for Field 6.

**Version DOIs under this concept** (recorded so a later refresh does not have to re-derive them):
1.1.2 https://doi.org/10.5281/zenodo.15801041, 1.1.3
https://doi.org/10.5281/zenodo.17236774, 1.1.4 https://doi.org/10.5281/zenodo.17914543. A version
DOI belongs in Field 12, not here.

### 3. Code Repository (MANDATORY)
https://github.com/JHUAPL/kaipy

Confirmed reachable, and confirmed as the project's own statement of record: `CITATION.cff` at the
pin carries `repository-code: "https://github.com/JHUAPL/kaipy"`, and the Zenodo deposit's
`isSupplementTo` points into the same repository.

**Do not take the repository URL from `setup.py`.** That file still carries the pre-migration
Bitbucket location, `url='https://bitbucket.org/aplkaiju/kaipy/src/master/',`, and a comment in
`kaipy/scripts/preproc/cda2wind.py` still points at `https://bitbucket.org/aplkaiju/kaiju/wiki/Gamerasphere`.
The project developed on Bitbucket first — the commit history at the pin begins 2024-05-16, while
the GitHub repository was created 2025-06-11 — so these are stale in-repo values, not alternatives.

### 4. Software Functionality (RECOMMENDED — treated as critical)

**Recorded values (30):**

*Coordinate Transforms*
- Coordinate Transforms
- Coordinate Transforms: Heliospheric
- Coordinate Transforms: Magnetospheric

*Data Processing and Analysis*
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Field-line Tracing
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis

*Data Visualization*
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: 3D Graphics
- Data Visualization: Line Plots
- Data Visualization: Movies
- Data Visualization: Orbit Plots
- Data Visualization: Spectrogram
- Data Visualization: Web-Based

*Models and Simulations*
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing
- Models and Simulations: MHD
- Models and Simulations: Physics-Based

*Servers and Environments*
- Servers and Environments
- Servers and Environments: High Performance Computing

Every value is written in the fully-qualified `Parent: Child` form deliberately. The
`FunctionCategory` vocabulary contains repeated child names — `Analysis`, `Processing`, `ML/AI` and
`Field-line Tracing` each appear under more than one parent — and a bare child name is resolved by an
unanchored case-insensitive lookup that takes the first row it finds, so an unqualified `Field-line
Tracing` could silently bind to the wrong branch. Every subcategory recorded here has its parent
recorded alongside it.

**Evidence for each value, by file at the pin.**

- **Coordinate Transforms / Magnetospheric.** `kaipy/transform.py` is a public module whose
  docstring opens "This module provides coordinate transformations relevant to geospace modeling."
  and which exports `SMtoGSM`, `GSMtoSM` and `GSEtoGSM`. `kaipy/cdaweb_utils.py` exposes
  `fetch_satellite_SM_position`, `fetch_spacecraft_SM_trajectory` and northern/southern magnetic
  footprint fetchers built on `frames.GeocentricSolarEcliptic`. These are user-facing conversions,
  not an internal utility step.
- **Coordinate Transforms / Heliospheric.** `kaipy/cdaweb_utils.py` builds `SkyCoord` objects in
  `frames.HeliocentricInertial` and transforms them into `frames.HeliographicStonyhurst`
  (`fetch_helio_spacecraft_HGS_trajectory`), and `kaipy/gamhelio/helioViz.py` does the same for the
  model grid. *`Coordinate Transforms: Solar` was considered and rejected*: Heliographic Stonyhurst
  appears in both the Solar and Heliospheric descriptions, but every use here converts spacecraft or
  grid positions in the inner heliosphere, not features on the solar disk, so Heliospheric is the
  honest single choice.
- **2D Slices (processing and visualization).** `kaipy/gamera/gampp.py` exposes `GetSlice` and
  `GetRootSlice`; `kaipy/gamera/magsphere.py` exposes `EggSlice`; `kaipy/chimp/kCyl.py` exposes
  `getSlc`. Those extract planes out of the 3-D volume (processing). `kaipy/gamera/msphViz.py`
  `plotXY`/`plotXZ`/`PlotEqB`/`PlotMerid` display them (visualization), and
  `docs/source/kaipy/usage.rst` walks a user through both.
- **Data Access and Retrieval.** `from cdasws import CdasWs` and per-spacecraft CDAWeb queries in
  `kaipy/cdaweb_utils.py` and `kaipy/satcomp/scutils.py`; `cdasws` appears in 12 of the 172 tracked
  `.py` files (`git grep -Pil -- "cdasws" <pin> -- '*.py'`) and 17 tracked files overall.
- **Data Reduction.** `kaipy/scripts/postproc/slimh5.py` opens "#Takes Gamera/Chimp/xxx file and
  slims it down based on start:stop:stride"; `slimFL` strides over points and over field lines
  (`-pskip`, `-flskip`); `slimh5_classic` and `pitmerge` are in the same family.
- **Energy Spectra.** `kaipy/satcomp/scRCM.py` `getSCOmniDiffFlux` — the code comment above it reads
  "grab specifically omnidirecitonal differential flux" (the misspelling is in the source) — plus
  `getIntensitiesVsL`, and the module-level `specFlux_factor_i` / `specFlux_factor_e` constants that
  convert to `[units/cm^2/keV/str]`.
- **Field-line Tracing (both parents).** `kaipy/gamera/magsphere.py` carries the comment "#Return
  data for meridional 2D field lines" above `bStream`, which integrates magnetic-field streamlines
  through the MHD volume; `genXLine` and `slimFL` handle field-line output files; REMIX's
  `BSFluxTubeInt` and `dB(self, xyz, hallOnly=True, Rin=2.0, rsegments=10)` integrate along field
  lines. *`Models and Simulations:
  Field-line Tracing` is retained rather than dropped* because the tracing is performed in a model
  field, which is what that subcategory describes; the `Data Processing and Analysis` sibling covers
  the same capability applied to stored output. Both were already recorded and both remain
  defensible.
- **File Format Conversion.** `wsa2gamera` — "This script converts a FITS file created by a WSA run
  to a HDF5 format" — plus `cda2wind` (CDAWeb/ASCII solar wind to Gamera HDF5), `ih2oh` (inner- to
  outer-heliosphere grid), and `genXDMF`/`genmpiXDMF`/`block_genmpiXDMF` (HDF5 to XDMF XML).
- **Time Series Analysis.** `kaipy/solarWind/` implements outlier rejection (`_coarseFilter`,
  n-sigma), gap interpolation (`_removeBadData`) and derived-quantity computation
  (`_appendDerivedQuantities`) over time-ordered solar wind data, with `TimeSeries.py` as the
  labelled container; `remixTimeSeries` is a dedicated CLI.
- **3D Graphics.** `kaipy/scripts/quicklook/vizTrj.py` imports `from mpl_toolkits.mplot3d import
  axes3d, Axes3D` and renders CHIMP particle trajectories with a 3-D Earth (`addEarth`, `axEqual3d`);
  `kaipy/paraview/` drives full 3-D ParaView pipelines.
- **Movies.** `kaipy/scripts/quicklook/gamerrVid.py` and `heliomovie.py` shell out to `ffmpeg` and
  write `.mp4`; `dbVid` and `gamsphVid` are in the same family.
- **Orbit Plots.** `kaipy/kaiViz.py` `trajPlot` and `helioTrajPlot`, and the `vizTrj` CLI.
- **Spectrogram (visualization).** `kaipy/satcomp/scRCM.py` `plt_ODF_Comp` renders
  `AxSC.pcolormesh(scTime, eGrid, np.transpose(scODF), norm=norm, shading='nearest', cmap=cmapName)`
  on a log energy axis — an energy–time spectrogram of measured against modelled differential flux.
  *`Data Processing and Analysis: Spectrogram` was considered and rejected*: the transform here is a
  flux calculation, not a time–frequency transform, so the processing side is recorded as `Energy
  Spectra` instead.
- **Web-Based.** `kaipy/scripts/quicklook/mageDash.py` is a complete Dash/Plotly application —
  "Display a live dashboard with information about an ongoing or completed MAGE run." — with
  `from dash import Dash, dcc, html, Input, Output, State`, `flask_caching`, `dash_bootstrap_components`,
  `plotly.graph_objs`, a `main()` and
  `app.run(host='127.0.0.1', port=port, debug=False, use_reloader=False)`. **Caveat worth
  keeping:** `mageDash` is registered as a console script in `setup.py` but is absent from
  `pyproject.toml`'s `[project.scripts]` (which lists 50 entries), and its `dash`,
  `dash_bootstrap_components`, `flask_caching` and `pyqt5` dependencies are declared in `setup.py`
  and `requirements.txt` but not in `pyproject.toml`. Because `pyproject.toml` carries a `[project]`
  table, that is the metadata a `pip install kaipy` uses — so the module ships but the command and
  its dependencies do not get wired up. The capability is real and in the shipped source; the
  packaging is inconsistent. It is also undocumented: `docs/source/scripts.rst` autoprograms the
  other quicklook scripts and omits this one.
- **Data Guided.** `kaipy/solarWind/` exists to turn observations into model boundary conditions:
  `OMNI`, `WIND` (Wind SWE + MFI files), `DSCOVRNC` (NOAA DSCOVR netCDF) and `ACESWPC` feed
  `cda2wind`, which writes the Gamera `bcwind.h5` upstream boundary file. That is precisely the
  "Models driven by observational data" case.
- **Empirical.** `kaipy/raiju/waveModel/genWM.py` and `kaipy/rcm/wmutils/genWM.py` build a
  wave-particle-interaction electron lifetime model by spline-fitting `chorus_polynomial.txt` and
  write it into the RAIJU configuration file; `kaipy/supermage.py` implements a 1-D layered-Earth
  magnetotelluric response — "Calculate 1D Z-Tensor for given ground resistivity profile." — and
  derives the ground geoelectric field from it (`E_Field_1D`, `EField1DCalculation`).
- **MHD and Physics-Based (both retained).** Kaipy does not integrate the MHD equations — Kaiju does.
  It is retained here because Kaipy is the MHD toolchain's Python side: `kaipy/gamera/gamGrids.py`
  and `genLFM` generate the MHD model grids, `XMLGenerator`/`kJobs.py` write the model input decks,
  and `kaipy/paraview/pvGam.py` reconstructs MHD quantities from the output (sound speed, Alfvén
  speed, magnetosonic Mach number) rather than merely displaying stored variables. Asked from the
  searcher's side — would someone browsing "Models and Simulations: MHD" be glad to find Kaipy? —
  the answer is yes: they are looking at the MAGE/GAMERA toolchain and Kaipy is how they will drive
  and read it. *`Models and Simulations: First Principles` was rejected* on the same logic run the
  other way: Kaipy solves nothing from first principles, and Kaiju's own entry legitimately carries
  that value.
- **Servers and Environments / High Performance Computing.** `kaipy/kJobs.py` emits PBS batch scripts
  with `#PBS -A`, `#PBS -q`, `#PBS -l select=`, `OMP_NUM_THREADS` and `omplace -nt`;
  `kaipy/satcomp/scutils.py` has `genSatCompPbsScript` and `genSatCompLockScript`;
  `msphPbsSatComp`, `run_calcdb` and `run_ground_deltaB_analysis` submit them with `qsub`; and
  `kaipy/scripts/postproc/templates/` ships four `.pbs`/`.xml` job templates.

**`Models and Simulations: ML/AI` was removed, on evidence.** The stored record carried that value
before this refresh; the pinned source does not support it, and it is absent from the 30 recorded
above.

There is no machine-learning code at the pin. Searching the tracked `.py`, `.rst`, `.md`, `.txt`,
`.toml` and `.cff` files case-insensitively for `tensorflow`, `torch`, `sklearn`, `scikit-learn`,
`keras`, `machine learning`, `neural`, `ML/AI`, `random forest` and `xgboost` returns zero files for
every term, while a control search for `matplotlib` over the same `.py` set returns 45 files, so the
tooling is working and the zeros are real. Those ten terms in fact return zero over the *whole*
tracked tree, binaries included, so the pathspec is not carrying the argument. The bare token `ML` is
different and the flag must be published with it: `git grep -Pil -- "\bML\b" <pin>` returns 5 files —
the four `.png` figures in `docs/source/_static/` and `kaipy/rcm/wmutils/DWang_chorus_lifetime.h5` —
every one of which merely contains those two bytes inside binary data. Run with `-I`, or over any
text pathspec, it returns none. **Recorded so a reader re-running a bare `ML` search does not read
this removal argument as falsified.**

From the searcher's side this is the clearest kind of defect: someone filtering HSSI for ML/AI models
and landing on a package with no machine learning in it has been misled. The general presumption
against spending a removal on an already-published value — the presumption that keeps the redundant
keywords under Field 16 — was weighed and is not reached here: those keywords are true but redundant,
whereas this value is false.

**Considered and rejected, with reasons** (recorded so a later refresh does not re-propose them):
- *Data Processing and Analysis: Plasma Moments* — `kaipy/paraview/pvGam.py` derives temperature and
  Mach number from the model's stored density and pressure. That is arithmetic on existing bulk
  quantities, not moment integration of a distribution function. Kaiju carries this value; Kaipy
  should not.
- *Data Processing and Analysis: 3D Particle Distribution Processing* — `kaipy/chimp/kCyl.py` reads a
  4-D (position, energy, pitch angle) phase-space-density grid produced by CHIMP and slices it. It
  consumes a distribution; it does not process one in velocity space.
- *Data Processing and Analysis: Pitch Angle Distributions* — pitch angle appears only as a grid axis
  read back from CHIMP output (`kaipy/chimp/kCyl.py` `getGrid(fIn, do4D=False)` returns the pitch
  angle grid when `do4D` is set), and `kaipy/satcomp/scRCM.py` carries a
  standing `# !!TODO: Properly calc OmniDiffFlux from FPDU. Currently just using pitch angle`. No PAD
  is computed.
- *Data Processing and Analysis: Image Processing* — `kaipy/kaiViz.py` `trimFig`, `ShaveX`, `ShaveY`
  and `isMagick` crop and trim saved PNG figures through ImageMagick. That is figure post-production,
  not scientific image analysis.
- *Mission-related (and its subcategories)* — Kaipy is not part of any mission ground system. It
  retrieves mission data from CDAWeb for model comparison, which is Data Access and Retrieval.
- *Servers and Environments: Software or Environment Container* — no Dockerfile, Singularity
  definition or container recipe exists at the pin.
- *Data Processing and Analysis: Data Assimilation, Curlometer, Magnetic Null Finding, Wave
  Polarization Analysis, Wavelet Analysis, Packet Decommutation, Calibration, Linear Gradient
  Estimation* — no corresponding code.
- *Data Visualization: Spacecraft Formation Plots* — the multi-spacecraft support is per-spacecraft
  time-series comparison, not constellation geometry.

### 5. Related Region (RECOMMENDED — treated as critical)

**Recorded values (6):**
- Earth Magnetosphere
- Earth Inner Magnetosphere
- Earth Ionosphere
- Earth Auroral Subregion
- Interplanetary Space
- Solar Wind

The `Region` vocabulary is **flat** — its 24 rows have no working parent/child relationships — so
`Earth Magnetosphere` does not imply `Earth Inner Magnetosphere`, `Interplanetary Space` does not
imply `Solar Wind`, and an argument of the form "X already encompasses Y" is not available here.
Each region has to be earned on its own evidence, and a searcher filtering on the fine value will
not see this entry unless the fine value is recorded.

- **Earth Magnetosphere** (already recorded). `kaipy/gamera/magsphere.py` (`GamsphPipe`),
  `msphViz.py`, and the `msphpic`/`gamsphVid`/`msphSatComp` script families read and plot the GAMERA
  global magnetosphere domain.
- **Earth Inner Magnetosphere.** `kaipy/rcm/` post-processes Rice Convection
  Model output and generates its energy-invariant channels; `kaipy/raiju/` handles the RAIJU
  inner-magnetosphere model including Dst, a plasmasphere density variable and a chorus wave model;
  `kaipy/chimp/kCyl.py` works on radiation-belt phase space density over an equatorial L / energy /
  pitch-angle grid; `rbspSCcomp` and `rcm_rbsp_satcomp` compare against Van Allen Probes data; and
  `kaipy/satcomp/scRCM.py` carries `tkl_lInner = 2  # Exclude points within 2 Re`, an inner-region
  cut. Case-insensitively, `RCM` appears in 46 tracked files under
  `git grep -Iil -- "RCM" <pin> -- '*.py' '*.rst'`. The pathspec is part of that claim, not a detail
  of how it was obtained: `'*.py'` alone gives 41, the whole tracked tree gives 49, dropping `-I`
  raises that to 50 because `kaipy/rcm/wmutils/DWang_chorus_lifetime.h5` contains the byte sequence,
  and the word-bounded `\brcm\b` over the whole tracked tree gives 41 (42 without `-I`).
- **Earth Ionosphere.** `kaipy/remix/remix.py` is a full REMIX
  ionospheric-electrodynamics reader and plotter whose variable table includes potential, current
  density, Pedersen and Hall conductance, Joule heating, ionospheric electric field components and
  field-aligned magnetic perturbation; `mixpic`, `remixTimeSeries` and `embiggenMIX` are its CLIs;
  and `docs/source/kaipy/usage.rst` instructs the user directly: "Importing the ionospheric data from
  REMIX follow the same format as the import of the magnetospheric data with the added requirement of
  specifying which hemisphere, e.g. NORTH or SOUTH, that you want to plot." `git grep -Pil --
  "ionospher" <pin> -- '*.py'` returns 8 files.
- **Earth Auroral Subregion.** REMIX's variable table carries the auroral precipitation quantities
  Kaipy plots: `'amtype'` / "Auroral model type", and mono and diffuse electron and proton energy,
  flux and energy flux (`Menergy`, `Mflux`, `Meflux`, `Denergy`, `Dflux`, `Deflux`, `Penergy`,
  `Pflux`, `Peflux`), all defined in `kaipy/remix/remix.py`'s variable table and populated from the
  REMIX file's `Auroral model type` and `IM Energy flux` datasets. `kaipy/gamera/deltabViz.py`
  computes and labels the auroral electrojet indices:
  `aStr = "Auroral Indices [nT]\nSME = %8.2f\nSML = %8.2f\nSMU = %8.2f" % (SME, SML, SMU)`.
  SME, SML and SMU are by definition auroral-electrojet indices, and mono and diffuse electron and
  proton precipitation are auroral-zone quantities; the package produces both. Asked from the
  searcher's side, someone browsing "Earth Auroral Subregion" software finds a package that maps
  auroral precipitation and computes auroral indices, which is a fair result.

  **Considered and not determinative: that the auroral content is a subset of an ionospheric
  capability already recorded.** Kaipy never restricts a domain to the auroral zone — the auroral
  variables are part of the REMIX ionospheric output that `Earth Ionosphere` already covers, so on
  that reading the finer value adds nothing a user would not reach through the coarser one. That was
  a reasonable reading and it did not prevail: the `Region` vocabulary is flat, so `Earth Ionosphere`
  does not surface this entry for an `Earth Auroral Subregion` query, and computing SME/SML/SMU is an
  auroral-specific product rather than an incidental slice of an ionospheric one. **Recorded rather
  than dropped so a later refresh reading the subset argument for itself can see it was known and
  weighed, not missed.**
- **Interplanetary Space** (carried over from the record as it stood before this refresh) and
  **Solar Wind** (added). These are
  separate flat rows and both are earned. `kaipy/gamhelio/` reads and plots the GAMERA-helio
  simulation domain, which begins at "21.5 Rsun (the inner edge of the gamhelio grid)." and extends
  outward — `helioViz.py` also handles the outer-heliosphere case, "#for 1-10 au helio". That domain
  is Interplanetary Space. Separately, the entire `kaipy/solarWind/` package exists to read and
  condition *solar wind* measurements (OMNI, Wind, DSCOVR, ACE), and `swpic` plots them; that is the
  Solar Wind region in its own right.

**Considered and rejected, with reasons:**
- *Earth Thermosphere* — MAGE couples to TIEGCM, but Kaipy at the pin cannot even write a TIEGCM
  input file: `kaipy/scripts/preproc/cda2wind.py` advertises a TIEGCM output format and then raises
  `Error:  Cannot currently produce TIEGCM output.` (the double space is in the source), with the
  adjacent comment `#FIXME: need to update when want to include, example code in
  pyLTR.SolarWind.Writer.TIEGCM`. `git grep -Pil -- "thermospher" <pin> -- '*.py'` returns 0 files.
  Kaiju's own entry carries this region; Kaipy has not earned it.
- *Earth Magnetotail*, *Earth Magnetosheath*, *Earth Outer Magnetosphere* — `magnetotail` and
  `magnetosheath` each return 0 files over the tracked `.py` set. `msphViz`'s default plot bounds
  `[-35,25,-25,25]` do include the near tail, but a default axis range is not a region of study, and
  there is no tail-, sheath- or outer-magnetosphere-specific analysis. `BowShockX/Y/Z` appear only as
  OMNI variable names passed through the solar-wind reader.
- *Planetary Magnetospheres*, *Jupiter Magnetosphere*, *Saturn Magnetosphere* — the README's
  "planetary magnetospheres" describes **Kaiju**, the parent suite, and Kaiju's entry records those
  regions. Kaipy exports planetary constants in `kaipy/kdefs.py` (`SaturnM0g`, `RSaturnXE`,
  `JupiterM0g`, `RJupiterXE`, `MercuryM0g`, `RMercuryXE`, `NeptuneM0g`, `RNeptuneXE`), but a search
  for those symbol names across the tracked `.py` files finds them only in `kdefs.py` itself and in
  `tests/test_kdefs.py` — no planetary reader, grid, plot or script uses them. A user filtering for
  Jupiter software would find a terrestrial magnetosphere toolkit that happens to define Jupiter's
  dipole moment, which is not a good result. The contrary reading — that the constants are a genuine
  public API and therefore earn `Planetary Magnetospheres` — is recorded as the strongest available
  case for the value, and was not selected.
- *Corona*, *Solar Environment*, *Photosphere*, *Chromosphere*, *Solar Interior* — `corona` returns 0
  files over the tracked `.py` set. A case-insensitive search for `CME|coronal mass` over
  `'*.py' '*.rst' '*.md'` matches 9 files, and the composition of that 9 is not the uniform result an
  earlier extraction recorded: 5 of the files contain the RCM function name `RCMEq`, 3 contain none
  of it and match only the substring `cme` inside the unrelated RCM variable name `rcmeeta`, and the
  ninth — `kaipy/scripts/OHelio/ih2oh.py:79` — is a genuine CME comment sitting above a commented-out
  call. Field 22 gives the breakdown file by file and explains why that ninth match still earns
  neither a coronal region nor a CME phenomenon. The
  gamhelio domain starts at 21.5 solar radii, above the corona; Kaipy reads WSA coronal-model FITS
  output only to set that inner boundary, which is a boundary condition, not a coronal analysis
  capability.
- *Heliosheath* — the outer-heliosphere case is documented as "#for 1-10 au helio", far inside the
  termination shock.

### 6. Authors (MANDATORY)

**Recorded authors (13).** Twelve come from `CITATION.cff` at the pin, which is also exactly the
creator list of the Zenodo 1.1.4 deposit, with matching ORCIDs and affiliations. The thirteenth,
Darren De Zeeuw, is already stored in HSSI and is retained by the union rule — no author is ever
dropped in a refresh.

| # | Name | ORCID | Affiliation(s) |
|---|---|---|---|
| 1 | Michael J. Wiltberger | https://orcid.org/0000-0002-4844-3148 | NSF National Center for Atmospheric Research (https://ror.org/05cvfcr44); NSF NCAR High Altitude Observatory (https://ror.org/03773p874) |
| 2 | Shanshan Bao | https://orcid.org/0000-0002-5209-3988 | Rice University (https://ror.org/008zs3103) |
| 3 | Jeffery Garretson | https://orcid.org/0000-0003-3805-9860 | Johns Hopkins University Applied Physics Laboratory (https://ror.org/029pp9z10) |
| 4 | Andrew McCubbin | https://orcid.org/0000-0002-6222-3627 | Johns Hopkins University Applied Physics Laboratory (https://ror.org/029pp9z10) |
| 5 | Slava Merkin | https://orcid.org/0000-0003-4344-5424 | Johns Hopkins University Applied Physics Laboratory (https://ror.org/029pp9z10) |
| 6 | Adam Michael | https://orcid.org/0000-0003-2227-1242 | Johns Hopkins University Applied Physics Laboratory (https://ror.org/029pp9z10) |
| 7 | Kevin H. Pham | https://orcid.org/0000-0001-5031-5519 | NSF National Center for Atmospheric Research (https://ror.org/05cvfcr44); NSF NCAR High Altitude Observatory (https://ror.org/03773p874) |
| 8 | Elena Provornikova | https://orcid.org/0000-0001-8875-7478 | Johns Hopkins University Applied Physics Laboratory (https://ror.org/029pp9z10) |
| 9 | Nikhil Rao | https://orcid.org/0000-0003-2639-9892 | NSF National Center for Atmospheric Research (https://ror.org/05cvfcr44); NSF NCAR High Altitude Observatory (https://ror.org/03773p874) |
| 10 | Anthony Sciola | https://orcid.org/0000-0002-9752-9618 | Johns Hopkins University Applied Physics Laboratory (https://ror.org/029pp9z10) |
| 11 | Kareem Sorathia | https://orcid.org/0000-0002-6011-5470 | Johns Hopkins University Applied Physics Laboratory (https://ror.org/029pp9z10) |
| 12 | Eric Winter | https://orcid.org/0000-0001-5226-2107 | Johns Hopkins University Applied Physics Laboratory (https://ror.org/029pp9z10) |
| 13 | Darren De Zeeuw | https://orcid.org/0000-0002-4313-5998 | Calvin University (https://ror.org/05r0q9p84); Goddard Space Flight Center (https://ror.org/0171mag52); National Aeronautics and Space Administration (https://ror.org/027ka1x80); University of Michigan (https://ror.org/00jmfr291) |

The names, ORCIDs and affiliations for authors 1–12 come from `CITATION.cff` at the pin, with two
deliberate departures. The given names follow the identified Person records already in HSSI, which
carry the fuller forms "Michael J." and "Kevin H." where `CITATION.cff` writes "Michael" and
"Kevin". And where `CITATION.cff` gives a single affiliation, the stored record's second affiliation
is kept alongside it: it names only "NSF National Center for Atmospheric Research" for Wiltberger,
Pham and Rao, while their Person records also carry NSF NCAR High Altitude Observatory, and the
union rule keeps both rather than trimming to the narrower source. Author 13's four affiliations are the ones already stored for him; they are preserved rather
than trimmed, because the union rule applies to affiliations as well as to authors.

**Six authors were absent from the stored record before this refresh** — Garretson, Merkin, Michael,
Pham, Provornikova and Sorathia. They are named in the repository's own `CITATION.cff` and in the
authoritative Zenodo 1.1.4 deposit, and each already has an identified Person record with the right
ORCID and affiliation, so their absence was a gap rather than a judgement.

**Darren De Zeeuw is retained even though he is not in `CITATION.cff`.** He is a real contributor:
commit `6ba3da3` ("Enable rotation of the colorbar for GAMERA slice plots") is his, merged through
the repository's first external pull request, and the Zenodo 1.1.3 deposit lists him as a creator.
Whether the project chooses to add him to `CITATION.cff` is theirs to decide; dropping him from HSSI
because a later `CITATION.cff` omits him would be a silent removal of a credited contributor.

**The stored "Michael Wiltbeger" label could not be corrected by a metadata update, and this refresh
did not try.** Before this refresh, the record's Wiltberger author link pointed at an identifier-less
Person row spelled **Wiltbeger** (transposed letters), affiliated to NSF National Center for
Atmospheric Research. The correctly spelled row — Michael J. Wiltberger, ORCID
`0000-0002-4844-3148`, affiliated to both NSF NCAR and NSF NCAR High Altitude Observatory — existed
separately and was already the row the Kaiju and TIEGCM v3.0 entries used, so the misspelling was
specific to this entry's link rather than a shared label those entries depend on.

**Why sending metadata could never have repaired that label, recorded so a later refresh does not
re-attempt it.** A metadata update never *renames* an existing Person: once an author is matched to a
stored row, only a blank given or family name is filled in, and a name already present is left
untouched. Sending the correct spelling would therefore have changed nothing on the misspelled row.
The route to the correct label was never to repair that row through metadata, but to stop pointing at
it — the identified row listed as author 1 above was always the correct target state.

**What this refresh did instead, and how the misspelled row ended.** The author list carries each
author's ORCID. An author carrying an identifier is matched on that identifier alone — the stored
name plays no part in finding the row — so each of the thirteen resolved to the Person row that
already holds their ORCID. All thirteen of those rows hold both a given and a family name, so this
refresh created no Person row and overwrote no name. Kaipy's Wiltberger link accordingly moved to the
correctly spelled identified row (`Michael J. Wiltberger`, ORCID
`https://orcid.org/0000-0002-4844-3148`), while the misspelled `Michael Wiltbeger` row — which
carried no identifier — could not be selected by that path at all, so it lost its Kaipy link and was
left attached to no software. It was then removed on 2026-09-05 by a direct database correction,
together with its single affiliation link to NSF National Center for Atmospheric Research. The
catalogue now holds exactly one Wiltberger Person row, the identified one, which Kaipy, Kaiju and
TIEGCM v3.0 all use; no correction to these author rows remains outstanding.

**The genuine minting hazard, stated precisely, so this warning stays true instead of overbroad.** A
new Person row is created only when the identifier sent is one that *no* stored row carries yet.
Sending an ORCID is not by itself hazardous — an ORCID already present on a row resolves to that row
and writes nothing. What a future refresh must avoid is introducing a Wiltberger ORCID that HSSI does
not already hold, which is what would quietly create a duplicate Wiltberger row alongside the
identified one. Sending the ORCID recorded above does the opposite: it is the mechanism that binds
this entry to the correct row. (An author sent with *no* identifier is matched instead on an exact
given-and-family-name pair and created when none matches, which is the path by which a misspelling
can acquire a row of its own.)

**One consequence worth knowing when comparing sources later.** Because a populated name is never
renamed, the stored given names persist through this refresh exactly as they already stood — notably
`Kevin H.` where `CITATION.cff` writes `Kevin`. A later comparison that finds the two disagreeing is
seeing correct behaviour, not a failed update.

**Where the seed's author list came from, and why it is not used.** A 2025 extraction recorded twelve
authors including `vmerkin`, `Jeff`, `phamkh`, `atmichael18` and `ksorat`, with no ORCIDs. Those are
GitHub usernames: they are the creator list of the **Zenodo 1.1.3** deposit, which Zenodo built from
GitHub account names before the project added `CITATION.cff`. `CITATION.cff` was added in this
release cycle for exactly that reason — commit `f9277f6` "Add citation file for author list on
Zenodo" and `6f06e90` "Adds citation file to generate authors for Zenodo DOIs" — and the 1.1.4
deposit shows it worked. The username forms are superseded and must not be reintroduced.

### 7. Software Name (MANDATORY)
**Kaipy**

Capitalised. This is the form the project uses in prose everywhere: `CITATION.cff` `title: "Kaipy:
Python package for analysis and visualization of MAGE and space weather modeling data"`, the README's
opening sentence, `docs/source/conf.py` `project = 'Kaipy'`, and all four GitHub release names
(`Kaipy 1.1.4`, `Kaipy 1.1.3`, `kaipy-1.1.2`, `kaipy-1.1.1` — the two older ones use the tag form).
The lower-case `kaipy` in `pyproject.toml` and on PyPI is the distribution name, which is
conventionally lower-cased and is not the software's display name. A prior extraction recorded
`kaipy`; the stored capitalised form is better and is kept.

### 8. Description (MANDATORY)

Kaipy is a Python package for analysis and visualization of simulation results from a scientific software package Kaiju. Kaiju includes the Multiscale Atmosphere-Geospace Environment (MAGE) model developed by the NASA DRIVE Center for Geospace Storms as well as other scientific software for simulation of heliospheric environments such as planetary magnetospheres and the solar wind.

This is the project's own description, taken from `README.md` at the pin with the Markdown link
syntax removed and the hard line wraps joined. The identical text appears in
`docs/source/index.rst`, in every GitHub release body, and in the Zenodo deposit description. It is
the authors' wording, and it is not rephrased here: a stylistic alternative would not be an
improvement, and editorial intent is preserved.

Note that the GitHub repository's own "About" blurb is a *shortened* variant that stops at
"heliospheric environments." — the full sentence in the README and the docs is the better source and
is what is recorded.

### 9. Concise Description (OPTIONAL)

Python package for analysis and visualization of Kaiju simulation results (MAGE model and other heliospheric environment models).

129 characters, within the 200-character limit. It is a faithful compression of Field 8 and reads
well as a search-result preview, which is the field's purpose. Retained as worded rather than
rewritten.

### 10. Publication Date (RECOMMENDED)

**2024-06-26**

The form defines this field as "Date of first broadcast/publication." and says it is "Used for the
initial version of the software." — so it wants the software's *first* public release, not its most
recent one.

2024-06-26 is the upload date of `kaipy-1.0.0-py3-none-any.whl` on PyPI, the first moment the package
was publicly installable under this name. The README directs users to install "via pip from
[https://pypi.org/project/kaipy/](PyPi)", so PyPI is the project's own distribution channel and its
first release there is the natural reading of "first publication".

**This replaces the 2025-09-30 the record held before this refresh.** That value is the Zenodo
publication date of version 1.1.3, an arbitrary mid-series release; it was in the record because DOI
autofill copies whichever version the DataCite lookup returned. It satisfies neither reading of the
field: it is not the first publication, and it was not the current one either (1.1.4 was published
2025-12-12). The form's "first publication" wording governs, which is what settles it in favour of
the PyPI 1.0.0 upload.

Alternatives considered:
- *2024-05-16*, the first commit in the pinned ancestry ("Initial commit", Michael Wiltberger) —
  rejected because that history was private on Bitbucket at the time and a commit is not a
  publication.
- *2025-06-11*, the GitHub repository creation date — rejected for the same reason plus a worse one:
  it post-dates the first PyPI release by a year, so it cannot be the first publication of anything.
- *2025-07-03*, the first Zenodo deposit (the concept DOI was minted alongside version 1.1.2) —
  rejected because it is the date the project began minting DOIs, roughly a year after the software
  was first published.
- *Leaving 2025-09-30* — rejected as described above.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

The form's rule is explicit: "For software where a DOI has been obtained through Zenodo (e.g.,
GitHub-Zenodo workflow), Zenodo is the correct entry." The `isSupplementTo` relation recorded under
Field 2 proves the GitHub–Zenodo workflow was used, so Zenodo — not GitHub — is right.

### 12. Version (RECOMMENDED)

- **Version Number:** v1.1.4
- **Version Date:** 2025-12-12
- **Version Description:** *(deliberately empty — see below)*
- **Version PID:** https://doi.org/10.5281/zenodo.17914543

**Why 1.1.4.** It is the pinned revision, it is a real annotated release (tag `kaipy-1.1.4`, GitHub
release "Kaipy 1.1.4" published 2025-12-12), and it has its own Zenodo version DOI. The `v` prefix
follows the `v1.1.3` convention this entry carried before the refresh; the underlying
`pyproject.toml` and
`CITATION.cff` both say `1.1.4` without a prefix, and the Zenodo record's `version` field says
`kaipy-1.1.4`, so the prefix is a display convention rather than a source value.

**Why the version date is 2025-12-12 and not 2025-12-03.** `CITATION.cff` at the pin says
`date-released: 2025-12-03`, but the tag, the GitHub release and the Zenodo deposit are all dated
2025-12-12 and the PyPI wheel was uploaded 2025-12-10. The `CITATION.cff` date was written before the
release actually happened and is stale by nine days; the three concurring release artefacts win.
**Recorded so a later refresh does not "correct" the date back to the CITATION.cff value.**

**The Version Description is deliberately empty, and that is the source-faithful choice.** The
GitHub release body for `kaipy-1.1.4` contains only the boilerplate package description and a compare
link — it states no changes at all — and neither `CITATION.cff` nor the Zenodo 1.1.4 deposit carries
a change list. Where the release record says nothing about what changed, asserting nothing is
asserting what the source says.

**Considered and not selected: a synthesised description built from the release range.** It was fully
derived, every clause was attributable to a named commit, and it is kept here in full so a later
refresh can see that it was available and declined rather than never produced. The candidate text
was:

> Adds the mageDash live MAGE run dashboard; adds a CITATION.cff author list so Zenodo DOIs carry
> real names and ORCIDs; adds mono/diffuse auroral precipitation plotting options to REMIX; fixes
> slimH5 copying of non-Step root groups; restores compatibility with both pyspedas 1.5 and 2.0.

The range `kaipy-1.1.3..kaipy-1.1.4` is a real ancestry range (confirmed by
`git merge-base --is-ancestor`) and contains 34 commits touching 18 files (+1419/−96). Clause by
clause:
- *mageDash dashboard* ← `671e487` "First version of dashboard, and updates to comparison plotting
  code", `8cad063` "First usable version of magedash", `db8dd45` "Adding dashboard requirements",
  `a0b57be` "Merged in dashboard (pull request #16)".
- *CITATION.cff author list* ← `f9277f6` "Add citation file for author list on Zenodo", `6f06e90`
  "Adds citation file to generate authors for Zenodo DOIs", `13a0ab9` "Citation update".
- *mono/diffuse precipitation plotting* ← `3c505d5` "Adding options to plot mono/diffuse on a
  linear/log green/blue colormap.", `8c3f052` "optimize eflux, nflux, and eavg limit in plotting.",
  `711770a` "Update contour line options."
- *slimH5 root groups* ← `606356c` "Updating slimH5 to properly copy root groups that are not Step
  (e.g. raiju's Grid group)".
- *pyspedas 1.5/2.0 compatibility* ← `c57cc76` "Compatibility with both pyspedas 1.5 and 2.0".

The case for the synthesis was that a searcher gets real information from a description where
otherwise there is none, and that every clause is checkable against a named commit. The case against,
which prevailed, is that a synthesis puts words in the project's mouth: on the rendered page the
sentence would read as the project's own release note while being a curator's reading of a commit
range, and a field describing a release is the wrong place for that when the release itself is
silent. The five clauses remain available above if a later refresh judges otherwise, and the commit
attributions mean it would not have to be re-derived.

**Why 1.1.4 replaces the v1.1.3 the record held before this refresh, rather than sitting alongside
it.** This field describes the current version of the software, and carrying two makes the entry
ambiguous. Nothing is lost by replacing — 1.1.3's number, date, PID and description are preserved in
this dossier immediately below. Replacing a version also leaves the superseded row orphaned in HSSI,
which has been accepted as normal behaviour for this platform and is not a reason to avoid the
change.

**Why not 1.1.5.** PyPI carries `kaipy-1.1.5-py3-none-any.whl` uploaded 2026-02-13, and the unmerged
branch `dev_h5concat` declares `version = "1.1.5"` in `pyproject.toml`. But there is no `kaipy-1.1.5`
tag, no GitHub release, no Zenodo deposit, and the code is not on `master` — recording it would point
the Version PID at nothing and would describe a state of the software that the repository's release
record does not acknowledge. 1.1.4 is the last version the project actually released. **Worth
revisiting at the next refresh if 1.1.5 gets tagged**, since the PyPI wheel shows the project is
already building it.

**The previously stored version, preserved for the record.** Number `v1.1.3`, release date
2025-09-30, PID `https://doi.org/10.5281/zenodo.17236774`, description
`First contribution from outside core development team.  Minor bug fixes.` (two spaces, as stored).
That description matches neither the name nor the body of any GitHub release, so it was checked
against the actual `kaipy-1.1.2..kaipy-1.1.3` range (a real ancestry range containing 4 commits and
changing 3 files, +11/−8). It is **not** inherited from the previous tag's notes — the 1.1.2 release
body has no changelog at all. Clause by clause:
- "First contribution from outside core development team." is **attributable**: the "## New Contributors" section of the 1.1.3
  release body, whose single entry begins "* @darrendezeeuw made their first contribution", commit `85f6611`
  "Merge pull request #1 from darrendezeeuw/master", and the branch name `external_contrib`.
- "Minor bug fixes." is **not attributable**: the only functional change in the range is `6ba3da3`,
  which threads a new optional `doVert=False` keyword through `plotPlane`, `plotXY` and `plotXZ` to
  allow a vertical colorbar. That is an added feature, not a bug fix.
So the superseded description was a mostly-attributable synthesis with one inaccurate clause —
worth knowing, but not itself the reason it was replaced, since the decision above replaces the whole
row regardless.

### 13. Programming Language (RECOMMENDED)
**Python 3.x**

**The criterion, settled once.** The form says this field holds "The computer programming languages
most important for the software" and instructs: "Select the most important languages (e.g., Python,
Fortran, C). This is not meant to be an exhaustive list." So the field catalogues the language the
software is *written in*, not every file type present in the repository. Every inclusion and every
exclusion below follows from that one criterion, so a future refresh does not have to re-argue it
construct by construct.

Kaipy is written in Python and nothing else. Of the 233 tracked paths at the pin, 172 are `.py`.
`pyproject.toml` declares `requires-python = ">=3.9,<3.13"`; `setup.py` classifies Python 3.10, 3.11
and 3.12; the installation guide says "We support using python 3.10 through python 3.12."

Nothing in the tree is a second implementation language. There is no Fortran, C, C++, IDL, MATLAB,
Julia, Java, JavaScript or TypeScript source: a filename search across the whole tracked tree for
`.f`, `.f90`, `.f95`, `.f03`, `.c`, `.cc`, `.cpp`, `.h`, `.hpp`, `.pro`, `.m`, `.jl`, `.java`, `.js`
and `.ts` returns no matches at all. The complete census of the 233 tracked paths is 172 `.py`, 17
`.rst`, 12 `.txt`, 4 `.md`, 4 `.png`, 3 `.json`, 3 `.pbs`, one each of `.gitignore`, `.yaml`, `.cff`,
`.in`, `.bat`, `.css`, `.config`, `.dat`, `.h5`, `.xml`, `.csh`, `.sh`, `.toml`, `.ini` and `.ipynb`,
and three extensionless files (`docs/Makefile`, `kaipy/rcm/dktable`, `kaipy/rcm/rcmlas1`). Not one of
the non-`.py` entries is an implementation language under the criterion above: the 3 `.pbs` and the
`.xml` are HPC job and model-input templates the package *generates*; `.sh` and `.csh` are the
`setupEnvironment` helpers that set shell variables; `.css` styles the docs while `docs/Makefile` and
`docs/make.bat` drive the Sphinx build; `.ipynb` is a test fixture; `.rst` and `.md` are prose; three
of the `.png` files are documentation figures and the fourth is the logo of Field 33; `.toml`,
`.cff`, `.ini`, `.in`, `.yaml` and `.gitignore` are packaging and repository configuration; and the
`.json`, `.config`, `.dat`, `.h5`, `dktable`, `rcmlas1` and `.txt` files are configuration, data
tables, notes and dependency lists.

`Python 2.x` is excluded by the declared floor of 3.9.

### 14. Reference Publication (OPTIONAL)
**Not found.**

There is no paper describing Kaipy. This is a settled conclusion, not an unsearched gap:
- `CITATION.cff` at the pin has no `preferred-citation` block — it points at the software's own DOI.
- The 37-line `README.md` has no citation section.
- The Zenodo deposits carry no `isDescribedBy`, `isSupplementedBy` or `Cites` relation to any
  article; the only related identifier is the `isSupplementTo` link back to the GitHub tag.
- A literature search over full text (`full:"kaipy"`) returns 14 records; the only one of
  `doctype` "software" is the Zenodo deposit itself, which is Field 2, and no article among them
  describes the package. `title:"kaipy"` returns exactly that one Zenodo record.

The nearest thing to a description of the package is a conference abstract, "Developing Python
Packages for Center for Geospace Storms Model Analysis and Cloud-Based Accessibility using ParaView
and JupyterLab" (Wiltberger, Smith, Winter, Sorathia, Merkin, Rodig; AGU Fall Meeting 2023; bibcode
`2023AGUFMSH33E3094W`), whose abstract states "We first discuss the design and implementation of the
Python package, kaipy, that facilitates the exploration and manipulation of CGS model data." It has
no DOI and an abstract is not a reference publication; it is carried into
Field 27 instead.

### 15. License (RECOMMENDED)
**BSD 3-Clause "New" or "Revised" License**

This is the exact controlled-vocabulary row name, including the straight double quotes around New and
Revised. The licence is stated consistently by five independent sources: `LICENSE.md` at the pin
carries the three-clause BSD text; `pyproject.toml` says `license = {text = "BSD 3-Clause"}`;
`CITATION.cff` says `license: "BSD-3-Clause"`; GitHub resolves the SPDX identifier as
`BSD-3-Clause`; and the Zenodo deposit records `{'id': 'bsd-3-clause'}`.

**Copyright holders**, recorded because they are the institutional record and bear on Field 25.
`LICENSE.md` opens with three lines:

    Copyright 2023 Johns Hopkins University Applied Physics Laboratory
    Copyright 2023 US National Science Foundation National Center for Atmospheric Research
    Copyright 2023 Rice University

and `docs/source/conf.py` says `copyright = '2023 - JHU/APL, NSF NCAR, and Rice University'`.

**A prior extraction recorded a "License URI" sub-value of `https://opensource.org/licenses/BSD-3-Clause`.
That is a defect, not a value to carry forward.** HSSI stores no per-software licence URI: the
software's licence is a foreign key to a shared licence row, and the URL lives on that shared row.
Writing a software-specific licence URI is not possible, and presenting one implies a field that does
not exist. The repository's `LICENSE.md` is the right thing to cite as evidence, which is what this
entry does.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Recorded keywords (19).** Stored spellings are lower-case; the site renders them title-cased, so
the values below are the stored forms and are what a later refresh should compare against.

Carried over from the record as it stood before this refresh (12): `2d graphics`, `cgs`,
`data analysis`, `geospace`, `hdf5`, `heliosphere`, `kaiju`, `mage`, `magnetosphere`, `plotting`,
`simulation`, `solar wind`.

Added (7): `space weather`, `geospace modeling`, `GAMERA`, `REMIX`, `magnetohydrodynamics`,
`ionosphere`, `model-data comparison`.

Removed (1): `local` — HSSI held it before this refresh, and it is deliberately not among the 19
recorded above.

**Where the retained ones come from.** `cgs`, `mage` and `kaiju` are the project's own
`pyproject.toml` keywords (`keywords = ["CGS", "MAGE", "KAIJU"]`); case differences are irrelevant
because keyword lookup is case-insensitive, so the stored lower-case spellings are correct as they
stand and must be sent verbatim. `geospace`, `2d graphics`, `plotting`, `hdf5` and `data analysis`
descend from the PyHC community registry entry (`_data/projects.yml`), which lists
`keywords: ["geospace","2D_graphics", "plotting", "hdf5", "local", "data_analysis", "specific"]`.
`magnetosphere`, `heliosphere`, `solar wind` and `simulation` are ordinary science terms well
supported by the code.

**Why `local` was removed.** Its provenance is established: it is a PyHC **registry filter tag**,
not a science keyword. In `_data/projects.yml` the tags `local`, `remote` and `web_service` form a
data-access-mode facet and `general`/`specific` form a scope facet, used to drive the PyHC site's
filters — the same file tags other projects `local`, `remote`, `csv`, `binary`, `general` and so on.
Stripped of that context and dropped into an HSSI keyword list, `local` tells a reader nothing about
Kaipy and, as a search term, would match this entry for a query that has nothing to do with it. The
form asks for "General science keywords relevant for the software (e.g., from the AGU Index List or
the UAT)", and `local` is not one. The companion tag `specific` from the same PyHC list was never
carried into HSSI, which is consistent with this reading. On the page it rendered as a bare "Local",
which tells a visitor nothing and is not a term anyone would search on with this software in mind.

**Why the seven were added.** All seven already exist as rows in the keyword vocabulary, so none of
them mints a new row.
- `space weather` and `geospace modeling` are the project's own words: `CITATION.cff` at the pin
  closes with a `keywords:` block listing `"space weather"`,
  `"MAGE"`, `"kaipy"` and `"geospace modeling"`, and the Zenodo 1.1.4 deposit carries the same four. This is a *newer and more authoritative* keyword statement than
  either `pyproject.toml` or the PyHC registry, and it postdates both.
- `GAMERA` and `REMIX` name the two Kaiju components with dedicated Kaipy subpackages
  (`kaipy/gamera/`, `kaipy/remix/`, both listed in `docs/source/package.rst`). They are how a MAGE
  user would actually search.
- `magnetohydrodynamics` is the physics of the model output Kaipy exists to analyse.
- `ionosphere` matches the REMIX capability recorded under Field 5.
- `model-data comparison` is the single best description of the `kaipy/satcomp/` subsystem and its
  six comparison CLIs; it is an existing vocabulary row and captures a capability no other field
  states in words.

**Considered and not added:**
- `kaipy` — it is in `CITATION.cff`'s keyword list, but no such vocabulary row exists, and a keyword
  identical to the software's own name adds nothing a name search would not already find. Adding it
  would mint a new row for no benefit.
- `RAIJU`, `CHIMP`, `WSA`, `GAMERA-helio`, `MHD`, `field-aligned currents`, `radiation belts`,
  `high performance computing`, `ionospheric electrodynamics` — all exist as rows and all have some
  support in the code, but the seven above already cover the same ground, and a keyword list long
  enough to restate the whole functionality list stops being a useful filter. Recorded here as
  reasonable future candidates rather than rejected outright.
- Removing `2d graphics`, `plotting`, `hdf5` and `data analysis` as redundant with Fields 4, 18 and
  19 was considered and rejected: they are meaningful English terms that help free-text search, they
  do no harm, and removing published values for tidiness alone is not worth an approval cycle.
  `local` is different in kind — it is not merely redundant, it is meaningless here.

### 17. Data Sources (OPTIONAL)

**Recorded values (3):** `CDAWeb`, `GFZ`, `Observatory/Mission-specific`.
`GFZ` was added by this refresh; HSSI held only `CDAWeb`, `HAPI` and `Observatory/Mission-specific`
before it.

**Removed (1):** `HAPI` — HSSI held it before this refresh, and it is deliberately not among the
three recorded above; the evidence is below.

- **CDAWeb** — the primary retrieval path. `from cdasws import CdasWs` and per-spacecraft queries in
  `kaipy/cdaweb_utils.py`, `kaipy/satcomp/scutils.py`, all three
  `kaipy/solarWind/` readers (`OMNI.py`, `SWPC.py`, `WIND.py`), `cda2wind.py`, two comparison scripts
  and three test modules. `git grep -Pil -- "cdasws" <pin> -- '*.py'` returns 12 of the 172 tracked
  `.py` files, and 17 tracked files overall once the dependency declarations are counted. `kaipy/solarWind/OMNI.py`'s
  class docstring says "Processes OMNI Solar Wind data from CDAweb [http://cdaweb.gsfc.nasa.gov/]."
- **GFZ** — `kaipy/scripts/preproc/cda2wind.py` imports `from gfz_client import
  GFZClient`, instantiates `client = GFZClient()` and calls
  `client.get_kp_index(starttime=t0Str, endtime=t1Str, index='Kp')` to fill the Kp series when the
  CDAWeb value is missing. `gfz-api-client` is a declared dependency in `pyproject.toml`,
  `requirements.txt`, `setup.py` and `docs/requirements.txt`. The `GFZ` vocabulary row has an empty
  identifier, like `AMDA`, `Madrigal` and `WDC`; that is a known property of those later additions
  and does not make the row unsafe to select.
- **Observatory/Mission-specific** — already recorded and well earned. `kaipy/satcomp/sc_cdasws_strs.json`
  (27 spacecraft) and `sc_helio.json` (5) hard-code per-spacecraft dataset identifiers, variable names
  and coordinate systems, and `kaipy/supermage.py` fetches station data through the SuperMAG API
  (`import supermag_api as smapi`). The form's instruction — "If observatory-specific, select
  'observatory-specific' and indicate the observatory/mission name in the Related Observatory field"
  — is exactly the pattern here, and Field 32 carries the names.

**Why `HAPI` was removed.** There is no HAPI support at the pin. `git grep -Fil -- "hapi" <pin>`,
run with no pathspec so that it covers **every tracked file**, returns no match and exits 1 — a true
negative rather than an empty result — while the control `git grep -Fil -- "cdasws" <pin>` over the
same tree returns 17 files, so the search is discriminating. Kaipy's data access is the CDAS REST web
service through `cdasws`, which is a different protocol from HAPI; `hapiclient` is not a dependency,
and the one PySPEDAS entry point Kaipy uses is the Kyoto Dst loader, not a HAPI reader. From the
searcher's side, a user filtering HSSI for HAPI-capable software would have been handed a package
that cannot speak HAPI, which is the misdirection the removal fixes.

**Considered and rejected:**
- `OMNIWeb` — Kaipy does read OMNI data, but it reads it from CDAWeb, not from the OMNIWeb service.
  Selecting `OMNIWeb` would name a service the software never contacts.
- `HTTP/HTTPS Directories` — `kaipy/solarWind/SWPC.py` builds daily filenames under
  `swpcdir = "https://sohoftp.nascom.nasa.gov/sdb/goes/ace/daily/"` and calls
  `urllib.request.urlretrieve(magstr,datestr + magpost)` on them. It is genuinely a directory-listing fetch, but it is a
  single code path and, as written at the pin, a broken one: `urllib` is not imported anywhere in
  `kaipy/solarWind/SWPC.py`, so `__downloadACE` would raise `NameError` on first call. Recording a
  data source the software cannot currently reach would mislead a searcher. **Worth re-checking at
  the next refresh** — if the missing import is fixed upstream, this becomes a valid value.
- `SSCWeb` — the configs use SSC-derived ephemeris *datasets* served through CDAWeb (identifiers such
  as `GOES13_EPHEMERIS_SSC`, `THA_OR_SSC`, `AC_OR_SSC`), but the software never calls the SSCWeb
  service itself. Searching the tracked tree for `sscweb` returns nothing.
- `Madrigal`, `AMDA`, `das2`, `VirES`, `WDC`, `TAP`, `The Virtual Solar Observatory.`,
  `S3/Cloud-aware`, `FTP/FTPS Directories`, `Other` — no supporting code.

### 18. Input File Formats (RECOMMENDED)

**Recorded values (7):** `HDF5`, `CDF`, `ascii`, `FITS`, `netCDF3/4`, `JSON`, `Other`.
`FITS`, `netCDF3/4` and `JSON` were added by this refresh; HSSI held only the other four beforehand.

- **HDF5** — the native format of the Kaiju model output Kaipy reads. `git grep -Pil -- "h5py|\.h5\b" <pin> -- '*.py'`
  returns 84 of the 172 tracked `.py` files.
- **CDF** — CDAWeb data arrive as CDF; `kaipy/satcomp/scutils.py` documents its query return type as
  "data (spacepy.pycdf.CDFCopy): Object containing data returned by the query, None if no results."
- **ascii** — `cda2wind.py` documents its plain-text solar wind input ("#Reads from ASCII file" with
  the column layout in the following comment); `kaipy/solarWind/SWPC.py` parses the SWPC daily text
  products `_ace_mag_1m.txt` and `_ace_swepam_1m.txt`; `kaipy/cmaps/` reads `cmDDiv.txt` and
  `cmMLT.txt`; `kaipy/rcm/` reads `enchan.dat`, `dktable` and `chorus_polynomial.txt`.
- **FITS** — `kaipy/scripts/preproc/wsa2gamera.py` states "This script converts a
  FITS file created by a WSA run to a HDF5 format" and sets `DESCRIPTION = "Convert WSA FITS output
  to gamhelio format."`; `kaipy/gamhelio/lib/wsa.py` uses `from astropy.io import fits` and calls
  `fits.open(wsa_file)` in three places. In the workflow Kaipy supports, this is how a GAMERA-helio run
  gets its inner boundary condition, so it is a first-class input format, not an incidental one.
- **netCDF3/4** — `kaipy/solarWind/SWPC.py` imports `netCDF4 as nc` and its
  `DSCOVRNC` class reads NOAA DSCOVR solar wind files, tagging the result
  `'Source': 'NOAA DSCOVR NetCDF File',`.
- **JSON** — `kaipy/satcomp/sc_cdasws_strs.json` and `sc_helio.json` are shipped
  configuration read at run time through `importlib.resources`, and `kaipy/kaijson.py` provides
  `load`/`loads` with a custom decode hook used to read back cached analysis products
  (`rcm_times.json`, `rcm_tkl.json`, `rcm_wedgetkl.json`, `rcm_eqlatlon.json`,
  `rcm_cumulFrac.json`). `git grep -Pil -- "\.json" <pin> -- '*.py'` returns 11 files.
- **Other** — already recorded; covers the XML model input decks read by `kaipy/kaixml.py` and
  `numSteps`, and the `.pbs`/`.config` inputs, for which the vocabulary has no rows.

Rejected: `csv` (`git grep -Pil -- "to_csv|read_csv|\.csv" <pin> -- '*.py'` returns 0 files),
`IDL.sav`, `Zarr`, `ISTP-Compliant` (Kaipy consumes ISTP-compliant CDFs from CDAWeb but implements
nothing ISTP-specific).

### 19. Output File Formats (RECOMMENDED)

**Recorded values (4):** `HDF5`, `JSON`, `ascii`, `Other`.
`JSON` and `ascii` were added by this refresh; HSSI held only `HDF5` and `Other` before it.

- **HDF5** — the main product format. `cda2wind` writes the Gamera `bcwind.h5` boundary file
  ("#Writes to HDF5 Gamera wind file"), `wsa2gamera` and `ih2oh` write gamhelio grids, `genLFM`
  generates an "LFM-style HDF-5 grid for Gamera", `slimh5`/`slimFL`/`pitmerge`/`embiggen*` write
  reduced or merged HDF5, and `kaipy/raiju/waveModel/genWM.py` `genh5` writes the wave model into
  `raijuconfig.h5`.
- **JSON** — `kaipy/kaijson.py` `dump`/`dumps` with a custom `json.JSONEncoder`
  that serialises datetimes and NumPy arrays; `kaipy/satcomp/scRCM.py` writes its computed products
  to named JSON caches through it.
- **ascii** — `kaipy/satcomp/scutils.py` writes plain-text model-versus-data error
  reports (`f.write(f'MAE: {MAE}\n')` and the same for MSE, RMSE, MAPE, RSE and PE); `kJobs.py` and
  `scutils.py` write PBS job scripts as text.
- **Other** — already recorded; covers XDMF/XML (`genXDMF`, `genmpiXDMF`, `block_genmpiXDMF`,
  `kaipy/kaixdmf.py`, `XMLGenerator`), the PNG figures written by `kaipy/kaiViz.py` `savePic`
  (`git grep -Pil -- "savefig" <pin> -- '*.py'` returns 7 files), and the MP4 movies written by `gamerrVid` and
  `heliomovie`. The vocabulary has no image or video rows, so `Other` is the correct home for those.

Rejected: `CDF` and `FITS` (read only, never written), `netCDF3/4` (the only netCDF-writing path is
the TIEGCM branch of `cda2wind`, which raises `Error:  Cannot currently produce TIEGCM output.`),
`csv`, `Zarr`, `IDL.sav`, `ISTP-Compliant`.

### 20. Operating System (RECOMMENDED)
**Operating System Independent**

Pure Python with no platform-specific code paths, no compiled extensions and no OS classifiers in
either `setup.py` or `pyproject.toml`.

Considered and rejected: narrowing to `Linux` and `Mac`. The evidence for narrowing is real but
insufficient — `docs/source/kaipy/installation.rst` gives Linux-only instructions (a
`Miniconda3-latest-Linux-x86_64.sh` installer, `Ctrl + Alt + T` "on Linux"), the Read the Docs build
runs `ubuntu-22.04`, `kaipy/scripts/` ships POSIX `setupEnvironment.sh` and `.csh` helpers, the HPC
tooling emits PBS scripts, and the movie and figure-trimming paths shell out to `ffmpeg` and
ImageMagick. But none of that is a platform *restriction*: `ffmpeg` and ImageMagick exist on all
three platforms, the shell helpers are optional conveniences, and the package itself is
`pip install`-able anywhere Python 3.9–3.12 runs. Kaiju, the Fortran suite, legitimately records
Linux and Mac because it must be compiled; Kaipy does not have that constraint.

### 21. CPU Architecture (RECOMMENDED)
**CPU Independent**

Pure Python, no architecture-specific requirements, no compiled artefacts.

Considered and rejected: `HPC or HEC`. Kaipy generates and submits PBS jobs for HPC clusters — which
is why `Servers and Environments: High Performance Computing` is recorded under Field 4 — but it does
not *require* HPC to run. This field describes what the software needs to execute on, and every
Kaipy capability works on a laptop. Kaiju records `HPC or HEC` because its simulations genuinely
need it; a searcher filtering for HPC-class software would be looking for the simulation, not its
plotting layer.

### 22. Related Phenomena (OPTIONAL)

**Recorded values (2):** `Solar Wind`, `Geomagnetic Storms`. HSSI held no value for this field
before this refresh, so both are additions.

The vocabulary is closed and flat — seven rows, no `Parent:Child` form — and anything not in it must
go to Keywords instead. The form defines the field as "The phenomena the software supports science
functionality for."

- **Solar Wind.** The whole `kaipy/solarWind/` package reads, filters and conditions solar wind
  measurements (`SolarWind.py`, `OMNI.py`, `WIND.py`, `SWPC.py`, `TimeSeries.py`, `swBCplots.py`);
  `swpic` plots them; `kaipy/gamhelio/` simulates the solar wind out to 1–10 AU; and
  `helioSatComp` compares modelled solar wind against ACE, STEREO, Parker Solar Probe and Solar
  Orbiter observations.
- **Geomagnetic Storms.** Kaipy is the analysis package of the NASA DRIVE **Center for Geospace
  Storms**, and it implements the standard storm diagnostics directly: `kaipy/raiju/dst.py` and the
  `dstpic`/`raijudst` CLIs compute and plot Dst; `kaipy/supermage.py` computes the SuperMAG ring
  current and auroral electrojet indices from simulation output;
  `kaipy/gamera/deltabViz.py` labels them `rStr = "Ring Current Indices [nT]\nSMR       = %8.2f\nDawn-Dusk = %8.2f\nDay-Night = %8.2f" % (`
  and `aStr = "Auroral Indices [nT]\nSME = %8.2f\nSML = %8.2f\nSMU = %8.2f" % (SME, SML, SMU)`;
  and `run_ground_deltaB_analysis` plus `run_calcdb` compute ground magnetic perturbations, the
  quantity that matters for storm-driven geomagnetically induced currents.

  **The inferential step, stated rather than hidden.** Kaipy never names the phenomenon in its own
  words: `git grep -PIil -- "storm" <pin>`, over the whole tracked tree, returns two files —
  `README.md` and `docs/source/index.rst` — and in both the match is the centre's name, "Center for
  Geospace Storms", not a description of what the software studies. So the value rests on what the
  package computes rather than on what it calls itself: Dst, SMR, and the auroral electrojet indices
  are the standard storm diagnostics, and a package that computes all of them for a global geospace
  simulation supports storm science whether or not it says so. Asked from the searcher's side,
  someone browsing software for geomagnetic storms would be glad to find the analysis layer of the
  Center for Geospace Storms' own model. The contrary reading — that a phenomenon should be recorded
  only where the software names it — is the stricter standard, and it was not adopted, because it
  would leave this field empty for a package built to study exactly this phenomenon.

**Considered and rejected:**
- *Coronal Mass Ejections* — there is no live CME code at the pin, but the earlier reading of the
  evidence was wrong and the corrected reading is worth having in full. A case-insensitive search for
  `CME|coronal mass` over the tracked `.py`, `.rst` and `.md` files matches 9 files. An earlier
  extraction recorded that every one of those matches was the RCM function name `RCMEq`; that is
  false. The true composition is:
  - **Five files contain `RCMEq`** — `kaipy/gamera/rcmpp.py` (3 occurrences),
    `kaipy/satcomp/scRCM.py` (1), `kaipy/scripts/datamodel/rcm_rbsp_satcomp.py` (3),
    `kaipy/scripts/quicklook/rcmpic.py` (1) and `tests/gamera/test_rcmpp.py` (9). Even within those
    five the matches are not uniformly `RCMEq`: `scRCM.py` and `rcm_rbsp_satcomp.py` also match on
    other `rcm`-prefixed identifiers such as `rcmEGrid`, `rcme_lower` and `rcmeeta`.
  - **Three files contain no `RCMEq` at all** and match only the substring `cme` inside the unrelated
    variable name `rcmeeta`: `kaipy/scripts/postproc/embiggenRCM.py:92`
    (`kh5.getDims(fIn,"rcmeeta")`), `kaipy/scripts/postproc/genXDMF.py:154` (the `-rcmv` argument
    help text, which lists `rcmeeta` among the RCM variable names a user may request) and
    `kaipy/scripts/quicklook/rcmDataProbe.py:124` (`kh5.PullVar(fIn,"rcmeeta",nStp)`).
  - **One file is a genuine CME reference** — `kaipy/scripts/OHelio/ih2oh.py:79`, the comment
    `#to generate non-uniform grid for GL cme (more fine in region 0.1-0.3 AU)` (the source line ends
    with a trailing space), sitting immediately above a commented-out
    `#X3,Y3,Z3 = gg.GenKSphNonUGL(Ni=Ni,Nj=Nj,Nk=Nk,Rin=Rin,Rout=Rout,tMin=tMin,tMax=tMax)` at line
    80. The live call is the uniform-grid
    `X3,Y3,Z3 = gg.GenKSph(Ni=Ni,Nj=Nj,Nk=Nk,Rin=Rin,Rout=Rout,tMin=tMin,tMax=tMax)` on line 77.
  The flag belongs with the count: the 9 is over `'*.py' '*.rst' '*.md'`. Run with no pathspec and no
  `-I`, the same pattern returns 12, because `docs/source/_static/ionExample.png`,
  `docs/source/_static/kaipy-logo.png` and `kaipy/rcm/wmutils/DWang_chorus_lifetime.h5` contain the
  byte sequence inside binary data.
  The value is still not recorded. Kaiju's entry carries it because Kaiju's solar wind driving can
  inject CMEs; Kaipy has not earned it. **Recorded so a later refresh neither adds the value from the
  case-insensitive match nor re-asserts that the match is uniformly `RCMEq`.**
- *`GenKSphNonUGL` as the reason to add Coronal Mass Ejections* — considered and rejected, because
  the capability is dead code. The function is real, not a stale name:
  `kaipy/gamera/gamGrids.py:429` defines
  `def GenKSphNonUGL(Ni=Ni0,Nj=Nj0,Nk=Nk0,Rin=5,Rout=40,tMin=0.2,tMax=0.8):`, a radially non-uniform
  spherical grid generator, and `tests/gamera/test_gamGrids.py` imports it at line 9 and exercises it
  at lines 56-57. The `GL` is plausibly Gibson-Low flux-rope CME initialisation, which is what the
  `ih2oh.py` comment beside it says the grid refinement is for. But its only non-test call site
  anywhere in the tree is that commented-out line, so no shipped code path builds a CME-refined grid.
  A user filtering HSSI for CME software would reach a package whose sole CME-specific capability is
  switched off in source, which is why the phenomenon is not recorded on the strength of it.
  **Recorded because this lead looks stronger than it is, and a later refresh should not have to
  re-trace it.**
- *Coronal Heating*, *Solar Corona*, *Solar Flares*, *X-ray emission* — no supporting code, and the
  gamhelio domain begins above the corona at 21.5 solar radii.

### 23. Development Status (RECOMMENDED)
**Active**

This field held no value before this refresh, so any value here is an addition.

The two candidate definitions, quoted from the vocabulary rows themselves:
- **Active** — "The project has reached a stable, usable state and is being actively developed."
- **Inactive** — "The project has reached a stable, usable state but is no longer being actively
  developed; support/maintenance will be provided as time allows."

Both halves of "stable, usable" are satisfied either way: fourteen PyPI releases since 2024-06-26,
four tagged GitHub releases, three Zenodo deposits, published documentation and a test suite.

The question is whether development is ongoing. The evidence cuts both ways and is set out in full,
because the answer was not obvious from either side alone.

*What carried the decision.* `kaipy 1.1.5` was uploaded to PyPI on 2026-02-13, a real release two
months into the current year. The branch `dev_h5concat` carries work through 2026-03-30 and already declares
`version = "1.1.5"`. The repository was last pushed 2026-03-30 and its metadata was last touched
2026-06-02. It is not archived and has three open issues, so it is neither closed nor abandoned by
its maintainers.

*Considered and not determinative — the case for Inactive.* `master` has had no commit since
2025-12-12: 463 commits in the pinned ancestry, 213 in 2024, 250 in 2025 and **zero in 2026**. The
last tagged release is 1.1.4, from December 2025, and nothing had been pushed anywhere in the
repository for five months as of this extraction. That is a real signal and it is kept on the record
rather than dismissed — a later refresh should be able to see that the quiet `master` branch was
known and weighed, not overlooked.

**Active is recorded**, because the definitions turn on whether the project is being developed, not
on where that development has landed: a project that shipped a release and pushed branch work in the
current year is being developed, whatever its default branch shows. There is also no maintainer
statement of reduced support, no archive flag and no deprecation notice, which is what `Inactive`
describes, and a five-month quiet spell on a research-group package is unremarkable. From the
searcher's side, presenting Kaipy as no longer developed would be the more misleading of the two.

**What would change this.** `master` going another release cycle without a merge, with no new PyPI
upload and no branch activity, would move the balance to `Inactive`. The next refresh should re-check
the branch tips and the PyPI upload dates rather than assuming this conclusion still holds.

### 24. Documentation (RECOMMENDED)
https://kaipy-docs.readthedocs.io/en/latest/

Confirmed reachable. `README.md` at the pin links it as "Current documentation for this package
available via our [Read The Docs website](https://kaipy-docs.readthedocs.io/en/latest/)." and the
PyHC community registry records `docs: "https://kaipy-docs.readthedocs.io/"`. The site is built from
`docs/source/` by Sphinx with the `sphinx_rtd_theme` and `sphinxcontrib.autoprogram`, configured by
`.readthedocs.yaml`, and it covers installation, requirements, usage, the command-line scripts and
the full package API.

The `/en/latest/` form is preferred over the bare `https://kaipy-docs.readthedocs.io/` because it is
the URL the project itself publishes in its README and it resolves without a redirect.

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

HSSI held no value for this field before this refresh. The value rests on a two-link chain rather
than on a single funding statement, so the chain is set out here in full, with the weakness named, so
that a later refresh can judge it on the same evidence instead of re-deriving it.

The repository itself contains no funding statement: there is no acknowledgements section, no
`NOTICE`, no funding line in `README.md` or `CITATION.cff`, and the Zenodo deposits carry
`grants: None`. So the case rests on external sources.

*The chain, and the source that carries both of its links.* The peer-reviewed, open-access paper
"Center for geospace storms graduate student workshop" (Keesee, Merkin, Wiltberger, Hale, Winter and
Rao; https://doi.org/10.3389/fspas.2025.1663738 — four of its six authors are Kaipy authors) asserts
both halves in the same document:
- **Kaipy is CGS's package.** Its body states "Instruction then focused on installing and using the
  kaipy Python package—developed by CGS for visualization and analysis of MAGE results".
- **CGS is funded by NASA under this award.** Its funding statement states "This work was supported
  by NASA DRIVE Science Center for Geospace Storms (CGS) under award #80NSSC22M0163."

That both links come from one peer-reviewed source, rather than from two sources joined together by
this dossier, is what makes the chain worth recording: the connection is asserted by the paper's own
authors — four of whom are Kaipy authors — not constructed here.

It is independently corroborated on both sides. The AGU 2023 abstract `2023AGUFMSH33E3094W`, authored
by six CGS members including four Kaipy authors, states "We first discuss the design and
implementation of the Python package, kaipy, that facilitates the exploration and manipulation of CGS
model data."; the AGU 2025 abstract `2025AGUFMSM33D2439W` says "a suite of tools for analysis and
visualization—packaged in the Kaipy Python library—has also been released to support community
research"; and Kaipy's own README describes MAGE as developed by the NASA DRIVE Center for Geospace
Storms, linking the centre's site. On the award side, an acknowledgements-field search finds 85
papers acknowledging `80NSSC22M0163`, of which 72 also acknowledge "Center for Geospace Storms", so
the number is the CGS award rather than a coincidental match; a nonsense control token returns zero,
so that search is discriminating.

*The weakness, stated plainly.* **No source found says this award funded Kaipy itself.** The sources
say the award funds the Center, and separate sources say the Center produced Kaipy. The inference
from
"NASA funds the Center" to "NASA funds the Center's software" is this dossier's, not any source's,
and a reader should treat the value as that inference rather than as a quoted fact.

*Why it is recorded anyway.* Asked from the searcher's side — would a user reading Kaipy's HSSI page
be glad to see NASA recorded as the funder? — the answer is clearly yes, and the alternative, an
empty funder field for a package that a NASA DRIVE center built and says it built, hides a true and
useful fact. **Considered and not determinative: the stricter standard that only an award naming the
software should be recorded.** That is a defensible rule, and it is the rule that rejects the NSF
cooperative agreement immediately below; it was not applied to NASA itself, because the package's
authorship by the funded Center is directly attested rather than inferred from an employment
relationship.

*What would re-open this.* Two things, in opposite directions:
- A direct funding statement in Kaipy's own repository or in one of its Zenodo deposits — an
  acknowledgements section, a `grants` entry, a funding line in `CITATION.cff` — would replace the
  chain with a primary source and should be adopted in preference to it.
- Evidence that Kaipy is funded separately from CGS, under a different award or by a different
  sponsor, would reverse the value rather than merely strengthen it. Nothing found so far points that
  way, but nothing rules it out either.

**Considered and rejected — the U.S. National Science Foundation** (ROR `https://ror.org/021nxhr62`).
`LICENSE.md` names "US National Science Foundation National Center for Atmospheric Research" as a
copyright holder, three of the twelve authors are NSF NCAR staff, and the Frontiers funding statement
also credits "the National Center for Atmospheric Research, which is a major facility sponsored by
the National Science Foundation under Cooperative Agreement No. 1852977." Rejected because that
cooperative agreement funds NCAR as a *facility* — it is the institutional home and employer of some
authors, not a grant supporting this package. Treating an employer's sponsor as the software's funder
is an inference, not a record. The same reasoning was applied to the sibling package gcmprocpy, and
applying it inconsistently across the two would be worse than applying it strictly to both.
**Recorded so a later refresh does not add NSF from the LICENSE copyright line.**

### 26. Award Title (OPTIONAL)
- **Award Title:** NASA DRIVE Science Center for Geospace Storms
- **Award Number:** 80NSSC22M0163

Recorded together with the funder in Field 25, whose evidence chain and stated weakness apply to
this field unchanged: an award cannot stand without its funder, so the two are recorded or omitted
together.

The title is the Center's name as the funding statement gives it: "NASA DRIVE Science Center for
Geospace Storms (CGS) under award #80NSSC22M0163". DRIVE Science Center awards are identified by
center name, and no more formal award title is published. It is 45 characters, well inside the
128-character limit that award titles are stored under.

**Considered and rejected — the NCAR project codes in the repository.** `kaipy/kJobs.py` sets
`aStr = "UJHB0010"` and `kaipy/satcomp/scutils.py` defines
`def genSatCompPbsScript(scId, fdir, cmd, account='P28100045'):`. These look like award identifiers
and are not: they are the `#PBS -A` account strings that charge compute time to an NCAR HPC
allocation. `P28100045` is the same code the sibling package gcmprocpy carries in its own batch
scripts, which confirms the reading — it identifies a shared machine allocation, not a grant to
either package. **Recorded so a later refresh does not mistake them for award numbers.**

**Considered and rejected — `80NSSC20K0604`.** It appears in 60 papers' acknowledgements and
co-occurs with "Center for Geospace Storms" in two full texts, which makes it look like a candidate.
But the 60 are dominated by Parker Solar Probe and solar wind turbulence papers, which is the wrong
science for CGS; the co-occurrence is two papers acknowledging two different centres. It is a
different DRIVE center's award. **Recorded because the superficial evidence is genuinely misleading.**

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Recorded values (3).** HSSI held no value for this field before this refresh, so all three are
additions.

1. https://doi.org/10.3389/fspas.2025.1663738 — Keesee, Merkin, Wiltberger, Hale, Winter and Rao,
   "Center for geospace storms graduate student workshop", *Frontiers in Astronomy and Space
   Sciences* (2025). Open access. Four of its six authors are Kaipy authors. It describes teaching
   the package: "Instruction then focused on installing and using the kaipy Python package—developed
   by CGS for visualization and analysis of MAGE results" — the sentence carries a footnote marker
   there, and footnote 4 is `https://kaipy-docs.readthedocs.io/en/latest/`, which independently
   corroborates Field 24 — and "The students worked through a curated set of Jupyter notebooks, which
   introduced key functionality in kaipy for reading and plotting data fields."
2. https://doi.org/10.5281/zenodo.17427356 — De Zeeuw, Rastaetter, Kuznetsova, Wiltberger and Merkin,
   "Advanced Visualization Tools at the CCMC: Contributed and CCMC Developed" (2025-10-20). Three of
   its five authors are Kaipy authors or contributors. It records that Kaipy is being surfaced
   through CCMC: "An example of one such tool is kaipy from the Center for Geospace Storms (CGS)."
   That is a fact about the software's reach that appears nowhere else in the record.
3. https://ui.adsabs.harvard.edu/abs/2023AGUFMSH33E3094W/abstract — Wiltberger, Smith, Winter,
   Sorathia, Merkin and Rodig, "Developing Python Packages for Center for Geospace Storms Model
   Analysis and Cloud-Based Accessibility using ParaView and JupyterLab", AGU Fall Meeting 2023. This
   is the closest thing that exists to a paper *about* Kaipy — "We first discuss the design and
   implementation of the Python package, kaipy, that facilitates the exploration and manipulation of
   CGS model data." It has no DOI, so the ADS abstract permalink is used, which the form explicitly
   allows for a publication with no DOI. Note that this URL returns 405 to a plain command-line
   fetch; it renders normally in a browser, so a validator seeing that status should not treat it as
   broken.

**How these three were chosen, and what was left out.** The form defines the field as "Publications
that describe, cite, or use the software that the software developer prioritizes but are different
from the reference publication." Kaipy's own repository prioritises nothing — `CITATION.cff` has no
`preferred-citation` and the README has no citation section — so which publications the developers would
prioritise had to be inferred, and the criterion applied was: the publication must be *about* Kaipy in some
substantive way, and Kaipy's own authors must be behind it. All three pass; each is co-authored by
Kaipy authors and each says something about the package that the metadata does not otherwise record
(how it is taught, where it is served, how it was designed).

A full-text literature search (`full:"kaipy"`) returns 14 records. Of the eleven not listed above,
ten were rejected for the reasons below and the eleventh is the software's own Zenodo deposit:
- Five research papers that mention Kaipy only in passing while presenting MAGE science results —
  `2024GeoRL..5110772S`, `2023JGRA..12831923B`, `2025GeoRL..5217469S`, `2023JGRA..12831594S`,
  `2025JGRA..13033884L`. These *use* the software, but a Related Publications list that grows with
  every MAGE paper stops being a curated pointer and becomes a citation count; from the searcher's
  side, three publications that explain the software beat eleven that merely used it.
- Three further conference abstracts — `2025AMS...10549296W`, `2025AGUFMSH23G2637K`,
  `2025AGUFMSM33D2439W` — all of which mention Kaipy in one clause while being about MAGE science or
  CGS programmes. Only the 2023 abstract is substantially about the package itself.
- `2026SpWea..2404922C`, "Advancing Heliophysics and Space Weather Modeling Through Open Science" —
  a large community position paper in which Kaipy is one of many named examples.
- `1993JMoSt.295..113D`, an X-ray study of organic silicon compounds, which matched only because of
  an unrelated string in its text. Recorded because it is an instructive false positive from
  full-text search.

That eleventh record, the Zenodo deposit, is deliberately not listed here: it is the software's own
DOI and belongs in Field 2.

### 28. Related Datasets (OPTIONAL)
**Not found.**

This emptiness is a decision, not a gap. Kaipy reads a large, specific set of published datasets —
`kaipy/satcomp/sc_cdasws_strs.json` alone names CDAWeb dataset identifiers such as
`RBSP-A_MAGNETOMETER_1SEC-GSM_EMFISIS-L3`, `MMS1_FGM_SRVY_L2`, `THA_L2_FGM`, `C1_CP_FGM_SPIN`,
`DN_MAGN-L2-HIRES_G16` and `GE_K0_MGF`, and `sc_helio.json` names `AC_H2_SWE`, `AC_H2_MFI`,
`STA_COHO1HR_MERGED_MAG_PLASMA`, `PSP_COHO1HR_MERGED_MAG_PLASMA`, `SOLO_L2_MAG-RTN-NORMAL-1-MINUTE`
and `SOLO_L2_SWA-PAS-GRND-MOM`. Enumerating those as sixty-odd individual dataset entries would swamp
the entry and tell a reader less than the structural answer already given: the archive is recorded in
Field 17 (`CDAWeb`, `Observatory/Mission-specific`) and the missions and instruments in Fields 31 and
32.

No dataset DOI appears anywhere in the repository, in `CITATION.cff`, or in the Zenodo deposits, so
there is also no curated short list to draw on. **Recorded so a later refresh does not read the
emptiness as unexplored.** A later refresh that judges the individual datasets worth listing should
record them as hpde.io landing pages, which are the correct URL form for the CDAWeb datasets above.

### 29. Related Software (OPTIONAL)

**Recorded values (4):**
- https://github.com/JHUAPL/kaiju
- https://github.com/spacepy/spacepy
- https://github.com/sunpy/sunpy
- https://github.com/NCAR/gcmprocpy

All four URLs are reachable and all are within the 128-character limit that applies to these entries
(the longest is 34 characters).

- **Kaiju** (the most important single change in this field). Kaipy exists to
  read Kaiju's output; six of the ten subpackages listed in `docs/source/package.rst` are named for a
  Kaiju component (`kaipy.gamera`, `kaipy.gamhelio`, `kaipy.raiju`, `kaipy.rcm`, `kaipy.remix`,
  `kaipy.chimp`; the other four are `kaipy`, `kaipy.paraview`, `kaipy.satcomp` and
  `kaipy.solarWind`), and
  `kaipy/kJobs.py` and `XMLGenerator` write Kaiju's XML input decks and PBS job scripts. The relation
  is already asserted from the other side: the Kaiju entry names Kaipy in both its related and
  interoperable software, and Kaiju's own description ends "Users are encouraged to use the companion
  Kaipy package for analysis and visualization of Kaiju simulations." Kaipy naming Kaiju back was the
  most conspicuous omission in this record. Note that the repository URL is used rather than Kaiju's
  DOI, per the convention below.
- **SpacePy** (retained). A domain peer tool, not generic infrastructure, and the exchange is
  documented in Kaipy's public API: `kaipy/satcomp/scutils.py` declares its return type as
  "spacepy.datamodel.SpaceData: All of the spacecraft for the specified time range and cadence." and
  its query result as "data (spacepy.pycdf.CDFCopy): Object containing data returned by the query,
  None if no results."; `kaipy/transform.py` states "The few remaining routines only wrap spacepy."
  and is built on `spacepy.coordinates.Coords` and `spacepy.time.Ticktock`.
  `git grep -Pil -- "spacepy" <pin> -- '*.py'` returns 13 of the 172 tracked `.py` files.
- **SunPy** (retained). Also a domain peer tool. `from sunpy.coordinates import frames` appears in 5
  tracked `.py` files, and Kaipy's heliospheric trajectory and grid transforms are performed in
  SunPy's frames (`HeliocentricInertial`, `HeliographicStonyhurst`, `GeocentricSolarEcliptic`) —
  SunPy's coordinate data model is the one Kaipy adopts for that work.
- **GCMprocpy.** **The relation is programmatic, not import-level, and the record should say exactly
  that.** There is no code-level link whatever: `git grep -Pil -- "gcmprocpy" <pin>` returns no files
  across the whole tracked tree and exits 1, while the control `git grep -Pil -- "cdasws" <pin>` over
  the same tree returns 17 files, so the zero is a true negative and not a broken search. Nothing
  here implies a code dependency, and a later refresh should not go looking for one.

  What makes them related is that they are the Center for Geospace Storms' paired Python analysis
  packages — Kaipy for the MAGE magnetosphere side, GCMprocpy for the thermosphere/ionosphere side —
  and CGS's own developers say so. The abstract "Advancing Space Weather Research with kaipy and
  gcmprocpy: Analysis, Metrics, and Tutorials"
  (https://ams.confex.com/ams/106ANNUAL/meetingapp.cgi/Paper/470396), session 8.5 of the 106th AMS
  Annual Meeting, presented 2026-01-27 and co-authored by Michael Wiltberger (the presenter), Eric
  Winter, Slava Merkin and Nikhil Rao, opens:

  > The NASA DRIVE Center for Geospace Storms (CGS) has developed two complementary Python software
  > packages—kaipy and gcmprocpy—to advance space weather modeling, analysis, and validation.

  The em-dashes around "kaipy and gcmprocpy" are unspaced, as the page carries them; a spaced-dash
  rendering of this sentence is a transcription artefact and should not be propagated. The abstract
  goes on to divide the labour explicitly — kaipy for MAGE model output, gcmprocpy for TIEGCM and
  WACCM-X — which is the same split recorded above. All four presenters are among Kaipy's twelve
  `CITATION.cff` authors (Wiltberger at ORCID `0000-0002-4844-3148`, Merkin at `0000-0003-4344-5424`,
  Rao at `0000-0003-2639-9892` and Winter at `0000-0001-5226-2107`), so this is the package's own
  developers describing their own pair, not a third party's characterisation.

  Field 29 is for software performing *similar tasks* without necessarily linking together, which
  describes this pair exactly, and from the searcher's side a MAGE user who has found Kaipy would be
  glad to be pointed at its companion.

  **Considered and not determinative: that the whole case is a conference abstract.** A single
  non-peer-reviewed abstract is thinner evidence than this dossier accepts elsewhere, and on a
  stricter standard the entry would be left out. It did not prevail because the abstract is the
  developers' own joint statement about their own two packages, which is about as authoritative as a
  claim of companionship gets — and because the cost of being wrong is a
  pointer to a genuinely adjacent package, not a false capability claim.

  **The abstract is deliberately not carried into Field 27.** It has no DOI; it is not indexed in
  ADS, where a title search for "Advancing Space Weather Research with kaipy and gcmprocpy" returns
  0 records while the same query form returns exactly 1 for the AGU 2023 abstract's title
  (`2023AGUFMSH33E3094W`), so the zero is a real absence rather than a failed query; and the Confex
  program URL is a conference-program page rather than a persistent identifier. Reading it needs a
  browser — the page loads its program client-side, so a plain fetch returns only the loading
  shell.

**URL form.** These are recorded as repository URLs rather than DOIs on purpose. The catalogue
renders a related-software entry using the raw URL as the visible link text, so a DOI entry displays
as `https://doi.org/10.5281/zenodo.591887` — which tells a reader nothing — while a repository URL
displays as `https://github.com/sunpy/sunpy`, which they can recognise.

**This replaces the two values the record held as DOIs before this refresh.** The SunPy value was
the SunPy concept DOI `https://doi.org/10.5281/zenodo.591887` and the SpacePy value was
`https://doi.org/10.5281/zenodo.14268750`. The SpacePy one had a second and worse problem: it is a
*version* DOI, for release-0.6.0, not SpacePy's concept DOI
(https://doi.org/10.5281/zenodo.3252523), so as stored it asserted a relationship to one frozen
SpacePy release rather than to SpacePy. Both were replaced by the repository URLs above, which are
also the exact `code_repository_url` values of those packages' own HSSI entries, so the relations
point at the catalogue's own records and render as link text a reader recognises.

**Considered and not determinative: that a DOI is the more citable identifier.** A DOI is the more
durable thing to record in the abstract, and replacing published values is not free. It did not
prevail because this field's rendering is what a reader actually meets: the entry displays the raw
URL as its visible link text, so the more citable identifier is the less usable one here. The
superseded DOIs are kept above so a later refresh can see they were deliberate replacements rather
than losses.

**Considered and rejected, with reasons.** These are recorded in full because the temptation to list
a package's dependency tree here is the single most common error in this field, and a later refresh
should not have to re-reason it.
- *cdasws* — a REST client for one archive, not a peer science tool a user would combine with Kaipy.
  What it provides is already recorded, more usefully, as `CDAWeb` in Field 17. It has no HSSI entry.
- *supermag-api* and *gfz-api-client* — same reasoning: single-service client libraries. SuperMAG is
  recorded in Fields 31 and 32 and GFZ in Field 17, which is where a searcher would look.
- *astropy* — a Tier B package requiring cited evidence of a specific documented exchange. Kaipy uses
  `astropy.io.fits` to open WSA files, `astropy.units`, `astropy.time.Time` and
  `astropy.coordinates.SkyCoord`, but all of that is internal: the docstring `Args:` and
  `Returns:` sections name no astropy type, in contrast to the SpacePy case above where they name
  `spacepy.datamodel.SpaceData` and `spacepy.pycdf.CDFCopy` explicitly. Reading FITS is a file format, and it is recorded as
  one in Field 18. This is the internal-use case Tier B excludes; the guidance's own contrast is that
  "The public API returns `xarray.Dataset` objects as its documented interchange format" qualifies,
  while "uses xarray internally" does not.
- *h5py, netCDF4* — Tier B, and the same test fails. They are how Kaipy reads and writes HDF5 and
  netCDF, which Fields 18 and 19 already say.
- *numpy, scipy, pandas, matplotlib, cartopy, plotly, jupyterlab, pytest, alive_progress,
  progressbar, cmasher, configparser, slack_sdk, PyQt5, dash, dash_bootstrap_components,
  flask_caching, sphinx-rtd-theme, sphinxcontrib-autoprogram* — generic infrastructure. The
  guidance's own words are "Never list these (Tier A), no exceptions:", and for the ones not
  enumerated there the test is whether the package would be equally at home in a web app, a finance
  model or a biology pipeline. Every one of these passes that test, so all get Tier A treatment. That
  they appear in `pyproject.toml` is not an argument — it is the argument the guidance rejects.
- *geopack* — named in a `cda2wind.py` comment, "#Utilizes cdasws and geopack, make sure to install
  modules before running.", but never imported anywhere in the tree. The comment is stale (it also
  points at the old Bitbucket wiki). **Recorded so a later refresh does not add it from that
  comment.**
- *TIEGCM* — Kaiju's entry lists it and it is part of the MAGE coupled system, but Kaipy's only
  reference to it is the output format it explicitly cannot write: `Error:  Cannot currently produce
  TIEGCM output.` A user searching for TIEGCM software and finding Kaipy would be misled. **Recorded
  because the Kaiju entry's list makes this look like an obvious addition, and it is not.**
- *pyLTR* — named once, in the `#FIXME` beside that TIEGCM branch ("example code in
  pyLTR.SolarWind.Writer.TIEGCM"). It is plausibly a predecessor of `kaipy/solarWind/`, which would
  make it a legitimate Field 29 entry, but the repository says nothing to that effect and one FIXME
  reference is not a provenance claim. **Recorded as a genuinely open lead** — if the maintainers
  confirm the lineage, pyLTR belongs here.

### 30. Interoperable Software (OPTIONAL)

**Recorded values (4).** HSSI held no value for this field before this refresh, so all four were
added by it:
- https://github.com/JHUAPL/kaiju
- https://github.com/spacepy/spacepy
- https://github.com/spedas/pyspedas
- https://gitlab.kitware.com/paraview/paraview

The bar for this field is a *demonstrated exchange* — a shared or converted data model, output from
one imported into the other, an adapter API, or a plugin relationship — and not mere co-installation.
Each of the four clears it with a named artefact.

- **Kaiju.** Kaipy consumes Kaiju's HDF5 output and produces Kaiju's XML input decks; the two are
  designed as a pair, and the Kaiju entry already declares the relation in this direction.
- **SpacePy.** The interchange is in the public API, as quoted under Field 29: Kaipy's documented
  return and argument types are `spacepy.datamodel.SpaceData` and `spacepy.pycdf.CDFCopy`, so a user
  moves data between the two packages as objects, not as files.
- **PySPEDAS.** `kaipy/solarWind/OMNI.py` calls PySPEDAS's Kyoto loader and then reads the resulting
  tplot variable back: `dst_vars = kyoto.dst(trange=[startStr,endStr])` followed by
  `dat = get_data('kyoto_dst')`, with `from pytplot import get_data` at the top of the module and a
  version-tolerant import (`from pyspedas.projects import kyoto`, falling back to
  `from pyspedas import kyoto`). The docstring states the purpose: "Obtains DST values within the
  specified time range via pyspedas". This is the tplot-variable exchange the guidance names as its
  worked example of genuine interoperability, and the fact that a release was spent on
  "Compatibility with both pyspedas 1.5 and 2.0" (commit `c57cc76`) shows the project maintains the
  interface deliberately. Note that `pytplot` is not itself a declared dependency; it arrives with
  PySPEDAS, which is why PySPEDAS rather than PyTplot is the entry.
- **ParaView.** Kaipy ships a dedicated adapter package, `kaipy/paraview/`, documented as "Paraview
  Package" in `docs/source/package.rst`, whose `pvGam.py` and `pvutils.py` build ParaView pipelines
  through `import paraview.simple as pvs` — programmable filters that compute Alfvén and sound speeds
  and magnetosonic Mach number, time annotations, and VTK string arrays. Complementing that,
  `genXDMF`/`genmpiXDMF`/`block_genmpiXDMF` and `kaipy/kaixdmf.py` exist to write XDMF wrappers so
  ParaView can read Kaiju's HDF5 directly. That is an adapter API plus a format bridge — the
  strongest kind of evidence this field asks for. The AGU 2023 abstract confirms it was designed
  that way, describing the pairing of Kaipy with "ParaView and Trame, a web-based framework for
  visualization and analytics".

  **The argument against was weighed and judged not determinative; it was not refuted.** ParaView is
  general-purpose scientific visualization rather than a heliophysics peer tool, and at this refresh
  it had no HSSI catalogue entry of its own, so a reader following the relation leaves the catalogue.
  The counterweight is that the guidance's generic-infrastructure test asks whether a package would
  be equally at home in a web app, a finance model or a biology pipeline — ParaView would not — and
  that the exclusion the test drives is aimed at packages which are merely depended upon, whereas
  Kaipy ships a subpackage written for no purpose but to drive this one. The entry is recorded on
  that balance, with the objection standing as a real cost rather than as an error.

  **The recorded URL is ParaView's own source repository,**
  `https://gitlab.kitware.com/paraview/paraview` — 44 characters, well inside the 200-character limit
  of the stored field. With no catalogue entry of its own to point at, ParaView fell under this
  field's instruction to give a DOI or repository URL, and the repository is the more precise of the
  two. The
  project page `https://www.paraview.org` was considered and not selected: it is the project's front
  door rather than its code, and it identifies the software less exactly than the repository the
  software is built from.

**Considered and rejected:**
- *SunPy* — kept in Field 29 but not promoted here. Kaipy uses SunPy's coordinate frames internally
  to compute trajectories; the values that cross Kaipy's public API boundary are plain arrays, not
  SunPy objects, so there is no demonstrated two-way exchange. This is the distinction between using
  a library and interoperating with a tool.
- *GCMprocpy* — a companion package by association, with no data exchange of any kind at the pin.
  Field 29 is the right home for it.
- *JupyterLab* — a declared dependency and named in the AGU 2023 abstract, and there is a
  `tests/notebookfortest.ipynb`, but Kaipy provides no Jupyter extension, kernel, widget or
  `_repr_html_`; being usable from a notebook is true of essentially every Python package.
- Everything listed under Field 29's rejections applies here unchanged. In particular, a blanket
  claim of the form "part of the standard scientific Python ecosystem" or "a PyHC member, so it
  interoperates with PyHC packages" is never sufficient on its own, and Kaipy's PyHC community
  membership is therefore not used as an argument anywhere in this field.

### 31. Related Instruments (OPTIONAL)

**Recorded values (60).** HSSI held no value for this field before this refresh, so all sixty are
additions: `SuperMAG Magnetometers`, plus the 59 fleet rows for the instruments Kaipy's
satellite-comparison subsystem reads by name.

Every row below was resolved against the controlled vocabulary rather than typed. Each matches
exactly one instrument row (`type == 1`), none has an `.html` duplicate, and every identifier is
under `https://spase-metadata.org/`, so each is genuinely SPASE-backed. The names are copied verbatim
from the matched rows.

**Six of these names carry internal double spaces, and they are correct as written.**
`GOES Triaxial Fluxgate Magnetometer on GOES  8` has two spaces before the `8`, and the five
`THEMIS-<x>:  Solid State Telescope` names have two spaces after the colon. The vocabulary rows carry
those spaces, and the identifier is what binds, but a value whose whitespace has been "tidied" no
longer reads back as the row it was taken from. **Recorded because whitespace normalisation is an
easy and silent way to corrupt exactly these six.**

| Name (verbatim from the vocabulary row) | SPASE identifier |
|---|---|
| SuperMAG Magnetometers | https://spase-metadata.org/SMWG/Instrument/SuperMAG/Magnetometers |
| GOES Triaxial Fluxgate Magnetometer on GOES  8 | https://spase-metadata.org/SMWG/Instrument/GOES/8/MAG |
| GOES Triaxial Fluxgate Magnetometer on GOES 9 | https://spase-metadata.org/SMWG/Instrument/GOES/9/MAG |
| GOES Triaxial Fluxgate Magnetometer on GOES | https://spase-metadata.org/SMWG/Instrument/GOES/10/MAG |
| GOES Triaxial Fluxgate Magnetometer on GOES | https://spase-metadata.org/SMWG/Instrument/GOES/11/MAG |
| GOES Triaxial Fluxgate Magnetometer on GOES | https://spase-metadata.org/SMWG/Instrument/GOES/12/MAG |
| Triaxial Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/GOES/13/MAG |
| Triaxial Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/GOES/14/MAG |
| Triaxial Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/GOES/15/MAG |
| Triaxial Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/GOES/16/MAG |
| Triaxial Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/GOES/17/MAG |
| RBSP ECT | https://spase-metadata.org/SMWG/Instrument/RBSP/A/ECT |
| RBSP EMFISIS | https://spase-metadata.org/SMWG/Instrument/RBSP/A/EMFISIS |
| RBSP RBSPICE | https://spase-metadata.org/SMWG/Instrument/RBSP/A/RBSPICE |
| RBSP ECT | https://spase-metadata.org/SMWG/Instrument/RBSP/B/ECT |
| RBSP EMFISIS | https://spase-metadata.org/SMWG/Instrument/RBSP/B/EMFISIS |
| RBSP RBSPICE | https://spase-metadata.org/SMWG/Instrument/RBSP/B/RBSPICE |
| Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/FGM |
| Cluster Ion Spectrometry | https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/CIS |
| Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/FGM |
| Cluster Ion Spectrometry | https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/CIS |
| Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/FGM |
| Cluster Ion Spectrometry | https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/CIS |
| Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/FGM |
| Cluster Ion Spectrometry | https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/CIS |
| THEMIS-A Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/A/FGM |
| THEMIS-A Electrostatic Analyzers | https://spase-metadata.org/SMWG/Instrument/THEMIS/A/ESA |
| THEMIS-A:  Solid State Telescope | https://spase-metadata.org/SMWG/Instrument/THEMIS/A/SST |
| THEMIS-B Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/B/FGM |
| THEMIS-B Electrostatic Analyzers | https://spase-metadata.org/SMWG/Instrument/THEMIS/B/ESA |
| THEMIS-B:  Solid State Telescope | https://spase-metadata.org/SMWG/Instrument/THEMIS/B/SST |
| THEMIS-C Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/C/FGM |
| THEMIS-C Electrostatic Analyzers | https://spase-metadata.org/SMWG/Instrument/THEMIS/C/ESA |
| THEMIS-C:  Solid State Telescope | https://spase-metadata.org/SMWG/Instrument/THEMIS/C/SST |
| THEMIS-D Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/D/FGM |
| THEMIS-D Electrostatic Analyzers | https://spase-metadata.org/SMWG/Instrument/THEMIS/D/ESA |
| THEMIS-D:  Solid State Telescope | https://spase-metadata.org/SMWG/Instrument/THEMIS/D/SST |
| THEMIS-E Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/E/FGM |
| THEMIS-E Electrostatic Analyzers | https://spase-metadata.org/SMWG/Instrument/THEMIS/E/ESA |
| THEMIS-E:  Solid State Telescope | https://spase-metadata.org/SMWG/Instrument/THEMIS/E/SST |
| MGF on GEOTAIL | https://spase-metadata.org/SMWG/Instrument/Geotail/MGF |
| Geotail CPI | https://spase-metadata.org/SMWG/Instrument/Geotail/CPI |
| ACE Magnetic Field Instrument | https://spase-metadata.org/SMWG/Instrument/ACE/MAG |
| ACE Solar Wind Electron, Proton and Alpha Monitor | https://spase-metadata.org/SMWG/Instrument/ACE/SWEPAM |
| Wind Magnetic Field Investigation | https://spase-metadata.org/SMWG/Instrument/Wind/MFI |
| Wind Solar Wind Experiment | https://spase-metadata.org/SMWG/Instrument/Wind/SWE |
| MMS FIELDS/FGM | https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/FGM |
| MMS FPI/DIS | https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DIS |
| MMS Positions | https://spase-metadata.org/SMWG/Instrument/MMS/1/Ephemeris |
| MMS FIELDS/FGM | https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/FGM |
| MMS FPI/DIS | https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DIS |
| MMS Positions | https://spase-metadata.org/SMWG/Instrument/MMS/2/Ephemeris |
| MMS FIELDS/FGM | https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/FGM |
| MMS FPI/DIS | https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DIS |
| MMS Positions | https://spase-metadata.org/SMWG/Instrument/MMS/3/Ephemeris |
| MMS FIELDS/FGM | https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/FGM |
| MMS FPI/DIS | https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DIS |
| MMS Positions | https://spase-metadata.org/SMWG/Instrument/MMS/4/Ephemeris |
| Magnetometer | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/MAG |
| Proton-Alpha Sensor | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/PAS |

`kaipy/supermage.py` opens "# Functions to calculate Supermag indices from simulated outputs",
imports the SuperMAG client (`import supermag_api as smapi`), and provides `FetchSMData`,
`FetchSMIndices` and `doFetch` to retrieve station magnetometer data, then
`CalculateSMRBins`, `InterpolateSimData`, `SMContourPlotPrep`, `MakeContourPlots` and
`MakeIndicesPlot` to compare it against simulation output. The `supermag_comparison` and
`supermag_analysis` console scripts are its CLIs. This is instrument-specific data handling, and the
matching observatory row was already stored before this refresh, so recording the instrument
completes a pairing that was half-present.

**Why the other 59 are here too.**
`kaipy/satcomp/sc_cdasws_strs.json` (27 spacecraft entries) and `sc_helio.json` (5) hard-code CDAWeb
dataset identifiers that name specific instruments — EMFISIS, RBSPICE and ECT/HOPE on the Van Allen
Probes; FGM and CIS on Cluster; FGM, ESA and SST on THEMIS; FGM, FPI and MEC on MMS; MGF and CPI on
Geotail; and the GOES fluxgate magnetometers, whose eleven `GOES08`–`GOES18` entries are all
magnetometer datasets but in two families — nine use `DN_MAGN-L2-HIRES_G08`…`_G18` with variable
`b_gsm`, while `GOES11` and `GOES12` use the older `GOES11_K0_MAG` and `GOES12_K0_MAG` with variable
`B_GSM_c`. In `sc_helio.json`, ACE contributes MAG and SWEPAM (`AC_H2_MFI`, `AC_H2_SWE`) and Solar
Orbiter contributes MAG and SWA-PAS. Wind's two rows come from elsewhere and are evidenced
separately below. Each of these passes the "designed to support" test: the software knows the
instrument by dataset identifier, variable name and coordinate frame, not merely by the archive it
came from.

**A correction to an earlier pass, which is why the fleet is recorded at all.** An earlier pass
recorded that instrument rows were *absent* for MMS, Solar Orbiter, STEREO and Parker Solar Probe,
and used that unevenness as the reason to keep the fleet at observatory level. Four of its five
absence claims are false: they were artifacts of a search pattern that could see only the `SMWG`
naming authority and only one spelling of each mission name. Re-derived across every authority and
every spelling variant, the instrument-row (`type == 1`) counts are:

| Spacecraft | instrument rows | naming authorities |
|---|---|---|
| MMS | 94 | SMWG 52, CNES 42 |
| Parker Solar Probe | 37 | SMWG 25, CNES 12 |
| STEREO-A | 28 | SMWG 13, CNES 11, NASA 4 |
| STEREO-B | 28 | SMWG 13, CNES 11, NASA 4 |
| Solar Orbiter | 18 | CNES 10, ESA 5, SMWG 2, NASA 1 |
| Wind | 17 | SMWG 11, CNES 6 |
| Geotail | 16 | SMWG 9, CNES 7 |
| ACE | 14 | SMWG 10, CNES 4 |
| GOES-18 | 1 | NOAA 1 |

**The durable method lesson.** Any future Fields 31/32 search must sweep **every authority prefix**
(present in the vocabulary at this refresh: `SMWG`, `IUGONET`, `CNES`, `HamSCI`, `ASWS`, `ISWI`,
`NASA`, `NSF`, `ESA`, `NOAA`) and **every spelling variant** (`SolarOrbiter` / `Solar_Orbiter` /
`SolO`, `ParkerSolarProbe` / `PSP`, `MMS1` / `MMS-1`) **before recording an absence**, and must state
the pattern it actually ran beside any count it publishes. Two of the corrected figures show why: MMS
has **52** SMWG instrument rows, thirteen per spacecraft across all four, and Solar Orbiter's rows
exist in two spellings — eight under `SolarOrbiter` and ten under `Solar_Orbiter`. A bare substring
probe also over-counts in the other direction: Cassini's `MIMI-LEMMS` contains the letters `MMS`,
which is why the MMS figure is 94 and not 95.

**How each group in the table was matched to the configuration.** The 59 fleet rows break down as
follows; the shared `https://spase-metadata.org/` prefix is omitted from the path fragments here and
written out in full in the table above.
- **GOES 8–17 magnetometers** (10) — `SMWG/Instrument/GOES/8/MAG` through `SMWG/Instrument/GOES/17/MAG`.
- **Van Allen Probes** (6) — `SMWG/Instrument/RBSP/{A,B}/{ECT,EMFISIS,RBSPICE}`.
- **Cluster** (8) — `SMWG/Instrument/Cluster-{Rumba,Salsa,Samba,Tango}/{FGM,CIS}`.
- **THEMIS** (15) — `SMWG/Instrument/THEMIS/{A,B,C,D,E}/{FGM,ESA,SST}`.
- **Geotail** (2) — `SMWG/Instrument/Geotail/MGF` and `SMWG/Instrument/Geotail/CPI`.
- **ACE** (2) — `SMWG/Instrument/ACE/MAG` and `SMWG/Instrument/ACE/SWEPAM`.
- **Wind** (2) — `SMWG/Instrument/Wind/MFI` and `SMWG/Instrument/Wind/SWE`. **These two are not in
  either satcomp configuration**, which has no Wind entry at all; their evidence is
  `kaipy/solarWind/WIND.py`, whose reader takes a Wind SWE file and a Wind MFI file as its two data
  arguments (`def __init__(self, fSWE,fMFI,t0,t1,doFilter = False, sigmaVal = 3.0):`, documented as
  "fSWE (str): Filepath for the SWE data." and "fMFI (str): Filepath for the MFI data.") and filters
  and interpolates each stream separately. **Recorded because the `MFI` and `SWE` strings also occur
  in the configurations as parts of ACE's dataset identifiers `AC_H2_MFI` and `AC_H2_SWE`, which is
  an easy way to mis-attribute these two rows to a Wind config entry that does not exist.**
- **MMS** (12) — `SMWG/Instrument/MMS/{1,2,3,4}/FIELDS/FGM` (name `MMS FIELDS/FGM`),
  `SMWG/Instrument/MMS/{1,2,3,4}/FastPlasmaInstrument/DIS` (`MMS FPI/DIS`) and
  `SMWG/Instrument/MMS/{1,2,3,4}/Ephemeris` (`MMS Positions`). These match the configuration exactly:
  it requests `MMS1_FGM_SRVY_L2`, `MMS1_FPI_FAST_L2_DIS-MOMS` and `MMS1_MEC_SRVY_L2_EPHT89D`, and the
  same three per spacecraft for MMS2–4. The sibling `.../FastPlasmaInstrument/DES` rows exist too;
  Kaipy reads only the ion moments, so they are not listed.
- **Solar Orbiter** (2) — `CNES/Instrument/CDPP-AMDA/Solar_Orbiter/MAG` (name `Magnetometer`) and
  `CNES/Instrument/CDPP-AMDA/Solar_Orbiter/PAS` (name `Proton-Alpha Sensor`, the SWA-PAS sensor),
  matching the configuration's `SOLO_L2_MAG-RTN-NORMAL-1-MINUTE` and `SOLO_L2_SWA-PAS-GRND-MOM`. The
  sibling SWA sensors `EAS` (`Electron Analyser System`) and `HIS` (`Heavy Ion Sensor`) also have
  rows; Kaipy reads neither.

**The MMS MEC candidate, decided rather than left as a bare absence.** Across the whole
instrument/observatory vocabulary, no row carries `MEC` in its identifier, name or abbreviation, and
none carries `MEC` as a standalone token anywhere at all — pattern `(?<![A-Za-z])MEC(?![A-Za-z])`,
case-insensitive, run over identifier, name, abbreviation, definition and landing URL alike, 0 hits.
The letter sequence survives only as a fragment of longer words, in 166 definitions: case-folded,
`mechanism` 75, `mechanisms` 63, `mechanical` 38, `mechanically` 10, `mechanics` 6,
`electromechanical` 1, and twice a surname the rows spell `NEMECEK`. No candidate row is cited
because none matches, and nothing near-miss-shaped exists for a later refresh to go hunting after.
Kaipy requests `MMS1_MEC_SRVY_L2_EPHT89D` for spacecraft ephemeris and for the northern and southern
magnetic footprints (`mms1_mec_pfn_gsm`, `mms1_mec_pfs_gsm`), and the same per spacecraft. The four
`SMWG/Instrument/MMS/{n}/Ephemeris` rows, named `MMS Positions`, are the
vocabulary's representation of exactly that ephemeris function, so **the MEC use is carried by those
Ephemeris rows rather than left unrepresented** — which is why they appear in the list above. What
that does not capture is the T89D field-line mapping MEC also supplies; an ephemeris row is the
closest true statement the vocabulary permits, and minting a MEC row is not an option.

**What genuinely does not resolve** — two cases, and they are different in kind:
- **GOES-18's magnetometer.** The configuration reads `DN_MAGN-L2-HIRES_G18`, but GOES-18 has exactly
  one instrument row in the entire vocabulary, `https://spase-metadata.org/NOAA/Instrument/GOES/18/SUVI`,
  named "Solar Ultraviolet Imager" — an imager, not the magnetometer Kaipy reads. This is the one
  absence claim from the earlier pass that survived checking. Field 32's observatory row
  `https://spase-metadata.org/NOAA/Observatory/GOES/18` carries the association instead, which is the
  documented substitution the resolution ladder prescribes.
- **STEREO-A, STEREO-B and Parker Solar Probe — a mapping problem, not an absence.** All three have
  plentiful instrument rows (28, 28 and 37). But Kaipy reads none of those instruments' own products:
  `sc_helio.json` requests `STA_COHO1HR_MERGED_MAG_PLASMA`, `STB_COHO1HR_MERGED_MAG_PLASMA` and
  `PSP_COHO1HR_MERGED_MAG_PLASMA`, merged hourly magnetic-field-plus-plasma composites assembled from
  several instruments, with `STA_HELIO1DAY_POSITION` and `STB_HELIO1DAY_POSITION` for ephemeris. No
  single instrument row corresponds to what is retrieved, so naming one — `SMWG/Instrument/STEREO-A/IMPACT/MAG`,
  say — would assert a specificity the software does not have. The observatory level is the honest one
  for these three, and Field 32 records them there.

**A choice, not an absence: the archive-specific Solar Orbiter rows.** Solar Orbiter's MAG and PAS
resolve only under `CNES/Instrument/CDPP-AMDA/…`, the CDPP/AMDA archive's own instrument catalogue.
Whether such a row serves an HSSI visitor as well as an `SMWG` row is a fair question — the display
names are the generic `Magnetometer` and `Proton-Alpha Sensor`, and a visitor browsing Solar Orbiter
instruments is likelier to arrive from the ESA rows. But that is a reason to *choose*, never a basis
for saying the rows do not exist. **They are recorded**, because omitting them would leave Solar
Orbiter looking instrument-unsupported while Kaipy reads two of its instruments by name. Recorded as
a choice, so that a later refresh preferring ESA-authority rows can revisit it knowing the CNES rows
were selected deliberately and not fallen into.

**Why the full evidenced set rather than SuperMAG alone.** Each of the 59 fleet rows is
individually evidenced: 57 of them by a hard-coded dataset identifier, variable name and coordinate
frame in `sc_cdasws_strs.json` or `sc_helio.json`, and the two Wind rows by the per-instrument file
arguments of `kaipy/solarWind/WIND.py` — the same standard the per-spacecraft observatory rows in
Field 32 rest on. The decisive consideration is the searcher arriving from the other direction:
someone on the THEMIS-D Fluxgate Magnetometer or MMS FPI/DIS page, asking what software works with
this instrument's data, gets a package that will fetch it, put it in the right frame and plot it
against a global geospace simulation. Recording only SuperMAG would hide that.

**Considered and rejected: recording `SuperMAG Magnetometers` only (1 row)**, treating the fleet as
covered by Field 32's observatory rows and by Field 17's `CDAWeb` and `Observatory/Mission-specific`.
That is a coherent position — it keeps the entry small and pushes granularity to the observatory
level — and it was rejected because the observatory rows do not answer an instrument-level query, and
because Field 17's values describe *how* Kaipy gets data rather than *whose* data it is. **Had it
been chosen, the fleet would not thereby have been judged irrelevant:** every row above is genuinely
supported, and nothing here was dropped for being irrelevant. A later refresh reading this section
should treat the one-row alternative as a rejected choice of granularity, not as evidence that the
instruments were never found.

**Two costs of this choice, accepted with open eyes.** First, volume: 60 instruments alongside Field
32's 29 observatories is a great deal of controlled vocabulary on one entry, defensible only because
each row is earned separately. Second, and worse here than the corresponding Field 32 problem, **the
display names collide**: the 59 fleet rows carry only 35 distinct names, so the entry's own page
shows `Triaxial Fluxgate Magnetometer` five times, `Fluxgate Magnetometer`, `Cluster Ion
Spectrometry`, `MMS FIELDS/FGM`, `MMS FPI/DIS` and `MMS Positions` four times each, `GOES Triaxial
Fluxgate Magnetometer on GOES` three times, and `RBSP ECT`, `RBSP EMFISIS` and `RBSP RBSPICE` twice
each. The identifiers differ and are what bind, so nothing is duplicated in the data — but a reader
of Kaipy's page sees runs of identical strings. As with the GOES COSPAR designators under Field 32,
the names must be copied verbatim regardless. **This is an upstream vocabulary problem, not a defect
in this entry**, and it is worth reporting upstream rather than working around by withholding true
associations or by inventing friendlier names.

### 32. Related Observatories (OPTIONAL)

**Recorded values (29).** HSSI held one value for this field before this refresh — SuperMAG
(https://spase-metadata.org/SMWG/Observatory/SuperMAG), which is correct and is retained, evidenced
as under Field 31 — so the other 28 are additions.

**The evidence.** Kaipy's satellite-comparison subsystem is a first-class, documented capability, not
an incidental feature: `kaipy/satcomp/` is a documented package (`docs/source/kaipy.satcomp.rst`),
`kaipy/cdaweb_utils.py` provides per-spacecraft position, trajectory and magnetic-footprint fetchers,
and six console scripts drive it (`msphSatComp`, `msphParallelSatComp`, `msphPbsSatComp`,
`helioSatComp`, `rbspSCcomp`, `rcm_rbsp_satcomp`). Two shipped JSON configurations name the
spacecraft it supports, each with its CDAWeb dataset identifiers, variable names and coordinate
systems: `sc_cdasws_strs.json` has 27 entries and `sc_helio.json` has 5. This is per-mission
parsing — the software knows that THEMIS-A's magnetic field lives in `tha_fgs_gsm` in `THA_L2_FGM`
in GSM, and that Solar Orbiter's lives in `B_RTN` in `SOLO_L2_MAG-RTN-NORMAL-1-MINUTE` in RTN — which
is precisely the "designed to support" test, not a generic archive client.

**The recorded set.** Every spacecraft named in the two configurations, plus the three solar-wind
sources read by `kaipy/solarWind/`, at the level SPASE actually models them. Every identifier below
was checked against the controlled vocabulary: each matches exactly one observatory row (`type == 2`),
none has an `.html` duplicate, all are under `https://spase-metadata.org/`, and the names are copied
verbatim from the matched rows.

| Name (verbatim) | SPASE identifier |
|---|---|
| 1994-022A | https://spase-metadata.org/SMWG/Observatory/GOES/8 |
| 1995-025A | https://spase-metadata.org/SMWG/Observatory/GOES/9 |
| 1997-019A | https://spase-metadata.org/SMWG/Observatory/GOES/10 |
| 2000-022A | https://spase-metadata.org/SMWG/Observatory/GOES/11 |
| 2001-031A | https://spase-metadata.org/SMWG/Observatory/GOES/12 |
| Geostationary Operational Environmental Satellite 13 | https://spase-metadata.org/SMWG/Observatory/GOES/13 |
| Geostationary Operational Environmental Satellite 14 | https://spase-metadata.org/SMWG/Observatory/GOES/14 |
| Geostationary Operational Environmental Satellite 15 | https://spase-metadata.org/SMWG/Observatory/GOES/15 |
| Geostationary Operational Environmental Satellite 16 | https://spase-metadata.org/SMWG/Observatory/GOES/16 |
| Geostationary Operational Environmental Satellite 17 | https://spase-metadata.org/SMWG/Observatory/GOES/17 |
| Geostationary Operational Environmental Satellite 18 | https://spase-metadata.org/NOAA/Observatory/GOES/18 |
| Geomagnetic Tail Lab | https://spase-metadata.org/SMWG/Observatory/Geotail |
| Radiation Belt Storm Probe A | https://spase-metadata.org/SMWG/Observatory/RBSP/A |
| Radiation Belt Storm Probe B | https://spase-metadata.org/SMWG/Observatory/RBSP/B |
| Cluster | https://spase-metadata.org/SMWG/Observatory/Cluster |
| Time History of Events and Macroscale Interactions during Substorms A | https://spase-metadata.org/SMWG/Observatory/THEMIS/A |
| Time History of Events and Macroscale Interactions during Substorms B | https://spase-metadata.org/SMWG/Observatory/THEMIS/B |
| Time History of Events and Macroscale Interactions during Substorms C | https://spase-metadata.org/SMWG/Observatory/THEMIS/C |
| Time History of Events and Macroscale Interactions during Substorms D | https://spase-metadata.org/SMWG/Observatory/THEMIS/D |
| Time History of Events and Macroscale Interactions during Substorms E | https://spase-metadata.org/SMWG/Observatory/THEMIS/E |
| Magnetospheric Multiscale | https://spase-metadata.org/SMWG/Observatory/MMS |
| Advanced Composition Explorer | https://spase-metadata.org/SMWG/Observatory/ACE |
| Solar Terrestrial Relations Observatory A | https://spase-metadata.org/SMWG/Observatory/STEREO-A |
| Solar Terrestrial Relations Observatory B | https://spase-metadata.org/SMWG/Observatory/STEREO-B |
| Parker Solar Probe | https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe |
| Solar Orbiter | https://spase-metadata.org/ESA/Observatory/SolarOrbiter |
| ISTP/Wind | https://spase-metadata.org/SMWG/Observatory/Wind |
| Deep Space Climate Observatory, DSCOVR | https://spase-metadata.org/SMWG/Observatory/DSCOVR |
| SuperMAG | https://spase-metadata.org/SMWG/Observatory/SuperMAG |

**Why the per-spacecraft set, from the searcher's side.** Imagine someone on a page about the Van
Allen Probes, or GOES-16, or Solar Orbiter, clicking "show software related to this observatory".
Would they be glad to find Kaipy, or find it out of place? They would be glad: Kaipy will fetch that
spacecraft's data from CDAWeb, put it in the right coordinate system, and plot it against a global
geospace simulation — which is a genuinely useful thing for someone working with that mission's data
to know exists. That is true at the individual-spacecraft level because the support is coded at that
level: GOES-16 and GOES-17 have separate configuration entries with separate dataset identifiers.

**Considered and rejected — mission level (14 rows).** The alternative was to collapse the
per-spacecraft rows to the mission rows SPASE also provides: `Geostationary Operational Environmental
Satellites` (https://spase-metadata.org/SMWG/Observatory/GOES), `Van Allen Probes`
(https://spase-metadata.org/SMWG/Observatory/RBSP), `Time History of Events and Macroscale
Interactions during Substorms` (https://spase-metadata.org/SMWG/Observatory/THEMIS), plus Cluster,
MMS, Geotail, ACE, STEREO-A, STEREO-B, Parker Solar Probe, Solar Orbiter, Wind, DSCOVR and SuperMAG.
It is a real option — fourteen rows read better on the page than twenty-nine, and the mission names
are the friendlier strings. **It was rejected because the observatory vocabulary is flat: a mission
row does not match a spacecraft query**, so recording `Geostationary Operational Environmental
Satellites` would make Kaipy invisible to someone searching from the GOES-16 page, which is exactly
the searcher this field exists to serve. The mission rows remain listed here so a later refresh can
find them without re-deriving them.

**Considered and rejected — retaining only SuperMAG**, treating everything reached through CDAWeb as
covered by Field 17's `CDAWeb` and `Observatory/Mission-specific`. Rejected for the same reason one
step further along: those Field 17 values describe how Kaipy obtains data, not whose data it is, and
they surface the entry for no mission query at all. Neither rejection implies the missions are
unsupported — each row in the table above is evidenced by its own dataset identifiers, variable names
and coordinate frames.

**Three costs of this choice, stated fairly and accepted.**
1. **Five of the GOES rows have unreadable names.** GOES 8 through 12 are named by COSPAR
   designator — `1994-022A`, `1995-025A`, `1997-019A`, `2000-022A`, `2001-031A` — in the vocabulary
   itself. Recorded as they are, they display on Kaipy's page as five opaque strings. The names must
   still be copied verbatim, because the identifier is what binds and inventing a friendlier name
   would create a duplicate row; but a reader will not know what they are looking at. This is an
   upstream vocabulary problem worth reporting there, and it is a real and accepted cost of recording
   these five.
2. **Twenty-nine observatories is a lot of rows on one entry.** It is defensible only because each
   one is individually evidenced.
3. **The GOES-8 through GOES-12 support is historical.** Those spacecraft stopped operating years
   ago; the configuration entries are there so old events can be re-run.

**Sub-decisions inside the recorded set, recorded so they can be varied independently.**
- *RBSP* is listed as the two spacecraft rows (`/RBSP/A`, `/RBSP/B`) because the configuration has
  separate `RBSPA` and `RBSPB` entries with different dataset lists — `RBSPB` includes
  `RBSPB_REL04_ECT-HOPE-PA-L3`, which `RBSPA` does not. The mission row, named `Van Allen Probes`,
  is the friendlier display name and was considered as a single-row substitute; it was not selected,
  for the flat-vocabulary reason above.
- *Cluster* is listed at mission level even though the configuration has `CLUSTER1` through
  `CLUSTER4`. The per-spacecraft SPASE rows are named `Cluster 2/FM5` through `Cluster 2/FM8`, which are
  even less recognisable than the GOES designators, and unlike GOES the four Cluster entries carry
  near-identical dataset sets. The mission row named simply `Cluster` serves a searcher better.
- *MMS* is listed at mission level for the same reason: the configuration's four entries are
  identical in structure, differing only in the spacecraft number embedded in the variable names.
- *THEMIS* is listed per-spacecraft because the five probes genuinely have distinct dataset
  identifiers, and because the mission-level row's name is a 67-character expansion that reads
  poorly in a list. Note that the 46 THEMIS observatory rows include 40 ground-station rows
  whose identifiers sit under `https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/`; those are
  **not** relevant here, because Kaipy reads only the five probes.
- *Wind, DSCOVR and ACE* come from `kaipy/solarWind/`, not from the satcomp configurations:
  `WIND.py` reads Wind SWE and MFI files, `SWPC.py`'s `DSCOVRNC` reads NOAA DSCOVR netCDF, and its
  `ACESWPC` subclass reads the SWPC daily ACE products. ACE is additionally in `sc_helio.json`.

**Considered and rejected as observatories:**
- *OMNI* — `kaipy/solarWind/OMNI.py` is the most-used reader in the package and SPASE does have an
  `OMNI` observatory row. It is excluded because OMNI is a derived, multi-mission dataset rather than
  an observatory a user would search for as a platform; the guidance sends a generic multi-mission
  data source to Field 17, and `CDAWeb` there already covers how Kaipy obtains it. **Recorded because
  the SPASE row's existence makes this look like an obvious inclusion.**
- *The 40 THEMIS ground-station rows* (those whose identifiers sit under
  `https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/`) — Kaipy reads ground magnetometer data through
  SuperMAG, not through the THEMIS ground array, and nothing in the tree names those stations.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/JHUAPL/kaipy/0028c69c52a91ff378a5798708daaba4cdfb5790/docs/source/_static/kaipy-logo.png

**This logo was added by this refresh** — HSSI held no logo for the entry before it.

The image is the project's own logo, not an example figure: `docs/source/conf.py` sets
`html_logo = '_static/kaipy-logo.png'` with `'logo_only': True`, so it is the banner the
documentation site displays in place of the project title. Looked at directly, it is a blue cartoon
snake wearing a purple wizard's hat, coiled, with "KAIPY" in pale blue capitals beneath — a
purpose-drawn wordmark, unambiguously this software's.

The URL serves the image itself rather than a page or a pointer file: `Content-Type: image/png`,
1,008,121 bytes with PNG magic present, 2411×2791 pixels, 8-bit RGBA. It is 122 characters, within
the 200-character limit for the stored field.

**Why it is pinned to the commit SHA rather than to `master`.** The requirement is that the URL be
permanent, not merely that the file exist today. A branch URL breaks silently the moment the file is
renamed, moved or deleted, and the catalogue has no way to notice. The counter-argument — that a
branch URL would always show the current logo, whereas a pinned URL freezes an old one — is the
argument for pinning, not against it: that mutability is the fragility being removed, and a logo
redesign is something a future refresh should notice and record deliberately rather than something
the catalogue should inherit silently.

The `raw.githubusercontent.com` host is correct here rather than the Git-LFS media host: no
`.gitattributes` exists at the pin, the file is a regular blob, and this host serves a megabyte of
real PNG rather than the ~130-byte text pointer an LFS-tracked file would return through it.
A `blob/` page URL was not used because it serves HTML.

**Three other PNGs exist in `docs/source/_static/`** — `ionExample.png`, `plotXYExample.png` and
`plotXZExample.png`. They are the example plots embedded in `docs/source/kaipy/usage.rst` and are not
logos. **Recorded so a later refresh does not mistake one of them for the project's mark.** The PyHC
community registry entry for kaipy has no `logo:` field, so it offers no competing candidate.
