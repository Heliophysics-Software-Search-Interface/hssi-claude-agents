# HSSI Metadata Extraction Results

**HSSI Software ID:** 13659e76-e911-41da-bf99-30eb7b05defc
**Repository:** https://github.com/nasa/Kamodo
**Source Revision:** 6706989574997795ce1b16b75af31c382eba0611
**Extraction Date:** 2026-08-13
**Validation Date:** 2026-08-15
**Validation Status:** PASS

**Scope note.** The GitHub repository `nasa/Kamodo` ships the CCMC *analysis suite* (`kamodo_ccmc`).
The functional core it is built on, `kamodo-core`, is a **separate** package with its own repository,
its own PyPI project and its own Zenodo software DOI; it is recorded under Related Software (Field 29),
not conflated with this record. Several fields below turn on that distinction — notably Persistent
Identifier (Field 2), Reference Publication (Field 14) and Software Name (Field 7) — so read the
evidence with it in mind.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** Not found
- **Negative research (re-verified against DataCite and Zenodo at this revision).** A DataCite search
  for "kamodo" returns 15 records. Exactly two carry `resourceTypeGeneral: Software`:
  `10.5281/zenodo.6773395` and its concept DOI `10.5281/zenodo.6773394`. Both are titled "Kamodo: A
  functional API for space weather models and data" and both archive a **single file,
  `kamodo-core-22.6.0.tar.gz`** — i.e. they are the JOSS review archive of `kamodo-core`, not of the
  CCMC analysis suite in this repository. Recording either as this record's persistent identifier
  would mis-identify a different software product; they are captured under Field 29 instead.
- The two Zenodo records `10.5281/zenodo.11121935` (concept) and `.11121936`, titled "Kamodo: A CCMC
  Open Source Toolkit for Space Physics Simulation Output" (2024), carry `resource_type.type =
  presentation`. Conference presentations are not a software persistent identifier.
- The JOSS software-paper DOI is recorded under Reference Publication (Field 14), not here.
- This repository has no Zenodo–GitHub integration file, no `CITATION.cff` and no `codemeta.json`, so
  no software DOI is minted on release. Its sole GitHub release (`25.12.1-FINAL`) has no associated
  DOI, which is also why Field 12's Version PID is empty.

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/nasa/Kamodo
- **Source:** git remote; `setup.cfg` `url` and `project_urls` (`Repository = https://github.com/nasa/Kamodo`);
  the PyHC **core** package registry `code` field. All three agree at this revision.

### 4. Software Functionality (MANDATORY)
Every subcategory below also lists its bare parent top-level category, as the taxonomy requires — a
subcategory without its parent is an incomplete classification, not a shorter one.

