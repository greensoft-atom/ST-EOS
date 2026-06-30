# MOV-010 — Pilot Deployment & Measurement

**Movement ID:** MOV-010  
**Phase:** Pilot — Deployment & Measurement  
**Timeline:** Weeks 23–30 (8 weeks)  
**Owner:** Program Manager + Customer Success lead  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Ready for execution (after MOV-009)

---

## 1. Purpose

Deploy ST-EOS MVP to the **anchor pilot institution**, onboard real users, run **3 official workflows**, measure outcomes against Movement 1 success metrics, and produce a **Go/No-Go decision** for Phase 2 expansion (MOV-011).

This is where the platform proves business value — or reveals what must change.

---

## 2. Pilot Timeline

```text
Week:  23   24   25   26   27   28   29   30
       ├────├────├────├────├────├────├────┤
       Deploy Train  Workflow 1
            Champions  Workflow 2
                      Workflow 3
                           Measure ──▶ Gate G3
```

| Phase | Weeks | Focus |
|-------|-------|-------|
| Deploy & stabilize | 23–24 | Production-like install, smoke tests |
| Enablement | 24–25 | Training, champions, support channel |
| Active pilot | 25–28 | 3 official workflows on platform |
| Measurement | 29–30 | Survey, metrics, Go/No-Go report |

---

## 3. Resources

### 3.1 Human resources (8 weeks)

| Role | FTE | Responsibilities |
|------|-----|------------------|
| Program Manager | 0.8 | Pilot coordination, reporting, Gate G3 |
| Tech Lead | 0.4 | Deploy, hotfixes, performance |
| AI/RAG Engineer | 0.3 | Corpus tuning, prompt fixes |
| Frontend Developer | 0.2 | UI bugs, UX friction fixes |
| Data Curator | 0.5 | Corpus completion, metadata fixes |
| Customer success / trainer | 0.5 | Training, champion support |
| Pilot champion users | 10–20 | Active usage (part-time) |
| Pilot IT liaison | 0.2 | Network, VPN, access |

### 3.2 Hardware — pilot production environment

| Component | Spec | Notes |
|-----------|------|-------|
| Production server | 16+ cores, 64–128 GB RAM, 2 TB SSD | Same or better than staging |
| GPU | 24 GB VRAM recommended | Shared inference |
| Backup | Daily to separate device | Per MOV-007 |
| UPS (recommended) | 30 min minimum | Power protection |

### 3.3 Software

| Item | Action |
|------|--------|
| ST-EOS MVP release package | From MOV-009 S6 |
| Monitoring | Grafana + Prometheus or simple health dashboard |
| Support channel | Email + shared chat (Teams/Slack) |
| Feedback form | Google Form or in-app thumbs up/down |

---

## 4. Cost Estimate (MOV-010)

| Item | Low (USD) | High (USD) |
|------|-----------|------------|
| Pilot server (if new) | $0 | $8,000 | Often institution-provided |
| On-site deployment travel | $500 | $3,000 | |
| Training materials print/video | $200 | $1,000 | |
| Support team (8 weeks, partial FTE) | $8,000 | $25,000 | If contractors |
| Contingency hotfix buffer | $2,000 | $5,000 | |
| **Total** | **$10,700** | **$42,000** | |

---

## 5. Deployment Plan

### 5.1 Deployment architecture

```text
Pilot Institution
─────────────────
┌──────────────────────────────────────────────┐
│  Staff VLAN / VPN                             │
│  ┌────────────────────────────────────────┐  │
│  │  ST-EOS Production Server               │  │
│  │  ┌────────┐ ┌────────┐ ┌────────────┐  │  │
│  │  │ Nginx  │ │ Backend│ │ PostgreSQL │  │  │
│  │  │ :443   │ │ Workers│ │ + pgvector │  │  │
│  │  └────────┘ └────────┘ └────────────┘  │  │
│  │  ┌────────┐ ┌────────┐ ┌────────────┐  │  │
│  │  │Frontend│ │ Ollama │ │ Doc store  │  │  │
│  │  │ static │ │ /vLLM  │ │ /data      │  │  │
│  │  └────────┘ └────────┘ └────────────┘  │  │
│  └────────────────────────────────────────┘  │
│  Backup NAS ◀── daily rsync                  │
└──────────────────────────────────────────────┘
```

