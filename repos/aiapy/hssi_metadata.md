# HSSI Metadata Extraction Results

**HSSI Software ID:** dda4b683-307d-4145-b75c-59f61c442484
**Repository:** https://github.com/LM-SAL/aiapy
**Source Revision:** afc3db737a2f140ec8069126371866cec9e14be5
**Extraction Date:** 2026-07-27
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** To be filled by actual submitter
- **Submitter Email:** To be filled by actual submitter
- **Source:** Submitter information is not present in the public HSSI view and must be supplied at submission time.

### 2. Persistent Identifier (RECOMMENDED)
- https://doi.org/10.5281/zenodo.10064346
- **Source:** Preserved from the existing HSSI record and confirmed as the current Zenodo concept DOI by the DataCite and Zenodo APIs.

### 3. Code Repository (MANDATORY)
- https://github.com/LM-SAL/aiapy
- **Source:** Preserved from the existing HSSI record; confirmed by the cloned Git origin, repository package metadata, PyPI, PyHC, GitHub, and SoMEF.

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Processing
- Mission-related
- Mission-related:Analysis
- Mission-related:Calibration
- Mission-related:Instrument Response
- Mission-related:Observatory/Instrument Models
- Mission-related:Processing
- Mission-related:Science Data Processing
- Models and Simulations
- Models and Simulations:Instrument Response
- Models and Simulations:Observatory/Instrument Models
- **Source:** The submitted Data Processing and Analysis parent is preserved. The aiapy public API and documentation implement AIA image registration, pointing correction, respiking, degradation correction, uncertainty estimation, PSF calculation and deconvolution, wavelength-response calculation, and retrieval of AIA calibration/pointing/spike data. The package is purpose-built for the SDO/AIA mission and explicitly models the instrument PSF and wavelength response. Every selected subcategory includes its required parent. Data Visualization and its three previously proposed subcategories were removed by explicit user decision because the gallery uses external plotting tools rather than visualization implemented by aiapy.
- **Note:** Coordinate Transforms was considered but omitted because image rotation/alignment is an AIA calibration operation, not a user-facing conversion among named coordinate systems.

### 5. Related Region (MANDATORY)
- Solar Environment
- Corona
- **Source:** `Solar Environment` is confirmed by the repository description, PyHC registry, package keywords, and JOSS paper. `Corona` is supported directly by the project's JOSS paper: `487a257^:joss/paper.md:73` identifies the corona as AIA's target for quiescent-heating studies, and `487a257^:joss/paper.md:80` scopes aiapy to analysis of calibrated AIA EUV imaging data. The current documentation independently confirms its EUV wavelength-response capability (`docs/index.rst:9`), and Field 22 records `Solar Corona` and `Coronal Heating` from the same project evidence.
- **How to re-read the JOSS paper evidence.** `joss/paper.md` is **not present at the extracted source revision**: it was deleted by commit `487a257` ("Package overhaul", 2023-11-02). The citations above therefore address `487a257^`, the parent commit, which is the last revision containing the file — retrieve it with `git show 487a257^:joss/paper.md`. A future agent should not read the file's absence from the current tree as evidence that these citations are wrong; the published JOSS article at `https://doi.org/10.21105/joss.02801` (Field 14) carries the same text.

### 6. Authors (MANDATORY)
- **Author:** Will Barnes
  - **Author Identifier:** https://orcid.org/0000-0001-9642-6089
  - **Affiliation:** American University
    - **Affiliation Identifier:** https://ror.org/052w4zt36
  - **Affiliation:** Department of Physics, American University
    - **Affiliation Identifier:** Not found
  - **Affiliation:** Goddard Space Flight Center
    - **Affiliation Identifier:** https://ror.org/0171mag52
  - **Affiliation:** United States Naval Research Laboratory
    - **Affiliation Identifier:** https://ror.org/04d23a975
- **Author:** Monica Bobra
  - **Author Identifier:** https://orcid.org/0000-0002-5662-9604
  - **Affiliation:** State of California, Office of Data and Innovation @cagov
    - **Affiliation Identifier:** Not found
  - **Affiliation:** W. W. Hansen Experimental Physics Laboratory, Stanford University
    - **Affiliation Identifier:** Not found
  - **Affiliation:** Stanford University
    - **Affiliation Identifier:** https://ror.org/00f54p054
