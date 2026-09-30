---
type: "source"
title: "NUCU Session 12: Sprint Debrief, RAG and AI Coding — 2026-04-07"
course_year: "2026"
status: "archived"
publication_status: "approved-public"
sources:
  - raw/curriculum/2026/nucu_lecture_session12_4_7_2026_CUT.txt
updated: "2026-09-30"
tags:
  - "design-sprint"
  - "rag"
  - "ai-coding"
  - "japanese-language"
  - "2026"
---

# NUCU Session 12: Sprint Debrief, RAG and AI Coding — 2026-04-07

The archived April 7, 2026 BAIM 3300 session, “Design Sprint Debrief + n8n & Claude Code deep dives,” combines Samuel Goodman's technical demonstrations, international-team reflection and Japanese phrases. **Sawako Tanaka** joins the site-visit and teamwork discussion. The transcript records **Makoto-kun 2.3**, a **3.0 proposal**, and tentative 2026 activities; it does not establish current MK3.1 deployment or a final itinerary.

## Makoto-kun's two-phase RAG explanation

The lecture contrasts a **custom GPT (1.0)** and a brochure-text **n8n 2.0/2.1** version with **2.3 using RAG, retrieval-augmented generation**. The instructor describes the earlier setup as too dependent on exact wording and regurgitating text. Those are observations about his versions, not universal limits of custom GPTs or plain-text context.

The ingestion demonstration proceeds as follows:

1. Prepare a lecture transcript, removing pre/post-class conversation from that historical upload.
2. Ask ChatGPT for topic keywords, then add headings and topics. **Igor**, inspired by *Young Frankenstein*, is the instructor's humorous assistant persona.
3. Upload the text to the **Nuku Docs GitHub repository** and use its raw-text URL in an **n8n HTTP node** (n8n is transcribed “NAN”).
4. Run the loader to split text into chunks, generate embeddings and store them in a vector database.
5. Inspect node output and run a count query; the demo reports **71 items** and **347 total database records**, up from a recollected count in the 200s. These are historical observations, not today's wiki or vector counts.

The demonstrated document is the **February 17 session 6 / Reiwa** lecture. Spoken references also call it session one and describe it as after World War II. Its supplied metadata and actual content identify session 6; the contradictory labels are preserved here rather than changing the source.

In the query phase, **Discord → webhook → AI agent → model and vector-store retrieval → Discord reply** is the high-level path. The instructions describe a quirky digital intern using its knowledge base rather than web search, with email offered for missing information. A mock Gmail connection and calendar function appear, but calendar/API access may have expired. No credential, private endpoint or calendar link is reproduced.

The first query, **“When did we talk about Reiwa?”**, fails with an assertion that it had not been discussed. A question about **overwork / karoshi** succeeds, locating **session 6, February 17, 2026**. Follow-up summary requests work imperfectly. A separate example about **Karpathy**, transcribed “Carpathian,” initially lacks a date until transformer context elicits **session 5**. **MITI**, transcribed “MIDI,” is resolved in course context as Japan's Ministry of International Trade and Industry rather than an unrelated acronym. Students are asked to mention the bot and try it in the off-topic room for shared feedback; DMs are another interface. This is not proof that all questions are reliably answered.

## Embeddings explanation and technical limits

The class uses **king/man and queen/woman** word analogies, a three-dimensional visualization and dot products **+4, −4 and 0**, with **90 degrees** representing orthogonality. The instructor acknowledges embeddings have more than three dimensions. The useful intuition is that numeric representations support similarity search and that queries can be embedded to retrieve related text.

The explanation also conflates **tokenization**, **document chunking**, **embedding similarity** and **next-token generation**. A language model does not generally generate each next word by fetching it from the application's external vector database. Antonyms do not necessarily have negative embedding similarity; those dot products are illustrations, not measured results. RAG can supply relevant chunks as context to a generator, but it does not guarantee retrieval or truth. The observed Reiwa failure despite successful upload is an important limitation, not a reason to claim the source was absent.

Compared with sending a whole corpus each time, selected chunks can reduce context. RAG still consumes tokens and can fail through retrieval or context selection. The class's broad efficiency comparisons lack measurements. See [[nucu-makoto-rag-demonstrations-2026]].

## Planned 3.0 and personal knowledge systems

**Makoto-kun 3.0** is proposed as a possible **OpenClaw** agent/second-brain system, not shown as deployed. The idea is to collect documents, screenshots, podcast audio and reports, compile a linked wiki, and retrieve personal knowledge later. A student discusses an unfinished **Obsidian + Claude Code** experiment, describing linked notes as a “neural web”; that phrase is a metaphor, not proof of a neural-network database. The transcript also says “Open Cloud/OpenClaude,” apparently referring to OpenClaw, but naming remains uncertain.

## Claude Code, deployment and small applications

The instructor runs **Claude Code on Linux** and distinguishes a local coding assistant from a general web chat. The live website task changes **“Apply now” to “Applications closed.”** Claude edits local files, receives permission to edit and push, sends changes to **GitHub**, and **Vercel** builds the deployment. The class watches the build and refreshes the website to confirm the new text. This is a demonstrated outcome for that website at that time, not authorization to edit or publish today's site.

**Railway** is described as **PaaS, platform as a service**, hosting n8n, a vector database and a Discord-related Makoto service. **SaaS** is mentioned for comparison. Vercel hosts websites; calling it a database in passing is imprecise. An OpenClaw cloud experiment is still exploratory.

