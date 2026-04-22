# 🤖 AI-Driven Customer Intelligence Dashboard
### HuggingFace · Python · Power BI · DAX · pandas

> **An end-to-end AI-powered analytics project** that goes beyond traditional dashboards —
> combining transformer-based NLP, zero-shot classification, and custom business metrics
> to identify $2.7M in revenue at risk across 20 product categories.

[![Python](https://img.shields.io/badge/Python-3.10-yellow?style=for-the-badge&logo=python)](https://python.org)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-orange?style=for-the-badge&logo=powerbi)]
[![HuggingFace](https://img.shields.io/badge/HuggingFace-NLP-red?style=for-the-badge)](https://huggingface.co)

---
## 📌 The Problem

Star ratings are lying to businesses.

**4,902 customers gave 4–5 stars but wrote negative text** — silent churners completely
invisible to traditional rating-based monitoring. This project was built to find them.

---
## 🎯 Objective

To answer critical business questions:

What are the main drivers of customer complaints?
Which categories are impacting revenue the most?
Where is the hidden churn risk?
What actions can improve customer health and protect revenue?

---

## 🔍 What This Project Does

| Layer | What Was Built | Tool |
|---|---|---|
| **Data Engineering** | Merged 5 Olist CSVs · cleaned 158K rows · feature engineering | pandas |
| **AI Sentiment** | Sentiment scored 95,159 Brazilian Portuguese reviews | HuggingFace pysentimiento |
| **Complaint Classification** | Zero-shot classified negatives into 5 complaint types | MoritzLaurer/mDeBERTa-v3-base-xnli-multilingual-nli-2mil7 |
| **Health Score** | Custom composite metric — sentiment + rating + complaints + volume | Python · Power BI |
| **Mismatch Detection** | Cross-validated AI labels vs star ratings to find hidden dissatisfaction | Python |
| **Validation** | F1 score + confusion matrix against 95,159 ground truth labels | scikit-learn |
| **Dashboard** | 5-page interactive Power BI report with DAX measures | Power BI · DAX |

---

## 📊 Key Findings

```
95,159  reviews analyzed across 20 product categories
4,902  hidden dissatisfied customers detected
$2.7M  revenue identified as at risk
40K   complaints AI-classified into 5 categories
18   → 60 health score target for Beauty & Health
$88K  estimated revenue recovery for top priority category
```

---

## 🧠 AI Models Used

**Sentiment Analysis**
```
Model:    pysentimiento/bertweet-pt-sentiment
Language: Brazilian Portuguese (native — no translation)
Classes:  POS · NEU · NEG
Result:   F1 = 0.74 on positive and negative classes
```

**Complaint Classification**
```
Model:    MoritzLaurer/mDeBERTa-v3-base-xnli-multilingual-nli-2mil7
Type:     Zero-shot — no labelled training data required
Classes:  Delivery · Quality · Wrong Item · Pricing · Service
```

---

## 📐 Custom Metrics

### AI Health Score (0–100)
```
Health Score = (
    (avg_sentiment + 1) / 2  × 0.35  +   # Sentiment signal
    avg_rating / 5           × 0.35  +   # Star rating
    (1 - negative_rate)      × 0.10  +   # Low complaint penalty
    complaint_count / max    × 0.20       # Volume weighting
) × 100  →  Normalized 0–100
```

### Revenue Recovery Formula
```
Recovery = Revenue At Risk × (Target HS − Current HS) / (100-Current HS)

Example — Beauty & Health:
  Current risk:  $172K  (health score 18)
  Target score:  60
  Recovery:      $172K × (60−18)/(100-18) = $88K protected
```

---

## 🗂️ Dashboard Pages

| Page | Title | Key Visual |
|---|---|---|
| 1 | Executive Overview | Revenue vs sentiment scatter · health score bar |
<img width="1297" height="731" alt="Executive Overview" src="https://github.com/user-attachments/assets/68551699-9415-4682-b195-3cb3a5a42150" />

| 2 | Sentiment Intelligence | Trend line · heatmap · mismatch analysis |
<img width="1300" height="732" alt="Sentiment Intelligence" src="https://github.com/user-attachments/assets/adf9ed62-c45f-4ff3-86bb-a12394af5427" />

| 3 | Complaint Intelligence | AI complaint matrix · revenue at risk |
<img width="1302" height="736" alt="Complaint Intelligence" src="https://github.com/user-attachments/assets/9109df75-f427-40a8-85e3-5f86bfb2d73f" />

| 4 | Strategic Recommendations | 4 priority cards · 8-point roadmap |
<img width="1281" height="725" alt="Recommendations" src="https://github.com/user-attachments/assets/ee11aff4-1f4b-4ebc-a701-53dc96b2cb8a" />

| 5 | Methodology & Validation | Formula derivation · confusion matrix · F1 proof |
<img width="1281" height="722" alt="Methodology" src="https://github.com/user-attachments/assets/6e231c8b-b5a9-4283-b609-6f6345790103" />


👉 **[View Live Dashboard](https://app.powerbi.com/links/HdwtPN2UKo?ctid=a63ade61-7bd6-415a-9dca-45db107b9972&pbi_source=linkShare&bookmarkGuid=0a049634-97bb-441f-aa72-7fe63f0cf3de)**

---

## ✅ Model Validation

| Metric | Value | Status |
|---|---|---|
| F1 Score (Weighted) | 0.692 | Good |
| Overall Accuracy | 63.5% | Good |
| Positive Class F1 | 0.74 | Strong ✅ |
| Negative Class F1 | 0.74 | Strong ✅ |
| Neutral Class F1 | 0.23 | Weak ⚠️ |
| Reviews Validated | 95,159 | Large sample |

> ⚠️ **Documented Limitation:** Neutral class F1 = 0.23 — expected in multilingual NLP.
> Business-critical positive and negative detection both achieve F1 = 0.74.
> Star ratings used as safety net for borderline predictions.

---

## 📁 Project Structure

```
ai_customer_intelligence/
│
├── notebooks/
│   ├── 01_data_preparation.ipynb        # Merge + clean 5 CSVs
│   ├── 02_sentiment_analysis.ipynb      # HuggingFace pipeline
│   ├── 03_complaint_classification.ipynb # Zero-shot NLP
│   └── 04_export_for_powerbi.ipynb      # 3 export tables
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
│   └── AI_Customer_Intelligence.pbix
│
└── README.md
```

---

## 🛠️ Tech Stack

```
Language:      Python 3.10
NLP:           HuggingFace Transformers · pysentimiento · MoritzLaurer/mDeBERTa-v3-base-xnli-multilingual-nli-2mil7
Data:          pandas · numpy
Validation:    scikit-learn
Visualization: Power BI · DAX
Dataset:       Olist Brazilian E-Commerce (Kaggle · 158K rows)
Period:        Sep 2016 – Aug 2018
```

---

## 👤 About

**Mohd Taha Ahmad** — Data Analyst open to opportunities

Focused on AI-augmented analytics — combining NLP, business intelligence,
and data storytelling to turn raw data into decisions.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/mohd-taha-ahmad-0772b5167/)

(https://app.powerbi.com/links/HdwtPN2UKo?ctid=a63ade61-7bd6-415a-9dca-45db107b9972&pbi_source=linkShare&bookmarkGuid=0a049634-97bb-441f-aa72-7fe63f0cf3de)

---

*Dataset: Olist Public Dataset (Kaggle) · Analysis Period: Sep 2016 – Aug 2018*
