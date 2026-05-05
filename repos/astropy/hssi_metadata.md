# HSSI Metadata Extraction Results

**Repository:** https://github.com/astropy/astropy
**Extraction Date:** 2026-04-27

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.4670728
- Source: Zenodo concept DOI (all versions), confirmed via CITATION.cff identifiers and README Zenodo badge; resolved via DataCite API.

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/astropy/astropy
- Source: pyproject.toml `[project.urls].repository`, README.rst, CITATION.cff `repository-code`.

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms:Planetary
- Coordinate Transforms:Solar
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Models and Simulations
- Models and Simulations:Empirical
- Models and Simulations:Physics-Based
- Models and Simulations:Theory
- Source: `astropy.coordinates` provides built-in HCRS/ICRS/GCRS/ITRS/ecliptic/Galactic/AltAz frames and transforms — Sun-centered ecliptic frames support solar-system positioning, planetary ephemerides via `astropy.coordinates.solar_system`. `astropy.io.fits`, `astropy.io.votable`, `astropy.io.ascii`, `astropy.io.misc` for file format read/write/conversion; `astropy.table`, `astropy.timeseries`, `astropy.stats`, `astropy.nddata`, `astropy.uncertainty`, `astropy.convolution` for data processing; `astropy.visualization` (with `wcsaxes`, stretches, normalizations, RGB image, histogram tools) for plotting; `astropy.modeling` provides analytic and physical model classes plus fitters; `astropy.cosmology` provides empirical and theoretical cosmological models. NOT applicable: Coordinate Transforms:Heliospheric (no HCI/HAE/HEE/Carrington/Stonyhurst/RTN frames — those are in SunPy), Coordinate Transforms:Magnetospheric, Coordinate Transforms:Ionospheric (no GSE/GSM/SM/MAG/AACGM frames).

### 5. Related Region (MANDATORY)
- Solar Environment
- Interplanetary Space
- Source: Solar Environment supportable via `HeliocentricMeanEcliptic`, `HCRS`, and `astropy.coordinates.solar_system` (Sun body positioning), plus the WCSAxes helioprojective axis-display capability (consumed by SunPy and other heliophysics tools). Interplanetary Space supportable via `astropy.coordinates.solar_system` ephemeris (`get_body`, `get_body_barycentric_posvel`) for positions of solar system bodies. Earth Magnetosphere and Planetary Magnetospheres NOT included — astropy has no magnetospheric coordinate frames (no GSE/GSM/SM/MAG/AACGM) and no planet-fixed or magnetospheric science capability. Earth Atmosphere also not included (no atmospheric/ionospheric models). Note for reviewers: astropy is NOT in any PyHC registry — included here as foundational infrastructure for heliophysics tooling rather than as a heliophysics package per se.

### 6. Authors (MANDATORY)
1. **The Astropy Developers** (corporate author) | astropy.team@gmail.com — from pyproject.toml
2. **Astropy Collaboration** (corporate author) — from CITATION.cff top-level `authors`
3. **Adrian M. Price-Whelan** | ORCID: https://orcid.org/0000-0003-0872-7098
4. **Pey Lian Lim** | ORCID: https://orcid.org/0000-0003-0079-4114
5. **Nicholas Earl** | ORCID: https://orcid.org/0000-0003-1714-7415
6. **Nathaniel Starkman** | ORCID: https://orcid.org/0000-0003-3954-3291
7. **Larry Bradley** | ORCID: https://orcid.org/0000-0002-7908-9284
8. **David L. Shupe** | ORCID: https://orcid.org/0000-0003-4401-0430
9. **Aarya A. Patil** | ORCID: https://orcid.org/0000-0002-7626-506X
10. **Lia Corrales** | ORCID: https://orcid.org/0000-0002-5466-3817
11. **C. E. Brasseur** | ORCID: https://orcid.org/0000-0002-9314-960X
12. **Maximilian Nöthe** | ORCID: https://orcid.org/0000-0001-7993-8189
13. **Axel Donath** | ORCID: https://orcid.org/0000-0003-4568-7005
14. **Erik Tollerud** | ORCID: https://orcid.org/0000-0002-9599-310X
15. **Brett M. Morris** | ORCID: https://orcid.org/0000-0003-2528-3409
16. **Adam Ginsburg** | ORCID: https://orcid.org/0000-0001-6431-9633
17. **Eero Vaher**
18. **Benjamin A. Weaver**
19. **James Tocknell** | ORCID: https://orcid.org/0000-0001-6637-6922
20. **William Jamieson** | ORCID: https://orcid.org/0000-0001-5976-4492
21. **Marten H. van Kerkwijk** | ORCID: https://orcid.org/0000-0002-5830-8505
22. **Thomas P. Robitaille** | ORCID: https://orcid.org/0000-0002-8642-1329
- Source: pyproject.toml authors (corporate) and CITATION.cff `preferred-citation.authors` (lead authors with ORCIDs from the v5.0 paper, Astropy Collaboration et al. 2022). CITATION.cff lists ~136 individual co-authors total plus "Astropy Project Contributors"; the first 21 named co-authors are enumerated above. Full contributor base on https://github.com/astropy/astropy/graphs/contributors.

