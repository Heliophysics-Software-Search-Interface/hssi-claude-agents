# HSSI Metadata Extraction Results

**HSSI Software ID:** 8e349bce-5860-4c0b-9ee9-ebb684574262
**Repository:** https://github.com/wtbarnes/fiasco
**Source Revision:** 1a1965066b192360bdc3681e128dec91d1a4ead0
**Extraction Date:** 2026-07-26
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** To be filled by actual submitter
- **Submitter Email:** To be filled by actual submitter
- **Source:** The HSSI view record does not expose submitter information.

### 2. Persistent Identifier (RECOMMENDED)
- https://doi.org/10.5281/zenodo.7504257
- **Source:** Existing HSSI record, repository DOI badge, DataCite, and Zenodo. This is the concept DOI for all fiasco releases.

### 3. Code Repository (MANDATORY)
- https://github.com/wtbarnes/fiasco
- **Source:** Existing HSSI record, git remote, repository metadata, Zenodo, and PyHC registry.

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Processing
- Models and Simulations
- Models and Simulations:Physics-Based
- Models and Simulations:Theory
- **Source:** Identity-aware union retaining the existing HSSI `Data Processing and Analysis` value and adding current public capabilities. `fiasco.Ion`, `fiasco.Element`, and `fiasco.IonCollection` expose atomic-data analysis, level populations, equilibrium ionization, line ratios, emissivities, intensities, ionization/recombination rates, continua, radiative losses, and synthetic spectra. `fiasco.io.Parser`, `download_dbase`, and `build_hdf5_dbase` retrieve and transform the raw CHIANTI ASCII database into HDF5. The physics-based/theory classifications are supported by the implemented atomic-rate, cross-section, Gaunt-factor, continuum-emission, and ionization-equilibrium calculations.
- **Note:** Data Visualization was considered but not selected: plotting occurs in documentation examples through Matplotlib, while fiasco's public APIs return scientific arrays/tables rather than implementing plot methods. No mission-related, coordinate-transform, or server/environment functionality was found.

### 5. Related Region (MANDATORY)
- Solar Environment
- Earth Atmosphere
- Interplanetary Space
- Corona
- Solar Wind
- **Source:** Identity-aware union retaining the existing HSSI `Solar Environment` value. The curated PyHC record additionally classifies fiasco for `ionosphere_thermosphere_mesosphere`, supporting Earth Atmosphere. The repository's developer-maintained works-citing list demonstrates use for solar-wind and coronal-mass-ejection charge-state modeling in interplanetary space.
- **Evidence, Corona:** Every `fiasco.Ion` defaults to the Feldman solar-coronal abundance set (`fiasco/ions.py:65`), and the AIA response guide explicitly uses coronal abundances while calculating a solar EUV response (`examples/user_guide/aia_response.py:44`).
- **Evidence, Solar Wind:** The developer-maintained citing bibliography includes Rivera et al. (2025), “Differentiating the Acceleration Mechanisms in the Slow and Alfvénic Slow Solar Wind” (`docs/works_citing.bib:80`), the same curated usage source already used in this dossier to support interplanetary-space charge-state modeling.

### 6. Authors (MANDATORY)
- **Author:** Will Barnes
  - **Author Identifier:** https://orcid.org/0000-0001-9642-6089
  - **Affiliations:**
    - American University — https://ror.org/052w4zt36
    - Department of Physics, American University — Identifier not found
    - Goddard Space Flight Center — https://ror.org/0171mag52
- **Author:** Nabil Freij
  - **Author Identifier:** https://orcid.org/0000-0002-6253-082X
  - **Affiliations:**
    - Lockheed Martin Solar and Astrophysics Laboratory — Identifier not found
    - SETI Institute — https://ror.org/02dxgk712
    - Bay Area Environmental Research Institute — https://ror.org/024tt5x58
- **Author:** Laura Hayes
  - **Author Identifier:** https://orcid.org/0000-0002-6835-2390
  - **Affiliations:**
    - Dublin Institute for Advanced Studies — https://ror.org/051sx6d27
    - European Space Research and Technology Centre — https://ror.org/03h3jqn23
- **Author:** Stuart J. Mumford
  - **Author Identifier:** https://orcid.org/0000-0003-4217-4642
  - **Affiliations:**
    - Aperio Software Ltd. — Identifier not found
    - University of Sheffield — https://ror.org/05krs5044
