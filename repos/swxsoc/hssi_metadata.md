# HSSI Metadata Extraction Results

**HSSI Software ID:** 1fd6fa60-cd5d-4e38-bfea-ea8dc5b25eaa
**Repository:** https://github.com/swxsoc/swxsoc
**Source Revision:** 2bf3f8b31c57f22abf1c17b9e98a61f55a8f38f9
**Extraction Date:** 2026-09-12
**Validation Date:** 2026-09-12
**Validation Status:** PASS

---

**Scope note — read the evidence this way.** `swxsoc` is not a science-analysis package. It is the
shared core library of NASA's Space Weather Science Operations Center: a mission-support framework
that defines a data container, reads and writes ISTP-compliant CDF files, fetches mission data from
cloud archives, tracks science-file provenance in a database, and pushes housekeeping values and
annotations to operations dashboards. Several fields below are therefore *correctly* empty in ways
that would look like gaps for an analysis package (Related Phenomena, Related Instruments), and
several are populated by *inheritance* from the missions whose configurations the package ships
(Related Region, Related Observatories, Keywords). Each such case is argued explicitly rather than
left blank.

A second caveat that changes how the code should be read: the package absorbed two formerly separate
packages during 2026 — `sdc_aws_utils` and a MetaTracker package — so its functional surface is
substantially wider at this source revision than its published description suggests. Evidence drawn
from before those merges understates what the software does.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This is the standard placeholder for a catalogue record that was not submitted through the public
form by its maintainers. It is not a defect and should not be "corrected" to an extractor's identity.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** `https://doi.org/10.5281/zenodo.15546486`

This is the Zenodo **concept** DOI for `swxsoc/swxsoc` — the version-independent identifier that
always points at the deposit series rather than a single release. That is the right choice for this
field, because it keeps resolving as the project releases new versions, whereas a version DOI would
pin the catalogue to one snapshot. The per-version DOI belongs in Field 12, where it is recorded.

A trap worth writing down for whoever refreshes this next: a Zenodo concept DOI resolves to the most
recently **created** deposit, not necessarily the highest version number. When this dossier was
compiled (2026-09-12) the concept DOI led to Zenodo record `18226255`, whose `metadata.version` was
`0.2.3` and whose `conceptdoi` was `10.5281/zenodo.15546486`; at that moment the two agreed, because
the newest deposit was also the highest version, so no contest arose. That agreement was a fact about
one moment rather than a property of the identifier, and it stops holding as soon as a deposit is
created out of version order. Do not infer from it that the concept DOI can be treated as a version
DOI in general; confirm the resolved deposit's own `version` field before relying on it.

### 3. Code Repository (MANDATORY)
**Value:** `https://github.com/swxsoc/swxsoc`

Confirmed as the live upstream: the GitHub API reports `default_branch` `main` and the repository is
not archived (measured 2026-09-12). `pyproject.toml` declares the same URL under
`[project.urls] Homepage`, and the PyHC community registry lists the same value in its `code` field.

### 4. Software Functionality (RECOMMENDED — treated as critical)

**Ordering rule — do not "tidy" this list.** `softwareFunctionality` is a sortedm2m field: the order
of these bullets *is* stored data. Entries 1–9 are the order HSSI held before this refresh, which is
deliberately not alphabetical and not grouped by parent. Never alphabetise, never regroup by parent,
and never reorder to make the list look neater — any of those rewrites every stored position. Entries
10–16 were appended after that original nine rather than interleaved, so every pre-existing position
was preserved. Appending was safe *here specifically* because every appended entry is a child whose
parent category already sat among the first nine, so no child is stranded from its parent; an
addition whose parent was absent would have to bring that parent with it.

Every value is written `Parent: Child`. This is mandatory rather than stylistic: thirteen
subcategory names in this vocabulary sit on more than one row (`2D Slices`, `Analysis`,
`Calibration`, `Distribution/Access`, `Field-line Tracing`, `Infrastructure as Code`,
`Instrument Response`, `ML/AI`, `Mission-Specific`, `Observatory/Instrument Models`,
`Packet Decommutation`, `Processing`, `Spectrogram`), so a bare child name can bind to the wrong
parent's row. A stored child without its parent top-level category is a defect.

Note for anyone seeking authoritative wording: every row in this vocabulary carries an empty
`definition`, so category meanings must be taken from the `software-functionality` skill, not from
the database.

**Entries 1–9 — the order HSSI held before this refresh:**

1. `Data Visualization`
2. `Mission-related`
3. `Data Processing and Analysis`
4. `Data Processing and Analysis: Data Access and Retrieval`
5. `Data Visualization: Line Plots`
6. `Data Processing and Analysis: Processing`
7. `Mission-related: Processing`
8. `Data Processing and Analysis: Analysis`
9. `Mission-related: Analysis`

**Entries 10–16 — appended after that nine:**

10. `Data Processing and Analysis: Time Series Analysis`
11. `Mission-related: Distribution/Access`
12. `Mission-related: Ingest`
13. `Mission-related: Inventory`
14. `Mission-related: Monitoring`
15. `Mission-related: Operations`
16. `Mission-related: Science Data Processing`

**Evidence for entries 1–9.** `swxsoc/swxdata.py` defines the `SWXData` container and a
`plot()` method built on matplotlib axes, supporting `Data Visualization` and
`Data Visualization: Line Plots`. `swxsoc/net/client.py` provides `SWXSOCClient`, whose module
docstring reads "SWXSOC FIDO Client for searching and fetching data from AWS S3." — squarely
`Data Processing and Analysis: Data Access and Retrieval`. The mission data-level pipeline and
`swxsoc/util/reprocessing.py` support both `Processing` entries, and the package's derived-quantity
and schema-driven handling supports both `Analysis` entries.

**Evidence for entries 10–16.**

- `Data Processing and Analysis: Time Series Analysis` — the package's primary data model *is* a
  time series. `SWXData.__init__` takes
  `timeseries: Union[astropy.timeseries.TimeSeries, dict[str, astropy.timeseries.TimeSeries]]`, the
  shipped configuration sets `default_timeseries_key: Epoch`, and `swxsoc/db/timeseries.py` exports
  `record_timeseries`. It was absent from the record before this refresh even though it is arguably
  the package's most central capability.
- `Mission-related: Inventory` — `swxsoc/db/tracker.py` implements MetaTracker over a schema of
  file-level, file-type, instrument, instrument-configuration, science-file, science-product and
  status tables. The user guide describes it as recording "processing status in a relational
  database", and says MetaTracker "tracks the lifecycle of science files as they move through a
  pipeline: it parses a file's metadata from its filename, records it in a science-file table,
  associates it with a science-product record, and optionally logs a processing-status entry …".
  This is a science-file inventory in the ordinary sense of the word.
- `Mission-related: Ingest` — `swxsoc/io/s3.py` is documented as moving science files "between the
  incoming and instrument-specific S3 buckets." and exposes `upload_file_to_s3`,
  `download_file_from_s3` and `copy_file_in_s3`; MetaTracker then parses each arriving file's
  metadata from its filename and records it. That arrival-and-registration path is ingest.
- `Mission-related: Distribution/Access` — the same S3 module plus `SWXSOCClient`, which
  "provides search and fetch functionality for SWXSOC data and is based on the sunpy BaseClient for
  FIDO." The package is how external users obtain SWxSOC mission data.
- `Mission-related: Monitoring` — `swxsoc/db/timeseries.py` is documented as "AWS Timestream
  recording functions for SWXSOC data." for dashboard viewing; `swxsoc/util/grafana.py` manages
  Grafana dashboards and annotations; `swxsoc/comm/` provides Slack and Mattermost clients with an
  `ALERT_TYPES` vocabulary. Together these are operations monitoring and alerting.
- `Mission-related: Operations` — the comms/alerting clients, the processing-status table, and
  `invoke_reprocessing_lambda` are SOC operations tooling rather than science analysis.
- `Mission-related: Science Data Processing` — the shipped mission configurations define graded data
  levels (raw/l0/l1/ql/l2/l3) and the package drives promotion through them, with ISTP schema
  enforcement in `swxsoc/util/schema.py` and checks in `swxsoc/util/validation.py`.

**Considered and rejected — do not re-propose these without new code.**

