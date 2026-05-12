# Case 3 — Food Delivery Demand Pulse

## TL;DR
Three months of food-delivery orders (50K rows, 7 cities) were analysed to find when demand *actually* peaks — and where we're wasting surge incentives. We found two 4-hour peak windows per day vs. a 15+ hour window currently incentivised, city demand profiles that differ by 2 hours, and ~38% of surge spend going to off-peak orders.

## Entry Points
| File | What It Is |
|------|-----------|
| `deck.pdf` | 5-slide Ops Head briefing — start here |
| `demand_pulse_notebook.ipynb` | Full analysis: EDA → city cohorts → forecast |
| `delhi_demand_forecast.csv` | 7-day Delhi daily demand forecast with 80% CI |
| `case3_food_delivery_orders.csv` | Synthetic dataset (50K rows, matches spec) |
| `DECISIONS.md` | Trade-offs and assumptions |

## How to Run the Notebook
```bash
pip install pandas numpy matplotlib scikit-learn jupyter
jupyter notebook demand_pulse_notebook.ipynb
```
Run top-to-bottom — all cells are self-contained.

## 3 Recommendations (30-second version)
1. **Tighten surge windows** to 12–14h and 19–22h only → save ~Rs.2.5L/month
2. **City-specific schedules** (3 cohorts) → +8–12% rider fill-rate at true peak
3. **Proactive weekend surge** (lower threshold Fri–Sun) → –4–6 min P95 delivery time

## Stretch Goals Delivered
- [x] City cohort analysis (3 behavioural groups)
- [x] A/B test design for Recommendation 1 (slide 5)
- [ ] Streamlit dashboard (not included — would require deployment)
