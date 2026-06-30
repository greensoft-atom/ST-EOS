# MOV-006 — UX Workflow Design (2 Core Flows)

**Movement ID:** MOV-006  
**Phase:** Phase 0 (Discovery)  
**Timeline:** Weeks 6–7 (parallel with MOV-005 RAG PoC)  
**Duration:** 10 working days  
**Owner:** Program Manager + UX Designer (or PM-led with frontend dev support)  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Ready for execution

---

## 1. Purpose

Define task-based user experiences for ST-EOS MVP — **not a generic chat interface**. This movement produces wireframes, screen inventory, navigation model, and role-based access alignment so Sprint 1+ development builds the right UI the first time.

**Principle:** Every core task reachable in ≤ 5 clicks from dashboard.

---

## 2. Movement Context

```text
Phase 0 Timeline (Weeks 1–8)
────────────────────────────────────────────────────────────────
W1   W2   W3   W4   W5   W6   W7   W8
│M0│ │M1│ │M2──────│ │M3│ │M4│
                  │M5──────────│
                  │MOV-006─────│  ← parallel with PoC
                              │MOV-007│ │MOV-008│
```

| Dependency | Status required before start |
|------------|------------------------------|
| MOV-003 Requirements lock | PRD feature list frozen |
| MOV-001 Pilot scope | Primary department chosen |
| MOV-005 RAG PoC (partial) | Sample answers available for UX copy realism |

| Blocks | Movement |
|--------|----------|
| Sprint 1 UI work | MOV-009 |
| Role permissions in UI | MOV-007 |

---

## 3. Goals & Success Criteria

| Goal | Metric | Target |
|------|--------|--------|
| Task-first UX approved | Pilot user sign-off | 3/3 reviewers approve flows |
| No chat-only dependency | Core flows use wizards | 100% of P0 features |
| Screen inventory complete | All MVP screens listed | ≥ **34** screens mapped |
| Role alignment | Access matrix documented | 6 roles × all screens ([DOC-307](../04-architecture/DOC-307-rbac-specification.md)) |
| Dev-ready handoff | Annotated wireframes | Frontend can estimate sprints |

---

## 4. Resources

### 4.1 Human resources

| Role | FTE | Days | Responsibilities |
|------|-----|------|------------------|
| Program Manager | 0.3 | 6 | Workshops, sign-off, pilot liaison |
| UX Designer | 0.5–1.0 | 10 | Wireframes, flows, component spec |
| Frontend Developer | 0.2 | 3 | Feasibility review, component reuse |
| Tech Lead | 0.1 | 2 | API/data constraints for UI |
| Pilot users (3) | — | 1 each | Feedback session (~90 min) |
| Domain curator | 0.2 | 2 | Template/review terminology |

**Minimum:** PM + 0.5 UX designer for 2 weeks.

### 4.2 Software & tools

| Tool | Purpose | Cost |
|------|---------|------|
| Figma (or Penpot) | Wireframes, prototypes | Free–$15/user/mo |
| Miro / FigJam | Workshop whiteboard | Free tier OK |
| shadcn/ui reference | Component alignment | Free |
| Screen ruler / accessibility checker | Contrast, touch targets | Free |

### 4.3 Knowledge inputs required

| Input | Source | Used for |
|-------|--------|----------|
| PRD feature list | DOC-101 | Screen scope |
| URS must-requirements | DOC-201 | Acceptance alignment |
| Pilot AS-IS workflows | MOV-001 | Flow realism |
| Review types & templates | MOV-002 corpus | Form fields |
| Role permissions draft | MOV-007 (parallel draft) | Access matrix |

---

## 5. Cost Estimate (MOV-006 only)

| Item | Low | High | Notes |
|------|-----|------|-------|
| UX designer (contract, 10 days) | $2,000 | $6,000 | Region-dependent |
| PM time (internal) | — | — | Absorbed |
| Figma license | $0 | $180 | 3 months |
| User workshop refreshments | $50 | $200 | If in-person |
| **Total incremental** | **$2,050** | **$6,380** | Excludes internal salary |

---

## 6. Information Architecture (MVP)

