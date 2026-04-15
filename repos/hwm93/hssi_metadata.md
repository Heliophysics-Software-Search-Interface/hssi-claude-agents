# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/hwm93
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** Not found

**Note:** No DOI found in repository files, README, or metadata files.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/space-physics/hwm93

**Source:** Repository URL

### 4. Software Functionality (MANDATORY)
**Values:**
- Models and Simulations
- Models and Simulations:Empirical
- Models and Simulations:Physics-Based
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Processing and Analysis

**Note:** HWM93 is an empirical, physics-based horizontal wind model for Earth's atmosphere. It computes meridional and zonal wind components at specified altitudes, locations, and times. The software includes visualization capabilities to plot wind profiles as line plots.

**Source:** Manual code examination, README, and SoMEF

### 5. Related Region (MANDATORY)
**Value:** Earth Atmosphere

**Note:** The model specifically covers the mesosphere, thermosphere, and ionosphere regions of Earth's atmosphere, with altitude coverage from approximately 0 km to 1000+ km.

**Source:** PyHC keywords (ionosphere_thermosphere_mesosphere), setup.cfg keywords, and model documentation in Fortran source code

### 6. Authors (MANDATORY)

**Author 1:**
- **Author Name:** Michael Hirsch, Ph.D.
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Note:** Michael Hirsch is the primary developer of this Python/Matlab implementation. The original Fortran 77 code was developed by A. E. Hedin (NASA) in 1993.

**Source:** setup.cfg, RunHWM93.py, Fortran source code header

### 7. Software Name (MANDATORY)
**Value:** HWM93

**Alternate name:** hwm93 (package name)

**Source:** PyHC registry, SoMEF, setup.cfg

### 8. Description (MANDATORY)
**Value:** NASA Horizontal Wind Model HWM93 in Python and Matlab. HWM93 is an empirical model that provides horizontal wind velocities (meridional and zonal components) for Earth's atmosphere from ground level to the exosphere. The model uses inputs including date, time, altitude, geographic location, solar activity indices (F10.7 flux), and geomagnetic activity indices (AP) to compute wind vectors. This Python implementation wraps the original Fortran 77 code by A. E. Hedin using f2py, making it accessible from Python and Matlab. The software supports multiple Fortran compilers (Gfortran, Intel ifort, PGI pgf90, Nvidia flang) and can output results to NetCDF/HDF5 format for further analysis.

**Source:** PyHC registry, SoMEF, README, setup.cfg

### 9. Concise Description (OPTIONAL)
**Value:** Python and Matlab interface to NASA's HWM93 empirical atmospheric horizontal wind model, computing meridional and zonal wind components for altitudes from 0 to 1000+ km.

**Source:** Derived from full description

### 10. Publication Date (RECOMMENDED)
**Value:** 2015-03-29

**Note:** Date of first commit to the repository

**Source:** SoMEF (date_created), git log

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Note:** No DOI/Zenodo publication found, so GitHub is the publisher

**Source:** Repository hosting platform

### 12. Version (RECOMMENDED)

#### Latest Version:
- **Version Number:** v0.9.1
- **Version Date:** 2018-08-16
- **Version Description:** Add Matlab HWM93 demo
- **Version PID:** Not found

**Note:** Latest release was v0.9.1 in 2018. Other versions include v0.9.0, v0.8.1, and v0.8.0.

**Source:** SoMEF (releases), setup.cfg, git tags

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x
- Fortran77
- MATLAB

**Note:** Python 3.6+ required. Uses Fortran 77 for computational core, wrapped with f2py. Also includes Matlab interface.

**Source:** setup.cfg, SoMEF, README

### 14. Reference Publication (RECOMMENDED)
**Value:** Hedin, A. E., et al. (1996), "Empirical wind model for the upper, middle and lower atmosphere," J. Atmos. Terr. Phys., 58, 1421–1447

**Note:** This publication describes the HWM93 model developed by A. E. Hedin and colleagues. The model is based on wind data from AE-E and DE 2 satellites. Earlier foundational work includes Hedin et al. (1991) in J. Geophys. Res., 96, 7657-7688, and Hedin et al. (1988) in J. Geophys. Res., 93, 9959–9978. The original Fortran 77 code is available from: ftp://hanna.ccmc.gsfc.nasa.gov/pub/modelweb/atmospheric/hwm93/

**Source:** Web search for "HWM93 A. E. Hedin", README, RunHWM93.py, Fortran source header

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT

**Source:** SoMEF, LICENSE.txt, setup.cfg

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- f2py
- fortran
- geoscience
- hwm93
- ionosphere
- matlab
- matlab-python-interface
- mesosphere
- python
- thermosphere
- stratosphere
- atmospheric science
- horizontal wind model
- empirical model

**Source:** SoMEF (GitHub topics), setup.cfg keywords, PyHC keywords

### 17. Data Sources (OPTIONAL)
**Value:** Not applicable

**Note:** HWM93 is a model that computes winds based on empirical formulas and input parameters (time, location, solar/geomagnetic indices). It does not read from external data sources.

**Source:** Code examination

### 18. Input File Formats (RECOMMENDED)
**Value:** Not applicable

**Note:** The model does not read input files. It accepts parameters directly via function calls or command-line arguments.

**Source:** Code examination