- **Author:** Nicholas A. Murphy
  - **Author Identifier:** https://orcid.org/0000-0001-6628-8033
  - **Affiliations:**
    - Center for Astrophysics, Harvard & Smithsonian — https://ror.org/03c3r2d17
    - Smithsonian Astrophysical Observatory — https://ror.org/04mh52z70
    - Smithsonian Institution — https://ror.org/01pp8nd67
- **Author:** Jeffrey Reep
  - **Author Identifier:** https://orcid.org/0000-0003-4739-1152
  - **Affiliations:**
    - University of Hawaii at Manoa — https://ror.org/01wspgy28
- **Author:** David Stansby
  - **Author Identifier:** https://orcid.org/0000-0002-1365-1908
  - **Affiliations:**
    - Advanced Research Computing Centre, University College London, UK — Identifier not found
    - Department of Mechanical Engineering, University College London — Identifier not found
    - Imperial College London — https://ror.org/041kmwe10
    - University College London — https://ror.org/02jx3x895
- **Author:** Jacob Parker
  - **Author Identifier:** https://orcid.org/0000-0001-8732-8284
  - **Affiliations:**
    - Montana State University — https://ror.org/02w0trx84
- **Source:** Identity-aware union of the existing HSSI authors/affiliations (matched by ORCID, then name), the current repository `.zenodo.json`, and the latest Zenodo/DataCite version metadata. No seeded author or affiliation was removed. The current repository adds Jacob Parker. It also adds Bay Area Environmental Research Institute for Nabil Freij; that current affiliation is retained alongside the seeded SETI Institute affiliation. ROR identifiers for the two newly added organizations and the European Space Research and Technology Centre were resolved through the ROR API.

### 7. Software Name (MANDATORY)
- fiasco
- **Source:** Existing HSSI record, repository README, package metadata, Zenodo/DataCite, SoMEF, and PyHC registry.

### 8. Description (MANDATORY)
fiasco provides a Python interface to CHIANTI, an atomic database used primarily for astrophysical spectroscopy. It exposes high-level representations of ions, elements, levels, and transitions; parses and converts raw CHIANTI ASCII data into an HDF5 database; and computes common atomic-plasma quantities including level populations, ionization and recombination rates, contribution functions, emissivities, spectra, continuum emission, radiative losses, and equilibrium ionization. Its documented examples use those rates to calculate non-equilibrium ionization.

- **Source:** Evidence-backed expansion of the existing HSSI/Zenodo description using the current README, documentation, public API, examples, and tests. It retains the submitted description's core wording while adding the repository-documented calculations and data-conversion capabilities.

### 9. Concise Description (OPTIONAL)
fiasco provides a Python interface to the CHIANTI, an atomic database used primarily for astrophysical spectroscopy.

- **Source:** Existing HSSI record and current Zenodo metadata; retained verbatim to preserve submitted editorial wording. It is 122 characters.

### 10. Publication Date (RECOMMENDED)
- 2017-08-10
- **Source:** GitHub repository creation timestamp reported by the GitHub API and SoMEF (`2017-08-10T04:03:15Z`), corroborated by the first repository commits on 2017-08-09/10.
- **Note:** This replaces the seeded `2025-08-14`, which is the release date of the formerly recorded v0.6.1 rather than fiasco's initial publication date. The first tagged/PyPI stable release, v0.1.0, followed on 2023-01-04.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** Existing HSSI record and Zenodo/DataCite metadata.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.8.1
- **Version Date:** 2026-03-10
- **Version Description:** Adds the developer-maintained works-citing list, fixes an individual-level-label bug, and adds an option to disable the database-build progress bar.
- **Version PID:** https://doi.org/10.5281/zenodo.18942693
- **Source:** Current GitHub latest release, PyPI 0.8.1 files, DataCite concept record, and Zenodo latest-version record. All independently identify v0.8.1 as the latest stable release on 2026-07-26.
- **Note:** This supersedes the stale seeded `fiasco - v0.6.1`. The current `main` branch is post-release development tagged `v0.9dev`, not a stable release. The repository's generated `fiasco/CITATION.rst` still names v0.8.0 and is therefore stale relative to GitHub, PyPI, DataCite, and Zenodo.

