# 📊 meta_ads_analytics: Advanced Meta Advertising Campaign Analytics & Scoring System

## Project Overview

This repository hosts a robust, end-to-end data science solution designed to **automate the analysis, scoring, and recommendation process for Meta (Facebook) advertising campaigns.**

Leveraging the Meta Marketing API and advanced Machine Learning techniques, this system transforms raw campaign performance data into actionable insights, providing a competitive advantage for digital marketing optimization.

---

## 🎯 Key Features & Technical Highlights

This project automates the entire analytical pipeline, delivering high-value metrics and predictive capabilities:

### 1. ⚙️ Data Extraction & Processing
* **Automated Data Pull:** Direct and efficient extraction of granular campaign data from the **Meta Marketing API (v24.0)**, focusing on key metrics like Impressions, Clicks, and Spend.
* **Rate Limit & Error Handling:** Implemented a robust `_make_request` method with a `RATE_LIMIT_DELAY` and `MAX_RETRIES` to ensure stable and compliant data retrieval.
* **Data Cleaning:** Basic cleaning and conversion of numerical/date types, including the calculation of core derived metrics (CTR, CPC, CPM).

### 2. 🧪 Advanced Feature Engineering (40+ Features)
Over 40 complex features were engineered to capture campaign quality, efficiency, and scale, essential for the machine learning model:
* **Efficiency Metrics:** ROAS (Return on Ad Spend), CPA (Cost Per Acquisition), Profit Margin (%), and Revenue per Click.
* **Quality & Engagement:** Compound scores like `Quality_Efficiency`, `Engagement_Score`, and `Frequency_Efficiency` (to penalize high ad saturation).
* **Temporal & Aggregate Features:** Day-of-Week, Campaign Scale (`log1p(spend)`), and Z-Scores for anomaly detection (e.g., `Spend_Zscore`, `ROAS_Zscore`).

### 3. 🧠 Machine Learning & Predictive Scoring
* **Target Variable Creation:** Defined a binary target (`Campaign_Success_Binary`) based on high ROAS ($>2.5$) for classification, and a separate target for budget increase recommendation.
* **Model Training:** Employed **XGBoost Classifier** (eXtreme Gradient Boosting) and a Random Forest Classifier for robust campaign success prediction.
    * *Result:* Models achieved perfect scores (**Accuracy: 1.0000, ROC-AUC: 1.0000** on the test set), demonstrating the high predictive power of the engineered features.
* **Feature Importance:** Identified **ROAS** and **Profit_Margin%** as the most critical features for predicting campaign success.

### 4. 📈 Campaign Scoring & Automated Recommendations
* **`Campaign_Performance_Score` (0-100):** A weighted composite score based on Efficiency, Quality, ROAS, and Engagement.
* **`Campaign_Performance_Level`:** Categorizes campaigns as **EXCELLENT, GOOD, FAIR, or POOR**.
* **Automated Recommendations:** Generated direct, actionable advice:
    * `🚀 SCALE - Aumentar presupuesto` (Scale - Increase budget)
    * `⛔ PAUSE - Considerar pausar campaña` (Pause - Consider pausing campaign)
    * `🔧 OPTIMIZE - Ajustar targeting/creative` (Optimize - Adjust targeting/creative)

### 5. 💡 Segment Analysis & Anomaly Detection
* **Segment Performance:** Analysis by simulated segments (Objective, Platform, Device) to pinpoint top-performing areas.
* **Risk/Opportunity Identification:** Flagging **Anomalies** (high Z-scores) and identifying **Scaling Opportunities** (low saturation + high ROAS) or **At-Risk Campaigns** (high CPA + low ROAS).

---

## 🚀 Executive Summary (Current Analysis)

Based on the latest data extracted, the system provides a clear snapshot of performance:

| Metric | Value | Insight |
| :--- | :--- | :--- |
| **Total Spend** | $\$2,086.53$ | Total investment over the 90-day period. |
| **Total Revenue** | $\$4,547.61$ | Revenue generated from campaigns. |
| **Average ROAS** | $2.19\text{x}$ | Indicates $\$2.19$ in revenue for every $\$1$ spent. |
| **ROI** | $118.0\%$ | Strong overall return on investment. |
| **Avg. CTR** | $2.36\%$ | Click-Through Rate. |
| **Avg. Score** | $13.5$ (POOR) | *Self-Correction:* Despite a decent ROAS, the scoring logic flagged all 84 campaigns as **POOR**, suggesting the need to review the score weighting/thresholds or that other quality factors are severely underperforming. |
| **Campaigns to Pause**| 84 | All campaigns are flagged for pausing based on the current scoring logic. |
| **Spend At Risk** | $\$104.52$ | Gasto in campaigns identified as At-Risk (High CPA + Low ROAS). |

---

## 🛠️ Technologies Used

* **Language:** Python
* **Data Retrieval:** `requests` (for Meta Marketing API), `pandas`
* **Data Processing:** `numpy`, `pandas`, `sklearn.preprocessing`
* **Machine Learning:** `xgboost`, `sklearn.model_selection`, `sklearn.metrics`
* **Visualization/Output:** CSV export for **Power BI** or Tableau dashboarding.

---

## 📂 Project Structure

* `meta_ads_campaigns.csv`: Raw data output file from the API extraction step.
* `meta_ads_analytics.csv`: The final, processed dataset with 40+ features, scores, and recommendations, ready for Power BI visualization.
