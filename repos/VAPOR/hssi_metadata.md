# HSSI Metadata Extraction Results

**HSSI Software ID:** 6325743f-ad5d-4c24-aca3-6262a70d78d7
**Repository:** https://github.com/NCAR/VAPOR
**Source Revision:** 9250664aec645aadab5b5cc29fdbf670a7d4f080
**Extraction Date:** 2026-07-23
**Validation Date:** 2026-07-23
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** To be filled by actual submitter
- **Submitter Email:** To be filled by actual submitter
- **Source note:** Required placeholder; the repository does not identify the HSSI submitter.

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.6567350

- **Source note:** Retained from the existing HSSI record and confirmed as the concept DOI by the current DataCite and Zenodo records.

### 3. Code Repository (MANDATORY)
https://github.com/NCAR/VAPOR

- **Source note:** Retained from the existing HSSI record and confirmed by the repository and current Zenodo metadata.

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Data Processing and Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Field-line Tracing
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: 3D Graphics
- Data Visualization: Line Plots
- Data Visualization: Movies
- Data Visualization: Web-Based

- **Source note:** The two seeded parent categories were retained. Data Access and Retrieval was added because the bundled getWMSImage utility retrieves maps and imagery through WMS GetMap requests. Other subcategories were added from repository evidence: SliceRenderer and arbitrary cut planes; statistics and Python-derived variables; progressive multiresolution VDC storage; explicit magnetic-field line advection and streamline/pathline integration; cf2vdc, wrf2vdc, raw2vdc, and vdc2raw converters; contour/image/volume/isosurface/flow/particle rendering; Plot Utility; animation and frame output; and the Jupyter/AnyWidget visualizer. General geographic projection transforms are implemented with PROJ, but no domain-specific Coordinate Transforms child category applies. All selected child categories include their required parents, and all child labels use canonical `Parent: Child` spacing.

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Solar Environment

- **Source note:** Retained from the existing HSSI record. The README explicitly targets atmosphere and solar researchers. Ocean research is also in scope but is not an HSSI region value. No primary evidence supports adding the other controlled heliophysics regions.

### 6. Authors (MANDATORY)
1. **Nihanth Wagmi Cherukuru**
   - **Author Identifier:** Not found
   - **Affiliation:** NSF National Center for Atmospheric Research — https://ror.org/05cvfcr44
2. **John Clyne**
   - **Author Identifier:** Not found
   - **Affiliation:** NSF National Center for Atmospheric Research — https://ror.org/05cvfcr44
3. **CoreCode**
   - **Author Identifier:** Not found
   - **Affiliation:** CoreCode — identifier not found
4. **Joel Daves**
   - **Author Identifier:** Not found
   - **Affiliation:** NSF National Center for Atmospheric Research — https://ror.org/05cvfcr44
5. **Orhan Eroglu**
   - **Author Identifier:** Not found
   - **Affiliation:** NSF National Center for Atmospheric Research — https://ror.org/05cvfcr44
6. **Ian Franda**
   - **Author Identifier:** Not found
   - **Affiliation:** Not found
7. **Kevin Hallock**
   - **Author Identifier:** Not found
   - **Affiliation:** Not found
8. **Rémi Lacroix**
   - **Author Identifier:** Not found
   - **Affiliations:**
     - Institute for Development and Resources in Intensive Scientific Computing — https://ror.org/02jz7m443
     - French National Centre for Scientific Research — https://ror.org/02feahw73
9. **Samuel Li**
   - **Author Identifier:** https://orcid.org/0000-0001-8295-2248
   - **Affiliation:** NVIDIA Corporation — https://ror.org/03jdj4y14
10. **Orion Poplawski**
    - **Author Identifier:** Not found
    - **Affiliation:** Northwest Research Associates — https://ror.org/0583jne22
11. **Giovanni Rosa**
    - **Author Identifier:** Not found
    - **Affiliation:** Not found
12. **Scott Pearse**
    - **Author Identifier:** Not found
    - **Affiliation:** NSF National Center for Atmospheric Research — https://ror.org/05cvfcr44
