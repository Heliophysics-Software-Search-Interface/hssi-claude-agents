# HSSI Metadata Extraction Results

**Repository:** https://github.com/spacepy/spacepy
**Extraction Date:** 2026-04-24
**HSSI Sync:** 2026-06-10 — reconciled with the final local HSSI record after the approved enrichment update (software UUID `7bd65217-fdbe-4945-a657-496a494fff48`). Field values below reflect HSSI.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.3252523

(Concept DOI from Zenodo, referenced via README badge and CITATION.cff)

### 3. Code Repository (MANDATORY)
https://github.com/spacepy/spacepy

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms: Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Field-line Tracing
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Pitch Angle Distributions
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Spectrogram
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Line Plots
- Data Visualization: Orbit Plots
- Data Visualization: Spectrogram
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing
- Models and Simulations: ML/AI

Notes on classification:
- Coordinate Transforms (Magnetospheric): `spacepy.coordinates` and `spacepy.ctrans` provide transforms among magnetospheric and Earth-fixed systems (GSE, GSM, SM, GEO, GEI/J2000/TOD/MOD, MAG/CDMAG, TEME, SPH, RLL, GDZ). The "Ionospheric" subcategory is intentionally not claimed because SpacePy does not implement AACGM/MLT/apex coordinate transforms.
- Data Processing and Analysis: file I/O (pycdf for NASA CDF, datamodel for HDF5/JSON-headed ASCII), OMNI data retrieval (`spacepy.omni`), SEA/superposed epoch analysis (`spacepy.seapy`), bootstrap statistics and association analysis (`spacepy.poppy`), AE9/AP9 flux processing (`spacepy.ae9ap9`), pybats for SWMF/BATS-R-US/RAM-SCB output processing, IRBEM-based field-line tracing and L* (`spacepy.irbempy`), generic Spectrogram binning in `spacepy.plot.spectrogram`.
- Data Visualization: `spacepy.plot` provides publication-quality 2D graphics, line plots, spectrograms, and time-tick helpers; pybats provides 2D slices through 3D model output (`Bats2d`, `ShellSlice`, `add_cont_shell`); orbit/trajectory plotting via `plotOrbit` (ae9ap9) and `add_orbit_plot` (pybats `bats` and `ram`).
- Models and Simulations: `spacepy.empiricals` (plasmapause, Shue magnetopause, Lmax, solar wind temperature) and IGRF via `spacepy.igrf` provide empirical models; LANLstar provides an artificial-neural-network-based L*/Lmax model (ML/AI); IRBEM-based magnetic field-line tracing through Tsyganenko field models (`find_footpoint`, `find_magequator`, `get_Lstar`) populates the model-based Field-line Tracing subcategory. The "Physics-Based" and "MHD" subcategories are intentionally not claimed because SpacePy does not run MHD or first-principles physics simulations itself; pybats reads and visualizes external model output.

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Earth Atmosphere
- Interplanetary Space
- Planetary Magnetospheres

Notes: SpacePy's primary focus is Earth's magnetosphere (coordinates, radiation belts, ring current, magnetopause). It also addresses the ionosphere/thermosphere (IGRF, ionospheric coordinate systems, ionospheric model output via pybats.rim) and interplanetary/solar wind (OMNI data, Shue model inputs, pybats IMF input).

### 6. Authors (MANDATORY)

- **Author:** Steven K. Morley
  - **Author Identifier:** https://orcid.org/0000-0001-8520-0199
  - **Affiliation:** Los Alamos National Laboratory
    - Affiliation Identifier: https://ror.org/01e41cf67

- **Author:** Jonathan T. Niehof
  - **Author Identifier:** https://orcid.org/0000-0001-6286-5809
  - **Affiliation:** University of New Hampshire
    - Affiliation Identifier: https://ror.org/01rmh9n78

- **Author:** Daniel T. Welling
  - **Author Identifier:** https://orcid.org/0000-0002-0590-1022
  - **Affiliation:** University of Michigan
    - Affiliation Identifier: https://ror.org/00jmfr291

