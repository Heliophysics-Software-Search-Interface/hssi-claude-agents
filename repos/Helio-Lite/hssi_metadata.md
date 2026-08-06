# HSSI Metadata Extraction Results

**HSSI Software ID:** 86c00a32-6dca-4d77-bddb-75c36d0ec0ca
**Repository:** https://github.com/indiajacksonphd/Helio-Lite
**Source Revision:** e5836e75e294a56e45e768b45ee4890d8d7a0140
**Extraction Date:** 2026-08-04
**Validation Date:** 2026-08-05
**Validation Status:** PASS

---

## Scope note

Helio-Lite is a **deployment framework**, not a library. It ships no importable package and has no
`setup.py`/`pyproject.toml`; the "software" is a set of bootstrap scripts, Conda environment
specifications, four custom Python data-retrieval modules, a JupyterHub login template, and example
notebooks. Two consequences shape the evidence below and should be read before any field is revised:

1. **A large fraction of the repository is other people's software.** `libraries_dependencies/requirements.txt`
   pins roughly 250 packages and is derived from the PyHC Docker environment; `START_HERE/jupyterHubBootstrap.py`
   is a vendored copy of The Littlest JupyterHub's own installer. Capabilities belonging to those
   bundled packages are **not** Helio-Lite capabilities, and several fields below record explicitly
   why a tempting classification was rejected on that ground.
2. **The shipped example notebooks are of two kinds.** `examples/AIA_DONKI_DMLab/` exercises
   Helio-Lite's *own* modules and is primary evidence of what the software does.
   `examples/PyHC/` and `examples/AI_ML/` are demonstrations of *bundled third-party packages*
   (several are verbatim upstream tutorials) and are weak evidence at best. Where a field's value
   turns on that distinction, the note says so.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*The person who originally submitted this record is not identified in the sources available for it,
so no submitter identity is asserted here.*

---

### 2. Persistent Identifier (RECOMMENDED)
`https://doi.org/10.5281/zenodo.17611740`

Carried over from the existing HSSI record and independently confirmed correct. The Zenodo API for
record 17611741 returns `"conceptdoi": "10.5281/zenodo.17611740"` — so 17611740 is the *concept*
(all-versions) DOI, which is exactly what Field 2 asks for, and 17611741 is the version DOI, which
belongs in Field 12 (and does).

**Rejected alternative:** `https://doi.org/10.5281/zenodo.17611741`. This is what the README's DOI
badge points at (`README.md` line 1), so a future agent reading only the README will be tempted to
"correct" Field 2 to it. Do not — it is the version-specific DOI and is already recorded in Field 12
as the Version PID. The existing split is right.

---

### 3. Code Repository (MANDATORY)
`https://github.com/indiajacksonphd/Helio-Lite`

Carried over from the existing HSSI record. Confirmed against the GitHub API, which returns
`full_name: indiajacksonphd/Helio-Lite`, `fork: false`, `archived: false`, `default_branch: main`.
Zenodo's `code:codeRepository` custom field carries the same URL.

**Rejected variant:** `https://github.com/indiajacksonphd/Helio-lite` (lower-case second "l"), which
is what `CITATION.cff` line 25 (`repository-code`) contains. GitHub resolves it by case-insensitive
redirect, but the canonical capitalisation is `Helio-Lite`. This is an upstream typo in CITATION.cff,
not drift in HSSI.

---

### 4. Software Functionality (MANDATORY)

- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: ML/AI
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Web-Based
- Servers and Environments
- Servers and Environments: Distribution/Access
- Servers and Environments: High Performance Computing
- Servers and Environments: Infrastructure as Code
- Servers and Environments: Software or Environment Container

Subcategories are written in the canonical `Parent: Child` form, and each parent is listed alongside
its subcategories.

**The previously stored set omitted both parents.** It was `Data Visualization`,
`Servers and Environments: High Performance Computing`,
`Data Processing and Analysis: Data Access and Retrieval`,
`Data Processing and Analysis: Analysis`,
`Servers and Environments: Software or Environment Container` — four subcategories under two parents,
with neither parent named. `Data Processing and Analysis` and `Servers and Environments` are
therefore part of this value on their own account, independent of the subcategories added below.

Evidence for each value:

- **Data Processing and Analysis: Data Access and Retrieval** — the software's headline feature.
  `custom_modules/aiaImages.py:132` `fetch_aia_images(year, month, day, wavelength)` scrapes the JSOC
  directory `http://jsoc.stanford.edu/data/aia/images/{year}/{month}/{day}/{wavelength}/` and
  downloads the selected `.jp2` files; `custom_modules/hmiImages.py:132` `fetch_hmi_images()` does the
  same for `http://jsoc.stanford.edu/data/hmi/images/{...}` and `.jpg`;
  `custom_modules/donkiData.py:29` `fetch_space_weather_data()` calls
  `https://kauai.ccmc.gsfc.nasa.gov/DONKI/WS/get/{FLR,SEP,CME}`; `custom_modules/dmLab.py:11`
  `get_dataset()` reads `s3://dmlab-datasets1/{name}.csv`.
- **Data Processing and Analysis: Analysis** — `examples/AIA_DONKI_DMLab/GSEP_DMLab.ipynb` cleans the
  GSEP event list, coerces `ppf_gt100MeV` to numeric, extracts the C/M/X letter from `fl_goes_class`
  with a regex, and computes per-class means of the >100 MeV proton peak flux. That is a derived
  physical result, not just plumbing.
- **Data Processing and Analysis: File Format Conversion** — added. `aiaImages.py:77` opens the
  fetched JPEG 2000 with PIL and writes PNG (`.replace('.jp2', '.png')`, `image.save(save_path)`);
  `hmiImages.py:77` converts `.jpg` to PNG the same way. Reading one container format and writing
  another is precisely this subcategory.
- **Data Processing and Analysis: ML/AI** — added. Helio-Lite provisions a dedicated AI/ML runtime:
  `libraries_dependencies/ml.yml` declares `scikit-learn`, `keras`, `pytorch`, `tensorflow`,
  `torchvision`, `tensorboard`, `xgboost`; `kernel_creation/create_aiml_kernel.sh` builds it and
  registers it as the "AI-ML Packages" Jupyter kernel; `examples/AI_ML/` ships four worked ML
  notebooks (`tensorflow_keras_classification.ipynb`, `xgboost.ipynb`,
  `pytorch_torchvision_RNN_PT.ipynb`, `seaborn.ipynb`). The software's own abstract states it
  "provides essential prerequisites for artificial intelligence (AI) and machine learning (ML)
  applications" — an advertised primary function.
  The four ML notebooks are **generic** ML tutorials (Fashion-MNIST, the Pima diabetes CSV, a toy
  RNN, the seaborn tips/iris datasets), not heliophysics ML, so this value rests on the provisioned
  kernel plus the advertised purpose rather than on any heliophysics-specific model in the
  repository. That is the correct basis — enabling AI/ML is what this software is for — and it is
  stated precisely here because the value cannot be defended by claiming the examples are science ML.
- **Data Processing and Analysis: Processing** — added. User-facing data-preparation transforms:
  `aiaImages.py:18` `utc_to_local()` and `:36` `local_to_utc()` (exposed to users through
  `examples/AIA_DONKI_DMLab/TimeConversion.ipynb` and used as the first step of
  `AIA_DONKI.ipynb`/`HMI_DONKI.ipynb`), plus the DONKI event-record reshaping in
  `donkiData.py:54/88/105` (`format_solar_flare_data`, `format_sep_data`, `format_cme_data`, which
  flatten nested `instruments`/`linkedEvents`/`cmeAnalyses` structures) and the GSEP cleaning
  pipeline noted above.
- **Data Visualization: Web-Based** — added, and strongly evidenced. The entire delivery mechanism is
  a browser-based JupyterHub. `aiaImages.py:141-152` builds an interactive `ipywidgets`
  `SelectMultiple` + `Button` UI and `:121-128` renders the selected solar images into a scrollable
  HTML container of base64-embedded `<img>` tags displayed in the browser; `donkiData.py:147-156`
  renders flare/SEP/CME records as `widgets.HTML` inside an `HBox`.
- **Data Visualization: 2D Graphics** — added, on two primary-tier citations from Helio-Lite's own
  code and own-module examples: two-dimensional image display of the fetched solar images
  (`aiaImages.py:111`, 256x256 `<img>` panels with captions), and the chart produced by
  `examples/AIA_DONKI_DMLab/GSEP_DMLab.ipynb`, whose final cell is
  `sns.barplot(x=flare_class_means.index, y=flare_class_means.values)` with the axes labelled "Solar
  Flare Class" and "Mean ppf_gt100MeV" — a visualization of the notebook's own derived result. The
  polar scatter of planetary heliographic positions in `examples/PyHC/planet_locations.ipynb` also
  qualifies on its face, but it is a bundled-package demonstration and is therefore *not* relied on
  here; see the scope note.
- **Servers and Environments: Software or Environment Container** — `kernel_creation/create_aiml_kernel.sh`
  and `create_pyhc_kernel.sh` create two isolated Conda prefixes (`/opt/tljh/user/envs/ai-ml` and
  `/opt/tljh/user/envs/pyhc-all`) from `ml.yml` and `environment.yml` and register each as a Jupyter
  kernel. Reproducible environment construction is the software's core deliverable.
- **Servers and Environments: Infrastructure as Code** — added, and the single most under-represented
  capability in the previous record. `START_HERE/jupyterHubBootstrap.py` (515 lines) is run as EC2
  user-data to install JupyterHub unattended; the README's Step 2 user-data block issues
  `tljh-config set https.enabled false` and rewrites `c.JupyterHub.template_paths`;
  `START_HERE/create_directories.sh` provisions `/shared`, clones the CDF library, and downloads the
  examples and modules; `START_HERE/link_directories.sh` is installed into `/etc/profile.d/` to
  symlink the shared tree per user. The repository *is* scripted cloud provisioning.
- **Servers and Environments: Distribution/Access** — added. The deployed platform is explicitly
  multi-user and data-sharing: README "Account Creation / User Login" ("New users simply create a
  username and password of their liking on the homepage"), `custom_templates/login.html` as the
  self-service login page, and `create_directories.sh`/`link_directories.sh` creating a
  world-writable `/shared` tree symlinked into every user's home. The abstract calls Helio-Lite "a
  specialized tool for data sharing and computation."
- **Servers and Environments: High Performance Computing** — retained from the existing record. Its
  basis is the prescribed hardware envelope: README Step 2 requires an EC2 `c5.4xlarge` "or larger"
  with at least 500 GiB gp3 EBS, and the abstract's premise is "accessible and scalable computational
  resources." This is the weakest of the fourteen values — a 16-vCPU cloud VM is not conventionally
  HPC — but it is a submitted value with a defensible reading (scalable cloud compute), so it is kept
  rather than removed. Recorded here so a future refresh knows the reasoning rather than re-deriving it.

**Considered and rejected — do not re-propose these without new evidence:**

- **Coordinate Transforms (and its Solar / Magnetospheric children).** `examples/PyHC/coordinate_systems.ipynb`
  performs GEO→SM with `spacepy.coordinates.Coords`, round-trips through `astropy` `SkyCoord`, and
  transforms to `sunpy.coordinates.frames.HeliographicCarrington` and `itrs`;
  `coordinates_demo.ipynb` uses `Helioprojective`, `HeliographicStonyhurst`, `Heliocentric` and
  `AltAz`. **None of this is Helio-Lite code.** These notebooks are demonstrations of the bundled
  spacepy/sunpy/astropy packages, which `examples/README.md` describes as "heliophysics examples,
  designed to work with the `pyhc` kernel." Helio-Lite implements no transform of its own, and
  claiming the capability would make its record indistinguishable from that of any environment that
  installs sunpy.
- **Models and Simulations (any child).** The bundled kernel contains models (`iri2016`, `msise00`,
  `igrf`, `geopack`, `wmm2020`, `pfsspy`, `enlilviz`, …) but Helio-Lite implements none and runs none.
- **Mission-related (any child).** Helio-Lite reads SDO data products; it is not part of SDO's ground
  system or any mission pipeline. The taxonomy draws exactly this line.
- **Data Processing and Analysis: Image Processing.** Considered because the software fetches and
  displays solar images, but the only operations performed on pixel data are container-format
  conversion and HTML-scale display. There is no deconvolution, feature detection, calibration, or
  `scikit-image` use in Helio-Lite's own code (the one PIL `thumbnail()` call, `aiaImages.py:98`, is
  commented out). Captured instead as *File Format Conversion*.
