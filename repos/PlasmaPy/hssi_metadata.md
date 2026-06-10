# HSSI Metadata Extraction Results

**Repository:** https://github.com/PlasmaPy/PlasmaPy
**Extraction Date:** 2026-04-24
**HSSI Sync:** 2026-06-10 — reconciled with the final local HSSI record after a clean metadata replay and author-union update (software UUID `4507d98e-44d1-40ea-8733-8047738b9a7a`). Field values below reflect HSSI. Related Software was subsequently trimmed to non-generic libraries and Interoperable Software was cleared (see Fields 29–30).

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
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Magnetic Null Finding
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: Line Plots
- Data Visualization: 2D Graphics
- Models and Simulations
- Models and Simulations: First Principles
- Models and Simulations: Forward-Fitting
- Models and Simulations: MHD
- Models and Simulations: Physics-Based
- Models and Simulations: Theory

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

The PlasmaPy `CITATION.cff` lists 157 contributing authors. The recommended group attribution is **PlasmaPy Community**, which is listed first and links directly to the authoritative contributor roster.

> **Recommendation for HSSI maintainers:** The author list may optionally be simplified to the single **PlasmaPy Community** group entry, using https://github.com/PlasmaPy/PlasmaPy/blob/main/CITATION.cff as its author identifier. The full individual roster is retained below because it mirrors the current HSSI record.

> **Folded contributors:** Twelve `CITATION.cff` entries without a usable personal name are represented by **PlasmaPy Community** rather than separate Person records: the GitHub handles `BH4`, `Bzero`, `CBrown345`, `cicciope`, `flaixman`, `itsraashi`, `lgoenner`, `nrb1234`, `Physics-is-awesome`, `seanjunheng2`, and `WineDarkMoon`, plus `Oscar` (alias `0scvr`).

**Full HSSI author list (148 entries): PlasmaPy Community + 145 named `CITATION.cff` contributors + 2 contributors retained from the original HSSI record (Anthony Vo and Frank Silva).**

- **Author:** PlasmaPy Community
  - *Author Identifier:* https://github.com/PlasmaPy/PlasmaPy/blob/main/CITATION.cff

- **Author:** Nicholas A. Murphy
  - *Author Identifier:* https://orcid.org/0000-0001-6628-8033
  - *Affiliation:* Center for Astrophysics, Harvard & Smithsonian
  - *Affiliation:* Smithsonian Astrophysical Observatory
  - *Affiliation:* Smithsonian Institution

- **Author:** Erik T. Everson
  - *Author Identifier:* https://orcid.org/0000-0001-6079-8307
  - *Affiliation:* University of California, Los Angeles

- **Author:** Dominik Stańczak-Marikin
  - *Author Identifier:* https://orcid.org/0000-0001-6291-8843
  - *Affiliation:* University of Warsaw

- **Author:** Peter V. Heuer
  - *Author Identifier:* https://orcid.org/0000-0001-5050-6606
  - *Affiliation:* University of Rochester

- **Author:** Pawel M. Kozlowski
  - *Author Identifier:* https://orcid.org/0000-0001-6849-3612
  - *Affiliation:* West Virginia University

- **Author:** Elliot Johnson
  - *Affiliation:* University of Delaware

- **Author:** Ritiek Malhotra
  - *Affiliation:* Chandigarh University

- **Author:** David Schaffner
  - *Author Identifier:* https://orcid.org/0000-0002-9180-6565
  - *Affiliation:* Bryn Mawr College

- **Author:** Steve Vincena
  - *Author Identifier:* https://orcid.org/0000-0002-6468-5710
  - *Affiliation:* University of California, Los Angeles

- **Author:** Mel Abler
  - *Author Identifier:* https://orcid.org/0000-0003-2528-8752

- **Author:** James Addison

- **Author:** Paula Valentina Alarcon
  - *Author Identifier:* https://orcid.org/0000-0002-7860-9567
  - *Affiliation:* North Carolina State University

- **Author:** Benjamin Antognetti
  - *Author Identifier:* https://orcid.org/0000-0002-1444-9680
  - *Affiliation:* University of Wisconsin–Madison

