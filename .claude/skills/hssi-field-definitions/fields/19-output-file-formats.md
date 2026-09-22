# Field 19 — Output File Formats

**Level:** RECOMMENDED · **API:** `outputFormats[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/FileFormat/rows/all/`
**Filter tab:** none · **Free-text search tier:** T4.6 (name, extension) · **Field-search code:** `output`

## What it is

**Type:** Multi-select dropdown

**What it is:** The file formats the software supports for data output.

**How to fill it:** Select all file formats your software supports for generated files. Only formats actually supported should be indicated.

<!-- vocab:FileFormat begin -->
**Possible Values** — *same 11-value `FileFormat` vocabulary as Field 18; snapshot 2026-07-29. Live `/api/models/FileFormat/rows/all/` is authoritative.*

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

This field shares Field 18's vocabulary, row mapping, sources, traps and payload behaviour; read
`fields/18-input-file-formats.md` for those. This file holds only what differs for output.

## Why it exists

A user choosing a tool often needs its products in a particular format — FITS for an image pipeline,
netCDF or CDF for an archive, CSV for a spreadsheet. The value tells them what files they will receive.
A format listed that the software never writes promises a product that does not exist; a real output
left off hides the tool from users who need exactly that product. The question is always **what a user
receives from the software**, not what it could be made to write.

## How it appears on the site

- **Detail page:** "Data & File Formats" section, "Output Formats" row; one plain (unlinked) tag per
  value, showing the row name.
- **Filter tab:** none.
- **Free-text search:** tier T4.6 (format name and extension).
- **Field search:** `output:"…"` matches `output_formats__name__icontains` or
  `output_formats__extension__icontains` (see Field 18 on the empty `extension` values).
- **JSON-LD:** each value is emitted under `keywords` as a `DefinedTerm` with `description`
  `outputFormats`, in the same term set as Field 18.

## Rubric: include / exclude

Settle this field separately from Field 18: input and output are different questions, and identical
lists are a sign both were copied from a tag list. Rules 1–7 decide whether a candidate format is
included; apply them top to bottom and stop at the first that fires. Map each included format with
Field 18's rule 7; rules 8–9 govern the incumbent value and an empty result.

1. **A commented-out or dead writer → exclude.** A `to_hdf(...)` that is commented out, or private
   code that no public function, CLI or shipped program reaches, produces nothing a user receives.
2. **A write that persists the software's inputs → exclude here.** Saving intermediate input frames
   for later use as input is evidence for Field 18, not an output product.
3. **Internal bookkeeping → exclude** (a cached file list written with `to_csv`, logs, state files). It
   is not a data product a user asks for.
4. **Transmitting a file is not authoring a format → exclude.** Uploading or copying user files of any
   format through the software does not make those formats outputs.
5. **An in-memory return value is not a file format → exclude**, when the API returns a generic
   container (a DataFrame, an `xarray.Dataset`, a dict, an array) and the save format is the caller's
   choice. **Exception — include** the format when the returned object carries that format's metadata,
   built or carried forward by the software, and the object's standard persistence writes that format
   (a returned sunpy map whose FITS header/WCS the software preserves → `FITS`).
6. **The software writes the format → include.** Evidence is a public writer function, a CLI output, or
   a program shipped and compiled with the install that writes a data file (even one the Python API does
   not expose), in the pinned code: `to_netcdf`, `writeto`, `json.dump` to a user-facing file,
   `to_csv` of results, a compiled tool writing an ASCII results file.
7. **Figures and movies** the software writes (`savefig` PNG/JPG, an MP4 `VideoWriter`) → include as
   `Other`, named in the note, since the vocabulary has no image or video rows. A format that has its own
   row (`JSON`) is recorded as that row, not folded into `Other`.
8. **Incumbent values are held to the same rules.** This field is enrich-only: an enrichment adds the
   outputs rule 6 or 7 admits that the record lacks. A full refresh also removes a stored output the
   rules exclude — an inference ("likely supported for results output"), a commented-out writer, or an
   `Other` that names nothing distinct from a listed row — with the reason recorded.
9. **Empty is legitimate** when the software writes no file a user receives (DataFrame in, DataFrame
   out). Record the write-path search and its positive control.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

Sources, the format-indicator grep and the shared traps are in Field 18. For output specifically:

- Search write paths across the installed package, examples and shipped programs:
  `git grep -n -P '\.(to_\w+|writeto|save\w*|dump)\s*\(|savefig|VideoWriter|open\([^)]*[\x27"]w' <pin> -- <package dir>`,
  then read each hit — the pattern matches bookkeeping and commented-out lines too. Pair a zero with a
  positive control on the same scope (a write the code does perform, or a read pattern that must match).
- Check whether each writer is live: a hit inside a comment, or in private code no public entry point
  reaches, is rule 1.
- For a compiled tool, check that the build compiles it on install (`cmake --build` over the whole
  project, `MANIFEST.in` shipping its source) even if nothing installs it to `PATH`.

## Payload and roundtrip notes

Key `outputFormats`; binding, PATCH and readback exactly as Field 18. Clear the field with `[]` or
`null` — it is a plain list field, not the dict-shaped `version`.

## Worked examples

- **Result writers commented out (SAVIC).** Every `to_hdf` call that would write results is commented
  out, the live calls write input frames (rule 2), and no CSV path exists anywhere in the tree. The API
  returns a DataFrame, so the stored `csv` and `HDF5` are both removed and the field is empty (rule 9);
  `HDF5` stays in Field 18.
- **Uploading is not writing (pyzenodo3).** The only file the package writes is a `.json` of deposit
  metadata → `JSON`. The stored `Other`, justified by the arbitrary files the tool uploads, is removed
  under rule 4, and it named nothing JSON does not already cover.
- **Figures, movies and JSON (PyAuroraX).** The package writes `savefig` images, MP4 movies and JSON
  import files and query templates, and no HDF5, CDF, IDL save or ASCII: `JSON` and `Other`, replacing a
  stored list that had simply copied the input formats.
- **A shipped program the API does not expose (WMM2020).** The Python API returns an `xarray.Dataset`
  and dicts (rule 5), but every install compiles `wmm20_file`, which writes an ASCII results file →
  `ascii` under rule 6, with the limits recorded beside it.
- **Metadata the software carries forward (sunkit-image).** No function writes a file, but the returned
  maps keep the input's FITS header and WCS and their standard save is FITS → `FITS` under rule 5's
  exception.

## Provenance

- Vocabulary block `vocab:FileFormat` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 501-523 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