```text
ST-EOS Portal
├── Dashboard                    ← landing after login
├── Knowledge
│   ├── Repository               ← browse, upload, preview
│   └── Search & Ask             ← RAG Q&A with citations
├── Workflows
│   ├── Document Review          ← Flow 1 (primary)
│   └── Document Create          ← Flow 2 (primary)
├── Assistant                    ← Research OR Evaluation module
├── My Work
│   ├── Recent outputs
│   └── Exports
└── Admin (role-gated)
    ├── Users & roles
    ├── Templates
    ├── Audit log
    └── System status
```

---

## 7. Core Flow 1 — Document Review

### 7.1 Flow diagram

```text
┌─────────────┐
│  Dashboard  │
└──────┬──────┘
       │ click "Review Document"
       ▼
┌─────────────────────┐
│ Step 1: Select Doc  │  upload new OR pick from repository
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 2: Review Type │  □ Completeness  □ Format
│                     │  □ Logic         □ Compliance
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 3: Processing  │  progress bar, ~30–120 sec
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 4: Findings    │  grouped by severity
│                     │  Critical / Major / Minor / Info
│  [1] Missing abs…   │  ← links to doc section/page
│  [2] Format dev…    │
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 5: User Action │  accept / dismiss / add comment
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 6: Export      │  PDF / DOCX review report
└─────────────────────┘
```

### 7.2 Screen list — Flow 1

| Screen ID | Name | Key elements |
|-----------|------|--------------|
| SCR-R01 | Review entry | CTA from dashboard, recent reviews |
| SCR-R02 | Document picker | Upload zone + searchable doc table |
| SCR-R03 | Review config | Checkboxes, policy doc auto-select |
| SCR-R04 | Processing | Spinner, cancel, estimated time |
| SCR-R05 | Findings panel | Filter by severity, expand detail |
| SCR-R06 | Finding detail | Excerpt, suggestion, section ref |
| SCR-R07 | Export dialog | Format, include/exclude sections |

### 7.3 UX rules (non-negotiable)

| Rule | Rationale |
|------|-----------|
| Show review type descriptions | Users must understand what AI checks |
| Never hide source policy docs used | Compliance transparency |
| Findings must link to page/section | Actionable, not vague |
| Allow dismiss with reason | Captures false-positive signal for improvement |
| Disclaimer banner on every AI output | "Advisory only — human decision required" |

---

## 8. Core Flow 2 — Knowledge Search & Document Draft

### 8.1 Flow diagram

```text
┌─────────────┐
│  Dashboard  │
└──────┬──────┘
       │ click "Search Knowledge"
       ▼
┌─────────────────────┐
│ Search & Ask        │  query box + filters (type, date, dept)
└──────────┬──────────┘
           ▼
┌─────────────────────┐     ┌──────────────────┐
│ Answer panel        │────▶│ Sources sidebar  │
│ with [1][2] cites   │     │ chunk excerpts   │
└──────────┬──────────┘     └──────────────────┘
           │ optional: "Create document from this"
           ▼
┌─────────────────────┐
│ Template picker     │  proposal / report / minutes / evaluation
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Input wizard        │  title, topic, budget, duration…
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Draft generation    │  progress, sections filling
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Draft editor        │  rich text, citations preserved
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Export              │  PDF / DOCX + bibliography
└─────────────────────┘
```

### 8.2 Screen list — Flow 2

| Screen ID | Name | Key elements |
|-----------|------|--------------|
| SCR-S01 | Search home | Query, filters, recent queries |
| SCR-S02 | Results | Answer + inline citations |
| SCR-S03 | Source panel | Expandable chunks, open full doc |
| SCR-S04 | Insufficient evidence | Empty state with guidance |
| SCR-S05 | Template gallery | Cards with preview |
| SCR-S06 | Creation wizard | Dynamic fields per template |
| SCR-S07 | Generation progress | Section-by-section status |
| SCR-S08 | Draft editor | Toolbar, citation markers |
| SCR-S09 | Export | Format + citation appendix |

---

## 9. Core Flow 3 — Evaluation (W2) — MVP Differentiator

**Priority:** P0 — equal to Flows 1 and 2. Full screen list: [DOC-504 §10](../06-modules/DOC-504-evaluation-assistant.md).

### 9.1 Flow diagram

