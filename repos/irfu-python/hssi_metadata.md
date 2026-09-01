# HSSI Metadata Extraction Results

**HSSI Software ID:** bdd706f0-b987-446b-b650-78d9d86f00b2
**Repository:** https://github.com/louis-richard/irfu-python
**Source Revision:** 40505b6a6e69c6c6ade8ff57062fbb21f23734b8
**Extraction Date:** 2026-07-26
**Validation Date:** 2026-08-26
**Validation Status:** PASS

**Source revision context:** `master` HEAD `40505b6a6e69c6c6ade8ff57062fbb21f23734b8` (2026-02-27, "Bump version 2.4.20 -> 2.4.21") is also the `v2.4.21` tag commit; verified against `GET https://api.github.com/repos/louis-richard/irfu-python/branches/master`. (`pushed_at` on the repo is later only because of the unreleased `devel` branch.)

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]
- **Note:** Submitter information is not available in the repository or public metadata sources, so the required placeholder is retained.

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.10678694
- **Note:** Zenodo **concept** DOI for all versions, confirmed by DataCite and the prior canonical record.

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/louis-richard/irfu-python
- **Note:** Matches `pyproject.toml [project.urls] source`, `CITATION.cff repository-code`, Zenodo `code:codeRepository`, and the PyHC registry `code` field.

### 4. Software Functionality (MANDATORY)

**Value:**

- Coordinate Transforms
- Coordinate Transforms:Magnetospheric
- Coordinate Transforms:Mission-Specific
- Data Processing and Analysis
- Data Processing and Analysis:2D Slices
- Data Processing and Analysis:3D Particle Distribution Processing
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Curlometer
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:Linear Gradient Estimation
- Data Processing and Analysis:Pitch Angle Distributions
- Data Processing and Analysis:Plasma Moments
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Spectrogram
- Data Processing and Analysis:Time Series Analysis
- Data Processing and Analysis:Wave Polarization Analysis
- Data Processing and Analysis:Wavelet Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:2D Slices
- Data Visualization:3D Graphics
- Data Visualization:Hodograms
- Data Visualization:Line Plots
- Data Visualization:Orbit Plots
- Data Visualization:Spacecraft Formation Plots
- Data Visualization:Spectrogram
- Mission-related
- Mission-related:Analysis
- Mission-related:Calibration
- Mission-related:Distribution/Access
- Models and Simulations
- Models and Simulations:Empirical
- Models and Simulations:Field-line Tracing
- Models and Simulations:Instrument Response
- Models and Simulations:Physics-Based
- Models and Simulations:Theory

**Formatting note:** The `Parent:Child` values use the older no-space form. It is semantically identical to the canonical `Parent: Child` form because HSSI strips surrounding whitespace around the colon.

**`Data Processing and Analysis:Wavelet Analysis`.** The evidence for this value is unambiguous: `pyrfu/pyrf/wavelet.py` implements a continuous wavelet transform (Morlet), `pyrfu/pyrf/compress_cwt.py` compresses CWT output, and `pyrfu/pyrf/ebsp.py` performs wavelet-based E/B spectral analysis — all three are exported in `pyrfu/pyrf/__init__.py` `__all__`.

The following values have specific code evidence at revision `40505b6a`:

| Value | Evidence (revision 40505b6a) |
|---|---|
| `Data Processing and Analysis:2D Slices` | `pyrfu/mms/vdf_projection.py` ("Compute the projection of the velocity distribution onto a specified plane"), `pyrfu/mms/reduce.py` ("Reduces (integrates) 3D distribution to 1D (line) or 2D (plane)"), `pyrfu/mms/vdf_reduce.py` |
| `Data Processing and Analysis:Data Reduction` | `pyrfu/mms/reduce.py`, `pyrfu/mms/psd_rebin.py`, `pyrfu/mms/eis_spin_avg.py`, `pyrfu/mms/feeps_spin_avg.py`, `pyrfu/mms/hpca_spin_sum.py`, `pyrfu/pyrf/mean_bins.py`, `pyrfu/pyrf/median_bins.py`, `pyrfu/pyrf/waverage.py`, `pyrfu/pyrf/movmean.py` |
| `Data Visualization:2D Slices` | `pyrfu/plot/plot_projection.py`, `pyrfu/plot/plot_reduced_2d.py` (both exported in `pyrfu/plot/__init__.py`) |
| `Data Visualization:3D Graphics` | `pyrfu/plot/plot_surf.py` (`axis.plot_surface(...)`), `pyrfu/plot/mms_pl_config.py` (`fig.add_subplot(..., projection="3d")`) |
| `Data Visualization:Hodograms` | `pyrfu/pyrf/mva_gui.py` — interactive minimum-variance GUI whose panels are explicitly "Min/Max hodogram", "Interm/Max hodogram", "B3/B1 hodogram", "B2/B1 hodogram"; exported as `mva_gui` in `pyrfu/pyrf/__init__.py` `__all__` |
| `Data Visualization:Spacecraft Formation Plots` | `pyrfu/plot/mms_pl_config.py` — "Plot spacecraft configuration with three 2d plots of the position in Re and one 3d plot of the relative position of the spacecraft" |
| `Mission-related:Calibration` | MMS-instrument-specific calibration/correction routines: `pyrfu/mms/feeps_flat_field_corrections.py`, `feeps_correct_energies.py`, `feeps_remove_sun.py`, `feeps_remove_sunlit_sectors.py`, `feeps_remove_bad_data.py`, `eis_proton_correction.py`, `correct_edp_probe_timing.py`, `remove_edist_background.py`, `remove_idist_background.py`, `remove_imoms_background.py` |
| `Models and Simulations` (parent) | Required parent for the four children below |
| `Models and Simulations:Empirical` | `pyrfu/models/igrf.py` (IGRF-13 empirical geomagnetic field, coefficients in `igrf13coeffs.csv`), `pyrfu/pyrf/magnetosphere.py` (Shue+1998 magnetopause and bow-shock models), `pyrfu/models/magnetopause_normal.py`, `pyrfu/models/ion_anisotropy_thresh.py` |
| `Models and Simulations:Field-line Tracing` | `pyrfu/plot/plot_magnetosphere.py` calls `geopack.trace(...)` twice to trace model field lines (`_add_field_lines`) |
| `Models and Simulations:Instrument Response` | `pyrfu/lp/` — `LangmuirProbe` class plus `photo_current.py` (per-surface-material photoemission current densities) and `thermal_current.py` model Langmuir-probe/spacecraft-potential instrument response; `pyrfu/mms/make_model_vdf.py`, `make_model_kappa.py` synthesize instrument-frame model distributions |
| `Models and Simulations:Physics-Based` | `pyrfu/dispersion/one_fluid_dispersion.py`, `pyrfu/mms/make_model_kappa.py`, `pyrfu/mms/make_model_vdf.py`, `pyrfu/lp/thermal_current.py` |
| `Models and Simulations:Theory` | `pyrfu/dispersion/disp_surf_calc.py` + `one_fluid_dispersion.py` (analytic plasma dispersion-relation solvers; `docs/examples/02_dispersion/`); corroborated by the PyHC registry keyword `theory` |

