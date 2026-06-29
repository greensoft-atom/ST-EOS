# DOC-404 — Knowledge Base Design

**Document ID:** DOC-404  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Draft

---

## 1. Purpose

Define the structure, taxonomy, and governance of ST-EOS institutional knowledge — how diverse S&T documents are organized to power retrieval and department agents.

---

## 2. Knowledge Base Concept

The ST-EOS knowledge base is not a single folder. It is a **layered, typed, metadata-rich corpus** that mirrors how S&T executive organizations actually work.

```text
┌─────────────────────────────────────────────────────────┐
│                  ST-EOS Knowledge Base                  │
├─────────────┬─────────────┬─────────────┬───────────────┤
│  Layer 1    │  Layer 2    │  Layer 3    │  Layer 4      │
│  Scientific │  Innovation │  Patent     │  Organizational│
│  Literature │  Projects   │  Knowledge  │  Documents    │
└─────────────┴─────────────┴─────────────┴───────────────┘
         │              │              │              │
         └──────────────┴──────────────┴──────────────┘
                              │
                    ┌─────────▼─────────┐
                    │ Templates & Frames │
                    │ (Cross-cutting)    │
                    └───────────────────┘
```

---

## 3. Knowledge Layers

### Layer 1 — Scientific Literature

**Content types:**
- Thesis and dissertations
- Research articles and preprints
- Journal and magazine articles
- Study and research reports
- Technical surveys and state-of-art reviews

**Primary consumers:** Research department, Planning, Innovation

**AI services enabled:**
- Literature review
- State-of-art analysis
- Research gap identification
- Citation extraction
- Summarization

**Metadata requirements:**

| Field | Required |
|-------|----------|
| title | ✓ |
| authors | ✓ |
| publication_date | ✓ |
| document_type | ✓ |
| subject/domain | ✓ |
| language | ✓ |
| keywords | recommended |
| abstract | recommended |
| source_institution | optional |

---

### Layer 2 — Innovation Projects

**Content types:**
- Science & technology exhibition submissions
- Award-winning and prized works documentation
- Competition project records
- Technology demonstration descriptions
- Innovation case studies
- Product and prototype descriptions

**Primary consumers:** Innovation, Exhibition, Evaluation, Tech Transfer

**AI services enabled:**
- Similar project search
- Innovation scoring
- Improvement suggestions
- Commercialization potential assessment
- Project comparison and ranking

**Metadata requirements:**

| Field | Required |
|-------|----------|
| project_title | ✓ |
| project_year | ✓ |
| category/domain | ✓ |
| award_status | ✓ |
| inventor/team | ✓ |
| institution | ✓ |
| outcome_type | recommended |
| trl_level | optional |

---

### Layer 3 — Patent & IP Knowledge

**Content types:**
- Patent applications and grants
- Patent claims and specifications
- Copyright documentation
- Prior art collections
- IP policy documents

**Primary consumers:** Patent office, Legal, Tech Transfer

**AI services enabled:**
- Prior-art search
- Patent similarity
- Novelty evaluation
- Claim analysis
- Patent landscape mapping

**Metadata requirements:**

| Field | Required |
|-------|----------|
| patent_id / application_no | ✓ |
| title | ✓ |
| filing_date | ✓ |
| status | ✓ |
| inventors | ✓ |
| ipc/cpc_class | recommended |
| jurisdiction | ✓ |

**Note:** Patent layer may be Phase 2 if corpus preparation is heavy.

---

### Layer 4 — Organizational Documents

**Content types:**
- Regulations and statutes
- Standard operating procedures
- Policies and guidelines
- Registration forms and official records
- Meeting minutes and decisions
- Strategic plans and annual reports
- Internal memos and circulars

**Primary consumers:** All departments, Administration, Executives

**AI services enabled:**
- Compliance checking
- Form generation guidance
- Process navigation
- Policy Q&A
- Plan drafting alignment

**Metadata requirements:**

| Field | Required |
|-------|----------|
| title | ✓ |
| document_type | ✓ |
| effective_date | ✓ |
| department | ✓ |
| status (active/superseded) | ✓ |
| version | recommended |

---

## 4. Cross-Cutting Asset — Templates & Frames

Templates are first-class knowledge assets, not regular documents.

**Content types:**
- Research report templates
- Study plan frames
- Research proposal formats
- Evaluation rubrics and score sheets
- Registration form structures
- Article source text frames
- Meeting minute formats
- Strategic plan outlines

**Storage:** Template registry (separate from vector index, but referenced by Creation Agent)

**Template schema example:**

