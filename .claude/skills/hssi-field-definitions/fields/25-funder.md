# Field 25 — Funder

**Level:** OPTIONAL · **API:** `funder[]` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.5 (name, abbreviation) · **Field-search code:** `funder`

## What it is

**Type:** Multi-entry nested group

**What it is:** A person or organization that supports (sponsors) something through some kind of financial contribution.

**How to fill it:** The name of the organization that provided the funding (e.g., National Aeronautics and Space Administration). Avoid acronyms and enter one organization per field.

**Sub-fields:**
- **Organization** (RECOMMENDED): Funder name
- **Funder Identifier** (RECOMMENDED): ROR identifier if available (e.g., https://ror.org/027ka1x80)

## Why it exists

A funder value answers "which agencies paid for this software?" — for a program manager tracing the
impact of their investment, and for a user searching the catalogue by agency. A missing funder hides a
true, useful attribution; a padded one (the salary sources of individual authors, a citing paper's
sponsor, an input mission's budget) gives a wrong answer to that question on every search it matches.

## How it appears on the site

- **Detail page:** a "Funders" item in the "Licensing & Funding" section, one tag per funder, linked to
  the funder's identifier (or the organization's website) when one is stored.
- **Free-text search:** tier T4.5 on funder name and abbreviation.
- **Field search:** `funder:"…"` matches the funder name.
- **Filter tab:** none.
- **JSON-LD:** the `funding` items are built from the entry's Award rows (Field 26), each with its
  `Award.funder` when set.

## Rubric: include / exclude

Decide each candidate funder with rules 1–8, top to bottom — **stop at the first rule that fires**. Then
shape each recorded funder with rules 9–10, and check the entry as a whole with rules 11–12.

**The funding rule: record a funder/award only when a source attributes funding to this software, or to
the project or center whose product this software is (CITATION/README/Zenodo funding, a paper naming the
software or its producing program); a statement funding a person ("X is supported by grant Y") never
qualifies, even when X wrote the software.**

1. **Stored funder that a qualifying source supports → keep.** Keep a stored full name even when a fresh
   source uses an acronym; it is not STALE.
2. **Stored funder that no qualifying source supports → remove it** (a top-level removal through the
   complete replacement list, shown in the diff for approval), and record it as a rejected alternative with
   its actual role.
3. **Person-level support → exclude.** "X is supported by…", "the research of X was supported by…", an
   author's fellowship or salary line, even when X wrote the software.
4. **A citing or describing paper's own funding → exclude.** A citing paper's funder is not the software's
   funder. A describing paper's funding counts only through a sentence that attributes it to the software
   or its producing project (rule 8).
5. **Funding of an input → exclude:** a predecessor model the package wraps, an input mission's or data
   facility's own funding, a validation-only data service.
6. **An employer's institutional sponsor → exclude.** A cooperative agreement that funds a facility or
   laboratory as the authors' institutional home (NSF's agreement for NCAR) is not a grant to this
   software, even when that institution holds the copyright.
7. **A facility, mission, program or project named as the source of support → not a funder by itself.**
   Record the agency that funds it when the source names that agency; otherwise record nothing and keep
   the name as a rejected alternative (substituting the operator is inference). A named program or
   project with an award number belongs in Field 26. Exception: a stored mission or program row that the
   project's own funding statement lists as a funder is kept under rule 1.
8. **Qualifying source → add one entry per organization.** Qualifying sources: the project's own
   CITATION.cff, codemeta.json, README or acknowledgements file, `.zenodo.json`/Zenodo/DataCite
   `fundingReferences`; a paper or award record that names the software; a statement that funds the center,
   platform or program whose product the software is, when a source also attests that the software is that
   center's or program's product (the two links may come from one peer-reviewed source). An award whose
   funder database record names the software as its subject also qualifies its awarding agency.
**Form of each recorded funder**

9. **Name the organization in full, one per entry.** Expand acronyms (`NASA` → `National Aeronautics and
   Space Administration`); split a value that combines several organizations into separate entries; drop a
   parenthetical acronym or program (`Technical University of Denmark (DTU, Swarm DISC Program)` →
   `Technical University of Denmark`). A new ROR-keyed row takes ROR's display name verbatim, which also
   corrects a source's slip (`Canadian Foundation for Innovation` → `Canada Foundation for Innovation`). If
   an acronym cannot be confidently expanded, leave it as-is and note it so the validator or user can
   resolve it.
10. **Identifier → the funder's ROR.** Choose among same-name ROR records by country and role (the United
    States Office of Naval Research is `https://ror.org/00rk2pe57`; `https://ror.org/01awap711` is the
    United Kingdom body of the same name). No ROR → no identifier, with the negative search recorded.
**The entry as a whole**

11. **Every funder of a recorded award (Field 26) appears here.** A funder may stand without an award; an
    award never stands without its funder.
12. **Nothing qualifies → leave the field empty and record why:** the sweep that found nothing (pattern,
    scope and a positive control), and every rejected candidate with its actual role, so a later refresh
    does not reintroduce it from Crossref.

## Ask the user only when

