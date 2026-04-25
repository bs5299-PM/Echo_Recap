# EchoRecap — Real-Time AI Lecture Intelligence Agent

> **Whisper STT + AI Agent + RAG  |  Accessibility / Education  |  AI PM Portfolio Project**

---

## The Problem

Students with ADHD or hearing impairments cannot simultaneously
listen, process, and write notes fast enough to keep up with a lecture.
By the time they write one point, three more have passed.

- **1 in 5 students** has a learning disability (ADHD, dyslexia, auditory processing disorder)
- **1 in 8 people** globally has disabling hearing loss — many are in higher education
- Existing tools (Otter.ai, Rev) produce **unstructured walls of text** — after class, not during it
- Human note-takers cost **$3,000–$8,000 per student per year** — expensive and inconsistent

---

## The Solution

EchoRecap is a real-time lecture companion that transcribes audio
using Whisper STT, then uses an AI agent to extract **Key Concepts**
and **Action Items** as the lecturer speaks — displaying them in a
live sidebar with **under 1.5 seconds of latency**.

Unlike every other tool, EchoRecap structures the lecture
**while it is still happening** — not after.

---

## System Architecture

System Architecture-PRD.png

---

## System Flow

User Flow Daigram-PRD.png

---

## Key PM Decisions

| Decision | Why |
|---|---|
| GPT-4o-mini not GPT-4o for extraction | Latency budget allows only 0.4s for the LLM — mini hits this, GPT-4o does not |
| Local Chroma vector store | Zero network latency on RAG retrieval + audio never leaves the device (FERPA) |
| Whisper medium not large | Best accuracy/speed balance — large model too slow for real-time 5-second chunks |
| 5-second rolling audio chunks | Short enough for real-time feel, long enough for sentence-level context |
| Local-first architecture | Universities will not approve tools that send lecture audio to external servers |
| Task Success Rate as north star | A low-WER transcript that produces useless concepts has failed — product outcome beats model metric |

---

## Tech Stack

`Whisper STT` · `GPT-4o-mini` · `GPT-4o` · `text-embedding-3-small` · `Chroma` · `WebRTC` · `LangGraph`

---

## Evaluation Framework

| Tier | Metric | Target |
|---|---|---|
| Transcription | Word Error Rate | < 10% |
| Transcription | Transcription latency | < 0.8s |
| Extraction | Concept precision | > 75% |
| Extraction | Grounding rate | > 95% |
| Extraction | Agent latency | < 0.4s |
| Product ⭐ | Task Success Rate | > 80% |
| Product | End-to-end latency P95 | < 1.5s |
| Product | Session completion rate | > 85% |
| Business | Cost per 60-min session | < $0.50 |

---

## Latency Budget

| Step | Budget | Design decision |
|---|---|---|
| Audio capture (WebRTC) | < 0.1s | Local — no network round-trip |
| Whisper STT (streaming) | < 0.8s | Words appear as recognised |
| RAG retrieval (Chroma) | < 0.2s | Local vector store — zero latency |
| GPT-4o-mini extraction | < 0.4s | Classify only, do not explain |
| UI sidebar render | < 0.1s | Streaming React state update |
| **Total P95** | **< 1.5s** | **Speech to sidebar card appearing** |

---

## Market Opportunity

| Signal | Data |
|---|---|
| Accessibility tech market (2024) | $26.8B → $54.1B by 2030 (12.4% CAGR) |
| EdTech AI segment growth | $4.5B, 18% CAGR |
| US students with documented disabilities | 7.5 million (NCES, 2023) |
| Current note-taker cost per student/year | $3,000–$8,000 |
| Total addressable market | $2.8B at 30% penetration |

---

## Competitive Landscape

| Tool | Real-time? | Structured? | Accessibility? | Latency |
|---|---|---|---|---|
| Otter.ai | Partial | No | No | Not stated |
| Rev | No | No | No | N/A |
| Microsoft Teams captions | Yes | No | Partial | ~2–3s |
| **EchoRecap** | **Yes** | **Yes** | **Yes** | **< 1.5s** |

---

## Full PRD

📄EchoRecap_PRD.docx

Covers all 9 sections of the professional AI PRD template plus
full technical design — System Architecture, Model Stack,
Evaluation Metrics, Latency Budget, Failure Modes, HITL Design,
Rollout Plan, and Success Metrics.

---

*Built by [Your Name] · AI Product Manager*
*[linkedin.com/in/your-username](https://linkedin.com/in/your-username)*
