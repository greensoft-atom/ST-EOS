# DOC-PILOT-001 — Government S&T Executive Office Pilot Scope

**Document ID:** DOC-PILOT-001  
**Version:** 1.2  
**Date:** 2026-06-29  
**Status:** Planning profile complete — pending formal MOU / sponsor sign-off  
**Pilot institution:** **Ministry of Science, Technology and Innovation (MSTI)**  
**Anchor:** Science & Technology **Government Executive Office** + selected internal departments  
**MVP module design:** [DOC-504 Evaluation Assistant](../06-modules/DOC-504-evaluation-assistant.md)

> **Note on names:** Personal names below are **program placeholders** for planning and documentation. Replace with formally appointed officials when the charter and pilot MOU are signed.

---

## 0. Organization Profile

Planning profile completed for ST-EOS MOV-001. Adjust only if your legal entity name differs.

| Field | Value |
|-------|-------|
| **Official office name** | Ministry of Science, Technology and Innovation |
| **Short name / acronym** | MSTI |
| **Jurisdiction** | National — government executive portfolio for science, technology, innovation, and research coordination |
| **Legal status** | Ministry / department of state (executive branch) |
| **Executive sponsor** | **Director-General (DG), MSTI** — overall accountability, steering committee chair |
| **Pilot champion** | **Director, Department of Research Programs and Grant Administration** — day-to-day pilot owner |
| **Program Manager (ST-EOS)** | Appointed by DG office — delivery, scope, timeline |
| **Primary language** | **English** (MVP UI and documentation); **local official language** UI strings Phase 2 |
| **IT contact** | **Director, Information Technology and Digital Transformation Division, MSTI** |
| **Data / corpus owner** | **Director, Strategic Planning and Policy Department** (with Research Programs co-custodianship) |
| **Legal / compliance contact** | **Head, Legal and Compliance Unit, MSTI** (or equivalent under DG office) |

### 0.1 Organization chart (MSTI — pilot mapping)

```text
Ministry of Science, Technology and Innovation (MSTI)
│
├── Office of the Director-General (DG)              → Executive sponsor (STK-01)
│   ├── Minister’s / DG Secretariat                    → Secondary C (briefings, W3 support)
│   └── Legal and Compliance Unit                      → AI policy & data clearance (STK-09)
│
├── Department of Strategic Planning and Policy        → Secondary A (W3: plans/reports)
│   ├── National S&T Policy Division
│   ├── Annual Planning and Reporting Division
│   └── International Cooperation Division
│
├── Department of Research Programs and Grant        → PRIMARY (W1, W2: evaluation)
│   │   Administration
│   ├── Research Grant Management Division
│   ├── Program Evaluation and Monitoring Division
│   └── Research Ethics and Compliance Unit
│
├── Department of Innovation Promotion and             → Secondary B (repository, review)
│   │   Technology Transfer
│   ├── Innovation Ecosystem Division
│   ├── Technology Transfer and Commercialization Unit
│   └── Industry–Academia Linkage Division
│
├── National Science and Technology Exhibition         → Secondary B (exhibition corpus,
│   and Competition Secretariat                            competitions, award records)
│
├── Monitoring, Evaluation and Performance Division    → Secondary C (KPIs, Phase 2 reporting)
│
└── Information Technology and Digital Transformation  → Enabler (STK-08: deploy, SSO, security)
    Division
```

### 0.2 Department confirmation (pilot roles)

| ST-EOS role | MSTI department | Lead (role title) | Confirmed |
|-------------|-----------------|-------------------|-----------|
| **Primary** | Department of Research Programs and Grant Administration | Director of Research Programs | ☑ Planning |
| **Secondary A** | Department of Strategic Planning and Policy | Director of Strategic Planning | ☑ Planning |
| **Secondary B** | Dept. of Innovation Promotion + National S&T Exhibition Secretariat | Director of Innovation; Secretariat Head | ☑ Planning |
| **Secondary C** (optional) | DG Secretariat / M&E Division | DG Chief of Staff | ☑ Planning |
| **IT enabler** | IT and Digital Transformation Division | IT Director | ☑ Planning |

### 0.3 Affiliated institutions (Phase 2 — named for planning)

| Institution | Relationship to MSTI | Phase 2 role |
|-------------|----------------------|--------------|
| **National Research and Innovation Council (NRIC)** | Advisory + grant implementation partner | Shared grant corpus, read-only RAG |
| **National universities (initial 5)** | Submit proposals and reports to MSTI programs | Submission review portal |
| **National Technology Innovation Centers (network)** | Innovation parks under MSTI policy | Innovation scouting corpus |
| **Regional / state S&T field offices (3 divisions)** | Sub-national coordination | Federated search (policy-controlled) |
| **National Intellectual Property Office** (liaison) | IP policy alignment | Patent Assistant corpus (Phase 2B) |

