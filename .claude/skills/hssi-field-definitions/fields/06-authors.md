# Field 6 — Authors

**Level:** MANDATORY · **API:** `authors[]` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.1 (given, family, identifier) · **Field-search code:** `author`

## What it is

**Type:** Multi-entry nested group

**What it is:** The author(s) of this software.

**How to fill it:** Multiple authors should be included in separate author fields.

**Sub-fields:**
- **Authors** (MANDATORY): Author name
- **Author Identifier** (RECOMMENDED): The identifier of the author. For a person author, this is the ORCiD (e.g., https://orcid.org/0000-0003-0875-2023). For an author that is an **organization** (a lab, consortium, or institution credited as an author), use its ROR instead (e.g., https://ror.org/03c3r2d17) — HSSI recognizes a ror.org identifier and treats that author as an organization. Enter the complete identifier URL.
- **Affiliation** (RECOMMENDED, multi-entry):
  - **Organization**: Complete name without acronyms (e.g., Center for Astrophysics Harvard & Smithsonian)
  - **Affiliation Identifier**: ROR identifier if one exists (e.g., https://ror.org/03c3r2d17)

## Why it exists

A site user reads the author list to learn whose work this is, whom to cite, and whom to contact, and
follows an author's identifier to their other work. Each author is a shared Person record, so a correct
identifier also joins this entry to everything else that person has in the catalogue. A missing author
denies someone credit; a padded list (committers, contacts, model originators) buries the people who
actually made the package; a wrong ORCID sends the reader to a stranger; a stale or wrong affiliation
misstates where the work was done on every entry that person appears on.

## How it appears on the site

- **Detail page:** an "Authors" section (expanded when there are ten or fewer). Each author renders as
  "given family", linked to the author identifier when one is stored; the author's affiliations follow in
  parentheses, each linked to its identifier (or the organization's website) when one is stored.
- **Order:** authors are a sorted many-to-many; the stored order is the order shown.
- **Free-text search:** tier T4.1 on author given name, family name and identifier. Affiliations are not
  searched.
- **Field search:** `author:"…"` matches any token against given or family name; for two or more tokens
  it also matches a Person whose given name contains the first token and family name contains the last.
- **Filter tab:** none.
- **JSON-LD:** `author` is an ordered `@list`. A person renders as `Person` with `givenName`,
  `familyName`, identifier and `affiliation`; an author whose identifier contains `ror.org` renders as
  `Organization` named "given family", with its affiliations as `parentOrganization`.

## Rubric: include / exclude

Decide each candidate author, then each attribute of each kept author, in the groups below. Within a
group apply the rules top to bottom and **stop at the first rule that fires**.

**Candidate pool.** Build it from the union of: the current HSSI record, CITATION.cff, codemeta.json,
`.zenodo.json` and the Zenodo/DataCite record's `creators` **and** `contributors`, AUTHORS/CONTRIBUTORS
files, package metadata (setup.py, pyproject.toml, setup.cfg, package.json authors and maintainers), and
the byline of a refereed paper describing this software. **Match candidates by ORCID first, then by
normalized name.** When both a prior `hssi_metadata.md` and live HSSI are seeded, live HSSI is the
baseline for what is published, and the author list is the identity-aware union of both seeds; for each
matched author, union affiliations by ROR and then normalized organization name, so choosing one author
object never discards affiliations from the other seed. Git history is evidence for a candidacy, never an
attestation of authorship.

### A. Who is an author

1. **Stored in HSSI as an author of this entry → keep.** No author is dropped in a refresh, including
   one a later CITATION.cff omits. If the stored link points at a defective duplicate row (a misspelled,
   identifier-less copy) of a person whose identified row already exists, send that person's stored ORCID
   under the identified row's stored name, so the entry binds the identified row; that is a relink, not a
   removal.
2. **Attested contributor known only by a handle → an author, recorded as the handle.** When an author
   source in the candidate pool (CITATION.cff, `.zenodo.json`/Zenodo creators, AUTHORS) credits a GitHub
   username or other handle and no human name can be established, the person is still an author. First
   try to resolve the handle to a person: a personal name becomes assertable only when a primary artifact
   carries it — a commit git-authored under that name, tied to the login by a GitHub noreply address
   (`<id>+<login>@users.noreply.github.com`) or by the commit API's `author.login`. If that fails, record
   **givenName = the exact login, capitalization verbatim, familyName = `(GitHub)`** (or the platform the
   account is on, e.g. `(GitLab)`), provided the handle is **proven** — a noreply address encoding the
   login, or the commit API attributing a commit to that account. When the string is certainly a username
   (the project's own metadata classifies it as one, or a commit address's local part is the handle) but
   no platform account can be established, record familyName **`(Username)`** instead. Never infer a human
   name from the handle's spelling, from a profile display name, or from `github.com/<handle>`; never
   carry an upstream literal such as `GithubUser` as a family name; assert no identifier and no
   affiliation for a handle author. A handle that appears only in git history and in no author source is
   a committer (rule 5), not an author.
3. **Originator of a model, algorithm or predecessor code that this package reimplements, adapts or was
   inspired by → not an author** — unless this package's own metadata (`CITATION.cff`, package
   `authors`, Zenodo creators) names them as an author at the pinned revision or did so in a released
   version, in which case rule 8 applies and the dossier records the predecessor relationship beside
   the attestation. Otherwise credit them in Field 27 (their paper) or Field 29 (their code).
4. **Wrapper that ships a third-party component whole → credit the people the sources name as authors of
   that shipped component**, alongside the wrapper's own author. Do not credit support or correspondence
   contacts, authors of individual routines inside a component, authors of a prior-language original a
   routine was adapted from, people acknowledged, or version-control keywords (`$Author: … $`).
5. **Committer absent from every attestation → not an author.** Commit volume is not authorship; neither
   is a CI-integration commit, a README-only commit, or a successor project's author touching the repo.
6. **Listed as a contributor under a heading the project keeps separate from its authors, and absent from
   every other author source → not an author.**
7. **Co-author of a paper or presentation about the software who appears in no software-metadata source
   → not an author.**
8. **Attested → add.** A person or organization named as an author, creator or maintainer in any source
   in the candidate pool, or credited as an author of the software in a scholarly citation of it (a
   paper's bibliography entry for the software, the software's own citation guidance), is an author. A
   refereed software paper's byline outranks a repository file that demotes its co-authors to testers.
9. **Otherwise → not an author.** Flag any author present in a source but missing from the metadata.

### B. Name form

10. **Stored name matches a project source, or the person's ORCID primary, credit or other name → keep it
    and document any divergence.** A middle initial, a fuller given name or an unaccented spelling is a
    style variant, not a correction. A PATCH cannot change a stored name's words (the spelling changes it
    can make are rule 11's), and the Person row is shared by the person's other entries.
11. **Stored name matches no source → record the correct form as the target.** How it lands depends on
    what differs:
    - **The same full name, spelled differently** (*Person resolution* below defines it): a different
      split (`Daniel da` / `Silva` for `Daniel` / `da Silva`), capitalization (`Darren de` / `Zeeuw` for
      `Darren` / `De Zeeuw`), accents or hyphens. A PATCH gives the sent names to the row it selects by
      `personId`, so send the corrected names with the row's `personId` (rule 30); they show on every
      entry the row serves. Sent names with fewer accent marks in total than the stored ones are not
      applied at all, so removing accents is NON-PATCHABLE.
    - **Anything else is a rename, NON-PATCHABLE:** a misspelled, changed, added or dropped word, or an
      honorific in the given name. It needs a database-side correction to a shared Person row, checked
      against every entry that row serves. A legacy row with a blank given name and a bare handle as its
      family name (a bulk contributor import) is corrected the same way: to the proven human name when a
      primary artifact carries one, otherwise to `<login>` / `(GitHub)` per rule 2.
12. **New author → the project's own spelling**, diacritics included as the project writes them, over a
    better-documented external form. Take the given/family split from the person's linked ORCID
    structured name, else from CITATION.cff `given-names`/`family-names`; keep surname particles with the
    family name (`De Zeeuw`, `Al Shidi`, `Van Kooten`); drop degree suffixes (`Ph.D.`). Names follow the
    "Given Name, Initials, Surname" convention. Never import a DataCite/Zenodo split that puts an
    honorific in the given name or the whole name in `familyName`.

### C. Identifier (person authors)

13. **Stored ORCID → keep.** If it demonstrably belongs to a different person, record the right one and
    report the change as NON-PATCHABLE: a PATCH never replaces a stored identifier, and sending the right
    one creates a new Person for this entry while the wrong one stays on the person's other entries.
14. **Candidate ORCID without independent identity linkage → do not record it.** The ORCID record itself
    must connect to this person or this work: its works list the software or its paper, its employment
    matches the commit address and the field of the work, its researcher URL leads to the contributor's
    GitHub account, or a project source or DOI record carries the ORCID beside this name. A name match
    alone is not enough, nor is a same-name, same-institution record with no works. Record the rejected
    candidate and the reason, so a later refresh neither re-hunts it nor adopts it.
15. **Linked ORCID for an author of this entry stored without an identifier → record it and send it with
    the row's `personId`** (rule 30). The row takes the ORCID, and any respelling rule 11 calls for. The
    ORCID is NON-PATCHABLE when the row also serves entries by a different person of the same name: the
    ORCID would show on theirs too (*Stored-row sharing* below).

    An ORCID that another Person row already carries means the entry should list that row instead, a
    relink (rule 1); sent with this row's `personId`, it is a 400.
16. **Linked ORCID for an author new to this entry → record and send it.** For an ORCID that no row
    carries yet, first look for an identifier-less row under this person's name. It is this person's when
    an entry it serves credits this person in its own author sources, and a namesake's when its entries
    are another person's work.
    - **This person's row → select it.** Sent without `personId`, the ORCID would create a second Person
      beside the row. On an update, send the author with the row's `personId`, the ORCID and the row's
      stored full name (rule 11 may respell it; a different word is a 400): the one PATCH binds the row
      and fills its identifier, and no namesake on the entry can take the ORCID (*Selecting a row by
      `personId`* below). On a new submission, a POST cannot select a row: send the author without the
      ORCID under the row's exact stored given and family names, which binds it, keep the ORCID in the
      dossier, and let a later update fill it (rule 15). That bind is NON-PATCHABLE when another Person
      row has the same exact split: a name sent without an identifier binds an arbitrary one of them.
    - **No row of this person's → send the ORCID;** the new Person it creates is correct. On a PATCH,
      though, an ORCID sent without `personId` attaches to the entry's identifier-less current author with
      the same full name, whichever author it was sent for. If that author is another person, report the
      identity collision as NON-PATCHABLE; sending the ORCID would give it to them. (If it is this person,
      the author is not new: rule 15.)

    An ORCID that a row already carries binds that row on either path; send it under that row's stored
    name.

### D. Affiliations

17. **Stored affiliation → keep.** Affiliations accumulate on PATCH and cannot be removed; a desired
    removal is NON-PATCHABLE and is reported, never attempted.
18. **Not an affiliation:** a GitHub organization handle (`@rice-solar-physics`), an alumni address (it
    says where someone studied), an employer the person joined after producing the software, a
    ROR false match found by name search (e.g. SciVision Biotech Inc. for Scivision, Inc.), or a raw
    affiliation string that does not name an institution.
19. **Years-stale source and the Person row serves other entries → do not add.** A past institution
    lengthens that person's display on every entry while telling a reader nothing about where the work is
    done now.
20. **Evidence conflicts about the institution → add only an institution true under every reading;
    otherwise assert nothing.** No affiliation is the reversible choice; an added affiliation cannot be
    withdrawn. Record the supported alternatives in the dossier so a later refresh can reconsider them.
21. **Institution the project's own metadata gives for the person** (CITATION.cff, codemeta.json,
    `.zenodo.json`/Zenodo creator affiliation), **or an ORCID employment or paper byline covering the
    period the software was produced → add it with its ROR.** Read an ORCID employment whole (organization,
    department, role, dates, city, country, disambiguation id) before relying on it. Split a Zenodo
    affiliation string that packs several institutions (`1 - … 2 - …`) and decide each part here.
22. **Organization name → the full institutional name, not an acronym** (`NASA` → `National Aeronautics
    and Space Administration`, `Naval Research Laboratory` → `United States Naval Research Laboratory`).
    The validator flags a bare-acronym affiliation (e.g. `ESA` instead of `European Space Agency`) as a
    WARNING with `Suggested fix: expand to the full institutional name`, and does not flag a value that
    includes an acronym alongside the full name (e.g. "European Space Agency (ESA)"). An acronym you cannot
    confidently expand stays as-is with a note so the validator or user can resolve it. A new ROR-keyed row takes ROR's display
    name verbatim; an existing row keeps its stored name, and a stored full name is never flagged STALE
    because a fresh source uses an acronym.
23. **Department or other sub-institutional unit → add it only when it resolves to an Organization row
    HSSI already stores;** otherwise record the institution. ROR does not register most departments, and
    an identifier-less row is permanent and cannot be renamed through the API.
24. **Institution with no ROR → record it with no identifier, and record the negative search** (the query
    forms tried and a positive control), so a later refresh does not re-hunt it.

### E. Organization authors

25. **Detect an organization author** from: a CITATION.cff author with a single `name:` key and no
    `given-names`/`family-names`; a codemeta.json/JSON-LD author with `"@type": "Organization"`; a
    DataCite or Zenodo creator with `nameType: "Organizational"`; or a name that is clearly a group
    (`… Team`, `… Community`, `… Consortium`, `… Collaboration`). Look up its **ROR**
    (`https://api.ror.org/organizations?query=<name>`) and record it as the author identifier; HSSI infers
    org-ness from the `ror.org` identifier, so no other marker exists. Use an ORCID for people and a ROR
    for organization authors; contributors remain person/ORCID-only.
26. **Organization author already stored → send its stored given/family split exactly, with its
    `personId`** (rule 30). Another spelling of the same words would respell the shared row (rule 11).
27. **New organization author with a multi-token name → split on the first whitespace:** first token →
    `givenName`, the remainder → `familyName` ("The SunPy Community" → `The` / `SunPy Community`).
28. **Single-token organization name (e.g. `NASA`) → cannot be encoded;** a new author needs both name
    parts non-empty. Put it on the Ask list; never guess a split.

### F. Order and refresh

29. **Keep the stored author order.** It is stored data; do not reorder stored authors to match a byline or
    a preference. Append new authors in the order of the source that attests them. Identify authors by
    name, never by their position in a dossier list.
30. **The PATCH carries the complete intended author list.** `authors` is replaced wholesale, so an author
    left out is removed from the entry. Send each author whose row stays on the entry with that row's
    `personId` (the ids are in `GET /api/data/software/<uid>/` `authors`, in order): a name sent without
    one binds an arbitrary row with that exact split, not necessarily the entry's own.

## Ask the user only when

- **A NON-PATCHABLE correction to a shared row is needed** — a rename of a stored name or an accent
  removal (rule 11, which includes repairing a legacy blank-given row), an ORCID or bind the API cannot
  apply (rules 15 and 16), the replacement of a wrong stored ORCID (rule 13), an affiliation removal, or a
  ROR for an identifier-less Organization row. The rubric decides the target value; the user decides whether it goes
  through the database workflow. It is a hard blocker for canonical completion until routed.
- **A single-token organization author name** that cannot be split into non-empty given and family names.

## Where to find it, and traps

**Sources, in priority order**
1. The current HSSI record (`GET /api/view/software/<uid>/`, `GET /api/data/software/<uid>/`).
2. CITATION.cff; codemeta.json; `.zenodo.json` and the Zenodo/DataCite record (creators and
   contributors).
3. AUTHORS or CONTRIBUTORS files; the software's citation guidance (`docs/citing.rst`, README).
4. Package metadata (setup.py, pyproject.toml, setup.cfg, package.json).
5. The byline and affiliation block of a refereed paper describing the software.
6. Git commit history, with caution: `git log --format='%an <%ae>' <pin> | sort | uniq -c` over the pinned
   ancestry, and every `.mailmap` under `repos/` for aliases. Use it to resolve names, never to promote
   committers.

**Cross-check and search.** Cross-check the metadata against all of CITATION.cff, codemeta.json,
AUTHORS/CONTRIBUTORS, `.zenodo.json` and package metadata where they exist. Search for unlisted authors by
comparing every source of author information against the metadata, including CONTRIBUTORS files and git
shortlog patterns.

**Identifier formats and verification**
- Author identifiers are full URLs: an ORCID (`https://orcid.org/XXXX-XXXX-XXXX-XXXX`) for a person, a
  ROR (`https://ror.org/XXXXXXXXX`) for an organization author. A `ror.org` author identifier is not an
  error and not a malformed ORCID; check that it resolves to that organization.
- Affiliation identifiers are full ROR URLs (Fields 6, 11 and 25 share this format).
- Verify every ORCID resolves to the right person, and every ROR to the right organization.
- ORCID search: use the fielded query
  `https://pub.orcid.org/v3.0/expanded-search/?q=given-names:<G>+AND+family-name:<F>` with
  `Accept: application/json`, and run a positive control beside it. A bare-name query ORs its terms and
  proves nothing either way. `/person` carries primary, credit and other names; the search index's
  institution is not the employment record, so read `/employments`.
- ROR search: use the v2 API. Names live in `names[{value, types}]`; there is no top-level `name`, so
  reading `name` makes an existing record look empty. Run a positive control in the same query set.

**Traps**
- An ORCID that no Person carries, sent without `personId`, creates a new Person unless, on a PATCH,
  exactly one current author of the entry has no identifier and the same full name; then it attaches to
  that author, even when it was sent for someone else (rule 16). A full name that differs in any word, an
  author new to the entry with no such namesake on it, and every POST get a new Person, even when an
  identifier-less row of that name exists elsewhere; only a PATCH's `personId` selects that row (rules 15
  and 16).