- **Author:** Mark C. M. Cheung
  - **Author Identifier:** https://orcid.org/0000-0003-2110-9753
  - **Affiliation:** Lockheed Martin Solar and Astrophysics Laboratory
    - **Affiliation Identifier:** Not found
- **Author:** Nabil Freij
  - **Author Identifier:** https://orcid.org/0000-0002-6253-082X
  - **Affiliation:** Bay Area Environmental Research Institute
    - **Affiliation Identifier:** https://ror.org/024tt5x58
  - **Affiliation:** Lockheed Martin Solar and Astrophysics Laboratory
    - **Affiliation Identifier:** Not found
  - **Affiliation:** SETI Institute
    - **Affiliation Identifier:** https://ror.org/02dxgk712
- **Author:** Georgios Chintzoglou
  - **Author Identifier:** https://orcid.org/0000-0002-1253-8882
  - **Affiliation:** Lockheed Martin Solar and Astrophysics Laboratory
    - **Affiliation Identifier:** Not found
  - **Affiliation:** University Corporation for Atmospheric Research
    - **Affiliation Identifier:** https://ror.org/04zhhyn23
- **Author:** J. Marcus Hughes
  - **Author Identifier:** https://orcid.org/0000-0003-3410-7650
  - **Affiliation:** Southwest Research Institute
    - **Affiliation Identifier:** https://ror.org/03tghng59
- **Author:** Manan Kocher
  - **Author Identifier:** Not found
  - **Affiliation:** Not found
- **Author:** Stuart J. Mumford
  - **Author Identifier:** https://orcid.org/0000-0003-4217-4642
  - **Affiliation:** Aperio Software Ltd.
    - **Affiliation Identifier:** Not found
  - **Affiliation:** University of Sheffield
    - **Affiliation Identifier:** https://ror.org/05krs5044
- **Author:** Nina Shirman
  - **Author Identifier:** https://orcid.org/0000-0001-7136-8628
  - **Affiliation:** Lockheed Martin Solar and Astrophysics Laboratory
    - **Affiliation Identifier:** Not found
- **Author:** Albert Y. Shih
  - **Author Identifier:** https://orcid.org/0000-0001-6874-2594
  - **Affiliation:** Goddard Space Flight Center
    - **Affiliation Identifier:** https://ror.org/0171mag52
- **Author:** David Stansby
  - **Author Identifier:** https://orcid.org/0000-0002-1365-1908
  - **Affiliation:** Advanced Research Computing Centre, University College London, UK
    - **Affiliation Identifier:** Not found
  - **Affiliation:** Department of Mechanical Engineering, University College London
    - **Affiliation Identifier:** Not found
  - **Affiliation:** Imperial College London
    - **Affiliation Identifier:** https://ror.org/041kmwe10
  - **Affiliation:** Mullard Space Science Laboratory, University College London
    - **Affiliation Identifier:** Not found
  - **Affiliation:** University College London
    - **Affiliation Identifier:** https://ror.org/02jx3x895
- **Author:** Paul Wright
  - **Author Identifier:** https://orcid.org/0000-0001-9021-611X
  - **Affiliation:** Dublin Institute for Advanced Studies
    - **Affiliation Identifier:** https://ror.org/051sx6d27
  - **Affiliation:** University of Exeter
    - **Affiliation Identifier:** https://ror.org/03yghzc09
  - **Affiliation:** W. W. Hansen Experimental Physics Laboratory, Stanford University
    - **Affiliation Identifier:** Not found
  - **Affiliation:** Stanford University
    - **Affiliation Identifier:** https://ror.org/00f54p054
- **Author:** Laura Hayes
  - **Author Identifier:** https://orcid.org/0000-0002-6835-2390
  - **Affiliation:** Dublin Institute for Advanced Studies
    - **Affiliation Identifier:** https://ror.org/051sx6d27
  - **Affiliation:** European Space Research and Technology Centre
    - **Affiliation Identifier:** https://ror.org/03h3jqn23
- **Author:** Paul F. Boerner
  - **Author Identifier:** https://orcid.org/0000-0002-4490-9860
  - **Affiliation:** Lockheed Martin Solar and Astrophysics Laboratory
    - **Affiliation Identifier:** Not found
