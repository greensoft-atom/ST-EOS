# DOC-306 — Security Architecture

**Document ID:** DOC-306  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Draft  
**Source:** [MOV-007](../07-movements/MOV-007-security-data-governance.md)

---

## 1. Security Design Principles

| # | Principle | Implementation |
|---|-----------|----------------|
| 1 | Defense in depth | Network + app + data layers |
| 2 | Least privilege | RBAC; DB user minimal grants |
| 3 | Local-first | No external LLM API in MVP |
| 4 | Fail secure | Deny access on auth error |
| 5 | Auditability | Append-only audit log |
| 6 | Classification-aware | Filter at retrieval, not after |

---

## 2. Security Architecture Diagram

```text
┌─────────────────────────────────────────────────────────────────┐
│                        TRUST BOUNDARY                            │
│  (Pilot institution network / VPN)                               │
│                                                                  │
│  ┌──────────────┐         TLS 1.2+         ┌─────────────────┐  │
│  │   Browser    │ ◀──────────────────────▶ │  Nginx (proxy)  │  │
│  └──────────────┘                            └────────┬────────┘  │
│                                                       │           │
│                              ┌────────────────────────▼────────┐  │
│                              │  FastAPI Application           │  │
│                              │  ┌──────────┐ ┌─────────────┐ │  │
│                              │  │ JWT Auth │ │ RBAC Guard  │ │  │
│                              │  └────┬─────┘ └──────┬──────┘ │  │
│                              │       └──────┬───────┘        │  │
│                              │              ▼                │  │
│                              │  ┌───────────────────────┐   │  │
│                              │  │ Services + AI Orch.   │   │  │
│                              │  │ (access filter inject)│   │  │
│                              │  └───────────┬───────────┘   │  │
│                              └──────────────┼───────────────┘  │
│                                             │                   │
│         ┌───────────────────────────────────┼───────────────┐  │
│         ▼                   ▼               ▼               ▼  │
│  ┌────────────┐    ┌────────────┐   ┌──────────┐   ┌──────────┐│
│  │ PostgreSQL │    │ pgvector   │   │  Redis   │   │  Ollama  ││
│  │ (encrypted)│    │ (internal) │   │ (internal)│  │ localhost││
│  └────────────┘    └────────────┘   └──────────┘   └──────────┘│
│         ▲                                                        │
│  ┌──────┴───────┐                                                │
│  │ File store   │  /data/documents (permissions 750)             │
│  └──────────────┘                                                │
└─────────────────────────────────────────────────────────────────┘
         ▲
         │ NO outbound LLM API (MVP)
         ✕ Internet (blocked except updates patch window)
```

---

## 3. Authentication

| Aspect | MVP | Phase 2 |
|--------|-----|---------|
| Method | Username + password | + LDAP/SSO |
| Password hash | bcrypt, cost 12 | Same |
| Session | JWT access 15 min + refresh 7d | Same |
| Lockout | 5 failed attempts / 15 min | Same |
| MFA | Not MVP | Optional Phase 2 |

---

## 4. Authorization (RBAC)

See MOV-007 Section 7. Enforcement points:

```text
HTTP Request
     │
     ▼
┌─────────────┐
│ JWT valid?  │──No──▶ 401
└──────┬──────┘
       │ Yes
       ▼
┌─────────────┐
│ Permission? │──No──▶ 403
└──────┬──────┘
       │ Yes
       ▼
┌─────────────┐
│ Resource ACL│──No──▶ 403 + AUD-014
└──────┬──────┘
       │ Yes
       ▼
   Handler
```

---

## 5. Data Protection

| Data state | Control |
|------------|---------|
| At rest | Disk encryption (LUKS); DB on encrypted volume |
| In transit | TLS 1.2+ |
| Secrets | Environment variables; never in git |
| Backups | Encrypted; off-server copy |
| PII | Minimize in logs; hash queries in audit |

---

## 6. AI-Specific Security

| Threat | Control |
|--------|---------|
| Prompt injection | System prompt hardening; no tool exec from user text |
| Data exfil via prompt | No external API; output filtered to user scope |
| Cross-user leakage | Retrieval pre-filter mandatory |
| Hallucination as policy | Disclaimer + human approval for official docs |
| Model tampering | Local model files integrity check on deploy |

---

## 7. Vulnerability Management

| Activity | Frequency |
|----------|-----------|
| Dependency scan (pip/npm audit) | Weekly CI |
| OWASP ZAP baseline | Sprint 3, 6 |
| OS patches | Monthly maintenance window |
| Pen test (optional) | Before national deploy |

---

## Related Documents

- [MOV-007](../07-movements/MOV-007-security-data-governance.md)
- [DOC-602 Data Classification](../07-data/DOC-602-data-classification.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial security architecture |
