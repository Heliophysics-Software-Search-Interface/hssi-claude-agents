# HSSI Metadata Extraction Results

**HSSI Software ID:** 6ad99ded-e693-4660-a1c5-86ead53a9bcf
**Repository:** https://github.com/ESCOMP/CESM
**Source Revision:** 926b9403ae276ec29e7b61ee458aa0bb1ca0d3c3
**Extraction Date:** 2026-07-30
**Validation Date:** 2026-07-30
**Validation Status:** PASS

This canonical file records the validated HSSI state as of 2026-07-30. It was seeded from the prior
record and reconciled against the pinned source revision and authoritative external sources.

**Scope note.** CESM is a top-level coupled Earth system model whose repository pins external
component repositories via `git-fleximod`/`.gitmodules` rather than vendoring their source. The
working clone has not run `./bin/git-fleximod update`, so `components/`, `cime/`, `share/` and
`ccs_config/` are empty by design. Evidence below is drawn from the top-level repository, its pinned
component manifest, its versioned documentation, and authoritative CESM/NCAR/UCAR sources. Metadata
scope is **CESM itself**, not the individual components.

**Controlled vocabularies.** Every controlled-list value written below was confirmed against the
live HSSI vocabulary during validation.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)

- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

---

### 2. Persistent Identifier (RECOMMENDED)

**Value:** `https://doi.org/10.5281/zenodo.11229775`

**Evidence.** Re-verified against the Zenodo API on 2026-07-30: `GET
https://zenodo.org/api/records/11229775` returns `conceptrecid: "11229775"` and
`conceptdoi: "10.5281/zenodo.11229775"`. This is the concept (all-versions) DOI, which is the form
Field 2 asks for, so it is preferred over the single version DOI `10.5281/zenodo.11229776`
("CESM-release-cesm2.2.0", publication_date 2024-05-21) that is the only version deposited under it.

**Note.** No DOI badge, `CITATION.cff`, or `codemeta.json` exists anywhere in the repository; the
Zenodo deposit is the only persistent identifier for the software.

---

### 3. Code Repository (MANDATORY)

**Value:** `https://github.com/ESCOMP/CESM`

**Why the replacement.** The stored value is not a code repository at all — it is the marketing page
for **CCSM**, the *predecessor* model that CESM superseded. It exposes no source code and no
checkout instructions. The authoritative repository is `https://github.com/ESCOMP/CESM`:

- `README.rst:98` — the official download procedure is `git clone https://github.com/escomp/cesm.git
  my_cesm_sandbox`, followed by `git tag` / `git checkout <tag>` / `./bin/git-fleximod update`
  (`README.rst:103-119`).
- `README.rst:90` — "CESM is now released via github."
- `git remote -v` in this clone → `https://github.com/ESCOMP/CESM.git`.
- `GET https://api.github.com/repos/ESCOMP/CESM` (2026-07-30) → `full_name: ESCOMP/CESM`,
  `html_url: https://github.com/ESCOMP/CESM`, `description: "The Community Earth System Model"`,
  `homepage: http://www.cesm.ucar.edu/`, `default_branch: cesm3.0-alphabranch`,
  `created_at: 2017-11-15`, `pushed_at: 2026-07-20`, `archived: false`, `fork: false`,
  `topics: [climate, climate-model, ncar]`. (Star and fork counts are deliberately not recorded —
  they are live metrics, not durable facts, and drifted during validation.)
- SoMEF 0.9.11 (`somef describe -t 0.7 -r https://github.com/ESCOMP/CESM`) independently reports
  `code_repository = https://github.com/ESCOMP/CESM` at confidence 1.

The superseded CCSM URL is not discarded — it is carried into Field 29 (Related Software), where a
predecessor model belongs.

---

### 4. Software Functionality (MANDATORY)

**Values (18):**

- `Models and Simulations`
- `Models and Simulations: First Principles`
- `Models and Simulations: Physics-Based`
- `Models and Simulations: Data Guided`
- `Models and Simulations: Forecasting`
- `Models and Simulations: Observatory/Instrument Models`
- `Models and Simulations: Instrument Response`
- `Models and Simulations: ML/AI`
- `Data Processing and Analysis`
- `Data Processing and Analysis: Analysis`
- `Data Processing and Analysis: Data Assimilation`
- `Data Processing and Analysis: Data Access and Retrieval`
- `Data Processing and Analysis: Processing`
- `Data Visualization`
- `Data Visualization: 2D Graphics`
- `Data Visualization: Line Plots`
- `Servers and Environments`
- `Servers and Environments: High Performance Computing`

**Version-scope policy for this field.** Field 4 describes the software's capabilities **as they exist
at the recorded Source Revision** (`926b9403ae276ec29e7b61ee458aa0bb1ca0d3c3`, repository HEAD),
because HSSI carries **one Software Functionality set per software, not one per version**. Field 12
records a specific release (`2.1.5`); Field 4 does not, and scoping it to that release would silently
discard capabilities the software demonstrably has today. Four values below rest on tooling that
exists at HEAD but **not** in `release-cesm2.1.5` — `Models and Simulations: ML/AI` (FTorch), and
`Data Processing and Analysis: Processing`, `Data Visualization: 2D Graphics` and `Data
Visualization: Line Plots` (all three CUPiD). Each carries the identical `HEAD-only` scope note
below, applied uniformly. Every other value is present at both HEAD and `release-cesm2.1.5`.

**Per-value evidence**

