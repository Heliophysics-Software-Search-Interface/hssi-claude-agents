# HSSI Metadata Extraction Results

**HSSI Software ID:** 337266f5-46b2-4abc-8b87-5555fe336f79
**Repository:** https://github.com/geospace-code/pymap3d
**Source Revision:** 033895e2f1cf6d1a132040d70143b8e893a06ca6
**Extraction Date:** 2026-09-08
**Validation Date:** 2026-09-09
**Validation Status:** PASS

---

Scope note. All repository evidence below was read from pinned revision
`033895e2f1cf6d1a132040d70143b8e893a06ca6`. PyMap3D is an
instrument-agnostic Python coordinate-conversion and geodesy library. The tree also contains
MATLAB-engine comparison tests and a small helper `.m` file, but no current standalone MATLAB
implementation; the language classification in Field 13 applies one “most important languages” criterion
to that distinction. Fields 29–32 apply their relevance gates before identifier lookup, so generic
dependencies, incidental example projects, and bare instrument names are deliberately excluded.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

No submitter identity is established by the repository, DOI record, or PyHC registry, so one is not
inferred.

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.595430
- **Source:** DataCite API (concept DOI for all versions)

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/geospace-code/pymap3d
- **Source:** GitHub repository API and pinned repository metadata
- **Note:** The configured Git remote and historical deposits use `https://github.com/scivision/pymap3d`,
  which redirects to the current organization. GitHub returns `geospace-code/pymap3d` as the
  repository's canonical `full_name` and HTML URL, so the current organization URL is retained.

### 4. Software Functionality (RECOMMENDED)
- **Coordinate Transforms**
- **Data Processing and Analysis**
- **Data Processing and Analysis: Analysis**

**Source:** The pinned `README.md`, JOSS paper, and public API document coordinate conversions among
geodetic, ECEF, ECI, ENU, NED, AER, RA/Dec, spherical, geocentric, n-vector, local/body, and
downrange/crossrange/above frames, plus geodesy calculations such as Vincenty distances, rhumb lines,
radius of curvature, and latitude transformations. The functionality vocabulary has no more
specific generic terrestrial/local-coordinate child, so no narrower value is invented. The parent
and Analysis child together preserve the controlled hierarchy while describing both transformation
and analysis capabilities.

### 5. Related Region (RECOMMENDED)
- **Earth Atmosphere**
- **Earth Magnetosphere**

**Source:** PyHC registry classification ("ionosphere_thermosphere_mesosphere") and repository paper description of coordinate conversions for airborne, space-based, and remote sensing systems near Earth. The software supports coordinate transformations commonly used for Earth's atmosphere and near-Earth space environments.

These two broad regions remain supported by the paper's terrestrial/geospace and near-Earth scope.
Planetary ellipsoid models are calculation options, not evidence that PyMap3D is designed for any
particular planetary magnetosphere. No narrower region is propagated solely from the PyHC category.

### 6. Authors (MANDATORY)

#### Author 1
- **Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation:** Boston University Department of Electrical and Computer Engineering; SciVision, Inc.
- **Affiliation Identifier:** Boston University: https://ror.org/05qwgg493; SciVision, Inc.: Not found
- **Source:** JOSS paper metadata, ORCID public record, DataCite API, LICENSE file, CITATION.cff, git commit history (primary contributor with 750+ commits)

#### Author 2
- **Name:** Ryan Pavlick
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Affiliation Identifier:** Not found
- **Source:** DataCite API, git contributors

#### Author 3
- **Name:** Cchuravy
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Affiliation Identifier:** Not found
- **Source:** DataCite API; GitHub profile does not expose a full personal name

#### Author 4
- **Name:** Samuel Marks
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Affiliation Identifier:** Not found
- **Source:** DataCite API and GitHub profile; raw social handles were not retained as formal affiliations

#### Author 5
- **Name:** Philippe Rivière
- **Author Identifier:** Not found
- **Affiliation:** Visionscarto.net
- **Affiliation Identifier:** Not found
- **Source:** DataCite API