- A name sent without an identifier or `personId`, and with a given name, binds only on an exact,
  case-sensitive given+family match; any spelling, case or split difference mints a duplicate.
- A `personId` naming the wrong row fails only when that row's name or identifier conflicts with what is
  sent; a namesake's identifier-less row of the same full name binds without error and takes the ORCID.
- The same person can appear under several commit identities (`, Ph.D` suffixes, numeric noreply
  prefixes, machine hostnames); treat none as a second person.
- A GitHub account whose login equals a stored string is often someone else.
- `.zenodo.json` gives one affiliation string per creator; several institutions are often packed into it
  and HSSI stores only what is sent.
- Zenodo's GitHub integration builds creators from account names; a later deposit built from CITATION.cff
  supersedes those handles.
- A Zenodo deposit's creator list is a snapshot; it does not prove a contributor absent from it was
  excluded, and it does not license expanding the list from the commit graph.
- Two ORCID queries differing only by a name variant (`Josh`/`Joshua`) can each return one record for
  different people.
- Near-miss RORs: a campus or academy of the same university, a company sharing a name (SciVision Biotech
  Inc.), a successor body that does not list the historic name among its aliases.
- The DataCite rendering of an old deposit may put `Ph.D.` in `givenName` and the whole name in
  `familyName`.

