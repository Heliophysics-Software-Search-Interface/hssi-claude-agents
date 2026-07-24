# HSSI Metadata Extraction Results

**HSSI Software ID:** 55fe5714-b786-4cda-83f2-44afeb341a92
**Repository:** https://github.com/helioforecast/Predstorm
**Source Revision:** 5691ab48dca19b1b7d18e76ce88c33d3002b5275
**Extraction Date:** 2026-07-23
**Validation Date:** 2026-07-23
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** To be filled by actual submitter
- **Submitter Email:** To be filled by actual submitter
- **Source note:** Required placeholder; the repository does not identify the HSSI submitter.

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.3750748

- **Source note:** Retained from the existing HSSI record and confirmed by DataCite and Zenodo as the concept DOI for the archived Predstorm versions.

### 3. Code Repository (MANDATORY)
https://github.com/helioforecast/Predstorm

- **Source note:** Retained from the existing HSSI record and confirmed by the repository remote, `setup.py`, GitHub, and SoMEF.

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms: Heliospheric
- Coordinate Transforms: Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: ML/AI
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: Forecasting
- Models and Simulations: ML/AI

- **Source note:** The seeded `Models and Simulations` and `Models and Simulations: Forecasting` values were retained, and the classification was expanded from the current README, public package API, prediction code, plotting code, and real-time driver. Predstorm provides user-facing RTN-to-GSE, GSE-to-GSM, HEEQ, and related heliospheric/magnetospheric transformations; retrieves DSCOVR, STEREO, NOAA, OMNI, Kyoto Dst, HELCATS, and other time-series data; interpolates, filters, averages, merges, time-shifts, validates, and converts data into unified and saved products; performs scientific analysis and both empirical and machine-learning Dst/Kp/auroral-power prediction; and generates static 2D time-series line plots. Its forecasting models are driven by observed solar-wind measurements, recurrence data, and optional 3DCORE flux-rope output. Every selected child category includes its required parent.

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere
- Interplanetary Space
- Solar Environment

- **Source note:** Earth Magnetosphere and Solar Environment were retained from the existing HSSI record. Earth Atmosphere was added because the package explicitly predicts auroral power, and Interplanetary Space was added because its central purpose is propagating and forecasting solar-wind and magnetic-flux-rope measurements from L1, L5, STEREO, and other spacecraft in the inner heliosphere.

### 6. Authors (MANDATORY)
1. **Rachel L. Bailey**
   - **Author Identifier:** https://orcid.org/0000-0003-2021-6557
   - **Affiliations:**
     - Space Research Institute — https://ror.org/002w0jp71
     - Austrian Space Weather Office (Helio4Cast) — identifier not found
     - GeoSphere Austria — https://ror.org/0181cy234
2. **Christian Möstl**
   - **Author Identifier:** https://orcid.org/0000-0001-6868-4152
   - **Affiliations:**
     - Space Research Institute — https://ror.org/002w0jp71
     - Austrian Space Weather Office (Helio4Cast) — identifier not found
     - GeoSphere Austria — https://ror.org/0181cy234
3. **Ute Amerstorfer**
   - **Author Identifier:** https://orcid.org/0000-0003-1516-5441
   - **Affiliation:** Space Research Institute — https://ror.org/002w0jp71

- **Source note:** All three seeded authors were retained. The current README expands `R L Bailey` to Rachel L. Bailey and identifies Rachel Bailey and Christian Möstl as contributors associated with the Austrian Space Weather Office (Helio4Cast) and Conrad Observatory at GeoSphere Austria; those current affiliations were added by identity-aware set union. The seeded `Uvamerstorfer` creator was resolved to Ute Amerstorfer from the matching repository commit identity and email. DataCite and Zenodo confirm the three original creator records and their Space Research Institute affiliations. ROR identifiers were resolved against current ROR records. Crossref's record for the PREDSTORM-based Bailey et al. study identifies the three authors' ORCIDs, including Ute V. Amerstorfer's middle initial, and each public ORCID record resolves to the matching author; the repository-supported display name Ute Amerstorfer is retained.

### 7. Software Name (MANDATORY)
PREDSTORM

- **Source note:** Replaces the seeded `helioforecast Predstorm: First working version`, which is a Zenodo/GitHub owner plus release-title string rather than the software name. The authoritative current README heading uses `PREDSTORM`; the package and repository use the case variants `predstorm` and `Predstorm`.

### 8. Description (MANDATORY)
PREDSTORM is Python 3 software for space-weather prediction research. It predicts the background solar wind, high-speed solar-wind streams, and solar-storm magnetic flux ropes from solar-wind monitors at the Sun-Earth L1 and L5 points and from spacecraft east of the Sun-Earth line at or within about 1 AU. It also derives forecasts of the geomagnetic Dst and Kp indices and auroral power. For use in peer-reviewed scientific publications, the maintainers ask users to contact the contributors by email or Christian Möstl on Bluesky at @chrisoutofspace. Real-time results are available at https://helioforecast.space/solarwind.

