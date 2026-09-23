# Field 30 — Interoperable Software

**Level:** OPTIONAL · **API:** `interoperableSoftware[]` · **Change class:** enrich-only
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.4 (name) · **Field-search code:** `interoperable`

## What it is

**Type:** Multi-entry URL (RelatedItem lookup — repository URL preferred; a DOI only when the target has no public repository. The form's tooltip says "DOI URL preferred"; the URL-form rules below supersede it.)

**What it is:** Other important software packages this software has demonstrated interoperability with. Can run package in the same environment as the others without errors.

**When to include it (relevance):** This field is about which other **high-level heliophysics/science tools** this software can actually interoperate with — **not its dependency list**. The bar is a *demonstrated exchange*: the two packages share or convert between data models, one's output can be imported into the other, there is an adapter/converter API (`to_sunpy_map()`, `from_pysat()`, `to_dataframe()`), a plugin/extension relationship, a companion package designed to be used with it, or a cross-language bridge to a named domain tool (an IDL SPEDAS or MATLAB interface). Read "can run in the same environment without errors" as presupposing that the two are **peer tools a user would deliberately combine** — it is a caveat on real interoperability, *not* the test for it. Merely sharing a Python runtime satisfies nothing.

**How to fill it:** Ideally, enter the DOI for the software code. Otherwise, link to code repository (e.g., https://github.com/sunpy/sunpy). If no public repository, enter link where users can find more information (e.g., related HSSI page). Publication DOIs should go in relatedPublications instead.

**The form's DOI preference is superseded by Field 29's URL-form rules (rules 11–13 there):** a
repository URL is recorded whenever the target has one, a DOI only when it has none.

This file holds the **single full copy of the Tier A and Tier B lists** and the generic-infrastructure test; Field 29 applies them by reference. Field 29 holds the single full copy of the URL-form rules (which URL to record for a relation); this field applies them by reference.

## Why it exists

A user who has chosen a tool wants to know what it plugs into: which other domain packages accept its
output, feed it input, or share its data model, so they can build a workflow without discovering the
connection themselves. A correct entry is a promise that the pairing works and is documented. A padded
entry — numpy, matplotlib, the dependency list — buries the one or two real partners under names that
are true of nearly every package in the catalogue, and a missing real partner hides the most useful
fact the field can carry.

## How it appears on the site

- **Detail page:** in the "Related Items" section, under an "Interoperable Software" heading, one link
  per entry. The link target is the stored identifier (the URL); the link text is the RelatedItem's
  stored `name` unless it is `UNKNOWN`, in which case the raw URL is shown. Rows created through the API
  store the URL as their name, so in practice the visible text is the raw URL.
- **Filter:** none.
- **Free-text search:** tier T4.4, matching the RelatedItem `name` — for API-created rows that is the URL
  text itself, so a repository URL is findable by the project's name and a DOI is not.
- **Field search:** `interoperable:"…"` matches `interoperable_software__name__icontains`.
- **JSON-LD:** each entry is emitted under `mentions` with `description` `interoperableSoftware`, `@id`
  and `url` set to the identifier, and `@type` taken from the RelatedItem's stored type
  (`SoftwareSourceCode` for a software-typed row).

## Rubric: include / exclude

Decide whether a package belongs **before** hunting for its DOI or repository URL. Apply the rules top
to bottom for each candidate and stop at the first rule that fires. For every package considered and
dropped, record a short note so there is an audit trail; for every package kept, the note names the
**specific evidence** (the adapter function, the doc page, the example, the test) — never "dependencies".

1. **Tier A — never list, no exceptions.** numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly,
   bokeh, requests, python-dateutil, pytest, tqdm, PyYAML, click, setuptools, and the rest of the generic
   scientific-Python/tooling stack. **Being a dependency is not interoperability.** "It directly depends
   on numpy" is true of nearly every package in HSSI, so it distinguishes nothing. No evidence
   rehabilitates a Tier A entry; a validator reports one under either field as an **ERROR** with
   `Suggested fix: remove — a dependency shared by most of the Python ecosystem is not interoperability`.
   Fires on: the package's name is in this list.

2. **Unnamed generic infrastructure gets Tier A treatment.** Tier A is a list of examples, not a closed
   list — the principle governs, not the names. Do not conclude that a package is acceptable merely
   because it is not enumerated. For any package not named in either tier, ask: **would this package be
   equally at home in a web app, a finance model, or a biology pipeline?** If yes, it is **generic
   infrastructure** — arrays, dataframes, plotting and mapping, I/O plumbing, packaging, testing, HTTP,
   logging, CLI parsing, numerical linear algebra and solvers, parallel-programming standards, file-path
   utilities — and is excluded. A genuine heliophysics/science peer tool fails that test immediately (it
   would be absurd in a finance model), so this rule does not put real domain software at risk. Fires
   on: HDF5, h5fortran, LAPACK, ScaLAPACK, MUMPS, MPI, ffilesystem, jinja2, alive_progress and their
   peers.

3. **Blanket justifications are never sufficient.** Reject by name, wherever they appear in a source
   note: *"listed as a dependency"* / *"in pyproject.toml"*, *"part of the standard scientific Python
   ecosystem"*, *"a PyHC member, so it interoperates with PyHC packages"* (ecosystem membership is not a
   demonstrated interoperation with any particular package), and *"maintained by the same organisation"*
   (a fact about governance, not about the software). General test: **if the claim would be equally true
   of most of the Python ecosystem, it carries no information about this software and does not belong.**
   Fires on: a candidate whose only support is one of these statements.

4. **Tier B — admit only on a documented package-specific exchange.** astropy, xarray, cdflib, h5py,
   netCDF4, dask, MATLAB, Jupyter and similar foundational-but-domain-adjacent packages qualify **only**
   when a specific exchange is documented in the public API, docs, examples or tests: a converter or
   adapter, a documented interchange type, a plugin registration, an extra plus a worked example — never
   on dependency presence alone. "The public API returns `xarray.Dataset` objects as its documented
   interchange format" qualifies; "uses xarray internally" does not. **A signature that accepts a generic
   type the other package also uses (`ndarray`, `DataFrame`) is not an exchange.** Also not an exchange:
   types used only inside the implementation while the documented `Args:`/`Returns:` name none of them;
   a file format the package reads through the library (record the format in Fields 18/19); "usable from
   a notebook" for Jupyter (true of essentially every Python package — a Jupyter exchange needs an
   extension, kernel, widget or rich display written for it). Fires: include when the exchange is cited;
   exclude when it is not (a validator reports an uncited Tier B entry as a **WARNING**).

