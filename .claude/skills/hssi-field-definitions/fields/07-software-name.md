# Field 7 — Software Name

**Level:** MANDATORY · **API:** `softwareName` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T1 · **Field-search code:** `name`

## What it is

**Type:** Text

**What it is:** The name of the software.

**How to fill it:** The name of the software package as listed on the code repository.

## Why it exists

The name is the entry's headline and the first thing a searcher matches against. A user who already
knows the software looks for it by the name its project uses, and a user scanning results recognises it
by that name. A repository slug where the project writes something else, an `owner/repo` locator, or a
release title glued onto the name makes the entry look like a different or duplicate record. Needless
renames cost the user too: the detail page's address is derived from the name once and never follows a
rename, so a changed name and the page URL disagree permanently.

## How it appears on the site

- **Detail page:** the `<h1>` of the header, beside the latest version number and the logo; the browser
  page title is `<name> - HSSI`; the logo's alt text is `<name> logo`.
- **Detail-page address:** the slug is built from the name (lower-cased, `/` and `.` turned into `-`,
  slugified, 128 characters, `-2`, `-3` … appended until unique) when the entry is first published, and it
  is never updated by a later rename.
- **Filter:** none.
- **Free-text search:** tier T1 (`software_name`), the highest-ranked tier.
- **Field search:** `name:"…"` matches `software_name__icontains`.
- **JSON-LD:** `name`, and the value of the HSSI `PropertyValue` identifier.

## Rubric: include / exclude

Apply top to bottom; stop at the first rule that fires. Record the alternatives considered (every name
in circulation: repository, distribution, import, registry, DOI title) and why each lost, so a later
refresh does not churn the value.

1. **A generated locator or release title is not a name → replace it with the project's own name.**
   Zenodo's GitHub integration titles a deposit `<owner>/<repo>: <release name>`, and DOI autofill carries
   that string into HSSI. A stored value of the form `<owner>/<repo>`, `<owner>/<repo>: <release title>`,
   or `<name>: <release title>` is a mechanical artifact, not editorial intent, and a stray section
   heading or other non-name text is the same defect. Fires on: the stored value equals the Zenodo or
   DataCite title, the GitHub `full_name`, or the release name joined to the repository name.

2. **Never compose a name.** The value is a name some source actually uses. A constructed form ("X in
   Python", a name plus a description) is rejected even when it would disambiguate — disambiguation is
   the job of Fields 8 and 9. Fires on: a candidate that no project source, registry or DOI record uses.

3. **The stored name is a form the project uses for itself → keep it.** **Preserve editorial intent.** Do
   not replace a software name, description, concise description, or other subjective wording merely
   because you would phrase it differently. A stylistic alternative is not "fresh metadata." Keep the
   seeded value and note the alternative only if it reveals a material ambiguity. A different casing,
   a fuller title, or the distribution spelling is a stylistic alternative when the stored form is one
   the project itself writes as its name at the pinned revision (README or docs title, prose usage, the
   curated PyHC registry `name:`). **Preserve intentional representation.** A different name, description,
   concise description, or other subjective wording is not stale merely because the prepared file
   phrases it differently. Keep HSSI by default; classify the alternative as CONFLICT only when it is
   materially different and evidence gives the user a real choice. STALE requires objective evidence that
   HSSI is older, factually wrong, broken, or materially incomplete. Fires on: the stored value matches
   any such project-used form.

4. **The stored name is only a slug or distribution spelling the project never writes as its name →
   the project's own displayed name.** GitHub repository names and PyPI distributions are conventionally
   lower-case; the project's name is what its README, docs and prose write (`pydarn` → `pyDARN`,
   `rhybrid` → `RHybrid`). A README section-heading style (all-caps headings throughout) is typography, not
   the name. Fires on: the stored value matches the repository slug or distribution name, and the
   project's README, docs and prose consistently write a different form.

5. **The project renamed itself → the new name, unless a curated registry still lists the incumbent.**
   Adopt a new name when the project presents itself under it (README title, package and repository
   renamed) and no curated registry entry still uses the stored name. When the PyHC registry still lists
   the software under the stored name, keep it and record the new names as alternates: the catalogue and
   the curated registry agree, and the write-once page slug stays in step with the displayed name. Fires
   on: README/package rename evidence (a rename commit, a renamed repository, a renamed distribution).

6. **A version or edition suffix stays only when the project uses it as the name.** Model-generation
   names such as `IGRF-13`, `IGRF-14`, `WMM2015` and `HWM-93`, and a README title that carries its release
   (`TIEGCM v3.0`), are kept as written. Never append a version number to a name that does not carry one,
   and never strip a generation suffix that distinguishes the entry from its siblings. Fires on: a
   candidate that adds or removes a version or generation token.

