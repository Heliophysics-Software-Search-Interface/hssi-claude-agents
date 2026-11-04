# HSSI Metadata Extraction Results

**HSSI Software ID:** 98835043-5c60-42d8-8f48-17ec91b60d75
**Repository:** https://github.com/SciQLop/CDFpp
**Source Revision:** 3fcc975e603dc59627bb073f16f301db281d0b9a
**Extraction Date:** 2026-11-03
**Validation Date:** 2026-11-03
**Validation Status:** PASS

---

**Scope note.** The source revision is the v0.20.0 release commit: the annotated tag `v0.20.0` points at it, and it was the head of `main` when this dossier was written. One tree ships three things, and this entry describes all of them:

1. the header-only C++20 library (`include/cdfpp/`, plus SIMD kernels in `src/arch/`);
2. the Python package `pycdfpp` (`pycdfpp/`), published to PyPI as compiled wheels, including the pure-Python `pycdfpp.cdflib` compatibility layer;
3. a WebAssembly build (`wacdfpp/`) whose JavaScript module is attached to the GitHub releases (`cdfpp-wasm-v0.20.0.zip` on v0.20.0, likewise on v0.19.0) and which powers the browser app **CDFpp Explorer**, deployed from this repository to `https://sciqlop.github.io/CDFpp/` by `.github/workflows/gh-pages.yml`.

