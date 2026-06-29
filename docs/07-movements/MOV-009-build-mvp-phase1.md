# MOV-009 — Build MVP (Phase 1 Execution)

**Movement ID:** MOV-009  
**Phase:** Phase 1 — Build  
**Timeline:** Weeks 9–22 (Sprint 0 through Sprint 6)  
**Duration:** 14 weeks  
**Owner:** Tech Lead  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Ready for execution (after Gate G2)

---

## 1. Purpose

Execute the ST-EOS MVP build across **7 sprints (S0–S6)** delivering a pilot-ready platform with: repository, RAG search, document review, template creation, one department assistant, security controls, and audit logging.

**Rule:** No scope additions without change control. Weekly demos to sponsor.

---

## 2. Phase 1 Timeline Overview

```text
Week:  9  10  11  12  13  14  15  16  17  18  19  20  21  22
       ├──S0──┤├──S1──┤├──S2──┤├──S3──┤├──S4──┤├──S5──┤├──S6──┤
       Found  Repo   RAG   Review Create Asst  Pilot
                              MVP FEATURE COMPLETE ────────▶ M6
```

| Milestone | Week | Deliverable |
|-----------|------|-------------|
| M0 Environment | 10 | Sprint 0 complete |
| M1 Searchable corpus | 12 | Ingestion + browse |
| M2 RAG live | 14 | Cited Q&A |
| M3 Review live | 16 | Review export |
| M4 Creation live | 18 | Template drafts |
| M5 Assistant live | 20 | Research OR Evaluation |
| M6 MVP release | 22 | UAT passed → MOV-010 |

---

## 3. Team & Resources (Full Phase 1)

### 3.1 Human resources (14 weeks)

| Role | FTE | Weeks | Person-weeks | Primary sprints |
|------|-----|-------|--------------|-----------------|
| Program Manager | 0.6 | 14 | 8.4 | All — demos, scope |
| Tech Lead / Backend | 1.0 | 14 | 14 | S0–S6 |
| AI/RAG Engineer | 1.0 | 14 | 14 | S1–S6 (heavy S1–S3) |
| Frontend Developer | 1.0 | 14 | 14 | S0–S6 |
| Data Engineer / Curator | 0.5 | 14 | 7 | S1–S2 corpus load |
| QA Engineer | 0.5 | 10 | 5 | S3–S6 |
| DevOps | 0.25 | 14 | 3.5 | S0, S2, S6 |
| UX Designer | 0.1 | 4 | 0.4 | S3–S4 polish |
| **Total** | **~4.95** | | **~66 FTE-weeks** | |

### 3.2 Hardware — staging/production-like (Phase 1)

| Component | Specification | Qty | Est. cost (USD) |
|-----------|---------------|-----|-----------------|
| Application server | 16 cores, 64 GB RAM, 1 TB NVMe | 1 | $3,000–$6,000 |
| GPU server (recommended) | RTX 4090 24GB or A5000 | 1 | $2,500–$8,000 |
| NAS/backup | 2 TB redundant | 1 | $500–$1,500 |
| Network | Gigabit LAN, VPN | — | Existing |
| Dev machines | 4 × 16 GB workstations | 4 | Existing/sunk |

**Without GPU:** Use Qwen2.5-7B on CPU — acceptable for pilot but 3–5× slower.

### 3.3 Software licenses (Phase 1)

| Software | Cost | Notes |
|----------|------|-------|
| PostgreSQL, Redis, Ollama | $0 | Open source |
| React, FastAPI, shadcn | $0 | Open source |
| GitHub / GitLab | $0–$400 | Team plan optional |
| Figma | $0–$180 | 3 months |
| Monitoring (Grafana/Prometheus) | $0 | Self-hosted |
| **Total software** | **$0–$580** | |

### 3.4 Knowledge assets consumed