- **Data Processing and Analysis: Time Series Analysis.** The DONKI queries are date-range bounded and
  the GSEP catalog is an event list, but nothing in Helio-Lite's code performs temporal filtering,
  autocorrelation, resampling or trend analysis. `examples/PyHC/pytplot_demo.ipynb` displays time
  series, but that is PyTplot's capability, not Helio-Lite's.
- **Data Visualization: Line Plots** and **Data Visualization: ML/AI.** The line/loss plots live in
  `examples/AI_ML/tensorflow_keras_classification.ipynb`, which is a verbatim copy of the upstream
  TensorFlow Keras tutorial (it carries François Chollet's MIT header and the Apache-2.0 notice in
  its first two cells). Upstream tutorial content is not a capability of the software that ships it.
- **Servers and Environments: Data servers processing and handling.** Helio-Lite stands up a
  *notebook/compute* server, not a data server: it exposes no data-serving endpoint, protocol, or
  catalog. The sharing dimension is already carried by *Distribution/Access*.

---

### 5. Related Region (MANDATORY)

- Solar Environment
- Corona
- Chromosphere
- Photosphere
- Interplanetary Space

`Solar Environment` is carried over from the existing HSSI record; the other four are added because
this field asks for the most specific applicable region, and older records were built from a much
broader five-value shortlist that stopped at `Solar Environment`.

- **Solar Environment** — retained. Broad but accurate, and it was the submitted value.
- **Corona** — `examples/AIA_DONKI_DMLab/AIA_DONKI.ipynb` calls
  `aiaImages.fetch_aia_images(2017, 9, 10, 94)`; the 94 Å AIA channel images hot coronal plasma. The
  DONKI CME analyses the software retrieves are parameterised at 21.5 solar radii
  (`donkiData.py:125`, `analysis['time21_5']`), i.e. the outer corona.
- **Chromosphere** — kept, on a **weaker evidentiary tier than the other four; a future agent should
  know which tier before defending it.** The basis is *documented support*, not demonstrated use.
  `fetch_aia_images()` takes `wavelength` as a free parameter and interpolates it straight into the
  JSOC path (`aiaImages.py:134`) with no allow-list, no validation and no default — but the stronger
  point is that the software documents its own valid range. The first (markdown) cell of **both**
  `examples/AIA_DONKI_DMLab/AIA_DONKI.ipynb` and `HMI_DONKI.ipynb`, in the own-module
  primary-evidence folder, carries a "Parameter Options" list reading verbatim:

  > `- **wavelength**: 94, 131, 171, 193, 211, 304, 335, 1600, 1700, 4500`

  So 304 Å (He II, chromosphere/transition region) and 1600/1700 Å (upper photosphere/chromosphere)
  are values this software's own documentation advertises as supported inputs, not merely values a
  permissive parameter fails to reject. HSSI's own controlled `InstrumentObservatory` row for AIA
  independently carries the same list in its SPASE definition text — "seven extreme UV (EUV) band
  passes (94, 131, 171, 193, 211, 304 and 335 Å), and 24 seconds for two UV channels (1600 and
  1700 Å)" — confirming these are real AIA channels rather than a plausible-looking list. Of the two
  notebooks, `AIA_DONKI.ipynb` is the load-bearing citation: `HMI_DONKI.ipynb`'s copy of the list is
  a copy-paste artifact, since `hmiImages.fetch_hmi_images` accepts a `wavelength` argument that its
  JSOC path never uses.

  **What keeps this a weaker tier is the gap between documented and exercised: the only wavelength
  ever passed to a function call anywhere in the repository is `94`** — `AIA_DONKI.ipynb` cell 5,
  `aiaImages.fetch_aia_images(2017, 9, 10, 94)`, and `HMI_DONKI.ipynb` cell 5 passing the same `94`
  into the argument HMI ignores. No example, test or docstring anywhere retrieves a chromospheric
  wavelength.

  Contrast the other four: Corona has a literal call site, Photosphere a dedicated module retrieving
  HMI surface products, Interplanetary Space actual SEP retrieval and analysis, and Solar Environment
  is the stored value's own basis. Chromosphere rests on documented-but-unexercised support, which
  is a real basis: the software advertises those channels, and a user fetching 304 Å is doing exactly
  what the module exists to do. The tier is recorded rather than glossed so that any future refresh
  weighing whether to prune Field 5 starts from this evidence instead of rediscovering the gap and
  mistaking it for an error.
- **Photosphere** — `hmiImages.fetch_hmi_images()` retrieves HMI browse products from
  `http://jsoc.stanford.edu/data/hmi/images/`, i.e. continuum intensity, magnetogram and Dopplergram
  images of the photosphere.
- **Interplanetary Space** — the software retrieves and analyses solar energetic particle events:
  `donkiData.py:39-43` queries the DONKI `SEP` endpoint and `:88` formats the results, and
  `GSEP_DMLab.ipynb` analyses >100 MeV proton peak flux from the GSEP catalog. SEP transport and CME
  propagation to 1 AU are interplanetary by nature.

**Considered and rejected:**

- **Solar Interior.** HMI's science purpose includes helioseismology, but the software retrieves only
  HMI *browse images* of surface observables — no helioseismic power spectra or inversions.
- **Earth Magnetosphere.** `examples/PyHC/pyspedas_demo.ipynb` loads THEMIS-D and MMS-1 FGM
  magnetospheric field data. That is a demonstration of the bundled PySPEDAS package, not a
  Helio-Lite capability; see the scope note. A future agent scanning the notebooks will find this and
  should not re-add the region on its strength.

---

### 6. Authors (MANDATORY)

**Author 1: India Jackson**
- **Author Identifier:** `https://orcid.org/0009-0001-5404-8689`
- **Affiliation:** Georgia State University — `https://ror.org/03qt6ba18`

Carried over from the existing HSSI record and independently confirmed against three primary sources:
`CITATION.cff` lines 15-21 (`given-names: India`, `family-names: Jackson`, `affiliation: Georgia
State University`, `orcid: https://orcid.org/0009-0001-5404-8689`); the Zenodo record
(`creators: [{name: "Jackson, India", affiliation: "Georgia State University", orcid:
"0009-0001-5404-8689"}]`); and the public ORCID record itself, whose current employment
(2025-02 → 2027-01, "Atmospheric & Geospace Postdoctoral Fellow", Department of Physics & Astronomy)
carries the ROR disambiguation `https://ror.org/03qt6ba18`. The affiliation is therefore current, not
merely historical. The ROR record for `03qt6ba18` has `ror_display` "Georgia State University" and
status `active`.

**Berkay Aydin and Petrus Martens are deliberately NOT listed as software authors.** They are
co-authors of the reference publication (Field 14), and a future agent working from that paper will be
tempted to add them. The software's own authorship statement is explicit and contradicts that: the
Description's Author Note (also present verbatim in the Zenodo record and the GitHub release notes)
reads "Helio-Lite was conceptualized, designed, and implemented by Dr. India R. Jackson … Dr. Jackson
led all phases of design, implementation, and documentation. Advisors: Dr. Petrus Martens and Dr.
Berkay Aydin provided feedback on functionality, usability, and testing." `CITATION.cff` lists one
author; the Zenodo software record lists one creator; the GitHub contributor list has exactly one
entry (`indiajacksonphd`, 312 commits — the git history carries two author *name strings*, "India
Jackson" on 268 commits and "India Jackson, PhD" on 44, but a single author email
`ijackson1@gsu.edu`, so that is one person, not two). Advisory feedback on a paper is not software authorship. For
reference, their ORCIDs are Berkay Aydin `https://orcid.org/0000-0002-9799-9265` and Petrus Martens
`https://orcid.org/0000-0001-8078-6856` — recorded here as context, not as values to add.

**Rejected name variant:** "India R. Jackson". The middle initial appears only in the prose Author
Note. ORCID, CITATION.cff and Zenodo all give the name without it. `CITATION.cff` also carries
`name-suffix: PhD`, which HSSI has no field for and which is not part of the name.

---

### 7. Software Name (MANDATORY)
`Helio-Lite: A Lightweight Version of HelioCloud`

Carried over from the existing HSSI record and **deliberately preserved**. It is the exact title of
the Zenodo software record that mints this software's DOI, so it is the name under which the software
is formally published and citable.

**Rejected alternatives, and why:**

- `Helio-Lite` — the bare repository name (GitHub `full_name: indiajacksonphd/Helio-Lite`) and what
  SoMEF extracts as `name`. Field 7's own wording ("as listed on the code repository") points here, so
  this is the most likely future "correction". It is rejected because the stored value is the
  published DOI title and is a submitter/curator editorial choice that carries more information
  (it states the relationship to HelioCloud). Changing a name for stylistic preference is not an
  improvement.
- `Helio-lite` — `CITATION.cff` line 5 (`title`). Lower-case "l"; inconsistent with every other
  source including the repository itself.
- `Helio-Lite: An Open Cloud Framework for Advancing Heliophysics Research` — the *paper* title
  (Field 14). Rejected: that is the title of the publication, not of the software.

---

### 8. Description (MANDATORY)

