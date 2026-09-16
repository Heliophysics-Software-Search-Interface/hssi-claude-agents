# HSSI Metadata Extraction Results

**HSSI Software ID:** Not applicable — new submission, not yet in HSSI
**Repository:** https://github.com/SwRI-IDEA-Lab/surya_workshop
**Source Revision:** 608be463a4673bcdf97f8e73fa74099ac1c7d0c7
**Extraction Date:** 2026-09-16
**Validation Date:** 2026-09-16
**Validation Status:** PASS

---

**Scope note — which repository this describes.** `SwRI-IDEA-Lab/surya_workshop` is the upstream
original (GitHub `fork: false`, created 2025-12-23). `amunozj/surya_workshop` is a personal fork
(`fork: true`, `parent`/`source` both `SwRI-IDEA-Lab/surya_workshop`, created 2026-09-11, 0 stars,
0 forks) and is **not** the appropriate HSSI subject: the upstream carries the entire 202-commit
history, all 27 downstream forks, and the workshop participants' branches.

**Scope note — vendored code.** The 366M-parameter Surya backbone
(`workshop_infrastructure/models/helio_spectformer.py`, `spectformer.py`, `transformer_ls.py`,
`embedding.py`, `flow.py`) is a *vendored copy* of upstream `NASA-IMPACT/Surya`, not original work
of this repository. The repository began with Surya as a git submodule (commit `558d601`, "Add
Surya submodule") and later copied it in so the repo runs standalone. Functionality below is
recorded for the software as distributed — a user installing this repository does obtain the
backbone — but attribution for the backbone's design belongs upstream, which is why
`NASA-IMPACT/Surya` is recorded in Field 29 and the Surya paper in Field 27.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Source: placeholder. HSSI requires a real submitter identity at submission time; it is not a
property of the software and cannot be derived from the repository.*

### 2. Persistent Identifier (RECOMMENDED)
Not found

*No DOI exists for this software. Negative research, so a future refresh need not repeat it:*
- *No `CITATION.cff`, `codemeta.json`, `.zenodo.json`, or `zenodo.json` exists at any revision of
  the repository; no DOI badge or `doi.org` string appears in `README.md` or anywhere in the
  tracked tree.*
- *Zenodo returns 0 hits for the free-text query `surya_workshop`.*
- *A creator-keyed Zenodo query (`metadata.creators.person_or_org.name:"Muñoz-Jaramillo, Andrés"`)
  returns 6 records — Generative_Interrogator, MEMPSEP codebase, an SDO cloud-computing
  presentation, DeepEM, SuNeRFs, and the SuryaBench SDO Dataset — none of which is this software.
  A creator-keyed search is used deliberately because a manually deposited Zenodo record need not
  contain the repository slug anywhere in its metadata, so a slug search alone would be a false
  negative.*
- *A title query for `surya` returns 137 unrelated records (Hindu-deity artifacts, Indonesian
  engineering papers, taxonomic species names). In particular `10.5281/zenodo.20244280`, titled
  simply "Surya", is a Scan-the-World 3D scan of a statue of the Hindu sun god and must not be
  mistaken for this software or for the Surya model.*
- *The repository has no GitHub releases and no git tags, so there is no GitHub–Zenodo release
  trigger that could have minted one.*

### 3. Code Repository (MANDATORY)
https://github.com/SwRI-IDEA-Lab/surya_workshop

*Source: the repository's own `origin` remote at the pinned revision, confirmed against the GitHub
API (`full_name: SwRI-IDEA-Lab/surya_workshop`, `fork: false`). See the scope note above for why
the upstream rather than the `amunozj` fork is the subject.*

### 4. Software Functionality (RECOMMENDED)
- Data Processing and Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: ML/AI
- Models and Simulations
- Models and Simulations: ML/AI
- Models and Simulations: Forecasting

*Every value above was confirmed to exist as a live `FunctionCategory` row on
`https://hssi.hsdcloud.org` before being recorded, and each subcategory is accompanied by its
parent because HSSI does not add parents implicitly.*

**Evidence for each selection.**

- **Data Access and Retrieval** — `HelioNetCDFDataset` (`workshop_infrastructure/datasets/helio.py`)
  loads SDO NetCDF timesteps transparently from local disk or S3, with three selectable access
  modes (`download`, `simplecache`, `stream`) dispatched through `_load_s3_nc_data` and validated
  by `VALID_S3_MODES`. `workshop_infrastructure/assets.py` fetches the normalization scalers and
  the pretrained backbone from HuggingFace on demand via `ensure_assets()`.
  `workshop_infrastructure/benchmark_s3.py` (591 lines) is a standalone CLI that measures S3
  download throughput across a (concurrency, part-size) grid and recommends transfer settings.
- **Processing** — the signum-log normalization pipeline: forward `transform()` (pure NumPy, safe in
  DataLoader workers), inverse `fast_inverse_transform()` (Numba `@njit(parallel=True)`), and
  `inverse_transform_single_channel()`. `transformations.py` supplies `MinMaxScaler`,
  `StandardScaler` (with `signum_log_transform` / `inverse_signum_log_transform`) and `MaskUnits2D`.
  The dataset also performs temporal frame sampling and validity filtering.
- **Data Reduction** — `transform_data()` applies
  `skimage.measure.block_reduce(data, block_size=(1, self.pooling, self.pooling), func=np.mean)`,
  a genuine spatial mean-pooling downsample of the 4096×4096 frames (the docstring notes the
  result is `(C, H//pooling, W//pooling)` and that pooling is not invertible).
  `workshop_infrastructure/data/split_csv_index.py` (448 lines) reduces a full timestep index to
  train/validation/test splits by day-of-year windows with year exclusions and padding windows, and
  `max_samples` caps dataset length.
- **Image Processing** — the operations above act on full-disk solar imagery per channel: spatial
  mean pooling, random vertical flips (`np.flip(sample["ts"], axis=-2)`), `RandomChannelMaskerTransform`
  (randomly zeroing input channels for robustness to missing observations), and inversion back to
  physical units (DN for AIA, Gauss for HMI, m/s for Doppler).
- **ML/AI under Data Processing and Analysis** — `apply_peft_lora()`, `discover_head_modules()` and
  `load_pretrained_weights()` in `workshop_infrastructure/utils.py`; `FlareLightningModule`; the
  `FlareMetrics` four-mode metric structure (MSE loss, RRSE via `torchmetrics`); the production
  training script with DDP, checkpointing and WandB logging.
- **Models and Simulations / ML/AI** — the repository distributes the full `HelioSpectFormer`
  backbone (2 spectral-gating blocks + 8 long-short attention blocks, patch size 16, embed_dim
  1280, 13 input channels at 4096×4096) plus the `HelioSpectformer1D` / `HelioSpectformer2D`
  fine-tuning wrappers, a `ClassToken` head component, and five head-pooling strategies.
- **Forecasting** — the template task is causal prediction: `job_id: solar_flare_forecasting` in
  `config_script.yaml`, with `ds_match_direction: forward` documented there as
  `"forward": use solar state *before* the flare (causal)`. The model regresses peak GOES X-ray
  flux from the prior solar state.

**Considered and rejected — recorded so a future agent does not re-propose them.**

- *Servers and Environments: High Performance Computing* — the multi-GPU capability comes entirely
  from Lightning's own `strategy="auto"` / `devices="auto"` in `build_trainer()`. The repository
  contributes no MPI code, no scheduler submission scripts, and no parallel-computing
  implementation of its own.
- *Servers and Environments: Software or Environment Container* — `environment.yml` is a conda
  environment specification, not a container image. There is no Dockerfile, no Singularity or Apptainer
  definition, and no container registry reference anywhere in the tree.
- *Servers and Environments: Infrastructure as Code* — the three
  `workshop_infrastructure/setup_scripts/AWS_Workshop_*.sh` scripts install Anaconda, git, and the
  conda environment onto an *already-provisioned* EC2 host. They declare no infrastructure (no
  Terraform, CloudFormation, Ansible, or Kubernetes manifests), so they are host configuration, not
  infrastructure as code.
- *Data Processing and Analysis: Time Series Analysis* — `FlareDSDataset` aligns the flare catalog
  to the Surya timestep index with `pd.merge_asof` plus a tolerance and a merge direction. That is
  time-indexed joining of labels to samples, not analysis of a time series; nothing computes
  trends, autocorrelation, or temporal filtering.
- *Data Processing and Analysis: File Format Conversion* — `create_csv_index.py` matches NetCDF
  *filenames* against the regex `(\d{8})_(\d{4})\.nc` to build a timestep index; it never opens the
  files or converts their contents. No format is translated into another anywhere in the repository.
- *Data Processing and Analysis: Analysis* — no derived physical quantity is computed from the data.
  The MSE and RRSE in `FlareMetrics` are model-evaluation metrics, not scientific analysis.
- *Coordinate Transforms* (and its `Solar` subcategory) — the only coordinate-adjacent call is
  `sunpy.coordinates.ephemeris.get_earth(ts).lat.value`, used under the optional
  `use_latitude_in_learned_flow` flag to supply the Earth's heliographic latitude as a scalar model
  input. No coordinate-system conversion is offered to users.
- *Mission-related* (any subcategory) — this is a community fine-tuning template, not part of any
  SDO ground system, pipeline, or operations chain.
- *Data Visualization*, and with it both candidate subcategories *2D Graphics* and *ML/AI* — the
  repository exports no visualization capability. The only plotting anywhere in the tree is a
  single 4×4 `ax.imshow` grid in one cell of one template notebook
  (`downstream_apps/template/0_dataset_dataloader_template.ipynb`), and `matplotlib` appears in
  `environment.yml` solely to support it. The supporting negative evidence, recorded so this does
  not have to be re-derived: no `.py` file anywhere in the repository references `matplotlib`,
  `imshow`, or `plt.`; the other three notebooks (`1_baseline_template`, `2_finetune_template_1D`,
  `A_shapes_and_broadcasting`) contain no plotting at all; and there is no non-matplotlib rendering
  path — no `wandb.Image` or `wandb.Video`, no PIL, no `IPython.display`, no TensorBoard
  `add_image`, and no figure saving. *2D Graphics* therefore fails for want of a user-facing
  capability: a single runnable step inside a teaching notebook is not a capability the software
  offers, and a user filtering HSSI for visualization software would not be served by this result.
  *ML/AI* fails on the additional ground that no model output or training diagnostic is plotted at
  all — WandB is used for scalar metric logging only.
- *Models and Simulations: Data Guided* — the backbone is a data-trained neural network, already
  captured by `Models and Simulations: ML/AI`. In heliophysics "data guided" conventionally denotes
  a physics model driven by observational boundary conditions, which this is not.

### 5. Related Region (RECOMMENDED)
- Photosphere
- Chromosphere
- Corona
- Solar Environment

*The selection follows directly from the 13 input channels declared in
`downstream_apps/template/configs/config_script.yaml`:*
`channels: [aia94, aia131, aia171, aia193, aia211, aia304, aia335, aia1600, hmi_m, hmi_bx, hmi_by, hmi_bz, hmi_v]`

- **Photosphere** — the five HMI products (line-of-sight magnetogram, the three vector-field
  components, and Doppler velocity) are photospheric measurements. `inverse_transform_data()`
  returns them in Gauss and m/s.
- **Chromosphere** — AIA 304 Å (He II) images the chromosphere and transition region; AIA 1600 Å
  images the upper photosphere and transition region.
- **Corona** — AIA 94, 131, 171, 193, 211 and 335 Å are the coronal EUV passbands.
- **Solar Environment** — recorded deliberately in addition to the three specific regions. HSSI's
  Region vocabulary is flat: a fine-grained value does not imply its coarse counterpart, so a user
  browsing the broad solar category would not otherwise find software that spans the entire
  SDO-observable solar atmosphere.

*Rejected: every non-solar region. The software reads no Earth, magnetospheric, heliospheric, solar
wind, or planetary data of any kind. The README notes that the upstream Surya model demonstrated
solar wind speed prediction, but that is an upstream result for a different downstream task and is
not something this repository implements, so `Solar Wind` would misrepresent it.*

### 6. Authors (MANDATORY)

**Author 1**
- **Name:** Andrés Muñoz-Jaramillo
- **Author Identifier:** https://orcid.org/0000-0002-4716-0840
- **Affiliation:**
  - **Organization:** Southwest Research Institute
  - **Affiliation Identifier:** https://ror.org/03tghng59

*Sole authorship, established three ways. (a) Every one of the 202 commits reachable from the
pinned revision is authored by one person under four `name <email>` spellings —
`Andres Munoz-Jaramillo <andres.munoz@swri.org>` (93), `Andrés Muñoz-Jaramillo
<andres.munoz@swri.org>` (84), `Andres Muñoz-Jaramillo <amunozj@users.noreply.github.com>` (18),
and `Quiet-Sun <amunoz.physics@gmail.com>` (7). (b) The GitHub contributors API returns exactly one
contributor, `amunozj`, with 202 contributions — matching the commit count exactly, which is what
establishes that the fourth spelling is the same person rather than a collaborator: fetching one of
the `amunoz.physics@gmail.com` commits through the commits API returns `author.login: amunozj`,
so GitHub has that personal address linked to the same account. This matters because the GitHub
user `quiet-sun` is an unrelated account belonging to a different person, and matching on the
display name alone would have credited the wrong individual. (c) Notebooks 0, 1, 2 and
`A_shapes_and_broadcasting.ipynb` each carry a "by Andrés Muñoz-Jaramillo" byline in their opening
markdown cell.*

*Name form: the accented "Andrés Muñoz-Jaramillo" is recorded because it is the form the author uses
in his own notebook bylines, in his ORCID record, and in the author list of arXiv:2508.14112. The
unaccented git spellings are an artifact of commit configuration.*

*ORCID resolution: a bare-name ORCID search is unreliable in both directions here — `given-names:Andres
AND family-name:Munoz-Jaramillo` returns 136 results containing no match, while `family-name:Muñoz-Jaramillo`
unquoted returns 36,695. The quoted fielded query `family-name:"Muñoz-Jaramillo"` narrows to 16
results, exactly one of which is a heliophysicist: `0000-0002-4716-0840`, given names "Andrés",
with institution history Georgia State University, Harvard-Smithsonian Center for Astrophysics,
Montana State University Bozeman, Southwest Research Institute Boulder, and Universidad de los
Andes. That trajectory matches the published record of the Surya co-author, and the `swri.org`
commit address independently corroborates the current employer.*

*Affiliation: the ORCID employments record lists "Southwest Research Institute Boulder"
(Boulder, CO, US; role "Lead Research Scientist"; start 2017-03; no end date) as the current
position. The ROR-registered legal entity is **Southwest Research Institute**
(https://ror.org/03tghng59, ROR display name "Southwest Research Institute", acronym "SwRI"); the
Boulder office has no separate ROR record. HSSI asks for the complete organization name without
acronyms, so the ROR display name is recorded rather than the ORCID site-qualified string or the
acronym.*

*Considered and not selected: an organization author for the **SwRI IDEA Lab**. The `LICENSE` file's
copyright line reads `Copyright (c) 2025 SwRI-IDEA-Lab`, and the repository is owned by the GitHub
organization of that name. It was not recorded as a Field 6 organization author because (a) the GitHub
organization `SwRI-IDEA-Lab` carries no `name`, `description`, `blog`, `location` or `email`, giving
no authoritative expansion of the group's formal title, (b) no ROR record exists for a lab at that
granularity — the ROR-registered entity is the parent institute, already captured as the author's
affiliation — and (c) HSSI infers organization-ness from a `ror.org` identifier, so an identifier-less
organization author would be unresolvable. The copyright attribution is recorded here instead, which
preserves the fact without inventing a value.*

### 7. Software Name (MANDATORY)
Surya Workshop

*Source: the `README.md` top-level heading, `# Surya Workshop`. SoMEF independently extracted the
same string as `full_title`. The repository slug is `surya_workshop`; the README's title case is
preferred as the human-readable name, and the slug remains discoverable through the Field 3
repository URL.*

### 8. Description (MANDATORY)
Surya Workshop is a documented template repository for fine-tuning Surya — a 366-million-parameter
spatiotemporal transformer foundation model for heliophysics, developed as a NASA-IMPACT / IBM
AI4Science collaboration and pre-trained on full-resolution NASA Solar Dynamics Observatory (SDO)
data — on a researcher's own downstream solar science task. It separates reusable infrastructure
from task-specific code: `workshop_infrastructure/` provides a typed YAML configuration layer, the
`HelioNetCDFDataset` loader for 13-channel SDO image stacks (8 AIA EUV/UV passbands plus HMI
line-of-sight magnetogram, vector field components and Doppler velocity) with transparent local or
S3 access, signum-log normalization and its inverses, PEFT LoRA utilities, an S3 throughput
benchmark, dataset-index construction and splitting tools, and a vendored copy of the Surya
backbone; `downstream_apps/template/` holds a complete worked example — solar flare intensity
regression against a HEK flare catalog — as three numbered notebooks, a lettered supporting
notebook on tensor shapes and broadcasting, and a numbered production training script sharing one
configuration file.

The package assumes a user starts from the pre-trained Surya checkpoint rather than training from
scratch, and that data is read as per-timestep NetCDF files indexed by a CSV (the shipped indices
point at the public SuryaBench bucket on AWS Open Data). Three fine-tuning regimes are available
through a single configuration switch: LoRA adapters on the feed-forward and fused attention
projections with the head trainable, a head-only linear probe, or full fine-tuning. Design choices
are documented rather than implicit — configuration is typed and rejects unknown keys with a list
of valid names, paths resolve relative to the configuration file, determinism is one configuration
key away with its measured throughput cost stated, and a dataset that needs an S3 cache directory
fails at construction rather than part-way through the first epoch. `ADAPTING.md` gives a
step-by-step procedure for copying the template to a new task, whose governing rule is that generic
code is imported from the shared layer and never copied.

*Source: composed from `README.md` (sections "The Surya Foundation Model", "Purpose of This
Repository", "Repository Structure", "How to Use This Repository", "Key Design Decisions"),
`downstream_apps/template/ADAPTING.md`, and `downstream_apps/template/configs/config_script.yaml`.
The 366M figure, the NASA-IMPACT / IBM AI4Science attribution, and the 13-channel composition are
the README's and are corroborated by the arXiv:2508.14112 abstract; the three fine-tuning regimes
and the configuration behaviors are stated in the README's "Key Design Decisions" and verified
against `workshop_infrastructure/configs.py` and `utils.py`.*

### 9. Concise Description (OPTIONAL)
A documented template for fine-tuning the Surya heliophysics foundation model on your own SDO-based
downstream task, with reusable data, config and LoRA infrastructure.

*168 characters, within the 200-character limit. Written separately because the description's first
200 characters open on the definition of Surya itself rather than on what this repository provides,
which would mislead a search-result preview into describing the model instead of the template.*

### 10. Publication Date (RECOMMENDED)
2025-12-23

*Source: the repository's first commit, `b91c1086` "Initial commit", authored 2025-12-23 16:57:54
-0700 — the same instant as the GitHub API's `created_at: 2025-12-23T23:57:54Z`. Used for the
initial version of the software, as the field instructs. There is no release or DOI that could
supply a formal publication date.*

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

*Per the field guidance, when no DOI has been obtained the repository host is the correct publisher.
Zenodo is not applicable: no DOI exists (Field 2). GitHub has no ROR record — ROR registers research
organizations, not commercial code-hosting platforms — so the platform URL is used, which the field
explicitly permits ("or URL otherwise").*

### 12. Version (RECOMMENDED)
- **Version Number:** Not found
- **Version Date:** Not found
- **Version Description:** Not found
- **Version PID:** Not found

*The project has never issued a version. `git tag -l` on the pinned revision returns nothing, the
GitHub releases endpoint returns an empty array, and the tags endpoint returns an empty array. There
is no `CHANGELOG.md`, no `__version__` attribute anywhere in the tracked tree, and no packaging
metadata (no `setup.py`, `pyproject.toml`, `setup.cfg`, or `PKG-INFO`) that could carry a version —
the repository is installed by cloning and creating the conda environment, not by a package manager.
The source revision in this dossier's header is the only precise identifier of the state described
here, which is why it is pinned. A future refresh should check for tags before assuming this is
still true.*

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*`environment.yml` pins `python=3.12`, and both `README.md` and the repository's `CLAUDE.md` state
that Python 3.12+ is required. The GitHub languages endpoint reports Python 282,681 bytes, Jupyter
Notebook 101,429 bytes, and Shell 25,757 bytes; the notebooks are Python, so Python is
overwhelmingly dominant.*

*Rejected: a value for the shell scripts. The three `AWS_Workshop_*.sh` setup scripts and
`download_scalers*.sh` are bash, but the vocabulary has no Bash or Shell row, and `Other` would
convey nothing while implying an unnamed significant language. The field explicitly asks for the
most important languages rather than an exhaustive list, and these scripts are one-time host
provisioning, not the software's implementation.*

### 14. Reference Publication (OPTIONAL)
Not found

*No publication describes this software. The repository contains no JOSS paper, no `paper.md`, and
no "cite this software" section. The one publication it cites — arXiv:2508.14112, "Surya:
Foundation Model for Heliophysics" — describes the upstream foundation model, not this fine-tuning
template, and so is not the reference publication for this entry; it is recorded in Field 27
instead, where the relationship it actually documents belongs.*

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

*Source: the repository's `LICENSE` file, whose first line is `MIT License` and whose copyright line
is `Copyright (c) 2025 SwRI-IDEA-Lab`. The GitHub API independently reports
`license.spdx_id: MIT`. `MIT License` was confirmed as a live `License` row; the URI is that row's
stored `url`. Note that HSSI's `Software.license` is a foreign key to a shared license row that
carries the URL, so the URI is not stored per-software — it is recorded here for completeness of the
dossier.*

*A conflict worth noting for a future refresh: the license grants MIT terms over the repository as
distributed, but the vendored Surya backbone is Apache 2.0 upstream (the README's "Resources" list
states "License: Apache 2.0" for Surya). Field 15 records the license the software declares for
itself, which is MIT; the upstream licensing of the vendored component is a fact about Field 29's
related software, not a reason to change this value.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- machine learning
- deep learning
- foundation model
- fine-tuning
- transfer learning
- solar dynamics observatory
- sdo
- aia
- magnetogram
- euv
- solar flares
- space weather
- heliophysics
- solar physics
- python
- pytorch

*Keywords is HSSI's only open vocabulary, so unknown values are created rather than rejected. To
avoid minting near-duplicates, each candidate was checked against the live `Keyword` list first.
Twelve of the sixteen already exist as rows and are reused verbatim: `machine learning`, `deep
learning`, `solar dynamics observatory`, `sdo`, `aia`, `magnetogram`, `euv`, `space weather`,
`heliophysics`, `solar physics`, `python`, `pytorch`. Four would be newly created — `foundation
model`, `fine-tuning`, `transfer learning` and `solar flares`. These four are the terms that most
specifically distinguish this software and have no acceptable existing substitute: the nearest
existing row to `solar flares` is `flare detection`, which describes a different task, and nothing
existing covers the foundation-model / parameter-efficient-fine-tuning subject matter at all. All
entries are lower-case and one term per entry, matching the established convention of the list.*

*Rejected: `surya` and `lora` as bare keywords. `Surya` is already carried by the software name,
description, and the Field 27 publication, and as a standalone keyword it collides with the large
body of unrelated Zenodo records noted in Field 2. `lora` is ambiguous with the LoRaWAN radio
protocol and is covered by `fine-tuning` and `transfer learning`.*

### 17. Data Sources (OPTIONAL)
- S3/Cloud-aware
- Observatory/Mission-specific

*`S3/Cloud-aware` is the primary and best-evidenced source: the four shipped index files in
`data/indices/` contain `s3://nasa-surya-bench/...` paths exclusively, `HelioNetCDFDataset`
implements three distinct S3 access modes over boto3 and s3fs, `workshop_infrastructure/utils.py`
provides `make_s3_client`, `parse_s3_uri` and `detect_ec2_region`, `UploadBestCheckpointToS3`
writes results back to S3, and `benchmark_s3.py` exists solely to tune S3 transfer parameters.*

*`Observatory/Mission-specific` is recorded because the science data the software consumes is
SDO-specific: the SuryaBench bucket contains AIA and HMI observations only, and the channel names
the dataset requests (`aia94` … `hmi_v`) are SDO variable names with no meaning for another
mission. The field's own instruction — select observatory-specific and name the mission in Related
Observatory — is satisfied by the Solar Dynamics Observatory entry in Field 32.*

*Rejected: `HTTP/HTTPS Directories`. `assets.py` does fetch over HTTPS from HuggingFace, but what it
retrieves is the pretrained checkpoint `surya.366m.v1.pt` and the normalization file `scalers.yaml`
— model assets, not science data input. This field asks which data input sources the software
supports, and no science data arrives over HTTP.*

*Rejected: `CDAWeb`, `The Virtual Solar Observatory.`, `HAPI`, `SSCWeb`, and every other named
archive. None appears anywhere in the tracked tree; the software has no client for any of them.*

### 18. Input File Formats (RECOMMENDED)
- netCDF3/4
- csv

*`netCDF3/4`: `HelioNetCDFDataset.load_nc_data()` opens each timestep with
`xr.open_dataset(filepath, engine="h5netcdf", chunks=None, cache=False)` and extracts the requested
channel variables. `environment.yml` pins `h5netcdf=1.7` for exactly this purpose.*

*`csv`: three distinct CSV inputs are read with `pd.read_csv` — the timestep index files in
`data/indices/` (`path`, `timestep`, `present` columns), the HEK flare catalog
`downstream_apps/template/data/hek_flare_catalog.csv` (61,210 events with `start_time`,
`peak_time`, `end_time`, `GOES_class`, `AR`, `CMX`, `CMX_VALUE`, `intensity`), and the split indices
produced by `split_csv_index.py`.*

*Considered and rejected: `HDF5`. The argument for it is real and is recorded here so a future agent
can weigh it rather than rediscover it — NetCDF4 files are HDF5 containers, the reader is the
HDF5-backed `h5netcdf` engine, `hdf5plugin` is imported into `helio.py` purely for its side effect
of registering HDF5 compression filters, and both the README and the config discuss HDF5 random-access
behaviour when explaining why `stream` mode is slow. It is nevertheless excluded because the software
offers no path that opens a generic HDF5 file: every read goes through xarray with a fixed expectation
of named SDO channel variables. Listing HDF5 would tell a searcher this software can read their HDF5
data, which it cannot.*

*Documented omission: YAML. `config_script.yaml` and `scalers.yaml` are read with `yaml.safe_load`,
but they are configuration and normalization statistics, not data input, and the `FileFormat`
vocabulary has no YAML row. `Other` was rejected as uninformative — it would signal an unnamed
supported data format that does not exist.*

### 19. Output File Formats (RECOMMENDED)
- csv

*`workshop_infrastructure/data/create_csv_index.py` writes the timestep index (`df.to_csv`);
`split_csv_index.py` writes three split files (`df_train.to_csv`, `df_val.to_csv`,
`df_test.to_csv`, each with `index=False`); and the training script attaches Lightning's
`CSVLogger`, which writes a metrics CSV per run.*

*Documented omission: model checkpoints. The primary artifact a training run produces is a
checkpoint — `ModelCheckpoint` writes `.ckpt` files to `cfg.output.ckpt_dir`, and
`UploadBestCheckpointToS3` optionally uploads the best one under the configured `s3_best_key`. The
`FileFormat` vocabulary has no row for a PyTorch checkpoint, and `Other` was rejected because it
would imply an unnamed *data* format. This omission is deliberate, not an oversight.*

### 20. Operating System (RECOMMENDED)
- Linux

*This is the only OS the repository provides evidence for, and the reasoning is recorded so a future
refresh does not silently broaden it. `workshop_infrastructure/setup_scripts/AWS_Workshop_Anaconda_install.sh`
hard-codes `ANACONDA_INSTALLER="Anaconda3-${ANACONDA_VERSION}-Linux-x86_64.sh"` and installs to
`/opt/anaconda3`; the README's performance guidance and the benchmark script's EC2 detection assume
an AWS Linux instance; and the documented workflow is `CUDA_VISIBLE_DEVICES=... python -m ...`.*

*`Mac` and `Windows` were considered and not recorded. The software is pure Python and every conda
and pip dependency in `environment.yml` ships macOS and Windows builds, so it very likely runs on
both — but "likely runs" is inference, not evidence, and no test matrix, CI configuration, or
documentation statement supports it. There is no `.github/` directory at all, so no CI has ever
exercised any platform. `Operating System Independent` was rejected for the same reason, and because
it would contradict the Linux-only installation path the project actually documents. If a future
refresh finds a CI matrix or a platform statement, these should be revisited.*

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- GPU

*`x86-64`: the Anaconda installer the setup script downloads is the `Linux-x86_64` build.*

*`GPU`: the training script sets `accelerator="gpu" if torch.cuda.is_available() else "cpu"` with
`precision="bf16-mixed"` on CUDA; every notebook opens by assigning `CUDA_VISIBLE_DEVICES`; the
config documents a determinism measurement taken on an A100 and warns that
`model.learned_flow: true` is incompatible with strict determinism because `F.grid_sample` has no
deterministic CUDA backward; and fine-tuning a 366M-parameter model on 4096×4096 imagery is not
practical without one.*

*Rejected: `HPC or HEC`. The multi-GPU path is DDP on a single cloud instance via Lightning's
`strategy="auto"`. There is no MPI dependency, no batch-scheduler integration, and no multi-node
configuration. A comment in `helio.py` mentions Numba hanging in DataLoader workers "on some GPU
clusters", but that is a portability caveat, not evidence the software targets HPC.*

*Rejected: `Apple Silicon arm64` and `CPU Independent`. The CPU-only test suite (`tests/`, which
`CLAUDE.md` describes as CPU-only and fast) shows the code imports and constructs tiny models
without a GPU, but that is a unit-test affordance, not a supported deployment architecture.*

### 22. Related Phenomena (OPTIONAL)
- Solar Flares
- X-ray emission

*`Solar Flares`: the template downstream task is solar flare intensity regression. The shipped
`hek_flare_catalog.csv` is a catalog of 61,210 flare events, `FlareDSDataset` aligns them to SDO
timesteps, and the job is named `solar_flare_forecasting`.*

*`X-ray emission`: the regression target is the catalog's `intensity` column — peak GOES soft X-ray
flux, alongside the `GOES_class` letter designation. Notebook 0's opening markdown describes the
setup as "casting the problem as an X-ray flux regression problem", and the dataset docstring
records the label as normalized log10 flare intensity.*

*Rejected: `Solar Corona`. The AIA EUV passbands observe the corona, but the software studies no
coronal phenomenon — the corona is the imaging domain, which is already captured by the `Corona`
value in Field 5. A user filtering Phenomena for `Solar Corona` is looking for coronal-physics
software and would not be served by this result.*

*Rejected: `Solar Wind`. The README reports that upstream Surya improved solar wind speed prediction
by 19%, but that is an upstream benchmark for a downstream task this repository does not implement.
Nothing in the tracked tree touches solar wind data.*

*Rejected: `Coronal Mass Ejections`, `Coronal Heating`, `Geomagnetic Storms`. No evidence of any
kind; none of these terms appears in the tracked tree.*

### 23. Development Status (RECOMMENDED)
Active

*The repository is being actively developed and is in a usable state. Evidence for activity: 202
commits, the most recent dated 2026-09-15 — the day before this extraction — merging pull request
#18 from `feature/fix_lora`, itself a substantive correctness fix with accompanying regression
tests. Evidence for usability: the template runs end to end (four notebooks plus a production
training script), `ADAPTING.md` documents the adaptation procedure, and 27 forks and 35 remote
branches indicate the workshop cohort actually used it.*

*Why `Active` and not `WIP`, recorded because this project has no release, no tag, and no version
of any kind (Field 12), which makes the choice look debatable at first glance. repostatus.org
defines the two statuses as follows. `Active`: "The project has reached a stable, usable state and
is being actively developed." `WIP`: "Initial development is in progress, but there has not yet
been a stable, usable release suitable for the public." `Active` is right because its criterion is
a stable, usable state rather than a formal release artifact, and that state has been reached — the
template runs end to end and is documented for adaptation. A template repository is consumed by
cloning and copying rather than by installing a release, so the absence of tags reflects the
distribution model rather than immaturity; `WIP` does not fit, because its "stable, usable release
suitable for the public" clause describes software that is not yet usable, which is not the case
here. The README additionally documents a completed correction cycle (earlier LoRA runs are
declared invalid and must be re-run), which is the behaviour of a maintained project rather than an
abandoned one.*

*On the wording of those two definitions: they are quoted from repostatus.org, which is the source
the field's guidance directs submitters to. HSSI's own `resource_submission_form_fields.md` renders
the same two statuses in a compressed house form — "Reached stable, usable state and being actively
developed" and "Initial development in progress; no stable, usable public release yet" — which is
HSSI's paraphrase, not repostatus.org's text. The two are easily conflated and must not be blended:
an earlier revision of this dossier quoted the HSSI phrasing while attributing it to
repostatus.org.*

### 24. Documentation (RECOMMENDED)
https://github.com/SwRI-IDEA-Lab/surya_workshop

*There is no separate documentation site: no `docs/` directory, no Sphinx or MkDocs configuration,
no ReadTheDocs project. Documentation is the repository itself — a substantial `README.md` covering
purpose, repository structure, environment setup, the notebook sequence, the production script, S3
access modes and tuning, and key design decisions; `downstream_apps/template/ADAPTING.md`, a
step-by-step guide to building a new downstream task; and extensive module- and function-level
docstrings. The field instructs that when the documentation link is the same as the access URL, that
link should be entered here, so the repository root — which renders the README, including its
installation instructions — is the correct value.*

### 25. Funder (OPTIONAL)
Not found

*No funding information exists for this software. There is no acknowledgments or funding section in
`README.md`, `ADAPTING.md`, `CLAUDE.md`, or `LICENSE`, no grant number anywhere in the tracked tree,
and no reference publication whose acknowledgments could be consulted (Field 14).*

*Explicitly rejected, because it is an easy trap for a future refresh: the funding visible on the
arXiv abstract page for 2508.14112 — the Simons Foundation, Simons Foundation International, and
Schmidt Sciences — is arXiv's own institutional donor footer, which appears identically on every
arXiv page. It is not the Surya paper's funding and has nothing to do with this software.*

*Also rejected on principle: whatever funded upstream Surya. Even if identified, it would be the
foundation model's funding, not this template's, and Field 25/26 guidance is explicit that only what
funded *this* software belongs here.*

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

*See Field 25 — no funding information of any kind exists for this software.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.48550/arXiv.2508.14112

*"Surya: Foundation Model for Heliophysics" (arXiv:2508.14112, submitted 2025-08-18, revised
2025-08-21; 33 authors including Andrés Muñoz-Jaramillo, this software's author). It is the paper
that describes the foundation model this repository exists to fine-tune and whose backbone it
vendors, and it is the single publication the README cites. The DOI is registered at DataCite
(publisher "arXiv", publication year 2025, resourceTypeGeneral "Preprint"), so the `doi.org` form
is used in preference to the bare arXiv abstract URL.*

*Title accuracy: the README renders the title as "Surya: A Foundation Model for Heliophysics", with
an indefinite article. The registered title in both the arXiv metadata and the DataCite record is
"Surya: Foundation Model for Heliophysics", without it. The registered form is used above; the
discrepancy is noted so a future agent does not "correct" the DOI record to match the README.*

*Considered and not selected: a Crossref search for a peer-reviewed version returned only unrelated
heliophysics works, so as of this extraction the preprint is the only published form. A future
refresh should check whether a journal version has appeared and, if so, whether it should replace or
accompany the preprint DOI.*

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.5281/zenodo.17872178
- https://huggingface.co/datasets/nasa-ibm-ai4science/core-sdo

*The Zenodo DOI is the **concept** DOI for the SuryaBench SDO Dataset (version DOI
`10.5281/zenodo.17872179`, published 2025-12-09; 25 creators including Andres Munoz-Jaramillo). The
concept DOI is recorded deliberately, so the reference tracks all versions. This is the dataset the
software actually reads: its Zenodo description states that the record "exists only to register a
DOI for the SuryaBench dataset hosted on the AWS Open Data Registry" and points at
`https://registry.opendata.aws/surya-bench/`, whose S3 bucket is `nasa-surya-bench` — exactly the
bucket every path in the four shipped `data/indices/*.csv` files resolves to. The AWS registry entry
describes it as machine-learning-ready SDO AIA and HMI observations spanning May 2010 to July 2024,
managed by NASA IMPACT, which matches the channel list the software requests and the 2010-05 start
of the shipped index.*

*The HuggingFace `core-sdo` dataset repository is recorded because `workshop_infrastructure/assets.py`
fetches `scalers.yaml` from it by name (`AssetSpec("nasa-ibm-ai4science/core-sdo", "dataset",
"scalers.yaml")`), and those per-channel normalization statistics are a hard requirement for every
run — without them the dataset cannot normalize a single sample. It has no DOI, so its permanent
HuggingFace landing page is used, as the field permits for a dataset lacking one. Verified reachable
(HTTP 200).*

*Documented omission: the HEK flare catalog. `downstream_apps/template/data/hek_flare_catalog.csv`
is a 61,210-row flare event catalog shipped inside the repository and derived from the Heliophysics
Event Knowledgebase. It is genuinely a dataset the software supports functionality for, but it has
no DOI and no permanent landing page of its own — it is a derived extract committed as a file, not a
published dataset, and linking the HEK service would point at a query interface rather than at this
data. It is recorded here in prose rather than invented as a URL.*

*Considered and not selected: `https://huggingface.co/nasa-ibm-ai4science/Surya-1.0`. It is fetched
by the same `assets.py` mechanism (`AssetSpec("nasa-ibm-ai4science/Surya-1.0", "model",
"surya.366m.v1.pt")`) and is equally essential, but it is a pretrained model checkpoint rather than
a dataset. It is recorded under Field 29 instead, as the distribution point for the related Surya
software.*

### 29. Related Software (OPTIONAL)
- https://github.com/NASA-IMPACT/Surya
- https://github.com/sunpy/sunpy

*`NASA-IMPACT/Surya` is the most distinguishing relation this software has. It is the upstream
foundation model: this repository exists to fine-tune it, began its life with Surya as a git
submodule (commit `558d601`, "Add Surya submodule", 2025-12-23), and now carries a vendored copy
of its backbone in `workshop_infrastructure/models/`. The README states the trade-off explicitly:
because the backbone was copied in rather than depended on, it does not track upstream Surya
automatically, and a reader is told to check upstream before assuming a fix has landed in this
copy. The submodule was removed in commit `6c29042`, "Remove surya submodule". The pretrained
weights are distributed separately at `https://huggingface.co/nasa-ibm-ai4science/Surya-1.0`
(verified reachable, HTTP 200) and are downloaded by `assets.py` as `surya.366m.v1.pt`; that URL
is recorded here as the distribution channel rather than as a second entry, to avoid listing the
same relationship twice. Upstream Surya is Apache 2.0 licensed, which is worth knowing alongside
this repository's MIT license (Field 15).*

*`sunpy` qualifies as a domain-specific dependency whose presence characterizes this software as
heliophysics rather than generic ML, and the uses are specific and citable rather than incidental:
notebook 0 imports `sunpy.visualization.colormaps` and draws the eight AIA passbands with
`cmap=f'sdo{channel}'` and the four HMI magnetic-field channels with `cmap=f'hmimag'`. Both of
those are SunPy-registered colormaps, which is precisely what makes this a SunPy dependency rather
than a plain matplotlib one. The Doppler-velocity channel `hmi_v` — the one channel the notebook's
`"_v" not in channel` test routes to the `else` branch instead of to `hmimag` — is drawn with
`coolwarm` at the same ±1000 limits. That is a stock matplotlib colormap, not supplied by SunPy,
and so is not evidence of SunPy use. Separately, `HelioNetCDFDataset.__getitem__` calls
`sunpy.coordinates.ephemeris.get_earth(ts).lat.value` to supply per-timestep heliographic latitude
when `use_latitude_in_learned_flow` is enabled. `environment.yml` pins `sunpy=7.1`.*

*Considered and rejected, with reasons, so these are not re-proposed: PyTorch, PyTorch Lightning,
PEFT, torchmetrics, timm, einops, huggingface_hub, datasets, hf_transfer, WandB, boto3, s3fs,
numpy, scipy, pandas, matplotlib, scikit-learn, scikit-image, opencv, numba, xarray, dask,
h5netcdf, hdf5plugin, bottleneck and pytest. Every one of these would be equally at home in a web
application, a finance model, or a biology pipeline — they are generic scientific-Python, ML and
infrastructure plumbing. Listing them would say nothing about this software that is not equally
true of most of the ecosystem. That PEFT and PyTorch Lightning are load-bearing here does not change
this: importance to the implementation is not the test; *distinguishing* the software is.*

### 30. Interoperable Software (OPTIONAL)
Not found

*No package meets the bar of a demonstrated exchange — a shared or converted data model, output of
one imported into the other, an adapter or converter API, a plugin relationship, a companion
package, or a cross-language bridge. The repository exposes no converter function, no foreign data
model, and no documented handoff to another tool. Its outputs are PyTorch checkpoints and CSV
metric logs consumed by nothing in particular.*

*Each candidate and why it fails, recorded so a future refresh does not relitigate them:*
- *`sunpy` — a genuine heliophysics peer tool, and the only candidate that survives the
  "would this be at home in a finance model?" test. But the relationship is consumption, not
  exchange: the software borrows SunPy's registered matplotlib colormaps and one ephemeris scalar.
  No `sunpy.Map` is ever constructed, accepted, or returned, and no SunPy object crosses the
  boundary in either direction. Recorded under Field 29 as a domain-specific dependency, which is
  where a consumption relationship belongs.*
- *`xarray`, `dask`, `h5netcdf` — Tier B packages requiring cited evidence of a specific exchange.
  Here `xr.open_dataset` is called internally inside `load_nc_data` and the result is immediately
  converted with `.to_array().load().to_numpy()`; no xarray object is ever part of the public
  interface. "Uses xarray internally" is explicitly not sufficient.*
- *PyTorch, PyTorch Lightning, PEFT, torchmetrics, timm, huggingface_hub — generic ML
  infrastructure, Tier A by the domain-independence test regardless of how central they are.*
- *A blanket claim that the software interoperates with "the scientific Python ecosystem", or with
  PyHC packages by ecosystem membership, was considered and rejected: such claims are never
  sufficient on their own, and this software is not a PyHC member in any case (Field 30's
  membership question is settled negatively — see the note below).*

*PyHC registry check: the software appears in none of the three heliophysicsPy registry files —
`projects_core.yml` (7 entries), `projects.yml` (59 entries), or `projects_unevaluated.yml` (28
entries). All 94 entries were enumerated and compared by package name, `code` repository URL, and
description; no entry references `surya_workshop`, `SwRI-IDEA-Lab`, or this author. No PyHC-curated
metadata was therefore available to seed any field in this dossier.*

### 31. Related Instruments (OPTIONAL)

**Instrument 1**
- **Instrument Name:** Atmospheric Imaging Assembly
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SDO/AIA

**Instrument 2**
- **Instrument Name:** HMI
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SDO/HMI

*Both pass the "designed to support" gate decisively: the software's entire data path is built
around these two instruments' products. `config_script.yaml` declares
`channels: [aia94, aia131, aia171, aia193, aia211, aia304, aia335, aia1600, hmi_m, hmi_bx, hmi_by,
hmi_bz, hmi_v]`; `HelioNetCDFDataset` extracts exactly those NetCDF variables; `build_scalers()`
loads per-channel normalization statistics keyed by those names; `inverse_transform_data()` returns
them in the instruments' physical units (DN for AIA, Gauss and m/s for HMI); and notebook 0 renders
the AIA passbands and the HMI magnetic-field channels with their instrument-specific colormaps.
A user searching HSSI for `instrument:"AIA"` should certainly get this back.*

*Resolution: each matched exactly one row of the correct type in the live
`InstrumentObservatory` vocabulary (ladder rule 1), with no `.html` duplicate and no same-name
collision. Names are copied verbatim from the matched rows — note that the HMI row's `name` is the
bare abbreviation `HMI`, not the expanded "Helioseismic and Magnetic Imager"; the expanded form
would not match and must not be substituted. The vocabulary was verified 100% SPASE-backed at
extraction time (7,602 rows, 0 rows failing the `https://spase-metadata.org/` prefix guard).*

*Considered and omitted: **GOES X-ray Sensor**. The regression target is peak GOES soft X-ray flux
and the shipped catalog carries a `GOES_class` column, so the connection is real — but the software
never reads GOES data, implements no GOES format or convention, and would return nothing useful to
someone working with GOES XRS data; the flux values arrive pre-extracted in a CSV. It also cannot be
resolved: the vocabulary offers only four XRS instrument rows (GOES 5, 13, 14 and 15) and nothing in
the repository selects among them — the catalog's first event is dated 1975-11-05, predating all
four spacecraft, so the catalog plainly aggregates the full GOES series. Omitted under the relevance
gate, and independently unresolvable under ladder rule 5. This is a documented omission, not an
oversight.*

*Considered and omitted: **SDO/EVE** (`https://spase-metadata.org/SMWG/Instrument/SDO/EVE`). It
exists in the vocabulary and is an SDO instrument, but the software never touches EVE data. The
README mentions that upstream Surya was evaluated on EUV spectra modelling across 1,343 bands; that
is an upstream benchmark result, not a capability of this repository.*

### 32. Related Observatories (OPTIONAL)

**Observatory 1**
- **Observatory Name:** Solar Dynamics Observatory
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SDO

*The software supports no other mission. Every science input is SDO: the SuryaBench bucket holds SDO
AIA and HMI observations only, the model is pre-trained on SDO data, and the dataset class is
documented as a "PyTorch dataset for SDO (Solar Dynamics Observatory) NetCDF files". A single
type-2 row matched (ladder rule 1); the name is copied verbatim from that row. This entry is also
what makes the `Observatory/Mission-specific` selection in Field 17 meaningful, as that field's
guidance requires.*

### 33. Logo (OPTIONAL)
Not found

*The repository contains no logo, and none could be invented. Searching the tracked tree at the
pinned revision for `.png`, `.jpg`, `.jpeg`, `.svg`, `.gif`, `.webp` and `.ico` files returns
nothing; `downstream_apps/template/assets/` contains only a `.gitkeep` placeholder. Neither
`README.md` nor any other markdown file contains a markdown image, an `<img>` tag, or the word
"logo", and there are no badges.*

*A structural reason this is unlikely to change, worth recording: the repository's `.gitignore`
excludes `*.png`, `*.jpg` and `*.jpeg` outright, so image assets cannot be committed without an
explicit force-add. There is also no project website, no documentation site, and no PyHC registry
entry (Field 30) that might host one externally. A documented omission is the correct outcome here.*
