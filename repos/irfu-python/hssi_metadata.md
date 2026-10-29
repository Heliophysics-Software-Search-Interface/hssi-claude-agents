# HSSI Metadata Extraction Results

**HSSI Software ID:** bdd706f0-b987-446b-b650-78d9d86f00b2
**Repository:** https://github.com/louis-richard/irfu-python
**Source Revision:** 40505b6a6e69c6c6ade8ff57062fbb21f23734b8
**Extraction Date:** 2026-07-26
**Validation Date:** 2026-10-29
**Validation Status:** PASS

**Source revision context:** `master` HEAD `40505b6a6e69c6c6ade8ff57062fbb21f23734b8` (2026-02-27, "Bump version 2.4.20 -> 2.4.21") is also the `v2.4.21` tag commit; verified against `GET https://api.github.com/repos/louis-richard/irfu-python/branches/master`. (`pushed_at` on the repo is later only because of the unreleased `devel` branch.)

**Release v2.5.7:** Sections brought forward to the `v2.5.7` release (2026-10-29) name the revision their new evidence was read at: `93f7e44f4a18ef3d70bb24ec1ae83c916d79ee34` (short `93f7e44`), which is both the `v2.5.7` tag commit and the head of `master` on 2026-10-29. Its ancestor `dca1a1567a31d97ec5dd6927645bfecc8cc91106` (`dca1a156`) is the `v2.5.6` tag commit. Evidence cited without a revision, or at `40505b6a`, was read at the Source Revision above.

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

**Checked against v2.5.7 (`93f7e44`).** The capabilities the 2.5.x releases add fall under rows already listed, and the files named above as evidence for the stored rows are all still present (except `igrf13coeffs.csv`, replaced by `igrf14coeffs.csv`):
- single-spacecraft probe interferometry and its frequency–wave-number power spectrum (`pyrfu/mms/probe_fields.py`, `fk_power_spectrum.py`) and the separations of the spacecraft pairs along and across B (`mms4_displacement.py`) → `Data Processing and Analysis:Analysis`;
- four-spacecraft timing by cross-correlation (`pyrfu/pyrf/c_4_v_xcorr.py`) and fractional-sample time shifts (`pyrfu/mms/dft_time_shift.py`) → `:Time Series Analysis` and `:Analysis`;
- FEEPS skymaps and gyrophase distributions (`pyrfu/mms/feeps_skymap.py`, `get_gyrophase_dist.py`), and the irfu-matlab `PDist` methods ported in 2.5.1 (`vdf_shift.py`, `vdf_rebin.py`, `vdf_cuts.py`, `vdf_macroparticles.py`, `vdf_partial_density.py`, `vdf_flux.py`, `vdf_mask.py`, `pad_palim.py`, `pad_diffusion.py` and their siblings) → `:3D Particle Distribution Processing` and `:Pitch Angle Distributions`;
- pitch-angle distributions drawn in the (v∥, v⊥) plane (`pyrfu/plot/plot_pad_polar.py`) → `Data Visualization:2D Graphics`;
- the FEEPS correction chain rebuilt in 2.5.1 → the two `Calibration` rows already listed;
- anonymous reads of the public MMS archive on AWS (`pyrfu/mms/list_files_aws.py`) and ancillary files read from the SDC (`load_ancillary.py`) → `:Data Access and Retrieval`;
- IGRF-14 in place of IGRF-13 (`pyrfu/models/igrf.py`) → `Models and Simulations:Empirical`;
- in 2.5.7, `pyrf.magnetosphere` taking the solar-wind pressure and IMF directly, `pyrf.gradient` honouring data gaps, the second-order-section `pyrf.lowpass`, the corrected HPCA distributions (`pyrfu/mms/get_hpca_dist.py`) and 146 more MMS CMAD variables in `mms.get_data`, the DSP power spectral densities among them → `Models and Simulations:Empirical`, `Data Processing and Analysis:Time Series Analysis`, `:3D Particle Distribution Processing` and `:Data Access and Retrieval`.

`Data Visualization:Mission-Specific` was considered: the plots in the style of the MMS SDC quicklooks are drawn only in example notebooks (`docs/examples/01_mms/example_mms_feeps.ipynb`, `example_mms_eis.ipynb`), which rule 4 excludes. A sweep of `pyrfu/` at `93f7e44` for `matplotlib.animation`, `plotly`, `bokeh`, `sklearn`, `torch`, `tensorflow`, `mpi4py`, `dask`, `multiprocessing` and CUDA, and of the tree for container files, finds none of them, so the other rejections above stand.

### 5. Related Region (MANDATORY)
- **Earth Magnetosphere**
- **Interplanetary Space**
- **Planetary Magnetospheres**
- **Mars Magnetosphere**
- **Solar Wind**
- **Earth Outer Magnetosphere**

**Note:** Earth Magnetosphere is supported by the whole `pyrfu/mms/` package (91 modules at `40505b6a`, 113 at `93f7e44`) plus `pyrf/magnetosphere.py`, `models/magnetopause_normal.py`, `models/igrf.py`, and `pyrf/l_shell.py`; Interplanetary Space is supported by `pyrf/get_omni_data.py` (solar-wind/IMF), `pyrf/shock_normal.py`, `shock_parameters.py`, `docs/examples/01_mms/example_mms_ipshocks.ipynb`, `example_mms_walen_test.ipynb`, and `pyrfu/solo/` (Solar Orbiter RPW in the inner heliosphere); Planetary Magnetospheres is supported by `pyrfu/maven/` (Mars). `Mars Magnetosphere` is supported by the first-class MAVEN Science Data Center client and its MAVEN instrument catalogue at `pyrfu/maven/download_data.py:114-132`. `Solar Wind` is supported by the OMNI solar-wind and IMF retrieval implemented at `pyrfu/pyrf/get_omni_data.py:127-137,140-167`. `Earth Outer Magnetosphere` is supported by the exported magnetopause-location routine at `pyrfu/pyrf/magnetosphere.py:29-36` and the spacecraft inside/outside magnetopause calculation at `pyrfu/models/magnetopause_normal.py:55-82`. `Solar Environment` and `Earth Atmosphere` are deliberately not selected: nothing in the package works with solar-disk/coronal or neutral-atmosphere data.

**Checked against v2.5.7 (`93f7e44`).** The 2.5.x releases add no region-specific code; the modules cited above keep their roles (`pyrfu/models/igrf.py` now evaluates IGRF-14). `Earth Magnetosheath` and `Earth Magnetotail` were walked and are not selected, because no routine is written for either region (rule 4). In the package code `magnetosheath` and `plasma sheet` occur only in the note of `pyrfu/mms/psd_moments.py` on FPI's recommended energy index, which names the intervals it was checked on, and `magnetosheath` also in a reference title in `pyrfu/pyrf/shock_normal.py`; `magnetotail` and `dipolarization` occur in no module. The bow-shock and magnetopause models are boundary models, already the evidence for `Solar Wind`, `Interplanetary Space` and `Earth Outer Magnetosphere`. The MMS routines work the same in every region the spacecraft cross, so the regions where they are applied in papers do not by themselves make region rows; code written for one of those regions would. `Earth Inner Magnetosphere` was also walked and is not selected: `pyrfu/pyrf/l_shell.py` evaluates a dipole L at the spacecraft position, a coordinate rather than inner-magnetosphere physics (rule 4), and the radiation-belt words in `pyrfu/pyrf/ebsp.py` name the MAARBLE project the routine was developed in, a borrowed label (rule 3). The MEC L, MLT and MLAT variables `mms.get_data` loads from 2.5.7 are coordinates too.

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
- **Affiliation:**
  - **Organization:** University of Oxford
  - **Affiliation Identifier:** https://ror.org/052gg0110

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

**Considered and not selected:** `CITATION.cff` at revision `40505b6a` lists a seventh, organization-style author as its first entry: a bare `- name: "PyRFU team"` with no `given-names` or `family-names`. It is absent from the prior canonical file and from both the DataCite and Zenodo creator lists, which contain only the six people. A ROR lookup finds no institution because "PyRFU team" is a project team, not a registered organization. By user decision on 2026-07-27, it is not included without maintainer confirmation and a durable organization identity. The project has since dropped it: `CITATION.cff` at `93f7e44` (v2.5.7) lists only the six people, and the README's new citation reference names the same six.

