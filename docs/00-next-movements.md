# Next Movements Playbook

**Document type:** Program execution directive  
**Author role:** CEO / Project Manager  
**Version:** 2.2  
**Date:** 2026-06-29  
**Horizon:** Phase 0 through Phase 2 (56 weeks)  
**Pilot institution:** [MSTI (DOC-PILOT-001)](./01-business/DOC-PILOT-001-government-executive-pilot-scope.md)

**Detailed movement docs:** [`07-movements/`](./07-movements/README.md)

---

## Purpose

This document defines **what to do next, in what order, and why**. It is the operational companion to the [Executive Assessment](./00-executive-assessment.md).

**Rule:** Do not start production coding until Movement 8 is complete.

---

## Movement Overview

```text
MOVEMENT 0  ─ Governance & team
MOVEMENT 1  ─ Anchor customer & pilot scope
MOVEMENT 2  ─ Data audit & corpus plan
MOVEMENT 3  ─ Requirements lock (MVP)
MOVEMENT 4  ─ Architecture & tech stack decision
MOVEMENT 5  ─ AI/RAG proof of concept
MOVEMENT 6  ─ UX workflow design (2 core flows)
MOVEMENT 7  ─ Security & data governance baseline
MOVEMENT 8  ─ MVP build plan & sprint 0
─────────────────────────────────────────────
MOVEMENT 9  ─ Build MVP (Phase 1 execution)
MOVEMENT 10 ─ Pilot deployment & measurement
MOVEMENT 11 ─ Iterate & expand module 2
```

---

## MOVEMENT 0 — Establish Program Governance

**Timeline:** Week 1  
**Owner:** Executive sponsor + Program Manager  
**Goal:** A real project exists with authority and accountability

### Actions

| # | Action | Deliverable |
|---|--------|-------------|
| 0.1 | Appoint executive sponsor | Named sponsor letter or charter sign-off |
| 0.2 | Assign Program Manager | Role confirmed in [Project Charter](./01-business/DOC-001-project-charter.md) |
| 0.3 | Form core team (minimum) | PM, tech lead, AI/RAG engineer, data engineer, UX (part-time acceptable) |
| 0.4 | Approve Phase 0 budget | Rough order: people + infra for 6 months |
| 0.5 | Set decision forum | Weekly steering; bi-weekly technical review |

### Exit criteria

- [ ] Charter approved
- [ ] Team roster confirmed
- [ ] Weekly cadence scheduled

---

## MOVEMENT 1 — Anchor Customer & Pilot Scope

**Timeline:** Weeks 1–2  
**Owner:** Program Manager + Business lead  
**Goal:** Build for the **Government S&T Executive Office** and named internal departments  
**Full documents:** [DOC-004 Stakeholder Analysis](./01-business/DOC-004-stakeholder-analysis.md) | [DOC-PILOT-001 Pilot Scope](./01-business/DOC-PILOT-001-government-executive-pilot-scope.md)

### Locked direction (2026-06-29)

| Decision | Choice |
|----------|--------|
| Anchor institution | **Ministry of Science, Technology and Innovation (MSTI)** |
| Extended scope (Phase 2+) | NRIC, universities (5), innovation centers, regional MSTI field offices |
| Primary pilot department | Department of Research Programs and Grant Administration |
| Secondary departments | Strategic Planning and Policy; Innovation + Exhibition Secretariat |
| MVP assistant (Sprint 5) | **Evaluation Assistant** |
| Deployment | On-premise, local LLM — mandatory |

Full profile: [DOC-PILOT-001 §0](./01-business/DOC-PILOT-001-government-executive-pilot-scope.md)

### Actions

