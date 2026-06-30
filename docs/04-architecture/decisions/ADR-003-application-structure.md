# ADR-003 — Application Structure (Monolith vs Microservices)

**Status:** Accepted  
**Date:** 2026-06-30  
**Deciders:** Tech Lead, Program Manager

---

## Context

ST-EOS MVP must ship in 14 weeks with ~5 FTE. Microservices add network, deployment, and observability overhead disproportionate to team size.

---

## Decision

**Modular monolith** — single FastAPI application with internal packages:

```text
apps/backend/          # API, auth, workflow
packages/ai/           # RAG, agents, prompts
packages/ingestion/    # extract, chunk, embed
```

Split criteria for Phase 2: independent scaling need for ingestion workers or LLM gateway under sustained load.

---

## Consequences

- One deploy artifact for MVP
- Clear module boundaries via Python packages enable future extraction
- Async workers (RQ/Celery) for ingestion and batch evaluation — separate **process**, not separate **service**

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-30 | Initial ADR |
