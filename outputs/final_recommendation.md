# Final Business Recommendation

## Executive Summary

Based on regression analysis of 306 store-month records across a retail chain, our multiple regression model explains **81.4% of the variation in monthly sales** (R² = 0.8137). Six variables emerged as statistically significant predictors. This report translates those findings into clear business actions.

---

## Which Factors Are Most Strongly Associated with Monthly Sales?

| Rank | Factor | Strength of Evidence | Direction |
|------|--------|---------------------|-----------|
| 1 | **Footfall** | Very strong (p < 0.001, simple R² = 0.73) | Positive |
| 2 | **Inventory Availability %** | Strong (p < 0.001) | Positive |
| 3 | **Region (South, West vs East)** | Strong (p < 0.003) | Positive |
| 4 | **Marketing Spend** | Significant (p < 0.001) | Positive |
| 5 | **Customer Rating** | Significant (p = 0.024) | Positive |

---

## Which Variables Should Leadership Focus On?

### 1. Footfall — Top Priority

Footfall is the single most powerful predictor, explaining 73% of monthly sales variation on its own. Every additional customer visit is associated with approximately **£34–36 in additional monthly sales**.

**Recommended actions:**
- Prioritise high-footfall locations when selecting new store sites
- Invest in in-store events, local community programmes, and partnerships to drive foot traffic
- Analyse why certain stores have lower-than-expected footfall relative to their marketing spend

### 2. Inventory Availability

Each 1% improvement in stock availability is associated with approximately **£2,575 more in monthly sales**.

**Recommended actions:**
- Set a minimum inventory availability target of 90%+ for all stores
- Review supply chain and replenishment cycles for stores below this threshold
- Prioritise high-demand products in inventory planning

### 3. Regional Strategy

South and West region stores outperform East stores by **£25,461 and £20,335 per month** respectively, after controlling for other factors.

**Recommended actions:**
- Investigate what structural advantages South and West stores have (demographics, competition, store formats)
- Consider prioritising new store openings in South and West regions
- Share best practices from high-performing South/West stores with East region

### 4. Marketing Spend

Each additional £1 of marketing spend is associated with approximately **£1.21 in monthly sales** (after controlling for footfall). This implies a positive but modest return.

**Recommended actions:**
- Allocate marketing budget with a focus on campaigns that drive footfall (events, local promotions), not just brand awareness
- Run controlled experiments to test whether higher marketing spend increases footfall or primarily reaches existing customers
- Avoid over-investing in marketing at stores with structurally low footfall (address root cause first)

### 5. Customer Rating

Each 1-point improvement in customer rating is associated with approximately **£11,175 more in monthly sales**.

**Recommended actions:**
- Invest in staff training and service quality programmes
- Monitor customer ratings regularly and set minimum targets for store managers
- Share learnings from high-rated stores (e.g. STR-1006 with rating 5.0)

---

## Which Variables Should NOT Be Over-Interpreted?

| Variable | Reason for Caution |
|----------|-------------------|
| **avg_discount_pct** | Not significant in regression; higher discounting is not associated with higher sales. Avoid the assumption that discounting drives growth. |
| **competitor_distance_km** | Not included in final model (missing data); competitive dynamics are complex and not fully captured. |
| **region_North** | Marginally significant (p = 0.088); North vs East difference may exist but evidence is weaker. Do not treat North stores as definitively superior to East. |
| **monthly_profit** | Not used as a predictor (it is an outcome variable like sales); avoid confusing it with a driver. |

---

## Business Actions We Recommend

1. **Footfall-first strategy:** Make increasing customer visits the primary KPI for store managers. Evaluate marketing ROI in terms of footfall generated, not just sales lift.
2. **Inventory improvement programme:** Audit all stores with inventory availability below 85% and set a 90% minimum target.
3. **Regional expansion in South and West:** New store investment and franchise opportunities should prioritise South and West regions.
4. **Customer experience investment:** Tie customer rating targets to store manager incentives. Investigate and replicate practices of top-rated stores.
5. **Residual store reviews:** Conduct targeted reviews of STR-1017, STR-1012, STR-1023, STR-1009, and STR-1077, which significantly underperform model predictions — these may have correctable operational issues.

---

## Risks and Limitations Leadership Should Keep in Mind

| Risk | Explanation |
|------|-------------|
| **Short time window** | Data covers only four months. Seasonal effects or economic cycles are not captured. |
| **Missing variables** | Factors like store size, local demographics, product mix, and competitor presence are not in the model. They may be causing omitted variable bias. |
| **Data quality** | 14 records had missing values (customer_rating, competitor_distance_km) and were excluded. If missing data is systematic, this could affect results. |
| **Outlier influence** | A few extreme records (very high marketing spend, e.g., STR-1007 at £172,415) may distort coefficient estimates. |

---

## Why Regression Shows Association, Not Causation

Our regression model identifies **statistical associations** — patterns in data — but cannot prove that any variable *causes* higher sales. For example:

- **Footfall and sales** are strongly correlated, but high footfall may itself be caused by a store being in a prime location, strong brand presence, or local demographics — factors the model doesn't directly measure. Increasing marketing spend to drive footfall may or may not replicate these natural advantages.
- **Customer rating and sales** are associated, but it is possible that stores with higher sales have *more resources* to invest in customer service, creating reverse causation.
- **Regional effects** may reflect unmeasured structural differences (population density, income levels, competition) rather than anything leadership can directly control.

**To establish causation, the business would need:** controlled experiments (e.g., randomly increasing marketing spend in selected stores and comparing to control stores), or natural experiments (e.g., measuring sales before and after an inventory improvement programme).

Regression is a powerful diagnostic tool, but business decisions should combine these statistical insights with operational knowledge and targeted experimentation.

---

## Final Model Selected

**Multiple Regression (R² = 0.8137)** using footfall, marketing_spend, inventory_availability_pct, customer_rating, and three region dummy variables (reference: East).

This model offers the best balance of explanatory power, statistical rigour, business interpretability, and actionability.