## Payload and roundtrip notes

- **Handle authors** are sent as `{"givenName": "<login>", "familyName": "(GitHub)"}` (or `(Username)`)
  with no `identifier` and no `affiliation`. Sent without `personId`, an identifier-less Person binds by an
  exact, case-sensitive given+family match, so the login's capitalization and the parenthesized platform
  label must be reproduced exactly or a duplicate row is created.

- **Shape:** `authors` is an array of Person objects
  `{givenName, familyName, identifier, affiliation: [{name, identifier}, ...]}`, and on a PATCH an
  optional `personId` (*Selecting a row by `personId`*); a POST rejects any `personId` key with a 400,
  even an empty or `null` one. `familyName` is required and non-empty. So is `givenName`, except on a
  PATCH for an author stored with an empty given name (see *Empty stored given name*).
- **Organization authors.** An author may be an organization (a lab, consortium, or institution credited
  as an author) rather than a person. To submit one, put its **ROR URL** in `identifier` (e.g.,
  `https://ror.org/03c3r2d17`). HSSI derives org-ness server-side purely from the `ror.org` identifier —
  there is no separate flag — and renders the author as a schema.org `Organization`, with its
  affiliations as `parentOrganization`. A new organization author still needs both `givenName` and
  `familyName` non-empty, and the stored name is `givenName + " " + familyName`, so split a new org name
  as rule 27 says. A single-token org name can't satisfy the non-empty `familyName` rule — flag it to the
  user rather than guessing a split. This applies to **authors only**; contributors remain
  person/ORCID-only.