**Initial university pilot partners (to confirm MOU in Phase 2):** five national public universities with active MSTI grant participation — exact list by Research Programs Department at Gate G3.

---

## 1. Pilot Statement

ST-EOS Phase 1 MVP will be built and piloted for the **Ministry of Science, Technology and Innovation (MSTI)** — the national government executive body responsible for S&T policy, funding programs, innovation promotion, exhibitions, and coordination with research institutions — with extension planned to **NRIC, universities, innovation centers, and regional S&T offices** in Phase 2.

---

## 2. Scope Boundaries

```text
IN SCOPE (Pilot)                          OUT OF SCOPE (Pilot)
────────────────────────────────          ─────────────────────────────
• One executive office deployment         • Multi-ministry federation
• 3–5 internal departments as users       • Public internet portal
• On-prem local LLM                       • Autonomous funding decisions
• 10,000+ internal documents              • Full national university network
• Evaluation Assistant (MVP module)       • Patent prosecution workflow
• Shared: search, review, create          • Mobile native apps
• 30–80 pilot users                       • External web scouting
```

---

## 3. Participating Departments (MSTI)

| Role | MSTI department | MVP usage | Users (est.) |
|------|-----------------|-----------|--------------|
| **Primary** | Department of Research Programs and Grant Administration | Evaluation Assistant, review, search | 15–25 |
| **Secondary A** | Department of Strategic Planning and Policy | Search, plan/report creation (W3) | 10–15 |
| **Secondary B** | Dept. of Innovation Promotion + National S&T Exhibition Secretariat | Search, review, repository | 10–15 |
| **Secondary C** | DG Secretariat / M&E Division (optional) | Search, briefing drafts | 5–10 |
| **Enabler** | IT and Digital Transformation Division | Admin, deploy, security | 2–5 |

**Total pilot users:** 40–70 (target ≥ 30 active weekly)

---

## 4. MVP Module Decision (Locked)

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Sprint 5 assistant | **Evaluation Assistant** | Core executive function: grants, programs, competitions |
| Not in MVP | Planning Assistant (full) | Phase 2 — after evaluation trust established |
| Not in MVP | Exhibition ranking at scale | Phase 2 — Exhibition Assistant |

Planning department still benefits from **template-based plan/report creation** (Sprint 4) without full Planning Assistant.

---

## 5. Corpus Scope (Pilot)

```text
Executive Office Knowledge Corpus (Pilot)
─────────────────────────────────────────
Layer 4 — Organizational (highest MVP priority)
  ├── Regulations, policies, guidelines
  ├── Strategic plans (past annual S&T plans)
  ├── Forms, registers, procedures
  └── Ministerial / council decisions

Layer 2 — Innovation & Programs
  ├── Exhibition / competition submissions (anonymized if needed)
  ├── Award-winning project records
  └── Funded program reports

Layer 1 — Research & Literature (subset)
  ├── National research reports
  ├── Theses (selected)
  └── Technical studies commissioned by office

Layer 3 — Patents (optional Phase 1)
  └── Defer unless IP unit is strong pilot partner

Cross-cutting
  └── Templates: evaluation rubrics, plan frames, report formats
```

| Corpus target | Count |
|---------------|-------|
| PoC (MOV-005) | 500–1,000 |
| Sprint 2 | 5,000 |
| Pilot go-live (MOV-010) | 10,000+ |

---

## 6. Three Official Pilot Workflows

### W1 — Grant / program submission pre-screening (Primary)

```text
AS-IS:  Staff manually check 50+ page proposals against checklist (4–8 hrs each)
TO-BE:  Upload → AI review (completeness, format, compliance) → Evaluation pre-score
        → Human confirms → Committee packet export
Target: 50% reduction in pre-screening time
Owner:  Research Programs Department
```

### W2 — Committee evaluation scoring (Primary)

```text
AS-IS:  Each evaluator reads alone; inconsistent notes; 3–5 days for batch of 20
TO-BE:  Rubric-based AI scoring with cited evidence → Evaluator edits → Approve → Rank
Target: 30% reduction in committee prep time
Owner:  Evaluation Committee secretariat
```

### W3 — Annual S&T plan / report section drafting (Secondary)