5. **An inference is not a demonstration — exclude, and record it.** Two packages whose signatures happen
   to match (one returns velocity arrays, the other consumes velocity arrays, and neither names the
   other), or that can both open the same archive's files, have an *inferred* pairing, not a documented
   one. Exclude it, record the evidence for and against, and reopen only on new evidence (a doc page, an
   example, a converter), not on a re-argument of the same facts. Fires on: a pairing no documentation,
   example, test or API on either side states.

6. **No URL, no entry.** The field needs a DOI or URL a reader can follow. A genuine partner with no
   public repository, DOI or landing page — or a package named in a changelog that was never published
   (the repository 404s and a search finds nothing) — cannot be listed. Record it as negative research so
   a later refresh re-checks only if it is published. Fires on: the target has no resolvable URL.

7. **A demonstrated exchange with a named domain tool — include.** The evidence is one of: a shared or
   converted data model; one package's output imported into the other; an adapter/converter API; a
   plugin or extension relationship; a companion package designed to be used with it; a cross-language
   bridge to a named domain tool (a Python front end to SolarSoft, an IDL SPEDAS or MATLAB interface).
   The evidence may live in **either** package: a module in the other package written against this
   software, or another tool importing this one and consuming its output, is a demonstrated exchange
   seen from the other side. A hosted domain tool with a documented import path counts too — the
   "same environment" sentence is a caveat, not the test. Fires on: a named function, doc page, example,
   test or build hook that performs the exchange. **Worked contrast:** PySPEDAS ↔ PyTplot (exchanges tplot
   variables) ✅ · hapiclient ↔ hapiplot (companion visualization package) ✅ · sunpy ↔ ndcube (shared
   NDCube data model) ✅ · "depends on numpy" ❌ · "uses matplotlib for all plotting" ❌ · "listed in
   pyproject.toml dependencies" ❌.

