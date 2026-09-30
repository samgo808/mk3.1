---
type: "entity"
title: "NUCU Historical AI Assistant Demonstrations — 2026"
course_year: "2026"
status: "archived"
publication_status: "approved-public"
sources:
  - raw/curriculum/2026/nucu_lecture_session3_1_27_2026_CUT.txt
updated: "2026-09-30"
tags:
  - "ai-assistants"
  - "makoto-kun"
  - "retrieval-augmented-generation"
  - "2026"
---

# NUCU Historical AI Assistant Demonstrations — 2026

The January 27, 2026 NUCU lecture demonstrates a Charlie Munger-style assistant, earlier Makoto-kun versions and a personal Weela AI prototype. The teaching pattern is **instructions/persona + supplied knowledge + optional tools**. These are archived demonstrations and planned capabilities, not documentation of the current Makoto-kun deployment.

## Charlie Munger Investment Assistant

The lecturer supplies a long-term investing persona, PDFs of interviews/profiles and suggested questions. An AI-written **JavaScript API action** retrieves stock quotes; the demonstration requests an **Apple** stock price. The transcript supplies no reliable numeric quote or credential values.

The example illustrates how a model combines instructions, reference material and external data. The lecturer notes that capabilities requiring custom work a year earlier may later appear in a general product. It does not validate investment recommendations or make this a currently supported tool.

## Makoto-kun development stages

The first-generation custom GPT contains lecture, meeting, virtual-session, calendar and itinerary documents. Repeated manual additions enlarge the prompt and knowledge base, with perceived slowness and ecosystem dependence. A demonstrated Station Ai question uses **last year's May 20/2025 itinerary**, not a 2026 schedule.

An **n8n** version, transcribed “NAN,” uses an AI agent, a chosen language model and a program brochure in a text document. Email escalation and coffee-chat scheduling are described as possible tools. The lecturer says whole-document reading becomes inefficient as transcripts and schedules accumulate.

A **Makoto-kun 2.3 RAG** version is described as work in progress: retrieve only relevant chunks, then answer from them. This explains the motivation for retrieval-augmented generation; it does not prove all earlier retrieval implementations actually reread every document or establish today's architecture. Runtime instructions remain governed by the project's operating documents, not this lecture page.

## Weela AI and social questions

The lecturer describes giving his mother a **StoryWorth** subscription that sends weekly life-story questions. Collected answers form a personal assistant's knowledge; Spanish/English persona instructions make the conversation feel familiar. He states that his mother is alive.

The example explores loneliness, preserving knowledge, simulated identity and the difference between talking to a persona and talking to a real person. The transcript does not establish therapeutic effectiveness. Private autobiographical answers are not reproduced in this compiled page. The human reviewer approved public release of the named family-related example and prototype on 2026-09-30.

## Review boundary

The lecture mentions course recordings/transcripts as future Makoto knowledge. That historical statement does not authorize ingestion of private chat histories, private family archives, or external messages. No passwords, API keys or private endpoints appear in this page. Tool names describe the demonstration, not permission to execute them.

See [[2026-01-27-nucu-session-3]] for source context, course announcements and the accompanying economic lecture.

For the later February and April observations, see [[nucu-makoto-rag-demonstrations-2026]].
