# HSSI Metadata Extraction Results

**HSSI Software ID:** 65364bdd-6a19-404a-9a87-c1aa123017d3
**Repository:** https://github.com/NCAR/gcmprocpy
**Source Revision:** 456398e8c76f9b341b279e0a592c1d12b6a8cf32
**Extraction Date:** 2026-08-04
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

**Scope note.** The installable package lives in a nested `gcmprocpy/` subdirectory of the
repository (`gcmprocpy/pyproject.toml`, `gcmprocpy/setup.py`, `gcmprocpy/src/gcmprocpy/`), while
`docs/`, `LICENSE` and the top-level `README.md` sit at the repository root. Evidence cited below
therefore comes from two levels, and a path such as `src/gcmprocpy/plot_gen.py` means
`gcmprocpy/src/gcmprocpy/plot_gen.py`.

The repository is the renamed continuation of **tiegcmpy**: its first commit (2023-10-18) is
"Moved tiegcmpy to tiegcm3.0", `https://github.com/NCAR/tiegcmpy` now redirects to
`https://github.com/NCAR/gcmprocpy`, an `arch_tiegcmpy` branch survives on the remote, and the
`benchmark/*.py` scripts still open with `from tiegcmpy import *`. That history matters for the
publication date (Field 10) and for Related Software (Field 29).

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*The record's original submitter is not part of the published metadata, so no submitter identity is
asserted here.*

### 2. Persistent Identifier (RECOMMENDED)
Not found.

gcmprocpy has no DOI. The repository contains no `CITATION.cff`, no `codemeta.json`, no
`.zenodo.json`, no DOI badge in either `README.md`, and no "How to cite" section anywhere in
`docs/`. A DataCite search for `gcmprocpy` returns only the two NCAR-TIEGCM records
(10.5281/zenodo.20076374 and .20076375) — the *model*, not this tool — which surface because their
release notes name gcmprocpy as TIE-GCM's post-processing package. A DataCite search for the
predecessor name `tiegcmpy` returns zero results. SoMEF found no `identifier` field for the
repository.

The Zenodo–GitHub integration is not enabled: the repository has published no GitHub Releases at
all, so no release has ever been minted a DOI even though the tag `v1.5.2` exists. A future refresh
should re-check this — the maintainer is a co-author of the TIE-GCM Zenodo record and knows the
workflow, so a gcmprocpy concept DOI may appear.

### 3. Code Repository (MANDATORY)
https://github.com/NCAR/gcmprocpy

Carried over from the existing HSSI record and confirmed against three independent sources: the
git remote of the extracted clone, `[project.urls] Homepage` in `gcmprocpy/pyproject.toml`, and the
PyPI project metadata for `gcmprocpy`. The PyHC community registry lists the same repository with a
`.git` suffix (`https://github.com/NCAR/gcmprocpy.git`); the suffix-free form stored here is the
canonical browse URL and is preferred.

### 4. Software Functionality (MANDATORY)

- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Line Plots
- Data Visualization: Movies
- Models and Simulations
- Models and Simulations: Physics-Based

`Data Visualization` and `Data Processing and Analysis` are the two values the existing HSSI record
already carried. Each of the three parent categories used above is listed alongside its own
children, as HSSI requires, and no listed leaf belongs to a parent that is absent from the list.

Evidence, value by value:

- **Data Visualization: 2D Graphics** — `plt_lat_lon` draws filled and line contours through
  cartopy on mercator, polar-stereographic (paired north/south panels), orthographic and mollweide
  projections, with optional coastline, `Nightshade`, geomagnetic-equator and thinned wind-quiver
  overlays (`src/gcmprocpy/plot_gen.py`).
- **Data Visualization: 2D Slices** — `plt_lev_lat`, `plt_lev_lon`, `plt_lev_time`, `plt_lat_time`,
  `plt_lon_time` each render a 2-D cut through the 4-D (time, level, lat, lon) model volume; the
  companion `arr_*` extractors are classified under Data Processing and Analysis: 2D Slices.
- **Data Visualization: Line Plots** — `plt_lev_var`, `plt_var_time`, `plt_var_lat`, `plt_var_lon`
  and the 1-D branch of `plt_sat_track`; also `gpigen.make_plots`, which writes per-year
  `f107d_<year>.png` / `f107a_<year>.png` line plots (`src/gcmprocpy/gpigen/plotting.py`).
- **Data Visualization: Movies** — `mov_lat_lon` renders one PNG per timestamp and assembles them
  into an `.mp4` with `matplotlib.animation.FuncAnimation` at a caller-set frame rate
  (`src/gcmprocpy/mov_gen.py`); documented as its own page,
  `docs/source/gcmprocpy/movie_functions.rst`.
- **Data Processing and Analysis: 2D Slices** — the `arr_lat_lon`, `arr_lev_lat`, `arr_lev_lon`,
  `arr_lev_time`, `arr_lat_time`, `arr_lon_time` family returns 2-D arrays sliced from the model
  volume, and `batch_arr_lat_lon` does so for several variables at once
  (`src/gcmprocpy/data_parse.py`). These are exported from `__init__.py`, so they are user-facing,
  not internal plumbing.
- **Data Processing and Analysis: Analysis** — derived physical quantities computed from model
  state: Eliassen–Palm flux components and divergence (`data_epflux.py`), volume emission rates
  (`data_emissions.py`, `data_oh.py`), total and species mass/number densities, mean molecular mass
  and `pkt` (`data_density.py`), the `RHO`/`PMB`/`TNFP` and `OX`/`NOZ`/`HOX` composition-group
  derivables ported from tgcmproc `mkderived.F`, raw and percent difference fields
  (`data_diff.py`), and cos-latitude area-weighted means (`_coslat_weighted_mean`).
- **Data Processing and Analysis: Processing** — the general post-processing pipeline: variable and
  dimension introspection (`var_list`, `dim_info`, `var_info`), log-level transforms, unit
  conversion (`convert_units.py`), height/pressure-level interpolation (`height_to_pres_level`,
  `interpolate_to_height`), a derive-if-missing resolver that computes and can persist intermediate
  fields (`data_derived.py`, `io.save_derived`), and the extraction cache
  (`containers.clear_data_cache`, `tests/test_cache.py`).
- **Data Processing and Analysis: Data Access and Retrieval** — `gpigen` fetches Kp and F10.7 from
  the GFZ Potsdam JSON API or downloads and parses the GFZ `Kp_ap_Ap_SN_F107_since_1932.txt` file
  (`gpigen/sources.py`); `imfgen` retrieves OMNI 1-minute data either from CDAWeb's HAPI server via
  `hapiclient` (the default) or over FTP-TLS from `spdf.gsfc.nasa.gov` (`imfgen/sources.py`).
  Users invoke this through `generate_gpi` / `generate_imf` and the `gpigen` / `imfgen` console
  commands.
- **Data Processing and Analysis: Time Series Analysis** — `gpigen` computes 81-day centered or
  27-day trailing running averages of F10.7 (`gpigen/processing.py`); `imfgen` applies a 10-minute
  trailing average to the OMNI 1-minute series, detects fill-flag runs, and linearly interpolates
  gaps while flagging them in per-channel mask variables (`imfgen/processing.py`). On the model
  side, `arr_var_time`, `arr_lev_time`, `arr_lat_time` and `arr_lon_time` extract time series from
  history files.
- **Data Processing and Analysis: Data Reduction** — the same averaging operations reduce data
  volume while preserving the signal: OMNI 1-minute to a trailing-averaged series, F10.7 daily to a
  running average, and the `'mean'` / `'wmean'` level-collapse modes that reduce a 3-D field to 2-D
  (cos-latitude area-weighted; commit `b79ca5e`, `tests/test_wmean.py`).
- **Data Processing and Analysis: File Format Conversion** — `imfgen --source bcwind` reads a
  BCWIND HDF5 file and writes a NetCDF IMF file; the `asc` path converts OMNI ASCII to NetCDF;
  `gpigen` converts GFZ JSON or fixed-column text to NetCDF; and `--model waccmx` emits the WACCM-X
  (CESM) variant of both file types, which `docs/source/gcmprocpy/input_generation.rst` describes as
  reproducing "in one step, the files that were previously produced by a separate NCL/`ncrcat`
  conversion."
