# DOC-307 — RBAC Specification

**Document ID:** DOC-307  
**Version:** 1.0  
**Date:** 2026-06-30  
**Status:** Approved for Sprint 0 implementation  
**Supersedes:** 4-role matrices in DOC-101, MOV-006 §11, MOV-007 §7 (legacy)  
**Canonical:** [00-mvp-decisions.md §8](../00-mvp-decisions.md)

---

## 1. Purpose

Define roles, permissions, and enforcement points for ST-EOS MVP — including **Evaluation Assistant** workflow roles required by MSTI pilot.

---

## 2. Role Definitions

| Role | Code | Typical MSTI assignee | Description |
|------|------|---------------------|-------------|
| Administrator | `admin` | IT / system operator | Users, audit, system config |
| Curator | `curator` | Domain specialist | Metadata, templates, rubrics |
| Program Officer | `program_officer` | Grant administration staff | Upload submissions, pre-screen, run evaluations |
| Committee Reviewer | `committee_reviewer` | Evaluation committee member | Review and edit AI scores |
| Committee Chair | `committee_chair` | Committee head | Approve and export official packets |
| General User | `user` | Planning, innovation staff | Search, review, create (non-eval admin) |

### 2.1 Role inheritance (optional MVP simplification)

If MSTI prefers fewer named accounts at pilot start:

```text
committee_chair  ⊃  committee_reviewer  ⊃  program_officer  ⊃  user
curator          ⊃  user
admin            ⊃  all permissions
```

Implement as permission sets, not OS-level inheritance.

---

## 3. Permission Catalog

| Permission | Description |
|------------|-------------|
| `documents:read:{class}` | Read by classification (pub, int, rst, cnf) |
| `documents:write` | Upload documents |
| `documents:delete` | Soft-delete / archive |
| `metadata:edit` | Edit document metadata |
| `templates:manage` | CRUD document templates |
| `rubrics:manage` | CRUD evaluation rubrics |
| `ai:query` | RAG search |
| `ai:review` | Document review jobs |
| `ai:generate` | Template-based creation |
| `ai:evaluate` | Run evaluation / scoring |
| `ai:evaluate:edit` | Override criterion scores |
| `ai:evaluate:approve` | Approve evaluation for export |
| `evaluations:export` | Export committee packet |
| `users:manage` | User CRUD |
| `audit:read` | View audit log |

---

## 4. Role × Permission Matrix

| Permission | admin | curator | program_officer | committee_reviewer | committee_chair | user |
|------------|-------|---------|-----------------|-------------------|-----------------|------|
| `documents:read:public` | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| `documents:read:internal` | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| `documents:read:restricted` | ✓ | ✓ | ✓ | ✓ | ✓ | · |
| `documents:read:confidential` | ✓ | ·* | ·* | ·* | ·* | · |
| `documents:write` | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| `documents:delete` | ✓ | ✓ | · | · | · | · |
| `metadata:edit` | ✓ | ✓ | · | · | · | · |
| `templates:manage` | ✓ | ✓ | · | · | · | · |
| `rubrics:manage` | ✓ | ✓ | · | · | · | · |
| `ai:query` | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| `ai:review` | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| `ai:generate` | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| `ai:evaluate` | ✓ | ✓ | ✓ | ✓ | ✓ | · |
| `ai:evaluate:edit` | ✓ | · | · | ✓ | ✓ | · |
| `ai:evaluate:approve` | ✓ | · | · | · | ✓ | · |
| `evaluations:export` | ✓ | · | · | · | ✓ | · |
| `users:manage` | ✓ | · | · | · | · | · |
| `audit:read` | ✓ | · | · | · | · | · |

*Confidential access via explicit document ACL grant only.

---

## 5. Evaluation Workflow State Machine

```text
DRAFT ──(committee_reviewer edits)──▶ DRAFT
DRAFT ──(committee_chair approves)──▶ APPROVED
APPROVED ──(export)──▶ EXPORTED (audit AUD-009, AUD-010)
```

| Action | Required permission | Required status |
|--------|---------------------|-----------------|
| Run AI scoring | `ai:evaluate` | — |
| Edit scores | `ai:evaluate:edit` | draft |
| Approve | `ai:evaluate:approve` | draft |
| Export packet | `evaluations:export` | **approved** |

---

## 6. Retrieval Enforcement

Same as MOV-007 — pre-filter at vector query:

```python
# Pseudocode — enforce in RAG service
allowed_classes = user.allowed_document_classes()
filter = {"access_class": {"$in": allowed_classes}}
```

Integration tests required per role × classification ([DOC-706](../06-development/DOC-706-testing-strategy.md) SEC-01, SEC-02).

---

## 7. UI Screen Access (aligned with MOV-006)

| Screen group | Minimum role |
|--------------|--------------|
| SCR-S*, SCR-R* (search, review, create) | `user` |
| SCR-E01–E04 (evaluation wizard, scorecard) | `program_officer` |
| SCR-E07 (reviewer edit) | `committee_reviewer` |
| SCR-E08 (approval gate) | `committee_chair` |
| SCR-E09 (export) | `committee_chair` |
| SCR-E10 (rubric manager) | `curator` |
| Admin screens | `admin` |

---

## 8. Implementation Notes (Sprint 0)

- Store roles as enum + optional permission overrides in `user_roles` table
- JWT claims include `role` and `permissions[]` (or resolve server-side)
- Middleware: `@requires("ai:evaluate:approve")` on approve endpoint
- Seed accounts for UAT: one user per role ([DOC-706](../06-development/DOC-706-testing-strategy.md))

---

## Related Documents

- [MOV-007 Security](../07-movements/MOV-007-security-data-governance.md)
- [DOC-306 Security Architecture](./DOC-306-security-architecture.md)
- [DOC-504 Evaluation Assistant](../06-modules/DOC-504-evaluation-assistant.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-30 | Initial 6-role RBAC for Evaluation MVP |
