# HSSI Metadata Extraction Results

**HSSI Software ID:** 3fddfda7-5eca-4501-839e-765eb49a8c1b
**Repository:** https://github.com/aringlis/afino_release_version
**Source Revision:** 6aceac9518fc8056052807e666da9d0c8bebb010
**Extraction Date:** 2026-07-23
**Validation Date:** 2026-07-23
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]
- **Source note:** Submitter information is not present in the current HSSI record or repository.

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.12611254

- **Source note:** DataCite and Zenodo identify this as the AFINO concept DOI; Zenodo record 12611255 links it to the version-specific DOI.

### 3. Code Repository (MANDATORY)
https://github.com/aringlis/afino_release_version

- **Source note:** Retained from the existing HSSI record and confirmed by the Git remote, GitHub API, PyHC registry, and SoMEF.

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Models and Simulations
- Models and Simulations:Data Guided
- Models and Simulations:Empirical
- Models and Simulations:Forward-Fitting

- **Source note:** Set-union retains the submitted parent category. Repository code applies Hanning-window preprocessing, computes Fourier power spectra, fits empirical power-law, broken-power-law, and Gaussian-bump models with SciPy optimization, compares likelihood, BIC, and goodness of fit, and creates static time-series and power-spectrum line plots. Parent categories are included for every selected subcategory. Data Guided is included because AFINO fits empirical spectral models to caller-provided observational time series. A Fourier power spectrum is not a time-frequency spectrogram, so Spectrogram was not selected.

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Solar Environment

- **Source note:** The set-union retains Solar Environment from the existing HSSI record and adds Earth Magnetosphere based on peer-reviewed AFINO applications to inner-magnetospheric ultralow-frequency waves. The documentation says AFINO was originally developed to study solar flare oscillations, although the implementation now accepts generic time series.

### 6. Authors (MANDATORY)
- **Author:** Andrew Inglis
  - **Author Identifier:** https://orcid.org/0000-0003-0656-2437
  - **Affiliation 1:**
    - **Organization:** Catholic University of America
    - **Affiliation Identifier:** https://ror.org/047yk3s18
  - **Affiliation 2:**
    - **Organization:** Goddard Space Flight Center
    - **Affiliation Identifier:** https://ror.org/0171mag52

- **Source note:** The current HSSI record stores the repository-owner handle `aringlis`. Repository `setup.py`, Sphinx metadata, Git history, and the curated PyHC entry identify this person as Andrew Inglis. The 2020 AFINO publication supplies the middle initial and ORCID and lists Goddard Space Flight Center; the repository contact address also uses the nasa.gov domain. The handle and full name were identity-resolved rather than emitted as duplicate authors.

### 7. Software Name (MANDATORY)
AFINO (Automated Flare Inference of Oscillations)

- **Source note:** Retained exactly from the existing HSSI record and confirmed by the repository README and SoMEF.

### 8. Description (MANDATORY)
AFINO (Automated Flare Inference of Oscillations) is an automatable timeseries analysis code designed to identify oscillatory signatures. AFINO uses a Fourier-based model comparison approach.
This code repository is a work in progress, and the functionality is provided as-is without guarantees.

- **Source note:** Retained exactly from the existing HSSI record. The same wording appears in the repository README and SoMEF extraction.

### 9. Concise Description (OPTIONAL)
A tool for finding oscillations in time series data.

- **Source note:** From the manually curated PyHC unevaluated-package registry entry for AFINO.

### 10. Publication Date (RECOMMENDED)
2020-01-21

- **Source note:** Retained from the existing HSSI record; it matches the GitHub repository creation date and first commit date.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

- **Source note:** DataCite and Zenodo identify Zenodo as the publisher for both the concept and version DOI records.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.0
- **Version Date:** 2024-07-01
- **Version Description:** Not found
- **Version PID:** https://doi.org/10.5281/zenodo.12611255

- **Source note:** GitHub release Version 1.0 was published on 2024-07-01, and tag v1.0 points to the extracted source revision. The older 0.5 value in setup.py and Sphinx configuration is retained here as a documented stale/conflicting candidate, not the selected current version. The release has no notes. DataCite and Zenodo identify https://doi.org/10.5281/zenodo.12611255 as the DOI for v1.0.

### 13. Programming Language (RECOMMENDED)
- Python 3.x

- **Source note:** Retained from the existing HSSI record. GitHub and SoMEF identify Python, and CI tests Python 3.6, 3.7, 3.8, 3.9, and 3.11.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.3847/1538-4357/833/2/284

- **Source note:** Inglis et al. (2016), A Large-scale Search for Evidence of Quasi-periodic Pulsations in Solar Flares. The later 2020 AFINO paper explicitly identifies the method as coming from Inglis et al. (2016) and says the technique is described there in detail. This association comes from the primary scientific literature rather than repository citation metadata.

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://spdx.org/licenses/BSD-2-Clause.html

