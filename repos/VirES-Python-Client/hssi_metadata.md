# HSSI Metadata Extraction Results

**HSSI Software ID:** 15e95cb0-2008-4b98-83e9-0ce5a614b42c
**Repository:** https://github.com/ESA-VirES/VirES-Python-Client
**Source Revision:** c00f81d93a94529d7b7337b43ef7a36659420232 (`git describe` = v0.16.0-3-gc00f81d, committed 2026-05-14; verified identical to GitHub `master` HEAD)
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-07-29
**Validation Status:** PASS

**Seed basis (this is a seeded refresh, not a blank-slate extraction):**
- Live HSSI record on the target instance (`http://localhost`) - authoritative baseline for currently published values
- Prior canonical `hssi_metadata.md` in this repo, dated 2025-10-09 (supported file-only additions retained)
- Repository evidence at the revision above, plus DataCite/Zenodo/PyPI/GitHub/Crossref/ROR/PyHC/SPASE sources

**Legend for per-field notes:**
`LIVE` = unchanged from the live HSSI record - `ADD` = new value added by set-union -
`FILL` = field was empty in live HSSI - `REPLACE` = replaces a live value (evidence given) -
`CLEAR` = live value intentionally removed by user decision -
`EXCLUDED` = considered and deliberately not listed, with the reason

All decisions raised during this refresh have been resolved; see "Completed decisions" at the end.
No open questions remain and there are no approval blockers.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

Not part of the stored record; no live value to reconcile.

### 2. Persistent Identifier (RECOMMENDED)
**DOI:** https://doi.org/10.5281/zenodo.2554162

- Status: `LIVE` (unchanged)
- Source: CITATION.cff `identifiers` ("All versions of the software"); README.rst acknowledgement section; Zenodo record 19898676 reports `conceptdoi = 10.5281/zenodo.2554162`.
- This is the concept DOI covering all versions; the version-specific DOI is in Field 12.

### 3. Code Repository (MANDATORY)
**URL:** https://github.com/ESA-VirES/VirES-Python-Client

- Status: `LIVE` (unchanged)
- Source: CITATION.cff `repository-code`; pyproject.toml `[project.urls] homepage`; Zenodo `custom_fields["code:codeRepository"]`.

### 4. Software Functionality (MANDATORY)
**Selected Values (13):**
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Processing
- Mission-related
- Mission-related:Distribution/Access
- Models and Simulations
- Models and Simulations:Empirical
- Models and Simulations:Physics-Based

**Parent-completeness check (re-verified after the drop below):** every child has its parent present -
`Coordinate Transforms:Ionospheric` -> `Coordinate Transforms`; the five `Data Processing and Analysis:*`
children -> `Data Processing and Analysis`; `Mission-related:Distribution/Access` -> `Mission-related`;
`Models and Simulations:Empirical` and `:Physics-Based` -> `Models and Simulations`. No orphaned child, and
no parent lacking a considered child.

**Per-value evidence and status:**

| Value | Status | Evidence |
|---|---|---|
| Data Processing and Analysis | `LIVE` | parent category, already present |
| Data Processing and Analysis:Data Access and Retrieval | `LIVE` | core purpose: `SwarmRequest.get_between()`, `AeolusRequest.get_between()` fetch products from the VirES WPS endpoints (`_wps/wps_vires.py`) |
| Data Processing and Analysis:File Format Conversion | `LIVE` | `ReturnedData.as_dataframe()/as_xarray()/as_xarray_dict()`, `to_file()`, `to_files()`, `to_netcdf()` convert served CSV/CDF/netCDF into pandas/xarray and back out to csv/cdf/nc (`_data_handling.py`) |
| Data Processing and Analysis:Processing | `LIVE` | request chunking, response concatenation, `reshape_dataset()` reshaping of AUX_OBS/VOBS data into higher-dimensional objects, model-interpolation handling for 50 Hz MAGx_HR |
| Models and Simulations:Physics-Based | `LIVE` | user-facing forward evaluation of spherical-harmonic geomagnetic field models, including composition/customisation and evaluation at arbitrary user coordinates (`SwarmRequest.eval_model`, `eval_model_for_cdf_file`, `available_models`, `get_model_info`; docs/geomagnetic_models.rst) |
| Mission-related:Distribution/Access | `LIVE` | official ESA client for the VirES for Swarm / VirES for Aeolus services (README.rst; service run for ESA by EOX) |
| **Mission-related** | `ADD` | required parent of `Mission-related:Distribution/Access`, missing from the live record |
| **Models and Simulations** | `ADD` | required parent of `Models and Simulations:Physics-Based`, missing from the live record |
| **Models and Simulations:Empirical** | `ADD` | `MAGNETIC_MODELS` exposes IGRF (an empirical reference field model), CHAOS-8 core/static/MMA/MIO, LCS-1, MF7, MCO/MLI/MIO/MMA_SHA_2C/2D/2E/2F and AMPS (`_client_swarm.py:1585-1616`, `MODEL_REFERENCES`) - all data-derived empirical spherical-harmonic models |
| **Data Processing and Analysis:Analysis** | `ADD` | documented analysis capabilities beyond retrieval: data-model residuals (`residuals=True`), spacecraft conjunction identification (`get_conjunctions`), orbit-number and orbit-time queries (`get_orbit_number`, `get_times_for_orbits`), collection metadata queries (`get_collection_info`, `available_times`) - docs/capabilities.rst |
| **Data Processing and Analysis:Data Reduction** | `ADD` | server-side subsetting/filtering (`set_range_filter`, `set_choice_filter`, `set_bitmask_filter`, `add_filter`, `AeolusRequest.set_bbox`) and resampling to a coarser cadence (`sampling_step` in `set_products`, `COLLECTION_SAMPLING_STEPS`) - docs/capabilities.rst "Data subsetting/filtering", "Data resampling" |
| **Coordinate Transforms** | `ADD` | required parent of the value below |
| **Coordinate Transforms:Ionospheric** | `ADD` | quasi-dipole magnetic coordinates and magnetic local time are delivered as user-requestable columns: `QDLat`, `QDLon`, `QDBasis`, `MLT`, `QDOrbitDirection`, `DipoleAxisVector`, `DipoleTiltAngle`, `NGPLatitude`, `NGPLongitude` (`AUXILIARY_VARIABLES`, `_client_swarm.py:1536-1575`); docs/available_parameters.rst states "``QDLat`` and ``QDLon`` are quasi-dipole coordinates" and "``MLT`` is calculated from the QDLon and the subsolar position". The transform is computed server-side and delivered by the client - the identical client/server relationship that justifies the already-live `Models and Simulations:Physics-Based` value, so dropping one while keeping the other would be incoherent |