#### Author 6
- **Name:** Felipe Geremia Nievinski
- **Author Identifier:** https://orcid.org/0000-0002-3325-1987
- **Affiliation:** Not found
- **Affiliation Identifier:** Not found
- **Source:** LICENSE file (copyright holder)

An exact-name ORCID match and its public record's geodesy/GNSS-aligned works identify
`https://orcid.org/0000-0002-3325-1987` as Felipe Geremia Nievinski's ORCID. No other identifier is
guessed.

#### Author 7
- **Name:** Michael Kleder
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Affiliation Identifier:** Not found
- **Source:** LICENSE file (copyright holder)

**Note:** CITATION.cff lists "SciVision" as the author name with ORCID 0000-0002-1637-6526. The repository JOSS paper and ORCID public record identify this ORCID as Michael Hirsch.

Exact-name ORCID matches for Ryan Pavlick, Michael Kleder, and Philippe Rivière were rejected because
their public records do not directly link the person to PyMap3D; Ryan's visible works are in
a different research domain. Samuel Marks is ambiguous across multiple ORCID results, and Cchuravy
had no exact family-name result. These rejected matches are retained to prevent future agents from
attaching plausible-looking identifiers without identity evidence. GitHub/social handles are not
treated as affiliations.

### 7. Software Name (MANDATORY)
- **Name:** PyMap3D
- **Source:** PyHC registry (authoritative HSSI software name), `CITATION.cff`, package metadata, and
  `README.md`. Current `codemeta.json` spells the name `PyMap3d`; that inconsistent capitalization is
  not selected over the authoritative registry and project title.

### 8. Description (MANDATORY)
Pure Python (no prerequisites beyond Python itself) 3-D geographic coordinate conversions and geodesy. Function syntax is roughly similar to Matlab Mapping Toolbox. PyMap3D is intended for non-interactive use on massively parallel (HPC) and embedded systems. The package provides coordinate transformations between multiple systems including geodetic, ECEF (Earth-Centered Earth-Fixed), ECI (Earth-Centered Inertial), ENU (East-North-Up), NED (North-East-Down), AER (Azimuth-Elevation-Range), and spherical coordinates. NumPy and Astropy are optional dependencies; the library can operate with pure Python for most transforms, making it suitable for embedded systems and streaming data applications.

**Source:** README.md, pyproject.toml

The description is retained because each substantive claim is supported by the pinned source.
“HPC” describes an intended non-interactive use, not a required processor
architecture (see Field 21).

### 9. Concise Description (OPTIONAL)
Pure Python 3-D geographic coordinate conversions and geodesy for geospace applications, with optional NumPy/Astropy support for enhanced accuracy.

**Source:** Synthesized from README.md and pyproject.toml

The JOSS title and current code metadata support the word “geospace”; it is not inferred only from
PyHC ecosystem membership.

### 10. Publication Date (RECOMMENDED)
- **Date:** 2014-08-03
- **Source:** GitHub repository API `created_at`. This is the software-repository publication date,
  not the 2018 JOSS article date or a later release date.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite concept record for the persistent identifier

### 12. Version (RECOMMENDED)

#### Latest Version (v3.2.0)
- **Version Number:** v3.2.0
- **Version Date:** 2025-07-08
- **Version Description:** Added enu2ecefv and support for downrange-crossrange-above coordinate conversions.
- **Version PID:** Not found

**Source:** GitHub's v3.2.0 release record and PyPI metadata agree on the version and 2025-07-08
release date. The release body names only `enu2ecefv` and downrange/crossrange/above support. The
previous description's n-vector and ECI statements are not v3.2.0 release notes and are removed.

Before this refresh, HSSI retained a description whose n-vector and ECI statements were not the
v3.2.0 release notes. The selected description uses only the two changes named by the primary
v3.2.0 release record; the version number and date remain unchanged.

