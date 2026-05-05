# HSSI Metadata Extraction Results

**Repository:** https://github.com/sunpy/ndcube
**Extraction Date:** 2025-12-02

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** Not found

**Note:** No concept DOI or version-specific DOI found for the software itself. The package has reference publications with DOIs (see field 14), but no DOI minted for the code repository on Zenodo or other DOI provider.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/sunpy/ndcube

**Source:** Repository URL

### 4. Software Functionality (MANDATORY)
**Values:**
- Coordinate Transforms
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Spectrogram
- Data Processing and Analysis:2D Slices
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:3D Graphics
- Data Visualization:Line Plots
- Data Visualization:Movies

**Source:** Analysis of JOSS paper, documentation, repository code structure, and PyHC keywords. ndcube provides:
- WCS-based coordinate transformations for astronomical data
- Multi-dimensional data manipulation (slicing, cropping, rebinning)
- Data visualization via matplotlib and mpl_animators
- Support for spectral and imaging data
- Analysis tools for coordinate-aware N-D arrays

### 5. Related Region (MANDATORY)
**Values:**
- Solar Environment
- Interplanetary Space

**Source:** JOSS paper and PyHC keywords. ndcube is used extensively for solar missions (SDO/AIA, IRIS, Hinode, Solar Orbiter, DKIST, PUNCH) and heliospheric data analysis.

### 6. Authors (MANDATORY)

**Source:** .zenodo.json file

1. **Author:** Daniel F. Ryan
   **ORCID:** https://orcid.org/0000-0001-8661-3825
   **Affiliation:** University College London, Mullard Space Science Laboratory (UCL/MSSL)

2. **Author:** Stuart J. Mumford
   **ORCID:** https://orcid.org/0000-0003-4217-4642
   **Affiliation:** Aperio Software Ltd.

3. **Author:** Nabil Freij
   **ORCID:** https://orcid.org/0000-0002-6253-082X
   **Affiliation:** SETI Institute & Lockheed Martin Solar and Astrophysics Laboratory

4. **Author:** Yash Sharma
   **ORCID:** https://orcid.org/0000-0002-7861-9677
   **Affiliation:** Meta Platforms Inc., UK

5. **Author:** Ankit Baruah
   **Affiliation:** Workato Gmbh, Germany

6. **Author:** Adwait Bhope
   **ORCID:** https://orcid.org/0000-0002-7133-8776
   **Affiliation:** Uptycs India Pvt. Ltd., India

7. **Author:** Samuel Bennett
   **ORCID:** https://orcid.org/0000-0001-6420-4422
   **Affiliation:** Aperio Software Ltd.

8. **Author:** Laura Hayes
   **ORCID:** https://orcid.org/0000-0002-6835-2390
   **Affiliation:** Dublin Institute of Advanced Studies (DIAS)

9. **Author:** Ricky O'Steen
   **ORCID:** https://orcid.org/0000-0002-2432-8946
   **Affiliation:** Space Telescope Science Institute, USA
   **Note:** ORCID in .zenodo.json appears to have typo "A0000" prefix, corrected to "0000"

10. **Author:** Baptiste Pellorce
    **Affiliation:** Claude Bernard Lyon 1 University, France & Institute of Theoretical Astrophysics, Norway

11. **Author:** Will Barnes
    **ORCID:** https://orcid.org/0000-0001-9642-6089
    **Affiliation:** NASA Goddard Space Flight Center, USA & American University, USA

12. **Author:** Drew Leonard
    **ORCID:** https://orcid.org/0000-0001-5270-7487
    **Affiliation:** Aperio Software Ltd.

13. **Author:** Mateo Inchaurrandieta

14. **Author:** Derek Homeier
    **ORCID:** https://orcid.org/0000-0002-8546-9128
    **Affiliation:** Aperio Software Ltd.

15. **Author:** Junyan Huo
    **ORCID:** https://orcid.org/0000-0002-5469-7697
    **Affiliation:** University College London

