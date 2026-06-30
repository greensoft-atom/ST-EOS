# DOC-402 — AI Agent Architecture

**Document ID:** DOC-402  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Draft

---

## 1. Purpose

Define how AI agents are structured, orchestrated, and extended in ST-EOS — from MVP single-agent flows to Phase 3 multi-agent collaboration.

---

## 2. Agent Design Philosophy

ST-EOS agents are **not autonomous personas**. They are:

- **Configured pipelines** — Prompt + tools + retrieval scope + output schema
- **Domain-bounded** — Each agent accesses specific knowledge layers
- **Evidence-based** — Citations required for factual outputs
- **Human-supervised** — Recommendations, not binding decisions

---

## 3. Agent Taxonomy

### 3.1 Core platform agents (MVP)

| Agent | Purpose | Tools |
|-------|---------|-------|
| **Retrieval Agent** | Find relevant knowledge | Vector search, metadata filter, rerank |
| **Review Agent** | Analyze document quality | Full-text read, policy RAG, checklist |
| **Creation Agent** | Generate structured documents | Template engine, RAG, format validator |
| **Citation Agent** | Attach and verify sources | Chunk lookup, reference formatter |

### 3.2 Department expert agents

| Agent | Phase | Primary knowledge layers |
|-------|-------|--------------------------|
| Evaluation Agent | **MVP** | Layer 2 (Projects), rubrics, policies |
| Research Agent | Phase 2B | Layer 1 (Literature), templates |
| Patent Agent | Phase 2 | Layer 3 (Patents) |
| Innovation Agent | Phase 2 | Layer 1, 2 |
| Planning Agent | Phase 2 | Layer 4, past plans |
| Exhibition Agent | Phase 2 | Layer 2 |
| Tech Transfer Agent | Phase 3 | Layer 2, 3, product specs |
| Reporting Agent | Phase 3 | All layers, KPI data |

### 3.3 Orchestration agents (Phase 3)

| Agent | Purpose |
|-------|---------|
| Router Agent | Classify user intent → route to expert agent |
| Decision Agent | Synthesize multi-agent outputs → recommendation |
| Risk Agent | Cross-cutting risk assessment |

---

## 4. Agent Architecture Diagram

```text
                    ┌─────────────────┐
                    │  User Request   │
                    └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │ AI Orchestrator │
                    │ - auth check    │
                    │ - policy apply  │
                    │ - audit start   │
                    └────────┬────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
     ┌────────▼────┐  ┌──────▼──────┐  ┌───▼──────────┐
     │ Router      │  │ Shared RAG  │  │ Shared LLM   │
     │ (Phase 3)   │  │ Service     │  │ Gateway      │
     └────────┬────┘  └──────┬──────┘  └───┬──────────┘
              │              │              │
     ┌────────▼──────────────▼──────────────▼────────┐
     │              Expert Agent                      │
     │  ┌─────────────────────────────────────────┐  │
     │  │ System prompt + domain instructions      │  │
     │  │ Tool access (search, template, validate) │  │
     │  │ Output schema (JSON / markdown)          │  │
     │  └─────────────────────────────────────────┘  │
     └────────────────────┬──────────────────────────┘
                          │
                 ┌────────▼────────┐
                 │ Post-processor  │
                 │ - citation link │
                 │ - format check  │
                 │ - confidence    │
                 └────────┬────────┘
                          │
                 ┌────────▼────────┐
                 │ Audit + Response│
                 └─────────────────┘
```

---

## 5. Agent Configuration Model

Each agent is defined by a configuration record (YAML/JSON in repo):

```yaml
agent_id: research_assistant
version: "1.0"
display_name: Research Assistant
description: Literature review and proposal support

knowledge_scope:
  layers: [1]
  document_types: [thesis, article, report, journal]
  max_chunks: 15

tools:
  - rag_search
  - template_fill
  - citation_format

llm:
  model: qwen2.5:14b
  temperature: 0.3
  max_tokens: 4096

output_schema: research_output_v1

prompts:
  system: prompts/research/system.md
  tasks:
    literature_review: prompts/research/lit_review.md
    proposal: prompts/research/proposal.md
    gap_analysis: prompts/research/gaps.md

policies:
  require_citations: true
  min_sources: 2
  human_review_required: false
```

