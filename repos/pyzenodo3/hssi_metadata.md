# HSSI Metadata Extraction Results

**HSSI Software ID:** d9a43a8e-0ad0-448f-8915-d9bb66d9e508
**Repository:** https://github.com/space-physics/pyzenodo3
**Source Revision:** 09bdb3f9f0ac9961f74220a21ca6d4fd666e198a
**Extraction Date:** 2026-09-07
**Validation Date:** 2026-09-08
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

Every claim below about the code is measured at the pinned revision
`09bdb3f9f0ac9961f74220a21ca6d4fd666e198a`, which is the **last commit on `main`** (2021-04-27) and equals
`refs/heads/main` on origin. The repository's *live* surface extends past that pin — three community pull
requests, the newest opened 2023-07-27, are open and unmerged, and none of their content is in the pinned
tree. So "the code does not do X" statements here are statements about the released and merged code, not
about what has been proposed. Where an open PR is the reason a capability is absent, this file says so.

A second framing point that governs three separate fields. PyZenodo3 is a Python-3 port of Tom Klaver's
earlier `pyzenodo` package (evidence under Field 6). Adjudicated **individually**, three of this entry's
oddities each yield a defensible wrong answer: drop Klaver as an author with no commits; flag the
Apache-2.0 licence as anomalous against its MIT-licensed `space-physics` siblings; leave Field 29 with no
predecessor. They share **one cause**, and the evidence for it is recorded under Fields 6, 15 and 29 so a
later reader does not re-litigate them one at a time.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Source:** Placeholder. The submitter is supplied at submission time and is not a property of the software.

---

### 2. Persistent Identifier (RECOMMENDED)

- **DOI:** https://doi.org/10.5281/zenodo.3239431

**Source:** Zenodo concept (all-versions) DOI, carried over from the existing HSSI record and re-derived
from Zenodo. Querying `conceptrecid:3239431` with `all_versions=true` returns exactly **4** deposits, and
every one carries `conceptdoi: 10.5281/zenodo.3239431`:

| record | version DOI | `metadata.version` | date | `isSupplementTo` |
|---|---|---|---|---|
| 3239432 | `10.5281/zenodo.3239432` | `v0.3.1` | 2019-06-05 | `https://github.com/scivision/pyzenodo3/tree/v0.3.1` |
| 3239436 | `10.5281/zenodo.3239436` | `v1.0.0` | 2019-06-05 | `https://github.com/scivision/pyzenodo3/tree/v1.0.0` |
| 3537730 | `10.5281/zenodo.3537730` | `v1.0.1` | 2019-11-11 | `https://github.com/space-physics/pyzenodo3/tree/v1.0.1` |
| 3772154 | `10.5281/zenodo.3772154` | `v1.0.2` | 2020-04-28 | `https://github.com/space-physics/pyzenodo3/tree/v1.0.2` |

Every deposit carries an `isSupplementTo` pointing at a `/tree/<tag>` URL, the signature of a
GitHub-integration deposit rather than a manual upload. The `scivision` → `space-physics` organisation
rename is visible across the 2019-06-05 and 2019-11-11 deposits; both spellings resolve today.

**Divergence from the repository, and why it is not an error.** The pinned `CITATION` file contains one
line and nothing else:

```
https://doi.org/10.5281/zenodo.3537730
```

That is the **v1.0.1 version DOI** — one release behind the newest. It is not stale by accident and not
worth "fixing" toward: `CITATION` was created at commit `b8a5049` (2019-12-06, "Create CITATION"),
which falls *after* the v1.0.1 tag (2019-11-11) and *before* the v1.0.2 tag (2020-04-28). It recorded
the then-current version DOI correctly and was simply never revised at the next release. Both DOIs are
real and both resolve. This is a documented divergence, not a conflict.

**Why the concept DOI is the better catalogue value.** `https://doi.org/10.5281/zenodo.3239431` redirects
to `https://zenodo.org/records/3772154` — the newest release — so it tracks forward on its own, whereas a
version DOI pins a reader to one release forever. A searcher who clicks Field 2 wants the software, not a
specific historical snapshot. The version DOI for the release actually recorded in Field 12 is held there
(`version_pid`), so nothing is lost.

**The choice between the two DOIs, settled.** The concept DOI
`https://doi.org/10.5281/zenodo.3239431` is the recorded value. The alternatives were weighed and not
taken, and both are recorded here so neither is rediscovered as new evidence. The repository's own
`CITATION` DOI, `https://doi.org/10.5281/zenodo.3537730`, has the genuine merit of being what the
maintainer wrote down by hand, and mirroring a project's stated citation is easy to defend; it was not
chosen because it freezes the citation at v1.0.1 while Field 12 records v1.0.2, and because the
concept DOI already resolves to the newest deposit without anyone having to maintain it. Clearing the
field was also considered and not taken: the entry's "Cite Me" block, headed *Software*, is built from
this DOI through doi.org content negotiation, and dropping a real, resolving DOI would remove that
block for no gain. Moving the DOI to Field 14 or Field 27 was never available — there is no
publication here, only software deposits.

---

### 3. Code Repository (MANDATORY)

- **Repository URL:** https://github.com/space-physics/pyzenodo3

**Source:** The repository itself; identity closed on four independent sources that agree — the pinned
`setup.cfg` (`url = https://github.com/space-physics/pyzenodo3`), the PyPI JSON API
(`home_page` for `pyzenodo3`), the PyHC registry entry's `code:` key, and the newest two Zenodo deposits'
`isSupplementTo` URLs. Unchanged from the existing HSSI record.

The older `scivision/pyzenodo3` spelling appears in the 2019-06-05 Zenodo deposits and in the pinned
README's "Latest development" install snippet (`git clone https://github.com/scivision/pyzenodo3`). It is
the pre-rename organisation name and still redirects, but `space-physics` is the current canonical form
and is what GitHub's API returns as `full_name`.

---

### 4. Software Functionality (RECOMMENDED)

- **Data Processing and Analysis**
- **Data Processing and Analysis: Data Access and Retrieval**

**Source:** Carried over from the existing HSSI record and re-confirmed against the pinned code. Both rows
resolve in the live `FunctionCategory` vocabulary, the child's parent is `Data Processing and Analysis`,
and that parent is stored — so there is no orphaned-child structural defect here. Both names are unique in
the vocabulary (83 rows, 67 distinct names, 13 names duplicated across parents), so neither can resolve
into the wrong branch.

**Form.** Written `Parent: Child` **with a space after the colon**. This is the canonical rendering: the
`software-functionality` classification guide documents the spaced `Parent: Child` form as the canonical
one the API returns, and this entry's own stored functionality values render as
`Data Processing and Analysis: Data Access and Retrieval`. A prior version of this dossier wrote the
unspaced `Data Processing and Analysis:Data Access and Retrieval`; that was the deviation, not the norm.
The serializer accepts both, so this is a presentation fix, not a value change.

**Why Data Access and Retrieval.** The public API in `src/pyzenodo3/base.py` is entirely remote-archive
querying: `Zenodo.search()` (free-text query against the Zenodo REST API), `find_record_by_doi()`,
`find_record_by_github_repo()`, `get_record()`, `Record.get_versions()` and
`Record.get_versions_from_webpage()`. `src/pyzenodo3/upload.py` adds the write direction —
`create()`, `upload_data()`, `upload_meta()` — against the same archive.

**Considered and rejected.**
- `Servers and Environments: Distribution/Access` — PyZenodo is a client library and a CLI, not a server,
  a container, or deployment infrastructure. That parent covers software that *is* the environment.
- `Mission-related: Archive` and its siblings — nothing here is mission ground-system software; Zenodo is
  a general-purpose research-data repository, not a mission archive.
- `Data Visualization` and every child — the pinned tree imports no plotting library and produces no
  figures. `git grep -P -i 'matplotlib|pyplot|plotly|bokeh'` over the pinned tree returns nothing.
- `Coordinate Transforms`, `Models and Simulations` and all their children — there is no physics, no
  numerics, and no coordinate system anywhere in the tree.

**Considered in this refresh and not added: `Data Processing and Analysis: File Format Conversion`.**
The case for it was substantive and is recorded in full, because the code evidence behind it is real
and will be found again. `upload.meta()` in `src/pyzenodo3/upload.py` reads a `.ini` file with
`ConfigParser`, assembles a `dict`, and writes it out as JSON to `inifn.with_suffix(".json")` —
literally reading one file format and writing another, as a user-facing step of the documented upload
workflow; and Fields 18 and 19 record exactly that pair (`Other` in for the `.ini`, `JSON` out), so
the category would have sat consistently alongside them. It was not added because what is converted is
**deposit metadata**, not scientific data, and this child sits among the data-processing categories: a
searcher filtering on File Format Conversion is looking for something that converts CDF to netCDF, not
INI to JSON. That is a judgement about what the filter should return, not a refutation of the code
evidence, which stands as written. The two values above are the settled classification.

