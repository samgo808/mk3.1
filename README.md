# Makoto-kun 3.1

Makoto-kun 3.1, or MK3.1, is an AI teaching assistant for the Nagoya University × CU Boulder NUCU program.

The project is also a teaching tool. Its structure makes it possible for students to examine how an AI assistant is designed, grounded in evidence, connected to tools, tested, and improved.

## Project goals

MK3.1 is designed to:

- answer questions using reviewed NUCU material;
- preserve specific facts from lectures and program documents;
- distinguish between course years;
- explain uncertainty instead of inventing answers;
- offer to contact the NUCU Team when necessary;
- create calendar events with student authorization;
- notify the NUCU Team when an event is created;
- support web, Discord, and possibly Slack chat interfaces.

## System overview

The intended knowledge pipeline is:

**Local private raw documents → local compilation and public-release review → public-safe wiki → GitHub → vector-store loader → Railway PGVector → MK3.1 → students**

Each stage has a separate responsibility:

1. `raw/` preserves original source material locally.
2. Local compilation turns source material into retrieval-friendly wiki pages.
3. Public-release review removes or blocks non-public information.
4. GitHub versions only approved wiki pages and project instructions.
5. The n8n loader creates embeddings from eligible wiki pages.
6. Railway PGVector stores searchable knowledge.
7. The MK3.1 agent retrieves evidence and answers students.
8. Chat interfaces deliver the answers.

## Public repository boundary

The GitHub repository is public.

The repository may contain:

- project instruction files;
- reviewed, public-safe wiki pages;
- `.gitkeep` placeholders preserving the directory structure.

The repository must not contain:

- original raw documents;
- student personal information;
- private staff information;
- passwords, API keys, tokens, or database credentials;
- private calendar or meeting links;
- internal-only material;
- compiled pages that have not passed public-release review.

The root `.gitignore` keeps documents under `raw/` local while allowing `.gitkeep` placeholders to be committed.

Adding `.gitignore` does not remove a file that was already committed, and a forced Git add can override it. Every staged change must still be reviewed.

Every new or meaningfully revised wiki knowledge page starts with:

`publication_status: "review-required"`

Only a human reviewer may change this to:

`publication_status: "approved-public"`

The versioned pre-commit hook blocks unapproved wiki pages, raw source documents, and obvious credentials.

Enable it once in each local clone:

`git config core.hooksPath .githooks`

The hook enforces mechanical checks. A human must still decide whether a student's name, startup, or unpublished idea is appropriate to publish.

## Instruction files

| File | Responsibility |
|---|---|
| `SOUL.md` | Identity, purpose, personality, values, tone, and ethical boundaries |
| `MIND.md` | Question interpretation, retrieval, reasoning, evidence, uncertainty, and escalation |
| `BODY.md` | Tools, interfaces, permissions, memory, data boundaries, email, and calendar actions |
| `AGENTS.md` | Rules for maintaining and compiling the repository |
| `LOGBUILD.md` | Chronological record of construction, decisions, tests, and unfinished work |
| `README.md` | Human-readable overview of the complete project |

These files remain outside `wiki/` because they are system instructions, not factual NUCU knowledge.

Creating the files does not automatically change the live agent. `SOUL.md`, `MIND.md`, and `BODY.md` must be explicitly loaded into the n8n AI Agent's system instructions.

## Project structure

- `.gitignore`
- `.githooks/pre-commit`
- `AGENTS.md`
- `BODY.md`
- `LOGBUILD.md`
- `MIND.md`
- `README.md`
- `SOUL.md`
- `raw/`
  - `automation/shared/`
  - `curriculum/2026/`
  - `curriculum/2027/`
  - `program/2026/`
  - `program/2027/`
- `wiki/`
  - `concepts/2026/`
  - `concepts/2027/`
  - `concepts/shared/`
  - `entities/2026/`
  - `entities/2027/`
  - `entities/shared/`
  - `sources/2026/`
  - `sources/2027/`
  - `sources/shared/`
  - `index.md`
  - `log.md`

## Raw and wiki responsibilities

### Local raw sources

Files in `raw/` are:

- private and local-only;
- immutable after they are added;
- the evidence used during local compilation;
- excluded from Git and GitHub.

Corrections and interpretations belong in `wiki/`, not in original raw files.

### Public compiled wiki

Files in `wiki/` are:

- compiled from raw sources;
- written for retrieval;
- reviewed for accuracy;
- reviewed separately for public release;
- eligible for GitHub and PGVector only after both reviews pass.

The compiler does not silently remove named people, startups, or ideas. Public historical figures and public organizations are normally publishable after review. Student names, unpublished startup ideas, and unclear material require a human publication decision.

## Wiki page types

### Source pages

Source pages preserve document- or lecture-specific information, including:

- exact facts;
- names;
- dates;
- quantities;
- distinctive wording;
- memorable examples.

### Concept pages

Concept pages explain:

- ideas;
- themes;
- theories;
- processes;
- causal relationships;
- connections across sources.