- **Person resolution.** "The same full name" means the same words in the same order, ignoring
  capitalization, accents and hyphens, however `givenName` and `familyName` split them. An accent is a
  mark Unicode can separate from its letter: `é` matches `e`, but `ø` and `ł` do not match `o` and `l`.
  - *With `personId`* (PATCH only): the row with that id, whatever entries it serves; see *Selecting a
    row by `personId`*.
  - *With an identifier:* match on the identifier only. A hit keeps its names, except that a blank given
    or family name is filled and, on a PATCH, sent names that spell the same full name replace the
    stored ones (*Name changes*). On a miss, a PATCH attaches the identifier to this entry's one current
    author with no identifier and the same full name, whichever author item sent it (two or more such
    authors are a 400 for the whole PATCH). Every other miss creates a new Person, even when an
    identifier-less row of that name exists elsewhere: any POST, and any PATCH where no identifier-less
    current author has that full name.
  - *With neither:* exact, case-sensitive given+family match, else create. Among rows with that exact
    split the binding is arbitrary.
  - *Empty or missing `givenName`* on a PATCH without `personId`: see *Empty stored given name*.

  So, without `personId`, sending name + ORCID binds the row that carries the ORCID. When no row carries
  it, a PATCH attaches it to the entry's own identifier-less row of the same full name, and anything else
  creates a Person. With `personId`, the ORCID goes to the selected row or the PATCH fails.