**Note (considered and rejected):** `Data Processing and Analysis:File Format Conversion` — `psd2def`/`psd2dpf`/`def2psd`/`dpf2psd` convert particle *units*, not file formats. `Data Processing and Analysis:Image Processing`, `:ML/AI`, `:Packet Decommutation`, `:Data Assimilation`, `:Magnetic Null Finding`, `:Field-line Tracing` — no implementation found. `Data Visualization:Movies`/`:Web-Based` — no `matplotlib.animation`, `plotly` or `bokeh` usage. `Servers and Environments*` — no container, server, or HPC/MPI code in the repository. `Coordinate Transforms:Heliospheric`/`:Planetary`/`:Solar` — `pyrfu/pyrf/cotrans.py` supports only geocentric systems (`geo/gei/gse/gsm/sm/mag` plus `dipoledirectiongse`); the Solar Orbiter and MAVEN modules perform no coordinate transforms.

### 5. Related Region (MANDATORY)
- **Earth Magnetosphere**
- **Interplanetary Space**
- **Planetary Magnetospheres**
- **Mars Magnetosphere**
- **Solar Wind**
- **Earth Outer Magnetosphere**

**Note:** Earth Magnetosphere is supported by the whole `pyrfu/mms/` package (91 modules) plus `pyrf/magnetosphere.py`, `models/magnetopause_normal.py`, `models/igrf.py`, and `pyrf/l_shell.py`; Interplanetary Space is supported by `pyrf/get_omni_data.py` (solar-wind/IMF), `pyrf/shock_normal.py`, `shock_parameters.py`, `docs/examples/01_mms/example_mms_ipshocks.ipynb`, `example_mms_walen_test.ipynb`, and `pyrfu/solo/` (Solar Orbiter RPW in the inner heliosphere); Planetary Magnetospheres is supported by `pyrfu/maven/` (Mars). `Mars Magnetosphere` is supported by the first-class MAVEN Science Data Center client and its MAVEN instrument catalogue at `pyrfu/maven/download_data.py:114-132`. `Solar Wind` is supported by the OMNI solar-wind and IMF retrieval implemented at `pyrfu/pyrf/get_omni_data.py:127-137,140-167`. `Earth Outer Magnetosphere` is supported by the exported magnetopause-location routine at `pyrfu/pyrf/magnetosphere.py:29-36` and the spacecraft inside/outside magnetopause calculation at `pyrfu/models/magnetopause_normal.py:55-82`. `Solar Environment` and `Earth Atmosphere` are deliberately not selected: nothing in the package works with solar-disk/coronal or neutral-atmosphere data.

### 6. Authors (MANDATORY)

Six person authors are matched by ORCID across the prior canonical file, `CITATION.cff`, DataCite and Zenodo. Affiliations are reconciled by ROR.

#### Author 1
- **Name:** Louis Richard
- **Author Identifier:** https://orcid.org/0000-0003-3446-7322
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11
- **Affiliation:**
  - **Organization:** Uppsala University
  - **Affiliation Identifier:** https://ror.org/048a87296

#### Author 2
- **Name:** Yuri V. Khotyaintsev
- **Author Identifier:** https://orcid.org/0000-0001-5550-3113
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11

#### Author 3
- **Name:** Andris Vaivads
- **Author Identifier:** https://orcid.org/0000-0003-1654-841X
- **Affiliation:**
  - **Organization:** KTH Royal Institute of Technology
  - **Affiliation Identifier:** https://ror.org/026vcq606
- **Affiliation:**
  - **Organization:** Ventspils University of Applied Sciences
  - **Affiliation Identifier:** https://ror.org/03sc6wx59

#### Author 4
- **Name:** Daniel B. Graham
- **Author Identifier:** https://orcid.org/0000-0002-1046-746X
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11

#### Author 5
- **Name:** Cecilia Norgren
- **Author Identifier:** https://orcid.org/0000-0002-6561-2337
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11

#### Author 6
- **Name:** Andreas Johlander
- **Author Identifier:** https://orcid.org/0000-0001-7714-1870
- **Affiliation:**
  - **Organization:** Swedish Defence Research Agency
  - **Affiliation Identifier:** https://ror.org/0470cgs30

**Considered and not selected:** `CITATION.cff` at revision `40505b6a` lists a seventh, organization-style author as its first entry: a bare `- name: "PyRFU team"` with no `given-names` or `family-names`. It is absent from the prior canonical file and from both the DataCite and Zenodo creator lists, which contain only the six people. A ROR lookup finds no institution because "PyRFU team" is a project team, not a registered organization. By user decision on 2026-07-27, it is not included without maintainer confirmation and a durable organization identity.

**Note (author-name provenance):** The display forms above match the prior canonical file and DataCite exactly. `CITATION.cff` uses the shorter given names "Yuri" and "Daniel"; DataCite and Zenodo use "Yuri V." and "Daniel B.", so the fuller forms are kept.

### 7. Software Name (MANDATORY)
- **Value:** PyRFU
- **Note:** The prior canonical file said `Python RymdFysik Utilities (PyRFU)`, but that is the DataCite/Zenodo record title rather than the name the software goes by. Repository evidence supports the short form: `pyproject.toml name = "pyrfu"`, `CITATION.cff title: "pyrfu"`, the README heading `pyRFU`, and the PyHC registry entry `name: PyRFU`. The shorter `PyRFU` is therefore used.

### 8. Description (MANDATORY)
**Value:**
PyRFU is a free and open-source Python package for advanced analysis of in-situ space plasma data. It provides routines to work with space data, particularly with Magnetospheric Multiscale (MMS) mission data, as well as MAVEN and Solar Orbiter missions. The package includes general plasma physics routines for coordinate transformations, particle distribution analysis, plasma moments calculations, wave analysis (including polarization and wavelets), multi-spacecraft techniques (curlometer, gradient estimation), and comprehensive data visualization capabilities. PyRFU is based on the IRFU-MATLAB library and supports data retrieval from multiple sources including local files, MMS Science Data Center, MAVEN Science Data Center, and cloud storage (AWS S3). The package additionally provides analytic plasma dispersion-relation solvers, Langmuir-probe and spacecraft-potential current models, and empirical field and boundary models including IGRF-13 and the Shue et al. (1998) magnetopause and bow shock.

- **Note:** The established description is retained, with a final sentence approved on 2026-07-27 to cover three substantial subpackages that the earlier wording omitted.
- **Evidence for the appended sentence:** it covers three of PyRFU's six subpackages that the original text omitted entirely. Dispersion-relation solvers — `pyrfu/dispersion/one_fluid_dispersion.py` and `disp_surf_calc.py` (`optimize.fsolve` on analytic dispersion relations), with two example notebooks in `docs/examples/02_dispersion/`. Langmuir-probe / spacecraft-potential current models — `pyrfu/lp/` (`LangmuirProbe` class, `photo_current.py`, `thermal_current.py`, all exported in `pyrfu/lp/__init__.py` `__all__`), plus `pyrfu/mms/scpot2ne.py`. Empirical field and boundary models — `pyrfu/models/igrf.py` (IGRF-13, coefficients in `igrf13coeffs.csv`), `pyrfu/pyrf/magnetosphere.py` (`model="mp_shue1998"` and bow shock), `pyrfu/models/magnetopause_normal.py`.

### 9. Concise Description (OPTIONAL)
- **Value:** PyRFU is a free and open-source Python package for advanced analysis of in-situ space plasma data.
- **Length:** 98 characters (within the 200-character limit)
- **Note:** This is the exact `description` string in the PyHC community registry. The prior canonical file had a different, longer 197-character sentence; that stylistic alternative is not used because the curated PyHC wording is authoritative and already concise.

