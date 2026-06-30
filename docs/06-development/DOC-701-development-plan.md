# DOC-701 — Development Plan

**Document ID:** DOC-701  
**Version:** 2.0  
**Date:** 2026-06-29  
**Status:** Draft  
**Companion docs:** [DOC-702 Sprint Plan](./DOC-702-sprint-plan.md) | [DOC-710 Resource & Budget](./DOC-710-resource-budget-plan.md) | [MOV-009 Build MVP](../07-movements/MOV-009-build-mvp-phase1.md)

---

## 1. Purpose

Define the development approach, **team loading**, **timeline**, **resource requirements**, **cost envelope**, **risk controls**, and **sprint delivery plan** for ST-EOS MVP (Phase 1).

---

## 2. Program Delivery Model

```text
                    ST-EOS Delivery Model
                    ─────────────────────

   Phase 0          Phase 1              Pilot           Phase 2
  (8 weeks)        (14 weeks)           (8 weeks)       (26 weeks)
      │                 │                    │                │
      ▼                 ▼                    ▼                ▼
  Discover ──G1──▶ Build MVP ──G2──▶ Deploy ──G3──▶ Expand
  PoC + UX          S0–S6               Measure          Modules
  Security          199 SP              KPIs             50K docs
```

| Aspect | Decision |
|--------|----------|
| Methodology | Agile/Scrum, 2-week sprints |
| MVP scope | Fixed — change control per [MOV-008](../07-movements/MOV-008-mvp-build-sprint0.md) |
| Architecture | Modular monolith (MVP) |
| Total backlog | **219 SP** ([DOC-702](./DOC-702-sprint-plan.md)) |
| Branch strategy | `main` (stable) + `develop` + `feature/*` |
| Definition of Done | Code reviewed, tested, staged, documented |

---

## 3. Master Timeline (56 Weeks)

```text
Week   1    4    8    10   14   18   22   26   30   38   46   56
       ├────┼────┼────┼────┼────┼────┼────┼────┼────┼────┼────┤
Phase  │ Ph0      │ Ph1 MVP      │Pilot│ Ph2 expansion          │
Move   M0-5  M6-8 │ M9 (S0-S6)   │ M10 │ M11                    │
Gate   G0    G1 G2 │              │ G3  │                        │
```

| Milestone | Week | Criteria |
|-----------|------|----------|
| M-Charter | 1 | DOC-001 signed |
| M-PoC | 7 | G1 pass — RAG metrics |
| M-Sprint0 | 10 | G2 pass — auth + LLM live |
| M-RAG | 14 | Search with citations |
| M-MVP | 22 | UAT pass — all P0 features |
| M-Pilot | 30 | G3 pass — KPI targets |
| M-v1.0 | 56 | Phase 2 complete |

---

## 4. Team Structure & Loading

### 4.1 Phase 1 team (MVP build)

| Role | FTE | Person-weeks (14 wk) | Key deliverables |
|------|-----|---------------------|------------------|
| Program Manager | 0.6 | 8.4 | Scope, demos, gates |
| Tech Lead / Backend | 1.0 | 14 | API, auth, orchestration |
| AI/RAG Engineer | 1.0 | 14 | Ingestion, RAG, agents |
| Frontend Developer | 1.0 | 14 | Portal, workflows |
| Data Engineer / Curator | 0.5 | 7 | Corpus, metadata, templates |
| QA Engineer | 0.5 | 7 | Test harness, UAT (S3+) |
| DevOps | 0.25 | 3.5 | Docker, CI, staging |
| UX Designer | 0.1 | 1.4 | S3–S4 polish |
| **Total** | **~4.95** | **~69.3** | |

### 4.2 Team loading chart

```text
FTE
5 │         ████████████████████████████████
4 │    ████████████████████████████████████████
3 │████████████████████████████████████████████
2 │████████████████████████████████████████████
1 │████████████████████████████████████████████
  └──────────────────────────────────────────▶ Week
    1  2  3  4  5  6  7  8  9 10 11 ... 22
       └─ Phase 0 ─┘└──── Phase 1 MVP ────┘
```

### 4.3 Skill matrix (knowledge requirements)

| Skill | Required level | Team member | Backup |
|-------|----------------|-------------|--------|
| Python / FastAPI | Advanced | Tech lead | AI engineer |
| RAG / embeddings | Advanced | AI engineer | Tech lead |
| React / TypeScript | Intermediate+ | Frontend | — |
| PostgreSQL / SQL | Intermediate | Tech lead | Backend |
| Docker / Linux | Intermediate | DevOps | Tech lead |
| PDF/OCR processing | Intermediate | AI engineer | Data lead |
| S&T domain corpus | Intermediate | Data curator | PM |
| Prompt engineering | Advanced | AI engineer | — |
| Security / RBAC | Intermediate | Tech lead | — |

