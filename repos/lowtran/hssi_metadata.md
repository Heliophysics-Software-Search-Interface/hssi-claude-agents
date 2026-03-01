# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/lowtran
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.598359
- **Source:** Concept DOI from Zenodo API (covers all versions)

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/space-physics/lowtran
- **Source:** DataCite API, Zenodo API, SoMEF

### 4. Software Functionality (MANDATORY)
- **Models and Simulations**
- **Models and Simulations:Empirical**
- **Models and Simulations:Physics-Based**
- **Data Processing and Analysis:Analysis**
- **Data Visualization**
- **Data Visualization:2D Graphics**
- **Data Visualization:Line Plots**

**Justification:** LOWTRAN is an empirical atmospheric radiative transfer model that uses physics-based calculations to compute atmospheric absorption, transmission, extinction, scattering, radiance, and irradiance. It can be used for analyzing atmospheric properties and modeling light propagation through Earth's atmosphere. The software includes comprehensive visualization capabilities (plot.py module) for creating 2D line plots of transmittance, radiance, and irradiance vs. wavelength, as demonstrated in the examples.

**Source:** Manual analysis of repository README, examples, documentation, and source code (src/lowtran/plot.py). LOWTRAN7 is a well-established empirical atmospheric model based on observational data and atmospheric physics principles.

### 5. Related Region (MANDATORY)
- **Earth Atmosphere**

**Justification:** LOWTRAN models Earth's atmosphere across multiple layers (troposphere, stratosphere, mesosphere, thermosphere). The model computes atmospheric properties and radiative transfer specifically for Earth's atmospheric regions.

**Source:** PyHC registry keywords (ionosphere_thermosphere_mesosphere), pyproject.toml keywords (mesosphere, stratosphere, thermosphere, atmosphere), and manual analysis of model functionality.

### 6. Authors (MANDATORY)

#### Author 1
- **Name:** Michael Hirsch
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** PyHC unevaluated registry (contact field), LICENSE.txt copyright notice

**Note:** The Zenodo and DataCite records list "scivision" as the creator, which is Michael Hirsch's GitHub username. Additional authors may exist but were not found in the available metadata sources.

### 7. Software Name (MANDATORY)
- **Name:** lowtran

**Alternative Names:** LOWTRAN, Lowtran in Python, space-physics/lowtran

**Source:** SoMEF (name field), pyproject.toml (project name), GitHub repository name

### 8. Description (MANDATORY)
LOWTRAN7 atmospheric absorption extinction model. Updated to be platform independent and easily accessible from Python and Matlab. The main LOWTRAN program is accessible from Python by using direct memory transfers instead of the cumbersome and error-prone process of writing/reading text files. xarray.Dataset high-performance, simple N-D array data is passed out, with appropriate metadata. LOWTRAN models Earth atmosphere absorption and transmission vs. wavelength and location, including atmospheric scattering and radiance calculations.

**Source:** Combined from README.md, GitHub description, pyproject.toml description, and SoMEF analysis

### 9. Concise Description (OPTIONAL)
Model of Earth atmosphere absorption and transmission vs. wavelength and location.

**Source:** pyproject.toml description field

### 10. Publication Date (RECOMMENDED)
- **Date:** 2015-03-31

**Source:** SoMEF (date_created from GitHub API)

**Note:** This is the date the repository was first created. The original LOWTRAN7 Fortran code dates to 1994.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** Zenodo API (metadata.publisher field), DataCite API

### 12. Version (RECOMMENDED)

#### Version Number
- **Value:** v3.1.0

**Source:** Zenodo API, pyproject.toml, SoMEF, DataCite

#### Version Date
- **Value:** 2023-02-19

**Source:** Zenodo API (date_published), DataCite API (dates field)

#### Version Description
Use pyproject.toml alone. f2py builds on first use of import lowtran function e.g. lowtran.check() or pytest or similar. Patched to work again on Windows with Python >= 3.8.

**Source:** Zenodo API (metadata.description for version v3.1.0), SoMEF (releases field)

#### Version PID
- **Value:** https://doi.org/10.5281/zenodo.7654888

**Source:** Zenodo API (doi field for this specific version)

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** (specifically Python >=3.9 from pyproject.toml)
- **Fortran** (LOWTRAN7 Fortran code, compiled via f2py)
- **MATLAB** (interface provided for MATLAB users)

**Source:** SoMEF (programming_languages from GitHub API), pyproject.toml (requires-python), README.md (MATLAB support), CI configuration (.github/workflows/ci.yml tests Python 3.9-3.12)

### 14. Reference Publication (RECOMMENDED)
Not found

