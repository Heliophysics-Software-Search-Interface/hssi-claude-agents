# Field 2 — Persistent Identifier

**Level:** RECOMMENDED · **API:** `persistentIdentifier` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** not searched · **Field-search code:** `pid`

## What it is

**Type:** DataCite DOI lookup with autofill

**What it is:** The globally unique persistent identifier for the software (e.g., the concept DOI for all versions).

**How to fill it:** If the software already has a concept DOI, enter the full DOI here (e.g., https://doi.org/10.5281/zenodo.13287868). Entering the concept DOI enables automatic population of metadata from that DOI.

The value is one URL. For a Zenodo deposit series it is the **concept DOI** (Zenodo's "all versions"
DOI); the DOI of one specific release is a *version DOI* and belongs in Field 12's Version PID.

## Why it exists

It gives a visitor one stable, citable handle for the software itself, independent of any single
release. The page turns it into the "Software" citation a visitor copies, so a wrong DOI hands them a
wrong citation — a poster cited as a journal article, or one old release cited as the software — with
no hint that anything is off. A missing DOI where one exists removes the only citable form of the code
from the page. Because the form autofills other fields from this DOI, a wrong value also spreads into
Fields 10, 11, 12 and 15.

## How it appears on the site

- **Action button:** a "DOI" button in the page header links to the stored value.
- **Citation block:** a "Cite Me" button opens a Citation section whose **"Software"** entry is
  generated server-side by `doi.org` content negotiation of this value (`Accept: text/x-bibliography`
  in the chosen style). It is generated only when the value begins exactly `https://doi.org/`; any
  other spelling leaves the software citation blank. The citation's type comes from the DOI's own
  registration, so a DOI registered as a poster or article is cited as one under the "Software"
  heading. When Field 14 also holds a DOI, both citations show with a notice to cite both; with
  neither Field 2 nor a Field 14 identifier there is no DOI button and no citation section at all.
- **JSON-LD:** the value is the entry's `@id` (falling back to the latest Version PID, then the code
  repository URL) and an `identifier` PropertyValue named `DOI: <doi>`.
- **Search:** not in the free-text tiers; `pid:"…"` matches it by substring.
- **Filter:** none.

A contested value therefore has exactly three page shapes: **keep** (the Software citation cites that
DOI), **clear** (no software citation), or **move to Field 14/27** (the item survives under a correctly
labelled heading). The rubric below picks among them.

## Rubric: include / exclude

Apply these to every candidate DOI and to the incumbent HSSI value, one at a time. Rules 1–5 decide
whether a value qualifies — stop at the first of them that fires. Rule 6 then normalises every survivor,
rule 7 selects when more than one qualifies, and rules 8–9 settle the outcome against the incumbent;
those four always run after a rule-4 or rule-5 acceptance.

1. **Not a software record → never Field 2.** Fires when the DOI's registration (DataCite
   `types.resourceTypeGeneral`, Zenodo `resource_type`) is a poster, presentation, article, preprint,
   thesis, report or dataset, however closely it describes the software. Route it by what it is: the
   paper the project asks users to cite → Field 14; any other publication about the software (poster,
   talk, conference abstract, paper) → Field 27; a dataset → Field 28. An incumbent of this kind is
   cleared unless rule 5 supplies a replacement.
2. **Software record of a different product → not Field 2.** Fires when the deposit archives other
   code: a dependency, a sibling package of the same umbrella project, a same-name package, or a
   review archive of a separate core library (evidence: the `IsSupplementTo` tree URL names another
   repository, or the deposited files are another package). It may belong in Field 29/30.
