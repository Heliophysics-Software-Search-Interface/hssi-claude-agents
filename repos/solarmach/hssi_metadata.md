# HSSI Metadata Extraction Results

**HSSI Software ID:** c9f100c2-e502-4a61-94d5-87ae0f4d3646
**Repository:** https://github.com/jgieseler/solarmach
**Source Revision:** dbafa3b06e021c651df7ed41dc31649b441c8909
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-10-29
**Validation Status:** PASS
---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** To be filled by actual submitter
- **Submitter Email:** To be filled by actual submitter
- **Source:** Submitter information is intentionally deferred to the person who performs the submission.

### 2. Persistent Identifier (RECOMMENDED)
- **Persistent Identifier:** https://doi.org/10.5281/zenodo.7016783
- **Source:** Preserved from the existing HSSI record and confirmed as the Zenodo concept DOI by the Zenodo and DataCite APIs.

### 3. Code Repository (MANDATORY)
- **Code Repository:** https://github.com/jgieseler/solarmach
- **Source:** Preserved from the existing HSSI record and confirmed by `CITATION.cff`, `pyproject.toml`, and the GitHub repository.

### 4. Software Functionality (RECOMMENDED)
- **Values:**
  - Coordinate Transforms
  - Coordinate Transforms:Heliospheric
  - Coordinate Transforms:Solar
  - Data Processing and Analysis
  - Data Processing and Analysis:Analysis
  - Data Processing and Analysis:Data Access and Retrieval
  - Data Processing and Analysis:Data Reduction
  - Data Processing and Analysis:Field-line Tracing
  - Data Processing and Analysis:Image Processing
  - Data Processing and Analysis:Processing
  - Data Visualization
  - Data Visualization:2D Graphics
  - Data Visualization:3D Graphics
  - Data Visualization:Line Plots
  - Data Visualization:Movies
  - Data Visualization:Orbit Plots
  - Data Visualization:Web-Based
  - Models and Simulations
  - Models and Simulations:Data Guided
  - Models and Simulations:Empirical
  - Models and Simulations:Field-line Tracing
  - Models and Simulations:Physics-Based
- **Source:** Repository code and the documented example notebook. Public APIs transform Carrington and Stonyhurst heliographic coordinates; retrieve ephemerides, solar-wind measurements, and GONG maps; process solar magnetogram maps; calculate Parker-spiral and PFSS magnetic connections; reduce measurements to hourly means; trace field lines; and produce tabular, 2D, interactive 3D, HTML, and animated-GIF outputs. Every selected subcategory includes its required parent category.

### 5. Related Region (RECOMMENDED)
- **Values:**
  - Interplanetary Space
  - Solar Environment
  - Corona
  - Photosphere
  - Solar Wind
- **Source:** Interplanetary Space and Solar Environment are preserved from the existing HSSI record and confirmed by the repository's heliospheric Parker-spiral and solar-coronal PFSS functionality.
- **Evidence, Corona:** The documented PFSS extension explicitly "connects the heliospheric magnetic field (HMF) to the solar corona" (`examples/example.ipynb:58640`).
- **Evidence, Photosphere:** `plot_pfss` tracks an open field line to the photosphere (`solarmach/__init__.py:1227`), `trace_field_line` documents the same endpoint (`solarmach/pfss_utilities.py:303-306`), and the user-facing results table labels its output as a magnetic footpoint at the photosphere (`solarmach/__init__.py:1822`).
- **Evidence, Solar Wind:** `get_sw_speed` retrieves measured solar-wind bulk speed (`solarmach/__init__.py:93`), which parameterizes the Parker-spiral model (`solarmach/__init__.py:428-431,669,675`). Solar Wind therefore describes a medium that the software measures and models, not merely one crossed by a connectivity line.

### 6. Authors (MANDATORY)
- **Author:** Jan Gieseler
  - **Author Identifier:** https://orcid.org/0000-0003-1848-7067
  - **Affiliation:** University of Turku
  - **Affiliation Identifier:** https://ror.org/05vghhr25
- **Author:** Nina Dresing
  - **Author Identifier:** https://orcid.org/0000-0003-3903-4649
  - **Affiliation:** University of Turku
  - **Affiliation Identifier:** https://ror.org/05vghhr25
- **Author:** Johan Lauritz Freiherr von Forstner
  (given name `Johan Lauritz`, family name `Freiherr von Forstner`)
  - **Author Identifier:** https://orcid.org/0000-0002-1390-4776
  - **Affiliation:** Institute of Experimental and Applied Physics, University of Kiel
  - **Affiliation Identifier:** Not found
  - **Affiliation:** Paradox Cat GmbH
  - **Affiliation Identifier:** Not found

**Name split and identifier.** An earlier revision of this file gave the given name
"Johan L. Freiherr von", family "Forstner", with no identifier — a split that put the nobiliary particle
chain "Freiherr von" in the given name. ORCID `0000-0002-1390-4776`, the author's own self-curated
record, gives `given-names` = "Johan Lauritz" and `family-name` = "Freiherr von Forstner", and its
**current** employment is "Paradox Cat, Machine Learning Engineer" — the very affiliation this entry
already stored, which is what identifies the two HSSI rows as one person rather than a name coincidence.
Both affiliations are retained: this author's record carries the union of the institutions any source
attributes to him, and an affiliation is never dropped in favour of a newer one.
- **Author:** Christian Palmroos
  - **Author Identifier:** https://orcid.org/0000-0002-7778-5454
  - **Affiliation:** University of Turku
  - **Affiliation Identifier:** https://ror.org/05vghhr25
