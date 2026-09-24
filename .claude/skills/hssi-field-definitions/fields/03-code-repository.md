# Field 3 — Code Repository

**Level:** MANDATORY · **API:** `codeRepositoryUrl` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.8 · **Field-search code:** `repo`

## What it is

**Type:** URL with repository autofill (SoMEF)

**What it is:** Link to the repository where the un-compiled, human readable code and related code is located (SVN, GitHub, CodePlex, institutional GitLab instance, etc.). If the software is restricted, put a link to where a potential user could request access.

**How to fill it:** Navigate to the root page of your repository, copy the entire link, and paste it into this field.

## Why it exists

This is how a visitor gets from the catalogue entry to the software itself: the "Code" button. A wrong
value sends them to a dead page, an old fork, or a different project; a page URL for one branch or file
shows them a stale slice of the code instead of the project. The value is also the entry's identity key
inside the catalogue: the repository-URL lookup resolves it to the entry, and other entries' Related and
Interoperable Software (Fields 29/30) point at this exact string. Changing it carelessly breaks those
links for users of other entries, so it changes only when the software itself has moved.

## How it appears on the site

- **Detail page:** a "Code" action button linking to the stored URL, shown only when the field is set.
  The homepage result card carries the same "Code" button.
- **Filter:** none.
- **Free-text search:** tier T4.8 (`code_repository_url`).
- **Field search:** `repo:"…"` matches `code_repository_url__icontains`.
- **JSON-LD:** emitted as `codeRepository`. It is also the record's `@id` when the entry has no
  persistent identifier and its latest version has no version PID.
- **Other entries:** an in-catalogue relation in another entry's Field 29 or 30 is stored as this URL and
  rendered with the raw URL as its link text, so a reader sees this exact string there.
- **API lookup:** `GET /api/list/software/?repo_url=<url>` finds the entry by this value (case-insensitive
  exact match after trimming whitespace; no other normalization).

## Rubric: include / exclude

Apply top to bottom; stop at the first rule that fires. For a **stored** value, test the incumbent rules
3–6 first — a rename or move (rule 3, with its inbound sweep), a stale ref (rule 4), an author-designated
pinned form (rule 5), a cosmetic variant (rule 6) — and use rule 2 only when none of them governs; rule 2
is for a value that points at something other than the repository, not for a repository URL in another
form. Record the evidence for the rule that fired, and
record every URL considered and not used with the reason, so a later refresh does not re-propose it.

1. **No public source repository → the page where a user obtains the software or requests access.**
   Some HSSI software has no Git repository at all: a model run as a service, a coefficient release, an
   agency product. A **model or product page** (a CCMC model page, an agency product page, the project's
   official download listing) **is a valid Field 3 value** — the form's own instruction for restricted
   software is "a link to where a potential user could request access." **Never invent, construct or
   substitute a repository.** A nearby repository in the same organization is not the source unless it
   is the release: evaluation tooling, a bleeding-edge snapshot whose README points elsewhere for
   releases, a mirror, or a companion package is rejected and recorded (a companion usually belongs in
   Field 29). Fires on: the project's own statements, the product page and the DOI record name no public
   source repository for this software.

2. **A public source repository exists but the value points elsewhere → the repository.** A homepage, a
   release-download page, a documentation site, a DOI landing page, or an unofficial fork is not the
   code repository when the project publishes its source. Fires on: a repository the project itself
   names as its source (git remote of the authoritative clone, `[project.urls]` Repository/Source,
   `CITATION.cff` `repository-code`, README clone instructions) that differs from the value.

3. **The repository moved or was renamed → the current canonical URL.** GitHub redirects prove a move:
   the old URL answers `301` to a new owner or name, and the GitHub API's `full_name` differs from the
   stored path. Record `https://github.com/<full_name>` and record the old URL as a **previous value
   with the redirect evidence**. Do not keep the old URL because it still redirects: a rename redirect
   lapses as soon as anyone re-creates the old path. Before replacing, run the inbound sweep — every other
   entry whose Field 29 or 30 stores the old string — and report those entries so their relations are
   repointed too. Fires on: a redirect to a different owner/name, or an API `full_name` that differs
   from the value beyond letter case.

4. **A stored `/tree/<ref>` or `/blob/<ref>` URL whose ref no longer exists → the base repository URL.**
   Replace it with `https://github.com/<owner>/<repo>` through the normal field-by-field diff; never treat
   a stale page URL as current. Fires on: `git ls-remote` shows no branch or tag named `<ref>`, or the URL
   no longer resolves while the base repository does.

5. **A stored `/tree/<ref>` URL whose ref still exists and that the project's own metadata records →
   keep it.** When the author's published software metadata (Zenodo `code:codeRepository`,
   `IsSupplementTo`, `CITATION.cff` `repository-code`) uses the tag-pinned tree — typically a
   publication-code archive naming the exact code state behind a paper — the stored value is the
   author's choice, not drift. Record the repository root as the considered alternative. Fires on: the
   ref resolves (`git ls-remote`) and the project's own metadata carries the same URL.

6. **The incumbent differs from the canonical form only cosmetically → keep it.** A trailing slash, or
   letter case in the owner or repository name when both forms reach the same repository, is not a
   reason to change the stored value: nothing changes for a visitor, while other entries' relations and
   the lookup key bind to the stored string. Record the canonical form as considered and not adopted, so
   the difference is read as settled rather than as drift. Fires on: both forms resolve to the same
   repository (same GitHub repository id, no redirect to a different owner or name).

