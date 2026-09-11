# HSSI Metadata Extraction Results

**HSSI Software ID:** 6b9189ab-3bdf-4b2c-9d95-2a5b93e72f69
**Repository:** https://github.com/PolarMesosphericClouds/SkyWinder
**Source Revision:** 1fd4fbc0e52029b88095b7dd0b542f74da9d4abe
**Extraction Date:** 2026-09-09
**Validation Date:** 2026-09-11
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)

- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

No submitter identity was supplied by the software sources.

### 2. Persistent Identifier (RECOMMENDED)

**Value:** Not found

The tracked repository contains no CITATION.cff, codemeta.json, .zenodo.json, DOI badge, or software DOI. PyPI metadata also supplies no project DOI. DataCite searches by title, subject, exact repository relation, and creators found the SkyWinder paper, thesis, and data records but no Software resource. Indexed Zenodo searches by exact title, repository path, and author identity found no SkyWinder record; the Zenodo API was unavailable, so authoritative exclusion through that route remains unresolved. The DOI `https://doi.org/10.3389/fspas.2023.1023550` identifies the journal article recorded in Field 14, not a software release.

### 3. Code Repository (MANDATORY)

**Value:** https://github.com/PolarMesosphericClouds/SkyWinder

This is the canonical repository URL in GitHub metadata, package metadata, the PyHC community registry, and the software paper. The repository is not marked archived.

### 4. Software Functionality (RECOMMENDED)

**Values:**

- Coordinate Transforms
- Coordinate Transforms: Mission-Specific
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Packet Decommutation
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Data Visualization: Mission-Specific
- Data Visualization: Movies
- Mission-related
- Mission-related: Analysis
- Mission-related: Calibration
- Mission-related: Distribution/Access
- Mission-related: Ingest
- Mission-related: Instrumentation
- Mission-related: Monitoring
- Mission-related: Operations
- Mission-related: Orchestration
- Mission-related: Packet Decommutation
- Mission-related: Processing
- Mission-related: Science Data Processing

The selection describes the combined SkyWinder flight-and-analysis software rather than every internal dependency. The pinned flight tree implements distributed subsystem coordination, camera acquisition, instrument commanding, telemetry packet creation and interpretation, downlink/uplink, housekeeping monitoring, ground receipt, relay, image conversion, and graphical displays. `skywinder/communication/file_format_classes.py`, `packet_classes.py`, and `downlink_classes.py` establish format conversion and packet decommutation; the camera and ground modules establish image correction, reduction, display, and mission operations. The 2023 software paper documents pointing reconstruction, projection from astrometric solutions, calibration, stray-light correction, star finding, mosaics, movies, keograms, and power spectra. The official SkyWinder-Analysis companion implements mission-specific pixel-to-sky coordinate transformations and Lomb–Scargle analysis of timestamped pointing trajectories, supporting `Coordinate Transforms: Mission-Specific` and `Data Processing and Analysis: Time Series Analysis`. Every selected child is parent-qualified, and each selected parent is included.

### 5. Related Region (RECOMMENDED)

**Values:**

- Earth Lower and Middle Atmosphere
- Earth Thermosphere

README.md describes mid- and upper-atmosphere science instrumentation. The software paper places the originating PMC-Turbo observations near 80 km in the mesosphere/lower thermosphere and describes neutral upper-atmosphere dynamics. These two more specific controlled terms deliberately replace the previously stored broad `Earth Atmosphere`, which is not retained in the complete set; the sources do not establish the ionosphere as the package's region.

### 6. Authors (MANDATORY)

**Author 1:**

- **Name:** Carl Bjorn Kjellstrand
- **Author Identifier:** https://orcid.org/0000-0003-3777-3886
- **Affiliation:** Not selected

**Author 2:**

- **Name:** Bifford P. Williams
- **Author Identifier:** https://orcid.org/0000-0002-1797-5985
- **Affiliation:** Not selected

The peer-reviewed software paper credits both people as authors. Its contribution statement says Carl Kjellstrand adapted legacy PMC-Turbo code to SkyWinder and Bifford Williams was the SkyWinder principal investigator. The setup metadata and PyHC entry independently identify Carl. Preserve the existing display spelling `Carl Bjorn Kjellstrand`; the paper's `Carl Björn Kjellstrand` is an identity-confirming variant. Glenn Jones and Christopher Geach are acknowledged for substantial predecessor-code contributions but are not SkyWinder or software-paper authors, so they are not selected.

