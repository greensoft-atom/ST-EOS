# DOC-801 — Deployment Guide

**Document ID:** DOC-801  
**Version:** 1.0  
**Date:** 2026-06-29  
**Audience:** DevOps, Tech Lead, Pilot IT  
**Status:** Draft

---

## 1. Deployment Overview

ST-EOS MVP deploys as **Docker Compose** stack on a single Linux server (Ubuntu 22.04 LTS recommended).

```text
Deployment Steps
────────────────
1. Provision server
2. Install Docker + Compose
3. Clone release package
4. Configure .env
5. docker compose -f docker-compose.prod.yml up -d
6. Run migrations
7. Seed admin user
8. Bulk ingest corpus
9. Smoke test
10. Enable backup cron
```

---

## 2. Server Requirements

| Resource | Minimum | Recommended |
|----------|---------|-------------|
| OS | Ubuntu 22.04 | Ubuntu 22.04 |
| CPU | 8 cores | 16 cores |
| RAM | 32 GB | 64–128 GB |
| Disk | 500 GB SSD | 2 TB NVMe |
| GPU | Optional | 24 GB VRAM |
| Network | 1 Gbps LAN | VPN access |

---

## 3. Directory Layout (Production)

```text
/opt/st-eos/
├── docker-compose.prod.yml
├── .env                    # secrets — chmod 600
├── data/
│   ├── documents/          # uploaded files
│   └── postgres/           # DB volume
├── backup/
├── logs/
└── releases/
    └── v0.9.0/
```

---

## 4. Environment Variables (essential)

| Variable | Example | Description |
|----------|---------|-------------|
| `DATABASE_URL` | postgresql://... | Postgres connection |
| `JWT_SECRET` | random 64 char | Auth signing |
| `LLM_BASE_URL` | http://ollama:11434 | LLM endpoint |
| `LLM_MODEL` | qwen2.5:14b | Default model |
| `STORAGE_PATH` | /data/documents | File store |
| `ADMIN_EMAIL` | admin@org.local | Seed admin |

---

## 5. Deploy Commands

```bash
# Pull release
cd /opt/st-eos/releases/v0.9.0

# Configure
cp .env.example .env
# edit .env with production values

# Start stack
docker compose -f docker-compose.prod.yml pull
docker compose -f docker-compose.prod.yml up -d

# Migrate
docker compose exec backend alembic upgrade head

# Seed admin (first run only)
docker compose exec backend python -m app.scripts.seed_admin

# Health check
curl -k https://localhost/api/health
```

---

## 6. Post-Deploy Checklist

| # | Check | Command / action |
|---|-------|------------------|
| 1 | All containers running | `docker compose ps` |
| 2 | Health OK | `GET /health` |
| 3 | LLM responding | `GET /health/llm` |
| 4 | Login works | UI test |
| 5 | Upload + index | UAT-01 |
| 6 | TLS valid | Browser padlock |
| 7 | Backup cron | `crontab -l` |

---

## 7. Rollback Procedure

```text
Rollback
────────
1. docker compose down
2. Restore DB from last backup
3. Restore /data/documents if needed
4. docker compose up previous release tag
5. Verify health
```

Target RTO: 4 hours.

---

## 8. Monitoring (MVP minimum)

| Check | Interval | Alert |
|-------|----------|-------|
| `/health` | 1 min | Email if 3 failures |
| Disk usage | 1 hr | > 85% |
| Container restart | Event | Immediate |
| Backup job | Daily | If missing |

---

## Related Documents

- [MOV-010 Pilot Deployment](../07-movements/MOV-010-pilot-deployment.md)
- [DOC-804 Disaster Recovery](../08-operations/DOC-804-disaster-recovery.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial deployment guide |
