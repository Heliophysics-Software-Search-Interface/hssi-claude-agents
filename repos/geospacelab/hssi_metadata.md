# HSSI Metadata Extraction Results

**HSSI Software ID:** 91f97996-69a3-43b8-bdfc-20895502415f
**Repository:** https://github.com/JouleCai/geospacelab
**Source Revision:** 213bbc22d47a5254584581b06692cb7e2cb65d76
**Extraction Date:** 2026-07-29
**Validation Date:** 2026-08-26
**Validation Status:** PASS

> **Field 12 is a bare version number.** The stored value is `v0.14.15`. Rendered HSSI output
> prefixes it with the software name (`GeospaceLAB - v0.14.15`); that prefix is presentation
> only and is not part of the version metadata.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Note:** The original submitter is not part of the published metadata, so the placeholder is retained.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.5377318

**Source:** Confirmed against CITATION.cff, repo `datacite.json`, and the Zenodo API (`conceptdoi` of record 20439561 is `10.5281/zenodo.5377318`). This is the concept DOI covering all versions.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/JouleCai/geospacelab

**Source:** Confirmed against CITATION.cff, `setup.py` (`url=`), PyPI `home_page`, Zenodo `custom_fields["code:codeRepository"]`, and PyHC `code`.

### 4. Software Functionality (MANDATORY)
**Values:**
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:2D Slices
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:Field-line Tracing
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Spectrogram
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:2D Slices
- Data Visualization:Line Plots
- Data Visualization:Mission-Specific
- Data Visualization:Orbit Plots
- Data Visualization:Spectrogram
- Models and Simulations
- Models and Simulations:Empirical
- Models and Simulations:Field-line Tracing

**Source:** Direct analysis of the packaged code at revision `213bbc2` (437 Python modules), plus README, docs, and the test suite. Every child value has its parent category present.

**Evidence:**
- *Coordinate Transforms* (+ *Ionospheric*, *Magnetospheric*): `geospacelab/cs/` defines `GEO`, `GEOD`, `GEOC` (spherical/Cartesian), `LENU` (local east-north-up), `AACGM`, `APEX`, dispatched by the public `cs.set_cs()`. Ionospheric: `_aacgm.py`, `_apex.py`, `Dataset.convert_to_APEX()` / `convert_to_AACGM()`, MLT/MLON mapping in the polar map panels. Magnetospheric: `geospacelab/wrapper/geopack/geopack.py` exposes `geogsm`, `gsmgse`, `smgsm`, `magsm`, `geomag`, `geigeo`, `gswgsm`, `geodgeo`, `sphcar` (GEO/GEI/MAG/SM/GSM/GSE).
- *Data Processing and Analysis:Data Access and Retrieval*: 14 backend directories under `geospacelab/datahub/sources/`, of which 13 are active (cdaweb, esa_eo, fmi, gfz, isee, jhuapl, madrigal, ncei, nipr, superdarn, supermag, tud, wdc), each with `downloader.py` + `loader.py`, driven by `DataHub.dock()`. The fourteenth, `noaa`, contains only empty placeholder `__init__.py` files and is excluded throughout this record.
- *Analysis*: `observatory/orbit/conjunction.py` (`conjunction_leo_to_site`, `calc_big_circle_distance`, `calc_el`, `calc_az`), `Dataset.get_conjunction_with_site()` (see `test/test_swarm/test_conjuctions.py`), `observatory/orbit/utilities.py::LEOToolbox.search_orbit_nodes` / `group_by_sector` / `trajectory_local_unit_vector`.
- *Processing*: the `DataHub` / `Dataset` / `Variable` pipeline in `geospacelab/datahub/__init__.py`; post-load derivation hooks (`calc_lat_lon`, `add_GEO_LST`, `add_SC_sun_position`).
- *Time Series Analysis*: `LEOToolbox.filter_by_time`, `smooth_along_track` / `smooth_savgol` (`scipy.signal.savgol_filter`), `Dataset.time_filter_by_range()`, automatic time-gap detection and adaptive time ticks in `visualization/mpl/axis_ticks.py`.
- *Spectrogram* (processing) and *Spectrogram* (visualization): DMSP SSJ energy-channel spectrogram arrays are constructed in `datahub/sources/madrigal/satellites/dmsp/e/loader.py` (`ENERGY_CHANNEL_GRID` built from `CH_CTRL_ENER` half-spacing) and rendered by `TSPanel._retrieve_data_2d` / `overlay_pcolormesh`; EISCAT range-time-intensity quicklooks likewise.
- *Data Processing and Analysis:2D Slices*: 2D field extraction and regridding via `toolbox/utilities/numpyarray.py::regridding_2d_xgaps` and `data_resample_2d`, producing the fixed-altitude 2D arrays that the polar map then renders. (Weakest of the retained values — see Notes.)
- *Data Visualization* (+ *2D Graphics*, *Line Plots*, *Orbit Plots*): `visualization/mpl/` — `TSPanel.overlay_line` / `overlay_bar` / `overlay_pcolormesh`, `geomap/geopanels.py::PolarMapPanel.overlay_pcolormesh` / `overlay_contour` / `overlay_gridlines` / `overlay_coastlines` / `overlay_lands`; orbit: `overlay_sc_trajectory`, `overlay_cross_track_vector`, `overlay_sc_coloured_line`, `overlay_vectors`.

**Further per-value evidence:**
- *Data Processing and Analysis:Data Reduction* — `toolbox/utilities/binning.py` (`binning1d`, `binning1d_moving`), `numpyarray.py` (`data_resample`, `data_resample_2d`, `regridding_2d_xgaps`), `LEOToolbox.griddata_by_sector` / `griddata_by_sector_v2`, and the public `Dataset.gridding(...)` API with `along_track_binning_method='mean'`, `along_track_binning_step`, `y_grid_res`. Exercised end-to-end by `test/test_swarm/test_gridding.py` (`test_gridding_binning_FAC_TMS`, `test_gridding_interpolation_DNS_POD`). This is one of the capabilities added in the v0.12–v0.14 series.
- *Data Processing and Analysis:Energy Spectra* — DMSP SSJ precipitating-particle products: `datahub/sources/madrigal/satellites/dmsp/e/loader.py` derives the energy-channel grid, and `variable_config.py` defines `JE_e`/`JE_i` ("Integrated energy flux of electrons/ions") and `E_e_MEAN`/`E_i_MEAN` ("Mean energy of electrons/ions"), plotted by `express/dmsp_dashboard.py`.
- *Data Processing and Analysis:Field-line Tracing* — `wrapper/geopack/geopack.py::trace(xi, yi, zi, dir, rlim, r0, parmod, exname, inname)` with `step`/`rhand` RK integration, tracing through an external model (`t89`/`t96`/`t01`/`t04`) plus an internal IGRF field.
- *Data Processing and Analysis:File Format Conversion* — downloaders retrieve one format and persist another: WDC Dst/AE/ASY-SYM fetch IAGA2002 ASCII then `save_to_netcdf()` (`datahub/sources/wdc/*/downloader.py`); the same ASCII-to-netCDF conversion is implemented for GFZ Kp/Ap, Hpo and SNF107, SuperDARN POTMAP, and SuperMAG indices/magnetometer.
- *Data Processing and Analysis:Image Processing* — `datahub/sources/nipr/asc/tro_wmi/loader.py` reads all-sky camera JPG frames with `plt.imread` and extracts the 558 nm monochromatic channel; `tro_wmi/__init__.py::calc_lat_lon()` geolocates every image pixel by converting azimuth/elevation/range through `LENUSpherical` into GEO and then AACGM/APEX. DMSP SSUSI auroral images are gridded and regridded for map overlay (`overlay_pcolormesh(..., regridding=...)`).
- *Data Visualization:2D Slices* — the *rendering* of those slices is a distinct capability with its own vocabulary row: `visualization/mpl/geomap/geopanels.py::PolarMapPanel.overlay_pcolormesh` / `overlay_contour` display a fixed-altitude 2D cut of the ionosphere on a polar projection (README Example 4 renders the SSUSI LBHS slice this way), and `PolarSectorPanel` does the same for a longitude/MLT sector. The `FunctionCategory` vocabulary carries two distinct `2D Slices` rows, one parented to *Data Processing and Analysis* and one to *Data Visualization*.
- *Data Visualization:Mission-Specific* — `geospacelab/express/` provides curated per-instrument quicklook layouts: `EISCATDashboard.quicklook()` (explicitly reproducing the official EISCAT online quicklook format, per README Example 2), `DMSPTSDashboard.quicklook()`, `MillstoneHillISRDashboard.quicklook()`, `OMNIDashboard.quicklook()`.
- *Models and Simulations* + *Models and Simulations:Empirical* — `geospacelab/wrapper/geopack/` bundles the Tsyganenko empirical external magnetospheric field models `t89.py`, `t96.py`, `t01.py`, `t04.py`, the IGRF internal field (`init_igrf`, `load_igrf`, `igrf_gsm`, `igrf_geo`, `igrf_gsw`, `dip`), and the Shue et al. and T96 empirical magnetopause models (`shuetal_mgnp`, `t96_mgnp`).
- *Models and Simulations:Field-line Tracing* — the same `trace()` entry point, tracing within those model fields rather than within observational data.