```text
┌─────────────┐
│  Dashboard  │
└──────┬──────┘
       │ click "Run Evaluation"
       ▼
┌─────────────────────┐
│ Step 1: New eval    │  Select campaign + rubric
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 2: Submissions │  Pick 1–20 docs (RESTRICTED)
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 3: Processing  │  Per-submission progress (batch)
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 4: Scorecard   │  Criterion scores + evidence [n]
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 5: Compare     │  Matrix (if N > 1) + ranked list
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 6: Review edit │  committee_reviewer overrides
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 7: Approve     │  committee_chair sign-off
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│ Step 8: Export      │  Committee packet PDF/DOCX
└─────────────────────┘
```

### 9.2 Screen list — Flow 3

| Screen ID | Name | Key elements |
|-----------|------|--------------|
| SCR-E01 | Evaluation home | Campaign list, recent runs |
| SCR-E02 | New evaluation wizard | Rubric → submissions → options |
| SCR-E03 | Processing | Batch progress per submission |
| SCR-E04 | Scorecard | Criterion scores, evidence expand |
| SCR-E05 | Comparison matrix | Side-by-side N submissions |
| SCR-E06 | Ranking view | Ordered list + justification |
| SCR-E07 | Reviewer edit | Override score + comment |
| SCR-E08 | Approval gate | Chair sign-off |
| SCR-E09 | Export dialog | PDF/DOCX committee packet |
| SCR-E10 | Rubric manager | Curator CRUD |

### 9.3 UX rules (evaluation)

| Rule | Rationale |
|------|-----------|
| Banner: "AI advisory — human approval required" | Legal / policy |
| Export disabled until approved | [DOC-307](../04-architecture/DOC-307-rbac-specification.md) |
| Show evidence per criterion | Fairness, audit |
| Flag low-confidence scores | Corpus gaps |

---

## 10. Secondary Flows (MVP — lighter design)

| Flow | Entry | Screens | Priority |
|------|-------|---------|----------|
| Repository browse | Knowledge → Repository | 3 | P0 |
| Upload document | Repository → Upload | 2 | P0 |
| Assistant task | Assistant → Evaluation (Flow 3) | 10 | P0 |
| Admin users | Admin → Users | 2 | P1 |
| Audit log view | Admin → Audit | 1 | P1 |

---

## 11. Dashboard Wireframe (ASCII)

```text
┌────────────────────────────────────────────────────────────────────┐
│ ST-EOS          [Search…]              🔔  User ▼  Admin          │
├────────────┬───────────────────────────────────────────────────────┤
│            │  Welcome back, Dr. Chen                                 │
│ Dashboard  │  ─────────────────────────────────────────────────  │
│ Knowledge  │  Quick Actions                                          │
│ Workflows  │  ┌────────────┐ ┌────────────┐ ┌────────────┐         │
│ Assistant  │  │ 🔍 Search  │ │ 📋 Review  │ │ 📝 Create  │         │
│ My Work    │  └────────────┘ └────────────┘ └────────────┘         │
│ Admin      │                                                         │
│            │  Recent Activity          System Status                 │
│            │  • Review: Proposal #42   Documents: 8,432 indexed    │
│            │  • Search: "water mgmt"   LLM: online                  │
│            │  • Draft: Research prop   Queue: 2 jobs                │
└────────────┴───────────────────────────────────────────────────────┘
```

---

## 12. Role × Screen Access Matrix

| Screen / Action | Admin | Curator | Reviewer | User |
|-----------------|-------|---------|----------|------|
| Dashboard | ✓ | ✓ | ✓ | ✓ |
| Search & Ask | ✓ | ✓ | ✓ | ✓ |
| Upload document | ✓ | ✓ | ✓ | ✓ |
| Edit metadata | ✓ | ✓ | · | · |
| Document review | ✓ | ✓ | ✓ | ✓ |
| Document create | ✓ | ✓ | ✓ | ✓ |
| Assistant module | ✓ | ✓ | ✓ | ✓ |
| Manage templates | ✓ | ✓ | · | · |
| User management | ✓ | · | · | · |
| Audit log | ✓ | · | · | · |
| View restricted docs | ✓ | ✓* | ✓* | · |

*If role granted explicit restricted access.

---