| Value | Evidence |
|---|---|
| Models and Simulations | Seeded value, retained. `doc/source/introduction.rst:59-64` — "The Community Earth System Model (CESM) is a coupled climate model for simulating Earth's climate system." |
| Models and Simulations: First Principles | Prognostic components solve the governing equations of geophysical fluid dynamics, thermodynamics and radiative transfer: `.gitmodules` pins CAM (atmosphere, `cam6_4_187`), MOM6 (ocean, `mi_260715`), CICE (sea ice, `cesm3_cice6_6_3_16`), CTSM (land, `ctsm5.4.042`), CISM (land ice, `cismwrap_2_2_015`), WW3 (waves, `main_0.1.0`). `doc/source/introduction.rst:61-63` — "separate models simultaneously simulating the Earth's atmosphere, ocean, land, river run-off, land-ice, and sea-ice". |
| Models and Simulations: Physics-Based | CESM couples first-principles dynamics with physical parameterizations (radiation, convection, gravity waves, cloud microphysics, sea-ice thermodynamics). `LICENSE.txt:29-34` separately licenses the **AER RRTMG** radiative transfer code, evidencing shipped physics parameterizations. |
| Models and Simulations: Data Guided | CDEPS supplies data/stub versions of any component so the model can be driven by observations and reanalyses: `.gitmodules:92-97` pins `cdeps1.0.101`. Compset grammar exposes this to users — `cime_config/config_compsets.xml:16-22` lists `LND = [CLM45, CLM50, SLND]`, `OCN = [MOM6, DOCN, SOCN]`, `ICE = [CICE, DICE, SICE]`, `WAV = [WW3, DWAV, XWAV, SWAV]`; `cime_config/config_compsets.xml:87` uses `DGLC%NOEVOLVE`; `:130,:139` use `DOCN%SOM`. Historical (`HIST_`) and scenario (`SSP*_`) compsets are driven by prescribed observed/CMIP6 forcings. |
| Models and Simulations: Forecasting | CESM is configured for initialized seasonal-to-multiyear *prediction* and forward scenario projection. `git show release-cesm2.1.5:cime_config/config_compsets.xml` defines the SMYLE (Seasonal-to-Multiyear Large Ensemble) prediction compsets `BSMYLE` and `BWsc1850smyle`, and the future-scenario compsets `BWSSP126/245/370/585/534os` plus their 2300 extensions. The 2.1.5 GitHub release notes list "add smyle compset BWsc1850smyle" and "Adding BSMYLE compset and definitions to config_compsets.xml". |
| Models and Simulations: Observatory/Instrument Models | CESM ships **COSP** (the CFMIP Observation Simulator Package), which generates synthetic satellite observables from model state. `doc/source/downloading_cesm.rst:91` lists `cosp2` among the CESM externals and `:100` gives its checkout path `./components/cam/src/physics/cosp2/src`; `.lib/git-fleximod/README.md:69-82` documents the `cosp2` submodule from `https://github.com/CFMIP/COSPv2.0`. `LICENSE.txt:82-87` separately licenses the **ISCCP Simulator Software**, a COSP instrument simulator, as a CESM-bundled component. |
| Models and Simulations: Instrument Response | Same COSP evidence. COSP simulators emulate each instrument's sampling and retrieval behaviour (ISCCP cloud-top-pressure retrieval, lidar attenuation, radar reflectivity) so model fields are directly comparable to satellite retrievals. **No version-scope caveat applies**: COSP is present at both HEAD and the production release — `Externals_CAM.cfg` at `cam_cesm2_1_rel_60` (the CAM tag pinned by `release-cesm2.1.5`, per `git show release-cesm2.1.5:Externals.cfg`) declares `[cosp2] repo_url = https://github.com/CFMIP/COSPv2.0`, `tag = v2.1.4cesm`, `required = True` (fetched and confirmed 2026-07-30). |
| Models and Simulations: ML/AI | `.gitmodules:169-175` pins `FTorch` → `https://github.com/ESCOMP/FTorch_interface` at `v0.0.5`, the CESM interface to FTorch, which lets Fortran components call PyTorch models (ML emulators and parameterizations). Also `fxrequired = ToplevelOptional`. **HEAD-only:** present at the recorded Source Revision but not in `release-cesm2.1.5` — see the version-scope policy above. |
| Data Processing and Analysis | Parent for the three subcategories below. |
| Data Processing and Analysis: Analysis | **CESM-ECT** (CESM Ensemble Consistency Test) performs statistical analysis of model output to decide whether a new machine/compiler configuration is statistically distinguishable from a trusted ensemble: `tools/statistical_ensemble_test/README:1-25`, `tools/statistical_ensemble_test/ensemble.py`, and `.gitmodules:155-160` pinning `pysect` → `https://github.com/NCAR/PyCECT` at `3.3.1`. This capability is not new to CESM3 — in the 2.1.x line the same tool shipped inside CIME (`GET https://api.github.com/repos/ESMCI/cime/contents/tools?ref=cime5.6.49` lists `statistical_ensemble_test`), the CIME tag pinned by `release-cesm2.1.5`. |
| Data Processing and Analysis: Data Assimilation | CESM provides a first-class DART coupling path. `cime_config/config_compsets.xml:13,23` define the `_ESP%phys` (External System Processing) component slot with `ESP = [SESP]` — the DART coupling slot. `cime_config/config_compsets.xml:95-101` defines the dedicated compset `BHISTC_LT_DART`. `cime_config/testmods_dirs/allactive/DART_BHIST_lowres/` (6 files, incl. `README_layout`, `shell_commands`, `user_nl_cam`, `user_nl_clm`, `user_nl_mosart`) configures the multi-instance (MCC) ensemble layouts DART assimilation requires. |
| Data Processing and Analysis: Data Access and Retrieval | CESM retrieves its input data (initial, boundary and forcing datasets) from remote servers as a user-facing step (`./check_input_data --download`). The server list is CESM's own, shipped in the pinned `ccs_config` submodule (`.gitmodules:29-34`, `ccs_config_cesm1.0.87`): `config_inputdata.xml` defines five HTTPS/wget servers plus an SVN server — `https://osdf-data.gdex.ucar.edu/ncar/gdex/d651077/cesmdata/inputdata/`, `https://ftp.cgd.ucar.edu/cesm/inputdata/`, `https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata/`, a THREDDS `fileServer` mirror, and NEON tower data at `https://storage.neonscience.org/neon-ncar/NEON/`. |
| Data Processing and Analysis: Processing | **CUPiD** (CESM Unified Postprocessing and Diagnostics) is pinned as a required tool at `.gitmodules:162-167` (`tools/CUPiD` → `https://github.com/NCAR/CUPiD.git`, `v0.5.1`). Its documented function is timeseries file generation, data standardization, and diagnostics/metrics across all CESM components, runnable from the CESM workflow through CIME. **HEAD-only:** present at the recorded Source Revision but not in `release-cesm2.1.5` — neither that tag's `.gitmodules` nor its `Externals.cfg` references CUPiD. See the version-scope policy above. |
| Data Visualization | Parent for the two subcategories below; supported by CUPiD (as pinned above). |
| Data Visualization: 2D Graphics | CUPiD v0.5.1 generates contour/map diagnostics — e.g. `nblibrary/ice/Hemis_seaice_visual_compare_contour.ipynb`, `nblibrary/glc/Greenland_SMB_visual_compare_obs.ipynb`, `cupid_utils/cupid_utils/ice/plot_diff.py`; its analysis environment (`environments/cupid-analysis.yml`) pins `cartopy=0.25.0`, `matplotlib=3.10.8`, `cmocean=4.0.3`, `geocat-comp`. **HEAD-only:** present at the recorded Source Revision but not in `release-cesm2.1.5` — neither that tag's `.gitmodules` nor its `Externals.cfg` references CUPiD. See the version-scope policy above. |
| Data Visualization: Line Plots | CUPiD's core function includes timeseries generation and diagnostics, and its analysis environment pins `nc-time-axis=1.4.1` — a library whose sole purpose is plotting `cftime` time axes with matplotlib. **HEAD-only:** present at the recorded Source Revision but not in `release-cesm2.1.5` — neither that tag's `.gitmodules` nor its `Externals.cfg` references CUPiD. See the version-scope policy above. |
| Servers and Environments | Parent for HPC below. |
| Servers and Environments: High Performance Computing | CESM is a distributed-memory MPI application designed for supercomputers. `README.rst:65-66` requires "a functioning MPI environment (unless you plan to run on a single core with the CIME mpi-serial library)"; `.gitmodules:143-148` pins `mpi-serial` and `.gitmodules:137-142` pins `ParallelIO` (`pio2_6_8`), the parallel I/O library for Earth system models. `.github/workflows/derecho.yaml:14-15` runs CI on `hpc-runner`, "currently derecho.hpc.ucar.edu"; `.github/workflows/build.yaml:15-20,33` sets `CC: mpicc`, `FC: mpifort`, `CXX: mpicxx` and submits through the `qcmd`/PBS batch system. `cime_config/config_pes.xml` defines processor-element layouts, and `cime_config/testmods_dirs/allactive/DART_BHIST_lowres/README_layout` works through node/PE arithmetic for a 128-PE-per-node machine. |

**Considered and rejected (audit trail)**

- `Coordinate Transforms` (and subcategories) — CESM does extensive *grid* remapping and interpolation
  (SCRIP is separately licensed at `LICENSE.txt:103-107`; ESMF/NUOPC regridding runs through CMEPS).
  This is horizontal grid interpolation between model meshes, **not** transformation between
  coordinate systems or reference frames (GSE/GSM/heliographic/AACGM), which is what the HSSI
  category means. Excluded.
- `Models and Simulations: MHD` — CESM contains no magnetohydrodynamic solver. Excluded.
- `Models and Simulations: Empirical` — CESM is a first-principles/physics-based model, not an
  empirical or climatological-fit model (IRI/MSIS/HWM class). Excluded.
- `Models and Simulations: Theory`, `Forward-Fitting`, `Field-line Tracing`, `Mission-Specific` — no
  evidence. Excluded.
- `Mission-related` (and subcategories) — CESM is not space-mission software and is not part of any
  mission ground system. Excluded.
- `Servers and Environments: Software or Environment Container` — the only container in the
  repository is `docker pull escomp/base` in `doc/README.md`, used to *build the documentation*, not
  to run or distribute the model. Excluded.
- `Servers and Environments: Infrastructure as Code` — CIME/`ccs_config` do declare machines, batch
  systems and compilers in XML, which is IaC-adjacent, but the category conventionally means
  Terraform/Kubernetes/Ansible-style provisioning. Excluded as over-classification; noted for the
  user.
- `Data Processing and Analysis: File Format Conversion`, `Data Reduction`, `Time Series Analysis`,
  `Image Processing`, `ML/AI` — no direct repository evidence at the CESM level. Excluded.
- `Data Visualization: Web-Based` — CUPiD emits a Jupyter Book and its environment pins `bokeh`, but
  there is no evidence CESM or CUPiD serves interactive browser visualizations. Excluded.

---

### 5. Related Region (MANDATORY)

**Values (4):**

- `Earth Atmosphere`
- `Earth Lower and Middle Atmosphere`
- `Earth Thermosphere`
- `Earth Ionosphere`

**Evidence**

- `Earth Atmosphere` — seeded value, retained. `doc/source/introduction.rst:61-62`; CAM is the
  prognostic atmosphere component (`.gitmodules:57-63`).
- `Earth Lower and Middle Atmosphere` — CESM's core domain spans troposphere, stratosphere and
  mesosphere. The atmosphere component exposes explicit model-top configurations:
  `cime_config/config_compsets.xml` uses `CAM70%LT` (low top, `:86-93`), `CAM70%MT` (middle top,
  `:42-72`) and `CAM70%HT` (high top, `:76-82`). In the current production release the WACCM
  configurations `CAM60%WCCM` (middle atmosphere) and `CAM60%WCTS` (troposphere-stratosphere
  chemistry) appear throughout `git show release-cesm2.1.5:cime_config/config_compsets.xml`
  (compsets `BWma1850`, `BWmaHIST`, `BW1850`, `BWHIST`, `BWSSP*`).
