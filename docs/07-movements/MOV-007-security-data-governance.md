# MOV-007 — Security & Data Governance Baseline

**Movement ID:** MOV-007  
**Phase:** Phase 0 (Discovery)  
**Timeline:** Weeks 7–8  
**Duration:** 10 working days  
**Owner:** Tech Lead + Program Manager  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Ready for execution

---

## 1. Purpose

Establish the **minimum security and data governance baseline** required before MVP build and pilot deployment. ST-EOS handles institutional S&T documents — many restricted or confidential. This movement produces policies, controls, and implementation requirements that engineering must build into Sprint 0–6.

**Honest scope:** This is a pilot-grade baseline, not full national certification. It must be sufficient for a government or university pilot to say "yes."

---

## 2. Movement Context

```text
Security & Governance Layer (where it sits)
──────────────────────────────────────────

     User Portal
          │
          ▼
┌─────────────────────┐
│ AuthN / AuthZ (RBAC)│  ← MOV-007 defines
└─────────┬───────────┘
          ▼
┌─────────────────────┐
│ Data Classification │  ← MOV-007 defines
│ Filter at retrieval │
└─────────┬───────────┘
          ▼
┌─────────────────────┐
│ Audit Log (append)  │  ← MOV-007 defines
└─────────┬───────────┘
          ▼
     AI + Knowledge Layer
```

| Depends on | Provides to |
|------------|-------------|
| MOV-002 Data audit (classification subsets) | MOV-008 Sprint 0 auth spec |
| MOV-004 Architecture | MOV-009 all sprints |
| MOV-006 Role matrix | Consistent RBAC |

---

## 3. Goals & Success Criteria

| Goal | Metric | Target |
|------|--------|--------|
| Data classified before ingestion | MVP corpus tagged | 100% |
| RBAC defined and implementable | Permission matrix | 4 roles, all endpoints |
| Audit spec complete | Events catalogued | ≥ 15 event types |
| AI usage policy approved | Sponsor sign-off | Written policy |
| DR baseline | Backup restore tested | 1 successful restore drill |
| Security checklist | Items passed | ≥ 90% for pilot |

---

## 4. Resources

### 4.1 Human resources

| Role | FTE | Days | Responsibilities |
|------|-----|------|------------------|
| Tech Lead | 0.5 | 8 | RBAC design, encryption, audit spec |
| Program Manager | 0.3 | 5 | Policies, sponsor alignment |
| Data Lead / Curator | 0.3 | 4 | Classification tagging rules |
| Pilot IT contact | 0.2 | 3 | SSO requirements, network policy |
| Legal / compliance advisor | 0.1 | 2 | Data rights, AI disclaimer (if available) |

### 4.2 Software & infrastructure (policy applies to)

| Component | Security control |
|-----------|------------------|
| PostgreSQL | Encrypted volume, least-privilege DB user |
| Vector DB | Same host/VLAN, no public port |
| Object storage | Filesystem permissions or MinIO bucket policy |
| LLM runtime | Localhost/bind internal IP only |
| Docker | Non-root containers where possible |
| Nginx/reverse proxy | TLS termination, rate limiting |

### 4.3 Knowledge inputs

| Document | Use |
|----------|-----|
| MOV-002 restricted doc inventory | Classification rules |
| DOC-404 Knowledge Base Design | Access classes |
| Pilot institution IT policy | Alignment checklist |

---

## 5. Cost Estimate (MOV-007 only)

| Item | Low | High | Notes |
|------|-----|------|-------|
| Legal/compliance review (external) | $0 | $3,000 | If in-house, $0 |
| TLS certificate (internal CA) | $0 | $500 | Often free with org CA |
| Backup storage (1 TB) | $50 | $200 | NAS or cloud backup |
| Security scan tool (optional) | $0 | $1,000 | OWASP ZAP free; Burp pro optional |
| **Total incremental** | **$50** | **$4,700** | |

---

## 6. Data Classification Framework

### 6.1 Classification levels

```text
Classification Hierarchy
────────────────────────
PUBLIC          → publishable research, open reports
    │
INTERNAL        → staff-only operational documents
    │
RESTRICTED      → evaluation submissions, draft patents
    │
CONFIDENTIAL    → named individuals only; legal privilege
```

### 6.2 Classification matrix by document type

| Type code | Default class | Override allowed | Example |
|-----------|---------------|------------------|---------|
| THS, ART, RPT | Internal | Yes | Published thesis → Public |
| EXH, AWD | Restricted | Yes | Public award summary → Internal |
| PAT (unpublished) | Confidential | No | Patent draft |
| POL, SOP, FRM | Internal | Yes | Public regulation → Public |
| Evaluation submission | Restricted | No | Grant proposal under review |
| TPL | Internal | Yes | — |

### 6.3 Handling rules

| Class | Storage | Retrieval filter | Export | AI training |
|-------|---------|------------------|--------|-------------|
| Public | Standard | All roles | Allowed | Allowed (future) |
| Internal | Encrypted volume | Authenticated users | Allowed | Not in MVP |
| Restricted | Encrypted + ACL | Reviewer+ or explicit grant | Logged | Never |
| Confidential | Separate bucket optional | Named users only | Approval required | Never |