### 10. Publication Date (RECOMMENDED)
- **Value:** 2020-11-27
- **Note:** By user decision on 2026-07-27, this uses PyRFU's genuine first public release date: PyPI `pyrfu` 1.8.3 was uploaded on 2020-11-27. The prior value `2024-02-19` is the DataCite issue date for the later Zenodo deposit of v2.4.12, not the software's first publication. `LICENSE.txt` also reads "Copyright (c) 2020" and `pyrfu/__init__.py` reads `Copyright 2020-2026`.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Note:** DataCite identifies the publisher as Zenodo. The prior canonical file used the ROR `https://ror.org/04t3en479`, but Field 11 permits the publisher URL and names `https://zenodo.org` as its Zenodo example, so that canonical URL is used.

### 12. Version (RECOMMENDED)

#### Version Number
- **Value:** v2.4.21
- **Note:** This supersedes the stale v2.4.12 value. `pyproject.toml` at revision `40505b6a` has `version = "2.4.21"`; tag `v2.4.21` points at that default-branch revision; and PyPI and the GitHub release both identify v2.4.21 as released on 2026-02-27.

#### Version Date
- **Value:** 2026-02-27
- **Note:** This supersedes the prior v2.4.12 date. The `v2.4.21` tag, commit, GitHub release, and PyPI upload all date the release to 2026-02-27.

#### Version Description
- **Value:** Version 2.4.21 adds new features and bug fixes across the generic and MMS subpackages. New features: `pyrfu.pyrf.filt` now supports tensors; `pyrfu.pyrf.pid_4sc` adds error propagation; `pyrfu.mms.tokenize` adds keys for loading FPI-DIS moment errors and FPI-DES temperature errors; and `pyrfu.mms.fk_power_spectrum_4sc` now also returns the mean and standard deviation of the wave vector and frequency. Bug fixes: `pyrfu.pyrf.calc_dt` corrects time-precision handling, and `pyrfu.pyrf.int_sph_dist` corrects index handling at bin edges.
- **Note:** This supersedes the prior v2.4.12 description and is composed from the official v2.4.21 GitHub release notes, cross-checked against the commits in `git log v2.4.20..v2.4.21`.

#### Version PID
- **Value:** Not found
- **Note:** The prior canonical file's `https://doi.org/10.5281/zenodo.10678695` belongs to v2.4.12 and must not be used as the PID of v2.4.21. DataCite and Zenodo both identify that DOI as version 2.4.12, published 2024-02-19. Zenodo archiving stopped at v2.4.12, so no version-specific DOI exists for v2.4.21. `CITATION.cff` and the README badge still point at the old deposit; re-enabling the GitHub–Zenodo integration would restore current version DOIs.

### 13. Programming Language (RECOMMENDED)
- **Value:** Python 3.x
- **Note:** The supported minor versions are 3.10–3.14 (`pyproject.toml requires-python = ">=3.10,<3.15"` and classifiers `Programming Language :: Python :: 3.10` through `3.14`, plus `3 :: Only`). This supersedes the prior canonical file's narrower 3.10–3.12 note; v2.4.18 added Python 3.13 and 3.14 compatibility.

### 14. Reference Publication (RECOMMENDED)
- **Value:** Not found
- **Note:** No paper describing PyRFU was found. The concept DOI has no `IsDescribedBy` or `IsSupplementTo` publication, `CITATION.cff` has no `preferred-citation`, and the README asks users to cite the repository URL rather than a paper.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT
- **Note:** Four independent sources agree: `LICENSE.txt` begins "MIT License / Copyright (c) 2020 L. RICHARD"; DataCite identifies the MIT License and URI; `pyproject.toml` uses the license file and the MIT classifier; and the README states that PyRFU is distributed under the open-source MIT license.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Value:** The terms use the vocabulary's stored form; `Langmuir probes` carries a capital L.

**User-selected terms (2026-07-27), each repo-evidenced:** `Langmuir probes` (the `pyrfu/lp/` subpackage), `igrf13` (`pyrfu/models/igrf.py` and `igrf13coeffs.csv`), `shue` (`pyrfu/pyrf/magnetosphere.py`), `l shell` (`pyrfu/pyrf/l_shell.py`), `istp` (the ISTP attribute dependence documented in Field 18), and `energetic particles` (EIS and FEEPS modules).

**Considered and not selected:** `magnetic reconnection` and `turbulence` are strongly evidenced but are not available vocabulary values, and expanding the vocabulary for this record was declined by user decision on 2026-07-27.

- calibration
- cdf
- coordinate transformations
- coordinates
- data access
- data analysis
- data retrieval
- data visualization
- energetic particles
- heliosphere
- igrf13
- in situ measurements
- instrumentation
- istp
- l shell
- Langmuir probes
- line plots
- magnetosphere
- maven
- mms
- multidimensional
- omni
- orbit
- pitch angle distributions
- planetary
- plasma parameters
- plasma physics
- plotting
- power spectra
- python 3
- shock waves
- shue
- solar orbiter
- solar wind
- space physics
- space plasma
- spectra
- spectrograms
- theory
- time
- time series
- velocity distribution functions
- wave polarization
- wavelet analysis

**Established terms:**
coordinates · data access · data retrieval · heliosphere · instrumentation · line plots · magnetosphere · maven · mms · multidimensional · omni · orbit · planetary · plasma physics · plotting · power spectra · python 3 · solar orbiter · space physics · spectra · theory · time

*(Origin: the PyHC registry keyword list for PyRFU — `heliosphere, magnetosphere, planetary, plasma_physics, coordinates, data_retrieval, line_plots, multidimensional, orbit, plotting, power_spectra, spectra, time, general, local, remote, web_service, data_access, data_analysis, instrumentation, theory, maven, mms, omni, solo` — plus the GitHub topics `python3`, `space-physics`.)*

**Additional repo-evidenced terms:**

