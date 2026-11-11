# HSSI Metadata Extraction Results

**HSSI Software ID:** 8e349bce-5860-4c0b-9ee9-ebb684574262
**Repository:** https://github.com/wtbarnes/fiasco
**Source Revision:** 1a1965066b192360bdc3681e128dec91d1a4ead0
**Extraction Date:** 2026-07-26
**Validation Date:** 2026-11-11
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** To be filled by actual submitter
- **Submitter Email:** To be filled by actual submitter
- **Source:** The HSSI view record does not expose submitter information.

### 2. Persistent Identifier (RECOMMENDED)
- https://doi.org/10.5281/zenodo.7504257
- **Source:** Existing HSSI record, repository DOI badge, DataCite, and Zenodo. This is the concept DOI for all fiasco releases.
- **Concept presentation:** DataCite's concept record presents version `v0.9.0` with title `fiasco` (read 2026-11-11), the current release (Field 12), and its `HasVersion` list includes that release's deposit.

### 3. Code Repository (MANDATORY)
- https://github.com/wtbarnes/fiasco
- **Source:** Existing HSSI record, git remote, repository metadata, Zenodo, and PyHC registry.

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Processing
- Models and Simulations
- Models and Simulations:Physics-Based
- Models and Simulations:Theory
- **Source:** Identity-aware union retaining the existing HSSI `Data Processing and Analysis` value and adding current public capabilities. `fiasco.Ion`, `fiasco.Element`, and `fiasco.IonCollection` expose atomic-data analysis, level populations, equilibrium ionization, line ratios, emissivities, intensities, ionization/recombination rates, continua, radiative losses, and synthetic spectra. `fiasco.io.Parser`, `download_dbase`, and `build_hdf5_dbase` retrieve and transform the raw CHIANTI ASCII database into HDF5. The physics-based/theory classifications are supported by the implemented atomic-rate, cross-section, Gaunt-factor, continuum-emission, and ionization-equilibrium calculations.
- **Note:** Data Visualization was considered but not selected: plotting occurs in documentation examples through Matplotlib, while fiasco's public APIs return scientific arrays/tables rather than implementing plot methods. No mission-related, coordinate-transform, or server/environment functionality was found.
- **v0.9.0 (read at `a3445e0b31aef865cb1b3f0008b21d5380abf121`, the commit the `v0.9.0` tag names):** the release ships four capabilities that no 0.8.x release carried: `fiasco.line_ratio` (`fiasco/fiasco.py:215`), the theoretical ratio of one or more bound-bound lines as a function of temperature and density, which the documentation uses as a density diagnostic; `fiasco.get_dem_model` (`fiasco/fiasco.py:98`), which returns a CHIANTI differential-emission-measure model from the HDF5 database as an Astropy `QTable`; `IonCollection.build_line_list` (`fiasco/collections.py:220`), a `QTable` with one row per bound-bound transition of every ion in the collection, its contribution function and, given an emission-measure model, its line-of-sight intensity; and a `proton_electron_ratio` argument on `fiasco.Ion` (`fiasco/ions.py:73`), beside a faster `fiasco.proton_electron_ratio`. They extend the stored `Analysis`, `Energy Spectra`, `Data Access and Retrieval` and `Physics-Based` capabilities and earn no further row: nothing fits a model to data (`Models and Simulations: Forward-Fitting`); the DEM models are CHIANTI's tabulated data, which fiasco returns rather than evaluating an empirical model of its own (`Models and Simulations: Empirical`); no instrument is modelled (`Models and Simulations: Observatory/Instrument Models`); and the Hinode/EIS density example (`examples/user_guide/plot_jet_density_figure.py`) plots only in the documentation gallery (rule 4). `build_line_list` and `get_dem_model` return in-memory tables and write no file, so Field 19 is unchanged too. Until v0.9.0 these four were on `main` only: v0.8.x was released from the `0.8` branch, which leaves `main` at `2ec62afa154c2b8b92cdad415f0b12602b48d1b4` before them, so no value rested on them while v0.8.3 was the current release. The release removes nothing the 0.8.x releases shipped: every `0.8`-branch commit after the branch point backports a `main` commit the tag contains, the three v0.8.3 fixes among them (`2a36a7a`, `185e87c`, `9962995`).
- **v0.8.3 (read at `bf21eb232eb54bca368190753e0e68f1de451f39`):** its three changes fix existing calculations in `fiasco/ions.py` — which levels the free-bound continuum includes, density arrays in the two-photon continuum, and the free-free continuum's solid-angle factor (Field 12) — and neither add nor remove a capability.