**University of Oxford (Louis Richard), added for v2.5.7.** `CITATION.cff` at `93f7e44` gives his affiliation as "Rudolf Peierls Centre for Theoretical Physics, University of Oxford, UK" (it read "IRF Uppsala, Sweden" at `40505b6a`), `pyproject.toml` gives his address as `louis.richard@physics.ox.ac.uk`, and the README credits say the software "is now maintained by Louis RICHARD at the Rudolf Peierls Centre for Theoretical Physics, University of Oxford". His ORCID record lists an employment at the University of Oxford (department "Theoretical Physics", Oxford, GB, no dates given) beside his Swedish Institute of Space Physics postdoctoral employment, which ends 2026-06-30. The 2.5.x releases were made there, so the institution covers the period the current software was produced (rule 21) and is recorded with its ROR, whose display name is `University of Oxford`; ROR's affiliation matching chooses that record for the `CITATION.cff` string. The department is not recorded: HSSI has no Organization row for it and ROR does not register it (a ROR search for `Peierls` returns nothing, against `Uppsala` and `Oxford` controls that return records), so rule 23 records the institution. His Swedish Institute of Space Physics and Uppsala University affiliations stay (rule 17); they are where the earlier releases were written.

**Note (author-name provenance):** The display forms above match the prior canonical file and DataCite exactly. `CITATION.cff` used the shorter given names "Yuri" and "Daniel" at `40505b6a`; at `93f7e44` it writes "Yuri V." and "Daniel B.", as DataCite, Zenodo and the README's citation reference do, so every project source now agrees with the fuller forms.

### 7. Software Name (MANDATORY)
- **Value:** PyRFU
- **Note:** The prior canonical file said `Python RymdFysik Utilities (PyRFU)`, but that is the DataCite/Zenodo record title rather than the name the software goes by. Repository evidence supports the short form: `pyproject.toml name = "pyrfu"`, `CITATION.cff title: "pyrfu"` (at `40505b6a`), the README heading `pyRFU`, and the PyHC registry entry `name: PyRFU`. The shorter `PyRFU` is therefore used.
- **Note (v2.5.7):** At `93f7e44` `CITATION.cff` has taken the record title, `title: "Python RymdFysik Utilities (PyRFU): An Open-Source Python Package for Advanced In-Situ Space Plasma Analysis"`, and the README's citation reference uses the same title in sentence case. It is a citation title with a subtitle, inside which the project still writes the name `PyRFU`; the stored name is a form the project uses (rule 3) and stays. `pyproject.toml`, the README heading and the PyHC entry are unchanged.

### 8. Description (MANDATORY)
**Value:**
PyRFU is a free and open-source Python package for advanced analysis of in-situ space plasma data. It provides routines to work with space data, particularly with Magnetospheric Multiscale (MMS) mission data, as well as MAVEN and Solar Orbiter missions. The package includes general plasma physics routines for coordinate transformations, particle distribution analysis, plasma moments calculations, wave analysis (including polarization and wavelets), multi-spacecraft techniques (curlometer, gradient estimation), and comprehensive data visualization capabilities. PyRFU is based on the IRFU-MATLAB library and supports data retrieval from multiple sources including local files, MMS Science Data Center, MAVEN Science Data Center, and cloud storage (AWS S3). The package additionally provides analytic plasma dispersion-relation solvers, Langmuir-probe and spacecraft-potential current models, and empirical field and boundary models including IGRF-14 and the Shue et al. (1998) magnetopause and bow shock.

- **Note:** The established description is retained, with a final sentence approved on 2026-07-27 to cover three substantial subpackages that the earlier wording omitted.
- **IGRF-14 (v2.5.7):** The final sentence named IGRF-13 until this update. Release 2.5.0 moved the model to the 14th generation: at `93f7e44` `pyrfu/models/igrf.py` loads `igrf14coeffs.csv` and documents "the IGRF-14 model", and `igrf13coeffs.csv` is deleted. Only the generation number in the approved sentence changed. By user decision on 2026-10-29 the number was replaced, rather than deleting the model name as Field 8 rule 2 would for a capability the code lacks, because the capability remains and only its generation moved.
- **Other claims re-tested at `93f7e44`:** the MMS, MAVEN and Solar Orbiter subpackages and the routine families named are all present; the README now says the package "started from the IRFU-MATLAB library"; and every retrieval route named still exists, AWS S3 now read anonymously (`pyrfu/mms/list_files_aws.py`, unsigned `boto3` session). The project's own descriptions changed wording in 2.5.1 — the `CITATION.cff` abstract is "pyrfu is an open-source Python package for advanced in-situ space plasma analysis, particularly of the Magnetospheric Multiscale (MMS) mission." and the README's lead sentence says much the same — but neither names a capability the stored text omits, so rule 3 does not fire and the stored text is kept (rule 6).
- **"based on the IRFU-MATLAB library":** commit `364d9b55` (2026-10-08, first released in 2.5.1) removed this wording from the README lead, `docs/index.rst` and the `CITATION.cff` abstract; its message reads "pyrfu has grown well beyond IRFU-MATLAB: describe it on its own in the README, the docs landing page and the CITATION.cff abstract, and keep IRFU-MATLAB as its origin in the credits." The stored clause is curator-retained wording that stays true of the package's origin (the README credits say it "started from the IRFU-MATLAB library", and the code ports irfu-matlab routines throughout, Field 29), so rule 6 keeps it; the code does not contradict it, so rule 2 does not fire.
- **Evidence for the appended sentence:** it covers three of PyRFU's six subpackages that the original text omitted entirely. Dispersion-relation solvers — `pyrfu/dispersion/one_fluid_dispersion.py` and `disp_surf_calc.py` (`optimize.fsolve` on analytic dispersion relations), with two example notebooks in `docs/examples/02_dispersion/`. Langmuir-probe / spacecraft-potential current models — `pyrfu/lp/` (`LangmuirProbe` class, `photo_current.py`, `thermal_current.py`, all exported in `pyrfu/lp/__init__.py` `__all__`), plus `pyrfu/mms/scpot2ne.py`. Empirical field and boundary models — `pyrfu/models/igrf.py` (IGRF-13, coefficients in `igrf13coeffs.csv`, at `40505b6a`; IGRF-14 and `igrf14coeffs.csv` from release 2.5.0, see above), `pyrfu/pyrf/magnetosphere.py` (`model="mp_shue1998"` and bow shock), `pyrfu/models/magnetopause_normal.py`.

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
- **Value:** v2.5.7
- **Note:** HSSI held v2.4.21 (released 2026-02-27) until this update, and v2.4.12 before that; each was superseded by a newer release (rule 3). Eight releases followed v2.4.21: 2.5.0 (2026-10-07) and 2.5.1 to 2.5.7 (2026-10-19 to 2026-10-29). Each has a `v`-prefixed tag on `master`'s own lineage (`git merge-base --is-ancestor v2.5.<n> 93f7e44` holds for all eight), a GitHub release that is neither a draft nor a pre-release, and a PyPI wheel and sdist that are not yanked; no version number carries a pre-release suffix. `v2.5.7` is the newest: its tag points at `93f7e44f4a18ef3d70bb24ec1ae83c916d79ee34`, the head of `master` on 2026-10-29, where `pyproject.toml` has `version = "2.5.7"` and `CITATION.cff` has `version: "2.5.7"`. The `v` prefix follows the form this entry already used; the tag writes `v2.5.7`, while the GitHub release name, PyPI and `pyproject.toml` write `2.5.7`.

#### Version Date
- **Value:** 2026-10-29
- **Note:** The GitHub release `v2.5.7` was published 2026-10-29T11:42:15Z (rule 7). The tagged commit (2026-10-29T10:57:45Z), the PyPI wheel upload (2026-10-29T11:46:09Z) and `CITATION.cff` `date-released: 2026-10-29` agree.

#### Version Description
- **Value:** the body of the GitHub release `v2.5.7`, with whole items trimmed as the note below lists:

