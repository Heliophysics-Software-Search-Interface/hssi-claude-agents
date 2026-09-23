# Field 17 — Data Sources

**Level:** OPTIONAL · **API:** `dataSources[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/DataInput/rows/all/`
**Filter tab:** Data Sources · **Free-text search tier:** T3 · **Field-search code:** `source`

## What it is

**Type:** Multi-select dropdown

**What it is:** The data input source the software supports.

**How to fill it:** Select all data input sources the software supports. If a source is not listed, select 'Other'. If the data input source is observatory specific, select the `Observatory/Mission-specific` row (the form's wording calls it 'observatory-specific') and indicate the observatory, mission, or group of instruments in the Related Observatory field. *(The live form currently shows the short field description in this tooltip's place — a website wiring slip points the tooltip at the wrong constant; the guidance above is the intended text.)*

<!-- vocab:DataInput begin -->
**Possible Values** — *17 values, snapshot 2026-08-06. Live `/api/models/DataInput/rows/all/` is authoritative. **Row counts differ by target**: `http://localhost` has these 17; `https://hssi.hsdcloud.org` still carries the junk row described below.*

- AMDA
- CDAWeb
- das2
- FTP/FTPS Directories
- GFZ
- HAPI
- HTTP/HTTPS Directories
- Madrigal
- Observatory/Mission-specific
- OMNIWeb
- Other
- S3/Cloud-aware
- SSCWeb
- TAP
- The Virtual Solar Observatory.
- VirES
- WDC
<!-- vocab:DataInput end -->

**Traps in this list:**

- **`The Virtual Solar Observatory.` ends with a period.** The stored row name includes a trailing
  full stop; `The Virtual Solar Observatory` (without it) does **not** match and will be rejected.
  The row is otherwise genuine — it carries the canonical `…/DataSources#VSO` identifier.
- **`Other - https://xrt.cfa.harvard.edu/level1/` — never emit this.** A free-text "Other" value that
  leaked into the controlled vocabulary; it carries no identifier and was selectable in the live
  submission form. As of the snapshot above it is absent from `http://localhost` but still present on
  `https://hssi.hsdcloud.org`. If you meet it on any stored record, treat it as **drift to correct**,
  not a value to preserve.
- **`AMDA`, `GFZ`, `Madrigal`, and `WDC` have empty `identifier` fields**, unlike every other row.
  They appear to be legitimate later additions rather than artifacts, and are safe to select.
- The rows carry no definitions; the rubric below is the working meaning of each.

## Why it exists

A user who already knows where their data live — CDAWeb, Madrigal, a HAPI server, one mission's
archive — uses this field to find software that can read from there. A correct value is a promise that
the software, as distributed, reaches that source. A padded value (a source reached only through a
separately distributed plug-in, a source planned for a future release, HTTP listed because the package
downloads its own model files) sends that user to a tool that cannot deliver; a missing source hides the
software from exactly the people it serves.

## How it appears on the site

- **Detail page:** in the "Data & File Formats" section, as "Data Sources" — one tag per stored row,
  showing the row `name` and linking to the homepage filtered by that source.
- **Filter:** the sidebar **Data Source** tab lists the rows as flat, independent items; filtering matches
  the exact row.
- **Free-text search:** tier T3 (`data_sources__name`).
- **Field search:** `source:"…"` matches `data_sources__name__icontains`.
- **JSON-LD:** each row is emitted in `keywords` as a `DefinedTerm` with description `dataSources` and the
  HSSI-vocab `DataSources.json` term set.

## Rubric: include / exclude

Apply per candidate row, top to bottom; stop at the first rule that fires, except that rule 10's
plug-in-framework case is tested before rule 4 excludes a source reached only through another package.
The vocabulary is small enough
to walk whole: give every row a verdict on each extraction and refresh.

1. **Only live rows, byte-exact.** A value must be a row of the live `/api/models/DataInput/rows/all/`
   vocabulary, including the trailing period of `The Virtual Solar Observatory.`. The junk
   `Other - https://xrt…` row is never emitted; on a stored record it is removed and replaced by whatever
   rules 2–11 support. Fires on: a candidate not in the live list, or the junk row.