### 7. Software Name (MANDATORY)
- **Name:** astropy
- **Full Name:** Astropy
- Source: pyproject.toml `name`, README.rst, CITATION.cff `title`.

### 8. Description (MANDATORY)
- **Description:** Astropy is a community-developed core Python package for astronomy. It provides a comprehensive, interoperable foundation for astronomical and astrophysical research, including astronomical coordinate systems and transforms, time and date handling, physical units and constants, FITS/VOTable/ASCII/HDF5/Parquet file I/O, world coordinate systems (WCS), tables, NDData, modeling and fitting, statistics, convolution, cosmological calculations, time series, uncertainties, and visualization. Astropy is the canonical core of a large astronomy ecosystem and is widely used as a dependency by mission analysis tools and heliophysics packages such as SunPy.
- Source: README.rst, pyproject.toml description, DataCite metadata.

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Astropy is the community-developed core Python package for astronomy: coordinates, time, units, FITS/HDF5 I/O, WCS, tables, modeling, statistics, cosmology, time series, and visualization.
- Source: Derived from README.rst and pyproject.toml description.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2011-07-21
- Source: GitHub repository creation date (`2011-07-21T01:33:49Z` via GitHub API). This is the first public broadcast of the astropy codebase. Chosen over the 2013 A&A paper publication (which is now Reference Publication, Field 14) and the v7.2.0 release date (which belongs in Version, Field 12), per the form spec definition "Date of first broadcast/publication; used for the initial version of the software." Matches the sunpy convention used elsewhere in this project.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- Source: DataCite API (publisher of concept DOI 10.5281/zenodo.4670728).

