---
type: "entity"
title: "Makoto-kun Classroom RAG Demonstrations — 2026"
course_year: "2026"
status: "archived"
publication_status: "approved-public"
sources:
  - raw/curriculum/2026/nucu_lecture_session6_2_17_2026_CUT.txt
  - raw/curriculum/2026/nucu_lecture_session12_4_7_2026_CUT.txt
updated: "2026-09-30"
tags:
  - "makoto-kun"
  - "rag"
  - "n8n"
  - "historical-demonstration"
  - "2026"
---

# Makoto-kun Classroom RAG Demonstrations — 2026

The archived February 17 and April 7, 2026 NUCU lectures demonstrate earlier **Makoto-kun** versions and their limitations. They explain why selected retrieval context can work better than repeatedly sending a long brochure or transcript. These are historical classroom observations, not documentation of the present MK3.1 runtime.

## Version distinctions

- **1.0:** custom GPT in ChatGPT.
- **2.0/2.1:** n8n agent using brochure text; the February lecture estimates roughly **2,800 tokens** for the brochure.
- **2.3:** RAG, **retrieval-augmented generation**, with lecture/program documents, vector retrieval and Discord.
- **3.0:** an April proposal to explore an **OpenClaw** agent and linked-wiki/second-brain approach. It was not demonstrated as operational.

The spelling “NAN” in these transcripts refers to **n8n**. “MIDI” in a course-content query refers to **MITI**, Japan's Ministry of International Trade and Industry.

## Two pipelines

In the historical ingestion demonstration, cleaned lecture text and topic keywords go to GitHub, an HTTP node retrieves the raw text, a splitter makes chunks, an embedding model represents them numerically, and the vector store saves them. April's demo reports **71 items** and a subsequent count of **347 records**. Neither number is a current production count.

At question time, Discord passes a message to a webhook and agent. Retrieval finds related stored material; the language model uses context to compose an answer. The February demo uses program information and session 2; April adds session 6. The instructor's historical cleaning of transcripts does not change today's rule that raw sources are immutable and compilation occurs in the wiki.

## Why successful storage is not successful retrieval

The April query **“When did we talk about Reiwa?”** failed even after loading the relevant text. Asking about **overwork/karoshi** returned **session 6, February 17, 2026**. Similarly, Karpathy's lecture date needed extra transformer context. These examples support testing exact, paraphrased and contextual questions, not assuming a successful loader guarantees answers.

The three-dimensional word analogy and **+4/−4/0 dot products** are teaching illustrations. Document chunking, tokenization, embeddings and generation are distinct operations. A model does not generally retrieve each next word from the application's vector store, and antonyms need not have negative similarity. The source records these oversimplifications explicitly.

## Tools and interface boundaries

The lectures describe email escalation, a separate **test calendar**, a live general-channel reply failure, and possibly expired calendar/API access. April's OpenClaw and cloud-hosting discussion remains exploratory. Discord channels, DMs and verification procedures belong to those classroom demonstrations; no private server URL or credential is included. Neither lecture proves current email/calendar availability, access control, memory isolation, deployment or year filtering.

For full context and source limitations, see [[2026-02-17-nucu-session-6]] and [[2026-04-07-nucu-session-12]].

The preceding January examples are recorded in [[nucu-ai-assistant-demonstrations-2026]].
