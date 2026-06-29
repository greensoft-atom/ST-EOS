# DOC-101 — Product Requirements Document (PRD)

**Document ID:** DOC-101  
**Version:** 1.0 (MVP focus)  
**Date:** 2026-06-29  
**Status:** Draft

---

## 1. Document Purpose

This PRD defines product features, functional requirements, non-functional requirements, and acceptance criteria for ST-EOS MVP (Version 0.9).

---

## 2. Product Summary

ST-EOS MVP delivers an institutional knowledge platform with AI-powered search, document review, template-based creation, and one department assistant — deployed on local infrastructure.

---

## 3. MVP Feature List

| ID | Feature | Priority | Phase |
|----|---------|----------|-------|
| F-001 | Document Repository | P0 | MVP |
| F-002 | Metadata & Classification | P0 | MVP |
| F-003 | Ingestion Pipeline | P0 | MVP |
| F-004 | RAG Search & Q&A | P0 | MVP |
| F-005 | Document Review | P0 | MVP |
| F-006 | Document Creation (Templates) | P0 | MVP |
| F-007 | Department Assistant (1) | P0 | MVP |
| F-008 | Authentication & RBAC | P0 | MVP |
| F-009 | Audit Logging | P0 | MVP |
| F-010 | Export Outputs | P1 | MVP |
| F-011 | Admin Dashboard | P1 | MVP |

---

## 4. Functional Requirements

### F-001 — Document Repository

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| FR-001-01 | System shall accept PDF and plain text uploads | Upload succeeds for PDF, TXT, MD |
| FR-001-02 | System shall store original files immutably | Original retrievable after processing |
| FR-001-03 | System shall display document list with filters | Filter by type, date, department |
| FR-001-04 | System shall support document preview | PDF rendered in browser |
| FR-001-05 | System shall track processing status | States: pending, processing, indexed, failed |

### F-002 — Metadata & Classification

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| FR-002-01 | System shall capture mandatory metadata | title, type, language, date |
| FR-002-02 | System shall support optional metadata | author, department, keywords, source |
| FR-002-03 | System shall map documents to knowledge layers | Layer 1–4 per taxonomy |
| FR-002-04 | Curators shall edit metadata post-ingestion | Edit saved and re-indexed if needed |

### F-003 — Ingestion Pipeline

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| FR-003-01 | System shall extract text from PDFs | Text extraction ≥ 95% on text-native PDFs |
| FR-003-02 | System shall OCR scanned PDFs when needed | OCR applied when text layer absent |
| FR-003-03 | System shall chunk documents | Chunks with overlap; chunk ID traceable |
| FR-003-04 | System shall generate embeddings | All chunks embedded in vector index |
| FR-003-05 | System shall log ingestion errors | Failed docs visible to admin |

### F-004 — RAG Search & Q&A

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| FR-004-01 | Users shall search via natural language query | Query returns within 10 seconds |
| FR-004-02 | System shall return answer with citations | Each claim links to source chunk(s) |
| FR-004-03 | Users shall view source excerpts | Click citation → see doc excerpt |
| FR-004-04 | Users shall filter search by metadata | type, date range, department |
| FR-004-05 | System shall indicate insufficient evidence | Explicit message when retrieval weak |

### F-005 — Document Review

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| FR-005-01 | Users shall submit document for AI review | Select doc + review type |
| FR-005-02 | System shall support review types | completeness, format, logic, compliance |
| FR-005-03 | System shall produce structured findings | Severity: critical, major, minor, info |
| FR-005-04 | Findings shall reference document sections | Section/page indicated |
| FR-005-05 | Users shall export review report | PDF or DOCX export |
| FR-005-06 | Review shall use institutional policies when available | Policy docs retrieved via RAG |

**Review types defined:**

| Type | Checks |
|------|--------|
| Completeness | Required sections present |
| Format | Template structure, headings, numbering |
| Logic | Internal consistency, unsupported claims flagged |
| Compliance | Alignment with policy/guideline documents |

### F-006 — Document Creation (Templates)

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| FR-006-01 | System shall maintain template library | Admin/curator CRUD templates |
| FR-006-02 | Users shall generate document from template | Select template + provide inputs |
| FR-006-03 | Generation shall use RAG context | Relevant sources cited in draft |
| FR-006-04 | Users shall edit draft in UI | Rich text or markdown editor |
| FR-006-05 | System shall support MVP template types | research proposal, review report, meeting minutes, evaluation summary |

### F-007 — Department Assistant (One Module)

**Option A — Research Assistant**

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| FR-007A-01 | Generate literature review outline | Sections with cited sources |
| FR-007A-02 | Generate research proposal draft | Follows proposal template |
| FR-007A-03 | Recommend methodology | Based on similar internal reports |
| FR-007A-04 | Identify research gaps | Gap list with supporting citations |

