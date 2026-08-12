# HSSI Metadata Extraction Results

**HSSI Software ID:** e211347f-4b04-4765-a230-295f366390d1
**Repository:** https://github.com/spacepy/dbprocessing
**Source Revision:** dcaa21b614cf49ed4cdb5b290b4cd7d303fd80bd
**Extraction Date:** 2026-08-12
**Validation Date:** 2026-08-12
**Validation Status:** PASS

---

**Scope note.** `dbprocessing` is deliberately mission-, instrument-, region- and file-format-agnostic
infrastructure: it is a process controller that decides *which* code to run on *which* file and
records the result, while the actual reading, transforming and writing of science data is delegated
to externally supplied "inspectors" and processing codes that are **not part of this repository**
(`docs/README.rst:19-27`, `docs/concepts.rst` "Files": *"dbprocessing itself does not create data
files; that is the responsibility of data processing codes."*). Several fields below therefore turn
on a distinction that must be kept in mind when re-reading the evidence: what `dbprocessing` itself
implements, versus what the pipelines it has controlled happen to do. Where a value rests on the
latter, the note says so explicitly.

The repository is also somewhat unusual in its layout: there is **no `README.md`, `LICENSE`,
`CITATION.cff` or `codemeta.json` at the repository root.** The README, license, copyright,
contributor list and release notes are all reStructuredText files under `docs/`, which are rendered
into the Sphinx site. Automated extractors that look only at the repository root will report these
as missing; they are not missing, only relocated.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Source note.* The original submitter of this record is not identified in HSSI's published metadata
and is not recoverable from the repository. The placeholder is intentional.

---

### 2. Persistent Identifier (RECOMMENDED)

`https://doi.org/10.5281/zenodo.6047133`

*Source note.* This is the Zenodo **concept DOI** — the identifier that resolves to all versions —
which is what this field asks for. It is confirmed from both directions: the Zenodo record for
6047134 reports `conceptdoi: 10.5281/zenodo.6047133` and `conceptrecid: 6047133`, and the DataCite
record for 6047133 carries `relatedIdentifiers: [{relationType: HasVersion, relatedIdentifier:
10.5281/zenodo.6047134}]`. The version-specific DOI belongs in Field 12 (Version PID), not here.
Carried over from the existing HSSI record and independently re-confirmed.

**Considered and not selected: `https://doi.org/10.11578/DC.20210924.1`.** The same software is
*also* registered in DOE CODE (record 63621, released 2021-09-16, authors Walker, Larsen, Yang,
Niehof, LANL), and that registration has its own DOI. It is a genuine, resolvable identifier for
dbprocessing, but it is not the right value for this field: it points at the LANL predecessor
repository `https://github.com/lanl/dbprocessing` rather than the canonical public repository, it
covers no specific version, and the Zenodo concept DOI is the one the project itself mints through
its GitHub–Zenodo integration on every release. It is recorded here so that a future agent meeting
the DOE CODE DOI recognises it as a parallel registration of this same software rather than a
different package, and does not "correct" Field 2 to it. (The predecessor repository itself is
recorded in Field 29.)

---

### 3. Code Repository (MANDATORY)

`https://github.com/spacepy/dbprocessing`

*Source note.* The canonical public repository. Confirmed as the development home by
`docs/README.rst:57-59` (*"Development is performed in the public github repository at
<https://github.com/spacepy/dbprocessing/>"*), by `docs/developer/pull_requests.rst`, and by the
Zenodo record's `related_identifiers` entry
(`https://github.com/spacepy/dbprocessing/tree/release-0.1.0`, relation `isSupplementTo`). Carried
over from the existing HSSI record.

Note that `https://github.com/lanl/dbprocessing` also exists and is named as the repository by the
DOE CODE registration. It is the *predecessor*, not an alternative for this field: it was created
2020-07-14 and last pushed 2020-07-16, bracketing the "creation of the public repository on
2020-07-15" recorded in `docs/release_notes.rst`, and its tags (`ver_1.0.0`, `hope_v1.0.0`,
`comm_ver_1`, `cmmt88272`) belong to the pre-public LANL history. See Field 29.

---

### 4. Software Functionality (MANDATORY)

- Data Processing and Analysis
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Mission-related
- Mission-related: Archive
- Mission-related: Distribution/Access
- Mission-related: Ingest
- Mission-related: Inventory
- Mission-related: Monitoring
- Mission-related: Orchestration
- Mission-related: Processing
- Mission-related: Science Data Processing

*Source note.* The previously stored value was the single top-level category `Data Processing and
Analysis`. That was correct but badly incomplete: it captured none of what actually distinguishes
dbprocessing, which is that it is a **mission ground-system pipeline controller**, not an analysis
library. Each subcategory above is listed alongside its parent, as the taxonomy requires.

Evidence for each selected value:

- **Mission-related: Orchestration** — the core purpose. `dbprocessing/dbprocessing.py`
  (`ProcessQueue`), `dbprocessing/DBqueue.py` and `dbprocessing/runMe.py` decide which processing
  codes can run, build their command lines, and execute them; `scripts/ProcessQueue.py` is the
  operational entry point. `docs/README.rst:14-18`: *"Given a description of relationship between
  data files, a set of codes to process data files to derived products, and input files themselves,
  dbprocessing iteratively runs the appropriate codes to make all possible output files."*
- **Mission-related: Ingest** — `ProcessQueue.py` has an explicit ingest mode
  (`docs/scripts.rst`, "Ingest mode options"); `dbprocessing/DBfile.py` and
  `dbprocessing/Diskfile.py` implement moving a file from the incoming directory into the managed
  store and recording its metadata; `scripts/linkUningested.py` finds files that match a product's
  format but are absent from the database and symlinks them into incoming for ingestion.
  `docs/concepts.rst` has a dedicated ingestion concept section.
- **Mission-related: Processing** and **Mission-related: Science Data Processing** — both are
  retained deliberately rather than collapsed. `Processing` covers the generic execution of a
  dependency-ordered chain of codes; `Science Data Processing` covers the fact that the chain is
  organised around science data *levels* (`docs/concepts.rst`, "Files": *"The 'level' of the data,
  following the convention that level 0 is processed into level 1, level 1 into 2, etc."*), which is
  what makes this a science-data pipeline rather than a general job runner. The functional test
  exercises exactly that L0 → L1 → L2 progression (`functional_test/L0`, `L1`, `L2`).
- **Mission-related: Inventory** — the database is a file/product/code/process inventory, and a
  large fraction of the shipped scripts exist to interrogate it: `scripts/printInfo.py`,
  `scripts/missingFiles.py`, `scripts/missingFilesByProduct.py`, `scripts/dbOnlyFiles.py`,
  `scripts/compareDB.py`, `scripts/printRequired.py`.
- **Mission-related: Monitoring** — `scripts/scrubber.py` and `scripts/possibleProblemDates.py`
  check the database for inconsistencies (the latter with a `--fix` option);
  `scripts/printProcessQueue.py` reports queue state and can signal it through its exit code;
  `dbprocessing/reports.py` parses the processing logs; `examples/scripts/weeklyReport.py` builds a
  weekly status page from them.
- **Mission-related: Archive** — `scripts/fast_data.py` removes superseded file versions and, with
  `-a/--archive`, moves them to an archive directory rather than deleting, while retaining the
  database records with `exists_on_disk` set false; `docs/concepts.rst` "Releases" describes
  first-class support for named public releases of data (`release` table,
  `DButils.addRelease`), and files in a release are protected from removal.
- **Mission-related: Distribution/Access** — `scripts/makeLatestSymlinks.py` builds a separate
  directory populated with symlinks to only the newest version of each product/date, which is the
  standard way these deployments expose data to users; `scripts/htmlCoverage.py` and
  `examples/scripts/writeDBhtml.py` publish browsable coverage/status pages.
- **Data Processing and Analysis** and **Data Processing and Analysis: Processing** — retained from
  the existing record and given its subcategory. dbprocessing describes itself as a "process
  controller which automates the production of derived data products"; the pipeline-step sense of
  `Processing` is exactly what it provides.
- **Data Visualization** and **Data Visualization: 2D Graphics** — two of the installed scripts
  generate figures. `scripts/coveragePlot.py` builds a 2-D product × date coverage image
  (`ax.imshow(...)` at line 254 with a `LinearSegmentedColormap`, `plt.savefig` at line 284, and a
  ghostscript step that concatenates the per-page images into a PDF);
  `scripts/histogramCodes.py` plots per-code execution-time histograms (`ax.hist` , `fig.savefig`
  at line 65). `setup.py` installs everything matching `scripts/*.py`, so both are user-facing
  commands, and both are documented under "Maintained scripts" in `docs/scripts.rst`.

Considered and rejected, with reasons — recorded so a later refresh does not re-propose them:

- **Data Processing and Analysis: Data Access and Retrieval** — rejected. The category as defined
  covers downloading or querying data from *remote archives* (Fido/astroquery/HAPI-style clients).
  dbprocessing has no such client: it indexes and locates files in a locally managed store, and
  every input arrives by being placed in an incoming directory. The package's two `urllib`
  references are not retrieval: `dbprocessing/Utils.py:119-138` is a docstring for a progress-bar
  helper copied from SpacePy, and `dbprocessing/DButils.py:27-30,115` uses `urllib.parse.quote_plus`
  only to URL-escape credentials inside a database connection string.
- **Data Processing and Analysis: Analysis**, **Time Series Analysis**, **Data Reduction**,
  **File Format Conversion**, **Calibration**, **Packet Decommutation** — all rejected for the same
  underlying reason: dbprocessing performs none of these itself, it *schedules codes that do*.
  `docs/concepts.rst` states plainly that dbprocessing does not create data files. `fast_data.py`
  superficially resembles Data Reduction but it deletes superseded file versions to reclaim disk;
  it does not average, bin or downsample data. Telemetry products such as
  `ect_{SPACECRAFT}_{nnnn}_{APID}_{nn}.ptp.gz` in `ConfigTest.txt` are *inputs to* externally
  supplied decommutation codes.
- **Mission-related: Operations** — rejected. dbprocessing is data-system operations software, but
  this category reads as spacecraft/mission operations (planning, commanding), which dbprocessing
  does not touch.
- **Mission-related: System Testing** — rejected. `functional_test/` tests dbprocessing itself
  (using a synthetic rot13 "mission"), not a flight or ground system.
- **Mission-related: Infrastructure as Code** and **Servers and Environments: Infrastructure as
  Code** — rejected, though arguable. A processing chain *is* declared in a configuration file and
  instantiated by `scripts/addFromConfig.py`, with `scripts/configFromDB.py` writing it back out.
  But the category is understood as provisioning compute infrastructure (Terraform/Ansible/
  Kubernetes), and selecting it would mislead a user filtering for deployment automation.
- **Servers and Environments** and its children — rejected. dbprocessing exposes no server or
  service endpoint; it is a set of command-line programs plus a library.
  `dbprocessing/module.py` is a thin wrapper around the Environment Modules `modulecmd` tool "as
  used on the LANL scheme", which is environment *configuration*, not a container, and it is not
  wired into `runMe`/`ProcessQueue` at this revision.
- **Data Visualization: Web-Based** — rejected. `scripts/htmlCoverage.py` emits a static HTML
  table (plain `output.write('<tr>…')` calls); there is no interactivity, no web framework and no
  browser-side visualisation library.
- **Coordinate Transforms** and **Models and Simulations**, with all their children — rejected;
  nothing in the package performs coordinate conversion or physical modelling.

---

### 5. Related Region (MANDATORY)

- Earth Magnetosphere
- Earth Inner Magnetosphere
- Interplanetary Space

*Source note.* dbprocessing has no region-specific physics of its own, so this field can only
reflect the regions whose data it has been built and used to produce. Two production deployments are
documented by the project and by its PI:

- **Earth Magnetosphere / Earth Inner Magnetosphere** — dbprocessing was written for and controlled
  the production of all Van Allen Probes RBSP-ECT data (`docs/CONTRIBUTORS.rst` Acknowledgements;
  NASA proposal 20-HDEE20_2-0017, ADS `2020hdee.prop...17N`: *"dbprocessing controlled the
  processing of all data from the RBSP-ECT suite, used in hundreds of peer-reviewed science
  publications studying the radiation belts"*). The Van Allen Probes orbit and the ECT science
  target are the inner magnetosphere and the radiation belts, so the more specific
  `Earth Inner Magnetosphere` is added alongside the broader region that was already stored, in line
  with the guidance to prefer the most specific applicable region.
- **Interplanetary Space** — the same proposal records that data processed the same way for Parker
  Solar Probe / IS☉IS *"resulted in over a dozen peer-reviewed publications investigating energetic
  particle dynamics in the inner heliosphere"*, and `docs/ConfigurationFiles.rst:490-502` and
  `scripts/makeLatestSymlinks.py:273-285` carry a worked `[isois]` configuration operating on
  `psp_isois_l1-*.cdf` files. Retained from the existing record and now evidenced.

**`Planetary Magnetospheres` was previously stored in HSSI and has been removed.** No supporting
evidence for it was found in any source consulted: the repository, the Sphinx documentation under
`docs/`, the Zenodo and DataCite records, the PyHC community registry entry, and the NASA proposal
abstract are all silent on any non-Earth planetary application. The deployments that *are* documented
are Earth-orbiting (RBSP-ECT, and the LANL satellites named in the proposal) or heliospheric
(PSP/IS☉IS). Because the vocabulary offers `Earth Magnetosphere` as its own separate value,
`Planetary Magnetospheres` reads specifically as a claim about non-Earth planets, and nothing
supports that claim.

This should not be re-proposed on the strength of the software's generality. dbprocessing is
deliberately region-agnostic infrastructure (see the scope note at the top of this file), which is a
reason for its region list to stay confined to the deployments that are actually documented, not a
licence to broaden it to regions where it merely *could* be used. Restoring the value would need a
documented non-Earth planetary deployment — a configuration, a publication, or a maintainer statement
naming such a mission.

Considered and not selected: `Solar Wind`. PSP/IS☉IS observes energetic particles in the inner
heliosphere, which `Interplanetary Space` already covers; nothing indicates dbprocessing-managed
pipelines are specifically solar-wind plasma products. Also considered and not selected:
`Earth Ionosphere` / `Earth Thermosphere`, which the PyHC registry's
`ionosphere_thermosphere_mesosphere` keyword might suggest. That keyword sits alongside `general` in
a four-item PyHC tag list that reads as broad domain tagging for a general-purpose tool; no
ionospheric or thermospheric deployment appears in the repository or the publications, so the tag
alone is too thin to carry a region claim.

---

### 6. Authors (MANDATORY)

Union of the existing HSSI author list, the Zenodo/DataCite creator list, and the project's own
contributor roll in `docs/CONTRIBUTORS.rst`. No previously recorded author was dropped.

| # | Name | Identifier | Affiliation |
|---|---|---|---|
| 1 | Lorna Ellis | *none found* | *none found* |
| 2 | Ken Fairchild | *none found* | *none found* |
| 3 | Reinhard Friedel | https://orcid.org/0000-0002-5228-0281 | Los Alamos National Laboratory (https://ror.org/01e41cf67) |
| 4 | Myles Johnson | *none found* | *none found* |
| 5 | Brian Larsen | https://orcid.org/0000-0003-4515-0208 | Los Alamos National Laboratory (https://ror.org/01e41cf67) |
| 6 | Nathan Masi | *none found* | *none found* |
| 7 | Steven K. Morley | https://orcid.org/0000-0001-8520-0199 | Los Alamos National Laboratory (https://ror.org/01e41cf67) |
| 8 | Denis Nadeau | *none found* | Los Alamos National Laboratory (https://ror.org/01e41cf67) |
| 9 | Jonathan T. Niehof | https://orcid.org/0000-0001-6286-5809 | University of New Hampshire (https://ror.org/01rmh9n78) |
| 10 | Evin O'Shea | *none found* | *none found* |
| 11 | Anthony Rogers | https://orcid.org/0000-0002-6127-449X | *none found* |
| 12 | Elizabeth Vandegriff | *none found* | *none found* |
| 13 | Andrew Walker | https://orcid.org/0000-0002-7890-1779 | Los Alamos National Laboratory (https://ror.org/01e41cf67) |
| 14 | Meilin Yan | *none found* | *none found* |
| 15 | Xiaoguang Yang | *none found* | Los Alamos National Laboratory (https://ror.org/01e41cf67) |

*Source note.* Nine of these (Fairchild, Friedel, Johnson, Larsen, Masi, Nadeau, Niehof, O'Shea,
Rogers) were already in HSSI, matching the Zenodo `creators` list for record 6047134 exactly —
Zenodo's GitHub integration captured whoever had commit credit at the 0.1.0 release. Six more come
from `docs/CONTRIBUTORS.rst`, which is the project's own authoritative credit list and names both
past contributors and current developers: Lorna Ellis, Elizabeth Vandegriff, Steven Morley, Andrew
Walker, Meilin Yan and Xiaoguang Yang. Those six supplement the Zenodo-derived nine rather than
displacing any of them.

Name reconciliation across sources:

- `docs/CONTRIBUTORS.rst` writes **"Reiner Friedel"**, while Zenodo, DataCite and HSSI all use
  **"Reinhard Friedel"**. These are the same person (Reiner is the familiar short form of Reinhard);
  ORCID 0000-0002-5228-0281 is the LANL record. The longer form is kept because it matches the
  ORCID-bearing DOI metadata and the value already stored.
- `docs/CONTRIBUTORS.rst` writes **"Tony Rogers"**; Zenodo and HSSI use **"Anthony Rogers"**
  (ORCID 0000-0002-6127-449X). The formal form is kept for the same reason.

Identifier evidence for the newly added authors:

- **Steven K. Morley** already exists as a person record in HSSI with ORCID
  `https://orcid.org/0000-0001-8520-0199` and a Los Alamos National Laboratory affiliation; the
  public ORCID record for that iD lists Los Alamos National Laboratory among its employments, and
  `docs/CONTRIBUTORS.rst` lists Morley as a current dbprocessing project administrator. The
  identity is not in doubt; note that a *different* Steven Morley (ORCID 0000-0002-7355-3349,
  University of Edinburgh) exists and must not be used.
- **Andrew Walker** → `https://orcid.org/0000-0002-7890-1779`. "Andrew Walker" is a very common
  name — an ORCID search returns dozens of candidates — so this was resolved on converging
  evidence rather than name match: that iD's only employment is *Los Alamos National Laboratory,
  Staff Scientist, ISR-3: Space Data Science & Systems* — the LANL division whose satellite data
  processing dbprocessing runs — and the DOE CODE registration of dbprocessing (record 63621) lists
  "Walker, Andrew" alongside Larsen, Yang and Niehof as LANL authors. Among the candidates reviewed,
  no other iD showed any space-science or LANL association. If this attribution is ever disputed,
  the LANL division affiliation is the discriminator to re-check.
- **Xiaoguang Yang** — LANL affiliation recorded, from the DOE CODE registration, which lists Yang
  as a LANL author of dbprocessing, corroborated by `docs/CONTRIBUTORS.rst` listing Yang as a
  current developer. No ORCID is recorded: an ORCID search for "Xiaoguang Yang" returns dozens of
  iDs and none of those reviewed showed any LANL or space-physics association, so assigning one
  would be a guess.
- **Lorna Ellis**, **Elizabeth Vandegriff**, **Meilin Yan**, **Ken Fairchild**, **Myles Johnson**,
  **Nathan Masi**, **Evin O'Shea**, **Denis Nadeau** — no identifier recorded. ORCID searches
  returned either nothing or only clearly unrelated people (the "Meilin Yan" candidates that
  surfaced were an air-quality researcher and a Hanyang University record; the Vandegriff already
  known to HSSI is Jon Vandegriff of JHU/APL, a different person). Nadeau's LANL affiliation comes
  from the existing HSSI record and is corroborated by the Zenodo creator entry
  `{"name": "Denis Nadeau", "affiliation": "Los Alamos National Laboratory"}`.

**Considered and not credited: Ryan Douglas.** The git history contains a commit authored by
`Ryan Douglas <rdouglas@isoc1.sr.unh.edu>`, `3909651f` (2019-05-27), *"updated insepctor.py so that
every inspector has filenameformat and filenameregex properties"*. It is a genuine ancestor of the
pinned revision, and it touches core package code rather than docs or tests — four added lines in
`dbprocessing/inspector.py` plus one removed line in `scripts/testInspector.py`. It is the only
commit by that author or that address across the refs in this clone.

Douglas is nonetheless credited by none of the three sources the project itself curates:
`docs/CONTRIBUTORS.rst`, whose opening line is *"The following individuals have contributed code to
``dbprocessing``"* and which lists both former contributors and current developers; the Zenodo
`creators` list for record 6047134; and the DOE CODE registration (record 63621). The name does not
occur anywhere in the working tree at the pinned revision.

The decision recorded here is not to add them. `CONTRIBUTORS.rst` continued to be maintained well
after the 2019 commit — it credits people who joined the project later — so its continued omission of
Douglas is more plausibly a deliberate curation decision by the maintainers than an oversight this
record should silently overturn, and HSSI authorship should follow the project's own statement of
credit rather than raw commit authorship. What would change the answer in a later refresh: an
updated `CONTRIBUTORS.rst`, a Zenodo or DOE CODE creator list naming Douglas, or a direct maintainer
statement. Absent one of those, the commit alone is not sufficient corroboration and this should not
be re-proposed.

**Durable upstream limitation.** The stored person records for Fairchild, Johnson, Masi, Nadeau and
O'Shea carry an empty `identifier`. That is correct — no identifier is known — but it is worth
knowing that HSSI's authors field is validated as a whole, so an unrelated edit to this software's
author list can be rejected because of a blank field on a *shared* person row. Person and
organization rows are shared across software records, so any correction to a name on one of these
rows would affect every other record referencing it and should not be attempted as part of a routine
metadata update without first checking what else references it.

---

### 7. Software Name (MANDATORY)

`dbprocessing`

*Source note.* The stored value was `spacepy/dbprocessing`. That is the GitHub **owner/repository
locator**, not the software's name, and it is replaced here. The name `dbprocessing` — all
lower-case, one word — is what the sources the project itself controls use, consistently:

- `setup.py:57` — `'name': 'dbprocessing'` (this is the distribution name, and the built artifacts
  are `dbprocessing-0.1.0-py2.py3-none-any.whl` and `dbprocessing-0.1.0.zip`).
- **PyPI** — the project is published at `https://pypi.org/project/dbprocessing/` with
  `"name": "dbprocessing"`.
- `docs/conf.py:95` — `project = u'dbprocessing'`; `docs/conf.py:170` composes the manual title from
  it, and the published documentation page title reads *"dbprocessing documentation — dbprocessing
  v0.1.0 manual"*.
- `docs/index.rst` — the document title is "dbprocessing documentation", and the body writes the
  name in lower-case literal formatting: ``` ``dbprocessing`` automates the routine data processing
  needs… ```. `docs/README.rst` does the same throughout.
- **PyHC community registry** (`_data/projects.yml`) — a curated, human-maintained entry with
  `name: dbprocessing`.
- **GitHub** — the repository `name` field is `dbprocessing`; `spacepy/dbprocessing` is its
  `full_name`. SoMEF, reading the same API, likewise reports `name: dbprocessing` and
  `full_name: spacepy/dbprocessing` as two different things.
- **DOE CODE** record 63621 — title `dbprocessing`.

**Why `spacepy/dbprocessing` is wrong, specifically.** It reaches HSSI through the DOI autofill
path: Zenodo's GitHub integration generates release titles mechanically as
`<owner>/<repo>: <release name>`, which is why the Zenodo and DataCite title for this software is
literally `spacepy/dbprocessing: 0.1.0`. The `spacepy/` prefix carries no naming intent — it is the
hosting organisation. Worse, keeping it actively misinforms, because the project takes pains to deny
exactly that relationship: `docs/README.rst:44-52` has a section headed "Relationship to SpacePy"
which states *"dbprocessing is not a component of SpacePy, nor does it require SpacePy"*, explaining
that the SpacePy organisation merely hosts the repository and provides community support while
dbprocessing grows its own community. A name of `spacepy/dbprocessing` presents it as a SpacePy
subpackage, which its authors explicitly reject.

Other alternatives considered and rejected: a longer formal name or expansion — the project uses
none, and the nearest candidate, `setup.py:51`'s `'description': 'database-driven Heliophysics
processing controller'`, is a description that the project uses *about* the software, never as its
name. Alternative stylings `DBprocessing`, `DbProcessing`, `DBProcessing` — no project-authored
source uses any of them; the lower-case form is used consistently in the package name, the module
name, the Sphinx project, the release notes and the PyHC entry.

---

### 8. Description (MANDATORY)

```
dbprocessing is a Python-based, database-driven process controller which automates the production of derived data products upon the arrival of new input data. Although originally written for Heliophysics data, it is intended to be flexible enough to manage most forms of digital time-series data.
Documentation is available at <https://spacepy.github.io/dbprocessing/>.
```

*Source note.* Carried over from the existing HSSI record and confirmed to be the
project's own wording: it is the opening paragraph of `docs/README.rst:1-9`, including the closing
documentation sentence. This is maintainer-authored prose describing the software accurately, so it
is preserved as written rather than re-phrased. It also states the scope caveat that matters most
for interpreting the rest of this record — the tool is domain-agnostic by design and was merely
*originally* written for heliophysics.

---

### 9. Concise Description (OPTIONAL)

`Automated processing controller for heliophysics data`

*Source note.* Carried over from the existing HSSI record. It matches the GitHub repository's own
`description` field verbatim, is 53 characters (well within the 200-character limit), and is an
accurate one-line preview. No reason to alter maintainer-set text.

---

### 10. Publication Date (RECOMMENDED)

`2022-02-10`

*Source note.* Carried over from the existing HSSI record and independently corroborated four
ways: Zenodo record 6047134 reports `publication_date: 2022-02-10`; the DataCite record for the
concept DOI carries `dates: [{date: "2022-02-10", dateType: "Issued"}]`; the GitHub release
`release-0.1.0` was published 2022-02-10T23:48:53Z; and the PyPI artifacts for 0.1.0 were uploaded 2022-02-10T22:52:48.
See Field 12 for why the *Zenodo record creation* timestamp of 2022-02-11 is not the release date.

---

### 11. Publisher (RECOMMENDED)

- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Source note.* Carried over from the existing HSSI record. Correct per the field's own guidance:
the DOI was obtained through the GitHub–Zenodo workflow, and DataCite reports
`publisher: "Zenodo"` for this DOI.

---

### 12. Version (RECOMMENDED)

- **Version Number:** `0.1.0`
- **Version Date:** `2022-02-10`
- **Version PID:** `https://doi.org/10.5281/zenodo.6047134`
- **Version Description:**
  ```
  First public packaged release of dbprocessing. Adds Python 3 support; initial PostgreSQL support; support for processes that take no input, with related DBRunner enhancements; a new linkUningested script that finds files matching a product format but absent from the database and symlinks them into the incoming directory for ingestion; and new printProcessQueue options (--count, --exist, --quiet, --product, --sort). Fixes ProcessQueue.buildChildren on older databases lacking the yesterday/tomorrow columns, corrects runMe's handling of the output interface version so that quality versions increment appropriately, and restricts input selection to files recorded in the database as existing on disk. SQLAlchemy and dateutil are required.
  ```

*Source note — the version number.* HSSI stored `release-0.1.0`. That is the **git tag string**, not
the release identifier, and it is corrected to `0.1.0` here. The project's own release procedure
draws exactly this distinction, in `docs/developer/release.rst:231-236`: *"Make the tag
'release-x.y.z' … Use just 'x.y.z' as the title."* Every version-bearing artifact follows that
rule — `setup.py` at tag `release-0.1.0` reads `'version': '0.1.0'`; `dbprocessing/__init__.py` at
the same commit reads `__version__ = '0.1.0'`; the GitHub release object has `tag_name:
"release-0.1.0"` but `name: "0.1.0"`; `docs/release_notes.rst` heads the section `0.1.0
(2022-02-10)`; PyPI publishes version `0.1.0`; and the published documentation renders
"dbprocessing v0.1.0 manual".

The stored `release-0.1.0` came in through DOI autofill: Zenodo's GitHub integration fills its
`version` field from the git tag name, so both the Zenodo record and DataCite report
`version: "release-0.1.0"`. That is Zenodo transcribing a tag, not the project naming a release.

*Source note — the version date.* HSSI stored `2022-02-11`; it is corrected to `2022-02-10`. The
2022-02-11 value is the **Zenodo record's own creation timestamp** (`created:
2022-02-11T16:40:23Z`, `registered: 2022-02-11T16:40:28Z`) — when Zenodo archived the release, a day
after the release itself. The release date is 2022-02-10 on the evidence listed under Field 10, plus
the release-notes heading and the tagged commit's own date (`3ae1d597`, authored 2022-02-10).
Zenodo's *own* `publication_date` field agrees at 2022-02-10; only its record-creation metadata
carries the 11th.

*Source note — the version PID.* `https://doi.org/10.5281/zenodo.6047134` is the version-specific
DOI: Zenodo record 6047134 is the 0.1.0 deposit, and its `conceptdoi` is 10.5281/zenodo.6047133,
which is the value in Field 2. Keeping the two straight matters — the concept DOI resolves to
"all versions" and would be wrong here, while the version DOI would be wrong in Field 2.

**`0.1.1rc0` is not a release and must never be recorded as one.** The default branch carries
`'version': '0.1.1rc0'` (`setup.py:64`) and `__version__ = '0.1.1rc0'`
(`dbprocessing/__init__.py:34`). This is a deliberate unreleased-development marker, not a newer
release: `docs/developer/release.rst:111-114` instructs that after the release commit the developer
should *"make a second commit setting all the versions to the next version number and `rc0`"*, and
commit `5acdfa8d` — titled "Mark as unreleased/pre-0.1.1" — is precisely that commit, applied
immediately after the 0.1.0 release commit. There is no 0.1.1 release: at this revision
`release-0.1.0` is the repository's sole tag, and 0.1.0 was the only release listed on GitHub and
the only version published on PyPI when this record was compiled.

*Version description provenance.* Condensed from `docs/release_notes.rst` (section "0.1.0
(2022-02-10)"), which is also the text Zenodo carries in its record description. The text above is a
summary; `docs/release_notes.rst` remains the fuller upstream source.

**Durable limitation of this field.** HSSI keeps a software's version in a record of its own, so
changing the version number creates a new version record and leaves the previous one orphaned rather
than editing it in place, and the version description is carried on that record rather than derived
from the release notes — it has to be re-supplied whenever the version changes. That is accepted
behaviour for this catalogue, not a defect to clean up. It is recorded here because it has a
practical consequence for the next refresh: a move to a later release must bring a freshly condensed
description from `docs/release_notes.rst` with it, since the summary above will not follow the new
version number by itself.

---

### 13. Programming Language (RECOMMENDED)

- Python 3.x
- Python 2.x

*Source note.* `Typescript` was previously stored and is **incorrect**; it is removed. There is no
TypeScript in this repository under any measure:

- A census of tracked files by extension gives 109 `.py`, 27 `.rst`, 12 `.conf`, 8 `.raw`, 7 `.txt`,
  5 `.rot`, 5 `.md`, 5 `.cat`, 3 `.tgz`, 2 `.yml`, 2 `.json`, 1 `.ui`, 1 `.js`, 1 `.html`, 1 `.dot`,
  1 `.css`, 1 `.in`, 1 `.pylintrc`, 1 `.gitignore`, plus `sphinx/Makefile` and one sentinel file.
  There is no `.ts` or `.tsx` file.
- GitHub's own language statistics report Python (718,821 bytes) and Makefile (7,753 bytes) and
  nothing else; SoMEF, reading the same API, reports the same two.
- The single `.js` file is `docs/_static/copybutton.js`, a Sphinx documentation UI helper, and the
  single `.html` file is `docs/_templates/layout.html`, a Sphinx template. Neither is TypeScript,
  and neither is part of the software.

The most likely origin of the stored value is the `gui/` directory, which a superficial pass might
take for a web front end. It is not: `gui/dbProcessingGUI.py` is a **PySide (Qt) desktop
application** (`from PySide import QtCore, QtGui`, line 7) and `gui/MainUI.ui` is a Qt Designer XML
layout (`<?xml version="1.0"?><ui version="4.0">`) intended to be compiled to Python with
`pyside-uic`, as its own first line documents.

`Python 3.x` is retained. `Python 2.x` is **added** because release 0.1.0 genuinely supports both:
`setup.py` declares `'requires': ['python (>=2.7, !=3.0)', …]`; `docs/getting_started.rst:15` states
*"Python is required, either 2.7 or 3.2+"*; the CircleCI configuration runs the unit-test suite
under both `circleci/python:2.7` and `circleci/python:3.7` (jobs `unittest` and `unittest3`); and the
codebase carries `from __future__ import` headers and explicit Python 2 fallbacks throughout (e.g.
`try: import configparser / except ImportError: import ConfigParser as configparser` in
`scripts/configFromDB.py` and `scripts/coveragePlot.py`). Python 3 support was itself a headline
feature of this release (`docs/release_notes.rst`, PR 77).

Considered and rejected: **`SQL`**. The database schema and effectively all queries are expressed
through SQLAlchemy in Python (`dbprocessing/tables.py`, `dbprocessing/DButils.py`), and SQLite and
PostgreSQL are supported back-ends rather than implementation languages. The repository contains a
single hand-written SQL statement, in `scripts/scrubber.py:27`; the extensive SQL documentation in
`docs/developer/tables.rst` is produced by a custom Sphinx domain (`docs/_ext/sql.py`) documenting
the ORM-declared schema. That does not make SQL one of the languages "most important for the
software". Also rejected: `Javascript` (one vendored Sphinx UI helper) and `Other` (nothing left to
cover).

---

### 14. Reference Publication (RECOMMENDED)

Not found.

*Source note.* No paper describes dbprocessing. This is a negative result reached by searching
rather than an omission: full-text and title searches of ADS/SciX for `dbprocessing` return only
three records, of which one is an unrelated 2003 CDMA-networks paper and the other two are (a) the
DOE CODE software registration and (b) the NASA proposal abstract — neither of which is a
publication describing the software in the sense this field means. There is no JOSS paper, no
`CITATION.cff`, and no "how to cite" section in `docs/`; the project directs users to cite nothing
in particular and simply publishes releases to Zenodo. Searches for citations to the Zenodo DOI
returned nothing in ADS, and Semantic Scholar has no record for it.

If a descriptive paper is ever published, it belongs here. Until then the Zenodo concept DOI in
Field 2 is the citation.

---

### 15. License (RECOMMENDED)

- **License:** `BSD 3-Clause "New" or "Revised" License`
- **License URI:** `https://spdx.org/licenses/BSD-3-Clause.html`

*Source note.* Carried over from the existing HSSI record and confirmed. `docs/LICENSE.rst`
contains the full, unmodified three-clause BSD text and states *"This program is open source under the BSD-3
License."*; `setup.py:53` declares `'license': 'BSD'` with the classifier
`License :: OSI Approved :: BSD License`; Zenodo records `license: {"id": "bsd-3-clause"}`; and
DataCite gives `rightsIdentifier: bsd-3-clause` with `rights: BSD 3-Clause "New" or "Revised"
License`. The stored value is the canonical row in the live `License` vocabulary, not one of the
legacy duplicate rows.

Worth knowing for any automated re-check: the GitHub API reports `license: null` for this repository
because there is no `LICENSE` file at the repository root — the license lives at `docs/LICENSE.rst`
and is rendered into the documentation site. The absence of a root license file is a packaging
detail, not a licensing ambiguity.

`docs/COPYRIGHT.rst` adds a second, non-conflicting copyright layer: "Copyright 2014-2021,
dbprocessing contributors" together with "Copyright 2019, Triad National Security, LLC" and the
standard LANL government-purpose rights statement for work produced under contract
89233218CNA000001. That is a copyright/government-rights notice, not a different licence, and it
does not change the BSD-3 grant.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- data management
- data processing
- database
- heliophysics
- metadata
- parker solar probe
- provenance
- python
- van allen probes

*Source note.* Previously empty. `setup.py:52` declares `'keywords': ['Heliophysics',
'data.processing']`, which map to the existing lower-case rows `heliophysics` and `data processing`
(HSSI stores keywords lower-case and renders them title-cased, so the comparison is on the
normalised form). The rest are drawn from what the software demonstrably is: it maintains a
**database** of file **metadata** (`docs/concepts.rst`: *"Data are stored entirely in files; the
database contains metadata only"*), which is **data management**; it is written in **python**; and
the missions whose data it has produced are the **van allen probes** and **parker solar probe**,
both of which already exist as keyword rows and align with Fields 31/32.

`provenance` is the one keyword here that the vocabulary did not already carry; Keywords is an open
vocabulary, so recording it mints a new row. Minting it is warranted: provenance tracking is a
first-class dbprocessing concept, not an incidental one — the `file` table carries a
`verbose_provenance` column recording the exact command line that produced each file, `examples/scripts/addVerboseProvenance.py` exists solely to copy that provenance
into the output files' own metadata, and the NASA proposal abstract names provenance tracking as one
of the two things the codebase does (*"manages complex dependencies from inputs to high-level
products and tracks provenance"*).

Considered and not selected: `data pipeline` and `workflow` (neither exists as a row, and
`data processing` plus `data management` already cover the concept without minting near-duplicates);
`sql` (does not exist as a row, and see Field 13 on why SQL is not a headline property);
`radiation belts` and `operations` (both exist, but attach to the science done with the *output* of
dbprocessing-managed pipelines rather than to dbprocessing itself); `telemetry` (exists, but the
only telemetry in the repository is an example product format in `ConfigTest.txt`).

---

### 17. Data Sources (OPTIONAL)

- Observatory/Mission-specific
- Other

*Source note.* Previously empty. Neither value is a perfect fit and both are recorded deliberately:

- **Other** — dbprocessing's actual data input mechanism is a **local filesystem incoming
  directory**: files are placed there by whatever external means the project uses, and
  `ProcessQueue.py --ingest` picks them up. There is no client for any remote archive in the
  package — no HAPI, CDAWeb, SSCWeb, VSO or S3 access, and no HTTP/FTP retrieval code at all. The
  two `urllib` references in the package are unrelated to fetching data: a progress-bar helper
  docstring copied from SpacePy (`dbprocessing/Utils.py:119-138`) and `urllib.parse.quote_plus`
  used to URL-escape credentials in a database connection string (`dbprocessing/DButils.py:115`).
  The vocabulary lists `FTP/FTPS Directories` and `HTTP/HTTPS Directories`, so directory-shaped
  sources are in scope, but there is no row for a local or mounted filesystem directory; the field's
  own instruction is to select `Other` when a source is not listed.
- **Observatory/Mission-specific** — selected as the cross-listing that Field 17's guidance requires
  whenever a mission is named in Field 32. In its documented deployments the incoming directory is
  fed by a specific mission's data flow (RBSP-ECT, PSP/IS☉IS), which is what makes the source
  mission-specific rather than a general archive.

Considered and rejected: `CDAWeb`, `HAPI`, `SSCWeb`, `OMNIWeb`, `The Virtual Solar Observatory.`,
`AMDA`, `das2`, `Madrigal`, `VirES`, `GFZ`, `WDC`, `TAP`, `S3/Cloud-aware` — dbprocessing implements
no client for any of them. `FTP/FTPS Directories` and `HTTP/HTTPS Directories` were rejected for the
same reason: the package never opens a network connection to fetch data.

---

### 18. Input File Formats (RECOMMENDED)

- ascii
- CDF

*Source note.* Previously empty. This field needs the scope caveat at the top of this file to be
read correctly. dbprocessing does not itself parse the contents of the science files it manages: it
identifies a file by matching its **name** against a product's format string
(`dbprocessing/DBstrings.py`, `dbprocessing/inspector.py`) and takes a SHA-1 digest of its bytes
(`dbprocessing/Diskfile.py:159-171`). Content-level metadata extraction is delegated to inspectors,
which are user-supplied Python modules — `docs/README.rst:24-26`: *"Support for a file format
requires about 30 lines of Python to identify the product and extract required metadata."* In that
sense dbprocessing supports *every* format and none.

The two values recorded are the formats the project itself demonstrably handles:

- **ascii** — dbprocessing reads INI-style plain-text configuration files as the primary way a
  processing chain is defined (`scripts/addFromConfig.py`, documented at length in
  `docs/ConfigurationFiles.rst`, with `ConfigTest.txt` as the worked example);
  `dbprocessing/reports.py` and `examples/scripts/weeklyReport.py` parse the plain-text processing
  logs; and the end-to-end functional test ingests plain ASCII data files
  (`functional_test/L0/*.raw`, `L1/*.cat`, `L2/*.rot` — all verified to be ASCII text).
- **CDF** — the only science data format the project ships working code for at this revision. The single
  worked inspector in `docs/developer/inspector_examples.rst` opens a CDF with
  `spacepy.pycdf.CDF` and derives the product's start/stop times from its `CDF_EPOCH` variables
  (lines 14, 29, 39-40); `examples/scripts/addVerboseProvenance.py:7` opens CDFs to write
  provenance into their global attributes; `scripts/printInfo.py:15` imports `spacepy.pycdf`; and
  the CDF-named products in `ConfigTest.txt`, `docs/concepts.rst:119` and
  `docs/ConfigurationFiles.rst` are the formats these deployments actually ingest.

Considered and rejected: `netCDF3/4`, `HDF5`, `FITS`, `IDL.sav`, `Zarr`, `csv`, `JSON`,
`ISTP-Compliant` — none appears in any inspector, script or documented example. (`.json` files
exist in the repository, but they are unit-test database dumps under `unit_tests/data/db_dumps/`,
i.e. test fixtures, not an ingestible data format.) `Other` was rejected as adding nothing beyond
the two values above.

---

### 19. Output File Formats (RECOMMENDED)

- ascii
- Other

*Source note.* Previously empty, and constrained by the same scope caveat: **dbprocessing does not
write science data files.** `docs/concepts.rst` states it outright — *"dbprocessing itself does not
create data files; that is the responsibility of data processing codes."* What it *does* write is
operational output, and those are the formats recorded:

- **ascii** — `scripts/configFromDB.py` writes a complete INI-style configuration file
  reconstructed from a database (round-tripping `addFromConfig.py`); `dbprocessing/DBlogging.py`
  writes daily rotating plain-text logs; `scripts/printProcessQueue.py --output` writes the queue as
  text; `dbprocessing/runMe.py:267-271` writes plain-text failure records for problem commands.
- **Other** — the graphical and web outputs, none of which has a vocabulary row. `scripts/
  htmlCoverage.py` and `examples/scripts/writeDBhtml.py` write HTML coverage tables;
  `scripts/coveragePlot.py` writes per-page raster images and then concatenates them into a **PDF**
  via ghostscript; `scripts/histogramCodes.py` writes **PNG** histograms.

Considered and rejected: `CDF`. `examples/scripts/addVerboseProvenance.py` can write a CDF — but
only by annotating an existing CDF produced by an external code with provenance global attributes,
either in place or to a copy. That is metadata annotation of someone else's output, not dbprocessing
generating a CDF, and it lives in `examples/`, which the project itself flags as
*"miscellaneous bits for sharing between developers … may be out-of-date"* (`examples/README.txt`).
Also rejected: `csv`, `JSON`, `netCDF3/4`, `HDF5`, `FITS`, `IDL.sav`, `Zarr`, `ISTP-Compliant` —
nothing in the package writes any of them.

---

### 20. Operating System (RECOMMENDED)

- Linux

*Source note.* Previously empty. This is the project's own claim, stated as an installation
requirement: `docs/getting_started.rst:13` — *"Currently dbprocessing runs on Linux systems (Mac and
Windows are in testing.)"* It is consistent with `setup.py:59` `'platforms': ['Linux', 'Unix']` and
the classifiers `Operating System :: POSIX` and `Operating System :: POSIX :: Linux`
(`setup.py:43-44`); the PyPI record shows `"platform": "Linux"`. CI runs on Linux only (CircleCI
`circleci/python:2.7` and `circleci/python:3.7` Docker images).

Considered and rejected: **`Windows`** and **`Mac`**. There is real evidence of movement toward
both — `docs/release_notes.rst` records PR 119 "Get unit tests working on Windows" as part of this
release, and `unit_tests/dbp_testing.py:68` branches on `sys.platform == 'win32'` — but the project's
own installation documentation at the pinned revision still says they are *in testing*, not
supported. Recording them would overstate what the maintainers claim. If a later release changes
that sentence in `getting_started.rst`, this is the field to revisit. Also rejected: `Operating
System Independent` — contradicted directly by the same sentence; and `Solaris`, `MobilePlatform`,
`Other` — no evidence at all.

---

### 21. CPU Architecture (RECOMMENDED)

- CPU Independent

*Source note.* Previously empty. dbprocessing is pure Python with no compiled extensions: `setup.py`
declares only `'packages': ['dbprocessing']` and a `scripts` list, with no `ext_modules`, no C
sources anywhere in the tree, and only pure-Python runtime requirements (`python_dateutil`,
`sqlalchemy`). The published wheel is `dbprocessing-0.1.0-py2.py3-none-any.whl` — the `none-any`
platform tag is the packaging system's own statement that the distribution is architecture
independent. `CPU Independent` is therefore precise, and specific architectures (`x86-64`,
`Apple Silicon arm64`, `Linux aarch64 or arm64`, `ppc64le`, `Sun (SPARC)`) would be both redundant
and under-inclusive. `GPU` and `HPC or HEC` were rejected: nothing in the package targets
accelerators, and there is no MPI, batch-scheduler or cluster integration.

---

### 22. Related Phenomena (OPTIONAL)

Not found — correctly empty.

*Source note.* This is a **closed** vocabulary of exactly seven terms: Coronal Heating, Coronal Mass
Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission. dbprocessing
supports science functionality for none of them: it is a pipeline controller with no physical model,
no phenomenon-specific processing and no phenomenon-specific data handling, and none of these seven
terms appears in the repository in any functional sense. The emptiness is the correct value, not a
gap to be filled — and because the vocabulary is closed, a phenomenon-flavoured term that a future
agent might want here (e.g. "radiation belts") would be rejected by the API and belongs in Keywords
instead.

---

### 23. Development Status (RECOMMENDED)

`Inactive`

*Source note.* Previously empty. `Inactive` is defined as "Reached stable, usable state but no
longer actively developed; support provided as time allows", and both halves fit.

*Reached a stable, usable state*: there is a packaged public release (0.1.0, on PyPI and Zenodo),
and `docs/README.rst:33-34` records that it *"has been used in production for nine years in several
different projects"*, controlling all RBSP-ECT data production and PSP/IS☉IS processing.

*No longer actively developed*: development activity ended abruptly after the release. Commits run
at 20-40 per month through February 2022, then total **four** commits ever since — one in September
2022 (renaming the default branch from `master` to `main`, `a0bf5e6`), one in February 2023 (a
networkx 2.0 compatibility fix in `fast_data.py`, `904bdf2`), one in November 2023 (pinning
SQLAlchemy below 2.0 in CI, `f68dc73`), and one in May 2024 (documentation typos, `dcaa21b`), which
is the pinned revision here. The issue tracker fell quiet at the same point: its most recently
created entry is issue #139, *Support pre-1.0 versions*, filed 2024-05-08 by Jonathan T. Niehof, who
also authored that final commit, and it is still open. Because GitHub numbers issues and pull
requests in a single sequence, an entry numbered above #139 would be the first sign that work has
resumed. The repository is not archived and `docs/SUPPORT.rst` still directs users to GitHub
Discussions Q&A, which matches "support provided as time allows".

Considered and rejected:

- **`Active`** — contradicted by the commit record above. `docs/README.rst:41-43` does say *"The
  developers are working daily to improve the maturity of the code"*, but that sentence was written
  for the 0.1.0 release in early 2022 and has not been true for years; it is stale prose, not
  current status.
- **`WIP`** — its definition requires "no stable, usable public release yet", which is false: 0.1.0
  is packaged and published. This was a genuine candidate because `docs/README.rst:37-40` calls the
  project *"an early beta state … not currently suitable for use without developer support"* and
  `setup.py:42` classifies it `Development Status :: 4 - Beta`. But beta maturity is not the same as
  having no release, and `Inactive` captures the situation more accurately.
- **`Unsupported`** — requires that the authors have ceased work and want a new maintainer. Nothing
  states that; the support channels are still advertised.
- **`Abandoned`**, **`Suspended`**, **`Moved`**, **`Concept`** — each is contradicted by a published
  release that is still the canonical location of an actively hosted, non-archived repository.

---

### 24. Documentation (RECOMMENDED)

`https://spacepy.github.io/dbprocessing/`

*Source note.* Previously empty. This is the project's declared homepage and documentation site:
`setup.py:63` sets `'url': 'https://spacepy.github.io/dbprocessing/'`, `docs/README.rst:9` says
*"Documentation is available at <https://spacepy.github.io/dbprocessing/>"*, and
`docs/SUPPORT.rst:12` repeats it. It resolves directly, without redirect, to the built Sphinx site,
whose page title is "dbprocessing documentation — dbprocessing v0.1.0 manual". It is published from
the repository's `gh-pages` branch.

The site includes installation instructions (`docs/getting_started.rst`, rendered as "Getting
Started"), which is what this field asks for. The PyHC registry lists the same URL without the
trailing slash; the trailing-slash form is used here because it is what the project's own `setup.py`
and README specify, and both resolve to the same page.

---

### 25. Funder (OPTIONAL)

| Organization | Funder Identifier |
|---|---|
| National Aeronautics and Space Administration | https://ror.org/027ka1x80 |
| Johns Hopkins University Applied Physics Laboratory | https://ror.org/029pp9z10 |

*Source note.* Previously empty. Both come from the project's own funding statement, the
"Acknowledgements" section of `docs/CONTRIBUTORS.rst`, which is explicit and enumerated:

> dbprocessing development has been supported in part by:
> * The Van Allen Probes Radiation Belt Storm Probe, Energetic particle, Composition, and Thermal
>   plasma suite, JHU/APL contract 967399 under NASA prime contract NAS5-01072.
> * The Parker Solar Probe Integrated Science Investigation of the Sun, JHU/APL contract 136435
>   under NASA prime contract NNN06AA01C.
> * NASA grant 80NSSC21K0307, "dbprocessing: Space Science Data Processing Controller in Python".

NASA is the prime sponsor of all three; JHU/APL is the entity that issued the two instrument-suite
subcontracts. Acronyms are expanded as the field requires ("JHU/APL" → Johns Hopkins University
Applied Physics Laboratory; "NASA" → National Aeronautics and Space Administration). Both
organisations are already represented in HSSI under these RORs.

**Which funder issued which award.** HSSI records funders at the software level and awards as
separate entries, and the link between a particular award and the agency that issued it is not
expressible through its update interface, so that correspondence survives only in this dossier:
`80NSSC21K0307` is the NASA grant made directly for dbprocessing; `967399` (Van Allen Probes
RBSP-ECT) and `136435` (Parker Solar Probe IS☉IS) are the two JHU/APL subcontracts, each let under a
NASA prime contract — `NAS5-01072` and `NNN06AA01C` respectively. Read back from HSSI alone, Fields
25 and 26 show two funders and three awards with nothing tying one to the other; this paragraph is
that tie.

**Considered and not selected: the United States Department of Energy / National Nuclear Security
Administration.** There are two independent traces of DOE involvement, and neither is a statement
that DOE funded dbprocessing's development:

1. `docs/COPYRIGHT.rst` states *"This program was produced under U.S. Government contract
   89233218CNA000001 for Los Alamos National Laboratory (LANL), which is operated by Triad National
   Security, LLC for the U.S. Department of Energy/National Nuclear Security Administration."* This
   is the boilerplate government-rights notice that LANL attaches to all released code, asserting
   the Government's licence in the work; it identifies the laboratory's management-and-operating
   contract, not a research award for this software.
2. The DOE CODE registration (record 63621) lists "Sponsoring Organization: USDOE Office of Science
   (SC), Advanced Scientific Computing Research (ASCR)" and "Contract/Award Number: AC52-06NA25396".
   That contract number is the *superseded* LANL operating contract (the pre-Triad one, replaced by
   89233218CNA000001), and ASCR sponsorship is corroborated by nothing in the repository, the
   documentation, or the NASA proposal. These read as registration-form defaults.

The project's own Acknowledgements section is the authoritative statement of what supported this
work, and it names three sources, all NASA-derived. DOE/NNSA is recorded here as considered so that
a future agent meeting either contract number recognises it as already evaluated rather than as a
missing funder.

---

### 26. Award Title (OPTIONAL)

| Award Title | Award Number |
|---|---|
| dbprocessing: Space Science Data Processing Controller in Python | 80NSSC21K0307 |
| Van Allen Probes Radiation Belt Storm Probe, Energetic particle, Composition, and Thermal plasma suite | 967399 |
| Parker Solar Probe Integrated Science Investigation of the Sun | 136435 |

*Source note.* Previously empty. All three are transcribed from the `docs/CONTRIBUTORS.rst`
Acknowledgements block quoted under Field 25.

The first award is the one directly aimed at this software, and its title is independently confirmed:
ADS/SciX indexes the funded proposal as `2020hdee.prop...17N`, "dbprocessing: Space Science Data
Processing Controller in Python", NASA Proposal ID 20-HDEE20_2-0017, PI Jonathan Niehof (University
of New Hampshire). That abstract is the most substantive published description of the software and
is recorded in Field 27.

For the other two, the award number recorded is the **JHU/APL subcontract** number under which the
dbprocessing team was actually funded (967399 and 136435). Each sits under a NASA prime contract —
`NAS5-01072` for Van Allen Probes and `NNN06AA01C` for Parker Solar Probe — which the acknowledgement
names but which funded the missions as a whole rather than this software specifically; those prime
numbers are recorded here in prose so the relationship is not lost, but the subcontract is the award
that supported dbprocessing. Which agency issued each of the three awards is recorded under Field
25, because HSSI itself cannot express that link. Titles are the acknowledgement's own phrasing with
the leading article and contract clause trimmed; both stay comfortably within the 128-character
limit that HSSI's award name field imposes.

Considered and not selected: contract `89233218CNA000001` and contract `AC52-06NA25396`, for the
reasons set out under Field 25.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- Niehof, J. (2020). *dbprocessing: Space Science Data Processing Controller in Python* [NASA
  proposal abstract, Proposal ID 20-HDEE20_2-0017].
  https://ui.adsabs.harvard.edu/abs/2020hdee.prop...17N/abstract

*Source note.* Previously empty. This entry uses the field's APA-with-permanent-link fallback
because the record has no DOI. It is included despite being a proposal abstract rather than a
journal article because, in the absence of any descriptive paper (see Field 14), it is the fullest
published account of what dbprocessing is, where it came from and what it has been used for — it
supplies the RBSP-ECT origin story, the PSP/IS☉IS and LANL deployments, and the design goals that
this record's Fields 4, 5, 31 and 32 rest on. ADS/SciX assigns it a stable bibcode and a permanent
URL, so the link is durable.

Considered and not selected:

- **DOE CODE record `10.11578/DC.20210924.1`** — a software registration, not a publication; the
  field's own guidance sends software DOIs to Fields 29/30 and publication DOIs here. It is
  discussed under Field 2.
- **The RBSP-ECT and PSP/IS☉IS instrument papers** — they describe the instrument suites whose data
  dbprocessing-managed pipelines produced, not the software. Listing them would attribute someone
  else's work to this record.
- **Papers citing dbprocessing** — none were found. ADS full-text searches for the Zenodo DOI, for
  `spacepy/dbprocessing`, and an acknowledgements-section search for `dbprocessing` all returned
  zero hits, and Semantic Scholar has no paper record for the concept DOI. The proposal abstract's
  claim of "hundreds of peer-reviewed science publications" refers to papers using RBSP-ECT *data*,
  which cite the mission and instrument papers rather than the pipeline software; those are not
  Related Publications for this record.

---

### 28. Related Datasets (OPTIONAL)

Not found.

*Source note.* Previously empty and left empty deliberately. dbprocessing produced the RBSP-ECT and
PSP/IS☉IS data products in operations, so a case could be made for listing those collections here.
It is not made, for two reasons. First, this field asks for datasets the software supports
functionality *for* — analysis of a dataset — and dbprocessing analyses nothing; it orchestrated the
codes that generated some of these files, which is a production relationship rather than a support
relationship. Second, and decisively, no authoritative dataset identifier ties a specific dataset to
this software: neither the repository, the Zenodo/DataCite record, nor the NASA proposal names a
dataset DOI or HPDE identifier. The mission-level relationship that *is* documented is captured
where it belongs, in Fields 31 and 32.

The unit-test fixtures under `unit_tests/data/db_dumps/` (`RBSP_MAGEIS_dump.json`,
`testDB_dump.json`) are database dumps used for testing, not datasets.

---

### 29. Related Software (OPTIONAL)

- `https://github.com/lanl/dbprocessing`

*Source note.* Previously empty. This is the **predecessor repository** — the private LANL codebase
from which the public project was created — which the field's guidance explicitly calls for
("software this work was forked from should also be included"). The evidence that it is the
predecessor rather than a mirror or fork: it was created 2020-07-14 and last pushed 2020-07-16,
bracketing the date `docs/release_notes.rst` gives for *"the creation of the public repository on
2020-07-15"*; its default branch is still `master` while the public repository renamed to `main` in
September 2022; its tags (`ver_1.0.0`, `hope_v1.0.0`, `comm_ver_1`, `cmmt88272`, `cmmt87599`) are
the pre-public LANL naming scheme, entirely unlike `release-0.1.0`; and the DOE CODE registration of
dbprocessing points at it as the repository. It has received nothing since July 2020. The
distinguishing information it carries — that dbprocessing began as internal LANL software and was
opened up in 2020 — is exactly what this field exists to record.

Considered and not selected:

- **SpacePy** — a genuine relationship, but recorded in Field 30 instead, where the demonstrated
  exchange is the stronger and more specific claim. See that field.
- **SQLAlchemy**, **python-dateutil**, **psycopg2**, **PostgreSQL**, **SQLite** — all real
  dependencies (the first two are the only declared runtime requirements), and all excluded. They
  are generic infrastructure: database plumbing and date parsing would be equally at home in a web
  application, a finance model or a biology pipeline, and saying "it depends on SQLAlchemy"
  distinguishes this software from almost nothing.
- **matplotlib**, **numpy**, **networkx**, **PySide/Qt**, **ghostscript** — same exclusion. All are
  used by individual scripts (`coveragePlot.py`, `histogramCodes.py`, `fast_data.py`,
  `gui/dbProcessingGUI.py`) but none is a domain tool whose presence characterises dbprocessing.
- **Environment Modules** (`http://modules.sourceforge.net`, wrapped by `dbprocessing/module.py`) —
  a site-specific job-environment tool, not heliophysics software, and not wired into the processing
  path at this revision.

---

### 30. Interoperable Software (OPTIONAL)

- `https://github.com/spacepy/spacepy`

*Source note.* Previously empty. SpacePy qualifies on demonstrated exchange, not on ecosystem
membership, and the specific evidence is:

- **Reading the files dbprocessing manages.** The project's only worked inspector example,
  `docs/developer/inspector_examples.rst:14,29,39-40`, uses `spacepy.pycdf` to open a CDF and derive
  the product's `utc_start_time`/`utc_stop_time` from its `CDF_EPOCH` variables. Inspectors are the
  documented extension point through which a format becomes supported, so this is the project
  teaching users to bridge dbprocessing to SpacePy.
- **Installed scripts that call SpacePy directly.** `scripts/fast_data.py:12,108,126` uses
  `spacepy.datamanager.RePath.path_split`/`path_slice` to reason about the managed directory tree;
  `scripts/coveragePlot.py:30` and `scripts/histogramCodes.py:12` use `spacepy.toolbox`
  (`bin_center_to_edges`, `binHisto`) when generating coverage and timing figures;
  `scripts/printInfo.py:15` imports `spacepy.pycdf`. These are installed console scripts, not
  examples.
- **Writing into the managed files.** `examples/scripts/addVerboseProvenance.py:7` uses
  `spacepy.pycdf` to copy dbprocessing's `verbose_provenance` record into a data file's CDF global
  attributes — an explicit, two-way exchange between dbprocessing's database and SpacePy-readable
  files.
- **The projects' own statement of the relationship.** `docs/README.rst:44-52`: the SpacePy
  organisation hosts dbprocessing and provides community support, and *"SpacePy is generally useful
  in processing Heliophysics data, e.g. in the codes that dbprocessing manages."*

That same section is equally clear about the limits, and the limit is the reason this is
interoperability rather than dependency: *"dbprocessing is not a component of SpacePy, nor does it
require SpacePy."* SpacePy appears in no `install_requires`; the scripts that use it fail without it
and the core package does not. Two peer heliophysics tools, deliberately combinable, with concrete
adapters between them — which is exactly what this field is for.

**Durable caveat worth knowing.** Several installed scripts have undeclared optional dependencies —
`coveragePlot.py` needs SpacePy, matplotlib, numpy and a `gs` binary; `histogramCodes.py` needs
SpacePy and matplotlib; `fast_data.py` needs SpacePy and networkx; `gui/dbProcessingGUI.py` needs
PySide and is written in Python 2 syntax that will not run under Python 3. `setup.py` declares only
`python_dateutil` and `sqlalchemy`. This does not change the values above, but it explains why a
dependency-file-based extractor sees none of these relationships.

Considered and rejected: the entire generic stack (numpy, matplotlib, SQLAlchemy, python-dateutil,
networkx, PySide) for the reasons given in Field 29; and any blanket claim of interoperability with
other PyHC packages on the strength of dbprocessing's PyHC community-registry listing — registry
membership is not a demonstrated exchange with any particular package.

---

### 31. Related Instruments (OPTIONAL)

| Instrument Name | Instrument Identifier |
|---|---|
| RBSP ECT | https://spase-metadata.org/SMWG/Instrument/RBSP/A/ECT |
| RBSP ECT | https://spase-metadata.org/SMWG/Instrument/RBSP/B/ECT |
| PSP Integrated Science Investigation of the Sun, ISOIS, Instrument | https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/ISOIS |

*Source note.* Previously empty. Each name above is the controlled-list row's own name, paired with
that row's `https://spase-metadata.org/` identifier. The identifier is what makes an entry
unambiguous — `RBSP ECT` is the name of two different rows, one per spacecraft — so the pairing above
is what should be preserved, not the names alone.

**Why these are "designed to support" despite dbprocessing being a generic framework.** This was the
hardest judgement in this record, and it is set out here in full so it does not have to be
re-litigated. The case against listing anything is real: the public package contains no
instrument-specific reader, parser or calibration code, and the RBSP/PSP strings that do appear in
the repository are illustrative rather than functional — documentation examples
(`docs/concepts.rst:119`, `docs/ConfigurationFiles.rst:429-502`, `docs/scripts.rst:1173-1195`),
commented-out configuration blocks (`scripts/coveragePlot.py:315-364`,
`scripts/makeLatestSymlinks.py:273-285`), a docstring (`dbprocessing/DButils.py:3239`), unit-test
fixtures (`unit_tests/data/db_dumps/RBSP_MAGEIS_dump.json`), and mission-specific helper scripts
kept under `examples/` and `developer/`. Example name-drops are exactly what the relevance gate
excludes.

The case for listing them is the "purpose-built or instrument-team tool" criterion, and it is
documented by primary sources rather than inferred:

- The NASA proposal abstract (ADS `2020hdee.prop...17N`), authored by the project's PI, states:
  *"To address this problem on the Radiation Belt Storm Probes-Energetic particle, Composition, and
  Thermal plasma suite (RBSP-ECT), the proposing team developed a system called dbprocessing …
  dbprocessing controlled the processing of all data from the RBSP-ECT suite"*, and *"The data
  similarly processed for Parker Solar Probe/Integrated Science Investigation of the Sun
  (PSP/ISOIS) have already resulted in over a dozen peer-reviewed publications."*
- `docs/CONTRIBUTORS.rst` independently confirms both, listing the RBSP-ECT suite and the PSP IS☉IS
  investigation as the two instrument-suite programmes that funded development.
- `docs/concepts.rst:533` records a feature built specifically for one of them: *"The QA loop was
  designed for RBSP-ECT to permit e.g. the validation of level 1 files before generating level 2."*

So dbprocessing is not merely "configurable for" these suites: it was written by the ECT team for
ECT, it produced the entirety of the ECT data record, at least one of its features exists because
ECT needed it, and it was then applied to IS☉IS. Someone asking what produced RBSP-ECT's data
products should find this software.

**Corroborating evidence in the deployment scripts.** `examples/scripts/hopeCoverageHTML.py:12,15`
and `examples/scripts/magephem-pre-CoverageHTML.py:12,15` each carry `import rbsp` and
`from rbsp import Version` alongside their `dbprocessing` imports, and call
`rbsp.UTC_to_mission_day('a', d)` — an RBSP mission-day conversion keyed by spacecraft letter — when
building their coverage tables. That `rbsp` package is not part of this repository, is not declared
in `setup.py`, and is not the `rbsp` name registered on PyPI (which belongs to an unrelated
text-indexing project); it is also not SpacePy, which neither script imports. It reads as a
site-local, apparently unpublished LANL/ECT mission package, and its use shows these scripts were
written to run inside a live RBSP deployment rather than as generic illustrations.

Two limits on how far that carries, recorded so the evidence is not over-read. It is **not** grounds
for a Field 30 entry: that field requires a public, named domain tool with a demonstrated exchange,
and this package is neither public nor identifiable. And both scripts sit under `examples/`, which
the project describes as "miscellaneous bits for sharing between developers" of which "some examples
may be out-of-date for current dbprocessing" (`examples/README.txt`). So this corroborates the
RBSP-specific deployment established above by the proposal abstract and the Acknowledgements; it does
not carry the field on its own. If a future refresh establishes what this `rbsp` package actually is
— a released package with its own repository or DOI, say — it would be worth revisiting whether it is
independently notable for Field 29 or 30.

**Granularity — why suites and not sub-instruments.** The evidence is stated at suite level ("the
RBSP-ECT suite", "PSP/ISOIS"), and the controlled vocabulary happens to match that granularity
exactly: it has `RBSP ECT` rows but **no rows at all for HOPE, MagEIS or REPT** individually, and it
has a single suite-level `PSP Integrated Science Investigation of the Sun, ISOIS, Instrument` row
distinct from the four EPI-Hi/EPI-Lo sub-instrument rows. Expanding to sub-instruments would
therefore have been both unsupported by the evidence and, for ECT, impossible without inventing
rows.

**Resolution details.** `RBSP ECT` matches two rows, one per spacecraft, and both are recorded
because the repository names both: `docs/ConfigurationFiles.rst:459-476` configures
`rbspa_int_ect-mageis*-L3` **and** `rbspb_int_ect-mageis*-L3` products in parallel panels, and
`docs/developer/tables.rst:643-644` explains the mission/satellite hierarchy using exactly
RBSP-A and RBSP-B. The IS☉IS suite row matched uniquely on name. None of these three rows has an
`.html` duplicate variant, so the bare identifiers above are the whole story for them.

Considered and not selected:

- **RBSP EMFISIS** (rows exist for both spacecraft). `examples/scripts/link_missing_ql_mag_l2_mag.py`
  manipulates `rbsp-a/b_magnetometer_uvw_emfisis-*` CDF filenames, and the NASA proposal notes that
  ECT and IS☉IS processing consumed *"level 2 magnetic field inputs from other instruments"*. But
  EMFISIS files enter as opaque externally produced inputs to an ECT product chain; there is no
  EMFISIS inspector, reader or format handling anywhere in the package. EMFISIS appears only as
  product-name strings in unit-test fixtures (`unit_tests/test_DButils.py`,
  `unit_tests/data/db_dumps/RBSP_MAGEIS_dump.json`) and in one symlink-management helper under
  `examples/`, which the project itself marks as possibly out of date. Being an upstream input to a
  supported pipeline is not the same as supporting the instrument.
- **RBSPICE, RBSP EFW, RBSP RPS, PSP FIELDS, PSP SWEAP** — vocabulary rows exist for all of them and
  none is supported: RBSPICE and EFW appear nowhere in the repository at all, and the others only as
  siblings of the suites that are listed.
- **The >20 LANL national-security satellites** named in the NASA proposal as another dbprocessing
  deployment. No instrument or observatory for them is identifiable, they are not in SPASE, and they
  are outside HSSI's scope. Documented omission.

---

### 32. Related Observatories (OPTIONAL)

| Observatory Name | Observatory Identifier |
|---|---|
| Van Allen Probes | https://spase-metadata.org/SMWG/Observatory/RBSP |
| Parker Solar Probe | https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe |

*Source note.* Previously empty. Both rest on the same primary evidence set out at length under
Field 31 — the PI-authored NASA proposal abstract and the project's own Acknowledgements — which
document these two missions as the deployments dbprocessing was built for and applied to. Both names
are the controlled-list rows' own names, paired with those rows' SPASE identifiers.

**Resolution details.** `Van Allen Probes` matched exactly one row, the mission-level
`SMWG/Observatory/RBSP`. The per-spacecraft rows `Radiation Belt Storm Probe A`
(`.../Observatory/RBSP/A`) and `Radiation Belt Storm Probe B` (`.../Observatory/RBSP/B`) also exist,
but the mission-level row is the right granularity: dbprocessing supported the ECT data production
for the mission as a whole rather than for one spacecraft, and both spacecraft appear symmetrically
throughout the documentation. `Parker Solar Probe` matched three same-name rows — two CNES/CDPP
catalogue entries (`CNES/Observatory/CDPP-AMDA/PSP` and `CNES/Observatory/CDPP-Archive/PSP`) and the
SMWG entry — resolved to `SMWG/Observatory/ParkerSolarProbe` by the SMWG tie-break rule that applies
to same-name duplicates.

Considered and not selected: no other mission. In particular, the LANL national-security satellites
mentioned in the NASA proposal have no SPASE observatory record and fall outside heliophysics scope,
and the synthetic "mission" used by `functional_test/` (a rot13 pipeline over invented `testDB_*`
products) is a test fixture, not an observatory.

**Consistency check for future refreshes.** These two missions are also the basis for
`Observatory/Mission-specific` in Field 17, for the `van allen probes` and `parker solar probe`
keywords in Field 16, and for the region choices in Field 5. If a later refresh removes them here,
those fields should be revisited together.

---

### 33. Logo (OPTIONAL)

Not found.

*Source note.* dbprocessing has no logo. There is no image asset in the repository other than
`docs/images/schema.dot`, a Graphviz source for the database schema diagram; the documentation site's
header is plain text (`docs/_templates/layout.html` renders `<h1>dbprocessing</h1>`, not an image);
the images published on the `gh-pages` branch are the Sphinx theme's own UI icons
(`_static/contents.png`, `file.png`, `minus.png`, `navigation.png`, `plus.png`) plus the rendered
schema diagram (`_images/graphviz-*.png`), none of which is a logo; and the dbprocessing block of the
PyHC community registry (`_data/projects.yml`) contains no `logo` key at all, whereas other entries
in that same file do carry an explicit `logo:` key holding an image URL. This is a real absence, not
an unsearched field.
