# Residual Analysis

## What Are Residuals?

A residual is the difference between the **actual monthly sales** of a store and the **predicted monthly sales** from our multiple regression model:

```
Residual = Actual Sales − Predicted Sales
```

- A **positive residual** means the store performed *better* than the model expected.
- A **negative residual** means the store performed *worse* than the model expected.

---

## Final Model Used

**Multiple Regression Model**
- Predictors: footfall, marketing_spend, inventory_availability_pct, customer_rating, region_North, region_South, region_West
- R-Squared: 0.8137

---

## Top 5 Records with Largest Positive Residuals

| Store ID | Actual Sales (£) | Predicted Sales (£) | Residual (£) | Store Type | Region |
|----------|-----------------|---------------------|--------------|------------|--------|
| STR-1028 | 713,611 | 582,777 | +130,834 | Mall | East |
| STR-1026 | 625,514 | 519,469 | +106,045 | Mall | East |
| STR-1051 | 787,716 | 687,317 | +100,398 | Airport | East |
| STR-1073 | 813,317 | 719,225 | +94,092 | Residential | East |
| STR-1064 | 799,047 | 707,639 | +91,408 | Airport | South |

### Business Interpretation — Positive Outliers

These stores are significantly **outperforming** model expectations. Possible reasons:
- **Mall stores (STR-1028, STR-1026)** may benefit from anchor tenants, local events, or promotional synergies not captured in the data.
- **Airport stores (STR-1051, STR-1064)** may have captive customer bases or above-average transaction values from travellers that the model underestimates.
- These stores may have **management practices, local marketing, or customer loyalty** factors that explain the outperformance but are not measured in the dataset.
- These stores represent best-practice benchmarks for the business.

---

## Top 5 Records with Largest Negative Residuals

| Store ID | Actual Sales (£) | Predicted Sales (£) | Residual (£) | Store Type | Region |
|----------|-----------------|---------------------|--------------|------------|--------|
| STR-1017 | 685,379 | 840,661 | −155,282 | High Street | West |
| STR-1012 | 595,468 | 732,020 | −136,553 | Residential | West |
| STR-1023 | 627,172 | 760,539 | −133,368 | Mall | South |
| STR-1009 | 641,865 | 767,046 | −125,181 | Residential | North |
| STR-1077 | 538,376 | 650,622 | −112,246 | Residential | South |

### Business Interpretation — Negative Outliers

These stores are significantly **underperforming** relative to their predictor profile. Possible reasons:
- **High Street store (STR-1017)** may be impacted by local competition, access issues, or declining footfall patterns in that specific high street that are not reflected in recorded footfall counts.
- **Residential stores underperforming** (STR-1012, STR-1009, STR-1077) may indicate that some residential store locations are saturated or face demographic challenges not captured in the model.
- The model may be **over-predicting for stores with high footfall but low conversion rates** — footfall counts do not distinguish between browsing and buying customers.
- These stores should be flagged for **operational review** to identify correctable issues.

---

## Patterns in Residuals

| Observation | Insight |
|-------------|---------|
| Airport stores tend to have positive residuals | Model may systematically under-predict Airport store sales |
| Some High Street and Residential stores show large negative residuals | Model may over-predict for certain location types with footfall that doesn't convert |
| East region stores feature prominently in the positive residuals | East region may have unmeasured advantages |

---

## Model Over- and Under-Prediction Assessment

- The model appears to **under-predict Airport store performance** — Airport stores have unique demand characteristics (captive audience, higher average transaction values) not fully captured by footfall alone.
- The model may **over-predict for High Street stores** in competitive or declining locations where recorded footfall does not translate to proportional sales.
- The overall residual pattern suggests the model is well-calibrated for most stores (R² = 0.8137) but the extreme residuals point to **store-type-specific effects** that a more granular model (e.g., including store_type dummies) might capture.

---

## Recommendation from Residual Analysis

1. **Investigate Airport stores** as potential outperformers and consider whether the business should prioritise this format.
2. **Conduct store-level reviews** for STR-1017, STR-1012, STR-1023, STR-1009, and STR-1077 to identify operational or market-level issues.
3. Consider **adding store_type dummy variables** to the next iteration of the model to better capture format-level effects.