- `Mission-related: Packet Decommutation` and `Data Processing and Analysis: Packet Decommutation` —
  rejected on measured absence. A case-insensitive search for `ccsds|decommut|packet` over the
  `swxsoc` and `docs` trees at this revision returns no hits, under a positive control (`instrument`)
  that returns hits in the same command shape. The mission configuration catalogues `.bin`, `.dat`
  and `.idx` file types, but that is filename bookkeeping for MetaTracker, not telemetry parsing.
  Decommutation happens in the per-instrument downstream packages, not here.
- `Mission-related: Calibration` and `Data Processing and Analysis: Calibration` — rejected, and the
  rejection rests on what the word "calibrat" marks where it appears rather than on its absence,
  because it appears in production code as well as in documentation. `docs/cmad/index.rst` is a
  Calibration and Measurement Algorithm Document stub which states that the individual missions host
  their own CMADs — the project's own statement that the algorithms live downstream.
  `swxsoc/io/s3.py` takes a `calibrated_filename` argument in `push_science_file`: the local path of
  a file some other component has already calibrated, which this function only keys and uploads;
  nothing in it inspects or transforms the data. `swxsoc/io/tests/test_io.py` builds a CDF fixture
  carrying a support-data variable named `Calibration_Factor` with `CATDESC` "Calibration factor",
  and `docs/examples/tutorial1.rst` and `docs/user-guide/reading_writing_data.rst` name an example
  variable `calibration_const` and `Calibration_const` respectively — payload names in example and
  test metadata, not code that derives them. `docs/dev-guide/downstream_testing.rst` cites "a
  calibration helper" as an example of the kind of shared utility a downstream package might depend
  on, and `docs/user-guide/cdf_format_guide.rst` mentions "change in calibration" when explaining
  what a data-version bump signifies. The bundled sample CDF matches too, again as a variable name
  inside a HERMES test file. Every occurrence is therefore a name, a filename argument, or a
  reference to calibration performed elsewhere; none is a calibration algorithm, response function,
  gain correction or flat-field. The package supplies no calibration capability, and someone
  filtering HSSI for calibration software would not want this package back.
- `Mission-related: Archive` — rejected. `swxsoc/net/client.py` and `swxsoc/net/attr.py` do describe
  the S3 buckets they query as "SWXSOC data archives", and `swxsoc/io/s3.py` stages files from an
  incoming bucket into instrument-specific ones, so the word is genuinely in play. But the package
  implements no archive: there is no retention or preservation policy, no accession or deaccession
  workflow, and no catalogue of holdings. It is a client of buckets that AWS hosts and the SDC
  operates. The two capabilities that are really present here are already recorded as
  `Mission-related: Ingest` and `Mission-related: Distribution/Access`, and adding `Archive` on top
  would put swxsoc in front of someone searching for archive software, which it is not.
- `Mission-related: Instrumentation` — rejected. `compute_instrument_metadata` and
  `compute_instrument_configurations` in `swxsoc/util/config.py` populate MetaTracker's `instrument`
  and `instrument_configuration` tables from the active mission configuration, emitting
  `instrument_id`, `full_name`, `short_name` and `description` rows plus every combination of
  instrument slots. That is bookkeeping *about* instruments — database keys and labels — not
  instrument software: nothing here commands, configures, calibrates or models an instrument.
  `Mission-related: Instrument Response` and `Models and Simulations: Observatory/Instrument Models`
  are rejected on the same reasoning and should not be re-derived separately.
- `Mission-related: Orchestration` — rejected, though it is the least clear-cut of the four.
  `swxsoc/util/reprocessing.py` exposes `invoke_reprocessing_lambda`, which builds an SNS-wrapped S3
  event and asynchronously invokes the SDC processing Lambda. That fires one job. There is no
  workflow definition, dependency graph, scheduler, state machine or retry topology anywhere in the
  package; the pipeline's control flow lives in the SDC AWS Lambda deployment (the `sdc_aws_*`
  packages noted in Field 29), to which swxsoc contributes a single trigger function.
- `Mission-related: System Testing` — rejected, and it is the closest of the four to warranting
  inclusion. `.github/workflows/downstream-testing.yml` and `.github/downstream-packages.json`
  register eleven downstream packages at this revision (ten of them enabled; `padre_sharp` carries
  `"enabled": false`) and run each package's own test suite against a candidate swxsoc branch, which
  is system-level integration testing in substance. It is nevertheless the project's own continuous
  integration configuration, not a capability the software offers anyone who installs it — by the
  same rule that a package's `pytest` suite does not make it testing software. A searcher looking
  for mission system-testing tooling would not be served by this package.
- `Data Visualization: Web-Based` — rejected, and this is a genuinely close call worth recording.
  The package writes measurements to AWS Timestream explicitly for dashboard display and creates
  Grafana annotations, so web dashboards are an outcome of using it. But swxsoc renders nothing
  itself: Grafana does. The only rendering code in the package is the matplotlib-backed
  `SWXData.plot()`, already covered by `Data Visualization: Line Plots`. The line drawn here is
  "does this software produce the visualization", and by that line the answer is no.
- `Data Processing and Analysis: File Format Conversion` — rejected. There is exactly one concrete
  I/O handler (see Fields 18/19); with a single supported format there is no format-to-format
  conversion. The `swxsoc/io/fillval.py` NaN/mask-to-`FILLVAL` round-trip is a representation
  detail within CDF, not a format conversion.
- `Servers and Environments` and its children — rejected. The package is a client library that calls
  AWS services (S3, Timestream, Lambda); it does not implement a server, a container image, or an
  HPC environment. The `.devcontainer/` directory is developer convenience, not a product feature.
- `Coordinate Transforms` and `Models and Simulations`, with all children — rejected. No coordinate
  system conversion and no physical model exists anywhere in the package; it neither computes nor
  simulates physical quantities.

### 5. Related Region (RECOMMENDED — treated as critical)

**Ordering rule:** `relatedRegion` is a sortedm2m field; the order below is HSSI's stored order and
is itself data. Do not alphabetise (that would swap both entries).

**Values, in stored order:**
1. `Interplanetary Space`
2. `Solar Environment`

Both retained. This vocabulary is **flat** — every row is top-level, and no value implies any other,
so a coarse region never entails a finer one and vice versa.

swxsoc is region-agnostic infrastructure in its own code; its regional character is inherited from
the missions whose configurations it ships. `swxsoc/data/config.yml` registers HERMES, whose
instruments (an electron electrostatic analyzer, a magnetometer, an electron/proton telescope and an
ion analyzer) measure the plasma and field environment traversed by the solar wind, and PADRE, a
solar X-ray mission. `Interplanetary Space` and `Solar Environment` cover those two cleanly, and a
searcher filtering HSSI by either region would reasonably expect the core library of those missions'
ground systems to appear.

**Considered and not selected: `Solar Wind`.** HERMES's instrument suite does measure solar wind
plasma directly, and because the vocabulary is flat, `Interplanetary Space` does not imply it, so
this would be a real addition rather than a redundant one. It was not selected because swxsoc
performs no solar-wind science: it contains no solar wind derivation, no plasma moment computation,
and no solar wind model. A user browsing HSSI's `Solar Wind` region for software to work with the
solar wind would find a CDF container and an S3 fetch client — useful to a HERMES team member,
mildly out of place to anyone else. That is the decision: `Solar Wind` stays out, and the reasoning
above is the accepted reasoning rather than a question left open. A future refresh should inherit
this judgement instead of reopening it; only new solar-wind *capability* in the package — a
derivation, a moment computation, a model — would warrant revisiting it. Note that `Solar Wind` also
exists as a Related Phenomena row, where it is excluded on the same reasoning; see Field 22.

**Considered and rejected:** every Earth-specific region (`Earth Ionosphere`, `Earth Magnetosphere`,
`Earth Thermosphere` and the rest), all planetary magnetospheres, `Corona`, `Chromosphere`,
`Photosphere`, `Solar Interior` and `Heliosheath`. None of the shipped missions targets these
regions, and the package contains no region-specific code at all.

### 6. Authors (MANDATORY)

**Ordering rule:** `authors` is a sortedm2m field. The order below is HSSI's stored order and is the
credit order that will be displayed and re-sent. Do not alphabetise or reorder by contribution.

**Author 1 — Steven Christe**
- **Given / Family:** Steven / Christe
- **Author Identifier:** `https://orcid.org/0000-0001-6127-795X`
- **Affiliation:** Goddard Space Flight Center — `https://ror.org/0171mag52`