- **A NON-PATCHABLE correction to a shared Organization row is needed** — a rename, or a ROR for a stored
  identifier-less row. The rubric decides the target; the user decides whether it goes through the
  database workflow.

## Where to find it, and traps

**Sources, in priority order**
1. The project's own funding statement: README acknowledgements, an `ACKNOWLEDGEMENTS` file,
   CITATION.cff, codemeta.json (`funding`, `funder`), `.zenodo.json` `grants`.
2. The DOI record: DataCite `fundingReferences`, Zenodo `grants`.
3. **A paper's Acknowledgments and Data Availability Statement are the best source for Fields 25/26**, and
   are where code/data DOIs surface. Prefer the reference publication (Field 14); read its whole funding
   section and its author-contribution statement, which says who built the software.
4. Funder award databases, to confirm the awarding agency and the award's subject: USAspending, the NSF
   Awards API.

**Why the acknowledgments beat Crossref.** Crossref's funding metadata flattens distinct tiers into one
undifferentiated list — support for the software's authors, an input mission's own funding, and a
validation-only data service's funding can all appear together, and it reports the paper's funding, not
the software's. Record only what funded this software; note the others' actual roles as rejected
alternatives, so a later refresh doesn't reintroduce them from Crossref.

**Verification**
- ROR identifiers are full URLs: `https://ror.org/XXXXXXXXX` (Fields 6, 11 and 25 share this format).
  Use the ROR v2 API (`names[{value, types}]`; there is no top-level `name`).
- USAspending `spending_by_award` takes one `award_type_codes` group per query (grants `02`–`05`,
  contracts `A`–`D`); a mixed list returns an error with no `results` key. Query the punctuation-stripped
  award number, with a nonsense-id control.
- A publisher page that returns 402/403 is usually bot-blocking; a browser often renders it.

**Traps**
- A funding section can hold only person-support clauses; count them before reading the section as
  software funding.
- A paper co-author who is not a software author can be the one a clause funds.
- A copyright holder is not a funder.
- A missions heading inside a project's own "provided funding" statement names sources of money, not data
  sources; do not promote those missions into Fields 31/32 from it.

## Payload and roundtrip notes

- **Shape:** `funder` is an array of Organization objects `{name, identifier}`, replaced wholesale by the
  submitted list.
- **Resolution:** with an identifier, match on the identifier only, else create with the name exactly as
  sent — an existing identifier-less row of the same name is not reused and becomes a duplicate; without
  an identifier, `name__iexact`, else create. Before sending a ROR, check for an identifier-less row of
  that name. A matched row's nonblank name is never overwritten, so a funder rename is NON-PATCHABLE.
- **Organization-name sanity.** For `funder[].name`, if a value is a bare acronym (e.g., `ESA` rather than
  `European Space Agency`), surface it in the verification report and ask the user before submitting. Do
  not auto-expand — the value should already be expanded upstream by the extractor. Also flag funder
  entries that combine multiple organizations into one value (the form expects one organization per
  entry). The validator flags a bare-acronym funder as a WARNING with `Suggested fix: expand to the full
  institutional name`, and does not flag a value that includes an acronym alongside the full name (e.g.,
  "European Space Agency (ESA)").
- **Web form differs.** The web submission and edit forms resolve organizations by identifier, then an
  exact case-sensitive name, and on creation move a parenthetical into `abbreviation`, stripping it from
  `name`. The API path used by agents does not strip; send the name without the parenthetical.
- **Organization rows are shared** across authors' affiliations, publishers and funders of every entry.
- **Award.funder is separate.** The funder shown beside each award on the detail page is `Award.funder`,
  which no API path can write; this field does not set it (see Field 26).

## Worked examples

- **Only person-level support (sami2py).** The reference paper's funding section has four clauses, each
  "X is supported by…", and one funds a paper co-author who never touched the code; NSF funded the
  predecessor Fortran model. Rules 3 and 5 fire; the field stays empty and NASA and the Office of Naval
  Research are recorded as considered and not determinative.
- **The producing center's funding (Kaipy).** One peer-reviewed paper says the package was developed by
  the NASA DRIVE Center for Geospace Storms and that the Center is funded by NASA under award
  80NSSC22M0163. Rule 8 records NASA; NSF, named for the NCAR facility that employs some authors, is
  excluded by rule 6.
- **Platform funders from the describing paper (PyAuroraX).** The repository and deposit name no funder;
  the paper's developers acknowledge "the AuroraX funding sources" for the platform and library they
  built. Rule 8 records the four organizations under their ROR display names; Crossref's single funder,
  which paid for the paper's lead authors, is rejected under rule 4.
- **A facility named as a source of support (ndcube).** The acknowledgment names NASA's HDEE program,
  the DKIST telescope and a Solar Orbiter/SPICE grant. NASA covers the first and third; DKIST is a
  facility with no ROR, so rule 7 records nothing for it, and Solar Orbiter/SPICE goes to Field 26 as an
  award.
- **A citing paper's funders (pysatCDF).** The pysat paper's acknowledgments name NASA and NSF and list
  pysatCDF among the software used. Rule 4 excludes them; the repository states the project is
  volunteer-driven, so the field is evidenced-empty.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 624-636 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