- **Source note:** The existing HSSI description was retained in substance and refreshed only where current repository evidence is objectively newer: the README now points to Bluesky rather than Twitter, and the repository has continued receiving substantive updates through the extracted 2026-07-17 revision, making the seeded statement that it was last updated in 2023 stale.

### 9. Concise Description (OPTIONAL)
Forecasting of the solar wind and geomagnetic storms with spacecraft at L1, L5 or trailing the Earth in its orbit

- **Source note:** Retained verbatim from the existing HSSI record and confirmed as the current GitHub repository description by SoMEF.

### 10. Publication Date (RECOMMENDED)
2020-04-14

- **Source note:** Retained from the existing HSSI record and confirmed as the issued/publication date of the initial archived Zenodo release by DataCite and Zenodo. The GitHub repository itself was created earlier, on 2018-06-16.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

- **Source note:** Retained from the existing HSSI record and confirmed by the concept DOI metadata.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.0.0
- **Version Date:** 2025-08-04
- **Version Description:** First release
- **Version PID:** Not found

- **Source note:** Replaces the seeded `helioforecast Predstorm: First working version - v0.1.0` with the objectively newer latest GitHub release. GitHub/SoMEF identifies v1.0.0 as `First release`, published on 2025-08-04. The concept DOI currently resolves to archived v0.1.0 records and does not provide a version DOI for v1.0.0, while the current default branch contains later unreleased changes.

### 13. Programming Language (RECOMMENDED)
- Python 3.x

- **Source note:** Retained from the existing HSSI record and confirmed by the README, `setup.py`, environment files, and SoMEF/GitHub language analysis.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1029/2019SW002424

- **Source note:** Added from the maintainers' current PREDSTORM forecast page, which identifies Bailey et al. (2020), “Prediction of Dst During Solar Minimum Using In Situ Measurements at L5,” as the baseline study for the PREDSTORM solar-wind forecast. Crossref confirms the DOI and bibliographic record, and the paper's data-availability material identifies Predstorm as the Python software used for data handling.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

- **Source note:** Added from the repository `LICENSE`, `setup.py` classifier, GitHub, and SoMEF; the exact license name and URI match the localhost HSSI controlled vocabulary.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- auroral power
- DSCOVR
- Dst index
- geomagnetic forecasting
- heliophysics
- high-speed solar-wind streams
- Kp index
- magnetic flux ropes
- solar physics
- solar wind
- space physics
- space weather
- STEREO

- **Source note:** Added from the current README, repository topics reported by GitHub/SoMEF, package APIs, and prediction outputs. The existing HSSI record had no keywords.

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- Observatory/Mission-specific
- OMNIWeb
- Other
- WDC

- **Source note:** The package directly retrieves NOAA/SWPC JSON feeds, SPDF/OMNI data, STEREO and DSCOVR mission data through HelioSat, Kyoto World Data Center Dst data, the HELCATS ICME catalogue, a Helio4Cast/PREDSTORM real-time feed, and an SDO image. `Other` covers HELCATS and the PREDSTORM-specific real-time source. Observatory/Mission-specific is cross-listed with Fields 31–32.

### 18. Input File Formats (RECOMMENDED)
- ascii
- CDF
- HDF5
- JSON
- Other

- **Source note:** Repository code reads OMNI/Kyoto/PREDSTORM text data, STEREO and DSCOVR CDF products through HelioSat, pandas-created HDF5 archives, NOAA and HELCATS JSON, and Python pickle/model files (`Other`).

### 19. Output File Formats (RECOMMENDED)
- ascii
- Other

- **Source note:** `save_to_file()` and the real-time driver write documented text products. The package also creates Python pickle archives and PNG plots, represented by `Other` because those formats are not separate controlled values.

### 20. Operating System (RECOMMENDED)
- Operating System Independent

- **Source note:** Added from the explicit `Operating System :: OS Independent` package classifier. The Python/Conda installation instructions contain no platform-specific restriction.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

- **Source note:** The Python implementation and documented dependencies do not require a specific CPU architecture or accelerator.

### 22. Related Phenomena (OPTIONAL)
- Coronal Mass Ejections
- Geomagnetic Storms
- Solar Wind

- **Source note:** Geomagnetic Storms and Solar Wind were retained from the existing HSSI record. Coronal Mass Ejections was added from the README's solar-storm magnetic-flux-rope scope, the HELCATS ICME catalogue integration, ICME-aware processing, and optional 3DCORE flux-rope forecasts. All values match the localhost controlled vocabulary.

### 23. Development Status (RECOMMENDED)
Active

- **Source note:** The repository has reached a usable released state and remains actively developed. The extracted default-branch revision is dated 2026-07-17 and adds new NOAA JSON handling, HDF storage handling, and a new Dst prediction method.

### 24. Documentation (RECOMMENDED)
https://github.com/helioforecast/Predstorm#readme

- **Source note:** The repository README is the authoritative installation, configuration, execution, dependency, and usage documentation; no separate documentation site was found.

### 25. Funder (OPTIONAL)
- **Organization:** FWF Austrian Science Fund
- **Funder Identifier:** https://ror.org/013tf3c58

