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

## Results

```
--- Calssification Report ---
              precision    recall  f1-score   support

           0       0.69      1.00      0.82       191
           1       1.00      0.03      0.07        87

    accuracy                           0.70       278
   macro avg       0.85      0.52      0.44       278
weighted avg       0.79      0.70      0.58       278
```
---
### 🔄 Optimization: Dynamic Contamination Tuning

The initial proof-of-concept utilized a highly restrictive contamination factor ($\alpha = 0.01$). While this baseline achieved a **100% Precision Rate**—ensuring zero false alarms for the audit team—the model suffered from high false negatives, capturing only a fraction of the total embedded risk due to the strict threshold ceiling. 

To transition the pipeline from an extreme outlier detector to a comprehensive risk triage system, the Isolation Forest was retrained with a **10% contamination factor**. This adjustment widened the detection envelope, dynamically scaling the model's recall to surface complex, distributed anomalies that closely mimic legitimate standard business activities.
```
--- Updated Confusion Matrix (10% contamination) ---
[[191   0]
 [ 59  28]]
--- Updated classification report ----
              precision    recall  f1-score   support

           0       0.76      1.00      0.87       191
           1       1.00      0.32      0.49        87

    accuracy                           0.79       278
   macro avg       0.88      0.66      0.68       278
weighted avg       0.84      0.79      0.75       278

```

### 👥 Behavioral Profiling via K-Means Clustering

Once the pipeline identifies high-risk anomalies, it passes the feature matrix to a **K-Means Clustering** algorithm ($k=3$). Rather than forcing investigators to manually parse a flat, undifferentiated list of alerts, K-Means mathematically groups anomalies based on shared behavioral signatures.

This hybrid approach transforms raw statistical outliers into actionable risk typologies. Instead of asking "Is this transaction fraudulent?", compliance and internal audit teams can ask "Which specific risk pattern does this anomaly represent?", allowing organizations to deploy specialized investigative resources more efficiently.
```
#rerun the isolation forest to catch more fraud cases, increasing the contamination

--- Breakdown of Fraud flags accross 3 behaviour clusters ---
fraud_flag          0   1
behaviour_cluster        
0                  46  26
1                  74  24
2                  71  37

```

### 🔍 Empirical Cluster Definitions & Risk Profiles

Based on feature aggregation across the trained K-Means clusters, the dataset naturally partitions into three distinct operational risk typologies:

1. **Cluster 0: Systemic Price Variance Exception (36% Fraud Density)**
   * **Characteristics:** Highest average system price variance (21%) and severe expected price differentials (~£550k), with a deeply negative vendor deviation.
   * **Audit Focus:** Flagged for administrative or systemic pricing misalignment between system contract baselines and actual invoices.

2. **Cluster 1: High-Value Macro Price Escalation (24% Fraud Density)**
   * **Characteristics:** Highest absolute transaction values (~£8.19M) paired with an extreme positive vendor deviation (~+£2.99M) relative to the supplier's historical baseline.
   * **Audit Focus:** High-risk financial exposure. Flagged for massive, high-magnitude spend and sudden supplier price inflation.

3. **Cluster 2: High-Value Concentration & Density (34% Fraud Density)**
   * **Characteristics:** Elevated absolute transaction values (~£4.69M) paired with the highest employee-vendor transaction density profiles (1.34).
   * **Audit Focus:** Flagged for concentrated procurement loops, highlighting high-value systemic relationships between specific staff and vendors requiring independent oversight.

## 🛠️ Tech Stack & Dependencies

* **Language:** Python 3.10+
* **Data Wrangling:** `pandas`, `numpy`
* **Machine Learning:** `scikit-learn` (Ensemble Methods, Clustering)
* **Visualization:** `matplotlib`, `seaborn`

---
