# Summary of Cleaning Steps – Sales Dataset Mini Project

**Approach:** load everything as text so bad values stay visible, inspect, clean column by column, then convert types and export.

| # | Issue | How it was handled |
|---|-------|--------------------|
| 1 | Extra spaces | Stripped leading/trailing spaces and collapsed repeated inner spaces in name, city, product and status |
| 2 | Inconsistent text | Converted to Title Case so `delhi`, `DELHI`, `Delhi` became `Delhi`; same for order status |
| 3 | Data-type errors | Number words → digits (`three` → 3, `forty` → 40); removed commas/units (`18,500` → 18500, `2 pcs` → 2); non-numeric text (`unknown`) → missing |
| 4 | Date inconsistencies | Parsed all formats (ISO, dd/mm/yyyy, "Mon dd, yyyy", etc.) into one datetime type, assuming day-first for slash dates; impossible dates (e.g. 30 Feb) → missing |
| 5 | Duplicates | Removed exact duplicate rows *after* standardising text and dates, so hidden duplicates were caught too |
| 6 | Outliers | Age outside 18–100 → flagged. Unit price beyond 3×IQR **within its product** (or ≤ 0) → flagged. Quantity beyond 3×IQR (or ≤ 0) → flagged. Flagged values were set to missing and handled with the other gaps, so the rest of each order was kept |
| 7 | Missing values | Name, city → `"Unknown"`; quantity and age → median; unit price → median of the same product; order date → left blank (not invented) |
| 8 | Data types | `OrderID`, `Quantity`, `CustomerAge` → integer; `UnitPrice`, `TotalAmount` → float; `OrderDate` → datetime; text columns → string/category |
| 9 | New column | `TotalAmount = Quantity × UnitPrice` |
| 10 | Export | Saved as `cleaned_sales_dataset.csv` |

## Why these choices

- **Median, not mean,** for quantity and age: it isn't pulled around by extreme values.
- **Price outliers checked per product,** because a laptop is naturally far more expensive than a mouse.
- **Outliers set to missing instead of dropping rows,** so no other valid information in those orders is lost.
- **Missing dates not filled:** any date would be a guess; leaving them blank keeps the data honest and the rows can be reviewed.
