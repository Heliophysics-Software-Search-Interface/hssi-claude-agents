# HSSI Metadata Extraction Results

**HSSI Software ID:** 596d3936-d754-4c02-b8ae-20f69d4ac16b
**Repository:** https://github.com/lasp/space_packet_parser
**Source Revision:** e76f14151c15ab73d810c4b35970a6269d643d3c
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-10-29
**Validation Status:** PASS

**How to read this file.** The values here were reconciled against the entry's previously recorded
metadata and then gap-filled and corrected from the source repository at the revision above, the
Zenodo/DataCite records for the concept DOI, PyPI, the PyHC community registry, ORCID, and SoMEF.
Passages brought forward to a later release name the revision they were read at. Previously recorded
values are preserved unless an evidence-cited justification for superseding one is given in the field,
and multi-valued fields are set-unions of the earlier values and newly evidenced ones.

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
  by the README DOI badge. Since commit `ae1338f` (read at `b14d4e23c70dd678170074c486eb5b9dea0b8cfc`),
  `CITATION.cff` also declares it under `identifiers` (`type: doi`, `value: 10.5281/zenodo.7735001`,
  "Concept DOI resolving to the latest release of space_packet_parser").
- **Note (a second concept DOI, considered and not selected):** `10.5281/zenodo.7734999` is also a
  software concept DOI for this code. Its only version, `10.5281/zenodo.7735000` (4.0.1, issued
  2023-03-10, creators Gavin Medley and Michael Chambliss), is `IsSupplementTo`
  `https://github.com/medley56/space_packet_parser/tree/4.0.1`, the repository's location before it moved
  to `lasp` (`https://github.com/medley56/space_packet_parser` now redirects to
  `https://github.com/lasp/space_packet_parser`). Every later deposit, from 4.0.2 (2023-03-14) on, is a
  version of `10.5281/zenodo.7735001`. With two concept DOIs passing Field 2 rule 5, rule 7 selects the one
  the project's own files cite: the README badge and `CITATION.cff` both cite `10.5281/zenodo.7735001`.

### 3. Code Repository (MANDATORY)
- **Code Repository:** https://github.com/lasp/space_packet_parser
- **Source:** Preserved from the existing HSSI record and confirmed by `CITATION.cff`
  (`repository-code`), `pyproject.toml` (`[project.urls] repository`), `meta.yaml` (`home`/`dev_url`),
  the Zenodo record's `code:codeRepository` custom field, and SoMEF.

### 4. Software Functionality (RECOMMENDED)
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

### 5. Related Region (RECOMMENDED)
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
  preserved untouched and must not be pruned. Repository contributors who are not credited as
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

- **Note:** The description HSSI held before the 2026-07-28 refresh is preserved verbatim as the opening
  text, and none of its wording was reworded or removed. Two sentences were appended to cover capabilities
  added in the 6.x series that the earlier text predates. The two appended sentences are separable from the
  author-written opening text, and the append was accepted.
- **Source:** The preserved opening text is the author-written abstract in `CITATION.cff` (also the Zenodo and
  DataCite abstract). The appended sentences are supported by `space_packet_parser/generators/`
  (`ccsds_generator`, `fixed_length_generator`, `udp_generator`, plus the documented custom-generator pattern
  in `docs/source/users.md`), `space_packet_parser/xtce/calibrators.py`,
  `space_packet_parser/xarr.py::create_dataset()`, `XtcePacketDefinition.write_xml()` / `to_xml_tree()`,
  `space_packet_parser/xtce/validation.py::validate_xtce()`, and the `spp` entry point in
  `space_packet_parser/cli.py` (`describe-xtce`, `describe-packets`, `parse`, `validate`) — all introduced or
  expanded in the 6.0.0–6.1.2 changelog entries in `docs/source/changelog.md` (now `CHANGELOG.md`).