- `Earth Thermosphere` and `Earth Ionosphere` — **WACCM-X is shipped as active, non-commented
  compsets in the exact CAM tags CESM pins, at both HEAD and the production release.** The compset
  physics token is `WXIE` — WACCM-X with **I**onosphere and **E**lectrodynamics — which is
  thermosphere and ionosphere by definition. Verified by fetching each pinned tag directly on
  2026-07-30:

  - **CAM @ `cam6_4_187`** (the tag pinned at CESM HEAD `926b940`, `.gitmodules:57-63`),
    `cime_config/config_compsets.xml` — 8 `WXIE` occurrences, all active:
    `FX2000` → `2000_CAM60%WXIE_CLM50%SP_CICE%PRES_DOCN%DOM_MOSART_SGLC_SWAV` (`:672-673`);
    `FXHIST` → `HIST_CAM60%WXIE_...` (`:677-678`);
    `FXmadHIST` → `HIST_CAM60%WXIED_...` (`:682-683`);
    `FXSD` → `HIST_CAM60%WXIE%SDYN_...` (`:687-688`);
    `FXmadSD` → `HIST_CAM60%WXIED%SDYN_...` (`:692-693`);
    `QPX2000` → `2000_CAM40%WXIE_SLND_SICE_DOCN%AQP3_SROF_SGLC_SWAV` (`:211-212`).
    The same file conditions `USE_ESMF_LIB` on `compset="_CAM\d0%WXIE"` (`:801`).
  - **CAM @ `cam_cesm2_1_rel_60`** — the tag pinned by the production release recorded in Field 12
    (`git show release-cesm2.1.5:Externals.cfg` → `[cam] tag = cam_cesm2_1_rel_60`), same file, 6
    `WXIE` occurrences, all active: `FX2000` → `2000_CAM40%WXIE_CLM40%SP_CICE%PRES_DOCN%DOM_RTM_SGLC_SWAV`
    (`:366-367`); `FXHIST` (`:371-372`); `FXmadHIST` → `CAM40%WXIED` (`:376-377`);
    `FXSD` → `CAM40%WXIE%SDYN` (`:381-382`); `FXmadSD` → `CAM40%WXIED%SDYN` (`:386-387`); plus
    `<value compset="_CAM40%WXIE">TRUE</value>` (`:434`).
  - **The top-level repository itself exercises WACCM-X in its own regression testing.** `ChangeLog`
    records the test `ERS_Ld3.f19_f19_mg17.**FXHIST**.derecho_intel.cam-**waccmx_weimer**` at
    `ChangeLog:2444` and four further occurrences (`:3771`, `:4744`, `:5502`, `:5770`) — the FXHIST
    WACCM-X compset run on Derecho with the `waccmx_weimer` testmod, i.e. the Weimer high-latitude
    ionospheric electric-potential model. `ChangeLog` carries 117 WACCM-X mentions and 337 WACCM
    mentions overall, including "Answer changing for ne16 and WACCM-X configurations" (`:1541`),
    "High-resolution (ne120) WACCM-X" (`:3010`) and "Clean up WACCMX use of ESMF gridded component"
    (`:6580`).

  Corroborating (but no longer load-bearing): `https://www.cesm.ucar.edu/models/waccm-x` (retrieved
  2026-07-30) describes WACCM-X as "a comprehensive numerical model, spanning the range of altitude
  from the Earth's surface to the upper thermosphere", developed "within the CESM framework". This
  capability is the specific reason CESM is in scope for a heliophysics software index.

**Counter-evidence, disclosed.** Two facts cut against a naive reading of the above, and are recorded
so the assessment is honest rather than one-sided:

1. **The literal string "WACCM" does not appear in the HEAD working tree** outside `ChangeLog` —
   `grep -ril waccm --exclude-dir=.git --exclude=ChangeLog` returns nothing. The capability lives in
   the **pinned CAM component**, not in top-level source files. It is nonetheless *in* the top-level
   repository via `ChangeLog` (337 mentions, above) and via the top-level compsets at the production
   tag, where `git show release-cesm2.1.5:cime_config/config_compsets.xml` contains 20 literal
   "WACCM" occurrences and 72 `%WC` (WACCM physics) tokens across the `BW*` coupled compsets.
2. **`cime_config/config_compsets.xml:74-84` at HEAD is an XML comment** reading `Not yet available in
   cam component`, which disables the coupled high-top compsets `B1850C_WAt4ma` and `BHISTC_WAt4ma`
   (`CAM70%HT%CT4MA`). This does **not** bear on the WACCM-X evidence above: those are a *different,
   CESM3-era coupled* configuration (CAM7 high-top with CT4MA chemistry) still under development,
   whereas the `FX*`/`QPX2000` WACCM-X compsets cited above are active and uncommented in both pinned
   CAM tags. The commented block shows one CESM3 coupled configuration is not yet ready; it says
   nothing about WACCM-X availability.

**Considered and rejected.** `Solar Environment` — CESM ingests solar spectral irradiance and
geomagnetic indices as *forcing inputs*; it does not model the Sun. `Earth Magnetosphere` and the
planetary regions — no evidence.

---

### 6. Authors (MANDATORY)

**Author 1**

- **Name:** CESM Team (stored in HSSI as `givenName: "CESM"`, `familyName: "Team"`)
- **Author Identifier:** Not found
- **Affiliation 1:** NSF National Center for Atmospheric Research —
  `https://ror.org/05cvfcr44`
- **Affiliation 2:** University Corporation for Atmospheric Research —
  `https://ror.org/04zhhyn23`

**Evidence**

- Author name and NCAR affiliation are the seeded HSSI values and are corroborated by the Zenodo
  deposit: `creators: [{name: "CESM Team", affiliation: "NCAR"}]`
  (`GET https://zenodo.org/api/records/11229775`, 2026-07-30).
- The NCAR affiliation is "NSF National Center for Atmospheric Research",
  `https://ror.org/05cvfcr44` — confirmed against `https://api.ror.org/v2/organizations/05cvfcr44`
  (`ror_display: "NSF National Center for Atmospheric Research"`, status active). No change needed.
- The second affiliation is supported by `LICENSE.txt:3-4` — "Copyright (c) 2018, University Corporation for
  Atmospheric Research (UCAR) All rights reserved." UCAR is the copyright holder for CESM, and
  `https://ror.org/04zhhyn23` is verified as the active ROR whose display name is exactly "University
  Corporation for Atmospheric Research".

**Author identifier.** "CESM Team" is an organizational-style author, so the field definition would
call for a ROR. A ROR search for "Community Earth System Model"
(`https://api.ror.org/v2/organizations?query=...`) returns no matching organization — CESM is a
project, not a ROR-registered institution. Left empty rather than substituting NCAR's ROR, which
would misidentify the author as the institution.

**No additional authors added.** The repository contains no `CITATION.cff`, `AUTHORS`,
`CONTRIBUTORS`, `codemeta.json` or `.zenodo.json`. SoMEF reported `authors: Jim Edwards
<jedwards@ucar.edu>` at confidence 1, but that is a **false positive** — it is scraped from the
vendored `.lib/git-fleximod/pyproject.toml:5`, which is the git-fleximod tool's authorship, not
CESM's. The ~40 authors of the CESM2 reference paper are paper authors, not declared software
authors; adding them would fabricate authorship. Recorded here so the omission is auditable.

---

### 7. Software Name (MANDATORY)

**Value:** `CESM`

**Evidence.** Repository name `ESCOMP/CESM`; SoMEF `name = "CESM"` at confidence 1. The expanded form
"Community Earth System Model" is the GitHub repository description and appears throughout the
documentation, but Field 7 asks for "the name of the software package as listed on the code
repository", and the seeded short form matches. Editorial intent preserved — the expansion is carried
in the Description instead.

---

### 8. Description (MANDATORY)

**Value:**