**Author 2 — Damian Barrous-Dume**
- **Given / Family:** Damian / Barrous-Dume
- **Author Identifier:** `https://orcid.org/0009-0006-2684-0675`
- **Affiliations:** Community Coordinated Modeling Center — `https://ror.org/01dy3j343`; Navteca (no identifier)

**Author 3 — Andrew Robbertz**
- **Given / Family:** Andrew / Robbertz
- **Author Identifier:** `https://orcid.org/0009-0008-6857-0882`
- **Affiliations:** General Dynamics Mission Systems (no identifier); Goddard Space Flight Center — `https://ror.org/0171mag52`

**The author set is complete at three people, and that is a checked claim rather than an assumption.**
`pyproject.toml` declares exactly three authors. The Zenodo deposit for the current release lists
four `creators` entries but only three distinct people, because Damian Barrous-Dume appears twice
(see below). The deposit's `contributors` array is empty. There is no `CITATION.cff` and no
`.zenodo.json` in the tracked tree; `swxsoc/CITATION.rst` is a prose acknowledgement page naming no
individuals. No source names a fourth person, so no one is being dropped.

**Each ORCID was resolved and confirmed to be the right person.** `0000-0001-6127-795X` returns
given name Steven, family name Christe, with a current employment at NASA Goddard Space Flight
Center in the Solar Physics Laboratory as a Research Astrophysicist beginning 2010 — which
independently corroborates the stored Goddard affiliation. `0009-0006-2684-0675` returns
Damian / Barrous-Dume and `0009-0008-6857-0882` returns Andrew / Robbertz; neither record lists any
employment, so neither can corroborate or contradict its stored affiliations. None of the three
records carries a credit name or any other name, so the stored display names are the authoritative
forms.

**The hyphen in "Barrous-Dume" is correct, and the name question is settled.** A catalogue-wide
name-split correction was applied to this author on 2026-09-02; that decision stands and should not
be reopened. It is recorded here because the project's own sources disagree with each other and will
keep tempting a future agent to "fix" the stored value: `pyproject.toml` writes
"Damian Barrous Dumme" (doubled *m*, no hyphen), the Zenodo deposit contains both
"Damian Barrous Dume" and "Damian Barrous-Dume", and the PyHC registry `contact` field writes
"Damian Barrous Dumme". ORCID `0009-0006-2684-0675` gives the family name as `Barrous-Dume`, and the
person's own identifier record outranks a packaging file. HSSI's stored form already matches ORCID.

**The duplicated Zenodo creator explains the two stored affiliations, and the stored form is better
than its source.** The deposit lists Barrous-Dume once with affiliation `Navteca (NASA's
SMCE/CCMC/SWxSOC Teams)` and again with affiliation `Navteca`. The first is a packed affiliation
string — several institutions crammed into one free-text field, the shape that a naive import stores
only the first component of. HSSI instead holds two properly separated affiliation rows, Community
Coordinated Modeling Center and Navteca, which is a faithful unpacking of that string and strictly
better than what Zenodo provides. Do not "simplify" it back toward the deposit.

**The two identifier-less affiliations are correct as they stand — negative research, so this is not
re-run each refresh.** Navteca returned zero results from the ROR API when searched for this dossier
(2026-09-12), which is unsurprising for a small private contractor; it has no ROR to record.
"General Dynamics Mission Systems" had no ROR row of its own either — the closest candidate is the
parent company, `https://ror.org/05pyq8e17`
("General Dynamics (United States)"), which is a different legal entity from the subsidiary and
would be a downgrade in precision, not an improvement. Both affiliations should stay identifier-less.

**Do not attempt to add identifiers to these rows as part of a routine metadata update.** Sending an
identifier for an already-stored identifier-less person or organization does not annotate the
existing row; it resolves to a *new* row and orphans the original. If an identifier ever genuinely
needs to be attached to Navteca or General Dynamics Mission Systems, it requires a deliberate
database-side correction with its own review, not a field update.

**One divergence between sources, deliberately not acted on.** `pyproject.toml` at this revision
gives Robbertz the address `andrew.l.robbertz@nasa.gov`, while the published 0.2.3 distribution
carries `a.robbertz@gmail.com`. HSSI stores no author emails, so nothing follows for the record; it
is noted only so a future agent does not read the difference as evidence of two different people.

### 7. Software Name (MANDATORY)
**Value:** `SWxSOC`

The stored mixed-case form is correct and is an improvement over the lowercase package name `swxsoc`
that an earlier extraction recorded. The project renders itself "SWxSOC" throughout: the
documentation front page (`docs/index.rst`) is titled "SWxSOC Core Documentation", the README's Code
of Conduct section addresses the reader with "When you are interacting with the SWxSOC community you
are asked to follow our Code of Conduct." (the last three words are a hyperlink in the source; only
the link target is dropped here), and the project logo is a wordmark reading SWxSOC. The README's
Licenses section is *not* evidence for this and must not be cited as such: it reads in full "See the
license/LICENSE file for more information." and names no community. An earlier revision of this
dossier attributed the community phrasing to it, which was wrong; the front-page title and the logo
are each independently sufficient. `swxsoc` is merely the importable module and PyPI distribution
name, which convention forces to lowercase; it is not the software's name. Do not revert this to the
package name.

### 8. Description (MANDATORY)
**Value:**

> A Python package to support the SWxSOC instrument packages. This package provides core
> functionality for all SWxSOC Mission Packages, including data access, pipeline processing, and
> analysis tools for space weather data processing. The package provides a generic object (SWXData)
> for loading, storing, and manipulating space weather time series data with support for
> ISTP-compliant CDF files.

Retained unchanged. Its first sentence matches the `description` field in `pyproject.toml` exactly,
and the remainder accurately describes `SWXData` and the CDF/ISTP support that the code implements.
This text is also richer than the variant in the earlier extraction, which omitted "data access"
from the capability list; the stored wording is the better one and is kept.

This description does understate the package as it now stands — it predates the absorption of
`sdc_aws_utils` and MetaTracker, and so says nothing about file tracking, cloud transfer, or
operations dashboards. That is a candidate for a future rewrite, but it is a matter of editorial
judgement about maintainer-authored prose rather than a factual error, so the maintainers' own
wording stands.

### 9. Concise Description (OPTIONAL)
**Value:**

> Core functionality package for SWxSOC mission providing data access, processing, and analysis
> tools for space weather instruments.

Retained unchanged. Accurate, appropriately short, and a better summary than the earlier
extraction's variant, which dropped "data access". No stylistic rewrite was attempted: this is
serviceable prose and replacing it would be churn.

### 10. Publication Date (RECOMMENDED)
**Value:** `2024-11-27`

The date of the first public release, `0.1.0`. Corroborated three ways: the GitHub release for tag
`0.1.0` was published `2024-11-27T20:05:16Z`, the PyPI upload for `0.1.0` is timestamped
`2024-11-27T20:05:55Z`, and the Zenodo deposit series begins there. Retained.

Note that this is deliberately the *first* release date, not the latest one — the latest release
date belongs to Field 12, where it is recorded. Do not update this field when a new version ships.

### 11. Publisher (RECOMMENDED)
**Value:** Zenodo — `https://zenodo.org`

Retained. Zenodo is where the software's DOIs are minted and where the archived releases live. No
other publisher is claimed by any source.

### 12. Version (RECOMMENDED)

- **Version Number:** `0.2.3`
- **Version Date:** `2026-01-12`
- **Version Description:** Maintenance and pipeline release: adds PADRE spacecraft support and Unix
  timestamp parsing, adds a data descriptor, extends Timestream recording to arrays, NaNs and
  boolean types, updates logger formatting, migrates linting to ruff, and fixes a bad time match and
  a ReadTheDocs build failure.
- **Version PID:** `https://doi.org/10.5281/zenodo.18226255`

**This supersedes `v0.2.2`, the version HSSI recorded before this refresh, which had gone stale.**
Release `0.2.3` was published `2026-01-12T21:37:03Z` on GitHub, uploaded to PyPI at
`2026-01-12T21:37:43Z`, and archived as Zenodo record `18226255` with `metadata.version` `0.2.3`.
PyPI's own `info.version` for the project is `0.2.3`. That was an objective advance on the superseded
value, not a matter of taste.

