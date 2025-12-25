# Bank Customer Segmentation & Targeted Marketing (Production-Ready ML API)

## 🧠 Project Overview
This project implements an **end-to-end customer segmentation system** for credit card users using **unsupervised machine learning (KMeans)** and deploys it as a **production-ready FastAPI service**.

The goal is not just clustering, but **turning clusters into actionable business segments** that can be consumed by downstream systems (CRM, marketing engines, dashboards).

---

## 🎯 Business Problem
Banks often treat all customers the same.

This leads to:
- Poor targeting
- Low engagement
- Missed high-value customers
- Increased churn

This project solves that by:
- Segmenting customers based on spending behavior
- Mapping each segment to **clear marketing strategies**
- Serving predictions via an API for real-world integration

---

## 🗃️ Dataset Summary
- **Source:** Kaggle – Credit Card Dataset for Clustering
- **Rows:** 8,950
- **Columns:** 18
- **Learning Type:** Unsupervised (No target variable)

Key features include:
`BALANCE`, `PURCHASES`, `CREDIT_LIMIT`, `PAYMENTS`, `CASH_ADVANCE`, etc.

---

## 🧩 Key Components

### 1️⃣ Data Cleaning & Feature Engineering
- Handled missing values
- Removed irrelevant identifiers (e.g., `CUST_ID`)
- Engineered business-driven features:
  - `CREDIT_UTILIZATION`
  - `PAYMENT_RATIO`
  - `CASH_USAGE_RATIO`
  - `ACTIVITY_INDEX`
- Applied **frozen IQR caps** to control outliers consistently in production

---

### 2️⃣ Clustering Strategy
- Compared multiple preprocessing strategies:
  - No scaling
  - MinMaxScaler
  - RobustScaler
  - Log transformation
- Evaluated using **Silhouette Score**
- Final selection prioritized:
  - Interpretability
  - Stability
  - Business usefulness

#### 📌 Final Model Choice
| Approach | Clusters | Silhouette |
|--------|----------|------------|
| Cleaned (No Scaling) | 3 | ~0.44 ✅ |

---

### 3️⃣ Cluster Profiles (Business Interpretation)

#### 🟡 Cluster 0 — Moderate Users
- Mid-range balances
- Moderate purchases
- Higher cash advance usage  
**Strategy:** Promote installment plans and balance-transfer offers

#### 🔵 Cluster 1 — Low-Activity Users
- Low balances
- Low spending
- Smaller credit limits  
**Strategy:** Welcome rewards, cashback incentives

#### 🟢 Cluster 2 — High-Value Spenders
- Highest purchase volume
- High purchase frequency
- Large credit limits  
**Strategy:** Exclusive rewards, concierge services, premium upgrades

---

## 🚀 Model Deployment (Core Highlight)

The trained clustering model is deployed as a **FastAPI service**.

### ✅ API Capabilities
- Accepts **batch customer data**
- Performs:
  - Schema validation (Pydantic)
  - Column alignment
  - Numeric & range validation
  - Feature engineering
  - Scaling
  - Cluster prediction
- Returns:
  - Cluster ID
  - Segment name
  - Behavior summary
  - Marketing strategy

### Example Response
{
  "results": [
    {
      "cluster": 2,
      "segment_name": "High-Value Spenders",
      "behavior": "Highest purchase volumes and frequency",
      "marketing_strategy": "Exclusive rewards and concierge services"
    }
  ],
  "ignored_columns": [],
  "model_version": "1.0.0"
}

🛡️ Production-Grade Practices Implemented

✔ Frozen preprocessing logic (no training–serving skew)
✔ Artifact versioning (model.pkl, scaler.pkl, iqr_caps.pkl)
✔ Strong input validation
✔ Defensive handling of extra/missing columns
✔ Structured logging for traceability
✔ Clean project structure (src/, api/, artifacts/)


📂 Project Structure

project/
│
├── api/
│   └── main.py
│
├── src/
│   ├── preprocessing.py
│   ├── predict.py
│   ├── validators.py
│   ├── schemas.py
│   ├── cluster_profiles.py
│   └── logger.py
│
├── artifacts/
│   ├── model.pkl
│   ├── scaler.pkl
│   └── iqr_caps.pkl
│
├── notebooks/
│   ├── EDA.ipynb
│   ├── Feature_Engineering.ipynb
│   ├── Clustering_Evaluation.ipynb
│   └── Customer_Profiling.ipynb
│
├── README.md


🔍 Monitoring & Observability (Planned)
Runtime monitoring (data drift, cluster distribution tracking) was intentionally excluded to keep this deployment lightweight.
A follow-up project will integrate MLflow for:

- Experiment tracking
- Model versioning
- Metrics comparison
- Lifecycle management
 
🧠 Skills Demonstrated
- Machine Learning (Unsupervised)
- Feature Engineering
- Model Evaluation
- Production ML Design
- FastAPI Deployment
- Data Validation
- Logging & Error Handling
- Business-Oriented ML Thinking

📬 Let's Connect
LinkedIn: https://www.linkedin.com/in/sudais-shah-938b9a312/