```markdown
pyrfu 2.5.7 fixes `mms.get_hpca_dist`, which paired each HPCA sample with the azimuth of the next one, and lets `mms.get_data` load 146 more variables of the MMS CMAD. `pyrf.magnetosphere` takes the solar wind directly, as irfu-matlab; `pyrf.lowpass` is stable for low cutoffs; `pyrf.gradient` no longer differentiates across data gaps. Seven routines are faster, with the same results.

> **Before updating:** some results change.
> - `mms.get_hpca_dist`: the data of each half-spin are one sample later, the polar angles are those of the anodes, and there is one distribution per half-spin, NaN where it is incomplete.
> - `pyrf.gradient` differs next to data gaps (and so dB/dt in `pyrf.st_diff`).
> - `pyrf.magnetosphere`: the magnetopause has one more point (angles 0, 0.1, ..., 3.1 rad, as irfu-matlab).
> - `pyrf.lowpass` differs for cutoffs below about 1e-4 of the Nyquist frequency, and at the first and last samples.
> - `pyrf.optimize_nbins_1d/2d` also try `n_max` bins.

## New
- `mms.get_data`: 146 more variables of the MMS CMAD:
  - FPI: heat flux and its error, error flags, density extrapolation, DES pitch angle distributions, partial pressure, DES fast parallel and perpendicular temperatures;
  - EDP: quality and bitmask (E field and spacecraft potential), slow `dce` error and E parallel;
  - FGM: flag and position;
  - MEC: quaternions to 11 frames, MLT, MLAT, L, Kp, Dst, eclipse flags, position in SM;
  - HPCA: pressure tensors, parallel and perpendicular temperatures, spin-averaged B;
  - DSP: E and B power spectral densities;
  - EDI: E and drift velocity (survey);
  - SCM: survey and high-speed burst.
- `pyrf.magnetosphere`: `d_p`, `b_z` and `m_a` give the solar wind directly, as irfu-matlab `irf_magnetosphere(model, Dp, Bz)`, and identical to it.
- `pyrf.gradient`: `time_step` sets the data gaps, by default as irfu-matlab `irf_gradient`.
- `mms.get_hpca_dist`: `elevation`, `source` and `data_path`, as `mms.hpca_pad`, and the times of the distributions.
- `mms.reduce`: `verbose=False` turns off the progress bar.

## Changed behaviour
- `pyrf.lowpass`: the sampling frequency is `f_s`, as elsewhere in pyrfu, by default that of the input; `fhz` still works with a `FutureWarning`. NaN inputs, cutoffs outside (0, f_s / 2) and 12 samples or fewer raise `ValueError`.
- `mms.get_hpca_dist`: one distribution per half-spin, NaN where it is not complete or has no azimuths (they were zeros, and a single zero azimuth raised `AssertionError`). The anode elevations are read from the file of the data by default.
- `pyrf.magnetosphere`, `mms.reduce`, `mms.get_hpca_dist` and `pyrf.iso86012datetime` raise `ValueError` for invalid inputs.

## Fixes that change results
- `mms.get_hpca_dist`: the 16 samples of a half-spin start at its first sample. They were shifted by one, as in SPEDAS `mms_get_hpca_dist`: each sample had the azimuth of the next one (11.4° off), and the first sample came from the previous half-spin. The polar angles were 90° minus the anode numbers.
- `pyrf.gradient` differentiates each segment between data gaps separately, as `irf_gradient`; it differentiated across the gaps.
- `pyrf.magnetosphere`: the magnetopause angles are those of irfu-matlab.
- `pyrf.lowpass`: second-order sections. The old filter was unstable below about 3e-5 of the Nyquist frequency (outputs of 40 for an input of 1) and off by 4 % at 1e-4. The padding is MATLAB's `filtfilt`.
- `pyrf.optimize_nbins_1d/2d` include `n_max`, as documented.
- `pyrf.autocorr` computes in double precision (float32 inputs: differences of about 1e-7).

## Fixes
- `mms.reduce`: integer `lower_e_lim`, case-insensitive `dim` and `base`, NaN for time steps without any channel above the spacecraft potential (it raised `IndexError`).
- `pyrf.dist_append` and `mms.get_dist`: distributions without energy widths can be appended and reduced (`KeyError`, `AttributeError`, `TypeError`).
- `mms.psd_moments`: no warnings for unused speeds or a zero density.
- `pyrf.autocorr` accepts integers; `pyrf.optimize_nbins_1d/2d` leave out NaN samples (they raised).
- `pyrf.lowpass` keeps the attributes.
- Faster, same results:
  - `pyrf.wavelet`: about 2 times, and 1 to 1.5 GB less memory on long series.
  - `pyrf.autocorr`: 65 times on 200000 samples.
  - `mms.rotate_tensor`: 10 to 15 times.
  - `pyrf.optimize_nbins_2d`: 15 to 20 times (it took about 30 s for the default 100 × 100 and 1e5 samples).
  - `pyrf.iso86012datetime`: about 100 times.
  - `pyrf.ebsp` (25 %) and `pyrf.cotrans` through GSM and SM.

## Upgrade notes
- `mms.tokenize` no longer lists the parameter names without data (`nbge`, `pbge`, `defbge`, `tsi`, `tse`, `epar`; they always failed in `get_data`). For the scalar temperatures, take the trace of `ti_dbcs`/`te_dbcs` over 3; for E parallel, the `e_par` keys.
```

- **Note:** Derived afresh for v2.5.7 (rule 10) from the release body; the release name is the bare `2.5.7` and adds nothing (rule 13). Every kept line is verbatim, with line endings normalised (rule 15). Kept: the opening summary, the "Before updating" list of results that change, the *New*, *Changed behaviour*, *Fixes that change results* and *Fixes* sections, which are new functionality, changed behaviour and bugs a user could hit (rule 14) — the speed and memory gains listed under *Fixes* included, since they change what a user can run — and the *Upgrade notes* item on the `mms.tokenize` parameter names it no longer lists, a changed API. Dropped as whole items: the blockquote's closing pointer to the sections below and the changelog, the *Documentation* section (docstring work), the *Upgrade notes* line saying the requirements are unchanged, and the closing changelog link. The v2.4.21 description this replaces was a summary composed from that release's notes, a form rule 15 excludes, and it is not carried forward. The `CHANGELOG.rst` entry for 2.5.7 covers the same changes in longer prose; the notes of 2.5.0 to 2.5.6 belong to those releases (rule 11) and are not merged in.

#### Version PID
- **Value:** Not found
- **Note:** The concept DOI `10.5281/zenodo.10678694` still has a single version, `10.5281/zenodo.10678695` (version 2.4.12, published 2024-02-19), per the Zenodo versions API and DataCite on 2026-10-29, after the v2.5.7 release. No deposit exists for v2.5.7, so the PID stays empty (rule 18), as it was for v2.4.21. `CITATION.cff` (`doi: 10.5281/zenodo.10678695`) and the README's DOI badge and citation reference still point at the v2.4.12 deposit; that DOI must not be used as the PID of a later release.

### 13. Programming Language (RECOMMENDED)
- **Value:** Python 3.x
- **Note:** At `93f7e44` (v2.5.7) the supported minor versions are 3.12–3.15: `pyproject.toml` `requires-python = ">=3.12,<3.16"`, classifiers `Programming Language :: Python :: 3.12` through `3.15` plus `3 :: Only`, and a CI matrix of 3.12–3.15. Release 2.5.0 dropped 3.10 and 3.11, following PHEP 3. At `40505b6a` the range was 3.10–3.14 (v2.4.18 had added 3.13 and 3.14), which superseded the prior canonical file's 3.10–3.12 note. A file-extension census at `93f7e44` finds `.py` sources besides notebooks, data, configuration and documentation files, so `Python 3.x` stays the only row.

### 14. Reference Publication (RECOMMENDED)
- **Value:** Not found
- **Note:** No paper describing PyRFU was found. The concept DOI has no `IsDescribedBy` or `IsSupplementTo` publication and `CITATION.cff` has no `preferred-citation`. At `40505b6a` the README asked users to cite the repository URL; at `93f7e44` (v2.5.7) its Acknowledgement section asks them to cite the Zenodo software deposit `10.5281/zenodo.10678695` (Richard et al., 2024) with the version used. That is a software deposit, which rule 1 keeps out of this field. On 2026-10-29 ADS title and abstract searches for `pyrfu` and a title search for `RymdFysik` returned nothing (control: `title:"pyspedas"` returned 14 records), and Louis Richard's Zenodo deposits include no paper about the package.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT
- **Note:** Four independent sources agree: `LICENSE.txt` begins "MIT License / Copyright (c) 2020 L. RICHARD"; DataCite identifies the MIT License and URI; `pyproject.toml` declares it; and the README states that PyRFU is distributed under the open-source MIT license. At `40505b6a` `pyproject.toml` pointed at the license file and carried the MIT classifier; at `93f7e44` (v2.5.7) it declares the SPDX expression `license = "MIT"` with `license-files = ["LICENSE.txt"]` and the classifier is gone. `LICENSE.txt` is unchanged between the two revisions, and `CITATION.cff` has `license: MIT`.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Value:** The terms use the vocabulary's stored form; `Langmuir probes` carries a capital L.

**User-selected terms (2026-07-27), each repo-evidenced:** `Langmuir probes` (the `pyrfu/lp/` subpackage), `igrf13` (`pyrfu/models/igrf.py` and `igrf13coeffs.csv`), `shue` (`pyrfu/pyrf/magnetosphere.py`), `l shell` (`pyrfu/pyrf/l_shell.py`), `istp` (the ISTP attribute dependence documented in Field 18), and `energetic particles` (EIS and FEEPS modules).

