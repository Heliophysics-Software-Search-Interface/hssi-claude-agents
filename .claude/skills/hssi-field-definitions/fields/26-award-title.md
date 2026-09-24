# Field 26 — Award Title

**Level:** OPTIONAL · **API:** `award[]` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.5 (name), T4.6 (identifier) · **Field-search code:** `award`

## What it is

**Type:** Multi-entry nested group

**What it is:** The title of the specific grant or award that funded the work.

**How to fill it:** Copy the full title of the award.

**Agent guidance — where funding information comes from.** Prefer the reference publication's **Acknowledgments** section, and read its **Data Availability Statement** too. Crossref's funding metadata flattens distinct tiers into one undifferentiated list — support for the software's authors, an input mission's own funding, and a validation-only data service's funding can all appear together. Record only what funded *this software*; note the others' actual roles as rejected alternatives, so a later refresh doesn't reintroduce them from Crossref. This applies equally to Field 25.

**Sub-fields:**
- **Award Title** (OPTIONAL, multi-entry): Full award title
- **Award Number** (RECOMMENDED): Identifier associated with the award (e.g., NNG19PQ28C). Used by funding agencies to track impact.

## Why it exists

The award tells a program manager which grant produced this software, and lets a reader look the grant up
by its number. A missing award loses that trace; an award that funded an author's salary, a citing paper
or an input facility claims impact the grant did not have; an unlookupable number (a typo, a solicitation
id) is a dead end.

## How it appears on the site

- **Detail page:** a "Funding Awards" item in the "Licensing & Funding" section, one line per award: the award
  name, then the award identifier in parentheses when stored, then "- " and the award's funder
  (`Award.funder`) when that is set.
- **Free-text search:** award name at tier T4.5, award identifier at tier T4.6.
- **Field search:** `award:"…"` matches the award name only.
- **Filter tab:** none.
- **JSON-LD:** each award becomes a `MonetaryGrant` in `funding` with its name, identifier, and funder
  when `Award.funder` is set.

## Rubric: include / exclude

Decide each candidate award with rules 1–8, top to bottom — **stop at the first rule that fires**. Then
settle each recorded award's title with rules 9–12 and its identifier and binding with rules 13–15.

**The funding rule: record a funder/award only when a source attributes funding to this software, or to
the project or center whose product this software is (CITATION/README/Zenodo funding, a paper naming the
software or its producing program); a statement funding a person ("X is supported by grant Y") never
qualifies, even when X wrote the software.**

1. **Stored award that a qualifying source supports → keep.**
2. **Stored award that no qualifying source supports → remove it** from the entry's list (shown in the
   diff for approval) and record it as a rejected alternative with its actual role.
3. **Person-level support, a citing paper's funding, or an input's funding → exclude** — the same tiers
   Field 25 rules 3–6 exclude (an author's grant, a citing or describing paper's own funding, a
   predecessor model's or input facility's award, an employer's institutional agreement).
4. **A solicitation number → exclude.** A NASA ROSES announcement id (`NNH20ZDA001N`) identifies an annual
   call, not an award.
5. **An HPC allocation or account code → exclude** (`#PBS -A` strings such as `P28100045`).
6. **A number that co-occurs with the software's center in a few papers but belongs to a different
   program → exclude;** check what the award record says it funds.
7. **Qualifying source names the award → add.** One entry per award the source attributes; the stored
   list is the entry's complete set, so a later list that names only some awards detaches the others.
8. **Nothing qualifies → leave the field empty and record why.** An award with no matching evidence is
   never supplied as a default. A funder recorded in Field 25 without any award is legitimate.

**Title**

9. **An award always has a title;** an award with no title cannot be stored, so a number without a title
   is lost. Take the title, in order, from: the funder's award record (NSF Awards API, USAspending
   description); the source's own name for the award or program ("TIMED/GUVI Project", "NASA DRIVE Science
   Center for Geospace Storms", "Space Precipitation Impacts (SPI)"); else a descriptive label
   `<funder full name> grant`. Record in the dossier that a descriptive title is not the official one, so it
   is neither "corrected" to empty nor mistaken for a formal title.
10. **Clean an award-database description minimally:** drop a leading internal accounting code
    (`E014042 - `); restore ordinary case from an all-capitals rendering only when an independent source
    gives the ordinary-case title; otherwise keep the rendering. Do not append the award number to the
    title; it renders beside the title.
11. **Title over 128 characters → drop a leading administrative prefix** (`Collaborative Research: `) and
    keep the full title verbatim in the dossier. Still over 128 → Ask.
12. **Do not read the software's functionality out of an award title**; it describes the funded research.

**Identifier and binding**

13. **Award number → the form an existing Award row carries.** Look up existing rows on the
    punctuation-stripped key (`N00173-19-1-G016` ↔ `N00173191G016`); a hit binds that row, and a
    differently punctuated number would create a duplicate. With no existing row, use the form the source
    gives.