> The Community Earth System Model (CESM) is a fully coupled, community-developed global Earth system
> model that provides state-of-the-art computer simulations of Earth's past, present and future
> climate states. CESM simultaneously simulates the atmosphere (CAM), ocean (MOM6, previously POP2),
> land surface (CTSM/CLM), sea ice (CICE), land ice (CISM), river runoff (MOSART, mizuRoute, RTM) and
> ocean waves (WW3), exchanging fluxes through a central coupler/mediator (CMEPS) built on the
> ESMF/NUOPC interfaces. Any component can be replaced by a data or stub version (CDEPS) so that
> individual subsystems can be studied in isolation or driven by observations and reanalyses.
> Experiments are selected as "compsets" that span pre-industrial control, historical, CMIP6 DECK and
> future SSP scenario simulations, as well as initialized seasonal-to-multiyear prediction (SMYLE)
> and large-ensemble configurations. The Whole Atmosphere Community Climate Model (WACCM) and its
> thermosphere/ionosphere extension WACCM-X are CESM atmosphere configurations that raise the model
> top from the troposphere and stratosphere into the mesosphere, thermosphere and ionosphere, making
> CESM applicable to whole-atmosphere and sun-climate research in addition to tropospheric climate.
> This repository is the top-level CESM code base: rather than containing component source directly,
> it pins an exact version of every external component, the CIME case control system and the
> supporting libraries, so that a single checkout plus `./bin/git-fleximod update` reproduces a
> specific CESM tag. CESM is written mostly in Fortran with a Python and Perl scripting layer,
> requires a Fortran 2003 compiler, MPI, NetCDF 4.3 or newer and LAPACK/BLAS, reads and writes
> netCDF, and is designed to run on Unix-like high-performance computing systems.

**Why the replacement.** The stored description is a corrupted, version-pinned Zenodo blurb, not a
description of the software. Zenodo stores
`"<p>The Community Climate Earth System Model<br>release version cesm2.2.0</p>"`; HSSI's copy stripped
the `<br>` without substituting whitespace, producing the run-together "Modelrelease". It also
misnames the software ("Community **Climate** Earth System Model" — CESM is the Community Earth
System Model), pins itself to a version that is neither current nor the current production release,
and conveys nothing about what the software does. Merely re-inserting the missing space would leave
all of those defects in place, so a proper description was written per Field 8's guidance ("what the
software does, why to use it, assumptions it makes").

**Evidence for the replacement text.** `doc/source/introduction.rst:59-64` (coupled model; component
list; past/present/future climate states); `https://www.cesm.ucar.edu/models/cesm2` ("a
fully-coupled, community, global Earth system model that provides state-of-the-art computer
simulations of the Earth's past, present, and future states"); `.gitmodules` (component and library
manifest with pinned `fxtag`s); `README.rst:13-15` ("This repository provides tools for managing the
external components that make up a CESM tag") and `README.rst:96-125` (clone/checkout/fleximod
procedure); `doc/source/introduction.rst:14` ("CESM2 is built on the CIME framework");
`.github/workflows/build.yaml:19` (`CIME_DRIVER: nuopc`); `cime_config/config_compsets.xml:13-22`
(compset grammar and data/stub component options); `git show
release-cesm2.1.5:cime_config/config_compsets.xml` (CMIP6, SSP, SMYLE compsets);
`https://www.cesm.ucar.edu/models/waccm-x` (WACCM-X surface-to-upper-thermosphere coverage);
`README.rst:42-66` and `doc/source/introduction.rst:88-128` (requirements);
`doc/source/introduction.rst:122` ("CESM is written mostly in Fortran").

---

### 9. Concise Description (OPTIONAL)

**Value:**

> A fully coupled, community global Earth system model of the atmosphere, ocean, land, sea ice, land
> ice, rivers and waves, whose WACCM/WACCM-X configurations reach the thermosphere and ionosphere.

(195 characters — within the 200-character limit.)

---

### 10. Publication Date (RECOMMENDED)

**Value:** `2018-06-08`

**Why the replacement.** Field 10 is defined as "Date of first broadcast/publication ... Used for the
initial version of the software" (`resource_submission_form_fields.md:271-273`). `2024-05-21` is
neither first nor initial: it is the Zenodo deposit date of a **mid-line cesm2.2.0 snapshot** archived
in 2024, four generations of release after CESM2 first appeared, and it reflects when someone created
a Zenodo record rather than when the software was published. `2018-06-08` is the publication date of
`release-cesm2.0.0`, the **first release in this repository** — confirmed via `GET
https://api.github.com/repos/ESCOMP/CESM/releases?per_page=100`, where `release-cesm2.0.0` is the
oldest non-prerelease entry (`prerelease: false`, `published_at: 2018-06-08T19:46:31Z`) — consistent
with the repository's own `created_at: 2017-11-15`.

**Caveat recorded.** CESM1 (and CCSM before it) predates this repository entirely, so a stricter
reading of "the initial version of *CESM*" could reach back further than 2018. There is no repository
evidence for such a date, and every other field in this entry — the persistent identifier, the
reference publication, and the version — is CESM2-generation, so 2018-06-08 is the earliest defensible
date consistent with the rest of the record.

---

### 11. Publisher (RECOMMENDED)

- **Organization:** `Zenodo`
- **Publisher Identifier:** `https://zenodo.org`

**Evidence.** The persistent identifier in Field 2 is a Zenodo DOI, which is exactly the case Field 11
names ("For software where a DOI has been obtained through Zenodo ... Zenodo is the correct entry").
Confirmed against `GET https://zenodo.org/api/records/11229775`.

---

### 12. Version (RECOMMENDED)

- **Version Number:** `2.1.5`
- **Version Date:** `2023-12-22`
- **Version Description:** Current CESM production release. Adds support for the NSF NCAR Derecho
  supercomputer; replaces SVN access to component repositories with git sparse checkout
  (manage_externals update); adds the seasonal-to-multiyear prediction compsets `BSMYLE` and
  `BWsc1850smyle`; adds the smoothed biomass-burning historical compset `HISTsmbb`; extends the
  SSP5-8.5 and SSP5-3.4-overshoot scenario compsets to 2300; updates processor-element layouts
  (including default layouts for AWS 1- and 2-degree coupled runs); moves to versioned documentation
  and refreshes the CESM2 copyright notice.
- **Version PID:** Not found

**Version determination — re-checked from scratch on 2026-07-30.** Four independent sources agree
that the current release is **CESM2.1.5**:

1. **The repository's own README, at HEAD.** `README.rst:20-27` has a "Current CESM releases"
   section that states verbatim: `CESM2.1.5` — "Current CESM production release."; `CESM2.2.2` —
   "Current CESM development release."; and warns that "The `CESM2.2.z` release is not a
   scientifically supported version; that is, we do not have any long simulations with this model
   version yet. In most cases, users should continue to use the `CESM2.1.z` series for their science
   and especially for CMIP6-related simulations."
2. **The official CESM website.** `https://www.cesm.ucar.edu/models/cesm2` (retrieved 2026-07-30)
   repeats the same designation: production release CESM 2.1.5, development release CESM 2.2.2, with
   the identical 2.2.z caveat.
3. **GitHub release marking.** `GET https://api.github.com/repos/ESCOMP/CESM/releases?per_page=100`
   returns 16 releases, of which 7 are non-prerelease. `release-cesm2.1.5` is the newest of those
   (`prerelease: false`, `created_at: 2023-12-22T23:39:33Z`, `published_at: 2025-06-25T18:53:24Z`).
   Notably, **none of `release-cesm2.2.0`, `release-cesm2.2.1` or `release-cesm2.2.2` has a GitHub
   Release object at all** — they exist only as git tags. The currently stored `2.2.0` is therefore
   neither the current release nor a GitHub-marked release of any kind.
4. **CESM3 is not released.** The newest tags are prereleases only — `cesm3_0_alpha09g` (2026-07-20)
   and `cesm3_0_beta08` (2026-04-02, `prerelease: true`). The repository default branch is
   `cesm3.0-alphabranch`. No CESM3 alpha or beta may be used for Field 12.

**Why 2.1.5 rather than 2.2.2.** 2.2.2 carries the numerically higher version string and shares the
same tag date, but the project itself designates it a *development* release and explicitly directs
users to the 2.1.z series for science. Field 12 records the version of the software instance a user
would obtain and cite, which is the production release. The higher-numbered `2.2.2` is not selected
because the project designates it a development release.

**Version Date.** `2023-12-22`, from the annotated git tag `release-cesm2.1.5`
(`taggerdate=2023-12-22`, subject "Tagging release-cesm2.1.5 release."; tagged commit
`7a6c5b0d4e045085633dd9553cdd6aa8a8ea728d`, committed 2023-12-22) and corroborated by the GitHub
release object's `created_at: 2023-12-22`. The GitHub `published_at` of 2025-06-25 reflects when the
release page was published on GitHub, ~18 months after the tag, and is not the release date.

**Version Description source.** The GitHub release body for `release-cesm2.1.5` (13 merged PRs) plus
`git show release-cesm2.1.5:ChangeLog` head, whose one-line summary reads "Derecho support and manage
externals update to address git/svn."