- **Models and Simulations** and **Models and Simulations: Physics-Based** — `data_oh.py` is a
  physics model, not a data reduction: it solves the coupled steady-state vibrational rate equations
  for OH levels v=0 through v=9 at every grid point and computes emission rates for all 39 Meinel
  bands, using HITRAN vibrational energies, Nelson et al. (1990) / Makhlouf (1999) Einstein A
  coefficients, Adler-Golden (1997) O2 quenching rates, N2 and O quenching rates with
  detailed-balance reverse terms, and the Klenerman & Smith and Kaye branching ratios for H+O3 and
  O+HO2 (ported from tgcmproc `ohrad.F`). `data_emissions.py` likewise forward-models 5.3 micron NO
  and 15 micron CO2 volume emission rates from temperature and composition. These synthesize
  observables that the parent model does not output.

Considered and rejected, with reasons — recorded so a future refresh does not re-propose them:

- **Coordinate Transforms** and **Coordinate Transforms: Ionospheric** — there is real
  coordinate-conversion code in the repository, but it is not a capability this software provides to
  users, which is the bar the classification requires. `plot_gen.py` defines
  `longitude_to_local_time()` and `local_time_to_longitude()`, and neither is exported from the
  package `__init__.py`; `local_time_to_longitude` is called nowhere in the repository at all, and
  `longitude_to_local_time` is called exactly once, internally, to assemble a plot-title string
  (`"LON=" … " SLT=" … "Hrs"`, `plot_gen.py:1385`). The remaining evidence is module-private:
  `_polar_ring_labels`, which labels the polar-stereographic boundary in solar local time computed
  from UT plus longitude (caption "SOLAR LOCAL TIME (HRS)", mirroring tgcmproc's IDL `labpol.pro`),
  and `_compute_gm_equator_lats`, which evaluates the World Magnetic Model through the `geomag`
  package to locate the geomagnetic equator for the `gm_equator` overlay exposed on `plt_lat_lon`,
  `mov_lat_lon` and the `-gmeq/--gm_equator` CLI flag. Reinforcing the rejection: gcmprocpy offers
  no AACGM, apex or quasi-dipole transforms, and the WMM evaluation is delegated entirely to a
  dependency and used only to place one overlay line on a map. The `geomag` dependency is recorded
  in Field 29, which is the right home for it.
- **Data Visualization: 3D Graphics** — no `mplot3d`, `Axes3D`, `vtk`, `mayavi` or `pyvista`
  anywhere; the only `imshow` call is `mov_gen.py` re-displaying saved PNG frames.
- **Data Visualization: Web-Based** — `ipympl` is declared so figures are interactive inside a
  Jupyter notebook, and the installation docs cover NCAR JupyterHub, but there is no plotly, bokeh,
  dash, server or dashboard. A notebook widget backend is not a web-based visualization product.
- **Data Visualization: Orbit Plots** — `plt_sat_track` plots the *variable* against along-track
  point index (1-D) or level versus along-track point (2-D contour). It never draws the trajectory
  itself, and the trajectory is supplied by the caller as arbitrary time/lat/lon arrays.
- **Data Visualization: Spectrogram** and **Data Processing and Analysis: Spectrogram**,
  **Wavelet Analysis**, **Energy Spectra** — no FFT, STFT, wavelet or spectral machinery of any
  kind.
- **Data Processing and Analysis: Data Assimilation** — nothing assimilates observations into a
  model state. `gpigen`/`imfgen` build *forcing* files consumed by a model run, which is input
  preparation, not assimilation.
- **Data Processing and Analysis: Calibration**, **Image Processing**, **Packet Decommutation**,
  **Curlometer**, **Plasma Moments**, **Pitch Angle Distributions**,
  **3D Particle Distribution Processing**, **Linear Gradient Estimation**,
  **Magnetic Null Finding**, **Wave Polarization Analysis**, **ML/AI**, **Field-line Tracing** —
  none present. gcmprocpy reads gridded model history files; there is no instrument data path, no
  particle distribution handling, no multi-spacecraft analysis, no field tracing and no machine
  learning.
- **Models and Simulations: Empirical** — the strongest candidate was the World Magnetic Model
  evaluation behind the geomagnetic-equator overlay, but that is delegated entirely to the `geomag`
  dependency and used only to position a line on a map, not offered as a model capability. The
  Kp-to-ap conversion (`gpigen/indices.py`) is the official 28-value lookup table, a definitional
  mapping rather than an empirical model.
- **Models and Simulations: First Principles**, **MHD**, **Forecasting**, **Data Guided**,
  **Forward-Fitting**, **Theory**, **Instrument Response**, **Observatory/Instrument Models**,
  **Mission-Specific**, **ML/AI** — gcmprocpy advances no state in time and solves no PDE on a grid;
  TIE-GCM and WACCM-X do that, and they are separate software (see Field 30).
- **Mission-related** (and all its subcategories) — gcmprocpy is not part of any mission ground
  system, pipeline or operations chain. It processes numerical model output.
- **Servers and Environments: High Performance Computing** — the repository does contain PBS batch
  scripts requesting 128 cores on NCAR Derecho (`benchmark/*.pbs`) and the installation guide covers
  Derecho, Casper and NASA Pleiades, but the package itself is single-process; `dask` is used only
  for lazy chunked reads, and there is no MPI, no domain decomposition and no HPC infrastructure
  code. The HPC fact is recorded in Field 21 (`HPC or HEC`), which is its correct home.
- **Servers and Environments: Software or Environment Container** — no Dockerfile, no Singularity
  definition, no container recipe.

### 5. Related Region (MANDATORY)

- Earth Atmosphere
- Earth Ionosphere
- Earth Lower and Middle Atmosphere
- Earth Thermosphere
- Interplanetary Space
- Solar Wind

- **Earth Atmosphere** — carried over from the existing HSSI record and independently supported:
  TIE-GCM and WACCM-X are both atmospheric general circulation models, and every field this package
  reads, derives or plots is an atmospheric state variable. It is retained alongside the three more
  specific Earth regions because HSSI's `Region` vocabulary is flat, so the specific values do not
  imply the broad one.
- **Earth Thermosphere** — TIE-GCM is the NSF NCAR thermosphere-ionosphere-electrodynamics general
  circulation model, and gcmprocpy's TIE-GCM variable defaults are thermospheric: `TN`,
  `UN`/`VN`/`WN` neutral winds, `O1`/`O2`/`N2`/`NO`/`N4S`/`HE` composition, `QJOULE`
  (`src/gcmprocpy/containers.py`). Height interpolation uses the TIE-GCM geopotential field `ZG`.
- **Earth Ionosphere** — the same defaults cover `NE`, `NMF2`, `HMF2`, `TEC`, `OP`, `TE`, `TI`,
  electric potential `POTEN` and the `UI_ExB`/`VI_ExB`/`WI_ExB` ion drifts; the WACCM-X defaults add
  `EDens`, `ElecColDens`, `Op`, `O2p`, `NOp`, `N2p` and the `ED1`/`ED2` electric fields.
- **Earth Lower and Middle Atmosphere** — WACCM-X spans the surface to the thermosphere, and
  gcmprocpy's WACCM-X defaults include surface and tropospheric fields (`TREFHT`, `FSDS`, `FSNS`,
  `FLNS`, `SWCF`, `LWCF`) and middle-atmosphere chemistry (`O3`, `CH4`, `H2O`, `N2O`, `HNO3`, `NOY`,
  `CLOY`, `BROY`). The Eliassen–Palm flux diagnostics quantify wave-mean-flow interaction, the OH
  Meinel airglow layer sits near the mesopause, and the 15 micron CO2 emission is the dominant
  mesosphere/lower-thermosphere infrared cooling term.
- **Solar Wind** — `imfgen` is a first-class part of the package (its own console command, its own
  documentation page, its own test suite). It reads OMNI 1-minute IMF `Bx`/`By`/`Bz` together with
  solar-wind proton density and flow speed, trailing-averages and gap-fills them, and writes them as
  boundary conditions. Solar-wind quantities are processed data products of this software, not just a
  passing mention.
- **Interplanetary Space** — supported by the same first-class `imfgen` capability:
  `gcmprocpy/src/gcmprocpy/imfgen/sources.py:35-36` maps the OMNI high-resolution IMF components and
  solar-wind plasma quantities, and `:301-317` retrieves the corresponding OMNI HAPI product. It was
  originally omitted as redundant to the more specific `Solar Wind` value. That premise was
  falsified on 2026-08-25: the Region vocabulary is flat, so neither value implies the other and an
  `Interplanetary Space` filter would otherwise miss this applicable capability. The value was added
  by user approval, resolving the dossier's prior self-contradiction while leaving the correct
  flat-vocabulary rationale for `Earth Atmosphere` intact.

