# Decisions, Trade-offs & Assumptions

## Dataset
- **No file uploaded** → synthetic data generated to exactly match schema/stats from the case brief (50K rows, 7 cities, 9 cuisines, Jan–Mar 2025, ~24% surge rate as stated).
- Real analysis would start with `df.info()`, null checks, and outlier detection before any modelling.

## Forecasting Approach
- **Chose**: 7-day rolling average with day-of-week weekend multiplier.
- **Why not Prophet / ARIMA?**: Overkill for a 1-day investigation; interpretable baseline is more credible in a first presentation. The notebook explicitly notes upgrading to Prophet/LightGBM in production.
- **Granularity**: Daily (not hourly) — sufficient for rider pre-positioning planning; hourly adds noise without decision value at this stage.

## Surge Waste Estimation
- Assumed **Rs.35 incremental incentive per surge order** — a common industry placeholder. Real number to pull from Finance.
- "Off-peak" defined as hours where order volume < 60th percentile AND surge rate > 5%. Threshold is tunable.

## City Cohorts
- Manual segmentation (3 groups) based on visual inspection of peak hour distribution. With more data (≥6 months), k-means on hourly demand curves would be appropriate.

## A/B Test Design
- Control: 2 cities on current policy. Treatment: 2 cities with tightened windows.
- Duration: 14 days (≥7 days needed to capture weekly pattern twice).
- Primary metric: incentive spend/order. Secondary: P95 delivery time, rider fill-rate.
- Decision rule: if treatment saves >15% incentive with <2 min P95 degradation → roll out.

## What I Would Do With More Time
1. Pull real holiday calendar (Republic Day 26 Jan, Holi in March) and add as features.
2. Build hourly forecast (not just daily) using Prophet with regressors.
3. Streamlit dashboard for Ops Head self-serve cuts.
4. Quantify revenue impact of missed demand (unserved orders during peak due to poor rider supply).
