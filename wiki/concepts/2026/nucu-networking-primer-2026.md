---
type: "concept"
title: "NUCU Networking Primer: OSI and TCP/IP — 2026"
course_year: "2026"
status: "archived"
publication_status: "approved-public"
sources:
  - raw/curriculum/2026/nucu_lecture_session4_2_3_2026_CUT.txt
updated: "2026-09-30"
tags:
  - "osi"
  - "tcp-ip"
  - "networking"
  - "2026"
---

# NUCU Networking Primer: OSI and TCP/IP — 2026

The February 3, 2026 NUCU lecture teaches **OSI** and **TCP/IP** to explain the infrastructure behind AI services. OSI is a seven-layer reference for communication and troubleshooting; the lecture's TCP/IP mapping groups Internet functions into four layers. This is an archived teaching model, with simplifications noted rather than used as exact protocol specifications.

## Layer mapping

| OSI layer | Teaching function | TCP/IP grouping |
|---|---|---|
| 7 Application | Web, mail, messaging services | Application |
| 6 Presentation | Representation, compression, encryption | Application |
| 5 Session | Establish/manage/end a session | Application |
| 4 Transport | End-to-end data transport, TCP example | Transport |
| 3 Network | IP addresses and routing | Internet |
| 2 Data link | Local-network delivery and MAC addresses | Network access |
| 1 Physical | Signals through copper, fiber or radio | Network access |

**OSI** expands to **Open Systems Interconnection**; **ISO** is the **International Organization for Standardization**. **TCP/IP** expands to **Transmission Control Protocol / Internet Protocol**. Here IP means Internet Protocol, not intellectual property. The lecture also acknowledges four/five-layer presentations of TCP/IP; the four-group map is the one explained in detail.

## Packets and troubleshooting

The **FedEx/UPS-box analogy** explains packaging information into manageable units rather than sending a loose pile. Routing gets units toward their destination, and recipient-side processing reconstructs useful content. **MAC** and **IP** addresses have different roles in the teaching model: local link identification versus routed network addressing.

A movie that will not play can fail because the device lacks power, connectivity is absent, or a higher-level service is unavailable. A failed photo message can similarly prompt checks of signals, local connectivity and routing. The value is narrowing the question instead of treating the whole Internet as one black box.

The source video uses an oversimplified photo story, and the lecturer compares web-session timeout with OSI session functions. Do not assume those analogies identify the exact failing implementation layer. TCP's reliability should not be generalized to every transport protocol, nor should IP be described as guaranteeing delivery/retransmission. “Prompting at the transport layer” is a source simplification, not a classification of all model interaction.

## Why this matters to AI

**Telegram, Signal and Discord** illustrate application-level services built on networks. **Ethernet, Wi-Fi, fiber and Starlink** illustrate access technologies; **Cisco** illustrates networking hardware. GPUs and CPUs also depend on storage, memory, electricity and cooling, so a digital service still has physical bottlenecks.

The lecture's proposed factory workflow moves sensor data to local decisions, sends selected information through TCP/IP for cloud analysis, and returns technician guidance through visual overlays. This is a conceptual exercise; it does not establish verified control-system safety or that all AI must run over the Internet.

See [[2026-02-03-nucu-session-4]] for the source's examples and qualification record, and [[nucu-ai-model-tradeoffs-2026]] for local-versus-cloud tradeoffs.
