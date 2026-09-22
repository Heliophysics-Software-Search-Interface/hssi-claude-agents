# Field 23 — Development Status

**Level:** RECOMMENDED · **API:** `developmentStatus` · **Change class:** dynamic
**Vocabulary:** `/api/models/RepoStatus/rows/all/`
**Filter tab:** none · **Free-text search tier:** T4.7 · **Field-search code:** `status`

## What it is

**Type:** Single-select dropdown

**What it is:** The development status of the software.

**How to fill it:** Select the development status of the code repository. See repostatus.org for term descriptions.

Submit the bare term only (`Active`, `WIP`, …); the descriptions below are the repostatus.org
definitions, not part of the value.

<!-- vocab:RepoStatus begin -->
**Possible Values** — *8 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/RepoStatus/rows/all/` is authoritative.*

- **Abandoned**: Initial development started but abandoned; no stable release
- **Active**: Reached stable, usable state and being actively developed
- **Concept**: Minimal/no implementation; limited example/demo/proof-of-concept only
- **Inactive**: Reached stable, usable state but no longer actively developed; support provided as time allows
- **Moved**: Project moved to new location; that version is authoritative
- **Suspended**: Initial development started but stopped temporarily; authors intend to resume
- **Unsupported**: Reached stable, usable state but authors ceased work; new maintainer desired
- **WIP**: Initial development in progress; no stable, usable public release yet
<!-- vocab:RepoStatus end -->

**Decide against the full definitions, not the one-line glosses above.** The glosses abbreviate, and
the abbreviation has changed a decision before ("new maintainer desired" is not what the row says).
The rows' `definition` column carries the repostatus.org wording verbatim:

- **Abandoned** — "Initial development has started, but there has not yet been a stable, usable release; the project has been abandoned and the author(s) do not intend on continuing development."
- **Active** — "The project has reached a stable, usable state and is being actively developed."
- **Concept** — "Minimal or no implementation has been done yet, or the repository is only intended to be a limited example, demo, or proof-of-concept."
- **Inactive** — "The project has reached a stable, usable state but is no longer being actively developed; support/maintenance will be provided as time allows."
- **Moved** — "The project has been moved to a new location, and the version at that location should be considered authoritative."
- **Suspended** — "Initial development has started, but there has not yet been a stable, usable release; work has been stopped for the time being but the author(s) intend on resuming work."
- **Unsupported** — "The project has reached a stable, usable state but the author(s) have ceased all work on it. A new maintainer may be desired."
- **WIP** — "Initial development is in progress, but there has not yet been a stable, usable release suitable for the public."

`Abandoned`, `Suspended` and `WIP` share the precondition that no stable, usable release exists;
`Active`, `Inactive` and `Unsupported` share the opposite one. `Inactive` and `Unsupported` are
contrary claims about support, not a weaker and a stronger version of one claim.

## Why it exists

A user deciding whether to build on a tool needs to know whether anyone is still developing it, whether
a bug report will be answered, and whether development has moved elsewhere. The value tells them at a
glance. `Active` on a dormant project invites reliance that will not be repaid; `Unsupported` on a
quiet but open project wrongly tells users their issues will go unread; a missing `Moved` leaves users
on a copy when the authoritative version lives somewhere else.

## How it appears on the site

- **Detail page:** "Technical Details" section, "Development Status" row; one status tag showing the
  term.
- **Filter tab:** none.
- **Free-text search:** tier T4.7 (`development_status` name).
- **Field search:** `status:"…"` matches `development_status__name__icontains`.
- **JSON-LD:** emitted twice — `codemeta:developmentStatus` (the term) and `creativeWorkStatus`, a
  `DefinedTerm` carrying the row's repostatus.org identifier, the term, its definition and
  `inDefinedTermSet` `https://www.repostatus.org`.

## Rubric: include / exclude

Apply top to bottom; stop at the first rule that fires.

1. **The project points to a new location** — a README, docs or archive notice saying development
   continues elsewhere or that a new version is developed at a named location → `Moved`. The pointer
   must come from the project; a fork or a similar project found by search is not a move. An
   organisation rename that redirects to the same repository is not a move.
2. **The repository is archived** (GitHub `archived: true`, or the equivalent read-only state on another
   host) → `Unsupported` if the software ever reached a stable, usable state, otherwise `Abandoned`.
   Archiving is the author's own act of closing the project; `Inactive` is excluded because support "as
   time allows" is impossible on a read-only repository. `Unsupported`'s second sentence, "A new
   maintainer may be desired.", is permissive: no evidence that a maintainer is wanted is needed.
3. **A repostatus.org status badge in the README** → that term, bare. It is the project's own
   declaration and wins over commit recency.
4. **An explicit status statement by the project** (README, docs, package description) → the term whose
   full definition the statement matches: "no longer maintained" / "deprecated" → `Unsupported`;
   "maintenance only" / "fixes as time allows" → `Inactive`; "work in progress" → `WIP` (even when a
   release exists); "on hold, will resume" with no stable release → `Suspended`; "demo" /
   "proof of concept" → `Concept`. The statement wins over commit recency.
