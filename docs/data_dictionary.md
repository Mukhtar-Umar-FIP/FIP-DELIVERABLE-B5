# Data Dictionary

**File:** `data/cleaned/sales_cleaned.csv`
**Rows:** 104 (one row = one order)
**Period:** January to June 2024

The raw file (`data/raw/sales_raw.csv`) has the same information, but with messy column names and values.
The "Raw column" column shows where each field came from.

| Column | Raw column | Type | Description | Allowed values / format | Example |
|---|---|---|---|---|---|
| `order_id` | `Order ID` | text | Unique ID for each order | `ORD` + 4 digits, no repeats | `ORD1045` |
| `order_date` | ` Order Date` | date | Day the order was made | `YYYY-MM-DD` | `2024-01-02` |
| `customer_name` | `customer name` | text | Customer's full name in Title Case | Any name, or `Unknown` if not recorded | `Ibrahim Adeyemi` |
| `city` | `City` | text | City where the customer is | `Abuja`, `Ibadan`, `Kano`, `Lagos`, `Port Harcourt`, `Unknown` | `Lagos` |
| `product` | `Product ` | text | Product bought | `Beans 5kg`, `Garri 10kg`, `Indomie Carton`, `Rice 50kg`, `Sugar 1kg`, `Vegetable Oil 5L` | `Rice 50kg` |
| `quantity` | `Qty` | whole number | Number of items bought | 1 or more | `4` |
| `unit_price` | `Unit Price` | number (₦) | Price of one item in Naira | More than 0 | `78000.0` |
| `total_amount` | *(new)* | number (₦) | `quantity × unit_price` | More than 0 | `312000.0` |
| `payment_method` | `Payment Method` | text | How the customer paid | `Cash`, `POS`, `Bank Transfer`, `Unknown` | `POS` |

## Product prices

Each product has one fixed price in the data. This is why missing prices could be filled safely.

| Product | Unit price (₦) |
|---|---|
| Sugar 1kg | 1,800 |
| Indomie Carton | 9,800 |
| Beans 5kg | 11,500 |
| Garri 10kg | 12,000 |
| Vegetable Oil 5L | 14,500 |
| Rice 50kg | 78,000 |

## Notes

- `Unknown` means the value was blank in the raw file. Those rows were kept because the sale itself is still valid.
- All money values are in Nigerian Naira (₦).
- The dataset is a made-up sample created for this practice exercise. It is not real customer data.
