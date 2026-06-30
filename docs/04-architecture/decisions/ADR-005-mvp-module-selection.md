# ADR-005 — MVP Department Module Selection

**Status:** Accepted  
**Date:** 2026-06-30  
**Deciders:** Executive Sponsor (MSTI), Program Manager, Pilot Champion

---

## Context

MVP allows **one** department assistant after platform wedge (repository, RAG, review, create). Candidates: **Research Assistant** vs **Evaluation Assistant**.

Pilot anchor: **MSTI** — Research Programs and Grant Administration as primary department.

---

## Decision

**Evaluation Assistant** is the sole MVP department module (Sprint 5–6).

**Research Assistant** deferred to **Phase 2B** (weeks 39–46) unless Gate G3 report recommends otherwise.

---

## Rationale

| Factor | Evaluation | Research |
|--------|------------|----------|
| Primary department fit | Direct (W1, W2) | Secondary |
| Executive visibility | High (grants, exhibitions) | Medium |
| Uses shared MVP utilities | Review + rubric + export | Literature + proposals |
| Risk profile | Human approval gate designed | Broader open-ended generation |
| Corpus alignment | Layer 2 + 4 + rubrics | Layer 1 heavy |

---

## Consequences

- All Sprint 5–6 stories use **Track B** only ([DOC-702](../../06-development/DOC-702-sprint-plan.md))
- URS-050–054 (Research) excluded from MVP acceptance ([DOC-205](../../03-requirements/DOC-205-traceability-matrix.md))
- MOV-006 includes **Flow 3: Evaluation** wireframes
- Phase 2B default second module: **Planning Assistant** or **Patent Assistant** — not Evaluation ([MOV-011](../../07-movements/MOV-011-iterate-expand-phase2.md))

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-30 | Initial ADR — locks Evaluation MVP |
