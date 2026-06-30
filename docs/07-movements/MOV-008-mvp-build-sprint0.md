# MOV-008 — MVP Build Plan & Sprint 0

**Movement ID:** MOV-008  
**Phase:** Phase 0 exit / Phase 1 entry  
**Timeline:** Week 8 (+ Sprint 0 weeks 9–10)  
**Duration:** 1 week planning + 2 weeks Sprint 0  
**Owner:** Program Manager + Tech Lead  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Ready for execution

---

## 1. Purpose

Convert frozen requirements, architecture, UX, and security baseline into an **executable backlog** and deliver **Sprint 0** — a runnable platform skeleton that proves the team can build and deploy ST-EOS.

This movement is the **Gate G2** decision point: Go → MOV-009; No-Go → fix gaps, do not scale build.

---

## 2. Movement Structure

```text
MOV-008 = Planning Week (W8) + Sprint 0 (W9–W10)
────────────────────────────────────────────────

Week 8 (Planning)                    Weeks 9–10 (Sprint 0)
┌─────────────────────┐              ┌─────────────────────┐
│ Backlog grooming    │              │ Repo + Docker       │
│ Environment setup   │    ───▶      │ Auth + RBAC         │
│ CI/CD pipeline      │              │ DB + migrations     │
│ Sprint 0 kickoff    │              │ Frontend shell      │
│ Team commitments    │              │ LLM smoke test      │
└─────────────────────┘              └─────────────────────┘
```

---

## 3. Prerequisites (must be complete)

| Movement / Doc | Gate item |
|----------------|-----------|
| MOV-003 | PRD/URS signed |
| MOV-004 | Stack ADRs approved |
| MOV-005 | RAG PoC Go decision |
| MOV-006 | Wireframes approved |
| MOV-007 | RBAC + audit spec ready |
| DOC-701 | Development plan reviewed |

---

## 4. Resources — Planning Week (W8)

### 4.1 Human resources

| Role | FTE | Days (W8) | Tasks |
|------|-----|-----------|-------|
| Program Manager | 0.8 | 5 | Backlog, ceremonies, gate pack |
| Tech Lead | 1.0 | 5 | Repo, CI, ADR finalization |
| AI/RAG Engineer | 0.5 | 3 | LLM container, eval harness stub |
| Frontend Developer | 0.5 | 3 | Frontend scaffold plan |
| Data Engineer | 0.3 | 2 | Sample corpus staging |
| QA | 0.2 | 1 | Test strategy outline |
| DevOps | 0.5 | 3 | Docker Compose, staging server |

### 4.2 Hardware — dev & staging (Sprint 0)

| Environment | Spec (minimum) | Purpose |
|-------------|----------------|---------|
| Dev workstation × 4 | 16 GB RAM, 4 cores | Developer machines |
| Shared dev server | 32 GB RAM, 8 cores, 500 GB SSD | CI runner + integration |
| Staging server | 64 GB RAM, 16 cores, 1 TB SSD | Sprint demos |
| GPU (optional S0) | 12 GB+ VRAM | LLM smoke test; CPU ok for S0 |

### 4.3 Software stack (locked for Sprint 0)

```text
┌─────────────────────────────────────────┐
│ Frontend: React 18 + TypeScript + Vite   │
│ UI: shadcn/ui + Tailwind CSS            │
├─────────────────────────────────────────┤
│ Backend: FastAPI + Python 3.11+           │
│ ORM: SQLAlchemy 2.x                     │
│ Auth: JWT + bcrypt                      │
├─────────────────────────────────────────┤
│ DB: PostgreSQL 16 (+ pgvector ext)      │
│ Queue: Redis + RQ (or Celery)           │
│ LLM: Ollama (dev) / vLLM (staging opt)  │
├─────────────────────────────────────────┤
│ Infra: Docker Compose, GitHub Actions   │
└─────────────────────────────────────────┘
```

---

## 5. Cost Estimate (MOV-008 + Sprint 0)

| Item | Low | High | Notes |
|------|-----|------|-------|
| Staging server (one-time) | $2,000 | $8,000 | Or existing VM |
| GPU card (if purchased) | $800 | $2,500 | Optional for S0 |
| GitHub Teams / CI minutes | $0 | $400 | Free tier often sufficient |
| Domain/internal cert | $0 | $200 | |
| Team labor (2.5 weeks × 4 FTE)* | internal | internal | *See DOC-710 |
| **Incremental hardware** | **$2,800** | **$11,100** | |

---

## 6. Week 8 — Day-by-Day Planning Schedule

| Day | Activity | Owner | Output |
|-----|----------|-------|--------|
| W8-D1 | Gate G1 review (PoC results) | PM + AI lead | Go/No-Go memo |
| W8-D2 | Backlog creation from PRD | PM + Tech lead | Jira/Linear backlog |
| W8-D3 | Story pointing; Sprint 0–2 plan | Full team | Sprint plan |
| W8-D4 | Repo init; Docker Compose skeleton | Tech lead | `develop` branch |
| W8-D5 | CI pipeline first run | DevOps | Green build badge |
| W8-D5 | Sprint 0 kickoff | PM | Sprint goal committed |