```yaml
template_id: research_proposal_v2
name: Research Proposal
version: "2.0"
sections:
  - id: abstract
    title: Abstract
    required: true
    guidance: "Max 300 words summarizing objectives and methods"
  - id: background
    title: Background and Literature
    required: true
    rag_enabled: true
  - id: methodology
    title: Methodology
    required: true
  - id: budget
    title: Budget Estimate
    required: true
    type: table
  - id: timeline
    title: Timeline
    required: true
    type: gantt
variables:
  - name: project_title
    type: string
    required: true
  - name: duration_months
    type: integer
    required: true
  - name: budget
    type: currency
    required: true
```

---

## 5. Document Type Taxonomy

Master list for classification:

| Code | Type | Layer |
|------|------|-------|
| THS | Thesis | 1 |
| ART | Article | 1 |
| JRN | Journal issue | 1 |
| RPT | Research report | 1 |
| EXH | Exhibition submission | 2 |
| AWD | Award record | 2 |
| PRD | Product description | 2 |
| PAT | Patent document | 3 |
| CPY | Copyright record | 3 |
| POL | Policy | 4 |
| REG | Regulation | 4 |
| SOP | Procedure | 4 |
| FRM | Form/register | 4 |
| PLN | Plan | 4 |
| MIN | Meeting minutes | 4 |
| TPL | Template | Cross |

---

## 6. Subject Domain Taxonomy (Starter)

Adapt to national/institutional standards:

```text
Science & Technology
├── Natural Sciences
│   ├── Physics
│   ├── Chemistry
│   ├── Biology
│   └── Earth Science
├── Engineering
│   ├── Mechanical
│   ├── Electrical
│   ├── Civil
│   └── Software/IT
├── Agriculture & Food
├── Health & Medicine
├── Energy & Environment
├── Materials & Manufacturing
├── Innovation & Entrepreneurship
└── Science Policy & Management
```

Curators map documents to ≥1 domain node.

---

## 7. Access Classification

| Class | Description | Example |
|-------|-------------|---------|
| Public | Shareable externally | Published articles |
| Internal | Staff only | Internal reports |
| Restricted | Role-based | Evaluation submissions |
| Confidential | Named access | Unpublished patent drafts |

**Rule:** Classification set at ingestion; enforced at retrieval.

---

## 8. Corpus Inventory (Your Assets Mapped)

Based on stated existing assets:

| Your asset | Layer | Type code | MVP priority |
|------------|-------|-----------|--------------|
| Thesis | 1 | THS | High |
| Articles | 1 | ART | High |
| Magazines | 1 | JRN | Medium |
| Exhibition prized/awarded works | 2 | AWD, EXH | High |
| Patent documentation | 3 | PAT | Phase 2 |
| Copyright documentation | 3 | CPY | Phase 2 |
| Technical product descriptions | 2 | PRD | Medium |
| Research/study reports | 1 | RPT | High |
| Templates and frames | Cross | TPL | **Highest** |
| Register forms | 4 | FRM | High |
| Plans | 4 | PLN | Medium |

---

## 9. MVP Corpus Target

| Layer | MVP doc count (target) |
|-------|------------------------|
| Templates | All available (50–200) |
| Layer 4 (policies/forms) | 200–500 |
| Layer 1 (literature sample) | 2,000–5,000 |
| Layer 2 (projects/awards) | 500–2,000 |
| Layer 3 (patents) | 0–500 (optional) |
| **Total** | **3,000–10,000** |

---

## 10. Data Quality Standards

| Dimension | Standard |
|-----------|----------|
| Completeness | Mandatory metadata 100% |
| Text extractability | ≥ 95% docs machine-readable |
| Duplicate detection | Hash + title fuzzy match |
| Currency | Superseded docs flagged, not deleted |
| Language tagging | ISO 639-1 code on every doc |
| Provenance | Source institution and ingest date logged |

---

## 11. Curation Workflow

```text
Upload → Auto-classify (suggest type/layer) →
Curator review queue → Approve/edit metadata →
Index → Available for search
```

Curators see:
- Low OCR confidence flag
- Missing metadata flag
- Possible duplicate flag

---

## 12. Knowledge Graph (Phase 3 — Preview)

Entities and relationships for future graph layer:

**Entities:** Project, Person, Institution, Patent, Publication, Technology, Award

**Relationships:**
- `authored_by`, `submitted_to`, `awarded`, `cites`, `similar_to`, `derived_from`, `funded_by`

Not required for MVP RAG; plan for Phase 3.

---

## 13. Governance

| Role | Responsibility |
|------|----------------|
| Data Owner (department) | Content authority |
| Curator | Metadata quality |
| Admin | Access policies |
| AI Lead | Retrieval quality monitoring |

Review cadence: quarterly corpus audit.

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial knowledge base design |