13. **Stanislaw Jaroszynski**
    - **Author Identifier:** Not found
    - **Affiliation:** NSF National Center for Atmospheric Research — https://ror.org/05cvfcr44
14. **Kenny Gruchalla**
    - **Author Identifier:** Not found
    - **Affiliation:** Not found
15. **Niklas Roeber**
    - **Author Identifier:** Not found
    - **Affiliation:** Not found
16. **Pamela Gillman**
    - **Author Identifier:** Not found
    - **Affiliation:** Not found
17. **Alan Norton**
    - **Author Identifier:** Not found
    - **Affiliation:** NSF National Center for Atmospheric Research — https://ror.org/05cvfcr44

- **Source note:** Seeded authors were retained and identity-aware merges replaced the aliases clyne, sgpearse, and StasJ with full names supported by the current README, Zenodo creators, and the cited publication. Scott Pearse now has the NCAR affiliation supplied by the latest Zenodo version. Kenny Gruchalla, Niklas Roeber, and Pamela Gillman were added from the authoritative README project-member list. Alan Norton was added from repeated VAPOR source-header authorship credits and assigned the source-supported NSF National Center for Atmospheric Research affiliation; John Clyne received the same source-supported affiliation. Samuel Li’s verified ORCID was added from the reference-publication, repository-identity, and ORCID evidence resolved in validation. Affiliation acronyms were expanded and identifiers resolved with the ROR API. CoreCode remains represented as a personal creator because current DataCite classifies it as Personal; the similarly named ROR result was not assigned because identity is uncertain.

### 7. Software Name (MANDATORY)
NCAR/VAPOR

- **Source note:** Retained verbatim from the existing HSSI record; the repository full name and SoMEF output confirm it. The README uses the shorter name VAPOR.

### 8. Description (MANDATORY)
VAPOR is the Visualization and Analysis Platform for Ocean, Atmosphere, and Solar Researchers. VAPOR provides an interactive 3D visualization environment that can also produce animations and still frame images. VAPOR runs on most UNIX and Windows systems equipped with modern 3D graphics cards.

The VAPOR Data Collection (VDC) data model allows users progressively access the fidelity of their data, allowing for the visualization of terascale data sets on commodity hardware. VAPOR can also directly import data formats including WRF, MOM, POP, ROMS, and some GRIB and NetCDF files.

Users can perform ad-hoc analysis with VAPOR's interactive Python interpreter; which allows for the creation, modification, and visualization of new variables based on input model data.

VAPOR is a product of the NSF National Center for Atmospheric Research's Computational and Information Systems Lab. Support for VAPOR is provided by the U.S. National Science Foundation (grants # 03-25934 and 09-06379, ACI-14-40412), and by the Korea Institute of Science and Technology Information

Project homepage and binary releases can be found at https://www.vapor.ucar.edu/

- **Source note:** Retained verbatim from the existing HSSI record. It is substantially identical to the current README, preserving prior editorial intent.

### 9. Concise Description (OPTIONAL)
VAPOR is the Visualization and Analysis Platform for Ocean, Atmosphere, and Solar Researchers, providing interactive 3D visualization, animations, still images, and ad hoc Python analysis.

- **Source note:** Proposed replacement for the seeded 200-character value, which ended mid-word at “still fra”. This complete 188-character summary preserves the submitted meaning and is supported by the README.

### 10. Publication Date (RECOMMENDED)
2017-06-14

- **Source note:** **User decision:** 2017-06-14 is the earliest verifiable public GitHub repository date and is used as a proxy because VAPOR source evidence predates it and no authoritative initial-release date was found. This replaces the clearly semantically incorrect rolling Weekly release date previously used in Field 10; that release date is retained only as the Field 12 Version Date.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

- **Source note:** Retained from the existing HSSI record and confirmed by current DataCite metadata.

