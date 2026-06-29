# DOC-004 — Stakeholder Analysis

**Document ID:** DOC-004  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Approved direction — MSTI pilot profile v1.2  
**Anchor institution type:** **Ministry of Science, Technology and Innovation (MSTI)** and affiliated bodies

---

## 1. Purpose

Define stakeholders for ST-EOS when the primary deployment context is a **government science and technology executive organization** — the ministry, department, or national council that leads S&T policy, funding, innovation programs, and coordination with research and industry.

This analysis drives pilot scope, requirements priority, security posture, and Phase 2 module order.

---

## 2. Institutional Context

```text
                    GOVERNMENT S&T ECOSYSTEM
                    ────────────────────────

              ┌─────────────────────────────────┐
              │  S&T GOVERNMENT EXECUTIVE       │  ◀── ANCHOR (ST-EOS pilot)
              │  OFFICE (Ministry / Council)    │
              │  • Policy & strategy            │
              │  • National programs              │
              │  • Budget & planning              │
              │  • Evaluation & oversight         │
              └───────────────┬─────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
┌───────────────┐   ┌───────────────┐   ┌───────────────┐
│ Internal      │   │ Affiliated    │   │ External      │
│ departments   │   │ institutions  │   │ stakeholders  │
└───────────────┘   └───────────────┘   └───────────────┘
```

**Your choice:** Build ST-EOS for this executive office **first**, then extend to related institutions and departments that operate under or coordinate with it.

---

## 3. Anchor Institution — Executive Office

### 3.1 Typical organizational units (internal)

```text
S&T Government Executive Office
├── Office of the Minister / Director-General
├── Strategic Planning & Policy Department
├── Research Programs & Grants Department
├── Innovation, Technology Transfer & Industry Linkage
├── Science Promotion & Public Outreach
├── International Cooperation & Agreements
├── Intellectual Property & Standards (or liaison unit)
├── Science & Technology Exhibitions / Competitions Secretariat
├── Monitoring, Evaluation & Reporting (M&E)
├── Finance & Administration
└── Information Technology / Digital Transformation Unit
```

Not every office has all units — map to **your** actual structure during MOV-001 workshops.

### 3.2 Executive office — primary pain points

| Pain | ST-EOS response |
|------|-----------------|
| Volume of grant/exhibition submissions to review | Evaluation Assistant + Document Review |
| Drafting annual S&T plans and reports | Template Creation + Planning Assistant (Phase 2) |
| Policy Q&A across regulations | RAG Search (Layer 4 corpus) |
| Inconsistent scoring across committees | Evaluation rubrics + cited evidence |
| Lost institutional memory (past programs, awards) | Knowledge repository + search |
| Data sovereignty requirements | Local LLM — **mandatory fit** |
| Ministerial briefings under time pressure | Reporting Assistant (Phase 2) |

---

## 4. Related Institutions & Departments (Extended Stakeholders)

### 4.1 Stakeholder map

| Stakeholder | Relationship to executive office | ST-EOS role (phase) | Priority |
|-------------|----------------------------------|---------------------|----------|
| **National research council / fund** | Implements grants | Evaluation, research corpus | High — Phase 1 pilot partner |
| **Universities & academies** | Submit proposals, research outputs | Research Assistant, repository | High — Phase 1–2 |
| **Innovation centers / tech parks** | Incubation, commercialization | Innovation Assistant | Medium — Phase 2 |
| **Patent / IP office** | IP examination liaison | Patent Assistant | Medium — Phase 2 |
| **Exhibition / science fair organizers** | National competitions | Exhibition Assistant | High — Phase 2 (if heavy exhibition load) |
| **Standardization / metrology bodies** | Technical standards | RAG policy corpus | Low — Phase 3 |
| **Regional S&T departments** | Sub-national coordination | Federated search (future) | Phase 3+ |
| **Industry / chamber R&D units** | Partnership programs | Tech transfer module | Phase 2–3 |
| **International agencies (UNESCO, etc.)** | Reporting alignment | Reporting, templates | Phase 3 |

### 4.2 Deployment tiers

```text
Tier 1 — Pilot (Year 1)
───────────────────────
  S&T Executive Office (single on-prem deployment)
  └── 3–5 internal departments as users

Tier 2 — Extended government (Year 2)
─────────────────────────────────────
  + National research council (read-only or shared corpus)
  + Exhibition secretariat (evaluation workflows)

Tier 3 — National platform (Year 3+)
────────────────────────────────────
  + Universities (submission portal integration)
  + Regional offices (policy-controlled federation)
```

---

## 5. Stakeholder Register

| ID | Stakeholder | Type | Interest | Influence | Engagement |
|----|-------------|------|----------|-----------|------------|
| STK-01 | Minister / Director-General | Internal executive | Dashboards, briefings, risk | High | Quarterly demo |
| STK-02 | Planning & Policy Department | Internal user | Plans, roadmaps, policy RAG | High | Pilot champion |
| STK-03 | Research Programs Department | Internal user | Proposals, literature, review | High | Primary pilot dept |
| STK-04 | Evaluation / Grant committee | Internal user | Scoring, ranking, compliance | High | MVP assistant user |
| STK-05 | Exhibition / competition secretariat | Internal user | Intake, categorization | Medium | Phase 2 |
| STK-06 | Innovation & tech transfer unit | Internal user | Scouting, commercialization | Medium | Phase 2 |
| STK-07 | M&E / Reporting unit | Internal user | KPIs, progress reports | Medium | Phase 2 |
| STK-08 | IT / Digital transformation | Internal enabler | Deploy, SSO, security | High | Weekly tech sync |
| STK-09 | Legal / data protection | Internal gatekeeper | Classification, AI policy | High | MOV-007 sign-off |
| STK-10 | National research council | Affiliated | Shared grant corpus | Medium | Phase 2 MOU |
| STK-11 | Universities (applicants) | External submitter | Easier compliance | Medium | Phase 2 portal |
| STK-12 | Public / media | External | Transparency (published outputs only) | Low | Indirect |
| STK-13 | ST-EOS program sponsor | Internal | ROI, timeline | High | Weekly steering |
| STK-14 | ST-EOS development team | Internal | Clear requirements | High | Daily |

