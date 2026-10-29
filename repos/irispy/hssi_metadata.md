# HSSI Metadata Extraction Results

**HSSI Software ID:** 3f058476-5010-48f4-9bd9-e27648d2ecea
**Repository:** https://github.com/LM-SAL/irispy
**Source Revision:** cd8ad59083e883d5a1db661ef56ab81856bf81eb
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-10-29
**Validation Status:** PASS

*Scope note: upstream rewrote the whole history of `LM-SAL/irispy` after this dossier's July 2026 extraction, purging binary test data: no commit of the earlier lineage, the root included, is in the current history, and the release tags were re-pointed to the rewritten commits. The Source Revision above belongs to the earlier lineage; its counterpart in the current history is `888980bef9f12347845108670f819f58ab72a63f`, whose tree differs only by the FITS test files under `irispy/data/test/` and `irispy/data/test/compress.py` that the rewrite removed. By the catalogue maintainer's decision (2026-10-29), this entry describes the recorded release, v0.9.1post1 at tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`, not unreleased work on the default branch: the release's evidence is read at that tag, and capabilities that exist only on the default branch after it are kept as notes to re-check at the next release. Sections that cite the tag were read there; the release history, the repository's activity and external records (Zenodo, PyPI, ADS, ORCID, the PyHC registry, the HSSI vocabularies) were read on 2026-10-28 and 2026-10-29, when the default branch stood at `134c2996b1db3887c9d9337a9338710440b0c1fb`; any other evidence was read at the Source Revision. A clone made before the rewrite shares no history with the current default branch, so release history is read from the current remote's tags, never from tags left in an older clone.*

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

*Source note: confirmed by `git remote -v`, `pyproject.toml` (`urls."Source Code"`), PyPI `project_urls`, and Zenodo `custom["code:codeRepository"]`. The repository was renamed from `LM-SAL/irispy-lmsal` (that path now redirects here), and the PyHC registry still lists the old URL, so the value above is the current repository. The history rewrite noted in the header left the repository at this URL (GitHub reports it unarchived, created 2022-12-27), so it is not a move.*

### 4. Software Functionality (MANDATORY)

*Evidence in this section was read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`. Capabilities that exist only on the default branch after that tag are listed at the end of this section, to be re-checked at the next release.*

**Coordinate Transforms**
- `Coordinate Transforms` — parent of the two entries below.
- `Coordinate Transforms:Mission-Specific` — `irispy/io/sji.py::_create_gwcs` builds a per-exposure IRIS pointing model from the AUX extension (`XCENIX`/`YCENIX` reference coordinates, `PC1_1IX`…`PC2_2IX` rotation matrices) using DKIST's `VaryingCelestialTransform`; `irispy/io/spectrograph.py` builds a FITS `-TAB` WCS from the per-step AUX pointing of rasters and sit-and-stare observations (v0.8.0) and reverses V34 rasters (`revert_v34`); `SJIMeta.satellite_rotation` exposes `SAT_ROT` roll. *At the Source Revision this entry also cited a slit-offset correction from `POFFYFUV`/`POFFYNUV`; v0.8.0 removed it, keeping the Level 2 slit WCS instead of applying the detector offsets a second time.*
- `Coordinate Transforms:Solar` — cubes carry solar frames the user can transform: the `sunpy.coordinates.frames.Helioprojective` celestial frame of the gWCS, exposed as `SJICube.celestial_frame` (v0.9.1); `SGMeta.observer`, the IRIS observer, assumed at Earth, from `sunpy.coordinates.get_earth` (v0.9.1); the readers' Earth-observer ephemeris from `get_body_heliographic_stonyhurst`; `cube.axis_world_coords()` returns solar coordinates; `examples/coalign/02_reproject_iris_roll_aia.py` reprojects IRIS into the SDO/AIA frame.

**Data Processing and Analysis**
- `Data Processing and Analysis` — parent.
- `Data Processing and Analysis:2D Slices` — slicing an `SJICube` or `SpectrogramCube` extracts 2D cuts from 3D cubes (negative indices through `_ResolveNegativeIndicesMixin` in `irispy/_wcs.py`; `SJICube.fits_wcs` describes the sliced pixels, v0.9.1); `examples/analysis/01_spectral_fitting.py` crops the raster at a single `SpectralCoord`; `irispy/utils/_spectral.py::make_spatial_template` builds 2D spatial cubes from 3D spectral cubes.
- `Data Processing and Analysis:Analysis` — `irispy/utils/moments.py::calculate_moments` (0th/1st/2nd spectral moments, Doppler velocity and line-width maps), `irispy/utils/red_blue.py::calculate_red_blue_asymmetry` (RBA maps with per-pixel quality flags and error propagation), `irispy/utils/density.py::density_diagnostic` (electron density from line ratios).
- `Data Processing and Analysis:Calibration` — `irispy/utils/spectrograph.py::radiometric_calibration`, `convert_photons_per_sec_to_radiance`, `calculate_dn_to_radiance_factor` (DN → photons → erg cm⁻² s⁻¹ sr⁻¹ Å⁻¹, with exposure-time correction); `irispy/utils/response.py::get_latest_response` / `get_interpolated_effective_area`; `docs/tutorial/calibration.rst`; `examples/calibration/03_radiometric_calibration.py`.
- `Data Processing and Analysis:Data Access and Retrieval` — `irispy/data/sample.py` + `irispy/data/_sample.py::_get_sample_files` download IRIS sample data on attribute access via `sunpy.util.parfive_helpers.Downloader` across three mirrors; `download_all()` is public API.
- `Data Processing and Analysis:Data Reduction` — cosmic-ray sigma-clipping/median cleaning (`irispy/utils/cosmic_rays.py`), spectral-window subsetting (`read_spectrograph_lvl2(spectral_windows=...)`), `memmap=True` out-of-core reading, temporal downsampling in `generate_wobble_movie` (`wobble_cadence`), spatial/spectral rebinning in `examples/analysis/01_spectral_fitting.py`.
- `Data Processing and Analysis:Image Processing` — `irispy/utils/utils.py::calculate_dust_mask` (`scipy.ndimage.binary_dilation`), `irispy/utils/dust.py::remove_dust` (temporal replacement with local-median spatial fallback), `irispy/utils/cosmic_rays.py::remove_cosmic_rays` (`rsliding` sliding sigma-clipping and `astroscrappy.detect_cosmics` backends), `irispy/utils/utils.py::image_clipping` histogram-based intensity scaling.
- `Data Processing and Analysis:Processing` — `irispy/io/utils.py::read_files` orchestrates reading/grouping/tar-extraction of a whole IRIS observation into `NDCollection`s; `irispy/meta.py` (`SJIMeta`/`SGMeta`) converts the IRIS FITS keywords into physical quantities.
- `Data Processing and Analysis:Spectrogram` — `irispy/io/spectrograph.py::read_spectrograph_lvl2` builds `SpectrogramCube` / `SpectrogramCubeSequence` / `RasterCollection` spectrogram data products from IRIS raster FITS; `SpectrogramCube.spectral_dispersion`, `.solid_angle` (v0.8.0), `.wavelength_axis`. IRIS "sit-and-stare" observations (`docs/tutorial/level_2.rst`, `docs/known_issues.rst`) hold the slit fixed and produce a genuine 2D intensity array over **wavelength × time**, which is structurally the same product as a classic time-frequency spectrogram; `SpectrogramCubeSequence` carries these. The term is used here in the slit-spectrograph sense rather than the FFT/wavelet sense; HSSI already applies `Spectrogram` to non-FFT spectral/temporal data elsewhere (e.g. the live `speasy` entry).
- `Data Processing and Analysis:Time Series Analysis` — time is a first-class cube axis (`extra_coords.add("time", ...)`, `gwcs` `TemporalFrame`, `SJIMeta.temporal_cadence`, exposure-midpoint times since v0.8.0); `examples/analysis/03_umbral_flashes.py` builds space–time images and intensity-vs-time light curves of sunspot umbral oscillations and cross-matches SJI/raster cadences.

**Data Visualization**
- `Data Visualization` — parent.
- `Data Visualization:2D Graphics` — `SJICube.plot` / `SpectrogramCube.plot` render WCS-aware images through `IRISPlotter`; `irispy/utils/rgb.py::plot_rgb` renders a spectrogram cube as a false-color image whose hue follows the Doppler shift (v0.9.0); moment, RBA, dopplergram and density maps are plotted as 2D images in `examples/analysis/*`.
- `Data Visualization:2D Slices` — `IRISArrayAnimatorWCS` (subclass of `mpl_animators.ArrayAnimatorWCS`) displays a 2D slice of a 3D/4D cube with sliders; `IRISSequenceAnimator` sets IRIS slider labels `["Raster step", "Scan number"]`.
- `Data Visualization:Line Plots` — `SpectrogramCube.plot` drops the colormap for 1D data and produces line plots of spectra; `examples/analysis/01_spectral_fitting.py`, `04_spectral_moments.py`, `05_red_blue_asymmetry.py`, `07_mg_ii_two_gaussian_fitting.py` plot spectral profiles and light curves.
- `Data Visualization:Mission-Specific` — `irispy/visualization.py` is IRIS-specific: `IRISPlotter`, `SJIPlotter` and `IRISSequencePlotter`, registered through ndcube's plotter framework (v0.9.0), and the `IRISArrayAnimatorWCS`/`IRISSequenceAnimator` animators label and colour the helioprojective axes in arcsec and the wavelength axis in nm (`set_axis_properties`) and choose the per-passband IRIS SJI colormaps (`irissji<passband>`, and `sunpy.visualization.colormaps.color_tables.iris_sji_color_table` in the wobble movies).
- `Data Visualization:Movies` — `irispy/utils/wobble.py::generate_wobble_movie` writes MP4 files from IRIS SJI FITS files via `matplotlib.animation.FuncAnimation` + `FFMpegWriter` (FFMPEG required; `.github/workflows/ci.yml` installs it in the `core`, `test`, `docs`, `online` and `build_dists` jobs, not in `sdist_verify` or the upload job).
- `Data Visualization:Spectrogram` — `SpectrogramCube.plot` / `SpectrogramCubeSequence.plot` display IRIS raster spectrograms (wavelength × slit position) and, for sit-and-stare observations, wavelength × time spectrograms, with wavelength-aware axes via `IRISSequencePlotter`/`IRISPlotter`. *Same slit-spectrograph sense as the processing counterpart above.*

