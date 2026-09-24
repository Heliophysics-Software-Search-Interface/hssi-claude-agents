# Field 28 — Related Datasets

**Level:** OPTIONAL · **API:** `relatedDatasets[]` · **Change class:** enrich-only
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.4 (name) · **Field-search code:** `dataset`

## What it is

**Type:** Multi-entry URL (RelatedItem lookup — DOI URL preferred)

**What it is:** Datasets the software supports functionality for (e.g., analysis).

**How to fill it:** Enter the URLs — ideally DOIs — for all datasets related to the software, one URL per entry. Only a URL is accepted per entry; free-text citations are rejected. For a dataset with no DOI, use its permanent landing page (e.g., an hpde.io page such as `https://hpde.io/NASA/NumericalData/MMS/4/HotPlasmaCompositionAnalyzer/Burst/Level2/Ion/PT0.625S.html`).

In practice: the datasets the software is **built to read** (or ships and evaluates), and the datasets
it **produced**, each by DOI or permanent landing page.

## Why it exists

It links the software to the data it works with, so a visitor who knows a dataset can find the tool
that reads it, and a visitor on the software's page learns exactly which data products it supports.
An input dataset the software cannot actually read (the wrong processing level, a derived movie, a
revised release it does not ship) sends a user to data the tool will not open.

## How it appears on the site

- **Detail page:** a "Related Datasets" subsection of the "Related Items" section, one link per entry.
  Link text is the related item's name, or the raw URL when the name is `UNKNOWN`; items created
  through the API store the URL as their name, so the link text is normally the URL.
- **JSON-LD:** each entry is a `mentions` item typed by the related item's stored type (`Dataset` for
  a dataset row).
- **Search:** free-text tier T4.4 on the name; `dataset:"…"` matches it by substring. Because the name
  is the URL, searches match the DOI or URL string, not the dataset's title.
- **Not displayed:** the dataset's title — record it in the dossier prose.

## Rubric: include / exclude

Apply to each candidate and to each incumbent entry. Rule 1 screens everything. Then assess the
candidate under the rule for its relationship to the software — rules 2–3 for data the software reads,
rule 4 for data it ships, rule 5 for data it produced — and stop at the first that fires within that
relationship; rule 2 never excludes a produced or shipped dataset. Rule 6 then selects within a versioned
series admitted under rule 3 or 5; it never overrides rule 4's exact shipped release.

1. **Not a dataset → not Field 28.** Fires for a publication (Field 14 or 27), software (Field 29 or
   30), a documentation page, or a tool's web interface.
2. **Input data the software cannot read → not Field 28.** Fires for a candidate **input** product in a
   level, format or release the software does not handle, even from the same instrument: an unsupported processing
   level, a derived product (movies, spreadsheets) made from data it reads, a revised release it does
   not ship, or a sibling instrument's data with no reader in the code.
3. **A dataset the software is built to read → include.** Evidence: a dedicated reader or loader in
   the code, a documented input, or test fixtures that are real files of that dataset. Include every
   dataset that passes; do not pick a subset for brevity.
4. **A dataset the software ships and evaluates → include the exact release it ships.** Fires for
   coefficient files, model tables or reference data carried in the repository. Confirm the release
   from the file's own header, not from its name.
5. **A dataset the software produced → include.** Fires for a data release made with the software, or
   the supplementary data of the software's own performance paper. A dataset attached to a later
   science analysis that merely used the software does not qualify.
6. **A versioned data series with no series-level identifier → the newest release.** Fires when the
   data are published as independent release DOIs with no concept or series DOI linking them. Record
   the newest, not every release; a refresh moves it forward when a newer release appears.
7. **Incumbent entry → keep** when rule 3, 4 or 5 still holds; remove it when rule 1 or 2 fires or it
   no longer resolves. Within a rule-6 series only the selected newest release is kept: an incumbent that
   is an older release of that same series is replaced by the newest, not kept beside it. Rule 4's exact
   shipped release is never replaced by a newer release the software does not ship.
8. **No identifier and no permanent landing page → empty, with the search recorded.** The field needs
   a URL; never invent one.

