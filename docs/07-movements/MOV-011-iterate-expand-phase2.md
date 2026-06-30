# MOV-011 — Iterate & Expand (Phase 2 Entry)

**Movement ID:** MOV-011  
**Phase:** Phase 2 — Expansion  
**Timeline:** Months 8–14 (Weeks 31–56, ~26 weeks)  
**Owner:** Program Office (PM + Tech Lead)  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Planned (requires Gate G3 Go)

---

## 1. Purpose

After a successful pilot, **expand ST-EOS** with additional department modules, platform enhancements, and scaled corpus — while maintaining stability for the pilot institution and preparing for a second customer.

**Discipline:** Add **ONE major module per 8-week block**. Do not parallelize multiple assistants without team growth.

---

## 2. Phase 2 Strategy

```text
Gate G3: GO
    │
    ▼
┌─────────────────────────────────────────────────────────┐
│ Phase 2A (W31–38): Stabilize + Platform enhancements    │
│ Phase 2B (W39–46): Second department module             │
│ Phase 2C (W47–56): Third module OR multi-tenant prep    │
└─────────────────────────────────────────────────────────┘
    │
    ▼
Version 1.0 General Release (optional second customer)
```

---

## 3. Phase 2 Decision Matrix (what to build first)

Score each candidate 1–5 based on pilot feedback:

| Module | Pilot demand | Corpus ready | Revenue potential | Complexity | Recommended if… |
|--------|--------------|--------------|-------------------|------------|-----------------|
| Evaluation Assistant | — (in MVP) | ★★★ | ★★★★ | ★★★ | Already delivered |
| Research Assistant | — | ★★★★ | ★★★ | ★★★ | **Default Phase 2B** if planning not priority |
| Patent Assistant | ★★★ | ★★ | ★★★★★ | ★★★★★ | IP dept engaged |
| Planning Assistant | ★★★★ | ★★★ | ★★★★ | ★★★ | Executive planning pain |
| Innovation / Scouting | ★★★ | ★★★ | ★★★ | ★★★★ | Innovation dept lead |
| Reporting Assistant | ★★★★ | ★★★★ | ★★★ | ★★★ | Dashboard demand |

| Default recommendation after **Evaluation MVP** (MSTI): |
| 1. Phase 2B → **Planning Assistant** OR **Research Assistant** |
| 2. Phase 2C → **Patent Assistant** OR Innovation scouting |

---

## 4. Resources (Phase 2)

### 4.1 Team scaling

| Role | MVP (Phase 1) | Phase 2 | Change |
|------|---------------|---------|--------|
| Program Manager | 0.6 | 0.8 | +0.2 |
| Tech Lead | 1.0 | 1.0 | — |
| Backend | 0 | 0.5–1.0 | +hire |
| AI/RAG Engineer | 1.0 | 1.0–1.5 | +0.5 |
| Frontend | 1.0 | 1.0 | — |
| Data / Curator | 0.5 | 0.75 | +corpus scale |
| QA | 0.5 | 0.75 | +automation |
| DevOps | 0.25 | 0.5 | +SSO, monitoring |
| **Total FTE** | **~4.9** | **~6.5–7.5** | |

### 4.2 Hardware scaling

| Need | Action | Est. cost |
|------|--------|-----------|
| Larger corpus (50K+ docs) | +1 TB storage | $200–$500 |
| More concurrent users (100+) | RAM upgrade 128 GB | $500–$2,000 |
| Faster inference | Second GPU or larger model | $2,500–$8,000 |
| HA (optional) | Standby server | $4,000+ |

### 4.3 Phase 2 cost envelope (6 months)

| Category | Low (USD) | High (USD) |
|----------|-----------|------------|
| Team (6.5 FTE × 6 mo) | $120,000 | $350,000 |
| Hardware upgrades | $3,000 | $12,000 |
| Second pilot/customer onboarding | $5,000 | $20,000 |
| Contingency 15% | $19,200 | $57,300 |
| **Total** | **$147,200** | **$439,300** |

---

## 5. Phase 2A — Stabilize & Enhance (Weeks 31–38)

**Goal:** Fix pilot debt; add platform capabilities that unlock modules

### 5.1 Sprint 7–8 backlog (platform)

| Feature | Priority | Rationale |
|---------|----------|-----------|
| Hybrid search (BM25 + vector) | P0 | Improves retrieval at scale |
| Comparison tool (multi-doc) | P0 | Evaluation + planning need |
| SSO/LDAP integration | P0 if pilot requires | Enterprise adoption |
| Reviewer comment threads | P1 | Pilot feedback |
| Batch upload | P1 | Corpus scaling |
| In-app feedback (thumbs) | P1 | Quality loop |
| Performance: query cache | P1 | Latency |
| Parent-child chunking | P2 | Long doc quality |

```text
Hybrid Search Architecture (Phase 2A)
─────────────────────────────────────
         Query
           │
     ┌─────┴─────┐
     ▼           ▼
 Vector       Keyword
 search       (BM25)
     │           │
     └─────┬─────┘
           ▼
      Reranker
           ▼
      Top-N chunks
```

