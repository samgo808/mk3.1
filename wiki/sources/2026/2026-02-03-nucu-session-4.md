---
type: "source"
title: "NUCU Session 4: Networking and AI Model Primer — 2026-02-03"
course_year: "2026"
status: "archived"
publication_status: "approved-public"
sources:
  - raw/curriculum/2026/nucu_lecture_session4_2_3_2026_CUT.txt
updated: "2026-09-30"
tags:
  - "networking"
  - "ai-models"
  - "prompting"
  - "2026"
---

# NUCU Session 4: Networking and AI Model Primer — 2026-02-03

The archived February 3, 2026 BAIM 3300 technology primer connects networking fundamentals with language models, specialized AI, infrastructure and prompting. The instructor presents OSI/TCP/IP as useful business-technology literacy before comparing model types. This transcript includes simplified and sometimes technically questionable explanations; the qualifications below are part of the compiled teaching record.

## Course context and resources

Quiz 2 will cover **sessions 4 and 5**, become available after the following lecture and allow roughly **one week**, untimed. Slides are linked through the course spreadsheet and Canvas. The transcript reports a class-level quiz average; that nonessential assessment information is not reproduced in this public-review draft. Named faculty/context include **Jason Thatcher**, **Kai Larson**, **Alex Ratosky** and **Heather Adams**, plus the instructor's Purdue background. Institutional recruitment details are source anecdotes, not verified biographies. Later suggested technical experts include **David Doebley, Abe Handler, Liu Liu and Dan Zhang**, with spelling/roles unverified. A short **KnowledgeCatch** OSI video and longer optional explainers are described, but recoverable URLs are absent.

## OSI and TCP/IP

**OSI = Open Systems Interconnection**, associated with **ISO = International Organization for Standardization**. Its seven layers, bottom to top, are:

1. **Physical:** cables, radio/Wi-Fi, fiber and electrical/optical signals.
2. **Data link:** local-network frames and **MAC** device addressing.
3. **Network:** **IP** addressing and routing between networks.
4. **Transport:** host-to-host data transport; **TCP** supplies ordered/reliable delivery in the example.
5. **Session:** establishes, manages and ends sessions.
6. **Presentation:** representation/translation, compression and encryption in the teaching model.
7. **Application:** services used by applications such as web, mail and messaging.

Packetization is compared to putting goods in **FedEx/UPS boxes** instead of shipping a loose pile; recipients unpack/reassemble. A photo sent to a friend, a frozen movie and session timeout illustrate diagnostic questions. Layer boundaries are conceptual: not every router is a physical-layer device, every transport retransmits, or every website session timeout is literally OSI session-layer behavior. The video's bottom-up photo story is not a precise sender/receiver protocol trace.

**TCP/IP = Transmission Control Protocol / Internet Protocol**, not intellectual property. The four-layer mapping taught is **network access = OSI 1–2**, **internet = 3**, **transport = 4**, **application = 5–7**. OSI is the diagnostic/reference model; TCP/IP is the practical Internet suite, sometimes described as four/five layers. Both are quiz material. Messaging via **Telegram, Signal and Discord**, live-video packet loss, Ethernet/Wi-Fi and **Starlink** contextualize the stack. The transcript's “prompting at the transport layer” and describing IP as reassembling/retransmitting everything are simplifications, not operational networking guidance. See [[nucu-networking-primer-2026]].

## Physical infrastructure and scarce resources

AI services depend on networks, CPUs, GPUs, memory, storage, cooling fans and water. **Cisco** illustrates networking businesses; **copper, silver, gold and nickel** illustrate material dependencies. The speaker predicts strong demand and high earnings for data-center electricians/plumbers and opportunities in energy, including oil/gas, nuclear, hydro, wind and fusion/fission; these are career/economic forecasts, not salary guarantees.

An **Indianapolis/Google data-center rejection** anecdote illustrates grid demand, prices, water, **20–30 decibels** of background noise, heat and light pollution. The specific event and figures are unverified. A **Virga** water-analysis anecdote describes conflicting needs of farmers, rafting companies and ski resorts, legal allocation/payment questions, and the irony that AI water use may constrain AI-assisted water modeling. Its organization/project details are incomplete and should not be treated as verified policy. CU sustainability priorities and renaming a hackathon a sustainability challenge are contextual remarks.

## Generalists, specialists and limitations

The lecturer describes the field as developing over **15–20 years**, a simplified framing rather than its full history. The lecturer sketches **big data → machine learning/patterns → probabilistic language models**, using “there/their” as a language example. LLMs are generalists or a **quarterback/front desk** coordinating specialist knowledge and tools. More scale can bring compute, latency and cost tradeoffs; the lecture does not establish that bigger always means better or slower.

