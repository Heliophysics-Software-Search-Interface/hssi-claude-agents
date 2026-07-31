# HSSI Metadata Extraction Results

**HSSI Software ID:** aade4249-dedf-4938-9ad1-432553bf0c36
**Repository:** https://github.com/ccsdspy/ccsdspy
**Source Revision:** 4d91371fc9d07535d583fe9c28a4db39f5096a2a
**Extraction Date:** 2026-07-30
**Validation Date:** 2026-07-30
**Validation Status:** PASS

This canonical file records the validated HSSI state as of 2026-07-30. It was seeded from the prior
record and reconciled against the pinned source revision and authoritative external sources.
Controlled-vocabulary values were checked against the live HSSI vocabulary during validation.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]



---

### 2. Persistent Identifier (RECOMMENDED)
`https://doi.org/10.5281/zenodo.7819990`

*Source:* Confirmed as the Zenodo **concept** DOI (all-versions DOI), which is what this field asks
for. `https://zenodo.org/api/records/7819991` returns `conceptdoi: 10.5281/zenodo.7819990` and
`conceptrecid: 7819990`; DataCite for `10.5281/zenodo.7819990` reports
`versionCount: 1, versionOfCount: 0` with `HasVersion → 10.5281/zenodo.7819991`.
*Note:* The README.rst and docs/index.rst badges point at the **version** DOI
`10.5281/zenodo.7819991` (v1.1.0), which would be the wrong value for this field. The stored value
is the more correct of the two — no change.

---

### 3. Code Repository (MANDATORY)
`https://github.com/ccsdspy/ccsdspy`

*Source:* Verified live; matches the local clone's `origin` remote.
*Note:* GitHub's canonical casing of the owner is `CCSDSPy` (`full_name: "CCSDSPy/ccsdspy"` from the
GitHub API). GitHub owner/repo paths are case-insensitive and the stored URL resolves correctly, so
this is cosmetic only and is deliberately **not** changed.

---

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis: Packet Decommutation
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Processing
- Mission-related
- Mission-related: Packet Decommutation
- Mission-related: Ingest
- Mission-related: System Testing



*Evidence per value:*

- **Data Processing and Analysis** *(stored)* — required parent; the package's whole purpose is
  reading and transforming spacecraft data.
- **Data Processing and Analysis: Packet Decommutation** *(stored)* — the core capability.
  `ccsdspy/decode.py` (`_decode_fixed_length`, `_decode_variable_length`) parses tightly-packed,
  non-byte-aligned bit fields out of raw CCSDS Space Packet binary into NumPy arrays;
  `ccsdspy/packet_types.py` exposes it as `FixedLength.load()` / `VariableLength.load()`;
  `ccsdspy/packet_fields.py` defines the `PacketField` / `PacketArray` layout DSL
  (`uint`/`int`/`float`/`str`/`fill`, arbitrary `bit_length`, `byte_order` of `big`/`little`/`"3412"`).
- **Data Processing and Analysis: Calibration** *(new)* — matches the subcategory definition
  ("converting raw instrument data to physical units") exactly. `ccsdspy/converters.py` module
  docstring: "applies post-process to decoded packet fields. This post-processing includes applying
  linear/polynomial **calibration curves**, dictionary replacement, and time parsing."
  `PolyConverter` docstring: "applies **calibration** using a series of coefficients ordered from
  highest power to intercept"; `LinearConverter` is the y=mx+b case. Exercised in
  `ccsdspy/tests/test_converters.py` and documented at `docs/user-guide/converters.rst`.
- **Data Processing and Analysis: Processing** *(new)* — a real post-decode processing pipeline, not
  just decoding: `_apply_converters()` and `_apply_post_byte_reoderings()` in
  `ccsdspy/packet_types.py`, `_do_array_byte_reordering()` for arbitrary byte orders,
  `_expand_array_fields()` / `_unexpand_field_arrays()` for multidimensional array fields, plus
  `EnumConverter` (int→string replacement), `DatetimeConverter` (coarse/fine offsets from a reference
  epoch, multi-input-field), and `StringifyBytesConverter` (bin/hex/oct).
- **Mission-related** *(new)* — required parent for the three below.
- **Mission-related: Packet Decommutation** *(new)* — the vocabulary carries a second
  `Packet Decommutation` row under `Mission-related`, and this library is the archetype: it is
  deployed inside flight-mission ground data systems (Zenodo/GitHub description: "Library used in
  flight missions at NASA, NOAA, and SWRI"; README.rst and docs/index.rst "Used By" list ten
  missions). Its subject matter is mission-operations, not science analysis: CCSDS primary-header
  semantics (APID, sequence count, telemetry-vs-command packet type, secondary-header flag) are
  implemented in `_prepend_primary_header_fields()` and `utils.read_primary_headers()`.
- **Mission-related: Ingest** *(new)* — CCSDSPy ships the classic Level-0 ingest step:
  `utils.split_by_apid()` splits a mixed-APID downlink stream into per-APID streams, exposed as a
  command-line tool in `ccsdspy/__main__.py` (`python -m ccsdspy split <file> --valid-apids`) that
  writes `apid{apid:05d}.tlm` files; `utils.validate()` (added in 1.4.0) performs ingest-time file
  QA — truncation/extra-byte detection, unknown APIDs, and missing or out-of-order sequence counts —
  returning a list of `logging.LogRecord`s.
- **Mission-related: System Testing** *(new)* — synthetic packet generation for verification.
  `docs/user-guide/synthetic.rst`: "It is sometimes necessary or useful to generate synthetic CCSDS
  packets with known data for **testing and validation**." Implemented as
  `FixedLength.to_file()` / `VariableLength.to_file()` → `_to_file()` → `ccsdspy/encode.py`
  (`_encode_fixed_length`, `_encode_variable_length`, via `bitstruct.pack`). CHANGELOG.rst 2.0.0
  lists this as a headline new capability, and notes the companion SPaC-kit uses it to "generate test
  datasets".

*Considered and deliberately excluded (audit trail):*

- **Data Processing and Analysis: File Format Conversion** — CCSDSPy never reads format A and writes
  format B. `load()` goes binary → in-memory NumPy arrays (that is decommutation), `to_file()` goes
  arrays → the same CCSDS binary, and `split_by_apid()` goes CCSDS binary → CCSDS binary. CSV is read
  only as a *packet definition* (`_get_fields_csv_file()`), not as data.
- **Data Processing and Analysis: Analysis** — no scientific analysis, statistics, or derived physical
  quantities. `_inspect_primary_header_fields()` and `utils.validate()` are file/header integrity
  checks, not science.
- **Data Processing and Analysis: Time Series Analysis** — `DatetimeConverter` builds datetimes from
  timestamp fields; there is no temporal filtering, trend, or correlation analysis.