Considered and rejected:

- **Earth Auroral Subregion** — there is circumstantial support (paired polar-stereographic panels
  covering absolute latitude 40 degrees and poleward, `QJOULE`, and WACCM-X's `QRS_AUR` auroral
  heating rate in the radiation variable group) but nothing auroral-specific: no auroral-oval
  boundary, no precipitation parameterization, no magnetic-latitude binning. gcmprocpy plots
  whatever the global model wrote.
- **Earth Magnetosphere** and its subregions — TIE-GCM's high-latitude electrodynamics is driven by
  magnetospheric convection (the Heelis and Weimer benchmark configurations), but that coupling
  happens inside the model. gcmprocpy neither models nor reads magnetospheric fields.

### 6. Authors (MANDATORY)

**Author 1: Nikhil Rao**
- **Author Identifier:** https://orcid.org/0000-0003-2639-9892
- **Affiliation 1:** NSF NCAR High Altitude Observatory — https://ror.org/03773p874
- **Affiliation 2:** NSF National Center for Atmospheric Research — https://ror.org/05cvfcr44

Carried over from the existing HSSI record, and independently corroborated on every
element. `gcmprocpy/pyproject.toml` and `gcmprocpy/setup.py` name `Nikhil Rao <nikhilr@ucar.edu>` as
sole author; `docs/source/conf.py` sets `author = 'Nikhil Rao'`; the PyHC community registry lists
Nikhil Rao as contact; and the LICENSE closes with "This software was written by Nikhil Rao for US
National Science Foundation National Center for Atmospheric Research (NSF NCAR)." The ORCID and both
affiliations are confirmed by the NCAR-TIEGCM Zenodo record (10.5281/zenodo.20076375), where
"Rao, Nikhil" carries ORCID 0000-0003-2639-9892 and the affiliation "High Altitude Observatory, NSF
National Center for Atmospheric Research, Boulder, CO, USA" — i.e. exactly the two organizations
already stored. Both RORs verify: 03773p874 is "NSF NCAR High Altitude Observatory" (acronym HAO,
alias "High Altitude Observatory") and 05cvfcr44 is "NSF National Center for Atmospheric Research".

No second author is added. Git history shows three committer identities, all the same person:
`cookieenick <nikhilr@ucar.edu>` (115 commits),
`Nikhil Rao <44057004+AnonNick@users.noreply.github.com>` (42) and
`AnonNick <nikhilrao8@gmail.com>` (2). There are no other contributors, no `AUTHORS` or
`CONTRIBUTORS` file, and no co-authored commits.

The affiliation name recorded here, "NSF NCAR High Altitude Observatory", is ROR's display name for
03773p874. An earlier form, "NCAR High Altitude Observatory", is superseded and should not be
reintroduced: ROR registers no such name for this organization — only the display name, the acronym
HAO and the alias "High Altitude Observatory" — and it leaves the NCAR acronym unexpanded, which the
field guidance discourages. The ROR remains the stable identifier for this affiliation and is
unaffected by the wording. Note that the organization name is a value shared with other HSSI
records, so any future question about its wording is a question about that shared organization
rather than about this record alone.

### 7. Software Name (MANDATORY)
GCMprocpy

