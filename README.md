# MRP Liberty homes: Lennar homes bought by Millrose's MRP Liberty LLC

Data on the finished Lennar homes that **MRP Liberty LLC** (a subsidiary of Millrose Properties, Inc.) bought in Aug–Oct 2026: purchase prices, last asking prices, time on market, comparable sales, asking rents, Zillow price outlook, location density and investment returns. Every headline number can be **rebuilt in Excel by copy and paste**, with live formulas and check columns.

Snapshot: **2026-10-07** (Oklahoma deed prices, Muskogee County and 7 Lincoln County parcel links added 2026-10-08; list prices re-sourced 2026-10-08). Zillow data: base month Aug 2026.

## What we found

We identified **1,045 properties** deeded to MRP Liberty LLC in public county records (Aug–Oct 2026), almost all bought from Lennar entities. **988** are advertised for rent as single-family homes by its property manager, Evergreen Live; for **918** of those, MRP ownership and the rental listing are verified at the exact address or parcel.

| Evidence | Properties | How solid |
|---|---|---|
| Deeded to MRP Liberty LLC in county records | **1,045** | 1,030 with an MRP Liberty deed seen; 15 with MRP Liberty as owner of record (deed not seen) |
| ...bought from a Lennar entity | 1,028 | 987 with the deed seen; 41 inferred from Lennar as prior owner in the title chain. 2 bought from other sellers |
| **Rental listing linked: verified** | **918** | 670 exact deed address (+8 with a hand-checked spelling difference), 182 county parcel matches (block/lot or parcel ID to address), 58 with MRP Liberty as owner of record at the listing's address |
| Rental listing linked: moderate | 70 | Deed seen, but the address was assigned within a batch of deeds (e.g. 13 in Brunswick County NC) |
| No rental listing matched | 57 | 37 have a home-level recorded price ($161,039+); the rest are lot-only deeds or not yet listed |

Every property's `link_quality` and `seller_basis` are in [`mrp_liberty_homes.csv`](mrp_liberty_homes.csv), so you can filter to any tier.

## Headline numbers