| Keyword | Evidence |
|---|---|
| in situ measurements | README/PyHC/description core framing: "advanced analysis of **in-situ** space plasma data" |
| space plasma | Same; `Topic :: Scientific/Engineering :: Physics` classifier; whole package scope |
| solar wind | `pyrfu/pyrf/get_omni_data.py` (OMNI solar-wind/IMF retrieval), `shock_normal.py`, `shock_parameters.py`, `docs/examples/01_mms/example_mms_ipshocks.ipynb`, `example_mms_walen_test.ipynb` |
| cdf | Primary input format; `pyrfu/pyrf/read_cdf.py`, `pyrfu/mms/get_ts.py`, `get_dist.py`, `get_variable.py` (pycdfpp), `pyrfu/pyrf/cdfepoch2datetime64.py` (cdflib) |
| calibration | `pyrfu/mms/feeps_flat_field_corrections.py`, `feeps_correct_energies.py`, `eis_proton_correction.py`, `correct_edp_probe_timing.py`, `remove_edist_background.py` |
| coordinate transformations | `pyrfu/pyrf/cotrans.py`, `gse2gsm.py`, `convert_fac.py`, `new_xyz.py`, `eb_nrf.py`, `pyrfu/mms/dsl2gse.py`, `dsl2gsm.py` |
| wavelet analysis | `pyrfu/pyrf/wavelet.py`, `compress_cwt.py`, `ebsp.py` |
| wave polarization | `pyrfu/pyrf/wavepolarize_means.py`, `ebsp.py`, `docs/examples/01_mms/example_mms_polarizationanalysis.ipynb` |
| pitch angle distributions | `pyrfu/mms/get_pitch_angle_dist.py`, `feeps_pad.py`, `feeps_pad_spinavg.py`, `eis_pad.py`, `hpca_pad.py`, `docs/examples/01_mms/example_mms_particle_pad.ipynb` |
| velocity distribution functions | `pyrfu/mms/vdf_omni.py`, `vdf_projection.py`, `vdf_reduce.py`, `vdf_elim.py`, `vdf_to_e64.py`, `make_model_vdf.py`, `pyrfu/pyrf/ts_skymap.py`, `average_vdf.py` |
| shock waves | `pyrfu/pyrf/shock_normal.py`, `shock_parameters.py`, `shock_models_parameters.json`, `pyrfu/pyrf/magnetosphere.py` (bow shock), `example_mms_ipshocks.ipynb` |
| time series | `pyrfu/pyrf/ts_scalar.py`, `ts_vec_xyz.py`, `ts_tensor_xyz.py`, `ts_spectr.py`, `ts_append.py`, `resample.py`, `filt.py`, `time_clip.py`, `autocorr.py` |
| plasma parameters | `pyrfu/pyrf/plasma_calc.py`, `iplasma_calc.py`, `plasma_beta.py`, `pres_anis.py`, `dynamic_press.py` |
| spectrograms | `pyrfu/plot/plot_spectr.py`, `pyrfu/pyrf/ts_spectr.py`, `wave_fft.py`, `psd.py`, `pyrfu/mms/spectr_to_dataset.py`, `feeps_sector_spec.py`, `eis_omni.py` |
| data visualization | Entire `pyrfu/plot/` subpackage (21 modules, 22 exported names) |

**Considered and not selected by user decision on 2026-07-27 because they were not existing vocabulary rows:**
- `magnetic reconnection` — strongly evidenced: `docs/examples/01_mms/example_mms_edr_signatures.ipynb` (electron diffusion region), `example_mms_walen_test.ipynb`, `pyrfu/pyrf/match_phibe_dir.py`, `match_phibe_v.py`, `pyrfu/mms/calculate_epsilon.py`, `docs/examples/01_mms/example_mms_ohmslaw.ipynb`
- `turbulence` — evidenced: `pyrfu/pyrf/pvi.py`, `pvi_4sc.py` (partial variance of increments), `struct_func.py`, `increments.py`

**`data analysis`:** PyHC lists `data_analysis`, `general`, `local`, `remote`, `web_service`, and `solo` for PyRFU. `solo` is covered by `solar orbiter`; `general`, `local`, `remote`, and `web_service` are infrastructure tags rather than science keywords. `data analysis` is supported by the curated PyHC registry and the prior canonical file and is therefore included.

### 17. Data Sources (OPTIONAL)
- **HTTP/HTTPS Directories**
- **Observatory/Mission-specific**
- **OMNIWeb**
- **S3/Cloud-aware**

**Evidence:**
- **OMNIWeb** — `pyrfu/pyrf/get_omni_data.py` builds `https://omniweb.gsfc.nasa.gov/cgi/nx1.cgi?activity=retrieve&spacecraft=omni2|omni_min…` and reads the response with `urllib.request.urlopen`.
- **Observatory/Mission-specific** — MMS Science Data Center (`pyrfu/mms/list_files_sdc.py`, `download_data.py`, `download_ancillary.py`, `list_files_ancillary_sdc.py`) and MAVEN SDC (`pyrfu/maven/download_data.py`, `LASP_PUBL = "https://lasp.colorado.edu/maven/sdc/public/files/api/v1/"`). Per Field 17's instruction, the corresponding missions are cross-listed in Field 32.
- **S3/Cloud-aware** — `pyrfu/mms/list_files_aws.py` uses `boto3.resource("s3")` with a configurable bucket/prefix (`pyrfu/mms/config.json` `"aws"` key); `boto3>=1.35.0` and `botocore>=1.35.0` are hard dependencies; `mms.get_data(..., source="aws")`.
- **HTTP/HTTPS Directories** — the SDC/OMNIWeb retrievals above plus `pyrfu/mms/load_brst_segments.py`, which fetches over plain **HTTP** at `http://www.spedas.org/mms/mms_brst_intervals.sav`.

**Considered and rejected:** `CDAWeb`, `HAPI`, `das2`, `SSCWeb`, `TAP`, `VirES`, `The Virtual Solar Observatory`, `FTP/FTPS Directories` — no client code for any of these. Solar Orbiter data are read from a **local** directory tree only (`pyrfu/solo/db_init.py`, `config.json` `local_data_dir`), with no remote fetch, so Solar Orbiter adds no new data-source value.

### 18. Input File Formats (RECOMMENDED)
- **CDF**
- **IDL.sav**
- **ISTP-Compliant**
- **ascii**

**`IDL.sav`:** An earlier rationale wrongly rejected this format on the claim that `scipy.io.readsav` is not a dependency. `pyrfu/mms/load_brst_segments.py` imports and calls `readsav` on the externally hosted MMS burst-segment IDL SAVE file, and `load_brst_segments` is a public exported function. The corrected value is therefore retained.

**Other evidence:** `CDF` is the primary format used by `pyrfu/pyrf/read_cdf.py`, the MMS readers, and the Solar Orbiter readers. The other values are supported as follows:
- **ISTP-Compliant** — `pyrfu/mms/get_ts.py` reads and depends on ISTP metadata attributes: `file[cdf_name].attributes["DEPEND_0"]`, an assertion that `"DEPEND_0" in var_attrs and "epoch" in var_attrs["DEPEND_0"].lower()`, plus handling of `DEPEND_1`/`REPRESENTATION_1`; `pyrfu/mms/eis_ang_ang.py` writes `FILLVAL`, `VALIDMIN` ISTP attributes. The package relies on the ISTP convention, not merely on raw CDF.
- **ascii** — `pyrfu/pyrf/get_omni_data.py` parses the plain-text OMNIWeb response; `pyrfu/mms/load_ancillary.py` reads whitespace-delimited MMS ancillary (ephemeris/attitude) products with `pd.read_csv(file, sep=r"\s+", header=None, skiprows=…)` driven by `pyrfu/mms/ancillary.json` column definitions.
- **`csv` — considered and rejected by user decision on 2026-07-27.** The `pd.read_csv` paths read only tables bundled inside the package, not user-supplied science data. That is the same internal-lookup-table category used to reject `JSON`. `ascii` is different because it covers external OMNIWeb responses and downloaded MMS ancillary products.

**Considered and rejected:** `JSON` — JSON is read only for package-internal configuration/lookup tables (`pyrfu/{mms,maven,solo}/config.json`, `ancillary.json`, `mms_keys.json`, `feeps_bad_data.json`, `shock_models_parameters.json`) and for the MAVEN SDC's file-listing API response, never as a science-data input format (but see the `csv` inconsistency above). `HDF5`, `netCDF3/4`, `FITS`, `Zarr` — no reader present (`h5py`, `netCDF4`, `astropy` are not dependencies). **Correction:** an earlier version of this note also rejected `IDL.sav` on the false claim that `scipy.io.readsav` is absent; it is present and used, and `IDL.sav` is now listed as a value above.

### 19. Output File Formats (RECOMMENDED)
- *(none)*

**Rationale:** `CDF` was removed by user decision on 2026-07-27 because the package has no CDF-writing API.