Products mentioned are **ChatGPT, Gemini, Claude/Claude Code, Copilot, Grok/xAI and DeepSeek**. Examples include hallucinated prospects, useful outreach once a person is verified, coding support, and enterprise constraints on transcripts/email/Teams summaries. A participant's employer/security details are not republished; the substantive issue is that governance and data residency can limit features. The instructor contrasts Google's algorithmic search with Yahoo's human indexing and observes that users often want an answer rather than a list of links. **Mixture of experts, reasoning and long-horizon models** are named without detailed treatment.

Time-sensitive claims include **1.1 billion ChatGPT monthly active users**, **49% Microsoft ownership**, cheap/non-embargoed DeepSeek hardware, and a **three-week** marketing task turning **three years** of social metrics into **three years** of future posts. They remain unverified lecture-time statements/anecdotes. **November 2022 / ChatGPT 3.5** anchors the discussion; enthusiasm or criticism of GPT-5 and iPhone generations is opinion, not a benchmark.

**Small language models (SLMs)** motivate smaller scope, local/edge operation, privacy, speed and billions rather than trillions of parameters. Analogies are a boombox versus headphones/Bluetooth/watch speakers, or Apple AirPods as a miniaturization business. Examples include an auto mechanic's engine knowledge, company inventory/reordering, a class assistant and **Thomson Reuters CoCounsel** for legal/accounting work. Product specialization alone does not establish model size, local execution or absence of hallucinations. A custom GPT with uploaded files is not evidence that a new small model was trained.

The lecturer argues local tools may be useful on an airplane, underwater or in a tunnel and with sensitive home/security data. Claims about chat-history controls automatically determining training use are product-specific and cannot be treated as current privacy guidance. “All public data is indexed” and convergence claims are speculative. A **Clawdbot/Moltbot** discussion, transcribed in several forms, describes an open-source “free Claude,” **$500–$800 Mac Minis**, **Kimi 2.5**, full local-model equivalence and cost savings. These conflate agent software, underlying models and hosting; no installation or security recommendation is supported by the transcript. The AirPods “top-50 company” comparison is also unverified.

## Two meanings of LCM and recursive models

**Latent Consistency Model** and **Large Concept Model** share **LCM** but are different terms. The lecture associates the former with one/few-step speed, surgical/military AR overlays and robot navigation. Its claims of identical runtime, perfect first/second-attempt answers or mandatory use for friend-or-foe recognition are unsupported and must not be promoted as engineering guarantees.

The latter is presented as operating on concepts rather than only next-word prediction. **Financial versus environmental sustainability** demonstrates contextual meaning: profit, runway and solvency versus trees/water. A **Japanese translation/hospital directions versus emergency** example motivates meaning beyond literal vocabulary. The transcript does not supply an architecture or evidence for universally language-agnostic understanding. Neural-network/reward/corpus comparisons are high-level speculation.

**Recursive language models (RLMs)** and MIT work are introduced through unseen charts: a GPT-5 curve degrades with long context while an alternative handles more with less degradation. Exact benchmark results are unavailable. Better quality and lower cost are presented as possibilities, not verified forecasts. See [[nucu-ai-model-tradeoffs-2026]].

## Prompting and automation exercise

The **5P framework** is referenced but its five labels are not enumerated in the audible text; do not invent them from missing slides. Prompts specify the task, role and success criteria. Examples target **strategic market research, lean canvas and product-market fit (PMF)**. Students should share a useful prompt after removing sensitive/identifying information; an LLM can help write a **meta-prompt**. Student examples concern stock screening and synthesizing papers into a database, without operational trading instructions.

A **Zapier → Salesforce** lead-enrichment example filters test/junk leads, formats text, uses **FireCrawl** for web/LinkedIn data, calls **Gemini** with a market-research/strategic-donation-advisor role, asks it to check work and avoid repeating instructions, then returns a concise dossier to Salesforce. A lead may arrive via a web form; **two/three seconds** is an anecdotal latency, not a guarantee. The client is already redacted and must remain so. Unintelligible setup language is not reconstructed.

The closing factory example connects sensors (e.g., **72-degree** temperature, projector and microphone state) with local anomaly decisions, cloud root-cause analysis across factories and visual technician overlays with serial numbers/instructions. Automatic alarms or shutdowns are hypothetical architecture examples, not validated safety controls.

## Review and related pages

Keep unsupported technical claims, forecasts and enterprise anecdotes qualified. No private employer identity, client detail or individual assessment record is supplied in the compiled narrative. Classroom chatter, duplicates and unintelligible passages are omitted, while the missing 5P labels and charts are explicit limitations. Public publication was approved on 2026-09-30; factual caveats remain.

- [[nucu-networking-primer-2026]] — stack mapping and troubleshooting.
- [[nucu-ai-model-tradeoffs-2026]] — terms, use cases and source cautions.
- [[2026-02-10-nucu-session-5]] — training and tokenization lecture.

Course map: [[nucu-course-architecture-2026]].
