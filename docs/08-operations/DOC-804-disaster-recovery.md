# DOC-804 — Disaster Recovery Plan (Pilot)

**Document ID:** DOC-804  
**Version:** 1.0  
**Date:** 2026-06-29  
**RTO:** 4 hours | **RPO:** 24 hours

---

## 1. Scope

Covers ST-EOS pilot single-server deployment: application, database, document store, configuration.

---

## 2. Backup Strategy

```text
Daily 02:00 local time
──────────────────────
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  pg_dump    │     │  rsync docs │     │  copy .env  │
│  → backup/  │     │  → backup/  │     │  → backup/  │
└─────────────┘     └─────────────┘     └─────────────┘
                           │
                           ▼
                    Verify checksum
                           │
                           ▼
                    Log AUD-015
```

| Asset | Method | Retention |
|-------|--------|-----------|
| PostgreSQL | pg_dump custom format | 30 days |
| Documents | rsync incremental | 30 days |
| Config/.env | encrypted copy | 30 days |
| Vector index | pg_dump + **optional pgvector snapshot** | 30 days |

---

## 3. Restore Procedure

| Step | Action | Time est. |
|------|--------|-----------|
| 1 | Stop application | 2 min |
| 2 | Restore PostgreSQL | 15–60 min |
| 3 | Restore document files | 15–120 min |
| 4 | Restore .env | 2 min |
| 5 | Start stack | 5 min |
| 6 | Re-run failed ingest jobs if needed | Variable |
| 7 | **Or** restore pgvector snapshot if available | 15–60 min |
| 8 | Smoke test | 15 min |

**Note:** Full re-embed of 10,000+ documents may exceed 4-hour RTO. Mitigation: weekly pgvector table snapshot (`pg_dump` includes embeddings) or accept **degraded mode** (review/create up; search down) until re-index completes. See [00-mvp-decisions.md](../00-mvp-decisions.md).

---

## 4. DR Test Schedule

| Test | When | Owner |
|------|------|-------|
| Restore drill #1 | MOV-007 D9 | DevOps |
| Restore drill #2 | Sprint 6 | DevOps |
| Full DR simulation | Before national scale | DevOps + PM |

---

## Related Documents

- [MOV-007](../07-movements/MOV-007-security-data-governance.md)
- [DOC-801 Deployment Guide](./DOC-801-deployment-guide.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial DR plan |
| 1.1 | 2026-06-30 | Vector snapshot; realistic RTO note |
