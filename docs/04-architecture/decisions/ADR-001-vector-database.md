# ADR-001 — Vector Database Selection

**Status:** Accepted (MVP default — validate recall in PoC)  
**Date:** 2026-06-30  
**Deciders:** Tech Lead, AI/RAG Engineer  
**Related:** [DOC-403 RAG Architecture](../../05-ai/DOC-403-rag-architecture.md)

---

## Context

ST-EOS requires vector similarity search over 10,000+ documents (100K+ chunks at pilot scale). Options evaluated: **Qdrant** (dedicated vector DB) vs **pgvector** (PostgreSQL extension).

Pilot operations favor **minimal moving parts** on a single on-prem server with limited DevOps FTE (0.25).

---

## Decision

**Use pgvector** embedded in PostgreSQL 16 for MVP and pilot deployment.

---

## Rationale

| Factor | pgvector | Qdrant |
|--------|----------|--------|
| Operational complexity | Single DB for relational + vectors | Additional service |
| Backup/DR | Same pg_dump pipeline | Separate backup |
| RBAC pre-filter | SQL + metadata join natural | Filter API supported |
| Team skill | PostgreSQL already required | New ops surface |
| Scale (MVP) | Sufficient to ~500K chunks | Higher headroom |

---

## Consequences

**Positive:**
- Simpler Docker Compose stack
- Transactional consistency between metadata and embeddings
- Easier restore story (single DB dump)

**Negative:**
- May need migration to Qdrant or hybrid at 500K+ chunks / Phase 2 scale
- Slightly lower peak QPS than dedicated vector engine

**Mitigation:** Abstract vector store behind `VectorIndex` interface in backend; benchmark recall in PoC (Gate G1).

---

## Validation (PoC — MOV-005)

| Metric | Pass threshold |
|--------|----------------|
| Recall@5 on 50-question eval set | ≥ 70% |
| Query latency p95 (retrieval only) | ≤ 2s |

If pgvector fails Gate G1, supersede this ADR with Qdrant evaluation before Sprint 1.

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-30 | Initial ADR |
