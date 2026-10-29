# HSSI Metadata Extraction Results

**HSSI Software ID:** da5cb52c-1e0a-4c22-ab96-e05c210c0e60
**Repository:** https://github.com/punch-mission/solpolpy
**Source Revision:** a60095811fb6d4f4263d58e78dab3285a26bcf04
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-10-29
**Validation Status:** PASS

*Unqualified citations are at the header's Source Revision `a600958` (the 0.7.0 tag); passages that name `a118e6f` cite that revision (the 0.8.0 tag).*

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Source note: Not exposed by the HSSI view/data API; this entry was not submitted by us. Placeholder retained.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.10076326

*Source note: Confirmed as the Zenodo **concept** DOI by `CITATION.cff` (`doi: 10.5281/zenodo.10076326`), the README DOI badge (`https://zenodo.org/doi/10.5281/zenodo.10076326`), and the Zenodo API (all 20 version records, 0.0.1 through 0.8.0, report `conceptdoi: 10.5281/zenodo.10076326`). When 0.8.0 was recorded, DataCite's concept record presented version 0.8.0, matching the newest tag.*

### 3. Code Repository (MANDATORY)
https://github.com/punch-mission/solpolpy

*Source note: Confirmed by `CITATION.cff` `url:` and the git remote; the URL is live and not redirected.*

### 4. Software Functionality (RECOMMENDED)
- Coordinate Transforms
- Coordinate Transforms: Mission-Specific
- Coordinate Transforms: Solar
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Wave Polarization Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Mission-Specific
- Mission-related
- Mission-related: Calibration
- Mission-related: Science Data Processing

*Source note (per-value evidence, from the source tree at `a600958`; names that changed in 0.8.0 are given as they are at `a118e6f`):*

