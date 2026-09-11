# Makoto-kun 3.1 Build Log

This file records how MK3.1 was constructed, why architectural decisions were made, how changes were verified, and what remains unfinished.

## Status labels

- **COMPLETE** — created and reviewed locally.
- **CONFIGURED — UNVERIFIED** — configured but not confirmed through an end-to-end test.
- **PLANNED** — agreed upon but not yet implemented.
- **BLOCKED** — cannot continue without missing information, access, or a decision.

## Log-file distinction

- `LOGBUILD.md` records construction of the MK3.1 system.
- `wiki/log.md` records ingestion and changes to compiled knowledge.

Do not replace older history silently. Add a dated correction when a previous status changes.

---

## 2026-09-06 — Project foundation

**Status:** COMPLETE

### Built

- Created `/Users/tanuki/Documents/GPT/mk3.1`.
- Created separate `raw/` and `wiki/` areas.
- Created curriculum, program, and automation source categories.
- Created source, concept, and entity wiki categories.
- Created `wiki/index.md` and `wiki/log.md`.
- Copied the MK3.0 Wiki to Vector Store Loader for MK3.1.

### Decisions

- Preserve original source material separately from compiled knowledge.
- Compile retrieval-friendly wiki pages before embedding content.
- Use `makoto_wiki_vectors_v31` as the designated MK3.1 vector table.
- Keep MK2, MK3.0, MK3.1, and Angie PA vector tables isolated.

### n8n configuration

- Changed the table-removal SQL to target `makoto_wiki_vectors_v31`.
- Changed the loader's PGVector Store table name to `makoto_wiki_vectors_v31`.

**Status:** CONFIGURED — UNVERIFIED

### Verification

- Reviewed the local directory structure.
- Reviewed the n8n loader settings visually.
- Did not verify table population, chat retrieval, or production cutover.

---

## 2026-09-09 — Course-year structure

**Status:** COMPLETE

### Built

- Created 2026 and 2027 directories for curriculum and program material.
- Created shared directories for year-independent material.
- Created 2026, 2027, and shared wiki scopes for sources, concepts, and entities.

### Decisions

- Preserve 2026 material rather than overwriting it with 2027 updates.
- Use directory paths and YAML metadata to distinguish course years.
- Do not present archived information as current.
- Treat differences between course years as revisions rather than source conflicts.

### Verification

- Inspected the directory tree.
- Confirmed `wiki/sources/shared/` exists.

---

## 2026-09-09 — Agent instruction files

**Status:** COMPLETE

### Built

- Created `AGENTS.md` for repository maintenance and compilation rules.
- Created `SOUL.md` for identity, values, tone, and boundaries.
- Created `MIND.md` for retrieval, reasoning, evidence, and uncertainty.
- Created `BODY.md` for tools, interfaces, permissions, and data boundaries.

### Decisions

- Keep instruction files outside the factual wiki.
- Require explicit loading of `SOUL.md`, `MIND.md`, and `BODY.md` into the n8n system prompt.
- Preserve narrow facts, named examples, dates, quantities, and memorable asides during compilation.
- Do not conclude that information is absent after one failed retrieval.
- Allow MK3.1 to offer to ask the NUCU Team when an answer cannot be confirmed.
- Require permission before sending email or using a student's reply address.
- Require a successful calendar event to be followed by a separate NUCU Team notification email.
- Report calendar and email outcomes separately.

### Verification

- Created and manually reviewed all four instruction files.
- Did not yet load the runtime instruction files into n8n.
- Did not yet test retrieval, email, calendar, or student-session behavior.

---

## 2026-09-09 — Project overview and interface plan

**Status:** COMPLETE for documentation; PLANNED for interfaces

### Built

- Created a student-readable `README.md`.
- Documented the pipeline, file responsibilities, year scopes, vector-table boundaries, tools, and testing categories.

### Planned interfaces

- n8n test chat
- Discord
- possibly Slack
- a dedicated student web interface

### Interface requirements

- Route every interface through the same MK3.1 agent and vector table.
- Provide a unique session identifier for each student.
- Prevent conversation memory from crossing between students.
- Keep credentials and Railway access on the server side.
- Preserve the same email, calendar, evidence, and permission rules everywhere.
- Do not ingest chat history without a separate privacy and retention policy.

---

## 2026-09-10 — Local Git repository

**Status:** COMPLETE

### Built

- Initialized a local Git repository.
- Set the initial branch to `main`.
- Added `.gitkeep` placeholders to preserve empty directories.
- Created `.gitignore` for credentials, temporary files, generated files, and local raw documents.

### Verification

- `git status` confirmed the repository is on `main` with no commits yet.
- `git status --short` showed the intended project files as untracked.
- A read-only credential-pattern scan found no obvious credentials in the initial project files.
- No files had been staged or committed at this point.

---

## 2026-09-10 — Local raw sources and public GitHub boundary

**Status:** COMPLETE for policy; UNVERIFIED for future compiled pages

### Decision

