# HSSI Metadata Extraction Results

**Repository:** https://github.com/spacepy/spacepy
**Extraction Date:** 2026-04-24

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
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:Field-line Tracing
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Pitch Angle Distributions
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Spectrogram
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:2D Slices
- Data Visualization:Line Plots
- Data Visualization:Orbit Plots
- Data Visualization:Spectrogram
- Models and Simulations
- Models and Simulations:Empirical
- Models and Simulations:Field-line Tracing
- Models and Simulations:ML/AI

Notes on classification:
- Coordinate Transforms (Magnetospheric): `spacepy.coordinates` and `spacepy.ctrans` provide transforms among magnetospheric and Earth-fixed systems (GSE, GSM, SM, GEO, GEI/J2000/TOD/MOD, MAG/CDMAG, TEME, SPH, RLL, GDZ). The "Ionospheric" subcategory is intentionally not claimed because SpacePy does not implement AACGM/MLT/apex coordinate transforms.
- Data Processing and Analysis: file I/O (pycdf for NASA CDF, datamodel for HDF5/JSON-headed ASCII), OMNI data retrieval (`spacepy.omni`), SEA/superposed epoch analysis (`spacepy.seapy`), bootstrap statistics and association analysis (`spacepy.poppy`), AE9/AP9 flux processing (`spacepy.ae9ap9`), pybats for SWMF/BATS-R-US/RAM-SCB output processing, IRBEM-based field-line tracing and L* (`spacepy.irbempy`), generic Spectrogram binning in `spacepy.plot.spectrogram`.
- Data Visualization: `spacepy.plot` provides publication-quality 2D graphics, line plots, spectrograms, and time-tick helpers; pybats provides 2D slices through 3D model output (`Bats2d`, `ShellSlice`, `add_cont_shell`); orbit/trajectory plotting via `plotOrbit` (ae9ap9) and `add_orbit_plot` (pybats `bats` and `ram`).
- Models and Simulations: `spacepy.empiricals` (plasmapause, Shue magnetopause, Lmax, solar wind temperature) and IGRF via `spacepy.igrf` provide empirical models; LANLstar provides an artificial-neural-network-based L*/Lmax model (ML/AI); IRBEM-based magnetic field-line tracing through Tsyganenko field models (`find_footpoint`, `find_magequator`, `get_Lstar`) populates the model-based Field-line Tracing subcategory. The "Physics-Based" and "MHD" subcategories are intentionally not claimed because SpacePy does not run MHD or first-principles physics simulations itself; pybats reads and visualizes external model output.

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Earth Atmosphere
- Interplanetary Space

Notes: SpacePy's primary focus is Earth's magnetosphere (coordinates, radiation belts, ring current, magnetopause). It also addresses the ionosphere/thermosphere (IGRF, ionospheric coordinate systems, ionospheric model output via pybats.rim) and interplanetary/solar wind (OMNI data, Shue model inputs, pybats IMF input).

### 6. Authors (MANDATORY)

- **Author:** Steven K. Morley
  - **Author Identifier:** https://orcid.org/0000-0001-8520-0199
  - **Affiliation:** Los Alamos National Laboratory
    - Affiliation Identifier: https://ror.org/01e41cf67

- **Author:** Jonathan T. Niehof
  - **Author Identifier:** https://orcid.org/0000-0001-6286-5809
  - **Affiliation:** University of New Hampshire
    - Affiliation Identifier: https://ror.org/03rmrcq20

- **Author:** Daniel T. Welling
  - **Author Identifier:** https://orcid.org/0000-0002-0590-1022
  - **Affiliation:** University of Michigan
    - Affiliation Identifier: https://ror.org/00jmfr291

- **Author:** Brian A. Larsen
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
  - **Affiliation:** Not found

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
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

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
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

- **Author:** Albert Y. Shih
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

- **Author:** Amanda Stricklan
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

(Source: CITATION.cff and DataCite metadata for DOI 10.5281/zenodo.3252523)

### 7. Software Name (MANDATORY)
SpacePy

