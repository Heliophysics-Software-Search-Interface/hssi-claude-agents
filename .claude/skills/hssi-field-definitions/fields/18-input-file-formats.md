# Field 18 — Input File Formats

**Level:** RECOMMENDED · **API:** `inputFormats[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/FileFormat/rows/all/`
**Filter tab:** none · **Free-text search tier:** T4.6 (name, extension) · **Field-search code:** `input`

## What it is

**Type:** Multi-select dropdown

**What it is:** The file formats the software supports for data input.

**How to fill it:** Select all file formats your software supports for input files. Only formats actually supported should be indicated.

<!-- vocab:FileFormat begin -->
**Possible Values** — *11 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/FileFormat/rows/all/` is authoritative. Fields 18 and 19 draw on the same vocabulary.*

- ascii
- CDF
- csv
- FITS
- HDF5
- IDL.sav
- ISTP-Compliant
- JSON
- netCDF3/4
- Other
- Zarr
<!-- vocab:FileFormat end -->

This file holds the shared guidance for both format fields — sources, traps, row mapping and payload
notes. Field 19 (Output File Formats) uses the same vocabulary and points here for everything except
its own output rubric.

## Why it exists

A user holding data in a particular format — FITS images, CDF files, HDF5 archives — wants the
software that can open it. The value tells them, before they install anything, that the tool reads
their files. A format listed that the code cannot read costs that user an install and makes format
search useless; a format the code reads but the record omits hides the tool from the users it would
serve best.

## How it appears on the site

- **Detail page:** "Data & File Formats" section, "Input Formats" row; one plain (unlinked) tag per
  value, showing the row name.
- **Filter tab:** none.
- **Free-text search:** tier T4.6 (format name and extension).
- **Field search:** `input:"…"` matches `input_formats__name__icontains` or
  `input_formats__extension__icontains`. The rows' `extension` values are empty in the vocabulary
  snapshot, so in practice the name is what matches.
- **JSON-LD:** each value is emitted under `keywords` as a `DefinedTerm` with `description`
  `inputFormats` and `inDefinedTermSet` the HSSI-vocab InputFileFormats term set.

## Rubric: include / exclude

Rules 1–6 decide whether a candidate format is included: apply them top to bottom for each candidate
and stop at the first that fires. Rule 7 maps each included format to its row; rules 8–9 govern the
incumbent value and an empty result.

1. **A format read only by the test suite, a regression fixture or a benchmark → exclude.** A reference
   text file read by one test is not a format the API accepts.
2. **A format read only through a companion package, plug-in or separately installed reader → exclude.**
   The field records what this distribution itself can read; the format belongs to the companion's
   entry, and the companion goes in Field 29 or 30. Fires on: no reader for the format in this package
   (pysat and CDF, which pysatCDF reads).
3. **Bytes passed through unread → exclude.** Files a tool uploads, copies or streams without parsing
   are not an input format it supports.
4. **A file the software writes and reads back for its own bookkeeping → exclude** (a cached file list,
   a state or parameter JSON). A file the user supplies and the software parses counts even when it is
   configuration rather than science data (an `.ini` of deposit metadata → `Other`).
5. **The pinned code reads the format → include.** Evidence is a public reader, loader or CLI option
   that opens the format, or format-library I/O in the installed package: `astropy.io.fits`, `h5py`,
   `netCDF4`, `cdflib`, `pandas.read_csv`, `pandas.read_hdf`, `scipy.io.readsav`,
   `xarray.open_dataset`, `zarr`. A documented workflow shipped with the software (tutorial notebooks,
   examples) that reads the format as the software's input, backed by a declared dependency on the
   format's backend, also counts.
6. **A generic multi-instrument format belongs here, not in Fields 31/32.** A reader for any mission's
   CDF or FITS files is the format `CDF` or `FITS`; it is not a list of instruments.
7. **Map each included format to its row:**
   - comma-separated tables → `csv`; add `ascii` too when the reader accepts arbitrary delimited plain
     text (a `sep` or `read_csv` keyword pass-through), because a whitespace-delimited table is not a
     CSV. `ascii` means ASCII **data tables** — not a configuration stanza and not a progress-bar flag.
   - IDL save files → `IDL.sav`; netCDF of either generation → `netCDF3/4`; HDF5 (including files read
     via `pandas.read_hdf` / PyTables) → `HDF5`.
   - `ISTP-Compliant` when the software's documentation or reader targets the SPDF ISTP/IACG metadata
     conventions, in addition to the container format's own row.
   - `Other` **only for a real, named format with no row** (PGM, PNG inside a tar, INI), with the format
     named in the note — never as a stand-in for "any format a plug-in might read".
8. **Incumbent values are held to the same rules.** This field is enrich-only: an enrichment adds the
   formats rule 5 admits that the record lacks, keeping the stored ones. A full refresh also removes a
   stored format the pinned code cannot read, with the reason recorded — the usual source is a registry
   taxonomy tag (PyHC keywords such as `cdf`, `ascii`, `hdf5`) propagated into the record.
9. **Empty is legitimate** when the software reads no files (its API takes in-memory arrays, or fetches
   data over a network API into memory). Record the search that shows it.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

**Sources, in priority order:**
1. Code analysis (file I/O operations) at the pin: public reader and loader functions and their
   docstrings, CLI options, and the format libraries the installed package imports.
2. Documentation: the docs' supported-formats pages, tutorials and examples.
3. README.md feature lists.
4. Dependencies that exist only to read a format (`tables` for HDF5 via pandas, `cdflib`, `netCDF4`).

**Check for file format support not mentioned:**
- Grep for common format indicators: `fits`, `hdf5`, `netcdf`, `cdf`, `csv`, `json`, `zarr`
  (`git grep -n -i -P 'fits|hdf5|netcdf|\bcdf\b|csv|json|zarr' <pin> -- <package dir>`), and read the
  matching lines.
- Check import statements for format-specific libraries.
- Back every negative with a positive control on the same scope (a format the code does read must
  match), and state the file scope beside every count.

**Traps:**
- **Registry taxonomy tags classify the package, not its readers.** A PyHC keyword list that includes
  `cdf` or `ascii` is not evidence the code reads CDF or ASCII; inherited input and output lists that
  are identical are a sign both came from tags.
- **Base64 notebook payloads match short patterns.** `\bcdf\b` can hit inside an embedded image in an
  `.ipynb`; read the match.
- **Unrelated identifiers.** tqdm's `ascii=` progress-bar parameter, a JSON file of the package's own
  parameters, and a docstring that mentions a format all match a grep and are not formats read.
- **A format is not a language.** Reading IDL save files makes `IDL.sav` an input format; it does not
  put `IDL` in Field 13.
- **A format is not an instrument.** A generic reader goes here, not in Fields 31/32 (rule 6).

## Payload and roundtrip notes

- **Keys:** `inputFormats` (this field) and `outputFormats` (Field 19) — arrays of row names.
- **Binding:** each name is stripped and matched with `FileFormat.objects.filter(name__iexact=…)
  .first()`; no match raises `{"FileFormat": "Unknown value '<v>'."}` (400). Case is ignored
  (`csv`, `FITS`), spelling is not (`netCDF3/4`, `IDL.sav`, `ISTP-Compliant`).
- **PATCH** replaces the whole set; `[]` or `null` clears it; an omitted key leaves it unchanged. Not a
  sorted field — compare as a set.
- **Readback:** `/api/view/` returns names and omits an empty list entirely (a missing `outputFormats`
  key means empty, not a different field); `/api/data/` returns row UUIDs — resolve them before treating
  the list as drifted.

## Worked examples

- **A format only a companion reads (pysat).** The stored `CDF` is removed: no CDF library is imported
  anywhere in the package, and CDF reading is what pysatCDF exists for (rule 2), which is recorded in
  Field 30. `netCDF3/4` (`load_netcdf`), `csv` (`load_csv_data`) and `ascii` (arbitrary `read_csv`
  keyword pass-through) stay under rules 5 and 7.
- **Readers decide, tags do not (PyAuroraX).** The readers' docstrings name PGM, HDF5, PNG-in-tar and
  IDL-save skymap and calibration files, so `HDF5`, `IDL.sav` and `Other` (PGM, PNG) are recorded. The
  stored `CDF` and `ascii` came from registry tags; the only grep hits are base64 image data and tqdm's
  `ascii` parameter, so both are removed (rule 8).
- **The documented workflow's format (SAVIC).** The package exposes no reader, but its tutorials read
  the bundled `.h5` example with `pd.read_hdf` and it declares `tables` as a dependency; rule 5 keeps
  `HDF5`.
- **A configuration file and a pass-through (pyzenodo3).** The only file parsed is a user-supplied
  `.ini` of deposit metadata → `Other` (rule 4); upload payloads are streamed unread (rule 3); the JSON
  it reads back is a file it has just written (rule 4). `ascii` is not taken for the `.ini` because the
  row signals data tables.

## Provenance

- Vocabulary block `vocab:FileFormat` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 478-500 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