**Version PID.** Not found. The only version deposited under the concept DOI is
`10.5281/zenodo.11229776`, which is "CESM-release-cesm2.2.0" — a different version. Recording it here
would mislabel 2.1.5.

---

### 13. Programming Language (RECOMMENDED)

**Values (3):**

- `Fortran 2003`
- `C`
- `Python 3.x`

**Evidence**

- `Fortran 2003` — `README.rst:70-71`: "The Fortran compiler must support Fortran 2003 features";
  `doc/source/introduction.rst:104`: "Fortran compiler with support for Fortran 2003";
  `doc/source/introduction.rst:122`: "CESM is written mostly in Fortran". Component language stats
  confirm the dominance: CTSM 12.3 MB Fortran, tuv-x 4.2 MB Fortran, ParallelIO 387 KB Fortran, CIME
  451 KB Fortran (`GET https://api.github.com/repos/<owner>/<repo>/languages`, 2026-07-30). Fortran
  2003 is the exact standard the project requires, so it is preferred over `Fortran90`/`Fortran 2008`.
- `C` — `README.rst:54`: "Fortran and C compilers"; `doc/source/introduction.rst:106`: "C compiler";
  `.github/workflows/build.yaml:15`: `CC: mpicc`. ParallelIO, pinned at `.gitmodules:137-142`, is
  2.4 MB of C, and `doc/source/introduction.rst:122` notes the Fortran-to-C layer against netCDF.
- `Python 3.x` — `README.rst:48`: "python3 version 3.8 or newer";
  `.github/workflows/fleximod_test.yaml:13` tests `python-version: ["3.7", "3.x"]`. Python is the
  scripting layer for the whole CESM workflow: `bin/git-fleximod`, `describe_version`,
  `tools/statistical_ensemble_test/{ensemble.py,single_run.py}`, `cime_config/SystemTests/funitshare.py`,
  CUPiD, and CIME (2.7 MB Python). GitHub reports Python as this repository's top language
  (125,940 bytes).

**Considered and not selected**

- **Perl 5** — genuinely part of CESM (`README.rst:50` "perl version 5"; CIME contains 878 KB of Perl
  and CTSM 454 KB; `LICENSE.txt:109-112` separately licenses the Perl XML-Lite module used by CESM's
  namelist generation). The vocabulary has no `Perl` row, so it could only be recorded as the
  uninformative `Other`, which is not selected.
- **C++** — present but minor (tuv-x 54 KB); `.github/workflows/build.yaml:17` sets `CXX: mpicxx`.
  Below the "most important languages" bar of Field 13.
- **SoMEF's language output is not usable here.** It returned Python/Shell/Batchfile/Makefile — the
  GitHub statistics for the *top-level manifest repository only*, since all model source lives in
  external submodules. Taken literally it would omit Fortran entirely, which would be wrong for CESM.

---

### 14. Reference Publication (RECOMMENDED)

**Value:** `https://doi.org/10.1029/2019MS001916`

**Evidence.** Danabasoglu, G., Lamarque, J.-F., Bacmeister, J., Bailey, D. A., DuVivier, A. K.,
Edwards, J., Emmons, L. K., Fasullo, J., et al. (2020). "The Community Earth System Model Version 2
(CESM2)." *Journal of Advances in Modeling Earth Systems*. Verified via
`GET https://api.crossref.org/works/10.1029/2019MS001916` (2026-07-30): title, container-title and
publication date (2020-02) all confirm. This is the canonical model-description paper for CESM2 and
the standard citation for the software.

---

### 15. License (RECOMMENDED)

- **License:** `Other`
- **License URI:** `https://www.cesm.ucar.edu/models/cesm2/copyright.html`

**Why the replacement.** CESM is not released under CC-BY-4.0. The repository's actual licence is a
custom instrument:

- `LICENSE.txt:1-4` — "CESM2 Copyright and Terms of Use / Copyright (c) 2018, University Corporation
  for Atmospheric Research (UCAR) All rights reserved." followed by a BSD-style warranty disclaimer
  (`LICENSE.txt:12-22`) with no accompanying grant clause and no SPDX identifier.