### 12. Version (RECOMMENDED)
- **Version Number:** v7.2.0
- **Version Date:** 2025-11-28
- **Version Description:** Adds CODATA 2022 support in `astropy.constants`; allows `np.concatenate`, `np.stack` and similar numpy functions on representations, differentials, frames, and `SkyCoord`; introduces named attributes on `match_coordinates_*` and `search_around_*` results; adds new `astropy.cosmology.traits` (CurvatureComponent, HubbleParameter, DarkEnergyComponent, DarkMatterComponent, MatterComponent, BaryonComponent); cosmology methods now exclusively return arrays.
- **Version PID:** https://doi.org/10.5281/zenodo.17756022
- Source: Zenodo/DataCite metadata for concept DOI 10.5281/zenodo.4670728; version-specific DOI resolved via DataCite `HasVersion` relations; version description summarized from CHANGES.rst (which dates v7.2.0 as 2025-11-25 vs Zenodo's issued date 2025-11-28). Note: no git tags in local shallow clone; CITATION.cff lacks top-level `version` and `date-released`, both sourced from Zenodo metadata.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- C
- Other
- Source: pyproject.toml classifiers and `requires-python` (Python >=3.11); C extensions present in `cextern/` and `astropy/wcs/`. "Other" covers Cython, used throughout for performance-critical extension modules.

### 14. Reference Publication (RECOMMENDED)
- **DOI:** https://doi.org/10.3847/1538-4357/ac7c74
- Title: "The Astropy Project: Sustaining and Growing a Community-oriented Open-source Project and the Latest Major Release (v5.0) of the Core Package" (Astropy Collaboration et al. 2022, ApJ 935, 167)
- Source: astropy/CITATION (latest reference paper).

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause
- Source: pyproject.toml `license` (BSD-3-Clause), CITATION.cff `license`, LICENSE.rst, README.rst.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- astronomy
- astrophysics
- cosmology
- space
- science
- units
- table
- wcs
- samp
- coordinate
- fits
- modeling
- models
- fitting
- ascii
- Source: pyproject.toml `keywords`.

### 17. Data Sources (OPTIONAL)
Not found
- Source: Astropy is observatory-agnostic and does not include specific data-source modules. IERS data and ephemerides are loaded internally via `astropy-iers-data` and `jplephem`; remote data services for astronomical archives are provided by the separate `astroquery` package.

### 18. Input File Formats (RECOMMENDED)
- FITS
- ascii
- csv
- HDF5
- JSON
- Other
- Source: `astropy.io` modules — FITS (`astropy.io.fits`), ASCII tables in many flavors including CSV/IPAC/CDS/MRT/AASTeX/fixed-width/RST/HTML (`astropy.io.ascii`), HDF5 (`astropy.io.misc.hdf5`), JSON. "Other" covers VOTable (`astropy.io.votable`), Parquet (`astropy.io.misc.parquet`), ASDF (via `asdf-astropy`), ECSV, YAML, IERS Bulletin A/B tables, and JPL DE-series ephemerides.

### 19. Output File Formats (RECOMMENDED)
- FITS
- ascii
- csv
- HDF5
- JSON
- Other
- Source: Astropy writes the same formats it reads. "Other" covers VOTable, Parquet, ASDF, ECSV, YAML, plus matplotlib figures, PNG bitmaps via `fits2bitmap`, and SAMP messages via `astropy.samp`.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows
- Source: pyproject.toml classifier "Operating System :: OS Independent"; cibuildwheel configured for macOS x86_64+arm64 and Linux auto+aarch64; CI exercises all three platforms.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64
- Linux aarch64 or arm64
- Source: cibuildwheel configuration in pyproject.toml (macOS x86_64+arm64, Linux auto+aarch64).

### 22. Related Phenomena (OPTIONAL)
Not found
- Source: Astropy is a general-purpose astronomy library and does not target specific heliophysics phenomena.

### 23. Development Status (RECOMMENDED)
- **Status:** Active
- Source: Continuous releases (v7.2.0 issued 2025-11-28); active CI; pyOpenSci peer-reviewed (https://github.com/pyOpenSci/software-review/issues/251); >100 contributors; regular release cadence.

### 24. Documentation (RECOMMENDED)
- **URL:** https://docs.astropy.org
- Source: pyproject.toml `[project.urls].documentation`, README.rst.

### 25. Funder (OPTIONAL)
- **Organization:** NumFOCUS
- **Funder Identifier:** https://ror.org/004eyxv41
- Source: README.rst notes Astropy is sponsored by NumFOCUS, a 501(c)(3) nonprofit. The Astropy 2022 paper acknowledges support from the Heising-Simons Foundation, NSF, NASA, and STScI; no machine-readable funder/award identifiers are exposed in CITATION.cff or DataCite metadata.

### 26. Award Title (OPTIONAL)
Not found
- Source: No machine-readable award/grant identifiers in CITATION.cff or DataCite metadata.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.3847/1538-3881/aabc4f — "The Astropy Project: Building an Open-science Project and Status of the v2.0 Core Package" (Astropy Collaboration et al. 2018, AJ 156, 123)
- https://doi.org/10.1051/0004-6361/201322068 — "Astropy: A community Python package for astronomy" (Astropy Collaboration et al. 2013, A&A 558, A33)
- Source: astropy/CITATION. The v5.0 paper (2022) is promoted to Reference Publication (Field 14); the v2.0 (2018) and original community papers (2013) are retained here.

### 28. Related Datasets (OPTIONAL)
Not found
- Source: Astropy is a library, not a dataset. It bundles small reference data (constants, IERS via `astropy-iers-data`, observatory sites database) but does not publish or curate scientific datasets.

### 29. Related Software (OPTIONAL)
- https://github.com/liberfa/erfa — ERFA / pyerfa (Essential Routines for Fundamental Astronomy; required runtime dependency)
- https://github.com/astropy/astropy-iers-data — Earth orientation reference data (required runtime dependency)
- https://github.com/astropy/asdf-astropy — ASDF format support
- https://github.com/sunpy/sunpy — SunPy (heliophysics package built on astropy)
- https://github.com/astropy/astroquery — astroquery (remote data access; Astropy coordinated package)
- https://github.com/astropy/photutils — photutils (Astropy coordinated package)
- https://github.com/astropy/specutils — specutils (Astropy coordinated package)
- https://github.com/astropy/regions — regions (Astropy coordinated package)
- https://github.com/astropy/reproject — reproject (Astropy coordinated package)
- https://ascl.net/1304.002 — ASCL listing (`ascl:1304.002`)
- Source: pyproject.toml dependencies, Astropy coordinated packages list, ASCL.

### 30. Interoperable Software (OPTIONAL)
- https://numpy.org — NumPy (required dependency; >=2.0)
- https://scipy.org — SciPy (recommended; >=1.13)
- https://matplotlib.org — Matplotlib (recommended; >=3.8.4)
- https://github.com/sunpy/sunpy — SunPy (heliophysics interoperability)
- https://github.com/spacetelescope/gwcs — gwcs (Astropy coordinated package)
- Source: pyproject.toml dependencies and Astropy ecosystem interoperability.

### 31. Related Instruments (OPTIONAL)
Not found
- Source: Astropy does not target specific instruments.

### 32. Related Observatories (OPTIONAL)
Not found
- Source: Astropy is observatory-agnostic. `astropy.coordinates.EarthLocation.of_site()` supports many ground-based observatories generically, but no specific heliophysics observatory affiliation is claimed.

### 33. Logo (OPTIONAL)
- **URL:** https://github.com/astropy/repo_stats/blob/main/dashboard_template/astropy_banner_gray.svg
- Source: README.rst Astropy Logo image link.