- **Author:** Ataf Fazledin Ahamed
  - *Affiliation:* OpenRefactory Inc.

- **Author:** Christoper Arran
  - *Author Identifier:* https://orcid.org/0000-0002-8644-8118
  - *Affiliation:* University of York

- **Author:** Haman Bagherianlemraski
  - *Author Identifier:* https://orcid.org/0000-0001-7381-1996
  - *Affiliation:* University of Massachusetts Amherst

- **Author:** Jasper P. Beckers
  - *Affiliation:* ASML (United States)

- **Author:** Manas Satish Bedmutha

- **Author:** Camilo Bedoya-Lopez

- **Author:** Justin Bergeron

- **Author:** Ludovico Bessi

- **Author:** Riley Britten

- **Author:** Shane Brown
  - *Author Identifier:* https://orcid.org/0000-0003-3309-3939
  - *Affiliation:* University of Delaware

- **Author:** Khalil Bryant
  - *Author Identifier:* https://orcid.org/0000-0002-2105-0280
  - *Affiliation:* University of Michigan

- **Author:** Sean Carroll

- **Author:** Carlos Cartagena-Sanchez
  - *Author Identifier:* https://orcid.org/0000-0002-0486-1292
  - *Affiliation:* Beloit College

- **Author:** Sarthak Choudhary

- **Author:** Christian Clauss

- **Author:** Sean Chambers

- **Author:** Ankur Chattopadhyay

- **Author:** Apoorv Choubey

- **Author:** Sebastian Colom
  - *Author Identifier:* https://orcid.org/0009-0006-0863-0180
  - *Affiliation:* NASA Ames Research Center

- **Author:** Chase Davies

- **Author:** Jacob Deal

- **Author:** Gregor Decristoforo
  - *Author Identifier:* https://orcid.org/0000-0002-7616-0946
  - *Affiliation:* UiT The Arctic University of Norway

- **Author:** Diego A. Diaz Riega

- **Author:** Fionnlagh Mackenzie Dover
  - *Author Identifier:* https://orcid.org/0000-0002-1984-7303
  - *Affiliation:* SP2RC, School of Mathematics and Statistics, University of Sheffield

- **Author:** David Drozdov

- **Author:** Tiger Du
  - *Author Identifier:* https://orcid.org/0000-0002-8676-1710
  - *Affiliation:* Vanderbilt University

- **Author:** Leah Einhorn

- **Author:** Tamar Ervin
  - *Author Identifier:* https://orcid.org/0000-0002-8475-8606
  - *Affiliation:* University of California, Berkeley

- **Author:** Thomas Fan

- **Author:** Samaiyah I. Farid
  - *Author Identifier:* https://orcid.org/0000-0003-0223-7004
  - *Affiliation:* Center for Astrophysics, Harvard & Smithsonian

- **Author:** Emmanuel Ferdman
  - *Author Identifier:* https://orcid.org/0009-0004-8953-0151

- **Author:** Michael Fischer

- **Author:** Bryan Foo
  - *Author Identifier:* https://orcid.org/0000-0001-5308-6870
  - *Affiliation:* Massachusetts Institute of Technology

- **Author:** Heinz-Alexander Fütterer
  - *Author Identifier:* https://orcid.org/0000-0003-4397-027X

- **Author:** Rajagopalan Gangadharan

- **Author:** Seth Gerow
  - *Author Identifier:* https://orcid.org/0009-0008-3588-0497
  - *Affiliation:* Embry-Riddle Aeronautical University

- **Author:** Mahlet Getahun
  - *Affiliation:* Marietta College

- **Author:** Jessica Gonzalez
  - *Affiliation:* California Institute of Technology

- **Author:** Brian Goodall

- **Author:** Shauna Gordon-McKeon
  - *Author Identifier:* https://orcid.org/0000-0002-2373-8927

- **Author:** Marco Gorelli

- **Author:** Graham Goudeau

- **Author:** Silvina Guidoni
  - *Author Identifier:* https://orcid.org/0000-0003-1439-4218
  - *Affiliation:* American University

- **Author:** Julia Guimiot