---

## 7. Role-Based Access Control (RBAC)

### 7.1 Role definitions

```text
┌──────────┐     manages      ┌──────────┐
│  Admin   │ ───────────────▶ │  Users   │
└────┬─────┘                  └──────────┘
     │ configures
     ▼
┌──────────┐     curates      ┌──────────┐
│ Curator  │ ───────────────▶ │ Corpus   │
└────┬─────┘                  └──────────┘
     │
     ▼
┌──────────┐     reviews      ┌──────────┐
│ Reviewer │ ───────────────▶ │ Submissions│
└────┬─────┘                  └──────────┘
     │
     ▼
┌──────────┐     uses         ┌──────────┐
│  User    │ ───────────────▶ │ AI tools │
└──────────┘                  └──────────┘
```

### 7.2 Permission matrix (API-level)

| Permission | Admin | Curator | Reviewer | User |
|------------|-------|---------|----------|------|
| `documents:read:public` | ✓ | ✓ | ✓ | ✓ |
| `documents:read:internal` | ✓ | ✓ | ✓ | ✓ |
| `documents:read:restricted` | ✓ | ✓ | ✓ | · |
| `documents:read:confidential` | ✓ | ·* | ·* | · |
| `documents:write` | ✓ | ✓ | ✓ | ✓ |
| `documents:delete` | ✓ | ✓ | · | · |
| `metadata:edit` | ✓ | ✓ | · | · |
| `templates:manage` | ✓ | ✓ | · | · |
| `ai:query` | ✓ | ✓ | ✓ | ✓ |
| `ai:review` | ✓ | ✓ | ✓ | ✓ |
| `ai:evaluate:approve` | ✓ | · | ✓ | · |
| `users:manage` | ✓ | · | · | · |
| `audit:read` | ✓ | · | · | · |

### 7.3 Retrieval enforcement (critical)

```text
User query → Auth middleware → Build filter:
    access_class IN (user.allowed_classes)
    AND department IN (user.allowed_depts) [optional]
    → Vector search WITH metadata pre-filter
    → Never rely on post-filter alone
```

---

## 8. Audit Logging Specification

### 8.1 Events to log (mandatory)

| Event ID | Event | Fields logged |
|----------|-------|---------------|
| AUD-001 | User login | user_id, ip, success/fail, timestamp |
| AUD-002 | User logout | user_id, timestamp |
| AUD-003 | Document upload | user_id, doc_id, classification, hash |
| AUD-004 | Document delete | user_id, doc_id, timestamp |
| AUD-005 | Metadata change | user_id, doc_id, field, old, new |
| AUD-006 | AI search query | user_id, query_hash, chunk_ids[], model |
| AUD-007 | AI review run | user_id, doc_id, review_type, finding_count |
| AUD-008 | AI generation | user_id, template_id, chunk_ids[], model |
| AUD-009 | Export document | user_id, artifact_id, format |
| AUD-010 | Evaluation score | user_id, submission_id, rubric_id, scores |
| AUD-011 | Admin user change | admin_id, target_user, action |
| AUD-012 | Failed auth (×5) | ip, username, lockout triggered |
| AUD-013 | Classification change | user_id, doc_id, old, new |
| AUD-014 | Restricted access denied | user_id, doc_id, reason |
| AUD-015 | Backup completed | job_id, size, status |
| AUD-016 | AI usage policy acknowledged | user_id, timestamp, policy_version |

### 8.2 Audit architecture

```text
Application ──▶ Audit Service ──▶ audit_log table (append-only)
                      │
                      └──▶ No UPDATE/DELETE on audit rows
                           Retention: ≥ 12 months (pilot)
                           Export: CSV for compliance review
```

### 8.3 What NOT to log (privacy)

- Full document body in audit (log IDs only)
- Full LLM prompts containing PII in plain text (log hash + reference ID)
- Passwords or tokens

---

## 9. Encryption & Network Security

| Layer | Requirement | MVP implementation |
|-------|-------------|-------------------|
| Transit | TLS 1.2+ | Nginx cert on pilot server |
| Rest | AES-256 | LUKS/disk encryption on server |
| Secrets | Not in git | `.env` + Docker secrets |
| LLM API | Internal only | Bind 127.0.0.1 or private VLAN |
| DB | No public port | Docker internal network |
| Backups | Encrypted | gpg or encrypted volume |

### Network diagram (pilot)

```text
                    Internet (optional, VPN only)
                              │
                         [ Firewall ]
                              │
              ┌───────────────┴───────────────┐
              │     Pilot Institution LAN      │
              │  ┌─────────────────────────┐  │
              │  │   ST-EOS Server         │  │
              │  │   :443 → Nginx          │  │
              │  │   :5432 internal only   │  │
              │  │   LLM localhost:11434   │  │
              │  └─────────────────────────┘  │
              │         ▲                      │
              │    Staff browsers (VPN)        │
              └───────────────────────────────┘
```

---

## 10. AI Usage Policy (Pilot)

### 10.1 Policy statements (require sponsor approval)