**The number is recorded without a leading `v`, and dropping the prefix is deliberate.** The version
entry HSSI held before this refresh spelled the number `v0.2.2`, with a prefix the project itself
does not use: all five tags in the repository — `0.1.0`, `0.2.0`, `0.2.1`, `0.2.2`, `0.2.3` — are
unprefixed, as the tag inventory below records, and every published form of the release agrees with
the tags rather than with the prefixed spelling (PyPI's releases are `0.1.0`, `0.2.1`, `0.2.2` and
`0.2.3`; each GitHub release `name` is identical to its `tag_name`; the Zenodo deposit's
`metadata.version` is `0.2.3` and its title is "swxsoc/swxsoc: 0.2.3"). So `0.2.3` drops the `v` as
well as advancing the number, and that drop is intentional rather than a transcription slip. Record
the number in the project's own unprefixed form in future refreshes; do not restore the `v` for
consistency with the older entry. The same superseded entry recorded a release date of `2025-06-07`,
a version PID of `https://doi.org/10.5281/zenodo.15615510`, and an **empty** description — which is
why a version description is supplied above.

**The version description was derived from the release body, because the release `name` carries no
information.** Both the `0.2.3` and `0.2.2` GitHub releases have a `name` identical to their
`tag_name` — the project does not title its releases. The description above therefore summarises the
eleven merged pull requests listed in the release body, which is the only substantive content
available. A future refresh should check the `name` again rather than assuming it stays empty.

**Two version anomalies, established rather than guessed at, so they are not re-investigated later.**

*There is no orphan-lineage problem.* All five tags — `0.1.0`, `0.2.0`, `0.2.1`, `0.2.2`, `0.2.3` —
are ancestors of this source revision, and five tags is the repository's complete tag set. Version
history can be read from the pinned lineage directly.

*Release `0.2.0` was tagged and released on GitHub but never published to PyPI.* PyPI carries
`0.1.0`, `0.2.1`, `0.2.2` and `0.2.3` only, while GitHub carries a non-draft, non-prerelease `0.2.0`
published `2025-05-29`. This is a declared-but-not-distributed release. It does not affect the
current value and requires no action; it is recorded so a later agent reconciling GitHub against
PyPI does not treat the gap as a fetch failure.

*The changelog is stale and internally inconsistent — do not date anything from it.* `CHANGELOG.rst`
contains two separate headings reading `Latest` and a single numbered heading, `0.0.0 (2023-03-22)`.
That entry cannot describe a real release: no `0.0.0` tag exists in the repository, and the earliest
commit in this lineage is dated 2024-01-12, more than nine months after the claimed date. It is
leftover template text. All release dates in this dossier come from GitHub releases, PyPI upload
timestamps and Zenodo deposits instead.

### 13. Programming Language (RECOMMENDED)
**Value:** `Python 3.x`

**The criterion, settled once and applied to inclusions and exclusions alike:** this field asks for
the languages *most important* to the software and is explicitly not meant to be exhaustive. So the
question is not "does any file of language X exist" but "would a user need X to understand, build or
extend this software".

By that criterion `Python 3.x` is the answer and the only answer. The package is pure Python:
across all 138 tracked files at this revision, 72 are `.py`, and a search of the whole tracked tree
for `*.c`, `*.h`, `*.f`, `*.f90`, `*.pyx` and `*.cpp` returns zero files, so there is no compiled
extension to speak of. `pyproject.toml` sets `requires-python = ">=3.10"`, and continuous
integration tests Python 3.10 through 3.14.

**Exclusions derived from the same criterion.** `Python 2.x` is excluded because the floor is 3.10.
`C` is excluded despite CDF support ultimately reaching a C library: that library is NASA's CDF
distribution, an external system dependency reached through spacepy, and no C is written, shipped or
built here. YAML, TOML and reStructuredText appear in the tree but are configuration and
documentation formats, and in any case none is a row in this vocabulary. `SQL` is excluded even
though MetaTracker uses a relational database, because the package expresses its schema through
SQLAlchemy's Python API and ships no SQL source.

Cross-check: the Python version range in the earlier extraction (3.9–3.13) is now stale; the pinned
revision tests 3.10–3.14. This does not change the field's value, which is version-agnostic.

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found — **evidenced empty, on the project's own statement.**

This is not a failed search. The package ships a citation page, `swxsoc/CITATION.rst`, which
instructs users to cite the version-specific Zenodo DOI and then states plainly:
"A paper citation does not yet exist."

That is the maintainers' own declaration that no reference publication exists, and it outranks any
inference from a literature search. A future agent should re-read that file: if the sentence has
been replaced by a citation, this field should be filled from it.

Note the distinction from Field 27: conference material *about* this software does exist and is
recorded there. None of it is a peer-reviewed reference publication for the software, and promoting
a conference poster into this field would misrepresent it.

### 15. License (RECOMMENDED)
**Value:** `Apache License 2.0`

HSSI held no licence value for this entry before this refresh; this is the value that fills that
gap, recorded verbatim as the live `License` vocabulary's row name.

**The repository states three different things about licensing, so this needs to be argued rather
than asserted.**

1. The formal licence file is Apache-2.0. `LICENSE.rst` at the repository root contains only the
   redirect "see licenses/LICENSE.md", and `licenses/LICENSE.md` is the full Apache License 2.0
   text. This is also the file the packaging metadata points at:
   `pyproject.toml` declares `license = {file = "LICENSE.rst"}`.
2. The README carries a "Public Domain" section dedicating the work to CC0, on the grounds that
   "This project constitutes a work of the United States Government and is not subject to domestic
   copyright protection under 17 USC § 105. Additionally, we waive copyright and related rights in
   the work worldwide through the CC0 1.0 Universal public domain dedication." (In the source both
   the statutory citation and the dedication are hyperlinks; only the link targets are dropped here.)
3. The Zenodo deposit records `{'id': 'cc-by-4.0'}`.

**Apache-2.0 is the right answer.** It is the project's actual, complete licence *file*, and it is
the licence the distribution declares — PyPI's metadata for `swxsoc` reports the licence as the
literal string `see licenses/LICENSE.md`, resolving to Apache-2.0. Licence history reinforces this:
`licenses/LICENSE.md` was added in the initial infrastructure commit on 2024-01-22 and has not been
modified in this lineage since, and no licence file has ever been deleted from the repository. The
current licence therefore is, and has always been, Apache-2.0.

**The Zenodo `cc-by-4.0` value is explicitly rejected**, and the vocabulary row
`Creative Commons Attribution 4.0 International` must not be selected on its strength. DOI-autofill
licence values are re-derived from the repository as settled policy, because Zenodo's licence field
is a depositor-selected default that frequently fails to match the code's actual licence — as it
does here. CC-BY-4.0 is a content licence, unsuited to software, and nothing in the repository
mentions it.

**The README's CC0 dedication is noted but not selected, for two independent reasons.** First, it
cannot be recorded even if one wanted to: the live `License` vocabulary contains no CC0 or public
domain row at all, so there is no value to choose. Second, it conflicts with the licence file itself,
and a formal `LICENSE` file that the packaging metadata points to is the stronger signal of intent
than a README passage inherited from a US-Government project template. The tension is real and
belongs upstream — a maintainer could reasonably be asked which governs — but it does not make
Apache-2.0 the wrong catalogue value.

**Near-match row ruled out by name:** `Creative Commons Attribution 4.0 International` is the only
Creative Commons row in the vocabulary and is not this software's licence, per the reasoning above.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values:**
`cdf`, `data analysis`, `data container`, `hermes`, `nasa mission`, `padre`, `space weather`,
`swxsoc`, `impax`

These are the stored lowercase row names; compare against those rather than against HSSI's
title-cased display form. Eight of the nine were on the record before this refresh; `impax` is the
ninth, and is argued below.

`pyproject.toml` declares `keywords = ["swxsoc", "nasa mission", "space weather"]`, and the PyHC
registry adds `data_container`, `cdf`, `data_analysis` and `hermes`. The eight that predate this
refresh — every value above except `impax` — cover both, normalised to spaced lowercase, and
additionally carry `padre`, which is supported by the shipped mission configuration.

A caution about case: this vocabulary is open, so an unmatched value creates a new row, but a
case variant binds the existing row rather than duplicating it. Record the lowercase forms above.

