# Model Equations and Dummy Variable Explanation

## Simple Regression Equations

### Model 1: Footfall → Monthly Sales

```
monthly_sales = 447,699.03 + 35.64 × footfall
```

| Component | Value | Business Meaning |
|-----------|-------|-----------------|
| Intercept | 447,699.03 | Baseline monthly sales when footfall is zero (theoretical floor) |
| Footfall coefficient | +35.64 | Each additional store visitor is associated with approximately £35.64 more in monthly sales |
| R-Squared | 0.7348 | Footfall alone explains 73.5% of the variation in monthly sales |
| P-value (footfall) | <0.001 | This relationship is highly statistically significant |

**Business Interpretation:** Footfall is the single strongest predictor of monthly sales. Strategies that drive more customers into stores — location selection, promotional events, local advertising — are likely to have the highest impact.

---

### Model 2: Marketing Spend → Monthly Sales

```
monthly_sales = 567,463.56 + 2.05 × marketing_spend
```

| Component | Value | Business Meaning |
|-----------|-------|-----------------|
| Intercept | 567,463.56 | Baseline monthly sales with zero marketing spend |
| Marketing coefficient | +2.05 | Each additional £1 of marketing spend is associated with approximately £2.05 more in monthly sales (positive but modest ROI) |
| R-Squared | 0.1574 | Marketing spend alone explains only 15.7% of sales variation |
| P-value (marketing_spend) | <0.001 | Relationship is statistically significant |

**Business Interpretation:** While marketing spend is statistically significant, it has relatively low standalone explanatory power. Marketing likely works in conjunction with other factors (e.g., footfall conversion) rather than in isolation.

---

## Multiple Regression Equation (Final Model)

```
monthly_sales = 104,987.95
              + 34.12 × footfall
              + 1.21 × marketing_spend
              + 2,574.69 × inventory_availability_pct
              + 11,175.48 × customer_rating
              + 12,753.00 × region_North
              + 25,460.69 × region_South
              + 20,335.01 × region_West
```

### Coefficient Explanations

| Variable | Coefficient | P-value | Business Interpretation |
|----------|-------------|---------|------------------------|
| Intercept | 104,987.95 | 0.036 | Theoretical baseline sales when all predictors are zero |
| footfall | +34.12 | <0.001 | Each extra visitor → +£34.12 in monthly sales |
| marketing_spend | +1.21 | <0.001 | Each extra £1 of marketing → +£1.21 in sales (after controlling for other factors) |
| inventory_availability_pct | +2,574.69 | <0.001 | Each 1% improvement in stock availability → +£2,575 in monthly sales |
| customer_rating | +11,175.48 | 0.024 | Each 1-point improvement in rating → +£11,175 in monthly sales |
| region_North | +12,753.00 | 0.088 | North stores earn ~£12,753 more than East stores (marginal significance) |
| region_South | +25,460.69 | 0.001 | South stores earn ~£25,461 more than East stores |
| region_West | +20,335.01 | 0.002 | West stores earn ~£20,335 more than East stores |

---

## Dummy Variable Approach

### Why Dummy Variables Are Required

The variables `region` and `store_type` are **categorical** — they represent groups, not numbers. Regression requires numerical inputs, so we convert each category into a binary (0 or 1) indicator variable called a **dummy variable**.

### Region Dummy Variables

The `region` variable has four categories: East, North, South, West.

We create **3 dummy variables** (one fewer than the number of categories):

| Dummy Variable | Value = 1 When | Value = 0 When |
|----------------|---------------|---------------|
| region_North | Store is in North region | Store is NOT in North |
| region_South | Store is in South region | Store is NOT in South |
| region_West | Store is in West region | Store is NOT in West |

**Reference Category: East**

The **East** region is omitted — it serves as the baseline. All region coefficients are interpreted *relative to East stores*. For example, `region_South = +25,461` means South stores earn approximately £25,461 more per month than equivalent East stores, holding all other variables constant.

**Why we omit one category (avoid the dummy variable trap):**
If we included dummies for all four regions simultaneously, they would perfectly predict each other (perfect multicollinearity), causing the regression to fail. Dropping one category — the reference — avoids this.

### Store Type Dummy Variables

Although store_type dummy variables were created (Airport, High Street, Mall — with Residential as reference), they were **not included in the final model** to keep the model parsimonious and avoid multicollinearity with region variables. The residual analysis showed store_type effects appear in the residuals and could be incorporated in a future model iteration.

---

## Final Model Selected

**Multiple Regression with footfall, marketing_spend, inventory_availability_pct, customer_rating, and three region dummies.**

**Reason for selection:**
1. Highest R-Squared (0.8137) — explains over 81% of sales variation
2. Six out of seven predictors are statistically significant (p < 0.05)
3. All included variables are **actionable** — leadership can directly influence footfall (location/events), marketing spend, inventory levels, and customer experience
4. The dummy variables appropriately capture regional baseline differences without overfitting
5. The model is interpretable in business language, not just statistics
