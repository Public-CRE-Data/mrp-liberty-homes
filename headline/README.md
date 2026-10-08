# Headline numbers: check our work

These files rebuild **`summary_by_state.csv`** (the headline numbers by state and for all homes) from the home-level data, using live Excel formulas.

| File | Paste into sheet | Contents |
|---|---|---|
| [`1_homes.tsv`](1_homes.tsv) | `homes` | One row per property (values from `mrp_liberty_homes.csv`) plus formulas: MRP price vs. last list (%), days listed (deed date − first list date), gross yield (rent × 12 ÷ price) |
| [`2_summary.tsv`](2_summary.tsv) | `summary` | By state and ALL: counts, averages and medians as formulas over `homes`; our results beside them; a check column |

## Check our work in Excel

The files are tab-separated text: columns split automatically when pasted, and every cell starting with `=` becomes a live formula. Nothing needs downloading. Needs Excel 2010 or later (365 recommended). Pasted dates and zip codes may change format; that's fine, because it happens on every sheet.

1. Open a **new, blank Excel workbook** and create 2 sheets named exactly **`homes`**, **`summary`**. The formulas refer to these names.
2. On GitHub open [`1_homes.tsv`](1_homes.tsv), click **Raw**, press **Ctrl+A** then **Ctrl+C**, click cell **A1** on the **`homes`** sheet and press **Ctrl+V**.
3. On GitHub open [`2_summary.tsv`](2_summary.tsv), click **Raw**, press **Ctrl+A** then **Ctrl+C**, click cell **A1** on the **`summary`** sheet and press **Ctrl+V**.
4. Wait a few seconds for Excel to finish calculating.
5. **Check:** every cell in the **check** column should be **0**. A 0 means Excel's formula reproduces our number exactly.

## How each number is calculated

- **Average deed price:** sum of recorded prices ÷ number of homes with a recorded price.
- **Median MRP vs. last list:** `AGGREGATE(17,6, values/condition, 2)`, the median over homes in that state with both prices **and** `discount_sample` = `core` (column O): a recorded per-home price and a verified address. Other homes show blank in column L.
- **Median days listed:** the same median over `deed_record_date − first_list_date`.
- **MRP vs. comps (aggregate):** sum of MRP prices ÷ sum of comparable values − 1, over homes with both.
- **Average gross yield:** the average of each home's `rent × 12 ÷ price`, over homes with both.

[← Back to the main page](../README.md)
