
# Bank Customer Churn Analysis (PySpark)

## Project Overview

Customer churn is a critical challenge for subscription and financial products.  
Understanding **why customers leave** and **which behavioral signals indicate higher churn risk** can help companies design better retention strategies.

This project explores a bank customer dataset to identify **the main behavioral drivers of churn** and evaluate whether these variables can be used to **predict churn risk**.

The analysis focuses on answering two questions:

1. What behavioral patterns are associated with customers who churn?
2. Can these signals be used to build a simple model that identifies customers at risk?

The entire analysis is implemented using **PySpark**, with additional libraries used only for visualization and result interpretation.

---

# Dataset

The dataset used in this project is the **BankChurners dataset**, which contains information about customer demographics, credit card usage, and transaction activity.

Each row represents a customer, including features such as:

- transaction counts
- inactivity months
- credit utilization
- relationship depth with the bank

The target variable indicates whether the customer **remained active or churned**.
Source: https://www.kaggle.com/datasets/sakshigoyal7/credit-card-customers?resource=download

---

# Analytical Approach

The project follows a structured analytical process:

### 1. Exploratory Data Analysis (EDA)

The first step explores patterns between churned and active customers in order to identify possible behavioral signals.

Special attention is given to engagement indicators such as:

- number of transactions
- changes in transaction activity
- inactivity periods
- credit card utilization

---

### 2. Risk Segmentation

Instead of only describing churned customers, the analysis measures **conditional churn risk** by segment.

This helps answer questions such as:

“If a customer has this characteristic today, how much higher is their probability of churn?”

---

### 3. Statistical Validation

A **Generalized Linear Model (GLM)** with a binomial distribution and logit link function is used to test whether the relationships observed in the exploratory analysis are statistically significant.

This step provides:

- coefficient direction
- statistical significance (p-values)
- odds ratio interpretation

---

### 4. Multivariate Analysis

Many behavioral variables capture similar patterns.

To isolate the **independent effects** of each variable, a multivariate regression model is fitted including several potential predictors.

This allows us to identify which signals remain relevant when controlling for overlapping information.

---

### 5. Correlation and Feature Selection

Correlation analysis helps detect redundancy between variables.

For example, transaction amount and transaction count often move together.

To improve interpretability, the model is simplified to a **minimal set of meaningful behavioral indicators**.

---

### 6. Predictive Evaluation

Finally, the selected variables are used to train a logistic regression classifier.

The model is evaluated using **AUC (Area Under the ROC Curve)** to measure its ability to distinguish churned customers from active customers.

This step verifies whether the identified drivers also have **predictive value**.

---

# Key Findings

The analysis suggests that **customer churn is primarily associated with declining engagement rather than financial exposure**.

The most important behavioral signals identified were:

### Months_Inactive_12_mon
The strongest churn indicator.

Customers with increasing inactivity are significantly more likely to churn.

Business interpretation:  
Rising inactivity should be monitored as an early warning signal for churn risk.

---

### Total_Ct_Chng_Q4_Q1
Represents the change in transaction activity over time.

Customers whose transaction activity declines are much more likely to leave.

Business interpretation:  
Maintaining transaction engagement may significantly reduce churn risk.

---

### Avg_Utilization_Ratio
Captures the intensity of credit card usage.

Customers who actively use their credit capacity tend to remain engaged with the product.

Business interpretation:  
Encouraging active usage can strengthen retention.

---

### Total_Relationship_Count
Measures the number of products a customer holds with the bank.

Customers with deeper relationships with the institution tend to churn less.

Business interpretation:  
Cross‑selling additional financial products may increase customer retention.

---

# Model Performance

A logistic regression model built using the selected behavioral variables shows meaningful ability to distinguish churners from active customers, measured using **ROC AUC**.

This indicates that the identified variables can be used not only to explain churn behavior, but also to **estimate churn risk**.

In practice, such a model could be used to assign a **risk score** to customers and prioritize retention actions.

---

# Example Application

A simplified churn risk score derived from the model could help identify customers requiring proactive engagement.

Example:

Customers with predicted churn probability above a defined threshold (e.g. 0.7) could be flagged for retention campaigns.

---

# Limitations

This analysis identifies **statistical associations**, not causal relationships.

Additionally, the results depend on the variables available in the dataset.  
In real‑world scenarios, additional behavioral signals such as digital engagement, customer support interactions, or product usage patterns may further improve churn prediction.

---

# Technologies Used

- PySpark
- Python
- Pandas
- Matplotlib / Seaborn

---

# Repository Structure

project/

data/  
└── BankChurners.csv  

notebook/  
└── churn_analysis.ipynb  

README.md

---

# Final Thoughts

This project demonstrates how a combination of exploratory analysis, statistical validation, and predictive modeling can transform raw behavioral data into actionable insights about customer churn.

While the dataset is simplified, the analytical process reflects the reasoning used in real‑world customer analytics projects.