### 13. Programming Language (RECOMMENDED)
- IDL
- Python 3.x
- **Source:** Identity-aware union retaining both existing HSSI values. Python 3.x is the package implementation and declared runtime language. IDL is materially represented by the maintained CHIANTI-IDL comparison suite and supporting procedures; GitHub/SoMEF language metadata also reports both.

### 14. Reference Publication (RECOMMENDED)
- Not found
- **Source:** The repository requests citation of the version-specific Zenodo software DOI and the CHIANTI database, but does not identify a publication whose subject is the fiasco software itself.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause
- **Source:** Existing HSSI record, repository `LICENSE.rst`, `.zenodo.json`, GitHub license API, and Zenodo/DataCite. The file contains all three BSD conditions.
- **Note:** SoMEF's code-parser also proposed BSD-2-Clause, but that conflicts with the actual license text, GitHub, Zenodo, and the existing HSSI value and was rejected.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- Astronomy
- Astrophysics
- Atomic Data
- Atomic Physics
- Chianti
- Chianti Atomic Database
- Heliophysics
- Plasma Physics
- Python
- Science
- Solar
- Solar Physics
- Spectroscopy
- Emission spectroscopy
- Extreme ultraviolet
- Ionization equilibrium
- Non-equilibrium ionization
- Radiative loss
- Solar wind
- Ionosphere
- Thermosphere
- Mesosphere
- **Source:** Identity-aware union retaining every existing HSSI keyword and adding current package-metadata, PyHC, documentation, public-API, and developer-curated usage concepts.

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- **Source:** `fiasco.util.download_dbase` retrieves versioned CHIANTI database archives directly from `download.chiantidatabase.org`; users can also provide an existing local CHIANTI database tree.

### 18. Input File Formats (RECOMMENDED)
- ascii
- HDF5
- **Source:** The public parser reads the raw CHIANTI ASCII database, and the public data layer reads the generated HDF5 database.

### 19. Output File Formats (RECOMMENDED)
- HDF5
- **Source:** `fiasco.util.build_hdf5_dbase` converts parsed CHIANTI data into a single HDF5 database.

### 20. Operating System (RECOMMENDED)
- Operating System Independent
- Linux
- Mac
- Windows
- **Source:** The package declares `Operating System :: OS Independent`; the current CI workflow explicitly tests Linux, macOS, and Windows.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent
- **Source:** fiasco is published as a `py3-none-any` wheel and contains no architecture-specific implementation. Its compiled scientific dependencies remain responsible for their own platform support.

### 22. Related Phenomena (OPTIONAL)
- Coronal Heating
- Coronal Mass Ejections
- Solar Corona
- Solar Flares
- Solar Wind
- X-ray emission
- **Source:** Current CHIANTI/fiasco documentation covers solar-coronal abundances, ultraviolet/X-ray spectroscopy, emission spectra, and ionization calculations. The documented non-equilibrium-ionization example directly models a rapid coronal heating and cooling episode using fiasco rates, and the public API computes radiative losses used in coronal-heating modeling. The repository's developer-maintained works-citing list demonstrates fiasco use for coronal-mass-ejection charge-state modeling, solar-flare studies, and slow-solar-wind charge-state work (`docs/works_citing.bib:80`).
- **Note:** `Coronal Holes` was weighed during extraction and not selected because the repository does not establish it as a direct fiasco science target — but it was never actually available: it appeared only in a stale documentation list and has never been a row in the HSSI Phenomena vocabulary (noted 2026-08-24), so it must not be re-proposed as a value here regardless of evidence.

### 23. Development Status (RECOMMENDED)
- Active
- **Source:** The latest stable release is v0.8.1 (2026-03-10), and the GitHub `main` branch has continued active development through revision `1a1965066b192360bdc3681e128dec91d1a4ead0` on 2026-07-23.

### 24. Documentation (RECOMMENDED)
- https://fiasco.readthedocs.io
- **Source:** Existing HSSI record, repository README and package metadata, SoMEF, and PyHC registry.

### 25. Funder (OPTIONAL)
- Not found
- **Source:** No funder is identified in the current repository, `.zenodo.json`, Zenodo/DataCite record, package metadata, or documentation. Author affiliations were not treated as funders.

