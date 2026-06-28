# Part 3: Regression-Based Business Insights & Model Interpretation

## Business Problem Summary

A retail chain's leadership team wants to understand what factors drive monthly sales performance across stores. They are considering business actions such as increasing marketing spend, improving inventory availability, changing discounting strategy, reallocating staff, and prioritising certain store types or regions. This analysis uses regression modelling to identify the strongest predictors of monthly sales and provide evidence-based recommendations.

---

## Dataset Description

**File:** `data/business_regression_data.xlsx`  
**Records:** 320 store-month observations (306 after cleaning missing values)  
**Stores:** 80 stores observed over 4 months (January–April 2025)

| Column | Type | Description |
|--------|------|-------------|
| store_id | Categorical | Unique store identifier |
| month | Date | Month of observation |
| region | Categorical | Geographic region (East, North, South, West) |
| store_type | Categorical | Store format (Residential, High Street, Airport, Mall) |
| marketing_spend | Numeric | Monthly marketing expenditure (£) |
| footfall | Numeric | Number of customer visits in the month |
| avg_discount_pct | Numeric | Average discount percentage applied |
| staff_count | Numeric | Number of staff employed |
| inventory_availability_pct | Numeric | % of SKUs in stock |
| competitor_distance_km | Numeric | Distance to nearest competitor (km) |
| holiday_flag | Binary | 1 if month includes a major holiday, 0 otherwise |
| customer_rating | Numeric | Average customer satisfaction score (1–5) |
| monthly_sales | Numeric | **Dependent variable** — total monthly sales (£) |
| monthly_profit | Numeric | Total monthly profit (£) — not used as predictor |

**Missing values:** 6 records missing competitor_distance_km; 8 records missing customer_rating. 14 records excluded from regression analysis.

---

## Dependent and Independent Variables

**Dependent Variable:** `monthly_sales`

**Independent Variables Selected for Modelling:**
- `footfall` — strongest numerical predictor
- `marketing_spend` — directly controllable business lever
- `inventory_availability_pct` — operational factor
- `customer_rating` — service quality proxy
- Region dummy variables: `region_North`, `region_South`, `region_West` (reference: East)

**Variables Excluded from Final Model:**
- `avg_discount_pct` — not significant in testing
- `staff_count` — correlated with footfall; excluded for parsimony
- `holiday_flag` — not significant on its own
- `competitor_distance_km` — missing values; marginal significance
- `monthly_profit` — outcome variable, not a predictor
- `store_id`, `month`, `store_type` — identifiers / handled via dummies

---

## Regression Approach

1. **Simple Regression 1:** footfall → monthly_sales (R² = 0.7348)
2. **Simple Regression 2:** marketing_spend → monthly_sales (R² = 0.1574)
3. **Multiple Regression (Final):** footfall + marketing_spend + inventory_availability_pct + customer_rating + 3 region dummies → monthly_sales (R² = 0.8137)

All regressions used Ordinary Least Squares (OLS). P-values reported from statsmodels.

---

## Dummy Variable Approach

The `region` variable (4 categories: East, North, South, West) was converted into 3 binary dummy variables:
- `region_North` = 1 if store is in North, else 0
- `region_South` = 1 if store is in South, else 0
- `region_West` = 1 if store is in West, else 0

**Reference Category: East** — all region coefficients are interpreted relative to East stores.

One category must be omitted to avoid perfect multicollinearity (the "dummy variable trap"). The East region was chosen as the reference as it had the largest number of records and serves as a natural baseline.

Store type dummies were created but excluded from the final model to maintain parsimony and avoid collinearity.

---

## Model Comparison Summary

| Model | R-Squared | Adj. R-Squared | Significant Predictors |
|-------|-----------|---------------|------------------------|
| Simple Reg 1 (Footfall) | 0.7348 | 0.7340 | footfall |
| Simple Reg 2 (Marketing) | 0.1574 | 0.1547 | marketing_spend |
| **Multiple Regression** | **0.8137** | **0.8093** | footfall, marketing_spend, inventory_avail, customer_rating, region_South, region_West |

---

## Final Model Selected

**Multiple Regression Model** (R² = 0.8137, Adj. R² = 0.8093)

**Equation:**
```
monthly_sales = 104,987.95 + 34.12×footfall + 1.21×marketing_spend 
               + 2,574.69×inventory_availability_pct + 11,175.48×customer_rating
               + 12,753.00×region_North + 25,460.69×region_South + 20,335.01×region_West
```

Selected because it explains the most variance, includes actionable predictors, and has strong statistical validation across most coefficients.

---

## Business Recommendation

1. **Prioritise footfall-driving strategies** — footfall is the dominant predictor of monthly sales.
2. **Improve inventory availability** — target 90%+ availability across all stores.
3. **Invest in customer experience** — each 1-point rating improvement is worth ~£11,175/month.
4. **Focus expansion in South and West regions** — both significantly outperform East.
5. **Review underperforming stores** — STR-1017, STR-1012, STR-1023, STR-1009, and STR-1077 show large negative residuals and should be operationally reviewed.

---

## Assumptions and Limitations

- Data covers only 4 months — seasonality and annual trends are not captured.
- Regression shows association, not causation. Controlled experiments are needed to confirm causal relationships.
- Store size, local demographics, and full competitive landscape are not measured.
- 14 records were dropped due to missing values — if missing data is non-random, this may introduce bias.
- Some predictors may be correlated (e.g., footfall and staff_count), which could affect coefficient stability.

---

## Screenshots Included

| File | Contents |
|------|----------|
| `screenshots/simple_regression_output.png` | Simple regression output (footfall model) |
| `screenshots/multiple_regression_output.png` | Multiple regression coefficient table |
| `screenshots/residuals_preview.png` | Predicted vs actual values with residuals |
| `screenshots/model_comparison_preview.png` | Model comparison summary table |

---

## Repository Structure

```
part3_regression_insights/
├── data/
│   └── business_regression_data.xlsx
├── analysis/
│   ├── regression_workbook.xlsx
│   ├── model_comparison.md
│   └── residual_analysis.md
├── outputs/
│   ├── regression_summary.xlsx
│   ├── final_recommendation.md
│   └── model_equations.md
├── screenshots/
│   ├── simple_regression_output.png
│   ├── multiple_regression_output.png
│   ├── residuals_preview.png
│   └── model_comparison_preview.png
└── README.md
```
