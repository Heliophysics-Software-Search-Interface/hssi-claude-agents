# HSSI Metadata Extraction Results

**HSSI Software ID:** a74cb76b-da08-4412-817f-3240e52c5dde
**Repository:** https://github.com/HinodeXRT/xrtpy
**Source Revision:** 0ef8e3636bde9c619dbcb1f74519f31829f238ad (branch `main`, 2026-07-22)
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** Joy Velasquez
- **Submitter Email:** joy.velasquez@cfa.harvard.edu
- **Source:** Submitter of record in HSSI (ORCID 0009-0005-4804-0946).
- **Note:** The earlier duplicate HSSI submission of the same software was made by Shawn A. Polson
  (shawn.polson@lasp.colorado.edu); the submitter of record for this entry is unchanged.

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.13157913
- **Source:** Live HSSI; independently confirmed as the Zenodo **concept** DOI — DataCite reports
  `conceptdoi = 10.5281/zenodo.13157913` for record 13157914, and the DOI resolves.
- **Note:** The repository README badge points at the **version** DOI
  `https://doi.org/10.5281/zenodo.13157914` (v0.4.1), not the concept DOI. The concept DOI is the
  correct Field 2 value; the badge is not evidence of drift.

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/HinodeXRT/xrtpy
- **Source:** Live HSSI; `pyproject.toml` `urls.Repository`; git remote. URL resolves.

### 4. Software Functionality (MANDATORY)

The set below is supported by a direct audit of `xrtpy/`
(`response/`, `image_correction/`, `util/`, `response/tools/`), the shipped sphinx-gallery examples
(`examples/`, wired in via `docs/conf.py` `examples_dirs = ../examples`), the docs, and the JOSS
paper. Eleven of the values were also present in an earlier duplicate HSSI submission of the same
software.

- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Mission-related
- Mission-related:Analysis
- Mission-related:Calibration
- Mission-related:Instrument Response
- Mission-related:Instrumentation
- Mission-related:Science Data Processing
- Models and Simulations
- Models and Simulations:Instrument Response
- Models and Simulations:Observatory/Instrument Models
- Models and Simulations:Physics-Based

All four required bare parents are present.

**Per-value justification:**

1. **Data Processing and Analysis** — required bare parent for values 2–6.
2. **Data Processing and Analysis:Analysis** — `xrtpy.response.temperature_from_filter_ratio`
   derives electron temperature and volume emission measure maps from an XRT image pair
   (`_derive_temperature`) with propagated uncertainties (`calculate_TE_errors`). Documented in
   `docs/getting_started.rst` "Deriving Temperature and Emission Measure".
3. **Data Processing and Analysis:Calibration** — `EffectiveAreaFundamental` computes
   time-dependent effective areas including CCD and filter contamination-layer transmission
   (`contamination_on_CCD`, `_CCD_contamination_transmission`,
   `_filter_contamination_transmission`); `TemperatureResponseFundamental` converts to
   DN cm^5 s^-1 pix^-1 using CCD gain and eV-per-electron (`ccd_gain_right`, `ev_per_electron`).
   Contamination calibration files are updated per release (`docs/changelog/0.5.1.rst`: CCD
   contamination files updated through 2026-02-22).
4. **Data Processing and Analysis:Image Processing** — `xrtpy.image_correction.deconvolve`
   performs Richardson–Lucy PSF deconvolution via FFT (`_richardson_lucy_deconvolution`,
   `_fft_2dim_convolution`); `xrtpy.image_correction.remove_lightleak` subtracts visible
   stray light from synoptic composite images; `_rebin_psf` applies
   `sunpy.image.transform.affine_transform` and `sunpy.image.resample.resample`.
5. **Data Processing and Analysis:Data Access and Retrieval** — `xrtpy/util/filename2repo_path.py`
   resolves an XRT filename to its URL in the CfA XRT archive (Level 1, Level 1 Qual,
   Level 2 Synoptics composites, Level 2 grade maps, JPEG2000), default
   `urlroot="https://xrt.cfa.harvard.edu/"`. `xrtpy/util/make_exposure_map.py` then calls
   `astropy.utils.data.download_file` on those URLs. `deconvolve` and `remove_lightleak` use
   `sunpy.data.manager.require` to fetch PSF (`PSF560.fits`, `PSF1000.fits`) and light-leak
   (`term_p*.fits`) calibration files from the SolarSoft mirrors in `xrtpy.util.SSW_MIRRORS`.
   Users call these functions to obtain data, so this is a user-facing capability.
6. **Data Processing and Analysis:Data Reduction** — `temperature_from_filter_ratio(binfac=...)`
   spatially bins image pairs via `sunpy.image.resample.reshape_image_to_4d_superpixel` explicitly
   to reduce photon noise; `_rebin_psf` downsamples the 2048x2048 PSF to the image `chip_sum`;
   `Te_err_threshold` / `photon_noise_threshold` masks pixels failing quality thresholds.
7. **Data Visualization** — required bare parent for values 8–9.
8. **Data Visualization:2D Graphics** — the shipped gallery renders 2D image products:
   `examples/remove_lightleak.py` (`xrt_map.plot`, `ax.imshow(diff_data)`),
   `examples/deconvolving.py` (side-by-side original/deconvolved maps),
   `examples/temperature_from_filter_ratios.py` (derived temperature map with colorbar).
9. **Data Visualization:Line Plots** — `examples/effective_area.py` plots effective area versus
   wavelength for multiple dates; `examples/temperature_response.py` plots temperature response
   versus log10(T); `examples/channels.py` plots channel properties. These are the package's
   headline scientific figures (JOSS Figures 1 and 2).
10. **Mission-related** — required bare parent for values 11–15. XRTpy is a Hinode/XRT
    mission-instrument tool authored by the XRT team at the Center for Astrophysics, not a
    general-purpose utility that happens to read XRT files.
11. **Mission-related:Analysis** — mission-specific science analysis of XRT observations
    (temperature/emission-measure diagnostics of the corona from XRT filter pairs).
12. **Mission-related:Calibration** — implements the XRT instrument calibration chain described in
    the SolarSoft XRT Analysis Guide, validated against the IDL reference outputs in
    `xrtpy/response/tests/data/` and generated by `IDL_scripts/IDL_test_scripts/*.pro`.
13. **Mission-related:Instrument Response** — `EffectiveAreaFundamental` and
    `TemperatureResponseFundamental` are the XRT instrument-response computation, driven by the
    mission channel file `xrtpy/response/data/xrt_channels_v0017.genx`.
14. **Mission-related:Instrumentation** — `xrtpy.response.channel` provides an object model of XRT
    hardware: `Geometry` (focal length, aperture area), `EntranceFilter`, `Mirror` (graze angle,
    reflectivity), `Filter` (material, thickness, mesh transmission), `CCD` (gain left/right, full
    well, pixel size, eV per electron), and `Channel` over the 14 XRT filter configurations.
15. **Mission-related:Science Data Processing** — XRTpy consumes Hinode/XRT Level 1 images and
    Level 2 synoptic composites and produces higher-level derived science products (temperature,
    emission measure and uncertainty maps; deconvolved images; light-leak-corrected images), each
    returned as an `XRTMap` with updated FITS `HISTORY` provenance.
16. **Models and Simulations** — required bare parent for values 17–19.
17. **Models and Simulations:Instrument Response** — the effective area and temperature response
    are *forward-modeled* from component physics rather than read from a lookup table:
    `_transmission_equation` builds a complex refractive index `(1-delta) + i*beta` from
    `xrtpy/response/data/n_DEHP.txt`, computes `_angular_wavenumber_CCD` and
    `_filter_contamination_angular_wavenumber` from the graze angle and wavelength, and folds
    mirror reflectivity, filter transmission and CCD response together; `TemperatureResponseFundamental`
    then folds that with CHIANTI emission spectra (`integration`). `deconvolve` additionally uses
    the XRT mirror-model PSF.