2. **The source must be read by the pinned code.** Select the archive, service, or protocol the software
   actually reads data from: a client, a query interface, or a download routine a user calls, present in
   the pinned tree. Fires on: no code path in the distribution reaches the source — exclude it.

3. **A prospective or future source is excluded.** A paper's or roadmap's "future work will retrieve from
   SPDF" is not a capability. Fires on: the only evidence is a statement of intent.

4. **The capability standard: what the distribution alone reaches.** A framework does not claim the
   archives its separately distributed plug-ins or extensions reach; those belong to the plug-ins' own
   records. Nor does a wrapper claim the retrieval routines of the library it runs. Fires on: the source is
   reached only after installing another package.

5. **Downloading its own assets is not a data source.** Fetching the package's trained models, tutorial
   files, or reference tables from its own repository is not reading science data from an HTTP directory.
   Fires on: the only fetched content is the package's own bundled material.

6. **A named service over HTTP is that service, not a directory.** When HTTP is only the transport to a
   named service API (Madrigal CGI services, HEK), select the service's row if it has one, never
   `HTTP/HTTPS Directories`. A document that merely cites a project (a code of conduct adapted from the
   HAPI project) is not a client for it. Fires on: every remote call goes to a named service's endpoints.

7. **A generic multi-mission archive, service, or access protocol goes here, not in Fields 31/32.** `CDAWeb`, `HAPI`,
   `The Virtual Solar Observatory.`, `SSCWeb`, `OMNIWeb`, `AMDA`, `das2`, `Madrigal`, `GFZ`, `WDC`,
   `VirES`, `TAP`, `S3/Cloud-aware`: select the row the software's client reaches. These are data services,
   not instruments or observatories. Fires on: code that queries or downloads through that service or protocol.

8. **An instrument- or mission-specific source selects `Observatory/Mission-specific` here and goes to
   Fields 31/32.** When the software reads a particular mission's or observatory's data products or
   archive, select `Observatory/Mission-specific` and name the instrument or observatory in Fields 31/32
   (subject to their SPASE-only rule; a 31/32 left empty because no SPASE row exists does not undo this
   value). Not when the software is instrument- and mission-agnostic, and not when the mission link is only
   the provenance of training data or of the pixels a user supplies. Fires on: code that reads that
   mission's products or fetches from its archive.

9. **`HTTP/HTTPS Directories` / `FTP/FTPS Directories`** are selected when the software fetches data files
   from a plain directory tree over that protocol and the host is not a single mission's archive already
   carried by rule 8 (index files from GFZ and WDC Kyoto directories qualify; a mission archive's
   directory does not add the transport row). Fires on: code that builds paths under a directory URL and
   downloads the files.

10. **`Other` only for a real source with no row.** Name the source in the dossier. A framework whose
    retrieval machinery is its own but whose endpoints are supplied by plug-ins has a real, user-facing
    source no row names, and takes `Other`. Remove `Other` once every source it stood for has its own row.
    Fires on: a real source, evidenced under rule 2, with no matching row.

11. **Data the user hands the software is not a source.** Software that takes arrays or local files the
    user already has, and reaches nothing itself, is evidenced-empty — not `Other` and not
    `Observatory/Mission-specific`. Fires on: no network, archive, or directory access anywhere in the
    distribution.

12. **Incumbents.** On a refresh give every stored row its own verdict under rules 1–11: keep a row the
    evidence supports, add every row that now passes, remove one that fails. A stored value a fair reading
    of the code supports is kept — removal needs evidence that it is false, not that it is arguably
    imprecise. Enrichment adds to the stored set and never drops from it.

13. **Empty is legitimate.** An evidenced-empty field (the sweep for network, archive and directory access
    recorded) is correct for software that reaches no source.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

**Sources, in priority order:**
1. The code's network and archive access: HTTP/FTP clients (`urllib`, `requests`, `ftplib`), archive
   clients (`hapiclient`, `sunpy.net.Fido`, `cdasws`, Madrigal and VirES clients), constructed URLs,
   download functions, and what they are called from.