**Mission-related** — irispy is the IRIS instrument team's own analysis library (`pyproject.toml` author `IRIS Instrument Team  @ LMSAL`; `licenses/LICENSE.rst` copyright "IRIS Instrument Team @ LMSAL"; hosted in the `LM-SAL` GitHub organization; `.cruft.json` `author_email: https://iris.lmsal.com/contact.html`), so it is mission software rather than a generic tool that happens to read IRIS data.
- `Mission-related` — parent.
- `Mission-related:Analysis` — IRIS-specific analysis utilities: `irispy.utils.moments`, `irispy.utils.red_blue`, `irispy.utils.density`, `irispy.obsid.ObsID` (decodes 10-digit IRIS OBS IDs against the shipped v34/v36/v38/v40 OBS-ID tables).
- `Mission-related:Calibration` — `radiometric_calibration` is documented as "designed to do the same as `iris2/iris_calib_spectrum.pro`" and as confirmed to give the same results as the SolarSoft IDL routine `IRIS_CALIB` (`nrl/iris_calib.pro`); dust and cosmic-ray/spike removal address known IRIS detector artefacts.
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
- `Data Processing and Analysis:File Format Conversion` — `SJICube.to_maps()` converts *objects* (cube → `sunpy.map.Map`), not files; the only output file format the package writes is the MP4 movie (besides a JSON marker it keeps for its own bookkeeping when it extracts tar archives). Excluded.
- `Data Processing and Analysis:Energy Spectra` — irispy handles UV *wavelength* spectra, not particle energy spectra. Excluded.
- `Data Processing and Analysis:Wavelet Analysis`, `:Spectrogram` (as FFT/STFT), `:ML/AI`, `:Plasma Moments`, `:Pitch Angle Distributions`, `:Data Assimilation`, `:Packet Decommutation`, `:Field-line Tracing` — no corresponding code. (`calculate_moments` computes *spectral* moments of a line profile, not plasma velocity-distribution moments.) Excluded.
- `Data Visualization:3D Graphics`, `:Web-Based`, `:Orbit Plots`, `:Hodograms`, `:Spacecraft Formation Plots` — no corresponding code. Excluded.
- `Mission-related:Ingest`, `:Distribution/Access`, `:Operations`, `:Monitoring`, `:Inventory`, `:Instrumentation`, `:Packet Decommutation`, `:System Testing`, `:Archive`, `:Orchestration`, `:Infrastructure as Code` — irispy is a downstream analysis library, not part of the IRIS ground system/pipeline. Excluded.
- `Models and Simulations:Mission-Specific` — irispy's IRIS-specific model of the instrument response, the effective-area model, is already recorded as `Mission-related:Observatory/Instrument Models` and `Models and Simulations:Observatory/Instrument Models`; a third row would restate it (Field 4 rule 9). Excluded.
- `Models and Simulations:MHD`, `:First Principles`, `:Empirical`, `:Forecasting`, `:Theory`, `:Data Guided`, `:Physics-Based`, `:Field-line Tracing`, `:ML/AI` — no solver or physical model implemented; the theoretical line-ratio curves come from fiasco/CHIANTI, not from irispy. Excluded.
- `Servers and Environments` and all its subcategories — no server, container, or HPC component (dask is used for out-of-core arrays only). Excluded.

**On the default branch after v0.9.1post1 (re-check at the next release; read at `134c2996b1db3887c9d9337a9338710440b0c1fb`, 2026-10-28):** each of these would add evidence to the rows above rather than new rows — `irispy.net.IRISClient`, a `sunpy.net.Fido` client for the IRIS archive (Data Access and Retrieval; still not `Mission-related:Distribution/Access`, since a search client is not part of the archive's distribution system); Hinode/SOT readers (`SOTCube`, `SOTFG.tar.gz`/`SOTSP.tar.gz` archives) and the full-disk mosaic reader `read_mosaic` with `MosaicCube.to_map` (Processing, Mission-related Processing, 2D Slices); `irispy.utils.bursts`, `irispy.utils.mg_features`, `irispy.utils.fitting` (`line_model`, `starts_from_model`, `maps_from_fit`, `non_thermal_velocity`) and the packaged line catalog `irispy.utils.lines.get_lines` (Analysis, Forward-Fitting, Mission-related Analysis — the burst and Mg II finders port SolarSoft's `iris_burst_check.pro`, `iris_sji_burst_check` and `iris_get_mg_features.pro`); `calculate_wavelength_drift` (a port of `iris_prep_wavecorr_l2`), `radiation_temperature` and slit-jaw radiometric calibration (Calibration); `subtract_background` and `average_window` (Data Reduction, 2D Slices); `BaseMeta.mu`/`SGMeta.exposure_mu` and an Earth-seen `fov_center` (Solar coordinates); a dust mask from the IRIS pipeline's bad-pixel table (Image Processing). Removed there: `gaussian1d_on_linear_bg` (replaced by `irispy.utils.fitting`), `image_clipping`, `convert_photons_per_sec_to_radiance`, the public animator classes and `density_diagnostic`'s fiasco `Ion` argument. `radiation_temperature` and `non_thermal_velocity` convert observed quantities, and `get_lines` ranks lines by strengths precomputed by an unshipped script, so none of them makes `Models and Simulations:Physics-Based` or `:Theory` apply.

### 5. Related Region (MANDATORY)
- Solar Environment
- Chromosphere
- Corona

*Source note (line numbers at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`): `Solar Environment` is retained because all irispy functionality is solar. `Chromosphere` is supported directly by the IRIS mission statement and passband description: `docs/iris.rst:11` says the mission studies mass and energy flow through the chromosphere and transition region, and `docs/iris.rst:14` says the passbands are focused on those regions. `Corona` is supported by the same passband description, which explicitly includes light coverage of the corona (`docs/iris.rst:14`), and by the documented 4,500 K to 10 MK spectral-line coverage (`docs/iris.rst:42` and the FUV 1 row of Table 1, `:52`, log T 3.7–7.0).*
*The finer Region values were previously deferred solely because the agent documentation exposed only a five-value list, even though the dossier already recognized that they described IRIS more precisely. That procedural premise was falsified on 2026-08-25: the Region vocabulary is flat, so `Solar Environment` does not imply the finer rows, and the user approved adding `Chromosphere` and `Corona`. `Photosphere` remains considered and declined: the release identifies only photospheric wavelength-calibration lines (`docs/tutorial/calibration.rst:12`) and a Mg II wing passband (`docs/iris.rst:69`), not the photosphere as an IRIS science target. `Solar Interior` remains excluded because no repository source supports sub-photospheric diagnostics.*
*On the default branch after v0.9.1post1 (re-check at the next release; read at `134c2996b1db3887c9d9337a9338710440b0c1fb`): irispy reads the Hinode/SOT images and magnetic data supplied with IRIS observations (`irispy.sji.SOTCube`, the `sot_l2_*`/`sotsp_l2_*` dispatch of `irispy/io/utils.py::read_files`) as co-aligned context, but no project source calls those data photospheric. Only a test-fixture note, `irispy/data/test/sot/overview.txt`, describes what each product is (G-band broadband filtergrams, Na I 5896 narrowband magnetograms, an SOT-SP line-of-sight field map), and Field 5 rule 3 does not accept fixtures as evidence; the other mentions are labels, file names, reader branches and generic "images and magnetic data" wording, for example the band label "G band 4305" in `changelog/299.bugfix.rst`, the fixture file names in `irispy/conftest.py`, the `instrume == "SOT-SP"` branch of `irispy/io/utils.py` and the SOT-SP handling in `irispy/visualization.py`, and "image and magnetic data" in the `SOTCube` docstring; none calls the data photospheric. Mapping them to the photosphere would be domain knowledge rather than the project's statement, and irispy does no analysis of them beyond reading, masking and plotting (rule 4). The branch's other photospheric mentions are of the same kind as the calibration lines: the Mg II Dopplergram example measures wavelength shifts from "photospheric lines of known rest wavelength" (`examples/analysis/02_mg_ii_dopplergrams.py:85`), and the line catalog lists photospheric absorption lines and offers a `"photospheric"` abundance set (`docs/line_database.rst`, `irispy/utils/lines.py`). Reconsider if a release documents photospheric data or analysis.*

### 6. Authors (MANDATORY)

The author list is supported by repository, Zenodo/DataCite and ORCID evidence, with identities matched by ORCID and affiliations resolved by ROR.

> **Author identity history.**
>
> - The author previously recorded only as `juanms` is **Juan Martínez-Sykora**, now carrying ORCID `https://orcid.org/0000-0002-0333-5717`, with his Lockheed Martin Solar and Astrophysics Laboratory and Bay Area Environmental Research Institute affiliations recorded.
> - The Rosseland Centre for Solar Physics, University of Oslo affiliation now carries its verified ROR `https://ror.org/01xtthb56`. This organization is shared with the SunPy entry, which is correctly identified by the same ROR.
> - **IRIS Instrument Team @ LMSAL** is an approved author. No ROR exists for the team or for LMSAL, so it is recorded without an identifier.
> - **Roy Smart** is an author from the v0.9.0 Zenodo deposit onward, with ORCID `https://orcid.org/0000-0002-9997-5515` and his Montana State University affiliation. He is the same person as the identifier-less "Roy Smart" HSSI credited on its ndcube entry before this update, so this entry uses that person, and the ORCID belongs on it.
>
> The intended public author order is **Freij, Martínez-Sykora, Pereira, IRIS Instrument Team @ LMSAL, Smart** — the organizational author follows the three human authors by curatorial decision, preserving their established order while still crediting the team, and Roy Smart, attested later, follows the authors already listed.

**Author 1 — Nabil Freij**
- **Author Identifier:** https://orcid.org/0000-0002-6253-082X
- **Affiliation:**
  - Bay Area Environmental Research Institute — https://ror.org/024tt5x58
  - Lockheed Martin Solar and Astrophysics Laboratory — *(no ROR record exists; searched ror.org for "Lockheed Martin Solar and Astrophysics Laboratory" — only generic Lockheed Martin country entities returned)*
  - SETI Institute — https://ror.org/02dxgk712

*Source note: corroborated by `pyproject.toml` authors, 365 of the 373 commits reachable from the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c` (`nabil.freij@gmail.com`), GitHub profile `nabobalis` ("Research Scientist in Solar Physics", company "SETI Institute & LMSAL (@LM-SAL)"), and Zenodo/DataCite creator affiliation "SETI Institute & LMSAL (@LM-SAL)".*

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

*Source note / rationale: listed as the **first** author in `pyproject.toml` (`{ name = "IRIS Instrument Team  @ LMSAL" }` at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`), holds the copyright in `licenses/LICENSE.rst` ("Copyright (c) 2020-2025, IRIS Instrument Team @ LMSAL" at the tag), and is the templated author in `.cruft.json` (`author_name: "IRIS Instrument Team"`, `author_email: https://iris.lmsal.com/contact.html`). SoMEF also extracts it as an author. Zenodo/DataCite omit the team because their creator list is derived from GitHub contributors. The canonical spelling `IRIS Instrument Team @ LMSAL` matches the copyright holder in `licenses/LICENSE.rst`; `pyproject.toml` carries the same string with a double space at the tag, so the single-spaced LICENSE form is used; the default branch after v0.9.1post1 single-spaces it, so the two sources will agree from the next release. Although `pyproject.toml` lists the team first, it is placed last by the settled curatorial decision to preserve the established order of the human authors while still crediting the team. No ROR exists for either "IRIS Instrument Team" or its parent Lockheed Martin Solar and Astrophysics Laboratory, so it is recorded without an identifier. An expanded form — "Interface Region Imaging Spectrograph Instrument Team at the Lockheed Martin Solar and Astrophysics Laboratory" — was considered and rejected because it is not a name the project itself uses.*

