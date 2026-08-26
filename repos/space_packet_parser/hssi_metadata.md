# HSSI Metadata Extraction Results

**HSSI Software ID:** 596d3936-d754-4c02-b8ae-20f69d4ac16b
**Repository:** https://github.com/lasp/space_packet_parser
**Source Revision:** e76f14151c15ab73d810c4b35970a6269d643d3c
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-07-28
**Validation Status:** PASS

**How to read this file.** The values here were reconciled against the entry's previously recorded
metadata and then gap-filled and corrected from the source repository at the revision above, the
Zenodo/DataCite records for the concept DOI, PyPI, the PyHC community registry, ORCID, and SoMEF.
No earlier canonical dossier existed for this software. Previously recorded values are preserved
unless an evidence-cited justification for superseding one is given in the field, and multi-valued
fields are set-unions of the earlier values and newly evidenced ones.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** To be filled by actual submitter
- **Submitter Email:** To be filled by actual submitter
- **Source:** Submitter information is intentionally deferred to the person who performs the update.

### 2. Persistent Identifier (RECOMMENDED)
- **Persistent Identifier:** https://doi.org/10.5281/zenodo.7735001
- **Source:** Preserved from the existing HSSI record and confirmed as the Zenodo *concept* DOI
  (`conceptdoi: 10.5281/zenodo.7735001`, `conceptrecid: 7735001`) by the Zenodo and DataCite APIs, and
  by the README DOI badge.

### 3. Code Repository (MANDATORY)
- **Code Repository:** https://github.com/lasp/space_packet_parser
- **Source:** Preserved from the existing HSSI record and confirmed by `CITATION.cff`
  (`repository-code`), `pyproject.toml` (`[project.urls] repository`), `meta.yaml` (`home`/`dev_url`),
  the Zenodo record's `code:codeRepository` custom field, and SoMEF.

### 4. Software Functionality (MANDATORY)
- **Values:**
  - Data Processing and Analysis
  - Data Processing and Analysis:Calibration
  - Data Processing and Analysis:File Format Conversion
  - Data Processing and Analysis:Packet Decommutation
  - Data Processing and Analysis:Processing
  - Mission-related
  - Mission-related:Ingest
  - Mission-related:Packet Decommutation
  - Mission-related:System Testing
- **Note:** The prior record held only `Data Processing and Analysis:Packet Decommutation`, which is
  preserved. The remaining eight values, including the two required parent categories, rest on the
  evidence below.
- **Source and code evidence (per value):**
  - *Data Processing and Analysis* — required parent of the four selected subcategories.
  - *Data Processing and Analysis:Packet Decommutation* — preserved from HSSI and the core purpose of the
    library: `XtcePacketDefinition.parse_bytes()` (`space_packet_parser/xtce/definitions.py`) decodes binary
    CCSDS telemetry into `SpacePacket` field values; `space_packet_parser/generators/{ccsds,fixed_length,udp}.py`
    yield individual packets from files, byte buffers, and sockets, including CCSDS segmented-packet
    reassembly and out-of-sequence warnings.
  - *Data Processing and Analysis:Calibration* — `space_packet_parser/xtce/calibrators.py` implements
    `PolynomialCalibrator`, `SplineCalibrator` (zero- and first-order interpolation), and `ContextCalibrator`
    with a `calibrate()` API that converts raw encoded telemetry counts to calibrated engineering values
    during decoding; documented in `docs/source/users.md` ("Numeric Calibration") and tested in
    `tests/unit/test_xtce/test_calibrators.py`.
  - *Data Processing and Analysis:File Format Conversion* — the library converts binary CCSDS packet files
    into structured outputs and converts between XTCE representations:
    `XtcePacketDefinition.write_xml()` / `to_xml_tree()` serialize a definition built from Python objects to
    XTCE XML, `from_xtce()` deserializes it, and `space_packet_parser/xarr.py::create_dataset()` converts
    binary packet files to `xarray.Dataset` objects keyed by APID.
  - *Data Processing and Analysis:Processing* — general pipeline processing of telemetry streams:
    chunked buffered reading (`generators/utils.py::_setup_binary_reader`), packet filtering
    (`create_dataset(packet_filter=...)`, `examples/packet_filtering.py`), enumerated/string/boolean
    derivation of parameter values, and robust skipping of malformed or unrecognized packets.
  - *Mission-related* — required parent of the three selected subcategories.
  - *Mission-related:Packet Decommutation* — decommutation of CCSDS telemetry against an XTCE
    command-and-telemetry database is itself a mission ground-data-system function, and this library
    implements that function directly rather than merely being used near it:
    `XtcePacketDefinition.parse_bytes()` (`space_packet_parser/xtce/definitions.py`) and the
    `space_packet_parser/generators/` package turn a raw downlinked CCSDS/UDP byte stream into named,
    calibrated telemetry points, which is the decommutation stage of a ground system. HSSI's live
    functionality vocabulary registers `Packet Decommutation` as a valid child of **both**
    `Data Processing and Analysis` and `Mission-related`, so selecting it under both parents is precisely the
    distinction the vocabulary exists to express: the same operation as a data-processing capability and as a
    ground-system role. Supporting evidence that the implementation handles real operational telemetry
    databases rather than only synthetic cases:
    `tests/integration/test_xtce_based_parsing/test_{ctim,jpss,suda}_parsing.py` decode real mission
    telemetry against real mission XTCE documents.
  - *Mission-related:Ingest* — the library performs the Level-0 ingest step of a telemetry pipeline, reading
    raw downlinked telemetry files, buffered readers, in-memory bytes, and live sockets and emitting
    structured records (`generators/utils.py::_read_packet_file`, `_setup_binary_reader` with
    `socket.socket` support, `spp parse` CLI command).
  - *Mission-related:System Testing* — user-facing capabilities aimed at verification of flight-software
    telemetry products: `create_ccsds_packet()` and `create_udp_packet()` synthesize binary packets
    ("extremely useful for generating test packets for debugging or mocking purposes"),
    `validate_xtce()` / `spp validate` perform XTCE schema and structural validation of flight-software
    command-and-telemetry-database exports (`space_packet_parser/xtce/validation.py`,
    `docs/source/users.md` "XTCE Document Validation"), and `spp describe-packets` / `spp describe-xtce`
    inspect packet files and definition structure without a full pipeline.
