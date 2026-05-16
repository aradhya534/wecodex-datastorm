# wecodex-datastorm
## Team: WeCodex

## Problem
Predict the Maximum Monthly Purchase Potential (liters) for 20,000 
traditional trade outlets across 4 Sri Lankan provinces for January 2026.

## Pipeline Structure

| Layer | Folder | Description |
|---|---|---|
| Bronze | `bronze/` | Raw data preserved exactly as ingested |
| Silver | `silver/` | Cleaned data after all quality checks |
| Gold | `gold/` | Features + final predictions |
| Quarantine | `quarantined/` | Rejected records with documented reasons |
| Reports | `reports/` | EDA and feature importance charts |

## How to Run

1. Upload all 5 CSV source files to Colab root directory:
   - `transactions_history_final.csv`
   - `outlet_master.csv`
   - `outlet_coordinates.csv`
   - `distributor_seasonality_details.csv`
   - `holiday_list.csv`
2. Open `wecodex.ipynb` in Google Colab
3. Run all cells top to bottom
4. Final predictions saved to `gold/wecodex_predictions.csv`

## Data Quality Issues Found & Fixed

| Issue | Dataset | Count | Action |
|---|---|---|---|
| Duplicate rows | holidays | 93 | Removed |
| Missing Outlet_Size | outlets | 196 | Imputed with mode |
| Zero/negative volume | transactions | 4,853 | Quarantined |
| Outlet_Type typos | outlets | 595 | Standardized |
| Coordinates outside Sri Lanka | coords | checked | Flagged |

## Modeling Approach

- **Target variable:** `peak_month_volume` (proxy for uncapped demand)
- **Model:** Gradient Boosting Regressor
- **Train R²:** 0.9859
- **Test R²:** 0.9776
- **Top features:** mean_bill_value, mean_volume, std_volume

## Potential Formula
Potential = GBM_prediction × season_multiplier × poi_multiplier
## Results

- Outlets predicted: 20,000
- Mean potential: 382 liters/month
- Max potential: 2,181 liters/month