### 8. Description (MANDATORY)
SpacePy is a package for Python, targeted at the space sciences, that aims to make basic data analysis, modeling and visualization easier. It builds on the capabilities of the well-known NumPy and MatPlotLib packages. Publication-quality output direct from analyses is emphasized. Core capabilities include: quickly obtaining data (e.g., OMNI/Qin-Denton solar-wind and geomagnetic indices); reading and writing data in formats like NASA CDF, HDF5, and JSON-headed ASCII; creating publication-quality plots; performing complicated scientific analysis easily (superposed epoch analysis, association analysis, bootstrap statistics); running common empirical models (plasmapause, magnetopause, Lmax, radiation-belt models); changing coordinate and time systems effortlessly (GSE, GSM, SM, GEO, GEI/ECI2000/ECITOD/ECIMOD, MAG, TEME, SPH, RLL, GDZ, plus quaternion-based generalized transforms and many time systems including UTC, TAI, GPS, ISO, JD/MJD, CDF epoch, TT2000). SpacePy also wraps IRBEMlib (magnetic-field tracing and L*/phase-space-density calculations), ships an IGRF implementation, provides the LANLstar neural-network model, supports AE9/AP9 radiation-belt model output, and includes PyBats for analysis and visualization of SWMF/BATS-R-US/RAM-SCB/GITM output. The SpacePy project seeks to promote accurate and open research by providing a comprehensive, open-source library of widely-used space-physics analysis and visualization tools in a free, modern, and intuitive language.

### 9. Concise Description (OPTIONAL)
SpacePy is a Python package for the space sciences providing data analysis, modeling, coordinate and time conversions, file I/O (including NASA CDF), and publication-quality visualization for magnetospheric and space-weather research.

### 10. Publication Date (RECOMMENDED)
2010-05-20

(Date of initial commit in the public repository. First Zenodo release of the software with DOI 10.5281/zenodo.3252523 issued 2019-06-19; first scholarly publication Morley et al., SciPy 2010 Proceedings, 2011.)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://ror.org/01ggx4157

(Zenodo is operated by CERN; the ROR record is for CERN — European Organization for Nuclear Research. Zenodo does not have a separate ROR entry.)

