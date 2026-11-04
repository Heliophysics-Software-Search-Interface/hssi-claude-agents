# HSSI Metadata Extraction Results

**HSSI Software ID:** 9d1318b8-bb6b-490f-bdce-fe7811c6d879
**Repository:** https://github.com/aburrell/pyIntensityFeatures
**Source Revision:** 72e6e1de8dd439ea9e152ac58d8fc93e8f1bffc4
**Extraction Date:** 2026-11-03
**Validation Date:** 2026-11-03
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

The source revision is the `v0.2.0` release commit, which is also the head of `main` (the default
branch). The only other branch, `develop`, differs from it by a single same-day merge of `main` back
into `develop` that changes no file; the release and the default branch are what this record
describes.

**pyIntensityFeatures reads no files and reaches no network.** Its one public class,
`pyIntensityFeatures.AuroralBounds`, takes an in-memory data object of any type that exposes the named
variables as attributes or keys (the class docstring names `pysat.Instrument`, `xr.Dataset`,
`pds.DataFrame` and a dict of arrays) and returns its result as an in-memory `xarray.Dataset`. Several
fields below (17, 18, 19, 22, 31, 32) are therefore evidenced-empty rather than unexamined, and the
instruments named in the documentation (TIMED/GUVI) and in the reference paper (TIMED/GUVI and
DMSP/SSUSI) are worked-example and demonstration inputs, not data the package itself is built to
read. The one durable link this software has to those instruments is the pair of boundary data sets
its lead author produced with it, recorded in Field 28.

Literature evidence is taken from the reference publication (Field 14). The publisher's site refuses
automated requests; the authors' open-access copy in the NERC Open Research Archive
(`https://nora.nerc.ac.uk/id/eprint/540294/`) carries the full text, and its acknowledgements, data
availability statement and author contributions are the passages cited below.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** Shawn Polson
- **Submitter Email:** shawn.polson@lasp.colorado.edu

