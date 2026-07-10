# customer-campaign-response-prediction

A machine learning classification project that predicts whether a customer will resposd to a marketing campaign, helping business optomise their marketing spend and target the right people. 

---

## Problem Description 

Most customers ignore marketing campaigns. This project tackles that by building a model to identify *which* customers are likely to respond positively, so the company can focus its budget where it actually counts.
 
> Only ~15% of customers responded to campaigns — this model helps find them before spending on the other 85%.
 
--- 

## Dataset
 
**Source:** [Marketing Campaign Dataset — Kaggle](https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis)
 
- **2,240 customers** with demographic, purchase, and campaign history data
- **Target variable:** `Response` — did the customer accept the most recent campaign? (binary: 0/1)
- 24 missing values in `Income` — dropped via `dropna()`
---
 
## ⚙️ Features Used
 
| Feature | Description |
|---|---|
| `Recency` | Days since last purchase |
| `Age` | Derived from Year_Birth |
| `Income` | Annual household income |
| `MntWines` / `MntMeatProducts` | Spending on wines and meat |
| `MntFruits` / `MntFishProducts` / `MntSweetProducts` / `MntGoldProds` | Other product spending |
| `NumDealsPurchases` | Purchases made with a discount |
| `Dt_Customer` | Years as a customer (engineered from join date) |
| `Marital_Status` | Label-encoded |
| `Education` | Label-encoded |
| `Complain` | Binary — has the customer complained? |
 
---
 
## Approach
 
1. **Data cleaning** — dropped 24 rows with missing `Income`
2. **Feature engineering** — converted join date to tenure (years), derived `Age` from birth year
3. **Encoding** — label-encoded categorical features (`Marital_Status`, `Education`)
4. **Scaling** — StandardScaler applied to continuous features only (categorical left unscaled)
5. **Train/test split** — 80/20 split, `random_state=42`
---
 
## Models
 
### Baseline — Logistic Regression
Simple, interpretable, good for understanding feature influence via coefficients.
 
### Main Model — Random Forest Classifier
Handles non-linear relationships and feature interactions; more robust to outliers.
 
---
 
## Results
 
| Metric | Logistic Regression | Random Forest |
|---|---|---|
| Accuracy | 85.6% | 87.2% |
| ROC-AUC | 0.572 | 0.611 |
| False Negatives | 56 | 51 |
| False Positives | 8 | 6 |
 
> Random Forest had fewer false negatives — meaning it missed fewer actual responders, which matters most for a campaign targeting problem.
 
---
 
## Key Insights
 
From feature coefficients (Logistic Regression) and feature importances (Random Forest):
 
- **Positive signals** → `Dt_Customer`, `MntWines`, `MntMeatProducts` — long-tenure customers who spend on wine and meat are more likely to respond
- **Negative signals** → `Recency`, `Age` — customers who haven't engaged recently, and older customers, are less likely to respond
- **Income** and **Recency** were among the top predictors by Random Forest importance
**Business takeaway:** Target loyal, high-spending customers who have interacted recently. Consider re-engagement campaigns specifically for long-dormant customers.
 
---
 
## Librabry used
 
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=flat&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4c72b0?style=flat&logoColor=white)
 
---
 
## Files
 
```
├── marketing_campaign.csv      # Dataset (tab-separated)
├── customer_campaign_response_prediction.ipynb  # Main notebook
└── README.md
```
 
---
 
## How to Run
 
```bash
# Clone the repo
git clone https://github.com/yashxp10/customer-campaign-response-prediction.git
cd customer-campaign-response-prediction
 
# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn
 
# Run the notebook
jupyter notebook customer_campaign_response_prediction.ipynb
```
 
---
 
*Part of my Data Science portfolio — BIT @ Macquarie University*
