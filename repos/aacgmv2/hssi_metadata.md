# HSSI Metadata Extraction Results

**HSSI Software ID:** ac6f7ea3-062c-442f-abf9-9732a88fcc6b
**Repository:** https://github.com/aburrell/aacgmv2
**Source Revision:** 5f855791f04f4071f7ee12c4f901915b6a1d6b98
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-08-24
**Validation Status:** PASS

**Applied to HSSI:** 2026-07-29. **Every field in this file, including Field 6 (Authors), has been applied
and verified against live HSSI.** All 33 sections match the live record.

**Extraction mode:** Seeded full metadata refresh. All fields were pre-populated from the live HSSI
record (both its rendered and stored representations) and then
improved from the source repository at tag `v2.7.1`. No prior canonical `hssi_metadata.md` existed.
Every many-to-many field below is an identity-aware union of the live HSSI values and newly-found
values; no existing HSSI value was dropped except where explicitly marked **REPLACED** with its evidence.

**Reading the per-field *Status* annotations:** each one describes this field's change relative to the
pre-refresh HSSI record — `UNCHANGED`, `NEW`, or `REPLACED`. Every such change has been applied and
verified.

**Sources consulted:** live HSSI record; repository at `5f85579` (README.rst, CHANGELOG.rst,
AUTHORS.rst, .zenodo.json, LICENSE, LICENSE-AstAlg.txt, pyproject.toml, setup.py, docs/,
aacgmv2/, c_aacgmv2/, .github/workflows/); DataCite API (concept DOI 10.5281/zenodo.1212694);
Zenodo API (record 19462137); PyPI JSON API; GitHub REST API; PyHC community registry; ROR API;
ORCID public API; SoMEF
(`somef describe -t 0.7 -r https://github.com/aburrell/aacgmv2`).

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Status: placeholder. HSSI does not expose the original submitter through the view API.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.1212694

*Status: UNCHANGED. Confirmed correct — the Zenodo API reports `conceptdoi: 10.5281/zenodo.1212694`
for record 19462137 (v2.7.1), so this is the all-versions concept DOI, which is what this field wants.
Also matches the DOI badge target in README.rst.*

### 3. Code Repository (MANDATORY)
https://github.com/aburrell/aacgmv2

*Status: UNCHANGED. Confirmed by `pyproject.toml [project.urls] source`, the Zenodo record's
`custom["code:codeRepository"]`, and the GitHub API.*

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms: Ionospheric
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing

*Status: 1 UNCHANGED (`Coordinate Transforms`), 4 NEW. Live HSSI had only `Coordinate Transforms`.
All parent categories required by the HSSI hierarchy are included.*

Per-value evidence:

- **Coordinate Transforms** (unchanged, parent) — the entire package exists to convert between
  coordinate systems. Public API: `convert_latlon`, `convert_latlon_arr`, `convert_mlt`,
  `get_aacgm_coord`, `get_aacgm_coord_arr` (`aacgmv2/__init__.py` exports; `aacgmv2/wrapper.py`).
- **Coordinate Transforms: Ionospheric** (NEW) — the coordinate systems converted are AACGM
  (Altitude Adjusted Corrected Geomagnetic) magnetic latitude/longitude and Magnetic Local Time,
  the standard ionospheric magnetic coordinates. Evidence: `method_code` values `G2A`/`A2G` in
  `aacgmv2/wrapper.py:150-283`; `c_aacgmv2/src/mlt_v2.c` (`MLTConvert_v2`, `inv_MLTConvert_v2`);
  `aacgmv2/__init__.py:48` comment `high_alt_trace = 6378.0  # 1 RE, these are ionospheric
  coordinates`; coefficient validity limit `high_alt_coeff = 2000.0` km; PyHC classifies this
  package under `ionosphere_thermosphere_mesosphere`.
- **Models and Simulations** (NEW, parent required by the two values below).
- **Models and Simulations: Empirical** (NEW) — the package embeds and evaluates empirical
  geomagnetic field models. Evidence: bundled IGRF-14 coefficients (`aacgmv2/igrf14coeffs.txt`) and
  the combined GUFM1/IGRF-14 model spanning 1590-2025 (`aacgmv2/magmodel_1590-2025.txt`);
  `c_aacgmv2/src/igrflib.c` implements `IGRF_loadcoeffs`, `IGRF_interpolate_coefs`, `IGRF_compute`
  (spherical-harmonic field evaluation) and `IGRF_Tilt` (dipole tilt); 89 AACGM-v2 spherical-harmonic
  coefficient epochs in `aacgmv2/aacgm_coeffs/` (1590-2030 in 5-year steps), which are themselves the empirical
  functional approximation published in Shepherd (2014). User-facing entry point:
  `aacgmv2.utils.igrf_dipole_axis(date)` interpolates/extrapolates the IGRF Gauss coefficients and
  returns the dipole axis (`aacgmv2/utils.py:141-208`), documented in `docs/usage.rst` "Utilities".
- **Models and Simulations: Field-line Tracing** (NEW) — `c_aacgmv2/src/aacgmlib_v2.c` implements
  `AACGM_v2_Trace` and `AACGM_v2_Trace_inv`, which integrate along IGRF model field lines using the
  adaptive `AACGM_v2_RK45` Runge-Kutta integrator. This is user-selectable, not internal-only: the
  `method_code` strings `TRACE` / `ALLOWTRACE` / `BADIDEA` are documented on `convert_latlon`,
  `convert_latlon_arr`, `get_aacgm_coord` (default `ALLOWTRACE`), and the CLI exposes `-t/--trace`,
  `-a/--allowtrace`, `-b/--badidea` (`aacgmv2/__main__.py:53-63`).
  **Caveat for the reviewer:** `docs/usage.rst:82-86` states the package "does not perform field-line
  tracing from one location for another" and recommends `apexpy` for that. That disclaimer concerns
  conjugate-point *mapping* / returning traced field lines, which the package indeed does not expose;
  the field-line tracing that *is* present is the RK45 integration used to derive coordinates. This
  judgment call was reviewed and the value confirmed for inclusion.