**`impax` is recorded on exactly the same evidence that justifies the stored `hermes` and `padre`,
and that is settled.** `swxsoc/data/config.yml` registers `impax` as a first-class mission — the
Imaging Microburst Precipitation with Atmospheric X-ray emissions CubeSat — with its own data levels
and three instruments, and the downstream testing manifest lists three IMPAX packages
(`impax_iaxis`, `impax_ifire`, `impax_craft`) that build on swxsoc. Someone searching HSSI for IMPAX
software should find the core library those packages depend on, and would be glad to — which is the
test this keyword passes and the two rejected below fail.

**Considered and rejected: `reach`.** REACH is also present in the configuration, but it appears
under a `swxsoc_pipeline` grouping described in the file as a convenience collection rather than as a
mission in its own right — a weaker warrant than HERMES, PADRE or IMPAX have. More decisively,
"reach" is a common English word, so as a search keyword it would match noise rather than help
anyone find this package. The purpose of a keyword is to be found by, and this one would not serve.

**Considered and rejected: `general`.** The PyHC registry lists `general` among this project's
keywords, and an earlier extraction carried it across. It is deliberately not recorded here, and
that is the better outcome: a keyword that applies to everything distinguishes nothing and is
useless for search. Do not reintroduce it from the registry.

### 17. Data Sources (OPTIONAL)

**Values:**
- `S3/Cloud-aware`
- `Observatory/Mission-specific`

HSSI held no data sources for this entry before this refresh. Both values are recorded verbatim as
live `DataInput` row names.

`S3/Cloud-aware` is established directly by the code: `swxsoc/net/client.py` opens with "SWXSOC FIDO
Client for searching and fetching data from AWS S3.", and `swxsoc/io/s3.py` implements a full
boto3-backed transfer layer (`create_s3_client_session`, `list_files_in_bucket`,
`download_file_from_s3`, `upload_file_to_s3`, `copy_file_in_s3`). Cloud object storage is this
package's data source, not an implementation detail.

`Observatory/Mission-specific` follows because the client does not search a general archive: queries
are expressed with mission-scoped attributes (`Instrument`, `Level`, `Descriptor`,
`DevelopmentBucket`) resolved against the active mission's configuration, so the data retrieved is
specific to SWxSOC's own missions. This is also the value that Field 31/32 guidance directs to be
selected alongside an observatory-specific data source.

**Considered and rejected:** `CDAWeb`, `HAPI`, `SSCWeb`, `OMNIWeb`, `VirES`, `Madrigal`, `AMDA`,
`das2`, `GFZ`, `WDC`, `TAP` and `The Virtual Solar Observatory.` — the package implements no client
for any of these; its only remote protocol is AWS S3. `FTP/FTPS Directories` and
`HTTP/HTTPS Directories` were also rejected: although the package makes HTTP calls, those are to the
Grafana, Slack and Mattermost APIs, not to directory-listing data archives, and the science-data
path is S3. `Other` was rejected because two specific rows apply, making the catch-all
strictly less informative. An earlier extraction recorded `Other`; the specific values supersede it.

### 18. Input File Formats (RECOMMENDED)
**Values:** `CDF`, `ISTP-Compliant` — retained.

### 19. Output File Formats (RECOMMENDED)
**Values:** `CDF`, `ISTP-Compliant` — retained.

`swxsoc/io/cdf_handler.py` defines `CDFHandler`, which both reads and writes CDF, and
`swxsoc/util/schema.py` enforces ISTP-compliant metadata on the files produced, so the same pair is
correct for input and output.

**FITS was investigated at length and is deliberately excluded. Do not add it.** Several signals
invite the mistake: `pyproject.toml` defines a `fits` extra, the shipped configuration lists a
`fits` file type, and the PADRE mission is configured with `file_extension: fits`. All three are
misleading. The `fits` extra is annotated in `pyproject.toml` as "provided for completeness but
installs no additional packages". `swxsoc/io/__init__.py` states that the package provides
"concrete file-format handlers (currently :class:`CDFHandler` for CDF files) and shared utilities
such as :mod:`swxsoc.io.fillval` …" — one concrete handler, and it is not FITS. And the
test suite asserts the absence directly: `swxsoc/io/tests/test_io.py` contains the comment
"But SWXData.load() cannot read FITS format (only CDF)" followed by
"SWXData.load(fits_path)  # Will fail - no FITS handler exists" inside a raises-block. The
configuration's FITS entries drive MetaTracker's filename parsing and bookkeeping, not file I/O.

**`csv` and `JSON` excluded** for the same reason: the configuration's `.csv` and `.json` file rules
parse *filenames* to extract timestamps and data levels; no CSV or JSON science reader exists.
JSON appears otherwise only as HTTP request payloads to the Grafana, Slack and Mattermost APIs,
which is API plumbing rather than a data format the software supports.

**`ascii`, `HDF5`, `netCDF3/4`, `IDL.sav`, `Zarr` and `Other` excluded** — no reader or writer for
any of them exists in the package.

### 20. Operating System (RECOMMENDED)
**Values:** `Linux`, `Mac`, `Windows` — retained.

Established by continuous integration rather than by claim: `.github/workflows/testing.yml` runs the
full test suite on a matrix of `[ubuntu-latest, macos-latest, windows-latest]` against Python 3.10
through 3.14, on every push and pull request to `main` and on a daily schedule. All three stored
values are therefore actively verified by the project itself.

`Operating System Independent` was considered and rejected in favour of naming the three tested
platforms, which is more informative to a user deciding whether the package runs on their machine —
particularly because the optional CDF support depends on NASA's CDF library being installable
separately, a platform-sensitive step the README warns about. `Solaris`, `MobilePlatform` and
`Other` are untested and unclaimed.

### 21. CPU Architecture (RECOMMENDED)
**Value:** `CPU Independent` — retained.

The package is pure Python with no compiled extension modules anywhere in the tracked tree (see
Field 13), and it publishes no architecture-specific wheels. Nothing in it is sensitive to CPU
architecture. `x86-64`, `Apple Silicon arm64`, `Linux aarch64 or arm64`, `ppc64le`, `Sun (SPARC)`,
`GPU` and `HPC or HEC` are all rejected: naming any specific architecture would wrongly imply the
others are unsupported.

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found — **evidenced empty. This field was examined, not skipped.**

This vocabulary is **flat** and small; every row was considered individually against the software:
`Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`,
`Solar Wind`, `X-ray emission`.

The package implements nothing that detects, models, characterises or analyses any physical
phenomenon. It is a container, an I/O layer, a fetch client, a file-tracking database and a set of
dashboard integrations. A user filtering HSSI by a phenomenon is looking for software that will help
them study that phenomenon, and swxsoc would not.

**The near misses, so that a future agent does not mistake them for evidence.** A search of the
`swxsoc` and `docs` trees for phenomenon terms returns essentially nothing usable: "flare" appears
only as example annotation text in the Grafana user guide ("Observed solar flare") and as dashboard
names in Grafana unit-test fixtures — illustrative strings, not functionality. "X-ray" appears only
inside instrument and mission *names* in the configuration (`Solar HARd X-ray Polarimeter`, and the
IMPAX expansion). "Solar Wind" appears once, as an allowed value in the ISTP discipline list inside
the default global CDF attribute schema — that is a generic ISTP controlled vocabulary the package
enforces on any mission's metadata, not a statement about swxsoc's science. "Coronal mass",
"geomagnetic storm", "corona" and "aurora" return no hits at all.

**The one arguable case, considered and decided: `Solar Flares` and `X-ray emission` are not
inherited from PADRE, and this field stays empty.** Both could be argued for — PADRE's entire
scientific purpose is hard X-ray polarimetry of solar flares, and swxsoc ships PADRE's mission
configuration. The same inheritance argument *was* accepted for Related Region (Field 5), so the
asymmetry needs a reason, and it has one: region and phenomenon ask different questions. A region
describes where a mission's data comes from, which is a property of the data swxsoc handles; a
phenomenon describes what the software helps you study, which is a property of its capabilities.
swxsoc has no flare capability — no detection, no characterisation, no modelling — so someone
filtering HSSI by `Solar Flares` for software to study flares with would find this package out of
place. The decision is settled and a future refresh should inherit it; only actual flare or X-ray
analysis capability entering the package would warrant reopening it.

### 23. Development Status (RECOMMENDED)
**Value:** `Active`

HSSI held no development status for this entry before this refresh. `Active` is recorded verbatim
as the live `RepoStatus` vocabulary's row name.

