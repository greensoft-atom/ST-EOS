# DOC-202 — Software Requirements Specification (SRS)

**Document ID:** DOC-202  
**Version:** 1.0 (MVP)  
**Date:** 2026-06-30  
**Status:** Draft for build  
**Traceability:** [DOC-205 Traceability Matrix](./DOC-205-traceability-matrix.md)  
**User requirements:** [DOC-201](./DOC-201-user-requirements.md)

---

## 1. Purpose

This SRS translates MVP user requirements into **software-level requirements** suitable for development, QA, and pilot acceptance. Scope: ST-EOS Version 0.9 (MVP) for MSTI pilot.

**Locked decisions:** [00-mvp-decisions.md](../00-mvp-decisions.md)

---

## 2. System Context

```text
[Browser] ──HTTPS──▶ [Nginx] ──▶ [FastAPI Backend]
                                      ├── PostgreSQL + pgvector
                                      ├── Redis (job queue)
                                      ├── Filesystem document store
                                      └── Ollama (local LLM)
```

External systems: **none in MVP** (no SSO, no grant system API).

---

## 3. Functional Requirements (Software)

### 3.1 Authentication & authorization

| ID | Requirement | Priority |
|----|-------------|----------|
| SRS-AUTH-01 | System shall authenticate users via username/password and issue JWT access + refresh tokens | P0 |
| SRS-AUTH-02 | Access token TTL shall be 15 minutes; refresh 7 days | P0 |
| SRS-AUTH-03 | System shall enforce RBAC per [DOC-307](../04-architecture/DOC-307-rbac-specification.md) on every API route | P0 |
| SRS-AUTH-04 | System shall lock account after 5 failed logins for 15 minutes | P0 |
| SRS-AUTH-05 | System shall record AUD-001, AUD-002, AUD-012 | P0 |

### 3.2 Document repository & ingestion

| ID | Requirement | Priority |
|----|-------------|----------|
| SRS-DOC-01 | System shall accept PDF, TXT, MD uploads up to 50 MB per file | P0 |
| SRS-DOC-02 | System shall require classification on upload (PUB/INT/RST/CNF) | P0 |
| SRS-DOC-03 | System shall process uploads asynchronously via job queue | P0 |
| SRS-DOC-04 | System shall extract text, chunk, embed, and index into pgvector | P0 |
| SRS-DOC-05 | Document status shall be: pending, processing, indexed, failed | P0 |
| SRS-DOC-06 | System shall store original files immutably under configurable path | P0 |
| SRS-DOC-07 | Bulk ingest CLI shall support batch load for pilot corpus | P1 |

### 3.3 RAG search

| ID | Requirement | Priority |
|----|-------------|----------|
| SRS-RAG-01 | System shall answer natural-language queries using top-K retrieval + LLM | P0 |
| SRS-RAG-02 | Responses shall include inline citations resolvable to source chunks | P0 |
| SRS-RAG-03 | Retrieval shall pre-filter by user access class before similarity search | P0 |
| SRS-RAG-04 | System shall return insufficient-evidence message when max score < threshold | P0 |
| SRS-RAG-05 | End-to-end query p95 shall be ≤ 10 seconds on pilot hardware | P0 |
| SRS-RAG-06 | System shall log AUD-006 with chunk IDs and model version | P0 |

### 3.4 Document review

| ID | Requirement | Priority |
|----|-------------|----------|
| SRS-REV-01 | System shall support review types: completeness, format, logic, compliance | P0 |
| SRS-REV-02 | Findings shall be structured JSON with severity levels | P0 |
| SRS-REV-03 | Compliance review shall retrieve policy documents via RAG | P0 |
| SRS-REV-04 | System shall export review report as PDF or DOCX | P0 |
| SRS-REV-05 | System shall log AUD-007 | P0 |

### 3.5 Document creation

| ID | Requirement | Priority |
|----|-------------|----------|
| SRS-CRE-01 | System shall load templates from YAML registry | P0 |
| SRS-CRE-02 | Generation shall inject RAG context with citations | P0 |
| SRS-CRE-03 | User shall edit draft in browser before export | P0 |
| SRS-CRE-04 | MVP shall ship ≥ 5 templates including evaluation summary | P0 |
| SRS-CRE-05 | System shall log AUD-008, AUD-009 | P0 |

