# Field 4 — Software Functionality

**Level:** RECOMMENDED · **API:** `softwareFunctionality[]` · **Change class:** enrich-only (refresh on request)
**Vocabulary:** `/api/models/FunctionCategory/rows/all/`
**Filter tab:** Category · **Free-text search tier:** T3 · **Field-search code:** `function`

## What it is

**Type:** Multi-select dropdown

**What it is:** The type of software.

**How to fill it:** Select all software functionalities that apply. Be as exhaustive as possible—these selections determine which filters and search results your software appears in.

**Write subcategories as `Parent: Child` — with a space after the colon.** That is the canonical form: it is what `get_full_name()` produces, what the API returns, what the submission form displays, and what the `submission-payload` / `update-payload` skills specify for payloads. Using it means a roundtrip diff against HSSI compares equal instead of showing a spurious whitespace difference.

The no-space form `Parent:Child` is also **accepted on input** — the serializer does `part.strip()` on `value.split(":")` — so older `hssi_metadata.md` files written that way are not wrong and must not be flagged as errors. Prefer the spaced form in anything new.

The 6 top-level categories are also selectable on their own, and **when a subcategory applies its parent must be listed too** (selecting a subcategory does not auto-add its parent). 13 subcategory names (`ML/AI`, `Spectrogram`, `Analysis`, …) recur under more than one parent — that is intentional, and the parent prefix disambiguates them. Every child has exactly one parent, so paths are never deeper than two levels.