7. **Never adopt a name that makes the entry indistinguishable from a different catalogue record.** When
   one project family has several implementations (a Python and a MATLAB edition, a wrapper and the model
   it wraps), use the name that identifies this implementation, not the family name. Fires on: a
   candidate name that is the name of a sibling or parent record.

8. **New value.** Take the name the project uses for itself: the README or docs title and how the prose
   writes it; where the project's sources disagree among themselves, the curated PyHC registry `name:`
   decides; failing that, the README's top-level heading. The distribution or import name is the fallback
   only when the project uses nothing else. Keep it within 128 characters. Never empty.

## Ask the user only when

- **A CONFLICT under rule 3:** the project itself uses two materially different names (not a casing or
  a fuller form of the same name), the stored one is one of them, and no later rule settles it. Present
  both with where each is used.

Every other case is decided by the rubric. Do not re-raise a name a prior dossier records as settled.

## Where to find it, and traps

**Sources, in priority order:**
1. The project's own presentation: README title (H1 or RST title block), docs title (`project =` in
   `docs/conf.py`, `site_name` in `mkdocs.yml`), and how the README and docs write the name in prose.
2. The curated PyHC registry `name:` — pin the specific `_data/*.yml` file the entry lives in.
3. Package metadata: `pyproject.toml` / `setup.cfg` / `setup.py` `name`, `CITATION.cff` `title` (when it is
   a name and not a paper title).
4. The repository name (GitHub API `name`), and the software name typically found in the repository
   name or README.
5. DOI records (Zenodo, DataCite) — for corroboration only; their titles carry the rule-1 artifact.

**Verification:** compare the value against the repository name, the README title and the package name
in config files, and note every inconsistency (a repository `pydarn` whose package is written `pyDARN`),
then resolve it under the rubric.

**Traps:**
- **A registry entry with a similar name may be a different package.** Match a registry entry by its
  `code:` URL, never by name alone; two wrappers of the same model can carry near-identical names.
- **PyPI's HTML project page answers 200 even for a nonexistent package**; only the JSON or Simple API
  proves whether a distribution exists, and a match proves this software only when its `project_urls` or
  `home_page` point at this repository. A same-named PyPI project can be unrelated.
- **The page slug does not follow a rename.** A stale slug on a renamed entry is expected, not drift.
- **Unicode matters.** Copy the project's spelling byte for byte (accented letters, internal capitals).

## Payload and roundtrip notes

- **Key:** `softwareName` — a string. Required on create.
- **Validation:** the serializer strips whitespace and rejects an empty value (`Value cannot be empty.`).
  The column is a 128-character `CharField`; keep the value within it.
- **PATCH** is a plain scalar replace; nothing is minted. The detail-page slug does not change.
- **Roundtrip:** `/api/view/` returns `softwareName` as stored; compare after trimming.
- **Lookup fallback:** when the repository-URL lookup finds nothing, `GET /api/search/?q=<name>&mode=id`
  searches by name.
- **Change class:** static — rarely changes; a full, file-driven refresh still compares it.

## Worked examples

- **A release title stored as the name (GeoDataPython).** The stored `jswoboda/GeoDataPython: ISR Sim
  Paper` is Zenodo's generated title — the repository plus the release name. Rule 1 fires. The README
  title block reads `GeoDataPython`; `setup.py`'s `GeoData` is rejected under rule 7 because it names the
  family that also has a MATLAB implementation with its own record.
- **Slug versus displayed name (pyDARN, RHybrid).** pyDARN's repository and distribution are `pydarn`, but
  the registry, README, docs and release titles write `pyDARN`, so rule 3 keeps the stored `pyDARN`. For
  RHybrid the stored value was the slug `rhybrid` while every prose use writes `RHybrid`; rule 4 fires, and
  the all-caps `RHYBRID` first line is rejected as heading style.
- **A generation suffix and a composed name rejected (IGRF-13).** The repository and distribution are
  `igrf`, the README title is "IGRF 13 in Python", and the registry `name:` is `IGRF-13`. Rule 3 keeps
  `IGRF-13`: the project's registry uses it and the generation number is what a user types. "IGRF-13 in
  Python" falls to rule 2.
- **A rename with the incumbent kept (MGSutils).** The repository became `mgs-radio` and the distribution
  `mgsradio`, but the PyHC registry still lists `MGSutils` and the page slug is `mgsutils`. Rule 5 keeps
  the incumbent and records the three other names as alternates.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 241-249 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