16. **Author:** David Stansby
    **ORCID:** https://orcid.org/0000-0002-1365-1908
    **Affiliation:** Advanced Research Computing Centre, University College London, UK

17. **Author:** Shane Maloney
    **ORCID:** https://orcid.org/0000-0002-4715-1805
    **Affiliation:** Trinity College Dublin & Dublin Institute for Advanced Studies

18. **Author:** J. Marcus Hughes
    **ORCID:** https://orcid.org/0000-0003-3410-7650
    **Affiliation:** Southwest Research Institute, USA

19. **Author:** Kris Akira Stern
    **ORCID:** https://orcid.org/0000-0003-1613-8947
    **Affiliation:** University of Hong Kong & University of London

20. **Author:** Andrew Robbertz
    **ORCID:** https://orcid.org/0009-0008-6857-0882
    **Affiliation:** General Dynamics Mission Systems, USA

21. **Author:** Aoife Maria Ryan

22. **Author:** Gabe Shafiq

23. **Author:** Roy Smart

24. **Author:** Mihail Bankov

25. **Author:** P. L. Lim
    **ORCID:** https://orcid.org/0000-0003-0079-4114
    **Affiliation:** Space Telescope Science Institute, USA

26. **Author:** Samuel J. Van Kooten
    **ORCID:** https://orcid.org/0000-0002-4472-8517
    **Affiliation:** Southwest Research Institute

27. **Author:** Sanvi Sharma

28. **Author:** Dan F-M

29. **Author:** Kritika Ranjan
    **ORCID:** https://orcid.org/0000-0001-5638-016X
    **Affiliation:** Jain (Deemed-to-be University), Bangalore

30. **Author:** Matthew J. West
    **ORCID:** https://orcid.org/0000-0002-0631-2393
    **Affiliation:** Southwest Research Institute, USA

31. **Author:** Shelbe Timothy

### 7. Software Name (MANDATORY)
**Value:** ndcube

**Source:** Repository name, pyproject.toml, PyHC registry

### 8. Description (MANDATORY)
**Value:** ndcube is an open-source SunPy affiliated package for manipulating, inspecting and visualizing multi-dimensional contiguous and non-contiguous coordinate-aware data arrays. It combines data, uncertainties, units, metadata, masking, and coordinate transformations into classes with unified slicing and generic coordinate transformations and plotting/animation capabilities. It is designed to handle data of any number of dimensions and axis types (e.g. spatial, temporal, spectral, etc.) whose relationship between the array elements and the real world can be described by World Coordinate System (WCS) translations.

**Source:** README.rst and .zenodo.json

### 9. Concise Description (OPTIONAL)
**Value:** A Python package for manipulating, inspecting and visualizing multi-dimensional contiguous and non-contiguous coordinate-aware data arrays.

**Source:** PyHC registry and .zenodo.json (under 200 characters)

### 10. Publication Date (RECOMMENDED)
**Value:** 2015-07-20

**Source:** Git repository initial commit date

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Note:** No DOI has been minted via Zenodo for the software, so GitHub is listed as the repository host.

### 12. Version (RECOMMENDED)
- **Version Number:** v2.3.4
- **Version Date:** 2025-10-06
- **Version Description:** Not found - CHANGELOG.rst does not include v2.3.4 details yet (latest in changelog is v2.3.0 from 2025-01-14)
- **Version PID:** Not found

**Source:** Git tags for version number and date; CHANGELOG.rst

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** pyproject.toml (requires-python = ">=3.11")

### 14. Reference Publication (RECOMMENDED)
**Values:**
- https://doi.org/10.21105/joss.05296 (JOSS paper: "ndcube: Manipulating N-dimensional Astronomical Data in Python", 2023)
- https://doi.org/10.3847/1538-4357/ace0bd (ApJ paper: "A Unified Framework for Manipulating N-dimensional Astronomical Data and Coordinate Transformations in Python: The NDCube 2 & Astropy APE-14 WCS APIs", 2023)