Field 7 asks for the name "as listed on the code repository", and the repository's own
human-readable listing — the GitHub repository description — reads "GCMprocpy is a tool used for
TIE-GCM and WACCM-X post processing and analysis." The same form is the H1 of the rendered
documentation homepage (`docs/source/index.rst`), the `name:` value in the PyHC community registry
entry, and the opening sentence of both READMEs: the top-level `README.md` ("GCMprocpy is a
post-processing and plot generation tool for TIE-GCM and WACCM-X NetCDF output.") and the package
`gcmprocpy/README.md` ("GCMprocpy is a tool used for TIE-GCM and WACCM-X post processing and plot
generation.").

This corrects the previously stored value `gcmprocpy`. That spelling is real, but it is the machine
identifier rather than the display name: it is the PyPI distribution name, the import name, the CLI
entry-point name, `[project] name` in `pyproject.toml`, and `project = 'gcmprocpy'` in the Sphinx
configuration. The stored record was also self-inconsistent, pairing the name `gcmprocpy` with its
own description beginning "GCMprocpy is…" — the display name and the identifier had been conflated.

Two further variants exist and are rejected:

- **`GCMPROCPY`** — the all-caps `README.md` H1 (`# GCMPROCPY`). This is heading styling only; the
  next line of prose in the same file writes `GCMprocpy`.
- **`GCMProcPy`** — appears only as the Qt GUI window title and the main-window docstring
  (`src/gcmprocpy/gui/gcmprocpy.py:242,257`). A single in-code UI string does not outweigh the
  repository description, the documentation homepage and the registry entry.

One nuance worth recording so it is not later mistaken for counter-evidence: the Sphinx
documentation is itself inconsistent, and lowercase is in fact the more common form inside it. Only
`docs/source/gcmprocpy/index.rst` uses `GCMprocpy` consistently in prose (all five occurrences). The
Sphinx root `docs/source/index.rst` titles itself `GCMprocpy` in the H1 and the toctree caption, but
its single prose sentence uses lowercase `gcmprocpy`. `usage.rst` is predominantly lowercase in prose
with one `GCMprocpy` sentence. The eight per-function subpages (`plot_functions.rst`,
`data_functions.rst`, `installation.rst`, `requirements.rst`, `movie_functions.rst`,
`postproc_functions.rst`, `file_structure.rst`, `input_generation.rst`) contain no mixed-case
occurrence at all.

That internal inconsistency does not disturb the choice, because none of those files is the listing
Field 7 asks about. The value rests on the sources that present the software to a human reader as a
named product — the GitHub repository description, the rendered documentation homepage H1, the PyHC
registry `name:` field, and both READMEs' opening sentences — and those agree on `GCMprocpy`.

### 8. Description (MANDATORY)

GCMprocpy is a post-processing and plot generation tool for TIE-GCM and WACCM-X NetCDF output. It provides three interfaces (a PySide6 desktop GUI, a Python API, and one console command per plot type) and produces latitude-longitude maps in several projections with optional coastline, nightshade and wind-vector overlays, vertical cross-sections, time series, and fields interpolated along a satellite track. Supporting functions convert units, interpolate between pressure level and geometric height, and compute derived quantities including the NO, CO2 and OH band emission rates ported from the legacy tgcmproc processor. Its gpigen and imfgen commands also build the geophysical-index and IMF/solar-wind NetCDF files that drive a model run.

This replaces the previously stored one-line description, which read:

> GCMprocpy is a tool used for TIE-GCM and WACCM-X post processing and plot generation.

That sentence is accurate but did no work in the record. It was byte-identical to the stored Concise
Description, so the same 85 characters appeared twice and Field 9 — whose purpose is to supply an
alternate preview when the description's opening does not serve — had nothing to distinguish itself
from. The one-liner also predated substantial capability: `gpigen` and `imfgen`, which generate model
*input* files rather than post-process output, were vendored in at v1.5.0 (commit `e4c249a`,
2026-06-11); satellite-track interpolation arrived at v1.4.0; and the derived-variable registry and
the OH Meinel band model are likewise invisible in "post processing and plot generation". A user
reading only the stored sentence would not learn that this package also writes the GPI and IMF
forcing files that drive a TIE-GCM or WACCM-X run.

The expansion is deliberately conservative — a summary of about 745 characters, not a feature
inventory. Earlier drafting produced a version roughly twice this length that enumerated every map
projection, every overlay, every cross-section and time-series axis pair, both height fields, and the
output file formats; that level of detail belongs in the documentation, and a description that long
stops functioning as a description. The recorded version names the plot *families* rather than their
variants, and omits the output formats entirely (figures as raster or PDF, sequences as MP4) because
Field 19 already records them.

Editorial intent is preserved rather than overwritten. The opening sentence is the maintainer's own
current wording, taken verbatim from the top-level `README.md`, and it stands alone within the first
150-200 characters that HSSI uses as the preview. The maintainer's original submitted sentence is
retained verbatim as the Concise Description (Field 9). Every remaining clause is supported by
`README.md` (its "three modes", Plot Types, Features and Input File Generation sections),
`docs/source/gcmprocpy/*.rst`, or the code those documents describe — the expansion introduces no
claim the repository does not already make.

The alternative of retaining the stored one-liner unchanged was considered and rejected. It is
defensible under a strict "respect submitted values" reading, but it leaves both description fields
identical and the record materially incomplete about what the software now does.

### 9. Concise Description (OPTIONAL)
GCMprocpy is a tool used for TIE-GCM and WACCM-X post processing and plot generation.

Kept verbatim from the existing HSSI record. At 85 characters it is inside the 200-character limit
and is a genuinely good preview: it names the tool, the two models and the two headline activities.
This is the maintainer's own submitted wording and is deliberately not reworded.

Its former byte-identity with the stored Description is resolved by expanding Field 8 rather than by
shortening or rewriting this field — which is what Field 9 is for ("If the first 150-200 characters
of the description do not provide the desired preview, you may enter an alternate text here").

### 10. Publication Date (RECOMMENDED)
2024-10-28

Field 10 is "Date of first broadcast/publication ... Used for the initial version of the software."
The first public release of the software under the name gcmprocpy is PyPI `gcmprocpy` 1.0.0,
uploaded **2024-10-28T16:04:07Z**.

This corrects the previously stored `2025-03-10`, which is the upload date of PyPI `gcmprocpy`
**1.2.0** — the version that happened to be current when the HSSI record was created. It is a
then-current-release date recorded in a first-publication field, and no source supports it as a
first publication under any reading.

Four candidate dates were weighed:

| Date | What it is | Verdict |
|---|---|---|
| 2023-10-18 | First release of the predecessor, PyPI `tiegcmpy` 1.0.0; also the date of this repository's first commit, "Moved tiegcmpy to tiegcm3.0" | Rejected. The same codebase, but published under a different name. Field 7 identifies this record as GCMprocpy, so this is the predecessor's publication date, not this record's. It would be the right answer only for a record that identified the software as tiegcmpy. |
| 2024-05-07 | GitHub repository creation | Rejected. Repository creation is not publication; the code was already released on PyPI as tiegcmpy nearly seven months earlier. |
| **2024-10-28** | PyPI `gcmprocpy` 1.0.0, the first release bearing this name | **Recorded.** First publication of the software as named and identified by this record. |
| 2025-03-10 | PyPI `gcmprocpy` 1.2.0 | Rejected; previously stored. Not a first publication. |

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

Field 11 is explicit for this case: "If no DOI has been obtained, indicate the repository host, such
as GitHub or GitLab." gcmprocpy has no DOI (Field 2), and the repository is hosted on GitHub under
the NCAR organization. `GitHub` with identifier `https://github.com` is the established form of that
organization's name and identifier, so those exact strings are recorded rather than a variant
spelling that would sit alongside them as a near-duplicate.

Alternatives considered. **PyPI** is where the distribution is actually served from, and one could
argue it publishes the released artifact — but the field names the *repository host* as the
fallback, and the source repository is on GitHub. **NSF National Center for Atmospheric Research**
was considered on the strength of the LICENSE copyright line ("Copyright 2024 US National Science
Foundation National Center for Atmospheric Research (NSF NCAR)"); it is the copyright holder and the
author's institution, which the field guidance does not equate with publisher. **Zenodo** does not
apply — no DOI has been minted.

### 12. Version (RECOMMENDED)
- **Version Number:** 1.5.2
- **Version Date:** 2026-07-01
- **Version Description:** Adds a `--model waccmx` option to both input-file generators, so gpigen and imfgen emit the WACCM-X (CESM) formats directly: unlimited time dimension, `date`/`datesec`, and a 3-hourly `ap` series derived from Kp via the official lookup table. Adds a derive-if-missing resolver with in-place NetCDF persistence for intermediate fields, the `RHO`, `PMB` and `TNFP` derivables and the `OX`/`NOZ`/`HOX` composition groups and O/CO2 ratios ported from tgcmproc `mkderived.F`, cosine-latitude area-weighted `wmean` averaging, and WACCM-X hybrid-pressure support in the density conversions. Fixes the EP flux divergence mass density and raises a chain-aware error naming the missing dependency when a derivable cannot be computed.
- **Version PID:** Not found — no DOI exists for gcmprocpy or for any of its releases (see Field 2).

Three sources agree on the number: `version = "1.5.2"` in `gcmprocpy/pyproject.toml` and
`version='1.5.2'` in `gcmprocpy/setup.py` at the recorded revision, and PyPI `gcmprocpy` 1.5.2. The
version date is the release date under both available readings, so there is nothing to reconcile:
the annotated git tag `v1.5.2` ("Release 1.5.2") was created 2026-07-01 17:25:57 UTC and the PyPI
upload followed at 2026-07-01 17:29:20 UTC.

The version number is recorded bare, as `1.5.2`. The git tag carries a `v` prefix (`v1.5.2`) and the
field's example shows `v1.0.0`, but `pyproject.toml` and PyPI both use the bare form, and the number
is displayed with the software name prefixed to it — so a prefix carried inside the value itself
would be duplicated on display.

The version description is derived from the fifteen commits after the 1.5.1 bump (`26cdbcf`,
2026-06-11) and the 1.5.2 bump (`456398e`, 2026-07-01). There is no `CHANGELOG.md` in the repository
and no GitHub release notes — the repository has published zero GitHub Releases — so the git log is
the only available account of what changed.

**Documented upstream inconsistency: `docs/source/conf.py` declares `release = '2.0.0'`.** Anyone
who consults the rendered documentation and sees "2.0.0" should know that this is not a version of
gcmprocpy. The string was set by the docs-only commit `d7a6539` ("Updated docs with autodocs",
2024-06-27), which bumped it from `1.0.1` while the project was still named tiegcmpy, and it has
never tracked a real release since. Every authoritative source says 1.5.2: `pyproject.toml`,
`setup.py`, the git tag `v1.5.2`, and PyPI. There are no GitHub Releases to contradict them, and the
published documentation is versioned by Read the Docs from the branch rather than from that string.

### 13. Programming Language (RECOMMENDED)
Python 3.x

Carried over from the existing HSSI record and confirmed: `requires-python = ">=3.8"` with
`Programming Language :: Python :: 3.8` through `3.12` classifiers, and CI running the test suite on
3.9 through 3.12.

GitHub's language statistics report Jupyter Notebook as the largest language by bytes (16.3 MB
against 756 KB of Python), but that is entirely the four example notebooks under
`docs/source/gcmprocpy/notebooks/` with their embedded output images — documentation, not
implementation, and in any case the Programming Language vocabulary offers no value for Jupyter
Notebook. The 4.4 KB of Shell that GitHub also reports is the six tcsh/PBS batch scripts in
`gcmprocpy/benchmark/`; no applicable Shell value is available either, and the field asks only for
"the most important languages", which for this package is Python alone.

### 14. Reference Publication (RECOMMENDED)
Not found.

No publication describes gcmprocpy. The repository has no `CITATION.cff`, no citation section in
either `README.md`, and no paper reference in the docs. The papers that appear in adjacent searches
describe other things: "The NCAR-TIEGCM Version 3.0" (10.1029/2025JA034219, *JGR: Space Physics*,
September 2025), of which Nikhil Rao is a co-author, describes **TIE-GCM**, and Volland's
*Atmospheric Tidal and Planetary Waves* (cited in `data_epflux.py`) is the theoretical reference for
the EP flux formulation. Neither is a reference publication for this tool. See Field 27 for the
related-publication search.

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** https://spdx.org/licenses/Apache-2.0

Four sources agree: the root `LICENSE` file is the verbatim Apache License 2.0 text with the
copyright line "Copyright 2024 US National Science Foundation National Center for Atmospheric
Research (NSF NCAR)"; `pyproject.toml` declares `license = "Apache-2.0"`; the PyPI metadata carries
`license_expression: Apache-2.0`; and the GitHub API reports `spdx_id: Apache-2.0`. SoMEF
independently resolved the same SPDX identifier.

`Apache License 2.0` is the exact controlled value for this license in HSSI's vocabulary, and
`https://spdx.org/licenses/Apache-2.0` is the SPDX URI that vocabulary pairs with it, so both halves
are recorded in their canonical form and no near-miss variant is introduced. The URL printed inside
the LICENSE file
itself (`http://www.apache.org/licenses/LICENSE-2.0`) was not used, in favour of the SPDX URI the
vocabulary already carries.

Note that PyPI's legacy `license` field is `null` for this project — only the newer
`license_expression` is populated — so a tool reading the old field alone would wrongly conclude
there is no license.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- TIEGCM
- waccm-x
- general circulation model
- thermosphere
- ionosphere
- mesosphere
- upper atmosphere
- whole atmosphere
- model output
- post-processing
- netcdf
- data visualization
- plotting
- python
- airglow
- geophysical indices
- kp index
- f10.7
- IMF
- solar wind
- omni
- interpolation
- satellite flythrough

Keywords are the one open vocabulary in the form, so an unrecognised value is accepted rather than
rejected — which makes near-duplicate wording the real hazard. All but two of these reuse terms
already established in HSSI's keyword vocabulary, and are written with the established capitalization
(`TIEGCM`, `IMF`) so that the recorded text matches those terms exactly rather than differing from
them only in case.

Two values are new to the vocabulary: **`waccm-x`** and **`post-processing`**. On `waccm-x`: a
`waccm` term already exists, but WACCM-X (the thermosphere-ionosphere extension) is a distinct model
from WACCM, and the accurate term is worth adding rather than associating this record with the wrong
model. On `post-processing`: it is the defining activity of this package and one of its own declared
PyPI keywords, and no established term covers it.

Provenance of the selections: `TIE-GCM`, `WACCM-X`, `atmospheric-science`, `post-processing` and
`visualization` are the package's own `keywords` in `pyproject.toml`;
`ionosphere_thermosphere_mesosphere`, `2D_graphics`, `plotting`, `netcdf`, `local`, `data_analysis`
and `specific` are the PyHC community registry's curated keywords for this entry; the rest name
capabilities documented above (`airglow` for the OH Meinel and NO/CO2 emission models,
`geophysical indices` / `kp index` / `f10.7` for gpigen, `IMF` / `solar wind` / `omni` for imfgen,
`interpolation` for the height and track interpolation, `satellite flythrough` for `arr_sat_track` /
`plt_sat_track`).

Deliberately not included: `ionosphere_thermosphere_mesosphere` and
`ionosphere thermosphere mesosphere`, both of which are established terms but are PyHC taxonomy
tokens made redundant here by the separate `thermosphere`, `ionosphere` and `mesosphere` keywords;
`atmospheric-science` and `atmospheric modelling`, which would add nothing over
`general circulation model` and `whole atmosphere`; `space weather`, which is arguably supported by
the storm-benchmark plotting scripts but is broad enough to be uninformative here; `visualization`,
covered by `data visualization` and `plotting`; and `World Magnetic Model`, which is an established
term but would over-weight a single overlay feature.

### 17. Data Sources (OPTIONAL)

- CDAWeb
- FTP/FTPS Directories
- GFZ
- HAPI
- HTTP/HTTPS Directories
- OMNIWeb
- Other

- **HAPI** and **CDAWeb** — `imfgen`'s default OMNI access mode calls `hapiclient`'s `hapi()`
  against CDAWeb's HAPI server for the `OMNI_HRO_1MIN` dataset, retrieving only the requested window
  (`imfgen/sources.py: omni_samples_hapi`; `imfgen/core.py` defaults `omni_access="hapi"`;
  documented in `docs/source/gcmprocpy/input_generation.rst`).
- **FTP/FTPS Directories** — the `asc` access mode opens an `ftplib.FTP_TLS` connection to
  `spdf.gsfc.nasa.gov`, changes to `/pub/data/omni/high_res_omni/`, lists `omni_min*.asc`, and
  downloads with a staleness check against the remote `MDTM` (`imfgen/sources.py:
  download_omni_files`).
- **OMNIWeb** — the data product retrieved by both of the above is OMNI high-resolution 1-minute
  data; `README.md` and the input-generation docs link `https://omniweb.gsfc.nasa.gov/ow_min.html`
  as its reference.
- **GFZ** — `gpigen` queries `https://kp.gfz.de/app/json/` for the `Fobs` (F10.7 observed) and `Kp`
  indices (`gpigen/sources.py: _fetch_json`, the default source).
- **HTTP/HTTPS Directories** — `gpigen`'s `textfile` source downloads
  `https://kp.gfz.de/app/files/Kp_ap_Ap_SN_F107_since_1932.txt` with `requests.get` and parses it
  locally (`gpigen/sources.py: _download_textfile`, `parse_textfile`).
- **Other** — the package's primary input is a local directory of TIE-GCM or WACCM-X NetCDF history
  files, or a single BCWIND HDF5 file, supplied by the user from their own model run
  (`io.load_datasets`; `imfgen --source bcwind`). No listed source covers locally held files, and the
  field instructs "If a source is not listed, select 'Other'." The PyHC registry independently tags
  this entry `local`.

**Observatory/Mission-specific** is deliberately not selected. Field 17 pairs that value with a
named entry in Related Observatories, and Fields 31-32 are correctly empty for this software (see
below); selecting it would assert an observatory association that does not exist.

### 18. Input File Formats (RECOMMENDED)

- ascii
- HDF5
- JSON
- netCDF3/4

- **netCDF3/4** — the format of every TIE-GCM and WACCM-X history file the package reads;
  `io.load_datasets` opens `*.nc` with `xarray.open_dataset(chunks='auto')` and distinguishes the two
  models from `ds.lev.units`.
- **HDF5** — `imfgen --source bcwind` reads a BCWIND HDF5 file through `h5py`
  (`imfgen/sources.py: bcwind_samples`; `h5py` is a declared dependency and the docs state that
  "`imfgen` depends on `h5py` (BCWIND)").
- **ascii** — the OMNI `omni_min<year>.asc` fixed-column files are parsed with `np.loadtxt`
  (`imfgen/sources.py: load_omni_year`), and the GFZ `Kp_ap_Ap_SN_F107_since_1932.txt` file is
  parsed line by line (`gpigen/sources.py: parse_textfile`).
- **JSON** — the GFZ index API returns JSON, which `gpigen` parses via `resp.json()`
  (`gpigen/sources.py: _fetch_json`). This arrives over HTTP rather than from a file on disk; it is
  included because it is a genuine input encoding the software parses, and no other field records it.

**CDF** was considered and rejected: OMNI is distributed as CDF on CDAWeb, but gcmprocpy never
touches a CDF file — the HAPI transport hands `hapiclient` decoded arrays. **csv** was rejected for
the same reason: HAPI's wire format may be CSV, but that is negotiated inside `hapiclient` and is not
a format this package supports for input.

### 19. Output File Formats (RECOMMENDED)

- netCDF3/4
- Other

- **netCDF3/4** — `gpigen.save_gpi` and `imfgen.save_imf` write NetCDF files (the GPI file of
  `year_day`/`f107d`/`f107a`/`kp`, and the IMF file of `bx`/`by`/`bz`/`swden`/`swvel` with
  per-channel quality masks), in either the TIE-GCM or the WACCM-X layout. `io.save_derived`
  additionally appends computed variables into an existing history file in place through
  `netCDF4.Dataset(path, 'a')`.
- **Other** — the package's most visible output is figures and movies, and the vocabulary offers no
  more specific image or video format, so `Other` is the only way to record them.
  `io.save_output` passes the caller's format string straight to `Figure.savefig`, the per-plot
  console commands default to `jpg`, the interactive `main.py` offers `jpeg`/`pdf` plus multi-page
  PDF collection via `PdfPages`, and `mov_gen.mov_lat_lon` writes `.mp4`.

**HDF5** was considered and rejected. NetCDF-4 is physically an HDF5 container, so a technically
true claim could be made, but the package writes through the NetCDF API and never produces a file a
user would describe as HDF5 output; asserting it would misrepresent the interface. HDF5 remains
correctly listed as an *input* format, where the BCWIND reader justifies it.

### 20. Operating System (RECOMMENDED)
Linux

Linux is the only operating system with positive evidence. CI runs lint and the full test suite on
`ubuntu-latest` across Python 3.9 through 3.12 (`.github/workflows/ci.yml`); Read the Docs builds on
`ubuntu-22.04` (`.readthedocs.yaml`); and every path in `docs/source/gcmprocpy/installation.rst` is
Linux — the Miniconda **Linux** installer, NCAR Derecho and Casper, and NASA Pleiades. The GUI
section of `README.md` adds "Requires an X11-capable session (`ssh -X` for remote use)".

macOS and Windows are deliberately not claimed. The package is pure Python and every dependency
(cartopy, matplotlib, netCDF4, h5py, PySide6, scipy) publishes macOS and Windows wheels, so it very
probably installs on both — but "very probably" is not evidence, the field asks for systems the
software "can successfully be installed on", there is no CI coverage, no documentation and no
classifier for either, and the X11 instruction points the other way. `Operating System Independent`
was rejected for the same reason: it would assert untested breadth. If the maintainer confirms macOS
or Windows use, those values should simply be added.

### 21. CPU Architecture (RECOMMENDED)

- HPC or HEC
- x86-64

- **x86-64** — the only architecture with evidence: GitHub's `ubuntu-latest` runners are x86-64, and
  the three documented deployment targets (NCAR Derecho, NCAR Casper, NASA Pleiades) are all x86-64
  clusters.
- **HPC or HEC** — the installation guide devotes a section each to NCAR Derecho/Casper and NASA
  Pleiades, including module loads and PBS interactive-session recipes, and
  `gcmprocpy/benchmark/*.pbs` are real batch scripts (`#PBS -l select=1:ncpus=128:mpiprocs=128`,
  `walltime=12:00:00`, the `ncarenv/23.09` module stack, `TGCMDATA` on `/glade/campaign`) that run
  the benchmark plotting jobs on Derecho. Running under an HPC scheduler is a documented, exercised
  deployment mode.

`Apple Silicon arm64` and `Linux aarch64 or arm64` were rejected — no evidence of either.
`CPU Independent` was considered, since the package contains no compiled code of its own, but its
dependency stack (cartopy/GEOS, netCDF4, h5py, PySide6, scipy) is compiled and only x86-64 has been
exercised, so the claim would outrun the evidence. `GPU` does not apply: no CUDA, no CuPy, no
GPU-aware array library.

### 22. Related Phenomena (OPTIONAL)

- Geomagnetic Storms
- Solar Wind

`Phenomena` is a closed vocabulary despite the form's free-text affordance, so anything not on the
list belongs in Keywords instead.

- **Geomagnetic Storms** — `gcmprocpy/benchmark/storms_singleut.py`, `storms_utlat_full.py` and
  `storms_utvert_full.py` are purpose-built plotting drivers for TIE-GCM's storm benchmark suite,
  iterating over `dec2006_heelis_gpi`, `dec2006_weimer_imf`, `jul2000_heelis_gpi`,
  `jul2000_weimer_imf`, `nov2003_heelis_gpi`, `nov2003_weimer_imf`, `whi2008_heelis_gpi` and
  `whi2008_weimer_imf` — the July 2000, December 2006 and November 2003 storm cases, in their
  Heelis-GPI and Weimer-IMF driver configurations. `gpigen` and `imfgen` produce exactly the GPI and
  IMF forcing files those storm configurations consume.
- **Solar Wind** — `imfgen` reads, averages, gap-fills and writes solar-wind IMF components, proton
  density and flow speed as a primary function (see Field 5).

The other values the vocabulary offers (`Coronal Heating`, `Coronal Mass Ejections`, `Solar Corona`,
`Solar Flares`, `X-ray emission`) do not apply: gcmprocpy handles no solar or coronal data. The
airglow and infrared emissions it models (OH Meinel bands, 5.3 micron NO, 15 micron CO2) are
terrestrial upper-atmosphere emissions, not the solar `X-ray emission` the vocabulary means — which
is why `airglow` is carried in Keywords instead.

### 23. Development Status (RECOMMENDED)
Active

repostatus.org defines `Active` as "reached a stable, usable state and being actively developed",
which describes this repository on both halves. Stable and usable: twelve PyPI releases, a tagged
1.5.2, a documented Python API, CLI and GUI, published docs on Read the Docs, and a test suite of
about thirty files run in CI on four Python versions. Actively developed: 159 commits, the most
recent 2026-07-01 — one month before this extraction — with substantive feature work through 2026
(WACCM-X input formats, the derive-if-missing resolver, HAPI access, satellite-track interpolation),
and the GitHub repository is not archived.

The PyPI classifier says `Development Status :: 4 - Beta`, which is a different vocabulary and does
not map onto `WIP` here: `WIP` means "no stable, usable public release yet", and there have been
twelve. `Inactive`, `Unsupported` and `Abandoned` are all contradicted by the commit and release
cadence. PyHC's curated ratings for this entry corroborate the choice — `software_maturity: Good`,
`documentation: Good`, `license: Good`, with `testing: Requires improvement` and
`community: Partially met` — a maturing but working package, not a work in progress.

### 24. Documentation (RECOMMENDED)
https://gcmprocpy.readthedocs.io/

Carried over from the existing HSSI record and confirmed live (it resolves to
`https://gcmprocpy.readthedocs.io/en/latest/`). The same target appears as
`[project.urls] Documentation` in `pyproject.toml`, in both `README.md` files, and in the PyHC
registry entry.

Two variants were rejected in favour of the stored value: `https://gcmprocpy.readthedocs.io`
(without the trailing slash — the form used in `pyproject.toml` and PyHC; identical target, so
changing the stored value would be pure churn) and
`https://gcmprocpy.readthedocs.io/en/latest/index.html` (the GitHub repository's `homepage` field —
version-pinned and page-specific, so a worse canonical entry point). The documentation covers
installation, requirements, usage, plot functions, movie functions, data functions, post-processing
functions, input generation and file structure, plus four example notebooks, so it satisfies the
field's "including installation instructions" requirement.

### 25. Funder (OPTIONAL)
Not found.

This field is deliberately empty, and the emptiness is a settled conclusion rather than an
unexplored gap. The repository contains no funding acknowledgement, no award number, no `NOTICE`
file and no acknowledgements section anywhere in the code or the documentation. Two candidate
funders were researched and both were rejected, because neither is convincing evidence of direct
grant support for *this software's* development. Their evidence is preserved in full so a future
refresh does not re-propose them without new information.

**Candidate A — U.S. National Science Foundation** (ROR `https://ror.org/021nxhr62`). Evidence: the
`LICENSE` file states "Copyright 2024 US
National Science Foundation National Center for Atmospheric Research (NSF NCAR)" and "This software
was written by Nikhil Rao for US National Science Foundation National Center for Atmospheric Research
(NSF NCAR)", and NSF NCAR is an NSF federally funded research centre managed by UCAR. Rejected
because the LICENSE line establishes the author's institutional home and employer — and the
copyright holder — rather than a funding award for this package. Treating an employer's sponsor as
the software's funder is an inference, not a record.

**Candidate B — National Aeronautics and Space Administration** (ROR `https://ror.org/027ka1x80`).
Evidence: the abstract for "Advancing Space Weather Research with kaipy and gcmprocpy: Analysis,
Metrics, and Tutorials" at the 106th AMS Annual Meeting states that "The NASA DRIVE Center for
Geospace Storms (CGS) has developed two complementary Python software packages — kaipy and
gcmprocpy". CGS is a NASA DRIVE Science Center led by the Johns Hopkins Applied Physics Laboratory
and supported by NASA's Heliophysics Division, with NSF NCAR among its partners. Rejected because
this is a programmatic attribution rather than an award supporting this package's development: it
names no award, it appears in a conference abstract rather than in the repository, and the abstract's
author list could not be retrieved (the AMS Confex page renders client-side).

No award number was verifiable from any source for either candidate — CGS papers cite more than one
identifier, so quoting any of them here would risk recording a number that does not apply. The two
readings are not mutually exclusive; NSF institutional support and NASA CGS project support could
both be true. Recording either without an award would assert a funding relationship the sources do
not establish, which is why Field 26 is correspondingly empty as well.

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

Empty for the same reason as Field 25: no award title or number appears anywhere in the repository.
The two NCAR project codes in the batch scripts and installation docs — `P28100036` in
`gcmprocpy/benchmark/*.pbs` and `P28100045` in `docs/source/gcmprocpy/installation.rst` — were
considered and rejected: those are NCAR HPC allocation account codes charged for compute time on
Derecho and Casper, not funding award numbers, and the docs present the second one purely as a
placeholder ("replace with your own"). Note for any future attempt: an Award Title value is capped at
128 characters, so a long official award title must be checked against that limit first.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found.

Negative research, recorded so it is not repeated. There is no `CITATION.cff`, no citation section in
either `README.md`, and no publication reference in `docs/`. Three candidates were examined and none
qualifies:

- **"The NCAR-TIEGCM Version 3.0"** (10.1029/2025JA034219, *JGR: Space Physics*, September 2025;
  Nikhil Rao is the fifth of 24 authors). It describes TIE-GCM v3.0, not gcmprocpy. Its full text
  could not be checked for a gcmprocpy citation — the AGU page returns 403 to automated fetches — so
  whether it cites this tool is genuinely unknown. Since the companion Zenodo record does point
  readers at gcmprocpy for post-processing, this is worth one manual look during a future refresh; if
  the paper's software-availability statement names gcmprocpy, it becomes a valid entry here.
- **"Advancing Space Weather Research with kaipy and gcmprocpy: Analysis, Metrics, and Tutorials"**,
  106th AMS Annual Meeting (2026). This one genuinely is about gcmprocpy, but it is a conference
  abstract with no DOI, and the field's fallback requires an APA citation with a permanent link — the
  AMS Confex program URL is neither permanent nor retrievable in full (the page loads its content
  client-side, so the author list could not be captured). Omitted rather than recorded with a
  half-known citation.
- **"Advancing Heliophysics and Space Weather Modeling through Open Science"** (Corti et al.,
  10.1029/2025SW004922, *Space Weather*, 2026; arXiv:2605.30626). A community open-science strategy
  paper; its abstract does not mention gcmprocpy, and it is not a publication about this software.

Volland's *Atmospheric Tidal and Planetary Waves* (cited in `data_epflux.py`) and the spectroscopic
references in `data_oh.py` (Nelson et al. 1990, Makhlouf 1999, Adler-Golden 1997, Klenerman & Smith,
Kaye) are sources for the implemented physics, not publications about the software.

### 28. Related Datasets (OPTIONAL)

- https://doi.org/10.5880/Kp.0001
- https://hpde.io/NASA/NumericalData/OMNI/HighResolutionObservations/Version1/PT1M

Both are datasets this software directly reads and processes, which is what Field 28 asks for
("Datasets the software supports functionality for").

- **Geomagnetic Kp index** — DataCite confirms 10.5880/Kp.0001 as "Geomagnetic Kp index", Matzka,
  Bronkalla, Tornow, Elger & Stolle, GFZ Data Services, 2021. This is the dataset behind both of
  `gpigen`'s sources: the `https://kp.gfz.de/app/json/` API queried with `index=Kp`, and the
  `Kp_ap_Ap_SN_F107_since_1932.txt` file whose columns 7 to 15 `parse_textfile` reads as the eight
  three-hourly Kp values per day. `gpigen/indices.py` then derives `ap` from Kp via the official
  28-value table for the WACCM-X output format.
- **OMNI High Resolution 1-minute data** — the dataset `imfgen` reads under both access modes: as
  `OMNI_HRO_1MIN` from CDAWeb's HAPI server, and as the SPDF `omni_min<year>.asc` files, which the
  docs confirm "draw on the same underlying product (the same variables, fill values and 1-minute UTC
  grid)". The dataset has no DOI; the hpde.io SPASE landing page is used instead, which is the form
  Field 28's own example prescribes for datasets without one, and it resolves.

Considered and not included: the **F10.7 solar radio flux** series, which `gpigen` fetches as `Fobs`
from the same GFZ endpoints — GFZ redistributes it rather than publishing it, and no separate DOI
covers the redistribution, so the Kp DOI above already stands for that request path. **TIE-GCM and
WACCM-X history files**, the package's primary input, are not a published dataset: they are output
from the user's own model run, with no DOI and no archive landing page. The **TIE-GCM benchmark runs**
that `gcmprocpy/benchmark/*.py` plot are distributed by NCAR HAO but as part of the model release
rather than as a citable dataset.

### 29. Related Software (OPTIONAL)

- https://www.hao.ucar.edu/modeling/tgcm/tiegcm2.0/userguide/html/postproc.html — **tgcmproc**
- https://pypi.org/project/tiegcmpy/ — **tiegcmpy**
- https://github.com/nasa/Kamodo — **Kamodo**
- https://github.com/hapi-server/client-python — **hapiclient**
- https://github.com/cmweiss/geomag — **geomag**

All five URLs resolve and all are well inside HSSI's 200-character URL limit.

- **tgcmproc** — the direct predecessor: NCAR HAO's legacy TIE-GCM post-processor, comprising the
  Fortran 90 batch processor `tgcmproc_f90` and the IDL GUI `tgcmproc_idl`. gcmprocpy is
  substantially a port of it, and says so throughout: `data_epflux.py` is a "Port of tgcmproc
  `epflux.F` (B. Foster and Hanli Liu, 2-4/98)", `data_oh.py` a "Port of tgcmproc `ohrad.F`
  (B. Foster, U. B. Makhlouf, SDL/Stewart Radiance Lab)", `data_emissions.py` is "Ported from
  tgcmproc `mkemiss.F`", the `RHO`/`PMB`/`TNFP` derivables come from `mkderived.F`, the density
  conversions from `denconv.F`, and `_polar_ring_labels` "Mirrors the tgcmproc IDL `labpol.pro`
  look". Commit `f152181` exists specifically to "Reference tgcmproc provenance (file, subroutine,
  author) in ported physics docstrings and docs". tgcmproc has no public repository or DOI; the URL
  given is the TIE-GCM user guide page that documents the tools, per the field's "link where users
  can find more information" fallback.
- **tiegcmpy** — this software's own former name, and a predecessor relationship is exactly what
  Field 29 is for. The repository's first commit is "Moved tiegcmpy to tiegcm3.0",
  `github.com/NCAR/tiegcmpy` now redirects to this repository, and `benchmark/*.py` still open with
  `from tiegcmpy import *`. The PyPI project `tiegcmpy` remains separately installable, frozen at
  2.1.0 (2024-10-21), one week before `gcmprocpy` 1.0.0 — so a user who knows the old name, or who
  lands on the old distribution, needs the pointer to where the software went. It is also the fact
  that determines the publication date in Field 10. That this is one continuous codebase under a
  former name, rather than separate software, is what makes it a predecessor rather than a peer; it
  is recorded for exactly that reason.
- **Kamodo** — NASA's model-output functionalization and visualization package, and the closest peer:
  it performs the same task (reading, interpolating and visualizing ionosphere-thermosphere model
  output) for the same two models, carrying both `tiegcm` and `waccmx` among its keywords in the PyHC
  core registry alongside its other model readers. A user weighing how to work with TIE-GCM output
  will be choosing between these two, which is exactly what Field 29 is for.
- **hapiclient** — a domain-specific dependency, not generic infrastructure: `imfgen`'s *default*
  OMNI access path calls its `hapi()` function against CDAWeb's HAPI server for `OMNI_HRO_1MIN`
  (`imfgen/sources.py: omni_samples_hapi`, guarded by an `ImportError` that names `hapiclient`;
  `imfgen/core.py` defaults `omni_access="hapi"`; `tests/imfgen/test_core.py` exercises the path,
  including a live test). It is recorded here rather than in Field 30 because the relationship is
  gcmprocpy calling a library to fetch data, not two peer tools exchanging data products.
- **geomag** — a domain-specific dependency implementing the World Magnetic Model.
  `plot_gen._compute_gm_equator_lats` instantiates `geomag.geomag.GeoMag()` to place the
  geomagnetic-equator overlay offered by `plt_lat_lon`, `mov_lat_lon` and the `-gmeq` CLI flag. It is
  recorded because a WMM implementation is a specific, domain-meaningful dependency a reader would
  not otherwise infer. Note that its presence is *not* sufficient to earn gcmprocpy a Coordinate
  Transforms classification in Field 4, where the reasons are set out.

Excluded, and why — the generic scientific-Python and tooling stack carries no information about this
package because it would read identically for most of the ecosystem: **numpy**, **scipy**,
**matplotlib**, **cartopy**, **requests**, **ipython**, **ipympl**, **mplcursors**, **PySide6**,
**dask**, **setuptools**, **pytest**, **flake8**. **netCDF4** and **h5py** are excluded as well: both
are real dependencies used for real I/O (appending derived variables; reading BCWIND files), but that
is I/O plumbing rather than a distinguishing peer relationship, and neither appears in the public
API. **pytiegcm** (`github.com/asher-pembroke/pytiegcm`, "python reader for TIE-GCM") was considered
as a second similar-purpose tool and dropped: it is a single-purpose, long-unmaintained reader whose
role Kamodo now fills. **kaipy** was considered because the AMS 2026 abstract presents it alongside
gcmprocpy as the other CGS package — but that is co-presentation, not a software relationship: kaipy
serves the MAGE model, shares no data model with gcmprocpy, and neither imports or converts for the
other.

### 30. Interoperable Software (OPTIONAL)

- https://doi.org/10.5281/zenodo.20076374 — **TIE-GCM**
- https://www.cesm.ucar.edu/models/waccm-x — **WACCM-X**
- https://github.com/pydata/xarray — **xarray**

Each entry rests on a specific, cited exchange rather than on dependency presence or ecosystem
membership.

- **TIE-GCM** — the exchange runs both ways and is documented on both sides. gcmprocpy reads TIE-GCM
  NetCDF history output directly, detecting the model from `ds.lev.units` and switching to TIE-GCM's
  variable names, `ZG` height field and cm/s wind scaling (`io.load_datasets`,
  `containers.MODEL_DEFAULTS`); and `gpigen`/`imfgen` write the GPI and IMF NetCDF files that drive a
  TIE-GCM run, in TIE-GCM's own input layout (`--model tiegcm`, the default). Reciprocally, the
  NCAR-TIEGCM 3.0.1 release notes name this package as the model's post-processing tool:
  "Post-processing (gcmprocpy): https://gcmprocpy.readthedocs.io/en/latest/". The DOI recorded is
  TIE-GCM's Zenodo concept DOI — `doi.org/10.5281/zenodo.20076374` resolves to the latest version
  record (zenodo.20076375, TIEGCM-3.0.1, issued 2026-05-08), confirming it is the all-versions
  identifier rather than a version DOI.
- **WACCM-X** — the same two-way exchange: WACCM-X history files are read with WACCM-X's variable
  names, `Z3` height field, m/s winds and hybrid-pressure density handling
  (`containers.MODEL_DEFAULTS`, `data_density.compute_pkt`, commit `821ee59`), and
  `gpigen --model waccmx` / `imfgen --model waccmx` emit the WACCM-X (CESM) input formats — unlimited
  `time` dimension, `date` plus `datesec`, a 3-hourly `ap` series derived from Kp, and a `WACCMX`
  filename tag — which the docs describe as replacing a separate NCL/`ncrcat` conversion step. No
  software DOI was found for WACCM-X itself; the CESM model page is used as the "link where users can
  find more information", in preference to `github.com/ESCOMP/CAM`, which houses WACCM-X as one
  configuration among many and would not lead a reader to the right place.
- **xarray** — included under the evidence bar for foundational-but-domain-adjacent packages, because
  the exchange is in the public API and is documented as such, not merely internal.
  `docs/source/gcmprocpy/input_generation.rst` states: "Each `generate_*` function returns an
  `xarray.Dataset`, so the data can be inspected or post-processed before being written to NetCDF",
  and `gpigen.generate_gpi` / `imfgen.generate_imf` / `generate_imf_years` do exactly that.
  `io.load_datasets` returns `ModelDataset` objects whose documented public `ds` attribute is an open
  `xarray.Dataset`, so a user can hand gcmprocpy's loaded data to any other xarray-aware tool and
  hand xarray data back. That is a documented interchange format, which is the qualifying condition;
  "uses xarray internally" would not have been.

Excluded, and why: **numpy**, **scipy**, **matplotlib**, **cartopy**, **requests**, **PySide6**,
**ipython**, **ipympl**, **mplcursors** and **setuptools** are generic infrastructure — each would be
equally at home in a web application or a finance model, and "it depends on numpy" is true of nearly
every package in HSSI. **dask** is used only to open datasets with `chunks='auto'` for lazy reads;
nothing is exchanged. **netCDF4** and **h5py** are used for writing and reading files
(`io.save_derived`, the BCWIND reader) but appear nowhere in the public API as an interchange type.
**hapiclient** is a real domain relationship and is recorded in Field 29, where a called library
belongs, rather than duplicated here. No entry rests on "part of the scientific Python ecosystem" or
on PyHC membership, neither of which demonstrates interoperation with any particular package.

### 31. Related Instruments (OPTIONAL)
None.

gcmprocpy is instrument-agnostic. It reads numerical model output — TIE-GCM and WACCM-X NetCDF
history files — plus two index and solar-wind products used as model forcing. It reads no
instrument's data, implements no instrument-specific format, calibrates nothing, and is not an
instrument-team tool. A user searching HSSI for `instrument:"X"` should not get this package back for
any X.

The full search behind that conclusion, so it is not repeated: a case-insensitive sweep of all
`*.py`, `*.rst` and `*.md` files for instrument, mission and observatory names (CHAMP, GRACE, GOLD,
ICON, Swarm, DMSP, GOES, ACE, Wind, Cluster, THEMIS, SuperDARN, Madrigal, Millstone, Arecibo,
Jicamarca, FPI, and the generic terms "satellite", "spacecraft", "instrument", "mission") returned no
instrument reference anywhere in the repository. The only apparent hits were the satellite-track
feature and the neutral-wind variables, neither of which names a platform.

Two things that look instrument-adjacent and are correctly filed elsewhere:

- **Satellite-track interpolation** (`arr_sat_track`, `plt_sat_track`, the `sat_track` command). The
  trajectory is supplied by the caller as arbitrary `sat_time`/`sat_lat`/`sat_lon` arrays; the docs
  demonstrate it with a "simulated satellite pass" and the README calls it interpolation "along
  arbitrary trajectories". No specific satellite or instrument is supported, so this is a Field 4
  capability (`Data Processing and Analysis: Analysis`, `Data Visualization: Line Plots`) and a
  Keyword (`satellite flythrough`), not an instrument association.
- **The airglow and infrared emission models** (5.3 micron NO, 15 micron CO2, 39 OH Meinel bands).
  These compute volume emission rates from model state as synthetic observables. They are not tied to
  any instrument's passband, response function or data product, so they belong under Field 4
  (`Models and Simulations: Physics-Based`), not here.

### 32. Related Observatories (OPTIONAL)
None.

Two candidate identifiers do exist in HSSI's SPASE-backed observatory vocabulary for data sources
this software reads, and both were examined and rejected on relevance, not on resolvability:

- **`OMNI`** — `https://spase-metadata.org/SMWG/Observatory/OMNI`. `imfgen` genuinely reads
  OMNI 1-minute data as its primary source, so the temptation is real. Rejected because OMNI is not a
  mission or observatory: it is a multi-mission merged, time-shifted solar-wind product assembled from
  several spacecraft, and Field 32 explicitly routes generic multi-mission archives and sources to
  Data Sources. The Data Sources vocabulary offers dedicated `OMNIWeb`, `CDAWeb` and `HAPI` values,
  all three of which are selected in Field 17 — that is where this relationship is recorded, at the
  right granularity. (Two further OMNI-named identifiers exist and are equally inapplicable:
  `https://spase-metadata.org/SMWG/Instrument/OMNI` "OMNI Instrument" and the AMDA-scoped
  `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/OMNI`.)
- **`German Research Centre for Geosciences`** —
  `https://spase-metadata.org/SMWG/Observatory/Ground/GFZ`. `gpigen` fetches Kp and F10.7
  from GFZ Potsdam's API. Rejected for the same structural reason: GFZ is the index *provider*, and
  Kp is derived from a distributed global magnetometer network rather than measured by a GFZ
  observatory instrument that this software processes. The Data Sources vocabulary offers a dedicated
  `GFZ` value, which is selected in Field 17, and the underlying dataset is cited by DOI in Field 28.

Also searched and absent: no identifier matches `TIE-GCM`, `TIEGCM`, `WACCM` or `BCWIND` as either an
instrument or an observatory — consistent with these being models and a file format rather than
observatories.
`https://spase-metadata.org/SMWG/Observatory/DRAO` (Dominion Radio Astrophysical Observatory) exists
and is the ultimate origin of the F10.7 flux that `gpigen` requests, but the software neither reads
DRAO data products nor knows DRAO exists; it reads GFZ's redistribution. Associating it would be an
inference two steps removed from anything in the code.

`Observatory/Mission-specific` is correspondingly not selected in Field 17, keeping the record
internally consistent.

### 33. Logo (OPTIONAL)
Not found.

There is no logo. The repository contains no image assets outside the embedded output figures in the
documentation notebooks; `docs/source/conf.py` sets no `html_logo` and no `html_favicon`, and uses
the stock `sphinx_rtd_theme`; neither `README.md` has a header image or badge; the PyHC community
registry entry for GCMprocpy has no `logo` key, unlike many neighbouring entries; and SoMEF returned
no `logo` result. If one is created later, the natural places to look are a new
`docs/source/_static/` asset or a `logo` field added to the PyHC registry entry.
