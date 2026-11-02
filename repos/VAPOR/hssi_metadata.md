# HSSI Metadata Extraction Results

**HSSI Software ID:** 6325743f-ad5d-4c24-aca3-6262a70d78d7
**Repository:** https://github.com/NCAR/VAPOR
**Source Revision:** 9250664aec645aadab5b5cc29fdbf670a7d4f080
**Extraction Date:** 2026-07-23
**Validation Date:** 2026-11-02
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
3. **core-code (GitHub)** *(stored as givenName `core-code`, familyName `(GitHub)`)*
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

**core-code — username representation.** This creator is recorded as given name `core-code`, family name
`(GitHub)`: the catalogue's convention for a proven platform handle whose holder has published no human
name. An earlier revision of this file recorded a blank given name with the family name "CoreCode". The
form asserts a handle and its platform, and deliberately **not** a personal name. Evidence: this repository's git author is `CoreCode <core-code@users.noreply.github.com>`, a legacy
GitHub noreply address that encodes the login directly, and GitHub's commit API attributes commit
`38389bc9a67e04481cfe3ec1c4448ae3a26f89aa` to account **`core-code`, ID 1261954**. "CoreCode" was that
account's profile display name; `core-code` is the exact login, and handle capitalization is preserved
verbatim.

*Trap recorded so it is not repeated:* `github.com/corecode` — the same string without the hyphen — is a
**different account** (ID 177979, profile name "Simon Schubert"). It must never be substituted here, and
no real name may be inferred from it. The uncertainty noted above about this creator's human identity is
unchanged; only the handle representation is now exact.

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

- **Source note:** This complete 188-character summary replaces the earlier 200-character value, which ended mid-word at “still fra”; it preserves the submitted meaning and is supported by the README.

### 10. Publication Date (RECOMMENDED)
2017-06-14

- **Source note:** 2017-06-14 is the earliest verifiable public GitHub repository date and is used as a proxy because VAPOR source evidence predates it and no authoritative initial-release date was found. This replaces the date of the rolling Weekly pre-release build that Field 10 held before the 2026-07-23 extraction, which is not a publication date of the software; the Weekly build is not a release, so Field 12 does not record it either.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

- **Source note:** Retained from the existing HSSI record and confirmed by current DataCite metadata.

### 12. Version (RECOMMENDED)
- **Version Number:** 3.10.1
- **Version Date:** 2025-05-19
- **Version Description:**
  * Fix VAPOR freezes after rendering #3768
  * Fix warning and invalid animation state
  * Fix Open session from command line broken #3772
- **Version PID:** https://doi.org/10.5281/zenodo.15466071

The description is exactly these three `* ` bullet lines, joined by single newlines.

