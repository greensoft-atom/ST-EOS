# DOC-702 — Sprint Plan (MVP Backlog)

**Document ID:** DOC-702  
**Version:** 1.0  
**Date:** 2026-06-29  
**Sprints:** S0–S6 (14 weeks)  
**Status:** Draft

---

## 1. Sprint Calendar

Assuming Phase 0 ends Week 8; Sprint 0 starts Week 9:

| Sprint | Dates (example) | Week | Goal | SP |
|--------|-----------------|------|------|-----|
| S0 | Jul 28 – Aug 8 | 9–10 | Foundation | 21 |
| S1 | Aug 11 – Aug 22 | 11–12 | Repository + ingestion | 34 |
| S2 | Aug 25 – Sep 5 | 13–14 | RAG search | 34 |
| S3 | Sep 8 – Sep 19 | 15–16 | Document review | 34 |
| S4 | Sep 22 – Oct 3 | 17–18 | Document creation | 34 |
| S5 | Oct 6 – Oct 17 | 19–20 | Department assistant | 21 |
| S6 | Oct 20 – Oct 31 | 21–22 | Hardening + UAT | 21 |

*Adjust dates to actual kickoff.*

---

## 2. Velocity Assumptions

| Parameter | Value |
|-----------|-------|
| Team size (dev) | 3–4 |
| Sprint length | 2 weeks |
| Target velocity | 18–22 SP |
| Total MVP scope | ~199 SP |

---

## 3. Sprint 0 — Foundation (21 SP)

| ID | Story | SP | Assignee | Depends |
|----|-------|-----|----------|---------|
| S0-01 | Monorepo + Docker Compose all services | 3 | DevOps | — |
| S0-02 | PostgreSQL + Alembic migrations | 3 | Backend | S0-01 |
| S0-03 | User model + register seed admin | 2 | Backend | S0-02 |
| S0-04 | JWT login/logout/refresh | 3 | Backend | S0-03 |
| S0-05 | RBAC middleware + 4 roles | 5 | Backend | S0-04 |
| S0-06 | Audit log model + append service | 3 | Backend | S0-02 |
| S0-07 | Health API + LLM status endpoint | 2 | AI | S0-01 |
| S0-08 | Frontend: Vite + login + layout | 5 | Frontend | — |
| S0-09 | Frontend: dashboard shell (MOV-006) | 3 | Frontend | S0-08 |
| S0-10 | CI: lint, test, build on PR | 2 | DevOps | S0-01 |
| S0-11 | Staging deploy script | 2 | DevOps | S0-10 |
| S0-12 | Ollama in compose + smoke test | 2 | AI | S0-07 |

---

## 4. Sprint 1 — Repository & Ingestion (34 SP)

| ID | Story | SP | Assignee |
|----|-------|-----|----------|
| S1-01 | POST /documents multipart upload | 5 | Backend |
| S1-02 | File storage abstraction (local/MinIO) | 3 | Backend |
| S1-03 | Document metadata model + validation | 3 | Backend |
| S1-04 | Classification enum on upload (MOV-007) | 3 | Backend |
| S1-05 | GET /documents list + filters | 3 | Backend |
| S1-06 | Document upload UI + drag-drop | 5 | Frontend |
| S1-07 | Document list UI + filters | 5 | Frontend |
| S1-08 | PDF preview component | 3 | Frontend |
| S1-09 | Redis + RQ worker setup | 3 | DevOps |
| S1-10 | PDF text extraction worker | 5 | AI |
| S1-11 | Chunking pipeline (configurable) | 5 | AI |
| S1-12 | Embedding + pgvector insert | 5 | AI |
| S1-13 | Processing status API + UI poll | 2 | BE+FE |
| S1-14 | Bulk ingest CLI script | 3 | AI |
| S1-15 | Ingest 2000 docs (curator task) | — | Data |

---

## 5. Sprint 2 — RAG Search (34 SP)