Supplied by the user for this new submission (Field 1 rule 4). The only personal address in the
repository, `angeline.g.burrell.civ@us.navy.mil` (`pyproject.toml` `authors` and the contact line of
`CODE_OF_CONDUCT.md`; also the reference paper's corresponding-author address), is the lead author's
correspondence address and is deliberately not the submitter (rule 2). Before this submission the
submitter's Person record in HSSI already held given name `Shawn`, family name `Polson`, with ORCID
`https://orcid.org/0000-0003-0619-5745`; the name above is written in exactly that form, which is
what binds that record rather than creating a new one.

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.15102100

The concept ("all versions") DOI of the project's GitHub–Zenodo integration series (Field 2 rule 5).
DataCite registers it as `resourceTypeGeneral: Software`, publisher Zenodo, with `HasVersion`
relations to two version deposits:

- `10.5281/zenodo.19135203` — `aburrell/pyIntensityFeatures: Version 0.2.0`, version `v0.2.0`, issued
  2026-03-20, `IsSupplementTo https://github.com/aburrell/pyIntensityFeatures/tree/v0.2.0`;
- `10.5281/zenodo.15102101` — `aburrell/pyIntensityFeatures: Version 0.1.0`, version `v0.1.0`, issued
  2025-03-28, `IsSupplementTo https://github.com/aburrell/pyIntensityFeatures/tree/v0.1.0`.

The `IsSupplementTo` tree links prove both are integration deposits of this repository. The project
itself cites this concept DOI: the README's DOI badge points at `https://doi.org/10.5281/zenodo.15102100`,
and all 25 Python files in the package carry the header line `# DOI: 10.5281/zenodo.15102100`.

What the Software citation will show: a Zenodo concept DOI resolves to the most recently created
deposit, which is the v0.2.0 deposit — DataCite gives the concept the version `v0.2.0` and the title
`aburrell/pyIntensityFeatures: Version 0.2.0`. That is the same release Field 12 records. The public
`v0.0.1` alpha release has no deposit; the Zenodo series begins at v0.1.0.

Considered and not used here:
- `10.5281/zenodo.15102101` — the v0.1.0 version DOI, cited by `docs/citing.rst` (line 21) and by the
  reference paper's bibliography. A version DOI is never Field 2 (rule 3), and it is not Field 12's
  Version PID either, because Field 12 records 0.2.0.
- `10.5281/zenodo.19135203` — the v0.2.0 version DOI; it is Field 12's Version PID.
- `10.1029/2025JA034230` — the journal article describing the software; an article is never Field 2
  (rule 1). It is Field 14.

Coupled field: because Field 2 is a Zenodo DOI, Field 11 is Zenodo.

### 3. Code Repository (MANDATORY)
https://github.com/aburrell/pyIntensityFeatures

The canonical repository root (Field 3 rule 7). Every source agrees on the same string: the clone's
`origin` remote, the GitHub API (`full_name` `aburrell/pyIntensityFeatures`, not a fork, not
archived), `pyproject.toml` `[project.urls] Source`, `setup.cfg` `url`, the Zenodo deposits'
`code:codeRepository`, and the PyHC registry entry's `code:`. Two stale strings in the repository were
considered and are not alternatives: the README's clone instruction uses the retired
`git://github.com/aburrell/pyIntensityFeatures.git` protocol form of the same repository, and
`docs/installation.rst` still carries the template placeholder `https://github.com/PACKAGE_REPOSITORY`.
No wiki repository exists (`pyIntensityFeatures.wiki.git` answers "Repository not found").

### 4. Software Functionality (RECOMMENDED — treated as critical)
- Data Processing and Analysis
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Reduction
- Coordinate Transforms
- Coordinate Transforms: Ionospheric

All six are live `FunctionCategory` rows, written in the qualified `Parent: Child` form, and each child
is accompanied by its bare parent (rule 10). The package's primary family is listed first. Evidence,
value by value, from the code at the source revision:

- **Data Processing and Analysis: Image Processing** — the package exists to detect features in imager
  data ("identifies features in imager intensity data", README; "routines to identify features in
  imager intensity data", `docs/index.rst`). `instruments.satellites.get_auroral_slice` extracts from a
  satellite imager's time × sweep-location intensity, latitude and longitude arrays the scan that
  covers the auroral zone of one hemisphere (applying an optional clean mask and a `min_colat`
  latitude cut), and `AuroralBounds.set_boundaries` → `proc.intensity.find_intensity_boundaries`
  locates the poleward and equatorward auroral luminosity boundaries in each gridded image. That is
  feature detection in 2D image data, which is what this row means.
- **Data Processing and Analysis: Analysis** — the package derives physical quantities and their
  uncertainties: boundary locations (`proc.boundaries.locate_boundaries`,
  `locate_single_peak_boundaries`, `locate_mult_peak_boundaries`, `get_eval_boundaries`) and their
  uncertainties (`proc.boundaries.calc_boundary_uncertainty`), from least-squares fits of one or more
  Gaussian peaks on a quadratic background (`proc.fitting.get_gaussian_func_fit`,
  `get_fitting_params`, `estimate_peak_widths`; `utils.distributions.mult_gauss_quad`), followed by
  statistical evaluation (`utils.checks.evaluate_gauss_quad`, `evaluate_pearson`, `compare_pearson`,
  `evaluate_dayglow`, and `evaluate_boundary_in_mlt`, which removes outliers by interquartile range
  across local time). The docs page "Using the Fitting Functions" (`docs/examples/ex_fitting.rst`)
  presents the fitting functions as usable "for more than just identifying auroral boundaries".
- **Data Processing and Analysis: Data Reduction** — `utils.grids.grid_intensity` bins the scattered
  imager intensities into a magnetic-latitude × magnetic-local-time grid (bin sizes set by the user
  through `set_boundaries(mlat_inc=..., mlt_inc=...)`, defaults 1° and 0.5 h) and returns the mean,
  standard deviation and count in each bin. Those reduced grids are handed to the user in the returned
  `boundaries` Dataset as `mean_intensity`, `std_intensity` and `num_intensity`, so the reduction is a
  user-facing product, not only an internal step.
- **Coordinate Transforms: Ionospheric** — `utils.coords.convert_geo_to_mag` converts geographic
  latitude and longitude at the emission altitude to magnetic latitude, magnetic longitude and magnetic
  local time, using AACGM-v2 (`aacgmv2.get_aacgm_coord_arr` with method `TRACE`, `ALLOWTRACE`,
  `BADIDEA` or `GEOCENTRIC`) or, when the optional apexpy is installed, apex or quasi-dipole
  coordinates. The user selects the system through the documented `set_boundaries(mag_method=...)`
  keyword and receives every boundary in the converted coordinates, so the transform is user-facing
  under rule 3. AACGM, apex and quasi-dipole coordinates and MLT are exactly the systems this child
  names.

Considered and rejected:
- **Data Visualization (any child)** — the package contains no plotting code; `matplotlib` appears only
  in the documentation example `docs/examples/ex_fitting.rst`, which draws its own figures (rule 4).
- **Data Processing and Analysis: Data Access and Retrieval** — the package has no network code. The
  GUVI download in the README and in `docs/examples/ex_pysat.rst` is performed by pysat and pysatNASA
  (rules 4 and 5).
- **Data Processing and Analysis: Processing** — the catch-all; the specific children above already
  carry every capability it would stand for.
- **Data Processing and Analysis: Time Series Analysis** — time is used only to select the scan to
  process; nothing analyses a time series (the outlier check runs across local time within one scan).
- **Data Processing and Analysis: 2D Slices** — `get_auroral_slice` takes a time-ordered subset of a
  2D imager sweep, not a cross-section of a 3D data volume, so the "slice" in its name is not this
  row's capability.
- **Data Processing and Analysis: File Format Conversion** — the package writes no file (Field 19).
- **Data Processing and Analysis: Calibration** — intensity cleaning is a user-supplied `clean_func`
  (the docs' GUVI example applies the instrument team's quality flag); the package applies no
  calibration.
- **Models and Simulations (Empirical, Forward-Fitting or any child)** — the multi-Gaussian-plus-quadratic
  fit is curve fitting used to locate features in observed profiles, not a model of a physical system,
  and nothing is simulated or forecast.
- **Coordinate Transforms: Magnetospheric** — no GSE/GSM/SM/GEO/MAG frame conversion exists; the
  systems converted are the ionospheric ones above.
- **Mission-related** — the package is data-source agnostic and part of no mission's processing chain
  (rule 8).
- **ML/AI** — no machine-learning code or dependency.

### 5. Related Region (RECOMMENDED — treated as critical)
- Earth Atmosphere
- Earth Ionosphere
- Earth Auroral Subregion

All three are live `Region` rows; the coarse row is written first, followed by the fine rows it
contains.

- **Earth Auroral Subregion** and **Earth Ionosphere** (rule 4) — the software locates the poleward
  and equatorward boundaries of auroral luminosity, i.e. the edges of the auroral oval
  (`docs/overview.rst`: "auroral luminosity boundaries at the poleward and equatorward edges of the
  auroral oval"). Its code is restricted to auroral latitudes (`get_auroral_slice`'s `min_colat=45`
  equatorward limit; `set_boundaries(min_mlat_base=59.0)`), it places the observed emission at the
  ionospheric altitude the user supplies (`alt`, 110 km in the documented example), and the reference
  paper frames the imagers it serves as instruments "used to identify and study ionospheric phenomena".
  This is the same pairing the rubric gives an all-sky-imager tool.
- **Earth Atmosphere** — the coarse row containing both fine rows (rule 5), so the entry is found by a
  user filtering at the broad level.

Considered and rejected:
- **Earth Thermosphere** — the luminosity is treated as a 2D image mapped to one user-supplied
  altitude; nothing computes neutral-atmosphere physics. The dayglow threshold
  (`utils.checks.evaluate_dayglow`) is a fit-quality check, not thermospheric analysis.
- **Earth Magnetosphere and its fine rows** — `magnetosphere` appears in the project only as a declared
  keyword (`pyproject.toml`, `.zenodo.json`), which is a label, not evidence of where the physics
  happens (rule 3). The reference paper notes that the poleward boundary is often used as a proxy for
  the open–closed magnetic field line boundary; that is a downstream use of the output, not something
  the software computes (rule 4).
- **Earth Lower and Middle Atmosphere** and every solar, heliospheric and planetary row — nothing in the
  code, docs or paper concerns them.

### 6. Authors (MANDATORY)
- **Author 1:**
  - **Name:** Angeline Burrell (given name `Angeline`, family name `Burrell`)
  - **Author Identifier:** https://orcid.org/0000-0001-8875-9326
  - **Affiliation:**
    - **Organization:** United States Naval Research Laboratory
    - **Affiliation Identifier:** https://ror.org/04d23a975
- **Author 2:**
  - **Name:** Nicola S. Longden (given name `Nicola S.`, family name `Longden`)
  - **Author Identifier:** Not found — see below
  - **Affiliation:** None recorded — see below
- **Author 3:**
  - **Name:** Gareth Chisham (given name `Gareth`, family name `Chisham`)
  - **Author Identifier:** https://orcid.org/0000-0003-1151-5934
  - **Affiliation:**
    - **Organization:** British Antarctic Survey
    - **Affiliation Identifier:** https://ror.org/01rhff309

**Who the authors are.** The project's own software-metadata sources name exactly these three people:
the `.zenodo.json` `creators` (and hence both Zenodo/DataCite deposits) list Angeline G. Burrell,
Nicola S. Longden and Gareth Chisham in that order; `docs/citing.rst` cites the software as
`Burrell, A. G. and Longden, N. S. and Chisham, G.`; the `LICENSE` copyright line names Angeline G.
Burrell, Gareth Chisham and Nicola Longden; and the reference paper's bibliography cites the software
deposit as "Burrell, A. G., Longden, N. S., & Chisham, G. (2025)". `pyproject.toml` lists Burrell alone
as `authors`. The order recorded is the order of the creator list and of the project's software
citation. Every one of the 119 commits on the pinned history is authored by Angeline Burrell (under
five name/address variants), so git history adds no candidate.

**Nicola Longden is the originator of the method** the package implements (Longden et al. 2010, Field
27; the code's docstrings describe the boundary search as "based on, but not identical to, the method
developed by Longden, et al. (2010)"). An originator is not an author by that fact alone (rule 3), but
the project's own Zenodo creators name her as an author, so rule 8 applies; the reference paper's
author-contribution statement also credits her with Methodology and Software. Her name is the
project's own fullest spelling, from `.zenodo.json` ("Nicola S. Longden"), split by the
"Given Name, Initials, Surname" convention because no ORCID record or `CITATION.cff` supplies a
structured split (rule 12).

**No ORCID for Nicola Longden.** No project source or DOI record carries one, and a fielded ORCID search
(`given-names:Nicola AND family-name:Longden`) returns no record, and a broader `family-name:Longden`
search returns no one named Nicola. The same fielded form returns exactly Gareth Chisham's record for
`Gareth`/`Chisham` and Angeline Burrell's for `Angeline`/`Burrell` (positive controls). Recorded so a
later refresh re-checks rather than adopts a name-only match (rule 14).

**No affiliation for Nicola Longden — a deliberate, reversible omission (rules 18 and 20).** The
sources disagree about her institution: `.zenodo.json` gives `KPMG`, while the reference paper's byline
(2025) gives "Formerly at British Antarctic Survey, Cambridge, UK". The method she originated was
published from the British Antarctic Survey (all four BAS authors of Longden et al. 2010 give its
Cambridge address), and the 2025 byline marks that affiliation as former, so KPMG reads as an employer
joined after the work she contributed (rule 18); a "formerly at" institution, displayed without dates,
would instead tell a reader she is at BAS now. No institution is true under both readings, so none is
asserted (rule 20); an affiliation can be added later, but not withdrawn. Both candidates are recorded
here so a later refresh can reconsider them if the project's metadata changes.

**Affiliations of the other two authors (rule 21).** Burrell: `.zenodo.json` gives "Naval Research
Laboratory", her ORCID employment record lists US Naval Research Laboratory, Space Science Division,
from 2018 with no end date, and the reference paper's byline agrees; it is recorded under the full
institutional name and ROR `https://ror.org/04d23a975` (ROR display name "United States Naval Research
Laboratory"; rule 22). Chisham: `.zenodo.json`, his ORCID employment record (British Antarctic Survey,
Space Weather and Atmosphere, from 1998, no end date) and the paper's byline all give the British
Antarctic Survey, ROR `https://ror.org/01rhff309`. HSSI already holds Organization records under exactly
these two names with these two RORs.

**Name forms (rule 10).** Burrell and Chisham are recorded under the forms their existing HSSI Person
records carry (`Angeline`/`Burrell`, `Gareth`/`Chisham`, each with the ORCID above), which is also how
their ORCID records structure their names; "Angeline G." in `.zenodo.json` is a middle-initial style
variant, and `pyproject.toml` itself writes "Angeline Burrell". An ORCID that an existing record
carries binds that record, so these two authors join the catalogue's existing Person records rather
than new ones. Before this submission HSSI held no Person record for any Longden, so she enters as a
new person.

Considered and rejected:
- **Bruce Fritz** (ORCID `0000-0003-0588-8558`, NRL) and **Kate A. Zawdie** (NRL) — co-authors of the
  reference paper, and creators of the boundary data sets in Field 28. Neither appears in any
  software-metadata source (Zenodo creators, `LICENSE`, `pyproject.toml`, `docs/citing.rst`, or the
  paper's own bibliography entry for the software), and neither has a commit. They are paper
  co-authors, not software authors (rule 7). The paper's author-contribution statement does list
  Fritz under "Software" alongside Burrell and Longden. That credit was weighed and is not enough: no
  software-metadata source and no commit names him. It is recorded so a later refresh weighs it rather
  than rediscovers it; if the project's own creator list ever adds him, rule 8 would make him an
  author.
- **Larry J. Paxton** — named in the paper's acknowledgements as GUVI principal investigator; a data
  acknowledgement, not authorship.

### 7. Software Name (MANDATORY)
pyIntensityFeatures

The project's own name, spelled the same way in every project source: the README and docs prose, the
docs title ("Welcome to the pyIntensityFeatures documentation"; `project = 'pyIntensityFeatures'` in
`docs/conf.py`), the `pyproject.toml` and `setup.cfg` distribution name, the GitHub repository name,
and the curated PyHC registry `name:` (Field 7 rule 8). Rejected: the Zenodo/DataCite title
`aburrell/pyIntensityFeatures: Version 0.2.0`, which is the integration's generated `<owner>/<repo>:
<release name>` locator (rule 1), and PyPI's normalised lower-case file names
(`pyintensityfeatures-0.2.0…`), which are a distribution-tool convention, not the project's spelling.

### 8. Description (MANDATORY)
pyIntensityFeatures is a Python module that identifies features in imager intensity data. It currently supports the identification of the Auroral Luminosity Boundaries (ALBs). This package is designed to be data source agnostic and uses a fitting method based on Longden et al. (2010) to identify the poleward and equatorward ALBs. Current support focuses on satellite-based imagers.

The README's lead paragraph under its "Overview" heading (Field 8 rule 7; there is no `CITATION.cff`),
unwrapped to single spaces between sentences. It says what the software does (identifies features in
imager data; auroral luminosity boundaries today), how (a fitting method), its stated assumption (data
source agnostic, with support focused on satellite-based imagers), and every capability it names is in
the code (Field 4).

**The citation year is corrected to 2010; every other word is the README's.** The README writes
"Longden et al. (2009)", but the paper it means is Longden et al., *Annales Geophysicae* 28, 1659–1678,
published 2010 (`https://doi.org/10.5194/angeo-28-1659-2010`), and the project itself cites it as 2010
everywhere else — `docs/citing.rst` line 56 and eight docstring mentions across `_main.py`,
`proc/boundaries.py`, `proc/fitting.py` and `utils/checks.py`. Quoting the README's "(2009)" verbatim
was considered and rejected: fidelity to a typo would send a reader looking for a 2009 paper that does
not exist, against the project's own consistent citation. This is a settled decision, not drift to be
"restored" from the README on a later refresh; if the README is corrected upstream, the description
matches it verbatim.

Considered and not used: the `pyproject.toml`/GitHub summary ("Identify features, such as auroral
luminosity boundaries, in imager data"), which is a one-line summary better suited to Field 9; the
`docs/overview.rst` paragraph, which says the same thing in fewer words and carries typos
("identificaiton", "obsrevations"); and the DataCite description of the concept DOI, which is the v0.2.0
release body ("A new beta release with updated citation information…"), not a description of the
software.

### 9. Concise Description (OPTIONAL)
A tool to identify features, such as auroral luminosity boundaries, in imager data.

The curated PyHC registry `description:` (`_data/projects.yml`), 83 characters (Field 9 rule 6). Field
8's opening sentence ("…identifies features in imager intensity data.") is true but does not say what
distinguishes the software — the aurora appears only in the second sentence — so a one-line preview
that names auroral luminosity boundaries serves a scanning user better. The `pyproject.toml`
`description` and GitHub repository description ("Identify features, such as auroral luminosity
boundaries, in imager data") are a near-identical rendering of the same sentence; choosing between them
changes nothing for a reader, and the registry's is first in the rubric's order.

### 10. Publication Date (RECOMMENDED)
2025-03-25

The first public release (Field 10 rule 4, anchor (a)): GitHub release `v0.0.1` "Alpha Release",
`published_at` 2025-03-25T21:54:01Z, whose body reads "Public version of private alpha release." The
GitHub repository was created the same day (`created_at` 2025-03-25T20:34:41Z). Later anchors are
corroboration, not alternatives: the first PyPI upload is 0.1.0 on 2025-03-28 and the first Zenodo
deposit (v0.1.0) is dated 2025-03-28.

Considered and rejected: **2024-03-01**, the date of the `v0.0.1` tag's commit, of the repository's
first commit (`ea5de06`), and of the CHANGELOG entry headed "0.0.1 (2024-03-01)" ("Alpha Release"). The code was
private until the repository was created on GitHub in March 2025 — the release text itself calls
v0.0.1 the public version of a *private* alpha — so 2024-03-01 is not a date on which the software was
publicly available. Anchor (b) (repository creation with a same-day first commit) does not hold either,
because the first commit predates the repository by a year; it would give the same 2025-03-25 date
anyway via the release.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Field 2 is a Zenodo DOI, so the publisher is Zenodo (Field 11 rule 1); DataCite's `publisher` for the
concept DOI is "Zenodo". Zenodo has no ROR, and CERN's ROR identifies the operator, not the repository,
so the identifier is Zenodo's own URL (rule 7). HSSI's existing Organization record for Zenodo carries
exactly this name and identifier. PyPI, where the package is also published, is a distribution channel
and never the publisher (rule 6).

### 12. Version (RECOMMENDED)
- **Version Number:** 0.2.0
- **Version Date:** 2026-03-20
- **Version Description:**

  A new beta release with updated citation information and bug fixes found when using the package to perform mission planning.

  - Updated supported Python and scipy versions
- **Version PID:** https://doi.org/10.5281/zenodo.19135203

**Number.** The newest release (Field 12 rule 5): tag `v0.2.0`, an ancestor of — in fact equal to — the
source revision; GitHub release "Version 0.2.0"; PyPI 0.2.0 (wheel and sdist uploaded
2026-03-20T15:34Z, not yanked); `pyproject.toml` and `setup.cfg` declare 0.2.0 at the tag. The release
history is `v0.0.1` (GitHub release only), `v0.1.0` and `v0.2.0` (GitHub release, PyPI and Zenodo
each); no pre-release exists and no tag is off the pinned lineage. The number is written without the
tag's `v`, as the package metadata and PyPI write it; the tag form `v0.2.0` is equally correct and is
not a reason to change the value later.

**Date.** The GitHub release `published_at` 2026-03-20T15:36:34Z (rule 7). PyPI's upload (15:34Z), the
Zenodo deposit and the CHANGELOG heading "0.2.0 (2026-03-20)" all agree.

**Description.** Taken from the release body (the release name "Version 0.2.0" adds nothing to the
tag; rule 13), trimmed to whole items a user cares about (rules 14–15). The body is:

> A new beta release with updated citation information and bug fixes found when using the package to
> perform mission planning.
>
> Summary
> =======
> - Updated supported Python and scipy versions
> - Improved citations and documentation
> - Expanded unit tests

Kept: the lead sentence, which reports user-facing bug fixes (an item is kept or dropped whole, so its
mention of citation information stays), and "Updated supported Python and scipy versions" (supported
platforms changed). Dropped: "Improved citations and documentation" (documentation housekeeping) and
"Expanded unit tests" (test housekeeping). The "Summary" heading is dropped with them: with one bullet
left under it, it would only render as an oversized heading in the page's Release Notes. The
CHANGELOG's fuller 0.2.0 list was not used, because the release body comes first in the source order
and is the project's own summary for users.

**PID.** The v0.2.0 version DOI, identified by DataCite version `v0.2.0` and `IsSupplementTo
…/tree/v0.2.0` (rule 17). Not the concept DOI (Field 2) and not the v0.1.0 version DOI
(`10.5281/zenodo.15102101`) that `docs/citing.rst` still cites.

### 13. Programming Language (RECOMMENDED)
- Python 3.x

A pure-Python package (Field 13 rule 4): every source file in the package is `.py`, `pyproject.toml`
declares `requires-python = ">=3.10"` with Python 3.10–3.14 classifiers, and PyPI publishes only a
`py3-none-any` wheel. No Python 2 target exists (rule 5). The rest of the tracked tree is
documentation (reStructuredText, Markdown, a Sphinx `conf.py` and `Makefile`), configuration and
packaging files (TOML, CFG, YAML, JSON, `MANIFEST.in`) and PNG figures — none of which adds a language
row.

### 14. Reference Publication (OPTIONAL)
https://doi.org/10.1029/2025JA034230

Burrell, A. G., Chisham, G., Longden, N., Fritz, B., & Zawdie, K. A. (2025). "Automated Identification
of Auroral Luminosity Boundaries Using pyIntensityFeatures." *Journal of Geophysical Research: Space
Physics*, 130(9), e2025JA034230 (title and volume from Crossref).

The project's own citation guidance names this one paper for the software (Field 14 rule 3):
`.zenodo.json` `notes` say "When referencing this package, please cite both the package DOI and the
pyIntensityFeatures journal article", giving this DOI, and `docs/citing.rst` lists it first with its
BibTeX entry. The paper presents the package by name in its title and describes its method. It is
therefore not also listed in Field 27 (rule 9).

Considered and not used here: Longden et al. (2010), the method paper the package builds on — a method
paper, not a description of this software (rule 5); it is Field 27. The EGU General Assembly 2025
abstract of the same title (`10.5194/egusphere-egu25-12327`) is a meeting abstract, never eligible
(rule 2).

### 15. License (RECOMMENDED)
BSD 3-Clause "New" or "Revised" License

The `LICENSE` file at the source revision is the three-clause BSD text: retain the copyright notice in
source, reproduce it in binary distributions, and the no-endorsement clause ("Neither the name of ocbpy
nor the names of its contributors may be used to endorse or promote products…"). The no-endorsement
clause is what makes it 3-Clause rather than 2-Clause (Field 15 rule 3). It names "ocbpy", the lead
author's earlier package, because the text was carried over from that project: at the first commit the
file opened with ocbpy's own copyright line, "Copyright (c) 2017, Angeline G. Burrell (AGB) and Gareth
Chisham (GC)". The slip does not change the licence. The terms have been the same since the first
commit; the only change (commit `809991e`, 2025-02-20) updated the copyright line to "Copyright (c)
2025, Angeline G. Burrell (AGB), Gareth Chisham (GC), and Nicola Longden (NL)".

**Rejected readings, recorded so the field is not "corrected" from them:**
- Zenodo licence id `bsd-license`, which DataCite renders as "BSD 1-Clause License" (`rightsIdentifier`
  `bsd-1-clause`) — a hand-set deposit label that the file contradicts.
- SoMEF's detection of `BSD-2-Clause` — wrong for a file that carries the no-endorsement clause.
- GitHub's `NOASSERTION` and the unversioned trove classifier `License :: OSI Approved :: BSD License`
  — neither names a BSD variant; PyPI's `license` field holds the full file text.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- aurora
- aurora australis
- aurora borealis
- boundaries
- imager
- ionosphere
- heliophysics
- magnetosphere
- northern lights
- southern lights
- features
- intensity
- auroral oval
- auroral luminosity boundaries
- pyhc package

**Project-declared (rule 9).** The first twelve are the project's own keywords: `pyproject.toml`
`keywords` and `.zenodo.json` `keywords` declare the same twelve terms (in slightly different orders),
and DataCite carries them as the deposits' `subjects`. None is excluded by rules 2–4. Two points are
noted so a later refresh does not second-guess them: `heliophysics`, `boundaries`, `features` and
`intensity` are broad, but rules 6–7 govern only terms an extractor proposes, not terms the project
declares; and `magnetosphere`, which appears in the project only in these two keyword lists, is kept
because the project declares it and the reference paper ties the boundaries to magnetospheric
structure (the poleward boundary as a proxy for the open–closed field line boundary). That is a
reason for a keyword, not for a Field 5 region (see Field 5). The repository has no GitHub topics.

**Added domain terms (rule 10).** `auroral luminosity boundaries` is the software's signature product
and the project's own term for it (README, docs, the reference paper's title); `auroral oval` is what
the boundaries delimit (`docs/overview.rst`: "the poleward and equatorward edges of the auroral oval").
Both are terms a searcher would type to find this software.

**PyHC package marker (rule 15).** The package is listed in the PyHC registry's `_data/projects.yml`,
so it carries `pyhc package`.

**Row binding (rules 11–12).** At extraction (2026-11-03) live Keyword rows already existed for
`aurora`, `aurora borealis`, `ionosphere`, `heliophysics`, `magnetosphere`, `northern lights`,
`southern lights`, `auroral oval` and `pyhc package`, and these bind them. The live list also holds a
misspelled `norther lights` row, which is not the row to bind. `aurora australis`, `boundaries`,
`imager`, `features`, `intensity` and `auroral luminosity boundaries` had no row in any case, separator
or plural variant before this submission, so they enter the vocabulary as new lower-case rows.

Considered and rejected:
- PyHC registry tags `specific` (scope tag, rule 2), `data_analysis` (restates Field 4) and
  `ionosphere_thermosphere_mesosphere` (the domain test passes, but the underscore machine spelling is
  never added as a new keyword, and `ionosphere` already carries the term).
- `python` (catalogue-wide generic, rule 7) and the reference paper's publisher keywords
  `auroral boundaries`, `auroral imagers`, `boundary identification`, `data processing` — near-variants
  of terms already recorded or restatements of Field 4.
- `GUVI`, `SSUSI`, `TIMED`, `DMSP` — instrument and mission names used only in worked examples and the
  reference paper's demonstration (see Fields 31/32); not added as keywords for the same reason.
- `open-closed boundary` — the software does not compute it; it is a downstream use of the poleward
  boundary.

### 17. Data Sources (OPTIONAL)
Not found — evidenced empty

The package reaches no data source of any kind (Field 17 rule 11): users hand `AuroralBounds` an
in-memory data object they have already loaded. A sweep of the package
(`git grep -P -i 'urlopen|urlretrieve|requests\.|ftplib|https?://'` over `pyIntensityFeatures/` at the
source revision) finds one hit, a URL in a comment in `tests/test_utils_distributions.py`; the same
pattern over the whole tree finds URLs in the CI workflows, `.readthedocs.yml`, the README and other
documents (positive control). The package's imports are the standard library, numpy, pandas, scipy,
xarray, aacgmv2 and the optional apexpy — no HTTP, FTP or archive client.

Considered and rejected:
- **CDAWeb / HTTP/HTTPS Directories** — the README and `docs/examples/ex_pysat.rst` download TIMED/GUVI
  data, and the reference paper obtained GUVI and SSUSI data from NASA SPDF, but in every case through
  pysat and pysatNASA (rule 4). That pairing is recorded in Field 30.
- **Observatory/Mission-specific** — the package is data-source agnostic and reads no mission's
  archive; Fields 31/32 are empty for the same reason.

### 18. Input File Formats (RECOMMENDED)
Not found — evidenced empty

The package opens no file (Field 18 rule 9). It takes an in-memory object — `pysat.Instrument`,
`xarray.Dataset`, `pandas.DataFrame` or a dict of arrays — and `AuroralBounds._get_variable` reads each
named variable as an attribute or a key. No format library is imported, and a sweep of the installed
package for `hdf5|netcdf|\bcdf\b|csv|json|zarr` finds nothing; the only hits for the broader pattern
`fits` are the word "fits" in the sense of Gaussian fits (12 lines in four modules). The package has no
`open()` call. The TIMED/GUVI netCDF files of the documented example are read by pysat/pysatNASA, not
by this package (rule 2).

### 19. Output File Formats (RECOMMENDED)
Not found — evidenced empty

The package writes no file (Field 19 rule 9). A write-path sweep of the package
(`git grep -P '\.(to_\w+|writeto|save\w*|dump)\s*\(|savefig|VideoWriter|open\([^)]*['"]w'`) finds one
match, `pyIntensityFeatures/utils/coords.py:157` (`pds.to_datetime`), which shows the pattern fires
on this scope and is a time conversion, not a write. The result is returned in memory as the
`boundaries` attribute, an `xarray.Dataset`.

**netCDF considered and not recorded (rule 5).** The README says "You can then save the data as a
NetCDF using the built-in xarray Dataset method" (`docs/examples/ex_pysat.rst` says the same with a
Sphinx cross-reference), and adds that the `set_boundaries` keyword values are stored as Dataset
attributes "to ensure reproducibility". The file
is nonetheless written by xarray at the caller's choice, and the attributes the package adds are its
own processing parameters (`min_mlat_base`, `mag_method`, `mlat_inc`, `mlt_inc`, `un_threshold`,
`lt_out_bin`, `max_iqr`), not netCDF-specific metadata such as CF `units`, `long_name` or `Conventions`
(a sweep for `units`, `long_name` and `Conventions` across the package, tests included, returns
nothing). An `xarray.Dataset` returned without format-specific metadata is the rule's base case, not
its exception. The netCDF boundary files the
authors published (Field 28) were written this way, by their own processing around the returned
Datasets. **Condition for revisiting:** a writer function in the package, or format-specific metadata
built into the returned Dataset, would make `netCDF3/4` an output format.

### 20. Operating System (RECOMMENDED)
- Operating System Independent
- Linux
- Mac
- Windows

A pure-Python package with no compiled extension and no OS restriction (Field 20 rule 3) →
`Operating System Independent`, plus each OS the project names and tests: the classifiers
`Operating System :: POSIX :: Linux`, `Operating System :: MacOS :: MacOS X` and
`Operating System :: Microsoft :: Windows`, and the CI matrix in `.github/workflows/main.yml`, which runs
the test suite on `ubuntu-latest`, `windows-latest` and `macos-latest`. The one compiled dependency,
aacgmv2, is a separate package whose platform support is its own (rule 5).

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Pure interpreted code (Field 21 rule 3): PyPI publishes only `pyintensityfeatures-0.2.0-py3-none-any.whl`
and an sdist, and the package builds nothing. The macOS CI runner does not add an arm64 row, and no
GPU or cluster code exists (rules 6–7).

### 22. Related Phenomena (OPTIONAL)
Not found — evidenced empty

The seven live rows were each examined: `Coronal Heating`, `Coronal Mass Ejections`, `Solar Corona`,
`Solar Flares`, `Solar Wind` and `X-ray emission` have no connection to an auroral-boundary tool.
`Geomagnetic Storms` is rejected: the software locates auroral boundaries at every activity level and
computes no storm diagnostic; the reference paper mentions storm-time expansion of the auroral oval
only to explain why the example uses a 45° latitude limit (rules 5–6). The phenomenon the software
genuinely addresses — the aurora — has no row, so it is carried by Keywords (`aurora`, `auroral oval`)
under rule 1.

### 23. Development Status (RECOMMENDED)
Active

Dated anchors: the last commit on the default branch `main` is `72e6e1d` on 2026-03-20 (the `v0.2.0`
release commit), and the last release is v0.2.0 on 2026-03-20. The software has reached a stable,
usable state — three tagged releases, two on PyPI, a peer-reviewed description, and two published data
sets produced with it. No status badge, move notice or archive flag exists (rules 1–4). At extraction
(2026-11-03) the last commit was between 6 and 24 months old, and for software entering HSSI for the
first time that band gives `Active` (rule 6). A later refresh should re-apply rule 6 from these dates: with no further commit,
`Inactive` from 2028-03-20.

Not used as status evidence: the release text's "beta release", the trove classifier
`Development Status :: 3 - Alpha` and the docs' `0.2.0-beta` release string are maturity labels, not
repostatus terms, and none states that work is in progress toward a first usable release.

### 24. Documentation (RECOMMENDED)
https://pyintensityfeatures.readthedocs.io/en/latest/

The project's own Read the Docs site (Field 24 rule 3), named in `pyproject.toml` `[project.urls]
Documentation` and built from the repository's `.readthedocs.yml` and `docs/`. It resolves directly,
with no redirect; its title is "Welcome to the pyIntensityFeatures documentation — pyIntensityFeatures
0.2.0-beta documentation", and it includes an installation page. Recorded in the declared, query-free
form (rule 6). Considered: the README badge's `http://pyIntensityFeatures.readthedocs.io/en/latest/?badge=latest`
(redirects to the https form) and the PyHC registry's
`https://pyintensityfeatures.readthedocs.io/en/latest/?badge=latest` — the same page with a badge
query string. The repository has no wiki.

### 25. Funder (OPTIONAL)
Not found — evidenced empty

No source attributes funding to the software or to a project whose product it is (Field 25 rule 12):
- `ACKNOWLEDGEMENTS.rst`: "A.G.B was supported by the Office of Naval Research (ONR)." — support of a
  person (rule 3).
- `.zenodo.json` has no `grants`, and DataCite `fundingReferences` is empty for every deposit.
- The reference paper's Acknowledgments: "AGB, BF, and KAZ are supported by the Office of Naval
  Research. GC is supported as part of the British Antarctic Survey (BAS) Polar Science for a
  Sustainable Planet Programme, funded by the UK Natural Environment Research Council (NERC). The GUVI
  data used here are provided through support from the NASA MO&DA program…" — person-level support
  (rule 3) and the funding of input data (rule 5). The paper's Data Availability Statement names no
  funder.
- The two boundary data sets (Field 28) acknowledge that their creators "were supported by the Office
  of Naval Research (ONR)" — again support of people.

Crossref's funder block for the paper lists the Office of Naval Research and the British Antarctic
Survey; those are the paper's person-level funders, recorded here as rejected so a later refresh does
not import them from Crossref. (Were a qualifying statement to appear, the United States Office of
Naval Research is `https://ror.org/00rk2pe57`.)

### 26. Award Title (OPTIONAL)
Not found — evidenced empty

No award number or award title appears in any project file, DOI record, or the reference paper's
acknowledgements (Field 26 rule 8), and the funding statements that exist are person-level (Field 25).

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.5194/angeo-28-1659-2010

Longden, N., Chisham, G., Freeman, M. P., Abel, G. A., & Sotirelis, T. (2010). "Estimating the location
of the open-closed magnetic field line boundary from auroral images." *Annales Geophysicae*, 28,
1659–1678 (title, authors and pages from Crossref).

**The method paper the package implements (rule 4).** The project presents it as the basis of the
software in every place it describes the method: `docs/citing.rst` lists it as the one entry under its
"References" heading, introduced as "Important publications that have contributed to this package"; the
reference blocks of
`AuroralBounds.set_boundaries`, three functions in `proc/boundaries.py` and `utils/checks.py` cite it;
and the reference paper says the method "is based on that developed for the Imager for
Magnetopause-to-Aurora Global Exploration (IMAGE) observations (Longden et al., 2010)" and lists how the
package's version differs. It is the only method paper the project cites, so the list stays useful.

Considered and not added:
- **The reference paper** (`10.1029/2025JA034230`) — it is Field 14 and is never listed here too
  (rule 2).
- **EGU General Assembly 2025 abstract** "Automated Identification of Auroral Luminosity Boundaries
  using pyIntensityFeatures" (Burrell, Chisham, Longden and Zawdie; `10.5194/egusphere-egu25-12327`) —
  a meeting abstract, never eligible (rule 1).
- **Chisham, Burrell, Thomas & Chen (2022)**, "Ionospheric Boundaries Derived From Auroral Images", JGR
  (`10.1029/2022JA030622`) — cited by the reference paper as earlier boundary work, but the project's
  own files do not present it as a basis of the software, and its full text does not name
  pyIntensityFeatures (rule 6).
- **Chisham, Burrell & Zawdie (2025)**, "The Impact of Adaptive High-Latitude Coordinates",
  GRL (`10.1029/2025GL115265`) — uses SSUSI luminosity boundaries, but its full text does not name
  pyIntensityFeatures, so it gives the software no deliberate credit (rule 6). Should a later version
  credit the software, it would qualify under rule 5.
- **Moré et al. (1984)** and **Virtanen et al. (2020)** (`10.1038/s41592-019-0686-2`), cited in the
  reference paper because the fitting uses `scipy.optimize.leastsq`, SciPy's wrapper for MINPACK —
  generic numerical methods and software (rule 4's exclusion).

Search behind the field: ADS full-text `full:"pyIntensityFeatures"` returns exactly three records (the
reference paper, the EGU abstract and the v0.1.0 software deposit; a nonsense-token control returns
0); ADS and OpenAlex both reported no paper citing the reference paper as of 2026-11-03, while the
same ADS citation query does return the citations of another paper (control); and DataCite held no
relation pointing at the software's DOIs from any record other than its own deposits. Uses of the
software are news while they are this few, so a later refresh should re-run these searches and apply
rule 5 to anything new.

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.5281/zenodo.22238095
- https://doi.org/10.5281/zenodo.22258433

**Data sets produced with the software (rule 5).** Both are Zenodo data releases by the software's lead
author whose descriptions state that they were "processed using pyIntensityFeatures
(https://doi.org/10.5281/zenodo.15102100)":
- `10.5281/zenodo.22238095` — **GUVI Auroral Luminosity Boundary Files**, version 1.0.0, issued
  2026-09-01 (creators Angeline Burrell and Kate Zawdie, NRL): auroral luminosity boundary locations
  from TIMED/GUVI for 2002–2007, one netCDF file per day, hemisphere and LBH channel, made from the
  GUVI SDR disk data at NASA SPDF.
- `10.5281/zenodo.22258433` — **SSUSI Auroral Luminosity Boundary Files**, version 1.0.0, issued
  2026-09-02 (creators Angeline Burrell, Bruce Fritz and Kate Zawdie, NRL): the same product from the
  DMSP SSUSI imagers on F16–F19.

Each value is the record's concept DOI: DataCite gives each a `HasVersion` relation to its single
version so far (`10.5281/zenodo.22238096` and `10.5281/zenodo.22258434`), and Zenodo reports these as
the `conceptdoi` of those versions; a concept DOI follows later releases, so rule 6's newest-release
selection does not arise. Both are typed `Dataset`. They answer the reference paper's Data Availability
Statement ("The boundaries produced in this project may be reproduced exactly using
pyIntensityFeatures").

**Considered and not selected: the TIMED/GUVI SDR imaging data of the README and docs example, and the
GUVI and SSUSI SDR data the paper processed.** The package reads neither — pysat and pysatNASA load
them — and it is data-source agnostic, so these are inputs of a worked example and of the paper, not
data sets the software is built to read. Reading the docs example as rule 3's "documented input" was
weighed and rejected: the README presents the GUVI walk-through as a "template" for "your own data
set", the same example-only status that keeps GUVI out of Fields 31/32, and listing it would imply a
specialisation the software disclaims. The GUVI and SSUSI association is carried instead by the two
boundary data sets recorded above, which the software did produce.
Other SSUSI data sets found at DataCite (scintillation, data-assimilation and storm studies) are
unrelated to this software.

### 29. Related Software (OPTIONAL)
- https://github.com/aburrell/aacgmv2
- https://github.com/aburrell/apexpy

**Domain-specific dependencies whose presence characterises the software (rule 9).**
- **aacgmv2** — a required dependency (`pyproject.toml` `dependencies`) to which the package delegates
  its coordinate science: `utils.coords.convert_geo_to_mag` calls `aacgmv2.get_aacgm_coord_arr`, and
  AACGM-v2 magnetic latitude and MLT are the default coordinates of every boundary the package
  returns (`mag_method='ALLOWTRACE'`, an AACGM-v2 method flag). The reference paper names AACGMV2 as the
  conversion used for its examples.
- **apexpy** — the optional dependency (the `apex` extra; `docs/installation.rst` lists "apexpy
  (optional)") that supplies the alternative apex and quasi-dipole coordinates selectable through
  `mag_method='apex'` or `'qd'`; the CI matrix runs a dedicated apexpy integration job.

URL form (rules 11 and 13): both are catalogue entries, so each value is that entry's stored code
repository URL, byte for byte — the AACGMv2 and ApexPy entries store
`https://github.com/aburrell/aacgmv2` and `https://github.com/aburrell/apexpy`. Their concept DOIs, passed over because the site renders a
related item as its raw URL and a repository URL reads as the package's name, are
`10.5281/zenodo.1212694` (aacgmv2) and `10.5281/zenodo.1214206` (apexpy).

Considered and rejected:
- **numpy, scipy, pandas** — Tier A generic infrastructure (rule 1); `scipy.optimize.leastsq` does the
  fitting and pandas handles times, which says nothing distinctive.
- **xarray** — Tier B; recorded in Field 30 on its documented interchange, and with no separate Field 29
  ground (rule 3).
- **pysat and pysatNASA** — the relationship is the documented data handoff, which is Field 30's; there
  is no Field 29 ground of their own (rule 3).
- **ocbpy** (`https://github.com/aburrell/ocbpy`) — the lead author's package for boundary-adjusted
  coordinates, the natural consumer of poleward boundaries. Its only appearance in this repository is
  the name left in the `LICENSE` no-endorsement clause by copying the licence text; the package never
  imports or refers to it, so there is no relation from this software's own sources (rule 4).
- **The original implementation behind Longden et al. (2010)** — the reference paper says the method
  "was originally developed for the Imager for Magnetopause-to-Aurora Global Exploration (IMAGE)
  observations", but no source names or links a public code release of that earlier implementation;
  recorded so a later refresh re-checks only if one is published.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/pysat/pysat
- https://github.com/pysat/pysatNASA
- https://github.com/pydata/xarray

**pysat — a documented interchange object (rule 7).** The `AuroralBounds` docstring names
`pysat.Instrument` as an accepted `inst_data` type, and the documentation's "Using pysat Data" page
(`docs/examples/ex_pysat.rst`, repeated in the README) is the package's main worked example: a loaded
pysat `Instrument` is passed straight into `AuroralBounds`, the variables are read from it by name, and
pysat's `custom_attach` mechanism is used to prepare a single-channel intensity variable for it. The
example's printed output shows the class reporting the pysat Instrument it holds. The value is the
pysat catalogue entry's stored code repository URL; its concept DOI is `10.5281/zenodo.1199703`.

**pysatNASA — one package's output imported into the other (rule 7).** The same worked example obtains
TIMED/GUVI `sdr-imaging` data through `pysatNASA.instruments.timed_guvi` and hands the resulting
Instrument to `AuroralBounds`; the docs say that pysatNASA "provides access to the TIMED GUVI data
through CDAWeb", and the reference paper's Data Availability Statement says the GUVI and SSUSI data
"were accessed for this project using pysatNASA". pysatNASA had no catalogue entry at extraction; the value
is its upstream repository root (GitHub `full_name` `pysat/pysatNASA`), a URL the catalogue already uses
for other entries' relations. Its concept DOI is `10.5281/zenodo.3986131`.

**xarray — the public API's documented interchange type (rule 4, Tier B).** The result is returned as
an `xarray.Dataset` (`AuroralBounds.boundaries`, documented as "Dataset with Auroral Luminosity
Boundaries"), built by `utils.output.convert_boundary_dict`, and the README and docs show the printed
Dataset and tell users to save it with the Dataset's own method; `xr.Dataset` is also an accepted input
type, with a dedicated comparison branch in `AuroralBounds.__eq__`. xarray had no catalogue entry at
extraction; the value is the upstream repository root, and its concept DOI is `10.5281/zenodo.598201`.

Considered and rejected:
- **pandas** — `pds.DataFrame` is also an accepted input and has its own `__eq__` branch, but pandas is
  Tier A and no evidence rehabilitates it (rule 1).
- **numpy, scipy, matplotlib** — Tier A; matplotlib appears only in a documentation example.
- **aacgmv2 and apexpy** — used internally for coordinate conversion with no documented exchange of
  objects with the user; recorded in Field 29 only (rule 9).
- **Inbound sweep** — no HSSI record's related or interoperable software pointed at this repository or
  at any of its three DOIs at extraction (checked against every related-item identifier in the
  catalogue), so no reverse relation awaited a reciprocal entry.

### 31. Related Instruments (OPTIONAL)
Not found — documented omission

**The package is instrument-agnostic (Field 31 rule 2).** The README states that it is "designed to be
data source agnostic", the one class accepts any data object with the named variables, and the code
contains no reader, calibration or branch for any instrument: a word-anchored sweep of the package for
`guvi|ssusi|timed|dmsp|image|wic|lbh` finds only the generic phrase "auroral image" in docstrings and a
single docstring that still says "Convert and reshape GUVI location output" on the general coordinate
function `utils.coords.convert_geo_to_mag`; the tests contain none of these names. GUVI appears as the
README's and docs' worked example (rule 3), and the reference paper demonstrates the method on GUVI and
SSUSI and tuned the default number of Gaussian peaks on those two data sets — an otherwise-agnostic
tool "commonly used with" them (rule 4). The instruments' association with this software is carried
instead by the boundary data sets in Field 28.

Rows that exist and are deliberately not used, so a later refresh sees a relevance decision rather than
a lookup failure:
- `Global Ultraviolet Imager` — `https://spase-metadata.org/SMWG/Instrument/TIMED/GUVI`
- `DMSP/F16, SESS Special Sensor Ultraviolet Limb Imager, SESS/SSUSI` (and its F17, F18, F19 and S20
  siblings) — `https://spase-metadata.org/SMWG/Instrument/DMSP_5D-3/F16/SESS/SSUSI` and siblings
- `Far Ultraviolet Imager` (IMAGE/FUV; the original Longden et al. 2010 method was developed on "FUV
  images recorded by the IMAGE satellite") — `https://spase-metadata.org/SMWG/Instrument/IMAGE/FUV`

Sweep: the production vocabulary (every row SPASE-identified as of 2026-11-03) was searched on `name`,
`abbreviation`, `identifier` and `definition` for `GUVI`, `SSUSI`, `WIC`, `Wideband Imaging Camera`,
`Far Ultraviolet Imager` and `TIMED`; `SUVI` (four GOES rows) served as the positive control and a
nonsense token returned nothing.

### 32. Related Observatories (OPTIONAL)
Not found — documented omission

Same decision as Field 31: the package targets no mission or platform. Rows that exist and are
deliberately not used: `Thermosphere-Ionosphere-Mesosphere Energetics and Dynamics` —
`https://spase-metadata.org/SMWG/Observatory/TIMED`; `Defense Meteorological Satellite Program,
DMSP-F16` through `DMSP-F19` — `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-3/F16` and
siblings; `Imager for Magnetopause-to-Aurora Global Exploration` —
`https://spase-metadata.org/SMWG/Observatory/IMAGE`. Field 17 accordingly carries no
`Observatory/Mission-specific` value.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/aburrell/pyIntensityFeatures/72e6e1de8dd439ea9e152ac58d8fc93e8f1bffc4/docs/figures/pyIntensityFeatures_logo.png

**The project's own logo (rule 2), presented three ways:** `docs/conf.py` sets
`html_logo = …/figures/pyIntensityFeatures_logo.png` (with `logo_only`), the README's header shows the
same file beside the "Overview" title with the alt text "Snakes marking the boundaries of the auroral
oval" and the title "pyIntensityFeatures logo", and the PyHC registry's `logo:` names it. The image is a
circular emblem with the wordmark "pyIntensityFeatures" over an imager swath of auroral intensity, with
two snake shapes marking the poleward and equatorward boundaries.

**URL form (rule 7).** Pinned to the source revision; the file has been unchanged since the repository's
first commit (`ea5de06`), and no `.gitattributes` exists, so it is not LFS-tracked. Verified: the
pinned URL returns `image/png`, 201,114 bytes, a 2560 × 1920 PNG whose SHA-256
(`68f33b4285c7e96be6314889c9fd2b02bd2853d900988fffc8c88a68dd718e71`) equals the tracked blob's; the URL
is 145 characters. Not used: the registry's and README's branch-referenced
`https://raw.githubusercontent.com/aburrell/pyIntensityFeatures/refs/heads/main/docs/figures/pyIntensityFeatures_logo.png`,
which serves the same file today but would break silently if the file moved (rules 7 and 12).
