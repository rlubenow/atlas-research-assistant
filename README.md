# Atlas — Research Assistant System

Atlas is a **two-phase research assistant** designed to perform **targeted research**, build a **persistent knowledge base**, and enable **interactive, grounded question-answering** over retrieved sources.

This project emphasizes **agentic planning, deterministic execution, and evaluation-ready system design**, rather than prompt-only demos.

---

## Problem Statement

Researchers and knowledge workers frequently need to:
- Perform targeted research across multiple documents
- Synthesize findings into concise summaries
- Re-query and explore the same source material iteratively
- Maintain traceability to original sources

Most GenAI systems treat research as a **single-shot interaction**, discarding retrieved context and lacking persistence, observability, or evaluation rigor.

---

## Solution Overview

Atlas separates research into **two explicit phases**:

### Phase 1 — Targeted Research & Knowledge Base Construction
1. User submits a research prompt
2. The system plans and executes a targeted research workflow
3. Retrieved documents are:
   - Synthesized into a structured research report
   - Persisted into a searchable knowledge base
4. All sources are indexed for future use

### Phase 2 — Interactive Exploration
1. User interacts with an LLM backed by the newly created knowledge base
2. Questions are answered using retrieved, grounded context
3. Responses include traceability to indexed source documents

This mirrors how real internal research tools operate: **research first, interaction second**.

---

## Design Principles

- Deterministic agent workflows over free-form chaining
- Persistent knowledge, not ephemeral context
- Hybrid retrieval (semantic + structured metadata)
- Clear separation of orchestration, retrieval, and reasoning
- Evaluation-first system design

---

## System Architecture

User
├── Phase 1: Research Request
│ ├── LangGraph Research Planner
│ ├── Document Retrieval
│ ├── Summarization & Synthesis
│ ├── Storage (S3 / MinIO)
│ └── Indexing (Postgres + pgvector)
│
└── Phase 2: Interactive Q&A
├── Query Understanding
├── Retrieval from Knowledge Base
├── Contextual Answer Generation
└── Source-grounded Responses


---

## Core Components

### Orchestration
- **LangGraph** for stateful, multi-step research workflows
- **LangChain** primitives used selectively (retrievers, loaders, tools)

### Storage & Retrieval
- **PostgreSQL** — primary metadata store
- **pgvector** — embedding storage and semantic search
- **Redis** — caching, session state, intermediate results
- **S3 / MinIO** — raw document and artifact storage

### Models
- LLMs used for:
  - Query understanding
  - Planning
  - Summarization
  - Answer synthesis

(Model providers are abstracted behind interfaces.)

### API & Product
- **FastAPI** backend (async, streaming-ready)
- **Next.js** frontend for research submission and interactive querying

---

## Phase Breakdown

### Phase 1 — Research Execution
- Input: Targeted research prompt
- Output:
  - Structured research summary
  - Indexed document corpus
  - Persistent embeddings
- Characteristics:
  - Explicit planning
  - Deterministic execution graph
  - Reproducible outputs

### Phase 2 — Knowledge-Aware Interaction
- Input: Follow-up questions
- Retrieval:
  - Semantic search over indexed documents
- Output:
  - Grounded answers
  - Source references
- No re-scraping or re-indexing required

---

## Tech Stack

### AI & Orchestration
- LangGraph
- LangChain

### Data & Storage
- PostgreSQL
- pgvector
- Redis
- S3 / MinIO

### Backend & Product
- FastAPI
- Next.js

### Infrastructure
- Docker
- Local-first, cloud-optional architecture
