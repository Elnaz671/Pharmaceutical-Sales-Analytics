# Pharmaceutical Sales Analytics Project

## Project status
**Milestone 1 — Initial data profiling and AI-assisted exploratory analysis**

This is a learning portfolio project built with **synthetic practice data**. It does not contain real pharmaceutical company, customer, or patient information. The datasets were created for analytical practice.

## Project objective
Explore a fictional pharmaceutical sales dataset, assess its data quality, identify patterns in revenue over time, and practise joining transaction data to a customer master file.

## Repository structure

```text
pharmaceutical-sales-analytics/
├── data/
│   ├── pharmaceutical_sales_practice.csv
│   └── pharmaceutical_customer_master_practice.csv
├── docs/
│   └── milestone-1-analysis-notes.md
├── README.md
└── .gitignore
```

## Data files

### Sales transactions
`data/pharmaceutical_sales_practice.csv`

100 fictional sales transactions with 11 columns:
- Order_ID
- Order_Date
- Customer_ID
- Product
- Category
- Region
- Sales_Channel
- Quantity
- Unit_Price_DKK
- Discount_Pct
- Revenue_DKK

### Customer master
`data/pharmaceutical_customer_master_practice.csv`

A separate fictional customer reference file used to practise JOIN operations.

## Work completed in Milestone 1
- Dataset shape, column names, inferred data types and missing-value profiling
- Numeric descriptive statistics and categorical value counts
- Initial anomaly and duplicate checks
- Date parsing and date-range validation
- Revenue calculation consistency check (open issue; see analysis notes)
- Monthly revenue trend and moving-average exploration
- Preliminary weekly/monthly seasonality review
- Customer master JOIN with matched, left-only and right-only records

## Important interpretation notes
- The data is synthetic and conclusions are only about this practice dataset.
- One calendar year is not enough to establish recurring annual seasonality.
- A date with no transaction in this file is not automatically proof of a zero-sales day; dataset coverage must be understood.
- Unmatched JOIN records should not be deleted automatically.
- The revenue formula and rounding convention still require confirmation.

## Next steps
Continue the course and extend this project with reproducible Python analysis, documented business rules, and further analytical work. This repository represents an interim milestone, not a completed end-to-end project.
