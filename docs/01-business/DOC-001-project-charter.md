# DOC-001 — Project Charter

**Project name:** ST-EOS (Science & Technology Executive Operating System)  
**Document ID:** DOC-001  
**Version:** 1.1  
**Date:** 2026-06-29  
**Status:** Draft for approval  
**Pilot institution:** [Ministry of Science, Technology and Innovation (MSTI)](./DOC-PILOT-001-government-executive-pilot-scope.md)

---

## 1. Project Authorization

This charter authorizes the ST-EOS program to design and deliver an AI-powered platform for science and technology executive and business operations, using local LLM infrastructure and institutional knowledge assets.

---

## 2. Vision

To become the trusted AI operating system for science, technology, innovation, and research management — enabling executives and staff to review, create, plan, evaluate, and decide with institutional knowledge at their fingertips, without compromising data sovereignty.

---

## 3. Mission

Build a modular, local-first platform that embeds AI into real S&T workflows — starting with knowledge access, document review, and structured document creation — and expanding to department-specific expert assistants.

---

## 4. Problem Statement

Science and technology executive organizations manage large volumes of heterogeneous documents (research, patents, exhibitions, reports, policies, templates) across multiple departments. Staff spend excessive time on:

- Manual document review and compliance checking
- Literature and prior-art search
- Drafting plans, proposals, and reports from scratch
- Comparing and evaluating projects with inconsistent criteria
- Retrieving institutional knowledge scattered in PDF archives

Generic AI tools lack domain context, local deployment options, and workflow integration. Existing document systems lack intelligent assistance.

---

## 5. Proposed Solution

ST-EOS integrates:

1. **Knowledge repository** — Ingested PDF/text corpus with metadata
2. **RAG-powered search** — Citation-backed answers from institutional documents
3. **AI workflow services** — Review, create, plan, evaluate, scout, report
4. **Department assistants** — Configured expert agents per organizational unit
5. **Local LLM runtime** — On-premise inference for data sovereignty

---

## 6. Goals & Success Criteria

### 6.1 Program goals (Year 1)

| # | Goal | Success indicator |
|---|------|-------------------|
| G1 | Deliver MVP to pilot institution | Live deployment |
| G2 | Prove AI document review and creation value | ≥ 30% time reduction in pilot workflows |
| G3 | Establish trusted knowledge retrieval | ≥ 80% user satisfaction on search |
| G4 | Foundation for multi-module expansion | Architecture supports 3+ assistants |

### 6.2 Non-goals (Year 1)

- National-scale public deployment
- Autonomous decision-making without human review
- Replacement of existing ERP/grant systems
- Consumer-facing product

---

## 7. Scope

### 7.1 In scope (Phase 1 — MVP)

- Document ingestion and repository
- Metadata management
- RAG search with source citations
- Document review (completeness, format, logic, compliance hints)
- Template-based document creation
- One vertical assistant (**Evaluation Assistant** — government executive pilot; see [DOC-PILOT-001](./DOC-PILOT-001-government-executive-pilot-scope.md))
- User authentication and role-based access
- AI interaction audit logging

### 7.2 Out of scope (Phase 1)

- Multi-agent cross-department orchestration
- External web technology scouting
- Custom LLM fine-tuning
- Mobile applications
- Full patent prosecution workflow
- National knowledge graph

### 7.3 Future phases

See [Product Roadmap](../02-product/DOC-102-product-roadmap.md).

---

## 8. Stakeholders

| Role | Responsibility | Assignment (MSTI) |
|------|----------------|-------------------|
| Executive Sponsor | Funding, strategic alignment | Director-General, MSTI |
| Program Manager | Delivery, scope, timeline | Appointed by DG office (ST-EOS program) |
| Technical Lead | Architecture, engineering | ST-EOS development team |
| AI/RAG Lead | Models, retrieval, prompts | ST-EOS development team |
| Data Lead | Corpus, metadata, governance | Strategic Planning + Research Programs (curator lead) |
| Pilot Institution Lead | Requirements, acceptance | Director, Research Programs and Grant Administration |
| Pilot Champion | Day-to-day pilot coordination | Program Evaluation Division Head, MSTI |
| IT Sponsor | Hosting, security, SSO path | Director, IT and Digital Transformation Division |
| Domain Curators | Content quality, taxonomy | Research Programs + Exhibition Secretariat |

---

## 9. High-Level Timeline

| Phase | Duration | Deliverable |
|-------|----------|-------------|
| Phase 0 — Discovery | 8 weeks | PoC, requirements, architecture |
| Phase 1 — MVP Build | 14 weeks | Pilot-ready platform |
| Pilot — Deployment & Measurement | 8 weeks | Measured deployment at MSTI |
| Phase 2 — Expansion | 26 weeks | Additional modules |

**Canonical phase naming:** [00-mvp-decisions.md](../00-mvp-decisions.md)

**Target MVP delivery:** ~6 months from charter approval (subject to team availability).

---

## 10. Budget Estimate (Indicative)

| Category | Estimate | Notes |
|----------|----------|-------|
| Core team (6 months) | Variable | 4–6 FTE equivalent |
| GPU/server hardware | One-time | Local LLM inference |
| Software/licenses | Low | Open-source preferred |
| Pilot support | Variable | Training, customization |
| Contingency | 15% | Scope and infra buffer |

Detailed budget requires hardware sizing and team confirmation.

---

## 11. Assumptions

1. Local LLM infrastructure is available or procurable
2. Document corpus rights permit internal platform use
3. One pilot institution commits to 8-week evaluation
4. Open-source stack is acceptable to pilot customer
5. Initial UI language aligns with corpus primary language

---

## 12. Constraints

1. **Data sovereignty** — No mandatory cloud LLM dependency
2. **Human oversight** — AI outputs are advisory for official decisions
3. **Resource limit** — MVP team ≤ 6 people
4. **Time** — MVP within 6 months

---

## 13. Risks (Summary)

| Risk | Severity | Owner |
|------|----------|-------|
| Corpus quality insufficient | High | Data Lead |
| Local LLM underperforms | Medium | AI Lead |
| Scope creep | High | PM |
| No pilot customer | High | Sponsor |
| User distrust of AI | Medium | PM |

Full mitigation in [Executive Assessment](../00-executive-assessment.md).

---

## 14. Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Executive Sponsor | | | |
| Program Manager | | | |
| Technical Lead | | | |

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-06-29 | Program Office | Initial charter |
| 1.1 | 2026-06-29 | Program Office | MSTI pilot institution; stakeholder assignments |
| 1.2 | 2026-06-30 | Program Office | Phase naming aligned with 00-mvp-decisions |