### Entity pages

Entity pages describe named subjects such as:

- people;
- places;
- organizations;
- programs;
- projects;
- events.

## Course-year organization

MK3.1 separates knowledge into:

- `2026` — material associated with the 2026 course;
- `2027` — material associated with the 2027 course;
- `shared` — information that genuinely applies across years.

The system must not silently merge year-specific information or present an earlier year's material as current policy.

## Vector database

The designated PGVector table for MK3.1 is:

`makoto_wiki_vectors_v31`

Other tables belong to separate systems:

| Table | System |
|---|---|
| `documents` | MK2 |
| `makoto_wiki_vectors` | MK3.0 |
| `makoto_wiki_vectors_v31` | MK3.1 |
| `angie_documents` | Angie PA |

The MK3.1 loader and chat workflow must both use `makoto_wiki_vectors_v31`.

## Retrieval design

MK3.1 should not conclude that information is absent after one failed search.

When necessary, it performs:

1. a direct search;
2. an expanded search using related terms;
3. a source-focused search using the year, lecture, or document context.

The agent should:

- prefer source pages for exact lecture facts;
- prefer concept pages for synthesis;
- prefer entity pages for named subjects;
- inspect the correct course year;
- distinguish evidence from inference;
- acknowledge conflicts and uncertainty.

## Tools and actions

Depending on the connected n8n nodes, MK3.1 may be able to:

- search the knowledge base;
- maintain short-term conversation context;
- email the NUCU Team;
- create calendar events;
- respond through connected chat interfaces.

A tool is available only when it is connected, configured, and verified in n8n.

### Email

MK3.1 must obtain permission before emailing the NUCU Team. It requests a student reply address only when needed and uses it only with permission.

### Calendar

MK3.1 must confirm event details and authorization before creating an event. After successful calendar creation, it must separately email the NUCU Team and report both results.

## Conversation memory

Conversation memory is short-term context, not permanent student memory or authoritative NUCU knowledge.

Before student deployment, every interface must provide an isolated session identifier so conversations belonging to different students cannot mix.

## Student interfaces

Planned or possible interfaces include:

- n8n test chat;
- Discord;
- Slack;
- a dedicated student web interface.

All interfaces should use the same MK3.1 agent, vector table, safety rules, and tool-confirmation requirements.

Chat history does not automatically become knowledge-base content. Any future ingestion of student conversations requires a separate consent, access, retention, and deletion policy.

## Intended ingestion workflow

1. Add an original document to the correct local `raw/` directory.
2. Compile it locally into appropriate wiki pages.
3. Check fact preservation against the original source.
4. Conduct a separate public-release review.
5. Keep new or revised pages marked `review-required` until a human approves them.
6. Change approved pages to `approved-public`.
7. Update `wiki/index.md` and `wiki/log.md`.
8. Stage only approved project and wiki files.
9. Inspect the staged Git diff.
10. Commit and push the reviewed changes to GitHub.
11. Run the MK3.1 Wiki to Vector Store Loader.
12. Verify the table and test representative questions.

## Testing categories

MK3.1 should be tested with:

- direct factual questions;
- lecture-specific details;
- synthesis and comparison questions;
- program logistics;
- course-year separation;
- unavailable answers;
- NUCU Team email escalation;
- calendar creation and notification;
- separate student sessions;
- end-to-end chat interfaces.

## Build status

### Complete locally

- [x] Project directory structure
- [x] Course-year separation
- [x] `.gitignore` protecting local raw documents
- [x] Versioned public-release pre-commit hook
- [x] Required human publication approval for wiki pages
- [x] `AGENTS.md`
- [x] `SOUL.md`
- [x] `MIND.md`
- [x] `BODY.md`
- [x] `README.md`
- [x] `LOGBUILD.md`
- [x] Local Git repository initialized on `main`
- [x] MK3.1 vector-table name selected

### Configured but not verified

- [ ] MK3.1 loader targeting `makoto_wiki_vectors_v31`
- [ ] Table creation and population
- [ ] MK3.1 chat retrieval from the new table

### Not yet completed

- [ ] Create and connect the GitHub repository
- [ ] Make the first Git commit
- [ ] Migrate selected 2026 sources locally
- [ ] Add 2027 sources locally
- [ ] Compile and publicly review the first wiki pages
- [ ] Run and verify the loader
- [ ] Load `SOUL.md`, `MIND.md`, and `BODY.md` into the AI Agent
- [ ] Configure isolated student session identifiers
- [ ] Test email and calendar behavior
- [ ] Complete an end-to-end Discord test
- [ ] Decide whether to support Slack
- [ ] Build the student web interface
- [ ] Define chat-history privacy and retention rules

## Build documentation

Every meaningful change should be recorded in `LOGBUILD.md` with:

- what changed;
- why it changed;
- how it was verified;
- what remains unfinished;
- the next action.

## Current next step

Inspect and stage the public-safe initial project files, review the staged diff, and create the first local Git commit.
