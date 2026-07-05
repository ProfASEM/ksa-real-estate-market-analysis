# Data Limitations and Assumptions

This document describes the main data limitations, assumptions, and interpretation notes for the **KSA Real Estate Market Analysis** project.

The purpose of this document is to make the analysis more transparent and to reduce the risk of misleading conclusions.

---

## 1. Overview

The dashboard analyzes Saudi real estate sales, rental activity, population indicators, and macroeconomic variables across selected cities.

Although the project provides useful market insights, the results should be interpreted within the context of data availability, reporting periods, aggregation logic, and data coverage.

The main limitation areas are:

- Different coverage periods between sales and rental data
- Incomplete 2023 sales data
- City-level population assumptions
- Price-per-square-meter coverage
- Aggregation effects
- Possible transaction mix differences between cities and years
- Interpretation limits of year-over-year growth

---

## 2. Sales and Rental Period Differences

Sales data and rental data do not cover the exact same time periods.

The dashboard handles this by separating analysis periods depending on the topic.

| Analysis Area | Period Used | Reason |
|---|---|---|
| Sales Market | 2019–2022 | Main complete sales comparison period |
| Rental Market | 2019–2024 | Rental data is available for a longer period |
| City Comparison | 2019–2022 | Common period for sales and rental comparison |
| 2023 YTD Update | 2023 Q1–Q3 vs 2022 Q1–Q3 | Like-for-like partial-year comparison |

Because of this, sales and rental indicators should not always be compared across the full available period.

### Interpretation Note

When comparing sales and rental activity, the dashboard mainly uses the common period **2019–2022** to reduce period mismatch.

---

## 3. Incomplete 2023 Sales Data

The 2023 sales data is available only for Q1–Q3.

For this reason, the dashboard does not compare 2023 Q1–Q3 with full-year 2022.

Instead, the 2023 YTD page compares:

```text
2023 Q1–Q3
```

with:

```text
2022 Q1–Q3
```

This creates a more reliable like-for-like comparison.

### Interpretation Note

Any 2023 sales change shown in the dashboard should be interpreted as a **year-to-date comparison**, not as a full-year market performance conclusion.

---

## 4. 2024 Sales Data Limitation

The main sales analysis does not use 2024 sales data because the available sales coverage was not sufficient for a reliable full-year comparison.

As a result:

- Sales Market analysis focuses on 2019–2022.
- 2023 is treated separately as a Q1–Q3 YTD update.
- 2024 is not used for sales trend conclusions.

### Interpretation Note

The absence of 2024 sales analysis does not imply market inactivity. It reflects data availability and coverage constraints.

---

## 5. Population Assumptions

Population is used as a city-level baseline to calculate population-adjusted indicators.

Examples include:

- Sales per 1,000 population
- Rentals per 1,000 population

The population data is treated as a city-level baseline and does not vary quarterly in the model.

### Limitation

Because population is not updated by quarter, population-adjusted indicators should be interpreted as relative city-level intensity measures, not exact demographic time-series indicators.

### Interpretation Note

Population-adjusted metrics are useful for comparing cities of different sizes, but they should not be interpreted as precise quarterly per-capita rates.

---

## 6. Price per Square Meter Coverage

The `avg_price_m2` field is used to analyze price-per-square-meter patterns.

However, price-per-square-meter analysis depends on data coverage.

To support interpretation, the dashboard includes a price coverage measure:

```text
Price Coverage Ratio
```

This measure estimates the share of sales transactions covered by available price-per-square-meter data.

### Limitation

If price coverage is low for a city, year, or property type, price-per-square-meter results may not fully represent the market.

### Interpretation Note

Unusual price-per-square-meter movements should be reviewed carefully before being interpreted as direct market trends.

---

## 7. Weighted Average Calculations

The dashboard uses weighted averages for rent and price indicators where appropriate.

Examples:

- Weighted average rent
- Weighted average price per square meter

Weighted averages are used to reduce distortion from simple averages.

### Limitation

Weighted averages still depend on the underlying transaction or rental contract mix.