**`igrf14` replaces `igrf13` (v2.5.7).** HSSI held `igrf13` until this update. Release 2.5.0 moved `pyrfu/models/igrf.py` to the 14th generation and deleted `igrf13coeffs.csv`, so `igrf13` lost its only support (rule 13); at `93f7e44` the model loads `igrf14coeffs.csv` and the tracked tree holds no `IGRF-13` or `igrf13` string. The existing `igrf14` row names the generation the code now evaluates (rules 10–11).

**`magnetic reconnection` and `turbulence`, added for v2.5.7.** On 2026-07-27 they were not selected because neither was a vocabulary row and expanding the vocabulary for this record was declined. Both are rows now, written exactly `magnetic reconnection` and `turbulence`, so they bind without minting (rule 11). They name PyRFU's two main fields of application, a searcher would type them (rule 10), and the evidence listed below still holds at `93f7e44`.

**`pyhc package`.** PyRFU is listed in the PyHC registry's `_data/projects.yml`, so the record carries the catalogue's PyHC marker keyword, written exactly `pyhc package` (rule 15). HSSI held it before this file listed it.

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
- igrf14
- in situ measurements
- instrumentation
- istp
- l shell
- Langmuir probes
- line plots
- magnetic reconnection
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
- pyhc package
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
- turbulence
- velocity distribution functions
- wave polarization
- wavelet analysis

**Established terms:**
coordinates · data access · data retrieval · heliosphere · instrumentation · line plots · magnetosphere · maven · mms · multidimensional · omni · orbit · planetary · plasma physics · plotting · power spectra · python 3 · solar orbiter · space physics · spectra · theory · time

*(Origin: the PyHC registry keyword list for PyRFU — `heliosphere, magnetosphere, planetary, plasma_physics, coordinates, data_retrieval, line_plots, multidimensional, orbit, plotting, power_spectra, spectra, time, general, local, remote, web_service, data_access, data_analysis, instrumentation, theory, maven, mms, omni, solo` — plus the GitHub topics `python3`, `space-physics`. The registry entry, its keywords and the topics were unchanged on 2026-10-29.)*

**Additional repo-evidenced terms:**

| Keyword | Evidence |
|---|---|
| in situ measurements | README/PyHC/description core framing: "advanced analysis of **in-situ** space plasma data" |
| space plasma | Same; `Topic :: Scientific/Engineering :: Physics` classifier; whole package scope |
| solar wind | `pyrfu/pyrf/get_omni_data.py` (OMNI solar-wind/IMF retrieval), `shock_normal.py`, `shock_parameters.py`, `docs/examples/01_mms/example_mms_ipshocks.ipynb`, `example_mms_walen_test.ipynb` |
| cdf | Primary input format; `pyrfu/pyrf/read_cdf.py`, `pyrfu/mms/get_ts.py`, `get_dist.py`, `get_variable.py` (pycdfpp), `pyrfu/pyrf/cdfepoch2datetime64.py` (cdflib at `40505b6a`; at `93f7e44` it converts CDF epochs without cdflib) |
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
| data visualization | Entire `pyrfu/plot/` subpackage (21 modules and 22 exported names at `40505b6a`; 22 modules at `93f7e44`) |

**Evidence for `magnetic reconnection` and `turbulence`** (selected for v2.5.7; see above):
- `magnetic reconnection` — strongly evidenced: `docs/examples/01_mms/example_mms_edr_signatures.ipynb` (electron diffusion region), `example_mms_walen_test.ipynb`, `pyrfu/pyrf/match_phibe_dir.py`, `match_phibe_v.py`, `pyrfu/mms/calculate_epsilon.py`, `docs/examples/01_mms/example_mms_ohmslaw.ipynb`; at `93f7e44` also the agyrotropy measures `pyrfu/pyrf/calc_dng.py` and `calc_sqrtq.py`, whose references are papers on collisionless magnetic reconnection (Aunai et al. 2013; Swisdak 2016)
- `turbulence` — evidenced: `pyrfu/pyrf/pvi.py`, `pvi_4sc.py` (partial variance of increments), `struct_func.py`, `increments.py`; at `93f7e44` also `pid_4sc.py` (pressure–strain interaction, which cites work on Vlasov-Maxwell turbulence)

**`data analysis`:** PyHC lists `data_analysis`, `general`, `local`, `remote`, `web_service`, and `solo` for PyRFU. `solo` is covered by `solar orbiter`; `general`, `local`, `remote`, and `web_service` are infrastructure tags rather than science keywords. `data analysis` is supported by the curated PyHC registry and the prior canonical file and is therefore included.

### 17. Data Sources (OPTIONAL)
- **Observatory/Mission-specific**
- **OMNIWeb**
- **S3/Cloud-aware**

**Evidence:**
- **OMNIWeb** — `pyrfu/pyrf/get_omni_data.py` builds `https://omniweb.gsfc.nasa.gov/cgi/nx1.cgi?activity=retrieve&spacecraft=omni2|omni_min…` and reads the response with `urllib.request.urlopen`.
- **Observatory/Mission-specific** — MMS Science Data Center (`pyrfu/mms/list_files_sdc.py`, `download_data.py`, `download_ancillary.py`, `list_files_ancillary_sdc.py`) and MAVEN SDC (`pyrfu/maven/download_data.py`, `LASP_PUBL = "https://lasp.colorado.edu/maven/sdc/public/files/api/v1/"`). Per Field 17's instruction, the corresponding missions are cross-listed in Field 32.
- **S3/Cloud-aware** — `pyrfu/mms/list_files_aws.py` uses `boto3.resource("s3")` with a configurable bucket/prefix (`pyrfu/mms/config.json` `"aws"` key); `boto3>=1.35.0` and `botocore>=1.35.0` are hard dependencies; `mms.get_data(..., source="aws")`. At `93f7e44` (v2.5.7) the resource is opened with an unsigned session (`signature_version=UNSIGNED`), so `mms.db_init(default="aws")` reads the public MMS archive on NASA HelioCloud without AWS credentials (2.5.0), and `mms.get_eis_allt` can also load from AWS (2.5.1).
- **Observatory/Mission-specific, at `93f7e44`** — `mms.load_ancillary` reads the DEFATT, DEFEPH and DEFQ ancillary files from the SDC (2.5.4 and 2.5.5), and `load_brst_segments` reads the burst-segment list from the SDC's LaTiS service (`https://lasp.colorado.edu/mms/sdc/public/service/latis/mms_burst_data_segment.csv`); from 2.5.7 `mms.get_hpca_dist` takes the same `source` choice as the other MMS loaders.

**`HTTP/HTTPS Directories` — held until v2.5.7, removed.** It rested on the SDC and OMNIWeb retrievals and on `pyrfu/mms/load_brst_segments.py` fetching `http://www.spedas.org/mms/mms_brst_intervals.sav` over plain HTTP (`40505b6a`). At `93f7e44` that function reads the SDC's LaTiS service instead, and no `spedas.org` address remains in `pyrfu/`. What is left is the MMS and MAVEN Science Data Centers' file APIs, a mission archive that `Observatory/Mission-specific` carries (rule 9), and OMNIWeb, a named service with its own row (rule 6); no routine downloads files from a plain directory tree.

**Considered and rejected:** `CDAWeb`, `HAPI`, `das2`, `SSCWeb`, `TAP`, `VirES`, `The Virtual Solar Observatory`, `FTP/FTPS Directories` — no client code for any of these (rechecked at `93f7e44`: every remote request in `pyrfu/` goes to the MMS or MAVEN SDC, OMNIWeb or the S3 bucket). `CDAWeb` gets its own verdict: the default S3 prefix, `gov-nasa-hdrl-data1/spdf/cdaweb/data/mms`, is HelioCloud's copy of the CDAWeb MMS data tree (`pyrfu/mms/list_files_aws.py` calls it the "Public copy of the MMS archive (CDAWeb) on NASA HelioCloud"), but the package lists and reads that copy through the S3 API, which `S3/Cloud-aware` carries; it calls no CDAWeb service and fetches nothing from the CDAWeb site, so the `CDAWeb` row, for a client that reaches CDAWeb itself (rule 7), is not selected. Solar Orbiter data are read from a **local** directory tree only (`pyrfu/solo/db_init.py`, `config.json` `local_data_dir`), with no remote fetch, so Solar Orbiter adds no new data-source value.

### 18. Input File Formats (RECOMMENDED)
- **CDF**
- **ISTP-Compliant**
- **ascii**

