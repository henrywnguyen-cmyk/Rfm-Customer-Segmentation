<div align="center">
  <h1>RFM Customer Segmentation</h1>
  <h2>Segmenting Ditch customers by Recency, Frequency, and Monetary value to prioritize retention and re-engagement</h2>
</div>

## Overview
This project segments Ditch's customer base using the RFM (Recency, Frequency, Monetary) framework, applied to real Shopify order data spanning **April 2025 – April 2026**. Each customer is scored on how recently they bought, how often they buy, and how much they've spent, then bucketed into six actionable segments — from Champions to One-Time Buyers — to guide marketing and retention decisions.

## What's Inside
The notebook walks through the full analysis end to end:

| Section | What it covers |
|---|---|
| Data Loading & Cleaning | Filters to paid, non-cancelled orders with valid emails; deduplicates multi-line-item orders; computes net revenue after refunds |
| RFM Metrics | Calculates recency (days since last order), frequency (unique orders), and monetary value (net spend) per customer |
| Scoring | Splits each metric into quintiles (1–5), with recency inverted so more recent = higher score |
| Segmentation | Maps R/F combinations into 6 segments: Champion, Loyal Customer, New Customer, At Risk, Win Back, One-Time Buyer |
| Visualizations | Segment size and revenue-share bar charts, a recency-vs-frequency scatter, and an R×F heatmap of average spend |
| Export | Outputs a clean `rfm_segments.csv` with anonymized customer IDs for use in other tools (e.g., email platforms, dashboards) |

## Segmentation Logic
| Segment | Criteria | Recommended Action |
|---|---|---|
| Champion | R≥4 & F≥4 | Reward, ask for reviews |
| Loyal Customer | R≥3 & F≥3 | Upsell, early access |
| New Customer | R≥4 & F≤2 | Second purchase campaign |
| At Risk | R≤2 & F≥3 | Re-engagement email |
| Win Back | R=1 & F≥2 | Last-chance discount |
| One-Time Buyer | Everything else | Nurture sequence |

## Key Insights
- **Champions drive outsized revenue** — 18.6% of customers generate 31.9% of all revenue, making retention of this group the highest-ROI focus area.
- **At Risk is the highest-urgency segment** — 7,974 customers who've ordered multiple times haven't returned in 263 days on average, representing the most recoverable revenue right now.
- **Most customers only order once** — median frequency is 1, pointing to a retention problem rather than an acquisition problem. A post-purchase email flow could shift this meaningfully.
- **Frequency drives spend more than recency** — the R×F heatmap shows that customers with the highest frequency score spend roughly 3x more than any other group, regardless of how recently they last bought. Converting first-time buyers into repeat buyers is the single biggest lever for revenue growth.

## Data Source
Built on Ditch's Shopify order export (`orders_cleaned.csv`), covering **95,282 line items across 54,830 unique orders**, filtered down to **49,411 valid paid orders from 36,062 unique customers** after cleaning. *(Note: this uses real company sales data — confirm internally whether it's appropriate to publish exact revenue and customer-count figures before making this repo public.)*

## Tools & Skills Used
- **Python** (pandas, numpy) — data cleaning, RFM metric calculation, quintile scoring
- **Matplotlib & Seaborn** — segment visualizations and the R×F heatmap
- **Jupyter Notebook** — end-to-end analysis and documentation

## Getting Started
1. Clone this repo and open `RFM_analysis.ipynb` in Jupyter.
2. Place your own cleaned orders CSV at the path referenced in the notebook (`orders_cleaned.csv`), matching the expected columns (`Name`, `Email`, `Created at`, `Total`, `Refunded Amount`, `Financial Status`, `Cancelled at`).
3. Run all cells top to bottom — the notebook will output segment charts and export `rfm_segments.csv`.

## Future Improvements
- Automate the segment definitions with configurable thresholds instead of hardcoded quintile cutoffs
- Add a cohort-based view to track how customers move between segments over time
- Layer in product-level data to see which product families are most associated with Champion-tier customers
- Build a lightweight dashboard (e.g., in Power BI or Streamlit) on top of the exported CSV for non-technical stakeholders

## Author
*[Your Name]* • [LinkedIn](#) • [GitHub](#)

## License
This project is available under the [MIT license](LICENSE).