<!-- vocab:FunctionCategory begin -->
**Possible Values** — *83 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/FunctionCategory/rows/all/` is authoritative.*

- Coordinate Transforms
- Coordinate Transforms: Heliospheric
- Coordinate Transforms: Ionospheric
- Coordinate Transforms: Magnetospheric
- Coordinate Transforms: Mission-Specific
- Coordinate Transforms: Planetary
- Coordinate Transforms: Solar
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: 3D Particle Distribution Processing
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Curlometer
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Assimilation
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Field-line Tracing
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Linear Gradient Estimation
- Data Processing and Analysis: Magnetic Null Finding
- Data Processing and Analysis: ML/AI
- Data Processing and Analysis: Packet Decommutation
- Data Processing and Analysis: Pitch Angle Distributions
- Data Processing and Analysis: Plasma Moments
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Spectrogram
- Data Processing and Analysis: Time Series Analysis
- Data Processing and Analysis: Wave Polarization Analysis
- Data Processing and Analysis: Wavelet Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: 3D Graphics
- Data Visualization: Hodograms
- Data Visualization: Line Plots
- Data Visualization: Mission-Specific
- Data Visualization: ML/AI
- Data Visualization: Movies
- Data Visualization: Orbit Plots
- Data Visualization: Spacecraft Formation Plots
- Data Visualization: Spectrogram
- Data Visualization: Web-Based
- Mission-related
- Mission-related: Analysis
- Mission-related: Archive
- Mission-related: Calibration
- Mission-related: Distribution/Access
- Mission-related: Infrastructure as Code
- Mission-related: Ingest
- Mission-related: Instrumentation
- Mission-related: Instrument Response
- Mission-related: Inventory
- Mission-related: ML/AI
- Mission-related: Monitoring
- Mission-related: Observatory/Instrument Models
- Mission-related: Operations
- Mission-related: Orchestration
- Mission-related: Packet Decommutation
- Mission-related: Processing
- Mission-related: Science Data Processing
- Mission-related: System Testing
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing
- Models and Simulations: First Principles
- Models and Simulations: Forecasting
- Models and Simulations: Forward-Fitting
- Models and Simulations: Instrument Response
- Models and Simulations: MHD
- Models and Simulations: Mission-Specific
- Models and Simulations: ML/AI
- Models and Simulations: Observatory/Instrument Models
- Models and Simulations: Physics-Based
- Models and Simulations: Theory
- Servers and Environments
- Servers and Environments: Data servers processing and handling
- Servers and Environments: Distribution/Access
- Servers and Environments: High Performance Computing
- Servers and Environments: Infrastructure as Code
- Servers and Environments: Software or Environment Container
<!-- vocab:FunctionCategory end -->

**Taxonomy shape.** The snapshot holds **83 values** — 6 top-level categories plus 77 `Parent: Child`
subcategory paths, built from 67 distinct names. The 6 top-level categories are Coordinate Transforms,
Data Processing and Analysis, Data Visualization, Mission-related, Models and Simulations, and Servers
and Environments. The 13 child names that sit under more than one parent are `2D Slices`, `Analysis`,
`Calibration`, `Distribution/Access`, `Field-line Tracing`, `Infrastructure as Code`,
`Instrument Response`, `ML/AI` (four parents), `Mission-Specific` (three), `Observatory/Instrument Models`,
`Packet Decommutation`, `Processing`, and `Spectrogram`. Treat the counts as a dated observation: the live
endpoint is authoritative, and the `update-api-spec` skill re-checks the taxonomy against it.

**The rows carry no definitions.** Every FunctionCategory row's `definition` is empty, so the category
reference under *Where to find it, and traps* is the working meaning of each value.

## Why it exists

This is the field most searchers use to narrow the catalogue by what software does — "show me data-access
tools", "show me MHD models". The sidebar Functionality filter and the third free-text search tier are
built on it, so a missing value hides the software from everyone browsing that capability, and the most
common real defect is a capability the software has but the record omits. A missing parent row leaves the
entry's top-level category off its own detail page and out of name searches for that category. An
over-claimed value — a dependency's feature, a wrapped
library's reach, a gallery example, a word in a grant title — puts the software in front of users who
need something it does not do and erodes their trust in the filter.

## How it appears on the site

- **Detail page:** a "Functionality" section of tags. Stored rows are grouped by parent family (the parent
  tag first, then its children), and families appear in the order their first member is stored. Each tag
  shows the row's own `name` — the bare child name for a subcategory — coloured by family (a strong shade
  for the parent, a lighter shade of the same hue for its children), and links to the homepage filtered by
  that exact row.
- **Filter:** the sidebar **Functionality** tab lists the 6 top-level categories, each expandable to its
  children. A child item matches entries that store that child row; a parent item matches entries that
  store the parent row **or any of its children** (`filterGroup.ts` checks the item's id and its
  sub-items' ids). The filter is therefore the one place a missing parent does not hide the entry.
- **Free-text search:** tier T3 (`software_functionality__name`), which matches row names — a search for a
  parent's name reaches only entries that store the parent row.
- **Field search:** `function:"…"` matches `software_functionality__name__icontains`.
- **JSON-LD:** `applicationCategory` lists the sorted top-level names (stored parents plus the parents of
  stored children), `applicationSubCategory` the full `Parent: Child` path of each stored child, and each
  stored row also appears in `keywords` as a `DefinedTerm` with description `softwareFunctionality`.

## Rubric: include / exclude

RECOMMENDED on the form; **treat as critical**. It is one of the most important fields, and it requires
understanding the full breadth of what the software does; extraction and validation both spend more time
here than on any other field, reading the code rather than the README. Walk the whole vocabulary on every
extraction and refresh, asking which new values now apply — validating only the recorded values reads as
complete while missing the point.

Rules 1–9 screen each candidate value: apply them top to bottom and stop at the first that fires. A
candidate none of them excludes is included under rule 12 when it has code evidence. Rules 10–11 then
complete the parent rows, and rules 12–15 govern the whole set.

1. **Only live rows, always fully qualified.** Confirm each candidate against the live
   `/api/models/FunctionCategory/rows/all/` vocabulary before writing it (see
   `sources/vocabulary-authority.md`). Write a subcategory as `Parent: Child` with a space after the colon,
   and **always send the qualified name**: the 13 recurring child names bind to an arbitrary row when sent
   bare. **Never flag colon spacing as an error, in either direction** — `Parent: Child` and `Parent:Child`
   bind to the same row, and a pre-existing no-space file is valid and must not be rewritten for spacing
   alone. Fires on: a candidate not in the live list — drop it or map it to the row it misspells.

2. **A dependency is not a feature.** Importing a library shows the software uses it, not that users get
   its capability: importing `matplotlib` doesn't mean "3D Graphics" unless the software actually generates
   3D plots, and importing `astropy.coordinates` or `sunpy.coordinates` to compute a pointing angle is not
   offering coordinate transforms. The library map below lists **indicators**, not guarantees. Fires on: a
   candidate whose only support is an import or a dependency declaration.

3. **Distinguish "uses internally" from "provides to users."** A package that internally converts
   coordinates as a utility step doesn't necessarily need "Coordinate Transforms" listed — only if
   coordinate transformation is a user-facing capability. However, if the user can access or benefit from
   the transform (even indirectly), err on the side of inclusion: a transform the user selects through a
   documented keyword or CLI flag, or whose converted output the user receives, qualifies. Fires on: a
   capability no public function, CLI entry point, exported symbol, or returned value exposes — exclude it.

4. **Example scripts and gallery pages are not the library's capability.** A plot drawn only in
   `examples/` or a docs gallery does not earn a Data Visualization child for the package. Fires on: the
   only evidence lives outside the distributed package's code.

5. **A wrapper does not inherit its wrapped library's capabilities.** A bridge that runs another library
   carries what the bridge itself does (assembling a runtime, converting data across the boundary), not
   what the wrapped library can do; access to functions is not access to data. Fires on: the capability
   exists only in the library being wrapped or called.

6. **A capability shipped only in separately distributed plug-ins is excluded.** Judge the distribution
   alone: the machinery a framework ships (a download API, file discovery, a processing pipeline) is its
   own; what a plug-in package implements belongs to that plug-in's record. Fires on: the capability
   appears only after installing another package.

7. **Never derive a value from a name.** An award title, a funding program, a project or institution name,
   or a paper about what the output is later used for is not evidence of what the code does (a grant
   titled "Assimilative Analysis…" does not make the software do data assimilation). Fires on: a candidate
   whose only support is such a name — exclude it, and record the source so it is not re-derived.

8. **Mission-related means part of a mission's own chain.** A package that *reads* MMS data is
   "Data Processing and Analysis: Data Access and Retrieval"; a package that is *part of the MMS ground
   system* — or ships the code that produces a mission's archive-standard science files, and is used by
   named missions for that — is "Mission-related". A third-party reader of finished archived products is
   not Mission-related. Fires on: the software's role relative to a mission's pipeline.

9. **A same-name child under a second parent needs a different capability.** Computing a spectrogram is
   "Data Processing and Analysis: Spectrogram"; displaying a spectrogram is "Data Visualization:
   Spectrogram". Many packages do both — list both; they are distinct rows under different parents. Code
   that produces arrays is processing, code that produces figures is visualization. Do **not** add the twin
   when it only restates a capability another stored value already carries (`Models and Simulations:
   Instrument Response` beside an evidenced `Mission-related: Instrument Response`). Fires on: a candidate
   whose child name is already stored under another parent.

10. **Every child needs its bare parent, listed separately.** A child never implies its parent, and **a
    stored child without its parent is a defect**. When a child applies, list its top-level category as its
    own value too (`Data Visualization` beside `Data Visualization: Spectrogram`). When a refresh finds an
    evidenced child stored without its parent, repair it by adding the parent, not by dropping the child.
    Fires on: any child in the final set.

11. **A parent alone is legitimate when no child fits.** When the evidence supports a top-level category
    but none of its children describes the capability (a solar-local-time routine, a terrestrial
    geodetic-to-geocentric switch under Coordinate Transforms), record the parent only and say which
    children were rejected. No parent category is listed without its children having been considered.
    Fires on: an evidenced category with every child rejected.

12. **Be exhaustive; each value needs code evidence.** Include every capability the software exposes to
    users, each justified by specific code evidence — a module, function, or file. If a package does data
    access AND visualization AND coordinate transforms, list all three with all relevant subcategories.
    The most common validator finding is *missing* functionalities. Under-classifying is as wrong as
    over-classifying: check whether several model subcategories apply at once (physics-based AND MHD AND
    forecasting), and check every child of each category the software touches.

13. **Order is stored data.** Preserve the stored order; insert a new member inside its parent's block
    (after that family's existing members), and never reorder stored rows as a side effect.

14. **Incumbents: enrich-only by default, refreshed on request.** Enrichment is identity-aware
    set-union: keep every stored value and add the new ones, even when the field already holds some
    values. A refresh the user asks for re-derives every stored value under rules 1–11 and removes one the
    evidence contradicts (a case-insensitive sweep for the capability returns nothing, or rule 5 or 7
    fires). A stored value a fair reading of the code supports is kept — removal needs evidence that it is
    wrong, not that it is arguably imprecise.

15. **Never invent; never leave it unexamined.** An empty value is legitimate only when the dossier
    carries durable evidence that no value applies; an unexamined blank is an **ERROR**.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

Examine the repo thoroughly to understand the full breadth of what it does; read the code, not just the
README.

**Sources, in priority order:**
1. The public API: what `__init__.py` exposes, exported functions and classes, CLI entry points. These are
   the user-facing capabilities.
2. Submodule and directory names — a directory called `coordinates/` or `visualization/` is a strong
   structural signal.
3. Tests and examples — they often reveal functionality not mentioned in the README; a test file named
   `test_spectrogram.py` is a strong signal. (Examples indicate where to look; rule 4 still governs.)
4. Imports, matched against the library map below as indicators.
5. README, documentation, and the reference publication — every capability they claim should be reflected
   in the classification, and confirmed in code.

**Verification steps (validating a classification):**
- [ ] Every listed value is from the allowed list (exact string match), written `Parent: Child`.
- [ ] Every subcategory has its parent category also listed.
- [ ] No parent category is listed without at least considering its subcategories.
- [ ] Package README claims are reflected in the classification.
- [ ] Code structure (directories, modules) is reflected in the classification.
- [ ] Test files and examples don't reveal unclassified functionality.
- [ ] Import statements in the package don't suggest missing functionality.
- [ ] The classification is defensible — each entry can be justified with specific code evidence
      (module, function, or file).
- [ ] For each functionality NOT listed: check the library map and the key indicators below against the
      actual codebase to find gaps.

**Commonly missed:**
- **Data Access and Retrieval** — data downloading is seen as "utility" not "functionality". If users call
  a function to get data, it's Data Access.
- **Coordinate transforms used internally** — packages do transforms as part of the workflow without
  advertising them. Search for coordinate system names and transform functions, then apply rule 3.
- **The processing-vs-visualization distinction for spectrograms** — check whether the code produces
  arrays (processing) or figures (visualization), or both.
- **Missing subcategories** — "Data Visualization" listed without the specific types; check each
  subcategory against the code.
- **`Data Processing and Analysis: Analysis`** — the catch-all child is easy to forget; check it whenever
  the package derives physical quantities.

**Traps:**
- **The bare parent and the `Analysis` child look alike in a rendered list.** `Data Processing and
  Analysis` (the top-level row) and `Data Processing and Analysis: Analysis` are different rows; read which
  one is stored before describing it.
- **JSON-LD looks complete when the page is not.** `applicationCategory` derives parents from stored
  children, so it lists a parent the entry does not store; the detail page and the filter show only
  stored rows. Check the stored rows, not the JSON-LD.
- **Archive-label arithmetic is not calibration.** Applying a scale and offset supplied in a product label
  is reading the product; calibration is gain models, response functions, flat-fielding.
- **Correcting storage order is not image processing** (flipping an array the archive stores bottom-up).
- **In-memory parsing is not file format conversion**; the software must write a format or hand one format
  on as another.
- **Assembling a time–frequency array counts as spectrogram processing** even when the Fourier transform
  happened upstream: what the searcher wants is software that hands them time–frequency data.
- **Evaluating an empirical model's secular-variation term is not `Models and Simulations: Forecasting`**,
  which is for prediction and nowcast products.

### Classification reference

The taxonomy uses two levels: **top-level categories** and **subcategories**. When a subcategory applies,
also include its parent top-level category (rule 10). Example: if software produces spectrograms, list
BOTH `Data Visualization` and `Data Visualization: Spectrogram`.

#### 1. Coordinate Transforms

**What it means:** Software that converts between coordinate systems or reference frames as a user-facing capability.

**Key indicators:**
- Functions named `transform`, `convert`, `to_*`, `from_*` relating to coordinate systems
- Import or use of coordinate libraries (see library table below)
- References to specific coordinate systems: GSE, GSM, GEO, SM, MAG, AACGM, HEE, HCI, HAE, RTN, Carrington, Stonyhurst, helioprojective, geographic, geomagnetic, MLT

**Subcategories and when to use them:**

| Subcategory | Use when the software converts... | Typical indicators |
|---|---|---|
| **Heliospheric** | Between heliospheric coordinate systems (HCI, HAE, HEE, Carrington, Stonyhurst, RTN) | Solar wind data, heliospheric modeling, inner heliosphere |
| **Ionospheric** | Between ionospheric coordinate systems (AACGM, MLT, magnetic latitude, apex coordinates) | `aacgmv2`, magnetic local time, auroral research, ionospheric models |
| **Magnetospheric** | Between magnetospheric coordinate systems (GSE, GSM, SM, GEO, MAG) | `spacepy.coordinates`, `geopack`, magnetosphere modeling |
| **Mission-Specific** | Using spacecraft-specific frames (instrument pointing, attitude, FOV) | `spiceypy`, SPICE kernels, instrument alignment |
| **Planetary** | Between planetary coordinate systems (non-Earth) | Planetary body references, Jupiter/Saturn/Mars coordinates |
| **Solar** | Between solar coordinate systems (Carrington, Stonyhurst, helioprojective, heliographic) | `sunpy.coordinates`, solar disk coordinates, solar features |

#### 2. Data Processing and Analysis

**What it means:** Software that reads, transforms, processes, or analyzes scientific data.

**Key indicators:**
- Data reading/writing functions
- Mathematical operations on scientific datasets
- Statistical analysis, signal processing
- Filtering, interpolation, curve fitting

**Subcategories and when to use them:**

| Subcategory | What it means | Typical indicators |
|---|---|---|
| **2D Slices** | Extracting 2D cross-sections from 3D data volumes | Slice extraction, plane cuts, volumetric data sampling |
| **3D Particle Distribution Processing** | Processing velocity distribution functions | Distribution function math, velocity space operations, phase space density |
| **Analysis** | General scientific analysis beyond basic processing | Statistical methods, derived physical quantities, scientific calculations |
| **Calibration** | Converting raw instrument data to physical units | Calibration files, response functions, gain corrections, flat-fielding |
| **Curlometer** | Computing curl of B from multi-spacecraft data | Multi-point analysis, Cluster/MMS, `curl` calculations on tetrahedra |
| **Data Access and Retrieval** | Downloading or querying data from remote archives | API clients, `sunpy.net.Fido`, `astroquery`, CDAWeb/HAPI clients |
| **Data Assimilation** | Combining observations with models | Assimilation algorithms, Kalman filters on geophysical data |
| **Data Reduction** | Reducing data volume preserving information | Averaging, binning, downsampling, filtering for noise reduction |
| **Energy Spectra** | Computing or analyzing energy spectra | Spectral calculations, energy channels, flux vs energy |
| **Field-line Tracing** | Tracing magnetic or electric field lines through data | Field line integration, `pfsspy`, streamline tracing |
| **File Format Conversion** | Converting between data file formats | Reading one format, writing another |
| **Image Processing** | Processing 2D image data scientifically | Deconvolution, feature detection, `scikit-image`, solar image processing |
| **Linear Gradient Estimation** | Estimating spatial gradients from multi-point data | Gradient calculations, multi-spacecraft spatial analysis |
| **Magnetic Null Finding** | Locating magnetic null points | Null point detection, magnetic topology analysis |
| **ML/AI** | Machine learning applied to data analysis | `tensorflow`, `pytorch`, `scikit-learn` for scientific analysis tasks |
| **Packet Decommutation** | Parsing raw telemetry packets into usable data | Binary packet parsing, CCSDS, telemetry stream processing |
| **Pitch Angle Distributions** | Computing particle pitch angle distributions | PAD calculations, magnetic field-aligned distributions |
| **Plasma Moments** | Computing density, velocity, temperature, pressure from distributions | Moment integration, distribution function → bulk quantities |
| **Processing** | General data processing (pipeline steps, transforms) | Data pipeline operations, transformation chains |
| **Spectrogram** | Computing time-frequency representations | FFT, STFT, wavelet transforms producing time-frequency arrays |
| **Time Series Analysis** | Analysis of time-ordered data | Temporal filtering, trend analysis, autocorrelation, `pandas` time series |
| **Wave Polarization Analysis** | Analyzing wave polarization properties | Stokes parameters, polarization ellipse, wave analysis methods |
| **Wavelet Analysis** | Wavelet-based signal analysis | Wavelet transforms, `pycwt`, wavelet coherence, scalograms |

#### 3. Data Visualization

**What it means:** Software that creates visual representations of scientific data.

**Key indicators:**
- `matplotlib`, `plotly`, `bokeh`, `vtk` imports
- Plot/figure generation functions
- Rendering, display, or animation functions

**Subcategories and when to use them:**

| Subcategory | What it means | Typical indicators |
|---|---|---|
| **2D Graphics** | Static 2D plots (contour, heatmap, image) | `pcolormesh`, `imshow`, contour plots, 2D maps |
| **2D Slices** | Visualizing 2D slices of 3D data | Slice display, cut-plane visualization |
| **3D Graphics** | 3D visualizations | `mplot3d`, `vtk`, `mayavi`, volume rendering |
| **Hodograms** | Plotting field component vs component | Hodogram functions, B-field component plots |
| **Line Plots** | Time series or 1D line plots | `plt.plot`, line charts, time series display |
| **Mission-Specific** | Visualizations unique to a mission's data types | Custom instrument-specific plot formats |
| **ML/AI** | ML-related visualizations | Model output display, feature importance |
| **Movies** | Animations or video from data sequences | `matplotlib.animation`, frame generation, movie export |
| **Orbit Plots** | Spacecraft or object trajectory visualization | Orbital path display, trajectory plots |
| **Spacecraft Formation Plots** | Multi-spacecraft configuration display | Constellation geometry, tetrahedron quality |
| **Spectrogram** | Displaying spectrograms | Dynamic spectra display, time-frequency image plots |
| **Web-Based** | Interactive browser-based visualizations | `plotly`, `bokeh`, `dash`, web dashboards |

#### 4. Mission-related

**What it means:** Software specifically designed to support a space mission's operations or data pipeline. This is distinct from general-purpose analysis software that happens to work with mission data.

**Key distinction:** A package that *reads* MMS data is "Data Processing and Analysis: Data Access and Retrieval". A package that is *part of the MMS ground system* is "Mission-related".

**Subcategories:** Analysis, Archive, Calibration, Distribution/Access, Infrastructure as Code, Ingest, Instrumentation, Instrument Response, Inventory, ML/AI, Monitoring, Observatory/Instrument Models, Operations, Orchestration, Packet Decommutation, Processing, Science Data Processing, System Testing

#### 5. Models and Simulations

**What it means:** Software that models physical systems or runs simulations.

**Key indicators:**
- Numerical solvers (ODE/PDE integrators)
- Physical model implementations (empirical or first-principles)
- Simulation frameworks
- Forward modeling or synthetic data generation

**Subcategories and when to use them:**

| Subcategory | What it means | Typical indicators |
|---|---|---|
| **Data Guided** | Models driven by observational data | Data-driven boundaries, observational inputs |
| **Empirical** | Statistical/empirical models | Empirical formulas, climatological models (IRI, MSIS, HWM, IGRF) |
| **Field-line Tracing** | Tracing field lines in model fields | PFSS, potential field extrapolation |
| **First Principles** | Models from fundamental physics | Full MHD equations, kinetic theory, ab initio |
| **Forecasting** | Prediction/nowcasting | Space weather prediction, forecast output |
| **Forward-Fitting** | Synthetic data + parameter optimization | Forward model, chi-square fitting, inversion |
| **Instrument Response** | Modeling instrument behavior | Response matrix, effective area, PSF simulation |
| **MHD** | Magnetohydrodynamic simulations | MHD solver, BATSRUS, Athena, Pencil Code |
| **Mission-Specific** | Models for a specific mission | Spacecraft-specific modeling |
| **ML/AI** | ML-based models | Neural network predictions, surrogate models |
| **Observatory/Instrument Models** | Modeling observatories or instruments | Instrument simulation, synthetic observations |
| **Physics-Based** | Physics-based (broader than first principles) | Physical equations, semi-empirical physics |
| **Theory** | Analytical/theoretical calculations | Analytical solutions, theoretical frameworks |

#### 6. Servers and Environments

**What it means:** Infrastructure, deployment, and runtime environment software.

**Subcategories:** Data servers processing and handling, Distribution/Access, High Performance Computing, Infrastructure as Code, Software or Environment Container

**Key indicators:** Server implementations, Dockerfiles, MPI/parallel computing, HPC job scripts, Kubernetes manifests, data serving endpoints

### Library-to-functionality indicators

These mappings are **indicators**, not guarantees. Always verify the software actually exposes the functionality to users.

| Library / Import | Likely Functionality |
|---|---|
| `sunpy.coordinates` | Coordinate Transforms, Coordinate Transforms: Solar |
| `astropy.coordinates` | Coordinate Transforms |
| `aacgmv2` | Coordinate Transforms: Ionospheric |
| `spacepy.coordinates` | Coordinate Transforms: Magnetospheric |
| `spiceypy` | Coordinate Transforms: Mission-Specific |
| `geopack` | Coordinate Transforms: Magnetospheric |
| `sunpy.net`, `sunpy.net.Fido` | Data Processing and Analysis: Data Access and Retrieval |
| `astroquery` | Data Processing and Analysis: Data Access and Retrieval |
| `hapiclient` | Data Processing and Analysis: Data Access and Retrieval |
| `cdflib`, `spacepy.pycdf` | Data Processing and Analysis (file I/O) |
| `astropy.io.fits` | Data Processing and Analysis (FITS file I/O) |
| `h5py` | Data Processing and Analysis (HDF5 file I/O) |
| `matplotlib` | Data Visualization |
| `matplotlib.animation` | Data Visualization: Movies |
| `plotly`, `bokeh` | Data Visualization: Web-Based |
| `vtk`, `mayavi`, `pyvista` | Data Visualization: 3D Graphics |
| `scikit-image`, `skimage` | Data Processing and Analysis: Image Processing |
| `scipy.signal` | Data Processing and Analysis: Time Series Analysis |
| `pycwt` | Data Processing and Analysis: Wavelet Analysis |
| `tensorflow`, `pytorch`, `sklearn` | ML/AI (under whichever parent category applies) |
| `pfsspy` | Models and Simulations: Field-line Tracing |
| `Docker`, `Singularity` | Servers and Environments: Software or Environment Container |
| `mpi4py` | Servers and Environments: High Performance Computing |

## Payload and roundtrip notes

- **Key:** `softwareFunctionality` — an array of strings.
- **Format:** Use `"Parent: Child"` (with space after colon). Values must be exact matches from the endpoint.
  Graph-list lookup walks the parent → child chain: the part before the colon must match a top-level row
  (`parent_nodes__isnull=True`), and each later part must match a child of the row before it
  (`name__iexact`). A value without a colon matches `name__iexact` across **all** rows and takes the first
  — which is why a bare recurring child name binds arbitrarily. An unknown value raises
  `Unknown value '<value>'` and rejects the whole atomic request.
- **Always also include the bare parent top-level category as its own array entry** (e.g. include
  `"Data Processing and Analysis"` in addition to `"Data Processing and Analysis: Data Access and
  Retrieval"`). Selecting a subcategory does NOT automatically add its parent — the parent must be listed
  separately or it won't appear on the record.