---

### 5. Related Region (RECOMMENDED)

- **Not found**

**Source:** Evidenced-empty. Before this refresh the record carried three regions — `Earth Atmosphere`,
`Earth Magnetosphere` and `Solar Environment` — each of which resolves in the live `Region` vocabulary.
Their provenance was never the code: they were a one-to-one restatement of three of the four PyHC
registry keywords for this package (`ionosphere_thermosphere_mesosphere`, `magnetosphere`, `solar`),
which are PyHC's browse facets rather than statements about what the software computes. All three were
removed in this refresh, leaving the field deliberately empty.

**Why they were removed.** PyZenodo is a REST client for a general-purpose research-data repository.
The pinned tree contains no region-specific code, no region-specific data handling, and no domain
vocabulary at all — the word-anchored sweep recorded under Fields 31/32 finds **zero** occurrences of
any heliophysics term in any tracked file. Nothing in the package behaves differently for an
ionospheric dataset than for a genomics dataset. Decided from the searcher's side: someone filtering
HSSI by `Earth Magnetosphere` is asking for software that does something with the magnetosphere, and
handing them a Zenodo REST API wrapper spends their attention for nothing.

**The case for keeping them, which was real and lost on judgement rather than on fact.** The three
values came from PyHC's curated registry, which is a trustworthy source and the highest-priority one
this workflow recognises; they are how PyHC's own faceted browse surfaces this package; and a broad
region tag costs an individual searcher little while opening one more path into the entry. Clearing
them does make this software invisible to anyone who arrives through a region facet, and that loss is
accepted rather than denied. The argument did not prevail because registry facet tags of this kind
propagate widely and are frequently unsupported by the software they are attached to, and because
preserving one path in trades away the precision of every searcher who filters on those regions.
Nothing here refutes the PyHC provenance — it remains accurate, and it is set out under Field 16,
where the same tags are discussed as keywords.

**Decided together with Field 16, and not to be reopened separately.** These three regions and the
three PyHC keywords dropped in Field 16 descend from the same four registry facet tags seen through
two fields. They were adjudicated as a single judgement about those tags; restoring either set alone
would leave the record asserting through keywords what it denies through regions.

**Note on the vocabulary's shape.** `Region` is flat — every row is top-level, with no parent/child
edges populated. So `Earth Atmosphere` did not imply `Earth Ionosphere` or `Earth Thermosphere`, and
an argument of the form "X encompasses Y" carries no weight here; each value stands or falls alone.
Fields 4 and 5 are RECOMMENDED, not mandatory, so an evidenced-empty Field 5 is a legitimate outcome;
what would be wrong is an unexamined blank, which this is not.

---

### 6. Authors (MANDATORY)

#### Author 1
- **Author:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation 1:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** https://ror.org/05qwgg493
- **Affiliation 2:**
  - **Organization:** Scivision, Inc.
  - **Affiliation Identifier:** Not found

#### Author 2
- **Author:** Tom Klaver
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Source:** Both authors are carried over from the existing HSSI record, and the pair matches the pinned
`setup.cfg` line 4 exactly:

```
author = Michael Hirsch; Tom Klaver
```

That is the only place a real person is credited as an author anywhere in the tracked tree at the pin.
(One other file carries an `author =` key: `src/pyzenodo3/tests/meta.ini` line 2 reads `author = Jane Doe`,
the placeholder in the test fixture used to exercise the `.ini`-to-JSON metadata conversion.) PyPI's
`author` field for `pyzenodo3` carries the same string. Hirsch's ORCID and both affiliations come from the
stored record; the earlier dossier for this software recorded his identifier as "Not found", which was
poorer than what the catalogue already held, and is superseded here.

The `Scivision, Inc.` / `SciVision, Inc.` capitalisation varies across sources. The stored form is
`Scivision, Inc.`; that spelling is parked catalogue-wide and is deliberately left alone here.

**Why Tom Klaver is an author despite having zero commits — the provenance evidence.**

Klaver is credited in `setup.cfg` but appears in no commit in this repository. The reason is that
**pyzenodo3 is a Python-3 modernisation of Klaver's earlier `pyzenodo` package**, and the credit is for
the original code, not for work in this repository. Recorded here in full so that a future refresh does
not "correct" the author list by dropping him.

*The predecessor.* `https://github.com/Tommos0/pyzenodo` — created 2017-09-26, last pushed 2017-11-09,
`fork: false`, licensed Apache-2.0. Published on PyPI as `pyzenodo`, latest version `0.0.6` (uploaded
2017-11-09), summary `Python wrapper for the Zenodo REST API`, `author: Tom Klaver`, `author_email:
t.klaver@esciencecenter.nl`, `license: Apache 2.0`.

*The derivation, established mechanically.* Comparing Klaver's `pyzenodo/zenodo.py` (117 lines) against
this repository's `src/pyzenodo3/base.py` at the pin (143 lines):

- Both files define **exactly the same 14 classes and functions, with none unique to either side**:
  `Record`, `Zenodo`, `__init__`, `__str__`, `_extract_github_repo`, `_get_records`, `_row_to_version`,
  `find_record_by_doi`, `find_record_by_github_repo`, `get_record`, `get_versions`,
  `get_versions_from_webpage`, `original_version`, `search`.
- Five distinctive strings occur **once in each file, byte-identical**: the docstring
  `Get version details from Zenodo webpage (it is not available in the REST api)`; the CSS selector
  `.well.metadata > table.table tr`; the comment `zenodo can't handle '/' in search query`; the base URL
  `https://zenodo.org/api/`; and the comment `when only 1 version`.
- The GitHub-repo regex is the same pattern in both, differing only in quote style
  (`r'.*github.com/(.*?/.*?)[/$]'` upstream vs `r".*github.com/(.*?/.*?)[/$]"` here) — a `black`
  reformatting artifact; `pyproject.toml` at the pin sets `[tool.black]` with `line-length = 100`.
- **Negative control**, which is what makes this a demonstration rather than an observation that two
  Python files resemble each other: `from __future__ import annotations` occurs **0** times in Klaver's
  file and **1** time in `base.py`. The comparison is not trivially matching everything.

The port's differences from the original are exactly what a Python-3 modernisation looks like: type
annotations, f-strings, `raise LookupError` / `KeyError` where the original returned `None`, and the
`src/` layout.

*The attribution predates the ported code.* The first three commits, in order:

| # | commit | date | what it adds |
|---|---|---|---|
| 1 | `0a6ac35` | 2018-06-24 | "Initial commit" — adds `.gitignore` and `LICENSE` (201 lines, opening `Apache License` / `Version 2.0, January 2004`) |
| 2 | `eeb6a3c` | 2018-06-24 | "setup template" — creates `setup.cfg` as a new file, in one hunk setting both `author = Michael Hirsch, Tom Klaver` and `license = Apache 2.0`, alongside `install_requires` of `requests` and `Beautifulsoup4` (the two libraries Klaver's module imports) and `Development Status :: 3- Alpha` |
| 3 | `2bb34a1` | 2018-06-24 | "INWORK: init migrate  (not yet working)" — only now does the ported source arrive, as `pyzenodo3/__init__.py` at 111 lines |

So the licence text lands at commit 1, the author-and-licence metadata at commit 2, and the ported code at
commit 3: **both the Klaver credit and the Apache-2.0 licence are established before the ported code
exists.** `git log -S'Klaver' -- setup.cfg` returns exactly one commit, `eeb6a3c` — the credit entered
once, at creation, and was never retrofitted or revised. (The separator later changed from `,` to `;`;
the names never did.)

**Commit authorship at the pin**, from `git rev-list <pin>` with a per-commit `%an <%ae>` — deliberately
not `git log --all`, which would sweep in refs unreachable from the pin:

| commits | author string |
|---|---|
| 24 | `Michael Hirsch, Ph.D <scivision@users.noreply.github.com>` |
| 4 | `Michael Hirsch <scivision@users.noreply.github.com>` |
| 3 | `Michael Hirsch, Ph.D <10931741+scivision@users.noreply.github.com>` |
| 1 | `Kaspar Emanuel <kaspar.emanuel@gmail.com>` |

32 commits total. The numeric-prefix GitHub noreply form is genuine here — it carries three real commits,
not a mailmap artifact. All four strings are one person plus one, under two spellings of Hirsch's name and
two generations of his GitHub noreply address.

**Kaspar Emanuel is not a third author — the question was put in this refresh and settled.**

*The facts, each verified at the pin.*
- Emanuel authored **one** commit reachable from the pin: `1c63c64`, 2020-04-09, "Add --use-sandbox switch
  to upload_zenodo.py", merged at `3a74e67` ("Merge branch 'allow-sandbox' of
  git://github.com/kasbah/pyzenodo3 into kasbah-allow-sandbox").
- His contribution is **named in the catalogue record three times over**: the stored Field 8 description
  credits the `--use-sandbox` flag; the stored Field 12 version description ends "(thanks to @kasbah)";
  and the upstream v1.0.2 GitHub release body reads "thanks to @kasbah for adding
  `upload_zenodo.py --use-sandbox` flag to avoid cluttering Zenodo with test uploads".
- `kasbah` and `emanuel` appear **nowhere in the tracked tree** at the pin — case-insensitively, in any
  file. The tree's only real-person author credit is `setup.cfg` line 4, and he is not in it.
- All four Zenodo deposits credit `Michael Hirsch, Ph.D.` alone, with no ORCID and no affiliation.
- The PyHC registry lists `contact: Michael Hirsch` and no other person.

*The criterion, derived from this tree rather than imported.* This repository states its authorship in one
deliberate place and has done so since its second commit. That statement includes a person with **zero**
commits (Klaver, for authoring the upstream code) and excludes a person **with** a commit (Emanuel). So
`setup.cfg`'s author line is demonstrably not a commit ledger — it is an editorial statement of who wrote
the package, maintained by hand, and it was updated across the repository's life (the separator changed,
the version and classifiers changed) without ever adding Emanuel. Applying that one criterion:
Hirsch **in** (wrote the port), Klaver **in** (wrote the original), Emanuel **out** (contributed one
feature to an existing package, and the maintainer thanked him in a release note rather than promoting him
to author). Every inclusion and every exclusion here comes from that single test.

