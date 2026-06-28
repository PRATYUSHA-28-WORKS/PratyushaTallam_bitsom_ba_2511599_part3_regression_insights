# Model Comparison Analysis

## Overview

Three regression models were built to understand the drivers of monthly sales across stores.

---

## Model 1: Simple Regression — Footfall

| Item | Detail |
|------|--------|
| **Model Name** | Simple Regression 1 — Footfall |
| **Dependent Variable** | monthly_sales |
| **Independent Variable** | footfall |
| **R-Squared** | 0.7348 |
| **Adjusted R-Squared** | 0.7340 |
| **Significant Variables** | footfall (p < 0.001) |
| **Business Usefulness** | High — footfall alone explains about 73% of the variation in monthly sales. This is a strong single-variable predictor. |
| **Limitations** | Does not account for marketing spend, regional effects, or operational factors. Cannot guide specific investment decisions beyond "drive more foot traffic." |

**Equation:**
```
monthly_sales = 447,699.03 + 35.64 × footfall
```

---

## Model 2: Simple Regression — Marketing Spend

| Item | Detail |
|------|--------|
| **Model Name** | Simple Regression 2 — Marketing Spend |
| **Dependent Variable** | monthly_sales |
| **Independent Variable** | marketing_spend |
| **R-Squared** | 0.1574 |
| **Adjusted R-Squared** | 0.1547 |
| **Significant Variables** | marketing_spend (p < 0.001) |
| **Business Usefulness** | Moderate — statistically significant but explains only 15.7% of variation. Marketing spend is associated with sales but is not the primary driver on its own. |
| **Limitations** | Very low explanatory power as a standalone model. Other major factors are completely absent. Likely suffers from omitted variable bias. |

**Equation:**
```
monthly_sales = 567,463.56 + 2.05 × marketing_spend
```

---

## Model 3: Multiple Regression (Final Model)

| Item | Detail |
|------|--------|
| **Model Name** | Multiple Regression — Full Model |
| **Dependent Variable** | monthly_sales |
| **Independent Variables** | footfall, marketing_spend, inventory_availability_pct, customer_rating, region_North, region_South, region_West |
| **R-Squared** | 0.8137 |
| **Adjusted R-Squared** | 0.8093 |
| **Significant Variables** | footfall (p<0.001), marketing_spend (p<0.001), inventory_availability_pct (p<0.001), customer_rating (p=0.024), region_South (p=0.001), region_West (p=0.002) |
| **Non-Significant** | region_North (p=0.088) — marginally significant |
| **Business Usefulness** | Very High — explains over 81% of variance. Provides actionable guidance across multiple levers: footfall, marketing, inventory, customer experience, and regional strategy. |
| **Limitations** | Observational data; regression shows association, not causation. Multicollinearity between footfall and other variables possible. Does not capture store size, local demographics, or competitive dynamics fully. |

**Equation:**
```
monthly_sales = 104,987.95 + 34.12×footfall + 1.21×marketing_spend 
               + 2,574.69×inventory_availability_pct + 11,175.48×customer_rating
               + 12,753.00×region_North + 25,460.69×region_South + 20,335.01×region_West
```
*(Reference category: East region)*

---

## Comparison Summary Table

| Metric | Simple Reg 1 (Footfall) | Simple Reg 2 (Marketing) | Multiple Regression |
|--------|------------------------|--------------------------|---------------------|
| R-Squared | 0.7348 | 0.1574 | **0.8137** |
| Adj. R-Squared | 0.7340 | 0.1547 | **0.8093** |
| # Predictors | 1 | 1 | 7 |
| Significant Vars | footfall | marketing_spend | 6 of 7 |
| Business Actionability | Medium | Low | **High** |

---

## Conclusion

The **Multiple Regression Model** is the clear best choice:
- It explains ~81% of monthly sales variation (vs 73% for the best simple model)
- It identifies six actionable business levers
- The inclusion of dummy variables for region accounts for geographic effects
- The adjusted R-squared confirms the improvement is not merely from adding more variables