18. **Models and Simulations:Observatory/Instrument Models** — the `Geometry`/`EntranceFilter`/
    `Mirror`/`Filter`/`CCD`/`Channel` class hierarchy is a reusable model of the XRT instrument,
    parameterized by the SolarSoft GENX channel model version 17.
19. **Models and Simulations:Physics-Based** — temperature response is computed from a physical
    emission model: CHIANTI v10 atomic emission spectra (coronal, hybrid, photospheric abundance
    sets in `xrtpy/response/data/chianti_emission_models/`) integrated against effective area, solid
    angle per pixel and CCD quantum conversion, using `astropy.constants` (`h`, `c`) and explicit
    astropy units throughout.

**Considered and deliberately excluded** (audit trail):
- `Coordinate Transforms` / `Coordinate Transforms:Solar` — `temperature_from_filter_ratio` does
  compute `sunpy.coordinates.sun.B0` and `angular_radius` and rewrites deprecated `CTYPE1/CTYPE2`
  `SOLAR-X`/`SOLAR-Y` to helioprojective `HPLN-TAN`/`HPLT-TAN`, but this is WCS-metadata hygiene on
  output maps, not a user-facing coordinate-transformation API. `affine_transform` in `_rebin_psf`
  is a pixel-grid transform, not a coordinate-system transform.
- `Data Visualization:Movies` — `examples/sorting_data.py` builds a `MapSequence` animation and
  `docs/conf.py` sets `matplotlib_animations: True`, but the animation is entirely
  `sunpy.map.MapSequence.plot`; XRTpy contributes no animation code.
- `Data Processing and Analysis:Processing` and `Mission-related:Processing` — fully subsumed by
  Calibration / Image Processing / Science Data Processing; listing them would be redundant.
- `Mission-related:Observatory/Instrument Models` — redundant with `Mission-related:Instrumentation`
  plus `Models and Simulations:Observatory/Instrument Models`.
- `Data Processing and Analysis:Energy Spectra` — XRTpy integrates *wavelength* emission spectra for
  instrument response; it does not produce particle energy spectra.
- `Data Processing and Analysis:File Format Conversion` — XRTpy *reads* IDL SolarSoft
  `.genx`/`.geny`/`.sav` and FITS but never writes a converted format (see Field 18).
- `Data Processing and Analysis:Time Series Analysis` — time dependence is calibration
  interpolation (contamination thickness vs. date, light-leak phase selection), not analysis of
  science time series.
- `Models and Simulations:Forward-Fitting` — `_derive_temperature` inverts the observed filter ratio
  against the model ratio by monotonic lookup plus linear interpolation; there is no optimizer or
  chi-square minimization. (`lmfit>=1.2.2` is declared in `pyproject.toml` but is **not imported
  anywhere** in the package — a stale dependency, not evidence of fitting.)
- `Models and Simulations:Empirical` — the monthly CCD/filter contamination tables are measured
  calibration inputs to a physics-based transmission model, not a standalone empirical model.
- `Servers and Environments:*` — no server, container, HPC or IaC component.

### 5. Related Region (MANDATORY)
- **Value:** Solar Environment
- **Value:** Corona
- **Source:** Live HSSI; the earlier duplicate HSSI submission carried the identical value.
  `Corona` is supported directly by `docs/about_xrt.rst:32`, which describes XRT as observing the
  solar corona at 1–10 MK; `docs/index.rst:15` and `joss/paper.md:50` independently describe
  XRTpy's coronal observations and temperature diagnostics.
- **Controlled-list spellings:** `Solar Environment` and `Corona`.
- **Settled rationale for `Corona`:** It was originally declined because `Solar Environment` was
  thought to encompass it. That premise was falsified on 2026-08-25: the Region vocabulary is flat,
  so the broad value does not imply the finer one and a `Corona` filter would otherwise miss this
  entry. The domain evidence was never in dispute, and `Corona` was added by user approval while
  retaining `Solar Environment`.
- **`Photosphere` considered and deliberately declined.** The photosphere-to-corona span in
  `docs/about_xrt.rst:17` and `joss/paper.md:50` belongs to Hinode's three instruments collectively,
  not XRTpy. Its only photosphere-capable XRT channel is G-band, which XRTpy explicitly does not
  support (`docs/getting_started.rst:203`; `docs/about_xrt.rst:67`).

### 6. Authors (MANDATORY)

**Author set: 8 authors.** Authors 7 and 8 are supported by the repository's explicit
`pyproject.toml` authorship declaration in addition to their contribution history.

**Author 1: Will Barnes**
- **Author Identifier:** https://orcid.org/0000-0001-9642-6089
- **Affiliations:**
  - American University — https://ror.org/052w4zt36
  - Department of Physics, American University — (no ROR)
  - Goddard Space Flight Center — https://ror.org/0171mag52
  - United States Naval Research Laboratory — https://ror.org/04d23a975
- **Source:** Live HSSI (4 affiliations). The 2025-10-09 canonical file had only 2 (American
  University, Goddard Space Flight Center). ROR `https://ror.org/04d23a975` supports the
  `United States Naval Research Laboratory` affiliation rather than the shorter form
  `Naval Research Laboratory`.
- **Note:** `joss/paper.md` gives the fuller form "Will T. Barnes". Not applied because the HSSI
  name is not wrong, and the fuller form is not necessary to distinguish the author.

**Author 2: Nicholas A. Murphy**
- **Author Identifier:** https://orcid.org/0000-0001-6628-8033
- **Affiliations:**
  - Center for Astrophysics Harvard & Smithsonian — https://ror.org/03c3r2d17
  - Smithsonian Astrophysical Observatory — https://ror.org/04mh52z70
  - Smithsonian Institution — https://ror.org/01pp8nd67
- **Source:** Live HSSI; matches `joss/paper.md` ("Nicholas A. Murphy", ORCID confirmed).
- **Note:** Supersedes the 2025-10-09 canonical file's "Nicholas Murphy" — live already carries the
  correct middle initial as published in JOSS. `pyproject.toml` misspells him as "Nick Murpy";
  ignored as a typo.

**Author 3: Katharine Reeves**
- **Author Identifier:** https://orcid.org/0000-0002-6903-6832
- **Affiliations:**
  - Center for Astrophysics Harvard & Smithsonian — https://ror.org/03c3r2d17
  - Smithsonian Astrophysical Observatory — https://ror.org/04mh52z70
  - Smithsonian Institution — https://ror.org/01pp8nd67
- **Source:** Live HSSI. Supersedes the 2025-10-09 canonical file, which carried DataCite's
  unnormalized "Harvard-Smithsonian Center for Astrophysics" with no ROR; live already resolves it
  to the ROR-backed `Center for Astrophysics Harvard & Smithsonian`.
- **Note:** `joss/paper.md` gives "Katharine K. Reeves". Not applied (see Author 1 note).

**Author 4: Jonathan Slavin**
- **Author Identifier:** https://orcid.org/0000-0002-7597-6935
- **Affiliation:** Center for Astrophysics Harvard & Smithsonian — https://ror.org/03c3r2d17
- **Source:** Live HSSI; DataCite concept-DOI creators agree (single affiliation).

**Author 5: Joy Velasquez**
- **Author Identifier:** https://orcid.org/0009-0005-4804-0946
- **Affiliations:**
  - Center for Astrophysics Harvard & Smithsonian — https://ror.org/03c3r2d17
  - Smithsonian Astrophysical Observatory — https://ror.org/04mh52z70
  - Smithsonian Institution — https://ror.org/01pp8nd67
- **Source:** Live HSSI; DataCite; `pyproject.toml`; PyHC registry contact.

**Author 6: Mark Weber**
- **Author Identifier:** https://orcid.org/0000-0001-7098-7064
- **Affiliations:**
  - Center for Astrophysics Harvard & Smithsonian — https://ror.org/03c3r2d17
  - Smithsonian Astrophysical Observatory — https://ror.org/04mh52z70
  - Smithsonian Institution — https://ror.org/01pp8nd67
- **Source:** Live HSSI; DataCite.