- **Note (considered and not selected):** *Data Processing and Analysis:Data Access and Retrieval* — the
  library accepts sockets and file paths but never queries or downloads from a data archive (the only network
  fetch is an XTCE XSD schema download in `validation.py`). *Data Processing and Analysis:Analysis*,
  *Time Series Analysis*, *Data Reduction* — no scientific analysis, temporal analysis, or averaging/binning
  functions exist; APID filtering is selection, not reduction. *Data Visualization* and subcategories — the
  CLI renders `rich` terminal tables/trees for inspection and `matplotlib` appears only in the optional
  `examples` extra (`examples/parsing_and_plotting_idex_waveforms_from_socket.py`), so plotting is not a
  library capability. *Servers and Environments:Software or Environment Container* — the only container is
  `.devcontainer/Dockerfile` for development. *Data Processing and Analysis:Data Assimilation* — the PyHC
  registry entry lists a `data_assimilation` keyword, but the code contains no assimilation capability, so
  that keyword was not mapped. *Coordinate Transforms* and *Models and Simulations* — no such capability.
- **Note (relationship to Fields 31 and 32 — deliberate, not an oversight):** This field records the
  software's *functional role*, while Fields 31 and 32 record *specific instrument and observatory
  associations*. A mission-agnostic, reusable ground-system component legitimately holds the
  `Mission-related` role — it performs ground-system telemetry decommutation, ingest, and verification
  functions — while supporting no named instrument or observatory, because which mission's telemetry it
  decodes is determined entirely by the user-supplied XTCE document. Accordingly, the `Mission-related`
  values here rest on code-level and vocabulary evidence, not on the README's "Missions using Space Packet
  Parser" list, which Fields 31 and 32 correctly reject as evidence of a designed-to-support relationship.
  A future reviewer should not "fix" this apparent asymmetry: the two fields are answering different
  questions.

### 5. Related Region (MANDATORY)
- **Values:**
  - Earth Atmosphere
  - Earth Magnetosphere
  - Interplanetary Space
  - Solar Environment
- **Note:** All three previously recorded regions are preserved; `Interplanetary Space` is added.
- **Source:** The library is region-agnostic by design, so region applies through the missions whose
  telemetry it decodes, which is the same basis as the stored values. README "Missions using Space Packet
  Parser": CLARREO Pathfinder, Libera, and CTIM-FD are Earth atmosphere/radiation-budget missions
  (Earth Atmosphere); MMS-FEEPS is a magnetospheric mission (Earth Magnetosphere). `Interplanetary Space`
  is added because IMAP — listed first in that README section — is an interplanetary/heliospheric mission,
  and the repository's own test suite ships IMAP IDEX XTCE definitions and real IDEX telemetry
  (`tests/test_data/idex/`) plus a Europa Clipper SUDA definition and data (`tests/test_data/suda/`), both of
  which are interplanetary-cruise instruments.
- **Note (considered and not selected):** *Planetary Magnetospheres* — the Europa Clipper SUDA test fixture is
  a dust analyzer rather than a magnetospheric investigation, which is too weak a basis for this region.

### 6. Authors (MANDATORY)
- **Author:** Gavin Medley
  - **Author Identifier:** https://orcid.org/0000-0002-3520-9715
  - **Affiliation:** Laboratory for Atmospheric and Space Physics
    - **Affiliation Identifier:** https://ror.org/01fcjzv38
  - **Affiliation:** University of Colorado Boulder
    - **Affiliation Identifier:** https://ror.org/02ttsq026
- **Author:** Michael Chambliss
  - **Author Identifier:** https://orcid.org/0009-0003-7493-0542
  - **Affiliation:** Laboratory for Atmospheric and Space Physics
    - **Affiliation Identifier:** https://ror.org/01fcjzv38
  - **Affiliation:** University of Colorado Boulder
    - **Affiliation Identifier:** https://ror.org/02ttsq026