**Rejected historical alternative:** `https://doi.org/10.5281/zenodo.3262738` is the v1.8.1 deposit,
dated 2019-06-30. It is the newest discoverable release-specific DOI, but v1.8.1 is not the current
software version and its DOI must not be assigned to v3.2.0. DataCite records keyed by the title,
creator, concept DOI, and both historical and current repository names expose only the known
historical integration deposits, ending at v1.8.1. No v3.2.0 Version PID is fabricated; the concept
DOI in Field 2 still identifies the software work.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** (primary - requires Python >= 3.9 as of v3.2.0)

**Source:** `pyproject.toml`, installable package tree, and pinned tracked tree

The single criterion is “languages most important to using or implementing the current shipped
software.” Python 3.x qualifies because the package and implementation are Python. MATLAB does not
qualify under that criterion: the pinned tree contains MATLAB-engine comparison tests and a small
helper `.m` file, but no current standalone MATLAB implementation. The historical JOSS paper
describes a `matlab/` implementation that has since moved to the separate matmap3d repository.
Before this refresh, HSSI also listed MATLAB; it is excluded from the selected current-language
value under the same criterion used to include Python 3.x.

### 14. Reference Publication (OPTIONAL)
- **DOI:** https://doi.org/10.21105/joss.00580
- **Source:** `CITATION.cff`, README badge, JOSS paper, and Crossref. Crossref classifies this as a
  journal article published 2018-03-12 by The Open Journal, titled “PyMap3D: 3-D coordinate
  conversions for terrestrial and geospace environments,” by Michael Hirsch. It is the software's
  reference article, not its software DOI (Field 2) or publication date (Field 10).

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://spdx.org/licenses/BSD-2-Clause.html
- **SPDX ID:** BSD-2-Clause
- **Source:** Tracked `LICENSE`, `pyproject.toml`, and current code metadata. DataCite's generic
  `Other (Open)` value for the historical deposit is less specific and does not override the
  repository's exact BSD-2-Clause license.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- coordinate-conversion
- coordinate-transformation
- geodesy
- geospace

**Source:** The first three values are the repository's exact GitHub topics. The `geospace`
value exists in the HSSI vocabulary and is supported by the JOSS title and current
`codemeta.json` application category.

`geospace` is included because it is supported directly by the project title and code metadata.
Before this refresh, HSSI included `ionosphere_thermosphere_mesosphere`, inherited from the PyHC
registry; that value is excluded because the package lacks evidence at that scientific-domain
specificity. No narrower science keyword is inferred from example projects.

The PyHC registry's additional keyword `specific` was considered and rejected as a non-informative
classification marker rather than a useful science or discovery term; it is not an HSSI keyword.

### 17. Data Sources (OPTIONAL)
Not found. PyMap3D is a computational coordinate library and does not retrieve data from a named
service or repository. Example inputs do not establish a supported data source.

### 18. Input File Formats (RECOMMENDED)
Not found. The public API operates on scalar/array-like coordinate values, and the CLI accepts
positional/option values including comma-delimited numeric values. Neither interface reads a file or
a documented serialized input format. Command-line text is not treated as an input file format.

### 19. Output File Formats (RECOMMENDED)
- **ascii**
- **JSON**

**Source:** The pinned `src/pymap3d/__main__.py` exposes `--output {text,json}`. It emits
space-delimited text to standard output in text mode and JSON via `json.dumps` in JSON mode. Both
are exact controlled FileFormat terms.

Before this refresh, HSSI had no output-format value. `ascii` and `JSON` are selected because they
are the exact controlled terms for the CLI's two user-visible output modes.

### 20. Operating System (RECOMMENDED)
- **Operating System Independent**

**Source:** Exact `pyproject.toml` classifier `Operating System :: OS Independent`. CI portability is
supporting evidence, not a reason to replace the broad controlled value with a platform list.

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Source:** The shipped implementation has no CPU-specific requirement. The README's intended use on
massively parallel systems does not require a particular instruction set and is not evidence for an
HPC/HEC architecture value.

### 22. Related Phenomena (OPTIONAL)
Not found. The software is useful in workflows involving many phenomena but is not designed around
any one of the seven current controlled phenomena. No value is inferred from example projects.

### 23. Development Status (RECOMMENDED)
- **Active**

