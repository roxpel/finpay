# 📊 FinPay Subscriptions Uplift: Predictive Targeting Solution

## 🧠 Project Summary

FinPay is seeking to accelerate adoption of its Subscriptions product among existing merchants. Leveraging FinPay’s merchant and payment data, I developed a robust, data-driven **propensity modeling framework** to surface the highest-potential merchants for targeted sales and marketing outreach.

This approach combines:
- Exploratory analysis  
- Targeted feature engineering  
- Advanced machine learning  

The goal: prioritize segments with the greatest likelihood to convert — enabling FinPay to deploy GTM resources efficiently and maximize product adoption.

---

## 1. 🎯 Approach

To address the challenge, I framed the problem as a **binary classification task**: predict which merchants are most likely to adopt Subscriptions, based on:
- Historical product usage
- Business metadata
- Payments volume data

I established a baseline using **Logistic Regression**, then advanced to **XGBoost** to better capture nonlinear interactions, mitigate class imbalance, and optimize recall — critical for maximizing the upsell pool.

---

## 2. 🔍 EDA

### Key Insights:
- 🇺🇸 The US and Software/Tech verticals account for the majority of FinPay’s merchant base.
- 📉 Subscriptions are underpenetrated: **<20%** of merchants have adopted the product.
- 🔗 Most merchants rely on Custom API, Payment Link, or Checkout only — key whitespace for upsell.
- ⚠️ Severe class imbalance and potential data leakage (cohort features reflecting Subscription status) shaped our modeling and feature engineering strategy.

---

## 3. 🛠️ Feature Engineering & Data Preparation

### Numeric Features:
- Applied **winsorization** at the 99th percentile (e.g., `total_volume`) to reduce outlier impact.
- Used **log transforms** on `total_volume` and `tenure_years` to reduce right skew.

### Categorical Features:
- **Grouped and bucketed** industry, country, and product usage cohorts to avoid sparsity and overfitting.
- Applied **one-hot encoding** after bucketing.
- Imputed missing values:
  - Mean for numeric features
  - “Other” or “Unknown” for categorical
- **Prevented data leakage** by excluding Subscription data from usage cohort definitions.

All preprocessing was handled in **cross-validated, reproducible pipelines**.

---

## 4. 🧪 Modeling & Evaluation

### Strategy:
- **Validation**: 80/20 stratified split with cross-validation
- **Baseline**: Logistic Regression
- **Final Model**: Tuned XGBoost, selected for its performance with imbalanced data and business relevance
- **Threshold Tuning**: Adjusted to `0.30` to increase recall

### Evaluation Metrics (Tuned XGBoost):

| Metric                      | Score |
|----------------------------|-------|
| ROC AUC                    | 0.77  |
| PR AUC                     | 0.56  |
| Recall (Subscribed class)  | 0.83  |
| Precision (Subscribed)     | 0.30  |

---

## 5. 📈 Results & Targeting Recommendations

### Top Segments by Propensity Score (Top 20%):
- 🇺🇸 **United States**: 56% of top scorers (**+23pp over base**)
- 💻 **Software/Tech**: 38% (**+21pp**)
- 🔗 **Payment Link** users: 32% (**+15pp**)

**Custom API/Terminal** usage was underrepresented, suggesting lower incremental opportunity.

### Cross-Unit Analysis:
- **Best-fit upsell targets**: US-based Software/Tech and Business Services using Payment Link or API.
- **High-potential regions**: 🇬🇧 UK, 🇨🇦 Canada, 🇦🇺 Australia, 🇫🇷 France — particularly for high-tech verticals.

> 📊 **Lift**: Top 20% of scored merchants captures ~41% of all subscribers — a **2.1× improvement** over random targeting.

---

## 6. 📊 Model Evaluation & Monitoring

Robustness and reliability priorities included:

- Emphasis on **recall** and **PR AUC**, not accuracy, due to class imbalance
- All splits/pipelines designed to avoid leakage and class bias
- Ongoing recalibration recommended as cohorts and campaigns evolve

---

## 7. 🚀 How FinPay Should Use This Solution

The model supports a tactical, data-driven GTM motion:

- **High-priority outreach**: Route US-based Software/Tech leads to SDRs for sandbox demos and 1:1 follow-up
- **Lifecycle marketing**: Trigger in-app/email nudges for non-Subscription merchants using Payment Link or Checkout
- **Expansion**: Target high-fit verticals in UK, Canada, Australia, and France
- **Sales enablement**: Provide prioritized lead lists + tailored messaging/scripts to sales

---

## 8. 🔄 Next Steps (If More Resources)

### 📌 Feature Expansion:
- Use behavioral signals (support tickets, engagement logs, etc.)
- Detect recurring payments to flag “hidden” subscription use cases

### ⚙️ Model Enhancements:
- Test uplift or ensemble models to sharpen targeting

### 🧪 Experimentation:
- A/B test outreach to high-propensity leads vs. baseline cohorts to measure uplift

---

## 🗂 Supporting Assets

- 📓 [Notebook: `finpay_subscription_propensity_model.ipynb`](./finpay_subscription_propensity_model.ipynb)  
- 📦 [Data (zipped): `drive-data-download.zip`](./drive-data-download.zip)

---

## 📌 Disclaimer

> This project was built using **synthetic data** provided for a take-home case study.  
> “FinPay” is a fictional company name used solely for demonstration purposes.  
> No proprietary information, datasets, or internal processes from any real company were used or disclosed.
