# HSSI Metadata Extraction Results

**HSSI Software ID:** 43700827-e657-4937-ae69-c333b70d3756
**Repository:** https://github.com/mshumko/asilib
**Source Revision:** 79d166a17c5a25a70fad1dee8294fad21e04c7b5
**Extraction Date:** 2026-07-26
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** To be filled by actual submitter
- **Submitter Email:** To be filled by actual submitter
- **Source Note:** Submitter information is not present in the public HSSI view record or source repository.

### 2. Persistent Identifier (RECOMMENDED)
- https://doi.org/10.5281/zenodo.4746446
- **Source Note:** The repository README, DataCite, and Zenodo confirm this as the concept DOI.

### 3. Code Repository (MANDATORY)
- https://github.com/mshumko/asilib
- **Source Note:** Confirmed by the repository remote, README, PyPI metadata, Zenodo, and the PyHC community registry.

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Field-line Tracing
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Movies
- Data Visualization:Orbit Plots
- **Source Note:** Repository code, public APIs, docs, examples, and tests show remote ASI data access; PGM/HDF5/IDL SAV/raw image loading; image masking, contrast adjustment, downsampling, mosaicking, and keogram/time-series analysis; fisheye and mapped 2D plots; availability and intensity line plots; PNG/MP4 animation generation; satellite-track visualization; AACGM ionospheric-coordinate conversion; and IRBEM magnetic-footprint and magnetic-equator mapping. Every selected subcategory includes its required parent. Mission-related was considered and excluded because the README expressly says asilib is not associated with instrument development or operations. Spectrogram was considered and excluded because a keogram is a time-versus-position image, not a time-frequency representation.

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere
- Earth Auroral Subregion
- Earth Ionosphere
- Earth Thermosphere
- **Source Note:** The repository explicitly supports upper-atmosphere/ionosphere auroral imaging, satellite-to-aurora conjunction analysis, magnetic-footprint tracing, and mapping auroral images to the magnetic equator. `Earth Auroral Subregion` is supported by `asilib/asi/themis.py:2`, which describes white-light aurora observations covering a large section of the auroral oval. `Earth Ionosphere` is supported by `docs/tutorials/magnetic_equator.ipynb:14`, which maps a TREx mosaic from the ionosphere to the magnetic equator. `Earth Thermosphere` is supported by `asilib/asi/mango.py:2`, which describes MANGO observations of nighttime thermosphere-ionosphere dynamics at thermospheric emission altitudes.

### 6. Authors (MANDATORY)
- **Author:** Cassandra Litwinowich
  - **Author Identifier:** https://orcid.org/0009-0002-1171-4415
  - **Affiliation:** University of Alberta
  - **Affiliation Identifier:** https://ror.org/0160cpw27
- **Author:** Mykhaylo Shumko
  - **Author Identifier:** https://orcid.org/0000-0002-0437-7521
  - **Affiliation:** Johns Hopkins University Applied Physics Laboratory
  - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Source Note:** The current Zenodo concept record confirms both creators and affiliations; `pyproject.toml` and SoMEF also confirm Mykhaylo Shumko. The names and RORs shown here identify the affiliation organizations. No CITATION.cff, codemeta.json, AUTHORS, or CONTRIBUTORS file is present.

### 7. Software Name (MANDATORY)
- asilib
- **Source Note:** Confirmed by the README title, `pyproject.toml`, PyPI, SoMEF, and the PyHC community registry.

### 8. Description (MANDATORY)
asilib is an open source package providing data access and analysis tools for the world's all-sky imager (ASI) data.

The purpose of this project is to combine data from numerous observational ASI arrays into a single unified framework and is thus not associated with the development and operations of all sky cameras, or the curation of ASI datasets. All data is publicly available and is provided as-is. Please give appropriate credit and coordinate with instrument teams with regards to data issues and/or interpretation.

It provides unified loaders for THEMIS, REGO, TREx NIR and RGB, MANGO, the Pulsating Aurora Project, and LAMP-supporting all-sky imagers; image and skymap access; fisheye and mapped-image plotting; multi-imager mosaics and animations; keograms; ASI-satellite conjunction and auroral-intensity analysis; magnetic-footprint tracing; and magnetic-equator projection.

- **Source Note:** The first two paragraphs come from the repository README, and the capability summary is supported by the current public API, docs, examples, and tests. An earlier HSSI description appended the old `Changed / Standardized download exception handling` fragment; it is omitted because it is stale v0.26.x changelog text rather than part of the software description.