| # | Action | Deliverable | Status |
|---|--------|-------------|--------|
| 1.1 | Formalize anchor office name & sponsor | Signed pilot scope or MOU | ☑ Named **MSTI** — MOU pending |
| 1.2 | Confirm 3 internal departments | Table in DOC-PILOT-001 §0.2 | ☑ Planning complete |
| 1.3 | Assign pilot champion (evaluation/programs unit) | Named contact | Pending DG letter |
| 1.4 | Define pilot success metrics | KPIs in DOC-PILOT-001 §7 | ☑ Defined |
| 1.5 | Map workflows W1–W3 (AS-IS interviews) | Workshop notes | Scheduled |

### Official pilot workflows (government executive)

| # | Workflow | Department |
|---|----------|------------|
| W1 | Grant/program submission pre-screening | MSTI Research Programs Dept. |
| W2 | Committee evaluation scoring | MSTI Evaluation secretariat |
| W3 | Annual S&T plan/report section drafting | MSTI Strategic Planning Dept. |

### Exit criteria

- [ ] DOC-PILOT-001 approved by sponsor
- [ ] 3 workflows documented with AS-IS baselines
- [ ] Legal path for corpus ingestion confirmed
- [ ] IT commits to on-prem server timeline

---

## MOVEMENT 2 — Data Audit & Corpus Plan

**Timeline:** Weeks 2–4  
**Owner:** Data lead + domain curator  
**Goal:** Know exactly what data you have and what "good enough" means

### Actions

| # | Action | Deliverable |
|---|--------|-------------|
| 2.1 | Inventory all document sources | Spreadsheet: type, count, format, language, rights |
| 2.2 | Sample 100 documents for quality review | OCR quality, metadata completeness |
| 2.3 | Classify by [Knowledge Base layers](./05-ai/DOC-404-knowledge-base-design.md) | Layer 1–4 assignment |
| 2.4 | Define metadata minimum standard | Title, author, date, type, department, language |
| 2.5 | Identify restricted/confidential subsets | Access rules before ingestion |
| 2.6 | Prioritize MVP corpus subset | Target: 2,000–5,000 docs for PoC; 10,000+ for pilot |

### Corpus priority for MVP

1. Templates and frames (highest ROI for document creation)
2. Internal policies, forms, guidelines (compliance review)
3. Research reports and theses (research assistant)
4. Exhibition/award project records (evaluation assistant)
5. Patents (Phase 2 — complex, defer if needed)

### Exit criteria

- [ ] Data inventory complete
- [ ] MVP corpus subset defined (with counts)
- [ ] Data rights/legal clearance path documented

---

## MOVEMENT 3 — Requirements Lock (MVP)

**Timeline:** Weeks 3–4  
**Owner:** PM + Product  
**Goal:** Frozen MVP scope — no feature creep during build

### Actions

| # | Action | Deliverable |
|---|--------|-------------|
| 3.1 | Finalize [Product Vision](./01-business/DOC-003-product-vision.md) | Stakeholder sign-off |
| 3.2 | Complete [URS](./03-requirements/DOC-201-user-requirements.md) for MVP | Must/Should/Won't |
| 3.3 | Complete [PRD](./02-product/DOC-101-product-requirements.md) MVP section | Feature list frozen |
| 3.4 | Write acceptance criteria per feature | Testable definitions |
| 3.5 | Publish "Not in MVP" list | Explicit exclusions |

### MVP scope (locked)

| In scope | Out of scope |
|----------|--------------|
| Document upload & repository | Multi-agent orchestration |
| Metadata tagging | External web scouting |
| RAG search with citations | Fine-tuned custom LLM |
| Document review (completeness, format, logic) | Full patent prosecution workflow |
| Template-based document creation | National-scale knowledge graph |
| One vertical assistant (**Evaluation Assistant**) | Mobile app |
| Role-based access (admin, reviewer, user) | SSO/LDAP (unless pilot requires) |
| Audit log of AI interactions | Advanced analytics dashboard |

### Exit criteria

- [ ] MVP scope signed by sponsor and PM
- [ ] Requirements traceability started
- [ ] Change control process defined

---

## MOVEMENT 4 — Architecture & Technology Stack Decision

**Timeline:** Weeks 4–5  
**Owner:** Tech lead + AI lead  
**Goal:** One coherent stack — no debates during sprints

