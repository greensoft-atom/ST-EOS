# MOV-000 — Movements Index

**Folder:** `docs/07-movements/`  
**Purpose:** Detailed execution playbooks for each program movement (Phase 0 through Phase 2)

---

## Movement Map

```text
PHASE 0 (Weeks 1–8) — Discovery
────────────────────────────────
MOV-000  Governance          → (see 00-next-movements.md § M0)
MOV-001  Pilot scope          → (see 00-next-movements.md § M1)
MOV-002  Data audit           → (see 00-next-movements.md § M2)
MOV-003  Requirements lock    → (see 00-next-movements.md § M3)
MOV-004  Architecture         → (see 00-next-movements.md § M4)
MOV-005  RAG PoC              → (see 00-next-movements.md § M5)
MOV-006  UX workflow design   → ✅ MOV-006-ux-workflow-design.md
MOV-007  Security & governance→ ✅ MOV-007-security-data-governance.md
MOV-008  MVP build + Sprint 0 → ✅ MOV-008-mvp-build-sprint0.md

PHASE 1 (Weeks 9–22) — Build
────────────────────────────
MOV-009  Build MVP            → ✅ MOV-009-build-mvp-phase1.md

PHASE 2 (Weeks 23–30) — Pilot
─────────────────────────────
MOV-010  Pilot deployment      → ✅ MOV-010-pilot-deployment.md

PHASE 3 (Weeks 31+) — Expand
────────────────────────────
MOV-011  Iterate & expand       → ✅ MOV-011-iterate-expand-phase2.md
```

---

## Document Quick Links

| Movement | Document | Timeline | Key deliverable |
|----------|----------|----------|-----------------|
| MOV-006 | [UX Workflow Design](./MOV-006-ux-workflow-design.md) | W6–7 | Wireframes, 24+ screens |
| MOV-007 | [Security & Governance](./MOV-007-security-data-governance.md) | W7–8 | RBAC, audit, classification |
| MOV-008 | [Sprint 0 & Build Prep](./MOV-008-mvp-build-sprint0.md) | W8–10 | Backlog, runnable skeleton |
| MOV-009 | [Build MVP Phase 1](./MOV-009-build-mvp-phase1.md) | W9–22 | Pilot-ready platform |
| MOV-010 | [Pilot Deployment](./MOV-010-pilot-deployment.md) | W23–30 | Metrics, Gate G3 |
| MOV-011 | [Phase 2 Expansion](./MOV-011-iterate-expand-phase2.md) | W31–56 | Module 2–3, v1.0 |

---

## Supporting Implementation Docs

| Doc | Purpose |
|-----|---------|
| [DOC-710 Resource & Budget](../06-development/DOC-710-resource-budget-plan.md) | FTE, hardware, costs |
| [DOC-702 Sprint Plan](../06-development/DOC-702-sprint-plan.md) | Full backlog S0–S6 |
| [DOC-706 Testing Strategy](../06-development/DOC-706-testing-strategy.md) | QA + AI eval |
| [DOC-306 Security Architecture](../04-architecture/DOC-306-security-architecture.md) | Technical security |
| [DOC-801 Deployment Guide](../08-operations/DOC-801-deployment-guide.md) | Production install |

---

## Decision Gates

| Gate | After | Document reference |
|------|-------|-------------------|
| G0 | MOV-001 | Pilot institution agreed |
| G1 | MOV-005 | PoC metrics pass |
| G2 | MOV-008 | Sprint 0 complete |
| G3 | MOV-010 | Pilot KPIs pass |

See [00-next-movements.md](../00-next-movements.md) for full playbook summary.
