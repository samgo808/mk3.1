---
type: "concept"
title: "NUCU LLM Training, Tokens and Inference — 2026"
course_year: "2026"
status: "archived"
publication_status: "approved-public"
sources:
  - raw/curriculum/2026/nucu_lecture_session5_2_10_2026_CUT.txt
updated: "2026-09-30"
tags:
  - "pretraining"
  - "sft"
  - "reinforcement-learning"
  - "tokenization"
  - "2026"
---

# NUCU LLM Training, Tokens and Inference — 2026

The February 10, 2026 NUCU lecture introduces **pretraining, supervised fine-tuning (SFT) and reinforcement learning (RL)** using an adapted Andrej Karpathy teaching workflow. Its main aim is to explain how a text model becomes an assistant and why fluent output can still be wrong. This archived page preserves the lesson while separating demonstrations from training and identifying uncertain source claims.

## Text, tokens and learned weights

The lecture starts with **Common Crawl/FineWeb**, text filtering, language selection, deduplication and personal-information filtering. A Hobbit-review passage illustrates **1,468 bytes = 11,744 bits**, compressed into **313 tokens** in its selected tokenizer. Tokenization can encode parts of words, spacing and case; token IDs belong to a particular tokenizer.

For **“A few weeks ago,”** the lecture shows predicting the next token and adjusting mathematical weights when training targets are known. The knobs analogy represents optimization. A transformer illustration includes embeddings, positions and attention; it is not a literal picture of hardware. FineWeb token totals, GPT-2 parameter counts and other scale figures conflict or lack evidence in the transcript; see the source page before using them.

## Training versus inference

**Pretraining** develops broad continuation capability from examples. **Inference** uses the trained model and supplied context to generate output. “A few weeks later” can be a plausible sampled continuation even when the example originally ended “ago.” Inference does not necessarily browse the web or update weights.

A **Llama 3.1 base** demonstration answers imperfectly to ordinary questions; a **Human/Assistant few-shot prompt** helps it follow an answer pattern. That prompt demonstration steers inference. It should not itself be labeled weight-updating SFT. **Base** and **Instruct** are meaningful distinctions when evaluating model behavior.

## Assistant behavior and uncertainty

**SFT** uses worked examples of desired responses. The lecture describes human experts and synthetic dialogues, with tasks such as translation, summaries, factual answers and Japanese tea-ceremony explanation. Helpful, truthful, harmless and non-toxic responses are the stated goals.

A fictitious **Orson Kovacs** biography illustrates hallucination. Training examples that admit uncertainty and tools that retrieve evidence can help, but neither guarantees correctness. Role-delimiter tokens are discussed; the speaker's guessed expansion of “IM” is not established. An assistant's declared identity is not reliable proof of its underlying model.

Training knowledge is compared with long-term memory; a **context window** with working information. Providing a **War and Peace** passage gives directly available evidence. These analogies do not imply human memory or guaranteed perfect recall of long contexts.

## Reasoning and tools

The fruit problem—**three apples plus two $2 oranges for $13**—gives **$3 per apple**. Intermediate steps can support an answer; they do not inherently require fewer tokens. **9.9 exceeds 9.11** in the live demonstration. Strawberry-letter counts and the inconsistently checked “every third letter of ubiquitous” task show why token-level generation and exact character manipulation need different care.

**Python execution** and retrieval are possible external tools, not guaranteed internal actions. **RL** uses feedback on outcomes or behavior; the lecture's chemistry-book analogy compares reading basics, studying worked examples and solving exercises. Its **DeepSeek/Deep Think** example illustrates self-correction and longer computation, not proof of continual weight updates or full access to internal reasoning.

Human feedback, SFT and machine-verifiable reasoning rewards should remain distinct; the source's compressed explanation does not supply a full RL taxonomy. Hardware prices, proprietary-model parameter estimates and platform controls are historical claims, not current recommendations.

See [[2026-02-10-nucu-session-5]] for all example IDs, figures, attribution and unresolved details, and [[nucu-ai-model-tradeoffs-2026]] for the preceding model-selection discussion.
