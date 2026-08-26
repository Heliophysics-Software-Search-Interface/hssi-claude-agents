# HSSI Metadata Extraction Results

**HSSI Software ID:** 3f058476-5010-48f4-9bd9-e27648d2ecea
**Repository:** https://github.com/LM-SAL/irispy
**Source Revision:** cd8ad59083e883d5a1db661ef56ab81856bf81eb
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Source note: placeholder. The live HSSI view API does not expose the original submitter.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.10443678

*Source note: the Zenodo record identifies this as the **concept** DOI — `zenodo.org/api/records/20073073` reports `conceptdoi: 10.5281/zenodo.10443678` and `conceptrecid: 10443678`.*

### 3. Code Repository (MANDATORY)
https://github.com/LM-SAL/irispy

*Source note: confirmed by `git remote -v`, `pyproject.toml` (`urls."Source Code"`), PyPI `project_urls`, and Zenodo `custom["code:codeRepository"]`. The repository was renamed from `LM-SAL/irispy-lmsal` (that path now redirects here), and the PyHC registry still lists the old URL, so the value above is the current repository.*

### 4. Software Functionality (MANDATORY)

**Coordinate Transforms**
- `Coordinate Transforms` — parent of the two entries below.
- `Coordinate Transforms:Mission-Specific` — `irispy/io/sji.py::_create_gwcs` builds a per-exposure IRIS pointing model from the AUX extension (`XCENIX`/`YCENIX` reference coordinates, `PC1_1IX`…`PC2_2IX` rotation matrices) using `VaryingCelestialTransform`; `irispy/io/spectrograph.py` corrects the IRIS slit offset (`POFFYFUV`/`POFFYNUV`) and reverses the V34 raster scan direction; `SJIMeta.satellite_rotation` exposes `SAT_ROT` roll.
- `Coordinate Transforms:Solar` — cubes carry solar frames the user can transform: `sunpy.coordinates.frames.Helioprojective` celestial frame in the gWCS output frame, `get_body_heliographic_stonyhurst` Earth-observer ephemeris, `HeliographicStonyhurst` transform under `SphericalScreen` in `irispy/io/spectrograph.py`; `cube.axis_world_coords()` returns solar coordinates; `examples/coalign/02_reproject_iris_roll_aia.py` reprojects IRIS into the SDO/AIA frame.

**Data Processing and Analysis**
- `Data Processing and Analysis` — parent.
- `Data Processing and Analysis:2D Slices` — `SJICube.__getitem__` / `_normalize_tuple_index` slice 3D cubes (preserving `basic_wcs` per slice); `examples/analysis/01_spectral_fitting.py` crops the raster at a single `SpectralCoord` to extract a 2D spatial slice; `irispy/utils/_spectral.py::make_spatial_template` builds 2D spatial cubes from 3D spectral cubes.
- `Data Processing and Analysis:Analysis` — `irispy/utils/moments.py::calculate_moments` (0th/1st/2nd spectral moments, Doppler velocity and line-width maps), `irispy/utils/red_blue.py::calculate_red_blue_asymmetry` (RBA maps with per-pixel quality flags and error propagation), `irispy/utils/density.py::density_diagnostic` (electron density from line ratios).
- `Data Processing and Analysis:Calibration` — `irispy/utils/spectrograph.py::radiometric_calibration`, `convert_photons_per_sec_to_radiance`, `calculate_dn_to_radiance_factor` (DN → photons → erg cm⁻² s⁻¹ sr⁻¹ Å⁻¹, with exposure-time correction); `irispy/utils/response.py::get_latest_response` / `get_interpolated_effective_area`; `docs/tutorial/calibration.rst`; `examples/calibration/03_radiometric_calibration.py`.
- `Data Processing and Analysis:Data Access and Retrieval` — `irispy/data/sample.py` + `irispy/data/_sample.py::_get_sample_files` download IRIS sample data on attribute access via `sunpy.util.parfive_helpers.Downloader` across three mirrors; `download_all()` is public API; `irispy/conftest.py` uses `pooch.retrieve`.
- `Data Processing and Analysis:Data Reduction` — cosmic-ray sigma-clipping/median cleaning (`irispy/utils/cosmic_rays.py`), spectral-window subsetting (`read_spectrograph_lvl2(spectral_windows=...)`), `memmap=True` out-of-core reading, temporal downsampling in `generate_wobble_movie` (`wobble_cadence`), spatial/spectral rebinning in `examples/analysis/01_spectral_fitting.py`.
- `Data Processing and Analysis:Image Processing` — `irispy/utils/utils.py::calculate_dust_mask` (`scipy.ndimage.binary_dilation`), `irispy/utils/dust.py::remove_dust` (temporal replacement with local-median spatial fallback), `irispy/utils/cosmic_rays.py::remove_cosmic_rays` (`rsliding` sliding sigma-clipping and `astroscrappy.detect_cosmics` backends), `image_clipping` histogram-based intensity scaling.
- `Data Processing and Analysis:Processing` — `irispy/io/utils.py::read_files` orchestrates reading/grouping/tar-extraction of a whole IRIS observation into `NDCollection`s; `irispy/meta.py` (`SJIMeta`/`SGMeta`) converts ~60 IRIS FITS keywords into physical quantities.
- `Data Processing and Analysis:Spectrogram` — `irispy/io/spectrograph.py::read_spectrograph_lvl2` builds `SpectrogramCube` / `SpectrogramCubeSequence` / `RasterCollection` spectrogram data products from IRIS raster FITS; `SpectrogramCube.spectral_dispersion`, `.solid_angle`, `.wavelength_axis`. IRIS "sit-and-stare" observations (`docs/tutorial/level_2.rst`, `docs/known_issues.rst`) hold the slit fixed and produce a genuine 2D intensity array over **wavelength × time**, which is structurally the same product as a classic time-frequency spectrogram; `SpectrogramCubeSequence` carries these. The term is used here in the slit-spectrograph sense rather than the FFT/wavelet sense; HSSI already applies `Spectrogram` to non-FFT spectral/temporal data elsewhere (e.g. the live `speasy` entry).
- `Data Processing and Analysis:Time Series Analysis` — time is a first-class cube axis (`extra_coords.add("time", ...)`, `gwcs` `TemporalFrame`, `SJIMeta.temporal_cadence`); `examples/analysis/03_umbral_flashes.py` builds space–time images and intensity-vs-time light curves of sunspot umbral oscillations and cross-matches SJI/raster cadences.

**Data Visualization**
- `Data Visualization` — parent.
- `Data Visualization:2D Graphics` — `SJICube.plot` / `SpectrogramCube.plot` render WCS-aware images through `IRISPlotter`; moment, RBA, dopplergram and density maps are plotted as 2D images in `examples/analysis/*`.
- `Data Visualization:2D Slices` — `IRISArrayAnimatorWCS` (subclass of `mpl_animators.ArrayAnimatorWCS`) displays a 2D slice of a 3D/4D cube with sliders; `IRISSequenceAnimator` sets IRIS slider labels `["Raster step", "Scan number"]`.
- `Data Visualization:Line Plots` — `SpectrogramCube.plot` drops the colormap for 1D data and produces line plots of spectra; `examples/analysis/01_spectral_fitting.py`, `04_spectral_moments.py`, `05_red_blue_asymmetry.py`, `07_mg_ii_two_gaussian_fitting.py` plot spectral profiles and light curves.
- `Data Visualization:Mission-Specific` — `irispy/visualization.py` is entirely IRIS-specific: `IRISPlotter`, `IRISArrayAnimatorWCS`, `IRISSequencePlotter`, `set_axis_properties` (helioprojective axis labelling/colouring in arcsec, wavelength axis in nm) and per-passband IRIS SJI colormaps `plt.get_cmap(f"irissji{TWAVE1}")` / `sunpy.visualization.colormaps.color_tables.iris_sji_color_table`.
- `Data Visualization:Movies` — `irispy/utils/wobble.py::generate_wobble_movie` writes MP4 files via `matplotlib.animation.FuncAnimation` + `FFMpegWriter` (FFMPEG required, installed in all CI jobs).
- `Data Visualization:Spectrogram` — `SpectrogramCube.plot` / `SpectrogramCubeSequence.plot` display IRIS raster spectrograms (wavelength × slit position) and, for sit-and-stare observations, wavelength × time spectrograms, with wavelength-aware axes via `IRISSequencePlotter`/`IRISPlotter`. *Same slit-spectrograph sense as the processing counterpart above.*

