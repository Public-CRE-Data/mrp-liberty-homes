# Unlevered IRR, 1–5 year holds

For each home with a recorded purchase price, an advertised rent and a Zillow zip-code forecast (513 homes), we compute the unlevered IRR of buying at MRP's price, renting, and selling after 1–5 years. The portfolio IRR combines all homes' cash flows.

| Hold | Portfolio IRR |
|---|---|
| 1 | 2.3% |
| 2 | 5.1% |
| 3 | 6.0% |
| 4 | 6.5% |
| 5 | 6.8% |

## Assumptions (editable in `1_assumptions.tsv`)

| Assumption | Base case |
|---|---|
| NOI margin (share of rent kept after vacancy, taxes, insurance, management, repairs) | 60% |
| Rent growth | 3% a year |
| Home price growth | Year 1: Zillow's 12-month forecast for the zip code; then 3% a year |
| Selling costs at exit | 3% |
| Initial lease-up (days with no rent; fixed costs still paid) | 0 days. Try 30 or 60. |

**Cash flows per home:** year 0 = −price. Year *y* = rent × 12 × margin × (1 + rent growth)^(y−1). Year 1 loses rent × lease-up days ÷ (365/12). In the final year, add price × (1 + Zillow forecast) × (1 + growth)^(N−1) × (1 − selling costs).

## Check our work in Excel

The files are tab-separated text: columns split automatically when pasted, and every cell starting with `=` becomes a live formula. Nothing needs downloading. Needs Excel 2010 or later (365 recommended). Pasted dates and zip codes may change format; that's fine, because it happens on every sheet.

1. Open a **new, blank Excel workbook** and create 3 sheets named exactly **`assumptions`**, **`homes`**, **`summary`**. The formulas refer to these names.
2. On GitHub open [`1_assumptions.tsv`](1_assumptions.tsv), click **Raw**, press **Ctrl+A** then **Ctrl+C**, click cell **A1** on the **`assumptions`** sheet and press **Ctrl+V**.
3. On GitHub open [`2_homes.tsv`](2_homes.tsv), click **Raw**, press **Ctrl+A** then **Ctrl+C**, click cell **A1** on the **`homes`** sheet and press **Ctrl+V**.
4. On GitHub open [`3_summary.tsv`](3_summary.tsv), click **Raw**, press **Ctrl+A** then **Ctrl+C**, click cell **A1** on the **`summary`** sheet and press **Ctrl+V**.
5. Wait a few seconds for Excel to finish calculating.
6. **Check:** every cell in the **check** column should be **0**. A 0 means Excel's formula reproduces our number exactly. The checks compare against our base case, so change the assumptions only after checking.

**Test your own assumptions:** change any value in column B of the `assumptions` sheet, for example the lease-up days to 60 or the margin to 0.55. Every home's IRR and the portfolio IRR update instantly. The check column will then show differences from our base case, which is expected.

**Caveats:** advertised rents may exceed signed leases. A 60% margin may be generous where insurance and taxes are high (Florida, Texas). There's no separate budget for major repairs. All-cash: no debt.

[← Back to the main page](../README.md)