2. The public API and documentation of retrieval functions.
3. The reference publication — for what the released software does, never for planned work (rule 3).

**Verification steps:**
- Sweep the pinned tree for network access (`git grep -P -i 'urlopen|urlretrieve|requests\.|ftplib|https?://' <pin>`)
  and read every hit: licence URLs, docstring links and README pointers for humans are not access.
- For each selected row, cite the function and the endpoint it reaches; for each rejected near-miss
  (especially `HTTP/HTTPS Directories`, `Other`, `Observatory/Mission-specific`), record why.
- Values must be rows of the live vocabulary. Watch the byte-level trap: `The Virtual Solar Observatory.`
  carries a trailing period.
- Row sets differ by target (the junk row is on production only); fetch the list from the target you will
  write to.

**Traps:**
- **Field 4 versus Field 17.** A framework can carry `Data Processing and Analysis: Data Access and
  Retrieval` (its retrieval machinery is its own) while Field 17 excludes the archives its plug-ins reach
  (the endpoints are not). The two fields answer different questions.
- **Mentions are not access.** A template comment about CDAWeb labelling conventions, a changelog line
  saying CDAWeb methods moved to another package, a docs page about a sibling package's Madrigal reader.
- **HEK has no row.** A package that queries HEK for one mission's events is carried by
  `Observatory/Mission-specific`; `Other` would tell a searcher nothing more.
- **Madrigal is a federation of observatory servers.** A client pointed at one observatory's Madrigal
  site can fairly carry `Observatory/Mission-specific` beside `Madrigal`.

## Payload and roundtrip notes

- **Key:** `dataSources` — an array of exact row names.
- **Binding:** `_get_controlled_item` matches `name__iexact` and takes the first row; case is ignored but
  every other byte (the trailing period) must match. An unknown value raises `Unknown value '<value>'` and
  rejects the whole atomic request.
- **Not order-sensitive.** `data_sources` is a plain many-to-many field; order is not stored.
- **PATCH replaces the whole list.** Enrichment is identity-aware set-union (send existing ∪ new); an
  approved removal sends the complete final list. `[]` or `null` clears the field; an omitted key is
  unchanged.
- **`/api/data/` returns row UUIDs**, not names; resolve them before comparing against a baseline.

## Worked examples

- **Balloon-borne imaging system (SkyWinder).** It ingests its own camera and lidar data, and its paper says
  it can use lidar and imaging data hosted by Madrigal: `Observatory/Mission-specific` and `Madrigal` are
  selected. The paper's retrieval from NASA SPDF is described as future work and the pinned tree has no such
  client, so `CDAWeb` is excluded (rule 3).
- **Instrument framework with plug-ins (pysat).** Stored `CDAWeb`, `Madrigal`, `HTTP/HTTPS Directories`
  and `Observatory/Mission-specific` are reached only through separately distributed plug-ins and are
  removed (rule 4); the core's own download machinery, whose endpoints the plug-ins supply, keeps `Other`
  (rule 10).
- **Flow-tracking wrapper (pyflct).** It takes two arrays or local files and has no network code. The stored
  `Observatory/Mission-specific` is removed and the field is evidenced-empty (rule 11).
- **Geophysical-index model interface (pyglow).** It downloads Kp/Ap/F10.7 from GFZ and Dst/AE from WDC
  Kyoto directories: `GFZ`, `WDC`, and `HTTP/HTTPS Directories` are selected (rules 7, 9), and the stored
  `Other` is removed because every source it stood for now has a row (rule 10).
- **Solar instrument toolkit (sunkit-instruments).** Every fetch goes to one mission's archive (GOES events
  from HEK, Fermi pointing files, PROBA2/LYRA annotations): `Observatory/Mission-specific` stands, and
  `HTTP/HTTPS Directories` is not added for those mission directories (rule 9).

## Provenance

- Vocabulary block `vocab:DataInput` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 436-477 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