```
Helio-Lite v0.1.0

Abstract

In the rapidly evolving field of heliophysics research, the demand for accessible and scalable computational resources is paramount. Helio-Lite, a free and open-source framework operating within the Amazon Web Services (AWS) ecosystem, leverages its infrastructure and services to provide a reproducible research environment. Derived from HelioCloud, it supports smaller research groups, provides essential prerequisites for artificial intelligence (AI) and machine learning (ML) applications, and serves as a specialized tool for data sharing and computation. Utilizing AWS’s robust data storage and processing capabilities, Helio-Lite integrates customized Python kernels for heliophysics and AI/ML, facilitating efficient data analysis and advancing our understanding of solar phenomena. Key functionalities include interactive data extraction modules for Atmospheric Imaging Assembly (AIA) and Helioseismic and Magnetic Imager (HMI) images, and near real-time space weather data from the Database of Notifications, Knowledge, Information (DONKI). A comprehensive examples repository further supports users in analysis and exploration. Helio-Lite addresses challenges posed by large solar datasets by parsing directly from Amazon Simple Storage Service (S3) buckets, improving accessibility and efficiency. Moving forward, Helio-Lite will continue to evolve through community feedback and iterative development to enhance usability and system management.

Simple Language

In simple terms:

1. You launch an AWS EC2 instance and paste the Helio-Lite bootstrap script.
2. The system automatically installs JupyterHub and configures two Conda environments: AI/ML and PyHC.
3. You access the JupyterHub interface from your browser and run preloaded heliophysics examples.
4. You can add new users, share data, and extend the platform for custom research workflows.

Helio-Lite bridges professional and citizen research, making space-weather analysis accessible, reproducible, and cloud-ready.

System Overview

- AWS services: EC2, S3, CloudFront, Route 53, CloudWatch, IAM
- External APIs: JSOC (AIA/HMI), DONKI (space weather events)
- Outputs: Jupyter notebooks, CSV datasets, Conda environments, tutorial video

AWS architecture diagram: https://indiajacksonphd.s3.us-east-1.amazonaws.com/architecture.pdf
Setup tutorial on YouTube: https://www.youtube.com/watch?v=318Z1h9paMU

Repository Structure

- START_HERE/ – automated bootstrap scripts for EC2 deployment
- custom_modules/ – Python utilities for data extraction and processing
- custom_templates/ – JupyterHub login and UI templates
- examples/ – example Jupyter notebooks (e.g., AI/ML, solar data analysis)
- kernel_creation/ – scripts for creating Conda kernels (AI/ML and PyHC)
- libraries_dependencies/ – environment and requirements files (requirements.txt, environment.yml)
- README.md – main project documentation

Author Note

Helio-Lite was conceptualized, designed, and implemented by Dr. India R. Jackson as part of her PhD dissertation work at Georgia State University. The platform was inspired by and developed as a lightweight, single-instance counterpart to HelioCloud (https://github.com/heliocloud-data). Dr. Jackson led all phases of design, implementation, and documentation. Advisors: Dr. Petrus Martens and Dr. Berkay Aydin provided feedback on functionality, usability, and testing.

Version Info

- Release type: First public release
- Tag: v.0.1.0
- License: MIT
```

**This supersedes the previously stored Description.** The author's own prose is preserved verbatim
throughout — including its punctuation, character for character. What changed are four specific
defects introduced when the Zenodo record's HTML was flattened into plain text on submission, plus
one factual error.

The source of truth is the Zenodo record's `metadata.description` HTML, which the previously stored
text is a lossy rendering of. The four repairs:

1. **Two dead links restored.** The stored text contained the bare strings
   `Click here to view the AWS Architecture!` and `Click here watch the setup tutorial on YouTube!`
   with no URLs — the `<a href>` targets were discarded by the flattening. The Zenodo HTML has them:
   `<a href="https://indiajacksonphd.s3.us-east-1.amazonaws.com/architecture.pdf">here</a>` and
   `<a href="https://www.youtube.com/watch?v=318Z1h9paMU">here</a>`. Both targets are live: the architecture URL serves a
   183 KB PDF, and the YouTube URL is independently corroborated by `README.md` lines 26-30, which
   embed the same video ID `318Z1h9paMU`. They are rendered as labelled explicit URLs rather than "Click here" link text,
   because plain-text metadata cannot carry a hyperlink and because the author's original second
   sentence has a missing word ("Click here watch"). Recasting them sidesteps reproducing that typo.
2. **Missing spaces after sentences in the Author Note restored.** The stored text read
   `…Georgia State University.The platform…`, `…(https://github.com/heliocloud-data).Dr. Jackson…`
   and `…documentation.Advisors:…`. Those are `<br>` tags dropped without substituting whitespace;
   Field 8 requires proper punctuation.
3. **`Tag: v0.1.0` corrected to `Tag: v.0.1.0`.** The actual git tag and GitHub release `tag_name`
   are `v.0.1.0`, with a literal dot after `v`. The upstream Zenodo description and the GitHub release
   notes both write it as `v0.1.0` in prose; that is an upstream error, and Field 12 already stores
   the correct string.
4. **Markdown-ish list markers normalised** (`1.`–`4.` for the ordered "Simple Language" steps, `-`
   for the bullet lists). Stripping the `<ol>`/`<ul>` markup left the list items separated by runs of
   blank lines and carrying no markers at all — literally
   `In simple terms:\n\n\n\n\n\nYou launch an AWS EC2 instance…` — so the items no longer read as a list.

**Deliberately *not* changed: the eight non-ASCII characters.** Both authoritative sources — the
Zenodo `metadata.description` HTML (as the entities `&rsquo;` ×1 and `&ndash;` ×7) and the
currently stored HSSI Description (as the decoded characters) — carry exactly eight non-ASCII
code points, and the text above reproduces all eight:

| Character | Count | Where |
|---|---|---|
| U+2019 RIGHT SINGLE QUOTATION MARK | 1 | `Utilizing AWS’s robust data storage` |
| U+2013 EN DASH | 7 | the separator in each Repository Structure bullet, e.g. `START_HERE/ – automated…` |

They are the author's typography, not damage, and flattening them to `'` and `-` would be an
undisclosed rewrite of her punctuation. Keeping them also keeps the eventual change to this field
confined to the four repairs above. **A future agent editing this block must preserve them**; a scan
of the Description for characters above U+007F must return exactly these eight.

**Considered and rejected: deleting the "Repository Structure" block.** It is repository-layout
information rather than a description of capability, and Field 3 already links the repository, which
is a genuine argument for cutting it. It is kept because it is the author's own published Zenodo
content, it tells a prospective user concretely what the distribution contains, and removing
author-written substance is a larger editorial intervention than repairing flattening damage. The
block is self-contained, so a later curator who weighs it differently can drop it without disturbing
anything else in this field.

**Considered and rejected: replacing the whole text with the README's opening paragraph or with the
`CITATION.cff` `abstract`.** Both are shorter and cleaner, but both are *less* informative than the
Zenodo abstract, and the CITATION.cff abstract is an earlier draft of the same paragraph (e.g.
"Helio-Lite is poised to undergo continuous enhancements" versus the Zenodo text's "will continue to
evolve through community feedback and iterative development"). The published DOI record is the more
authoritative of the two.

---

### 9. Concise Description (OPTIONAL)

```
A free, open-source AWS framework that deploys a reproducible single-instance JupyterHub for heliophysics, bundling PyHC and AI/ML Python kernels, AIA/HMI and DONKI data modules, and examples.
```

192 characters — within the 200-character maximum and inside the 150-200 target band.

**This supersedes a broken stored value.** The previous Concise Description was a mechanical
first-200-character slice of the Description, which is what Field 9 exists to override. It read
`"Helio-Lite v0.1.0\n\nAbstract\n\nIn the rapidly evolving field of heliophysics research, the demand
for accessible and scalable computational resources is paramount. Helio-Lite, a free and open-source
fra"` — it began with a version heading and a section label, contained embedded newlines, and was
cut mid-word at "fra". As a search-result preview it conveyed nothing about what the software does.

The replacement is written to stand alone and to name the four things a reader needs in order to
decide relevance: it is free and open source; it deploys a reproducible JupyterHub on AWS
(single-instance, distinguishing it from HelioCloud); it ships PyHC and AI/ML kernels; and it ships
AIA/HMI and DONKI data-retrieval modules plus examples. Every claim is drawn from the Description and
the README's "Key Features" list, so the preview and the full text cannot drift apart.

---

### 10. Publication Date (RECOMMENDED)
`2025-11-14`

Carried over from the existing HSSI record and confirmed twice: the Zenodo record's
`metadata.publication_date` is `2025-11-14`, and the GitHub release's `published_at` is
`2025-11-14T16:56:58Z`.

**Rejected alternatives.** `2025-08-14` — the GitHub release's `created_at` (`2025-08-14T23:05:23Z`)
and the date the `v.0.1.0` tag was cut (commit `5ba0d6b8`). The release was drafted in August and
published in November; publication is the later date. `2024-01-20` — the GitHub repository
`created_at`. That is when the code first became public, not when the software was published with a
DOI, and Field 10 is about publication of the initial version.

---

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** `https://zenodo.org`

Carried over from the existing HSSI record. Correct per Field 11's explicit guidance: the DOI was
obtained through the GitHub-Zenodo workflow, so Zenodo is the publisher, and `https://zenodo.org` is
the right identifier form where no ROR applies.

---

### 12. Version (RECOMMENDED)
- **Version Number:** `v.0.1.0`
- **Version Date:** `2025-11-14`
- **Version PID:** `https://doi.org/10.5281/zenodo.17611741`
- **Version Description:**
  ```
  First public release. Provides the complete Helio-Lite deployment path: a bootstrap script that installs JupyterHub (The Littlest JupyterHub) on a single AWS EC2 instance; scripts that build and register two Conda kernels, "AI-ML Packages" and "PyHC All Packages"; custom Python modules for AIA and HMI image retrieval from JSOC, DONKI space-weather event retrieval, and Georgia State University Data Mining Lab dataset access from Amazon S3; a customized JupyterHub login template; and example notebooks for PyHC, AI/ML, and solar data analysis. Archived on Zenodo as v.0.1.0.
  ```

**`v.0.1.0` is confirmed as the latest authoritative release.** The literal `v.` prefix (dot after
`v`) is not a transcription error — it is the exact string in all three authoritative places: the
only git tag in the repository is `v.0.1.0` (tagged commit `5ba0d6b8`), the GitHub API returns exactly
one release with `tag_name: v.0.1.0`, and Zenodo's `metadata.version` is `v.0.1.0`. `HEAD`
(`e5836e75`, 2026-06-11, "Update login.html") is one commit past the tag and no newer release,
pre-release or draft exists.

**Rejected version-number variant:** `v0.1.0` (no dot). This appears in prose in three places — the
Zenodo description's "Tag: v0.1.0", the GitHub release notes' "**Tag**: `v0.1.0`", and the
Description's own heading "Helio-Lite v0.1.0" — so it is well-attested as the *human-readable* form
and will look like the correction to make. It is not: the tag, the release, and the Zenodo version
field all carry the dot.

**Version Date** `2025-11-14` matches the release `published_at` and Zenodo's `publication_date`; the
2025-08-14 tag/draft date is the rejected alternative, for the same reason as Field 10.

**Version PID** `https://doi.org/10.5281/zenodo.17611741` is Zenodo's `doi` for this specific version
(the concept DOI 17611740 is correctly in Field 2). This is also what the README's DOI badge points at.

**The Version Description supersedes the previously stored one,** which was a byte-for-byte duplicate
of the full Field 8 Description. Field 12 asks for "a brief summary of major changes in the new
version," and duplicating the software-level description satisfies nothing while doubling the
maintenance burden of any future Description edit. The replacement is derived from the GitHub release
notes for "Initial Release" plus the repository contents at the tagged commit, and states what a first
release actually delivered.

**Documented upstream error in the release notes.** The GitHub release body's Repository Structure
section says "**LICENSE** – open-source license (Apache-2.0)" while its own Version Info section says
"**License**: MIT" and the shipped `LICENSE` file is MIT. The Apache-2.0 mention is simply wrong. It
is recorded here so that a future agent reading the release notes does not "correct" Field 15 to
Apache License 2.0. See Field 15.

