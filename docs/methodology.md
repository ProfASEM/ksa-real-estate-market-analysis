# Methodology

This document explains the methodology followed to build the **KSA Real Estate Market Analysis** project, from data preparation to Power BI dashboard development.

---

## 1. Project Objective

The objective of this project is to analyze real estate market activity across selected Saudi cities using sales, rental, population, and macroeconomic indicators.

The analysis aims to provide a structured view of:

- Sales transaction activity
- Market value distribution
- Rental contract activity
- Population-adjusted market intensity
- 2023 year-to-date sales changes
- Price-per-square-meter patterns
- City-level differences across property types

---

## 2. Data Collection

The project uses multiple datasets related to the Saudi real estate market and supporting economic indicators.

The main data categories include:

- Real estate sales transactions
- Rental contract data
- City-level population data
- Average income indicators
- Inflation rate data
- Repo rate data

The datasets were reviewed and prepared before being integrated into the final analytical model.

---

## 3. Data Cleaning

Several cleaning steps were applied before modeling the data.

Main cleaning steps included:

- Standardizing city names across datasets
- Standardizing region names
- Fixing inconsistent Arabic and English naming formats
- Removing duplicate records
- Handling missing values
- Validating date and quarter fields
- Standardizing property type categories
- Checking transaction and rental values for consistency

City and region standardization was especially important because inconsistent naming can lead to incorrect joins and duplicated categories in Power BI.

---


## 4. Time Period Standardization

A quarterly time key was created to support consistent time-based analysis.

The main time field used in the model is:

```text
quarter_key
```

Example format:

```text
2022Q1
2022Q2
2022Q3
2022Q4
```

This allowed sales, rental, and economic datasets to be aligned at a quarterly level.

---

## 5. Data Aggregation

The final fact table was aggregated at the following grain:

```text
city + quarter_key + property_type
```

This means each row represents one city, one quarter, and one property type.

The aggregation process included:

- Summing sales transactions
- Summing market value
- Summing rental contracts
- Calculating weighted average rent
- Calculating weighted average price per square meter where available
- Preserving city and property type structure for Power BI analysis

This grain was chosen to avoid many-to-many issues and to support reliable city-level and time-based reporting.

---

## 6. Data Modeling in Power BI

The Power BI model follows a star-schema structure.

The model includes one main fact table and several dimension tables.

### Fact Table

```text
fact_real_estate_quarterly
```

This table contains the main real estate metrics at city-quarter-property type level.

### Dimension Tables

```text
dim_city
dim_date
dim_property_type
analysis_scope
```

The relationships were designed as one-to-many relationships from dimension tables to the fact table.

This structure improves filtering behavior, reduces ambiguity, and makes DAX measures easier to maintain.

---

## 7. Power BI Relationships

The main relationships used in the model are:

| Dimension Table | Key | Fact Table | Key |
|---|---|---|---|
| `dim_city` | `city` | `fact_real_estate_quarterly` | `city` |
| `dim_date` | `quarter_key` | `fact_real_estate_quarterly` | `quarter_key` |
| `dim_property_type` | `property_type` | `fact_real_estate_quarterly` | `property_type` |

The `analysis_scope` table is used as a documentation/helper table and is not directly related to the fact table.

---

## 8. DAX Measure Development

DAX measures were created to support the dashboard analysis.

The main measure categories include:

- Total sales transactions
- Total market value
- Market value in billions
- Total rental contracts
- Weighted average rent
- Weighted average price per square meter
- Sales per 1,000 population
- Rentals per 1,000 population
- Year-over-year growth
- 2023 YTD comparison
- Price coverage ratio

The measures were designed to support both absolute and population-adjusted analysis.

Detailed DAX documentation is available in:

```text
dax/measures.md
```

---

## 9. Dashboard Design

The final Power BI dashboard includes six main desktop pages:

1. Market Overview
2. Sales Market — 2019–2022
3. Rental Market — 2019–2024
4. City Comparison — 2019–2022
5. 2023 YTD Sales Update
6. Price & Growth Analysis — 2019–2022

Each page was designed with a specific analytical purpose.

The report uses consistent formatting for:

- Page titles
- KPI cards
- Color usage
- Chart titles
- Data labels
- Units
- Notes and caveats

---

## 10. Mobile Layout

A mobile-optimized layout was also created inside the Power BI report.

The mobile layout focuses on simplified views with fewer visuals per page.

The mobile design prioritizes:

- Clear KPI cards
- Short titles
- Dropdown slicers
- Horizontal bar charts
- Reduced visual clutter
- Easy scrolling on smartphones

Not all desktop visuals were transferred to the mobile layout. Only the most important indicators were selected.

---

## 11. Analysis Period Logic

Different analysis periods were used depending on data availability.

| Dashboard Area | Period |
|---|---|
| Market Overview | Available data |
| Sales Market | 2019–2022 |
| Rental Market | 2019–2024 |
| City Comparison | 2019–2022 |
| 2023 YTD Update | 2023 Q1–Q3 vs 2022 Q1–Q3 |
| Price & Growth Analysis | 2019–2022 |

The dashboard avoids comparing incomplete 2023 sales data with full-year 2022 data.

Instead, the 2023 page compares Q1–Q3 of 2023 with Q1–Q3 of 2022.

---

## 12. Validation and Quality Checks

Several validation checks were performed during the project.

These included:

- Checking duplicate records at the final grain
- Confirming city counts after standardization
- Validating relationship behavior in Power BI
- Comparing sales and rental totals before and after aggregation
- Reviewing missing values in price-per-square-meter fields
- Checking whether YTD calculations used comparable periods
- Reviewing charts for misleading period comparisons
- Ensuring population-adjusted metrics used city-level population data

These checks helped reduce the risk of inflated totals, incorrect joins, or misleading visuals.

---

## 13. Design Considerations

The dashboard design uses a clean analytical layout with a light background.

The main design decisions include:

- Blue for sales-related visuals
- Gold for rental-related visuals
- Green for positive changes
- Red for negative changes
- White cards and chart containers
- Light background with subtle decorative elements
- Consistent units such as SAR bn, SAR M, Price/m², and per 1,000 population

The design was kept intentionally simple to support readability and business interpretation.

---

## 14. Final Output

The final project includes:

- Cleaned and processed datasets
- Power BI data model
- DAX measures
- Desktop dashboard
- Mobile layout
- GitHub documentation
- Dashboard screenshots
- Methodology and limitation notes

The result is a portfolio-ready real estate analytics project that demonstrates data cleaning, modeling, DAX, dashboard design, and analytical storytelling.