### 12. Version (RECOMMENDED)
- **Version Number:** 0.7.0
- **Version Date:** 2024-11-08
- **Version Description:** Binary wheels now provided for 64-bit ARM Linux (Raspberry Pi). `help()` supports searching the documentation. Full NumPy 2.0 support. NumPy and f2py are no longer required to build SpacePy (binary wheels decoupled from NumPy/Python version). Support for Python 3.6 removed; Python 3.7+ required. Several deprecations including `toolbox.timeout_check_call`. `data_assimilation`, `radbelt`, and `spacepy_EnKF` modules moved to sandbox.
- **Version PID:** Not found (per-version DOI not published; concept DOI is https://doi.org/10.5281/zenodo.3252523)

(Note: pyproject.toml indicates an in-development version of 0.8.0a0; 0.7.0 is the most recent tagged public release. A preliminary 0.8.0 release-notes section exists for an upcoming release.)

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- C
- Fortran77
- Fortran90

(Python is the primary language. C source is present in `libspacepy`. The bundled IRBEMlib Fortran is primarily fixed-format Fortran77 but uses Fortran 90 features (e.g., `!`-prefixed line comments) so both `Fortran77` and `Fortran90` are listed. The project's classifiers explicitly list "Programming Language :: C" and "Programming Language :: Fortran".)

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.3389/fspas.2022.1023612

(Niehof, J. T., Morley, S. K., Welling, D. T., & Larsen, B. A. (2022). The SpacePy space science package at 12 years. Frontiers in Astronomy and Space Sciences, 9. This is the preferred package reference per the README and CITATION.cff. An additional historical reference is the SciPy 2010 paper at https://doi.org/10.25080/Majora-92bf1922-012.)

### 15. License (RECOMMENDED)
- **License:** Python Software Foundation License 2.0
- **License URI:** https://spdx.org/licenses/PSF-2.0.html

(LICENSE.md contains a license modeled on the Python Software Foundation License, granted by Triad National Security, LLC (Los Alamos National Laboratory). pyproject.toml classifier: "License :: OSI Approved :: Python Software Foundation License". The bundled modified IRBEMlib is separately covered by the LGPL.)

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- magnetosphere
- plasma
- physics
- space
- solar wind
- space weather
- magnetohydrodynamics
- heliophysics
- coordinates
- cdf
- hdf5
- ascii
- csv
- data access
- data analysis
- data container
- ionosphere
- igrf
- omni
- plotting
- simulation
- swmf
- batsrus
- shue
- tsyganenko
- reference data
- time
- radiation belts

(Sources: pyproject.toml `keywords`, PyHC registry entry, README, and capabilities documentation.)

### 17. Data Sources (OPTIONAL)
- OMNIWeb
- HTTP/HTTPS Directories
- FTP/FTPS Directories
- Observatory/Mission-specific
- Other

(OMNIWeb via `spacepy.omni` and the Qin-Denton OMNI database; toolbox.update() fetches leapseconds, OMNI, PSDdata, and QD-OMNI over HTTP/FTP; pybats reads mission/model outputs (SWMF/BATS-R-US, RAM-SCB, GITM); AE9/AP9 files are supported.)

### 18. Input File Formats (RECOMMENDED)
- CDF
- HDF5
- netCDF3/4
- ISTP-Compliant
- ascii
- JSON
- IDL.sav
- Other

(NASA CDF via `spacepy.pycdf`; HDF5 and netCDF via `spacepy.datamodel`; ISTP-compliant CDF metadata checks and tooling via `pycdf.istp`; JSON-headed ASCII via datamodel; IDL .sav via scipy.io.readsav usage noted in docs; "Other" covers proprietary SWMF/BATS-R-US IDL binary output, RAM-SCB binary/NetCDF, AE9/AP9 text outputs.)

### 19. Output File Formats (RECOMMENDED)
- CDF
- HDF5
- ascii
- JSON
- ISTP-Compliant

(SpacePy datamodel and pycdf support writing to each of these formats via `toCDF`, `toHDF5`, and `toJSONheadedASCII`. netCDF is supported only on input (via `fromNC3`/`fromHDF5` for netCDF4-as-HDF5), not output, so it is intentionally omitted here.)

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

(pyproject.toml classifiers explicitly list MacOS X, Microsoft Windows, POSIX, and POSIX:Linux. CI runs across Linux, macOS, and Windows.)

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64
- Linux aarch64 or arm64

(Release notes for 0.7.0 explicitly add 64-bit ARM Linux wheels (Raspberry Pi); macOS wheels include Apple Silicon; x86-64 supported on all three OSes.)

### 22. Related Phenomena (OPTIONAL)
Not found

(SpacePy's primary phenomena focus is magnetospheric/ionospheric: geomagnetic storms, radiation belts, substorms, ring current, plasmapause, magnetopause, solar wind. None of these match the HSSI controlled vocabulary for this field (Coronal Heating, Coronal Holes, Coronal Mass Ejections, Solar Corona, Solar Flares, X-ray emission), so the field is left empty rather than submit values outside the controlled list.)

### 23. Development Status (RECOMMENDED)
Active

(Recent commits through March 2026; ongoing releases; pyproject.toml classifier "Development Status :: 4 - Beta"; PyHC rating "Software Maturity: Good".)

### 24. Documentation (RECOMMENDED)
https://spacepy.github.io/

### 25. Funder (OPTIONAL)
- **Organization:** Los Alamos National Laboratory (Triad National Security, LLC)
  - **Funder Identifier:** https://ror.org/01e41cf67

(Copyright notices across the codebase attribute development to Los Alamos National Security/Triad National Security, LLC; no explicit external funding agencies listed in the repository or DataCite record. Additional funders may exist but are not documented in authoritative repository files.)

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
- https://github.com/PRBEM/IRBEM (IRBEM library - bundled and wrapped by `spacepy.irbempy`)
- https://github.com/MAVENSDC/cdflib (pure-Python CDF library, similar/alternative to `spacepy.pycdf`)
- https://github.com/sunpy/sunpy (sister heliophysics Python package; PyHC core)
- https://github.com/heliopython/heliopy (HelioPy - related heliophysics Python toolbox; note: archived/no longer actively maintained, with much of its functionality now in sunpy)
- https://github.com/spacepy/dbprocessing (companion data processing framework from the SpacePy organization)

### 30. Interoperable Software (OPTIONAL)
- https://www.numpy.org/ (NumPy - required runtime dependency)
- https://matplotlib.org/ (Matplotlib - required runtime dependency for visualization)
- https://scipy.org/ (SciPy - required runtime dependency)
- https://www.h5py.org/ (h5py - required for HDF5 I/O)
- https://www.astropy.org/ (Astropy - optional interoperability in `spacepy.time` and `spacepy.coordinates` via SkyCoord conversion)
- https://pandas.pydata.org/ (pandas - datamodel provides pandas integration for SpaceData/dmarray)

### 31. Related Instruments (OPTIONAL)
Not found

(SpacePy is a general-purpose toolkit and is not designed for a specific instrument. Many modules (e.g., pycdf, pybats) are used with data from many instruments but no single "related instrument" is appropriate.)

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Space Weather Modeling Framework (SWMF) / BATS-R-US
- **Observatory Name:** RAM-SCB
- **Observatory Name:** GITM (Global Ionosphere-Thermosphere Model)
- **Observatory Name:** OMNI
- **Observatory Name:** AE9/AP9 (radiation-belt model ensemble)

(These are model frameworks/data products the pybats, omni, and ae9ap9 modules specifically support. SpacePy is not mission-specific.)

### 33. Logo (OPTIONAL)
https://spacepy.github.io/_static/spacepy_logo.jpg

(Source: PyHC registry entry.)

