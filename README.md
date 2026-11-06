# Customer Churn Prediction Using Machine Learning

## 1. Project Overview

Customer churn occurs when customers stop using a company's services. Predicting churn helps businesses identify customers who are likely to leave and take preventive retention measures.

This project uses machine learning to predict customer churn and identify the factors that influence customer decisions.

## 2. Business Problem

The objective is to answer three important questions:

- Which customers are more likely to leave?
- What factors contribute to customer churn?
- How can businesses prioritize customer retention strategies?

## 3. Dataset

**Dataset:** IBM Telco Customer Churn

- Total records: 7,043
- Target variable: `Churn`
- Prediction classes: Yes / No
- Churn rate: Approximately 26%

The dataset contains customer demographics, services, contract details, payment methods, and billing information.

## 4. Data Cleaning and Preprocessing

The following steps were performed:

- Removed the `customerID` column.
- Converted `TotalCharges` into numeric format.
- Handled 11 missing `TotalCharges` values by replacing them with 0.
- Converted the target variable into binary format.
- Applied one-hot encoding to categorical variables.
- Split the data into training and testing sets using stratification.

## 5. Exploratory Data Analysis

The analysis highlighted several churn patterns:

- Month-to-month customers had a churn rate of 42.71%.
- Customers with less than 12 months of tenure had a churn rate of 47.44%.
- Contract type and customer tenure were important factors to investigate when understanding churn.

## 6. Machine Learning Models

Two classification models were developed:

1. Logistic Regression — Baseline model.
2. XGBoost — Tuned using GridSearchCV with 5-fold Stratified Cross-Validation.

**Best XGBoost parameters:**
- Learning rate: 0.05
- Maximum depth: 3
- Number of estimators: 300

Average precision during cross-validation: 0.6674.

## 7. Model Performance

| Evaluation Metric | Logistic Regression | Tuned XGBoost |
|---|---:|---:|
| Precision | 66.14% | 50.94% |
| Recall | 55.88% | 79.68% |
| ROC-AUC | 84.18% | 84.21% |
| PR-AUC | 63.24% | 66.33% |

**Final Model: Tuned XGBoost**

XGBoost was selected because it achieved higher recall and PR-AUC, making it more suitable for identifying customers at risk of churning.

Its lower precision means it also flags more customers who may not actually churn.

## 8. Threshold Optimization

Threshold selection was performed using cross-validation predictions from the training dataset, targeting a minimum recall of 80%.

- Default threshold: 0.50
- Selected threshold: 0.4969
- Default recall: 79.68%
- Selected recall: 79.95%

The improvement was marginal, indicating that the default threshold already provided comparable performance.

## 9. Model Explainability Using SHAP

SHAP was used to understand how different features influence churn predictions.

Important features identified included:

- Customer tenure
- Contract type
- Internet service type
- Payment method
- Total charges
- Monthly charges
- Paperless billing

The analysis indicated that lower tenure, month-to-month contracts, fiber optic service, electronic check payments, and higher monthly charges were associated with increased churn predictions.

## 10. Business Recommendations

Based on EDA and SHAP analysis:

1. Introduce onboarding and engagement programs for new customers.
2. Encourage month-to-month customers to switch to long-term contracts through suitable incentives.
3. Investigate service quality and pricing among fiber optic customers.
4. Encourage automatic payment methods.
5. Provide personalized pricing plans and retention offers.
6. Use churn probabilities to prioritize high-risk customers for retention campaigns.

## 11. Top 10% Churn Capture Analysis

The model was used to rank customers by predicted churn probability.

- Total actual churners in the test set: 374
- Churners identified in the top 10%: 109
- Top 10% churn capture rate: 29.14%

This demonstrates how a business could prioritize a smaller group of high-risk customers for retention campaigns.

This is a prioritization result, not proof that the campaign would prevent churn.

## 12. Tools and Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- XGBoost
- SHAP
- Jupyter Notebook
- Joblib

## 13. Project Files

- `customer_churn.ipynb` — Data analysis, model training, evaluation, and explainability.
- `customer_churn_xgboost.pkl` — Saved trained XGBoost model.
- `model_features.pkl` — Saved model feature names and order.

## 14. Conclusion

This project demonstrates how machine learning can help identify customers at risk of churn.

The tuned XGBoost model achieved a recall of 79.68% and PR-AUC of 66.33%. SHAP interpretation provided insights into important churn-related patterns, while the top 10% capture analysis demonstrated a practical way to prioritize retention efforts.

The project combines data analysis, predictive modelling, model explainability, and business recommendations to address a real-world business problem.
