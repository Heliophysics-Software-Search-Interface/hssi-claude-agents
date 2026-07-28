# HSSI Metadata Extraction Results

**HSSI Software ID:** ec808735-972e-41e7-8549-a96d93881e26
**Repository:** https://github.com/punch-mission/regularizepsf
**Source Revision:** 8bd926e16460cc8af127c05469606df230c100ce
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-07-28
**Validation Status:** PASS

**Seed sources:** live HSSI record (`GET http://localhost/api/view/software/ec808735-972e-41e7-8549-a96d93881e26/`,
captured 2026-07-28) + prior canonical `hssi_metadata.md` (extracted 2025-10-14, stale at version 1.1.0).
Live HSSI is the authoritative baseline on conflict; supported prior-file values are retained by
identity-aware union and every non-carried prior-file value is documented in a `Note:` so nothing is
silently dropped.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Source:** Placeholder. This is an update to an existing HSSI record; the original submitter is not
exposed by the view API.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.7392170

**Source:** PRESERVED from live HSSI. Independently confirmed as the *concept* DOI by the Zenodo API
(`GET https://zenodo.org/api/records/7392170` → `"conceptdoi": "10.5281/zenodo.7392170"`,
`"conceptrecid": "7392170"`) and by CITATION.cff (`doi: 10.5281/zenodo.7392170`).

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/punch-mission/regularizepsf

**Source:** PRESERVED from live HSSI. Confirmed by CITATION.cff (`url:`), Zenodo
`metadata.custom["code:codeRepository"]`, SoMEF (`code_repository`), and the PyHC registry `code` field.

### 4. Software Functionality (MANDATORY)
**Values (10):**
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Processing  *(NEW)*
- Data Visualization
- Data Visualization:2D Graphics
- Models and Simulations  *(NEW)*
- Models and Simulations:Instrument Response  *(NEW)*
- Models and Simulations:Observatory/Instrument Models  *(NEW)*

Every `Parent:Child` value has its bare parent category present (Data Processing and Analysis,
Data Visualization, Models and Simulations).

**Vocabulary form:** HSSI's view API renders these with a space after the colon
("Data Processing and Analysis: Calibration"); the HSSI `FunctionCategory` table stores the child name
bare with a parent link. The values above use the submission form's canonical `Parent:Child` spelling.
The six values already on the live record are therefore **unchanged**: Data Visualization;
Data Processing and Analysis; Data Processing and Analysis: Calibration; Data Visualization: 2D Graphics;
Data Processing and Analysis: Analysis; Data Processing and Analysis: Image Processing.

**Source / evidence (repository code at 8bd926e1):**
- *Data Processing and Analysis* + *:Analysis* — the package's core scientific work: `regularizepsf/psf.py`
  (`ArrayPSF`, FFT evaluation of PSF models), `regularizepsf/transform.py`
  (`regularized_reciprocal()`, `ArrayPSFTransform.construct()` computing transfer kernels from a source and
  target PSF), `regularizepsf/util.py` (`calculate_covering()` overlapping-patch geometry).
- *:Calibration* — PSF regularization is an image-calibration step: `ArrayPSFTransform.apply()` corrects an
  observed image to a homogeneous target PSF, with saturated-pixel handling
  (`saturation_threshold`, `saturation_dilation`, `neighborhood_width`) and a `normalization_coefficient`.
  Downstream, `punchbowl` (PUNCH's "science calibration code") calls exactly this API.
- *:Image Processing* — `regularizepsf/image_processing.py`: `sep.Background`/`sep.extract` star detection,
  planar background fitting (`calculate_background()` via `scipy.linalg.lstsq`), sub-pixel `scipy.ndimage.shift`,
  `RectBivariateSpline` interpolation/upscaling, `binary_erosion`/`binary_dilation`/`label` morphology,
  `skimage.transform.downscale_local_mean`, image masking and square-root decompression.
- *:Processing* — `ArrayPSFBuilder.build()` is a multi-stage processing pipeline
  (`regularizepsf/builder.py`): multiprocessing `Pool.map(process_single_image, …)` over an image
  generator, patch extraction, per-patch normalization, mean/median/percentile patch averaging
  (`_average_patches*`), NaN handling, core masking and renormalization.
- *Data Visualization* + *:2D Graphics* — `regularizepsf/visualize.py`: `visualize_grid()` builds a
  `GridSpec` mosaic of `imshow` panels with a shared colorbar and a custom `ListedColormap`;
  `visualize_patch_counts()` renders a 2D star-count map; `ArrayPSF.visualize_psfs()`,
  `ArrayPSF.visualize_ffts()` and `ArrayPSFTransform.visualize()` expose these publicly. All output is
  2D raster imagery — there are no line plots, 3D, movie, or web-based renderers in the package.
- *Models and Simulations* + *:Instrument Response* — the package's other half is **modeling an
  instrument's optical response**. `simple_functional_psf` / `varied_functional_psf` (exported in
  `__init__.py`) let a user declare an analytic PSF model, optionally varying across the field of view,
  and `as_array_psf()` evaluates it onto a coordinate grid; `ArrayPSFBuilder` derives a spatially varying
  PSF model from observed starfields. `ArrayPSFTransform.apply()` can also be run *forward* to
  synthetically observe an image through a PSF — the documented example
  (`docs/source/example.ipynb`) does precisely this and labels the panel "Synthetic observation", as does
  the README figure. The `software-functionality` skill lists "PSF simulation" under
  Models and Simulations:Instrument Response.