### 12. Version (RECOMMENDED)
- **Version Number:** NCAR/VAPOR - Weekly
- **Version Date:** 2026-07-20
- **Version Description:** Current untested Weekly prerelease build of VAPOR 3.11.0 (w61), built from commit 9250664aec645aadab5b5cc29fdbf670a7d4f080. The release warns that Weekly installers may not be stable.
- **Version PID:** https://doi.org/10.5281/zenodo.21460699

- **Source note:** The seeded version label was retained. Date, description, underlying 3.11.0 asset version, commit, and version DOI were refreshed from the current GitHub Weekly release and latest Zenodo/DataCite version. The official Zenodo version string is “Weekly”. The README badge DOI https://doi.org/10.5281/zenodo.13332956 is stale and identifies v3.9.3, so it is not proposed as the current Version PID.

### 13. Programming Language (RECOMMENDED)
- C
- C++
- IDL
- Java
- Javascript
- MATLAB
- Other
- Python 3.x
- Rust
- SQL

- **Source note:** Set-union policy retains every existing HSSI value. Current GitHub/SoMEF language analysis directly confirms C++, C, Python, IDL, and JavaScript; Other covers substantial GLSL, NCL, CMake, Shell, Perl, Objective-C++, and related code. **Uncertainty for Validator:** current GitHub language statistics do not substantiate the seeded Java, MATLAB, Rust, or SQL values, but extraction did not remove them.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.3390/atmos10090488

- **Source note:** Added from the preferred citation in the current README and confirmed by SoMEF.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

- **Source note:** Retained from the existing HSSI record and confirmed by LICENSE.txt, GitHub, current DataCite, and Zenodo. The conda recipe still says MIT and appears stale/inconsistent with these primary sources.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- Atmosphere
- Science
- Visualization
- 3D visualization
- Earth system science
- flow visualization
- geospatial data
- GRIB
- multiresolution
- netCDF
- ocean research
- scientific visualization
- simulation data
- solar research
- terascale data
- VDC
- volume rendering
- WRF

- **Source note:** The three seeded keywords were retained. Additions are supported by the README, reference publication, repository renderer/data-model code, and supported format/model readers. `ocean research` was added from the README scope and ocean-specific coordinate/model support identified during validation.

### 17. Data Sources (OPTIONAL)
- Other

- **Source note:** VAPOR primarily consumes local simulation/model files and can obtain geographic imagery through WMS/TMS-style services; none maps cleanly to a more specific controlled source value. No observatory-specific source is supported.

### 18. Input File Formats (RECOMMENDED)
- csv
- netCDF3/4
- Other

- **Source note:** `csv` was added by set-union because VAPOR selects and parses comma-separated X,Y,Z seed-coordinate files. NetCDF/CF and NetCDF-backed DCP/VDC support is explicit in the README, source, and DCP format documentation. Other is retained for WRF, MOM, POP, ROMS, MPAS, UGRID, RAM, GRIB, BOV, VDC/VDF, DCP, and raw model-data formats.

### 19. Output File Formats (RECOMMENDED)
- ascii
- csv
- netCDF3/4
- Other

- **Source note:** `csv` was added by set-union because VAPOR writes comma-separated flowline headers and records. VDCNetCDF writes VDC data to NetCDF files; ascii is retained for text output; and Other is retained for raw binary, VDC, GeoTIFF/TIFF, PNG, JPEG, image sequences, and movies.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

- **Source note:** The README states most UNIX and Windows systems. Current Weekly release assets provide x86-64 Linux AppImage, x86 macOS, Apple Silicon macOS, and win64 installers.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64
- GPU

- **Source note:** Current Weekly asset names directly confirm x86-64 and Apple Silicon arm64 builds. The README requires modern 3D graphics hardware, supporting GPU.

### 22. Related Phenomena (OPTIONAL)
Not found

- **Source note:** VAPOR is a general visualization and analysis platform rather than software designed around a particular heliophysics phenomenon.

### 23. Development Status (RECOMMENDED)
Active

- **Source note:** The repository is actively maintained; the current default-branch revision is included in the current Weekly release, and the documentation repository is also current.