- **Author:** Greg Lucas
  - **Author Identifier:** https://orcid.org/0000-0003-1331-1863
  - **Affiliation:** Laboratory for Atmospheric and Space Physics
    - **Affiliation Identifier:** https://ror.org/01fcjzv38
  - **Affiliation:** National Aeronautics and Space Administration
    - **Affiliation Identifier:** https://ror.org/027ka1x80
  - **Affiliation:** Sandia National Laboratories
    - **Affiliation Identifier:** https://ror.org/01apwpt12
  - **Affiliation:** United States Geological Survey
    - **Affiliation Identifier:** https://ror.org/035a68863
  - **Affiliation:** University of Colorado Boulder
    - **Affiliation Identifier:** https://ror.org/02ttsq026
- **Author-set note:** The author set is exactly the three people already on record (matched by ORCID) —
  nobody is added or removed. Affiliations are added for Gavin Medley and Michael Chambliss, who had none.
  All five affiliations on the shared Greg Lucas Person record are preserved unchanged. The listing order
  is the authoritative credit order from `CITATION.cff` and the Zenodo/DataCite creator list (Medley,
  Chambliss, Lucas). Author order is stored metadata, so adopting it superseded an earlier incidental
  alphabetical order (Chambliss, Lucas, Medley); that ordering change was reviewed and approved
  explicitly.
- **Source (author set):** `CITATION.cff` `authors` (three entries with ORCIDs and `@lasp.colorado.edu`
  emails), `pyproject.toml` `authors`, and the Zenodo/DataCite creator list all agree on exactly these three
  people and ORCIDs. Organization names are written out in full with no acronyms.