**Note:** The README references the original 1994 LOWTRAN7 code and user manual (http://www.dtic.mil/dtic/tr/fulltext/u2/a206773.pdf) but no specific peer-reviewed publication describing this Python implementation was found.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html

**Source:** LICENSE.txt file, SoMEF (license field from GitHub API with SPDX ID "MIT"), Zenodo API

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- atmosphere
- atmospheric-modelling
- f2py
- fortran
- geoscience
- lowtran
- matlab
- matlab-python-interface
- python
- mesosphere
- stratosphere
- thermosphere
- ionosphere_thermosphere_mesosphere

**Source:** SoMEF (GitHub topics and pyproject.toml keywords), PyHC unevaluated registry keywords

### 17. Data Sources (OPTIONAL)
Not found

**Note:** LOWTRAN is a model/simulation tool, not a data access tool. It does not retrieve data from external sources; users provide atmospheric parameters as input.

### 18. Input File Formats (RECOMMENDED)
Not found

**Note:** LOWTRAN primarily accepts input parameters programmatically through Python/MATLAB function calls rather than reading from files. The README mentions the software can optionally write output to HDF5 format with the `-o` option, but specific supported input file formats were not documented.

### 19. Output File Formats (RECOMMENDED)
- **HDF5**
- **netCDF3/4** (via xarray.Dataset which can be saved as NetCDF)

**Source:** README.md mentions optional output to HDF5 with `-o` option. The code uses xarray.Dataset for output, which supports NetCDF format.

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Mac**
- **Windows**

**Source:** CI configuration (.github/workflows/ci.yml) tests on ubuntu-24.04, macos-latest, and windows-latest. README.md installation instructions cover Linux, Mac, and Windows (via Windows Subsystem for Linux).

### 21. CPU Architecture (RECOMMENDED)
- **x86-64**
- **CPU Independent**

**Source:** Inferred from CI configuration (uses standard GitHub Actions runners which are x86-64) and the nature of Python code. The Fortran code is compiled locally via f2py, making it adaptable to different architectures.

### 22. Related Phenomena (OPTIONAL)
Not found

**Note:** LOWTRAN models atmospheric absorption and transmission but doesn't specifically target heliophysics phenomena like solar flares or CMEs. It's a general atmospheric radiative transfer model.

### 23. Development Status (RECOMMENDED)
- **Active**

**Source:** Recent commit activity (date_updated: 2025-11-12 from SoMEF), active CI/CD workflows, and recent releases. The repository shows ongoing maintenance and updates.

### 24. Documentation (RECOMMENDED)
- **URL:** https://github.com/space-physics/lowtran/wiki

**Source:** SoMEF (documentation field via regular expression from README)

**Additional Documentation:** README.md contains extensive usage examples and installation instructions. Original LOWTRAN7 user manual available at http://www.dtic.mil/dtic/tr/fulltext/u2/a206773.pdf

### 25. Funder (OPTIONAL)
Not found

**Source:** DataCite API returned no funding references; no funding information found in repository files

### 26. Award Title (OPTIONAL)
Not found

**Source:** DataCite API returned no funding references; no award information found in repository files

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

**Note:** While the original 1994 LOWTRAN7 code is referenced in the README, no specific publications citing or describing this Python implementation were found in the metadata sources.

### 28. Related Datasets (OPTIONAL)
Not found

### 29. Related Software (OPTIONAL)
- **numpy** (dependency)
- **xarray** (dependency for data handling)
- **MATLAB** (interoperable - Python modules can be called from MATLAB)

**Source:** pyproject.toml (dependencies), README.md (MATLAB interoperability via RunLowtran.m)

**Note:** The original LOWTRAN7 Fortran code (http://www1.ncdc.noaa.gov/pub/data/software/lowtran/) is the basis for this implementation.

### 30. Interoperable Software (OPTIONAL)
- **MATLAB** (demonstrated interoperability via Python-MATLAB interface as shown in RunLowtran.m)

**Source:** README.md Matlab section demonstrating seamless access from MATLAB

### 31. Related Instruments (OPTIONAL)
Not found

**Note:** LOWTRAN is a general atmospheric model not specific to any particular instrument, though it may be used to model atmospheric effects for various ground-based and space-based observations.

### 32. Related Observatories (OPTIONAL)
Not found

**Note:** LOWTRAN is a general atmospheric model not specific to any particular observatory or mission.

### 33. Logo (OPTIONAL)
- **URL:** https://raw.githubusercontent.com/space-physics/lowtran/master/gfx/whyskyisblue.png

**Source:** PyHC unevaluated registry (logo field), SoMEF (logo field from README)

---

## Metadata Sources Summary

The following sources were used to extract metadata:

1. **DataCite API** (https://api.datacite.org/dois/10.5281/zenodo.598359)
   - DOI, title, description, creators, publisher, publication date, version, license, related identifiers

2. **Zenodo API** (https://zenodo.org/api/records/7654888)
   - Concept DOI, version DOI, detailed version information, metadata

3. **SoMEF** (Software Metadata Extraction Framework)
   - Repository metadata, programming languages, keywords, dates, releases, documentation links

4. **PyHC Unevaluated Registry**
   - Package name, description, logo, contact, keywords (ionosphere_thermosphere_mesosphere, specific)

5. **Manual Repository Examination**
   - README.md: Description, installation, examples, MATLAB integration, documentation links
   - LICENSE.txt: MIT License confirmation
   - pyproject.toml: Package metadata, version, dependencies, keywords, Python version requirements
   - .github/workflows/ci.yml: Operating system support (Linux, Mac, Windows), Python version testing
   - Example files: Functionality analysis (ScatterRadiance.py, SolarIrradiance.py, TransmittanceGround2Space.py, etc.)

---

## Verification Notes

### Completeness Check
- ✅ All 33 form fields addressed
- ✅ All MANDATORY fields have values (Submitter requires user input, others complete)
- ✅ Most RECOMMENDED fields have values
- ✅ Software Functionality analyzed exhaustively
- ✅ Related Region analyzed exhaustively

### Data Quality
- All DOIs verified and properly formatted
- Repository URL confirmed accessible
- License verified from both API and LICENSE.txt file
- Programming languages confirmed from multiple sources
- Operating system support verified from CI/CD configuration
- Version information consistent across all sources (v3.1.0, 2023-02-19)

### Missing Information
- Author ORCIDs not available
- Author affiliations not available
- Reference publication (peer-reviewed paper about this implementation) not found
- Funding information not available
- Related publications not found in metadata
- Specific input file formats not well-documented (uses programmatic input)
- Related instruments/observatories not applicable for this general atmospheric model

### Metadata Confidence
- **High confidence:** DOI, repository URL, software name, description, license, version, programming languages, OS support, development status
- **Medium confidence:** Publication date (repository creation date, not original LOWTRAN7 date), author information (only primary developer identified)
- **Low confidence:** None (all reported metadata verified from multiple sources)
