# Taxpayer Risk Classification Project

## Overview  
This project aims to develop a machine learning model to classify taxpayers into **high** or **low-risk** categories for tax compliance. The objective is to enable tax authorities to prioritize audits effectively, reduce costs, and improve revenue recovery by accurately identifying potential non-compliant taxpayers. The classification focuses on leveraging financial and behavioral data to build robust predictive models.

## Business and Data Understanding

### Stakeholder Audience  
- **Tax Authority/Revenue Service:** Responsible for tax collection and enforcement of compliance.  
- **Audit Teams:** Use risk classifications to prioritize audit targets efficiently.  
- **Policy Makers:** Use model insights to refine tax policies and compliance strategies.  
- **Taxpayers:** Affected by audit decisions and compliance enforcement.  
- **Data Analysts/Scientists:** Develop, validate, and maintain predictive models.


### Data Source  
[Tax Risk Identification Dataset (Kaggle)](https://www.kaggle.com/datasets/ziya07/tax-risk-identification-dataset)
### Dataset Choice  
The dataset used is the **Tax Risk Identification Dataset** sourced from Kaggle, with approximately 1000 observations and 13 features, including:  
- Financial data: Revenue, Expenses, Tax Liability, Tax Paid, Profit  
- Behavioral data: Late Filings, Compliance Violations, Audit Findings  
- Categorical data: Industry, and the target variable **Risk_Label** (binary: High/Low risk)

The **Risk_Label** is derived from financial and compliance behaviors to represent taxpayer risk.

## Modeling  

### Data Preparation 

- Performed exploratory data analysis (EDA) including data structure inspection, missing values check (none found), and visualizations of feature distributions and target relationships.  
- Data cleaning included outlier removal and quality checks.

### Feature Engineering  
- Created features such as **Tax_Compliance_Ratio** (Tax Paid / Tax Liability) and **Audit_to_Tax_Ratio**.  
- Applied one-hot encoding for categorical variables such as **Industry**.

### Model Selection  
Three classification models were evaluated:  
- **Logistic Regression:** Served as a strong baseline.  
- **Decision Tree Classifier:** Both untuned and tuned versions, chosen for interpretability and non-linear relationships.  
- **Random Forest Classifier (Tuned):** Emerged as the best model, offering ensemble advantages and improved robustness.

### Handling Class Imbalance  
Applied **SMOTE** to balance the target classes and improve fairness in model predictions.

## Evaluation  

### Model Performance  
| Model               | Accuracy | Precision (Low / High) | Recall (Low / High) | F1-Score (Low / High) | ROC AUC | Key Insight                                                    |
|---------------------|----------|-----------------------|---------------------|-----------------------|---------|----------------------------------------------------------------|
| Logistic Regression  | 93%      | 0.74 / 0.97           | 0.88 / 0.94         | 0.80 / 0.96           | 0.91    | Strong baseline; good at identifying high risk but some false positives |
| Untuned Decision Tree| 100%     | 1.00 / 1.00           | 0.97 / 1.00         | 0.99 / 1.00           | 0.9875  | Excellent performance; near perfect classification             |
| Tuned Decision Tree  | 100%     | 1.00 / 1.00           | 0.97 / 1.00         | 0.99 / 1.00           | 0.9875  | Maintains top performance post tuning; improved robustness and reliability |
| Tuned Random Forest  | 100%     | 1.00 / 1.00           | 0.97 / 1.00         | 0.99 / 1.00           | 1.00    | Perfect class separation; zero false negatives; minimal false positives |

### Evaluation Metric Choice  
The primary metric for this classification task is **ROC AUC** because:  
- It measures the model’s ability to distinguish between high and low risk taxpayers across all classification thresholds.  
- Balances sensitivity (recall) and specificity, critical for audit prioritization.  
- Provides a threshold-independent performance measure, aiding robust business decisions.

| Model               | ROC AUC Score |
|---------------------|---------------|
| Logistic Regression  | 0.91          |
| Untuned Decision Tree| 0.9875        |
| Tuned Decision Tree  | 0.9875        |
| Tuned Random Forest  | 1.00          |

The **Tuned Random Forest** model achieves a perfect ROC AUC of 1.00, outperforming all others.

### Tuned Decision Tree vs Tuned Random Forest  
| Metric               | Tuned Decision Tree | Tuned Random Forest |
|----------------------|---------------------|---------------------|
| ROC AUC (Test)       | 0.9875              | 1.00                |
| Accuracy             | 100%                | 100%                |
| False Negatives      | 0                   | 0                   |
| False Positives      | 1                   | 1                   |
| Precision (High Risk) | 1.00                | 1.00                |
| Recall (High Risk)    | 1.00                | 1.00                |
| F1-Score (High Risk)  | 1.00                | 1.00                |
| Business Alignment   | Excellent           | Perfect             |

While both tuned models perform exceptionally well, the **Tuned Random Forest** edges ahead due to its flawless ROC AUC score, making it the most reliable for deployment.

## Conclusion  

### Final Model Selection  
The **Tuned Random Forest** model is the best choice:  
- Perfect ROC AUC of 1.0, indicating flawless class separation.  
- Zero false negatives, ensuring no high-risk taxpayer is missed.  
- Minimal false positives, maintaining audit efficiency and fairness.  
- Perfectly aligns with business goals: maximize revenue recovery while minimizing disruption to compliant taxpayers.

### Business Recommendations  
- **Deploy the Tuned Random Forest model** as the core audit risk classification system.  
- **Develop user-friendly decision support tools** (dashboards, real-time scoring apps) to empower auditors and stakeholders.  
- **Continuously update and expand data sources** to maintain accuracy amid changing risk patterns.  
- **Implement continuous monitoring and bias checks** to ensure fairness and regulatory compliance.  
- **Explore advanced ensemble and hybrid methods** like Gradient Boosting or model stacking to further enhance robustness.

### Future Work  
- Continuous monitoring and data integration to adapt to evolving taxpayer behaviors.  
- Expansion into complementary models and advanced techniques for better audit targeting.

---

This README bridges your business presentation and the detailed Jupyter Notebook, providing a comprehensive overview of your methodology and results without including code.
## Project Structure

```plaintext
├── data/                      # CSV datasets used in the project  
├── notebooks/                 # Jupyter notebooks containing analysis and modeling  
├── README.md                  # Project documentation  
