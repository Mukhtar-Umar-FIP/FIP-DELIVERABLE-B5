# Data Profile: Before and After Cleaning

This file is created automatically by `notebook/data_cleaning.ipynb` (section 9). Don't edit it by hand.

## Summary

| measure | before | after | change |
|---|---|---|---|
| rows | 120 | 104 | -16 |
| columns | 8 | 9 | 1 |
| missing cells | 29 | 0 | -29 |
| exact duplicate rows | 6 | 0 | -6 |
| duplicate order IDs | 8 | 0 | -8 |

## Raw data (before)

File: `data/raw/sales_raw.csv`

| column | type | missing | missing_% | unique_values |
|---|---|---|---|---|
| Order ID | str | 0 | 0.0 | 112 |
|  Order Date | str | 2 | 1.7 | 102 |
| customer name | str | 5 | 4.2 | 100 |
| City | str | 9 | 7.5 | 18 |
| Product  | str | 0 | 0.0 | 19 |
| Qty | str | 1 | 0.8 | 14 |
| Unit Price | str | 8 | 6.7 | 23 |
| Payment Method | str | 4 | 3.3 | 10 |

## Cleaned data (after)

File: `data/cleaned/sales_cleaned.csv`

| column | type | missing | missing_% | unique_values |
|---|---|---|---|---|
| order_id | str | 0 | 0.0 | 104 |
| order_date | datetime64[us] | 0 | 0.0 | 78 |
| customer_name | str | 0 | 0.0 | 79 |
| city | str | 0 | 0.0 | 6 |
| product | str | 0 | 0.0 | 6 |
| quantity | int64 | 0 | 0.0 | 10 |
| unit_price | float64 | 0 | 0.0 | 6 |
| total_amount | float64 | 0 | 0.0 | 52 |
| payment_method | str | 0 | 0.0 | 4 |

## Text values after cleaning

- **city**: Abuja, Ibadan, Kano, Lagos, Port Harcourt, Unknown
- **product**: Beans 5kg, Garri 10kg, Indomie Carton, Rice 50kg, Sugar 1kg, Vegetable Oil 5L
- **payment_method**: Bank Transfer, Cash, POS, Unknown

## Number columns after cleaning

| stat | quantity | unit_price | total_amount |
|---|---|---|---|
| count | 104.0 | 104.0 | 104.0 |
| mean | 5.53 | 22468.27 | 119615.38 |
| std | 2.87 | 26630.97 | 165897.11 |
| min | 1.0 | 1800.0 | 1800.0 |
| 25% | 3.0 | 9800.0 | 24000.0 |
| 50% | 6.0 | 11500.0 | 69000.0 |
| 75% | 8.0 | 14500.0 | 104625.0 |
| max | 10.0 | 78000.0 | 780000.0 |

## What changed (cleaning log)

| # | step | rows_affected | reason |
|---|---|---|---|
| 0 | Rename columns | 0 | Only column names changed, no data. Names had extra spaces and mixed case |
| 1 | Trim spaces | 28 | Extra spaces made the same value look different |
| 2 | Customer name to Title Case | 38 | Same person was written in different cases |
| 3 | Fill missing customer name | 5 | Sale is still valid without a name, so keep the row |
| 4 | Standardise city names | 57 | Same city spelt in different ways |
| 5 | Fill missing city | 9 | Can't guess the city, so mark it Unknown |
| 6 | Standardise product names | 79 | Same product spelt in different ways |
| 7 | Standardise payment method | 82 | Same payment type written in different ways |
| 8 | Fill missing payment method | 4 | Payment type not recorded |
| 9 | Convert order_date to a date | 117 | Three different date formats in one column |
| 10 | Convert unit_price to a number | 120 | Prices were text with symbols and commas |
| 11 | Fill missing unit_price | 8 | Each product has one fixed price, so use it |
| 12 | Convert quantity to a number | 120 | Quantity was stored as text |
| 13 | Remove exact duplicate rows | 8 | Same order entered more than once would double count sales |
| 14 | Remove repeated order IDs | 0 | Order ID must be unique |
| 15 | Remove rows with no valid date | 3 | Date missing or impossible |
| 16 | Remove rows with invalid quantity | 5 | Quantity missing, not a number or not above 0 |
| 17 | Add total_amount column | 104 | Needed for revenue analysis |