**Source:** The exact RepoStatus definition for Active is: “The project has reached a stable, usable
state and is being actively developed.” PyMap3D has a stable v3.2.0 release, the
`Development Status :: 5 - Production/Stable` classifier, an unarchived repository, and continued
source work through the 2026-06-21 inspected pin. This satisfies the definition; crude repository
Repository recency alone would not establish this classification.

Before this refresh, HSSI's development-status field was empty. `Active` is selected because the
stable release, production classifier, unarchived repository, and continued development satisfy the
controlled definition above.

### 24. Documentation (RECOMMENDED)
- **URL:** https://geospace-code.github.io/pymap3d/
- **Source:** GitHub repository homepage and README documentation link

### 25. Funder (OPTIONAL)
- **Organization:** United States Air Force Office of Scientific Research
- **Funder Identifier:** https://ror.org/011e9bt93
- **Source:** codemeta.json lists "AFOSR"; ROR identifies AFOSR as the United States Air Force Office of Scientific Research

The NSF grants in the JOSS paper are attached to named projects that used PyMap3D. They do not
demonstrate that those awards funded the software itself and therefore are not added as funders.

### 26. Award Title (OPTIONAL)
Not found

The project-use grant numbers in the JOSS paper are rejected here for the same reason: an award for a
downstream project is not a software award.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

#### Publication 1
- **DOI:** https://doi.org/10.1029/2019GL084473
- **Title:** The Vertical Distribution of the Optical Emissions of a Steve and Picket Fence Event
- **Page Role:** Journal article
- **Source:** DataCite `IsCitedBy` relation and Crossref work metadata

#### Publication 2
- **DOI:** https://doi.org/10.1111/mice.12493
- **Title:** Automated building image extraction from 360° panoramas for postdisaster evaluation
- **Page Role:** Journal article
- **Source:** DataCite `IsCitedBy` relation and Crossref work metadata

#### Publication 3
- **URL:** https://lib.ugent.be/fulltxt/RUG01/002/785/834/RUG01-002785834_2019_0001_AC.pdf
- **Title:** Predicting cycling results using machine learning
- **Page Role:** Master's dissertation
- **Source:** DataCite `IsCitedBy` relation and the primary dissertation PDF

#### Publication 4
- **URL:** https://hdl.handle.net/11250/2566894
- **Title:** Vector corrections in scalar gravimetry
- **Page Role:** Master's thesis
- **Source:** DataCite `IsCitedBy` relation, Handle resolution, and the Norwegian National Research
  Archive publication record

#### Publication 5
- **URL:** https://oacis.repo.nii.ac.jp/records/1650
- **Title:** 国際VHF通信とAIS情報の対応付けに関する基礎研究
- **Page Role:** Master's thesis
- **Source:** DataCite `IsCitedBy` relation and Tokyo University of Marine Science and Technology
  repository citation metadata

All five targets are publications that cite or use PyMap3D, so they remain Field 27 values. None is
the software's primary description; the JOSS article retains that Field 14 role. None is a software
or dataset landing page that should be moved to another field.

### 28. Related Datasets (OPTIONAL)
Not found

Datasets mentioned by citing works and example projects are not datasets that PyMap3D is designed to
support, so they are not inherited into this field.

### 29. Related Software (OPTIONAL)

#### Software 1
- **Name:** matmap3d (Matlab/GNU Octave version)
- **URL:** https://github.com/geospace-code/matmap3d
- **Source:** README.md (Similar toolboxes section)

#### Software 2
- **Name:** maptran3d (Fortran version)
- **URL:** https://github.com/geospace-code/maptran3d
- **Source:** README.md (Similar toolboxes section)

#### Software 3
- **Name:** map_3d (Rust version)
- **URL:** https://github.com/gberrante/map_3d
- **Source:** README.md (Similar toolboxes section)

#### Software 4
- **Name:** cppmap3d (C++ version)
- **URL:** https://github.com/ClancyWalters/cppmap3d
- **Source:** README.md (Similar toolboxes section)