- **Source note:** The institutional PREDSTORM conference record states that the software was developed as part of the project “Enhanced lead time for geomagnetic storms.” The official project record at https://doi.org/10.55776/P31659 identifies the Austrian Science Fund as funder, and the ROR record supplies the canonical name and identifier.

### 26. Award Title (OPTIONAL)
- **Award Title:** Enhanced lead time for geomagnetic storms
- **Award Number:** P31659

- **Source note:** Added from the institutional PREDSTORM conference record and the official Austrian Science Fund project record at https://doi.org/10.55776/P31659.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
https://doi.org/10.5194/egusphere-egu2020-7892

- **Source note:** Added from the developer-authored EGU abstract “Forecasting the Dst index from L5 in-situ data using PREDSTORM: accuracy and applicability,” confirmed by Crossref and the Copernicus meeting record. The Bailey et al. journal article remains in Field 14 and is not duplicated here.

### 28. Related Datasets (OPTIONAL)
- **Dataset:** HELCATS WP4 Interplanetary Coronal Mass Ejection Catalogue (ICMECAT)
- **Dataset DOI:** https://doi.org/10.6084/m9.figshare.4588315.v1

- **Source note:** `get_icme_catalogue()` directly downloads and parses the HELCATS WP4 ICMECAT V10 JSON and links to the catalogue page. That primary catalogue page identifies the exact catalogue version and its Figshare DOI.

### 29. Related Software (OPTIONAL)
- Helio4Cast — https://github.com/helioforecast/helio4cast
- HelioSat — https://github.com/helioforecast/HelioSat

- **Source note:** The README explicitly requires a local Helio4Cast installation for NOAA real-time solar-wind handling, and `setup.py` plus the source data readers directly depend on HelioSat for heliospheric spacecraft data and positions.

### 30. Interoperable Software (OPTIONAL)
- 3DCORE — https://github.com/cmoestl/3DCORE

- **Source note:** The real-time driver has an explicit `--use3DCORE` mode and consumes 3DCORE magnetic-flux-rope output to fill and visualize the forecast interval.

### 31. Related Instruments (OPTIONAL)
1. **Instrument Name:** DSCOVR PlasMag Faraday Cup
   - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/DSCOVR/PlasMag/FaradayCup
2. **Instrument Name:** DSCOVR PlasMag Fluxgate Magnetometer
   - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/DSCOVR/PlasMag/FluxgateMagnetometer
3. **Instrument Name:** STEREO-A IMPACT Magnetometer
   - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-A/IMPACT/MAG
4. **Instrument Name:** Plasma and Supra-Thermal Ion Composition
   - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-A/PLASTIC
5. **Instrument Name:** STEREO-B IMPACT Magnetometer
   - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-B/IMPACT/MAG
6. **Instrument Name:** Plasma and Supra-Thermal Ion Composition
   - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-B/PLASTIC

- **Source note:** Predstorm's mission-specific readers directly consume the magnetic-field and plasma measurements used for DSCOVR and STEREO solar-wind forecasts. The corresponding Faraday Cup, fluxgate magnetometer, IMPACT magnetometer, and PLASTIC rows were resolved against the localhost HSSI vocabulary by mission path and measurement role, preferring canonical non-`.html` SMWG identifiers. The helper that downloads a latest SDO/AIA image was considered but excluded: it provides ancillary presentation imagery rather than making Predstorm a tool designed to process or analyze AIA observations.

### 32. Related Observatories (OPTIONAL)
1. **Observatory Name:** Deep Space Climate Observatory, DSCOVR
   - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/DSCOVR
2. **Observatory Name:** Solar Terrestrial Relations Observatory A
   - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/STEREO-A
3. **Observatory Name:** Solar Terrestrial Relations Observatory B
   - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/STEREO-B

- **Source note:** Predstorm directly downloads, processes, time-shifts, models, and visualizes DSCOVR and STEREO-A/B measurements as core forecast inputs. Each mission was resolved against the localhost SPASE-backed vocabulary, using the SMWG entry to break same-mission duplicate-name/path candidates. SDO was considered but excluded under the designed-to-support relevance gate because only an ancillary latest-image download helper references it.

### 33. Logo (OPTIONAL)
Not found

- **Source note:** No software logo is present in the repository, current README, PyHC registry, DataCite/Zenodo records, or SoMEF output.

---

## Extraction Sources Summary

- Existing HSSI metadata from `GET http://localhost/api/view/software/55fe5714-b786-4cda-83f2-44afeb341a92/`, used as the authoritative seed.
- Repository revision `5691ab48dca19b1b7d18e76ce88c33d3002b5275`, including README, package metadata, license, environments, public APIs, forecasting/data/plotting modules, real-time scripts, tags, releases, and git history.
- DataCite and Zenodo records for concept DOI `10.5281/zenodo.3750748`.
- SoMEF 0.9.11 output for the current GitHub repository.
- All three current PyHC registry files; no Predstorm entry was found.
- Localhost HSSI controlled vocabularies, including SPASE-backed instrument/observatory rows.
- ROR API records used to resolve institutional identifiers.
