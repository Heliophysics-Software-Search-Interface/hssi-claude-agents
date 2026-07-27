# SPASE backfill audit — identifierless Field 31/32 entries in `repos/*/hssi_metadata.md`

**Audited:** 2026-07-27 · **Baseline:** live production `https://hssi.hsdcloud.org`
**Status:** audit only — **no metadata file was modified by this pass.**

## Why this exists

The agent instructions used to authorize free-typing a bare instrument/observatory name when nothing
in the vocabulary matched. That path is not inert: the backend
(`serializers/submission.py` `_get_or_create_observatory`, `data_parser.py`) falls through to
`InstrumentObservatory.objects.create(name=…, type=…)` — creating a **new row with a blank
identifier**, exactly the legacy row class hssi-website PR #54 deleted (63 → 0). The instructions
have now been corrected to a SPASE-only resolution ladder (see `resource_submission_form_fields.md`,
Field 31). This file records the pre-existing drift that policy leaves behind.

**20 canonical metadata files** carry Field 31/32 entries with `Identifier: Not found`. Nearly all
are April-2026 extractions predating the SPASE guidance (commit `0b0bac5`, 2026-07-07).

## Headline finding

**Production is already correct in every case. The drift is entirely local.** Every affected repo's
HSSI entry either already carries the right SPASE-backed rows or has been deliberately emptied. No
production PATCH is required by this audit — the remediation is a local file sync.

Note also that these files' Field 31/32 content is *already* out of step with production
independently of the identifier problem: several are missing observatory rows production carries
(`mcalf` → Dunn Solar Telescope, `xrtpy` → Hinode).

## Per-file findings

Legend for **Ladder rule**: 1 unique match · 2 evidence-backed multi-row expansion ·
4 instrument→observatory substitution · 5 documented omission.

| # | File | HSSI entry | Local (identifierless) | Production (authoritative) | Action | Rule |
|---|---|---|---|---|---|---|
| 1 | `ACE_magnetometer` | ACEmag | ACE Magnetometer (MAG) | instr **ACE Magnetic Field Instrument**; obs **Advanced Composition Explorer** | Adopt prod name + identifier. Local name is not canonical. | 1 |
| 2 | `GOESplot` | **GOESutils** | GOES-13 Imager; GOES-16 ABI | instr *(none)*; obs **GOES 13**, **GOES 16** | Drop both instruments, adopt the two observatories. | 4 |
| 3 | `LOFAR-Sun-tools` | lofarSun | LOFAR (Low Frequency Array) | *(none)* | Omit + document. Confirm no SPASE LOFAR row before finalizing. | 5 |
| 4 | `NEXRAD` | NEXRADutils | NEXRAD (Next-Generation Radar) | *(none)* | Omit + document: earth radar, out of heliophysics scope (PR #54 Table 4). | 5 |
| 5 | `POLAN` | POLAN | Ionosonde (general class) | *(none)* | Omit + document: generic class label, no single SPASE target. | 5 |
| 6 | `PyGS` | PyGS | 5 vague "…instruments" labels | instr *(none)*; obs **ACE, Ulysses, Wind, Parker Solar Probe, Solar Orbiter** | Replace the 5 instrument-suite labels with the 5 observatories. | 4 |
| 7 | `TomograPy` | TomograPy | SECCHI; SOHO | instr **STEREO-A SECCHI**, **STEREO-B SECCHI**; obs **SOHO**, **STEREO** | Adopt; SECCHI legitimately expands to two rows. | 2 |
| 8 | `VirES-Python-Client` | viresclient | Swarm VFM/ASM/EFI/ACC, Aeolus ALADIN, Swarm (7) | instr *(none)*; obs **Aeolus**, **Swarm** | Collapse the instrument-level payloads to the two observatories. | 4 |
| 9 | `aidapy` | AIDApy | MMS; Cluster; SDO/AIA | obs **Magnetospheric Multiscale** only | Adopt MMS. **Cluster and SDO/AIA need a decision** — both have canonical SPASE rows but production carries neither. | 1 + review |
| 10 | `astrometry_geomap` | AstrometryAzEl | Digital All Sky Cameras | *(none)* | Omit + document: generic class label (PR #54 Table 4). | 5 |
| 11 | `dascasi` | DASCutils | DASC (Digital All-Sky Camera) | instr **all-sky imager at Poker Flat…**; obs **Poker Flat aurora observatory** | Adopt both. | 1 |
| 12 | `digital-meridian-spectrometer` | Digital Meridian Spectrometer | Digital Meridian Spectrometer | obs **Poker Flat aurora observatory** | Replace instrument with the observatory (SPASE/HDRL guidance). | 4 |
| 13 | `gima-magnetometer` | GIMAmag | GIMA | obs **GIMA** | Move instrument → observatory. | 4 |
| 14 | `mcalf` | MCALF | IBIS | instr **IBIS**; obs **Dunn Solar Telescope (DST)** | Adopt identifier; **also add the DST observatory** the local file lacks. | 1 |
| 15 | `mgs-utils` | MGSutils | MGS Radio Science Subsystem | **Not in production.** Seed CSV: drop instrument, keep `SMWG/Observatory/MGS` | Apply the seed answer; re-check after the next prod import. | 4 |
| 16 | `ndcube` | ndcube | AIA, IRIS, XRT, SPICE, DKIST | *(none)* | Omit all five — these fail the **relevance gate** as framework demo name-drops, before any vocab question. Document. | 5 |
| 17 | `scanning-doppler-interferometer` | Scanning Doppler Interferometer | Scanning Doppler Interferometer | obs **Poker Flat aurora observatory** | Replace instrument with the observatory. | 4 |
| 18 | `sunraster` | sunraster | SPICE | instr **SPICE**; obs **Solar Orbiter** | Adopt both. | 1 |
| 19 | `themisasi` | THEMISasi | THEMIS All-Sky Imagers (ASI) | instr **24 THEMIS Ground `*/ASI` rows**; obs **THEMIS** | Expand the aggregate label to the 24 station rows + observatory. | 2 |
| 20 | `xrtpy` | XRTpy | X-Ray Telescope (XRT) | instr **X-Ray Telescope (XRT)**; obs **Hinode** | Adopt identifier; **also add the Hinode observatory**. | 1 |

## Two discrepancies worth a separate look

1. **Seed CSV vs production disagree.** The `hssi-website` seed CSV (clone at `94fd572`, 2026-07-13)
   shows `AIDApy` with *no* relations, while production carries **Magnetospheric Multiscale** —
   which is what PR #54 Table 1 intended. Conversely `MGSutils` exists in the seed but **not in
   production at all**. The seed and prod are not in sync in both directions. Worth reconciling
   before the next gated seed import, since that import is wipe-and-replace.
2. **`repos/mgs-utils/hssi_metadata.md` records `https://github.com/space-physics/mgs-radio`**,
   which does not resolve via HSSI's `repo_url` lookup. Either the local URL or the HSSI entry's
   `code_repository_url` is wrong.

## Files deliberately untouched

`repos/asilib/` and `repos/fiasco/` are untracked and in flight in other sessions; several other
`repos/*/hssi_metadata.md` carry foreign modifications. None were read into this audit's
recommendations or modified.

## Suggested next step

Remediation is a **local file sync**, one repo at a time, adopting the production values above —
not a production change. `asilib` should be excluded until its in-flight session lands.