- **Author:** Seve Nyberg
  - **Author Identifier:** https://orcid.org/0000-0003-2672-5491
  - **Affiliation:** University of Turku
  - **Affiliation Identifier:** https://ror.org/05vghhr25
- **Author:** Rami Vainio
  - **Author Identifier:** https://orcid.org/0000-0002-3298-2067
  - **Affiliation:** University of Turku
  - **Affiliation Identifier:** https://ror.org/05vghhr25
- **Source:** Identity-aware union of the existing HSSI authors with the API-representable current software authors in `CITATION.cff`, `.zenodo.json`, and the Zenodo v0.5.3 record. The University of Turku ROR was confirmed through the live HSSI organization record and the ROR API. The public ORCID record confirms that https://orcid.org/0000-0003-2672-5491 belongs to Seve Nyberg. No ROR match was found for Paradox Cat GmbH. The one-token username-style release creator `drazerd` is authoritative source credit but is not emitted as an HSSI author because the schema requires non-empty given and family names and no non-invented split is available.

### 7. Software Name (MANDATORY)
- **Software Name:** solarmach
- **Source:** Preserved from the existing HSSI record and confirmed by the repository, PyPI, Zenodo, and PyHC registry.

### 8. Description (MANDATORY)
- **Description:** solarmach is the Python package for Solar-MACH, a multi-spacecraft heliospheric configuration and magnetic-connectivity tool. It obtains spacecraft ephemerides from JPL Horizons, can retrieve measured solar-wind speeds for selected missions through Speasy, computes Parker-spiral backmapping in Carrington or Stonyhurst coordinates, and produces tabular, 2D polar, interactive 3D, and optional PFSS field-line results driven by GONG maps. When a measured solar-wind speed cannot be obtained, it uses a configurable default value.
- **Source:** Materially expanded from the short existing HSSI description using the README, public API docstrings, source code, and example notebook. The submitted wording and identity as the Solar-MACH Python package are preserved.

**The fallback sentence still holds at v0.5.7** (read at `cd4d8366d78b0029a1ad6f18f2efdc69f45a52ec`). It restates the `vsw_list` docstring of `SolarMACH` (`solarmach/__init__.py:471`), and `get_sw_speed` still returns `default_vsw` when Speasy is not installed, when a body has no supported solar-wind dataset, when no data are found, and, since v0.5.7, when AMDA refuses a query for missing credentials (`solarmach/__init__.py:141,232`). Since v0.5.4 it instead raises a `ConnectionError` asking for speeds through `vsw_list` when Speasy's CDA or AMDA inventory is unavailable (`solarmach/__init__.py:184,190`); before v0.5.4 that case raised an uncaught `AttributeError`, so the change does not narrow what the sentence describes, and the description is kept.

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Python package of the multi-spacecraft longitudinal configuration plotter Solar-MACH
- **Source:** Preserved verbatim from the existing HSSI record and confirmed by the current Zenodo record.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2022-03-14
- **Source:** GitHub API repository creation date. HSSI held `2025-01-29` until an earlier refresh replaced it; that date is the v0.5.0 release date rather than the software's initial publication. The first PyPI release followed on 2022-03-17.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** Preserved from the existing HSSI record and confirmed by the concept and version DOI metadata.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.5.7
- **Version Date:** 2026-10-27
- **Version Description:** Handle MissingCredentials exception in get_sw_speed function
- **Version PID:** https://doi.org/10.5281/zenodo.23696250

**Why v0.5.7** (Field 12 rule 3; read at `cd4d8366d78b0029a1ad6f18f2efdc69f45a52ec`, the head of the default
branch `main` and the commit the `v0.5.7` tag names). The annotated tags `v0.5.4` (`7a0d824`), `v0.5.5`
(`28d4d82`), `v0.5.6` (`cc70959`) and `v0.5.7` (`cd4d836`) lie on `main`'s own lineage:
`git merge-base --is-ancestor <tag> cd4d836` holds for each. Each has a GitHub release, named with the
bare number, that is neither a draft nor a pre-release, and PyPI's JSON API lists a `py3-none-any` wheel
and an sdist for each, none yanked, with `info.version` `0.5.7`. No later tag, release or upload existed
on 2026-10-29. The version is dynamic (`pyproject.toml` declares `dynamic = ["version"]` and
`[tool.setuptools_scm]`), so the tag sets it; at `v0.5.7` the fallback string in `solarmach/version.py`
and `CITATION.cff` both read `0.5.7`. At `v0.5.5` both still read `0.5.4`, because no commit in
`v0.5.4..v0.5.5` updates them; the tag, its GitHub release and its PyPI upload make 0.5.5 a release all
the same, and 0.5.6 followed it the same day. The number is written with a `v`, as the tags write it and
as the superseded value was stored; the GitHub release names and PyPI write it bare.

**Version Date** (rule 7). The GitHub release `v0.5.7` was published 2026-10-27T16:08:45Z; the tagged
commit is dated 2026-10-27T17:58:28+02:00 (15:58:28Z), PyPI's wheel was uploaded 2026-10-27T16:07:46Z,
and the Zenodo deposit's publication date, DataCite's `Issued` date and `CITATION.cff` `date-released`
are all 2026-10-27.