---

### 13. Programming Language (RECOMMENDED)

- Javascript
- Python 3.x
- Other

Note the spelling of the first value: `Javascript`, not the usual `JavaScript`. That is the form this
field takes, and it should not be "corrected".

- **Python 3.x** — carried over. `libraries_dependencies/environment.yml` pins `python=3.9.18`;
  `ml.yml` pins `python=3.7`; the README copies modules into `.../lib/python3.7` and `.../lib/python3.9`;
  GitHub linguist reports Python as the dominant language (41,696 bytes). No Python 2 anywhere.
  The reference publication's own metadata states "Python 3.7–3.12".
- **Javascript** — carried over and confirmed as genuinely present, though the evidence needs care.
  GitHub linguist does *not* report JavaScript, because all of it is inline in HTML: linguist reports
  `Python 41696, HTML 8210, Shell 7481`. The JavaScript is real code, in
  `custom_templates/login.html`'s `{% block script %}` — a jQuery form-submit handler, a
  `window.isSecureContext` check that unhides the insecure-login warning, and a date computation that
  rewrites the background video's `source.src` to a per-day S3 object. Zenodo's
  `code:programmingLanguage` custom field independently asserts Python and JavaScript. Keep it.
- **Other** — added, standing for **Bash / shell**, which the vocabulary has no row for. Shell is
  13% of the codebase by linguist's count (7,481 bytes) and is not incidental: it is the deployment
  mechanism. `START_HERE/create_directories.sh`, `START_HERE/link_directories.sh`,
  `kernel_creation/create_aiml_kernel.sh`, `kernel_creation/create_pyhc_kernel.sh`, and the README's
  EC2 user-data block are all Bash. The reference publication's own Programming Language field reads
  "Python 3.7–3.12; Bash scripts for automation". `Other` is opaque, which is the cost of a closed
  vocabulary with no Shell row; the alternative — omitting a third of the deployment logic — is worse.

**Considered and rejected: HTML.** Linguist's second-largest language (8,210 bytes,
`custom_templates/login.html`). Rejected on two grounds: the vocabulary has no HTML/markup row, and
HTML is markup rather than a programming language. The executable content of that file is already
covered by `Javascript`.

---

### 14. Reference Publication (RECOMMENDED)
`https://doi.org/10.5334/jors.519`

Helio-Lite has a peer-reviewed software paper, and this DOI is it.

Jackson, I., Aydin, B., & Martens, P. (2026). *Helio-Lite: An Open Cloud Framework for Advancing
Heliophysics Research.* Journal of Open Research Software, 14(1), article 3. Published 2026-02-04.
Publisher: Ubiquity Press. Crossref confirms the DOI, title, container, volume 14, the three authors
with ORCIDs (India Jackson `0009-0001-5404-8689`, Berkay Aydin `0000-0002-9799-9265`, Petrus Martens
`0000-0001-8078-6856`), and the funding record NASA / award `80NSSC22K0272`. The article's own
metadata page names the software repository `https://github.com/indiajacksonphd/Helio-Lite`, the
archive `https://doi.org/10.5281/zenodo.17611741`, version archived `v0.1.0`, date archived
2025-11-14, and license MIT — all matching this record. This is a JORS software paper about exactly
this software, which is precisely what Field 14 asks for.

**On the DOI in `CITATION.cff`: `10.3847/1538-4365/ad3fba` is NOT the reference publication, and it is
NOT a cffinit copy/paste artifact from an unrelated paper either.** It resolves (via Crossref; DataCite
has no record, because the American Astronomical Society deposits with Crossref) to:

> Jackson, I., & Martens, P. (2024). *Advancing Solar Energetic Particle Event Prediction through
> Survival Analysis and Cloud Computing. I. Kaplan–Meier Estimation and Cox Proportional Hazards
> Modeling.* The Astrophysical Journal Supplement Series, 272(2), 37.

It is a real paper by the same first author, so the "artifact" hypothesis is wrong. But it does not
describe Helio-Lite: it is an SEP-prediction study that *uses* AWS together with the `lifelines` and
`scikit-survival` libraries. It never presents the platform. Field 14 wants "the publication
describing the software"; this one describes a science application built in the same cloud context.
It is therefore recorded in **Field 27 (Related Publications)** instead, which is the right home for
a publication the developer prioritises but which is not the reference publication — and the developer
did prioritise it, by placing it in `CITATION.cff`'s `identifiers:` block herself.

**Negative research on other candidate publications**, so this is not searched again:

- A Crossref author search on "India Jackson" returned exactly two heliophysics works: `10.5334/jors.519`
  and `10.3847/1538-4365/ad3fba`. Everything else returned was a different person.
- **Paper II of the survival-analysis series does not appear to be published as of 2026-08-04.**
  Paper I's title promises "a two-part series" and its abstract says predictive models "will be the
  focus of the subsequent paper," but no Paper II is indexed in Crossref or arXiv. If a later refresh
  finds it, it belongs in Field 27 alongside Paper I, not in Field 14.
- **The dissertation itself is not recorded.** The Description states Helio-Lite was built "as part of
  her PhD dissertation work at Georgia State University," and GSU's ScholarWorks hosts theses, but no
  DOI or stable landing page for that specific dissertation was located. The JORS paper is the
  peer-reviewed software publication and is the better value regardless.

---

### 15. License (RECOMMENDED)
- **License:** `MIT License`
- **License URI:** `https://spdx.org/licenses/MIT`

The URI is SPDX's own canonical URL for the MIT License, `https://spdx.org/licenses/MIT`, rather than
the `.html` variant `https://spdx.org/licenses/MIT.html` that SPDX also serves.

Four independent sources agree: the repository's `LICENSE` file is the MIT License text
("Copyright (c) 2024 India Jackson"); the GitHub API reports
`license: {key: mit, name: "MIT License", spdx_id: "MIT"}`; `CITATION.cff` line 58 is `license: MIT`;
Zenodo's `metadata.license` is `{"id": "mit-license"}`. The reference publication's metadata also
states MIT.

**Do not change this to Apache License 2.0.** The GitHub release notes for v.0.1.0 contain the line
"**LICENSE** – open-source license (Apache-2.0)" in their Repository Structure section, contradicting
their own Version Info section ("**License**: MIT") and the shipped file. That string is an upstream
mistake, and it lives only in the release notes on GitHub — the word "Apache" appears nowhere in the
repository's own licensing. The only Apache-2.0 text in the repository at all is inside
`examples/AI_ML/tensorflow_keras_classification.ipynb`, whose first two cells carry Apache-2.0 and
MIT headers because the notebook is copied verbatim from an upstream TensorFlow tutorial; that
governs that notebook's third-party content, not Helio-Lite.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- space weather
- heliophysics
- artificial intelligence
- machine learning
- cloud computing
- python
- amazon web services
- jupyter
- jupyterhub
- reproducibility
- citizen science
- solar energetic particles

**This supersedes a single malformed keyword row.** The previously stored value was **one** Keyword
row whose entire name was the comma-jammed string
`space weather, heliophysics, artificial intelligence, machine learning, cloud computing, python, amazon web services`.
Its upstream origin is `CITATION.cff` lines 53-57, where `keywords:` is a single YAML block scalar
(`- >-`) containing all seven terms in one string; Zenodo copied that faithfully
(`"keywords": ["space weather, heliophysics, artificial intelligence, machine learning, cloud computing, python, Amazon Web Services"]`)
and the submission carried it through. The result is unsearchable: none of the seven terms matches the
row, and the row matches nothing a user would type. Splitting it into the seven intended keywords is a
defect repair, not a re-interpretation.

The first seven values above are exactly that split, restored to the individual terms the author
intended. The test each term has to pass is simply whether it is one a reader would actually search
for — which is what the jammed eight-word string could never satisfy.

Five keywords are added beyond that split, each tied to evidence and each chosen to say something the
other 32 fields do not:

- **jupyter** and **jupyterhub** — the substrate of the entire product.
  `START_HERE/jupyterHubBootstrap.py` installs JupyterHub; `custom_templates/login.html` is its login
  page; `kernel_creation/*.sh` register Jupyter kernels; and the shipped examples are 16 Jupyter
  notebooks (`examples/` otherwise holds only its README and two CSVs that two of the notebooks read).
- **reproducibility** — the abstract's stated purpose ("to provide a reproducible research
  environment"), realised concretely by pinned environment specifications
  (`environment.yml` `python=3.9.18`, ~250 pinned lines in `requirements.txt`).