### 3.6 Evaluation Assistant

| ID | Requirement | Priority |
|----|-------------|----------|
| SRS-EVAL-01 | System shall CRUD evaluation rubrics (YAML/JSON schema) | P0 |
| SRS-EVAL-02 | System shall score submission against rubric with per-criterion evidence | P0 |
| SRS-EVAL-03 | Batch evaluation shall support 1–20 submissions per job | P0 |
| SRS-EVAL-04 | System shall produce comparison matrix for N > 1 | P0 |
| SRS-EVAL-05 | System shall rank submissions with weighted totals | P0 |
| SRS-EVAL-06 | Reviewer shall override scores; chair shall approve before export | P0 |
| SRS-EVAL-07 | Export shall be blocked unless status = approved | P0 |
| SRS-EVAL-08 | System shall log AUD-010 on every scoring run | P0 |
| SRS-EVAL-09 | API shall match [DOC-504 §9](../06-modules/DOC-504-evaluation-assistant.md) | P0 |

### 3.7 Administration & audit

| ID | Requirement | Priority |
|----|-------------|----------|
| SRS-ADM-01 | Admin shall manage users and role assignment | P0 |
| SRS-ADM-02 | Admin shall query audit log with filters | P0 |
| SRS-ADM-03 | Audit log shall be append-only | P0 |
| SRS-ADM-04 | User shall acknowledge AI usage policy before first AI action (AUD-016) | P0 |

---

## 4. Non-Functional Requirements (Software)

| ID | Category | Requirement | Target |
|----|----------|-------------|--------|
| SRS-NFR-01 | Performance | Concurrent interactive users | ≥ 30 |
| SRS-NFR-02 | Performance | Review job (50 pages) | ≤ 120s p95 |
| SRS-NFR-03 | Availability | Pilot uptime (business hours) | ≥ 99% |
| SRS-NFR-04 | Security | TLS 1.2+ on user endpoints | Required |
| SRS-NFR-05 | Security | No outbound LLM API calls | Required |
| SRS-NFR-06 | Maintainability | Deploy via Docker Compose | Required |
| SRS-NFR-07 | Observability | Health endpoints: app, DB, LLM, queue depth | Required |
| SRS-NFR-08 | Data | AI audit retention | ≥ 12 months |

---

## 5. Data Requirements

- Metadata minimum: [DOC-603](../07-data/DOC-603-metadata-standard.md)
- Classification: [DOC-602](../07-data/DOC-602-data-classification.md)
- Knowledge layers: [DOC-404](../05-ai/DOC-404-knowledge-base-design.md)

---

## 6. Interface Requirements

| Interface | Standard |
|-----------|----------|
| REST API | OpenAPI 3.1; JSON payloads; `/api/v1/` prefix |
| Authentication | Bearer JWT |
| Frontend | React SPA; responsive desktop (1280px+ primary) |
| LLM | Ollama HTTP API (internal) |

Detailed evaluation endpoints: DOC-504 §9. Full OpenAPI: DOC-305 (Phase 1 sprint deliverable).

---

## 7. Acceptance Criteria (MVP Release)

MVP 0.9 is accepted when:

1. All P0 SRS requirements pass QA
2. Quality gates QG-1 through QG-6 pass ([DOC-701](../06-development/DOC-701-development-plan.md))
3. UAT scenarios UAT-01 through UAT-06 pass ([DOC-706](../06-development/DOC-706-testing-strategy.md))
4. MSTI pilot champion confirms readiness for MOV-010
5. Security checklist 12/12 ([MOV-007](../07-movements/MOV-007-security-data-governance.md))

---

## 8. Out of Scope (Software)

- SSO/LDAP (Phase 2A unless change-approved)
- DOCX upload parsing (Phase 2)
- Multi-agent orchestration
- External grant system integration
- Mobile native clients
- Research Assistant module

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-30 | Initial MVP SRS |