**Source:** README.rst badges, JOSS paper metadata, acknowledging.rst

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://opensource.org/licenses/BSD-2-Clause

**Source:** LICENSE.rst and .zenodo.json

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- coordinates
- data analysis
- data container
- heliosphere
- plotting
- solar
- astronomy
- Python
- WCS
- World Coordinate System
- spectral data
- multi-dimensional data
- NDCube
- SunPy
- astrophysics

**Source:** PyHC registry keywords, JOSS paper tags, repository topics

### 17. Data Sources (OPTIONAL)
**Values:**
- Observatory/Mission-specific

**Note:** ndcube is used with data from various solar and heliophysics missions including SDO/AIA, IRIS, Hinode, Solar Orbiter, DKIST, JWST, and PUNCH.

**Source:** JOSS paper section "Community Applications of ndcube"

### 18. Input File Formats (RECOMMENDED)
**Values:**
- FITS
- HDF5
- netCDF3/4
- ASDF

**Source:** Analysis of pyproject.toml dependencies (asdf support), examples (FITS file reading), and general astronomical data format support. ndcube works with any array-like object with .dtype and .shape attributes (NumPy, Dask, CuPy).

### 19. Output File Formats (RECOMMENDED)
**Values:**
- FITS
- HDF5
- ASDF

**Note:** Output formats depend on the underlying array storage and serialization options. ndcube can work with various array backends.

**Source:** Code analysis and ASDF support in pyproject.toml

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows
- OS Independent

**Source:** Python package with no OS-specific dependencies; PyPI distribution indicates cross-platform compatibility

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- CPU Independent

**Note:** Pure Python package with dependencies that support multiple architectures. Can leverage GPU via CuPy backend for array operations.

**Source:** JOSS paper mentions CuPy support for GPU operations; pure Python implementation

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Solar Corona
- Solar Flares
- Coronal Mass Ejections

**Note:** While ndcube is a general-purpose tool for coordinate-aware N-D data, it is extensively used in solar physics for analyzing phenomena observable in solar imaging and spectral data.

**Source:** JOSS paper and typical use cases from affiliated solar missions

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** PyHC registry rating (all "Good" ratings), recent commits (v2.3.4 released October 2025), active development visible in git history

### 24. Documentation (RECOMMENDED)
**Value:** https://docs.sunpy.org/projects/ndcube

**Source:** README.rst, pyproject.toml, PyHC registry

### 25. Funder (OPTIONAL)
**Values:**
1. **Organization:** NASA
   **Funder Identifier:** https://ror.org/027ka1x80

2. **Organization:** Daniel K. Inouye Solar Telescope

3. **Organization:** Solar Orbiter/SPICE

**Source:** JOSS paper Acknowledgements section

### 26. Award Title (OPTIONAL)
**Values:**
1. **Award Title:** NASA's Heliophysics Data Environment Enhancement program
   **Award Number:** Not found

2. **Award Title:** Solar Orbiter/SPICE
   **Award Number:** 80NSSC19K1000

**Source:** JOSS paper Acknowledgements section

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Values:**
- https://doi.org/10.21105/joss.05296 (ndcube JOSS paper, 2023)
- https://doi.org/10.3847/1538-4357/ace0bd (NDCube 2 & APE-14 WCS APIs paper, ApJ, 2023)

**Note:** These are also listed as Reference Publications (field 14), as they describe the software itself.

**Source:** JOSS paper, acknowledging.rst

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Note:** ndcube is a general-purpose tool that works with various datasets from different missions. No specific datasets are bundled or required.

