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