**Not applicable, and why:**
- *Data Visualization:3D Graphics* — the only `mpl_toolkits.mplot3d` use is `geospacelab/future/test_sscws.py`, an unreleased experimental module, not packaged user-facing functionality.
- *Data Visualization:Web-Based* — `visualization/plotly/ipanel.py` exists but every method body is `pass`; it is a placeholder, not a capability.
- *Data Visualization:Movies* — no `matplotlib.animation` / frame-export code anywhere.
- *Data Visualization:Spacecraft Formation Plots* — dual-satellite Swarm FAC products are read, but no constellation-geometry or formation-quality plotting exists.
- *Data Processing and Analysis:ML/AI*, *Wavelet Analysis*, *Data Assimilation*, *Curlometer*, *Pitch Angle Distributions*, *Plasma Moments*, *Packet Decommutation* — no matching code (grep for `sklearn|tensorflow|torch|keras`, `pywt|pycwt|wavelet`, `kalman|assimilat`, `curlometer`, `pitch_angle` returns nothing outside `future/`).
- *Data Processing and Analysis:Calibration* — the only `calibrat*` matches are Tsyganenko docstrings and the SSUSI `CALIBRATION_PERIOD_VERSION` metadata field being read; no calibration is performed.
- *Coordinate Transforms:Mission-Specific* — `LEOToolbox.trajectory_local_unit_vector` and `overlay_cross_track_vector` build an along-/cross-track satellite frame, but it is a generic LEO-relative frame, not a mission- or instrument-specific frame (no SPICE kernels, attitude, or FOV modelling). Borderline; excluded as the more defensible call.
- *Mission-related* (all subcategories) — GeospaceLAB is an independent analysis framework, not part of any mission ground system or science data pipeline.
- *Servers and Environments* (all subcategories) — no Dockerfile, no MPI/`mpi4py`, no server or HPC job code.

### 5. Related Region (MANDATORY)
**Values:**
- Earth Atmosphere
- Earth Auroral Subregion
- Earth Ionosphere
- Earth Magnetosphere
- Earth Thermosphere
- Interplanetary Space
- Solar Wind

**Source:** Repository evidence below supports all seven values.
**Evidence:**
- **Earth Atmosphere** — umbrella for the neutral/ionised upper atmosphere products below.
- **Earth Magnetosphere** — AMPERE field-aligned currents, Swarm FAC/AOB_FAC/PPI_FAC, SuperDARN convection, Dst/AE/ASY-SYM/Kp indices, Tsyganenko magnetospheric field models.
- **Interplanetary Space** — CDAWeb/OMNI solar wind and IMF.
- **Earth Ionosphere** — EISCAT/Millstone Hill/PFISR/RISR-N incoherent scatter `n_e`, `T_e`, `T_i`, `v_i_los`; Madrigal and ISEE GNSS TEC maps; Swarm `EFI_LP_HM`, `EFI_TCT02/16`, `IBI_TMS`, `IPD_IRR`, `MIT_LP`, `MIT_TEC`, `TEC_TMS`.
- **Earth Thermosphere** — TU Delft neutral density and neutral wind from accelerometer/GPS for CHAMP, GRACE, GRACE-FO, GOCE and Swarm (`tud/*/dns_acc`, `dns_pod`, `wnd_acc`); Swarm `DNS_ACC`/`DNS_POD`.
- **Earth Auroral Subregion** — DMSP/SSUSI auroral emission (`EDR_AUR`, LBHS/LBHL bands), DMSP SSJ auroral precipitation energy flux, Swarm auroral oval boundary (`AOB_FAC_2F`) and auroral electrojet products (`AEJ_LPL`, `AEJ_LPS`, `AEJ_PBL`, `AEJ_PBS`), FMI IMAGE electrojet indices, NIPR Tromsø all-sky auroral imager.
- **Solar Wind** — the CDAWeb/OMNI backend is a core built-in capability and its variables are solar-wind plasma and interplanetary magnetic field quantities in the strict sense: `sources/cdaweb/omni/variable_config.py` defines `v_sw` (line 162, `fullname = 'Solar wind speed'`), `n_p` (proton density, line 184) and `p_dyn` (dynamic pressure, line 208); `omni/loader.py:49-51` derives the IMF components `B_x_GSM`, `B_T_GSM` and `B_TOTAL`; `omni/__init__.py:42-45` places `SC_ID_IMF`, `IMF_PTS`, `B_x_GSM`, `B_y_GSM`, `B_z_GSM`, `B_T_GSM` in the default variable set; and `omni/__init__.py:222` exposes the IMF clock-angle helper `add_IMF_CA()` (with `add_IMF_AZ()` and `add_IMF_EL()` alongside). Surfaced through the `OMNIDashboard` express quicklook (README Example 3) and `test/test_omni.py`.
  `Solar Wind` is the more specific region for these measurements; `Interplanetary Space` is retained alongside it, as `Earth Atmosphere` is retained alongside the finer Earth regions.

**Considered and excluded:** *Solar Environment* — the NOAA/SWPC `goesxray` and `solarwind` modules are empty placeholder `__init__.py` files (0 bytes); GFZ F10.7 and sunspot number are ingested only as geospace drivers, not as solar-region science functionality. *Planetary Magnetospheres* — all coordinate systems and models are Earth-specific.

### 6. Authors (MANDATORY)

#### Author 1
- **Authors:** Lei Cai
- **Author Identifier:** https://orcid.org/0000-0003-0127-7303
- **Affiliation:**
  - **Organization:** University of Oulu
  - **Affiliation Identifier:** https://ror.org/03yj89h83

**Source:** Lei Cai is the sole software author. Five independent software-authorship sources agree: `CITATION.cff`, the repository's `datacite.json`, the Zenodo record for v0.14.15, the DataCite record for `10.5281/zenodo.20439561`, and `setup.py` (`author='Lei Cai'`, `author_email='lei.cai@oulu.fi'`).

**Publication co-authors, recorded for provenance.** The reference publication (Cai et al. 2022, Field 14) has eight authors, per Crossref: Lei Cai, Anita Aikio, Anita Kullen, Yue Deng, Yongliang Zhang, Shun-Rong Zhang, Ilkka Virtanen, Heikki Vanhamäki (Crossref supplies no ORCIDs). Affiliations from the article: University of Oulu (Cai, Aikio, Virtanen, Vanhamäki); KTH Royal Institute of Technology (Kullen); University of Texas at Arlington (Deng); Johns Hopkins University Applied Physics Laboratory (Y. Zhang); Massachusetts Institute of Technology Haystack Observatory (S.-R. Zhang). These are authors of the paper, not of the software, and are not listed in Field 6.

### 7. Software Name (MANDATORY)
**Value:** GeospaceLAB

**Source:** Matches CITATION.cff `title`, Zenodo/DataCite title, PyHC `name`, and the README heading. Editorial wording preserved.

### 8. Description (MANDATORY)
**Value:** GeospaceLAB provides a framework of data access, analysis, and visualization for researchers in space physics and space weather. It features a class-based data manager (DataHub, Dataset, Variable), extendable architecture for adding new data sources, comprehensive visualization tools for time series and map projections (including polar views with AACGM coordinates), space coordinate system transformations, and built-in support for numerous data sources including CDAWeb/OMNI, Madrigal/EISCAT, DMSP/SSUSI, ESA SWARM, AMPERE, SuperDARN, and various geomagnetic indices. More recent releases add extensive coverage of the ESA Swarm mission with around thirty supported data products, gridding and binning of satellite measurements by orbit sector, satellite-to-ground conjunction search, and data retrieval through the HAPI and VirES interfaces.