- **Author:** Andrew J. Leonard
  - **Author Identifier:** https://orcid.org/0000-0001-5270-7487
  - **Affiliation:** Aperio Software Ltd.
    - **Affiliation Identifier:** Not found
- **Author:** Nicholas Padmanabhan
  - **Author Identifier:** https://orcid.org/0000-0001-8067-6788
  - **Affiliation:** Princeton University
    - **Affiliation Identifier:** https://ror.org/00hx57361
- **Source:** The author and affiliation set is supported by the current v0.12.1 Zenodo/DataCite creators, repository history, and the project JOSS paper/archived Zenodo metadata. JOSS supplies authoritative ORCIDs and full names for Mark C. M. Cheung, Georgios Chintzoglou, and Nina Shirman; repository history maps the handles `gchintzo`, `mkocher56`, and `nsshirman` to Georgios Chintzoglou, Manan Kocher, and Nina Shirman. The established identity labels for Will Barnes, Monica Bobra, Laura Hayes, Paul Wright, and Andrew J. Leonard are retained. Laura Hayes is resolved by ORCID and carries the complete supported affiliation set of Dublin Institute for Advanced Studies and European Space Research and Technology Centre. The JOSS author list supports Paul F. Boerner, Andrew J. Leonard, and Nicholas Padmanabhan.
- **Note:** By explicit user decision, `Hellseher` is omitted because no authoritative two-part personal name exists, and `AIA Instrument Team @ LMSAL` is omitted because no exact ROR exists and the API would misclassify it as a Person.
- **Affiliation naming note:** ROR `https://ror.org/04d23a975` registers **United States Naval Research Laboratory** as its display name, and that is the form recorded above and held on the shared organization record. An earlier revision of this file carried the shorter `Naval Research Laboratory`; that bare form is stale and should not be restored. Affiliations bind on the ROR identifier, so the shorter label never mis-linked anything — it was a display inconsistency only.

### 7. Software Name (MANDATORY)
- aiapy
- **Source:** Preserved from the existing HSSI record and confirmed by the repository, Python package metadata, PyPI, PyHC, GitHub, Zenodo, and JOSS paper.

### 8. Description (MANDATORY)
aiapy is a Python package for analyzing data from the Atmospheric Imaging Assembly (AIA) instrument onboard NASA's Solar Dynamics Observatory (SDO) spacecraft. It calibrates and processes AIA images by updating pointing metadata, registering level 1 images to level 1.5, reinserting removed spikes, correcting instrument degradation, estimating uncertainty, calculating and deconvolving the instrument point-spread function, and calculating wavelength response functions. Its public workflows exchange SunPy maps and Astropy quantities, coordinates, times, and tables.

- **Source:** The submitted opening sentence is preserved verbatim. The capability details come from the current repository documentation, public API, maintained gallery, and JOSS paper.
- **Replacement rationale:** The existing HSSI description appended the complete v0.10.2 GitHub release-note body to the valid package description. That objectively unrelated release text was removed and replaced with current, source-backed capability detail.

### 9. Concise Description (OPTIONAL)
Python tools for calibrating, registering, correcting, deconvolving, and analyzing Solar Dynamics Observatory Atmospheric Imaging Assembly data.

- **Source:** Current repository documentation and public API.
- **Replacement rationale:** The existing concise description is a truncated fragment of the accidentally appended v0.10.2 release notes, not a description of aiapy.

### 10. Publication Date (RECOMMENDED)
- 2020-03-31
- **Source:** The annotated `v0.1.0` tag and release commit are both dated 2020-03-31, and PyPI identifies 0.1.0 as the first release on that date.
- **Replacement rationale:** The submitted 2025-09-13 date is the release date of v0.10.2, not aiapy's initial publication date.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** Preserved from the existing HSSI record and confirmed by the concept and version DOI records.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.12.1
- **Version Date:** 2026-06-25
- **Version Description:** Documentation release that revamped the aiapy installation page.
- **Version PID:** https://doi.org/10.5281/zenodo.20873249
- **Source:** Current Git tag and changelog, GitHub Release, PyPI, DataCite, and Zenodo all independently identify v0.12.1 on 2026-06-25. The version DOI is from the current Zenodo record.
- **Replacement rationale:** The existing HSSI version is v0.10.2 dated 2025-09-13; v0.12.1 is the latest authoritative release and supersedes it.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- **Source:** Preserved from the existing HSSI record. Confirmed by repository language metadata, SoMEF, PyPI, and `pyproject.toml`, which currently requires Python 3.12 or newer.

