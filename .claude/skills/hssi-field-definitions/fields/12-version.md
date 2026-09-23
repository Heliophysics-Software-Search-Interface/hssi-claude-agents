# Field 12 — Version

**Level:** RECOMMENDED · **API:** `version` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** not searched · **Field-search code:** `version` (number)

## What it is

**Type:** Nested group

**What it is:** Version of the software instance.

**How to fill it:** The version number is often an alphanumeric value, easily accessible on the code repository page (e.g., v1.0.0).

**Sub-fields:**
- **Version Number** (RECOMMENDED): The version identifier
- **Version Date** (RECOMMENDED): Date the specified version was released
- **Version Description** (RECOMMENDED): Brief summary of major changes in the new version (deprecated/new functionalities, features, resolved bugs, etc.)
- **Version PID** (RECOMMENDED): The globally unique persistent identifier for this specific version (e.g., the DOI for the version). Enter full DOI (e.g., https://doi.org/10.5281/zenodo.13287868)

The field describes **one** release: the newest version the project has actually released. HSSI stores
it as a separate version row attached to the entry.

## Why it exists

It tells a visitor what the current release is, when it came out, what changed in it, and how to cite
exactly that release. A stale version makes the whole record look unmaintained and undermines trust in
the other fields; an invented version (for unreleased code, or a PyPI-only build) sends people looking
for something that does not exist. Release notes the project did not write, or notes from a different
release, are read as the maintainers' own account and mislead. A version DOI attached to the wrong
number makes a reader download a different release than the one they think they are citing.

## How it appears on the site

- **Header:** the version number sits beside the software name.
- **Version Information section:** "Current Version" (number), "Release Date", "Version DOI" (a link
  to the Version PID) and "Release Notes" (the description, rendered as markdown). Empty sub-fields
  are omitted.
- **Which row shows:** when several version rows are attached, the page shows only one — the row with
  the latest release date (then the highest number).
- **JSON-LD:** `softwareVersion` and `version` carry the same latest number; when Field 2 is empty the
  entry's `@id` falls back to this Version PID.
- **Search:** not in the free-text tiers; `version:"…"` matches the number by substring.
- **View API rendering:** `/api/view/` shows versions as `<software name> - <number>`. That is a
  rendering; the stored number has no prefix.

## Rubric: include / exclude

The four sub-fields are decided in four groups. Within each group apply the rules top to bottom and
stop at the first that fires.

**Before any rule: establish the release history from the pinned revision.** List tags in creation
order, confirm each candidate is on the pin's own lineage (`git merge-base --is-ancestor <tag> <pin>`),
read every GitHub release's `name` and `body`, and read PyPI's release list from its JSON API. Then
identify which anomaly shape, if any, applies before deciding: an **orphan lineage** (a newer-looking
tag on a pre-rewrite lineage that shares no history with the pin — it is older, not newer), a version
**declared but never released** (in package metadata only: no tag, no release, no PyPI file), or a
release that **predates the headline feature** the entry describes (the code the description is about
is unreleased). "A tag is newer or older than the stored version" is where the question starts, not
the answer.

### Version Number

1. **More than one attached row → collapse to one.** Fires when the entry holds two or more version
   rows. Byte-identical duplicates collapse to one with no loss; distinct rows are replaced by the
   single row rules 3–6 select.
2. **Unreleased code never gets a version** (for a new value; a stored version that was declared but
   never released is handled by rule 4, not cleared here). Fires for: commits after the last release; a version
   declared only on an unmerged branch; a tag whose tagged code still declares the previous version
   and has no release; a PyPI file built from code not on the main line; release text drafted in a
   wiki or a release-candidate branch with no tag. Record nothing for them; note in the dossier what
   to check at the next refresh.
3. **A newer release than the stored one exists → replace the stored row.** "Newer" means a release
   later in the main line's release order: a tag on the pin's lineage with a GitHub release or a PyPI
   upload, or (for a project that does not tag) a PyPI upload of a version declared at a commit on the
   pin's lineage. Replacing the row orphans the old `SoftwareVersion` row; that is accepted HSSI
   behaviour and never a reason to keep a stale version. Write the new number in the same form the
   stored number used (with or without a `v`).
4. **Otherwise keep the stored number.** This covers every case with no newer release:
   - a cosmetic difference in how the same release is written (`v0.9.1` versus `0.9.1`) — **never
     replace for it**, in either direction;
   - a stored version that was declared but never released, when nothing newer has been released —
     keep it and record its status in the dossier;
   - a newest release that predates the headline feature — keep it and state in the dossier that the
     described code is post-release;
   - a newer-looking tag that turns out to be an orphan lineage.
5. **No stored row and a release exists → record the newest release,** with the number as the tag,
   release name or package metadata writes it. Either form is correct; record which was used so a
   later refresh does not "fix" it.
6. **No release of any kind → leave the field empty,** and record the declared version (if any) and
   what was searched.

**One entry, two packages.** When an entry covers two separately packaged components with
independent version histories, record the version of the package the entry's name and code
repository identify, and keep the other's history in the dossier only.

### Version Date

7. **The release event's UTC calendar day.** Use the GitHub release `published_at`; without a release
   object, the annotated tag's date or the tagged commit's date in UTC; for an untagged project, the
   PyPI upload of that version. Corroborate with the PyPI upload time and the Zenodo version deposit.
   When a PyPI timestamp crosses midnight UTC a few minutes after the release, the release day stands.
8. **These never override the release event when they disagree:** a tagged commit dated weeks before
   the release was published (it was drafted then), a local-time commit date that falls on another
   day than UTC, a CHANGELOG heading, `CITATION.cff` `date-released`, a wiki draft's date, and a
   Zenodo `Issued` or `updated` date. Record the disagreement so a later refresh does not "correct"
   the date back.
9. **Incumbent date on an unchanged release:** keep it when it matches rule 7; correct it when it
   came from a rule-8 source (see *Correcting the same release* below).

### Version Description

The description is **the release's own words, filtered for the site user.**

10. **Row being replaced for a newer release → derive the description afresh** for the new release
    under rules 13–16. Never carry the old release's description onto the new number.
11. **Incumbent description on an unchanged release → test it against its release range.** Compute
    the range previous tag → this tag (never tag → pin), after first checking
    `git merge-base --is-ancestor <previous> <this>`; if the two tags share no merge base, the range is
    undefined, so use the set of commits reachable from this tag and say so. Read the `name` and the
    `body` of this release and of its neighbours. Classify each clause as **attributable** (to this
    release's notes or range), **inherited** (from another release's notes) or **unattributable**.
    - Every clause attributable → keep it, even if it was lightly normalised (capitalisation, a
      corrected typo, joined sentences); record the difference so it is not "fixed" back.
    - Any clause inherited or unattributable → remove those clauses whole; if what remains fails
      rules 13–16, re-derive the description under them.
12. **Empty incumbent on an unchanged release → fill it** only when rules 13–16 yield text.
13. **Source order:** the release title (GitHub release `name`, when it is more than the tag), then
    the release body, then the CHANGELOG entry for that tag (a project's own version-history page
    counts as its changelog). A Zenodo integration deposit's title, `<owner>/<repo>: <release name>`,
    mirrors the release name and corroborates it.
14. **Keep verbatim only what a user cares about:** new or removed functionality; changed behaviour
    or API; changed inputs, outputs, supported platforms or Python versions; a fixed bug a user could
    hit. **Drop** build/CI/packaging chores, refactors, test and docs housekeeping, dependency pins and
    commit noise.
15. **Trim whole items only; never reword, merge or compose.** Bullets may stay bullets, since the page
    renders markdown under "Release Notes". A trailing contributor-and-pull-request credit on an item
    (`by @user in https://…/pull/N`) may be dropped; the item's own words may not be changed. A
    summary written from commit subjects, or any curator's account of the range, is never recorded,
    however well attributed.
16. **Leave empty** when nothing user-relevant survives, or when the survivor would confuse a reader
    without project context: a pointer ("Refer to RELEASE_NOTES"), boilerplate that repeats the
    package description, or an auto-generated pull-request list.

### Version PID

17. **The version DOI of exactly this release,** identified by the concept's `HasVersion` list and by
    the deposit's own `version`, title, or `IsSupplementTo …/tree/<tag>` link. Written as a full
    `https://doi.org/…` URL.
18. **Otherwise empty.** Never the concept DOI (that is Field 2 — the single exception is a legacy
    deposit with no concept DOI, Field 2 rule 4), never another version's DOI, never a poster's or
    paper's DOI. When the number is replaced and the new release has no deposit, the PID is cleared,
    even though the old row had one. A missing deposit for one release does not mean the release did
    not happen.

### Correcting the same release

The number changes only for a newer release; that rule governs the **number**. A wrong sub-value of the
**same** release — a date from a rule-8 source, a description that fails the description rules, another
version's PID — is corrected with the number unchanged; HSSI stores the correction as a new row and the
orphan is accepted. A difference that is only cosmetic is never corrected.

## Ask the user only when

Nothing — the rubric decides every known case. A case no rule covers is a rubric gap: ask, and report
it as one.

## Where to find it, and traps

**Sources, in priority order.** Version information may be in:
- Git tags
- Release notes
- Package version files
- CHANGELOG.md

DOIs (Persistent Identifier, Version PID, Reference Publication) may be in:
- CITATION.cff
- README badges
- Zenodo integration
- codemeta.json

**Verification.**
- Run `git tag --sort=-creatordate` and compare the latest tag. Use creation order, not a version-string
  sort: creator date follows the order releases were cut even when version strings sort oddly
  (`v0.10` before `v0.9` lexically, `.post` and release-candidate suffixes).
- Check pyproject.toml, setup.cfg, setup.py, package.json for version, **at the tag**
  (`git show <tag>:pyproject.toml`), not only at the pin. A dynamic version (setuptools-scm) has no
  static string to read.
- Verify version date against git tag date, then against the release and PyPI (rules 7–8).
- GitHub releases: `https://api.github.com/repos/<owner>/<repo>/releases` — read both `name` and
  `body`; projects differ in which one they write in, and a check that reads only `body` is blind on
  projects that summarise in the title.
- **PyPI JSON API is authoritative** for upload dates and the release list
  (`https://pypi.org/pypi/<name>/json`, `upload_time_iso_8601`). The HTML project page returns 200 even
  for packages that do not exist. A JSON 200 proves the name is taken, not that it is this software:
  match `info.project_urls`/`home_page` to the repository.
- For Version PID: verify the DOI resolves (`curl -s -o /dev/null -w "%{http_code}" https://doi.org/{DOI}`)
  and cross-check against CITATION.cff, README badges, codemeta.json; read DataCite's `version` for it.
- Dates must be YYYY-MM-DD (Fields 10, 12).

**Traps.**
- **Orphan lineages.** Walk history with `git rev-list <pin>`, never `git log --all`, which also shows
  tags on pre-rewrite lineages. A tag absent from the pin's history may still have been a real release
  of an earlier lineage; its absence from the walk proves nothing about whether it happened.
- **Backport tags.** A maintenance-branch release can be the newest by creation date while an earlier
  creation is the higher main-line version. The current version is the newest release on the main
  line; a backport tag is usually not an ancestor of the pin.
- **Changelog headings.** Prefixes vary within one file (`v2.4.0`, `2.3.0`); list headings with
  `^v?[0-9]+\.[0-9]+` or read them all. Changelog dates can disagree with tags and with each other.
- **Unreleased notes.** Towncrier fragments (`changelog/<n>.<type>.rst`) and a changelog's
  "Unreleased"/"Latest" section describe code not yet released; never use them for this field.
- **The wiki is a separate repository** (`<repo>.wiki.git`) and may hold release policy and drafted
  release text; drafted text is not evidence that a release exists — check for the tag first.
- **A same-date range** can look pre-tag: commits sharing the previous tag's date may still be inside
  the range. Trust the ancestry range, not the dates.
- **Autofill.** An entry autofilled from a Zenodo DOI can carry the deposit's issue or modification
  date as the release date, and a version PID of the deposited version; re-derive both.
- **Third-party deposits.** A deposit made from someone else's fork carries its own version label,
  which is not the project's release number.
- **Incomplete release lists.** PyPI and the tag list are each incomplete release histories (an
  untagged PyPI release, a tag never uploaded), and so is a Zenodo deposit list; none alone is the
  release list.

## Payload and roundtrip notes

**Version sub-keys are camelCase.** The version object uses `releaseDate` and `versionPid` (camelCase).
Snake_case (`release_date`, `version_pid`) also works due to auto-decamelization, but camelCase is the
documented convention to match the rest of the payload.

```json
"version": {
  "number": "2.4.1",
  "releaseDate": "2025-05-01",
  "description": "Adds GPU acceleration.",
  "versionPid": "https://doi.org/10.XXXX/example"
}
```

- **Shape.** `version` must be an object; `number` is required and must be a non-empty string (128
  characters max); `releaseDate` must parse as a date; `versionPid` must be a valid URL.
- **Replace, never edit.** Sending an object creates a new `SoftwareVersion` row and sets it as the
  entry's only version; the previous row is detached, not deleted. Orphaned version rows are accepted
  HSSI behaviour — this is the one shared row type where orphaning is tolerated.
- **Clear with `null`, never `[]`.** `Software.version` is a many-to-many but is not treated as a list
  field: `"version": []` fails the object check with a 400, and because the PATCH is atomic the whole
  update rolls back. `"version": null` clears the link and leaves the row intact.
- **Several attached rows.** Read all attached rows (`.all()`, never `.first()`) in any baseline or
  roundtrip, and report a count other than one.
- **Roundtrip representation.** Stored forms may flatten the sub-keys (`versionNumber`, `versionDate`,
  `versionDescription`) or use snake_case. `/api/data/` returns the row's UUID; `/api/view/` returns
  `<software name> - <number>` — never copy that string into a payload. A legacy row storing
  `version_pid = ""` is replaced by one storing `NULL`, which a naive diff flags although the values
  mean the same.

## Worked examples

- **Cosmetic prefix kept.** WMM2015 stores `1.1.1`; the git tag is `v1.1.1`, while `setup.cfg` and
  PyPI say `1.1.1`. No newer release exists, so rule 4 keeps the stored form; the opposite case (HWM93
  storing `v0.9.1` against PyPI's `0.9.1`) is kept the same way.
- **Stale version refreshed, PID cleared.** PyAuroraX stored 1.0.0 with a Zenodo version DOI while
  1.23.0 had been released. Rule 3 replaces the row; rule 18 clears the PID because no deposit exists
  after 1.0.0; the release body is only a pointer to the release notes, so rule 16 leaves the
  description empty.
- **Inherited clause removed.** ReesAurora's stored v1.0.5 description added a sentence paraphrasing
  the v1.0.4 release body. Rule 11 classifies it as inherited; what remains is the v1.0.5 release
  title, "Update selftest, cleanup prereqs.", which is kept.
- **Newer tag that is not a release.** SkyWinder has a reachable `v0.0.4` tag whose code still
  declares 0.0.3, with no release object, while PyPI's newest is 0.0.3. Rule 2 fires for `v0.0.4`;
  Field 12 records 0.0.3.
- **Orphan lineage.** MGSutils' `v1.0.0` and `v1.0.1` tags share no merge base with the current
  history, so the `v1.0.1..v1.1.0` range is undefined. The stored 1.1.0 description is tested against
  the commits reachable from `v1.1.0` and matches the GitHub release name `rename, refactor`; it is
  kept (rule 11).

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 290-304 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