**Option B — Evaluation Assistant**

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| FR-007B-01 | Score proposal against rubric | Scores per criterion with evidence |
| FR-007B-02 | Compare multiple submissions | Side-by-side comparison table |
| FR-007B-03 | Assess feasibility and risk | Structured risk list |
| FR-007B-04 | Rank submissions | Ordered list with justification |

### F-008 — Authentication & RBAC

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| FR-008-01 | Users shall authenticate with username/password | Login/logout works |
| FR-008-02 | System shall enforce roles | admin, curator, reviewer, user |
| FR-008-03 | Restricted documents visible only to authorized roles | Access denied without permission |
| FR-008-04 | Admin shall manage users | CRUD users and roles |

**Role permissions matrix (MVP):**

| Action | Admin | Curator | Reviewer | User |
|--------|-------|---------|----------|------|
| Upload documents | ✓ | ✓ | ✓ | ✓ |
| Edit metadata | ✓ | ✓ | · | · |
| Manage templates | ✓ | ✓ | · | · |
| Run AI review | ✓ | ✓ | ✓ | ✓ |
| Manage users | ✓ | · | · | · |
| View audit log | ✓ | · | · | · |

### F-009 — Audit Logging

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| FR-009-01 | System shall log all AI interactions | user, timestamp, query, model, sources |
| FR-009-02 | Admin shall query audit log | Filter by user, date, feature |
| FR-009-03 | Logs shall be immutable | Append-only storage |

### F-010 — Export Outputs

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| FR-010-01 | Export review reports | PDF/DOCX |
| FR-010-02 | Export created documents | PDF/DOCX |
| FR-010-03 | Export includes citations | Source list attached |

---

## 5. Non-Functional Requirements

| ID | Category | Requirement | Target |
|----|----------|-------------|--------|
| NFR-01 | Performance | Search response time | ≤ 10s (p95) |
| NFR-02 | Performance | Review generation time | ≤ 120s for 50-page doc |
| NFR-03 | Scalability | Concurrent users (MVP) | ≥ 30 |
| NFR-04 | Availability | Pilot uptime | ≥ 99% business hours |
| NFR-05 | Security | Data at rest encryption | AES-256 or equivalent |
| NFR-06 | Security | Transport encryption | TLS 1.2+ |
| NFR-07 | Privacy | No external data transmission | LLM inference local only |
| NFR-08 | Maintainability | Deploy via containers | Docker Compose minimum |
| NFR-09 | Usability | Task completion without training | Core flows ≤ 5 clicks |
| NFR-10 | Localization | UI language | Match pilot institution |
| NFR-11 | Audit | Retention | AI logs retained ≥ 1 year |

---

## 6. User Stories (MVP Sample)

```text
US-001: As a research officer, I want to search the institutional repository
        with a natural language question so that I find relevant past work quickly.

US-002: As a reviewer, I want AI to check a proposal for missing sections
        so that I don't manually compare against the template.

US-003: As a grant administrator, I want to generate an evaluation summary
        from a template so that committee packets are prepared faster.

US-004: As a curator, I want to tag documents with type and department
        so that search filters return accurate results.

US-005: As an admin, I want to see who queried the AI and what sources were used
        so that I can audit system usage.
```

---

## 7. Out of Scope (MVP)

Explicitly excluded — see [Next Movements](../00-next-movements.md):

- Multi-agent orchestration
- External web scouting/crawling
- Custom model fine-tuning
- SSO/LDAP (unless pilot mandates — then P1)
- Mobile native apps
- Real-time collaboration/editing
- Full patent prosecution workflow
- Automated final decisions without human approval

---

## 8. Dependencies

| Dependency | Owner | Required by |
|------------|-------|-------------|
| Local LLM runtime | Infra | Sprint 2 |
| MVP document corpus | Data team | Sprint 1 |
| Templates (5+) | Domain curator | Sprint 4 |
| Pilot institution | Sponsor | Phase 0 |
| GPU/server hardware | Infra | Sprint 0 |

---

## 9. Acceptance Criteria (MVP Release)

MVP is accepted when:

1. All P0 functional requirements pass QA
2. RAG citation accuracy ≥ 80% on evaluation set
3. Document review detects ≥ 75% of intentional omissions in test set
4. 5 templates operational for document creation
5. Pilot institution confirms readiness for 8-week evaluation
6. Security checklist complete
7. Admin and user documentation draft available

---

## 10. Open Questions

| # | Question | Owner | Due |
|---|----------|-------|-----|
| Q1 | Research or Evaluation assistant for MVP? | **Evaluation Assistant** (government executive pilot) | Closed |
| Q2 | Primary UI language? | Pilot institution | Phase 0 W2 |
| Q3 | SSO required for pilot? | Pilot IT | Phase 0 W4 |
| Q4 | Maximum document size? | Tech lead | Phase 0 W4 |

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial MVP PRD |
