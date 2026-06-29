# DOC-710 — Resource, Budget & Infrastructure Plan

**Document ID:** DOC-710  
**Version:** 1.0  
**Date:** 2026-06-29  
**Horizon:** Phase 0 through Phase 2 (18 months)  
**Status:** Draft — update with local salary and currency

---

## 1. Purpose

Consolidate **human, hardware, software, and knowledge resources** with **indicative costs and risks** for ST-EOS program planning and sponsor approval.

**Note:** Personnel costs vary significantly by region. Tables provide **low/high ranges** using blended contractor-equivalent rates. Replace with your organization's actual figures.

---

## 2. Program Timeline & Resource Phases

```text
Month:  1    2    3    4    5    6    7    8    9   10   11   12   13   14   15   16   17   18
        ├──── Phase 0 ────┤├──── Phase 1 MVP ────┤├── Pilot ──┤├──── Phase 2 ────────────────►
        M0–M5            M8–M9                  M10         M11
        Discovery        Build                  Measure     Expand
```

| Phase | Weeks | Movements | Primary spend |
|-------|-------|-----------|---------------|
| Phase 0 | 1–8 | MOV-000–008 | People 60%, HW 20%, SW 5% |
| Phase 1 | 9–22 | MOV-009 | People 75%, HW 15% |
| Pilot | 23–30 | MOV-010 | People 50%, support 30% |
| Phase 2 | 31–56 | MOV-011 | People 80%, HW 10% |

---

## 3. Human Resources — Full Program

### 3.1 Team composition by phase

| Role | Ph0 | Ph1 | Pilot | Ph2 | Skills required |
|------|-----|-----|-------|-----|-----------------|
| Executive Sponsor | 0.05 | 0.05 | 0.1 | 0.05 | Decision authority |
| Program Manager | 0.6 | 0.6 | 0.8 | 0.8 | Agile, stakeholder mgmt |
| Tech Lead / Backend | 0.5 | 1.0 | 0.4 | 1.0 | FastAPI, PostgreSQL, security |
| AI/RAG Engineer | 0.5 | 1.0 | 0.3 | 1.0–1.5 | RAG, prompts, embeddings |
| Frontend Developer | 0.2 | 1.0 | 0.2 | 1.0 | React, TypeScript |
| UX Designer | 0.5 | 0.1 | 0 | 0.1 | Figma, task UX |
| Data Engineer / Curator | 0.5 | 0.5 | 0.5 | 0.75 | Metadata, OCR, taxonomy |
| QA Engineer | 0 | 0.5 | 0.2 | 0.75 | Test automation, AI eval |
| DevOps | 0.3 | 0.25 | 0.3 | 0.5 | Docker, CI, Linux |
| Trainer / CS | 0 | 0 | 0.5 | 0.25 | Documentation, training |
| **Total FTE** | **~3.1** | **~4.95** | **~3.2** | **~6.5–7.5** | |

### 3.2 Person-weeks summary

| Phase | Duration | Avg FTE | Person-weeks |
|-------|----------|---------|--------------|
| Phase 0 | 8 weeks | 3.1 | 24.8 |
| Phase 1 | 14 weeks | 4.95 | 69.3 |
| Pilot | 8 weeks | 3.2 | 25.6 |
| Phase 2 | 26 weeks | 7.0 | 182.0 |
| **Total** | **56 weeks** | | **~301.7** |

### 3.3 Hiring sequence

```text
Week 1:  PM + Tech Lead (mandatory)
Week 2:  AI/RAG Engineer
Week 3:  Data Curator (part-time OK)
Week 5:  UX (contract, 2 weeks)
Week 8:  Frontend + QA (before Sprint 0)
Week 31: Backend #2 or DevOps (Phase 2)
```

---

## 4. Hardware Resources

### 4.1 Environment matrix

| Environment | When | CPU | RAM | GPU | Storage | Est. cost (USD) |
|-------------|------|-----|-----|-----|---------|-----------------|
| Dev workstation × 4 | W1+ | 4c | 16 GB | — | 512 GB | $4,000 (or existing) |
| PoC server | W5–7 | 8c | 32 GB | opt | 500 GB | $1,500–$3,000 |
| Staging | W8+ | 16c | 64 GB | 12 GB | 1 TB | $3,000–$8,000 |
| Pilot production | W23+ | 16c | 64–128 GB | 24 GB | 2 TB | $4,000–$12,000 |
| Backup NAS | W23+ | — | — | — | 2 TB | $500–$1,500 |
| Phase 2 scale | W31+ | +cores | 128 GB | 2× GPU opt | +2 TB | $3,000–$15,000 |

### 4.2 LLM hardware guidance

| Model tier | VRAM | Example models | Use case |
|------------|------|----------------|----------|
| Small | 8 GB | Qwen2.5-7B, Llama-3.2-8B | Dev, CPU fallback |
| Medium | 16 GB | Qwen2.5-14B | Pilot default |
| Large | 24 GB+ | Qwen2.5-32B, Llama-3.1-70B (quant) | Production quality |

```text
Hardware Decision Tree
──────────────────────
Budget tight? ──▶ CPU + 7B model (slow but works)
Pilot quality? ──▶ 1× 24GB GPU + 14B model
100+ users?    ──▶ 128GB RAM + 2× GPU or vLLM batching
```

### 4.3 Hardware cost summary (one-time)

| Item | Low | High |
|------|-----|------|
| Phase 0–1 infrastructure | $5,000 | $15,000 |
| Pilot production (if new) | $4,000 | $12,000 |
| Phase 2 upgrades | $3,000 | $15,000 |
| **Total hardware** | **$12,000** | **$42,000** |

---

## 5. Software Resources

### 5.1 Stack inventory (all open-source core)

