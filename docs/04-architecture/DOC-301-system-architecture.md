# DOC-301 — System Architecture Document

**Document ID:** DOC-301  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Draft

---

## 1. Architecture Overview

ST-EOS follows a **layered, modular, local-first** architecture. Components are containerized for on-premise deployment.

```text
┌─────────────────────────────────────────────────────────────────┐
│                     PRESENTATION LAYER                          │
│  Web Portal (React/Vue) — Task wizards, search, review, create  │
└───────────────────────────────┬─────────────────────────────────┘
                                │ HTTPS / REST
┌───────────────────────────────▼─────────────────────────────────┐
│                     APPLICATION LAYER                           │
│  API Gateway / Backend (FastAPI)                                │
│  ┌─────────────┐ ┌──────────────┐ ┌─────────────────────────┐    │
│  │ Auth/RBAC   │ │ Workflow Svc │ │ Document Service        │    │
│  └─────────────┘ └──────────────┘ └─────────────────────────┘    │
└───────────────────────────────┬─────────────────────────────────┘
                                │
┌───────────────────────────────▼─────────────────────────────────┐
│                     AI ORCHESTRATION LAYER                      │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │ AI Orchestrator — routing, policies, prompt assembly      │  │
│  └──────────────────────────────────────────────────────────┘  │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────────┐  │
│  │ RAG Svc  │ │ Review   │ │ Create   │ │ Expert Agents    │  │
│  │          │ │ Agent    │ │ Agent    │ │ (Research, Eval…)│  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────────────┘  │
└───────────────────────────────┬─────────────────────────────────┘
                                │
┌───────────────────────────────▼─────────────────────────────────┐
│                     KNOWLEDGE LAYER                             │
│  Ingestion Pipeline │ Vector Index │ Metadata DB │ Object Store │
└───────────────────────────────┬─────────────────────────────────┘
                                │
┌───────────────────────────────▼─────────────────────────────────┐
│                     INFRASTRUCTURE LAYER                          │
│  Local LLM Runtime (Ollama/vLLM) │ PostgreSQL │ Qdrant/pgvector  │
│  MinIO/Filesystem │ Redis (optional queue) │ Docker               │
└─────────────────────────────────────────────────────────────────┘
```

---

## 2. Architecture Principles

| # | Principle | Implication |
|---|-----------|-------------|
| 1 | Local-first | All inference and storage on-premise |
| 2 | Citation-first | RAG service mandatory for factual outputs |
| 3 | Modular agents | Department assistants are configured agents |
| 4 | Async ingestion | Upload ≠ immediate index; queue-based processing |
| 5 | Audit everything | Orchestrator logs all AI calls |
| 6 | Start simple | Monolith backend acceptable for MVP; split later |

---

## 3. Component Descriptions

### 3.1 Presentation Layer — Web Portal

**Responsibility:** User interaction, task workflows, result display

| Module | Functions |
|--------|-----------|
| Dashboard | Quick access to search, review, create, assistant |
| Repository | Browse, upload, preview documents |
| Search | Query input, answers, citation panel |
| Review | Select doc → review type → findings → export |
| Create | Template select → inputs → draft editor → export |
| Assistant | Department-specific guided workflows |
| Admin | Users, templates, audit log, system status |

**Technology (recommended):** React + TypeScript, Tailwind/shadcn UI

### 3.2 Application Layer — Backend API

**Responsibility:** Business logic, authentication, orchestration entry point

| Service | Functions |
|---------|-----------|
| Auth Service | Login, JWT/session, RBAC enforcement |
| Document Service | Upload, metadata CRUD, preview URLs |
| Workflow Service | Review jobs, creation jobs, status tracking |
| Template Service | Template CRUD, variable definitions |
| User Service | User/role management |
| Audit Service | Append-only AI interaction log |

**Technology (recommended):** Python FastAPI, SQLAlchemy, Pydantic

### 3.3 AI Orchestration Layer

**Responsibility:** Route requests to appropriate AI pipelines; enforce policies

```text
Request → Policy check → Prompt assembly → RAG retrieval →
LLM call → Post-process (citations, format) → Audit log → Response
```

See [AI Agent Architecture](../05-ai/DOC-402-ai-agent-architecture.md).

### 3.4 Knowledge Layer

**Responsibility:** Document storage, processing, indexing

| Component | Function |
|-----------|----------|
| Object Store | Original PDF/text files |
| Metadata DB | Document records, tags, status |
| Ingestion Worker | Extract, chunk, embed, index |
| Vector Index | Similarity search |
| Template Store | Document templates |

