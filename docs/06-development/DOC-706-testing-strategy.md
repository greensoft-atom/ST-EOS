# DOC-706 — Testing Strategy

**Document ID:** DOC-706  
**Version:** 1.0  
**Date:** 2026-06-29  
**Status:** Draft

---

## 1. Purpose

Define testing approach for ST-EOS — including conventional software tests and **AI-specific evaluation** for RAG, review, and generation quality.

---

## 2. Testing Pyramid

```text
                    ┌─────────────┐
                    │   UAT       │  Pilot users, 5 scenarios
                    │  (Manual)   │
                ┌───┴─────────────┴───┐
                │  AI Eval Harness     │  RAG, review, agent
                │  (Weekly regression) │
            ┌───┴─────────────────────┴───┐
            │   Integration / API tests    │
            │   (pytest, per sprint)       │
        ┌───┴─────────────────────────────┴───┐
        │        Unit tests                    │
        │   (parsers, auth, schema, utils)     │
        └─────────────────────────────────────┘
```

---

## 3. Test Types & Schedule

| Type | Tool | Frequency | Owner | Sprint start |
|------|------|-----------|-------|--------------|
| Unit | pytest | Every PR | Dev | S0 |
| API integration | pytest + httpx | Every PR | Dev | S0 |
| Frontend component | Vitest | Every PR | FE | S0 |
| E2E (critical paths) | Playwright | Weekly | QA | S2 |
| RAG eval | Custom CLI | Weekly | AI | S2 |
| Review eval | Checklist suite | Per release | QA | S3 |
| Security scan | OWASP ZAP | S3, S6 | QA | S3 |
| Load test | k6/locust | S6 | DevOps | S6 |
| UAT | Manual scripts | S6, Pilot | PM | S6 |

---

## 4. AI Evaluation Framework

### 4.1 RAG test set structure

```text
data/eval/rag_questions.jsonl
──────────────────────────────
Each row:
  id, question, expected_doc_ids[], knowledge_layer, difficulty
```

| Difficulty | Count | Example |
|------------|-------|---------|
| Easy | 15 | Exact title lookup |
| Medium | 25 | Concept in single doc |
| Hard | 10 | Multi-doc synthesis |

### 4.2 RAG metrics & gates

| Metric | Formula | MVP gate | Phase 2 target |
|--------|---------|----------|----------------|
| Recall@5 | correct in top 5 | ≥ 70% | ≥ 80% |
| MRR | mean reciprocal rank | ≥ 0.55 | ≥ 0.65 |
| Citation accuracy | manual sample 20 | ≥ 80% | ≥ 90% |
| Faithfulness | LLM-judge + human | ≥ 75% | ≥ 85% |
| Latency p95 | seconds | ≤ 10 | ≤ 6 |

### 4.3 Review evaluation

| Test | Method | Gate |
|------|--------|------|
| Omission detection | 10 docs with known missing sections | ≥ 75% |
| False positive rate | 10 clean docs | ≤ 20% flagged critical |
| Compliance catch | 5 docs vs known policy gaps | ≥ 70% |

### 4.4 Generation evaluation

| Test | Method | Gate |
|------|--------|------|
| Template completeness | All required sections filled | 100% |
| Minor edit rate | Curator review 10 outputs | ≥ 60% |
| Citation presence | Automated check | ≥ 90% have ≥2 cites |

---

## 5. Security Test Cases

| ID | Test | Expected |
|----|------|----------|
| SEC-01 | User cannot access restricted doc API | 403 |
| SEC-02 | RAG excludes confidential for standard user | No chunks |
| SEC-03 | SQL injection on search | Sanitized |
| SEC-04 | JWT expired | 401 |
| SEC-05 | Audit log append-only | UPDATE fails |
| SEC-06 | File upload .exe rejected | 400 |

---

## 6. UAT Scenarios (Sprint 6)

| # | Scenario | Roles |
|---|----------|-------|
| UAT-01 | Upload and index document | User |
| UAT-02 | Search with citations | User |
| UAT-03 | Full document review export | Reviewer |
| UAT-04 | Create proposal from template | User |
| UAT-05 | Assistant primary workflow | User |

---

## 7. Test Environments

| Env | Data | Purpose |
|-----|------|---------|
| Local | Synthetic | Dev |
| CI | Fixtures | Automated |
| Staging | Anonymized subset | Integration, demos |
| Pilot | Production corpus | UAT, MOV-010 |

---

## 8. Risks

| Risk | Mitigation |
|------|------------|
| AI eval fl flaky | Fixed seed; version lock model |
| No ground truth | Curator labels eval set in Phase 0 |
| UAT skipped | Mandatory for M6 sign-off |

---

## Related Documents

- [MOV-009](../07-movements/MOV-009-build-mvp-phase1.md)
- [DOC-403 RAG Architecture](../05-ai/DOC-403-rag-architecture.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-29 | Initial testing strategy |
