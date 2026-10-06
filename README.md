# MRP Liberty homes: Lennar homes bought by Millrose's MRP Liberty LLC

Home-level data on the finished Lennar homes that **MRP Liberty LLC** (a subsidiary of Millrose Properties, Inc.) bought from Lennar entities in Aug–Oct 2026, with purchase prices, last asking prices, time on market, comparable sales and asking rents.

Snapshot: **2026-10-04** (Zillow data added 2026-10-05, Zillow base month Aug 2026). 1,034 homes in 15 states.

## Files

| File | What it is |
|---|---|
| `mrp_liberty_homes.csv` | One row per home (1,034 rows). |
| `summary_by_state.csv` | State totals and medians, plus an `ALL` row. |
| `mrp_vs_slate_same_house_type.csv` | MRP vs. Slate (another institutional buyer of Lennar homes): same community, same bedrooms, within 10% of the same square footage. |
| `zillow/` | Zillow home price forecasts and home value history for MRP's zip codes. See [Zillow home price analysis](#zillow-home-price-analysis). |

## Headline numbers

| Measure | Result |
|---|---|
| Homes identified | 1,034 (500 with a recorded purchase price) |
| MRP price vs. last asking price | median **−2.8%**, mean −1.6% (289 homes) |
| Days listed for sale before the MRP deed | median **86 days** (229 homes) |
| MRP price vs. same-community comparable sales | **−1.2%** in aggregate (399 homes) |
| MRP vs. Slate, same house type | MRP median −1.9% vs. Slate (7 matched homes; small sample) |
| Homes with an asking rent | 873 |
| Zillow 12-month home price forecast, MRP zip codes (value-weighted) | **+0.3%** vs. +1.4% for the US (Aug 2026 to Aug 2027) |

## Column notes: `mrp_liberty_homes.csv`

- **mrp_price:** from county deed records (stated consideration, deed stamps or assessor sale price; method in `price_source`). **Texas does not disclose sale prices**, so Texas homes have none.
- **evidence:** how the home was tied to MRP Liberty. A = deed seen and matched to the address; B = deed seen, address matched within a batch or not yet resolved; C = weaker evidence.
- **last_list_price / last_list_date:** the last asking price before the home went pending, sold or off market, from MLS price histories (mostly realtor.com price history, plus movoto.com, local MLS broker sites and dated Lennar builder listings). A sale price is never used as a list price, and entries posted at exactly MRP's price after the sale are excluded.
- **list_price_quality:** `one_source`, `two_sources` (two independent sites agree) or `resolved_by_date` (two sites disagreed; the most recent was used).
- **first_list_date / days_listed_before_mrp_deed:** first date the home was offered for sale within the 12 months before the deed, ignoring brief pre-construction listings that came down within 7 days. Days are counted to the deed record date.
- **mrp_vs_last_list_pct:** MRP price ÷ last list price − 1. Negative means MRP paid below the last asking price.
- **comp_value / mrp_vs_comp_pct:** value from Lennar sales to individual buyers in the same community (same plan size where available); `comp_basis` gives the method.
- **asking_rent:** advertised monthly rent on the property manager's public rental listings (Evergreen Live). These are **asking** rents, not signed leases.
- **gross_yield_pct:** asking rent × 12 ÷ MRP price.
- **zillow_fc_1m_pct / zillow_fc_3m_pct / zillow_fc_12m_pct:** Zillow's forecast % change in typical home value for the home's zip code (or its metro if the zip has no forecast) over 1, 3 and 12 months from Aug 31, 2026. `zillow_forecast_source` says which.
- **weight_value / weight_value_basis:** the dollar value used to weight this home in the Zillow averages (see below).
- **zhvi_zip_basis:** which Zillow zip-code home value series this home's weight goes to.

## Caveats

- **Coverage.** Not every MRP purchase may be found. Some deeds recorded in early October 2026 are known only by lot and block (`address` says "lot only").
- **List prices are missing for many homes.** Homes sold before reaching the public MLS have no listing history.
- **Outliers.** About 17 homes show MRP paying more than 10% above the last asking price. Some are probably a different builder's listing at the same address, so the **median** is the more reliable figure.
- **Small samples in some states.** The Slate comparison rests on 7 matched homes.
- **Not investment advice.** Data is compiled from public records and public listing pages and may contain errors. Check against the original sources before relying on it.