- *Models and Simulations:Observatory/Instrument Models* — ADDED on validator recommendation (S1). The
  taxonomy's indicator for this value is "synthetic observations", and `docs/source/example.ipynb` labels
  the forward `ArrayPSFTransform.apply()` output panel exactly that ("Synthetic observation", notebook
  cells at lines 243/288/336), as does the README figure. It sits alongside :Instrument Response rather
  than replacing it: :Instrument Response covers *characterizing/modeling* the PSF
  (`simple_functional_psf`, `varied_functional_psf`, `ArrayPSFBuilder`), while
  Observatory/Instrument Models covers *producing synthetic observations* through that model. The parent
  Models and Simulations is already present.

**Note (considered and excluded, with reasons):**
- *Models and Simulations:Empirical* / *:Data Guided* — the array PSF model is data-derived, but these
  taxonomy entries target empirical/climatological geophysical models and observation-driven simulations
  respectively, not instrument characterization. Flagged as defensible alternates if a curator prefers them.
- *Data Processing and Analysis:File Format Conversion* — `save()`/`load()` support both `.h5` and `.fits`,
  so a user *can* round-trip a model between formats, but format conversion is not an advertised capability.
- *Data Processing and Analysis:Data Reduction* — patch averaging/downsampling is internal to model
  building, not a user-facing data-volume-reduction feature.
