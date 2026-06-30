# ADR-002 — LLM Runtime Selection

**Status:** Accepted (MVP default)  
**Date:** 2026-06-30  
**Deciders:** Tech Lead, AI/RAG Engineer, DevOps

---

## Context

ST-EOS requires **local-only** LLM inference for data sovereignty. Candidates: **Ollama**, **vLLM**, **llama.cpp** server.

MVP team size is small; staging and pilot need reproducible deployment with minimal tuning.

---

## Decision

| Environment | Runtime |
|-------------|---------|
| Development / Sprint 0 | **Ollama** in Docker Compose |
| Staging / Pilot production | **Ollama** default; **vLLM** if batch latency fails acceptance |

---

## Rationale

- Ollama: fastest path to working local inference, model pull workflow, team familiarity
- vLLM: better throughput for batch evaluation (20 submissions) — adopt in Phase 2A if S5 load tests fail

---

## Consequences

- Bind LLM to internal network only (`127.0.0.1` or Docker internal DNS)
- Model files stored on encrypted volume; document air-gap transfer in [DOC-801](../../08-operations/DOC-801-deployment-guide.md)
- All calls logged via AI orchestrator (AUD-006, AUD-007, AUD-010)

---

## Validation

Sprint 0 AC-5: `GET /health` returns LLM status OK.  
Sprint 5: batch evaluation of 5 submissions completes within 30 minutes on pilot hardware.

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-30 | Initial ADR |
