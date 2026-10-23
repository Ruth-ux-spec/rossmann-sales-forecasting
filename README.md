# Rossmann Store Sales Forecasting

Forecasting daily sales for 1,115 Rossmann drug stores across Germany, six weeks ahead. This is Module 4 of the CadetX Practice Lab.

## Business question
"Predict daily sales for each store, six weeks into the future, and tell us how much we can trust the numbers."

## Data
The datasets come from the CadetX Practice Lab and are not included in this repository:
- rossmann_train.csv: daily sales history (1,017,209 rows)
- rossmann_store.csv: store details (1,115 stores)
- rossmann_test.csv: the period to forecast (41,088 rows)

## Approach
1. *Load and merge:* joined store details to the sales data on Store (left join).
2. *Clean:* removed closed days and open days with zero sales (1,017,209 to 844,338 rows).
3. *Time-based split:* trained on data up to 19 Jun 2015 and validated on the final 6 weeks, to avoid future-to-past leakage.
4. *Feature engineering:* sales lags at 42 and 49 days, a Promo2Active flag, and competitor age (capped at 120 months).
5. *Model and evaluation:* compared a moving-average baseline against a gradient boosting model, using RMSPE.

## Results

| Approach | RMSPE |
|---|---|
| Baseline (8-week weekday average per store) | 0.273 |
| Gradient boosting model | 0.168 |

The model's error is about 39% lower than the baseline.

## How much to trust the numbers
- A typical daily forecast is within about 10 to 13% of actual sales.
- Errors are similar across store types (RMSPE 0.139 to 0.174).
- A few days are badly off, so single-day forecasts are estimates.
- Results come from one 6-week validation window, so accuracy in other seasons is untested
