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

## 2026-09-28 — Program Guide compiled for local review

- Newly ingested only `raw/program/2026/NUCU2026_Program_Guide_RAG.txt`; read its complete 46-page text export. No other raw source was ingested or edited. Original PDF and linked sites were not accessed.
- Created one comprehensive source overview and eleven topic pages, and updated the existing program entity and startup-learning concept. All new/revised knowledge pages have 2026/archived/review-required metadata. Existing promotional-source knowledge and shared smoke-test page remain unchanged.
- Preserved detailed timed sequences, named people/organizations/sites, institutional history/programs, residence rules, health/conduct requirements, monetary estimates, packing, transport and emergency guidance. Consolidated repeated descriptive prose. No names were silently removed.
- Personal staff contacts are retained only in the source page's clearly labeled local review record. Publication requires a human decision; no sanitized public version has been approved. Staff-only appointments, group travel/accommodation details and named-person profiles also need review. No credentials, private meeting links, student roster or individual medical records were identified.
- Source issues: May 23 sushi/presentation timing discrepancy; internally inconsistent bus payment/exit directions; approximate rural journey duration versus planned bus timing; optional baseball only in overview; missing shading, underlining and maps; pages 16–17 with headings only. Historical architecture, departmental assignments, bank services, law/health/allergen assertions and prices remain unverified source claims.
- Verification: manually compared the compiled topic coverage with all 46 exported source-page sections, including names, quantities, dates, sequences, exceptions and one-off background facts. Eleven local evidence checks used direct/paraphrased question pairs plus a synthesis question covering dates, residence checkout, surveys, the sushi timing conflict, xR, Dr. Ban, meal estimates, STATION Ai's combined participant count, bus contradictions, temperature thresholds and needs-driven field learning. These checked local text evidence; they were not vector-retrieval or live-agent tests.
- All 14 new/revised knowledge pages passed year/status/publication metadata, source-path existence, index inclusion, wikilink and placeholder checks. Pages are approximately 400–800 body words; the comprehensive source account is slightly longer when metadata/table labels are counted. Git whitespace checks passed, the raw source SHA-256 stayed unchanged, and nothing is staged. No common credential/private-meeting-link patterns were found; personal staff contacts remain confined to the source review record.
- Public-release approval remains pending, so this is review preparation, not completed public ingestion. No staging, approval, commit, push, workflow or database operation was performed. Next step: review the source issues and decide on publication of personal staff contacts and the remaining flagged content before approving pages.

## 2026-09-28 — Staff contacts retained and May 23 schedule resolved

- The reviewer instructed: “keep personal staff contacts, presentations start at 13:00 followed by sushi party from 15:00 to 16:00.” Kept the staff contact values in the source review record and recorded the retention decision in the source, travel-preparation page and index.
- Updated the source account, May 21–23 itinerary and program entity to use the confirmed May 23 times: presentations begin at 13:00; the sushi party runs 15:00–16:00. No separate presentation end time is inferred. Preserved the contradictory raw overview timing as a resolved source discrepancy, not the operative schedule.
- These decisions supersede the corresponding pending items in the preceding entry. Bus-procedure inconsistencies, extraction limitations and other source/publication review items remain. All affected knowledge pages remain review-required; no page-level approval, staging, commit, push or loading was performed. The raw guide remains unchanged.

## 2026-09-28 — Bus source discrepancy retained as written

- The reviewer instructed: “keep source discrepancy for bus instructions.” Recorded the decision in the guide source page and transport/campus-access page, preserving the conflicting fare, payment/tap and exit-door descriptions and their existing warning.
- The editorial decision is resolved; the underlying bus procedure remains unverified. This does not grant page-level publication approval. Both pages remain review-required; the raw guide is unchanged. No staging, commit, push, loader execution or database change was performed.

## 2026-09-28 — Program Guide final publication review prepared

