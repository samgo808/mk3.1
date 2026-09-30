---
type: "source"
title: "NUCU Session 13: Travel Briefing and App Prototyping — 2026-04-14"
course_year: "2026"
status: "archived"
publication_status: "approved-public"
sources:
  - raw/curriculum/2026/nucu_lecture_session13_4_14_2026_CUT.txt
updated: "2026-09-30"
tags:
  - "predeparture"
  - "no-code"
  - "vibe-coding"
  - "team-collaboration"
  - "2026"
---

# NUCU Session 13: Travel Briefing and App Prototyping — 2026-04-14

The archived April 14, 2026 BAIM 3300 session is titled “Team Collaboration & FCQs,” but its recorded content chiefly covers Education Abroad preparation, team tasks and app prototyping with **Glide** and **Lovable**. **Professor Matt Brady** introduces **Sarah Westmoreland** of CU Education Abroad, then leads technical demonstrations and discussion. The source does not include a substantive FCQ procedure; no missing course-evaluation instructions are invented.

## Pitching and academic announcements

Brady describes a Silicon Valley pitch competition following a cohort begun in **January**: identify a target market, communicate a solution to a problem, and rehearse a **four-minute pitch**. He promises to demonstrate his pitch later; it is not delivered in this transcript. A proposal/final travel briefing and “last class” are announced for **next Tuesday**; the calendar implies April 21, but the source supplies no explicit date.

The **MSBA, MS in Business Analytics**, is promoted as a **10-month accelerated master's**. The price is compared with **40%** of the instructor's master's tuition **20 years earlier**, then roughly **20%** after an informal inflation adjustment. These are personal comparisons, not tuition quotes or ROI evidence. High rankings, scholarships and an assertion of automatic acceptance for Leeds students lack supporting criteria and are not admissions guarantees. **[Redacted: identifying alumni/family educational and employment-history anecdotes.]** Their teaching point is internship-to-career opportunity, not a verified placement rate.

The Human-Centered App's curated job board mentions **Pure Fishing** and an AI Club partnership, plus remote marketing/creative roles with Chicago-based **Rethink First**. A hiring contact is transcribed **Mark Alep**, spelling unverified. Brady offers recommendations and asks students to share opportunities. These are dated, personally curated leads, not verified current vacancies; the human reviewer approved publication of the retained contact relationships on 2026-09-30.

## Education Abroad preparation and responsibilities

Westmoreland identifies the **Education Abroad office at C4C** and says students can ask questions before, during or after travel. The course is graded as a regular CU course rather than through a separate overseas grading process. **Sam Goodman and Professor Brady** are the primary on-site contacts; **Tisha** is also described as accompanying the group. Their personal contact values are not reproduced.

The **myCUabroad health and wellness worksheet** is emphasized because accommodation needs may differ abroad. Students should complete outstanding acceptance tasks, read the accepted-student guide and faculty communications, check passport expiration, and plan phone use and packing. Personal health/accommodation information belongs in appropriate private channels; no completed form or student condition is included.

CU's risk-assessment process involves the **International Risk Committee** and coordination with the program provider if circumstances require itinerary changes. The speaker describes Japan as **Level 1** at that time and says no Japan-specific vaccination was required for the trip. Those are archived statements, not current destination or medical guidance; the referenced handout, links and full criteria are absent.

Medication discussion specifically names **Adderall** as prohibited in Japan and asks students to plan with their prescriber and Education Abroad if a usual medication cannot travel. General advice is original packaging/documentation and enough supply for the trip. The broad statement that most other prescriptions are fine is incomplete; this page does not establish import permission or replace current official requirements. No student's medication use is identified.

## Health insurance and emergency planning as described in class

The speaker distinguishes the program's **international health insurance** from campus CU insurance and from **travel/property insurance**. It is described as covering illness/injury and mental-health services while abroad, not routine preventive dental care, lost luggage, stolen phones or laptops. A common member identifier is mentioned but no number is present or copied. Exact policy wording, limits and exclusions are not supplied.