### 9. Concise Description (OPTIONAL)
asilib is an open source package providing data access and analysis tools for the world's all-sky imager (ASI) data.
- **Source Note:** The repository and PyHC description, 116 characters. An earlier HSSI concise description appended stale release-note text; the substantive repository wording is used without that fragment.

### 10. Publication Date (RECOMMENDED)
- 2021-02-14
- **Source Note:** The date of the repository's first versioned release tag, `v0.1.0`. This corrects existing HSSI `2025-05-30`, which corresponds to a much later v0.26.x-era release rather than initial publication.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source Note:** Confirmed by DataCite and Zenodo for the concept DOI.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.30.1fix
- **Version Date:** 2026-02-19
- **Version Description:** Adds `asilib.asi.trex_rgb_available()` and `asilib.asi.plot_trex_rgb_available()` for finding and plotting TREx-RGB data availability for a time or time range, with tests and no-data handling.
- **Version PID:** https://doi.org/10.5281/zenodo.18690991
- **Source Note:** Supersedes existing HSSI `v0.26.5`. As of extraction, `v0.30.1fix` is the newest non-draft, non-prerelease GitHub release and newest Zenodo concept version, published 2026-02-19. DataCite reports version `v0.30.1fix` and Zenodo version DOI `10.5281/zenodo.18690991`. PyPI and `pyproject.toml` use the package version `0.30.1`; the `fix` suffix distinguishes the authoritative GitHub/Zenodo release tag that published that package version. The source revision is seven commits after this release and does not declare a newer version.

### 13. Programming Language (RECOMMENDED)
- Other
- Python 3.x
- **Source Note:** `Python 3.x` is confirmed by `pyproject.toml` (`requires-python >=3.11`, classifiers for 3.11–3.14), PyPI, CI, and the source. `Other` is supported editorial metadata consistent with substantial versioned Jupyter Notebook and TeX content reported by the GitHub/SoMEF language analysis.

### 14. Reference Publication (RECOMMENDED)
- https://doi.org/10.3389/fspas.2022.1009450
- **Source Note:** The repository documentation explicitly asks users to cite this paper as the publication describing asilib. The earlier `http` DOI URL is normalized to `https`.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html
- **Source Note:** Confirmed by `pyproject.toml` (`BSD-3-Clause`), the three-condition LICENSE text, GitHub license metadata, DataCite, and Zenodo. SoMEF's file-text classifier also emitted a conflicting `BSD-2-Clause` label, but its GitHub and package parsers identify BSD-3-Clause; the authoritative package metadata and actual three conditions resolve the conflict in favor of BSD-3-Clause.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- Aurora
- Image Processing
- Physics
- Python
- Space Physics
- Themis
- All-sky imager
- Ionosphere
- Thermosphere
- Mesosphere
- Data Access
- Data Analysis
- REGO
- TREx
- MANGO
- Pulsating Aurora
- IGRF
- Keogram
- Auroral conjunctions
- Magnetic field-line tracing
- **Source Note:** The PyHC community registry supplies `ionosphere_thermosphere_mesosphere`, data access/analysis, instrumentation, THEMIS, and IGRF concepts; `pyproject.toml`, README, docs, modules, and tests support the ASI-network and analysis terms. Low-information PyHC terms `general`, `remote`, and `plotting` were considered and omitted.

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- Observatory/Mission-specific
- **Source Note:** Source modules directly download from University of Calgary Space Environment Canada directories for THEMIS, REGO, and TREx; the MANGO archive; and Nagoya University PsA/LAMP archives. These are named network/instrument sources, so `Observatory/Mission-specific` is selected in addition to the transport mechanism.

### 18. Input File Formats (RECOMMENDED)
- ascii
- HDF5
- IDL.sav
- Other
- **Source Note:** The public loaders parse ASCII calibration/skymap text, HDF5 and MATLAB v7.3/HDF5 files, IDL SAV image/skymap files, and array-specific PGM/PGM.gz/PGM.bz2, PNG/tar, raw.bz2, and related image/calibration formats represented by `Other`. Repository code and tests provide direct file-level evidence.

