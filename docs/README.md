# ST-EOS Documentation Hub

**Science & Technology Executive Operating System (ST-EOS)**  
AI-powered Science, Technology, Innovation, and Research Management Platform

---

## Pilot institution

| Field | Value |
|-------|-------|
| **Anchor** | [Ministry of Science, Technology and Innovation (MSTI)](./01-business/DOC-PILOT-001-government-executive-pilot-scope.md) |
| **MVP module** | [Evaluation Assistant (DOC-504)](./06-modules/DOC-504-evaluation-assistant.md) |
| **Deployment** | On-premise · local LLM |
| **Phase 2 affiliates** | NRIC · universities (5) · innovation centers · regional MSTI offices |

---

## Purpose of This Folder

This documentation set defines the business case, product direction, requirements, architecture, AI design, and execution plan for ST-EOS — with **detailed movement playbooks**, **resource/cost plans**, and **implementation guides**.

**Start with locked decisions:** [00-mvp-decisions.md](./00-mvp-decisions.md) — canonical source when documents disagree.

---

## Start Here (Recommended Reading Order)

| Order | Document | Audience |
|-------|----------|----------|
| 0 | **[MVP Locked Decisions](./00-mvp-decisions.md)** | All — read first |
| 1 | [Executive Assessment](./00-executive-assessment.md) | Leadership |
| 2 | [MSTI Pilot Scope (DOC-PILOT-001)](./01-business/DOC-PILOT-001-government-executive-pilot-scope.md) | Sponsor, PM |
| 3 | [Stakeholder Analysis (DOC-004)](./01-business/DOC-004-stakeholder-analysis.md) | PM, sponsor |
| 4 | [Project Charter (DOC-001)](./01-business/DOC-001-project-charter.md) | Sponsors |
| 5 | [Evaluation Assistant (DOC-504)](./06-modules/DOC-504-evaluation-assistant.md) | AI, engineering |
| 6 | [Next Movements Playbook](./00-next-movements.md) | PM, leadership |
| 7 | [Traceability Matrix (DOC-205)](./03-requirements/DOC-205-traceability-matrix.md) | QA, engineering |
| 8 | [Sprint Plan (DOC-702)](./06-development/DOC-702-sprint-plan.md) | Engineering |
| 9 | [Resource & Budget (DOC-710)](./06-development/DOC-710-resource-budget-plan.md) | Sponsor, finance |

---

## Movement Playbooks (Detailed Execution)

| Movement | Document | Timeline |
|----------|----------|----------|
| MOV-006 UX Workflow Design | [07-movements/MOV-006](./07-movements/MOV-006-ux-workflow-design.md) | Weeks 6–7 |
| MOV-007 Security & Governance | [07-movements/MOV-007](./07-movements/MOV-007-security-data-governance.md) | Weeks 7–8 |
| MOV-008 Sprint 0 & Build Prep | [07-movements/MOV-008](./07-movements/MOV-008-mvp-build-sprint0.md) | Weeks 8–10 |
| MOV-009 Build MVP | [07-movements/MOV-009](./07-movements/MOV-009-build-mvp-phase1.md) | Weeks 9–22 |
| MOV-010 Pilot Deployment (MSTI) | [07-movements/MOV-010](./07-movements/MOV-010-pilot-deployment.md) | Weeks 23–30 |
| MOV-011 Phase 2 Expansion | [07-movements/MOV-011](./07-movements/MOV-011-iterate-expand-phase2.md) | Weeks 31–56 |

---

## Key Implementation Documents

| Document | ID | Purpose |
|----------|-----|---------|
| [MVP Decisions](./00-mvp-decisions.md) | — | Canonical locked decisions |
| [SRS](./03-requirements/DOC-202-software-requirements.md) | DOC-202 | Software requirements |
| [Traceability Matrix](./03-requirements/DOC-205-traceability-matrix.md) | DOC-205 | URS → SRS → sprints |
| [RBAC Specification](./04-architecture/DOC-307-rbac-specification.md) | DOC-307 | 6 roles, permissions |
| [Architecture Decisions](./04-architecture/decisions/README.md) | ADR-001–005 | Stack & module choices |
| [Business Process Mapping](./01-business/DOC-005-business-process-mapping.md) | DOC-005 | W1–W3 AS-IS/TO-BE |
| [Metadata Standard](./07-data/DOC-603-metadata-standard.md) | DOC-603 | Ingestion fields |
| [Evaluation Assistant](./06-modules/DOC-504-evaluation-assistant.md) | DOC-504 | Sprint 5–6 MVP module |
| [Development Plan](./06-development/DOC-701-development-plan.md) | DOC-701 | Master dev timeline |
| [Sprint Plan](./06-development/DOC-702-sprint-plan.md) | DOC-702 | Backlog S0–S6 (219 SP) |
| [Testing Strategy](./06-development/DOC-706-testing-strategy.md) | DOC-706 | QA + AI eval |
| [Resource & Budget](./06-development/DOC-710-resource-budget-plan.md) | DOC-710 | FTE, HW, costs |

---

## Program Timeline (Summary)

```text
Weeks 1–8    Phase 0    Discovery, PoC, UX, Security, Sprint 0
Weeks 9–22   Phase 1    MVP build (S0–S6) — Evaluation Assistant
Weeks 23–30  Pilot      MSTI deploy, measure, Gate G3
Weeks 31–56  Phase 2    NRIC, universities, module expansion
```

**Indicative program budget:** $310K – $727K over 18 months ([DOC-710](./06-development/DOC-710-resource-budget-plan.md)).

---

## MVP wedge

```text
Knowledge Repository → RAG Search → Document Review
    → Template Creation → Evaluation Assistant
```

---

## Status

| Item | State |
|------|-------|
| Documentation | **MVP minimum set 14/14 (100%)** — 42 docs total |
| Consolidation | **2026-06-30** — audit fixes applied |
| MSTI pilot profile | Filled ([DOC-PILOT-001 v1.2](./01-business/DOC-PILOT-001-government-executive-pilot-scope.md)) |
| Formal MOU / DG sign-off | Pending |
| Codebase | Pre-development (Phase 0) |

---

## Version Control

| Field | Value |
|-------|-------|
| Documentation version | 0.4.0 |
| Last updated | 2026-06-30 |
| Root readme | [`../readme.md`](../readme.md) |