**Evidence for the removal:** A full search of the package found **no CDF-writing API** (no `cdfwrite`/`CDFWriter`/`pycdfpp` write calls, no `to_netcdf`, `to_csv`, `to_json`, `to_zarr`, `to_hdf`, `np.save`, or `savemat` anywhere in `pyrfu/`). Every `pycdfpp` call is `pycdfpp.load`, and `cdflib` is imported only for `cdfepoch` time conversion. The only files the package writes are downloaded mission CDFs copied into the local data store (`pyrfu/mms/download_data.py` → `copyfileobj` into a temp file then `copy(ftmp.name, out_file)`; `pyrfu/maven/download_data.py`; `pyrfu/mms/download_ancillary.py`; `pyrfu/mms/load_brst_segments.py`). In-memory results are returned as `xarray` objects, not written to disk. The prior canonical file's note ("Software can write CDF files based on the CDF library dependencies") was an inference this evidence does not support. Field 19's instruction is "only formats actually supported should be indicated" for **generated** files; caching a downloaded mission `.cdf` is not generating CDF output.

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Mac**
- **Windows**

**Note:** `pyproject.toml` declares Unix, macOS, and Windows classifiers, and `.github/workflows/tests.yml` tests `macos-latest`, `windows-latest`, and `ubuntu-latest`. `Solaris`, `MobilePlatform`, and `Operating System Independent` are not used because the three concrete platforms are directly supported.

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Note:** This is a pure-Python package; `pyproject.toml` declares no architecture constraint and builds no compiled extensions. `numba` provides architecture-portable JIT acceleration, and there is no CUDA, `mpi4py`, or HPC job-script support.

### 22. Related Phenomena (OPTIONAL)
- **Solar Wind**

**Note:** The prior canonical file said "Not found", but `Solar Wind` is directly supported by `pyrfu/pyrf/get_omni_data.py`, the Shue magnetopause and bow-shock models, the shock-normal and shock-parameter routines, and the interplanetary-shock and Walen-test notebooks.

**Considered and rejected:** the other controlled values. `Coronal Heating`, `Coronal Mass Ejections`, `Solar Corona`, `Solar Flares`, `X-ray emission` — PyRFU is an in-situ plasma package with no solar imaging, coronal, or remote-sensing functionality. (`Coronal Holes` was listed here previously but is **not** a row in the live vocabulary; the `hssi-field-definitions` list is stale on that point.)

**`Geomagnetic Storms` — considered and excluded (decision settled 2026-08-25).** The original rationale claimed there was no storm-index or Dst/Kp handling. That premise was false: `pyrfu/pyrf/get_omni_data.py` maps OMNI columns for `dst`, `ae`, `al`, `au`, `kp`, and `pc`, and the function is publicly exported. The exclusion still stands on the narrower rationale that retrieving an index is not science functionality for storms and the package has no storm-phase, superposed-epoch, or Dst-modelling code. The package's characteristic phenomena of magnetic reconnection, plasma turbulence, and plasma waves or instabilities have no controlled phenomena rows; `magnetic reconnection` and `turbulence` were also considered and declined as newly created Field 16 keywords by user decision on 2026-07-27.

### 23. Development Status (RECOMMENDED)
- **Value:** Active
- **Note:** Zenodo declares the development status `Active`; releases continue through v2.4.21; the repository is not archived; four CI workflows remain active; and PyHC rates software maturity and documentation `Good`. This matches the repostatus.org definition of a stable, usable project under active development.
- **Conflicting signal, deliberately not followed:** `pyproject.toml` still carries the classifier `Development Status :: 2 - Pre-Alpha`, and individual modules carry `__status__ = "Prototype"`. Both are stale boilerplate that contradicts a 100-release PyPI history, an explicit maintainer-set Zenodo status of "active", and PyHC's maturity rating; `Pre-Alpha` also has no HSSI equivalent (the nearest, `WIP`, means "no stable, usable public release yet", which is plainly false here).

### 24. Documentation (RECOMMENDED)
- **Value:** https://pyrfu.readthedocs.io/en/latest/
- **Note:** Four sources agree: `pyproject.toml [project.urls] documentation`, the PyHC registry, README, and SoMEF. The site includes installation instructions corresponding to `docs/installation.rst` and the worked example gallery under `docs/examples/`; `.readthedocs.yaml` is present at the repository root.

### 25. Funder (OPTIONAL)

#### Funder 1
- **Organization:** Swedish National Space Agency
- **Funder Identifier:** https://ror.org/04t512h04

**Note:** DataCite's funding reference names the former "Swedish National Space Board," ROR `04t512h04`, for award 139/18. The ROR record now gives **Swedish National Space Agency** as the official display name and retains the former name only as an alias. By user decision on 2026-07-27, the current official name is used with the unchanged ROR identifier.

### 26. Award Title (OPTIONAL)

#### Award 1
- **Award Title:** Plasma Jet Fronts: Energy Conversion and Particle Acceleration
- **Award Number:** 139/18

**Note:** Award title and number are verbatim from DataCite `fundingReferences` on concept DOI 10.5281/zenodo.10678694.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2021JA029152
- https://doi.org/10.1029/2022JA030430
- https://doi.org/10.1029/2022GL101693
- https://doi.org/10.1103/PhysRevLett.131.115201
- https://doi.org/10.1103/PhysRevLett.132.105201
- https://doi.org/10.1103/PhysRevLett.134.215201

**Note:** The prior canonical file said "Not found," but these six curator-supplied DOIs are supported by Crossref: every paper is first-authored by Louis Richard, PyRFU's principal author, and concerns the package's MMS reconnection and turbulence domain. They do not appear in the repository or concept DOI metadata, so that provenance caveat is retained. Roughly 20 other DOIs in source docstrings are deliberately excluded because they document algorithms implemented by individual functions rather than publications describing, citing, or using PyRFU itself.

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found
- **Note:** The concept DOI has no dataset related identifier. The repository names MMS and Solar Orbiter data products extensively but never cites dataset DOIs or `hpde.io` identifiers, so none is asserted. SPDF NumericalData records would require separate curation rather than being inferred from product names.

### 29. Related Software (OPTIONAL)

**Established entries:**
- **https://doi.org/10.5281/zenodo.1481144** — cdflib. Domain-specific heliophysics dependency (`cdflib>=1.3.0`); PyRFU's public time-conversion API is built on it: `pyrfu/pyrf/cdfepoch2datetime64.py`, `datetime642ttns.py`, `ttns2datetime64.py` all `from cdflib import cdfepoch`, and all three are exported in `pyrfu/pyrf/__init__.py` `__all__`. DataCite confirms the DOI resolves to "MAVENSDC/cdflib" (Software, Zenodo).
- **https://doi.org/10.5281/zenodo.15110786** — geopack. Domain-specific heliophysics dependency (`geopack>=1.0.10`); `pyrfu/plot/plot_magnetosphere.py` imports `from geopack import geopack` and calls `geopack.recalc()` and `geopack.trace()` to draw traced model field lines. DataCite confirms "tsssss/geopack: v1.0.12" (Software, Zenodo).

