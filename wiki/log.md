# Wiki Ingestion Log

## 2026-09-28 — NUCU 2026 program information prepared for review

- Read only `raw/program/2026/nucu_program_info.txt` as the source for this ingestion; the raw file remains unchanged.
- Created [[nucu-program-info-2026]], [[nucu-program-2026]], and [[nucu-startup-learning-2026]] with `course_year: "2026"`, `status: "archived"`, and `publication_status: "review-required"`. Updated the index, including its existing shared smoke-test page.
- Fact-preservation review compared every source section with the compiled pages, including names, three credits, two micro-credentials, 15 days, March/May timing, four challenge areas, named methods/topics, five promotional reasons, 11 testimonial passages, and four advice passages. Direct, paraphrased, and synthesis retrieval checks used the local wiki text; no vector retrieval or runtime test was performed.
- Preserved uncertainties: no reliable source date, exact itinerary, named host companies/judges, or formal credential award conditions; demographic prediction is unsupported. Anonymous testimony and advice are paraphrased; no material factual section was intentionally omitted, and no unreadable material or internal source conflict was found.
- Preliminary public-release inspection found no credentials, private links, personal contact details, or student identifiers in the new content. The source and concept pages preserve anonymous testimony/advice with unclear publication permission; these require human judgment. The entity page contains public institutional names and archived program descriptions, but also remains unapproved.
- Review preparation only: public-release approval is pending, so ingestion is not declared complete for publication. No approval, staging, commit, push, loader execution, or database change was performed. Next step: human review when requested.

## 2026-09-28 — Testimonial and advice publication permission confirmed

- The human reviewer stated: “Testimonials and advice may be published publicly.” This resolves the testimonial/advice permission flag for the three NUCU 2026 pages.
- Updated the source, entity, and concept pages to record that permission separately from the raw source evidence. The original ingestion entry above remains a historical record.
- All three knowledge pages remain `review-required`; this permission does not resolve the unsupported demographic prediction or grant final page-level approval.
- The raw source remains unchanged. No staging, commit, push, loader execution, or database change was performed.

## 2026-09-28 — Demographic caveat retained as written

- After being shown the unsupported population-prediction claim and its existing warning, the human reviewer instructed: “keep as written.” The demographic claim and warning remain unchanged in all three NUCU 2026 pages; no external verification or factual correction was requested or performed.
- This resolves the wording decision. Testimonial and advice publication permission was recorded in the preceding entry.
- All three pages remain `publication_status: "review-required"` under the earlier instruction to stop before page approval. No staging, commit, push, loader execution, or database change was performed.

## 2026-09-28 — Three NUCU 2026 pages approved for public publication

- The human reviewer explicitly instructed: “approve all three pages.” Recorded `publication_status: "approved-public"` for [[nucu-program-info-2026]], [[nucu-program-2026]], and [[nucu-startup-learning-2026]]. Updated the index and removed outdated pending-approval wording from the pages.
- Approval includes the previously authorized anonymous testimonials/advice and retention of the demographic claim with its existing unsupported-claim warning. The warning and factual content remain unchanged; publication approval does not verify the demographic prediction.
- Final public-release inspection of the five changed wiki files found no prohibited credentials, private links, private contact details, or student identifiers. Institutional names are public; testimonial permission is recorded. Fact-preservation checks from preparation remain applicable because this approval changes only review status and related administrative wording.
- Local ingestion and publication review are complete. The raw source remains unchanged. The five wiki files are eligible for staging, but nothing was staged, committed, pushed, or loaded. Publication and vector-store ingestion remain separate future actions.

## 2026-09-28 — Three NUCU 2026 pages published and loaded