14. **Correct a typo in a source's number only when the agency's own record resolves the corrected number
    and the uncorrected one resolves to nothing** (NSF `125908` → `1259508`), and record both in the dossier.
15. **Existing Award row → bind it and accept its stored title.** A matched row keeps its name; a better
    title for it is a NON-PATCHABLE rename of a shared row (see the Ask list). **No existing row → send
    the title, number and funder the rubric chose**; the PREPARE report states that EXECUTE will create
    the row, and approval of the exact payload covers that creation.

## Ask the user only when

- **A shared Award row needs a rename or a funder link.** Award rows are shared across software entries,
  so a rename changes every entry on the row; it is NON-PATCHABLE and goes through the database workflow.
  Name every entry the row serves (query the row's `softwares` reverse relation, not the name string).
- **A title is still over 128 characters** after rule 11.

## Where to find it, and traps

**Sources, in priority order**
1. The project's own funding statement (README acknowledgements, an `ACKNOWLEDGEMENTS` file,
   CITATION.cff, codemeta.json, `.zenodo.json` `grants`).
2. DataCite `fundingReferences` and Zenodo `grants` for the DOI.
3. **A paper's Acknowledgments and Data Availability Statement are the best source for Fields 25/26**, and
   are where code/data DOIs surface. See Field 25 for why they beat Crossref's funding block.
4. The funder's award record, for the title, recipient and subject: USAspending
   (`POST https://api.usaspending.gov/api/v2/search/spending_by_award/`), the NSF Awards API, ADS proposal
   records.

**Verification**
- USAspending `spending_by_award` takes one `award_type_codes` group per query (grants `02`–`05`,
  contracts `A`–`D`); a mixed list returns an error with no `results` key — print `message`. Query the
  punctuation-stripped number and run a nonsense-id control.
- NSF award records print two spaces after `Collaborative Research:`; a stored single space is
  whitespace normalization, so never present a stored title as a byte-exact quotation.
- Measure every title's length before approving a patch.

**Traps**
- Crossref's funder block flattens tiers (see Field 25).
- An identifier-less Award row binds on a case-insensitive exact title, so a common project name
  (`Space Precipitation Impacts (SPI)`) silently attaches this entry to another entry's award row.
- A placeholder title (`U.S. Naval Research Laboratory award`) can sit on several rows with different
  numbers; the number, not the name, identifies the row.

## Payload and roundtrip notes

- **Shape:** `award` is an array of Award objects `{name, identifier}`; the API field is `award`, **not**
  `awardTitle`. `identifier` is a string, not validated as a URL. The list replaces the entry's awards
  wholesale.
- **Resolution:** with an identifier, match on the identifier only; on a hit the row is reused and the
  payload `name` is discarded; on a miss a new row is created with that name and identifier. Without an
  identifier, `name__iexact`, else create.
- **`name` is required** and non-empty; an award object with no name 400s.
- **Caps:** `Award.name` and `Award.identifier` are 128 characters; the serializer does not check length,
  so an over-length value fails at the database write with a 500 and rolls back the whole PATCH.
- **Award.funder is DB-only.** It renders beside the award on the detail page and feeds JSON-LD, but no API
  path writes it; a newly created Award row has no funder until a database-side correction sets it.
- **Renames are NON-PATCHABLE.** A matched Award row's name is never overwritten through the API.

## Worked examples

- **An award that names the software (PyGS).** The README acknowledges NASA grant 80NSSC23K0256, and
  USAspending's description for it is "E014042 - PYGS: ANALYSIS TOOLS FOR SMALL-SCALE MAGNETIC FLUX ROPES
  …". Rules 7 and 10 give the title without the accounting prefix, in the ordinary case the ADS proposal
  record uses. The stored row carried a synthesised name, so the better title was a shared-row rename.
- **Typo'd numbers in the project's own file (pysat).** `ACKNOWLEDGEMENTS.md` lists NSF `125908` and NASA
  `80NSSC18K120`; the agencies return nothing for either, and real awards to the same PI for `1259508`
  and `80NSSC18K1203`. Rule 14 records the corrected numbers; awards with no public title carry the label
  `NASA grant` (rule 9).
- **A solicitation id and person support (sami2py).** The paper gives "JS is supported by NASA
  NNH20ZDA001N-NASA" and "The research of JH was supported by NSF (AGS-1931415)". Rule 3 excludes both
  as person support, and rule 4 excludes the first independently as a solicitation number.
- **A hyphenated number (OMMBV).** The README gives `N00173-19-1-G016`; an Award row already stores
  `N00173191G016`. Rule 13 sends the stored form, which binds the existing row instead of creating a
  duplicate.
- **A title over the cap (amisrsynthdata).** NSF's title for award 2027300 is 152 characters. Rule 11
  drops the leading `Collaborative Research: `, landing at 128, and the dossier keeps the full title.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 637-651 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
