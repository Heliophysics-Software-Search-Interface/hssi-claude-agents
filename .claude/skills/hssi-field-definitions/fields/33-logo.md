# Field 33 — Logo

**Level:** OPTIONAL · **API:** `logo` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** not searched · **Field-search code:** none

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 755-776; other sections are authored in Phase 2. -->

## What it is

**Type:** URL

**What it is:** A link to the logo for the software.

**How to fill it:** The logo should be stored online in a permanent place and made publicly accessible.

**Agent guidance — pin the URL, then look at the image.** "A permanent place" is a requirement about the URL, not just the file. Apply in order:

1. **Git-hosted asset (GitHub/GitLab) — pin it to an exact commit.** Write `https://raw.githubusercontent.com/<owner>/<repo>/<40-char-sha>/<path>` (GitLab: `https://gitlab.com/<group>/<project>/-/raw/<sha>/<path>`). Never a branch name — `main`, `master`, or `refs/heads/<branch>` — and never a `blob/…` URL, which is GitHub's HTML *file-viewer page* and serves `text/html` rather than image bytes (the `?raw=true` variant only works by redirect). A branch reference silently breaks the logo whenever the file is renamed, moved, or deleted, and a branch can itself be renamed: several catalogue entries survived a `master`→`main` rename only through GitHub's compatibility redirect, which is not a guaranteed contract.
2. **The asset is Git-LFS-tracked** (`.gitattributes` has a `filter=lfs` rule for that path) — use `https://media.githubusercontent.com/media/<owner>/<repo>/<sha>/<path>`, which resolves the LFS object to real bytes. `raw.githubusercontent.com` returns the ~130-byte pointer *as `text/plain` with HTTP 200*, which renders as a broken image.
3. **Not hosted in a git repository at all** — a project or institutional site, a documentation build, a registry-hosted asset. This is a **perfectly good Field 33 value**; there is no commit to pin, so record it as-is and verify reachability. Do not discard such a logo, and do not treat "unpinnable" as a defect.
4. **No logo found** — a documented omission is a fine outcome. Never invent one.

**Verify before recording, in two ways.** First, fetch the URL: require an `image/*` content-type (`image/svg+xml` counts) and a plausible byte size. An HTTP 200 alone proves nothing — see the LFS case above, and the `blob/` page, which also answers 200. Second, **look at the image**. If it does not read as a logo for this software — a screenshot, an example plot, a data product, an unrelated mission patch, a sub-component's mark — **raise it with the user rather than rejecting it or swapping it yourself**, and bring the evidence: whether the project itself presents that image as its logo (README header, docs banner or `html_logo`, registry `logo:` field) is good reason to keep it, and that judgement is the user's to make. Record the outcome so a later refresh does not reopen a settled choice.