### 5. Related Region (MANDATORY)
- Interplanetary Space
- Solar Environment
- Corona
- Solar Wind
- **Order:** listed in HSSI's stored order, which this field keeps.
- **Source:** Identity-aware union retaining the existing HSSI `Solar Environment` value. The repository's developer-maintained works-citing list demonstrates use for solar-wind and coronal-mass-ejection charge-state modeling in interplanetary space.
- **Evidence, Corona:** Every `fiasco.Ion` defaults to the Feldman solar-coronal abundance set (`fiasco/ions.py:65` at `1a1965066b192360bdc3681e128dec91d1a4ead0`; line 70 at `a3445e0b31aef865cb1b3f0008b21d5380abf121`), and the AIA response guide explicitly uses coronal abundances while calculating a solar EUV response (`examples/user_guide/aia_response.py:44` at both revisions).
- **Evidence, Solar Wind:** The developer-maintained citing bibliography includes Rivera et al. (2025), “Differentiating the Acceleration Mechanisms in the Slow and Alfvénic Slow Solar Wind” (`docs/works_citing.bib:80` at `1a19650…`; line 102 at `a3445e0…`), the same curated usage source already used in this dossier to support interplanetary-space charge-state modeling.
- **Removed, `Earth Atmosphere`:** HSSI held it, first in stored order, until the v0.8.2 release update. Its only support was the PyHC registry's Science Area tag `ionosphere_thermosphere_mesosphere` on fiasco's entry in `_data/projects.yml` (`keywords: ["solar","ionosphere_thermosphere_mesosphere","general"]`, read 2026-10-29), and rule 3 does not accept a registry facet tag as evidence for a region. fiasco does nothing in Earth's atmosphere: a word-anchored, case-insensitive sweep of the tree at `a3445e0…` (binary `.asdf` test data excluded) finds no `ionospher*`, `thermospher*`, `mesospher*`, `Earth atmosphere`, `terrestrial`, `airglow` or `aurora*`, and its only `atmospher*` matches are two paper titles in `docs/references.bib` (the AIA calibration paper and “Ultraviolet and X-ray Spectroscopy of the Solar Atmosphere”), while the positive control `corona*` matches five files and a nonsense token matches none. The project describes itself only as “A Python interface to the CHIANTI atomic database” (`pyproject.toml` `description`). No fine Earth-atmosphere row passes rule 4, so rule 5 cannot bring the coarse row either. Do not re-add it from the registry tag; the same tag's three keywords left Field 16 for the same reason.

### 6. Authors (MANDATORY)
- **Author:** Will Barnes
  - **Author Identifier:** https://orcid.org/0000-0001-9642-6089
  - **Affiliations:**
    - American University — https://ror.org/052w4zt36
    - Department of Physics, American University — Identifier not found
    - Goddard Space Flight Center — https://ror.org/0171mag52
    - United States Naval Research Laboratory — https://ror.org/04d23a975
- **Author:** Nabil Freij
  - **Author Identifier:** https://orcid.org/0000-0002-6253-082X
  - **Affiliations:**
    - Lockheed Martin Solar and Astrophysics Laboratory — Identifier not found
    - SETI Institute — https://ror.org/02dxgk712
    - Bay Area Environmental Research Institute — https://ror.org/024tt5x58
- **Author:** Laura Hayes
  - **Author Identifier:** https://orcid.org/0000-0002-6835-2390
  - **Affiliations:**
    - Dublin Institute for Advanced Studies — https://ror.org/051sx6d27
    - European Space Research and Technology Centre — https://ror.org/03h3jqn23
- **Author:** Stuart J. Mumford
  - **Author Identifier:** https://orcid.org/0000-0003-4217-4642
  - **Affiliations:**
    - Aperio Software Ltd. — Identifier not found
    - University of Sheffield — https://ror.org/05krs5044
- **Author:** Nicholas A. Murphy
  - **Author Identifier:** https://orcid.org/0000-0001-6628-8033
  - **Affiliations:**
    - Center for Astrophysics, Harvard & Smithsonian — https://ror.org/03c3r2d17
    - Smithsonian Astrophysical Observatory — https://ror.org/04mh52z70
    - Smithsonian Institution — https://ror.org/01pp8nd67
- **Author:** Jeffrey Reep
  - **Author Identifier:** https://orcid.org/0000-0003-4739-1152
  - **Affiliations:**
    - University of Hawaii at Manoa — https://ror.org/01wspgy28
- **Author:** David Stansby
  - **Author Identifier:** https://orcid.org/0000-0002-1365-1908
  - **Affiliations:**
    - Advanced Research Computing Centre, University College London, UK — Identifier not found
    - Department of Mechanical Engineering, University College London — Identifier not found
    - Imperial College London — https://ror.org/041kmwe10
    - Mullard Space Science Laboratory, University College London — Identifier not found
    - University College London — https://ror.org/02jx3x895
- **Author:** Jacob Parker
  - **Author Identifier:** https://orcid.org/0000-0001-8732-8284
  - **Affiliations:**
    - Montana State University — https://ror.org/02w0trx84