### 9. Concise Description (OPTIONAL)
- **Concise Description:** A generalized, configurable Python library for decoding CCSDS telemetry packets, including complex and polymorphic structures, from files, buffers, or sockets using XTCE packet structure definitions.
- **Note:** 199 characters, within the 200-character limit.
- **Replacement justification:** The value HSSI held before the 2026-07-28 refresh was not a description at
  all — it was a mechanical truncation of the long description that ended mid-word ("It supports compl"), so
  it failed the field's purpose of providing a readable standalone preview and rendered as a broken sentence
  in the HSSI UI. The replacement is
  a complete, self-contained sentence drawn from the same author-written abstract wording ("generalized,
  configurable", "complex and polymorphic", the file/buffer/socket input sources, "XTCE standard for packet
  structure definitions") plus the repository's own one-line summary in `pyproject.toml`/`CITATION.cff`
  ("A CCSDS telemetry packet decoding library based on the XTCE packet format description standard"). No new
  claims are introduced.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2022-09-22
- **Previous incorrect value:** 2025-09-04.
- **Replacement justification:** The field is defined as the date of first broadcast/publication, and its
  form guidance reads "Used for the initial version of the software." The 2025-09-04 that HSSI held before
  the 2026-07-28 refresh is the release date of version 6.0.0 — the version that was current when the entry
  was first submitted — not the software's first publication. This software was first published under a
  predecessor name, so first publication predates the current repository. `docs/source/changelog.md:201-207`
  (now `CHANGELOG.md`; heading "Historical Changes (`lasp_packets`)") states that
  "Changes documented in v3.0 and earlier correspond to development efforts undertaken before this library was
  moved to GitHub (it was previously known as `lasp_packets`)" and that "None of the git history is available
  for these versions as the git history was truncated in preparation for the move to GitHub"; the changelog
  then documents versions 1.0, 1.1.0, 1.2, 1.3, 2.0, 2.1, and 3.0 as this project's own history. The PyPI
  project `lasp-packets` (summary "CCSDS packet decoding library") is public with exactly three releases —
  `2.1` uploaded 2022-09-22T23:04:04Z, `3.0rc1` 2023-02-12T05:00:02Z, and `3.0` 2023-02-17T21:53:15Z — making
  **2022-09-22 the earliest confirmed public publication** of this software.
- **Note (dates considered and not selected):** 2023-03-10 is the first release under the *current* name
  (first open-source commit `bc1da47c1af74c929a4b13133df1c223001f031b`, "First commit to open source project";
  oldest git tag `4.0.1`; oldest `space-packet-parser` PyPI upload 2023-03-10T16:54:49Z) and the date of
  the first Zenodo deposit, `10.5281/zenodo.7735000` (4.0.1), the only version under the separate concept
  DOI `10.5281/zenodo.7734999` (see Field 2). 2023-03-14 is the first deposit under the current concept DOI
  (`10.5281/zenodo.7735002`, 4.0.2). Both dates are recorded here for the record but not selected, because
  both postdate the confirmed first publication under the predecessor name. An earlier revision of this
  note called the 2023-03-14 deposit the first Zenodo deposit; it had missed the 4.0.1 deposit under the
  other concept DOI.
- **Note (caveat):** Changelog versions 1.0 through 2.0 are all dated "Unknown" and have no public
  distribution trace, so they may predate 2022-09-22; that date is the earliest *confirmable* public release,
  not necessarily the absolute first.
- **Note (mapping pitfall for future refreshes):** The concept DOI's DataCite
  `dates[dateType=Issued]` follows its *latest* version rather than its first: it read 2026-04-03 while
  6.1.2 was the newest deposit, and 2026-09-13 once 6.2.0 was deposited. That field must not be used as the
  publication date for this entry.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** Preserved from the existing HSSI record and confirmed by DataCite (`publisher: "Zenodo"`) for the
  concept DOI, which is the correct publisher for a GitHub–Zenodo archived release.

### 12. Version (RECOMMENDED)
- **Version Number:** 6.2.0
- **Version Date:** 2026-09-13
- **Version Description:** the indented block below, exactly, with its four-space indent removed
  from each line (its blank lines are part of it).

    ### Security

    - Fix a local file read vulnerability (CWE-73) and a Server-Side Request Forgery vulnerability (CWE-918) in `validate_xtce`. A document-supplied `xsi:schemaLocation` is now treated as untrusted: absolute and relative local filesystem paths are rejected (use `local_xsd` for a local schema), and schema URLs are fetched only over `https` from an allowlisted host (default `www.omg.org`), with requests to internal/link-local addresses (e.g. `169.254.169.254`, `127.0.0.1`) always blocked. Downloaded content is size-capped and is written to the cache only after it validates as an XSD, so a non-schema response can no longer be persisted to disk. [#266](https://github.com/lasp/space_packet_parser/issues/266)

    ### Added

    - Bundle the standard OMG XTCE 1.2 schema with the package so documents referencing it validate offline with no network request.
    - Add `allowed_schema_hosts`, `allow_insecure_http`, and `allow_schema_download` options to `validate_xtce` (and the corresponding `--allowed-schema-host`, `--allow-insecure-http`, and `--no-schema-download` flags to `spp validate`). The allowlist may also be set via the `SPP_ALLOWED_SCHEMA_HOSTS` environment variable, and insecure http via `SPP_ALLOW_INSECURE_HTTP`. The default allowlist is exported as `DEFAULT_ALLOWED_SCHEMA_HOSTS`.
    - Support multiple `<xtce:Unit>` elements within an `<xtce:UnitSet>`, so parameter types can declare compound units. Applies to every parameter type, both when reading an XTCE document and when serializing one back out. [#47](https://github.com/lasp/space_packet_parser/issues/47)

    ### Changed

    - Widen the `unit` attribute of parameter types from `str | None` to `str | tuple[str, ...] | None`. An `<xtce:UnitSet>` containing more than one `<xtce:Unit>` previously emitted a warning and joined the units into a single space-separated string; it now yields a tuple of the individual unit strings. Definitions declaring a single unit are unaffected. [#47](https://github.com/lasp/space_packet_parser/issues/47)

- **Version PID:** https://doi.org/10.5281/zenodo.22732164

HSSI held `6.1.2` (release date 2026-04-02, version PID `https://doi.org/10.5281/zenodo.19392826`) until
this update. **6.2.0** is the current release: a newer release than the 6.1.2 HSSI held, so it replaces that
row (rule 3) rather than being added beside it, because Field 12 describes one release, the newest the
project has released, and not the release history. The number is written bare, as the tag, PyPI and the
package metadata write it and as HSSI wrote 6.1.2. The release evidence was read on 2026-10-29, at `main`
head `b14d4e23c70dd678170074c486eb5b9dea0b8cfc`:

- **Tags.** `6.2.0` is the newest tag by creation date, on commit
  `8a43eb1cf1c94445060c08f2fdbebb90306594cd` ("Prepare 6.2.0 release", 2026-09-13T04:02:01Z), an ancestor
  of `main`; `6.1.2` is an ancestor of `6.2.0`. The tagged code declares `version = "6.2.0"` in
  `pyproject.toml` and `version: '6.2.0'` in `CITATION.cff`. No tag follows it, and the user-facing changes
  made on `main` since are listed under the CHANGELOG's `[Unreleased]` heading: they are not a release
  (rule 2).
- **GitHub release.** `6.2.0`, named `6.2.0`, published 2026-09-13T04:19:30Z from `main`, not a
  pre-release.
- **PyPI.** `info.version` is `6.2.0`; its wheel and sdist were uploaded at 2026-09-13T04:19:41Z and
  04:19:42Z, and neither is yanked. `project_urls` name this repository.
- **Version PID.** `10.5281/zenodo.22732164` is the 6.2.0 deposit: DataCite gives its `version` as `6.2.0`,
  `IsSupplementTo https://github.com/lasp/space_packet_parser/tree/6.2.0` and
  `IsVersionOf 10.5281/zenodo.7735001`, issued 2026-09-13, and it is the newest entry in the concept's
  `HasVersion` list (rule 17).
- **Version Date.** 2026-09-13 is the UTC day of the release's `published_at` (rule 7). The tag commit,
  the PyPI upload and the Zenodo deposit fall on the same UTC day, and `CITATION.cff` `date-released`
  (added after the release, in commit `ae1338f`) and the CHANGELOG heading `[6.2.0] - 2026-09-13` agree.
  The `release/6.2` merge commit `e6359c6` shows 2026-09-12 because its timestamp is in Mountain time
  (−0600); that local day does not override the release's UTC day (rule 8).
- **Version Description (rules 13–16).** The release's name is the bare tag, and its body is GitHub's
  auto-generated pull-request list ("What's Changed", "New Contributors", "Full Changelog"), which rule 16
  rules out, so the text comes from the `[6.2.0] - 2026-09-13` section of `CHANGELOG.md` at the tag (the
  section is identical at `b14d4e2`). Kept verbatim under the changelog's own headings, with each item's
  hard line wraps joined and its trailing issue link kept: the security fix to `validate_xtce` (#266); the
  three Added items, which bundle the XTCE 1.2 schema, add the schema-host options and flags, and support
  several `<xtce:Unit>` elements (#47); and the Changed item that widens `unit` (#47). Each is behaviour or
  API a user meets. Dropped whole under rule 14: the two documentation items under Changed (the split of
  the user documentation into Getting Started and a User Guide, and the benchmarking documentation
  refresh), four documentation corrections under Fixed (the `root_container_name` docstrings, the
  duplicated table of contents, the in-browser demo's sidebar, and the user-documentation inaccuracies),
  and the devcontainer `CLAUDE_CONFIG_DIR` fix. The last Fixed item, that `validate_xtce(local_xsd=...)`
  and `spp validate --local-xsd` "again accept absolute paths", is dropped too: the regression it repairs
  never reached a release, so no user could hit it. `space_packet_parser/xtce/validation.py` is identical
  at `6.1.2` and at `d21e9f6^`, the commit before the schema-validation hardening; 6.1.2 opens a
  `local_xsd` path directly, and the `DISALLOWED_SCHEMA_LOCATION` code the item's second sentence names
  first appears in 6.2.0. With every Fixed item dropped, the `### Fixed` heading goes too.
- **Previous values.** The 6.1.2 row's description, "Bug-fix release: prevents `BinaryParameter`
  truncation in `create_dataset` (issue #246).", restated that release's changelog entry ("Prevent
  BinaryParameter truncation in `create_dataset`.") in other words rather than quoting it; nothing from it
  is carried onto 6.2.0 (rule 10). Before 6.1.2 the record held `6.0.0` (release date 2025-09-04, version
  PID `https://doi.org/10.5281/zenodo.17055485`) with a description that was a verbatim copy of the
  software description rather than a version note; that row was replaced at the 2026-07-28 refresh.
- **Note:** The version number is recorded in its bare stored form (`6.2.0`). HSSI's view layer renders it
  as `Space Packet Parser - 6.2.0`; that rendered string must never be written back.

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

### 14. Reference Publication (OPTIONAL)
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
  - pyhc package
  - python
  - science
  - space
  - space data systems
  - space packet protocol
  - telemetry
  - xml
  - xtce
- **Note:** All ten previously recorded keywords are preserved (compared by normalized lowercase
  identity, not display casing); fourteen were added at the 2026-07-28 refresh: `binary data`,
  `data decoding`, `data encoding`, `data extraction`, `data manipulation`, `data processing`,
  `data transformation`, `heliophysics`, `packet inspection`, `packet parsing`, `space data systems`,
  `space packet protocol`, `telemetry`, `xml`. The 25th value, `pyhc package`, is explained in the note
  below.
- **Source:** The ten keywords HSSI held before the 2026-07-28 refresh match the GitHub repository topics
  exactly. Eleven of the additions are
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
- **Note (`pyhc package`, Field 16 rule 15):** Space Packet Parser is listed, as `space-packet-parser`, in
  the PyHC registry's `_data/projects.yml` (read at `heliophysicsPy/heliophysicsPy.github.io` commit
  `f7b0421b08c2cbc614a8d68372b42428d3a53cb2`, 2026-10-29), so the record carries `pyhc package`, which
  binds the existing keyword row of exactly that spelling. HSSI held it before this file did; an earlier
  revision of this list left it out.
- **Note (sources re-read 2026-10-29, at `b14d4e23c70dd678170074c486eb5b9dea0b8cfc`):** the
  `pyproject.toml` `keywords`, the ten repository topics and the registry entry's `keywords` are unchanged
  since the 2026-07-28 extraction (the registry entry gained only an `hssi:` link); `CITATION.cff`
  declares no keywords, and the 6.2.0 deposit carries no subjects.

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
- **Note:** The generic `OS Independent` / `Operating System Independent` values were not selected: on top
  of the three concrete, CI-verified platforms they would make a redundant and partly duplicated selection.
  The pure-Python packaging evidence is recorded above.

### 21. CPU Architecture (RECOMMENDED)
- **Values:**
  - CPU Independent
  - x86-64
  - Apple Silicon arm64
- **Source:** The package is pure Python with no compiled extensions (`hatchling` wheel build with
  `packages = ["space_packet_parser"]`; conda recipe declares `noarch: python`), so `CPU Independent` is the
  primary value. `x86-64` and `Apple Silicon arm64` are recorded as concretely verified because the CI matrix
  exercises the test suite on GitHub's `ubuntu-latest` and `windows-latest` (x86-64) and `macos-latest`
  (Apple Silicon arm64) runners. This breadth is settled: `CPU Independent` with the two architectures the
  CI runners verify, alongside the three CI-verified operating systems Field 20 records.

### 22. Related Phenomena (OPTIONAL)
- **Related Phenomena:** Not found
- **Source:** The controlled vocabulary for this field is solar-phenomenon specific (Coronal Heating, Coronal
  Holes, Coronal Mass Ejections, Solar Corona, Solar Flares, X-ray emission). Space Packet Parser is a
  telemetry transport/decoding library and supports no phenomenon-specific science functionality; no value in
  the list applies.

### 23. Development Status (RECOMMENDED)
- **Development Status:** Active
- **Source:** Field 23 rule 6 (recency, for software that has reached a stable, usable state). Read on
  2026-10-29: the last commit on the default branch `main` is `b14d4e23c70dd678170074c486eb5b9dea0b8cfc`,
  dated 2026-10-28, and the last release is 6.2.0 (2026-09-13), so the last commit is under six months old.
  Rules 1–4 do not fire: the repository is not archived, nothing points to a new location, and the README
  carries no repostatus.org badge (its badges are Conda, PyPI, DOI, CI, codecov and two Read the Docs build
  badges) and no status statement. The release series (6.0.0 on 2025-09-04 through 6.2.0 on 2026-09-13)
  shows a stable, usable state, and a nightly scheduled CI job runs the test suite on `main`
  (`.github/workflows/ci.yml`); `pyproject.toml`'s `Development Status :: 5 - Production/Stable` classifier
  corroborates that stable releases exist but is not itself a repostatus term. At the 2026-07-28 extraction
  the anchors were commit `e76f141` (2026-07-07) and release 6.1.2 (2026-04-02), which gave the same value.

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
- **Source:** No eligible publication describes, cites or uses Space Packet Parser (rule 8). The repository
  cites no paper about the library or its method: at `b14d4e23c70dd678170074c486eb5b9dea0b8cfc`,
  `CITATION.cff` has no `references` or `preferred-citation`, no documentation page carries a reference
  list or a citing-works page, and the README's only references are the format standards weighed below.
  The DataCite records of the concept DOI and of all 25 of its version DOIs carry no publication relation:
  their only related identifiers are the GitHub tag URL (`IsSupplementTo`) and the version links
  (`HasVersion`/`IsVersionOf`).
- **Weighed and not recorded:**
  - The README's "Resources" list links three CCSDS documents on XTCE: the XTCE Green Book (Informational
    Report, `https://public.ccsds.org/Pubs/660x2g2.pdf`), the XTCE Element Description Green Book
    (`https://public.ccsds.org/Pubs/660x1g2.pdf`) and the XTCE Blue Book (Recommended Standard,
    `https://public.ccsds.org/Pubs/660x0b2.pdf`). They are standards-body specifications of a file format,
    the XTCE packet-definition format the library reads and writes (the project describes itself as "based
    on the XTCE packet format description standard"), which the project lists as resources. They are not
    publications that describe, cite or use the software, so they do not belong in this field.
  - "Forging a Path to Multi-Institution, Open-Source Mission Software for Science" (Jon Vandegriff and
    Greg Lucas, NASA SMD Software Workshop 2024; Zenodo presentation
    `https://doi.org/10.5281/zenodo.11114328`), found through a creator-keyed search on Greg Lucas's ORCID:
    a slide deck on shared, open-source mission data-system software whose text names CCSDSPy but never
    Space Packet Parser, so it is not about this software.
  - "Transitioning to the Cloud: Insights from the Emirate Mars Mission Science Data System" (Bryan Harter,
    Greg Lucas, Gavin Medley et al., DASH 2023; ADS `2023dash.confE..47H` and `2023dash.confE..58H`, Zenodo
    presentations `https://doi.org/10.5281/zenodo.8412932` and `https://doi.org/10.5281/zenodo.8419823`):
    two versions of a slide deck on the Emirates Mars Mission's cloud science data system. Neither deck's
    slide or note text mentions packets, a parser, XTCE or CCSDS, so it is not about this software.
  - "AWS Native Science Data Processing Center for the Libera Mission" (Matt Watwood, Gavin Medley et al.,
    AGU Fall Meeting 2024, ADS `2024AGUFMIN51F2424W`): a meeting abstract, which rule 1 excludes, and its
    text does not name the software.
  - Two IMAP mission papers co-authored by Greg Lucas, "Science and Mission Operations of the Interstellar
    Mapping and Acceleration Probe (IMAP)" (ADS `2026SSRv..222...37R`) and "Space Weather Science to Enhance
    Forecasting with the NASA IMAP Active Link for Real-Time (I-ALiRT) System" (ADS `2025SSRv..221..117L`):
    ADS holds the full text of both (a `body:"packet"` probe finds each), and neither names the software, a
    parser, Python or XTCE.
  - "The Emirates Mars Ultraviolet Spectrometer (EMUS) for the EMM Mission" (ADS `2021SSRv..217...79H`,
    `https://doi.org/10.1007/s11214-021-00854-3`) is the only ADS hit for the predecessor name
    `lasp_packets`, and it is a tokenization artifact: the matched text is "(LASP). After packets are
    extracted from the L0 files", not the package.
  - OpenAlex's three full-text hits for "space packet parser" are a software deposit
    (`rudywasfound/aethelix`, `https://doi.org/10.5281/zenodo.19536795`; rule 1) and two unrelated papers,
    on messaging-application encryption and on attack-tactic identification.
- **Search record.** Searched on 2026-10-29 with no lower date bound; no earlier search had been recorded.
  ADS/SciX `full:` queries for "space packet parser", `space_packet_parser`, `space-packet-parser`,
  `SpacePacketParser`, `lasp/space_packet_parser` and `zenodo.7735001`, and `ack:` queries for "space packet
  parser" and `space_packet_parser`, return nothing, and `full:"lasp_packets"` returns only the EMUS
  artifact above; a nonsense-token control returned 0, and `full:"sunpy"` and `full:"pyspedas"` returned
  hits. ADS author searches for Gavin Medley, Michael Chambliss and Greg Lucas (Lucas's restricted to XTCE,
  CCSDS or packet terms) find no paper about the software. Zenodo creator-keyed searches on the three
  authors' ORCIDs find the software's own deposits, unrelated software and the 2024 deck above; a Zenodo
  search for "space packet parser" finds only the software's own record. DataCite records no citations of
  the concept DOI or of any version DOI, and OpenAlex records none for the concept work; OpenAlex full-text
  search, checked with `sunpy` (hits) and a nonsense token (0), finds only the three hits above, and
  Crossref's bibliographic search returns only general XTCE and packet-parsing literature. Semantic Scholar
  could not be queried (rate-limited on every attempt), so the next search should cover it for all years;
  the other sources can start from 2026-10-29.

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
- **Logo:** https://raw.githubusercontent.com/lasp/space_packet_parser/d21e9f6ed6390e3f4d42a09df72ad72a1e6423bf/docs/source/_static/logo-no-background.png
- **Source:** `docs/source/conf.py` sets `html_logo = "_static/logo-no-background.png"`, making this file the
  project's official documentation logo. The commit-pinned raw URL above was verified publicly accessible
  (HTTP 200, `image/png`, 50,558 bytes), serving the same image the default-branch URL served.
- **Note (an earlier revision declined pinning; that reasoning is superseded):** this record previously
  held the branch form `.../space_packet_parser/main/docs/source/_static/logo-no-background.png`, on the
  argument that a `main` URL "keeps the logo current if the project redesigns it." That has it the wrong
  way round: a branch URL breaks silently if the file is renamed, moved or deleted, and a redesign is
  something a metadata refresh should notice and record deliberately rather than inherit unannounced. The
  commit-pinned form cannot drift. A *tag*-pinned permalink
  (`.../space_packet_parser/6.1.2/docs/source/_static/logo-no-background.png`) is still the wrong shape,
  but for a different reason — it would need updating at every release, where a commit SHA needs none.
- **Note:** SoMEF reported a logo of
  `https://lasp.colorado.edu/ctim/files/2023/01/CTIM_LOGO_350x100_centered_transparent.png`; that is the CTIM
  mission patch from the README's "Missions using" section, not this software's logo, and was rejected.