### Actions

| # | Action | Deliverable |
|---|--------|-------------|
| 4.1 | Confirm [System Architecture](./04-architecture/DOC-301-system-architecture.md) | HLD approved |
| 4.2 | Select components (see decision table below) | ADR (Architecture Decision Records) |
| 4.3 | Define deployment target | On-prem server spec or VM cluster |
| 4.4 | Define integration boundaries | File upload first; API integrations later |
| 4.5 | Set non-functional targets | Latency, concurrent users, uptime |

### Recommended stack (starting point — validate in PoC)

| Layer | Recommendation | Notes |
|-------|----------------|-------|
| LLM runtime | Ollama / vLLM / llama.cpp | Match your existing local LLM setup |
| LLM model | Qwen2.5, Llama 3.x, Mistral — benchmark | Choose per language and hardware |
| Embeddings | bge-m3 or nomic-embed | Multilingual if needed |
| Vector DB | Qdrant or pgvector | pgvector simplifies ops if PostgreSQL already used |
| Object storage | MinIO or filesystem | PDF originals |
| Metadata DB | PostgreSQL | Users, docs, audit |
| Backend | Python (FastAPI) or Node | Python preferred for AI ecosystem |
| Frontend | React or Vue | Task-oriented UI, not chat-only |
| Orchestration | LangGraph or custom pipeline | Start simple |
| OCR | PyMuPDF + Tesseract or docling | Benchmark on your PDFs |

### Exit criteria

- [ ] Stack decisions recorded as ADRs
- [ ] Dev environment reproducible (Docker Compose minimum)
- [ ] Hardware requirements documented

---

## MOVEMENT 5 — AI/RAG Proof of Concept

**Timeline:** Weeks 5–7  
**Owner:** AI lead  
**Goal:** Prove retrieval quality and answer usefulness on real documents

### Actions

| # | Action | Deliverable |
|---|--------|-------------|
| 5.1 | Ingest 500–1,000 sample documents | Working ingestion script |
| 5.2 | Implement chunking + embedding + retrieval | Baseline RAG pipeline |
| 5.3 | Create 50 test questions with expected sources | Evaluation set |
| 5.4 | Measure: retrieval recall, answer relevance, citation accuracy | PoC report |
| 5.5 | Test document review prompt on 20 real docs | Review quality sample |
| 5.6 | Test template fill on 5 templates | Creation quality sample |

### PoC success thresholds

| Metric | Minimum acceptable |
|--------|-------------------|
| Retrieval: correct doc in top-5 | ≥ 70% |
| Citation points to correct chunk | ≥ 80% |
| Review catches missing sections | ≥ 75% vs human checklist |
| Template generation needs minor edits only | ≥ 60% |

If thresholds not met: fix ingestion and retrieval before MVP build.

### Exit criteria

- [ ] PoC report with metrics
- [ ] Go/No-Go decision for MVP build
- [ ] Prompt templates v1 in repo

---

## MOVEMENT 6 — UX Workflow Design (2 Core Flows)

**Timeline:** Weeks 6–7 (parallel with PoC)  
**Owner:** PM + UX  
**Goal:** Task-based UI, not a blank chat box  
**Full document:** [MOV-006 UX Workflow Design](./07-movements/MOV-006-ux-workflow-design.md)

| Resource | Estimate |
|----------|----------|
| Human | UX 0.5–1 FTE × 10 days; PM 0.3; pilot users × 3 |
| Cost | $2,050 – $6,380 (incremental) |
| Software | Figma/Penpot |

### Priority flows

**Flow 1: Document Review**
```text
Upload/select doc → Choose review type → AI review with findings →
User accepts/edits → Export report
```

**Flow 2: Knowledge Search & Draft**
```text
Enter question → Retrieved sources shown → AI answer with citations →
"Create document from this" → Template selection → Draft editor → Export
```

### Key deliverables (from MOV-006)

