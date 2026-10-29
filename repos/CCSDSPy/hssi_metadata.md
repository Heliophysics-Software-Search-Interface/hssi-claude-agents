# HSSI Metadata Extraction Results

**HSSI Software ID:** aade4249-dedf-4938-9ad1-432553bf0c36
**Repository:** https://github.com/ccsdspy/ccsdspy
**Source Revision:** 4d91371fc9d07535d583fe9c28a4db39f5096a2a
**Extraction Date:** 2026-07-30
**Validation Date:** 2026-10-29
**Validation Status:** PASS

This file records the HSSI metadata for CCSDSPy, reconciled against the pinned source revision and
authoritative external sources. It was extracted on 2026-07-30 and brought forward on 2026-10-28 and
2026-10-29 for the 2.1.0 release. Evidence that names revision `ce84316`
(`ce84316b5f41dd40f32da5e69ec2e265885d56b9`, the `2.1.0` tag and the default branch's head on both
days) was read there, and evidence that names another tag was read at that tag; the tree at
`ce84316` differs from the preceding head, `0d2ce3f`, only in CHANGELOG.rst. All other evidence was
read at the Source Revision above.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]



---

### 2. Persistent Identifier (RECOMMENDED)
`https://doi.org/10.5281/zenodo.7819990`

*Source:* This is the Zenodo **concept** DOI (all-versions DOI), which is what this field asks
for. `https://zenodo.org/api/records/7819991` returns `conceptdoi: 10.5281/zenodo.7819990` and
`conceptrecid: 7819990`; DataCite for `10.5281/zenodo.7819990` reports
`versionCount: 1, versionOfCount: 0` with `HasVersion → 10.5281/zenodo.7819991`.
*Note:* The README.rst and docs/index.rst badges point at the **version** DOI
`10.5281/zenodo.7819991` (v1.1.0), which would be the wrong value for this field; the concept DOI
is the right one.

---

### 3. Code Repository (MANDATORY)
`https://github.com/ccsdspy/ccsdspy`

*Source:* The repository's `origin` remote is `https://github.com/ccsdspy/ccsdspy`, and the URL serves
the repository.
*Note:* GitHub's canonical casing of the owner is `CCSDSPy` (`full_name: "CCSDSPy/ccsdspy"` from the
GitHub API). GitHub owner/repo paths are case-insensitive and the lower-case URL resolves to the same
repository, so the difference is cosmetic and the lower-case form stands (Field 3 rule 6).

---

### 4. Software Functionality (RECOMMENDED)
- Data Processing and Analysis
- Data Processing and Analysis: Packet Decommutation
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Processing
- Mission-related
- Mission-related: Packet Decommutation
- Mission-related: Ingest
- Mission-related: System Testing



*Evidence per value:*

- **Data Processing and Analysis** — required parent; the package's whole purpose is
  reading and transforming spacecraft data.
- **Data Processing and Analysis: Packet Decommutation** — the core capability.
  `ccsdspy/decode.py` (`_decode_fixed_length`, `_decode_variable_length`) parses tightly-packed,
  non-byte-aligned bit fields out of raw CCSDS Space Packet binary into NumPy arrays;
  `ccsdspy/packet_types.py` exposes it as `FixedLength.load()` / `VariableLength.load()`;
  `ccsdspy/packet_fields.py` defines the `PacketField` / `PacketArray` layout DSL
  (`uint`/`int`/`float`/`str`/`fill`, arbitrary `bit_length`, `byte_order` of `big`/`little`/`"3412"`).
- **Data Processing and Analysis: Calibration** — matches the subcategory's definition in
  `fields/04-software-functionality.md`, "Converting raw instrument data to physical units".
  `ccsdspy/converters.py` module docstring: "applies post-process to decoded packet fields. This
  post-processing includes applying linear/polynomial calibration curves, dictionary replacement, and
  time parsing." `PolyConverter` docstring: "applies calibration using a series of coefficients ordered
  from highest power to intercept"; `LinearConverter` is the y=mx+b case. Exercised in
  `ccsdspy/tests/test_converters.py` and documented at `docs/user-guide/converters.rst`.
- **Data Processing and Analysis: Processing** — a real post-decode processing pipeline, not
  just decoding: `_apply_converters()` and `_apply_post_byte_reoderings()` in
  `ccsdspy/packet_types.py`, `_do_array_byte_reordering()` for arbitrary byte orders,
  `_expand_array_fields()` / `_unexpand_field_arrays()` for multidimensional array fields, plus
  `EnumConverter` (int→string replacement), `DatetimeConverter` (coarse/fine offsets from a reference
  epoch, multi-input-field), and `StringifyBytesConverter` (bin/hex/oct).
- **Mission-related** — required parent for the three below.
- **Mission-related: Packet Decommutation** — the vocabulary carries a second
  `Packet Decommutation` row under `Mission-related`, and this library is the archetype: it is
  deployed inside flight-mission ground data systems (Zenodo/GitHub description: "Library used in
  flight missions at NASA, NOAA, and SWRI"; README.rst and docs/index.rst "Used By" list eleven
  missions at `ce84316`, STRIVE having joined in commit `a5438ce`). Its subject matter is
  mission-operations, not science analysis: CCSDS primary-header semantics (APID, sequence count,
  telemetry-vs-command packet type, secondary-header flag) are implemented in
  `_prepend_primary_header_fields()` and `utils.read_primary_headers()`.