---

## 7. Product Backlog Summary (MVP)

### 7.1 Epic breakdown

```text
EPIC-01 Platform Foundation     (Sprint 0)     21 SP
EPIC-02 Document Repository     (Sprint 1)     34 SP
EPIC-03 RAG Search              (Sprint 2)     34 SP
EPIC-04 Document Review         (Sprint 3)     34 SP
EPIC-05 Document Creation       (Sprint 4)     34 SP
EPIC-06 Department Assistant    (Sprint 5)     21 SP
EPIC-07 Hardening & Pilot Prep  (Sprint 6)     21 SP
────────────────────────────────────────────────────
Total estimated:                          ~219 SP
Velocity assumption (team of 4):          ~20 SP/sprint
```

### 7.2 Priority stack (first 30 stories)

| Rank | Story ID | Title | Epic | SP | Sprint |
|------|----------|-------|------|-----|--------|
| 1 | S0-01 | Monorepo + Docker Compose | E01 | 3 | S0 |
| 2 | S0-02 | PostgreSQL + migrations | E01 | 3 | S0 |
| 3 | S0-03 | User model + JWT auth | E01 | 5 | S0 |
| 4 | S0-04 | RBAC middleware | E01 | 5 | S0 |
| 5 | S0-05 | Audit log table + service | E01 | 3 | S0 |
| 6 | S0-06 | Health + version API | E01 | 1 | S0 |
| 7 | S0-07 | Frontend shell + auth UI | E01 | 5 | S0 |
| 8 | S0-08 | CI: lint, test, build | E01 | 2 | S0 |
| 9 | S0-09 | Ollama connection smoke test | E01 | 2 | S0 |
| 10 | S0-10 | Staging deploy script | E01 | 2 | S0 |
| 11 | S1-01 | Document upload API | E02 | 5 | S1 |
| 12 | S1-02 | Object storage integration | E02 | 3 | S1 |
| 13 | S1-03 | Metadata CRUD | E02 | 3 | S1 |
| 14 | S1-04 | Classification on upload | E02 | 3 | S1 |
| 15 | S1-05 | Document list UI | E02 | 5 | S1 |
| 16 | S1-06 | PDF preview | E02 | 3 | S1 |
| 17 | S1-07 | Ingestion worker skeleton | E02 | 5 | S1 |
| 18 | S1-08 | Text extraction (PDF) | E02 | 5 | S1 |
| 19 | S1-09 | Chunk + embed pipeline | E02 | 5 | S1 |
| 20 | S1-10 | Processing status UI | E02 | 2 | S1 |

*(Full backlog: see [DOC-702 Sprint Plan](../06-development/DOC-702-sprint-plan.md))*

---

## 8. Sprint 0 — Detailed Plan (Weeks 9–10)

### 8.1 Sprint goal

> A developer or demo user can run `docker compose up`, log in as admin, see the dashboard shell, and receive a response from the local LLM via an authenticated API health endpoint — with audit log recording the session.

### 8.2 Sprint 0 architecture target

```text
docker compose up
─────────────────
┌────────────┐     ┌────────────┐     ┌────────────┐
│  frontend  │────▶│   backend  │────▶│ postgres   │
│  :5173     │     │   :8000    │     │ :5432      │
└────────────┘     └─────┬──────┘     └────────────┘
                         │
                    ┌────▼────┐     ┌────────────┐
                    │  redis  │     │  ollama    │
                    │  :6379  │     │  :11434    │
                    └─────────┘     └────────────┘
```

### 8.3 Sprint 0 task board

| Day | Backend | Frontend | DevOps | AI |
|-----|---------|----------|--------|-----|
| S0-D1 | Project scaffold, DB models | Vite + React init | Docker Compose | — |
| S0-D2 | Auth endpoints | Login page | CI workflow | Ollama in compose |
| S0-D3 | RBAC middleware | Dashboard layout | pgvector ext | LLM client wrapper |
| S0-D4 | Audit service | Route guards | Staging server | Smoke test endpoint |
| S0-D5 | Integration tests | Dashboard widgets | Deploy staging | — |
| S0-D6 | Bug fixes | UI polish | Backup script stub | — |
| S0-D7 | Code review | Code review | Docs | — |
| S0-D8 | Sprint demo prep | Demo prep | Demo env | Demo |
| S0-D9 | Retrospective | Retro | — | — |
| S0-D10 | Buffer / debt paydown | — | — | — |

### 8.4 Sprint 0 acceptance criteria

