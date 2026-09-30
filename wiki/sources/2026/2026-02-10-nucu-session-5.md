---
type: "source"
title: "NUCU Session 5: LLMs, Transformers and Training — 2026-02-10"
course_year: "2026"
status: "archived"
publication_status: "approved-public"
sources:
  - raw/curriculum/2026/nucu_lecture_session5_2_10_2026_CUT.txt
updated: "2026-09-30"
tags:
  - "llm-training"
  - "tokenization"
  - "transformers"
  - "2026"
---

# NUCU Session 5: LLMs, Transformers and Training — 2026-02-10

The archived February 10, 2026 BAIM 3300 lecture explains LLM development through **pretraining → supervised fine-tuning (SFT) → reinforcement learning (RL)**. Samuel Goodman adapts an **Andrej Karpathy** educational workflow and demonstrations for a business-school audience. It is a simplified teaching record; model figures, token IDs, product behavior and uncertain explanations must not be treated as current specifications.

## Dataset construction and source figures

The lecturer describes **Common Crawl**, a nonprofit collecting web pages over roughly **20 years**, quoting **300 billion pages**. **FineWeb** is the filtered example: text extraction, English preference, adult-content filtering, deduplication and personal-information removal. Such filtering is described as an aim/process, not proof that all private or unsafe content is absent.

The transcript calls FineWeb **44 terabytes** and **15 million tokens**; these quantities appear inconsistent and require checking. The claim that Llama models use this exact dataset is not substantiated. A scraped **Tumblr/blog review of The Hobbit** provides the tokenization demonstration; the actual dataset/download links are not recoverable here. Preserve these as source claims rather than silently replacing numbers.

## Tokenization demonstration

Text is represented as bytes/bits, then recurring sequences are merged into token units. The example moves from about **1,400 characters**, more exactly **1,468 bytes**, to **11,744 bits**, then **313 tokens**. Eight bits allow **256 values**; **84** is shown for uppercase **T**. The **32,116** byte pattern is described as recurring about **18 times**. “Converting bytes into bits” is spoken inconsistently; the arithmetic illustrates representation rather than a general compression guarantee.

The tokenizer is case-sensitive. The demo quotes **791** for “The,” **37876** for part of “Hobbit” and **4590** for its ending, but spoken segmentation is inconsistent. For “A few weeks ago,” IDs are **32 = A**, **2478 = space/few**, **5672 = space/weeks**, **4227 = ago**; alternatives include **3010 = later** and **892 = time**. These are illustrative IDs for an unspecified tokenizer, not universal word codes. The later Q&A explicitly recognizes tokenizer dependence and uncertainty about asking another model to decode IDs.

## Pretraining and inference

The network predicts a next token from prior tokens. During training, the dataset supplies the target; mathematical optimization changes **weights/parameters**, compared with knobs adjusting probabilities. No person manually sets every knob. A transformer visualization shows embeddings/positions, attention and repeated processing before an output; it is not literal hardware. The transcript calls one demonstration “GPT-2 / 85,000 parameters,” then later gives GPT-2 **1.6 billion**. These cannot be read as a consistent specification of one model; a toy visualization and full model may be conflated.

During **inference**, the trained model generates continuations. “A few weeks later” can be coherent even when “ago” was the training example; the instructor invokes a **SpongeBob “three weeks later”** meme. References to flipping coins are analogies for sampling, not claims that outputs are uniformly random. A student's description of consulting all stored Internet content should not be mistaken for live browsing on every token.

## Compute and scale anecdotes

An **eight-GPU rack** leads into **H100/B200** examples. Quoted **Lambda** rental rates are **$2.20/hour H100** and **$3.79/hour B200**. Purchase estimates are **$25,000–$40,000** and **$45,000–$50,000**, respectively. These are lecture-time estimates, not current offers or necessarily comparable configurations.

The lecturer mentions **Colossus 1: 200,000 GPUs**, **Colossus 2: 500,000**, possible Colossus 3, and over **1,000 MW = 1 GW**, likened to one reactor or a medium-sized city such as Denver/San Diego. Exact capacity, completion status and city comparisons are not verified. More compute is presented as enabling training, not as a guarantee of accuracy.

A comparison gives GPT-2 **1,024 context length**, **1.6 billion parameters**, **100 billion training tokens** versus GPT-5 **400,000 context**, estimated **3–5 trillion parameters** and **50–70 trillion training tokens**. The lecturer explicitly says newer internals are unpublished estimates; all figures need qualification, especially the older-model dataset claim. Do not convert this into a current model-comparison table of verified facts.