**Author 7: Nabil Freij**
- **Author Identifier:** https://orcid.org/0000-0002-6253-082X
- **Affiliations:**
  - Bay Area Environmental Research Institute — https://ror.org/024tt5x58
  - Lockheed Martin Solar and Astrophysics Laboratory — (no ROR)
  - SETI Institute — https://ror.org/02dxgk712
- **Source:** `pyproject.toml` `[project] authors` lists `Nabil Freij <nabil.freij@gmail.com>`;
  `git shortlog` at revision `0ef8e363` shows 35 commits, the 5th-largest contribution to the
  repository after identity-merging contributors who commit under multiple git configs (Joy
  Velasquez 243, Nicholas Murphy 120, Jonathan Slavin 75, Nicolas Trueba 36). HSSI records this
  ORCID with the affiliations above.
- **Note:** Not present in the Zenodo/DataCite creator list or the JOSS author list. Added under the
  union rule on the strength of `pyproject.toml` authorship plus sustained contribution.

**Author 8: Stuart J. Mumford**
- **Author Identifier:** https://orcid.org/0000-0003-4217-4642
- **Affiliations:**
  - Aperio Software Ltd. — (no ROR)
  - University of Sheffield — https://ror.org/05krs5044
- **Source:** `pyproject.toml` `[project] authors` lists `Stuart Mumford`; `git shortlog` shows 1
  commit (`Stuart Mumford <stuart@cadair.com>`).
- **Name rationale.** Retain the existing HSSI spelling **`Stuart J. Mumford`** (with middle
  initial), **not** the bare `Stuart Mumford` in `pyproject.toml`; the ORCID confirms that these
  names identify the same person. Contribution evidence is thinner than Author 7's (1 commit), but
  `pyproject.toml` `[project] authors` is an explicit authorship declaration by the maintainers, so
  the author is included.

**Considered and deliberately excluded — Nicolas Trueba** (audit trail): 36 merged commits across
five git configs at revision `0ef8e363`, more than either of Authors 7 and 8. Excluded because he is
absent from `pyproject.toml` `[project] authors`, the Zenodo/DataCite creator list, the JOSS author
list, and the README — i.e. from every citation-facing authority. Recorded so the omission reads as
a decision rather than an oversight.

### 7. Software Name (MANDATORY)
- **Value:** XRTpy: A Hinode X-Ray Telescope Python Package
- **Source:** Live HSSI; identical to the DataCite/Zenodo title. **Not** identical to the published
  JOSS article title, which hyphenates it as `XRTpy: A Hinode-X-Ray Telescope Python Package`
  (Crossref `10.21105/joss.06396`, `joss/paper.md` frontmatter) — see Field 14.
- **Note:** The earlier duplicate HSSI submission used the shorter `XRTpy`, and the distribution
  name on PyPI and in `pyproject.toml` is `xrtpy`. The full descriptive title is retained as the
  submitted editorial choice and because it matches the citable publication.

### 8. Description (MANDATORY)
- **Value (820 characters):**

> XRTpy is a modern, open-source Python package for working with data from the X-Ray Telescope (XRT) aboard the Hinode spacecraft - that observes the Sun’s atmosphere from the photosphere to the corona. The package provides a complete set of tools for modeling the XRT instrument, computing effective areas and temperature responses, calibrating images, correcting instrumental effects such as light leaks, and improving image quality. It enables scientists to estimate key physical properties of the solar corona and to analyze XRT observations within a reproducible, Python-based workflow that integrates naturally with the broader heliophysics software ecosystem. XRTpy is designed to replace and modernize legacy IDL routines, making advanced XRT data analysis more accessible and easier to maintain for the community.

- **Source:** Live HSSI (2026-curated). The wording is retained as editorial intent, including the
  U+2019 right single quotation mark in "Sun’s".
- **Supersedes:** the 2025-10-09 canonical file, which carried the 2024 Zenodo/DataCite abstract
  ("The XRTpy Python package is a specialized tool developed for the analysis of observations…").
  The stored text is newer, better organized, and accurately reflects v0.5.x scope; the older
  abstract was also the text the earlier duplicate HSSI submission carried.

### 9. Concise Description (OPTIONAL)
- **Value (188 characters):**

> XRTpy is an open-source Python package for analyzing solar X-ray data from the Hinode X-Ray Telescope, providing modern, reproducible tools for instrument modeling and coronal diagnostics.

- **Source:** Live HSSI (2026-curated). Within the 200-character limit.
- **Supersedes:** the 2025-10-09 canonical file value
  "A Python package for analyzing data from the X-Ray Telescope (XRT) on the Hinode spacecraft.",
  which was the earlier duplicate HSSI submission's stored `conciseDescription` verbatim. It is
  *not* the `pyproject.toml` `description`, which reads "For analyzing data from the X-Ray Telescope
  (XRT) on the Hinode spacecraft." without the "A Python package" prefix.

### 10. Publication Date (RECOMMENDED)
- **Value:** 2024-08-08
- **Source:** Live HSSI; DataCite `dates[].dateType = "Issued"` for the Zenodo deposit; Zenodo
  record 13157914 `publication_date`.
- **Definitional note (settled — value retained):** The form defines this as the date of first
  publication "used for the initial version of the software". XRTpy's first public release was
  **v0.1.0 on 2022-09-26** (git tag), and the repository dates to 2021. The stored 2024-08-08 is the
  Zenodo/DOI issue date for v0.4.1. Both readings are defensible; the submitted, DOI-backed value is
  retained rather than changed on interpretation alone.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** Live HSSI (existing Organization row, name `Zenodo`, identifier `https://zenodo.org`);
  DataCite `publisher = "Zenodo"`. Correct per the form guidance for a GitHub–Zenodo DOI workflow.

### 12. Version (RECOMMENDED)

The previously stored value was both malformed and stale.

- **Version Number:** `v0.5.1`
- **Version Date:** `2026-04-22`
- **Version Description:** Bug-fix release promoting `v0.5.1-pre` to a stable release. Corrects the
  temperature response filter method by removing a stray print statement and fixing logger
  placement, removes obsolete CCD contamination files, and updates the monthly CCD contamination
  data through 2026-02-22.
- **Version PID:** **Not found** — see the Zenodo determination below.

**Stored vs. rendered — do not confuse them.** The version this one replaced was stored as the
literal string **`version 0.4.1`** (a leading word, not a `v` prefix), with release date
`2024-08-08` and version PID `https://doi.org/10.5281/zenodo.13157914`. It was *displayed* as
`XRTpy: A Hinode X-Ray Telescope Python Package - version 0.4.1`, with the software name prefixed to
the stored string. **Never copy a displayed version string (or its `<softwareName> - ` prefix) back
into a stored value.** The malformed stored literal came straight from Zenodo/DataCite, whose
`version` field for record 13157914 is itself the string `version 0.4.1`.

**Release evidence:**

| Tag | Date | Commit | Status |
|---|---|---|---|
| `v0.5.2-pre` | 2026-07-22 | `0ef8e363` | pre-release — must NOT be reported as current |
| `v0.5.1` | 2026-04-22 | `8a0567ed` | **latest stable** |
| `v0.5.1-pre` | 2025-07-15 | `d7b00f9e` | pre-release |
| `v0.5.0` | 2025-04-08 | `733a259d` | superseded stable |
| `v0.4.1` | 2024-07-31 | `4bc22275` | JOSS submission release |

- PyPI `info.version` = `0.5.1`; `xrtpy-0.5.1-py3-none-any.whl` uploaded 2026-04-22T19:23:59Z.
  `0.5.1rc0` (2025-07-15) and `0.5.2rc0` (2026-07-23) are release candidates.
- GitHub release `v0.5.1` — "XRTpy v0.5.1", `prerelease: false`, published 2026-04-22T19:23:28Z.
- Repo changelog `docs/changelog/0.5.1.rst` is titled "XRTpy 0.5.1 (2026-04-22)" and lists exactly
  the three bug fixes summarized above (PRs 387, 386/385, 382/380).
