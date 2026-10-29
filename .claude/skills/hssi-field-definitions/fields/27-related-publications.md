# Field 27 — Related Publications

**Level:** OPTIONAL · **API:** `relatedPublications[]` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.3 (name) · **Field-search code:** `publication`

## What it is

**Type:** Multi-entry URL (RelatedItem lookup — DOI URL preferred)

**What it is:** Publications that describe, cite, or use the software that the software developer prioritizes but are different from the reference publication.

**How to fill it:** Enter the URLs — ideally DOIs — for all notable publications the software is cited in, one URL per entry (the form's "+ add" button adds a field per URL). Only a URL is accepted per entry; free-text citations are rejected. For a publication with no DOI, use any permanent link (e.g., its ADS abstract page, `https://ui.adsabs.harvard.edu/abs/<bibcode>/abstract`) and record the full citation in the dossier prose instead.

In practice: the developers' own publications about the software, the few papers the project presents
as the basis of the software, and papers that substantively use it, whoever wrote them — never the
Field 14 paper, and never a paper that merely cites it.

## Why it exists

The field holds publications: documents of scientific merit written for, about or by the software.
It gives a visitor the literature behind and around the software: where the method comes from, what
the developers have published about it, and real science done with it. A curated list tells them the
software is used and how. Padding it with every paper that happens to name the software turns it into
an arbitrary, ever-growing citation index that hides the few entries worth reading, and a long list
of the method papers its code cites does the same; leaving out the few papers the software is built
on hides the science the code implements.

## How it appears on the site

- **Detail page:** a "Related Publications" subsection of the "Related Items" section, one link per
  entry. Link text is the related item's name, or the raw URL when the name is `UNKNOWN`; items created
  through the API store the URL as their name, so the link text is normally the URL.
- **JSON-LD:** each entry is a `mentions` item, typed by the related item's stored type
  (`ScholarlyArticle` for a publication row).
- **Search:** free-text tier T4.3 on the name; `publication:"…"` matches it by substring (together with
  Field 14). Because the name is the URL, searches match the DOI string, not the paper's title.
- **Not displayed:** the paper's title, authors or venue — record those in the dossier prose.

## Rubric: include / exclude

Apply to each candidate and to each incumbent entry; stop at the first rule that fires. For an
**incumbent**, rules 1–2 are tested and then rule 7; rules 3–6 apply only to candidates for addition.
Decide Fields 14 and 27 together.

**Eligible publication types.** Every rule below that admits or keeps an entry applies only to one of
these: a peer-reviewed article (a JOSS paper included), a full paper in conference or workshop
proceedings, a preprint, a technical report, a thesis, a book chapter, or a poster deposited as the
poster itself (a Zenodo or ESS Open Archive record, say). A slide deck is eligible only when it reads
as a substantial standalone document, with text and results a reader can follow without the talk; a
deck of headings and images is not, and the user makes that call (see *Ask the user only when*). A
conference or meeting abstract is never eligible, even when the poster or paper it announces would
be: link the deposited poster or paper instead, and when neither is deposited, add nothing and record
the abstract as weighed. The type makes an entry eligible; rules 2–7 decide whether it is included.

1. **Not an eligible publication → not Field 27.** Fires for a software deposit (Field 2, 12, 29 or
   30), a dataset (Field 28), a repository or documentation URL, a conference or meeting abstract (an
   ADS meeting-abstract record or an abstract-book entry, for a talk or for a poster), a talk with no
   document of its own, a slide deck the user has judged to fail the standalone test, or a document
   with no DOI and no permanent public landing page (a PDF shipped in the repository).
2. **The Field 14 paper → not also here.** Remove it from this field under any identifier (DOI, ADS
   URL, publisher URL).
3. **The developers' own publication about the software → include.** Its subject is this software
   and its authors include the software's. Include also one by an author about the platform the
   software serves, with the dossier noting what it covers.
4. **A publication the project presents as the basis of the software, or asks users to cite for it →
   include while the list stays useful.** It is a method or model paper the code implements,
   whatever the package's structure, or a paper the project's citation guidance asks for. Evidence:
   the README or docs reference list for the method, model or algorithm; the code's own reference
   block; a second paper the project's citation guidance asks for; a per-component citation list.
   **Judge the list as a whole, from a searcher's view, and record the reasoning in the dossier.**
   Count every qualifying paper, whether or not HSSI lists it, and weigh how much each explains the
   software's purpose or an important capability, how incidental it is, and whether the combined list
   stays useful to a visitor or makes them sift. The count informs the judgment without deciding it:
   two papers behind the software's core computation are listed (solarmach); some forty, each behind
   one routine, are not (PyRFU). When the list would be too long, list none of it except a few the
   README, docs or citation guidance presents as the whole package's foundation or asks every user to
   cite: a long list buries the publications actually about the software. A per-component citation
   list, or a request to cite the references the routines give, counts with the rest and is never
   that exception. **Excluded under this rule, and not counted:** a generic numerical, statistical or
   mathematical method, a textbook or a table of standard constants, cited for one step of a
   computation (a power-spectral-density estimator, a histogram bin-width rule, a spline
   interpolation); a paper cited only by an example or tutorial; a paper the project lists only as
   further or useful reading ("Other references you might find useful"); and a reference for a file
   format the software merely reads.
5. **A publication that substantively uses the software → include, whoever wrote it, while such
   uses are still news.** Fires only when the paper's own results or software are built with this
   software **and** it says so deliberately: in its Acknowledgments, its Data Availability or Open
   Research statement, or a methods statement naming the software for a specific result. Authorship
   plays no part: a paper by the software's developers that uses it but is not about it is judged on
   this same test. Semantic Scholar citation contexts and intents help separate this from a passing
   mention. Uses are news while the software's citing literature is small: each one shows a searcher
   how and where the software is used. For widely used software, as with Astropy or SunPy, a list of
   users tells a searcher nothing: add none, and say so in the dossier. Rules 3 and 4 apply however
   widely the software is used.
6. **A publication that merely cites or mentions the software → not added.** Fires for a
   name in a bibliography, a list of tools or dependencies, background text, or a full-text hit with no
   deliberate credit; also for papers found only through an author's publication list that use the
   same data or methods rather than the software. Record the ones weighed in the dossier so a later
   refresh does not rediscover them as new.
7. **Incumbent entry → keep** when it is an eligible publication that describes, cites or uses the
   software, even if it would not be added under rules 3–6. Remove an incumbent only
   when rule 1 or 2 fires, when it does not resolve, or when it is unrelated to this software. Removing
   an incumbent because it is a meeting abstract or a talk, or a slide deck the user has judged to fail
   the standalone test, needs the user's confirmation before it enters a patch (see *Ask the user
   only when*). When an incumbent is a non-DOI URL for a paper that has a DOI, replace it with the
   DOI.
