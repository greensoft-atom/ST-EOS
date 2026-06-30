# DOC-603 — Metadata Standard

**Document ID:** DOC-603  
**Version:** 1.0  
**Date:** 2026-06-30  
**Status:** Approved for MVP ingestion  
**Related:** [DOC-404 Knowledge Base Design](../05-ai/DOC-404-knowledge-base-design.md) | [DOC-602 Classification](../07-data/DOC-602-data-classification.md)

---

## 1. Purpose

Define **mandatory and optional metadata fields** for every document ingested into ST-EOS. Curators and uploaders must comply before indexing completes.

---

## 2. Core Document Record

| Field | Type | Required | Validation | Example |
|-------|------|----------|------------|---------|
| `title` | string | ✓ | 3–500 chars | National Research Grant Guidelines 2026 |
| `document_type` | enum | ✓ | See §3 | POL |
| `knowledge_layer` | int | ✓ | 1–4 | 4 |
| `language` | ISO 639-1 | ✓ | en, my, … | en |
| `publication_date` | date | ✓ | ISO 8601 | 2026-01-15 |
| `access_class` | enum | ✓ | PUB, INT, RST, CNF | INT |
| `department` | string | ✓ | Controlled vocab §4 | research_programs |
| `author` | string | · | | MSTI Policy Division |
| `keywords` | string[] | · | Max 20 | grant, eligibility |
| `source_institution` | string | · | | MSTI |
| `status` | enum | · | active, superseded | active |
| `version` | string | · | | 1.2 |
| `campaign_id` | uuid | · | Eval submissions | 2026-national-grant |
| `external_id` | string | · | Legacy system ref | MSTI-DOC-2024-042 |

---

## 3. Document Type Codes

| Code | Label | Default layer | Default class |
|------|-------|---------------|---------------|
| THS | Thesis | 1 | INT |
| ART | Article | 1 | INT |
| RPT | Research report | 1 | INT |
| EXH | Exhibition submission | 2 | RST |
| AWD | Award record | 2 | RST |
| PAT | Patent | 3 | CNF |
| POL | Policy | 4 | INT |
| SOP | Procedure | 4 | INT |
| FRM | Form/register | 4 | INT |
| PLN | Plan | 4 | INT |
| TPL | Template | cross | INT |
| GRANT_SUB | Grant submission | 2 | RST |

Full taxonomy: DOC-404 §5.

---

## 4. Department Vocabulary (MSTI Pilot)

| Code | Department |
|------|------------|
| `dg_office` | Office of the Director-General |
| `strategic_planning` | Strategic Planning and Policy |
| `research_programs` | Research Programs and Grant Administration |
| `innovation` | Innovation Promotion and Technology Transfer |
| `exhibition` | National S&T Exhibition Secretariat |
| `it` | IT and Digital Transformation |
| `legal` | Legal and Compliance |

---

## 5. Chunk-Level Metadata

Each vector chunk inherits document fields plus:

| Field | Type | Required |
|-------|------|----------|
| `chunk_id` | uuid | ✓ |
| `document_id` | uuid | ✓ |
| `chunk_index` | int | ✓ |
| `page_start` | int | · |
| `page_end` | int | · |
| `text_hash` | string | ✓ |

Schema reference: [DOC-403 §3.3](../05-ai/DOC-403-rag-architecture.md).

---

## 6. Quality Rules

| Rule | Enforcement |
|------|-------------|
| 100% mandatory fields on indexed docs | Ingestion worker rejects incomplete |
| `superseded` docs remain searchable but flagged | UI badge |
| Duplicate detection | SHA-256 file hash + fuzzy title match → curator queue |
| Language tag required | Default `en` if single-language PDF |

---

## 7. Curator Workflow

```text
Upload → Auto-suggest type/layer/class → Curator queue if low confidence
      → Approve → Index
```

Flags: missing metadata, low OCR confidence, possible duplicate.

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-30 | Extracted from DOC-404 for ingestion implementation |
