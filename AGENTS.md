# AGENTS.md — Makoto-kun 3.1

## Project purpose

This repository is the knowledge base for **Makoto-kun 3.1**, an AI teaching assistant for the Nagoya University × CU Boulder NUCU program.

Humans keep original source material locally in `raw/`. Codex reads those sources and compiles retrieval-friendly knowledge into `wiki/`. Only reviewed, public-safe wiki pages and project instructions are committed to the public GitHub repository. An n8n workflow loads the compiled wiki pages into PostgreSQL with PGVector for use by student-facing web, Discord, or Slack interfaces.

This project is also a teaching tool. Make important design choices understandable and record completed construction work in `LOGBUILD.md`.

## Project structure

```text
mk3.1/
├── .gitignore
├── .githooks/
│   └── pre-commit
├── AGENTS.md
├── SOUL.md
├── MIND.md
├── BODY.md
├── README.md
├── LOGBUILD.md
├── raw/
│   ├── automation/
│   │   └── shared/
│   ├── curriculum/
│   │   ├── 2026/
│   │   └── 2027/
│   └── program/
│       ├── 2026/
│       └── 2027/
└── wiki/
    ├── concepts/
    │   ├── shared/
    │   ├── 2026/
    │   └── 2027/
    ├── entities/
    │   ├── shared/
    │   ├── 2026/
    │   └── 2027/
    ├── sources/
    │   ├── shared/
    │   ├── 2026/
    │   └── 2027/
    ├── index.md
    └── log.md
```

## File responsibilities

- `AGENTS.md` governs how Codex builds and maintains this repository.
- `.githooks/pre-commit` blocks raw files, obvious credentials, and unapproved wiki pages before a commit.
- `SOUL.md` defines who Makoto-kun is and how he relates to students.
- `MIND.md` defines how Makoto-kun retrieves evidence and constructs answers.
- `BODY.md` documents Makoto-kun’s interfaces, tools, capabilities, and limitations.
- `README.md` explains the project to people.
- `LOGBUILD.md` records project construction and architectural changes.
- `raw/` contains local-only original source material and is excluded from Git except for `.gitkeep` placeholders.
- `wiki/` contains reviewed, public-safe compiled factual knowledge used for retrieval.

Root-level operating documents are not factual knowledge sources and must remain outside `wiki/`.

Before changing Makoto-kun’s runtime behavior or n8n system instructions, read `SOUL.md`, `MIND.md`, and `BODY.md` together.

## Ownership and safety

1. **`raw/` is local-only and immutable.** Never edit, rename, move, delete, stage, commit, or push source documents under `raw/`. Only `.gitkeep` placeholders may be tracked. If a source contains an error, record the issue in its corresponding `wiki/sources/` page.
2. **`wiki/` is compiled knowledge.** Codex may create, update, merge, and split wiki pages while preserving source attribution.
3. **Root instruction files are human-owned.** Propose changes before editing `AGENTS.md`, `SOUL.md`, `MIND.md`, or `BODY.md`, unless the user explicitly requests the edit.
4. Never store passwords, API keys, tokens, database credentials, or private student information in this repository.
5. Do not describe a planned workflow, database table, collection, or deployment as active until it has been verified.
6. Do not silently correct or replace a raw source.
7. If source material is ambiguous, preserve the ambiguity and report it.
8. Treat the public GitHub repository as publicly readable, even if its visibility changes later.
9. Review every wiki page for personal, confidential, credential, and internal-only information before staging it.
10. Remember that `.gitignore` reduces accidental commits but does not prevent a forced commit.
11. Never bypass the pre-commit hook merely to make a commit succeed. Resolve or explicitly review the flagged content.

## Course-year scopes

Every local raw source and compiled wiki page must belong to one of these scopes:

- `2026`: archived material from the 2026 course.
- `2027`: current material for the 2027 course.
- `shared`: genuinely year-independent information.

Determine the scope from the file’s directory path. Do not guess the year from its contents.

### Course-year routing rules

- Files under a `2026/` directory use `course_year: "2026"` and `status: "archived"`.
- Files under a `2027/` directory use `course_year: "2027"` and `status: "current"`.
- Files under a `shared/` directory use `course_year: "shared"` and `status: "evergreen"`.
- Place compiled pages in the corresponding year or shared wiki directory.
- Never overwrite a 2026 page with 2027 information.
- Differences between course years are revisions, not contradictions.
- Use `shared/` only when the information is genuinely valid across course years.
- If a raw file is stored outside a year or shared directory, report the ambiguity instead of assigning a year.
- Never move an incorrectly filed raw source without explicit permission.
- When 2027 material replaces a 2026 policy, preserve both versions and clearly label their years.
- Do not present archived information as current.