Based on commit activity, not on a repository timestamp. The pinned lineage carries 113 commits, of
which 32 fall in 2026, and the most recent is dated 2026-09-09 — three days before this extraction.
Recent work is substantive rather than cosmetic: two formerly separate packages were merged in
during August 2026 (`sdc_aws_utils` and MetaTracker), a Mattermost client was added, and CDF support
was made optional. The most recent release, 0.2.3, shipped 2026-01-12, and continuous integration
runs on a daily schedule.

`Unsupported` is ruled out because the repository is not archived (measured 2026-09-12 via the
GitHub API). `Inactive` is ruled out by the commit record above — this is not a quiet-but-open
repository. `WIP` was considered, since `pyproject.toml` still declares the classifier
`Development Status :: 3 - Alpha`; it was rejected because that classifier has not been revised
since early in the project's life and is contradicted by five tagged releases — four of them
published to PyPI, the exception being `0.2.0`, as Field 12 records — downstream mission packages
depending on the library, and daily CI. `Concept`,
`Moved`, `Suspended` and `Abandoned` are all plainly inapplicable.

Note for future refreshes: GitHub's `updated_at` field is not a measure of commit activity — it
advances on stars, forks and metadata edits. Derive this field from the commit log.

### 24. Documentation (RECOMMENDED)
**Value:** `https://swxsoc.readthedocs.io/en/latest/`

Retained. Fetched and confirmed reachable (HTTP 200, no redirect away from the URL). This exact URL
is declared in `pyproject.toml` under `[project.urls] Documentation`, is linked from the README, and
matches the PyHC registry's `docs` entry apart from the explicit `/en/latest/` suffix, which is the
more precise form and is preferred.

The documentation is substantial and version-controlled in the repository: 38 of the 138 tracked
files are `.rst`, organised into a user guide (twelve topic pages), a developer guide, an API
reference, a CMAD section and examples.

**The GitHub wiki did not exist when this was checked (2026-09-12).** The durable point is the trap,
not the result: a repository's wiki lives in a *separate* git repository, and the API's `has_wiki`
flag reports only that the feature is enabled, never that any content exists — so `has_wiki` must
never be read as evidence either way. Probing the wiki repository directly returned "Repository not
found", so there was no wiki documentation to record. A maintainer could create one later; if this
field is ever revisited, probe the wiki repository again rather than re-deriving the question.

### 25. Funder (OPTIONAL)
**Value:** Not found — **evidenced empty.**

### 26. Award Title (OPTIONAL)
**Value:** Not found — **evidenced empty.**

**The repository contains no funding information at all, and this was searched rather than assumed.**
A case-insensitive search of the entire tracked tree for `fund`, `grant`, `award`, `acknowledg`,
`NNX`, `80NSSC` and `contract` returns only false positives, every one of which was resolved
individually: the "grants"/"contract" hits are Apache-2.0 licence boilerplate in
`licenses/LICENSE.md` and liability clauses in the bundled `ASTROPY.rst`, `SPACEPY.rst` and
`SUNPY.rst` third-party licence files; `README.rst` has an "Acknowledgements" heading, but it
acknowledges the OpenAstronomy and SunPy *package template*, not any funder; `swxsoc/CITATION.rst`
uses "acknowledgement" in the sense of how to cite the software; and the two remaining hits are the
generic ISTP `Acknowledgement` attribute definition in the default global CDF attribute schema and a
table row naming that attribute in the CDF format guide. Neither Zenodo deposit metadata nor PyPI
metadata carries funding information either.

**Rejected on principle, not merely on absence: author-level support statements from related
publications.** The conference material recorded in Field 27 is NASA-affiliated work and its
acknowledgements may well name awards supporting its authors. Such statements are *author-level
support, not software funding*, and must not be copied into Fields 25/26 — this distinction has been
confirmed twice as campaign policy. Likewise, a funder named by a paper that merely cites this
software is that paper's funder, not this software's. These fields stay empty unless the repository,
the deposit metadata, or a maintainer states who funded *swxsoc itself*.

Should a specific award ever be identified, note that recording it is a decision to escalate rather
than a default: an award with no matching row in HSSI requires a deliberate choice, not an
invented entry.

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Values:**
- `https://doi.org/10.5281/zenodo.8408028` — "Open Science in Action: SWxSOC's Role in Accelerating Data Release and Cloud Processing for Heliophysics Missions" (2023-10-09)
- `https://doi.org/10.5281/zenodo.8400671` — "The Architecture and Functionality of HERMES Core and Instrument Python Packages" (2023-10-09)

HSSI held no related publications for this entry before this refresh. Both were located through a
full-text literature search and then verified against their own deposit records for title, date, type
and authorship.

The first is squarely about this software's project: a presentation on SWxSOC's role in data release
and cloud processing, describing the Science Operations Center that `swxsoc` is the core library of.
Its author list — Damian Barrous-Dume, Amy Catherine Rager, Andrew Robbertz, Daniel Skeberdis,
Steven Christe, Steve Kreisler, Tony Mercer, William R Paterson — includes all three of this
software's authors.

The second is a poster on the architecture of the HERMES core and instrument Python packages, by the
same team. It is included deliberately even though it names `hermes_core` rather than `swxsoc`: the
two are directly connected in lineage. `CHANGELOG.rst` records "Added Functionality from HERMES
partner package.", and `swxsoc` is the generalisation of that HERMES-specific core into a
multi-mission library, with `hermes_core` now among its downstream consumers (see Field 29). It is
the closest thing to a written architecture description this software has, and a user reading the
swxsoc entry would be glad to find it rather than puzzled by it.

**A name collision that will mislead the next literature search — do not add these.** Searching for
HERMES returns a substantial body of work on a completely different HERMES: the Italian
HERMES Pathfinder / HERMES-TP-SP CubeSat constellation for high-energy astrophysics. Papers such as
"HERMES SOC activities at the ASI space science data center (SSDC)", "The HERMES-technologic and
scientific pathfinder" and "HERMES Pathfinder & SpIRIT: a progress report" refer to that project and
have no connection to NASA's Heliophysics Environmental and Radiation Measurement Experiment Suite
or to this software. The phrase "HERMES SOC" appears in both projects, which makes the trap
particularly easy to fall into.

**Considered and not selected:** several AGU abstracts by the same team mention SWxSOC — including
"SWxSOC Packages for Processing Space Weather Science Data in Python" (2024,
`2024AGUFMSM43C2858R`), "The Architecture and Functionality of the Python Packages for the HERMES
Mission" (2023, `2023AGUFMSH33E3097R`) and two years of "Enhancing SWxSOC through Open Collaboration
for Multi-Mission Data Processing and Expedited Release" (`2024AGUFMIN13C2176B` and
`2025AGUFMIN33E0396K`, which carry that identical full title). All are topically apt, and the first
is the closest thing to a paper about these packages. None carries a DOI in the literature index,
and this field is filled with DOIs. They are recorded here with their bibcodes so that a future agent
who does locate DOIs for them can add them without repeating the search.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found.

No dataset DOI is referenced anywhere in the repository, in either Zenodo deposit's
`related_identifiers`, or in the two publications above. The package ships one small sample CDF file
(`swxsoc/data/sample/hermes_nms_default_l1_20160322T123031_v0.0.1.cdf`) used for tests and examples;
it is a test fixture bundled inside the source distribution, not a published dataset with an
identifier, and it must not be recorded here. The mission data the package fetches lives in SWxSOC's
S3 buckets and is not separately deposited with a DOI.

### 29. Related Software (OPTIONAL)

**Values:**
- `https://doi.org/10.5281/zenodo.14887800` — sammi-cdf
- `https://github.com/HERMES-SOC/hermes_core`
- `https://github.com/spacepy/spacepy`

**What that DOI actually is — resolved, because the record gave no clue.** HSSI carried
`10.5281/zenodo.14887800` in both this field and Field 30 before this refresh, with no accompanying
name to say what it was. It is the Zenodo **concept** DOI for `swxsoc/sammi`, titled `sammi-cdf` and
licensed Apache-2.0. Concept rather than version is a structural property and does not need
re-checking: its DataCite record carries `HasVersion` relations to the individual release DOIs,
which a version DOI does not. Which deposit it happens to land on moves with every sammi release and
is not worth recording as a fact about this software — when this dossier was compiled (2026-09-12)
it led to record `20858467`, version `v1.1.0`. It is *not* a swxsoc DOI. That identifier is correct
and is recorded in both fields; the reasoning for each differs and is given separately.