---

## 6. Needs & Expectations Matrix

| Stakeholder | Primary need | Expectation of ST-EOS | Non-negotiable |
|-------------|--------------|----------------------|----------------|
| Minister / DG | Decision-ready briefings | Fast, cited summaries | No cloud data leak |
| Planning dept | Annual / strategic plans | Template + past plan RAG | Alignment with policy |
| Research programs | Proposal review at scale | Review + evaluation assist | Fair, auditable scoring |
| Evaluation committee | Consistent rubric scoring | Evidence per criterion | Human final decision |
| Exhibition secretariat | Rank hundreds of projects | Similar-project search | Transparent criteria |
| IT department | Operable secure system | Docker, on-prem, logs | SSO (may Phase 2) |
| Legal | Compliance | Classification, audit trail | AI disclaimer |
| Universities | Clear submission guidance | Review before submit (future) | Data protection |

---

## 7. Pilot Configuration (Locked Direction)

Based on stakeholder choice: **Government S&T Executive Office**

### 7.1 Anchor

| Field | Value |
|-------|-------|
| Institution | **Ministry of Science, Technology and Innovation (MSTI)** |
| Type | National government S&T executive office |
| Deployment | On-premise, single organization |
| User scale (pilot) | 40–70 staff across 5 internal units |
| Corpus scope | MSTI archives + national program and exhibition records |

### 7.2 Recommended pilot department mix

```text
PRIMARY (MVP assistant + workflows)
──────────────────────────────────
  Research Programs & Evaluation Unit
  OR Grant / Program Evaluation Committee
  → MVP Assistant: EVALUATION ASSISTANT

SECONDARY (shared utilities only in MVP)
────────────────────────────────────────
  Strategic Planning & Policy Department  → Search, review, plan templates
  Innovation / Exhibition Secretariat     → Search, repository, review

TERTIARY (Phase 2 modules)
──────────────────────────
  Planning Department      → Planning Assistant
  Exhibition Secretariat   → Exhibition Assistant (if volume high)
  IP liaison unit          → Patent Assistant
```

### 7.3 Why Evaluation Assistant for MVP (government context)

| Reason | Detail |
|--------|--------|
| Central executive function | Screening grants, programs, exhibitions is core ministry work |
| Uses existing corpus | Exhibition awards, past projects, evaluation rubrics |
| High visible ROI | Committees save days per review cycle |
| Shared platform proof | Planning and research units still use search/review/create |
| Lower risk than autonomous planning | Human approval gate matches government accountability |

**Alternative:** If your office is **planning-heavy** (annual national S&T plan is the burning pain), swap Sprint 5 to **Planning Assistant** lite (roadmap + plan draft only) — confirm in MOV-001 workshop.

---

## 8. Official Pilot Workflows (Government Executive Office)

| # | Workflow | Primary unit | MVP features |
|---|----------|--------------|--------------|
| W1 | Pre-screen grant/program submissions | Evaluation unit | Review + Evaluation Assistant |
| W2 | Prepare committee scoring packet | Evaluation committee | Evaluation + export |
| W3 | Draft sections of annual S&T report | Planning unit | Search + template creation |
| W4 | Policy compliance check on proposals | Legal liaison + programs | Review (compliance type) |
| W5 | Find past award-winning similar projects | Exhibition / innovation | RAG search |

**MVP pilot requires W1–W3 executed in MOV-010.** W4–W5 optional stretch.

---

## 9. Communication & Governance

```text
Steering Committee
├── Sponsor (DG office or deputy)
├── Program Manager
├── IT director (STK-08)
└── Pilot champion (Research programs or Planning)

Working Group (weekly)
├── PM + Tech lead
├── Department reps (3–5)
└── Data curator

Technical Review (biweekly)
├── Tech lead + AI lead + IT
```

---

## 10. Risks — Stakeholder-Specific

| Risk | Stakeholder | Mitigation |
|------|-------------|------------|
| Minister expects full dashboard Day 1 | STK-01 | Set Phase 2 for Reporting Assistant |
| IT mandates SSO before pilot | STK-08 | Budget SSO in Phase 2A; basic auth MVP if approved |
| Legal blocks AI on restricted docs | STK-09 | MOV-007 classification + human-in-loop |
| Universities demand portal access early | STK-11 | Defer external portal to Phase 2 |
| Department silos resist shared corpus | Internal | Executive mandate + champion program |
| Cross-institution data sharing unclear | Affiliated | Pilot internal only; MOU for Phase 2 |

---

## 11. Success Criteria (Stakeholder-Aligned)

| Stakeholder | Success looks like |
|-------------|-------------------|
| DG / Sponsor | 3 workflows faster; trusted pilot report |
| Evaluation committee | ≥ 30% less prep time; cited scores |
| Planning dept | First draft of plan section in hours not days |
| IT | Clean security checklist; stable on-prem |
| Legal | Signed AI policy; audit log sample reviewed |

---

## Related Documents

- [DOC-PILOT-001 Pilot Scope](./DOC-PILOT-001-government-executive-pilot-scope.md)
- [MOV-010 Pilot Deployment](../07-movements/MOV-010-pilot-deployment.md)
- [DOC-003 Product Vision](./DOC-003-product-vision.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Government S&T executive office anchor |