- The unreleased `changelog/` fragments (`350.doc.rst`, `401.feature.rst`) belong to the
  forthcoming v0.5.2 and are excluded.

**Version PID determination — no v0.5.1 Zenodo DOI exists.** Zenodo concept record `13157913` has
exactly **one** version: record `13157914` (`version 0.4.1`, 2024-08-08), flagged
`relations.version[0].is_last = true`. DataCite lists a single `HasVersion` relation, to
`10.5281/zenodo.13157914`. Zenodo GitHub archiving evidently stopped after the v0.4.1 deposit, so
neither v0.5.0 nor v0.5.1 has a version DOI. Field 12 Version PID is therefore **Not found**, and
the concept DOI remains in Field 2.

**No Version PID is carried, and the stale one was cleared deliberately.** The replacement cleared
the stored version PID `https://doi.org/10.5281/zenodo.13157914`, because that DOI resolves to
v0.4.1 and would be factually wrong attached to v0.5.1. The v0.4.1 version DOI is still recorded in
this file's Field 2 note, and the concept DOI stays in Field 2 itself, so no identifier is lost.

### 13. Programming Language (RECOMMENDED)
- **Value:** `Python 3.x`
- **Source:** Live HSSI; the earlier duplicate HSSI submission carried the identical value;
  `pyproject.toml` `requires-python = ">=3.11"` and `Programming Language :: Python :: 3 :: Only`.
- **Controlled-list spelling:** `Python 3.x`.
- **Supported Python versions (repo detail, updated):** 3.11, 3.12, 3.13, **3.14**. Source:
  `pyproject.toml` classifiers plus the `.github/workflows/ci.yml` test matrix (3.14/Ubuntu,
  3.13/Ubuntu, 3.12/macOS with coverage, 3.11/Windows lowest-direct-dependencies). This supersedes
  the 2025-10-09 canonical file's 3.11–3.13; Python 3.14 support was added in
  `changelog/401.feature.rst`.
- **Secondary languages present in the repository (not controlled values):** two IDL `.pro` scripts
  under `IDL_scripts/IDL_test_scripts/` used solely to generate reference test data for validating
  XRTpy against SolarSoft, and BibTeX bibliography files. The 2025-10-09 canonical file listed "TeX"
  and "IDL" from SoMEF; neither is a user-facing language capability of the package, so neither is
  added as a controlled value.

### 14. Reference Publication (RECOMMENDED)
- **Value:** https://doi.org/10.21105/joss.06396
- **Citation:** Velasquez, J., Murphy, N., Reeves, K. K., Slavin, J., Weber, M., & Barnes, W.
  (2024). XRTpy: A Hinode-X-Ray Telescope Python Package. *Journal of Open Source Software*,
  9(100), 6396. https://doi.org/10.21105/joss.06396
- **Source:** Live HSSI; `docs/acknowledging_xrtpy.rst`; `docs/bibliography.bib` (`velasquez:2024`);
  README citation section. DOI resolves.

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://spdx.org/licenses/BSD-2-Clause.html
- **Source:** Live HSSI; `LICENSE` file (BSD 2-Clause, "Copyright (c) 2021-2024, XRTpy
  contributors"); `pyproject.toml` classifier `License :: OSI Approved :: BSD License`; DataCite
  `rightsIdentifier = bsd-2-clause` (SPDX).
- **Controlled-list spelling:** `BSD 2-Clause "Simplified" License`, whose live `License` row
  carries `url = https://spdx.org/licenses/BSD-2-Clause.html`. This supersedes the 2025-10-09
  canonical file's `https://opensource.org/licenses/BSD-2-Clause`, which is not the URI the
  controlled list binds to.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values:**

- `heliophysics`
- `hinode spacecraft`
- `open source software`
- `python`
- `solar physics`
- `x ray telescope (xrt)`
- `data analysis`
- `solar`
- `solar imaging`

- **Source:** Live HSSI's six derive from DataCite `subjects` (`Solar Physics`,
  `Hinode Spacecraft`, `Python`, `Heliophysics`, `open source software`,
  `X-Ray Telescope (XRT)`). The two additions come from the earlier duplicate HSSI submission and
  are independently corroborated by the PyHC community registry entry for XRTpy
  (`keywords: solar, specific, data_analysis, hinode`).
- **Normalization note:** keywords are stored lowercase and rendered Title Case (HSSI renders
  `X Ray Telescope (Xrt)`).
- **Deliberately not added:** `hinode`, `x-ray`, `xrt` (from `pyproject.toml` `keywords`) — they are
  near-duplicates of the existing `hinode spacecraft` and `x ray telescope (xrt)` and would only add
  vocabulary noise. `data_analysis` (the PyHC token form from the 2025-10-09 canonical file) is
  superseded by the live vocabulary's clean `data analysis`.
- **`solar imaging`.** `docs/index.rst` frames the package around "the world of X-ray solar
  imaging", and XRT imaging is what every XRTpy product is derived from.

### 17. Data Sources (OPTIONAL)

**Values:**

- `Observatory/Mission-specific`
- `HTTP/HTTPS Directories`
- `The Virtual Solar Observatory.`

**Controlled-list spelling:** retain the trailing period in `The Virtual Solar Observatory.`.

**Corrected 2026-07-29:** the former controlled-list value
`Other - https://xrt.cfa.harvard.edu/level1/` no longer exists in the Data Sources vocabulary and is
no longer a valid Field 17 value. Its meaning remains represented by `Observatory/Mission-specific`
together with `HTTP/HTTPS Directories`, so nothing is lost by its absence and it should not be
re-proposed.

- **`Observatory/Mission-specific`** — the CfA XRT archive is Hinode/XRT-specific. Per Field 17's
  instruction, the observatory is cross-listed in Field 32 (`Hinode`).
- **`HTTP/HTTPS Directories`.** `filename2repo_path` constructs `https://` archive
  directory URLs; `make_exposure_map` retrieves them with `astropy.utils.data.download_file`; and
  `xrtpy.util.SSW_MIRRORS` = (`https://sohoftp.nascom.nasa.gov/solarsoft/`,
  `https://hesperia.gsfc.nasa.gov/ssw/`) are HTTPS directory trees from which `deconvolve` and
  `remove_lightleak` fetch PSF and light-leak calibration files via `sunpy.data.manager`.
- **`The Virtual Solar Observatory.`.** The shipped gallery documents VSO as the
  recommended way to obtain XRT input data: `examples/sorting_data.py`,
  `examples/deconvolving.py` and `examples/temperature_from_filter_ratios.py` all query it via
  `sunpy.net.Fido.search(a.Instrument("xrt"))`, and `examples/sorting_data.py` states outright that
  it will "download a range of XRT data from the Virtual Solar Observatory (VSO)". The query
  capability itself is sunpy's — XRTpy ships no VSO client code — but Field 17 asks which data
  input sources the software *supports*, and VSO is the documented, primary route by which XRT data
  reaches XRTpy's public API.

### 18. Input File Formats (RECOMMENDED)

**Values:**

- `FITS`
- `IDL.sav`

- **`FITS`** — live HSSI and the earlier duplicate HSSI submission agreed. XRT Level 1 / Level 2
  data are read as `sunpy.map.Map` (`XRTMap`) objects; `xrtpy/util/make_exposure_map.py` uses
  `astropy.io.fits` (`fits.getheader`, `fits.getval`, `fits.open`) directly; PSF and light-leak
  calibration files are FITS.
- **`IDL.sav`.** Reading SolarSoft IDL save-format files is a defining capability, since
  XRTpy's whole design goal is reproducing the IDL routines' numbers:
  `xrtpy/response/channel.py` reads `xrt_channels_v0017.genx` via
  `sunpy.io.special.genx.read_genx`; `xrtpy/response/effective_area.py` reads
  `xrt_contam_on_ccd.sav` and `xrt_contam_on_filter.geny` via `scipy.io.readsav`;
  `xrtpy/response/temperature_response.py` reads the three CHIANTI emission models
  (`XRT_emiss_model.default_CHIANTI*.geny`) via `scipy.io.readsav`. `scipy.io.readsav` is the IDL
  SAVE-file reader, and GENX is a SolarSoft IDL save format.
