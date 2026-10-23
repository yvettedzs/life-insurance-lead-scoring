# Life Insurance Lead Prioritisation

An end-to-end lead scoring and reporting project: Python generates the data, DuckDB SQL scores and tiers the leads, and Power BI delivers the dashboard. It gives a sales team a ranked call list.

## Business question
Which leads should sales call first, and does the scoring model actually separate buyers from non-buyers?

## Key results (8,000 synthetic leads)
| Tier | % of leads | Historical conversion |
|---|---|---|
| Platinum | 5% | 41.4% |
| Gold | 15% | 31.6% |
| Silver | 39% | 19.4% |
| Bronze | 41% | 10.9% |

- Overall conversion is 18.8%. Platinum and Gold convert about **1.8x better than average**.
- Contacting the top 20% of leads (Platinum and Gold) captures about **36% of conversions**.
- Platinum brings in the least total revenue but the most expected revenue per lead.
- **Channel matters:** Referral (24.4%) and Partner Bank (22.5%) leads convert best, against 15.9% for Paid Social, so referral and partner programmes are worth expanding, subject to cost per lead.
- **Top leads are rare:** the score distribution is right-skewed and only 5% of leads reach Platinum, so each one can get an immediate, personal follow-up.
- **Don't discard Bronze:** it is 41% of leads but about 24% of expected revenue, so route it to low-cost automated nurturing instead of the sales queue.

## Pipeline
1. **Python:** generates the synthetic lead data (life-stage triggers, engagement, source, product, premium, agent, date). A fixed seed makes it reproducible.
2. **DuckDB SQL:** calculates a rule-based Lead Score and assigns tiers. The cutoffs (42 / 78 / 109) are set from the score distribution so tier sizes fit sales capacity.
3. **Power BI:** a 3-page report with DAX measures (conversion, lift, expected revenue, cumulative gains).

## Dashboard pages
- **Executive Summary:** KPI cards, conversion and expected revenue by tier, cumulative gains curve, monthly trend, slicers.
- **Analysis:** conversion by source, tier × age band matrix, score distribution, agent table.
- **Lead List:** drill-through from any tier to a ranked call list.

## Files
- `insurance_synthetic_data_creation.ipynb`: data generation and SQL scoring
- `Insurance_Lead_Analytics_Dashboard_Oct_2026.pbix`: Power BI report (opens in the free Power BI Desktop)
- `Insurance_Lead_Analytics_Dashboard_Oct_2026.pdf`: static copy of the report

## Notes and limitations
- The data is **synthetic**. Conversion was generated from the same weights as the score, so the results show the model works as designed, not that it predicts real-world behaviour.
- Agent assignment is random, so differences between agents are noise.
- With real data I would calibrate the weights from actual conversion history (for example with logistic regression) and recalibrate the tier cutoffs.

## Tools
Python (pandas, NumPy), DuckDB SQL, Power BI (DAX)