### 5.2 Deployment checklist

| # | Step | Owner | Day |
|---|------|-------|-----|
| 1 | Server provisioned & hardened | Pilot IT | W23-D1 |
| 2 | TLS cert installed | DevOps | W23-D1 |
| 3 | Docker Compose prod deploy | Tech lead | W23-D2 |
| 4 | Database migrate | Tech lead | W23-D2 |
| 5 | Bulk corpus ingest (10K docs) | Data lead | W23-D3–5 |
| 6 | Smoke test all P0 flows | QA | W23-D5 |
| 7 | Admin accounts created | PM | W23-D5 |
| 8 | Monitoring alerts configured | DevOps | W24-D1 |
| 9 | Backup job verified | DevOps | W24-D1 |
| 10 | Pilot go-live announcement | Sponsor | W24-D2 |

Full guide: [DOC-801 Deployment Guide](../08-operations/DOC-801-deployment-guide.md)

---

## 6. Training & Enablement

### 6.1 Champion user program

```text
Champion Model
──────────────
Sponsor selects 10–20 champions
        │
        ▼
2-hour training session (Week 24)
        │
        ├── Module 1: Search & citations (30 min)
        ├── Module 2: Document review (30 min)
        ├── Module 3: Document creation (30 min)
        └── Module 4: Assistant + Q&A (30 min)
        │
        ▼
Champions support peers + weekly feedback to PM
```

### 6.2 Training materials deliverables

| Material | Format | Owner |
|----------|--------|-------|
| Quick start guide (5 pages) | PDF | PM |
| Video: Search workflow | 5 min | PM + champion |
| Video: Review workflow | 5 min | PM + champion |
| FAQ document | MD/PDF | Support |
| AI usage policy acknowledgment | Form | Legal/PM |

---

## 7. Official Pilot Workflows (3 required)

Select at pilot kickoff based on MOV-001 choice:

### Option set — Government S&T Executive Office (default pilot)

| # | Workflow | AS-IS baseline | Success metric |
|---|----------|----------------|----------------|
| W1 | Grant/program submission pre-screening | 4–8 hrs manual checklist per proposal | ≤ 50% time reduction |
| W2 | Committee evaluation scoring (batch of ~20) | 3–5 days committee prep | ≤ 30% time reduction |
| W3 | Annual S&T plan / report section drafting | 2–5 days per section | ≤ 40% first-draft time reduction |

### Workflow execution template

```text
For each workflow:
  1. Record AS-IS time (baseline from MOV-001)
  2. Run ≥ 3 real cases on ST-EOS
  3. Record TO-BE time
  4. Collect user trust rating (1–5)
  5. Document issues / workarounds
  6. Write 1-page case study
```

---

## 8. Measurement Framework

### 8.1 Quantitative KPIs

| KPI ID | Metric | Baseline | Target | Measurement |
|--------|--------|----------|--------|-------------|
| KPI-01 | Active users (weekly) | 0 | ≥ 30 | Login analytics |
| KPI-02 | Documents indexed | — | ≥ 10,000 | System count |
| KPI-03 | AI queries per week | 0 | ≥ 100 | Audit log |
| KPI-04 | Reviews completed | 0 | ≥ 50 | Audit log |
| KPI-05 | Documents created | 0 | ≥ 20 | Audit log |
| KPI-06 | Avg search time | manual 30+ min | ≤ 5 min | User survey |
| KPI-07 | Review cycle time | baseline | −30% | Workflow W2 |
| KPI-08 | Citation click-through | — | ≥ 40% | UI analytics |
| KPI-09 | System uptime | — | ≥ 99% | Monitoring |
| KPI-10 | P1 bug count open | — | ≤ 5 | Issue tracker |

### 8.2 Qualitative measures

| Measure | Method | Target |
|---------|--------|--------|
| User trust in AI outputs | Survey (1–5) | ≥ 3.8 avg |
| Usefulness rating | Per-session thumbs | ≥ 80% positive |
| Would recommend | NPS-style | ≥ 30 |
| Champion satisfaction | Interview | 8/10 champions positive |