**`IDL.sav` — held until v2.5.7, removed.** At `40505b6a` `pyrfu/mms/load_brst_segments.py`, a public exported function, imported and called `readsav` on the externally hosted MMS burst-segment IDL SAVE file, which is why the format was listed (an earlier rationale had wrongly rejected it on the claim that `scipy.io.readsav` is not a dependency). From release 2.5.0 (and at `93f7e44`) the function parses the SDC's burst-segment CSV instead, and no `readsav` call or `.sav` reader remains in `pyrfu/`, so the format lost its only reader.

**`csv` — considered for v2.5.7 and not selected.** From release 2.5.0 `mms.load_brst_segments` requests the burst-segment list from the MMS SDC's LaTiS service (`https://lasp.colorado.edu/mms/sdc/public/service/latis/mms_burst_data_segment.csv`) and parses the response in memory with `csv.reader`. It takes no file: its `data_path` and `download` arguments are "Deprecated and ignored". Field 18 records the formats of input files, and its rule 9 treats software that fetches data over a network API into memory as reading no files, so this response is not an input file a user could hand the package. Read together, rule 5 (a reader that opens the format) and rule 9 therefore leave `csv` out. The comma-separated tables the package reads from disk are all bundled with it (`igrf14coeffs.csv`, the FEEPS sun-mask CSVs read by `read_feeps_sector_masks_csv.py`), which is the reason `csv` was declined on 2026-07-27, and that reason still holds.

**Other evidence:** `CDF` is the primary format used by `pyrfu/pyrf/read_cdf.py`, the MMS readers, and the Solar Orbiter readers. The other values are supported as follows:
- **ISTP-Compliant** — `pyrfu/mms/get_ts.py` reads and depends on ISTP metadata attributes: `file[cdf_name].attributes["DEPEND_0"]`, an assertion that `"DEPEND_0" in var_attrs and "epoch" in var_attrs["DEPEND_0"].lower()`, plus handling of `DEPEND_1`/`REPRESENTATION_1`; `pyrfu/mms/eis_ang_ang.py` writes `FILLVAL`, `VALIDMIN` ISTP attributes. The package relies on the ISTP convention, not merely on raw CDF.
- **ascii** — `pyrfu/pyrf/get_omni_data.py` parses the plain-text OMNIWeb response; `pyrfu/mms/load_ancillary.py` reads whitespace-delimited MMS ancillary (ephemeris/attitude) products, from the local data store with `source="local"` or from the SDC, with `pd.read_csv(file, sep=r"\s+", header=None, skiprows=…)` driven by `pyrfu/mms/ancillary.json` column definitions.
- **`csv` — considered and rejected by user decision on 2026-07-27.** The comma-separated tables the package reads are all bundled inside it, not user-supplied science data. That is the same internal-lookup-table category used to reject `JSON`. `ascii` is different because it covers external OMNIWeb responses and downloaded MMS ancillary products. The rationale was recorded at `40505b6a` and still holds at `93f7e44` (see the `csv` note above). Under rule 9 it is the downloaded ancillary files, which `load_ancillary` also reads from the local data store, that carry `ascii`; the OMNIWeb response, parsed in memory, would not carry it alone. At `93f7e44` `load_ancillary` reads the whitespace-delimited ancillary products, now including DEFQ, with `pd.read_csv(..., sep=r"\s+")`.

**Considered and rejected:** `JSON` — JSON is read only for package-internal configuration/lookup tables (`pyrfu/{mms,maven,solo}/config.json`, `ancillary.json`, `mms_keys.json`, `feeps_bad_data.json`, `shock_models_parameters.json`) and for the MAVEN SDC's file-listing API response, never as a science-data input format. `HDF5`, `netCDF3/4`, `FITS`, `Zarr` — no reader present (`h5py`, `netCDF4`, `astropy` are not dependencies, at `40505b6a` or at `93f7e44`). **Correction history:** an earlier version of this note rejected `IDL.sav` on the false claim that `scipy.io.readsav` was absent; it was present and used at `40505b6a`, and `IDL.sav` was listed until release 2.5.0 removed its reader.

### 19. Output File Formats (RECOMMENDED)
- *(none)*

**Rationale:** `CDF` was removed by user decision on 2026-07-27 because the package has no CDF-writing API.

**Evidence for the removal (read at `40505b6a`):** A full search of the package found **no CDF-writing API** (no `cdfwrite`/`CDFWriter`/`pycdfpp` write calls, no `to_netcdf`, `to_csv`, `to_json`, `to_zarr`, `to_hdf`, `np.save`, or `savemat` anywhere in `pyrfu/`). Every `pycdfpp` call was `pycdfpp.load`, and `cdflib` was imported only for `cdfepoch` time conversion (from release 2.5.0 `cdflib` is not imported at all, Field 29). The only files the package writes are downloaded mission CDFs copied into the local data store (`pyrfu/mms/download_data.py` → `copyfileobj` into a temp file then `copy(ftmp.name, out_file)`; `pyrfu/maven/download_data.py`; `pyrfu/mms/download_ancillary.py`; `pyrfu/mms/load_brst_segments.py`). In-memory results are returned as `xarray` objects, not written to disk. The prior canonical file's note ("Software can write CDF files based on the CDF library dependencies") was an inference this evidence does not support. Field 19's instruction is "only formats actually supported should be indicated" for **generated** files; caching a downloaded mission `.cdf` is not generating CDF output.

**Checked against v2.5.7 (`93f7e44`).** The write-path search finds the same: besides downloads and copies of mission data files (`download_data.py`, `copy_files.py`), the only files written are configuration files, the JSON that `pyrfu/{mms,maven,solo}/db_init.py` save with `json.dump` and the packaged configuration that `pyrfu/_user_config.py` and `pyrfu/mms/db_init.py` copy into the user directory (bookkeeping, rule 3). `pycdfpp` is used for `load` and for time conversions (`to_tt2000`, `to_datetime64`), never to save, and `load_brst_segments` no longer caches the burst-segment list (its docstring: "Deprecated and ignored: the segments are not cached any more.").

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Mac**
- **Windows**
- **Operating System Independent**

**Note:** `pyproject.toml` declares Unix, macOS, and Windows classifiers, and `.github/workflows/tests.yml` tests `macos-latest`, `windows-latest`, and `ubuntu-latest` (both still so at `93f7e44`). PyRFU is pure Python with no compiled extension and no platform restriction; the v2.5.7 wheel on PyPI is `pyrfu-2.5.7-py3-none-any.whl`. Field 20 rule 3 therefore records `Operating System Independent` together with each OS the project names or tests. HSSI held the three concrete rows without `Operating System Independent` until v2.5.7; an earlier rationale left it out because the three platforms are directly supported, which rule 3 does not treat as a reason. `Solaris` and `MobilePlatform` have no evidence.

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Note:** This is a pure-Python package; `pyproject.toml` declares no architecture constraint and builds no compiled extensions. `numba` provides architecture-portable JIT acceleration, and there is no CUDA, `mpi4py`, or HPC job-script support.

### 22. Related Phenomena (OPTIONAL)
- **Solar Wind**

**Note:** The prior canonical file said "Not found", but `Solar Wind` is directly supported by `pyrfu/pyrf/get_omni_data.py`, the Shue magnetopause and bow-shock models, the shock-normal and shock-parameter routines, and the interplanetary-shock and Walen-test notebooks.

**Considered and rejected:** the other controlled values. `Coronal Heating`, `Coronal Mass Ejections`, `Solar Corona`, `Solar Flares`, `X-ray emission` — PyRFU is an in-situ plasma package with no solar imaging, coronal, or remote-sensing functionality. (`Coronal Holes` was listed here previously but is **not** a row in the live vocabulary; the `hssi-field-definitions` list is stale on that point.)

**`Geomagnetic Storms` — considered and excluded (decision settled 2026-08-25).** The original rationale claimed there was no storm-index or Dst/Kp handling. That premise was false: `pyrfu/pyrf/get_omni_data.py` maps OMNI columns for `dst`, `ae`, `al`, `au`, `kp`, and `pc`, and the function is publicly exported. The exclusion still stands on the narrower rationale that retrieving an index is not science functionality for storms and the package has no storm-phase, superposed-epoch, or Dst-modelling code. The package's characteristic phenomena of magnetic reconnection, plasma turbulence, and plasma waves or instabilities have no controlled phenomena rows; `magnetic reconnection` and `turbulence` were also considered and declined as newly created Field 16 keywords by user decision on 2026-07-27, and were added to Field 16 for v2.5.7 once both were existing rows. From 2.5.7 `mms.get_data` also loads Kp and Dst from the MEC files; loading an index computes no storm diagnostic (rule 5) and an index is not the phenomenon (rule 6), so the exclusion stands.