### 29. Related Software (OPTIONAL)
**Values:**
- https://github.com/sunpy/sunpy (SunPy - parent project)
- https://github.com/astropy/astropy (Astropy - WCS and core functionality dependency)
- https://github.com/spacetelescope/gwcs (gWCS - generalized WCS implementation)
- https://github.com/astropy/specutils (specutils - depends on ndcube)
- https://github.com/spacetelescope/jdaviz (jdaviz - depends on ndcube)
- https://github.com/sunpy/sunraster (sunraster - depends on ndcube)
- https://github.com/LM-SAL/irispy-lmsal (irispy-lmsal - depends on ndcube)
- https://github.com/USNavalResearchLaboratory/eispac (EISPAC - depends on ndcube)
- https://github.com/dask/dask (Dask - array backend support)
- https://github.com/cupy/cupy (CuPy - GPU array backend support)
- https://github.com/astropy/reproject (reproject - reprojection functionality)
- https://matplotlib.org (Matplotlib - visualization backend)

**Source:** JOSS paper "Community Applications" section, pyproject.toml dependencies, README.rst

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://github.com/sunpy/sunpy (SunPy)
- https://github.com/astropy/astropy (Astropy)
- https://github.com/astropy/specutils (specutils)
- https://github.com/spacetelescope/jdaviz (jdaviz)
- https://github.com/sunpy/sunraster (sunraster)
- https://github.com/LM-SAL/irispy-lmsal (irispy-lmsal)
- https://github.com/dask/dask (Dask)
- https://github.com/matplotlib/matplotlib (Matplotlib)

**Source:** JOSS paper and dependency analysis; these packages can be used together without errors in the same environment

### 31. Related Instruments (OPTIONAL)
**Values:**
1. **Instrument Name:** AIA (Atmospheric Imaging Assembly) on SDO
   **Instrument Identifier:** Not found

2. **Instrument Name:** IRIS (Interface Region Imaging Spectrograph)
   **Instrument Identifier:** Not found

3. **Instrument Name:** XRT (X-Ray Telescope) on Hinode
   **Instrument Identifier:** Not found

4. **Instrument Name:** SPICE on Solar Orbiter
   **Instrument Identifier:** Not found

5. **Instrument Name:** DKIST instruments
   **Instrument Identifier:** Not found

**Source:** JOSS paper "Community Applications" section lists these instruments as using packages that depend on ndcube

### 32. Related Observatories (OPTIONAL)
**Values:**
1. **Observatory Name:** SDO (Solar Dynamics Observatory)

2. **Observatory Name:** IRIS (Interface Region Imaging Spectrograph)

3. **Observatory Name:** Hinode

4. **Observatory Name:** Solar Orbiter

5. **Observatory Name:** DKIST (Daniel K. Inouye Solar Telescope)

6. **Observatory Name:** JWST (James Webb Space Telescope)

7. **Observatory Name:** PUNCH (Polarimeter to UNify the Corona and Heliosphere)

**Source:** JOSS paper "Community Applications" section

### 33. Logo (OPTIONAL)
**Value:** https://raw.githubusercontent.com/sunpy/ndcube/master/docs/logo/ndcube.png

**Source:** PyHC registry and acknowledging.rst

---

## Metadata Sources Summary

**Priority Order Used:**
1. **PyHC metadata** - Used for keywords, contact, logo, docs URL (manually curated, most trustworthy)
2. **Repository files** - .zenodo.json, pyproject.toml, LICENSE.rst, README.rst, JOSS paper files (primary source for authors, description, license, dependencies)
3. **Git history** - Used for version information and publication date
4. **JOSS paper** - Used for detailed functionality description, related software/instruments, funders
5. **SoMEF** - Not heavily relied upon due to large output size and potential unreliability

**Notes:**
- No software DOI exists for ndcube (no Zenodo integration detected)
- The package has two reference publications (JOSS and ApJ papers)
- Extensive author list from .zenodo.json
- Active development with "Good" ratings across all PyHC quality metrics
- Part of the SunPy ecosystem
- Used by multiple solar and space physics missions and instruments