*The argument for adding him, recorded in full so it is not mistaken for an oversight.* The union rule
for author reconciliation says not to silently drop a credited contributor, and Emanuel *is* credited —
by name, in the upstream release notes and in the version description this catalogue stores — so a site
user browsing by author would arguably be glad to find him. He wrote the `--use-sandbox` feature that
the record's own user-visible prose describes, which is not a marginal contribution to a package this
small. That argument was weighed and did not prevail. The credit that exists is a thank-you in a
changelog, which is the conventional way a project distinguishes a contributor from an author; the
catalogue already surfaces it in the Field 12 version description, where a reader will see it; and the
repository's own consistently applied criterion, set out just above, excludes him. Two authors —
Hirsch and Klaver — is the settled value: it matches `setup.cfg`, matches every external source, and
follows the test the repository itself demonstrates.

*A durable fact for anyone who reopens this.* No `Person` row exists for Kaspar Emanuel, and no stored
person carries `kaspar` or `emanuel` in a name field. Adding him would therefore **mint** a new shared
person row as a side effect, which makes the addition a database-side creation rather than a metadata
patch value, and places it with whoever administers the database.

**Deliberately not proposed, for either Klaver or Emanuel: an ORCID or an affiliation.**
- **No ORCID is identifiable for either**, but the searches are worth recording precisely, because one of
  them turns up a tempting near-match that must not be used. Using ORCID's public expanded search with
  *fielded* queries (an unfielded `q=Kaspar Emanuel` is an OR search and returns tens of thousands of
  irrelevant records — do not read a raw count from one):
  - `given-names:Kaspar AND family-name:Emanuel` returns **0**. The control
    `given-names:Michael AND family-name:Hirsch` returns **7**, among them Hirsch's own
    `https://orcid.org/0000-0002-1637-6526` affiliated to Boston University — so the query shape works and
    the zero is a real absence, not a syntax artifact.
  - `family-name:Klaver` alone returns a broad set of records, and
    `given-names:Tom AND family-name:Klaver` narrows to exactly **one** record,
    `https://orcid.org/0000-0001-9411-2107`, whose name is "Tom Klaver". **It is not usable.** That
    record is empty: no employments, no educations, no works, no email, no researcher URLs.
    Nothing in it connects to the Netherlands eScience Center, to the `pyzenodo` package, or to any
    software or publication at all. A name match alone does not identify a person, and Klaver is a common
    Dutch surname. Recorded here so a future refresh finds this record, recognises that it was already
    examined and rejected for want of any corroborating evidence, and does not attach it.
- Klaver's stored person row exists **without** an identifier. Sending an ORCID for an already-stored
  identifier-less author orphans his existing row and mints a duplicate, so no ORCID may be attached to
  him through a metadata update even if one were later found.
- Klaver's PyPI `author_email` (`t.klaver@esciencecenter.nl`) implies the Netherlands eScience Center, but
  an email domain in a 2017 package is weak evidence of his affiliation *for this work*, and no
  `Organization` row exists for that institution. (The ROR is `https://ror.org/00rbjv475`, confirmed by its
  registered domain `esciencecenter.nl`; no stored organisation carries it, and none carries the name,
  against a control that finds `Boston University` by its ROR. The one superficially similar row,
  `University of Washington eScience Institute`, is a different institution on a different continent and
  must not be substituted.) Asserting the
  affiliation would mint an organisation row as a side effect. Not proposed.

---

### 7. Software Name (MANDATORY)

- **Software Name:** PyZenodo

**Source:** Carried over from the existing HSSI record, and independently the PyHC registry's authoritative
`name:` for this package and the pinned README's H1 (`# PyZenodo`).

The distribution and import name is `pyzenodo3` — that is the PyPI project name, the GitHub repository
name, and the package directory (`src/pyzenodo3/`). `PyZenodo` is the display name and is what a reader
recognises; the numeral in `pyzenodo3` marks the Python-3 port of Klaver's `pyzenodo` (Field 6) rather
than a version. Both are correct in their own register, and the display name is the right one for a
catalogue heading. Recorded here so the identifier form is not mistaken for a discrepancy.

---

### 8. Description (MANDATORY)

- **Description:** PyZenodo, distributed as the `pyzenodo3` Python package, is a pure Python wrapper for the Zenodo REST API. It provides a Python 3 interface for interacting with Zenodo records, including functionality to search Zenodo by query, GitHub repository, or DOI; retrieve record/version metadata; prepare Zenodo metadata from `.ini` files; and upload files to Zenodo depositions. The package includes a `--use-sandbox` flag to avoid cluttering Zenodo with test uploads during development. PyZenodo is useful for researchers who need to programmatically deposit datasets or inspect Zenodo records as part of their data management workflows.

**Source:** Carried over verbatim from the existing HSSI record. Retained as editorial intent, and checked
clause by clause against the pinned code — every claim holds:

| clause | code at the pin |
|---|---|
| "search Zenodo by query, GitHub repository, or DOI" | `Zenodo.search()`, `find_record_by_github_repo()`, `find_record_by_doi()` in `base.py` |
| "retrieve record/version metadata" | `get_record()`, `Record.get_versions()`, `Record.get_versions_from_webpage()` |
| "prepare Zenodo metadata from `.ini` files" | `upload.meta()` reads an `.ini` with `ConfigParser` and writes the JSON |
| "upload files to Zenodo depositions" | `upload.create()` then `upload.upload_data()` |
| "a `--use-sandbox` flag" | `upload.main()` adds `--use-sandbox`, switching the base URL to `https://sandbox.zenodo.org/api` |

**One thing this description deliberately does not say, and should not be "improved" to say.** The
repository's own README states `Allows upload / download of data from Zenodo.` and GitHub's repository
description reads `Simple, clean pure Python 3 Zenodo API (upload, download). ` — but **no download
function exists in the pinned tree.** `base.py` retrieves record *metadata* over the REST API; `upload.py`
only writes. Adding file download is the subject of open pull request #9 ("Adding support to download the
Files", opened 2023-04-10 — the upstream title ends in a trailing space, elided here), which is
unmerged. The stored description is more accurate than the project's own README, and a future refresh
should not regress it toward the README's wording.

---

### 9. Concise Description (OPTIONAL)

- **Concise Description:** Pure Python wrapper for the Zenodo REST API that enables programmatic record search, metadata retrieval, and file upload.

**Source:** Carried over verbatim from the existing HSSI record. Retained as editorial intent. It is a
faithful compression of Field 8 and shares its accuracy about download (it claims record search, metadata
retrieval and file *upload* — not download). No change proposed.

---

### 10. Publication Date (RECOMMENDED)

- **Publication Date:** 2018-06-25

**Source:** Carried over from the existing HSSI record and **triply evidenced** from primary sources that
agree to within hours:

- **PyPI**, first release: `pyzenodo3` version `0.1.0`, earliest file upload `2018-06-25T16:26:28Z`.
- **GitHub**, repository `created_at`: `2018-06-25T04:32:28Z`.
- **Git**, first commit `0a6ac35`: author date 2018-06-24 22:32:29 −0600, i.e. **2018-06-25 04:32:29 UTC**
  — the same minute as the GitHub creation timestamp, as expected for a repository created through the web
  UI with an initial commit.

**Why the earliest tag does not contradict this.** The earliest tag in the repository is `v0.1.1` at
`3859bdc`, dated **2018-06-26** — one day *later* than the publication date. That ordering is normal, not
anomalous: version `0.1.0` was published to PyPI on 2018-06-25 without ever being tagged, and tagging began
one release later. A future agent seeing "publication date precedes the first tag" should not treat it as
a defect. This note replaces the earlier dossier's bare citation of SoMEF's `date_created` field, which
invited exactly that doubt.

