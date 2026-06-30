# ST-EOS MVP — Locked Program Decisions

**Document type:** Canonical decision record  
**Version:** 1.0  
**Date:** 2026-06-30  
**Status:** Approved for planning and build  
**Authority:** Supersedes conflicting text in any draft document dated before 2026-06-30

---

## 1. Purpose

This document is the **single source of truth** for program decisions that were previously stated inconsistently across the documentation set. When another document conflicts with this record, **this document wins** until formally amended.

---

## 2. Phase & Timeline Naming (Locked)

```text
Phase 0 — Discovery & PoC           Weeks 1–8
Phase 1 — MVP Build                 Weeks 9–22
Pilot   — Deployment & Measurement  Weeks 23–30
Phase 2 — Module Expansion          Weeks 31–56
```

**Do not use:** "Phase 2 = Pilot" or "Phase 3 = Expansion" (deprecated labels in DOC-001 v1.1).

---

## 3. Pilot Institution (Locked)

| Field | Decision |
|-------|----------|
| Anchor | Ministry of Science, Technology and Innovation (MSTI) |
| Primary department | Research Programs and Grant Administration |
| MVP module | **Evaluation Assistant** (Sprint 5) |
| UI language (MVP) | **English** |
| Deployment | On-premise, local LLM only |
| Formal MOU | Pending — Gate G0 partial until signed |

---

## 4. MVP Module Decision (Locked)

| Decision | Value | Rationale |
|----------|-------|-----------|
| Sprint 5 assistant | **Evaluation Assistant only** | MSTI W1/W2 workflows; executive ROI |
| Research Assistant | **Phase 2B** (after Gate G3) | Not in MVP scope |
| Planning Assistant (full) | **Phase 2B/C** | Template creation covers W3 in MVP |

See [ADR-005](./04-architecture/decisions/ADR-005-mvp-module-selection.md).

---

## 5. Official Pilot Workflows (Locked)

| ID | Workflow | Primary KPI (time reduction) |
|----|----------|------------------------------|
| W1 | Grant/program pre-screening | −50% |
| W2 | Committee evaluation scoring | −30% |
| W3 | Annual S&T plan/report section drafting | −40% |

Full KPI table: [DOC-PILOT-001 §7](./01-business/DOC-PILOT-001-government-executive-pilot-scope.md).

---

## 6. Pilot Success Metrics (Locked — Canonical KPIs)

| KPI | Target | Source of truth |
|-----|--------|-----------------|
| Weekly active users | ≥ 30 | Enrolled 40–70; active ≥ 30 |
| Documents indexed | ≥ 10,000 | |
| AI queries / week | ≥ 100 | |
| Reviews completed (pilot period) | ≥ 50 | |
| Evaluations scored | ≥ 20 submissions | |
| User trust (survey 1–5) | ≥ 3.8 | Gate G3 minimum: ≥ 3.5 |
| System uptime | ≥ 99% | |
| Workflows hitting time target | ≥ 2 of 3 | Gate G3 |

---

## 7. Technology Stack (Locked for MVP Build)

| Layer | Decision | ADR |
|-------|----------|-----|
| Vector store | **pgvector** (PostgreSQL 16 extension) | [ADR-001](./04-architecture/decisions/ADR-001-vector-database.md) |
| LLM runtime | **Ollama** (staging/pilot); vLLM optional Phase 2 | [ADR-002](./04-architecture/decisions/ADR-002-llm-runtime.md) |
| Application structure | **Modular monolith** (FastAPI) | [ADR-003](./04-architecture/decisions/ADR-003-application-structure.md) |
| Primary LLM model | **Qwen2.5-14B** (quantized if VRAM limited) | [ADR-004](./04-architecture/decisions/ADR-004-primary-llm-model.md) |
| Object storage | **Filesystem** (`/data/documents`); MinIO Phase 2 | |
| Embeddings | **bge-m3** (benchmark in PoC; change via ADR only) | |
| Frontend | React 18 + TypeScript + shadcn/ui | |
| Backend | FastAPI + SQLAlchemy + Alembic | |

PoC may benchmark alternatives; **change requires new ADR** after Gate G1.

---

## 8. RBAC Model (Locked)

MVP uses **6 roles** mapped from generic and evaluation-specific needs:

| Role | Code | Description |
|------|------|-------------|
| Administrator | `admin` | Full system access |
| Curator | `curator` | Corpus, templates, rubrics |
| Program Officer | `program_officer` | Upload, pre-screen, run evaluations |
| Committee Reviewer | `committee_reviewer` | Edit scores, comment |
| Committee Chair | `committee_chair` | Approve and export committee packets |
| General User | `user` | Search, review, create (non-restricted) |

Full permission matrix: [DOC-307 RBAC Specification](./04-architecture/DOC-307-rbac-specification.md).

Legacy 4-role docs (admin, curator, reviewer, user) are **superseded** by DOC-307.

---

## 9. MVP Backlog Sizing (Locked)

| Sprint | SP | Focus |
|--------|-----|-------|
| S0 | 21 | Foundation |
| S1 | 34 | Repository + ingestion |
| S2 | 34 | RAG search |
| S3 | 34 | Document review |
| S4 | 34 | Template creation |
| S5 | 34 | Evaluation Assistant (core) |
| S6 | 28 | Evaluation completion + hardening + UAT |
| **Total** | **219** | ~20 SP/sprint velocity; 11 weeks active dev in S1–S6 |

Sprint detail: [DOC-702](./06-development/DOC-702-sprint-plan.md).

---

## 10. Requirements Scope (Locked)

- **Must deliver:** All URS items mapped to Evaluation MVP in [DOC-205](./03-requirements/DOC-205-traceability-matrix.md).
- **Research Assistant URS (URS-050–054):** Phase 2 — not MVP acceptance criteria.
- **SSO/LDAP:** Phase 2A unless MSTI IT mandates earlier (change request + budget).

---

## 11. Document Hierarchy

When planning or building, read in this order:

1. This document (`00-mvp-decisions.md`)
2. [DOC-PILOT-001](./01-business/DOC-PILOT-001-government-executive-pilot-scope.md)
3. [DOC-504 Evaluation Assistant](./06-modules/DOC-504-evaluation-assistant.md)
4. [DOC-702 Sprint Plan](./06-development/DOC-702-sprint-plan.md)
5. [DOC-205 Traceability Matrix](./03-requirements/DOC-205-traceability-matrix.md)

---

## 12. Amendment Process

| Change type | Approver |
|-------------|----------|
| Wording only | Program Manager |
| KPI, module, or phase change | Executive Sponsor + PM |
| Stack change | Tech Lead + ADR |
| Scope increase | Sponsor + change control ([MOV-008](./07-movements/MOV-008-mvp-build-sprint0.md) §11) |

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-30 | Initial locked decisions; consolidation of audit fixes |