### 24. Documentation (RECOMMENDED)
https://ncar.github.io/VaporDocumentationWebsite/

- **Source note:** Added from the repository contribution guide and current release links. This project documentation site is more authoritative than the GitHub wiki URL guessed by SoMEF.

### 25. Funder (OPTIONAL)
1. **Organization:** National Science Foundation
   - **Funder Identifier:** https://ror.org/021nxhr62
2. **Organization:** Korea Institute of Science and Technology Information
   - **Funder Identifier:** https://ror.org/01k4yrm29

- **Source note:** Added from the current README; organization names were expanded and ROR identifiers resolved through the ROR API.

### 26. Award Title (OPTIONAL)
1. **Award Title:** ITR:  Gleaning Insight into Large Time-Varying Scientific and Engineering Data
   - **Award Number:** 03-25934
2. **Award Title:** Enabling Transformational Science and Engineering Through Collaborative Visualization and Data Analysis
   - **Award Number:** 09-06379
3. **Award Title:** SI2-SSE: Wavelet Enabled Progressive Data Access and Storage Protocol (WASP)
   - **Award Number:** ACI-14-40412

- **Source note:** The National Science Foundation award numbers were retained in the README formatting. Exact award titles were added from NSF Awards API records 0325934, 0906379, and 1440412 after resolving the repository number formatting. For award 09-06379, the exact original official NSF title is `Enabling Transformational Science and Engineering Through Integrated Collaborative Visualization and Data Analysis for the National User Community`. The canonical payload title was shortened because HSSI's `Award.name` database column is `varchar(128)`, while the official title is 146 characters; the shortened title preserves the award's core meaning and fits the limit.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

- **Source note:** The repository prioritizes one publication, recorded in Field 14; no separate developer-prioritized publications were found.

### 28. Related Datasets (OPTIONAL)
- **Dataset:** VAPOR Sample Data
- **Permanent URL:** https://gdex.ucar.edu/datasets/d897007/
- **Citation:** Visualization and Enabling Technologies Section/Computational and Information Systems Laboratory/National Center for Atmospheric Research/UCAR (2024): VAPOR Sample Data. NSF National Center for Atmospheric Research. Dataset. https://gdex.ucar.edu/datasets/d897007/.

- **Source note:** VAPOR’s user-facing Import tab links the “Download example Datasets” collection; that repository-linked page points to this institutional GDEX record.

### 29. Related Software (OPTIONAL)
- netCDF-C — https://github.com/Unidata/netcdf-c
- PROJ — https://github.com/OSGeo/PROJ
- OSPRay — https://github.com/ospray/ospray

- **Source note:** Added as important core dependencies evidenced by CMake, conda metadata, VDCNetCDF, geographic projection code, and volume-rendering implementations.

### 30. Interoperable Software (OPTIONAL)
- ParaView — https://www.paraview.org/
- VisIt — https://visit-dav.github.io/visit-website/
- xarray — https://github.com/pydata/xarray

- **Source note:** The repository contains ParaView VDF-reader and VisIt VDC plugins. The Python API includes xarray loading, examples, and a declared xarray runtime dependency.

### 31. Related Instruments (OPTIONAL)
Not found

- **Source note:** VAPOR is instrument-agnostic. Solar-domain wording, generic model formats, and examples do not pass the designed-to-support relevance gate. No instrument candidate required SPASE resolution.

### 32. Related Observatories (OPTIONAL)
Not found

- **Source note:** VAPOR is not designed for a specific mission or observatory. Generic solar use and simulation-model support do not pass the relevance gate. The HSSI target vocabulary was fetched, but no observatory candidate was applicable.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/NCAR/VAPOR/9250664aec645aadab5b5cc29fdbf670a7d4f080/share/images/vapor_banner.png

- **Source note:** Proposed replacement for the seeded CircleCI status badge, which is not a software logo. The replacement is the VAPOR banner embedded by the current README and pinned to the extracted source revision.