- **Source note:** License name retained from the existing HSSI record and confirmed by the authoritative repository LICENSE, GitHub SPDX metadata, PyHC, and SoMEF. Zenodo/DataCite rights metadata conflicts by declaring CC-BY-4.0, but no repository evidence shows that the source code was relicensed.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- data analysis
- Fourier analysis
- oscillations
- power spectral density
- quasi-periodic pulsations
- Bayesian Information Criterion
- time series analysis
- ultralow-frequency waves

- **Source note:** data analysis is normalized from the curated PyHC keyword data_analysis; the implementation and documentation support time series analysis, and peer-reviewed magnetospheric applications support ultralow-frequency waves. The remaining terms describe concepts explicitly implemented or documented in the README, user guide, and analysis modules.

### 17. Data Sources (OPTIONAL)
Not found.

- **Source note:** AFINO accepts caller-supplied time and flux arrays and contains no remote archive or data retrieval client.

### 18. Input File Formats (RECOMMENDED)
- JSON
- FITS

- **Source note:** `restore_json_save_file` reads AFINO JSON result files. The included `afino_test_script.py` opens a FITS flare time-series file with Astropy and passes its time and flux columns to AFINO. FITS support is example-level rather than a file-path argument in the main API and should be confirmed during validation.

### 19. Output File Formats (RECOMMENDED)
- JSON
- Other

- **Source note:** The user guide and code save analysis results as JSON or Python Pickle and summary plots as PDF. `Other` represents Pickle and PDF, which are not separate controlled values.

### 20. Operating System (RECOMMENDED)
- Linux

- **Source note:** GitHub Actions tests the package on `ubuntu-latest`. No repository evidence confirms complete package testing on Mac or Windows; the Windows batch file only builds documentation.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

- **Source note:** The Python implementation contains no architecture-specific code or accelerator requirement. This is an evidence-based inference from the source and dependencies and should be confirmed during validation.

### 22. Related Phenomena (OPTIONAL)
- Solar Flares

- **Source note:** The software name and documentation state that AFINO was originally developed to study oscillations in solar flares.

### 23. Development Status (RECOMMENDED)
WIP

- **Source note:** Retained as WIP because the README explicitly calls the repository a work in progress and provides functionality as-is. A v1.0 release was published in 2024, but inactivity is not inferred over the repository explicit status statement.

### 24. Documentation (RECOMMENDED)
https://afino-release-version.readthedocs.io/

- **Source note:** From the curated PyHC registry and confirmed by the README and SoMEF. The README links the equivalent `/en/latest/` path.

### 25. Funder (OPTIONAL)
Not found.

- **Source note:** No software funding statement was found in the repository metadata or source.

### 26. Award Title (OPTIONAL)
Not found.

- **Source note:** No grant title or award number was found in the repository metadata or source.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1088/0004-637x/798/2/108
- https://doi.org/10.3847/1538-4357/ab8d40
- https://doi.org/10.1088/0004-637x/789/2/152
- https://doi.org/10.3847/1538-4365/ab40b3
- https://doi.org/10.1029/2017JA024877
- https://doi.org/10.1029/2020JA027887

- **Source note:** The first publication is identified by the 2020 AFINO paper as a detailed description of the technique. The second explicitly names and summarizes AFINO. The source code directly cites Nita et al. (2014), the third DOI, for the FFT-spectrum goodness-of-fit equations implemented in afino_model_fitting.py. Broomhall et al. (2019) provides a detailed performance discussion, and the two JGR Space Physics papers explicitly apply AFINO to inner-magnetospheric ultralow-frequency-wave observations.

### 28. Related Datasets (OPTIONAL)
Not found.

- **Source note:** The main API is data-agnostic, and the repository does not identify a supported dataset with a persistent citation.

### 29. Related Software (OPTIONAL)
- https://github.com/numpy/numpy
- https://github.com/scipy/scipy
- https://github.com/matplotlib/matplotlib
- https://github.com/astropy/astropy
- https://github.com/mwaskom/seaborn

- **Source note:** NumPy, SciPy, Matplotlib, and Astropy are declared in `requirements.txt`; Seaborn is imported directly by the plotting functions but is not declared there. These are important dependencies rather than merely similar software.

### 30. Interoperable Software (OPTIONAL)
Not found.

- **Source note:** No separately demonstrated interoperable heliophysics package was found. Dependencies are recorded under Related Software.

### 31. Related Instruments (OPTIONAL)
Not found.

- **Source note:** AFINO is instrument-agnostic and accepts generic arrays. Legacy helper names mention MMS and a default path mentions PROBA2, while an example opens an unspecified flare FITS file; none implements an instrument-specific parser, archive, calibration, or convention. These mentions fail the designed-to-support relevance gate, so no SPASE instrument value is emitted.

### 32. Related Observatories (OPTIONAL)
Not found.

- **Source note:** AFINO is not designed around a specific mission or observatory. MMS and PROBA2 references were considered and excluded as legacy helper/path names without mission-specific data support. Scientific papers applying the method to GOES and other missions do not make the repository implementation mission-specific, so no SPASE observatory value is emitted.

### 33. Logo (OPTIONAL)
Not found.

- **Source note:** No software logo was found in the repository, PyHC entry, or SoMEF output. README status badges are not treated as a logo.
