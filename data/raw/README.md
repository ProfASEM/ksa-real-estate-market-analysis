# Raw Data

This folder is reserved for raw source data used in the **KSA Real Estate Market Analysis** project.

Due to file size, source structure, and reproducibility considerations, the raw data files may not all be included directly in this repository.

---

## Source Data Categories

The project was prepared using raw data related to:

- Real estate sales transactions
- Rental contract records
- City-level population data
- Average income indicators
- Inflation rate data
- Repo rate data

---

## Processing Notes

The raw datasets were cleaned, standardized, and transformed before being used in Power BI.

Main preparation steps included:

- Standardizing city names
- Standardizing region names
- Creating quarterly time keys
- Aggregating data at city-quarter-property type level
- Handling duplicate records
- Reviewing missing values
- Preparing fact and dimension tables for Power BI

---

## Processed Data

The cleaned datasets used in the final Power BI model are available in:

```text
data/powerbi_data/
fact_real_estate_quarterly.csv
dim_city.csv
dim_date.csv
dim_property_type.csv
analysis_scope.csv
```


## Reproducibility Note

The final dashboard is based on the processed datasets included in this repository.

If raw source files are added in the future, this folder can be updated with:

- Original data files
- Source links
- Download dates
- Source-specific documentation