3. **Version DOI → not Field 2; use its concept.** Fires when the record is one version of a series
   (DataCite `IsVersionOf`, Zenodo `conceptdoi` differs from the record's own DOI). This covers a
   `doi:` in `CITATION.cff`, a README `zenodo.org/badge/latestdoi/<repo-id>` badge (it resolves to
   whichever version is newest), and a version DOI already stored. Take its concept DOI and apply
   rule 5 to that. The version DOI goes to Field 12's Version PID only if it identifies the version
   Field 12 records. **A stale version DOI in `CITATION.cff` never beats a stored concept DOI.**
4. **Legacy single deposit with no concept DOI → the version DOI is Field 2.** Fires only when the
   Zenodo record's `conceptdoi` is empty and no all-versions DOI is registered at DataCite. The same
   DOI then also serves as Field 12's Version PID for that version. Never construct a concept DOI
   from a `conceptrecid`.
5. **Concept DOI of a software deposit of this software → record it.** Written as
   `https://doi.org/<concept DOI>`. Identity is shown by an `IsSupplementTo` link to this repository's
   tree, by title plus creators, or, for a manual upload, by hashing the deposited files against the
   tagged blobs. Keep it even when:
   - the concept presents an older version than Field 12 (it resolves to the most recently
     **created** deposit — a backport, or deposits that stopped while releases continued);
   - one deposit covers this software together with a sibling library;
   - the deposit was uploaded by hand rather than by the GitHub integration;
   - it is a third party's deposit of this code and the project has none of its own.
   Record these facts in the dossier as known costs; none is a reason to clear or move the value.
6. **Same DOI, different spelling → rewrite as `https://doi.org/<doi>`.** Fires for a bare `10.…`,
   `http://dx.doi.org/…`, `https://zenodo.org/doi/…` or `zenodo.org/records/<id>` form of a DOI that
   passes rule 4 or 5. This is not cosmetic: the citation block renders only for the `https://doi.org/`
   prefix.
7. **Several software concept DOIs survive → the one the project's own files cite.** Fires when two
   or more concept DOIs pass rule 5. Choose the one in the README badge, `CITATION.cff`
   `identifiers`/`doi`, `codemeta.json` or the docs' citation page. If the project cites none of them,
   or more than one, ask (see below).
8. **No candidate survives → empty, with the negative research recorded.** Fires only after the
   no-DOI proof under *Where to find it* has been run with controls. An incumbent that failed rules
   1–3 with nothing to replace it is cleared. An evidenced-empty Field 2 is correct; an unsearched one
   is not.
9. **Incumbent that passes rule 4 or 5 → keep.** Field 2 is static: a refresh does not re-derive it,
   and a correct concept DOI is never swapped for a version DOI, a badge URL or a record URL. A full
   refresh re-verifies it with rules 1–5.

**Coupled fields.** When Field 2 changes between a Zenodo DOI and empty, re-decide Field 11 in the
same change (Publisher is Zenodo only when a Zenodo DOI identifies the software). On any entry whose
Field 2 is a DOI, re-derive Fields 10, 12 and 15 from the repository rather than trusting autofill
(see traps).

## Ask the user only when

- Two or more software concept DOIs identify this software and the project's own files cite none of
  them, or more than one (rule 7).

Anything else is decided by the rubric. A case no rule covers is a rubric gap: ask, and report it as
one.

## Where to find it, and traps

**Sources, in priority order.**

1. The project's own files at the pinned revision. **DOIs** (Persistent Identifier, Version PID,
   Reference Publication) may be in:
   - CITATION.cff
   - README badges
   - Zenodo integration
   - codemeta.json

   Also grep for `doi` (case-insensitive) across the whole repository, and check for `.zenodo.json`
   or `codemeta.json`.
2. DataCite for the candidate: `https://api.datacite.org/dois/<doi>` gives `types`, `version`,
   `titles`, `dates` and `relatedIdentifiers` (`HasVersion` on a concept, `IsVersionOf` on a version,
   `IsSupplementTo https://github.com/<owner>/<repo>/tree/<tag>` on an integration deposit).
3. Zenodo: `https://zenodo.org/api/records/<id>` (use `-L` and `Accept: application/json`) gives
   `conceptdoi`, `resource_type`, `related_identifiers` and files. A concept record id answers with a
   302 to its newest version.

**Verification.**

- DOIs must be full URLs: `https://doi.org/10.XXXX/XXXXX` (Fields 2, 12, 14, 27, 28, 29, 30). Field 31
  (Instrument Identifier) is normally a SPASE Resource ID URL (`https://spase-metadata.org/...`), not a
  DOI — do not flag a SPASE identifier as a malformed DOI (a DOI there is only a manual exception).
- Verify the DOI resolves: `curl -s -o /dev/null -w "%{http_code}" https://doi.org/{DOI}`.
- Cross-check against CITATION.cff, README badges, codemeta.json.
- **Read what the concept presents.** A Zenodo concept DOI resolves to the most recently *created*
  deposit, not the highest version. Read the concept's own `version` and `titles` at DataCite and
  compare them with the current tag; state both in the dossier.
- **Integration versus manual deposit.** An integration deposit carries `IsSupplementTo` → a
  `/tree/<tag>` URL and a populated `version`; a manual upload carries neither. Do not conclude
  "manual" from absence alone — compare with a contemporaneous deposit by the same author or
  organisation that does carry the link.