- The operator's terminal screenshot confirmed commit `e763d60`, a successful push to `origin/main`, and a clean synchronized working tree. This supersedes the pending-publication state recorded above.
- The operator restricted the loader to the three approved NUCU page paths and validated all three pages. A Loop Over Items node was added so pages would be sent individually to the PGVector node; the corrected wiring was verified visually. The Wipe Wiki node remained disabled.
- A read-only SQL query before loading showed only [[mk31-loader-smoke-test]], stored as one chunk. After the operator's manual load, the same query showed [[nucu-startup-learning-2026]] with 6 chunks, [[nucu-program-2026]] with 5 chunks, [[nucu-program-info-2026]] with 10 chunks, and [[mk31-loader-smoke-test]] with 1 chunk. Total: 22 chunks.
- The three NUCU source groups had `course_year: "2026"` and `status: "archived"`; the smoke-test group remained `course_year: "shared"` and `status: "evergreen"`.
- The operator supplied a chat answer that correctly returned three CU credits, both micro-credential providers, and the expected source-page citation. The operator also reported the expected responses for an unanswerable 2027 travel-date question and the unsupported population-prediction question.
- Verification limit: database storage and metadata were confirmed from the supplied SQL result. The answers passed content checks, but the underlying PGVector tool traces were not inspected. Actual retrieval evidence, embedding-model compatibility, and enforced year filtering therefore remain to be verified separately.
- The current loader is insert-only and temporarily restricted to these three paths. It must not be rerun unchanged because duplicate prevention or a deliberate replacement procedure has not yet been added.

## 2026-09-28 — PGVector retrieval trace confirmed

- The operator supplied the PGVector tool response for the tested BAIM 3300 credits and micro-credentials question. The tool returned two relevant chunks rather than an empty retrieval result.
- One chunk came from [[nucu-program-2026]] and contained the archived 2026 program identity and three-credit description. Its metadata identified `source: "wiki/entities/2026/nucu-program-2026.md"`, `page_type: "entity"`, `course_year: "2026"`, `status: "archived"`, and `publication_status: "approved-public"`.
- The second chunk came from [[nucu-program-info-2026]] and contained the exact three-credit and two-provider passage, including CU Innovation & Entrepreneurship and Ludus Labs. Its metadata identified `source: "wiki/sources/2026/nucu-program-info-2026.md"`, `page_type: "source"`, `course_year: "2026"`, `status: "archived"`, and `publication_status: "approved-public"`.
- This confirms retrieval of relevant compiled content with the expected source and year metadata for the tested question. It does not by itself prove metadata-filter enforcement for every query or verify the separate 2027 and unsupported-claim responses at the tool-trace level.

## 2026-09-28 — Duplicate-safe staged replacement verified

- Reworked the operator's n8n loader so the PGVector insertion node writes to `makoto_wiki_vectors_v31_staging` rather than directly to production. The preparation step creates the staging table from the production schema when needed and truncates only staging at the start of a run. The production Wipe Wiki node remained disabled.
- Added checks requiring the staging table to contain exactly the three selected source paths before promotion. A staging-only preflight passed with 3 sources and 21 chunks: [[nucu-startup-learning-2026]] 6, [[nucu-program-2026]] 5, and [[nucu-program-info-2026]] 10.
- Added one atomic SQL promotion statement that deletes production chunks only for source paths present in staging and inserts their staged replacements. If insertion fails, PostgreSQL rolls back the matching deletions.
- Added post-promotion SQL and code checks comparing staging and production chunk counts for every selected source. The completed workflow returned `replacement_verified: true`, `verified_sources: 3`, and `verified_chunks: 21`.
- A final read-only production query returned the expected four source groups and 22 total chunks: the three NUCU pages at 6, 5, and 10 chunks, plus the unchanged shared smoke-test page at 1 chunk. The replacement created no duplicate source chunks.
- The inspected recovery export is `MK3.1 Wiki to Vector Store Loader-2.json`, SHA-256 `c81f07024b13ee3450e88dcac608b509414efce7531be7c681105d139b362f40`. It was inactive, contained no obvious secret values, and preserved the exact three-page selection and disabled production-wipe node.
- The staging table retains the latest 21 staged chunks as a recovery snapshot until the next run truncates staging. The selected path list remains intentionally explicit and must be updated for a different ingestion set.