- `LICENSE.txt:24-25` — "The following components are copyrighted and may only be used, modified, or
  redistributed under the terms indicated below", followed by a table of twelve separately-licensed
  bundled components with materially different terms: CISM under **GNU LGPL v3**
  (`LICENSE.txt:66-71`), ESMF under the **University of Illinois/NCSA Open Source License**
  (`:48-53`), CIME, FATES, AER RRTMG, MCT, POP2, CICE, SCRIP, ISCCP, XML-Lite, and the Lahey
  `Inf_NaN_Detection` module whose terms are **not** open source (`:73-80`: "Copies of this source
  code, or standalone compiled files derived from this source may not be sold without permission
  from Lahey Computers Systems").
- GitHub's licence detector reports `license: {key: "other", spdx_id: "NOASSERTION"}` for
  ESCOMP/CESM (`GET https://api.github.com/repos/ESCOMP/CESM`, 2026-07-30).
- `https://www.cesm.ucar.edu/models/cesm2/copyright.html` (retrieved 2026-07-30) is the authoritative
  project licence page and carries the same custom terms; `LICENSE.txt:114-115` points to it.

The stored `Creative Commons Attribution 4.0 International` originates solely from the Zenodo
deposit's `license: {id: "cc-by-4.0"}` field — a depositor-side selection for one archived snapshot,
not the terms under which the code is distributed. Asserting CC-BY-4.0 misrepresents CESM in two
ways: it is a content licence rather than a software licence, and it would silently drop the
component-specific LGPL/NCSA/non-redistributable terms the project explicitly attaches.

**Why `Other` and not a specific SPDX row.** The HSSI `License` vocabulary is closed
(`License.objects.filter(name__iexact=...)`, `Unknown license` on no match). Live
HSSI license choices have no entry corresponding to "CESM2 Copyright and Terms of Use". The field
definition's own instruction is that an SPDX title absent from the list must be recorded as `Other`.
`Other` is confirmed present in the live vocabulary.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values (22, lower-case, one per entry):**

`climate`, `climate model`, `earth system model`, `coupled model`, `general circulation model`,
`atmosphere`, `ocean`, `sea ice`, `land ice`, `land surface`, `whole atmosphere`, `stratosphere`,
`mesosphere`, `thermosphere`, `ionosphere`, `upper atmosphere`, `waccm`, `cmip6`,
`data assimilation`, `high performance computing`, `fortran`, `ncar`

**Evidence.** The keywords were checked for exact and near-duplicate matches in the live HSSI
vocabulary and normalized to the stored lower-case form.

Sources: GitHub repository topics `climate`, `climate-model`, `ncar` (`GET
https://api.github.com/repos/ESCOMP/CESM`; SoMEF also returns `keywords: "climate, climate-model,
ncar"` at confidence 1 — `climate-model` normalized to the spaced form `climate model` to match HSSI
keyword conventions); component domains from `.gitmodules` and
`doc/source/introduction.rst:61-63` (atmosphere, ocean, land surface, sea ice, land ice, river runoff,
waves); WACCM/whole-atmosphere and the upper-atmosphere terms from the WACCM compsets in
`git show release-cesm2.1.5:cime_config/config_compsets.xml` and
`https://www.cesm.ucar.edu/models/waccm-x`; `cmip6` from the pervasive `*cmip6` compsets and
`README.rst:27` ("especially for CMIP6-related simulations"); `data assimilation` from the
`BHISTC_LT_DART` compset (`cime_config/config_compsets.xml:98`); `high performance computing` from
`.github/workflows/derecho.yaml:14-15`; `fortran` from `doc/source/introduction.rst:122`.

---

### 17. Data Sources (OPTIONAL)

**Values (2):** `HTTP/HTTPS Directories`, `FTP/FTPS Directories`

Both protocols are genuinely used across CESM's lineage, and which one dominates depends on the
version: **FTP/gftp** at the CIME tag pinned by the production release recorded in Field 12, and
**HTTPS** at the `ccs_config` tag pinned at HEAD. Both values are therefore recorded and were
confirmed in the live HSSI `DataInput` vocabulary.

**Evidence — `HTTP/HTTPS Directories` (HEAD).** CESM's input-data acquisition configuration ships in
the `ccs_config` submodule that CESM pins as required (`.gitmodules:29-34`,
`fxtag = ccs_config_cesm1.0.87`). Its `config_inputdata.xml` (fetched at that exact pinned tag from
`https://raw.githubusercontent.com/ESMCI/ccs_config_cesm/ccs_config_cesm1.0.87/config_inputdata.xml`,
2026-07-30) lists, in precedence order, five `wget` servers and one `svn` server — all HTTPS
directory trees:

- `https://osdf-data.gdex.ucar.edu/ncar/gdex/d651077/cesmdata/inputdata/`
- `https://ftp.cgd.ucar.edu/cesm/inputdata/` (with `inputdata_checksum.dat`)
- `https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata/` (wget) and the same address via `svn`
- a THREDDS `fileServer` mirror at `https://redoak.cs.toronto.edu/.../CESM/inputdata/`
- NEON tower forcing at `https://storage.neonscience.org/neon-ncar/NEON/`

**Evidence — `FTP/FTPS Directories` (the version recorded in Field 12).** At `release-cesm2.1.5` the
input-data server list lived in CIME rather than `ccs_config`. `git show
release-cesm2.1.5:Externals.cfg` pins `[cime] tag = cime5.6.49`; that tag's
`config/cesm/config_inputdata.xml` (fetched from
`https://raw.githubusercontent.com/ESMCI/cime/cime5.6.49/config/cesm/config_inputdata.xml`,
2026-07-30) defines four **active, non-comment** `<server>` entries and **zero HTTPS `wget`**
servers:

- `<protocol>gftp</protocol>` → `ftp://gridanon.cgd.ucar.edu:2811/cesm/inputdata/` ("grid ftp requires
  the globus-url-copy tool on the client side")
- `<protocol>wget</protocol>` → `ftp://ftp.cgd.ucar.edu/cesm/inputdata/` (anonymous FTP)
- `<protocol>ftp</protocol>` → `ftp.cgd.ucar.edu/cesm/inputdata` ("ftp requires the python package
  ftplib")
- `<protocol>svn</protocol>` → `https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata`

**Correction of a prior claim.** An earlier draft of this file asserted that the `ftp://` address
"appears only in an XML comment ... no active server uses FTP". That is **false for the version
recorded in Field 12**: three of the four servers at `cime5.6.49` are FTP-family and are active
`<server>` elements, not comments. The claim has been removed and replaced with the version split
above.

**Considered and rejected.** `S3/Cloud-aware` — the OSDF/GDEX endpoint is fetched over plain HTTPS by
`wget`, not through an S3 or object-store API. `Observatory/Mission-specific` — CESM's inputs are
gridded geophysical forcing datasets, not a specific observatory's data products (consistent with
Fields 31/32 being empty).

---

### 18. Input File Formats (RECOMMENDED)

**Values (3):** `netCDF3/4`, `ascii`, `Other`

**Evidence**

- `netCDF3/4` — the primary science-data format for all initial, boundary and forcing datasets.
  `README.rst:60-63`: "a NetCDF library version 4.3 or newer built with the same compiler ... a
  PnetCDF library is optional, but recommended"; `doc/source/introduction.rst:110,114,124-128`
  (PnetCDF is "file-format compatible with netCDF"). Parallel netCDF I/O is provided by ParallelIO,
  pinned at `.gitmodules:137-142` (`pio2_6_8`). `tools/statistical_ensemble_test/README:32-33,100`
  confirms the ensemble summary and history files are netCDF.
- `ascii` — Fortran namelist input is the standard user-facing configuration channel: the `user_nl_*`
  files throughout `cime_config/testmods_dirs/` (`user_nl_cam`, `user_nl_clm`, `user_nl_cice`,
  `user_nl_cpl`, `user_nl_pop`, `user_nl_rtm`, `user_nl_mosart`, `user_nl_cism`) are plain text read
  by the model at run time, as are `rpointer` restart-pointer files and CDEPS stream text files.
- `Other` — XML. CESM's entire case configuration is XML that the model workflow reads and writes
  (`cime_config/config_compsets.xml`, `config_pes.xml`, `config_tests.xml`,
  `testlist_allactive.xml`, `testfiles/ExpectedTestFails.xml`, and the generated `env_*.xml`
  manipulated by `./xmlquery` / `./xmlchange`, per `doc/source/quickstart.rst:31-34`). XML has no row
  in the 11-value `FileFormat` vocabulary, so `Other` is the correct mapping.

**Considered and rejected.** `HDF5` — netCDF-4 is HDF5-based and reachable through PIO's
`NETCDF4C`/`NETCDF4P` types, but CESM does not read native HDF5; `netCDF3/4` already covers it and
listing HDF5 would overstate support. `csv` — the only CSV in the stack is the optional inventory
listing (`<inventory>../listing.csv</inventory>`) used by the NEON input-data servers; too narrow to
represent CESM as a CSV-consuming tool.

---

### 19. Output File Formats (RECOMMENDED)

**Values (3):** `netCDF3/4`, `ascii`, `Other`

**Evidence**

- `netCDF3/4` — all CESM history and restart output is netCDF, written in parallel through
  ParallelIO (`.gitmodules:137-142`). `tools/statistical_ensemble_test/README:95-105` names the
  history files CESM produces (`*.cam.h0.*`, `*.pop.h.*`) and states that the ensemble summary
  written from them is NetCDF; `tools/statistical_ensemble_test/addmetadata.sh:3` — "Adds metadata to
  netcdf statistical ensemble test files."
- `ascii` — CESM writes plain-text component log files, timing/performance summaries, `rpointer`
  restart-pointer files, and the resolved namelists produced by `preview_namelists` (see
  `.github/workflows/preview_namelist.yaml`).
- `Other` — XML. The case-configuration XML files are written as well as read (`./xmlchange`,
  `create_newcase`, `create_test`), and CUPiD emits a Jupyter Book HTML diagnostics site. Neither XML
  nor HTML has a `FileFormat` row.

---

### 20. Operating System (RECOMMENDED)

**Values (3):** `Linux`, `Mac`, `Other`

**Evidence.** `README.rst:44` — "a Unix-like operating system (Linux, AIX, OS X, etc.)";
`doc/source/introduction.rst:94` — "UNIX style operating system such as CNL, AIX or Linux".

- `Linux` — named explicitly in both sources; `.github/workflows/fleximod_test.yaml:8` runs
  `ubuntu-latest`; the CI target machine Derecho runs a Linux distribution.
- `Mac` — "OS X" in `README.rst:44`.
- `Other` — AIX and Cray CNL are named as supported and have no row in the 7-value vocabulary.

**Considered and rejected.** `Windows` — excluded; the requirement is explicitly a Unix-like OS.
`Operating System Independent` — excluded; CESM requires a Unix-like environment with MPI and a
Fortran 2003 toolchain, so it is not OS-independent. (`OS Independent` is not a value at all.)

---

### 21. CPU Architecture (RECOMMENDED)

**Values (2):** `x86-64`, `HPC or HEC`

**Evidence**

- `HPC or HEC` — `.github/workflows/derecho.yaml:14-15`: CI runs on `hpc-runner`, "currently
  derecho.hpc.ucar.edu", NSF NCAR's supercomputer; `.github/workflows/build.yaml:33` submits through
  `qcmd -q main` (PBS) with an allocation project code; `cime_config/config_pes.xml` defines
  processor-element layouts; `README.rst:65-66` requires MPI.
- `x86-64` — the machines CESM is tested on are x86-64: `cime_config/testlist_allactive.xml`
  exercises `derecho` with the `gnu` and `intel` compilers (Derecho's CPU nodes are AMD EPYC
  x86-64); the 2.1.x test lists target `cheyenne` with `intel` (Intel Xeon x86-64);
  `.github/workflows/fleximod_test.yaml:8` runs `ubuntu-latest` (x86-64).

**Considered and rejected.** `GPU` — `.github/workflows/derecho.yaml:31` includes `nvhpc` in the
compiler matrix, but that only shows the NVIDIA HPC SDK is exercised as a *compiler*; there is no
repository evidence of GPU-offloaded CESM execution. Excluded to avoid overstating support; noted for
the user. `ppc64le` — no evidence at HEAD. `Apple Silicon arm64` / `Linux aarch64 or arm64` — `Mac`
support is stated at the OS level (`README.rst:44`) but no architecture-specific evidence exists.

---

### 22. Related Phenomena (OPTIONAL)

**Value:** Not found — deliberately left empty.

**Rationale.** The live `Phenomena` vocabulary has exactly 7 closed values — `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`,
`X-ray emission` — all solar or magnetospheric. CESM is a coupled Earth-system/climate model; none of
these is a phenomenon it is built to study. The vocabulary is closed (`_get_graph_list_item` raises
`Unknown value`), so a phenomenon such as "climate variability" or "ENSO" cannot be added here; those
belong in Keywords, where the whole-atmosphere terms have been recorded.

**Candidate considered and not selected.** `Geomagnetic Storms` is arguable *via WACCM-X*, which
simulates the thermosphere/ionosphere response to geomagnetic forcing. It is not applied because the
top-level CESM repository contains no geomagnetic-forcing evidence whatever, and asserting it would
push past the evidence threshold used for this record.

---

### 23. Development Status (RECOMMENDED)

**Value:** `Active`

**Evidence.** CESM has reached a stable, usable state and is under vigorous ongoing development.
`git log --since=2025-07-30 --oneline | wc -l` → 159 commits in the last twelve months; latest commit
`926b940` dated 2026-07-17 ("Update for cesm3_0_alpha09g testing."). `GET
https://api.github.com/repos/ESCOMP/CESM` reports `pushed_at: 2026-07-20`, `archived: false`,
`fork: false`. (Issue, star and fork counts are deliberately not recorded here either — same
volatile-metric rationale as Field 3.) The `ChangeLog` records 454 tags, with `cesm3_0_alpha09g`
dated 17 July 2026 at its head. CESM3 development is in active alpha (`cesm3_0_alpha09a`…`09g` all
tagged in 2026) on the default branch `cesm3.0-alphabranch`, while CESM2.1.5 remains the supported
production release. This matches repostatus.org "Active" exactly.

---

### 24. Documentation (RECOMMENDED)

**Value:** `https://escomp.github.io/CESM/`

**Evidence.** `README.rst:9-11` — "The CESM Quickstart Guide is available at:
http://escomp.github.io/cesm". `doc/README.md` confirms this site is built from this repository's
`doc/` directory and published to the orphan `gh-pages` branch. The guide contains exactly what
Field 24 asks for — installation and download instructions plus a quick start:
`doc/source/downloading_cesm.rst`, `doc/source/quickstart.rst`, `doc/source/introduction.rst`
(software prerequisites at `:88-128`), `doc/source/cesm_configurations.rst`. The landing page and
the versioned build for the production release at
`https://escomp.github.io/CESM/versions/cesm2.1/html/index.html` both resolve successfully.

**Related, not selected.** `https://www.cesm.ucar.edu` (`README.rst:5-7`) is the project website, and
the CIME Case Control System documentation at `http://esmci.github.io/cime`
(`doc/source/introduction.rst:14-22,130`) carries the bulk of the CESM2 User's Guide. The GitHub wiki
that SoMEF returned (`https://github.com/ESCOMP/CESM/wiki`) is not the project's documentation.

---

### 25. Funder (OPTIONAL)

| Organization | Funder Identifier |
|---|---|
| U.S. National Science Foundation | `https://ror.org/021nxhr62` |
| United States Department of Energy | `https://ror.org/01bj3aw27` |
| National Aeronautics and Space Administration | `https://ror.org/027ka1x80` |
| University Corporation for Atmospheric Research | `https://ror.org/04zhhyn23` |

**Evidence.** `LICENSE.txt:6-10` — "The Community Earth System Model (CESM) was developed primarily in
cooperation with the National Science Foundation, the Department of Energy, the National Aeronautics
and Space Administration, and the University Corporation for Atmospheric Research National Center for
Atmospheric Research." Corroborated by `doc/source/introduction.rst:72-79` — "Primarily supported by
the National Science Foundation (NSF) and centered at the National Center for Atmospheric Research
(NCAR) in Boulder, Colorado, the CESM project enjoys close collaborations with the U.S. Department of
Energy (DOE) and the National Aeronautics and Space Administration (NASA)" — and by
`https://www.cesm.ucar.edu/models/cesm2/copyright.html` (2026-07-30): "The Community Earth System
Model (CESM) was developed with support primarily from the National Science Foundation."

All four names are written in full per the field definition (no acronyms), and every ROR was verified
against `https://api.ror.org/v2/organizations/<id>` on 2026-07-30 — each is `status: active` and each
`ror_display` name matches the string above **exactly**. All four also already exist as HSSI
organization rows with these exact names and identifiers, so no new rows are minted.

**Not listed.** NSF National Center for Atmospheric Research (`https://ror.org/05cvfcr44`) — named in
the same `LICENSE.txt` phrase, but as CESM's *host institution* rather than a funder; it is already
recorded as the author affiliation in Field 6.

---

### 26. Award Title (OPTIONAL)

**Value:** Not found

**Rationale.** No grant or award title or number appears anywhere in the repository, the Zenodo
deposit (`fundingReferences` absent), or the CESM licence/copyright pages.

**Documented non-award.** `.github/workflows/build.yaml:33` contains `PROJECT=P93300606 -A P93300606`
and `tools/statistical_ensemble_test/README` uses `--project P99999999`. These are NSF NCAR/CISL
**supercomputing allocation codes** passed to the PBS scheduler (the second is a placeholder), not
funding awards, and are deliberately not recorded as award numbers.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

| DOI | Publication |
|---|---|
| `https://doi.org/10.1002/2017MS001232` | Liu et al. (2018), "Development and Validation of the Whole Atmosphere Community Climate Model With Thermosphere and Ionosphere Extension (WACCM-X 2.0)", *JAMES* |
| `https://doi.org/10.1029/2019JD030943` | Gettelman et al. (2019), "The Whole Atmosphere Community Climate Model Version 6 (WACCM6)", *JGR: Atmospheres* |
| `https://doi.org/10.1175/BAMS-D-12-00121.1` | Hurrell et al. (2013), "The Community Earth System Model: A Framework for Collaborative Research", *BAMS* |
| `https://doi.org/10.5194/esd-12-1393-2021` | Rodgers et al. (2021), "Ubiquity of human-induced changes in climate variability" (CESM2 Large Ensemble), *Earth System Dynamics* |

**Evidence.** All four DOIs were resolved and their titles, containers and publication dates verified
against `https://api.crossref.org/works/<doi>` on 2026-07-30. Selection rationale: the two WACCM
papers document the whole-atmosphere and thermosphere/ionosphere configurations that make CESM
relevant to heliophysics and that justify Field 5's thermosphere/ionosphere regions; the BAMS paper
is the CESM framework paper describing the predecessor generation of the model; the Rodgers paper is
the reference publication for the CESM2 Large Ensemble recorded in Field 28. All are distinct from
the Field 14 reference publication.

---

### 28. Related Datasets (OPTIONAL)

**Value:** `https://doi.org/10.26024/kgmp-c556` — CESM2 Large Ensemble Community Project (LENS2),
NSF NCAR Geoscience Data Exchange dataset `d651056`

**Evidence.** `https://gdex.ucar.edu/datasets/d651056/` (retrieved 2026-07-30) publishes
`DOI: 10.26024/KGMP-C556` for the dataset and directs users to cite Rodgers et al. 2021
(`https://doi.org/10.5194/esd-12-1393-2021`, recorded in Field 27). The dataset is 100 CESM2 ensemble
members at 1-degree resolution spanning 1850-2100 under CMIP6 historical and SSP370 forcing.

**Selection rationale.** Field 28 asks for "datasets the software supports functionality for (e.g.,
analysis)". LENS2 is CESM2 *output* rather than CESM *input*; it is included because CESM is the
software that produces, extends and is used to interpret it, and because the CESM release lineage
directly supports reproducing it (`git show release-cesm2.1.5:cime_config/config_compsets.xml`
defines the `BHISTsmbb` / `BSSP370smbb` large-ensemble compsets and sets LENS2 members such as
`b.e21.BSSP370smbb.f09_g17.LE2-1171.009` as `REFCASE` values). The CESM input-data collections that
the model actually reads have no DOI.

---

### 29. Related Software (OPTIONAL)

**Prognostic components and core infrastructure** (CESM's domain-specific pinned dependencies, all
from `.gitmodules` at revision `926b940`, with the exact `fxtag` CESM pins):

| Software | URL | Pinned tag | Role |
|---|---|---|---|
| CIME | `https://github.com/ESMCI/cime` | `cime6.4.1` | Case control system CESM is built on (`doc/source/introduction.rst:14`) |
| CAM | `https://github.com/ESCOMP/CAM` | `cam6_4_187` | Atmosphere component (host of WACCM/WACCM-X) |
| CTSM | `https://github.com/ESCOMP/CTSM` | `ctsm5.4.042` | Land surface component (CLM) |
| CESM_CICE | `https://github.com/ESCOMP/CESM_CICE` | `cesm3_cice6_6_3_16` | Sea ice component |
| MOM_interface | `https://github.com/ESCOMP/MOM_interface` | `mi_260715` | Ocean component (MOM6) |
| cism-wrapper | `https://github.com/ESCOMP/cism-wrapper` | `cismwrap_2_2_015` | Land ice component (CISM) |
| CMEPS | `https://github.com/ESCOMP/CMEPS` | `cmeps1.1.54` | Coupler/mediator (NUOPC) |
| CDEPS | `https://github.com/ESCOMP/CDEPS` | `cdeps1.0.101` | Data component models |
| MOSART | `https://github.com/ESCOMP/MOSART` | `mosart1.1.13` | River transport model |
| mizuRoute | `https://github.com/ESCOMP/mizuRoute` | `v3.1.1` | River routing |
| RTM | `https://github.com/ESCOMP/RTM` | `rtm1_0_89` | River transport model (legacy) |
| WW3_interface | `https://github.com/ESCOMP/WW3_interface` | `main_0.1.0` | Ocean wave component (WaveWatch III) |
| ParallelIO | `https://github.com/NCAR/ParallelIO` | `pio2_6_8` | Parallel I/O library for Earth system models |

**Predecessor and peer model**

| Software | URL | Relationship |
|---|---|---|
| CCSM (Community Climate System Model) | `https://www.cesm.ucar.edu/models/ccsm` | Predecessor model that CESM superseded. This is exactly the value previously mis-filed in Field 3; it is preserved here, where a predecessor belongs. |
| E3SM | `https://github.com/E3SM-Project/E3SM` | Peer coupled Earth system model performing the same task; shares the CIME case control system with CESM and shares CIME's copyright (`LICENSE.txt:36-46` — "Common Infrastructure for Modeling the Earth (CIME) ... UCAR and DOE BER E3SM project team members, including those at SNL and ANL"). |

**Considered and rejected (audit trail).** `git-fleximod`
(`https://github.com/jedwards4b/git-fleximod`, vendored at `.lib/git-fleximod`) — an important
dependency in the mechanical sense, but a **generic** git submodule/sparse-checkout manager that
would be equally at home in a web app or a finance model. Generic infrastructure is excluded from
Field 29 as well as Field 30. Likewise `mpi-serial`, `FMS_interface`, `CESM_share`,
`ccs_config_cesm`, `tuv-x` and `COSPv2.0` are pinned build/infrastructure or intra-component pieces
that carry no distinguishing information about CESM at this level; recorded here rather than listed.
Component-level dependencies of components (POP2, MARBL, FATES, CLUBB, PUMAS, CARMA) are out of scope
per the scope-discipline rule.

---

### 30. Interoperable Software (OPTIONAL)

| Software | URL | Demonstrated exchange (specific evidence) |
|---|---|---|
| ESMF | `https://github.com/esmf-org/esmf` | CESM's coupling is built on the ESMF/NUOPC interfaces. `.github/workflows/build.yaml:19` sets `CIME_DRIVER: nuopc` as the CI driver; CMEPS (`.gitmodules:99-105`) is the NUOPC mediator, and its ChangeLog path is `src/drivers/nuopc/`. `doc/source/introduction.rst:112` lists "ESMF 5.2.0 or newer" among CESM's external requirements. Each component supplies a NUOPC cap through which state is exchanged. |
| DART | `https://github.com/NCAR/DART` | Purpose-built data-assimilation coupling. `cime_config/config_compsets.xml:23` reserves the `ESP` (External System Processing) component slot DART occupies; `:95-101` defines the dedicated compset `BHISTC_LT_DART`; `cime_config/testmods_dirs/allactive/DART_BHIST_lowres/` supplies the multi-instance ensemble configuration (`README_layout`, `shell_commands`, and `user_nl_cam`/`user_nl_clm`/`user_nl_mosart` overrides) that DART assimilation requires. |
| CUPiD | `https://github.com/NCAR/CUPiD` | Companion post-processing/diagnostics package that consumes CESM output and can be driven from the CESM workflow through CIME. Pinned as a required tool at `.gitmodules:162-167` (`tools/CUPiD`, `v0.5.1`). |
| PyCECT | `https://github.com/NCAR/PyCECT` | Companion package that reads CESM netCDF history files to run the CESM Ensemble Consistency Test. `tools/statistical_ensemble_test/README:95-113` documents the exchange concretely: copy every `*.cam.h0.*` (CAM-ECT/UF-CAM-ECT) or `*.pop.h.*` (POP-ECT) history file into a directory, then run `pyEnsSum.py`/`pyEnsSumPop.py` and `pyCECT.py`. Pinned at `.gitmodules:155-160` (`3.3.1`). |
| FTorch | `https://github.com/Cambridge-ICCS/FTorch` (CESM interface: `https://github.com/ESCOMP/FTorch_interface`) | Cross-language bridge letting CESM's Fortran components call PyTorch models. Pinned at `.gitmodules:169-175` (`v0.0.5`, `fxrequired = ToplevelOptional`). *Scope caveat:* CESM3 development line only — not present in `release-cesm2.1.5`. |

**Relevance gate applied.** Every entry above names a specific artifact demonstrating exchange (a
compset, a testmods directory, a documented file-handoff procedure, a pinned interface library, a CI
driver setting) rather than mere co-presence. No entry rests on "part of the ecosystem" reasoning.

**Considered and rejected.** netCDF, PnetCDF, HDF5, LAPACK/BLAS, CMake, MPI — foundational
infrastructure required to build and run CESM, but "requires netCDF" is true of essentially every
Earth-system model and conveys nothing distinguishing; the netCDF interchange capability is recorded
in Fields 18/19 where it belongs. `git-fleximod` — generic tooling (see Field 29). `COSPv2.0` — a
sub-component embedded inside CAM rather than a peer tool CESM exchanges data with; recorded as
Field 4 evidence instead.

---

### 31. Related Instruments (OPTIONAL)

**Value:** None — deliberately empty.

**Rationale.** CESM is an instrument-agnostic numerical model. It does not read, parse, calibrate or
process any specific instrument's data, and implements no instrument-specific format. Applying the
Field 31 sanity check: a user searching HSSI for `instrument:"X"` would not expect a coupled climate
model back, and someone working with instrument X's data would not reach for CESM. This is exactly
the case the field definition describes as "instrument-agnostic tools (general models/utilities/
frameworks) support none specifically". An empty Field 31 is the correct outcome here, not a gap.

