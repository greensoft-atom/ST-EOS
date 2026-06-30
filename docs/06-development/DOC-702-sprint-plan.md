# DOC-702 — Sprint Plan (MVP Backlog)

**Document ID:** DOC-702  
**Version:** 2.0  
**Date:** 2026-06-30  
**Sprints:** S0–S6 (14 weeks)  
**Status:** Approved for build  
**Locked decisions:** [00-mvp-decisions.md](../00-mvp-decisions.md) | **Module:** Evaluation Assistant only

---

## 1. Sprint Calendar

Assuming Phase 0 ends Week 8; Sprint 0 starts Week 9:

| Sprint | Week | Goal | SP |
|--------|------|------|-----|
| S0 | 9–10 | Foundation + 6-role RBAC | 21 |
| S1 | 11–12 | Repository + ingestion | 34 |
| S2 | 13–14 | RAG search | 34 |
| S3 | 15–16 | Document review | 34 |
| S4 | 17–18 | Template creation | 34 |
| S5 | 19–20 | Evaluation Assistant (core) | 34 |
| S6 | 21–22 | Evaluation completion + hardening + UAT | 28 |
| **Total** | | | **219** |

*Velocity target: 20–22 SP/sprint. S5–S6 carry Evaluation scope per [DOC-504](../06-modules/DOC-504-evaluation-assistant.md).*

---

## 2. Velocity Assumptions

| Parameter | Value |
|-----------|-------|
| Team size (dev) | 3–4 |
| Sprint length | 2 weeks |
| Target velocity | 20–22 SP |
| Total MVP scope | **219 SP** |

---

## 3. Sprint 0 — Foundation (21 SP)

| ID | Story | SP | Assignee |
|----|-------|-----|----------|
| S0-01 | Monorepo + Docker Compose (postgres, redis, ollama) | 3 | DevOps |
| S0-02 | PostgreSQL + Alembic + pgvector extension | 3 | Backend |
| S0-03 | User model + JWT login/logout/refresh | 5 | Backend |
| S0-04 | RBAC middleware — 6 roles ([DOC-307](../04-architecture/DOC-307-rbac-specification.md)) | 5 | Backend |
| S0-05 | Audit log model + append service (AUD-001–003) | 3 | Backend |
| S0-06 | Health API + LLM status endpoint | 2 | AI |
| S0-07 | Frontend: Vite + login + dashboard shell (MOV-006) | 5 | Frontend |
| S0-08 | CI: lint, test, build on PR | 2 | DevOps |
| S0-09 | Ollama smoke test + staging deploy script | 3 | DevOps + AI |

**Sprint 0 total: 21 SP**

---

## 4. Sprint 1 — Repository & Ingestion (34 SP)

| ID | Story | SP | Assignee |
|----|-------|-----|----------|
| S1-01 | POST /documents multipart upload (50 MB) | 5 | Backend |
| S1-02 | Filesystem storage abstraction | 3 | Backend |
| S1-03 | Document metadata + [DOC-603](../07-data/DOC-603-metadata-standard.md) validation | 3 | Backend |
| S1-04 | Classification required on upload | 3 | Backend |
| S1-05 | GET /documents list + filters | 3 | Backend |
| S1-06 | Document upload UI + drag-drop | 5 | Frontend |
| S1-07 | Document list UI + filters | 5 | Frontend |
| S1-08 | PDF preview component | 3 | Frontend |
| S1-09 | Redis + RQ worker setup | 3 | DevOps |
| S1-10 | PDF text extraction worker | 5 | AI |
| S1-11 | Chunking + embedding + pgvector insert | 5 | AI |
| S1-12 | Processing status API + UI poll | 2 | BE+FE |
| S1-13 | Bulk ingest CLI | 3 | AI |
| S1-14 | Ingest 2000 docs (curator task) | — | Data |

---

## 5. Sprint 2 — RAG Search (34 SP)

| ID | Story | SP | Assignee |
|----|-------|-----|----------|
| S2-01 | POST /search query endpoint | 3 | Backend |
| S2-02 | Query embedding + vector search top-K | 5 | AI |
| S2-03 | RBAC pre-filter on retrieval ([DOC-307](../04-architecture/DOC-307-rbac-specification.md)) | 5 | AI |
| S2-04 | LLM generation with context + citations | 5 | AI |
| S2-05 | Citation post-processor + source panel API | 5 | AI |
| S2-06 | Insufficient evidence threshold | 2 | AI |
| S2-07 | Search UI (SCR-S01–03) | 8 | Frontend |
| S2-08 | Metadata filter UI | 3 | Frontend |
| S2-09 | Audit AUD-006 | 2 | Backend |
| S2-10 | RAG eval harness CLI | 5 | AI |
| S2-11 | **QG-1/QG-2 gate** — eval pass | — | QA |

