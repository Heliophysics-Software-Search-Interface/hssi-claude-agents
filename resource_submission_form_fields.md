# HSSI Resource Submission Form Fields

This document describes all fields in the Heliophysics Software Search Interface (HSSI) Resource Submission Form. The form is divided into three sections: basic information, additional data, and additional metadata.

## Form Structure

The form collects metadata about heliophysics software packages for inclusion in the HSSI website. Fields are marked as:
- **MANDATORY** - Required to submit the form
- **RECOMMENDED** - Strongly encouraged
- **OPTIONAL** - Not required but helpful

---

## Controlled Vocabularies — read this before using any value list

Every **Possible Values** list below is a **dated snapshot**, not the source of truth. The live
vocabulary on the submission target is authoritative and wins on any conflict:

```
GET <target>/api/models/<Model>/rows/all/
```

**Use the snapshot to pick candidates; use the API to confirm they exist.** Confirm every
controlled-list value against the live endpoint for the target you are working with before writing it
into a payload or an `hssi_metadata.md`.

**Why exactness matters.** `serializers/submission.py` resolves controlled lists with
`Model.objects.filter(name__iexact=value)` after nothing more than `.strip()`. There is no alias
table and no fuzzy matching. A value that is one character off — a missing trailing period, a
straight quote where the row has a curly one — raises `ValidationError: Unknown value` and fails the
entire submission. Case is the only difference that is forgiven.

**Vocabularies can differ between targets.** As of the 2026-07-29 audit every vocabulary was
identical between `https://hssi.hsdcloud.org` and `http://localhost` **except `License`**, which has
two prod-only rows. Never assume a value that worked on one target exists on the other.

**Only Keywords (Field 16) is an open vocabulary** — `_get_or_create_keyword` creates missing rows.
Every other list rejects unknown values.

The field-to-endpoint mapping is in `.claude/skills/hssi-field-definitions/SKILL.md`, which wraps this
document. To re-verify these snapshots against live and refresh them, run **Step A** of the
`update-api-spec` skill.

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

**Possible Values** — *83 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/FunctionCategory/rows/all/` is authoritative.*

Written `Parent:Child`; the serializer splits on `:`. The 6 top-level categories are also selectable on their own, and **when a subcategory applies its parent must be listed too**. 13 subcategory names (`ML/AI`, `Spectrogram`, `Analysis`, …) recur under more than one parent — that is intentional, and the parent prefix disambiguates them. Every child has exactly one parent, so paths are never deeper than two levels.

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

**Possible Values** — *24 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/Region/rows/all/` is authoritative.*

The vocabulary is currently flat — every row is a top-level value, no `Parent:Child` form.

- Chromosphere
- Corona
- Earth Atmosphere
- Earth Auroral Subregion
- Earth Inner Magnetosphere
- Earth Ionosphere
- Earth Lower and Middle Atmosphere
- Earth Magnetosheath
- Earth Magnetosphere
- Earth Magnetotail
- Earth Outer Magnetosphere
- Earth Thermosphere
- Heliosheath
- Interplanetary Space
- Jupiter Magnetosphere
- Mars Magnetosphere
- Neptune Magnetosphere
- Photosphere
- Planetary Magnetospheres
- Saturn Magnetosphere
- Solar Environment
- Solar Interior
- Solar Wind
- Uranus Magnetosphere

> **Historical note.** Until the 2026-07-29 audit this field listed only 5 values (Earth Atmosphere,
> Earth Magnetosphere, Interplanetary Space, Planetary Magnetospheres, Solar Environment). Those are
> the keys of `REGION_MAPPING_TTL` in `models/vocab.py` — a mapping used for TTL export, **not** the
> selectable vocabulary. All 24 rows above are offered by `/api/models/Region/choices/`. Prefer the
> most specific applicable region (e.g. `Earth Ionosphere` over `Earth Atmosphere`) rather than
> defaulting to the old five.

---

### 6. Authors (MANDATORY)
**Type:** Multi-entry nested group

**What it is:** The author(s) of this software.

**How to fill it:** Multiple authors should be included in separate author fields.