| Asset | When | Owner |
|-------|------|-------|
| MVP corpus 3,000–10,000 docs | Sprint 1–2 | Data lead |
| 5+ templates | Sprint 4 | Curator |
| 50 RAG eval questions | Sprint 2+ | AI lead |
| 20 review test docs | Sprint 3 | QA + curator |
| Evaluation rubric OR research prompts | Sprint 5 | Pilot dept |

---

## 4. Phase 1 Cost Summary (Indicative)

| Category | Low (USD) | High (USD) | Assumptions |
|----------|-----------|------------|-------------|
| Hardware (one-time) | $4,000 | $15,500 | GPU optional on low end |
| Software licenses | $0 | $580 | |
| Personnel (contractor equiv.) | $80,000 | $200,000 | 66 person-weeks, region varies |
| Personnel (internal) | — | — | Absorbed salary |
| Pilot travel/training prep | $500 | $3,000 | |
| Contingency 15% | $12,675 | $32,862 | |
| **Total (cash, excl. internal salary)** | **$97,175** | **$251,942** | |

*See [DOC-710](../06-development/DOC-710-resource-budget-plan.md) for full program budget.*

---

## 5. Sprint-by-Sprint Execution Plan

### Sprint 0 — Foundation (Weeks 9–10)

**Goal:** Runnable skeleton — see [MOV-008](./MOV-008-mvp-build-sprint0.md)

| Metric | Target |
|--------|--------|
| Story points | 21 |
| Demo | Login + dashboard + LLM health |

---

### Sprint 1 — Document Repository & Ingestion (Weeks 11–12)

**Goal:** Upload PDF → extract → chunk → embed → searchable index

```text
Upload Flow (Sprint 1 target)
────────────────────────────
User → POST /documents → Store file → Queue job
                              │
                         Worker pipeline
                              │
         ┌────────────────────┼────────────────────┐
         ▼                    ▼                    ▼
    Extract text          Chunk text           Embed chunks
         │                    │                    │
         └────────────────────┴────────────────────┘
                              ▼
                      Vector index + metadata
                              ▼
                      status = INDEXED
```

| Story | SP | Owner | Acceptance |
|-------|-----|-------|------------|
| S1-01 Upload API | 5 | Backend | 50 MB PDF ok |
| S1-02 Storage | 3 | Backend | Immutable original |
| S1-03 Metadata | 3 | Backend | Required fields enforced |
| S1-04 Classification | 3 | Backend | Default Internal |
| S1-05 List UI | 5 | Frontend | Filter by type |
| S1-06 PDF preview | 3 | Frontend | In-browser |
| S1-07 Worker queue | 5 | AI/DevOps | Redis job |
| S1-08 Extraction | 5 | AI | 95% text-native PDFs |
| S1-09 Embed pipeline | 5 | AI | pgvector insert |
| S1-10 Status UI | 2 | Frontend | Real-time poll |

**Sprint 1 corpus target:** 2,000 documents indexed  
**Risk focus:** OCR failures, large PDF timeouts

**Demo:** Upload thesis PDF → appears in repository → status "Indexed"

---

### Sprint 2 — RAG Search (Weeks 13–14)

**Goal:** Natural language Q&A with citations and access filtering

```text
RAG Query Path
──────────────
Query → Embed → Vector search (top-20)
                    │
              Metadata pre-filter (RBAC + class)
                    │
              Rerank → top-5 chunks
                    │
              LLM + citation prompt → Answer + [1][2]
                    │
              Audit log AUD-006
```

| Story | SP | Owner | Acceptance |
|-------|-----|-------|------------|
| S2-01 Query embed + search | 5 | AI | < 2s retrieval |
| S2-02 RBAC retrieval filter | 5 | AI | No leak test pass |
| S2-03 LLM generation | 5 | AI | Cited answer |
| S2-04 Search UI | 5 | Frontend | MOV-006 SCR-S01–03 |
| S2-05 Insufficient evidence | 2 | AI | Threshold handled |
| S2-06 Audit logging | 3 | Backend | AUD-006 |
| S2-07 Filters UI | 3 | Frontend | Type, date |
| S2-08 Eval harness | 5 | AI | Recall@5 ≥ 70% |

