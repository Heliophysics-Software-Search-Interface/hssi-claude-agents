# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/GOESplot
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found - No DOI found in repository files (CITATION.cff, .zenodo.json, or codemeta.json do not exist)

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/GOESplot

### 4. Software Functionality (MANDATORY)
Based on code analysis and documentation:
- **Data Processing and Analysis**
- **Data Processing and Analysis:Data Access and Retrieval** (downloads GOES satellite data from NOAA servers)
- **Data Processing and Analysis:Image Processing** (processes and loads satellite imagery)
- **Data Processing and Analysis:Processing** (loads and processes GOES data from multiple formats)
- **Data Visualization**
- **Data Visualization:2D Graphics** (plots on geographic/map coordinates using Cartopy)
- **Mission-related:Distribution/Access** (provides access to GOES mission data)

### 5. Related Region (MANDATORY)
Based on GOES satellite mission scope and PyHC keywords:
- **Earth Atmosphere** (GOES satellites primarily observe Earth's weather and atmospheric phenomena)
- **Solar Environment** (GOES monitors solar activity and space weather)
- **Earth Magnetosphere** (related to space weather observations)

### 6. Authors (MANDATORY)
- **Authors:** Michael Hirsch, Ph.D.
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

### 7. Software Name (MANDATORY)
GOESplot (also referred to as "goesplot" in package metadata and "GOESutils" in PyHC registry)

### 8. Description (MANDATORY)
Download and plot GOES satellite PNGs and high-resolution NetCDF4 by date/time. This Python package provides tools to download GOES (Geostationary Operational Environmental Satellite) preview images at 3-hour cadence and full-fidelity NetCDF4 data at 1-minute cadence from NOAA repositories. The software includes functionality to plot GOES infrared and other data georegistered on map coordinates using Cartopy. It supports both GOES-13 and GOES-16 satellites and can access data from the NOAA NCDC GIBBS service for preview images and NOAA CLASS for high-resolution data.

### 9. Concise Description (OPTIONAL)
Quick Python script to download and plot GOES satellite preview and hi-resolution data by date/time.

### 10. Publication Date (RECOMMENDED)
2018-02-22 (from first git commit)

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

### 12. Version (RECOMMENDED)
- **Version Number:** v1.1.0 (from setup.cfg; most recent tagged release is v1.0.8)
- **Version Date:** 2018-08-19 (date of v1.0.8 tag; v1.1.0 is untagged)
- **Version Description:** Initial Release (description for v1.0.8)
- **Version PID:** Not found

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** (requires Python >= 3.7)

### 14. Reference Publication (RECOMMENDED)
Not found

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** http://www.apache.org/licenses/LICENSE-2.0

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
From multiple sources:
- goes (setup.cfg)
- satellite (setup.cfg)
- goes13 (GitHub topics)
- goes16 (GitHub topics)
- noaa (GitHub topics)
- ionosphere_thermosphere_mesosphere (PyHC)
- solar (PyHC)
- magnetosphere (PyHC)
- space weather
- atmospheric science (from setup.cfg classifier)

### 17. Data Sources (OPTIONAL)
- **HTTP/HTTPS Directories** (NOAA NCDC GIBBS for preview images: https://www.ncdc.noaa.gov/gibbs/)
- **FTP/FTPS Directories** (NOAA CLASS for high-resolution NetCDF data)
- **Observatory/Mission-specific** (GOES satellite data from NOAA)

### 18. Input File Formats (RECOMMENDED)
- **ascii** (.wld world files for coordinate information)
- **netCDF3/4** (high-resolution GOES satellite data)
- **Other** (JPG images for preview data)

### 19. Output File Formats (RECOMMENDED)
The software downloads and saves files in their native formats but does not explicitly export processed data:
- **Other** (JPG - downloaded preview images saved to disk)
- **netCDF3/4** (downloaded high-resolution data saved to disk)

Note: Visualization outputs are displayed interactively and not automatically saved to files.

### 20. Operating System (RECOMMENDED)
- **Operating System Independent** (from setup.cfg classifier)
- **Linux** (tested in CI workflow)

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent** (Python package with no specific architecture requirements)

### 22. Related Phenomena (OPTIONAL)
Not explicitly specified in repository, but GOES satellites observe:
- Solar flares
- Coronal mass ejections
- X-ray emission
(Note: These are inferred from GOES mission scope but not explicitly stated in the software documentation)

### 23. Development Status (RECOMMENDED)
**Active** - Based on setup.cfg classifier "Development Status :: 4 - Beta". Repository was last updated 2024-06-22 (from SoMEF), indicating continued maintenance.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/GOESplot (documentation is in the README; no separate documentation site found)

### 25. Funder (OPTIONAL)
Not found

### 26. Award Title (OPTIONAL)
Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

### 28. Related Datasets (OPTIONAL)
The software supports access to GOES satellite datasets from NOAA, but specific dataset DOIs were not found in the repository.

### 29. Related Software (OPTIONAL)
Dependencies that this software requires:
- python-dateutil
- numpy
- imageio
- xarray
- requests
- cartopy (optional, for plotting)
- matplotlib (optional, for plotting)
- netCDF4 (optional, for high-resolution data)

### 30. Interoperable Software (OPTIONAL)
Based on dependencies, this software is designed to work with:
- xarray (for data handling)
- cartopy (for geospatial visualization)
- matplotlib (for plotting)

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** GOES-13 Imager
- **Instrument Identifier:** Not found

- **Instrument Name:** GOES-16 Advanced Baseline Imager (ABI)
- **Instrument Identifier:** Not found

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** GOES-13 (Geostationary Operational Environmental Satellite-13)
- **Observatory Name:** GOES-16 (Geostationary Operational Environmental Satellite-16)
- **Observatory Name:** GOES East (mentioned in code)

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/space-physics/GOESplot/main/src/goesplot/tests/goes13-IR-2017-07-13-12.jpg

Note: The PyHC registry lists this with "master" branch, but the repository uses "main" as the default branch.

---

## Metadata Sources Summary

1. **SoMEF Output:** Software name, description, license, programming language, keywords, repository information, creation/update dates
2. **PyHC Unevaluated Registry:** Listed as "GOESutils" with keywords (ionosphere_thermosphere_mesosphere, solar, magnetosphere, specific), logo URL, and contact (Michael Hirsch)
3. **setup.cfg:** Version (1.1.0), author information, dependencies, classifiers (OS independent, Beta status, Python 3.x)
4. **README.md:** Description, usage examples, data source URLs
5. **LICENSE.txt:** Apache License 2.0 confirmation
6. **Source Code Analysis (io.py, plots.py):** Functionality (download, load, plot), file format support (JPG, NetCDF4, ASCII), data sources (NOAA GIBBS, NOAA CLASS via FTP)
7. **Git History:** Publication date (2018-02-22), tagged version v1.0.8 (2018-08-19)
8. **CI Workflow (.github/workflows/ci.yml):** Operating system (Linux)

---

## Notes

- **No DOI found:** This package does not appear to have a persistent identifier (DOI) registered through Zenodo or other services.
- **Version discrepancy:** The setup.cfg lists version 1.1.0, but the only git tag is v1.0.8 from 2018. Version 1.1.0 appears to be untagged.
- **Limited author information:** Only the primary author (Michael Hirsch) is identified. No ORCID or institutional affiliation information was found in the repository.
- **PyHC Status:** Listed in the PyHC unevaluated packages registry, indicating it's recognized by the Python in Heliophysics Community but hasn't undergone full evaluation.
- **Active but minimal maintenance:** Last update was 2024-06-22, showing the package is still maintained, though updates appear infrequent.