- **Author:** Brian Larsen
  - **Author Identifier:** https://orcid.org/0000-0003-4515-0208
  - **Affiliation:** Los Alamos National Laboratory
    - Affiliation Identifier: https://ror.org/01e41cf67

- **Author:** Antoine Brunet
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

- **Author:** Miles A. Engel
  - **Author Identifier:** https://orcid.org/0000-0003-4248-9636
  - **Affiliation:** Los Alamos National Laboratory
    - Affiliation Identifier: https://ror.org/01e41cf67

- **Author:** Jan Gieseler
  - **Author Identifier:** https://orcid.org/0000-0003-1848-7067
  - **Affiliation:** University of Turku
    - Affiliation Identifier: https://ror.org/05vghhr25

- **Author:** John Haiducek
  - **Author Identifier:** https://orcid.org/0000-0002-4027-8475
  - **Affiliation:** Not found

- **Author:** Michael Henderson
  - **Author Identifier:** https://orcid.org/0000-0003-4975-9029
  - **Affiliation:** Not found

- **Author:** Aaron Hendry
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

- **Author:** Michael Hirsch
  - **Author Identifier:** https://orcid.org/0000-0002-1637-6526
  - **Affiliation:** Boston University
    - Affiliation Identifier: https://ror.org/05qwgg493

- **Author:** Peter Killick
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

- **Author:** Josef Koller
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

- **Author:** Asher Merrill
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

- **Author:** Lutz Rastatter
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

- **Author:** Ashton Reimer
  - **Author Identifier:** https://orcid.org/0000-0002-4621-3453
  - **Affiliation:** SRI International
    - Affiliation Identifier: https://ror.org/05s570m15

- **Author:** Albert Y. Shih
  - **Author Identifier:** https://orcid.org/0000-0001-6874-2594
  - **Affiliation:** Goddard Space Flight Center
    - Affiliation Identifier: https://ror.org/0171mag52

- **Author:** Amanda Stricklan
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

> **Name preservation:** `CITATION.cff` gives **Brian A. Larsen**, but the shared HSSI Person record is **Brian Larsen**. The user explicitly chose to preserve the existing HSSI name, so the final HSSI author list uses **Brian Larsen**.

(Source: Final local HSSI author list, unioned with all 18 `CITATION.cff` authors while preserving existing HSSI Person records and affiliations.)

### 7. Software Name (MANDATORY)
SpacePy

### 8. Description (MANDATORY)
SpacePy is a Python package for the space sciences that makes data analysis, modeling, and visualization easier. It supports obtaining OMNI and Qin-Denton data; reading and writing NASA CDF, HDF5, and JSON-headed ASCII; publication-quality plotting; superposed epoch, association, and bootstrap analyses; empirical plasmapause, magnetopause, Lmax, and radiation-belt models; coordinate and time conversion; IRBEM magnetic-field tracing and L-star calculations; IGRF; the LANLstar neural-network model; AE9/AP9 output; and PyBats analysis and visualization of SWMF, BATS-R-US, RAM-SCB, and GITM output.

### 9. Concise Description (OPTIONAL)
Python tools for space-science data analysis, coordinate and time conversion, empirical modeling, scientific file I/O, and publication-quality visualization.

### 10. Publication Date (RECOMMENDED)
2010-05-20

(Date of initial commit in the public repository. First Zenodo release of the software with DOI 10.5281/zenodo.3252523 issued 2019-06-19; first scholarly publication Morley et al., SciPy 2010 Proceedings, 2011.)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

### 12. Version (RECOMMENDED)
- **Version Number:** 0.7.0
- **Version Date:** 2024-11-08
- **Version Description:** Binary wheels now provided for 64-bit ARM Linux (Raspberry Pi). `help()` supports searching the documentation. Full NumPy 2.0 support. NumPy and f2py are no longer required to build SpacePy (binary wheels decoupled from NumPy/Python version). Support for Python 3.6 removed; Python 3.7+ required. Several deprecations including `toolbox.timeout_check_call`. `data_assimilation`, `radbelt`, and `spacepy_EnKF` modules moved to sandbox.
- **Version PID:** https://doi.org/10.5281/zenodo.14057789

