# Field 16 — Keywords

**Level:** OPTIONAL · **API:** `keywords[]` · **Change class:** dynamic
**Vocabulary:** `/api/models/Keyword/rows/all/` — (open)
**Filter tab:** none · **Free-text search tier:** T2 · **Field-search code:** `keyword`

## What it is

**Type:** Multi-select dropdown (allows custom entries)

**What it is:** General science keywords relevant for the software (e.g., from the AGU Index List or the UAT) not supported by other metadata fields.

**How to fill it:** Begin typing the keyword in the box. Keywords from UAT and AGU Index lists will appear in a dropdown. Choose correct one(s) or type in if not listed.

**This is the only genuinely open vocabulary in the form.** `_get_or_create_keyword` creates a row
for any keyword not already present (case-insensitive match), so a new keyword will never fail a
submission — but it also means typos and un-split comma-delimited strings become permanent rows.
Enter **one keyword per entry**, lower-case, and check the live list first to reuse an existing row
rather than minting a near-duplicate.

<!-- vocab:Keyword begin -->
**Example Values** — *20 of 483 rows on `https://hssi.hsdcloud.org` / 572 on `http://localhost`, sampled 2026-07-29. Full list at `/api/models/Keyword/rows/all/`.*

- analysis
- batsrus
- cdf
- charge exchange
- coordinates
- csv
- esa
- heliophysics
- heliosphere
- magnetohydrodynamics
- magnetosphere
- physics
- plasma
- python
- solar orbiter
- solar wind
- space
- space physics
- space weather
- swmf
<!-- vocab:Keyword end -->

## Why it exists

Keywords are the second-ranked free-text search tier, just behind name and description, so they decide
whether a searcher who types a domain term — `hmF2`, `neutral winds`, `keogram` — finds this software
near the top of the results. The field exists for exactly the terms the structured fields cannot carry:
the quantities computed, the techniques and products named by the community, the project's own
vocabulary. A keyword that restates another field adds nothing; a registry bookkeeping tag (`specific`,
`general`) or an unsupported term (`orbit` on an imager library) misdirects everyone who searches it; a
misspelling makes the software findable only by someone who repeats the typo.

## How it appears on the site

- **Detail page:** a "Keywords" section with one plain (unlinked) tag per keyword, showing the stored
  `name` as written.
- **Filter:** none.
- **Free-text search:** tier T2 (`keywords__name`), ranked above the controlled-vocabulary fields (T3).
- **Field search:** `keyword:"…"` matches `keywords__name__icontains`.
- **JSON-LD:** each keyword is emitted in `keywords` as a `DefinedTerm` carrying its name.
- **The `/api/view/` JSON and the ORM's `str()` title-case keywords** (`Keyword.__str__` returns
  `name.title()`); the stored `name` is what the detail page shows and what every comparison must use.

## Rubric: include / exclude

Apply per candidate term, top to bottom. Rules 1–10 decide whether a term belongs — stop at the first
of them that fires, except that a **project-declared** term is tested under rule 9 before rules 6–7,
which apply only to terms the extractor proposes. Every term that belongs then passes through rules 11–12, which decide the row it
binds (stop at the first that fires). Rules 13–14 cover incumbents and emptiness.

1. **One keyword per entry.** Split comma- or semicolon-delimited strings into separate terms before
   applying anything else. Fires on: a candidate containing a list.

2. **PyHC scope tags never belong.** `general` and `specific` are the registry's "Span" facet ("the user
   scope of a project"), and `specific` is sometimes a fragment of "instrument-specific". They say nothing
   about the software to a catalogue visitor. Fires on: either term, from any source — exclude, and remove
   it from a stored record.

3. **Registry domain tags are kept only when the software itself touches that domain.** PyHC "Science
   Area" tags (`ionosphere_thermosphere_mesosphere`, `magnetosphere`, `solar`, …) are inherited from the
   registry taxonomy and propagate across unrelated entries. Keep one only when the pinned code or the
   project's own description works in that domain; **never because the registry lists it**. Do not add the
   underscore-joined machine spelling as a new keyword; a stored one that passes the domain test is kept.
   Fires on: a tag whose only source is the registry — exclude it unless the domain test passes.