**Version Description** (rules 13–15). The release name is the bare number, so the text comes from the
release body, a list generated from `.github/release.yml` whose only item, under the "Bugfixes" heading,
is "Handle MissingCredentials exception in get_sw_speed function by @jgieseler in
https://github.com/jgieseler/solarmach/pull/113". The generator's comment line, the headings, the
item's trailing contributor-and-pull-request credit and the body's "Full Changelog" compare link are
dropped; the item's
own words are kept verbatim. The change it describes (`b1895b3`, pull request #113) adds Speasy's
`MissingCredentials` to the exceptions `get_sw_speed` catches (`solarmach/__init__.py:141,232`), so a
solar-wind query that AMDA refuses for missing credentials falls back to `default_vsw` instead of
raising. The project keeps no CHANGELOG file; `pyproject.toml` names its GitHub releases page as the
changelog (`pyproject.toml:68`).

**Version PID** (rule 17). `10.5281/zenodo.23696250` is v0.5.7's GitHub-integration deposit: its Zenodo
`metadata.version` and DataCite `version` are `v0.5.7`, it carries
`IsSupplementTo https://github.com/jgieseler/solarmach/tree/v0.5.7` and
`IsVersionOf 10.5281/zenodo.7016783`, the concept's `HasVersion` list includes it, and the DOI resolves.
`CITATION.cff` at `cd4d836` still writes `doi: 10.5281/zenodo.16882017`, the v0.5.1 deposit, so the
file's DOI is not used here.

**Releases between the superseded value and this one**, each superseded by v0.5.7 and not recorded:
0.5.4 (PyPI upload 2026-08-17, GitHub release published 2026-08-18, deposit 10.5281/zenodo.21989960),
and 0.5.5 and 0.5.6 (both 2026-10-12, deposits 10.5281/zenodo.23316451 and 10.5281/zenodo.23316716).

**Superseded values.** HSSI held v0.5.3 (release date 2026-03-27, Version PID
https://doi.org/10.5281/zenodo.19257728) until the v0.5.7 release update, and v0.5.0 before an earlier
refresh replaced it; the view API renders a version as `solarmach - <number>`, and that prefix is a
display transform, not part of the stored number. The v0.5.3 description, "Fixes GONG-map path
selection in PFSS analysis, PFSS plotting and reference-coordinate edge cases, and PFSS table value
typing; adds SOLAR-1 to the supported-spacecraft list; and refactors the GitHub Actions setup.", was a
summary composed from that release's items rather than the items themselves, which rule 15 does not
allow; nothing of it carries onto v0.5.7 (rule 10).

### 13. Programming Language (RECOMMENDED)
- **Values:**
  - Python 3.x
- **Source:** Preserved from the existing HSSI record and confirmed by `pyproject.toml`, PyPI classifiers, and GitHub language metadata. The current project requires Python 3.11 or newer.

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication:** https://doi.org/10.3389/fspas.2022.1058810
- **Source:** Preferred citation in `CITATION.cff`, README, and documentation.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause
- **Source:** `pyproject.toml`, `LICENSE.rst`, Zenodo, and DataCite. SoMEF's file-text classifier suggested BSD-2-Clause, but the repository declares `BSD-3-Clause` and the license text includes the third non-endorsement clause, so BSD-3-Clause is authoritative.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Values:**
  - esa
  - coordinates
  - GONG
  - heliophysics
  - heliosphere
  - magnetic connectivity
  - multi-spacecraft
  - Parker spiral
  - PFSS
  - pyhc package
  - solar
  - solar wind
  - space physics
  - space weather
- **Source:** Identity-aware union of the existing HSSI keywords with current GitHub topics, PyHC community-registry keywords, README terminology, and public API concepts. Each value is written as its stored keyword row spells it.

**`pyhc package`** (Field 16 rule 15). solarmach is listed in the PyHC registry's `_data/projects.yml`
(read at `heliophysicsPy/heliophysicsPy.github.io` commit `f7b0421b08c2cbc614a8d68372b42428d3a53cb2`,
2026-10-29), so the record carries `pyhc package`. HSSI held it before this file did; an earlier
revision of this list left it out.

**`esa`, not `ESA`.** The stored keyword row is `esa`, and the GitHub topic is `esa`. An earlier revision
of this file wrote `ESA` and said the record's `Esa` was "normalized to the authoritative acronym `ESA`".
`Esa` was the view API's title-cased rendering, and keywords bind to an existing row case-insensitively,
so nothing was renamed; rule 13 also rules out re-sending a keyword to change only its case.

**Sources, read at `cd4d8366d78b0029a1ad6f18f2efdc69f45a52ec` and on 2026-10-29.** The package metadata
declares no `keywords` (`pyproject.toml`, `CITATION.cff`, `setup.py`, `.zenodo.json`), and the Zenodo
deposits for v0.5.3 and v0.5.7 carry none. The GitHub topics `esa`, `heliophysics`, `space-physics`,
`spacephysics` and `spaceweather` bind `esa`, `heliophysics`, `space physics` and `space weather`. Live
HSSI holds both `space physics` and `space-physics` as rows; rule 11 binds an existing row and never
mints a separator variant, but no rule says which of two existing rows a topic binds, so the record
keeps `space physics`, the row it already carried, and does not add `space-physics` beside it (rule 13
also rules out re-sending a keyword only to change its separator). The PyHC entry's keywords
are `solar`, `heliosphere`, `coordinates`, `2D_graphics`, `plotting`, `general` and `web_service`,
unchanged since before the 2026-07-28 extraction (the entry has since gained only its `hssi:` link).
`solar`, `heliosphere` and `coordinates` are kept because the code works in those domains; `2D_graphics`
and `plotting` restate Field 4's visualization rows (rule 6); `web_service` describes no part of this
package, whose tree never names a web service (`git grep -i -P 'web.?service'` finds nothing at the pin,
while `streamlit` matches in `solarmach/`), the web application being the companion recorded in Field 29
(rule 4); and `general` is a PyHC scope tag (rule 2).

### 17. Data Sources (OPTIONAL)
- **Values:**
  - CDAWeb
  - AMDA
  - Observatory/Mission-specific
  - Other
- **Other Data Sources:** AMDA through Speasy, JPL Horizons, and GONG synoptic-map access through SunPy Fido.
- **Source:** `get_sw_speed`, `SolarMACH.__init__`, and `get_gong_map` in the source. `solarmach/__init__.py:133` binds the Speasy AMDA inventory, lines 138-142 select AMDA parameter paths for multiple missions, and line 169 dispatches those datasets to `spz.get_data`, so AMDA is a direct data backend. Observatory/Mission-specific is selected because the package directly retrieves named mission/instrument data products; those relationships are resolved in Fields 31–32. Other remains supported by JPL Horizons and GONG access through SunPy Fido.

### 18. Input File Formats (RECOMMENDED)
- **Values:**
  - FITS
  - Other
- **Other Input File Formats:** Python pickle files containing cached PFSS solutions.
- **Source:** `pfss_utilities.py` loads GONG/HMI FITS maps and can load cached pickled PFSS outputs.

### 19. Output File Formats (RECOMMENDED)
- **Values:**
  - Other
- **Other Output File Formats:** PNG, PDF, HTML, animated GIF, and Python pickle.
- **Source:** Plot methods, PFSS cache code, and the documented example notebook. DataFrames and Plotly figure objects are also returned in memory but are not claimed as file formats.

### 20. Operating System (RECOMMENDED)
- **Values:**
  - Operating System Independent
- **Source:** Exact live HSSI controlled value, normalized from the `Operating System :: OS Independent` classifier in `pyproject.toml` and PyPI.

### 21. CPU Architecture (RECOMMENDED)
- **Values:**
  - CPU Independent
- **Source:** The current PyPI release publishes a `py3-none-any` wheel and the repository contains no architecture-specific compiled code.

### 22. Related Phenomena (OPTIONAL)
- **Values:**
  - Solar Corona
  - Solar Wind
- **Source:** Solar Corona and Solar Wind are exact live HSSI controlled values supported by the package's PFSS and solar-wind functionality. Interplanetary Magnetic Field and Parker Spiral are scientifically supported by the directly implemented and documented backmapping, but are omitted because they are absent from the live Phenomena vocabulary.

### 23. Development Status (RECOMMENDED)
- **Development Status:** Active
- **Source:** Field 23 rule 3: the README's repostatus.org badge declares Active (`README.rst:17-19` at `cd4d8366d78b0029a1ad6f18f2efdc69f45a52ec`: `https://www.repostatus.org/badges/latest/active.svg`, alt text "Project Status: Active – The project has reached a stable, usable state and is being actively developed."). Dated anchors: the last commit on `main` is `cd4d836` (2026-10-27T15:58:28Z), and the latest release is v0.5.7 (2026-10-27). The repository was not archived on 2026-10-29 (GitHub API).

### 24. Documentation (RECOMMENDED)
- **Documentation:** https://solarmach.readthedocs.io
- **Source:** Preserved from the existing HSSI record and confirmed by the README, documentation configuration, and PyHC registry. Since v0.5.5, `pyproject.toml` `[project.urls]` declares `Documentation = "https://solarmach.readthedocs.io"` (`pyproject.toml:66` at `cd4d8366d78b0029a1ad6f18f2efdc69f45a52ec`), and PyPI's `project_urls` for 0.5.7 carry the same URL, so Field 24 rule 3 fires on the project's own declaration. The bare host redirects to `https://solarmach.readthedocs.io/en/latest/`, which answered 200 on 2026-10-29 with a page whose title begins "solarmach documentation"; the stored bare-host form is kept, because rule 6 keeps an incumbent's choice between equivalent landing forms.

### 25. Funder (OPTIONAL)
- **Organization:** European Commission
- **Funder Identifier:** https://ror.org/00k4n6c32
- **Source:** Preserved from the existing HSSI record and confirmed by the live HSSI organization record, Zenodo/DataCite funding metadata, README acknowledgements, and CORDIS project records. The repository says "European Union"; the existing HSSI/Zenodo identity `European Commission` is retained as the funding organization.

### 26. Award Title (OPTIONAL)
- **Award Title:** Solar EneRgetic ParticlE aNalysis plaTform for the INner hEliosphere (SERPENTINE)
  - **Award Number:** 101004159
- **Award Title:** The Energetic Solar Eruptions: Data and Analysis Tools (SOLER)
  - **Award Number:** 101134999
- **Source:** The existing HSSI award and Zenodo/DataCite metadata provide SERPENTINE; the README adds both grant numbers, and the European Commission CORDIS record supports SOLER. The SOLER label is reconciled to the existing shared HSSI Award record matched by identifier `101134999`.

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Values:**
  - https://doi.org/10.48550/arXiv.2608.24458
  - https://doi.org/10.1051/0004-6361/201731047
  - https://doi.org/10.1051/0004-6361:20054262

**https://doi.org/10.48550/arXiv.2608.24458** — Dresing, N., Gieseler, J., Baumgartner-Steinleitner, M.,
Briand, C., Dissauer, K., Fedeli, A., et al. (2026). *Comprehensive solar eruption analyses enabled by
the tools of the SOLER project*. arXiv:2608.24458 (preprint; its first page says it was submitted to the
Journal of Space Weather and Space Climate).
*Evidence (rule 3, its platform clause, "one by an author about the platform the software serves"):* the
preprint's authors include four solarmach authors, Dresing, Gieseler, Palmroos and Vainio, and it
introduces the analysis infrastructure built in the SOLER project, the Horizon Europe project whose
grant 101134999 is recorded in Field 26 and among whose tools it presents solarmach. Its Section 3.6.2,
"PFSS extension of Solar-MACH", describes the package: a Parker-spiral connection in interplanetary
space joined at the source surface to a PFSS model computed from an automatically obtained GONG map,
with an optional bundle of field lines traced from a ring of points around the observer's
source-surface footpoint. Its Fig. 19 shows the semi-logarithmic plot, and the section cites the
solarmach v0.5.3 deposit (10.5281/zenodo.19257728), the Field 14 paper and the Solar-MACH
application's v0.1.7 deposit (10.5281/zenodo.10069803). The paper's combined use cases also show
Solar-MACH plots of the spacecraft constellation. Read in the arXiv v1 PDF; DataCite types the DOI a
preprint, and it resolves to the arXiv abstract page. It is not the Field 14 paper (rule 2). A later
update should check whether the journal has published it, and record the journal version's DOI if it
has.

**https://doi.org/10.1051/0004-6361/201731047** — Poljančić Beljan, I., Jurdana-Šepić, R., Brajša, R.,
Sudar, D., et al. (2017). *Solar differential rotation in the period 1964–2016 determined by the
Kanzelhöhe data set*. Astronomy & Astrophysics, 606, A72.
*Evidence (rule 4, the code's own reference block):* the public `solar_diff_rot` function is documented
as "Based on rLSQ method of Beljan et al. (2017), doi: 10.1051/0004-6361/201731047"
(`solarmach/__init__.py:381` at `cd4d8366d78b0029a1ad6f18f2efdc69f45a52ec`) and returns the rate
14.50 − 2.87 sin²(latitude) degrees per day, in degrees per second (`solarmach/__init__.py:397`);
`backmapping_angle` takes the solar rotation rate of its Parker-spiral backmapping from it
(`solarmach/__init__.py:453`). The code's "Beljan et al." is the paper's first author, Poljančić Beljan.
Title, authors and venue from Crossref; the DOI resolves.

**https://doi.org/10.1051/0004-6361:20054262** — Thompson, W. T. (2006). *Coordinate systems for solar
image data*. Astronomy & Astrophysics, 449, 791–803.
*Evidence (rule 4, the code's own reference block):* `spheric2cartesian` converts Stonyhurst
heliographic coordinates to HEEQ "following Eq. (2) of Thompson (2006)", with the DOI beside it
(`solarmach/pfss_utilities.py:504-509`). `SolarMACH.plot_3d` and `SolarMACH.plot_pfss_3d` place the
Parker spirals, the Sun–spacecraft lines and the other geometric elements of their 3D figures with it
(`solarmach/__init__.py:2524-2724` and `solarmach/__init__.py:2076-2355`); the PFSS field lines are
drawn from their own coordinates. Title and venue from Crossref; the DOI resolves.

HSSI's Related Publications were empty until this update. An earlier revision of this file recorded
"Not found", on the ground that the repository prioritizes the Field 14 paper, and recorded no
literature search and nothing about the code's two references; the preprint did not exist at the
2026-07-28 extraction (arXiv v1 is dated 25 August 2026).

**No further rule 4 references.** Besides the two above and the Field 14 paper, which the code cites for
Eq. (1) of its backmapping (`solarmach/__init__.py:402,427`; rule 2), the pinned tree cites no
publication: `CITATION.cff` has no `references`, the README's and docs' citation sections ask only for
the Field 14 paper, the example notebook's PFSS link is an NSO data page
(`https://nso.edu/data/nisp-data/pfss/`), and no PFSS or Parker-spiral method paper is named in the
code, docs, README or notebook.

**Rule 3's platform clause is read as admitting one publication**, the reading applied to the HAPI
client's record, so the developers' other publications about the tool platform are not added: listing
them would put the platform's output in front of a searcher looking for this package. The field file
does not say whether its "one" limits the count; should it come to read the clause otherwise, the
platform publications weighed below are the ones to revisit. That platform began in the
SERPENTINE project (Horizon 2020 grant 101004159, Field 26) and continues in SOLER: the 2024 deck below
describes the tools developed in SERPENTINE as extended in SOLER and SPEARHEAD, and the preprint's
Section 3.7 builds SOLER's particle tools on methodology developed within SERPENTINE. Of the platform
publications these searches found, the preprint is the only full paper with a section on solarmach, so
it is the publication the clause admits; Palmroos et al. (2022), below, is a second full
paper about the platform, and it names Solar-MACH only through a citation. Weighed and excluded on that
ground:

- Palmroos, C., Gieseler, J., Dresing, N., Morosan, D. E., Asvestari, E., Yli-Laurila, A., Price, D. J.,
  Valkila, S., and Vainio, R. (2022). *Solar energetic particle time series analysis with Python*.
  Frontiers in Astronomy and Space Sciences, 9, 1073578 (https://doi.org/10.3389/fspas.2022.1073578;
  arXiv:2210.10432). A peer-reviewed paper by four solarmach authors, Palmroos, Gieseler, Dresing and
  Vainio, that introduces SEPpy and the SERPENTINE Jupyter-notebook tools, the SERPENTINE side of the
  platform; the preprint's Section 3.7 cites it for that methodology. It names Solar-MACH only by citing
  the Field 14 paper once ("see Gieseler et al., 2022a for an introduction"). Title and venue from
  Crossref; text read in the arXiv PDF.
- Poster https://doi.org/10.5281/zenodo.23035749, "SOLER Open-Source Python Tools for the Analysis of
  Energetic Solar Eruptions" (2026; Zenodo creators Jan Gieseler and "SOLER Team"; the deposited file is
  `SOLER_DASH_2026_A0.pdf`). Its solarmach content is a single panel, "Solar-MACH with PFSS". The poster
  prints an attribution, "Palmroos et al. 2025", near that panel and has no reference list; the one 2025
  record ADS lists first-authored by Palmroos is the SEP onset-time method paper in A&A 694, A221
  (10.1051/0004-6361/202451280), which is not a publication about solarmach.
- Poster https://doi.org/10.5281/zenodo.8406142, "Open-Source Analysis Platform for Solar Energetic
  Particles provided by SERPENTINE" (Gieseler, Palmroos, Dresing, et al., 2023; the deposited file is
  `Gieseler_Jan__DASH__SERPENTINE.pdf`). Its abstract mentions "extensive examples on how to use the
  multi-spacecraft spatial configuration and solar magnetic connection plotter Solar-MACH", and its tool
  list includes "Advanced Solar-MACH functionality", with a panel on the PFSS extension.
- Presentations https://doi.org/10.5281/zenodo.8410961, "Providing Tools for the Analysis of Solar
  Energetic Particles as Jupyter Notebooks – Experiences from the SERPENTINE Project" (Gieseler et al.,
  2023), and https://doi.org/10.5281/zenodo.13990632, "Open-Source Python Tools for the Analysis of
  Energetic Solar Eruptions" (Gieseler, 2024, given at DASH on 16 October 2024 for the SERPENTINE, SOLER
  and SPEARHEAD teams). These slide decks are about the same platform; in them solarmach appears as an
  existing package the project's notebooks build on, and solar-mach.github.io as an example web app.
  The clause excludes them as further platform publications whatever their standalone status, so the
  standalone test was not applied.