Both ORCIDs resolve to the named authors' official ORCID records. Carl's verified ORCID matches his existing HSSI identity, so future maintenance should reuse that identity rather than create a duplicate.

No affiliation is selected for either author. The paper supports Carl's affiliation with `Arizona State University` / `https://ror.org/03efmqc40`, and Bifford's affiliation with the paper name `Global Atmospheric Technologies and Sciences`, an alias of the ROR display `G & A Technical Software (United States)` / `https://ror.org/01rqa9952`. These primary-source-supported alternatives are deliberately omitted from the current author metadata, but a future metadata review may legitimately reconsider them.

### 7. Software Name (MANDATORY)

**Value:** SkyWinder

The repository, README.md heading, setup.py package name, PyPI project, PyHC community entry, and software-paper title all use this name.

### 8. Description (MANDATORY)

**Value:** SkyWinder is an open-source Python package useful for instrument control, telemetry, and image analysis. It is adapted from software that successfully managed flight control, telemetry, preliminary image analysis, and data visualization for a balloon-borne mission and it has broad uses for mid- and upper-atmosphere science instrumentation including aurora, cloud, and airglow imagers. SkyWinder will save future aeronomy experiments significant time and money, and lowers the barrier to entry in analyzing data hosted in public available repositories.

Our software consists of two distinct parts: the flight and analysis modules. The SkyWinder flight package includes modular distributed flight control including telemetry and subsystem coordination for running mobile aeronomy experiments such as balloon-borne payloads, airplanes, sounding rockets, and suborbital reusable launch vehicles (sRLVs), as well as isolated semi-autonomous ground instruments. The SkyWinder analysis software provides functionality more broadly useful in neutral upper atmosphere dynamics, such as pointing reconstruction, image projection, preliminary image processing, and various image analysis techniques.

This established description remains factually consistent with README.md and the published software-paper abstract. The pinned tree contains the flight-control, telemetry, camera, ground-station, and utility portions; the article is the primary evidence for the separately described analysis capabilities.

### 9. Concise Description (OPTIONAL)

**Value:** An open-source Python package for instrument control, telemetry, and image analysis for mid- and upper-atmosphere science instrumentation including aurora, cloud, and airglow imagers.

This concise description accurately condenses the repository description and software-paper scope.

### 10. Publication Date (RECOMMENDED)

**Value:** 2019-11-08

PyPI records public wheel and source-distribution uploads for SkyWinder 0.0.1 on 2019-11-08. This is direct evidence of public availability and predates the repository's 2022 creation/first-commit date, so the earlier package-publication date is selected.

### 11. Publisher (RECOMMENDED)

**Publisher:**

- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

No software DOI repository was found. GitHub hosts the canonical public source and remains the applicable publisher under the form's no-DOI guidance; PyPI is additionally a package distribution channel.

### 12. Version (RECOMMENDED)

- **Version Number:** 0.0.3
- **Version Date:** 2022-09-09
- **Version Description:** Not found
- **Version PID:** Not found

The selected version is the internally consistent published SkyWinder flight package: pinned setup.py declares `0.0.3`, and PyPI's latest distribution is 0.0.3, uploaded on 2022-09-09. The newer reachable annotated tag `v0.0.4` is rejected because the tagged code still declares 0.0.3; GitHub has no corresponding release object, release name, or release body. The separately packaged SkyWinder-Analysis component has independent version history—its source declares 0.0.5 while its latest PyPI distribution is 0.0.2—so those numbers do not replace the selected SkyWinder flight-package version. No selected version has a DOI or release description.

### 13. Programming Language (RECOMMENDED)

**Value:** Python 3.x

Python is the only important implementation language in the pinned tracked tree. README.md requires Python 3.9+, setup.py declares Python 3 and `python_requires >=3.6`, and the current workflow tests Python 3.9. YAML, shell snippets, and configuration/data syntax are ancillary. The deleted historical Travis configuration's Python 2.7 reference is stale and conflicts with the current package and runtime evidence.

### 14. Reference Publication (OPTIONAL)

**Value:** https://doi.org/10.3389/fspas.2023.1023550

Kjellstrand and Williams, “SkyWinder: A Python package for flight control, telemetry, and image analysis,” Frontiers in Astronomy and Space Sciences (2023), directly describes this software's architecture, capabilities, provenance, applications, authorship, and funding. The page represents a journal article, so this DOI belongs here rather than in Field 2.

### 15. License (RECOMMENDED)

- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

LICENSE.md at the pinned revision contains the BSD 3-Clause terms. The name and SPDX URI exactly match the controlled license record; the older opensource.org URL is replaced by this canonical controlled value.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values:**