| # | Deliverable |
|---|-------------|
| D1 | Information architecture + dashboard wireframe |
| D2 | 24+ annotated screens (Figma) |
| D3 | Clickable prototype for 2 core flows |
| D4 | Role × screen access matrix |
| D5 | Component list (TaskWizard, CitationChip, etc.) |

### Exit criteria

- [ ] Approved wireframes
- [ ] UI scope matches MVP PRD
- [ ] No "chat-only" dependency for core tasks
- [ ] Frontend sprint estimates confirmed

---

## MOVEMENT 7 — Security & Data Governance Baseline

**Timeline:** Weeks 7–8  
**Owner:** Tech lead + PM  
**Goal:** Minimum compliance for pilot institution  
**Full document:** [MOV-007 Security & Data Governance](./07-movements/MOV-007-security-data-governance.md)

| Resource | Estimate |
|----------|----------|
| Human | Tech lead 0.5 × 8d; PM 0.3; data lead 0.3 |
| Cost | $50 – $4,700 (legal review optional) |
| Outputs | DOC-602, DOC-306, AI Usage Policy, DR runbook |

### Actions

| # | Action | Deliverable |
|---|--------|-------------|
| 7.1 | Data classification policy | [DOC-602](./07-data/DOC-602-data-classification.md) |
| 7.2 | RBAC + API permission map | 4 roles, 15+ permissions |
| 7.3 | Audit logging (15 event types) | AUD-001–015 spec |
| 7.4 | Backup & restore drill | [DOC-804](./08-operations/DOC-804-disaster-recovery.md) |
| 7.5 | AI usage policy | [AI-USAGE-POLICY](./09-enterprise/AI-USAGE-POLICY.md) |

### Exit criteria

- [ ] Security checklist complete for pilot (12 items)
- [ ] No confidential data ingested without classification
- [ ] Audit schema in Sprint 0 migration plan
- [ ] Restore drill successful

---

## MOVEMENT 8 — MVP Build Plan & Sprint 0

**Timeline:** Week 8 planning + Weeks 9–10 Sprint 0  
**Owner:** PM + Tech lead  
**Goal:** Backlog ready + runnable platform skeleton  
**Full document:** [MOV-008 MVP Build & Sprint 0](./07-movements/MOV-008-mvp-build-sprint0.md)

| Resource | Estimate |
|----------|----------|
| Human | 4 FTE × 2.5 weeks (planning + S0) |
| Hardware | Staging server $3K–$8K |
| Cost | $2,800 – $11,100 incremental |
| Backlog | ~219 SP across S0–S6 |

### Actions

| # | Action | Deliverable |
|---|--------|-------------|
| 8.1 | Finalize [DOC-701](./06-development/DOC-701-development-plan.md) + [DOC-702](./06-development/DOC-702-sprint-plan.md) | Sprint breakdown |
| 8.2 | Repo, CI, staging | Docker Compose green |
| 8.3 | Backlog from PRD | 30+ stories pointed |
| 8.4 | Sprint 0 execution | Auth, RBAC, audit, LLM smoke |
| 8.5 | Gate G2 review | Go → MOV-009 |

### MVP sprint outline

| Sprint | Focus | Weeks | SP |
|--------|-------|-------|-----|
| S0 | Foundation | 9–10 | 21 |
| S1 | Ingestion + repository | 11–12 | 34 |
| S2 | RAG search | 13–14 | 34 |
| S3 | Document review | 15–16 | 34 |
| S4 | Template creation | 17–18 | 34 |
| S5 | **Evaluation Assistant** | 19–20 | 34 |
| S6 | Eval completion + hardening + UAT | 21–22 | 28 |

### Exit criteria (Gate G2)

- [ ] Sprint 0 acceptance criteria pass (see MOV-008 §8.4)
- [ ] Staging deploy live
- [ ] Backlog through Sprint 2 ready

---

## MOVEMENT 9 — Build MVP (Phase 1 Execution)