**Author 5 — Roy Smart**
- **Author Identifier:** https://orcid.org/0000-0002-9997-5515
- **Affiliation:**
  - Montana State University — https://ror.org/02w0trx84

*Source note / rationale: a creator of the Zenodo/DataCite records of v0.9.0, v0.9.1 and v0.9.1post1 (record 23023081: "Roy Smart", affiliation "Montana State University"; the v0.8.1 and earlier deposits do not list him). He wrote the false-color RGB rendering released in v0.9.0 (pull request #168; three commits by `Roy Smart <roytsmart@gmail.com>` reachable from the v0.9.1post1 tag). Name form: "Roy Smart", as the Zenodo creator and the commits write it; his ORCID record gives given name "Roy", family name "Smart" and credit name "Roy T. Smart". ORCID `0000-0002-9997-5515` is tied to this contributor by its researcher URL `http://roytsmart.github.io`, the GitHub Pages site of the contributor's account `roytsmart`, and its works list his solar spectroscopy papers and software, `colorsynth` among them. Before this update HSSI's ndcube entry credited an identifier-less "Roy Smart", the same person: ndcube's history carries four commits from the same address `roytsmart@gmail.com`. This entry therefore uses that person, and the ORCID, which no HSSI person carried before this update, belongs on it and shows on the ndcube entry too. Montana State University is the affiliation the project's own Zenodo metadata gives for him at these releases.*

*Not an author: Souvik Bose (GitHub `souvikita`) has two commits on the default branch (2026-09-30, the AIA synthetic-raster co-alignment example `examples/coalign/04_aia_synthetic_raster.py`) and appears in no author source: not in `pyproject.toml`, and not among the creators of any Zenodo deposit, all of which up to v0.9.1post1 predate his commits. He is a committer (Field 6 rule 5); a later deposit that lists him as a creator would make him an author.*

### 7. Software Name (MANDATORY)
irispy

*Source note: matches the repository name, `README.rst` ("``irispy`` is a library…"), `docs/index.rst`, and `pyproject.toml` `[tool.setuptools] provides = ["irispy"]`. The PyPI/conda-forge **distribution** name is `irispy-lmsal` (to avoid a name clash), but README and docs state the package "is imported as ``irispy`` and is referred to as ``irispy`` in the documentation". `irispy` is therefore the correct software name; the distribution name is recorded in the Description instead.*

### 8. Description (MANDATORY)

irispy is a library that provides the tools to read in and analyze data from Interface Region Imaging Spectrograph (IRIS). IRIS is a NASA Small Explorer satellite whose 20 cm telescope feeds a high-frame-rate ultraviolet imaging spectrograph, observing the solar chromosphere and transition region (with lighter coverage of the corona) in far-ultraviolet and near-ultraviolet passbands at about 0.33 arcsecond spatial resolution and roughly 1 second cadence. irispy provides classes for handling both IRIS slit-jaw imager (SJI) images and spectrograph (SG) raster observations, linking each observation to its measurement uncertainties, physical units, a mask marking unreliable or unphysical pixels, World Coordinate System transformations describing position, wavelength and time, and the full IRIS metadata. It reads IRIS level 2 SJI and raster FITS files, including gzipped files, _raster.tar.gz archives and the IRIS-aligned SDO/AIA data cubes distributed with each observation by the IRIS team, and can load an entire observation with a single call. Analysis and calibration capabilities include exposure-time correction and radiometric calibration between data number, photons and physical radiance units using the time-dependent IRIS effective-area response, cosmic-ray and dust-artefact removal, spectral moment maps, red-blue asymmetry maps, electron-density diagnostics from line ratios, decoding of IRIS OBS IDs into human-readable observing descriptions, IRIS-specific plotting and animation, and wobble movie generation. The package assumes the IRIS level 2 data products, which are the recommended science product; level 1 data must first be processed with the SolarSoft IDL calibration routines. Note that the package is distributed on PyPI and conda-forge as irispy-lmsal to avoid a name clash, but is imported and referred to as irispy.

*Source note / rationale: the HSSI description held at first extraction was a single 121-character sentence identical to the concise description, which did not meet this field's stated purpose ("sufficiently detailed to provide the potential user with information to determine if the software is useful to their work… what the software does, why to use it, assumptions it makes"). The submitted sentence is preserved verbatim as the opening; everything appended is drawn from primary sources: `docs/index.rst` (classes, uncertainties/units/mask/WCS/metadata, calibration routines), `docs/iris.rst` (mission, telescope, passbands, resolution/cadence, level definitions and the level 1 caveat), `README.rst` (NASA-funded Small Explorer, the `irispy-lmsal` naming warning), `irispy/io/utils.py::read_files` (whole-observation reading, tar and SDO archive handling), `CHANGELOG.rst` 0.7.0 and the corresponding modules (`utils/moments.py`, `utils/red_blue.py`, `utils/density.py`, `utils/cosmic_rays.py`, `utils/dust.py`, `utils/spectrograph.py`, `utils/response.py`, `utils/wobble.py`, `obsid.py`). This is an evidence-backed completeness improvement, not a stylistic rewrite.*
*Formatting note: written as plain text with no markdown inline-code backticks because HSSI stores `description` as a plain-text field and would display the backticks literally.*
*Capability coverage (read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`): every capability the text names is in the release. The text predates the false-color RGB rendering added in v0.9.0. The project's own descriptions — the `README.rst` lead sentence, which opens the stored text, the `docs/index.rst` introduction and the `pyproject.toml` summary — are unchanged since the Source Revision, so the stored text is neither out of date against them nor contradicted by the code and stays (Field 8 rule 6); extending its list would be composing new prose rather than adopting the project's. On the default branch after v0.9.1post1 (re-check at the next release) the code adds an IRIS archive client, Hinode/SOT and full-disk mosaic readers, line fitting, UV-burst detection, Mg II feature finding, wavelength-drift correction, background subtraction and a packaged line catalog; a later update should adopt fuller project text if the project publishes one.*

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
- **Version Number:** v0.9.1post1
- **Version Date:** 2026-09-28
- **Version Description:** Not found
- **Version PID:** https://doi.org/10.5281/zenodo.23023081

*Source note / rationale (release history read from the current remote's tags and the default branch at `134c2996b1db3887c9d9337a9338710440b0c1fb`): v0.9.1post1 is the newest release. Its tag points to commit `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`, an ancestor of the default branch; it has a GitHub release, not marked pre-release, published 2026-09-28T17:23:15Z; and Zenodo deposited it as record 23023081 (`version: "v0.9.1post1"`, `IsSupplementTo https://github.com/LM-SAL/irispy/tree/v0.9.1post1`, under the concept DOI of Field 2). A post-release is not a pre-release, and it follows v0.9.1 in the project's release order. The releases after v0.7.0 are v0.8.0 (2026-08-10), v0.8.1 (2026-08-14), v0.9.0 (2026-09-10), v0.9.1 (2026-09-28) and v0.9.1post1; HSSI held v0.7.0 until this update. The `v` prefix follows the tag, the GitHub release name and the Zenodo version string, as the earlier stored value did.*

*v0.9.1post1 differs from v0.9.1 only in `docs/tutorial/installation.rst` (pull request #196, which corrects the conda package name to `irispy-lmsal`), and PyPI has no upload of it: PyPI's newest `irispy-lmsal` release is 0.9.1 (uploaded 2026-09-28T05:11:58Z, not yanked), the same code. No PyPI upload is newer than the v0.9.1post1 tag, so no PyPI-only release competes with it; a PyPI upload of the project's own package that is neither yanked nor a pre-release would count as a release whichever commit it was built from. Commits on the default branch after the v0.9.1post1 tag are unreleased (the fragments under `changelog/`); a later update records the next tagged or uploaded release.*

*GitHub's `/releases/latest` endpoint returned v0.9.1, not v0.9.1post1, on 2026-10-29; the release list, the tag and the Zenodo deposits all place v0.9.1post1 after v0.9.1, so that endpoint is no reason to move this field back to v0.9.1.*

*Date: the GitHub release's `published_at` UTC day, 2026-09-28; the tagged commit (2026-09-28T17:21:48Z) and the Zenodo deposit (`publication_date` 2026-09-28) agree.*

*Description: deliberately empty. The release body's only item is "SCrewed up wrong package name" (#196), a documentation fix whose words would not tell a reader without project context what changed, and `CHANGELOG.rst` has no 0.9.1post1 section (its newest heading is `0.9.1 (2026-09-27)`). The v0.7.0 description stored until this update was a curator's condensation of the 0.7.0 changelog; it is not carried onto the new number.*

*PID: the version DOI of exactly this release; the concept DOI stays in Field 2.*

*Release lineage: the release tags were re-pointed by the history rewrite noted in the header — `v0.7.0`, for one, now resolves to commit `6557ba9e58f90ff723506b8de06ae41c62ccda6c`, not the pre-rewrite `5cb236d` that a clone made before the rewrite still holds. Read release history from the current remote's tags and `git rev-list` of the current default branch.*

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source note (read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`): Python 3.x is correct and overwhelmingly dominant — the tag's tracked `.py` files total 530,641 bytes against 594 bytes of IDL and 673 of shell (sizes from `git ls-tree -l`); `pyproject.toml` requires Python >= 3.12 with classifiers for 3.12/3.13/3.14, and `.cruft.json` records `use_compiled_extensions: "n"` (pure Python, `py3-none-any` wheel). On the default branch after v0.9.1post1 the minimum is Python 3.13 and five more IDL reference scripts sit under `irispy/data/test/`, excluded from the wheel; re-check at the next release.*

*Previous values `IDL` and `Other` are deliberately excluded. The only IDL in the release is the single 594-byte SolarSoft test-data generator `irispy/data/test/get_cali_test_data.pro`, which the wheel carries only as test data under `irispy/data/test/` and the package never executes; "Other" corresponded to two CircleCI shell scripts (`.circleci/codecov_upload.sh`, `.circleci/early_exit.sh`, 673 bytes combined), which are CI plumbing rather than software functionality. Field 13 asks the submitter to "Select the most important languages", and neither meets that bar against 530,641 bytes of Python. The SSWIDL calibration lineage that motivated the original `IDL` value is preserved where it belongs — Field 29 records the SolarSoft IRIS package as Related Software, and Fields 4/18 record the IDL-artifact reading (`scipy.io.readsav`) irispy performs.*

### 14. Reference Publication (RECOMMENDED)
Not found

*Source note (read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`): there is no software paper for irispy — no JOSS submission, no CITATION.cff and no `codemeta.json`. The "Citing irispy" section added to `README.rst` and `docs/index.rst` in v0.9.1 asks users to "cite the Zenodo record of the version you used" through the concept DOI 10.5281/zenodo.10443678: a software deposit (Fields 2 and 12), not a paper, so this field stays empty. The IRIS **instrument** paper is recorded under Related Publications (Field 27) instead, since it describes the instrument rather than the software.*

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

*Source note (read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`): the license name is confirmed by `licenses/LICENSE.rst` (three-clause BSD text, "Copyright (c) 2020-2025, IRIS Instrument Team @ LMSAL"), `pyproject.toml` (`license-files = ["licenses/LICENSE.rst"]`, classifier "License :: OSI Approved :: BSD License"), and `.cruft.json` (`license: "BSD 3-Clause"`). The URI is the SPDX BSD-3-Clause identifier. On the default branch after v0.9.1post1 `pyproject.toml` declares the PEP 639 SPDX expression `license = "BSD-3-Clause"` instead of the classifier and the copyright runs to 2026, the same license. GitHub's repository API reports `license: null` for this repository, whose license text is `licenses/LICENSE.rst` rather than a root `LICENSE` file; the license files and package metadata are the authority.*
*Conflict noted and deliberately rejected: DataCite/Zenodo report `rightsList` "Creative Commons Attribution 4.0 International" (`cc-by-4.0`) for this DOI, the v0.9.1post1 deposit included. That is a Zenodo deposit default and contradicts the repository's own LICENSE; the repository license is authoritative. Do not autofill the license from the DOI for this entry.*

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
- doppler velocity — existing HSSI vocabulary term; a quantity irispy computes and a term a searcher would type: `calculate_moments` returns a `"velocity"` map, the "Doppler shift from the centroid in km/s" (`irispy/utils/moments.py:83`), and `irispy.utils.rgb.plot_rgb` colors spectra by Doppler velocity (v0.9.0), at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`.

- pyhc package — the PyHC package marker (Field 16 rule 15): irispy is listed as `irispy-lmsal` in the PyHC registry's `_data/projects.yml` (read at `heliophysicsPy/heliophysicsPy.github.io` `f7b0421b08c2cbc614a8d68372b42428d3a53cb2`), so the entry carries it whatever other sources say. HSSI already held it; this dossier's earlier revision omitted it.

*Source note: `iris`, `lmsal`, `nasa`, `science`, `solar`, `solar physics`, and `spectra` come from `pyproject.toml` `keywords` (unchanged at the v0.9.1post1 tag). The remaining science keywords are drawn from the package's own documentation; existing controlled terms are reused where available to avoid near-duplicates.*
*PyHC note: irispy is a PyHC **community** package, registered in `_data/projects.yml` (at `f7b0421b`) as `irispy-lmsal` with PyHC facet keywords `["solar", "specific", "data_analysis", "spectra", "fits", "time", "coordinates", "plotting", "multidimensional"]`. These are PyHC's internal facets rather than science keywords, so they are used to corroborate other fields (functionality, formats) rather than copied here. The PyHC entry's `code` (`github.com/LM-SAL/irispy-lmsal`) and `docs` (`irispy-lmsal.readthedocs.io`) URLs are stale relative to the current repository and documentation URLs used in Fields 3 and 24.*
*On the default branch after v0.9.1post1 (re-check at the next release): `irispy.utils.bursts.find_si_iv_bursts` finds "UV bursts in Si IV spectra"; once released it supports a new lower-case keyword `uv bursts` (no keyword in HSSI's vocabulary names bursts, and the Phenomena vocabulary has no burst row).*

### 17. Data Sources (OPTIONAL)

*Evidence read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`.*

- HTTP/HTTPS Directories — `irispy/data/_sample.py` builds file paths under three sample-data mirrors, plain directory trees outside the mission archive (`github.com/sunpy/data/raw/main/irispy-lmsal/`, `github.com/sunpy/sample-data/raw/master/irispy-lmsal/`, `data.sunpy.org/irispy-lmsal/`), and downloads the files; that is the evidence this row rests on (Field 17 rules 9 and 12). The gallery examples fetch cut-down IRIS files from the release assets of `github.com/LM-SAL/irispy-data` with `pooch.retrieve` (v0.9.1), which serve only the docs and tests, and the full observations they link sit in the IRIS archive, carried by `Observatory/Mission-specific` (rule 9).
- Observatory/Mission-specific — the primary documented source is the IRIS mission's own archive and search tool: `docs/tutorial/acquiring_data.rst` "IRIS data search webpage" (`iris.lmsal.com/search/`), `README.rst` "The data is publicly available" (`iris.lmsal.com/data.html`), and the `www.lmsal.com/solarsoft/irisa/data/level2_compressed/` level-2 tree the examples link and download from. Cross-listed with Related Observatories per this field's instructions.
- The Virtual Solar Observatory. — *(the trailing period is part of the controlled value)* — `docs/tutorial/acquiring_data.rst` devotes a section to searching and fetching IRIS data through `sunpy.net.Fido` with `a.Instrument.iris`, with worked `VSOClient` output. The value is included because irispy documents this as a supported acquisition path and depends on SunPy, even though irispy does not implement its own VSO client.

**Considered and excluded:** CDAWeb, OMNIWeb, SSCWeb, HAPI, das2, TAP, VirES, S3/Cloud-aware, FTP/FTPS Directories — no client, URL, or documentation reference for any of these.

*On the default branch after v0.9.1post1 (re-check at the next release; read at `134c2996b1db3887c9d9337a9338710440b0c1fb`): `irispy.net.IRISClient`, a `sunpy.net.Fido` client, searches the IRIS archive through LMSAL's Heliophysics Coverage Registry (`https://www.lmsal.com/hek/hcr`) and downloads its files — more `Observatory/Mission-specific` evidence; the tutorial's Fido section uses it in place of the VSO and notes that the VSO lists the same files; and the sample data come from two mirrors, the `sunpy/sample-data` one dropped.*

### 18. Input File Formats (RECOMMENDED)

*Evidence read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`.*

- FITS — `astropy.io.fits` throughout `irispy/io/sji.py`, `irispy/io/spectrograph.py`, `irispy/io/utils.py` (`fits_info`, `_get_simple_metadata`), `irispy/utils/wobble.py`; IRIS level-2 SJI and raster FITS are the package's primary input.
- IDL.sav — `irispy/utils/response.py` reads the shipped IRIS response file with `scipy.io.readsav(ROOTDIR / "iris_sra_c_20231106.geny", python_dict=True)`; tests read `.sav` files (`fit_iris_xput_input.sav`, `input_calibration.sav`, `iris_response_2025_08_05T22_25_04_723.sav`) through the same IDL SAVE reader.
- csv — `irispy/obsid.py` reads the shipped IRIS OBS-ID tables `data/v{34,36,38,40}-table10.csv` and `-table2000.csv` with `pandas.read_csv`.
- Other — gzip-compressed FITS (`*.fits.gz`, e.g. `SJI_1330_t000.fits.gz`) and tar archives handled by `irispy/io/utils.py::_extract_tarfile` (`*_raster.tar.gz` IRIS raster bundles and `*SDO.tar.gz` IRIS-aligned SDO/AIA bundles).

**Considered and excluded:** CDF, HDF5, netCDF3/4, Zarr, ISTP-Compliant, ascii — no reader. JSON — the only JSON the package reads is the `.irispy-extracted.json` marker that `read_files` writes, through `_extract_tarfile`, and reads back for its own bookkeeping (`irispy/io/utils.py:58–74`), which Field 18 rule 4 excludes; `irispy/tests/figure_hashes_*.json` is a pytest-mpl figure-hash fixture, not a user data input.

*On the default branch after v0.9.1post1 (re-check at the next release; read at `134c2996b1db3887c9d9337a9338710440b0c1fb`): the readers add Hinode/SOT files, the `*SOTFG.tar.gz`/`*SOTSP.tar.gz` archives and the gzipped full-disk mosaics (all FITS, or `Other` for the archives); `obsid.py` reads its CSV tables with `astropy.io.ascii` instead of pandas; `irispy/utils/lines.py` reads a packaged ECSV line catalog, `irispy/data/iris_lines.ecsv.gz`, with `QTable.read(..., format="ascii.ecsv")`, which rule 5 would admit as `ascii` on the footing of the stored `csv` and `IDL.sav` values, which also rest on packaged files; and `irispy.net.IRISClient` parses the registry's JSON responses in memory over the network, not from files (rule 9).*

### 19. Output File Formats (RECOMMENDED)

- Other — MP4 (H.264) video files written by `irispy/utils/wobble.py::generate_wobble_movie` via `matplotlib.animation.FFMpegWriter` (filename pattern `{TDESC1}_{date}_wobble.mp4`). This is the only user-facing file output in the package.

*Source note / audit trail (read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`): FITS is deliberately **not** listed as an output. The only `fits.writeto` call is in test infrastructure (`irispy/conftest.py` fake-data fixtures), not in the public API. Figures are returned as matplotlib axes for the user to save, not written by irispy; `read_files` extracts tar archives, which copies the archive's files rather than writing a format. On the default branch after v0.9.1post1 `generate_wobble_movie` takes an `SJICube` instead of FITS files and still writes MP4, and the test-data scripts live in `tools/`, outside the package; re-check at the next release.*

### 20. Operating System (RECOMMENDED)

- Linux
- Mac
- Windows

*Source note (read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`): `.github/workflows/ci.yml` runs the test matrix on `windows: py312`, `macos: py313`, `linux: py312-oldestdeps` and `linux: py314-devdeps`, plus a `linux: py314` core job, with ffmpeg installed via choco/brew/apt respectively. `docs/tutorial/installation.rst` gives per-platform install instructions for Linux, Windows and Mac. `pyproject.toml` also carries the classifier "Operating System :: OS Independent" and `platforms = ["any"]`; the three concrete CI-verified platforms are recorded rather than the generic value.*

### 21. CPU Architecture (RECOMMENDED)

- x86-64
- Apple Silicon arm64
- Linux aarch64 or arm64
- ppc64le

*Source note: `docs/tutorial/installation.rst` explicitly lists the supported install targets — Linux x86-64 / aarch64 / ppc64le, Windows x86-64, and Mac arm64 (Apple Silicon) / x86-64. Consistent with the package being pure Python: `.cruft.json` `use_compiled_extensions: "n"` and the PyPI distribution `irispy_lmsal-0.9.1-py3-none-any.whl`; read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`. GPU is not listed (no GPU code path).*

### 22. Related Phenomena (OPTIONAL)

- Solar Flares — `docs/iris.rst`: "IRIS data is also used for a wide range of other science topics including: solar flares…"; the spectral lines "cover temperatures from 4,500 K to 10 MK… possibly 10 MK under flaring conditions"; `irispy/obsid.py` decodes IRIS flare observing programs ("Flare linelist 1").
- Solar Corona — `docs/iris.rst`: IRIS observations include "light coverage of the corona"; FUV1 covers log T 3.7–7.0 (`docs/iris.rst` Table 1).
- Coronal Heating — the IRIS mission statement quoted in `docs/iris.rst`: "to understand how the solar atmosphere is energized and to understand how mass and energy flows through the chromosphere and transition region".

*The quoted `docs/iris.rst` passages are at lines 11, 12, 14 and 42 and in Table 1 at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`.*

**Considered and excluded:** X-ray emission (IRIS is a UV instrument); Coronal Mass Ejections, Solar Wind, Geomagnetic Storms (no supporting functionality or documentation claim — the docs mention prominences, sunspots, coronal rain and spicules, none of which are in the vocabulary). UV bursts, which `irispy.utils.bursts` finds on the default branch after v0.9.1post1, have no row either; Field 16 notes them as a keyword for the next release.

### 23. Development Status (RECOMMENDED)
Active

*Source note / rationale: repostatus.org "Active" = "reached a stable, usable state and is being actively developed" (Field 23 rule 6: last commit under six months old). Dated anchors: last commit on the default branch `134c2996b1db3887c9d9337a9338710440b0c1fb`, 2026-10-28T20:05:52Z; last release v0.9.1post1, 2026-09-28, after v0.8.0 (2026-08-10), v0.8.1 (2026-08-14), v0.9.0 (2026-09-10) and v0.9.1 (2026-09-28); the repository is not archived and the README carries no repostatus badge or status statement. Publication on PyPI and conda-forge with stable Read the Docs, and active towncrier changelog fragments in `changelog/`, corroborate it. `pyproject.toml` carries the trove classifier "Development Status :: 3 - Alpha" at the v0.9.1post1 tag ("4 - Beta" on the default branch after it), a packaging label from a distinct vocabulary that does not override the activity evidence for `Active`.*

### 24. Documentation (RECOMMENDED)
https://irispy.readthedocs.io/en/stable/

*Source note: confirmed by `pyproject.toml` `urls.Documentation`, PyPI `project_urls.Documentation`, `README.rst` ("Documentation is hosted on Read the Docs"), and SoMEF. Installation instructions live under this URL at `docs/tutorial/installation.rst`. The PyHC registry's `irispy-lmsal.readthedocs.io` value is stale.*

### 25. Funder (OPTIONAL)
Not found

*Source note: this field is deliberately left empty. The repository contains no package-level funding acknowledgement — no funding section in `README.rst`, the documentation, or `pyproject.toml`, and the Zenodo/DataCite record's `fundingReferences` is empty. Both still hold at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c` and for its deposit (10.5281/zenodo.23023081); the README's only funding words describe the mission ("IRIS is a NASA-funded Small Explorer").*

*__DECISION RECORD (user-approved 2026-07-29): NASA was considered and deliberately NOT added.__ A NASA funder row (`National Aeronautics and Space Administration`, `https://ror.org/027ka1x80`) was proposed on the strength of irispy being the IRIS instrument team's own library for a NASA-funded mission (`README.rst` "IRIS is a NASA-funded Small Explorer…"; `docs/iris.rst` "… is a NASA Small Explorer (SMEX) satellite"; `pyproject.toml` author "IRIS Instrument Team  @ LMSAL" and keyword `NASA`), and cross-entry precedent does exist — live HSSI's aiapy entry records that exact ROR alongside `Science and Technology Facilities Council`. The user's decision is that mission-level funding is too indirect to attribute to the software library itself: the available evidence funds the IRIS mission and its instrument team, not this package. Recorded here so the reasoning is not re-litigated on a future refresh, and so the empty value is understood as a considered choice rather than a gap in extraction.*

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

*Source note: no award title or grant number appears anywhere in the repository, documentation, PyPI metadata, or the Zenodo/DataCite record (`fundingReferences` is empty).*

*__DECISION RECORD (user-approved 2026-07-29): an evidenced award candidate was considered and deliberately NOT added__, consistent with the Field 25 decision to omit mission-level funding. The IRIS instrument paper cited in Field 27 (De Pontieu et al. 2014, `10.1007/s11207-014-0485-y`) states verbatim in its Acknowledgements, verified directly against the Springer article of record: "This work is supported by NASA under contract NNG09FA40C and the Lockheed Martin Independent Research Program." That is a real, numbered NASA contract, and it would have supported an award entry ("NASA contract for the Interface Region Imaging Spectrograph (IRIS) mission", number `NNG09FA40C`) had mission-level funding been accepted. It funds the IRIS mission, not this software package, so it is omitted along with the Field 25 funder. Recorded here — including the contract number — so the evidence is preserved for any future refresh that revisits the mission-vs-package question.*

*Also named in the same acknowledgement and likewise omitted: the Lockheed Martin Independent Research Program (an internal LM program, no ROR, no award number) and the Norwegian Space Centre / ESA PRODEX contract (funds the Svalbard data downlink, i.e. mission operations, further still from the software). An earlier, weaker candidate ("NASA Small Explorer (SMEX) program support…") was rejected outright as an unsourced paraphrase of the mission type rather than a stated award.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

*Code and documentation evidence in this section was read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`; the literature was searched on 2026-10-29.*

**The instrument paper and the method references the release cites (incumbents, kept under Field 27 rule 7):**

- https://doi.org/10.1007/s11207-014-0485-y — De Pontieu, B., Title, A. M., Lemen, J. R., Kushner, G. D., Akin, D. J., et al. (2014). The Interface Region Imaging Spectrograph (IRIS). *Solar Physics*, 289, 2733–2779.
  *Source note: the IRIS instrument paper, linked from `README.rst` ("For more information see the instrument paper which is available online for free") and cited directly in the code as the source of the detector constants irispy applies — `irispy/utils/constants.py`: "Source: IRIS instrument paper (https://link.springer.com/article/10.1007/s11207-014-0485-y)" for `DETECTOR_GAIN`, `DETECTOR_YIELD`, `READOUT_NOISE`. It describes the instrument rather than the software, which is why it is here rather than in Field 14; it is the reference any user of irispy's calibrated output needs.*
- https://doi.org/10.3847/1538-4357/ab9014 — Yu, K., Li, Y., Ding, M. D., Li, D., Zhou, Y.-A., & Hong, J. (2020). IRIS Si IV Line Profiles at Flare Ribbons as Indications of Chromospheric Condensation. *The Astrophysical Journal*.
  *Source note: cited as the methodological reference for irispy's spectral-moment implementation — `irispy/utils/moments.py` References links "arXiv:2005.02029, Section 3.1", which resolves to this DOI. An IRIS science paper whose method irispy implements.*
- https://doi.org/10.1088/0004-637X/772/2/90 — Leenaarts, J., Pereira, T. M. D., Carlsson, M., Uitenbroek, H., & De Pontieu, B. (2013). The Formation of IRIS Diagnostics. II. The Formation of the Mg II h and k Lines in the Solar Atmosphere. *The Astrophysical Journal*, 772, 90.
  *Source note: the diagnostic basis for irispy's Mg II h/k analysis. `examples/analysis/07_mg_ii_two_gaussian_fitting.py` states that the flux, asymmetry and peak-separation maps it builds "are motivated by the Mg II h/k diagnostics described by Leenaarts et al. (2013)" and links this DOI. DOI verified to resolve via CrossRef.*
- https://doi.org/10.1088/2041-8205/780/1/L12 — Dudík, J., Del Zanna, G., Dzifčáková, E., Mason, H. E., & Golub, L. (2014). Solar Transition Region Lines Observed by the Interface Region Imaging Spectrograph: Diagnostics for the O IV and Si IV Lines. *The Astrophysical Journal Letters*, 780, L12.
  *Source note: the reference irispy's O IV density diagnostic reproduces. `examples/analysis/06_oiv_density_diagnostics.py` states "We will reproduce aspects of the top row of Fig. 4 from Dudík et al. (2014)" and links this DOI, exercising `irispy/utils/density.py::density_diagnostic`. Kept as an incumbent under rule 7; an example's science reference alone would not admit a new entry. Bibliographic details verified against CrossRef (title, all five authors, volume 780, page L12); cited as 2014 per the journal volume and the repository's own reference, though CrossRef records online publication 2013-12-13.*

**Third-party publications that state they used irispy (Field 27 rule 5).** irispy's citing literature is small, so each deliberate use is news to a searcher; the catalogue's maintainer chose these four on 2026-10-29 after weighing the evidence for and against each:

- https://doi.org/10.1038/s41550-024-02396-4 — Lörinčík, J., Dudík, J., Sainz Dalda, A., Aulanier, G., Polito, V., et al. (2025). Observation of super-Alfvénic slippage of reconnecting magnetic field lines on the Sun. *Nature Astronomy*, 9, 45–54.
  *Methods: IRIS data processed with the "SolarSoft package in the Interactive Data Language (IDL) as well as the ‘iris_lmsalpy’ and ‘irispy_lmsal’ [ref. 43] libraries in Python" (the bracketed reference marker is the article's superscript 43).*
- https://doi.org/10.3847/1538-4357/adccc8 — Lörinčík, J., Polito, V., Kerr, G. S., Hayes, L. A., & Russell, A. J. B. (2025). Probing Progression of Heating Through the Lower Flare Atmosphere via High-cadence IRIS Spectroscopy. *The Astrophysical Journal*, 986, 73.
  *Methods: "The IRIS observations were processed using packages available within the SolarSoft and irispy_lmsal software libraries."*
- https://doi.org/10.1051/0004-6361/202558068 — Dolliou, A., Peter, H., Mandal, S., Chitta, L. P., Teriaca, L., et al. (2026). Small-scale impulsive extreme-UV emission enhancements along network loops. *Astronomy & Astrophysics*, 709, A71.
  *Methods: "In this work the analysis of IRIS data was performed with the help of the irispy python package".*
- https://doi.org/10.3847/1538-4357/ae61ad — Lörinčík, J., Collier, H., Polito, V., Hayes, L. A., Ashfield, W., et al. (2026). Quasiperiodic Pulsations and Three-dimensional Magnetic Reconnection during 2022 March 31 Flare Observed by IRIS and STIX. *The Astrophysical Journal*, 1003, 95.
  *Methods: "Level-2 IRIS data were loaded and processed using the SolarSoft and irispy-lmsal libraries." Its sixth author is Nabil Freij, irispy's lead developer; the paper is a science study that uses irispy, not one about it (rule 3).*

*Literature search (ADS/SciX full text and acknowledgements, 2026-10-29): `full:"irispy"`, `full:"irispy-lmsal"` and `ack:"irispy"`. No record naming irispy was indexed after 2026-07-28: `full:"irispy" entdate:[2026-07-28 TO *]` finds none, while `full:"sunpy"` over the same dates (positive control) finds records and a nonsense token (negative control) finds none; `citations(doi:"10.5281/zenodo.10443678")` finds none. The papers above predate that date but this dossier had recorded no search, so they were weighed in this update.*

**Considered and excluded (audit trail):**
- Settled by the catalogue's maintainer on 2026-10-29: Zhu, Y., Harra, L., Barczynski, K., et al. (2025), *A&A*, 701, A205 (https://doi.org/10.1051/0004-6361/202555618), names irispy-lmsal only in its acknowledgements' list of the software used, without saying what it did — a list of tools (rule 6), as the ndcube entry's dossier decided for papers that name ndcube only in an acknowledgements roll-call. Excluded.
- Settled by the catalogue's maintainer on 2026-10-29: Cheung, M. C. M., Martínez-Sykora, J., Testa, P., et al. (2022), *ApJ*, 926, 53 (https://doi.org/10.3847/1538-4357/ac4223) is admitted only when the release's `calculate_moments` names it. At the v0.9.1post1 tag its References read "Færder et al. (2024), ApJ, Appendix C" while linking this paper's URL (`irispy/utils/moments.py:98`), so the release does not name it and it is excluded; the default branch after the tag names it as `cheung2022`, Appendix C, so the next release update should weigh it again.
- Settled by the catalogue's maintainer on 2026-10-29: De Pontieu, B., McIntosh, S. W., Hansteen, V. H., & Schrijver, C. J. (2009), *ApJ*, 701, L1 (https://doi.org/10.1088/0004-637X/701/1/L1) and Tian, H., McIntosh, S. W., De Pontieu, B., et al. (2011), *ApJ*, 738, 18 (https://doi.org/10.1088/0004-637X/738/1/18). The release does not cite them; the default branch's `calculate_red_blue_asymmetry` names them as the origin of the red–blue asymmetry technique and says it is not a port of either method, which does not make them the basis of the software. Excluded.
- Settled by the catalogue's maintainer on 2026-10-29: Pereira, T. M. D., Leenaarts, J., De Pontieu, B., et al. (2013), *ApJ*, 778, 143 (https://doi.org/10.1088/0004-637X/778/2/143) and Young, P. R., Tian, H., Peter, H., et al. (2018), *Space Science Reviews*, 214, 120 (https://doi.org/10.1007/s11214-018-0551-0), the method references of `calculate_mg_features` and of the UV-burst finders, are cited only by code on the default branch after v0.9.1post1, and the entry describes the release. Excluded; the next release update should weigh them under rule 4.
- Weighed under rules 5–6 and not added: Lörinčík et al. 2022, ApJ, 934, 80 (https://doi.org/10.3847/1538-4357/ac78e2), whose arXiv version (arXiv:2206.10114, the text read) says its data "were processed using the standard routines contained within the SolarSoft package in IDL and the IRISpy package (SunPy Community et al. 2020) in Python" — a credit that fits the older SunPy-affiliated IRISpy (now `sunraster`) as well as this package, so its identity is unconfirmed; Herde, V. L., Bose, S., et al., arXiv:2411.08801 ("Identifying Spicules in Mg II: Statistics and Comparisons with Hα"), whose v1 names "IRISpy" only in its "Software:" list (rule 6) and whose v2 withdraws the paper; the ndcube paper (Ryan et al. 2023, ApJ, 956, 44) and the SunPy 1.0 paper (2020, ApJ, 890, 68), which mention irispy as an ecosystem package (rule 6); and the meeting abstracts 2017SPD....4811508R, 2018tess.conf30711R, 2018AGUFMIN11B0628R, 2023SPD....5411020F and 2023AGUFMSH33E3099F and the proposals 2019hdee.prop....2R and 2020nsf....2025986Z, which are not eligible publication types (rule 1).
- The IRIS Technical Notes the release's docs and examples reference (ITN 1, 11, 20, 24, 26 and 32) have no DOIs, and `Calabretta & Greisen 2002` is cited in `docs/known_issues.rst` only for a WCS equation. Excluded.

*On the default branch after v0.9.1post1 (re-check at the next release; read at `134c2996b1db3887c9d9337a9338710440b0c1fb`): the documentation gains a bibliography (`docs/references.bib`, `docs/bibliography.rst`). Besides the papers settled above, it cites `polito2016` (Polito et al. 2016, https://doi.org/10.1051/0004-6361/201628965) for the O IV line physics the density example applies and `long2024` (Long et al. 2024, https://doi.org/10.3847/1538-4357/ad3234) for the figure the Mg II features example "attempt[s] to reproduce", neither cited by the functions themselves; general numerical, constant and textbook references — `cline1974` (Cline 1974, splines under tension, https://doi.org/10.1145/360924.360971, in the References of `calculate_mg_features`), `rybicki1985` (for the Planck function `radiation_temperature` inverts), `prohaska2022` (standard atomic weights), `dere2023` and `dufresne2024` (CHIANTI) and `calabretta2002` (the FITS WCS convention); background papers (`wulser2018`, `peter2014`, `dudik2017`, `moore1973` and the line-formation papers on `docs/line_database.rst`); and technical notes without DOIs. When they reach a release, weigh each from a site user's view: rule 4 names "the code's own reference block" as evidence without separating a domain method paper from a general numerical routine or a textbook, and is silent on an example's science references.*

### 28. Related Datasets (OPTIONAL)

*Evidence read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`.*

- https://doi.org/10.48322/k079-z133 — IRIS Level 2 Calibrated Images and Spectra Data (`spase://NASA/NumericalData/IRIS/Level_2/PT1S`).
  *Source note: the dataset irispy is built to read. `irispy/io/sji.py::read_sji_lvl2` and `irispy/io/spectrograph.py::read_spectrograph_lvl2` parse exactly these level-2 SJI and raster products; `docs/iris.rst` "we strongly recommend that everyone use the Level 2 data products".*
- https://doi.org/10.48322/agkq-fv14 — Co-aligned Interface Region Imaging Spectrograph (IRIS) and Solar Dynamics Observatory (SDO) Atmospheric Imaging Assembly (AIA) Observations (`spase://NASA/NumericalData/IRIS/Level_2/IRIS_SDO`).
  *Source note: irispy has a dedicated reader path and class for these — `read_files` recognises `*SDO.tar.gz` bundles and `INSTRUME` values starting with `AIA`, and `irispy.sji.AIACube` represents them; `examples/how_to/05_open_aia_cubes.py` ("Open the IRIS Aligned AIA Cubes").*

**Considered and excluded (audit trail):** IRIS Level 1 data (https://doi.org/10.48322/gdjv-sn12) — irispy does not read level 1; `docs/iris.rst` states level 1 "**MUST** be passed through the calibration routines `iris_prep.pro`" first (line 98). Co-aligned IRIS + Hinode (https://doi.org/10.48322/55gv-bg80) — `docs/tutorial/acquiring_data.rst` notes that the IRIS search finds observations with "co-aligned SDO and/or Hinode data cubes", but the release's `read_files` recognises only IRIS/SJI/AIA files, so it does not read them. Coordinated IRIS + SST (https://doi.org/10.48322/1mf1-nb89) — irispy reads no SST data, and the docs mention SST/CRISP only as format lineage (`docs/iris.rst:88` and `:122`). The shipped IRIS response file `iris_sra_c_20231106.geny` has no DOI.

*On the default branch after v0.9.1post1 (re-check at the next release; read at `134c2996b1db3887c9d9337a9338710440b0c1fb`): Hinode/SOT readers read the co-aligned IRIS and Hinode dataset above (`spase://NASA/NumericalData/IRIS/Level_2/IRIS_Hinode`), and `irispy.io.read_mosaic` reads the IRIS full-disk mosaics, which have no DOI — a DataCite search of the HPDE prefix 10.48322 for IRIS titles on 2026-10-29 returned only the five IRIS datasets named in this section — and no SPASE record (`hpde/NASA` `NumericalData/IRIS` holds `Level_1` and the four `Level_2` records PT1S, IRIS_SDO, IRIS_Hinode and IRIS_SST), so their landing page would be the IRIS team's page https://iris.lmsal.com/mosaic.html. Both pass rule 3 once released. The branch also ships a line catalog derived from the NIST Atomic Spectra Database and CHIANTI (`irispy/data/iris_lines.ecsv.gz`) and an IRIS bad-pixel table (`irispy/data/iris_sji_badpix_20260822.fits`), neither with an identifier of its own.*

### 29. Related Software (OPTIONAL)

- https://hesperia.gsfc.nasa.gov/ssw/iris/idl/ — SolarSoft (SSWIDL) IRIS analysis package.
  *Source note (read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`): the predecessor and functional counterpart irispy is explicitly written against. `irispy/utils/response.py`: "Goal is to replicate the base functionality of the IDL routine ``iris_get_response.pro`` in the SSWIDL package" and "…``fit_iris_xput.pro``… but without the optional keyword argument"; `irispy/utils/spectrograph.py`: "designed to do the same as `iris2/iris_calib_spectrum.pro`… The calibration output has been confirmed to provide the same results as those provided by the SolarSoft IDL routine `IRIS_CALIB`"; `docs/iris.rst` points to `iris_prep.pro` for level 1 → 1.5 processing; the shipped `irispy/data/test/get_cali_test_data.pro` generates the IDL reference data used to validate irispy's calibration against SSWIDL. No DOI or public VCS repository; the linked SSW IRIS IDL tree, which resolves, is the location cited by irispy itself. On the default branch after v0.9.1post1 (re-check at the next release; read at `134c2996b1db3887c9d9337a9338710440b0c1fb`) irispy ports more of the package — `iris_burst_check.pro` and `iris_sji_burst_check` (`irispy/utils/bursts.py`), `iris_get_mg_features.pro` (`irispy/utils/mg_features.py`), `iris_prep_wavecorr_l2` (`irispy/utils/wavelength_drift.py`) and the density bounds of `iris_ne_oiv.pro` — and its tests compare them with SolarSoft outputs written by further IDL scripts under `irispy/data/test/`.*

**Considered and excluded (audit trail):**
- Tier A generic infrastructure, excluded regardless of dependency status: numpy, scipy, pandas, matplotlib, setuptools, setuptools-scm, wheel, pooch, tqdm, pytest / pytest-astropy / pytest-mpl, sphinx and all sphinx extensions.
- `dask` — a hard dependency and genuinely exercised (`irispy/utils/cosmic_rays.py` branches on `dask.array` inputs; `parallel_fit_dask` in the fitting examples), but parallel/lazy arrays are generic infrastructure that would be equally at home outside science. Excluded from both fields.
- `rsliding` — the default cosmic-ray backend (`rsliding.SlidingSigmaClipping`), but it is a general sliding-window sigma-clipping/mean/median/stddev utility (PyPI summary), i.e. generic numerical infrastructure. Excluded.
- `mpl-animators` — `IRISArrayAnimatorWCS` subclasses `mpl_animators.ArrayAnimatorWCS`, but it is a general matplotlib animation helper rather than a domain tool. Excluded.
- `asainz-solarphysics/IRIS-LMSALpy` — a nominally similar-purpose IRIS Python effort, but a stub (no README, last push 2018, 0 stars). Not distinguishing; excluded.
- `sunkit-instruments` — similar in spirit (SunPy-affiliated instrument-specific tools) but has no relationship to irispy in code or docs. HSSI's sunkit-instruments entry lists irispy as related software; the release does not mention sunkit-instruments at all (the default branch after it names it only in a test-data provenance line, `irispy/data/test/unparsable_card/overview.txt`), so the relation stays one-directional. Excluded.
- `colorsynth` — the optional `rgb` extra behind `irispy.utils.rgb.calculate_rgb`/`plot_rgb` (`colorsynth.rgb_and_colorbar`, v0.9.0), but a general library "for creating false-color images from arrays of spectral radiance" (PyPI summary) that would serve any spectral imaging; generic infrastructure (Field 30 rule 2). Excluded from both fields.
- `LM-SAL/irispy-data` — release assets of cut-down IRIS files that the documentation and the remote-data tests download (v0.9.1); a data and test-fixture repository, not related software. Excluded.
- `iris_lmsalpy` — another IRIS Python package from LMSAL, named beside irispy in third-party methods sections (Field 27), but irispy's own sources do not name it (Field 29 rule 4). Excluded.
- Packages that met the Field 30 bar (sunpy, ndcube, sunraster, astropy, gwcs, dkist, fiasco, aiapy, sunkit-image, astroscrappy) are listed there rather than duplicated here.

### 30. Interoperable Software (OPTIONAL)

- https://github.com/sunpy/sunpy — `irispy.sji.SJICube.to_maps()` converts IRIS cubes into `sunpy.map.Map` / `MapSequence` objects (documented adapter API, used in `examples/coalign/01_coalign_iris_aia.py`); readers construct headers with `sunpy.map.header_helper.make_fitswcs_header` and coordinate frames with `sunpy.coordinates` (`Helioprojective`, `get_body_heliographic_stonyhurst`); SJI colour tables come from `sunpy.visualization.colormaps.color_tables.iris_sji_color_table`; sample data uses `sunpy.util.parfive_helpers.Downloader`. Read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`. *On the default branch after v0.9.1post1 (re-check at the next release), `irispy.net.IRISClient` is a `sunpy.net.Fido` client — a plugin relationship — that `import irispy.net` adds to `Fido`.*
- https://github.com/sunpy/ndcube — shared NDCube data model: `irispy.spectrograph.RasterCollection` subclasses `ndcube.NDCollection`, `read_files` returns an `NDCollection`, `irispy.visualization.IRISPlotter` subclasses `ndcube.visualization.mpl_plotter.MatplotlibPlotter` and the IRIS plotters are registered through ndcube's plotter framework (v0.9.0), and `SpectrogramCube._fits_wcs` uses `ndcube.wcs.tools.unwrap_wcs_to_fitswcs`.
- https://github.com/sunpy/sunraster — shared spectrogram data model: `irispy.spectrograph.SpectrogramCube` and `irispy.sji.SJICube` subclass `sunraster.SpectrogramCube`, and `SpectrogramCubeSequence` subclasses `sunraster.SpectrogramSequence`, so IRIS cubes are usable anywhere sunraster objects are. (Lineage note: `github.com/sunpy/irispy` now redirects to `sunpy/sunraster` — sunraster is the generalised descendant of the original irispy, and this package is the IRIS-specific library built on top of it.)
- https://github.com/astropy/astropy — the public interchange types are astropy's: cube data carry `astropy.units` `Quantity` units (`irispy/utils/constants.py` defines `DN_IRIS_*` units and `RADIANCE_UNIT`), `astropy.time.Time` coordinates, `astropy.coordinates.SkyCoord`, `astropy.wcs.WCS`, and `astropy.nddata.StdDevUncertainty`; `irispy.utils.gaussian1d_on_linear_bg` is a public `astropy.modeling` `custom_model` intended to be fit with astropy fitters (`LMLSQFitter`/`TRFLSQFitter` in `examples/analysis/01_spectral_fitting.py` and `07_mg_ii_two_gaussian_fitting.py`). Read at the v0.9.1post1 tag; on the default branch after it, `irispy.utils.fitting` replaces that model with `line_model`, `starts_from_model` and `maps_from_fit` around `astropy.modeling.fitting.parallel_fit_dask`.
- https://github.com/spacetelescope/gwcs — `irispy/io/sji.py::_create_gwcs` builds and returns a `gwcs.WCS` (with `gwcs.coordinate_frames` `CelestialFrame`/`TemporalFrame`/`CompositeFrame`) that is exposed as `SJICube.wcs`, so IRIS SJI cubes hand a fully-formed gWCS object to any gwcs-aware consumer.
- https://github.com/DKISTDC/dkist — `irispy/io/sji.py` imports `dkist.wcs.models.VaryingCelestialTransform` and `CoupledCompoundModel` and composes them into the IRIS per-exposure gWCS forward transform; DKIST's WCS model objects are embedded in irispy's public WCS.
- https://github.com/wtbarnes/fiasco — `irispy.utils.density.density_diagnostic(..., ion=<fiasco.Ion>)` takes fiasco `Ion` objects and calls `fiasco.line_ratio(ion, numerator, denominator, density_grid)` to build the theoretical curve it inverts; declared as the optional extra `irispy-lmsal[density]`; demonstrated in `examples/analysis/06_oiv_density_diagnostics.py` and covered by `irispy/utils/tests/test_density.py`. Read at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`. *On the default branch after v0.9.1post1 (re-check at the next release), `density_diagnostic` takes the theoretical curve as an argument instead and the `density` extra is gone; the density example and the docstring still compute that curve with fiasco, a fiasco output passed into irispy (Field 30 rule 7), so the entry would stand.*
- https://github.com/LM-SAL/aiapy — `examples/coalign/01_coalign_iris_aia.py` and `02_reproject_iris_roll_aia.py` use `aiapy.calibrate.update_pointing` and `aiapy.calibrate.utils.get_pointing_table` to prep the AIA maps that IRIS data are then co-aligned/reprojected against; declared in the `docs` extra. (Also the closest sibling package: same LM-SAL organisation, same sunpy package template, same mission-specific analysis role for SDO/AIA.)
- https://github.com/sunpy/sunkit-image — `examples/coalign/01_coalign_iris_aia.py` passes the `sunpy.map.Map` produced by `SJICube.to_maps()` into `sunkit_image.coalignment.coalign_map`; declared in the `docs` extra; `CHANGELOG.rst` 0.6.0 records "an example to demonstrate co-alignment of IRIS SJI and SDO/AIA images using sunkit-image's ``match_template`` method".
- https://github.com/astropy/astroscrappy — a user-selectable backend of irispy's public API: `remove_cosmic_rays(method="astroscrappy")` hands each frame and mask to `astroscrappy.detect_cosmics` and consumes the cleaned frame (`irispy/utils/cosmic_rays.py`); declared as the optional extra `irispy-lmsal[cosmic-rays]`; demonstrated in `examples/calibration/02_remove_spikes_sji.py` (this entry earlier cited `01_remove_spikes_sg.py`, which uses the `rsliding` backend) and tested in `irispy/utils/tests/test_cosmic_rays.py`.

*Exclusions are recorded in the Field 29 audit trail above (Tier A generic stack, dask, rsliding, mpl-animators, colorsynth). HSSI's sunraster and ndcube entries list irispy as interoperable software, which the sunraster and ndcube entries here reciprocate. No entry here rests on Field 30 rule 3's blanket justifications, "part of the standard scientific Python ecosystem" or "a PyHC member, so it interoperates with PyHC packages".*

### 31. Related Instruments (OPTIONAL)

Each instrument is supported directly by the package and carries its canonical SPASE identifier.

- **Instrument Name:** Interface Region Imaging Spectrograph
  **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/IRIS/IRIS
  *Resolution: exactly one `type=1` row matches on name, on abbreviation `IRIS`, and on the identifier path segments `IRIS/IRIS`. Canonical `name` copied verbatim from the matched row. Designed-to-support evidence: the entire package reads, calibrates, models the response of, and visualises this instrument's SJI and SG level-2 data (`irispy/io/sji.py`, `irispy/io/spectrograph.py`, `irispy/utils/response.py`, `irispy/utils/spectrograph.py`, `irispy/obsid.py`, `irispy/meta.py`). The fetched SPASE record confirms the match ("multi-channel imaging spectrograph with a 20 cm UV telescope… spectra along a slit… and slit-jaw images").*
- **Instrument Name:** Atmospheric Imaging Assembly
  **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SDO/AIA
  *Resolution: exactly one `type=1` row now matches, the bare `.../SDO/AIA` (name "Atmospheric Imaging Assembly", abbreviation `AIA`), and its `name` is copied verbatim. When this entry was first resolved the vocabulary also held an `.html` variant, `.../SDO/AIA.html` (name "Atmospheric Imaging Assembly (AIA)"); the bare identifier was chosen under the `.html` normalisation rule, and the vocabulary fetched on 2026-10-29 no longer holds the `.html` row. Designed-to-support evidence (at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`): irispy has a dedicated `irispy.sji.AIACube` class; `read_sji_lvl2` is documented as reading "a SINGLE level 2 SJI FITS or the IRIS aligned AIA Cube" and returns an `AIACube` for an AIA file; `read_files` extracts `*SDO.tar.gz` AIA bundles and accepts `INSTRUME` values starting with `AIA`; `examples/how_to/05_open_aia_cubes.py`, `examples/coalign/01_coalign_iris_aia.py` and `02_reproject_iris_roll_aia.py` read, co-align and reproject AIA data; the co-aligned IRIS+AIA dataset is listed in Field 28. Cross-entry consistency confirmed: HSSI's existing aiapy entry stores this same instrument as name "Atmospheric Imaging Assembly" with identifier `https://spase-metadata.org/SMWG/Instrument/SDO/AIA` — the bare form used here, so the two entries agree.*

**Considered and excluded (audit trail):**
- IRIS SJI and SG are not listed as separate instruments: SPASE models IRIS as a single instrument (`SMWG/Instrument/IRIS/IRIS`) with both light paths, and there are no sub-instrument rows to expand into.
- Hinode instruments (e.g. XRT, EIS, SOT) — `docs/iris.rst` mentions that level 2/3 formats are "analyzed using tools adapted from Hinode/EIS and SST/CRISP" and `docs/tutorial/acquiring_data.rst` notes co-aligned Hinode cubes are searchable, but the release's `read_files` recognises only IRIS/SJI/AIA `INSTRUME` values and `SDO.tar.gz` archives. Mention only, not designed-to-support. Excluded.
- SST/CRISP — irispy reads no SST data; the docs mention SST/CRISP only as format lineage (`docs/iris.rst:88` and `:122`). Excluded.
- SDO/HMI and SDO/EVE — present in the vocabulary but never referenced by irispy. Excluded.
- FITS generally → Field 18 (Input File Formats), not an instrument.

*On the default branch after v0.9.1post1 (re-check at the next release; read at `134c2996b1db3887c9d9337a9338710440b0c1fb`): `irispy.sji.SOTCube` holds "Hinode/SOT image and magnetic data supplied with IRIS observations", and `read_files` reads the `sot_l2_*`/`sotsp_l2_*` files and the `SOTFG.tar.gz`/`SOTSP.tar.gz` archives, with a branch for `instrume == "SOT-SP"`: designed-to-support once released. It would resolve to exactly one `type=1` row, "Solar Optical Telescope", `https://spase-metadata.org/SMWG/Instrument/Hinode/SOT` (empty abbreviation); a sweep of the vocabulary's names, abbreviations, identifiers and definitions on 2026-10-29 for "Hinode", "Solar-B" and "Solar Optical Telescope" found only the Hinode EIS, SOT and XRT instrument rows and the Hinode observatory row, and none for its filtergraph or spectro-polarimeter.*

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
- Hinode and the Swedish 1 m Solar Telescope — the release's documentation mentions co-aligned Hinode cubes and SST/CRISP format lineage only; no reader. Excluded (see Field 31).
- The Virtual Solar Observatory and CDAWeb-style archives — data sources, recorded in Field 17, not observatories.

*On the default branch after v0.9.1post1 (re-check at the next release): with the Hinode/SOT readers noted under Field 31, Hinode would resolve to exactly one `type=2` row, "Hinode", `https://spase-metadata.org/SMWG/Observatory/Hinode`, listed beside its instrument on the same footing as SDO beside AIA.*

### 33. Logo (OPTIONAL)
Not found

*Source note (re-checked at the v0.9.1post1 tag `2b3229016ae5962a9ebbc5f9ec631bfbc00be67c`): the repository contains no software logo. `docs/_static/images/` holds `iris_spacecraft.jpg` and `iris_instrument.jpg` (schematic diagrams of the satellite and its optical paths) and, under `tutorial/`, screenshots of the IRIS search page and of fiducial marks; the docs' link-preview image and gallery thumbnails use SunPy's mark, which belongs to the parent project (Field 33 rule 5); and the PyHC registry entry for `irispy-lmsal` has no `logo` field. The banner image at `https://raw.githubusercontent.com/LM-SAL/irispy/refs/heads/main/iris_full.jpg` is deliberately excluded: it is a photograph of the IRIS spacecraft rather than a logo for the software.*
*On the default branch after v0.9.1post1 (read at `134c2996b1db3887c9d9337a9338710440b0c1fb`; re-check at the next release), also rejected: the Lockheed Martin Solar and Astrophysics Laboratory logo `docs/_static/images/lmsal_logo.png` (a Sun with field lines and the words "Solar and Astrophysics Lab"; pinned `https://raw.githubusercontent.com/LM-SAL/irispy/134c2996b1db3887c9d9337a9338710440b0c1fb/docs/_static/images/lmsal_logo.png`, `image/png`, 201,001 bytes), added after v0.9.1post1 as the gallery's default thumbnail and, as `https://lmsal.com/images/lmsal_logo_highres_small.png`, the documentation's link-preview image. The project calls it "the LMSAL logo" (`changelog/217.doc.rst`) and does not set it as `html_logo`; it is the developing institution's mark, not irispy's (Field 33 rule 5). The published documentation's header shows the SunPy theme's icon (`_static/sunpy_icon.svg`), which belongs to the theme (rule 5). Not recorded; a curator may adopt it deliberately.*