---

### 11. Publisher (RECOMMENDED)

- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** Carried over from the existing HSSI record; independently supported by the four Zenodo deposits
under Field 2, which are the software's formal publication.

**On the identifier form.** Every other organisation identifier in this dossier is a ROR, so the site URL
looks anomalous. It is not: a ROR query for `Zenodo` returns **0** results — Zenodo has no ROR of its own
(the operating institution, CERN, does, but CERN is not the publisher named on these deposits).
`https://zenodo.org` is the correct persistent identifier available. Recorded so a later refresh does not
go hunting for a ROR that does not exist, or substitute CERN's.

The `Organization` row behind this value is shared across the catalogue, so any change to its name or
identifier is a database-side edit affecting other entries, not a per-software field update. No change is
proposed.

---

### 12. Version (RECOMMENDED)

#### Latest published release
- **Version Number:** 1.0.2
- **Version Date:** 2020-04-28
- **Version Description:** Added `upload_zenodo.py --use-sandbox` flag to avoid cluttering Zenodo with test uploads (thanks to @kasbah). Moved package to src/ layout.
- **Version PID:** https://doi.org/10.5281/zenodo.3772154

**Source:** Carried over from the existing HSSI record. The number, date and PID are corroborated by three
independent primary sources that agree exactly:

- **Git tag** `v1.0.2` at commit `e603d99`, dated **2020-04-28**.
- **PyPI**: `pyzenodo3` `info.version` is `1.0.2`; its earliest file upload is `2020-04-28T05:03:19Z`.
- **Zenodo**: deposit 3772154, `metadata.version` `v1.0.2`, publication date 2020-04-28, DOI
  `10.5281/zenodo.3772154` — matching the stored `version_pid` exactly.

**Form.** Stored unprefixed as `1.0.2`. The `v` prefix appears in the git tag and in Zenodo's
`metadata.version` (`v1.0.2`), but PyPI's canonical form is unprefixed and the catalogue stores it that
way. Do not read the entry's rendered display, which prefixes the software name (`PyZenodo - 1.0.2`), as
the stored value.

**The version anomaly, and which source was taken.** The pinned `setup.cfg` declares:

```
version = 1.1.0
```

which is *newer* than everything published. Establishing its shape: the bump to `1.1.0` happened **in the
pin commit itself** — `09bdb3f` (2021-04-27, "python -m cli") changed `version = 1.0.2` to
`version = 1.1.0` — and that commit is the last on `main`. Tracing every version line through
`setup.cfg`'s history, every earlier bump but one (`0.1.0`→`0.1.1`, `0.1.2`→`1.0.0`,
`1.0.0`→`1.0.1`, `1.0.1`→`1.0.2`) was followed by a tag and a PyPI upload. The single exception
strengthens this reading rather than weakening it: `0.1.1`→`0.1.2`, set at `ff2a22d` (2019-02-18), was
never tagged and never uploaded — there is no `v0.1.2` tag and no `0.1.2` key in PyPI's `releases` map
— so a version string bumped in-tree and then left behind already has a precedent in this repository.
`1.1.0` is the same shape: there is no `v1.1.0` tag (the repository has six tags — `v0.1.1`,
`v.0.3.0`, `v0.3.1`, `v1.0.0`, `v1.0.1`, `v1.0.2` — and none is `v1.1.0`), no `1.1.0` key in PyPI's
`releases` map, and no fifth Zenodo deposit.

So this is the **"bumped in-tree, never released"** shape: a development version-string set in the same
commit that made the last change, after which work stopped. It is not evidence of an unrecorded release.
`1.0.2` is taken because Field 12 records a *published* release with a date and a DOI, and `1.1.0` has
none of the three. A future refresh that sees `1.1.0` in `setup.cfg` should reach this same conclusion
rather than treating the catalogue as stale.

**The version description, classified clause by clause.** `git merge-base --is-ancestor v1.0.1 v1.0.2`
is true, so `v1.0.1..v1.0.2` is a genuine range — **7 commits**. Testing each clause of the stored
description against it:

| clause | classification |
|---|---|
| "Added `upload_zenodo.py --use-sandbox` flag to avoid cluttering Zenodo with test uploads (thanks to @kasbah)." | **Attributable.** A light declarative rewrite of the v1.0.2 GitHub release body's own words, "thanks to @kasbah for adding `upload_zenodo.py --use-sandbox` flag to avoid cluttering Zenodo with test uploads", and backed by commit `1c63c64` in the range. |
| "Moved package to src/ layout." | **Attributable.** Verbatim in substance from the same release body ("Moved package to src/ layout") and backed by commit `5352036` "src/ layout" in the range. |

Both clauses are attributable to the correct release's own release notes, with a matching commit each.
Nothing is inherited from an earlier tag and nothing is unattributable, so the description is left
unchanged.

**One nuance worth preserving.** The description names `upload_zenodo.py`, a file that **no longer exists
at the pin** — the pin commit deleted it, folding its CLI into `src/pyzenodo3/upload.py` as
`python -m pyzenodo3.upload`. It *did* exist at the `v1.0.2` tag, so the description is correct for the
release it describes. A future agent should not "fix" the filename against the pinned tree.

**Other tags on the pin lineage**, for context (all reachable from the pin; not proposed as Field 12
entries, which records the current release):

| tag | commit | date | GitHub release name |
|---|---|---|---|
| `v1.0.1` | `731aea9` | 2019-11-11 | `modernize packaging, move CI to Github actions` |
| `v1.0.0` | `51043be` | 2019-06-05 | `initial release` |
| `v0.3.1` | `bde1610` | 2019-06-05 | (no release object) |
| `v.0.3.0` | `bde1610` | 2019-06-05 | (no release object; same commit as `v0.3.1`, and note the stray dot in the tag name) |
| `v0.1.1` | `3859bdc` | 2018-06-26 | `Update Zenodo API` |

**The choice between `1.0.2` and `1.1.0`, settled.** `1.0.2`, dated 2020-04-28, with version PID
`https://doi.org/10.5281/zenodo.3772154`, is the recorded value — the only one of the two that was ever
tagged, uploaded to PyPI and assigned a DOI. `1.1.0` was put seriously, on the strength of being the
source tree's own declaration at the pin, which is genuine evidence about the code and is set out
above rather than dismissed. It was not taken because Field 12 records a *published* release: `1.1.0`
has no release date and no version PID, so selecting it would have meant clearing both companion
sub-fields in exchange for a version string that was never released.

---

### 13. Programming Language (RECOMMENDED)

- **Python 3.x**

**Source:** Carried over from the existing HSSI record and confirmed at the pin. `setup.cfg` declares
`python_requires = >= 3.6` and the classifier `Programming Language :: Python :: 3`; PyPI reports
`requires_python: >=3.6`. Every tracked source file is Python. `Python 2.x` is affirmatively excluded —
`base.py` and `upload.py` both open with `from __future__ import annotations` and use PEP 585 generics
(`list[dict]`, `dict[str, str]`) and PEP 604 unions (`str | Path`), none of which parse under Python 2.
The Python-3-only character of the package is the reason for the `3` in its distribution name (Field 6).

---

### 14. Reference Publication (OPTIONAL)

- **Reference Publication:** Not found

**Source:** No publication describes this software. There is no JOSS paper, no `paper.md` or `paper.bib`
in the tracked tree, and no publication DOI in `CITATION` (which holds a Zenodo software DOI — see
Field 2), in `setup.cfg`, or in the README. All four Zenodo deposits have `resource_type` software with no
`isDescribedBy` or `cites` relation to any article; their only related identifier is the `isSupplementTo`
link back to the GitHub tag. Recorded as negative research so a later refresh does not repeat the search.

---

### 15. License (RECOMMENDED)

- **License:** Apache License 2.0

**Source:** The repository's own `LICENSE.txt` at the pin — 201 lines, opening

```
                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/
```

GitHub's repository API independently reports `license.spdx_id: Apache-2.0`. `setup.cfg` at the pin
declares `license_files = LICENSE.txt`. An explicit `license = Apache 2.0` key was also present from the
second commit (`eeb6a3c`, 2018-06-24) and was removed at `538b415` (2018-07-02); the pointer to the
licence file has been there continuously since that same second commit, first as `license_file = LICENSE`
and, from `8abe8ae` (2019-10-02), as `license_files`. So the verbatim licence text is now the sole in-tree
declaration, and it has never changed.

`Apache License 2.0` is written byte-for-byte as it appears in the live `License` vocabulary, which has
11 rows: `Apache License 2.0`, `BSD 2-Clause "Simplified" License`, `BSD 3-Clause "New" or "Revised"
License`, `Creative Commons Attribution 4.0 International`, `GNU General Public Licenses (GPL version 2)`,
`GNU General Public License v3.0 or later`, `GNU Lesser General Public License v3.0 only`, `GNU Library or
‘Lesser’ General Public Licenses (LGPL version 2)`, `MIT License`, `Other`, `Restricted`. The first row is
an exact match, so no `Other` fallback is needed.