---

## 6. MVP Agent Flows

### 6.1 Review Agent flow

```text
Input: document_id, review_type
  1. Load document text
  2. Load review checklist for type
  3. RAG retrieve relevant policies (compliance type)
  4. Assemble prompt with doc + policies + checklist
  5. LLM generate structured findings
  6. Validate JSON schema
  7. Link findings to sections
  8. Return review report
```

### 6.2 Creation Agent flow

```text
Input: template_id, user_inputs, optional context_query
  1. Load template with variable slots
  2. If context_query: RAG retrieve relevant chunks
  3. Assemble prompt: template + inputs + sources
  4. LLM fill template sections
  5. Insert citation markers
  6. Return editable draft
```

### 6.3 Research Agent flow (MVP)

```text
Input: task_type, topic, parameters
  1. RAG search corpus for topic (broad retrieval)
  2. Rerank and deduplicate sources
  3. Select task prompt (lit review / proposal / gaps)
  4. LLM generate structured output
  5. Citation Agent verify chunk references
  6. Return result with source bibliography
```

### 6.4 Evaluation Agent flow (MVP alternative)

```text
Input: submission_ids[], rubric_id
  1. Load rubric criteria and weights
  2. For each submission: load full text
  3. RAG retrieve comparable past projects
  4. LLM score per criterion with evidence
  5. Aggregate weighted score
  6. Generate comparison matrix
  7. Return ranked results (human approval required)
```

---

## 7. Multi-Agent Workflow (Phase 3)

Example: "Should we fund Project X?"

```text
┌─────────────────┐
│ User Question   │
└────────┬────────┘
         ▼
┌─────────────────┐
│ Router Agent    │ → intent: funding_decision
└────────┬────────┘
         ▼
┌─────────────────┐     ┌─────────────────┐
│ Research Agent  │     │ Patent Agent    │
│ (state of art)  │     │ (IP risk)       │
└────────┬────────┘     └────────┬────────┘
         │                       │
         └───────────┬───────────┘
                     ▼
         ┌─────────────────┐
         │ Evaluation Agent│
         │ (rubric score)  │
         └────────┬────────┘
                  ▼
         ┌─────────────────┐
         │ Decision Agent  │
         │ synthesize      │
         └────────┬────────┘
                  ▼
         ┌─────────────────┐
         │ Evidence Pack   │
         │ + Recommendation│
         └─────────────────┘
```

**Orchestration engine:** LangGraph or custom state machine with checkpointing.

---

## 8. Tool Library

| Tool | Description | Used by |
|------|-------------|---------|
| `rag_search` | Semantic + filtered search | All agents |
| `get_document` | Full document text | Review, Evaluation |
| `get_template` | Load template definition | Creation |
| `validate_schema` | Check output JSON | All agents |
| `format_citations` | Standardize references | Research, Creation |
| `compare_documents` | Diff/summary across docs | Evaluation |
| `score_rubric` | Apply scoring framework | Evaluation |
| `generate_roadmap` | Milestone generator | Planning (Phase 2) |

---

## 9. Policy Enforcement

| Policy | Enforcement point |
|--------|-------------------|
| Require citations | Post-processor rejects output if missing |
| Classified data | RAG filter excludes unauthorized chunks |
| Token limits | Orchestrator truncates context |
| Model version | Logged in audit |
| Human review flag | UI blocks export until approved (evaluation) |

---

## 10. Agent Quality & Testing

Each agent must have:

1. **Golden test cases** — Input → expected structure (not exact text)
2. **Citation accuracy test** — Sources match claims
3. **Regression suite** — Run on model/prompt changes
4. **User feedback hook** — Thumbs up/down → improvement backlog

See DOC-407 AI Evaluation Framework (planned).

---

## 11. MVP Implementation Approach

**Keep it simple:**

- Orchestrator = Python module with agent registry
- Each agent = config + prompt files + handler function
- No LangGraph in MVP unless team already proficient
- Single LLM call per task where possible; chain only when necessary

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial agent architecture |
