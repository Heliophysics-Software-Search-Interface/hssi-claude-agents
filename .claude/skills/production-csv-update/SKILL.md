---
name: production-csv-update
description: >
  Version-controlled workflow for changing HSSI **production** metadata through seed-CSV pull
  requests instead of direct production PATCHes. Documents the production architecture, the
  destructive wipe-and-replace DB import, and the full sync → edit-locally → PR → re-import
  "dance", with every hard-won gotcha. Use when a user wants production metadata changes
  captured in version control (the recommended path), or when the Updater needs to explain that
  alternative before a direct prod PATCH.
user-invocable: false
---

# Production Metadata Updates via CSV Pull Requests

This is the **version-controlled** way to change HSSI production metadata. It is slower than a
direct `PATCH` to the production API, but it keeps the change in git and prevents it from being
silently erased by a future database import.

## The core problem (why this exists)

HSSI production has **two separate sources of truth that are NOT auto-synced**:

1. The **live PostgreSQL database** — what the website serves and what the Update/Submission API writes to.
2. The **seed CSVs** committed in the `hssi-website` repo at `django/website/config/db/` — the
   version-controlled snapshot the DB is (re)built from.

A direct `PATCH`/`POST` to the production API changes **only the database**. The seed CSVs are not
touched, so GitHub drifts from production. The maintainer "Import HSSI Database" admin action is a
**full wipe-and-replace** that deletes every row and reloads from those CSVs — so the next import
**silently erases any DB-only change**. Conversely, anything in the live DB that never made it back
into the CSVs (new submissions, vocabulary fetches) is lost on import too.

**Therefore: keep the CSVs equal to the DB, and drive every production change through a CSV PR.**

---

## ⚠️ Before you rely on this skill: sanity-check `hssi-website`

This skill hard-codes facts about the `hssi-website` codebase and the production deployment that are
accurate **as of 2026-06** but may drift. **Before trusting the mechanics below, confirm the current
source still matches**, and if anything has moved, adapt the workflow and tell the user. Check:

- **Import is still wipe-and-replace, export is still read-only** — `django/website/admin/actions.py`
  `view_import_db_new` calls `remove_all_model_entries()` **then** `import_db_csv()`; `view_export_db_new`
  calls only `export_db_csv()`. The implementations live in `django/website/admin/csv_export.py`
  (`remove_all_model_entries` does `model.objects.all().delete()` for every model; `export_db_csv` only
  reads and writes files).
- **Admin endpoints & seed-CSV dir** — `/admin/export_db_new/` and `/admin/import_db_new/` (superuser POST);
  CSVs in `django/website/config/db/`.
- **Container layout** — `docker-compose.yml`: service/container `HSSI` (Django app) with the bind mount
  `./django:/django`, and `website_db` (Postgres) on a persistent named volume. The mount means container
  path `/django/website/config/db/` == host `~/hssi/django/website/config/db/`.
- **Person matching** — `django/website/models/serializers/submission.py` `_get_or_create_person`
  (matches by `identifier` first, else by exact name; only fills blank names).

The existing **`update-api-spec`** skill is the precedent/mechanism for re-syncing reference material from
`hssi-website` source when it has drifted — use it if the API or these internals have changed materially.

---

## Operating model (how you, the agent, work here)

- **You do not SSH into production and you do not hold production credentials.** The user drives the
  prod SSH session. You provide exact, copy-pasteable commands and interpret the output they paste back.
- **Read-only first.** Every diagnostic step (git state, exports, diffs) is read-only on the DB. Only two
  steps mutate state: the **local** re-seed (Phase 2) and the **production import** (Phase 3). Both are
  destructive and **require explicit user approval** immediately before running.
- **Production work is human-driven and gated.** Treat the prod import like a deployment: pre-flight check,
  backup, approve, execute, verify.

---

## Production architecture (as of 2026-06)

