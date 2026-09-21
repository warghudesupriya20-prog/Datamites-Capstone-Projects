# Home Loan Default Risk Management

## Project Overview

This project focuses on predicting the likelihood of home loan default using machine learning classification techniques.

The objective is to identify customers who may be at higher risk of default so that financial institutions can perform additional assessment and risk management.

The project uses customer application, financial, employment, credit, and previous application information to build and evaluate classification models.

---

## Problem Statement

Financial institutions face the risk of loan defaults, which can result in financial losses.

The objective of this project is to develop a machine learning model that predicts whether a customer is likely to default on a home loan.

* **Target = 0:** Customer does not default
* **Target = 1:** Customer defaults

---

## Dataset

The project uses the Home Credit-style dataset containing multiple related datasets:

* `application_train.csv`
* `bureau.csv`
* `bureau_balance.csv`
* `previous_application.csv`
* `POS_CASH_balance.csv`
* `installments_payments.csv`
* `credit_card_balance.csv`

The main modelling dataset is `application_train.csv`.

---

## Data Preprocessing

The following preprocessing techniques were used:

* Handling missing values
* Median imputation for numerical features
* Most-frequent imputation for categorical features
* One-Hot Encoding for categorical variables
* Train-test split with stratification
* Handling unknown categories using `handle_unknown='ignore'`

The data was divided into training and testing sets using an **80:20 split** with `random_state=42`.

---

## Feature Engineering

Additional features were created to provide useful financial and demographic information to the model:

* `AGE_YEARS`
* `EMPLOYMENT_YEARS`
* `INCOME_CREDIT_RATIO`
* `CREDIT_INCOME_RATIO`
* `ANNUITY_INCOME_RATIO`
* `CREDIT_GOODS_RATIO`
* `INCOME_PER_FAMILY_MEMBER`

---

## Class Imbalance

The target variable was highly imbalanced:

* **Non-default (0): 91.93%**
* **Default (1): 8.07%**

Because of this imbalance, accuracy alone was not considered sufficient for model evaluation.

Class weighting using `scale_pos_weight` was applied to XGBoost to give greater importance to the minority default class.

---

## Models Evaluated

The following models were evaluated:

1. Logistic Regression
2. Decision Tree
3. Random Forest
4. Gradient Boosting
5. XGBoost
6. Balanced XGBoost
7. Tuned XGBoost

The models were evaluated using:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC
* Confusion Matrix
* ROC Curve
* Precision-Recall Curve

---

## Model Performance

| Model               | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
| ------------------- | -------: | --------: | -----: | -------: | ------: |
| Logistic Regression |   91.91% |     0.00% |  0.00% |    0.00% |  0.6482 |
| Decision Tree       |   85.91% |    15.14% | 16.19% |   15.65% |  0.5411 |
| Random Forest       |   91.93% |    50.00% |  0.22% |    0.44% |  0.7328 |
| Gradient Boosting   |   91.98% |    59.49% |  1.89% |    3.67% |  0.7651 |
| XGBoost             |   91.98% |    67.74% |  1.27% |    2.49% |  0.7659 |
| Balanced XGBoost    |   70.30% |    16.98% | 68.92% |   27.25% |  0.7655 |
| Tuned XGBoost       |   84.94% |    24.75% | 42.40% |   31.25% |  0.7655 |

---

## Threshold Tuning

The Balanced XGBoost model was evaluated using different classification thresholds.

The threshold was varied from **0.20 to 0.70** to study the trade-off between precision and recall.

A threshold of **0.65** produced the highest F1 Score among the tested thresholds.

At this threshold:

* Accuracy: **84.94%**
* Precision: **24.75%**
* Recall: **42.40%**
* F1 Score: **31.25%**
* ROC-AUC: **0.7655**

---

## Feature Importance

The most influential features identified by the XGBoost model included:

* `EXT_SOURCE_2`
* `EXT_SOURCE_3`
* `EMPLOYMENT_YEARS`
* `NAME_EDUCATION_TYPE_Higher education`
* `CREDIT_GOODS_RATIO`
* `EXT_SOURCE_1`
* `CODE_GENDER`
* `PREV_TOTAL_DOWN_PAYMENT`
* `DAYS_EMPLOYED`
* `POS_CASH_AVG_DPD_DEF`

These features represent a combination of external risk indicators, employment characteristics, financial ratios, education, previous application information, and repayment-related variables.

Feature importance indicates which variables the model relied on most; it does not establish that these variables directly cause default.

---

## Risk Factors

The model identified several groups of variables that are useful for assessing default risk:

* External risk indicators
* Employment duration
* Credit-to-goods relationship
* Previous application behaviour
* Repayment-related information
* Age and employment information
* Financial and asset information

These factors can be considered as model-based risk indicators during further assessment.

---

## Challenges Faced

The major challenges encountered during the project included:

### Large Dataset Size

Multiple large CSV datasets required careful data handling and preprocessing.

### Missing Values

Missing values were handled using median imputation for numerical variables and most-frequent imputation for categorical variables.

### Categorical Variables

One-Hot Encoding was used to convert categorical variables into numerical features.

### Class Imbalance

Only 8.07% of observations belonged to the default class. `scale_pos_weight` was therefore used with XGBoost.

### Low Default-Class Recall

The original XGBoost model had low recall at the default threshold. Threshold tuning was performed to improve the precision-recall balance.

### Model Evaluation

Because of class imbalance, multiple metrics including Precision, Recall, F1 Score, and ROC-AUC were used instead of relying only on accuracy.

---

## Business Recommendations

* Use model predictions to identify applications requiring additional assessment.
* Consider risk-based screening for potentially high-risk applications.
* Use an appropriate classification threshold depending on the institution's risk requirements.
* Review financial, employment, credit, and previous application indicators.
* Combine machine learning predictions with human review and existing lending policies.
* Periodically monitor model performance.
* Validate the model on new data before deployment.

---

## Final Conclusion

The project demonstrates the application of machine learning to home loan default risk management.

Several classification algorithms were evaluated, and class imbalance was addressed using Balanced XGBoost. Threshold tuning was then performed to obtain a more suitable balance between precision and recall.

The final selected approach was **Balanced XGBoost with a classification threshold of 0.65**, which achieved an F1 Score of **31.25%** and Recall of **42.40%** on the test dataset.

The model can be used as a decision-support tool to identify potentially higher-risk loan applications and prioritize them for further assessment.

---

## Model Files

The trained model and preprocessing pipeline were saved using Joblib:

* `home_loan_final_model.pkl`
* `home_loan_preprocessor.pkl`

The final model file contains the Balanced XGBoost model and the selected classification threshold of **0.65**.

---

## Tools and Technologies

* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* Matplotlib
* Joblib
* Jupyter Notebook

---

## Project Structure

```text
Home-Loan-Default-Risk-Management/
│
├── Home_Loan_Default_Prediction.ipynb
├── README.md
├── PRCP-1006-HomeLoanDef.docx
│
├── application_train.csv
├── bureau.csv
├── bureau_balance.csv
├── previous_application.csv
├── POS_CASH_balance.csv
├── installments_payments.csv
├── credit_card_balance.csv
│
├── home_loan_final_model.pkl
└── home_loan_preprocessor.pkl
```