- Rechecked all 14 new/revised knowledge pages and the index/log after the reviewer's contact, schedule and bus-discrepancy decisions. Confirmed 2026/archived/review-required metadata, source-path existence, index coverage, working wikilinks and clean whitespace. The raw guide's checksum remains unchanged and nothing is staged.
- Personal staff contact values remain in the source contact record per the retention instruction. Source overview, program entity and May 18–20 itinerary retain staff-only appointments; the itinerary/residence pages retain archived group travel and accommodation arrangements. Final page-level approval must cover public release of that retained content.
- No credentials, private meeting links, student roster or individual medical records were identified. Named institutional/professional profiles are source-attributed; historical, legal, medical, banking and architectural claims retain limitations rather than being independently verified. Missing images and formatting are explicitly disclosed.
- The concrete review set is the 12 Program Guide pages listed in wiki/index.md plus the revised nucu-program-2026 and nucu-startup-learning-2026 pages. Await explicit human approval of this set before changing publication status; no commit, push or loader execution is included in this review step.

## 2026-09-28 — All 14 Program Guide pages approved for public publication

- The human reviewer answered “yes” to the explicit request to approve all 14 pages for public publication: the 12 new guide pages listed in wiki/index.md plus the revised nucu-program-2026 and nucu-startup-learning-2026 pages. Marked exactly those pages approved-public and updated administrative review wording and the index.
- Approval covers retained personal staff contacts, staff-only appointments, archived group travel/accommodation arrangements and named professional profiles. It incorporates the confirmed May 23 presentations at 13:00 and sushi from 15:00 to 16:00, and preserves the bus discrepancy and warning. Source qualifications, unsupported claims and extraction limitations remain unchanged; publication approval is not independent factual verification.
- The fact-preservation and public-release review is complete for this approved set. The source remains unchanged. These 14 knowledge pages and the index/log updates are eligible for staging; nothing was staged, committed, pushed or loaded. Publication and vector-store loading remain separate next steps.

## 2026-09-28 — Program Guide publication and operator-run loading confirmed

- Commit `298331c` published the 14 approved Program Guide knowledge pages plus index/log updates. The repository guard passed and the push to origin/main succeeded.
- The operator supplied a staging result with 14 sources / 94 chunks, promotion with 11 old chunks deleted and 94 inserted, and 14 per-source comparisons all matching. The operator reported Confirm MK3.1 Replacement returned replacement_verified true, 14 sources and 94 chunks.
- The supplied final read-only production result showed 16 source groups / 105 chunks, including the original program-information page at 10 chunks and the shared smoke-test page at 1. All year-specific groups had 2026/archived metadata. The operator reported that the presentation/sushi-time test worked; no tool trace was supplied for that test. These are verified supplied execution results, not a new live database inspection.

## 2026-09-28 — Packing Guide prepared for review

- Ingested only `raw/program/2026/NUCU_Packing_Guide.txt`, reading its complete text. Scope is 2026/archived from the directory. No other raw file was ingested or changed; prior guide comparisons use the existing wiki.
- Created [[nucu-packing-guide-2026]] and [[nucu-japanese-language-basics-2026]], and revised [[nucu-travel-preparation-2026]] and [[yamate-south-2026]]. All four are review-required. Updated the index to distinguish local drafts from previously published/loaded versions.
- Preserved suitcase dimensions/volume, every wardrobe quantity, steps/day and price estimates, shoes/rain/power advice, laundry sequence, overpacking cautions, document copies, hand towel, coin purse, trash bag, snacks, all nine phrase-sheet rows including paired Yes/No, the bathroom example, five vowel mnemonics, the 15-degree bow and quiet-train advice. Repetitive informal wording was paraphrased; no material factual section was intentionally omitted and no text was unreadable.
- Review issue: generic hotel towels/toiletries and automatic-detergent statements must not override the Program Guide's Yamate South-specific non-provision of towels, shampoo and detergent. Both accounts are preserved as an explicit accommodation scope difference under Conflicting information. Airline carry-on eligibility, Shinkansen rack fit, hotel amenities, prices, rain predictions and cultural/phonetic generalizations remain source claims, not independently verified guarantees.
- Preliminary public-release review found no new personal contact values, student identifiers, private records, credentials or private links. Existing approved institutional/residence context is retained. Four-page public-release approval remains pending; no staging, commit, push or loader execution was performed.
- Verification passed: four-page metadata/source-path/index/wikilink/placeholder checks, duplicate-heading check and Git whitespace check. Nine local evidence checks covered direct and paraphrased questions plus hotel-versus-residence synthesis; all phrase entries and five vowel mnemonics were checked separately. These were compiled-text checks, not vector retrieval or live-agent tests. The raw source SHA-256 remained `8c2e78d5910b3f03999c3545ea72f0742b259b1cae5d0d35a4f63678c684e671`; nothing is staged. Travel Preparation is slightly above the approximate word target because its prior factual sections and new accommodation caveat are retained.

