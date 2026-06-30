# DOC-205 — Requirement Traceability Matrix (MVP)

**Document ID:** DOC-205  
**Version:** 1.0  
**Date:** 2026-06-30  
**Status:** Active for MVP build  
**Scope:** MSTI pilot — Evaluation Assistant MVP

---

## 1. Purpose

Map user requirements (URS) → product features (PRD) → software requirements (SRS) → sprints → test gates.

**MVP module:** Evaluation Assistant only ([ADR-005](../04-architecture/decisions/ADR-005-mvp-module-selection.md)).

---

## 2. Legend

| Code | Meaning |
|------|---------|
| M | Must — MVP acceptance |
| S | Should — deliver if capacity |
| C | Could — Phase 2 |
| W | Won't — excluded |
| ✓ | Covered in this release |

---

## 3. Platform Traceability

| URS ID | Priority | PRD | SRS | Sprint | Test |
|--------|----------|-----|-----|--------|------|
| URS-001 Upload PDF/text | M | F-001 | SRS-DOC-01 | S1 | UAT-01 |
| URS-002 Index within 24h | M | F-003 | SRS-DOC-03 | S1 | Integration |
| URS-003 NL search | M | F-004 | SRS-RAG-01 | S2 | UAT-02 |
| URS-004 Citations | M | F-004 | SRS-RAG-02 | S2 | QG-2 |
| URS-005 Metadata filters | M | F-004 | SRS-RAG-01 | S2 | UAT-02 |
| URS-006 Insufficient evidence | M | F-004 | SRS-RAG-04 | S2 | RAG eval |
| URS-007 Bulk upload | S | F-001 | SRS-DOC-07 | S1 | — |
| URS-010–015 Review | M | F-005 | SRS-REV-01–05 | S3 | UAT-03, QG-3 |
| URS-020–025 Create | M | F-006 | SRS-CRE-01–05 | S4 | UAT-04, QG-4 |
| URS-090–093 Auth/audit/local | M | F-008, F-009 | SRS-AUTH, SRS-ADM | S0 | SEC-* |
| URS-083 No binding AI decisions | M | F-007 | SRS-EVAL-06 | S5–S6 | UAT-06 |
| URS-094 Classification | S | F-002 | SRS-DOC-02 | S1 | SEC-01 |

---

## 4. Evaluation Assistant Traceability (MVP Module)

| URS ID | Priority | PRD | SRS | Sprint | Test |
|--------|----------|-----|-----|--------|------|
| URS-040 Compare submissions | M | F-007 | SRS-EVAL-04 | S5 | UAT-06 |
| URS-041 Rubric scoring | M | F-007 | SRS-EVAL-02 | S5 | Eval golden set |
| URS-042 Feasibility/risk | M | F-007 | SRS-EVAL-02 | S5 | DOC-504 §14 |
| URS-043 Rank with justification | M | F-007 | SRS-EVAL-05 | S5 | UAT-06 |
| URS-044 SWOT | S | — | — | — | Phase 2 |
| URS-045 MCDA | C | — | — | — | Phase 2 |

**DOC-504 features → sprints:**

| DOC-504 capability | SRS | Sprint |
|--------------------|-----|--------|
| Rubric CRUD | SRS-EVAL-01 | S5 |
| score_rubric tool | SRS-EVAL-02 | S5 |
| Batch worker (max 20) | SRS-EVAL-03 | S5 |
| Comparison matrix | SRS-EVAL-04 | S5 |
| Ranking | SRS-EVAL-05 | S5 |
| Reviewer edit | SRS-EVAL-06 | S6 |
| Chair approve gate | SRS-EVAL-06 | S6 |
| Export committee packet | SRS-EVAL-07 | S6 |
| Evaluation UI (SCR-E01–E10) | SRS-EVAL-09 | S5–S6 |
| Eval quality test suite | DOC-504 §14 | S6 |

---

## 5. Research Assistant — Explicitly Excluded from MVP

| URS ID | Priority (URS v1.0) | MVP status | Phase |
|--------|---------------------|------------|-------|
| URS-050 Literature review | M → **C for MVP** | Won't | Phase 2B |
| URS-051 Proposal assist | M → **C for MVP** | Won't | Phase 2B |
| URS-052 Methodology suggest | M → **C for MVP** | Won't | Phase 2B |
| URS-053 Research gaps | M → **C for MVP** | Won't | Phase 2B |
| URS-054 Citation extract | S | Won't | Phase 2B |

*URS document updated to reflect MoSCoW realignment.*

---

## 6. Pilot Workflow Traceability

| Workflow | Features | URS / DOC-504 | Success KPI |
|----------|----------|---------------|-------------|
| W1 Pre-screen | F-005, F-007 | SRS-REV, SRS-EVAL | −50% time |
| W2 Committee eval | F-007 | SRS-EVAL-01–08 | −30% time |
| W3 Plan section draft | F-004, F-006 | SRS-RAG, SRS-CRE | −40% time |

Process baselines: [DOC-005](../01-business/DOC-005-business-process-mapping.md)

---

## 7. Security & Governance Traceability

| Requirement | SRS | MOV-007 | Sprint |
|-------------|-----|---------|--------|
| RBAC 6 roles | SRS-AUTH-03 | DOC-307 | S0 |
| Retrieval pre-filter | SRS-RAG-03 | MOV-007 §7.3 | S2 |
| AUD-001–015 | SRS-ADM-03 | MOV-007 §8 | S0–S6 |
| AUD-016 policy ack | SRS-ADM-04 | AI-USAGE-POLICY | S3 |
| Security checklist 12/12 | — | MOV-007 §13 | S6 |

---

## 8. Coverage Summary

| Category | Must items | MVP covered | Gap |
|----------|------------|-------------|-----|
| Platform | 28 | 28 | 0 |
| Evaluation | 4 | 4 | 0 |
| Research (deferred) | 4 | 0 (by design) | Phase 2B |
| Security | 8 | 8 | 0 |

---

## Related Documents

- [DOC-201 URS](./DOC-201-user-requirements.md)
- [DOC-202 SRS](./DOC-202-software-requirements.md)
- [DOC-101 PRD](../02-product/DOC-101-product-requirements.md)
- [00-mvp-decisions.md](../00-mvp-decisions.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-30 | Initial MVP traceability matrix |