| Measure | Result |
|---|---|
| Properties identified | 1,045 (550 with a recorded purchase price) |
| Estimated total spent by MRP Liberty | ≈ $285 million (recorded prices plus estimates where prices aren't public, e.g. Texas and Idaho; method in [zillow/README.md](zillow/README.md)) |
| MRP price vs. last asking price | median **−3.2%**, mean −2.9% (302 homes with a recorded per-home price and a verified address; −3.7% for the 215 with a full listing history) |
| Days listed for sale before the MRP deed | median **79 days** (338 homes) |
| MRP price vs. same-community comparable sales | **0.0%** in aggregate (379 homes) |
| Advertised for rent | 988 homes, average $1,859/month; average gross yield 8.2% |
| Zillow 12-month home price forecast, MRP zip codes | **+0.3%** (value-weighted) vs. +1.4% for the US |
| Unlevered IRR (60% NOI margin, 3% growth, 3% selling costs) | **2.3%** over 1 year, **6.0%** over 3, **6.8%** over 5 |
| Population density of MRP zip codes, rank within metro | median **22nd** percentile vs. 24th for Lennar communities, 42nd for Invitation Homes, 33rd for AMH |

### MRP price vs. last asking price: which homes count

The headline uses the **302 homes** where both prices are solid: a recorded per-home deed price and a verified address. 51 homes with both prices are left out and marked in `discount_sample`: 45 where the MRP price is an estimate (deed stamps, CoStar, or a bulk deed split evenly) and 6 whose address was assigned within a batch of deeds.

| Sample | Homes | Median | Mean |
|---|---|---|---|
| All homes with both prices | 353 | −2.9% | −1.8% |
| **Headline: recorded price + verified address** | **302** | **−3.2%** | **−2.9%** |
| …last list price from realtor.com price history | 259 | −3.4% | −2.9% |
| …home has a full listing history (first list date known) | 215 | −3.7% | −3.1% |

By state (headline sample): Arkansas −5.8% (54 homes), Florida −4.3% (74), Oklahoma −3.0% (25), Minnesota −2.8% (14), South Carolina −2.4% (51), North Carolina −1.8% (48), Tennessee −1.7% (21).

Homes that sold after a full public listing show larger discounts than homes that were barely marketed, so the figure depends on which homes are in the sample. Builder-aggregator prices (Jome, NewHomeSource) are not used: they are often undated or stale.

## What's here

| Folder / file | What it is | Check it in Excel |
|---|---|---|
| `mrp_liberty_homes.csv` | One row per property (1,045) with all fields; column notes below | via [headline/](headline/) |
| `summary_by_state.csv` | State totals and medians, plus an `ALL` row | via [headline/](headline/) |
| `mrp_vs_slate_same_house_type.csv` | MRP vs. Slate (another institutional buyer of Lennar homes), same community and house type | |
| [`headline/`](headline/) | Copy-paste rebuild of the headline numbers by state | [headline/README.md](headline/README.md) |
| [`zillow/`](zillow/) | Zillow home values (indexed) and price forecasts for MRP's zip codes vs. the US | [zillow/README.md](zillow/README.md) |
| [`irr/`](irr/) | 1–5 year unlevered IRRs per home and for the portfolio, with editable assumptions | [irr/README.md](irr/README.md) |
| [`density/`](density/) | Zip-code population density vs. Lennar's communities, Invitation Homes and AMH | [density/README.md](density/README.md) |
| [`homebuilders/`](homebuilders/) | 2026 vs. 2025 deliveries and starts for 14 public homebuilders | [homebuilders/README.md](homebuilders/README.md) |

## Column notes: `mrp_liberty_homes.csv`

- **deed_record_date / deed_date_note:** the deed's recording date (YYYY-MM-DD); where the county index shows more than one date, the full text is in `deed_date_note`.
- **mrp_price:** from county deed records (stated consideration, deed stamps or assessor sale price; method in `price_source`). **Texas does not disclose sale prices**, so Texas homes have none.
- **evidence:** how the home was tied to MRP Liberty. A = deed seen and matched to the address; B = deed seen, address matched within a batch or not yet resolved; C = weaker evidence.
- **last_list_price / last_list_date:** the last asking price before the home went pending, sold or off market, from MLS price histories (mostly realtor.com price history, plus movoto.com and local MLS broker sites). A sale price is never used as a list price, and entries posted at exactly MRP's price after the sale are excluded.
- **list_price_quality:** `one_source`, `two_sources` (two independent sites agree) or `resolved_by_date` (two sites disagreed; the most recent was used).
- **first_list_date / days_listed_before_mrp_deed:** first date the home was offered for sale within the 12 months before the deed, ignoring brief pre-construction listings that came down within 7 days. Days = `deed_record_date` − `first_list_date`.
- **mrp_vs_last_list_pct:** MRP price ÷ last list price − 1. Negative means MRP paid below the last asking price.
- **discount_sample:** `core` if the home counts in the headline MRP-vs-last-list figures; otherwise the reason it is left out.
- **comp_value / mrp_vs_comp_pct:** value from Lennar sales to individual buyers in the same community (same plan size where available); `comp_basis` gives the method.
- **link_quality:** how the rental listing was tied to the deed: `verified: exact address`, `verified: county parcel match`, `verified: MRP owner of record at address`, `moderate: address assigned within a batch of deeds`, or `no rental listing matched`. Probable matches are never used.
- **seller_basis:** `deed seen (Lennar seller)`, `Lennar inferred from prior owner in title chain`, `owner of record only (deed not seen)` or `deed seen (non-Lennar seller)`.
- **asking_rent:** advertised monthly rent on the property manager's public rental listings (Evergreen Live). These are **asking** rents, not signed leases.
- **gross_yield_pct:** asking rent × 12 ÷ MRP price.
- **zillow_fc_1m_pct / zillow_fc_3m_pct / zillow_fc_12m_pct:** Zillow's forecast % change in typical home value for the home's zip code (or its metro if the zip has no forecast) over 1, 3 and 12 months from Aug 31, 2026. `zillow_forecast_source` says which.
- **weight_value / weight_value_basis:** the dollar value used to weight this home in the Zillow averages (see [zillow/README.md](zillow/README.md)).
- **zhvi_zip_basis:** which Zillow zip-code home value series this home's weight goes to.


## Caveats

- **Coverage.** These are the properties we could find in public deed records. Purchases recorded after early October, and counties whose records need a login or CAPTCHA, aren't included, so the true total is likely somewhat higher. 37 deeds are still known only by lot and block (`address` says "lot only").
- **List prices are missing for many homes.** Homes sold before reaching the public MLS have no listing history.
- **Outliers.** About 17 homes show MRP paying more than 10% above the last asking price. Some are probably a different builder's listing at the same address, so the **median** is the more reliable figure.
- **Small samples in some states.** The Slate comparison rests on 7 matched homes.
- **Not investment advice.** Data is compiled from public records and public listing pages and may contain errors. Check against the original sources before relying on it.

## Sources

County recorder and assessor records (deeds, parcels, stated consideration); realtor.com and movoto.com listing price histories and local MLS broker sites; Lennar.com; Evergreen Live public rental listings (listings.ender.com); okcountyrecords.com and county GIS parcel layers for lot-to-address matching; Zillow Research home value and forecast data ([zillow.com/research/data](https://www.zillow.com/research/data/)); US Census Bureau population (ACS 2019–2023) and zip-code land area (2024 Gazetteer); Invitation Homes, AMH and Lennar public websites (density benchmarks). Each folder README lists its exact sources and download dates.