### 23. Development Status (RECOMMENDED)
- **Value:** Active
- **Note:** The last commit on `master` is `93f7e44` (2026-10-29), the `v2.5.7` release commit of the same day, so rule 6 gives `Active`. Zenodo declares the development status `Active`; the repository is not archived; four CI workflows run at `93f7e44` (`tests.yml`, `pylint.yml`, `publish-to-pypi.yml`, and `pyhc-actions.yml`, added in 2.5.3; `codeql.yml` was removed in 2.5.1); and PyHC rates software maturity and documentation `Good`. This matches the repostatus.org definition of a stable, usable project under active development. The README's `Status` badge shows the PyPI classifier status, not a repostatus.org badge, so rule 3 does not apply.
- **Conflicting signal, deliberately not followed:** `pyproject.toml` still carries the classifier `Development Status :: 2 - Pre-Alpha`, and individual modules carry `__status__ = "Prototype"`. Both are stale boilerplate that contradicts a PyPI release history running from 1.8.3 (2020-11-27) to 2.5.7 (2026-10-29), an explicit maintainer-set Zenodo status of "active", and PyHC's maturity rating; `Pre-Alpha` also has no HSSI equivalent (the nearest, `WIP`, means "no stable, usable public release yet", which is plainly false here).

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
- https://doi.org/10.1029/2024GL112038
- https://doi.org/10.1029/2025JA033745
- https://doi.org/10.1029/2025GL116933
- https://doi.org/10.1029/2025JA034175
- https://doi.org/10.1029/2025JA034952
- https://doi.org/10.1029/2026GL125110
- https://doi.org/10.3847/1538-4357/ae9ebc

**The six curator-supplied papers (kept, rule 7).** The prior canonical file said "Not found," but these six curator-supplied DOIs are supported by Crossref: every paper is first-authored by Louis Richard, PyRFU's principal author, and concerns the package's MMS reconnection and turbulence domain. Each also credits the software. ADS full text matches the acknowledgement wording the README suggested at `40505b6a` (the phrases "performed using the pyrfu" and "pyrfu analysis package") in five of them; the sixth, 10.1103/PhysRevLett.132.105201, is not matched in ADS's full text, but its arXiv version (arXiv:2303.08693) ends its data statement with "Data analysis was performed using the pyrfu analysis package [90].", reference 90 being the PyPI project page. They do not appear in the repository or concept DOI metadata.

**Method references in the code and the docs — weighed and not listed (user decision, 2026-10-29).** At `93f7e44` PyRFU's docstrings cite 31 distinct DOIs in their reference blocks, plus references without a DOI, and the example notebooks cite further papers. Weighed one by one, 48 would qualify under Field 27 rule 4 as written, which counts "the code's own reference block" as evidence; three of them are notebook citations whose papers the text does not identify. Of the 48, 43 are heliophysics method, model and instrument papers: among them the curlometer (Dunlop et al. 2002; Robert et al. 1998), minimum variance and de Hoffmann–Teller analysis (Sonnerup & Scheible 1998; Khrabrov & Sonnerup 1998), four-spacecraft timing (Vogt et al. 2011), the agyrotropy measures, the bow-shock and magnetopause models behind `shock_normal` and `magnetopause_normal`, and the FPI background corrections (Gershman et al. 2017, 2019). The other five are generic numerical, statistical, geometric or engineering routines: Welch's PSD estimator, histogram bin-size selection (two papers), the solid angle of a triangle and the capacitance of a cylinder. The rest of the references are not publications, cannot be identified from the citation, or are the source of an example's event. None of the 48 is listed on these grounds, by user decision on 2026-10-29. Each motivated the behaviour of one routine, and listing some 48 of them would bury the publications actually about the software under a list a user would have to sift. A small number of method papers that a piece of software is itself based on can be listed; a library whose functions each cite their own method papers does not list them. A later refresh should not re-propose them. Kolokotronis et al. (2026), one of the 48, is also weighed below as a developer-authored paper.

**Literature search, 2026-10-29.** ADS full text (`full:"pyrfu"`) returns 28 records: 14 space-physics papers (the five incumbents it matches, the seven third-party papers listed below and the two developer-authored papers weighed below) and 14 papers from biochemistry, genomics and neighbouring fields, outside this one. `ack:"pyrfu"` returns 4. The acknowledgement sentence the README suggested at `40505b6a`, "Data analysis was performed using the pyrfu analysis package available at https://github.com/louis-richard/irfu-python", was used to find deliberate credits: `full:"pyrfu analysis package"` returns 12 records and `full:"performed using the pyrfu"` 9. From release 2.5.0 the README suggests instead "Data analysis was performed using the open-source pyrfu package (Richard et al., 2024), version X.Y.Z."; ADS full text matched no paper with it (`full:"open-source pyrfu package"`: 0), and a later search should use both wordings. Controls: a nonsense token returned 0, `full:"pyspedas"` returned 171, and `full:"performed using the pyspedas"` returned 8. Neither Zenodo DOI is named in ADS full text (`10678694`, `10678695`: 0), and a creator-keyed Zenodo search for Louis Richard finds only datasets and analysis code of individual papers besides the PyRFU deposit. PyRFU's citing literature is small, so acknowledged uses are still news (rule 5); a later update should re-test that as the list grows.

**Third-party papers that credit the software, added for v2.5.7 (rule 5).** Each is a peer-reviewed article with no PyRFU author whose results were produced with the package and which says so in its own text, in its Acknowledgments or in a statement naming the package as the analysis software (titles as ADS gives them):
- https://doi.org/10.1029/2024GL112038 — Lewis, Stawarz, Matteini et al. (2024), "Turbulent Energy Conversion Associated With Kinetic Microinstabilities in Earth's Magnetosheath", Geophysical Research Letters: the `40505b6a` README's acknowledgement wording and the repository name `irfu-python` appear in its text.
- https://doi.org/10.1029/2025JA033745 — Singh, Fraschetti and Giacalone (2025), "Generation of Perpendicular Ion Acoustic Waves in the Ramp Region of Earth's Bow Shock in the Presence of a Flat-Top Electron Velocity Distribution", Journal of Geophysical Research: Space Physics: the sentence after its MMS Science Data Center data address reads "Data analysis was performed using irfu‐matlab (see https://github.com/irfu/irfu‐matlab/ ) and pyrfu (see https://pypi.org/project/pyrfu/ ) analysis packages." The article is closed access; the sentence was read in ADS's full-text index of its body.
- https://doi.org/10.1029/2025GL116933 — Montagud-Camps, Toledo-Redondo, Goldstein et al. (2025), "Statistical Analysis of the Warm Plasma Cloak in the Dayside Magnetosphere: 9 Years of MMS Observations", Geophysical Research Letters: credited in its Acknowledgments ("analysis was performed using the pyrfu").
- https://doi.org/10.1029/2025JA034175 — Tarvus, Turc, Settino et al. (2025), "Heat Flux Signatures of Finite Larmor Radius Ion Mixing Driven by Magnetopause Kelvin-Helmholtz Waves", Journal of Geophysical Research: Space Physics: credited in its Acknowledgments.
- https://doi.org/10.1029/2025JA034952 — Settino, Vörös, Sorriso-Valvo et al. (2026), "Energy Conversion Pathways Inside Kelvin-Helmholtz Vortices", Journal of Geophysical Research: Space Physics: the acknowledgement wording ("performed using the pyrfu") appears in its text.
- https://doi.org/10.1029/2026GL125110 — Guo, Lu, Lu et al. (2026), "Spiky Bursts of Energetic Electron Beams Upstream of Nonstationary Quasi-Perpendicular Shocks", Geophysical Research Letters: credited in its Acknowledgments.
- https://doi.org/10.3847/1538-4357/ae9ebc — Montagud-Camps, Hellinger, Toledo-Redondo et al. (2026), "Decay of Space Plasma Turbulence Downstream of Bow Shocks: MMS Magnetosheath Unbiased Campaign Observations", The Astrophysical Journal: credited in its Acknowledgments.

