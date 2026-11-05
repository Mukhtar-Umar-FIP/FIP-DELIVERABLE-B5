# Sales Data Cleaning (FIP Deliverable B5)

A Jupyter notebook that cleans a messy shop sales dataset and turns it into a reliable file that's ready for analysis.
The original raw data is never changed, and every cleaning decision is written down.

## The dataset

120 sales records from a small shop (January to June 2024): order ID, date, customer, city, product, quantity, price and payment method.

The raw file has the usual real-world problems:
- duplicate orders
- missing values (names, cities, prices, payment methods)
- dates in 3 different formats, plus one date that doesn't exist (`2024-02-30`)
- the same city or product spelt many ways (`lagos`, `LAGOS`, `Abj`, `Veg Oil 5L`, ...)
- prices stored as text (`₦12,000`, `N9800`)
- negative quantities and the word `two` in a number column

> The data is a made-up sample for practice. It isn't real customer data.

## Result

| | Before | After |
|---|---|---|
| Rows | 120 | 104 |
| Missing cells | 29 | 0 |
| Duplicate rows | 6 exact (8 once spacing and case were fixed) | 0 |
| Spellings of city | 18 | 6 |
| Spellings of product | 19 | 6 |
| Date formats | 3 | 1 |

## What's in the repo

```
FIP-DELIVERABLE-B5/
├── data/
│   ├── raw/sales_raw.csv            original data, never edited
│   └── cleaned/sales_cleaned.csv    clean data made by the notebook
├── notebook/
│   └── data_cleaning.ipynb          all the cleaning steps
├── docs/
│   ├── data_dictionary.md           what each column means
│   ├── data_profile.md              before vs after profile (made by the notebook)
│   ├── decision_log.md              every change and why
│   └── reproducibility_checklist.md
├── requirements.txt
└── README.md
```

## Setup

You need **Python 3.10 or newer**.

```bash
# 1. clone the repo
git clone https://github.com/Mukhtar-Umar-FIP/FIP-DELIVERABLE-B5.git
cd FIP-DELIVERABLE-B5

# 2. (optional) create a virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # Mac / Linux

# 3. install the packages
pip install -r requirements.txt
```

## How to run

**Option 1: Jupyter**
```bash
jupyter notebook notebook/data_cleaning.ipynb
```
Then click **Kernel → Restart & Run All**.

**Option 2: VS Code**
Open `notebook/data_cleaning.ipynb`, pick your Python as the kernel, and click **Run All**.

**Option 3: command line (no browser)**
```bash
jupyter nbconvert --to notebook --execute --inplace notebook/data_cleaning.ipynb
```

Running the notebook will:
1. read `data/raw/sales_raw.csv` without changing it
2. clean the data step by step
3. save `data/cleaned/sales_cleaned.csv`
4. check the cleaned file (no missing values, no duplicates, valid numbers)
5. write the before/after report to `docs/data_profile.md`
6. confirm the raw file is unchanged by comparing its hash before and after

## Main cleaning decisions

| Problem | What I did |
|---|---|
| Duplicate orders | Removed, after fixing spaces and case so hidden copies are caught too |
| Missing name, city or payment | Filled with `Unknown` and kept the row, because the sale is still real |
| Missing price | Filled with that product's price, because each product only has one price |
| Mixed date formats | Read each known format. `05/03/2024` = 5 March (day first) |
| Bad date or bad quantity | Removed, because I couldn't know the right value and didn't want to guess |

The full list, with row counts, is in [docs/decision_log.md](docs/decision_log.md).

## Author

Mukhtar Umar. FIP Deliverable B5