- aeronomy
- airglow
- aurora
- balloon borne
- flight control
- geospace
- gravity waves
- image
- image analysis
- image processing
- instrument control
- instrumentation
- ionosphere thermosphere mesosphere
- mesosphere
- middle atmosphere
- neutral atmosphere
- planetary
- pmc
- polar mesospheric clouds
- remote sensing
- telemetry
- upper atmosphere

These keywords are supported by the PyHC community entry, README.md, pinned flight modules, software paper, and combined flight-and-analysis scope. `image analysis` and `instrument control` name defining package capabilities; `mesosphere`, `middle atmosphere`, and `neutral atmosphere` describe the stated region and analysis scope; `remote sensing` describes the imager/lidar applications; and `gravity waves` is a central PMC-Turbo science application. Keywords are open vocabulary, so the two terms without pre-existing controlled rows remain valid selections.

### 17. Data Sources (OPTIONAL)

**Values:**

- Observatory/Mission-specific
- Madrigal

`Observatory/Mission-specific` is selected because SkyWinder directly ingests, transmits, stores, and analyzes PMC-Turbo camera/lidar data and is designed for comparable mission instruments. `Madrigal` is selected because the software paper says SkyWinder can be used with imaging and lidar data hosted by the NSF Madrigal database. `CDAWeb` remains excluded: the paper describes future retrieval from NASA SPDF, and the pinned implementation has no such client.

### 18. Input File Formats (RECOMMENDED)

**Values:**

- ascii
- csv
- JSON
- Other

`skywinder/communication/file_format_classes.py` reads text/general files, JSON, compressed JSON, and custom binary containers, while `skywinder/utils/index_watcher.py` reads comma-delimited index files. Camera and telemetry modules read Blosc-compressed images, JPEG payloads, packet streams, and raw instrument records. JSON and csv have exact controlled values; `Other` represents the custom binary, Blosc, JPEG, packet, and raw formats that lack exact controlled rows.

### 19. Output File Formats (RECOMMENDED)

**Values:**

- ascii
- csv
- JSON
- netCDF3/4
- Other

The flight package serializes text/general files, JSON, compressed JSON, and custom binary containers; its ground receiver and error-counter modules write CSV files, and its camera pipeline emits Blosc images and JPEG payloads. Under the selected combined scope, the SkyWinder-Analysis companion provides a user-facing conversion application that writes `NETCDF3_CLASSIC`, represented by the exact controlled value `netCDF3/4`. `JPEG` is not an available FileFormat value and is therefore represented by `Other`, not emitted as a bare near-match.

### 20. Operating System (RECOMMENDED)

**Values:**

- Linux
- Mac

README.md provides macOS and Linux installation instructions, and the workflows test on Linux. The software paper says the flight software was designed and tested on Linux and cautions that alternate systems require substantial expertise. A historical Windows GUI module and the generic setup classifier do not establish full Windows or operating-system-independent support.

### 21. CPU Architecture (RECOMMENDED)

**Value:** CPU Independent

The published wheel is `py3-none-any`, the package is implemented in Python, and no package-level CPU restriction is declared. External instrument interfaces constrain connected hardware rather than the CPU architecture on which SkyWinder runs.

### 22. Related Phenomena (OPTIONAL)

**Value:** Not found

Polar mesospheric clouds, aurora, airglow, gravity waves, and atmospheric turbulence are well-supported science phenomena, but none has an exact value in the closed Phenomena vocabulary. They are represented in Keywords where applicable; unrelated controlled near-matches are not substituted.

### 23. Development Status (RECOMMENDED)

**Value:** Inactive

The applicable controlled definition is:

> The project has reached a stable, usable state but is no longer being actively developed; support/maintenance will be provided as time allows.

SkyWinder has published stable distributions and documented field use, but its latest source commit was 2022-09-28 and its latest source push was 2022-09-29. A later GitHub `updated_at` timestamp reflects repository-metadata activity rather than a code commit. `Unsupported` is not selected because the maintainers do not say that all work has ceased or that users should seek a replacement.

### 24. Documentation (RECOMMENDED)

**Value:** https://github.com/PolarMesosphericClouds/SkyWinder

The repository README provides package scope, installation instructions, acknowledgments, and links. The form permits the access/repository URL when it serves as documentation. No separate documentation site, docs tree, or ReadTheDocs configuration exists.

### 25. Funder (OPTIONAL)

**Funder:**

- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

