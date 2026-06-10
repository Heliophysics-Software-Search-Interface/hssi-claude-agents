# HSSI Metadata Extraction Results

**Repository:** https://github.com/nasa/Kamodo
**Extraction Date:** 2026-06-09 (revised 2026-06-10 after independent validation)
**HSSI Sync:** 2026-06-10 — reconciled with the live HSSI record after a local metadata update (software UUID `13659e76-e911-41da-bf99-30eb7b05defc`). Field values below reflect HSSI: enrichments were applied; for Software Name, Description, Publication Date, Logo, and Related Region the existing HSSI values were kept; License is stored as "Other" (see Field 15).

---

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** Not found
- **Note:** No Zenodo/DataCite *software* concept DOI exists for Kamodo. The Zenodo records `10.5281/zenodo.11121935` / `.11121936` are *presentations* (resource type "Presentation"), not the software. The JOSS software-paper DOI is recorded under Reference Publication (Field 14), not here. Source: README "Citing Kamodo", DataCite/Zenodo API searches.

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/nasa/Kamodo
- **Source:** git remote, `setup.cfg` url/project_urls, PyHC core registry.

### 4. Software Functionality (MANDATORY)
Classified per the software-functionality skill; every subcategory also lists its bare parent top-level category. All values verified against `/api/models/FunctionCategory/rows/all/`.

- **Coordinate Transforms**
- **Coordinate Transforms: Magnetospheric** — `ConvertCoord` in `kamodo_ccmc/flythrough/utils.py` converts among GDZ, GEO, GSM, GSE, SM, GEI, MAG, SPH, RLL via spacepy/PyGeopack.
- **Coordinate Transforms: Heliospheric** — `ConvertCoord` also supports heliocentric ecliptic systems (heliocentricmeanecliptic, heliocentrictrueecliptic, heliocentriceclipticiau76) via astropy (`utils.py` astropy_coordlist).
- **Data Processing and Analysis**
- **Data Processing and Analysis: Data Access and Retrieval** — HAPI client integration (`kamodo_ccmc/hapi/`, `functionalize_hapi.py`), S3 access (`s3fs`/`boto3`), remote CCMC model-output retrieval.
- **Data Processing and Analysis: Analysis** — function composition, derived quantities, model validation / model-data comparison (`Validation/`).
- **Data Processing and Analysis: Processing** — functionalization of model outputs, `reader_utilities.py`.
- **Data Processing and Analysis: File Format Conversion** — `*_tocdf.py` readers convert native model outputs into standardized **netCDF4** intermediate files; `SF_output.py` writes nc/csv/txt.
- **Data Processing and Analysis: Field-line Tracing** — `tools/vectorfieldtracer.py` (magnetic field lines, streamlines), `lastclosedmag.py` (last-closed field lines).
- **Data Processing and Analysis: 2D Slices** — model slice extraction (`tools/plotfunctions.py` `GDZSlice4D`).
- **Data Processing and Analysis: Magnetic Null Finding** — `tools/nullfinder.py` (magnetic null / reconnection-site finder).
- **Data Processing and Analysis: Time Series Analysis** — flythrough time-ordered outputs (`flythrough/SF_output.py` `Functionalize_TimeSeries`).
- **Data Visualization**
- **Data Visualization: 2D Graphics** — plotly/matplotlib 2D contour/map plots (`plotfunctions.py`, `plots.py`).
- **Data Visualization: 3D Graphics** — `SatPlot4D` 3D plotly; 3D field-line rendering.
- **Data Visualization: Line Plots** — 1D / time-series line plots in flythrough plotting routines.
- **Data Visualization: Orbit Plots** — satellite trajectory / orbit visualization (`SatPlot4D`, orbit groupby).
- **Data Visualization: Movies** — time-animated 4D plots (animation/groupby by day/hour/orbit).
- **Data Visualization: Web-Based** — interactive plotly HTML output (`htmlfile`/`divfile`), code-free/web interfaces.
- **Data Visualization: 2D Slices** — slice-plot rendering (`plotfunctions.py` `gm2DSliceFig`/`GDZSlice4D`).
- **Models and Simulations**
- **Models and Simulations: Empirical** — wraps empirical models (IRI, DTM, Weimer, JB2008, Tsyganenko/Geopack).
- **Models and Simulations: Physics-Based** — functionalizes first-principles model outputs Kamodo reads (SWMF/BATSRUS-GM, OpenGGCM-GM, GAMERA-GM); post-processing only, does not run the solvers.
- **Models and Simulations: Field-line Tracing** — traces field lines through model fields (SWMF/BATSRUS, OpenGGCM).
- **Servers and Environments**
- **Servers and Environments: Software or Environment Container** — 8 Dockerfiles under `dockerfiles/` plus `docker-compose.yaml`.
- **Servers and Environments: Data servers processing and handling** — HAPI server implementation in `kamodo_ccmc/hapi/HAPI_KamodoRealFlight.py`.
- **Removed during validation:** "Coordinate Transforms: Ionospheric" (no AACGM/apex; `ConvertCoord` supports only magnetospheric/inertial systems) and "Models and Simulations: Mission-Specific" (the constellation tool is general-purpose, not specific to one mission).
- **Source:** manual code inspection of `kamodo_ccmc/`, README, docs notebooks.

