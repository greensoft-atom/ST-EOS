# ADR-004 — Primary LLM Model Selection

**Status:** Proposed — **must validate in PoC (MOV-005)** before Sprint 0  
**Date:** 2026-06-30  
**Deciders:** AI/RAG Engineer, Tech Lead, Pilot Sponsor (inform)

---

## Context

MVP workloads: RAG Q&A, structured JSON review findings, rubric scoring with citations, template generation. Primary pilot language: **English**. Mixed-language corpus possible in metadata; full bilingual UI is Phase 2.

Hardware default: **24 GB VRAM GPU** or **64 GB RAM CPU fallback**.

---

## Proposed Decision

**Primary model:** `qwen2.5:14b` (Ollama) or equivalent GGUF Q4_K_M quantization.

**Fallback (no GPU):** `qwen2.5:7b` — acceptable for PoC and limited pilot if latency disclosed.

---

## Benchmark Protocol (PoC Week 6–7)

Run on **50 real MSTI documents** and **20 evaluation-style prompts**:

| Criterion | Weight | Minimum |
|-----------|--------|---------|
| Citation adherence (JSON schema valid) | 30% | ≥ 80% |
| Rubric scoring coherence (expert review) | 25% | ≥ 70% agreement |
| Review finding quality vs checklist | 25% | ≥ 75% |
| Latency p95 (single query) | 10% | ≤ 15s |
| VRAM/RAM fit on pilot hardware | 10% | Must fit |

**Candidates:** Qwen2.5-14B, Llama-3.1-8B, Mistral-7B — same quantization tier.

---

## Consequences

- Model version pinned in production `.env` and logged in every audit record
- Model change requires regression run of RAG + evaluation golden tests
- Fine-tuning **out of scope** for MVP ([00-mvp-decisions.md](../../00-mvp-decisions.md))

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-30 | Initial ADR |
