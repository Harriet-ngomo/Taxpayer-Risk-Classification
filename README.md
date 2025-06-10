# FairTax Analytics: Taxpayer Risk Classification Project

- 🔗 [Final Presentation](./Presentation.pdf) 
## Overview

**FairTax Analytics** is a data driven initiative aimed at transforming how tax authorities identify and prioritize high risk taxpayers. Tax evasion and non compliance undermine government revenue critical for essential services like education, healthcare and infrastructure. This project leverages machine learning to automate taxpayer risk classification, enabling smarter audit targeting, early risk detection and more equitable enforcement

## Business and Data Understanding

### Business Problem

Manual audit selection often relies on limited human judgment and scarce resources, leading to inefficiencies and unfair targeting. Our core business goal is to:

> **Develop a predictive model to classify taxpayers by risk level (Low VS High)** to support targeted audits, enhance compliance monitoring and optimize revenue recovery

### Stakeholders

| Stakeholder                  | Interest / Role                                |
|-----------------------------|------------------------------------------------|
| **Tax Authority / Revenue Service** | Maximize revenue, improve compliance     |
| **Audit Teams**             | Prioritize audits efficiently                   |
| **Policy Makers**           | Inform regulation and policy design             |
| **Taxpayers**               | Ensure fair compliance monitoring               |
| **Data Analysts / Scientists** | Build, maintain, and explain predictive models |

### Dataset Summary

- **Data Source**:
[Tax Risk Identification Dataset (Kaggle)](https://www.kaggle.com/datasets/ziya07/tax-risk-identification-dataset)
- **Observations**: 1000
- **Features**: 13 columns including financial and behavioral metrics
- **Target Variable**: `Risk_Label` (High = 1, Low = 0).Medium risk entries were excluded for binary classification

#### Key Features

| Column Name                | Description                                    | Type            |
|---------------------------|------------------------------------------------|-----------------|
| `Taxpayer_ID`             | Unique taxpayer identifier                     | Categorical (ID)|
| `Revenue`, `Expenses`     | Financial metrics                              | Continuous       |
| `Tax_Liability`, `Tax_Paid` | Tax owed vs. paid                          | Continuous       |
| `Late_Filings`, `Compliance_Violations`, `Audit_Findings` | Behavioral indicators | Discrete         |
| `Industry`                | Taxpayer's industry sector                     | Categorical      |
| `Profit`                  | Revenue minus Expenses                         | Continuous       |
| `Tax_Compliance_Ratio`    | Tax Paid / Tax Liability                       | Continuous       |
| `Audit_to_Tax_Ratio`      | Audit Findings relative to tax amounts         | Continuous       |

---

## Data Preparation

- Conducted exploratory data analysis (EDA)
- Visualized feature distributions and class relationships
- Verified no missing data
- Removed outliers and medium risk records
- Categorical encoding and class balancing using SMOTE
- Train-test split: Default split 

---

## Modeling

### Models Tested

- **Logistic Regression** ::Baseline
- **Untuned Decision Tree**
- **Tuned Decision Tree** ::via GridSearchCV
- **Tuned Random Forest** ::*Best Performing*

### Feature Engineering

- Ratio-based feature construction
- One Hot Encoding encoding for categorical features
- Addressed class imbalance using  SMOTE

---

## Evaluation

### Chosen Metric: ROC AUC

We prioritized **ROC AUC** because it:
- Is threshold independent
- Measures separability between classes
- Balances recall and precision

| Model                    | Accuracy | F1 (High) | Recall (High) | ROC AUC | Notes                               |
|--------------------------|----------|-----------|----------------|---------|--------------------------------------|
| Logistic Regression      | 0.85     | 0.91      | 0.84           | 0.87    | Good baseline, but high FP for Low   |
| Untuned Decision Tree    | 0.90     | 0.94      | 0.94           | 0.82    | Overfitting risk                     |
| Tuned Decision Tree      | 0.87     | 0.92      | 0.89           | 0.90    | Better generalization                |
| **Tuned Random Forest**  | **0.90** | **0.94**  | **0.93**       | **0.94**| ⭐ Best performance overall           |

---

## Conclusion

The **Tuned Random Forest** model demonstrated the best balance between recall, precision and AUC. It effectively flags high risk taxpayers, supports fair audit prioritization and enhances compliance efforts

### Key Takeaways

- **Efficient Audit Selection**: Targets risky taxpayers while minimizing false positives
- **Fair Enforcement**: Reduces scrutiny on compliant individuals
- **Revenue Recovery**: Detects under-reporting and potential evasion

---

## Recommendations

1. **Deploy Tuned Random Forest** as the core classification engine for audits
2. **Develop Auditor Dashboards** with risk scores and interpretability tools like  SHAP
3. **Establish Monitoring Frameworks** to track fairness, drift and performance
4. **Explore Advanced Ensembles** like Gradient Boosting or model stacking in future versions

---
## Repository Structure

├── notebooks/ # EDA and model development notebooks
│ ├── 01_data_cleaning.ipynb
│ ├── 02_feature_engineering.ipynb
│ ├── 03_modeling.ipynb
│ └── 04_evaluation.ipynb
├── data/ # Cleaned dataset 
├── models/ # Modelling
├── outputs/ # Figures, charts, and reports
├── README.md # Project documentation
└── presentation.pdf #  🔗 [Final Presentation](./Presentation.pdf) 

