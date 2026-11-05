# Transformation and Decision Log

Every change made to the data, in the order it happens in the notebook.
Row counts come from the notebook run (section 8 of `notebook/data_cleaning.ipynb`).

**Start:** 120 rows, 8 columns. **End:** 104 rows, 9 columns.

| # | Step | What I did | Why | Rows affected | Other option I didn't pick |
|---|---|---|---|---|---|
| 1 | Column names | Removed spaces, made lowercase, used `_`, renamed `qty` → `quantity` | Names like `" Order Date"` and `"Product "` are easy to get wrong in code | 8 columns (no data changed) | – |
| 2 | Extra spaces | Trimmed start/end spaces and doubled spaces in every text cell. Empty cells set as missing | `" Lagos "` and `"Lagos"` would count as two different cities | 28 | – |
| 3 | Customer name case | Changed to Title Case | `"musa balogun"` and `"MUSA BALOGUN"` are the same person | 38 | – |
| 4 | Missing customer name | Filled with `Unknown` | The sale still happened. Deleting the row would lose real revenue | 5 | Delete the rows |
| 5 | City spelling | Title Case, then `Abj` → `Abuja`, `PH` / `P/H` → `Port Harcourt` | Same city was written up to 5 different ways | 57 | – |
| 6 | Missing city | Filled with `Unknown` | No safe way to guess a customer's city | 9 | Guess from the customer's other orders. Not reliable because names repeat |
| 7 | Product spelling | Mapped every spelling to one official name (e.g. `Veg Oil 5L` → `Vegetable Oil 5L`, `Gari` → `Garri`) | 19 spellings for 6 products | 79 | – |
| 8 | Payment method | Grouped into `Cash`, `POS`, `Bank Transfer` (`trf` and `transfer` mean bank transfer) | 10 spellings for 3 methods | 82 | – |
| 9 | Missing payment method | Filled with `Unknown` | Not recorded, can't be guessed | 4 | Fill with most common (Bank Transfer). That would be made-up data |
| 10 | Order date | Read 3 formats: `YYYY-MM-DD`, `DD/MM/YYYY`, `Month D YYYY`. `05/03/2024` is read as 5 March (day first, Nigerian format) | Mixed formats can't be sorted or grouped by month | 117 converted, 3 couldn't be read | Let pandas guess. It could read `05/03` as May 3 |
| 11 | Unit price to number | Removed `₦`, `N` and commas, then converted to a number | Can't do maths on `"₦2,500"` | 120 | – |
| 12 | Missing unit price | Filled with the product's median price | Every product has exactly one price in the data (checked in the notebook), so the right value is known | 8 | Delete the rows |
| 13 | Quantity to number | Converted to a number. `two` became missing | Quantity was stored as text | 120 | Change `two` to `2`. It's only one row, so I flagged it instead of hand-editing |
| 14 | Exact duplicates | Removed rows that were exact copies (after steps 2–3, so copies with different spacing or case are caught) | Duplicates double-count sales | 8 removed | Remove duplicates first. That would miss 2 of them |
| 15 | Repeated order IDs | Kept the first row for any order ID still repeated | Order ID must be unique | 0 (all were caught in step 14) | – |
| 16 | Invalid dates | Removed rows with a blank date or a date that doesn't exist (`2024-02-30`) | Can't be used for analysis over time, and the real date is unknown | 3 removed | Keep with a blank date. Would break monthly totals |
| 17 | Invalid quantity | Removed rows where quantity was blank, `two`, or negative (`-3`, `-7`, `-8`) | A negative could be a refund, a typo or something else. I didn't want to guess | 5 removed | Use the positive number (`-3` → `3`). Risky if they were refunds |
| 18 | Total amount | Added `total_amount = quantity × unit_price` | Needed for revenue analysis | 104 | – |
| 19 | Order and sort | Put columns in a logical order and sorted by date then order ID | Easier to read and the same order every run | 104 | – |

## Rows removed (16 in total)

| Reason | Count |
|---|---|
| Exact duplicates | 8 |
| Missing or impossible date | 3 |
| Missing, non-number or negative quantity | 5 |
| **Total** | **16** |

The removed rows are printed in the notebook (steps 10 and 11), so they can be checked with the shop owner.
In a real job I would ask the owner about the negative quantities before removing them.

## General rules I followed

1. **Never edit the raw file.** It's only read. A hash check at the end of the notebook proves it wasn't changed.
2. **Don't make up data.** Fill a gap only when the correct value is known for sure (product price). Otherwise use `Unknown` or remove the row.
3. **Keep rows where possible.** A missing name or city doesn't make the sale wrong, so those rows stay.
4. **Show what was removed.** Nothing is dropped without being printed first.
