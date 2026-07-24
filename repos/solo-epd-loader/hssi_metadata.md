# HSSI Metadata Extraction Results

**HSSI Software ID:** 06813bb3-7c73-425d-b9fe-6b4e80add160
**Repository:** https://github.com/jgieseler/solo-epd-loader
**Source Revision:** fcbba24e79bb2563759c383917b76a04f8b9a5b9
**Extraction Date:** 2026-07-24
**Validation Date:** 2026-07-24
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** To be filled by actual submitter
- **Submitter Email:** To be filled by actual submitter
- **Source note:** Required placeholder; the repository does not identify the HSSI submitter.

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.7100450

- **Source note:** Retained from the existing HSSI record and confirmed by current DataCite and Zenodo metadata as the concept DOI for all versions of `solo-epd-loader`.

### 3. Code Repository (MANDATORY)
https://github.com/jgieseler/solo-epd-loader

- **Source note:** Retained from the existing HSSI record and confirmed by the repository remote, `CITATION.cff`, `pyproject.toml`, GitHub, PyHC, DataCite/Zenodo, and SoMEF.

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:Pitch Angle Distributions
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Time Series Analysis

- **Source note:** Added from the current README, public API, implementation, and tests. The package queries the Solar Orbiter Archive (SOAR) TAP service and downloads mission CDF products; reads EPT, HET, and STEP fluxes, uncertainties, energy-channel metadata, pitch angles, RTN particle-flow directions, and HCI spacecraft context into pandas objects; computes STEP electron measurements with correction factors and contamination masks; corrects EPT electrons for ion contamination using a packaged contamination matrix; combines energy channels and STEP pixels; creates omnidirectional averages; and resamples time series with propagated uncertainties. These are user-facing scientific analysis, calibration/correction, retrieval, reduction, energy-spectrum, pitch-angle-distribution, general processing, and time-series capabilities. Every selected child includes the required parent. Data Visualization was considered but not selected because the plotting shown in the README is performed by downstream pandas/Matplotlib calls rather than a plotting API implemented by this package. Mission-related was also not selected because this is an independent mission-data loader, not Solar Orbiter ground-system or operations software.

### 5. Related Region (MANDATORY)
- Interplanetary Space
- Solar Environment

- **Source note:** Interplanetary Space was retained from the existing HSSI record. Solar Environment was added because the package is explicitly designed for Solar Orbiter energetic-particle measurements and its documented science examples analyze solar energetic electron and ion events in the inner heliosphere.

### 6. Authors (MANDATORY)
1. **Jan Gieseler**
   - **Author Identifier:** https://orcid.org/0000-0003-1848-7067
   - **Affiliation:** University of Turku — https://ror.org/05vghhr25
2. **Christian Palmroos**
   - **Author Identifier:** https://orcid.org/0000-0002-7778-5454
   - **Affiliation:** University of Turku — https://ror.org/05vghhr25

- **Source note:** Both seeded authors and their ORCIDs were retained. The existing affiliation UUID was resolved through the localhost HSSI organization vocabulary to University of Turku, and its ROR was confirmed through the ROR API. `CITATION.cff`, `.zenodo.json`, DataCite, and Zenodo independently confirm both authors and the affiliation.

### 7. Software Name (MANDATORY)
solo-epd-loader

- **Source note:** Retained verbatim from the existing HSSI record and confirmed by the repository name and README heading, `CITATION.cff`, `pyproject.toml`, PyPI, PyHC, GitHub, DataCite/Zenodo, and SoMEF.

### 8. Description (MANDATORY)
Data loader (and downloader) for Solar Orbiter/EPD energetic charged particle sensors EPT, HET, and STEP. Supports level 2, 3, and low latency data provided by ESA's Solar Orbiter Archive. It reads EPD CDF files into pandas DataFrames with fluxes, uncertainties, energy-channel metadata, and, for supported level 3 products, pitch-angle distributions and RTN/HCI spacecraft context. It can retrieve missing files from SOAR, combine energy channels and STEP pixels, resample time series, calculate STEP electron fluxes, and correct EPT electron fluxes for ion contamination. Only standard rates products are supported; SIS, burst, and high-cadence products are not included.

- **Source note:** Preserves the complete seeded description as its opening text and enriches it with authoritative current README, API, implementation, and test evidence about returned data, processing capabilities, and documented limitations. This also preserves the repository's important scientific-use caveat rather than implying support for all EPD products.

### 9. Concise Description (OPTIONAL)
Data loader (and downloader) for Solar Orbiter/EPD energetic charged particle sensors EPT, HET, and STEP. Supports level 2, 3, and low latency data provided by ESA's Solar Orbiter Archive.

- **Source note:** Retained verbatim from the existing HSSI record. It is 188 characters and remains within the 200-character field limit.

### 10. Publication Date (RECOMMENDED)
2022-01-12

- **Source note:** Replaces the seeded `2025-08-07`, which does not correspond to the software's initial publication. The repository was created and development began on 2022-01-11, and the first tagged public version, v0.1.0, was released on 2022-01-12.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