**Sprint 2 corpus target:** 5,000 documents  
**Quality gate:** Eval harness must pass PoC thresholds before Sprint 3

**Demo:** Ask domain question → answer with 3+ citations → click source

---

### Sprint 3 — Document Review (Weeks 15–16)

**Goal:** Structured AI review with export

| Review type | Checks | Output |
|-------------|--------|--------|
| Completeness | Required sections vs template | Missing section list |
| Format | Headings, numbering, length | Format deviations |
| Logic | Contradictions, unsupported claims | Flagged passages |
| Compliance | Policy RAG match | Compliance gaps |

| Story | SP | Owner |
|-------|-----|-------|
| S3-01 Review job API | 3 | Backend |
| S3-02 Completeness + format | 8 | AI |
| S3-03 Logic + compliance | 8 | AI |
| S3-04 Findings schema | 3 | Backend |
| S3-05 Review UI (MOV-006) | 8 | Frontend |
| S3-06 Export PDF/DOCX | 5 | Backend |
| S3-07 Audit AUD-007 | 2 | Backend |
| S3-08 Quality test suite | 5 | QA |

**Demo:** Submit research proposal → 4-type review → export report

---

### Sprint 4 — Document Creation (Weeks 17–18)

**Goal:** Template-based RAG-augmented document generation

| Template (MVP minimum) | Department |
|------------------------|------------|
| Research proposal | Research |
| Literature review summary | Research |
| Evaluation summary | Evaluation |
| Meeting minutes | All |
| Progress report | All |

| Story | SP | Owner |
|-------|-----|-------|
| S4-01 Template registry | 5 | Backend |
| S4-02 Load 5 templates | 3 | Curator |
| S4-03 Creation wizard UI | 8 | Frontend |
| S4-04 RAG generation | 8 | AI |
| S4-05 Draft editor | 5 | Frontend |
| S4-06 Export + bibliography | 5 | Backend |

**Demo:** Create research proposal from template with 5+ citations

---

### Sprint 5 — Department Assistant (Weeks 19–20)

**Track A — Research Assistant**

```text
Research Assistant Tasks
────────────────────────
├── Literature review (topic → cited summary)
├── Proposal generation (params → full draft)
├── Gap analysis (topic → gap list + sources)
└── Methodology suggestion (topic → methods + examples)
```

**Track B — Evaluation Assistant**

```text
Evaluation Assistant Tasks
──────────────────────────
├── Configure rubric (criteria + weights)
├── Score submission (per-criterion + evidence)
├── Compare submissions (matrix)
├── Rank list (ordered + justification)
└── Human approval gate (export blocked until approve)
```

| Story | SP | Track |
|-------|-----|-------|
| S5-01 Task picker UI | 3 | Both |
| S5-02 Primary workflow | 8 | A or B |
| S5-03 Secondary workflow | 5 | A or B |
| S5-04 Tertiary workflow | 5 | A or B |
| S5-05 Audit + disclaimer | 2 | Both |

**Demo:** End-to-end assistant task with institutional sources

---

### Sprint 6 — Hardening & Pilot Prep (Weeks 21–22)

**Goal:** Production-like stability, security checklist, UAT

| Workstream | Tasks |
|------------|-------|
| Performance | Query caching, batch embed tuning |
| Security | OWASP scan, checklist 12/12 |
| Operations | Backup job, restore drill #2 |
| Documentation | Admin guide draft, user quick-start |
| UAT | 5 scenarios × 3 champion users |
| Data | Full MVP corpus 10,000 docs |

