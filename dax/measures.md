# DAX Measures Documentation

This document contains the main DAX measures used in the **KSA Real Estate Market Analysis** Power BI dashboard.

The measures are organized by analytical purpose to make the report logic easier to understand, review, and maintain.

---

## Measure Categories

The dashboard uses the following measure groups:

1. Core aggregation measures
2. Sales market measures
3. Rental market measures
4. Population-adjusted measures
5. Weighted average measures
6. Price coverage measures
7. Year-over-year growth measures
8. 2023 year-to-date comparison measures

---

## 1. Core Aggregation Measures

These measures calculate the main totals used across the dashboard.

### Total Sales Transactions

Calculates the total number of real estate sales transactions.

```DAX
Total Sales Transactions =
SUM ( fact_real_estate_quarterly[sales_transactions] )
```

Used in:

- Market Overview
- Sales Market
- City Comparison
- 2023 YTD Sales Update
- Price & Growth Analysis

---

### Total Market Value

Calculates the total value of real estate sales transactions.

```DAX
Total Market Value =
SUM ( fact_real_estate_quarterly[market_value] )
```

Used in:

- Market Overview
- Sales Market
- City Comparison
- 2023 YTD Sales Update

---

### Market Value Billion

Converts total market value into billions of Saudi Riyals for easier reporting.

```DAX
Market Value Billion =
DIVIDE ( [Total Market Value], 1000000000 )
```

Used in:

- Market Overview
- Sales Market
- 2023 YTD Sales Update

---

### Total Rental Contracts

Calculates the total number of rental contracts.

```DAX
Total Rental Contracts =
SUM ( fact_real_estate_quarterly[rental_contracts] )
```

Used in:

- Market Overview
- Rental Market
- City Comparison

---

### Population

Calculates total population from the city dimension table.

```DAX
Population =
SUM ( dim_city[population] )
```

Used in:

- Market Overview
- Population-adjusted indicators
- City Comparison
