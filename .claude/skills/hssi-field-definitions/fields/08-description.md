# Field 8 — Description

**Level:** MANDATORY · **API:** `description` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T1 · **Field-search code:** `description`

## What it is

**Type:** Text area

**What it is:** A description of the item. The first 150-200 characters will be used as the preview.

**How to fill it:** The description should be sufficiently detailed to provide the potential user with information to determine if the software is useful to their work. Include what the software does, why to use it, assumptions it makes, and similar information. Should be written with proper capitalization, grammar, and punctuation.

## Why it exists

A searcher decides from this text whether the software fits their work, and its words are matched in the
top search tier. What it claims is a promise: a user who finds the entry by a capability, installs the
package and discovers the capability is missing has been misled by the catalogue. A description that is
thin, truncated, or garbled by autofill hides what the software can do; its opening is, for most entries,
the only text a scanning user reads.

## How it appears on the site

- **Detail page:** the "Description" section, rendered as markdown ("No description available." when
  empty).
- **Result card:** when Field 9 is empty, the card preview is the first 199 characters of this text plus
  "…", inserted as **plain text** — markdown is not rendered there, so link syntax, headings and emphasis
  markers in the opening show literally. The expanded card shows the full text, also as plain text.
- **`<meta name="description">`:** Field 9 when set, otherwise this text, truncated to 30 words.
- **Filter:** none.
- **Free-text search:** tier T1 (`description`).
- **Field search:** `description:"…"` matches this field and Field 9 (`description__icontains`,
  `concise_description__icontains`).
- **JSON-LD:** `description` is a list of Field 9 (when set) followed by this text.

## Rubric: include / exclude

Apply top to bottom; stop at the first rule that fires. When the value changes, change only what the
rule names and keep every other word; record the superseded text and why, so a later refresh does not
restore it. Keep Fields 8 and 9 consistent: a claim removed from one is removed from the other.

1. **Autofill artifacts are defects, not editorial intent → remove them.** DOI autofill copies whatever
   the deposit holds: a section heading captured with the summary ("Abstract"), release notes appended
   to or replacing the description, Zenodo integration boilerplate, badge text. Remove the artifact; if
   nothing descriptive remains, rebuild from the project's own text (rule 6). Fires on: text that matches
   the DOI record's non-descriptive content or a release body rather than a description.

2. **A claim the pinned code does not support → drop that claim**, even when the project's own README
   makes it. The obligation runs to the site user: a searcher who selects the software for a capability
   it cannot deliver has been misled. Remove only the unsupported term or clause and keep the rest of the
   wording; record the evidence (the code path, the missing dispatch, the open feature request) and the
   **condition for restoring it** (the capability lands at a later pin). Fires on: a capability absent
   from the code at the pinned revision — the dispatch raises, the module does not exist, the only
   support is an unreferenced fixture.

3. **Materially incomplete or out of date against the project's own description → adopt the project's
   text.** When the stored text is a thin or older copy of a description the project itself maintains —
   most often the pinned `CITATION.cff` `abstract` — and it omits a headline capability, adopt that
   project text **verbatim**, including details you might otherwise modernise (an `http://` URL, the
   author's punctuation). Silently editing an author-supplied abstract is itself drift. Fires on: the
   project's own declared description names a capability the stored text omits, or the stored text is a
   truncated or earlier revision of it.

4. **A transcription loss from the project's own sentence → restore the lost words.** When the stored
   text quotes the author's summary except for a dropped word or phrase, restore it so the quotation is
   faithful, and leave the rest of the curator's wording alone. Fires on: the stored opening equals a
   project sentence (`setup.cfg`/`pyproject.toml` description, README tagline) minus words.

5. **A spelling, capitalization or grammar error → fix that error only.** The form asks for proper
   capitalization, grammar and punctuation. Correct the word; do not rewrite the sentence. Fires on: a
   misspelling or grammatical error with no plausible editorial reading.

6. **Otherwise keep the stored description.** **Preserve editorial intent.** Do not replace a software
   name, description, concise description, or other subjective wording merely because you would phrase it
   differently. A stylistic alternative is not "fresh metadata." Keep the seeded value and note the
   alternative only if it reveals a material ambiguity. **Preserve intentional representation.** A
   different name, description, concise description, or other subjective wording is not stale merely
   because the prepared file phrases it differently. Keep HSSI by default; classify the alternative as
   CONFLICT only when it is materially different and evidence gives the user a real choice. STALE requires
   objective evidence that HSSI is older, factually wrong, broken, or materially incomplete. A curator's
   light cleanup of the project's text (asides, links and badges removed) is editorial intent and stays.
   Fires on: a stored value that none of rules 1–5 touch.

7. **New value (empty field or new submission) → the project's own words.** In order: the pinned
   `CITATION.cff` `abstract`; the README's lead paragraph; the package summary (`pyproject.toml` /
   `setup.cfg` `description`); the docs index introduction. Light cleanup is allowed — remove badges,
   markdown links, parenthetical asides — but do not compose marketing prose or merge sources into new
   sentences. It must say what the software does and, where the project states them, why to use it and
   the assumptions it makes. When the lead paragraph is too thin for that, or a clause was dropped
   under rule 2, add further **whole sentences** from the project's own text (later README sections,
   the docs introduction), unaltered and in the project's order — extending the quotation is allowed,
   composing is not. A README written as a landing page (installation headings, badges, a
   navigation structure) is the wrong source even when it is the most current prose. Fires on: every
   remaining case.