- Meeting abstracts (rule 1): Lang, J., Gieseler, J., Dresing, N., et al. (2026), "SOLER Open-Access
  Python Tools for Solar Energetic Particle Data Visualisation and Analysis", 46th COSPAR Scientific
  Assembly (ADS `2026cosp...46.1055L`); Gieseler, J., Palmroos, C., Dresing, N., et al., "Solar-MACH and
  Other Open-Source Python Tools for Solar Energetic Particle Analysis Provided by the SERPENTINE
  Project" and "Solar energetic particle analysis made easy - How to run the SERPENTINE tools in your
  browser", AGU Fall Meeting 2023 (ADS `2023AGUFMSH33E3098G` and `2023AGUFMSH13C2691G`), for neither of
  which a deposited poster or paper was found; "Open-Source Analysis Platform for Solar Energetic
  Particles provided by SERPENTINE", EGU General Assembly 2024 (10.5194/egusphere-egu24-10356); the
  EGU 2024 abstracts on SERPENTINE's results (Vainio et al., 10.5194/egusphere-egu24-6382), its event
  catalogue (Dresing, 10.5194/egusphere-egu24-6092) and its data centre (Gómez-Herrero et al.,
  10.5194/egusphere-egu24-12767); the EGU 2025
  SOLER overview by Vainio et al. (10.5194/egusphere-egu25-11202); and "SOLER Open-Source Python Tools
  for the Analysis of Energetic Solar Eruptions", EGU General Assembly 2026
  (10.5194/egusphere-egu26-21849).