| Story | SP | Owner |
|-------|-----|-------|
| S6-01 Admin dashboard | 5 | Frontend |
| S6-02 Audit viewer | 3 | Frontend |
| S6-03 Error UX | 3 | Frontend |
| S6-04 Performance | 5 | AI + Backend |
| S6-05 Security scan fixes | 5 | Tech lead |
| S6-06 Backup/restore | 3 | DevOps |
| S6-07 User docs | 3 | PM |
| S6-08 Deploy package | 3 | DevOps |
| S6-09 UAT | 5 | QA + PM |

**Exit:** MVP signed off → handoff to [MOV-010](./MOV-010-pilot-deployment.md)

---

## 6. Velocity & Burndown Expectations

| Sprint | Planned SP | Cumulative | Notes |
|--------|------------|------------|-------|
| S0 | 21 | 21 | Foundation |
| S1 | 34 | 55 | Heaviest infra |
| S2 | 34 | 89 | RAG quality gate |
| S3 | 34 | 123 | |
| S4 | 34 | 157 | |
| S5 | 21 | 178 | |
| S6 | 21 | 199 | Buffer in S6 |

**If velocity < 18 SP/sprint:** Drop P1 stories (PDF preview polish, extra templates).

---

## 7. Quality Gates (Phase 1)

| Gate | Sprint | Metric | Pass |
|------|--------|--------|------|
| QG-1 | S2 | Recall@5 | ≥ 70% |
| QG-2 | S2 | Citation accuracy | ≥ 80% |
| QG-3 | S3 | Review omission detection | ≥ 75% |
| QG-4 | S4 | Draft minor-edit rate | ≥ 60% |
| QG-5 | S6 | UAT scenarios | 5/5 pass |
| QG-6 | S6 | Security checklist | 12/12 |

---

## 8. Risk Register (Phase 1)

| ID | Risk | L | I | Mitigation | Owner |
|----|------|---|---|------------|-------|
| R1 | RAG quality regresses at scale | M | H | Weekly eval; curator fixes metadata | AI lead |
| R2 | LLM latency unacceptable | H | M | GPU; smaller model; streaming UI | DevOps |
| R3 | Ingestion backlog at 10K docs | M | M | Parallel workers; batch overnight | AI lead |
| R4 | Frontend falls behind backend | M | M | API-first; mock UI early | Tech lead |
| R5 | Assistant scope too large | M | H | 3 tasks only in S5 | PM |
| R6 | Key developer leaves | L | H | Pair programming; docs | PM |
| R7 | Pilot changes assistant choice | L | M | Decide at S0; freeze | Sponsor |
| R8 | Security finding critical late | M | H | Scan at S3, not S6 only | QA |

---

## 9. Weekly Demo Schedule (to Sponsor)

| Week | Demo focus |
|------|------------|
| 10 | Login, dashboard, LLM health |
| 12 | Upload + indexed document |
| 14 | RAG search with citations |
| 16 | Document review export |
| 18 | Template creation export |
| 20 | Assistant workflow |
| 22 | Full MVP walkthrough + UAT results |

---

## 10. Exit Criteria (Movement 9 Complete)

- [ ] All P0 PRD requirements implemented
- [ ] Quality gates QG-1 through QG-6 passed
- [ ] 10,000+ documents indexed (or pilot-agreed minimum)
- [ ] Security checklist complete
- [ ] UAT sign-off from 3 champion users
- [ ] Deployment package ready for MOV-010
- [ ] Known issues log with severities (no open Critical)

---

## Related Documents

- [MOV-008 Sprint 0](./MOV-008-mvp-build-sprint0.md)
- [MOV-010 Pilot Deployment](./MOV-010-pilot-deployment.md)
- [DOC-701](../06-development/DOC-701-development-plan.md)
- [DOC-702 Sprint Plan](../06-development/DOC-702-sprint-plan.md)
- [DOC-706 Testing Strategy](../06-development/DOC-706-testing-strategy.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial detailed movement doc |