**Source:** The description opens with the curator-authored text, preserved verbatim, and closes with one sentence covering capabilities added in the v0.14 series that the original predates.
**Evidence for the closing sentence:** ~30 Swarm products — 31 implemented product modules under `datahub/sources/esa_eo/swarm/{l1b,advanced,l2daily}`, each several hundred to >1,700 lines, with 22 dedicated test modules in `test/test_swarm/`. Orbit-sector gridding/binning — the public `Dataset.gridding(sector=…, along_track_binning=…, y_grid_res=…)` API, exercised by `test/test_swarm/test_gridding.py`. Conjunction search — `observatory/orbit/conjunction.py::conjunction_leo_to_site` surfaced as `Dataset.get_conjunction_with_site()`, exercised by `test/test_swarm/test_conjuctions.py`. HAPI/VirES — `esa_eo/swarm/loader.py::load_from_HAPI` / `load_from_VirES` (see Fields 17 and 30).

### 9. Concise Description (OPTIONAL)
**Value:** A Python framework for managing and visualizing data in space physics, with built-in support for numerous data sources including EISCAT, DMSP, SWARM, OMNI, and geomagnetic indices.

**Source:** Retained verbatim from the established record (180 characters, within the 200-character limit). Still accurate; editorial wording preserved.

### 10. Publication Date (RECOMMENDED)
**Value:** 2021-03-13

**Source:** GitHub repository creation date. The first Zenodo-archived release followed on 2021-09-02; the earlier date is retained as the date of first publication of the initial version.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite gives `publisher: "Zenodo"` for both the concept and version DOIs. The submission form permits a URL as the publisher identifier where no ROR is used, so `https://zenodo.org` is a valid identifier for this field. Zenodo also has a ROR, `https://ror.org/04aj4c181`, which is an equivalent alternative.

### 12. Version (RECOMMENDED)

#### Latest Version
- **Version Number:** v0.14.15
- **Version Date:** 2026-05-29
- **Version Description:** Support for 30 Swarm data products, with separate GeospaceLAB-Swarm documentation at https://geospacelab-swarm.readthedocs.io/en/latest/; improved dependency compatibility.
- **Version PID:** https://doi.org/10.5281/zenodo.20439561

**Source — four authoritative sources agree:**
1. **Zenodo API** (primary, used for the version PID): resolving the concept record `5377318` returns latest record `20439561`, `metadata.version = "v0.14.15"`, `publication_date = 2026-05-29`.
2. **DataCite API** for `10.5281/zenodo.20439561`: `version = "v0.14.15"`, `dates = [{date: "2026-05-29", dateType: "Issued"}]`, `IsVersionOf 10.5281/zenodo.5377318`, `IsSupplementTo https://github.com/JouleCai/geospacelab/tree/v0.14.15`.
3. **PyPI**: `info.version = 0.14.15`, sdist/wheel uploaded 2026-05-29T06:20:02.
4. **Git tags in this repository**: `v0.14.15` is the newest tag, dated 2026-05-29; `geospacelab/__init__.py` declares `__version__ = "0.14.15"`.

The version description follows the Zenodo/DataCite release abstract for v0.14.15. The version PID is the **version-specific** DOI (`zenodo.20439561`), not the concept DOI. The version number is a bare string, `v0.14.15`; the software-name prefix in rendered HSSI output is presentation only.

#### Release history
- The preceding recorded version was `v0.11.0` (2025-06-13, PID `https://doi.org/10.5281/zenodo.15656924`). Releases since: v0.12.0 (2026-01-30), v0.13.0 (2026-02-20), v0.14.0 (2026-05-18), v0.14.13 (2026-05-28), v0.14.14 and v0.14.15 (2026-05-29).
- `CITATION.cff` is stale at `version: 0.5.10` / `date-released: 2023-02-15` and is **not** the version source for this record. (Upstream repository observation.)

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** Confirmed by 437 `.py` files and no other source-language files in the package tree (`find geospacelab -type f | sed 's/.*\.//' | sort | uniq -c` yields only `py`, plus data/doc assets). `setup.py` declares `python_requires='>=3.12'` with classifiers for Python 3.12, 3.13 and 3.14.
**Note:** The minimum Python has risen from `>=3.7` (recorded in the 2025-10-09 file) to `>=3.12`. This does not change the HSSI field value, which has no minor-version granularity.

### 14. Reference Publication (RECOMMENDED)
**Value:** https://doi.org/10.3389/fspas.2022.1023163

**Source:** Confirmed against the README "Citation" section, `docs/citation.rst`, and Crossref.
**Full citation:** Cai, L., Aikio, A., Kullen, A., Deng, Y., Zhang, Y., Zhang, S.-R., Virtanen, I., & Vanhamäki, H. (2022). GeospaceLAB: Python package for managing and visualizing data in space physics. *Frontiers in Astronomy and Space Sciences*, 9, 1023163.
**Note:** HSSI may associate a placeholder display name `UNKNOWN` with this DOI internally; the DOI is the durable identity and no separate name correction is needed.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause

**Source:** DataCite `rightsList[0].rights` for the v0.14.15 DOI supplies this license and `rightsIdentifier: bsd-3-clause` under the SPDX scheme. Corroborated by the repository `LICENSE` file and `setup.py` (`license='BSD 3-Clause License'`).
**SPDX Identifier:** BSD-3-Clause

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- all-sky imager
- ampere
- analysis
- aurora
- auroral electrojet
- coordinate transformation
- data access
- data analysis
- data container
- data retrieval
- dmsp
- eiscat
- field-aligned currents
- geospace
- gnss
- hapi
- heliophysics
- incoherent scatter radar
- ionosphere
- ionosphere thermosphere mesosphere
- madrigal
- magnetometer
- magnetosphere
- omni
- plotting
- python
- space
- space physics
- space weather
- superdarn
- supermag
- swarm
- thermosphere
- total electron content
- vires
- visualization

**Source:** Repository metadata and capabilities support the terms below; lowercase spelling preserves canonical keyword identity and avoids near-duplicates.

**Evidence:**
- `magnetosphere` — `setup.py` `keywords` list and PyHC `keywords`.
- `superdarn` — `datahub/sources/superdarn/potmap/`.
- `supermag` — `datahub/sources/supermag/{indices,magnetometer}/`.
- `ampere` — `datahub/sources/jhuapl/ampere/`.
- `field-aligned currents` — AMPERE fitted FAC, Swarm `fac_tms`, `fac_tms_dual`, `fac_lls_dual`, `aob_fac`, `ppi_fac`.
- `aurora` — DMSP/SSUSI `EDR_AUR`, Swarm auroral oval boundary, NIPR all-sky imager.
- `auroral electrojet` — WDC/AE, FMI IMAGE IE indices, Swarm `aej_*`.
- `thermosphere` — TU Delft neutral density/wind products.
- `total electron content` — Madrigal and ISEE GNSS TEC maps, Swarm `tec_tms`, `mit_tec`.
- `gnss` — GNSS TEC maps and Swarm GNSS/POD-derived products.
- `magnetometer` — ground and space-borne magnetometer data are read directly: `sources/supermag/magnetometer/` (SuperMAG ground stations, with the `SuperMAG_stations.dat` station table), `sources/ncei/dmsp/ssm_mfr/` (DMSP SSM magnetometer), and Swarm `l1b/mag_lr` and `l1b/mag_hr` (VFM/ASM). The WDC and FMI IMAGE index series ingested by `sources/wdc/*` and `sources/fmi/image/ie/` are likewise magnetometer-derived.
- `all-sky imager` — `datahub/sources/nipr/asc/tro_wmi/`.
- `coordinate transformation` — `geospacelab/cs/` and the geopack transform wrappers.
- `hapi`, `vires` — `datahub/sources/esa_eo/swarm/loader.py::load_from_HAPI` / `load_from_VirES`.

**Dropped from the 2025-10-09 file (with reason):** `spaceweather` — a near-duplicate of the live keyword `space weather`, which is already present. Adding it would create a redundant vocabulary row.

### 17. Data Sources (OPTIONAL)
**Values:**
- CDAWeb
- FTP/FTPS Directories
- GFZ
- HAPI
- HTTP/HTTPS Directories
- Madrigal
- Observatory/Mission-specific
- OMNIWeb
- Other
- SSCWeb
- VirES
- WDC

**Source:** Repository evidence below supports all 12 sources, including site-specific values such as `GFZ`, `Madrigal` and `WDC` alongside the generic ones.