## 13. Component Library Alignment

Use consistent components across flows (maps to shadcn/ui or equivalent):

| Component | Used in |
|-----------|---------|
| `TaskWizard` (steps 1–N) | Review, Create |
| `CitationChip` [1] | Search, Draft, Review |
| `SeverityBadge` | Review findings |
| `SourcePanel` | Search, Assistant |
| `DocumentPicker` | Review, Assistant |
| `ProcessingJobCard` | Ingestion, Review, Generate |
| `EmptyState` | No results, insufficient evidence |
| `AiDisclaimerBanner` | All AI output screens |

---

## 14. Day-by-Day Schedule

| Day | Activity | Output |
|-----|----------|--------|
| D1 | Kickoff; review PRD + pilot workflows | Workshop notes |
| D2 | IA + navigation; dashboard wireframe | IA doc v1 |
| D3 | Flow 1 wireframes (SCR-R01–R07) | Figma page: Review |
| D4 | Flow 2 wireframes (SCR-S01–S09) | Figma page: Search & Create |
| D5 | Repository + Assistant screens | Figma page: Secondary |
| D6 | Role matrix; admin screens | Access matrix v1 |
| D7 | Clickable prototype (happy paths) | Figma prototype |
| D8 | Pilot user session #1 (3 users) | Feedback log |
| D9 | Revise wireframes from feedback | v2 wireframes |
| D10 | Dev handoff meeting; annotate specs | Handoff pack |

---

## 15. Deliverables Checklist

| # | Deliverable | Format | Owner |
|---|-------------|--------|-------|
| D1 | Information architecture | MD + diagram | UX |
| D2 | Wireframes (24+ screens) | Figma | UX |
| D3 | Clickable prototype (2 core flows) | Figma | UX |
| D4 | Screen inventory spreadsheet | XLSX/MD | PM |
| D5 | Role × screen access matrix | MD | PM |
| D6 | Component list for frontend | MD | UX + FE |
| D7 | User feedback summary | MD | PM |
| D8 | UX sign-off from sponsor | Email/PDF | Sponsor |

---

## 16. Risks & Mitigations

| ID | Risk | Likelihood | Impact | Mitigation |
|----|------|------------|--------|------------|
| R1 | Chat-style UI preferred by users | Medium | High | Show task wizard in demo; cite time savings |
| R2 | Too many screens for MVP | Medium | Medium | Strict P0/P1 tag; defer admin polish |
| R3 | Pilot users unavailable | Medium | High | Schedule Day 8 early; backup internal domain experts |
| R4 | UX not aligned with API reality | Low | High | Frontend + tech lead review on Day 5 |
| R5 | Bilingual UI requirement emerges | Medium | Medium | Capture in open issues; plan i18n shell in Sprint 0 |

---

## 17. Exit Criteria (Gate G2 input)

- [ ] Flow 1 and Flow 2 wireframes approved by sponsor
- [ ] 3 pilot users reviewed prototype; feedback incorporated
- [ ] Screen inventory matches PRD P0 features
- [ ] Role access matrix agreed with MOV-007
- [ ] Frontend developer confirmed estimates per screen group
- [ ] No unresolved P0 UX questions before Sprint 1

---

## 18. Handoff to Development

Frontend Sprint mapping:

| Sprint | UX screens consumed |
|--------|---------------------|
| Sprint 0 | Shell, login, dashboard skeleton |
| Sprint 1 | SCR-R02, repository, upload |
| Sprint 2 | SCR-S01–S04 (search) |
| Sprint 3 | SCR-R01–R07 (review) |
| Sprint 4 | SCR-S05–S09 (create) |
| Sprint 5 | SCR-E01–E06 (evaluation core) |
| Sprint 6 | SCR-E07–E10 + admin, audit, polish |

---

## Related Documents

- [Next Movements Playbook](../00-next-movements.md)
- [PRD DOC-101](../02-product/DOC-101-product-requirements.md)
- [MOV-007 Security](./MOV-007-security-data-governance.md)
- [MOV-008 Sprint 0](./MOV-008-mvp-build-sprint0.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial detailed movement doc |
| 1.1 | 2026-06-30 | Flow 3 Evaluation; 6-role RBAC; DOC-307 alignment |