- **Controlled-list spellings:** `FITS`, `IDL.sav`.
- **`ascii` — considered and deliberately excluded.** `xrtpy/response/effective_area.py`
  (`n_DEHP_attributes`) reads the plain-text table `xrtpy/response/data/n_DEHP.txt` line by line,
  but that is a small bundled constants table, not a format users can supply data in. Field 18 is
  limited to formats actually supported for data input.

### 19. Output File Formats (RECOMMENDED)
- **Value:** `FITS`
- **Source / evidence:** `make_results_maps` in `xrtpy/response/temperature_from_filter_ratio.py`
  constructs complete FITS/WCS headers for every derived product — copying and repairing `NAXIS`,
  `NAXIS1/2`, `CRPIX1/2`, `CRVAL1/2`, `CDELT1/2`, `CUNIT1/2`, `CTYPE1/2`, `CROTA1/2`, `DSUN_OBS`,
  `RSUN_REF`, `RSUN_OBS`, `SOLAR_B0`, `HGLN_OBS`, `HGLT_OBS`, and setting `BUNIT`, `L1_file1`,
  `L1_file2`, `HISTORY` and `keycomments`. `deconvolve` and `remove_lightleak` likewise append to
  `HISTORY` and return `XRTMap` objects. Every public XRTpy product is therefore a
  FITS-header-complete `sunpy.map` object that serializes to FITS via `Map.save()`.
- **Caveat (stated honestly):** XRTpy itself never calls a file writer — no `writeto`, `Map.save`,
  `savetxt` or equivalent appears anywhere in `xrtpy/`. FITS is the format of the generated
  products, produced by the caller invoking `Map.save()`. No other output format has any support.
- **Controlled-list spelling:** `FITS`.

### 20. Operating System (RECOMMENDED)

**Values:**

- `Linux`
- `Mac`
- `Windows`
- `Operating System Independent`

- **Source:** `.github/workflows/ci.yml` runs the test matrix on `ubuntu-latest`, `macos-latest` and
  `windows-latest` at every commit; `pyproject.toml` declares
  `Operating System :: OS Independent`.
- **Controlled-list correction:** the valid OS-agnostic value is `Operating System Independent`,
  not `OS Independent` as listed in the 2025-10-09 canonical file.
- **Controlled-list spellings:** `Linux`, `Mac`, `Windows`, `Operating System Independent`.

### 21. CPU Architecture (RECOMMENDED)
- **Value:** `CPU Independent`
- **Source / evidence:** XRTpy is pure Python with no compiled extensions — PyPI publishes only
  `xrtpy-0.5.1-py3-none-any.whl` (universal `py3-none-any` wheel) plus an sdist, and
  `pyproject.toml` declares no build extensions. CI additionally passes on x86-64 Linux/Windows and
  Apple Silicon macOS runners.
- **Controlled-list spelling:** `CPU Independent`.
- **Deliberately not added:** `x86-64` and `Apple Silicon arm64`, although both are CI-verified —
  `CPU Independent` already asserts the stronger, accurate claim, and listing specific architectures
  alongside it is redundant.

### 22. Related Phenomena (OPTIONAL)

**Values:**

- `Coronal Heating`
- `Solar Corona`
- `Solar Flares`
- `X-ray emission`

- The stored set was already a strict superset of the set the earlier duplicate HSSI submission
  carried, which lacked `X-ray emission`.
- **Source / evidence:** `docs/about_xrt.rst` (XRT observes the corona at 1–10 MK);
  `docs/getting_started.rst` (coronal temperature and emission measure diagnostics);
  `joss/paper.md` ("diagnosing coronal temperatures from less than 1 MK to more than 10 MK");
  the bibliography's flare and X-ray references (`Guidoni:2015`, `Fludra:1999`).
- **Considered and deliberately excluded:** `Coronal Mass Ejections`, `Geomagnetic Storms`, and
  `Solar Wind` are not XRTpy functionality. `Coronal Holes` is not an available value.

### 23. Development Status (RECOMMENDED)
- **Value:** `Active`
- **Source / evidence:** repostatus.org's `Active` = "reached a stable, usable state and is being
  actively developed". XRTpy has stable releases on PyPI (v0.5.1, 2026-04-22), a published JOSS
  paper, and continuing development at the extraction revision (`v0.5.2-pre` tagged 2026-07-22,
  Python 3.14 support added, DEM solver announced for v0.6.0 in the GitHub release notes).
- **Controlled-list spelling:** `Active`.
- **Note:** `pyproject.toml` carries the trove classifier `Development Status :: 4 - Beta`. That is a
  different taxonomy and does not map to repostatus `WIP`, which requires "no stable, usable public
  release yet" — false for XRTpy.

### 24. Documentation (RECOMMENDED)
- **Value:** https://xrtpy.readthedocs.io
- **Source:** Live HSSI; `pyproject.toml` `urls.Documentation`; README; PyHC registry `docs`. URL resolves.
- **Additional documentation entry points (context, not additional field values):**
  - Installation guide — https://xrtpy.readthedocs.io/en/latest/install.html
  - Getting started — https://xrtpy.readthedocs.io/en/latest/getting_started.html
  - Example gallery — https://xrtpy.readthedocs.io/en/latest/generated/gallery/index.html
  - Changelog — https://xrtpy.readthedocs.io/en/stable/changelog/index.html
  - Contributing guide — https://xrtpy.readthedocs.io/en/latest/contributing.html

### 25. Funder (OPTIONAL)

Both funders are corroborated by the repository.

**Funder 1:**
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80
- **Source:** `README.md` — "The development of XRTpy is supported by NASA contract **NNM07AB07C**
  to the Smithsonian Astrophysical Observatory"; `joss/paper.md` Acknowledgements, same wording.
  ROR `027ka1x80` display name is confirmed as `National Aeronautics and Space Administration`
  (acronym `NASA`); the acronym is fully expanded as the form requires.

**Funder 2:**
- **Organization:** U.S. National Science Foundation
- **Funder Identifier:** https://ror.org/021nxhr62
- **Source:** `joss/paper.md` Acknowledgements — "N.A.M. acknowledges support from NSF CSSI award
  1931388". Confirmed against NSF Award 1931388 (see Field 26), whose awardee is the Smithsonian
  Institution Astrophysical Observatory.
- **Naming note.** The ROR record's display name is `U.S. National Science Foundation`, which is
  the name recorded above. An earlier revision used `National Science Foundation`; the shared ROR
  shows that these names refer to the same entity, not separate organizations.

### 26. Award Title (OPTIONAL)

**Award 1:**
- **Award Title:** Hinode X-Ray Telescope — **curatorial display label, not an official award title.
  See the note below.**
- **Award Number:** NNM07AB07C — **this is the authoritative datum for Award 1.**
- **Funder:** National Aeronautics and Space Administration
- **Source (award number):** `README.md` Acknowledgements; `joss/paper.md` Acknowledgements. NASA
  contract to the Smithsonian Astrophysical Observatory.
- **Source (award title):** none — the title is a curatorial display label, not extracted metadata.
- **Rationale:** The award number appeared in the 2025-10-09 canonical file and remains supported
  by the README at revision `0ef8e363`. The title is a user-approved curatorial display label.

