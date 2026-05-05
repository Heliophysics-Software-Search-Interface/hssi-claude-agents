# HSSI Metadata Extraction Results

**Repository:** https://github.com/PlasmaPy/PlasmaPy
**Extraction Date:** 2026-04-24

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.1436011

*Source: CITATION.cff cross-referenced with Zenodo API (this is the concept DOI for all versions; current latest version DOI is 10.5281/zenodo.18706665).*

### 3. Code Repository (MANDATORY)
https://github.com/PlasmaPy/PlasmaPy

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:Magnetic Null Finding
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:Line Plots
- Data Visualization:2D Graphics
- Models and Simulations
- Models and Simulations:First Principles
- Models and Simulations:Forward-Fitting
- Models and Simulations:MHD
- Models and Simulations:Physics-Based
- Models and Simulations:Theory

*Source: Manual examination of `src/plasmapy/` subpackages.*
- `plasmapy.particles` — particle/atomic data, ionization states (Analysis).
- `plasmapy.formulary` — extensive plasma physics formulas (NRL Plasma Formulary), including frequencies, lengths, speeds, drifts, collisions, dielectric tensor, distributions, dimensionless parameters (Theory, Physics-Based, First Principles).
- `plasmapy.dispersion` — analytical (Stix cold-plasma, MHD waves) and numerical (Hollweg, kinetic Alfvén) dispersion solvers (MHD, Theory, Physics-Based).
- `plasmapy.simulation` — particle tracker, Boris/Relativistic Boris integrators, Yee CFL constraints (First Principles, Physics-Based).
- `plasmapy.diagnostics` — Thomson scattering analysis (`spectral_density` computes scattered power spectra; `spectral_density_model` returns an `lmfit.Model` for fitting Thomson spectra), Langmuir probe analysis, charged particle radiography (Analysis, Energy Spectra, Forward-Fitting).
- `plasmapy.formulary.radiation.thermal_bremsstrahlung` — computes the bremsstrahlung emission spectrum for a Maxwellian plasma (Energy Spectra).
- `plasmapy.analysis` — fit functions, swept Langmuir analysis, time series conditional averaging, 3D magnetic null point finding (Analysis, Time Series Analysis, Magnetic Null Finding).
- `plasmapy.plasma` — plasma grids (Cartesian/non-uniform), 1D/cylindrical equilibria, OpenPMD HDF5 reader (general analysis).
- Plotting (`matplotlib`) is used for visualization in `plasmapy.diagnostics.langmuir` and throughout example notebooks (Line Plots, 2D Graphics).

### 5. Related Region (MANDATORY)
- Solar Environment
- Interplanetary Space
- Earth Magnetosphere

*Source: Manual examination + PyHC keywords. PlasmaPy provides general plasma physics functionality applicable to the solar atmosphere/corona, the solar wind (`formulary.collisions.helio` is explicitly for "solar wind"), and magnetospheric/space plasmas. PyHC keywords list "heliosphere", "solar", "magnetosphere". Also used in laboratory/fusion contexts which are not HSSI regions.*

### 6. Authors (MANDATORY)

The PlasmaPy CITATION.cff lists 157 contributing authors. The recommended group attribution is "PlasmaPy Community"; primary maintainers and lead developers are listed individually below. The complete list of contributors with ORCIDs and affiliations is in `CITATION.cff` in the repository.

- **Author:** PlasmaPy Community
  - *Affiliation:* (collective; see CITATION.cff)

- **Author:** Nicholas A. Murphy
  - *Author Identifier:* https://orcid.org/0000-0001-6628-8033
  - *Affiliation:* Center for Astrophysics | Harvard & Smithsonian

- **Author:** Erik T. Everson
  - *Author Identifier:* https://orcid.org/0000-0001-6079-8307
  - *Affiliation:* University of California, Los Angeles (UCLA)

- **Author:** Dominik Stańczak-Marikin
  - *Author Identifier:* https://orcid.org/0000-0001-6291-8843
  - *Affiliation:* (independent contributor)

- **Author:** Peter V. Heuer
  - *Author Identifier:* https://orcid.org/0000-0001-5050-6606
  - *Affiliation:* University of Rochester

- **Author:** Pawel M. Kozlowski
  - *Author Identifier:* https://orcid.org/0000-0001-6849-3612
  - *Affiliation:* Los Alamos National Laboratory

- **Author:** Elliot Johnson
  - *Author Identifier:* https://orcid.org/0000-0003-2892-6924
  - *Affiliation:* University of Delaware

