# Zillow home price analysis

![Single-family home values: MRP Liberty zip codes vs. United States](home_value_index_mrp_vs_us.png)

| Measure | MRP Liberty zip codes | United States |
|---|---|---|
| Zillow forecast, 12 months to Aug 2027 | **+0.3%** (value-weighted) | +1.4% |
| Zillow forecast, 3 months to Nov 2026 | +0.3% | +0.6% |
| Home values, change since Jan 2020 | +44.2% | +48.2% |
| Home values, last 12 months (to Aug 2026) | −1.0% | +1.3% |
| Share of portfolio value where Zillow forecasts a decline | 37% | |

By state, Zillow's 12-month forecast is weakest for Texas (−0.9%, 30% of value) and Florida (−0.8%, 14%), and strongest for Georgia (+2.2%) and Oklahoma (+2.1%). Full breakdown by state and metro: `hpa_forecast_summary.csv`.

## Files

| File | What it is |
|---|---|
| `hpa_forecast_summary.csv` | Value-weighted 1-, 3- and 12-month forecasts: all homes, US benchmark, by state, by metro. Also the equal-weighted average, min/max, and share of value with a negative forecast. |
| `home_value_index_mrp_vs_us.csv` | Monthly index, Jan 2000 to Aug 2026 (Jan 2020 = 100): MRP-weighted zip codes vs. Zillow's US index, plus the US dollar value and how many MRP zips had data each month. The last row is Zillow's forecast for Aug 2027 (`type` column marks actual vs. forecast). |
| `home_value_index_mrp_vs_us.png` | The chart above. |
| `zip_weights_and_forecasts.csv` | The 287 zip codes used: MRP homes, dollar weight, weight share, latest Zillow home value and Zillow forecasts. |
| `zhvi_sfr_monthly_mrp_zips.csv` | Zillow's monthly single-family home value series for those 287 zips, Jan 2000 to Aug 2026 (input to the index). |

## How it is calculated

**1. Weights (how much each home counts).** Each home is weighted by its dollar value, so larger holdings count more:
- the MRP deed price where recorded (500 homes);
- otherwise its last asking price less 1.63%, the average gap between MRP's price and the last asking price (293 homes; mostly Texas, where deed prices are not public);
- otherwise the average MRP deed price for its state (104 homes), or for all states (144 homes; mostly Texas and Idaho, which don't disclose prices).

Total weight: $289 million (an estimate of MRP's total spend; about half is recorded prices, half estimated). Each home's value and method are in [`mrp_liberty_homes.csv`](../mrp_liberty_homes.csv) (`weight_value`, `weight_value_basis`).

**2. Forecast.** Each home takes the Zillow Home Value Forecast for its zip code (1,008 homes). Where the zip has no forecast, mostly lot-only deeds without a full address, it takes the forecast for the metro covering its county (33 homes). The portfolio forecast is the value-weighted average:
  `forecast = Σ(weight × zip forecast) ÷ Σ(weight)`.
Equal-weighting the homes gives almost the same answer (+0.29% vs. +0.30%).

**3. Home value index.**
- Each home's weight goes to its zip code's Zillow Home Value Index series. A home whose zip has no Zillow series is split evenly across the Zillow zips in its county.
- Each month, the index moves by the weighted average of the zips' one-month % changes, using only zips with data in both months: `index(t) = index(t−1) × (1 + Σ wᵢ·(ZHVIᵢ(t)/ZHVIᵢ(t−1) − 1) ÷ Σ wᵢ)`.
- Chaining the monthly changes this way means zips that start reporting later (new-build areas) neither drop out nor cause jumps.
- The index is rebased to Jan 2020 = 100. The US line is Zillow's own national index for the same series, rebased the same way.
- The dotted forecast lines extend each series by its 12-month forecast.

**Zillow series used, and why**
- **History:** ZHVI, **single-family homes only**, mid tier (the middle third of home values, 33rd–67th percentile), smoothed and seasonally adjusted. MRP owns single-family homes and townhomes, not condos, and its homes are priced in the middle of their local markets.
- **Forecast:** Zillow Home Value Forecast, smoothed and seasonally adjusted, base month Aug 2026. Zillow publishes forecasts only for single-family and condo homes combined, so the forecast covers a slightly broader set of homes than the history. Zillow also publishes an unadjusted forecast, which shows +1.7% for the US over 12 months.

**Limits.** Zillow's indices and forecasts describe a typical existing home in each zip code, not MRP's new-build homes. Newly built homes can lag the local index when builders cut prices or offer incentives. Zillow revises its forecasts monthly.

## Source data (downloaded Oct 5, 2026)

All from Zillow Research, [zillow.com/research/data](https://www.zillow.com/research/data/):
- **Home Values (ZHVI):** *ZHVI Single-Family Homes Time Series ($)*, mid tier, smoothed and seasonally adjusted, by zip code (`Zip_zhvi_uc_sfr_tier_0.33_0.67_sm_sa_month.csv`) and by metro and US (`Metro_zhvi_uc_sfr_tier_0.33_0.67_sm_sa_month.csv`).
- **Home Value Forecasts (ZHVF):** *ZHVF, all homes (single-family and condo)*, mid tier, smoothed and seasonally adjusted, by zip code (`Zip_zhvf_growth_uc_sfrcondo_tier_0.33_0.67_sm_sa_month.csv`) and by metro and US (`Metro_zhvf_growth_uc_sfrcondo_tier_0.33_0.67_sm_sa_month.csv`).

Zillow data is used with attribution under Zillow's terms of use for its research data. The ZHVI and ZHVF are Zillow's estimates, not appraisals.

## Check our work in Excel

Two independent checks: the **forecast** (one sheet) and the **home value index** (two sheets). Do them in separate workbooks.

The files are tab-separated text: columns split automatically when pasted, and every cell starting with `=` becomes a live formula. Nothing needs downloading. Needs Excel 2010 or later (365 recommended). Pasted dates and zip codes may change format; that's fine, because it happens on every sheet.

**Forecast by state:**
1. Open a **new, blank Excel workbook** and create 1 sheet named exactly **`forecast`**. The formulas refer to these names.
2. On GitHub open [`check_3_forecast.tsv`](check_3_forecast.tsv), click **Raw**, press **Ctrl+A** then **Ctrl+C**, click cell **A1** on the **`forecast`** sheet and press **Ctrl+V**.
3. Wait a few seconds for Excel to finish calculating.
4. **Check:** every cell in the **check** column should be **0**. A 0 means Excel's formula reproduces our number exactly.

**Home value index (Jan 2000 – Aug 2026):**
1. Open a **new, blank Excel workbook** and create 2 sheets named exactly **`zips`**, **`index`**. The formulas refer to these names.
2. On GitHub open [`check_1_zips.tsv`](check_1_zips.tsv), click **Raw**, press **Ctrl+A** then **Ctrl+C**, click cell **A1** on the **`zips`** sheet and press **Ctrl+V**.
3. On GitHub open [`check_2_index.tsv`](check_2_index.tsv), click **Raw**, press **Ctrl+A** then **Ctrl+C**, click cell **A1** on the **`index`** sheet and press **Ctrl+V**.
4. Wait a few seconds for Excel to finish calculating.
5. **Check:** every cell in the **check** column should be **0**. A 0 means Excel's formula reproduces our number exactly.

- `zips`: each zip code's dollar weight and its monthly Zillow values.
- `index`: each month's weighted 1-month change, `SUMPRODUCT(weight × (this month ÷ last month − 1))` over zips with data in both months ÷ their total weight, chained into an index and rebased to Jan 2020 = 100.

[← Back to the main page](../README.md)