**Mission-related** — irispy is the IRIS instrument team's own analysis library (`pyproject.toml` author `IRIS Instrument Team  @ LMSAL`; `licenses/LICENSE.rst` copyright "IRIS Instrument Team @ LMSAL"; hosted in the `LM-SAL` GitHub organization; `.cruft.json` `author_email: https://iris.lmsal.com/contact.html`), so it is mission software rather than a generic tool that happens to read IRIS data.
- `Mission-related` — parent.
- `Mission-related:Analysis` — IRIS-specific analysis utilities: `irispy.utils.moments`, `irispy.utils.red_blue`, `irispy.utils.density`, `irispy.obsid.ObsID` (decodes 10-digit IRIS OBS IDs against the shipped v34/v36/v38/v40 OBS-ID tables).
- `Mission-related:Calibration` — `radiometric_calibration` is documented as replicating the SolarSoft IDL routines `iris2/iris_calib_spectrum.pro` and `nrl/iris_calib.pro`; dust and cosmic-ray/spike removal address known IRIS detector artefacts.
- `Mission-related:Instrument Response` — `irispy/utils/response.py` ships and evaluates the IRIS response file `irispy/data/iris_sra_c_20231106.geny`, reproducing SSWIDL `iris_get_response.pro` and `fit_iris_xput.pro` to give time-dependent FUV/NUV SG and 4-channel SJI effective areas.
- `Mission-related:Observatory/Instrument Models` — the same response computation multiplies per-optical-element transmission curves (`ELEMENTS`, `INDEX_EL_SG`, `INDEX_EL_SJI`, `GEOM_AREA`) and applies the FUV SG "slant" normalisation, i.e. an optical model of the IRIS instrument. *Matches how HSSI already classifies the analogous aiapy response capability.*
- `Mission-related:Processing` — `irispy/io/*` implements the IRIS level-2 product layout (raster/SJI/AUX extensions, `TDESC`/`TDET`/`TWMIN`/`TWMAX` keywords, `OBSID`+`STARTOBS` observation grouping, V34 handling, `SDO.tar.gz` and `_raster.tar.gz` archives).
- `Mission-related:Science Data Processing` — the package's purpose is turning IRIS level-2 science data products into calibrated, coordinate-aware science-ready cubes (`docs/index.rst`, `docs/iris.rst` "IRIS Data Level Definitions").

**Models and Simulations**
- `Models and Simulations` — parent.
- `Models and Simulations:Forward-Fitting` — `irispy/utils/utils.py::gaussian1d_on_linear_bg` is a public `astropy.modeling` `custom_model` supplied for spectral-line fitting; `examples/analysis/01_spectral_fitting.py` and `07_mg_ii_two_gaussian_fitting.py` fit single/double Gaussian + constant models to IRIS spectra with `LMLSQFitter`/`TRFLSQFitter`/`parallel_fit_dask`; `density_diagnostic` inverts observed line ratios against theoretical CHIANTI/fiasco ratio curves.
- `Models and Simulations:Instrument Response` — `get_latest_response(observation_time)` computes the time-dependent instrument throughput model (least-squares exponential-decay throughput fits, spline interpolation onto the observed wavelength grid).
- `Models and Simulations:Observatory/Instrument Models` — as above, the IRIS effective-area model built from optical-element transmission products.

**Considered and excluded (audit trail):**
- `Data Processing and Analysis:File Format Conversion` — `SJICube.to_maps()` converts *objects* (cube → `sunpy.map.Map`), not files; the only file writing in the repo is MP4 movies and test-fixture generation. Excluded.
- `Data Processing and Analysis:Energy Spectra` — irispy handles UV *wavelength* spectra, not particle energy spectra. Excluded.
- `Data Processing and Analysis:Wavelet Analysis`, `:Spectrogram` (as FFT/STFT), `:ML/AI`, `:Plasma Moments`, `:Pitch Angle Distributions`, `:Data Assimilation`, `:Packet Decommutation`, `:Field-line Tracing` — no corresponding code. (`calculate_moments` computes *spectral* moments of a line profile, not plasma velocity-distribution moments.) Excluded.
- `Data Visualization:3D Graphics`, `:Web-Based`, `:Orbit Plots`, `:Hodograms`, `:Spacecraft Formation Plots` — no corresponding code. Excluded.
- `Mission-related:Ingest`, `:Distribution/Access`, `:Operations`, `:Monitoring`, `:Inventory`, `:Instrumentation`, `:Packet Decommutation`, `:System Testing`, `:Archive`, `:Orchestration`, `:Infrastructure as Code` — irispy is a downstream analysis library, not part of the IRIS ground system/pipeline. Excluded.
- `Models and Simulations:MHD`, `:First Principles`, `:Empirical`, `:Forecasting`, `:Theory`, `:Data Guided`, `:Physics-Based`, `:ML/AI` — no solver or physical model implemented; the theoretical line-ratio curves come from fiasco/CHIANTI, not from irispy. Excluded.
- `Servers and Environments` and all its subcategories — no server, container, or HPC component (dask is used for out-of-core arrays only). Excluded.

### 5. Related Region (MANDATORY)
- Solar Environment
- Chromosphere
- Corona

*Source note: `Solar Environment` is retained because all irispy functionality is solar. `Chromosphere` is supported directly by the IRIS mission statement and passband description: `docs/iris.rst:11` says the mission studies mass and energy flow through the chromosphere and transition region, and `docs/iris.rst:14` says the passbands are focused on those regions. `Corona` is supported by the same passband description, which explicitly includes light coverage of the corona (`docs/iris.rst:14`), and by the documented 4,500 K to 10 MK spectral-line coverage (`docs/iris.rst:42,52`).*
*The finer Region values were previously deferred solely because the agent documentation exposed only a five-value list, even though the dossier already recognized that they described IRIS more precisely. That procedural premise was falsified on 2026-08-25: the Region vocabulary is flat, so `Solar Environment` does not imply the finer rows, and the user approved adding `Chromosphere` and `Corona`. `Photosphere` remains considered and declined because the evidence identifies photospheric wavelength-calibration lines (`docs/tutorial/calibration.rst:12`) and a Mg II wing passband (`docs/iris.rst:69`), not the photosphere as an IRIS science target. `Solar Interior` remains excluded because no repository source supports sub-photospheric diagnostics.*

### 6. Authors (MANDATORY)

The author list is supported by repository, Zenodo/DataCite and ORCID evidence, with identities matched by ORCID and affiliations resolved by ROR.