| Layer | Component | License | Cost |
|-------|-----------|---------|------|
| LLM runtime | Ollama / vLLM | Apache/MIT | $0 |
| Backend | FastAPI, Python | MIT | $0 |
| Frontend | React, Vite | MIT | $0 |
| Database | PostgreSQL 16 | PostgreSQL | $0 |
| Vector | pgvector / Qdrant | OSS | $0 |
| Queue | Redis, RQ | BSD | $0 |
| OCR | PyMuPDF, Tesseract | OSS | $0 |
| Embeddings | bge-m3 (local) | MIT | $0 |
| CI/CD | GitHub Actions | Free tier | $0 |
| Monitoring | Prometheus, Grafana | OSS | $0 |

### 5.2 Optional paid tools

| Tool | Purpose | Annual cost |
|------|---------|-------------|
| GitHub Team | Private repos, CI | $0–$600 |
| Figma Professional | UX | $0–$720 |
| Linear/Jira | Project mgmt | $0–$1,200 |
| Sentry | Error tracking | $0–$500 |
| **Optional total** | | **$0–$3,020/yr** |

---

## 6. Knowledge Resources

| Asset | Phase | Effort | Owner |
|-------|-------|--------|-------|
| Document corpus (10K MVP) | Ph0–1 | 200 curator hours | Data lead |
| Templates (5–10) | Ph0–1 | 40 hours | Domain expert |
| RAG eval set (50 Q) | Ph0 | 24 hours | AI + curator |
| Review test set (20 docs) | Ph1 | 16 hours | QA |
| Rubrics / policy docs | Ph0–1 | 40 hours | Pilot dept |
| Training materials | Pilot | 40 hours | PM |
| Patent corpus (Phase 2) | Ph2 | 400 hours | IP unit |

**Knowledge cost (internal time):** ~400–800 hours domain + curator effort over 18 months.

---

## 7. Budget Summary (Cash — Indicative USD)

### 7.1 By phase

| Phase | Personnel (contractor equiv.) | Hardware | Software | Other | Total low | Total high |
|-------|------------------------------|----------|----------|-------|-----------|------------|
| Phase 0 (8 wk) | $25,000 | $3,000 | $200 | $2,000 | **$30,200** | **$55,000** |
| Phase 1 (14 wk) | $85,000 | $8,000 | $300 | $3,000 | **$96,300** | **$180,000** |
| Pilot (8 wk) | $15,000 | $0–8,000 | $0 | $3,000 | **$18,000** | **$42,000** |
| Phase 2 (26 wk) | $150,000 | $5,000 | $500 | $10,000 | **$165,500** | **$450,000** |
| **Program total** | **$275,000** | **$16,000** | **$1,000** | **$18,000** | **$310,000** | **$727,000** |

*Personnel assumes blended $80–150/hour contractor equivalent. Internal staff = opportunity cost only.*

### 7.2 Cost breakdown pie (Phase 1 example)

```text
Phase 1 Budget (~$100K–180K typical)
────────────────────────────────────
Personnel     ████████████████████████████  75%
Hardware      ██████                        15%
Travel/training ██                          5%
Software      █                             2%
Contingency   ██                            3%
```

### 7.3 Minimum viable budget (bootstrap)

If team is **fully internal** and hardware exists:

| Item | Minimum cash |
|------|--------------|
| UX contract (2 weeks) | $2,000 |
| Extra storage | $500 |
| Training / travel | $1,000 |
| Contingency | $2,000 |
| **Bootstrap minimum** | **~$5,500** |

---

## 8. Rate assumptions (adjust for your region)

| Role | Low ($/hr) | Mid ($/hr) | High ($/hr) |
|------|------------|------------|-------------|
| PM | $50 | $80 | $120 |
| Tech Lead | $60 | $100 | $150 |
| AI Engineer | $60 | $110 | $160 |
| Frontend | $45 | $80 | $130 |
| Data Curator | $35 | $60 | $90 |
| QA | $40 | $70 | $100 |

---

## 9. Risk Register (Resource & Budget)

| ID | Risk | Impact | Mitigation | Budget reserve |
|----|------|--------|------------|----------------|
| RB1 | GPU unavailable | High | CPU fallback; cloud burst forbidden | +$3K GPU |
| RB2 | Team under-resourced | High | Delay Phase 1; don't start with 2 devs | Timeline |
| RB3 | Corpus curation slower | Medium | Hire temp curator 3 months | +$15K |
| RB4 | Pilot requires SSO | Medium | DevOps +0.5 FTE Sprint 7 | +$10K |
| RB5 | Currency / inflation | Low | Fixed-price HW early | — |
| RB6 | Scope creep | High | Change control; PM enforcement | Contingency |
| RB7 | Hardware failure | Medium | UPS + backup server | +$2K |

**Recommended contingency:** 15% of cash budget per phase.

---

## 10. Approval Thresholds

| Spend | Approver |
|-------|----------|
| < $1,000 | Tech Lead |
| $1,000–$10,000 | Program Manager |
| $10,000–$50,000 | Executive Sponsor |
| > $50,000 | Sponsor + finance |

---

## 11. Resource Loading Chart (FTE by month)

```text
FTE
7 │                              ████████ Phase 2
6 │                              ████████
5 │                    ██████████
4 │                    ██████████
3 │          ████████████████████
2 │    ██████████████████████████
1 │██████████████████████████████
  └──────────────────────────────────▶ Month
    1  2  3  4  5  6  7  8  9 10 11 12 ...
```

---

## Related Documents

- [MOV-008 Sprint 0](../07-movements/MOV-008-mvp-build-sprint0.md)
- [MOV-009 Build MVP](../07-movements/MOV-009-build-mvp-phase1.md)
- [DOC-001 Project Charter](../01-business/DOC-001-project-charter.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial resource & budget plan |