**Evidence:**
- **FTP/FTPS Directories** — `datahub/sources/gfz/downloader.py:45` selects
  `ftp.gfz-potsdam.de`, and `:58-79` connects, logs in, changes directory and retrieves the requested
  file over FTP. The GFZ Kp/Ap and Hpo downloaders call this path directly from their constructors
  (`datahub/sources/gfz/kpap/downloader.py:42`;
  `datahub/sources/gfz/hpo/downloader.py:46`).
- **HAPI** — `datahub/sources/esa_eo/swarm/loader.py::load_from_HAPI(server="https://vires.services/hapi", dataset=..., parameters=...)` calls `hapiclient.hapi()` and maps the returned record array into GeospaceLAB `Variable` objects. Dispatched from `swarm/dataset.py` via the `from_HAPI` flag; implemented for the Swarm `l1b/mag_lr` product.
- **VirES** — `swarm/loader.py::load_from_VirES(collection, kwargs_products)` builds a `viresclient.SwarmRequest`, sets the collection and products, and ingests `request.get_between(...)`. Dispatched via the `from_VirES` flag; implemented for `l1b/mag_lr`.
- **SSCWeb** — `observatory/orbit/sc_orbit.py::OrbitPosition_SSCWS` uses `from sscws.sscws import SscWs` and `sscws.coordinates` to query NASA's Satellite Situation Center for orbit positions ("Searching the orbit data from NASA/SscWs ..."), including `list_satellites()`, `get_sat_info()`, `list_stations()`.

**Further evidence:** CDAWeb (`sources/cdaweb/{omni,dmsp/ssusi}`), GFZ (`sources/gfz/{kpap,hpo,snf107}`), Madrigal (`sources/madrigal/{isr,satellites,gnss}` via `madrigalWeb`), WDC (`sources/wdc/{dst,ae,asysym}`), OMNIWeb (CDAWeb/OMNI products), HTTP/HTTPS Directories (`requests` + `BeautifulSoup` directory scraping in most downloaders), Observatory/Mission-specific (ESA Swarm, JHUAPL/AMPERE, TU Delft, NCEI, NIPR, ISEE, FMI, SuperDARN, SuperMAG endpoints — cross-listed with Fields 31/32 as the form directs), Other (SuperMAG web API, EISCAT schedule portal).

### 18. Input File Formats (RECOMMENDED)
**Values:**
- ascii
- CDF
- HDF5
- ISTP-Compliant
- JSON
- netCDF3/4
- Other

**Source:** The readers actually present in the code: `h5py.File` (30 call sites — EISCAT/Madrigal HDF5, DMSP s1/s4/e, GNSS TEC), `netCDF4.Dataset` / `nc.Dataset` (33 call sites — SSUSI, AMPERE, Swarm, SuperDARN, and all locally-cached products), `cdflib.CDF` (CDAWeb OMNI and Swarm CDF, ISTP-compliant), `np.loadtxt` and IAGA2002/ASCII parsers (WDC, GFZ, TU Delft, SuperDARN POTMAP), and `plt.imread` for all-sky camera JPG frames (covered by *Other*, along with the `EISCAT-hdf5` / `Madrigal-hdf5` dialects).

**Evidence for `JSON`:** the SuperMAG web API is consumed as JSON. `sources/supermag/supermag_api.py::sm_GetUrl(fetchurl, fetch='json')` parses the response with `json.loads(longstring)` (line 244), and both SuperMAG entry points request that path unconditionally — `SuperMAGGetIndices()` at line 310 and `SuperMAGGetData()` at line 338 each call `sm_GetUrl(urlstr, 'json')`. Both are reached from **production** downloader code, not from a demo: `sources/supermag/indices/downloader.py:135` and `sources/supermag/magnetometer/downloader.py:100`. `JSON` is an exact member of the `FileFormat` vocabulary.

**Omitted because no reader exists — `IDL.sav`:** there is no IDL save-file reader anywhere in the package — no `readsav`, no `scipy.io` import, no `.sav` handling. There is no GITM module (`find . -iname "*gitm*"` returns nothing), and `git log --all --diff-filter=A '*gitm*'` shows GITM has never been present in tracked history. The README's built-in-data-sources table (rows 77–78) advertises `UTA/GITM/2DALL` and `UTA/GITM/3DALL` with formats *binary* and *IDL-sav*, but both rows are marked **`beta`** with **`Downloadable: False`** — documentation for a module that was never shipped.

**Omitted because no reader exists — `csv`, `FITS`, `Zarr`:** the only `pd.read_csv` occurrence (`supermag_api.py:461`) sits inside `supermag_testing(userid)`, a vendored demonstration helper defined at line 404 and never called from anywhere in the package; it is dead code. No FITS or Zarr readers exist.

### 19. Output File Formats (RECOMMENDED)
**Values:**
- ascii
- netCDF3/4

**Source:** Direct repository code evidence supersedes the earlier "Not explicitly documented" conclusion.

**Evidence:**
- **netCDF3/4** — the software converts and persists downloaded data as netCDF in at least eight modules, each opening a writable handle (`nc.Dataset(fp, 'w')`) and populating dimensions/variables: `wdc/dst/downloader.py::save_to_netcdf`, `wdc/ae`, `wdc/asysym`, `gfz/downloader.py::save_to_netcdf` with `gfz/kpap`, `gfz/kpap/nowcast`, `gfz/hpo`, `gfz/hpo/nowcast`, `superdarn/potmap/downloader.py::save_to_netcdf` and `potmap/loader.py::save_to_nc`, `supermag/indices/downloader.py::save_to_nc`, `supermag/magnetometer/downloader.py::save_to_nc`, and `observatory/orbit/sc_orbit.py::save_to_netcdf` (writing SSCWeb orbit data).
- **ascii** — `fmi/image/ie/downloader.py` writes the retrieved IMAGE electrojet index data to a `.dat` ASCII file as its only persisted form; the WDC downloaders likewise write the raw IAGA2002 ASCII to `.dat` alongside the netCDF; and `madrigal/isr/eiscat/downloader.py::to_txt()` writes a formatted EISCAT experiment catalogue to a text file.

**Considered and excluded:** `CDF` — `datahub/__init__.py::save_to_cdf()` exists but its body is `pass` (an unimplemented stub), as is `save_to_pickle()`. Claiming CDF output would be wrong. Figure output (PNG/PDF via `save_figure()`) is image rendering, not a data file format, and has no corresponding value in the `FileFormat` list.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Operating System Independent

**Source:** README §1 states the package was tested "under **Ubuntu 20.04** and **MacOS Big Sur**"; `.github/workflows/pyhc-actions.yml` runs on `ubuntu-latest`; `.readthedocs.yaml` builds on `ubuntu-22.04`. The package is pure Python with no compiled extensions of its own.
**Note:** No Windows evidence exists (no Windows CI job, no Windows mention in the install docs), so `Windows` is not added.

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Source:** Pure-Python package (437 `.py` files, no `.pyx`, `.c`, or `.f` sources); architecture dependence would come only from third-party wheels.

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Geomagnetic Storms
- Solar Wind

**Source:** Repository evidence, resolved against the HSSI `Phenomena` controlled vocabulary. Both values are exact matches; the vocabulary's remaining terms are solar-specific and do not apply to this software.

**Evidence:**
- **Geomagnetic Storms** — the storm-index products are a core built-in capability: `sources/wdc/dst` (Dst), `sources/wdc/asysym` (ASY/SYM), `sources/wdc/ae` (AE), `sources/gfz/kpap` (Kp/Ap) and `sources/gfz/hpo` (Hp30/Hp60), plus SuperMAG indices (`sources/supermag/indices`) and FMI IMAGE electrojet indices. `test/test_indices.py` exercises them.
- **Solar Wind** — `sources/cdaweb/omni` provides OMNI solar wind plasma and IMF (`B_x_GSM` etc.), surfaced through the `OMNIDashboard` express quicklook (README Example 3) and `test/test_omni.py`.

**Other applicable phenomena have no vocabulary row.** Auroral emissions, field-aligned currents, geomagnetic indices, ionospheric convection, ionospheric density, ionospheric electric fields and neutral atmosphere all describe this software accurately but have no corresponding `Phenomena` term. Rather than mint free-text rows, they are captured as Field 16 keywords (`field-aligned currents`, `aurora`, `auroral electrojet`, `total electron content`, `thermosphere`) and Field 5 regions (`Earth Ionosphere`, `Earth Thermosphere`, `Earth Auroral Subregion`).

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** Repository, registry and PyHC evidence supports `Active` under the repostatus.org definition.