**Form of each entry.** The dataset's DOI as `https://doi.org/<doi>`; with no DOI, its permanent
landing page (an hpde.io SPASE page, a data center's dataset page), or the public HTTPS archive root
that the software's own code reads from (an `ftp://` link does not open in current browsers). Never a
single data file or a query URL.

## Ask the user only when

Nothing — the rubric decides every known case. A case no rule covers is a rubric gap: ask, and report
it as one.

## Where to find it, and traps

**Sources, in priority order.**
1. The code: reader and loader modules, download URLs and archive roots, test fixtures, bundled data
   files and their headers.
2. The docs: data-access pages, rules-of-the-road statements that name dataset DOIs.
3. DataCite: `https://api.datacite.org/dois?query=<term>` with `resource-type-id=dataset`, or a
   `url:"<data host>"` query to find every DOI registered for the archive the code reads from;
   DataCite `client-id=` is a parameter, not a query term.
4. SPASE records (`https://hpde.io/…`) for a permanent landing page, and the instrument and
   observatory records resolved for Fields 31 and 32.
5. The Data Availability statements of the software's own papers, where produced datasets surface.

**Verification.**
- DOIs must be full URLs: `https://doi.org/10.XXXX/XXXXX` (Fields 2, 12, 14, 27, 28, 29, 30).
- Resolve each DOI and read its DataCite `types.resourceTypeGeneral` (`Dataset`), title and
  `relatedIdentifiers`; a release DOI with an empty `relatedIdentifiers` list is not part of a linked
  series.
- Map each dataset to the reader that handles it and record the mapping in the dossier.

**Traps.**
- **"No DOIs registered" is a claim to test.** An archive whose landing pages carry no DOI badge may
  still have every dataset registered at DataCite; query by the data host's URL before concluding.
- **Same instrument, different product.** Level 1 versus Level 2, raw images versus compiled movies,
  an original coefficient release versus its revision — check which one the code opens.
- **Fields 17 and 24** already carry a data platform's home page or documentation; this field is for
  the datasets themselves.

## Payload and roundtrip notes

**RelatedItem URL fields (27–30):** each entry must be a real URL. Free text fails the serializer's
`URLValidator` (`Invalid URL: '<value>'`) and rejects the whole atomic request. Keep each URL ≤128
characters: `_get_or_create_related` stores the URL as both `identifier` and the 128-capped `name`, so
a longer URL passes validation and then fails at the database write.

- Key `relatedDatasets`, an array of URL strings. The array **replaces** the whole list; `[]` or
  `null` clears it; an omitted key leaves it unchanged.
- Each URL binds an existing related item on the exact identifier, else creates one typed Dataset.
  **A related item keeps its type on reuse:** a URL first created as a publication or software stays
  typed that way (including in JSON-LD) when listed here; moving a URL between Fields 14, 27, 28, 29
  and 30 does not retype it.
- Related item names are placeholders — the URL itself, or `UNKNOWN`, in which case the page shows the
  identifier as link text. Compare on `identifier`, never on name.
- Field 28 is enrich-only: a routine refresh does not re-derive it.

## Worked examples

- **Six readers, six DOIs.** PyAuroraX has dedicated readers for six University of Calgary all-sky
  imager datasets, each registered with a DOI. Rule 3 records all six; three other datasets from the
  same host (riometers and GNSS) have no reader and rule 2 excludes them.
- **Newest release of an unlinked series.** sunraster reads Solar Orbiter SPICE Level 2 FITS files,
  published as five release DOIs with no series DOI. Rule 6 records release 5.0 and notes that a later
  refresh should move it forward.
- **The exact coefficients shipped.** WMM2015 ships the original World Magnetic Model 2015 coefficient
  file; its first line identifies the December 2014 release. Rule 4 records that release's DOI and, because it
  fixes the exact shipped release, the revised "version 2" DOI the software does not ship is not recorded.
- **Derived product rejected.** DASCutils reads raw all-sky FITS images; the closest deposit holds MP4
  movies compiled from those images. Rule 2 fires; the raw archive is an FTP tree with no DOI or
  landing page, so the field stays empty (rule 8).

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 663-671 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
