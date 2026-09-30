---
type: "concept"
title: "NUCU AI Model Types and Tradeoffs — 2026"
course_year: "2026"
status: "archived"
publication_status: "approved-public"
sources:
  - raw/curriculum/2026/nucu_lecture_session4_2_3_2026_CUT.txt
updated: "2026-09-30"
tags:
  - "llm"
  - "slm"
  - "edge-ai"
  - "model-selection"
  - "2026"
---

# NUCU AI Model Types and Tradeoffs — 2026

The February 3, 2026 NUCU lecture compares broad language models, specialized/local systems, two meanings of LCM and recursive language models. The teaching aim is to choose tools for a task rather than assume one chatbot is best at everything. Several product and architecture claims are unsupported or conflated in the transcript, so this page records them as teaching examples with explicit limits.

## Broad capability versus specialization

**LLMs** are presented as generalists, likened to a quarterback or front desk that can coordinate specialists. Benefits are breadth and flexible interaction; possible costs are latency, computation and hallucination. **ChatGPT, Gemini, Claude/Claude Code, Copilot, Grok and DeepSeek** are discussed as contemporary examples, not ranked by verified benchmarks.

**SLMs** motivate compact models and narrower tasks. Examples are engine diagnosis for an auto mechanic, inventory/reordering, class knowledge and **CoCounsel** in legal/accounting work. A smaller model may be useful locally, but domain specialization, uploaded documents and model size are different properties. The lecture does not demonstrate that its custom GPT or named products actually use small locally trained models.

**Edge/local operation** means processing near the work or on a device instead of always contacting a distant service. The lecture imagines use on airplanes, in tunnels or without reliable connectivity, with privacy benefits from keeping data local. Such benefits depend on actual software and data flows; they are not automatic guarantees.

Miniaturization is illustrated by boomboxes, headphones, Bluetooth/watch speakers and AirPods. The **Clawdbot/Moltbot, Mac Mini and Kimi 2.5** anecdote conflates an agent interface with models and infrastructure. Its “free Claude” and equivalence claims should not be used as verified implementation instructions.

## LCM does not identify one model family

- **Latent Consistency Model:** the lecturer associates this with one/few-step responsiveness, AR overlays and robotics. Claims of perfect answers or fixed execution time are not supported by the supplied material.
- **Large Concept Model:** the lecture describes abstraction over ideas, using **financial sustainability** (profit, runway, solvency) versus **environmental sustainability** (water, trees) to explain context. Japanese directions and emergency language illustrate why literal translation may miss intent. No complete training design or guaranteed language independence is supplied.

The two expansions must remain distinct. Neither discussion establishes a medical, military or robotic deployment as safe or effective.

## Long context and resource limits

**Recursive language models**, associated with MIT research, are introduced through charts comparing context-length degradation. The plots themselves are absent; no numeric benchmark or current product recommendation can be recovered. The instructor's predicted improvement in quality and cost remains a forecast.

Networks, memory, processors, cooling, water and electricity constrain all these systems. An Indianapolis data-center story and a **Virga** water-modeling story illustrate competing resource needs; they are unverified anecdotes. Claims about energy prices, trades salaries and model market share are dated lecture claims.

## Combining tools

A factory example combines sensors, local anomaly processing, cloud analysis across sites and a technician's visual overlay. A separate lead-enrichment workflow combines Salesforce, Zapier, FireCrawl and Gemini. The lesson is to separate data collection, inference, tools and action, while checking governance and privacy requirements.

See [[2026-02-03-nucu-session-4]] for complete examples and limitations, [[nucu-networking-primer-2026]] for networking, and [[nucu-llm-training-lifecycle-2026]] for the next lecture's training explanation.