- **Coordinate Transforms**
- **Coordinate Transforms: Magnetospheric** — `ConvertCoord` in `kamodo_ccmc/flythrough/utils.py`
  converts among the SpacePy systems `GDZ, GEO, GSM, GSE, SM, GEI, MAG, SPH, RLL` (declared in
  `spacepy_coordlist`). `ConvertCoord` alone carries this classification; the module also *defines*
  `ComputeLshell` (Lm, Lstar and MLT from spacepy's IRBEM drift-shell machinery) but never calls it —
  see the Ionospheric rejection below.
- **Coordinate Transforms: Heliospheric** — the same `ConvertCoord` accepts the AstroPy frames in
  `astropy_coordlist`, including `heliocentricmeanecliptic`, `heliocentrictrueecliptic`,
  `heliocentriceclipticiau76`, `hcrs`, and the barycentric ecliptic frames.
- **Data Processing and Analysis**
- **Data Processing and Analysis: Data Access and Retrieval** — HAPI client integration
  (`kamodo_ccmc/readers/hapi.py`, `tools/functionalize_hapi.py`), satellite-trajectory retrieval from
  the SSCWeb HAPI server (`flythrough/SatelliteFlythrough.SatelliteTrajectory`), CCMC Runs-on-Request
  extractions over HTTP (`readers/sat_extractions.py`), and S3 object access in
  `readers/reader_utilities.py` (`s3fs.S3FileSystem`, `boto3.client('s3')`, `s3://` path handling).
- **Data Processing and Analysis: Analysis** — function composition and derived quantities; model
  validation and model–data comparison (`Validation/` notebooks and spreadsheets); magnetopause and
  bow-shock surface extraction (`tools/plotfunctions.py` `gmComputeSurface`);
  `lastclosedmag.analyze_magnetopause_shape`.
- **Data Processing and Analysis: Processing** — functionalization of model outputs;
  `readers/reader_utilities.py`; the one-way model-coupling driver in `kamodo_ccmc/filedriver/`, which
  reads SWMF-IE output and generates forcing input files for GITM, WACCM-X and TIE-GCM.
- **Data Processing and Analysis: File Format Conversion** — the thirteen `*_tocdf.py` modules plus
  `gameragm_grids.py` convert native model output into standardized netCDF intermediates: adelphi,
  gitm, openggcm_gm (both the top-level and `OpenGGCM/` copies), openggcm_ie, superdarn, swmfie,
  verb3d and gameragm_grids write `format='NETCDF4'`; ctipe and tiegcm use `Dataset(out_file, 'w')`,
  which is netCDF4 by default; waccmx, wamipe and weimer write `format='NETCDF3_64BIT_OFFSET'`.
  `flythrough/SF_output.py` writes `.nc`, `.csv` and `.txt` and reads the same three back.
- **Data Processing and Analysis: Field-line Tracing** — `tools/vectorfieldtracer.py`
  (`KamodoVectorFieldTracer` with RK4 integration and numba acceleration; factory functions
  `create_magnetic_tracer`, `create_velocity_tracer`, `create_current_tracer`,
  `create_electric_tracer`); `tools/lastclosedmag.py` (`find_last_closed_field_lines`).
- **Data Processing and Analysis: 2D Slices** — `tools/plotfunctions.py` `GDZSlice4D`,
  `gm3DSlicePlus`, `swmfgm3Darb` (arbitrary-normal cut planes).
- **Data Processing and Analysis: Magnetic Null Finding** — `tools/nullfinder.py`
  (`find_magnetic_null_points`, `refine_null_point_location`, `classify_field_line_topology`,
  `trace_special_field_lines_near_null`).
- **Data Processing and Analysis: Time Series Analysis** — `flythrough/SF_output.py`
  `Functionalize_TimeSeries` and `Functionalize_SFResults`; `tools/timefunctions.py`.
- **Data Visualization**
- **Data Visualization: 2D Graphics** — plotly/matplotlib contour and map plots in
  `tools/plotfunctions.py` (`XYC`, `gm2DSliceFig`, `ITM_Cutout_Plot`) and `flythrough/plots.py`
  (`custom2Dsat`, `custom2Dpolar`).
- **Data Visualization: 3D Graphics** — `SatPlot4D` type `3D`/`3Dv`, `custom3Dsat`, `swmfgm3D`,
  `B3Dfig`, `BlinesFig`, `LastClosedBfig`, and the plotly/matplotlib 3D renderers in
  `vectorfieldtracer.py` and `nullfinder.py`.
- **Data Visualization: Line Plots** — `flythrough/plots.py` `custom1Dsat` (`SatPlot4D` type `1D`).
- **Data Visualization: Orbit Plots** — `SatPlot4D` orbit grouping (`groupby='orbitE'`/`'orbitM'`),
  `plotfunctions.SatPosFig` and `SatOrbitPlane`.
- **Data Visualization: Movies** — time-animated 4D plots via `SatPlot4D`'s `groupby` animation
  frames, plus `plotfunctions.BlinesMovie` and `gmSurfaceMovie`.
- **Data Visualization: Web-Based** — interactive plotly output written as standalone HTML or an
  embeddable div (`htmlfile`/`divfile` arguments throughout `SatPlot4D` and `plotfunctions`); the
  container stack in `docker-compose.yaml` publishes browser-served Jupyter/Kamodo endpoints.
- **Data Visualization: 2D Slices** — `gm2DSliceFig`, `GDZSlice4D`, `gm3DSlicePlus` slice rendering.
- **Data Visualization: Spacecraft Formation Plots** — the Satellite Constellation Mission Planning
  Tool (`tools/constellation.py` `Constellation`, four `Tutorials/ConstellationTutorial_*.ipynb`
  notebooks, and the AGU poster `10.22541/essoar.167214257.73153757/v1` cited in the class docstring)
  designs and evaluates multi-satellite configurations from time and coordinate offset lists. The
  plotting layer supports this directly: the `SatPlot4D` plot dictionary carries a `sats` key
  documented as "Array of satellites to include in plot", and `custom3Dsat`, `custom2Dsat`,
  `custom2Dpolar` and `custom1Dsat` all iterate `for sat in datad['sats']` to overlay several
  spacecraft in one figure.
- **Models and Simulations**
- **Models and Simulations: Empirical** — wraps and functionalizes empirical models: IRI, DTM,
  Weimer, Ovation-Prime, the SuperDARN TS18 statistical convection model (the `superdarn_tocdf.py`
  header records `Model: TS18`), JB2008 (`readers/kamodo-JB2008/`) and Tsyganenko
  (`readers/kamodo-tsyganenko/`).
- **Models and Simulations: Physics-Based** — functionalizes first-principles model output that
  Kamodo reads (SWMF/BATSRUS-GM, OpenGGCM-GM, GAMERA-GM, CTIPe, GITM, TIE-GCM, WACCM-X, WAM-IPE,
  VERB-3D). Post-processing only — Kamodo does not run the solvers, which is why
  `Models and Simulations: MHD` and `: First Principles` are deliberately **not** selected.
- **Models and Simulations: Field-line Tracing** — traces field lines through functionalized model
  fields (SWMF/BATSRUS-GM, OpenGGCM-GM) via `vectorfieldtracer.py` and `lastclosedmag.py`.
- **Models and Simulations: Data Guided** — the containerized Tsyganenko wrapper runs an empirical
  magnetospheric field model driven by observed solar-wind/IMF and geomagnetic-index data:
  `readers/kamodo-tsyganenko/scripts/initialize_pygeopack.py` calls `PyGeopack.Params.UpdateParameters()`
  and `readers/kamodo-tsyganenko/docker-compose.yaml` mounts `kp_data:/data/kp/`,
  `omni_data:/data/omni/` and `geopack_data:/data/geopack/`. The JB2008 wrapper
  is likewise index-driven, and `kamodo_ccmc/filedriver/kp_reader.py` builds the daily Kp series the
  FileDriver coupling needs from GFZ Kp data.
- **Servers and Environments**
- **Servers and Environments: Software or Environment Container** — eight Dockerfiles under
  `dockerfiles/` (`API`, `Dockerfile`, `dockerfile_jb2008`, `dockerfile_tsyganenko`, `kamodo-wrap`,
  `kamodo_ccmc_readers`, `satellite_extractions`, `spacepy`), a top-level `docker-compose.yaml`
  defining seven services, and two further reader-level compose files under
  `readers/kamodo-JB2008/` and `readers/kamodo-tsyganenko/`.
- **Servers and Environments: Data servers processing and handling** — `kamodo_ccmc/hapi/` implements
  a HAPI server backend that serves Kamodo flythrough results (`HAPI_KamodoRealFlight.py`,
  `HAPI_KamodoRealFlight_JSONs.py`, `HAPI_KamodoJSONs.py`, plus CTIPe dataset/parameter JSON
  descriptors). Note for future refreshes: the ASR paper describes a full HAPI interface over Kamodo
  as still being investigated, so this is a working server backend rather than a hosted production
  service — the code is present, which is what the category asks for.

**Considered and not selected** (kept so a future refresh does not re-propose them):
- **Coordinate Transforms: Ionospheric** — re-tested at this revision. `ConvertCoord`'s two
  vocabularies (`spacepy_coordlist`, `astropy_coordlist`) contain no AACGM, apex, quasi-dipole or
  geomagnetic-apex frame, and no such conversion exists anywhere in `kamodo_ccmc/`. The MLT point is
  stronger than it first appears: Kamodo *defines* an MLT-computing function but never calls it.
  `flythrough/utils.py:458` `ComputeLshell` returns Lm, Lstar and MLT via spacepy/IRBEM, and its own
  docstring says "(Not currently used in Kamodo.)" — a repository-wide grep finds only the
  definition itself and the one-line summary in the module docstring, with no call site anywhere in
  the package, the tests, the notebooks or the documentation. No MLT is computed anywhere in the
  shipped code. The `MLAT`/`MLT` grids in the ADELPHI and SuperDARN readers are *read from* the model
  files, not derived. Classified as Magnetospheric instead.
- **Models and Simulations: MHD** and **: First Principles** — Kamodo reads and interpolates MHD
  output; it contains no MHD solver.
- **Models and Simulations: Mission-Specific** — the constellation tool is general-purpose and takes
  arbitrary user-supplied trajectories and offsets; it is not built for one mission.
- **Data Processing and Analysis: Data Assimilation** — AMGeO ("Assimilative Mapping of Geospace
  Observations") is a supported *input* model. Kamodo reads its output and performs no assimilation.
- **Data Processing and Analysis: Spectrogram**, **Wavelet Analysis**, **Image Processing** and
  **Data Visualization: Spectrogram** — no FFT, STFT, wavelet, periodogram or scientific
  image-processing code exists in `kamodo_ccmc/`. The figure helpers (`figMods`, `toColor`,
  `toLog10`, `fig2darkmode`) restyle plotly figures; they do not process image data.
- The stored Description advertises "Simulated imagery" and "a line of sight calculation tool". Those
  remain **stated aims**: no line-of-sight, column-integration or synthetic-imaging code exists at
  this revision. They are therefore not classified. Re-check on a future refresh rather than
  classifying from the description.
- **Data Processing and Analysis: Data Reduction** — the constellation reconstruction averages and
  bins model slices, but its purpose is field reconstruction rather than volume reduction; covered by
  `Analysis`.
- **Mission-related** (any subcategory) — Kamodo is a general analysis suite, not part of a mission
  ground system.
- **Source:** direct inspection of `kamodo_ccmc/` at this revision, plus README, `docs/notebooks/`
  and `Tutorials/`.

### 5. Related Region (MANDATORY)
Kamodo is a broad geospace suite, so this field carries both the two broad regions and the specific
ones beneath them. The `Region` vocabulary is finer-grained than the five broad regions this record
was originally built from, and Kamodo's coverage is specific enough to use that granularity; the two
broad regions are held alongside the specific ones rather than replaced by them, because the model
readers genuinely span whole domains rather than single sub-regions.

- **Earth Atmosphere** — the broad parent for the ionosphere/thermosphere/mesosphere readers.
- **Earth Magnetosphere** — the broad parent for the global-magnetosphere readers.
- **Earth Ionosphere** — dedicated readers for IRI, CTIPe, TIE-GCM, WAM-IPE, SWMF-IE, OpenGGCM-IE,
  SuperDARN (TS18 convection), ADELPHI, AMGeO, Weimer and Ovation-Prime.
- **Earth Thermosphere** — DTM (the Drag Temperature Model), GITM, TIE-GCM, WACCM-X and CTIPe
  readers, plus the containerized JB2008 thermospheric density model.
- **Earth Auroral Subregion** — Ovation-Prime is an auroral particle-precipitation model and its
  reader (`ovationprime_4D.py`) exists solely to support it; ADELPHI, AMGeO, SuperDARN and Weimer are
  all high-latitude products; `flythrough/plots.py` provides north/south polar projections
  (`custom2Dpolar`, `SatPlot4D` types `2DPN`/`2DPS`) and `plotfunctions.getIEPCB`/`getIEPCBk` extract
  the ionospheric polar-cap boundary.
- **Earth Inner Magnetosphere** — the VERB-3D radiation-belt reader (`verb3d_4D.py`,
  `verb3d_tocdf.py`), its `tests/test_verb4d.py` adiabatic-invariant tests, the `rbamlib` and
  `pyverbplt` radiation-belt dependencies, and `Tutorials/VERB-3D_plotting_examples.ipynb`.
- **Earth Magnetotail** — the global-magnetosphere readers (SWMF-GM, OpenGGCM-GM, GAMERA-GM) span the
  tail, and the topology tools that operate on them target tail physics:
  `lastclosedmag.find_last_closed_field_lines` and `nullfinder.find_magnetic_null_points`
  (reconnection-site identification). Note that the `CS` ("Tail Current Sheet") branch of
  `gmGetSurfacePlot` is an unimplemented stub that returns `None, False`, so it is *not* part of this
  evidence.
- **Earth Magnetosheath** — `plotfunctions.gmComputeSurface` computes both bounding surfaces of the
  magnetosheath from global MHD output: `what='MP'` locates the magnetopause by bisecting on the
  `status` variable, and `what='BS'` locates the bow shock; `gmGetSurfacePlot`, `gmSaveSurface` and
  `gmSurfaceMovie` render and animate them.
- **Earth Outer Magnetosphere** — the magnetopause surface extraction and the last-closed-field-line
  finder (`find_last_closed_field_lines`, `find_last_closed_field_lines_auto_bounds`,
  `analyze_magnetopause_shape`) are outer-magnetosphere boundary science.
- **Earth Lower and Middle Atmosphere** — the WACCM-X reader (`waccmx_4D.py`, `waccmx_tocdf.py`)
  functionalizes the Whole Atmosphere Community Climate Model with thermosphere/ionosphere extension,
  whose domain runs from the surface upward; `filedriver/WACCMX_filedriver_v2.py` drives it.

**Considered and not selected:**
- **Interplanetary Space** and **Solar Wind** — re-tested at this revision and still rejected. Kamodo
  has no heliospheric or solar-wind model reader (`model_wrapper.model_dict` contains none), so
  heliospheric coverage remains incidental: it comes from generic HAPI access, from the upstream
  boundary of a global-magnetosphere domain, and from OMNI indices used to *drive* the Tsyganenko
  wrapper. `plotfunctions.BlinesMovie(showSW=...)` toggles display of solar-wind field lines drawn
  from that same global-MHD domain; it is a display option, not solar-wind science functionality. The
  2026-06-10 reconciliation reached the same conclusion, which this revision confirms rather than
  reopens.
- All solar and planetary regions (Corona, Chromosphere, Photosphere, Solar Interior, Solar
  Environment, Heliosheath, and the per-planet magnetospheres) — no supported model or reader covers
  any of them. The PyHC registry's `solar` keyword for Kamodo is not borne out by any reader in the
  source.

### 6. Authors (MANDATORY)
Ten authors. Affiliation names below are the organizations the record links to; the JOSS and
Frontiers papers corroborate each one.

**Author 1:**
- **Name:** Alexander Drozdov
- **Author Identifier:** https://orcid.org/0000-0002-5334-2026
- **Affiliation - Organization:** University of California, Los Angeles (https://ror.org/046rm7j60)
- Corroborated in-repo: `readers/verb3d_4D.py` and `readers/verb3d_tocdf.py` both carry
  `@author: xandrd`, and his commits use `adrozdov@ucla.edu`.

**Author 2:**
- **Name:** Asher Pembroke
- **Author Identifier:** Not found. No ORCID is given in the JOSS paper, the Zenodo record, or the
  repository. An ORCID expanded search for given name `Asher` / family name `Pembroke` returns
  exactly one hit, `0000-0002-5718-1303` — an essentially empty profile created 2021-09-28 with no
  employment history, no works, no external identifiers, no biography and no keywords, and nothing
  tying it to Predictive Science, Ensemble Government Services, or any heliophysics publication.
  It is not attached, because a name-only match to a blank profile is not identification. Recorded
  so a future refresh does not attach it on a second look.
- **Affiliation - Organization:** Predictive Science (no ROR recorded)
- The stored affiliation is corroborated by his commit address `apembroke@predsci.com` and the
  `API.Dockerfile` maintainer label. Note that his *paper-time* affiliations differ — JOSS 2022 gives
  "Asher Pembroke, DBA" and the Zenodo record "Asher Pembroke DBA" — so the stored value reflects his
  current institution rather than the byline. Both were considered; the current institution is the
  more useful and is what the record holds.

**Author 3:**
- **Name:** Lutz Rastaetter
- **Author Identifier:** https://orcid.org/0000-0002-7343-4147
- **Affiliation - Organization:** Community Coordinated Modeling Center (https://ror.org/01dy3j343);
  National Aeronautics and Space Administration (https://ror.org/027ka1x80)
- The ORCID is confirmed by the README's own team section. The stored name corrects an earlier
  misspelling, "Raestatter", carried by the record before the 2026-06-10 reconciliation.

**Author 4:**
- **Name:** Rebecca Ringuette
- **Author Identifier:** https://orcid.org/0000-0003-0875-2023
- **Affiliation - Organization:** Adnet Systems (United States) (https://ror.org/05we1n045);
  Heliophysics Data and Modeling Consortium (https://ror.org/04xbq1n92); Heliophysics Digital
  Resource Library (https://ror.org/00d1g0h88)
- JOSS 2022 gives "ADNET Systems Inc." and "Community Coordinated Modeling Center, NASA GSFC"; the
  Frontiers paper states her work was "funded by the CCMC through ADNET Systems, Inc." The three
  stored affiliations are a superset consistent with that record and are retained in full.

**Author 5:**
- **Name:** Darren De Zeeuw
- **Author Identifier:** https://orcid.org/0000-0002-4313-5998
- **Affiliation - Organization:** Calvin College (https://ror.org/05r0q9p84); Goddard Space Flight
  Center (https://ror.org/0171mag52); National Aeronautics and Space Administration
  (https://ror.org/027ka1x80); University of Michigan (https://ror.org/00jmfr291)
- **Corrected name split.** HSSI previously stored this author as given name "Darren de" and
  family name "Zeeuw", which rendered as "Darren de Zeeuw". That split was wrong. The correct form
  is given name "Darren", family name "De Zeeuw", with a capital D, and first-party sources agree
  on it: ORCID 0000-0002-4313-5998 records exactly that split; `setup.cfg` has
  `author = Darren De Zeeuw`; the README team section reads "Dr. Darren De Zeeuw"; the PyHC core
  registry `contact` is "Darren De Zeeuw"; and the JOSS byline credits him under the same surname.
- **A name split belongs to the person, not to this record.** The split is a property of a shared
  person row rather than of this software's metadata: the same row is cited by other software in
  HSSI, so changing a name propagates to every record that references it. A discrepancy of this
  kind is therefore resolved at the person level, after checking what else that row is attached
  to — not through a field edit on this record, which cannot reach it. Recorded so the wrong split
  is not reintroduced and so the constraint is understood the next time a name looks off.

**Author 6:**
- **Name:** Katherine Garcia-Sage
- **Author Identifier:** https://orcid.org/0000-0001-6398-8755
- **Affiliation - Organization:** Community Coordinated Modeling Center (https://ror.org/01dy3j343);
  National Aeronautics and Space Administration (https://ror.org/027ka1x80)
- **Provenance correction.** This record previously stated that Garcia-Sage was "added from the JOSS
  paper". She is **not** a JOSS author; the JOSS byline is Pembroke, DeZeeuw, Rastaetter, Ringuette,
  Gerland, Patel, Contreras. Her actual authorship evidence is the Frontiers 2022 flythrough paper
  (`10.3389/fspas.2022.1005977`, sixth author) and the 2022 AGU constellation poster
  (`10.22541/essoar.167214257.73153757/v1`); the JOSS Acknowledgements thank her separately for
  "advice and support".
- **Upstream drift, 2026-07-07.** Commit `267bb2c` ("Fix duplicate entries in team section of
  README") removed her entry from the README's Kamodo team section, leaving only De Zeeuw and
  Rastaetter. Inspection of `267bb2c^` shows the section listed Rastaetter, De Zeeuw and Garcia-Sage
  once each, so the commit deduplicated nothing and in fact deleted her listing. The README team
  section is a current-staff roster, not an authorship list, and her publication authorship is
  unaffected — she is retained.

**Author 7:**
- **Name:** Oliver Gerland
- **Author Identifier:** Not found
- **Affiliation - Organization:** Not found — the papers place him at Ensemble Government Services,
  which has no ROR record (searched; the ROR API returns no matching organization).

**Author 8:**
- **Name:** Dhruv Patel
- **Author Identifier:** Not found
- **Affiliation - Organization:** Not found — Ensemble Government Services, no ROR (as above).

**Author 9:**
- **Name:** Michael Contreras
- **Author Identifier:** Not found
- **Affiliation - Organization:** Not found — Ensemble Government Services, no ROR (as above).

**Author 10:**
- **Name:** Joshua Pettit
- **Author Identifier:** Not found — deliberately, see below.
- **Affiliation - Organization:** Not found — deliberately, see below.
- **Why he is an author.** Pettit is the sole self-identified author of the entire
  `kamodo_ccmc/filedriver/` subpackage, which ships in the installed distribution and implements the
  one-way model coupling that turns SWMF-IE output into forcing input for GITM, WACCM-X and TIE-GCM.
  `kp_reader.py` carries `@author: Josh Pettit, GMU/NASA GSFC`, and `GITM_filedriver.py`,
  `WACCMX_filedriver_v2.py` and `master_script_v2.py` each carry `@author: jmpettit`. Authoring a
  complete shipped module is authorship of the software, which is what this field records.
- **Why no identifier is attached.** ORCID `0000-0003-3733-6774` was examined as a candidate and
  rejected. Its publication list — relativistic electron precipitation, WACCM polar-ozone response,
  storm-time thermospheric neutral density, FIREBIRD-II/POES electron comparisons — matches the
  FileDriver module's subject matter closely, but that record's only employment entry is University
  of Helsinki, whereas the source header states George Mason University / NASA GSFC. The match is
  strong but not certain, and a probable ORCID is worse than none: an identifier is a claim of
  identity, and a wrong one is harder to detect than a missing one. No affiliation is recorded for
  the same reason — the only affiliation evidence is the acronym pair in that one source header,
  which cannot be attributed to a point in time or resolved to a single institution with confidence.
- **Negative research, so this is not re-litigated.** Pettit appears in no Kamodo publication byline
  (not JOSS, Frontiers, ASR, or the AGU poster), not in the README's Kamodo team section, and not in
  the git commit log — his code was committed by others. The in-source `@author:` headers are the
  whole of the evidence, and they are sufficient on their own.

**Considered and rejected — R. Robinson.** Listed as a co-author on the 2022 AGU constellation
poster: README line 151 reads "Ringuette, R., L. Rastaetter, D. De Zeeuw, K. Garcia-Sage,
R. Robinson, and O. Gerland (2022). Kamodo's Satellite Constellation Mission Planning Tool…"
(`10.22541/essoar.167214257.73153757/v1`), and `tools/constellation.py` reads a trajectory file
described in-source as "Bob's file". That poster is the same source used to justify retaining
Garcia-Sage, so the asymmetry needs stating: Garcia-Sage additionally holds a peer-reviewed byline
on the Frontiers paper and was a listed Kamodo team member until 2026-07-07, whereas a
conference-poster byline is Robinson's only authorship signal. There is no repository presence, no
package-metadata presence, no journal byline, and no commit-log authorship. Recorded so the name is
not rediscovered cold and added on weaker evidence than the rest of the list.

### 7. Software Name (MANDATORY)
- **Value:** The CCMC Kamodo Analysis Suite

**Why this name, over each alternative.** The field asks for "the name of the software package as
listed on the code repository". The repository's title is the README H1, `# The CCMC Kamodo Analysis
Suite`, which has been stable since commit `6d7b704` on 2023-02-01 and is unchanged at this revision.
That is the most direct first-party answer to the field as defined. It also does real disambiguating
work: the installable distribution is named `kamodo_ccmc` precisely to separate this CCMC suite from
`kamodo-core`, a distinct package with its own repository (`nasa/Kamodo-core`), its own PyPI project
and its own software DOI. The "CCMC" token is therefore not decorative attribution — it is what
distinguishes this software from the other Kamodo.

Alternatives evaluated and rejected:
- **`Kamodo`** — by far the most frequent form (README prose, all four publications, the Zenodo
  software record title, the GitHub repository name, the import namespace, the PyHC core registry
  `name` field). Rejected because it is the *family* name shared with `kamodo-core`: the JOSS paper
  titled "Kamodo: A functional API for space weather models and data" describes kamodo-core, and the
  Zenodo record with that title archives `kamodo-core-22.6.0.tar.gz`. Naming this record "Kamodo"
  would make the two indistinguishable. Frequency is evidence, but it is counting the family name.
- **`Kamodo Analysis Suite`** — the strongest runner-up, and the only alternative with authoritative
  first-party backing on two independent axes. The NOSA LICENSE names it as the legal release title
  ("Government Agency Original Software Title: Kamodo Analysis Suite", designation GSC-18210-1,
  restated in clause 1.G), and `mkdocs.yml` sets `site_name: Kamodo Analysis Suite`, which is the
  title and navigation label rendered on the official documentation site
  https://nasa.github.io/Kamodo/. Rejected because it drops the CCMC qualifier that separates this
  package from kamodo-core, and because the repository's own title — the field's stated criterion —
  includes that qualifier. It remains the second-best-supported name: should the question ever be
  reopened, this is the only short form with authoritative first-party backing, and any other
  shortening would be less well founded than the name in use.
- **`CCMC Kamodo`** — the heading and title on the official CCMC product page
  (https://ccmc.gsfc.nasa.gov/tools/kamodo/, page title "CCMC Kamodo | NASA CCMC"), and the running
  in-house label for this package in the repository's own documentation
  (`docs/ContributionGuidelines.md`, `docs/notebooks/QuickStart.ipynb`,
  `FunctionalizingModeledDatasets.ipynb`, `FlythroughCommandLine.ipynb` — four files; a fifth
  `grep -rl` hit, `README.md`, matches only as a substring of the H1 counted separately above).
  Rejected as a
  product-page label and short-hand rather than the software's title; it is a truncation of the
  README title, not an independent name.
- **`Kamodo CCMC`** — no first-party usage anywhere. A repository-wide search finds zero occurrences.
  Rejected outright.
- **`Kamodo-CCMC` / `kamodo_ccmc` / `kamodo-ccmc`** — the distribution and package identifiers
  (`setup.cfg` `name = kamodo_ccmc`; the PyPI project `kamodo-ccmc`; `Kamodo-CCMC` appears once, in
  the `setup.py` module docstring). Rejected: these are packaging identifiers, not the software's
  name, and PyPI's `kamodo-ccmc` is in any case stale at 23.3.1 (2023-03-23).
- **`CCMC Kamodo Analysis Suite`** (the README title minus the definite article) — has no first-party
  source of its own; it exists only as a substring of the README H1. Dropping just the article would
  invent a form nobody uses. Rejected.

**Consequence note.** Field 7 governs the displayed name only. Nothing here should be read as a
recommendation about the record's public slug, which is a separate concern.

### 8. Description (MANDATORY)
- **Source:** the maintainers' README Vision Statement, held in HSSI in Markdown-valid form.

**Verified at this revision.** The stored description and the current README Vision Statement
(README.md lines 6–23, from "Kamodo is an official NASA open-source python package…" through
"…Join us!") are word-for-word identical after normalising whitespace and bullet markers. The one
deliberate difference is formatting: the README uses tab-indented `-\t` pseudo-bullets, which the
site's Markdown renderer collapsed into a run-on paragraph, so the stored text uses `- ` dash-space
bullets and a blank line before the list. That formatting change was made during the 2026-06-10
reconciliation and must be preserved — reverting to the README's literal bytes would reintroduce the
rendering bug.

**Value (as stored):**

Kamodo is an official NASA open-source python package built upon the functionalization of datasets. Once a dataset is functionalized in Kamodo, several important capabilities are then available to the user, including data analysis via function composition, automatic unit conversions, and publication quality graphics all using intuitive and simplistic syntax. By applying these capabilities to heliophysics model outputs, we aim to:

- Drastically simplify the currently complex data utilization process for model outputs,
- Provide interactive access to functionalized model outputs for users ranging in programming skill from beginners – via code-free interfaces and video tutorials – to advanced users – via thorough documentation, Jupyter notebook examples and sample workflows,
- Layer multiple functionalities on top of the functionalized model outputs, all with model-agnostic and uniform syntax, including but not limited to:
    - Flythrough tools,
    - Vector field tracing (including magnetic field mapping),
    - Coordinate conversions,
    - Domain-specific interactive plots of publication quality,
    - Modular driver swapping,
    - Satellite constellation mission planning tools,
    - Simulated imagery, and
    - A line of sight calculation tool,
- Greatly reduce the programming skill currently required outside of Kamodo to perform model validation studies and model-data comparisons,
- Enable model output utilization both on the cloud and on personal laptops in a variety of methods (e.g. through HAPI and interactive calls from the command line),
- Streamline the CCMC user workflow by becoming interoperable with other CCMC services (e.g. CAMEL and the various scoreboards),
- And become the next generation interface for CCMC users to interact with and analyze model outputs (e.g. through ROR and IR),

...all while keeping the developed software open-source and freely available. The Kamodo team also supports the heliophysics community by pursuing interoperability with commonly-used python packages, collaborating with community members to add model outputs and new functionalities, and remaining involved with community events (e.g. conferences, challenges, and research support). As the library of supported model outputs types expands and new model-agnostic tools are added, Kamodo will become a staple software package in the heliophysics community to transform current workflows into a more efficient and productive process. We are building the next generation of capability with Kamodo. Join us!

**Caveat for readers of this description.** It is a vision statement, so parts of it describe intent
rather than shipped code. "Simulated imagery" and "a line of sight calculation tool" have no
implementation at this revision (see Field 4). The description is nevertheless the maintainers' own
wording and is retained as written.

### 9. Concise Description (OPTIONAL)
- **Value:** A functional Python API from NASA's Community Coordinated Modeling Center for accessing, interpolating, unit-converting, and visualizing heliophysics/space-weather model outputs and data.
- **Source:** `setup.cfg` `description` ("A functional api for scientific data") expanded with the
  README, condensed to fit the field's 200-character limit. The bare `setup.cfg` string was rejected
  as a value on its own: it is the description `kamodo-core` also uses, so it does not identify this
  package or its heliophysics scope.

### 10. Publication Date (RECOMMENDED)
- **Value:** 2019-08-06
- **Verified:** the GitHub API reports `created_at: 2019-08-06T18:09:52Z` for `nasa/Kamodo` — the date
  of first public availability, which is what this field asks for. The JOSS software paper
  (2022-07-14) is a later event and is recorded as the Reference Publication (Field 14), not here.

### 11. Publisher (RECOMMENDED)
- **Organization:** Community Coordinated Modeling Center
- **Publisher Identifier:** https://ror.org/01dy3j343 (confirmed via the ROR API; the record's
  homepage is https://ccmc.gsfc.nasa.gov)
- **Note:** Kamodo is developed and published by NASA's CCMC at Goddard Space Flight Center and hosted
  under the `nasa` GitHub organization; the CCMC's own page states it "has been under development at
  the Community Coordinated Modeling Center (CCMC), NASA GSFC since May, 2018". The field's guidance
  to name Zenodo as publisher does not apply, because no Zenodo DOI exists for this software
  (Field 2). GitHub was considered as the repository host but rejected: CCMC is the actual publishing
  institution and carries a ROR.

### 12. Version (RECOMMENDED)
- **Version Number:** 25.12.1
- **Version Date:** 2026-07-01
- **Version Description:** Final release before major change to build system.
- **Version PID:** Not found — the release has no DOI (see Field 2).

**Why `25.12.1` and not `25.12.1-FINAL`.** The repository has exactly one tag and one GitHub release,
both named `25.12.1-FINAL`, published 2026-07-01T20:05:02Z from a tag created 2026-07-01T18:40:00Z.
The tag is a lightweight tag on commit `12a9cf51d750e327cc8ee50f2e303ea8c23f7a6d`, and
`git show 25.12.1-FINAL:setup.cfg` at that commit declares `version = 25.12.1`. The `-FINAL` suffix
is therefore a release-line label, not part of the version the package reports — a reading the
release body confirms in as many words: "Final release before major change to build system." The
version number is `25.12.1`; `-FINAL` is not stored.

**Why 2026-07-01 rather than the earlier CalVer inference.** The previous value, 2025-12-01, was
explicitly an inference from the CalVer string made when no tag was visible in the working clone.
That caveat no longer holds: the tag and release exist, and both are dated 2026-07-01. The version
*string* `25.12.1` was first written into `setup.cfg` on 2025-12-18 by commit
`973c80028205ac0673cbb2c30406c09f60d773de`, but this field asks for the date the version was
*released*, and the only release of `25.12.1` is the 2026-07-01 GitHub release. 2025-12-18 was
considered and rejected on that ground.

**Why not `26.07.1`.** `setup.cfg` on `master` reads `version = 26.07.1`, set by commit `cf8c8ae`
("Bump version from 25.12.1 to 26.07.1 before merging") on 2026-07-01. That in-development version has
no tag and no release, and at this revision sits 39 commits past the released tag. It is an unreleased
development version and must not be recorded as the released one.

**Why not the PyPI version.** PyPI `kamodo-ccmc` still tops out at 23.3.1 (uploaded 2023-03-23) and is
years behind the repository. It is not authoritative for the current version and was rejected as a
source. A future refresh should expect this to change: the release note and the substantially
rewritten `setup.py`/`pyproject.toml` (abi3 wheels, cibuildwheel, direct C/Fortran shared-library
compilation) point at a PyPI-publishing overhaul, after which PyPI may become authoritative again.

**Version Description provenance.** Taken verbatim from the GitHub release body for `25.12.1-FINAL`.
This field was previously "Not found" only because the release had not yet been located.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** — the primary language; `setup.cfg` declares `python_requires = >= 3.10` and the
  classifier `Programming Language :: Python :: 3.10`. 93 `.py` files plus 83 Jupyter notebooks.
- **C** — compiled interpolation extensions: 16 `.c` files with 7 `.h` headers across
  `readers/OCTREE_BLOCK_GRID/` (10 `.c`, 5 `.h`; AMR octree block search and interpolation for
  SWMF-GM) and `readers/Tri2D/` (6 `.c`, 2 `.h`; triangular-grid interpolation for the GAMERA
  reader). `setup.py` compiles both to shared libraries loaded via ctypes. The repository's eighth
  header, `kamodo-wrapper/KamodoWrapper.h`, belongs to the C++ wrapper and is cited under C++ below.
- **C++** — `kamodo-wrapper/KamodoWrapper.cpp` and `test.cpp` with `KamodoWrapper.h`.
- **Fortran90** — six `.f90` files: `kamodo-wrapper/FortranWrapper.f90`, `main.f90` and four
  `kamodo-wrapper/examples/*.f90`.
- **Fortran77** — the OpenGGCM reader sources `readers/OpenGGCM/readmagfile3d.f`, `read_b_grids.f` and
  `DBGDEV.F`.
- **Other** — retained from the stored record. It covers the parts of the codebase that have no row in
  the 19-value vocabulary: the 83-notebook Jupyter tutorial and documentation corpus (which GitHub's
  language statistics report as the single largest component by bytes), and the `kamodo-wrapper`
  Makefile and shell build glue.

**Previous incorrect value, corrected: `Typescript`.** This record used to list `Typescript`, and no
evidence supports it. **No TypeScript source exists anywhere in this repository**: `git ls-files` on
the checked-out revision finds zero `.ts`/`.tsx` files; `git ls-tree -r` finds zero on each of the
six remote branches (`master`, `develop`, `main`, `validation`, `gh-pages`,
`revert-156-fix/numpy2-compat`); and a whole-history `git log --all --diff-filter=A` sweep shows no
`.ts`/`.tsx` file has ever been added on any branch. GitHub's own language statistics for
`nasa/Kamodo` report only Jupyter Notebook, Python, C, Fortran, C++, Dockerfile, Makefile and Shell.
The value was removed for those reasons; the evidence is kept here so it is not re-added.

**Legacy JavaScript exists, and does not change that conclusion** — disclosed here so a future
refresh does not mistake it for evidence either way. `master`, the branch that produces the released
package, carries no `.js` file at all. Eleven distinct `.js` paths have been added across the
repository's history, in two unrelated groups: (a) Dash GUI assets of the older in-repo `kamodo/`
package layout that survives on `develop` and `main` — `kamodo/cli/assets/clientside.js` (added
2020-02-05) and `kamodo/cli/assets/MathJax.js` (added 2023-06-16); and (b) third-party assets
vendored into the generated documentation site on `gh-pages` — `js/html5shiv.min.js`,
`js/jquery-2.1.1.min.js`, `js/jquery-3.6.0.min.js`, `js/modernizr-2.8.3.min.js`, `js/theme.js`,
`js/theme_extra.js`, `search/lunr.js`, `search/main.js` and `search/worker.js`, all belonging to the
mkdocs `readthedocs` theme and its search index rather than to Kamodo. Neither group is TypeScript,
neither is part of the distributed package, and neither is authored Kamodo source, so neither
supports a `Typescript` or a `Javascript` entry in this field.

- Note on values previously rejected: "Jupyter Notebook" and bare "Python" were dropped because
  neither is a row in the `ProgrammingLanguage` vocabulary; the notebook corpus is covered by `Other`
  and the Python code by `Python 3.x`.

### 14. Reference Publication (RECOMMENDED)
- **Value:** https://doi.org/10.21105/joss.04053
- **Citation:** Pembroke, A., De Zeeuw, D., Rastaetter, L., Ringuette, R., Gerland, O., Patel, D., &
  Contreras, M. (2022). Kamodo: A functional API for space weather models and data. *Journal of Open
  Source Software*, 7(75), 4053.
- **Source:** the README's "Citing Kamodo" section lists it first, and Crossref confirms the volume,
  issue, article number and 2022-07-14 publication date.
- **Caveat worth knowing.** The JOSS paper's own "Repository" link points at
  `github.com/EnsembleGovServices/kamodo-core` and its archive is the kamodo-core Zenodo record, so
  strictly the paper describes `kamodo-core`. It is nonetheless the correct Reference Publication for
  this record because the maintainers designate it as *the* citation for Kamodo in this repository's
  README, and because its Acknowledgements are the authoritative funding statement for Kamodo as a
  whole (see Fields 25 and 26). The Frontiers flythrough paper and the ASR model-reader paper — both
  of which describe `kamodo_ccmc` specifically — are recorded under Related Publications (Field 27).

### 15. License (RECOMMENDED)
- **License (stored HSSI value):** `Other`
- **Actual license:** NASA Open Source Agreement Version 1.3 (SPDX: `NASA-1.3`)
- **Why `Other`.** The live `License` vocabulary has 11 rows — Apache License 2.0; BSD 2-Clause
  "Simplified" License; BSD 3-Clause "New" or "Revised" License; Creative Commons Attribution 4.0
  International; GNU General Public License v3.0 or later; GNU General Public Licenses (GPL version
  2); GNU Lesser General Public License v3.0 only; GNU Library or 'Lesser' General Public Licenses
  (LGPL version 2); MIT License; Other; Restricted. None of them is or approximates the NASA Open
  Source Agreement, so `Other` is the only correct selection, and this file carries the real license
  so the information is not lost. Do not substitute a near-miss row.
- **Evidence:** `setup.cfg` declares `license = NASA OPEN SOURCE AGREEMENT VERSION 1.3` and
  `license_files = LICENSE`; the `LICENSE` file is the full NOSA v1.3 text with "Government Agency:
  National Aeronautics and Space Administration", "Government Agency Original Software Designation:
  GSC-18210-1" and "Government Agency Original Software Title: Kamodo Analysis Suite". GitHub's own
  license detection reports `key: other`, `spdx_id: NOASSERTION`, corroborating that no standard SPDX
  row applies.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
heliophysics, space weather, model output, functionalization, unit conversion, interpolation,
visualization, satellite flythrough, coordinate transformation, field-line tracing, ionosphere,
thermosphere, magnetosphere, heliosphere, HAPI, model-data comparison, constellation mission
planning, radiation belts, particle precipitation, magnetosphere-ionosphere coupling, tsyganenko
model

- Keywords are stored lower-case and rendered in title case; the identities above are what matters,
  not the display casing.
- Keywords is the one open vocabulary in the form, so a new term becomes a permanent row. Each of
  the four terms below was matched to a row that already existed rather than minted as a
  near-duplicate, and each is tied to a capability the earlier keyword set predated:
  - `radiation belts` — the VERB-3D reader (`verb3d_4D.py`, `verb3d_tocdf.py`) and the `rbamlib` /
    `pyverbplt` dependencies, none of which existed when the earlier keyword set was assembled.
  - `particle precipitation` — the Ovation-Prime reader (`ovationprime_4D.py`), described in
    `model_wrapper.model_dict` as "an ionospheric empirical precipitation model driven by solar wind
    input data"; likewise a later addition to the package.
  - `magnetosphere-ionosphere coupling` — `kamodo_ccmc/filedriver/` reads SWMF-IE output and generates
    forcing input for GITM, WACCM-X and TIE-GCM; the SWMF-IE and OpenGGCM-IE readers cover the
    coupling region.
  - `tsyganenko model` — the containerized `readers/kamodo-tsyganenko/` wrapper.
- **Retained rejections:** the bare acronyms "CCMC" and "NASA" stay out; they are already carried by
  Publisher (Field 11) and Funder (Field 25).
- Field 22's controlled vocabulary cannot express several phenomena Kamodo genuinely supports. Where
  a phenomenon has no `Phenomena` row, this field is the correct home for it — see Field 22 for which
  ones were routed here.

### 17. Data Sources (OPTIONAL)
- **HAPI** — `readers/hapi.py` wraps `hapiclient` against arbitrary HAPI servers;
  `tools/functionalize_hapi.py` turns HAPI responses into Kamodo functions; the README states Kamodo
  "supports any data available through the HAPI interface".
- **HTTP/HTTPS Directories** — `readers/sat_extractions.py` queries the CCMC Runs-on-Request VMR
  service over `urllib` (`https://ccmc.gsfc.nasa.gov/RoR_WWW/VMR`), and CCMC hosts model output over
  plain HTTP directories.
- **S3/Cloud-aware** — `readers/reader_utilities.py` handles `s3://` paths directly with
  `s3fs.S3FileSystem` and `boto3.client('s3')` for both netCDF3 and netCDF4 objects; `s3fs` and
  `boto3` are declared dependencies.
- **CDAWeb** — `readers/hapi.py` documents `server2 = 'https://cdaweb.gsfc.nasa.gov/hapi'`
  as a supported endpoint; `examples/hapi.yaml` ships three ready-to-run CDAWeb reader configurations;
  `flythrough/SatelliteFlythrough.SatelliteTrajectory` is documented as retrieving trajectories "from
  HAPI/CDAWeb". The ASR paper states it plainly: "There are also readers in Kamodo for observational
  data such as datasets from CDAWeb … and satellite trajectories from SSCWeb".
- **SSCWeb** — `flythrough/SatelliteFlythrough.py` hard-codes
  `server = 'http://hapi-server.org/servers/SSCWeb/hapi'` for the `RealFlight` trajectory path;
  `plotfunctions.SatPosFig` and `SatOrbitPlane` do the same and direct users to the SSCWeb HAPI
  catalog; `hapi/HAPI_KamodoRealFlight.py` fetches the SSCWeb catalog to enumerate spacecraft.
- **Considered and not selected:**
  - **GFZ** — `filedriver/kp_reader.py` is documented as reading `kp_2000-2025.txt`, "built from data
    pulled from https://kp.gfz.de/en/data", and the repository ships that file plus `KP_Daily.npz`.
    Not selected because Kamodo implements no GFZ client: the data arrives as a bundled static file
    that a user refreshes by hand.
  - **OMNIWeb** — the Tsyganenko container mounts an `omni_data` volume and
    `scripts/initialize_pygeopack.py` calls `PyGeopack.Params.UpdateParameters()`. Not selected
    because the OMNI retrieval is performed by PyGeopack (recorded under Field 29), not by Kamodo.
  - `Observatory/Mission-specific` — not selected, consistently with Fields 31 and 32: Kamodo's
    data-access paths are generic multi-mission archives, not observatory-specific endpoints.

### 18. Input File Formats (RECOMMENDED)
- **netCDF3/4** — the dominant model-output and intermediate format, and genuinely *both*
  generations: the `*_tocdf.py` converters write netCDF4 (explicitly in adelphi, gitm, openggcm_gm,
  openggcm_ie, superdarn, swmfie and verb3d; by netCDF4-python default in ctipe and tiegcm) and
  netCDF3 (`format='NETCDF3_64BIT_OFFSET'` in waccmx, wamipe and weimer), and the matching `*_4D.py`
  readers consume them. `reader_utilities.py` branches on both netCDF3 and netCDF4 when reading,
  including over S3.
- **HDF5** — `.h5` model output via the declared `h5py` and `h5netcdf` dependencies.
- **ascii** — text/`.dat`/`.txt` model output (the SuperDARN uniform-grid reader documents "one ascii
  file per timestep per N/S hemisphere"), and tab-separated trajectory input via
  `SF_output.SFascii_reader` and `constellation.read_GDC_sattraj`.
- **csv** — `flythrough/SF_output.SFcsv_reader` reads comma-separated flythrough files, and
  `SF_read` explicitly dispatches on the `csv` extension, which is how `SatelliteFlythrough.MyFlight`
  ingests a user-supplied trajectory. csv was already recorded as an output format; it is equally an
  input format.
- **Other** — assorted native binary and model-specific formats, most concretely the VERB `.plt`
  files that `readers/verb3d_tocdf.py` parses through `pyverbplt.load_plt`, plus OpenGGCM binary
  output and GAMERA grid files.
- **CDF deliberately excluded, re-verified at this revision.** The `*_tocdf.py` naming is misleading:
  those modules write netCDF (netCDF4 in most, netCDF3_64BIT_OFFSET in waccmx, wamipe and weimer),
  never SPDF CDF. `cdflib` is declared in both `setup.cfg` and `requirements.txt` but is imported
  nowhere in the source — a
  fresh repository-wide grep at this revision finds it only in those two dependency lists and in one
  `conda install` line in `docs/notebooks/QuickStart.ipynb`. The earlier conclusion stands.

### 19. Output File Formats (RECOMMENDED)
- **netCDF3/4** — `SF_output.SFdata_tocdf` writes `.nc`; the converter family writes netCDF4
  intermediates that persist as user-facing artifacts.
- **csv** — `SF_output.SFdata_tocsv`.
- **ascii** — `SF_output.SFdata_toascii` writes tab-separated `.txt`.
- **Other** — formats with no vocabulary row: interactive plotly HTML and embeddable div files
  (`htmlfile`/`divfile` throughout the plotting API), static image export via kaleido, and — newly
  evidenced at this revision — Wavefront **OBJ** meshes, **MTL** materials and OpenSpace **`.asset`**
  scene files written by `tools/openspace.py` (`gmSaveOpenSpace`, `_write_obj_file`,
  `_write_colored_obj_file`, `_write_mtl_file`, `_write_openspace_asset`), and the `.npz`/trace files
  written by `vectorfieldtracer.save_traces_to_file`.
- The free-text value "Interactive HTML / Plotly figures" that this record once carried was replaced
  by `Other` because it is not a vocabulary row; that decision stands.

### 20. Operating System (RECOMMENDED)
- **Operating System Independent**
- **Evidence:** `setup.cfg` carries the classifier `Operating System :: OS Independent`; the README's
  installation section gives compiler instructions for Linux (apt `gcc gfortran`), macOS (Xcode CLT
  plus `brew install gcc`) and Windows (conda `m2w64-gcc-fortran`); `pyproject.toml`'s cibuildwheel
  configuration builds wheels for manylinux, macOS (with `MACOSX_DEPLOYMENT_TARGET = 11.0`) and
  Windows (with delvewheel repair).
- **Trap avoided:** the vocabulary row is `Operating System Independent` spelled out in full;
  `OS Independent` is not a value and would be rejected.

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**
- **Evidence:** no CPU-architecture constraint is declared anywhere in the packaging. The compiled
  C/Fortran components are built per-platform from source by `setup.py`, and cibuildwheel targets both
  `x86_64` and `aarch64` manylinux images plus macOS arm64 — i.e. the software is not tied to one
  architecture. `numba` JIT in `vectorfieldtracer.py` is optional and degrades to pure Python when
  absent. `GPU` was considered and rejected: there is no CUDA, ROCm or GPU-array code.

### 22. Related Phenomena (OPTIONAL)
**Geomagnetic Storms** and **Solar Wind**. This record previously held no phenomena at all, which
understated Kamodo's scope. The `Phenomena` vocabulary is **closed** — free text is rejected — and
has exactly seven rows: Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona,
Solar Flares, Solar Wind, X-ray emission. Two of the seven apply; the other five are rejected
below, with the reason.

- **Geomagnetic Storms** — the geospace models Kamodo functionalizes are storm-response models
  (SWMF-GM, OpenGGCM-GM, CTIPe, TIE-GCM, WACCM-X, WAM-IPE, VERB-3D radiation belts), and the
  high-latitude electrodynamics readers (SuperDARN TS18, ADELPHI, AMGeO, Weimer, Ovation-Prime) exist
  to characterise disturbed conditions. `filedriver/kp_reader.py` maintains a Kp geomagnetic-activity
  series to drive the coupling, and the `Validation/` notebooks and images work storm intervals.
- **Solar Wind** — solar-wind quantities are first-class throughout: the OpenGGCM-GM reader
  functionalizes plasma velocity, density and IMF components on a GSE grid; the SuperDARN reader
  exposes `E_sw` (solar-wind electric field); the AMGeO reader exposes OMNI-derived solar-wind speed
  and IMF; the Tsyganenko wrapper is driven by OMNI solar-wind parameters (`Vx`, `Vy`, `Vz` overrides
  documented in its README); and `plotfunctions.BlinesMovie(showSW=...)` renders solar-wind field
  lines.

**Rejected rows:** Coronal Heating, Coronal Mass Ejections, Solar Corona, Solar Flares and X-ray
emission — Kamodo has no solar or coronal model reader and no solar imaging or spectroscopy code.

**Phenomena routed to Keywords instead.** Earlier versions of this record listed free-text phenomena
that have no `Phenomena` row and would be rejected on submission: "Space weather", "Ionospheric
variability", "Thermospheric density (satellite drag)", "Auroral electrodynamics" and "Radiation belt
dynamics". Per the field's own guidance, a supported phenomenon with no row belongs in Keywords
(Field 16, the open vocabulary), where `space weather`, `ionosphere`, `thermosphere`,
`radiation belts` and `particle precipitation` now carry that information.

### 23. Development Status (RECOMMENDED)
- **Active**
- **Evidence at this revision:** HEAD `6706989574997795ce1b16b75af31c382eba0611` is dated 2026-08-07,
  with 19 commits dated after 2026-05-21; the GitHub API reports
  `pushed_at: 2026-08-07` and `archived: false`; a release was cut on 2026-07-01; and
  the repository is a PyHC **core** package rated "Good" for software maturity, documentation, Python
  3 support and license. Recent work is substantive rather than housekeeping: numpy ≥ 2.0 support, a
  rewritten build system producing abi3 wheels, and a 180-degree-longitude correction.

### 24. Documentation (RECOMMENDED)
- **Value:** https://nasa.github.io/Kamodo/ (verified reachable; site title "Kamodo Analysis Suite",
  page heading "Kamodo Documentation")
- **Also available:** `setup.cfg` `project_urls` names the same URL; `mkdocs.yml` builds it from the
  in-repo `docs/notebooks/` tutorials (Quick Start, Introduction, Data Functionalization, HAPI,
  Choosing Models and Variables, Satellite Trajectories, Coordinate Conversions, two Flythrough
  notebooks, the Constellation Mission Planning Tool, Advanced Plotting Routines, Contribution
  Guidelines and "How to Write a Model Reader"); the repository also carries `QuickStart.md`, 23
  `Tutorials/` notebooks (with 11 more archived under `Tutorials/_old/`), `Model_Onboarding_v3.pdf`, the CCMC page
  https://ccmc.gsfc.nasa.gov/tools/kamodo/ (verified reachable), and a YouTube tutorial playlist
  (verified reachable).

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80
- **Organization:** U.S. National Science Foundation
- **Funder Identifier:** https://ror.org/021nxhr62

**Evidence — the reference publication's Acknowledgements, which is the authoritative source.** The
JOSS paper states: "Development of Kamodo was initiated by the Community Coordinated Modeling Center,
with funding provided by Catholic University of America under the NSF Division of Atmospheric and
Geospace Sciences, Grant No 1503389. Continued support for Kamodo is provided by Ensemble Government
Services, LTD. via NASA Small Business Innovation Research (SBIR) Phase I/II, grant No 80NSSC20C0290,
80NSSC21C0585, resp. Additional support is provided by NASA's Heliophysics Data and Model
Consortium." The Frontiers paper's Funding section corroborates the NASA side and adds the per-author
detail: Ringuette via CCMC through ADNET Systems; De Zeeuw via CCMC through Catholic University of
America; Rastaetter and Garcia-Sage directly by CCMC; Pembroke and Gerland via the NASA SBIR contract.

**Roles deliberately not recorded as funders:**
- **Catholic University of America**, **ADNET Systems** and **Ensemble Government Services** are the
  recipient/employing institutions through which the NSF and NASA money flowed, not funders. They are
  correctly represented as author affiliations (Field 6).
- **NASA's Heliophysics Data and Model Consortium** is a NASA program, already covered by the NASA
  entry; it is also recorded as one of Ringuette's affiliations.
- The **Community Coordinated Modeling Center** is the developing institution and the record's
  Publisher (Field 11); the papers describe it as funding *through* NASA rather than as an
  independent funding source.
- The Frontiers Acknowledgments note that "The CINDI team was supported by NASA grant NAS5-01068" and
  that the CCMC "is a multi-agency partnership between NASA, AFMC, AFOSR, AFRL, AFWA, NOAA, NSF, and
  ONR". Neither is this software's funding: the first funds an *input dataset's* instrument team, and
  the second describes the host centre's general partnership. Recording either would misattribute
  funding. Noted so a later refresh does not sweep them in from a Crossref funding block.

### 26. Award Title (OPTIONAL)
- **Award Title:** Kamodo Containerized Space Weather Models
- **Award Number:** 80NSSC20C0290

- **Award Title:** Kamodo Containerized Space Weather Models
- **Award Number:** 80NSSC21C0585

- **Award Title:** U.S. National Science Foundation grant
- **Award Number:** 1503389

**Where the award numbers come from.** All three are stated in the reference publication's
Acknowledgements. The JOSS paper reads: "Development of Kamodo was initiated by the Community
Coordinated Modeling Center, with funding provided by Catholic University of America under the NSF
Division of Atmospheric and Geospace Sciences, Grant No 1503389. Continued support for Kamodo is
provided by Ensemble Government Services, LTD. via NASA Small Business Innovation Research (SBIR)
Phase I/II, grant No 80NSSC20C0290, 80NSSC21C0585, resp." So the two NASA awards are the SBIR
Phase I and Phase II contracts, and 1503389 is the NSF Division of Atmospheric and Geospace Sciences
grant. The funders themselves are recorded in Field 25.

**Titles for the two NASA SBIR awards.** `80NSSC20C0290` carries the title quoted identically by two
independent sources: the ASR/arXiv paper ("a NASA SBIR Phase 2: Space Weather R2O/O2R Technology
Development grant titled 'Kamodo Containerized Space Weather Models' (Contract #80NSSC20C0290)
awarded to Ensemble Consultancy") and the Frontiers Funding section (same title, "awarded to
Ensemble Government Services, LLC"). Crossref's funding block on `10.1016/j.asr.2023.03.033`
independently records NASA award 80NSSC20C0290, corroborating the number but supplying no title.
`80NSSC21C0585` carries the same title, and it is sourced independently: the official published
award record at https://www.sbir.gov/awards/189296 gives its title as "Kamodo Containerized Space
Weather Models". The two awards therefore hold the same title in this record on the authority of
their own award records, not by transcription from one another. That is not a duplication error and
should not be "corrected" to differ.

**Why the NSF award is stored under a display title.** NSF's formal title for award 1503389 is:

> The Community Coordinated Modeling Center: Ionosphere-Thermosphere-Mesosphere Models, Applications
> and Services for Research, Forecasting and Analysis

That is the wording of the official record at
`https://api.nsf.gov/services/v1/awards.json?id=1503389`. It runs to 150 characters, and HSSI's
`Award.name` column is capped at 128, so the formal title does not fit and cannot be the stored
value. `U.S. National Science Foundation grant` (38 characters) is the display title that stands in
for it — a deliberate consequence of that cap rather than an imprecise reading of the source. The
formal title is preserved above so the award stays identifiable, and so a later refresh does not
put it forward as a value: it will not fit, and the attempt fails at the database write rather than
at validation, where the cause would be easier to see.

**Upstream defect worth reporting: JSON-LD renders at most one award, and drops award identifiers.**
The record's JSON-LD funding serialization has two problems that are independent of the values above.
First, the per-award `grant` dictionary is assembled from the award's `identifier` and `funder` and
then never assigned anywhere, so award identifiers and per-award funders do not reach the output at
all. Second, a `break` after the first award ends the loop, so only one award is ever serialized.
The consequence for Kamodo is that its JSON-LD understates its funding: two of the three awards
never reach the output, and the one that does reaches it without its identifier or its funder. The
defect is in the serializer, not in this record's award list, and is worth reporting upstream.

**Discrepancy left visible rather than resolved.** The JOSS paper labels 80NSSC20C0290 as SBIR
**Phase I** and 80NSSC21C0585 as **Phase II**; the ASR and Frontiers papers both call 80NSSC20C0290 a
**Phase 2** grant. The phase labelling conflicts between first-party sources. It does not affect the
award numbers or the recorded titles, so nothing is asserted about phase here.

**This field was previously "Not found" on the stated ground that "no award/grant number [is] stated;
implicit NASA institutional funding."** That conclusion was wrong, and is corrected here: three award
numbers are stated outright in the reference publication's Acknowledgements. The earlier extraction
had not read the JOSS paper's back matter.

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **https://doi.org/10.3389/fspas.2022.1005977** — Ringuette, R., De Zeeuw, D., Rastaetter, L.,
  Pembroke, A., Gerland, O., & Garcia-Sage, K. (2022). Kamodo's model-agnostic satellite flythrough:
  Lowering the utilization barrier for heliophysics model outputs. *Frontiers in Astronomy and Space
  Sciences*, 9. Describes the flythrough subsystem in this repository.
- **https://doi.org/10.1016/j.asr.2023.03.033** — Ringuette, R., Rastaetter, L., De Zeeuw,
  D., Pembroke, A., & Gerland, O. (2023). Kamodo: Simplifying model data access and utilization.
  *Advances in Space Research*, 72(12), 5682–5706. This is the **published** version of the paper the
  README still lists as "Adv. Space. Res. under review" and that this record previously carried only
  as an arXiv preprint. It is the definitive description of the `kamodo_ccmc` model readers, and its
  Acknowledgements supply the title for award 80NSSC20C0290 in Field 26.
- **https://doi.org/10.48550/arxiv.2303.00854** — Ringuette, R., et al. (2023). Kamodo: Simplifying
  model data access and utilization (arXiv preprint). It is the same work as the ASR article above,
  and collapsing the two into one entry was considered and rejected. Both are kept because they
  serve different readers: the preprint is what the README's citation list points at, it is openly
  readable where the publisher version is not, and it is the version already stored in the record.
  The ASR DOI is the citable version of record. A future refresh should keep both rather than
  "deduplicating" them.

**Considered and not added:**
- **https://doi.org/10.22541/essoar.167214257.73153757/v1** — Ringuette et al. (2022), "Kamodo's
  Satellite Constellation Mission Planning Tool (AGU 2022)", an ESSOAr posted-content record for a
  conference poster. It is listed in the README's "Citing Kamodo" section and is cited directly in
  the `Constellation` class docstring as the reference for the reconstruction method, so it has a
  genuine claim. Not added because it is a poster abstract rather than a publication, and the
  Frontiers and ASR papers already cover the same functionality peer-reviewed. Recorded here so the
  next refresh can add it deliberately rather than rediscover it.
- The Zenodo presentation records `10.5281/zenodo.11121935` / `.11121936` ("Kamodo: A CCMC Open
  Source Toolkit for Space Physics Simulation Output", 2024) — conference presentations, and already
  accounted for under Field 2.

### 28. Related Datasets (OPTIONAL)
- **https://ccmc.gsfc.nasa.gov/RoR_WWW/output_files/KAMODO_DEMO/** — the CCMC-hosted sample model
  outputs for Kamodo.
- **Upstream link rot, recorded deliberately.** As of 2026-08-13 this URL returns **404**. The parent
  directory `https://ccmc.gsfc.nasa.gov/RoR_WWW/output_files/` still returns 200 and its listing no
  longer contains a `KAMODO_DEMO` entry, so the data has been moved or withdrawn rather than the host
  being down. Probes of several plausible relocations (`/kamodo_demo/`, `/tools/kamodo/KAMODO_DEMO/`,
  the un-slashed form) all 404. The value is **kept anyway**: it is what the README's Resources
  section still advertises and what the Frontiers paper's Data Availability Statement cites as the
  archival location of the analysed data, so it remains the citable identifier for that dataset even
  while the server path is broken. Removing it was considered and rejected: no replacement location
  exists to substitute, and dropping the value would erase the link between this record and the
  dataset the reference literature analyses. A future refresh should re-probe it and substitute only
  if CCMC publishes a replacement path — the 404 alone is not a reason to delete the entry.
- **Model outputs Kamodo is built to read** (context for this field, not separate entries): ADELPHI,
  AMGeO, CTIPe, DTM, GITM, IRI, Ovation-Prime, OpenGGCM-GM, OpenGGCM-IE, SuperDARN (uniform and
  equal-area TS18 grids), SWMF-IE, SWMF-GM, TIE-GCM, WACCM-X, WAM-IPE, Weimer, VERB-3D, plus the
  containerized JB2008 and Tsyganenko wrappers — enumerated from
  `flythrough/model_wrapper.model_dict` and `Choose_Model` at this revision. GAMERA-GM has a reader
  (`gameragm_4D.py`, `gameragm_grids.py`) but `model_dict` still annotates it "(coming soon)".
- **Correction to an earlier claim.** This record previously listed **SAMI3** and **Enlil** among
  supported model outputs. Neither has a reader: `model_dict` and `Choose_Model` contain no entry for
  either, and no `sami3`/`enlil` module exists under `kamodo_ccmc/readers/`. The claim came from the
  PyHC core registry's keyword list for Kamodo, which still carries `sami3`, `enlil` and `solar`;
  those keywords are aspirational or stale and should not be treated as reader evidence.
- **Also read by Kamodo:** any dataset served over HAPI, CDAWeb datasets and SSCWeb trajectories
  (Field 17), and CCMC Runs-on-Request satellite extractions via `readers/sat_extractions.py`.

### 29. Related Software (OPTIONAL)
- **kamodo-core** — https://pypi.org/project/kamodo-core/ — the functional core that `kamodo_ccmc` is
  built on and declares as its first `install_requires` entry (as `kamodo`). It is a separate product
  with its own JOSS paper and its own Zenodo software DOI. **Why this URL.** Two arguably
  better identifiers exist and were both considered and rejected: the live repository
  **https://github.com/nasa/Kamodo-core** (reachable and actively pushed), and the concept DOI
  **https://doi.org/10.5281/zenodo.6773394**, which is more durable than any URL. Neither was
  adopted because the stored PyPI URL resolves, is neither stale nor wrong, and tracks the
  installable artifact (currently 1.0.11) — swapping it would be churn without gain. Both
  alternatives are recorded here so a future refresh has them ready if the PyPI URL ever rots. Note
  which URLs are already dead: the JOSS paper's own repository link
  `github.com/EnsembleGovServices/kamodo-core` returns 404, and so does
  `github.com/ensemblegov/kamodo-core`, the successor recorded in the PyPI project metadata.
- **Kameleon** — https://ccmc.gsfc.nasa.gov/tools/kameleon/ — **Kamodo's predecessor.** The
  reference publication states it outright: the Kameleon software suite was "a predecessor to
  Kamodo developed between 1999-2011 at the Community Coordinated Modeling Center, NASA GSFC"
  (Maddox, M. M., Berrios, D. H., Rastaetter, L., & Pembroke, A. (2013). Kameleon software suite
  (Version 6.1.0) [Computer software]), and the JOSS paper devotes most of its Statement of Need to
  what Kameleon did — converting raw simulation output to standardized HDF or CDF with space-weather
  metadata, and offering C, C++, Fortran, Java and Python interpolation APIs — and to why its
  per-model hand-written interpolators became an onboarding bottleneck that "were a strong
  motivating factor for Kamodo's functional design". Field 29's scope explicitly covers predecessor
  relationships, and two of Kameleon's authors (Rastaetter, Pembroke) are Kamodo authors.
  **URL note:** the URL the JOSS reference itself cites,
  `https://ccmc.gsfc.nasa.gov/Kameleon/Overview.html`, now returns 404, as does
  `github.com/nasa/Kameleon`. The CCMC tool page above is the live first-party location and is what
  is recorded; do not restore the JOSS-cited URL on a later refresh.
- **SGP4** — https://github.com/brandon-rhodes/python-sgp4 — `flythrough/SatelliteFlythrough.py`
  imports `sgp4.api.Satrec` and `days2mdhms` and calls `satellite.sgp4(jd, 0.0)` to propagate orbits
  from TLEs in `TLETrajectory`/`TLEFlight`. A domain-specific orbital-mechanics dependency, not
  generic infrastructure.
- **PyGeopack** — https://github.com/mattkjames7/PyGeopack — the backend of Kamodo's Tsyganenko
  reader: `readers/kamodo-tsyganenko/kamodo_geopack/tsyganenko.py` does `import PyGeopack as gp`, the
  wrapper's own README credits it, and the reader's generated citation string names it.
- **pyverbplt** — https://github.com/radiation-belts/pyverbplt — `readers/verb3d_tocdf.py`
  does `import pyverbplt` and calls `pyverbplt.load_plt(...)` to parse VERB `.plt` grid and
  phase-space-density files. This is the format-specific parser that makes the VERB-3D reader
  possible, and `setup.cfg` pins `pyverbplt>=24.9`. Domain-specific by construction: its PyPI summary
  is "Python library designed to load `.plt` files, created by the Versatile Electron Radiation Belts
  (VERB) code".
- **rbamlib** — https://github.com/radiation-belts/rbamlib — declared in `setup.cfg` and
  exercised by `tests/test_verb4d.py`, which uses `rbamlib.conv.Lal2K` and `rbamlib.conv.en2mu` for
  radiation-belt adiabatic-invariant conversions. Its PyPI summary: "A lightweight, open-source
  Python library for the analysis and modeling of radiation belts."
- **Deliberately excluded, with reasons:**
  - **SpacePy, Astropy and hapiclient** — real and important runtime dependencies (coordinate
    conversion, time handling, HAPI access), but the 2026-06-10 reconciliation judged them ordinary
    dependencies rather than *distinguishing* related software, and nothing at this revision changes
    that. Left excluded rather than relitigated.
  - **numpy, pandas, scipy, plotly, matplotlib, netCDF4, h5py, h5netcdf, numba, psutil, boto3, s3fs,
    setuptools, nbformat, cdflib** — generic scientific-Python and infrastructure packages. Listing
    them would say nothing that is not equally true of most Python packages.
  - **pysat** — belongs under Interoperable Software (Field 30), not here.

### 30. Interoperable Software (OPTIONAL)
- **pysat** — https://github.com/pysat/pysat — a demonstrated two-way exchange, not a dependency.
  `kamodo-pysat.yaml` in the repository root configures a `pysat_kamodo.Pysat_Kamodo` model class
  binding a pysat instrument (platform `cnofs`, name `vefi`, tag `dc_b`) into Kamodo, and
  `Tutorials/Kamodo_pysat_ModelDataComparison.ipynb` is a worked model–data comparison across the two.
  The ASR paper states the relationship explicitly: "The CCMC team is collaborating with the pysat
  developers to extend their capability through a link to Kamodo, and have established
  interoperability with pysat", and the Frontiers Acknowledgments thank pysat's lead developer for
  comments on the pysat–Kamodo notebooks.
- **OpenSpace** — https://github.com/OpenSpace/OpenSpace — `kamodo_ccmc/tools/openspace.py`
  is a purpose-built exporter from Kamodo into the OpenSpace astrovisualization software.
  `gmSaveOpenSpace` and `gmSaveOpenSpaceIndexed` convert computed magnetopause, bow-shock and slice
  surfaces into a Wavefront `.obj` mesh, an optional `.mtl` material for vertex colours, and an
  OpenSpace `.asset` scene file. The asset is not generic: it emits
  `asset.require("scene/solarsystem/planets/earth/transforms_gsm_sm")`, parents the surface to
  OpenSpace's `GeocentricSolarMagnetospheric` frame, and declares a
  `Renderable = { Type = "RenderableModel", GeometryFile = …, MaterialFile = …, TimeFrame = … }`
  block against OpenSpace's own scene schema. That is a concrete, named cross-tool exchange.
- **Considered and not added:** blanket claims of the form "part of the scientific Python ecosystem"
  or "a PyHC core package, therefore interoperable with PyHC packages" carry no information and are
  not used. `pysatModels`, referenced in the ASR paper's footnotes as the pysat-side model bridge,
  was considered; pysat is the named counterpart in the repository's own configuration and notebook,
  so it is the entry recorded.

### 31. Related Instruments (OPTIONAL)
- **Value:** Not found
- **Conclusion re-tested against the current source, not inherited.** Kamodo is instrument-agnostic
  by design. All nineteen entries in `flythrough/model_wrapper.model_dict` are models, and every
  reader module under `kamodo_ccmc/readers/` targets model output or a generic multi-mission
  archive rather than one instrument's data. There is no
  instrument-specific parser, calibration routine, or response model anywhere in the package.
- **Specific candidates examined and rejected, each with its reason:**
  - **SuperDARN** — the closest call, and the one most likely to be re-proposed. Kamodo ships five
    SuperDARN modules (`superdarnuni_4D.py`, `superdarnequ_4D.py`, `superdarn_tocdf.py`,
    `superdarnequ_interp.py`, `superdarn_rename.py`) and SPASE rows exist that would resolve cleanly
    (`https://spase-metadata.org/SMWG/Observatory/SuperDARN`,
    `https://spase-metadata.org/SMWG/Instrument/SuperDARN/Radars`). Rejected because what Kamodo reads
    is not radar data: the converter's file header records `Model: TS18`, i.e. the Thomas & Shepherd
    2018 *statistical convection model* distributed by CCMC as gridded output, and the reader
    docstring calls it "SuperDARN model data … model output". Kamodo parses no `rawacf`/`fitacf` and
    performs no radar processing; someone holding SuperDARN radar data would not reach for it. It is
    classified instead under `Models and Simulations: Empirical`.
  - **AMPERE / Iridium** — ADELPHI is "AMPERE-Derived ELectrodynamic Properties of the High-latitude
    Ionosphere", an empirical product derived from AMPERE observations, and Kamodo reads ADELPHI
    output files. Rejected for the same reason: Kamodo supports the derived model, not the Iridium
    magnetometer data. (SPASE rows exist for both, so this is a relevance judgement, not a resolution
    failure.)
  - **C/NOFS CINDI/VEFI, GRACE, GOES, DMSP, MMS, Cluster, ISS, ICON, RBSP** — these appear only in
    tutorials, demo notebooks, docstring examples and example configuration files, as illustrations
    of the *generic* HAPI and SSCWeb readers: `readers/hapi.py`'s module docstring (grace1 from
    SSCWeb, `GOES12_K0_MAG` from CDAWeb), `examples/hapi.yaml` (GOES12, DMSP-F16, MMS1, grace1),
    `Tutorials/RealFlightDemo.ipynb` and the pysat notebook (`cnofs`),
    `Tutorials/ConstellationTutorial_IrregularConstellations.ipynb` (dmspf15–f18),
    `Tutorials/VERB-3D_plotting_examples.ipynb` (rbspa), `docs/notebooks/Files/DMSPOrbits.txt`. The
    relevance gate excludes tutorial and demo mentions, and excludes generic multi-mission archives —
    those belong to Data Sources, where CDAWeb and SSCWeb are now recorded (Field 17).
  - **GDC (Geospace Dynamics Constellation)** — `tools/constellation.py` defines
    `read_GDC_sattraj(filename)`. Rejected on two independent grounds: the function is a plain
    tab-delimited trajectory-file reader with nothing GDC-specific in its logic, and the
    `InstrumentObservatory` vocabulary contains no GDC row at all (searches for both "gdc" and
    "geospace dynamics" return zero rows of either type).
- **Never emit a bare name.** Fields 31 and 32 are SPASE-only. A name recorded without an
  `https://spase-metadata.org/` identifier does not associate with the intended resource — it either
  binds to an arbitrary same-name row or creates a new identifierless row. An empty field is the
  correct outcome here; an invented one would be a defect.

### 32. Related Observatories (OPTIONAL)
- **Value:** Not found
- Same analysis as Field 31, and the same conclusion. No observatory or mission platform is a target
  of this software: Kamodo's spacecraft-facing code paths
  (`SatelliteFlythrough.SatelliteTrajectory`, `RealFlight`, `plotfunctions.SatPosFig`,
  `SatOrbitPlane`, `hapi/HAPI_KamodoRealFlight.py`) all take an arbitrary dataset identifier from the
  SSCWeb HAPI catalog and work equally for any spacecraft in it. That generality is precisely why
  `SSCWeb` and `CDAWeb` belong in Data Sources rather than here.
- This is a relevance decision, not a resolution failure, and the distinction matters for a future
  refresh. Seven of the entities considered each resolve to exactly one SPASE observatory row:
  `https://spase-metadata.org/SMWG/Observatory/SuperDARN`, `.../SMWG/Observatory/AMPERE`,
  `.../SMWG/Observatory/GRACE` (which also has the usual `.html` duplicate, normalising to the bare
  form), `.../SMWG/Observatory/ISS`, `.../SMWG/Observatory/CNOFS`, `.../SMWG/Observatory/ICON` and
  `.../SMWG/Observatory/RBSP` (row name "Van Allen Probes"). Each could have been recorded without
  ambiguity; none should be, for the reasons given in Field 31. The remaining families —
  GOES, DMSP, MMS and Cluster — each have a bare top-level observatory row *plus* fifteen to twenty
  per-spacecraft rows, so they would need in-repo version evidence to resolve. That evidence does
  not exist here and would not matter if it did, because those names come only from demo
  configurations. Recorded so a future refresh does not mistake the multi-row situation for the
  reason the field is empty; relevance is the reason.

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/nasa/Kamodo/master/docs/notebooks/Files/Kamodo.png
- **Verified reachable** at this revision. This is the logo the README displays in its header banner
  alongside the CCMC logo, which is why it is preferred over the alternatives.
- **Alternatives:** the repository also carries `logos/Kamodo1.png`, `Kamodo2.png` and `Kamodo3.png`;
  the PyHC core registry points at
  `https://raw.githubusercontent.com/nasa/Kamodo/master/logos/Kamodo2.png`. Either would be
  defensible; the stored value is kept because it is the one the project puts at the top of its own
  README.

---

## Provenance and Sources

- **No `CITATION.cff`, `codemeta.json`, `.zenodo.json`, `AUTHORS` or `CONTRIBUTORS` file** exists in
  this repository, and a whole-history sweep (`git log --all --diff-filter=A`) shows none has ever
  been added on any branch. Author, identifier and citation metadata therefore has to be assembled from
  `setup.cfg`, the README (including its team section and "Citing Kamodo" list), the LICENSE, the four
  Kamodo publications, in-source `@author:` headers, ORCID, ROR and the PyHC core registry. A future
  refresh should re-check for these files first — adding one upstream would make several fields
  directly authoritative.
- **PyHC registry**: Kamodo is a PyHC **core** package (`_data/projects_core.yml`), with `code`,
  `docs` and `url` matching Fields 3, 24 and the CCMC page, `contact: Darren De Zeeuw`, and "Good"
  ratings for documentation, software maturity, Python 3 and license. Its keyword list is a useful
  cross-check but is not reader evidence — see the SAMI3/Enlil correction in Field 28.
- **Repository shape at this revision**, for orientation: 93 Python modules, 83 Jupyter notebooks,
  16 C sources with 8 headers, 6 Fortran 90 and 3 Fortran 77 sources, 2 C++ sources, 8 Dockerfiles,
  and a `tests/` suite of 11 pytest modules covering ADELPHI, AMGeO, CTIPe, DTM, GITM, IRI, SWMF-GM,
  SWMF-IE, TIE-GCM, VERB-3D and the time utilities.