### 19. Output File Formats (RECOMMENDED)
**Values:**
- netCDF3/4
- HDF5

**Note:** The software can output results to NetCDF (which uses HDF5 format) using xarray's to_netcdf() method.

**Source:** RunHWM93.py, README

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

**Note:** Tested on all three platforms via CI/CD (GitHub Actions)

**Source:** .github/workflows/ci.yml

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Note:** Works on standard CPU architectures. Requires a Fortran compiler (gfortran, ifort, pgf90, or flang).

**Source:** README, CI configuration

### 22. Related Phenomena (OPTIONAL)
**Values:** Not found

**Note:** The model computes horizontal winds but is not specifically tied to particular phenomena like CMEs or flares. It models the general state of atmospheric winds.

**Source:** Model description

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Note:** The repository shows recent activity (last updated 2025-05-21 according to SoMEF). The setup.cfg indicates "Development Status :: 4 - Beta".

**Source:** SoMEF (date_updated), setup.cfg classifiers

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/space-physics/hwm93/wiki

**Note:** Documentation is available on the GitHub wiki. Installation and usage instructions are also in the README.

**Source:** SoMEF, PyHC registry

### 25. Funder (OPTIONAL)
**Value:** Not found

**Note:** No funding information found in repository files

**Source:** Repository examination

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Note:** No award or grant information found in repository files

**Source:** Repository examination

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found

**Note:** No publications citing or using this specific Python implementation were found in the repository

**Source:** Repository examination

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Note:** The model uses solar and geomagnetic indices (F10.7, AP) as inputs, but no specific datasets are referenced

**Source:** Code examination

### 29. Related Software (OPTIONAL)
**Values:**
- numpy (dependency)
- xarray (dependency)
- python-dateutil (dependency)
- sciencedates (dependency)

**Note:** The package depends on several Python scientific computing libraries. Other related atmospheric models may include MSIS, IRI, and IGRF, though these are not explicitly mentioned in the repository.

**Source:** setup.cfg, pyproject.toml

### 30. Interoperable Software (OPTIONAL)
**Values:**
- numpy
- xarray
- matplotlib

**Note:** The software integrates with standard scientific Python libraries and can be used alongside other packages in the Python scientific ecosystem.

**Source:** Code examination, setup.cfg

### 31. Related Instruments (OPTIONAL)
**Value:** Not applicable

**Note:** HWM93 is a model, not instrument-specific software. However, it can be used to interpret data from atmospheric and ionospheric instruments.

**Source:** Model description

### 32. Related Observatories (OPTIONAL)
**Value:** Not found

**Note:** No specific observatories or missions are mentioned in the repository, though the model is relevant to atmospheric and ionospheric research missions.

**Source:** Repository examination

### 33. Logo (OPTIONAL)
**Value:** https://ccmc.gsfc.nasa.gov/images/CCMC-LOGO-2.gif

**Note:** PyHC registry lists the NASA CCMC logo as the package logo

**Source:** PyHC unevaluated registry

---

## Additional Notes

### Original Model Information
- **Original Developer:** A. E. Hedin (NASA)
- **Original Code:** Fortran 77
- **Original Code Location:** ftp://hanna.ccmc.gsfc.nasa.gov/pub/modelweb/atmospheric/hwm93/
- **Model Year:** 1993

### Python Implementation
- **Developer:** Michael Hirsch, Ph.D.
- **Contact:** scivision@users.noreply.github.com
- **GitHub Organization:** space-physics
- **PyHC Status:** Unevaluated package

### Technical Details
- **Fortran Compilers Supported:** Gfortran >= 5, Intel ifort, PGI pgf90, Nvidia flang
- **Python Version:** >= 3.6
- **Build Systems:** setup.py, pyproject.toml, Meson, CMake
- **Wrapper Technology:** f2py (part of numpy)
- **Output Data Structure:** xarray.Dataset with coordinates and attributes

### Model Inputs
- Year and day (YYDDD format)
- Universal time (seconds)
- Altitude (km)
- Geodetic latitude (degrees)
- Geodetic longitude (degrees)
- Local apparent solar time (hours)
- F10.7 flux (3-month average and daily)
- Magnetic activity index (AP)

### Model Outputs
- Meridional wind component (m/s, positive northward)
- Zonal wind component (m/s, positive eastward)

### Altitude Range
The model is valid from ground level to the exobase (approximately 0-1000+ km), covering:
- Troposphere and stratosphere
- Mesosphere (50-85 km)
- Thermosphere (85-600 km)
- Ionosphere (overlaps with thermosphere)

---

## Metadata Extraction Summary

**Total Fields:** 33
**Fields with Values:** 24
**Fields Not Found:** 9
**MANDATORY Fields Completed:** 6/6
**RECOMMENDED Fields Completed:** 12/16

### Fields Not Found
1. Persistent Identifier (DOI)
2. Author ORCID
3. Author Affiliation
4. Funder
5. Award Title
6. Related Publications
7. Related Datasets
8. Related Instruments
9. Related Observatories

### Data Sources Used
1. ✓ PyHC Unevaluated Registry
2. ✓ SoMEF (Software Metadata Extraction Framework)
3. ✓ Manual repository examination (README, LICENSE, setup files, source code)
4. ✗ DataCite API (no DOI found)
5. ✗ Zenodo API (no DOI found)
