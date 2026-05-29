# telco-churn-analysis
Analysis of customer data to identify trends, churn rate, and predicting customer churn 

# Telecom Customer Churn Prediction
### Predicting which customers will leave — and what it costs when they do
 
---
 
## Business Problem
 
A telecom company is losing **£1.67 million annually** to customer churn. With a churn rate of 26.6%, roughly 1 in 4 customers leaves every year. This project identifies *which* customers are most likely to churn, *why* they churn, and *what the business should do about it* — using machine learning to score every customer by risk level.
 
> **The goal:** Give the retention team an actionable list of high-risk customers *before* they leave, not after.
 
---
 
## Key Findings
 
| Finding | Detail |
|---|---|
| Contract type is the biggest churn driver | Month-to-month customers churn at **42.7%** vs just **2.8%** on two-year contracts — a 15x difference |
| Fiber optic customers are high risk | Despite paying more, fiber customers churn at higher rates — suggesting a service quality issue |
| Tenure is the strongest retention signal | Churn drops sharply after month 12 — early engagement is critical |
| Payment method matters | Electronic check users churn significantly more than auto-pay customers |
| Tech support nearly halves churn | 41.6% churn without tech support vs 15.2% with it |
 
---
 
## Business Recommendations
 
1. **Prioritise contract conversion** — Incentivise month-to-month customers to upgrade to annual contracts. This single action has the highest projected impact on retention.
2. **Investigate fiber optic service quality** — The model flags fiber optic as the top churn risk factor. A product review is warranted.
3. **Target new customers early** — Churn is highest in months 1–6. An onboarding engagement campaign during this window would meaningfully reduce attrition.
4. **Bundle tech support into base plans** — Customers with tech support churn at half the rate. Removing the friction of adding it separately could improve retention across all segments.
---
 
## Tools & Technologies
 
![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-lightgrey?logo=pandas)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML%20Model-orange?logo=scikit-learn)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?logo=powerbi)
![PostgreSQL](https://img.shields.io/badge/SQL-Analysis-blue?logo=postgresql)
 
---
 
## Project Structure
 
```
telco-churn-analysis/
│
├── churn_analysis.ipynb          # Main notebook: EDA, cleaning, ML model
├── telco_churn_with_predictions.csv  # Enriched dataset with risk scores
├── feature_importance.csv        # ML model feature coefficients
├── Churn_Dashboard.pbix          # Power BI dashboard file
└── README.md
```
 
---
 
## Project Workflow
 
### 1. Data Cleaning
- Identified 11 rows with blank `TotalCharges` disguised as empty strings (not caught by standard null checks)
- Converted `TotalCharges` from object to float using `pd.to_numeric` with `errors='coerce'`
- Encoded target variable `Churn` from Yes/No to binary 1/0
### 2. Exploratory Data Analysis
- Calculated churn rates across contract type, internet service, payment method, and senior citizen status
- Quantified financial impact: **£139,131/month** in lost revenue from churned customers
- Identified tenure as the clearest retention signal — churn drops sharply after month 12
### 3. Machine Learning Model
- Encoded 19 categorical features using `pd.get_dummies` with `drop_first=True` to avoid multicollinearity
- Split data 80/20 with `stratify=y` to preserve class balance in both sets
- Trained a **Logistic Regression** classifier — chosen for interpretability over complexity
- Applied `class_weight='balanced'` to address 3:1 class imbalance
- Final model achieves **80% recall on churners** — catching 4 in 5 customers who would leave
### 4. Model Evaluation
 
| Metric | Score |
|---|---|
| Overall Accuracy | 73% |
| Churn Recall | **80%** |
| Churn Precision | 49% |
| Churners Caught (test set) | 298 out of 374 |
 
> **Why recall over accuracy?** Missing a churner costs the full lifetime value of that customer. A false alarm costs only a retention offer. Optimising for recall is the correct business decision here.
 
### 5. Risk Segmentation
Every customer was scored with a churn probability and assigned to a risk tier:
 
| Segment | Customers | Recommended Action |
|---|---|---|
| 🟢 Low Risk (0–30%) | 2,966 | No action needed |
| 🟡 Medium Risk (30–60%) | 1,676 | Light-touch email campaign |
| 🔴 High Risk (60–100%) | 2,390 | Priority retention outreach |
 
### 6. Power BI Dashboard
Two-page interactive dashboard built on the enriched dataset:
- **Page 1 — Churn Overview:** KPI cards, churn by contract/tenure/internet service, ML risk factors
- **Page 2 — Risk Segmentation:** Customer risk breakdown, probability distribution, high-risk customer table filterable by segment
---
 
## Dashboard Preview
 
![Churn Overview](Dashboard/Customer%20Churn%20Analysis.png)
 
![Risk Segmentation](Dashboard/Predictive%20Risk%20Segmentation.png)
 
---
 
## How to Run This Project
 
1. Clone the repository
2. Open `churn_analysis.ipynb` in Jupyter or [run it on Kaggle](https://www.kaggle.com/)
3. The dataset is sourced from [IBM Telco Customer Churn on Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
4. Run all cells in order — outputs will generate the two CSV files
5. Open `Churn_Dashboard.pbix` in Power BI Desktop and refresh the data source to point to your local CSV files
---
 
## What I Learned
 
- How to detect non-standard missing values that evade `isnull()` checks
- The precision-recall tradeoff and why it matters more than accuracy for imbalanced classification problems
- How to use logistic regression coefficients as interpretable feature importance scores
- How to translate model outputs into business language a non-technical stakeholder can act on
---
 
## Author
 
**[Your Name]**  
Junior Data Analyst | SQL · Python · Power BI  
[LinkedIn](https://linkedin.com) · [Kaggle](https://kaggle.com)