**Other developer items weighed and not added:**
- Dresing, N., et al. (2024), "The solar cycle 25 multi-spacecraft solar energetic particle event
  catalog of the SERPENTINE project", A&A 687, A72 (10.1051/0004-6361/202449831): its subject is the
  event catalogue, whose entries link Solar-MACH plots (`solar_mach_link` in the catalogue deposit,
  10.5281/zenodo.15599147); it uses the software and is not about it or about the platform (rules 3 and
  5). The catalogue deposit is a dataset (rule 1), and it is not a Field 28 candidate either: a
  catalogue made in a science analysis that used the software is excluded there by rule 5.
- Dresing, N., et al. (2023), "The 17 April 2021 widespread solar energetic particle event", A&A 674,
  A105 (10.1051/0004-6361/202345938): a study of one event, first-authored by a solarmach author, whose
  full text names Solar-MACH; it is not about the software or the platform (rules 3 and 5).
- Morosan, D. E., et al. (2026), arXiv:2610.20026, "Tracking a solar energetic eruption and associated
  energetic particles from Sun to spacecraft": a study of the 10 March 2024 eruption made with the SOLER
  tools, whose authors include solarmach authors; it uses the software and is not about it or about the
  platform.
- Software deposits (rule 1): the solarmach and Solar-MACH Zenodo records, the SERPENTINE notebook
  deposits, SOLER SEP Tools (10.5281/zenodo.15827561) and the ASCL record `2022ascl.soft10015G`.