The software paper assigns NASA Grant `80NSSC20K0178` to PyHC SkyWinder development. README.md's statement that PyHC supported development describes the community context, not a second funding organization. Funders of the predecessor PMC-Turbo mission and later science analyses are not selected as SkyWinder-development funders.

### 26. Award Title (OPTIONAL)

- **Award Title:** NASA grant
- **Award Number:** 80NSSC20K0178

The software paper explicitly says this NASA grant funded PyHC SkyWinder. `NASA grant` is a descriptive API-safe label for the identified award, not an authoritative formal title; no authoritative full award title was found. NASA Contract `80NSSC18K0050` is excluded because the paper assigns it to the precursor PMC-Turbo mission rather than SkyWinder development.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Value:** https://doi.org/10.1029/2020EA001238

“The PMC Turbo Balloon Mission to Measure Gravity Waves and Turbulence in Polar Mesospheric Clouds: Camera, Telemetry, and Software Performance” describes and evaluates the camera, telemetry, ground software, and flight-software precursor refined into SkyWinder. The SkyWinder paper relies on it for architecture and image-viewer evidence and acknowledges the later SkyWinder development grant. The direct SkyWinder article remains in Field 14. The broader PMC-Turbo mission overview `10.1029/2019JD030298`, Kjellstrand thesis `10.7916/d8-az4s-b142`, and later PMC science papers focus on the mission, data, or science rather than the package and are not selected.

### 28. Related Datasets (OPTIONAL)

**Value:** https://doi.org/10.13020/df2m-a470

This repository contains supplementary PMC-Turbo image data for the camera, telemetry, and software-performance paper. SkyWinder was developed from that system and is explicitly designed to process and display those camera data. Dataset `https://doi.org/10.13020/te3n-hj23` is attached to a later science analysis rather than the selected software-performance artifact, so it is not selected.

### 29. Related Software (OPTIONAL)

**Value:** https://github.com/PolarMesosphericClouds/SkyWinder-Analysis

The project's organization publishes SkyWinder-Analysis as the separately installable analysis half of the combined SkyWinder software described by the README and paper. Its package metadata points to the companion repository, and its implementations supply the analysis-specific coordinate transforms, time-series analysis, visualization, and netCDF conversion represented elsewhere in this dossier. Pyro/Pyro4, OpenCV, Pillow, NumPy, Blosc, PySerial, PyModbus, aiohttp, and camera-vendor libraries remain excluded as dependencies or generic infrastructure rather than distinguishing related heliophysics software.

### 30. Interoperable Software (OPTIONAL)

**Value:** https://github.com/dstndstn/astrometry.net

The official SkyWinder-Analysis source identifies Astrometry.net at command level: its pointing tools add an `astrometry.net-0.73` path and invoke `solve-field`, `wcsinfo`, and `wcs-xy2rd` to exchange WCS and right-ascension/declination solutions used by SkyWinder image projection. Astrometry.net's own repository identifies `solve-field` as its solver interface and `dstndstn/astrometry.net` as the development repository. This demonstrated exchange supports interoperability, unlike mere dependency presence. The distinct HSSI item AstrometryAzEl at `https://github.com/space-physics/astrometry_geomap` is rejected because the primary SkyWinder-Analysis code identifies Astrometry.net instead.

### 31. Related Instruments (OPTIONAL)

**Value:** Not found

The pinned source and software paper establish direct work with PMC-Turbo wide- and narrow-field cameras, Rayleigh lidar/BOLIDE telemetry, camera controllers, and housekeeping instruments. None of those candidates resolves to an exact instrument row with a full `https://spase-metadata.org/` identifier in the controlled catalogue. Generic camera/lidar entries and unrelated acronym or definition hits are invalid substitutes. The earlier bare `PMC-Turbo` proposal is rejected because Fields 31–32 are SPASE-only and bare names would create an identifier-less record.

### 32. Related Observatories (OPTIONAL)

**Value:** Not found

PMC-Turbo, SuperTIGER, and BALBOA are supported mission/platform deployments described by the paper, but none resolves to an exact observatory row with a full `https://spase-metadata.org/` identifier. No defensible observatory-level platform fallback was found, so no bare name or generic near-match is selected.

### 33. Logo (OPTIONAL)

**Value:** Not found

The current tracked tree, its ever-added path history, README.md, and the fully parsed PyHC registry entry contain no image/logo asset or logo declaration. The software paper's diagrams, plots, and screenshots are explanatory figures rather than project-presented logos; the GitHub organization avatar is likewise not presented as SkyWinder's logo. There is therefore no viable project asset to commit-pin, fetch as an image, and visually approve.