- **Name changes.** A PATCH gives a Person it resolves by identifier, or selects by `personId`, the sent
  names when they spell the same full name, so one PATCH can change the split, capitalization, accents
  and hyphens together. Sent names with fewer accent marks in total than the stored ones are not applied
  at all, with a 200. A different full name is never applied: by identifier it
  returns 200 and changes nothing beyond filling a blank name part, and with `personId` it is a 400. A
  POST changes no stored name beyond filling a blank part. So send a kept author under its stored names
  exactly unless rule 11 corrects them: any other spelling sent with an identifier or `personId`
  rewrites the shared row.
- **Selecting a row by `personId` (rules 11, 15, 16 and 30).** On a PATCH, an author item with `personId`
  binds the existing Person row with that id, whatever entries it serves, and never falls back to a name
  match or creates a row. Every author whose row stays on the entry goes this way (rule 30), and so does
  an author new to the entry whose row already exists (rule 16).
  - The id must name an existing Person, and the sent names must spell its full name; otherwise the whole
    PATCH is a 400, and a name error gives the stored name. An empty or missing `givenName` is accepted
    only for a row stored without one.
  - A sent `identifier` fills the row's empty one or repeats its stored one; one that differs from the
    stored identifier, or that another Person holds, is a 400. Omitted or empty, it leaves the row's
    identifier as it is.
  - The row takes the sent names (*Name changes*).
  - Take the id from the `authors` of `GET /api/data/software/<uid>/` or `GET /api/view/software/<uid>/`
    for a row on a visible entry, else from
    `GET /api/models/Person/rows/all/?columns=id,given_name,family_name,identifier`. Before sending it
    for a row new to the entry, check the row's other entries (*Stored-row sharing*), since a namesake's
    row binds without error. After the PATCH, verify that the id sits in
    `GET /api/data/software/<uid>/` `authors` at that author's position.

  A POST rejects `personId`, so a new submission sends such an author without the ORCID (rule 16).