- The Field 14 paper under its preprint identifier, arXiv:2210.00819 (rule 2).

**Third-party uses are not added** (rule 5, widely used). On 2026-10-29 ADS listed more than a hundred
refereed papers citing the Field 14 paper and more than 150 records whose full text names Solar-MACH or
solarmach, about fifty of them from 2025; the package is widely used in solar-energetic-particle
studies, typically for the spacecraft-constellation and magnetic-connection figures it draws. A list of
those users would keep growing and tell a searcher nothing, so the citing and full-text pools were
weighed on that ground rather than listed. Over the records ADS entered from 2026-07-28 to 2026-10-29,
`ack:"Solar-MACH"` and `ack:"solarmach"` matched no record, while `ack:"sunpy"` returned hits. DataCite
records no `IsCitedBy` relation on the concept DOI.

**Search record** (2026-10-29, all years):
- ADS: title and abstract searches for "Solar-MACH", "solarmach" and "Solar MAgnetic Connection Haus";
  the abstract search restricted to the six solarmach authors; title searches for SERPENTINE or SOLER and
  abstract searches for "SERPENTINE project", "SOLER project" or "SERPENTINE platform", both restricted
  to Gieseler, Dresing, Palmroos and Vainio ("SERPENTINE platform" alone returned 0, and the project
  searches also returned meeting abstracts about neither the software nor the platform, namely COSPAR
  `2026cosp...46.1041L` and the EGU 2024 abstracts 10.5194/egusphere-egu24-417, -6233 and -15030, all
  rule 1); `full:("Solar-MACH" OR "solarmach")` restricted to records first-authored by any of the six
  (`author:"^Palmroos, C"` and the like), the search that finds Palmroos et al. (2022) and Dresing et al.
  (2023), whose other results are all recorded above;
  `citations(doi:"10.3389/fspas.2022.1058810")`; and, for records entered from 2026-07-28, `full:` and
  `ack:` for both names and `author:"Gieseler, J"`. Controls: nonsense tokens returned 0, and
  `abs:"pfsspy"`, `title:"sunpy"`, `full:"sunpy"` (also under the first-author restriction) and
  `ack:"sunpy"` returned hits.