There is no storable licence URI: the licence is a foreign key to a shared row that carries its own URL,
so the software record has no per-software URI field. `https://www.apache.org/licenses/LICENSE-2.0` is
cited here only as corroborating evidence, never as a value to propose.

**Never relicensed.** Reading the licence file's *content* at every commit that touches the path (not
merely tracing added files) shows Apache-2.0 at the initial commit `0a6ac35` (2018-06-24) and unchanged
since. The only other event on the path is the pure rename `LICENSE` → `LICENSE.txt` at `8abe8ae`
(2019-10-02), which git records as `R100` — a 100 % similarity rename, i.e. not one byte of text changed.

**Why this differs from its siblings, and why that is not a mistake.** Other `space-physics` repositories
are MIT-licensed, so an agent comparing across the family will be tempted to "correct" this one. Do not.
The Apache-2.0 licence is **inherited from Tom Klaver's `pyzenodo`**, the package this one is a Python-3
port of (full evidence under Field 6): Klaver's repository is Apache-2.0 on GitHub and his PyPI
distribution declares `license: Apache 2.0`. The inheritance is visible in the commit order — the Apache
licence text lands in commit 1 and `license = Apache 2.0` in commit 2, both **before** the ported code
arrives in commit 3. The licence, the Klaver author credit, and the `3` in the package name all have this
one cause.

**A divergence to document, not to resolve toward Zenodo.** All four Zenodo deposits record
`license: {"id": "other-open"}` — not `apache-2.0`. This is the well-known DOI-autofill error class in
which a deposit's own metadata is copied forward uncritically; Zenodo's GitHub integration frequently
fails to map a repository licence and falls back to `other-open`. The repository is the authoritative
source for its own licence terms, and it says Apache-2.0 unambiguously in a 201-line verbatim licence
text. A future refresh reading the Zenodo record should not "correct" this field to `Other`.

HSSI held no value for this field before this refresh, so recording it fills a genuine gap
rather than changing a curated decision.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- json
- open data
- zenodo

**Source:** All three are carried over from the existing HSSI record, **lowercase as stored**. The
entry's rendered view title-cases keywords (`Json`, `Open Data`, …); that is a display transform, and
the title-cased forms must never be copied back as values. Each of the three has direct evidence in
the software's own metadata:

| keyword | evidenced by |
|---|---|
| `zenodo` | `setup.cfg` `keywords` block at the pin; also a GitHub repository topic |
| `open data` | `setup.cfg` `keywords` block at the pin |
| `json` | GitHub repository topic (`topics: ['json', 'zenodo']`) |

**Three PyHC facet keywords were dropped in this refresh.** Before this refresh the record also carried
`ionosphere_thermosphere_mesosphere`, `magnetosphere` and `solar`. None had any evidence in the
software: their sole source was the PyHC registry entry in `_data/projects_unevaluated.yml`, lines
123–127, whose `keywords:` list is
`["ionosphere_thermosphere_mesosphere","magnetosphere","solar","specific"]`. The fourth of those,
`specific`, is a PyHC browse facet meaning "domain-specific" rather than a subject term and was
correctly never stored. (`_data/projects.yml` and `_data/projects_core.yml` both fetch successfully and
contain zero `pyzenodo` hits, so the unevaluated list is the right one to cite.)

**Why they were dropped.** PyZenodo is a REST client for a general-purpose research-data repository —
it works identically for a solar-physics dataset, a linguistics corpus and a protein structure. The
word-anchored sweep recorded under Fields 31/32 finds **zero** heliophysics terms in any tracked file
at the pin, and neither `setup.cfg`, the README, PyPI, nor any of the four Zenodo deposits mentions
the ionosphere, the magnetosphere or the Sun. A searcher who filters HSSI on `magnetosphere` is asking
for software that has something to do with the magnetosphere.

**The case for keeping them, which was real and lost on judgement rather than on fact.** They come
from PyHC's curated registry, which this workflow treats as its most trustworthy source; they are how
PyHC's own faceted browse reaches this package; and a broad keyword that widens discovery costs an
individual searcher little. That is a genuine discoverability argument and it was weighed, not
dismissed. It did not prevail because facet tags of this kind propagate widely across registries and
are frequently unsupported by the software they are attached to, and because a domain keyword on a
domain-independent tool spends the precision of everyone who searches that keyword in order to buy one
route into this entry. The PyHC provenance itself is not in dispute and is recorded above, so a later
refresh recognises these tags on sight instead of rediscovering them as fresh evidence.

**Decided together with Field 5, and not to be reopened separately.** These three keywords and the
three regions cleared in Field 5 descend from the same four PyHC registry facet tags seen through two
fields. They were adjudicated as a single judgement about those tags.

---

### 17. Data Sources (OPTIONAL)

- **Other**

**Source:** Carried over from the existing HSSI record. The software's one data source is the Zenodo REST
API (`BASE_URL = "https://zenodo.org/api/"` in `base.py`, and `https://sandbox.zenodo.org/api` under
`--use-sandbox`).

`Other` is correct because Zenodo is genuinely absent from the vocabulary. The live `DataInput` list has
17 rows in full — `AMDA`, `CDAWeb`, `das2`, `FTP/FTPS Directories`, `GFZ`, `HAPI`,
`HTTP/HTTPS Directories`, `Madrigal`, `Observatory/Mission-specific`, `OMNIWeb`, `Other`, `S3/Cloud-aware`,
`SSCWeb`, `TAP`, `The Virtual Solar Observatory.`, `VirES`, `WDC` — and every named row is either a
heliophysics archive or a data-access protocol. None denotes a general-purpose research-data
repository. The enumeration is recorded here as the reason the value is `Other`, so a future refresh
can see the gap rather than re-deriving it.

**Considered and rejected: `HTTP/HTTPS Directories`.** Superficially attractive since all access is over
HTTPS, but that row denotes browsable directory listings served over HTTP, which is a different access
pattern from a JSON REST API with query parameters and a token-authenticated deposition endpoint. Choosing
it would mislead a searcher filtering for bulk directory retrieval.

**Also considered and rejected:** `Observatory/Mission-specific` (Zenodo belongs to no observatory or
mission), `S3/Cloud-aware` (no object-store access anywhere in the tree), and `HAPI`/`TAP`/`das2` (none of
those protocols is implemented).

---

### 18. Input File Formats (RECOMMENDED)

- **Other**

**Source:** Carried over from the existing HSSI record. The only file format the package parses is the
`.ini` deposit-metadata file consumed by `upload.meta()` via `ConfigParser` — the example fixture is
`src/pyzenodo3/tests/meta.ini`, whose whole content is a `[zenodo]` section with `author`, `title` and
`description` keys. Payload files handed to `upload_data()` are opened in binary and streamed to Zenodo
untouched, so they are passed through rather than read as a format.

`Other` is correct against the 11-row live `FileFormat` vocabulary — `ascii`, `CDF`, `csv`, `FITS`,
`HDF5`, `IDL.sav`, `ISTP-Compliant`, `JSON`, `netCDF3/4`, `Other`, `Zarr` — which contains no INI or
config-file row. Every scientific format in that list is affirmatively absent from the tree: nothing
imports `astropy.io.fits`, `cdflib`, `h5py`, `netCDF4` or `zarr`, and there is no CSV or ASCII table
reader.

**Two candidate additions were considered in this refresh and not made.** Both rest on real code
facts, recorded here so a later refresh recognises them as already weighed.
- **`JSON`.** `upload.upload_meta()` reads the generated metadata file back off disk
  (`meta = metafn.read_text()`) before PUT-ing it to Zenodo, so a JSON file *is* an input on that
  path. Two things weighed against it. The file is one the package itself has just written, so nothing
  external is being ingested; and `upload_meta()` is not called by `upload()` at the pin — the call is
  present but commented out (`# upload_meta(token, metafn, depid)`), the known cause of open issue #4,
  "Meta info upload doesn't work" (2020-04-10). It remains a public function a caller can invoke
  directly, which is what made the candidate genuine rather than idle.
- **`ascii`.** An `.ini` file is plain ASCII text, so the row is literally true of it. It was not taken
  because in this vocabulary `ascii` sits among scientific data formats and signals ASCII *data
  tables*: a searcher filtering on it wants readable data files, not a three-key config stanza.

`Other` alone is the settled value — the narrowest reading, and the one that does not overstate what
the package ingests.

---

### 19. Output File Formats (RECOMMENDED)

- **JSON**