- **citizen science** — a distinguishing audience claim made repeatedly by the software itself:
  README paragraph 1 ("designed to empower heliophysics researchers in smaller groups and citizen
  scientists, particularly those operating within budget constraints") and the Description
  ("Helio-Lite bridges professional and citizen research").
- **solar energetic particles** — the software queries DONKI's `SEP` endpoint
  (`donkiData.py:39-43`), formats SEP events (`:88 format_sep_data`), and retrieves and analyses the
  GSEP catalog. SEPs have **no row in the Field 22 `Phenomena` vocabulary** (which offers only
  Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind,
  X-ray emission), and Field 22 explicitly directs an unlisted phenomenon to Keywords. This is that
  case.

**Considered and rejected, to prevent near-duplicate rows and cross-field duplication:**

- **`aws`** — a synonym of `amazon web services`; carrying both would leave a near-duplicate pair
  standing for one concept. `amazon web services` is the one kept, because it is the author's own
  wording in `CITATION.cff` and because Field 25's convention is to spell organisations out.
- **`solar flares`, `coronal mass ejections`, `solar dynamics observatory`** — all tempting, but
  Field 16 is for keywords "not supported by other metadata fields", and these are already carried by
  Field 22 (Solar Flares, Coronal Mass Ejections) and Field 32 (Solar Dynamics Observatory).
  Duplicating them here would add nothing a search could not already reach through those fields. The
  omission is deliberate, not a lookup failure.
- **`deep learning`, `solar`, `sun`, `solar physics`, `open source`** — each defensible in the
  abstract, none adding discriminating information beyond the keywords already listed.

---

### 17. Data Sources (OPTIONAL)

- HTTP/HTTPS Directories
- Observatory/Mission-specific
- S3/Cloud-aware
- Other

- **HTTP/HTTPS Directories** — `aiaImages.py:134` and `hmiImages.py:134` build a JSOC directory URL
  (`http://jsoc.stanford.edu/data/{aia,hmi}/images/{YYYY}/{MM}/{DD}/[{wavelength}/]`), `GET` it, and
  parse the returned Apache index with BeautifulSoup, selecting `<a href>` entries ending in `.jp2`
  or `.jpg`. That is literally scraping an HTTP directory listing.
- **Observatory/Mission-specific** — the same two modules exist only to retrieve SDO/AIA and SDO/HMI
  products from the mission's own science operations center. Field 17 instructs selecting this and
  naming the mission in Related Observatories; SDO is recorded in Field 32 accordingly.
- **S3/Cloud-aware** — `dmLab.py:5` creates an unauthenticated `boto3` S3 client and `:13` reads
  `pd.read_csv(f's3://{s3_bucket_name}/{csv_file}.csv')` against the public bucket `dmlab-datasets1`;
  `libraries_dependencies/custom_requirements.txt` provides `s3fs`, `fsspec`, `pyarrow`, `boto3` for
  exactly this. The abstract calls it out as a design feature: Helio-Lite "addresses challenges posed
  by large solar datasets by parsing directly from Amazon Simple Storage Service (S3) buckets."
- **Other** — for DONKI. `donkiData.py:30` queries
  `https://kauai.ccmc.gsfc.nasa.gov/DONKI/WS/get/{FLR,SEP,CME}?startDate=…&endDate=…`. DONKI is a
  multi-mission space-weather event web service with no row in the vocabulary, and Field 17's
  instruction for an unlisted source is to select `Other`.

**Considered and rejected: CDAWeb, HAPI, SSCWeb, Madrigal, VirES, `The Virtual Solar Observatory.`,
OMNIWeb.** All exist as rows, and the bundled PyHC kernel installs clients for every one of them
(`cdasws`, `hapiclient`, `sscws`, `madrigalWeb`, `viresclient`, `speasy`, `sunpy`'s Fido/VSO client
are all in `requirements.txt`). `examples/PyHC/pyspedas_demo.ipynb` even downloads THEMIS and MMS data
through PySPEDAS. None of these is a Helio-Lite data source: they are capabilities of packages
Helio-Lite installs, and asserting them would make this record claim support for the union of every
bundled client's archives — see the scope note. Helio-Lite's own four modules reach JSOC, DONKI and S3,
and nothing else.

---

### 18. Input File Formats (RECOMMENDED)

- csv
- JSON
- Other

`Other` is carried over from the existing HSSI record; `csv` and `JSON` are added. Fields 18 and 19
draw on the same list of formats.

- **csv** — `dmLab.py:13` `pd.read_csv('s3://dmlab-datasets1/{name}.csv')`, exercised for ten distinct
  catalogs in `examples/AIA_DONKI_DMLab/DMLab.ipynb`; plus the two local CSVs read by the ML examples
  (`examples/AI_ML/pima-indians-diabetes.data.csv` via `xgboost.ipynb`,
  `examples/AI_ML/marathon-data.csv` via `seaborn.ipynb`).
- **JSON** — `donkiData.py:37/43/49` consume DONKI responses via `response.json()`.
- **Other** — retained, and it is doing real work rather than papering over a gap. The AIA browse
  images are **JPEG 2000** (`.jp2`, `aiaImages.py:140/77`) and the HMI browse images are **JPEG**
  (`.jpg`, `hmiImages.py:140/77`); neither raster format has a row in the vocabulary. The HTML
  directory indices parsed with BeautifulSoup are likewise unrepresented.

**Considered and rejected: FITS and CDF.** Both are tempting. `create_directories.sh:4` clones
`heliophysicsPy/pyhc-docker-environment` specifically to install the NASA CDF library
(`cdf38_0-dist`) into `/usr/lib/`, and `requirements.txt` pins `astropy`, `aiapy`, `sunpy`, `cdflib`,
`pycdfpp`, `ccsdspy`, `netcdf4`, `h5py`. So the *deployed environment* reads FITS, CDF, netCDF and
HDF5 fluently. But no Helio-Lite code reads any of them — the AIA/HMI modules deliberately fetch JPEG
2000/JPEG browse images rather than science-grade FITS. These are bundled-package capabilities; see
the scope note. Also rejected on the same basis: the `.tplot` pickle restored in
`examples/PyHC/pytplot_demo.ipynb`, which is PyTplot's own serialisation format.

---

### 19. Output File Formats (RECOMMENDED)

- csv
- JSON
- Other

`csv` and `JSON` are carried over from the existing HSSI record; `Other` is added.

- **JSON** — `donkiData.py:10-16` `save_data_to_file()` does `json.dump(data, file, indent=4)` into
  `donki_data/donki_data_{start}_to_{end}.json`, wired to a "Save Data" button
  (`:18-26 create_save_button`).
- **Other** — added, for **PNG**. `aiaImages.py:77-79` and `hmiImages.py:77-79` write converted
  browse images to `aia_images/{date}/*.png` and `hmi_images/{date}/*.png` via `image.save(save_path)`,
  behind a "Save Images" button. PNG is not among the formats this field enumerates, which is what
  `Other` stands for here.
- **csv** — retained. Note the evidence is documentary rather than a code call: no `to_csv()` appears
  in the repository. It rests on the software's advertised capability — README "Storage of CSV
  Datasets in S3 Bucket: Helio-Lite enables the storage of CSV datasets in an Amazon S3 bucket. This
  approach includes 'parsing in place' capabilities…" and the Description's "Outputs: Jupyter
  notebooks, CSV datasets, Conda environments, tutorial video". Because it was also a submitted value,
  it is kept. Flagged here so a future refresh does not mistake the absence of a `to_csv()` call for
  evidence that the value is wrong.

---

### 20. Operating System (RECOMMENDED)
`Linux`

Carried over from the existing HSSI record; confirmed and deliberately left as the only value.
Helio-Lite is not cross-platform by design — it targets a Linux server, not a desktop. README Step 2
instructs "Operating System: Select Ubuntu"; the setup uses `apt-get install`; the underlying
distribution (The Littlest JupyterHub) supports only Ubuntu/Debian and `jupyterHubBootstrap.py`
enforces that with an explicit distro/version check; and `environment.yml` requests the
platform-specific compilers `gfortran_linux-64`, `gcc_linux-64`, `gxx_linux-64`.

**Considered and rejected: Mac, Windows, Operating System Independent.** No evidence of support for
any of them, and the bootstrap script actively refuses non-Debian-family systems.

---

### 21. CPU Architecture (RECOMMENDED)
`x86-64`

Carried over from the existing HSSI record and confirmed. README Step 2 prescribes an EC2
`c5.4xlarge` "or larger"; the C5 family is Intel Xeon x86-64. `environment.yml`'s compiler packages
are `*_linux-64` (Conda's x86-64 subdirectory).

**Considered and rejected: `Linux aarch64 or arm64` and `GPU`.** No ARM instance type is mentioned
and the pinned Conda packages are x86-64-only, so ARM is unsupported as documented. GPU was
considered because `ml.yml` and the README install `pytorch`, `tensorflow` and `torchvision`, but the
prescribed instance type has no GPU, nothing installs CUDA, and no code selects a device — the ML
stack runs on CPU as configured.

---

### 22. Related Phenomena (OPTIONAL)

- Solar Flares
- Coronal Mass Ejections
- Solar Corona

- **Solar Flares** — `donkiData.py:29` exposes `solar_flare=True`, which queries DONKI's `FLR`
  endpoint, and `:54 format_solar_flare_data()` renders flare ID, begin/peak/end times, class type,
  source location and active-region number. `examples/AIA_DONKI_DMLab/GSEP_DMLab.ipynb` classifies
  events by GOES flare class.
- **Coronal Mass Ejections** — `donkiData.py:45` exposes `cme=True` (DONKI `CME` endpoint) and
  `:105 format_cme_data()` renders each CME's activity ID, catalog, source location, and the per-event
  `cmeAnalyses` (latitude, longitude, half-angle, speed, type, level of data). The FL2CME datasets in
  Field 28 are flare-to-CME association catalogs.
- **Solar Corona** — the AIA imagery the software retrieves is coronal: `AIA_DONKI.ipynb` requests the
  94 Å channel, and the DONKI CME analyses are parameterised at 21.5 solar radii.

**Considered and rejected — Geomagnetic Storms.** DONKI does publish a `GST` (geomagnetic storm)
endpoint, so a future agent may reasonably expect it here. `donkiData.fetch_space_weather_data()`
exposes only three flags — `solar_flare`, `sep`, `cme` — and constructs only `FLR`, `SEP` and `CME`
URLs. Geomagnetic storms are not retrievable through this software as written. If the module later
gains a `gst` flag, add it.

**Considered and rejected — Solar Wind, Coronal Heating.** No solar-wind or coronal-heating data or
analysis in Helio-Lite's own code. (`examples/PyHC/pytplot_demo.ipynb` displays MAVEN SWIA solar-wind
variables, but that is PyTplot's bundled test file; see the scope note.)

**Considered and rejected — X-ray emission.** This is the closest of the rejections and has a real
argument behind it: the GSEP catalog column `fl_goes_class` that `GSEP_DMLab.ipynb` parses is a GOES
*soft X-ray* flare classification, and `DMLab.ipynb` retrieves `soho_goes_flares` and
`sdo_goes_flares`, which are GOES X-ray flare event lists. It is excluded because the software uses
the X-ray class as a flare *magnitude label* within an SEP study rather than doing X-ray science, and
`Solar Flares` already carries that meaning; adding it would assert a science focus the code does not
have. The argument is set out in full here so that a future agent meeting the same evidence can see it
was weighed rather than overlooked.

**Note on solar energetic particles.** SEPs are the phenomenon this software engages with most
directly (the DONKI `SEP` endpoint, the GSEP catalog, and the author's SEP-prediction paper in
Field 27), but the `Phenomena` vocabulary has no SEP row. Per Field 22's own instruction, it is
recorded in Field 16 Keywords as `solar energetic particles` instead. This is why Field 22 looks
thinner than the software's science focus would suggest.

---

### 23. Development Status (RECOMMENDED)
`Active`

The "reached a stable, usable state" half of the definition is settled: v.0.1.0 is a tagged release
with a Zenodo DOI, an MIT license, and a peer-reviewed software paper in the Journal of Open Research
Software (Field 14, published 2026-02-04). The repository is not archived (`archived: false`).

The "being actively developed" half is the judgement, and the commit record is genuinely sparse.
Commits by month: 255 in 2024-01 (the initial import), 1 in 2024-02, 3 in 2024-03, 9 in 2024-04, 1 in
2024-07, 41 in 2025-08 (release preparation), 1 in 2025-11, 1 in 2026-06 — 312 total, all from the
single contributor `indiajacksonphd` (one author email across the entire history; see Field 6 on the
two name spellings). Exactly one commit (`e5836e75`, 2026-06-11, "Update login.html")
postdates the 2025-11-14 release. There is no CI configuration, no open issues, no forks, and no
second contributor.

`Active` is chosen because the last commit is recent in absolute terms (2026-06-11, roughly two months
before this extraction), the software paper appeared only months earlier in 2026-02, the author's
stated intent in the abstract is continued work ("Helio-Lite will continue to evolve through
community feedback and iterative development"), and her ORCID shows a Georgia State University
postdoctoral appointment running to 2027-01. Low commit volume from a single maintainer is not the
same as abandonment.

**`Inactive` was the serious alternative and was rejected**, on the ground that its definition
requires the project to be "no longer actively developed" — which a maintainer who committed eight
weeks ago and published the software paper six months ago is not. This is the closest call in this
record, so the trigger for revisiting it is stated explicitly: **if a future refresh finds no commits
after `e5836e75` (2026-06-11) and still no release beyond v.0.1.0, `Inactive` becomes the better
value.** `WIP` and `Concept` are wrong in the other direction (there is a stable public release);
`Abandoned`, `Suspended`, `Unsupported` and `Moved` all require signals — an archive flag, a
deprecation notice, a relocation pointer — that are absent.

---

### 24. Documentation (RECOMMENDED)
`https://github.com/indiajacksonphd/Helio-Lite`

Carried over from the existing HSSI record and confirmed correct rather than merely tolerated. There
is no separate documentation site: the GitHub `homepage` field is `null`, there is no `docs/`
directory, no `.readthedocs.yml`, and no GitHub Pages (`has_pages: false`). The `README.md` *is* the
documentation and is unusually complete for this purpose — a six-step AWS setup walkthrough
(account, EC2 instance sizing, elastic IP, server access, environment creation), full kernel-creation
instructions for both environments, verification steps, and screenshots. Four subdirectory READMEs
(`START_HERE/`, `custom_modules/`, `examples/`, `kernel_creation/`, `libraries_dependencies/`) document
each component. Field 24 explicitly permits reusing the access URL when they coincide, which they do.

**Supplementary documentation not recorded here** because Field 24 takes a single URL: the 20-minute
setup video at `https://www.youtube.com/watch?v=318Z1h9paMU` (README lines 24-30, verified to resolve)
and the AWS architecture diagram at
`https://indiajacksonphd.s3.us-east-1.amazonaws.com/architecture.pdf` (a live PDF). Both are reachable from the Field 8 Description, which is why restoring those
links there mattered.

---

### 25. Funder (OPTIONAL)

**Funder 1: Heliophysics Science Division**
- **Funder Identifier:** `https://ror.org/03myraf72`

**Funder 2: National Aeronautics and Space Administration**
- **Funder Identifier:** `https://ror.org/027ka1x80`

Funder 1 is carried over from the existing HSSI record. Its origin is Zenodo's grant record for this
software, whose `funder.name` is "Heliophysics Science Division" and whose `internal_id` is
`03myraf72::80NSSC22K0272` — i.e. Zenodo's own OpenAIRE-backed lookup resolved award 80NSSC22K0272 to
that ROR. The ROR record for `03myraf72` confirms `ror_display` "Heliophysics Science Division",
types `["funder", "government"]`, status `active`, parent Goddard Space Flight Center. It is already
the full institutional name (its acronym is HPD), so no expansion is needed.

Funder 2 is added, at the agency level, on two independent primary sources: the software's own login
page states "Funding: NASA || Award Number: SWR2O2R 80NSSC22K0272"
(`custom_templates/login.html`, footer block), and the reference publication's Crossref funding record
is `{name: "NASA", DOI: "10.13039/100000104", award: ["80NSSC22K0272"]}`. The two funders are distinct
ROR entities in a parent chain (NASA → Goddard Space Flight Center → Heliophysics Science Division),
so this is an addition rather than a conflict, and recording both is the usual agency-plus-division
attribution. `NASA` is deliberately expanded to `National Aeronautics and Space Administration`, per
Field 25's "Avoid acronyms"; the ROR `ror_display` for `027ka1x80` is exactly that string, with `NASA`
and `NASA HQ` as acronym forms.

**Considered and rejected: Georgia State University** (`https://ror.org/03qt6ba18`, which ROR types as
a funder as well as an education institution). It is the author's affiliation and the host of the
dissertation work, and it appears in `login.html`'s footer as "Affiliation: Georgia State University"
— but as an affiliation, not a funding source. No source attributes financial support to GSU. It is
correctly recorded in Field 6 only.

---

### 26. Award Title (OPTIONAL)

- **Award Title:** `Space Weather Research-to-Operations-to-Research (SWR2O2R)`
- **Award Number:** `80NSSC22K0272`

Carried over from the existing HSSI record and confirmed exactly. Zenodo's grant record gives
`title: "Space Weather Research-to-Operations-to-Research (SWR2O2R)"` and `code: "80NSSC22K0272"`,
linking to the NSPIRES SWR2O2R solicitation abstracts document. The award number is independently
corroborated by `custom_templates/login.html` ("Award Number: SWR2O2R 80NSSC22K0272") and by the
reference publication's Crossref funding record and its stated funding statement ("NASA SWR2O2R Grant
80NSSC22K0272").

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

`https://doi.org/10.3847/1538-4365/ad3fba`

Jackson, I., & Martens, P. (2024). *Advancing Solar Energetic Particle Event Prediction through
Survival Analysis and Cloud Computing. I. Kaplan–Meier Estimation and Cox Proportional Hazards
Modeling.* The Astrophysical Journal Supplement Series, 272(2), 37.

This DOI is the one listed in `CITATION.cff` lines 22-24
under `identifiers:`, so the developer herself attached it to the software — which is exactly the
"publications the software developer prioritizes but [that] are different from the reference
publication" that Field 27 describes. Field 14 records why it is *not* the reference publication: it
is an SEP-prediction study that uses AWS and the `lifelines`/`scikit-survival` libraries, not a
description of the platform.

Substantively it belongs here too. The paper's subject matter is the science the software serves:
solar energetic particle event prediction from the same GOES-based event catalogs that
`custom_modules/dmLab.py` retrieves (Field 28), by the same author, using the same cloud approach.

Resolved via Crossref, not DataCite — the American Astronomical Society deposits with Crossref, so
`https://api.datacite.org/dois/10.3847/1538-4365/ad3fba` returns no record. A future agent seeing that
empty DataCite response should not conclude the DOI is invalid.

**Documented negative research:** no Paper II of this two-part series is indexed in Crossref or arXiv
as of 2026-08-04, though Paper I's abstract promises one. Add it here if it appears. The reference
publication `https://doi.org/10.5334/jors.519` is deliberately not duplicated into this field, since
Field 27 is for publications *other than* the reference publication.

**Also deliberately excluded: the three publications that describe the datasets in Field 28** —
`https://doi.org/10.3847/1538-4365/ac87ac` (GSEP), `https://doi.org/10.3847/1538-4365/ab9a42`
(the SOHO/EIT Flare Catalog) and `https://doi.org/10.1038/s41597-020-0548-x` (SWAN-SF). All three are
by the Georgia State University groups whose data `custom_modules/dmLab.py` retrieves, and all three
are cited by name in `DMLab.ipynb`, so each is a plausible-looking addition. None belongs here:
Field 27 covers publications that describe, cite or use *this software*, and these describe data the
software fetches. Each is recorded in its Field 28 entry instead, where a describing publication is
the field's own designated fallback. Adding one without the others would also be arbitrary. This
paper — `10.3847/1538-4365/ad3fba` — is different in kind: the developer attached it to the software
herself in `CITATION.cff`.

---

### 28. Related Datasets (OPTIONAL)

- `https://doi.org/10.7910/DVN/DZYLHK` — GSEP Dataset (Rotti, S., Aydin, B., Georgoulis, M. K., &
  Martens, P. C.; Harvard Dataverse)
- `https://doi.org/10.7910/DVN/C9H34R` — The SOHO/EIT Flare Catalog (Rotti, S., Martens, P., &
  Aydin, B.; Harvard Dataverse)
- `https://doi.org/10.7910/DVN/WSEY4T` — Flare to CME Association Integration [FL2CME] (Ji, A.,
  Aydin, B., et al.; Harvard Dataverse)
- `https://doi.org/10.7910/DVN/EBCFKM` — SWAN-SF (Angryk, R., Martens, P., Aydin, B., Kempton, D.,
  et al.; Harvard Dataverse)

All four DOIs resolve, and none of these is an inferred association: each is established either by
matching individual file names or, for SWAN-SF, by exact byte-size correspondence.

**The primary evidence is the "Available Datasets" markdown cell at the top of
`examples/AIA_DONKI_DMLab/DMLab.ipynb`.** That cell enumerates the datasets the `dmLab` module exposes,
groups them under four named catalogs, and gives a source publication link for three of the four. It
is the authoritative statement of what this software's dataset-access module is for, and the four
entries above are its four groups. `custom_modules/dmLab.py` then reads them from the public bucket
`dmlab-datasets1` (Georgia State University's Data Mining Lab); note that `get_dataset(csv_file)`
hard-codes the `.csv` suffix (`pd.read_csv(f's3://{bucket}/{csv_file}.csv')`), so a name is
retrievable through this software only if `<name>.csv` exists as an object in that bucket.

- **GSEP** — the notebook's first group, `gsep_list`, retrieved in a code cell and analysed in
  `GSEP_DMLab.ipynb` via the columns `fl_goes_class` and `ppf_gt100MeV` (GOES flare class and >100 MeV
  proton peak flux). The GSEP Dataverse record contains `GSEP_List.tab`. Described by Rotti et al.
  (2022), *Integrated Geostationary Solar Energetic Particle Events Catalog: GSEP*, ApJS,
  `https://doi.org/10.3847/1538-4365/ac87ac`, which is the link the notebook itself cites as the
  group's "Source".
- **SOHO/EIT** — the notebook's second group, `soho_eit_flares`, retrieved in a code cell. The
  Dataverse record `10.7910/DVN/C9H34R` is titled "The SOHO/EIT Flare Catalog", is authored by
  Sumanth Rotti, Petrus Martens and Berkay Aydin — the same GSU Data Mining Lab group as GSEP — and
  contains a single file, `The_SOHO_EIT_Flare_catalog.tab`. Described by Rotti, Martens & Aydin
  (2020), ApJS, `https://doi.org/10.3847/1538-4365/ab9a42`, which is the "Source" link the notebook
  gives for this group.
  This entry is easy to lose. `soho_eit_flares` appears in a bare `get_dataset` call with nothing
  around it to identify what it is, so anyone working from `DMLab.ipynb`'s **code** cells alone will
  find no way to attach it to a published dataset and will conclude, wrongly, that it has no DOI. The
  identification lives entirely in the notebook's **markdown**, and it meets exactly the same
  evidentiary bar as GSEP and FL2CME. **Anyone re-deriving Field 28 must read the notebook's markdown
  cells, not just its code.**
- **FL2CME** — the notebook's third group, "Flare to CME Catalogs", and the only one for which the
  notebook gives no source link; it was identified by file-name correspondence instead. Seven of its
  eight names match files in the FL2CME Dataverse record: `cdaw_cactus_lz_halo_integrated`,
  `cdaw_cactus_lz_nonhalo_integrated`, `cdaw_cactus_qkl_halo_integrated`,
  `cdaw_cactus_qkl_nonhalo_integrated` (all `.csv` there), `fl2cme_soho` (`fl2cme_soho.tab`),
  `sdo_goes_flares` (`sdo_goes_flares.tab`) and `soho_goes_flares` (`soho_goes_flares.csv`);
  `fl2cme_sdo` corresponds to `fl2cme_sdo_vconf.tab`. The Dataverse title is "Flare to CME Association
  Integration", authored by Anli Ji and Berkay Aydin of Georgia State University — the same group as
  the S3 bucket, and Aydin is a co-author of the reference publication.
- **SWAN-SF** — the notebook's fourth group (`goes_flares_integrated`, `Hinode_all`, `ssw_hpc`),
  sourced by the notebook to Angryk et al. (2020), *Multivariate time series dataset for space weather
  data analytics*, Scientific Data, `https://doi.org/10.1038/s41597-020-0548-x`. This group needed
  more work than the others, because these three names are documented in the markdown cell but are
  **never invoked in any code cell**, and because the SWAN-SF Dataverse record's top-level file list
  (`partition1-5_instances.tar.gz`, `SWAN.tar.gz`, `addenda.tar.gz`) shows no matching names — a
  Dataverse-wide search for each of the three returns nothing. The mapping is nevertheless **proven**,
  by looking inside `addenda.tar.gz`, whose members include:

  | Member of `addenda.tar.gz` | Size | Bucket object |
  |---|---|---|
  | `integrated_flare_data/goes_flares_integrated.csv` | 5,221,350 bytes | `goes_flares_integrated.csv`, 5,221,350 bytes |
  | `base_flare_data/ssw_hpc.csv` | 2,492,736 bytes | `ssw_hpc.csv`, 2,492,736 bytes |
  | `base_flare_data/Hinode_all_fromXRT.csv` | 1,844,279 bytes | *(absent — see below)* |

  Two of the three names correspond to SWAN-SF addenda files **byte-for-byte in size**, and both
  objects are retrievable from the bucket. The DMLab bucket republishes SWAN-SF's addenda tables under
  shortened names, so `10.7910/DVN/EBCFKM` is the correct dataset DOI and is recorded above in
  preference to the notebook's publication link, consistent with the other three entries.

**Documented upstream gap: `Hinode_all` is advertised but not retrievable.** The notebook lists it,
but no `Hinode_all.csv` object exists in the bucket, so `get_dataset('Hinode_all')` cannot succeed as
written. The corresponding SWAN-SF addenda file is named `Hinode_all_fromXRT.csv`, so the shortened
bucket name was most likely never uploaded. This is an upstream defect in Helio-Lite's example
notebook, not a metadata error, and it does not affect the SWAN-SF entry, which is carried by the
other two files. A related and harmless upstream inconsistency: the markdown cell names the SOHO/EIT
dataset `soho_eit_flare` (singular) while the code cell correctly calls `soho_eit_flares` (plural),
and only the plural object exists.

**Why the four describing publications are recorded here rather than in Field 27.** Each entry above
names the publication that describes its dataset — `10.3847/1538-4365/ac87ac` (GSEP),
`10.3847/1538-4365/ab9a42` (SOHO/EIT) and `10.1038/s41597-020-0548-x` (SWAN-SF) — and **none of them
is added to Related Publications.** Field 28's own instruction treats a describing publication as the
*fallback* when no dataset DOI exists, and all three datasets have one, so the dataset DOI is the
better value in every case. Field 27, by contrast, is for publications that describe, cite or use
*this software*, which none of these do — they describe data the software happens to fetch. Applying
this consistently matters: adding any one of the three while omitting the others would be arbitrary.
The rule for a future agent is therefore explicit — **a dataset's describing publication belongs in
this field's note, not in Field 27.**

---

### 29. Related Software (OPTIONAL)

- `https://github.com/heliocloud-data` — **HelioCloud**
- `https://github.com/jupyterhub/the-littlest-jupyterhub` — **The Littlest JupyterHub (TLJH)**
- `https://github.com/heliophysicsPy/pyhc-docker-environment` — **PyHC Docker Environment**

These three are the predecessor and the two upstream projects Helio-Lite is assembled from — the
entries that actually tell a reader what this software is.

- **HelioCloud** is the project Helio-Lite is derived from, and Field 29 explicitly asks for "software
  this work was forked from". It is asserted in the software's own name (Field 7,
  "A Lightweight Version of HelioCloud"), in the abstract ("Derived from HelioCloud"), and in the
  Author Note ("developed as a lightweight, single-instance counterpart to HelioCloud
  (https://github.com/heliocloud-data)"). The URL recorded is the one the author herself cited: the
  GitHub organisation. That choice is deliberate, because the repository level is ambiguous and
  moving. `heliocloud-data/platform` (the current "Core platform codebase", MIT) was created
  2026-02-03, i.e. *after* Helio-Lite was derived, while `heliocloud-data/platform-legacy` (created
  2023-08-22, also "Core platform codebase", MIT) is the codebase that existed in 2024. Citing either
  as "what this was derived from" would be misleading; the organisation URL is stable across that
  reorganisation and is what the primary source says. **No HelioCloud software DOI exists** — a Zenodo
  search returns only HelioCloud presentations and posters (for example
  `10.5281/zenodo.13887203`, "HelioCloud as a replicable open science architecture"), none of which is
  the software.
- **The Littlest JupyterHub** is vendored, not merely depended on. `START_HERE/jupyterHubBootstrap.py`
  is a copy of TLJH's own `bootstrap/bootstrap.py`: 515 lines against upstream's 517, differing in
  only **38 lines (20 removed, 18 added) across 9 hunks**. Most of that is the vendored copy lagging
  upstream on version thresholds — four hunks are the Ubuntu 20.04→22.04 and Python 3.8→3.9 bumps
  and their docstring/comment restatements, and one is a blank line. But **not all of it is version
  drift**: one hunk replaces the systemd detection with a more tolerant form ("some distros ship
  systemctl without a top-level systemd binary"), and a three-hunk block around upstream lines
  445–459 restructures the `software-properties-common` install — upstream moved it out of the
  Ubuntu-only branch and added commentary about skipping it and the "universe" section on Debian, as
  part of broadening Debian-family support. Those are upstream behavioural changes the vendored copy
  predates, not textual drift.

  Beyond the vendored file, the README's EC2 user-data block configures the installed hub with
  `tljh-config`, and both kernels are installed into TLJH's `/opt/tljh/user/envs/` prefix. Helio-Lite
  is a heliophysics-specialised TLJH deployment, and it cannot be described accurately without naming
  TLJH.

  TLJH is general-purpose infrastructure, so it sits close to the generic-tooling exclusion that
  Field 29 shares with Field 30, and the reason it clears that bar is worth stating precisely: the
  claim being made is specific and verifiable from this repository alone — a file-level copy of
  TLJH's own installer, demonstrable by diff — rather than the content-free "depends on a common
  library" the exclusion exists to block. What deliberately does **not** support it is any suggestion
  that vendoring TLJH is rare across HSSI's catalogue. No value in this file rests on a claim about
  what other records do or do not contain, because such a claim is not checkable from here and can
  change without notice.
- **PyHC Docker Environment** supplies the entire heliophysics kernel.
  `START_HERE/create_directories.sh` line 4 clones
  `https://github.com/heliophysicsPy/pyhc-docker-environment.git` into `/usr/lib/` and moves
  `docker/pyhc-environment/contents/cdf38_0-dist` (the NASA CDF library) into place — a hard runtime
  dependency, not a reference. Beyond that, `libraries_dependencies/requirements.txt` is visibly
  derived from that project: it retains its build-order marker comments verbatim, including
  `# kamodo==23.3.0  # gets installed from GitHub instead`,
  `# numpy>=1.23.0,<1.27,!=1.15.0  # gets installed first in the Dockerfile` and
  `# pyspedas==1.5.1  # gets installed last in the Dockerfile` — comments that only make sense in a
  Dockerfile-based pipeline Helio-Lite does not use. This is a domain-specific upstream that
  characterises the software.

**Considered and rejected: the roughly 250 packages pinned in `requirements.txt`.** Being present in a
bundled environment specification is not a relationship this field records; if it were, this record
would list most of the heliophysics Python ecosystem and say nothing. The four packages with
individually documented integration are recorded in Field 30 instead. Also considered and rejected:
**CloudCatalog** (`https://github.com/heliocloud-data/cloudcatalog`), which is appealing because it is
a PyHC package from the HelioCloud project — but it is not installed, imported or referenced anywhere
in Helio-Lite, so the only link is a shared parent organisation.

---

### 30. Interoperable Software (OPTIONAL)

- `https://github.com/sunpy/sunpy` — **SunPy**
- `https://github.com/spacepy/spacepy` — **SpacePy**
- `https://github.com/spedas/pyspedas` — **PySPEDAS**
- `https://github.com/MAVENSDC/PyTplot` — **PyTplot**

Repository URLs are used rather than DOIs, which Field 30 permits explicitly.

**The operative standard, stated up front because this software is an unusual case for this field.**
Helio-Lite is not a library that hands objects to other libraries — it is a **deployed environment
product** whose deliverable is a curated, working heliophysics analysis platform. Field 30 is read
here at the level of that product: the entries are the peer domain tools whose **demonstrated data
exchanges the platform exists to make work**, evidenced inside Helio-Lite's own shipped examples.
What follows is the exchange evidence, which is the load-bearing part.

1. **PySPEDAS and PyTplot exchange tplot variables** — the `hssi-field-definitions` skill's own
   worked example of a valid Field 30 pair. `examples/PyHC/pyspedas_demo.ipynb` demonstrates exactly
   that exchange in the shipped environment: `pyspedas.themis.fgm(...)` and `pyspedas.mms.fgm(...)`
   create tplot variables that are then read, rewritten and displayed through PyTplot —
   `get_data("thd_fgs_gse")`, `store_data("new_thd_fgs_gse", {'x': time, 'y': data})`,
   `pytplot.options(...)`, `tplot([...])` — and `clean_spikes()` produces new `-despike` variables
   consumed the same way.
2. **SpacePy, astropy and SunPy exchange a coordinate object** — `examples/PyHC/coordinate_systems.ipynb`
   carries one `spacepy.coordinates.Coords` object across all three data models and back:
   `Coords([...], 'GEO', 'car')`, `.convert('SM','car')`, `.to_skycoord()` into an astropy `SkyCoord`,
   `.transform_to(frames.HeliographicCarrington(observer="earth"))` into a SunPy frame, then
   `'itrs'`, then `Coords.from_skycoord(...)` back into SpacePy with its `Ticktock` time axis intact.
   That is a documented, round-tripping conversion between peer domain tools, not co-residence.
3. **The reference publication names them as the platform's related software.** The JORS paper's
   Related Software and Dependencies section lists SunPy, HelioPy, PyHC packages, PyTplot and
   PySPEDAS.

**The astropy exclusion, reconciled explicitly so it is not re-litigated.** Under the standard above,
astropy is excluded not because it is absent from the exchange but because of the *role* it plays in
it. In citation 2 astropy is the **substrate through which** the SpacePy-to-SunPy conversion is
mediated — the common `SkyCoord`/units representation both peers convert into — rather than a peer
participant a user would deliberately combine with this platform as an analysis tool in its own
right. Recording SunPy and SpacePy while excluding astropy is therefore a distinction of role, not an
inconsistency: the exchange runs *between* the two peers, *via* astropy.

**The exclusion rests on that role argument alone, and two tempting supports for it are both wrong.**
The first is that astropy is "present only as a transitive dependency of sunpy" — it is not.
`libraries_dependencies/requirements.txt:24` pins `astropy>=5.3,!=5.1.0` directly, alongside
`asdf-astropy` and `astropy-iers-data`; astropy is a first-class pin in this environment and is
excluded despite that. The second is that the exchange in citation 2 runs "between astropy and
spacepy/sunpy, not between astropy and anything Helio-Lite provides" — that formulation collapses,
because applied evenly it would exclude SunPy and SpacePy as well, on identical grounds. Neither
argument should be reintroduced; role is the whole of it.

**Two framings deliberately abandoned, because they are close to what Field 30 forbids.** Earlier
drafts leaned on (a) Helio-Lite's own modules being copied into the same site-packages directory as
these four packages (`/opt/tljh/user/envs/pyhc-all/lib/python3.9`, README Step 4) and (b) each
package being installed or given a shared data directory individually rather than swept in by a
requirements file (`pip install --no-build-isolation spacepy`, `pytplot==1.7.28`, `pyspedas` by name;
`create_directories.sh` creating `/shared/.sunpy` and `/shared/.spacepy/data`). Both are factually
true and are retained here as context about how the platform is assembled — but both amount to
*co-residence in one interpreter*, which the field rules explicitly reject ("merely sharing a Python
runtime satisfies nothing"). They must not be used as the justification for these entries. The
exchange evidence in 1-2 is what carries them.

**Considered and rejected: numpy, pandas, matplotlib, seaborn, requests, boto3, s3fs, fsspec,
pyarrow, Pillow, ipywidgets, beautifulsoup4, pytz, torch** (i.e. all of
`libraries_dependencies/custom_requirements.txt`), and the roughly 250 further pins in
`requirements.txt`. These are dependencies and generic infrastructure; being importable alongside
something is not interoperating with it. `pandas`, `boto3` and `s3fs` are genuinely central to
`dmLab.py`, and `ipywidgets`, `Pillow` and `beautifulsoup4` to `aiaImages.py`, but a statement of that
form would read identically for a web application or a finance model and therefore says nothing about
this software.

**Considered and rejected — HelioPy and GeospaceLAB.** Both are closer calls than the packages above,
because both carry provisioning evidence of the same kind the platform gives SpacePy:
`create_directories.sh` creates `/shared/heliopy/data` and `/shared/Geospacelab/Data`, and both are
pinned (`heliopy==0.15.4`, `geospacelab==0.6.1`). They are excluded because provisioning is not the
standard this field applies — neither package appears in any shipped example, so there is no
demonstrated exchange to point at — and because HelioPy is retired upstream, which makes an assertion
of live interoperability with it misleading. The evidence is set out here so the same two packages are
not proposed again as though it had been missed.

**Rejected justifications, recorded so they are not re-used here:** "Helio-Lite bundles the PyHC
package set, so it interoperates with PyHC packages" and "part of the standard scientific Python
ecosystem". Field 30 rules both out explicitly, and the first would license listing every package in
`requirements.txt`.

**Each entry is a bare code-repository URL, which is what this field asks for**, and each URL is the
canonical one for its project. Nothing here depends on those projects being described anywhere else —
what identifies an entry is the URL, so the only thing that has to be right is that the URL is the
project's canonical address.

**PyTplot's URL must keep its capitalisation: `MAVENSDC/PyTplot`, not `MAVENSDC/pytplot`.**
`MAVENSDC/PyTplot` is GitHub's own canonical name for the repository; the all-lower-case spelling is
only a redirect alias, which is why both resolve in a browser and why the lower-case form looks like
a harmless tidy-up. It is not — two spellings of one repository are two different strings, and only
the canonical one reliably lines up with how the same project is referenced elsewhere. The same care
applies to every URL in Fields 27-30: copy the canonical casing from the source, and do not normalise
a URL's case on the assumption that the web treats it as insignificant.

---

### 31. Related Instruments (OPTIONAL)

- **Instrument Name:** `Atmospheric Imaging Assembly`
  **Instrument Identifier:** `https://spase-metadata.org/SMWG/Instrument/SDO/AIA`
- **Instrument Name:** `HMI`
  **Instrument Identifier:** `https://spase-metadata.org/SMWG/Instrument/SDO/HMI`

Each name is the SPASE record's own name for the instrument, reproduced verbatim, and each is paired
with that record's SPASE identifier.
**Relevance.** Both pass the "designed to support" test decisively — these are not incidental
mentions. `custom_modules/aiaImages.py` exists solely to retrieve AIA imagery
(`fetch_aia_images(year, month, day, wavelength)` building
`http://jsoc.stanford.edu/data/aia/images/{YYYY}/{MM}/{DD}/{wavelength}/`, selecting `.jp2` files,
converting them to PNG under `aia_images/`), and `custom_modules/hmiImages.py` does the same for HMI
(`fetch_hmi_images()`, `http://jsoc.stanford.edu/data/hmi/images/{YYYY}/{MM}/{DD}/`, `.jpg` files,
`hmi_images/`). Instrument-specific data retrieval from the mission's own science operations center is
the designed-to-support case. Both are named as headline features in the README's Key Features list
and in the abstract, and `custom_modules/README.md` says the modules handle data "from various sources
like the Solar Dynamics Observatory (SDO)". A user searching HSSI for `instrument:"AIA"` should find
this software.

**Two SPASE traps, both easy to fall into.**

- **"AIA" is not unique in SPASE, and one of the look-alikes is not even a solar instrument.**
  SPASE carries this SDO instrument twice, once as
  `https://spase-metadata.org/SMWG/Instrument/SDO/AIA` and once in `.html` form
  (`Atmospheric Imaging Assembly (AIA)`, `.../SDO/AIA.html`); these are one resource, and the bare
  identifier is the one to use. Separately, the abbreviation `AIA` also belongs to a different
  observatory network entirely — `Magnetometers at Argentine Island`
  (`https://spase-metadata.org/IUGONET/Instrument/WDC_Kyoto/WDC/AIA/Magnetometer`) and its parent
  `Argentine Island Geomagnetic Observatory`
  (`https://spase-metadata.org/IUGONET/Observatory/WDC_Kyoto/WDC/AIA`), noted here so the IUGONET
  family is recognisable at a glance. Neither is a candidate: the repository's own expansion of the
  acronym ("Atmospheric Imaging Assembly", README Key Features) together with the JSOC `/data/aia/`
  path settle which instrument is meant.
- **`HMI` is the SPASE record's own name; "Helioseismic and Magnetic Imager" is not.** SPASE names
  `https://spase-metadata.org/SMWG/Instrument/SDO/HMI` with the bare three-letter string. The
  expanded form is what the repository, the README and the abstract all use, so it is what a future
  agent will be inclined to write here — but it is not what SPASE calls the instrument, and searching
  SPASE for "helioseismic" leads somewhere else entirely: to ESA Solar Orbiter's *Polarimetric and
  Helioseismic Imager* (PHI, `https://spase-metadata.org/ESA/Instrument/SolarOrbiter/PHI`), a
  different instrument on a different spacecraft. Record `HMI`.

---

### 32. Related Observatories (OPTIONAL)

- **Observatory Name:** `Solar Dynamics Observatory`
  **Observatory Identifier:** `https://spase-metadata.org/SMWG/Observatory/SDO`

`Solar Dynamics Observatory` is the SPASE record's own name for the mission, reproduced verbatim
with its SPASE identifier. Both instruments in Field 31 fly on SDO, and the software retrieves their products from SDO's own
science operations center. `custom_modules/README.md` states the modules fetch data "from various
sources like the Solar Dynamics Observatory (SDO)". This is the mission-level counterpart of the
`Observatory/Mission-specific` selection in Field 17, which Field 17 explicitly directs be
cross-listed here.

**Considered and rejected — GOES and SOHO.** These are the most likely future additions, so the
reasoning is recorded. Several of the DMLab catalogs retrieved by `dmLab.py` and enumerated in
`DMLab.ipynb` carry those mission names: `soho_eit_flares`, `soho_goes_flares`, `sdo_goes_flares`,
`fl2cme_soho`, and the four `cdaw_cactus_*` tables (derived from SOHO/LASCO CME catalogs). They are
rejected because what the software retrieves are *derived event catalogs* published on Harvard
Dataverse (Field 28), not GOES or SOHO data products, and because `dmLab.get_dataset(csv_file)` is a
mission-agnostic one-line CSV reader against a bucket — it implements nothing specific to either
mission's data, formats or conventions. A user working with GOES X-ray data or SOHO/LASCO images would
not reach for Helio-Lite. Contrast SDO, where two dedicated modules implement mission-specific
retrieval as a headline feature.

**Considered and rejected — THEMIS, MMS and MAVEN.** `examples/PyHC/pyspedas_demo.ipynb` loads
THEMIS-D FGM and MMS-1 burst-mode FGM data, and `pytplot_demo.ipynb` restores a MAVEN SWIA/SEP/MAG
test file. All three are tutorial demonstrations of bundled third-party packages — exactly the
"tutorial/demo name-drop" the relevance gate excludes — and all three would be equally present in any
environment that installs PySPEDAS and PyTplot. See the scope note.

**Considered and rejected — DONKI.** `donkiData.py` queries
`https://kauai.ccmc.gsfc.nasa.gov/DONKI/WS/get/` as a first-class feature, but DONKI is NASA CCMC's
multi-mission space-weather event notification database, not an observatory or mission. It is recorded
in Field 17 Data Sources (as `Other`) and its event types in Field 22, which is where it belongs.

---

### 33. Logo (OPTIONAL)
Not found.

**Helio-Lite has no logo, and this field is correctly empty.** That is a finding, not a gap. Four
independent places a logo would live were checked, and all four are negative:

1. **The repository contains no image assets at all.** Its 40 tracked files were enumerated: not one
   carries a `.png`, `.jpg`, `.jpeg`, `.svg`, `.ico`, `.gif` or `.webp` extension, and there is no
   `docs/` or `assets/` directory.
2. **`custom_templates/login.html` has no logo.** Its only `<img>` tags are a 16x16 ORCID icon (`https://orcid.org/sites/default/files/images/orcid_16x16.png`), a 16x16 GitHub
   Mark (`https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png`) and a 16x16
   envelope emoji, all in the author-credit footer. Its visual identity is a full-screen background
   video (`https://www.fitsflow.org/daily_videos/20250808_stitched.mp4`, with an inline script
   rewriting the source to a dated object under
   `https://helioconvert-sdo.s3.us-east-1.amazonaws.com/daily_videos/`) — a rotating daily video, not a
   logo, and not a stable image URL of the kind Field 33 requires.
3. **The README's images are not a logo.** They are a Zenodo DOI badge SVG
   (`https://zenodo.org/badge/DOI/10.5281/zenodo.17611741.svg`), a YouTube video thumbnail
   (`https://img.youtube.com/vi/318Z1h9paMU/0.jpg`) and four screenshots hosted as GitHub
   user-attachments.
4. **SoMEF returned no `logo` field** for this repository, and Helio-Lite is not a registered PyHC
   package, so there is no curated PyHC logo entry either (see the note below).

Field 33 requires a logo "stored online in a permanent place and made publicly accessible". Nothing
here meets that. Guessing a value — the YouTube thumbnail, a screenshot, the DOI badge — would be
worse than leaving it empty.

---

## PyHC registry status

**Helio-Lite is not a registered PyHC package.** It appears in none of the three PyHC registry files —
`projects_core.yml`, `projects.yml` (community) and `projects_unevaluated.yml` — under any name, and
no entry's `code` field points at `indiajacksonphd/Helio-Lite`. No curated PyHC metadata — logo, docs
URL, keywords, maturity ratings — is therefore available to supplement this record, which is why
several fields above rest on repository evidence alone.

This is not a defect: absence from the PyHC registry says nothing about software quality, and
Helio-Lite is a deployment framework rather than an importable Python package, which is what the
registry catalogues. It is recorded so a future refresh does not repeat the search expecting a hit.
Note the nearest neighbours that *are* registered and may cause confusion: `CloudCatalog`
(`heliocloud-data/cloudcatalog`, with `logo: https://heliocloud.org/static/img/logo.jpg`) is a
different package from the HelioCloud organisation, and `aiapy` (`LM-SAL/aiapy`) is the PyHC package
for SDO/AIA analysis — neither is this software.
