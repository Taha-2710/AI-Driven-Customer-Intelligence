# 🤖 AI-Driven Customer Intelligence Dashboard

**HuggingFace · Python · Power BI · DAX · pandas**

> ⚡ **[$2.7M revenue at risk identified · 4,902 hidden churners detected · 158K records analysed]**

📊 **[View Live Dashboard](https://app.powerbi.com/links/HdwtPN2UKo?ctid=a63ade61-7bd6-415a-9dca-45db107b9972&pbi_source=linkShare&bookmarkGuid=0a049634-97bb-441f-aa72-7fe63f0cf3de)** · 👤 **[LinkedIn](https://linkedin.com/in/mohd-taha-ahmad-0772b5167)**

---

!![Uploading Executive Overview.png…]()

> *Executive Overview — Revenue vs Sentiment scatter · AI Health Score by category · $2.7M risk mapped*

---

## The Problem

**Star ratings are lying to businesses.**

4,902 customers gave 4–5 stars but wrote negative reviews — silent churners completely invisible to traditional rating-based monitoring. Businesses making decisions from star ratings alone are missing their most at-risk customers entirely.

This project was built to find them.

---

## Impact at a Glance

| Metric | Result |
|--------|--------|
| 💰 Revenue at Risk Identified | **$2.7M across 65 product categories** |
| 🔍 Hidden Churners Detected | **4,902 customers invisible to star-rating monitoring** |
| 📋 Reviews Analysed | **95,159 Brazilian Portuguese reviews** |
| 🏷️ Complaints AI-Classified | **40K+ reviews → 5 root-cause complaint types** |
| 🎯 Top Recovery Opportunity | **$88K — Beauty & Health (Health Score: 18 → 60)** |

---

## What This Project Does

An end-to-end AI analytics pipeline — from raw CSV data through transformer-based NLP to an interactive executive dashboard — answering four business questions:

- **What are the main drivers of customer complaints?**
- **Which categories are impacting revenue the most?**
- **Where is the hidden churn risk?**
- **What actions can improve customer health and protect revenue?**

---

## Architecture

```
Raw Data (5 CSVs · 158K rows)
        ↓
Data Engineering — pandas merge · cleaning · feature engineering
        ↓
AI Sentiment Analysis — HuggingFace pysentimiento (Brazilian Portuguese native)
        ↓
Complaint Classification — Zero-shot mDeBERTa-v3 (no labelled data required)
        ↓
Mismatch Detection — AI sentiment vs star rating cross-validation
        ↓
Health Score Engine — composite metric (sentiment + rating + complaints + volume)
        ↓
Power BI Dashboard — 5-page interactive report · DAX measures · executive storytelling
```

---

## AI Models

### Sentiment Analysis
| Property | Detail |
|----------|--------|
| Model | `pysentimiento/bertweet-pt-sentiment` |
| Language | Brazilian Portuguese — native, no translation |
| Classes | POS · NEU · NEG |
| F1 Score | 0.74 (positive and negative classes) |

**Why native Portuguese?** Translation before sentiment analysis introduces quality loss. Using a Portuguese-native model preserves linguistic nuance in reviews — especially negations and colloquialisms that translation models frequently distort.

### Complaint Classification
| Property | Detail |
|----------|--------|
| Model | `MoritzLaurer/mDeBERTa-v3-base-xnli-multilingual-nli-2mil7` |
| Type | Zero-shot — no labelled training data required |
| Classes | Delivery · Quality · Wrong Item · Pricing · Service |
| Reviews Classified | 40,000+ negative reviews |

---

## Custom Business Metrics

### AI Health Score (0–100)

```python
Health Score = (
    (avg_sentiment + 1) / 2  × 0.35   # Sentiment signal
  + avg_rating / 5           × 0.35   # Star rating anchor
  + (1 - negative_rate)      × 0.10   # Low complaint penalty
  + complaint_count / max    × 0.20   # Volume weighting
) × 100
```

Categories scoring below 40 are flagged as critical. Categories above 70 are prioritised for scaling.

### Revenue Recovery Formula

```
Recovery = Revenue At Risk × (Target Score − Current Score) / (100 − Current Score)
```

**Example — Beauty & Health:**
- Current risk: $172K (Health Score: 18)
- Target score: 60
- Estimated recovery: **$88K protected**

---

## Key Findings

**Wrong-item fulfilment (31%) and delivery failures are the primary churn catalysts** — not product quality. This means operational fixes (logistics, warehouse accuracy) drive more revenue recovery than product changes.

**Top 3 Priority Categories:**

| Category | Health Score | Revenue at Risk | Primary Action |
|----------|-------------|-----------------|----------------|
| Beauty & Health | 18 — Critical 🔴 | $172K | Supplier quality audit |
| Computer Accessories | 34 — At Risk 🟡 | $300K | SLA enforcement |
| Bed & Bath | 52 — Watch 🟡 | $1.3M | Scale what works |

---

## Dashboard Pages

| Page | Title | Key Visuals |
|------|-------|-------------|
| 1 | Executive Overview | Revenue vs sentiment scatter · health score bar chart |
| 2 | Sentiment Intelligence | Trend line · heatmap · mismatch analysis |
| 3 | Complaint Intelligence | AI complaint matrix · revenue at risk by category |
| 4 | Strategic Recommendations | 4 priority cards · 8-point action roadmap |
| 5 | Methodology & Validation | Formula derivation · confusion matrix · F1 proof |

📊 **[View Live Dashboard →](https://app.powerbi.com/links/HdwtPN2UKo?ctid=a63ade61-7bd6-415a-9dca-45db107b9972&pbi_source=linkShare&bookmarkGuid=0a049634-97bb-441f-aa72-7fe63f0cf3de)**

---

## Model Validation

| Metric | Value | Status |
|--------|-------|--------|
| F1 Score (Weighted) | 0.692 | Good ✅ |
| Overall Accuracy | 63.5% | Good ✅ |
| Positive Class F1 | 0.74 | Strong ✅ |
| Negative Class F1 | 0.74 | Strong ✅ |
| Neutral Class F1 | 0.23 | Weak ⚠️ |
| Reviews Validated | 95,159 | Large sample ✅ |

**Documented limitation:** Neutral class F1 = 0.23 — expected behaviour in multilingual zero-shot NLP. Business-critical positive and negative detection both achieve F1 = 0.74. Star ratings are used as a safety net for borderline neutral predictions. This limitation is intentionally documented rather than hidden.

---

## Project Structure

```
ai_customer_intelligence/
│
├── notebooks/
│   ├── 01_data_preparation.ipynb          # Merge + clean 5 CSVs · 158K rows
│   ├── 02_sentiment_analysis.ipynb        # HuggingFace NLP pipeline
│   ├── 03_complaint_classification.ipynb  # Zero-shot classification
│   └── 04_export_for_powerbi.ipynb        # 3 export tables for dashboard
│
├── output/
│   ├── sales_sentiment.csv
│   ├── complaint_analysis.csv
│   ├── category_health.csv
│   ├── mismatch_summary.csv
│   ├── validation_metrics.csv
│   └── confusion_matrix.png
│
├── dashboard/
│   ├── AI_Customer_Intelligence.pbix
│   └── screenshots/
│       ├── executive_overview.png
│       ├── sentiment_intelligence.png
│       ├── complaint_intelligence.png
│       └── recommendations.png
│
└── README.md
```

---

## Tech Stack

```
Language:      Python 3.10
NLP:           HuggingFace Transformers · pysentimiento · mDeBERTa-v3
Data:          pandas · numpy
Validation:    scikit-learn (F1, confusion matrix)
Visualisation: Power BI · DAX
Dataset:       Olist Brazilian E-Commerce — Kaggle (158K rows · Sep 2016–Aug 2018)
```

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/Taha-2710/AI-Driven-Customer-Intelligence

# 2. Install dependencies
pip install transformers pysentimiento pandas numpy scikit-learn

# 3. Run notebooks in order
# Start with 01_data_preparation.ipynb
# Dataset: download Olist from Kaggle and place CSVs in /data folder

# 4. Open dashboard
# Load AI_Customer_Intelligence.pbix in Power BI Desktop
# Connect to the CSV outputs from step 3
```

---

## About

**Mohd Taha Ahmad** — Data Analyst · Lucknow, India

I build analytics systems that surface what numbers alone miss — hidden revenue risk, silent churn signals, and customer patterns buried in unstructured data.

[LinkedIn](https://linkedin.com/in/mohd-taha-ahmad-0772b5167) · [GitHub](https://github.com/Taha-2710) · [SaaS Churn Project →](https://github.com/Taha-2710/saas-churn-revenue-analysis)