**Additional entries:**
- **https://doi.org/10.5281/zenodo.11550090** — IRFU-Matlab (Zenodo concept DOI; DataCite title "IRFU-Matlab", `IsSupplementTo https://github.com/irfu/irfu-matlab`, creators Khotyaintsev, Nilsson, Johansson, Vaivads, Graham, Karlsson — overlapping PyRFU's own author list). **This is the single most distinguishing related-software link and it was missing.** PyRFU is explicitly the Python re-implementation of it: `README.rst` says the package is based on the IRFU-MATLAB library, and the established description says the same. Field 29 explicitly covers predecessors.
- **https://doi.org/10.5281/zenodo.6391115** — pycdfpp. Domain-specific heliophysics dependency (`pycdfpp>=0.7.0`) and PyRFU's *primary* CDF reader: `pyrfu/pyrf/read_cdf.py`, the MMS readers, and the Solar Orbiter readers all use `pycdfpp.load`. An earlier rationale claimed no DOI existed and used the repository URL, but the deposit is titled `CDFpp` rather than `pycdfpp`; Zenodo and DataCite confirm this concept DOI, so it supersedes the URL.

**Considered and REJECTED (audit trail).** Generic scientific-Python / infrastructure dependencies, excluded under the Field 29/30 relevance gate because the entry would be equally true of most Python packages and says nothing about PyRFU: `numpy>=2.0,<2.4`, `scipy>=1.14.0`, `pandas>=2.2.3`, `matplotlib>=3.9.0`, `requests>=2.32.0`, `python-dateutil>=2.9.0`, `tqdm>=4.66.0`, `numba>=0.63.0` (JIT compiler — generic infrastructure), `boto3`/`botocore` (AWS SDK — generic I/O plumbing), `keyring`/`keyrings.alt` (credential storage), `setuptools`/`wheel` (packaging), and the optional dev/test/docs extras (`pytest`, `pytest-cov`, `ddt`, `black`, `flake8`, `isort`, `pylint`, `mypy`, `pre-commit`, `sphinx` and its plugins, `nbsphinx`, `numpydoc`, `pydata-sphinx-theme`). Also rejected: `xarray` **here**, because it belongs in Field 30 where the demonstrated data-model exchange is documented (see below); and Cluster/THEMIS/Cassini tooling — those names appear in `pyrfu/lp/photo_current.py` only as spacecraft-surface *material* presets (`surface_materials = ["cluster", "themis", "cassini", "aluminium", …]`) and in `pyrfu/plot/pl_tx.py` only as a color-scheme option, which is not a software relationship.

### 30. Interoperable Software (OPTIONAL)

- **https://doi.org/10.5281/zenodo.598201** — xarray (DataCite: "xarray", Software, Zenodo).
  **Cited evidence of a demonstrated data-model exchange (Tier B bar):** `xarray` is not merely a dependency — `xarray.DataArray`/`xarray.Dataset` *is* PyRFU's documented public interchange format, so a user's PyRFU results are directly consumable by, and constructible from, any other xarray-based tool.
  - Public constructors that **return** xarray objects: `pyrfu.pyrf.ts_scalar`, `ts_vec_xyz`, `ts_tensor_xyz`, `ts_spectr`, `ts_skymap`, `ts_time`, `ts_append` (all in `pyrfu/pyrf/__init__.py` `__all__`).
  - Public readers that **return** xarray objects: `pyrfu.pyrf.read_cdf` (`import xarray as xr`; "Construct xarray DataArray" → returns a dict of `xr.DataArray`), `pyrfu.mms.get_data` (signature annotated `-> Union[DataArray, Dataset]`), `pyrfu.mms.get_ts`, `get_dist`, `get_variable`, `pyrfu.solo.read_tnr`, `read_lfr_density`, `pyrfu.mms.load_ancillary` (`data_frame.to_xarray()`), `pyrfu.mms.spectr_to_dataset`.
  - Public functions that **accept** xarray objects as their documented input type — e.g. `pyrfu/pyrf/cotrans.py` asserts `isinstance(inp, xr.DataArray)`; `pyrfu/mms/reduce.py` and `vdf_projection.py` document `vdf : xarray.Dataset`; `pyrfu/pyrf/wave_fft.py` documents `inp : xarray.DataArray`.
  This is exactly the "public API returns/accepts `xarray.Dataset` as its documented interchange format" case the field definition admits, not "uses xarray internally".

**Considered and REJECTED (audit trail):**
- **cdflib, pycdfpp** — Tier B; they are used to *read* files, which is dependency use rather than a peer-tool exchange. Recorded in Field 29 as domain-specific dependencies instead.
- **IRFU-Matlab** — a predecessor/re-implementation relationship with no data bridge, converter, or shared model between the two codebases (PyRFU cannot read irfu-matlab output and there is no MATLAB interface). Belongs in Field 29, and is listed there.
- **matplotlib** — Tier A, no exceptions. PyRFU's plot functions take a caller-supplied `matplotlib` axis, but "uses matplotlib for all plotting" is the field definition's own worked ❌ example.
- **numpy, scipy, pandas, requests, tqdm, python-dateutil, numba, boto3/botocore, keyring, pytest, setuptools** — Tier A / generic infrastructure by the "equally at home in a web app, a finance model, or a biology pipeline" test.
- **geopack** — a model library PyRFU calls internally for field-line tracing, not a tool a user would combine with PyRFU via a shared data model. Field 29 only.
- **Jupyter** — Tier B; the docs ship notebook examples (`nbsphinx`, `docs/examples/*.ipynb`), but shipping notebooks is not a documented package-to-package exchange.
- **PyHC ecosystem / "standard scientific Python ecosystem" blanket claims** — explicitly never sufficient. PyRFU's PyHC membership is recorded via Field 16 keywords and Field 24, not as an interoperability claim; no PySPEDAS/pytplot/SunPy/SpacePy/HAPI adapter, converter, or import path exists anywhere in `pyrfu/`.
- **The prior canonical file's Field 30 entries** (`xarray`, `matplotlib`, `cdflib`/`pycdfpp`, justified as "based on its design and PyHC membership") are therefore **not** carried over wholesale: only `xarray` survives the gate, and it now carries specific cited evidence instead of an ecosystem claim.

### 31. Related Instruments (OPTIONAL)

**Settled rationale (user decision 2026-07-27):** All four per-spacecraft SPASE rows are used for each of the ten supported MMS instruments, and `MMS ASPOC` is excluded. Each name is copied from its corresponding controlled-vocabulary row.

Rationale for the granularity: PyRFU supports all four MMS observatories equally (`mms_id` ∈ {1,2,3,4} throughout `pyrfu/mms/`, plus the explicit 4-spacecraft routines `c_4_j`, `c_4_grad`, `c_4_k`, `c_4_v`, `avg_4sc`, `pvi_4sc`, `pid_4sc`, `eis_skymap_combine_sc`, `feeps_avg_4sc`, `fk_power_spectrum_4sc`). The SMWG vocabulary has no constellation-level row for these instruments, so recording one spacecraft's identifier would state something false. Accepting all four is the only option that encodes no false claim.

**Known display consequence:** Nine of the ten instruments carry an identical name across all four per-spacecraft rows, so name-only displays repeat entries such as `MMS FEEPS`. This is an upstream vocabulary limitation, not a reason to encode a single arbitrary spacecraft.