### 19. Output File Formats (RECOMMENDED)
- Other
- **Source Note:** The public animation APIs write PNG frames and MP4 movies via Matplotlib and FFmpeg. Neither is a dedicated option in the HSSI output-format vocabulary, so they are represented by `Other`. Array-returning analysis methods do not themselves write a listed scientific file format.

### 20. Operating System (RECOMMENDED)
- Operating System Independent
- **Source Note:** The package is distributed as a universal `py3-none-any` wheel, uses platform-neutral Python/path APIs, and contains explicit Windows handling for FFmpeg errors. Linux is continuously tested. No evidence of an architecture- or operating-system restriction appears in package metadata.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent
- **Source Note:** PyPI publishes a universal `py3-none-any` wheel and the source contains no architecture-specific implementation requirement. Compiled third-party dependencies may supply platform wheels, but asilib itself is CPU independent.

### 22. Related Phenomena (OPTIONAL)
- Not found
- **Source Note:** Aurora, pulsating aurora, substorms, STEVE, airglow, and geomagnetic-storm applications are strongly evidenced by the repository, but none except `Geomagnetic Storms` appears in the localhost controlled vocabulary, and the only geomagnetic-storm occurrence is a MANGO tutorial example rather than a package-wide design target. No controlled term is therefore asserted. `Aurora` and `Pulsating Aurora` remain represented as keywords rather than creating an unpatchable controlled-list value.

### 23. Development Status (RECOMMENDED)
- Active
- **Source Note:** The repository has a stable 0.30.1 release, recent release activity through 2026-02-19, additional commits through 2026-06-25, active CI for Python 3.11–3.13, and PyHC `Good` software-maturity/community ratings.

### 24. Documentation (RECOMMENDED)
- https://aurora-asi-lib.readthedocs.io/
- **Source Note:** Confirmed by the README, `pyproject.toml`, SoMEF, and the PyHC community registry.

### 25. Funder (OPTIONAL)
- Not found
- **Source Note:** Data-network acknowledgements name the National Science Foundation, Canada Foundation for Innovation, and Canadian Space Agency, and the reference paper lists broader author/AuroraX support. These sources fund supported instruments, datasets, authors, or the broader AuroraX effort; they do not unambiguously identify a funder of asilib itself. They are not promoted into the software Funder field without software-specific evidence.

### 26. Award Title (OPTIONAL)
- Not found
- **Source Note:** Award identifiers in network acknowledgements (including AGS-1933013 and 23SUGOSEC) support MANGO/REGO/TREx instrumentation and operations, not unambiguously asilib development, so they are excluded from the software Award field.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Not found
- **Source Note:** The developer-prioritized asilib publication is already recorded as the Reference Publication. Scientific papers cited in examples/tests describe auroral events, instruments, coordinate systems, or dependencies rather than additional publications describing or prioritizing the software, so they are not duplicated here.

### 28. Related Datasets (OPTIONAL)
- **THEMIS all-sky imager archive:** https://data.phys.ucalgary.ca/sort_by_project/THEMIS/asi/stream0/
- **Redline Emission Geospace Observatory archive:** https://data.phys.ucalgary.ca/sort_by_project/GO-Canada/REGO/stream0/
- **Transition Region Explorer NIR archive:** https://data.phys.ucalgary.ca/sort_by_project/TREx/NIR/stream0/
- **Transition Region Explorer RGB archive:** https://data.phys.ucalgary.ca/sort_by_project/TREx/RGB/stream0/
- **Mid-latitude All-sky-imaging Network for Geophysical Observations archive:** https://data.mangonetwork.org/data/transport/mango/archive/
- **Pulsating Aurora Project archive:** https://ergsc.isee.nagoya-u.ac.jp/psa-gnd/pub/raw/
- **LAMP-supporting PsA archive:** https://ergsc.isee.nagoya-u.ac.jp/psa-pwing/pub/raw/lamp/
- https://doi.org/10.34515/DATA.GND-0059-0006-0201_v01
- https://doi.org/10.34515/DATA.GND-0049-0006-0202_v01
- https://doi.org/10.34515/DATA.GND-0059-0006-0203_v01
- https://doi.org/10.34515/DATA.GND-0062-0006-0204_v01
- https://doi.org/10.34515/DATA.GND-0059-0006-0205_v01
- https://doi.org/10.34515/DATA.GND-0022-0006-0206_v01
- https://doi.org/10.34515/DATA.GND-0013-0006-0207_v01
- https://doi.org/10.34515/DATA.GND-0040-0006-0208_v01
- **Source Note:** The archive URLs are the exact public dataset roots encoded in the array-specific source modules. The eight DOI URLs are the authoritative camera datasets listed in the PsA rules-of-the-road, mapped in camera order to the repository's site table: C1 Tromsø (0201), C2 Sodankylä (0202), C3 Tromsø 844.6 nm (0203), C4 Tjautjas (0204), C5 Tromsø 427.8 nm (0205), C6 Kevo (0206), C7 Gakona (0207), and C8 Poker Flat (0208). No DataCite dataset DOI is supplied by the repository for the complete THEMIS, REGO, TREx, MANGO, or LAMP archive roots. The MANGO instrument paper DOI is kept out of this field because it is a publication, not a dataset PID.