**sammi-cdf belongs in Field 29** as a companion package by the same team. `pyproject.toml` states
that "sammi-cdf is maintained by the SWxSOC team with metadata support for SWxSOC data products",
and it appears in the PyHC registry in its own right, described as "Share Attribute and Metadata
Management Interface - Manage attributes for ISTP CDF files using YAML". It is a domain-specific
dependency, installed with the `cdf` extra — precisely the sort of distinguishing, non-generic
package this field is for.

**`hermes_core` is recorded as the predecessor and partner package.** `CHANGELOG.rst` records "Added
Functionality from HERMES partner package.", and the developer guide states that "``swxsoc`` is a
foundational library shared by multiple mission packages (``hermes_core``, ``padre_meddea``,
``padre_sharp``, ``padre_craft``, ``swxsoc_reach``, ``sdc_aws_utils``, ``MetaTracker``, and
others)." — naming `hermes_core` first. It is a distinct, separately catalogued package — PyHC
lists it as "HERMES-Core", "A central
Python Package for common functionality across all HERMES instruments" — and understanding the
relationship between the two is exactly what this field exists to convey. The URL used is the one
HSSI's related-item vocabulary already carried for this package, which keeps the two references
pointing at the same target rather than creating a near-duplicate.

**`spacepy` belongs here as a domain-specific dependency, and its placement in this field rather
than in Field 30 is deliberate.** It is heliophysics software, not generic infrastructure, so the
Tier A exclusion does not reach it. It is also genuinely load-bearing and user-visible: all CDF
reading and writing goes through `spacepy.pycdf`, the `cdf` extra installs it, and the README warns
that "CDF support requires the NASA CDF library to be installed separately on your system", pointing
users at spacepy's installation guide. A user who needs CDF support from swxsoc must deal with
spacepy directly, which makes the relationship worth surfacing. Why it is *not* in Field 30 is
argued there.

**Considered and not selected: the downstream mission packages.** The repository's
`.github/downstream-packages.json` lists eleven packages that build on swxsoc and are tested against
it: `padre_meddea`, `padre_sharp`, `padre_craft`, `swxsoc_reach`, `impax_iaxis`, `impax_ifire`,
`impax_craft`, and four `sdc_aws_*` Lambda functions. Each is a genuine companion, and a case can be
made for listing them. They were not added for two reasons: listing eleven repository URLs would
swamp the field and bury the three relationships that actually explain what this software is, and
none of them is catalogued in HSSI, so each would render as a bare external URL. `hermes_core` was
selected from this group because it alone is the lineage ancestor and is already known to the
catalogue. **The scope of this field is settled at three — sammi-cdf, `hermes_core` and `spacepy` —
and the eleven downstream packages stay out.** The reasoning above stands as the reason for a
rejected alternative, not as an open question. The one condition that would justify reopening it is
those packages being catalogued in HSSI themselves, at which point each would render as a real
in-catalogue relation instead of a bare external URL.

**Rejected — the generic stack.** `numpy`, `PyYAML`, `parfive`, `boto3`, `httpx`, `requests`,
`SQLAlchemy`, `tenacity`, `slack_sdk`, `mattermostautodriver`, `pytest`, `setuptools`, `ruff` and
`matplotlib` are all dependencies and none belongs here. Applying the governing test — would this
package be equally at home in a web application, a finance model, or a biology pipeline? — each is
plainly yes: they are HTTP clients, cloud SDKs, ORMs, chat SDKs, downloaders, serialisation,
plotting, packaging and testing. Being a dependency is not a relationship worth cataloguing, and the
Tier A exclusion applies to this field just as it does to Field 30.

### 30. Interoperable Software (OPTIONAL)

**Values:**
- `https://doi.org/10.5281/zenodo.14887800` — sammi-cdf
- `https://github.com/sunpy/sunpy`
- `https://github.com/sunpy/ndcube`
- `https://github.com/astropy/astropy`

Each entry below is justified by a *specific* exchange in the public API, as this field requires;
none rests on dependency presence, ecosystem membership, or PyHC affiliation.

**sammi-cdf — a plugin/extension relationship.** The identifier recorded here,
`10.5281/zenodo.14887800`, is sammi-cdf's Zenodo **concept** DOI rather than a version DOI — its
DataCite record carries `HasVersion` relations to the individual release DOIs — so it keeps pointing
at the package itself rather than at one frozen release, which is what this field wants. Field 29
records the same identifier and the same fact; it is restated here so that an audit of this field
alone is not left to infer it. `swxsoc/util/schema.py` contains
`from sammi.cdf_attribute_manager import CdfAttributeManager`, and `SWXSchema` extends that class to
drive ISTP attribute handling. swxsoc does not merely call sammi; it builds its schema type on
sammi's. Storing the same identifier in both Fields 29 and 30 is correct here, because sammi-cdf is
simultaneously a companion package and a demonstrated integration.

**sunpy — a plugin/extension relationship, which this field names explicitly as qualifying.**
`SWXSOCClient` is declared as `class SWXSOCClient(BaseClient)` against sunpy's
`sunpy.net.base_client.BaseClient`, and its docstring states that it "provides search and fetch
functionality for SWXSOC data and is based on the sunpy BaseClient for FIDO." `swxsoc/net/attr.py`
imports `sunpy.net.attrs` and sunpy's `AttrAnd`, `AttrOr`, `AttrWalker` and `SimpleAttr`, and maps
sunpy attributes onto SWxSOC ones. In practical terms swxsoc registers itself as a client within
sunpy's Fido search framework — a sunpy user reaches SWxSOC data through sunpy's own interface.

**ndcube — a shared data model.** This is the same relationship the field guidance offers as
a worked example of a qualifying case. `SWXData.__init__` accepts `spectra: Optional[ndcube.NDCollection]`
and raises if given anything else, and the I/O layer's public contract returns one:
`def load_data(self, file_path: Path) -> Tuple[dict, dict, NDCollection, dict]:`. `NDCube` and
`NDCollection` objects pass across swxsoc's public boundary in both directions.

**astropy — Tier B, cleared on a documented interchange format rather than on dependency.**
The public constructor's own signature is the evidence:
`timeseries: Union[astropy.timeseries.TimeSeries, dict[str, astropy.timeseries.TimeSeries]]`, with
`support: Optional[dict[Union[astropy.units.Quantity, astropy.nddata.NDData]]]`. A user builds an
astropy `TimeSeries`, hands it to swxsoc, and gets one back — astropy objects *are* swxsoc's
interchange currency, which is the documented-interchange standard this tier requires, not the
"uses it internally" case it excludes.

**spacepy — considered carefully and rejected from this field, though it is recorded in Field 29.**
This is the closest call in the pair of fields and is written down so it is not relitigated.
spacepy is genuine heliophysics software and clears Tier A easily, so the rejection is not about
what kind of package it is. It fails the *demonstrated exchange* test specifically: no spacepy type
ever crosses swxsoc's public boundary. The handler signatures are
`load_data(...) -> Tuple[dict, dict, NDCollection, dict]` and `save_data(self, data, file_path: Path, ...)` —
dictionaries and ndcube objects, never `spacepy.pycdf.CDF` or `spacepy.pycdf.Var`. Those spacepy
types appear only inside `swxsoc/io/cdf_handler.py` and in parameter documentation for internal
helpers. This is the "uses X internally" pattern that this field explicitly does not accept, as
distinct from "the public API returns X as its documented interchange format", which is what
astropy and ndcube do. A user does not combine swxsoc and spacepy as peer tools; spacepy is the
engine under swxsoc's CDF support, which is why Field 29 is the right home for it.

**Rejected — the generic stack**, on the same reasoning given in Field 29: `numpy`, `matplotlib`,
`PyYAML`, `boto3`, `httpx`, `requests`, `parfive`, `SQLAlchemy`, `tenacity`, `slack_sdk`,
`mattermostautodriver` and `pytest`. Note particularly that `matplotlib` is excluded despite
`SWXData.plot()` being a real, documented feature: plotting with matplotlib is true of most of the
scientific Python ecosystem and distinguishes nothing about this package. `Grafana` was also
considered and rejected — swxsoc calls its HTTP API, but Grafana is a general-purpose dashboarding
product rather than a heliophysics peer tool, and the relationship is consumption of a service, not
interoperation between two science packages.

