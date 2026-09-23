# Field 13 — Programming Language

**Level:** RECOMMENDED · **API:** `programmingLanguage[]` · **Change class:** dynamic
**Vocabulary:** `/api/models/ProgrammingLanguage/rows/all/`
**Filter tab:** Language · **Free-text search tier:** T4.2 · **Field-search code:** `lang`

## What it is

**Type:** Multi-select dropdown

**What it is:** The computer programming languages most important for the software.

**How to fill it:** Select the most important languages (e.g., Python, Fortran, C). This is not meant to be an exhaustive list.

Note the exact spellings: **`Javascript`** (not `JavaScript`) and **`Typescript`** (not `TypeScript`).
The Fortran rows are also inconsistent: `Fortran77` and `Fortran90` have no space; `Fortran 2003`,
`Fortran 2008` and `Fortran 2023` do. There is no `Fortran 2018` row and no `Cython`, `R`, `Perl` or
`Go` row.

<!-- vocab:ProgrammingLanguage begin -->
**Possible Values** — *19 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/ProgrammingLanguage/rows/all/` is authoritative.*

- C
- C#
- C++
- Fortran 2003
- Fortran 2008
- Fortran 2023
- Fortran77
- Fortran90
- IDL
- Java
- Javascript
- Julia
- MATLAB
- Other
- Python 2.x
- Python 3.x
- Rust
- SQL
- Typescript
<!-- vocab:ProgrammingLanguage end -->

## Why it exists

A user who has to write code against the software, or build it, needs to know which languages that
involves: a Python user wants Python packages, an IDL user wants something they can call from IDL, and
a packager needs to know a Fortran or C compiler is involved. The Language filter tab is one of the
four ways to narrow the catalogue, so a wrong value sends users to software they cannot use (a Python
package tagged `IDL` because it reads IDL save files) and a missing one hides software from exactly the
users it serves. A padded list — every file extension in the tree, build tooling, a vendored reference
file — makes the filter promise something the software does not deliver.

## How it appears on the site

- **Detail page:** "Technical Details" section, "Programming Languages" row; one tag per value, each
  linking to the homepage filtered by that language.
- **Filter tab:** Language. The tab **folds every Python row into one "Python" item and every Fortran
  row into one "Fortran" item**, so the choice between `Python 2.x` and `Python 3.x`, or among the
  Fortran standards, does not change whether a filtering user finds the entry; it changes the tag the
  user reads on the detail page.
- **Free-text search:** tier T4.2 (`programming_language` name).
- **Field search:** `lang:"…"` matches `programming_language__name__icontains`, so `lang:"Python"`
  matches both Python rows and `lang:"Fortran"` matches every Fortran row.
- **JSON-LD:** emitted as `programmingLanguage` (a single string when there is one value, else a list).

## Rubric: include / exclude

Rules 1–4 decide **which languages count**, by the kind of software; apply the first of them that
matches the software and stop. Rules 5–7 then decide **which vocabulary row** each counted language
becomes. Rules 8–10 govern the incumbent value and an empty result.

1. **Website or hosted service with no exposed source.** Record the implementation language only when
   it is disclosed (the service's own documentation, a paper, a SPASE or registry record); otherwise
   the field is evidenced-empty. **Never record the client language** — the Javascript of a web page or
   the language of a user's HTTP calls is not the software's implementation. Fires on: no source code a
   user can obtain.
2. **Model without public source (e.g. CCMC-hosted).** Record the implementation language stated on the
   model page or in its paper (CCMC's structured record carries it as `code: {languages: …}`); otherwise
   empty. Fires on: a model whose code is not distributed.
3. **IDL or MATLAB library.** Record that language. A MATLAB (or IDL) front end over a Fortran core
   lists both. Fires on: the software's own API is IDL or MATLAB code.
4. **Source-available package or library.** Record **the language a user writes to use it plus any
   compiled or scripted core in the repository that carries the science** (a Python wrapper over a
   Fortran core lists both). **Vendored code counts only as the science core:** a third-party C or
   Fortran library the package compiles or calls to do its science (a vendored model, a bundled CDF
   library) lists that language; vendored or archived third-party code the package does not build or
   call is excluded. Exclude build, CI and documentation tooling (CMake, Meson, Make, shell scripts, the
   generated Javascript of a built docs site) and test-only languages (a test harness not installed with
   the package). A **supported front end** in a second
   language that ships with the software and has its own tests or build target counts (a MATLAB
   package directory with a test suite); a stub the author marks as not working, or that nothing builds
   or runs, does not. Fires on: public source.
5. **Python rows.** Record `Python 3.x` when `requires-python`, the classifiers or the code say Python 3.
   Add `Python 2.x` only if Python 2 is **still targeted** (a classifier, a `python_requires` that admits
   2.7, CI on 2.7). When the code is Python-2-only, record `Python 2.x` and **not** `Python 3.x`.
6. **Fortran rows: one row per standard the sources actually require**, not every standard they compile
   under. For each Fortran source rule 4 admits, the row is set by its form and the features it uses:
   fixed-form (`.f`, `.for`) with nothing later → `Fortran77`; free-form (`.f90`) or Fortran 90 syntax
   (attribute declarations with `INTENT`, `DO WHILE … END DO`) with nothing later → `Fortran90`; a
   Fortran 2003 feature (`use, intrinsic :: iso_fortran_env`, deferred-length `character(:),
   allocatable`) → `Fortran 2003`; a Fortran 2008 feature (`error stop`, `do concurrent`, submodules,
   coarrays) → `Fortran 2008`. A compiler `-std=` flag in the build names the standard the project
   targets and counts as evidence for that row; `-std=legacy` names no standard and adds none. The field
   is the union over the admitted sources.
7. **A real language with no row** (R, Perl, Go) that rule 4 admits → `Other`, with the language named
   in the dossier note. `Other` is never a stand-in for a file format (Jupyter Notebook), a build
   system, glue code (a single Cython bridge between two counted languages) or "and some other files".
8. **Use the exact row spelling** from the live vocabulary: `Javascript`, `Typescript`, `Fortran77`,
   `Fortran 2003`. A value with no row cannot be written; map it by rules 5–7 or drop it.
9. **Incumbent values are held to the same rules.** On a refresh or enrichment, keep a stored value the
   rules admit, add what they admit and the record lacks, and remove a stored value they exclude (an
   `IDL` inferred from a data format or a deposit title; `Python 3.x` on Python-2-only code; a build
   system; a test-only language). Record the reason for every removal so the value is not re-proposed.
   This field is dynamic: languages change as the software changes, so re-derive it at the pinned
   revision rather than carrying it forward.
10. **Empty is legitimate only when evidenced** — rules 1 and 2 with no disclosed language. Record what
    was searched.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

**Sources, in priority order:**
1. Package configuration at the pin: `requires-python`, `python_requires`, `Programming Language ::`
   classifiers, `ext_modules` / `Extension(...)` in `setup.py`, `[build-system]` requirements, the
   language list of `CMakeLists.txt` / `meson.build`, and compiler flags (`-std=`).
2. A file-extension census of the tracked tree at the pin (`git ls-tree -r --name-only <pin>`), read
   together with what the build compiles and what the package installs (`packages = find:`,
   `MANIFEST.in`, `package_data`). File extensions in the repository are the first signal, not the
   answer.
3. GitHub's language statistics (`/repos/<owner>/<repo>/languages`) and package configuration files —
   corroboration only; Linguist omits vendored, minified and generated files and honours
   `.gitattributes linguist-vendored`, so its byte counts and the tree census legitimately differ.
4. For software without public source: the model page, the service's documentation, the reference
   paper, or the SPASE/registry record. DataCite/Zenodo codemeta `programmingLanguage` and SoMEF output
   are hints to verify, not values to copy.

**Validator checks:** every value is a row of `/api/models/ProgrammingLanguage/rows/all/` (Field 13),
spelled exactly — `Javascript`, `Typescript`. Check actual file extensions in the repo, compare against
what is listed, and flag a significant language present but unlisted — then apply rule 4 before calling
it missing.

**Traps:**
- **Build systems are not languages.** CMake, Meson and Make show up in automated extractions; they have
  no row and are excluded by rule 4.
- **Jupyter Notebook is not a language.** GitHub reports it as one; the notebooks' kernel language is
  what counts.
- **A data format named after a language is Field 18.** Reading IDL `.sav` files through
  `scipy.io.readsav` makes `IDL.sav` an input format, not `IDL` a language.
- **A deposit or title naming a sibling library** ("PyAuroraX and IDL-AuroraX") is evidence about the
  deposit, not about this software; the sibling belongs in Field 29.
- **Python 2 syntax in a docstring** (`print inst` inside a module docstring) is a stale example, not
  Python 2 support; the executable `requires-python` governs. Conversely, extension modules that include
  `<python2.5/Python.h>` and call `Py_InitModule` with no `PyInit_` anywhere are mechanical proof of
  Python-2-only code.
- **Vendored third-party code in an `archive/` directory**, marked `linguist-vendored`, unpackaged and
  untested, is excluded even when it is the largest file in the tree (an instrument team's IDL reader
  kept for reference).
- **A README "requires gfortran" note** may be for building a dependency, not this package; check for
  Fortran sources in the tree before recording a Fortran row.
- **gfortran diagnostics cascade.** A rejected nonstandard declaration (`REAL*8`) makes gfortran re-read
  later array assignments as pointer-function results and emit spurious `Fortran 2008: Pointer procedure
  assignment` errors; confirm a feature with a minimal control (`DOUBLE PRECISION` in place of
  `REAL*8`) before counting it. When ranking sources with a `gfortran -std=<edition> -c` ladder, each
  rung's first diagnostic is only the earliest blocker at that level, and a clean pass needs a positive
  control (a file known to fail) to mean anything.
- **Compile-to-a-standard is not the criterion.** A fixed-form file that builds only under
  `-std=legacy` still has a requirement set by what it uses; do not drop `Fortran77` because no numbered
  standard accepts the file, and do not add `Fortran 2008` because the file compiles under it.

## Payload and roundtrip notes

- **Key:** `programmingLanguage` — an array of row names.
- **Binding:** each name is stripped and matched with `ProgrammingLanguage.objects.filter(name__iexact=…)
  .first()`; no match raises `{"ProgrammingLanguage": "Unknown value '<v>'."}` (400). Case is ignored,
  spacing and spelling are not (`Fortran 77` fails).
- **PATCH** replaces the whole set (`.set()`); `[]` or `null` clears it; an omitted key leaves it
  unchanged. It is not a sorted field — compare as a set.
- **Readback:** `/api/view/` returns names; `/api/data/` returns row UUIDs — resolve them before treating
  the list as drifted.
- The model has a `version` column appended to the display string when set; JSON-LD uses that display
  string.

## Worked examples

- **Fortran standards by requirement (IRI-90).** A Python 3 package over a vendored fixed-form IRI
  library, a free-form driver and an extension source. Rule 4 admits Python and the Fortran; rule 6 maps
  each source by what it needs: the fixed-form library → `Fortran77`, its files using `INTENT`
  attribute declarations and `DO WHILE … END DO` → `Fortran90`, the driver's deferred-length allocatable
  character → `Fortran 2003`, the extension's deliberate `error stop` → `Fortran 2008`. `Fortran 2023`
  is excluded because nothing uses a later feature, the build's `-std=legacy` adds no row, and CMake and
  Meson are not languages.
- **Test harness out, front end in (LOWTRAN).** The vendored fixed-form engine that pip compiles →
  `Fortran77`; the Python API → `Python 3.x`; the shipped `+lowtran` MATLAB package with its own
  `runtests` target → `MATLAB` (rule 4's supported front end). The free-form Fortran test driver built
  only by the CTest path is test-only, so `Fortran90`/`2003`/`2008` are not recorded despite its
  constructs.
- **A Cython bridge is not a language (pyflct).** The science is a vendored C library, the user writes
  Python, and one `.pyx` file glues them: `C` and `Python 3.x`. Recording `Other` for Cython (there is no
  `Cython` row) would tell a searcher nothing, so rule 7 does not fire.
- **A broken stub is not a front end (ReesAurora).** The one MATLAB file is a thirteen-line test stub
  that prints that it is "not working" and imports a module renamed away years earlier; nothing builds,
  ships or runs it. The incumbent `MATLAB` is removed under rules 4 and 9, leaving `Python 3.x`; the
  README's gfortran note is for the `msise00` dependency, so no Fortran row either.
- **A format and a sibling are not a language (PyAuroraX).** The tree has no `.pro` file; `IDL` appears
  only in dataset names ("IDL save format") and in a Zenodo deposit title shared with the separate
  IDL-AuroraX library. The incumbent `IDL` is removed; IDL save files go to Field 18 as `IDL.sav` and the
  IDL library to Field 29.

## Provenance

- Vocabulary block `vocab:ProgrammingLanguage` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 305-337 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