## Zillow home price analysis

![Single-family home values: MRP Liberty zip codes vs. United States](zillow/home_value_index_mrp_vs_us.png)

| Measure | MRP Liberty zip codes | United States |
|---|---|---|
| Zillow forecast, 12 months to Aug 2027 | **+0.3%** (value-weighted) | +1.4% |
| Zillow forecast, 3 months to Nov 2026 | +0.3% | +0.6% |
| Home values, change since Jan 2020 | +44.4% | +48.2% |
| Home values, last 12 months (to Aug 2026) | −0.9% | +1.3% |
| Share of portfolio value where Zillow forecasts a decline | 38% | |

By state, Zillow's 12-month forecast is weakest for Texas (−0.9%, 30% of value) and Florida (−0.8%, 14%), and strongest for Georgia (+2.2%) and Oklahoma (+2.1%). Full breakdown by state and metro: `zillow/hpa_forecast_summary.csv`.

### Files

| File | What it is |
|---|---|
| `zillow/hpa_forecast_summary.csv` | Value-weighted 1-, 3- and 12-month forecasts: all homes, US benchmark, by state, by metro. Also the equal-weighted average, min/max, and share of value with a negative forecast. |
| `zillow/home_value_index_mrp_vs_us.csv` | Monthly index, Jan 2000 to Aug 2026 (Jan 2020 = 100): MRP-weighted zip codes vs. Zillow's US index, plus the US dollar value and how many MRP zips had data each month. |
| `zillow/home_value_index_mrp_vs_us.png` | The chart above. |
| `zillow/zip_weights_and_forecasts.csv` | The 506 zip codes used: MRP homes, dollar weight, weight share, latest Zillow home value and Zillow forecasts. |
| `zillow/zhvi_sfr_monthly_mrp_zips.csv` | Zillow's monthly single-family home value series for those 506 zips, Jan 2000 to Aug 2026 (input to the index). |

### How it is calculated

**1. Weights (how much each home counts).** Each home is weighted by its dollar value, so larger holdings count more:
- the MRP deed price where recorded (500 homes);
- otherwise its last asking price less 1.63%, the average gap between MRP's price and the last asking price (293 homes; mostly Texas, where deed prices are not public);
- otherwise the average MRP deed price for its state (104 homes), or for all states (137 homes).

Total weight: $286 million. Each home's value and method are in `mrp_liberty_homes.csv` (`weight_value`, `weight_value_basis`).

**2. Forecast.** Each home takes the Zillow Home Value Forecast for its zip code (941 homes). Where the zip has no forecast, mostly lot-only deeds without a full address, it takes the forecast for the metro covering its county (93 homes). The portfolio forecast is the value-weighted average:
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

### Source data (downloaded Oct 5, 2026)

All from Zillow Research, [zillow.com/research/data](https://www.zillow.com/research/data/):
- **Home Values (ZHVI):** *ZHVI Single-Family Homes Time Series ($)*, mid tier, smoothed and seasonally adjusted, by zip code (`Zip_zhvi_uc_sfr_tier_0.33_0.67_sm_sa_month.csv`) and by metro and US (`Metro_zhvi_uc_sfr_tier_0.33_0.67_sm_sa_month.csv`).
- **Home Value Forecasts (ZHVF):** *ZHVF, all homes (single-family and condo)*, mid tier, smoothed and seasonally adjusted, by zip code (`Zip_zhvf_growth_uc_sfrcondo_tier_0.33_0.67_sm_sa_month.csv`) and by metro and US (`Metro_zhvf_growth_uc_sfrcondo_tier_0.33_0.67_sm_sa_month.csv`).

Zillow data is used with attribution under Zillow's terms of use for its research data. The ZHVI and ZHVF are Zillow's estimates, not appraisals.

## Sources

County recorder and assessor records (deeds, parcels, stated consideration); realtor.com and movoto.com listing price histories and local MLS broker sites; Lennar.com; Evergreen Live public rental listings (listings.ender.com); okcountyrecords.com and county GIS parcel layers for lot-to-address matching; Zillow Research home value and forecast data ([zillow.com/research/data](https://www.zillow.com/research/data/)).
