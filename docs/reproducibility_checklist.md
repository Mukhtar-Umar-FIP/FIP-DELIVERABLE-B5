# Reproducibility Checklist

Things I did so anyone can run this and get the same cleaned file.

## Data

- [x] The original raw file is saved in the repo (`data/raw/sales_raw.csv`)
- [x] The notebook only **reads** the raw file and never writes to it
- [x] A SHA-256 hash of the raw file is taken at the start and checked at the end of the notebook
- [x] The cleaned output goes to a separate folder (`data/cleaned/`)

## Code

- [x] All cleaning is done in one notebook (`notebook/data_cleaning.ipynb`) with no manual edits in Excel
- [x] The notebook runs top to bottom with no errors (Kernel → Restart & Run All)
- [x] File paths are relative (`../data/...`), so it works on any computer once the repo is cloned
- [x] No random steps, so the output is the same every run
- [x] Mapping tables for city, product and payment are written in the code, so they're easy to check
- [x] The notebook stops with an error if a new, unknown product shows up (`assert`)
- [x] The cleaned file is loaded back and tested with `assert` checks: no missing values, no duplicates, valid numbers

## Environment

- [x] Packages are listed in `requirements.txt`
- [x] Tested with Python 3.13 and pandas 3.1.1

## Documentation

- [x] Every step in the notebook has a note explaining what and why
- [x] `docs/decision_log.md` lists every change, the reason, and the rows affected
- [x] `docs/data_dictionary.md` describes every column in the cleaned file
- [x] `docs/data_profile.md` is created by the notebook, so the before/after numbers always match the latest run
- [x] README explains setup and how to run

## How to check it yourself

1. Clone the repo and install the requirements (see README).
2. Delete `data/cleaned/sales_cleaned.csv`.
3. Run the notebook from top to bottom.
4. The file comes back with **104 rows**, every check in section 6 passes, and section 10 says `Raw file is unchanged.`