4. **Unsupported terms are excluded.** A term with no support in the software (a word-anchored sweep of
   the pinned tree returns nothing, and no project description uses it) misdirects the searcher. So does a
   term that promises something the record lacks — `idl` on software with no IDL code, when the
   IDL-adjacent facts already sit in Fields 18 and 29. Fires on: a term whose claim the evidence does not
   support.

5. **Correct a misspelling to the project's spelling.** A stored typo (`norther lights`) is replaced with
   the spelling the project uses (`northern lights`), even when that mints a row; the misspelled row is
   left behind unused. Fires on: a stored keyword that misspells a term the project itself writes.

6. **Do not add a keyword that restates another field.** Keywords carry meaning not carried by other
   fields. A derived candidate that only repeats a Field 4 functionality (`empirical model`), a Field 5
   region, a Field 13 language (`fortran`), a Field 17 data source, a Field 22 phenomenon (`x-ray`), or a
   Field 31/32 instrument or mission (`proba2`, `goes-r`) is not added. Fires on: a proposed addition whose
   meaning another field already carries.

7. **Do not add a dependency, an institution, or a catalogue-wide generic.** A dependency's name
   (`ndcube`) belongs to Fields 29/30; an institution tag (`noaa`) is not a subject; `python`,
   `solar physics`, `space` are true of much of the catalogue and distinguish nothing. Fires on: a proposed
   addition of one of these kinds.

8. **Do not bind a different concept because the strings are close.** `differential emission measure` is
   a different quantity from `emission measure`; a row one word away is a candidate only if it names what
   the software does. Fires on: a candidate chosen for string similarity rather than meaning.

9. **Include the project's own accurate keywords.** Terms the project declares — `keywords` in
   `setup.cfg`/`pyproject.toml`/`CITATION.cff`, repository topics, subjects the project wrote on its
   Zenodo deposit — are included when rules 2–4 do not exclude them, even when one overlaps another field;
   rules 6–7 govern only terms the extractor proposes. Fires on: a project-declared term that survived
   rules 1–8.

10. **Add a domain term a searcher would type to find this software.** The quantity it computes (`hmF2`,
    `NmF2`, `emission measure`, `neutral winds`), its signature product or technique (`keogram`), the
    service it is the client for (`madrigal`), when the term is evidenced in the code or the project's
    documentation and would return this software to someone who needs it. Fires on: such a term that
    survived rules 1–8.

