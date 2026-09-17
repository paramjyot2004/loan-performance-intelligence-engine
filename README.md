# LoanLens — Loan Performance Intelligence Engine

> **AI-powered loan performance intelligence for risk prediction, loan-state monitoring, anomaly detection, scenario simulation, explainability, and grounded LLM-assisted review.**

**Intain FinTech Challenge 2026 — AI Track | Top 20 Finalist**

🔗 **Live Demo:** https://loan-intelligence-engine.streamlit.app/  
🔗 **GitHub:** https://github.com/paramjyot2004/loan-performance-intelligence-engine

---

## Overview

**LoanLens** is an AI-driven Loan Performance Intelligence Engine that analyzes loan-level data and provides a structured view of loan risk and performance.

The system combines machine learning, time-based loan analysis, anomaly detection, scenario simulation, explainability, and a grounded Gemini reviewer layer.

### Core Principle

> **ML makes the prediction. Gemini explains the prediction. A human makes the final decision.**

Gemini is **not** used to predict loan default. The ML pipeline first generates structured evidence such as predicted risk, confidence, feature drivers, and anomaly status. Gemini then converts this evidence into a concise reviewer-friendly explanation.

---

## Key Features

| Area | Capabilities |
|---|---|
| **Data Intelligence** | Data profiling, cleaning, missing-value handling, and feature engineering |
| **Risk Prediction** | Random Forest default-risk prediction with time-aware validation |
| **Loan Dynamics** | Monthly loan-state transition analysis |
| **Monitoring** | Isolation Forest anomaly detection |
| **What-if Analysis** | Adverse-credit and high-prepayment scenario simulation |
| **Explainability** | Feature importance and loan-level risk drivers |
| **GenAI Reviewer** | Grounded Gemini explanations based on actual ML outputs |
| **Responsible AI** | Stress testing, fairness screening, prompt logging, and human-in-the-loop review |

---

## System Architecture

```text
                         ┌──────────────────┐
                         │   Loan Dataset   │
                         └────────┬─────────┘
                                  │
                                  ▼
                    ┌──────────────────────────┐
                    │ Profiling & Data Cleaning│
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │ Feature Engineering      │
                    │ 19 Model Features        │
                    └────────────┬─────────────┘
                                 │
             ┌───────────────────┼───────────────────┐
             │                   │                   │
             ▼                   ▼                   ▼
      ┌──────────────┐   ┌──────────────┐   ┌────────────────┐
      │ Default Risk │   │  Transition  │   │    Anomaly     │
      │ Random Forest│   │    Model     │   │ IsolationForest│
      └──────┬───────┘   └──────┬───────┘   └───────┬────────┘
             │                   │                   │
             └───────────────────┼───────────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │ Explainability &         │
                    │ Scenario Simulation      │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │ Structured Model Evidence│
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │ Gemini Grounded Reviewer │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │     Human Reviewer       │
                    └──────────────────────────┘
```

---

## Key Results

| Metric | Result |
|---|---:|
| Records processed | 16,889 |
| Features used | 19 |
| ROC-AUC | 0.600 |
| Anomalies detected | 507 (~3%) |
| Transition accuracy | 90.9% |
| Naive baseline | 89.5% |
| Test predictions | 4,246 |

> **Prototype results on synthetic practice data.**

---

## Screenshots

### Dashboard

![LoanLens Dashboard](assets/dashboard.png)

### Explainability

![LoanLens Explainability](assets/explainability.png)

---

## Limitations

- Evaluated on synthetic practice data.
- ROC-AUC of 0.600 is not production-ready performance.
- Feature importance indicates model contribution, not causation.
- Anomaly detection identifies unusual records, not fraud.
- Fairness analysis is an initial screening, not a formal audit.
- Gemini explains model outputs and does not make lending decisions.

---