| ID | Story | SP | Assignee |
|----|-------|-----|----------|
| S2-01 | POST /search query endpoint | 3 | Backend |
| S2-02 | Query embedding service | 2 | AI |
| S2-03 | Vector search + top-K | 3 | AI |
| S2-04 | RBAC pre-filter on retrieval | 5 | AI |
| S2-05 | LLM generation with context | 5 | AI |
| S2-06 | Citation post-processor | 5 | AI |
| S2-07 | Insufficient evidence threshold | 2 | AI |
| S2-08 | Search UI (SCR-S01–03) | 8 | Frontend |
| S2-09 | Metadata filter UI | 3 | Frontend |
| S2-10 | Audit AUD-006 | 2 | Backend |
| S2-11 | RAG eval harness CLI | 5 | AI |
| S2-12 | **QG-1/QG-2 gate** — eval pass | — | QA |

---

## 6. Sprint 3 — Document Review (34 SP)

| ID | Story | SP | Assignee |
|----|-------|-----|----------|
| S3-01 | POST /reviews job creation | 3 | Backend |
| S3-02 | Review worker queue | 2 | Backend |
| S3-03 | Completeness review prompt | 5 | AI |
| S3-04 | Format review prompt | 3 | AI |
| S3-05 | Logic review prompt | 5 | AI |
| S3-06 | Compliance review + policy RAG | 5 | AI |
| S3-07 | Findings JSON schema + validation | 3 | Backend |
| S3-08 | Review wizard UI (SCR-R01–07) | 8 | Frontend |
| S3-09 | Export review PDF/DOCX | 5 | Backend |
| S3-10 | Audit AUD-007 | 2 | Backend |
| S3-11 | Review quality test suite | 5 | QA |

---

## 7. Sprint 4 — Document Creation (34 SP)

| ID | Story | SP | Assignee |
|----|-------|-----|----------|
| S4-01 | Template model + YAML loader | 5 | Backend |
| S4-02 | Template CRUD API (curator) | 3 | Backend |
| S4-03 | Curator: author 5 templates | — | Data |
| S4-04 | POST /generate from template | 5 | AI |
| S4-05 | Creation wizard UI | 8 | Frontend |
| S4-06 | Draft editor (TipTap/MD) | 5 | Frontend |
| S4-07 | Bibliography generator | 3 | AI |
| S4-08 | Export draft PDF/DOCX | 5 | Backend |
| S4-09 | Audit AUD-008, AUD-009 | 2 | Backend |

---

## 8. Sprint 5 — Assistant (21 SP)

### Track A — Research

| ID | Story | SP |
|----|-------|-----|
| S5-A01 | Agent config research_assistant | 2 |
| S5-A02 | Literature review workflow | 5 |
| S5-A03 | Proposal generation workflow | 5 |
| S5-A04 | Gap analysis workflow | 5 |
| S5-A05 | Assistant UI task picker | 5 |

### Track B — Evaluation Assistant (Government executive pilot — default)

| ID | Story | SP |
|----|-------|-----|
| S5-B01 | Rubric model + CRUD | 5 |
| S5-B02 | score_rubric tool | 5 |
| S5-B03 | Single + batch scoring | 5 |
| S5-B04 | Comparison matrix UI | 5 |
| S5-B05 | Human approval gate | 3 |

---

## 9. Sprint 6 — Hardening (21 SP)

| ID | Story | SP |
|----|-------|-----|
| S6-01 | Admin user management UI | 5 |
| S6-02 | Audit log viewer | 3 |
| S6-03 | Global error boundaries + toasts | 3 |
| S6-04 | Performance: embed batch tuning | 3 |
| S6-05 | OWASP ZAP scan + fixes | 5 |
| S6-06 | Backup cron + restore test | 3 |
| S6-07 | User quick-start PDF | 2 |
| S6-08 | Production docker-compose.prod.yml | 3 |
| S6-09 | UAT 5 scenarios × 3 users | 5 |

---

## 10. Burndown Target

```text
SP
200 │█
180 │██
160 │████
140 │██████
120 │████████
100 │██████████
 80 │████████████
 60 │██████████████
 40 │████████████████
 20 │██████████████████
  0 │████████████████████
    S0  S1  S2  S3  S4  S5  S6
```

---

## Related Documents

- [MOV-009](../07-movements/MOV-009-build-mvp-phase1.md)
- [DOC-701](./DOC-701-development-plan.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial sprint plan |