5. **The software never reached a stable, usable state** — no tagged or registry release and no
   evidence it runs end to end or has been used — and rules 1–4 did not fire → `WIP` when it has
   commits in the last 24 months. With no commits for 24 months or more and no statement of intent,
   see *Ask the user only when*.
6. **Recency, for software that reached a stable, usable state**, measured by the **last commit date
   on the default branch** (not GitHub `updated_at`):
   - **under 6 months** → `Active`;
   - **6 to 24 months** → keep a stored `Active` or `Inactive`; with no stored value, `Active` — a quiet
     stretch under two years is not evidence that development has stopped;
   - **24 months or more** → `Inactive`. Open issues and unmerged pull requests left unanswered do
     **not** make it `Unsupported`: that row asserts the authors have ceased all work, which silence
     cannot show.
7. **Software without a repository** (a hosted model, a website): take the stable-state question from
   the publisher's own status (a catalogue status such as "Production", a published version) and the
   recency from the publisher's dated change log or version history; then apply rule 6.
8. **Incumbent values.** This field is dynamic: re-derive it on every refresh and replace the stored
   term when the rules give a different one. Record the dated anchors (last commit, last release) rather
   than an elapsed span, so a later refresh can re-apply rule 6 without trusting a stale number.
9. **Empty is legitimate** only when no status statement and no dated activity exist anywhere (no
   repository, no change log, no version history). Record what was searched.

## Ask the user only when

- **The software never reached a stable, usable state, the repository is not archived, it has had no
  commits for 24 months or more, and nothing states the authors' intent** — the choice among `WIP`,
  `Suspended` and `Abandoned` turns on an intent no source records.

Every other case is decided by the rubric.

## Where to find it, and traps

**Sources, in priority order:**
1. The README and docs: a successor pointer, a repostatus.org badge, a status statement.
2. Repository status indicators: GitHub `archived`, `disabled`; the equivalent on GitLab or Bitbucket.
3. Recent commit activity: the last commit on the default branch
   (`git log -1 --format='%H %cI' origin/<default>` after a fetch, or
   `GET /repos/<owner>/<repo>/commits?sha=<default>&per_page=1`).
4. Releases, tags and registry uploads, for the stable-state question.
5. For software without a repository: the publisher's catalogue record and change log.

**Validator checks:** **Development Status** must be one of: Abandoned, Active, Concept, Inactive,
Moved, Suspended, Unsupported, WIP (Field 23) — the bare term.

**Traps:**
- **GitHub `updated_at` is not commit activity.** It advances on metadata events such as starring;
  `pushed_at` counts pushes to any branch or tag. Only the default branch's last commit feeds rule 6.
- **Trove `Development Status ::` classifiers are not repostatus terms.** "4 - Beta" is a packaging
  maturity label frozen at a release; it can corroborate that a release exists, and nothing more. Do
  not map it onto a row.
- **Quote the definitions from the rows, never from memory or the glosses.** Reading "A new maintainer
  may be desired." as "a new maintainer is desired" turns a permissive clause into a requirement and
  wrongly rules out `Unsupported` for an archived project.
- **A publisher's "Last Updated" line can be a site build date.** CCMC's model pages show one date,
  identical across models and advancing daily; date CCMC software from its `/change-log/` instead.
- **A repository export or organisation rename is not a move.** The old URL redirecting to the current
  repository means nothing relocated.

## Payload and roundtrip notes

- **Key:** `developmentStatus` — a string, the bare term.
- **Binding:** the value is stripped and matched with `RepoStatus.objects.filter(name__iexact=…)
  .first()`; no match raises `{"RepoStatus": "Unknown value '<v>'."}` (400). Sending the term with its
  description fails.
- `"developmentStatus": null` or `""` clears the foreign key; an omitted key leaves it unchanged.
- **Readback:** `/api/view/` returns the term; `/api/data/` returns the row UUID — resolve it before
  treating the value as drifted.

## Worked examples

- **Archived after a release (HWM-93).** The repository is archived, the last release shipped on PyPI
  and was used in a published study. Rule 2 gives `Unsupported`: both clauses hold, and the maintainer
  sentence is permissive, so the absence of any maintainer solicitation counts for nothing against it.
  `Inactive` is excluded because an archived repository cannot receive the support it promises.
- **A successor pointer (TomograPy).** Code unchanged for over a decade, not archived; the latest
  commit adds a README banner saying a new version is being developed as `solartom`, placed by that
  project's developer. Rule 1 gives `Moved`, and the successor goes in Field 29.
- **Quiet but open (pyzenodo3).** Several stable releases, no commit for more than 24 months, not
  archived, open issues and community pull requests unanswered. Rule 6 gives `Inactive`; the unanswered
  issues do not show the author has ceased all work, so `Unsupported` is not selected.
- **A recent release burst (SAVIC).** Stable releases on PyPI, about ten months since the last commit,
  which closed a run of five releases in five weeks, and no stored value. Rule 6's middle band gives
  `Active`.
- **Archived before any release (solar-forcing).** Development started, the repository was archived,
  and no tag, release or registry upload was ever made. Rule 2's second branch gives `Abandoned`.

## Provenance

- Vocabulary block `vocab:RepoStatus` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 592-614 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