- **Mission-related: Ingest** — CCSDSPy ships the classic Level-0 ingest step:
  `utils.split_by_apid()` splits a mixed-APID downlink stream into per-APID streams, exposed as a
  command-line tool in `ccsdspy/__main__.py` (`python -m ccsdspy split <file> --valid-apids`) that
  writes `apid{apid:05d}.tlm` files; `utils.validate()` (added in 1.4.0) performs ingest-time file
  QA — truncation/extra-byte detection, unknown APIDs, and missing or out-of-order sequence counts —
  returning a list of `logging.LogRecord`s. Since 2.1.0 (commit `5c3babd`, PR #166)
  `utils.iter_packet_bytes()` also reads a blocking binary stream incrementally, combining short reads
  and yielding each packet as soon as it is complete (`_read_bytes()`; `docs/user-guide/utils.rst`
  gives a connected-TCP-socket example), so the same per-packet iteration applies to a live downlink
  feed as well as to a file.
- **Mission-related: System Testing** — synthetic packet generation for verification.
  `docs/user-guide/synthetic.rst`: "It is sometimes necessary or useful to generate synthetic CCSDS
  packets with known data for testing and validation." Implemented as
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
- **Mission-related: Monitoring**, **Mission-related: Operations** — weighed for the blocking-stream
  input `utils.iter_packet_bytes()` gained in 2.1.0. CCSDSPy yields packets from a stream the caller
  has already connected; it performs no limit checking, health or status display, commanding, or
  scheduling, so neither row describes it. The stream input is ingest and decommutation, already
  recorded above. `Data Processing and Analysis: Data Access and Retrieval` stays excluded on the same
  reading: the caller opens the socket, and CCSDSPy queries no archive.
- **Mission-related: Processing** — CCSDSPy runs no mission's processing chain. Its post-decode
  processing (converters, byte reordering, array expansion) is generic and applies to whatever packet
  definition the user supplies; mission-specific definitions and their use live in SPaC-kit plugins
  and in the missions' own pipelines. That processing is recorded as
  `Data Processing and Analysis: Processing`.
- **Mission-related: Science Data Processing** — CCSDSPy produces no science data product: its only
  file output is CCSDS packet binary (Field 19), and decoded results are returned in memory as NumPy
  arrays. Producing a mission's archive-standard science files is done downstream of it.

---

### 5. Related Region (RECOMMENDED)
Not found — **no region. Deliberate, evidenced-empty value (rule 2).**



*Why empty:* CCSDSPy is a packet-format library. It decodes and encodes the CCSDS Space Packet
Protocol and behaves identically whatever physical domain the packets describe (see Fields 4, 18 and
31), which is the domain-independent case of rule 2. A word-anchored, case-insensitive sweep of the
tree at `ce84316` (binary `.tlm`/`.bin`/image fixtures excluded) finds no `magnetospher*`,
`ionospher*`, `thermospher*`, `mesospher*`, `heliospher*`, `atmospher*`, `interplanetary`,
`corona`/`coronal`, `photospher*`, `chromospher*`, `aurora`/`auroral`, `plasma`, `solar wind`,
`magnetotail`, `magnetosheath`, `heliosheath`, or planet name, while the positive control `ccsds`
matches throughout the package. The only `solar` and `sun` matches are spacecraft-engineering
housekeeping mnemonics — sun sensors, solar-array currents and voltages, sun-pointing modes — in the
CYGNSS packet-definition fixtures under `ccsdspy/tests/data/split/defs/`; they are test data and
describe the spacecraft bus, not the physics of a region (rule 4). Neither the code nor the project's
own descriptions (`pyproject.toml` `description`, the GitHub and Zenodo description, README.rst,
`docs/index.rst`) names a region. The field is RECOMMENDED, so a documented empty value is legitimate
(rule 9).

*Superseded value.* HSSI held six rows until this update, in this stored order: `Earth Magnetosphere`,
`Solar Environment`, `Earth Ionosphere`, `Earth Thermosphere`, `Earth Lower and Middle Atmosphere`,
`Interplanetary Space`. The 2026-07-30 extraction kept and extended them because it read this field as
mandatory and so needed some basis for a value; the field is RECOMMENDED, and every row rested on a
borrowed label that rule 3 excludes, so rule 8 clears them:

- `Earth Magnetosphere`, `Earth Ionosphere`, `Earth Thermosphere`, `Earth Lower and Middle Atmosphere`
  and `Interplanetary Space` were mapped from the PyHC registry's Science Area facet tags for CCSDSPy
  (`magnetosphere`, `ionosphere_thermosphere_mesosphere`, `heliosphere` — `_data/projects.yml`, the
  CCSDSPy entry at lines 101–114 of
  `heliophysicsPy/heliophysicsPy.github.io@f7b0421b08c2cbc614a8d68372b42428d3a53cb2`). A registry facet
  tag is not evidence for a region.
- `Solar Environment` was supported only by the solar missions in the README "Used By" list (PUNCH,
  GOES-R/SUVI, PADRE), that is, by the regions of missions that use the software.

*Considered and rejected (recognise these on sight):*

- **Corona**, **Solar Wind** — would rest only on the "Used By" listing of PUNCH (rule 3).
- **Jupiter Magnetosphere** — Europa Clipper telemetry is shipped in-repo
  (`ccsdspy/tests/data/europa_clipper/apid012*.tlm`), but only as regression fixtures for generic
  bit-packing bugs (`ccsdspy/tests/test_regression.py:93`, issue #76): the missions whose files appear
  as test fixtures are not evidence (rule 3).
- **A region for STRIVE** (added to "Used By" in commit `a5438ce`) **or any other listed mission** — a
  consuming mission's region (rule 3).
- **A solar row from the sun-sensor and solar-array fixture mnemonics** — spacecraft engineering, not
  region physics (rule 4).

*Condition for revisiting:* region-specific code, or a stated region purpose in the project's own
description.

---

### 6. Authors (MANDATORY)
Authors are listed in HSSI's stored order.

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
5. **Daniel da Silva** (given name `Daniel`, family name `da Silva`)
   - Author Identifier: `https://orcid.org/0000-0001-7537-3539`
   - Affiliation: Goddard Space Flight Center — `https://ror.org/0171mag52`
   - Affiliation: Laboratory for Atmospheric and Space Physics — `https://ror.org/01fcjzv38`



*Source:* The repository contains **no** CITATION.cff, codemeta.json, .zenodo.json, AUTHORS, or
CONTRIBUTORS file. The authoritative author list is the DataCite/Zenodo record for the Field 2
concept DOI, whose five `creators` are exactly these five people with exactly these four ORCIDs.
`pyproject.toml` `[project].authors` names a subset — Daniel da Silva `<mail@danieldasilva.org>` and
Steven Christe `<steven.d.christe@nasa.gov>`. The four ROR identifiers resolve in the ROR v2 API to
the organizations they are recorded for: `0171mag52` = "Goddard Space Flight Center" (GSFC),
`02z5nhe81` = "National Oceanic and Atmospheric Administration", `02ttsq026` = "University of
Colorado Boulder", `03tghng59` = "Southwest Research Institute". `Goddard Space Flight Center` is
ROR's own display name (not an unexpanded acronym), so it is the correct name as it stands. ROR has
no record for **PickNik Robotics** (a private robotics company), so that affiliation correctly
carries no identifier. ORCID employment records corroborate: Christe → NASA Goddard Space Flight
Center, Solar Physics Laboratory; Hughes → Southwest Research Institute Boulder; da Silva → NASA
Goddard Space Flight Center; Codrescu lists no employments (his NOAA and CU Boulder affiliations rest
on the DOI record's authority).

**Name split (rule 11).** The ORCID record `0000-0001-7537-3539` gives given-names `Daniel` and
family-name `da Silva`, so the split is `Daniel` / `da Silva`, with the surname particle kept in the
family name. HSSI's shared Person row for this ORCID stored givenName `Daniel da` / familyName `Silva`
until this update: the same words split differently, which rule 11 corrects on the row itself, so the
corrected split shows on every entry the row serves.

**Second affiliation for author 5.**
The DataCite/Zenodo record gives Daniel da Silva's affiliation as the single combined string
`"NASA Goddard Spaceflight Center, Laboratory for Atmospheric and Space Physics"`, naming two
institutions. HSSI stored only the Goddard half until the 2026-07-30 refresh, which recorded
**Laboratory for Atmospheric and Space Physics** (`https://ror.org/01fcjzv38`) as his second
affiliation. Rationale: Zenodo's `creators` entry is the authoritative author source for this software,
it names both institutions, and the Goddard-only value captured only half of what that source says —
so the second affiliation restores information the DOI autofill lost rather
than inventing any. The counter-signal is
noted for completeness: his ORCID record lists NASA Goddard Space Flight Center only.

**Additional contributors considered.**
`git shortlog -sne ce84316` (the default branch's history at that revision) shows these contributors,
none of whom appears in any author source: **Joshua Garde** (`jgarde@jpl.nasa.gov`, 31 commits),
**Thomas Loubrieu** (`@jpl.nasa.gov`, 8), **Andrew Robbertz** (8), **Gwyn Fireman** (`@nasa.gov`, 3),
**Luna Smith** (2; PR #157), **karlhillx** (2; PR #158 for issue #156, and PR #160), **Derek Lamb**
(2, under an `@swri.org` address and a GitHub noreply address; PR #163), **Thanasi Pantazides** (1;
PR #161), **Giovanni Cozzolongo** (1; PR #166), and **MattyG** (`meawoppl@gmail.com`, 1). Counted over
all branches (`git shortlog -sne --all`) some totals are higher (Garde 33; Loubrieu 10 across two
addresses), because unmerged branches carry extra commits.

**None of them is an author (rule 5).** No source in the candidate pool names any of them: the
Zenodo/DataCite record lists only the five `creators` above and no `contributors`, `pyproject.toml`
`[project].authors` names only Daniel da Silva and Steven Christe, and the repository has no
CITATION.cff, codemeta.json, AUTHORS, CONTRIBUTORS or .zenodo.json file. Commit history evidences
contribution, not authorship, and a committer absent from every attestation is not an author whatever
the commit count; karlhillx and Derek Lamb, who reached two commits each after the Source Revision, are
decided the same way. The fact that the Zenodo record has not been updated since v1.1.0 (2023-04-12)
even though the releases from 1.2.0 to 2.1.0 shipped substantial new work was weighed as an argument
that the credited list may be stale; it did not change the outcome, because staleness of the
authoritative source is not itself evidence of who should be added. Should the maintainers publish a
CITATION.cff or refresh the Zenodo deposit, this decision should be revisited.

---

### 7. Software Name (MANDATORY)
`CCSDSPy`

*Source:* DataCite/Zenodo title, `docs/index.rst` heading, and the PyHC registry `name` field all
give `CCSDSPy`. The PyPI distribution and Python import name are lower-case `ccsdspy`; the
capitalized display form is the correct name for this field.

---

### 8. Description (MANDATORY)
I/O interface and utilities for CCSDS binary spacecraft data in Python. Library used in flight missions at NASA, NOAA, and SWRI. CCSDSPy provides a Python interface for reading and writing the tightly packed bits of the Consultative Committee for Space Data Systems (CCSDS) Space Packet Protocol, the low-level telemetry format used by many NASA and ESA missions. Users describe a packet's layout declaratively with PacketField and PacketArray objects — or load that layout from a CSV definition file — and CCSDSPy decodes a binary telemetry file into a dictionary of NumPy arrays using vectorized shifting and masking. The FixedLength class handles packets whose layout never changes, while the VariableLength class handles packets containing a field that expands to fill the packet or whose length is set by another field. Fields need not be byte-aligned and may have odd bit lengths, unsigned or signed integer, IEEE floating point, string, or fill types, and big-endian, little-endian, or arbitrary byte orderings. A converter system applies post-processing to decoded fields, including linear and polynomial calibration curves, integer-to-string enumeration replacement, datetime construction from coarse and fine time offsets against a reference epoch, and byte stringification in binary, hexadecimal, or octal. Utility functions read primary headers, split a mixed-APID downlink stream by APID (also available as a `python -m ccsdspy split` command line tool), iterate over or count packets, and validate a packet file for truncation, extra bytes, unknown APIDs, and missing or out-of-order sequence counts. Both packet classes can also write synthetic CCSDS packet files from user-supplied arrays for testing and validation. The library is pure Python, is developed with requirements sourced from the community, is extensively tested, and is a Python in Heliophysics Community (PyHC) package.

*Sources:* the opening two sentences are the Zenodo abstract verbatim (the GitHub repository
description is the same text without the final period); the rest draws on README.rst (opening
paragraph, Usage Example, Installation),
`docs/index.rst` ("Brief Tour": "highly efficient vectorized shifting and masking"),
`docs/user-guide/ccsds.rst`, `docs/user-guide/synthetic.rst`, `docs/user-guide/loadfile.rst`,
`docs/user-guide/utils.rst`, `ccsdspy/packet_fields.py` (data types and `byte_order`),
`ccsdspy/packet_types.py` (`FixedLength` / `VariableLength` docstrings), `ccsdspy/converters.py`
(the five converter classes), `ccsdspy/utils.py` (`read_primary_headers`, `split_by_apid`,
`iter_packet_bytes`, `count_packets`, `validate`), `ccsdspy/__main__.py` (the `split` CLI), and the
PyHC registry entry.

*Stream input (rule 6):* the blocking-stream input `utils.iter_packet_bytes()` gained in 2.1.0
(PR #166) is covered by the description's "iterate over … packets", and none of
README.rst, `docs/index.rst`, the `pyproject.toml` `description` or the GitHub description names it,
so rule 3 does not fire; every claim in the description has code support at `ce84316`. Revisit
under rule 3 if the project's own description comes to name stream input.

---

### 9. Concise Description (OPTIONAL, ≤200 characters)
I/O interface and utilities for CCSDS binary spacecraft data in Python. Library used in flight missions at NASA, NOAA, and SWRI.

*Reasoning:* Field 8 opens with this string and goes on to a full account of the software, so the two
fields do not duplicate each other and this one can stay a one-line preview. This string is the
maintainers' own one-line summary — the Zenodo abstract verbatim, and the GitHub repository
description apart from its final period — and a good ≤200-character preview. Rule 5 keeps it: a
stylistic alternative is not fresh metadata.

---

### 10. Publication Date (RECOMMENDED)
`2017-06-29`



*Why 2017-06-29:* `fields/10-publication-date.md` defines this field as the "[d]ate of first
broadcast/publication", to be "[u]sed for the initial version of the software". CCSDSPy's first public
publication was the PyPI release of version `0.0.7` on **2017-06-29**
(`https://pypi.org/pypi/ccsdspy/json`, `releases["0.0.7"][0].upload_time = 2017-06-29T00:15:49`),
which is corroborated by the GitHub repository having been created 2017-05-24.

*Superseded value.* HSSI held `2023-04-12` until the 2026-07-30 refresh. That is DataCite's `Issued`
date for the concept DOI (`dates[] → {date: "2023-04-12", dateType: "Issued"}`; Zenodo
`metadata.publication_date`), i.e. the date Zenodo *minted the DOI* — nearly six years and thirteen
releases after first publication. It is an artifact of when the maintainers set up DOI integration,
not a publication date for the initial version, so it does not satisfy this field's definition.

---

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** `https://zenodo.org`

*Source:* DataCite `publisher: "Zenodo"`. Correct per the field guidance ("For software where a DOI
has been obtained through Zenodo … Zenodo is the correct entry").

---

### 12. Version (RECOMMENDED)
- **Version Number:** `2.1.0`
- **Version Date:** `2026-10-28`
- **Version Description:**
  * The function `utils.iter_packet_bytes()` now supports reading from blocking binary streams, such as from a socket. The user is responsibile for aligning the stream so that reading starts at the beginning of a packet. See an example at :doc:`/user-guide/utils`.
  * When loading array fields from a CSV file, the array dimensions may now include whitespace
  * A packet APID, name, and description can now be specified when loading a packet definition from a CSV
- **Version PID:** Not found



The description is exactly these three `* ` bullet lines, joined by single newlines.

*Why 2.1.0 is the current release (rule 3):* `2.1.0` is an annotated tag (tagger Daniel da Silva,
2026-10-28T04:17:16Z, message "Release version 2.1.0") on commit
`ce84316b5f41dd40f32da5e69ec2e265885d56b9` ("Update changelog for 2.1.0"), which was the default
branch's head on 2026-10-28 and 2026-10-29; `2.0.1` and `2.0.0` are its ancestors. PyPI's JSON API
lists `ccsdspy-2.1.0.tar.gz`, uploaded 2026-10-28T04:17:46Z, and its `info.version` is `2.1.0`. The
version is dynamic (`dynamic = ["version"]` with `setuptools_scm` in `pyproject.toml`), so the tag is
what declares it, and nothing marks it a pre-release. The repository still publishes no GitHub
Releases (`/releases` returns an empty list), so the tag and PyPI are the release record. The number
is written without a `v`, as the tag and 2.0.0 are.

*Version date* `2026-10-28` is the release event's UTC calendar day (rule 7): with no GitHub release
object, the annotated tag's date (2026-10-28T04:17:16Z) and the tagged commit's (2026-10-28T04:15:25Z)
fall on 2026-10-28 UTC, corroborated by the PyPI upload at 04:17:46Z. CHANGELOG.rst's heading
"Version 2.1.0 - 2026-10-28" gives the same day.

*Version description* comes from the CHANGELOG.rst 2.1.0 entry, the only release text: there is no
GitHub release and no Zenodo deposit for 2.1.0 (rule 13). Three of its four items describe new or
changed behaviour a user meets and are kept verbatim, as bullets (rules 14 and 15): stream input for
`utils.iter_packet_bytes()` (commit `5c3babd`, PR #166), whitespace in CSV array dimensions
(`a3fe884`, PR #161), and an APID, name and description when loading a packet definition from a CSV
(`f06e5fb`, PR #160 for issue #159). The fourth, "Fixed missing import in Synthetic Packets
Documentation", corrects a documentation example; it is docs housekeeping (rule 14) and is dropped
whole (rule 15). Two of the kept items end in a reStructuredText link reference,
"(`Pull Request #161 <https://github.com/CCSDSPy/ccsdspy/pull/161>`_)" and
"(`Issue #159 <https://github.com/CCSDSPy/ccsdspy/issues/159>`_)". These trailing references are
dropped: rule 15 allows dropping a trailing pull-request credit, the issue reference has the same
trailing form, and RST link syntax would show as raw markup under the page's markdown "Release Notes".
The first item's closing sentence, "See an example at :doc:`/user-guide/utils`.", is part of the
item's own text, not a trailing credit, so it stays, as does the project's spelling "responsibile".
Nothing else in any item is changed.

*Version PID is genuinely absent (rule 18).* On 2026-10-28 Zenodo still held exactly one deposit for
this software: the concept `10.5281/zenodo.7819990` lists one version, `10.5281/zenodo.7819991`
(`metadata.version: "1.1.0"`), and DataCite reports `versionCount: 1`. No version-specific DOI exists
for 2.1.0, as none existed for 2.0.0 or 2.0.1. *Observation for the maintainers (no metadata action):*
the absence is structural — the project tags releases in git but never publishes a GitHub *Release*,
which is the event the GitHub→Zenodo integration listens for. Publishing an actual GitHub Release
would restore version-DOI minting and let this field be populated in future.

*Superseded values.* HSSI held `2.0.0` (release date 2026-06-10, no version PID) until this update.
2.0.0 was a correctly dated release (tag `2.0.0` on commit `f1bc1f428b74c887a4c9f0a02e62ad6f6445465f`,
2026-06-10T21:47:16Z; PyPI upload 21:47:29Z), but its stored description was a curator's summary of the
CHANGELOG.rst 2.0.0 entry rather than the entry's own items, which rule 15 does not allow. Nothing of it
is carried onto 2.1.0 (rule 10). Before 2026-07-30 HSSI held `1.1.0`, and each of its sub-fields was
wrong:

- **The number was stale.** 1.1.0 was released 2023-04-11, nine releases and three years before the
  2026-07-30 extraction.
- **`release_date: 2024-12-29` matched no release at all.** It is exactly the Zenodo record's own
  last-`updated` timestamp (2024-12-29T01:22:45), a metadata-modification time captured in place of a
  release date. 1.1.0's git tag commit is dated 2023-04-11 and the PyPI upload of
  `ccsdspy-1.1.0-r1.tar.gz` is 2023-04-11T15:23:17.
- **`version_pid` `https://doi.org/10.5281/zenodo.7819991` is 1.1.0's own version DOI** (Zenodo record
  7819991 reports `metadata.version: "1.1.0"`); it does not identify any later release and never will.
  The concept DOI `…7819990` belongs in Field 2.
- **The description was not a version description.** It duplicated the Field 8 software summary and
  said nothing about what changed in the release.

*Release history notes.*

- **2.0.1** was released between 2.0.0 and 2.1.0 and never recorded in HSSI: an annotated tag on
  commit `6d018f92d87b7e066f34ab828f25ac162e9746bd` at 2026-08-13T00:49:38Z (2026-08-12 20:49:38
  −0400), with its PyPI upload at 2026-08-13T00:50:27Z. Its UTC release day is 2026-08-13;
  CHANGELOG.rst's heading "Version 2.0.1 - 2026-08-12" is the maintainer's local (UTC−4) calendar day,
  which never overrides the release event (rule 8). Its two items are bug fixes: logging to a file off
  by default (issue #156) and fill-field encoding (PR #157).
- CHANGELOG.rst documents a "Version 1.4.3 - 2025-11-06" that exists on PyPI (uploaded 2025-11-05) but
  was never git-tagged; it is superseded either way.

*No unreleased commits.* On 2026-10-29 the default branch's head was still the `2.1.0` tag itself, so
every commit after 2.0.1 shipped in 2.1.0. A later release update starts from the commits after
`ce84316`.

---

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source:* `pyproject.toml` `requires-python = ">=3.10"` with trove classifiers for Python 3.10–3.13;
CI matrix `python-version: ["3.10", "3.11", "3.12", "3.13"]`
(`.github/workflows/ccsdspy-ci.yml`). Pure Python — the repository contains no C, Fortran, or other
compiled source.

---

### 14. Reference Publication (OPTIONAL)
Not found

*Source:* No DOI'd publication describes the software. There is no JOSS paper; a DataCite query for
`ccsdspy` returns only the two Zenodo software DOIs plus the two DOIs of the DASH 2023 slide deck
weighed under Field 27, which names the software in its abstract but does not describe it. The closest
artifact is the ADASS 2018 poster "CCSDSPy - Convenient Decoding of Binary Spacecraft Telemetry" by
Daniel da Silva, known only from its conference abstract page
(https://adass2018.astro.umd.edu/abstracts/P7.2.html; see Field 27). A poster, slide deck or
conference abstract is never this field's value, whatever its subject (rule 2), and no ADASS XXVIII
proceedings paper by him was found (Field 27). README.rst's "Acknowledging or Citing ccsdspy" section
directs citers to the Zenodo DOI, not to a paper.

---

### 15. License (RECOMMENDED)
- **License:** `BSD 3-Clause "New" or "Revised" License`
- **License URI:** `https://spdx.org/licenses/BSD-3-Clause.html`



*Evidence the earlier BSD 2-Clause value was wrong (HSSI held `BSD 2-Clause "Simplified" License`
until the 2026-07-30 refresh):*
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

*Where the earlier value came from:* the DOI autofill. Zenodo's record carries
`metadata.license: {"id": "bsd-2-clause-netbsd"}` and DataCite renders that as
`BSD 2-Clause "Simplified" License`. The Zenodo deposit's licence field is simply mis-set (it names
the NetBSD 2-clause variant, which the repository does not use); the repository's own LICENSE file is
authoritative. `pyproject.toml` only says `License :: OSI Approved :: BSD License`, which does not
distinguish the variants.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
binary, calibration, ccsds, decoding, esa, nasa, operations, packet parsing, packets, pyhc package,
python, science, space, space data systems, space packet protocol, spacecraft data, telemetry



*Sources:* the GitHub topics and the Zenodo keywords give `binary`, `ccsds`, `decoding`, `operations`,
`packets`, `python`, `science` and `space`. The others come from:
- `nasa`, `space packet protocol` — `pyproject.toml`
  `keywords = ["python", "nasa", "ccsds", "space packet protocol"]`, the maintainers' own list.
- `telemetry` — README.rst / `docs/index.rst`: "used for many NASA and ESA missions for low-level
  telemetry".
- `spacecraft data` — the software's own description: "CCSDS binary spacecraft data".
- `space data systems` — the expansion of CCSDS, "Consultative Committee for Space Data Systems"
  (`docs/user-guide/ccsds.rst`).
- `packet parsing` — the core capability (`ccsdspy/decode.py`, `FixedLength.load()`).
- `calibration` — `ccsdspy/converters.py` calibration curves (see Field 4).
- `esa` — README.rst / `docs/index.rst`: "used by many NASA and ESA missions".
- `pyhc package` — the PyHC package marker (rule 15). CCSDSPy is listed in the PyHC registry's
  `_data/projects.yml` (the entry at lines 101–114 of
  `heliophysicsPy/heliophysicsPy.github.io@f7b0421b08c2cbc614a8d68372b42428d3a53cb2`), so the record
  carries `pyhc package`, written exactly so.

*Not recorded:* PyHC's `specific` (a registry-internal tag, not a science keyword); `binary data` and
`data decoding` (near-duplicates of `binary` and `decoding`).

*Declined, with reasons:* `flight software` and `ground data system`
were considered and declined. Neither exists in the live `Keyword` vocabulary — nor do
`ground data systems`, `mission operations`, `spacecraft`, or `flight` — so each would mint a new
permanent row. This field's guidance is to check the live list first and reuse an existing row rather
than mint a near-duplicate, and the keywords above already cover that concept space
(`telemetry`, `space packet protocol`, `spacecraft data`, `space data systems`, `packets`,
`packet parsing`, `operations`). `data processing` *does* exist as a row but was declined as
redundant with Field 4's `Data Processing and Analysis`.

*At `ce84316`:* every term in `pyproject.toml` `keywords` and in the GitHub topics is recorded above.
`streaming` was considered for the blocking-stream input of `utils.iter_packet_bytes()`
and declined: it is one utility function's input mode rather than the software's signature technique
(rule 10), no `Keyword` row exists for it, so it would mint one, and a free-text search for "stream"
already returns this entry through Field 8 ("split a mixed-APID downlink stream").

*Removed at the 2.1.0 update (rules 3 and 13):* `heliosphere`, `magnetosphere`, `ionosphere`,
`thermosphere`. HSSI held all four until this update. They were the PyHC registry's Science Area facet
tags for CCSDSPy (`heliosphere`, `ionosphere_thermosphere_mesosphere`, `magnetosphere`), split into
single-term rows, and the registry was their only source. A registry domain tag is kept only when the
software itself works in that domain, and CCSDSPy does not: a word-anchored sweep of the tree at
`ce84316` finds none of the four terms (nor `mesosphere`), none of the project's declared keyword
sources (`pyproject.toml` `keywords`, the GitHub topics, the Zenodo keywords) lists them, and no
project description uses them (see Field 5). Do not restore them from the registry.

---

### 17. Data Sources (OPTIONAL)
- Other

*Source:* CCSDSPy has no networked data-source client at all — no HTTP/FTP/S3/HAPI/CDAWeb code
anywhere, and its only dependencies are `numpy`, `bitstruct`, `pyyaml`, `appdirs`. Its input is
a local path or a file-like object the caller supplies. At `ce84316`, `pkt.load(file)`
(`ccsdspy/packet_types.py`) and four of the `ccsdspy.utils` entry points — `split_packet_bytes()`,
`read_primary_headers()`, `split_by_apid()` and `count_packets()` — document "Path to file on the
local file system, or file-like object", reading via `np.fromfile` / `np.frombuffer`; `validate()`
documents "A file path or file-like object with a `.read()` method". Since 2.1.0,
`utils.iter_packet_bytes()` documents "Path to file on the local file system, or blocking binary
file-like object with a read(size) method" and reads through `file.read()`, so a socket stream the
caller has already connected also works; it is still caller-supplied input, not a data-source client.
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

*Source:* As data output, CCSDSPy writes exactly one thing — raw CCSDS Space Packet binary, which has
no vocabulary row, hence `Other`. Two paths: `FixedLength.to_file()` / `VariableLength.to_file()` →
`_to_file()` → `ccsdspy/encode.py` (`bitstruct.pack`), documented at `docs/user-guide/synthetic.rst`;
and the `python -m ccsdspy split` CLI in `ccsdspy/__main__.py`, which writes per-APID
`apid{apid:05d}.tlm` binary files.
*Not selected:* `JSON` — `ccsdspy/logger.py`'s `JSONFormatter` and the `log_file_json` config option
produce structured **log** files, not data output, so under this field's instruction "[o]nly formats
actually supported should be indicated" (`fields/19-output-file-formats.md`), read for *data* output,
they do not qualify; nor does `config.copy_default_config()` (`ccsdspy/config.py`), which copies the
default YAML configuration file into the user's configuration directory. In-memory results are
returned as `dict` of NumPy arrays, not written to a file format.

---

### 20. Operating System (RECOMMENDED)
- Operating System Independent
- Linux
- Mac
- Windows

*Source:*
- **`Operating System Independent`** — the maintainers' own declaration:
  `pyproject.toml` classifier `"Operating System :: OS Independent"` (also on PyPI for 2.1.0).
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
  compiled extensions of its own; PyPI 2.1.0 ships only `ccsdspy-2.1.0.tar.gz` (an sdist, no
  architecture-specific wheels), as 2.0.0 and 2.0.1 did. Byte order is handled explicitly in software
  rather than inherited from the host: `PacketField(byte_order=...)` accepts `"big"`, `"little"`, or
  an arbitrary digit string, and `_do_array_byte_reordering()` (`ccsdspy/packet_types.py`) and
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
A user searching HSSI for `phenomena:"Solar Flares"` should not get a telemetry I/O library back.
Populating this field from the phenomena studied by the missions in the README "Used By" list would
be exactly the excluded name-drop inference, and would be inconsistent with the reasoning applied in
Fields 31 and 32. A documented empty field is the correct outcome; the field is OPTIONAL.

*Re-derived at the 2.1.0 update:* none of the seven rows applies. CCSDSPy is an I/O layer with no
phenomenon-specific code (rule 2); its relation to every row is identical and indirect (rule 3); and
any link runs through the missions that use its output (rule 4). A word-anchored sweep of the tree at
`ce84316` finds no `flare`, `storm`, `CME`, `corona`/`coronal`, `solar wind` or `x-ray`; the only
`solar` and `sun` matches are spacecraft-engineering mnemonics in test fixtures (see Field 5). No value
here ever rested on the PyHC registry's facet tags, and the field stays empty.

---

### 23. Development Status (RECOMMENDED)
`Active`

*Source:* rule 6 — the software reached a stable, usable state, and its default branch has recent
commits.
- **Dated anchors:** the last commit on the default branch `main` is `ce84316` ("Update changelog for
  2.1.0"), 2026-10-28; the last release is 2.1.0, 2026-10-28 (tag and PyPI upload). Re-apply rule 6
  from these dates.
- **Stable, usable state:** `pyproject.toml` classifier `"Development Status :: 5 - Production/Stable"`,
  and a PyPI release history running from 0.0.7 (2017) to 2.1.0.
- **Rules 1–4 do not fire:** GitHub reports `archived: false`; README.rst and `docs/index.rst` carry
  no repostatus.org badge and no status statement, and nothing points to a new location.
- **Corroborating:** CI workflows run on every push and pull request to `main`, and PyHC's curated
  quality ratings for CCSDSPy are "Good" across community, documentation, testing, software maturity,
  Python 3, and license.

---

### 24. Documentation (RECOMMENDED)
`https://docs.ccsdspy.org/en/latest/`

*Source:* The project's own canonical documentation host. `https://ccsdspy.readthedocs.io/en/latest/`
**redirects** to `https://docs.ccsdspy.org/en/latest/`, and the repository's GitHub `homepage` field is
`https://ccsdspy.org`, which redirects to the same target. The curated PyHC registry independently
lists `docs: "https://docs.ccsdspy.org/en/latest/#"` — the same URL, with a trailing empty `#`
fragment dropped here as noise. Installation instructions are present at that URL
(README.rst "Installation" / `docs/index.rst` "Install ccsdspy": `pip install ccsdspy`), satisfying
this field's "[d]ocumentation link including installation instructions"
(`fields/24-documentation.md`).
*Superseded value.* HSSI held the string ``https://ccsdspy.readthedocs.io/en/latest/>`__.`` until the
2026-07-30 refresh: trailing reStructuredText hyperlink syntax scraped from README.rst's link to the
documentation, producing a URL that cannot resolve.

---

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** `https://ror.org/027ka1x80`

*Source:* The only explicit funding statement anywhere in the repository is in CHANGELOG.rst, in the
2.0.0 release entry: "Coinciding with this release is the release of SPaC-kit. Funded through a
ROSES High-Priority Open-Source Software award, SPaC-kit extends the capabilities of ccsdspy to
streamline CCSDS Space Packet management for flight missions." (quoted as rendered; the
reStructuredText link markup on both "SPaC-kit"s is omitted). ROSES is NASA's Research Opportunities
in Space and Earth Sciences solicitation, so the funder is NASA. Corroborating (but not itself a
funding statement): the two authors named in `pyproject.toml` are NASA Goddard staff
(`steven.d.christe@nasa.gov`; Daniel da Silva commits as `daniel.e.dasilva@nasa.gov`), and further
contributors commit from `@jpl.nasa.gov` and `@nasa.gov` addresses.
*Why NASA is recorded (a settled user decision, made on 2026-07-30 and re-confirmed on 2026-10-29):*
the ROSES High-Priority Open-Source Software award is announced in CCSDSPy's **own** release notes, as
coinciding with CCSDSPy 2.0.0 and as funding work that "extends the capabilities of ccsdspy"; the core
maintainers are NASA Goddard civil servants with further contributors at the Jet Propulsion
Laboratory; and there is no competing funder candidate anywhere in the repository or registries. The
counter-reading was weighed and outweighed both times: the changelog sentence's grammatical **subject
is SPaC-kit**, the companion package, not CCSDSPy itself, so a strict reading would attribute the
award only to SPaC-kit's own record, and this field's funding rule would then remove the funder
(rule 2). A later refresh should not re-propose removing NASA on this evidence; what would reopen it
is new funding evidence, such as a funding statement for CCSDSPy itself or `fundingReferences` on its
DOI record.

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
Not found

*Why empty:* no eligible publication describes, cites or uses CCSDSPy (rule 8). This field admits
only the *Eligible publication types* its rubric lists (a paper, preprint, report, thesis or chapter,
a poster deposited as the poster itself, or a slide deck that reads as a standalone document); neither
of the two entries HSSI held qualifies, and the search below found no other candidate.

*Superseded values.* HSSI held two entries until this update, both removed under rules 1 and 7:

- `https://adass2018.astro.umd.edu/abstracts/P7.2.html` — the ADASS 2018 (ADASS XXVIII, College Park,
  MD) conference website's abstract page for poster P7.2, "CCSDSPy - Convenient Decoding of Binary
  Spacecraft Telemetry", by Daniel da Silva, CCSDSPy's lead author. The page gives the title, the
  author affiliation "NASA/GSFC, Trident Vantage Systems, Johns Hokpins [sic] University", the poster's
  theme and a three-sentence abstract describing the library. A conference abstract is never
  eligible, even when the poster it announces would be (rule 1), and no deposited copy of the poster
  was found to link instead (below).
- `https://doi.org/10.5281/zenodo.8412310` — a Zenodo presentation deposit (version record
  `10.5281/zenodo.8412311`) from the 2023 Data, Analysis and Software in Heliophysics (DASH) conference
  (ADS `2023dash.confE...6H`), by seven authors led by J. Marcus Hughes, CCSDSPy author #4. Its only
  file is the PowerPoint deck `hughes_marcus_dash_punch.pptx` (41,807,224 bytes): eight slides with
  about 490 words of slide text and no speaker notes — a title slide, a PUNCH introduction, a package
  diagram, dependencies with a Prefect screenshot, a bullet list of challenges, a communication slide,
  a "Demo!" slide linking a DeepNote notebook, and a summary. It is not a substantial standalone
  document a reader could follow without the talk, so it fails the slide-deck test (rule 1; the
  user's judgment, 2026-10-29). No slide names CCSDSPy: the software appears only in the deposit's
  abstract ("Our packages heavily leverage SunPy, AstroPy, CCSDSPy, and ndcube…"). The PUNCH
  pipeline's use of CCSDSPy is recorded under Field 30 (punchbowl).

*Weighed and not recorded: the ADASS 2018 poster itself, for which no permanent record was found.* The
abstract page's "Link to PDF (may not be available yet)" points at `P7-2.pdf`, which returned 404 on
2026-10-29, and its "Poster preview" is a Google Slides share link: an editable document, not a
deposit and not a permanent landing page. The ADASS XXVIII proceedings (ASP Conference Series vol.
523) hold no paper by da Silva and none whose indexed text mentions CCSDS: ADS author and full-text
queries of the volume return nothing, while the volume itself and an author control (Taylor's TOPCAT
paper) are found. A Zenodo creator-keyed search for `da Silva, Daniel` finds no CCSDSPy, telemetry or
ADASS deposit; a Zenodo search for `"CCSDSPy"` returns only the software and the DASH 2023 deck; and
DataCite and Crossref hold no other record titled or described as CCSDSPy.

*Search record.* Searched on 2026-10-28 for publications since the 2026-07-30 extraction. ADS/SciX
`full:"ccsdspy"` returns only the DASH 2023 deck (`2023dash.confE...6H`) and nothing entered since
2026-07-30, and `ack:"ccsdspy"` returns nothing; a nonsense-token control returned 0, and a positive
control (`full:"spacepy"` over the same window) returned hits. DataCite `query=ccsdspy` returns only
CCSDSPy's two software DOIs and the deck's two DOIs; Zenodo's search returns only the 1.1.0 deposit
and the deck; OpenAlex returns nothing; and DataCite records no citations of the concept DOI. No
candidate was found. Semantic Scholar could not be queried (rate-limited), so the next search should
cover it from 2026-07-30; the other sources can start from 2026-10-28.

---

### 28. Related Datasets (OPTIONAL)
Not found

*Source:* CCSDSPy supports no specific published dataset — it is format-generic. The mission
telemetry in the repository (`ccsdspy/tests/data/europa_clipper/`, `.../csa/apid00400.tlm`,
`.../split/CYGNSS_F7_L0_2022_086_10_15_V01_F__first101pkts.tlm`, `.../hs/`) consists of unpublished
regression-test fixtures with no DOIs and no dataset landing pages; `ccsdspy/tests/data/hs/README.rst`
records that its files are synthetic ("It is fake data which he granted permission to use for the
project"). None of it is a dataset the software is built to read or one it produced, with a DOI or a
permanent landing page, which is what this field records (`fields/28-related-datasets.md`).

---

### 29. Related Software (OPTIONAL)
1. `https://github.com/lasp/space_packet_parser` — **space_packet_parser**

*Source and relevance (rule 9, similar-purpose tool):* space_packet_parser is an independent Python
library for the same task — "A CCSDS telemetry packet decoding library based on
the XTCE packet format description standard" (PyHC registry `_data/projects.yml`; identical GitHub
repository description). It is the direct alternative a user choosing a Python CCSDS decommutation
library must weigh against CCSDSPy, and the two differ in exactly the way that matters: CCSDSPy
defines packets in Python objects or simple CSV, space_packet_parser consumes XTCE XML. CCSDSPy's own
sources do not name space_packet_parser, so the ground is the two projects' own descriptions of the
same task, together with the relation already in the catalogue: as of 2026-10-28, space_packet_parser's
HSSI entry lists `https://github.com/ccsdspy/ccsdspy` among its Related Software.

*Identifier form (rules 11 and 13):* as of 2026-10-28 space_packet_parser has an HSSI entry (Space
Packet Parser), so the URL is that entry's stored `code_repository_url`,
`https://github.com/lasp/space_packet_parser`, byte for byte (rule 11). Its concept DOI,
`https://doi.org/10.5281/zenodo.7735001`, is passed over: a software relation to a target with a
public repository uses the repository URL, because the site shows the raw URL as link text (rule 13).
HSSI held that concept DOI as this field's value until this update. Should the DOI form ever be
preferred, `10.5281/zenodo.7735001` is the right one: it is the active concept, under which DataCite
lists the current releases and which space_packet_parser's own entry carried as its Persistent
Identifier on 2026-10-28. The older `10.5281/zenodo.7734999` is a stale concept record, last at 4.0.1
under the pre-transfer `medley56/space_packet_parser` owner.

*Considered and deliberately excluded (audit trail):*
- **SPaC-Kit** — a genuine companion package, but its relationship with CCSDSPy is a
  plugin/extension exchange, so it is recorded under Field 30 rather than duplicated here.
- **numpy, pyyaml, appdirs, pytest / pytest-astropy / pytest-cov, black, flake8, coverage, sphinx,
  sphinx-automodapi, graphviz, numpydoc** — Tier A generic scientific-Python and tooling stack.
  Listing them would be equally true of most of the ecosystem.
- **bitstruct** — a required dependency (`bitstruct>=8.17.0`), used by `ccsdspy/encode.py` to pack
  bits. Excluded because it is generic infrastructure under the Field 30 rule-2 test (would it be
  "equally at home in a web app, a finance model, or a biology pipeline?"): it is a general-purpose
  bit-field packing library with no heliophysics content, and its presence characterises nothing about
  this software beyond the fact that it manipulates bits.
- **astropy** — excluded with especially clear evidence: CHANGELOG.rst 0.0.8 records "Removed astropy
  dependency. Changes return type of ccsdspy.FixedLength.load from astropy.table.Table to
  OrderedDict." The dependency was deliberately dropped. `pytest-astropy` remains a *dev-only* test
  dependency, and `ccsdspy/logger.py` is "adapted from the AstropyLogger class" (link markup omitted;
  with `licenses/ASTROPY.rst` shipped) — attributed code reuse, which is an implementation detail
  rather than a related-software relationship.
- **sunpy** — `ccsdspy/config.py`: "This code is based on that provided by SunPy"; and
  `docs/dev-guide/index.rst` says its standards are based on those provided by sunpy. Attributed
  code/convention borrowing, not a dependency, not a fork, and not distinguishing. Excluded.
- **punchbowl / regularizePSF / solpolpy** (PUNCH packages) — the 2023 DASH presentation weighed under
  Field 27 says the PUNCH packages "heavily leverage … CCSDSPy". punchbowl does import and use CCSDSPy
  (the evidence is under Field 30), but it is a downstream consumer: not a similar-purpose tool, a
  predecessor, a companion by the same team, or a dependency of CCSDSPy, so none of rule 9's grounds
  applies and the relation is recorded in Field 30 alone (rule 3 here; Field 30 rule 9). regularizePSF
  (at `ff22e8d9319c28bdb8bee124e154d626a7045ab7`) and solpolpy (at
  `a118e6f72d2605291827abc485d5bbe5f9fad96c`) do not mention ccsdspy anywhere, so neither has a
  relation to cite in either field. The 2026-07-30 extraction recorded that punchbowl's dependency
  list had no `ccsdspy` entry. That held only for `[project] dependencies`: punchbowl's `pipe`
  dependency group already declared `ccsdspy`, and its Level 0 flow already imported it, at
  `10157d1e7a65` (its last commit before 2026-07-30).
- CCSDSPy has no predecessor and was not forked from anything: the repository was created
  2017-05-24 by Daniel da Silva as an original work.

---

### 30. Interoperable Software (OPTIONAL)
1. `https://github.com/CCSDSPy/SPaC-Kit` — **SPaC-Kit** (Space Packet as Code Kit)
2. `https://github.com/punch-mission/punchbowl` — **punchbowl** (the PUNCH mission's core pipeline
   package)

*SPaC-Kit: cited evidence of a demonstrated exchange* — it clears the Field 30 bar on three
independent counts:
- **A companion release announced by CCSDSPy itself.** CHANGELOG.rst, 2.0.0 entry: "Coinciding with
  this release is the release of SPaC-kit… SPaC-kit extends the capabilities of ccsdspy to
  streamline CCSDS Space Packet management for flight missions. It provides a GitHub repository
  template for defining and documenting mission packet formats… Mission-specific packet definitions
  are distributed as SPaC-kit plugins and can be used with SPaC-kit utilities to parse and generate
  test datasets." (quoted as rendered; reStructuredText link markup omitted)
- **A declared plugin/extension architecture built on CCSDSPy.** SPaC-Kit's README: "SpaC-Kit
  supports mission or instrument-specific CCSDS packet structures via plugin packages built on the
  CCSDSPy library" (quoted as rendered; the README's link and bold markup on "CCSDSPy library" is
  omitted), with the published plugin being
  `https://github.com/nasa-jpl/spac-kit-europa-clipper`.
- **A concrete, version-pinned API consumption.** SPaC-Kit's `pyproject.toml` declares
  `ccsdspy (>=2.0.0,<3.0.0)`; its `spac-parse`, `spac-ls`, and `spac-generate` console scripts consume
  CCSDSPy packet definitions and CCSDSPy-decoded output and export it to Pandas DataFrames, Excel, and
  CSV, and drive CCSDSPy's synthetic-packet generation. Both projects live in the same GitHub
  organisation (`CCSDSPy/ccsdspy`, `CCSDSPy/SPaC-Kit`).
*SPaC-Kit identifier form (rule 11, via Field 29 rule 12):* as of 2026-10-28 SPaC-Kit has no HSSI
entry, so its upstream repository root is recorded. It has no DOI either: on 2026-10-28 DataCite and
Zenodo searches for `SPaC-Kit` returned no record, and its PyPI project `spac_kit` lists only
`Homepage = https://github.com/CCSDSPy/SPaC-Kit`.

*punchbowl: a demonstrated exchange seen from the other side (rule 7).* At punchbowl revision
`d2d44328fcf861018758290242e3fa273464a0d9` (2026-10-27), `punchbowl/auto/flows/level0.py` imports
CCSDSPy (`import ccsdspy` at line 16; `from ccsdspy import PacketArray, PacketField, converters` and
`from ccsdspy.utils import split_by_apid` at lines 23–24), builds `ccsdspy.FixedLength` and
`ccsdspy.VariableLength` packet definitions in `create_packet_definitions()` (lines 231 and 276), and
decodes the PUNCH Level 0 telemetry stream with them, splitting it with `split_by_apid()` and calling
each definition's `load()` (lines 1507 and 1518). Its `pyproject.toml` declares
`"ccsdspy >= 1.4.0, <= 1.4.3"` in the `pipe` dependency group (line 84). A domain tool that imports
this software and consumes its output is a demonstrated exchange, so rule 7 includes it. The relation
is also inbound: as of 2026-10-28 punchbowl's own HSSI entry lists
`https://github.com/ccsdspy/ccsdspy` among its Related Software, and testing the reverse on this
evidence passes (rule 10). A user should know that the pin admits only the CCSDSPy 1.4 series, not
2.x.
*punchbowl identifier form (rule 11, via Field 29 rules 11 and 13):* as of 2026-10-28 punchbowl has an
HSSI entry, so the URL is that entry's stored `code_repository_url`,
`https://github.com/punch-mission/punchbowl`, byte for byte. Its concept DOI,
`https://doi.org/10.5281/zenodo.14029123`, is passed over because the site shows the raw URL as link
text.
*punchbowl is not also in Field 29 (rule 9):* as a downstream consumer it has no Field 29 ground of its
own, so listing it there would show the same link twice for one fact.

*Exclusions:* identical to the Field 29 audit trail above — numpy, bitstruct, pyyaml, appdirs, the
test/docs toolchain, astropy (dependency deliberately removed in 0.0.8), sunpy (attributed code
borrowing only), and regularizePSF and solpolpy (neither mentions ccsdspy). No entry rests on
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
   SPHEREx, ELFIN, PADRE, and (since commit `a5438ce`, 2026-10-20) STRIVE, and the Zenodo/GitHub
   description says "Library used in flight missions at NASA, NOAA, and SWRI". These are adopter
   name-drops — the section closes with an open invitation, "Do you know of other missions that use
   CCSDSPy?", followed by a link for reporting one through a GitHub issue. The library behaves
   identically for all of them and for any mission not on the list.
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
   plugin packages built on the CCSDSPy library" (link and bold markup omitted), the published
   example being `nasa-jpl/spac-kit-europa-clipper`. This field's rules exclude instruments belonging
   to a separate ecosystem/plugin package — they belong to *that package's* record, not to the
   umbrella framework's.
5. **Both sanity checks fail.** A user searching HSSI for a specific instrument wants that
   instrument's science software, not a generic packet library; and someone working with a given
   instrument's science data would not reach for CCSDSPy.

*Vocabulary due diligence:* resolvable SPASE rows exist for six of the eleven "Used By" missions — for
example instrument rows `Narrow Field Imager`
(`https://spase-metadata.org/NASA/Instrument/PUNCH/NFI`) and four `Solar Ultraviolet Imager` rows
(`.../NOAA/Instrument/GOES/{16,17,18,19}/SUVI`) — and none exist for Europa Clipper, the Canadian
Space Agency, PACE, SPHEREx, or STRIVE (on 2026-10-28 no row's name or identifier contained
`STRIVE`). They are omitted on relevance, not because they could not be resolved.

*On the Canadian Space Agency specifically:* it is one of the eleven entries in the "Used By" section,
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
(`https://spase-metadata.org/NASA/Observatory/PUNCH`),
`Heliophysics Environmental and Radiation Measurement Experiment Suite`
(`.../SMWG/Observatory/HERMES`), `Solar Polarization and Directivity X-Ray Experiment`
(`.../SMWG/Observatory/PADRE`), `Electron Losses and Fields Investigation A, CubeSat`
(`.../SMWG/Observatory/ELFIN/A`), and `Geostationary Operational Environmental Satellite 16`–`19`
(`.../{SMWG,NOAA}/Observatory/GOES/{16,17,18,19}`). No row exists for Europa Clipper, the Canadian
Space Agency, PACE, SPHEREx, or STRIVE — and in the CSA's case none can, because it is a **space
agency, not a mission or observatory** (see the note under Field 31), making it a ladder rule-5
omission independent of the relevance gate. **No name is recorded without a SPASE identifier, and
nothing is flagged as ambiguous** — every one of these is omitted on relevance, which this field's
guidance treats as a correct outcome.

---

### 33. Logo (OPTIONAL)
`https://docs.ccsdspy.org/en/latest/_static/logo.png`

*Source:* Two independent sources agree, and the URL serves the image at 816×811. The host's CDN may
serve it recompressed, as a smaller PNG or as WebP, so the bytes fetched need not equal the repository
blob. The curated PyHC registry lists exactly
`logo: https://docs.ccsdspy.org/en/latest/_static/logo.png` for CCSDSPy, and the asset exists in the
repository at `docs/_static/logo.png`, published to the project's canonical documentation host (see
Field 24) and referenced by `docs/_templates/logo.html`. This is a permanent, publicly accessible
location, as the field requires.
