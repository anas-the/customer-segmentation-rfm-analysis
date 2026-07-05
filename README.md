# customer-segmentation-rfm-analysis
# Customer Segmentation & RFM Analysis

Customer-level analytics project applying the RFM (Recency, Frequency, Monetary) framework and weekly cohort retention analysis to identify high-value customers, quantify revenue concentration, and inform targeted retention strategies.

---

## Business Problem
Not all customers contribute equally to revenue. Without segmentation, businesses risk spending equal marketing and retention effort across all customers — wasting resources on low-value segments while under-investing in high-value ones. This project segments customers based on actual purchasing behavior and tracks short-term retention patterns to identify where retention efforts will have the greatest business impact.

---

## Dataset

- **Source:** [E-Commerce Behavior Data (REES46 Marketing Platform)](https://www.kaggle.com/datasets/mkechinov/ecommerce-behavior-data-from-multi-category-store) — Kaggle
- **Period:** November 2019
- **Scope:** 137,931 purchase events across 108,648 unique customers (drawn from a 15% representative sample of the original 67.5M-event dataset)

**Note on data scope:** This dataset covers a single month. As a result, "Recency" and cohort retention are measured within this observation window rather than across a long-term customer lifecycle. This limitation is addressed transparently throughout the analysis.

---

## Tools Used

| Category | Tools |
|---|---|
| Data Processing | Python (Pandas, NumPy) |
| Visualization | Matplotlib, Seaborn |
| Analysis | Jupyter Notebook |
| Techniques | RFM Segmentation, Cohort Analysis, Retention Analysis |

---

## Key Findings

### 1. RFM Segmentation
Customers were scored on Recency, Frequency, and Monetary value (1–5 quantile-based scoring) and grouped into 6 actionable segments:

| Segment | Customers | Revenue Share | Avg. Revenue/Customer |
|---|---|---|---|
| Champions | 14,838 (13.7%) | **34.5%** | $962.58 |
| Loyal Customers | 36,762 (33.8%) | 20.1% | $227.07 |
| Needs Attention | 23,712 (21.8%) | 15.4% | $268.97 |
| At Risk (High Value) | 5,703 (5.2%) | 11.5% | $836.06 |
| Lost Customers | 15,599 (14.4%) | 10.2% | $272.33 |
| New Customers | 12,034 (11.1%) | 8.3% | $284.87 |

**Insight:** Champions represent only 13.7% of customers but generate 34.5% of total revenue — a 2.5x overrepresentation. The "At Risk (High Value)" segment, though small, has the second-highest average revenue per customer ($836), meaning these are high-value customers at real risk of churning.

### 2. Cohort Retention Analysis
Weekly retention was tracked for customers grouped by the week of their first purchase:

| Cohort Week | Week 0 | Week 1 | Week 2 | Week 3 | Week 4 |
|---|---|---|---|---|---|
| 44 | 100% | 10.1% | 8.0% | 5.4% | 4.1% |
| 45 | 100% | 8.2% | 5.1% | 3.9% | — |
| 46 | 100% | 4.1% | 2.7% | — | — |
| 47 | 100% | 5.7% | — | — | — |
| 48 | 100% | — | — | — | — |

**Insight:** Retention drops sharply after Week 0 across all cohorts — fewer than 10% of customers return for a repeat purchase within a week of their first purchase. This aligns with the RFM finding that a large share of customers fall into "New" or "Lost" categories rather than "Loyal" or "Champion" segments.

---

## Visualizations

**Revenue Share by Customer Segment**
![Segment Revenue](charts/segment_revenue_chart.png)

**Customer Share vs Revenue Share**
![Customer vs Revenue Share](charts/customer_vs_revenue_share_chart.png)

**Weekly Cohort Retention Heatmap**
![Cohort Retention Heatmap](charts/cohort_retention_heatmap.png)

---

## Business Recommendations

1. **Protect the Champions segment** (34.5% of revenue from 13.7% of customers) with personalized loyalty rewards and priority service — losing even a small fraction of this segment would have an outsized revenue impact.
2. **Launch an urgent win-back campaign** for the At Risk (High Value) segment — targeted discounts or personalized outreach before these high-spending customers fully churn. Recovering even 20% of this segment could preserve roughly $950K in revenue.
3. **Introduce a time-limited second-purchase incentive** (e.g., a discount code valid for 3–5 days after first purchase) to counter the sharp Week 0 → Week 1 retention drop-off and convert one-time buyers into repeat customers.
4. **Convert New Customers into Loyal Customers** through onboarding nudges and early engagement campaigns, given their currently low frequency and revenue contribution.

---

## Project Structure

```
customer-segmentation-rfm-analysis/
│
├── notebooks/
│   ├── 05_Customer_Segmentation_RFM.ipynb
│   └── 06_Cohort_Retention_Analysis.ipynb
│
├── reports/
│   ├── rfm_customer_data.csv
│   ├── segment_revenue_summary.csv
│   └── cohort_retention_matrix.csv
│
├── charts/
│   ├── segment_revenue_chart.png
│   ├── customer_vs_revenue_share_chart.png
│   └── cohort_retention_heatmap.png
│
└── README.md
```

---

## Methodology Notes

- RFM scores were calculated using quantile-based binning (`pd.qcut`); Frequency was ranked before binning to handle a large number of tied values (many customers with exactly 1 purchase).
- Cohort weeks were assigned using ISO calendar week numbers; retention percentages are relative to each cohort's Week 0 size.
- Revenue and monetary values are approximated using `price` on `purchase` events, as the dataset does not include a separate order/transaction table.
- This analysis is a companion piece to the [E-Commerce Product Analytics: Funnel, Conversion & Revenue Optimization](https://github.com/anas-the/E-Commerce-Product-Analytics-Funnel-Conversion-Optimization) project, using the same underlying dataset from a customer-centric lens.

---

## Author

**Mohd Anas**
[LinkedIn](https://www.linkedin.com/in/mohdanasnsut/) | mohdanas9832@gmail.com