- Zenodo: every page of the deposits whose creators carry the ORCIDs of Gieseler, Dresing, Freiherr von
  Forstner, Palmroos, Nyberg and Vainio; title searches for "Solar-MACH" (two software records, the
  positive control) and for the AGU 2023 title above (none).
- DataCite: an exact-title search for "Solar-MACH" (the Solar-MACH application's software deposits and
  arXiv:2210.00819), with a `pfsspy` title search returning hits and a nonsense title 0. A free-text
  DataCite query splits the hyphenated name and returns unrelated records, so it is not a usable route.
- Crossref: a bibliographic search for the AGU 2023 title, which found only meeting abstracts; the same
  search on the Field 14 paper's title found that paper, as a control.
- The pinned tree, for rule 4 references (above).

The next update should search from 2026-10-29.

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found
- **Source:** The source names dynamic CDAWeb/AMDA instrument variables, JPL Horizons ephemerides, and GONG maps, but the repository does not curate a dataset DOI or a preferred permanent dataset citation. Their data services and controlled instrument/observatory relationships are recorded in Fields 17 and 31–32.

### 29. Related Software (OPTIONAL)
- **Values:**
  - https://github.com/jgieseler/Solar-MACH
  - https://github.com/dstansby/pfsspy
- **Source:** The README identifies the first as the corresponding Streamlit web application. GitHub release v0.4.0 documents `pfsspy` as the former PFSS backend replaced by `sunkit-magex`, making it a distinguishing predecessor rather than a generic dependency.
- **Evidence at v0.5.7:** Since v0.5.5, `pyproject.toml` `[project.urls]` declares `"Web App" = "https://solar-mach.github.io"` (`pyproject.toml:70` at `cd4d8366d78b0029a1ad6f18f2efdc69f45a52ec`), the application whose repository is recorded first here; that repository's GitHub homepage is the same URL. The repository root stays the value (rule 12(a)): the application has a public repository and no HSSI entry. No visible entry's Code Repository is `https://github.com/jgieseler/Solar-MACH` (the lookup ignores letter case), and an HSSI search for "Solar-MACH" returned only this entry on 2026-10-29.
- **Concept DOIs passed over** (rule 13): Solar-MACH's is 10.5281/zenodo.7100481 and pfsspy's is 10.5281/zenodo.2566461. The repository URLs are recorded because the site renders a related item's raw URL as its link text.
- **Note:** Generic scientific-Python and tooling dependencies were considered and omitted under the HSSI relevance gate; dependency presence alone does not make them related software.

### 30. Interoperable Software (OPTIONAL)
- **Values:**
  - https://github.com/sunpy/sunpy
  - https://github.com/sunpy/sunkit-magex
  - https://github.com/SciQLop/speasy
  - https://github.com/astropy/astropy