- **Source:** Identity-aware union of the existing HSSI authors/affiliations (matched by ORCID, then name), the current repository `.zenodo.json`, and the latest Zenodo/DataCite version metadata. No seeded author or affiliation was removed. The current repository adds Jacob Parker. It also adds Bay Area Environmental Research Institute for Nabil Freij; that current affiliation is retained alongside the seeded SETI Institute affiliation. ROR identifiers for the two newly added organizations and the European Space Research and Technology Centre were resolved through the ROR API.
- **v0.9.0:** the release's Zenodo deposit (`10.5281/zenodo.24121214`, read 2026-11-11) lists the same eight creators with the same ORCIDs and the affiliations `.zenodo.json` gives, and `.zenodo.json` is the same at `1a1965066b192360bdc3681e128dec91d1a4ead0` and at the `v0.9.0` tag. The release's pull requests are by Nabil Freij, Will Barnes and Jacob Parker, all listed.
- **Stored on shared rows:** United States Naval Research Laboratory (on Will Barnes) and Mullard Space Science Laboratory, University College London (on David Stansby) are in no fiasco source; HSSI stores them on these authors' Person rows, which are shared with the authors' other entries. They are kept as stored (rule 17): an update cannot remove an affiliation from a Person row.

### 7. Software Name (MANDATORY)
- fiasco
- **Source:** Existing HSSI record, repository README, package metadata, Zenodo/DataCite, SoMEF, and PyHC registry.

### 8. Description (MANDATORY)
fiasco provides a Python interface to CHIANTI, an atomic database used primarily for astrophysical spectroscopy. It exposes high-level representations of ions, elements, levels, and transitions; parses and converts raw CHIANTI ASCII data into an HDF5 database; and computes common atomic-plasma quantities including level populations, ionization and recombination rates, contribution functions, emissivities, spectra, continuum emission, radiative losses, and equilibrium ionization. Its documented examples use those rates to calculate non-equilibrium ionization.

- **Source:** Evidence-backed expansion of the existing HSSI/Zenodo description using the current README, documentation, public API, examples, and tests. It retains the submitted description's core wording while adding the repository-documented calculations and data-conversion capabilities.
- **v0.9.0:** the release adds line ratios, access to CHIANTI's DEM models and line lists (Field 4), which this text does not name. The project's own descriptions (the README, `pyproject.toml` `description` and the documentation index, none changed by the release) name none of them either, so rule 3 does not fire and rule 6 keeps the description.

### 9. Concise Description (OPTIONAL)
fiasco provides a Python interface to the CHIANTI, an atomic database used primarily for astrophysical spectroscopy.

- **Source:** Existing HSSI record and current Zenodo metadata; retained verbatim to preserve submitted editorial wording. It is 116 characters.

### 10. Publication Date (RECOMMENDED)
- 2017-08-10
- **Source:** GitHub repository creation timestamp reported by the GitHub API and SoMEF (`2017-08-10T04:03:15Z`), corroborated by the first repository commits on 2017-08-09/10.
- **Note:** This replaces the seeded `2025-08-14`, which is the release date of the formerly recorded v0.6.1 rather than fiasco's initial publication date. The first tagged/PyPI stable release, v0.1.0, followed on 2023-01-04.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** Existing HSSI record and Zenodo/DataCite metadata.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.9.0
- **Version Date:** 2026-11-10
- **Version Description:**
  * Added line_ratio and example with EIS data
  * Add an interface to the CHIANTI DEM models
  * Speed up proton-electron ratio calculation and make it settable
  * Add `IonCollection.build_line_list`
- **Version PID:** https://doi.org/10.5281/zenodo.24121214

The description is exactly these four `* ` bullet lines, joined by single newlines.

