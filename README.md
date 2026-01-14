# Atlas

Two‑phase research assistant with targeted retrieval and a conversational knowledge base.

## Problem
Teams need fast, targeted research without losing provenance. Traditional research tools struggle to keep sources organized and make it hard to revisit findings interactively.

## Solution
Atlas runs in two phases: Phase 1 performs targeted research and produces a structured report plus a source index. Phase 2 lets users query the new knowledge base through a conversational model, enabling deep follow‑ups with citations.

## Tech Stack
- LangChain / LangGraph
- Postgres
- Redis
- PGVector
- S3/MinIO
- Next.js
- Hydra

## Phases
**Phase 1**
- Run targeted retrieval from trusted sources
- Generate a structured summary report
- Build an indexed source corpus for traceability

**Phase 2**
- Expose the knowledge base to a conversational model
- Enable Q&A with source‑level provenance and drill‑downs

## Status
Planned.