- **Data Processing and Analysis: Data Reduction** — no averaging, binning, or downsampling.
- **Data Visualization** (all) — no plotting anywhere; `matplotlib` is not a dependency
  (`pyproject.toml` dependencies are `numpy`, `bitstruct`, `pyyaml`, `appdirs`).
- **Models and Simulations** (all) — `to_file()` writes user-supplied arrays; it models no physical
  system.
- **Coordinate Transforms**, **Data Processing and Analysis: Data Access and Retrieval**,
  **Servers and Environments** (all) — no coordinate systems, no remote-archive clients, no server or
  container/HPC functionality.
- **Mission-related: Calibration** — CCSDSPy provides the calibration *mechanism*; the mission supplies
  the coefficients. Covered by `Data Processing and Analysis: Calibration`.

---

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Solar Environment
- Earth Ionosphere
- Earth Thermosphere
- Earth Lower and Middle Atmosphere
- Interplanetary Space



*Source:* CCSDSPy is itself region-agnostic (it is a telemetry format library), so the only defensible
basis for this mandatory field is curated community metadata about who uses it. The PyHC community
registry — the highest-priority metadata source — curates CCSDSPy's keywords as
`["ccsds", "specific", "heliosphere", "ionosphere_thermosphere_mesosphere", "magnetosphere"]`
(`_data/projects.yml`, lines 94–100 of
`heliophysicsPy/heliophysicsPy.github.io@main`). Mapping those to the live `Region` rows:
`magnetosphere` → **Earth Magnetosphere** (already stored, corroborated);
`ionosphere_thermosphere_mesosphere` → **Earth Ionosphere** + **Earth Thermosphere** +
**Earth Lower and Middle Atmosphere**; `heliosphere` → **Interplanetary Space**.
**Solar Environment** (already stored) is corroborated by the solar missions in the "Used By" list
(PUNCH, GOES-R/SUVI, PADRE). All three sub-terms of the compound PyHC keyword are now treated
consistently: an earlier draft of this file admitted the ionosphere and thermosphere terms but
discarded the mesosphere term as "too weak on its own," which was circular — the three rest on
identical evidence at identical weight, so either all three follow from the keyword or none do.
`Earth Lower and Middle Atmosphere` is the HSSI row covering the mesosphere.

*Considered and deliberately excluded, for consistency with the agnostic-tool reasoning applied in
Fields 22, 31 and 32:*

- **Corona**, **Solar Wind** — would rest only on the README "Used By" name-drop of PUNCH, which is
  the excluded evidence class. `Solar Environment` already covers the solar case.