**Source:** `JSON` is carried over from the existing HSSI record and is squarely evidenced:
`upload.meta()` builds a `dict`, serialises it with `json.dumps(Meta, indent="\t")`, and writes it to
`inifn.with_suffix(".json")` — a real JSON file on disk. Separately, every `base.py` retrieval method
returns the parsed JSON payload of a Zenodo API response.

**`Other` was removed in this refresh.** Before this refresh the field carried `JSON` and `Other`
together. An earlier dossier glossed `JSON` as "API responses" and `Other` as "metadata JSON files
generated from `.ini` upload metadata" — but both of those things are JSON, so on that reading
`Other` named nothing distinct. Searching the pinned tree for any other write path: the only file
the package creates is `outfn.write_text(json_meta)` in `upload.meta()`. There is no other
serialiser, no other writer, and no binary output.

**The case for keeping `Other`, which was weighed and did not prevail.** The package *transmits*
arbitrary user files to Zenodo through `upload_data()`, and the formats of those files are entirely
unconstrained — a user may hand it a FITS cube, a CSV or a tarball, so in a plain sense files of
unlisted formats do leave the machine because of this software. That reading lost to the distinction
that transmitting a file is not authoring a format: the bytes are opened in binary and streamed
through untouched, and the package neither produces nor understands them. Reducing to `JSON` alone also
keeps Field 19 consistent with Field 18's settled reading that pass-through payloads are not a format
the software handles.

---

### 20. Operating System (RECOMMENDED)

- **Linux**
- **Mac**
- **Operating System Independent**
- **Windows**

**Source:** Carried over from the existing HSSI record; all four names are byte-exact rows in the live
7-row `OperatingSystem` vocabulary. Doubly evidenced:

- **CI at the pin** (`.github/workflows/ci.yml`) has two jobs: `linux` running on `ubuntu-latest` (lint,
  type-check and tests), and `integration` running a matrix `os: [windows-latest, macos-latest]` (tests).
  So all three named platforms are actually exercised, not merely claimed.
- **Declared portability**: `setup.cfg` at the pin carries the classifier
  `Operating System :: OS Independent`, which PyPI also reports for the released `1.0.2`. The package is
  pure Python with no compiled extensions and no platform-specific imports; paths are handled through
  `pathlib`.

Listing both the three concrete platforms and `Operating System Independent` is intentional and not
redundant: the concrete rows record where the project *tests*, and the independence row records the
maintainer's own portability claim. A searcher filtering for either will find it.

Superseded from the earlier dossier: it wrote this value as `OS Independent`, which is not a row in the
vocabulary. The correct row name is `Operating System Independent`, and the catalogue already stores it
correctly.

Two legacy CI configurations, `archive/.travis.yml` and `archive/.appveyor.yml`, remain in the tree at the
pin. They were moved into `archive/` at `8abe8ae` rather than deleted, are not run by anything, and are
not used as evidence here.

---

### 21. CPU Architecture (RECOMMENDED)

- **CPU Independent**

**Source:** Carried over from the existing HSSI record; byte-exact against the live 9-row
`CpuArchitecture` vocabulary. The package is pure Python with no compiled extensions: `setup.cfg` declares
no `ext_modules`, there is no build backend beyond setuptools, no C/Fortran/Cython source exists in the
tree, and PyPI distributes it as a pure-Python wheel. Its runtime work is HTTP requests and string
handling, so nothing binds it to an instruction set. The CI matrix runs it on GitHub's Linux, Windows and
macOS runners without any per-architecture handling.

`x86-64`, `Apple Silicon arm64`, `Linux aarch64 or arm64`, `GPU`, `HPC or HEC`, `ppc64le` and
`Sun (SPARC)` are all affirmatively wrong here — selecting any of them would imply a build or performance
characteristic the package does not have.

---

### 22. Related Phenomena (OPTIONAL)

- **Not found**

**Source:** Evidenced-empty. The live `Phenomena` vocabulary has exactly 7 rows — `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`,
`X-ray emission` — and none of them has any connection to a Zenodo REST client. This enumeration is
recorded as the *reason* the field is correctly empty, so a later refresh can see that the vocabulary was
weighed rather than skipped. The word-anchored sweep under Fields 31/32 independently confirms that no
physical phenomenon is named anywhere in the tracked tree.

---

### 23. Development Status (RECOMMENDED)

- **Inactive**

**Source:** Selected against the live `RepoStatus` vocabulary, whose rows — unusually among HSSI's
controlled lists — carry real definitions, quoted below rather than paraphrased.

**The evidence.**
- Last commit on `main`: `09bdb3f`, **2021-04-27**, which is also the pinned revision and equals
  `refs/heads/main` on origin.
- Last release: **v1.0.2, 2020-04-28**. No release, tag, or PyPI upload since.
- Declared maturity: `setup.cfg` at the pin carries `Development Status :: 4 - Beta`, and PyPI reports the
  same classifier for the released `1.0.2`. It was raised from `Development Status :: 3- Alpha`, which the
  second commit set in 2018.
- The repository is **not archived** (`archived: false`) and not disabled.
- **4 open issues**: #4 "Meta info upload doesn't work" (2020-04-10), #5 "Download all files from record"
  (2020-05-23), #6 "Uploading to existing Zenodo REPO" (2020-07-17), #7 "ConnectionError
  \"WSAECONNRESET\" when uploading a 1GB ZIP: " (2020-07-17).
- **3 open pull requests**, all from outside contributors: #8 "Pass kwargs to search parameters to enable
  better control" (2021-08-12), #9 "Adding support to download the Files " (2023-04-10), #11 "Metadata
  upload update" (2023-07-27).
- Two of those titles end in characters that transcription tends to swallow, and are quoted verbatim above:
  issue #7 ends in a colon followed by a space, and pull request #9 ends in a space. A future refresh
  comparing these strings against the upstream titles should expect them, not "correct" them away.
- GitHub's `open_issues_count: 7` counts issues and pull requests together; the split above comes from
  separating the open-issues list on the `pull_request` key. A future agent should not read 7 as seven
  bug reports.

**Why `Inactive` rather than the alternatives.** The vocabulary defines it as:

> The project has reached a stable, usable state but is no longer being actively developed;
> support/maintenance will be provided as time allows.

Both halves fit. The project reached a stable, usable state — five PyPI releases, four archived Zenodo
deposits, a 1.x version line, and a Beta maturity classifier. And it is no longer actively developed —
no commit since 2021-04-27 and no release since 2020-04-28. Those two dates are the whole basis of the
claim, and are stated as dates rather than as an elapsed span so the sentence cannot go stale; a
future refresh should re-anchor to newer dates if any appear, not convert these back into years.

**Engaging the open issues and unmerged pull requests, which are the strongest argument for a different
value.** Community PRs sitting unmerged since 2021 and 2023, and issues unanswered since 2020, are real
evidence that maintenance is not in fact being provided. That points at:

> **Unsupported** — The project has reached a stable, usable state but the author(s) have ceased all work
> on it. A new maintainer may be desired.

`Unsupported` was considered seriously and **not** selected, for three reasons. First, it asserts
something about the author's *intent* — that work has ceased — and no primary source says so: there is no
deprecation notice, no "unmaintained" banner in the README, no archive, and no statement anywhere in the
repository. Second, `Inactive`'s "support/maintenance will be provided as time allows" is a permissive
claim that unmerged PRs do not falsify; it is not a promise of responsiveness. Third, the row's closing
sentence is "A new maintainer may be desired" — and the *may* there (emphasis added; the stored definition
carries none) is a conditional that must not be read as a statement that one *is* desired, which is the
only reading that would make it fit here.

**Also considered and rejected.**
- `Abandoned` — its definition begins "Initial development has started, but there has not yet been a
  stable, usable release", which is factually false here: there are five releases and four DOIs.
- `Suspended` and `WIP` — both are defined by the same "there has not yet been a stable, usable release"
  precondition, so both are excluded for the same reason.
- `Active` — "being actively developed" is contradicted by the commit and release history.
- `Concept` — the repository is neither minimal nor a demo.
- `Moved` — nothing has moved. The 2019 `scivision` → `space-physics` organisation rename is a rename of
  the owning organisation, visible in the older Zenodo deposits, not a relocation of the project to a new
  authoritative home; `space-physics/pyzenodo3` remains the live repository.
- The "archived implies Unsupported" shortcut does not apply, because this repository is not archived.

HSSI held no value for this field before this refresh.

---

### 24. Documentation (RECOMMENDED)

- **Documentation URL:** https://github.com/space-physics/pyzenodo3

**Source:** Carried over from the existing HSSI record. The README **is** the documentation: at the pin it
carries the install instructions, a worked upload walkthrough (obtain a `deposit:write` API token, write a
`mymeta.ini`, run the CLI with `--use-sandbox`), and two usage examples for finding records by GitHub repo
and by GitHub username. `search_zenodo.py` at the repository root is a second, runnable example.
`setup.cfg` declares `long_description = file: README.md`, so the README is also what PyPI renders.

