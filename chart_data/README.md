# Chart data: Millrose rental homes

Excel-ready data behind charts of the Millrose (MRP Liberty) rental-home analysis. Each file is tab-separated text, so columns split automatically when pasted into Excel, and cells starting with `=` become live formulas.

| Chart | What it shows | Data file | Excel chart |
|---|---|---|---|
| 1 | Homes by state | [`ex1_homes_by_state.tsv`](exhibits/ex1_homes_by_state.tsv) | Clustered column (State, Homes) |
| 2 | % of homes deeded per week, by recording date | [`ex2_deeds_by_recording_week.tsv`](exhibits/ex2_deeds_by_recording_week.tsv) | Clustered column of column C (% of dated homes, formula) |
| 2b | % of homes by signing or sale date (433-home sample) | [`ex2b_homes_by_signing_week.tsv`](exhibits/ex2b_homes_by_signing_week.tsv) | Clustered column of column C (% of sampled homes, formula) |
| 3 | MRP price vs. last asking price | [`ex3_price_vs_last_list.tsv`](exhibits/ex3_price_vs_last_list.tsv) | Clustered column (band, % of homes) |
| 4 | Days listed before MRP bought | [`ex4_days_listed.tsv`](exhibits/ex4_days_listed.tsv) | Clustered column |
| 5 | Purchase price bands | [`ex5_purchase_price.tsv`](exhibits/ex5_purchase_price.tsv) | Clustered column |
| 5b | Population density vs. new-home communities, AMH and Invitation Homes | [`ex5b_density.tsv`](exhibits/ex5b_density.tsv) | Clustered bar (Portfolio, Median density); add the percentile as data labels |
| 5c | Asking rents vs. AMH and Invitation Homes, same metros | [`ex5c_rents_vs_peers.tsv`](exhibits/ex5c_rents_vs_peers.tsv) | Clustered column (Metro; Millrose, AMH and Invitation Homes rents); columns H–I give Millrose's gap (formulas) |
| 6 | Gross yield and estimated NOI yield by state | [`ex6_yields_by_state.tsv`](exhibits/ex6_yields_by_state.tsv) | Combo: gross yield as columns, NOI yield (formula = gross × 60%) as markers only |
| 6b | Gross and NOI yield by discount to deed price | [`ex6b_yields_by_discount.tsv`](exhibits/ex6b_yields_by_discount.tsv) | Clustered column (discount; gross and NOI yield, both formulas) |
| 7 | Unlevered IRR by hold period, three scenarios, at deed prices | [`ex7_irr_scenarios.tsv`](exhibits/ex7_irr_scenarios.tsv) | Line with markers; format the "9% core option-book yield" series as a red dashed line with no markers |
| 7b | Same, at a 20% discount to deed prices | [`ex7b_irr_20pct_discount.tsv`](exhibits/ex7b_irr_20pct_discount.tsv) | As for Exhibit 7 |
| 7c | Home price growth needed for a 9% IRR, and 5-yr IRR, by discount to deed price | [`ex7c_irr_by_discount.tsv`](exhibits/ex7c_irr_by_discount.tsv) | Two charts: clustered column (column B) and line with markers (columns C–D); add a 9% horizontal line to the second |
| 8 | Zillow home value index, Millrose markets vs. US | [`ex8_home_value_index.tsv`](exhibits/ex8_home_value_index.tsv) | Line (Month on the horizontal axis) |
| 9 | Rental-home spend vs. homesite book | [`ex9_rental_vs_book.tsv`](exhibits/ex9_rental_vs_book.tsv) | Clustered bar ($ billions) |

**Steps (Excel 2010 or later):**

1. Open a new, blank Excel workbook.
2. Open the exhibit's data file on GitHub, click **Raw**, press **Ctrl+A** then **Ctrl+C**.
3. Click cell **A1** on a blank sheet and press **Ctrl+V**.
4. Select the filled cells and choose **Insert → Recommended Charts**, then pick the chart type listed in the table.
5. Format percentage columns as **%** if they show decimals (e.g. 0.0866 = 8.66%).
6. **Chart 6 only:** right-click the chart → **Change Chart Type → Combo**. Set the NOI yield series to **Line with Markers**, then set its line to **No line**.
7. **Charts 7 and 7b:** right-click the 9% series → **Format Data Series**. Set the line to red and dashed, and set markers to **None**.

**Where the numbers come from:** home-level data for Exhibits 1–6 is in [`../mrp_liberty_homes.csv`](../mrp_liberty_homes.csv), and the density data and its Excel checks are in [`../density/`](../density/). Weekly pace and county record checks are in [`../pace/`](../pace/). Return inputs are in [`../irr/`](../irr/), and the Zillow index and forecasts are in [`../zillow/`](../zillow/).

[← Back to the main page](../README.md)