##### Wiki page frontmatter

Every knowledge page must begin with YAML frontmatter.

The following block is a **template, not literal content**. Replace every uppercase placeholder with page-specific values. Never leave template values or placeholders in a finished wiki page.

```yaml
---
type: "PAGE_TYPE"
title: "PAGE_TITLE"
course_year: "COURSE_YEAR"
status: "PAGE_STATUS"
publication_status: "review-required"
sources:
  - raw/CATEGORY/YEAR_OR_SHARED/EXACT_SOURCE_FILENAME
updated: "CURRENT_DATE"
tags:
  - PAGE_SPECIFIC_TAG
---
```

Populate each field dynamically:

- `type`: Use `concept`, `entity`, or `source`, based on the page’s purpose.
- `title`: Write the human-readable subject of the page.
- `course_year`: Use `"2026"`, `"2027"`, or `"shared"`, based on the directory path.
- `status`: Use `"archived"`, `"current"`, or `"evergreen"` according to the course-year routing rules.
- `publication_status`: The compiling agent must use `"review-required"`. Only a human reviewer may change it to `"approved-public"`.
- `sources`: List the exact project-relative local path of every raw file supporting the page. The raw file may be Git-ignored, but its filename must still be safe to reveal publicly.
- `updated`: Use the actual current date in `YYYY-MM-DD` format whenever the page is created or meaningfully revised.
- `tags`: Derive concise, lowercase, page-specific tags from the content.

For year-specific pages:

- Include the course year in the title.
- Identify the course year in the opening paragraph.
- Include the year as a tag.

When multiple raw files support a page, list every source path.

Before saving a page, verify:

1. No uppercase placeholders remain.
2. Every listed source path exists.
3. The frontmatter year matches the directory year.
4. The status matches the course-year routing rules.
5. A newly created or meaningfully revised page uses `publication_status: "review-required"`.
6. The title and opening paragraph identify the year when the page is year-specific.
6. Archived information is not described as current.

## Wiki page types

### Source pages

Source pages belong in:

```text
wiki/sources/shared/
wiki/sources/2026/
wiki/sources/2027/
```

Create one comprehensive source page for every raw source. A source page should preserve the source’s important claims, details, examples, terminology, and context.

### Concept pages

Concept pages explain ideas, processes, themes, and general principles.

Examples include:

- vector embeddings;
- Meiji modernization;
- cultural adaptation;
- entrepreneurship;
- retrieval-augmented generation.

Place a concept in `shared/` only when it is independent of a particular course year. Place year-specific presentations or interpretations in the matching year directory.

### Entity pages

Entity pages describe specific named things, including:

- people;
- organizations;
- universities;
- locations;
- software platforms;
- events;
- named objects;
- programs.

Stable entity information may live in `shared/`. Year-specific policies, roles, schedules, or arrangements must live in the matching year directory.

## Filenames

- Use lowercase, hyphenated filenames.
- Use clear, descriptive names.
- Include `2026` or `2027` in year-specific filenames.
- Use a source date in source-page filenames when a reliable date exists.
- Do not rename an existing wiki file without recording the change in `wiki/log.md`.

Examples:

```text
wiki/sources/2026/2026-01-20-session-2-reinvention-under-pressure.md
wiki/concepts/shared/vector-embeddings.md
wiki/entities/2027/yamate-south-2027.md
```

## Writing for retrieval

Wiki pages are retrieved in isolation. Therefore:

- Make every page understandable without following links.
- Front-load a direct two- or three-sentence summary.
- Preserve exact names, dates, quantities, terminology, and alternate spellings.
- Identify people, organizations, places, events, and named objects explicitly.
- Repeat essential context when necessary for isolated retrieval.
- Avoid vague references such as “this,” “it,” or “the event” when the subject can be named.
- Use plain English suitable for students who may be non-native English speakers.
- Prefer concrete examples over abstract summaries.
- Use wikilinks for navigation, but never rely on a link to supply essential meaning.
- Target approximately 300–800 words.
- Split substantially longer pages when practical.
- Never remove a narrow fact merely because it does not fit the main summary.