- **Source:** Specific repository evidence demonstrates exchange rather than mere co-installation: public APIs consume and return SunPy coordinate/Map objects and use SunPy Fido; PFSS methods exchange `sunkit-magex` PFSS input/output and field-line objects; `get_sw_speed` consumes Speasy data containers and converts their measurements to DataFrames; and public backmapping/coordinate APIs accept and return Astropy `SkyCoord` and `Quantity` objects.
- **Note:** NumPy, SciPy, pandas, Matplotlib, Plotly, imageio, CMasher, orjson, Jinja2, lxml, parfive, threadpoolctl, tqdm, zeep, and packaging/testing dependencies were considered and omitted because they are generic infrastructure, not high-level demonstrated heliophysics interoperability. Pandas is omitted even though a DataFrame is exposed because it is a Tier-A generic dependency under the HSSI policy.

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** ACE Solar Wind Electron, Proton and Alpha Monitor
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ACE/SWEPAM
- **Instrument Name:** Charge, Element, and Isotope Analysis System
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SOHO/CELIAS
- **Instrument Name:** PSP SWEAP
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/SWEAP/SPC
- **Instrument Name:** Proton-Alpha Sensor
  - **Instrument Identifier:** https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/PAS
- **Instrument Name:** Plasma and Supra-Thermal Ion Composition
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-A/PLASTIC
- **Instrument Name:** Plasma and Supra-Thermal Ion Composition
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-B/PLASTIC
- **Instrument Name:** Wind Solar Wind Experiment
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/Wind/SWE
- **Instrument Name:** HMI
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SDO/HMI
- **Source:** Exact mission/instrument paths in `get_sw_speed` select ACE/SWEPAM, SOHO/CELIAS Proton Monitor, PSP/SWEAP-SPC, Solar Orbiter/SWA-PAS, STEREO-A and STEREO-B/PLASTIC, and Wind/SWE. The `get_pfss_hmimap` implementation directly supports SDO/HMI magnetograms. Duplicate CNES/SMWG representations were normalized to the preferred non-`.html` SMWG rows except where the exact AMDA inventory path selects the CNES Solar Orbiter/PAS row.
- **Note:** No GONG station-level instrument is emitted. The generic `attrs.Instrument("GONG")` query provides no evidence selecting any station among the six station-specific SPASE rows; the uniquely resolved Global Oscillation Network Group observatory remains recorded in Field 32.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Advanced Composition Explorer
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/ACE
- **Observatory Name:** BepiColombo Spacecraft
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/BepiColombo
- **Observatory Name:** Mercury Planetary Orbiter
  - **Observatory Identifier:** https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/BepiColombo/MPO
- **Observatory Name:** Cassini Orbiter
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Cassini
- **Observatory Name:** JUpiter ICy moons Explorer
  - **Observatory Identifier:** https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/Juice
- **Observatory Name:** Juno Orbiter
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Juno
- **Observatory Name:** Mars Express
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MarsExpress
- **Observatory Name:** Mars Atmosphere and Volatile EvolutioN
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MAVEN
- **Observatory Name:** Mercury Surface, Space Environment, Geochemistry and Ranging
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MESSENGER
- **Observatory Name:** Parker Solar Probe
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe
- **Observatory Name:** 1972-012A
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Pioneer10
- **Observatory Name:** 1973-019A
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Pioneer11
- **Observatory Name:** Rosetta Comet Rendezvous
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Rosetta
- **Observatory Name:** Solar and Heliospheric Observatory
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SOHO
- **Observatory Name:** Solar Orbiter
  - **Observatory Identifier:** https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SolO
- **Observatory Name:** Solar Terrestrial Relations Observatory A
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/STEREO-A
- **Observatory Name:** Solar Terrestrial Relations Observatory B
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/STEREO-B
- **Observatory Name:** International Solar Polar Mission
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Ulysses
- **Observatory Name:** Mariner Jupiter/Saturn A
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Voyager1
- **Observatory Name:** Mariner Jupiter/Saturn B
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Voyager2
- **Observatory Name:** ISTP/Wind
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Wind
- **Observatory Name:** Global Oscillation Network Group
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/GONG
- **Observatory Name:** Solar Dynamics Observatory
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SDO
- **Source:** The repository's concrete `body_dict` supported-spacecraft list, mission-specific solar-wind dataset paths, GONG map retrieval, and HMI helper. The matched controlled-list row names are copied verbatim. SMWG rows are preferred over duplicate provider-specific representations except where an evidenced resource has only a CNES row or the exact AMDA `SolarOrbiter.SWAPAS` path selects the CNES Solar Orbiter row. Both BepiColombo and its explicitly aliased MPO spacecraft are included because the repository evidence names both.
- **Note:** Europa Clipper, Psyche, and SOLAR-1/SWFO-L1 are explicitly supported by the source but have no defensible observatory row in the live SPASE-backed vocabulary; they are omitted rather than emitted as identifierless names. Planets and Lagrange points are also omitted because they are bodies/locations rather than observatories.

### 33. Logo (OPTIONAL)
- **Logo:** Not found
- **Source:** No durable software-logo URL was found in the existing HSSI record, current repository metadata, PyHC registry, or SoMEF output. The repository's `examples/solarmach.png` is a generated example plot, not a software logo.