**`EXCLUDED` (considered, deliberately not listed):**
- **Data Processing and Analysis:Time Series Analysis** - considered and rejected. There is no analytical time-series operation in `src/` (no filtering, detrending, autocorrelation or spectral analysis of the returned series). The underlying evidence - `sampling_step`, `COLLECTION_SAMPLING_STEPS`, time-based request chunking - is already fully represented by `:Data Reduction` and `:Processing`, so listing it as well would triple-count one piece of evidence.
- **Data Visualization / Data Visualization:2D Graphics** - present in the 2025-10-09 canonical file but **not** in live HSSI, and not supported: there is no plotting code anywhere in `src/`. `matplotlib` appears only in docs/installation.rst as a suggestion for the *user's* environment. Not carried forward; this removes nothing from live HSSI.
- **Mission-related:Ingest** - `DataUpload` / `viresclient upload_file` uploads a user's own CDF/CSV into their private VirES account; this is user data going into a service, not mission-data ingest.
- **Mission-related:Inventory** - `available_collections/measurements/models/auxiliaries/observatories` are catalogue lookups for users, not mission inventory management.
- **Servers and Environments:\*** - viresclient is a client library; it implements no server.
- **Data Processing and Analysis:Calibration** - the ML-/ACAL-calibrated platform-magnetometer products (`MAG_GOCE_ML`, `MAG_GFO_ML`, `*_ACAL_CORR`) are *pre-calibrated products served to the client*; viresclient performs no calibration.
- **Models and Simulations:Data Guided** - AMPS is parameterised by solar-wind/IMF/F10.7 inputs, but that parameterisation happens inside the VirES server, so the claim is too indirect.

**Note on string form:** values are written in the documented `Parent:Child` form (no space after the colon). The HSSI *view* API renders them with a space (e.g. `Data Processing and Analysis: File Format Conversion`); that is a rendering transform, not stored drift.

### 5. Related Region (MANDATORY)
**Selected Values (4):**
- Earth Atmosphere - `LIVE`
- Earth Magnetosphere - `LIVE`
- **Earth Ionosphere** - `ADD`
- **Earth Thermosphere** - `ADD`

- **These additions reuse pre-existing values; they do not create vocabulary.** All four values come from the same HSSI Region vocabulary the two live values already come from. `Earth Ionosphere` and `Earth Thermosphere` are simply finer-grained members of that vocabulary that the documented Field 5 summary list does not enumerate.
- Evidence, Earth Ionosphere: the ionospheric product suite - `IPDxIRR` ionospheric plasma characteristics, `IBIxTMS` ionospheric bubble index, `TECxTMS` total electron content, `FACxTMS`/`FAC_TMS` field-aligned currents, PRISM `MITx_LP` and `MITxTEC` mid-latitude trough products, MIGRAS `NIX_TMS`/`TIX_TMS` gradient products, and the ULF/Pc1 wave products - together with the MIO ionospheric field models (`MIO_SHA_2C/2D`, `CHAOS-MIO`).
- Evidence, Earth Thermosphere: the source itself labels these products, at the explicit comment `# Swarm thermospheric density products:` (`_client_swarm.py:695`) introducing `DNS_POD` and `DNS_ACC`, immediately followed by `# TOLEOS thermospheric density and crosswind products:` introducing `DNS_ACC_CHAMP/GRACE/GFO` and `WND_ACC_CHAMP/GRACE/GFO`.
- Evidence retained for the two live values: Earth Atmosphere - Aeolus atmospheric wind products (L1B/L2A/L2B/L2C) plus the thermospheric and ionospheric products above. Earth Magnetosphere - magnetospheric field models (`CHAOS-MMA-Primary/Secondary`, `MMA_SHA_2C/2F`), field-aligned currents (`FAC`, `AOB_FAC`, `PPI_FAC`), auroral electrojets (`AEJ_*`), and `Kp`, `Dst`, `dDst`, `IMF_BY_GSM`, `IMF_BZ_GSM` auxiliaries.
- `EXCLUDED`: Interplanetary Space - `IMF_*` and `F107` are auxiliary context indices attached to LEO measurements, not a supported science region (they are recorded under Field 22 instead). Solar Environment, Planetary Magnetospheres - no support.

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Ashley R. A. Smith
- **Author Identifier:** https://orcid.org/0000-0001-5198-9574
- **Affiliation:** University of Edinburgh - https://ror.org/01nrxwf90
- Status: `LIVE` (unchanged, including affiliation)

**Author 2:**
- **Name:** Martin Pačes
- **Author Identifier:** Not found
- **Affiliation:** EOX IT Services (Austria) - https://ror.org/04yk5j107
- Status: `LIVE` (unchanged, including affiliation)

**Author 3:**
- **Name:** Daniel Santillan
- **Author Identifier:** Not found
- **Affiliation:** EOX IT Services (Austria) - https://ror.org/04yk5j107 - `ADD`
- Status: author `LIVE`; affiliation `FILL` (live record has no affiliation for this author)

**Sources and reconciliation:**
- Author set reconciled by union across live HSSI, the 2025-10-09 canonical file, CITATION.cff (Smith / Pačes / Santillan) and the Zenodo record creators. All four sources agree on exactly these three people; nobody is dropped.
- Affiliation for Daniel Santillan is evidenced by `daniel.santillan@eox.at` (CITATION.cff) and the EOX IT Services GmbH copyright on the source headers and LICENSE. Matched by ROR to the organisation row already used for Martin Pačes, so no new organisation is created.
- Organisation names are the existing HSSI/ROR display forms ("EOX IT Services (Austria)" = EOX IT Services GmbH, Vienna; "University of Edinburgh"). Independently corroborated by the reference publication's affiliations: "A. R. A. Smith - School of GeoSciences, University of Edinburgh"; "M. Pačes - EOX IT Services GmbH, Vienna, Austria".
- ORCIDs for Pačes and Santillan: searched the public ORCID API by family name; no confident match. Left as "Not found" rather than guessed.
- **Author order is meaningful metadata.** HSSI persists and displays author order, so the order listed here is part of the record rather than incidental. The order used above - Smith, Pačes, Santillan - is the authoritative maintainer-declared credit order, corroborated by three independent repository sources: the `CITATION.cff` `authors:` list, CITATION.cff's own example citation ("Smith, A. R. A., Pačes, M., & Santillan, D. (2025)"), and `pyproject.toml`, which names Ashley Smith as the sole author and maintainer. Live HSSI stores Pačes, Santillan, Smith, which credits the lead author and maintainer last; correcting that order is a deliberate, evidence-backed change to a live value, not incidental drift.
- `EXCLUDED`: "Swarm DISC" is a co-author of the *reference publication* (Crossref lists it as an organisational author) but is **not** a creator of the software in CITATION.cff or on Zenodo, so it is not added as an author. It is captured in Field 26 instead.

### 7. Software Name (MANDATORY)
**Name:** viresclient

- Status: `LIVE` (unchanged)
- Source: pyproject.toml `[project] name`; `src/viresclient/`; PyPI project name; PyHC registry `name`.
- Note: the repository/Zenodo title is `ESA-VirES/VirES-Python-Client` and SoMEF reports the repository name `VirES-Python-Client`. The package name `viresclient` is the correct HSSI software name and is retained; no change proposed.

