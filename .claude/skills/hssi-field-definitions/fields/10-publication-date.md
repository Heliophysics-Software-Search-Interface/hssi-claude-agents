# Field 10 — Publication Date

**Level:** RECOMMENDED · **API:** `publicationDate` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** not searched · **Field-search code:** none

## What it is

**Type:** Date

**What it is:** Date of first broadcast/publication.

**How to fill it:** Used for the initial version of the software.

One calendar date, written `YYYY-MM-DD`: the day this software first became publicly available. It is
not the date of the latest release (Field 12), of a DOI, or of a paper about the software.

## Why it exists

It tells a visitor how long the software has existed in public, which helps them judge its maturity
and place it among older and newer tools. A date that jumps forward when a project first mints a DOI,
or that records a paper's date instead of the code's, makes established software look new and
misleads anyone comparing tools by age.

## How it appears on the site

- **Detail page:** a "Publication Date" item in the metadata block, formatted like `Jun 13, 2020`.
  Not shown when empty.
- **JSON-LD:** `datePublished`.
- **Search and filter:** not searched, no field-search code, no filter.

## Rubric: include / exclude

Apply to the incumbent HSSI value first, then to candidates for a new value; stop at the first rule
that fires.

1. **A date of a record, not of the software → never Field 10.** Fires for a DataCite `Issued` or
   Zenodo `publication_date` of a deposit made after the software was already public (it is the DOI
   mint date), a Zenodo `created`/`updated` timestamp, the date of a paper about the software (for
   example a JOSS article), or the date of any release after the first. An incumbent of this kind is
   replaced under rule 4.
2. **A date of a different project → never Field 10.** Fires for an artifact of a separate predecessor
   project, even if this code grew out of it (a fork, a port, a rewrite that started a new repository).
   Its date does not date this software. **A rename is not a different project:** when one continuous
   lineage — the same repository history — first published under an earlier package or distribution
   name, the earlier public date is this software's publication date and is kept.
3. **Incumbent that follows an accepted anchor → keep.** Before proposing any change, test whether
   the stored value already follows one of these:
   - **(a) first release:** the date of the earliest public release of this software — its first
     GitHub release `published_at` or tag, its first PyPI upload, its first Zenodo version deposit
     that archives the code, or its first archive download — whichever is earliest;
   - **(b) first public source:** the repository creation date, when a first commit on the pinned
     revision's continuous ancestry carries the same date (so the source was public from its first
     commit, not created empty and pushed later).
   If it follows either, keep it, and record the other anchor as a considered alternative. Two
   readings that are both correct are not a reason to change the value.
4. **New value → the first-release date; the repository creation date only when no release exists.**
   Use anchor (a). When the software has no release of any kind, use anchor (b). When the earliest
   distribution predates the repository (the project moved to GitHub after years of releases), use
   that distribution's date and never move it forward to the repository creation date.
5. **Nothing datable → empty,** with what was searched recorded. An empty value is legitimate only
   after tags, releases, PyPI, Zenodo and the repository history have all been checked.

Field 10 is static: a routine refresh does not re-derive it. A full refresh applies rules 1–3 to the
stored value.

## Ask the user only when

Nothing — the rubric decides every known case. A case no rule covers is a rubric gap: ask, and report
it as one.

## Where to find it, and traps

**Sources, in priority order.**

1. Git tags and GitHub releases: `git tag --sort=creatordate | head`, and
   `https://api.github.com/repos/<owner>/<repo>/releases` (read `published_at` of the oldest).
2. PyPI JSON API: `https://pypi.org/pypi/<name>/json`, the earliest `upload_time_iso_8601` across
   `releases`. The HTML project page returns 200 even for packages that do not exist; only the JSON or
   Simple API is evidence. Match `info.project_urls`/`home_page` to the repository before trusting it.
3. Zenodo/DataCite: the first version deposit in the concept's `HasVersion` list.
4. GitHub `created_at` (`https://api.github.com/repos/<owner>/<repo>`) together with the first commit
   on the pin's ancestry (`git rev-list --max-parents=0 <pin>` then `git show -s --format=%aI <sha>`).
5. Archive manifests for software distributed elsewhere first (for example a Google Code export's
   download list).

**Format.** Dates must be YYYY-MM-DD (Fields 10, 12).

**Traps.**
- **DOI autofill.** An entry autofilled from a Zenodo DOI receives the DOI's `Issued` date, which for a
  project that adopted Zenodo late is years after first publication. Re-derive from the repository.
- **Identical `Issued` dates across versions.** Several version deposits carrying the same `Issued`
  date means the date was applied to the deposits, not derived per version; use it as corroboration,
  not as separate release dates.
- **Repository created empty.** A `created_at` that disagrees with the first commit's date (either
  way) does not satisfy anchor (b).
- **Tags on orphan lineages.** Walk history from the pin (`git rev-list <pin>`), not `git log --all`,
  which also shows pre-rewrite lineages; confirm a tag with `git merge-base --is-ancestor <tag> <pin>`.
- **UTC.** Read timestamps in UTC; a local-time commit date can differ by a day from the release event.

## Payload and roundtrip notes

- Key `publicationDate`, a `YYYY-MM-DD` string; the serializer parses it as a date and rejects any
  other form (`Invalid date`). An empty string or `null` stores no date.
- Stored as a Django `DateField`; the value roundtrips unchanged.

## Worked examples

- **DOI mint date replaced.** PyAuroraX stored 2024-06-25, the `Issued` date of its 1.0.0 Zenodo
  deposit. Rule 1 fires; rule 4 gives 2020-06-13, the first PyPI upload (0.0.1), the same day the
  repository was created.
- **Repository date kept.** ReesAurora stores 2015-06-02, GitHub's `created_at` and the date of the
  first commit. Rule 3(b) fires; the first PyPI upload (2017-04-24) is recorded as the alternative.
- **Predecessor package.** python-magnetosphere's earliest download (2009-12-27) is a zip of `pygrf`,
  an earlier package under another name. Rule 2 fires for it; the stored 2009-12-29, the first commit
  of this project, stays.
- **Release history older than the repository.** madrigalWeb's first PyPI upload (2016-06-16)
  predates its GitHub repository (2024-09-19). Rule 3(a) keeps 2016-06-16; the repository date would
  be strictly less accurate.
- **Empty-repository date replaced.** HERMES Core stored its repository `created_at` (2022-03-17),
  which matches no commit; the changelog and GitHub release date v0.1.0 to 2022-10-05. Rule 3 does
  not fire, and rule 4 gives 2022-10-05.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 268-276 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