#### Software 5
- **Name:** PyProj
- **URL:** https://github.com/pyproj4/pyproj
- **Source:** README.md (comparison/notes section)

#### Software 6
- **Name:** Astropy
- **URL:** https://github.com/astropy/astropy
- **Description:** Domain-specific optional dependency for established/high-accuracy astronomical and ECI transformations
- **Source:** README.md, `pyproject.toml`, and Astropy calculation paths in `src/pymap3d`

#### Software 7
- **Name:** PyGeodesy
- **URL:** https://github.com/mrJean1/PyGeodesy
- **Description:** Similar-purpose pure-Python geodesy tools
- **Source:** Pinned JOSS paper “Other Programs” section and current GitHub repository metadata

#### Software 8
- **Name:** AstrometryAzEl
- **URL:** https://github.com/space-physics/astrometry_geomap
- **Description:** Downstream astronomy/geospatial companion that uses PyMap3D to project calibrated image azimuth/elevation onto geodetic coordinates
- **Source:** Complete HSSI inbound relationship scan and current AstrometryAzEl source

#### Software 9
- **Name:** DASCutils
- **URL:** https://github.com/space-physics/dascasi
- **Description:** Downstream all-sky-camera companion that declares and imports PyMap3D
- **Source:** Complete HSSI inbound relationship scan and current DASCutils source

#### Software 10
- **Name:** GEOrinex
- **URL:** https://github.com/geospace-code/georinex
- **Description:** GNSS/RINEX companion that uses PyMap3D to derive geodetic receiver positions from ECEF coordinates
- **Source:** Complete HSSI inbound relationship scan, GEOrinex README, public API, and tests

#### Software 11
- **Name:** THEMISasi
- **URL:** https://github.com/space-physics/themisasi
- **Description:** THEMIS all-sky-imager package whose documented coordinate-conversion example passes calibrated arrays to PyMap3D
- **Source:** Complete HSSI inbound relationship scan and current THEMISasi README

**Relevance and settled rationale:** Primary sources for AstrometryAzEl, DASCutils, GEOrinex, and
THEMISasi confirm a concrete PyMap3D integration in each package. They and PyGeodesy are included
because they are distinguishing domain companions or similar-purpose software, not merely because
their names or dependency metadata mention PyMap3D. Repository URLs are used for catalogue peers
because HSSI renders RelatedItem URLs directly, making the relationship legible to visitors.

Before this refresh, HSSI included NumPy in this field. NumPy is excluded because it is Tier A
generic array infrastructure, even though PyMap3D supports it. Astropy remains here because it is a
domain-specific dependency whose high-accuracy astronomy/ECI path characterizes the software; this
does not make it interoperable in Field 30. MATLAB Mapping/Aerospace Toolbox was considered but is
not included: it is an API comparison and test oracle, while matmap3d and the direct open
implementations already capture the durable software relationship.

### 30. Interoperable Software (OPTIONAL)

#### Software 1
- **Name:** AstrometryAzEl
- **URL:** https://github.com/space-physics/astrometry_geomap
- **Demonstrated Exchange:** AstrometryAzEl calls PyMap3D `aer2geodetic` with calibrated image azimuth/elevation arrays to produce geodetic coordinates.
- **Source:** Current AstrometryAzEl source

#### Software 2
- **Name:** DASCutils
- **URL:** https://github.com/space-physics/dascasi
- **Demonstrated Exchange:** The all-sky-camera package declares, imports, and calls PyMap3D in its data implementation.
- **Source:** Current DASCutils package metadata and source

#### Software 3
- **Name:** GEOrinex
- **URL:** https://github.com/geospace-code/georinex
- **Demonstrated Exchange:** GEOrinex imports `ecef2geodetic` and adds PyMap3D-derived `position_geodetic` values to its RINEX receiver output.
- **Source:** Current GEOrinex README, public API, and tests

#### Software 4
- **Name:** THEMISasi
- **URL:** https://github.com/space-physics/themisasi
- **Demonstrated Exchange:** The documented THEMISasi example passes its calibrated all-sky-imager `az`, `el`, location, and time arrays to `pymap3d.azel2radec`.
- **Source:** Current THEMISasi README; its HSSI entry also classifies PyMap3D as interoperable

