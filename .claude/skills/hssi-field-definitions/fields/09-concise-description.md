# Field 9 — Concise Description

**Level:** OPTIONAL · **API:** `conciseDescription` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T1 · **Field-search code:** `description`

## What it is

**Type:** Text area (max 200 characters)

**What it is:** A description of the item limited to 150-200 characters. If the first 150-200 characters of the description do not provide the desired preview, you may enter an alternate text here.

**How to fill it:** The text should be short and provide a concise preview of the longer description.

## Why it exists

It is the one line a searcher reads while scanning results: the result card, the search-engine snippet
and the first JSON-LD description all use it when it is set. A good one tells the user in a sentence what
the software is and whether to click. A bad one — a truncated fragment, a stray autofill heading, a claim
the software does not honour — is the first thing every visitor sees, on every listing. When the
description already opens with a sentence that works as a preview, this field adds nothing.

## How it appears on the site

- **Result card:** the preview text, inserted as **plain text** (markdown is not rendered), with the logo
  prepended. When this field is empty the card shows the first 199 characters of Field 8 plus "…".
- **Detail page:** a "Concise Description" section rendered as markdown, shown only when the field is set.
- **`<meta name="description">`:** this field when set, otherwise Field 8; truncated to 30 words.
- **Filter:** none.
- **Free-text search:** tier T1 (`concise_description`).
- **Field search:** `description:"…"` matches this field and Field 8.
- **JSON-LD:** the first member of the `description` list when set.

## Rubric: include / exclude

Apply top to bottom; stop at the first rule that fires. Keep this field consistent with Field 8: a claim
removed from one is removed from the other. Record a superseded value and why, so it is not restored.

1. **Autofill artifacts are defects → remove them.** A trailing section heading ("Abstract"), a fragment
   of release notes, or other text captured from the DOI record is removed. When removing it leaves the
   author's sentence, keep that sentence exactly; when nothing descriptive remains, rebuild under rule 6.
   Fires on: text that matches the DOI record's non-descriptive content or a release body.

2. **A claim the pinned code does not support → drop that claim**, exactly as Field 8 rule 2, and keep
   the rest of the wording. Fires on: the same evidence as Field 8 rule 2.

3. **Over 200 characters → the value cannot be stored.** Do not truncate mid-sentence and do not
   compose a shorter paraphrase: take a shorter project-authored summary (rule 6 sources); if none exists,
   leave the field empty and let Field 8's opening serve as the preview. Fires on: a candidate longer than
   200 characters after trimming.

4. **A spelling, capitalization or grammar error → fix that error only.** Fires on: a misspelling or
   grammatical error with no plausible editorial reading.

5. **Otherwise keep the stored value.** **Preserve editorial intent.** Do not replace a software name,
   description, concise description, or other subjective wording merely because you would phrase it
   differently. A stylistic alternative is not "fresh metadata." Keep the seeded value and note the
   alternative only if it reveals a material ambiguity. **Preserve intentional representation.** A
   different name, description, concise description, or other subjective wording is not stale merely
   because the prepared file phrases it differently. Keep HSSI by default; classify the alternative as
   CONFLICT only when it is materially different and evidence gives the user a real choice. STALE requires
   objective evidence that HSSI is older, factually wrong, broken, or materially incomplete. A preview is
   legitimately lossy; that it omits something the description says is not a defect. A value shorter than
   150 characters is not a defect either. Fires on: a stored value that none of rules 1–4 touch.

6. **Empty field → fill only when Field 8's opening does not work as a preview.** If the description's
   first sentence stands alone and tells a scanning user what the software is, leave this field empty and
   record that the description's opening serves. Otherwise take the project's own one-line summary, in
   order: the curated PyHC registry `description:`; `pyproject.toml` / `setup.cfg` / `setup.py`
   `description`; the README tagline; `CITATION.cff` `abstract` when it is a single sentence. A repository
   tagline that embeds a DOI, badge text or a pipe-separated slogan is not a description. Prefer the
   candidate that names what distinguishes the software (its mechanism, its instrument, its data) over one
   that drops it. Fires on: every remaining case.

## Ask the user only when

- **A CONFLICT under rule 5:** the project's own sources give two materially different one-line
  summaries (different scope or capabilities, not different wording), the stored one is neither wrong
  nor materially incomplete, and rules 1–4 do not fire. Present both with their sources.

Every other case is decided by the rubric.

## Where to find it, and traps

**Sources, in priority order:**
1. The PyHC registry `description:` (community-curated, usually a one-line summary).
2. Package metadata: `pyproject.toml` / `setup.cfg` / `setup.py` `description`.
3. The README's one-line summary or tagline.
4. The GitHub repository `description` — only when it is a description rather than a slogan.
5. DOI records — for corroboration only.

The description and concise description are often in README.md or package metadata.

**Verification:** count characters after trimming (not bytes); read the value as a stand-alone card
preview; test every capability it names against the pinned code, as for Field 8.

**Traps:**
- **DOI autofill captures neighbouring text.** A deposit description that begins with a title line and
  an "Abstract" heading yields a concise description with the heading attached; an accidentally
  appended release body yields a fragment of release notes.
- **Plain-text rendering on the card.** Markdown syntax shows literally in the preview.
- **Two near-identical renderings of the author's sentence** (hyphenated or not, README versus
  registry) are equivalent; choosing between them is not a change worth making.

## Payload and roundtrip notes

- **Key:** `conciseDescription` — a string, ≤200 characters.
- **Format and types** — Required fields present and non-empty; objects/arrays match required shapes;
  dates are ISO `YYYY-MM-DD`; URLs are valid; `conciseDescription` is ≤200 characters.
- **Validation:** the serializer strips whitespace and rejects a value over 200 characters with
  `{"conciseDescription": "Must be 200 characters or fewer."}`, failing the whole request. The model's
  `max_length=200` on a `TextField` is not enforced by the database; the serializer check is the limit.
- **Clearing:** `null` or `""` clears the field.
- **PATCH** is a plain scalar replace; nothing is minted.
- **Roundtrip:** `/api/view/` returns the stored text; compare after trimming.
- **Change class:** static — derived from the description; a full, file-driven refresh still compares it.

## Worked examples

- **Kept consistent with Field 8 (GEOrinex).** When the unsupported RINEX 4 claim was dropped from the
  description, the concise description's `2/3/4` became `2/3` under rule 2, taking it from 157 to 155
  characters with no other change.
- **An autofill heading removed (FitsFlow).** The stored value was the author's summary sentence followed
  by a blank line and the bare word "Abstract", captured from the DOI record's section heading. Rule 1
  removes the heading and keeps the sentence exactly. The repository tagline "Browser-based FITS to ASDF
  pipeline | DOI: …" was rejected under rule 6: it embeds a DOI and drops what makes the tool distinctive.
- **Release notes replaced (aiapy).** The stored value was a truncated fragment of release notes
  accidentally appended during autofill. Rule 1 fires and nothing descriptive remains, so the value is
  rebuilt from the project's own documentation.
- **A reworded alternative declined (pysat).** A previously drafted rewording was accurate but only a
  stylistic variant of the stored maintainer-voiced text; rule 5 keeps the stored value.
- **Registry summary kept over the README's (hissw).** The stored value is the registry's `description:`,
  which names SSWIDL, Python and the Jinja templating; the README's near-identical one-liner omits the
  templating, the mechanism a prospective user most needs to know about. Rule 5 keeps the stored value.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 259-267 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