```text
AS-IS:  Planning staff search archives manually; draft from scratch (2–5 days/section)
TO-BE:  RAG search past plans + policies → Template creation → Staff edit → Export
Target: 40% reduction in first-draft time
Owner:  Strategic Planning Department
```

---

## 7. Success Metrics (MOV-010 KPIs — Prefilled)

| KPI | Target |
|-----|--------|
| Weekly active users | ≥ 30 |
| Documents indexed | ≥ 10,000 |
| AI queries / week | ≥ 100 |
| Reviews completed (pilot period) | ≥ 50 |
| Evaluations scored | ≥ 20 submissions |
| Pre-screen time (W1) | −50% |
| Committee prep time (W2) | −30% |
| Plan draft time (W3) | −40% |
| User trust (survey 1–5) | ≥ 3.8 |
| Uptime | ≥ 99% |

---

## 8. Institutional Requirements (Government)

| Requirement | MVP | Phase 2 |
|-------------|-----|---------|
| On-premise deployment | ✓ Required | ✓ |
| Local LLM only | ✓ Required | ✓ |
| Data classification | ✓ Required | ✓ |
| Audit log | ✓ Required | ✓ |
| AI usage policy signed | ✓ Required | ✓ |
| SSO / LDAP | Optional (MVP) | Required (MSTI enterprise AD/LDAP) |
| Local language UI | English MVP | Full bilingual UI Phase 2 |
| Accessibility (WCAG) | Basic | Full |

---

## 9. Phase 2 Extension — Related Institutions

After Gate G3 (successful pilot), extend in this order:

| Order | Institution | Integration model |
|-------|-------------|-------------------|
| 1 | National Research and Innovation Council (NRIC) | Shared read corpus or API |
| 2 | National S&T Exhibition and Competition Secretariat (MSTI) | Evaluation + exhibition module |
| 3 | Five national public universities (MSTI grant partners) | Submission review portal |
| 4 | National Technology Innovation Centers network | Innovation scouting (internal corpus) |
| 5 | MSTI regional S&T field offices (3 divisions) | Federated search (policy-controlled) |

```text
Phase 2 Extension Model
───────────────────────

   ┌─────────────────────┐
   │ MSTI (ST-EOS core)  │  Master on-prem deployment
   └──────────┬──────────┘
              │ policy-controlled sharing
   ┌──────────┼──────────┬─────────────┐
   ▼          ▼          ▼             ▼
  NRIC     Exhibition   Universities  Innovation
           Secretariat  (5 partners)  centers
```

---

## 10. Approvals Required

| Approval | MSTI role | Status |
|----------|-----------|--------|
| Pilot scope | Director-General, MSTI | Pending signature |
| Data use of archival documents | Legal and Compliance Unit + DG office | Pending (Week 2–4) |
| IT hosting & security | IT and Digital Transformation Division | Pending (server spec Week 4–6) |
| AI usage policy | Legal Unit + DG | Draft ready — [AI-USAGE-POLICY](../09-enterprise/AI-USAGE-POLICY.md) |
| Evaluation rubric sharing | Research Programs and Grant Administration | Pending (curator Week 3) |
| Corpus ingestion (restricted docs) | Research Programs + Legal | Pending classification review |

---

## 11. Immediate Next Steps (MOV-001)

| # | Action | Owner | Week | Status |
|---|--------|-------|------|--------|
| 1 | Name exact executive office entity | Sponsor | 1 | ☑ **MSTI** |
| 2 | Confirm 3 participating departments | PM | 1–2 | ☑ See §0.2 |
| 3 | Assign pilot champion (Evaluation unit) | DG, MSTI | 2 | Pending formal letter |
| 4 | Schedule AS-IS workflow interviews (W1–W3) | PM + champions | 2 | Scheduled |
| 5 | Legal clearance for corpus ingestion | Data lead + Legal Unit | 2–4 | In progress |
| 6 | IT server provision commitment | IT Division | 4–6 | Pending hardware requisition |
| 7 | Load 2 evaluation rubrics into curator queue | Research Programs | 3 | Pending |
| 8 | Sign AI usage policy for pilot users | Legal + DG | 7 | Draft ready |

---

## Related Documents

- [DOC-004 Stakeholder Analysis](./DOC-004-stakeholder-analysis.md)
- [MOV-001 in Next Movements](../00-next-movements.md)
- [MOV-010 Pilot Deployment](../07-movements/MOV-010-pilot-deployment.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial government executive pilot scope |
| 1.1 | 2026-06-29 | Organization profile template (§0); DOC-504 link |
| 1.2 | 2026-06-29 | MSTI profile filled: org chart, departments, Phase 2 affiliates |