*Why 3.10.1 and not `Weekly` (rules 2 and 3):* VAPOR publishes a rolling GitHub release on the moving tag `Weekly`. GitHub flags it as a pre-release, and its body reads "Weekly installers are untested an may not be stable." (the typo is the project's). The tag is re-pointed and the release republished with each build, so the label names no fixed build: the build HSSI recorded was w61 (Zenodo deposit dated 2026-07-20), while on 2026-11-02 the release, republished 2026-10-12, carried w73 installers of `VAPOR-3.11.0` built from `9250664aec645aadab5b5cc29fdbf670a7d4f080`. A GitHub release marked pre-release is unreleased code and never a release (rules 2 and 3), and a row for it would carry a date, notes and a PID that go stale every week. The 3.11.0 the weekly builds carry is declared in `CMakeLists.txt` (lines 46–49) at `9250664` but not yet released. 3.10.1 is the newest release: its GitHub release (tag `3.10.1`, name `3.10.1`), published 2025-05-19T17:13:11Z, is neither a draft nor a pre-release; the tag points to commit `040899c79006599bc9b47ae8567499c313115f3a` ("bump version"), an ancestor of `9250664`, where `CMakeLists.txt` declares 3.10.1. The tag `v3.10.1` points to the same commit and names the same release. Every GitHub release published after it is a build of the Weekly pre-release. The NCAR conda channel (`ncar-vapor/vapor`) stops at 3.10.0, and the PyPI project named `vapor` is an unrelated package (`https://github.com/xiaket/vapor`), so neither lists a newer release. The number is written without a `v`, as the GitHub release's tag and name and the CMake version write it.

*Version date* 2025-05-19 is the GitHub release's UTC publication day (rule 7); both tags and the Zenodo deposit (publication date 2025-05-19) agree.

*Version description* (rules 13–16): the release name is the bare number and the repository has no changelog file at the tag, so the text comes from the release body, a "What's Changed" list of four items. Three are kept verbatim, each a fix a user can hit (commits `d39843b`, `75e482f` and `f116ef6` in the `3.10.0..v3.10.1` range). "Upgrade conda" (`650f087`) is a packaging chore and is dropped (rule 14), as are the "What's Changed" heading, each item's trailing credit naming its author and pull request and the "Full Changelog" compare link.

*Version PID* (rule 17): `10.5281/zenodo.15466071` is this release's GitHub-integration deposit. Its Zenodo `version` is `v3.10.1` and its title `NCAR/VAPOR: 3.10.1`, it carries `IsSupplementTo https://github.com/NCAR/VAPOR/tree/v3.10.1`, and the concept's `HasVersion` list includes it. The DOI resolves. The README badge DOI `10.5281/zenodo.13332956` identifies v3.9.3 and is stale, so it is not the Version PID.

*Superseded value.* HSSI held `Weekly` (release date 2026-07-20, version PID `https://doi.org/10.5281/zenodo.21460699`) until the 3.10.1 release update; an earlier revision of this file wrote the number as `NCAR/VAPOR - Weekly`, which is how the view API renders a version, not the stored number. The label had been carried over from the seeded record, and its description, "Current untested Weekly prerelease build of VAPOR 3.11.0 (w61), built from commit 9250664aec645aadab5b5cc29fdbf670a7d4f080. The release warns that Weekly installers may not be stable.", was a curator's summary rather than the release's own words (rule 15). Do not re-propose `Weekly`, and do not treat the weekly Zenodo deposits as versions: every one carries the version string `Weekly`.

*For the next release update:* the default branch carries 3.11.0 work that has reached users only in the weekly pre-release builds, including a rectilinear-grid volume renderer (`eb20d0f`), transfer-function and keyframing updates (`a991cb7`) and Marimo support for the Python API's interactive widgets (`43b85ed`). Record 3.11.0 once a GitHub release that is not a pre-release publishes it.

### 13. Programming Language (RECOMMENDED)
- C
- C++
- Other
- Python 3.x

- **Source note:** Rule 4 counts the language a user writes plus the code that carries the science, read at `9250664`. C++ is the application and its libraries (`apps/`, `lib/`). Python 3.x is the Python API (`apps/pythonapi`; the conda recipe pins `python=3.9`). C is the C-callable VDC interface built into the VDC library (`include/vapor/VDC_c.h`, an `extern "C"` API implemented in `lib/vdc/VDC_c.cpp`). Other is GLSL, the shader language of the renderers (`share/shaders/*.vert`, `*.frag`, `*.geom`), which has no row.

*Removed in the 3.10.1 release update (rule 9), after an earlier revision of this file asked for these carried-over values to be re-examined:*
- **Java, MATLAB, Rust, SQL:** the tree at `9250664` contains no `.java`, `.m`, `.rs` or `.sql` file, and GitHub's language statistics list none of these languages; they had been carried over from the seeded record.
- **IDL:** the only IDL code is `share/examples/idl/`, 27 example procedures; its `README.txt` says they demonstrate "how to read and write VDF files from IDL". The procedures call `vdc_*` routines (for example `vdc_bufreadcreate` in `AddCurlVDF.pro`, line 154), which nothing in this tree defines for IDL. This tree has no `lib/idl` and no CMake target for IDL wrappers; the `BUILD_IDL_WRAPPERS` placeholder survives only in `scripts/vapor-setup.*.sed`, which no CMake file references. Examples for an interface nothing builds are not a supported front end (rule 4).
- **Javascript:** `apps/pythonapi/vapor/widget.js` and `widget-jquery.js` are the browser side of the Jupyter widget. Users write Python, and the rendering runs in C++ and GLSL, so the widget's client code is neither the language a user writes nor the science core (rule 4).

Not counted, so a later refresh does not add them: CMake, shell and Perl (`buildutils/*.pl`) are build tooling; the NCL scripts in `share/examples/NCL/` are examples run with NCL itself; Objective-C++ (`*.mm`) is macOS platform code for the C++ application.

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

- **Source note:** The README states most UNIX and Windows systems. The 3.10.1 release ships x86-64 Linux AppImage, x86 macOS, Apple Silicon macOS, and win64 installers (`VAPOR-3.10.1-x86_64.AppImage`, `VAPOR3-3.10.1-macOSx86.dmg`, `VAPOR3-3.10.1-AppleSilicon.dmg`, `VAPOR3-3.10.1-win64.exe`), and the Weekly pre-release builds ship the same four.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64
- GPU

- **Source note:** The 3.10.1 release's installer names, which the Weekly pre-release builds repeat, directly confirm x86-64 and Apple Silicon arm64 builds. The README requires modern 3D graphics hardware, supporting GPU.

### 22. Related Phenomena (OPTIONAL)
Not found

- **Source note:** VAPOR is a general visualization and analysis platform rather than software designed around a particular heliophysics phenomenon.

### 23. Development Status (RECOMMENDED)
Active

- **Source note:** The repository is actively maintained; the current default-branch revision is included in the current Weekly release, and the documentation repository is also current. Rule 6 anchors: the last commit on `main` is `9250664`, dated 2026-06-02T08:21:50−06:00, and the last release is 3.10.1, published 2025-05-19. The repository is not archived, and the README carries no repostatus.org badge or status statement.

### 24. Documentation (RECOMMENDED)
https://ncar.github.io/VaporDocumentationWebsite/

- **Source note:** Added from the repository contribution guide and current release links. This project documentation site is more authoritative than the GitHub wiki URL guessed by SoMEF.

### 25. Funder (OPTIONAL)
1. **Organization:** U.S. National Science Foundation
   - **Funder Identifier:** https://ror.org/021nxhr62
2. **Organization:** Korea Institute of Science and Technology Information
   - **Funder Identifier:** https://ror.org/01k4yrm29

- **Source note:** Added from the current README; organization names were expanded and ROR identifiers resolved through the ROR API. HSSI's organization row for `https://ror.org/021nxhr62` is named `U.S. National Science Foundation`, ROR's display name, which rule 9 makes the name of a ROR-keyed row; an earlier revision of this file wrote `National Science Foundation`, which did not match it.

### 26. Award Title (OPTIONAL)
1. **Award Title:** ITR:  Gleaning Insight into Large Time-Varying Scientific and Engineering Data
   - **Award Number:** 03-25934
2. **Award Title:** Enabling Transformational Science and Engineering Through Collaborative Visualization and Data Analysis
   - **Award Number:** 09-06379
3. **Award Title:** SI2-SSE: Wavelet Enabled Progressive Data Access and Storage Protocol (WASP)
   - **Award Number:** ACI-14-40412

- **Source note:** The National Science Foundation award numbers were retained in the README formatting. Exact award titles were added from NSF Awards API records 0325934, 0906379, and 1440412 after resolving the repository number formatting. For award 09-06379, the exact original official NSF title is `Enabling Transformational Science and Engineering Through Integrated Collaborative Visualization and Data Analysis for the National User Community`. The stored title is shortened because HSSI's `Award.name` database column is `varchar(128)`, while the official title is 146 characters; the shortened form preserves the award's core meaning and fits the limit.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

- **Source note:** The repository prioritizes one publication, recorded in Field 14; no separate developer-prioritized publications were found.

*Search for publications since the 2026-07-23 extraction, made 2026-11-02:* Semantic Scholar's list of works citing the Field 14 paper, a Crossref bibliographic search for the VAPOR platform, and a Crossref author search for John Clyne. No new publication by VAPOR's developers about VAPOR appeared (rule 3). VAPOR is widely used: the works citing the Field 14 paper span atmospheric, ocean and solar research and keep appearing, so under rule 5 a list of papers that use it would not help a searcher, and none is added. Papers seen in this search, such as Kuridze et al. 2026 (https://doi.org/10.1038/s41586-026-10871-3) and Liu et al. 2026 (https://doi.org/10.3847/1538-4357/ae88ec), were weighed under that rule and not added.

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

- **Source note:** VAPOR is not designed for a specific mission or observatory. Generic solar use and simulation-model support do not pass the relevance gate, so no observatory candidate is applicable.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/NCAR/VAPOR/9250664aec645aadab5b5cc29fdbf670a7d4f080/share/images/vapor_banner.png

- **Source note:** This VAPOR banner replaces the earlier CircleCI status badge, which is not a software logo. The banner is embedded by the current README and pinned to the extracted source revision.