**Evidence:**
- **Release cadence** — six releases in the eight months preceding this extraction: v0.12.0 (2026-01-30), v0.13.0 (2026-02-20), v0.14.0 (2026-05-18), v0.14.13 (2026-05-28), v0.14.14 and v0.14.15 (2026-05-29); 77 releases on PyPI in total. The most recent commit on `master` is `213bbc2`, dated 2026-06-30.
- **`setup.py` classifier** — `Development Status :: 4 - Beta`, i.e. a usable released state (not `3 - Alpha`, which would suggest WIP). Actively updated: the classifier list now covers Python 3.12/3.13/3.14 and `python_requires='>=3.12'`.
- **PyHC** — GeospaceLAB is listed in the PyHC *community* package registry with `software_maturity: Good`, and `community`, `documentation`, `testing`, `python3` and `license` all rated `Good`. The repository runs the `heliophysicsPy/pyhc-actions` PHEP 3 compliance and PyHC environment-compatibility workflows on every push and quarterly.

Per repostatus.org, "Active" = *reached a stable, usable state and is being actively developed*, which the above satisfies. (The README's legacy line "The current version is a pre-released version" is contradicted by 77 PyPI releases and the Beta classifier, and is not treated as authoritative.)

### 24. Documentation (RECOMMENDED)
**Value:** https://geospacelab.readthedocs.io/en/latest/

**Source:** Confirmed by README, `.readthedocs.yaml`, `docs/`, and PyHC `docs`.
**Note:** Field 24 accepts a single URL. Two further documentation resources exist and are recorded here rather than replacing the main link: the Swarm-specific documentation at https://geospacelab-swarm.readthedocs.io/en/latest/ and the GitHub wiki at https://github.com/JouleCai/geospacelab/wiki.

### 25. Funder (OPTIONAL)
**Values:**

1. **Organization:** University of Oulu
   **Funder Identifier:** https://ror.org/03yj89h83
2. **Organization:** Swedish National Space Agency
   **Funder Identifier:** https://ror.org/04t512h04
3. **Organization:** Research Council of Finland
   **Funder Identifier:** https://ror.org/05k73zm37
4. **Organization:** U.S. National Science Foundation
   **Funder Identifier:** https://ror.org/021nxhr62
5. **Organization:** National Aeronautics and Space Administration
   **Funder Identifier:** https://ror.org/027ka1x80
6. **Organization:** United States Air Force Office of Scientific Research
   **Funder Identifier:** https://ror.org/011e9bt93
7. **Organization:** Office of Naval Research
   **Funder Identifier:** https://ror.org/00rk2pe57

**Source:** The Funding statement of the reference publication (Cai et al. 2022, Field 14), which is the authoritative funding declaration for the work that produced GeospaceLAB. Funders 1–6 come from **Crossref structured funder metadata** for `10.3389/fspas.2022.1023163`, each carrying a Funder Registry DOI (`10.13039/501100018871` Kvantum-Instituutti Oulun Yliopisto, `10.13039/501100001859` Swedish National Space Agency, `10.13039/501100002341` Academy of Finland, `10.13039/100000001` National Science Foundation, `10.13039/100000104` NASA, `10.13039/100000181` AFOSR). Funder 7 (Office of Naval Research) appears in the article's Funding section text but not in Crossref's structured list.

Every organization name is the ROR display name — full institutional names, acronyms expanded, per the Field 25 guidance. All seven ROR identifiers were resolved via the ROR v2 API.
**Notes:** (a) Funder 1's Crossref entry is the Finnish-language "Kvantum-Instituutti, Oulun Yliopisto"; the Kvantum Institute has no ROR of its own, so its parent University of Oulu is recorded, with the institute named in Field 26. (b) "Academy of Finland" is the historical name of the body now called the Research Council of Finland; both share ROR `https://ror.org/05k73zm37`, and the current display name is used.
**Also checked and found empty:** DataCite `fundingReferences` for both the concept DOI and the v0.14.15 DOI, the Zenodo record's `grants` field, the repository `datacite.json` (`fundingReferences: []`), README, and `docs/citation.rst` — none of these carries funding metadata, which is why the field was previously empty.

### 26. Award Title (OPTIONAL)
**Values:**

One award number is recorded per entry because an award title may have only one award number. The three NASA numbers and the two NSF numbers are therefore separate Award entries rather than comma-joined strings.

1. **Award Title:** Kvantum Institute funding for the development of GeospaceLAB, University of Oulu
   **Award Number:** Not found
   *Funder:* University of Oulu (https://ror.org/03yj89h83)
2. **Award Title:** Swedish National Space Agency postdoctoral grant
   **Award Number:** DNR-155A/17
   *Funder:* Swedish National Space Agency (https://ror.org/04t512h04)
3. **Award Title:** Academy of Finland project
   **Award Number:** 314664
   *Funder:* Research Council of Finland (https://ror.org/05k73zm37)
4. **Award Title:** Air Force Office of Scientific Research award
   **Award Number:** FA9559-16-1-0364
   *Funder:* United States Air Force Office of Scientific Research (https://ror.org/011e9bt93)
5. **Award Title:** National Aeronautics and Space Administration grant
   **Award Number:** 80NSSC20K0195
   *Funder:* National Aeronautics and Space Administration (https://ror.org/027ka1x80)
6. **Award Title:** National Aeronautics and Space Administration grant
   **Award Number:** 80NSSC20K1786
   *Funder:* National Aeronautics and Space Administration (https://ror.org/027ka1x80)
7. **Award Title:** National Aeronautics and Space Administration grant
   **Award Number:** 80NSSC22K0061
   *Funder:* National Aeronautics and Space Administration (https://ror.org/027ka1x80)
8. **Award Title:** Office of Naval Research Multidisciplinary University Research Initiative grant
   **Award Number:** ONR15-FOA-0011
   *Funder:* Office of Naval Research (https://ror.org/00rk2pe57)
9. **Award Title:** U.S. National Science Foundation grant
   **Award Number:** AGS-2033787
   *Funder:* U.S. National Science Foundation (https://ror.org/021nxhr62)
10. **Award Title:** U.S. National Science Foundation grant
   **Award Number:** AGS-1952737
   *Funder:* U.S. National Science Foundation (https://ror.org/021nxhr62)

**Source:** The Funding section of the reference publication (Cai et al. 2022). Award *numbers* are quoted verbatim from that section; Crossref's structured funder records for this DOI carry no `award` values, so the article text is the only source for them. Each entry retains its funder linkage to the corresponding Field 25 organization, shown above in italics.
**Scope of the funding statement:** the publication states these grants in the aggregate for the paper's authors — the Kvantum Institute funding is the one explicitly tied to GeospaceLAB development, while the remaining awards supported contributing co-authors. Award *titles* are descriptive reconstructions (the article gives agency and number, not formal grant titles); only the numbers are verbatim.

### 27. Related Publications (OPTIONAL)
**Values:**
- https://doi.org/10.1029/2020JA028808

**Source:** README "Example 4" and the 2025-10-09 file; DOI verified against Crossref.
**Full citation:** Cai, L., Aikio, A. T., Kullen, A., Deng, Y., Zhang, Y., Zhang, S.-R., Virtanen, I., & Vanhamäki, H. (2021). DMSP Observations of High-Latitude Dayside Aurora (HiLDA). *Journal of Geophysical Research: Space Physics*.
**Why it belongs here:** README Example 4 is presented as a reproduction of a figure from this paper ("This is an example showing the HiLDA aurora in the dayside polar cap region (see also DMSP observations of the HiLDA aurora (Cai et al., JGR, 2021))"), i.e. a publication whose science the package demonstrably supports. It is distinct from the Field 14 reference publication.
**Also searched, nothing further found:** `docs/citation.rst`, `docs/index.rst`, `docs/user/`, `docs/dev/`, the `examples/` tree, DataCite `relatedIdentifiers` for both DOIs (only `IsVersionOf` and `IsSupplementTo` to the GitHub tag), and the Zenodo record's `related_identifiers`.

### 28. Related Datasets (OPTIONAL)
**Values:**
- https://doi.org/10.1029/2004JA010649 — OMNI (CDAWeb/OMNI solar wind and IMF)
- https://doi.org/10.1016/0021-9169(95)00047-X — EISCAT incoherent scatter analysed data (GUISDAP)
- https://doi.org/10.1186/BF03351933 — ESA Swarm mission data products
- https://doi.org/10.1029/2000GL012725 — AMPERE / Iridium-derived field-aligned currents
- https://doi.org/10.1007/s10712-007-9017-8 — SuperDARN convection data
- https://doi.org/10.1029/2012JA017683 — SuperMAG indices and magnetometer data
- https://doi.org/10.1029/2008JA013682 — IMAGE magnetometer network electrojet indices

**Source:** Field 28 directs that "at minimum, the DOI should be the publication that described the dataset". Each DOI above is the canonical dataset-describing publication for a data product that GeospaceLAB has a built-in reader for, and **every DOI was individually verified against the Crossref API** (title, first author and year all confirmed):
- `10.1029/2004JA010649` — King & Papitashvili (2005), *Solar wind spatial scales in and comparisons of hourly Wind and ACE plasma and magnetic field data*, JGR Space Physics → the OMNI dataset (`sources/cdaweb/omni`).
- `10.1016/0021-9169(95)00047-X` — Lehtinen & Huuskonen (1996), *General incoherent scatter analysis and GUISDAP*, JATP → the GUISDAP-analysed EISCAT product the package loads (`sources/madrigal/isr/eiscat`; README Example 2 states the quicklook "shows the GUISDAP analysed results").
- `10.1186/BF03351933` — Friis-Christensen, Lühr & Hulot (2006), *Swarm: A constellation to study the Earth's magnetic field*, Earth, Planets and Space → the ESA Swarm products (`sources/esa_eo/swarm`, 30+ products).
- `10.1029/2000GL012725` — Waters, Anderson & Liou (2001), *Estimation of global field aligned currents using the Iridium System magnetometer data*, GRL → the AMPERE fitted FAC product (`sources/jhuapl/ampere`).
- `10.1007/s10712-007-9017-8` — Chisham et al. (2007), *A decade of the Super Dual Auroral Radar Network (SuperDARN)*, Surveys in Geophysics → the SuperDARN potential maps (`sources/superdarn/potmap`).
- `10.1029/2012JA017683` — Gjerloev (2012), *The SuperMAG data processing technique*, JGR Space Physics → SuperMAG indices and magnetometer data (`sources/supermag`).
- `10.1029/2008JA013682` — Tanskanen (2009), *A comprehensive high-throughput analysis of substorms observed by IMAGE magnetometer network*, JGR Space Physics → the FMI IMAGE electrojet indices (`sources/fmi/image/ie`).

**Considered but not included:** a dataset-describing DOI for DMSP/SSUSI could not be verified with confidence and is therefore omitted rather than guessed; likewise for the TU Delft thermosphere density/wind products, the Madrigal GNSS TEC maps, and the GFZ and WDC index series. The 2025-10-09 file listed ten dataset *names* with no identifiers at all; those names are superseded by the seven verified DOIs above, while the unsupported remainder stays omitted.

### 29. Related Software (OPTIONAL)
**Values:**
- https://doi.org/10.5281/zenodo.3598705 — aacgmv2 (Altitude-Adjusted Corrected Geomagnetic coordinates)
- https://doi.org/10.5281/zenodo.1214206 — apexpy (Apex / Quasi-Dipole geomagnetic coordinates)
- https://doi.org/10.5281/zenodo.1481144 — cdflib (CDF file reading)
- https://doi.org/10.5281/zenodo.15110786 — geopack (Tsyganenko models in Python)
- https://github.com/MITHaystack/madrigalWeb — madrigalWeb (Madrigal database client)
- https://berniegsfc.github.io/sscws/REST/ — sscws (NASA Satellite Situation Center web-services client)

**Source:** DataCite confirms the identities of the first four DOIs (`aburrell/aacgmv2: Version 2.6.0`, `apexpy`, `MAVENSDC/cdflib`, `tsssss/geopack: v1.0.12`). Placeholder display names do not override the DOI identities. All four pass the Field 29 gate as *domain-specific* dependencies that characterise the software.

**Why madrigalWeb and sscws pass the gate:**
- **madrigalWeb** — a heliophysics-specific client for the Madrigal distributed database. It is imported directly (`import madrigalWeb.madrigalWeb as madrigalweb`) and is the access layer for a large fraction of GeospaceLAB's built-in sources (EISCAT, Millstone Hill, PFISR, RISR-N, DMSP s1/s4/e, GNSS TEC). It fails the "equally at home in a web app, a finance model, or a biology pipeline" test outright. No software DOI was found, so the repository URL is used.
- **sscws** — NASA's Satellite Situation Center web-services client, also domain-specific. Imported as `from sscws.sscws import SscWs` and `from sscws.coordinates import ...` in `observatory/orbit/sc_orbit.py`, where it supplies spacecraft orbit positions. PyPI lists no repository, so its documentation home is given, as Field 29 permits ("link where users can find more information").

**Not listed, and why:**
- **cartopy** — proposed by the 2025-10-09 file. Tier A generic infrastructure (map projection/plotting); would be equally at home outside heliophysics. Excluded from both Fields 29 and 30.
- **numpy, scipy, pandas, matplotlib, requests, beautifulsoup4, tqdm, natsort, toml, keyring, palettable, cython, h5py, netCDF4** — all `install_requires` entries, all generic scientific-Python or I/O plumbing. Being a dependency is not relatedness. Excluded.
- A rejected Field 30 candidate was **not** relocated here; the same exclusion applies to both fields.

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://doi.org/10.5281/zenodo.2554162 — viresclient (ESA VirES for Swarm Python client)
- https://github.com/hapi-server/client-python — hapiclient (HAPI server Python client)

**Source:** Repository code analysis. Both entries clear the strict Field 30 bar of a **demonstrated exchange** with a named heliophysics peer tool — not a dependency listing. Neither package is in `install_requires`; both are imported lazily inside the loader methods that use them, which is itself evidence that they are optional interoperation paths rather than infrastructure.

**Evidence — specific exchange, not ecosystem membership:**
- **viresclient** — `geospacelab/datahub/sources/esa_eo/swarm/loader.py::load_from_VirES(collection, kwargs_products)` executes `from viresclient import SwarmRequest`, constructs a `SwarmRequest`, calls `set_collection()` / `set_products()` / `get_between(start_time, end_time)`, and hands the returned object back to the GeospaceLAB loader. `swarm/dataset.py` exposes this as the `from_VirES` / `kwargs_VirES` constructor flags and dispatches through `_load_from_VirES()`; `swarm/l1b/mag_lr/loader.py` implements the concrete mapping. Zenodo concept DOI `10.5281/zenodo.2554162` (ESA-VirES/VirES-Python-Client) is used in preference to the repository URL, per the field's "ideally, enter the DOI" instruction.
- **hapiclient** — `swarm/loader.py::load_from_HAPI(server="https://vires.services/hapi", dataset, parameters)` executes `from hapiclient import hapi`, calls `hapi(server, dataset, parameters, start_iso, stop_iso)`, and then `swarm/l1b/mag_lr/loader.py` walks `data.dtype.names` and maps each HAPI parameter name onto a GeospaceLAB `Variable` through `self.variable_name_dict` — an explicit data-model conversion between the two packages. Dispatched via the `from_HAPI` flag and `_load_from_HAPI()`. No software DOI was found, so the repository URL is used.

**Not listed, and why:**
- **Tier A, always excluded** — numpy, scipy, pandas, matplotlib, cartopy, requests, beautifulsoup4, tqdm, natsort, toml, keyring, palettable, cython. Being a dependency is not interoperability.
- **Tier B, excluded for lack of cited evidence** — `cdflib`, `h5py`, `netCDF4` are used purely as internal file readers; no public GeospaceLAB API accepts or returns their objects as a documented interchange format, so the Tier B bar is not met. (`cdflib` remains in Field 29 as a domain-specific dependency, which is the correct destination.)
- **aacgmv2, apexpy, geopack, madrigalWeb, sscws** — genuinely domain-specific, but the relationship is *dependency*, not peer-tool exchange: GeospaceLAB calls into them, and in geopack's case vendors the model routines. They are recorded in Field 29 instead.
- **Blanket claims rejected** — "part of the scientific Python ecosystem" and "a PyHC package, so it interoperates with PyHC packages" were not accepted as justification for any entry.
- **GeospaceLAB-Swarm** — investigated as a possible companion package; it is a separate *documentation site* (https://geospacelab-swarm.readthedocs.io) for code that lives inside this same repository under `datahub/sources/esa_eo/swarm/`, not a separate distributable. Recorded in Field 24, not here.

---

## Section 3: Additional Metadata

### 31. Related Instruments (OPTIONAL)
**Values:**

| Name (verbatim from controlled list) | SPASE Identifier |
|---|---|
| Incoherent Scatter Radar | https://spase-metadata.org/SMWG/Instrument/MEASURE/Millstone.Hill/ISR |
| SuperMAG Magnetometers | https://spase-metadata.org/SMWG/Instrument/SuperMAG/Magnetometers |
| Tromso UHF | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/EISCAT/UHF |
| Tromso VHF | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/EISCAT/VHF |
| Electric Field Instrument : Langmuir Probe | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-A/LP |
| Electric Field Instrument : Thermal Ion Imager | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-A/TII |
| Absolute Scalar Magnetometer / Vector Field Magnetometer | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-A/MAG |
| Global Navigation Satellite System | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-A/GNSS |
| Electric Field Instrument : Langmuir Probe | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-B/LP |
| Electric Field Instrument : Thermal Ion Imager | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-B/TII |
| Absolute Scalar Magnetometer / Vector Field Magnetometer | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-B/MAG |
| Global Navigation Satellite System | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-B/GNSS |
| Electric Field Instrument : Langmuir Probe | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-C/LP |
| Electric Field Instrument : Thermal Ion Imager | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-C/TII |
| Absolute Scalar Magnetometer / Vector Field Magnetometer | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-C/MAG |
| Global Navigation Satellite System | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-C/GNSS |

**Resolution:** Each name is copied verbatim from its matched SPASE-backed record. For the twelve Swarm-satellite rows the name+type pair is not unique — the four instrument names each appear on three rows, one per satellite, and disambiguation is by the SPASE identifier's satellite-specific path segment (see the Swarm instrument evidence below); the remaining four rows are unique name-and-type matches.

**Notes on the retained rows:**
- **Millstone Hill ISR** — `sources/madrigal/isr/millstonehill` plus the `MillstoneHillISRDashboard` express quicklook.

**Further evidence:**
- **SuperMAG Magnetometers** — `sources/supermag/magnetometer/` (loader, downloader, `variable_config`, `SuperMAG_stations.dat` station table) and `sources/supermag/indices/` read SuperMAG ground magnetometer data and derived indices through the SuperMAG web API. Unique instrument-type row and unique name.

**Omitted, and why:**
- **Tromsø all-sky imager (NIPR WMI)** — supported (`sources/nipr/asc/tro_wmi`), but the module reads the 558 nm monochromatic channel, whereas the two candidate SPASE records at Tromsø (`IUGONET/Instrument/NIPR/EISCAT/TRO/AWI_whitelight` and `.../TRO/NWI_whitelight`) both describe **white-light** imagers. Neither matches the instrument this module reads.
- **GNSS TEC receivers** — `sources/madrigal/gnss/tecmap` and `sources/isee/gnss/tecmap` read *global gridded TEC map products*, not any individual receiver. Every candidate SPASE record is a site-specific receiver (chiefly Japanese networks) or the Swarm on-board GNSS; none represents a global TEC map product. The capability is captured in Field 16 (`total electron content`, `gnss`) and Field 5 (`Earth Ionosphere`).
- **Iridium constellation** — the AMPERE product is derived from Iridium magnetometer data, but GeospaceLAB reads the fitted AMPERE product only, never raw Iridium data; the AMPERE record already covers this.
- **EISCAT Svalbard Radar, EISCAT Kiruna/Sodankylä, Poker Flat ISR, Resolute Bay ISR North, and DMSP sensors** — see the omission notes below.

**Instruments omitted, and why:**

- **EISCAT Svalbard Radar (ESR).** The software does not distinguish the two Svalbard antennas: `madrigal/isr/eiscat/downloader.py` `instrument_codes` maps both `'42m'` and `'32m'` to the same code `[95]`, `downloader.py:135` collapses `32m`, `42m` and `esr` into the single label `'ESR'`, and `EISCATSite` maps `['ESR', 'LYB']` to one site, "Longyearbyen". SPASE splits the facility into two records — `.../EISCAT/32M` ("ESR 32M", steerable, 32 m) and `.../EISCAT/42M` ("ESR 42M", field-aligned, 42 m) — which both carry the vocabulary name "Longyearbyen". Listing either would assert an antenna distinction the software never makes.
- **EISCAT Kiruna and Sodankylä.** `instrument_codes` lists them (`[73, 76]` and `[71, 75]`) for the download layer, but `EISCATSite.__init__` raises `NotImplementedError` for any site other than `UHF`/`TRO`, `VHF` and `ESR`/`LYB`, so no dataset can be constructed for them.
- **Poker Flat ISR and Resolute Bay ISR North.** Both are genuinely supported (`madrigal/isr/pfisr` with `test/test_pfisr.py`, and `madrigal/isr/risr_n`), but no SPASE record of any type represents either incoherent scatter radar. The records that share those sites describe other facilities: `SMWG/Observatory/Ground/Poker.Flat` ("Poker Flat Geophysical Observatory") is grouped under `ObservatoryGroupID: Ground/GMAG` and `Ground/GIMA` — ground-magnetometer and Geophysical Institute Magnetometer Array networks — and `SMWG/Observatory/Ground/Resolute.Bay` ("The Resolute Bay geophysical observatory") under `Ground/WDC`, `Ground/GMAG`, `Ground/CANMOS` and `Ground/INTERMAGNET`, all magnetometer networks. Binding an incoherent scatter radar to a magnetometer station would be a factual mis-link.
  This is why the AMPERE precedent does not extend here. `SMWG/Observatory/AMPERE` is itself the description of the measurement system GeospaceLAB reads — its Description explains that Iridium satellites carry engineering magnetometers and that techniques developed at JHU/APL process Iridium magnetic field data into the fitted product — and no separate AMPERE instrument record exists. There the observatory record and the supported data product are the same thing; at Poker Flat and Resolute Bay they are not.
- **DMSP sensors (SSUSI, SSJ, SSIES, SSM).** SPASE has no block-generic 5D-3 sensor records: every SSUSI / SSJ5 / SSI-ES-3 / SSM-Boom record is per-spacecraft across F15–F19 and S20, and the 5D-2 block carries a different sensor generation (SSJ4, SSIES). GeospaceLAB's DMSP support is constellation-generic — `sat_id` is consumed purely as string interpolation (`.lower()`, `.upper()`) into request paths, with no whitelist or assertion anywhere in any DMSP module. The only satellite literals in the repository are in examples and tests (`f16` ×4, `f17` ×4, `f18` ×3), which is demonstration data rather than a support claim. The mission-level observatory row `Defense Meteorological Satellite Program` (Field 32) is the correct granularity.

**Evidence for the Swarm instrument rows.**

*Which instruments*, from the repository's own per-product metadata: each product module declares an `'instrument'` key. **EFI → Langmuir Probe** (`l1b/efi_lp`, `l1b/efi_lpi`, `advanced/efi_lp_fp`, `advanced/efi_lp_hm`, `l2daily/efi_tie`, `nix_tms`, `tix_tms` — 7 products); **EFI-TII and EFI-IDM → Thermal Ion Imager** (`advanced/efi_tct02`, `efi_tct16`, `efi_idm` — 3); **MAG** (`l1b/mag_lr`, `l1b/mag_hr` and 15 L2 products including `fac_tms`, `aob_fac`, `aej_*`, `ibi_tms`, `mit_*` — 17); **GPS and POD → GNSS** (`l2daily/tec_tms`, `whi_evt`, `dns_pod` — 3).

*Which satellites.* Swarm A and C are directly exercised by the ESA product tests (`sat_id='A'` ×39, `sat_id='C'` ×21). Swarm B is supported by the same code path, established end to end:

1. **The code builds satellite-specific collection identifiers by interpolation.** `l1b/mag_lr/loader.py:114` sets the default `collection = "SW_OPER_MAG__LR_1B"` and line 116 does `collection = collection.replace("MAG_", "MAG" + self.sat_id)`; the HAPI path at line 172 uses the same default. `dataset.py:76` accepts `sat_id` with no whitelist (`kwargs.pop('sat_id', 'A')`) and `dataset.py:335` builds `Sat_{sat_id}` directory segments. With `sat_id='B'` the transform yields `SW_OPER_MAGB_LR_1B` (and `SW_FAST_MAGB_LR_1B` in FAST mode).
2. **The queried service serves those collections.** The VirES HAPI catalog at `https://vires.services/hapi/catalog` — the endpoint behind `load_from_VirES` and `load_from_HAPI` — publishes Swarm-B collections for all four instruments: **LP** `SW_OPER_EFIB_LP_1B`, `SW_FAST_EFIB_LP_1B`; **TII** `SW_EXPT_EFIB_TCT02`, `SW_EXPT_EFIB_TCT16`; **MAG** `SW_OPER_MAGB_LR_1B`, `SW_OPER_MAGB_HR_1B`, `SW_FAST_MAGB_LR_1B`, `SW_FAST_MAGB_HR_1B`; **GNSS** `SW_OPER_TECBTMS_2F`, `SW_FAST_TECBTMS_2F`, `SW_OPER_IPDBIRR_2F`. Satellite-specific collections are symmetric across the constellation at 48 per satellite (counting collection identifiers that have an A/B/C satellite-letter position at which all three variants exist in the catalog). That symmetry is the point: the service draws no distinction between the three satellites. (Catalog read 2026-07-29.)

*Scope note:* `fac_tms_dual` and `fac_lls_dual` hard-code `sat_id='AC'` (`fac_tms_dual/downloader.py:36`, "The product is only for AC"); those two products are specific to the Swarm A–C pair.

*Vocabulary gap:* the Swarm accelerometer (`l2daily/dns_acc`, declared `'instrument': 'ACC'`) has no SPASE instrument record, so accelerometer-derived support is representable only at observatory level (Field 32).

*Note for HSSI maintainers:* rendered HSSI output lists related instruments by name only. Because the Swarm instrument records share a name across the three satellites, the four instrument names will each appear three times with no indication of the satellite. The stored identifiers are distinct and unambiguous; this is a display characteristic only.

### 32. Related Observatories (OPTIONAL)
**Values:**

| Name (verbatim from controlled list) | SPASE Identifier |
|---|---|
| Active Magnetosphere and Planetary Electrodynamics Response Experiment | https://spase-metadata.org/SMWG/Observatory/AMPERE |
| CHAMP | https://spase-metadata.org/SMWG/Observatory/CHAMP |
| Defense Meteorological Satellite Program | https://spase-metadata.org/SMWG/Observatory/DMSP |
| European Incoherent Scatter Scientific Association | https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/EISCAT |
| Gravity Field and Steady-State Ocean Circulation Explorer | https://spase-metadata.org/SMWG/Observatory/GOCE |
| Gravity Recovery and Climate Experiment | https://spase-metadata.org/SMWG/Observatory/GRACE |
| International Monitor for Auroral Geomagnetic Effects | https://spase-metadata.org/SMWG/Observatory/Ground/IMAGE |
| SuperDARN | https://spase-metadata.org/SMWG/Observatory/SuperDARN |
| SuperMAG | https://spase-metadata.org/SMWG/Observatory/SuperMAG |
| Swarm : ESA mission | https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM |
| Swarm Alpha | https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM-A |
| Swarm Bravo | https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM-B |
| Swarm Charlie | https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM-C |

**Resolution:** As for Field 31, names are copied verbatim and records are matched by SPASE identifier rather than by name.

**Per-value evidence:**
- **Swarm Alpha / Bravo / Charlie** — `datahub/sources/tud/downloader.py` enumerates and asserts the complete constellation for the TU Delft accelerometer and precise-orbit-determination products: `_validate_sat_id()` line 155 sets `valid_sat_ids = ['A', 'B', 'C']` followed by `assert self.sat_id in valid_sat_ids`, and `_validate_product()` line 141 gates on `self.mission == 'Swarm' and self.sat_id in ['A', 'B', 'C']`. Per-satellite data is downloaded for each. The Swarm test suite makes 60 per-satellite instantiations (`sat_id='A'` ×39, `sat_id='C'` ×21), and the dual-satellite products `fac_tms_dual` / `fac_lls_dual` hard-code `sat_id='AC'`. These three records also carry the only per-satellite distinction visible in rendered HSSI output, since the Field 31 instrument records share names across satellites; and the Swarm accelerometer (`l2daily/dns_acc`, declared `'instrument': 'ACC'`) has no SPASE instrument record, so that support is representable only here.
- **SuperMAG** — `sources/supermag/{indices,magnetometer}` with `supermag_api.py`, `utilities.py` and the `SuperMAG_stations.dat` station list. Unique row.
- **International Monitor for Auroral Geomagnetic Effects** — `sources/fmi/image/ie/` (downloader, loader, `variable_config`) retrieves the IMAGE magnetometer network's electrojet (IE/IL/IU) indices from FMI. Unique row. Note the vocabulary also contains a same-acronym but entirely different mission, "Imager for Magnetopause-to-Aurora Global Exploration" (`SMWG/Observatory/IMAGE`); the two full names are wholly distinct, so recording the full name plus identifier removes any ambiguity. The NASA IMAGE mission is **not** supported by this software and is not listed.

**Notes on the retained rows:**
- **AMPERE** is recorded here, not in Field 31. AMPERE is an observatory-class entity — a network experiment, not an instrument — and its SPASE identity is an Observatory path, `https://spase-metadata.org/SMWG/Observatory/AMPERE`; the association therefore belongs in Related Observatories. It was previously carried in Field 31 against a row that had been mis-typed as an instrument, which put the association in the wrong field. GeospaceLAB reads the JHUAPL AMPERE fitted field-aligned-current product (`sources/jhuapl/ampere/{fitted,grd}`).
- **Swarm** — the record's stored display name is `Swarm : ESA mission`, which is how the upstream SPASE registry names it. The odd punctuation is upstream-faithful and deliberately kept; the identifier `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM` is the durable half of the value.
- **CHAMP** is the only retained value whose `name` is not unique in the vocabulary (two rows: `SMWG/Observatory/CHAMP` and `IUGONET/Observatory/RISH/CHAMP/CHAMP`). Because live HSSI already binds it to a specific identifier and that identifier is carried through unchanged, no collision arises. Evidence: `sources/tud/champ/{dns_acc,wnd_acc}`.
- **GRACE** — `sources/tud/grace/{dns_acc,wnd_acc}`. **GOCE** — `sources/tud/goce/{dns_acc,wnd_acc,dns_wnd_acc_v01}`. **SuperDARN** — `sources/superdarn/potmap`. **DMSP** — mission-level record covering the SSUSI, SSJ, SSIES and SSM products (see Field 31). **EISCAT** — umbrella record covering the Tromsø and Svalbard radars (see Field 31).

**Omitted, and why:**
- **GRACE Follow-On (GRACE-FO)** — supported (`sources/tud/grace_fo/{dns_acc,wnd_acc}`), but no SPASE record of any type exists for the mission, in either the instrument or the observatory vocabulary. Omitted rather than free-typed. This is the one supported mission with no vocabulary representation at all.
- **Poker Flat and Resolute Bay** — the available records describe co-located magnetometer facilities, not the incoherent scatter radars (see Field 31).
- **NIPR Tromsø optical site** — the imaging instrument itself has no matching record (see Field 31), and the site-level records are the EISCAT Tromsø observatory records already covered by the umbrella EISCAT entry.
- **CDAWeb, Madrigal, OMNIWeb, WDC, GFZ, NCEI, TU Delft** — multi-mission archives and index services, not observatories. Correctly recorded in Field 17 (Data Sources), per the field guidance.

### 33. Logo (OPTIONAL)
**Value:** https://github.com/JouleCai/geospacelab/blob/master/docs/images/logo_v1_landscape_accent_colors.png

**Source:** Identical to the PyHC registry `logo` value and to the image referenced at the top of README.md.

---

## Upstream follow-ups

These concern systems outside this record and are noted for whoever maintains them.

1. **SPASE vocabulary gaps.** Three facilities this software genuinely supports cannot be represented: the EISCAT Svalbard Radar 32 m / 42 m antenna pair (representable only by asserting a distinction the software does not make); Poker Flat ISR and Resolute Bay ISR North (no radar record exists, only co-located magnetometer observatories); and GRACE Follow-On (`sources/tud/grace_fo/`), which has no record of any type. The Swarm accelerometer likewise has no instrument record. Worth reporting to SPASE.
2. **Instrument display in HSSI.** Rendered HSSI output lists related instruments by name only. The Swarm instrument records share a name across the three satellites, so four names will each appear three times with no indication of the satellite. The stored identifiers are distinct; this is a display characteristic worth raising with the HSSI maintainers.
3. **GeospaceLAB repository.** The README's built-in-data-sources table advertises `UTA/GITM/2DALL` and `UTA/GITM/3DALL`, which have never been shipped, and an `AMPEREDashboard` that is not implemented. `CITATION.cff` is stale at v0.5.10 / 2023-02-15 against a current release of v0.14.15. `visualization/plotly/ipanel.py`, `datahub.save_to_cdf` and `datahub.save_to_pickle` are unimplemented stubs.
