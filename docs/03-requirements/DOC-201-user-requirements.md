# DOC-201 — User Requirement Specification (URS)

**Document ID:** DOC-201  
**Version:** 1.0 (MVP)  
**Date:** 2026-06-29  
**Status:** Draft

---

## 1. Purpose

This URS captures user-facing requirements for ST-EOS from the perspective of science and technology executive organizations. Requirements are prioritized using MoSCoW:

- **M** — Must have (MVP blocker)
- **S** — Should have (MVP if time permits)
- **C** — Could have (Phase 2)
- **W** — Won't have (this release)

---

## 2. User Classes

| Class | Description |
|-------|-------------|
| UC-01 General User | Researchers, officers, analysts |
| UC-02 Reviewer | Committee members, evaluators |
| UC-03 Curator | Librarians, domain specialists managing corpus |
| UC-04 Administrator | IT admin, system operator |
| UC-05 Executive | Directors viewing summaries (Phase 2 dashboards) |

---

## 3. Platform Requirements

### 3.1 Knowledge access

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-001 | The system shall allow users to upload PDF and text documents | M |
| URS-002 | The system shall index uploaded documents for search within 24 hours | M |
| URS-003 | The system shall allow users to search using natural language questions | M |
| URS-004 | The system shall show source citations for AI-generated answers | M |
| URS-005 | The system shall allow filtering search by document type and date | M |
| URS-006 | The system shall indicate when it cannot find sufficient evidence | M |
| URS-007 | The system should support bulk upload of document folders | S |
| URS-008 | The system could support saved searches and alerts | C |

### 3.2 Document review

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-010 | The system shall review documents for missing required sections | M |
| URS-011 | The system shall review documents for formatting against templates | M |
| URS-012 | The system shall flag logical inconsistencies and unsupported claims | M |
| URS-013 | The system shall check compliance against institutional policy documents | M |
| URS-014 | The system shall produce a structured review report with severity levels | M |
| URS-015 | The system shall allow export of review reports | M |
| URS-016 | The system should support reviewer comments on AI findings | S |
| URS-017 | The system could support multi-reviewer approval workflows | C |

### 3.3 Document creation

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-020 | The system shall generate documents from institutional templates | M |
| URS-021 | The system shall use retrieved knowledge when drafting content | M |
| URS-022 | The system shall include citations in generated drafts | M |
| URS-023 | The system shall allow users to edit generated drafts before export | M |
| URS-024 | The system shall support research proposal generation | M |
| URS-025 | The system shall support evaluation report generation | M |
| URS-026 | The system should support work plan and roadmap generation | S |
| URS-027 | The system could support meeting minutes generation | S |

### 3.4 Work planning & design

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-030 | The system should generate work plans with milestones and timelines | S |
| URS-031 | The system should identify risks in proposed work plans | S |
| URS-032 | The system could generate roadmaps from goals, budget, and resources | C |
| URS-033 | The system could collect feedback on plans and suggest revisions | C |

### 3.5 Analysis, comparison & evaluation

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-040 | The system shall compare multiple documents or projects side by side | M |
| URS-041 | The system shall score submissions against configurable rubrics | M |
| URS-042 | The system shall provide feasibility and risk assessment | M |
| URS-043 | The system shall rank projects with justification | M |
| URS-044 | The system should perform SWOT analysis on projects | S |
| URS-045 | The system could support multi-criteria decision analysis | C |

### 3.6 Research services

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-050 | The system shall generate literature review summaries from corpus | M |
| URS-051 | The system shall assist in research proposal creation | M |
| URS-052 | The system shall suggest methodology based on similar studies | M |
| URS-053 | The system shall identify research gaps | M |
| URS-054 | The system should extract and format citations | S |

### 3.7 Innovation & technology scouting

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-060 | The system should suggest innovation opportunities from internal corpus | S |
| URS-061 | The system should analyze technology trends in stored documents | S |
| URS-062 | The system could ingest curated external technology sources | C |
| URS-063 | The system could monitor external publications for scouting | C |
| URS-064 | The system won't autonomously crawl the open web in MVP | W |

### 3.8 Patent services (Phase 2)

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-070 | The system could search prior art in patent corpus | C |
| URS-071 | The system could assess novelty of invention descriptions | C |
| URS-072 | The system could support claim analysis | C |

### 3.9 Solution & decision support

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-080 | The system should propose solutions to stated S&T problems using corpus | S |
| URS-081 | The system should present options with pros, cons, and risks | S |
| URS-082 | The system could provide executive decision briefings | C |
| URS-083 | The system won't make binding decisions without human approval | M |

### 3.10 Administration & governance

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-090 | The system shall authenticate users | M |
| URS-091 | The system shall enforce role-based access | M |
| URS-092 | The system shall log all AI interactions for audit | M |
| URS-093 | The system shall run entirely on local infrastructure | M |
| URS-094 | The system should support document classification levels | S |
| URS-095 | The system could integrate with LDAP/SSO | C |

---

## 4. Usability Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-U01 | Core tasks shall be accessible within 3 clicks from dashboard | M |
| URS-U02 | System shall provide task wizards for review and creation flows | M |
| URS-U03 | AI outputs shall clearly distinguish facts (cited) from suggestions | M |
| URS-U04 | System shall display processing progress for long operations | S |
| URS-U05 | System should provide contextual help per module | S |

---

## 5. Performance Requirements

| ID | Requirement | Target |
|----|-------------|--------|
| URS-P01 | Search response time | ≤ 10 seconds |
| URS-P02 | Document review (50 pages) | ≤ 2 minutes |
| URS-P03 | Document generation | ≤ 3 minutes |
| URS-P04 | Concurrent users | ≥ 30 |

---

## 6. Security & Compliance Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| URS-S01 | All data stored within organization infrastructure | M |
| URS-S02 | No document content sent to external AI services | M |
| URS-S03 | Audit trail for AI queries and outputs | M |
| URS-S04 | Encrypted storage and TLS in transit | M |
| URS-S05 | Restricted documents accessible only to authorized users | M |

---

## 7. MVP Requirement Summary

| Priority | Count |
|----------|-------|
| Must (M) | 38 |
| Should (S) | 14 |
| Could (C) | 14 |
| Won't (W) | 1 |

**MVP delivery = all Must requirements + maximum Should requirements feasible in timeline.**

---

## 8. Traceability

Requirements map to PRD features:

| URS range | PRD feature |
|-----------|-------------|
| URS-001–008 | F-001, F-003, F-004 |
| URS-010–017 | F-005 |
| URS-020–027 | F-006 |
| URS-040–045 | F-007 (Evaluation) |
| URS-050–054 | F-007 (Research) |
| URS-090–095 | F-008, F-009 |

Full traceability matrix: DOC-205 (planned).

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial MVP URS |