7. **Otherwise, record the canonical base URL.** For a new value, or an incumbent that already matches:
   `https://github.com/<owner>/<repo>` (GitLab: `https://gitlab.com/<group>/<project>`), spelled as the
   GitHub API's `full_name` / `html_url` gives it — complete with protocol, **no `.git` suffix, no
   trailing slash, never a `/tree/<ref>` or `/blob/<ref>` page, no `#readme` anchor**. A new value is never
   a tag- or branch-pinned page URL. Where the project names a mirror, record the primary host the
   project designates; a dead mirror is recorded as history only. Fires on: every remaining case.

8. **Never empty.** The field is MANDATORY and the serializer requires it on a create. An empty string
   sent on a PATCH stores null — never send one.

## Ask the user only when

- **No page exists anywhere from which a user can obtain the software or request access** — no public
  repository, no product or model page, no download listing, no contact route. The field cannot be
  filled and the entry cannot be submitted as it stands.

Every other case is decided by the rubric.

## Where to find it, and traps

**Sources, in priority order:**
1. The repository itself: run `git remote -v` in the clone and compare; the Code Repository URL can
   usually be read directly from the repository's own URL.
2. The GitHub API (`https://api.github.com/repos/<owner>/<repo>`): `full_name`, `html_url`, `archived`,
   `fork`. Follow redirects: `curl -sIL https://github.com/<owner>/<repo>` shows a rename as a `301`.
3. The project's own metadata at the pinned revision: `pyproject.toml` `[project.urls]`, `setup.cfg` /
   `setup.py` `url`, `CITATION.cff` `repository-code`, `mkdocs.yml` `repo_url`, README badges and clone
   instructions.
4. Curated registries: the PyHC registry `code:` field.
5. The DOI record: Zenodo `metadata.custom["code:codeRepository"]` and `IsSupplementTo` related
   identifiers; DataCite related identifiers.
6. For software with no repository: the agency product page, the CCMC model page, the project's download
   listing, the reference publication.

**Verification:** the URL must be complete with protocol; resolve it and confirm it lands on this
software's source (or, under rule 1, on the page that offers it), not on a redirect to something else.

**Traps:**
- **DOI metadata and registries lag moves.** A Zenodo deposit keeps the owner and name the repository
  had when it was minted, and GitHub-integration deposits record `/tree/<tag>` URLs; the PyHC registry's
  `code:` can predate a move. None of these overrides rule 3.
- **Never build a repository URL from a distribution or package name** and treat its 404 as evidence
  about the repository. A distribution name is not a repository path.
- **GitHub serves both letter cases without a redirect**, so a case difference is invisible to a
  visitor; the catalogue's relations, however, bind to the exact stored string (rule 6).
- **GitHub `updated_at` is not commit activity**, and an archived repository is still the right value:
  archival is a Field 23 fact, not a Field 3 change.
- **A repository inside the official organization is not automatically the release.** Read its README:
  a repository that sends release seekers elsewhere, or describes itself as evaluation or development
  tooling, is rejected under rule 1.
- **A repository's wiki (`<repo>.wiki.git`) is a separate git repository**, never the Field 3 value.

## Payload and roundtrip notes

- **Key:** `codeRepositoryUrl` (lowercase `Url`) — a URL string. Some response representations, including
  `/api/view/`, render it as `codeRepositoryURL`; treat that key rename as equivalent on roundtrip.
- **Validation:** the serializer strips whitespace and applies Django's `URLValidator`; a non-URL fails
  the whole request with `Invalid URL`. An empty string is stored as null. The column is a `URLField`, so
  keep the value within 200 characters.
- **Required on create** (with `submitter`, `softwareName`, `authors`, `description`); a PATCH may omit it.
- **PATCH** is a plain scalar replace; nothing is minted. It changes the entry's lookup key: after a
  change, `?repo_url=` finds the entry only under the new URL.
- **Lookup:** `GET /api/list/software/?repo_url=<url>` is exact (case-insensitive) after trimming, with no
  URL normalization on the server, so try variants in order — with and without a trailing `/`, with and
  without `.git`, and for GitHub `tree`/`blob` URLs the bare `https://github.com/<owner>/<repo>` form —
  and use the first that returns a non-empty `data` array.
- **Change class:** static — a refresh does not re-check it, but a full, file-driven refresh compares it
  like every other field, and rules 3–4 apply there.

## Worked examples

- **An organization move (cdflib).** The stored `https://github.com/MAVENSDC/cdflib` permanently
  redirects to `https://github.com/lasp/cdflib`, the API's `full_name` is `lasp/cdflib`, and the
  project's own metadata and badges name the new location. Rule 3 fires: the current URL is recorded and
  the old one kept as the previous value with the redirect evidence.
- **No repository, and a tempting one rejected (IGRF-14).** The release is published through an agency
  product page and a DOI. A repository in the model's organization exists, but it is evaluation software
  whose README sends release seekers elsewhere. Rule 1 fires: the product page is the value and the
  repository is recorded as a rejected alternative.
- **A download page where source exists (Autoplot).** The stored value was a release-download page. The
  project's source lives in a public GitHub repository migrated from its former SVN trunk, which the
  current README documents. Rule 2 fires and the repository replaces the download page.
- **A case difference left alone (WMM2020).** GitHub reports the lowercase `space-physics/wmm2020`, while
  the entry stores the capitalized form that the registry also uses, and the sibling WMM2015 entry's
  related-software link binds to that exact string. Both spellings reach the same repository with no
  redirect, so rule 6 fires and the stored value is kept with the lowercase form recorded.
- **A rename chain recorded as history (MGSutils).** Two historic paths answer `301` to
  `space-physics/mgs-radio`. Rule 3 records the current canonical URL and lists the old paths as history,
  since a redirect is a courtesy that lapses if the old path is re-created.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 70-78 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