### 8. Description (MANDATORY)
**Description:** viresclient is a Python package which connects to a VirES server, of which there are two: VirES for Swarm (https://vires.services) and VirES for Aeolus (https://aeolus.services), through the WPS interface. This package handles product requests and downloads, enabling easy access to data and models from ESA's Earth Explorer missions, Swarm and Aeolus. Data and models are processed on demand on the VirES server - a combination of measurements from any time interval can be accessed. The package handles the returned data to allow direct loading as a single pandas.DataFrame or xarray.Dataset, facilitating analysis of magnetic field measurements, atmospheric wind data, and associated geophysical models. Beyond Swarm and Aeolus, the service also provides recalibrated platform magnetometer data, thermospheric density and crosswind products, and total electron content and electron density products derived from CHAMP, CryoSat-2, GRACE, GRACE-FO and GOCE, as well as INTERMAGNET ground observatory data and Geomagnetic Virtual Observatory products, all retrievable through viresclient.

- Status: `REPLACE` by **addition only**. The live text is preserved verbatim and unedited; the final sentence is appended. No maintainer-derived wording was rewritten, reordered or shortened.
- Reason for the addition: the live description named only Swarm and Aeolus and therefore materially understated scope.
- Evidence for the appended sentence: README.rst - "Note that this service is not only for Swarm: Multi-mission products including magnetometry from CHAMP, CryoSat-2, and more; INTERMAGNET ground magnetometers via the ``AUX_OBS`` collection"; docs/available_parameters.rst - "...also INTERMAGNET ground observatories..., recalibrated platform magnetometer data from selected LEO missions..., total electron content (TEC), electron densities, temperatures... derived from spacecraft such as GOCE, CryoSat, GRACE, GRACE-FO, and more"; `COLLECTIONS` in `_client_swarm.py:522-729`.

### 9. Concise Description (OPTIONAL)
**Concise Description:** Tool for accessing ESA Swarm & Aeolus products from the VirES service

- Status: `LIVE` (kept unchanged). 69 characters, well within the 200-character limit.
- Decision recorded: the submitted value is respected because it is not stale, incomplete or incorrect. The 2025-10-09 canonical file's alternative ("A Python package for easy access to Swarm & Aeolus products as xarray.Dataset") is maintainer-authored and appears verbatim in four primary sources (CITATION.cff `abstract`, the GitHub repository description, the Zenodo record description, and SoMEF's highest-confidence description), but the difference is stylistic rather than factual, and a stylistic preference is not grounds for overwriting a curated value.

### 10. Publication Date (RECOMMENDED)
**Date:** 2018-06-20

- Status: `LIVE` (unchanged, independently confirmed)
- Source: GitHub API `created_at = 2018-06-20T13:07:28Z`; SoMEF `date_created = 2018-06-20T13:07:28Z`.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

- Status: `LIVE` (unchanged)
- Source: DataCite/Zenodo record for the concept DOI (`publisher = Zenodo`). Zenodo has no ROR of its own, so the URL form is used as the form permits.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.16.0
- **Version Date:** 2026-04-29
- **Version Description:** Adds the Swarm FAST product variants `SW_FAST_AEJxLPL_2F`, `SW_FAST_AEJxPBL_2F` and `SW_FAST_AOBxFAC_2F`; fixes a missing STT ground observatory; and fixes `reshape=True` when loading `AUX_OBSH` data as xarray by adding a `SiteCode` data variable.
- **Version PID:** https://doi.org/10.5281/zenodo.19898676

- Status: `REPLACE` - supersedes the stale live value `v0.13.0` (2025-04-27, PID `https://doi.org/10.5281/zenodo.15292625`).
- Evidence that v0.16.0 is the newest authoritative release available now (checked in all four places, not assumed):
  - Git: `v0.16.0` is the newest tag; `src/viresclient/__init__.py` declares `__version__ = "0.16.0"`.
  - GitHub Releases: latest is `v0.16.0`, published 2026-04-29 (next-newest `v0.15.2`, 2026-03-16).
  - PyPI: `info.version = 0.16.0`, uploaded 2026-04-29 (nothing newer).
  - Zenodo: the concept DOI's latest record is 19898676, `version = "v0.16.0"`, `publication_date = 2026-04-29`, DOI `10.5281/zenodo.19898676`.
  - Six releases were published between the live value and now: v0.14.0, v0.14.1, v0.15.0, v0.15.1, v0.15.2, v0.16.0.
- Version description sourced from docs/release_notes.rst ("Changes from 0.15.2 to 0.16.0") cross-checked against the GitHub release body. Where the two disagree (the GitHub release body says "AEJxPBS"), the release notes' `SW_FAST_AEJxPBL_2F` is used because it matches the code: `COLLECTIONS["AEJ_PBL"]` contains the FAST variant while `AEJ_PBS` does not.
- **Do not store the view-rendered form.** The live view renders the version as `viresclient - v0.13.0`; the stored value is the bare `v0.13.0`. The value to store is the bare `v0.16.0`.
- Full changelog for this version: https://github.com/ESA-VirES/VirES-Python-Client/compare/v0.15.2...v0.16.0

### 13. Programming Language (RECOMMENDED)
**Selected Values:**
- Python 3.x

- Status: `LIVE` (unchanged)
- Source: pyproject.toml `requires-python = ">=3.9"` with classifiers for Python 3.9-3.14; pure Python source tree; SoMEF `programming_languages = Python`.

### 14. Reference Publication (RECOMMENDED)
**DOI:** https://doi.org/10.3389/fspas.2022.1002697

- Status: `FILL` (live record was empty)
- Source: CITATION.cff `message` - "You may also wish to cite this paper: Smith A.R.A., Pačes M. and Swarm DISC (2022) Python tools for ESA's Swarm mission: VirES for Swarm and surrounding ecosystem. Front. Astron. Space Sci. 9:1002697"; the same recommendation appears in README.rst ("How to acknowledge VirES") and is linked from the README's Swarm section.
- Crossref confirms: "Python tools for ESA's Swarm mission: VirES for Swarm and surrounding ecosystem", Frontiers in Astronomy and Space Sciences, published 2022-10-31, authors A. R. A. Smith, M. Pačes, Swarm DISC. This is the publication describing the software and its ecosystem, and it is the maintainer-recommended paper to cite alongside the software DOI.
- This DOI is now held **only** here. It was removed from Field 27 by decision so that the two fields do not duplicate one another; see Field 27.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT

- Status: `FILL` (live record was empty)
- Source: `LICENSE` (full MIT text, "Copyright (c) 2018 EOX IT Services GmbH"); pyproject.toml classifier `License :: OSI Approved :: MIT License` and `license = { file = "LICENSE" }`; CITATION.cff `license: MIT`; Zenodo record `license = mit-license`; GitHub API `license.spdx_id = MIT`; SoMEF license detection.
- SPDX identifier: `MIT`. The name "MIT License" matches the existing HSSI License vocabulary row exactly, so no new row is created.
- Copyright holder: EOX IT Services GmbH (2018).

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Live values retained (14, stored lowercase; the view renders them Title Case - casing is not drift):**
aeolus, array, data access, data retrieval, earth observation, esa, geomagnetic field, geospace, ionosphere thermosphere mesosphere, magnetosphere, swarm, vires, webservices, wps

**`ADD` (16). Every one of these already exists in the live HSSI Keyword vocabulary, so no new vocabulary rows are created:**

