# Field 24 — Documentation

**Level:** RECOMMENDED · **API:** `documentation` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.8 · **Field-search code:** `docs`

## What it is

**Type:** URL

**What it is:** Link to the documentation and installation instructions. If this is the same as the access URL, then enter that link here.

**How to fill it:** Documentation link including installation instructions. Should be entered as a complete URL.

## Why it exists

The "Docs" button is where a user who has found the software learns to install and use it. A dead link,
a documentation build the project has abandoned, or a portal that documents something other than this
package sends that user away with wrong or no instructions. Documentation URLs move more often than
anything else in the record — hosting changes, renames, new build systems — so a stored value that once
worked is the most likely field in an entry to go stale.

## How it appears on the site

- **Detail page:** a "Docs" action button linking to the stored URL, shown only when the field is set.
  The homepage result card carries the same "Docs" button.
- **Filter:** none.
- **Free-text search:** tier T4.8 (`documentation`).
- **Field search:** `docs:"…"` matches `documentation__icontains`.
- **JSON-LD:** emitted as `codemeta:buildInstructions`.

## Rubric: include / exclude

Rules 1–5 choose the documentation — apply them top to bottom and stop at the first that fires. Rule 6
then normalises the chosen URL and always runs. Every value is verified by fetching it (see
*Where to find it*) before it is recorded, and every URL considered and not used is recorded with the
reason — especially a declared URL that is dead, so a later refresh does not "correct" the field into it.

1. **The stored URL is dead or serves a stale build, and the project names a working successor → the
   successor.** A documentation site the project has moved away from (the README now links only the new
   site; the build configuration for the old one was deleted) is replaced even if the old site still
   answers 200, because it serves instructions the project no longer maintains. Fires on: the project's
   current README or `[project.urls]` names a different documentation site, and the old one is dead or is
   built from configuration no longer in the repository.

2. **The project's own declared documentation URL is dead but the stored one works → keep the stored
   one.** Package metadata can point at a page that no longer exists (a docs path broken by a repository
   rename, a hosting move the metadata never caught up with). Record the dead declared URL and its
   response so a refresh does not replace a working value with a 404. Re-test both before changing
   anything. Fires on: the declared URL fails to reach a terminal 200 while the stored URL serves this
   package's documentation.

3. **The project's own documentation site → the value.** A documentation site generated for this
   package — Read the Docs, GitHub Pages, an MkDocs or Sphinx build, a manual hosted by the project — named
   by the project (`[project.urls] Documentation`, a README documentation link or badge,
   `.readthedocs.yml`/`.readthedocs.yaml`, an MkDocs `site_url`, a Pages deploy workflow, the PyHC
   registry `docs:`). It must document **this package**: a project homepage, an organization portal, a
   data portal, or the parent project's docs is not it, even when the package metadata lists it as `url`.
   A page for the wrapped model that the project itself nominates as its documentation (its registry
   `docs:` value) counts. Fires on: such a site exists and resolves.

4. **A wiki that holds real documentation → the wiki, when nothing else documents what it does.** A
   repository's wiki is a **separate git repository** (`<repo>.wiki.git`): clone it to see whether it has
   pages. `has_wiki: true` in the GitHub API proves nothing either way — it says only that the feature is
   enabled, and a wiki can exist while the flag is false. Record the wiki when it carries documentation
   pages that no other link from the entry surfaces, even if the installation instructions live in the
   README; Field 3 already puts the README one click away. A wiki the README designates as the project's
   documentation qualifies directly. An empty wiki, or one holding only a placeholder page, is not
   documentation. Fires on: the cloned wiki has substantive pages.

5. **The README is the only documentation → the repository URL.** The form says: "If this is the same as
   the access URL, then enter that link here." When there is no documentation site, no `docs/` build, no
   documentation-bearing wiki, and the README carries the installation and usage instructions, record the
   Field 3 value — the README renders on the repository's landing page. An incumbent that points at the
   README file itself (`/blob/<branch>/README.md`, `#readme`) and resolves is kept: it is the same
   documentation, and changing it gains the user nothing. A repository folder or manual file that the
   project designates as its documentation (`documentation/`, a PDF manual) is recorded as that path
   instead. Fires on: an exhaustive negative for every source in rules 1–4.

6. **Prefer the stable landing page over a versioned deep link.** Record the documentation root or its
   default version (`/en/latest/`, `/en/stable/`), not a pinned release (`/en/v1.2.3/`) or an individual
   page, unless the project itself nominates the deep page as its documentation entry point. Prefer the
   redirect-free form of the landing page, and `https://` when the `http://` form redirects to it. Keep an
   incumbent's choice between equivalent landing forms (`latest` versus `stable`, bare host versus
   `/en/latest/`) when both resolve. Fires on: a candidate or incumbent that is a versioned or deep link.