### 29. Related Software (OPTIONAL)
- https://github.com/aurorax-space/pyaurorax
- https://github.com/ucalgary-aurora/themis-imager-readfile
- https://github.com/ucalgary-aurora/rego-imager-readfile
- https://github.com/ucalgary-aurora/trex-imager-readfile
- **Source Note:** PyAuroraX is the companion AuroraX client described alongside asilib in the reference publication. The three University of Calgary array-specific readfile packages are explicitly credited by the asilib documentation and perform closely related, distinguishing ASI-read tasks. Generic infrastructure and plotting dependencies (NumPy, SciPy, pandas, Matplotlib, Cartopy, OpenCV, HDF5 plumbing, Requests, FFmpeg, and packaging/testing tools) were considered and excluded under the strict relevance gate.

### 30. Interoperable Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.6867552
- https://github.com/aburrell/aacgmv2
- **Source Note:** IRBEM-Lib passes the interoperability gate through the documented `Conjunction.lla_footprint()` and `Imagers.map_eq()` APIs, which call IRBEM magnetic-field models and consume their coordinate outputs. AACGMV2 passes through the documented `plot_keogram(..., aacgm=True)`/keogram-latitude path, which converts geodetic inputs into AACGM magnetic latitude. `cdasws` was considered but excluded because it appears only in a MANGO plotting example, and no asilib data-model exchange or adapter is implemented. PyAuroraX is related but not interoperable in current code (`pyaurorax` support remains a TODO).

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** THEMIS Ground Athabasca All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/ATHA/ASI
- **Instrument Name:** THEMIS Ground Chibougamau All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/CHBG/ASI
- **Instrument Name:** THEMIS Ground Ekati All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/EKAT/ASI
- **Instrument Name:** THEMIS Ground Fort Simpson All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/FSIM/ASI
- **Instrument Name:** THEMIS Ground Fort Smith All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/FSMI/ASI
- **Instrument Name:** THEMIS Ground Fort Yukon All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/FYKN/ASI
- **Instrument Name:** THEMIS Ground Gakona All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/GAKO/ASI
- **Instrument Name:** THEMIS Ground Goose Bay All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/GBAY/ASI
- **Instrument Name:** THEMIS Ground Gillam All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/GILL/ASI
- **Instrument Name:** THEMIS Ground Inuvik All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/INUV/ASI
- **Instrument Name:** THEMIS Ground Kapuskasing All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/KAPU/ASI
- **Instrument Name:** THEMIS Ground Kiana All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/KIAN/ASI
- **Instrument Name:** THEMIS Ground Kuujjuaq All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/KUUJ/ASI
- **Instrument Name:** THEMIS Ground McGrath All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/MCGR/ASI
- **Instrument Name:** THEMIS Ground Narsarsuaq All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/NRSQ/ASI
- **Instrument Name:** THEMIS Ground Prince George All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/PGEO/ASI
- **Instrument Name:** THEMIS Ground Rankin Inlet All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/RANK/ASI
- **Instrument Name:** THEMIS Ground Sanikiluaq All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/SNKQ/ASI
- **Instrument Name:** THEMIS Ground Snap Lake All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/SNAP/ASI
- **Instrument Name:** THEMIS Ground Taloyoak All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/TALO/ASI
- **Instrument Name:** THEMIS Ground The Pas All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/TPAS/ASI
- **Instrument Name:** THEMIS Ground White Horse All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/WHIT/ASI
- **Instrument Name:** THEMIS Ground Yellowknife All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/YKNF/ASI
- **Instrument Name:** Near Infrared All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/TREX/NIRASI
- **Instrument Name:** Red-Green-Blue All Sky Imager
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/TREX/RBGASI
- **Instrument Name:** All-sky EMCCD imager with a 845nm filter at Tromso, Norway
  - **Instrument Identifier:** https://spase-metadata.org/IUGONET/Instrument/ISEE/EMCCD/TRS/EMCCD_845nm