- **Author:** Ritiek Malhotra
  - *Affiliation:* Chandigarh University

- **Author:** David Schaffner
  - *Author Identifier:* https://orcid.org/0000-0002-9180-6565
  - *Affiliation:* Bryn Mawr College

- **Author:** Steve Vincena
  - *Author Identifier:* https://orcid.org/0000-0002-6468-5710
  - *Affiliation:* University of California, Los Angeles (UCLA)

*Source: CITATION.cff (top-listed maintainers/lead authors).*

### 7. Software Name (MANDATORY)
PlasmaPy

### 8. Description (MANDATORY)
PlasmaPy is an open source, community-developed Python package for plasma research and education. It is intended to contain core functionality needed by plasma scientists across disciplines — analogous to what Astropy provides for astronomy. PlasmaPy provides object-oriented and functional interfaces for representing and accessing particle data (`plasmapy.particles`); a comprehensive `plasmapy.formulary` subpackage implementing many common plasma parameter formulas drawn from the NRL Plasma Formulary (frequencies, lengths, speeds, drifts, collisions, dielectric and dimensionless quantities, distribution functions, quantum and relativistic plasma physics); and the `plasmapy.dispersion` subpackage for analytical (Stix cold-plasma, MHD wave) and numerical (Hollweg, kinetic Alfvén) plasma dispersion relations and the plasma dispersion function. The `plasmapy.diagnostics` subpackage provides analysis routines for Thomson scattering, swept Langmuir probe characteristics, and synthetic charged particle (proton) radiography, while `plasmapy.analysis` provides utilities for fit functions, conditional averaging of time series, and 3D magnetic null point finding. The `plasmapy.simulation` subpackage offers a general particle tracker with Boris and relativistic Boris integrators, and `plasmapy.plasma` defines 1D and cylindrical MHD equilibria, generic plasma classes, and structured/unstructured Cartesian grids, including a reader for OpenPMD HDF5 files. PlasmaPy uses `astropy.units` extensively to enforce physical-unit correctness on all inputs and outputs.

*Source: README.md, CITATION.cff abstract, and DataCite metadata, augmented from manual repository examination.*

### 9. Concise Description (OPTIONAL)
PlasmaPy is an open source, community-developed Python package for plasma research and education, providing core particle, formulary, dispersion, diagnostics, and simulation functionality.

### 10. Publication Date (RECOMMENDED)
2018-04-29

*Source: Earliest git tag (v0.1.0) in the repository.*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://ror.org/01ggx4157

*Source: DataCite API for the concept DOI.*

### 12. Version (RECOMMENDED)
- **Version Number:** 2026.2.0
- **Version Date:** 2026-02-20
- **Version Description:** Latest stable release as recorded in CITATION.cff. See https://docs.plasmapy.org/en/stable/whatsnew/index.html for changelog.
- **Version PID:** https://doi.org/10.5281/zenodo.18706665

*Source: CITATION.cff and docs/about/citation.rst.*

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source: pyproject.toml (`requires-python = ">=3.12"`); README badges; SoMEF.*

### 14. Reference Publication (RECOMMENDED)
Not found

*PlasmaPy does not have a separate JOSS or peer-reviewed reference publication. The canonical citation is the version-specific Zenodo record (see Version PID).*

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause

*Source: LICENSE.md and pyproject.toml.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- plasma
- plasma physics
- plasma science
- heliophysics
- solar physics
- space plasmas
- space physics
- physics
- astronomy
- astrophysics
- atomic physics
- particles
- fusion
- high-energy-density physics
- science
- python
- open source software
- Thomson scattering
- proton radiography
- plasma diagnostics
- Langmuir probes
- plasma parameters
- plasma astrophysics

*Source: pyproject.toml keywords, DataCite subjects, GitHub repo topics (via SoMEF), and PyHC entry.*

### 17. Data Sources (OPTIONAL)
- Other

*PlasmaPy is not primarily a data-access tool; users supply their own data. The OpenPMD HDF5 reader can ingest simulation output files, but no remote data archive client is exposed.*

### 18. Input File Formats (RECOMMENDED)
- HDF5

*Source: `plasmapy.plasma.sources.openpmd_hdf5` provides an `HDF5Reader` for OpenPMD-formatted HDF5 plasma simulation files. `h5py` is also used for reading saved synthetic radiography data.*

### 19. Output File Formats (RECOMMENDED)
- HDF5