### 5. Related Region (MANDATORY)
- **Earth Atmosphere** — thermosphere/ionosphere/mesosphere models (CTIPe, GITM, IRI, TIE-GCM, WACCM-X, DTM, WAM-IPE).
- **Earth Magnetosphere** — magnetospheric models (SWMF/BATSRUS-GM, OpenGGCM-GM, Tsyganenko, VERB).
- **Note:** Interplanetary Space was considered but dropped during reconciliation (heliosphere coverage is only HAPI-accessible, no dedicated reader); HSSI keeps Earth Atmosphere + Earth Magnetosphere.
- **Source:** README supported-models list, PyHC keywords (magnetosphere, ionosphere_thermosphere_mesosphere).

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Alexander Drozdov
- **Author Identifier:** https://orcid.org/0000-0002-5334-2026
- **Affiliation - Organization:** University of California, Los Angeles
**Author 2:**
- **Name:** Asher Pembroke
- **Author Identifier:** Not found
- **Affiliation - Organization:** Not found
**Author 3:**
- **Name:** Lutz Rastaetter
- **Author Identifier:** https://orcid.org/0000-0002-7343-4147
- **Affiliation - Organization:** Community Coordinated Modeling Center; National Aeronautics and Space Administration
**Author 4:**
- **Name:** Rebecca Ringuette
- **Author Identifier:** https://orcid.org/0000-0003-0875-2023
- **Affiliation - Organization:** Heliophysics Data and Modeling Consortium
**Author 5:**
- **Name:** Darren de Zeeuw
- **Author Identifier:** https://orcid.org/0000-0002-4313-5998
- **Affiliation - Organization:** Calvin College; Goddard Space Flight Center; National Aeronautics and Space Administration; University of Michigan
**Author 6:**
- **Name:** Katherine Garcia-Sage
- **Author Identifier:** https://orcid.org/0000-0001-6398-8755
- **Affiliation - Organization:** Community Coordinated Modeling Center; National Aeronautics and Space Administration
**Author 7:**
- **Name:** Oliver Gerland
- **Author Identifier:** Not found
- **Affiliation - Organization:** Not found
**Author 8:**
- **Name:** Dhruv Patel
- **Author Identifier:** Not found
- **Affiliation - Organization:** Not found
**Author 9:**
- **Name:** Michael Contreras
- **Author Identifier:** Not found
- **Affiliation - Organization:** Not found

- **Note:** Reflects the reconciled HSSI author list (9). Alexander Drozdov was already in the HSSI record (kept). "Lutz Rastaetter" was corrected from the misspelled "Raestatter" and given his ORCID. Garcia-Sage, Gerland, Patel, and Contreras were added from the JOSS paper. Existing authors' ORCIDs/affiliations were preserved; affiliation acronyms expanded (CCMC → Community Coordinated Modeling Center, NASA → National Aeronautics and Space Administration).

### 7. Software Name (MANDATORY)
- **Value:** The CCMC Kamodo Analysis Suite
- **Note:** Kept the HSSI record's full name (matches the README title). The PyHC registry / PyPI use the short forms "Kamodo" / `kamodo_ccmc`. Source: HSSI record, README.