**Timeline:** Weeks 9–22  
**Owner:** Tech lead  
**Goal:** Pilot-ready platform  
**Full document:** [MOV-009 Build MVP](./07-movements/MOV-009-build-mvp-phase1.md)

| Resource | Estimate |
|----------|----------|
| Human | ~4.95 FTE × 14 weeks (~66 person-weeks) |
| Hardware | App + GPU server $4K–$15.5K |
| Cost | $97K – $252K (cash, excl. internal salary) |
| Corpus | 10,000 docs indexed by S6 |

Weekly sponsor demos (W10, 12, 14, 16, 18, 20, 22). Quality gates QG-1–QG-6 must pass. See [DOC-706 Testing Strategy](./06-development/DOC-706-testing-strategy.md).

---

## MOVEMENT 10 — Pilot Deployment & Measurement

**Timeline:** Weeks 23–30  
**Owner:** PM + Customer success  
**Goal:** Real users, measured value, Gate G3  
**Full document:** [MOV-010 Pilot Deployment](./07-movements/MOV-010-pilot-deployment.md)

| Resource | Estimate |
|----------|----------|
| Human | PM 0.8, tech 0.4, trainer 0.5, 10–20 champions |
| Cost | $10.7K – $42K |
| KPIs | 10 quantitative + qualitative surveys |

Deploy per [DOC-801](./08-operations/DOC-801-deployment-guide.md) at **MSTI**. Run workflows W1–W3. Deliver pilot report + Go/No-Go for MOV-011 (Phase 2: NRIC, universities).

---

## MOVEMENT 11 — Iterate & Expand (Phase 2 Entry)

**Timeline:** Weeks 31–56 (~6 months)  
**Owner:** Program Office  
**Goal:** Module 2–3, Version 1.0 criteria  
**Full document:** [MOV-011 Phase 2 Expansion](./07-movements/MOV-011-iterate-expand-phase2.md)

| Resource | Estimate |
|----------|----------|
| Human | Scale to 6.5–7.5 FTE |
| Cost | $147K – $439K (6 months) |
| Corpus | 10K → 50K+ documents |

Phase 2A: hybrid search, SSO, platform fixes. Phase 2B: second module. Phase 2C: third module or scale. **One module per 8-week block.**

---

## Decision Gates

| Gate | When | Question | MSTI status |
|------|------|----------|-------------|
| G0 | End Movement 1 | Do we have a pilot customer? | **Partial** — MSTI named; MOU pending |
| G1 | End Movement 5 | Does RAG PoC meet thresholds? | Not started |
| G2 | End Movement 8 | Is team ready to build? | Not started |
| G3 | End Movement 10 | Did pilot prove value? | Not started |

**If No at G0:** Continue internal PoC only; do not scale team.  
**If No at G1:** Fix data pipeline; do not build UI.  
**If No at G3:** Narrow scope or change pilot workflows before Phase 2.

---

## Immediate Next 2 Weeks (Action List)

For the team **now** (post–MSTI profile):

| Day | Action |
|-----|--------|
| 1–2 | Read Executive Assessment + this playbook; approve [Charter (DOC-001)](./01-business/DOC-001-project-charter.md) |
| 3–5 | Movement 1: obtain DG sign-off on [DOC-PILOT-001](./01-business/DOC-PILOT-001-government-executive-pilot-scope.md) |
| 5–10 | Movement 2: begin MSTI data inventory spreadsheet |
| 8–10 | Movement 0: confirm team roles and weekly meetings |
| 10–14 | Movement 3: MVP URS/PRD review with MSTI sponsor |

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial playbook |
| 2.0 | 2026-06-29 | Linked MOV-006–011; resources & costs |
| 2.1 | 2026-06-29 | Government S&T executive office anchor; Evaluation MVP |
| 2.2 | 2026-06-29 | MSTI profile; MOV-1 progress; DOC-504 sprint link |
| 2.3 | 2026-06-30 | 219 SP; Evaluation-only scope; link 00-mvp-decisions |
