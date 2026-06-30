# UAE E-Commerce Fraud Signal Analysis
## Phase 3: Machine Learning Classification

This repository covers the third and final phase of a three-part fraud 
analytics project analyzing 100,000 synthetic UAE e-commerce transactions.

This phase was completed as a learning project to apply supervised 
classification techniques covered in coursework to a real-world style 
fraud detection problem. The primary goal was to practice the end-to-end 
ML workflow — feature selection, model building, evaluation, and honest 
interpretation of results — including leakage detection and statistical 
diagnostics, rather than to deploy a production-ready fraud detector.

**Phase 1 — SQL:** Database design and structured fraud signal analysis — [repo](https://github.com/FatihaOkesola/UAE_E-Commerce_Fraud_Signal_Analysis)
**Phase 2 — Python EDA:** Visualizations and pattern validation — [repo](https://github.com/FatihaOkesola/UAE_Fraud_EDA_Analysis)
**Phase 3 — ML Classification:** This repository

---

## What This Phase Covers

Four models were built and evaluated:
- **Logistic Regression** — used for statistical inspection and 
  data-driven feature selection via p-values and VIF, rather than as 
  a final predictive model
- **Decision Tree** — tuned via GridSearchCV with SMOTE correctly 
  applied inside cross-validation
- **Random Forest** — 500 trees, used for both prediction and feature 
  importance analysis
- **KNN** — tuned across a wide range of K values guided by the √n 
  rule of thumb

---

## Key Methodological Finding

During this phase, an initial approach applying SMOTE to the full 
training set before cross-validation was found to produce artificially 
optimistic recall estimates — a data leakage issue. This was identified, 
investigated, and corrected using an imbalanced-learn Pipeline that 
applies SMOTE only within each training fold. This correction is 
documented in full in the notebook as part of the analytical process, 
not edited out.

---

## Key Findings

This dataset includes several pre-engineered fraud flag columns, which 
shaped both the analytical approach and the scope of business 
recommendations that could be drawn from the models. Further 
investigation showed that signals identified as strongest during SQL 
analysis (`fraud_flag_prev_cb`, `user_is_high_risk`) ranked low in 
Random Forest feature importance because they occurred infrequently. 
Although highly reliable when triggered, their limited coverage reduced 
their influence on model training — a useful distinction between 
precision and breadth.

| Model | Recall | F1 Score | False Positives |
|---|---|---|---|
| Decision Tree | 33.9% | 0.156 | 7,543 |
| Random Forest | 30.2% | 0.163 | 6,055 |
| KNN | 68.2% | 0.196 | 13,255 |

**The objective of this phase was not to maximize predictive performance, 
but to understand the strengths, limitations, and trade-offs of common 
classification techniques on a structured fraud dataset.**

All three models returned low F1 scores, indicating that none are 
suitable for standalone deployment without further feature engineering 
and validation against real transaction data. The notebook includes a 
full risk team recommendation based on these results, including a 
proposed hybrid approach combining rule-based signals with ML scoring.

---

## Limitations

- This is a synthetic dataset; some expected signals (transaction 
  velocity) showed no variation
- Pre-engineered fraud flags limit how much can be concluded about 
  genuine fraud pattern discovery versus model use of existing labels
- More advanced approaches (gradient boosting, neural networks) were 
  not explored in this phase

---

## Tools
Python · pandas · scikit-learn · imbalanced-learn · statsmodels · matplotlib

---

## Status
- [x] Logistic regression and statistical feature selection
- [x] Decision Tree with corrected SMOTE pipeline
- [x] Random Forest with feature importance analysis
- [x] KNN with K-value tuning
- [x] Model comparison and risk team recommendation

---

## Part of a Broader Portfolio
This project is part of a multi-tool analytics portfolio. The SQL and 
EDA phases of this project demonstrate stronger, more directly 
actionable findings — this ML phase focuses on demonstrating the 
classification workflow and methodological rigor, including identifying 
and correcting a data leakage issue mid-analysis.