> **The Award 1 title is a curatorial display label, not extracted metadata.**
>
> - **No official NASA award title exists for `NNM07AB07C`.** Verified by web search; the number
>   appears throughout the literature only as a bare contract number.
> - **The contract is broader than XRTpy, and broader than Hinode/XRT.** NASA NTRS shows
>   `NNM07AB07C` also funding Marshall Grazing Incidence X-Ray Spectrometer (MaGIXS) sounding-rocket
>   work at the Smithsonian Astrophysical Observatory
>   (https://ntrs.nasa.gov/citations/20230017937). It is a broad NASA/MSFC–SAO contract. The label
>   therefore names **the mission this software serves**; it must not be read as describing the
>   contract's scope, and it is not a citation.
> - **Why a label exists at all.** The submission form makes Award Title OPTIONAL and Award Number
>   RECOMMENDED, but HSSI cannot store an award without a title. Without a label this award could not
>   be recorded at all.
> - **Precedent.** HSSI already labels title-less awards by the mission served rather than by the
>   contract's legal scope — `MMS` / `NNG04EB99C` and `THEMIS` / `NAS5-02099`. The award name serves
>   as a display label; the award number is the authoritative value.

**Award 2:**
- **Award Title:** Collaborative Research: Frameworks: An open source software ecosystem for plasma physics
- **Award Number:** 1931388
- **Funder:** U.S. National Science Foundation
- **Identification note:** three sibling awards share this title under different numbers
  (1931393 / 1931429 / 1931435), so award number 1931388 must accompany the title.
- **Source:** `joss/paper.md` Acknowledgements gives the award number; the title is resolved from
  the NSF award record for ID 1931388 (Directorate for Computer &
  Information Science & Engineering / Office of Advanced Cyberinfrastructure; awardee "Smithsonian
  Institution Astrophysical Observatory"; 2019-10-01 to 2025-09-30). This is the PlasmaPy CSSI award
  that supports N. A. Murphy. The 2025-10-09 canonical file recorded the number with
  "Award Title: Not found"; that gap is now closed.

**Per-award funder attribution, and where it can and cannot be read.** The pairings are
NASA ↔ `NNM07AB07C` and U.S. National Science Foundation ↔ `1931388`, each stated in the
Acknowledgements sources cited above. HSSI stores the two organizations and the two awards as flat
lists without a per-award funder relationship, so the pairings are recorded here for future use.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

Entries 1–4 were present in the 2025-10-09 canonical file; entries 5–8 extend that set. Every DOI
below resolves to the stated article via Crossref.

These are the instrument, mission, calibration and atomic-physics papers that XRTpy directly
implements or cites as the basis of its computations — they are distinct from the Field 14 reference
publication (the JOSS paper), which is not repeated here.

1. **Golub, L. et al. (2007).** The X-Ray Telescope (XRT) for the Hinode Mission. *Solar Physics*,
   243(1), 63–86. https://doi.org/10.1007/s11207-007-0182-1
   *Evidence:* the XRT instrument paper; cited in `docs/index.rst` (`golub:2007`) and `joss/paper.md`.
2. **Kosugi, T. et al. (2007).** The Hinode (Solar-B) Mission: An Overview. *Solar Physics*, 243(1),
   3–17. https://doi.org/10.1007/s11207-007-9014-6
   *Evidence:* the Hinode mission paper; cited in `docs/index.rst` (`kosugi:2007`) and `joss/paper.md`.
3. **Narukage, N. et al. (2011).** Coronal-Temperature-Diagnostic Capability of the Hinode/X-Ray
   Telescope. *Solar Physics*, 269(1), 169–236. https://doi.org/10.1007/s11207-010-9685-2
   *Evidence:* the emission model behind XRTpy's temperature response; cited in
   `docs/getting_started.rst` (`narukage:2011`).
4. **Narukage, N. et al. (2014).** Coronal-Temperature-Diagnostic Capability of the Hinode/X-Ray
   Telescope Based on Self-consistent Calibration. II. *Solar Physics*, 289(3), 1029–1042.
   https://doi.org/10.1007/s11207-013-0368-7
   *Evidence:* cited in `docs/getting_started.rst` (`narukage:2014`).
5. **Takeda, A., Yoshimura, K., & Saar, S. H. (2016).** The Hinode/XRT Full-Sun Image Corrections
   and the Improved Synoptic Composite Image Archive. *Solar Physics*, 291, 317–333.
   https://doi.org/10.1007/s11207-015-0823-8
   *Evidence:* Cited directly in the code — `xrtpy/image_correction/remove_lightleak.py`
   docstring cites `Takeda:2016`, p. 317 as the basis of the light-leak correction.
6. **Feldman, U. (1992).** Elemental abundances in the upper solar atmosphere. *Physica Scripta*,
   46(3), 202–220. https://doi.org/10.1088/0031-8949/46/3/002
   *Evidence:* XRTpy's default CHIANTI **coronal** abundance model; cited twice in
   `docs/getting_started.rst` (`feldman:1992`).
7. **Grevesse, N., Asplund, M., & Sauval, A. J. (2007).** The Solar Chemical Composition.
   *Space Science Reviews*, 130(1–4), 105–114. https://doi.org/10.1007/s11214-007-9173-7
   *Evidence:* Basis of XRTpy's `"photospheric"` abundance option; cited in
   `docs/getting_started.rst` (`Grevesse:2007`).
8. **Dere, K. P. et al. (1997).** CHIANTI — an atomic database for emission lines.
   *Astronomy and Astrophysics Supplement Series*, 125, 149–173. https://doi.org/10.1051/aas:1997368
   *Evidence:* The atomic database underpinning every temperature response computation
   (`xrtpy/response/data/chianti_emission_models/`, CHIANTI v10.0); cited in `joss/paper.md`.

**Considered and deliberately excluded** (both lack a DOI in any primary repository source, which
Field 27 asks for; recorded so the omissions read as decisions):
- **Fludra, A. & Schmelz, J. T. (1999).** The absolute coronal abundances of sulfur, calcium, and
  iron from Yohkoh-BCS flare spectra. *Astronomy & Astrophysics*, 348, 286–294. Basis of XRTpy's
  `"hybrid"` abundance option (`docs/getting_started.rst`), but **no DOI exists** for this article
  in either repository bibliography; it would have to be entered as an APA citation with the ADS
  permanent link https://ui.adsabs.harvard.edu/abs/1999A&A...348..286F.
- **Del Zanna, G. et al. (2021).** CHIANTI — An Atomic Database for Emission Lines. XVI. Version 10.
  *The Astrophysical Journal*, 909, 38. https://doi.org/10.3847/1538-4357/abd8ce. This is the exact
  CHIANTI version XRTpy uses, cited as `DelZanna:2020` in `joss/paper.bib` — but **with no DOI in
  the repository**, so the DOI above was resolved externally rather than from a primary repo source.

**Data-quality finding (repository bug, not propagated):** `docs/bibliography.bib` gives
`Guidoni:2015` the DOI `10.1007/s11214-007-9173-7`, which actually belongs to `Grevesse:2007`.
`joss/paper.bib` has the correct value `10.1088/0004-637X/800/1/54`. The erroneous DOI was not
carried into this file. Guidoni et al. (2015) is otherwise only the source of the example dataset in
JOSS Figure 3, so it is not proposed for Field 27.

### 28. Related Datasets (OPTIONAL)

**No DOI exists for Hinode/XRT data
products** — neither the CfA XRT archive, DARTS, nor SPASE publishes a dataset DOI for XRT Level 1
or Level 2 Synoptics. The form explicitly permits an APA citation with a permanent link in that
case, so both entries below are asserted in citation-with-link form. They identify the exact archive
products XRTpy is built to read.

1. Smithsonian Astrophysical Observatory. *Hinode/X-Ray Telescope (XRT) Level 1 Data* [Data set].
   https://xrt.cfa.harvard.edu/level1/
   *Evidence:* `xrtpy/util/filename2repo_path.py` resolves `L1_XRT*.fits` and `L1_XRT*.qual.fits`
   filenames to `level1/` and `data_products/Level1_Qual/` on this archive;
   `temperature_from_filter_ratio` is documented throughout as operating on "XRT level 1 data
   image" maps; `docs/getting_started.rst` "Data Products" names Level 1 data explicitly.
2. Smithsonian Astrophysical Observatory. *Hinode/X-Ray Telescope (XRT) Level 2 Synoptic Composite
   Images* [Data set]. https://xrt.cfa.harvard.edu/data_products/Level2_Synoptics/
   *Evidence:* `filename2repo_path` resolves `comp_XRT*` composites to
   `data_products/Level2_Synoptics/` and grade maps to `data_products/Level2_gmap/`;
   `remove_lightleak` operates specifically on "XRT synoptic composite images";
   `make_exposure_map` builds exposure maps from composite image headers
   (`SRTFNAME`/`MEDFNAME`/`LNGFNAME`); `docs/getting_started.rst` "Data Products" names Level 2
   Synoptics explicitly.

- **Note:** both entries use citation-with-permanent-link form because no DOI is available for XRT
  data — not because a DOI was overlooked.
- **CHIANTI atomic database v10.0 — considered and deliberately excluded**
  (https://www.chiantidatabase.org/). XRTpy ships it as derived `.geny` emission-model files, but it
  is reference data consumed internally rather than a dataset users analyze *with* XRTpy, and it is
  already represented by the two CHIANTI publications in Field 27.

### 29. Related Software (OPTIONAL)

**Values:**

- sunpy — https://doi.org/10.5281/zenodo.591887
- SolarSoft — https://www.lmsal.com/solarsoft/

- **sunpy — https://doi.org/10.5281/zenodo.591887**
  - **Concept DOI confirmed:** Zenodo reports `conceptdoi = 10.5281/zenodo.591887` /
    `conceptrecid = 591887`, currently resolving to
    "sunpy: A Core Package for Solar Physics" v8.0.0 (2026-06-30). Already the concept DOI, so no
    version-to-concept correction is needed.
  - **Relevance:** passes the Field 29 gate as the **domain-specific framework XRTpy is built on**,
    not as a generic dependency. `pyproject.toml` requires `sunpy[map]>=5.1`; XRTpy's entire public
    API is expressed in sunpy types (`sunpy.map.sources.hinode.XRTMap`), and it uses
    `sunpy.io.special.genx`, `sunpy.data.manager`, `sunpy.image.resample`,
    `sunpy.image.transform`, `sunpy.time` and `sunpy.coordinates.sun`. `joss/paper.md`: "building on
    the SunPy framework, XRTpy effectively utilizes the `Map` object for handling Hinode/XRT image
    data."

- **SolarSoft (the SolarSoft XRT IDL analysis routines) — https://www.lmsal.com/solarsoft/**
  - **Relevance:** SolarSoft is XRTpy's direct **predecessor**, and replacing it is the package's
    stated reason for existing. The live description says XRTpy "is designed to replace and modernize
    legacy IDL routines"; `joss/paper.md` says XRTpy "has been carefully written to ensure the
    consistency and replication of results obtained from the official IDL routines as described in
    the SolarSoft XRT Analysis Guide", and names the guide as "the official software and instrument
    guide for XRT data analysis". The coupling is concrete, not rhetorical: XRTpy downloads SSW
    calibration products (`PSF560.fits`, `PSF1000.fits`, the `term_p*.fits` light-leak images) from
    the SolarSoft mirrors in `xrtpy.util.SSW_MIRRORS`, reads SolarSoft GENX/`.geny` instrument files,
    and `IDL_scripts/IDL_test_scripts/*.pro` generate the IDL reference outputs its test suite
    validates against. This is exactly the "software that performs similar tasks" and "the project
    this was forked from / predecessor" case Field 29 exists for.
  - **Identifier basis — third tier.** SolarSoft has **no DOI** and **no browsable public git
    repository** (it is distributed by rsync and from the project website; the only public git
    repositories are third-party projects that *use* SSW routines), and it has **no existing HSSI
    entry** to point at. Field 29's fill instructions are a three-tier fallback: the DOI for the
    software code, *otherwise* a link to the code repository, *otherwise* **a link where users can
    find more information**. `https://www.lmsal.com/solarsoft/` is asserted under that third tier as
    the distribution root — the closest available analogue to a code-repository link. This is the
    same citation-with-permanent-link logic applied to the sibling Field 28, where no DOI exists
    either.
  - **Supporting evidence link:** the SolarSoft XRT Analysis Guide,
    https://xrt.cfa.harvard.edu/resources/documents/XAG/XAG.pdf — the instrument/software guide
    whose results XRTpy reproduces. Recorded as evidence, not as a second Field 29 value (it is a
    document, not software).

**Excluded under the relevance gate (audit trail).** The 2025-10-09 canonical file listed the raw
dependency block here; those entries are dropped:
- **Tier A, always excluded:** `numpy>=1.24`, `scipy>=1.11.1`, `matplotlib>=3.7`,
  `scikit-image>=0.21`, `setuptools`, `setuptools-scm`, `wheel`, `pytest`/`pytest-astropy`/
  `pytest-cov`/`pytest-xdist`, `nox`, `sphinx` and its extensions. These are generic scientific-Python
  and tooling infrastructure — equally at home in a web app, a finance model or a biology pipeline —
  and being a dependency is not a relationship worth recording.
- **`astropy>=6` (Tier B) — excluded.** Pervasively used (units, constants, `astropy.io.fits`,
  `astropy.time`, `astropy.utils.data`) but as internal infrastructure; there is no documented
  XRTpy↔astropy *exchange* beyond returning `Quantity`-typed values, which is true of most of the
  astronomy stack.
- **`lmfit>=1.2.2` — excluded.** Declared in `pyproject.toml` but **imported nowhere** in the
  repository; a stale dependency.

### 30. Interoperable Software (OPTIONAL)

**Values:**

- EISPAC — https://doi.org/10.5281/zenodo.7949515
- aiapy — https://doi.org/10.5281/zenodo.10064346
- irispy — https://doi.org/10.5281/zenodo.10443678
- sunpy — https://doi.org/10.5281/zenodo.591887

1. **EISPAC — https://doi.org/10.5281/zenodo.7949515** — **Concept DOI confirmed:**
   `conceptdoi = 10.5281/zenodo.7949515` / `conceptrecid = 7949515`, currently
   resolving to "EISPAC — The EIS Python Analysis Code" v0.99.4 (2026-06-02). (The seed context
   labelled this "EISPAC v0.99.4"; it is in fact the concept DOI, which merely resolves to the
   latest version.) **Relevance:** `joss/paper.md` names an explicit, ongoing interoperability
   collaboration with the EISPAC developers for combined XRT + Hinode/EIS analysis — a named
   heliophysics peer tool, not a dependency.
2. **aiapy — https://doi.org/10.5281/zenodo.10064346** — **Concept DOI confirmed:**
   `conceptdoi = 10.5281/zenodo.10064346` / `conceptrecid = 10064346`, currently
   resolving to `LM-SAL/aiapy` v0.12.1 (2026-06-25). **Relevance:** `joss/paper.md` names the aiapy
   developers as interoperability collaborators for combined XRT + SDO/AIA analysis; the two
   packages are structural analogues (instrument response and calibration built on the same sunpy
   `Map` model) and share the author Will Barnes.
3. **irispy — https://doi.org/10.5281/zenodo.10443678.** The value this replaced,
   `https://doi.org/10.5281/zenodo.16989847`, was a **version** DOI: Zenodo record 16989847 is
   `LM-SAL/irispy: v0.4.0` (2025-08-28), whose `conceptdoi` is `10.5281/zenodo.10443678`. The concept
   DOI currently resolves to v0.7.0 (2026-05-07). Recording the concept DOI rather than that version
   DOI keeps the link valid as irispy releases and is what the "prefer concept DOIs" rule requires.
   **Relevance:** `joss/paper.md` names irispy-lmsal (now `LM-SAL/irispy`) as an interoperability
   collaborator for combined XRT + IRIS analysis.
4. **sunpy — https://doi.org/10.5281/zenodo.591887.** Concept DOI, also documented under
   Field 29. sunpy satisfies Field 30's *demonstrated exchange* bar in the strongest possible form:
   XRTpy's public API both **accepts and returns** sunpy's data model.
   `temperature_from_filter_ratio(map1, map2)` is documented to take
   `~sunpy.map.sources.hinode.XRTMap` inputs and return a namedtuple of four `XRTMap` objects;
   `deconvolve(image_map)` and `remove_lightleak(in_map)` take and return `XRTMap`;
   `make_results_maps` constructs sunpy `Map` objects with full WCS headers. This bidirectional
   exchange of a shared data model is directly analogous to the worked example
   "sunpy ↔ ndcube (shared NDCube data model)". It is deliberately listed in **both** Field 29 (as
   the domain framework XRTpy is built on) and Field 30 (as a demonstrated interoperation); the two
   roles are distinct and both are true.

**Excluded under the relevance gate (audit trail).** The 2025-10-09 canonical file's Field 30
overlapped its dependency list; corrected here. Same Tier A / Tier B exclusions as Field 29 apply —
numpy, scipy, matplotlib, scikit-image and astropy are not listed. Note especially that
"XRTpy is a PyHC community package, so it interoperates with PyHC packages" is **not** used as
justification anywhere above; each of the four entries rests on a specific, cited exchange or a
named collaboration in the JOSS paper.

**Standing caveat from the primary source:** `joss/paper.md` states "interoperability with other
packages is a work in progress that we've started with the developers of aiapy…, EISpack…, and
irispy-lmsal". These are declared, in-progress collaborations rather than shipped adapter APIs; the
sunpy exchange (entry 4) is the only one demonstrated in XRTpy's own code.

### 31. Related Instruments (OPTIONAL)

- **Instrument Name:** `X-Ray Telescope`
- **Instrument Identifier:** `https://spase-metadata.org/SMWG/Instrument/Hinode/XRT`
- **Relevance gate:** passes decisively. XRTpy is purpose-built by the XRT instrument team to read,
  calibrate, model and analyze Hinode/XRT data specifically — instrument name in the software title,
  XRT channel/filter/CCD models, XRT effective area and temperature response, XRT PSF deconvolution,
  XRT light-leak correction, XRT archive path resolution.
- **SPASE resolution:** exactly **one** vocabulary entry represents this SPASE
  resource — name `X-Ray Telescope`, identifier `https://spase-metadata.org/SMWG/Instrument/Hinode/XRT`.
  The canonical label is the bare `X-Ray Telescope`, never `X-Ray Telescope (XRT)`.
- **Bare identifier adopted; the earlier decision declining it is superseded.** The vocabulary once
  held **three** distinct entries for this one SPASE resource — `X-Ray Telescope` under the bare
  identifier, and both `Hinode X-ray Telescope` (formerly stored on this entry) and
  `X-Ray Telescope (XRT)` under `.../SMWG/Instrument/Hinode/XRT.html`. Because HSSI distinguishes
  instruments by identifier alone, that duplicated `.html` identifier did not determine which of its
  two labels an entry resolved to. HSSI's instrument/observatory vocabulary has since been
  consolidated onto the identifiers registered in the maintained upstream vocabulary
  (api.heliophysics.net), in which **no `.html` identifier exists at all**: the `.html` forms were
  copy-paste artifacts of SPASE landing-page URLs created by the submission path, and the bare
  identifier is the maintained form. Exactly one row per canonical identifier now exists, so both the
  duplication and the label ambiguity are gone, and the labels `Hinode X-ray Telescope` and
  `X-Ray Telescope (XRT)` no longer exist as separate entries. An earlier revision of this file
  declined bare normalization on the premise that HSSI showed no convention favouring bare over
  `.html` and that "many entries deliberately use `.html`"; that decision was taken without comparing
  HSSI's vocabulary against the maintained upstream one, and the comparison falsifies its premise.
  The bare identifier recorded above is the correct value, and
  `https://spase-metadata.org/SMWG/Instrument/Hinode/XRT.html` should not be re-proposed.
- **Correction vs. the 2025-10-09 canonical file:** that file recorded
  `Instrument Name: X-Ray Telescope (XRT)` with `Instrument Identifier: Not found`. Both are
  superseded — the identifier exists, and the bare name `X-Ray Telescope (XRT)` would resolve to the
  *other* vocabulary entry, not this one's.
- **Considered and excluded under the relevance gate** (`Note:` for the audit trail):
  - `Hinode/EIS` (`.../SMWG/Instrument/Hinode/EIS`) and `Hinode/SOT`
    (`.../SMWG/Instrument/Hinode/SOT`) — named in `docs/about_xrt.rst` only as Hinode's other two
    instruments, and EIS appears via EISPAC *interoperability*. XRTpy reads neither instrument's data.
  - `SDO/AIA` and `IRIS` — aiapy / irispy interoperability context only (Field 30).
  - `Yohkoh/SXT` (`.../SMWG/Instrument/Yohkoh/SXT`) and `Yohkoh/HXT` — Yohkoh appears only as the
    heritage comparison in the SPASE Hinode description and, indirectly, as the source of the
    Yohkoh-BCS spectra behind the `Fludra:1999` hybrid abundance model. XRTpy does not support
    Yohkoh data.
  - FITS and the IDL GENX/`.sav` formats → Fields 18/19, not here (they are multi-instrument or
    generic formats).

### 32. Related Observatories (OPTIONAL)

- **Observatory Name:** `Hinode`
- **Observatory Identifier:** `https://spase-metadata.org/SMWG/Observatory/Hinode`
- **Source:** Earlier HSSI metadata for this software, confirmed against SPASE.
- **SPASE resolution:** exactly **one** matching vocabulary entry, name
  `Hinode`, identifier `https://spase-metadata.org/SMWG/Observatory/Hinode`. There is **no `.html`
  twin** and no same-name duplicate, unlike Field 31's since-resolved pre-consolidation state. The
  SPASE record itself confirms `ResourceID = spase://SMWG/Observatory/Hinode`,
  `ResourceName = Hinode`.
- **Relevance gate:** passes. XRTpy works exclusively with Hinode mission data products, reads the
  mission's own CfA archive (Field 17/28), and implements Hinode/XRT data conventions. Cross-listed
  with `Observatory/Mission-specific` in Field 17 as Field 17 instructs.
- **Considered and excluded** (`Note:` for the audit trail): `Solar Dynamics Observatory`, `IRIS`
  and `Yohkoh` — all present in the controlled list, all excluded because they appear only as
  interoperability or heritage context, never as data XRTpy reads.

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/HinodeXRT/xrtpy/main/docs/_static/images/XRTpy_logo.png
- **Source:** Live HSSI; `README.md` header image (`docs/_static/images/XRTpy_logo.png`);
  `docs/index.rst`; also configured as the gallery `default_thumb_file` in `docs/conf.py` at exactly
  this raw URL. Verified to resolve.
- **Provenance correction:** the 2025-10-09 canonical file claimed the logo was "Listed in PyHC
  registry as well". The PyHC community-registry entry for XRTpy has **no `logo` field**; the URL
  comes from the repository, not PyHC.

---

## Supporting Context

### PyHC registry status
XRTpy is a **PyHC community package**, found in `_data/projects.yml` (not core, not unevaluated).
Registry entry: name `XRTpy`; description "A Python package for analyzing data from the X-Ray
Telescope instrument onboard the Hinode spacecraft."; docs `https://xrtpy.readthedocs.io`; code
`https://github.com/HinodeXRT/xrtpy`; contact Joy Velasquez; keywords `solar`, `specific`,
`data_analysis`, `hinode`. Quality ratings: community, documentation, testing and software maturity
"Partially met"; Python 3 and license "Good". `joss/paper.md` also thanks "the Python in
Heliophysics Community at large".

### Contact points
- General contact: XRTpy@cfa.harvard.edu (README)
- Issue tracker: https://github.com/HinodeXRT/xrtpy/issues
- Primary contact / PyHC registry contact: Joy Velasquez

### Release history (context for Field 12)
First public release v0.1.0 (2022-09-26); v0.4.0 (2023-12-05); v0.4.1 (2024-07-31, the JOSS
submission release and the only Zenodo deposit); v0.5.0 (2025-04-08); v0.5.1 (2026-04-22, current
stable); v0.5.2-pre (2026-07-22, pre-release at the extraction revision). The GitHub release notes
for both v0.5.1 and v0.5.2-pre announce that v0.6.0 will add a DEM solver.