**Sub-fields:**
- **Authors** (MANDATORY): Author name
- **Author Identifier** (RECOMMENDED): The identifier of the author. For a person author, this is the ORCiD (e.g., https://orcid.org/0000-0003-0875-2023). For an author that is an **organization** (a lab, consortium, or institution credited as an author), use its ROR instead (e.g., https://ror.org/03c3r2d17) — HSSI recognizes a ror.org identifier and treats that author as an organization. Enter the complete identifier URL.
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

**Possible Values** — *19 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/ProgrammingLanguage/rows/all/` is authoritative.*

Note the exact spellings: **`Javascript`** (not `JavaScript`) and **`Typescript`** (not `TypeScript`).

- C
- C#
- C++
- Fortran 2003
- Fortran 2008
- Fortran 2023
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

### 14. Reference Publication (RECOMMENDED)
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

**Possible Values** — *snapshot 2026-07-29. **This vocabulary differs by target**: 13 distinct names on `https://hssi.hsdcloud.org`, 11 on `http://localhost`. Live `/api/models/License/rows/all/` is authoritative.*

This is a **closed** list despite the "copy the SPDX title" instruction above: the serializer does
`License.objects.filter(name__iexact=<value>)` and raises `Unknown license` on no match. An SPDX
title that is not a row below will be rejected — use `Other` instead.

- Apache License 2.0
- BSD 2-Clause "Simplified" License
- BSD 3-Clause "New" or "Revised" License
- Creative Commons Attribution 4.0 International
- GNU General Public Licenses (GPL version 2)
- GNU General Public License v3.0 or later
- GNU Lesser General Public License v3.0 only
- GNU Library or ‘Lesser’ General Public Licenses (LGPL version 2)
- GNU Library or ‘Lesser’ General Public Licenses (LGPL version 3) — **prod only**
- MIT License
- New BSD license — **prod only**
- Other
- Restricted

**Traps in this list:**

- **Curly quotes.** The two LGPL rows use typographic quotes — `‘Lesser’` (U+2018/U+2019), *not*
  `'Lesser'`. A straight-quote copy will not match.
- **Two prod-only rows.** `New BSD license` and `GNU Library or ‘Lesser’ General Public Licenses
  (LGPL version 3)` exist on production but **not** on localhost; sending either to a local instance
  returns a 400. For BSD-3 on localhost use `BSD 3-Clause "New" or "Revised" License`.
- **Duplicate `Other` on prod.** Production carries two `Other` rows, both with an empty URL.
  `License.get_other_licence()` resolves them with `.first()`, so which one a submission binds to is
  arbitrary. Harmless for submission, but worth knowing when a roundtrip diff shows an unexpected
  license id.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Type:** Multi-select dropdown (allows custom entries)

**What it is:** General science keywords relevant for the software (e.g., from the AGU Index List or the UAT) not supported by other metadata fields.

**How to fill it:** Begin typing the keyword in the box. Keywords from UAT and AGU Index lists will appear in a dropdown. Choose correct one(s) or type in if not listed.

**Example Values** — *20 of 483 rows on `https://hssi.hsdcloud.org` / 572 on `http://localhost`, sampled 2026-07-29. Full list at `/api/models/Keyword/rows/all/`.*

**This is the only genuinely open vocabulary in the form.** `_get_or_create_keyword` creates a row
for any keyword not already present (case-insensitive match), so a new keyword will never fail a
submission — but it also means typos and un-split comma-delimited strings become permanent rows.
Enter **one keyword per entry**, lower-case, and check the live list first to reuse an existing row
rather than minting a near-duplicate.

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

**Possible Values** — *18 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/DataInput/rows/all/` is authoritative.*

- AMDA
- CDAWeb
- das2
- FTP/FTPS Directories
- GFZ
- HAPI
- HTTP/HTTPS Directories
- Madrigal
- Observatory/Mission-specific
- OMNIWeb
- Other
- ~~`Other - https://xrt.cfa.harvard.edu/level1/`~~ — **junk row, never select** (see below)
- S3/Cloud-aware
- SSCWeb
- TAP
- The Virtual Solar Observatory.
- VirES
- WDC

**Traps in this list:**

- **`The Virtual Solar Observatory.` ends with a period.** The stored row name includes a trailing
  full stop; `The Virtual Solar Observatory` (without it) does **not** match and will be rejected.
  The row is otherwise genuine — it carries the canonical `…/DataSources#VSO` identifier.
- **`Other - https://xrt.cfa.harvard.edu/level1/` is a data-entry artifact**, not vocabulary — a
  free-text "Other" value that leaked into the controlled list. It is listed here only so it is
  recognizable; select plain `Other` instead.
- **`AMDA`, `GFZ`, `Madrigal`, and `WDC` have empty `identifier` fields**, unlike every other row.
  They appear to be legitimate later additions rather than artifacts, and are safe to select.

---

### 18. Input File Formats (RECOMMENDED)
**Type:** Multi-select dropdown

**What it is:** The file formats the software supports for data input.

**How to fill it:** Select all file formats your software supports for input files. Only formats actually supported should be indicated.

**Possible Values** — *11 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/FileFormat/rows/all/` is authoritative. Fields 18 and 19 draw on the same vocabulary.*

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

**Possible Values** — *same 11-value `FileFormat` vocabulary as Field 18; snapshot 2026-07-29. Live `/api/models/FileFormat/rows/all/` is authoritative.*

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

**Possible Values** — *7 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/OperatingSystem/rows/all/` is authoritative.*

- Linux
- Mac
- MobilePlatform
- Operating System Independent
- Other
- Solaris
- Windows

> **Trap.** `OS Independent` is **not** a value and never has been — it was listed here in error
> until the 2026-07-29 audit and would be rejected on submission. The only cross-platform value is
> `Operating System Independent`, spelled out in full.

---

### 21. CPU Architecture (RECOMMENDED)
**Type:** Multi-select dropdown

**What it is:** The CPU architecture the software requires.

**How to fill it:** Select all CPU architectures the software can successfully be installed and executed on.

**Possible Values** — *9 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/CpuArchitecture/rows/all/` is authoritative (`CPUArchitecture` also resolves — model names are case-insensitive).*

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
**Type:** Multi-select dropdown (**closed** controlled vocabulary — custom entries are rejected)

**What it is:** The phenomena the software supports science functionality for.

**How to fill it:** Select phenomena terms from the controlled vocabulary below. Despite the web form's free-text affordance, the API path is strict: `related_phenomena` resolves through `_get_graph_list_item`, which raises `Unknown value` on anything not in the list. A phenomenon the software supports that has no row belongs in **Keywords** (Field 16, the open vocabulary), not here.

**Possible Values** — *7 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/Phenomena/rows/all/` is authoritative.*

- Coronal Heating
- Coronal Mass Ejections
- Geomagnetic Storms
- Solar Corona
- Solar Flares
- Solar Wind
- X-ray emission

> **Trap.** `Coronal Holes` is **not** a value — it was listed here in error until the 2026-07-29
> audit and would be rejected on submission. `Geomagnetic Storms` and `Solar Wind` were missing from
> that same stale list. The vocabulary is currently flat: every row is a top-level value, no
> `Parent:Child` form.

---

### 23. Development Status (RECOMMENDED)
**Type:** Single-select dropdown

**What it is:** The development status of the software.

**How to fill it:** Select the development status of the code repository. See repostatus.org for term descriptions.

**Possible Values** — *8 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/RepoStatus/rows/all/` is authoritative.*

Submit the bare term only (`Active`, `WIP`, …); the descriptions below are the repostatus.org
definitions, not part of the value.

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

**How to fill it:** The name of the organization that provided the funding (e.g., National Aeronautics and Space Administration). Avoid acronyms and enter one organization per field.

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

**When to include it (relevance):** List software that is *distinguishing* — it tells a reader something about **this** software. That means a package performing similar tasks, a predecessor or the project this was forked from, a companion package, or a **domain-specific** dependency (a heliophysics/science library whose presence characterizes the software). "Important software dependencies" means exactly that: *important*, not merely *present*. **The generic scientific-Python stack is excluded here too** — numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly, bokeh, requests, python-dateutil, pytest, tqdm, PyYAML, click, setuptools and their peers are not related software, because listing them says nothing that isn't equally true of most of the ecosystem. Those names are **examples, not a closed list**: apply Field 30's "web app, finance model, or biology pipeline" test to anything unnamed, and treat generic infrastructure as excluded here too. Same test as Field 30: **if the entry would be equally true of most Python packages, it carries no information and does not belong.** The two gates are one rule — a package rejected from Field 30 is *not* thereby a Field 29 entry; it usually belongs in neither.

**How to fill it:** Ideally, enter the DOI for the software code. Otherwise, link to code repository (e.g., https://github.com/sunpy/sunpy). If no public repository, enter link where users can find more information (e.g., related HSSI item). Publication DOIs should go in relatedPublications instead.

---

### 30. Interoperable Software (OPTIONAL)
**Type:** Multi-entry DataCite DOI

**What it is:** Other important software packages this software has demonstrated interoperability with. Can run package in the same environment as the others without errors.

**When to include it (relevance):** This field is about which other **high-level heliophysics/science tools** this software can actually interoperate with — **not its dependency list**. The bar is a *demonstrated exchange*: the two packages share or convert between data models, one's output can be imported into the other, there is an adapter/converter API (`to_sunpy_map()`, `from_pysat()`, `to_dataframe()`), a plugin/extension relationship, a companion package designed to be used with it, or a cross-language bridge to a named domain tool (an IDL SPEDAS or MATLAB interface). Read "can run in the same environment without errors" as presupposing that the two are **peer tools a user would deliberately combine** — it is a caveat on real interoperability, *not* the test for it. Merely sharing a Python runtime satisfies nothing.

**Never list these (Tier A), no exceptions:** numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly, bokeh, requests, python-dateutil, pytest, tqdm, PyYAML, click, setuptools, and the rest of the generic scientific-Python/tooling stack. **Being a dependency is not interoperability.** "It directly depends on numpy" is true of nearly every package in HSSI, so it distinguishes nothing. General test: **if the claim would be equally true of most of the Python ecosystem, it carries no information about this software and does not belong here.**

**Tier A is a list of examples, not a closed list — the principle governs, not the names.** Do not conclude that a package is acceptable merely because it is not enumerated above. For any package not named in either tier, ask: **would this package be equally at home in a web app, a finance model, or a biology pipeline?** If yes, it is **generic infrastructure** — arrays, dataframes, plotting and mapping, I/O plumbing, packaging, testing, HTTP, logging, CLI parsing — and gets Tier A treatment whether or not it appears in the list. A genuine heliophysics/science peer tool fails that test immediately (it would be absurd in a finance model), so this rule does not put real domain software at risk.

**Include only with cited evidence (Tier B):** astropy, xarray, cdflib, h5py, netCDF4, dask, MATLAB, Jupyter and similar foundational-but-domain-adjacent packages. These qualify **only** when a specific exchange is documented in the public API, docs, examples, or tests — never on dependency presence alone. "The public API returns `xarray.Dataset` objects as its documented interchange format" qualifies; "uses xarray internally" does not. Two justifications that are **never** sufficient on their own: *"part of the standard scientific Python ecosystem"* and *"a PyHC member, so it interoperates with PyHC packages"* — ecosystem membership is not a demonstrated interoperation with any particular package.

**Worked contrast:** PySPEDAS ↔ PyTplot (exchanges tplot variables) ✅ · hapiclient ↔ hapiplot (companion visualization package) ✅ · sunpy ↔ ndcube (shared NDCube data model) ✅ · "depends on numpy" ❌ · "uses matplotlib for all plotting" ❌ · "listed in pyproject.toml dependencies" ❌.

**Where a rejected entry goes:** usually **nowhere**. A genuinely distinguishing domain package may belong in Field 29 (Related Software) — but Field 29 applies the same exclusion to the generic stack, so do not relocate a Tier A package there.

**How to fill it:** Ideally, enter the DOI for the software code. Otherwise, link to code repository (e.g., https://github.com/sunpy/sunpy). If no public repository, enter link where users can find more information (e.g., related HSSI page). Publication DOIs should go in relatedPublications instead.

---

### 31. Related Instruments (OPTIONAL)
**Type:** Multi-entry nested group

**What it is:** The instrument the software is designed to support.

**When to include it (relevance):** List an instrument only if the software is *designed to support* it — it directly reads/writes/parses/calibrates/processes that specific instrument's data, implements a data format/convention specific to it (as a means of supporting it), is purpose-built or an instrument-team tool for it, or models/visualizes its measurements as a primary function. Sanity check: would a user searching HSSI for `instrument:"X"`, or someone working with X's data, expect this software back? If not, leave it out. **Exclude** instrument-agnostic tools (general models/utilities/frameworks support none specifically), tutorial/demo/example name-drops, "configurable for" / "commonly used with" / "optimized for" mentions of an otherwise-agnostic tool, and links that belong to another field — **generic** support for a multi-instrument *file format* (FITS/CDF/netCDF) → Input/Output File Formats, or a **generic/multi-mission** *data archive/source* (e.g. CDAWeb broadly) → Data Sources. **But** an instrument-**specific** parser, format, convention, or data source/API *does* count as designed-to-support — list that instrument here. Note: an instrument the software genuinely supports but that isn't in the controlled vocabulary is still *related* — don't drop it at the relevance stage. Carry it into the resolution ladder below, which decides between an observatory-level association and a documented omission. "Related but unresolvable" is never a licence to invent a value.

**How to fill it:** Begin typing the instrument name. Matches from HSSI's controlled instrument/observatory vocabulary appear in the dropdown; choose the correct one. This vocabulary is sourced from the heliophysics.net API and resolved to SPASE identifiers (it replaced the older IVOA-based list, which is now retired). If no entry matches, type the full name. **(That last sentence describes what the web form lets a *human* submitter do. Agents must never free-type a value — see Agent guidance below.)**

**Agent guidance — the SPASE resolution ladder.** This is the canonical procedure for **both** Field 31 and Field 32; everything else in this repo refers back to it.

Resolve against the controlled list at `/api/models/InstrumentObservatory/rows/all/` (fetch the ~7,700-row list once to a file with `?columns=id,name,identifier,type,abbreviation` and filter locally — keep `id` or the API returns an empty `data[]`; don't load every row into context). Match by `type` (1 = instrument → Field 31, 2 = observatory → Field 32), comparing against the row `name`, its `abbreviation`, source parenthetical aliases, and the SPASE identifier path segments (repos often mention only an acronym like `MFI`/`AIA`, and the path carries platform evidence, e.g. `.../GOES/17/SUVI`). Treat `.html` and bare identifiers as the same resource (prefer the bare one). Prefer `SMWG/...` only as a tie-breaker among same-name duplicates — a single non-SMWG match is still correct (Solar Orbiter is `ESA/Observatory/SolarOrbiter`). **Copy the matched row's `name` verbatim.**

**Vocabulary state (verify, don't assume).** As of the PR #54 backfill (2026-07-07) the vocabulary is 100% SPASE-backed — 7,648 rows, 0 non-SPASE — re-verified 2026-07-27. Treat that as a **dated observation, not an invariant**. Keep `identifier.startswith("https://spase-metadata.org/")` as a **real guard**: any row failing it means either upstream drift or a row an agent wrongly created, and must be **reported, never used**.

Then apply the ladder in order and stop at the first rule that fires:

1. **Exactly one row matches** → emit that row's `name` (verbatim) + its `identifier`. Done.
2. **Several rows match and specific in-repo evidence names which ones** → emit **all** the evidenced rows, and cite the evidence in the source note. Evidence means a concrete artifact — a supported-version list (`VALID_SPACECRAFT = [16, 17, 18, 19]` → the four GOES SUVI rows), a station table (THEMIS ASI → its 24 `SMWG/Instrument/THEMIS/Ground/*/ASI` rows), an explicit doc/API statement (DMSP SSJ → the F16/F17/F18 rows; SECCHI → STEREO-A and STEREO-B). A plausible guess is not evidence.
3. **Several rows match and nothing in the repo selects among them** → record `NEEDS MANUAL RESOLUTION (ambiguous instrument/observatory)` listing the candidate identifiers. Non-submittable; the user picks.
4. **No row for the instrument, but its platform/mission has one** → associate the **observatory** row instead and note the substitution. (SPASE/HDRL guidance, 2026-07-01: a missing instrument record should not block the software's association; prefer the observatory/platform record. PR #54 precedent: MGS Radio Science Subsystem → `SMWG/Observatory/MGS`; GOES-13 Imager → `SMWG/Observatory/GOES/13`; GOES-16 ABI → `SMWG/Observatory/GOES/16`.)
5. **Nothing defensible resolves** — a generic class label (`Ionosonde`, `Digital All Sky Cameras`), or something outside heliophysics scope (`NEXRAD`) → **omit the entry and document why.** A documented omission is a correct outcome, not a failure.
6. **Never emit a `name` without an `identifier`.** There is no free-type path for agents. The backend's no-identifier fallback is a case-sensitive `filter(name=…, type=…).first()` that either binds to an arbitrary same-name row or **creates a new identifierless row** (`serializers/submission.py`) — reintroducing exactly the legacy rows PR #54 deleted (63 → 0). If an entry does not resolve, it is omitted (5) or flagged (3) — never invented. A genuinely new instrument enters the vocabulary through the heliophysics.net refresh, not through a submission.

See the `submission-payload` / `update-payload` skills for the payload-level restatement.

**Sub-fields:**
- **Instrument Name** (OPTIONAL): Name of the instrument — the matched controlled-list row's `name`, copied verbatim
- **Instrument Identifier** (OPTIONAL): Globally unique persistent identifier — for controlled-list resolution this is the SPASE Resource ID URL from the list (e.g. `https://spase-metadata.org/SMWG/Instrument/...`). Optional on the form, but **for agents it is mandatory in practice**: an entry without one is not submittable (ladder rule 6). A human may supply a DOI as a manual exception, but **agents must not substitute a DOI to satisfy controlled-list resolution** — resolve to SPASE, or omit per rule 5. (A genuine repo-provided instrument DOI may be recorded in the source note as out-of-vocab context, but it never becomes the identifier.) Enables improved linking and reliable matching.

---

### 32. Related Observatories (OPTIONAL)
**Type:** Multi-entry nested group

**What it is:** The mission, observatory, and/or group of instruments the software is designed to support.

**When to include it (relevance):** List a mission/observatory only if the software is *designed to support* it — it directly works with that observatory's/mission's data or data products, implements its data conventions, is purpose-built or a mission-team tool for it, or models/visualizes its measurements as a primary function. Sanity check: would a user searching HSSI for `observatory:"X"`, or a scientist working with X's data, expect this software back? If not, leave it out. **Exclude** observatory-agnostic tools (general models/utilities support none specifically), tutorial/demo/example name-drops and "platforms you *could* support," "configurable for a location/observatory" general tools, and links that belong to another field — a **generic/multi-mission** *data archive/source* (e.g. CDAWeb broadly) → Data Sources, or a generic *file convention* → Input/Output File Formats. **But** if the software directly supports a **specific named mission's** data — including via that mission's own archive, API, or format — that mission *is* designed-to-support: list it here **and** mark the source `observatory-specific` in Data Sources (Field 17 already instructs this cross-listing). A mission/observatory the software genuinely supports but that isn't in the controlled vocabulary is still *related* — don't drop it at the relevance stage. Carry it into the Field 31 resolution ladder, which decides between a broader platform association and a documented omission. "Related but unresolvable" is never a licence to invent a value.

**How to fill it:** Begin typing the name. Matches from HSSI's controlled instrument/observatory vocabulary appear in the dropdown; choose the correct one. This vocabulary is sourced from the heliophysics.net API and resolved to SPASE identifiers (it replaced the older IVOA-based list, which is now retired). If no entry matches, type the full name. **(That last sentence describes what the web form lets a *human* submitter do. Agents must never free-type a value — see Agent guidance below.)**

**Agent guidance:** Apply the **SPASE resolution ladder under Field 31** — it governs Field 32 identically, matching on `type` 2 (observatory) instead of 1. Do not restate or reinterpret it here.

Field-32-specific notes: match against the row `name`, its `abbreviation`, source parenthetical aliases (repos often mention only `PSP`/`MMS`), and the SPASE identifier path segments. The canonical SMWG name is often the long form — `SMWG/Observatory/THEMIS` is named "Time History of Events and Macroscale Interactions during Substorms", not "THEMIS" — so copy the row's `name` verbatim rather than re-deriving it. Ladder rule 4 (instrument → observatory fallback) has no analogue here: an observatory that doesn't resolve goes to rule 3 or rule 5. Rule 6 applies unchanged — **never emit an observatory name without an identifier.**

**Sub-fields:**
- **Observatory Name** (OPTIONAL): Name of the observatory/mission — the matched controlled-list row's `name`, copied verbatim
- **Observatory Identifier** (OPTIONAL): Globally unique persistent identifier — the SPASE Resource ID URL from the controlled list (e.g. `https://spase-metadata.org/SMWG/Observatory/...`). Optional on the form, but **for agents it is mandatory in practice**: an entry without one is not submittable (ladder rule 6). Enables improved linking and reliable matching.

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
  - Author Identifier (from `attributes.creators[].nameIdentifiers[]`): an **ORCID** (`nameIdentifierScheme` = "ORCID") for person creators, or a **ROR** (`nameIdentifierScheme` = "ROR", usually with `nameType` = "Organizational") for organization creators
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