---

## 5. Infrastructure & Software Resources

### 5.1 Hardware (Phase 1)

| Asset | Spec | Purpose | Cost (USD) |
|-------|------|---------|------------|
| Staging server | 16c / 64GB / 1TB | Integration, demos | $3K–$8K |
| GPU (recommended) | 24GB VRAM | LLM inference | $2.5K–$8K |
| Dev workstations × 4 | 16GB RAM | Development | Existing |
| NAS backup | 2TB | Daily backup | $500–$1.5K |

### 5.2 Software stack

```text
┌─────────────────────────────────────────┐
│ Presentation: React + TS + shadcn/ui    │
├─────────────────────────────────────────┤
│ API: FastAPI + SQLAlchemy + Alembic     │
├─────────────────────────────────────────┤
│ AI: Ollama/vLLM + bge-m3 + custom RAG   │
├─────────────────────────────────────────┤
│ Data: PostgreSQL 16 + pgvector + Redis  │
├─────────────────────────────────────────┤
│ Ops: Docker Compose + GitHub Actions    │
└─────────────────────────────────────────┘
```

All core components: **open source**. Optional tooling budget: $0–$580 (see [DOC-710](./DOC-710-resource-budget-plan.md)).

### 5.3 Knowledge assets (must be ready)

| Asset | Quantity | Ready by | Owner |
|-------|----------|----------|-------|
| MVP document corpus | 3K→10K | Sprint 2 | Data lead |
| Document templates | 5 minimum | Sprint 4 | Curator |
| RAG eval questions | 50 | Sprint 2 | AI lead |
| Review test documents | 20 | Sprint 3 | QA |
| Policy docs for compliance | 10+ | Sprint 3 | Curator |
| Assistant rubric OR research prompts | 1 set | Sprint 5 | Pilot dept |

---

## 6. Cost Summary (Phase 1)

| Category | Low (USD) | High (USD) |
|----------|-----------|------------|
| Personnel (contractor equivalent, 69 pw) | $80,000 | $200,000 |
| Hardware (staging + GPU) | $4,000 | $15,500 |
| Software licenses | $0 | $580 |
| Training / travel prep | $500 | $3,000 |
| Contingency 15% | $12,675 | $32,862 |
| **Phase 1 total** | **$97,175** | **$251,942** |

Full program budget (18 months): **$310K – $727K** — see [DOC-710](./DOC-710-resource-budget-plan.md).

---

## 7. Phase 0 — Pre-Development (8 Weeks)

| Week | Movement | Focus | Output |
|------|----------|-------|--------|
| 1–2 | M0, M1 | Governance, pilot | Charter, pilot scope |
| 2–4 | M2 | Data audit | Corpus inventory |
| 3–4 | M3 | Requirements | Frozen PRD/URS |
| 4–5 | M4 | Architecture | Stack ADRs |
| 5–7 | M5 | RAG PoC | G1 decision |
| 6–7 | M6 | UX | [MOV-006](../07-movements/MOV-006-ux-workflow-design.md) |
| 7–8 | M7 | Security | [MOV-007](../07-movements/MOV-007-security-data-governance.md) |
| 8–10 | M8 | Sprint 0 | [MOV-008](../07-movements/MOV-008-mvp-build-sprint0.md) |

**Phase 0 cost:** $30,200 – $55,000 (cash, indicative)

---

## 8. Phase 1 — Sprint Plan Summary

Detailed stories: [DOC-702](./DOC-702-sprint-plan.md). Execution guide: [MOV-009](../07-movements/MOV-009-build-mvp-phase1.md).

### 8.1 Sprint overview

| Sprint | Weeks | Goal | SP | Demo |
|--------|-------|------|-----|------|
| S0 | 9–10 | Foundation | 21 | Login + LLM health |
| S1 | 11–12 | Repository + ingest | 34 | Upload → indexed |
| S2 | 13–14 | RAG search | 34 | Cited Q&A |
| S3 | 15–16 | Document review | 34 | Review export |
| S4 | 17–18 | Template creation | 34 | Draft export |
| S5 | 19–20 | Evaluation Assistant (core) | 34 | Full eval scoring + comparison |
| S6 | 21–22 | Eval completion + hardening + UAT | 28 | Approval, export, UAT |

### 8.2 Feature delivery map