Considered and **deliberately excluded** (audit trail):

- `Coordinate Transforms: Magnetospheric` — the bundled C library does implement geographic-to-geomagnetic
  dipole (`geo2mag`/`mag2geo`) and eccentric-dipole (`geod2ecdip`/`ecdip2geod`, plus `ecdip_mlt`)
  transforms in `c_aacgmv2/src/igrflib.c`, and MAG/GEO are magnetospheric systems. **Excluded because
  none of these are reachable from the Python API**: `aacgmv2/aacgmv2module.c` exposes only
  `set_datetime`, `convert`, `convert_arr`, `mlt_convert*`, `inv_mlt_convert*`. They are compiled-in
  internals, not user-facing capabilities.
- `Data Processing and Analysis` / `:Processing` — the CLI reads a whitespace-delimited ASCII file and
  writes one (`np.loadtxt`/`np.savetxt` in `aacgmv2/__main__.py`). **Excluded because** the only
  operation performed is the coordinate transform already captured above; tagging a library's batch CLI
  as generic data processing would be equally true of most packages and carries no information.
- `Data Visualization` (any) — the package produces no plots; `matplotlib` is not a dependency.
- `Data Processing and Analysis: Data Access and Retrieval` — no remote data access anywhere in the
  package; all coefficient files ship with the distribution.

*All five values were confirmed against HSSI's live controlled vocabulary as exact matches, including the
parent-qualified form that distinguishes `Models and Simulations: Field-line Tracing` from the
identically-named value under `Data Processing and Analysis`.*

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere

*Status: 1 UNCHANGED (`Earth Magnetosphere`), 1 NEW (`Earth Atmosphere`).*

- **Earth Magnetosphere** (retained) — AACGM coordinates are defined by tracing geomagnetic field
  lines that thread the magnetosphere, and AACGM/MLT is the standard ordering coordinate system for
  magnetosphere-ionosphere coupling and high-latitude conjugate studies. `.zenodo.json` keywords
  include "Magnetic Field"; `magnetosphere` is also the region under which downstream consumers use it.
- **Earth Atmosphere** (NEW) — AACGM is an *ionospheric* coordinate system; the coefficient-based
  conversion is valid from the surface to 2000 km (`high_alt_coeff` in `aacgmv2/__init__.py`), i.e.
  entirely within Earth's upper atmosphere/ionosphere. `.zenodo.json` and `pyproject.toml` keywords
  include "Ionosphere"; PyHC classifies AACGMV2 under `ionosphere_thermosphere_mesosphere`;
  `aacgmv2/__init__.py:48` calls the outputs "ionospheric coordinates".

Not selected: Interplanetary Space, Planetary Magnetospheres, Solar Environment — the software models
only Earth's internal geomagnetic field (IGRF-14/GUFM1) and has no non-terrestrial functionality.

### 6. Authors (MANDATORY)
Identity-aware union of the pre-refresh HSSI record (3 authors), `.zenodo.json` `creators` (4),
`AUTHORS.rst` (4), and the DataCite record for the concept DOI (4). Matched by ORCID first, then
normalized name. **No author was dropped.** Author order is the authoritative source order, which all
four sources agree on.

**Author 1 — Angeline G. Burrell** *(position 1; UNCHANGED)*
- **Author Identifier:** https://orcid.org/0000-0001-8875-9326
- **Affiliation:** United States Naval Research Laboratory — https://ror.org/04d23a975
- *Source: `.zenodo.json` creator 1 (`affiliation: "Naval Research Laboratory"`, same ORCID); DataCite
  creators[0]; `pyproject.toml` maintainer; ORCID public record confirms "Angeline Burrell".*
- *Affiliation name is ROR's authoritative `ror_display` value for `04d23a975` (verified via
  `https://api.ror.org/v2/organizations/04d23a975`, status active; "NRL" is its registered acronym).*
- *Note: `.zenodo.json`, `AUTHORS.rst` and DataCite render the name with the middle initial
  ("Angeline G. Burrell") while HSSI stores given name "Angeline". Both are valid renderings; the stored
  form is retained deliberately.*