**Considered and rejected (audit trail).** The **COSP** satellite simulators bundled with CAM
(`doc/source/downloading_cesm.rst:91,100`; ISCCP separately licensed at `LICENSE.txt:82-87`) emulate
ISCCP, MISR, MODIS, CloudSat and CALIPSO observables. They were evaluated and rejected: COSP produces
*synthetic* observables so model output can be compared with satellite retrievals; CESM neither reads
nor processes those instruments' actual data. The instruments are also Earth-observing cloud/aerosol
sensors outside heliophysics scope, and this synthetic-observation capability is already correctly
captured as `Models and Simulations: Observatory/Instrument Models` in Field 4.

No instrument entry is recorded because none is relevant to CESM's role as a general coupled model.

---

### 32. Related Observatories (OPTIONAL)

**Value:** None — deliberately empty.

**Rationale.** CESM is not designed to support any specific mission or observatory. It works with
gridded geophysical forcing and boundary datasets (emissions, sea-surface temperatures, solar
spectral irradiance, land-use change), not with a named mission's data products, and it implements no
mission data conventions. Consistent with Field 17, where `Observatory/Mission-specific` was likewise
rejected. An empty Field 32 is the correct outcome.

**Considered and omitted (audit trail).** HEAD's `ccs_config` `config_inputdata.xml`
(`ccs_config_cesm1.0.87`) defines a `<server CLM_USRDAT_NAME="NEON">` entry supplying NEON tower
forcing data from `https://storage.neonscience.org/neon-ncar/NEON/` — a specific *named network*
rather than a generic archive, so it was evaluated rather than waved past. It is correctly omitted:
no NEON row exists in the live `InstrumentObservatory` vocabulary (7,648 rows, checked 2026-07-30),
and NEON is the National Ecological Observatory Network, a terrestrial ecological observing network
outside heliophysics scope. Per the resolution ladder this is rule 5 — nothing defensible resolves,
so the entry is omitted and documented rather than invented.

---

### 33. Logo (OPTIONAL)

**Value:** Not found

**Rationale.** No CESM logo exists at a permanent, publicly accessible URL. Checked on 2026-07-30:
the repository contains no logo asset (`doc/source/_static/` holds only `pop_ver.js`); the CESM
website `https://www.cesm.ucar.edu/` and `https://www.cesm.ucar.edu/models/cesm2` serve only the
generic NSF and NCAR institutional marks
(`/profiles/composer/unity-profile/themes/unity/img/NSF_Official_logo.png` and `logo-ncar.png`) with
no CESM-specific image; the published documentation on the `gh-pages` branch uses the stock Sphinx
Read-the-Docs theme with no project logo; and SoMEF returned no `logo` field. Recording the ESCOMP
GitHub organization avatar would misidentify the org's mark as the software's logo. Correctly left
empty rather than fabricated.
