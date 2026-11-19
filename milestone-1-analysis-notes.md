# Milestone 1 — Analysis Notes

## 1. Dataset overview

The sales dataset contains 100 rows and 11 columns. The initial AI-assisted profile reported no missing values and identified `Order_Date` as the date column, parsed in ISO format (`YYYY-MM-DD`). The reported date range is 2025-01-02 to 2025-12-27.

The initial checks also reported no duplicate `Order_ID` values and no fully duplicated rows. These are recorded as outputs from the profiling exercise and should be reproduced independently in the project code before being treated as final validation.

## 2. Descriptive statistics

Reported numeric summaries:

| Column | Mean | Median |
|---|---:|---:|
| Quantity | 131.18 | 128 |
| Unit_Price_DKK | 6.3264 | 6.27 |
| Discount_Pct | 0.065 | 0.05 |
| Revenue_DKK | 804.723 | 680.335 |

No numeric column was flagged by the initial `mean > 3 × median` screening rule. The most frequent reported categories were Esbjerg (27% of rows), Online (28%), and Diabetes Care (17%).

## 3. Date checks

The date-validation exercise reported:
- 100 of 100 dates parsed successfully
- no missing or invalid dates
- all dates fell in 2025
- earliest date: 2025-01-02
- latest date: 2025-12-27
- 88 distinct calendar dates
- 12 dates occurred twice

Repeated calendar dates are not necessarily duplicate transactions. Distinct order identifiers should be considered when assessing transaction duplication.

## 4. Revenue business-rule issue — open

The proposed calculation used during validation was:

`Revenue_DKK = Quantity × Unit_Price_DKK × (1 − Discount_Pct)`

The validation exercise reported one apparent mismatch and multiple small rounding differences. The example discussed was Order_ID `PH-0095`:
- Quantity: 65
- Unit_Price_DKK: 5.03
- Discount_Pct: 0.10
- Calculated amount before rounding: 294.255
- Standard rounding to two decimal places: 294.26
- Recorded Revenue_DKK: 294.25

This may reflect truncation or a different business rule, but the cause has not been confirmed. Do not silently alter the source data. Confirm the intended revenue formula and rounding policy, then document the decision.

## 5. TREND findings — preliminary

The AI-assisted trend output reported:
- Total recorded revenue: DKK 80,472.30 across 100 transactions
- Highest monthly revenue: May, DKK 14,572.39 across 14 transactions
- Lowest monthly revenue: February, DKK 4,144.49 across 7 transactions
- Revenue rose from March through May, then fell sharply from May to June (reported change: -67.9%)
- Revenue increased from November to December (reported change: +33.5%)

These are descriptive observations, not causal explanations. May also had the highest transaction count in the monthly summary, so transaction volume may contribute to the monthly total.

The output identified a possible weekday pattern, with Tuesday having the most orders (21). Monthly seasonality was marked as insufficient evidence because only one year is available. Festival/holiday effects could not be established because the dataset contains no holiday, promotion, or external-event indicators.

The report also noted 272 dates without recorded orders and correctly raised a coverage question: does the file contain every transaction for 2025, or only selected transactions? Until coverage is defined, dates without rows must not automatically be interpreted as zero-sales days.

## 6. JOIN findings — preliminary

The JOIN exercise used `Customer_ID` to compare sales transactions with the customer master file. The reported results were:
- 20 distinct customer IDs in each file
- 18 distinct IDs shared by both files (81.82% overlap, calculated against the 22-ID union)
- 91 sales transactions matched a customer master record
- 9 sales transactions had no matching customer master record
- 2 customer master records had no matching sales transaction

The nine unmatched sales transactions were associated with two IDs:
- `CUST-004`: 6 transactions
- `CUST-017`: 3 transactions

The two right-only customer master records were `CUST-021` and `CUST-022`.

The AI-assisted checks reported no obvious case, whitespace, encoding, or ID-format differences. These findings suggest a referential-integrity issue to investigate, but do not prove either source file is incorrect.

**Do not delete unmatched sales transactions automatically.** They contain transaction and revenue information.

## 7. Open questions for the next milestone

1. Confirm the revenue formula and rounding convention.
2. Reproduce the profiling and JOIN results with Python code.
3. Confirm whether the sales extract is complete for the reporting period.
4. Clarify why `CUST-004` and `CUST-017` are absent from the customer master.
5. Clarify why `CUST-021` and `CUST-022` have no transactions in the sales file.

## 8. Scope and limitations

This is an interim learning milestone based on synthetic data and AI-assisted exploration. Figures and findings in this note reflect the outputs reviewed during the exercise; they should be independently reproduced in code before being presented as fully validated analytical results.
