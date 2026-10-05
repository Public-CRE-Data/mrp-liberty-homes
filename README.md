# MRP Liberty homes: Lennar homes bought by Millrose's MRP Liberty LLC

Home-level data on the finished Lennar homes that **MRP Liberty LLC** (a subsidiary of Millrose Properties, Inc.) bought from Lennar entities in Aug–Oct 2026, with purchase prices, last asking prices, time on market, comparable sales and asking rents.

Snapshot: **2026-10-04**. 1,034 homes in 15 states.

## Files

| File | What it is |
|---|---|
| `mrp_liberty_homes.csv` | One row per home (1,034 rows). |
| `summary_by_state.csv` | State totals and medians, plus an `ALL` row. |
| `mrp_vs_slate_same_house_type.csv` | MRP vs. Slate (another institutional buyer of Lennar homes): same community, same bedrooms, within 10% of the same square footage. |

## Headline numbers

| Measure | Result |
|---|---|
| Homes identified | 1,034 (500 with a recorded purchase price) |
| MRP price vs. last asking price | median **−2.8%**, mean −1.6% (289 homes) |
| Days listed for sale before the MRP deed | median **86 days** (229 homes) |
| MRP price vs. same-community comparable sales | **−1.2%** in aggregate (399 homes) |
| MRP vs. Slate, same house type | MRP median −1.9% vs. Slate (7 matched homes; small sample) |
| Homes with an asking rent | 873 |

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

## Caveats

- **Coverage.** Not every MRP purchase may be found. Some deeds recorded in early October 2026 are known only by lot and block (`address` says "lot only").
- **List prices are missing for many homes.** Homes sold before reaching the public MLS have no listing history.
- **Outliers.** About 17 homes show MRP paying more than 10% above the last asking price. Some are probably a different builder's listing at the same address, so the **median** is the more reliable figure.
- **Small samples in some states.** The Slate comparison rests on 7 matched homes.
- **Not investment advice.** Data is compiled from public records and public listing pages and may contain errors. Check against the original sources before relying on it.

## Sources

County recorder and assessor records (deeds, parcels, stated consideration); realtor.com and movoto.com listing price histories and local MLS broker sites; Lennar.com; Evergreen Live public rental listings (listings.ender.com); okcountyrecords.com and county GIS parcel layers for lot-to-address matching.
