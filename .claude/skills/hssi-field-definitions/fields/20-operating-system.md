# Field 20 — Operating System

**Level:** RECOMMENDED · **API:** `operatingSystem[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/OperatingSystem/rows/all/`
**Filter tab:** none · **Free-text search tier:** T4.7 · **Field-search code:** `os`

## What it is

**Type:** Multi-select dropdown

**What it is:** The operating systems the software supports.

**How to fill it:** Select all operating systems the software can successfully be installed on.

<!-- vocab:OperatingSystem begin -->
**Possible Values** — *7 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/OperatingSystem/rows/all/` is authoritative.*

- Linux
- Mac
- MobilePlatform
- Operating System Independent
- Other
- Solaris
- Windows
<!-- vocab:OperatingSystem end -->

> **Trap.** `OS Independent` is **not** a value and never has been; it is rejected on submission.
> The only cross-platform value is `Operating System Independent`, spelled out in full.

## Why it exists

A user on a particular machine wants to know whether the software will install there before trying.
The value answers that for Windows, Mac and Linux users, and `Operating System Independent` tells them
the platform does not matter. A listed OS the software cannot be built on costs a user a failed install;
an OS the project supports but the record omits keeps that platform's users from finding it through an
`os:` search, which matches the specific row name and does not return `Operating System Independent`
records.

## How it appears on the site

- **Detail page:** "Technical Details" section, "Operating Systems" row; one plain (unlinked) tag per
  value.
- **Filter tab:** none.
- **Free-text search:** tier T4.7 (`operating_system` name).
- **Field search:** `os:"…"` matches `operating_system__name__icontains`, so `os:"Windows"` does not
  match an entry that lists only `Operating System Independent`.
- **JSON-LD:** emitted as `operatingSystem` (a single string when there is one value, else a list).

## Rubric: include / exclude

Rules 1–4 decide the value by the kind of software; apply the first that matches and stop. Rules 5–7
qualify the evidence those rules use; rules 8–9 govern the incumbent value and an empty result.

1. **A web application used through a browser, with nothing to install** → `Operating System
   Independent`. The server's or deployment platform's OS is the maintainer's, not a user's, and is not
   recorded.
2. **A hosted model or service whose code is not distributed, with no platform statement** →
   evidenced-empty. Never infer an OS from the language's portability or from where the host happens to
   run the code.
3. **A pure-Python (or other interpreted) package with no compiled extension that declares no OS
   restriction** → `Operating System Independent`, **plus each specific OS the project itself names as
   supported** (an `Operating System ::` classifier, a README or docs statement) **or that its CI runs
   on**. The specific rows are what an `os:` search finds.
4. **A compiled extension or native build** → the OSes it is actually built, tested or published for:
   CI jobs that run there, wheel platform tags (`manylinux`, `macosx`, `win`), conda-forge subdirs
   (`linux-64`, `osx-64`, `win-64`), `Operating System ::` classifiers, and install documentation naming
   the OS. **Never `Operating System Independent`.** Exclude an OS on which the default toolchain cannot
   build it (GCC-only flags such as `-fopenmp` with no platform branch fail under MSVC, the default
   Windows toolchain).
5. **Evidence about other software never counts.** A vendored library's README listing the platforms
   *it* was tested on, or the OS of the host's servers, says nothing about this package.
6. **Read CI by what ran.** Read a job's `runs-on`, not its name (a job called `conda-mac` may run on
   `windows-latest`). A job cancelled because its runner label was retired is evidence of nothing. A
   dated CI failure does not unseat an OS that has published artifacts and a documented install path.
7. **No OS by inference.** A project that says "unix" has not named macOS; a language that is portable
   has not made this code OS-independent. Add the row when the project names it or CI runs there, not
   before. `Solaris`, `MobilePlatform` and `Other` need the same explicit evidence.
8. **Incumbent values are held to the same rules.** This field is enrich-only: an enrichment adds the
   OSes the rules admit that the record lacks, keeping the stored ones. A full refresh also removes a
   stored value the rules exclude — `Operating System Independent` on a compiled package, an OS resting
   only on another program's platform list — with the reason recorded. Package-specific evidence of use
   (the project's own issue tracker showing users building it on that OS) keeps an incumbent row.
9. **Empty is legitimate** under rule 2. Record what was searched.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

**Sources, in priority order:**
1. CI/CD configuration (`.github/workflows`, `.travis.yml`, `.appveyor.yml`, etc.) — the matrix
   `runs-on` values, and the run history for which jobs actually ran and passed.
2. Published artifacts: PyPI wheel filenames from the JSON API, conda-forge subdirs.
3. Installation documentation (platform-specific instructions, "we only support Windows through
   conda").
4. Package metadata: `Operating System ::` classifiers.
5. The build configuration: compiled extensions, compiler flags, hard-coded POSIX paths.

**Validator checks:** every value is a row of the live `/api/models/OperatingSystem/rows/all/`;
`Operating System Independent` is spelled out in full — there is no `OS Independent`.

**Traps:**
- **`Operating System :: OS Independent`** is the Python classifier; the HSSI row is
  `Operating System Independent`.
- **A job's name is not its platform** and a retired runner label is not a test result (rule 6).
- **Hard-coded POSIX paths** (`/usr/lib`, `/usr/local/lib`, `<python2.5/Python.h>`) are evidence against
  Windows for a compiled package.
- **A vendored library's platform list** (rule 5) maps one-to-one onto a tempting set of rows; check
  whose README it is.
- **A Mac row does not imply an arm64 CPU**, and an Intel-only macOS artifact set is qualified by
  Field 21, which is read together with this field.

## Payload and roundtrip notes

- **Key:** `operatingSystem` — an array of row names.
- **Binding:** each name is stripped and matched with `OperatingSystem.objects.filter(name__iexact=…)
  .first()`; no match raises `{"OperatingSystem": "Unknown value '<v>'."}` (400) — which is what
  `OS Independent` returns.
- **PATCH** replaces the whole set; `[]` or `null` clears it; an omitted key leaves it unchanged. Not a
  sorted field — compare as a set.
- **Readback:** `/api/view/` returns names; `/api/data/` returns row UUIDs — resolve them before treating
  the list as drifted.

## Worked examples

- **A pure-Python client that names Windows (MadrigalWeb).** No compiled code and the `OS Independent`
  classifier give `Operating System Independent`; CI on `ubuntu-latest` keeps `Linux`; three installed
  scripts' docstrings say it "runs on either unix or windows", so `Windows` is added (rule 3). `Mac` is
  declined: "unix" is not a claim about macOS and no CI runs there (rule 7).
- **Another program's platform list (python-magnetosphere).** The stored `Linux`, `Mac`, `Solaris`,
  `Windows` map exactly onto a vendored C library's README sentence about where *it* was tested. The
  package itself hard-codes POSIX paths and a Linux binary build, and its own issues show Linux use and
  a Mac build attempt, so `Linux` and `Mac` stay and `Solaris` and `Windows` are removed (rules 5, 8).
- **Artifacts over a dated CI state (pyflct).** A compiled C extension: classifiers name all three OSes,
  PyPI ships Linux and macOS wheels, and Windows is supported through conda-forge `win-64` builds. The
  latest Windows CI run failed and the Intel-macOS job is cancelled on a retired runner, but neither
  unseats a platform with published artifacts and a documented install path (rule 6), so `Linux`, `Mac`
  and `Windows` stay.
- **A toolchain that excludes an OS (TomograPy).** `setup.py` passes `-fopenmp` to every C extension
  with no platform branch, which MSVC rejects. The stored `Operating System Independent` is removed
  (rule 4) and `Windows` is not added, leaving `Linux` and `Mac`.

## Provenance

- Vocabulary block `vocab:OperatingSystem` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 524-546 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