### 14. Reference Publication (RECOMMENDED)
- https://doi.org/10.21105/joss.02801
- **Source:** Preserved from the existing HSSI record and confirmed by the repository citation instructions and the Journal of Open Source Software.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause
- **Source:** The license name is preserved from the existing HSSI record and confirmed by DataCite, Zenodo, PyPI, GitHub, SoMEF, and `LICENSE.rst`. DataCite supplies the SPDX-linked license URI.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- AIA calibration
- extreme ultraviolet
- image deconvolution
- instrument degradation
- instrument response
- point-spread function
- solar imaging
- solar physics
- **Source:** Repository package keywords, PyHC registry, JOSS paper, documentation, and public module capabilities. SDO/AIA names are represented structurally in Fields 31-32 rather than repeated as free keywords.

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- Observatory/Mission-specific
- **Source:** User-facing functions retrieve AIA correction/error files from SSW HTTPS mirrors and the LMSAL GitHub backup, and retrieve AIA response, pointing, and spike records from the mission-specific Joint Science Operations Center (JSOC).
- **Note:** The Virtual Solar Observatory appears in a SunPy-based gallery acquisition example but was not added because aiapy itself does not implement that client; JSOC and the AIA/SDO file sources are the direct package-supported sources.

### 18. Input File Formats (RECOMMENDED)
- ascii
- FITS
- Other
- **Other format:** SolarSoftWare IDL GENX instrument-response files
- **Source:** AIA images are accepted as FITS-backed SunPy maps; correction and error tables are read from ASCII files; `aiapy.response.Channel` reads SolarSoftWare GENX instrument files.

### 19. Output File Formats (RECOMMENDED)
- FITS
- **Source:** Calibration and deconvolution functions return SunPy AIA maps, and the maintained test suite verifies that registered level 1.5 output is saved to and reloaded from FITS without losing adjusted metadata.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows
- **Source:** Current CI tests Linux, macOS, and Windows. The installation guide supplies installers for all three operating systems.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64
- Linux aarch64 or arm64
- ppc64le
- GPU
- **Source:** The current installation guide explicitly supplies Miniforge paths for Linux x86-64/aarch64/ppc64le, Windows x86-64, and macOS x86-64/arm64. Optional JAX-backed performance extras support NVIDIA GPU acceleration.

### 22. Related Phenomena (OPTIONAL)
- Coronal Heating
- Coronal Mass Ejections
- Solar Corona
- Solar Flares
- **Source:** The JOSS paper describes AIA observations and aiapy's AIA analysis capabilities in the context of flare and coronal-mass-ejection initiation, quiescent coronal heating, and the solar corona.

### 23. Development Status (RECOMMENDED)
- Active
- **Source:** The repository has a stable current release (v0.12.1), commits after that release through source revision afc3db737a2f140ec8069126371866cec9e14be5 on 2026-07-24, active CI, current documentation, and scheduled tests.

### 24. Documentation (RECOMMENDED)
- https://aiapy.readthedocs.io/en/stable/
- **Source:** Preserved from the existing HSSI record and confirmed by README, `pyproject.toml`, PyPI, PyHC, and SoMEF.

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
  - **Funder Identifier:** https://ror.org/027ka1x80
- **Organization:** Science and Technology Facilities Council
  - **Funder Identifier:** https://ror.org/057g20z61
- **Source:** The project JOSS paper acknowledges NASA SDO/AIA, Hinode, HSR, and HMI support, plus an STFC grant. Full organization names and ROR identifiers were verified against HSSI/ROR.

### 26. Award Title (OPTIONAL)
- **Award Title:** NASA SDO/AIA contract to Lockheed Martin Solar and Astrophysics Laboratory
  - **Award Number:** NNG04EA00C
- **Award Title:** NASA Hinode program support
  - **Award Number:** Not found
- **Award Title:** NASA HSR grant
  - **Award Number:** 80NSSC19K0855