Other demonstrations include a possible **Longmont senior tech-support business**, reportedly set up in an evening/weekend for **under $30**, using a website, Google phone-number forwarding/masking and Google Workspace email. No contact values are reproduced. A personal driving-hours application named **“Team Drive”** in the transcript records trips, totals and night hours and can export a DMV log. Build-time estimates vary between **less than one hour** and **less than two hours**. **[Redacted: a minor's age and personal driving-log status.]** The point is making a small tool for a specific need; self-building alone does not prove privacy, safety or official DMV acceptance.

A disputed business story concerns an **unnamed $1.8 billion healthcare company**, said to be built by two brothers using automated marketing/back-office tools and selling drugs transcribed “Ozon/Zempic.” **Hims** is mentioned as a competitor. A student reports subsequent allegations about fabricated doctors and possible financial problems; the instructor says he had not seen that follow-up and requests it. No cited article or evidence establishes either the valuation or alleged misconduct, and the company is not guessed. The claim that fewer than **five people** could build a **trillion-dollar company** is speculation, not an achieved result. The transferable point is lower prototyping/admin costs, subject to verification and trust.

## Sprint debrief and the actual challenge

The brief is **“As a global team, design a tech-enabled solution that helps societies adapt to demographic change.”** Students should target labor shortages, aging and related needs, not promise to reverse population collapse. Some societies may adapt to a smaller population; Japan is framed as a learning opportunity for problems that may also affect the US.

The four-week virtual sprint had **run out of time before selecting a direction**. Nagoya students had finished the virtual program and resumed classes; participation and time-zone differences made consensus difficult. The instructor contrasts proceeding alone with actively seeking teammates' views, without establishing those as fixed national traits.

Teams are asked to reach out through **Discord** or existing agreed contact channels, request missing solution sketches if feasible, and organize **asynchronous voting**. In **Miro**, green dots create a **heat map** of preferred sketch elements/ideas. The example uses about **20 dots**, giving **five** to one sketch, none to another and **10** to a favorite. A **red star / supervote** selects the direction. The exact per-person allocation and tie-breaking rules are not established. Reach out even if teammates do not reply; choose a useful direction while remaining willing to **pivot in Japan**. Voting instructions are promised in Discord.

## Previous-year video versus prospective 2026 visits

The video is explicitly of **last year's trip**, not evidence that each site was visited in 2026. It shows the university **xR Center** and VR medical/surgery applications; **Nagoya University Hospital** market-research conversations with patients/caregivers; Hasegawa's lecture; entrepreneurs; **STATION Ai** collaboration space; an autonomous-vehicle professor/lab; and **Idea Stoa**, also transcribed “Idea Stow,” as student collaboration space. The already recorded reviewer correction identifies Idea Stoa at **NIC, Nagoya University**; this transcript does not create a different “Idea Store” venue.

Rural examples include a **LiDAR-equipped golf-cart-like autonomous vehicle** in a hilly town, contrasted with the resources required for **Waymo**; a former school used as a community/lecture space; a rural clinic; a senior home; a mayor discussing the town and hearing team ideas; formal business-card exchanges; and a drone startup that prohibited interior photos because of R&D. The transcript does not name these rural sites or the drone company, so they are not matched speculatively to other wiki entities. Final pitches, Q&A, judges' feedback, a best-team selection and certificates are shown at Idea Stoa.

The instructor contrasts **five participants last year with 20 this year**, and a standalone experience with integration into a course. **Tanaka-sensei** is helping arrange visits. A survey and site descriptions are planned; students should request broad areas such as healthcare or robotics. A larger final-pitch venue is possible, not confirmed. No patient-survey procedure here authorizes unsupervised research.

## Other announcements and Japanese practice

A planned epistemology lecture is postponed. **David Deutsch's The Beginning of Infinity (2011)** is recommended as influential on the instructor's thinking about knowledge creation; the book is not said to be about LLMs. Two volunteer work groups are proposed: **NUCU Code**, an ethics/ambassadorship document students would sign before Japan, and **tech support**. These are dated proposals, not a newly adopted code.

The practiced expressions are **itadakimasu** before a meal; **gochisosama**, more politely **gochisosama deshita**, after; **hajimemashite** on first meeting; **yoroshiku onegaishimasu** after an introduction, glossed as “please take care of me” with a wider relational meaning; **dozo** when offering something; **domo** for casual thanks; and **gambatte**, transcribed “gambate,” for encouragement/do your best. The lecture distinguishes offering **dozo** from request **kudasai**, and uses a chair and convenience-store change as examples. These are beginner contextual glosses, not interchangeable translations for all situations. See the revised [[nucu-japanese-language-basics-2026]].

## Conflicting information and publication review

Retain the conflicting session labels, app build-time estimates, technical conflations and unverified healthcare-company story. Missing slides, videos, article links and voting details are not reconstructed. The human reviewer approved publication of the retained family application, prospective senior-support business, internal team coordination and volunteer groups on 2026-09-30. Incidental student identities and private chatter are excluded from the conceptual account; identifying minor details are redacted. See [[nucu-design-sprint-collaboration-2026]] and [[nucu-ai-assisted-prototyping-2026]].

Course map: [[nucu-course-architecture-2026]].