## Base models, demonstrations and knowledge limits

A **Llama 3.1 base** demo continues “Why is the sky blue?” rather than reliably behaving like an assistant, with output capped at **128 tokens**. A Teacher/Sensei example illustrates continuation by pattern. The distinction is **base** versus **Instruct**, not simply an older versus newer brand.

The lecturer uses a **November 2024 Trump/running-mate** prompt to illustrate cutoff-related uncertainty. The intended answer is **J. D. Vance**; demo continuations include **Mike Pence** and **Ron DeSantis**. This is a historical example, not present political guidance. The asserted training cutoff explains the demo in the lecture but is not independently verified model provenance.

A **few-shot** Human/Assistant pattern includes blockchain, who invented the Internet, simple explanations and admitting uncertainty, then revisits why the sky is blue. Providing examples in a prompt can steer inference; this demonstration alone is not evidence of changed weights or actual SFT. The lecture sometimes uses “training” loosely here.

## SFT, human labelers and synthetic data

SFT teaches assistant-like responses through example dialogues. An **InstructGPT/GPT-3 paper, page 27**, is cited for human-produced tasks: Broadway-play summary, Spanish translation, a short story and Earth's shape. The transcript discusses expert labelers, helpful/truthful/harmless/non-toxic guidance and labor cost, plus **synthetic dialogue data** generated by models. A **Japanese tea-ceremony history/significance** question is the synthetic-data example.

The lecture explains role delimiters but guesses “IM” means internal monologue. That expansion is uncertain and should not be taught as a verified definition or as access to hidden reasoning. **Orson Kovacs** is described as a fictional name used to test fabricated biographies; do not create a real-person entity for it. Admitting uncertainty and retrieving external evidence are presented as ways to reduce hallucinations. “10 or 20 examples” is a pedagogical illustration, not a guarantee of reliable uncertainty calibration.

Training knowledge is likened to long-term memory, while the **context window** is short-term working information. Supplying a **War and Peace** chapter may ground a question better than relying on pretrained recall. The abbreviation **RL** is disambiguated by conversational context. Model self-identification can be influenced by system instructions; the lecture's universal “hard-coded” explanation is simplified.

## Reasoning, math and tools

The worked problem has **three apples**, **two oranges at $2 each**, and **$13 total**: the apple unit price is **$3**. The lecturer argues intermediate steps help, but the assertion that step-by-step output necessarily uses fewer tokens is unsupported. Tool use such as **Python execution** or Internet retrieval can improve particular tasks; it is not automatic for every complex question.

Comparing **9.11 and 9.9** correctly gives **9.9** in the live examples, despite expectations of an older-model failure. Counting **r** in “strawberry” is another token/character distinction. An “every third letter of ubiquitous” task has an ambiguous starting convention and contradictory spoken checking: the lecturer first says U/I/T/S and later U/Q/... . Preserve the demo uncertainty rather than publish either as a verified sequence. A **GPT-4/4o retirement** aside is dated product commentary, not a current schedule.

## Reinforcement learning

A **chemistry textbook** analogy compares learning fundamentals, studying worked examples and solving problems with back-of-book answers. RL is presented as optimizing ways to reach useful/correct answers through feedback, including efficiency. This should not collapse every post-training method into RLHF: the transcript names human feedback and machine feedback without a rigorous taxonomy or full reward design.

The **DeepSeek** paper/demo describes longer reasoning and self-correction, with **Deep Think** selected in the interface. Longer computation improving answers and a “most efficient path” are not identical claims. The lecture contrasts visible model-generated reasoning displays with ChatGPT's presentation choices; displayed text is not proof of the full internal process. It does not show that the deployed model updates weights during each conversation. Fast versus thinking modes are suggested for simpler versus harder tasks.

## Review limits and related pages

The lecturer recommends Karpathy's roughly **three-and-a-half-hour** video and a later epistemology lecture, but complete links are absent. Technical conflations, uncertain figures, invisible slides, repeated speech and garbled stretches remain documented. No secrets or private student records were found in this session's substantive compiled content. Public publication was approved on 2026-09-30; factual caveats remain.

- [[nucu-llm-training-lifecycle-2026]] — training/inference distinctions and examples.
- [[2026-02-03-nucu-session-4]] — broader networking/model primer.

Course map: [[nucu-course-architecture-2026]].