- **Affiliations accumulate.** Each sent affiliation is `.add()`ed to whichever Person row was resolved;
  re-sending an existing affiliation inserts nothing, and nothing is ever removed.
- **Organization resolution** (affiliations): with an identifier, match on the identifier only, else
  create with the name exactly as sent — an existing identifier-less row of the same name is not reused
  and becomes a duplicate; without an identifier, `name__iexact`, else create. Before sending a ROR for a
  name the catalogue already holds, check for an identifier-less row of that name.
- **Organization-name sanity.** For `affiliation[].name`, if a value is a bare acronym (e.g., `ESA` rather
  than `European Space Agency`), surface it in the verification report and ask the user before
  submitting. Do not auto-expand — the value should already be expanded upstream by the extractor.
- **Full replacement.** `authors` is replaced by the submitted list (`.set()`), in the submitted order.
  Each Person row may appear in it once: two items that resolve to the same row, such as the same
  `personId` or identifier twice or the same name twice, are a 400 for the whole request, on a POST or a
  PATCH.
- **Empty stored given name.** On a PATCH, send an author stored with an empty given name with its
  `personId` (rule 30), `givenName` empty or omitted, and the stored family name. Without `personId`, it
  resolves only to this entry's one current author with an empty given name and the same family-name
  words; none or several is a 400, and a sent identifier fills only an empty one that no other Person
  holds. A Person with an empty given name is never created, and a POST rejects an empty `givenName`. A
  non-empty `givenName` for that author is a different name: it lands only as a rule 11 respelling of the
  same words (a row storing the whole name `Jane Doe` as its family name, sent as `Jane` / `Doe`).