- **Source note:** Retained from the existing HSSI record and confirmed by current DataCite and Zenodo metadata for the concept DOI.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.4.4
- **Version Date:** 2025-10-06
- **Version Description:** Fixes a missing `mpl_animator` requirement and a pandas performance issue.
- **Version PID:** https://doi.org/10.5281/zenodo.17279850

- **Source note:** Added from the latest GitHub release, current repository tag history, PyPI, DataCite, and Zenodo. Zenodo resolves the concept DOI to v0.4.4 and identifies `10.5281/zenodo.17279850` as its version DOI. The current `CITATION.cff` has the correct v0.4.4 number and date but incorrectly retains `10.5281/zenodo.15130823`, which DataCite and Zenodo identify as the older v0.4.3 release; the authoritative current DOI APIs therefore supersede that stale field.

### 13. Programming Language (RECOMMENDED)
- Python 3.x

- **Source note:** Retained from the existing HSSI record and confirmed by `pyproject.toml` (Python >=3.9), Python source, current CI for Python 3.9–3.13, PyPI, GitHub, PyHC, and SoMEF.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.3389/fspas.2022.1073578

- **Source note:** Palmroos et al. (2022), “Solar energetic particle time series analysis with Python,” is a peer-reviewed Technology and Code article that explicitly identifies and documents `solo-epd-loader`, its Solar Orbiter/EPD and SOAR role, its level-2 and low-latency behavior, and its pandas/CDF workflow. The article's author-contribution statement credits Jan Gieseler with the data-loader software. The README's two developer-prioritized science-use papers remain in Field 27, and the EPD instrument/data-description paper remains in Field 28.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

- **Source note:** Added from `LICENSE.rst`, the README, `CITATION.cff`, `.zenodo.json`, GitHub, DataCite/Zenodo, and the matching localhost HSSI license row. SoMEF's file-content classifier also emitted a conflicting BSD-2-Clause label, but that automated guess is contradicted by the repository's explicit BSD-3-Clause declarations and three-clause license text.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- ESA
- Heliophysics
- Solar Orbiter
- energetic particles
- heliosphere
- solar energetic particles
- space physics
- space weather

- **Source note:** Heliophysics and Solar Orbiter were retained from the existing HSSI record. The submitted `Esa` spelling was corrected to the authoritative acronym `ESA`. The remaining terms were added by identity-aware set union from the current GitHub topics, the fully parsed PyHC community registry entry, the README's scientific scope, and the repository's particle-species/data-product support.

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific
- TAP

- **Source note:** Observatory/Mission-specific was retained from the existing HSSI record. TAP was added because `get_available_soar_files()` directly queries the SOAR TAP synchronous endpoint before the downloader retrieves the selected mission products. The mission-specific source is cross-listed with Solar Orbiter in Field 32.

### 18. Input File Formats (RECOMMENDED)
- CDF

- **Source note:** Retained from the existing HSSI record and confirmed throughout the README, included test data, implementation, and tests. VOTable is used only as an internal SOAR TAP response format and is not an available HSSI input-format value or a user-provided scientific input.

### 19. Output File Formats (RECOMMENDED)
Not found

- **Source note:** The public API returns pandas DataFrames and Python dictionaries in memory but does not implement a documented file-output format, so no unsupported file-format value was inferred.

### 20. Operating System (RECOMMENDED)
- Operating System Independent

- **Source note:** Added from the explicit `Operating System :: OS Independent` `pyproject.toml`/PyPI classifier. Current CI verifies Linux, and the pure Python package documentation contains no OS-specific restriction.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

- **Source note:** Added because the package is pure Python, PyPI distributes a `py3-none-any` wheel, and the repository declares no CPU-architecture or accelerator requirement.

### 22. Related Phenomena (OPTIONAL)
Not found

- **Source note:** The localhost controlled Phenomena list has no matching value for Solar Energetic Particles, and the user explicitly chose to omit the field.

### 23. Development Status (RECOMMENDED)
Active

- **Source note:** Added from the repository's explicit Repostatus Active badge and confirmed by a stable PyPI/GitHub v0.4.4 release plus continuing default-branch maintenance through the extracted 2026-07-01 revision.

### 24. Documentation (RECOMMENDED)
https://github.com/jgieseler/solo-epd-loader#readme

- **Source note:** Added from the fully parsed PyHC community registry and confirmed by the repository. The README is the current authoritative installation, usage, API, data-layout, caveat, and example documentation. A `.readthedocs.yaml` configuration exists, but no live Read the Docs project/site was found, so no unresolvable documentation URL was used.

### 25. Funder (OPTIONAL)
- **Organization:** European Commission
- **Funder Identifier:** https://ror.org/00k4n6c32

- **Source note:** Retained from the existing HSSI record. `.zenodo.json`, the README acknowledgements, DataCite, Zenodo, and Crossref's funder registry confirm European Commission funding for grant 101004159; the existing ROR matches the localhost HSSI organization row.

### 26. Award Title (OPTIONAL)
- **Award Title:** Solar EneRgetic ParticlE aNalysis plaTform for the INner hEliosphere (SERPENTINE)
- **Award Number:** 101004159