(Note: `pyproject.toml` indicates an in-development version of 0.8.0a0; 0.7.0 remains the most recent tagged public release.)

### 13. Programming Language (RECOMMENDED)
- C
- Fortran77
- Fortran90
- Python 3.x

(Python is the primary language. C source is present in `libspacepy`. The bundled IRBEMlib Fortran is primarily fixed-format Fortran77 but uses Fortran 90 features (e.g., `!`-prefixed line comments) so both `Fortran77` and `Fortran90` are listed. The project's classifiers explicitly list "Programming Language :: C" and "Programming Language :: Fortran".)

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.3389/fspas.2022.1023612

(Niehof, J. T., Morley, S. K., Welling, D. T., & Larsen, B. A. (2022). The SpacePy space science package at 12 years. Frontiers in Astronomy and Space Sciences, 9. This is the preferred package reference per the README and CITATION.cff. An additional historical reference is the SciPy 2010 paper at https://doi.org/10.25080/Majora-92bf1922-012.)

### 15. License (RECOMMENDED)
- **Repository License:** Python Software Foundation License 2.0
- **License URI:** https://spdx.org/licenses/PSF-2.0.html

> **HSSI vocabulary recommendation:** Add Python Software Foundation License 2.0 to HSSI's controlled license vocabulary. The current local HSSI record leaves the license field empty rather than mapping SpacePy to the inaccurate generic `Other` entry.

(LICENSE.md contains a license modeled on the Python Software Foundation License, granted by Triad National Security, LLC (Los Alamos National Laboratory). pyproject.toml classifier: "License :: OSI Approved :: Python Software Foundation License". The bundled modified IRBEMlib is separately covered by the LGPL.)

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- Ascii
- Batsrus
- Cdf
- Coordinates
- Csv
- Data Access
- Data Analysis
- Data Container
- Hdf5
- Heliophysics
- Igrf
- Ionosphere
- Magnetohydrodynamics
- Magnetosphere
- Omni
- Physics
- Plasma
- Plotting
- Python
- Radiation Belts
- Reference Data
- Shue
- Simulation
- Solar Wind
- Space
- Space Weather
- Swmf
- Time
- Tsyganenko

(Sources: pyproject.toml `keywords`, PyHC registry entry, README, and capabilities documentation.)

### 17. Data Sources (OPTIONAL)
- FTP/FTPS Directories
- HTTP/HTTPS Directories
- Observatory/Mission-specific
- OMNIWeb
- Other

(OMNIWeb via `spacepy.omni` and the Qin-Denton OMNI database; toolbox.update() fetches leapseconds, OMNI, PSDdata, and QD-OMNI over HTTP/FTP; pybats reads mission/model outputs (SWMF/BATS-R-US, RAM-SCB, GITM); AE9/AP9 files are supported.)

### 18. Input File Formats (RECOMMENDED)
- ascii
- CDF
- HDF5
- IDL.sav
- ISTP-Compliant
- JSON
- netCDF3/4
- Other

(NASA CDF via `spacepy.pycdf`; HDF5 and netCDF via `spacepy.datamodel`; ISTP-compliant CDF metadata checks and tooling via `pycdf.istp`; JSON-headed ASCII via datamodel; IDL .sav via scipy.io.readsav usage noted in docs; "Other" covers proprietary SWMF/BATS-R-US IDL binary output, RAM-SCB binary/NetCDF, AE9/AP9 text outputs.)

### 19. Output File Formats (RECOMMENDED)
- ascii
- CDF
- HDF5
- ISTP-Compliant
- JSON
- Other

(SpacePy datamodel and pycdf support writing to each of these formats via `toCDF`, `toHDF5`, and `toJSONheadedASCII`. netCDF is supported only on input (via `fromNC3`/`fromHDF5` for netCDF4-as-HDF5), not output, so it is intentionally omitted here.)

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

(pyproject.toml classifiers explicitly list MacOS X, Microsoft Windows, POSIX, and POSIX:Linux. CI runs across Linux, macOS, and Windows.)

### 21. CPU Architecture (RECOMMENDED)
- Apple Silicon arm64
- Linux aarch64 or arm64
- x86-64

(Release notes for 0.7.0 explicitly add 64-bit ARM Linux wheels (Raspberry Pi); macOS wheels include Apple Silicon; x86-64 supported on all three OSes.)

### 22. Related Phenomena (OPTIONAL)
Not found

(No related phenomena are present in the final HSSI record. SpacePy supports geomagnetic storms, radiation belts, substorms, ring current, plasmapause, magnetopause, and solar-wind studies. This field was left empty in the approved update; a future review could consider the currently controlled terms Solar Wind and Geomagnetic Storms.)

### 23. Development Status (RECOMMENDED)
Active

(Recent commits through March 2026; ongoing releases; pyproject.toml classifier "Development Status :: 4 - Beta"; PyHC rating "Software Maturity: Good".)

### 24. Documentation (RECOMMENDED)
https://spacepy.github.io/

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
  - **Funder Identifier:** https://ror.org/027ka1x80
- **Organization:** United States Department of Energy
  - **Funder Identifier:** https://ror.org/01bj3aw27

(These two funders were preserved from the pre-existing HSSI record. Repository copyright notices additionally document development at Los Alamos National Laboratory, but that institution is not currently represented as a SpacePy funder in HSSI.)

### 26. Award Title (OPTIONAL)
Not found

(No explicit grant/award title or number is listed in the repository or the Zenodo/DataCite record.)

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.25080/Majora-92bf1922-012 (Morley, S. K. et al. (2011). SpacePy - A Python-based library of tools for the space sciences. Proceedings of the 9th Python in Science Conference (SciPy 2010).)
- https://doi.org/10.3389/fspas.2022.1023612 (Niehof, J. T. et al. (2022). The SpacePy space science package at 12 years. Frontiers in Astronomy and Space Sciences, 9.)

(Both are listed as general references for the package in CITATION.cff.)

### 28. Related Datasets (OPTIONAL)
Not found

(SpacePy operates on data from many external sources (OMNI/Qin-Denton, NASA CDF archives, AE9/AP9 model output, SWMF model output) but no specific dataset DOIs are documented in the repository as "related datasets".)

### 29. Related Software (OPTIONAL)
- https://github.com/heliopython/heliopy (HelioPy - related heliophysics Python toolbox; archived/no longer actively maintained)
- https://github.com/MAVENSDC/cdflib (pure-Python CDF library, similar/alternative to `spacepy.pycdf`)
- https://github.com/PRBEM/IRBEM (IRBEM library - bundled and wrapped by `spacepy.irbempy`)
- https://github.com/spacepy/dbprocessing (companion data processing framework from the SpacePy organization)
- https://github.com/sunpy/sunpy (sister heliophysics Python package; PyHC core)

### 30. Interoperable Software (OPTIONAL)
- https://matplotlib.org/ (Matplotlib - required runtime dependency for visualization)
- https://pandas.pydata.org/ (pandas - datamodel provides pandas integration for SpaceData/dmarray)
- https://scipy.org/ (SciPy - required runtime dependency)
- https://www.astropy.org/ (Astropy - optional interoperability in `spacepy.time` and `spacepy.coordinates` via SkyCoord conversion)
- https://www.h5py.org/ (h5py - required for HDF5 I/O)
- https://www.numpy.org/ (NumPy - required runtime dependency)

### 31. Related Instruments (OPTIONAL)
Not found

(SpacePy is a general-purpose toolkit and is not designed for a specific instrument. Many modules (e.g., pycdf, pybats) are used with data from many instruments but no single "related instrument" is appropriate.)

### 32. Related Observatories (OPTIONAL)
Not found

(No observatories are present in the final HSSI record. The extracted candidates — SWMF/BATS-R-US, RAM-SCB, GITM, OMNI, and AE9/AP9 — are model frameworks or data products rather than observatories, so they were intentionally not added to HSSI's global observatory vocabulary.)

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/spacepy/spacepy/main/Doc/source/_static/spacepy_logo.jpg

(Source: Canonical logo asset in the SpacePy repository.)