11. **Bind the existing row; never mint a variant.** Look the term up case-insensitively in the live list.
    A case variant binds the existing row — write the stored spelling. **Never mint a case, separator,
    plural or spelling variant of an existing row**: bind the existing row (`web service`, not the
    registry's `web_service`; a later refresh must not "correct" it). A row that is itself a misspelling is
    never the row to bind; rule 5 replaces it. Fires on: a live row that is the same term.

12. **Mint only a genuinely new domain term, lower-case.** A new row is minted only for a domain term
    absent from the vocabulary that a searcher would type to find this software (rule 10), written
    lower-case, one keyword per entry. Minting is normal for this open vocabulary and is not a reason to
    drop a qualifying term; report each mint in the diff. Fires on: a term included under rule 5, 9 or 10
    with no correctly spelled live row in any case, separator or plural variant.

13. **Incumbents.** Give every stored keyword its own verdict on a refresh: remove it only under rules 2–5
    (scope tag, failed domain test, unsupported, misspelled); keep every other stored keyword, including one
    that overlaps another field. Never remove or re-send a keyword to change only its case or separator.

14. **Empty is legitimate** when no project-declared term survives and no domain term qualifies. Record
    the sources checked.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

**Sources, in priority order:**
1. The project's declared keywords: `keywords` in `setup.cfg`, `pyproject.toml`, `CITATION.cff`,
   `package.json` or equivalent package metadata.
2. Repository topics (`curl -s https://api.github.com/repos/<owner>/<repo>/topics`), README badges.
3. The Zenodo / DataCite deposit's keywords and `subjects`.
4. The code and documentation, for domain terms the software computes or produces (rule 10).
5. The PyHC registry entry's `keywords` — read as registry taxonomy tags, tested under rules 2–3, never
   taken on the registry's authority. Pin the specific `_data/*.yml` file the entry lives in.

**Verification steps:**
- Fetch the full live list once and test every candidate against it case-insensitively and for
  separator/plural variants:
  `curl -s <target>/api/models/Keyword/rows/all/ | python3 -c 'import json,sys; [print(r["name"]) for r in json.load(sys.stdin)["data"]]' > keywords.txt`.
  Row counts differ by target; resolve against the target you will write to.
- For a removal under rule 4, run a word-anchored sweep of the pinned tree (`git grep -P -i '\bterm\b'
  <pin>`) and back the negative with a positive control.
- Search for unlisted keywords: check repo topics and package metadata, and compare against the PyHC
  keywords if applicable (then apply rules 2–3 to them).

**Traps:**
- **Compare stored names, not the title-cased rendering.** `/api/view/` shows `Goes`, `Lyra`,
  `Ionosphere_Thermosphere_Mesosphere`; the stored rows are `goes`, `lyra`,
  `ionosphere_thermosphere_mesosphere`. Copying a rendered form back as a "correction" is a defect. Read
  `.name` in the ORM, never `str()`.
- **Case-insensitive binding is not variant-insensitive.** `web_service` does not match `web service`;
  `atmospheric modelling` and `atmospheric-modelling` are two rows. Check separators and plurals by hand.
- **Some existing rows are capitalised** (`Keogram`, `All-sky imager`); a case variant binds them, and the
  stored capitalisation is what renders.
- **Registry tags travel.** The same `["ionosphere_thermosphere_mesosphere","specific"]` pair sits on
  unrelated entries (an ionogram inverter, a grid-square converter, a 3D coordinate library); judge each
  on the software, not the pair.
- **Registry underscore keys may already be stored with spaces** (`ionosphere thermosphere mesosphere`,
  `data retrieval`); that is a separate row from the underscored form.

## Payload and roundtrip notes

- **Key:** `keywords` — an array of strings.
- **Binding:** `_get_or_create_keyword` strips the value, looks up `name__iexact` and takes the first
  match; otherwise it creates a row with the value **exactly as sent** (case preserved). Sending
  `Neutral Winds` when no row exists mints a capitalised row, which is why a new term is sent lower-case.
- **A mint is a shared-row creation** that no later PATCH undoes: verify it by the new row's identity
  after the write, not by a table-count delta. A keyword name is capped at 128 characters.
- **Not order-sensitive.** `keywords` is a plain many-to-many field; order is not stored.
- **PATCH replaces the whole list.** Send every kept keyword plus the additions; `[]` or `null` clears
  the field; an omitted key is unchanged. Removing a keyword from a record leaves its row in the
  vocabulary.

## Worked examples

- **Zenodo REST client (PyZenodo).** Stored `ionosphere_thermosphere_mesosphere`, `magnetosphere`, `solar`
  came only from PyHC facet tags; the tree contains no heliophysics term. Rule 3 removes all three, decided
  together with the same tags in Field 5; the project-declared `json`, `open data`, `zenodo` stay (rule 9).
- **Ionogram inversion (POLAN).** `specific` is removed (rule 2); `ionosphere_thermosphere_mesosphere` is
  kept because the software works in the ionosphere (rule 3); `hmF2` and `NmF2`, its headline outputs,
  are added and bind existing rows (rules 10–11). The same pair of tags is removed from the World Magnetic
  Model wrapper (WMM2015), whose core-field model computes no ITM quantity.
- **Madrigal client (MadrigalWeb).** `general` is removed (rule 2); `madrigal` is added (rule 10); the
  registry's `web_service` is written as the existing `web service` row (rule 11).
- **Neutral wind model (HWM-93).** No stored keyword named the neutral wind, the quantity that
  distinguishes it from drift and convection models, and no row contained `neutral`. Rule 12 mints
  `neutral winds`; `upper atmosphere` and `middle atmosphere` bind existing rows.
- **Solar instrument toolkit (sunkit-instruments).** `emission measure`, the flagship routine's output, is
  added (rule 10); `differential emission measure` is rejected as a different quantity (rule 8); `proba2`
  is rejected because Fields 31/32 carry the missions (rule 6).

## Provenance

- Vocabulary block `vocab:Keyword` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 398-435 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