| Value | Evidence |
|---|---|
| Coordinate Transforms | Parent of the two child values below (required parent). |
| Coordinate Transforms: Solar | `solpolpy/util.py::solnorth_from_wcs` (a **public** export in `__init__.py`'s `__all__`) computes the per-pixel solar-north direction from a helioprojective WCS (since 0.8.0 from the local Jacobian of the WCS, which stays accurate at wide angles; `a118e6f`); `solpolpy/util.py::compute_lats` uses `astropy.wcs.utils.pixel_to_skycoord` to get solar `Tx`/`Ty` per pixel; `solpolpy/alpha.py::radial_from_wcs` builds the per-pixel `alpha` angle field referenced to solar north from helioprojective coordinates; `transforms.py::mzpsolar_to_mzpinstru` / `mzpinstru_to_mzpsolar` rotate polarization between the solar and instrument reference frames using those solar-north angles. |
| Coordinate Transforms: Mission-Specific | Instrument/spacecraft-frame conversion driven by per-instrument polarizer offsets (`POLAROFF`) and mission-specific reference angles: `solpolpy/constants.py` `STEREOA_REFERENCE_ANGLE = 45.8 deg`, `STEREOB_REFERENCE_ANGLE = -18 deg`, applied via `core.py::determine_reference_angle` keyed on the `OBSRVTRY` header. |
| Data Processing and Analysis | Required parent for the selected processing and analysis subcategories; independently supported by the package's polarization-processing entry points. |
| Data Processing and Analysis: Analysis | Derives physical quantities from observations: total brightness `tB`, excess polarized brightness `pB`/`pB'`, Stokes `I`/`Q`/`U`, polarization angle `theta`, degree of polarization `p` (`transforms.py::mzpsolar_to_tbpb`, `mzpsolar_to_stokes`, `mzpsolar_to_bp3`, `bp3_to_bthp`; 0.8.0 renamed `B` to `tB` and `mzpsolar_to_bpb` to `mzpsolar_to_tbpb`, `a118e6f`). |
| Data Processing and Analysis: Calibration | Instrument-geometry corrections applied to instrument data before/while resolving: polarizer-angle foreshortening ("IMAX effect") folded into the MZPinstru<->MZPsolar conversion (`CHANGELOG.rst` 0.6.0), per-polarizer `POLAROFF` offsets (`transforms.py::mzpsolar_to_npol`, `mzpinstru_to_mzpsolar`), and per-observatory reference angles (`constants.py`). |
| Data Processing and Analysis: Image Processing | Operates on 2D FITS image arrays: coronagraph occulter mask construction and propagation (`instruments.py::construct_mask`, `get_instrument_mask`, `util.py::combine_all_collection_masks`), optical-distortion pixel resampling (`util.py::compute_distortion_shift`, `apply_distortion_shift`), and radial gradient image enhancement via `sunkit_image.radial` (`nrgf`, `fnrgf`, `rhef`, `intensity_enhance`) in `plotting.py::generate_rgb_image`. |
| Data Processing and Analysis: Processing | `core.py` composes transformation chains: `get_transform_path` runs `networkx.shortest_path` over `transforms.py::transform_graph`, then `get_transform_equation`/`_compose2` builds the composed pipeline function actually executed by `resolve`. |
| Data Processing and Analysis: Wave Polarization Analysis | The taxonomy's own indicator list for this value names **Stokes parameters** and polarization-ellipse quantities. `transforms.py::mzpsolar_to_stokes` and `fourpol_to_stokes` compute Stokes I/Q/U via a Mueller matrix; `bp3_to_bthp` computes the polarization angle `theta` and degree of polarization `p`. The durable decision note below records why this category is retained even though it is more often applied to plasma-wave polarimetry than to Thomson-scattering imaging polarimetry. |
| Data Visualization | **Required parent of `Data Visualization: Mission-Specific`.** The earlier record lacked this required parent; `plotting.py::plot_collection` also supports it independently. |
| Data Visualization: 2D Graphics | `plotting.py::plot_collection` renders each collection member as a WCS-projected 2D image (`NDCube.plot` / `imshow`) with helioprojective longitude/latitude ticks, formatters, grid and optional colorbar; exercised by `tests/test_plotting.py`. |
| Data Visualization: Mission-Specific | `plotting.py::get_colormap_str` selects instrument-specific SunPy colormaps by `INSTRUME`/`DETECTOR` (`soholasco2`, `soholasco3`, `kcor`, `stereocor1`, `stereocor2`), and `plotting.py::generate_rgb_image` produces the mission-style MZP-triplet chromatic polarization composite of Patel et al. 2023. |
| Mission-related | **Required parent of `Mission-related: Calibration`.** The earlier record lacked this required parent. Independent support: `docs/source/index.rst` states solpolpy "has been developed as part of the PUNCH mission"; `docs/source/conf.py` copyright is "PUNCH Science Operations Center"; `instruments.py::load_data` carries a PUNCH-specific `hdu_index` instruction. |
| Mission-related: Calibration | punchbowl ("PUNCH science calibration code", https://github.com/punch-mission/punchbowl) declares `solpolpy` as a required dependency and performs its polarization transformation / "Corrections for polarized data production" (punchbowl `CHANGELOG.rst` line 130 at `d2d44328`) through it. |
| Mission-related: Science Data Processing | solpolpy performs the polarization-resolution step of PUNCH science data production, invoked from the punchbowl pipeline (see above); `resolve` is the pipeline-facing entry point. |

*Considered and deliberately excluded (audit trail): `Data Processing and Analysis: Data Access and Retrieval` — no remote fetch, API client or archive query anywhere; inputs are local file paths. `Data Processing and Analysis: File Format Conversion` — `resolve` converts polarization **systems**, not file formats, and no writer exists. `Data Processing and Analysis: Data Reduction` — no binning, averaging or downsampling. `Data Processing and Analysis: 2D Slices` / `Data Visualization: 2D Slices` — no 3D volumes. `Data Visualization: Movies` — no animation code. `Data Visualization: Line Plots` / `3D Graphics` — no 1D or 3D plotting. `Mission-related: Processing` — redundant with `Science Data Processing`. `Mission-related: Instrument Response` and `Models and Simulations: Instrument Response` — the polarizer conversion matrix is an analytic inversion of measurements, not an instrument-response model. All of `Models and Simulations` — the transforms are closed-form algebra from DeForest et al. 2022, not physical models or simulations; `util.py::make_empty_distortion_model` only allocates an empty `DistortionLookupTable`. All of `Servers and Environments` — no server, container, HPC or IaC code.*

*0.8.0 release check (`a118e6f`): the release renamed the total-brightness system and output key (`bpb` to `tbpb`, `B` to `tB`), recomputed solar north from the WCS Jacobian, fixed a cosine/sine error in `bp3_to_mzpsolar`, and made the empty distortion model zero-offset in both axes. It added no capability and removed none, so every value above stands and no further value applies.*

### 5. Related Region (RECOMMENDED)
- Solar Environment
- Corona
- Interplanetary Space

*Source note: `Solar Environment` is retained. `Corona` is supported by the package's implementation of the method in "Three-polarizer Treatment of Linear Polarization in Coronagraphs and Heliospheric Imagers" (`solpolpy/transforms.py:3-5`) and its hard-coded coronagraph masks for LASCO, COSMO K-Coronagraph, and SECCHI (`solpolpy/instruments.py:121-166`); Field 22 independently records `Solar Corona`. `Interplanetary Space` is supported by the same reference paper's explicit heliospheric-imager scope, `docs/source/index.rst` describes the software as serving "solar physics and heliophysics", and the package is built for PUNCH, whose Wide Field Imagers image the inner heliosphere well beyond the corona.*

### 6. Authors (MANDATORY)
The nine-author list is supported by the established HSSI identities, `CITATION.cff`, and `pyproject.toml`.

1. **J. Marcus Hughes**
   - Author Identifier: https://orcid.org/0000-0003-3410-7650
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
2. **Ritesh Patel**
   - Author Identifier: https://orcid.org/0000-0001-8504-2725
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
3. **Matthew West**
   - Author Identifier: https://orcid.org/0000-0002-0631-2393
   - Affiliation: European Space Research and Technology Centre — https://ror.org/03h3jqn23
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
4. **Craig DeForest**
   - Author Identifier: https://orcid.org/0000-0002-7164-2786
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
5. **Sarah Kovac**
   - Author Identifier: https://orcid.org/0000-0003-1714-5970
   - Affiliation: NSF NCAR High Altitude Observatory — https://ror.org/03773p874
6. **Derek Lamb**
   - Author Identifier: https://orcid.org/0000-0002-6061-6443
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
7. **Chris Lowder**
   - Author Identifier: https://orcid.org/0000-0001-8318-8229
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
8. **Daniel Seaton**
   - Author Identifier: https://orcid.org/0000-0002-0494-2025
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
9. **Bryce Walbridge**
   - Author Identifier: Not found
   - Affiliation: Not found

*Source note: `CITATION.cff` lists the same nine people with the same eight ORCIDs and likewise gives Walbridge no ORCID. DataCite (concept DOI 10.5281/zenodo.10076326) lists the same nine creators with the same ORCIDs, and also carries no identifier for Walbridge. Affiliation organization names and RORs resolve to Southwest Research Institute (`https://ror.org/03tghng59`), European Space Research and Technology Centre (`https://ror.org/03h3jqn23`) and NSF NCAR High Altitude Observatory (`https://ror.org/03773p874`). ROR `03773p874` registers `NSF NCAR High Altitude Observatory` as its `ror_display` label, with `HAO` as its acronym and `High Altitude Observatory` as an alias — the shorter `NCAR High Altitude Observatory` form appears in none of the ROR record's name variants, so it should not be restored. A public ORCID registry search for `family-name:Walbridge AND given-names:Bryce` returned 0 results, so his identifier stays empty — nothing invented. `pyproject.toml` contributes five author entries with emails (`J. Marcus Hughes`, `Matthew J. West`, `Ritesh Patel`, `Bryce M. Walbridge`, `Chris Lowder`) — all five are already in the list; the `CITATION.cff` name forms are retained rather than adopting the `pyproject.toml` middle-initial variants (see the settled name-variant rationale below). Sam Van Kooten was weighed as a candidate author and deliberately not listed: `CITATION.cff` curates authorship by intellectual contribution rather than commit history — four of the nine listed authors have zero commits — so his absence from the author list is a project choice, not a metadata gap.*

*Author 5 spelling — `Sarah Kovac` (see the durable decision evidence in A6 below). `CITATION.cff` (line 16, `family-names: "Kovak"`) and DataCite both spell it **Kovak**, but those are not independent: Zenodo/DataCite populate creators from the repository's `CITATION.cff`, so DataCite inherits the same typo. The authoritative record for that identifier is the person's own ORCID entry, which gives `given-names: Sarah`, `family-name: **Kovac**` with no credit-name and no other-names. Crossref's author list for the Patel et al. 2023 paper (`Patel, Seaton, Caspi, Kovac, …`) and punchbowl's `pyproject.toml` (`{ name = "Sarah Kovac" }`) independently agree. This is also consistent with Field 27's source note, which cites her as "Kovac, S."*

### 7. Software Name (MANDATORY)
solpolpy

*Source note: Matches `pyproject.toml` `name`, `CITATION.cff` `title`, the README heading and the PyPI project name.*

### 8. Description (MANDATORY)
solpolpy is a solar polarization resolver based on Deforest et al. 2022. It converts between various polarization formats, e.g. from the native three triple version from observations (also known as the MZP convention) to polarization brightness (pB) and total brightness (tB), Stokes I, Q and U, etc.

*Source note: The stored text is the curator's light rendering of the README's opening paragraph (README lines 7-9 at `a118e6f`), with the markdown link and code formatting removed; that cleanup is editorial intent and is kept (rule 6). The 0.8.0 release renamed total brightness from `B` to `tB` throughout the API (`System.bpb` became `System.tbpb`, and the output key `"B"` became `"tB"`), the docs and the README, whose sentence now reads "…to polarization brightness (pB) and total brightness (tB), Stokes I, Q and U, etc." The stored "(B)" had thereby become an earlier revision of the project's own sentence (rule 3), so only that token was changed and every other word kept. HSSI held "total brightness (B)" until the 0.8.0 release update. `docs/source/example.ipynb` cell 0 carries the same sentence with "total polarization (tB)" at `a118e6f`; the README's "total brightness" is the form kept.*

### 9. Concise Description (OPTIONAL)
solpolpy is a solar polarization resolver.

*Source note: Preserved verbatim (43 characters, within the 200-character limit). Closely matches the GitHub repository description "A solar polarization resolver."*

### 10. Publication Date (RECOMMENDED)
2023-11-06

*Source note: Confirmed as the date of first publication — Zenodo record 10076327 (version 0.0.1) has `publication_date: 2023-11-06`, and `CHANGELOG.rst` records "Version 0.0.1: Nov 6, 2023".*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Source note: DataCite identifies `publisher: "Zenodo"` for the concept DOI, consistent with the GitHub-Zenodo release workflow.*

### 12. Version (RECOMMENDED)
- **Version Number:** 0.8.0
- **Version Date:** 2026-10-16
- **Version Description:** exactly the text in the block below: three lines, each beginning `- `, joined by single newlines.

```text
- Improved solar north angle determination at wide angles using the Jacobian. The previous gradient-based method works well close to the Sun but produces large errors at large angles.
- Update B -> tB and BpB -> tBpB to match updates to PUNCH FITS metadata.
- Fixed a cosine/sine typo in ``solpolpy.transforms.bp3_to_mzpsolar``.
```

- **Version PID:** https://doi.org/10.5281/zenodo.23421406

***The Version Number is `0.8.0` — never `solpolpy - 0.8.0`.*** *HSSI's user view adds the software-name prefix when rendering a bare stored version number. Including that prefix in the value would render it twice, so future refreshes must preserve the bare form.*

*Why 0.8.0 is the current release (rule 3): `0.8.0` is a lightweight tag on commit `a118e6f72d2605291827abc485d5bbe5f9fad96c` ("update version", 2026-10-16T15:20:38Z), the head of `main` when the release was recorded; `0.7.0` (`a600958`) is an ancestor of it, and all 20 tags lie on `main`'s lineage. GitHub release `0.8.0` is neither a draft nor a pre-release, and PyPI's JSON API lists `solpolpy-0.8.0.tar.gz`, not yanked, with `info.version` `0.8.0`. The version is dynamic (`pyproject.toml` `dynamic = ["version"]`, built with setuptools-scm), so the tag is what declares it. The number is written without a `v`, as the tag, the release name, PyPI and the stored 0.7.0 wrote it.*

*Version date (rule 7): the GitHub release was published 2026-10-16T15:21:06Z; the tagged commit is dated 2026-10-16T15:20:38Z; PyPI's sdist was uploaded 2026-10-16T15:21:52Z; the Zenodo deposit's `publication_date` and DataCite `Issued` are 2026-10-16; and `CHANGELOG.rst` heads the section "Version 0.8.0: October 16, 2026". All agree.*

*Version description (rules 10, 13–16): the release name is the bare tag, and the release body is GitHub's auto-generated "What's Changed" list of five pull-request titles with contributor credits, a "New Contributors" line and a "Full Changelog" link, which rule 16 does not record. The text therefore comes from the project's `CHANGELOG.rst` section "Version 0.8.0: October 16, 2026" at `a118e6f`. Its two New Features items and its one Bug Fixes item are kept verbatim, each without its trailing pull-request link; the project's reStructuredText double backticks around `solpolpy.transforms.bp3_to_mzpsolar` render as inline code under "Release Notes" and are kept. Dropped whole: the two Internal Changes items, "Minor style fixes to make newer Ruff versions happy." and "Updated pre-commit" (rule 14). The section headings are not carried, because their reStructuredText underlines would render as markdown headings; each kept item reads on its own. The second item's changelog link names `#1214`, the number in its branch name (`1214-update-public-punch-pages-based-on-feedback`); the change merged as solpolpy pull request #225. Both #224 and #225 merged after the `0.7.0` tag.*

*Forms not used, so a later refresh does not re-propose them: the GitHub release body in any form — raw markdown, or with its markers stripped as the 0.7.0 entry held it — because it is an auto-generated pull-request list (rule 16); and a summary composed from the changelog, because rule 15 records only the project's own items.*

*Version PID (rule 17): `10.5281/zenodo.23421406` is this release's GitHub-integration deposit. DataCite gives it `version` `0.8.0`, `IsSupplementTo https://github.com/punch-mission/solpolpy/tree/0.8.0` and `IsVersionOf 10.5281/zenodo.10076326`, and the concept's `HasVersion` list includes it. The DOI resolves.*

*Superseded values. HSSI held 0.7.0 (release date 2026-07-28, version PID https://doi.org/10.5281/zenodo.21640376) until the 0.8.0 release update. That release's date and PID were its own, but its description was the GitHub release body with the markdown markers stripped, an auto-generated pull-request list that rule 16 does not record; nothing of it carries onto 0.8.0 (rule 10). Before the 2026-07-28 extraction HSSI held 0.5.1 (see A2).*

*Release-history notes: `CITATION.cff` still declares `version: 0.7.0` and `date-released: 2026-07-28` at the `0.8.0` tag; the file was not updated for the release, so it is stale rather than evidence against 0.8.0 (rule 8). No commits followed the tag on `main` when 0.8.0 was recorded; a later release update should look for the next release after 0.8.0.*

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source note: confirmed by `pyproject.toml` `requires-python = ">=3.11"`, the CI matrix (3.11, 3.12, 3.13, 3.14) in `.github/workflows/CI.yml`, and GitHub's language statistics, which list Python alone (re-read at `a118e6f`).*

### 14. Reference Publication (OPTIONAL)
https://doi.org/10.1109/SSIAI59505.2024.10508701

*Source note: Patel, R., Hughes, J. M., West, M. J., Lowder, C., Seaton, D. B., Redfern, J., DeForest, C., & Killough, R. (2024), "3D Imaging With The Polarimeter to Unify The Corona and Heliosphere", 2024 IEEE Southwest Symposium on Image Analysis and Interpretation (SSIAI), pp. 57–60. Recorded under Field 14 rule 6, the developers' paper that describes this software:*
- *No citation guidance names a paper, so rule 3 does not fire. The README's "Citing" section and `docs/source/cite.rst` (at `a118e6f`) ask users to cite the version they used through its Zenodo record, which is the software deposit (Fields 2 and 12), not a paper.*
- *It is the developers' paper: six of its eight authors (Patel, Hughes, West, Lowder, Seaton, DeForest) are solpolpy authors.*
- *It presents the code in a dedicated section. Its abstract says "We introduce solpolpy, a Python package developed by the PUNCH Science Operations Center (SOC) to carry out this analysis" and ends "Finally, we outline future plans for this technique and software." The IEEE Xplore document outline (https://ieeexplore.ieee.org/document/10508701, read 2026-10-29) lists "I. Introduction, II. PUNCH Mission Overview, III. Methodology, IV. Design of Solpolpy, V. Experimental Application". The ADS full-text index of the paper (2024ssia.conf...57P) independently matches "Design of Solpolpy", "PUNCH Mission Overview", "Methodology" and "Experimental Application" as phrases, while a nonsense-token control matches nothing; it cannot confirm their numerals or order. The full text after Section I requires IEEE sign-in.*
- *It is peer-reviewed: "IEEE requires all conference papers go through the peer review process before publication" (IEEE Author Center, "Understand Peer Review", https://conferences.ieeeauthorcenter.ieee.org/understand-peer-review/). The SSIAI 2024 call for papers asked for four-page full papers and announced acceptance decisions. ADS marks the record NOT REFEREED; that is ADS's classification of conference proceedings, not a statement about the venue's review.*
- *Its authors point to it as solpolpy's paper: Kovac et al. 2026 (arXiv:2512.13407, §8.3) credit "solpolpy, a solar polarization resolver (Hughes et al. 2024; Patel et al. 2024)", that is the 0.4.0 Zenodo deposit (https://doi.org/10.5281/zenodo.14207554) and this paper.*
- *DOI verified via Crossref (proceedings article, published 2024-03-17, pages 57–60, the eight authors above); it resolves.*

*The paper's Acknowledgments could not be read (behind IEEE sign-in). A statement there funding solpolpy would bear on Fields 25 and 26 (see O4), so a later refresh with access should read it.*

*Superseded value. HSSI held https://doi.org/10.3847/1538-4357/ac43b6 — DeForest, C. E., Seaton, D. B., & West, M. J. (2022), "Three-polarizer Treatment of Linear Polarization in Coronagraphs and Heliospheric Imagers", The Astrophysical Journal 927(1), 98 — from the 2026-07-28 extraction until the 0.8.0 release update. It had been chosen because README line 7 says solpolpy is "based on" it. It is the method paper the software implements: it predates the code, and its full text (searched in ADS) contains no "software", "python" or "solpolpy", while a control term, "polarizer", matches. Field 14 rule 5 therefore excludes it, and rule 8 moved it to Field 27, where rule 4 admits it; it should not be moved back.*

### 15. License (RECOMMENDED)
- **License:** GNU Lesser General Public License v3.0 only
- **License URI:** https://spdx.org/licenses/LGPL-3.0-only.html

*Source note: `LICENSE.txt` is an explicit LGPL-v3 grant. This supersedes the previously recorded `Creative Commons Attribution 4.0 International`, which describes the Zenodo deposit record rather than the code. The conflicting source evidence and correction rationale are recorded under Durable Metadata Decisions below.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- polarization
- polarimetry
- coronagraph
- corona
- solar
- solar physics
- solar imaging
- heliophysics
- image processing
- calibration
- fits
- python
- punch
- astronomy astrophysics
- data analysis

*Source note: `astronomy astrophysics`, `data analysis`, `polarization`, `punch` and `solar` map directly to the repository's GitHub topics (`astronomy-astrophysics`, `data-analysis`, `polarization-data`, `polarization-imaging`, `punch`, `solar`), also reported by SoMEF. `solar physics` and `heliophysics` come from `docs/source/index.rst` ("transforming between different polarization systems in solar physics and heliophysics"). `corona`/`coronagraph` come from `instruments.py::construct_mask` ("This is a standard coronograph mask") and `get_instrument_mask`. `solar imaging` and `fits` describe the FITS solar image-triplet inputs; `image processing` describes the `sunkit_image.radial` enhancement and mask handling; `calibration` describes the polarizer-offset/reference-angle corrections; and `python` follows Field 13. Field 16 permits the project-specific `polarization` and `polarimetry` terms.*

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific

*Source note: `instruments.py::load_data` takes a list of local FITS file paths and dispatches on observatory/instrument header keywords (`INSTRUME`, `DETECTOR`, `OBSRVTRY`, `POLAR`, `POLARREF`, `POLAROFF`); `get_instrument_mask` and `get_colormap_str` branch per instrument. The bundled sample data are observatory-specific products (`tests/test_support_files/lasco_*.fts` with `INSTRUME=LASCO, DETECTOR=C2, TELESCOP=SOHO`; `stereo_*.fts` with `INSTRUME=SECCHI, DETECTOR=COR2, OBSRVTRY=STEREO_A`). Per Field 17 and the Field 31/32 guidance, an observatory-specific source is cross-listed here alongside the Related Observatories. No remote archive client exists, so no other source is selected.*

### 18. Input File Formats (RECOMMENDED)
- FITS

*Source note: Confirmed by `instruments.py::load_data` using `astropy.io.fits.open`, the `.fts` sample files in `tests/test_support_files/` and `docs/source/data/`, and the `resolve` docstring ("a list of paths to FITS files"). No other input format is read anywhere in the package.*

### 19. Output File Formats (RECOMMENDED)
Not found

*Source note: the previously recorded value `FITS` is deliberately excluded because solpolpy writes no files at all: a repository-wide search for `writeto`, `.write(`, `to_fits` and file-open-for-write across `solpolpy/` and `tests/` returns zero matches. `core.py::resolve` returns in-memory `ndcube.NDCollection`/`NDCube` objects, which carry the FITS-derived headers and WCS copied from the inputs (`instruments.py::load_data` sets `meta=dict(hdul[hdu_index].header)`; each transform propagates and updates that header, e.g. `POLAR`, `POLARREF`, `POLAROFF`), and `util.py::collection_to_maps` hands off `sunpy.map.Map` objects that the **caller** may choose to serialize. Field 19 records the formats the software itself writes, so no value is defensible here. Field 18 is unaffected: solpolpy definitively reads FITS.*

### 20. Operating System (RECOMMENDED)
- Operating System Independent

*Source note: Confirmed by the `pyproject.toml` classifier `Operating System :: OS Independent` (also on PyPI) and by the package being pure Python with no compiled extensions or platform-specific code. Not narrowed to Linux/Mac/Windows, which would be less informative; CI only exercises `ubuntu-latest`.*

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

*Source note: Confirmed by the package being pure Python (`[tool.setuptools] packages = ['solpolpy']`, no compiled extensions, no GPU/MPI/HPC code).*

### 22. Related Phenomena (OPTIONAL)
- Solar Corona

*Source note: The package resolves polarization of coronal Thomson-scattered light from coronagraph images (DeForest et al. 2022; `instruments.py` coronagraph occulter masks; `plotting.py` coronal radial-enhancement filters). `Coronal Mass Ejections` was considered and dropped: no CME detection, tracking or CME-specific code or documentation exists in the repository, and the value is not implied merely by supporting coronagraph instruments.*

### 23. Development Status (RECOMMENDED)
Active

*Source note: Rule 6 (recency) gives `Active`. The last commit on the default branch `main` is `a118e6f` (2026-10-16T15:20:38Z, "update version"), the commit tagged `0.8.0`; the 20 release tags on `main`'s lineage run from 0.0.1 (2023-11-06) to 0.8.0 (2026-10-16), and every release is published on PyPI. GitHub reports `archived: false`; the README carries no repostatus badge, and neither it nor the docs make a status statement, so rules 1–4 do not fire. CI runs on push, pull request and a weekly cron, with `pre-commit.ci` autoupdates. A later refresh re-applies rule 6 from the date of the last commit on `main`.*

### 24. Documentation (RECOMMENDED)
https://solpolpy.readthedocs.io/

*Source note: Confirmed by the README link, `.readthedocs.yaml`, and SoMEF (`documentation` -> `https://solpolpy.readthedocs.io/`, format `readthedocs`). The GitHub repository homepage field gives the equivalent `https://solpolpy.readthedocs.io/en/latest/`; HSSI's version-independent root form is kept.*

### 25. Funder (OPTIONAL)
Not found

*Source note: Not found — the repository contains no funding statement, acknowledgement section, grant number, or funder metadata; DataCite `fundingReferences` for the concept DOI is an empty list; SoMEF found no funding or acknowledgement fields. National Aeronautics and Space Administration was considered and rejected on the settled rationale recorded below: PUNCH mission sponsorship is not evidence that NASA funded this software package.*

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

*Source note: Not found — no award title or number appears anywhere in the repository, and DataCite `fundingReferences` is empty.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.3847/2515-5172/ad0b0d
- https://doi.org/10.3847/1538-4357/ac43b6

*Source notes:*
- *`https://doi.org/10.3847/2515-5172/ad0b0d` — Patel, R., Seaton, D. B., Caspi, A., Kovac, S., et al. (2023), "A Chromatic Treatment of Linear Polarization in the Solar Corona at the 2023 Total Solar Eclipse", Research Notes of the AAS 7(11), 241 (also arXiv:2312.07490). Cited by the software itself: the `plotting.py::generate_rgb_image` docstring reads "Generate an RGB color image from an NDCollection **based on Patel et al. 2023 Res. Notes AAS 7 241**", and `docs/source/example.ipynb` cell 34 repeats the attribution with the DOI link. The note itself uses the software: its images are "converted to triplets using the solpolpy solar polarization resolver Python package". First recorded at the 2026-07-28 extraction, when HSSI carried no related publications; kept as an incumbent (rule 7) and as the basis of `generate_rgb_image` (rule 4). DOI verified via Crossref (title, journal, volume 7, page 241, first author Patel).*
- *`https://doi.org/10.3847/1538-4357/ac43b6` — DeForest, C. E., Seaton, D. B., & West, M. J. (2022), "Three-polarizer Treatment of Linear Polarization in Coronagraphs and Heliospheric Imagers", The Astrophysical Journal 927(1), 98. Rule 4: the one method paper solpolpy is built on, and the project presents it as such. README line 7 says solpolpy is "based on" it; the `solpolpy/transforms.py` module docstring names it as the source of the equations; the transform functions' `Notes` sections cite specific equation numbers from it; and `docs/source/quickstart.rst` says "The equations required for the transformations from one system to another can be found in `Deforest et al. 2022`_" (all at `a118e6f`). It was Field 14's value until the 0.8.0 release update moved it here (see Field 14). DOI verified via Crossref (title, journal, volume 927, page 98, authors DeForest/Seaton/West).*

*Literature search, 2026-10-29, covering all years (no earlier search was recorded):*
- *Routes: ADS/SciX full text, abstracts and titles for "solpolpy", "solar polarization resolver" and "punch-mission/solpolpy", and its acknowledgements index for "solpolpy" (no paper acknowledges solpolpy there); DataCite and Crossref queries for "solpolpy"; Zenodo creator-keyed searches on Patel, Hughes and West by ORCID and by name, and on Walbridge by name. Controls: a nonsense token returned nothing in ADS and DataCite; a comparable package name returned hits in ADS (full text and acknowledgements), DataCite and Crossref; and the Zenodo creator searches returned the DASH 2023 record that ADS had found.*
- *Semantic Scholar's keyword search was not covered; the next literature search should include it. Its citation list for the Field 14 paper held only Kovac et al. 2026.*
- *The developers' SSIAI 2024 paper presenting solpolpy is the Field 14 value, so it is not repeated here.*

*Weighed and not listed, so a later refresh does not re-propose them:*
- *Kovac, S. A., Caspi, A., Seaton, D. B., et al. (2026), "Citizen CATE 2024: Extending Totality During the 8 April 2024 Total Solar Eclipse with a Distributed Network of Community Participants", Solar Physics 301, 12, https://doi.org/10.1007/s11207-025-02588-9 (arXiv:2512.13407). Its §8.3, "RGB Polarization Processing", converts the eclipse images to a three-polarizer basis "using solpolpy, a solar polarization resolver (Hughes et al. 2024; Patel et al. 2024)". It is a developer-led use paper: the first author, Sarah Kovac, is a solpolpy author, and six solpolpy authors (Kovac, Seaton, DeForest, Hughes, Lamb, Patel) are among its 243 authors. It is neither the developers' paper about the software (rule 3) nor a third-party use (rule 5), and the maintainer decided on 2026-10-29 not to list it. The decision turns on who led the paper: a use paper led by a solpolpy developer is not listed.*
- *Meeting abstracts (rule 1), each led by a solpolpy author: Walbridge et al., AGU Fall Meeting 2022, "A New Universal Polarization Resolving Software Package for Solar Coronal and Heliospheric Observations" (2022AGUFMSH42E2331W); Patel et al., SPD 2023, "SolPolPy: Solar Polarization Resolver in Python" (2023SPD....5440506P); Patel et al., AGU 2023, "PUNCH Polarization Resolver and the IMAX Effect" (2023AGUFMSH23E2977P); Hughes et al., AGU 2024 and AGU 2025, on PUNCH Science Operations Center data products and software (2024AGUFMSH23B2943H, 2025AGUFMSH11E2095H); Patel et al., AAS 246 (2025), "Resolving Wide-field Polarization with Evolving Capabilities of solpolpy" (2025AAS...24612606P); Patel et al., AGU 2025, "PUNCHing Through the Heliosphere with Polarized Light" (2025AGUFMSH21C..06P); and Patel et al., SPD 2026, "Viewing Heliosphere through the Polarized Glasses" (2026SPD....5710403P). The Zenodo creator searches found no deposited poster for any of them.*
- *Hughes et al. (2023), "Interoperability of PUNCH software in the Python ecosystem", DASH 2023 slide deck, https://doi.org/10.5281/zenodo.8412311. Rule 3 does not admit it: its subject is the interoperability of the PUNCH packages and its demo is regularizepsf; solpolpy appears only as one box in its package-dependency diagram (slide 3) and in the deposit's abstract. Because it fails on subject, the slide-deck standalone test does not arise.*
- *PUNCH Science Operations Center and punchbowl presentations by the same team: https://doi.org/10.5281/zenodo.8412195 (DASH 2023, punchbowl), https://doi.org/10.5281/zenodo.13925458 (2024, PUNCH SOC data products and software), https://doi.org/10.5281/zenodo.17382250 (2025, punchbowl) and https://doi.org/10.5281/zenodo.23126384 (2026, PUNCH data-system reusability). Their subject is the mission's data system and punchbowl, not solpolpy.*
- *The solpolpy Zenodo software deposits that ADS indexes are software, not publications (rule 1; Fields 2 and 12).*

### 28. Related Datasets (OPTIONAL)
Not found

*Source note: Not found — the repository bundles small sample FITS files (SOHO/LASCO C2 from 2000-09-03 and STEREO-A/SECCHI COR2 from 2010-04-03) for tests and documentation, but these are excerpts committed to the repository with no dataset DOI or archive landing page cited anywhere. No dataset DOI appears in the README, docs, `CITATION.cff` or DataCite metadata.*

### 29. Related Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.14029123

*Source note: This DOI identifies **punchbowl** (DataCite title "punchbowl", Zenodo, resourceTypeGeneral Software; repository https://github.com/punch-mission/punchbowl, described as "PUNCH science calibration code" / "Calibration for the PUNCH mission"). It passes the Field 29 relevance gate as a **companion package from the same mission**: punchbowl's `pyproject.toml` lists `solpolpy` in its required `dependencies` (`solpolpy == 0.8.0` at punchbowl `d2d44328`, 2026-10-27), and its changelog shows it performing the PUNCH polarization transformation and "Corrections for polarized data production" through solpolpy (`CHANGELOG.rst` line 130 at `d2d44328`). It is distinguishing — it tells a reader that solpolpy is the polarization engine inside the PUNCH science pipeline. No evidence supports removal, so it is kept.*

*Gate decisions (audit trail). Excluded from Field 29: `numpy`, `matplotlib`, `networkx` — Tier A generic infrastructure (arrays, plotting, graph algorithms; all would be equally at home in a web app, a finance model or a biology pipeline). `astropy` — Tier B, and its use here (units, `io.fits`, `wcs`) is ordinary dependency use, not a distinguishing relationship. `sunpy`, `ndcube`, `sunkit_image` — declared dependencies, and per the refresh instruction they are not listed here merely for being dependencies; `sunpy` and `ndcube` instead appear in Field 30 on specific public-API exchange evidence, and `sunkit_image` is excluded from both fields (see Field 30). `regularizepsf` (https://github.com/punch-mission/regularizepsf) — considered because it is a sibling punch-mission package and a punchbowl dependency, but rejected: it performs an unrelated task (point-spread-function correction), and there is no dependency, import, adapter or data exchange in either direction between solpolpy and regularizepsf.*

### 30. Interoperable Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.14029123
- https://doi.org/10.5281/zenodo.5715150
- https://doi.org/10.5281/zenodo.591887

*Source note:*
- *`https://doi.org/10.5281/zenodo.14029123` (**punchbowl**) — punchbowl's `pyproject.toml` declares `solpolpy` as a required dependency (pinned `== 0.8.0` at punchbowl `d2d44328`), and punchbowl passes its `ndcube` data products through solpolpy's `resolve` to produce PUNCH polarized data products (punchbowl `CHANGELOG.rst` at `d2d44328`, lines 129–130: "Shifting masking in the starfield image processor before polarization transformations, to ensure masking." and "Corrections for polarized data production.", pull requests #857 and #860). This is a demonstrated exchange between two peer heliophysics tools from the same mission.*
- *`https://doi.org/10.5281/zenodo.5715150` (**ndcube**, https://github.com/sunpy/ndcube) — recorded on specific evidence: `ndcube`'s data model **is** solpolpy's documented public interchange format, not an internal implementation detail. `core.py::resolve` is typed `(input_data: list[str] | NDCollection, ...) -> NDCollection`; `instruments.py::load_data` returns an `NDCollection`; every function in `transforms.py` accepts and returns `NDCollection`; `plotting.py::plot_collection` and `util.py::collection_to_maps` consume them; `docs/source/example.ipynb` cell 5 directs users to the NDCube documentation; and `docs/source/quickstart.rst` accesses results as `output_collection['tB'].data` (the key was `'B'` before 0.8.0; both at `a118e6f`). This is the "shared NDCube data model" pattern the field guidance marks as qualifying. Concept DOI resolved via the Zenodo API.*
- *`https://doi.org/10.5281/zenodo.591887` (**sunpy**, https://github.com/sunpy/sunpy) — recorded on specific evidence: `util.py::collection_to_maps` is a **public exported adapter** (listed in `solpolpy/__init__.py`'s `__all__`) whose documented purpose is "Convert an NDCollection to a list of SunPy Map objects", returning `sunpy.map.Map` instances — the `to_sunpy_map()` converter pattern named as qualifying in the field guidance. Additionally `plotting.py::get_colormap_str` is a public function returning SunPy colormap names (`soholasco2`, `kcor`, `stereocor2`, …) for use with `sunpy.visualization.colormaps`, and `docs/source/example.ipynb` cell 2 imports `collection_to_maps` directly. Concept DOI confirmed via DataCite ("sunpy: A Core Package for Solar Physics", Software).*

*Gate decisions (audit trail). Excluded from Field 30: `numpy`, `matplotlib`, `networkx` — Tier A, never listed; being a dependency is not interoperability. `astropy` — Tier B; its use (`astropy.units` quantities, `io.fits` reading, `wcs`) is internal dependency use and no adapter or documented interchange with astropy-as-a-peer-tool exists, so it does not clear the Tier B evidence bar. `sunkit_image` — genuinely domain-specific and user-visible through `generate_rgb_image(enhancement_method=...)`, which lets a user select `nrgf`/`fnrgf`/`rhef`/`intensity_enhance`, but this is best characterised as "uses internally with a user-facing switch" rather than a bidirectional data-model exchange or a plugin relationship, so it is excluded from both fields; that exclusion is settled, and the reasoning is recorded here so it is not re-proposed. `regularizepsf` — excluded, see Field 29. Blanket claims of the form "part of the scientific Python ecosystem" were not used for any entry.*

### 31. Related Instruments (OPTIONAL)
1. **Large Angle Spectroscopic Coronagraph**
   - Instrument Identifier: https://spase-metadata.org/SMWG/Instrument/SOHO/LASCO
2. **Stereo-A Sun Earth Connection Coronal and Heliospheric Investigation**
   - Instrument Identifier: https://spase-metadata.org/SMWG/Instrument/STEREO-A/SECCHI
3. **Stereo-B Sun Earth Connection Coronal and Heliospheric Investigation**
   - Instrument Identifier: https://spase-metadata.org/SMWG/Instrument/STEREO-B/SECCHI
4. **MLSO K-Coronagraph**
   - Instrument Identifier: https://spase-metadata.org/NSF/Instrument/Ground/MLSO/K-Cor

*Source note: Each instrument is directly supported by instrument-specific code paths and carries its SPASE identifier. Full per-candidate resolution evidence is recorded below.*

*Relevance evidence:*
- *LASCO — `instruments.py::get_instrument_mask` branches on `header["INSTRUME"] == "LASCO"` with detector-specific occulter radii (C2 -> 2.5 R_sun, C3 -> 4.0 R_sun) and raises `UnsupportedInstrumentError` otherwise; `plotting.py::get_colormap_str` selects `soholasco2`/`soholasco3` for the same detectors; `tests/test_support_files/lasco_{-60,0,+60,clear}.fts` are real LASCO C2 frames (`INSTRUME=LASCO, DETECTOR=C2, TELESCOP=SOHO`); the README and `docs/source/index.rst` use LASCO/C2 as the headline worked example; `tests/fixtures.py` sets `OBSRVTRY: "LASCO"`.*
- *SECCHI on STEREO-A and STEREO-B — `get_instrument_mask` branches on `INSTRUME == "SECCHI"` with COR1 -> 1.57 R_sun and COR2 -> 3.0 R_sun; `get_colormap_str` returns `stereocor1`/`stereocor2`; `constants.py` defines per-spacecraft polarizer reference angles `STEREOA_REFERENCE_ANGLE = 45.8 deg` and `STEREOB_REFERENCE_ANGLE = -18 deg`, applied by `core.py::determine_reference_angle` on `OBSRVTRY in {"STEREO_A", "STEREO_B"}` — explicit, separate support for each spacecraft; `tests/test_support_files/stereo_*.fts` and `docs/source/data/stereo_*.fts` are real STEREO-A SECCHI COR2 triplets; `docs/source/example.ipynb` is built end-to-end on STEREO/COR-2 data.*
- *MLSO K-Coronagraph (the COSMO K-Coronagraph) — `get_instrument_mask` branches on `INSTRUME == "COSMO K-Coronagraph"` with a 1.15 R_sun occulter radius, and `get_colormap_str` returns the `kcor` colormap for the same header value.*

### 32. Related Observatories (OPTIONAL)
1. **PUNCH Mission**
   - Observatory Identifier: https://spase-metadata.org/NASA/Observatory/PUNCH
2. **Solar and Heliospheric Observatory**
   - Observatory Identifier: https://spase-metadata.org/SMWG/Observatory/SOHO
3. **Solar Terrestrial Relations Observatory A**
   - Observatory Identifier: https://spase-metadata.org/SMWG/Observatory/STEREO-A
4. **Solar Terrestrial Relations Observatory B**
   - Observatory Identifier: https://spase-metadata.org/SMWG/Observatory/STEREO-B
5. **Mauna Loa Solar Observatory**
   - Observatory Identifier: https://spase-metadata.org/SMWG/Observatory/Ground/MaunaLoaSO

*Source note: `PUNCH Mission` is the surviving canonical form after the vocabulary consolidated the earlier `.html` duplicate onto the upstream bare identifier; the accompanying name is the surviving row's stored name, not an unevidenced rename. Every value carries its SPASE identifier. Full per-candidate resolution evidence and the settled PUNCH decision are recorded below.*

*Relevance evidence:*
- *PUNCH — `docs/source/index.rst`: "It has been developed as part of the PUNCH mission"; `docs/source/conf.py` copyright "2026, PUNCH Science Operations Center"; `instruments.py::load_data` carries a PUNCH-specific instruction ("For many spacecraft this should be 0. For PUNCH it should be set to 1"); `docs/source/quickstart.rst` documents the polarizer-foreshortening correction for PUNCH's Wide Field Imager; GitHub topic `punch`, organization `punch-mission`; and punchbowl (the PUNCH pipeline) drives solpolpy. Purpose-built mission-team tool.*
- *SOHO — host observatory of LASCO, whose data solpolpy has instrument-specific support for (Field 31); the bundled LASCO sample frames carry `TELESCOP = SOHO`, and the colormap names `soholasco2`/`soholasco3` are SOHO/LASCO-specific.*
- *STEREO-A and STEREO-B — supported individually and by name: `core.py::determine_reference_angle` matches `OBSRVTRY` values `"STEREO_A"` and `"STEREO_B"` and applies the distinct per-spacecraft polarizer reference angles from `constants.py`; the bundled sample data are `OBSRVTRY = STEREO_A`.*
- *Mauna Loa Solar Observatory — host observatory of the K-Coronagraph supported in Field 31 (`INSTRUME == "COSMO K-Coronagraph"` occulter radius and `kcor` colormap).*

### 33. Logo (OPTIONAL)
Not found

*Source note: Not found — no logo file or logo reference exists in the repository, SoMEF's output contains no `logo` key, the README has no logo image, and solpolpy is not in any PyHC registry (so no curated PyHC logo is available). The repository's `eg_image.png` (also `docs/source/eg_image.png`) is an example polarization-conversion result figure used in the README and documentation, not a project logo, so it is deliberately not used here.*

---

## Durable Metadata Decisions and Resolution Evidence

### A. Previous incorrect values and why they were corrected

**A1. Field 15 (License): `GNU Lesser General Public License v3.0 only` supersedes `Creative Commons Attribution 4.0 International`.**

Three sources disagreed; all four were checked directly.

1. **`LICENSE.txt` (852 lines, 43 KB) — the actual license grant in the repository, and the file `pyproject.toml` points at.** Its opening paragraph reads: *"Copyright (c) 2024, PUNCH Science Operations Center / This software may be used, modified, and distributed under the terms of the GNU Lesser General Public License v3 (LGPL-v3); both the LGPL-v3 and GNU General Public License v3 (GPL-v3) are reproduced below. / There is NO WARRANTY associated with this software."* The complete LGPL-3.0 text followed by the complete GPL-3.0 text is reproduced beneath it. This is an unambiguous LGPL-3.0-only grant.
2. **`pyproject.toml` classifier `License :: OSI Approved :: MIT License` — stale and unsupported.** No MIT license text appears anywhere in the repository. The same file's authoritative `license` key is `{ file="LICENSE" }`, i.e. it defers to the license file, whose text is LGPL-v3. PyPI reflects only this classifier (`info.license` and `info.license_expression` are both `null`) and carries no MIT text. A trove classifier with no corresponding license text cannot override an explicit written grant. (Minor related defect: the key names `LICENSE` while the file on disk is `LICENSE.txt`.)
3. **GitHub's licensee detection — neither supports nor refutes, but rules out MIT and CC-BY.** `GET /repos/punch-mission/solpolpy/license` returns `{"key":"other","name":"Other","spdx_id":"NOASSERTION"}` for `path: LICENSE.txt`; the custom PUNCH preamble prevents automatic classification. It does not detect MIT or CC-BY-4.0.
4. **Zenodo/DataCite `rightsList` `cc-by-4.0` — describes the Zenodo deposit, not the code.** DataCite reports `Creative Commons Attribution 4.0 International` for the concept DOI, and the Zenodo API shows `license.id == "cc-by-4.0"` identically on **all 20** version records from 0.0.1 (2023-11-06) through 0.8.0 (2026-10-16). That uniformity is the signature of a one-time default chosen in the GitHub-Zenodo integration; Zenodo's license field is not derived from the repository's LICENSE file and here contradicts it.

An archive's deposit-record default does not override the software's own explicit legal license grant, and HSSI Field 15 asks for "the full name of the license **assigned to this software**". `GNU Lesser General Public License v3.0 only` is the exact SPDX title for `LGPL-3.0-only`. The settled result is that the software's own written licence grant governs Field 15, while CC-BY-4.0 describes the Zenodo deposit record rather than the code.

**A2. Field 12 (Version): history of the stored release.**

The number must remain bare (`0.8.0`, never `solpolpy - 0.8.0`): HSSI adds the software-name prefix when rendering a version, so a stored prefix would render twice. The entry carries all four sub-fields shown in Field 12 rather than only a number.

At the 2026-07-28 extraction HSSI held 0.5.1, six releases behind. Five sources then agreed that 0.7.0, released 2026-07-28, was current: git tag `0.7.0` (at `a600958`, "Merge pull request #221 from punch-mission/release-0.7.0"); `CITATION.cff` `version: 0.7.0` / `date-released: 2026-07-28`; `CHANGELOG.rst` "Version 0.7.0: July 28, 2026"; PyPI `info.version` 0.7.0, uploaded 2026-07-28T08:43:27; and DataCite for the concept DOI, `version: "0.7.0"`, `Issued 2026-07-28`. The 0.8.0 release of 2026-10-16 superseded 0.7.0; Field 12 records its evidence and why the 0.7.0 description form was not carried forward.

**A3. Field 19 (Output File Formats): `FITS` was removed by the settled user decision of 2026-07-28.** Solpolpy writes no files — a repository-wide search for `writeto`, `.write(`, `to_fits` and file-open-for-write across `solpolpy/` and `tests/` returns zero matches. `resolve` returns in-memory `NDCollection`/`NDCube` objects, and `util.py::collection_to_maps` hands off `sunpy.map.Map` objects that the *caller* may serialize; Field 19 means formats the software itself writes, so no value is defensible and the field remains "Not found".

**A6. Field 6 (Authors): the canonical spelling is `Sarah Kovac`.** The ORCID registry record for `https://orcid.org/0000-0003-1714-5970` gives `family-name: Kovac` (no credit-name, no other-names), and Crossref (Patel et al. 2023 author list) and punchbowl's `pyproject.toml` independently agree. The repository's `CITATION.cff` still carries the upstream typo `Kovak`, and DataCite inherits it by deriving its creators from that file — worth reporting upstream. Author count remains exactly 9; her ORCID and her `NSF NCAR High Altitude Observatory` / `https://ror.org/03773p874` affiliation are unchanged.

### B. Field 31/32 SPASE resolution evidence

Resolved against HSSI's controlled instrument/observatory vocabulary, in which `type` 1 = instrument (Field 31) and `type` 2 = observatory (Field 32). Every selected entry carries a `https://spase-metadata.org/...` identifier.

| Candidate | Searched | Found | Ladder rung applied | Result |
|---|---|---|---|---|
| PUNCH (observatory) | `/\bPUNCH\b/`, `/Polarimeter to Unify/` | 2 same-resource observatory rows at extraction time: `PUNCH Mission` (`.../NASA/Observatory/PUNCH`) and `Polarimeter to Unify the Corona and Heliosphere (PUNCH)` (`.../NASA/Observatory/PUNCH.html`) | **Rung 1** — the earlier `.html` choice was superseded when the vocabulary consolidated onto the upstream bare identifier | Field 32 records `PUNCH Mission` + `https://spase-metadata.org/NASA/Observatory/PUNCH`; the settled decision is explained below |
| LASCO (instrument) | `/LASCO/`, `/Large Angle/` | the row `Large Angle Spectroscopic Coronagraph`, abbr `LASCO` | **Rung 1** | Selected with `https://spase-metadata.org/SMWG/Instrument/SOHO/LASCO` |
| SOHO (observatory) | `/\bSOHO\b|Solar and Heliospheric Obs/` type 2 | same-name rows `Solar and Heliospheric Observatory`: `CNES/Observatory/CDPP-AMDA/SOHO` and `SMWG/Observatory/SOHO` | **Rung 1 after the documented SMWG tie-break** for same-name duplicates | Selected `Solar and Heliospheric Observatory` + `https://spase-metadata.org/SMWG/Observatory/SOHO` |
| SECCHI (instrument) | `/SECCHI/` | Spacecraft-level rows `Stereo-A …` (`SMWG/Instrument/STEREO-A/SECCHI`) and `Stereo-B …` (`SMWG/Instrument/STEREO-B/SECCHI`); detector-level Cor1/Cor2 rows for each spacecraft; EUVI, HI-1 and HI-2 rows | **Rung 2** — concrete per-spacecraft evidence for A and B (`STEREOA_REFERENCE_ANGLE`, `STEREOB_REFERENCE_ANGLE`, `OBSRVTRY` match arms) | Selected both spacecraft-level SECCHI rows. EUVI/HI rows lack repository evidence, and Cor1/Cor2 rows are deliberately represented by their parent suites as explained below |
| STEREO (observatory) | `/\bSTEREO\b/` type 2 | `SMWG/Observatory/STEREO`, `…/STEREO-A` and `…/STEREO-B`, plus CNES/CDPP variants | **Rung 2** — concrete evidence for A and B individually; SMWG preferred over the CNES duplicates | Selected the STEREO-A and STEREO-B observatory rows. Mission-level `Solar-Terrestrial Relations Observatory` is omitted as redundant |
| COSMO K-Coronagraph (instrument) | `/COSMO|K-Cor|KCor|Coronal Solar Magnetism/` | the row `MLSO K-Coronagraph` (`NSF/Instrument/Ground/MLSO/K-Cor`) — the COSMO K-Coronagraph at Mauna Loa | **Rung 1** | Selected `MLSO K-Coronagraph` + `https://spase-metadata.org/NSF/Instrument/Ground/MLSO/K-Cor` |
| Mauna Loa Solar Observatory (observatory) | `/Mauna Loa|MLSO/` type 2 | same-name rows `Mauna Loa Solar Observatory`: `NSF/Observatory/Ground/MLSO` and `SMWG/Observatory/Ground/MaunaLoaSO` | **Rung 1 after the documented SMWG tie-break** | Selected `Mauna Loa Solar Observatory` + `https://spase-metadata.org/SMWG/Observatory/Ground/MaunaLoaSO`; the namespace difference is settled below |
| PUNCH WFI / NFI (instruments) | `/\bPUNCH\b/` type 1 | rows named `Wide Field Imager` and a `Narrow Field Imager` row | **Rung 5 — omitted, and it fails the relevance gate first** | `docs/source/quickstart.rst` frames the correction generically, and the current source contains no WFI- or NFI-specific code path. Mission-level PUNCH support is captured in Field 32 |
| PROBA-3 / ASPIICS, Metis, Solar Orbiter | `/proba|aspiics|metis|solar[-_ ]orbiter|solo/` across all `*.py`, `*.rst`, `*.md`, `*.toml`, `*.cff`, `*.yml`, `*.yaml`, plus a JSON-level scan of `docs/source/example.ipynb` | **zero matches anywhere in the repository** | **Rung 5 — omitted** | PROBA-3/ASPIICS was considered and rejected because it is not supported, mentioned, or hinted at anywhere in the source tree at `a600958` |

No Field 31/32 value is recorded without a `https://spase-metadata.org/` identifier.

### C. Settled decisions and negative research

- **O1 — PUNCH observatory row: settled on the bare (non-`.html`) SPASE identifier.** When this dossier was first written, HSSI's vocabulary carried the same PUNCH observatory twice, under *different* names: `PUNCH Mission` (`https://spase-metadata.org/NASA/Observatory/PUNCH`) and `Polarimeter to Unify the Corona and Heliosphere (PUNCH)` (`https://spase-metadata.org/NASA/Observatory/PUNCH.html`). The record HSSI already held for solpolpy was the `.html` row, so that form was initially retained to avoid renaming an established value without evidence it was wrong. That premise was later superseded: `https://spase-metadata.org/NASA/Observatory/PUNCH` is the registered identifier in the maintained upstream SPASE registry, which does not publish the `.html` variant, and HSSI's vocabulary has since been consolidated onto those upstream identifiers, retiring the `.html` duplicate as a row. Field 32 therefore records `PUNCH Mission` + `https://spase-metadata.org/NASA/Observatory/PUNCH`, the surviving row's stored name copied verbatim; the accompanying name change is a consequence of that consolidation, not an unevidenced rename. The `.html` form should not be reintroduced.
- **O2 — SECCHI granularity.** `get_instrument_mask` and `get_colormap_str` branch on the `DETECTOR` keyword for COR1 vs COR2, which is concrete detector-level evidence. The selected values deliberately use the two spacecraft-level SECCHI parent rows rather than expanding one instrument suite into four detector rows. The detector alternatives considered and declined were `STEREO-A SECCHI Cor1 Coronagraph` (`https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/Cor1`), `STEREO-A SECCHI Cor2 Coronagraph` (`https://spase-metadata.org/SMWG/Instrument/STEREO-A/SECCHI/Cor2`), `STEREO-B SECCHI Cor1 Coronagraph` (`https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/Cor1`), and `STEREO-B SECCHI Cor2 Coronagraph` (`https://spase-metadata.org/SMWG/Instrument/STEREO-B/SECCHI/Cor2`).
- **O3 — MLSO namespace mismatch.** The selected observatory uses the SMWG duplicate (`SMWG/Observatory/Ground/MaunaLoaSO`) per the same-name SMWG tie-break, while the selected K-Coronagraph instrument sits under the NSF namespace (`NSF/Instrument/Ground/MLSO/K-Cor`). Both identifiers are correct and unambiguous. The NSF observatory alternative, `https://spase-metadata.org/NSF/Observatory/Ground/MLSO`, was considered and declined because namespace-path consistency does not outweigh the standing same-name SMWG tie-break.
- **O4 — Funder: investigated, and deliberately not asserted.** No funding statement, acknowledgement or grant reference exists anywhere in the repository, and DataCite `fundingReferences` for the concept DOI is empty, so Field 25 stays "Not found". A plausible candidate — `National Aeronautics and Space Administration` (ROR https://ror.org/027ka1x80), since PUNCH is a NASA Small Explorer mission and the code is copyright the PUNCH Science Operations Center — was weighed and rejected: it rests on the mission's sponsorship rather than on any funding statement attached to this software, and asserting it would be fabrication. The candidate is recorded so a future refresh can recognise it as already investigated, and can record NASA only if the project publishes such a statement. The Field 14 paper (Patel et al. 2024, SSIAI) is the likeliest place for one; its Acknowledgments were behind IEEE sign-in on 2026-10-29.
- **O5 — Bryce Walbridge's identifier and affiliation.** These remain empty. `CITATION.cff` gives him no ORCID, DataCite gives him no `nameIdentifiers`, and a public ORCID registry search for "Bryce Walbridge" returned 0 results. `pyproject.toml` lists his email as `bmw39@calvin.edu`, which suggests **Calvin University** (ROR https://ror.org/059ktz377 — unverified) as an affiliation candidate; this is an inference from an email domain only and was not written into Field 6.
- **O6 — Author name variants.** `pyproject.toml` uses `Matthew J. West` and `Bryce M. Walbridge`; `CITATION.cff` uses `Matthew West` and `Bryce Walbridge`. The `CITATION.cff` forms are retained because the middle-initial variants do not improve identity resolution and could create near-duplicate person records.
- **O8 — `Data Processing and Analysis: Wave Polarization Analysis` is kept.** Included because the taxonomy's own indicator list for that value names "Stokes parameters" and polarization-ellipse quantities, all of which solpolpy computes. The narrower reading — that the category belongs to plasma-wave polarimetry rather than to Thomson-scattering imaging polarimetry — was weighed and rejected: the taxonomy defines the value by the quantities computed, and solpolpy computes exactly those.
- **O10 — Not a PyHC package.** All three PyHC registry files (`projects_core.yml`, `projects.yml`, `projects_unevaluated.yml`) were fetched and read in full; solpolpy appears in none of them (the only punch-mission entry is `regularizepsf`). No curated PyHC metadata was therefore available for logo, documentation or keywords.
