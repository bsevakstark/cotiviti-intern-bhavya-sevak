# ML Pattern Recognition on GWAS/mQTL Data for Cancer Risk Prediction
### Cotiviti Intern Assessment — Bhavya Sevak | Arizona State University | June 2026

---

## Topic
**Topic 2: Clinical Decision Making and Pattern Recognition in Health Care**

An end-to-end two-layer agentic pipeline for cancer risk prediction — combining a GWAS/mQTL machine learning classifier with an autonomous LLM TPO router that triggers Treatment, Payment, and Operations actions without manual review.

---

## Repository Contents

| File | Description |
|------|-------------|
| `cotiviti_report_final.docx` | Two-page written report + APA bibliography (Word) |
| `cotiviti_slides_v2.pptx` | 9-slide PowerPoint presentation |
| `cotiviti_poc_agentic.ipynb` | Jupyter notebook — full two-layer agentic pipeline |
| `README.md` | This file |

> Video recording submitted separately per assessment instructions.

---

## Architecture

```
[Patient Clinical Profile]
         │
         ▼
┌─────────────────────────┐
│  Layer 1: XGBoost       │  ← GWAS/mQTL ML pipeline
│  Cancer Risk Classifier │    CV AUC: 0.861
└─────────────────────────┘
         │  High Risk Detected?
         ▼
┌─────────────────────────┐
│  Layer 2: Agentic LLM   │  ← Llama 3.3 via Groq API
│  TPO Router             │    Autonomous clinical reasoning
└─────────────────────────┘
         │
         ▼
  [Structured JSON Action]
  Treatment / Payment / Operations
```

---

## Proof of Concept — Quick Start

### Requirements

```bash
pip install numpy pandas scikit-learn xgboost groq
```

### Run in Google Colab

1. Upload `cotiviti_poc_agentic.ipynb` to [colab.research.google.com](https://colab.research.google.com)
2. Get a free Groq API key at [console.groq.com](https://console.groq.com)
3. Paste your key into cell 9: `GROQ_API_KEY = "your_key_here"`
4. Runtime → Run All

### Pipeline Steps

| Step | Description | Technology |
|------|-------------|------------|
| 1 | Simulate GWAS dataset | 1,000 samples × 5,000 SNPs, Hardy-Weinberg equilibrium |
| 2 | mQTL feature engineering | Beta-value methylation interaction scores |
| 3 | Feature selection | Chi-squared (5,000→500) + LASSO (→~47 SNPs) |
| 4 | XGBoost classifier | Gradient-boosted trees, 5-fold cross-validation |
| 5 | PRS calibration | Isotonic regression, risk tier assignment |
| 6 | Agentic LLM router | Llama 3.3 via Groq — autonomous TPO action routing |

### Key Results

| Metric | Value |
|--------|-------|
| Cross-validated AUC | 0.861 ± 0.010 |
| SNPs selected (LASSO) | ~47 of 5,000 |
| Runtime | < 30 seconds (CPU) |
| Agentic actions | Treatment / Payment / Operations |

---

## Agentic TPO Actions

The Layer 2 LLM router autonomously selects from:

| Action | Trigger |
|--------|---------|
| `TRIGGER_PRE_AUTHORIZATION` | High/Very High risk + no recent screening |
| `APPROVE_EARLY_SCREENING` | High risk + age or ancestry flags |
| `ESCALATE_TO_ONCOLOGY` | Very High risk + family history |
| `OPTIMIZE_BILLING_CODE` | Any tier — assigns CPT 81479 / ICD-10 Z80.0 |
| `ROUTINE_MONITORING` | Low/Intermediate risk |

Output is structured JSON — ready to plug into FHIR CDS Hooks, payer dashboards, or pre-authorization workflows.

---

## Report Summary

**Trends:** Genomic foundation models (Nucleotide Transformer, 62B params), multi-omics integration at scale (UK Biobank 500K+), FDA SaMD + CMS CPT 81479 reimbursement momentum.

**Strategic Recommendations:**
- **Option A (6-12 months):** GWAS-PRS Risk Stratification API — ancestry-calibrated microservice plugging into existing Cotiviti care management portals
- **Option B (18-36 months):** mQTL-Informed Agentic CDS — FHIR hooks in EHR workflows via biobank partnerships (Sangre Por Salud, NIH All of Us)

---

## Author

**Bhavya Sevak**
M.S. Biomedical Informatics Candidate (Expected 2026)
Arizona State University
[brsevak1504@gmail.com](mailto:brsevak1504@gmail.com) | [GitHub](https://github.com/bsevakstark) | [Portfolio](https://bsevakstark.github.io)

---

*Submitted for the Cotiviti Intern Assessment — Generative AI / Agentic AI / Research. All data is synthetic. Not clinically validated.*