- **Author:** Colby C. Haggerty
  - *Author Identifier:* https://orcid.org/0000-0002-2160-7288
  - *Affiliation:* University of Chicago

- **Author:** Raymon Skjørten Hansen

- **Author:** Mohammed Haque
  - *Affiliation:* Columbia University

- **Author:** Julien Hillairet
  - *Author Identifier:* https://orcid.org/0000-0002-1073-6383

- **Author:** Chris Hoang

- **Author:** Poh Zi How

- **Author:** Yi-Min Huang
  - *Author Identifier:* https://orcid.org/0000-0002-4237-2211
  - *Affiliation:* Princeton University

- **Author:** Nabil Humphrey
  - *Author Identifier:* https://orcid.org/0000-0002-4227-2544

- **Author:** Maria Isupova

- **Author:** Alexis Jeandet
  - *Author Identifier:* https://orcid.org/0000-0003-2892-6924
  - *Affiliation:* Laboratory of Plasma Physics (LPP/CNRS)

- **Author:** Evan Jones
  - *Author Identifier:* https://orcid.org/0009-0004-6699-4869

- **Author:** Marcin Kastek
  - *Author Identifier:* https://orcid.org/0009-0002-5918-4652
  - *Affiliation:* Institute of Plasma Physics and Laser Microfusion

- **Author:** James Kent

- **Author:** Dusan Klima
  - *Author Identifier:* https://orcid.org/0009-0008-5134-6171

- **Author:** Alf Köhn-Seemann
  - *Author Identifier:* https://orcid.org/0000-0002-1192-2057
  - *Affiliation:* University of Stuttgart

- **Author:** Siddharth Kulshrestha

- **Author:** Sundaran Kumar

- **Author:** Piotr Kuszaj

- **Author:** Samuel J. Langendorf
  - *Author Identifier:* https://orcid.org/0000-0002-7757-5879
  - *Affiliation:* Los Alamos National Laboratory

- **Author:** Anna Lanteri

- **Author:** Terrance Takho Lee

- **Author:** Andrew J. Leonard
  - *Author Identifier:* https://orcid.org/0000-0001-5270-7487
  - *Affiliation:* Aperio Software Ltd.

- **Author:** Nicolas Lequette
  - *Affiliation:* Laboratoire de Physique des Plasmas

- **Author:** Pey Lian Lim
  - *Author Identifier:* https://orcid.org/0000-0003-0079-4114
  - *Affiliation:* Space Telescope Science Institute

- **Author:** Aditya Magarde

- **Author:** Joao Victor Martinelli

- **Author:** Muhammad Masood
  - *Affiliation:* University of Edinburgh

- **Author:** Isaias McHardy
  - *Author Identifier:* https://orcid.org/0000-0001-5394-9445

- **Author:** Dhawal Modi

- **Author:** Kevin Montes
  - *Author Identifier:* https://orcid.org/0000-0002-0762-3708
  - *Affiliation:* Massachusetts Institute of Technology

- **Author:** Stuart J. Mumford
  - *Author Identifier:* https://orcid.org/0000-0003-4217-4642
  - *Affiliation:* Aperio Software Ltd.
  - *Affiliation:* https://orcid.org/0000-0001-5270-7487
  - *Affiliation:* University of Sheffield

- **Author:** Joshua Munn

- **Author:** Leo Murphy
  - *Affiliation:* College of William & Mary

- **Author:** Bao Nguyen
  - *Author Identifier:* https://orcid.org/0000-0002-1753-4223
  - *Affiliation:* Imperial College London

- **Author:** Suzanne Nie

- **Author:** Carlos Ortiz
  - *Affiliation:* University of Wisconsin–Madison

- **Author:** Shivam Panda

- **Author:** Mahima Pannala

- **Author:** Tulasi Parashar
  - *Author Identifier:* https://orcid.org/0000-0003-0602-8381
  - *Affiliation:* University of Delaware

- **Author:** Neil Patel

- **Author:** Francisco Silva Pavon

- **Author:** Roberto Díaz Pérez

- **Author:** Preston Pitzer
  - *Author Identifier:* https://orcid.org/0009-0007-0655-1347
  - *Affiliation:* Virginia Tech