```text
Sprint:     S0    S1    S2    S3    S4    S5    S6
            │     │     │     │     │     │     │
Auth/RBAC   ████
Repository        ████
Ingestion         ████
RAG                     ████
Review                        ████
Creation                            ████
Assistant                                 ████
Admin/UAT                                       ████
Audit       ██    ██    ██    ██    ██    ██    ████
```

### 8.3 Quality gates

| Gate | Sprint | Metric | Pass |
|------|--------|--------|------|
| QG-1 | S2 | Recall@5 | ≥ 70% |
| QG-2 | S2 | Citation accuracy | ≥ 80% |
| QG-3 | S3 | Review omission detect | ≥ 75% |
| QG-4 | S4 | Draft minor-edit rate | ≥ 60% |
| QG-5 | S6 | UAT scenarios | 5/5 |
| QG-6 | S6 | Security checklist | 12/12 |

Testing detail: [DOC-706](./DOC-706-testing-strategy.md).

---

## 9. Repository Structure

```text
ST-EOS/
├── apps/
│   ├── backend/               # FastAPI
│   └── frontend/              # React
├── packages/
│   ├── ai/                    # RAG, agents, prompts
│   ├── ingestion/             # Extract, chunk, embed
│   └── shared/
├── infra/docker/              # Compose files
├── data/
│   ├── templates/
│   └── eval/
├── docs/                      # Program docs
└── tests/
    ├── unit/
    ├── integration/
    └── eval/
```

---

## 10. Risk Register (Phase 1)

| ID | Risk | L | I | Mitigation | Owner | Trigger |
|----|------|---|---|------------|-------|---------|
| D1 | RAG quality fails at scale | M | H | Weekly eval; metadata QA | AI lead | Recall drops >10% |
| D2 | LLM latency > 30s | H | M | GPU; streaming; 7B fallback | DevOps | p95 > 15s |
| D3 | Ingestion backlog | M | M | Parallel workers; overnight batch | AI lead | Queue > 500 |
| D4 | Frontend behind API | M | M | Mock API; strict sprint scope | Tech lead | >3 open FE stories at sprint end |
| D5 | Scope creep | H | H | Change control; PM gate | PM | Any unprioritized story |
| D6 | Corpus not ready | M | H | Curator starts Week 2 | Data lead | <1000 docs at S2 |
| D7 | Security finding critical | M | H | Scan S3 + S6 | QA | ZAP critical |
| D8 | Team attrition | L | H | Pairing; bus factor docs | PM | Notice given |
| D9 | Pilot changes assistant | L | M | Freeze at S0 kickoff | Sponsor | Request after S3 |
| D10 | GPU supply delay | M | M | CPU + 7B model path | DevOps | No GPU by S2 |

---

## 11. Ceremonies

| Ceremony | When | Duration | Output |
|----------|------|----------|--------|
| Daily standup | Daily | 15 min | Blockers |
| Sprint planning | Biweekly Mon | 2 hr | Sprint backlog |
| Demo to sponsor | Biweekly Fri | 30 min | Feedback log |
| Retrospective | Biweekly | 1 hr | 1–3 improvements |
| Steering | Weekly | 30 min | Decisions |
| RAG eval review | Weekly | 30 min | Metrics dashboard |

---

## 12. Definition of Done

```text
☑ Code reviewed (1+ approver)
☑ Unit tests pass (new code covered)
☑ Integration tests for API changes
☑ OpenAPI updated
☑ Deployed to staging
☑ Audit logging if AI/auth/data change
☑ Product owner accepts
☑ No Critical bugs introduced
```

---

## 13. Phase 2 & Pilot (Forward Reference)

| Phase | Movement | Doc | Duration |
|-------|----------|-----|----------|
| Pilot | MOV-010 | [Pilot Deployment](../07-movements/MOV-010-pilot-deployment.md) | 8 weeks |
| Expand | MOV-011 | [Phase 2](../07-movements/MOV-011-iterate-expand-phase2.md) | 26 weeks |

---

## 14. Immediate Actions

| # | Action | Owner | By |
|---|--------|-------|-----|
| 1 | Approve charter + budget range | Sponsor | Week 1 |
| 2 | Confirm team roster | PM | Week 1 |
| 3 | Start data inventory | Data lead | Week 2 |
| 4 | Schedule MOV-006 UX kickoff | PM | Week 6 |
| 5 | Procure staging server | DevOps | Week 7 |

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial development plan |
| 2.0 | 2026-06-30 | 219 SP backlog; Evaluation S5–S6 split |