- **Source note:** Preserves the seeded award title and enriches it with the missing grant number from `.zenodo.json`, the README acknowledgement, DataCite/Zenodo, and the official Zenodo grant record.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1051/0004-6361/202039883
- https://doi.org/10.1051/0004-6361/202140940

- **Source note:** Added from the README's developer-prioritized references and normalized to full DOI URLs. They are, respectively, “First near-relativistic solar electron events observed by EPD onboard Solar Orbiter” and “First year of energetic particle measurements in the inner heliosphere with Solar Orbiter's Energetic Particle Detector.”

### 28. Related Datasets (OPTIONAL)
1. **Dataset DOI:** https://doi.org/10.1051/0004-6361/201935287
2. **Dataset:** SERPENTINE Solar Orbiter EPD Level 3 Data
   - **Dataset URL:** https://data.serpentine-h2020.eu/l3data/solo/

- **Source note:** The EPD instrument/data-description paper was retained from the existing HSSI record as the submitted descriptor for the supported Solar Orbiter EPD data. The SERPENTINE Level 3 dataset was added because the current README and `epd_load()` explicitly document and directly support those Solar Orbiter EPT one-minute products; no dataset DOI was found for that collection.

### 29. Related Software (OPTIONAL)
- SunPy — https://github.com/sunpy/sunpy
- cdflib — https://github.com/lasp/cdflib

- **Source note:** Added as the two core scientific data-I/O dependencies evidenced by `pyproject.toml` and the implementation. The loader directly uses SunPy's CDF reader and time utilities and cdflib's CDF access/epoch APIs. Current upstream repository URLs were confirmed through the corresponding PyPI metadata.

### 30. Interoperable Software (OPTIONAL)
- SEPpy — https://doi.org/10.5281/zenodo.7100437

- **Source note:** SEPpy is retained as the demonstrated high-level heliophysics integration: its current package directly depends on `solo-epd-loader`, and its documentation integrates the loader for Solar Orbiter EPD STEP, EPT, and HET data. The concept DOI identifies SEPpy persistently. pandas and Matplotlib are intentionally excluded from Interoperable Software because the user classifies these generic low-level dependencies as inappropriate for this field.

### 31. Related Instruments (OPTIONAL)
1. **Instrument Name:** Energetic Particle Detector
   - **Instrument Identifier:** https://spase-metadata.org/ESA/Instrument/SolarOrbiter/EPD
2. **Instrument Name:** Energetic Particle Detector / Electron Proton Telescope
   - **Instrument Identifier:** https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/EPD-EPT
3. **Instrument Name:** Energetic Particle Detector / High Energy Telescope
   - **Instrument Identifier:** https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/EPD-HET
4. **Instrument Name:** Energetic Particle Detector / SupraThermal Electrons and Protons
   - **Instrument Identifier:** https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/EPD-STEP

- **Source note:** The package is purpose-built to retrieve and process Solar Orbiter EPD data and explicitly supports its EPT, HET, and STEP sensors, so all four pass the designed-to-support relevance gate. Each was resolved by exact canonical name and Solar Orbiter mission path against the localhost SPASE-backed HSSI vocabulary. The Suprathermal Ion Spectrograph (SIS) was considered but deliberately excluded because the current README explicitly says it is not yet included.

### 32. Related Observatories (OPTIONAL)
1. **Observatory Name:** Solar Orbiter
   - **Observatory Identifier:** https://spase-metadata.org/ESA/Observatory/SolarOrbiter

- **Source note:** The package directly queries, downloads, reads, corrects, reduces, and exposes Solar Orbiter data as its primary function, so Solar Orbiter passes the designed-to-support relevance gate. The ESA vocabulary row was selected because it is the canonical Solar Orbiter observatory identified by the extraction guidance; the CNES/CDPP-AMDA duplicate is an archive-specific alternate row.

### 33. Logo (OPTIONAL)
Not found

- **Source note:** No software logo is present in the repository, current README, all three parsed PyHC registries, DataCite/Zenodo records, GitHub metadata, or SoMEF output. The two repository PNGs are scientific example plots, not logos.

---

## Extraction Sources Summary

- Existing HSSI metadata from `GET http://localhost/api/view/software/06813bb3-7c73-425d-b9fe-6b4e80add160/`, used to pre-populate every published field before enrichment.
- Repository revision `fcbba24e79bb2563759c383917b76a04f8b9a5b9`, including README, `CITATION.cff`, `.zenodo.json`, package metadata, license, documentation, CI, public API, tests, sample CDF data, tags, releases, and git history.
- Current DataCite and Zenodo concept/version records, GitHub repository/release metadata, PyPI package metadata, and Crossref publication/funder records.
- SoMEF output for the current GitHub repository.
- All three current PyHC registry files, parsed in full; `solo-epd-loader` was found in the community registry.
- Localhost HSSI organization, license, phenomenon, and SPASE-backed instrument/observatory vocabularies.
- ROR API records used to confirm institutional identifiers.
