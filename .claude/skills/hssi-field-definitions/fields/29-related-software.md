# Field 29 — Related Software

**Level:** OPTIONAL · **API:** `relatedSoftware[]` · **Change class:** enrich-only
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.4 (name) · **Field-search code:** `related`

## What it is

**Type:** Multi-entry URL (RelatedItem lookup — repository URL preferred; a DOI only when the target has no public repository. The form's tooltip says "DOI URL preferred"; the URL-form rules below supersede it.)

**What it is:** Software that performs similar tasks but does not necessarily link together (which would be 'interoperable software'). For example, two software that model the upper atmosphere of Earth but using different assumptions. Important software dependencies and software this work was forked from should also be included.

**When to include it (relevance):** List software that is *distinguishing* — it tells a reader something about **this** software. That means a package performing similar tasks, a predecessor or the project this was forked from, a companion package, or a **domain-specific** dependency (a heliophysics/science library whose presence characterizes the software). "Important software dependencies" means exactly that: *important*, not merely *present*. **The generic scientific-Python stack is excluded here too** — the Tier A packages listed in Field 30 and their peers are not related software, because listing them says nothing that isn't equally true of most of the ecosystem. Those names are **examples, not a closed list**: apply Field 30's "web app, finance model, or biology pipeline" test to anything unnamed, and treat generic infrastructure as excluded here too. Same test as Field 30: **if the entry would be equally true of most Python packages, it carries no information and does not belong.** The two gates are one rule — a package rejected from Field 30 is *not* thereby a Field 29 entry; it usually belongs in neither.

**How to fill it:** Ideally, enter the DOI for the software code. Otherwise, link to code repository (e.g., https://github.com/sunpy/sunpy). If no public repository, enter link where users can find more information (e.g., related HSSI item). Publication DOIs should go in relatedPublications instead.

**The form's DOI preference is superseded by the URL-form rules below (rules 11–13):** the site shows a
related item's raw URL as its link text, so a repository URL is recorded whenever the target has one and a
DOI only when it has none.

The single full copy of the **Tier A and Tier B lists** and the generic-infrastructure test lives in
Field 30 (`30-interoperable-software.md`, Rubric rules 1–4); this field applies them by reference. This
file holds the single full copy of the **URL-form rules** (rules 11–16 below), which Field 30 applies by
reference.

## Why it exists

A user evaluating a package wants to know its neighbourhood: what else does this job (so they can
compare), where the code came from (the model it wraps, the project it was split out of), what
companion packages go with it, and which domain library it is built on. Those relations answer "is
this the right tool, and what else should I look at?" in one glance. Padding the field with the
dependency list, organisation siblings or dead links hides that answer and sends the reader somewhere
useless.

## How it appears on the site

- **Detail page:** in the "Related Items" section, under a "Related Software" heading, one link per
  entry. The link target is the stored identifier (the URL); the link text is the RelatedItem's stored
  `name` unless it is `UNKNOWN`, in which case the raw URL is shown. Rows created through the API store
  the URL as their name, so in practice the visible text is the **raw URL** — a repository URL reads as
  the project, a DOI reads as an opaque string.
- **Filter:** none.
- **Free-text search:** tier T4.4, matching the RelatedItem `name` — for API-created rows that is the URL
  text itself.
- **Field search:** `related:"…"` matches `related_software__name__icontains`.
- **JSON-LD:** each entry is emitted under `mentions` with `description` `relatedSoftware`, `@id` and
  `url` set to the identifier, and `@type` taken from the RelatedItem's stored type
  (`SoftwareSourceCode` for a software-typed row).

## Rubric: include / exclude

Decide relevance first, then the URL. Apply rules 1–10 top to bottom for each candidate and stop at the
first rule that fires; then apply rules 11–16 to every entry that is kept. Record a short note for every
package considered and dropped, and name the specific evidence for every package kept.

**Relevance**

1. **Tier A and generic infrastructure — never.** Apply Field 30 rules 1–3 unchanged: the Tier A names,
   the "web app, finance model, or biology pipeline" test for anything unnamed, and the blanket
   justifications ("listed as a dependency", "part of the standard scientific Python ecosystem", "a PyHC
   member", "same organisation"). Generic numerical and I/O libraries are excluded here even when they
   are compiled, prominent in the README, or user-visible in a known-limitations note (an HDF5 wrapper, a
   sparse solver, a path library): visibility is not a ground for listing. Fires on: any Field 30 rule
   1–3 match.

2. **Tier B without documented package-specific evidence — exclude.** A Tier B package (Field 30 rule
   4's list) is admitted here only on the same documented, package-specific exchange Field 30 rule 4
   requires; a signature that accepts a generic type the other package also uses (`ndarray`,
   `DataFrame`) is not an exchange. Fires on: no such evidence. With the evidence, continue to rule 9.

3. **A package rejected from Field 30 does not automatically land here.** It needs its own ground under
   rule 9; usually it belongs in neither. Fires on: the only relationship is that the two link together —
   that relation belongs in Field 30 alone, and listing the same URL in both fields would show a reader
   the same link twice for one fact.

4. **Support must come from this software's sources or its developers.** A relation asserted only by the
   other project (a third-party refactor describing itself as derived from this one), a single stale
   comment naming a package that is never imported, or one `FIXME` naming a possible predecessor is not
   a provenance claim. Record it as an open lead; admit it when this project's sources, or its
   developers' own statement (a paper or abstract by the same team), establish it.

5. **The wrong thing with the right name — exclude.** A different implementation of the same model is
   different software. Fires on: a candidate offered as the thing this software builds, wraps or depends
   on when it is a different implementation from the one actually used (a Python wrapper of a Fortran
   model, when the build compiles its own Fortran adaptation) — record the implementation actually used
   instead. A separate implementation can still qualify on its own ground as a similar-purpose tool
   under rule 9 (software that vendors a model can be related to a standalone package running the same
   model). A commercial runtime already recorded in Field 13 (IDL, MATLAB as a language) is not related
   software by that fact alone. A single-service client library (an archive's REST client) is recorded
   as the data source in Field 17, not here. A CI-fixture repository tells a prospective user nothing.

6. **Ecosystem context is not a similar-task claim.** A sentence that names other packages as
   equivalents to something *else* (to the IDL library this software bridges to, say) is context, not
   a statement that they perform this software's task. Exclude unless rule 9 fires on other evidence.

7. **Current relations only.** An alternative the project has since removed from its README, or whose
   repository is archived after the split, is excluded under the same bar that admits the still-current
   ones. Functionality planned but not shipped is not a relation.

8. **Do not enumerate an organisation.** Prefer the parent package over an auxiliary script collection
   whose parent is already listed; a project's other repositories are not related merely by living in
   the same GitHub organisation.

9. **Distinguishing software — include.** Fires on one of these, with the evidence cited:
   - **similar-purpose tools** the project itself names as alternatives or equivalents (a README
     "Alternatives" section, a docs link labelled "another version"), or packages the software's own
     papers co-describe as performing the same task;
   - **a predecessor, fork parent or code origin** — the project it was forked from, the subpackage it
     was extracted from (documented by a commit on either side), the earlier distribution name it was
     published under, or the original code it wraps or vendors;
   - **a companion package** — the same project's documentation or examples repository, a front end in
     another language, an IDL or MATLAB counterpart by the same team, a sister implementation
     deliberately split out of this repository, or a package its developers describe as its companion;
   - **a domain-specific dependency whose presence characterises the software** — a heliophysics model
     the build includes by default, a coordinate or data library the code delegates its science to.
     *Important*, not merely present.

10. **Empty is a legitimate outcome** when nothing passes; record that the sources were searched and what
    was rejected.

**URL form (for every kept entry, here and in Field 30)**

11. **An in-catalogue target uses that entry's exact stored `code_repository_url`** — bind, don't mint.
    Look up the other HSSI entry and copy its `code_repository_url` byte for byte, even when that entry
    also has a DOI: the page shows the raw URL as link text, a repository URL is legible where a DOI is
    not, and the exact string keys the catalogue's own record.

12. **An external target uses its upstream repository root URL.** (a) The repository root of the
    **upstream project** (`https://github.com/<owner>/<repo>`), never a fork a build script happens to
    fetch from, never a `/tree/` or `/blob/` sub-path, never a docs or PyPI page when a repository exists.
    (b) Only when the target has **no public repository**, its concept DOI. (c) Otherwise a page where
    users can find more information (a model's CCMC page, a vendor's product page). If a RelatedItem row
    already exists with exactly the prescribed URL, send it byte for byte so it binds; a row for the same
    target in another form (a DOI, a docs page, a sub-path) is **not** reused — send the prescribed form
    even though it mints a new row, and leave the other rows to be corrected when their own entries are
    refreshed.

13. **Never a version DOI** for a software relation — it asserts a relationship to one frozen release.
    Any stored DOI, version or concept, to a target that has a public repository is replaced by that
    repository URL (the stored `code_repository_url` in-catalogue, the upstream root externally).
    **Record the DOI you passed over.** Whenever a repository URL is recorded for a target that also has a
    concept DOI, the field's dossier section names that concept DOI beside the recorded URL and states
    that the repository form was chosen because the site renders the raw URL. Both forms are then on
    file, so the choice can be reversed cheaply if HSSI ever renders resolved titles for related items.

14. **New URLs are at most 128 characters** (the RelatedItem name column is capped at 128; see payload
    notes).

15. **A dead link is replaced, not kept and not silently dropped.** When the relation is still real and
    the original URL no longer resolves, record an Internet Archive (Wayback) capture of the original
    that still shows the content, and keep the evidence that the original is dead so a later refresh
    does not restore it. When the relation itself is gone, remove the entry.

16. **RelatedItem names are placeholders** (`UNKNOWN` or the raw URL) and must never drive the choice of
    URL or be treated as a data-quality problem to fix.

**Incumbents**

17. **Every stored value gets its own verdict** under rules 1–16 on a refresh. An incumbent kept without
    an argument is the same defect as a candidate rejected without one: when the stored justification is
    too weak to carry the value (a shared registry keyword), replace the justification or remove the
    value. A Tier A or generic-infrastructure incumbent is removed — the rule applied, not a choice to
    offer. A stored URL that still resolves to the intended project — through a redirect, or with
    different case in the path — keeps its exact identity; a redirect alone is not a reason to rewrite
    it. Never enrich a Tier A or unevidenced Tier B package into this enrich-only field.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

**Sources, in priority order:**
1. The project's README and docs: "Alternatives", "See also", "Other references", acknowledgements of the
   original code, links to companion repositories.
2. Git history: the initial commit (code moved in from elsewhere), rename commits, commits that split an
   implementation out to another repository — and the other repository's history for the matching
   removal.
3. The package registry record (a predecessor distribution name, `project_urls`); only PyPI's JSON/Simple
   API is authoritative, and a 200 from the HTML page proves nothing.
4. Build files that fetch or vendor other models (`cmake/libraries.json`, vendored Fortran directories).
5. The reference publication and the developers' own talks/abstracts (author contributions, "companion
   package" statements).
6. The catalogue: the inbound sweep (other entries' Fields 29/30 keyed on this software's repository URL
   **and** every DOI it has carried) and a by-concept sweep for similar-purpose entries; look up each
   candidate's stored `code_repository_url`.

**Verification:** fetch every URL you record and confirm it resolves to the intended project; for a
dead original, find a Wayback capture that still lists the content and record both facts.

**Traps:**
- GitHub `fork: true` and the upstream relationship: a build may fetch a zero-star fork; the upstream is
  the project to record.
- A Zenodo concept DOI and a version DOI look alike; read DataCite (`HasVersion` → concept,
  `IsVersionOf` → version) before recording one under rule 12(b) or naming one beside a URL under rule 13.
- A catalogue entry with a similar name may be a different implementation (a Python wrapper versus the
  Fortran adaptation the software builds) — rule 5.
- A redirect from the stored URL is not a broken link; a 404 or a removed subtree is.
- Word-anchored greps: `git grep -P`, never `git grep -E` with `\b`; back a zero with a positive control.

## Payload and roundtrip notes

- **Key:** `relatedSoftware` — an array of URL strings.
- **Shared RelatedItem rules (Fields 27–30):** each entry must be a real URL — free text fails the
  serializer's `URLValidator` (`Invalid URL: '<value>'`) and rejects the whole atomic request. Keep each
  URL ≤128 characters: `_get_or_create_related` stores the URL as both `identifier` and the 128-capped
  `name`, so a longer URL passes validation and then fails at the database write.
- **Binding:** the URL is stripped and matched on exact `identifier`; a match reuses the existing row
  unchanged (its `name` is write-once and cannot be repaired through the API), otherwise a new row is
  created with `name = identifier = <URL>` and type software.
- **Moving between Fields 29 and 30** needs no retype. A URL that already exists as a publication or
  dataset row keeps that type when reused here, which leaves the JSON-LD `@type` wrong; the correction is
  NON-PATCHABLE and is reported, not patched.
- **PATCH** replaces the whole list; a stored member left out is removed; `[]` or `null` clears; an
  omitted key leaves the field unchanged. Compare as a multiset.
- **Readback:** `/api/view/` returns the identifier; `/api/data/` returns row UUIDs — resolve before
  treating a list as drifted. RelatedItem rows have `id, name, definition, type, identifier` (no `url`);
  compare on `identifier`.

## Worked examples

- **One bar applied both ways (pyflct).** pyflct's initial commit says "Moved everything from
  sunkit-image to here", and sunkit-image's matching commit removes the subpackage, so sunkit-image is
  added as the code origin (rule 9). An independent wrapper of the same C library, linked from the docs
  as "another version", is kept as a similar-purpose tool. sunpy — shared organisation, badges and docs
  theme, but no import and no dependency — is removed (rule 1), and ndcube, with zero matches anywhere in
  the tree, is removed with it.
- **Infrastructure out, models in (PyGemini).** The built-in GLOW, HWM14 and MSIS models, the docs and
  examples repositories and the MATLAB front end are kept on rule 9. h5fortran (an HDF5 wrapper) and MUMPS
  (a sparse solver) are removed: generic infrastructure, and neither README prominence nor a
  known-limitations note is a ground for listing (rule 1).
- **A dead origin link (LOWTRAN).** The README cites the original 1994 NOAA distribution the vendored
  Fortran came from, but that subtree was removed. The relation is still real, so the Wayback capture of
  the directory listing is recorded instead (rule 15), and the dossier keeps the evidence that the
  original is dead.
- **DOIs to repository URLs (Kaipy, PyAuroraX, MGSutils).** Two stored relations were DOIs — one a stale
  version DOI for a single release, one a concept DOI — to software that has its own HSSI entry. Both are
  replaced by the target entry's stored `code_repository_url` (rules 11 and 13), which a reader recognises
  and which keys the catalogue's record. An external target is treated the same way: xarray has a concept
  DOI (`10.5281/zenodo.598201`), but `https://github.com/pydata/xarray` is recorded under rule 12(a) and
  the concept DOI is named beside it in the dossier (rule 13), so the pair is on file either way.
- **A DOI kept because nothing else exists (rule 12(b)).** A Fortran model distributed only as a Zenodo
  deposit, with no repository, is recorded by its concept DOI; the dossier states that no repository was
  found so a later refresh re-checks that fact rather than the URL form.
- **Alternatives, predecessor, sister implementation (Maidenhead).** The README's "Alternatives" section
  names two converters; the PyPI record and a rename commit establish the earlier distribution name; a
  commit moved the Fortran implementation to a gist. All four are recorded under rule 9. The Julia
  implementation, since dropped from the README and archived, is excluded under rule 7.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 672-682 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