- **Award Title:** Science and Technology Facilities Council grant
  - **Award Number:** ST/S000240/1
- **Award Title:** NASA HMI contract to Stanford University
  - **Award Number:** NAS5-02139
- **Source:** Exact support statements and award numbers from the Acknowledgements section of the project JOSS paper. The acknowledgement proves NASA Hinode program support but publishes no specific award number. Award Number is RECOMMENDED rather than mandatory, and the user explicitly chose to retain this supported entry for completeness. No unsupported formal award titles were inferred beyond the descriptions given there.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1007/s11207-011-9804-8
- **Source:** Boerner et al. (2012), "Initial Calibration of the Atmospheric Imaging Assembly (AIA) on the Solar Dynamics Observatory (SDO)," is repeatedly cited by aiapy's response/calibration source and gallery as the scientific basis of implemented AIA calibration and wavelength-response calculations.

### 28. Related Datasets (OPTIONAL)
- National Aeronautics and Space Administration. SDO/AIA FITS Data. SDO HMI-AIA Joint Science Operations Center at Stanford. https://catalog.data.gov/dataset/sdo-aia-fits-data
- Galvez, R. et al. (2019). A Machine Learning Dataset Prepared From the NASA Solar Dynamics Observatory Mission. https://doi.org/10.3847/1538-4365/ab1005
- **Source:** aiapy directly processes SDO/AIA FITS data from JSOC. The maintained degradation example explicitly identifies the SDO Machine Learning Dataset as an aiapy correction use case; the dataset paper provides the persistent DOI requested by this field.

### 29. Related Software (OPTIONAL)
- https://www.lmsal.com/solarsoft/
- https://github.com/sunpy/drms
- **Source:** SolarSoftWare is the domain-specific IDL predecessor/counterpart whose `aia_prep`, PSF, calibration, and response routines aiapy reproduces or validates against. The JOSS paper and source identify the domain-specific `drms` client as the mechanism for retrieving AIA metadata and records from JSOC.
- **Note:** CHIANTI was considered but omitted because aiapy exposes response functions that other tools can combine with CHIANTI; no aiapy adapter or direct exchange is implemented. Generic scientific Python, plotting, packaging, testing, and JAX acceleration dependencies are intentionally excluded.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/sunpy/sunpy
- https://github.com/astropy/astropy
- **Source:** The JOSS paper explicitly states that aiapy is fully interoperable with SunPy and Astropy. Public APIs accept and return SunPy `AIAMap`/`Map`, `PixelPair`, and time-range objects and Astropy `Quantity`, `Time`, `QTable`, and `SkyCoord` objects. These are demonstrated data-model exchanges, not dependency-only claims.
- **Note:** Matplotlib, NumPy, JAX, pytest, and other generic infrastructure are excluded. `hissw` is test-only and is also excluded.

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** Atmospheric Imaging Assembly
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SDO/AIA
- **Instrument Name:** HMI
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SDO/HMI
- **Source:** aiapy is purpose-built to calibrate and analyze AIA data, and its registration implementation explicitly supports HMI maps. The controlled vocabulary contained a canonical bare SPASE resource and an `.html` duplicate for AIA; the bare identifier and its canonical row name are used. The unrelated "Magnetometers at Argentine Island" abbreviation collision is excluded by the repository's explicit SDO/AIA context. HMI uses the exact SPASE row above because aiapy's registration implementation explicitly supports HMI maps.
- **Replacement rationale:** The previous value displayed "Atmospheric Imaging Assembly (AIA)" without its identifier. The same instrument is now represented by the canonical controlled-row name and non-`.html` SPASE identifier; the bare name is not used.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Solar Dynamics Observatory
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SDO
- **Source:** aiapy is purpose-built for SDO/AIA data. The observatory uniquely matched one type-2 SPASE row in the target vocabulary, and the controlled-row name was copied verbatim.

### 33. Logo (OPTIONAL)
- Not found
- **Source:** The PyHC registry supplies an old GitLab static asset URL for `AIA_logo_small.jpg`, but that host no longer resolves in DNS and the broken URL is therefore omitted. The repository's `docs/_static/sdo.png` is an illustration of the SDO spacecraft rather than an aiapy software logo, so it was not misclassified.
