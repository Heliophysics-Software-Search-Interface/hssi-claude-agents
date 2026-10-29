# HSSI Metadata Extraction Results

**HSSI Software ID:** 8e349bce-5860-4c0b-9ee9-ebb684574262
**Repository:** https://github.com/wtbarnes/fiasco
**Source Revision:** 1a1965066b192360bdc3681e128dec91d1a4ead0
**Extraction Date:** 2026-07-26
**Validation Date:** 2026-10-29
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
- **Note, line lists (read at `a3445e0b31aef865cb1b3f0008b21d5380abf121`):** `IonCollection.build_line_list` (`fiasco/collections.py:220`, PR #472, on `main` after v0.8.2) returns an Astropy `QTable` with one row per bound-bound transition of every ion in the collection, its contribution function and, given an emission-measure model, its line-of-sight intensity. It extends the stored `Analysis`, `Energy Spectra` and `Physics-Based` capabilities and earns no further row; it returns an in-memory table and writes no file, so Field 19 is unchanged too. The other changes up to that revision (free-bound, free-free and two-photon continuum fixes, a settable proton-to-electron density ratio) neither add nor remove a capability.

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
    - University College London — https://ror.org/02jx3x895
- **Author:** Jacob Parker
  - **Author Identifier:** https://orcid.org/0000-0001-8732-8284
  - **Affiliations:**
    - Montana State University — https://ror.org/02w0trx84
- **Source:** Identity-aware union of the existing HSSI authors/affiliations (matched by ORCID, then name), the current repository `.zenodo.json`, and the latest Zenodo/DataCite version metadata. No seeded author or affiliation was removed. The current repository adds Jacob Parker. It also adds Bay Area Environmental Research Institute for Nabil Freij; that current affiliation is retained alongside the seeded SETI Institute affiliation. ROR identifiers for the two newly added organizations and the European Space Research and Technology Centre were resolved through the ROR API.

### 7. Software Name (MANDATORY)
- fiasco
- **Source:** Existing HSSI record, repository README, package metadata, Zenodo/DataCite, SoMEF, and PyHC registry.

### 8. Description (MANDATORY)
fiasco provides a Python interface to CHIANTI, an atomic database used primarily for astrophysical spectroscopy. It exposes high-level representations of ions, elements, levels, and transitions; parses and converts raw CHIANTI ASCII data into an HDF5 database; and computes common atomic-plasma quantities including level populations, ionization and recombination rates, contribution functions, emissivities, spectra, continuum emission, radiative losses, and equilibrium ionization. Its documented examples use those rates to calculate non-equilibrium ionization.

- **Source:** Evidence-backed expansion of the existing HSSI/Zenodo description using the current README, documentation, public API, examples, and tests. It retains the submitted description's core wording while adding the repository-documented calculations and data-conversion capabilities.

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
- **Version Number:** v0.8.2
- **Version Date:** 2026-07-28
- **Version Description:**
  * Misc bugfixes
  * Fix level_populations matrix solve shapes for numpy<2 compatibility
  * Use elvlc data to compute energy spacing in upsilon calculation rather than scups data
- **Version PID:** https://doi.org/10.5281/zenodo.21716503

The description is exactly these three `* ` bullet lines, joined by single newlines.

*Why v0.8.2 is the current release (rule 3):* fiasco keeps a branch per release series (`origin/0.4` through `origin/0.8`), and its GitHub releases v0.7.0 to v0.8.2 target `0.7` or `0.8`. `v0.8.2` is a lightweight tag on commit `5ac62d4d8b89aa5eec912f06582b4e1d5022c3ab` (“Backport PR #462: Fix tests for v8 and v9 (#463)”) on `origin/0.8`, which branches from `main` at `2ec62afa154c2b8b92cdad415f0b12602b48d1b4`; `v0.8.1` (`1cdbae5`) is its ancestor. Its GitHub release `v0.8.2` is neither a draft nor a pre-release, and PyPI's JSON API lists `fiasco-0.8.2-py3-none-any.whl` and `fiasco-0.8.2.tar.gz` with `info.version` `0.8.2`. The version is dynamic (`setuptools_scm`), so the tag is what declares it. The number is written with a `v`, as the tag and release name write it and as v0.8.1 was stored.

*Version date* 2026-07-28 is the release event's UTC calendar day (rule 7): the GitHub release was published 2026-07-28T20:11:28Z, the tagged commit is dated 2026-07-28T13:50:38−04:00 (17:50:38Z), and PyPI's wheel was uploaded 2026-07-28T22:26:46Z. Zenodo's deposit for this version records 2026-07-31 as its publication date and DataCite as `Issued`, the day the deposit was made; that never overrides the release event (rule 8).

*Version description* (rules 13–15): the release name is the bare tag, so the text comes from the release body, a “What's Changed” list of four items. Three are kept verbatim, because each changes what a user gets from a calculation: “Misc bugfixes” (PR #454, backported as `c79bbfc`: `formation_temperature` now takes `np.nanargmax` of the ionization fraction, and the level-resolved radiative-recombination rate interpolation is given `bounds_error: False`), the `level_populations` fix for NumPy < 2 (PR #450, `270ae17`), and the switch of the upsilon calculation's energy spacing from `scups` to `elvlc` data (PR #459, `44007e3`). The fourth, “Fix tests for v8 and v9)”, repairs the test suite and is dropped whole (rule 14). Each item's trailing “by @user in https://github.com/wtbarnes/fiasco/pull/N” credit and the body's “Full Changelog” compare link are dropped; nothing else in the kept items is changed, including “numpy<2”. `CHANGELOG.rst` is empty and `changelog/` holds only its README, so the release body is the only release text.

*Version PID* (rule 17): `10.5281/zenodo.21716503` is this release's GitHub-integration deposit. Its Zenodo `metadata.version` and DataCite `version` are `v0.8.2`, it carries `IsSupplementTo https://github.com/wtbarnes/fiasco/tree/v0.8.2` and `IsVersionOf 10.5281/zenodo.7504257`, and the concept's `HasVersion` list includes it. The DOI resolves.

*Superseded values.* HSSI held `v0.8.1` (release date 2026-03-10, version PID `https://doi.org/10.5281/zenodo.18942693`) until the v0.8.2 release update. v0.8.1 was correctly dated and its PID was its own deposit, but its stored description, “Adds the developer-maintained works-citing list, fixes an individual-level-label bug, and adds an option to disable the database-build progress bar.”, was a summary composed from that release's three items rather than the items themselves, which rule 15 does not allow; nothing of it carries onto v0.8.2 (rule 10). Before the 2026-07-26 extraction HSSI held the stale seeded `v0.6.1` (the view API renders it `fiasco - v0.6.1`; the prefix is a display transform).

*Release-history notes.*
- `v0.9dev` (on `main`, 2026-02-11) is a development marker, not a release: no GitHub release carries it and PyPI has no 0.9 upload. PyPI's development uploads, `0.4.dev0` and `0.8.dev0`, are pre-releases, which rule 3 never counts.
- The `0.8` branch carries three backports after `v0.8.2` — PRs #477, #479 and #480 (the free-bound level limit, the free-free solid-angle factor, density arrays in the two-photon continuum) — that no tag, release or PyPI upload had shipped by 2026-10-29, the branch head then being `bf21eb2` (2026-10-24). They are unreleased (rule 2); a later release update should look for a v0.8.3.
- The repository's generated `fiasco/CITATION.rst` still names v0.8.0, both at `a3445e0…` and at the `v0.8.2` tag, and is therefore stale relative to GitHub, PyPI, DataCite and Zenodo.

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
- pyhc package
- **Spelling:** each value is written as its stored keyword row's name. A case variant binds the same row, so the earlier revision of this dossier that wrote `Astronomy` or `Extreme ultraviolet` named these same rows; a keyword is never re-sent to change only its case.
- **Source:** Identity-aware union retaining every existing HSSI keyword that passes the rubric and adding current package-metadata, documentation, public-API, and developer-curated usage concepts. The project declares `heliophysics`, `solar physics`, `astrophysics`, `plasma physics`, `science`, `atomic data` and `atomic physics` in `pyproject.toml` `keywords` (unchanged from the extraction's revision to `a3445e0b31aef865cb1b3f0008b21d5380abf121`), and the GitHub topics `astronomy`, `atomic-physics`, `chianti`, `chianti-atomic-database`, `python`, `solar`, `solar-physics` and `spectroscopy` (read 2026-10-29).
- **`line list`** (minted lower-case): `IonCollection.build_line_list` (`fiasco/collections.py:220` at `a3445e0…`, PR #472) builds “a table of the emission lines of all ions in the collection”, one row per bound-bound transition with its contribution function and, given an emission-measure model, its intensity. Someone looking for software that produces a CHIANTI line list would search for this term (rule 10), and no keyword row named it in any case, separator or plural form (rule 12). The method is on `main` after v0.8.2 and is not part of that release; a later release update should confirm that it shipped.
- **`pyhc package`:** fiasco is listed in the PyHC registry's `_data/projects.yml`, and rule 15 gives every PyHC package this keyword, written exactly so. HSSI held it before this dossier recorded it.
- **Removed, `ionosphere`, `thermosphere` and `mesosphere`:** HSSI held these until the v0.8.2 release update. They split the PyHC Science Area tag `ionosphere_thermosphere_mesosphere` and had no other source. Rule 3 keeps a registry domain tag only when the pinned code or the project's own description works in that domain, and rule 4 excludes an unsupported term: a word-anchored, case-insensitive sweep of the tree at `a3445e0…`, its binary `.asdf` test data included, finds no `ionospher*`, `thermospher*` or `mesospher*` (positive control `corona*`: five files outside the `.asdf` data), and no project description names these regions. Do not re-add them from the registry tag; Field 5's `Earth Atmosphere` left for the same reason.

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- **Source:** `fiasco.util.download_dbase` retrieves versioned CHIANTI database archives directly from `download.chiantidatabase.org`; users can also provide an existing local CHIANTI database tree.

### 18. Input File Formats (RECOMMENDED)
- ascii
- HDF5
- **Source:** The public parser reads the raw CHIANTI ASCII database, and the public data layer reads the generated HDF5 database.

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
- **Source:** fiasco is published as a `py3-none-any` wheel and contains no architecture-specific implementation. Its compiled scientific dependencies remain responsible for their own platform support.

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
- **Source:** Rule 6. fiasco has made stable releases since v0.1.0 (2023-01-04); its newest is v0.8.2, published 2026-07-28, and the last commit on the default branch `main` is `a3445e0b31aef865cb1b3f0008b21d5380abf121`, dated 2026-10-23T22:57:43Z. The repository is not archived, the README carries no repostatus.org badge, and no project text declares another status (rules 1–4). The extraction recorded the same status from v0.8.1 (2026-03-10) and revision `1a1965066b192360bdc3681e128dec91d1a4ead0` (2026-07-23).

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
- **Reep & To 2026, arXiv:2610.28961:** “We use the fiasco package (Barnes et al. 2026), v0.8.1, with CHIANTI version 11.0.2 (Dufresne et al. 2024), to calculate level populations and contribution functions necessary to estimate line intensities”, forward-modelling a flare's line emission. Jeffrey Reep is one of fiasco's authors, so the paper is neither a developers' publication about fiasco (rule 3) nor a third-party use (rule 5). It is included by the user's decision of 2026-10-29: like a third-party use, it shows a searcher where fiasco is used, and the list already holds three developer-coauthored uses from the project's own works-citing list (Benavitz et al., with Jeffrey Reep; Kerr et al. and Ryan et al., each with Laura Hayes).
- **Search, 2026-10-29:** ADS/SciX `full:"fiasco" full:"CHIANTI"` returns 11 records in all; those entered since the 2026-07-26 extraction are García et al. (journal version), McKevitt et al., Molnar et al., Reep & To, and a fiasco Zenodo version deposit. `ack:"fiasco"` returns 10 records: the six solar-physics papers already listed whose acknowledgement text, as ADS indexes it, names fiasco (Benavitz, García, McKevitt, Molnar, Ryan and Varesano et al.; for Molnar et al. that text is its “Software:” list), and four unrelated uses of the word. Controls: a nonsense token returns 0 and `full:"ChiantiPy"` returns hits. DataCite reports no citations of the concept DOI. A later update searches from 2026-10-29.
- **Weighed and not added:** “The SunPy Ecosystem” (AGU Fall Meeting 2018, `2018AGUFMIN11B0628R`) mentions fiasco but is a meeting abstract, which is never eligible (rule 1). The fiasco Zenodo version deposits that ADS indexes (`2025zndo..14757042B`, `2025zndo..17329038B`) are software releases (Field 12), not publications.
- **User decision:** The Hart dissertation URL is 133 characters and is intentionally excluded from the HSSI Field 27 values because the current HSSI backend stores a related publication URL in a 128-character `RelatedItem.name` field. Future agents must not re-add this URL to the emitted Field 27 values unless backend compatibility changes and the user explicitly revisits this decision.

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.3847/1538-4357/ad6765
- **Source:** fiasco is specifically an interface to and analysis layer for the CHIANTI atomic database. This DOI is the repository-cited paper describing CHIANTI Version 11, the newest database generation supported and tested by the current source.

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

### 31. Related Instruments (OPTIONAL)
- Not found
- **Source:** fiasco is instrument-agnostic atomic-data and modeling software.
- **Note:** The Atmospheric Imaging Assembly was considered because one documentation example combines fiasco with aiapy, but the example imports aiapy for all instrument-specific response behavior. Under the designed-to-support relevance gate, the instrument belongs to aiapy rather than fiasco, so no controlled-vocabulary instrument value is emitted.

### 32. Related Observatories (OPTIONAL)
- Not found
- **Source:** fiasco is observatory- and mission-agnostic.
- **Note:** The Solar Dynamics Observatory was considered through the same AIA/aiapy example and excluded as example-only ecosystem context. Solar Orbiter and Parker Solar Probe mentions in works that cite fiasco demonstrate scientific use, not mission-specific data support, so no controlled-vocabulary observatory value is emitted.

### 33. Logo (OPTIONAL)
- https://raw.githubusercontent.com/wtbarnes/fiasco/1a1965066b192360bdc3681e128dec91d1a4ead0/docs/_static/fiasco-logo.png
- **Source:** Repository `docs/_static/fiasco-logo.png`; the URL is pinned to the extracted full source revision and was verified to return HTTP 200 with `image/png`.