- **Host:** AWS EC2, Ubuntu. The user connects with `ssh -i <key>.pem ubuntu@<ec2-host>`.
- **Repo:** a clone of `hssi-website` at `~/hssi` (on the prod host). It legitimately carries a couple of
  **uncommitted, production-only config edits** (e.g. `config/nginx/django.conf`, `django/hssi/settings.py`) —
  leave those alone; they are not part of any PR.
- **Docker:** the host uses **legacy Compose v1**, so the command is **`docker-compose`** (hyphen), not
  `docker compose`. Containers: `HSSI` (app) and `website_db` (Postgres, persistent volume — survives
  redeploys). `git pull` / redeploy do **not** import the CSVs; the DB persists untouched.
- **Disk is tight** (~1.2 GB free) — keep DB dumps small and gzipped.
- **Prod URL:** `https://hssi.hsdcloud.org`.

## Seed CSVs & data model

~27 CSVs in `django/website/config/db/`:

- `software.csv` — one row per software. Many M2M fields are stored **inline as comma-joined UUID lists**
  in columns (keywords, related_software, interoperable_software, funder, award, programming_language,
  data_sources, input/output formats, operating_system, cpu_architecture, related_region, related_publications,
  related_datasets, related_instruments, related_observatories). FK columns: publisher, version, license.
- **Entity tables** — `person.csv`, `organization.csv`, `keyword.csv`, `related_item.csv`, `award.csv`,
  `software_version.csv`, plus controlled vocabularies (`function_category.csv`, `region.csv`, `phenomena.csv`,
  `instrument_observatory.csv`, `cpu_architecture.csv`, `file_format.csv`, `operating_system.csv`,
  `programming_language.csv`, `data_input.csv`, `license.csv`, `repo_status.csv`).
- **Through tables** — `software_authors.csv`, `software_software_functionality.csv`,
  `software_related_region.csv`, `software_related_phenomena.csv`. These have an **integer PK + `sort_value`**.
  The import **excludes** authors / software_functionality / related_region / related_phenomena from the
  `software.csv` import and loads them from these through-table CSVs instead.

## Import vs. export — the two admin actions

- **Export** (`export_db_csv()`) — **read-only on the DB**; reads every model and overwrites the CSV files.
  Byte-deterministic. Trigger via the admin button `POST /admin/export_db_new/` (superuser) **or** the Django
  shell:
  ```bash
  docker exec HSSI sh -lc 'cd /django && python manage.py shell -c "from website.admin.csv_export import export_db_csv; export_db_csv()"'
  ```
- **Import** (`remove_all_model_entries()` then `import_db_csv()`) — **DESTRUCTIVE full wipe-and-replace**:
  deletes every row in every HSSI model, then loads from the CSVs. Trigger via the admin button
  "Import HSSI Database (new)" `POST /admin/import_db_new/` (superuser) **or** the shell:
  ```bash
  docker exec HSSI sh -lc 'cd /django && python manage.py shell -c "from website.admin.csv_export import remove_all_model_entries, import_db_csv; remove_all_model_entries(); import_db_csv()"'
  ```
  (If `python` is missing in the container, try `python3`.)

---

## The dance — three phases

> Phase 1 makes GitHub `main` equal production. Phase 2 makes the metadata change locally and ships it as a
> reviewable PR. Phase 3 imports the merged CSVs into production. Each phase is its own PR / discrete step.

### Phase 1 — Sync GitHub's CSVs to the live production DB (own PR)

GitHub's committed CSVs are frequently **stale** relative to the live DB (maintainers submit/edit directly in
prod, run `fetch_vocab`, etc.). **Never open a CSV-change PR until `main` reflects current production**, or the
eventual import will clobber that prod-only data.

1. SSH to prod; confirm `git` state (`git rev-parse HEAD`, `git status`); note the prod-only config edits.
2. **Export the live DB** (read-only) into the working tree, then pull a copy to local for inspection (tar +
   `scp`). Restore the prod working tree afterward (`git checkout -- django/website/config/db/`).
3. Locally, create a `sync-prod-db-snapshot` branch off `main`, drop in the exported CSVs **normalized to LF**
   (`tr -d '\r'`), review the diff (expect: new software, new people/orgs/keywords, vocabulary refresh), commit,
   push, open a PR, and merge it. Now `main` == production.
