# Field 33 — Logo

**Level:** OPTIONAL · **API:** `logo` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** not searched · **Field-search code:** none

## What it is

**Type:** URL

**What it is:** A link to the logo for the software.

**How to fill it:** The logo should be stored online in a permanent place and made publicly accessible.

"A permanent place" is a requirement about the **URL**, not just the file: the rubric below turns it into
URL rules (commit-pinned for git-hosted assets) as well as rules about which image qualifies.

## Why it exists

The logo is the software's visual identity on the site: it heads the detail page and sits beside the
preview text on every result card, so a scanning user recognises the software by it. A wrong image
misidentifies the software — another project's mark, an institution's mark, or a plot reads to a visitor
as "this is what this software is". A broken URL shows a broken image on every listing. An empty logo
costs the user nothing, so an honest blank beats a borrowed or accidental image.

## How it appears on the site

- **Detail page:** in the header beside the name and latest version number, as
  `<img class="software-logo" alt="<name> logo">`, shown only when the field is set.
- **Result card:** the image is prepended to the preview text and to the expanded description.
- **Filter:** none. **Search:** not searched; no field-search code.
- **JSON-LD:** emitted as `image`.

## Rubric: include / exclude

Rules 1–6 choose **the image**. Rule 1 governs whenever HSSI already stores a logo. Otherwise assess
**every** candidate image under rules 2, 4 and 5; when more than one survives, rule 3 selects; rule 6
applies only when none survives. Rules 7–9
choose **the URL form** for that image: test rule 8 (Git LFS) before rule 7, and rule 9 for an asset
with no git host. Rule 10 applies to every value before it is
recorded, and rules 11–12 govern a stored URL on refresh. Never record a URL you have not fetched, and
never record the string a source hands you (a repo's `conf.py`/`README`, the PyHC registry `logo:` field,
a DataCite/Zenodo record) without re-deriving it. Record the outcome — including every candidate image rejected, with its
URL — so a later refresh does not reopen a settled choice.

1. **A stored logo → keep the image.** A refresh never silently removes a logo HSSI already holds,
   whatever the image depicts: the earlier curation is the settled value, and the one exception — a
   dead, unrecoverable URL — is only ever *proposed* for clearing, below. What a refresh may do is change the URL
   form (rules 7–9, 11), recover the same image when the stored URL no longer serves it (rules 7–10), and —
   only when the project has since adopted a designed mark of its own — propose the swap in the diff as a
   separate, named change for the user to accept or decline at the payload gate. When the stored URL is
   dead and nothing recovers the same image, **propose clearing the value** in the diff the same way, as a
   named change with the dead URL and every recovery attempt recorded; the stored value is never cleared
   or swapped silently, and rule 6 never applies to a stored logo. Fires on: HSSI stores a logo for the
   entry.

2. **The project presents an image as its logo → include it, whatever it depicts.** Presentation
   evidence is the docs `html_logo` (or the docs theme's logo option), the PyHC registry `logo:` entry, a
   README header image used as branding, or a dedicated logo file the project references (`logo.png`,
   `docs/logo/…`, `docs/**/_static/*logo*`). The project's choice governs: a wordmark or emblem qualifies,
   and so does a plot, photograph, or an institution's or mission's banner **when the project itself
   presents it as its logo**. Record what the image depicts in the dossier so the choice is visible.
   Fires on: presentation evidence for the image.

3. **Several images are presented → the one the project ranks first.** The docs `html_logo` outranks a
   README header, which outranks a registry `logo:` entry maintained by a third party; a dedicated logo
   file the docs use outranks a gallery figure. Record the others as alternatives. Fires on: more than
   one image with presentation evidence.

4. **An image the project does not present as its logo → exclude it.** Never a plot, screenshot,
   diagram or data product — an example output, a test fixture, a demonstration animation, or a
   photograph illustrating the docs — that the project does not present as its logo (rule 2). A figure
   in a README's hero position with nothing else presenting it as branding is a figure, not a logo. Record each
   candidate with its URL as a rejected alternative. Fires on: an image with no presentation evidence.

5. **Another organization's mark → exclude it.** Never an institution's mark for software that has none
   of its own: the developing institution's logo on a product page, the parent project's icon supplied by
   a shared docs theme, a parent-project mark copied into the repository but never used by it. Recording
   it would present that organization's identity as this software's. Record the URL as a rejected
   alternative so a curator can adopt it deliberately if they choose. Fires on: the mark belongs to an
   organization or parent project, and the project does not present it as this software's logo (if it
   does, rule 2 fires first).