There is no separate documentation site. The tracked tree at the pin contains **19** files and no `docs/`
directory, no `mkdocs.yml`, no Sphinx `conf.py`, and no ReadTheDocs configuration.

**There is also no wiki**, despite appearances. GitHub's API reports `has_wiki: true` for this repository,
which is only the setting's default and proves nothing about content; a wiki lives in a separate git
repository, and `git ls-remote https://github.com/space-physics/pyzenodo3.wiki.git` answers
`remote: Repository not found.` Recorded so a future refresh does not chase the `has_wiki` flag.

Pointing Field 24 at the repository URL therefore duplicates Field 3 by necessity rather than by
oversight — the repository landing page genuinely is where a user reads the documentation.

---

### 25. Funder (OPTIONAL)

- **Not found**

**Source:** Negative research. No funding statement exists in any tracked file at the pin, in any of the
four Zenodo deposits (none carries a `grants` entry), on PyPI, or in the PyHC registry entry. There is no
paper whose acknowledgements could be consulted (Field 14). A `.github/FUNDING.yml` file existed earlier
in the repository's history but was **deleted at the pin commit**, and a GitHub Sponsors link is a
donation channel rather than a research funder in any case.

Tom Klaver's 2017 PyPI email domain (`esciencecenter.nl`) hints at institutional support for the
*predecessor* package, but that is an employer inference about a different package and is not evidence
that any organisation funded this work. Not recorded.

---

### 26. Award Title (OPTIONAL)

- **Not found**

**Source:** No award, grant number, or programme is named anywhere in the repository, the Zenodo deposits,
PyPI, or the PyHC registry. Consistent with Field 25 — with no funder identified, there is no award to
attach to one.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- **Not found**

**Source:** Negative research. No article describes, cites, or uses this software in a way this refresh
could evidence. The repository names no publication; the four Zenodo deposits carry no citation relations
beyond `isSupplementTo` back to their own GitHub tags; and `CITATION` holds a software DOI, not a paper.
Recorded so a later refresh does not repeat the search from scratch.

---

### 28. Related Datasets (OPTIONAL)

- **Not found**

**Source:** The software is a general client for a repository that hosts millions of unrelated records; it
has no privileged relationship with any particular dataset. An earlier dossier called the field not
applicable on the grounds that the tool provides access to any dataset hosted on Zenodo, which is the
right reasoning: naming any individual Zenodo dataset here would misrepresent a general-purpose tool as
dataset-specific, and there is no principled way to choose one. The LOWTRAN record used as a search
argument in the README and in `search_zenodo.py` is a documentation example, not a supported dataset —
see the Field 29 verdict on LOWTRAN for the same reasoning applied to the software relation.

---

### 29. Related Software (OPTIONAL)

- https://github.com/zenodo/zenodo
- https://github.com/Tommos0/pyzenodo
- https://github.com/lgloege/zenodopy
- https://github.com/dvolgyes/zenodo_get

**What this refresh changed.** Before this refresh the record held three entries:
`https://github.com/psf/requests`, `https://www.crummy.com/software/BeautifulSoup/` and
`https://github.com/zenodo/zenodo`. The first two were removed, the third kept, and three entries were
added. Each of the six determinations is set out below with its reason.

**The two removals are the rule applied, not curator taste.** The field's own definition excludes both
by name and by test.

- **`https://github.com/psf/requests`** — `requests` is enumerated in the Tier A list at
  `resource_submission_form_fields.md` line 690, headed "**Never list these (Tier A), no exceptions:**",
  and again in Field 29's own exclusion list at line 677, which states that the generic scientific-Python
  stack "**is excluded here too**" and names `requests` among the packages that "are not related software,
  because listing them says nothing that isn't equally true of most of the ecosystem." Being a dependency
  is not a relation. Removal is the rule applied.
- **`https://www.crummy.com/software/BeautifulSoup/`** — `beautifulsoup4` is not enumerated, so the doc's
  own unnamed-package test at line 692 governs: "**would this package be equally at home in a web app, a
  finance model, or a biology pipeline?**" An HTML parser plainly would be — it is generic I/O plumbing, and it is
  used here only to scrape Zenodo's version table in `Record.get_versions_from_webpage()`. It therefore
  "gets Tier A treatment whether or not it appears in the list." Line 698 additionally forecloses the
  obvious escape hatch: a package rejected under Tier A does not relocate into Field 29. Removal is the
  rule applied. (Separately, the removed value was a project page rather than a repository URL, which
  the field permits — that was not why it went.)

**The incumbent that stays.** `https://github.com/zenodo/zenodo` is not a Python dependency at all; it is
the **server this client exists to talk to**, hard-coded as `BASE_URL = "https://zenodo.org/api/"` in
`base.py`. It passes the doc's information test decisively: the entry would be false of essentially every
other package in the catalogue, so it carries real information. From the searcher's side, a reader who
lands on PyZenodo and wants to know what it actually connects to is served by exactly this link. Kept.

**The three additions, each a judgement made on its own evidence rather than a rule applied.**

- **`https://github.com/Tommos0/pyzenodo` — added.** This is the package PyZenodo3 was derived from, and
  line 675 states plainly that "Important software dependencies and software this work was forked from
  should also be included." The forked-from clause is the one that governs here. It is not a GitHub fork
  in the mechanical sense (`fork: false` on both repositories), but it is a derivation in the sense the
  sentence means: the two modules define exactly the same 14 classes and functions with none unique to
  either side, and five distinctive strings appear once in each file byte-identical, against a negative
  control that separates them (full evidence under
  Field 6). This is the single most distinguishing relation this software has, and it is also what makes
  the Apache-2.0 licence (Field 15) and the Klaver author credit (Field 6) intelligible. Before this
  refresh the catalogue recorded the relation nowhere, so the entry closed a real gap.
  `https://github.com/Tommos0/pyzenodo` resolves, and at 35 characters is far inside the
  128-character `RelatedItem.name` cap.