1. ST-EOS AI outputs are **advisory** — not official decisions or legal opinions.
2. **Human review required** before evaluation scores or official documents are issued.
3. Users must **verify citations** before relying on factual claims.
4. **Confidential documents** must not be uploaded without classification and approval.
5. Users must **not prompt** the system to bypass access controls.
6. Known limitations (hallucination, incomplete corpus) must be communicated in training.

### 10.2 UI enforcement

| Control | Implementation |
|---------|----------------|
| Disclaimer banner | Every AI output screen |
| Evaluation export block | Requires reviewer "Approve" click |
| Low-confidence warning | When retrieval score < threshold |
| Source count minimum | Warn if < 2 sources retrieved |

---

## 11. Backup & Disaster Recovery (Pilot baseline)

| Item | Policy |
|------|--------|
| Backup frequency | Daily automated |
| Backup contents | PostgreSQL dump + document store + config |
| Retention | 30 days rolling |
| Restore RTO | ≤ 4 hours (pilot) |
| Restore RPO | ≤ 24 hours |
| Test | 1 restore drill before pilot go-live |

```text
Backup flow:
  cron 02:00 → pg_dump → /backup/db/
            → rsync documents → /backup/files/
            → verify checksum → log AUD-015
```

---

## 12. Day-by-Day Schedule

| Day | Activity | Output |
|-----|----------|--------|
| D1 | Classification workshop with data lead | Classification v1 |
| D2 | RBAC matrix + API permission map | RBAC spec |
| D3 | Audit event catalog + schema | Audit spec |
| D4 | Encryption & network checklist | Infra checklist |
| D5 | AI usage policy draft | Policy doc |
| D6 | Backup/DR procedure | DR runbook |
| D7 | Pilot IT alignment call | Gap list |
| D8 | Security architecture update (DOC-306) | Architecture doc |
| D9 | Restore drill on dev environment | Drill report |
| D10 | Sponsor sign-off pack | Approved baseline |

---

## 13. Security Checklist (Pilot Go-Live)

| # | Check | Owner | Sprint |
|---|-------|-------|--------|
| 1 | TLS enabled on all user endpoints | DevOps | S0 |
| 2 | Default passwords changed | Admin | S0 |
| 3 | RBAC enforced on all API routes | Backend | S1 |
| 4 | Classification required on upload | Backend | S1 |
| 5 | Retrieval pre-filter by access class | AI/RAG | S2 |
| 6 | Audit events AUD-001–010 implemented | Backend | S2–S3 |
| 7 | AUD-016 policy acknowledgment | Backend | S3 |
| 8 | AI disclaimer on all output screens | Frontend | S3 |
| 8 | Export actions logged | Backend | S4 |
| 9 | Backup job scheduled | DevOps | S6 |
| 10 | Restore drill passed | DevOps | S6 |
| 11 | OWASP ZAP scan — no critical findings | QA | S6 |
| 12 | AI usage policy acknowledged by users | PM | Pilot |

---

## 14. Risks & Mitigations

| ID | Risk | L | I | Mitigation |
|----|------|---|---|------------|
| R1 | Pilot requires SSO immediately | M | H | Phase SSO to Sprint 7 or parallel if contract requires |
| R2 | Confidential docs uploaded without tag | H | H | Mandatory classification on upload; default Internal |
| R3 | Audit log not implemented early | M | H | Sprint 2 requirement, not Sprint 6 |
| R4 | Retrieval leak across classes | L | C | Integration tests per class; pen test sample |
| R5 | No legal review of AI policy | M | M | Use conservative disclaimer; human-in-loop |
| R6 | Backup untested | M | H | Mandatory drill in MOV-007 D9 and S6 |

---

## 15. Deliverables

| ID | Deliverable | Location |
|----|-------------|----------|
| D1 | Data Classification Policy | [DOC-602](../07-data/DOC-602-data-classification.md) |
| D2 | Security Architecture | [DOC-306](../04-architecture/DOC-306-security-architecture.md) |
| D3 | RBAC & permission spec | Section 7 of this doc + API spec |
| D4 | Audit logging spec | Section 8 of this doc |
| D5 | AI Usage Policy | `docs/09-enterprise/AI-USAGE-POLICY.md` |
| D6 | Backup & DR runbook | [DOC-804](../08-operations/DOC-804-disaster-recovery.md) |
| D7 | Security checklist | Section 13 |
| D8 | Sponsor approval | Signed PDF/email |

---

## 16. Exit Criteria

- [ ] Classification policy approved
- [ ] RBAC matrix matches MOV-006 UX matrix
- [ ] Audit schema in database migration plan (Sprint 0)
- [ ] AI usage policy signed by sponsor
- [ ] Backup restore drill successful
- [ ] No open **Critical** security gaps for pilot

---

## Related Documents

- [MOV-006 UX Workflow](./MOV-006-ux-workflow-design.md)
- [MOV-008 Sprint 0](./MOV-008-mvp-build-sprint0.md)
- [DOC-307 RBAC Specification](../04-architecture/DOC-307-rbac-specification.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial detailed movement doc |