Where a field turns on which component carries a capability, its note says so. The repository has no git submodules: its third-party C/C++ dependencies (pybind11, xsimd, libdeflate, fmt, Catch2, hedley, zlib, zstd, lz4, c-blosc2, google-benchmark and SciQLop's own `cpp_utils` helper library) are Meson wrap files under `subprojects/`, fetched at build time; their source is not in the tree and is evidence for no field. The repository's own `CLAUDE.md` is development guidance for coding agents and is cited here only as project text.

The project writes its name two ways: **CDFpp** in its README and documentation titles, **PyCDFpp** in its contributing guide, its Sphinx project name and its README caveats; its Python package is `pycdfpp`. The PyHC registry lists it as **PyCDFpp** (`_data/projects.yml` at heliophysicsPy.github.io commit `b1e3c973eebe77486b9530bf06667b8a0fb2be3e`), and the entry takes that name (Field 7).

**Quotation convention.** Quotations of Markdown and reStructuredText prose drop link, emphasis and double-backtick markup, keeping the link text, unless the markup itself is the subject of the note; any other omission is marked with an ellipsis.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** Shawn Polson
- **Submitter Email:** shawn.polson@lasp.colorado.edu

**Source:** supplied by the user for this new submission (rule 4). The addresses found in the source — `alexis.jeandet@member.fsf.org` in `pyproject.toml` and the commit addresses of the three authors — identify authors, not the submitter, and are not this field's value (rule 2).

---

### 2. Persistent Identifier (RECOMMENDED)
`https://doi.org/10.5281/zenodo.6391115`

**Rule 5 — concept DOI of a software deposit of this software.**
- DataCite registers `10.5281/zenodo.6391115` as `resourceTypeGeneral: Software`, publisher Zenodo, with a `HasVersion` list running from the v0.2.0 deposit (`10.5281/zenodo.6391116`, issued 2022-03-28) to the v0.20.0 deposit (`10.5281/zenodo.23933238`). The v0.20.0 Zenodo record gives `conceptdoi: 10.5281/zenodo.6391115`, so this is the all-versions DOI.
- Identity: the deposits are GitHub-integration deposits of this repository, titled `SciQLop/CDFpp: v<version>` — the v0.20.0 record carries `IsSupplementTo https://github.com/SciQLop/CDFpp/tree/v0.20.0` and `custom["code:codeRepository"] = https://github.com/SciQLop/CDFpp`, and its title is the integration's `SciQLop/CDFpp: v0.20.0`.
- What the concept presents: when this dossier was written it resolved to the v0.20.0 record (title `SciQLop/CDFpp: v0.20.0`, DataCite `version: v0.20.0`), the same release Field 12 records. A Zenodo concept resolves to the most recently *created* deposit, so the Software citation will advance with each new release deposit.
- The project's own files cite no DOI: there is no `CITATION.cff`, `codemeta.json` or `.zenodo.json`, no DOI badge in the README, and no citing page in `docs/`. A case-insensitive sweep of the pinned tree (notebooks and test fixtures excluded) for `doi`, `zenodo`, `cite`, `citing` and `citation` returns only three mentions of the ISTP `DOI` global attribute in `docs/istp.rst`. DataCite's title search (`titles.title:*CDFpp*`) finds this concept and its version deposits.
- Only one software concept DOI exists for this software, so rule 7 has nothing to choose.

**Considered and not used here:**
- `https://doi.org/10.5281/zenodo.23933238` — the v0.20.0 *version* DOI (DataCite `IsVersionOf 10.5281/zenodo.6391115`). Rule 3 sends it to Field 12's Version PID, where it is recorded.
- The SciQLop DASH 2026 poster (`10.5281/zenodo.23169248` concept / `10.5281/zenodo.23169249` version) is a poster, not a software record (rule 1); it is in Field 27.

**Known costs, recorded and accepted (rule 5):** the deposits start at v0.2.0 (2022), so the 2020 releases v0.1.x have no DOI; the creators and affiliations in recent deposits are the GitHub-integration defaults (display names, and GitHub "company" strings such as `@LaboratoryOfPlasmaPhysics`), not curated metadata — Field 6 takes the creator list as attestation of authorship, but not its name splits or affiliation strings.

**Coupled fields:** Field 11 is `Zenodo` because this DOI is a Zenodo DOI. Fields 10, 12 and 15 were derived from the repository, not from the deposit (see their notes).

---

### 3. Code Repository (MANDATORY)
`https://github.com/SciQLop/CDFpp`

**Rule 7 — canonical base URL of the public source repository.** Agreeing sources: the clone's `origin` remote; the GitHub API (`full_name: SciQLop/CDFpp`, not a fork, not archived, default branch `main`, created 2019-12-15); `pyproject.toml` `[project.urls]` `repository` and `homepage`; the PyHC registry `code:`; and the Zenodo deposits' `code:codeRepository`. No redirect: the repository has not moved or been renamed.

**Considered and not used:**
- `https://sciqlop.github.io/CDFpp/` — the GitHub repository's "homepage" setting; it is the CDFpp Explorer web app, not the source (rule 2).
- `https://pypi.org/project/pycdfpp/` and the Zenodo `/tree/v<tag>` URLs — a distribution page and release-pinned page URLs, never a new Field 3 value (rule 7).

**Inbound relations:** before this entry was submitted, three catalogue entries — Speasy, CDFlib and PyRFU — already pointed at exactly this string in their Related Software, so recording it byte for byte makes those links resolve to this entry.

---

### 4. Software Functionality (RECOMMENDED — treated as critical)

Values, grouped by family (order is stored data):

1. `Data Processing and Analysis`
2. `Data Processing and Analysis: Data Access and Retrieval`
3. `Data Processing and Analysis: File Format Conversion`
4. `Data Processing and Analysis: Data Reduction`
5. `Data Processing and Analysis: 2D Slices`
6. `Data Processing and Analysis: Processing`
7. `Data Visualization`
8. `Data Visualization: Line Plots`
9. `Data Visualization: Spectrogram`
10. `Data Visualization: 2D Slices`
11. `Data Visualization: Web-Based`

Each child is written `Parent: Child`, and every child's parent is listed (rule 10).

**Why CDFpp Explorer counts (rules 4 and 6).** Several values rest on CDFpp Explorer and the WebAssembly module behind it, which the PyPI wheels do not contain. They count because they are part of what this entry describes, not examples or plug-ins: the entry is the repository (Field 3), and the repository builds the module and the app with its own Meson build (`wacdfpp/meson.build`), tests them (`tests/wasm_*`, `tests/wacdfpp_yaml/`), versions them with the library (`docs/history.rst` records Explorer changes under the library's releases), deploys the app from the repository to GitHub Pages (`.github/workflows/gh-pages.yml`) and attaches the JavaScript module to the GitHub releases. Rule 4 excludes example scripts and gallery pages, which these are not; rule 6 excludes separately distributed plug-ins, which these are not.

**Evidence for each value (rule 12):**
- **Data Processing and Analysis** — the core of the software is reading and writing CDF files: `cdf::io::load` / `cdf::io::save` (`include/cdfpp/cdf-io/`), `pycdfpp.load` / `pycdfpp.save`, and variable and attribute editing (`CDF.add_variable`, `add_attribute`). This is the family the library map assigns to CDF I/O libraries (`cdflib`, `spacepy.pycdf`).
- **Data Access and Retrieval** — `pycdfpp.load` accepts an `https://`, `s3://`, `gs://` or other fsspec URL, or any object with `size()` and `read_ranges()`, and fetches only the byte ranges parsing needs (`pycdfpp/__init__.py` `load`, `pycdfpp/_remote.py` `FsspecReader`; public S3 buckets are read anonymously by default). The C++ side reads remote files through the same loader (`include/cdfpp/cdf-io/loading/loading.hpp` `default_remote_options`). The README and `docs/reading.rst` present it as reading NASA HelioCloud's S3 copy of the SPDF archive without downloading whole files. CDFpp Explorer also fetches a public CDF file by URL. This is a user-facing retrieval capability, not an internal utility.
- **File Format Conversion** — CDFpp Explorer reads a CDF file and writes its plotted data as CSV or JSON (`wacdfpp/plot-model.js` `toCSV` / `toJSON`, offered as download buttons in `wacdfpp/plot.js`; `docs/explorer.rst`: "You can export the plotted data as CSV or JSON"), and writes the file's structure and attributes as a YAML skeleton (`wacdfpp/cdf-yaml.js`, "Export YAML"). In-memory conversions alone would not qualify (`pycdfpp.cdflib.xarray.cdf_to_xarray` returns an `xarray.Dataset`; `to_dict_skeleton` returns a dict); the Explorer exports are files in other formats.
- **Data Reduction** — `wacdfpp/reduce.hpp` collapses the non-record dimensions of multi-dimensional variables (particle distributions) by masked sum or mean, leaving out fill and invalid values. It is part of the module's public TypeScript declarations, shipped with the JavaScript module (`wacdfpp/cdfpp.d.ts` `reduce_values(name, modes, op: "sum" | "mean", fill, valid_min, valid_max)`, which returns a `Float64Array`), and it drives the Explorer's plots (`docs/explorer.rst`: "Variables with more dimensions … are reduced before they are drawn").
- **Data Processing and Analysis: 2D Slices** — the same `reduce_values` takes one mode per non-record dimension — "-1 keeps it, -2 collapses it with `op`, an index >= 0 slices it" (`wacdfpp/cdfpp.d.ts`) — and returns a row-major array of records × kept dimensions, so an embedding application receives a two-dimensional cross-section of three- and four-dimensional data as an array. Returning the slice as data and drawing it (`Data Visualization: 2D Slices`) are different capabilities, so both are listed (rule 9).
- **Data Processing and Analysis: Processing** — user-facing transforms of a file's content beyond reading and writing it: conversion of the three CDF time types to and from `datetime64[ns]`, Python `datetime` and formatted strings (`to_datetime64`, `to_datetime`, `to_tt2000`, `to_epoch`, `to_epoch16`, `to_time_string`, with SIMD kernels in `src/arch/`; the README's "SIMD-accelerated time conversions"); filtering variables and attributes by name, pattern or function, in place or into a new CDF (`filter_cdf`, `CDF.filter`); and recompressing a file or its variables with another codec or level (`CDF.compression`, `compression_level`, the Explorer's "Convert codec").
- **Data Visualization: Line Plots** — the Explorer draws time series as lines (`wacdfpp/plot.js`, uPlot), ISTP-aware (`DEPEND_0` time axis, `DISPLAY_TYPE`, `SCALETYP` log scales, `FILLVAL` / `VALIDMIN` / `VALIDMAX` masking).
- **Data Visualization: Spectrogram** — the Explorer draws spectrograms as colour maps (`wacdfpp/spectrogram.js`), including the omnidirectional energy spectrogram it builds by default from particle distributions (`wacdfpp/plot-model.js` keeps the axis whose `DEPEND_k` name matches `/energ/i` and collapses the rest).
- **Data Visualization: 2D Slices** — for a variable with several non-record dimensions, each dimension gets a menu, and "= value: keep a single slice, for example one energy channel" (`docs/explorer.rst`), so the Explorer displays a two-dimensional slice (time × one dimension) of three- and four-dimensional data.
- **Data Visualization: Web-Based** — CDFpp Explorer is an interactive browser app (pan and zoom, log/linear toggles), running the library compiled to WebAssembly client-side.

**Considered and not selected:**
- `Data Processing and Analysis: Spectrogram` (rule 3) — `reduce_values` hands an embedder a records × energy array when the kept dimension is energy, but the capability users get is dimension reduction and slicing, already carried by `Data Reduction` and `2D Slices`. Nothing computes a time–frequency representation (no Fourier, wavelet or frequency binning), and the result is spectrogram-shaped only when the input variable already has an energy axis; the value would send a searcher looking for spectral analysis to a file library.
- `Data Processing and Analysis: Energy Spectra` — the Explorer's default energy spectrogram is a display choice over the generic sum/mean reduction (it picks the axis by its `DEPEND_k` name); nothing computes energy spectra as such (no flux weighting, no unit conversion).
- `Data Processing and Analysis: Analysis` — nothing derives physical quantities.
- `Data Processing and Analysis: Calibration` and `Mission-related: Calibration` — CDFpp is *used by* the Solar Orbiter LFR calibration code; it calibrates nothing itself.
- **`Mission-related` and `Mission-related: Science Data Processing` (rule 8).** Weighed on CDFpp's writer and its producer documentation (`docs/masters.rst` on filling master CDFs, `docs/istp.rst` "Producing ISTP-compliant files", the `docs/index.rst` card addressed to ground-segment and instrument teams) and on the developers' DASH 2026 poster (Field 27): "In mission pipelines: the Solar Orbiter LFR calibration code runs almost 2× faster with pycdfpp, and BepiColombo MSA uses it too." Rule 8 needs a source showing named missions producing their archive-standard science files with the software, and none does: the poster says mission code runs on pycdfpp, not that pycdfpp writes those missions' archive products; the Solar Orbiter RPW ground-pipeline packages on PyPI (`roc-film`, `roc-rap`, `roc-rpl`, `roc-dingo` and others) declare no dependency on pycdfpp; and the one mission toolbox found writing CDF through pycdfpp, ESA Swarm's SwarmPAL, is a downstream consumer recorded in Field 30. Being a dependency of mission code does not make a library part of the mission's chain (rules 2 and 8), and CDFlib's entry, a CDF library of the same kind, carried no `Mission-related` value when this dossier was written. Restore both values if a primary source shows a mission producing its archive files with CDFpp.
- `Coordinate Transforms` (all children) — time-system conversions (TT2000, CDF_EPOCH, EPOCH16) are not coordinate frames; no frame transform exists in the tree.
- Other Data Visualization children (`2D Graphics`, `3D Graphics`, `Hodograms`, `Movies`, `Orbit Plots`, `Spacecraft Formation Plots`, `Mission-Specific`, `ML/AI`) — the Explorer draws only line plots and spectrograms.
- `Models and Simulations`, `Servers and Environments` (all children) — no model, no server (the Explorer is a static client-side page), no container or HPC tooling (threads only, no MPI).
- The Explorer's "Validate" button is a handoff to AstraLint (a separate SciQLop tool, Field 30); validation is AstraLint's capability, not CDFpp's.

---

### 5. Related Region (RECOMMENDED — treated as critical)
Not found — evidenced empty.

**Rule 2 — domain-independent software.** CDFpp is an implementation of a file format: the loader, writer, codecs, time conversions and Explorer behave identically whatever physical domain a CDF file describes, and no module computes, models or analyses the physics of any region. The README and docs describe a format library ("A modern, from-scratch C++20 implementation of NASA's CDF"); the docs note CDF is "the file format most space physics missions use to distribute their data", which places the software in heliophysics but not in any region. No row of the Region vocabulary passes rule 4.

**Rejected candidates, recorded so they are recognised on sight (rule 3 and the traps):**
- GitHub topics `plasma-physics` and `space` — borrowed labels; `plasma-physics` reflects the developing laboratory (see Field 16).
- Test fixtures under `tests/resources/` from ACE (MFI, SIS), Geotail CPI, Interball, Solar Orbiter RPW, THEMIS ground magnetometers, Ulysses SWOOPS and Wind — mostly SPDF master CDFs (`*_00000000_v*.cdf`), chosen for structural variety.
- CDFpp Explorer's demo presets (`wacdfpp/presets.js`: MMS1 EDP and FPI, THEMIS-A ESA, Solar Orbiter MAG, OMNI SYM-H, Cluster C1 FGM) and the docs' running example (ACE MFI H0) — example files, not scope.
- Use in Solar Orbiter and BepiColombo pipelines (Field 4) — downstream users' regions, not the software's.

---

### 6. Authors (MANDATORY)

**Values — 3 authors**, in the order of the Zenodo/DataCite creator list (the only source naming more than one author):

**Author 1 — Alexis Jeandet**
- **Name:** Alexis Jeandet (given `Alexis`, family `Jeandet`)
- **Author Identifier:** `https://orcid.org/0000-0003-2892-6924`
- **Affiliation:**
  - **Organization:** Laboratoire de Physique des Plasmas
  - **Affiliation Identifier:** `https://ror.org/05c95bg36`
- **Source:** `pyproject.toml` `authors`; `docs/authors.rst` ("Development Lead"); `docs/conf.py` `author`; Zenodo/DataCite creators of every deposit; nearly all commits at the pin (`alexis.jeandet@member.fsf.org`, plus three from `alexis.jeandet@lpp.polytechnique.fr`).
- **Identifier:** the ORCID record (name "Alexis Jeandet") lists employment at Laboratoire de Physique des Plasmas, Palaiseau, disambiguated by ROR `05c95bg36`, from 2008 with no end date; the same ORCID sits beside his name in the `CITATION.cff` of his Speasy project. When this dossier was written the catalogue's Person row for him already carried this ORCID (it serves Speasy, SciQLop, CDFlib and PlasmaPy), so the submission binds that row by identifier.
- **Affiliation:** ORCID employment covering the whole period of the software (rule 21), corroborated by his `lpp.polytechnique.fr` commit address and the copyright line ("Laboratory of Plasma Physics, Ecole Polytechnique, CNRS, Sorbonne Université, Université Paris-Saclay" in `COPYING`). The deposits' affiliation string `@LaboratoryOfPlasmaPhysics` is a GitHub organization handle, not an affiliation (rule 18); the institution it points to is the one recorded.

**Author 2 — Zijin Zhang**
- **Name:** Zijin Zhang (given `Zijin`, family `Zhang`)
- **Author Identifier:** `https://orcid.org/0000-0002-9968-067X` — **the new submission names this author by given and family name only, with no identifier; the ORCID reaches his Person row through an update that selects that row (see below).**
- **Affiliation:**
  - **Organization:** University of California, Los Angeles
  - **Affiliation Identifier:** `https://ror.org/046rm7j60`
- **Source:** creator of the v0.20.0 Zenodo/DataCite deposit (`10.5281/zenodo.23933238`, and therefore of the concept record as it presents v0.20.0). He is the git author of `a02692720b44deba233641bb4ed09fc63fbe9078` (2026-11-02, "fix(loading): keep rVariable and zVariable attribute entries apart", a fix listed in the v0.20.0 release notes), committed as `Beforerr <zzj956959688@gmail.com>`. GitHub account `Beforerr` (id 58776897) publishes the profile name "Zijin Zhang". A Zenodo creator is an attested author (rule 8).
- **Identifier linkage (rule 14):** ORCID `0000-0002-9968-067X` ("Zijin Zhang"; employment University of California, Los Angeles, Earth, Planetary, and Space Sciences, graduate student researcher, from 2022, no end date; works in space plasma physics). The link to this contributor is direct: `CITATION.cff` of `JuliaSpacePhysics/CDFDatasets.jl` (at `27c070c3cf71bd060a90cd8096647ab0f444487e`) gives `given-names: Zijin`, `family-names: Zhang`, `orcid: 0000-0002-9968-067X`, `email: zijin@ucla.edu`, while that project's `Project.toml` names its author `Beforerr <zzj956959688@gmail.com>` — the exact address of his CDFpp commit — and GitHub account `Beforerr` is that repository's only human contributor; its Zenodo deposit (`10.5281/zenodo.23461762`) carries the same ORCID beside "Zhang, Zijin".
- **How the identifier reaches the catalogue (rules 16 and 15).** Before this entry was submitted, the catalogue already held a Person row `Zijin` / `Zhang`, the only row with that exact split, carrying no identifier and crediting him on PySPEDAS. It is the same person: PySPEDAS's `CITATION.cff` credits `Beforerr`, and its commits come from `58776897+Beforerr@users.noreply.github.com` and the same gmail address as his CDFpp commit. A new submission cannot select a Person row by `personId`, and an ORCID that no row carried would have created a second Person for him. So the submission binds the existing row by its exact given and family names, with no identifier, and the ORCID is attached by an update that selects that row by `personId`. After both writes the one Person row carries the ORCID on this entry and on PySPEDAS alike, which is correct for the same person; the PySPEDAS dossier had left this ORCID unassigned for lack of the linkage recorded above.
- **Affiliation:** ORCID employment covering the period of his contribution (rule 21), corroborated by the `zijin@ucla.edu` address in his own `CITATION.cff`. The ROR's display name matches the catalogue's existing UCLA Organization row, which the identifier binds. The Person row it is added to also serves PySPEDAS; the affiliation is current, not years-stale (rule 19), and true of his PySPEDAS commits too (2023–2026, all within the UCLA employment). The deposit gives no affiliation for him.

**Author 3 — Nicolas Aunai**
- **Name:** Nicolas Aunai (given `Nicolas`, family `Aunai`)
- **Author Identifier:** `https://orcid.org/0000-0002-9862-4318`
- **Affiliation:**
  - **Organization:** Laboratoire de Physique des Plasmas
  - **Affiliation Identifier:** `https://ror.org/05c95bg36`
- **Source:** creator of the Zenodo/DataCite deposits (affiliation string "CNRS / Laboratory of Plasma Physics"); git author of `503cb9e0ff89d54221abdd2c1f28c71ee501298e` (2023-11-01, from `nicolas.aunai@lpp.polytechnique.fr`).
- **Identifier and affiliation:** his ORCID record lists employment "Laboratoire de Physique des Plasmas  / CNRS" (spacing as ORCID stores it), Palaiseau, researcher, from 2014 with no end date; the same ORCID sits beside his name in Speasy's `CITATION.cff`, and the catalogue's Person row for him already carried it when this dossier was written (it serves Speasy and SciQLop). The deposit string "CNRS / Laboratory of Plasma Physics" names that one laboratory (LPP, UMR 7648), recorded under its ROR-identified name, as the Speasy and SciQLop dossiers settled for the same person. The ORCID record writes the name in lower case ("nicolas aunai"); the capitalised form is used.

**Considered and not added:**
- `dependabot[bot]` (dependency-update commits) — a bot (rule 5).
- The copyright holders in `COPYING` and the file headers (Laboratory of Plasma Physics, Ecole Polytechnique, CNRS, Sorbonne Université, Université Paris-Saclay) — copyright holders, not authors; no author source credits an organization.
- The other co-authors of the DASH 2026 poster (Vincent Génot, Benjamin Renard, Myriam Bouchemit, Nicolas André) — co-authors of a presentation about the SciQLop stack who appear in no CDFpp software-metadata source (rule 7).
- Name splits from the recent deposits (DataCite puts each whole name in `familyName`, e.g. `"familyName": "Alexis Jeandet"`) are not used (rule 12); the splits come from the ORCID records and the earliest deposit (`Jeandet, Alexis`).

---

### 7. Software Name (MANDATORY)
`PyCDFpp`

**The curated PyHC registry name, chosen by the catalogue maintainer so that the catalogue and PyHC name the software identically.** The registry lists it as `name: PyCDFpp` (`_data/projects.yml` at `b1e3c973eebe77486b9530bf06667b8a0fb2be3e`, shown on PyHC's Projects page). The project's own sources use two names, and where they disagree rule 8 lets the curated registry `name:` decide, which gives the same answer:
- **PyCDFpp** — the contributing guide (`docs/contributing.rst`: "PyCDFpp could always use more documentation, whether as part of the official PyCDFpp docs", lines 41–42; "Ready to contribute? Here's how to set up `PyCDFpp` for local development." and "Fork the `PyCDFpp` repo on GitHub.", lines 60 and 62), the Sphinx project name (`SPHINXPROJ = PyCDFpp` in `docs/Makefile`, and `'SPHINXPROJ': 'PyCDFpp'` in `docs/meson.build`), and the README's Caveats ("PyCDFpp exposes the record count as the first dimension …").
- **CDFpp** — the README's top-level heading `CDFpp (CDF++)`, the docs title (`docs/conf.py` `project = 'CDFpp'` and `html_title = f'CDFpp {version}'`, the `docs/index.rst` title), the repository name `SciQLop/CDFpp`, and the docs' introduction ("CDFpp is a modern implementation of it, written from scratch in C++20. Its Python package is called pycdfpp.").

**Alternatives weighed, so a later refresh does not churn the value:**
- `CDFpp` — the project's title form. Not adopted: the project writes PyCDFpp too, and the registry form keeps HSSI and PyHC consistent. The cost is small: `name:` field searches match substrings, so a search for `CDFpp` still finds `PyCDFpp`, and the description presents CDFpp, its C++ library and its WebAssembly build, so the entry does not read as a Python-only package.
- `pycdfpp` — the PyPI distribution and import name; the fallback only when the project uses nothing else.
- `CDF++` — an alias in the README heading's parenthesis, used nowhere else.
- `SciQLop/CDFpp: v0.20.0` — the Zenodo integration title, a generated locator (rule 1).

---

### 8. Description (MANDATORY)

```markdown
A modern, from-scratch C++20 implementation of NASA's CDF (Common Data Format) with full Python bindings.

Why another CDF library? NASA's official C implementation has no multi-thread support (global shared state), an aging C89 interface, and a license incompatible with most Linux distribution policies. CDFpp solves all three: it is thread-safe, idiomatic C++20, and MIT-licensed.

- **C++20 library, mostly headers**
- **Complete read/write support** — CDF versions 2.2 through 3.x, row and column major, compressed files and variables (GZip, RLE)
- **Python bindings (`pycdfpp`)** via pybind11 — zero-copy NumPy integration, GIL-free I/O
- **SIMD-accelerated time conversions** — AVX512/AVX2/SSE2 runtime dispatch for TT2000, EPOCH, EPOCH16
- **Lazy loading** — variable data is read on first access, not at file open
- **Read files where they live** — `pycdfpp.load("s3://…")` reads only the byte ranges it needs, through fsspec or your own byte-range reader, instead of downloading the file
- **Drop-in `cdflib` replacement** — replace `import cdflib` with `import pycdfpp.cdflib as cdflib` and your cdflib code runs on pycdfpp, unchanged. For a library you can't edit, such as SunPy, call `pycdfpp.cdflib.install()` before importing it: its own `import cdflib` then gets pycdfpp's version too
- **Fast** — 5.6× to several hundred times faster than spacepy and cdflib at reading, 3.7× to 14× at writing compressed files; SIMD time conversions at up to 8 billion epochs/s (TT2000, AVX-512)
- **Runs everywhere** — Linux, Windows, macOS (x86_64 + ARM64), and WebAssembly (Pyodide / emscripten-forge)

CDFpp compiles to **WebAssembly**, so the whole library runs client-side — no install, no server, and your files never leave your machine. **CDFpp Explorer** is a small web app built on it:

- **Inspect** — browse variables and attributes grouped by ISTP `VAR_TYPE`, with live search and a value preview
- **Plot** — line plots and spectrograms, ISTP-aware (`DEPEND_0` time axis, `DISPLAY_TYPE`, `SCALETYP`, fill/valid masking), with CSV / JSON export
- **Validate** — hand the file to AstraLint for ISTP conformance checking

The WebAssembly wrapper lives in `wacdfpp/` and ships TypeScript declarations (`wacdfpp/cdfpp.d.ts`) for embedding CDF read/write — with zero-copy typed arrays — in your own JavaScript app.
```

(The value is the text inside the fence, 2,322 characters.)

**Rule 7 — the project's own words.** There is no `CITATION.cff` abstract. The README's lead sentence is the opening; it is a complete preview on its own, but too thin to say why to use the software, so the text extends the quotation with whole passages of the pinned README in the README's own order: the "Why another CDF library?" paragraph, the Highlights list, and the CDFpp Explorer section. Light cleanup only:
- markdown links removed (`[CDF](https://cdf.gsfc.nasa.gov/)`, `[**CDFpp Explorer**](…)`, `[AstraLint](…)`, and the relative link on `` `wacdfpp/` ``, which would break outside GitHub);
- the bold markers removed from `**Why another CDF library?**`, which falls inside the first 199 characters the result card shows as plain text;
- two navigation asides removed: "— see the [C++ guide](…) for the compiler flags" from the first Highlights item, and "([see below](#compared-with-spacepy-and-cdflib))" from the **Fast** item.

**Omitted on purpose:**
- The Highlights item "In-browser app — CDFpp Explorer inspects, plots, and ISTP-validates CDF files entirely client-side, no install". The Explorer's validation is a handoff to AstraLint, a separate tool (`wacdfpp/astralint.js` opens AstraLint's web app with the file), so "ISTP-validates" would credit CDFpp with AstraLint's capability (rule 8). The README's own Explorer section, quoted instead, attributes validation correctly ("hand the file to AstraLint").
- The installation, quick-start, benchmark tables, roadmap and caveats sections — landing-page material.

**Each capability named is present in the pinned code (rule 2):** CDF read/write across versions and majorities with GZip and RLE (`include/cdfpp/cdf-io/`); pybind11 bindings released from the GIL (`pycdfpp/pycdfpp.cpp`); SIMD time conversions with x86 runtime dispatch (`src/arch/x86/`) and NEON (`src/arch/arm/`); lazy loading (`load(..., lazy_load=True)`); remote byte-range reads (`pycdfpp/_remote.py`, `load_reader`); the cdflib layer and `install()` (`pycdfpp/cdflib/`); wheels for Linux, Windows and macOS on x86_64 and ARM64 plus Pyodide `wasm32` wheels on PyPI for 0.20.0; the Explorer's inspect, plot, CSV/JSON export and AstraLint handoff (`wacdfpp/`); `wacdfpp/cdfpp.d.ts`. The **Fast** item is the project's own benchmark claim (README "Benchmarks", reproducible with `benchmarks/python_libs/compare.py`), quoted as the project states it.

**Alternatives considered:** the `pyproject.toml` `description` (PyPI's summary line) "A modern C++ header only cdf library" and the GitHub description "A modern C++ header only cdf library with Python bindings" are older and thinner (the library is now "mostly headers", with compiled extensions); `pyproject.toml` also carries a stray `summary = "A simple to use CDF files reader"`, which is not a standard project-metadata key and appears nowhere on PyPI; the PyHC registry's "A fast and easy to use C++ CDF library with Python bindings." is a one-line summary (Field 9).

---

### 9. Concise Description (OPTIONAL)
`A fast and easy to use C++ CDF library with Python bindings.`

(The value is the text inside the backticks, 60 characters.)

**Source: the PyHC registry's `description:` for PyCDFpp** (`_data/projects.yml` at `b1e3c973eebe77486b9530bf06667b8a0fb2be3e`), taken verbatim. It is the first source in rule 6's order, and it is the curated registry's summary, under the same name as Field 7.
- Every claim it makes holds at the pinned code (rule 2): a C++ CDF library (`include/cdfpp/`) with Python bindings (`pycdfpp`); "fast" is the project's own benchmarked claim (README "Benchmarks").
- It is 60 characters, well within the 200-character limit (rule 3).
- "easy to use" without hyphens is an accepted style, not an error, so rule 4 does not fire.

**Why the field is filled.** The catalogue maintainer decided that every new entry in this submission batch carries both a description and a concise description. That decision overrides rule 6's empty outcome, the alternative not taken. Under rule 6 alone the field would stay empty, because the description's opening sentence already stands alone as a preview ("A modern, from-scratch C++20 implementation of NASA's CDF (Common Data Format) with full Python bindings.", 105 characters).

**Other candidates, considered and not adopted:**
- The `pyproject.toml` `description`, "A modern C++ header only cdf library" (also PyPI's summary), and the GitHub description, "A modern C++ header only cdf library with Python bindings". "Header only" no longer holds: the README now says "mostly headers", and the package ships compiled extensions.
- The README's lead sentence. It is accurate, but it is Field 8's opening word for word, so on the detail page it would only repeat the description.

---

## Section 2: Additional Data

### 10. Publication Date (RECOMMENDED)
`2020-01-19`

**Rule 4 — first-release date.** The earliest public release is GitHub release `v0.1.0`, published 2020-01-19T16:00:01Z and not marked pre-release; its tag (`770627e856c2010eec3fdf77d427be67cb1f0a98`, 2020-01-19T15:58:39Z) is on the pinned revision's ancestry. The releases that follow it (`v0.1.1`, `v0.1.2` and `v0.1.3` on 2020-01-19, `v0.1.6` on 2020-01-20) are marked pre-release on GitHub. The first PyPI upload is 0.1.6, 2020-01-20T13:10:39Z, a day later.

**Considered and not selected:**
- `2019-12-15` — anchor (b), first public source: the repository was created 2019-12-15T13:37:46Z and its first commit (`32fe99420fac852e6f3a6680d2450b3d688c681e`, "Init") is dated 2019-12-15T13:38:46Z, so the source was public from day one. Rule 4 prefers the first release for a new value.
- `2022-03-28` — the first Zenodo deposit (v0.2.0, `10.5281/zenodo.6391116`): a DOI mint date long after first publication (rule 1).
- `2026-11-03` — the concept DOI's DataCite `Issued` date, which is the date of the newest deposit (rule 1).

---

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** `https://zenodo.org`

**Rule 1.** Field 2 is a Zenodo DOI, and DataCite's `publisher` for it is `Zenodo`. Zenodo has no ROR; CERN's ROR identifies the operator, not the repository, and is not a substitute. The identifier `https://zenodo.org` is the form the catalogue's existing Zenodo Organization row carries, so the submission binds that row.

**Not used:** `GitHub` (rule 5 applies only when no DOI exists); PyPI (a package index is never the publisher, rule 6); the copyright holders in `COPYING` (not a distribution statement).

---

### 12. Version (RECOMMENDED)
- **Version Number:** `0.20.0`
- **Version Date:** `2026-11-03`
- **Version PID:** `https://doi.org/10.5281/zenodo.23933238`
- **Version Description:**

```markdown
## Read files where they live

`pycdfpp.load` now takes an `https://`, `s3://`, `gs://` or any other fsspec URL. It fetches only the bytes it needs, each at most once, and nothing is downloaded whole by default.

- Values are fetched when they are read. On NASA's HelioCloud, opening a 53.6 MB file fetched 2.3 MB, and reading one variable fetched 8.6 MB.
- Public buckets are read anonymously. AWS credentials on the machine are used when there are some.
- Any object with `size()` and `read_ranges()` works too, so you can plug in your own reader.
- Five settings tune the requests: `read_ahead`, `tail_prefetch`, `backing`, `temp_dir` and `download_whole_below`. Each is a keyword of `pycdfpp.load` and has a `CDFPP_REMOTE_*` environment variable.
- C++ code reads remote files the same way, through the same loader.
- Install the fsspec support with `pip install pycdfpp[s3]`.

## A drop-in cdflib replacement

`pycdfpp.cdflib` mirrors the API of [cdflib](https://github.com/MAVENSDC/cdflib) 1.3.16: `CDF`, `cdfwrite.CDF`, `cdfepoch`, `cdf_to_xarray` and `xarray_to_cdf`. It runs on pycdfpp, so it is faster.

- For a library you can't edit, such as SunPy, call `pycdfpp.cdflib.install()` before importing it. Its own `import cdflib` then gets pycdfpp's version.
- Install it with `pip install pycdfpp[cdflib]`.

## Fixes

- **rVariable and zVariable attribute entries are kept apart.** Each entry is numbered after its own kind of variable, but the loader read both kinds into one list. So in a file holding both kinds, rVariable N got the entries of zVariable N, and most variables had no attributes at all.
- **Out-of-range variable numbers.** A file numbering a variable past the number of variables in its header loads that variable without attributes, instead of reading out of bounds.
- **`NumStrings` in saved files.** Each text attribute entry now carries the right number of strings, as NASA's library writes it. A variable entry holding `"first\N second"` counts 2, a global entry 0. pycdfpp used to count newlines instead. Readers that split entries on that field, like cdflib's `attget`, got one string instead of several. The text itself was never wrong.
- **`pycdfpp.cdflib.xarray_to_cdf` writing twice** to a name without the `.cdf` suffix reports that nothing was written, instead of raising on the `.cdf` file it had already written.

## Python versions

- Python 3.9 is no longer supported. It reached its end of life in October 2025.
- Wheels are built for Python 3.10 to 3.15, with cibuildwheel 4.3.5.
```

(The value is the text inside the fence.)

**Release history at the pin.** Release tags run from `v0.1.0` (2020-01-19) to `v0.20.0`. Most are on the pinned revision's ancestry; `v0.4.7`, `v0.8.7` and `v0.9.2` sit on maintenance branches (`origin/0.4.7`, `origin/v0.8` and `origin/release/0.9.2`), `v0.4.1` is on no remote branch, and `test`, `v0.0.0` and `v0.0.0.0` are stray tags, not releases. None of these is newer than `v0.20.0`. No anomaly shape applies: the pin is the release commit itself, and no newer tag, PyPI upload or GitHub release exists.

**Version Number** (rule 5). `0.20.0` is the newest release: GitHub release `v0.20.0` (not a pre-release), the annotated tag `v0.20.0` on the pinned commit, and the PyPI upload `0.20.0` (not yanked). The number is written as `version.txt`, `pyproject.toml` (`[tool.bumpversion] current_version`) and PyPI write it; the tag and the GitHub release name write `v0.20.0`. Either form is correct; a later refresh should keep the unprefixed form rather than "fix" it.

**Version Date** (rule 7). GitHub release `v0.20.0` was published 2026-11-03T23:20:17Z. The tagged commit is 2026-11-04T00:18:42+01:00 (2026-11-03T23:18:42Z) and the Zenodo deposit was created 2026-11-03T23:20:22Z (DataCite `Issued` 2026-11-03), all on the release day in UTC. The first PyPI file was uploaded 2026-11-04T00:14:29Z, 54 minutes after the release and past midnight UTC; the release day stands. `docs/history.rst` heads the entry "0.20.0 (2026-11-04)", the Paris local date of the tag; per rule 8 a changelog heading does not override the release event, so a later refresh should not "correct" the date to 2026-11-04.

**Version PID** (rule 17). `10.5281/zenodo.23933238` is the v0.20.0 GitHub-integration deposit: DataCite `version: v0.20.0`, `IsSupplementTo https://github.com/SciQLop/CDFpp/tree/v0.20.0`, `IsVersionOf 10.5281/zenodo.6391115`, and it is in the concept's `HasVersion` list.

**Version Description** (rules 13–16). The GitHub release name is only the tag, so the source is the release body, kept verbatim with whole items trimmed:
- kept: the two new features (remote reads; the cdflib replacement layer), every user-visible fix, and the supported-Python change;
- dropped: the two code examples and the two "See [Reading files](…)" / "See [the cdflib page](…)" pointer lines (pointers and examples, not changes), and the closing "**Full changelog**" compare link.

The kept text is the release body's own lines with nothing reworded; its one markdown link (to cdflib's old `MAVENSDC` repository URL, which redirects to `lasp/cdflib`) is the project's own and renders under "Release Notes". `docs/history.rst` carries the same changes in different wording; the release body is preferred as the higher source in rule 13's order.

---

### 13. Programming Language (RECOMMENDED)
- `C++`
- `Python 3.x`
- `Javascript`

**Rule 4 — source-available package; the languages a user writes plus the science core.**
- **C++** — the library itself, header-only C++20 under `include/cdfpp/` with SIMD kernels in `src/arch/` and the pybind11 bindings (`pycdfpp/*.hpp`, `pycdfpp/pycdfpp.cpp`); `meson.build` sets `cpp_std=c++20`. C++ is also a user language (the `docs/index.rst` card "Use CDFpp from C++", and the C++ guide `docs/cpp.rst`).
- **Python 3.x** (rule 5) — the `pycdfpp` package (`pycdfpp/__init__.py`, `_remote.py`, the CLI scripts `cdfdump` and `cdfirsdump`, and the pure-Python `pycdfpp/cdflib/` layer); `requires-python = ">=3.10"`, classifiers for Python 3.10–3.15. No Python 2 target, so no `Python 2.x`.
- **Javascript** — a supported front end in a second language: the WebAssembly build is used from JavaScript (`docs/wasm.rst`: "The result is a JavaScript module, cdfpp.js, that reads CDF files in a web page, a Web Worker, or Node.js"), has its own build target (`wacdfpp/meson.build`) and tests (`tests/wasm_*`, `tests/wacdfpp_yaml/test.mjs`), is attached as `cdfpp-wasm-<tag>.zip` to the GitHub releases by `.github/workflows/gh-pages.yml` (v0.19.0 and v0.20.0 carry it), and CDFpp Explorer itself is written in JavaScript (`wacdfpp/*.js`). Spelled `Javascript`, as the vocabulary row is.

**Considered and not selected:**
- `Typescript` — the only TypeScript file is `wacdfpp/cdfpp.d.ts`, type declarations for the JavaScript module; the front end is JavaScript.
- `C` — the C libraries the build fetches (libdeflate, zlib, zstd, lz4, c-blosc2) are compression dependencies, not the science core, and are not in the tree; two C fixture generators in `tests/resources/` (`make_sparse_records.c`, `make_structural_fixtures.c`) are test-only.
- Meson, shell and the CI YAML — build tooling, not languages (rule 4).

---

### 14. Reference Publication (OPTIONAL)
Not found.

**Rule 7 — nothing qualifies.** The project gives no citation guidance: there is no `CITATION.cff`, `codemeta.json`, README "Citing" section, docs citing page or JOSS badge (the sweep under Field 2 found no `cite`, `citing` or `citation` anywhere in the pinned tree outside notebooks and fixtures). No paper describes the software: an ADS full-text and abstract search for `CDFpp` and `pycdfpp` finds only three unrelated papers that use "CDFPP" as an acronym in optics and epidemiology, with `full:"speasy"` returning the expected SciQLop-family hits as a positive control and a nonsense term returning none; the developers' publication list at DataCite (creator-keyed on Alexis Jeandet) holds no paper about CDFpp.

**Considered:** the DASH 2026 poster on the SciQLop stack (`10.5281/zenodo.23169249`) has a paragraph on CDFpp but is a poster, which never fills this field (rule 2); it is in Field 27.

---

### 15. License (RECOMMENDED)
`MIT License`

**Rules 1 and 3.** The current licence is MIT: `COPYING` at the pin is the MIT text ("Copyright (c) 2024 Laboratory of Plasma Physics, Ecole Polytechnique, CNRS, Sorbonne Université, Université Paris-Saclay"); the source headers carry the same MIT permission notice; `pyproject.toml` declares `license = {file="COPYING"}` with the classifier `License :: OSI Approved :: MIT License`; GitHub detects `MIT`; the Zenodo deposit declares `mit-license`.

**Licence history — durable context, not a candidate value.** `COPYING` held the GNU GPL v3 from commit `d43232f111595bc706fe2e9e2e69304c387584d4` (2019-12-15, the day of the first commit) until commit `8a788b1d48ee3172efc264a4a5551e0647f3bcbd` (2024-10-24) replaced it with MIT; `v0.7.4` is the last release under GPL-3.0 and `v0.7.5` the first under MIT. Early PyPI releases and Zenodo deposits made before v0.7.5 may therefore state the GPL; that explains any disagreement found there and must not be "restored" (rule 8: never correct backwards to an earlier licence).

---

### 16. Keywords (OPTIONAL)
- `cdf`
- `c++`
- `nasa`
- `python`
- `sciqlop`
- `space`
- `tt2000`
- `webassembly`
- `pyhc package`

**Project-declared terms (rule 9) — the repository's GitHub topics** are `cdf`, `cpp-library`, `cpp17`, `nasa`, `plasma-physics`, `python`, `sciqlop` and `space`; the PyHC registry entry's `keywords` is `["cdf"]`. There are no keywords in `pyproject.toml` and no Zenodo subjects.
- `cdf`, `nasa`, `python`, `sciqlop`, `space` — accurate (the software implements NASA's CDF, is a Python package, and is a SciQLop project); kept as declared even where they overlap Fields 13 and 18, which rule 9 permits (rules 6–7 govern only terms the extractor proposes). Each is an existing keyword row.
- `cpp-library` → `c++` (rule 11). GitHub topic slugs cannot contain `+` or spaces, so `cpp-library` is the topic spelling of "C++ library"; the existing `c++` row carries the term's distinguishing content. Minting `cpp-library` (a machine slug) or `c++ library` (a respelling) was rejected, in the spirit of rule 3's ban on minting registry machine spellings.
- `cpp17` — excluded (rule 4): stale. The library requires C++20 (`meson.build` `cpp_std=c++20`, README "C++20", `pyproject.toml` `-Dcpp_std=c++20`), so the term promises a compatibility the code does not have.
- `plasma-physics` — excluded (rule 4): a word-anchored sweep of the pinned tree for `plasma` (notebooks and fixtures excluded) matches only the copyright holder's name "Laboratory of Plasma Physics" in `COPYING` and the source headers, and no project description uses the term. It names the developing laboratory, not anything the format library does.

**Added domain terms (rule 10):**
- `tt2000` — CDF's leap-second-aware time type; the software's headline SIMD conversions (`to_tt2000`, `to_datetime64`, `include/cdfpp/chrono/`) are exactly what a searcher typing it needs. No row existed in any variant before this entry, so it is added lower-case (rule 12).
- `webassembly` — the WebAssembly build, its JavaScript module and the in-browser Explorer; no other field can carry it (Fields 20 and 21 have no WebAssembly row). No row existed in any variant before this entry (nor `wasm` or `pyodide`), so it is added lower-case.

**PyHC marker (rule 15):** `pyhc package` — the software is listed in the PyHC registry's `_data/projects.yml`.

**Considered and not added (rule 6 — restates another field):** `common data format`, `nasa cdf` and `istp` (rows exist) restate Fields 18/19 (`CDF`, `ISTP-Compliant`); `s3` and `cloud` restate Field 17 (`S3/Cloud-aware`); `space physics` and `heliophysics` are catalogue-wide generics (rule 7). `cdflib`, `xarray` and `sunpy` are other packages (Fields 29/30).

---

### 17. Data Sources (OPTIONAL)
- `S3/Cloud-aware`

**Rules 2 and 7.** `pycdfpp.load` reads CDF files in place from cloud object stores: given an `s3://` (or `gs://`, `az://` …) URL it opens the store through fsspec and fetches only the byte ranges the parser needs (`pycdfpp/__init__.py` `load`; `pycdfpp/_remote.py` `FsspecReader`, which reads public S3 buckets anonymously when no AWS credentials exist; the `[s3]` extra pulls `fsspec` and `s3fs`). The cdflib layer keeps cdflib's S3 support (`pycdfpp/cdflib/s3.py`). The README and `docs/reading.rst` document it on NASA HelioCloud's S3 bucket. This is a user-called access route present in the pinned tree.

**The other rows, each with a verdict:**
- `HTTP/HTTPS Directories` — not selected (rule 9). `pycdfpp.load` and the Explorer also fetch a single `https://` file URL the user supplies, but nothing builds paths under a directory tree or lists one; the capability is already carried by Field 4's `Data Access and Retrieval`.
- `CDAWeb` — not selected (rule 2): no CDAWeb client exists; CDAWeb appears only in example URLs (the docs' ACE file, HelioCloud's S3 copy of the SPDF archive, the Explorer's demo presets in `wacdfpp/presets.js`) and in the ISTP guide's prose.
- `Observatory/Mission-specific` — not selected: the software is mission-agnostic (Fields 31/32).
- `Other` — not selected: no other real source is reached.
- `AMDA`, `das2`, `FTP/FTPS Directories`, `GFZ`, `HAPI`, `Madrigal`, `OMNIWeb`, `SSCWeb`, `TAP`, `The Virtual Solar Observatory.`, `VirES`, `WDC` — no client or reference in the code.

---

### 18. Input File Formats (RECOMMENDED)
- `CDF`
- `ISTP-Compliant`

**Rules 5 and 7.**
- **CDF** — the loader reads CDF versions 2.2 through 3.x, row and column major, GZip- and RLE-compressed files and variables, from a path, an in-memory buffer or a remote reader (`include/cdfpp/cdf-io/loading/`, `pycdfpp.load`, `cdf::io::load`, the cdflib layer's `CDF`, the Explorer).
- **ISTP-Compliant** — the software reads the SPDF ISTP conventions: CDFpp Explorer groups variables by ISTP `VAR_TYPE` and plots by `DEPEND_0`, `DEPEND_k`, `DISPLAY_TYPE`, `SCALETYP`, `FILLVAL`, `VALIDMIN` and `VALIDMAX`; `pycdfpp.cdflib.xarray.cdf_to_xarray` builds coordinates from `DEPEND_n` and `LABL_PTR_n` (`pycdfpp/cdflib/xarray/cdf_to_xarray.py`).

**Not selected:** no other format is read. `xarray_to_cdf` takes an in-memory `xarray.Dataset`, not a file; the experimental zstd/blosc2/lz4 codecs are compressions inside CDF files, not formats; the `.txt` files in `tests/resources/` are reference captures for tests (rule 1).

---

### 19. Output File Formats (RECOMMENDED)
- `CDF`
- `ISTP-Compliant`
- `csv`
- `JSON`
- `Other` — YAML (the Explorer's metadata skeleton)

**Rules 6 and 7.**
- **CDF** — `pycdfpp.save` / `cdf::io::save` write CDF files, uncompressed or compressed, to disk or to bytes (`include/cdfpp/cdf-io/saving/`); `pycdfpp.cdflib.cdfwrite.CDF` and `xarray_to_cdf` write through them; the Explorer's "Convert codec" panel offers the re-encoded file for download. CI validates CDFpp-written files with NASA's `cdfvalidate` (Field 30).
- **ISTP-Compliant** — the documentation targets writing ISTP files (`docs/istp.rst` "Producing ISTP-compliant files", with a complete example that passes AstraLint's ISTP checks; `docs/masters.rst` on filling master CDFs), and `xarray_to_cdf` runs cdflib's ISTP checks on the way (`pycdfpp/cdflib/xarray/_istp.py`).
- **csv** and **JSON** — CDFpp Explorer exports the plotted data of a variable as `<name>.csv` or `<name>.json` (`wacdfpp/plot-model.js` `toCSV` / `toJSON`; download buttons in `wacdfpp/plot.js`).
- **Other (YAML)** — the Explorer's "Export YAML" writes `<file>.skeleton.yaml`, the file's structure and attributes without data (`wacdfpp/cdf-yaml.js`, `wacdfpp/app.js`); YAML has no row.

**Not selected:** `pycdfpp.to_dict_skeleton` returns an in-memory dict that the caller may serialise (rule 5); `cdfdump` and `cdfdump --irsdump` print text dumps to standard output, not data files; `cdf_to_xarray` returns an in-memory `xarray.Dataset` whose save format is the caller's choice (rule 5).

---

### 20. Operating System (RECOMMENDED)
- `Linux`
- `Mac`
- `Windows`

**Rule 4 — compiled extension; the OSes it is built, tested and published for.** PyPI 0.20.0 ships wheels for `manylinux` and `musllinux` (x86_64, aarch64), `macosx_13_0` (x86_64, arm64), and `win_amd64` / `win_arm64`. CI tests run on `ubuntu-latest`, `ubuntu-24.04-arm`, `macos-15-intel`, `macos-latest`, `windows-latest` and `windows-11-arm` (`.github/workflows/CI.yml`, plus `tests-windows.yml`); the README's "Packages & CI" table names the same platforms.

**Not selected:** `Operating System Independent` — never for a compiled extension (rule 4), even though CDFpp Explorer runs in any browser and Pyodide `wasm32` wheels exist (an `os:` search finds the three named rows); `Solaris`, `MobilePlatform`, `Other` — no evidence (rule 7).

---

### 21. CPU Architecture (RECOMMENDED)
- `x86-64`
- `Apple Silicon arm64`
- `Linux aarch64 or arm64`

**Rule 5 — prebuilt binaries with architecture-specific code.** The package carries architecture-specific code (x86 SIMD kernels with AVX-512/AVX2/SSE2 runtime dispatch in `src/arch/x86/`, NEON kernels in `src/arch/arm/`), so rule 4's portable-source branch does not apply and `CPU Independent` is excluded. The published artifacts map as follows: wheels `manylinux_*_x86_64`, `musllinux_*_x86_64`, `macosx_13_0_x86_64` and `win_amd64` → `x86-64`; `macosx_13_0_arm64` → `Apple Silicon arm64`; `manylinux_*_aarch64` and `musllinux_*_aarch64` → `Linux aarch64 or arm64`. CI builds and tests each of these on matching runners (`macos-latest` for Apple Silicon, `ubuntu-24.04-arm` for Linux arm64).

**Published architectures with no row, recorded and not mapped:**
- `win_arm64` wheels (built and tested on `windows-11-arm`) — the vocabulary's arm64 rows are qualified by OS (Apple Silicon, Linux), and neither describes Windows on ARM.
- `wasm32` Pyodide wheels (`pyemscripten_*_wasm32`) and the `wasm32`/`wasm64` JavaScript module attached to the releases — WebAssembly has no row.

`Other` was not added for them: it would tell a searcher nothing that the two arm64 rows and the `webassembly` keyword (Field 16) do not already say. `GPU` and `HPC or HEC` do not apply (CPU threads only; no CUDA, offload, MPI or scheduler).

---

### 22. Related Phenomena (OPTIONAL)
Not found — evidenced empty.

None of the seven rows applies (`Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`, `X-ray emission`). A file-format implementation analyses, models or detects no phenomenon (rule 5 cannot fire), and its relation to every row is identical and indirect (rule 3). The Explorer's demo presets (an OMNI SYM-H geomagnetic-index file, a Solar Orbiter magnetic-field file) are example data (rule 4).

---

### 23. Development Status (RECOMMENDED)
`Active`

**Rule 6.** No successor pointer, no archive flag (GitHub `archived: false`), no repostatus.org badge and no status statement in the README or docs (rules 1–4 do not fire). The software reached a stable, usable state long ago (releases since 2020, on PyPI since 2020; the `Development Status :: 5 - Production/Stable` classifier corroborates a release but is not mapped). Dated anchors: the last commit on the default branch `main` is `3fcc975e603dc59627bb073f16f301db281d0b9a` (2026-11-03T23:18:42Z), and the latest release is `v0.20.0` (2026-11-03) — under six months, so `Active`.

---

### 24. Documentation (RECOMMENDED)
`https://pycdfpp.readthedocs.io/en/latest/`

**Rule 3 — the project's own documentation site.** Named in `pyproject.toml` `[project.urls] documentation` (and so in PyPI's `project_urls`), linked from the README's documentation badge and from its documentation link above the highlights, built from this repository by `.readthedocs.yaml` (Sphinx, `docs/conf.py`), and given as the PyHC registry `docs:`. It is the documentation home without a redirect, titled with the release version, with installation, quickstart, reading and writing guides, the ISTP and master-CDF guides, the C++ guide and the WebAssembly/Explorer pages. Rule 6: the `/en/latest/` landing page is the project's own declared form.

**Considered and not used:** `https://sciqlop.github.io/CDFpp/` (the GitHub "homepage", which is the CDFpp Explorer app, not documentation); the GitHub wiki (`has_wiki` is set, but rule 4 applies only when nothing else documents the software, and the Read the Docs site does).

---

### 25. Funder (OPTIONAL)
Not found — evidenced empty.

**Rule 12 — no qualifying source attributes funding to CDFpp.** A case-insensitive sweep of the pinned tree (notebooks, fixtures and the `subprojects/` wraps excluded) for `fund`, `CNES`, `ANR`, `acknowledg`, `grant`, `sponsor`, `support(ed) by` and `financ` finds, beyond the MIT notice ("Permission is hereby granted"), only the ISTP `Acknowledgement` attribute in `docs/istp.rst`'s example and checklist, the same attribute's value in a test (`tests/simple_open/main.cpp`), and the word "fundamental" in a code comment — no funding statement anywhere. DataCite `fundingReferences` is empty for the concept and the v0.20.0 deposit; the Zenodo record has no grants. The developers' DASH 2026 poster (Field 27) acknowledges no funder; its text names CDPP only as a data service (CDPP 3DView).

**Considered and rejected, with their actual roles, so a later refresh does not reintroduce them:**
- **CDPP (Centre de Données de la Physique des Plasmas)** and **Plas@Par (Fédération de recherche PLAS@PAR, `https://ror.org/02rmk5x23`)** — the READMEs of Speasy ("The development of Speasy is supported by the CDPP") and of the SciQLop application ("The development of SciQLop is supported by the CDPP." and "We acknowledge support from the federation Plas@Par") credit them for those packages. No source extends the support to CDFpp, and treating CDFpp as covered by the SciQLop application's credit would be inference (rule 8 needs a source attesting both links).
- **Laboratory of Plasma Physics, École polytechnique, CNRS, Sorbonne Université, Université Paris-Saclay** — copyright holders in `COPYING` (a copyright holder is not a funder).
- **ANR (Agence Nationale de la Recherche)** — appears only in Nicolas Aunai's ORCID as the funding of his 2013–2014 postdoctoral position: person-level support, unrelated to this software (rule 3).

---

### 26. Award Title (OPTIONAL)
Not found — evidenced empty.

**Rule 8.** No award title or number appears in the repository, the DataCite or Zenodo records, or the DASH 2026 poster (the same sweep as Field 25). No award is supplied as a default.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- `https://doi.org/10.5281/zenodo.23169249`

**Rule 3 — the developers' own publication about the platform the software serves.** Jeandet, A., Aunai, N., Génot, V., Renard, B., Bouchemit, M., & André, N. (2026). *The SciQLop ecosystem: a layered open-source stack for in-situ heliophysics data.* Poster, Data, Analysis, and Software in Heliophysics (DASH) 2026. Zenodo. Deposited as the poster itself (Zenodo resource type `poster`, files `poster_DASH2026_jeandet.pdf` and `poster_pitch_DASH2026_jeandet.pdf`, issued 2026-10-05), so it is an eligible publication type. Two of its authors are CDFpp authors (Jeandet, Aunai). It presents the SciQLop stack layer by layer, and CDFpp is one of the layers with its own panel: the record's abstract describes it as "a from-scratch, MIT-licensed, thread-safe C++20 CDF implementation with full read and write support and SIMD-accelerated epoch conversion, usable from C++, from Python as `pycdfpp` … and from JavaScript through a WebAssembly build", and the poster's panel "pycdfpp: faster reads, smaller archives" gives its benchmarks and its use in the Solar Orbiter LFR calibration code and by BepiColombo MSA, and the poster states that pycdfpp output is checked by NASA's `cdfvalidate` in CI. The rest of the poster covers AstraLint, Speasy, SciQLopPlots, tscat, cocat and the SciQLop application.
- **Identifier choice:** `10.5281/zenodo.23169249` is the version DOI of the poster's deposit (concept `10.5281/zenodo.23169248`). The Speasy entry records the same version DOI, so the two entries share one related item.

**Weighed and not added:**
- *ISTP Metadata Guidelines: Current Status and Future Development* (Koval, A., et al., 2026, `10.5281/zenodo.23111203`, a presentation; Alexis Jeandet is one of its 26 authors) — its subject, by its title and record, is the ISTP metadata conventions, not CDFpp (rule 6).
- *Ground-based and space-based radio spectra in SciQLop* (`10.5281/zenodo.23150226`) and *Agentic LLM workflows inside SciQLop* (`10.5281/zenodo.23196188`) — the developers' DASH 2026 presentations about the SciQLop application; their records do not mention CDFpp.
- The SciQLop EGU 2022–2025 and EPSC-DPS 2025 contributions (`10.5194/egusphere-egu22-5774`, `-egu23-13581`, `-egu24-3515`, `-egu25-10101`, `10.5194/epsc-dps2025-1422`) — meeting abstracts (rule 1) about SciQLop and Speasy.
- *Python in Heliophysics Community (PyHC): Current status and future outlook* (Barnum et al. 2023, `10.1016/j.asr.2022.10.006`) — the ADS full text does not mention CDFpp.

**Uses (rule 5):** none found. ADS `full:` and `ack:` searches for `pycdfpp` and `CDFpp` return no paper that uses the software (the only `CDFpp` hits are unrelated acronyms); the control `full:"speasy"` returns Speasy's known uses, and a nonsense term returns none. Downstream software that builds on CDFpp is in Field 30.

---

### 28. Related Datasets (OPTIONAL)
Not found — evidenced empty.

CDFpp is a reader and writer for a file format, not a reader built for any dataset (rule 3's premise), and it produced no dataset (rule 5). The real dataset files in `tests/resources/` (ACE SIS `ac_h2_sis_20101105_v06.cdf`, Geotail CPI `ge_k0_cpi_19921231_v02.cdf`, Interball `ia_k0_epi_19970102_v01.cdf`, and SPDF master CDFs of ACE MFI, Solar Orbiter RPW, THEMIS ground magnetometers, Ulysses SWOOPS and Wind) were chosen for structural variety; the docs' running example (ACE MFI H0, `ac_h0_mfi_20200101_v07.cdf`) and the Explorer's demo presets are examples. Listing any of them would claim a specialisation the software does not have.

---

### 29. Related Software (OPTIONAL)
- `https://cdf.gsfc.nasa.gov/`
- `https://github.com/lasp/cdflib`
- `https://github.com/spacepy/spacepy`

**Rule 9 — similar-purpose tools the project itself names as the alternatives:**
1. `https://cdf.gsfc.nasa.gov/` — **NASA's CDF library**, the official C implementation. The README positions CDFpp against it directly: "A modern, from-scratch C++20 implementation of NASA's CDF … Why another CDF library? NASA's official C implementation has no multi-thread support …, an aging C89 interface, and a license incompatible with most Linux distribution policies. CDFpp solves all three". It has no public source repository and no DOI was found (a DataCite title search for "Common Data Format" software returns CommonDataFormat.jl, COMFORD and ESCDF, none of them NASA's library), so its home page is recorded (rule 12(c)), in the form the README links and the form CDFlib's entry already uses.
2. `https://github.com/lasp/cdflib` — **CDFlib** (in the catalogue; its stored `code_repository_url`, rule 11). The README benchmarks pycdfpp "Compared with spacepy and cdflib", and `pycdfpp.cdflib` reimplements cdflib's API as a drop-in replacement. CDFlib's concept DOI `https://doi.org/10.5281/zenodo.1481144` was passed over because the site shows the raw URL (rule 13). The README and release notes link cdflib's former location `https://github.com/MAVENSDC/cdflib`, which redirects; the in-catalogue string is used.
3. `https://github.com/spacepy/spacepy` — **SpacePy** (in the catalogue, rule 11), named in the same benchmark section as the other comparable CDF library: its `spacepy.pycdf` module, a wrapper of NASA's library. Concept DOI `https://doi.org/10.5281/zenodo.3252523` passed over (rule 13).

**Reverse relations:** when this dossier was written, CDFlib's entry listed CDFpp as a same-purpose peer, and Speasy's and PyRFU's entries listed it as a dependency. CDFlib is reciprocated here; Speasy and PyRFU consume CDFpp, which is a Field 30 relation (rule 3), recorded there.

**Considered and not added:**
- AstraLint, PyISTP, PyRFU, Speasy, SunPy, SwarmPAL and xarray — the relation is a demonstrated exchange, which belongs in Field 30 alone (rule 3).
- SciQLop (`https://github.com/SciQLop/SciQLop`) — same organisation and the application of the stack CDFpp belongs to (its README lists CDFpp as a stack component), but it imports CDFpp only through Speasy; organisation membership is not a relation (rule 8).
- CDFDatasets.jl (`JuliaSpacePhysics/CDFDatasets.jl`, by co-author Zijin Zhang) — had a pycdfpp backend, removed in its v0.4.0 (its GitHub release notes: "The PyCDFpp backend and the backend keyword of CDFDataset are removed."); not a current relation (rule 7).
- CommonDataFormat.jl, pysatCDF and sammi-cdf — other CDF readers, not named by this project (rule 4).
- pybind11, xsimd, libdeflate, fmt, zlib, zstd, lz4, c-blosc2, Catch2, hedley, `cpp_utils`, fsspec, s3fs, uPlot, Pyodide/emscripten-forge — generic build, compression, I/O, plotting and packaging infrastructure (rule 1); numpy is Tier A.

---

### 30. Interoperable Software (OPTIONAL)
- `https://github.com/SciQLop/AstraLint`
- `https://github.com/lasp/cdflib`
- `https://cdf.gsfc.nasa.gov/`
- `https://github.com/louis-richard/irfu-python`
- `https://github.com/SciQLop/speasy`
- `https://github.com/sunpy/sunpy`
- `https://github.com/pydata/xarray`
- `https://github.com/SciQLop/PyISTP`
- `https://github.com/Swarm-DISC/SwarmPAL`
- `https://github.com/SciQLop/sciqlop-plugins`
- `https://github.com/nicolasaunai/sciqlop-vdf`
- `https://github.com/Beforerr/space-analysis.py`

**Rule 7 — a demonstrated exchange with a named domain tool, each with its evidence:**
1. **AstraLint** (`https://github.com/SciQLop/AstraLint`; not catalogued in HSSI when this dossier was written, no DOI found) — an ISTP/PDS4 conformance linter. CDFpp Explorer's **Validate** button hands the loaded file to AstraLint's web app, by a `?url=` deep link or by transferring the bytes with `postMessage`, and accepts a CDF handed back (`wacdfpp/astralint.js`, `wacdfpp/app.js`; `docs/explorer.rst` "Validate"); `docs/istp.rst`'s ISTP example "passes the ISTP checks of AstraLint". From the other side, AstraLint declares `pycdfpp>=0.19.0` as a dependency (its `pyproject.toml` at `c25e4c68c2ff6c4165fdda17ba31ea560911a608`).
2. **CDFlib** (`https://github.com/lasp/cdflib`, in the catalogue) — `pycdfpp.cdflib` mirrors cdflib 1.3.16's API and shares its data model: "cdflib itself is needed: pycdfpp.cdflib reuses its leap second table and its data classes", and `pycdfpp.cdflib.dataclasses` and `epochs_astropy` "are cdflib's own modules, so the objects you get are cdflib's" (`docs/cdflib.rst`); the `[cdflib]` extra pulls `cdflib>=1.3.16,<2`; `tests/python_cdflib_api/` checks API parity against the installed cdflib; files written back are read by both ("writing it back makes a file that pycdfpp and cdflib read"). Listed in Field 29 too, on its own ground (a named alternative) — rule 9.
3. **NASA's CDF library** (`https://cdf.gsfc.nasa.gov/`) — CI builds NASA's CDF 3.9.2 toolkit and validates CDFpp-saved files with its `cdfvalidate` (`.github/workflows/tests-with-nasa-cdf-validation.yml`, `tests/nasa_cdf_validation/validate.py`); `cdfdump --irsdump` reproduces NASA's `cdfirsdump` output byte for byte, tested against real captures (`include/cdfpp/cdf-io/debug/nasa_compat_repr.hpp`, `tests/resources/*cdfirsdump*`). Listed in Field 29 too, on its own ground — rule 9.
4. **PyRFU** (`https://github.com/louis-richard/irfu-python`, in the catalogue) — the consumer side: PyRFU builds its MMS data loading on pycdfpp (`pycdfpp>=0.9.0` in its `pyproject.toml`; `from pycdfpp import load` and `to_datetime64` in `pyrfu/mms/get_ts.py`, `get_dist.py`, `db_get_ts.py`, `get_eis_allt.py`, at `89b5f7042513a64f15b55b69ee466146c3995338`; its changelog: "cdflib is no longer used: CDF time conversions use pycdfpp …"). PyRFU's own entry lists CDFpp in its Related Software. Concept DOI `https://doi.org/10.5281/zenodo.10678694` passed over (rule 13).
5. **Speasy** (`https://github.com/SciQLop/speasy`, in the catalogue) — the consumer side: Speasy's ISTP CDF codec writes Speasy variables to CDF through pycdfpp (`speasy/core/codecs/bundled_codecs/istp/cdf.py`: `pycdfpp.CDF()`, TT2000 time axes, gzip-compressed variables, `pycdfpp.save`), and its docs show a custom archive reader built on `pycdfpp.load(any_loc_open(url, …).read())` and `pycdfpp.to_datetime64` (`docs/user/direct_archive/direct_archive.rst`), at `b76618e8914f8cd4c0ec5310340ea262d32009dc`; `pycdfpp>=0.15.0` is a dependency. Speasy's entry lists CDFpp in its Related Software. Concept DOI `https://doi.org/10.5281/zenodo.4118780` passed over (rule 13).
6. **SunPy** (`https://github.com/sunpy/sunpy`, in the catalogue) — a documented import path: `pycdfpp.cdflib.install()` places pycdfpp's cdflib layer in `sys.modules` under the `cdflib` names, so SunPy's CDF reader, which imports `cdflib` and `cdflib.epochs.CDFepoch` (`sunpy/io/_cdf.py` at `edd0449c375ea109ec74bfe0f3fefc6781861e28`), runs on pycdfpp; the README, `docs/cdflib.rst` (with an example importing `sunpy.io._cdf` after `install()`) and the v0.20.0 release notes all name SunPy. Concept DOI `https://doi.org/10.5281/zenodo.591887` passed over (rule 13).
7. **xarray** (`https://github.com/pydata/xarray`; Tier B, admitted under rule 4) — a documented interchange type: `pycdfpp.cdflib.xarray.cdf_to_xarray` returns an `xarray.Dataset` and `xarray_to_cdf` writes one, shown as an "xarray round trip" in `docs/cdflib.rst` and checked by `tests/python_cdflib_api/test.py` `test_xarray_api`. Concept DOI `https://doi.org/10.5281/zenodo.598201` passed over (rule 13).
8. **PyISTP** (`https://github.com/SciQLop/PyISTP`; not catalogued in HSSI when this dossier was written, no DOI found) — "An ISTP standard layer for CDF files" (its GitHub description) whose default CDF backend is pycdfpp: a driver written against this software (`pyistp/drivers/pycdfpp.py`), a README stating it "Loads ISTP-compliant CDF files (via pycdfpp by default, or spacepy)", and `pycdfpp>=0.6.0` among its dependencies, at `6e9d4b9deba63c69ad1ea1ba3f754cb731741965`. The exchange is seen from PyISTP's side (rule 7). When this dossier was written, Speasy's entry listed PyISTP in its Related Software under this exact URL.
9. **SwarmPAL** (`https://github.com/Swarm-DISC/SwarmPAL`; not catalogued in HSSI when this dossier was written) — "The Swarm Product Algorithm Laboratory: A Python toolbox for ESA's Swarm mission" (its GitHub description). Its CDF interface reads files with `pycdfpp.load` and `pycdfpp.to_datetime64` and writes them with `pycdfpp.CDF()` and `pycdfpp.save` (`src/swarmpal/io/_cdf_interface.py`), its data container's `to_cdf(..., handler="pycdfpp")` makes pycdfpp the default writer (`src/swarmpal/io/_paldata.py`), and `pycdfpp >= 0.7` is a dependency, at `e55bb31f0f4b685267f82f75dfdcdeafef607dac`. Concept DOI `https://doi.org/10.5281/zenodo.7826899` passed over (rule 13).
10. **SciQLop plugins — CDF Workbench** (`https://github.com/SciQLop/sciqlop-plugins`; SciQLop's official plugin collection, not catalogued in HSSI when this dossier was written, no DOI found) — its `cdf_workbench` plugin, packaged as `sciqlop-cdf-workbench` 0.7.0, is a "Multi-function CDF file explorer for SciQLop" built on pycdfpp: its README says it opens "a CDF (local path, URL, or raw bytes via `pycdfpp`)", `cdf_workbench/cdf_workbench/loader.py` loads every file through `pycdfpp.load` into the `pycdfpp.CDF` objects its editing, codec-comparison and export modules work on, and its `pyproject.toml` declares `pycdfpp>=0.18.0`, at `1758457e54e85baff312d63e28ffc18d878d5495`. The collection's repository root is recorded because the plugin lives in a subdirectory of it (Field 29 rule 12(a): never a `/tree/` sub-path).
11. **sciqlop-vdf** (`https://github.com/nicolasaunai/sciqlop-vdf`; by CDFpp author Nicolas Aunai, not catalogued in HSSI when this dossier was written, no DOI found) — a "Velocity distribution function (VDF) viewer for SciQLop" (its README) whose Solar Orbiter SWA-PAS source reads each day's file with `pycdfpp.load` and `pycdfpp.to_datetime64` (`sciqlop_vdf_solo/pas.py` `_load_day`); `pycdfpp` is a dependency, at `32a1bcdcba20253ebc8ed273cb7070f2a99ef29b`.
12. **space-analysis** (`https://github.com/Beforerr/space-analysis.py`; by CDFpp author Zijin Zhang, published on PyPI as `space-analysis`, not catalogued in HSSI when this dossier was written) — a "Python library for data analysis in space physics" (its `pyproject.toml` description) whose `space_analysis.io.cdf` module lists a file's ISTP data variables (`inspect_cdf`) and turns CDF variables into a polars DataFrame (`cdf2pl`) through `pycdfpp.load` and `pycdfpp.to_datetime64`; `pycdfpp` is in its `io` extra, at `af98556bdccf6aa9aec974f1f50c783e2c153bc9`.

**Considered and not added:**
- numpy (zero-copy NumPy arrays, the buffer protocol) and pandas — Tier A (rule 1).
- astropy — `epochs_astropy` is cdflib's own module, passed through unchanged; pycdfpp itself exchanges nothing with astropy (rule 4).
- SciQLop — reaches CDFpp only through Speasy (no import of its own); recorded in neither field.
- Pyodide, JupyterLite, emscripten-forge, Binder, Jupyter, fsspec, s3fs, botocore, matplotlib (used in notebooks) — generic runtimes, packaging and I/O plumbing (rules 1–2).
- CDFDatasets.jl — its pycdfpp backend was removed in v0.4.0, so no current exchange exists (see Field 29).
- **What a wider search found, and what it left open.** A GitHub code search for `pycdfpp` returns a capped, ranked set of hits, not every dependent. Among its hits, the domain tools whose own code reads or writes through pycdfpp are entries 1, 4, 5 and 8–12 above. Three more were assessed and not added:
  - `arvidwennerstrom/RPWI_calibration` — a personal set of calibration scripts with no README, description or packaging, one of which reads Langmuir-probe CDF files with `pycdfpp.load` (`LP_data_creation.py`, at `87ca67a3b574178ceafde5e6ca8b0a94c7e63821`); there is no tool here for a user to combine with CDFpp.
  - `SciQLop/space_ouija` ("A toolkit to read really old space data files") — pycdfpp appears only in documentation scaffolding copied from CDFpp's docs and in one example notebook that writes MESSENGER FIPS data to CDF (`docs/examples/MessengerFIPS_EDR.ipynb`); the package declares no pycdfpp dependency and none of its Python modules imports it, at `17b2749297f85d7989339bba3d572d70ac80bb39`. A docs-only use is not an exchange.
  - `SciQLop/speasy_proxy` (Speasy's caching proxy server) — declares `pycdfpp>=0.16.0`, but its own code produces CDF through Speasy's codec (`get_codec('application/x-cdf')` in `speasy_proxy/api/v1/get_data.py`) and imports pycdfpp only in a test (`test_encode_cdf.py`), at `e4193fdfd85ccb9c1ee9c6877bcac411bb1b1346`; that exchange is Speasy's, recorded above.

  Hits that only list pycdfpp as a dependency are not exchanges: JupyterLite environments (`SciQLop/Speasy-lite`, `jeandet/speasy-xeus_lite`), the requirements of the catalogued Helio-Lite (`indiajacksonphd/Helio-Lite`), packaging recipes and indexes (Pyodide, emscripten-forge, PyScript, the Julia General registry, wheel and PyPI crawlers) and PyHC environment repositories. The remaining hits, judged by repository name only (course assignments, workshop material, AI-tooling and agent-skill collections), were not assessed, so a later refresh may still find further tools built on CDFpp.

---

### 31. Related Instruments (OPTIONAL)
Not found — evidenced empty.

**Stage A, rule 2 — an instrument-agnostic tool.** CDFpp reads and writes any CDF file; no reader, calibration or code branch is written for any instrument. Instrument names in the tree are examples and fixtures (rule 3): the Explorer's demo presets (MMS1 EDP and FPI, THEMIS-A ESA, Solar Orbiter MAG, OMNI SYM-H, Cluster C1 FGM in `wacdfpp/presets.js`), the docs' ACE MFI example, test fixtures (ACE MFI and SIS, Geotail CPI, Interball EPI, Solar Orbiter RPW LFR, THEMIS ground magnetometers, Ulysses SWOOPS, Wind), and a comment on an MMS file in `loading.hpp`. Use by the Solar Orbiter LFR calibration code and BepiColombo MSA (Field 4) makes those missions' pipelines users of CDFpp, not instruments CDFpp is designed to support.

**Vocabulary sweep** (the production vocabulary, every row SPASE-identified and none in `.html` form when this dossier was written): word-anchored over `name`, `abbreviation`, `identifier` and `definition`, `CDFpp` and `pycdfpp` match no row; controls: `SUVI` matches its GOES rows, and a nonsense term matches nothing. Rows that exist and are deliberately not used, so a later refresh sees a settled relevance decision: `Fast Plasma Investigation` (e.g. `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MMS1/FPI`) and the other example instruments' rows.

---

### 32. Related Observatories (OPTIONAL)
Not found — evidenced empty.

Field 31's Stage A applies unchanged: CDFpp is mission-agnostic, and missions appear only as examples, fixtures and downstream users. Rows that exist and are deliberately not used: `Magnetospheric Multiscale` (`https://spase-metadata.org/SMWG/Observatory/MMS`), `MMS-1` (`https://spase-metadata.org/SMWG/Observatory/MMS/1`), `Solar Orbiter` (`https://spase-metadata.org/ESA/Observatory/SolarOrbiter`), `Advanced Composition Explorer` (`https://spase-metadata.org/SMWG/Observatory/ACE`), `Time History of Events and Macroscale Interactions during Substorms A` (`https://spase-metadata.org/SMWG/Observatory/THEMIS/A`), `Cluster` (`https://spase-metadata.org/SMWG/Observatory/Cluster`), `OMNI` (`https://spase-metadata.org/SMWG/Observatory/OMNI`). Field 17 accordingly carries no `Observatory/Mission-specific` (rule 6).

---

### 33. Logo (OPTIONAL)
Not found — documented omission.

**Rule 6.** No image is presented as the project's logo:
- `docs/conf.py` sets no `html_logo` and the Furo theme options set no logo; the rendered docs header shows the title text only.
- No file in the tree is named for a logo, and the README has no header image (badges only).
- The PyHC registry entry has no `logo:` key.
- CDFpp Explorer's page shows no mark of its own.

**Rejected candidates, with URLs:**
- `https://raw.githubusercontent.com/SciQLop/CDFpp/3fcc975e603dc59627bb073f16f301db281d0b9a/docs/_static/CDF_loading_nb_thumbnail.png` (`image/png`, 116,759 bytes) — a matplotlib line plot of three field components over one day, named as a notebook thumbnail; the docs stopped referencing it in the 2026-09-25 rewrite (`36e1591`), and nothing in the tree references it at the pin. A figure, not a logo (rule 4).
- `https://raw.githubusercontent.com/SciQLop/AstraLint/main/logo.png` — AstraLint's logo, shown as a small icon on the Explorer's Validate button (`wacdfpp/wacdfpp.html`); another project's mark (rule 5).