6. **No logo found → a documented omission.** A documented omission is a fine outcome; never invent one.
   Record where you looked (every source in *Where to find it*) so the blank is evidenced rather than
   unexamined. Fires on: HSSI stores no logo and no candidate survives rules 2–5.

7. **Git-hosted asset (GitHub/GitLab) → pin it to the exact commit.** Resolve the commit SHA the file is
   at and record `https://raw.githubusercontent.com/<owner>/<repo>/<40-hex-sha>/<path>` (GitLab:
   `https://gitlab.com/<group>/<project>/-/raw/<sha>/<path>`). Never a branch name — `main`, `master`, or
   `refs/heads/<branch>` — and never a `blob/…` URL, with or without `?raw=true`: `blob/` is GitHub's HTML
   *file-viewer page* and serves `text/html` rather than image bytes, and the `?raw=true` variant only works
   by redirect. A branch URL breaks silently the moment a maintainer renames, moves, or deletes the file,
   and HSSI has no way to detect it; a branch can itself be renamed, and a `master`→`main` rename survives
   only through GitHub's compatibility redirect, which is not a guaranteed contract. Fires on: the chosen
   image lives in a git repository.

8. **The asset is Git-LFS-tracked → `media.githubusercontent.com`.** When `.gitattributes` has a
   `filter=lfs` rule for that path, or the fetch returns ~130 bytes of `text/plain`, use
   `https://media.githubusercontent.com/media/<owner>/<repo>/<sha>/<path>`, which resolves the LFS object
   to real bytes. `raw.githubusercontent.com` returns the ~130-byte pointer *as `text/plain` with HTTP
   200*, which renders as a broken image. Fires on: LFS tracking for the path.

9. **Not hosted in a git repository at all → record it as-is.** A project or institutional site, a
   documentation build (a Read the Docs–served static asset), a registry-hosted asset: this is a
   **perfectly good Field 33 value**. There is no commit to pin, so record it and verify reachability. Do
   not discard such a logo, and do not treat "unpinnable" as a defect. When the source's URL redirects to
   a byte-identical image, store the redirect target, which does not depend on the redirect surviving.
   Fires on: a chosen image with no git host.