8. **Nothing qualifies → empty, with the search recorded.** Check the paper sources under *Where to
   find it* before recording "Not found".

**Form of each entry.** The paper's DOI as `https://doi.org/<doi>`; with no DOI, its ADS abstract
permalink or arXiv abstract page, with the full citation in the dossier prose.

## Ask the user only when

- **A slide deck, as a candidate or an incumbent.** The standalone test (*Eligible publication
  types*) needs a human read:
  present the deck with a one-line account of its content and how much a reader can follow without
  the talk.
- **Removing an incumbent because it is a meeting abstract or a talk, or a slide deck the user has
  judged to fail the standalone test** (rules 1 and 7). The rubric decides that an abstract or a talk
  goes, and the user's judgment decides a deck; either way the user confirms each removal before it
  enters a patch, separately from approving the final patch.

Anything else is decided by the rubric. A case no rule covers is a rubric gap: ask, and report it as
one.

## Where to find it, and traps

**Sources, in priority order.**
1. The project's own files: README and docs reference lists, citing/acknowledging pages, reference
   blocks in the code, `CITATION.cff` `references`.
2. The developers' own deposits and papers: Zenodo creator-keyed search
   (`metadata.creators.person_or_org.name:"Family, Given"`, with a control — see Field 2), ADS/SciX
   for their papers. A meeting abstract found there points to a talk or poster: look for the
   deposited poster or paper itself, and record the abstract as weighed (rule 1).
3. The literature that uses the software: ADS/SciX `full:"<name>"` and `ack:"<name>"` (acknowledgements
   are indexed separately), DataCite `IsCitedBy` relations on the software's DOIs, and Semantic Scholar
   (`api.semanticscholar.org/graph/v1`, no key), whose citation `contexts`/`intents` separate
   substantive use from a passing mention. Routes and controls are in
   `../sources/extraction-sources.md` (*Literature sources*).

**Verification.**
- DOIs must be full URLs: `https://doi.org/10.XXXX/XXXXX` (Fields 2, 12, 14, 27, 28, 29, 30).
- Resolve each DOI and read its title and type from Crossref or DataCite.
- For a field that a publication could supply (Fields 14, 25, 26, 27), check the paper's
  Acknowledgments and Data Availability Statement before concluding it isn't there — that is also
  where code DOIs surface.
- Validate every literature search with controls: a nonsense token must return 0, and a comparable
  package name must return hits, so a real zero is distinguishable from a broken query.

**Traps.**
- **Publisher 402/403** is usually bot-blocking, not a paywall; a browser renders the article, and an
  arXiv preprint or Europe PMC copy often carries the same acknowledgements. Report an unreachable
  paper as a blocker rather than recording the field as empty.
- **ADS web pages** may answer automated requests with a 405 "Human Verification" page; the record's
  existence is confirmed through the ADS API. ADS/SciX needs no personal token (anonymous bootstrap).
- **Code docstring shorthand** ("Author et al. 'Short title' JGR 2013") is not the article's title;
  take titles from the DOI record.