- **MMS FIELDS/FGM** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/FGM`
- **MMS FIELDS/FGM** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/FGM`
- **MMS FIELDS/FGM** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/FGM`
- **MMS FIELDS/FGM** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/FGM`
- **MMS FIELDS/SCM** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/SCM`
- **MMS FIELDS/SCM** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/SCM`
- **MMS FIELDS/SCM** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/SCM`
- **MMS FIELDS/SCM** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/SCM`
- **MMS FIELDS/SDP** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/SDP`
- **MMS FIELDS/SDP** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/SDP`
- **MMS FIELDS/SDP** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/SDP`
- **MMS FIELDS/SDP** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/SDP`
- **MMS 1 FIELDS Suite, Axial Double Probe** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/ADP`
- **MMS 2 FIELDS Suite, Axial Double Probe** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/ADP`
- **MMS 3 FIELDS Suite, Axial Double Probe** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/ADP`
- **MMS 4 FIELDS Suite, Axial Double Probe** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/ADP`
- **MMS FPI/DES** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DES`
- **MMS FPI/DES** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DES`
- **MMS FPI/DES** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DES`
- **MMS FPI/DES** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DES`
- **MMS FPI/DIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DIS`
- **MMS FPI/DIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DIS`
- **MMS FPI/DIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DIS`
- **MMS FPI/DIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DIS`
- **MMS HPCA** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/HotPlasmaCompositionAnalyzer`
- **MMS HPCA** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/HotPlasmaCompositionAnalyzer`
- **MMS HPCA** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/HotPlasmaCompositionAnalyzer`
- **MMS HPCA** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/HotPlasmaCompositionAnalyzer`
- **MMS EIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/EnergeticParticleDetector/EIS`
- **MMS EIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/EnergeticParticleDetector/EIS`
- **MMS EIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/EnergeticParticleDetector/EIS`
- **MMS EIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/EnergeticParticleDetector/EIS`
- **MMS FEEPS** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/EnergeticParticleDetector/FEEPS`
- **MMS FEEPS** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/EnergeticParticleDetector/FEEPS`
- **MMS FEEPS** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/EnergeticParticleDetector/FEEPS`
- **MMS FEEPS** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/EnergeticParticleDetector/FEEPS`
- **MMS Positions** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/Ephemeris`
- **MMS Positions** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/Ephemeris`
- **MMS Positions** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/Ephemeris`
- **MMS Positions** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/Ephemeris`
- **Plasma Wave Investigation** — `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/RPW`

**`MMS ASPOC` — considered and excluded by user decision on 2026-07-27.** Its only support is the data key `aspoc` in `pyrfu/mms/mms_keys.json`; there is no ASPOC-specific reader, calibration, or processing anywhere in the package, making it the weakest of the eleven candidates.

**Solar Orbiter RPW evidence:**
- **Instrument Name:** Plasma Wave Investigation
- **Instrument Identifier:** https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/RPW
- **Evidence (designed-to-support):** `pyrfu/solo/read_tnr.py` and `pyrfu/solo/read_lfr_density.py` are RPW-specific readers — they match the RPW product filename patterns `solo_L2_rpw-tnr-surv.*_YYYYMMDD_Vnn.cdf` and `solo_L3_rpw-bia-density.*_YYYYMMDD_Vnn.cdf`, walk RPW's `L2/thr/` and `L3/lfr_density/` directory trees, and implement RPW-specific science processing (TNR band/sweep reconstruction from `tnr_band_freq`/`tnr_band`/`sweep_num`, `-1e31` fill handling for BIA density). Both are exported from `pyrfu/solo/__init__.py`.
- **Resolution note:** exactly one type-1 row in the controlled vocabulary corresponds to Solar Orbiter's Radio and Plasma Waves instrument (matched via the identifier path segment `Solar_Orbiter/RPW`, since the repo only ever writes "rpw"/"TNR"/"LFR"). Canonical `name` copied verbatim. Two vocabulary rows share the name "Plasma Wave Investigation" (the other is `.../Galileo/PWS`), which is why the SPASE identifier is supplied — it is the de-duplication key and removes the collision.

**Per-instrument evidence:**

| Instrument (canonical vocab `name`) | Candidate SPASE identifiers | Repository evidence at 40505b6a |
|---|---|---|
| MMS FIELDS/FGM | `https://spase-metadata.org/SMWG/Instrument/MMS/{1,2,3,4}/FIELDS/FGM` | `pyrfu/mms/get_data.py` FGM keys (`b_gse_fgm_srvy_l2`, `b_gsm_fgm_brst_l2`, `b_bcs/dmpa_…`), `pyrfu/mms/mms_keys.json` `fgm`/`afg`/`dfg`/`fsm`, `dsl2gse.py`, `dsl2gsm.py` |
| MMS FIELDS/SCM | `.../SMWG/Instrument/MMS/{1,2,3,4}/FIELDS/SCM` | `get_data.py` `SCM: b_gse_scm_brst_l2`; `mms_keys.json` `scm`; `whistler_b2e.py`, `lh_wave_analysis.py` |
| MMS FIELDS/SDP **and** MMS *n* FIELDS Suite, Axial Double Probe | `.../SMWG/Instrument/MMS/{1,2,3,4}/FIELDS/SDP` and `.../FIELDS/ADP` (EDP = SDP + ADP; a per-spacecraft `Electric field Double Probe` row also exists at `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MMS{1,2,3,4}/EDP`) | `get_data.py` EDP keys (`e_gse_edp_brst_l2`, `e_dsl_edp_*`, `hmfe_dsl_edp_brst_l2`, `v_edp_*`, `phase_edp_*`, `sdev12/34_edp_*`), `correct_edp_probe_timing.py`, `scpot2ne.py`, `probe_align_times.py`, `mms_keys.json` `edp` |
| MMS FPI/DES | `.../SMWG/Instrument/MMS/{1,2,3,4}/FastPlasmaInstrument/DES` | `get_data.py` FPI electron keys, `get_dist.py`, `psd_moments.py`, `remove_edist_background.py`, `vdf_*`, `docs/examples/01_mms/example_mms_electron_psd.ipynb`, `example_mms_reduced_electron_dist.ipynb` |
| MMS FPI/DIS | `.../SMWG/Instrument/MMS/{1,2,3,4}/FastPlasmaInstrument/DIS` | `get_data.py` FPI ion keys, `remove_idist_background.py`, `remove_imoms_background.py`, `example_mms_reduced_ion_dist.ipynb`, `example_mms_reduced_ion_dist_para.ipynb` |
| MMS HPCA | `.../SMWG/Instrument/MMS/{1,2,3,4}/HotPlasmaCompositionAnalyzer` | `get_hpca_dist.py`, `hpca_calc_anodes.py`, `hpca_energies.py`, `hpca_pad.py`, `hpca_spin_sum.py`, `get_data.py` HPCA keys, `docs/examples/01_mms/example_mms_hpca.ipynb` |
| MMS EIS | `.../SMWG/Instrument/MMS/{1,2,3,4}/EnergeticParticleDetector/EIS` | 12 dedicated modules: `eis_ang_ang.py`, `eis_combine_proton_pad.py`, `eis_combine_proton_skymap.py`, `eis_combine_proton_spec.py`, `eis_moments.py`, `eis_omni.py`, `eis_pad.py`, `eis_pad_combine_sc.py`, `eis_pad_spinavg.py`, `eis_proton_correction.py`, `eis_skymap.py`, `eis_skymap_combine_sc.py`, `eis_spec_combine_sc.py`, `eis_spin_avg.py`, `get_eis_allt.py`; `docs/examples/01_mms/example_mms_eis.ipynb` |
| MMS FEEPS | `.../SMWG/Instrument/MMS/{1,2,3,4}/EnergeticParticleDetector/FEEPS` | 16 dedicated modules: `feeps_active_eyes.py`, `feeps_avg_4sc.py`, `feeps_bad_data.json`, `feeps_correct_energies.py`, `feeps_corrections.py`, `feeps_energy_table.py`, `feeps_flat_field_corrections.py`, `feeps_omni.py`, `feeps_pad.py`, `feeps_pad_spinavg.py`, `feeps_pitch_angles.py`, `feeps_remove_bad_data.py`, `feeps_remove_sun.py`, `feeps_remove_sunlit_sectors.py`, `feeps_sector_spec.py`, `feeps_spin_avg.py`, `feeps_split_integral_ch.py`, `get_feeps_alleyes.py`, `get_feeps_omni.py`, `read_feeps_sector_masks_csv.py`; `example_mms_feeps.ipynb`, `example_mms_feeps_electrons_4sc.ipynb` |
| MMS Positions | `.../SMWG/Instrument/MMS/{1,2,3,4}/Ephemeris` | MEC support: `get_data.py` `MEC: r_gse_mec_srvy_l2, r_gsm_mec_srvy_l2, r_gse_mec_brst_l2, r_gsm_mec_brst_l2, v_gse/gsm_mec_*`; `mms_keys.json` `mec`; `pyrfu/plot/add_position.py`, `mms_pl_config.py`; ancillary DEFATT/DEFEPH via `load_ancillary.py` |
| MMS ASPOC (excluded) | `.../SMWG/Instrument/MMS/{1,2,3,4}/InstrumentControl/ASPOC` | `pyrfu/mms/mms_keys.json` key `aspoc` only — data-key support with no ASPOC-specific processing. Weakest of the eleven candidates and excluded by user decision on 2026-07-27 |

