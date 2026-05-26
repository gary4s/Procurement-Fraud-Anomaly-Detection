# Proactive Procurement Fraud Detection using Unsupervised Machine Learning

## 📌 Project Overview
This repository contains an end-to-end unsupervised machine learning pipeline designed to proactively identify anomalous procurement transactions. By leveraging advanced data analytics, this project shifts the traditional counter-fraud paradigm from reactive investigation to proactive, automated risk triage.

In organizational procurement, malicious fraud (e.g., split-invoicing, price-gouging, phantom vendors) and high-cost administrative anomalies are rare compared to the vast volume of legitimate daily transactions. Because historical ground-truth fraud labels are often unavailable or highly confidential, this pipeline utilizes **unsupervised anomaly detection** to surface high-risk exceptions for human audit.

## 📊 Data Source & Context

### Procurement and Payroll Fraud Dataset (Synthetic)
* **Author:** Ramadhan Ridho Arrohman (Kaggle)
* **Type:** Artificially Generated / Synthetic

#### 🧾 Overview
This project utilizes a synthetic dataset explicitly designed for educational, research, and experimental applications within fraud detection frameworks. The data simulates organizational financial workflows, closely mimicking real-world transactional behaviors and risk typologies such as vendor manipulation, inflated invoicing structures, ghost employee profiles, and irregular payment frequency distributions.

> ⚠️ **Important Note:** This dataset does not contain real, classified, or sensitive proprietary data. All records are artificially generated and intended solely for controlled machine learning experimentation, practice, and portfolio development.

#### 🎯 Educational Purpose & Alignment
In counter-fraud data science, access to production transactional registries is heavily restricted due to privacy laws and operational security. This dataset serves as a high-fidelity proxy to:
* Safely dissect and isolate complex fraud patterns in procurement structures.
* Practice unsupervised feature engineering, statistical anomaly detection, and cluster analysis.
* Prototype end-to-end detection models that can be adapted to authentic organizational schemas under secure environments.

## 🎯 Core Objectives
* **Procurement Protection:** Targets vulnerability points where organizational funds are disbursed to external suppliers and contractors.
* **Proactive Threat Triage:** Generates automated anomaly intelligence reports, allowing internal audit and compliance teams to optimize investigative resources.
* **Loss Prevention:** Flags financial leakage points, ensuring resources are protected and spent efficiently.

---

## 🏗️ Technical Architecture & Pipeline

The pipeline processes financial datasets through a four-stage unsupervised workflow:

```
[ Raw Procurement Data ]
│
▼
[ Feature Engineering ] ──► (Price Variance, Vendor Inflation, Density)
│
▼
[ Isolation Forest ]     ──► (Global Outlier Detection & Anomaly Scoring)
│
▼
[ K-Means Clustering ]   ──► (Behavioral Risk Profiling for Investigators)

```
1.  **Ingestion & Data Cleansing:** Ingests relational transactional data, stripping out system flags, rule-based indicators, and target labels to preserve a strictly unsupervised learning environment.
2.  **Behavioral Feature Engineering:** Transforms static transactional values into behavioral risk indicators:
    * **Price Variance Percentage:** Deviations between the system's expected item cost and the actual invoice amount.
    * **Vendor Price Inflation:** Outliers calculating an invoice price against a specific supplier's historical median billing rate.
    * **Employee-Vendor Density:** Tracking transaction frequencies between specific internal staff and external vendors to surface potential conflicts of interest.
3.  **Isolation Forest Isolation:** Leverages an ensemble of isolation trees to isolate anomalous transactions based on structural feature space distances rather than profiling normal activity.
4.  **K-Means Behavioral Profiling:** Clusters identified anomalies to group them into distinct risk typologies (e.g., systemic billing errors vs. high-velocity split invoicing).

---

## 📊 Evaluation & Methodology

While built as an unsupervised tool, the pipeline is evaluated using a hidden baseline dataset to understand its precision and operational dynamics:

* **High Precision Baseline:** Initial strict contamination benchmarks ($1\%$) yielded a **100% Precision Rate**, ensuring that every transaction surfaced was a verified high-profile exception—minimizing "alarm fatigue" for audit and compliance teams.
* **Dynamic Contamination Tuning:** The implementation demonstrates how adjusting the model's contamination parameters scales recall, capturing subtle, distributed fraud schemes that closely mimic standard business activities.

---

## 🛠️ Tech Stack & Dependencies

* **Language:** Python 3.10+
* **Data Wrangling:** `pandas`, `numpy`
* **Machine Learning:** `scikit-learn` (Ensemble Methods, Clustering)
* **Visualization:** `matplotlib`, `seaborn`

---
