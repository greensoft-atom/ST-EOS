# DOC-102 — Product Roadmap

**Document ID:** DOC-102  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Draft

---

## 1. Roadmap Overview

```text
2026 Q3-Q4          2027 Q1-Q2          2027 Q3-Q4          2028+
────────────────    ────────────────    ────────────────    ────────
Phase 0             Phase 1 MVP         Phase 2             Phase 3
Discovery & PoC     Pilot Platform      Module Expansion    Platform Scale
```

---

## 2. Phase 0 — Discovery & Proof of Concept

**Duration:** 8 weeks  
**Goal:** Validate feasibility before major build investment

| Deliverable | Description |
|-------------|-------------|
| Pilot agreement | 1 anchor institution scoped |
| Data inventory | Corpus catalog and MVP subset |
| RAG PoC | Retrieval + citation quality measured |
| Architecture decision | Stack and deployment model locked |
| MVP requirements | Frozen scope |

**Exit gate:** PoC metrics pass → proceed to Phase 1

---

## 3. Phase 1 — MVP (Version 0.9)

**Duration:** 14 weeks build + 8 weeks pilot  
**Codename:** Foundation  
**Goal:** Pilot-ready platform with core wedge

### 3.1 Features

| Feature | Priority | Description |
|---------|----------|-------------|
| F-001 Document repository | P0 | Upload, store, browse PDF/text |
| F-002 Metadata management | P0 | Tag type, date, author, department |
| F-003 Ingestion pipeline | P0 | OCR, chunk, embed, index |
| F-004 RAG search | P0 | Q&A with source citations |
| F-005 Document review | P0 | Structured review reports |
| F-006 Template creation | P0 | Generate docs from templates + context |
| F-007 Vertical assistant | P0 | **Evaluation Assistant** (MSTI) |
| F-008 User roles & auth | P0 | 6 roles per DOC-307 |
| F-009 Audit log | P0 | AI query/response logging |
| F-010 Export | P1 | PDF/DOCX export of outputs |

### 3.2 MVP module (locked)

| Pilot | MVP assistant |
|-------|---------------|
| MSTI (current) | **Evaluation Assistant** |

Research Assistant: Phase 2B per [ADR-005](../04-architecture/decisions/ADR-005-mvp-module-selection.md).

### 3.3 Success metrics

- 10,000+ documents indexed
- **≥ 30** active weekly users (40–70 enrolled)
- 80% search satisfaction
- 30% committee prep time reduction (W2); see [DOC-PILOT-001 §7](../01-business/DOC-PILOT-001-government-executive-pilot-scope.md)

---

## 4. Phase 2 — Version 1.0 (Module Expansion)

**Duration:** 16 weeks  
**Goal:** Full utility suite + 3 department modules

### 4.1 Platform enhancements

| Feature | Description |
|---------|-------------|
| Hybrid search | Keyword + vector + reranking |
| Review workflows | Assign, comment, approve |
| Template library UI | Curator-managed templates |
| Batch ingestion | Folder/bulk upload |
| Comparison tool | Multi-document/project compare |
| Roadmap generator | Goal → milestones → KPIs |
| SSO/LDAP | Enterprise authentication |

### 4.2 New modules (deliver 3)

| Module | Rationale |
|--------|-----------|
| Evaluation Assistant | If not in MVP; high executive value |
| Patent Assistant | Distinct corpus, clear ROI |
| Planning Assistant | Strategic plans and roadmaps |
| Innovation Assistant | Scouting on internal corpus first |

**Recommended order:** Evaluation → Patent → Planning

### 4.3 Technology scouting (Phase 2 scope)

- Internal trend analysis from corpus
- Curated external source ingestion (optional)
- Technology comparison frameworks
- **Not:** fully autonomous open-web crawling

---

## 5. Phase 3 — Version 2.0 (Orchestration & Scale)

**Duration:** 20+ weeks  
**Goal:** Multi-agent workflows and executive decision support

| Capability | Description |
|------------|-------------|
| Multi-agent orchestrator | Cross-department agent pipelines |
| Decision support dashboard | Situation → options → recommendation |
| Reporting Assistant | KPI dashboards, auto-briefings |
| Exhibition Assistant | Large-scale project ranking |
| Tech Transfer Assistant | Commercialization analysis |
| Knowledge graph layer | Entity relationships (projects, people, patents) |
| Multi-tenant / multi-org | If national deployment required |

---

## 6. Phase 4 — Version 3.0 (National Platform — Optional)

| Capability | Description |
|------------|-------------|
| Federated repositories | Cross-institution search (policy-controlled) |
| National innovation registry | Exhibition and award archive |
| Grant management integration | API connectors |
| Policy simulation | What-if scenario modeling |
| Advanced analytics | Portfolio trends, forecasting |

---

## 7. Feature Timeline (Visual)

```text
Feature                    Ph0   Ph1   Ph2   Ph3   Ph4
─────────────────────────────────────────────────────────
Knowledge repository        ·    ████  ████  ████  ████
RAG search                  ██   ████  ████  ████  ████
Document review             ██   ████  ████  ████  ████
Document creation           ·    ████  ████  ████  ████
Research assistant          ·    ████  ████  ████  ████
Evaluation assistant        ·    ████  ████  ████  ████
Patent assistant            ·     ·    ████  ████  ████
Planning assistant          ·     ·    ████  ████  ████
Innovation/scouting         ·     ·    ████  ████  ████
Comparison & SWOT           ·     ·    ████  ████  ████
Multi-agent workflows       ·     ·     ·    ████  ████
Knowledge graph             ·     ·     ·    ████  ████
National federation         ·     ·     ·     ·    ████
```

---

## 8. Release Naming

| Version | Name | Target |
|---------|------|--------|
| 0.5 | PoC | Internal only |
| 0.9 | MVP | Pilot deployment |
| 1.0 | Foundation+ | General institutional release |
| 2.0 | Executive | Multi-agent, full module suite |
| 3.0 | National | Federation scale |

---

## 9. Dependencies & Sequencing Rules

1. **No module before RAG works** — All assistants depend on retrieval quality
2. **No scouting before taxonomy** — Classification enables trend detection
3. **No multi-agent before single agents stable** — Orchestration adds complexity
4. **No fine-tuning before evaluation harness** — Must measure baseline first
5. **Templates before creation at scale** — Curator investment required

---

## 10. Roadmap Review Cadence

- **Monthly:** Progress vs milestones
- **Quarterly:** Reprioritize modules based on pilot/customer feedback
- **At each phase gate:** Go/No-Go with sponsor

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial roadmap |
| 1.1 | 2026-06-30 | Evaluation-only MVP; KPI alignment with DOC-PILOT-001 |
