# Field 11 — Publisher

**Level:** RECOMMENDED · **API:** `publisher` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.1 (name, abbreviation) · **Field-search code:** `publisher`

## What it is

**Type:** Nested group

**What it is:** The publisher (entity) of the creative work.

**How to fill it:** For software where a DOI has been obtained through Zenodo (e.g., GitHub-Zenodo workflow), Zenodo is the correct entry. If no DOI has been obtained, indicate the repository host, such as GitHub or GitLab.

**Sub-fields:**
- **Organization** (RECOMMENDED): Publisher name
- **Publisher Identifier** (RECOMMENDED): ROR identifier when available (e.g., https://ror.org/03c3r2d17) or URL otherwise (e.g., https://zenodo.org)

## Why it exists

The publisher tells a reader who makes the citable form of the software available: the archive that
issued its DOI, the institution that distributes it, or the platform that hosts its source. It completes
a software citation and tells a reader where the authoritative copy lives. A wrong value (a package index,
an operating institution's ROR on an archive, a DOI in the identifier slot) misdirects the reader's
publisher link.

## How it appears on the site

- **Detail page:** a "Publisher" item, linked to the publisher's identifier (or the organization's
  website) when one is stored.
- **Free-text search:** tier T4.1 on publisher name and abbreviation.
- **Field search:** `publisher:"…"` matches the publisher name.
- **Filter tab:** none.
- **JSON-LD:** `publisher` is an `Organization` with name, and identifier when stored.

## Rubric: include / exclude

Choose the organization with rules 1–6, applied top to bottom — **stop at the first rule that fires**.
Then settle its identifier and the incumbent value with rules 7–9, which all apply. The publisher follows
the host of the software's identifier.

1. **Field 2 is a Zenodo DOI → `Zenodo`, identifier `https://zenodo.org`.** This holds whether the
   deposit came through the GitHub–Zenodo integration or a manual upload; DataCite's `publisher` for the
   DOI confirms it. Zenodo has no ROR: do not substitute CERN's ROR, which identifies the operator, not the
   repository.
2. **Field 2 is a DOI registered by another repository → the publisher that DOI's DataCite (or Crossref)
   record names.**
3. **No DOI, and the software names its own publishing or distributing institution → that institution,
   with its ROR.** A README "distributed … by the Finnish Meteorological Institute", a licence "is making
   available the … software package", or an institution that is the software's sole distributor and hosts
   it (CCMC for its models, LMSAL for SolarSoft) outranks the repository host. Prefer the publishing unit
   when it has its own ROR over its parent agency.
4. **No DOI, source private, published through an institutional portal → the institution that runs the
   portal.**
5. **No DOI → the repository host:** `GitHub` (`https://github.com`), `GitLab` (`https://gitlab.com`).
6. **A package index is never the publisher.** PyPI, conda-forge and similar are distribution channels;
   record their role in Field 12 if anywhere.
7. **Identifier → the organization's ROR when one exists; for a hosting platform without one, its URL**
   (`https://zenodo.org`, `https://github.com`); **an institution without a ROR gets no identifier.** Never
   a DOI, a project page, or the software's own URL, which would label the shared Organization row with one
   project's page.
8. **Incumbent value:** keep a stored publisher the rules above yield. Replace it when Field 2 changes the
   branch (a DOI newly obtained through Zenodo moves `GitHub` → `Zenodo`) or when the stored identifier is
   wrong; record the previous value and why it was replaced.
9. **The chosen organization already exists as an identifier-less row → send it without an identifier**,
   so it binds that row by name. Sending any identifier would create a second row; if a ROR exists for it,
   record the ROR in the dossier and report attaching it as a NON-PATCHABLE shared-row correction.

## Ask the user only when

- **A NON-PATCHABLE correction to a shared Organization row is needed** (a ROR for a stored
  identifier-less publisher row, or a rename). The rubric decides the target; the user decides whether it
  goes through the database workflow.

## Where to find it, and traps

**Sources, in priority order**
1. Field 2's DOI record: DataCite `attributes.publisher` (Zenodo DOIs), or the registering agency's record.
2. The software's own statements of who distributes or makes it available (README, licence, citation
   text).
3. The repository host of Field 3.

**Verification**
- ROR identifiers must be full URLs: `https://ror.org/XXXXXXXXX` (Fields 6, 11 and 25 share this format).
  Resolve every ROR and check that it names the publisher.
- A ROR v2 query for `Zenodo` returns no result; that is settled negative research.

**Traps**
- A ROR found by guessing can name an unrelated organization (`https://ror.org/03cpe7c52` is the Allen
  Institute, not Zenodo).
- The concept DOI is not a publisher identifier.
- Zenodo records mentioning the software can be a fork snapshot or a paper's supplement, not the project's
  own deposit; they do not make Zenodo the publisher.
- A co-copyright holder is not the publisher when the distribution statement names only one institution.

## Payload and roundtrip notes

### Publisher has no `publisherIdentifier` key

The publisher object uses `{name, identifier}` only. There is no `publisherIdentifier` key — use `identifier` for the ROR or other organizational ID.

```json
"publisher": {
  "name": "Zenodo",
  "identifier": "https://zenodo.org"
}
```

- **Resolution:** with an identifier, the Organization is matched on the identifier only, else created with
  the name exactly as sent — an existing identifier-less row of the same name is not reused and becomes a
  duplicate; without an identifier, `name__iexact`, else create.
- **Shared rows:** the publisher is an Organization row shared with every entry's publisher, affiliations
  and funders; a matched row's nonblank name is never overwritten, so a rename is NON-PATCHABLE.
- **Clearing:** `"publisher": null` clears the field.
- **Roundtrip:** the curator view may return the identifier under a renamed key such as
  `publisherIdentifier`, although submission uses `identifier`.

## Worked examples

- **An institution names itself as distributor (rhybrid).** No DOI exists, and the README says the code is
  distributed under GPL v3 by the Finnish Meteorological Institute. Rule 3 records FMI with its ROR
  instead of the fallback `GitHub`; Aalto, a co-copyright holder, goes to Field 6 as an affiliation.
- **Hosted on GitLab, released on PyPI (aidapy).** No DOI; rule 5 gives `GitLab`, and rule 6 keeps PyPI
  out.
- **A Zenodo DOI (NEXRAD).** Rule 1 gives `Zenodo` with `https://zenodo.org`; the dossier records that
  Zenodo has no ROR and that CERN's is not a substitute.
- **An identifier-less stored row (SolarSoft).** The laboratory has no ROR and already exists as an
  identifier-less row serving several affiliations. Rules 3, 7 and 9 record it with no identifier; sending
  the SolarSoft page URL would mint a second row and mislabel the institution.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 277-289 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