Coverage dates were to arrive by email, described as beginning a couple of days before arrival and ending a few days after the program. Extra personal travel may require other coverage. Those estimates are not the actual policy dates.

The classroom procedure is to notify Sam and/or Brady, obtain suitable medical care with their help, usually pay initially and submit a reimbursement claim. A **couple of hundred dollars** is offered as a rough expectation for manageable upfront expense, explicitly without Japanese cost expertise. Larger bills or overnight admission should involve Education Abroad coordinating with the insurer; this is not a guaranteed payment cap or promise of direct billing.

**International SOS / ISOS** and a **24/7 Education Abroad emergency contact** are discussed. Brady recommends redundant contact copies on phone, watch/laptop and paper in luggage or pockets, plus passport photo/paper copies, a card and some cash. Local staff should hear promptly rather than relying solely on parents relaying an emergency from far away. The transcript does not provide a complete emergency algorithm, local emergency number or policy terms.

The talk encourages early discussion of mental-health, interpersonal or roommate concerns, including during short programs. It describes therapist calls and more serious treatment as potentially within the program's cover; this remains the speaker's account. No individual health disclosure is compiled. For previous guide context see [[nucu-conduct-and-health-2026]] and [[nucu-travel-preparation-2026]]; those pages do not resolve missing policy detail here.

## Team tasks and information privacy

By **Friday**, teams are asked to finish voting, re-engage Nagoya teammates despite semester/time-zone differences, complete the **site-visit survey**, and supply **T-shirt sizes / dietary or allergy information**. The survey invites preferences among drone, healthcare, AI and other companies; visits may change even after mutual agreement because of logistics.

The source explicitly offers a privacy alternative to the shared spreadsheet: write **“DM”** in a cell and send Sam the information privately. Later, the app lesson says each user should see only their own personal details and switches to **sample exercise/sleep data** instead of building with the students' actual records. No roster, measurements, allergies or private message is copied here. The Friday reference remains archived, not a new task for current students.

## Glide: spreadsheet to an app

The introductory video presents a spreadsheet's rows, columns, formulas, tasks and roles as a base for collaborative, real-time mobile apps. In the demo, a spreadsheet/Google Sheet supplies **exercise and sleep sample data**. Exercises have dates, names, repetitions and sets, including “as many reps as possible.” Glide generates a first interface; **Pexels** stock images are retrieved using exercise keywords and an API integration, with an image column used in the layout. A new logged exercise is intended to fetch an image automatically. **Unsplash** is a comparison, not a required dependency.

A **Gemini** smart column then estimates calories from an exercise description for a “typical healthy person.” The instructor does not refine or validate that prompt; these are demonstration estimates, not fitness or medical measurements. **[Credentials are not reproduced; the transcript only describes obtaining API keys.]**

The architecture discussion separates **data**, **layout/UI**, **workflow/logic** and settings. A student's question about where data physically lives exposes the abstraction: the lecturer says it is behind Glide's platform, not that the vendor has no documented storage policy. Desire for more control, export or a different backend such as **SQL Server, MySQL or Convex**, and more customized UI than lists/cards, motivates moving beyond no-code. **Airtable, Monday.com, Google Sheets, Office 365, Typeform and Zapier** are named comparisons or prior tools. A **sixth sprint** using Glide is mentioned in a separate low-code class; it is not another NUCU sprint date.

A unified **Build in Japan app** covering registration and course tasks is a future intention. The existing app and a set of about **70 FAQs** illustrate the value of a chatbot interface such as **AITA** or Makoto-kun, but the future workflow is not shown as complete.

## Lovable and the no-code-to-code continuum

“**Vibe coding**” is explained as specifying the outcome in natural language and letting tools produce software, attributed to **Andrej Karpathy** about a year earlier. The user still defines the problem, journey and intended audience. The lecturer describes **React** as a JavaScript library and **Tailwind** as a CSS styling library, plus backend functions, storage and authentication.

