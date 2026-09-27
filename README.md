# Retail Demand Forecasting

Forecasting daily store-item sales demand using 5 years of real retail transaction data, to support inventory and staffing decisions.

## Problem

Retailers need to predict future product demand at the store-item level to avoid two costly outcomes: stockouts (lost sales, unhappy customers) and overstock (wasted capital, especially on perishable or seasonal goods). This project builds and evaluates increasingly sophisticated forecasting approaches to address this.

## Dataset

- **Source:** [Kaggle — Store Item Demand Forecasting Challenge](https://www.kaggle.com/c/demand-forecasting-kernels-only/data)
- **Size:** 913,000 daily sales records
- **Scope:** 10 stores × 50 items, January 2013 – December 2017
- **Quality:** Complete dataset, no missing values after minor cleaning

## Methodology

1. **Data validation** — checked structure, types, and completeness before analysis
2. **Exploratory analysis** — identified seasonal, weekly, and store-level demand patterns
3. **Baseline modeling** — started with a naive historical-average model to establish a benchmark
4. **Iterative improvement** — progressively added seasonality, weekday, and recent-sales-trend features
5. **Machine learning** — trained a Random Forest Regressor and compared it against simpler grouped-average approaches
6. **Evaluation** — used Mean Absolute Error (MAE) throughout, with a proper time-based train/test split (no data leakage)

## Key Findings

- **Seasonality:** Sales roughly double from a January low (~2.75M units) to a July peak (~5.19M units)
- **Weekly pattern:** Sales climb steadily across the week, from a Monday low to a Sunday peak (~50% swing) — a gradual trend rather than a sudden weekend spike
- **Store variation:** Top-performing store outsells the lowest by roughly 2x
- **Item concentration:** Demand is spread fairly evenly across top-selling items, with no single dominant product

## Modeling Results

| Model | Mean Absolute Error | Improvement vs. baseline |
|---|---|---|
| Naive baseline (historical average) | 10.19 | — |
| + Month (seasonality) | 10.15 | 0.5% |
| + Weekday | 8.82 | 13.4% |
| Random Forest (same features) | 8.83 | 13.4% |
| **Random Forest + 7-day sales lag** | **8.17** | **19.8%** |

**Feature importance** (from the final model) showed that recent sales history (`sales_lag_7`) accounted for ~89% of predictive power — far more than calendar features like month, weekday, store, or item combined.

## Business Recommendation

Inventory and staffing decisions should weight **recent sales trends** more heavily than seasonal calendars, particularly for fast-moving items where week-to-week demand can shift quickly.

## Limitations

This analysis relies solely on internal sales history. It does not account for external factors such as promotions, holidays, pricing changes, weather, or competitor activity — all of which likely influence real-world demand and could improve accuracy further if incorporated.

## Tech Stack

- Python, pandas, matplotlib
- scikit-learn (Random Forest Regressor)
- Google Colab

## Files

- `retail_demand_forecasting.ipynb` — full analysis notebook (EDA, modeling, evaluation)

---
*Author: Samra Mariyam — https://www.linkedin.com/in/samramariyam/*