**Developer-authored papers that use the software — weighed and not listed (user decision, 2026-10-29).** https://doi.org/10.1029/2026GL122885 — Kolokotronis, Graham, Khotyaintsev, Norgren, Steinvall and Richard (2026), "Statistical Study of Betatron and Fermi Electron Acceleration at Dipolarization Fronts", Geophysical Research Letters — and https://doi.org/10.1029/2026GL123161 — Richard, Khotyaintsev and Norgren (2026), "Occurrence of Flat-Top Electron Velocity Distributions in Magnetotail Plasma Jets", Geophysical Research Letters — both carry the `40505b6a` README's acknowledgement wording ("pyrfu analysis package"). They are the developers' own science done with the package, not publications about it: Field 27 rule 3 admits the developers' papers about the software and rule 5 third-party uses, and neither admits them. By user decision on 2026-10-29 neither is listed. The six curator-supplied papers of the same kind stay under rule 7, which keeps an incumbent that uses the software even when it would not be added today. A later refresh should not re-propose these two. The documentation cites the Kolokotronis paper in two example notebooks at `93f7e44`: `docs/examples/01_mms/example_mms_feeps_electrons_4sc.ipynb` says that the four-spacecraft FEEPS energy-channel combination it passes to `mms.feeps_avg_4sc` "is explained in the supplementary information of Kolokotronis et al. (2026)", and `example_mms_feeps_skymap.ipynb` takes its worked event, the dipolarization front DF2, from the paper. As a per-routine method reference it falls under the method-references decision above, not rule 4. The Richard et al. paper is cited nowhere in the repository at `93f7e44`.

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found
- **Note:** The concept DOI has no dataset related identifier. The repository names MMS and Solar Orbiter data products extensively but never cites dataset DOIs or `hpde.io` identifiers, so none is asserted. SPDF NumericalData records would require separate curation rather than being inferred from product names.

### 29. Related Software (OPTIONAL)

**Entries:**
- **https://github.com/irfu/irfu-matlab** — IRFU-Matlab, PyRFU's predecessor. **This is the single most distinguishing related-software link.** PyRFU is explicitly the Python re-implementation of it: `README.rst` says the package is based on the IRFU-MATLAB library (at `93f7e44`: it "started from the IRFU-MATLAB library"), and the established description says the same. The 2.5.x releases port further irfu-matlab routines and check results against it; at `93f7e44` 64 non-test modules under `pyrfu/` name irfu-matlab, typically as the implementation they reproduce ("As irfu-matlab mms.scpot2ne."). Field 29 explicitly covers predecessors (rule 9). Its Zenodo concept DOI, `https://doi.org/10.5281/zenodo.11550090` (DataCite title "IRFU-Matlab", `IsSupplementTo https://github.com/irfu/irfu-matlab/tree/v1.18.0`, creators Khotyaintsev, Nilsson, Johansson, Vaivads, Graham, Karlsson — overlapping PyRFU's own author list), is passed over for the repository URL (rule 13).
- **https://github.com/SciQLop/CDFpp** — pycdfpp, PyRFU's CDF library (`pycdfpp>=0.9.0` at `93f7e44`, `pycdfpp>=0.7.0` at `40505b6a`). `pyrfu/pyrf/read_cdf.py`, the MMS readers and the Solar Orbiter readers all use `pycdfpp.load`, and since 2.5.0 the CDF time conversions (`datetime642ttns.py`, `ttns2datetime64.py`) go through it as well. A domain-specific dependency that characterises the software (rule 9). An earlier rationale claimed no DOI existed, because the deposit is titled `CDFpp` rather than `pycdfpp`; its concept DOI, `https://doi.org/10.5281/zenodo.6391115`, is passed over for the repository URL (rule 13).
- **https://github.com/tsssss/geopack** — geopack (`geopack>=1.0.10`): `pyrfu/plot/plot_magnetosphere.py` imports `from geopack import geopack` and calls `geopack.recalc()` and `geopack.trace()` to draw traced model field lines (still so at `93f7e44`). A domain-specific dependency (rule 9). geopack has its own HSSI entry, and this is that entry's stored `code_repository_url` (rule 11); its Zenodo DOI `https://doi.org/10.5281/zenodo.15110786` (DataCite "tsssss/geopack: v1.0.12") is passed over.

**URL form (v2.5.7).** HSSI held each of these as a Zenodo DOI until this update. The site shows a related item's raw URL as its link text, so a repository URL a reader recognises replaces each DOI (rules 11–13); the passed-over DOIs are named above, so the choice can be reversed if HSSI ever renders resolved titles. The IRFU-Matlab and CDFpp repositories are upstream projects, not forks, and neither has an HSSI entry.

**`cdflib` — held until v2.5.7, removed.** HSSI listed cdflib (`https://doi.org/10.5281/zenodo.1481144`, DataCite "MAVENSDC/cdflib") as a domain-specific dependency: at `40505b6a` `cdflib>=1.3.0` was required, and `pyrfu/pyrf/cdfepoch2datetime64.py`, `datetime642ttns.py` and `ttns2datetime64.py`, all exported, imported `cdfepoch` from it. Release 2.5.0 dropped it (release notes: "`cdflib` is no longer used; new dependency `platformdirs`"). At `93f7e44` it is in neither `pyproject.toml` nor `requirements.txt`, no package module imports it (the remaining mentions are in `CHANGELOG.rst` and a test comment), and the three conversions use their own arithmetic or `pycdfpp`. The relation is gone (rules 7 and 15). CDFlib has its own HSSI entry (`https://github.com/lasp/cdflib`), the form to use should the relation return.

**Considered and REJECTED (audit trail).** Generic scientific-Python / infrastructure dependencies, excluded under the Field 29/30 relevance gate because the entry would be equally true of most Python packages and says nothing about PyRFU: `numpy>=2.0,<2.4`, `scipy>=1.14.0`, `pandas>=2.2.3`, `matplotlib>=3.9.0`, `requests>=2.32.0`, `python-dateutil>=2.9.0`, `tqdm>=4.66.0`, `numba>=0.63.0` (JIT compiler — generic infrastructure), `boto3`/`botocore` (AWS SDK — generic I/O plumbing), `keyring`/`keyrings.alt` (credential storage), `platformdirs` (the user configuration directory, a dependency from 2.5.0), `setuptools`/`wheel` (packaging), and the optional dev/test/docs extras (`pytest`, `pytest-cov`, `ddt`, `black`, `flake8`, `isort`, `pylint`, `mypy`, `pre-commit`, `sphinx` and its plugins, `nbsphinx`, `numpydoc`, `pydata-sphinx-theme`). Also rejected: `xarray` **here**, because it belongs in Field 30 where the demonstrated data-model exchange is documented (see below); and Cluster/THEMIS/Cassini tooling — those names appear in `pyrfu/lp/photo_current.py` only as spacecraft-surface *material* presets (`surface_materials = ["cluster", "themis", "cassini", "aluminium", …]`) and in `pyrfu/plot/pl_tx.py` only as a color-scheme option, which is not a software relationship.

- **pyspedas and IDL SPEDAS (considered at v2.5.7).** At `93f7e44` the FEEPS routines document that they reproduce `mms_load_feeps` step by step ("the order of IDL SPEDAS and pyspedas"), and the 2.5.1 release notes say the corrected FEEPS chain matches pyspedas to round-off. That names a reference implementation the routines were checked against, not an alternative the project offers its users (rule 9), and no module imports either package.

### 30. Interoperable Software (OPTIONAL)

- **https://github.com/pydata/xarray** — xarray.
  **Cited evidence of a demonstrated data-model exchange (Tier B bar):** `xarray` is not merely a dependency — `xarray.DataArray`/`xarray.Dataset` *is* PyRFU's documented public interchange format, so a user's PyRFU results are directly consumable by, and constructible from, any other xarray-based tool.
  - Public constructors that **return** xarray objects: `pyrfu.pyrf.ts_scalar`, `ts_vec_xyz`, `ts_tensor_xyz`, `ts_spectr`, `ts_skymap`, `ts_time`, `ts_append` (all in `pyrfu/pyrf/__init__.py` `__all__`).
  - Public readers that **return** xarray objects: `pyrfu.pyrf.read_cdf` (`import xarray as xr`; "Construct xarray DataArray" → returns a dict of `xr.DataArray`), `pyrfu.mms.get_data` (signature annotated `-> Union[DataArray, Dataset]`), `pyrfu.mms.get_ts`, `get_dist`, `get_variable`, `pyrfu.solo.read_tnr`, `read_lfr_density`, `pyrfu.mms.load_ancillary` (`data_frame.to_xarray()`), `pyrfu.mms.spectr_to_dataset`.
  - Public functions that **accept** xarray objects as their documented input type — e.g. `pyrfu/pyrf/cotrans.py` asserts `isinstance(inp, xr.DataArray)`; `pyrfu/mms/reduce.py` and `vdf_projection.py` document `vdf : xarray.Dataset`; `pyrfu/pyrf/wave_fft.py` documents `inp : xarray.DataArray`.
  This is exactly the "public API returns/accepts `xarray.Dataset` as its documented interchange format" case the field definition admits, not "uses xarray internally".
  The evidence above was read at `40505b6a` and still holds at `93f7e44` (v2.5.7): the seven `ts_*` constructors are exported, `read_cdf` builds `xr.DataArray` objects, `mms.get_data` is annotated `-> Union[DataArray, Dataset]`, `load_ancillary` returns `data_frame.to_xarray()`, and `cotrans` still asserts an `xr.DataArray` input.