*Why v0.9.0 is the current release (rule 3):* `v0.9.0` is a lightweight tag on commit `a3445e0b31aef865cb1b3f0008b21d5380abf121` (“Add `IonCollection.build_line_list` (#472)”), the head of the default branch `main` and of `origin/0.9`. Its GitHub release `v0.9.0` is published, marked Latest and not a pre-release, and PyPI's JSON API lists `fiasco-0.9.0-py3-none-any.whl` and `fiasco-0.9.0.tar.gz`, neither yanked, with `info.version` `0.9.0`. It opens the 0.9 series, which follows the 0.8 series in the project's release order. `git tag --sort=-creatordate` lists `v0.8.3` first only because a lightweight tag sorts by its commit's date, and the last backport on the `0.8` branch (2026-10-24T06:27Z) was committed hours after `a3445e0` (2026-10-23T22:57Z); v0.8.3 is a maintenance release of the series v0.9.0 succeeds (*Backport tags*). The version is dynamic (`setuptools_scm`), so the tag is what declares it. The number is written with a `v`, as the tag, the Zenodo and DataCite `version` and the stored v0.8.3 write it.

*Version date* 2026-11-10 is the release event's UTC calendar day (rule 7): the GitHub release was published 2026-11-10T22:55:49Z, and the Zenodo deposit for this version was created seven seconds later, its publication date and DataCite `Issued` both 2026-11-10. PyPI's files were uploaded 2026-11-11T02:52Z, after midnight UTC; the release day stands. The tagged commit is dated 2026-10-23, when the last change landed on `main`; that never overrides the release event (rule 8).

*Version description* (rules 13–15): the release name is the bare tag, so the text comes from the release body, a “What's Changed” list of four items. All four are kept verbatim, because each adds or changes something a user calls (read at `a3445e0`): PR #441 adds `fiasco.line_ratio` (`fiasco/fiasco.py:215`) with a Hinode/EIS density-diagnostic example; PR #457 adds `fiasco.get_dem_model` (`fiasco/fiasco.py:98`); PR #471 makes the proton-to-electron density ratio a `fiasco.Ion` argument (`fiasco/ions.py:73`) and speeds up `fiasco.proton_electron_ratio`; and PR #472 adds `IonCollection.build_line_list` (`fiasco/collections.py:220`). Each item's trailing “by @user in https://github.com/wtbarnes/fiasco/pull/N” credit and the body's “Full Changelog” compare link are dropped; nothing else is changed. The backticks around `IonCollection.build_line_list` are the body's own markdown, and `line_ratio` has none because the body writes it plain. The body does not list the three continuum fixes v0.9.0 also contains (PRs #477, #479 and #480, released first as v0.8.3's backports), and rule 15 adds nothing to it. `CHANGELOG.rst` is empty at the tag and `changelog/` holds only its README, so the release body is the only release text.

*Version PID* (rule 17): `10.5281/zenodo.24121214` is this release's GitHub-integration deposit. Its Zenodo `metadata.version` and DataCite `version` are `v0.9.0`, it carries `IsSupplementTo https://github.com/wtbarnes/fiasco/tree/v0.9.0` and `IsVersionOf 10.5281/zenodo.7504257`, and the concept's `HasVersion` list includes it. The DOI resolves. Its title is `fiasco`, which `.zenodo.json` sets, so it does not mirror the release name.

*Superseded values.* HSSI held `v0.8.3` (release date 2026-10-30, version PID `https://doi.org/10.5281/zenodo.23820293`, and as description that release's three items, “Fix limit on which levels are included in the FB calculation”, “Fix bug in allowing arrays of density into two-photon continuum calculation” and “Account for solid angle integral in free-free continuum)”, the last with the release body's own unmatched parenthesis) until the v0.9.0 release update; it was correct for its release, and nothing of it carries onto v0.9.0 (rule 10). HSSI held `v0.8.2` (release date 2026-07-28, version PID `https://doi.org/10.5281/zenodo.21716503`, and as description the three kept items of that release's notes) until the v0.8.3 release update. HSSI held `v0.8.1` (release date 2026-03-10, version PID `https://doi.org/10.5281/zenodo.18942693`) until the v0.8.2 release update; its stored description, “Adds the developer-maintained works-citing list, fixes an individual-level-label bug, and adds an option to disable the database-build progress bar.”, was a summary composed from that release's three items rather than the items themselves, which rule 15 does not allow. Before the 2026-07-26 extraction HSSI held the stale seeded `v0.6.1` (the view API renders it `fiasco - v0.6.1`; the prefix is a display transform).

*Release-history notes.*
- fiasco keeps a branch per release series (`origin/0.4` through `origin/0.9`); its GitHub releases v0.7.0 to v0.8.3 target `0.7` or `0.8`. The `0.8` branch leaves `main` at `2ec62afa154c2b8b92cdad415f0b12602b48d1b4`, so `v0.8.3` (`bf21eb232eb54bca368190753e0e68f1de451f39`) is not an ancestor of `v0.9.0`, and the release's “Full Changelog: v0.8.3...v0.9.0” range compares two branches. Of the 19 commits on `main` after the branch point, the eight with no `0.8` backport (PRs #441, #443, #446, #449, #457, #469, #471 and #472) are what v0.9.0 adds; the other eleven reached users first in 0.8.x releases as backports.
- `v0.9dev` (on `main`, 2026-02-11) is a development marker, not a release: no GitHub release carries it and PyPI has no upload of it. PyPI's development uploads, `0.4.dev0` and `0.8.dev0`, are pre-releases, which rule 3 never counts.
- The repository's generated `fiasco/CITATION.rst` still names v0.8.0 at the `v0.9.0` tag, and is therefore stale relative to GitHub, PyPI, DataCite and Zenodo.

### 13. Programming Language (RECOMMENDED)
- IDL
- Python 3.x
- **Source:** Identity-aware union retaining both existing HSSI values. Python 3.x is the package implementation and declared runtime language. IDL is materially represented by the maintained CHIANTI-IDL comparison suite and supporting procedures; GitHub/SoMEF language metadata also reports both.

### 14. Reference Publication (RECOMMENDED)
- Not found
- **Source:** The repository requests citation of the version-specific Zenodo software DOI and the CHIANTI database, but does not identify a publication whose subject is the fiasco software itself.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause
- **Source:** Existing HSSI record, repository `LICENSE.rst`, `.zenodo.json`, GitHub license API, and Zenodo/DataCite. The file contains all three BSD conditions.
- **Note:** SoMEF's code-parser also proposed BSD-2-Clause, but that conflicts with the actual license text, GitHub, Zenodo, and the existing HSSI value and was rejected.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- astronomy
- astrophysics
- atomic data
- atomic physics
- chianti
- chianti atomic database
- heliophysics
- plasma physics
- python
- science
- solar
- solar physics
- spectroscopy
- Emission spectroscopy
- extreme ultraviolet
- Ionization equilibrium
- Non-equilibrium ionization
- Radiative loss
- solar wind
- line list
- line ratio
- pyhc package
- **Spelling:** each value is written as its stored keyword row's name. A case variant binds the same row, so the earlier revision of this dossier that wrote `Astronomy` or `Extreme ultraviolet` named these same rows; a keyword is never re-sent to change only its case.
- **Source:** Identity-aware union retaining every existing HSSI keyword that passes the rubric and adding current package-metadata, documentation, public-API, and developer-curated usage concepts. The project declares `heliophysics`, `solar physics`, `astrophysics`, `plasma physics`, `science`, `atomic data` and `atomic physics` in `pyproject.toml` `keywords` (unchanged from the extraction's revision to `a3445e0b31aef865cb1b3f0008b21d5380abf121`), and the GitHub topics `astronomy`, `atomic-physics`, `chianti`, `chianti-atomic-database`, `python`, `solar`, `solar-physics` and `spectroscopy` (read 2026-10-29, and again on the live repository page on 2026-11-11: the same eight). fiasco's PyHC registry entry is unchanged (read 2026-11-11).
- **`line list`:** `IonCollection.build_line_list` (`fiasco/collections.py:220` at `a3445e0b31aef865cb1b3f0008b21d5380abf121`, released in v0.9.0) builds “a table of the emission lines of all ions in the collection”, the line list a spectroscopist searches for (rule 10). The value binds the existing lower-case `line list` row (rule 11). HSSI held it from the v0.8.2 release update, which minted that row, until the v0.8.3 release update removed it, with the user's confirmation of 2026-11-02, because the method was then on `main` only: a word-anchored, case-insensitive sweep of the `v0.8.3` tag (`bf21eb2…`, binary `.asdf` test data excluded) found no `line list`, `line_list` or `line-list`. That removal named a release shipping the method as the condition for re-adding it, and v0.9.0 ships it.
- **`line ratio`:** `fiasco.line_ratio` (`fiasco/fiasco.py:215` at `a3445e0…`, released in v0.9.0), a top-level public function, computes the “Theoretical line ratio for one or more bound-bound transitions as a function of temperature and density”; the documentation's Hinode/EIS example uses it as a density diagnostic, and `fiasco/tests/idl/test_idl_line_ratio.py` checks it against CHIANTI IDL. It is a quantity the software computes that a searcher types (rule 10). No live row names line ratios in any case, separator or plural variant (the vocabulary's only `ratio` matches are `calibration`, `AIA calibration` and `operations`, read 2026-11-11), so rule 12 mints `line ratio`, lower-case.
- **Weighed and not added, `differential emission measure`:** the live row exists, and v0.9.0's `fiasco.get_dem_model` returns CHIANTI's tabulated DEM models, which `build_line_list` takes as an input. fiasco derives no DEM from observations, so a searcher typing the term, usually looking for DEM inversion, would not find what they need here (rule 10); the access itself is carried by Field 4. Reconsider if fiasco gains a DEM calculation. `electron density` and `plasma diagnostics` were weighed for the same example and not added: the example derives its density map itself, by interpolating the observed ratio onto the curve `line_ratio` returns.
- **`pyhc package`:** fiasco is listed in the PyHC registry's `_data/projects.yml`, and rule 15 gives every PyHC package this keyword, written exactly so. HSSI held it before this dossier recorded it.
- **Removed, `ionosphere`, `thermosphere` and `mesosphere`:** HSSI held these until the v0.8.2 release update. They split the PyHC Science Area tag `ionosphere_thermosphere_mesosphere` and had no other source. Rule 3 keeps a registry domain tag only when the pinned code or the project's own description works in that domain, and rule 4 excludes an unsupported term: a word-anchored, case-insensitive sweep of the tree at `a3445e0…`, its binary `.asdf` test data included, finds no `ionospher*`, `thermospher*` or `mesospher*` (positive control `corona*`: five files outside the `.asdf` data), and no project description names these regions. Do not re-add them from the registry tag; Field 5's `Earth Atmosphere` left for the same reason.

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- **Source:** `fiasco.util.download_dbase` retrieves versioned CHIANTI database archives directly from `download.chiantidatabase.org`; users can also provide an existing local CHIANTI database tree.
- **Note:** the Hinode/EIS example released with v0.9.0 (`examples/user_guide/plot_jet_density_figure.py`) downloads two precomputed FITS files from the `sunpy/data` repository; a gallery script fetching its own example data is not a source fiasco's code reads (rules 2 and 5).

### 18. Input File Formats (RECOMMENDED)
- ascii
- HDF5
- **Source:** The public parser reads the raw CHIANTI ASCII database, and the public data layer reads the generated HDF5 database.
- **Weighed and not added, FITS:** the Hinode/EIS example released with v0.9.0 opens two precomputed FITS files with `astropy.io.fits`, but their intensities never reach fiasco: the example interpolates their observed ratio onto the curve `fiasco.line_ratio` computes from the HDF5 database. Rule 5 counts an example's format only when the example reads it as the software's input.

### 19. Output File Formats (RECOMMENDED)
- HDF5
- **Source:** `fiasco.util.build_hdf5_dbase` converts parsed CHIANTI data into a single HDF5 database.

### 20. Operating System (RECOMMENDED)
- Operating System Independent
- Linux
- Mac
- Windows
- **Source:** The package declares `Operating System :: OS Independent`; the current CI workflow explicitly tests Linux, macOS, and Windows.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent
- **Source:** fiasco is published as a `py3-none-any` wheel (v0.9.0's is `fiasco-0.9.0-py3-none-any.whl`, PyPI JSON API read 2026-11-11) and contains no architecture-specific implementation. Its compiled scientific dependencies remain responsible for their own platform support.

### 22. Related Phenomena (OPTIONAL)
- Coronal Heating
- Coronal Mass Ejections
- Solar Corona
- Solar Flares
- Solar Wind
- X-ray emission
- **Source:** Current CHIANTI/fiasco documentation covers solar-coronal abundances, ultraviolet/X-ray spectroscopy, emission spectra, and ionization calculations. The documented non-equilibrium-ionization example directly models a rapid coronal heating and cooling episode using fiasco rates, and the public API computes radiative losses used in coronal-heating modeling. The repository's developer-maintained works-citing list demonstrates fiasco use for coronal-mass-ejection charge-state modeling, solar-flare studies, and slow-solar-wind charge-state work (`docs/works_citing.bib:80`).
- **Note:** `Coronal Holes` was weighed during extraction and not selected because the repository does not establish it as a direct fiasco science target — but it was never actually available: it appeared only in a stale documentation list and has never been a row in the HSSI Phenomena vocabulary (noted 2026-08-24), so it must not be re-proposed as a value here regardless of evidence.

### 23. Development Status (RECOMMENDED)
- Active
- **Source:** Rule 6. fiasco has made stable releases since v0.1.0 (2023-01-04); its newest is v0.9.0, published 2026-11-10, and the last commit on the default branch `main` is `a3445e0b31aef865cb1b3f0008b21d5380abf121`, dated 2026-10-23T22:57:43Z, the commit v0.9.0 tags. The repository is not archived, the README carries no repostatus.org badge, and no project text declares another status (rules 1–4). The v0.8.3 and v0.8.2 release updates recorded the same status from those releases (2026-10-30 and 2026-07-28) and the same `main` head; the extraction recorded it from v0.8.1 (2026-03-10) and revision `1a1965066b192360bdc3681e128dec91d1a4ead0` (2026-07-23).

### 24. Documentation (RECOMMENDED)
- https://fiasco.readthedocs.io
- **Source:** Existing HSSI record, repository README and package metadata, SoMEF, and PyHC registry.

### 25. Funder (OPTIONAL)
- Not found
- **Source:** No funder is identified in the current repository, `.zenodo.json`, Zenodo/DataCite record, package metadata, or documentation. Author affiliations were not treated as funders.

### 26. Award Title (OPTIONAL)
- Not found
- **Source:** No award title or award number is identified in the current repository or Zenodo/DataCite metadata.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.3847/1538-4357/ae019d
- https://doi.org/10.3847/1538-4357/ae824d
- https://doi.org/10.1038/s41550-025-02747-9
- https://doi.org/10.3847/1538-4357/aceef8
- https://doi.org/10.3847/1538-4357/ada699
- https://doi.org/10.1007/s11207-025-02561-6
- https://doi.org/10.1051/0004-6361/202554166
- https://doi.org/10.1093/pasj/psag078
- https://doi.org/10.3847/1538-4357/ae99e7
- https://doi.org/10.48550/arXiv.2610.28961
**Evidence-only citation (intentionally not an HSSI Field 27 value):** Hart, S. T. (2024). Understanding the Origins and Acceleration Mechanisms of 3He-Rich Solar Energetic Particle Events [Doctoral dissertation, The University of Texas at San Antonio]. https://grad.space.swri.edu/please-join-us-in-congratulating-samuel-hart-our-newest-phd-as-he-successfully-defended-his-dissertation/
- **Source:** The values are papers that use fiasco. Eight are on the repository's developer-maintained `docs/works_citing.bib`: Benavitz et al. 2025 (ApJ), García et al. 2026 (ApJ), Kerr et al. 2026 (Nature Astronomy), Rivera et al. 2023 and 2025 (ApJ), Ryan et al. 2025 (Solar Physics), Varesano et al. 2026 (A&A) and McKevitt et al. 2026 (PASJ). Molnar et al. 2026 and Reep & To 2026 come from the literature search below. The seven values held before the v0.8.2 release update are kept as eligible publications that cite or use fiasco (rule 7), García et al. now as its version of record. McKevitt et al. and Molnar et al. are added because their own results were computed with fiasco and they say so: both in their methods, McKevitt et al. also in its Acknowledgments, and Molnar et al. in its “Software:” list, while fiasco's citing literature is still small enough that each use tells a searcher where and how the software is used (rule 5). Every value resolves; all are journal articles except the Reep & To preprint, so each is an eligible publication type. The Hart dissertation citation and its official SwRI/University of Texas at San Antonio institutional permalink are preserved above as evidence only.
- **Note:** For the Varesano et al. work, the repository's works-citing list gave the arXiv preprint DOI `10.48550/arXiv.2502.12045` at `1a1965066b192360bdc3681e128dec91d1a4ead0` and gives the journal DOI at `a3445e0b31aef865cb1b3f0008b21d5380abf121` (changed in commit `ae43445`); only the final journal DOI, `https://doi.org/10.1051/0004-6361/202554166`, is retained.
- **García et al. 2026, version of record:** `https://doi.org/10.3847/1538-4357/ae824d` (ApJ 1006, 209, issued 2026-07-28 per Crossref; the same work as arXiv:2512.09234) replaces the preprint DOI `https://doi.org/10.48550/arXiv.2512.09234`, which HSSI held until the v0.8.2 release update. The project's works-citing list now gives the journal DOI, and, by the user's decision of 2026-10-29, only the version of record is listed, as for Varesano et al.; do not re-add the preprint. The paper states that “All atomic properties are computed using atomic data from CHIANTI v11 (Del Zanna et al. 2021) as well as using version 0.2.3 of the fiasco open source software package” (quoted from arXiv:2512.09234; the journal version writes “open-source”), and its Acknowledgments credit fiasco v0.2.3.
- **McKevitt et al. 2026, PASJ 78, 1524:** “For our work here, we use CHIANTI version 10.0 (Del Zanna et al. 2021) through the fiasco Python interface (Barnes et al. 2025)” for the atomic data behind its synthetic SOLAR-C/EUVST short-wavelength-camera observations of a “three-dimensional MHD-simulated pre-flare active region” (its abstract's words), and its Acknowledgments state “This research used version 0.6.2 (Barnes et al. 2025) of the fiasco open source software package” (rule 5; quoted from arXiv:2607.11447). Crossref dates its journal version 2026-07-10, before this dossier's extraction, but the developers added it to `docs/works_citing.bib` only in commit `ae43445` (2026-09-24), after that extraction's source revision.
- **Molnar et al. 2026, ApJ 1009, 4:** computes the atomic quantities for its SPICE DEM and abundance analysis with CHIANTI v8.0.7, “where we have used the Python wrapper fiasco (W. Barnes et al. 2025) to perform these computations”, and lists fiasco in its Software statement (rule 5; quoted from arXiv:2608.12881). No fiasco author is among its authors.
- **Reep & To 2026, arXiv:2610.28961:** “We use the fiasco package (Barnes et al. 2026), v0.8.1, with CHIANTI version 11.0.2 (Dufresne et al. 2024), to calculate level populations and contribution functions necessary to estimate line intensities”, forward-modelling a flare's line emission. Its line-intensity results are computed with fiasco and its methods say so, so rule 5 includes it on the same test as anyone's paper; that Jeffrey Reep, its first author, is one of fiasco's authors plays no part. The user decided on 2026-10-29 to list it, before rule 5 stated that authorship plays no part; the rule now gives the same outcome.
- **Search, 2026-10-29:** ADS/SciX `full:"fiasco" full:"CHIANTI"` returns 11 records in all; those entered since the 2026-07-26 extraction are García et al. (journal version), McKevitt et al., Molnar et al., Reep & To, and a fiasco Zenodo version deposit. `ack:"fiasco"` returns 10 records: the six solar-physics papers already listed whose acknowledgement text, as ADS indexes it, names fiasco (Benavitz, García, McKevitt, Molnar, Ryan and Varesano et al.; for Molnar et al. that text is its “Software:” list), and four unrelated uses of the word. Controls: a nonsense token returns 0 and `full:"ChiantiPy"` returns hits. DataCite reports no citations of the concept DOI.
- **Search, 2026-11-02:** the same two ADS/SciX queries return the same 11 and 10 records; restricted to `entdate:[2026-10-29 TO *]`, `full:"fiasco" full:"CHIANTI"` returns 0 (control: `full:"ChiantiPy"` over `entdate:[2026-10-01 TO *]` returns 1; a nonsense token returns 0). DataCite still reports no citations of the concept DOI, and no commit since that search touches `docs/works_citing.bib`: `main`'s head is still `a3445e0…`, and v0.8.2→v0.8.3 leaves the file as it was. Nothing new qualifies. A later update searches from 2026-11-02.
- **Search, 2026-11-11:** DataCite reports no citations of the concept DOI or of the v0.9.0 deposit, and `docs/works_citing.bib` at the `v0.9.0` tag is the file read at `a3445e0…` above (the same commit). Nothing new qualifies from these routes. The same two ADS/SciX queries return the same 11 and 10 records, the newest entered 2026-10-22 (Reep & To, `2026arXiv261028961R`) and 2026-09-13 (Molnar et al.) respectively; restricted to `entdate:[2026-11-02 TO *]`, both return 0. Controls: a nonsense token returns 0; `full:"ChiantiPy"` returns 2 over `entdate:[2026-10-01 TO *]` and 0 over `entdate:[2026-11-02 TO *]`; over that same window `full:"solar"` returns 9193 and `full:"CHIANTI"` returns 2, neither of which names fiasco. Nothing new qualifies for this field or for Fields 14, 25 and 26. A later update searches from 2026-11-11.
- **Weighed and not added:** Mulay, Del Zanna & Mason (2017), “Temperature and Density Structure of a Recurring Active Region Jet” (A&A 598, A11, `10.1051/0004-6361/201628796`), entered `docs/references.bib` with PR #441 as the observation the v0.9.0 Hinode/EIS example reproduces; it neither presents, underlies nor uses fiasco (rules 3–5). “The SunPy Ecosystem” (AGU Fall Meeting 2018, `2018AGUFMIN11B0628R`) mentions fiasco but is a meeting abstract, which is never eligible (rule 1). The fiasco Zenodo version deposits that ADS indexes (`2025zndo..14757042B`, `2025zndo..17329038B`) are software releases (Field 12), not publications.
- **User decision:** The Hart dissertation URL is 133 characters and is intentionally excluded from the HSSI Field 27 values because the current HSSI backend stores a related publication URL in a 128-character `RelatedItem.name` field. Future agents must not re-add this URL to the emitted Field 27 values unless backend compatibility changes and the user explicitly revisits this decision.

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.3847/1538-4357/ad6765
- **Source:** fiasco is specifically an interface to and analysis layer for the CHIANTI atomic database. This DOI is the repository-cited paper describing CHIANTI Version 11, the newest database generation supported and tested by the current source.
- **Note:** the CHIANTI DEM models that v0.9.0's `fiasco.get_dem_model` returns are part of the same database. The precomputed Hinode/EIS products the v0.9.0 example reads have no identifier and are not read by fiasco (rules 2 and 8).

### 29. Related Software (OPTIONAL)
- https://www.chiantidatabase.org/chianti_download.html
- https://github.com/chianti-atomic/ChiantiPy
- https://github.com/PlasmaPy/PlasmaPy
- **Source:** CHIANTI IDL is the domain counterpart against which fiasco's calculations are explicitly compared and shares the same database; the official CHIANTI site identifies ChiantiPy as the alternative Python interface; PlasmaPy is a required domain-specific dependency used throughout fiasco's public ion/element abstractions.
- **Note:** Generic scientific-Python and tooling dependencies were excluded under the Field 29 relevance gate.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/astropy/astropy
- https://github.com/LM-SAL/aiapy
- https://www.chiantidatabase.org/chianti_download.html
- **Source:** Specific demonstrated exchanges, not dependency presence: fiasco's public API accepts and returns Astropy `Quantity` and `QTable` objects; the maintained AIA example combines a fiasco contribution function with an aiapy instrument-response object; and fiasco parses the same CHIANTI database used by the IDL package while its maintained comparison suite exchanges and validates corresponding IDL/Python calculation outputs.
- **Note:** NumPy, SciPy, Matplotlib, h5py, ASDF, hissw, and other generic/internal/test dependencies were considered but excluded. SunPy appears only through documentation cross-references or transitive/example context, with no direct demonstrated fiasco exchange.
- **Weighed and not added, EISPAC:** the Hinode/EIS example released with v0.9.0 names `eispac` as the fitting step behind its precomputed intensities and is written so as not to run it; neither the example nor fiasco calls EISPAC or reads an EISPAC-specific product, so no exchange is performed (rules 5 and 7).

### 31. Related Instruments (OPTIONAL)
- Not found
- **Source:** fiasco is instrument-agnostic atomic-data and modeling software.
- **Note:** The Atmospheric Imaging Assembly was considered because one documentation example combines fiasco with aiapy, but the example imports aiapy for all instrument-specific response behavior. Under the designed-to-support relevance gate, the instrument belongs to aiapy rather than fiasco, so no controlled-vocabulary instrument value is emitted.
- **Note, Hinode/EIS (v0.9.0):** the EUV Imaging Spectrometer appears in the documentation example `examples/user_guide/plot_jet_density_figure.py`, which applies the instrument-agnostic `fiasco.line_ratio` to precomputed EIS intensities, and in the name of the IDL comparison test `test_eis_fe_xiii_density_ratio_from_idl`, which checks that generic function on an Fe XIII line pair. fiasco has no EIS reader, response or EIS-specific branch; an example name-drop on an instrument-agnostic tool is not support (rules 2 and 3), so no value is emitted.

### 32. Related Observatories (OPTIONAL)
- Not found
- **Source:** fiasco is observatory- and mission-agnostic.
- **Note:** The Solar Dynamics Observatory was considered through the same AIA/aiapy example and excluded as example-only ecosystem context. Solar Orbiter and Parker Solar Probe mentions in works that cite fiasco demonstrate scientific use, not mission-specific data support, so no controlled-vocabulary observatory value is emitted.
- **Note, Hinode (v0.9.0):** excluded for the reason Field 31 gives for its EUV Imaging Spectrometer: a documentation example and a test name on instrument-agnostic code.

### 33. Logo (OPTIONAL)
- https://raw.githubusercontent.com/wtbarnes/fiasco/1a1965066b192360bdc3681e128dec91d1a4ead0/docs/_static/fiasco-logo.png
- **Source:** Repository `docs/_static/fiasco-logo.png`; the URL is pinned to the extracted full source revision and was verified to return HTTP 200 with `image/png`.