- **Instrument Name:** All-sky EMCCD imager with a 428nm filter at Tromso, Norway
  - **Instrument Identifier:** https://spase-metadata.org/IUGONET/Instrument/ISEE/EMCCD/TRS/EMCCD_428nm
- **Source Note:** The 23 THEMIS station instruments, two TREx instruments, and two PsA instruments map to the canonical names and stable SPASE identifiers shown above; non-`.html` identifiers are preferred. They correspond to public loaders and supported locations in `asilib/data/asi_locations.csv`.
- **PsA Resolution Note:** Only C3 (Tromsø, 844.6 nm) maps to `All-sky EMCCD imager with a 845nm filter at Tromso, Norway`, and C5 (Tromsø, 427.8 nm) maps to `All-sky EMCCD imager with a 428nm filter at Tromso, Norway`. C1, C2, C4, C6, C7, and C8 use BG3 filters and are omitted from Field 31 because no safe exact SPASE match exists; same-site RG665 or generic instrument rows are not assumed equivalent. The identifierless aggregate PsA instrument candidate remains excluded, and the identifierless PsA observatory is omitted from Field 32 under the SPASE-only policy.
- **REGO Resolution Note:** A separate REGO Field 31 instrument is omitted. `Redline Emission Geospace Observatory` at `https://spase-metadata.org/SMWG/Observatory/REGO` is an observatory resource; a `.html` duplicate named `Redline Emission Geospace Observatory (REGO)` is not a defensible distinct instrument because it normalizes to the same observatory resource. The canonical bare observatory resource remains in Field 32.
- **SPASE-only Exclusion Note:** Merged hssi-website PR #54 (`https://github.com/Heliophysics-Software-Search-Interface/hssi-website/pull/54`) removed legacy non-SPASE instrument/observatory rows and requires omission when no legitimate SPASE equivalent exists. `MANGO all-sky imagers` and `LAMP-supporting Phantom and EMCCD all-sky imagers` remain relevant to asilib but are omitted from Field 31 because neither has an exact SPASE instrument match.
- **Exclusion Note:** The unused TREx Blue constants/location table were considered but excluded because no public loader or exported API supports the distinct Blue ASI; selecting the blue color channel of TREx RGB still uses the RGB instrument.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Redline Emission Geospace Observatory
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/REGO
- **Observatory Name:** Transition Region Explorer
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/TREX
- **Source Note:** REGO and TREx use canonical non-`.html` SPASE observatory identifiers.
- **THEMIS Resolution Note:** An aggregate THEMIS Field 32 observatory is omitted because no controlled aggregate accurately covers the complete supported ground ASI network. Candidates cover different or misleading scopes, including `NASA THEMIS GBO Ground Stations` (`https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/UCLA-GBO`) and `THEMIS-Associated Ground Magnetometer Stations` (`https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground`), plus separate CANMAG/station rows. All 23 supported station ASI instruments remain individually resolved in Field 31. The spacecraft `THEMIS` observatory row remains excluded because asilib supports ground ASI data, not the spacecraft observatory as such.
- **SPASE-only Exclusion Note:** Under merged hssi-website PR #54, `Mid-latitude All-sky-imaging Network for Geophysical Observations (MANGO)`, `Pulsating Aurora (PsA) Project`, and `Loss through Auroral Microburst Pulsations (LAMP) sounding rocket` are omitted from Field 32 because no legitimate exact SPASE observatory equivalent exists. Their omission from this controlled field does not remove the supported networks/missions from other appropriate metadata fields.

### 33. Logo (OPTIONAL)
- https://raw.githubusercontent.com/mshumko/asilib/79d166a17c5a25a70fad1dee8294fad21e04c7b5/docs/_static/asilib_logo.png
- **Source Note:** The asset designated by the manually curated PyHC community registry, confirmed as a live PNG at the pinned revision (which is this record's Source Revision). The registry's own `logo:` string references the default branch; the URL here pins the commit instead, since a branch reference breaks silently on any upstream rename, move or deletion. The repository also contains an SVG version.