**Considered and REJECTED (audit trail):**
- **All MAVEN instruments** (ACC, EUV, IUVS, KP, LPW, MAG, NGIMS, PFP, SEP, STATIC, SWEA, SWIA — each has SPASE rows). `pyrfu/maven/` contains only `db_init.py`, `config.json` and `download_data.py`; the latter is a **generic archive downloader** that passes an instrument acronym straight through to the LASP SDC query string (`url = f"{url}instrument={var['inst']}"`, docstring "inst: instrument acronym (acc, euv, iuv, kp, lpw, mag, ngi, pfp, sep, sta, swe, swi)"). There is no MAVEN instrument-specific reader, calibration, or processing anywhere in the package — support is at the *mission archive* level, so MAVEN is listed in Field 32 (with `Observatory/Mission-specific` in Field 17) and no MAVEN instrument is listed here.
- **MMS AFG, DFG, FSM** — genuinely supported data keys (`mms_keys.json` `afg`, `dfg`, `fsm`; `get_data.py` `b_*_afg_srvy_l2pre`, `b_*_dfg_srvy_l2pre`) but the controlled vocabulary has **no rows** for them (only the merged `MMS FIELDS/FGM`); their support is already represented by the FGM entry above.
- **MMS DSP, EDI** — SPASE rows exist (`.../FIELDS/DSP`, `.../FIELDS/EDI`) but PyRFU has no DSP or EDI keys or routines.
- **Cluster, THEMIS, Cassini instruments** — appear only as Langmuir-probe *surface-material* presets in `pyrfu/lp/photo_current.py` (`surface_materials = ["cluster", "themis", "cassini", "aluminium", "aquadag", "gold", "graphite", "solar cells", "1eV", "TiN", "elgiloy"]`) and as a plot color scheme in `pyrfu/plot/pl_tx.py` (`colors: {'cluster', 'mms'}`). No data are read for any of them.
- **Other Solar Orbiter instruments** (EPD, EUI, Metis, PHI, SPICE, STIX, SoloHI, Ephemeris) — SPASE rows exist, but `pyrfu/solo/` reads RPW products only.
- **Generic multi-mission plumbing** — CDF/ISTP support → Field 18 (Input File Formats); OMNIWeb → Field 17 (Data Sources); the AWS S3 HelioCloud bucket → Field 17. None of these are instrument-specific and none are listed here.

**Historical note:** The prior canonical file used freeform instrument text for MMS, MAVEN, and Solar Orbiter. The SPASE-resolved entries above supersede it; MAVEN remains at the mission level because the package has no instrument-specific processing for its archive client.

### 32. Related Observatories (OPTIONAL)

#### Observatory 1
- **Observatory Name:** Magnetospheric Multiscale
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MMS
- **Note:** `pyrfu/mms/` covers MMS data retrieval, instrument-specific calibration, moments, pitch-angle distributions, spectra, velocity-distribution reduction, and four-spacecraft techniques; the README quickstart is an MMS workflow. The SMWG constellation-level row is preferred over archive mirrors and per-spacecraft observatory rows because PyRFU supports the full constellation.

#### Observatory 2
- **Observatory Name:** Solar Orbiter
- **Observatory Identifier:** https://spase-metadata.org/ESA/Observatory/SolarOrbiter
- **Note:** `pyrfu/solo/` reads Solar Orbiter RPW L2/L3 products with mission-specific filename and directory conventions. The agency-canonical `ESA/Observatory/SolarOrbiter` row is chosen over the third-party CDPP-AMDA archive mirror.

#### Observatory 3
- **Observatory Name:** Mars Atmosphere and Volatile EvolutioN
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MAVEN
- **Note:** The prior canonical file named `MAVEN`; the controlled-vocabulary spelling and SPASE identifier are used here. `pyrfu/maven/` is a first-class subpackage whose client targets the MAVEN Science Data Center and lays files out in a MAVEN-specific local tree. The description, `maven` keyword, and `Planetary Magnetospheres` region corroborate this mission relationship. The SMWG row is preferred over the CDPP-AMDA archive mirror.

**Considered and REJECTED (audit trail):** Cluster / THEMIS / Cassini / Galileo — see Field 31's rejection note (surface-material presets and a plot color scheme only). Per-spacecraft rows `SMWG/Observatory/MMS/{1,2,3,4}` — PyRFU supports the whole constellation, so the constellation-level row is the right granularity. CDAWeb / OMNIWeb — multi-mission archives, recorded in Field 17 (Data Sources) as the field definitions direct, not as observatories.

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/louis-richard/irfu-python/40505b6a6e69c6c6ade8ff57062fbb21f23734b8/docs/_static/logo-pyrfu.png
- **Note:** The same asset as the prior canonical file and the PyHC registry, recorded as a raw URL pinned to revision `40505b6a` — which is also this record's Source Revision — rather than to the default `master` branch that both of those sources reference; a branch reference breaks silently on any upstream rename, move or deletion. `docs/_static/logo-pyrfu.png` exists at that revision; an SVG version is also available at `docs/_static/logo-pyrfu.svg`.

---

### Durable upstream limitations
- Zenodo archiving stopped at v2.4.12; `CITATION.cff` and the README DOI badge still point at the v2.4.12 deposit, nine releases behind. Re-enabling the GitHub–Zenodo integration would restore version DOIs.
- `pyproject.toml` still carries `Development Status :: 2 - Pre-Alpha` and 250 modules carry `__status__ = "Prototype"`, contradicting a 100-release history.
- Two code contributors — Apostolos Kolokotronis (6 modules) and Atlas Silverhult (`pyrf/mva_gui.py`) — carry `__author__` tags but appear in no citation source, including `CITATION.cff`.