### 5.2 Corpus scaling (Phase 2A)

| Milestone | Document count |
|-----------|------------------|
| Pilot end | 10,000 |
| Phase 2A end | 25,000 |
| Phase 2C end | 50,000+ |

### 5.3 Phase 2A exit criteria

- [ ] Pilot P1 bugs resolved
- [ ] Hybrid search deployed; Recall@5 + 5%
- [ ] SSO live (if required)
- [ ] Corpus ≥ 25,000 docs

---

## 6. Phase 2B — Second Module (Weeks 39–46)

**MSTI MVP used Evaluation Assistant.** Phase 2B default options:

| Module | When to choose |
|--------|----------------|
| **Planning Assistant** | W3 plan drafting demand high in Gate G3 report |
| **Research Assistant** | Research Programs requests literature/proposal support |
| **Patent Assistant** | IP liaison engaged; corpus ≥ 2,000 patents |

### 6.1 Example: Planning Assistant

| Capability | Output |
|------------|--------|
| Strategic plan draft | Annual/quarterly |
| Roadmap generator | Milestones, KPIs, risks |
| Resource estimator | Budget breakdown |
| `generate_roadmap` tool | Integrated |

**Phase 2B exit:** Second module in production; one additional workflow metric improved.

---

## 7. Phase 2C — Third Module or Scale (Weeks 47–56)

Choose **one** based on Gate G3 report:

### Option A — Patent Assistant

| Prerequisite | Action |
|--------------|--------|
| Patent corpus ≥ 2,000 docs | Ingest claims separately |
| IPC taxonomy | Map to subject domains |
| Legal review | Disclaimer for non-legal advice |

| Capability | Phase |
|------------|-------|
| Prior-art search | 2C |
| Novelty screening | 2C |
| Claim structure analysis | 2D |
| Patent landscape viz | 3 |

### Option B — Research Assistant

| Capability | Output |
|------------|--------|
| Literature review | Cited summary from corpus |
| Proposal generation | Full draft from template |
| Gap analysis | Gap list + sources |

### Option C — Innovation / Technology Scouting (internal first)

```text
Scouting Pipeline (Phase 2C — internal corpus only)
───────────────────────────────────────────────────
Corpus → Topic clustering → Trend extraction
              │
              ▼
    Opportunity brief (cited)
              │
              ▼
    Compare with org strategic priorities
```

**No open-web crawl in Phase 2C** — curated RSS/journal feeds only if added.

---

## 8. Version 1.0 Release Criteria

| # | Criterion |
|---|-----------|
| 1 | 3+ department modules OR 2 modules + strong platform |
| 2 | 50,000+ documents indexed |
| 3 | 2 institutions (pilot + beta) OR 1 institution 100+ users |
| 4 | SSO, hybrid search, comparison tool live |
| 5 | Uptime ≥ 99.5% over 30 days |
| 6 | Security review passed |
| 7 | User manual + admin guide complete |

---

## 9. Roadmap alignment

```text
Timeline                    Module / Release
──────────────────────────────────────────────────
Month 8–9    Phase 2A        Platform + hybrid search
Month 10–11  Phase 2B        Module 2 (Eval/Patent/Plan)
Month 12–14  Phase 2C        Module 3 or scale
Month 15+    Phase 3         Multi-agent, knowledge graph
```

See [DOC-102 Product Roadmap](../02-product/DOC-102-product-roadmap.md)

---

## 10. Risks (Phase 2)

| ID | Risk | Mitigation |
|----|------|------------|
| R1 | Pilot success doesn't generalize | Second beta customer |
| R2 | Module overload | One module per 8-week block |
| R3 | Patent legal exposure | Strong disclaimers; human review |
| R4 | Corpus quality degrades at scale | Curator QA sampling 5%/month |
| R5 | Team burnout | Hire before Phase 2B |
| R6 | Competitor ships similar | Accelerate on-prem + domain moat |

---

## 11. KPIs for Phase 2 Success

| KPI | Target (Phase 2 end) |
|-----|----------------------|
| Weekly active users | ≥ 100 |
| Modules in production | ≥ 3 |
| Documents indexed | ≥ 50,000 |
| Customer institutions | ≥ 2 |
| Net revenue (if commercial) | Break-even path defined |
| Recall@5 | ≥ 80% |
| User trust | ≥ 4.0 |

---

## 12. Exit Criteria (MOV-011 Complete)

- [ ] Phase 2A platform enhancements deployed
- [ ] Second module live and measured
- [ ] Third module OR scale milestone achieved
- [ ] Version 1.0 criteria assessed
- [ ] Phase 3 charter drafted (multi-agent, knowledge graph)
- [ ] Budget approved for Phase 3 or commercial launch

---

## Related Documents

- [MOV-010 Pilot Deployment](./MOV-010-pilot-deployment.md)
- [DOC-102 Product Roadmap](../02-product/DOC-102-product-roadmap.md)
- [DOC-710 Resource & Budget](../06-development/DOC-710-resource-budget-plan.md)
- Module designs DOC-501–508 (planned)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial detailed movement doc |