**Rejected pre-refresh entries and settled rationale:** Before this refresh, HSSI listed NumPy,
pandas, xarray, and Astropy here. NumPy and pandas are excluded because Tier A generic
array/dataframe infrastructure is never Field 30 interoperability. Xarray is excluded because the
pinned current tree has no public API, documentation, example, or test that demonstrates an
xarray-specific exchange; historical compatibility commits do not establish a current supported
interface. Astropy is excluded because PyMap3D uses Astropy objects internally but accepts/returns
numeric values, and the README explicitly says Astropy `Quantity` inputs are unsupported. Internal
use is not interoperability. MATLAB Engine tests compare results against MATLAB toolboxes but do not
provide a user-facing exchange bridge. The four selected science tools remain because their public
sources demonstrate concrete exchanges with PyMap3D.

### 31. Related Instruments (OPTIONAL)
Not found. PyMap3D is a general-purpose, instrument-agnostic coordinate library.

### 32. Related Observatories (OPTIONAL)
Not found. PyMap3D is not designed to support a specific observatory or mission.

**Designed-to-support relevance rationale:** The JOSS paper names HERA radiotelescope, Mahali, Solar
Eclipse network, and High Speed Auroral Tomography only as projects that used PyMap3D. Other
repository references are generic examples or algorithm descriptions involving radar, cameras,
satellites, airborne platforms, GPS, or GNSS. PyMap3D does not read, write, parse, calibrate, or
process data for any named instrument or observatory, nor implement a format or convention specific
to one. Project use is not evidence that this general library was designed to support the project's
instrument or observatory, so none passes the relevance gate.

SPASE metadata was also checked for the named projects. It has no exact HERA, Mahali, or High Speed
Auroral Tomography resource, while Solar Eclipse matches describe generic eclipse context rather
than the named project. Because the named projects do not pass the relevance gate, no SPASE
relationship is recorded. Generic platform terms are not substituted, and no bare name or
identifierless instrument or observatory is retained.

### 33. Logo (OPTIONAL)
Not found

The pinned tree contains no SVG, PNG, JPEG, GIF, WebP, icon, bitmap, or TIFF asset. The only
README images are remote Zenodo, JOSS, code-coverage, continuous-integration, PyPI-version, and
download-count status badges; these communicate status rather than software branding. The PyHC
registry, `codemeta.json`, `CITATION.cff`, package metadata, and documentation configuration do not
declare a logo. An owner avatar or status badge is not substituted for a project-presented asset.

---

## Metadata Sources Summary

**Primary Sources:**
- DataCite API (10.5281/zenodo.595430)
- Crossref API for publication classification
- GitHub repository and release APIs
- PyPI JSON metadata
- ORCID public search/record APIs
- PyHC core, community, and unevaluated registries
- Repository files at the pinned revision: `README.md`, `CITATION.cff`, `LICENSE`,
  `pyproject.toml`, `codemeta.json`, JOSS paper sources, package source, tests, and examples
- HSSI controlled vocabularies
- Primary repositories for PyGeodesy and the four inbound science-tool integrations

**Metadata Quality Notes:**
- Concept DOI exists and is well-documented
- Reference publication available (JOSS)
- Stable current release and continued active development
- Listed in PyHC unevaluated registry
- Comprehensive documentation available
- Several contributor identities remain insufficiently resolved for ORCID attachment
- No discoverable release-specific Zenodo DOI after v1.8.1 (2019)
- Funder information is present in codemeta.json (AFOSR)
- Fields 31–33 are evidenced-empty rather than merely unresearched

**Recommendations for Improvement:**
1. Restore or replace the historical Zenodo release integration so current releases have
   release-specific persistent identifiers.
2. Represent Michael Hirsch directly in `CITATION.cff` rather than using the organization label
   `SciVision` with his personal ORCID, and add only identity-verified contributors/identifiers.
3. Add a project logo upstream if the maintainers want one represented in catalogues.
