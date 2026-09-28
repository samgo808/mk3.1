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
- [ ] Configure and document the active program year before student deployment
- [ ] Enforce `course_year` during retrieval through metadata filtering or separate year-aware retrieval tools
- [ ] Test that 2027 questions cannot silently return 2026 policies and that ambiguous year-sensitive questions trigger clarification
- [ ] Test retrieval, email, and calendar behavior
- [ ] Complete an end-to-end Discord test
- [ ] Decide whether to support Slack
- [ ] Build the student web interface
- [ ] Define chat-history privacy and retention rules

## Next step

Connect the MK3.1 Wiki to Vector Store Loader to `https://github.com/samgo808/mk3.1`, verify that it reads only eligible `wiki/**/*.md` pages, and confirm that it writes only to `makoto_wiki_vectors_v31`.

---

## 2026-09-28 — First NUCU 2026 wiki load and initial chat checks

**Status:** COMPLETE for publication and first load; PARTIALLY VERIFIED for retrieval

### Built and changed

- Compiled, publicly reviewed, committed, and pushed three pages from `raw/program/2026/nucu_program_info.txt`: the comprehensive source account, program entity, and startup-learning concept.
- Published the approved pages in commit `e763d60`.
- Restricted this loader run to the three approved page paths so the existing smoke-test record would not be inserted again.
- Added a Loop Over Items connection around Postgres PGVector Store so pages would be sent individually for insertion. The corrected loop wiring was verified visually.
- Kept Wipe Wiki disabled and retained `makoto_wiki_vectors_v31` as the destination table.

### Verification

- Operator screenshots confirmed a successful pre-commit check, commit, push, three validated loader items, and corrected loop wiring.
- Before loading, a read-only SQL result showed one stored chunk for `wiki/concepts/shared/mk31-loader-smoke-test.md`.
- After loading, SQL showed four source groups and 22 total chunks: startup learning 6, program entity 5, source account 10, and smoke test 1.
- The three new groups carried `course_year: "2026"` and `status: "archived"`; the smoke test remained `course_year: "shared"` and `status: "evergreen"`.
- A supplied chat answer correctly returned three CU credits, CU Innovation & Entrepreneurship, Ludus Labs, and the expected 2026 source citation.
- The operator reported that fresh-chat tests did not invent 2027 travel dates and correctly treated the source's population prediction as unsupported.
- A fresh workflow export, `MK3.1 Wiki to Vector Store Loader-2.json`, was inspected without execution. It confirmed the inactive workflow, disabled Wipe Wiki node, exact three-page filter, approval validation, loop wiring, insert mode, and `makoto_wiki_vectors_v31` destination. No obvious secret values were found. Export SHA-256: `03c8ffbec35b31c8663b38949bf1bb93c9ef378d7535f1b94ece5803f9889845`.

### Remaining uncertainty

- The chat answers passed content checks, but the PGVector tool traces were not inspected. The answers alone do not prove which records were retrieved.
- Active agent-table configuration, embedding-model compatibility, and metadata-filter enforcement were not independently verified in this step.
- Loading `SOUL.md`, `MIND.md`, and `BODY.md` into the runtime, session isolation, email/calendar behavior, and end-to-end student interfaces remain unverified.
- The exported loader is insert-only and can create duplicates if rerun. Its temporary three-path selection is not a general update strategy.

### Next planned step

Inspect a chat execution's PGVector tool trace to confirm retrieved content and source/year metadata, then design duplicate-safe updates before the next ingestion.

---

## 2026-09-28 — PGVector retrieval trace verified

**Status:** VERIFIED for the tested BAIM 3300 retrieval

### Evidence

- The operator supplied the PGVector tool response for the BAIM 3300 credits and micro-credentials question.
- The tool returned a chunk from `wiki/entities/2026/nucu-program-2026.md` containing the program identity and three-credit description.
- The tool also returned the decisive chunk from `wiki/sources/2026/nucu-program-info-2026.md`, containing three CU academic credits and the two providers: CU Innovation & Entrepreneurship and Ludus Labs.
- Both chunks carried the expected metadata: `course_year: "2026"`, `status: "archived"`, and `publication_status: "approved-public"`. Page type and title also matched their repository paths.
- The agent's answer was therefore grounded in relevant PGVector results for this test rather than merely matching the expected wording by coincidence.

### Limits

- This trace verifies one direct-fact retrieval. It does not prove that course-year metadata is enforced as a database filter on every request.
- Tool traces were not supplied for the 2027 travel-date or unsupported population-prediction tests; those remain answer-level behavior checks.
- The chat workflow's table-name field and embedding-model setting still need direct configuration inspection or a fresh workflow export for a complete configuration record.

### Next planned step

Design and implement duplicate-safe page replacement before another loader run, then capture a fresh loader export and test the replacement path with a controlled page update.

---

## 2026-09-28 — Duplicate-safe staged replacement

**Status:** COMPLETE and VERIFIED for the selected three-page replacement

### Built

- Added `makoto_wiki_vectors_v31_staging`, created from the production table structure and cleared at the beginning of each loader run.
- Redirected the loader's PGVector insertion node from `makoto_wiki_vectors_v31` to the staging table.
- Preserved the one-page loop so page text and metadata remain paired during embedding and insertion.
- Added a staging inspection and code gate that require exactly the three selected repository paths before production promotion.
- Added a single atomic promotion statement. It deletes production chunks only for staged source paths and inserts the staged replacements in the same PostgreSQL statement, so an insertion failure rolls back the corresponding deletions.
- Added production-versus-staging count verification and a final code gate that throws an error for missing sources, unexpected sources, or unequal chunk counts.
- Kept the broad production Wipe Wiki node disabled.

### Verification

- A staging-only preflight returned `staging_validated: true`, 3 expected sources, and 21 chunks.
- The complete replacement returned `replacement_verified: true`, 3 verified sources, and 21 verified chunks: startup learning 6, program entity 5, and source account 10.
- A final read-only production query returned the same three source counts plus the unchanged one-chunk shared smoke test, for 22 total chunks. No duplicate chunks were introduced.
- The corrected workflow export passed structural and secret-pattern checks. It was inactive, targeted `makoto_wiki_vectors_v31_staging` for insertion, retained the disabled production wipe, and contained the full staging, promotion, and verification path.
- Export filename: `MK3.1 Wiki to Vector Store Loader-2.json`
- Export SHA-256: `c81f07024b13ee3450e88dcac608b509414efce7531be7c681105d139b362f40`

### Operational behavior

- Production remains available if repository fetching, page validation, embedding, staging validation, or insertion fails before promotion.
- Promotion replaces only source paths present in the validated staging set; unrelated MK3.1 documents remain untouched.
- The staging table retains the latest successful 21 chunks as a recovery snapshot. The next loader run truncates staging before inserting its selected pages.
- The selected path list is explicit. A future ingestion must update both the selection and expected-path validation lists before execution.

### Remaining work

- Archive the corrected workflow export in an intentional local backup location.
- Commit and push this documentation update after review.
- Verify the chat workflow's table-name and embedding-model settings from a fresh export.
- Implement and test enforced course-year filtering rather than relying only on prompt behavior and returned metadata.
- Continue runtime-instruction, session-isolation, email/calendar, and student-interface testing.

### Next planned step

Review and publish this documentation update, then export and inspect the current `Makoto_kun 3.1` chat workflow before changing retrieval behavior.
