# DOC-403 — RAG Architecture

**Document ID:** DOC-403  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Draft

---

## 1. Purpose

Define the Retrieval-Augmented Generation (RAG) pipeline for ST-EOS — how documents become searchable knowledge and how retrieval integrates with LLM generation.

---

## 2. RAG Pipeline Overview

```text
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│ Ingest   │ →  │ Chunk    │ →  │ Embed    │ →  │ Index    │
│ Extract  │    │ Split    │    │ Vectorize│    │ Store    │
└──────────┘    └──────────┘    └──────────┘    └──────────┘

Query time:
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│ Query    │ →  │ Retrieve │ →  │ Rerank   │ →  │ Generate │
│ Embed    │    │ Top-K    │    │ Top-N    │    │ + Cite   │
└──────────┘    └──────────┘    └──────────┘    └──────────┘
```

---

## 3. Ingestion Stage

### 3.1 Supported formats (MVP)

| Format | Handler |
|--------|---------|
| PDF (text-native) | PyMuPDF / pdfplumber |
| PDF (scanned) | OCR (Tesseract / docling) |
| TXT, MD | Direct read |
| DOCX | python-docx (Phase 2) |

### 3.2 Extraction quality gates

| Check | Action if fail |
|-------|----------------|
| Empty text | Flag for manual review |
| OCR confidence < threshold | Flag `quality=low` |
| Wrong encoding | Attempt detection/conversion |
| Password protected | Reject with user message |

### 3.3 Metadata attachment (per chunk)

```json
{
  "chunk_id": "uuid",
  "document_id": "uuid",
  "chunk_index": 12,
  "page_start": 5,
  "page_end": 6,
  "document_title": "...",
  "document_type": "thesis",
  "knowledge_layer": 1,
  "department": "research",
  "language": "en",
  "date": "2024-03-15",
  "access_class": "internal"
}
```

---

## 4. Chunking Strategy

### 4.1 Default parameters (starting point — tune in PoC)

| Parameter | Value | Rationale |
|-----------|-------|-----------|
| Chunk size | 512–1024 tokens | Balance context vs precision |
| Overlap | 10–15% | Preserve cross-boundary meaning |
| Splitter | Semantic/paragraph aware | Avoid mid-sentence cuts |

### 4.2 Document-type overrides

| Type | Strategy |
|------|----------|
| Thesis/article | Split by section headings |
| Patent | Split by claim/section |
| Template | Keep whole or by field |
| Form/register | Row or field level |
| Report | Section-based |

### 4.3 Parent-child indexing (Phase 2)

- **Child chunks** — Small, for precise retrieval
- **Parent chunks** — Larger context for generation
- Retrieve child → expand to parent for LLM context

---

## 5. Embedding Strategy

### 5.1 Model selection

| Candidate | Notes |
|-----------|-------|
| bge-m3 | Strong multilingual |
| nomic-embed-text | Good general purpose |
| e5-large | High quality, heavier |

**Decision:** Benchmark on actual corpus in PoC (Movement 5).

### 5.2 Embedding storage

- Vector dimension stored with index metadata
- Re-embedding required on model change (version index)

---

## 6. Index & Storage

### 6.1 Vector index options

| Option | Pros | Cons |
|--------|------|------|
| **Qdrant** | Purpose-built, filtering | Extra service |
| **pgvector** | Single DB, simpler ops | Scale limits |

**MVP recommendation:** Evaluate both in PoC; pgvector if team prefers simplicity.

### 6.2 Hybrid search (Phase 2)

Combine:
- **Dense** — Vector similarity
- **Sparse** — BM25/keyword (PostgreSQL full-text or Elasticsearch)

MVP may use vector-only with metadata filters.

---

## 7. Retrieval Stage

### 7.1 Query processing

```text
User query → Optional query expansion → Embed query →
Vector search (top-K=20) → Metadata filter → Rerank (top-N=5) →
Context assembly
```

### 7.2 Filters

| Filter | Source |
|--------|--------|
| document_type | User selection |
| knowledge_layer | Agent scope |
| date_range | User selection |
| department | User selection |
| access_class | User RBAC |

### 7.3 Reranking

| MVP | Phase 2 |
|-----|---------|
| Cosine similarity only | Cross-encoder reranker (e.g., bge-reranker) |

---

## 8. Generation Stage

### 8.1 Prompt structure

```text
SYSTEM: You are ST-EOS assistant. Answer only from provided sources.
        Cite sources as [1], [2]. Say "insufficient evidence" if needed.

CONTEXT:
[1] {chunk_text} (source: {title}, p.{page})
[2] {chunk_text} (source: {title}, p.{page})

USER: {query}
```

### 8.2 Citation enforcement

1. LLM instructed to cite inline
2. Post-processor maps [N] → chunk metadata → clickable link
3. Validate cited indices exist in context
4. Flag uncited factual sentences (Phase 2)

### 8.3 Insufficient evidence handling

If top retrieval score < threshold:
```text
"I could not find sufficient evidence in the institutional repository
 to answer this question confidently. Retrieved sources may be irrelevant."
```

---

## 9. RAG for Specialized Tasks

### 9.1 Document review

- Retrieve: full target document + policy/guideline chunks
- Context window: may require map-reduce for long docs

**Long document strategy:**
```text
Split doc into sections → Review each → Merge findings
```

### 9.2 Document creation

- Retrieve: topic-relevant chunks + similar past documents
- Template slots filled with cited content

### 9.3 Evaluation

- Retrieve: rubric definitions + comparable past submissions
- Score with evidence per criterion

---

## 10. Performance Targets

| Metric | MVP target |
|--------|------------|
| Ingestion throughput | 100 docs/hour (hardware dependent) |
| Query latency (retrieval only) | < 2s |
| End-to-end Q&A | < 10s |
| Index size | 100K+ chunks |

---

## 11. Evaluation Framework

### 11.1 Retrieval metrics

| Metric | Description |
|--------|-------------|
| Recall@5 | Correct doc in top 5 |
| MRR | Mean reciprocal rank |
| Precision@5 | Relevant in top 5 |

### 11.2 Generation metrics

| Metric | Method |
|--------|--------|
| Citation accuracy | Manual review sample |
| Faithfulness | LLM-as-judge + human |
| Completeness | Checklist coverage |

### 11.3 Test set

- 50+ questions with known source documents
- Created from domain experts during Phase 0
- Updated each release

---

## 12. Operational Concerns

| Concern | Approach |
|---------|----------|
| Index staleness | Re-index on metadata edit |
| Model upgrade | Blue/green index versioning |
| Failed ingestion | Dead letter queue + admin UI |
| Large corpus | Sharded collections by layer/type |

---

## 13. Security

- Embeddings stored locally only
- Access filters applied at retrieval time (not post-filter)
- Audit log includes retrieved chunk IDs
- No query content sent externally

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial RAG architecture |