| Keyword | Evidence |
|---|---|
| magnetic field | magnetic data products (`MAG`, `MAG_HR`, multi-mission `MAG_*`) and geomagnetic field models |
| geomagnetism | geomagnetic core/lithospheric/ionospheric/magnetospheric field models and observatory data |
| igrf | `IGRF` in `MAGNETIC_MODELS`; `MODEL_REFERENCES["IGRF"]` cites IGRF-14 |
| empirical model | spherical-harmonic empirical field models (IGRF, CHAOS-8, LCS-1, MF7, AMPS, MCO/MLI/MIO/MMA) |
| satellite data | LEO satellite products from Swarm, CHAMP, CryoSat-2, GRACE, GRACE-FO, GOCE |
| ground magnetometer | `AUX_OBSH/OBSM/OBSS` INTERMAGNET observatory collections keyed by IAGA code |
| ionosphere | `TEC`, `EFI` (`EFIx_LP`), `IBI`, `IPD`, `MIT_LP`, `MIT_TEC`, `FAC`, `NIX_TMS`, `TIX_TMS`, MIO ionospheric field models |
| thermosphere | `DNS_POD`, `DNS_ACC`, `DNS_ACC_CHAMP/GRACE/GFO`, `WND_ACC_*` thermospheric density and crosswind products |
| total electron content | `SW_OPER_TECxTMS_2F` "Total electron content"; `TEC_TIRO` multi-mission TEC |
| electron density | `EFIx_LP` `N_elec`; `NE_TIRO` (`GR/GF_OPER_NE__KBR_2F`) |
| electron temperature | `EFIx_LP` `T_elec` |
| ion temperature | `EFI_TIE` (`SW_OPER_EFIxTIE_2_`) ion temperature estimates |
| auroral electrojet | `AEJ_LPL`, `AEJ_LPS`, `AEJ_PBL`, `AEJ_PBS` "Auroral electrojets line profile" products |
| gnss | Swarm GNSS-derived TEC and precise-orbit products (`TEC`, `MOD_SC`, `DNS_POD`) |
| in situ measurements | in-situ LEO plasma and field measurements |
| xarray | `as_xarray()`/`as_xarray_dict()` are the documented primary output form (README.rst example; docs/api.rst) |

**`EXCLUDED`:**
- `remote`, `specific` - PyHC taxonomy tokens from the registry entry. Meaningless as standalone HSSI keywords; the informative PyHC tokens (`geospace`, `ionosphere_thermosphere_mesosphere`, `data_access`, `data_retrieval`) are already present in live HSSI.
- `pandas`, `python`, `time series` - either absent from the vocabulary (`pandas`) or too generic to aid discovery.

### 17. Data Sources (OPTIONAL)
**Selected Values:**
- Observatory/Mission-specific - `LIVE`
- Other - `LIVE`
- **VirES** - `ADD`

