# HSSI Resource Submission Form Fields

This document describes all fields in the Heliophysics Software Search Interface (HSSI) Resource Submission Form. The form is divided into three sections: basic information, additional data, and additional metadata.

## Form Structure

The form collects metadata about heliophysics software packages for inclusion in the HSSI website. Fields are marked as:
- **MANDATORY** - Required to submit the form
- **RECOMMENDED** - Strongly encouraged
- **OPTIONAL** - Not required but helpful

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
**Type:** Nested group with text and email fields

**What it is:** The name and email address of the person submitting the metadata.

**How to fill it:**
- **Submitter Name:** Given name, initials, and last/surname (e.g., Jack L. Doe)
- **Submitter Email:** Work email address (can add multiple)

---

### 2. Persistent Identifier (RECOMMENDED)
**Type:** DataCite DOI lookup with autofill

**What it is:** The globally unique persistent identifier for the software (e.g., the concept DOI for all versions).

**How to fill it:** If the software already has a concept DOI, enter the full DOI here (e.g., https://doi.org/10.5281/zenodo.13287868). Entering the concept DOI enables automatic population of metadata from that DOI.

---

### 3. Code Repository (MANDATORY)
**Type:** URL with repository autofill (SoMEF)

**What it is:** Link to the repository where the un-compiled, human readable code and related code is located (SVN, GitHub, CodePlex, institutional GitLab instance, etc.). If the software is restricted, put a link to where a potential user could request access.

**How to fill it:** Navigate to the root page of your repository, copy the entire link, and paste it into this field.

---

### 4. Software Functionality (MANDATORY)
**Type:** Multi-select dropdown

**What it is:** The type of software.

**How to fill it:** Select all types of software functionalities that apply to the software.

**Possible Values:**
- Coordinate Transforms
- Coordinate Transforms:Heliospheric
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Coordinate Transforms:Mission-Specific
- Coordinate Transforms:Planetary
- Coordinate Transforms:Solar
- Data Processing and Analysis
- Data Processing and Analysis:2D Slices
- Data Processing and Analysis:3D Particle Distribution Processing
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Curlometer
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Assimilation
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:Field-line Tracing
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Linear Gradient Estimation
- Data Processing and Analysis:Magnetic Null Finding
- Data Processing and Analysis:ML/AI
- Data Processing and Analysis:Packet Decommutation
- Data Processing and Analysis:Pitch Angle Distributions
- Data Processing and Analysis:Plasma Moments
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Spectrogram
- Data Processing and Analysis:Time Series Analysis
- Data Processing and Analysis:Wave Polarization Analysis
- Data Processing and Analysis:Wavelet Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:2D Slices
- Data Visualization:3D Graphics
- Data Visualization:Hodograms
- Data Visualization:Line Plots
- Data Visualization:Mission-Specific
- Data Visualization:ML/AI
- Data Visualization:Movies
- Data Visualization:Orbit Plots
- Data Visualization:Spacecraft Formation Plots
- Data Visualization:Spectrogram
- Data Visualization:Web-Based
- Mission-related
- Mission-related:Analysis
- Mission-related:Archive
- Mission-related:Calibration
- Mission-related:Distribution/Access
- Mission-related:Infrastructure as Code
- Mission-related:Ingest
- Mission-related:Instrumentation
- Mission-related:Instrument Response
- Mission-related:Inventory
- Mission-related:ML/AI
- Mission-related:Monitoring
- Mission-related:Observatory/Instrument Models
- Mission-related:Operations
- Mission-related:Orchestration
- Mission-related:Packet Decommutation
- Mission-related:Processing
- Mission-related:Science Data Processing
- Mission-related:System Testing
- Models and Simulations
- Models and Simulations:Data Guided
- Models and Simulations:Empirical
- Models and Simulations:Field-line Tracing
- Models and Simulations:First Principles
- Models and Simulations:Forecasting
- Models and Simulations:Forward-Fitting
- Models and Simulations:Instrument Response
- Models and Simulations:MHD
- Models and Simulations:Mission-Specific
- Models and Simulations:ML/AI
- Models and Simulations:Observatory/Instrument Models
- Models and Simulations:Physics-Based
- Models and Simulations:Theory
- Servers and Environments
- Servers and Environments:Data servers processing and handling
- Servers and Environments:Distribution/Access
- Servers and Environments:High Performance Computing
- Servers and Environments:Infrastructure as Code
- Servers and Environments:Software or Environment Container

---

### 5. Related Region (MANDATORY)
**Type:** Multi-select dropdown

**What it is:** The physical region the software supports science functionality for.

**How to fill it:** Select all physical regions the software's functionality is commonly used or intended for.

**Possible Values:**
- Earth Atmosphere
- Earth Magnetosphere
- Interplanetary Space
- Planetary Magnetospheres
- Solar Environment

---

### 6. Authors (MANDATORY)
**Type:** Multi-entry nested group

**What it is:** The author(s) of this software.

**How to fill it:** Multiple authors should be included in separate author fields.

**Sub-fields:**
- **Authors** (MANDATORY): Author name
- **Author Identifier** (RECOMMENDED): The identifier of the author, such as the ORCiD. Enter the complete identifier (e.g., https://orcid.org/0000-0003-0875-2023)
- **Affiliation** (RECOMMENDED, multi-entry):
  - **Organization**: Complete name without acronyms (e.g., Center for Astrophysics Harvard & Smithsonian)
  - **Affiliation Identifier**: ROR identifier if one exists (e.g., https://ror.org/03c3r2d17)

---

### 7. Software Name (MANDATORY)
**Type:** Text

**What it is:** The name of the software.

**How to fill it:** The name of the software package as listed on the code repository.

---

### 8. Description (MANDATORY)
**Type:** Text area

**What it is:** A description of the item. The first 150-200 characters will be used as the preview.

**How to fill it:** The description should be sufficiently detailed to provide the potential user with information to determine if the software is useful to their work. Include what the software does, why to use it, assumptions it makes, and similar information. Should be written with proper capitalization, grammar, and punctuation.

---

### 9. Concise Description (OPTIONAL)
**Type:** Text area (max 200 characters)

**What it is:** A description of the item limited to 150-200 characters. If the first 150-200 characters of the description do not provide the desired preview, you may enter an alternate text here.

**How to fill it:** The text should be short and provide a concise preview of the longer description.

---

### 10. Publication Date (RECOMMENDED)
**Type:** Date

**What it is:** Date of first broadcast/publication.

**How to fill it:** Used for the initial version of the software.

---

### 11. Publisher (RECOMMENDED)
**Type:** Nested group

**What it is:** The publisher (entity) of the creative work.

**How to fill it:** For software where a DOI has been obtained through Zenodo (e.g., GitHub-Zenodo workflow), Zenodo is the correct entry. If no DOI has been obtained, indicate the repository host, such as GitHub or GitLab.

**Sub-fields:**
- **Organization** (RECOMMENDED): Publisher name
- **Publisher Identifier** (RECOMMENDED): ROR identifier when available (e.g., https://ror.org/03c3r2d17) or URL otherwise (e.g., https://zenodo.org)

---

### 12. Version (RECOMMENDED)
**Type:** Nested group

**What it is:** Version of the software instance.

**How to fill it:** The version number is often an alphanumeric value, easily accessible on the code repository page (e.g., v1.0.0).

**Sub-fields:**
- **Version Number** (RECOMMENDED): The version identifier
- **Version Date** (RECOMMENDED): Date the specified version was released
- **Version Description** (RECOMMENDED): Brief summary of major changes in the new version (deprecated/new functionalities, features, resolved bugs, etc.)
- **Version PID** (RECOMMENDED): The globally unique persistent identifier for this specific version (e.g., the DOI for the version). Enter full DOI (e.g., https://doi.org/10.5281/zenodo.13287868)

---

### 13. Programming Language (RECOMMENDED)
**Type:** Multi-select dropdown

**What it is:** The computer programming languages most important for the software.

**How to fill it:** Select the most important languages (e.g., Python, Fortran, C). This is not meant to be an exhaustive list.

**Possible Values:**
- C
- C#
- C++
- Fortran 2003
- Fortran 2008
- Fortran77
- Fortran90
- IDL
- Java
- Javascript
- Julia
- MATLAB
- Other
- Python 2.x
- Python 3.x
- Rust
- SQL
- Typescript

---

### 14. Reference Publication (OPTIONAL)
**Type:** DataCite DOI

**What it is:** The DOI for the publication describing the software, sometimes used as the preferred citation for the software in addition to the version-specific citation to the code itself.

**How to fill it:** Enter the DOI for the publication describing the software (e.g., a JOSS paper).

---

### 15. License (RECOMMENDED)
**Type:** Nested group

**What it is:** The full name of the license assigned to this software. Licenses supported by SPDX are preferred. If the software is restricted, enter 'Restricted'.

**How to fill it:** Choose from a list of licenses with proper grammar and punctuation. If the license is listed on https://spdx.org/licenses/, copy the entire license title.

**Sub-fields:**
- **License** (RECOMMENDED): License name
- **License URI** (RECOMMENDED): URI of the license (auto-populated for SPDX licenses)

**Common License Options:**
- Apache License 2.0
- GNU General Public Licenses (GPL version 2)
- GNU Library or 'Lesser' General Public Licenses (LGPL version 2)
- MIT License
- New BSD license
- Other

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Type:** Multi-select dropdown (allows custom entries)

**What it is:** General science keywords relevant for the software (e.g., from the AGU Index List or the UAT) not supported by other metadata fields.

**How to fill it:** Begin typing the keyword in the box. Keywords from UAT and AGU Index lists will appear in a dropdown. Choose correct one(s) or type in if not listed.

**Example Values (from database):**
- analysis
- batsrus
- cdf
- charge exchange
- coordinates
- csv
- esa
- heliophysics
- heliosphere
- magnetohydrodynamics
- magnetosphere
- physics
- plasma
- python
- solar orbiter
- solar wind
- space
- space physics
- space weather
- swmf

---

### 17. Data Sources (OPTIONAL)
**Type:** Multi-select dropdown

**What it is:** The data input source the software supports.

**How to fill it:** Select all data input sources the software supports. If a source is not listed, select 'Other'. If observatory-specific, select 'observatory-specific' and indicate the observatory/mission name in the Related Observatory field.

**Possible Values:**
- CDAWeb
- das2
- FTP/FTPS Directories
- HAPI
- HTTP/HTTPS Directories
- Observatory/Mission-specific
- OMNIWeb
- Other
- S3/Cloud-aware
- SSCWeb
- TAP
- The Virtual Solar Observatory
- VirES

---

### 18. Input File Formats (RECOMMENDED)
**Type:** Multi-select dropdown

**What it is:** The file formats the software supports for data input.

**How to fill it:** Select all file formats your software supports for input files. Only formats actually supported should be indicated.

**Possible Values:**
- ascii
- CDF
- csv
- FITS
- HDF5
- IDL.sav
- ISTP-Compliant
- JSON
- netCDF3/4
- Other
- Zarr

---

### 19. Output File Formats (RECOMMENDED)
**Type:** Multi-select dropdown

**What it is:** The file formats the software supports for data output.

**How to fill it:** Select all file formats your software supports for generated files. Only formats actually supported should be indicated.

**Possible Values:**
- ascii
- CDF
- csv
- FITS
- HDF5
- IDL.sav
- ISTP-Compliant
- JSON
- netCDF3/4
- Other
- Zarr

---

### 20. Operating System (RECOMMENDED)
**Type:** Multi-select dropdown

**What it is:** The operating systems the software supports.

**How to fill it:** Select all operating systems the software can successfully be installed on.

**Possible Values:**
- Linux
- Mac
- MobilePlatform
- Operating System Independent
- OS Independent
- Other
- Solaris
- Windows

---

### 21. CPU Architecture (RECOMMENDED)
**Type:** Multi-select dropdown

**What it is:** The CPU architecture the software requires.

**How to fill it:** Select all CPU architectures the software can successfully be installed and executed on.

**Possible Values:**
- x86-64
- Apple Silicon arm64
- Sun (SPARC)
- Linux aarch64 or arm64
- CPU Independent
- GPU
- HPC or HEC
- ppc64le
- Other

---

### 22. Related Phenomena (OPTIONAL)
**Type:** Multi-select dropdown (allows custom entries)

**What it is:** The phenomena the software supports science functionality for.

**How to fill it:** Select phenomena terms from a supported controlled vocabulary.

**Possible Values:**
- Coronal Heating
- Coronal Holes
- Coronal Mass Ejections
- Solar Corona
- Solar Flares
- X-ray emission

---

### 23. Development Status (RECOMMENDED)
**Type:** Single-select dropdown

**What it is:** The development status of the software.

**How to fill it:** Select the development status of the code repository. See repostatus.org for term descriptions.

**Possible Values:**
- **Abandoned**: Initial development started but abandoned; no stable release
- **Active**: Reached stable, usable state and being actively developed
- **Concept**: Minimal/no implementation; limited example/demo/proof-of-concept only
- **Inactive**: Reached stable, usable state but no longer actively developed; support provided as time allows
- **Moved**: Project moved to new location; that version is authoritative
- **Suspended**: Initial development started but stopped temporarily; authors intend to resume
- **Unsupported**: Reached stable, usable state but authors ceased work; new maintainer desired
- **WIP**: Initial development in progress; no stable, usable public release yet

---

### 24. Documentation (RECOMMENDED)
**Type:** URL

**What it is:** Link to the documentation and installation instructions. If this is the same as the access URL, then enter that link here.

**How to fill it:** Documentation link including installation instructions. Should be entered as a complete URL.

---

### 25. Funder (OPTIONAL)
**Type:** Multi-entry nested group

**What it is:** A person or organization that supports (sponsors) something through some kind of financial contribution.

**How to fill it:** The name of the organization that provided funding (e.g., NASA or The Sloan Foundation).

**Sub-fields:**
- **Organization** (OPTIONAL): Funder name
- **Funder Identifier** (RECOMMENDED): ROR identifier if available (e.g., https://ror.org/027ka1x80)

---

### 26. Award Title (OPTIONAL)
**Type:** Multi-entry nested group

**What it is:** The title of the specific grant or award that funded the work.

**How to fill it:** Copy the full title of the award.

**Sub-fields:**
- **Award Title** (OPTIONAL, multi-entry): Full award title
- **Award Number** (RECOMMENDED): Identifier associated with the award (e.g., NNG19PQ28C). Used by funding agencies to track impact.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Type:** Multi-entry DataCite DOI

**What it is:** Publications that describe, cite, or use the software that the software developer prioritizes but are different from the reference publication.

**How to fill it:** Enter DOIs for all publications the software is cited in. If DOI not available, enter citation in APA format with permanent link (e.g., Shaifullah, G., Tiburzi, C., & Zucca, P. (2020) CMEchaser, Detecting Line-of-Sight Occultations Due to Coronal Mass Ejections Solar Physics, 295(10), 136. https://arxiv.org/abs/2008.12153).

---

### 28. Related Datasets (OPTIONAL)
**Type:** Multi-entry DataCite DOI

**What it is:** Datasets the software supports functionality for (e.g., analysis).

**How to fill it:** At minimum, the DOI should be the publication that described the dataset. If DOI not available, enter citation in APA format (e.g., Fuselier et al. (2022). MMS 4 Hot Plasma Composition Analyzer (HPCA) Ions, Level 2 (L2), Burst Mode, 0.625 s Data [Data set]. NASA Space Physics Data Facility. https://hpde.io/NASA/NumericalData/MMS/4/HotPlasmaCompositionAnalyzer/Burst/Level2/Ion/PT0.625S.html).

---

### 29. Related Software (OPTIONAL)
**Type:** Multi-entry DataCite DOI

**What it is:** Software that performs similar tasks but does not necessarily link together (which would be 'interoperable software'). Important software dependencies and software this work was forked from should also be included.

**How to fill it:** Ideally, enter the DOI for the software code. Otherwise, link to code repository (e.g., https://github.com/sunpy/sunpy). If no public repository, enter link where users can find more information (e.g., related HSSI item). Publication DOIs should go in relatedPublications instead.

---

### 30. Interoperable Software (OPTIONAL)
**Type:** Multi-entry DataCite DOI

**What it is:** Other important software packages this software has demonstrated interoperability with. Can run package in the same environment as the others without errors.

**How to fill it:** Ideally, enter the DOI for the software code. Otherwise, link to code repository (e.g., https://github.com/sunpy/sunpy). If no public repository, enter link where users can find more information (e.g., related HSSI page). Publication DOIs should go in relatedPublications instead.

---

### 31. Related Instruments (OPTIONAL)
**Type:** Multi-entry nested group

**What it is:** The instrument the software is designed to support.

**How to fill it:** Begin typing the instrument name. Instruments from IVOA will appear in dropdown; choose correct one. If not listed, type full name.

**Sub-fields:**
- **Instrument Name** (OPTIONAL): Name of the instrument
- **Instrument Identifier** (OPTIONAL): Globally unique persistent identifier (e.g., DOI like https://doi.org/10.5281/zenodo.13287868). Enables improved linking.

---

### 32. Related Observatories (OPTIONAL)
**Type:** Multi-entry nested group

**What it is:** The mission, observatory, and/or group of instruments the software is designed to support.

**How to fill it:** Begin typing the name. Missions and Observatories from IVOA will appear in dropdown; choose correct one. If not listed, type full name.

**Sub-fields:**
- **Observatory Name** (OPTIONAL): Name of the observatory/mission

---

### 33. Logo (OPTIONAL)
**Type:** URL

**What it is:** A link to the logo for the software.

**How to fill it:** The logo should be stored online in a permanent place and made publicly accessible.

---

## Agreement

### Metadata Agreement (MANDATORY)
Before submission, you must agree to the following terms:

"By submitting this form, you acknowledge and agree that any metadata you provide is submitted voluntarily and becomes part of the public domain. You waive all rights, claims, and interests to the submitted metadata, and grant unrestricted use, reproduction, modification, and distribution rights to the receiving party or its designees."

---

## Automated Metadata Extraction

The HSSI web form supports automated metadata extraction through a cascade of API calls. AI agents can replicate this behavior to pre-fill many form fields automatically.

### Autofill Cascade Overview

The form uses a three-stage cascade when a DOI is provided:

1. **DataCite API** → Extract basic metadata from the DOI
2. **Zenodo API** (if applicable) → Get additional version and repository information
3. **SoMEF** → If a code repository URL was found, extract metadata directly from the repository

Each stage adds more metadata, with later stages filling in gaps or providing more detailed information.

---

### Stage 1: DataCite API

**Endpoint:** `https://api.datacite.org/dois/{DOI}`

**Example:** `https://api.datacite.org/dois/10.5281/zenodo.13287868`

**Fields Extracted:**
- **Software Name** (from `attributes.titles[].title`)
- **Description** (from `attributes.descriptions[]` where `descriptionType` may be "Abstract")
- **Concise Description** (from short descriptions ≤200 chars or truncated description)
- **Authors** with sub-fields:
  - Author name (from `attributes.creators[].name` or `givenName` + `familyName`)
  - Author Identifier / ORCID (from `attributes.creators[].nameIdentifiers[]` where `nameIdentifierScheme` = "ORCID")
  - Affiliations (from `attributes.creators[].affiliation[]`)
- **Publisher** (from `attributes.publisher`)
- **Publication Date** (from `attributes.dates[]` where `dateType` = "Issued")
- **License** name and URI (from `attributes.rightsList[]`)
- **Funders** (from `attributes.fundingReferences[].funderName`)
- **Awards** (from `attributes.fundingReferences[].awardTitle` and `awardNumber`)
- **Version Number** (from `attributes.version`)
- **Keywords** (from `attributes.subjects[].subject`)
- **Code Repository URL** (from `attributes.relatedIdentifiers[]` where `relationType` = "IsDerivedFrom" and `relatedIdentifierType` = "URL")
- **Documentation URL** (from `attributes.relatedIdentifiers[]` where `relationType` = "IsDocumentedBy")
- **Reference Publication** (from `attributes.relatedIdentifiers[]` where `relationType` = "IsDescribedBy")
- **Related Publications** (from `attributes.relatedIdentifiers[]` where `resourceTypeGeneral` is publication-related)
- **Related Datasets** (from `attributes.relatedIdentifiers[]` where `resourceTypeGeneral` = "Dataset")
- **Related Software** (from `attributes.relatedIdentifiers[]` where `resourceTypeGeneral` is software-related)

**How to replicate:**
```bash
# Example: Get metadata for a DOI
curl "https://api.datacite.org/dois/10.5281/zenodo.13287868"
```

---

### Stage 2: Zenodo API (Conditional)

**Endpoint:** `https://zenodo.org/api/records/{RECORD_ID}`

**When to use:** If the DOI is a Zenodo DOI (contains "zenodo" in the DOI)

**Example:** For DOI `10.5281/zenodo.13287868`, extract record ID `13287868` and query:
`https://zenodo.org/api/records/13287868`

**Additional Fields Extracted:**
- **Concept DOI** (from `conceptdoi`) - The DOI for all versions, not just one version
- **Version PID** (from `doi`) - The DOI for this specific version
- **Code Repository URL** (from `metadata.custom["code:codeRepository"]` - alternative source)
- **Development Status** (from `metadata.custom["code:developmentStatus"]`)
- **Programming Languages** (from `metadata.custom["code:programmingLanguage"][]`)

**How to replicate:**
```bash
# Extract Zenodo record ID from DOI
RECORD_ID=$(echo "10.5281/zenodo.13287868" | grep -oP 'zenodo\.\K\d+')

# Query Zenodo API
curl "https://zenodo.org/api/records/${RECORD_ID}"
```

---

### Stage 3: SoMEF (Conditional)

**When to use:** If a code repository URL was found in Stage 1 or Stage 2

**Tool:** [SoMEF](https://github.com/KnowledgeCaptureAndDiscovery/somef) (Software Metadata Extraction Framework)

**Installation:**
```bash
pip install somef
```

**Command:**
```bash
somef describe -t 0.7 -r {REPOSITORY_URL} -o output.json
```

**Fields Extracted:**
- **Persistent Identifier** (from `identifier[].result.value`)
- **Authors** with names and URLs (from `authors[].result`)
- **Software Name** (from `full_title[].result.value` or `name[].result.value`, choosing highest confidence)
- **Description** (from `description[].result.value`, may combine multiple with similar confidence)
- **Publication Date** (from `date_created[].result.value`)
- **Version Number** (from `version[].result.value`, choosing newest version)
- **Version Date** (from `date_updated[].result.value`)
- **Programming Languages** (from `programming_languages[].result.value`)
- **License** (from `license[].result` with `spdx_id` or `name`)
- **Keywords** (from `keywords[].result.value`, comma-separated)
- **Development Status** (from `repository_status[].result.description`)
- **Documentation URL** (from `documentation[].result.value`, prioritizing non-repository domains)
- **Logo** (from `logo[].result.value`)

**Notes:**
- SoMEF uses confidence scores; the implementation chooses results with highest confidence
- SoMEF can be slow (may take 30+ seconds for large repositories)
- The threshold `-t 0.7` means only results with ≥70% confidence are included
- Output format `-o` produces JSON-LD format

**How to replicate:**
```bash
# Example: Extract metadata from a GitHub repository
somef describe -t 0.7 -r https://github.com/SuperDARN/pydarn -o pydarn_metadata.json

# Read the output
cat pydarn_metadata.json
```

---

### PyHC Package Metadata

**What is PyHC?** The Python in Heliophysics Community (PyHC) maintains a registry of Python packages used in heliophysics research. If the software being submitted is a PyHC package, additional curated metadata may be available.

**PyHC Registry Files:**
PyHC maintains its package registry in three YAML files on GitHub. An AI agent should check all three to determine if the package is registered:

1. **Core packages:** https://github.com/heliophysicsPy/heliophysicsPy.github.io/blob/main/_data/projects_core.yml
2. **Community packages:** https://github.com/heliophysicsPy/heliophysicsPy.github.io/blob/main/_data/projects.yml
3. **Unevaluated packages:** https://github.com/heliophysicsPy/heliophysicsPy.github.io/blob/main/_data/projects_unevaluated.yml

**Fields Available in PyHC Metadata:**
- **name** - Package name
- **description** - Package description
- **logo** - URL to package logo
- **docs** - Documentation URL
- **code** - Code repository URL
- **contact** - Primary contact/maintainer
- **keywords** - Array of keywords (may include domain-specific terms like "ionosphere_thermosphere_mesosphere", "magnetospheres", "solar", etc.)
- **community** - Quality rating for community engagement
- **documentation** - Quality rating for documentation
- **testing** - Quality rating for testing coverage
- **software_maturity** - Quality rating for software maturity
- **python3** - Quality rating for Python 3 compatibility
- **license** - Quality rating for license clarity

**How to check:**

1. **Read all three YAML files completely** - Don't use grep or search for specific terms, as you might use the wrong search term and miss a match
2. **Parse each file** and examine all entries to find matches based on:
   - Package name (may differ slightly from repository name)
   - Repository URL (code field)
   - Package description content
3. If found, extract the metadata from that entry
4. Use PyHC metadata to supplement other sources

**Example approach:**
```bash
# Download all three PyHC registry files for complete analysis
curl -s "https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects_core.yml" -o pyhc_core.yml
curl -s "https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects.yml" -o pyhc_community.yml
curl -s "https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects_unevaluated.yml" -o pyhc_unevaluated.yml

# Then parse each YAML file in its entirety to check for matches
# (Use a YAML parser to read all entries and compare against the package being analyzed)
```

**Important Notes:**
- Not all heliophysics packages are PyHC packages - absence from these files does not indicate a problem
- PyHC metadata is curated by the community and is considered more definitive/accurate than auto-extracted metadata
- The quality ratings (Good, Partially met, etc.) can inform the Development Status field
- PyHC keywords may map to HSSI's Related Region, Software Functionality, or Keywords fields

---

### Combining Results

The autofill cascade fills form fields in this recommended order:
1. **DataCite API** metadata is applied first
2. **Zenodo API** metadata overwrites/supplements DataCite data
3. **SoMEF** metadata is applied (only if repository URL was found)
4. **PyHC metadata** can supplement/replace any of the above, especially for logo, documentation, and keywords

Later stages generally don't overwrite fields that are already filled, unless the new data is more specific or complete. PyHC metadata, being manually curated, may be prioritized for certain fields like documentation URLs and description.

---

## Notes for AI Agents

When extracting metadata from a GitHub repository to fill this form:

1. **Code Repository URL** can be found directly from the repository URL
2. **Software Name** is typically in the repository name or README
3. **Description** and **Concise Description** are often in README.md or package metadata
4. **Authors** can be extracted from:
   - CITATION.cff file
   - codemeta.json file
   - AUTHORS file
   - CONTRIBUTORS file
   - Git commit history (with caution)
   - Package metadata (setup.py, package.json, etc.)
5. **License** information is typically in:
   - LICENSE or LICENSE.txt file
   - Package metadata files
   - Repository settings
6. **Programming Language** can be determined from:
   - File extensions in the repository
   - GitHub's language statistics
   - Package configuration files
7. **Reference Publication** tends to be obvious when it exists:
   - CITATION.cff file
   - README recommendations for how to cite the package
8. **Documentation** URL is often in:
   - README.md links
   - docs/ folder
   - .readthedocs.yml or other doc configuration
9. **Version** information may be in:
   - Git tags
   - Release notes
   - Package version files
   - CHANGELOG.md
10. **Keywords** might be found in:
   - Repository topics/tags
   - Package metadata
   - README.md
11. **DOIs** (Persistent Identifier, Version PID, Reference Publication) may be in:
    - CITATION.cff
    - README badges
    - Zenodo integration
    - codemeta.json
12. **Development Status** can be inferred from:
    - Recent commit activity
    - README status badges
    - Repository status indicators
13. **File Formats** supported may be mentioned in:
    - Documentation
    - Code analysis (file I/O operations)
    - README.md feature lists
14. **Operating System** compatibility may be in:
    - CI/CD configuration (.github/workflows, .travis.yml, etc.)
    - Installation documentation
    - Package metadata
15. **Software Functionality** is particularly important but requires a deep understanding of the package:
    - Examine the repo thoroughly to understand the full breadth of what it does
    - Be exhaustive; try not to miss any functionality
16. **Related Region** is also important and requires a deep understanding of the physical regions the software is commonly used for.

Many fields are domain-specific (heliophysics) and may require understanding of the software's scientific purpose, which might be found in papers, documentation, or descriptive text in the README.
