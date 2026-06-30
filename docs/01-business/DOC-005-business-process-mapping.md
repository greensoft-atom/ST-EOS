# DOC-005 — Business Process Mapping (MSTI Pilot)

**Document ID:** DOC-005  
**Version:** 1.0  
**Date:** 2026-06-30  
**Status:** AS-IS baselines for planning — validate in MOV-001 workshops  
**Pilot:** [DOC-PILOT-001](./DOC-PILOT-001-government-executive-pilot-scope.md)

---

## 1. Purpose

Document **AS-IS** and **TO-BE** process flows for the three official MSTI pilot workflows (W1–W3). Provides time baselines for MOV-010 measurement.

---

## 2. W1 — Grant / Program Submission Pre-Screening

**Owner:** Research Programs Department  
**Volume (typical):** 50–200 submissions per major call  
**ST-EOS features:** Document Review + Evaluation pre-score

### 2.1 AS-IS process

```text
Applicant submits PDF ──▶ Officer receives email/DMS copy
        │
        ▼
Manual checklist review (completeness, format, eligibility)
        │  4–8 hours per 50-page proposal
        ▼
Pass/Fail note to committee ──▶ Filing in spreadsheet
```

| Step | Actor | Avg time | Pain points |
|------|-------|----------|-------------|
| Receive & log | Program officer | 30 min | Multiple formats, missing sections |
| Checklist review | Program officer | 3–7 hrs | Repetitive, inconsistent |
| Policy cross-check | Senior officer | 1–2 hrs | Manual search in policy PDFs |
| Record decision | Program officer | 30 min | Duplicate data entry |

**AS-IS total:** **4–8 hours** per submission (planning baseline: **6 hours**)

### 2.2 TO-BE process (ST-EOS)

```text
Upload to ST-EOS (RST class) ──▶ AI Document Review (4 types)
        │
        ▼
Officer reviews findings (30–60 min) ──▶ Mark "Proceed to evaluation"
        │
        ▼
Optional rubric pre-score ──▶ Committee queue
```

**TO-BE target:** **2–3 hours** (−50%)

---

## 3. W2 — Committee Evaluation Scoring

**Owner:** Evaluation Committee secretariat  
**Volume:** Batches of 15–25 submissions per meeting  
**ST-EOS features:** Evaluation Assistant (full)

### 3.1 AS-IS process

```text
Committee packet assembled manually
        │
        ▼
Each evaluator reads independently (3–5 days for batch of 20)
        │
        ▼
Meeting: discuss, score, reconcile differences
        │
        ▼
Secretariat consolidates scores in spreadsheet ──▶ Report to DG
```

| Step | Actor | Avg time (batch of 20) | Pain points |
|------|-------|------------------------|-------------|
| Packet preparation | Secretariat | 2–3 days | Copy-paste, formatting |
| Individual reading | Each evaluator | 2–4 hrs × N | Inconsistent notes |
| Scoring reconciliation | Chair + secretariat | 1 day | Criteria drift |
| Final report | Secretariat | 4–8 hrs | Manual compilation |

**AS-IS committee prep:** **3–5 days** before meeting (planning baseline: **4 days**)

### 3.2 TO-BE process (ST-EOS)

```text
Select rubric + submissions (batch ≤ 20) ──▶ AI rubric scoring + evidence
        │
        ▼
Comparison matrix + ranked list ──▶ Reviewers edit scores
        │
        ▼
Chair approves ──▶ Export committee packet (PDF/DOCX)
```

**TO-BE target:** **2–3 days** (−30%)

---

## 4. W3 — Annual S&T Plan / Report Section Drafting

**Owner:** Strategic Planning Department  
**Volume:** 4–8 major sections per annual cycle  
**ST-EOS features:** RAG Search + Template Creation

### 4.1 AS-IS process

```text
Officer gathers past plans, policies, statistics manually
        │
        ▼
Draft section from scratch in Word (2–5 days per section)
        │
        ▼
Internal review cycles (2–3 rounds)
```

| Step | Actor | Avg time | Pain points |
|------|-------|----------|-------------|
| Archive search | Planning officer | 4–8 hrs | Scattered PDFs |
| First draft | Planning officer | 2–4 days | Blank page, inconsistent structure |
| Citation / refs | Planning officer | 2–4 hrs | Manual |

**AS-IS first draft:** **2–5 days** per section (baseline: **3 days**)

### 4.2 TO-BE process (ST-EOS)

```text
RAG search (policies + past plans) ──▶ Select plan section template
        │
        ▼
AI draft with citations ──▶ Officer edit (1–2 days)
        │
        ▼
Export for internal review
```

**TO-BE target:** **1–2 days** first draft (−40%)

---

## 5. Process / System Touchpoints

| Workflow | MVP modules | Roles (DOC-307) |
|----------|-------------|-----------------|
| W1 | Review, optional Eval | program_officer |
| W2 | Evaluation Assistant | program_officer, committee_reviewer, committee_chair |
| W3 | Search, Create | user, curator |

---

## 6. Workshop Validation Checklist (MOV-001)

- [ ] Confirm AS-IS times with 2+ officers per workflow
- [ ] Confirm submission formats (PDF primary; DOCX count?)
- [ ] Confirm rubrics available for digitization (≥ 2)
- [ ] Confirm RESTRICTED handling for grant submissions
- [ ] Record TO-BE acceptance criteria with pilot champion

---

## Related Documents

- [DOC-PILOT-001 §6](./DOC-PILOT-001-government-executive-pilot-scope.md)
- [DOC-504 Evaluation Assistant](../06-modules/DOC-504-evaluation-assistant.md)
- [MOV-010 Pilot Deployment](../07-movements/MOV-010-pilot-deployment.md)

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-06-30 | Initial AS-IS/TO-BE for W1–W3 |