- **Jupiter Magnetosphere** — Europa Clipper telemetry *is* shipped in-repo
  (`ccsdspy/tests/data/europa_clipper/apid012*.tlm`), but only as regression fixtures for generic
  bit-packing bugs (`test_regression.py:93`, issue #76); it carries no Jovian science functionality.

---

### 6. Authors (MANDATORY)
Author order preserved exactly as stored on HSSI.

1. **Ezra Brooks**
   - Author Identifier: Not found
   - Affiliation: PickNik Robotics — Affiliation Identifier: Not found
2. **Steven Christe**
   - Author Identifier: `https://orcid.org/0000-0001-6127-795X`
   - Affiliation: Goddard Space Flight Center — Affiliation Identifier: `https://ror.org/0171mag52`
3. **Stefan Codrescu**
   - Author Identifier: `https://orcid.org/0000-0002-8615-4216`
   - Affiliation: National Oceanic and Atmospheric Administration — `https://ror.org/02z5nhe81`
   - Affiliation: University of Colorado Boulder — `https://ror.org/02ttsq026`
4. **J. Marcus Hughes**
   - Author Identifier: `https://orcid.org/0000-0003-3410-7650`
   - Affiliation: Southwest Research Institute — `https://ror.org/03tghng59`
5. **Daniel da Silva** (stored on HSSI as givenName `Daniel da` / familyName `Silva`)
   - Author Identifier: `https://orcid.org/0000-0001-7537-3539`
   - Affiliation: Goddard Space Flight Center — `https://ror.org/0171mag52`
   - Affiliation: Laboratory for Atmospheric and Space Physics — `https://ror.org/01fcjzv38`



*Source and verification:* The repository contains **no** CITATION.cff, codemeta.json, .zenodo.json,
AUTHORS, or CONTRIBUTORS file. The authoritative author list is the DataCite/Zenodo record for the
Field 2 concept DOI, whose five `creators` are exactly these five people with exactly these four
ORCIDs. `pyproject.toml` `[project].authors` names a subset — Daniel da Silva
`<mail@danieldasilva.org>` and Steven Christe `<steven.d.christe@nasa.gov>`. All four stored ROR
identifiers were re-resolved against the ROR v2 API and are correct:
`0171mag52` = "Goddard Space Flight Center" (GSFC), `02z5nhe81` = "National Oceanic and Atmospheric
Administration", `02ttsq026` = "University of Colorado Boulder", `03tghng59` = "Southwest Research
Institute". `Goddard Space Flight Center` is ROR's own display name (not an unexpanded acronym), so
it is left as stored. ROR has no record for **PickNik Robotics** (a private robotics company), so
that affiliation correctly carries no identifier. ORCID employment records corroborate: Christe →
NASA Goddard Space Flight Center, Solar Physics Laboratory; Hughes → Southwest Research Institute
Boulder; da Silva → NASA Goddard Space Flight Center; Codrescu lists no employments (HSSI's
NOAA + CU Boulder are retained on the DOI record's authority).

**Name-split note.** ORCID `0000-0001-7537-3539` gives
given-names `Daniel`, family-name `da Silva`, so the person's correct split is given `Daniel` /
family `da Silva`, not the stored `Daniel da` / `Silva`. The shared identity was not altered in this
record.

**Second affiliation for author 5.**
The DataCite/Zenodo record gives Daniel da Silva's affiliation as the single combined string
`"NASA Goddard Spaceflight Center, Laboratory for Atmospheric and Space Physics"`, naming two
institutions; HSSI stored only the Goddard half. **Laboratory for Atmospheric and Space Physics**
(`https://ror.org/01fcjzv38`, verified in ROR) is therefore added as author 5's second affiliation.
Rationale of record: Zenodo's `creators` entry is the authoritative author source for this software,
it names both institutions, and the stored value captured only half of what that source says — so
this restores information the DOI autofill lost rather than inventing any. The counter-signal is
noted for completeness: his ORCID record lists NASA Goddard Space Flight Center only.

**Additional contributors considered.**
`git shortlog -sne --all` shows contributors absent from every authoritative author source, retained
here as the audit trail: **Joshua Garde** (`jgarde@jpl.nasa.gov`, 33 commits),
**Thomas Loubrieu** (`@jpl.nasa.gov`, 9), **Andrew Robbertz** (8), **Gwyn Fireman** (`@nasa.gov`, 3),
**Luna Smith** (2, author of the current HEAD's PR #157), and **MattyG** (`meawoppl@gmail.com`, 1 —
below the ≥2-commit threshold the rest of this list applied, recorded for completeness and immaterial
to the decision).

**None are added.** Rationale of record: no authoritative source credits any of them as an author —
the repository has no CITATION.cff, codemeta.json, AUTHORS, CONTRIBUTORS, or .zenodo.json file, and
the only packaging metadata (`pyproject.toml` `[project].authors`) names just two people. Git commit
history evidences *contribution*, not *authorship*, and is explicitly to be used with caution for
this field. The fact that the Zenodo record has not been updated since v1.1.0 (2023-04-12) even
though 1.2.0 → 2.0.0 shipped substantial new work was weighed as an argument that the credited list
may be stale; it did not change the outcome, because staleness of the authoritative source is not
itself evidence of who should be added. Should the maintainers publish a CITATION.cff or refresh the
Zenodo deposit, this decision should be revisited.

---

### 7. Software Name (MANDATORY)
`CCSDSPy`

*Source:* DataCite/Zenodo title, `docs/index.rst` heading, and the PyHC registry `name` field all
give `CCSDSPy`. The PyPI distribution and Python import name are lower-case `ccsdspy`; the
capitalized display form is the correct name for this field.

---

### 8. Description (MANDATORY)
I/O interface and utilities for CCSDS binary spacecraft data in Python. Library used in flight missions at NASA, NOAA, and SWRI. CCSDSPy provides a Python interface for reading and writing the tightly packed bits of the Consultative Committee for Space Data Systems (CCSDS) Space Packet Protocol, the low-level telemetry format used by many NASA and ESA missions. Users describe a packet's layout declaratively with PacketField and PacketArray objects — or load that layout from a CSV definition file — and CCSDSPy decodes a binary telemetry file into a dictionary of NumPy arrays using vectorized shifting and masking. The FixedLength class handles packets whose layout never changes, while the VariableLength class handles packets containing a field that expands to fill the packet or whose length is set by another field. Fields need not be byte-aligned and may have odd bit lengths, unsigned or signed integer, IEEE floating point, string, or fill types, and big-endian, little-endian, or arbitrary byte orderings. A converter system applies post-processing to decoded fields, including linear and polynomial calibration curves, integer-to-string enumeration replacement, datetime construction from coarse and fine time offsets against a reference epoch, and byte stringification in binary, hexadecimal, or octal. Utility functions read primary headers, split a mixed-APID downlink stream by APID (also available as a `python -m ccsdspy split` command line tool), iterate over or count packets, and validate a packet file for truncation, extra bytes, unknown APIDs, and missing or out-of-order sequence counts. Both packet classes can also write synthetic CCSDS packet files from user-supplied arrays for testing and validation. The library is pure Python, is developed with requirements sourced from the community, is extensively tested, and is a Python in Heliophysics Community (PyHC) package.

*Source of the added material:* README.rst (opening paragraph, Usage Example, Installation),
`docs/index.rst` ("Brief Tour": "highly efficient vectorized shifting and masking"),
`docs/user-guide/ccsds.rst`, `docs/user-guide/synthetic.rst`, `docs/user-guide/loadfile.rst`,
`docs/user-guide/utils.rst`, `ccsdspy/packet_fields.py` (data types and `byte_order`),
`ccsdspy/packet_types.py` (`FixedLength` / `VariableLength` docstrings), `ccsdspy/converters.py`
(the five converter classes), `ccsdspy/utils.py` (`read_primary_headers`, `split_by_apid`,
`iter_packet_bytes`, `count_packets`, `validate`), `ccsdspy/__main__.py` (the `split` CLI), and the
PyHC registry entry.

---

### 9. Concise Description (OPTIONAL, ≤200 characters)
I/O interface and utilities for CCSDS binary spacecraft data in Python. Library used in flight missions at NASA, NOAA, and SWRI.

*Reasoning:* The issue flagged for this field — Field 9 duplicating Field 8 *in full* — is resolved by
the Field 8 expansion above rather than by rewriting Field 9. This string is the maintainers' own
one-line summary (it is verbatim the GitHub repository description and the Zenodo abstract), it is a
genuinely good ≤200-character preview, and the seeding rule is to respect submitted wording rather
than substitute a stylistic alternative. Deliberately left as stored.

---

### 10. Publication Date (RECOMMENDED)
`2017-06-29`



*Why the stored value is superseded:* this field is defined as the "date of first
broadcast/publication," to be "used for the initial version of the software." CCSDSPy's first public
publication was the PyPI release of version `0.0.7` on **2017-06-29**
(`https://pypi.org/pypi/ccsdspy/json`, `releases["0.0.7"][0].upload_time = 2017-06-29T00:15:49`),
which is corroborated by the GitHub repository having been created 2017-05-24.

The stored `2023-04-12` is DataCite's `Issued` date for the concept DOI
(`dates[] → {date: "2023-04-12", dateType: "Issued"}`; Zenodo `metadata.publication_date`), i.e. the
date Zenodo *minted the DOI* — nearly six years and thirteen releases after first publication. It is
an artifact of when the maintainers set up DOI integration, not a publication date for the initial
version, so it does not satisfy this field's definition. The DOI issue date remains recorded in
Field 2's provenance where it belongs.

---

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** `https://zenodo.org`

*Source:* DataCite `publisher: "Zenodo"`. Correct per the field guidance ("For software where a DOI
has been obtained through Zenodo … Zenodo is the correct entry").

---

### 12. Version (RECOMMENDED)
- **Version Number:** `2.0.0`
- **Version Date:** `2026-06-10`
- **Version Description:** Major release. Adds the ability to generate synthetic CCSDS packet files from an existing packet definition, via `FixedLength.to_file()` and `VariableLength.to_file()`, for testing and validation. Replaces the previous `Warning`-based diagnostics with the Python standard-library `logging` module, adding a user-configurable logger (level, format, optional JSON log file) and making `utils.validate()` return log records. Adds optional metadata to packet definitions, so a packet can carry an APID, name, and description and an individual field can carry a description. Drops support for Python versions below 3.10. Released alongside SPaC-kit, a companion package funded by a NASA ROSES High-Priority Open-Source Software award that extends CCSDSPy to manage mission packet formats as distributable plugins.
- **Version PID:** Not found



*Why the stored value is superseded:* the prior version metadata held `number: 1.1.0`,
`release_date: 2024-12-29`, `version_pid: https://doi.org/10.5281/zenodo.7819991`, and a description
that was the Field 8 software description verbatim. `1.1.0` was released 2023-04-11 — nine releases
and three years stale — and each of the other three sub-fields was independently wrong:

- **`version_pid` pointed at the wrong version.** `https://doi.org/10.5281/zenodo.7819991` is
  **1.1.0's** version-specific DOI: Zenodo record 7819991 reports `metadata.version: "1.1.0"` (and
  `conceptdoi: 10.5281/zenodo.7819990`). Carrying it onto a `2.0.0` row would assert a false
  identifier — that DOI does not identify 2.0.0 and never will. Because Zenodo holds only one deposit
  for this software, **no 2.0.0 version DOI exists**, so blank is the truthful value. The **concept**
  DOI `…7819990` is unaffected and remains in Field 2, which is where it belongs.
- **`release_date` matched no release at all.** `2024-12-29` is not the date of any CCSDSPy release.
  1.1.0 shipped **2023-04-11**: the git tag `1.1.0` commit is dated 2023-04-11 and the PyPI upload of
  `ccsdspy-1.1.0-r1.tar.gz` is 2023-04-11T15:23:17. The stored value is a data-entry artifact — it is
  exactly the Zenodo record's own last-`updated` timestamp (2024-12-29T01:22:45), i.e. a
  metadata-modification time captured in place of a release date.
- **The description was not a version description.** It duplicated the software-level summary and said
  nothing about what changed in the release, which is what this sub-field asks for.

These facts support all four recorded version sub-fields.

*Evidence for `2.0.0` as the current authoritative release, from four independent sources that all
agree:*
- **Git tags:** `git for-each-ref --sort=-creatordate refs/tags` → newest is `2.0.0`, created
  2026-06-10 (tag commit `f1bc1f428b74c887a4c9f0a02e62ad6f6445465f`, 2026-06-10 17:47:07 -0400).
- **PyPI:** `info.version` is `2.0.0`; `ccsdspy-2.0.0.tar.gz` uploaded 2026-06-10T21:47:29.
- **CHANGELOG.rst:** the top entry is "Version 2.0.0 - 2026-06-10".
- **GitHub releases:** the repository publishes **no** GitHub Releases (`/releases` returns 0), so
  tags and PyPI are the release record.

*Version date* `2026-06-10` is agreed by all three date-bearing sources above.

*Version description* is a summary of the actual CHANGELOG.rst 2.0.0 entry (four bullets plus the
SPaC-kit paragraph), cross-checked against the code the bullets refer to:
`_to_file()`/`ccsdspy/encode.py` and `docs/user-guide/synthetic.rst` (synthetic packets);
`ccsdspy/logger.py` + `ccsdspy/config.py` + `ccsdspy/data/config.yml` and
`docs/user-guide/logging.rst` (logging); `_BasePacket.__init__(apid=, name=, description=)` and
`PacketField(description=)` (optional metadata); `pyproject.toml` `requires-python = ">=3.10"`
(Python floor).

*Version PID is genuinely absent.* Zenodo minted exactly one deposit for this software:
`https://zenodo.org/api/records/7819991` reports `metadata.version: "1.1.0"` and
`relations.version: [{index: 0, is_last: true}]`, and DataCite gives the concept DOI
`versionCount: 1`. Because the repository publishes no GitHub Releases, the GitHub→Zenodo
integration has not fired since 2023, so **no version-specific DOI exists for 2.0.0**.
*Observation for the maintainers (no metadata action):* the absence is structural rather than a
lookup failure — the project tags releases in git but never publishes a GitHub *Release*, which is
the event the GitHub→Zenodo integration listens for. Publishing an actual GitHub Release would
restore version-DOI minting and let this field be populated in future. Version PID stays
`Not found`.

*Note on the extraction revision:* the source revision `4d91371f` is 5 commits **after** the `2.0.0`
tag (`5067be4` website wording, `9633f88` SPaC-kit changelog note, `a8d41f1`+`e11584f`+`4d91371`
fill-field encoding fix, PR #157). Those changes are unreleased, so `2.0.0` remains the correct
released version. Also note CHANGELOG.rst documents a "Version 1.4.3 - 2025-11-06" that exists on
PyPI (uploaded 2025-11-05) but was never git-tagged; it is superseded either way.

---

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source:* `pyproject.toml` `requires-python = ">=3.10"` with trove classifiers for Python 3.10–3.13;
CI matrix `python-version: ["3.10", "3.11", "3.12", "3.13"]`
(`.github/workflows/ccsdspy-ci.yml`). Pure Python — the repository contains no C, Fortran, or other
compiled source.

---

### 14. Reference Publication (RECOMMENDED)
Not found

*Source:* No DOI'd publication describes the software. There is no JOSS paper; a DataCite query for
`ccsdspy` returns only the two Zenodo software DOIs plus one unrelated presentation. The closest
artifact is the ADASS 2018 poster "CCSDSPy — Convenient Decoding of Binary Spacecraft Telemetry" by
Daniel da Silva (https://adass2018.astro.umd.edu/abstracts/P7.2.html), which has **no DOI** and so
cannot populate this DataCite-DOI field; it is recorded under Field 27 instead. README.rst's
"Acknowledging or Citing ccsdspy" section directs citers to the Zenodo DOI, not to a paper.

---

### 15. License (RECOMMENDED)
- **License:** `BSD 3-Clause "New" or "Revised" License`
- **License URI:** `https://spdx.org/licenses/BSD-3-Clause.html`



*Evidence the stored value is factually wrong:*
- **`LICENSE.rst` contains three conditions, not two.** Alongside the two BSD-2-Clause clauses
  (retain the notice in source; reproduce it in binary form) it carries the BSD-3-Clause
  no-endorsement clause verbatim: "Neither the name of the ccsdspy project nor the names of its
  contributors may be used to endorse or promote products derived from this software without specific
  prior written permission." That third clause is precisely what distinguishes BSD-3-Clause from
  BSD-2-Clause.
- **The package says so itself.** `ccsdspy/__init__.py` line 1:
  `# Licensed under a 3-clause BSD style license - see LICENSE.rst`.
- **GitHub's license detection agrees:** the repository API reports
  `license.spdx_id: "BSD-3-Clause"`.
- Corroborating: `ccsdspy/logger.py` notes its adapted Astropy class "is licensed under the BSD
  3-Clause license" and the repository ships `licenses/ASTROPY.rst`.

*Where the wrong value came from:* the DOI autofill. Zenodo's record carries
`metadata.license: {"id": "bsd-2-clause-netbsd"}` and DataCite renders that as
`BSD 2-Clause "Simplified" License`. The Zenodo deposit's licence field is simply mis-set (it names
the NetBSD 2-clause variant, which the repository does not use); the repository's own LICENSE file is
authoritative. `pyproject.toml` only says `License :: OSI Approved :: BSD License`, which does not
distinguish the variants.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
binary, calibration, ccsds, decoding, esa, heliosphere, ionosphere, magnetosphere, nasa, operations,
packet parsing, packets, python, science, space, space data systems, space packet protocol,
spacecraft data, telemetry, thermosphere



*Source of the additions:*
- `nasa`, `space packet protocol` — `pyproject.toml`
  `keywords = ["python", "nasa", "ccsds", "space packet protocol"]`, the maintainers' own list.
- `heliosphere`, `magnetosphere`, `ionosphere`, `thermosphere` — the PyHC registry's curated keywords
  for CCSDSPy (`heliosphere`, `ionosphere_thermosphere_mesosphere`, `magnetosphere`), decomposed into
  existing single-term rows.
- `telemetry` — README.rst / `docs/index.rst`: "used for many NASA and ESA missions for low-level
  telemetry".
- `spacecraft data` — the software's own description: "CCSDS binary spacecraft data".
- `space data systems` — the expansion of CCSDS, "Consultative Committee for Space Data Systems"
  (`docs/user-guide/ccsds.rst`).
- `packet parsing` — the core capability (`ccsdspy/decode.py`, `FixedLength.load()`).
- `calibration` — `ccsdspy/converters.py` calibration curves (see Field 4).
- `esa` — README.rst / `docs/index.rst`: "used by many NASA and ESA missions".

*Not added:* PyHC's `specific` (a registry-internal tag, not a science keyword); `binary data` and
`data decoding` (near-duplicates of the already-stored `binary` and `decoding`).

*Declined additions, with reasons (recorded 2026-07-30):* `flight software` and `ground data system`
were considered and declined. Neither exists in the live `Keyword` vocabulary — nor do
`ground data systems`, `mission operations`, `spacecraft`, or `flight` — so each would mint a new
permanent row. This field's guidance is to check the live list first and reuse an existing row rather
than mint a near-duplicate, and the twenty keywords above already cover that concept space
(`telemetry`, `space packet protocol`, `spacecraft data`, `space data systems`, `packets`,
`packet parsing`, `operations`). `data processing` *does* exist as a row but was declined as
redundant with Field 4's `Data Processing and Analysis`.

---

### 17. Data Sources (OPTIONAL)
- Other

*Source:* CCSDSPy has no networked data-source client at all — no HTTP/FTP/S3/HAPI/CDAWeb code
anywhere, and its only dependencies are `numpy`, `bitstruct`, `pyyaml`, `appdirs`. Its input is
always a local path or an in-memory file-like object: `pkt.load(file)` and every `ccsdspy.utils`
entry point accept "Path to file on the local file system, or file-like object"
(`ccsdspy/utils.py`, `ccsdspy/packet_types.py`), reading via `np.fromfile` / `np.frombuffer`.
`Other` is the honest representation of that raw local CCSDS telemetry input, per the field's
instruction "If a source is not listed, select 'Other'."
*Deliberately NOT selected:* **`Observatory/Mission-specific`**. The field instructs that selecting
it requires naming the observatory/mission in Field 32, and — as documented at length under Fields 31
and 32 — CCSDSPy is mission-agnostic and lists no observatory. Selecting it would be internally
inconsistent and would misrepresent the software.

---

### 18. Input File Formats (RECOMMENDED)
- csv
- Other

*Source:*
- **`Other`** — raw CCSDS Space Packet binary telemetry, the library's primary input. The CCSDS
  Space Packet Protocol has no row in the `FileFormat` vocabulary. Test fixtures are `.tlm` and
  `.bin` (`ccsdspy/tests/data/**`); decoding is `ccsdspy/decode.py`.
- **`csv`** — packet *definitions* are loaded from CSV by `FixedLength.from_file()` /
  `VariableLength.from_file()` → `_get_fields_csv_file()` (`ccsdspy/packet_types.py`), documented at
  `docs/user-guide/loadfile.rst`, with 3-column and 4-column fixtures under
  `ccsdspy/tests/data/packet_def/` and real definition sets under `ccsdspy/tests/data/split/defs/`
  and `ccsdspy/tests/data/hs/apid*/defs.csv`.
*Not selected:* YAML (`ccsdspy/data/config.yml` via `config.load_config()`) — user configuration,
not a data format, and YAML has no vocabulary row. `CDF`, `FITS`, `HDF5`, `netCDF3/4`, `IDL.sav`,
`ISTP-Compliant`, `Zarr`, `JSON`, `ascii` — none are read; CCSDSPy deliberately has no such readers.

---

### 19. Output File Formats (RECOMMENDED)
- Other

*Source:* CCSDSPy writes exactly one thing — raw CCSDS Space Packet binary, which has no vocabulary
row, hence `Other`. Two paths: `FixedLength.to_file()` / `VariableLength.to_file()` → `_to_file()` →
`ccsdspy/encode.py` (`bitstruct.pack`), documented at `docs/user-guide/synthetic.rst`; and the
`python -m ccsdspy split` CLI in `ccsdspy/__main__.py`, which writes per-APID `apid{apid:05d}.tlm`
binary files.
*Not selected:* `JSON` — `ccsdspy/logger.py`'s `JSONFormatter` and the `log_file_json` config option
produce structured **log** files, not data output, so per this field's "only formats actually
supported" instruction for *data* output they do not qualify. In-memory results are returned as
`dict` of NumPy arrays, not written to a file format.

---

### 20. Operating System (RECOMMENDED)
- Operating System Independent
- Linux
- Mac
- Windows

*Source:*
- **`Operating System Independent`** — the maintainers' own declaration:
  `pyproject.toml` classifier `"Operating System :: OS Independent"` (also on PyPI for 2.0.0).
  Substantiated by the code: pure Python with no compiled extensions, no platform-specific code, and
  platform-neutral config-directory handling via `appdirs`
  (`ccsdspy/config.py`, `docs/user-guide/customization.rst` explicitly discusses per-OS config
  locations).
- **`Linux`** — directly exercised: CI matrix `platform: [ubuntu-latest]`
  (`.github/workflows/ccsdspy-ci.yml`, `.github/workflows/doc-build.yml`) and
  `readthedocs.yml` `build.os: ubuntu-22.04`.
- **`Mac`, `Windows`** — entailed by the OS-Independent declaration: a pure-Python sdist whose only
  runtime dependencies (`numpy`, `bitstruct`, `pyyaml`, `appdirs`) all publish macOS and Windows
  distributions. Not separately exercised by CI.

---

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent
- x86-64
- Apple Silicon arm64
- Linux aarch64 or arm64

*Source:*
- **`CPU Independent`** — the primary and best-supported value. CCSDSPy is pure Python with no
  compiled extensions of its own; PyPI 2.0.0 ships only `ccsdspy-2.0.0.tar.gz` (an sdist, no
  architecture-specific wheels). Byte order is handled explicitly in software rather than inherited
  from the host: `PacketField(byte_order=...)` accepts `"big"`, `"little"`, or an arbitrary digit
  string, and `_do_array_byte_reordering()` (`ccsdspy/packet_types.py`) and
  `_apply_custom_byte_order()` (`ccsdspy/encode.py`) implement the reordering, so results are
  independent of host endianness.
- **`x86-64`** — directly exercised by CI on GitHub `ubuntu-latest` runners.
- **`Apple Silicon arm64`, `Linux aarch64 or arm64`** — supported because the dependency set
  (`numpy`, `bitstruct`, `pyyaml`, `appdirs`) publishes wheels for those architectures and CCSDSPy
  itself is architecture-neutral. Not separately exercised by CI.
*Not selected:* `GPU`, `HPC or HEC`, `Sun (SPARC)`, `ppc64le` — no evidence of use or testing.

---

### 22. Related Phenomena (OPTIONAL)
Not found

*Source:* The live 7-row `Phenomena` vocabulary is `Coronal Heating`, `Coronal Mass Ejections`,
`Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`, `X-ray emission`. CCSDSPy
supports **no** science functionality for any phenomenon: it decodes a packet format. There is no
physics in the library — no phenomenon name appears anywhere in `ccsdspy/*.py`, and its outputs are
raw or engineering-unit field arrays whose scientific meaning is supplied entirely by the mission.
A user searching HSSI for `phenomenon:"Solar Flares"` should not get a telemetry I/O library back.
Populating this field from the phenomena studied by the missions in the README "Used By" list would
be exactly the excluded name-drop inference, and would be inconsistent with the reasoning applied in
Fields 31 and 32. A documented empty field is the correct outcome; the field is OPTIONAL.

---

### 23. Development Status (RECOMMENDED)
`Active`

*Source:* Matches the repostatus.org definition "reached a stable, usable state and is being actively
developed" on every available signal:
- `pyproject.toml` classifier `"Development Status :: 5 - Production/Stable"`.
- A major release, 2.0.0, on 2026-06-10 — 7 weeks before this extraction — and 20 releases on PyPI
  since 2017.
- Active development after that release: 5 commits between the `2.0.0` tag and the extraction
  revision, the most recent being PR #157 merged 2026-07-27.
- GitHub reports `archived: false`, `pushed_at: 2026-07-27`, 12 open issues, 122 stars, and CI
  workflows running on every push and pull request to `main`.
- PyHC's curated quality ratings for CCSDSPy are "Good" across community, documentation, testing,
  software maturity, Python 3, and license.

---

### 24. Documentation (RECOMMENDED)
`https://docs.ccsdspy.org/en/latest/`

*Source of the replacement:* The project's own canonical documentation host. Verified by request:
`https://ccsdspy.readthedocs.io/en/latest/` **redirects**, and resolves successfully, to
`https://docs.ccsdspy.org/en/latest/`, and the repository's GitHub `homepage` field is
`https://ccsdspy.org`, which redirects to the same target. The curated PyHC registry independently
lists `docs: "https://docs.ccsdspy.org/en/latest/#"` — the same URL, with a trailing empty `#`
fragment dropped here as noise. Installation instructions are present at that URL
(README.rst "Installation" / `docs/index.rst` "Install ccsdspy": `pip install ccsdspy`), satisfying
this field's "documentation link including installation instructions".

---

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** `https://ror.org/027ka1x80`

*Source:* The only explicit funding statement anywhere in the repository is in CHANGELOG.rst, in the
2.0.0 release entry: "Coinciding with this release is the release of SPaC-kit. **Funded through a
ROSES High-Priority Open-Source Software award**, SPaC-kit extends the capabilities of ccsdspy to
streamline CCSDS Space Packet management for flight missions." ROSES is NASA's Research Opportunities
in Space and Earth Sciences solicitation, so the funder is NASA. Corroborating (but not itself a
funding statement): the two authors named in `pyproject.toml` are NASA Goddard staff
(`steven.d.christe@nasa.gov`; Daniel da Silva commits as `daniel.e.dasilva@nasa.gov`), and further
contributors commit from `@jpl.nasa.gov` and `@nasa.gov` addresses.
*Decision — entry retained (user, 2026-07-30).* Rationale of record: the ROSES High-Priority
Open-Source Software award is announced in CCSDSPy's **own** release notes, as coinciding with
CCSDSPy 2.0.0 and as funding work that "extends the capabilities of ccsdspy"; the core maintainers
are NASA Goddard civil servants with further contributors at the Jet Propulsion Laboratory; and there
is no competing funder candidate anywhere in the repository or registries. The nuance behind the
question is preserved as evidence rather than removed: the changelog sentence's grammatical **subject
is SPaC-kit**, the companion package, not CCSDSPy itself, so a strict reading would attribute the
award only to SPaC-kit's own record. Weighed and settled in favour of recording NASA here.

---

### 26. Award Title (OPTIONAL)
Not found

*Source:* No award title or award number is published. CHANGELOG.rst refers only generically to "a
ROSES High-Priority Open-Source Software award" — a solicitation-element description (NASA ROSES
element F.15, "High Priority Open-Source Science"), not an award title. The repository has no
acknowledgements section, no `FUNDING` file, and no grant number; a code search of the companion
`CCSDSPy/SPaC-Kit` repository for `ROSES`, `award`, and `80NSSC` returns nothing. Recording a
paraphrase of the changelog sentence as an "award title" would be fabrication, so this field is left
empty.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
1. `https://doi.org/10.5281/zenodo.8412310`
   Hughes, J. M., DeForest, C., Kovac, S., Lowder, C., Patel, R., Seaton, D., & West, M. J. (2023).
   *Interoperability of PUNCH software in the Python ecosystem* [Presentation]. Zenodo.
2. da Silva, D. (2018). *CCSDSPy — Convenient Decoding of Binary Spacecraft Telemetry* [Poster P7.2].
   Astronomical Data Analysis Software and Systems XXVIII (ADASS 2018), College Park, MD.
   https://adass2018.astro.umd.edu/abstracts/P7.2.html

*Source:*
- **Entry 1** is a publication that explicitly uses and credits this software, by one of its own
  authors. Found via a DataCite full-text query for `ccsdspy`; its abstract reads "Our packages
  heavily leverage SunPy, AstroPy, **CCSDSPy**, and ndcube…". Concept DOI `10.5281/zenodo.8412310`
  recorded (rather than the version DOI `…8412311`); DOI resolution verified. Lead author
  J. Marcus Hughes is CCSDSPy author #4, satisfying the field's "publications … that the software
  developer prioritizes".
- **Entry 2** is the original presentation introducing CCSDSPy, by its lead author. It has **no DOI**,
  so it is recorded in APA format with a permanent link, exactly as this field's instructions allow.
  Content verified at the URL (title, author affiliation "NASA/GSFC, Trident Vantage Systems, Johns
  Hopkins University", and an abstract describing the library). It is not used for Field 14 because
  that field requires a DataCite DOI.

---

### 28. Related Datasets (OPTIONAL)
Not found

*Source:* CCSDSPy supports no specific published dataset — it is format-generic. The mission
telemetry in the repository (`ccsdspy/tests/data/europa_clipper/`, `.../csa/apid00400.tlm`,
`.../split/CYGNSS_F7_L0_2022_086_10_15_V01_F__first101pkts.tlm`, `.../hs/`) consists of unpublished
regression-test fixtures with no DOIs and no dataset landing pages; `ccsdspy/tests/data/hs/README.rst`
records that its files are synthetic ("It is fake data which he granted permission to use for the
project"). Nothing here meets this field's bar of "the DOI … [of] the publication that described the
dataset".

---

### 29. Related Software (OPTIONAL)
1. `https://doi.org/10.5281/zenodo.7735001` — **space_packet_parser**
   (repository: `https://github.com/lasp/space_packet_parser`)

*Source and relevance:* space_packet_parser is a *similar-purpose, distinguishing* tool: an
independent Python library for the same task — "A CCSDS telemetry packet decoding library based on
the XTCE packet format description standard" (PyHC registry `_data/projects.yml`; identical GitHub
repository description). It is the direct alternative a user choosing a Python CCSDS decommutation
library must weigh against CCSDSPy, and the two differ in exactly the way that matters: CCSDSPy
defines packets in Python objects or simple CSV, space_packet_parser consumes XTCE XML. Both are PyHC
packages. The DOI recorded is the **active concept DOI** — DataCite reports
`10.5281/zenodo.7735001` with `versionCount: 24` and current version 6.1.2, whereas the older
`10.5281/zenodo.7734999` is a stale concept record last at 4.0.1 under the pre-transfer
`medley56/space_packet_parser` owner.

*Considered and deliberately excluded (audit trail):*
- **SPaC-Kit** — a genuine companion package, but its relationship with CCSDSPy is a
  plugin/extension exchange, so it is recorded under Field 30 rather than duplicated here.
- **numpy, pyyaml, appdirs, pytest / pytest-astropy / pytest-cov, black, flake8, coverage, sphinx,
  sphinx-automodapi, graphviz, numpydoc** — Tier A generic scientific-Python and tooling stack.
  Listing them would be equally true of most of the ecosystem.
- **bitstruct** — a required dependency (`bitstruct>=8.17.0`), used by `ccsdspy/encode.py` to pack
  bits. Excluded because it is generic infrastructure by the "web app / finance model / biology
  pipeline" test: it is a general-purpose bit-field packing library with no heliophysics content, and
  its presence characterises nothing about this software beyond "it manipulates bits".
- **astropy** — excluded with especially clear evidence: CHANGELOG.rst 0.0.8 records "**Removed
  astropy dependency.** Changes return type of ccsdspy.FixedLength.load from astropy.table.Table to
  OrderedDict." The dependency was deliberately dropped. `pytest-astropy` remains a *dev-only* test
  dependency, and `ccsdspy/logger.py` is "adapted from the AstropyLogger class" (with
  `licenses/ASTROPY.rst` shipped) — attributed code reuse, which is an implementation detail rather
  than a related-software relationship.
- **sunpy** — `ccsdspy/config.py`: "This code is based on that provided by SunPy"; `docs/dev-guide`
  standards are "based on those provided by sunpy". Attributed code/convention borrowing, not a
  dependency, not a fork, and not distinguishing. Excluded.
- **punchbowl / regularizePSF / solpolpy** (PUNCH pipeline) — the 2023 presentation in Field 27 says
  the PUNCH packages "heavily leverage … CCSDSPy", but `punchbowl`'s current
  `pyproject.toml` dependency list contains no `ccsdspy` entry, so there is no verifiable present-day
  relationship to cite. Excluded.
- CCSDSPy has no predecessor and was not forked from anything: the repository was created
  2017-05-24 by Daniel da Silva as an original work.

---

### 30. Interoperable Software (OPTIONAL)
1. `https://github.com/CCSDSPy/SPaC-Kit` — **SPaC-Kit** (Space Packet as Code Kit)

*Source and cited evidence of a demonstrated exchange* — this clears the Field 30 bar on three
independent counts:
- **A companion release announced by CCSDSPy itself.** CHANGELOG.rst, 2.0.0 entry: "Coinciding with
  this release is the release of SPaC-kit… SPaC-kit **extends the capabilities of ccsdspy** to
  streamline CCSDS Space Packet management for flight missions. It provides a GitHub repository
  template for defining and documenting mission packet formats… **Mission-specific packet definitions
  are distributed as SPaC-kit plugins** and can be used with SPaC-kit utilities to parse and generate
  test datasets."
- **A declared plugin/extension architecture built on CCSDSPy.** SPaC-Kit's README: "SpaC-Kit
  supports mission or instrument-specific CCSDS packet structures **via plugin packages built on the
  CCSDSPy library**", with the published plugin being
  `https://github.com/nasa-jpl/spac-kit-europa-clipper`.
- **A concrete, version-pinned API consumption.** SPaC-Kit's `pyproject.toml` declares
  `ccsdspy (>=2.0.0,<3.0.0)`; its `spac-parse`, `spac-ls`, and `spac-generate` console scripts consume
  CCSDSPy packet definitions and CCSDSPy-decoded output and export it to Pandas DataFrames, Excel, and
  CSV, and drive CCSDSPy's synthetic-packet generation. Both projects live in the same GitHub
  organisation (`CCSDSPy/ccsdspy`, `CCSDSPy/SPaC-Kit`).
*Identifier form:* the repository URL is recorded because SPaC-Kit has no DOI — Zenodo and DataCite
searches return no record, and its PyPI project (`spac_kit`, 1.0.1) publishes only
`Homepage = https://github.com/CCSDSPy/SPaC-Kit`. The field's instructions explicitly permit a
repository link when no DOI exists.
*Exclusions:* identical to the Field 29 audit trail above — numpy, bitstruct, pyyaml, appdirs, the
test/docs toolchain, astropy (dependency deliberately removed in 0.0.8), sunpy (attributed code
borrowing only), and the PUNCH packages (no verifiable current dependency). No entry rests on
"part of the standard scientific Python ecosystem" or "a PyHC member, so it interoperates with PyHC
packages".

---

### 31. Related Instruments (OPTIONAL)
Not found — **no instrument entries. Deliberate, documented omission at the relevance gate.**



*This is a relevance decision, not a resolution failure.*

*Reasoning:*
1. **CCSDSPy contains no instrument-specific code of any kind.** No instrument name, APID table,
   calibration coefficient, or mission convention appears anywhere in the installable package
   (`ccsdspy/*.py`, `ccsdspy/data/config.yml`). What it implements is the **CCSDS Space Packet
   Protocol primary header** (`_prepend_primary_header_fields()`, `ccsdspy/decode.py`,
   `docs/user-guide/ccsds.rst` citing CCSDS 133.0-B-2) — a cross-agency, multi-mission standard.
   Under this field's own rules, generic support for a multi-instrument *format* belongs in
   Input/Output File Formats (Field 18/19, where it is recorded as `Other`), not here. CCSDSPy is the
   packet-format analogue of a FITS or CDF library.
2. **The "Used By" list is precisely the excluded evidence class.** README.rst and `docs/index.rst`
   show logos for GOES-R, Europa Clipper, MMS, PACE, HERMES, the Canadian Space Agency, PUNCH,
   SPHEREx, ELFIN, and PADRE, and the Zenodo/GitHub description says "Library used in flight missions
   at NASA, NOAA, and SWRI". These are adopter name-drops — the section closes with an open
   invitation, "Do you know of other missions that use CCSDSPy? Let us know through a github issue!"
   The library behaves identically for all of them and for any mission not on the list.
3. **In-repo mission telemetry is regression-test fixture data, not instrument support.** Real or
   realistic packets exist under `ccsdspy/tests/data/europa_clipper/apid012*.tlm`,
   `.../csa/apid00400.tlm`, and `.../split/CYGNSS_F7_L0_*.tlm`, but the tests that use them exercise
   *generic* decoder bugs and build their field layouts inline: `test_regression.py:93` targets
   "odd-length integers being negative" (issue #76) and `test_regression.py:258` uses the CSA file for
   another generic decode bug. No mission's packet definition ships in the package, and
   `ccsdspy/tests/data/hs/README.rst` records that the `hs` set is synthetic.
4. **Decisively: mission- and instrument-specific definitions live in a separate plugin ecosystem.**
   CHANGELOG.rst 2.0.0: "Mission-specific packet definitions are distributed as SPaC-kit plugins";
   SPaC-Kit's README: "SpaC-Kit supports mission or instrument-specific CCSDS packet structures via
   plugin packages built on the CCSDSPy library", the published example being
   `nasa-jpl/spac-kit-europa-clipper`. This field's rules exclude instruments belonging to a separate
   ecosystem/plugin package — they belong to *that package's* record, not to the umbrella framework's.
5. **Both sanity checks fail.** A user searching HSSI for a specific instrument wants that
   instrument's science software, not a generic packet library; and someone working with a given
   instrument's science data would not reach for CCSDSPy.

*Vocabulary due diligence:* resolvable SPASE rows exist for six of the ten "Used By" missions — for
example instrument rows `Narrow Field Imager`
(`https://spase-metadata.org/NASA/Instrument/PUNCH/NFI`) and four `Solar Ultraviolet Imager` rows
(`.../NOAA/Instrument/GOES/{16,17,18,19}/SUVI`) — and none exist for Europa Clipper, the Canadian
Space Agency, PACE, or SPHEREx. They are omitted on relevance, not because they could not be
resolved.

*On the Canadian Space Agency specifically:* it is one of the ten entries in the "Used By" section,
and it has no row in the vocabulary — the only Canada-related rows are ground stations and
magnetometer/VLF arrays (CARISMA/CANOPUS, CANMAG, the GO-ABOVE VLF receivers, the IUGONET
Athabasca/Kapuskasing/Nain instruments), none of which is the agency. That is expected: the CSA is a
**space agency, not a mission, observatory, or instrument**, so nothing in a SPASE-backed
instrument/observatory vocabulary can represent it. It is therefore an omission under ladder rule 5
(nothing defensible resolves), independently of the relevance gate that already excludes it.

---

### 32. Related Observatories (OPTIONAL)
Not found — **no observatory entries. Deliberate, documented omission at the relevance gate.**



*Source:* The five-point analysis under Field 31 applies unchanged at the mission/observatory level.
CCSDSPy directly works with no *specific* mission's data products, implements no mission's
conventions, is not a mission-team tool, and models or visualizes no mission's measurements. It
implements one multi-mission telecommunications standard, and the mission-specific layer is
explicitly delegated to SPaC-kit plugin packages. Consistent with this, Field 17 deliberately does
**not** select `Observatory/Mission-specific`.

*Due diligence:* candidate observatory rows (`type: 2`) that *would* have resolved cleanly if the
relevance gate had been met include `Magnetospheric Multiscale`
(`https://spase-metadata.org/SMWG/Observatory/MMS`), `PUNCH Mission`
(`https://spase-metadata.org/NASA/Observatory/PUNCH`), `Heliophysics Environmental and Radiation
Measurement Experiment Suite` (`.../SMWG/Observatory/HERMES`), `Solar Polarization and Directivity
X-Ray Experiment` (`.../SMWG/Observatory/PADRE`), `Electron Losses and Fields Investigation A,
CubeSat` (`.../SMWG/Observatory/ELFIN/A`), and `Geostationary Operational Environmental Satellite
16`–`19` (`.../{SMWG,NOAA}/Observatory/GOES/{16,17,18,19}`). No row exists for Europa Clipper, the
Canadian Space Agency, PACE, or SPHEREx — and in the CSA's case none can, because it is a **space
agency, not a mission or observatory** (see the note under Field 31), making it a ladder rule-5
omission independent of the relevance gate. **No name is recorded without a SPASE identifier, and
nothing is flagged as ambiguous** — every one of these is omitted on relevance, which this field's
guidance treats as a correct outcome.

---

### 33. Logo (OPTIONAL)
`https://docs.ccsdspy.org/en/latest/_static/logo.png`

*Source:* Two independent sources agree, and the URL was verified to resolve and serve the image. The curated
PyHC registry lists exactly `logo: https://docs.ccsdspy.org/en/latest/_static/logo.png` for CCSDSPy,
and the asset exists in the repository at `docs/_static/logo.png`, published to the project's
canonical documentation host (see Field 24) and referenced by `docs/_templates/logo.html`. This is a
permanent, publicly accessible location, as the field requires.