10. **Verify before recording, in two ways, and keep within 200 characters.** First, **fetch the URL**:
    require an `image/*` content-type (`image/svg+xml` counts) and a plausible byte size. HTTP 200 alone
    proves nothing — the LFS pointer and the `blob/` page both answer 200. Second, **look at the image**.
    Keep the whole URL within 200 characters (the stored column's limit); a pinned raw URL is typically
    90–145. A pinned URL is longer than a branch one; if a specific case would exceed 200, say so rather
    than falling back to a branch reference. A source URL that does not return an image (404, HTML) is
    never recorded as a new or changed value; look for the same image elsewhere, and otherwise apply
    rule 6 (no stored logo) or rule 1's proposed clearing (stored logo) with the dead URL recorded. Fires
    on: every new or changed value before it is recorded.

11. **An incumbent on a branch or `/blob/` URL → repoint it at the commit-pinned URL for the same file.**
    A refresh is exactly where a stored logo URL goes stale. Propose
    `https://raw.githubusercontent.com/<owner>/<repo>/<40-hex-sha>/<path>` for the commit the file is at
    (`media.githubusercontent.com/media/…` when LFS-tracked); this is a durability change of URL form, made
    even when the old URL still serves the image. Do not propose a *different image*. Fires on: a stored
    git-hosted URL with a branch reference or a `/blob/` segment.

12. **Do not re-argue pinning on freshness grounds.** "A branch URL always serves the current logo, so
    pinning would freeze a stale image" is a rejected argument: that mutability *is* the fragility being
    fixed. A logo redesign should reach the catalogue through a metadata refresh that re-derives and
    re-verifies the value, not silently through a moving reference.

## Ask the user only when

No listed shapes: every case is decided by the rubric. A stored logo is kept (rule 1), and a swap to a
newly adopted mark or the clearing of a dead, unrecoverable URL is proposed in the diff, not asked
separately; a project-presented image is included whatever it depicts (rule 2).

## Where to find it, and traps

**Where to look (all of them, before recording "Not found"):**
1. `docs/conf.py` `html_logo` (and the theme's logo option); `mkdocs.yml` theme logo.
2. `docs/**/_static/*logo*`, `docs/logo/`, `docs/images/`, `logo/`, `assets/`, `images/` — any file named
   for a logo.
3. The README header image (the first image, above or beside the title).
4. The PyHC registry `logo:` entry — pin the specific `_data/*.yml` file the entry lives in.
5. The project's own website or documentation build header.
Nothing else in the validation catches an under-included logo: an unexamined blank where one of these
exists upstream is a SUGGESTION, reported with the commit-pinned raw URL, fetched and viewed.

**Verification commands:**

```
curl -sIL {URL}                                   # content-type and content-length of the final hop
curl -sL -o logo.bin {URL} && file logo.bin && shasum -a 256 logo.bin
git show <sha>:<path> | shasum -a 256             # byte-identical to the tracked blob?
```

Before recording, confirm: the URL was fetched and returned image bytes (`image/*`, plausible size), you
have looked at the image, and — if it is git-hosted — it is pinned to a 40-hex commit SHA with no branch
name and no `blob/` segment.

**Traps:**
- **`text/plain` at ~130 bytes is a Git-LFS pointer file**, and **`text/html` is a repo page** rather than
  the image. Both return HTTP 200 and both render as a broken logo.
- **A docs site's displayed logo may belong to the theme.** A shared theme (for example the SunPy theme)
  supplies its project's icon to every affiliated package's documentation; that icon is not this
  package's logo (rule 5).
- **A registry `logo:` string can be dead or on a branch.** Re-derive it: fetch it, and pin a git-hosted
  one; a dead one is not recorded.
- **A registry logo can belong to a similarly named different package.** Match the registry entry by its
  `code:` URL before using its `logo:`.
- **A Read the Docs `_static` copy is recompressed**, so its hash differs from the repository blob; it is a
  valid non-git value, but hash-based drift checks against it false-alarm.
- **LFS can start mid-history.** A path may hold a real blob at an older commit and a pointer later;
  test the fetch at the pinned commit rather than inferring from `.gitattributes`.

## Payload and roundtrip notes

- **Key:** `logo` — a URL string. `logo` is a `URLField(max_length=200)`, so keep the whole URL under
  200 characters.
- **Validation:** the serializer strips whitespace and applies Django's `URLValidator`; a non-URL fails
  the whole request with `Invalid URL`. `""` or `null` clears the field.
- **Before the payload:** a git-hosted logo must be pinned to an exact commit SHA
  (`https://raw.githubusercontent.com/<owner>/<repo>/<40-hex-sha>/<path>`, or
  `https://media.githubusercontent.com/media/…` when the path is Git-LFS-tracked) — never a branch
  (`/main/`, `/master/`, `refs/heads/…`) and never a `/blob/` page URL. Fetch it before putting it in the
  payload and require an `image/*` content-type. A logo on a non-git host has no commit to pin and is a
  valid value once reachability is confirmed.
- **Validator severity:** a `content-type` that is not `image/*` is an **ERROR**; a git-hosted URL with a
  branch reference or a `/blob/` segment is an **ERROR** (suggested fix: the commit-pinned raw URL); a
  non-git host is never reported as "unpinned"; an image that does not read as a logo is **never an
  ERROR** — it is a WARNING asking the user to decide, satisfied outright when the dossier records that
  the project presents the image as its logo or that the value was already reviewed and approved.
- **PATCH** is a plain scalar replace; nothing is minted.
- **Change class:** dynamic — a refresh checks it every time (`curl -sIL`, require `image/*`).

## Worked examples

- **A registry-declared plot kept (LOWTRAN).** The PyHC registry's `logo:` is a README gallery figure —
  transmittance and path radiance against wavelength — with no designed mark anywhere in the tree. The
  project presents it as its logo, so rule 2 includes it, and once stored rule 1 keeps it. The registry's branch URL is re-derived to a commit-pinned raw URL under rule 7.
- **A test-fixture plot excluded (GEOrinex).** The only image in the tree is a four-panel GPS observation
  plot under `src/georinex/tests/`, which the README embeds mid-page as an example "RINEX plot". No header
  placement, docs logo, logo file or registry `logo:` presents it as the project's mark. Rule 4 fires:
  Field 33 stays empty, with the pinned candidate URL and its verification recorded.
- **An institution's mark excluded (IGRF-14).** The agency product page displays the developing
  association's logo. The software has no mark of its own and does not present that one as its logo, so
  rule 5 fires; the URL is recorded as a rejected alternative for a curator who wants it deliberately.
- **A theme's icon, not the package's (sunkit-instruments).** The repository tracks no image and
  `conf.py` sets no `html_logo`, but the rendered docs show the SunPy icon supplied by the shared theme.
  Rule 5 excludes it and rule 6 records an evidenced absence.
- **An LFS-tracked logo (Kaiju).** `conf.py` designates the MAGE logo, but the repository moved PNGs into
  Git LFS, so the raw URL serves a 131-byte `text/plain` pointer. Rule 8 fires: the value is the
  commit-pinned `media.githubusercontent.com` URL, fetched and confirmed as image bytes.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 755-776 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
