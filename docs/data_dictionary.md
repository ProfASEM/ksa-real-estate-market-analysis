# Data Dictionary

This document describes the main tables and fields used in the **KSA Real Estate Market Analysis** project.

The Power BI model is built around a quarterly city-level real estate fact table connected to supporting dimension tables.

---

## 1. Overview

The model uses a star-schema structure with one main fact table and several dimension tables.

| Table | Type | Description |
|---|---|---|
| `fact_real_estate_quarterly` | Fact table | Main quarterly real estate metrics by city and property type |
| `dim_city` | Dimension table | City, region, and population attributes |
| `dim_date` | Dimension table | Quarter and year structure |
| `dim_property_type` | Dimension table | Property type categories |
| `analysis_scope` | Helper table | Documents analysis periods and reporting scope |

---

## 2. Model Grain

The main fact table is aggregated at the following grain:

```text
city + quarter_key + property_type
```

This means each row represents one city, one quarter, and one property type.

Example:

```text
Riyadh + 2022Q1 + Residential

---

## 3. fact_real_estate_quarterly

The `fact_real_estate_quarterly` table is the main analytical table used in the dashboard.

It contains real estate sales and rental indicators aggregated by city, quarter, and property type.

### Table Grain

```text
city + quarter_key + property_type
```

### Columns

| Column | Type | Description |
|---|---|---|
| `city` | Text | City name used as the city-level join key |
| `quarter_key` | Text | Quarterly time key used to join with `dim_date` |
| `property_type` | Text | Property type category, such as residential or commercial |
| `sales_transactions` | Numeric | Number of real estate sales transactions |
| `market_value` | Numeric | Total market value of sales transactions in SAR |
| `avg_price_m2` | Numeric | Average price per square meter in SAR, where available |
| `rental_contracts` | Numeric | Number of rental contracts |
| `avg_rent` | Numeric | Average rent in SAR |
| `Average_Income` | Numeric | Average income indicator, where available |
| `inflation_rate` | Numeric | Inflation rate indicator |
| `repo_rate` | Numeric | Repo rate indicator |

### Notes

- `sales_transactions` and `market_value` are used for sales market analysis.
- `rental_contracts` and `avg_rent` are used for rental market analysis.
- `avg_price_m2` requires careful interpretation because price coverage may vary by city, period, or property type.
- `market_value` is stored in SAR, but many dashboard visuals display it in billions using DAX measures.

---

## 3. fact_real_estate_quarterly

The `fact_real_estate_quarterly` table is the main analytical table used in the dashboard.

It contains real estate sales and rental indicators aggregated by city, quarter, and property type.

### Table Grain

```text
city + quarter_key + property_type
```

### Columns

| Column | Type | Description |
|---|---|---|
| `city` | Text | City name used as the city-level join key |
| `quarter_key` | Text | Quarterly time key used to join with `dim_date` |
| `property_type` | Text | Property type category, such as residential or commercial |
| `sales_transactions` | Numeric | Number of real estate sales transactions |
| `market_value` | Numeric | Total market value of sales transactions in SAR |
| `avg_price_m2` | Numeric | Average price per square meter in SAR, where available |
| `rental_contracts` | Numeric | Number of rental contracts |
| `avg_rent` | Numeric | Average rent in SAR |
| `Average_Income` | Numeric | Average income indicator, where available |
| `inflation_rate` | Numeric | Inflation rate indicator |
| `repo_rate` | Numeric | Repo rate indicator |

### Notes

- `sales_transactions` and `market_value` are used for sales market analysis.
- `rental_contracts` and `avg_rent` are used for rental market analysis.
- `avg_price_m2` requires careful interpretation because price coverage may vary by city, period, or property type.
- `market_value` is stored in SAR, but many dashboard visuals display it in billions using DAX measures.

---

## 5. dim_date

The `dim_date` table provides the time structure used in the Power BI model.

The dashboard uses quarterly analysis rather than daily or monthly analysis.

### Columns

| Column | Type | Description |
|---|---|---|
| `quarter_key` | Text | Unique quarter key used to join with the fact table |
| `year` | Numeric | Calendar year |
| `quarter` | Numeric | Quarter number from 1 to 4 |

### Example Values

| quarter_key | year | quarter |
|---|---:|---:|
| `2019Q1` | 2019 | 1 |
| `2019Q2` | 2019 | 2 |
| `2019Q3` | 2019 | 3 |
| `2019Q4` | 2019 | 4 |

### Notes

- `quarter_key` connects `dim_date` to `fact_real_estate_quarterly`.
- Year and quarter fields are used in:
  - Year-over-year analysis
  - 2023 YTD comparison
  - Trend charts
  - Period filtering
 
  ---

## 6. dim_property_type

The `dim_property_type` table contains the property type categories used in the dashboard.

### Columns

| Column | Type | Description |
|---|---|---|
| `property_type` | Text | Property type category used as the relationship key |

### Example Values

| property_type |
|---|
| Residential |
| Commercial |

### Notes

- The `property_type` column connects this dimension table to the fact table.
- Property type slicers allow users to filter the dashboard by residential or commercial real estate.
- Property type standardization was applied during data preparation to avoid duplicated categories.

  ---

## 7. analysis_scope

The `analysis_scope` table is a helper table used to document the reporting scope and analysis periods.

It is not necessarily connected directly to the fact table.

### Suggested Columns

| Column | Type | Description |
|---|---|---|
| `analysis_area` | Text | Dashboard section or analysis area |
| `period_used` | Text | Time period used for the analysis |
| `notes` | Text | Explanation of why the period was used |

### Example Values

| analysis_area | period_used | notes |
|---|---|---|
| Market Overview | Available data | Broad overview based on available sales and rental periods |
| Sales Market | 2019–2022 | Main complete sales comparison period |
| Rental Market | 2019–2024 | Rental data available for a longer period |
| City Comparison | 2019–2022 | Common comparison period for sales and rental activity |
| 2023 YTD Update | 2023 Q1–Q3 vs 2022 Q1–Q3 | Like-for-like partial-year comparison |
| Price & Growth Analysis | 2019–2022 | Used for price-per-square-meter and YoY growth analysis |

### Notes

- This table helps document why different dashboard pages use different periods.
- It supports transparency and reduces the risk of misleading period comparisons.

---

## 8. Units and Formatting

The dashboard uses consistent reporting units to improve readability.

| Metric | Stored Unit | Dashboard Display |
|---|---|---|
| `sales_transactions` | Count | Whole number / K |
| `market_value` | SAR | SAR bn |
| `avg_price_m2` | SAR per m² | SAR |
| `rental_contracts` | Count | Whole number / K / M |
| `avg_rent` | SAR | SAR / K |
| `population` | People | Whole number / M |
| `Average_Income` | SAR | SAR |
| `inflation_rate` | Percentage / rate | % |
| `repo_rate` | Percentage / rate | % |

### Notes

- Financial values are often converted using DAX measures for clearer reporting.
- Market value is commonly displayed in billions of SAR.
- Average transaction value may be displayed in SAR or SAR M depending on the visual.
- Growth and change metrics are displayed as percentages.

---

## 9. Key Analytical Measures

The dashboard uses DAX measures to calculate business indicators from the data model.

Main analytical measures include:

| Measure | Description |
|---|---|
| `Total Sales Transactions` | Total number of sales transactions |
| `Total Market Value` | Total sales market value in SAR |
| `Market Value Billion` | Market value converted to billions of SAR |
| `Total Rental Contracts` | Total number of rental contracts |
| `Weighted Average Rent` | Weighted rent based on rental contracts |
| `Weighted Avg Price per m2` | Weighted price per square meter |
| `Sales per 1,000 Population` | Sales intensity adjusted by population |
| `Rentals per 1,000 Population` | Rental intensity adjusted by population |
| `Sales YoY %` | Year-over-year sales transaction growth |
| `Market Value YoY %` | Year-over-year market value growth |
| `Sales YTD Change %` | 2023 Q1–Q3 sales change vs 2022 Q1–Q3 |
| `Price Coverage Ratio` | Share of sales covered by price-per-square-meter data |

Detailed DAX logic is documented in:

```text
dax/measures.md
```

---

## 10. Data Quality Notes

Several data quality considerations were handled during the project.

### City and Region Standardization

City and region names were standardized to avoid duplicated categories and incorrect joins.

Examples of possible standardization issues include:

- Arabic vs English city names
- Region names written with or without the word "Region"
- Different spellings of the same city
- Inconsistent naming between sales and rental datasets

### Date Standardization

Quarterly keys were standardized using the `quarter_key` field.

This helped align sales, rental, and macroeconomic indicators at the same time level.

### Missing Values

Some fields may contain missing values depending on data availability.

Fields that require special attention include:

- `avg_price_m2`
- `avg_rent`
- Sales fields in periods where sales data is unavailable
- Rental fields in periods where rental data is unavailable

### Price Coverage

Price-per-square-meter analysis should be interpreted together with the `Price Coverage Ratio`.

If price coverage is low, price indicators may not fully represent the market.

---

## 11. Final Notes

This data dictionary is intended to make the project easier to understand, reproduce, and maintain.

It supports transparency by documenting:

- The model structure
- The meaning of each table
- The meaning of each key field
- The analytical grain
- The main reporting units
- Important data quality considerations

The dictionary should be updated if new data sources, columns, or dashboard pages are added in the future.


```

The grain was selected to support consistent sales, rental, city-level, and time-based reporting in Power BI.
