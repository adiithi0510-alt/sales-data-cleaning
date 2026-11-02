# Sales Data Cleaning

A Pandas mini project that cleans a messy sales dataset (`Messy_data.csv`) in Google Colab.

## Files
- `Messy_data.csv`: original dataset (185 rows)
- `sales_data_cleaning.ipynb`: cleaning notebook
- `cleaned_sales_dataset.csv`: cleaned output (180 rows, with a new `TotalAmount` column)
- `cleaning_summary.md`: short summary of the cleaning steps
- `problem_statement.md`: project brief

## What was cleaned
- Missing values filled (median, product-wise median price, or "Unknown"); blank dates left as is
- Outliers in age, price and quantity detected and replaced
- Text typed as numbers (`three`, `2 pcs`, `18,500`) converted
- Extra spaces and inconsistent capitalisation fixed
- 5 duplicate rows removed
- Mixed date formats unified; invalid date set to missing
- `TotalAmount = Quantity × UnitPrice` added

## How to run
Open the notebook in Google Colab, upload `Messy_data.csv`, and run all cells. The cleaned file is saved as `cleaned_sales_dataset.csv`.