See [RAG Architecture](../05-ai/DOC-403-rag-architecture.md) and [Knowledge Base Design](../05-ai/DOC-404-knowledge-base-design.md).

### 3.5 Infrastructure Layer

| Component | Function |
|-----------|----------|
| Local LLM | Text generation |
| Embedding Model | Vector generation |
| PostgreSQL | Relational data |
| Vector DB | Qdrant or pgvector |
| Job Queue | Celery/RQ/Redis for async ingestion |
| Docker | Container orchestration |

---

## 4. Deployment Architecture (MVP)

Single-server or small cluster on-premise:

```text
┌─────────────────────────────────────────────┐
│              ST-EOS Server                  │
│  ┌─────────┐ ┌─────────┐ ┌──────────────┐  │
│  │ Nginx   │ │ Backend │ │ Frontend     │  │
│  │ (proxy) │ │ (API)   │ │ (static)     │  │
│  └─────────┘ └────┬────┘ └──────────────┘  │
│                   │                         │
│  ┌─────────┐ ┌────▼────┐ ┌──────────────┐  │
│  │ LLM     │ │ Worker  │ │ PostgreSQL   │  │
│  │ Runtime │ │ (ingest)│ │ + Vector     │  │
│  └─────────┘ └─────────┘ └──────────────┘  │
│  ┌─────────────────────────────────────┐   │
│  │ File Storage (/data/documents)      │   │
│  └─────────────────────────────────────┘   │
└─────────────────────────────────────────────┘
```

### Minimum hardware (indicative)

| Resource | Minimum | Recommended |
|----------|---------|-------------|
| CPU | 8 cores | 16+ cores |
| RAM | 32 GB | 64–128 GB |
| GPU | Optional (CPU inference ok for PoC) | 24GB+ VRAM for larger models |
| Storage | 500 GB SSD | 2 TB+ SSD |

---

## 5. Data Flow Diagrams

### 5.1 Document ingestion

```text
User upload → API → Object store → Queue job →
Worker: extract text → chunk → embed → vector index →
Update metadata (status=indexed)
```

### 5.2 RAG search

```text
User query → API → Orchestrator → Embed query →
Vector search (+ optional keyword) → Rerank →
Top-k chunks → Prompt assembly → LLM →
Parse response + attach citations → Audit → User
```

### 5.3 Document review

```text
User selects doc + review type → Orchestrator →
Retrieve doc full text + relevant policies →
Review prompt → LLM → Structured findings JSON →
Render report → Export optional
```

---

## 6. Integration Points (MVP)

| Integration | MVP | Phase 2 |
|-------------|-----|---------|
| File upload (UI) | ✓ | |
| REST API | ✓ | |
| LDAP/SSO | | ✓ |
| Email notifications | | ✓ |
| External DMS | | ✓ |
| Grant management system | | ✓ |

---

## 7. Security Architecture (Summary)

| Layer | Control |
|-------|---------|
| Network | Internal/VPN; TLS termination at proxy |
| Auth | JWT or session; password policy |
| AuthZ | RBAC per endpoint and document |
| Data | Encryption at rest; classified doc flags |
| AI | No external API calls; audit all prompts/responses |
| Ops | Backup, access logging, admin separation |

Full specification: DOC-306 (planned).

---

## 8. Scalability Path

| Stage | Architecture |
|-------|--------------|
| MVP | Single server, monolith backend |
| v1.0 | Separate worker nodes; LLM on GPU server |
| v2.0 | Horizontal API scaling; read replicas |
| v3.0 | Multi-tenant; federated search nodes |

---

## 9. Technology Stack Decision (Proposed)

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Frontend | React + TypeScript | Ecosystem, component libraries |
| Backend | FastAPI (Python) | AI/ML library access |
| DB | PostgreSQL | Reliable, pgvector option |
| Vector | Qdrant or pgvector | Evaluate in PoC |
| LLM | Ollama/vLLM | Local inference |
| Queue | Redis + RQ/Celery | Async ingestion |
| Containers | Docker Compose | Simple on-prem deploy |

**Action:** Confirm in Phase 0 PoC (Movement 4).

---

## 10. Open Architecture Decisions

| ADR | Question | Target date |
|-----|----------|-------------|
| ADR-001 | Qdrant vs pgvector | PoC week 2 |
| ADR-002 | Ollama vs vLLM | PoC week 1 |
| ADR-003 | Monolith vs microservices | MVP = monolith |
| ADR-004 | Primary LLM model | PoC benchmark |

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial architecture |