> **Author identity history.**
>
> - The author previously recorded only as `juanms` is **Juan Martínez-Sykora**, now carrying ORCID `https://orcid.org/0000-0002-0333-5717`, with his Lockheed Martin Solar and Astrophysics Laboratory and Bay Area Environmental Research Institute affiliations recorded.
> - The Rosseland Centre for Solar Physics, University of Oslo affiliation now carries its verified ROR `https://ror.org/01xtthb56`. This organization is shared with the SunPy entry, which is correctly identified by the same ROR.
> - **IRIS Instrument Team @ LMSAL** is an approved author. No ROR exists for the team or for LMSAL, so it is recorded without an identifier.
>
> The intended public author order is **Freij, Martínez-Sykora, Pereira, IRIS Instrument Team @ LMSAL** — the organizational author is placed last by curatorial decision, preserving the established order of the human authors while still crediting the team.

**Author 1 — Nabil Freij**
- **Author Identifier:** https://orcid.org/0000-0002-6253-082X
- **Affiliation:**
  - Bay Area Environmental Research Institute — https://ror.org/024tt5x58
  - Lockheed Martin Solar and Astrophysics Laboratory — *(no ROR record exists; searched ror.org for "Lockheed Martin Solar and Astrophysics Laboratory" — only generic Lockheed Martin country entities returned)*
  - SETI Institute — https://ror.org/02dxgk712

*Source note: corroborated by `pyproject.toml` authors, 187 of 213 commits (`nabil.freij@gmail.com`, `freij@baeri.org`), GitHub profile `nabobalis` ("Research Scientist in Solar Physics", company "SETI Institute & LMSAL (@LM-SAL)"), and Zenodo/DataCite creator affiliation "SETI Institute & LMSAL (@LM-SAL)".*

**Author 2 — Juan Martínez-Sykora**
- **Author Identifier:** https://orcid.org/0000-0002-0333-5717
- **Affiliation:**
  - Lockheed Martin Solar and Astrophysics Laboratory — *(no ROR record; see above)*
  - Bay Area Environmental Research Institute — https://ror.org/024tt5x58

*Source note / rationale: this author was previously recorded only as `juanms`, which is a GitHub display name rather than a personal name. Resolution chain: Zenodo/DataCite creator `juanms` → the only matching repository contributor is GitHub login `jumasy` (4 commits, matching the 4 commits authored by `Juan Martinez Sykora <jumasy1980@gmail.com>` in `git log`), and the GitHub profile of `jumasy` has display name exactly `juanms` — which is what Zenodo's GitHub integration harvested. ORCID `0000-0002-0333-5717` is Juan Martínez-Sykora, confirmed as the solar physicist by 52 works on solar chromosphere/transition-region MHD (e.g. "Shock-induced magnetic reconnection driving Ellerman bomb emission and a spicule"). Affiliations confirmed as Lockheed Martin Solar & Astrophysics Laboratory (Palo Alto) and Bay Area Environmental Research Institute (NASA Research Park) across his 2018–2023 ApJ papers.*
**Author 3 — Tiago M. D. Pereira**
- **Author Identifier:** https://orcid.org/0000-0003-4747-4329
- **Affiliation:**
  - Rosseland Centre for Solar Physics, University of Oslo — https://ror.org/01xtthb56

*Source note: the affiliation previously lacked an identifier. The Rosseland Centre for Solar Physics has no ROR record of its own, so the parent institution's ROR (University of Oslo) is supplied, corroborated by this author's ORCID employment record. Author identity is corroborated by Zenodo/DataCite creator "Tiago M. D. Pereira" and GitHub contributor `tiagopereira` (display name "Tiago M. D. Pereira", "Astrophysicist").*

**Author 4 — IRIS Instrument Team @ LMSAL (organization author)**
- **Author Identifier:** Not found
- **Affiliation:** Not found

*Source note / rationale: listed as the **first** author in `pyproject.toml` (`{ name = "IRIS Instrument Team  @ LMSAL" }`), holds the copyright in `licenses/LICENSE.rst` ("Copyright (c) 2020-2025, IRIS Instrument Team @ LMSAL"), and is the templated author in `.cruft.json` (`author_name: "IRIS Instrument Team"`, `author_email: https://iris.lmsal.com/contact.html`). SoMEF also extracts it as an author. Zenodo/DataCite omit the team because their creator list is derived from GitHub contributors. The canonical spelling `IRIS Instrument Team @ LMSAL` matches the copyright holder in `licenses/LICENSE.rst`; `pyproject.toml` carries the same string with a double space, so the single-spaced LICENSE form is used. Although `pyproject.toml` lists the team first, it is placed last by the settled curatorial decision to preserve the established order of the human authors while still crediting the team. No ROR exists for either "IRIS Instrument Team" or its parent Lockheed Martin Solar and Astrophysics Laboratory, so it is recorded without an identifier. An expanded form — "Interface Region Imaging Spectrograph Instrument Team at the Lockheed Martin Solar and Astrophysics Laboratory" — was considered and rejected because it is not a name the project itself uses.*

### 7. Software Name (MANDATORY)
irispy

*Source note: matches the repository name, `README.rst` ("``irispy`` is a library…"), `docs/index.rst`, and `pyproject.toml` `[tool.setuptools] provides = ["irispy"]`. The PyPI/conda-forge **distribution** name is `irispy-lmsal` (to avoid a name clash), but README and docs state the package "is imported as ``irispy`` and is referred to as ``irispy`` in the documentation". `irispy` is therefore the correct software name; the distribution name is recorded in the Description instead.*

### 8. Description (MANDATORY)

irispy is a library that provides the tools to read in and analyze data from Interface Region Imaging Spectrograph (IRIS). IRIS is a NASA Small Explorer satellite whose 20 cm telescope feeds a high-frame-rate ultraviolet imaging spectrograph, observing the solar chromosphere and transition region (with lighter coverage of the corona) in far-ultraviolet and near-ultraviolet passbands at about 0.33 arcsecond spatial resolution and roughly 1 second cadence. irispy provides classes for handling both IRIS slit-jaw imager (SJI) images and spectrograph (SG) raster observations, linking each observation to its measurement uncertainties, physical units, a mask marking unreliable or unphysical pixels, World Coordinate System transformations describing position, wavelength and time, and the full IRIS metadata. It reads IRIS level 2 SJI and raster FITS files, including gzipped files, _raster.tar.gz archives and the IRIS-aligned SDO/AIA data cubes distributed with each observation by the IRIS team, and can load an entire observation with a single call. Analysis and calibration capabilities include exposure-time correction and radiometric calibration between data number, photons and physical radiance units using the time-dependent IRIS effective-area response, cosmic-ray and dust-artefact removal, spectral moment maps, red-blue asymmetry maps, electron-density diagnostics from line ratios, decoding of IRIS OBS IDs into human-readable observing descriptions, IRIS-specific plotting and animation, and wobble movie generation. The package assumes the IRIS level 2 data products, which are the recommended science product; level 1 data must first be processed with the SolarSoft IDL calibration routines. Note that the package is distributed on PyPI and conda-forge as irispy-lmsal to avoid a name clash, but is imported and referred to as irispy.