- *Mission-related* (and *:Calibration*) — regularizePSF was developed by the PUNCH SOC, but it is a
  standalone, instrument-agnostic library ("PSF regularization does not require access to the instrument
  that obtained the data" — reference publication abstract). The PUNCH ground-system component that
  consumes it is `punchbowl`, not this package.
- *Servers and Environments:High Performance Computing* — `multiprocessing.Pool` and `scipy.fft(workers=…)`
  are parallelism inside a library, not HPC infrastructure software.
- *Coordinate Transforms* (any) — the "coordinates" in this package are image pixel-patch corners
  (`IndexedCube`), not physical/celestial reference frames.

### 5. Related Region (MANDATORY)
**Value:** Solar Environment

**Source:** PRESERVED from live HSSI. Supported by `docs/source/index.rst` ("It was originally developed
for the `PUNCH`_ mission"), the PUNCH SOC copyright in LICENSE, and PUNCH's coronal/solar-wind imaging
science.

**Note (candidate for curator decision, not applied):** *Interplanetary Space* is arguably also in scope —
PUNCH is the "Polarimeter to Unify the Corona **and Heliosphere**" and its Wide Field Imagers observe the
solar wind well out into the inner heliosphere, and regularizePSF is the PSF-correction tool for that
imagery. It was not added because the software itself is instrument- and region-agnostic and the existing
single-region value is the curated live value; add it only on explicit approval.

### 6. Authors (MANDATORY)

**Author 1:**
- **Author Name:** J. Marcus Hughes
- **Author Identifier:** https://orcid.org/0000-0003-3410-7650
- **Affiliation:** Southwest Research Institute
- **Affiliation Identifier:** https://ror.org/03tghng59

**Author 2:**
- **Author Name:** Sam Van Kooten  (given name "Sam", family name "Van Kooten")
- **Author Identifier:** https://orcid.org/0000-0002-4472-8517
- **Affiliation:** Southwest Research Institute
- **Affiliation Identifier:** https://ror.org/03tghng59

**Author 3:**
- **Author Name:** Tania Varesano
- **Author Identifier:** https://orcid.org/0000-0003-0256-9295
- **Affiliation:** Not found

**Author 4:**
- **Author Name:** Suman Chapai
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 5:**
- **Author Name:** Craig DeForest
- **Author Identifier:** https://orcid.org/0000-0002-7164-2786
- **Affiliation:** Southwest Research Institute
- **Affiliation Identifier:** https://ror.org/03tghng59

**Author 6:**
- **Author Name:** Daniel Seaton
- **Author Identifier:** https://orcid.org/0000-0002-0494-2025
- **Affiliation:** Southwest Research Institute
- **Affiliation Identifier:** https://ror.org/03tghng59

**Source:** Identity-aware union of live HSSI (matched by ORCID) and CITATION.cff at 8bd926e1; the two
sources agree on the same six people and the same six ORCID assignments. Affiliations
(Organization UUID `7d4f0f58-8d42-4a8d-a6bb-94821a2079f3` = Southwest Research Institute,
ROR https://ror.org/03tghng59 confirmed via the ROR API) are PRESERVED from live HSSI; the prior canonical
file had "Not found" for every affiliation, so live wins. Author order follows CITATION.cff (credit order);
the live record displays them alphabetically by family name — order carries no semantics for this M2M field.
DataCite/Zenodo creators for the concept DOI list exactly these six, so no author is *added* here.

**NAME SPLIT — CORRECTED IN THE DATABASE 2026-07-28.** Live HSSI previously stored Sam Van Kooten as
`givenName: "Sam Van"` / `familyName: "Kooten"`, contradicting CITATION.cff (`given-names: "Sam"`,
`family-names: "Van Kooten"`), the DataCite record for 10.5281/zenodo.7392170
(`"givenName": "Sam", "familyName": "Van Kooten"`), and ORCID 0000-0002-4472-8517 (family name
"Van Kooten"). The HSSI API cannot rename an existing `Person` — PATCH matches by identifier and will not
overwrite a nonblank name, so a rename silently no-ops. The defect was therefore fixed by a direct,
user-approved `UPDATE` on `website_person` row `5543956f-39bf-41cf-8fe6-4ab41d39ee7b` in the active Django
database (`postgres` @ container `website_db`, used by app container `HSSI`): `given_name` `'Sam Van'` →
`'Sam'`, `family_name` `'Kooten'` → `'Van Kooten'`. Exactly one row was affected; the primary key was not
touched, so all four referencing associations were preserved (`website_software_authors` = 4,
`website_person_affiliation` = 1, curator = 0, submitter = 0) and the table still holds 858 rows.
Because `Person` is a shared entity, the correction also fixed the same wrong split on **ndcube**,
**punchbowl**, and **SunPy**, each of which now reports `givenName: "Sam"` / `familyName: "Van Kooten"` with
its affiliation intact. Pre-change backups: `/tmp/regularizepsf-refresh/backups/`
(`hssi_postgres_pre_vankooten_20260728.dump`, `person_5543956f_before.csv`,
`person_5543956f_refs_before.csv`). No seed CSV was edited — this correction is to be captured by the later
export/reconciliation workflow.

**UNCREDITED CONTRIBUTOR — upstream gap, deliberately not added (validator finding W1):** `Chris Lowder`
has **16 commits** in this repository touching `regularizepsf/builder.py`, `image_processing.py`,
`transform.py`, `exceptions.py`, and the changelog fragments `changelog/247.feature.rst` and
`changelog/249.feature.rst`. These are core, currently-shipping features — the v1.1.1 changelog entries
"Adds debug mode to psf build function" (PR #247) and "Adds support for multiprocessing in PSF generation
and patch cleanup changes" (PR #249) are this contributor's work, as are PSF patch cleanup, boundary
filtering, central-star-intensity filtering, and the square-root decompression toggle. Chris Lowder appears
in **none** of CITATION.cff, the DataCite/Zenodo creator list for the concept DOI, the live HSSI record, or
any other file in the repository (a case-insensitive grep for "lowder" across `.rst`/`.cff`/`.toml`/`.md`/
`.json` returns nothing), and no ORCID or affiliation is discoverable. HSSI Field 6 mirrors the project's
own citation metadata, so this name is **not** added unilaterally: doing so would create an unverifiable
`Person` row that the update API cannot later rename or correct. The correct remedy is upstream — ask the
PUNCH SOC to add Chris Lowder to CITATION.cff, after which a later refresh will pick the name up
automatically. Recorded here so the gap is visible rather than silently absent.

**Affiliation gaps:** no primary source (repo, CITATION.cff, Zenodo, DataCite, punchbowl author list)
gives an affiliation for Tania Varesano or Suman Chapai, so both are left empty rather than guessed.

**Primary contact:** Marcus Hughes (PyHC registry `contact` field; `maintainers` in punchbowl's pyproject).

### 7. Software Name (MANDATORY)
**Value:** regularizePSF

**Source:** PRESERVED from live HSSI (authoritative on conflict). Matches the PyHC registry `name`
("regularizePSF") and the documentation's prose form. The prior canonical file used the lowercase
package/repo form "regularizepsf" (also used by CITATION.cff `title:`, pyproject `name`, SoMEF, and the
Zenodo record title). The camelCase display name is the curated live value and is retained; this is an
editorial choice, not a factual correction.

### 8. Description (MANDATORY)
**Value:** A Python package for manipulating and correcting variable point spread functions. The package
implements a technique for regularizing spatially-varying PSFs in astronomical imaging data. It allows users
to correct images observed with slowly varying PSFs and transform them to have a target PSF, improving image
quality and enabling more accurate scientific analysis. The technique uses Fourier-domain methods and
includes tools for star detection, PSF modeling from stellar cutouts, and visualization utilities.

**Source:** PRESERVED verbatim from live HSSI. The prior canonical file differs by one word ("uses
*iterative* Fourier-domain methods"); live wins on conflict, and the live wording is also the more accurate
one — `ArrayPSFTransform.construct()`/`apply()` perform a single regularized Fourier-domain division and
multiplication, with no iteration. Content re-verified against the code and against the reference
publication abstract; no factual correction is needed.

### 9. Concise Description (OPTIONAL)
**Value:** A Python package for manipulating and correcting various point spread functions.

**Source:** PRESERVED verbatim from live HSSI (77 characters, within the 200-character limit). Matches the
PyHC registry `description` exactly. The prior canonical file's variant ("…variable point spread functions
in astronomical imaging data.") is an editorial alternative only and was not substituted.

### 10. Publication Date (RECOMMENDED)
**Value:** 2022-12-02

**Source:** PRESERVED from live HSSI. Confirmed as the first published Zenodo version: record 7392171 /
7392212, version `v0.0.1`, `publication_date: 2022-12-02` (Zenodo versions query on
`conceptrecid:7392170`). The GitHub repository was created earlier (2022-10-21, SoMEF `date_created`), but
the field asks for date of first publication.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** PRESERVED from live HSSI. Confirmed by DataCite (`"publisher": "Zenodo"`) for
10.5281/zenodo.7392170. The DOI is minted through the GitHub–Zenodo integration.

### 12. Version (RECOMMENDED)

**Version Number:** 1.2.1

**Version Date:** 2026-07-28

**Version Description:** Bug-fix release. Removes the grid artifacts in corrected images that were caused
by apodization and sampling (PR #256). Internal change: the old CI test suite was removed (PR #260). Full
changelog: https://github.com/punch-mission/regularizepsf/compare/1.2.0...1.2.1

**Version PID:** https://doi.org/10.5281/zenodo.21640420

**Source:** REPLACES the stale live value (`regularizePSF - 1.1.0`, released 2025-07-17) and the stale prior
canonical file value (also 1.1.0). Evidence: git tag `1.2.1` at commit 8bd926e1 dated 2026-07-28;
`CITATION.cff` (`version: 1.2.1`, `date-released: 2026-07-28`); `CHANGELOG.rst` heading
"Version 1.2.1: Jul 28, 2026" with the Bug Fixes / Internal Changes entries quoted above; Zenodo record
21640420 (`"version": "1.2.1"`, `"publication_date": "2026-07-28"`,
`"doi": "10.5281/zenodo.21640420"`) — the version-specific DOI **does** exist and resolves. DataCite for the
concept DOI likewise now reports `"version": "1.2.1"` with `dates[Issued] = 2026-07-28`.

Intervening releases not previously recorded: 1.1.1 (2025-12-05), 1.1.2 (2026-02-20), 1.2.0 (2026-03-28).

### 13. Programming Language (RECOMMENDED)
**Value:** Python 3.x

**Source:** PRESERVED from live HSSI. Confirmed by `pyproject.toml` (`requires-python = ">3.10"`),
`.github/workflows/ci.yml` matrix (3.10, 3.11, 3.12, 3.13, 3.14 — 3.14 added in 1.1.2), and SoMEF
(`programming_languages: Python`). The package is pure Python since v1.0.0 removed Cython.

### 14. Reference Publication (RECOMMENDED)
**Value:** https://doi.org/10.3847/1538-3881/acc578

**Source:** PRESERVED from live HSSI. Hughes, J. M., DeForest, C. E., & Seaton, D. B. (2023), "Coma Off It:
Regularizing Variable Point-spread Functions," *The Astronomical Journal* 165(5), 204. Requested in
README.md ("Please cite the associated paper if you use this technique") and `docs/source/cite.rst`.

### 15. License (RECOMMENDED)
**License:** GNU Library or 'Lesser' General Public Licenses (LGPL version 3)

**License URI:** https://www.gnu.org/licenses/lgpl-3.0.html

**Source:** License name PRESERVED from live HSSI (live renders the quotes as typographic
'Lesser' — same controlled-vocabulary row). Confirmed by LICENSE: "This software may be used, modified, and
distributed under the terms of the GNU Lesser General Public License v3 (LGPL-v3)". License URI carried
forward from the prior canonical file (live HSSI exposes only the license name through the view API).
Known discrepancy, unchanged: the Zenodo/DataCite deposit records `cc-by-4.0`, which describes the Zenodo
deposit, not the source license; the LICENSE file is authoritative.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values (15) — 14 live values plus `plotting`. Shown in the live HSSI view API's title-cased rendering;
the storage form is lowercase (see the payload warning below):**
- Astronomical Algorithms
- Astronomy
- Astronomy Astrophysics
- Astronomy Software
- Calibration
- Data Analysis
- Fits
- Image Processing
- Plotting  *(NEW — stored as `plotting`)*
- Point Spread Function
- Psf
- Psf Estimation
- Punch
- Regularization
- Solar Physics

**Source:** The 14 live HSSI keywords are PRESERVED unchanged; `plotting` is ADDED. Independently corroborated: SoMEF reports the
GitHub repository topics as `astronomical-algorithms, astronomy, astronomy-astrophysics, astronomy-software,
image-processing, point-spread-function, psf, psf-estimation, punch, solar-physics` — a subset match — and
the remaining four (Calibration, Data Analysis, Fits, Regularization) correspond to the PyHC registry
keywords `calibration`, `data_analysis`, `fits` plus the package's own subject matter.

**`plotting` (added):** carried forward from the 2025-10-14 canonical file and from the PyHC registry's
`keywords` list for this package (`["plotting", "calibration", "general", "fits", "local", "data_analysis"]`,
fetched from the live registry). It is substantively true — `regularizepsf/visualize.py` provides
`visualize_grid()` and `visualize_patch_counts()`, and `ArrayPSF.visualize_psfs()`,
`ArrayPSF.visualize_ffts()` and `ArrayPSFTransform.visualize()` expose them publicly — and it already
exists in HSSI's `Keyword` vocabulary as the row `'plotting'`, so adding it links an existing row rather
than creating one.

**MANDATORY storage-form requirement for the payload builder:** HSSI's `Keyword` table stores every row
lowercase (`'astronomical algorithms'`, `'solar physics'`, `'psf'`, `'plotting'`, …) and the view API
title-cases them only for display. All 546 rows were checked: there are **zero** case-variant duplicates in
the vocabulary today. Because Keywords is an M2M field, PATCH replaces the entire list — so the payload
must send **all 15 values in their exact lowercase vocabulary spelling**. Sending the title-cased display
form risks creating 15 duplicate Title-Case `Keyword` rows. Verify the backend's match behaviour before
sending; if it cannot be confirmed case-insensitive, send lowercase regardless, since lowercase is the
literal stored form.

**Note (prior-file values not carried forward):** the 2025-10-14 canonical file listed two further keywords
that are not on the live record and are not added here — `local` and `solar`. `local` (and `general`) are
PyHC-internal taxonomy tags with no HSSI meaning. `solar` is subsumed by the live `Solar Physics`; it was
an editorial addition in the prior file, drawn from the package description and reference publication, not
from the PyHC registry (whose tag list, quoted above, contains no `solar` entry).

### 17. Data Sources (OPTIONAL)
**Value:** Not found

**Source:** Investigated and deliberately left empty (live HSSI is also empty). The package has **no**
network/data-retrieval code whatsoever: there is no `requests`/`urllib`/`ftplib`/`s3`/HAPI/CDAWeb client,
and no download helper anywhere in `regularizepsf/`. Every input arrives as a local FITS path, a local
HDF5 path, an in-memory NumPy array, or a Python generator
(`ArrayPSFBuilder.build()`, `ArrayPSF.load()`, `ArrayPSFTransform.load()`). The PyHC registry tags it
`local` for exactly this reason. `Observatory/Mission-specific` was considered and rejected — the package
does not read any mission's archive or mission-specific product.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- FITS
- HDF5

**Source:** PRESERVED from live HSSI, re-verified in code. FITS: `astropy.io.fits.open()` in
`image_processing.process_single_image()` (with an `hdu_choice` selector and a `sqrt_compressed` path that
reads the `SCALE` header keyword) and in `ArrayPSF.load()` / `ArrayPSFTransform.load()`. HDF5:
`h5py.File(path, "r")` in the same two `load()` classmethods. `ArrayPSF.load()`/`ArrayPSFTransform.load()`
raise `NotImplementedError` for any suffix other than `.h5` and `.fits`, so the list is exhaustive.

### 19. Output File Formats (RECOMMENDED)
**Values:**
- FITS
- HDF5

**Source:** PRESERVED from live HSSI, re-verified in code. `ArrayPSF.save()` and
`ArrayPSFTransform.save()` write `.h5` via `h5py` and `.fits` via
`astropy.io.fits.HDUList([...CompImageHDU...]).writeto()`; any other suffix raises `NotImplementedError`.
Round-tripping in both formats is covered by `tests/test_psf.py::test_arraypsf_saves_and_loads` and
`tests/test_transform.py::test_transform_saves_and_loads` (both parametrized over the two extensions).

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Operating System Independent
- Windows

**Source:** PRESERVED unchanged from live HSSI. Pure-Python package with no compiled extensions (Cython was
removed in v1.0.0; `.github/workflows/python-publish.yml` builds an sdist only), so it installs anywhere
CPython 3.10+ and the dependency wheels are available. CI exercises `ubuntu-latest`.

**Note:** the prior canonical file's "OS Independent" is **not** a separate value — that string does not
exist in HSSI's `OperatingSystem` vocabulary; the equivalent row "Operating System Independent" is already
present. No change.

### 21. CPU Architecture (RECOMMENDED)
**Value:**
- CPU Independent

**Source:** PRESERVED unchanged from live HSSI. The package is pure Python with no compiled extensions
(Cython was removed in v1.0.0) and no architecture-specific code, so "CPU Independent" is the complete and
accurate answer.

**Note (prior-file values deliberately dropped):** the 2025-10-14 canonical file additionally listed
`x86-64` and `Apple Silicon arm64`. Both are real `CpuArchitecture` vocabulary rows, but no repository
source declares either one — the justification was only that CI runs on x86-64 `ubuntu-latest` runners and
that the dependency wheels exist for both. That is an inference about where the package *happens* to have
been run, not a statement about what it supports, and it adds nothing that "CPU Independent" does not
already say. Naming two architectures alongside "CPU Independent" also reads as a narrowing. Dropped so the
field stays precise; this produces **no** patch for Field 21.

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found

**Source:** Investigated and deliberately left empty (live HSSI is also empty). HSSI's `Phenomena`
vocabulary offers Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares,
Solar Wind, X-ray emission. regularizePSF implements no phenomenon-specific science: it corrects the
point-spread function of *any* imager, and its own reference publication states the method "does not
require access to the instrument that obtained the data" and frames it generically for "a telescope or
other imaging instrument". "Solar Corona" was considered (PUNCH images the corona and the inner
heliosphere, and PSF regularization helps recover faint coronal/CME signal) but rejected because the
package has no coronal-physics functionality — that science lives in `punchbowl`, not here. Recorded as a
deliberate "no", not an oversight.

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** NEWLY FILLED — live HSSI has `developmentStatus: null`. Matches the `RepoStatus` vocabulary row
"Active" ("reached a stable, usable state and is being actively developed", repostatus.org). Evidence:
four releases within the trailing twelve months plus a fifth immediately before that window
(1.1.0 2025-07-17, 1.1.1 2025-12-05, 1.1.2 2026-02-20, 1.2.0 2026-03-28, 1.2.1 2026-07-28, the last of
which is HEAD); a maintained `CHANGELOG.rst` driven by towncrier; weekly-scheduled CI plus per-PR CI across Python 3.10–3.14 (3.14 added 2026-02); active
pre-commit autoupdates; SoMEF `date_updated` 2026-07-28; PyHC registry rates community, documentation,
testing, software maturity, Python 3, and license all "Good"; and the package is a live dependency of
PUNCH's operational `punchbowl` pipeline. The prior canonical file also concluded "Active".

### 24. Documentation (RECOMMENDED)
**Value:** https://regularizepsf.readthedocs.io/

**Source:** PRESERVED from live HSSI (authoritative on conflict). Independently produced by SoMEF
(`documentation`, readthedocs format, confidence 1). The prior canonical file's
`https://regularizepsf.readthedocs.io/en/latest/` is the same site with an explicit version segment (it is
also the URL in README.md and the PyHC registry `docs` field); the version-less canonical root is the
better long-term value and is kept.

### 25. Funder (OPTIONAL)
**Value:** National Aeronautics and Space Administration

**Funder Identifier:** https://ror.org/027ka1x80

**Source:** NEWLY FILLED — live HSSI is empty. Evidence: Crossref funding metadata for the reference
publication (`GET https://api.crossref.org/works/10.3847/1538-3881/acc578`) records
`funder: [{"name": "NASA ∣ Goddard Space Flight Center", "award": ["80GSFC18C0014"]}]` — the NASA contract
under which the PUNCH Small Explorer, and therefore this technique and its implementation, were developed.
The organization name is given in full per the "expand acronyms" rule; ROR confirmed via
`https://api.ror.org/v2/organizations?query=National+Aeronautics+and+Space+Administration`.

**Note:** Crossref attributes the award specifically to the administering NASA center, Goddard Space Flight
Center (ROR https://ror.org/0171mag52). The parent agency is recorded above as the funder because HSSI's
guidance asks for the funding organization's full name; substituting or adding
"Goddard Space Flight Center" is a reasonable curator alternative. No funding statement appears in the
repository itself, and Zenodo/DataCite carry `grants: []` / `fundingReferences: []`, so this value rests
entirely on the reference publication's registered funding metadata.

### 26. Award Title (OPTIONAL)
**Award Title:** Polarimeter to UNify the Corona and Heliosphere (PUNCH)

**Award Number:** 80GSFC18C0014

**Source:** NEWLY FILLED — live HSSI's `award` list for this software is empty, but HSSI's shared `Award`
vocabulary **already contains this grant**: row `03ab3ee8-fbc6-4a4e-a2da-da87a6c2d5ab`,
`identifier = "80GSFC18C0014"`, `name = "Polarimeter to UNify the Corona and Heliosphere (PUNCH)"`. That
row is already linked to `punchbowl`, the companion PUNCH pipeline (Field 30) — independent confirmation
that it is the correct grant for PUNCH-SOC software.

The award *number* was independently derived from Crossref funding metadata for the reference publication
(`GET https://api.crossref.org/works/10.3847/1538-3881/acc578` →
`funder: [{"name": "NASA ∣ Goddard Space Flight Center", "award": ["80GSFC18C0014"]}]`), which matches the
existing row's identifier exactly. The award *title* is taken verbatim from that HSSI row.

**Why the title is HSSI's string and not one derived from an external source:** `Award` is a shared entity.
`submission.py::_get_or_create_award` requires a non-blank `name` (an identifier-only object returns 400),
and on an `identifier` match it returns the existing row immediately and **discards the submitted name**.
So the end state is this title regardless of what is sent; recording it here makes the file match reality
instead of asserting a title that would be silently thrown away. An earlier draft of this field said "no
primary source states an award title" — true of sources *outside* HSSI, but HSSI's own database does state
one, which is the better evidence.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** https://doi.org/10.3847/1538-3881/acc578

**Source:** PRESERVED from live HSSI (the same DOI is also the Reference Publication, Field 14). This is
the only publication the repository points to — README.md, `docs/source/cite.rst`, and
`docs/source/concepts.rst` all cite it and nothing else. No additional describing/citing publications are
identified by any primary source, so nothing was added.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Source:** Investigated and deliberately left empty (live HSSI is also empty). The repository ships exactly
one data file, `tests/data/compressed_dash.fits`, which is an unpublished test fixture with no DOI, no
citation, and no accompanying description. Zenodo/DataCite record no `Dataset` related identifiers. The
package is dataset-agnostic — it operates on whatever starfield imagery the user supplies.

### 29. Related Software (OPTIONAL)
**Values:**
- Source Extraction and Photometry (sep): https://github.com/sep-developers/sep
- Astropy: https://github.com/astropy/astropy

**Source:** NEWLY FILLED — live HSSI is empty. Both pass the Field 29 gate as *domain-specific* dependencies
whose presence characterizes the software:
- **sep** — astronomy-specific source-extraction library (SExtractor bindings; PyPI summary "Astronomical
  source extraction and photometry library"). It is how regularizePSF finds its point sources:
  `regularizepsf/image_processing.py` calls `sep.Background(image)` and `sep.extract(...)` in
  `_find_patches()`, which is the entry point for every empirical PSF model the package builds. Repository
  URL from the PyPI `sep` project metadata (`Homepage`/`Bug Tracker` → `sep-developers/sep`).
- **astropy** — the astronomy-domain FITS layer this package is built on: `astropy.io.fits` in
  `regularizepsf/psf.py`, `regularizepsf/transform.py`, and `regularizepsf/image_processing.py`, including
  the public `hdu_choice` argument on `ArrayPSFBuilder.build()` and the FITS branch of every
  `save()`/`load()`.

**Note (considered and excluded — audit trail):**
- **numpy, scipy, matplotlib, scikit-image, h5py** — Tier A / generic infrastructure. Arrays, numerics,
  plotting, general image filtering, and HDF5 plumbing would be equally at home in a web app, a finance
  model, or a biology pipeline; listing them says nothing about this package. All five were listed in the
  prior canonical file's Field 29 (which was a raw `pyproject.toml` dependency dump) and are **removed**
  here by the relevance gate. `scikit-image` is used only for `downscale_local_mean`.
- **photutils** — appears only in the documentation example (`docs/source/example.ipynb`) to synthesize a
  fake starfield; a tutorial name-drop, not a relationship. (It does overlap in purpose via `photutils.psf`,
  so a curator could argue for it as similar-purpose software; excluded here for lack of any stated
  relationship in the repository.)
- **pytest, pytest-cov, pytest-mpl, hypothesis, coverage, ruff, sphinx, nbsphinx, pre-commit, setuptools,
  setuptools-scm** — test/build/doc tooling.
- **punchbowl** — a genuine relationship, but it is a demonstrated *exchange*, so it is recorded under
  Field 30 rather than duplicated here.

### 30. Interoperable Software (OPTIONAL)
**Values:**
- punchbowl: https://github.com/punch-mission/punchbowl

**Source:** NEWLY FILLED — live HSSI is empty. `punchbowl` ("Calibration for the PUNCH mission" /
"PUNCH science calibration code") is the companion pipeline from the same PUNCH Science Operations Center,
and the exchange is concrete and citable, not ecosystem hand-waving:
`punchbowl/level1/psf.py` begins
`from regularizepsf import ArrayPSF, ArrayPSFBuilder, ArrayPSFTransform, simple_functional_psf, varied_functional_psf`
and `from regularizepsf.util import calculate_covering`, then defines
`build_psf_transform(...) -> ArrayPSFTransform` — i.e. regularizePSF's own model objects are the
interchange currency, constructed in punchbowl and applied to PUNCH Level-1 data. `regularizepsf` is a
declared runtime dependency in punchbowl's `pyproject.toml` (and is wired as an editable sibling checkout,
`regularizepsf = { path = "../regularizepsf", editable = true }`, showing the two are co-developed).

**Note (considered and excluded — audit trail):**
- **astropy** (Tier B) — no adapter or shared data model. The public API neither accepts nor returns
  `astropy` objects: `ArrayPSFBuilder.build()` takes paths, NumPy arrays, or generators, and `save()`/
  `load()` use `astropy.io.fits` internally to read and write files. That is "uses astropy internally"
  plus FITS support, which is already captured in Fields 18/19 — it does not meet the Tier B bar.
- **h5py** (Tier B) — same reasoning; HDF5 files are the interchange, not h5py objects.
- **numpy, scipy, matplotlib, scikit-image** — Tier A, never eligible.
- The prior canonical file listed **astropy** here justified by "the core astronomy package in Python and
  regularizepsf follows astropy conventions" — an explicit ecosystem-membership claim, which the gate rules
  out. Removed; flagged here so the removal is visible.

### 31. Related Instruments (OPTIONAL)
**Value:** Not found

**Source:** Investigated and deliberately left empty (live HSSI is also empty). This is a *relevance*
decision, not an unresolved lookup — no `NEEDS MANUAL RESOLUTION` blocker exists for this field.

The package is instrument-agnostic by design and by its own claim: the reference publication states the
method works "across [an instrument's] entire field of view" for "a telescope or other imaging instrument"
and "does not require access to the instrument that obtained the data … [it] can be bootstrapped from
existing data sets that include starfield images". There is no instrument-specific parser, calibration
constant, format, or convention anywhere in `regularizepsf/` — the only FITS-specific knobs are the generic
`hdu_choice` index and a `SCALE` header keyword used when `sqrt_compressed=True`. A user searching HSSI for
a specific instrument should not get this package back; a user searching for the PUNCH *mission* should,
and that is captured in Field 32.

**Considered and excluded:**
- **PUNCH Wide Field Imager / Narrow Field Imager** — regularizePSF supports PUNCH at the mission level
  (Field 32), not any individual PUNCH instrument; no NFI- or WFI-specific code exists. Independently, the
  SPASE vocabulary would not permit a clean WFI entry anyway: `Wide Field Imager` / abbreviation `WFI`
  matches three type-1 rows (`.../NASA/Instrument/PUNCH/WFI/1`, `/2`, `/3`) — an unresolved collision, which
  per the resolution ladder means omit and document rather than guess. `Narrow Field Imager` does resolve
  uniquely (`https://spase-metadata.org/NASA/Instrument/PUNCH/NFI`, with a `.html` duplicate), but listing
  NFI alone while omitting its three WFI siblings would misrepresent the package as NFI-specific.
- **"DASH"** (`tests/data/compressed_dash.fits`) — a test fixture filename only, never described or
  supported as an instrument in the repository, and absent from the SPASE vocabulary (zero type-1 or type-2
  rows named or abbreviated `DASH`). Test-data name-drops are excluded by the relevance gate.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Polarimeter to Unify the Corona and Heliosphere (PUNCH)
- **Observatory Identifier:** https://spase-metadata.org/NASA/Observatory/PUNCH.html

**Source:** PRESERVED exactly as bound on the live HSSI record (row `d882f614-6240-4f53-a423-295236b5c27b`);
name copied verbatim from the controlled `InstrumentObservatory` vocabulary (type 2, SPASE-backed).
Passes the relevance gate: `docs/source/index.rst` — "It was originally developed for the PUNCH mission";
LICENSE — "Copyright (c) 2024 PUNCH Science Operations Center"; the repository lives in the
`punch-mission` GitHub organization; and PUNCH's operational calibration pipeline `punchbowl` calls this
package to build and apply its Level-1 PSF transform. A scientist working with PUNCH data would expect this
package back.

**Note:** the vocabulary also contains a bare-identifier near-duplicate of this resource,
`PUNCH Mission` → `https://spase-metadata.org/NASA/Observatory/PUNCH` (the resolution ladder normally
prefers the non-`.html` form). The live record is already bound to the `.html` row, and re-pointing it would
risk creating a second observatory link on the record for the same resource, so the existing binding is kept
deliberately. The mission-level row is also preferred over the four platform-level rows (`PUNCH-NFI`,
`PUNCH-WFI-1/2/3`), which would over-specify a package that supports the mission generally.

### 33. Logo (OPTIONAL)
**Value:** Not found

**Source:** Investigated and deliberately left empty (live HSSI stores `""`). There is no logo asset in the
repository: `docs/source/conf.py` sets no `html_logo` or `html_favicon`, and no `docs/source/_static`
directory exists at all; the images that exist (`model_example.png`, `docs/source/images/*.png`) are scientific example
figures, not marks. The PyHC registry entry for regularizePSF has no `logo` field, and SoMEF returned no
`logo` result.

---

## Extraction Summary

### Sources consulted
1. **Live HSSI record** — `GET http://localhost/api/view/software/ec808735-972e-41e7-8549-a96d93881e26/`
   (decoded) and the UUID-keyed raw form, used as the authoritative seed.
2. **Prior canonical `hssi_metadata.md`** (2025-10-14) — seeded, then corrected where stale.
3. **Zenodo API** — concept record 7392170 (concept DOI confirmation) and the full version list
   (32 versions; 1.2.1 → 10.5281/zenodo.21640420, 2026-07-28; oldest v0.0.1 → 2022-12-02).
4. **DataCite API** — `10.5281/zenodo.7392170` (creators/ORCIDs, publisher, version, dates, rights,
   empty `fundingReferences`).
5. **Crossref API** — `10.3847/1538-3881/acc578` (funder NASA/GSFC, award 80GSFC18C0014, abstract).
6. **ROR API (v2)** — NASA `027ka1x80`, GSFC `0171mag52`, SwRI `03tghng59`.
7. **PyHC registry** — all three YAML files parsed in full; regularizePSF is a **community** package
   (`projects.yml`), all six quality ratings "Good".
8. **SoMEF 0.7** — GitHub topics, description, documentation URL, license text, release 1.2.1, no logo.
9. **HSSI controlled vocabularies** (localhost) — `FunctionCategory`, `RepoStatus`, `Phenomena`,
   `DataInput`, `OperatingSystem`, `CpuArchitecture`, `Keyword`, and the cached
   `InstrumentObservatory` list (7,648 rows, filtered locally).
10. **Repository at 8bd926e1** — README.md, CITATION.cff, LICENSE, pyproject.toml, CHANGELOG.rst,
    `regularizepsf/*.py` (all 8 modules), `tests/*.py`, `docs/source/*`, `.github/workflows/*`, git tags.
11. **punchbowl** (`punch-mission/punchbowl`) — `pyproject.toml` and `punchbowl/level1/psf.py`, for the
    Field 30 interoperability evidence.

### Change summary vs. live HSSI
- **Replaced (stale):** Field 12 Version → 1.2.1 / 2026-07-28 / new description / new version DOI.
- **Newly filled (was empty):** Field 23 Development Status; Field 25 Funder; Field 26 Award (number and
  title, via HSSI's existing shared `Award` row); Field 29 Related Software; Field 30 Interoperable Software.
- **Extended:** Field 4 Software Functionality (+4 values, all six live values retained);
  Field 16 Keywords (+`plotting`, all 14 live values retained).
- **Preserved unchanged:** Fields 2, 3, 5, 6 (people + affiliations), 7, 8, 9, 10, 11, 13, 14, 15, 18, 19,
  20, 21, 24, 27, 32.
- **Still "Not found" after investigation:** Fields 17, 22, 28, 31, 33 (each with written justification).

### Validation findings applied (validator report, 2026-07-28)
- **E1** — provenance header label corrected from `HSSI UUID:` to the corpus-standard `HSSI Software ID:`.
- **W1** — Field 6: removed the incorrect "No new authors were found" claim and documented the uncredited
  contributor Chris Lowder (16 commits, core shipping features) as an upstream CITATION.cff gap.
- **S1** — Field 4: added `Models and Simulations:Observatory/Instrument Models` (taxonomy indicator
  "synthetic observations" matches the docs notebook panel label verbatim).
- **S2** — Field 16: corrected the provenance note for the prior file's `solar` keyword.
- **S3** — Field 23: corrected "five releases in the last twelve months" to four-plus-one.
- **S4** — Field 33: corrected "`docs/source/_static` holds no brand image" to "no `_static` directory exists".
- **S5** — Field 29: no change; repository URLs are an explicitly permitted form and are the corpus convention.
- **S6** — Field 31: no change; the relevance-based omission was independently confirmed defensible.
- **S7** — Fields 25/26: no change; the Crossref funder/award data was independently reproduced by the
  validator and the inference is already disclosed in-field.
- Curator decisions taken alongside: Field 16 `plotting` added; Field 21 reduced to the live
  "CPU Independent" alone; Field 5 left at "Solar Environment" (Interplanetary Space not added); Field 32
  left bound to the existing `.html` SPASE row.

### Completeness
- All 33 fields present: **yes**
- All MANDATORY fields populated: **yes** (Submitter is the standard placeholder)
- Dates in YYYY-MM-DD: **yes** · DOIs as full `https://doi.org/…` URLs: **yes**
- Fields 31/32 SPASE-only, no bare names, no unresolved collisions emitted: **yes**
- Outstanding data issue for humans: the `Sam Van` / `Kooten` name split in the live HSSI `Person` row
  (see Field 6) — not fixable through the update API.