Keep original raw documents only on the local computer. Commit only reviewed, public-safe compiled wiki pages and project instructions to GitHub.

The pipeline is now:

**Local private raw documents → local compilation → fact review → public-release review → public-safe wiki → GitHub → PGVector**

### `.gitignore` rule

The repository ignores everything under `raw/` except `.gitkeep` placeholders.

This preserves the public directory structure without publishing source documents.

### Public-release review

Before staging a wiki page, inspect it for:

- student or staff personal information;
- email addresses, phone numbers, or home addresses;
- passwords, API keys, access tokens, or credentials;
- private URLs, calendar links, or meeting links;
- internal-only procedures or discussions;
- confidential academic, medical, financial, housing, or disciplinary information;
- raw-source filenames that reveal sensitive information.

Fact preservation and public-release safety are separate checks. A page can be accurate and still be unsafe to publish.

### Documentation changes

- Updated `AGENTS.md` with the local-only raw-source and public-release rules.
- Corrected `README.md` so it describes the project rather than duplicating the build log.
- Updated `README.md` with the new private-raw/public-wiki pipeline.
- Updated this build log to reflect the current project state.

### Verification

- Confirmed the raw exclusion rules exist in `.gitignore`.
- Confirmed `AGENTS.md` requires a public-release check.
- Confirmed the README identifies raw documents as local-only.
- Raw documents have not been staged or committed.

---

## 2026-09-10 — Publication classification and commit guard

**Status:** COMPLETE for configuration; UNVERIFIED on the first real wiki publication

### Decisions

- Preserve public historical figures, organizations, startups, and publicly released ideas during compilation.
- Require human review for student names, unpublished startup ideas, early-stage projects, and unclear material.
- Never publish credentials, private records, or private administration links.
- Do not silently omit named people, startups, or ideas solely because they have names.
- Mark every new or meaningfully revised wiki page `publication_status: "review-required"`.
- Allow only a human reviewer to change that value to `publication_status: "approved-public"`.

### Built

- Added explicit publication classifications to `AGENTS.md`.
- Added the trigger phrase `Run a public-release check.`
- Added `.githooks/pre-commit` as a versioned commit guard.
- Configured the guard to block raw documents, obvious credentials, and unapproved wiki pages.

### Limitations

- Automated pattern checks cannot determine whether a startup idea or personal name is confidential.
- Human review remains required before changing a page to `approved-public`.
- The hook configuration is local to each clone and must be enabled again on a different computer or fresh clone.

### Verification

- Reviewed the publication classifications and approval workflow.
- Made `.githooks/pre-commit` executable.
- Set `core.hooksPath` to `.githooks` in the local repository.
- Confirmed the hook passes a Bash syntax check.
- Confirmed the hook runs successfully when no files are staged.

---

## 2026-09-10 — Public GitHub repository launch

**Status:** COMPLETE

### Built

- Created the public GitHub repository at `https://github.com/samgo808/mk3.1`.
- Connected the local repository using the remote name `origin`.
- Pushed the local `main` branch to `origin/main`.
- Configured the local branch to track `origin/main`.

### Initial commit

- Commit: `69066c3`
- Message: `Initialize Makoto-kun 3.1 architecture`
- Files: 24
- Insertions: 2,129

### Verification

- The pre-commit public-release check passed.
- The push completed successfully.
- Local and GitHub `main` both resolved to commit `69066c387e6bde31df8f2a3d40cfa60caecdf147`.
- `git status` reported that the branch was up to date with `origin/main`.
- The working tree was clean after the push.
- Only `.gitkeep` placeholders were committed under `raw/`; no raw source documents were uploaded.

## Current status

### Complete locally

- [x] Directory structure
- [x] Course-year separation
- [x] Agent instruction files
- [x] README
- [x] Build log
- [x] Local Git repository on `main`
- [x] `.gitignore` protecting raw source documents
- [x] Public-release policy
- [x] Publication classification rules
- [x] Versioned pre-commit guard
- [x] MK3.1 vector-table name selected
- [x] Initial local Git commit
- [x] Public GitHub repository created
- [x] Local repository connected to `origin`
- [x] Initial `main` branch pushed and verified

### Configured but not verified

- [ ] Loader targeting `makoto_wiki_vectors_v31`
- [ ] Creation and population of the new vector table
- [ ] Chat retrieval from the new vector table

### Not yet completed

- [ ] Compile and publicly review the first wiki pages
- [ ] Load `SOUL.md`, `MIND.md`, and `BODY.md` into the n8n AI Agent
- [ ] Configure isolated student session IDs
- [ ] Test retrieval, email, and calendar behavior
- [ ] Complete an end-to-end Discord test
- [ ] Decide whether to support Slack
- [ ] Build the student web interface
- [ ] Define chat-history privacy and retention rules

## Next step

Connect the MK3.1 Wiki to Vector Store Loader to `https://github.com/samgo808/mk3.1`, verify that it reads only eligible `wiki/**/*.md` pages, and confirm that it writes only to `makoto_wiki_vectors_v31`.