*Source note / rationale: the live HSSI description is a single 121-character sentence identical to the concise description, which does not meet this field's stated purpose ("sufficiently detailed to provide the potential user with information to determine if the software is useful to their work… what the software does, why to use it, assumptions it makes"). The submitted sentence is preserved verbatim as the opening; everything appended is drawn from primary sources: `docs/index.rst` (classes, uncertainties/units/mask/WCS/metadata, calibration routines), `docs/iris.rst` (mission, telescope, passbands, resolution/cadence, level definitions and the level 1 caveat), `README.rst` (NASA-funded Small Explorer, the `irispy-lmsal` naming warning), `irispy/io/utils.py::read_files` (whole-observation reading, tar and SDO archive handling), `CHANGELOG.rst` 0.7.0 and the corresponding modules (`utils/moments.py`, `utils/red_blue.py`, `utils/density.py`, `utils/cosmic_rays.py`, `utils/dust.py`, `utils/spectrograph.py`, `utils/response.py`, `utils/wobble.py`, `obsid.py`). This is an evidence-backed completeness improvement, not a stylistic rewrite.*
*Formatting note: written as plain text with no markdown inline-code backticks because HSSI stores `description` as a plain-text field and would display the backticks literally.*

### 9. Concise Description (OPTIONAL)
irispy is a library that provides the tools to read in and analyze data from Interface Region Imaging Spectrograph (IRIS).

*Source note: 121 characters, within the 200-character limit. This is also the first line of `README.rst`, so it is both the original submitter's wording and the project's own summary, kept verbatim as the preview.*

### 10. Publication Date (RECOMMENDED)
2022-01-21

*Source note / rationale: the previous HSSI value, 2025-08-28, is exactly the release date of v0.4.0 rather than the date of first publication. This field is defined as "Date of first broadcast/publication… Used for the initial version of the software". The first public release is v0.1.0: git tag `v0.1.0` dated 2022-01-21 ("Releasing version v0.1.0") and PyPI `irispy-lmsal` 0.1.0 uploaded 2022-01-21T18:09:22Z. A pre-release, 0.1.0rc1, was uploaded 2021-11-09; the first non-prerelease publication is used because a release candidate is not normally considered published.*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Source note: the persistent identifier is a Zenodo concept DOI obtained through the GitHub–Zenodo workflow; DataCite reports `publisher: "Zenodo"`.*

### 12. Version (RECOMMENDED)
- **Version Number:** v0.7.0
- **Version Date:** 2026-05-07
- **Version Description:** New features: irispy.utils.dust.remove_dust and SJICube.remove_dust to repair dust-darkened pixels in IRIS slit-jaw images; remove_cosmic_rays methods for SJI and raster cubes with rsliding and astroscrappy backends; spectral moment calculation for spectrogram cubes; red-blue asymmetry maps; and IRIS density diagnostics from line ratios (irispy.utils.density.density_diagnostic, map_ratio_to_quantity). Bug fixes include gWCS timestamp handling, preservation of basic_wcs when slicing SJICube, radiometric calibration of sliced raster cubes, raster file-list reading, and edge cases in coordinate preservation, bad-pixel masking and memory use. Documentation adds an ITN26-style tutorial and new examples for astroscrappy spike removal, dust removal, and double-Gaussian Mg II k fitting.
- **Version PID:** https://doi.org/10.5281/zenodo.20073073

*Source note / rationale: live HSSI stores v0.4.0 (rendered by the view API as `irispy - v0.4.0`; the bare stored value is used here — no `<software> - ` prefix is carried into this file). v0.7.0 is the current authoritative release: git tag `v0.7.0` dated 2026-05-07 ("Releasing version v0.7.0"), PyPI `irispy-lmsal` 0.7.0 uploaded 2026-05-07T18:20:53Z, Zenodo record 20073073 `version: "v0.7.0"`, `publication_date: 2026-05-07`, and DataCite `version: "v0.7.0"` with `dateType: Issued` 2026-05-07. The `v` prefix follows both the git tag and the Zenodo/DataCite version string, and matches the convention of the existing stored value. Version description condensed from `CHANGELOG.rst` section "0.7.0 (2026-05-07)". Version PID is the version-specific Zenodo DOI (`links.self_doi`), distinct from the concept DOI in Field 2. The Version Description is written as plain text with no markdown backticks, for the same reason as Field 8.*

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source note: Python 3.x is correct and overwhelmingly dominant — GitHub linguist reports Python 334,565 bytes, Shell 673 bytes, IDL 594 bytes; `pyproject.toml` requires Python >= 3.12 with classifiers for 3.12/3.13/3.14, and `.cruft.json` records `use_compiled_extensions: "n"` (pure Python, `py3-none-any` wheel).*

*Previous values `IDL` and `Other` are deliberately excluded. The only IDL in the repository is the single 594-byte SolarSoft test-data generator `irispy/data/test/get_cali_test_data.pro`, which is neither shipped nor executed by the package; "Other" corresponded to two CircleCI shell scripts (`.circleci/codecov_upload.sh`, `.circleci/early_exit.sh`, 673 bytes combined), which are CI plumbing rather than software functionality. Field 13 asks for "the most important languages for the software," and neither meets that bar against 334,565 bytes of pure Python. The SSWIDL calibration lineage that motivated the original `IDL` value is preserved where it belongs — Field 29 records the SolarSoft IRIS package as Related Software, and Fields 4/18 record the IDL-artifact reading (`scipy.io.readsav`) irispy performs.*

### 14. Reference Publication (RECOMMENDED)
Not found

*Source note: there is no software paper for irispy — no JOSS submission, no CITATION.cff, no `codemeta.json`, and no "how to cite" section in `README.rst` or the documentation. The IRIS **instrument** paper is recorded under Related Publications (Field 27) instead, since it describes the instrument rather than the software.*

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