### 8. Description (MANDATORY)
- **Source:** HSSI record (maintainers' README vision statement), reformatted into valid Markdown — dash-space bullets and a blank line before the list — so it renders as a nested bulleted list. The originally-stored text used tab-indented pseudo-bullets that the site's Markdown renderer (`django-markdownify`) collapsed into a run-on paragraph.

**Value (as stored in HSSI):**

Kamodo is an official NASA open-source python package built upon the functionalization of datasets. Once a dataset is functionalized in Kamodo, several important capabilities are then available to the user, including data analysis via function composition, automatic unit conversions, and publication quality graphics all using intuitive and simplistic syntax. By applying these capabilities to heliophysics model outputs, we aim to:

- Drastically simplify the currently complex data utilization process for model outputs,
- Provide interactive access to functionalized model outputs for users ranging in programming skill from beginners – via code-free interfaces and video tutorials – to advanced users – via thorough documentation, Jupyter notebook examples and sample workflows,
- Layer multiple functionalities on top of the functionalized model outputs, all with model-agnostic and uniform syntax, including but not limited to:
    - Flythrough tools,
    - Vector field tracing (including magnetic field mapping),
    - Coordinate conversions,
    - Domain-specific interactive plots of publication quality,
    - Modular driver swapping,
    - Satellite constellation mission planning tools,
    - Simulated imagery, and
    - A line of sight calculation tool,
- Greatly reduce the programming skill currently required outside of Kamodo to perform model validation studies and model-data comparisons,
- Enable model output utilization both on the cloud and on personal laptops in a variety of methods (e.g. through HAPI and interactive calls from the command line),
- Streamline the CCMC user workflow by becoming interoperable with other CCMC services (e.g. CAMEL and the various scoreboards),
- And become the next generation interface for CCMC users to interact with and analyze model outputs (e.g. through ROR and IR),

...all while keeping the developed software open-source and freely available. The Kamodo team also supports the heliophysics community by pursuing interoperability with commonly-used python packages, collaborating with community members to add model outputs and new functionalities, and remaining involved with community events (e.g. conferences, challenges, and research support). As the library of supported model outputs types expands and new model-agnostic tools are added, Kamodo will become a staple software package in the heliophysics community to transform current workflows into a more efficient and productive process. We are building the next generation of capability with Kamodo. Join us!

### 9. Concise Description (OPTIONAL)
- **Value:** A functional Python API from NASA's Community Coordinated Modeling Center for accessing, interpolating, unit-converting, and visualizing heliophysics/space-weather model outputs and data.
- **Source:** `setup.cfg` description plus README, condensed.

### 10. Publication Date (RECOMMENDED)
- **Value:** 2019-08-06
- **Note:** Kept the HSSI value (GitHub repo creation = first public availability). The JOSS software paper (2022-07-14) is recorded as the Reference Publication (Field 14). Source: HSSI record, GitHub API.

### 11. Publisher (RECOMMENDED)
- **Organization:** Community Coordinated Modeling Center
- **Note:** Kamodo is published/hosted by NASA's CCMC (github.com/nasa). No Zenodo registrant applies (no software DOI). Source: README, repository owner.

### 12. Version (RECOMMENDED)
- **Version Number:** 25.12.1
- **Version Date:** 2025-12-01 (inferred from the CalVer `25.12.1`; no git tag exists in the clone to confirm)
- **Version Description:** Not found
- **Version PID:** Not found
- **Source:** `setup.cfg` version.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** — primary language (`python_requires >= 3.10`).
- **C** — compiled reader components: `kamodo_ccmc/readers/OCTREE_BLOCK_GRID/*.c`, `kamodo_ccmc/readers/Tri2D/*.c`.
- **C++** — `kamodo_ccmc/kamodo-wrapper/KamodoWrapper.cpp`.
- **Fortran90** — `kamodo_ccmc/kamodo-wrapper/FortranWrapper.f90`, `main.f90`.
- **Fortran77** — OpenGGCM reader sources (`kamodo_ccmc/readers/OpenGGCM/readmagfile3d.f`, `DBGDEV.F`).
- **Source:** `setup.cfg` classifiers, direct inspection of repository source files. (Removed "Jupyter Notebook" and bare "Python" — not controlled-list values.)

### 14. Reference Publication (OPTIONAL)
- **Value:** https://doi.org/10.21105/joss.04053
- **Citation:** Pembroke, A., De Zeeuw, D., Rastaetter, L., Ringuette, R., Gerland, O., Patel, D., & Contreras, M. (2022). Kamodo: A functional API for space weather models and data. *Journal of Open Source Software*, 7(75), 4053.
- **Source:** README "Citing Kamodo", JOSS.

### 15. License (RECOMMENDED)
- **License:** NASA Open Source Agreement Version 1.3
- **SPDX ID:** NASA-1.3
- **HSSI value:** `Other` — HSSI's License controlled list has no NASA Open Source Agreement entry, so the record stores "Other". This file documents the actual license (NASA-1.3).
- **Note:** `setup.cfg` license = "NASA OPEN SOURCE AGREEMENT VERSION 1.3"; LICENSE file is NOSA v1.3 (Government Agency Original Software Designation GSC-18210-1, "Kamodo Analysis Suite"). Source: LICENSE, `setup.cfg`.

### 16. Keywords (OPTIONAL)
heliophysics, space weather, model output, functionalization, unit conversion, interpolation, visualization, satellite flythrough, coordinate transformation, field-line tracing, ionosphere, thermosphere, magnetosphere, heliosphere, HAPI, model-data comparison, constellation mission planning
- **Note:** Bare acronyms "CCMC" and "NASA" removed (they are captured in Funder/Publisher). Source: PyHC registry keywords + README.

### 17. Data Sources (OPTIONAL)
- **HAPI** — any HAPI server (Heliophysics Application Programmer's Interface).
- **S3/Cloud-aware** — cloud-hosted model outputs via s3fs/boto3.
- **HTTP/HTTPS Directories** — CCMC web-hosted model-output archives (e.g. https://ccmc.gsfc.nasa.gov/RoR_WWW/output_files/KAMODO_DEMO/).
- **Source:** README Resources, hapi reader, s3fs/boto3 dependencies. (Mapped to controlled-list terms.)

### 18. Input File Formats (RECOMMENDED)
- **netCDF3/4** — primary model-output and intermediate format (`.nc`).
- **HDF5** — `.h5` model outputs (h5py / h5netcdf).
- **ascii** — text/.dat/.txt model output files.
- **Other** — assorted native binary model outputs (`.bin`) and model-specific formats.
- **Note:** "CDF" removed — the `*_tocdf.py` readers write **netCDF4** (`Dataset(..., format='NETCDF4')`), not SPDF CDF; cdflib is unused in the source. Source: `kamodo_ccmc/readers/` code.

### 19. Output File Formats (RECOMMENDED)
- **netCDF3/4** (`.nc`)
- **csv** (`.csv`)
- **ascii** (`.txt`)
- **Other** — interactive plotly HTML and static image exports (via kaleido).
- **Source:** `kamodo_ccmc/flythrough/SF_output.py` writers, plotly/kaleido usage. (Replaced free-text "Interactive HTML / Plotly figures" with `Other`.)

### 20. Operating System (RECOMMENDED)
- **Operating System Independent**
- **Note:** `setup.cfg` classifier "Operating System :: OS Independent"; Docker support present. Source: `setup.cfg`.

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**
- **Note:** No CPU-architecture constraint declared for the Python package; compiled reader components (C/Fortran in OpenGGCM/octree, numba JIT) are built per-platform. Source: package analysis.

### 22. Related Phenomena (OPTIONAL)
- Space weather
- Geomagnetic activity / geomagnetic storms
- Ionospheric variability
- Thermospheric density (satellite drag)
- Auroral electrodynamics (ADELPHI/AMGeO/SuperDARN)
- Radiation belt dynamics (VERB)
- **Source:** inferred from supported models and reader modules.

### 23. Development Status (RECOMMENDED)
- **Active**
- **Note:** Last commit 2026-05-21; CalVer 25.12.1; PyHC core package, "Good" software-maturity rating. Source: git log, PyHC registry.

### 24. Documentation (RECOMMENDED)
- **Value:** https://nasa.github.io/Kamodo/
- **Additional:** in-repo `docs/` notebook tutorials, `Tutorials/`, `QuickStart.md`, CCMC page https://ccmc.gsfc.nasa.gov/tools/kamodo/, YouTube tutorial playlist.
- **Source:** README, `setup.cfg` project_urls, mkdocs.yml.

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80
- **Note:** Official NASA open-source package developed at NASA's CCMC; no separate grant/award number stated. Source: README, LICENSE (Government Agency: National Aeronautics and Space Administration).

### 26. Award Title (OPTIONAL)
- **Value:** Not found
- **Note:** No award/grant number stated; implicit NASA institutional funding.

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.3389/fspas.2022.1005977 — Ringuette et al. (2022), "Kamodo's model-agnostic satellite flythrough", *Frontiers in Astronomy and Space Sciences*, 9.
- https://doi.org/10.48550/arxiv.2303.00854 — Ringuette et al. (2023), "Simplifying model data access and utilization" (arXiv preprint).
- **Source:** README "Citing Kamodo".

### 28. Related Datasets (OPTIONAL)
Heliophysics model outputs supported as input: ADELPHI, AMGeO, CTIPe, DTM, GITM, IRI, OpenGGCM-GM, SuperDARN, SWMF-IE, SWMF-GM, TIE-GCM, WACCM-X, WAM-IPE, Weimer; plus GAMERA-GM, SAMI3, Enlil, VERB, JB2008; and any dataset accessible via HAPI. Sample outputs: https://ccmc.gsfc.nasa.gov/RoR_WWW/output_files/KAMODO_DEMO/
- **Source:** README supported-models list, `kamodo_ccmc/readers/`, PyHC keywords.

### 29. Related Software (OPTIONAL)
- **kamodo-core** — https://pypi.org/project/kamodo-core/ — the core functionalization library that `kamodo_ccmc` is built on (required dependency).
- **SGP4** — https://github.com/brandon-rhodes/python-sgp4 — used by `flythrough/SatelliteFlythrough.py` to propagate satellite orbits from TLEs for the flythrough / constellation tools.
- **PyGeopack** — https://github.com/mattkjames7/PyGeopack — backend for Kamodo's Tsyganenko magnetic-field model reader (`readers/kamodo-tsyganenko/`).
- **Note:** SpacePy, Astropy, and hapiclient are runtime dependencies (coordinate conversions, time, HAPI access) rather than separately-related software, so they are not listed here. pysat is recorded under Interoperable Software (Field 30).
- **Source:** `setup.cfg` install_requires, code imports.

### 30. Interoperable Software (OPTIONAL)
- **pysat** — https://github.com/pysat/pysat
- **Note:** `kamodo-pysat.yaml` in the repo demonstrates a Kamodo↔pysat interoperability environment.

### 31. Related Instruments (OPTIONAL)
- **Value:** Not found
- **Note:** Kamodo operates on model outputs rather than specific instruments.

### 32. Related Observatories (OPTIONAL)
- **Value:** Not found
- **Note:** No specific observatory is named as a related resource.

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/nasa/Kamodo/master/docs/notebooks/Files/Kamodo.png
- **Note:** Kept the HSSI record's logo. The repo also has `logos/Kamodo1/2/3.png` (PyHC registry references Kamodo2.png). Source: HSSI record, repository.

---

## Extraction Notes / Caveats

- **Field numbering corrected (2026-06-10):** the original extraction had fields offset from #10 onward and included non-standard "PyHC Package" / "CCMC Affiliation" entries; this revision follows the canonical 33-field HSSI order and removes the non-standard fields.
- **No software DOI:** no Zenodo/DataCite *software* concept DOI exists (the Zenodo records found are presentations). The JOSS paper DOI is recorded as the Reference Publication (14), and Persistent Identifier (2) is left blank.
- **No CITATION.cff / codemeta.json / .zenodo.json** in the repo — authors/DOIs assembled from `setup.cfg`, README, the JOSS paper, code headers, and the PyHC registry.
- **Name reconciliation:** extraction uses "Kamodo"; the live HSSI record uses "The CCMC Kamodo Analysis Suite" — to be resolved during the update.
- **No git tags** in the clone; version `25.12.1` (CalVer) from `setup.cfg`.