### 8.3 Survey schedule

| Week | Survey |
|------|--------|
| 25 | Baseline experience (pre-ST-EOS recall) |
| 27 | Mid-pilot pulse (5 questions) |
| 30 | Final survey + interviews (3 champions) |

---

## 9. Support Model (Pilot)

```text
Issue Severity → Response
─────────────────────────
Critical (system down)     → 4 hours   → Tech lead
High (feature blocked)     → 1 business day
Medium (workaround exists) → 3 business days
Low (cosmetic)             → Next sprint / Phase 2
```

| Channel | Hours |
|---------|-------|
| Email support | Business hours |
| Champion Slack/Teams | Business hours |
| Emergency phone | Critical only |

---

## 10. Pilot Report Structure (Week 30)

| Section | Content |
|---------|---------|
| 1. Executive summary | Go/No-Go recommendation |
| 2. Deployment summary | Environment, corpus, users |
| 3. KPI dashboard | All KPI-01–10 |
| 4. Workflow case studies | 3 × 1 page |
| 5. User feedback | Survey results, quotes |
| 6. Issues & resolutions | Bug list, open items |
| 7. Security incident log | Any breaches (target: zero) |
| 8. Phase 2 recommendation | Module priority |
| 9. Appendices | Audit samples, training attendance |

---

## 11. Gate G3 — Go/No-Go Criteria

### Go to MOV-011 (Phase 2) if:

| # | Criterion | Threshold |
|---|-----------|-----------|
| 1 | KPI-01 active users | ≥ 30 |
| 2 | KPI trust score | ≥ **3.5** (target **3.8** per [DOC-PILOT-001 §7](../01-business/DOC-PILOT-001-government-executive-pilot-scope.md)) |
| 3 | At least 2/3 workflows hit time target | ≥ 67% |
| 4 | No unresolved Critical bugs | 0 |
| 5 | Sponsor written approval | Yes |

### No-Go actions:

| Condition | Action |
|-----------|--------|
| RAG trust low | Corpus + prompt sprint before Phase 2 |
| Low adoption | UX friction study; more training |
| Performance issues | Hardware upgrade; optimize |
| Wrong assistant chosen | Swap module in Phase 2 |

---

## 12. Risks & Mitigations

| ID | Risk | L | I | Mitigation |
|----|------|---|---|------------|
| R1 | Pilot IT delays server | M | H | Pre-provision at W22 |
| R2 | Low user adoption | M | H | Champions; executive mandate |
| R3 | Corpus incomplete at deploy | M | M | Bulk ingest week W23 |
| R4 | Production incident | L | H | Backup; rollback plan |
| R5 | Negative publicity if AI error | L | H | Disclaimer; human approval |
| R6 | Metrics not collected | M | M | Audit log queries automated |

---

## 13. Day-by-Day (Weeks 23–24 detail)

| Day | Activity |
|-----|----------|
| W23-D1 | Server handoff; OS hardening |
| W23-D2 | Deploy application stack |
| W23-D3 | Start bulk ingestion |
| W23-D4 | Continue ingestion; fix failures |
| W23-D5 | Smoke tests; admin setup |
| W24-D1 | Backup + monitoring live |
| W24-D2 | Go-live; announce to org |
| W24-D3 | Training session #1 (champions) |
| W24-D4 | Training session #2 (if needed) |
| W24-D5 | Support channel active; first usage review |

---

## 14. Exit Criteria

- [ ] Production deployment stable ≥ 2 weeks
- [ ] 10–20 champions trained
- [ ] 3 workflows executed with case studies
- [ ] Final pilot report delivered
- [ ] Gate G3 decision documented
- [ ] Handoff package for MOV-011 if Go

---

## Related Documents

- [MOV-009 Build MVP](./MOV-009-build-mvp-phase1.md)
- [MOV-011 Iterate & Expand](./MOV-011-iterate-expand-phase2.md)
- [DOC-801 Deployment Guide](../08-operations/DOC-801-deployment-guide.md)
- User quick-start (Sprint 6 deliverable; full DOC-803 Phase 2)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial detailed movement doc |