8. **Where a rejected entry goes: usually nowhere.** A package excluded here is **not** thereby a Field 29
   entry; Field 29 applies the same Tier A exclusion to the generic stack, so the fix for an over-inclusion
   is normally **removal, not relocation**. A genuinely distinguishing domain package may belong in Field 29
   on its own Field 29 evidence.

9. **Listing a package in both fields** is correct only when each field's own ground is independently
   evidenced — for example, a companion package (Field 29) that is also a tested exchange partner (Field
   30). When the only relationship is the link itself, the entry belongs here and not in Field 29 as well.

10. **Under-inclusion is as wrong as over-inclusion.** Check README, docs, examples and tests for genuine
    interoperability with named domain tools that is missing: `to_*`/`from_*` converters, documented
    export→import handoffs, companion or plugin packages, shared data models. Run the inbound sweep: when
    another HSSI entry lists this software in its Field 29 or 30, test the reverse relation on this
    software's own evidence and add it here when rule 7 fires — a one-directional relation in the
    catalogue is a finding, not a mandate. A real interoperability partner left out is as wrong as numpy
    left in; a validator flags a missing one as a WARNING or SUGGESTION.

11. **URL form** follows Field 29's URL rules, rules 11–16 there: repository URL first (in-catalogue target →
    that entry's exact stored `code_repository_url`; external target → the upstream repository root), a
    concept DOI only when the target has no public repository, never a version DOI, a passed-over concept
    DOI named beside the recorded URL in the dossier, ≤128 characters, placeholder names never drive the
    choice, dead links → a Wayback capture. Settle relevance first, then the URL.

12. **Incumbents are held to the same bar.** Give every stored value its own verdict under rules 1–9 on a
    refresh. A stored value kept without an argument is the same defect as a candidate rejected without
    one. A Tier A or generic-infrastructure incumbent is removed — that is the rule applied, not a choice
    to offer. Since this field is enrich-only, an enrichment run is the main path by which a generic
    dependency would otherwise reach a live entry: never enrich a Tier A or unevidenced Tier B package
    into it.

13. **Empty is a legitimate outcome** when nothing passes; record that the sources were searched and what
    was rejected, so the blank is evidenced rather than unexamined.

## Ask the user only when

No listed shapes: every case is decided by the rubric. A documented public `xarray.Dataset` (or other
package-specific) interchange type meets rule 4's bar without a separate converter or round-trip test;
internal use and generic `ndarray`/`DataFrame` compatibility do not.

## Where to find it, and traps

**Sources, in priority order:**
1. The public API: converter and adapter functions (`to_*`, `from_*`), documented argument and return
   types, plugin or entry-point registrations, extras declared for a partner package.
2. Documentation and examples that pass data between this software and a named tool.
3. Tests that exercise the exchange (a round trip through the partner's object, a comparison through the
   partner's API).
4. Build and CI hooks that probe for or invoke the partner (a CMake check that imports it, a test that
   shells out to it).
5. The partner's own repository — an import of this package, a module written for it, a dependency pin
   on it.
6. The reference publication and the project's own statements (a titled subsection on integration, a
   stated output format "constructed to be compatible with" a named tool).
7. The catalogue itself: the inbound sweep (other entries' Fields 29/30 keyed on this software's
   repository URL **and** on every DOI it has carried) and a by-concept sweep for peer tools.

**Traps:**
- `git grep -E` reads `\b` as a literal `b`; use `git grep -P` for word boundaries, and back a negative
  with an unanchored run and a positive control (a term that must match).
- A dependency declaration is not evidence of anything except presence; a test-only or docs-only import
  is not an exchange with a peer tool.