| # | Criterion | Verification |
|---|-----------|--------------|
| AC-1 | `docker compose up` starts all services | Manual + CI |
| AC-2 | Login returns JWT; invalid creds rejected | Integration test |
| AC-3 | Admin can access `/admin`; user cannot | RBAC test |
| AC-4 | Login event in audit_log | DB query |
| AC-5 | `GET /health` returns OK + LLM status | curl |
| AC-6 | Frontend dashboard renders after login | Manual demo |
| AC-7 | CI green on `develop` push | GitHub Actions |
| AC-8 | Staging URL accessible to team | Browser |

### 8.5 Definition of Done (Sprint 0)

```text
Definition of Done
──────────────────
☑ Code reviewed (1 approver minimum)
☑ Unit tests for auth + RBAC
☑ OpenAPI spec updated
☑ Migrations included
☑ No secrets in repository
☑ Deployed to staging
☑ Demo recorded or live to sponsor
```

---

## 9. Repository Structure (Sprint 0 deliverable)

```text
ST-EOS/
├── apps/
│   ├── backend/
│   │   ├── app/
│   │   │   ├── api/           # routes
│   │   │   ├── core/          # config, security
│   │   │   ├── models/        # SQLAlchemy
│   │   │   ├── services/      # business logic
│   │   │   └── main.py
│   │   ├── alembic/
│   │   └── tests/
│   └── frontend/
│       ├── src/
│       │   ├── pages/
│       │   ├── components/
│       │   └── lib/
│       └── package.json
├── packages/
│   └── ai/                    # stub in S0
├── infra/
│   ├── docker/
│   │   ├── docker-compose.yml
│   │   └── docker-compose.staging.yml
│   └── scripts/
│       ├── deploy.sh
│       └── backup.sh
├── data/
│   └── eval/                  # PoC questions migrated
├── docs/
└── .github/workflows/ci.yml
```

---

## 10. Ceremonies & Governance (ongoing from W8)

| Ceremony | Frequency | Duration | Participants |
|----------|-----------|----------|--------------|
| Daily standup | Daily | 15 min | Dev team |
| Sprint planning | Biweekly | 2 hr | Full team |
| Sprint review/demo | Biweekly | 1 hr | Team + sponsor |
| Retrospective | Biweekly | 1 hr | Dev team |
| Steering committee | Weekly | 30 min | PM + sponsor |
| Technical review | Biweekly | 1 hr | Tech + AI leads |

---

## 11. Change Control (from W8 onward)

```text
Change Request
     │
     ▼
┌─────────────┐    Minor (≤ 3 SP)    ┌──────────────┐
│ PM triage   │ ────────────────────▶ │ Sprint backlog│
└──────┬──────┘                       └──────────────┘
       │ Major (new epic)
       ▼
┌─────────────┐
│ Sponsor     │ → Approve → Re-plan sprint
│ approval    │ → Reject  → Log defer to Phase 2
└─────────────┘
```

---

## 12. Risks & Mitigations (MOV-008)

| ID | Risk | L | I | Mitigation |
|----|------|---|---|------------|
| R1 | Gate G1 No-Go but pressure to build UI | M | H | PM enforces gate; document failure |
| R2 | Docker/LLM setup blocks team Week 1 | H | H | DevOps owns compose day 1; fallback CPU model |
| R3 | Backlog too large for velocity | M | M | 199 SP / 20 = ~10 sprints; cut P1 items |
| R4 | RBAC scope creep | M | M | 4 roles only in MVP |
| R5 | No staging server | M | H | Shared dev server as interim |
| R6 | Team not fully hired | H | H | Delay MOV-009 2 weeks; do not start with 2 devs |

---

## 13. Gate G2 — Exit Criteria

| # | Criterion | Evidence |
|---|-----------|----------|
| 1 | Backlog prioritized through Sprint 2 | Board export |
| 2 | Sprint 0 acceptance criteria all pass | QA checklist |
| 3 | Staging environment live | URL + demo recording |
| 4 | Security Sprint 0 items (TLS optional dev) | Checklist partial OK |
| 5 | Team velocity baseline | Sprint 0 SP completed |
| 6 | Sponsor approves MOV-009 start | Email/minutes |

---

## 14. Handoff to MOV-009

Sprint 0 complete → immediately start **Sprint 1 (Document Repository & Ingestion)** per [MOV-009](./MOV-009-build-mvp-phase1.md).

Deliver to MOV-009:
- Running staging environment
- Auth/RBAC/audit foundation
- Frontend shell matching MOV-006 IA
- LLM connectivity proven
- Prioritized Sprint 1 stories ready

---

## Related Documents

- [DOC-701 Development Plan](../06-development/DOC-701-development-plan.md)
- [DOC-702 Sprint Plan](../06-development/DOC-702-sprint-plan.md)
- [DOC-710 Resource & Budget Plan](../06-development/DOC-710-resource-budget-plan.md)
- [MOV-009 Build MVP](./MOV-009-build-mvp-phase1.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial detailed movement doc |