- **A count of full-text hits** is a pool to read, not a list to add.

## Payload and roundtrip notes

**Important — RelatedItem URL fields (27–30):** each entry must be a real URL. Free text fails the serializer's `URLValidator` (`Invalid URL: '<value>'`) and rejects the whole atomic request. Keep each URL ≤128 characters: `_get_or_create_related` stores the URL as both `identifier` and the 128-capped `name`, so a longer URL passes validation and then fails at the database write.

- Key `relatedPublications`, an array of URL strings. The array **replaces** the whole list; `[]` or
  `null` clears it; an omitted key leaves it unchanged.
- Each URL binds an existing related item on the exact identifier, else creates one typed
  Publication. **A related item keeps its type on reuse:** a URL first created as software or a
  dataset stays typed that way (including in JSON-LD) when listed here; moving a URL between Fields
  14, 27, 28, 29 and 30 does not retype it.
- Related item names are placeholders — the URL itself, or `UNKNOWN`, in which case the page shows the
  identifier as link text. Never choose or compare values by name; compare on `identifier`.
- `/api/data/` returns related-item row UUIDs; `/api/view/` returns the URLs.

## Worked examples

- **Posters moved in from Field 2.** HERMES Core's two conference posters describe the package's
  architecture and were written by its authors. Rule 3 includes both here, after
  Field 2 rule 1 removed one of them from Field 2.
- **Users not added.** madrigalWeb has four third-party papers that used the package, none crediting
  it in acknowledgements. Rule 6 excludes them, and the dossier lists them as weighed.
- **Meeting abstracts excluded.** A package's developers presented it at several AAS and AGU
  meetings, and the search finds each presentation only as an ADS meeting abstract. Rule 1 excludes
  every abstract. A presentation whose poster is deposited (a Zenodo record with the PDF) enters
  through that deposit under rule 3; the rest add nothing, and the dossier records all of them as
  weighed.
- **Acknowledged use.** GEOrinex has eleven papers that use it; two credit it in their
  Acknowledgments (a real-time ionospheric assimilation model and a GNSS software paper built on it).
  Rule 5 includes those two; a topically close paper that names it only in the full text is excluded
  under rule 6 and recorded as weighed.
- **Developer-led use.** Kovac et al. (2026), the Citizen CATE 2024 paper in Solar Physics, is led
  by a solpolpy author but is not about solpolpy; its §8.3 converts the eclipse images "using
  solpolpy". Rule 5 includes it on the same test as anyone's paper.
- **Widely used.** SPEDAS's wiki links a bibliography of hundreds of refereed papers that used it.
  Rule 5 adds none of them: a list of users says nothing about the software. Field 27 keeps the
  publications rules 3 and 4 admit.
- **Model paper as ADS permalink.** ReesAurora's code cites Sergienko and Ivanov (1993), the model it
  implements, in its reference block. Rule 4 includes it; it has no DOI, so the entry is its ADS
  abstract permalink.
- **Two method papers listed.** solarmach's code cites exactly two method papers: Poljančić Beljan
  et al. (2017) for the differential-rotation rate its backmapping uses, and Thompson (2006) for the
  coordinate conversion that places the elements of its 3D figures. Both explain how the package
  computes what it exists to show, and a list of two stays useful, so rule 4 lists both.
- **Too many method papers to list.** PyRFU cites some 48 method, model and numerical papers, nearly
  all in the reference blocks of the routines they motivated: the curlometer, minimum variance
  analysis, the bow-shock and magnetopause models, Welch's spectral estimator and more. Its README
  asks users to cite the software deposit and, as well, the methods the routines' references give;
  that second request counts with the rest. Some forty qualify even without the generic ones, each
  incidental to the library as a whole, and together they would bury the papers about it, so rule 4
  lists none of them.
- **Further reading excluded.** pyflct's docs list a methods paper under "Other references you might
  find useful". Rule 4's further-reading exclusion fires; the two algorithm references stay.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 654-662 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
- Changed 2026-10-28: a new *Eligible publication types* paragraph governs every rule (meeting
  abstracts and talks are not publications, deposited posters are, slide decks need a human read), and
  removing an incumbent on these grounds needs the user's confirmation (rules 1 and 7, Ask list).
- Changed 2026-10-29 (the maintainer's ruling on PyRFU): rule 4 lists the method, model and cited
  papers only while, judged as a list from a searcher's view, they stay useful; when the list would
  be too long, only a few the project presents as the whole package's foundation or asks every user
  to cite. Generic numerical, statistical or mathematical references, textbooks and papers cited
  only by an example are not listed.
- Changed 2026-10-29: rules 5 and 6 no longer turn on authorship. Rule 5 includes any eligible paper
  whose own results or software are built with this software and that credits it deliberately,
  whoever wrote it, the developers included; rule 6 excludes a mere citation or mention by anyone.
  Rule 3, for the developers' papers about the software, is unchanged.