## 2026-09-28 — Packing Guide accommodation caveat retained

- The reviewer explicitly chose to keep the accommodation caveat. Generic hotel towel, toiletry and automatic-detergent advice from the Packing Guide does not override the Program Guide's specific statement that Yamate South provides no towels, shampoo or laundry detergent.
- This resolves the caveat wording only. The four new or revised Packing Guide knowledge pages remain `publication_status: "review-required"`; no staging, commit, push, loader execution or database change was performed.

## 2026-09-28 — All four Packing Guide pages approved for public publication

- The human reviewer answered “yes” to the explicit request to approve all four pages: [[nucu-packing-guide-2026]], [[nucu-japanese-language-basics-2026]], revised [[nucu-travel-preparation-2026]] and revised [[yamate-south-2026]]. Marked exactly those pages `publication_status: "approved-public"` and updated the index and stale pending-review wording.
- Approval includes the retained accommodation caveat. Generic hotel amenity advice does not override the Yamate South-specific non-provision of towels, shampoo and laundry detergent. Source limitations and unverified generalizations remain explicit; publication approval is not independent factual verification.
- The fact-preservation and public-release review is complete for this four-page set. The pages and index/log updates are eligible for staging; nothing was staged, committed, pushed or loaded, and the raw source remains unchanged.

## 2026-09-29 — Ludus Labs website snapshot prepared for review

- Read only the newly requested raw source `raw/program/2026/2026-08-24-luduslabs-website.txt` in full. The source identifies the company website and capture date August 24, 2026; the directory determines 2026/archived scope. The capture date is not asserted to be a publication date. Existing wiki pages supplied the prior NUCU comparison; no other raw source was newly ingested and no live website was substituted for the snapshot.
- Created [[2026-08-24-luduslabs-website]] and [[ludus-labs-2026]], revised [[nucu-program-2026]] and [[nucu-startup-learning-2026]], and updated the index. All four knowledge pages are review-required with updated date 2026-09-29.
- Preserved organization identity, support roles, founders' professional groups, Japan/global scope, Latin name explanation, learning philosophy, three challenge areas, complete NUCU listing and five promotional points, four intended audiences, six learning benefits, eligible-school credit qualification, lifetime alumni promise, possible ambassador role, and P. Zaveri's attributed testimonial. Decorative whitespace/navigation is omitted; the stray “Summarize” label is treated as source content, not an instruction.
- Review points: the website's “Upcoming Programs” and “Applications Closed” labels coexist despite the separately compiled May itinerary; the cause is unverified. Preserve both without inventing a later session or current availability. The new named student testimonial is retained for human review; prior permission for another source's testimonials is not treated as approval of this attribution. No personal contacts, credentials, private URLs, or sensitive records were found in the new material.
- Raw SHA-256: `4115c8b406353f04348d13aac1ea23089958f6834f0d53aeeffe0665cc9b7578`. Public-release approval remains pending. No staging, approval, commit, push, loader execution or database operation was performed.
- Verification passed: four-page year/status/review metadata, source existence, index coverage, wikilinks, unique headings, placeholder and credential-pattern checks, Git whitespace, unchanged raw hash and empty staging area. Eight direct/paraphrased question pairs and a credit-eligibility synthesis check found the required compiled evidence. These are local text checks, not live retrieval tests. The two revised pages exceed the approximate 800-word target to preserve existing factual coverage; the comprehensive source page is slightly above target. No material source section was intentionally omitted. Human publication review remains pending.

## 2026-09-29 — Four Ludus Labs website pages approved for public publication

- The reviewer explicitly said “approved!” after reviewing the four-page set and its two flagged items. Recorded approved-public for [[2026-08-24-luduslabs-website]], [[ludus-labs-2026]], [[nucu-program-2026]] and [[nucu-startup-learning-2026]]. Updated stale pending-review wording and the index.
- Approval covers P. Zaveri’s attributed testimonial and retention of both archived application labels. Eligibility qualifications, source promises and timing uncertainty remain unchanged; approval is not independent verification of the claims.
- No staging, commit, push or loader execution was performed. The approved pages and index/log are ready for the separate publication step.