- Evidence for `VirES`: the package exists solely to talk to the two VirES services - README.rst ("There are two VirES services (Virtual environments for Earth Scientists) which *viresclient* can communicate with"), `_wps/wps_vires.py`, `ClientConfig`/`set_token` defaults for `https://vires.services/ows`. `VirES` is an allowed Field 17 value and was simply missing.
- `Observatory/Mission-specific` is correct and is cross-listed with Fields 31/32 per the form instructions (mission-specific product collections for Swarm, Aeolus, CHAMP, GRACE, GOCE, Ørsted, and the INTERMAGNET observatory network).
- Specific services: VirES for Swarm (https://vires.services), VirES for Aeolus (https://aeolus.services).
- `EXCLUDED`: `HAPI` - the VirES *server* exposes a HAPI interface (docs/geomagnetic_models.rst "Model values through HAPI"), but viresclient itself communicates over WPS only and ships no HAPI client. `HTTP/HTTPS Directories` - the client calls a WPS endpoint, not directory listings.

### 18. Input File Formats (RECOMMENDED)
**Selected Values:**
- CDF - `LIVE`
- netCDF3/4 - `LIVE`
- Other - `LIVE`
- **csv** - `ADD`
- **HDF5** - `ADD`
- **ascii** - `ADD`

- CDF: `SwarmRequest.eval_model_for_cdf_file(models, input_cdf_filename, ...)` reads a local Swarm-like CDF; `FileReader._open_cdf()` reads CDF via cdflib; `DataUpload.post("example.cdf")`; `tests/data/test_data_01.cdf`.
- netCDF3/4: `AeolusRequest.get_from_file(path, filetype="nc")` loads a local netCDF file.
- csv: `make_pandas_DataFrame_from_csv()` and the `filetype="csv"` read path in `_data_handling.py`; `DataUpload.post("example.csv")` and `viresclient upload_file ... ./test.csv`; `tests/data/test_data_01.csv`.
- HDF5: `SwarmRequest.eval_model` reads the model-evaluation result back from an HDF5 file with `h5py` (`_read_hdf5_file`); `h5py >= 3.12.1` is a hard dependency.
- ascii: `set_products(custom_model=...)` opens and reads a user-supplied plain-text `.shc` spherical-harmonic coefficient file (`_client_swarm.py:2039-2046`, and again in `get_model_info`).

### 19. Output File Formats (RECOMMENDED)
**Selected Values:**
- CDF - `LIVE`
- csv - `LIVE`
- HDF5 - `LIVE`
- netCDF3/4 - `LIVE`
- Other - `LIVE`

- No change. All five remain justified: `ReturnedDataFile`/`ReturnedData` support `("csv", "cdf", "nc")` via `to_file()`/`to_files()` (exercised over all `SUPPORTED_FILETYPES` in `tests/test_ReturnedData.py`), `to_netcdf()` writes netCDF, `eval_model` writes an HDF5 request payload with `h5py`, and `eval_model_for_cdf_file` writes an output CDF.
- Note: the `tables`/PyTables dependency was removed in v0.15.0, but HDF5 output remains valid via `h5py`.

### 20. Operating System (RECOMMENDED)
**Selected Values:**
- Operating System Independent

- Status: `LIVE` (unchanged)
- Source: pyproject.toml classifier `Operating System :: OS Independent`; pure-Python implementation.
- `EXCLUDED`: `Linux`, `Mac`, `Windows` individually - CI does test `ubuntu-24.04`, `macos-14` and `windows-2022` (.github/workflows/main.yml), but listing them alongside "Operating System Independent" adds noise rather than information.

### 21. CPU Architecture (RECOMMENDED)
**Selected Values:**
- CPU Independent

- Status: `LIVE` (unchanged)
- Source: pure Python, no compiled extensions; flit_core build backend produces a pure-Python wheel.

### 22. Related Phenomena (OPTIONAL)
**Selected Values (2):**
- **Geomagnetic Storms** - `FILL`
- **Solar Wind** - `FILL`

- Both are pre-existing values in the HSSI Phenomena vocabulary, so neither creates vocabulary. The live record held no phenomena at all.
- Evidence, Geomagnetic Storms: the client delivers the standard storm diagnostics as user-requestable auxiliaries - `Kp`, `Kp10`, `Dst`, `dDst` (`AUXILIARY_VARIABLES`, `_client_swarm.py:1536-1575`) - together with magnetospheric field models (`CHAOS-MMA-Primary/Secondary`, `MMA_SHA_2C/2F`) and auroral/field-aligned-current products.
- Evidence, Solar Wind: `IMF_BY_GSM`, `IMF_BZ_GSM`, `IMF_V` (solar wind velocity), plus `F107` and `F10_INDEX`, are user-requestable auxiliaries at `_client_swarm.py:1546-1574` and are documented in the Swarm auxiliaries listing at `docs/available_parameters.rst:374`.
- Vocabulary expansion was considered for domain-specific phenomena evidenced by the product collections (for example field-aligned currents, plasma bubbles, auroral electrojets and ULF waves) and was **declined by decision**: the Phenomena vocabulary is small and solar-focused, and it is not to be extended from this record.

### 23. Development Status (RECOMMENDED)
**Status:** Active

- Status: `FILL` (live record was empty)
- Evidence: pyproject.toml classifier `Development Status :: 5 - Production/Stable`; six releases in the 15 months to 2026-04-29 (v0.14.0 -> v0.16.0); commits on `master` through 2026-05-14; weekly scheduled CI (.github/workflows/main.yml); PyHC registry rates software maturity "Good". Matches the repostatus.org definition of "Active" - stable, usable, and actively developed.

### 24. Documentation (RECOMMENDED)
**URL:** https://viresclient.readthedocs.io/

- Status: `REPLACE` (approved canonicalisation) - live value is `http://viresclient.readthedocs.io/`.
- Evidence: the GitHub repository's own `homepage` field is `https://viresclient.readthedocs.io`; the PyHC registry lists `https://viresclient.readthedocs.io`; Read the Docs serves the site over HTTPS and redirects the plain-HTTP form to it.
- Additional documentation (single-URL field, recorded here for reference): Swarm Notebooks https://notebooks.vires.services - Aeolus Notebooks https://notebooks.aeolus.services - GitHub wiki https://github.com/ESA-VirES/VirES-Python-Client/wiki (found by SoMEF) - Swarm handbook https://swarmhandbook.earth.esa.int.

### 25. Funder (OPTIONAL)
- **Organization:** European Space Agency
- **Funder Identifier:** https://ror.org/03wd9za21

- Status: `LIVE` (unchanged; ROR re-verified against the ROR API - `https://ror.org/03wd9za21` is European Space Agency).
- Corroborating evidence: README.rst - "This service is provided for ESA by EOX"; the reference publication's funding statement - "This work has been supported by the Swarm DISC project, funded by ESA through contract No. 4000109587/13/I-NB."
- `EXCLUDED`: EOX IT Services GmbH - the contractor that develops and operates the service, not a funder. It is recorded as an author affiliation (Field 6).

### 26. Award Title (OPTIONAL)
- **Award Title:** Swarm Data, Innovation, and Science Cluster (Swarm DISC)
- **Award Number:** 4000109587/13/I-NB

- Status: `FILL` (live record was empty)
- Source: funding statement of the reference publication that CITATION.cff recommends citing for this software (Smith, Pačes & Swarm DISC 2022, https://doi.org/10.3389/fspas.2022.1002697): "This work has been supported by the Swarm DISC project, funded by ESA through contract No. 4000109587/13/I-NB." Swarm DISC is also credited as an organisational co-author of that paper, and the repository's documentation links to the Swarm-DISC GitHub organisation (docs/index.rst).
- Confidence note: the award is documented in the reference publication rather than in the repository itself. No award/contract number appears anywhere in the repository, and Crossref carries no funder record for the paper.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Publications:** None - this field is intentionally empty.

- Status: `CLEAR` - the live value `https://doi.org/10.3389/fspas.2022.1002697` is **deliberately removed**, not overlooked.
- Reason: Field 27's definition covers publications *different from* the reference publication. That DOI is the reference publication, and it is now recorded in Field 14, so keeping it here would duplicate it and misrepresent the field's meaning. The DOI is therefore retained on the record - via Field 14 - and nothing is lost.
- No other publications qualify: the remaining DOIs cited in the source describe *data products and models* rather than this software, and are recorded under Field 28.

### 28. Related Datasets (OPTIONAL)
**Datasets (all `FILL` - live record was empty). Every entry is a DOI that the package itself cites for a collection or model it serves (`COLLECTION_REFERENCES` / `MODEL_REFERENCES` / `REFERENCES` in `src/viresclient/_client_swarm.py`), and every DOI was verified to resolve:**

| DOI | What it describes | Cited in code for |
|---|---|---|
| https://doi.org/10.5047/eps.2013.07.001 | The Swarm Satellite Constellation Application and Research Facility (SCARF) and Swarm data products (*Earth, Planets and Space*, 2013) | `REFERENCES["General Swarm"]` |
| https://doi.org/10.5047/eps.2013.07.011 | Observatory data and the Swarm mission (*Earth, Planets and Space*, 2013) | `AUX_OBSH`, `AUX_OBSM`, `AUX_OBSS` INTERMAGNET collections |
| https://doi.org/10.5880/GFZ.2.3.2019.004 | CH-ME-3-MAG - CHAMP 1 Hz Combined Magnetic Field Time Series (Level 3) dataset | `MAG_CHAMP` (`CH_ME_MAG_LR_3`) |
| https://doi.org/10.1186/s40623-020-01171-9 | Magnetic observations from CryoSat-2: calibration and processing of satellite platform magnetometer data | `MAG_CS` (`CS_OPER_MAG`) |
| https://doi.org/10.1186/s40623-021-01373-9 | Magnetometer data from the GRACE satellite duo | `MAG_GRACE` (`GRACE_A_MAG`, `GRACE_B_MAG`) |
| https://doi.org/10.1186/s40623-021-01364-w | Observing Earth's magnetic environment with the GRACE-FO mission | `MAG_GFO` (`GF1/GF2_OPER_FGM_ACAL_CORR`) |
| https://doi.org/10.5880/GFZ.2.3.2023.001 | GRACE-FO ML-calibrated magnetic field data | `MAG_GFO_ML` |
| https://doi.org/10.5880/GFZ.2.3.2022.001 | GOCE calibrated and characterised magnetometer data | `MAG_GOCE` |
| https://doi.org/10.5880/GFZ.2.3.2022.002 | GOCE ML-calibrated magnetic field data | `MAG_GOCE_ML` |
| https://doi.org/10.5281/zenodo.14012302 | IGRF-14 (International Geomagnetic Reference Field coefficients) | `MODEL_REFERENCES["IGRF"]` |

- Not listed: the ESA Swarm Level-1B/Level-2 products and the Aeolus L1B/L2 products themselves, which are referenced through the Swarm handbook (https://swarmhandbook.earth.esa.int) and the ESA Aeolus data pages rather than by DOI. The `AUX_OBS` collections additionally cite the BGS AUX_OBS API (https://auxobs-api.bgs.ac.uk/docs), which is not a DOI.

### 29. Related Software (OPTIONAL)
**Software (all `FILL` - live record was empty):**

| Entry | Relationship and specific evidence |
|---|---|
| https://github.com/ESA-VirES/VirES-Server | The companion server this client exists to talk to ("VirES for Swarm Server Packages"). viresclient's entire API is defined against that server's WPS processes - request templates `vires_fetch_filtered_data.xml`, `vires_get_model_info.xml`, `vires_times_from_orbits.xml`, `vires_get_observatories.xml`, `vires_get_conjunctions.xml`, `vires_get_collection_info.xml`, `model_eval_multipart_payload.xml` (`TEMPLATE_FILES`), driven through `_wps/wps_vires.py`. |
| https://github.com/hapi-server/client-python | Similar-purpose data-access client, named by this package's own documentation as the alternative for other data sources: docs/available_parameters.rst - "Check other packages such as `hapiclient`_ and others from `PyHC`_ for data from other sources." |
| https://github.com/klaundal/pyAMPS | Domain-specific model implementation behind a model viresclient exposes: `MODEL_REFERENCES["AMPS"]` = "AMPS - Polar currents magnetic field, https://github.com/klaundal/pyAMPS", and `AMPS` is listed in `MAGNETIC_MODELS`. |

- `EXCLUDED` (relevance gate): `numpy`, `pandas`, `requests`, `tqdm`, `Jinja2`, `flit_core`, `pytest`, `nox`, `Sphinx` - generic scientific-Python/tooling stack (Tier A); being a dependency is not a relationship that distinguishes this software. `netCDF4` and `h5py` - used internally only (netCDF writing via xarray; HDF5 payloads inside `eval_model`), with no user-facing exchange. `chaosmagpy` - plausible peer for CHAOS model evaluation but not referenced anywhere in this repository, so there is no evidence to cite.
- The 2025-10-09 canonical file listed this field as a raw dependency list (cdflib, Jinja2, netCDF4, pandas, requests, tables, tqdm, xarray). That is exactly what the current relevance gate excludes; those entries are not carried forward (they were never in live HSSI, so nothing is removed from the record). cdflib and xarray are relocated to Field 30, where a specific documented exchange exists.

### 30. Interoperable Software (OPTIONAL)
**Software:**

| Entry | Status | Demonstrated exchange (cited evidence) |
|---|---|---|
| https://doi.org/10.5281/zenodo.7826899 (SwarmPAL) | `LIVE` | SwarmPAL is the Swarm DISC analysis toolbox built on top of this client: its `pyproject.toml` declares `viresclient >= 0.11` as a hard dependency, and viresclient's own docs/installation.rst points users to the "Swarm DISC SwarmPAL processor (swarmpal-processor)" container image that ships viresclient. Output of viresclient is consumed directly by SwarmPAL. |
| https://doi.org/10.5281/zenodo.598201 (xarray) | `ADD` | `xarray.Dataset` is the package's documented primary interchange format, not an internal detail: `ReturnedData.as_xarray()`, `ReturnedDataFile.as_xarray()`, `as_xarray_dict()` and `to_netcdf()` are public, documented API (docs/api.rst); the README's worked example ends `ds = data.as_xarray()` and shows the resulting `xarray.Dataset`; the maintainers' one-line summary is "easy access to Swarm & Aeolus products as xarray.Dataset". Tier B requirement satisfied by a specific public-API exchange. |
| https://github.com/MAVENSDC/cdflib | `ADD` | Public API hands the user a cdflib object: `ReturnedDataFile.open_cdf()` is documented as "Returns the opened file as cdflib.CDF" (`_data_handling.py:491`, exposed through docs/api.rst), and `FileReader` reads served CDF products through cdflib. Tier B requirement satisfied by a specific public-API exchange. |

- `EXCLUDED` (relevance gate): `pandas` - Tier A, never listed, even though `as_dataframe()` is a documented interchange method. `numpy`, `requests`, `tqdm`, `Jinja2` - Tier A generic infrastructure. `h5py`, `netCDF4` - Tier B without a qualifying exchange (used internally; no h5py/netCDF4 object is handed to the user). `Jupyter` - viresclient is heavily used in the Swarm/Aeolus notebook recipes and the Swarm VRE, but that is a usage environment, not a data exchange. Blanket claims such as "part of the scientific Python ecosystem" or "a PyHC community package, so it interoperates with PyHC packages" are not sufficient and are not used here.
- The 2025-10-09 canonical file's entries for this field ("xarray ecosystem (matplotlib, scipy, dask, etc.)", "pandas ecosystem", "Jupyter notebooks", "Python scientific stack") are exactly the blanket ecosystem claims the gate rejects; only the specific, evidence-backed xarray exchange is carried forward.

### 31. Related Instruments (OPTIONAL)

All entries below were resolved against the live HSSI controlled instrument/observatory vocabulary (`type = 1` for instruments) and every SPASE identifier was verified to resolve. Names are copied verbatim from the matched row.

**Values (16, all `FILL` - live record had no related instruments):**

| # | Instrument Name (verbatim) | Instrument Identifier | Why the software is designed to support it |
|---|---|---|---|
| 1 | Absolute Scalar Magnetometer / Vector Field Magnetometer | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-A/MAG | Serves `SW_OPER_MAGA_LR_1B` / `MAGA_HR_1B` (and FAST variants), plus `ULFAMAG_2F`, `PC1AMAG_2F`; `PRODUCT_VARIABLES["MAG"]` exposes instrument-level fields `B_VFM`, `ASM_Freq_Dev`, `Flags_F`, `Flags_B` |
| 2 | Absolute Scalar Magnetometer / Vector Field Magnetometer | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-B/MAG | same, Swarm Bravo collections |
| 3 | Absolute Scalar Magnetometer / Vector Field Magnetometer | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-C/MAG | same, Swarm Charlie collections |
| 4 | Electric Field Instrument : Langmuir Probe | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-A/LP | Serves `SW_OPER_EFIA_LP_1B` (and FAST variant) and `SW_OPER_MITA_LP_2F`; `PRODUCT_VARIABLES["EFI"]` carries LP quantities `N_ion`, `N_elec`, `T_elec` and their flags |
| 5 | Electric Field Instrument : Langmuir Probe | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-B/LP | same, Swarm Bravo |
| 6 | Electric Field Instrument : Langmuir Probe | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-C/LP | same, Swarm Charlie |
| 7 | Electric Field Instrument : Thermal Ion Imager | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-A/TII | Serves `SW_EXPT_EFIA_TCT02` / `TCT16` cross-track ion flow, `SW_PREL_EFIAIDM_2_` ion drift, `SW_OPER_EFIATIE_2_` ion temperature |
| 8 | Electric Field Instrument : Thermal Ion Imager | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-B/TII | same, Swarm Bravo |
| 9 | Electric Field Instrument : Thermal Ion Imager | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-C/TII | same, Swarm Charlie |
| 10 | Global Navigation Satellite System | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-A/GNSS | Serves `SW_OPER_TECATMS_2F` (GPS-derived TEC, with `GPS_Position`, `PRN`, `L1`, `L2`, `Absolute_STEC` variables), `SW_OPER_MODA_SC_1B` positions and `SW_OPER_DNSAPOD_2_` POD-derived density |
| 11 | Global Navigation Satellite System | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-B/GNSS | same, Swarm Bravo |
| 12 | Global Navigation Satellite System | https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/SWARM-C/GNSS | same, Swarm Charlie |
| 13 | CHAMP Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/CHAMP/FGM | Serves `MAG_CHAMP` (`CH_ME_MAG_LR_3`), the CHAMP combined magnetic field time series derived from the fluxgate vector magnetometer |
| 14 | Scalar Overhauser Magnetometer | https://spase-metadata.org/SMWG/Instrument/CHAMP/OVM | Serves the same CHAMP combined magnetic field product, whose scalar component comes from the Overhauser magnetometer |
| 15 | Compact Spherical Coil | https://spase-metadata.org/SMWG/Instrument/Oersted/CSC | Ørsted's vector magnetometer, behind the Ørsted Geomagnetic Virtual Observatory products viresclient serves: `VOBS_OR_1M` / `VOBS_OR_4M` -> `OR_OPER_VOBS_1M_2_` / `OR_OPER_VOBS_4M_2_` (`_client_swarm.py:600-650`), including their `:SecularVariation` and per-site variants |
| 16 | Overhauser Effect Scalar Magnetometer on the Oersted spacecraft | https://spase-metadata.org/SMWG/Instrument/Oersted/OESM | Ørsted's scalar magnetometer, behind the same Ørsted Geomagnetic Virtual Observatory products |

**Per-spacecraft expansion rationale:** the vocabulary registers Swarm instruments separately for SWARM-A/B/C, and viresclient enumerates per-spacecraft collections for all three (`COLLECTIONS`, `MISSION_SPACECRAFTS = {"Swarm": ["A","B","C"], ...}`), so all three rows are genuinely supported. Because each row is supplied with its own SPASE identifier, the same-named rows are unambiguous on submission.

**No-collision check for the two Overhauser-magnetometer entries (#14 and #16):** they are distinct vocabulary entries that differ in **both** name and identifier - `Scalar Overhauser Magnetometer` (`.../SMWG/Instrument/CHAMP/OVM`) belongs to CHAMP, while `Overhauser Effect Scalar Magnetometer on the Oersted spacecraft` (`.../SMWG/Instrument/Oersted/OESM`) belongs to Ørsted. Both stay; there is no name clash to disambiguate. The Ørsted vector magnetometer is `Compact Spherical Coil` (abbreviation `CSC`, `.../SMWG/Instrument/Oersted/CSC`).

**`EXCLUDED` / omitted with documentation:**
- **Swarm accelerometer (ACC)** - listed in the 2025-10-09 canonical file. viresclient does serve `SW_OPER_DNSxACC_2_`, but no SPASE instrument row exists for it: searched the live vocabulary for `swarm` across name, abbreviation and identifier - only MAG, LP, TII, GNSS and Ephemeris rows exist for SWARM-A/B/C. Per the SPASE-only ladder, it is omitted rather than free-typed; its support is represented by the Swarm observatory entries in Field 32.
- **Aeolus ALADIN (Atmospheric LAser Doppler INstrument)** - listed in the 2025-10-09 canonical file. Searched the vocabulary for `aladin` in both `type = 1` and `type = 2`: zero matches; there is no SPASE instrument record for it. Omitted, with fallback to the `Aeolus` observatory entry in Field 32 as the ladder prescribes.
- **Swarm VFM and ASM as separate entries** - the 2025-10-09 canonical file listed them separately, but SPASE registers a single combined row per spacecraft ("Absolute Scalar Magnetometer / Vector Field Magnetometer"), which is what is used above.
- **`SWARM-A/B/C Orbital Information`, `CHAMP Ephemeris`** - ephemeris pseudo-instrument rows. The corresponding orbital products (`MOD_SC`, orbit-number and ascending-node queries) are better represented by the observatory entries; not listed to avoid inflating the instrument list.
- **`Digital Ion Drift Meter` (CHAMP/DIDM), IUGONET `CHAMP` GPS receiver row** - viresclient serves no CHAMP DIDM data; the IUGONET row is a duplicate registration of the CHAMP platform, superseded by the SMWG rows used above.
- **GRACE / GRACE-FO / GOCE / CryoSat-2 instruments** - no `type = 1` vocabulary rows exist for any of them (searched `grace`, `goce`, `cryo`: zero instrument matches). Their support is represented at observatory level in Field 32 where a SPASE record exists.

### 32. Related Observatories (OPTIONAL)

Resolved against the same controlled vocabulary (`type = 2`); every SPASE identifier verified to resolve. Names copied verbatim from the matched row.

**Values (9):**

| # | Observatory Name (verbatim) | Observatory Identifier | Status | Why the software is designed to support it |
|---|---|---|---|---|
| 1 | Swarm | https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM.html | `LIVE` | The mission the client is built for; the whole `SwarmRequest` API and the `SW_*` collection set |
| 2 | Aeolus | https://spase-metadata.org/SMWG/Observatory/AEOLUS.html | `LIVE` | `AeolusRequest` and the Aeolus L1B/L2A/L2B/L2C collections (docs/available_parameters_aeolus.rst) |
| 3 | Swarm Alpha | https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM-A | `ADD` | Per-spacecraft collections `SW_OPER_MAGA_*`, `EFIA_*`, `TECA*`, `FACA*`, `AEJA*`, `MODA_SC`, `DNSA*`; `MISSION_SPACECRAFTS["Swarm"]` includes "A"; A-C conjunction pairs |
| 4 | Swarm Bravo | https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM-B | `ADD` | Per-spacecraft `...B...` collections; `CONJUNCTION_MISSION_SPACECRAFT_PAIRS = {(("Swarm","A"),("Swarm","B"))}` |
| 5 | Swarm Charlie | https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM-C | `ADD` | Per-spacecraft `...C...` collections, including the dual-satellite `SW_OPER_FAC_TMS_2F` (A-C) product |
| 6 | CHAMP | https://spase-metadata.org/SMWG/Observatory/CHAMP | `ADD` | `MAG_CHAMP` (`CH_ME_MAG_LR_3`), `DNS_ACC_CHAMP`, `WND_ACC_CHAMP`, `TEC_TIRO` (`CH_OPER_TEC_TMS_2F`), `VOBS_CH_1M/4M` |
| 7 | Gravity Recovery and Climate Experiment | https://spase-metadata.org/SMWG/Observatory/GRACE | `ADD` | `MAG_GRACE` (`GRACE_A_MAG`, `GRACE_B_MAG`), `DNS_ACC_GRACE`, `WND_ACC_GRACE`, `TEC_TIRO`, `NE_TIRO`; `MISSION_SPACECRAFTS["GRACE"] = ["1","2"]` for orbit-number queries |
| 8 | Gravity Field and Steady-State Ocean Circulation Explorer | https://spase-metadata.org/SMWG/Observatory/GOCE | `ADD` | `MAG_GOCE` (`GO_MAG_ACAL_CORR`), `MAG_GOCE_ML`; `MISSION_SPACECRAFTS["GOCE"]` supported by `get_orbit_number` |
| 9 | International Real-time Magnetic Observatory Network | https://spase-metadata.org/SMWG/Observatory/Ground/INTERMAGNET | `ADD` | `AUX_OBSH`, `AUX_OBSM`, `AUX_OBSS` collections keyed by IAGA observatory code (`IAGA_CODES` in `_data/config_swarm.json`), plus `available_observatories()`; README.rst - "INTERMAGNET ground magnetometers via the ``AUX_OBS`` collection" |

**Resolved SPASE decisions:**
- **`.html`-vs-bare duplicate rows: retained as-is (recommended default, no change).** The two live entries bind to the `.html` form of their SPASE resource (`.../SWARM.html`, `.../AEOLUS.html`); bare-identifier rows for the same resources also exist (`.../CDPP-AMDA/SWARM`, named "Swarm : ESA mission", and `.../SMWG/Observatory/AEOLUS`, named "Aeolus"). Both forms resolve and denote the same resource, so re-pointing them would be a lateral move with no metadata gain, and for Swarm it would replace the clean display name "Swarm" with "Swarm : ESA mission". Decision: leave both live bindings untouched and record the duplication as a shared-vocabulary artifact rather than fixing it from this record.
- **Prior assumption corrected:** the two live observatory entries *do* already carry SPASE identifiers (the `.html` variants above). They were never identifier-less rows.
- **CHAMP same-name tie-break.** Two `type = 2` rows are named "CHAMP": `SMWG/Observatory/CHAMP` and `IUGONET/Observatory/RISH/CHAMP/CHAMP`. Resolved to the SMWG row using the documented SMWG tie-breaker, so this is a single unambiguous match rather than an open ambiguity.
- **GRACE / GOCE bare-vs-`.html`.** Both exist in bare and `.html` form; the bare rows (and their names) are used.
- **Ørsted: omitted here by decision, and captured instead at instrument level in Field 31.** The mission resolves to exactly one observatory row, `https://spase-metadata.org/SMWG/Observatory/Oersted`, but that row's `name` in the live vocabulary is the defective string `NSSDC ID: 1999-008B`, which would be displayed on this record. Because viresclient's Ørsted support runs through the `VOBS_OR_*` Geomagnetic Virtual Observatory products, the relationship is expressed more precisely - and without importing a broken display name - by the two Ørsted magnetometer rows added to Field 31 (`Compact Spherical Coil`, `Overhauser Effect Scalar Magnetometer on the Oersted spacecraft`). The mission is therefore represented on the record, not dropped.

**Omitted with documentation (genuinely supported, but no SPASE record found - not "not related"):**
- **CryoSat-2** - supported via `MAG_CS` (`CS_OPER_MAG`) and `VOBS_CR_1M/4M`, and named in `MISSION_SPACECRAFTS`. Searched the vocabulary for `cryo` across name/abbreviation/identifier in both types: zero matches; also probed `spase-metadata.org/SMWG/Observatory/CryoSat-2`, `/CryoSat2`, `/CryoSat`, `/Cryosat-2` - none exist. Omitted rather than free-typed, per the SPASE-only rule.
- **GRACE-FO (GRACE Follow-On)** - supported via `MAG_GFO`, `MAG_GFO_ML`, `DNS_ACC_GFO`, `WND_ACC_GFO`, `TEC_TIRO`, `NE_TIRO`, and named in `MISSION_SPACECRAFTS`. Searched `follow[- ]?on`, `GRACE-FO`, `GFO`: zero matches; probed `/SMWG/Observatory/GRACE-FO`, `/GRACEFO`, `/GRACE_FO`, `/GRACE-FO1`, `/GRACEFollowOn` - none exist. Omitted for the same reason. Note that `SMWG/Observatory/GRACE` covers only the original GRACE duo and must not be used as a stand-in.

**No unresolved ambiguity remains in Fields 31/32.** Every emitted value carries a verified `https://spase-metadata.org/` identifier and a single matched row, so there is no approval blocker on these fields.

### 33. Logo (OPTIONAL)
**URL:** https://raw.githubusercontent.com/ESA-VirES/Swarm-VRE/staging/docs/_static/vre_logo.png

- Status: `REPLACE` - the live value `https://raw.githubusercontent.com/ESA-VirES/VirES-Python-Client/refs/heads/master/docs/images/vre_lo` is dead. It is a truncated URL, exactly 100 characters long and cut off mid-filename, and it does not exist.
- Candidates tested, with the result for each:

  | Candidate | Result |
  |---|---|
  | `.../VirES-Python-Client/refs/heads/master/docs/images/vre_lo` (live value) | does not exist - dead |
  | `.../VirES-Python-Client/refs/heads/master/docs/images/vre_logo.png` (presumed intended target) | does not exist - the file is absent from the repo and from its entire git history |
  | `.../VirES-Python-Client/refs/heads/master/docs/images/vre_logo_light.svg` | resolves, serves `image/svg+xml` - valid alternative, in-repo |
  | `.../Swarm-VRE/staging/docs/_static/vre_logo.png` (**selected**) | resolves, serves `image/png` |

- Why the selected URL: it resolves to a real PNG image, and it is the value curated in the PyHC registry for this package (`logo:` in `_data/projects.yml`), which is the highest-priority metadata source in the HSSI extraction order. It is also the value carried in the 2025-10-09 canonical file, so this restores a previously-correct value rather than inventing one.
- In-repo alternative, if a same-repository asset is preferred: `https://raw.githubusercontent.com/ESA-VirES/VirES-Python-Client/refs/heads/master/docs/images/vre_logo_light.svg` (SVG, light-background variant; added in commit 70eb6e9 and the only logo asset in the repository).
- Both images are the VirES/VRE logo; there is no viresclient-specific logo.

---

## Completed corrections in this refresh

1. **Version was stale by six releases.** `v0.13.0` (2025-04-27) -> `v0.16.0` (2026-04-29), with matching version-specific DOI `10.5281/zenodo.19898676` and a release-notes-derived description. Confirmed newest via git tags, GitHub Releases, PyPI and Zenodo.
2. **Logo was a dead, truncated URL.** Replaced with the PyHC-curated PNG after testing every candidate; the previously-presumed target `vre_logo.png` never existed in this repository.
3. **Software Functionality made complete and coherent.** The two missing required parents (`Mission-related`, `Models and Simulations`) added, along with `Models and Simulations:Empirical`, `:Analysis`, `:Data Reduction`, `Coordinate Transforms` and `Coordinate Transforms:Ionospheric`; final total 13 values, every child with its parent. `Data Visualization:2D Graphics` (old canonical file only) and `Data Processing and Analysis:Time Series Analysis` were both rejected on code evidence.
4. **Eight empty live fields filled:** License, Development Status, Reference Publication, Related Phenomena, Related Datasets, Related Software, Award Title, Related Instruments.
5. **Related Region sharpened.** `Earth Ionosphere` and `Earth Thermosphere` added from the same existing `Region` vocabulary, alongside the two live values.
6. **Description scope corrected additively.** One sentence appended to cover the multi-mission, ground-observatory and virtual-observatory products; the maintainer-derived text is untouched.
7. **Author affiliation gap closed.** Daniel Santillan now carries the same EOX organisation (matched by ROR, not by string) as Martin Pačes; no author was dropped or renamed.
8. **Reference publication separated from related publications.** The Frontiers DOI moved to Field 14 and cleared from Field 27, which is now intentionally empty.
9. **Related Instruments / Observatories resolved to SPASE.** 16 instrument rows and 7 new observatory rows resolved with verified SPASE identifiers; the two existing live observatory bindings retained; Ørsted captured at instrument level; CryoSat-2, GRACE-FO, Swarm ACC and Aeolus ALADIN omitted with a documented search trail because no SPASE record exists for them.
10. **Field 29/30 relevance gate applied.** The old canonical file's raw dependency list and blanket ecosystem claims were replaced with three cited related-software entries and two cited interoperability additions.

## Completed decisions

All questions raised during this refresh are resolved; none is pending.

1. **Field 4 - `Data Processing and Analysis:Time Series Analysis`: dropped.** No analytical time-series operation exists in `src/`; the underlying evidence is already covered by `:Data Reduction` and `:Processing`.
2. **Field 4 - `Coordinate Transforms` + `:Ionospheric`: kept.** Server-computed QD/MLT auxiliaries are delivered as user-requestable columns - the same client/server relationship that justifies the already-live `Models and Simulations:Physics-Based`.
3. **Field 5 - `Earth Ionosphere` and `Earth Thermosphere`: added.** Pre-existing rows in the same `Region` vocabulary; the software's ionospheric and thermospheric product suites are explicit in the source.
4. **Field 8 - multi-mission sentence: applied, additively.** The live description understated scope; no existing wording was altered.
5. **Field 9 - live concise description: kept.** It is not stale, incomplete or incorrect, so the submitted value stands; the maintainer-authored alternative is a stylistic variant only.
6. **Field 14 - Frontiers DOI: kept as the reference publication.** It is the maintainer-recommended paper describing the software.
7. **Field 22 - `Geomagnetic Storms` + `Solar Wind` only.** Both are existing rows; expanding the Phenomena vocabulary was considered and declined.
8. **Field 24 - HTTPS documentation URL: applied.** Matches the repository's own homepage field and the PyHC registry.
9. **Field 27 - cleared deliberately.** Field 27 is for publications other than the reference publication; the DOI now lives only in Field 14.
10. **Field 31/32 - Ørsted: added at instrument level, omitted at observatory level.** The two Ørsted magnetometer rows carry clean names and verified identifiers, whereas the sole Ørsted observatory row's name is the defective string `NSSDC ID: 1999-008B`.
11. **Field 32 - `.html`-vs-bare duplicate rows: left unchanged.** Re-pointing gains no metadata and would degrade the Swarm display name.
12. **Field 6 - author order corrected to CITATION.cff order.** HSSI persists and displays author order, and the live order credited the lead author and maintainer last; three independent repository sources agree on Smith, Pačes, Santillan.