---

## 6. Sprint 3 — Document Review (34 SP)

| ID | Story | SP | Assignee |
|----|-------|-----|----------|
| S3-01 | POST /reviews job creation | 3 | Backend |
| S3-02 | Review worker queue | 2 | Backend |
| S3-03 | Completeness + format review prompts | 8 | AI |
| S3-04 | Logic + compliance review + policy RAG | 8 | AI |
| S3-05 | Findings JSON schema + validation | 3 | Backend |
| S3-06 | Review wizard UI (SCR-R01–07) | 8 | Frontend |
| S3-07 | Export review PDF/DOCX | 5 | Backend |
| S3-08 | Audit AUD-007 + AUD-016 policy acknowledgment | 3 | Backend |
| S3-09 | Review quality test suite | 5 | QA |

---

## 7. Sprint 4 — Document Creation (34 SP)

| ID | Story | SP | Assignee |
|----|-------|-----|----------|
| S4-01 | Template model + YAML loader | 5 | Backend |
| S4-02 | Template CRUD API (curator) | 3 | Backend |
| S4-03 | Curator: author 5 templates (incl. evaluation summary) | — | Data |
| S4-04 | POST /generate from template + RAG | 8 | AI |
| S4-05 | Creation wizard UI (SCR-S05–07) | 8 | Frontend |
| S4-06 | Draft editor (TipTap/MD) | 5 | Frontend |
| S4-07 | Export draft PDF/DOCX + bibliography | 5 | Backend |
| S4-08 | Audit AUD-008, AUD-009 | 2 | Backend |

---

## 8. Sprint 5 — Evaluation Assistant Core (34 SP)

**Track B only** — Research Assistant deferred to Phase 2B ([ADR-005](../04-architecture/decisions/ADR-005-mvp-module-selection.md)).

| ID | Story | SP | Assignee |
|----|-------|-----|----------|
| S5-B01 | Rubric model + CRUD API | 5 | Backend |
| S5-B02 | `score_rubric` tool + evaluation prompts | 5 | AI |
| S5-B03 | Batch evaluation worker (max 20) + job progress API | 5 | AI + Backend |
| S5-B04 | Comparison matrix API + UI (SCR-E05) | 5 | BE + FE |
| S5-B05 | Ranking engine + UI (SCR-E06) | 4 | AI + FE |
| S5-B06 | Evaluation wizard + scorecard UI (SCR-E01–E04) | 7 | Frontend |
| S5-B07 | Audit AUD-010 on scoring | 3 | Backend |
| S5-B08 | Curator: load 2 rubrics + 10 test submissions | — | Data |

**Sprint 5 total: 34 SP**

*Remaining evaluation screens SCR-E07–E10 complete in Sprint 6.*

---

## 9. Sprint 6 — Evaluation Completion + Hardening (28 SP)

| ID | Story | SP | Assignee |
|----|-------|-----|----------|
| S6-B01 | Reviewer score override UI (SCR-E07) | 5 | Frontend |
| S6-B02 | Chair approval gate (SCR-E08) | 5 | BE + FE |
| S6-B03 | Committee packet export PDF/DOCX (SCR-E09) | 5 | Backend |
| S6-B04 | Rubric manager UI (SCR-E10) | 3 | Frontend |
| S6-B05 | Evaluation golden test suite (10 submissions) | 1 | QA |
| S6-01 | Admin user management + audit log viewer | 3 | Frontend |
| S6-02 | OWASP ZAP scan + backup/restore test #2 | 2 | QA + DevOps |
| S6-03 | UAT scenarios UAT-01–06 | 2 | PM + QA |
| S6-04 | Production docker-compose.prod.yml + error UX | 2 | DevOps + FE |

**Sprint 6 total: 28 SP**

---

## 10. Burndown Target

```text
SP
220 │█
200 │██
180 │████
160 │██████
140 │████████
120 │██████████
100 │████████████
 80 │██████████████
 60 │████████████████
 40 │██████████████████
 20 │████████████████████
  0 │██████████████████████
    S0  S1  S2  S3  S4  S5  S6
```

---

## 11. Removed from MVP Backlog

| Former item | Disposition |
|-------------|-------------|
| S5 Track A (Research Assistant) | Phase 2B |
| Optional PDF preview polish | P1 defer if velocity low |

---

## Related Documents

- [MOV-009](../07-movements/MOV-009-build-mvp-phase1.md)
- [DOC-701](./DOC-701-development-plan.md)
- [DOC-504](../06-modules/DOC-504-evaluation-assistant.md)
- [DOC-205](../03-requirements/DOC-205-traceability-matrix.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial sprint plan |
| 2.0 | 2026-06-30 | Evaluation-only S5–S6; SP rebalance; 6-role RBAC; total 219 SP |