- **URL form (v2.5.7).** HSSI held xarray as its Zenodo concept DOI, `https://doi.org/10.5281/zenodo.598201` (DataCite: "xarray", Software, Zenodo), until this update. Field 30 rule 11 applies Field 29's URL rules, so the upstream repository root replaces it (Field 29 rules 12(a) and 13); the concept DOI is named here so the choice can be reversed if HSSI ever renders resolved titles. xarray has no HSSI entry.

**Considered and REJECTED (audit trail):**
- **cdflib, pycdfpp** — Tier B; they are used to *read* files, which is dependency use rather than a peer-tool exchange. pycdfpp is recorded in Field 29 as a domain-specific dependency; cdflib has not been used at all since 2.5.0 (Field 29).
- **pyspedas / IDL SPEDAS** (considered at v2.5.7) — the FEEPS routines reproduce `mms_load_feeps` and were checked against pyspedas (2.5.1), but no data passes between the packages: neither is imported, and there is no converter or shared object (rule 5).
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

**`MMS ASPOC` — considered and excluded by user decision on 2026-07-27.** Its support is a data key (`aspoc` in `pyrfu/mms/mms_keys.json`, `ionc_aspoc_srvy_l2` in `mms.get_data`) and an optional input of `mms.scpot2ne`, which adds the ASPOC ion-emitter current to the current balance when estimating density from the spacecraft potential (`i_aspoc`, present at `40505b6a` and at `93f7e44`; its docstring notes "ASPOC on does not work very well."). An earlier version of this note said there was no ASPOC-specific processing anywhere in the package, which that input contradicts. There is still no ASPOC reader, calibration or analysis of ASPOC's own measurements, so ASPOC remains the weakest of the eleven candidates: someone working with ASPOC data would not reach for PyRFU (rule 6), and the exclusion stands.

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
| MMS ASPOC (excluded) | `.../SMWG/Instrument/MMS/{1,2,3,4}/InstrumentControl/ASPOC` | `pyrfu/mms/mms_keys.json` key `aspoc`, the `get_data` key `ionc_aspoc_srvy_l2`, and the optional ASPOC-current input of `scpot2ne.py` — no ASPOC reader or calibration. Weakest of the eleven candidates and excluded by user decision on 2026-07-27 |

**Considered and REJECTED (audit trail):**
- **All MAVEN instruments** (ACC, EUV, IUVS, KP, LPW, MAG, NGIMS, PFP, SEP, STATIC, SWEA, SWIA — each has SPASE rows). `pyrfu/maven/` contains only `db_init.py`, `config.json` and `download_data.py`; the latter is a **generic archive downloader** that passes an instrument acronym straight through to the LASP SDC query string (`url = f"{url}instrument={var['inst']}"`, docstring "inst: instrument acronym (acc, euv, iuv, kp, lpw, mag, ngi, pfp, sep, sta, swe, swi)"). There is no MAVEN instrument-specific reader, calibration, or processing anywhere in the package — support is at the *mission archive* level, so MAVEN is listed in Field 32 (with `Observatory/Mission-specific` in Field 17) and no MAVEN instrument is listed here.
- **MMS AFG, DFG, FSM** — genuinely supported data keys (`mms_keys.json` `afg`, `dfg`, `fsm`; `get_data.py` `b_*_afg_srvy_l2pre`, `b_*_dfg_srvy_l2pre`) but the controlled vocabulary has **no rows** for them (only the merged `MMS FIELDS/FGM`); their support is already represented by the FGM entry above.
- **MMS DSP, EDI — at v2.5.7.** SPASE rows exist for each spacecraft: `MMS FIELDS/DSP` (`https://spase-metadata.org/SMWG/Instrument/MMS/{1,2,3,4}/FIELDS/DSP`) and `MMS FIELDS/EDI` (`https://spase-metadata.org/SMWG/Instrument/MMS/{1,2,3,4}/FIELDS/EDI`). Up to `dca1a156` (v2.5.6) PyRFU had no DSP or EDI keys or routines. From 2.5.7 `mms_keys.json` has `dsp` and `edi` keys, holding 16 DSP power-spectral-density variables and 6 EDI survey variables (E field and drift velocity), which `mms.get_data` loads like any other key. No module processes, calibrates or analyses either instrument's data; the `EDI` mentions in `vdf_rebin.py` describe an FPI energy range that matches EDI's. That is the variable table of an MMS-wide loader, where the user names the variable at run time (rule 2). It is less support than ASPOC's, which adds an optional input to `scpot2ne` and was excluded on 2026-07-27, and someone working with DSP or EDI data would find a loader key in PyRFU, not a tool for that instrument (rule 6). Neither is listed; a routine written for either instrument's data would change this. Rule 2 is written for an archive-wide client whose facility is chosen at run time, and rule 6 for software that directly reads an instrument's data; a mission-wide loader with a per-instrument variable table falls between the two, so this verdict rests on rule 2 by analogy and on the ASPOC precedent, a gap in the rules that a later update should not read as settled by them.
- **Cluster, THEMIS, Cassini instruments** — appear only as Langmuir-probe *surface-material* presets in `pyrfu/lp/photo_current.py` (`surface_materials = ["cluster", "themis", "cassini", "aluminium", "aquadag", "gold", "graphite", "solar cells", "1eV", "TiN", "elgiloy"]`) and as a plot color scheme in `pyrfu/plot/pl_tx.py` (`colors: {'cluster', 'mms'}`). No data are read for any of them.
- **Other Solar Orbiter instruments** (EPD, EUI, Metis, PHI, SPICE, STIX, SoloHI, Ephemeris) — SPASE rows exist, but `pyrfu/solo/` reads RPW products only.
- **Generic multi-mission plumbing** — CDF/ISTP support → Field 18 (Input File Formats); OMNIWeb → Field 17 (Data Sources); the AWS S3 HelioCloud bucket → Field 17. None of these are instrument-specific and none are listed here.

**Checked against v2.5.7 (`93f7e44`).** The 2.5.x releases extend support within the instruments listed: probe interferometry from the six EDP probe potentials, which are the spin-plane (SDP) and axial (ADP) probes (`pyrfu/mms/probe_fields.py`; new `get_data` keys `v6_edp_*` and `vpsp_edp_*`); FEEPS skymaps (`feeps_skymap.py`); FPI's recommended energy index (`partidx{i,e}_fpi_*`); the DEFATT, DEFEPH and DEFQ ancillary files read from the SDC (`load_ancillary.py`), which add to the `MMS Positions` ephemeris support; and the Solar Orbiter TNR reader ported from irfu-matlab (`pyrfu/solo/read_tnr.py`). Up to `dca1a156` (v2.5.6) `mms_keys.json` had the same ten top-level instrument keys as at `40505b6a`. Release 2.5.7 adds `dsp` and `edi` (see the DSP and EDI note above) and widens the variable tables of instruments already listed: HPCA pressure tensors, temperatures and spin-averaged B; MEC quaternions, MLT, MLAT, L, Kp and Dst; SCM survey and high-speed burst; FGM flags; EDP quality flags. No listed instrument lost support, and `pyrfu/maven/` and `pyrfu/solo/` keep the roles described above.

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
- **Checked against v2.5.7 (`93f7e44`):** the file is byte-identical at `93f7e44` and is still the documentation's light-theme logo (`docs/conf.py` `image_light` and `html_logo`). The docs add a dark-theme variant, `docs/_static/logo-pyrfu-dark.png`, and the tree holds `docs/_static/logo-pyrfu_new.png`, which nothing references; neither replaces the project's mark. The pinned URL served `image/png` on 2026-10-29.

---

### Durable upstream limitations
- Zenodo archiving stopped at v2.4.12 (2024-02-19) while releases continued to v2.5.7 (2026-10-29). At `93f7e44` `CITATION.cff`, the README DOI badge and the README's citation reference all point at the v2.4.12 deposit. Re-enabling the GitHub–Zenodo integration would restore version DOIs.
- `pyproject.toml` still carries `Development Status :: 2 - Pre-Alpha`, and module headers carry `__status__ = "Prototype"` (246 modules at `40505b6a`, 278 at `93f7e44`), contradicting a release history from 1.8.3 (2020) to 2.5.7 (2026).
- Two code contributors — Apostolos Kolokotronis (6 modules) and Atlas Silverhult (`pyrf/mva_gui.py`) — carry `__author__` tags but appear in no citation source, including `CITATION.cff` (still so at `93f7e44`).
