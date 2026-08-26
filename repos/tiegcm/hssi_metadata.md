# HSSI Metadata Extraction Results

**HSSI Software ID:** 52d61c70-77fd-4c4a-aae8-f4e24dde6de8
**Repository:** https://github.com/NCAR/tiegcm
**Source Revision:** cedd16dfe6bdb745cb6a0f6163e7831bf84db95b (tag `TIEGCM-3.0.1`, branch `master`, 2026-05-07)
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Not part of the stored record; placeholder retained.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.15214470

*Source: DataCite and Zenodo confirm this as the Zenodo **concept** DOI (`HasVersion` -> `10.5281/zenodo.15214471`).*

*Provenance caveat (durable, worth recording): this DOI is a **third-party reproducibility deposit**, not an NCAR-minted DOI. DataCite `relatedIdentifiers` gives `IsSupplementTo -> https://github.com/j0a8c2k1/tiegcm/tree/v1.0.0`, i.e. the deposit was made from a personal fork, and it was created to support Wang et al. (2025) (Field 27). The repository itself contains no DOI badge and no DOI in `CITATION.cff`; SoMEF found no identifier in the repo. NCAR has not published its own software DOI for TIEGCM. This is the correct value to keep -- it is the only persistent identifier that exists for this software -- but it explains why the deposit's own version label (`v1.0.0`) leaked into Field 12.*

### 3. Code Repository (MANDATORY)
https://github.com/NCAR/tiegcm

*Source: git remote, `CITATION.cff` line 7 (`https://github.com/NCAR/TIEGCM`, same repository with different capitalization), and the GitHub repository metadata. This correctly points at the official NCAR repository rather than the fork used for the Zenodo deposit.*

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Assimilation
- Data Processing and Analysis:Processing
- Models and Simulations
- Models and Simulations:Data Guided
- Models and Simulations:Empirical
- Models and Simulations:First Principles
- Models and Simulations:Physics-Based
- Servers and Environments
- Servers and Environments:High Performance Computing

*Every subcategory below is paired with its parent category. Evidence, per value:*