- **Order is stored data.** `software_functionality` is a sorted many-to-many field (sortedm2m); the order
  sent is the order stored and returned by `/api/view/`. A set comparison hides a reorder; compare the
  ordered list.
- **M2M enrichment is set-union, and applies to shallow non-empty lists too.** When fresh metadata has M2M
  values (especially **Software Functionality**) that HSSI lacks, propose ADDING them — even if HSSI
  already has *some* values for that field. Do not skip a field just because it is "already populated"; a
  list with 1–2 values can still be expanded. The default intended value is `existing ∪ new` (keep every
  existing value, add the new ones). An explicitly approved removal instead uses the complete
  user-approved final set. This matters because the PATCH API **fully replaces** each M2M field — see
  `update-payload`. `[]` or `null` clears the field; an omitted key is unchanged.
- **Roundtrip by row id.** `/api/data/` returns row UUIDs, not names, and a row's `name` is the bare leaf
  (`Spectrogram`); the qualified path is computed from its parent. Resolve every stored id to its full path
  before comparing, and verify each patched value by the row id it bound — two stored rows can share a
  leaf name. The hierarchy is `parent_nodes` on the ORM object and `parents` in the API JSON.

## Worked examples

- **Framework with a parentless child (pysat).** The record held `Mission-related: Science Data
  Processing` without `Mission-related`. The distribution ships the code that writes the SPDF-standard
  files named missions publish, so the child stands (rule 8) and rule 10 adds the parent. The stored
  `Data Processing and Analysis: Data Assimilation` is removed: `assimilat` matches nothing in the tree, and
  the value traced to an award title (rule 7). `Coordinate Transforms` is recorded as a parent only
  (rule 11).