- An import inside a function with a comment such as "avoid X as a hard dependency" is an
  interoperability affordance, not a dependency — read it as evidence *for* rule 4, not against.
- A changelog line saying functionality "moved to" another package invites an entry; confirm the package
  was actually published before recording it (rule 6).
- The partner may have changed since the relation was recorded (a module that once imported this package
  may have moved to a plug-in); check the partner at its current revision and record which side the code
  now lives on.
- The in-catalogue URL may differ from the one the build fetches (a pinned fork); see Field 29's URL
  rules.

## Payload and roundtrip notes

- **Key:** `interoperableSoftware` — an array of URL strings.
- **Shared RelatedItem rules (Fields 27–30):** each entry must be a real URL — free text fails the
  serializer's `URLValidator` (`Invalid URL: '<value>'`) and rejects the whole atomic request. Keep each
  URL ≤128 characters: `_get_or_create_related` stores the URL as both `identifier` and the 128-capped
  `name`, so a longer URL passes validation and then fails at the database write.
- **Binding:** the serializer strips the URL and looks up an existing RelatedItem by exact `identifier`;
  if found, that row is reused unchanged (its `name` is write-once), otherwise a new row is created with
  `name = identifier = <URL>` and type software. Send the exact identifier of an existing row to bind it.
- **Moving between Fields 29 and 30** needs no retype — both create and reuse software-typed rows. A URL
  that already exists as a **publication or dataset** row (Fields 27/28) keeps its old type when reused
  here, so JSON-LD would carry the wrong `@type`; that type correction is NON-PATCHABLE and must be
  reported rather than patched.
- **PATCH** replaces the whole list; a stored member left out is removed, and `[]` or `null` clears the
  field. An omitted key leaves the field unchanged. Compare as a multiset (order is not stored data here).
- **Readback:** `/api/view/` returns the identifier; `/api/data/` returns row UUIDs — resolve them before
  treating a list as drifted.

## Worked examples

- **A cross-language bridge and a Tier B admission (hissw).** hissw exists to run SolarSoft IDL from
  Python — its whole public behaviour sets up the SSW environment and emits SSW path commands — so
  SolarSoft passes rule 7 as a cross-language bridge. Astropy passes rule 4 on four surfaces: a public
  Jinja filter that requires an `astropy.units.Quantity`, registered by default; a dedicated `astropy`
  extra; a documented example passing a Quantity through the filter; and tests exercising it. SunPy and
  ChiantiPy, named once in a sentence contrasting them with SSW, have no exchange and go nowhere.
- **A signature match is not a demonstrated exchange (pyflct).** pyflct returns velocity arrays; a
  sunkit-image module consumes velocity arrays of the same shape. Neither side documents, tests or
  exemplifies the pairing, and the types are bare `numpy.ndarray`, so rule 5 fires and the entry is
  excluded with the evidence recorded. sunpy is removed too: no import, no dependency, and the only
  connection is shared maintainership (rule 3).
- **The consumer side counts (MadrigalWeb).** GeospaceLAB imports `madrigalWeb`, pins it as a dependency
  and builds its whole Madrigal data path on its client class, so rule 7 fires from the other side and
  GeospaceLAB is recorded here — not in Field 29, where it has no ground of its own. GeoDataPython, which
  can open Madrigal HDF5 files but never names this package, is an inference through a shared archive
  format (rule 5).
- **Dependencies out, a downstream tool in (PyGemini).** HDF5, h5fortran, LAPACK, ScaLAPACK, MUMPS and MPI
  are libraries the model links or calls, generic by rule 2, and are removed rather than relocated.
  amisrsynthdata, which imports the model's Python reader and turns its simulation output into synthetic
  radar data, is added under rule 7, and the relation now points both ways.
- **A hosted tool with a documented import (PyAuroraX).** Three public methods generate a Swarm-Aurora
  custom import file and open a conjunction search in the Swarm-Aurora Conjunction Finder, so the
  hosted tool's page is recorded under rule 7 even though it is not an installable package. The earlier
  candidates justified only by "PyHC registry shows these packages work with similar data" fall to rule 3.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 683-703 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