The classroom comparison places **Glide/Airtable/Base44** toward no-code; **Lovable, Replit, Cursor and Windsurf** in a more technical middle; and **Claude Code / OpenAI Codex** further toward code ownership and professional development. These are pedagogical groupings, not a definitive current product taxonomy. Claude Code can produce files kept in GitHub and hosted on services such as **AWS or Vercel**. A prior **SQL 3205** course is referenced for relational tables and keys. **VS Code**, Microsoft's Visual Studio Code, is demonstrated as an editor with a terminal; it is distinct from Visual Studio despite the spoken shorthand.

A **Google Stitch** design/wireframe step is compared with **Figma, Canva, PowerPoint** or hand-drawn screens. The phrase “formerly known as like Figma” does not establish a product rename. **Google AI Studio** is also mentioned. A wireframe might show login, home and workout screens before implementation.

Two interaction patterns are contrasted: collaborative **chat**, repeatedly steering changes, and **agent mode**, delegating more implementation/testing/design decisions. The latter trades direct control for potential productivity; it does not prove generated authentication or testing is adequate. **Plan mode** can explore an idea without building the full backend. The timeline of **minute 10** for database/authentication and another **13 minutes** for a themed app is explicitly aspirational, compared with **week 10** of older projects. Traditional cost examples of **$5,000 / $15,000 / $50,000 / $500,000** are illustrations, not estimates for a particular project.

## Prompting sequence and live prototype

Start with the problem and **ICP, ideal customer profile**, then broad requirements, component refinements, and finally visual polish such as rounded or animated buttons. The warning is that fast automation of a bad idea still yields a bad idea. A pitch deck can seed requirements: user, problem, solution, funding and desired service. Reusable pieces include signup, payment, shipping and tax functions; reuse still needs fit and validation, rather than assuming every prior component is freely available or correct.

The live **Lovable** example requests a **progressive web app (PWA)** for workouts and sleep, usable on different screen sizes, with an **anime / Studio Ghibli-inspired** style. The simplified explanation treats it as a browser-delivered app; it is not a complete definition of install/offline capabilities. **Whisper** dictation and **Gemini** are used to help draft the prompt. Gemini is asked to generate a fuller Lovable prompt, which the user can revise rather than writing it all from scratch.

The system reportedly thinks **18 seconds**, chooses **deep purple, neon cyan and sunset orange**, produces glass-like cards, and names the design **Sleep Sanctum**. The class compares the appearance with **iOS 26 Liquid Glass**. CSS controls presentation rather than the underlying data or business behavior. No full functional or security test is shown. Students get roughly the **last 15 minutes** to experiment individually or in teams, comparing simple outcome prompts with more structured prompts and choosing plan or build. A forecast that future tools will need less elaborate prompting remains a prediction.

## Student demographic-map prototype

A student identified as **Blake** demonstrates a Japan map reportedly based on the **2020 census**, showing age distribution, **65+** and working-age groups across areas called “provinces” in the transcript. He adds a year simulator, including **2050**, using **Claude Code in the VS Code terminal**. He first asks Claude to write a better prompt from a general idea, builds the initial map, then asks for feature suggestions and adds scenarios/projections. The class treats it as a spontaneous demo, not a confirmed team venture.

The source supplies no census dataset, projection method, assumptions or validation. Background chatter says **“41 out of 47”** without enough context to interpret it; it is not a population forecast. The map is an unpublished student-created artifact; the human reviewer approved publication of its description and Blake's attribution on 2026-09-30, retaining the validation caveats. See [[nucu-ai-assisted-prototyping-2026]].

## Source limits and review points

The wrap-up forecasts software firms becoming more data-centered, with **Salesforce** as an example. This is the instructor's market interpretation, not a proven future outcome. Product prices/free tiers, job openings, admissions, coverage and travel claims are dated statements only. The source has garbled passages, missing screen/handout content and unrelated background chatter; no missing links or instructions are invented. The human reviewer approved publication of the retained staff roles, job-contact attribution, student demo and internal task details on 2026-09-30. Identifying personal educational/medical records and credentials are excluded or redacted.

Course map: [[nucu-course-architecture-2026]].