Keep the whole URL within 200 characters (the stored column's limit). A pinned URL is longer than a branch one; if a specific case would exceed 200, say so rather than falling back to a branch reference.

**Do not re-argue pinning on freshness grounds.** That a commit-pinned URL "freezes" the image to one revision is the intended behaviour, not a drawback: branch mutability *is* the fragility being removed. A logo redesign should reach the catalogue through a metadata refresh that re-derives and re-verifies the value, not silently through a moving reference.

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- moved from .claude/agents/hssi-metadata-extractor.md:277-288 -->
**Logo (Field 33) — pin the URL to a commit, then look at the image.** The form asks for a logo "stored online in a permanent place," which is a requirement about the **URL**, not just about the file. Never record a URL you have not fetched, and never record the string a source hands you (a repo's `conf.py`/`README`, the PyHC registry `logo:` field, a DataCite/Zenodo record) without re-deriving it.

1. **Git-hosted asset (GitHub/GitLab) — pin it to the exact commit.** Resolve the commit SHA the file is at and record `https://raw.githubusercontent.com/<owner>/<repo>/<40-hex-sha>/<path>` (GitLab: `<project>/-/raw/<sha>/<path>`). Never a branch name — `main`, `master`, `refs/heads/<branch>` — and never a `blob/…` page URL, with or without `?raw=true`: those serve HTML or depend on a redirect. A branch URL breaks silently the moment a maintainer renames, moves, or deletes the file, and HSSI has no way to detect it.
2. **The asset is Git-LFS-tracked** (check `.gitattributes`, or the fetch in the next paragraph returns ~130 bytes of `text/plain`) → use `https://media.githubusercontent.com/media/<owner>/<repo>/<sha>/<path>` instead.
3. **Not hosted in a git repository at all** — a project site, an institutional page, a ReadTheDocs-served static asset. This is a **perfectly good Field 33 value**; there is no commit to pin, so record it as-is and verify reachability. Do not discard such a logo, and do not treat "unpinnable" as a defect.
4. **No logo found** — a documented omission is a fine outcome. Never invent one.

**Verify before recording, in two ways.** First, **fetch the URL**: require an `image/*` content-type (`image/svg+xml` counts) and a plausible byte size. HTTP 200 alone proves nothing — a `raw.githubusercontent.com` URL for an LFS-tracked file returns 200 with a ~130-byte `text/plain` pointer that renders as a broken image, and a `blob/` URL returns `text/html`. Second, **look at the image.** You can see; use it. If it does not read as a logo for this software — it is an example plot, a data product, a screenshot, an unrelated graphic — **raise it with the user rather than rejecting it or swapping it yourself**, and present the evidence alongside the question. In particular, whether the project itself presents that image as its logo (README header, docs banner/`html_logo`, PyHC registry `logo:`) is good reason to keep it even when it is not a conventional wordmark; gather that evidence before asking. If a prior dossier records the value as already reviewed and approved, that settles it — don't re-raise it.

Keep the whole URL within 200 characters (`Software.logo` is a `URLField(max_length=200)`); a pinned raw URL is typically 90–145.

**Do not re-argue pinning on freshness grounds.** "A branch URL always serves the current logo, so pinning would freeze a stale image" is a rejected argument: that mutability *is* the fragility being fixed. A logo redesign is something a metadata refresh should notice and record deliberately, not something the catalogue inherits silently.

<!-- moved from .claude/agents/hssi-metadata-validator.md:148-152 -->
**Field 33 (Logo):**
- **Fetch it — a status code is not enough.** `curl -sIL {URL}` and read the content-type and length. A `content-type` that is not `image/*` (`image/svg+xml` counts) is an **ERROR**: `text/plain` at ~130 bytes is a Git-LFS pointer file (use `https://media.githubusercontent.com/media/<owner>/<repo>/<sha>/<path>` instead), and `text/html` is a repo page rather than the image. Both return HTTP 200 and both render as a broken logo.
- **A git-hosted URL must be pinned to a commit.** If the URL is on `github.com`/`raw.githubusercontent.com`/`gitlab.*` and contains a branch reference (`/main/`, `/master/`, `refs/heads/…`) or a `/blob/` segment — including `blob/…?raw=true`, which only works through a redirect — that is an **ERROR**, with `Suggested fix: repoint at https://raw.githubusercontent.com/<owner>/<repo>/<40-hex-sha>/<path>` for the commit the file is at. Do not accept the counter-argument that a branch URL "always serves the current logo": that mutability is the defect, and a redesign should be recorded deliberately at refresh time rather than inherited silently.
- **A logo on a non-git host is not a defect.** Project sites, institutional pages, and ReadTheDocs-served assets have no commit to pin. Verify reachability and content-type only, and never report "unpinned" against them.
- **Look at the image.** You can see it — fetch and view it. If it does not read as a logo for this software (an example plot, a data product, a screenshot, an unrelated graphic), this is **never an ERROR**: report it as a WARNING that asks the user to decide, and include the image and your evidence. It is satisfied outright if the dossier records that the project itself uses the image as its logo in practice (README header, docs banner, PyHC registry `logo:`), or that the value was already reviewed and approved — in that case do not raise it at all.

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- moved from .claude/agents/hssi-metadata-extractor.md:335-335 -->
- Any Logo (Field 33) URL was fetched and returned image bytes (`image/*`, plausible size), you have looked at the image, and — if it is git-hosted — it is pinned to a 40-hex commit SHA with no branch name and no `blob/` segment

<!-- moved from .claude/agents/hssi-metadata-validator.md:195-199 -->
5. **Check for a logo (Field 33) recorded as "Not found" when one exists upstream.** Nothing else in
   this document catches an under-included logo. Look for `docs/**/_static/*logo*`, `docs/conf.py`'s
   `html_logo`, a README header image, an `assets/`/`images/` logo file, and the PyHC registry `logo:`
   entry. If you find one, report it as a SUGGESTION with the commit-pinned raw URL (see Field 33 in
   Phase 3), fetched and viewed. A deliberate documented omission is fine — an unexamined blank is not.

## Payload and roundtrip notes

<!-- moved from .claude/skills/submission-payload/SKILL.md:237-237 -->
**Important — Logo (33):** `logo` is a `URLField(max_length=200)`, so keep the whole URL under 200 characters. A git-hosted logo must be pinned to an exact commit SHA (`https://raw.githubusercontent.com/<owner>/<repo>/<40-hex-sha>/<path>`, or `https://media.githubusercontent.com/media/…` when the path is Git-LFS-tracked) — never a branch (`/main/`, `/master/`, `refs/heads/…`) and never a `/blob/` page URL. Fetch it before putting it in the payload and require an `image/*` content-type: both an LFS pointer (`text/plain`, ~130 bytes) and a `blob/` page (`text/html`) answer HTTP 200 while serving no image. A logo on a non-git host has no commit to pin and is a valid value once reachability is confirmed.

<!-- moved from .claude/agents/hssi-metadata-updater.md:163-163 -->
**Logo (Field 33) — a refresh is exactly where a stored logo URL goes stale.** A HEAD returning 200 proves nothing: a `raw.githubusercontent.com` URL for a Git-LFS-tracked file answers 200 with a ~130-byte `text/plain` pointer, and a `blob/…` URL answers 200 with HTML — both render as a broken image. Require an `image/*` content-type (`image/svg+xml` counts) and a plausible size. If the stored URL is git-hosted and references a branch (`/main/`, `/master/`, `refs/heads/…`) or a `/blob/` segment, propose repointing it at `https://raw.githubusercontent.com/<owner>/<repo>/<40-hex-sha>/<path>` for the commit the file is at (`media.githubusercontent.com/media/…` when LFS-tracked) — a branch reference breaks silently on any upstream rename or move. A logo on a non-git host has no commit to pin and needs only the reachability check. Keep the URL ≤200 characters. Do not propose a *different image*: this is a change of URL form, and swapping the asset itself is a value decision for the user.

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 755-776 on 2026-09-22.