- **Models and Simulations:First Principles / :Physics-Based** -- the current documentation describes TIE-GCM as "a comprehensive, first-principles, three-dimensional, non-linear representation of the coupled thermosphere and ionosphere system that includes a self-consistent solution of the middle and low-latitude dynamo field" (https://tiegcm-docs.readthedocs.io/en/latest/tiegcm/intro.html). Prognostic solvers for the coupled momentum, energy and continuity equations are in `src/dt.F`, `src/duv.F`, `src/dynamics.F`, `src/comp*.F`, `src/minor.F`, `src/oplus.F`, `src/elden.F`, `src/settei.F`, with the electrodynamo PDE solved by multigrid in `src/pdynamo.F` + `src/mud*.F`.
- **Models and Simulations:Empirical** -- embedded empirical sub-models: Heelis high-latitude convection (`src/heelis.F`), Weimer 2001/2005 convection (`src/wei05sc.F`, namelist `POTENTIAL_MODEL`), Roble & Ridley auroral parameterization (`src/aurora.F`, namelist `AURORA`), GSWM and CTMT tidal climatologies (`src/gswm.F`, `src/ctmt.F`), empirical SAPS drift (`src/subaur.F90`, namelist `SAPS`), IGRF geomagnetic field (`src/apex.F90`, `src/magfield.F`), and index-derived hemispheric power / cross-cap potential (`src/gpi.F`).
- **Models and Simulations:Data Guided** -- the documentation's own "Strengths" list: "Solar forcing can be specified by proxy models or measurements" and "Auroral forcing can be specified by empirical relationships, by output from the AMIE procedure, or by a magnetosphere model such as the GAMERA." Implemented by `src/gpi.F` (NGDC Kp/F10.7), `src/imf.F` (IMF/solar-wind driver file), `src/soldata.F` (measured solar EUV spectral flux, namelist `SEE_NCFILE`), `src/amie.F` (AMIE potential/energy-flux output), `src/saber_tidi.F` and `src/bgrd_data.F` (observation-based lower boundary), `src/nudge.F90` (relaxation toward external fields), `src/mage_coupling.F` / `src/mage_oneway.F` (magnetosphere model coupling).
- **Data Processing and Analysis:Data Assimilation** -- `src/nudge.F90` implements Newtonian relaxation of prognostic fields toward external data with configurable horizontal/vertical sponge weights (`NUDGE_*` namelist group; the reference publication lists "(h) nudging of prognostic fields near the lower boundary from external data"), and `src/saber_tidi.F` blends SABER/TIDI observations into the lower boundary each timestep. Caveat recorded for transparency: the namelist docs do not constrain whether `NUDGE_NCFILE` holds observational or reanalysis/model fields, so the unambiguously observational evidence for this value is the SABER/TIDI ingest, not nudging alone.
- **Data Processing and Analysis:Analysis** -- `src/diags.F` + `doc/diags.table` compute 43 optional derived diagnostics from the model state, including TEC, NmF2, hmF2, foF2, Pedersen/Hall conductivities and ion-drag coefficients, height-integrated currents (`KQLAM`, `KQPHI`, `JQR`), height-integrated Joule heating, CO2/NO cooling and ExB ion drifts; `src/current.F90` computes plasma-current diagnostics.
- **Data Processing and Analysis:Processing** -- `tiegcmrun/interpolation.py` and `scripts/interpic.py` interpolate/regrid netCDF history files between horizontal and vertical resolutions (2-D and 3-D interpolation with constant/linear/exponential vertical extrapolation); input drivers are time-interpolated to model time in `src/imf.F`, `src/gpi.F`, `src/gswm.F`, `src/ctmt.F`, `src/saber_tidi.F`.
- **Coordinate Transforms / :Ionospheric** -- a user-facing, first-class capability, not an internal detail: model fields are produced on both a geographic grid and a geomagnetic **modified-apex / quasi-dipole** grid, and diagnostics are written on both (`PHIM2D`, `ED1`, `ED2` are on the magnetic grid per `doc/diags.table`). Implemented in `src/apex.F90` (refactored Richmond 1995 apex code: `apex_mka`, `apex_mall`, `apex_q2g`), `src/getapex.F`, `src/magfield.F` (geographic<->geomagnetic Jacobians, `sunloc` for magnetic local time), and `src/esmf.F` (parallel `geo2mag` / `mag2geo` regridding via ESMF route handles).
- **Coordinate Transforms:Magnetospheric** -- GEO/MAG/SM/GSM/GSE transforms are provided and used when the model is built for magnetosphere coupling: `src/geopack.F` is GEOPACK-2008 (`GEOMAG_08`, `MAGSM_08`, `SMGSW_08`, `GEOGSW_08`, `GSWGSE_08`) and `src/mage_oneway.F` performs `iSMtoGSM`/`iGSMtoSM`/`iGEOtoGSM`/`iGSMtoGEO` conversions when exchanging fields with REMIX. Scope caveat: both files are compiled under `#ifdef GAMERA`, so this applies to coupled (MAGE) builds rather than the standalone build.
- **Servers and Environments / :High Performance Computing** -- pure-MPI parallelization with domain decomposition (`src/mpi.F`, `src/timing_mpi.F`), ESMF-based parallel regridding (`src/esmf.F`), parallel netCDF4 output via `nf_create_par(..., ior(NF_NETCDF4, NF_MPIIO), ...)` (`src/nchist.F:114`), in-memory MPI coupling to GAMERA/REMIX (`src/mage_coupling.F`), and PBS batch job scripts plus per-machine make files for NCAR Derecho, NASA Aitken/Pleiades/Electra, Clemson Palmetto and generic Linux clusters (`scripts/tiegcm-*.job`, `scripts/Make.intel_de`, `scripts/Make.intel_at`, `scripts/Make.gfort_palmetto`, `tiegcmrun/template.pbs`).

*Considered and deliberately EXCLUDED (audit trail):*
- **Data Visualization (all subcategories)** -- the repository contains no plotting code. Visualization is delegated to separate packages (`gcmprocpy`, `tgcmproc_f90`, `tgcmproc_idl`; `README.md` and `doc/userguide/postproc.rst`); the PNGs under `doc/userguide/_static/images/` are documentation figures. Recorded instead in Field 30.
- **Models and Simulations:MHD** -- TIEGCM is not an MHD model. Its electrodynamics is an electrostatic field-line-integrated dynamo (`src/pdynamo.F`, `doc/description/fieldline.tex`); MHD lives in the coupled GAMERA component, which is a different package.
- **Models and Simulations:Field-line Tracing** and **Data Processing and Analysis:Field-line Tracing** -- explicitly not done: `doc/description/fieldline.tex` states "The correct way to do the field line integration would be to trace points along the field line. However, the geomagnetic grid in TIEGCM is not oriented along the field line...". `TRACE_08` exists inside the vendored GEOPACK file but is never called anywhere in `src/`.
- **Models and Simulations:Forecasting** -- no forecast/nowcast driver, no real-time data ingest; runs are retrospective or idealized (`doc/release/benchmarks.rst`).
- **Data Processing and Analysis:Data Access and Retrieval** -- no network client of any kind (no `wget`/`curl`/`requests`/`urllib` anywhere); all inputs are read from local files. Data distribution is covered by Field 17.
- **Data Processing and Analysis:File Format Conversion** -- `interpic`/`interpolation.py` read netCDF and write netCDF (resolution change, not format change); `scripts/tgcm_ncdump` is a thin `ncdump` wrapper.
- **Mission-related:\*** -- TIEGCM is not part of any mission ground system.
- **Servers and Environments:Software or Environment Container** -- no Dockerfile, Singularity definition, or container recipe in the repository.
- **Data Processing and Analysis:2D Slices** / **:Time Series Analysis** / **:Image Processing** -- no such user-facing capability; slice extraction and time-series plotting are post-processor functions.

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere
- Earth Thermosphere
- Earth Ionosphere
- Earth Auroral Subregion

*Earth Atmosphere: `doc/userguide/intro.rst` -- "a three-dimensional, time-dependent, numeric simulation model of the Earth's upper atmosphere, including the upper Stratosphere, Mesosphere and Thermosphere", plus the full ionosphere.*

*Earth Magnetosphere: the model's high-latitude forcing is magnetosphere-ionosphere coupling and it is the ionosphere-thermosphere component of MAGE -- `src/mage_coupling.F` ("Module for MPI coupling TIEGCM with GAMERA and REMIX (MAGE)") exchanges potential, auroral energy and number flux, and Pedersen/Hall conductances with the magnetosphere; `src/heelis.F` / `src/wei05sc.F` impose magnetospheric convection; `src/current.F90` and `doc/diags.table` produce field-aligned/height-integrated current diagnostics (`JQR`, `KQLAM`, `KQPHI`); `src/subaur.F90` adds sub-auroral polarization streams.*

*Earth Thermosphere: the model's full name and description identify it as a thermosphere-ionosphere model (`doc/userguide/intro.rst:4-7`), and its vertical grid spans approximately 97-600 km (`doc/userguide/grid.rst:113-125`).*

*Earth Ionosphere: ionosphere is part of the model's full name (`doc/userguide/intro.rst:4-7`), and its diagnostics include ionospheric peak height and density, critical frequency, total electron content, and Pedersen/Hall conductance (`doc/diags.table:9-11,22-24`).*

*Earth Auroral Subregion: `src/aurora.F:8-33` documents the model's auroral-oval parameterization, including auroral-circle coordinates, polar-cap drizzle, and dayside cusp flux; the `AURORA` namelist enables this parameterization (`doc/userguide/namelist.rst:149-153`).*

*Considered and excluded: **Interplanetary Space** (IMF and solar-wind values are scalar/1-D drivers of an empirical convection model, `src/imf.F`; nothing in interplanetary space is modelled), **Solar Environment** (solar EUV irradiance and eclipse geometry are inputs, `src/soldata.F`, `src/eclipse.F90`; the Sun is not modelled), **Planetary Magnetospheres** (Earth only -- IGRF-based geomagnetic field, terrestrial chemistry).*

### 6. Authors (MANDATORY)

*The author set consists of the 24 named `CITATION.cff` authors, each with an ORCID and affiliation, plus the organizational author identified by ROR. The organizational author is an additional credited entity rather than a duplicate of any person author.*

*Affiliations use the most specific organization in `CITATION.cff` and the registered ROR display name. ROR `https://ror.org/03773p874` is therefore written "NSF NCAR High Altitude Observatory"; the constructed spelling "NCAR High Altitude Observatory" is not a registered name and should not be restored. Where a specific organization has no ROR, its parent institution is also listed so at least one resolvable identifier is present. "The University of Texas at Arlington" uses ROR `https://ror.org/019kgqr73`; no identifier exists for "Space Weather Technology Research and Education Center".*

*For authors associated with both HAO and its parent NSF NCAR, both affiliations are correct: HAO (ROR `https://ror.org/03773p874`) is a laboratory within NSF NCAR (ROR `https://ror.org/05cvfcr44`), and the two are distinct organizations rather than spelling variants.*

*Author order below follows `CITATION.cff` (credit order); HSSI does not treat author order as authoritative.*

- **Author:** Haonan Wu
  - **Author Identifier:** https://orcid.org/0000-0002-3272-8106
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Wenbin Wang
  - **Author Identifier:** https://orcid.org/0000-0002-6287-4542
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Kevin H. Pham
  - **Author Identifier:** https://orcid.org/0000-0001-5031-5519
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Dong Lin
  - **Author Identifier:** https://orcid.org/0000-0003-2894-6677
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Nikhil Rao
  - **Author Identifier:** https://orcid.org/0000-0003-2639-9892
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Michael J. Wiltberger
  - **Author Identifier:** https://orcid.org/0000-0002-4844-3148
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Gang Lu
  - **Author Identifier:** https://orcid.org/0000-0001-5350-2889
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Qian Wu
  - **Author Identifier:** https://orcid.org/0000-0002-7508-3803
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Hanli Liu
  - **Author Identifier:** https://orcid.org/0000-0002-6370-0704
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Liying Qian
  - **Author Identifier:** https://orcid.org/0000-0003-2430-1388
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Chih-Ting Hsu
  - **Author Identifier:** https://orcid.org/0000-0002-8789-1277
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Nicholas M. Pedatella
  - **Author Identifier:** https://orcid.org/0000-0002-8878-5126
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Jordi Vila-Pérez
  - **Author Identifier:** https://orcid.org/0000-0003-3164-0863
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Joseph M. McInerney
  - **Author Identifier:** https://orcid.org/0000-0002-6103-3311
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Arthur D. Richmond
  - **Author Identifier:** https://orcid.org/0000-0002-6708-1023
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Alan G. Burns
  - **Author Identifier:** https://orcid.org/0000-0001-6024-0020
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Stanley C. Solomon
  - **Author Identifier:** https://orcid.org/0000-0002-5291-3034
  - **Affiliation:**
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Astrid Maute
  - **Author Identifier:** https://orcid.org/0000-0003-3393-0987
  - **Affiliation:**
    - **Organization:** Cooperative Institute for Research in Environmental Sciences
      - **Affiliation Identifier:** https://ror.org/00bdqav06
- **Author:** Eric K. Sutton
  - **Author Identifier:** https://orcid.org/0000-0003-1424-7189
  - **Affiliation:**
    - **Organization:** Space Weather Technology Research and Education Center
      - **Affiliation Identifier:** Not found
    - **Organization:** University of Colorado Boulder
      - **Affiliation Identifier:** https://ror.org/02ttsq026
- **Author:** Xian Lu
  - **Author Identifier:** https://orcid.org/0000-0002-2535-8151
  - **Affiliation:**
    - **Organization:** Clemson University
      - **Affiliation Identifier:** https://ror.org/037s24f05
- **Author:** Xuguang Cai
  - **Author Identifier:** https://orcid.org/0000-0003-4632-1697
  - **Affiliation:**
    - **Organization:** Laboratory for Atmospheric and Space Physics
      - **Affiliation Identifier:** https://ror.org/01fcjzv38
- **Author:** Cheng Sheng
  - **Author Identifier:** https://orcid.org/0000-0002-1282-8265
  - **Affiliation:**
    - **Organization:** The University of Texas at Arlington
      - **Affiliation Identifier:** https://ror.org/019kgqr73
- **Author:** Jack C. Wang
  - **Author Identifier:** https://orcid.org/0000-0003-2165-505X
  - **Affiliation:**
    - **Organization:** Community Coordinated Modeling Center
      - **Affiliation Identifier:** https://ror.org/01dy3j343
    - **Organization:** Goddard Space Flight Center
      - **Affiliation Identifier:** https://ror.org/0171mag52
- **Author:** Jia Yue
  - **Author Identifier:** https://orcid.org/0000-0003-0577-5289
  - **Affiliation:**
    - **Organization:** Community Coordinated Modeling Center
      - **Affiliation Identifier:** https://ror.org/01dy3j343
    - **Organization:** Goddard Space Flight Center
      - **Affiliation Identifier:** https://ror.org/0171mag52
- **Author:** NCAR High Altitude Observatory  *(organizational author)*
  - **Author Identifier:** https://ror.org/03773p874
  - **Affiliation:** None recorded (none present in the source DOI record)

*The organizational author above deliberately keeps the name "NCAR High Altitude Observatory", while every affiliation entry naming the same institution reads "NSF NCAR High Altitude Observatory". The difference is intentional, not drift, and must not be "reconciled" by renaming the author. Both records carry the same identifier, ROR `https://ror.org/03773p874`, and that ROR -- not the name string -- is what identifies the institution in either place. They are nonetheless two different records: HSSI can attach an author only through a person-shaped record, so an organization credited as an author is stored as one, separately from the organization record that affiliations point at. Person-shaped storage of an organizational author is a platform representation limitation rather than a data error; the record is shared with other software (see the correction note below), and its name is not changeable by a routine metadata update in any case. Renaming it to match the affiliation spelling is therefore not the remedy for the apparent mismatch -- there is nothing to remedy.*

*Sources: the 24 named authors and their ORCIDs/affiliations are from `CITATION.cff` lines 8-104 at revision `cedd16df` (the same 24 also appear as the `preferred-citation` authors, and Crossref reports 24 authors for DOI 10.1029/2025JA034219). The organizational author is from the existing HSSI record and is corroborated by DataCite, which gives the sole creator as `{"name": "High Altitude Observatory", "nameType": "Organizational", "nameIdentifiers": [ROR 03773p874, ISNI 0000 0000 8976 9350]}`. ROR `03773p874` is active; `ror_display` = "NSF NCAR High Altitude Observatory", alias "High Altitude Observatory", acronym "HAO", parents University Corporation for Atmospheric Research and NSF National Center for Atmospheric Research.*

#### Historical correction -- three author names (2026-07-29)

Three earlier author forms were incorrect: `High Altitude` / `Observatory` was a person-shaped split of the organization name and is represented here as `NCAR High Altitude Observatory`; `Kevin` and `Michael` omitted the middle initials supplied by `CITATION.cff` and are represented as `Kevin H.` and `Michael J.` Identifiers were unchanged.

The organizational author needed the fix because HSSI author relationships can only reference person records, so an organization must be stored as one -- a schema limitation, not a data error -- and DataCite supplies the creator as the single unstructured string `"High Altitude Observatory"` (`nameType: "Organizational"`), which was split on the last word boundary into a person-shaped pair. Keeping the whole organization name in one component is what lets the record read as an organization rather than a person; the durable key is the ROR identifier, not the string, so this author record's spelling is not required to track the spelling of the organization record that shares the same ROR. The two personal names restore the middle initials given in `CITATION.cff` at revision `cedd16df`.

### 7. Software Name (MANDATORY)
TIEGCM v3.0

*Source: `README.md` line 1 is `# TIEGCM v3.0`, SoMEF's `full_title` is "TIEGCM v3.0", and the Zenodo/DataCite title is "TIEGCM v3.0".*

*Documented alternative (considered, not adopted): embedding a version in the name now sits slightly oddly against Field 12, which advances to 3.0.1 -- the entry will render as "TIEGCM v3.0" with version "3.0.1". `CITATION.cff` line 3 gives the fuller formal title "NCAR-TIEGCM: Thermosphere-Ionosphere-Electrodynamics General Circulation Model", and "TIEGCM" alone would be version-neutral. This is a stylistic/editorial choice; the submitted value was retained by decision.*

### 8. Description (MANDATORY)
The NCAR Thermosphere-Ionosphere-Electrodynamics General Circulation Model (TIEGCM) is a comprehensive, first-principles, three-dimensional, time-dependent numerical model of Earth's upper atmosphere, spanning the upper stratosphere, mesosphere, thermosphere and ionosphere. It solves the coupled momentum, energy and continuity equations for neutral and ionized species on a pressure-based vertical coordinate using semi-implicit fourth-order finite differences with sub-minute time steps, and includes a self-consistent solution of the middle- and low-latitude ionospheric wind dynamo on a geomagnetic apex grid. Output fields include neutral temperature and winds, major and minor neutral composition (O2, O, N(4S), N(2D), NO, He, Ar), ion and electron temperatures, electron and ion densities, vertical motion, geopotential height, electric potential and electric fields, Pedersen and Hall conductivities, currents, Joule heating, and derived ionospheric parameters such as NmF2, hmF2, foF2 and total electron content. Solar forcing may be specified from the F10.7 proxy or from measured solar EUV spectral irradiance; high-latitude forcing may come from the Heelis or Weimer empirical convection models, from AMIE output, or from in-memory MPI coupling to the GAMERA and REMIX magnetosphere models within MAGE; lower-boundary forcing may come from tidal climatologies (GSWM, CTMT, Hough modes), from SABER and TIDI observations, or by nudging toward external fields. Version 3.0 added flexible horizontal and vertical resolutions (5 to 0.625 degrees), an extended upper boundary, high-cadence model time, a rewritten helium module, a ring filter, O+ sub-cycling, parallel netCDF4 I/O, bit-for-bit reproducibility, an updated IGRF, a rewritten magnetospheric coupling module, and new capabilities including empirical SAPS, electrojet turbulent heating, field-aligned ion drag and solar-eclipse EUV masking. The model is written in standard Fortran 90, parallelized with MPI, requires the netCDF and ESMF libraries, and runs on Linux workstations and clusters; the bundled Python utility tiegcmrun automates configuration, build and job submission. Use of the source code is governed by the NCAR TIE-GCM Open Source Academic Research License Agreement, which permits use for research, academic and non-profit purposes only; NCAR retains all rights to the TIE-GCM source code. The persistent identifier recorded for this entry is a third-party Zenodo deposit of a copy of the source code as of April 14, 2025, made to support the study "Modulation of Thermospheric Circulation by Lower-Thermospheric Winter-to-Summer Circulation: The Atmosphere Gear Effect" (Wang et al., 2025); the authoritative source is the official NCAR repository.

*Historical correction approved 2026-07-28: the prior description opened with GitHub's repository blurb rather than describing the model; mis-transcribed Wang et al.'s title as "The Atmospheric Gear Effect" rather than "The Atmosphere Gear Effect"; and incorrectly applied the deposit fork's "solely for reproducibility and reference" caveat to the actively developed official NCAR repository. The replacement preserves the true DOI provenance, study connection, and NCAR rights statement while describing the software itself.*

*Seeded value (verbatim, for comparison): "The Official NCAR TIEGCM GitHub repository. The DOI is for a copy of the source code released by the official NCAR TIE-GCM repository as of April 14, 2025. The model was used in the study \"Modulation of Thermospheric Circulation by Lower-Thermospheric Winter-to-Summer Circulation: The Atmospheric Gear Effect\" (Wang et al., 2025). NCAR retains all rights to the TIE-GCM source code; this repository is provided solely for reproducibility and reference."*

1. *The seeded text describes **the Zenodo deposit and its repository**, not the software. Field 8 requires text "sufficiently detailed to provide the potential user with information to determine if the software is useful to their work... what the software does, why to use it, assumptions it makes". The seeded text says nothing about what TIEGCM computes, and its first 150-200 characters -- the search-result preview -- read as a repository blurb ("The Official NCAR TIEGCM GitHub repository...", which is literally the GitHub repo `description` field). For the flagship NCAR upper-atmosphere GCM this is the single largest metadata-quality gap in the entry.*
2. *Two statements in it are attached to the wrong object. "This repository is provided solely for reproducibility and reference" is true of the **fork** the deposit was made from (`j0a8c2k1/tiegcm`, per DataCite `IsSupplementTo`) and is **false of `NCAR/tiegcm`**, which is the actively developed official repository (264 commits since tag `tiegcm2.9`, last push 2026-06-16). Leaving that sentence attached to a record whose Code Repository is `NCAR/tiegcm` actively misleads users. The paper title is also mis-transcribed: Crossref gives "The Atmosphere Gear Effect", not "Atmospheric" (DOI 10.1029/2024GL113414).*
3. *Everything in the seeded text that is true and useful is **preserved** in the replacement: the DOI-is-a-copy-as-of-April-14-2025 provenance, the Wang et al. (2025) connection (with the title corrected and its DOI now recorded in Field 27), and the NCAR rights statement.*

*Sources for the new text: https://tiegcm-docs.readthedocs.io/en/latest/tiegcm/intro.html (functional description, numerics, strengths, inputs, outputs, hardware/software requirements -- quoted phrase "comprehensive, first-principles, three-dimensional, non-linear representation of the coupled thermosphere and ionosphere system that includes a self-consistent solution of the middle and low-latitude dynamo field"); `doc/userguide/intro.rst`; `doc/userguide/output.rst` and `doc/diags.table` (output fields and diagnostics); `README.md` lines 23-108 (v3.0 feature and physics changes); `LICENSE`; `CITATION.cff`; DataCite record for 10.5281/zenodo.15214470.*

### 9. Concise Description (OPTIONAL)
First-principles three-dimensional model of Earth's coupled thermosphere and ionosphere, with a self-consistent low- and mid-latitude wind dynamo on a geomagnetic apex grid.

*Source: condensed from https://tiegcm-docs.readthedocs.io/en/latest/tiegcm/intro.html. At 173 characters, this provides a self-contained preview of the longer description.*

### 10. Publication Date (RECOMMENDED)
2025-04-14

*Source: DataCite and Zenodo both give 2025-04-14 as the issue/publication date of the concept DOI.*

*Documented alternatives (considered, not adopted). Field 10 is defined as "date of first broadcast/publication... used for the initial version of the software", and by that definition 2025-04-14 is arguably wrong: it is the date a third party deposited a snapshot, roughly three decades after TIEGCM was first published. Candidates, in decreasing defensibility: (a) **2004-04-02** -- the earliest commit and earliest tags (`start`, `tiegcm1`) in this repository, i.e. the start of the preserved version history; (b) **2016-09-19** -- GitHub repository creation (`created_at`, GitHub API), which is only when the code moved to GitHub from HAO's SVN; (c) the model's first description in the literature (Richmond, Ridley & Roble 1992, GRL), which is a publication date, not a software release date. No candidate is clearly authoritative, and the seeded value is at least the correct issue date of the record's own persistent identifier; it was retained by decision.*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Source: DataCite gives `publisher: "Zenodo"`, consistent with Field 11's guidance for a Zenodo DOI. The third-party depositor does not change the DOI's publisher.*

### 12. Version (RECOMMENDED)

**Current version:**
- **Version Number:** `3.0.1`  *(store BARE -- the view layer renders `<software name> - <number>`, i.e. "TIEGCM v3.0 - 3.0.1". Never store the rendered prefix.)*
- **Version Date:** 2026-05-07
- **Version Description:** Release accompanying the JGR: Space Physics paper "The NCAR-TIEGCM Version 3.0" (doi:10.1029/2025JA034219). Adds `CITATION.cff` with the full author list and preferred citation; adds parallel ion velocity to the output; adds NASA Aitken and Electra node support; fixes year-boundary handling and the last-segment `PRISTOP` day; renames some output variables; extends `SECFLDS`; updates the README for data files and utility tools.
- **Version PID:** Not found -- no DOI exists for 3.0.1 (see note below).

**Historical correction approved 2026-07-28:** the prior `v1.0.0` entry, dated 2025-04-15 with PID `https://doi.org/10.5281/zenodo.15214471`, is not a TIEGCM version number. It is the third-party Zenodo deposit's own label. Keeping it as a software version would falsely imply that it preceded TIEGCM 3.0.1. Field 2 preserves the deposit's concept DOI and provenance, while Field 12 records the actual software release.

*CORRECTION RECORD. The seeded record's only version was `v1.0.0`, which is **the Zenodo deposit's own version label, not the TIEGCM software version** -- the fork the deposit was made from was tagged `v1.0.0` (DataCite: `IsSupplementTo -> https://github.com/j0a8c2k1/tiegcm/tree/v1.0.0`), and DataCite reports `version: "v1.0.0"` for the deposit. TIEGCM itself has never had a 1.0.0; its version series is 1.x -> 2.0 -> 2.9 -> 3.0.x.*

*Evidence for 3.0.1 being the current authoritative release: `CITATION.cff` line 4 declares `version: "3.0.1"`; the git tag `TIEGCM-3.0.1` points exactly at HEAD (`git rev-list --count TIEGCM-3.0.1..HEAD` = 0); the GitHub release "TIEGCM 3.0.1" (`tag_name: TIEGCM-3.0.1`, `prerelease: false`) was published 2026-05-07T22:43:45Z, matching the tagged commit date 2026-05-07. The next-most-recent tags are `MAGE_*` coupled-model tags (a different release line sharing this repository) and legacy `tiegcm2.9`/`tiegcm2.0`/`tiegcm1.9x` tags. Version-number form: `3.0.1` is used because that is the form `CITATION.cff` declares; `TIEGCM-3.0.1` (git tag) and `v3.0.1` (release-body heading) are the same release under different labels.*

*Version PID: none. The only Zenodo deposit for this software is the 2025 third-party mirror; there is no GitHub-Zenodo integration in the repository and no DOI badge, so release 3.0.1 has no version DOI. The PID `https://doi.org/10.5281/zenodo.15214471` is the version DOI **of the mirror deposit**, not of any TIEGCM release, and **must not be attached to 3.0.1**. With the `v1.0.0` entry removed, that DOI is no longer carried in Field 12; the deposit remains fully identified through Field 2's concept DOI `https://doi.org/10.5281/zenodo.15214470` and the provenance caveat recorded there.*

### 13. Programming Language (RECOMMENDED)
- Fortran90
- Python 3.x

*Source: current documentation states that the model uses "standard FORTRAN-90" and the source tree is `.F`/`.F90`/`.h`; `tiegcmrun/` uses Python 3.*

*Considered and excluded: adding `Other` to cover the Shell job scripts (`scripts/tiegcm-*.job`, `tiegcmrun/setEnvironment.sh`), the Perl utilities (`scripts/mkdepends`, `scripts/mklogs`) and the makefiles -- Field 13 explicitly asks for "the most important languages... not meant to be exhaustive", and these are build/run glue rather than the software's implementation language. Also considered and excluded: `Fortran 2003` / `Fortran 2008` -- the free-form `.F90` files use only Fortran 90/95 features and the documentation claims f90 compliance.*

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1029/2025JA034219

*Source: `CITATION.cff` names this as the preferred citation for TIEGCM 3.0, and the `TIEGCM-3.0.1` release notes ask users to cite it. Crossref identifies the paper as "The NCAR-TIEGCM Version 3.0" in JGR: Space Physics with the same 24 authors.*

### 15. License (RECOMMENDED)
- **License:** Other
- **License URI:** https://github.com/NCAR/tiegcm/blob/master/LICENSE

*`Other` is the closest controlled value because the repository uses a custom non-SPDX license.*

*Reasoning. The repository's `LICENSE` is the custom **"NCAR TIE-GCM OPEN SOURCE ACADEMIC RESEARCH LICENSE AGREEMENT"**: UCAR, NCAR and HAO grant a non-exclusive, non-transferable, world-wide, royalty-free license to use, reproduce and prepare derivative works "for research, academic, and non-profit purposes only", and it states that it applies to TIE-GCM Version 2, Version 3 and subsequent 3.xx versions. It is not an SPDX license and not OSI-approved; GitHub's own license detection independently reports `key: "other"`, `spdx_id: "NOASSERTION"`. `CITATION.cff` line 6 points at this same file (`license-url: https://github.com/NCAR/TIEGCM/blob/master/LICENSE`). A second copy ships as `src/tiegcmlicense.txt` and `doc/userguide/_static/tiegcmlicense.txt`, and nearly every source file carries the header "Use is governed by the Open Source Academic Research License Agreement contained in the file tiegcmlicense.txt".*

*Conflict resolved in favour of the repository. Zenodo/DataCite label the deposit `cc-by-4.0` ("Creative Commons Attribution 4.0 International"), which is available in HSSI's list but is **not** the software's license: CC-BY-4.0 permits commercial use and the NCAR agreement expressly does not. That label describes the third-party Zenodo deposit's own terms and cannot override the licensor's terms shipped with the code. The repository LICENSE is therefore authoritative and `Other` is recorded.*

*Why not `Restricted`: Field 15 reserves that for restricted software, and Field 3's guidance ties "restricted" to needing to request access. TIEGCM's source is openly and anonymously downloadable from a public GitHub repository -- the restriction is on the PURPOSE of use, not on access. Recorded as `Other` with the license URI so users can read the actual terms.*

*Additional nuance worth preserving: not all bundled source is under the NCAR agreement -- `src/subaur.F90` (the SAPS electric-field model) carries "Copyright 2009 The Johns Hopkins University Applied Physics Laboratory. All rights reserved." This reinforces `Other` over any single SPDX identifier.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- TIEGCM
- thermosphere
- ionosphere
- mesosphere
- upper atmosphere
- electrodynamics
- aeronomy
- ionosphere thermosphere mesosphere
- space weather
- simulation
- physics-based model
- high performance computing
- netcdf
- fortran
- total electron content
- magnetic apex coordinates
- aurora
- mage
- general circulation model
- thermospheric tides
- joule heating
- ionospheric electrodynamo
- helium
- solar eclipse

*The values use their exact vocabulary spelling. Six terms were selected by user approval on 2026-07-28 because they capture important, well-evidenced capabilities: `general circulation model` (TIEGCM's model class); `thermospheric tides` (`src/gswm.F`, `src/ctmt.F`, `src/saber_tidi.F`); `joule heating` (`QJOULE`, `QJOULE_INTEG`); `ionospheric electrodynamo` (`src/pdynamo.F`); `helium` (`src/comp.F`, `src/he_coefs.F90`); and `solar eclipse` (`src/eclipse.F90`).*

*Scope note: this keyword expansion is distinct from the Field 22 Phenomena vocabulary, which the user explicitly directed must NOT be expanded. `solar eclipse` is added here as a free-form discovery keyword only; no `Solar Eclipses` Phenomena row is created. See Field 22.*

*Vocabulary spelling note: keywords are not uniformly lowercase; the mixed-case `TIEGCM` value is therefore intentional.*


*Evidence for the selections: `TIEGCM` and `mage` (this software, and its role as the ionosphere-thermosphere component of MAGE, `src/mage_coupling.F`); `thermosphere` / `ionosphere` / `mesosphere` / `upper atmosphere` / `ionosphere thermosphere mesosphere` (`doc/userguide/intro.rst` domain); `electrodynamics` (`src/pdynamo.F`, and the model's own name); `aeronomy` (documentation "Strengths": "Calculates all important aeronomic parameters and minor species"); `simulation` and `physics-based model` (first-principles GCM); `high performance computing` (MPI/ESMF/PBS -- `src/mpi.F`, `scripts/*.job`); `netcdf` (all I/O); `fortran`; `total electron content` and `magnetic apex coordinates` (`doc/diags.table` TEC diagnostic, `src/apex.F90`); `aurora` (`src/aurora.F`, `AURORA` namelist); `space weather` (storm-time simulation and MAGE coupling).*

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific
- FTP/FTPS Directories
- HTTP/HTTPS Directories
- Other

*Evidence: **Observatory/Mission-specific** -- documented namelist inputs read specific instruments' data files: `SABER_NCFILE` and `TIDI_NCFILE` (`src/saber_tidi.F`: "Read and import netcdf files containing SABER (T,Z) and TIDI (U,V) data") and `see_ncfile` (`src/soldata.F`, written into history metadata as "TIMED SEE data file" at `src/nchist.F:1787`). Cross-listed with Field 32 exactly as Field 17's guidance instructs. **HTTP/HTTPS Directories** -- the model's required input and startup data sets are distributed from HAO over HTTP (`doc/README.download`: `http://www.hao.ucar.edu/modeling/tgcm/download.php`; the "TIEGCM Data Files" link in `README.md`). **FTP/FTPS Directories** -- `README.md`: "Additional data may be available on the HAO public FTP site: http://download.hao.ucar.edu/pub/tgcm". **Other** -- benchmark history files are distributed through the Globus research data-sharing service via the "NCAR Data Sharing Service" endpoint (`doc/release/benchmarks.rst`, `doc/userguide/benchmarks.rst`), which no listed value covers.*

*Transparency caveat: the software contains **no network client** (no `wget`/`curl`/`requests`/`urllib` anywhere in the tree); every read is from a local file. The values above describe where the supported input data comes from and how the documentation instructs users to obtain it, which is the normal reading of this field for a model.*

*Considered and EXCLUDED: **CDAWeb** and **OMNIWeb** -- `doc/userguide/namelist.rst` documents that the `IMF_NCFILE` driver files were **derived by HAO** from 1-minute OMNI data obtained from CDAWeb (gap-filling, 15-minute trailing average lagged 5 minutes, 5-minute sampling, quality mask). That is the provenance of a pre-built input file, not a source the software can query; a user searching HSSI for `CDAWeb` should not get TIEGCM back. They are therefore recorded as evidence of that provenance rather than as values of this field. Also excluded: HAPI, das2, SSCWeb, TAP, VirES, The Virtual Solar Observatory, S3/Cloud-aware -- no evidence of any.*

### 18. Input File Formats (RECOMMENDED)
- netCDF3/4
- HDF5
- JSON
- ascii

*Evidence: **netCDF3/4** -- every scientific input is netCDF: the startup/`SOURCE` history, `GPI_NCFILE`, `IMF_NCFILE`, the SEE flux file, `GSWM_*`, `CTMT_NCFILE`, `BGRDDATA_NCFILE`, `SABER_NCFILE`, `TIDI_NCFILE`, `HE_COEFS_NCFILE`, `AMIENH`/`AMIESH`, `ECLIPSE_LIST` and `NUDGE_NCFILE` (`src/input.F`, `src/nchist.F`, `src/eclipse.F90` `read_eclipse_list`); the documentation states the required library is netCDF and the data format is "netCDF format". **HDF5** -- one-way coupling reads the REMIX magnetosphere output file `msphere.mix.h5` and navigates its HDF5 group hierarchy (`src/mage_oneway.F`: `nf90_open`, `nf90_inq_grp_ncid`; namelist `MIXFILE` / `ONEWAY`, described as "Read remix h5 file"). **JSON** -- `tiegcmrun` reads `benchmarks.json`, `options_description.json` and the coupled-run `engage.json` (`tiegcmrun/tiegcmrun.py`, `tiegcmrun/engage_solver.py:engage_parser`). **ascii** -- the model's primary control input is a Fortran namelist text file (`scripts/tiegcm_default.inp`, `tiegcmrun/template.inp`, `&tgcm_input ...`).*

*Considered and excluded: CDF, FITS, IDL.sav, ISTP-Compliant, csv, Zarr -- none appears anywhere in the tree.*

### 19. Output File Formats (RECOMMENDED)
- netCDF3/4
- JSON
- ascii

*Evidence: **netCDF3/4** -- primary and secondary history files are netCDF-4 written with parallel MPI-IO: `istat = nf_create_par(flnm, ior(NF_NETCDF4, NF_MPIIO), ...)` (`src/nchist.F:114`); `doc/userguide/output.rst` documents the history files and states they are CF-compliant ("conform to the NetCDF Climate and Forecast (CF) Metadata Convention"); `README.md` lists "NetCDF4 Parallel IO" as a v3.0 feature. **JSON** -- `tiegcmrun` writes the resolved run configuration to `<run_name>.json` (`tiegcmrun/output_solver.py:119-120`, `tiegcmrun/tiegcmrun.py:1029,1068`). **ascii** -- the generated namelist input files and PBS scripts (`tiegcmrun/output_solver.py` `create_inp_scripts` / `create_pbs_scripts`, from `template.inp` / `template.pbs`) and the model's stdout log (`doc/userguide/_static/tiegcm_task0000.out`); `scripts/tgcm_ncdump` and `scripts/tgcm_contents` produce ascii dumps.*

*Considered and excluded: CDF, FITS, HDF5 (HDF5 is read, never written), IDL.sav, csv, ISTP-Compliant, Zarr.*

### 20. Operating System (RECOMMENDED)
- Linux

*Evidence: the current documentation's hardware/software requirements give the platforms as "Linux clusters and workstations"; `doc/userguide/build.rst` names 64-bit Linux desktop and Linux cluster support; the make files use Linux ESMF builds; and `tiegcmrun` recognizes `derecho`, `aitken`, and `linux`.*

*Considered and excluded: **Mac** -- `doc/userguide/build.rst` notes the model "has been built and executed on several other platforms" but names none, and no macOS build recipe, CI configuration or Darwin ESMF path exists; the only Mac reference in the tree is a Globus screenshot of transferring output files to a MacBook. **Windows**, **Solaris**, **OS Independent** / **Operating System Independent** -- no evidence (the model requires MPI, ESMF and netCDF-Fortran and ships PBS job scripts, so it is not OS-independent).*

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- HPC or HEC

*Evidence: **x86-64** is supported across NCAR Derecho, NASA Pleiades/Aitken/Electra, Clemson Palmetto, and generic 64-bit Linux build files. **HPC or HEC** is supported by PBS scripts and resource templates, MPI domain decomposition, ESMF parallel regridding, and parallel netCDF4 MPI-IO.*

*Considered and excluded: **GPU** (no CUDA, OpenACC or OpenMP-offload directives anywhere), **Apple Silicon arm64** / **Linux aarch64 or arm64** / **ppc64le** / **Sun (SPARC)** (no build support), **CPU Independent** (compiled Fortran with per-architecture optimization flags).*

### 22. Related Phenomena (OPTIONAL)
- Geomagnetic Storms
- Solar Flares

*Evidence: **Geomagnetic Storms** -- storm simulation is a primary documented use. The benchmark suite consists of named storm events (`doc/release/benchmarks.rst` and `doc/release/_static/namelist_files/`: `nov2003`, `dec2006`, `jul2000`, `whi2008`, with Heelis/GPI and Weimer/IMF driving); the namelist documentation warns about IMF data quality "before doing storm simulations... the 'Halloween Storm'"; and the reference publication presents "examples of the model validation during a moderate storm". Storm-time high-latitude forcing is implemented throughout (`src/wei05sc.F`, `src/aurora.F`, `src/amie.F`, `src/subaur.F90` SAPS).*
***Solar Flares** -- asserted on the strength of the model's own peer-reviewed description paper for this exact version (Field 14, DOI 10.1029/2025JA034219), whose abstract lists among the v3.0 additions "(k) new functionalities enabling model simulations of certain recurrent phenomena, such as solar flares and eclipses". Transparency caveat: the string "flare" does not appear anywhere in the source tree; the enabling mechanism is time-varying solar forcing -- measured EUV spectral irradiance (`src/soldata.F` + `see_ncfile`) and time-dependent `F107` / `f107_time` (`src/input.F`) -- rather than a module named for flares.*

*Considered and EXCLUDED: **Solar Wind** -- solar-wind density and velocity are scalar inputs that drive the Weimer convection model (`src/imf.F`, namelist `SWDEN` / `SWVEL`); the software provides no science functionality FOR the solar wind. **Coronal Mass Ejections / Coronal Heating / Solar Corona / X-ray emission** -- no solar-atmosphere functionality.*

*Settled user decision 2026-07-28: the Phenomena vocabulary is not expanded, so only the two supported existing values above are selected.*

*Considered and explicitly declined as new Phenomena rows: `Solar Eclipses` (`src/eclipse.F90`, `DOECLIPSE`, `ECLIPSE_LIST`); `Atmospheric Tides` (`src/gswm.F`, `src/ctmt.F`, `src/saber_tidi.F`); `Sub-Auroral Polarization Streams` (`src/subaur.F90`); `Aurora` (`src/aurora.F`); and `Joule Heating` (`QJOULE`, `QJOULE_INTEG`).*

*Where the underlying capabilities are still discoverable: `solar eclipse`, `thermospheric tides` and `joule heating` were approved as **Field 16 keywords** (a separate, free-form vocabulary the user did permit expanding), so the eclipse, tidal and Joule-heating functionality remains searchable without expanding the Phenomena vocabulary.*

### 23. Development Status (RECOMMENDED)
Active

*Per repostatus.org, "Active" means a stable, usable project under active development. TIEGCM has a non-prerelease 3.0.1 release dated 2026-05-07, subsequent repository activity, an active issue and pull-request workflow, a maintained companion tool, and current documentation. It is neither archived nor moved.*

### 24. Documentation (RECOMMENDED)
https://tiegcm-docs.readthedocs.io/en/latest/

*Source: `README.md` line 3, the GitHub repository homepage, and SoMEF all point to this documentation site. It covers the model, inputs and outputs, release notes, environments, quickstart, source, analysis, and benchmarks. The in-repository `doc/userguide/` tree is partly stale, so the ReadTheDocs site is the appropriate target.*

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
  - **Funder Identifier:** https://ror.org/027ka1x80
- **Organization:** U.S. National Science Foundation
  - **Funder Identifier:** https://ror.org/021nxhr62

*Source: Crossref funding metadata for the reference publication lists National Aeronautics and Space Administration and National Science Foundation. Their names are written in full and paired with their ROR identifiers. This is consistent with development at NSF NCAR HAO and NASA DRIVE-supported MAGE coupling.*

*Naming convention, the same rule Field 6 applies to affiliations: the funder carrying ROR `https://ror.org/021nxhr62` is named "U.S. National Science Foundation" -- the `label` / `ror_display` form ROR registers for it -- so that spelling is used. "National Science Foundation" is registered only as an alias, alongside the acronym "NSF" and a second alias "United States National Science Foundation"; the registered display form is the settled name here, and the bare alias should not be restored. Nothing was renamed -- the alias had simply been recorded where the display form belongs. The NASA entry needs no such correction: "National Aeronautics and Space Administration" is already the `ror_display` form registered for ROR `https://ror.org/027ka1x80`.*

### 26. Award Title (OPTIONAL)
Not found -- no award title or number is asserted anywhere in the repository (no funding statement in `README.md`, `CITATION.cff` or `LICENSE`; DataCite `fundingReferences` for the DOI is empty).

*Deliberate non-population, with the raw material kept as evidence for why no defensible title exists. The reference publication's Crossref record does carry 20 award numbers, but no award **titles**, and they are the acknowledgements of a 24-author paper -- attributing all 20 to this software would over-claim, and creating 20 title-less Award rows in a shared table would degrade rather than improve the record. The numbers, with their Crossref funder attribution, are:*

- *National Aeronautics and Space Administration: 80NSSC22M0163, 80NSSC21K1315, 80NSSC21K0008, 80NSSC23K1055, 80NSSC22K1635, 80NSSC21K1677, 80NSSC20K1784, 80NSSC21K1673, 80NSSC23K1123, NNG12FA45C, 80NSSC22K0018, NNX17AG10G, 80NSSC22K1010, 80NSSCK19K0810*
- *National Science Foundation: 1852977, 2223931, 2431688, 2149695, 1753214, 2437053*

*Were Field 26 ever populated, the most defensible entry would be NASA `80NSSC22M0163`, the DRIVE Science Center award behind the Center for Geospace Storms / MAGE effort in which TIEGCM is the ionosphere-thermosphere component (`src/mage_coupling.F`) -- but an award **title** would have to come from elsewhere, since neither the repository nor Crossref provides one. Left unpopulated by decision.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2024GL113414
- https://doi.org/10.1002/2015JA021223
- https://doi.org/10.1002/2013JA019744

*All three are distinct from the Field 14 reference publication.*

1. *`10.1029/2024GL113414` -- Wang et al. (2025), "Modulation of Thermospheric Circulation by Lower-Thermospheric Winter-to-Summer Circulation: The Atmosphere Gear Effect", Geophysical Research Letters, published 2025-05-19. This is the study named in the seeded HSSI description and in the Zenodo deposit's own description as the reason the snapshot was deposited -- i.e. a publication that used this software, already prioritized by the record itself but never captured as a DOI. Resolved via Crossref; note that the seeded description mis-transcribes the title as "Atmospheric Gear Effect".*
2. *`10.1002/2015JA021223` -- Sutton et al. (2015), JGR 120, 6884. Cited by the project's own release notes as the description of the helium implementation: `doc/release/release_notes.rst` -- "See Sutton et al. (2015), JGR, 120, 6884, doi:10.1002/2015JA021223 for details of the implementation and results."*
3. *`10.1002/2013JA019744` -- Jones et al. (2014), JGR 119, 2197. Cited by the release notes as the basis of the zonal-mean lower-boundary climatology (`BGRDDATA_NCFILE`) implemented in the model.*

*Considered and EXCLUDED (references for third-party model components the software merely USES; they describe those components rather than describing, citing or using TIEGCM): `10.1029/2004JA010884` (Weimer 2005 convection model, cited in `src/wei05sc.F`), `10.1029/2011JA016784` (Oberheide et al. 2011 CTMT tidal climatology, cited in `src/ctmt.F` and `doc/userguide/namelist.rst`), `10.1029/2008JA013384` (Fang et al. 2008 electron-impact ionization parameterization, cited in `src/aurora.F`), `10.1029/2004JA010765` and `10.1029/2005JA011160` (component references in `doc/description/main.bib`).*

### 28. Related Datasets (OPTIONAL)
Not found -- no dataset DOI or persistent dataset identifier appears anywhere in the repository, and DataCite reports no `Dataset` related identifiers for the software DOI.

*Recorded for completeness: the data collections the software works with all lack persistent identifiers. They are the `TGCMDATA` input/startup collection distributed as tar files from HAO's download page (`doc/README.download`) and via the "TIEGCM Data Files" link in `README.md`; the benchmark history-file archive on the NCAR Data Sharing Service Globus endpoint (`doc/release/benchmarks.rst`); and the individual driver files (`gpi_ncfile` built from NOAA NGDC Kp/F10.7 ascii data, `imf_OMNI_*.nc` derived from CDAWeb OMNI 1-minute data, the GSWM and CTMT tidal climatologies, `saber_lbcs_tngph_windiihrdi_unvn_notides.nc`, the TIMED SEE spectral flux file, and AMIE output). None is published with a DOI or an hpde.io identifier that could be cited here without fabrication.*

### 29. Related Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.11205526

*The **Earth System Modeling Framework (ESMF)** concept DOI comes from the repository's own DOI badge.*

*Relevance-gate justification: ESMF passes as an important, domain-specific dependency, not as generic infrastructure. It is **required to build the model at all** -- `doc/userguide/build.rst`: "External library dependencies are netCDF, MPI, and ESMF... To build the [model], the ESMF library must be included in the link step" -- and its role here is specifically geophysical: `src/esmf.F` uses ESMF regridding route handles to remap fields between the geographic and geomagnetic apex grids in the MPI environment (`routehandle_geo2mag`, `routehandle_mag2geo`). It fails the "equally at home in a web app, a finance model, or a biology pipeline" test, since ESMF exists only for Earth-system model coupling and grid remapping. Its presence tells a reader something real about TIEGCM (a parallel dual-grid dynamo), which is exactly what Field 29 is for.*

*Considered and EXCLUDED, with reasons (audit trail):*
- ***MPI*** *-- generic parallel-computing infrastructure, equally present in unrelated domains. Tier A treatment.*
- ***netCDF / netCDF-Fortran*** *-- Tier B, and here it is purely a file format, already recorded in Fields 18/19. No API-level exchange with another tool is claimed.*
- ***numpy, netCDF4, xarray, jinja2*** *(`tiegcmrun/requirements.txt`) -- generic scientific-Python and templating stack used internally by the run tool; no documented interchange. Tier A/B exclusions.*
- ***GEOPACK-2008*** *-- vendored **inside** this repository as `src/geopack.F`, so it is part of the source rather than a related package; and HSSI's existing "geopack" entry is a different, Python implementation, so pointing at it would misidentify the dependency.*
- ***Heelis / Weimer 2001 and 2005 / GSWM / CTMT / Roble-Ridley aurora / APL SAPS models*** *-- embedded model components (`src/heelis.F`, `src/wei05sc.F`, `src/gswm.F`, `src/ctmt.F`, `src/aurora.F`, `src/subaur.F90`), not separately distributed software packages with repositories or DOIs. Their describing publications were considered for Field 27 and excluded there too.*
- ***AMIE / AMGeO*** *-- TIEGCM reads AMIE output files (`src/amie.F`, namelist `AMIENH` / `AMIESH`, obtained by contacting the AMIE author), but the HAO AMIE procedure is not a published software package, and HSSI's `AMGeO` entry is a distinct successor package with no demonstrated file-level or API-level exchange with TIEGCM.*
- ***CESM / WACCM-X*** *-- an obvious peer NCAR upper-atmosphere model, and `gcmprocpy` post-processes both, but there is **no** reference to WACCM-X or CESM anywhere in this repository and no demonstrated exchange, so asserting the link would rest on domain intuition rather than evidence. It is recorded here as a considered-and-rejected "performs similar tasks" candidate, so that it is not re-proposed without new evidence.*
- ***tgcmproc_f90 / tgcmproc_idl / utproc*** *-- HAO post-processors named in `doc/userguide/postproc.rst`, but that page is legacy 2.0 documentation, the tools are distributed only from an HAO download page with no repository or DOI, and the v3.0-era replacement (`gcmprocpy`) is recorded in Field 30 instead.*

### 30. Interoperable Software (OPTIONAL)
- https://github.com/NCAR/gcmprocpy
- https://doi.org/10.5281/zenodo.16818620
- https://doi.org/10.5281/zenodo.3344536
- https://github.com/nasa/Kamodo

*Each entry has a specific demonstrated exchange rather than shared-ecosystem membership.*

1. ***gcmprocpy*** *(`https://github.com/NCAR/gcmprocpy`; no DOI exists, so the repository URL is used). Companion post-processing and visualization package for this model's output, documented in both directions: `README.md` "Utility Tools" -- "Tiegcmpy is a Python tool ([GCMProcpy github]) that is used for post processing and data visualization of TIEGCM outputs" -- and the `TIEGCM-3.0.1` release notes link it as "Post-processing (gcmprocpy)"; gcmprocpy's own README describes itself as "a post-processing and plot generation tool for TIE-GCM and WACCM-X NetCDF output", and its PyHC community-registry entry reads "A Python package for post processing and analysis of TIE-GCM and WACCM-X outputs". The exchange object is the netCDF history file written by `src/nchist.F`.*
2. ***Kaiju*** *(`https://doi.org/10.5281/zenodo.16818620`). Kaiju contains the MAGE components GAMERA and REMIX, and TIEGCM is MAGE's ionosphere-thermosphere component. Two concrete exchanges: (a) in-memory two-way **MPI field exchange** -- `src/mage_coupling.F` ("Module for MPI coupling TIEGCM with GAMERA and REMIX (MAGE)") sends REMIX the TIEGCM grid and exchanges potential, auroral energy and number flux, and Pedersen/Hall conductances; (b) **file-level one-way coupling** -- `src/mage_oneway.F` reads REMIX's `msphere.mix.h5` output (namelist `ONEWAY` / `MIXFILE`: "Enable one-way coupling from remix to TIEGCM. Read remix h5 file"). Confirmed from the other side: Kaiju ships `src/remix/tgcm.F90` and `docs/source/makeitso/engage_template/{derecho,aitken,pleiades}/tiegcmrun_input.json`, and this repository's `tiegcmrun/engage_solver.py` maps GAMERA grid types to TIEGCM resolutions for coupled ("engage") runs.*
3. ***GLOW*** *(`https://doi.org/10.5281/zenodo.3344536`; repository `https://github.com/space-physics/NCAR-GLOW`). The GLOW airglow/auroral emission model consumes TIEGCM history files directly: that repository contains `src/ncarglow/fortran/readtgcm.f90` (subroutines `read_tgcm`, `read_tgcm_coords`, `find_mtimes`) and the driver namelist `fortran/in.namelist.tgcm`, and its `glowdriver.f90` documents "For definitions of TGCM input variables see module READTGCM". The exchange object is again the TIEGCM netCDF history file.*
4. ***The CCMC Kamodo Analysis Suite*** *(`https://github.com/nasa/Kamodo`; no DOI stored). Kamodo ships a dedicated TIEGCM reader -- `kamodo_ccmc/readers/tiegcm_4D.py` and `kamodo_ccmc/readers/tiegcm_tocdf.py` -- which ingests TIEGCM output into Kamodo's functionalized data model for interpolation, satellite flythrough and model-data comparison.*

*Considered and EXCLUDED: **Kaipy** -- plausible by association as the Python toolkit for Kaiju/MAGE, but its repository tree contains **no** TIEGCM-related path, so there is no demonstrated exchange with TIEGCM specifically; the coupling evidence points at Kaiju/REMIX, which is recorded above. **CESM / WACCM-X** -- see Field 29. **xarray / netCDF4 / numpy / MPI / ESMF** -- dependencies, not peer tools; ESMF is recorded in Field 29 for a different reason. No entry here rests on "part of the scientific Python ecosystem" or "shares a runtime".*

*Negative research on HIDRA and RCM: `src/mpi.F:34` registers application IDs for TIEGCM, GAMERA, HIDRA, REMIX, VOLTRON, and RCM, but neither HIDRA nor RCM clears the Field 30 gate:*
- ***RCM*** *-- every call site resolves to the literal, unimplemented string "T not coupling to RCM yet": four occurrences in `src/mage_coupling.F` (lines 100, 399, 444, 475) are Fortran comments (`!write(*,*)...`), and the one live (non-commented) call site, `src/mpi.F:309`, executes but prints exactly that message. The code itself documents that no exchange exists yet. Fails "demonstrated exchange" outright.*
- ***HIDRA*** *-- unlike RCM, this shows genuine, currently active, non-commented MPI coupling-rank assignment in the same `select case` block in `src/mpi.F` (`case (hidraId)`/`hidraNId`/`hidraSId` -> `hidraCplRank = i-1`/`hidraNCplRank = i-1`/`hidraSCplRank = i-1`, printing "T coupling to hidra"/"hidraN"/"hidraS"), plus a user-facing `--hidra`/`-hi` CLI flag in `tiegcmrun/tiegcmrun.py` ("Enable HIDRA"), a `HIDRA=$hidra` run parameter (help text "Whether to couple with HIDRA via MPI") in five PBS job scripts (`scripts/tiegcm-de-bash.job`, `tiegcm-de-tcsh.job`, `tiegcm-pf-tcsh.job`, `tiegcm-linux.job`, `tiegcm-palmetto.job`), and a `-DHIDRA` build flag in `scripts/Makefile`. This is real, currently-implemented, user-facing coupling functionality -- not dead code. However, a web search and a scan of the HSSI software catalogue turned up **no independently identifiable software called "HIDRA"**: no DOI, no code repository, no publication, and no HSSI entry describes a model by this name anywhere (published MAGE-architecture literature -- e.g. the JHUAPL/kaiju repository and CCMC's MAGE 1.0 model page -- names only GAMERA, REMIX, RCM and TIEGCM as components, never HIDRA). Field 30 requires a DOI, a code repository, or at minimum a link where users can learn more about the partner software; none exists. Conclusion: TIEGCM's own code strongly indicates it couples to *something* real called HIDRA, but that software's external identity cannot be resolved from any public source, so no citable, submittable Field 30 entry can be constructed responsibly. **This lead is now closed, not carried into the field.** If a future release publishes a HIDRA repository or DOI, this should be revisited.*

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** Sounding of the Atmosphere using Broadband Emission Radiometry
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/TIMED/SABER
- **Instrument Name:** TIMED Doppler Interferometer
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/TIMED/TIDI
- **Instrument Name:** Solar EUV Experiment
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/TIMED/SEE

*All three names are copied verbatim from their controlled-vocabulary rows and paired with SPASE identifiers.*

*Relevance-gate justification -- these are **not** incidental mentions; TIEGCM contains purpose-built, instrument-specific ingest for each, exposed as documented namelist inputs:*
- ***SABER and TIDI*** *-- `src/saber_tidi.F` is a module whose stated purpose is "Read and import netcdf files containing SABER (T,Z) and TIDI (U,V) data"; it reads the files at initialization, interpolates them to model time every timestep (`get_saber_tidi`, called once per step from `advance`) and applies them as lower-boundary conditions. Exposed as `SABER_NCFILE` ("SABER data file (T,Z lower boundary condition)") and `TIDI_NCFILE` ("TIDI data file (U,V lower boundary condition)") in `doc/userguide/namelist.rst` and in `tiegcmrun/options_description.json` ("Data File for Tidal Perturbation of T, Z from SABER" / "... U, V from TIDI"), and validated as mutually exclusive with the GSWM/CTMT/Hough tidal options in `src/input.F`.*
- ***SEE*** *-- `src/soldata.F` reads a measured solar EUV spectral-irradiance file and, when present, uses it in place of the F10.7-proxy parameterization for photoionization and heating (`src/qrj.F` selects `soldata` over `f107` when `see_ncfile` is set; `src/init.F` calls `rd_soldata`). The instrument identity is explicit in the code rather than inferred: the history-file attribute is written as "TIMED SEE data file" (`src/nchist.F:1787-1789`).*

*Both sanity checks pass: a user searching HSSI for `instrument:"SABER"`, `"TIDI"` or `"SEE"` and wanting to know what consumes those data products should see this model, and a scientist working with those data would plausibly reach for TIEGCM to drive or interpret them. Judgment call recorded: TIEGCM is fundamentally an instrument-agnostic first-principles model, so these three entries rest specifically on the existence of dedicated instrument-specific readers, not on general-purpose modelling. The stricter reading -- that a GCM should list no instruments at all -- was considered and rejected by decision.*

*Resolution details: `SABER` and `TIDI` each have one exact row. `SEE` has two identically named rows; the `SMWG/...` row is chosen over the CDPP-AMDA mirror as the same-name tie-breaker.*

*Considered and EXCLUDED: **GUVI** (`SMWG/Instrument/TIMED/GUVI`) -- appears only as a comparison target for tuning the auroral-oval parameterization ("produce realistic oval compared to NOAA empirical auroral oval and TIMED/GUVI", `src/aurora.F:247,262`, `src/util.F:1316`); no GUVI data is read. **WINDII** and **HRDI** -- named only as the provenance of a pre-computed zonal-mean climatology file (`src/bgrd_data.F`: "Read background based on SABER,WINDII/HRDI at lower boundary...", file `saber_lbcs_tngph_windiihrdi_unvn_notides.nc`); the module parses a generic background-field file, not an instrument-specific format, and neither instrument has an available SPASE vocabulary value. **DMSP/NOAA** -- mentioned only inside a comment comparing polar-cap potential offsets in `src/wei05sc.F`.*

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Thermosphere-Ionosphere-Mesosphere Energetics and Dynamics
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/TIMED

*The name is copied verbatim from the matched observatory row and paired with its SPASE identifier.*

*Justification: this is not a fallback for an unresolvable instrument -- all three instruments in Field 31 resolved cleanly -- but a genuine platform-level relationship. The software reads data from **three separate instruments on the same spacecraft** (SABER, TIDI and SEE, per Field 31), which is a mission-level dependency rather than the expansion of a single instrument example. Cross-listed with `Observatory/Mission-specific` in Field 17 exactly as Field 17's guidance requires.*

*Resolution details: the SMWG TIMED row and a CDPP-AMDA mirror normalize to the same name. The SMWG row is used as the same-name tie-breaker.*

*Considered and EXCLUDED: **UARS** (`SMWG/Observatory/UARS`) -- appears only as the provenance of the pre-computed lower-boundary climatology ("empirical models, and UARS data", `doc/release/release_notes.rst:59`; `doc/userguide/namelist.rst:166`), the same weak provenance evidence that excluded WINDII and HRDI. **Derecho / Pleiades / Aitken / Electra / Palmetto** -- HPC systems, not observatories (recorded in Fields 20/21). No generic multi-mission archive is listed here; the OMNI/CDAWeb provenance is discussed under Field 17.*

### 33. Logo (OPTIONAL)
Not found -- the repository contains no logo image, `doc/userguide/conf.py` and `doc/release/conf.py` both leave `html_logo` commented out, the ReadTheDocs site displays no project logo, SoMEF extracted no `logo`, and TIEGCM is absent from the PyHC registries (a common source of curated logo URLs).

*Checked and rejected as substitutes: the diagnostic figures under `doc/userguide/_static/images/diags/` (documentation plots, not a logo) and the generic HAO banner image used by an unrelated PyHC entry.*