- **Author:** Jakub Polak

- **Author:** Ramiz Qudsi
  - *Author Identifier:* https://orcid.org/0000-0001-8358-0482
  - *Affiliation:* Boston University

- **Author:** Raajit Raj

- **Author:** Vishwas Rajashekar
  - *Author Identifier:* https://orcid.org/0000-0002-4914-6612

- **Author:** Afzal Rao

- **Author:** Jeffrey Reep
  - *Author Identifier:* https://orcid.org/0000-0003-4739-1152
  - *Affiliation:* University of Hawaii at Manoa

- **Author:** Steve Richardson
  - *Author Identifier:* https://orcid.org/0000-0002-3056-6334
  - *Affiliation:* U.S. Naval Research Laboratory

- **Author:** Jayden Roberts
  - *Author Identifier:* https://orcid.org/0009-0009-9490-5284

- **Author:** Shanshan Rodriguez
  - *Author Identifier:* https://orcid.org/0000-0003-2944-0424
  - *Affiliation:* Grinnell College

- **Author:** Reynaldo Rojas Zelaya

- **Author:** Armando Salcido

- **Author:** Andrew Sandeman

- **Author:** Antonia Savcheva
  - *Author Identifier:* https://orcid.org/0000-0002-5598-046X
  - *Affiliation:* Center for Astrophysics, Harvard & Smithsonian

- **Author:** Cora Schneck

- **Author:** Chengcai Shen
  - *Author Identifier:* https://orcid.org/0000-0002-9258-4490
  - *Affiliation:* Center for Astrophysics, Harvard & Smithsonian

- **Author:** Andrew Sheng

- **Author:** Dawa Nurbu Sherpa

- **Author:** Luciano Silvestri
  - *Author Identifier:* https://orcid.org/0000-0003-3530-7910
  - *Affiliation:* Michigan State University

- **Author:** Trestan F. Simon
  - *Author Identifier:* https://orcid.org/0009-0000-3029-8619

- **Author:** Angad Singh

- **Author:** Ankit Singh

- **Author:** Brigitta Sipőcz
  - *Author Identifier:* https://orcid.org/0000-0002-3713-6337
  - *Affiliation:* DIRAC Institute, University of Washington
  - *Affiliation:* Infrared Processing and Analysis Center

- **Author:** Cody Skinner
  - *Affiliation:* Phoenix Security Labs

- **Author:** Tomasz Adam Skrzypczak

- **Author:** Nikita Smirnov

- **Author:** Joseph Smith
  - *Author Identifier:* https://orcid.org/0000-0002-5978-6840
  - *Affiliation:* Marietta College

- **Author:** Stuart Sobeske
  - *Affiliation:* University of Michigan

- **Author:** Matteo Spedicato

- **Author:** David Stansby
  - *Author Identifier:* https://orcid.org/0000-0002-1365-1908
  - *Affiliation:* Advanced Research Computing Centre, University College London, UK
  - *Affiliation:* Department of Mechanical Engineering, University College London
  - *Affiliation:* Imperial College London
  - *Affiliation:* University College London

- **Author:** Tomás Stinson

- **Author:** Shelley Sugiharto
  - *Author Identifier:* https://orcid.org/0009-0003-3159-0541
  - *Affiliation:* Texas A&M University

- **Author:** Michaela Švancarová

- **Author:** Antoine Tavant
  - *Author Identifier:* https://orcid.org/0000-0003-0010-8073
  - *Affiliation:* Laboratoire de Physique des Plasmas, Ecole Polytechnique

- **Author:** Veronica Tranquilino
  - *Affiliation:* University of Michigan

- **Author:** Thomas Ulrich

- **Author:** Mychal Valle
  - *Author Identifier:* https://orcid.org/0000-0003-4230-6916
  - *Affiliation:* University of California, Los Angeles

- **Author:** Thomas Varnish
  - *Author Identifier:* https://orcid.org/0000-0002-8078-214X

- **Author:** Tien Vo
  - *Author Identifier:* https://orcid.org/0000-0002-8335-1441
  - *Affiliation:* Laboratory for Atmospheric and Space Physics