8. **Standing constraints on any value.**
   - **The opening sentence must stand alone as a preview:** the first 150–200 characters are what the
     result card and the meta description show, as plain text.
   - **Describe this software, not its ecosystem.** Capabilities that live in plug-ins, sibling packages
     or the wrapped model are attributed to them ("plug-ins provide …"), so that Fields 17, 18 and 31/32
     are not implied. Vendored or test-only code is never credited with behaviour.
   - **Never empty.** The field is MANDATORY and the serializer rejects an empty value.

## Ask the user only when

- **A CONFLICT under rule 6:** the project's own sources give two materially different descriptions
  (different scope or capabilities, not different wording), the stored one is neither wrong nor
  materially incomplete, and rules 1–5 do not fire. Present both with their sources.

Every other case is decided by the rubric.

## Where to find it, and traps

**Sources, in priority order:**
1. `CITATION.cff` `abstract` at the pinned revision.
2. README.md lead paragraph; the docs index introduction (`docs/index.*`).
3. Package metadata: `pyproject.toml` / `setup.cfg` / `setup.py` `description` and `long_description`.
4. The PyHC registry `description:` (community-curated).
5. DOI records (Zenodo, DataCite) — a GitHub-integration deposit's description is the release body
   verbatim, not a software description.

The description and concise description are often in README.md or package metadata.

**Verification:** compare the value against the README and package metadata descriptions. Is it
accurate? Does it mischaracterize the software? Test every capability it names against the code at the
pinned revision, not against the README. Is the first 150–200 characters a reasonable preview?

**Traps:**
- **A README can claim more than the code does.** Read the dispatch or entry point before trusting a
  list of supported formats or versions; an unreferenced test fixture is not support.
- **YAML folding changes the text.** `abstract: >-` folds single line breaks into spaces and keeps blank
  lines as paragraph breaks — unfold before comparing with a stored value.
- **Quote matching must be whitespace-normalised.** A phrase that wraps across a line in the source
  fails a single-line grep; normalise whitespace before concluding a sentence is absent.
- **Markdown in the opening renders raw on the result card.** A description that begins with a link, a
  heading or a badge shows the syntax in every preview.
- **Do not normalise an author's URL or punctuation** when adopting the project's text verbatim; the
  point of rule 3 is fidelity.

## Payload and roundtrip notes

- **Key:** `description` — a string. Required on create.
- **Validation:** the serializer strips leading and trailing whitespace and rejects an empty value
  (`Value cannot be empty.`). The column is a `TextField` with no length cap.
- **Rendering:** markdown on the detail page; plain text on the result card.
- **PATCH** is a plain scalar replace; nothing is minted.
- **Roundtrip:** `/api/view/` returns the stored text; compare after trimming and with identical line
  breaks — paragraph breaks are part of the value.
- **Change class:** static — subjective and curator-curated; a refresh does not re-check it, but a full,
  file-driven refresh compares it and the rubric applies there.

## Worked examples

- **An unsupported claim dropped (GEOrinex).** The stored description and the README both say RINEX 4,
  but the pinned reader dispatches only versions 1–3 and raises on anything else; a RINEX 4 fixture sits
  unreferenced and the feature request is open. Rule 2 fires: "RINEX 4" is removed from Fields 8 and 9,
  every other word is kept, and the dossier records that the term returns when the dispatch supports it.
- **The CITATION abstract adopted verbatim (MadrigalWeb).** HSSI held the first three paragraphs of the
  project's `CITATION.cff` abstract from an older revision; the current abstract adds a fourth paragraph
  on the package's citation script, one of its three headline capabilities. Rule 3 fires and the pinned
  abstract is adopted verbatim, keeping its `http://` link. The rewritten README is rejected as a landing
  page.
- **A lost word restored (hissw).** The stored description opened with the author's own summary sentence
  except that "Seamlessly" was missing. Rule 4 restores the word; the curator's cleaned rendering of the
  docs introduction that follows is kept unchanged under rule 6.
- **Scope kept honest (pysat).** The description's last sentence says that archive and mission support
  lives in the ecosystem's plug-ins. That attribution is what keeps the record from claiming those data
  sources and instruments for the core package (rule 8).

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 250-258 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