**Proving "no DOI exists".** Run all three, each with a control, before recording Field 2 empty:

1. **Title and subject search** at Zenodo and DataCite on the software's descriptive title and
   subject, with creator names (for example DataCite
   `titles.title:"<name>" AND creators.name:"<author>"`). A manual upload carries a human title and
   often no repository name, so repository-name queries alone cannot find it; several queries that
   all key on the repository name are one check, not several.
2. **Old repository name.** Fetch the repository under any former owner or name and see whether it
   redirects; search Zenodo for the former `owner/repo` too. A renamed or moved repository's deposits
   carry the old name.
3. **Creator-keyed search**, the only name-independent route:
   `https://zenodo.org/api/records?q=metadata.creators.person_or_org.name:"Family, Given"` and
   `…q=metadata.creators.person_or_org.identifiers.identifier:"<ORCID>"`. The `metadata.` prefix is
   load-bearing: without it the query returns a clean zero. Creator strings are not normalised
   (`Family, Given`, `Given Family`, a GitHub login, a bare first name), so union several variants.
   Unauthenticated `size` is at most 25; page with `page=N` until all hits are read. The positive
   control must be a record another route has already returned.

Traps in the search itself:
- `metadata.related_identifiers.identifier:"https://github.com/<owner>/<repo>"` is exact-match and
  integration deposits store the `/tree/<tag>` URL, so the bare repository URL returns zero even when
  deposits exist. Search free text `"<owner>/<repo>"` instead, with a control.
- Free-text queries containing a slash can return HTTP 500 for hours; `metadata.resource_type.type:`
  clauses have returned zero for everything. Record a failing route as *unverified by that route*,
  never as an absence.
- **DataCite mirrors Zenodo DOIs** and is the fallback when zenodo.org is unreachable
  (`https://api.datacite.org/dois/10.5281/zenodo.<id>` needs no token): version, issued date, the
  concept/version relations and the `/tree/` signature survive. It does not expose Zenodo's internal
  licence id or a concept's redirect target. DataCite's `client-id=` is a query parameter; written
  inside `query=` it silently matches nothing.

**Autofill traps.** HSSI's DOI autofill copies the Zenodo deposit faithfully, errors included, and the
copied values look authoritative. On any DOI-autofilled entry treat these as suspect until re-derived
from the repository: the licence (Zenodo's hand-set licence id is often wrong — the repository's
LICENSE file governs, Field 15); the version date (a Zenodo record's `updated` timestamp has been
captured as a release date — use the tag, release and PyPI dates, Field 12); the publication date
(DataCite `Issued` is the DOI mint date, Field 10); the Version PID (it belongs only to the deposited
version); and the author list when the deposit is stale (Field 6).

## Payload and roundtrip notes

- Key `persistentIdentifier`, a string URL, validated as a URL; the column is a Django `URLField`
  (200 characters).
- Clear with `null` (an empty string also clears); send `null` so the roundtrip compares like with like,
  since `/api/data/` returns `null` for a cleared value.
- Changing Field 2 touches no shared row; it does not affect Field 12's stored version row.

## Worked examples

- **Poster in Field 2.** HERMES Core held a Zenodo concept DOI whose record is an AGU conference
  poster (resource type Poster, a PDF file, no repository link). Rule 1 fires: Field 2 is cleared,
  both of the project's posters go to Field 27, and Field 11 moves back to the repository host.
- **Umbrella deposit, frozen at an old version.** PyAuroraX's README badge cites a concept DOI shared
  with the IDL-AuroraX library, whose last deposit is 1.0.0 while the software is at 1.23.0. Rule 5
  fires: the DOI is kept, and the shared scope and staleness are recorded as accepted costs; the
  describing article goes to Field 14 on its own merits.
- **Backport drags the citation backward.** ndcube's concept DOI presents v2.0.4 because that backport
  deposit was created after v2.1.3. Rule 5 still fires; the dossier states what the Software citation
  shows beside Field 12's newer version.
- **Stale CITATION.cff.** gcs_python's `CITATION.cff` carries the 0.2.3 version DOI (and carried the
  0.2.2 one at the 0.2.3 tag). Rule 3 fires for it; the stored concept DOI stays.
- **Legacy single deposit.** GeoDataPython's only deposit (2016) has an empty `conceptdoi` and no
  registered all-versions DOI. Rule 4 fires: the version DOI is both Field 2 and Field 12's Version PID.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 61-69 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
