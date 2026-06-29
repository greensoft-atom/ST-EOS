# DOC-602 — Data Classification Policy

**Document ID:** DOC-602  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Draft for pilot approval  
**Owner:** Data Lead + Program Manager

---

## 1. Policy Statement

All documents ingested into ST-EOS **must** be assigned a classification level at upload. Classification determines storage handling, retrieval visibility, export rules, and AI processing boundaries.

---

## 2. Classification Levels

```text
Level 4 ─ CONFIDENTIAL   (highest sensitivity)
Level 3 ─ RESTRICTED
Level 2 ─ INTERNAL
Level 1 ─ PUBLIC         (lowest sensitivity)
```

| Level | Code | Definition | Example |
|-------|------|------------|---------|
| PUBLIC | PUB | Approved for public release | Published paper |
| INTERNAL | INT | Staff-only operational use | Internal report |
| RESTRICTED | RST | Limited role/group access | Grant under review |
| CONFIDENTIAL | CNF | Named individuals only | Unpublished patent |

---

## 3. Default Classification by Type

| Type | Default | Curator may downgrade | Curator may upgrade |
|------|---------|----------------------|---------------------|
| THS, ART | INT | To PUB if published | To RST |
| RPT | INT | To PUB | To RST |
| EXH, AWD | RST | To INT | To CNF |
| PAT (draft) | CNF | Never | — |
| POL, SOP | INT | To PUB if public law | To RST |
| Evaluation submission | RST | Never | To CNF |
| TPL | INT | — | — |

---

## 4. Handling Requirements

| Level | Upload | Search/RAG | Export | Backup |
|-------|--------|------------|--------|--------|
| PUB | Any user | All authenticated | Open | Standard |
| INT | Any user | All authenticated | Logged | Standard |
| RST | Reviewer+ | Role filter | Logged | Standard |
| CNF | Admin/Curator | Named ACL | Approval | Encrypted optional |

---

## 5. Responsibilities

| Role | Duty |
|------|------|
| Uploader | Select correct class; escalate if unsure |
| Curator | Review queue; correct misclassified |
| Admin | Audit classification changes |
| AI system | Enforce filter; never bypass |

---

## 6. Violations

Misclassification discovered → curator notified → reclassify → re-index → incident logged if RST/CNF exposure suspected.

---

## Related Documents

- [MOV-007](../07-movements/MOV-007-security-data-governance.md)
- [DOC-404 Knowledge Base](../05-ai/DOC-404-knowledge-base-design.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial policy |