- **`https://github.com/lgloege/zenodopy` — added.** A peer Zenodo client (PyPI `zenodopy` 0.3.0, "manage
  zenodo project", by Luke Gloege). This is the field's core case — "Software that performs similar tasks
  but does not necessarily link together" — and from the searcher's side someone evaluating Python
  options for scripting Zenodo is materially helped by seeing the alternatives side by side. Resolves;
  35 characters. The peer-client case is a judgement about what helps a reader evaluating options, not
  a relation the field definition compels; it was made deliberately and applies equally to the entry
  below.
- **`https://github.com/dvolgyes/zenodo_get` — added.** A peer Zenodo client (PyPI `zenodo-get` 3.1.0,
  "Zenodo_get - a downloader for Zenodo records", by David Völgyes). Same "similar tasks" case, with an
  extra reason specific to this entry: PyZenodo has no download capability at the pin (Field 8), and open
  PR #9 exists to add it, so a reader who needs Zenodo downloads today is genuinely better served knowing
  this exists. Resolves; 38 characters.

**Considered and rejected — record this so it is not re-proposed.**

- **`https://github.com/space-physics/lowtran`** — the strongest-looking candidate, and the wrong one.
  LOWTRAN is in the HSSI catalogue, shares an author with PyZenodo, and is named in this package's own
  code and documentation: `search_zenodo.py` calls
  `zen.find_record_by_github_repo("scivision/lowtran")` and the README shows the same call (with a
  double-underscore typo, `find_record__by_github_repo`, that does not match the real method name).
  But that is an **example argument** — an arbitrary repository chosen to demonstrate a search — not a
  relation. LOWTRAN performs no similar task (it is an atmospheric transmission model), PyZenodo is not
  derived from it, neither depends on the other, and they are not companion packages. The Field 29 test
  is whether the entry "tells a reader something about **this** software"; a demo argument tells a reader
  only that a demo needed a repository name. Rejected. *(If a later decision reverses this, the correct
  URL is LOWTRAN's exact stored code repository value, `https://github.com/space-physics/lowtran`, since
  the page renders a related item's raw URL as its link text and a repository URL is legible where a DOI
  is opaque. Should HSSI ever render resolved titles instead, a DOI would become the better choice on
  persistence grounds.)*
- **`pytest`, `flake8`, `flake8-bugbear`, `flake8-builtins`, `flake8-blind-except`, `mypy`** — the
  `tests` and `lint` extras in `setup.cfg`. `pytest` is enumerated in Tier A; the rest are linters and a
  type checker, which are testing and tooling infrastructure and fail the "equally at home in a web app,
  a finance model, or a biology pipeline" test outright. None is related software.
- **PyHC packages generally** — the doc names "a PyHC member, so it interoperates with PyHC packages" as
  one of two justifications that are "**never** sufficient on their own". PyZenodo's presence in the PyHC
  unevaluated registry establishes no relation to any particular PyHC package.

**A narrower set was available and was not taken.** Applying the two removals and adding only
`Tommos0/pyzenodo` — the one addition the field definition explicitly calls for, under "software this
work was forked from" — would have been the conservative outcome, leaving the peer-client judgement
aside. It was rejected because a reader arriving at a small, inactive Zenodo client is served by
knowing what the live alternatives are, and because `zenodo_get` in particular covers the download
capability this package lacks. Applying the removals alone, or adding without removing, were both
rejected outright: the latter would retain two entries the field definition excludes by name and by
test.

**Field mechanics worth carrying forward.** Fields 29 and 30 store the same related-item type, so
moving an entry between them requires no change of type. All four recorded URLs resolve and all are far
inside the 128-character name cap (32, 35, 35 and 38 characters) — note the cap here is 128, not the
200 that applies to plain URL fields elsewhere in the record.

---

### 30. Interoperable Software (OPTIONAL)

- **Not found**

**Source:** Empty in the existing HSSI record and correctly so; re-tested rather than assumed.

The bar is a *demonstrated exchange* — a shared or converted data model, one package's output imported
into another, an adapter or converter API, a plugin relationship, a companion package, or a bridge to a
named domain tool. Nothing in the pinned tree meets it. PyZenodo's public surface returns plain Python
`dict`s wrapped in its own `Record` class and writes plain JSON; it defines no converter to any other
package's data model, ships no plugin interface, and has no companion package.

**The Tier A dependencies do not qualify** — `requests` is named in Tier A at line 690, and
`beautifulsoup4` fails the "equally at home in a web app, a finance model, or a biology pipeline" test as
generic infrastructure. "Being a dependency is not interoperability."

**There is no Tier B package to test.** `astropy`, `xarray`, `cdflib`, `h5py`, `netCDF4`, `dask`, MATLAB
and Jupyter are all absent from the tree. A case-insensitive sweep of the pinned tree for any of them,
plus `numpy` and `pandas`, matches exactly **one file**: `.gitignore` line 75, `# Jupyter Notebook`. That
is a section heading in the standard GitHub Python `.gitignore` template, introducing the
`.ipynb_checkpoints` pattern on the next line — not a dependency, not an import, and not a use of Jupyter
of any kind. It is a false positive of the same shape as the `permissions`/`Submission` substring artifact
recorded under Field 31, and is noted here so a future refresh recognises the hit instead of reading it as
evidence. With that hit discounted,
the Tier B question does not arise here: there is no package whose exchange could be evidenced or found
wanting.

Two blanket claims are recorded as explicitly rejected, since both would otherwise be tempting for a tool
whose whole purpose is moving data around: that PyZenodo is "part of the standard scientific Python
ecosystem", and that PyHC membership implies interoperation with PyHC packages. The field definition names
both as never sufficient on their own. Retrieving a file that some *other* package might later read is not
interoperability between the two packages.

---

### 31. Related Instruments (OPTIONAL)

- **Not found**

**Source:** Evidenced-empty. PyZenodo is instrument-agnostic by construction: it is a client for a
general-purpose research-data repository and supports no instrument specifically, which is precisely the
case the field's relevance gate excludes ("general models/utilities/frameworks support none
specifically"). A user searching HSSI for any `instrument:"X"` would not expect a Zenodo API wrapper back,
and someone working with any instrument's data would not reach for it as an instrument tool.

**The sweep, with its pattern, engine and case-sensitivity published so it can be reproduced.** Run over
the pinned revision, case-insensitive (`-i`), Perl-compatible engine (`-P`):

```
git grep -P -in '\b(msis|radar|observatory|observatories|satellite|magnetometer|instrument|spacecraft|mission|telescope)\b' 09bdb3f9f0ac9961f74220a21ca6d4fd666e198a
```

returns **zero** matches (exit status 1).

**The substring artifact this replaces, recorded because it will otherwise be rediscovered as a false
positive.** The same pattern *without* word anchors returns **6 lines in 2 files**: `LICENSE.txt` lines
24, 130, 138, 151 and 200, and `src/pyzenodo3/upload.py` line 145. Every one of the six is the letter
sequence `mission` inside `permission(s)` or `Submission` — five in the Apache licence's own boilerplate
("exercising permissions granted by this License", "5. Submission of Contributions", and so on) and one
in the source comment `# %% Create new submission`. Not one is a heliophysics mission.

**Engine caveat, which matters for reproducing this.** `git grep -E` treats `\b` as a literal `b` rather
than a word boundary, and so fails **silently toward zero** — a convincing-looking empty result that
proves nothing. Demonstrated on this same tree: `git grep -E -il '\bzenodo'` returns 0 files and
`git grep -E -il 'bzenodo'` also returns 0 files, while `git grep -P -il '\bzenodo'` returns 9 files. Use
`-P`. Positive controls on the pinned tree under `-P` confirm the instrument sweep can see what is there:
`\bzenodo\b` returns 41 lines and `\brequests\b` returns 15 lines.

**Vocabulary side.** The controlled `InstrumentObservatory` list was also searched from the other
direction, case-insensitively across the row `name`, `abbreviation`, `identifier` and `definition`
columns: `zenodo`, `data repository`, `open data`, `json` and `rest api` each return **0** rows. So the
emptiness is symmetric — nothing in the software names an instrument, and nothing in the vocabulary names
this software's subject. No entry reaches the resolution ladder, so no ambiguous or unresolvable entry is
being quietly dropped.

---

### 32. Related Observatories (OPTIONAL)

- **Not found**

**Source:** Evidenced-empty, on exactly the same evidence as Field 31 — the sweep covers observatory terms
(`observatory`, `observatories`, `satellite`, `spacecraft`, `mission`) in the same anchored pattern and
returns nothing. Zenodo is a research-data repository operated for the general research community; it is
not an observatory, not mission-specific, and not tied to any platform. No observatory-level substitution
arises, because there is no instrument entry to substitute for.

---

### 33. Logo (OPTIONAL)

- **Not found**

**Source:** Documented omission. There is **no image file of any kind** in the pinned tree:

```
git ls-tree -r --name-only 09bdb3f9f0ac9961f74220a21ca6d4fd666e198a | grep -iE '\.(png|jpg|jpeg|svg|gif|ico|webp|bmp|tif|tiff)$'
```

returns no output (exit status 1) across all 19 tracked files. The README's only images are four
service-generated status badges — a Zenodo DOI badge, a GitHub Actions build badge, a PyPI supported-versions
badge and a download-count badge — none of which is a project logo, and all of which are dynamically
rendered by third-party services rather than stored assets.

**Everywhere else checked, and empty.** The PyHC registry entry (`_data/projects_unevaluated.yml`, lines
123–127) has only `name`, `code`, `description`, `contact` and `keywords` keys — no `logo:` key, unlike
some other registry entries. None of the four Zenodo deposits carries an image asset. And there is no
wiki to hold one: `pyzenodo3.wiki.git` answers `remote: Repository not found.` (see Field 24).

No logo exists to record, and none may be invented. A documented omission is the correct outcome here.

---

## Contested questions and how they were settled

Nine field values were genuinely arguable. Each is settled, and each is argued in full under its own
field, with the evidence that lost recorded there rather than discarded. This table is a finding aid,
not a substitute for those entries, and nothing in it is open.

| Field | The question that was put | How it was settled |
|---|---|---|
| 2 Persistent Identifier | Concept DOI, or the repository's `CITATION` version DOI? | Concept DOI `https://doi.org/10.5281/zenodo.3239431`, which tracks forward to the newest deposit where the `CITATION` DOI freezes at v1.0.1 |
| 4 Software Functionality | Add `Data Processing and Analysis: File Format Conversion` for the `.ini`→JSON conversion? | Not added — what is converted is deposit metadata, not scientific data |
| 5 Related Region | Do three PyHC-derived regions belong on a general-purpose repository client? | Field cleared — the software has no region, and PyHC facet discoverability did not outweigh the precision lost to every region-filtering searcher |
| 6 Authors | Add Kaspar Emanuel, who authored one commit and is thanked by name in the release notes? | Not added — the repository's author line is an editorial statement, and a changelog thank-you is a contributor credit |
| 12 Version | Published `1.0.2`, or the source tree's unreleased `1.1.0`? | `1.0.2` with its date and DOI — `1.1.0` was never tagged, uploaded or deposited |
| 16 Keywords | Keep the three PyHC facet keywords the software does not support? | Dropped, leaving `json`, `open data` and `zenodo` — one judgement with Field 5 |
| 18 Input File Formats | Add `JSON` and/or `ascii` alongside `Other`? | `Other` alone — neither addition describes something the package ingests from outside itself |
| 19 Output File Formats | Is `Other` supported by anything the package writes? | Reduced to `JSON` — transmitting an arbitrary user file is not authoring a format |
| 29 Related Software | Two rule-mandated removals plus three candidate additions | Full set — `requests` and BeautifulSoup removed, `zenodo/zenodo` kept, the predecessor and two peer clients added |

Fields not listed here were settled at extraction, with their evidence and their rejected alternatives
recorded in place.