### 26. Award Title (OPTIONAL)
- Not found
- **Source:** No award title or award number is identified in the current repository or Zenodo/DataCite metadata.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.3847/1538-4357/ae019d
- https://doi.org/10.48550/arXiv.2512.09234
- https://doi.org/10.1038/s41550-025-02747-9
- https://doi.org/10.3847/1538-4357/aceef8
- https://doi.org/10.3847/1538-4357/ada699
- https://doi.org/10.1007/s11207-025-02561-6
- https://doi.org/10.1051/0004-6361/202554166
**Evidence-only citation (intentionally not an HSSI Field 27 value):** Hart, S. T. (2024). Understanding the Origins and Acceleration Mechanisms of 3He-Rich Solar Energetic Particle Events [Doctoral dissertation, The University of Texas at San Antonio]. https://grad.space.swri.edu/please-join-us-in-congratulating-samuel-hart-our-newest-phd-as-he-successfully-defended-his-dissertation/
- **Source:** The seven emitted Field 27 values come from the repository's current developer-maintained `docs/works_citing.bib` list, supplemented with the final peer-reviewed DOI for the Varesano et al. article. The Hart dissertation citation and official SwRI/University of Texas at San Antonio institutional permalink are preserved above as evidence only.
- **Note:** `https://doi.org/10.1051/0004-6361/202554166` replaces the repository's arXiv preprint DOI for the same Varesano et al. work; only the final journal DOI is retained.
- **User decision:** The Hart dissertation URL is 133 characters and is intentionally excluded from the HSSI Field 27 values because the current HSSI backend stores a related publication URL in a 128-character `RelatedItem.name` field. Future agents must not re-add this URL to the emitted Field 27 values unless backend compatibility changes and the user explicitly revisits this decision.

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.3847/1538-4357/ad6765
- **Source:** fiasco is specifically an interface to and analysis layer for the CHIANTI atomic database. This DOI is the repository-cited paper describing CHIANTI Version 11, the newest database generation supported and tested by the current source.

### 29. Related Software (OPTIONAL)
- https://www.chiantidatabase.org/chianti_download.html
- https://github.com/chianti-atomic/ChiantiPy
- https://github.com/PlasmaPy/PlasmaPy
- **Source:** CHIANTI IDL is the domain counterpart against which fiasco's calculations are explicitly compared and shares the same database; the official CHIANTI site identifies ChiantiPy as the alternative Python interface; PlasmaPy is a required domain-specific dependency used throughout fiasco's public ion/element abstractions.
- **Note:** Generic scientific-Python and tooling dependencies were excluded under the Field 29 relevance gate.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/astropy/astropy
- https://github.com/LM-SAL/aiapy
- https://www.chiantidatabase.org/chianti_download.html
- **Source:** Specific demonstrated exchanges, not dependency presence: fiasco's public API accepts and returns Astropy `Quantity` and `QTable` objects; the maintained AIA example combines a fiasco contribution function with an aiapy instrument-response object; and fiasco parses the same CHIANTI database used by the IDL package while its maintained comparison suite exchanges and validates corresponding IDL/Python calculation outputs.
- **Note:** NumPy, SciPy, Matplotlib, h5py, ASDF, hissw, and other generic/internal/test dependencies were considered but excluded. SunPy appears only through documentation cross-references or transitive/example context, with no direct demonstrated fiasco exchange.

### 31. Related Instruments (OPTIONAL)
- Not found
- **Source:** fiasco is instrument-agnostic atomic-data and modeling software.
- **Note:** The Atmospheric Imaging Assembly was considered because one documentation example combines fiasco with aiapy, but the example imports aiapy for all instrument-specific response behavior. Under the designed-to-support relevance gate, the instrument belongs to aiapy rather than fiasco, so no controlled-vocabulary instrument value is emitted.

### 32. Related Observatories (OPTIONAL)
- Not found
- **Source:** fiasco is observatory- and mission-agnostic.
- **Note:** The Solar Dynamics Observatory was considered through the same AIA/aiapy example and excluded as example-only ecosystem context. Solar Orbiter and Parker Solar Probe mentions in works that cite fiasco demonstrate scientific use, not mission-specific data support, so no controlled-vocabulary observatory value is emitted.

### 33. Logo (OPTIONAL)
- https://raw.githubusercontent.com/wtbarnes/fiasco/1a1965066b192360bdc3681e128dec91d1a4ead0/docs/_static/fiasco-logo.png
- **Source:** Repository `docs/_static/fiasco-logo.png`; the URL is pinned to the extracted full source revision and was verified to return HTTP 200 with `image/png`.