For example, changes in the mix of residential and commercial properties, or changes in the types of properties transacted, may affect average values.

### Interpretation Note

A change in average price or rent does not always mean that all properties became more expensive or cheaper. It may also reflect a change in the composition of transactions.

---

## 8. Aggregation Effects

The final fact table is aggregated at the following grain:

```text
city + quarter_key + property_type
```

This level of aggregation is suitable for dashboard reporting and city-level comparison.

### Limitation

Aggregation may hide more detailed patterns, such as:

- District-level differences
- Property size differences
- Transaction-level variation
- Neighborhood-specific pricing behavior
- Differences between property subtypes

### Interpretation Note

The dashboard is designed for city-level market analysis, not property-level valuation or neighborhood-level appraisal.

---

## 9. City and Region Standardization

City and region names were standardized during data preparation.

This step was necessary because naming differences can cause duplicated categories, incorrect joins, or missing values.

Examples of possible issues include:

- Arabic and English naming differences
- Different spellings of the same city
- Region names written with different formats
- City names not matching between sales and rental datasets

### Limitation

Although city and region standardization was reviewed carefully, minor naming or classification differences may still exist depending on the source data.

### Interpretation Note

Standardization improves model consistency, but source-level naming differences remain an important data quality consideration.

---

## 10. Year-over-Year Growth Interpretation

Year-over-year growth measures compare the selected year with the previous year.

Examples include:

- Sales YoY %
- Market Value YoY %
- Price/m² YoY %

### Limitation

YoY growth can become very large when the previous year has a small base.

For example, if a city had very few transactions in the previous year, a moderate increase in the current year may appear as a very high growth percentage.

### Interpretation Note

High YoY growth percentages should be interpreted together with the underlying transaction volume.

Growth rates based on small previous-year values may be mathematically correct but analytically unstable.

---

## 11. Market Value Interpretation

Market value represents the total value of sales transactions in SAR.

The dashboard often displays market value in billions of SAR for readability.

### Limitation

Market value is influenced by both:

- Number of transactions
- Average transaction value

A city may have high market value because of high transaction volume, high-value transactions, or both.

### Interpretation Note

Market value should be interpreted together with sales transactions and average transaction value to understand whether the market is driven by volume or deal size.

---

## 12. Rental Market Interpretation

Rental analysis is based on rental contract activity and average rent indicators.

### Limitation

Rental contract volume does not necessarily represent the full rental stock of a city.

It reflects recorded rental contract activity during the available period.

Average rent may also be affected by:

- Property type mix
- Contract duration
- City composition
- Residential vs commercial activity
- Changes in recorded rental contracts

### Interpretation Note

Rental metrics should be interpreted as indicators of rental contract activity, not as complete measures of the entire rental housing market.

---

## 13. Macroeconomic Indicators

The dataset includes macroeconomic indicators such as:

- Inflation rate
- Repo rate
- Average income indicators

These fields provide useful context for real estate market analysis.

### Limitation

The dashboard does not claim direct causal relationships between macroeconomic indicators and real estate outcomes.

For example, a change in repo rate may be associated with changes in market behavior, but the dashboard does not prove causality.

### Interpretation Note

Macroeconomic indicators should be interpreted as contextual variables, not as standalone explanations for market movement.

---

## 14. Selected Cities Scope

The analysis focuses on selected Saudi cities included in the prepared dataset.

### Limitation

The dashboard does not necessarily cover every city or locality in Saudi Arabia.

As a result, the findings should be understood as an analysis of the selected cities, not a complete representation of the entire national real estate market.

### Interpretation Note

The selected cities provide a strong view of major real estate activity, but the dashboard should not be treated as a full national census of all real estate transactions.

---

## 15. Final Interpretation Note

This dashboard is designed for analytical exploration, portfolio presentation, and market-level insight generation.

It should not be used as:

- A property valuation tool
- A legal or financial advisory tool
- A replacement for official market reports
- A transaction-level due diligence system

The findings are most useful when interpreted as city-level market indicators supported by transparent data preparation, clear period logic, and documented limitations.