### 31. Related Instruments (OPTIONAL)
**Value:** Not found — **evidenced empty. No usable SPASE identifier exists for any of them.**

**This is not a relevance failure — it is a vocabulary gap, and the distinction matters.** The
software genuinely supports specific instruments. `swxsoc/data/config.yml` registers, as first-class
configured instruments with target names, file rules and data levels:

- HERMES — `eea` (Electron Electrostatic Analyzer), `nemisis` ("Noise Eliminating Magnetometer
  Instrument in a Small Integrated System"), `merit` (Miniaturized Electron pRoton Telescope),
  `spani` (Solar Probe Analyzer for Ions)
- PADRE — `meddea`, `sharp` ("Solar HARd X-ray Polarimeter"), `craft` (PADRE Spacecraft)
- IMPAX — `iaxis`, `ifire`, `craft` (IMPAX Spacecraft)
- SWxSOC pipeline grouping — `reach`

These pass the designed-to-support test comfortably: this is not a tutorial mention or a
"configurable for" claim, but shipped configuration that drives filename parsing, data-level
promotion and archive layout for each named instrument.

**They are omitted because none of them resolved to a SPASE instrument row when this dossier was
compiled (2026-09-12), and a name without an identifier must never be recorded.** The controlled
vocabulary was searched by name, abbreviation and identifier path for each of the above, and every
one returned zero matches. What makes that a real absence rather than a search failure is that the
search instrument was validated in the same command shape: positive controls for `AIA`,
`magnetometer`, `Solar Orbiter` and `telescope` all returned matches, and a nonsense token returned
zero, over a vocabulary in which every instrument and observatory row carried a
`https://spase-metadata.org/` identifier. Re-run those same controls before trusting a future
negative — the vocabulary grows as upstream SPASE records are added, so an absence measured here is
dated rather than permanent.

**One dangerous near-match, explicitly rejected.** Searching for the full name "Electron
Electrostatic Analyzer" returned a row (2026-09-12) — but it is
`https://spase-metadata.org/CNES/Instrument/CDPP-Archive/GIOTTO/RPA1-EESA`, named "RPA1 - EESA
Electron Electrostatic Analyzer of the RPA experiment  aboard Giotto". That is an instrument on the
Giotto comet mission, from a different naming authority, with no relationship whatsoever to HERMES.
Binding HERMES's EEA to it would be a serious factual error. Match on the whole entity — including
its platform — not on an instrument-class name.

**Equally, no identifier may be constructed by analogy.** The observatory-level identifiers below
exist, but it does not follow that, say, `.../SMWG/Instrument/HERMES/EEA` does; it does not. An
identifier counts only when a row for it has actually been resolved.

**The association is recorded at observatory level instead.** Where an instrument has no SPASE
record, the correct action is to associate the software with the instrument's platform rather than
to drop the relationship or invent a value. Both HERMES and PADRE resolve cleanly at observatory
level, and are recorded in Field 32. REACH and IMPAX had no SPASE row at either level as of
2026-09-12 and were therefore genuinely unrepresentable; they are documented here so the omission
reads as a known gap rather than an oversight, and so a future refresh re-checks the vocabulary
rather than re-deriving the question. New instruments enter this vocabulary through its upstream
refresh, never through a submission.

### 32. Related Observatories (OPTIONAL)

**Values — each with its SPASE identifier, which is the reliable key:**

1. **`Heliophysics Environmental and Radiation Measurement Experiment Suite`**
   - SPASE identifier: `https://spase-metadata.org/SMWG/Observatory/HERMES`
   - When this dossier was compiled (2026-09-12) the row's `abbreviation` was `HERMES`. The
     `name` above is copied verbatim from the vocabulary row and must be recorded in that long
     form, not as the abbreviation.

2. **`Solar Polarization and Directivity X-Ray Experiment`**
   - SPASE identifier: `https://spase-metadata.org/SMWG/Observatory/PADRE`
   - When this dossier was compiled (2026-09-12) this row's `abbreviation` field was empty; the
     expansion is the row's `name`. The repository refers to this mission only as `padre`, so
     the binding is via the identifier path segment `PADRE`, confirmed by the row name
     expanding the acronym.

HSSI held no related observatories for this entry before this refresh; these two fill that gap.

**Both matched uniquely — one row each, across the whole vocabulary, searched by name, abbreviation
and identifier.** No same-name collision arose for either, so no naming-authority tie-break was
needed; both happen to be `SMWG` rows. Because each resolved to exactly one row, these are ordinary
Field 32 values and not ambiguous entries requiring manual resolution.

**Why these belong, decided from the perspective of someone using the site.** Imagine a visitor on
HERMES's observatory page clicking "show software related to this observatory". `swxsoc` is the core
library of the HERMES Science Operations Center: it ships HERMES's mission configuration and its
four instrument definitions, enforces the ISTP CDF schema its data products are written to, provides
the client that fetches HERMES data, and even bundles a HERMES sample file
(`swxsoc/data/sample/hermes_nms_default_l1_20160322T123031_v0.0.1.cdf`). Someone working with HERMES
data would be actively glad to find it, and would be surprised by its absence. The same argument
holds for PADRE, whose mission configuration, data levels, instruments and file-naming rules swxsoc
likewise ships, and whose downstream packages are tested against it.

**Considered and rejected: "SWxSOC (Space Weather Science Operation Center)" as an observatory.** An
earlier extraction proposed this as a bare name. It is wrong on two independent counts. A science
operations center is a ground-system organisation, not an observatory — it observes nothing — so it
does not belong in this field conceptually. And no SPASE row existed for it: a search for `swxsoc`
or `space weather science` across the vocabulary returned zero rows (2026-09-12), under the controls
described in Field 31. Recording it as a bare name would have created a new identifier-less row in
the catalogue, which is exactly the defect this field's rules exist to prevent.

**Considered and rejected: REACH and IMPAX.** Both are configured missions in the package and would
otherwise qualify on the same designed-to-support reasoning as HERMES and PADRE. Neither had a SPASE
row as of 2026-09-12 — searches for `REACH`, `Responsive Environmental`, `IMPAX` and
`Imaging Microburst` all returned zero under working controls. An evidenced "no usable identifier"
is the correct outcome here, and is strictly better than recording a bare name. IMPAX is a recent
CubeSat (its configuration sets a minimum valid time of 2026-01-01), so a future vocabulary refresh
may well add it; that is the
route by which it should be revisited.

**Ordering note:** unlike Fields 4, 5, 6 and 22, `relatedObservatories` is not a sortedm2m field, so
the order of the two entries above is presentational rather than stored data.

### 33. Logo (OPTIONAL)
**Value:** `https://raw.githubusercontent.com/swxsoc/swxsoc/fbbc26e70863f8acc4df53dee4876a40b5cca154/docs/logo/swxsoc_logo.png`

Retained unchanged, and verified rather than assumed.

**Fetched and confirmed to be a real image:** the URL returns HTTP 200 with content-type `image/png`
and 77,970 bytes, decoding as a 461 x 546 8-bit RGBA PNG. This check matters because an HTTP 200
alone proves nothing here — a raw GitHub URL for a Git-LFS-tracked file also returns 200, but with
about 130 bytes of `text/plain` pointer that renders as a broken image. The byte count and
content-type rule that out.

**Inspected, not merely fetched.** The image is a shield-shaped badge with the wordmark "SWxSOC" in
blue over a dark ground, above a concentric-ring device. It is unambiguously this project's logo —
a conventional wordmark, not an example plot or a data product — so there is no question to raise
about its suitability.

**The pinned URL is correctly formed and still current.** It is pinned to the 40-hex commit
`fbbc26e70863f8acc4df53dee4876a40b5cca154`, contains no branch name and no `blob/` segment, and is
114 characters, well inside the 200-character field limit. Crucially, the blob it serves is still the
project's present logo: the object hash of `docs/logo/swxsoc_logo.png` is identical
(`f9cce44ddaf6a8b1f4478fe05b884813c5047356`) at both the pinned logo commit and this dossier's source
revision, so the file has not changed in between. The same URL, character for character, is what the
PyHC registry carries in its `logo` field for this project.

**Do not "fix" this to a branch URL.** Replacing the commit SHA with `main` would make the link
mutable, and a future logo redesign would then silently change what HSSI displays. That mutability is
the failure mode the pinning prevents; a redesign should be noticed and recorded deliberately by a
refresh, which the identical-blob check above makes possible.
