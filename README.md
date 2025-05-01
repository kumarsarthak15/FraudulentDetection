# FraudulentDetection
Fradulent Detection using Random Forest
# 🔍 Fraud Detection System Using Machine Learning

This project focuses on proactively identifying fraudulent transactions using supervised machine learning on a real-world financial dataset of over **6 million transactions**. The dataset simulates 30 days of financial activity, capturing both legitimate and fraudulent behavior.

---

## 📁 Dataset Overview

- **Filename:** `fraud.csv`
- **Rows:** 6,362,620
- **Columns:** 10
- **Key Columns:**
  - `step` – Hour of transaction (0–744)
  - `type` – Transaction type (`CASH_IN`, `CASH_OUT`, `TRANSFER`, `PAYMENT`, `DEBIT`)
  - `amount` – Transaction value
  - `isFraud` – Label: 1 = Fraud, 0 = Legitimate
  - `isFlaggedFraud` – 1 = Flagged by rule-based system

---

## 🧼 Step 1: Data Cleaning & Preprocessing

- Checked for missing values and outliers
- Created engineered features:
  - `errorBalanceOrig` = `oldbalanceOrg - newbalanceOrig - amount`
  - `errorBalanceDest` = `oldbalanceDest + amount - newbalanceDest`
- One-hot encoded categorical `type` column
- Dropped unique ID columns (`nameOrig`, `nameDest`)

---

## 🧠 Step 2: Model Building

- **Model:** Random Forest Classifier
- **Why?**
  - Handles large data well
  - Robust to noise
  - Provides feature importance
- **Metrics Used:**
  - Accuracy
  - Precision & Recall
  - Confusion Matrix
  - ROC-AUC Curve

---

## 🛠 Step 3: Model Tuning

- Used **RandomizedSearchCV** to optimize hyperparameters:
  - `n_estimators`, `max_depth`, `min_samples_split`
- Cross-validation used to avoid overfitting

---

## 📊 Step 4: Results & Insights

| Metric | Value |
|--------|--------|
| Accuracy | ~99.9% |
| ROC-AUC | 0.97 |
| Precision (Fraud) | High |
| Recall (Fraud) | High |

- **Key Features in Detecting Fraud:**
  - `amount`
  - `type_TRANSFER`, `type_CASH_OUT`
  - `errorBalanceOrig`
  - `errorBalanceDest`
  - `step` (hourly patterns)

---

## 🔐 Business Recommendations

- Real-time fraud detection using this model
- Limit large `TRANSFER` and `CASH_OUT` at odd hours
- Monitor balance errors in transactions
- Apply 2FA for high-value operations
- Track fraud reduction KPIs post-implementation

---

## 📈 Evaluation Strategy

To determine if fraud prevention methods are working:
- Monitor fraud rate before/after deployment
- Track false positive and false negative counts
- Use customer feedback & alert-to-fraud ratio
- Periodic model retraining to maintain accuracy

---