- **Source (Gavin Medley's affiliations — both directly attested):** His public ORCID employment record
  (`0000-0002-3520-9715`) names both organizations directly: organization "University of Colorado Boulder"
  (ROR `https://ror.org/02ttsq026`) with department "Laboratory for Atmospheric and Space Physics"
  (ROR `https://ror.org/01fcjzv38`), role Software Engineer, current.
- **Source (Michael Chambliss's affiliations — one attested, one inferred):** His public ORCID employment
  record (`0009-0003-7493-0542`) names **only** Laboratory for Atmospheric and Space Physics
  (ROR `https://ror.org/01fcjzv38`, "Scientific Programmer / Software Engineer", current). University of
  Colorado Boulder is added as a documented inference from the parent-organization relationship — LASP's ROR
  record (`https://ror.org/01fcjzv38`) lists University of Colorado Boulder (`https://ror.org/02ttsq026`) as
  its parent organization, `LICENSE.txt` records "Copyright (c) 2023 University of Colorado", and this
  pairing matches the existing stored Greg Lucas HSSI record. This is explicitly *not* a claim that his ORCID
  record lists University of Colorado Boulder.
- **Note:** Greg Lucas's Person record is shared with other HSSI entries; his five stored affiliations are
  preserved untouched and must not be pruned by this update. Repository contributors who are not credited as
  authors in `CITATION.cff` (e.g. bot and Copilot commits in the git history) are intentionally excluded.
- **Completed correction (2026-07-28):** Gavin Medley had two HSSI Person records — the ORCID-bearing one used
  here, and a second, identifier-less record used by SpiceyPy. They were consolidated into the ORCID-bearing
  record, so Medley is now a single person across HSSI. His identity in this entry is unchanged; only the
  duplicate was removed.

### 7. Software Name (MANDATORY)
- **Software Name:** Space Packet Parser
- **Source:** Preserved from the existing HSSI record and confirmed by the README H1 title
  ("# Space Packet Parser") and SoMEF's `full_title` result. The distribution/package name is
  `space_packet_parser` (`pyproject.toml`, PyPI `space-packet-parser`, conda `space_packet_parser`), and the
  human-readable title is retained as the software name; this is an editorial choice of the stored record
  that is left intact.

### 8. Description (MANDATORY)
- **Description:**

  The Space Packet Parser Python library is a generalized, configurable packet decoding library for CCSDS
  telemetry packets based on the XTCE standard for packet structure definitions. It supports complex and
  polymorphic packet structures, using the XTCE UML model to represent dynamic inheritance structures and
  conditionals based on previously parsed data fields. The core functionality of the library is the
  configuration of an XtcePacketDefinition object from a static XTCE XML document. The configured definition
  object can then iterate over binary data, parsing and yielding parsed Packet objects containing the decoded
  packet field values in a generator pattern. The binary data may originate from an in-memory binary object,
  a buffered file reader opened in binary mode, or a python socket object; in every case, a small buffer is
  used to read chunks of data to reduce memory footprint. The space_packet_parser library supports robust
  error handling, is capable of handling malformed packet structures, and can dynamically parse muxed APID
  packet streams. In addition to the low-level parsing API, the library provides built-in packet bytes
  generators for CCSDS, fixed-length, and UDP packet streams as well as support for user-written generators
  for other binary formats, on-the-fly polynomial and spline calibration of raw parameter values, enumerated
  and string parameter decoding, and optional creation of Xarray Datasets keyed by APID. It can also build
  XTCE packet definitions from Python objects and serialize them to XML, validate XTCE documents against the
  XTCE schema and for internal structural consistency, and provides a command line interface (spp) for
  describing XTCE documents, inspecting packet files, and validating definitions.

- **Note:** The earlier description is preserved verbatim as the opening text; two
  sentences are appended to cover capabilities added in the 6.x series that the stored text predates. No
  stored wording was reworded or removed. If the maintainers prefer the shorter author-written abstract
  exactly as stored, the appended text can be dropped without affecting any other field.
- **Source:** The preserved opening text is the author-written abstract in `CITATION.cff` (also the Zenodo and
  DataCite abstract). The appended sentences are supported by `space_packet_parser/generators/`
  (`ccsds_generator`, `fixed_length_generator`, `udp_generator`, plus the documented custom-generator pattern
  in `docs/source/users.md`), `space_packet_parser/xtce/calibrators.py`,
  `space_packet_parser/xarr.py::create_dataset()`, `XtcePacketDefinition.write_xml()` / `to_xml_tree()`,
  `space_packet_parser/xtce/validation.py::validate_xtce()`, and the `spp` entry point in
  `space_packet_parser/cli.py` (`describe-xtce`, `describe-packets`, `parse`, `validate`) — all introduced or
  expanded in the 6.0.0–6.1.2 changelog entries in `docs/source/changelog.md`.

### 9. Concise Description (OPTIONAL)
- **Concise Description:** A generalized, configurable Python library for decoding CCSDS telemetry packets, including complex and polymorphic structures, from files, buffers, or sockets using XTCE packet structure definitions.
- **Note:** 199 characters, within the 200-character limit.
- **Replacement justification:** The stored value is not a description at all — it is a mechanical truncation
  of the long description that ends mid-word ("It supports compl"), so it fails the field's purpose of
  providing a readable standalone preview and renders as a broken sentence in the HSSI UI. The replacement is
  a complete, self-contained sentence drawn from the same author-written abstract wording ("generalized,
  configurable", "complex and polymorphic", the file/buffer/socket input sources, "XTCE standard for packet
  structure definitions") plus the repository's own one-line summary in `pyproject.toml`/`CITATION.cff`
  ("A CCSDS telemetry packet decoding library based on the XTCE packet format description standard"). No new
  claims are introduced.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2022-09-22
- **Previous incorrect value:** 2025-09-04.
- **Replacement justification:** The field is defined as the date of first broadcast/publication and is
  "used for the initial version of the software." The stored 2025-09-04 is the release date of version
  6.0.0 — the version that was current when the entry was first submitted — not the software's first
  publication. This software was first published under a predecessor name, so first publication predates the
  current repository. `docs/source/changelog.md:201-207` ("Historical Changes (`lasp_packets`)") states that
  "Changes documented in v3.0 and earlier correspond to development efforts undertaken before this library was
  moved to GitHub (it was previously known as `lasp_packets`)" and that "None of the git history is available
  for these versions as the git history was truncated in preparation for the move to GitHub"; the changelog
  then documents versions 1.0, 1.1.0, 1.2, 1.3, 2.0, 2.1, and 3.0 as this project's own history. The PyPI
  project `lasp-packets` (summary "CCSDS packet decoding library") is public with exactly three releases —
  `2.1` uploaded 2022-09-22T23:04:04Z, `3.0rc1` 2023-02-12T05:00:02Z, and `3.0` 2023-02-17T21:53:15Z — making
  **2022-09-22 the earliest confirmed public publication** of this software.
- **Note (dates considered and not selected):** 2023-03-10 is the first release under the *current* name
  (first open-source commit `bc1da47c1af74c929a4b13133df1c223001f031b`, "First commit to open source project";
  oldest git tag `4.0.1`; oldest `space-packet-parser` PyPI upload 2023-03-10T16:54:49Z), and 2023-03-14 is
  the first Zenodo deposit (oldest version DOI `10.5281/zenodo.7735002`, v4.0.2). Both are recorded here for
  the record but not selected, because both postdate the confirmed first publication under the predecessor
  name.
- **Note (caveat):** Changelog versions 1.0 through 2.0 are all dated "Unknown" and have no public
  distribution trace, so they may predate 2022-09-22; that date is the earliest *confirmable* public release,
  not necessarily the absolute first.
- **Note (mapping pitfall for future refreshes):** The concept DOI's DataCite
  `dates[dateType=Issued]` is 2026-04-03, because a Zenodo concept DOI mirrors its *latest* version rather
  than its first. That field must not be used as the publication date for this entry.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** Preserved from the existing HSSI record and confirmed by DataCite (`publisher: "Zenodo"`) for the
  concept DOI, which is the correct publisher for a GitHub–Zenodo archived release.

### 12. Version (RECOMMENDED)
- **Version Number:** 6.1.2
- **Version Date:** 2026-04-02
- **Version Description:** Bug-fix release: prevents `BinaryParameter` truncation in `create_dataset`
  (issue #246).
- **Version PID:** https://doi.org/10.5281/zenodo.19392826
- **Previous incorrect values, all four subfields.** The earlier version record was not a bare number: it
  held `6.0.0`, release date 2025-09-04, version PID `https://doi.org/10.5281/zenodo.17055485`, and a
  `description` that was a **verbatim copy of the software description** rather than a version note. The
  version date, description and PID above therefore supersede those values, and that stale description was
  a second copy-paste corruption in this entry alongside the truncated Concise Description.
- **Replacement justification:** 6.1.2 is the latest authoritative release and five independent primary
  sources agree: the newest git tag is `6.1.2` (2026-04-02); `pyproject.toml`, `CITATION.cff`, and `meta.yaml`
  all declare `version = 6.1.2`; the newest PyPI release is 6.1.2 (uploaded 2026-04-02T22:26:54Z); the
  DataCite record for the concept DOI reports `version: 6.1.2`; and `docs/source/changelog.md` records
  "## [6.1.2] - 2026-04-02". The stored `6.0.0` is two minor and two patch releases behind
  (6.0.0 → 6.0.1 → 6.1.0 → 6.1.1 → 6.1.2). The version PID is the Zenodo version DOI for the 6.1.2 record
  (`10.5281/zenodo.19392826`), distinct from the concept DOI in Field 2. The version description is taken
  verbatim in substance from the 6.1.2 changelog entry.
- **Note:** The version number is recorded in its bare stored form (`6.1.2`). HSSI's view layer renders it as
  `Space Packet Parser - 6.1.2`; that rendered string must never be written back. Zenodo's record for 6.1.2
  carries `publication_date: 2026-04-03` (archive timestamp); the release date used here is 2026-04-02, which
  is what the git tag, the GitHub release, and PyPI all report.

### 13. Programming Language (RECOMMENDED)
- **Values:**
  - Other
  - Python 3.x
- **Source:** `Python 3.x` is confirmed by `requires-python = ">=3.10"`, the CI matrix
  (Python 3.10–3.14 in `.github/workflows/ci.yml`), and the `Programming Language :: Python :: 3` classifier.
  `Other` is retained and is independently supported by the non-Python sources GitHub attributes to the
  repository (SoMEF language statistics report Shell and Dockerfile in addition to Python) along with the XTCE
  XML documents and the JavaScript/HTML Pyodide in-browser demo under `docs/source/_static/`. `Javascript` was
  not added, because that code is a documentation demo asset rather than part of the library.

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication:** Not found
- **Source:** No reference publication exists. `CITATION.cff` has no `preferred-citation`, the README's only
  citation pointer is the Zenodo DOI badge, and the DataCite record for the concept DOI contains no
  `IsDescribedBy`/`IsSupplementedBy` publication relation (its only related identifiers are the GitHub tag URL
  and sibling version DOIs). There is no JOSS or journal paper for this library.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause
- **Source:** `LICENSE.txt` (BSD 3-clause text, "Copyright (c) 2023 University of Colorado"),
  `pyproject.toml` (`license = { text = "BSD-3-Clause" }`), `CITATION.cff` (`license: BSD-3-Clause`),
  `meta.yaml`, PyPI (`BSD-3-Clause`), and the DataCite record, which supplies both the exact name
  `BSD 3-Clause "New" or "Revised" License` and the URI `https://opensource.org/licenses/BSD-3-Clause`
  under the SPDX scheme.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Values (stored lowercase):**
  - binary
  - binary data
  - ccsds
  - data decoding
  - data encoding
  - data extraction
  - data manipulation
  - data processing
  - data transformation
  - decoding
  - decommutation
  - heliophysics
  - packet inspection
  - packet parsing
  - packets
  - parsing
  - python
  - science
  - space
  - space data systems
  - space packet protocol
  - telemetry
  - xml
  - xtce
- **Note:** All ten previously recorded keywords are preserved (compared by normalized lowercase
  identity, not display casing); fourteen are added: `binary data`, `data decoding`, `data encoding`,
  `data extraction`, `data manipulation`, `data processing`, `data transformation`, `heliophysics`,
  `packet inspection`, `packet parsing`, `space data systems`, `space packet protocol`, `telemetry`, `xml`.
- **Source:** The ten stored keywords match the GitHub repository topics exactly. Eleven of the additions are
  declared by the authors themselves in `pyproject.toml` `keywords` (lines 17–34): `space data systems`,
  `space packet protocol`, `packet parsing`, `packet inspection`, `data processing`, `data extraction`,
  `data manipulation`, `data transformation`, `data encoding`, `data decoding`, and `binary data`. The PyHC
  community registry entry independently lists `packet_inspection`. The remaining additions are `telemetry`
  (CCSDS telemetry decoding is the library's entire purpose) and `xml` (XTCE definitions are XML documents
  read and written by the library), plus `heliophysics` from PyHC membership and the README's "Proud Member of
  the Python in Heliophysics Community" section.
- **Note (deliberate exclusion):** `pyproject.toml` additionally lists `lasp` and `university of colorado`.
  These are intentionally not added: they are institutional identifiers rather than topical search terms, and
  both organizations are already represented as author affiliations in Field 6.
- **Note:** Keywords are stored lowercase and rendered Title Case by the HSSI view layer; the values above are
  the stored forms.

### 17. Data Sources (OPTIONAL)
- **Values:**
  - Other
- **Source:** The library ingests raw binary telemetry from local packet files, buffered binary file-like
  readers, in-memory `bytes`, and live network sockets (`generators/utils.py::_read_packet_file` and the
  `_setup_binary_reader` dispatch, which has a dedicated `socket.socket` implementation; `udp_generator` for
  UDP datagram streams). None of the enumerated archive or protocol sources apply, so `Other` is the correct
  selection.
- **Note (considered and not selected):** `HTTP/HTTPS Directories` — the only HTTP fetch in the codebase is the
  XTCE XSD schema download in `xtce/validation.py`, which retrieves a schema, not data. `CDAWeb`, `HAPI`,
  `das2`, `OMNIWeb`, `SSCWeb`, `TAP`, `The Virtual Solar Observatory`, `VirES`, `S3/Cloud-aware`,
  `Observatory/Mission-specific` — no client, credential handling, or archive-specific code exists for any of
  these.

### 18. Input File Formats (RECOMMENDED)
- **Values:**
  - Other
- **Source:** The two input formats are raw binary CCSDS/UDP packet files (no enumerated value applies) and
  XTCE XML packet definition documents (`XtcePacketDefinition.from_xtce()`, `spp.load_xtce()`), plus the XTCE
  XSD schema files used by `validate_xtce(local_xsd=...)`. Neither binary telemetry nor XML is in the allowed
  list, so `Other` is correct.
- **Note (considered and not selected):** `csv` — `examples/csv_to_xtce_conversion.py` reads a CCSDSPy-style
  CSV definition, but it does so with the Python standard-library `csv` module inside the example script; the
  library itself exposes no CSV reader, and only formats actually supported by the software should be listed.
  `CDF`, `netCDF3/4`, `HDF5`, `FITS`, `ISTP-Compliant`, `JSON`, `Zarr`, `IDL.sav`, `ascii` — no reader for any
  of these exists in the codebase.

### 19. Output File Formats (RECOMMENDED)
- **Values:**
  - Other
- **Source:** The library's only file output is XTCE XML: `XtcePacketDefinition.write_xml()` and
  `to_xml_tree()` serialize a definition (including definitions constructed from Python objects, as in
  `examples/csv_to_xtce_conversion.py`) to an XTCE XML document. XML is not in the allowed list, so `Other` is
  correct.
- **Note (considered and not selected):** `netCDF3/4` and `Zarr` — `examples/parsing_to_xarray_dataset.py`
  mentions (in commented-out lines) that a returned `xarray.Dataset` can be saved with `ds.to_netcdf()` or
  `ds.to_zarr()`, but that writing is performed by xarray, not by this library; `create_dataset()` returns
  in-memory Dataset objects and writes no files. CLI output is formatted terminal text, not a data file.

### 20. Operating System (RECOMMENDED)
- **Values:**
  - Linux
  - Mac
  - Windows
- **Source:** `.github/workflows/ci.yml` runs the full unit and integration test suite on
  `[windows-latest, ubuntu-latest, macos-latest]` across Python 3.10–3.14 on every push, pull request, and
  nightly schedule, which is direct verification on all three platforms. `pyproject.toml` also declares the
  `Operating System :: OS Independent` classifier and the conda recipe builds `noarch: python`.
- **Note:** The generic `OS Independent` / `Operating System Independent` values were not added on top of the
  three concrete, CI-verified platforms to avoid a redundant and partly duplicated selection; the pure-Python
  packaging evidence is recorded above should a curator prefer them.

### 21. CPU Architecture (RECOMMENDED)
- **Values:**
  - CPU Independent
  - x86-64
  - Apple Silicon arm64
- **Source:** The package is pure Python with no compiled extensions (`hatchling` wheel build with
  `packages = ["space_packet_parser"]`; conda recipe declares `noarch: python`), so `CPU Independent` is the
  primary value. `x86-64` and `Apple Silicon arm64` are recorded as concretely verified because the CI matrix
  exercises the test suite on GitHub's `ubuntu-latest` and `windows-latest` (x86-64) and `macos-latest`
  (Apple Silicon arm64) runners.

### 22. Related Phenomena (OPTIONAL)
- **Related Phenomena:** Not found
- **Source:** The controlled vocabulary for this field is solar-phenomenon specific (Coronal Heating, Coronal
  Holes, Coronal Mass Ejections, Solar Corona, Solar Flares, X-ray emission). Space Packet Parser is a
  telemetry transport/decoding library and supports no phenomenon-specific science functionality; no value in
  the list applies.

### 23. Development Status (RECOMMENDED)
- **Development Status:** Active
- **Source:** repostatus.org "Active" (stable, usable, and under active development) is supported by
  `pyproject.toml`'s `Development Status :: 5 - Production/Stable` classifier, five releases in the last
  eleven months (6.0.0 2025-09-04, 6.0.1 2025-11-06, 6.1.0 2026-01-21, 6.1.1 2026-03-31, 6.1.2 2026-04-02),
  commits continuing past the latest release (HEAD `e76f141` dated 2026-07-07), a nightly scheduled CI job,
  and the PyHC registry rating this package "Good" for software maturity, testing, documentation, and
  community.

### 24. Documentation (RECOMMENDED)
- **Documentation:** https://space-packet-parser.readthedocs.io
- **Source:** Preserved from the existing HSSI record and confirmed live (HTTP 200) and canonical by
  `CITATION.cff` (`url`), `pyproject.toml` (`[project.urls] documentation`), `meta.yaml` (`doc_url`), the
  GitHub repository homepage, the PyHC registry `docs` field, and SoMEF. The README's
  `.../en/latest/` variant resolves to the same site; the version-agnostic root URL is retained.

### 25. Funder (OPTIONAL)
- **Funder:** Not found
- **Source:** No funding statement, acknowledgement section, grant number, or funder appears anywhere in the
  repository (README, docs, `CITATION.cff`, `pyproject.toml`, `LICENSE.txt`), and the DataCite record for the
  concept DOI has an empty `fundingReferences` array. The missions listed in the README are NASA missions and
  the copyright holder is the University of Colorado, but neither establishes who funded this library, so no
  funder is asserted.

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found
- **Source:** No award title or grant number appears in the repository or in the DataCite/Zenodo metadata for
  the concept DOI.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Related Publications:** Not found
- **Source:** The repository cites no papers describing or using the library, and the DataCite record's
  `relatedIdentifiers` contain only the GitHub tag URL (`IsSupplementTo`) and sibling version DOIs
  (`HasVersion`) — no publication relations.

### 28. Related Datasets (OPTIONAL)
- **Related Datasets:** Not found
- **Source:** The binary telemetry files under `tests/test_data/` (CTIM, IMAP IDEX, JPSS-1, Europa Clipper
  SUDA) are small unpublished test fixtures committed to the repository, not citable datasets with DOIs or
  archive landing pages. No dataset identifiers appear in the repository or DOI metadata.

### 29. Related Software (OPTIONAL)
- **Related Software:** https://github.com/ccsdspy/ccsdspy
- **Source:** CCSDSPy is the other Python library for decoding CCSDS space packets, i.e. software that
  performs a similar task, and this repository engages with it concretely rather than generically:
  `examples/csv_to_xtce_conversion.py` is a documented, CI-executed converter from the CCSDSPy CSV packet
  definition format to XTCE (its module docstring cites the CCSDSPy 1.3.2 `loadfile` documentation), and
  `tests/test_data/jpss/ccsdspy_jpss1_geolocation.csv` is a CCSDSPy-format definition kept as a test fixture.
  The repository URL is given because it is the code location for the software; CCSDSPy's JOSS paper is a
  publication and therefore not recorded here.
- **Note on the URL's casing (settled).** The owner segment is lower-case `ccsdspy`, matching the
  form CCSDSPy's own HSSI record stores as its Code Repository and the form its canonical dossier
  uses. GitHub resolves either casing, but related-item identifiers are matched as exact strings, so
  the two spellings occupy two separate catalogue entries; aligning with the subject software's own
  record is what keeps them one. A later refresh that reads the owner name as displayed on GitHub
  should not "correct" this to `CCSDSPy`.
- **Note (considered and not selected):** `lxml`, `click`, `rich`, `hatchling` (declared dependencies),
  `numpy`, `matplotlib`, `pytest`/`pytest-benchmark`/`ruff`/`pre-commit` (test and tooling extras), and
  `pyodide` (documentation demo runtime) are all generic infrastructure — XML parsing, CLI plumbing, terminal
  formatting, arrays, plotting, packaging, testing, browser runtime — that would be equally at home in a web
  app or a finance model, so they carry no information about this software and belong in neither Field 29 nor
  Field 30.

### 30. Interoperable Software (OPTIONAL)
- **Interoperable Software:** https://github.com/pydata/xarray
- **Source:** Cited, specific data-model exchange rather than dependency presence: the public function
  `space_packet_parser.xarr.create_dataset()` is documented and typed to return `dict[int, xr.Dataset]`
  (`space_packet_parser/xarr.py`), so parsed telemetry is handed to xarray's data model as the library's
  documented interchange format for analysis workflows. It is exposed through the dedicated optional extra
  `space_packet_parser[xarray]` (`pyproject.toml`), documented in `docs/source/users.md` under "Parsing
  Packets to Xarray Datasets", demonstrated in `examples/parsing_to_xarray_dataset.py` and
  `examples/packet_filtering.py`, and covered by dedicated tests (`tests/unit/test_xarr.py`,
  `tests/integration/test_xarr.py`) plus a `[test,xarray]` CI job. Per-parameter numpy dtypes are derived
  from the XTCE encodings specifically so the resulting Datasets are usable downstream
  (`_get_minimum_numpy_datatype`).
- **Note (considered and not selected):** CCSDSPy — the CSV-to-XTCE example does consume CCSDSPy's definition
  format, but the conversion lives in an example script rather than the library's public API, so CCSDSPy is
  recorded under Field 29 (similar-purpose software) instead. Tier A infrastructure named in the Field 29 note
  is excluded here as well; `numpy` in particular is used internally by `xarr.py` and is not an
  interoperability claim.

### 31. Related Instruments (OPTIONAL)
- **Related Instruments:** None — intentionally empty
- **Source:** Space Packet Parser is an instrument-agnostic library. It implements the CCSDS Space Packet
  Protocol and the XTCE packet-structure standard generically: the parsing behavior is entirely determined by
  the user-supplied XTCE document, and the codebase contains no instrument-specific parser, calibration
  table, format, convention, or data source. There is therefore no evidence tying it to any specific
  instrument, and leaving this field empty is the correct answer rather than inventing associations.
- **Note (considered and not listed):** IDEX (IMAP), SUDA (Europa Clipper), and the JPSS-1/NOAA-20
  geolocation and CTIM telemetry sources appear only as XTCE documents and small binary fixtures under
  `tests/test_data/` and in one plotting example (`examples/parsing_and_plotting_idex_waveforms_from_socket.py`,
  explicitly described in its docstring as a demonstration/quicklook example) — these are test and
  demonstration name-drops, which the relevance gate excludes. MMS-FEEPS, Libera, CTIM-FD, CLARREO
  Pathfinder, and IMAP appear under the README heading "Missions using Space Packet Parser", which documents
  that mission teams use the library, not that the library is designed to support those instruments. No entry
  was dropped for being hard to resolve, so no SPASE ambiguity blocker arises for this field.

### 32. Related Observatories (OPTIONAL)
- **Related Observatories:** None — intentionally empty
- **Source:** As with Field 31, the library is mission/observatory-agnostic: it decodes any CCSDS packet
  stream described by any XTCE document, contains no mission-specific code path, data convention, archive
  client, or mission API, and is distributed as a general-purpose library. A user searching HSSI for a
  specific observatory should not expect a generic packet-decoding library in the results, so no observatory
  is listed.
- **Note (considered and not listed):** IMAP, CLARREO Pathfinder, Libera, CTIM-FD, and MMS (FEEPS) are named
  in the README's "Missions using Space Packet Parser" logo section, and JPSS-1/NOAA-20, CTIM, IMAP (IDEX),
  and Europa Clipper (SUDA) appear as `tests/test_data/` fixtures. Both categories are usage and
  test/demonstration references for an otherwise agnostic tool, which the relevance gate excludes. Because
  nothing passed the relevance gate, no SPASE resolution was required and no identifierless name is emitted;
  there is no unresolved-ambiguity blocker for this field.

### 33. Logo (OPTIONAL)
- **Logo:** https://raw.githubusercontent.com/lasp/space_packet_parser/main/docs/source/_static/logo-no-background.png
- **Source:** `docs/source/conf.py` sets `html_logo = "_static/logo-no-background.png"`, making this file the
  project's official documentation logo. The raw GitHub URL on the default branch was verified publicly
  accessible (HTTP 200, `image/png`, 50,558 bytes).
- **Note (tag-pinned alternative considered and declined):** A commit- or tag-pinned raw permalink
  (`.../space_packet_parser/6.1.2/docs/source/_static/logo-no-background.png`) was considered and rejected.
  A branch-pinned raw URL is the established HSSI convention: of the 38 HSSI entries that carry a logo, 28
  use a `/main/` or `/master/` raw GitHub URL (including sunpy, PlasmaPy, pysat, spacepy, pydarn, speasy, and
  ndcube) while only two pin a commit SHA. A `main` URL also keeps the logo current if the project redesigns
  it.
- **Note:** SoMEF reported a logo of
  `https://lasp.colorado.edu/ctim/files/2023/01/CTIM_LOGO_350x100_centered_transparent.png`; that is the CTIM
  mission patch from the README's "Missions using" section, not this software's logo, and was rejected.

---

## Changes to Stored Values (decided)

Every item below changes a value that HSSI currently stores. Nothing was silently overwritten; the supporting
evidence is recorded in the corresponding field above. All open questions from the first extraction pass have
been decided and are recorded here as resolved.

- **Field 12 Version — REPLACE `6.0.0` with `6.1.2`** (plus version date 2026-04-02, the 6.1.2 changelog
  description, and version DOI `https://doi.org/10.5281/zenodo.19392826`). Confirmed by git tags,
  `pyproject.toml`, `CITATION.cff`, `meta.yaml`, PyPI, DataCite, and the changelog. **Decided: replace, not
  append** — 123 of the 124 HSSI entries store exactly one version, so Field 12 represents the current
  release rather than release history.
- **Field 10 Publication Date — REPLACE 2025-09-04 with 2022-09-22.** The stored value was the 6.0.0 release
  date, not first publication. 2022-09-22 is the earliest confirmed public release, made under the
  predecessor name `lasp_packets` (`docs/source/changelog.md:201-207` establishes the lineage; PyPI
  `lasp-packets` 2.1 was uploaded 2022-09-22T23:04:04Z). 2023-03-10 (first release under the current name)
  and 2023-03-14 (first Zenodo deposit) were considered and not selected because they postdate it.
- **Field 9 Concise Description — REPLACE the mid-word truncation** ("...It supports compl") with a complete
  199-character standalone sentence.
- **Field 8 Description — APPEND two sentences** covering 6.x capabilities (built-in and custom packet bytes
  generators, calibration, Xarray Dataset creation, XTCE construction/serialization, XTCE validation, the
  `spp` CLI). The stored text is preserved verbatim and unedited. **Decided: the append is accepted.**
- **Field 6 Authors — ADD affiliations** for Gavin Medley and Michael Chambliss (Laboratory for Atmospheric
  and Space Physics, University of Colorado Boulder). **Decided: keep both organizations for both authors** —
  Medley's ORCID record attests both directly; Chambliss's attests LASP directly, with University of Colorado
  Boulder added as a documented parent-organization inference. No author is added or removed, and Greg
  Lucas's five existing affiliations on his shared Person record are preserved untouched.
- **Additive-only enrichments** (no stored value altered): Field 4 Software Functionality (+8, all stored
  values kept), Field 5 Related Region (+`Interplanetary Space`), Field 16 Keywords (10 → 24), and the
  previously-empty Fields 17, 18, 19, 20, 21, 23, 29, 30, and 33.
- **Decided, no change:** Field 20/21 breadth is kept as recorded (the three CI-verified operating systems;
  `CPU Independent` plus the two CI-verified architectures). Field 33 keeps the branch-pinned `/main/` raw
  logo URL, which is the established HSSI convention.