- **Identity matching does not erase attribute differences.** Match authors by ORCID and then normalized
  name; for each matched author, union affiliations by ROR and then normalized organization name. Match
  organizations by their stable identifier before normalized/canonical name, then separately compare
  their labels and nested values. Do not mark two objects fully MATCH merely because their identifiers
  match.
- **Respect PATCH capability limits.** The endpoint reuses existing people and organizations and never
  renames them: a Person keeps its words, an Organization its nonblank name. On a PATCH it can fill the
  empty ORCID of a row it selects by `personId` (rules 15 and 16), and give such a row another spelling of
  the same words unless the sent names carry fewer accents in total (rule 11). It can add author
  affiliations but cannot remove an existing affiliation. Classify a desired rename or accent removal, an
  ORCID or bind those rules cannot apply, a stored ORCID's replacement, or a nested affiliation removal as
  NON-PATCHABLE, omit it from `patch`, and make it a hard blocker for canonical completion until the user
  routes it through the CSV/manual database workflow. Top-level relationship removals remain possible
  through a complete approved replacement list.
- **Refresh matching.** During refresh/enrich, match and dedupe organization authors by their ROR
  exactly as ORCID is used for people, and don't flag a `ror.org` author identifier as invalid.
- **Stored-row sharing.** A Person row is shared by every entry it serves, so an ORCID or a name change
  that a PATCH applies shows on all of them, as a database-side correction does (an added affiliation
  does too; rule 19). Before sending an ORCID or a name change for an existing row, or a `personId` for a
  row new to the entry, or routing a correction to one, find the row's other entries (its id in the
  `authors` of each listed entry's `GET /api/data/software/<uid>/`) and check they are this person's.