4. **Verify** the merge equals a clean export of prod: fetch on prod, re-export, and compare CRLF-normalized,
   sorted, against `origin/main` per file — every file should match (byte and semantic).

### Phase 2 — Make the metadata change locally and PR it (own PR)

1. `git pull` local `main` (now the prod snapshot).
2. **Re-seed a LOCAL HSSI DB from the snapshot CSVs** (wipe + import on localhost) so local == prod, including
   the production vocabulary UUIDs. (Back up the current local DB first if it holds unsaved work.)
3. Apply the metadata changes via the **Updater's normal PATCH flow against `http://localhost`** (PREPARE →
   approval → EXECUTE). Because payloads reference vocab by **name/URL**, they re-resolve correctly against the
   prod vocabulary UUIDs.
4. **Export** the local DB and **reconcile to a minimal, correct diff** (see Diff reconciliation below).
5. **Verify** before committing: referential integrity holds; **only the intended software rows changed** (no
   "foreign" software touched); new entity rows are additive; and **no author/identifier was lost** vs. the
   curated `hssi_metadata.md` (compare authors **by ORCID/identifier**, not name spelling).
6. Commit on a feature branch, open a PR with a **human-readable description** (the CSV diff is not
   line-readable — describe the per-package changes in prose), and merge.

### Phase 3 — Apply the merged CSVs to production

All on the prod host, user-driven. Provide these as a runbook with explicit STOP gates.