- **Mars radio-science reader (MGSutils).** The reader returns a labelled time–frequency array and the
  plotting module draws it with `pcolormesh`, so both `Data Processing and Analysis: Spectrogram` and
  `Data Visualization: Spectrogram` are recorded (rule 9). On the detail page they appear as two
  `Spectrogram` tags, each inside its own parent's colour group and linking to a different filter row; the
  API and JSON-LD carry the qualified names. Calibration, Image Processing and File Format Conversion are
  rejected per the traps above.
- **IGRF evaluator (igrf).** The user chooses geodetic or geocentric coordinates through a documented
  keyword and CLI flag. Rule 3 adds `Coordinate Transforms`; no child describes a terrestrial
  geodetic-to-geocentric conversion, so it stands alone (rule 11).
- **Solar instrument toolkit (sunkit-instruments).** `Mission-related` and `Data Visualization` were stored
  only as children; rule 10 adds both parents. `Models and Simulations: Instrument Response` is rejected
  because `Mission-related: Instrument Response` already carries the capability (rule 9), and
  `Data Visualization: 2D Graphics` because its only plot is a gallery example (rule 4).
- **Python bridge to SolarSoft (hissw).** The stored `Data Processing and Analysis: Data Access and
  Retrieval` came from SolarSoft's retrieval routines; hissw fetches nothing, so it is removed (rule 5).
  The stored `Servers and Environments: Software or Environment Container` gains its missing parent
  (rule 10).

## Provenance

- Vocabulary block `vocab:FunctionCategory` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 79-179 on 2026-09-22.
- The classification reference and library map were moved from the retired `software-functionality` skill on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