## Worked examples

- **A wrapper over a vendored C library (WMM2015).** The Python package ships NOAA's Geomagnetism Library
  unmodified, whose header says it was written by two named people. Rule 4 credits the wrapper's author
  and those two; the contact names in the address blocks, the routine-level credits, the Fortran-original
  credit and the `$Author:` keyword are recorded as excluded with their roles.
- **Verified ORCIDs for identifier-less stored authors (PyGS, PyAuroraX).** Fielded ORCID searches with
  controls tie each author to a single record whose employment and works match. The stored Person rows
  carry no identifier, so rule 15 sends each ORCID with the stored row's `personId`, and the row takes it
  instead of a new Person being created. A third author whose five same-name
  records are all other people gets no identifier (rule 14).
- **A split and a capitalization (CCSDSPy, Kamodo).** CCSDSPy's row stores `Daniel da` / `Silva` with an
  ORCID whose record gives `Daniel` / `da Silva`: the same words split differently, so rule 11 sends the
  corrected split with the row's `personId` and one PATCH re-splits the row. Kamodo's `Darren de` / `Zeeuw`
  for `Darren` / `De Zeeuw` also changes a capital, which leaves the same full name, so it lands the
  same way.
- **An author new to the entry who already has a row (DKIST User Tools).** Thomas Robitaille is added to
  DKIST User Tools with a linked ORCID that no row carries, while the catalogue holds an identifier-less
  `Thomas` / `Robitaille` row that serves SunPy, which credits the same person. Rule 16 selects that row:
  one PATCH sends the author with the row's `personId`, its stored names and the ORCID, which then shows
  on SunPy too.
- **GitHub handles in a Zenodo creator list (georinex, sunpy).** Handles that resolve to people through
  commits git-authored under personal names are recorded as those people. A creator whose every artifact
  carries only the handle and a noreply address encoding its login (`izzydrewlynn
  <38845559+izzydrewlynn@users.noreply.github.com>`; sunpy's `eebbaaf`, `OussCHE`) is recorded as
  `izzydrewlynn` / `(GitHub)` under rule 2 — an author, with no human name asserted. Named committers
  missing from the creator list are not added (rule 5).
- **A username with no platform account (pyspedas).** `CITATION.cff` lists `rale8469` with the literal
  family name `GithubUser`; the commit API attributes its commit to no account and no such GitHub user
  exists, but the commit address's local part is the handle. Rule 2 records `rale8469` / `(Username)`,
  never the upstream `GithubUser` literal; two other handles in the same roster, proven through noreply
  addresses, are recorded with `(GitHub)`, and three resolve to real people.
- **A years-stale affiliation (hissw).** The software was begun at a university the author has since
  left, and his Person row serves several entries. Rule 19 keeps that university off; his stored past
  affiliation from the period of the catalogued releases stays (rule 17).
- **A shorter stored name (OCBpy).** HSSI stores `Jone` / `Reistad` while the project writes
  "Jone P. Reistad". The stored form matches an ORCID other-name, so rule 10 keeps it and the dossier
  records which source each form matches.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 225-240 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
- Person resolution (rules 1, 10, 11, 13, 15, 16, 26 and 28, the traps and the payload notes)
  re-verified against hssi-website `f3f1a2ea` (#146) on 2026-10-28.
