# Saudi National Day Demand Forecasting

A machine learning case study for forecasting product demand and optimizing inventory for the Saudi National Day season using historical e-commerce sales data.

## Project Overview

This project analyzes historical sales patterns for a simulated home décor and gifts store operating on Zid. It explores seasonality, prepares product-level daily demand data, and builds a machine learning model to support two business decisions:

* How many units of each product should be stocked for the season?
* When should the promotional campaign begin?

## Dataset

The dataset covers the period from July 1, 2024, to August 10, 2026, and includes two complete Saudi National Day seasons.

* `orders.csv`: Historical order-line data.
* `products.csv`: Product names, categories, costs, and launch dates.
* `calendar.csv`: Seasonal, promotional, Ramadan, and Eid indicators.

The dataset includes:

* 118,602 order-line records
* 25 products
* 771 calendar days

## Project Workflow

1. Data loading and inspection
2. Data quality checks
3. Data integration
4. Daily product-level aggregation
5. Exploratory data analysis
6. Stockout and outlier treatment
7. Feature engineering
8. Temporal train-test split
9. Baseline model development
10. Random Forest training and evaluation
11. 2026 demand forecasting
12. Inventory and budget recommendations

## Model

The final model is a `RandomForestRegressor` trained using:

* Product ID
* Product category
* Day of the week
* Month
* National Day season indicator
* Promotion indicator
* Demand from the same product 365 days earlier

A growth-adjusted prior-year forecast was used as the baseline model.

## Model Performance

| Metric                                    |             Result |
| ----------------------------------------- | -----------------: |
| Model MAE                                 | 5.11 units per day |
| Baseline MAE                              | 6.57 units per day |
| RMSE                                      |         6.90 units |
| Seasonal product-level MAPE               |              12.0% |
| Validation windows outperforming baseline |       14 out of 14 |

## Key Results

* Expected demand for the 2026 season: **6,941 units**
* Recommended inventory with a 15% safety margin: **7,984 units**
* Estimated full inventory cost: **SAR 195,573**
* Recommended campaign launch date: **September 8, 2026**

Historical demand began rising materially on:

* September 13, 2024
* September 12, 2025

The campaign date was selected four to five days before the historical demand ramp-up.

## Top Inventory Recommendations

| Product                        | Predicted Demand | Recommended Stock |
| ------------------------------ | ---------------: | ----------------: |
| Saudi flag, desk size          |              531 |               611 |
| Green LED string lights, 10m   |              450 |               518 |
| Saudi flag mug                 |              399 |               459 |
| Projection lamp, KSA landmarks |              397 |               457 |
| Saudi flag, large outdoor      |              389 |               447 |

## Budget-Constrained Plan

The complete inventory recommendation exceeds the assumed SAR 50,000 budget.

The budget allocation method:

1. Preserves coverage across all products.
2. Prioritizes products with higher forecast confidence.
3. Considers expected profit margin.
4. Does not exceed each product’s recommended stock.

Final budget plan:

* Total purchased units: **2,047**
* Total cost: **SAR 49,999**
* Remaining budget: **SAR 1**

## Special Cases

### Product P004: Stockout

P004 recorded zero sales for 14 consecutive days because of a stockout. These values were replaced using the corresponding prior-year sales adjusted by the store growth rate.

### Product P025: New Product

P025 had no previous National Day season history. Its forecast was estimated using recent sales and the seasonal behavior of comparable products in the same category. Its prediction is therefore classified as low confidence.

## How to Run

1. Open `Zid_case_study_English_Completed.ipynb` in Google Colab.

2. Upload the following files to the Colab session:

   * `orders.csv`
   * `products.csv`
   * `calendar.csv`

3. Select **Runtime → Run all**.

4. Review the model evaluation, inventory plan, budget allocation, and recommendation memo.

## Requirements

```text
numpy
pandas
matplotlib
scikit-learn
```

Google Colab already includes these libraries.

## Limitations

* The model does not estimate the causal effect of a new promotional campaign.
* Stockouts may hide demand that was not recorded as sales.
* One-time promotions may not repeat in future seasons.
* P025 has limited historical data.
* Forecasts should be updated during the season using actual sales and inventory availability.

## Disclaimer

This project uses simulated data and was developed for educational purposes as part of a demand forecasting case study.
