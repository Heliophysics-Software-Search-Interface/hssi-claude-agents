# Field 1 — Submitter

**Level:** MANDATORY · **API:** `submitter[]` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** not searched · **Field-search code:** none

## What it is

**Type:** Nested group with text and email fields

**What it is:** The name and email address of the person submitting the metadata.

**How to fill it:**
- **Submitter Name:** Given name, initials, and last/surname (e.g., Jack L. Doe)
- **Submitter Email:** Work email address (can add multiple)

## Why it exists

The submitter is the person accountable for a record and the one HSSI contacts about it: the submission
confirmation and every later edit link go to the submitter's email. It describes the act of submitting,
not the software, so it carries no claim of authorship or maintenance. A wrong address locks the real
submitter out of editing the entry and gives someone else that access; an inferred one (the author's, a
maintainer's) makes HSSI mail a person who never submitted anything.

## How it appears on the site

- **Detail page:** not displayed. Submitter rows are curator-access and are not in the public record or
  its JSON-LD.
- **Edit-link flow:** when someone requests an edit link for an entry, the site shows the entry's
  submitter addresses masked (first and last character of the local part, whole domain) and emails the
  link only to an address that case-insensitively matches one of them.
- **Search, filter tabs, field search:** none.

## Rubric: include / exclude

Apply top to bottom; **stop at the first rule that fires**.

1. **Update (PATCH) → never include Field 1.** Submitter is out of scope for an update diff, baseline, or
   PATCH; the update endpoint rejects `submitter` with 400.
2. **A candidate inferred from the software → never the value.** An author, maintainer, committer,
   registry contact or an address found in the source is not the submitter. Such an address may be noted as
   context in the dossier's prose, never as this field's value.
3. **A test or example address (`example.org`, a probe mailbox) → never.** Every POST creates a permanent
   record and emails the submitter.
4. **The user has supplied the submitter's name and work email → record them exactly.** The address decides
   which Submitter row, and so which edit-link rights, the entry joins.
5. **A submission is being prepared and no submitter has been supplied → ask.** A placeholder never reaches
   a POST; collect the name and email before PREPARE.
6. **Otherwise → the placeholder** `[To be filled by actual submitter]` for both Submitter Name and Submitter
   Email. In a dossier this is the settled state of the field, not a gap: HSSI does not publish an existing
   record's submitter, and no repository, DOI record or registry identifies who submitted it, so a refresh
   leaves the placeholder alone rather than guessing.

## Ask the user only when

- **A submission is being prepared and the submitter's name and work email have not been given** in this
  session. Ask for both; never infer them.

## Where to find it, and traps

**Source:** the user, at submission time. Nothing in the software's sources establishes the submitter.

**Traps**
- The submitter's `person` is resolved before the email lookup. With no identifier it binds only on an
  exact, case-sensitive given+family match, and a name that matches no Person row creates a new, orphaned
  Person even when the email matches an existing Submitter row. Send the submitter's name exactly as their
  existing Person row stores it.
- Merging or re-pointing Submitter rows is an access-control change, not tidying: any address on a row
  unlocks every entry that row serves, and each entry publishes its submitters' masked addresses.
- A stored `Submitter.email` of the form `"['someone@example.org']"` is the supported multi-address form,
  not corruption.

## Payload and roundtrip notes

- **Shape:** `submitter` is an array of Submitter objects:

  ```json
  "submitter": [
    {
      "email": "user@example.org",
      "person": {
        "givenName": "Jane",
        "familyName": "Doe",
        "identifier": "https://orcid.org/0000-0000-0000-0000"
      }
    }
  ]
  ```

  (The address above only illustrates the shape; rule 3 forbids sending it.) `email` is required;
  `person` is a Person object with required non-empty `givenName` and `familyName`.
- **Resolution:** Submitter matches on `email` (case-insensitive); an existing row is reused and the
  payload's `person` is then discarded after being resolved (see Traps).
- **Required on POST, rejected on PATCH:** `submitter` is one of the five required fields of
  `/api/submission/`; the update endpoint rejects it with 400.
- **Confirmation email:** sent after the database commit and outside the transaction, so an email failure
  can return an error even though the record was created; check the record exists before concluding a
  submission failed.
- **Roundtrip:** the stored submitter may appear flattened (e.g. `submitterName`/`submitterEmail`) rather
  than as the submitted `submitter[].person/email` object.

## Worked examples

- **A curated record (ADELPHI).** The person who curated and transmitted the record is the submitter;
  the model's developer and its hosts are contacts for the software and appear in Field 6, not here.
- **Author's address in the source (FitsFlow).** The only address in the repository is the author's. Rule 2
  keeps it out of this field; rule 6 records the placeholder, and the dossier notes the address as
  correspondence context only.
- **A refresh of an existing entry.** Rule 1 fires: the diff and PATCH omit Field 1 entirely, and the
  dossier's placeholder stays as it is.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 50-60 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