- **Author:** Tingfeng Wu
  - *Author Identifier:* https://orcid.org/0000-0001-8745-204X

- **Author:** Sixue Xu
  - *Author Identifier:* https://orcid.org/0000-0001-7959-8495
  - *Affiliation:* University of California, Los Angeles

- **Author:** Chun Hei Yip

- **Author:** Carol Zhang

- **Author:** Clément Robert
  - *Author Identifier:* https://orcid.org/0000-0001-8629-7068

- **Author:** Shawn Polson
  - *Author Identifier:* https://orcid.org/0000-0003-0619-5745
  - *Affiliation:* Laboratory for Atmospheric and Space Physics

- **Author:** Yaocheng Chen
  - *Author Identifier:* https://orcid.org/0000-0002-8967-4911
  - *Affiliation:* Korea Astronomy and Space Science Institute

- **Author:** Anthony Vo

- **Author:** Frank Silva

*Source: final local HSSI record after union reconciliation, cross-checked against `CITATION.cff`; HSSI-only contributors Anthony Vo and Frank Silva were retained.*

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
- **Publisher Identifier:** https://zenodo.org

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
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

*Source: LICENSE.md and pyproject.toml.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- Astronomy
- Astrophysics
- Atomic Physics
- Fusion
- Heliophysics
- High-Energy-Density Physics
- Langmuir Probes
- Open Source
- Open Source Software
- Particles
- Physics
- Plasma
- Plasma Astrophysics
- Plasma Diagnostics
- Plasma Parameters
- Plasma Physics
- Plasma Science
- Proton Radiography
- Python
- Science
- Solar Physics
- Space Physics
- Space Plasmas
- Thomson Scattering

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
- Apple Silicon arm64
- x86-64

*Source: GitHub macOS-latest runners are Apple Silicon arm64 since 2024. Default GitHub-hosted Linux/Windows runners are x86-64. Pure Python package is also broadly portable.*

### 22. Related Phenomena (OPTIONAL)
Not found

*PlasmaPy is general-purpose plasma physics infrastructure rather than software dedicated to specific phenomena from the controlled vocabulary (Coronal Heating, Coronal Holes, CMEs, Solar Corona, Solar Flares, X-ray emission). It can be applied to many of these phenomena indirectly.*

### 23. Development Status (RECOMMENDED)
Active

*Source: Frequent commits, CI badges, regular releases (most recent: 2026.2.0 on 2026-02-20). Listed in PyHC core packages.*

### 24. Documentation (RECOMMENDED)
https://docs.plasmapy.org/

*Source: README.md, pyproject.toml, .readthedocs.yml, PyHC registry entry.*

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
  - *Funder Identifier:* https://ror.org/027ka1x80

- **Organization:** National Science Foundation
  - *Funder Identifier:* https://ror.org/021nxhr62

- **Organization:** Smithsonian Institution
  - *Funder Identifier:* https://ror.org/01pp8nd67

- **Organization:** United States Department of Energy
  - *Funder Identifier:* https://ror.org/01bj3aw27

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
- https://github.com/h5py/h5py (h5py — HDF5 I/O)
- https://github.com/lmfit/lmfit-py (lmfit — Thomson scattering fitting)

*Source: pyproject.toml dependencies. Matplotlib, NumPy, pandas, xarray, and SciPy were intentionally removed — they are ubiquitous, generic Python libraries, not distinguishing related software worth listing.*

### 30. Interoperable Software (OPTIONAL)
Not found

*SpacePy and SunPy were removed: although they are fellow PyHC core packages installable alongside PlasmaPy, there is no explicit interoperability layer between them and PlasmaPy, so listing them as "interoperable software" overstated the relationship.*

### 31. Related Instruments (OPTIONAL)
Not found

*PlasmaPy is general-purpose and not tied to a specific instrument, though it provides analysis support for Langmuir probes, Thomson scattering systems, and proton radiography setups generically.*

### 32. Related Observatories (OPTIONAL)
Not found

*PlasmaPy is not tied to a specific observatory or mission.*

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/PlasmaPy/PlasmaPy-logo/main/exports/with-text-dark.png

*Source: README.md and SoMEF.*