*Source note: the license name is confirmed by `licenses/LICENSE.rst` (three-clause BSD text, "Copyright (c) 2020-2025, IRIS Instrument Team @ LMSAL"), `pyproject.toml` (`license-files = ["licenses/LICENSE.rst"]`, classifier "License :: OSI Approved :: BSD License"), and `.cruft.json` (`license: "BSD 3-Clause"). The URI is the SPDX BSD-3-Clause identifier.*
*Conflict noted and deliberately rejected: DataCite/Zenodo report `rightsList` "Creative Commons Attribution 4.0 International" (`cc-by-4.0`) for this DOI. That is a Zenodo deposit default and contradicts the repository's own LICENSE; the repository license is authoritative. Do not autofill the license from the DOI for this entry.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

The keywords use their stored lowercase forms; HSSI renders those forms in title case when displaying them.

- iris
- lmsal
- nasa
- science
- solar
- solar physics
- spectra

- chromosphere — `docs/iris.rst`: IRIS is "focused on the chromosphere and transition region"; `docs/index.rst`.
- transition region — same source.
- ultraviolet — `README.rst` "high-frame-rate ultraviolet imaging spectrometer"; `docs/iris.rst` FUV1/FUV2/NUV passbands. (The existing vocabulary term `extreme ultraviolet` is deliberately *not* used: IRIS observes FUV/NUV, not EUV.)
- spectroscopy — existing HSSI vocabulary term; IRIS spectra analysis is the package's core purpose.
- spectrograph — existing HSSI vocabulary term; `irispy/spectrograph.py`, `irispy/io/spectrograph.py`, IRIS SG data products.
- calibration — existing HSSI vocabulary term; `irispy/utils/spectrograph.py::radiometric_calibration`, `irispy/utils/response.py`.
- slit-jaw imaging — `irispy/sji.py`, `irispy/io/sji.py`, `docs/iris.rst` Table 2 (SJI channels).

*Source note: `iris`, `lmsal`, `nasa`, `science`, `solar`, `solar physics`, and `spectra` come from `pyproject.toml` `keywords`. The remaining science keywords are drawn from the package's own documentation; existing controlled terms are reused where available to avoid near-duplicates.*
*PyHC note: irispy is a PyHC **community** package, registered in `_data/projects.yml` as `irispy-lmsal` with PyHC facet keywords `["solar", "specific", "data_analysis", "spectra", "fits", "time", "coordinates", "plotting", "multidimensional"]`. These are PyHC's internal facets rather than science keywords, so they are used to corroborate other fields (functionality, formats) rather than copied here. The PyHC entry's `code` (`github.com/LM-SAL/irispy-lmsal`) and `docs` (`irispy-lmsal.readthedocs.io`) URLs are stale relative to the current repository and documentation URLs used in Fields 3 and 24.*

### 17. Data Sources (OPTIONAL)

- HTTP/HTTPS Directories — `irispy/data/_sample.py` downloads IRIS sample data over HTTPS from three mirrors (`github.com/sunpy/data/raw/main/irispy-lmsal/`, `github.com/sunpy/sample-data/raw/master/irispy-lmsal/`, `data.sunpy.org/irispy-lmsal/`); every gallery example retrieves level-2 files by direct URL from `www.lmsal.com/solarsoft/irisa/data/level2_compressed/...` via `pooch.retrieve`.
- Observatory/Mission-specific — the primary documented source is the IRIS mission's own archive and search tool: `docs/tutorial/acquiring_data.rst` "IRIS data search website" (`iris.lmsal.com/search/`), `README.rst` "The data is publicly available" (`iris.lmsal.com/data.html`), and the `www.lmsal.com/solarsoft/irisa/data/level2_compressed/` level-2 tree used throughout the examples. Cross-listed with Related Observatories per this field's instructions.
- The Virtual Solar Observatory. — *(the trailing period is part of the controlled value)* — `docs/tutorial/acquiring_data.rst` devotes a section to searching and fetching IRIS data through `sunpy.net.Fido` with `a.Instrument.iris`, with worked `VSOClient` output. The value is included because irispy documents this as a supported acquisition path and depends on SunPy, even though irispy does not implement its own VSO client.

**Considered and excluded:** CDAWeb, OMNIWeb, SSCWeb, HAPI, das2, TAP, VirES, S3/Cloud-aware, FTP/FTPS Directories — no client, URL, or documentation reference for any of these.

### 18. Input File Formats (RECOMMENDED)

- FITS — `astropy.io.fits` throughout `irispy/io/sji.py`, `irispy/io/spectrograph.py`, `irispy/io/utils.py` (`fits_info`, `_get_simple_metadata`), `irispy/utils/wobble.py`; IRIS level-2 SJI and raster FITS are the package's primary input.
- IDL.sav — `irispy/utils/response.py` reads the shipped IRIS response file with `scipy.io.readsav(ROOTDIR / "iris_sra_c_20231106.geny", python_dict=True)`; tests read `.sav` files (`fit_iris_xput_input.sav`, `input_calibration.sav`, `iris_response_2025_08_05T22_25_04_723.sav`) through the same IDL SAVE reader.
- csv — `irispy/obsid.py` reads the shipped IRIS OBS-ID tables `data/v{34,36,38,40}-table10.csv` and `-table2000.csv` with `pandas.read_csv`.
- Other — gzip-compressed FITS (`*.fits.gz`, e.g. `SJI_1330_t000.fits.gz`) and tar archives handled by `irispy/io/utils.py::_extract_tarfile` (`*_raster.tar.gz` IRIS raster bundles and `*SDO.tar.gz` IRIS-aligned SDO/AIA bundles).

**Considered and excluded:** CDF, HDF5, netCDF3/4, Zarr, ISTP-Compliant, ascii, JSON — no reader. (`irispy/tests/figure_hashes_*.json` is a pytest-mpl figure-hash fixture, not a user data input.)

### 19. Output File Formats (RECOMMENDED)

- Other — MP4 (H.264) video files written by `irispy/utils/wobble.py::generate_wobble_movie` via `matplotlib.animation.FFMpegWriter` (filename pattern `{TDESC1}_{date}_wobble.mp4`). This is the only user-facing file output in the package.

*Source note / audit trail: FITS is deliberately **not** listed as an output. The only `fits.writeto` calls are in test infrastructure (`irispy/conftest.py` fake-data fixtures and `irispy/data/test/compress.py`, a maintainer script for shrinking test files), not in the public API. Figures are returned as matplotlib axes for the user to save, not written by irispy.*

### 20. Operating System (RECOMMENDED)

- Linux
- Mac
- Windows

*Source note: `.github/workflows/ci.yml` runs the test matrix on `windows: py312`, `macos: py313`, `linux: py312-oldestdeps`, `linux: py314-devdeps` plus `linux: py314` core, with ffmpeg installed via choco/brew/apt respectively. `docs/tutorial/installation.rst` gives per-platform install instructions for Linux, Windows and Mac. `pyproject.toml` also carries the classifier "Operating System :: OS Independent" and `platforms = ["any"]`; the three concrete CI-verified platforms are recorded rather than the generic value.*

### 21. CPU Architecture (RECOMMENDED)

- x86-64
- Apple Silicon arm64
- Linux aarch64 or arm64
- ppc64le

*Source note: `docs/tutorial/installation.rst` explicitly lists the supported install targets — Linux x86-64 / aarch64 / ppc64le, Windows x86-64, and Mac arm64 (Apple Silicon) / x86-64. Consistent with the package being pure Python: `.cruft.json` `use_compiled_extensions: "n"` and the PyPI distribution `irispy_lmsal-0.7.0-py3-none-any.whl`. GPU is not listed (no GPU code path).*

### 22. Related Phenomena (OPTIONAL)

- Solar Flares — `docs/iris.rst`: "IRIS data is also used for a wide range of other science topics including: solar flares…"; the spectral lines "cover temperatures from 4,500 K to 10 MK… possibly 10 MK under flaring conditions"; `irispy/obsid.py` decodes IRIS flare observing programs ("Flare linelist 1").
- Solar Corona — `docs/iris.rst`: IRIS observations include "light coverage of the corona"; FUV1 covers log T 3.7–7.0 (`docs/iris.rst` Table 1).
- Coronal Heating — the IRIS mission statement quoted in `docs/iris.rst`: "to understand how the solar atmosphere is energized and to understand how mass and energy flows through the chromosphere and transition region".

**Considered and excluded:** X-ray emission (IRIS is a UV instrument); Coronal Mass Ejections, Solar Wind, Geomagnetic Storms (no supporting functionality or documentation claim — the docs mention prominences, sunspots, coronal rain and spicules, none of which are in the vocabulary).

### 23. Development Status (RECOMMENDED)
Active

*Source note / rationale: repostatus.org "Active" = "reached a stable, usable state and is being actively developed". Evidence: four releases in the 12 months before extraction (v0.5.0 2025-10-06, v0.6.0 2026-01-26, v0.7.0 2026-05-07, plus v0.4.0 2025-08-28), most recent commit 2026-07-10 on `main`, 213 commits total, weekly scheduled CI (`cron: '0 7 * * 3'`), active towncrier changelog fragments in `changelog/`, and publication on PyPI and conda-forge with stable Read the Docs. `pyproject.toml` carries the PyPI trove classifier "Development Status :: 3 - Alpha", which is a distinct vocabulary from repostatus and does not override the repository activity evidence for `Active`.*

### 24. Documentation (RECOMMENDED)
https://irispy.readthedocs.io/en/stable/

*Source note: confirmed by `pyproject.toml` `urls.Documentation`, PyPI `project_urls.Documentation`, `README.rst` ("Documentation is hosted on Read the Docs"), and SoMEF. Installation instructions live under this URL at `docs/tutorial/installation.rst`. The PyHC registry's `irispy-lmsal.readthedocs.io` value is stale.*

### 25. Funder (OPTIONAL)
Not found

*Source note: this field is deliberately left empty. The repository contains no package-level funding acknowledgement — no funding section in `README.rst`, the documentation, or `pyproject.toml`, and the Zenodo/DataCite record's `fundingReferences` is empty.*

*__DECISION RECORD (user-approved 2026-07-29): NASA was considered and deliberately NOT added.__ A NASA funder row (`National Aeronautics and Space Administration`, `https://ror.org/027ka1x80`) was proposed on the strength of irispy being the IRIS instrument team's own library for a NASA-funded mission (`README.rst` "IRIS is a NASA-funded Small Explorer…"; `docs/iris.rst` "IRIS is a NASA Small Explorer (SMEX) satellite"; `pyproject.toml` author "IRIS Instrument Team  @ LMSAL" and keyword `NASA`), and cross-entry precedent does exist — live HSSI's aiapy entry records that exact ROR alongside `Science and Technology Facilities Council`. The user's decision is that mission-level funding is too indirect to attribute to the software library itself: the available evidence funds the IRIS mission and its instrument team, not this package. Recorded here so the reasoning is not re-litigated on a future refresh, and so the empty value is understood as a considered choice rather than a gap in extraction.*

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

*Source note: no award title or grant number appears anywhere in the repository, documentation, PyPI metadata, or the Zenodo/DataCite record (`fundingReferences` is empty).*

*__DECISION RECORD (user-approved 2026-07-29): an evidenced award candidate was considered and deliberately NOT added__, consistent with the Field 25 decision to omit mission-level funding. The IRIS instrument paper cited in Field 27 (De Pontieu et al. 2014, `10.1007/s11207-014-0485-y`) states verbatim in its Acknowledgements, verified directly against the Springer article of record: "This work is supported by NASA under contract **NNG09FA40C** and the Lockheed Martin Independent Research Program." That is a real, numbered NASA contract, and it would have supported an award entry ("NASA contract for the Interface Region Imaging Spectrograph (IRIS) mission", number `NNG09FA40C`) had mission-level funding been accepted. It funds the IRIS mission, not this software package, so it is omitted along with the Field 25 funder. Recorded here — including the contract number — so the evidence is preserved for any future refresh that revisits the mission-vs-package question.*

*Also named in the same acknowledgement and likewise omitted: the Lockheed Martin Independent Research Program (an internal LM program, no ROR, no award number) and the Norwegian Space Centre / ESA PRODEX contract (funds the Svalbard data downlink, i.e. mission operations, further still from the software). An earlier, weaker candidate ("NASA Small Explorer (SMEX) program support…") was rejected outright as an unsourced paraphrase of the mission type rather than a stated award.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- https://doi.org/10.1007/s11207-014-0485-y — De Pontieu, B., Title, A. M., Lemen, J. R., Kushner, G. D., Akin, D. J., et al. (2014). The Interface Region Imaging Spectrograph (IRIS). *Solar Physics*, 289, 2733–2779.
  *Source note: the IRIS instrument paper, linked prominently from `README.rst` ("For more information see the instrument paper which is available online for free") and cited directly in the code as the source of the detector constants irispy applies — `irispy/utils/constants.py`: "Source: IRIS instrument paper (https://link.springer.com/article/10.1007/s11207-014-0485-y)" for `DETECTOR_GAIN`, `DETECTOR_YIELD`, `READOUT_NOISE`. It describes the instrument rather than the software, which is why it is here rather than in Field 14; it is the reference any user of irispy's calibrated output needs.*
- https://doi.org/10.3847/1538-4357/ab9014 — Yu, K., Li, Y., Ding, M. D., Li, D., Zhou, Y.-A., & Hong, J. (2020). IRIS Si IV Line Profiles at Flare Ribbons as Indications of Chromospheric Condensation. *The Astrophysical Journal*.
  *Source note: cited as the methodological reference for irispy's spectral-moment implementation — `irispy/utils/moments.py` References section links "arXiv:2005.02029, Section 3.1", which resolves to this DOI. An IRIS science paper whose method irispy implements; flagged as a lower-confidence entry than the instrument paper.*
- https://doi.org/10.1088/0004-637X/772/2/90 — Leenaarts, J., Pereira, T. M. D., Carlsson, M., Uitenbroek, H., & De Pontieu, B. (2013). The Formation of IRIS Diagnostics. II. The Formation of the Mg II h and k Lines in the Solar Atmosphere. *The Astrophysical Journal*, 772, 90.
  *Source note: the diagnostic basis for irispy's Mg II h/k analysis. `examples/analysis/07_mg_ii_two_gaussian_fitting.py` states the k2v/k2r peak-intensity, asymmetry and peak-separation maps it builds "are motivated by the Mg II h/k diagnostics described by Leenaarts et al. (2013)", which underpins `irispy/utils/red_blue.py::calculate_red_blue_asymmetry` as applied to Mg II. Included on the same "science paper whose method irispy implements" basis as Yu et al. (2020). DOI verified to resolve via CrossRef.*
- https://doi.org/10.1088/2041-8205/780/1/L12 — Dudík, J., Del Zanna, G., Dzifčáková, E., Mason, H. E., & Golub, L. (2014). Solar Transition Region Lines Observed by the Interface Region Imaging Spectrograph: Diagnostics for the O IV and Si IV Lines. *The Astrophysical Journal Letters*, 780, L12.
  *Source note: the reference irispy's O IV density diagnostic reproduces. `examples/analysis/06_oiv_density_diagnostics.py` states "We will reproduce aspects of the top row of Fig. 4 from Dudik et al. (2014)" and links this DOI, exercising `irispy/utils/density.py::density_diagnostic`. Same inclusion basis as above. Bibliographic details verified against CrossRef (title, all five authors, volume 780, page L12); cited as 2014 per the journal volume and the repository's own reference, though CrossRef records online publication 2013-12-13.*

**Considered and excluded (audit trail):** `irispy/utils/moments.py` also cites "Færder et al. (2024), ApJ, Appendix C" but links `https://iopscience.iop.org/article/10.3847/1538-4357/ac4223`, which is actually Cheung, Martínez-Sykora et al. (2022), "Probing the Physics of the Solar Atmosphere with the Multi-slit Solar Explorer (MUSE). II. Flares and Eruptions". Because the citation text and the linked DOI disagree, no DOI is recorded for it — this looks like an upstream documentation bug worth reporting to the maintainers. The IRIS Technical Notes referenced in the docs (ITN 1, ITN 11, ITN 26, ITN 32) have no DOIs, and `Calabretta & Greisen 2002` is cited in `docs/known_issues.rst` only for a WCS equation.

### 28. Related Datasets (OPTIONAL)

- https://doi.org/10.48322/k079-z133 — IRIS Level 2 Calibrated Images and Spectra Data (`spase://NASA/NumericalData/IRIS/Level_2/PT1S`).
  *Source note: the dataset irispy is built to read. `irispy/io/sji.py::read_sji_lvl2` and `irispy/io/spectrograph.py::read_spectrograph_lvl2` parse exactly these level-2 SJI and raster products; `docs/iris.rst` "we strongly recommend that everyone use the Level 2 data products".*
- https://doi.org/10.48322/agkq-fv14 — Co-aligned Interface Region Imaging Spectrograph (IRIS) and Solar Dynamics Observatory (SDO) Atmospheric Imaging Assembly (AIA) Observations (`spase://NASA/NumericalData/IRIS/Level_2/IRIS_SDO`).
  *Source note: irispy has a dedicated reader path and class for these — `read_files` recognises `*SDO.tar.gz` bundles and `INSTRUME` values starting with `AIA`, and `irispy.sji.AIACube` represents them; `examples/how_to/05_open_aia_cubes.py` ("Open the IRIS Aligned AIA Cubes").*

**Considered and excluded (audit trail):** IRIS Level 1 data (https://doi.org/10.48322/gdjv-sn12) — irispy does not read level 1; `docs/iris.rst` states level 1 "**MUST** be passed through the calibration routines `iris_prep.pro`" first. Co-aligned IRIS + Hinode (https://doi.org/10.48322/55gv-bg80) and coordinated IRIS + SST (https://doi.org/10.48322/1mf1-nb89) — mentioned in `docs/tutorial/acquiring_data.rst` as searchable co-aligned products, but `read_files` only recognises IRIS/SJI/AIA `INSTRUME` values and `SDO.tar.gz` archives, so these are not supported.

### 29. Related Software (OPTIONAL)

- https://hesperia.gsfc.nasa.gov/ssw/iris/idl/ — SolarSoft (SSWIDL) IRIS analysis package.
  *Source note: the predecessor and functional counterpart irispy is explicitly written against. `irispy/utils/response.py`: "Goal is to replicate the base functionality of the IDL routine ``iris_get_response.pro`` in the SSWIDL package" and "…``fit_iris_xput.pro``… but without the optional keyword argument"; `irispy/utils/spectrograph.py`: "designed to do the same as `iris2/iris_calib_spectrum.pro`… The calibration output has been confirmed to provide the same results as those provided by the SolarSoft IDL routine `IRIS_CALIB`"; `docs/iris.rst` points to `iris_prep.pro` for level 1 → 1.5 processing; the shipped `irispy/data/test/get_cali_test_data.pro` generates the IDL reference data used to validate irispy's calibration against SSWIDL. No DOI or public VCS repository; the linked SSW IRIS IDL tree is the location cited by irispy itself.*

**Considered and excluded (audit trail):**
- Tier A generic infrastructure, excluded regardless of dependency status: numpy, scipy, pandas, matplotlib, setuptools, setuptools-scm, wheel, pooch, tqdm, pytest / pytest-astropy / pytest-mpl, sphinx and all sphinx extensions.
- `dask` — a hard dependency and genuinely exercised (`irispy/utils/cosmic_rays.py` branches on `dask.array` inputs; `parallel_fit_dask` in the fitting examples), but parallel/lazy arrays are generic infrastructure that would be equally at home outside science. Excluded from both fields.
- `rsliding` — the default cosmic-ray backend (`rsliding.SlidingSigmaClipping`), but it is a general sliding-window sigma-clipping/mean/median/stddev utility (PyPI summary), i.e. generic numerical infrastructure. Excluded.
- `mpl-animators` — `IRISArrayAnimatorWCS` subclasses `mpl_animators.ArrayAnimatorWCS`, but it is a general matplotlib animation helper rather than a domain tool. Excluded.
- `asainz-solarphysics/IRIS-LMSALpy` — a nominally similar-purpose IRIS Python effort, but a stub (no README, last push 2018, 0 stars). Not distinguishing; excluded.
- `sunkit-instruments` — similar in spirit (SunPy-affiliated instrument-specific tools) but has no relationship to irispy in code or docs. Excluded.
- Packages that met the Field 30 bar (sunpy, ndcube, sunraster, astropy, gwcs, dkist, fiasco, aiapy, sunkit-image, astroscrappy) are listed there rather than duplicated here.

### 30. Interoperable Software (OPTIONAL)

- https://github.com/sunpy/sunpy — `irispy.sji.SJICube.to_maps()` converts IRIS cubes into `sunpy.map.Map` / `MapSequence` objects (documented adapter API, used in `examples/coalign/01_coalign_iris_aia.py`); readers construct headers with `sunpy.map.header_helper.make_fitswcs_header` and coordinate frames with `sunpy.coordinates` (`Helioprojective`, `HeliographicStonyhurst`, `SphericalScreen`, `get_body_heliographic_stonyhurst`); SJI colour tables come from `sunpy.visualization.colormaps.color_tables.iris_sji_color_table`; sample data uses `sunpy.util.parfive_helpers.Downloader`.
- https://github.com/sunpy/ndcube — shared NDCube data model: `irispy.spectrograph.RasterCollection` subclasses `ndcube.NDCollection`, `read_files` returns an `NDCollection`, `irispy.visualization.IRISPlotter` subclasses `ndcube.visualization.mpl_plotter.MatplotlibPlotter`, and `SpectrogramCube._fits_wcs` uses `ndcube.wcs.tools.unwrap_wcs_to_fitswcs`.
- https://github.com/sunpy/sunraster — shared spectrogram data model: `irispy.spectrograph.SpectrogramCube` and `irispy.sji.SJICube` subclass `sunraster.SpectrogramCube`, and `SpectrogramCubeSequence` subclasses `sunraster.SpectrogramSequence`, so IRIS cubes are usable anywhere sunraster objects are. (Lineage note: `github.com/sunpy/irispy` now redirects to `sunpy/sunraster` — sunraster is the generalised descendant of the original irispy, and this package is the IRIS-specific library built on top of it.)
- https://github.com/astropy/astropy — the public interchange types are astropy's: cube data carry `astropy.units` `Quantity` units (`irispy/utils/constants.py` defines `DN_IRIS_*` units and `RADIANCE_UNIT`), `astropy.time.Time` coordinates, `astropy.coordinates.SkyCoord`, `astropy.wcs.WCS`, and `astropy.nddata.StdDevUncertainty`; `irispy.utils.gaussian1d_on_linear_bg` is a public `astropy.modeling` `custom_model` intended to be fit with astropy fitters (`LMLSQFitter`/`TRFLSQFitter` in `examples/analysis/01_spectral_fitting.py` and `07_mg_ii_two_gaussian_fitting.py`).
- https://github.com/spacetelescope/gwcs — `irispy/io/sji.py::_create_gwcs` builds and returns a `gwcs.WCS` (with `gwcs.coordinate_frames` `CelestialFrame`/`TemporalFrame`/`CompositeFrame`) that is exposed as `SJICube.wcs`, so IRIS SJI cubes hand a fully-formed gWCS object to any gwcs-aware consumer.
- https://github.com/DKISTDC/dkist — `irispy/io/sji.py` imports `dkist.wcs.models.VaryingCelestialTransform` and `CoupledCompoundModel` and composes them into the IRIS per-exposure gWCS forward transform; DKIST's WCS model objects are embedded in irispy's public WCS.
- https://github.com/wtbarnes/fiasco — `irispy.utils.density.density_diagnostic(..., ion=<fiasco.Ion>)` takes fiasco `Ion` objects and calls `fiasco.line_ratio(ion, numerator, denominator, density_grid)` to build the theoretical curve it inverts; declared as the optional extra `irispy-lmsal[density]`; demonstrated in `examples/analysis/06_oiv_density_diagnostics.py` and covered by `irispy/utils/tests/test_density.py`.
- https://github.com/LM-SAL/aiapy — `examples/coalign/01_coalign_iris_aia.py` and `02_reproject_iris_roll_aia.py` use `aiapy.calibrate.update_pointing` and `aiapy.calibrate.utils.get_pointing_table` to prep the AIA maps that IRIS data are then co-aligned/reprojected against; declared in the `docs` extra. (Also the closest sibling package: same LM-SAL organisation, same sunpy package template, same mission-specific analysis role for SDO/AIA.)
- https://github.com/sunpy/sunkit-image — `examples/coalign/01_coalign_iris_aia.py` passes the `sunpy.map.Map` produced by `SJICube.to_maps()` into `sunkit_image.coalignment.coalign_map`; declared in the `docs` extra; `CHANGELOG.rst` 0.6.0 records "an example to demonstrate co-alignment of IRIS SJI and SDO/AIA images using sunkit-image's ``match_template`` method".
- https://github.com/astropy/astroscrappy — a user-selectable backend of irispy's public API: `remove_cosmic_rays(method="astroscrappy")` hands each frame and mask to `astroscrappy.detect_cosmics` and consumes the cleaned frame (`irispy/utils/cosmic_rays.py`); declared as the optional extra `irispy-lmsal[cosmic-rays]`; demonstrated in `examples/calibration/01_remove_spikes_sg.py` and tested in `irispy/utils/tests/test_cosmic_rays.py`.

*Exclusions are recorded in the Field 29 audit trail above (Tier A generic stack, dask, rsliding, mpl-animators). No entry here rests on "part of the scientific Python ecosystem" or "PyHC membership".*

### 31. Related Instruments (OPTIONAL)

Each instrument is supported directly by the package and carries its canonical SPASE identifier.

- **Instrument Name:** Interface Region Imaging Spectrograph
  **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/IRIS/IRIS
  *Resolution: exactly one `type=1` row matches on name, on abbreviation `IRIS`, and on the identifier path segments `IRIS/IRIS`. Canonical `name` copied verbatim from the matched row. Designed-to-support evidence: the entire package reads, calibrates, models the response of, and visualises this instrument's SJI and SG level-2 data (`irispy/io/sji.py`, `irispy/io/spectrograph.py`, `irispy/utils/response.py`, `irispy/utils/spectrograph.py`, `irispy/obsid.py`, `irispy/meta.py`). The fetched SPASE record confirms the match ("multi-channel imaging spectrograph with a 20 cm UV telescope… spectra along a slit… and slit-jaw images").*
- **Instrument Name:** Atmospheric Imaging Assembly
  **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SDO/AIA
  *Resolution: two instrument entries in HSSI's vocabulary describe this one SPASE resource — the bare `.../SDO/AIA` (name "Atmospheric Imaging Assembly", abbreviation `AIA`) and an `.html` variant whose identifier differs by that suffix, `.../SDO/AIA.html` (name "Atmospheric Imaging Assembly (AIA)"). Because the two identifiers are not identical, the bare identifier is unambiguous; per the `.html` normalisation rule that is the correct entry, and its `name` is copied verbatim. Designed-to-support evidence: irispy has a dedicated `irispy.sji.AIACube` class; `read_sji_lvl2` is documented as reading "a SINGLE level 2 SJI FITS **or the IRIS aligned AIA Cube**" and branches on `INSTRUME` starting with `AIA`; `read_files` extracts `*SDO.tar.gz` AIA bundles; `examples/how_to/05_open_aia_cubes.py`, `examples/coalign/01_coalign_iris_aia.py` and `02_reproject_iris_roll_aia.py` read, co-align and reproject AIA data; the co-aligned IRIS+AIA dataset is listed in Field 28. Cross-entry consistency confirmed: HSSI's existing aiapy entry stores this same instrument as name "Atmospheric Imaging Assembly" with identifier `https://spase-metadata.org/SMWG/Instrument/SDO/AIA` — the bare form used here, so the two entries agree. (The `.html` variant remains a pre-existing duplicate row in the vocabulary for the same SPASE resource, but nothing in HSSI uses its name form.)*

**Considered and excluded (audit trail):**
- IRIS SJI and SG are not listed as separate instruments: SPASE models IRIS as a single instrument (`SMWG/Instrument/IRIS/IRIS`) with both light paths, and there are no sub-instrument rows to expand into.
- Hinode instruments (e.g. XRT, EIS, SOT) — `docs/iris.rst` mentions that level 2/3 formats are "analyzed using tools adapted from Hinode/EIS and SST/CRISP" and `docs/tutorial/acquiring_data.rst` notes co-aligned Hinode cubes are searchable, but `read_files` recognises only IRIS/SJI/AIA `INSTRUME` values and `SDO.tar.gz` archives. Mention only, not designed-to-support. Excluded.
- SST/CRISP — same reasoning as Hinode; a format-lineage remark in `docs/iris.rst`. Excluded.
- SDO/HMI and SDO/EVE — present in the vocabulary but never referenced by irispy. Excluded.
- FITS generally → Field 18 (Input File Formats), not an instrument.

### 32. Related Observatories (OPTIONAL)

Each observatory is supported directly by the package and carries its canonical SPASE identifier.

- **Observatory Name:** Interface Region Imaging Spectrograph
  **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/IRIS
  *Resolution: exactly one `type=2` row matches (name and identifier path segment `IRIS`); `name` copied verbatim. It shares its display name with the instrument row above, which is expected — SPASE names the IRIS mission after its single instrument — and the two are unambiguous because they differ in `type` and identifier. Designed-to-support evidence: irispy is the IRIS mission's own analysis library; `README.rst`, `docs/index.rst`, `docs/iris.rst`; readers stamp `TELESCOP`/`observatory = "IRIS"`; `SJIMeta.observatory`; the mission-specific level-2 archive is cross-listed as `Observatory/Mission-specific` in Field 17 per that field's instruction.*
  *Note: the one `type=2` row whose abbreviation is `AIA` — "Argentine Island Geomagnetic Observatory" (`IUGONET/Observatory/WDC_Kyoto/WDC/AIA`) — is an unrelated abbreviation collision, checked and rejected.*
- **Observatory Name:** Solar Dynamics Observatory
  **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SDO
  *Resolution: exactly one `type=2` row matches on name and on the identifier path segment `SDO`; `name` copied verbatim. Designed-to-support evidence: as for AIA above — `irispy.sji.AIACube`, the `*SDO.tar.gz` reader path in `irispy/io/utils.py::read_files`, `examples/how_to/05_open_aia_cubes.py`, and the two coalign/reproject examples; the co-aligned IRIS+SDO/AIA dataset DOI is recorded in Field 28. Consistent with HSSI's existing aiapy entry, which uses this same observatory row.*

**Considered and excluded (audit trail):**
- Hinode and the Swedish 1 m Solar Telescope — documentation mentions co-aligned/coordinated data products and format lineage only; no reader. Excluded (see Field 31).
- The Virtual Solar Observatory and CDAWeb-style archives — data sources, recorded in Field 17, not observatories.
### 33. Logo (OPTIONAL)
Not found

*Source note: the repository contains no software logo. `docs/_static/images/` holds only `iris_spacecraft.jpg` and `iris_instrument.jpg` (schematic diagrams of the satellite and its optical paths), and the PyHC registry entry for `irispy-lmsal` has no `logo` field. The banner image at `https://raw.githubusercontent.com/LM-SAL/irispy/refs/heads/main/iris_full.jpg` is deliberately excluded: it is a photograph of the IRIS spacecraft rather than a logo for the software.*