*Source: `plasmapy.simulation.particle_tracker.save_routines` and `plasmapy.diagnostics.charged_particle_radiography.synthetic_radiography` write outputs in HDF5 via `h5py`.*

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

*Source: `pyproject.toml` classifier "Operating System :: OS Independent" and `.github/workflows/installability.yml` test matrix `[windows-latest, macos-latest, ubuntu-latest]`.*

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64

*Source: GitHub macOS-latest runners are Apple Silicon arm64 since 2024. Default GitHub-hosted Linux/Windows runners are x86-64. Pure Python package is also broadly portable.*

### 22. Related Phenomena (OPTIONAL)
Not found

*PlasmaPy is general-purpose plasma physics infrastructure rather than software dedicated to specific phenomena from the controlled vocabulary (Coronal Heating, Coronal Holes, CMEs, Solar Corona, Solar Flares, X-ray emission). It can be applied to many of these phenomena indirectly.*

### 23. Development Status (RECOMMENDED)
Active

*Source: Frequent commits, CI badges, regular releases (most recent: 2026.2.0 on 2026-02-20). Listed in PyHC core packages.*

### 24. Documentation (RECOMMENDED)
https://docs.plasmapy.org

*Source: README.md, pyproject.toml, .readthedocs.yml, PyHC registry entry.*

### 25. Funder (OPTIONAL)
- **Organization:** U.S. National Science Foundation
  - *Funder Identifier:* https://ror.org/021nxhr62

- **Organization:** United States Department of Energy
  - *Funder Identifier:* https://ror.org/01bj3aw27

- **Organization:** National Aeronautics and Space Administration (NASA)
  - *Funder Identifier:* https://ror.org/027ka1x80

- **Organization:** Smithsonian Institution
  - *Funder Identifier:* https://ror.org/01pp8nd67

*Source: README.md acknowledgments section and DataCite fundingReferences.*

### 26. Award Title (OPTIONAL)
- **Award Title:** Collaborative Research: Frameworks: An open source software ecosystem for plasma physics
  - *Award Number:* 1931388
- **Award Title:** Collaborative Research: Frameworks: An open source software ecosystem for plasma physics
  - *Award Number:* 1931393
- **Award Title:** Collaborative Research: Frameworks: An open source software ecosystem for plasma physics
  - *Award Number:* 1931429
- **Award Title:** Collaborative Research: Frameworks: An open source software ecosystem for plasma physics
  - *Award Number:* 1931435
- **Award Title:** Collaborative Research: The Evolution of Magnetic Skeletons During 3D Magnetic Reconnection
  - *Award Number:* DE-SC0016363
- **Award Title:** NASA Heliophysics Data Environment Enhancements (HDEE)
  - *Award Number:* 80NSSC20K0174

*Source: DataCite fundingReferences and DataCite "Other" description.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

*No reference publication has been minted; PlasmaPy is cited via its Zenodo record.*

### 28. Related Datasets (OPTIONAL)
Not found

### 29. Related Software (OPTIONAL)
- https://github.com/astropy/astropy (Astropy — core dependency for units/constants)
- https://github.com/numpy/numpy (NumPy — core dependency)
- https://github.com/scipy/scipy (SciPy — core dependency)
- https://github.com/h5py/h5py (h5py — HDF5 I/O)
- https://github.com/matplotlib/matplotlib (Matplotlib — visualization)
- https://github.com/lmfit/lmfit-py (lmfit — Thomson scattering fitting)
- https://github.com/pandas-dev/pandas (pandas — tabular data)
- https://github.com/pydata/xarray (xarray — labeled arrays for grids)

*Source: pyproject.toml dependencies. PlasmaPy is built on the scientific Python ecosystem.*

### 30. Interoperable Software (OPTIONAL)
- https://github.com/sunpy/sunpy (SunPy — fellow PyHC core package)
- https://github.com/spacepy/spacepy (SpacePy — fellow PyHC core package)

*Source: PlasmaPy is part of the heliopythoniverse/PyHC ecosystem, designed to install alongside other PyHC core packages without conflict.*

### 31. Related Instruments (OPTIONAL)
Not found

*PlasmaPy is general-purpose and not tied to a specific instrument, though it provides analysis support for Langmuir probes, Thomson scattering systems, and proton radiography setups generically.*

### 32. Related Observatories (OPTIONAL)
Not found

*PlasmaPy is not tied to a specific observatory or mission.*

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/PlasmaPy/PlasmaPy-logo/main/exports/with-text-dark.png

*Source: README.md and SoMEF.*