1. **Confirm prod is at the pre-import commit** and the CSV dir is clean.
2. **Pre-flight drift check (read-only):** export the live DB and compare CRLF-normalized against the snapshot
   baseline. **If it reports drift, STOP** — new data entered prod since the snapshot; fold it in (a fresh
   Phase 1) before importing.
   ```bash
   cd ~/hssi
   docker exec HSSI sh -lc 'cd /django && python manage.py shell -c "from website.admin.csv_export import export_db_csv; export_db_csv()"'
   drift=0
   for f in django/website/config/db/*.csv; do
     diff <(git show "HEAD:$f" | tr -d '\r' | sort) <(tr -d '\r' < "$f" | sort) >/dev/null 2>&1 || { echo "DRIFT: $(basename "$f")"; drift=1; }
   done
   git checkout -- django/website/config/db/
   [ $drift -eq 0 ] && echo "PRE-FLIGHT: SAFE" || echo "PRE-FLIGHT: DRIFT — STOP"
   ```
   (Compare against the **snapshot commit** the enrichments were built on. If `HEAD` already includes the
   enrichment PR, compare against the snapshot commit instead so your own changes don't read as "drift".)
3. **Back up the DB** (small, gzipped):
   ```bash
   docker exec website_db pg_dumpall -U postgres | gzip > ~/hssi_prod_db_backup_$(date +%Y%m%d_%H%M).sql.gz
   ```
4. **Pull the merged main:** `git pull --ff-only origin main` (the prod-only config edits are untouched
   because no PR changes them).
5. **Import — DESTRUCTIVE wipe-and-replace** (get explicit user approval immediately before):
   ```bash
   docker exec HSSI sh -lc 'cd /django && python manage.py shell -c "from website.admin.csv_export import remove_all_model_entries, import_db_csv; remove_all_model_entries(); import_db_csv()"'
   ```
   Wait for `Finished Importing DB!`. (Equivalent to the admin "Import HSSI Database (new)" button.)
6. **Verify:** software count matches local; spot-check key records via `GET /api/view/software/<uid>/`; eyeball
   the live site. Recovery, if needed: restore the `pg_dumpall` backup or re-import the snapshot.
7. **(Optional) redeploy** for code/template changes that came along on `main`. Template-only changes need just
   `docker-compose restart hssi` (templates are cached; the bind mount already exposes the new files). Frontend
   asset changes need a rebuild (`npm install && npm run build && docker-compose up -d --build`). The **data
   import above needs no redeploy** — it writes the DB the running app reads live.

---

## Gotchas / hard-won lessons

- **CRLF vs. LF.** The export writes CSVs with **CRLF** line endings; git stores **LF**. A raw `git diff` after
  an export is therefore all line-ending noise. **Always `tr -d '\r'`** before diffing or committing exported
  CSVs, and normalize to LF when committing.
- **Prod ↔ GitHub drift is real and dangerous.** Do Phase 1 first, every time. A wipe-and-replace import of
  stale CSVs deletes real production submissions and vocabulary.
- **The serializer can't attach an ORCID to a name-matched person.** `_get_or_create_person` matches by
  `identifier` (ORCID/URL) first, else by exact given+family name, and **only fills blank names**. So replaying
  an author payload against a prod-seeded DB can **silently drop the ORCIDs your payload intended** when prod
  already has a name-only person record (its record wins). Catch this by comparing the result **by identifier**
  against the curated `hssi_metadata.md`, and **restore lost identifiers by editing `person.csv` directly**
  (the API cannot). Affiliations are added with `.add()` and **accumulate** (can create duplicates). Some
  curated enrichments may not exist as payload files at all — diff against the curated source to catch losses.
- **Diff reconciliation.** After re-seed → edit → export, the raw diff carries noise that must be stripped so
  the PR shows only intended changes:
  - Pure **row reordering** in unrelated tables (e.g. `instrument_observatory`) — revert to `main`.
  - `submission_info.date_modified` **auto-now churn** — revert (timestamps only).
  - **Integer-PK renumbering** in through tables — `.set()` deletes+recreates rows, so re-key to reuse `main`'s
    PKs for unchanged `(software, target)` pairs (preserve `sort_value`), appending only genuinely new rows.
  - **Entity-table reordering** — re-emit in `main` order, appending new rows.
  - **Accidental duplicate orgs** — e.g. a publisher given a ROR id when prod's record uses a different URL
    creates a second "Zenodo"; repoint the reference to the existing org and drop the dup.
  Then verify: exactly the intended software rows changed, 0 dangling references, no duplicate entities.
- **Import resets `date_modified`.** The wipe-and-reimport sets `date_modified` (auto-now) on **every** row to
  the import time; `date_created` / submission dates are preserved. Cosmetic but global — mention it.
- **Vocabulary UUID churn.** `fetch_vocab` re-mints controlled-vocab UUIDs in prod, which cascades into the
  software M2M reference columns. Mirror prod's vocab (Phase 1 captures it); because PATCH payloads reference
  vocab by name/URL, they re-resolve correctly after a re-seed.
- **Local PATCH token.** The `HSSI_UPDATE_TOKEN` in `hssi-website/.env` may be **quoted**; reading it naïvely
  keeps the quotes and the API returns 403. Pull it from the container instead:
  `docker exec HSSI printenv HSSI_UPDATE_TOKEN`.

## Quick command reference

| Action | Command |
|---|---|
| Export DB → CSVs (read-only) | `docker exec HSSI sh -lc 'cd /django && python manage.py shell -c "from website.admin.csv_export import export_db_csv; export_db_csv()"'` |
| Import CSVs → DB (DESTRUCTIVE) | `docker exec HSSI sh -lc 'cd /django && python manage.py shell -c "from website.admin.csv_export import remove_all_model_entries, import_db_csv; remove_all_model_entries(); import_db_csv()"'` |
| CRLF-safe drift check | `for f in django/website/config/db/*.csv; do diff <(git show "HEAD:$f" | tr -d '\r' | sort) <(tr -d '\r' < "$f" | sort) >/dev/null 2>&1 || echo "DRIFT: $f"; done` |
| Backup prod DB | `docker exec website_db pg_dumpall -U postgres | gzip > ~/hssi_prod_db_backup_$(date +%Y%m%d_%H%M).sql.gz` |
| Local PATCH token | `docker exec HSSI printenv HSSI_UPDATE_TOKEN` |
| Restart app (template changes) | `docker-compose restart hssi` |
