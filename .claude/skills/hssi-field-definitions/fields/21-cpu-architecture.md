# Field 21 — CPU Architecture

**Level:** RECOMMENDED · **API:** `cpuArchitecture[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/CpuArchitecture/rows/all/`
**Filter tab:** none · **Free-text search tier:** T4.7 · **Field-search code:** `cpu`

## What it is

**Type:** Multi-select dropdown

**What it is:** The CPU architecture the software requires.

**How to fill it:** Select all CPU architectures the software can successfully be installed and executed on.

<!-- vocab:CpuArchitecture begin -->
**Possible Values** — *9 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/CpuArchitecture/rows/all/` is authoritative (`CPUArchitecture` also resolves — model names are case-insensitive).*

- x86-64
- Apple Silicon arm64
- Sun (SPARC)
- Linux aarch64 or arm64
- CPU Independent
- GPU
- HPC or HEC
- ppc64le
- Other
<!-- vocab:CpuArchitecture end -->

Note the spellings: the row is `x86-64` (hyphen), while wheel tags and `uname` write `x86_64`; arm64
is split into `Apple Silicon arm64` (macOS) and `Linux aarch64 or arm64` (Linux). `GPU` and
`HPC or HEC` describe the hardware the software computes on, not an instruction set, and sit alongside
an architecture row rather than replacing it.

## Why it exists

A user on an Apple Silicon laptop, an ARM Linux server or a cluster needs to know whether the software
runs on their hardware, and a user with a GPU or supercomputer allocation wants tools that use it. The
value answers both. A row the software has never been built or run on promises something a user will
discover is false only after trying; pinning portable code to one architecture hides it from users on
every other; `GPU` or `HPC or HEC` on software that merely could run there misleads users looking for
accelerated or parallel tools.

## How it appears on the site

- **Detail page:** "Technical Details" section, "CPU Architecture" row; one plain (unlinked) tag per
  value.
- **Filter tab:** none.
- **Free-text search:** tier T4.7 (`cpu_architecture` name).
- **Field search:** `cpu:"…"` matches `cpu_architecture__name__icontains`.
- **JSON-LD:** emitted as `processorRequirements` (a list).

## Rubric: include / exclude

Rules 1–5 decide the architecture rows by how the software reaches the user's machine; apply the first
that matches and stop. Rules 6–7 add `GPU` and `HPC or HEC` independently of them. Rules 8–10 govern
other rows, the incumbent value and an empty result.

1. **A web application used through a browser** → `CPU Independent`; computation happens server-side
   and nothing is compiled for the user's machine.
2. **A hosted model or service whose code is not distributed, with no platform statement** →
   evidenced-empty. Language portability is not evidence.
3. **Pure interpreted code** (no compiled extension, no architecture-specific dependency built by the
   project) → `CPU Independent`. A macOS CI runner does not add an arm64 row.
4. **Portable source compiled on the user's machine at install time**, with no architecture-specific
   code (no SIMD intrinsics, inline assembly, architecture-conditional compilation or CPU-specific
   flags) → `CPU Independent`, **plus the architecture of any binary the project itself published**.
   Do not pin portable source to `x86-64` without such a binary.
5. **Distributed as prebuilt binaries** (wheels, conda packages, release binaries) whose source build is
   not a documented, working route elsewhere, **or built from source only through architecture-specific
   build configurations** (per-platform makefiles or optimization flags for named machines) → **the
   architectures of the published artifacts or of the targeted platforms**, reading artifact filenames
   as: `x86_64` / `amd64` / conda `linux-64`, `osx-64`, `win-64` → `x86-64`;
   `macosx_*_arm64` / conda `osx-arm64` → `Apple Silicon arm64`; `manylinux_*_aarch64` / conda
   `linux-aarch64` → `Linux aarch64 or arm64`; `ppc64le` → `ppc64le`. **Not `CPU Independent`.** An
   architecture the project tests and fails on is excluded; an arm64 row needs an arm64 artifact, a
   passing job on an arm64 runner, or a documented successful build — never a Mac OS row or a Mac CI
   runner alone.
6. **`GPU`** when the software computes on a GPU: CUDA/OpenACC/OpenMP-offload code, device selection
   such as `accelerator="gpu" if torch.cuda.is_available()`, or a documented GPU requirement. Not when a
   dependency merely could use one.
7. **`HPC or HEC`** when the software targets clusters: MPI domain decomposition, batch-scheduler
   (PBS, Slurm) scripts, documented supercomputer builds. Multi-GPU training on a single machine is not
   HPC.
8. **`Sun (SPARC)` and `Other`** need explicit evidence for this software; a vendored library's platform
   list does not count.
9. **Incumbent values are held to the same rules.** This field is enrich-only: an enrichment adds the
   rows the rules admit that the record lacks, keeping the stored ones. A full refresh also removes a
   stored value the rules exclude — `CPU Independent` on a binary-only package, `x86-64` on portable
   source with no published binary, an arm64 row the project's own tests fail — with the reason
   recorded.
10. **Empty is legitimate** under rule 2. Record what was searched.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

**Sources, in priority order:**
1. Published artifacts: PyPI wheel filenames from the JSON API (`/pypi/<name>/json`, every release's
   `urls`), conda-forge subdirs, GitHub release binaries.
2. CI configuration and run history: `cibuildwheel` targets (commented-out targets are a deliberate
   absence), matrix `runs-on`, and which jobs actually ran and passed.
3. Build configuration: compiled extensions, compiler flags (`-march`, `-fopenmp`), MPI/CUDA
   dependencies, scheduler scripts.
4. Installation documentation (platform-specific prefixes, supported hardware).
5. The source itself, for rule 4's architecture-specific-code test.

**Validator checks:** every value is a row of the live `/api/models/CpuArchitecture/rows/all/`
(`CPUArchitecture` also resolves), spelled exactly — `x86-64`, not `x86_64`.

**Traps:**
- **Cancelled is not failed.** A job cancelled because its runner label was retired says nothing about
  the software; a job that ran and failed is evidence against that architecture.
- **A job's name is not its runner.** Read `runs-on`; macOS runner labels differ in architecture, so
  determine which one the job used before counting it for either Mac row.
- **Short-pattern greps for architecture code** (`sse|avx|intrin|x86|arm|asm`) hit unrelated
  identifiers — `asm` inside `PyDict_AsMapHeader` — so read every match before counting it.
- **Intel-only Homebrew prefixes** (`/usr/local/lib`) in install docs are a signal that a documented
  macOS recipe targets Intel, not Apple Silicon.
- **A `TODO` for an architecture is an intention**, not support.

## Payload and roundtrip notes

- **Key:** `cpuArchitecture` — an array of row names.
- **Binding:** each name is stripped and matched with `CpuArchitecture.objects.filter(name__iexact=…)
  .first()`; no match raises `{"CpuArchitecture": "Unknown value '<v>'."}` (400) — `x86_64` fails.
- **PATCH** replaces the whole set; `[]` or `null` clears it; an omitted key leaves it unchanged. Not a
  sorted field — compare as a set.
- **Readback:** `/api/view/` returns names; `/api/data/` returns row UUIDs — resolve them before treating
  the list as drifted.

## Worked examples

- **A tested failure removes arm64 (pyflct).** A compiled extension shipped as wheels and conda builds,
  every one of them x86_64; the arm64 wheel targets are commented out and the project's own arm64 job,
  named `failing_mac_arm`, fails after a real build. Rule 5 gives `x86-64` alone and the stored
  `Apple Silicon arm64` is removed; Field 20's `Mac` is read together with it as Intel-only.
- **Portable source is not pinned (TomograPy).** A C kernel compiled at install with only OpenMP
  pragmas and no architecture-specific code → `CPU Independent` (rule 4); the stored `x86-64`, with no
  published binary behind it, is removed.
- **Portable source plus one binary (python-magnetosphere).** The C sources carry nothing
  architecture-specific, and the author published one `linux-x86_64` build: `CPU Independent` and
  `x86-64` together (rule 4).
- **GPU without HPC (Surya workshop).** The training script selects a CUDA device and the fine-tuning
  workload is impractical without one → `GPU` (rule 6); multi-GPU runs on one cloud instance with no MPI
  or scheduler, so rule 7 does not fire. Its only documented install route downloads the
  `Linux-x86_64` Anaconda build → `x86-64` (rule 5).
- **A cluster model (TIE-GCM).** Compiled Fortran with per-platform build files and optimization flags
  for named x86-64 supercomputers and generic 64-bit Linux → `x86-64` (rule 5); PBS scripts, MPI
  decomposition and parallel I/O add `HPC or HEC` (rule 7); no CUDA or offload directives, so no `GPU`.

## Provenance

- Vocabulary block `vocab:CpuArchitecture` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 547-567 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