7. **Dead with no successor → clear it, and record the dead URL.** A URL that does not resolve serves no
   one; record what it was, what it returned, and what was searched. Fires on: the stored URL fails to
   reach a terminal 200 and rules 1–6 find no replacement.

8. **Otherwise keep the stored value.** A resolving URL that documents this package is not replaced by an
   equivalent alternative. Fires on: every remaining case.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

**Sources, in priority order:**
1. `pyproject.toml` / `setup.cfg` `[project.urls]` or `project_urls` `Documentation`; the PyPI JSON
   `project_urls`.
2. README.md links and documentation badges.
3. Documentation configuration in the repository: `.readthedocs.yml` / `.readthedocs.yaml`, `docs/conf.py`,
   `mkdocs.yml`, a Pages deploy workflow (`mkdocs gh-deploy`, a `gh-pages` publish step), the `docs/`
   folder.
4. The GitHub API: `homepage`, `has_pages`.
5. The wiki: `git clone https://github.com/<owner>/<repo>.wiki.git` — its own HEAD and last-commit date
   show whether it is maintained.
6. The PyHC registry `docs:` field.

**Verification:** resolve the URL following redirects to a terminal 200, and confirm the page is this
package's documentation:

```
curl -sIL {URL}                                          # every hop and the final status
curl -s -o /dev/null -w "%{http_code} %{url_effective}\n" -L {URL}
```

Cross-check the result against the README links and the `docs/` folder, and read the page title: it
should name this package. The URL must be complete with protocol.

**Traps:**
- **`has_wiki` is not evidence** in either direction; probe `<repo>.wiki.git`. A wiki can also carry
  release policy that decides Field 12.
- **GitHub Pages does not redirect after a repository rename**, unlike the repository itself: the old
  Pages path 404s while the repository's own links to it may never be updated.
- **A Read the Docs project can outlive the project's move away from it**, still serving an old build and
  still pointing at the repository's former location. Check that the repository still contains the
  build configuration.
- **Never assume a Read the Docs slug.** Confirm the project exists, is linked to this repository, and
  builds this package's documentation.
- **A project homepage is not a documentation page.** `setup.py` `url` and `CITATION.cff` `url` are often
  homepage declarations; a page with no installation instructions for this package is not its docs.
- **A registration-gated documentation link** (redirecting to an access-denied page) is not a public
  documentation URL.

## Payload and roundtrip notes

- **Key:** `documentation` — a URL string.
- **Validation:** the serializer strips whitespace and applies Django's `URLValidator`; a non-URL fails
  the whole request with `Invalid URL`. The column is a `URLField` — keep the value within 200 characters.
- **Clearing:** `""` or `null` stores null.
- **PATCH** is a plain scalar replace; nothing is minted.
- **Roundtrip:** `/api/view/` returns the stored URL; compare the string exactly.
- **Change class:** dynamic — a refresh checks it every time: detect a URL change and verify the URL
  resolves.

## Worked examples

- **A data portal replaced by the package's own docs (MadrigalWeb).** HSSI held the CEDAR Madrigal portal,
  which `setup.py` lists as the project `url` but which has no installation instructions for the package.
  The project's `[project.urls] Documentation`, PyPI, the registry `docs:` and the README all name a Read
  the Docs site built from the repository, with an installation section. Rule 3 fires.
- **Documentation that moved (cdflib).** The stored Read the Docs URL still resolves, but the repository
  deleted its Read the Docs and Sphinx configuration when it moved to MkDocs on GitHub Pages, and the
  README links only the Pages site. Rule 1 fires: the Pages site replaces the stale build.
- **A dead declared URL, a working stored one (pyflct, PyGemini).** pyflct's `setup.cfg` points at a docs
  path that returns 404, while the stored Read the Docs URL serves the documentation; PyGemini's README
  links Pages paths broken by a repository rename, while the stored URL is the repository's own homepage.
  Rule 2 keeps both stored values and records the dead URLs.
- **The wiki kept (LOWTRAN).** The wiki is a separate repository with three pages documenting, card by
  card, how the model's inputs are set; the README does not link it. Rule 4 records the wiki even though
  the installation instructions are in the README, because Field 3 already reaches the README and nothing
  else surfaces the wiki.
- **README-only documentation (ReesAurora).** No documentation site, no `docs/` directory, no wiki
  repository; the README holds the description, install instructions and a worked example. Rule 5
  records the repository URL.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 615-623 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