## Ingestion workflow

Trigger phrase:

> New files have been added to raw/. Ingest them.

For every new source:

1. Confirm that the source is under `2026/`, `2027/`, or `shared/`.
2. Determine `course_year` and `status` from the directory path.
3. Read the complete source.
4. Create a corresponding page in the matching `wiki/sources/` directory.
5. Create or update relevant pages in the matching `wiki/concepts/` and `wiki/entities/` directories.
6. Prefer updating an existing matching page over creating a near-duplicate.
7. Keep year-specific claims out of shared pages unless the claim is valid across years.
8. Add useful wikilinks in both directions.
9. Preserve genuine source conflicts under a clearly labeled `Conflicting information` section.
10. Do not label differences between course years as source conflicts.
11. Update `wiki/index.md`.
12. Append a dated entry to `wiki/log.md`.
13. Perform the fact-preservation check.
14. Perform the public-release check before staging or committing compiled pages.
15. Declare ingestion complete only after both checks pass.

## Fact-preservation check

Compilation must preserve more than the source’s main themes.

Capture:

- quiz-relevant facts;
- named examples and memorable asides;
- people, places, organizations, objects, and events;
- dates and historical periods;
- quantities, prices, measurements, and percentages;
- sequences of steps;
- comparisons and contrasts;
- causes and effects;
- definitions and alternate names;
- exceptions, warnings, and limitations;
- claims that appear only once but could answer a direct question.

Do not assume a fact is unimportant merely because it appears only once.

If a detail does not justify its own concept or entity page, preserve it in the comprehensive source page.

Before completing ingestion:

1. Compare the compiled pages with the original source.
2. Check that every material factual section appears somewhere in the wiki.
3. Check proper nouns, dates, quantities, named examples, and memorable asides separately.
4. Test several direct fact questions using exact wording.
5. Test paraphrased versions of those questions.
6. Test at least one synthesis question.
7. Report any uncertain, unreadable, or intentionally omitted material.

## Public-release check

The GitHub repository is public. Before staging any compiled wiki page, check the page body, filename, links, and frontmatter for:

- student names or identifying details that are not approved for publication;
- personal email addresses, phone numbers, or home addresses;
- passwords, API keys, access tokens, credentials, or private URLs;
- private calendar or meeting links;
- internal-only procedures or staff discussions;
- confidential academic, medical, financial, housing, or disciplinary information;
- sensitive details copied from a raw source;
- raw-source filenames that reveal information that should remain private.

If a page contains non-public information:

1. Do not stage, commit, push, or embed it.
2. Report the issue to the user.
3. Create a sanitized public version only with explicit approval.
4. Preserve the original evidence locally in `raw/`.

Passing a fact-preservation check does not mean a page is safe to publish. Accuracy review and public-release review are separate requirements.

### Publication classifications

**Normally publishable after review:**

- names and facts about historical figures;
- public officials and public institutional leaders;
- public organizations, universities, and companies;
- publicly launched startups;
- startup ideas already presented or released publicly with the owner's permission;
- facts already contained in approved public course material.

**Review required before publication:**

- student names or other student identifiers;
- student-created startup ideas that may be unpublished;
- early-stage projects, pitches, or research not clearly public;
- internal program discussions or decisions;
- staff contact details;
- any information whose publication status is unclear.

**Never publish:**

- passwords, API keys, tokens, credentials, or private keys;
- private student records;
- medical, financial, disciplinary, or other highly sensitive personal information;
- private meeting, calendar, database, or administration links.

The compiler must not silently remove a person, startup, or idea merely because it has a name. Preserve accurate content locally, set the page to `publication_status: "review-required"`, and alert the user when a publication decision is needed.

Credentials and highly sensitive personal information are exceptions: do not reproduce them in a compiled page. Replace them with a clear redaction marker and alert the user.

Only a human reviewer may change a page to:

```yaml
publication_status: "approved-public"
```

Any meaningful revision resets the page to `publication_status: "review-required"`.

Trigger phrase:

> Run a public-release check.

When triggered:

1. Review every new or changed public-facing file.
2. Classify names, organizations, startups, and ideas using the rules above.
3. Flag every item requiring human judgment.
4. Confirm that prohibited content is absent or redacted.
5. Confirm that every changed wiki knowledge page is still marked `review-required`.
6. Ask the user to approve or reject each flagged page.
7. Change approved pages to `approved-public` only after explicit human approval.
8. Report which files are safe to stage and which must remain local.