**Author 2 — Christer van der Meeren** *(position 2; name CORRECTED)*
- **Author Identifier:** *(none — intentionally empty; see below)*
- **Affiliation:** Not found — no affiliation in `.zenodo.json`, DataCite, or `AUTHORS.rst`.
- *Source: `.zenodo.json` creator 2; DataCite creators[1]; `AUTHORS.rst` ("Christer van der Meeren -
  https://github.com/cmeeren"); LICENSE copyright line ("Burrell, van der Meeren, Laundal").*
- *Name correction: HSSI previously split this name as given `Christer Van Der` / family `Meeren`. The
  Dutch tussenvoegsel belongs with the surname, and every primary source writes it as given **Christer**
  / family **van der Meeren**. Now stored in the correct form.*
- *Identifier deliberately empty: ORCID `0000-0002-8043-0953` is asserted by both `.zenodo.json` and
  DataCite, but the ORCID public API reports that record as **deactivated**, so recording it would
  publish a link that does not resolve. It is retained here as evidence only and is not part of the
  metadata value. If a live replacement ORCID surfaces, this is the field to revisit.*

**Author 3 — Karl M. Laundal** *(position 3; identifier NEW)*
- **Author Identifier:** https://orcid.org/0000-0001-5028-4943
- **Affiliation:** University of Bergen — https://ror.org/03zga2b32
- *Source: `.zenodo.json` creator 3 and DataCite creators[2] both give this ORCID; the ORCID public API
  confirms the record resolves and reads "Karl M. Laundal", matching the stored name exactly. ROR display
  name verified as "University of Bergen".*
- *His ORCID and his Bergen affiliation were previously held on two separate HSSI person records; they are
  now unified on one record carrying both.*

**Author 4 — Hugo van Kemenade** *(position 4; NEW author, name CORRECTED, identifier NEW)*
- **Author Identifier:** https://orcid.org/0000-0001-5715-8632
- **Affiliation:** Nord Software — (no ROR identifier)
- *Source: `.zenodo.json` creator 4; DataCite creators[3]; `AUTHORS.rst` ("Hugo van Kemenade -
  https://github.com/hugovk"). ORCID public API resolves and returns given "Hugo", family
  "van Kemenade". A genuine addition — the package's authoritative author list has four entries and HSSI
  previously carried three.*
- *Name correction: previously stored as given `Hugo Van` / family `Kemenade`; now given **Hugo** /
  family **van Kemenade**. His pre-existing Nord Software affiliation was preserved.*

**Completed correction record (2026-07-29).** The HSSI update API can reuse or create person and
organization records but cannot rename them, so Field 6 could not be applied through the normal update
path — attempting it would have added duplicate records rather than correcting the existing ones. The
correction was therefore carried out as an explicitly approved shared-record operation. It achieved:

- the two duplicate Christer van der Meeren records consolidated into one correctly split identity, with
  the deactivated ORCID dropped rather than carried forward;
- the two complementary Karl M. Laundal records consolidated into one identity holding both the verified
  ORCID and the University of Bergen affiliation, with no duplicated affiliation;
- Hugo van Kemenade's name corrected in place and his verified ORCID attached, preserving his existing
  authorship elsewhere in the catalog;
- the duplicate blank-identifier Naval Research Laboratory organization record consolidated into the
  ROR-bearing record, renamed to ROR's authoritative display name, leaving Angeline Burrell with a single
  NRL affiliation instead of two;
- AACGMv2's authors linked in source order — Burrell, van der Meeren, Laundal, van Kemenade;
- all pre-existing author counts and positions elsewhere in the catalog preserved unchanged.

`Office of Naval Research` is a different institution and was deliberately left untouched.

**Not authors (recorded so they are not mistakenly promoted):** `AUTHORS.rst` has a separate "Thanks"
section listing Marina Shmidt (testing/code review), Bill Rideout (testing), and dinsmoro (testing).
These are acknowledged contributors, not authors, and the 33-field form has no contributor field.

### 7. Software Name (MANDATORY)
AACGMv2

*Status: UNCHANGED. Editorial intent preserved. (For reference only, not proposed: PyPI/import name is
`aacgmv2`, PyHC lists it as `AACGMV2`, GitHub repo is `aburrell/aacgmv2`. HSSI's `AACGMv2` is a valid
rendering of the package name and there is no reason to churn it.)*

### 8. Description (MANDATORY)
AACGMv2 is a Python wrapper for the AACGM-v2 C library, which converts between geographic (geodetic or
geocentric) coordinates and Altitude Adjusted Corrected Geomagnetic (AACGM) coordinates, and between
AACGM longitude and magnetic local time (MLT). AACGM coordinates are a magnetic-field-based coordinate
system in which points along the same geomagnetic field line share a common latitude and longitude,
which makes them well suited to high-latitude ionospheric studies and to magnetosphere-ionosphere
coupling and conjugate work. The package returns magnetic latitude, magnetic longitude and MLT for
single values or for arrays, computing them either from precomputed spherical harmonic coefficients or
by tracing IGRF field lines, with the ALLOWTRACE, TRACE and BADIDEA method codes controlling that
choice. It also provides utilities for geocentric-to-geodetic latitude conversion, the subsolar point,
and the IGRF dipole axis. The bundled C library is version 2.7 and ships AACGM-v2 coefficients derived
from IGRF-14 together with a combined GUFM1/IGRF magnetic field model spanning 1590-2025.
Coefficient-based conversions are valid up to 2000 km altitude, and AACGM coordinates are undefined
near the magnetic equator, where the routines return NaN. Both a Python API and a command-line
interface that reads and writes whitespace-delimited ASCII files are provided. When referencing this
package, cite both the package DOI and the AACGM-v2 journal article, Shepherd (2014),
doi:10.1002/2014JA020264.

*Status: **REPLACED**. Applied and verified.*

*Evidence for replacing rather than preserving: the live HSSI description is verbatim the **2.6.0
release note** ("This major release incorporates AACGM-v2.6 coefficients (2015-2020) derived using the
IGRF13 model. Other changes include removing a deprecated routine..."), which is confirmed by the fact
that the same string is stored as the description of the 2.6.0 version record, and it matches the
CHANGELOG.rst 2.6.0 entry. It is therefore not a
description of the software at all — it is changelog text for a version that is now three releases
stale, and it describes IGRF-13 coefficients that the package no longer ships (2.7.0 moved to IGRF-14,
`CHANGELOG.rst:16-25`). This is a correction of kind, not a stylistic rewrite, so the "preserve
editorial intent" default does not apply. The replacement text is grounded in README.rst:7-16,
docs/usage.rst, docs/installation.rst, `aacgmv2/__init__.py`, `aacgmv2/wrapper.py`,
`c_aacgmv2/README.txt` and `c_aacgmv2/release_notes.txt`.*

### 9. Concise Description (OPTIONAL)
A Python wrapper for the AACGM-v2 C library that converts between geographic and Altitude Adjusted Corrected Geomagnetic (AACGM) coordinates and between AACGM longitude and magnetic local time.

*Status: **REPLACED**. 193 characters — within the 200-character limit. The live HSSI value
is the first 200 characters of the same stale 2.6.0 release note and is additionally truncated
mid-word ("...providing version targets for other deprecated"). Grounded in README.rst:7-11 and the
`pyproject.toml` summary "A Python wrapper for AACGM-v2 magnetic coordinates".*

### 10. Publication Date (RECOMMENDED)
2015-10-07

*Status: **REPLACED** (previous HSSI value: 2020-01-06). Applied and verified.*

*Reasoning per the field definition — "Date of first broadcast/publication... Used for the initial
version of the software." The initial version is 1.0.0. `CHANGELOG.rst:183-186` records
`1.0.0 (2015-10-07) * Initial release`, and the PyPI JSON API gives the 1.0.0 upload time as
2015-10-07T11:45:01. The stored 2020-01-06 is the release date of version **2.6.0** (Zenodo record
3598705, "aburrell/aacgmv2: Version 2.6.0", `publication_date: 2020-01-06`), i.e. the field was filled
with the then-current version's release date rather than the first publication. For context, the GitHub
repository was created 2015-09-21, but first publication is the 1.0.0 release.*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Status: UNCHANGED. Correct per the field guidance (DOI obtained through the GitHub-Zenodo workflow);
DataCite reports `publisher: "Zenodo"` for the concept DOI. Zenodo has no organization-level ROR of its
own, so the URL form the field permits is retained.*

### 12. Version (RECOMMENDED)
- **Version Number:** 2.7.1
- **Version Date:** 2026-04-07
- **Version Description:** Patch release that extends the supported versions of Python and updates the use of numpy in various places to be consistent with the newest versions of that package. Summary: updated supported Python versions to 3.9-3.14; improved casting of floats; updated resources call to use `files` instead of `path`; updated GitHub Actions yamls.
- **Version PID:** https://doi.org/10.5281/zenodo.19462137

*Status: **REPLACED**. The previous value was 2.6.0 (release date `2020-07-30`, the 2.6.0 changelog text,
version PID `https://doi.org/10.5281/zenodo.3598705`). Applied and verified.*

*Value form: the number is recorded as a **bare version string**. The view API prefixes the rendered
value with the software name and a dash; that prefix is a rendering artifact and must never be written
into this file or into an update payload. Verified against the stored version record, which holds the
bare number with no prefix.*

*Evidence for 2.7.1: `pyproject.toml` `version = "2.7.1"`; git tag `v2.7.1` at HEAD
(5f855791f04f4071f7ee12c4f901915b6a1d6b98); `CHANGELOG.rst:5` `2.7.1 (2026-04-07)`; PyPI upload
2026-04-07T20:33:19; GitHub release `v2.7.1` published 2026-04-07T20:32:38Z; Zenodo record 19462137
`publication_date: 2026-04-07`, `version: v2.7.1`. The version description is the release abstract from
the Zenodo/DataCite record and the GitHub release body. The version PID
`https://doi.org/10.5281/zenodo.19462137` was verified to resolve (HTTP 200).*

*Additional correction noted for the record: the stored 2.6.0 row's `release_date` of **2020-07-30 is
itself wrong** — Zenodo record 3598705 gives 2020-01-06 for version 2.6.0. This is moot if the version
is replaced, but is recorded in case the user prefers to keep 2.6.0 alongside 2.7.1.*

*Decision surfaced for the user: Version is treated here as a single current-release value (replace),
consistent with how HSSI renders it, rather than a set-union field. If the intent is to keep a version
history, 2.6.0 should be corrected to release_date 2020-01-06 and 2.7.1 added alongside it.*

### 13. Programming Language (RECOMMENDED)
- C
- Python 3.x

*Status: UNCHANGED (union produced no additions). Confirmed by SoMEF language breakdown (C 167,328
bytes; Python 112,261 bytes; Makefile 858 bytes), by the C extension build in `setup.py`
(`aacgmv2/aacgmv2module.c` plus five `c_aacgmv2/src/*.c` files), and by `pyproject.toml`
`requires-python = ">=3.10"` with Python 3.10-3.14 classifiers. Makefile is not an allowed value.
Python 2.x is correctly absent — support was dropped in 2.6.2 (`CHANGELOG.rst:42`).*

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1002/2014JA020264

*Status: UNCHANGED. Shepherd, S. G. (2014), "Altitude-adjusted corrected geomagnetic coordinates:
Definition and functional approximations", JGR Space Physics, 119, 7501-7521. The repository names this
as the required citation in README.rst:11-16, `.zenodo.json` `references`/`notes`,
`aacgmv2/aacgmv2module.c:12-15`, `c_aacgmv2/README.txt:4-8` and `c_aacgmv2/release_notes.txt`.
(A `curl` of the DOI returns HTTP 403 — that is Wiley bot-blocking, not a broken DOI; the identifier is
asserted by every primary source in the repository.)*

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html

*Status: **NEW** — live HSSI stores `license: null`.*

*Evidence: `LICENSE` at the repository root is the MIT License text ("Copyright (c) [2019] Burrell,
van der Meeren, Laundal"); `.zenodo.json` `license.id: "MIT"`; `pyproject.toml` classifier
`License :: OSI Approved :: MIT License`; GitHub API `license.spdx_id: "MIT"`; SoMEF returns
`spdx_id: MIT`; DataCite `rightsList` gives `rights: "MIT License"`,
`rightsIdentifier: "mit"`, scheme SPDX. README.rst:10-11 states "The package is free software
(MIT license)".*

*Note (not a competing value): `LICENSE-AstAlg.txt` covers only the bundled astronomical-algorithms C
source (`c_aacgmv2/src/astalglib.c`, from Kile B. Baker, National Science Foundation, implementing
routines from Meeus, "Astronomical Algorithms") and is GNU General Public License v2 or later. The
package as distributed is MIT; the GPL file is a third-party component. Recorded so a reviewer who
notices the second license file has the explanation.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
Stored (lowercase) identities — 13 existing + 2 new:

- aacgm *(existing)*
- aacgm v2 *(existing)*
- aacgmv2 *(NEW)*
- altitude adjusted corrected geomagnetic coordinates *(existing)*
- conversion *(existing)*
- converting *(existing)*
- coordinate conversion *(existing)*
- heliophysics *(existing)*
- igrf *(NEW)*
- ionosphere *(existing)*
- magnetic coordinates *(existing)*
- magnetic field *(existing)*
- magnetic local time *(existing)*
- mlt *(existing)*
- space physics *(existing)*

*Status: 13 UNCHANGED, 2 NEW. The 13 existing forms were read from HSSI's stored keyword records rather
than from the rendered page, so these are the exact stored lowercase identities (the view renders them
Title Case, e.g. stored `mlt` renders as `Mlt`). Comparison was done on normalized lowercase values; no
case-variant duplicates are introduced.*

- **aacgmv2** (NEW) — present in both `pyproject.toml` `keywords` and `.zenodo.json`/DataCite
  `subjects`. It is the only term in the package's own declared keyword lists that HSSI does not
  already hold.
- **igrf** (NEW) — the package bundles and evaluates IGRF-14 coefficients
  (`aacgmv2/igrf14coeffs.txt`, `aacgmv2/magmodel_1590-2025.txt`, `c_aacgmv2/src/igrflib.c`) and exposes
  `aacgmv2.utils.igrf_dipole_axis`; `docs/maintenance.rst` is largely about updating IGRF. `igrf` is an
  established keyword in this vocabulary (e.g. PyHC uses it for asilib).

Considered and dropped: `superdarn` — AACGM is the SuperDARN standard coordinate system and the C
library is distributed by the Dartmouth SuperDARN group, but the package itself is not SuperDARN-specific
and tagging it so would mislead search; `coordinates` — near-duplicate of the existing `magnetic
coordinates` / `coordinate conversion`.

### 17. Data Sources (OPTIONAL)
Not found — not applicable.

*Reasoning: the software retrieves no data from any archive or service. It has no network code and no
HTTP/FTP/API client anywhere in `aacgmv2/` or `c_aacgmv2/`; the only dependency is numpy. All model
input is read from ASCII coefficient files that ship inside the distribution (`aacgm_coeffs/`,
`igrf14coeffs.txt`, `magmodel_1590-2025.txt`), located via the `AACGM_v2_DAT_PREFIX` and `IGRF_COEFFS`
environment variables set in `aacgmv2/__init__.py`. Selecting `Other` here would assert a data source
that does not exist, so the field is deliberately left empty (matching live HSSI, which has `[]`).*

### 18. Input File Formats (RECOMMENDED)
- ascii

*Status: **NEW** — live HSSI has `[]`.*

*Evidence: the CLI reads whitespace-delimited plain-text tables via `np.loadtxt(args.file_in, ndmin=2)`
(`aacgmv2/__main__.py:79`), documented in `docs/usage.rst:30-38` with an example `input.txt` of
`lat lon alt` rows plus `#` comment lines; test fixtures are `aacgmv2/tests/test_data/*.txt`. The
bundled coefficient files are also ASCII (`aacgm_coeffs-14-*.asc` read by `AACGM_v2_LoadCoefFP`,
`magmodel_1590-2025.txt` parsed line-by-line in `aacgmv2/utils.py:169-187` and by
`IGRF_loadcoeffs`).*

*No other format applies: there is no CDF, FITS, HDF5, netCDF, JSON, csv, IDL.sav or Zarr I/O anywhere
in the package.*

### 19. Output File Formats (RECOMMENDED)
- ascii

*Status: **NEW** — live HSSI has `[]`.*

*Evidence: the CLI writes plain text via `np.savetxt(args.file_out, ..., fmt='%.8f')`
(`aacgmv2/__main__.py:95` and `:104`), with stdout as the default sink; `docs/usage.rst:41-46,66-71`
shows the resulting ASCII output files. The library API itself returns numpy arrays/floats and writes
no files.*

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

*Status: **NEW** — live HSSI has `[]`.*

*Evidence: `docs/installation.rst:18` "Tested Setups" heading, `:23` "Mac (64 bit), Windows (64 bit), and Linux
(64 bit)". `pyproject.toml` classifiers list `Operating System :: Unix`, `:: POSIX`,
`:: MacOS :: MacOS X`, `:: Microsoft :: Windows`. `.github/workflows/main.yml` runs the full test suite
on `ubuntu-latest`, `windows-latest`, `macos-latest` and `macos-26-intel`.
`docs/installation.rst:26-40` documents a Windows-specific environment-variable workaround, confirming
Windows is genuinely supported rather than nominally listed.*

*Not selected: `Operating System Independent` / `OS Independent` — the package builds a C extension and
has documented platform-specific handling (Windows `setenv`/`M_PI`/`NAN` shims described in
`docs/maintenance.rst:60-70`), so it is not OS-independent; Solaris and MobilePlatform have no evidence.*

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64

*Status: **NEW** — live HSSI has `[]`.*

*Evidence for **x86-64**: `.github/workflows/main.yml` pins `architecture: 'x64'` for every job and runs
on `ubuntu-latest`, `windows-latest` and `macos-26-intel`; the published 2.7.1 wheel on PyPI is
`aacgmv2-2.7.1-cp310-cp310-macosx_26_0_x86_64.whl`, and 2.6.3 shipped
`aacgmv2-2.6.3-cp39-cp39-macosx_11_0_x86_64.whl`.*

*Evidence for **Apple Silicon arm64**: release 2.7.0 published
`aacgmv2-2.7.0-cp310-cp310-macosx_14_0_arm64.whl` on PyPI — an official native arm64 binary
distribution, which is authoritative that the package builds and runs on Apple Silicon.*

*Not selected (deliberately): `Linux aarch64 or arm64` — no wheel, no CI job, no documentation. The C
source is portable and would very likely build there, but "likely" is not evidence. GPU, HPC or HEC,
ppc64le, Sun (SPARC) and CPU Independent likewise have no evidence (and CPU Independent is wrong for a
compiled C extension).*

### 22. Related Phenomena (OPTIONAL)
Not found — no applicable value.

*Reasoning: the software is phenomenon-agnostic by design: it is a coordinate transformation library
that supports any study performed in magnetic coordinates rather than any particular phenomenon, so
no value from the controlled vocabulary applies — including its geospace rows (`Geomagnetic Storms`,
`Solar Wind`). An earlier version of this note instead called the vocabulary "entirely
solar-atmosphere phenomena" and enumerated a stale six-value documentation list (which included a
`Coronal Holes` phantom and omitted the two geospace rows); that description of the vocabulary was
wrong (corrected 2026-08-24), but the emptiness conclusion stands on the phenomenon-agnostic
rationale. Custom entries are permitted by the field, but inventing one (e.g. "aurora") would
over-claim a scientific scope the code does not implement. Left empty, matching live HSSI.*

### 23. Development Status (RECOMMENDED)
Active

*Status: **NEW** — live HSSI stores `developmentStatus: null`.*

*Evidence, against the repostatus.org definition ("reached a stable, usable state and is being actively
developed"): `pyproject.toml` classifier `Development Status :: 5 - Production/Stable`; the most recent
release 2.7.1 was published 2026-04-07, under four months before this extraction; the GitHub API
reports `archived: false` and `pushed_at: 2026-04-07T20:32:38Z` with 6 open issues; the CI matrix was
updated in 2.7.1 to cover Python 3.14 (`CHANGELOG.rst:5-14`); PyHC rates the package "Good" on all six
maturity axes (community, documentation, testing, software_maturity, python3, license — verified in the
PyHC `projects.yml` registry entry for AACGMV2). Not `Inactive` (there is ongoing maintenance), not `WIP` (there are 20+ stable releases
since 2015).*

### 24. Documentation (RECOMMENDED)
https://aacgmv2.readthedocs.io/en/latest/

*Status: UNCHANGED. Confirmed by README.rst:56, `pyproject.toml [project.urls] documentation`,
`.readthedocs.yml`, and SoMEF. (PyHC lists the equivalent `http://aacgmv2.readthedocs.io`; the stored
HTTPS `/en/latest/` form is the better value and is retained.) Installation instructions live at
`docs/installation.rst`, reachable from this URL, satisfying the field's "including installation
instructions" requirement.*

### 25. Funder (OPTIONAL)
Not found.

*Searched: every `.rst`, `.md`, `.py`, `.toml`, `.cfg`, `.txt` and `.json` file in the repository for
"fund", "grant", "award", "acknowledg", "sponsor", "NNX", "80NSSC" — no funding or acknowledgement
statement exists anywhere in the repository. DataCite reports `fundingReferences: []` for the concept
DOI. Deliberately not inferred from author affiliation (the fact that the lead author works at the
United States Naval Research Laboratory is not evidence that NRL funded this package), and not inferred
from the National Science Foundation attribution in `LICENSE-AstAlg.txt`, which is a copyright notice
on a third-party bundled C file, not a funder of this software.*

### 26. Award Title (OPTIONAL)
Not found.

*No award title or award number appears anywhere in the repository or in the DataCite record
(`fundingReferences: []`). Consistent with Field 25.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1007/s11214-016-0275-y — Laundal, K. M., and A. D. Richmond (2016), "Magnetic
  Coordinate Systems", Space Science Reviews.

*Status: **NEW** — live HSSI has `[]`.*

*Evidence: cited in the module docstring "References" section of `aacgmv2/utils.py:9-13`, which is the
module implementing `subsol`, `gc2gd_lat` and `igrf_dipole_axis`. It is the reference work for the
magnetic coordinate systems the package implements, and is co-authored by aacgmv2 author Karl M.
Laundal. DOI verified to resolve (HTTP 200).*

*Not included, with reasons: Shepherd (2014) — that is Field 14, the Reference Publication, and must not
be duplicated here. The IGRF-14 description paper — the package uses IGRF-14 coefficients but no IGRF
paper DOI is cited anywhere in the repository, and such a paper describes a model the software consumes
rather than "describing, citing, or using the software", which is what this field asks for. Meeus,
"Astronomical Algorithms" (cited in `c_aacgmv2/include/astalg.h`) — a book with no DOI, referenced only
by the bundled third-party C file. Baker and Wing's original AACGM work is alluded to in
`c_aacgmv2/src/aacgmlib_v2.c` and `mlt_v2.c` code comments but with no citation or DOI given, so it is
not recorded rather than reconstructed from memory.*

### 28. Related Datasets (OPTIONAL)
Not found.

*The package ships three coefficient datasets — 89 AACGM-v2 spherical-harmonic coefficient files
(`aacgmv2/aacgm_coeffs/aacgm_coeffs-14-*.asc`, epochs 1590-2030 in 5-year steps), the IGRF-14 coefficients
(`aacgmv2/igrf14coeffs.txt`) and the combined GUFM1/IGRF-14 model (`aacgmv2/magmodel_1590-2025.txt`),
all obtained per `docs/maintenance.rst` from the Dartmouth AACGM distribution. Searched DataCite for a
citable IGRF-14 coefficient dataset (`titles.title:"International Geomagnetic Reference Field"`) and
found records only for the 11th and 13th generations, none matching the IGRF-14 coefficients bundled
here; the AACGM-v2 coefficient files have no DOI. These are also bundled *inputs* to the software
rather than datasets the software provides analysis functionality for, which is what this field asks
for. Recorded as Not found rather than guessing at a DOI.*

### 29. Related Software (OPTIONAL)
- **AACGM-v2 C library** — https://superdarn.thayer.dartmouth.edu/aacgm.html
- **apexpy** — https://doi.org/10.5281/zenodo.1214206

*Status: 2 **NEW** — live HSSI has `[]`.*

- **AACGM-v2 C library** (S. G. Shepherd, Dartmouth College) — this is the software AACGMv2 wraps and
  vendors. Version 2.7 of the C source is bundled verbatim in `c_aacgmv2/` (`aacgmlib_v2.c`,
  `igrflib.c`, `mlt_v2.c`, `rtime.c`, `astalglib.c`) and compiled into the `aacgmv2._aacgmv2` extension
  by `setup.py`. `docs/maintenance.rst:19-23` names the Dartmouth site as the source for coefficient and
  code updates, and README.rst:7-9 links it. This is precisely the field's "important software
  dependency / software this work was derived from" case. No DOI exists for the C distribution; the
  Dartmouth distribution page is the canonical location and was verified to return HTTP 200.
- **apexpy** — a similar-purpose package (Python wrapper for the Apex Fortran library, converting
  between geodetic, modified apex and quasi-dipole magnetic coordinates, also with MLT), maintained by
  the same lead author. The evidence is in this repository's own documentation:
  `docs/usage.rst:82-86` states that aacgmv2 "does not perform field-line tracing from one location for
  another... We recommend using :py:mod:`apexpy` for this purpose." That is an explicit
  same-domain alternative/complement pointer, which is exactly what Field 29 is for. Concept DOI
  `10.5281/zenodo.1214206` confirmed via DataCite (title "apexpy", latest v2.1.1) and verified to
  resolve (HTTP 200). Already present in HSSI as "ApexPy".

Considered and **dropped** (audit trail):

- **numpy** — Tier A generic scientific-Python infrastructure. It is the package's only runtime
  dependency (`pyproject.toml`), but "depends on numpy" is true of nearly every package in HSSI and
  distinguishes nothing. Excluded from both Field 29 and Field 30.
- **setuptools, wheel, oldest-supported-numpy, build, flake8, pytest, pytest-cov, sphinx and the doc
  extras** — Tier A packaging/testing/documentation tooling.
- **IGRF-13 / IGRF-14 / igrfpy** (all present in HSSI) — aacgmv2 embeds its own IGRF evaluation in C
  rather than using any of these packages, and its purpose is coordinate conversion, not geomagnetic
  field computation. Same underlying model, different job; listing them would imply a relationship that
  does not exist.
- **OCBpy, pyDARN** — real relationships, but they are demonstrated *exchanges*, so they belong in
  Field 30 rather than here.

### 30. Interoperable Software (OPTIONAL)
- **OCBpy** — https://doi.org/10.5281/zenodo.1179230
- **pyDARN** — https://doi.org/10.5281/zenodo.3727269

*Status: 2 **NEW** — live HSSI has `[]`. Both are heliophysics peer tools already in HSSI, and both
pass the demonstrated-exchange bar with specific, citable evidence rather than mere co-installation.*

- **OCBpy** (open-closed field line boundary coordinates, same lead author) — declares a hard
  requirement `aacgmv2>=2.7.1` in its `pyproject.toml` `dependencies`, imports it in
  `ocbpy/_boundary.py:26` and `ocbpy/boundaries/dmsp_ssj_files.py:33`, and calls
  `aacgmv2.get_aacgm_coord_arr(...)` at `ocbpy/_boundary.py:743` and
  `ocbpy/boundaries/dmsp_ssj_files.py:387` to obtain the AACGM latitude/MLT that its boundary
  coordinate system is defined against. It also cites the aacgmv2 Zenodo concept DOI
  (10.5281/zenodo.1212694) in its module docstring references. This is a genuine data-model exchange —
  OCBpy's whole coordinate system is built on AACGM coordinates produced by this package. Concept DOI
  confirmed via DataCite; verified to resolve (HTTP 200). Present in HSSI as "OCBpy".
- **pyDARN** (SuperDARN data visualization) — lists `aacgmv2` in `setup.cfg` `install_requires`, and
  `pydarn/utils/coordinates.py` imports it (line 27) and calls `aacgmv2.get_aacgm_coord` (line 90) and
  `aacgmv2.convert_mlt` (line 113) to implement its user-facing `Coords.AACGM` and `Coords.AACGM_MLT`
  coordinate options (lines 225-226). SuperDARN radar geometry is converted to AACGM/MLT by this
  package before plotting — an output-consumed-by-peer-tool exchange, not incidental co-installation.
  Concept DOI confirmed via DataCite; verified to resolve (HTTP 200). Present in HSSI as "pyDARN".

Considered and **dropped** (audit trail):

- **numpy** — Tier A, never listed. Being aacgmv2's sole runtime dependency does not make it
  interoperable software.
- **apexpy** — an alternative implementation of a different magnetic coordinate system rather than a
  package that exchanges data with aacgmv2; recorded in Field 29 instead.
- **Blanket ecosystem claims** — "part of the scientific Python ecosystem" and "a PyHC community
  package, therefore interoperable with PyHC packages" were explicitly *not* used as justification for
  any entry here.

### 31. Related Instruments (OPTIONAL)
Not applicable — intentionally empty.

*AACGMv2 is instrument-agnostic coordinate-transformation software. It reads no instrument data,
implements no instrument-specific format or convention, is not an instrument-team tool, and models no
instrument's measurements. Per the Field 31 relevance gate, instrument-agnostic tools support no
instrument specifically, so the correct value is none. A user searching HSSI for a specific instrument
would not expect this package back. Live HSSI already has `[]`; this confirms rather than changes it.
**No entry was invented to fill the field.***

*Considered and dropped, with resolution detail so the audit trail is complete: **SuperDARN radars**.
AACGM is the SuperDARN community's standard coordinate system and the C library is distributed by the
Dartmouth SuperDARN group (`docs/maintenance.rst:19-23`, README.rst:7-9). The vocabulary does contain
resolvable SPASE rows — `https://spase-metadata.org/SMWG/Instrument/SuperDARN/Radars` (type 1) and
several IUGONET per-radar instrument rows — so this is a "dropped as irrelevant", not "dropped as
unresolvable". It fails the gate because the package neither reads nor processes SuperDARN data; the
relationship is "the coordinate system these radars use", which is exactly the excluded
"commonly used with" case.*

*No entry in this field is recorded without a verified `https://spase-metadata.org/` identifier, and no
entry was omitted for being hard to resolve.*

### 32. Related Observatories (OPTIONAL)
Not applicable — intentionally empty.

*Same reasoning as Field 31: the package is mission- and observatory-agnostic. It works from bundled
global geomagnetic model coefficients and user-supplied latitude/longitude/altitude, with no
mission-specific data product, archive, API or convention anywhere in the code. Live HSSI already has
`[]`. **No entry was invented to fill the field.***

*Considered and dropped: **SuperDARN** as an observatory — the vocabulary row
`https://spase-metadata.org/SMWG/Observatory/SuperDARN` (type 2) exists and resolves, so the drop is on
relevance grounds only, per the reasoning in Field 31. Also considered and dropped: DMSP (aacgmv2 itself
has no DMSP handling — the DMSP SSJ ingest lives in the downstream OCBpy package, and per the
"ecosystem/plugin package" rule it belongs to that package's record, not this one).*

*The complete SPASE-backed instrument/observatory vocabulary was searched to produce the drop notes
above, so each exclusion is a relevance judgment rather than a failure to find a match.*

### 33. Logo (OPTIONAL)
Not found.

*There is no logo asset anywhere in the repository (no `*logo*`, `.png`, `.svg` or `.gif` file outside
`.git/`), README.rst has no logo directive (unlike sibling package apexpy, whose README opens with a
`|logo|` substitution), the PyHC community registry entry for AACGMV2 has no `logo` key, and SoMEF
returned no `logo` result. Live HSSI stores `""`; unchanged.*

---

## Summary of changes applied (2026-07-29)

| Field | Change | Basis |
|---|---|---|
| 4 Software Functionality | +4 values (union) | Code analysis of Python API, C library, CLI |
| 5 Related Region | +1 value (union) | Ionospheric altitude limits, PyHC classification, keywords |
| 6 Authors | +1 author (Hugo van Kemenade), +2 ORCIDs (Laundal, van Kemenade), 2 name corrections, source order, affiliation deduplicated | `.zenodo.json`, `AUTHORS.rst`, DataCite, ORCID API, ROR API |
| 8 Description | Replaced | Previous value was the stale/mis-typed 2.6.0 release note |
| 9 Concise Description | Replaced | Same stale text, truncated mid-word |
| 10 Publication Date | 2020-01-06 → 2015-10-07 | Field means first publication; 1.0.0 released 2015-10-07 |
| 12 Version | 2.6.0 → 2.7.1 (+date, description, PID) | PyPI, GitHub release, git tag at HEAD, Zenodo |
| 15 License | null → MIT License | LICENSE file, `.zenodo.json`, classifiers, DataCite, GitHub |
| 16 Keywords | +2 values (union) | `pyproject.toml`/`.zenodo.json` keywords; bundled IGRF |
| 18 Input File Formats | [] → ascii | `np.loadtxt` CLI input, ASCII coefficient files |
| 19 Output File Formats | [] → ascii | `np.savetxt` CLI output |
| 20 Operating System | [] → Linux, Mac, Windows | `docs/installation.rst`, classifiers, CI matrix |
| 21 CPU Architecture | [] → x86-64, Apple Silicon arm64 | CI `architecture: x64`; PyPI x86_64 and arm64 wheels |
| 23 Development Status | null → Active | Production/Stable classifier, 2026-04-07 release, live CI |
| 27 Related Publications | [] → 1 DOI | `aacgmv2/utils.py` References section |
| 29 Related Software | [] → 2 entries | Vendored C library; apexpy recommended in own docs |
| 30 Interoperable Software | [] → 2 entries | OCBpy and pyDARN call this package's API |

Unchanged and confirmed correct: 2 Persistent Identifier, 3 Code Repository, 7 Software Name,
11 Publisher, 13 Programming Language, 14 Reference Publication, 24 Documentation, 31 Related
Instruments (empty), 32 Related Observatories (empty), 33 Logo (empty).

No authoritative evidence found: 17 Data Sources, 22 Related Phenomena, 25 Funder, 26 Award Title,
28 Related Datasets. **No existing HSSI value was removed.**

## Validation findings and their dispositions

Validation found **0 ERRORS**. Six warnings and three suggestions were raised; every one is dispositioned
below. Nothing was left silently unresolved.

| # | Item | Decision |
|---|---|---|
| W1 | Coefficient file count stated as 175 | **FIXED** — corrected to 89 (1590-2030 in 5-year steps) in Fields 4 and 28; independently reconfirmed |
| W2 | Christer van der Meeren's ORCID `0000-0002-8043-0953` is deactivated (HTTP 409) | **Leave the identifier empty.** Do not publish a link to a dead ORCID record. Evidence retained in Field 6 only |
| W3 | HSSI mis-split the name as `Christer Van Der` / `Meeren` | **CORRECTED.** Not expressible through the update API, which cannot rename a person record; carried out as an approved shared-record correction and verified. See the Field 6 correction record |
| W4 | Burrell had two affiliation records for one institution | **CORRECTED.** Consolidated into the single ROR-bearing record under ROR's authoritative display name, in the same shared-record correction. She now carries one NRL affiliation |
| W5 | Version replace vs. version history | **Replace** — 2.7.1 supersedes 2.6.0, consistent with Version being a singular nested group. (Recorded for the alternative: 2.6.0's stored `release_date` of 2020-07-30 is itself wrong; Zenodo 3598705 gives 2020-01-06) |
| W6 | `Models and Simulations: Field-line Tracing` inclusion | **Keep.** `AACGM_v2_Trace`/`AACGM_v2_Trace_inv` + the RK45 integrator are user-selectable via `TRACE`/`ALLOWTRACE`/`BADIDEA` and the CLI `-t/-a/-b` flags. The `docs/usage.rst` disclaimer concerns conjugate-point mapping, a different capability |
| S1 | Field 20 citation line numbers off | **FIXED** — corrected to `docs/installation.rst:18` and `:23` |
| S2 | "six PyHC maturity axes" unverified | **WITHDRAWN as a false finding.** The PyHC `projects.yml` entry for AACGMV2 does carry exactly six graded axes, all "Good": community, documentation, testing, software_maturity, python3, license. Field 23 now names them |
| S3 | "Angeline" vs "Angeline G." | **No action.** Stylistic; the stored HSSI form is a valid rendering, not an error |

## Shared-record scope note

The Field 6 correction recorded above touched Person and Organization records that HSSI shares with other
software entries, so its effect is not limited to AACGMv2: the corrected names, the added ORCIDs, and the
consolidated `United States Naval Research Laboratory` record now render wherever those people and that
institution appear. Pre-existing author counts and positions on other entries were preserved unchanged.

Any future canonical file that still records `Naval Research Laboratory` or `U.S. Naval Research
Laboratory` as an affiliation, or the name splits `Christer Van Der` / `Meeren`, `Christer van der` /
`Meeren`, or `Hugo Van` / `Kemenade`, or ORCID `0000-0002-8043-0953` for van der Meeren, is stale against
the current catalog.