### Automated pre-commit guard

The versioned hook at `.githooks/pre-commit` blocks:

- any staged file under `raw/` other than `.gitkeep`;
- common credential-bearing filenames;
- obvious API tokens, private keys, and credential-bearing database URLs;
- wiki knowledge pages that do not contain `publication_status: "approved-public"`.

The hook does not understand context well enough to decide whether a person, startup, or idea is confidential. Human public-release review remains required.

Enable the versioned hook once in each local clone:

```bash
git config core.hooksPath .githooks
```

## Query workflow

When asked to answer from the wiki:

1. Search `wiki/` before using general knowledge.
2. Determine whether the question refers to 2026, 2027, shared knowledge, or a comparison.
3. If the user specifies a year, prioritize that year plus shared knowledge.
4. If no year is specified, default current course, schedule, policy, housing, and logistics questions to 2027.
5. Use 2026 material only for explicitly historical, archived, or comparison questions.
6. When comparing years, search both and label each claim by year.
7. Try alternate names, spellings, related terms, and contextual searches when the first search fails.
8. Do not conclude that information is absent after only one unsuccessful search.
9. Cite the wiki page or raw source supporting the answer.
10. Clearly distinguish sourced statements from inference or general knowledge.
11. If the wiki cannot answer after reasonable searches, say what is missing instead of inventing an answer.

For year-sensitive answers, explicitly state the applicable course year.

Never present a 2026 schedule, policy, assignment, deadline, housing rule, or logistical instruction as current for 2027.

## Lint workflow

Trigger phrase:

> Run a lint pass.

Check for:

- broken wikilinks;
- pages missing from `wiki/index.md`;
- missing or invalid `sources` entries;
- source paths that do not exist;
- raw sources with no compiled source page;
- duplicated or conflicting pages;
- important concepts lacking their own page;
- pages that have grown too long;
- stale `updated` dates on modified pages;
- uppercase template placeholders left in frontmatter;
- mismatches between directory year and `course_year`;
- mismatches between year and `status`;
- year-specific titles that fail to identify the year;
- archived information described as current;
- current and archived claims combined without labels;
- personal or confidential information in public wiki pages;
- credentials, tokens, private URLs, or private meeting links;
- raw-source filenames that reveal sensitive information;
- compiled pages that have not passed the public-release check.

Report contradictions and year mismatches. Do not resolve them by deleting source material.

## Downstream vector-store rules

The MK3.1 loader should ingest only reviewed, public-safe factual pages under `wiki/**/*.md`.

- Keep `SOUL.md`, `MIND.md`, `BODY.md`, `AGENTS.md`, `README.md`, and `LOGBUILD.md` outside `wiki/`.
- Configure the loader to skip `wiki/index.md` and `wiki/log.md`.
- Preserve each wiki page’s repository path as source metadata.
- Preserve `course_year` and `status` as vector-store metadata.
- Keep current and archived course material distinguishable during retrieval.
- Verify the active PGVector table and collection in n8n before loading or querying.
- Do not wipe or write to another assistant’s vector table.
- Treat database-table and collection isolation as privacy and rollback boundaries.
- Do not claim that collection-based or metadata-filtered retrieval is active until it has been tested end to end.

## Runtime instruction files

`SOUL.md`, `MIND.md`, and `BODY.md` do not belong in the vector store.

The n8n runtime must load their contents explicitly into Makoto-kun’s system instructions.

Use them as follows:

- `SOUL.md`: identity, purpose, values, personality, voice, and relational behavior.
- `MIND.md`: retrieval strategy, reasoning discipline, evidence rules, year selection, and uncertainty handling.
- `BODY.md`: web, Discord, and Slack interfaces; n8n tools; PGVector access; connected services; capabilities; and limitations.

Do not place course facts, lecture notes, policies, or schedules in these files.

## Teaching record

After a meaningful completed build step, append a short entry to `LOGBUILD.md` containing:

- the date;
- what was built or changed;
- why the decision was made;
- how it was verified;
- any remaining uncertainty;
- the next planned step.

Use `wiki/log.md` for knowledge-ingestion history and `LOGBUILD.md` for system-construction history.

## Working principle

Accuracy over completeness. Evidence over confidence. Clear teaching over clever presentation. When uncertain, preserve the uncertainty and report it.
