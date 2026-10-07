# Population density: MRP vs. Lennar, Invitation Homes and AMH

Are MRP Liberty's homes in denser or more outlying areas than other single-family rental owners, and than Lennar's own communities? For every property we look up the **population density of its zip code** and rank it **within its own metro area**.

**Summary.** MRP's homes sit in about as outlying zip codes as **Lennar's own communities**, and in much less dense zip codes than the two largest single-family rental owners' listings.

| Portfolio | Properties | Median density (people per sq mi) | Median percentile in metro | % in least dense quarter |
|---|---|---|---|---|
| MRP Liberty | 1,006 | 364 | **23** | 52% |
| Lennar community | 1,376 | 584 | **24** | 51% |
| Invitation Homes | 3,461 | 1,887 | **42** | 29% |
| AMH | 3,361 | 1,154 | **33** | 36% |

**Median percentile in metro, by metro** (MRP's 12 largest metros; blank = no properties there):

| Metro | MRP Liberty | Lennar communities | Invitation Homes | AMH |
|---|---|---|---|---|
| San Antonio-New Braunfels, TX | 22 | 22 | 22 | 41 |
| Houston-The Woodlands-Sugar Land, TX | 8 | 9 | 37 | 28 |
| Dallas-Fort Worth-Arlington, TX | 13 | 12 | 28 | 26 |
| Ocala, FL | 61 | 57 |  |  |
| Myrtle Beach-Conway-North Myrtle Beach, SC-NC | 78 | 47 |  |  |
| Raleigh-Cary, NC | 25 | 34 | 35 | 31 |
| Austin-Round Rock-Georgetown, TX | 30 | 27 | 12 | 36 |
| Sherman-Denison, TX | 46 | 46 |  |  |
| Daphne-Fairhope-Foley, AL | 41 | 41 |  |  |
| Little Rock-North Little Rock-Conway, AR | 9 | 34 |  |  |
| Columbia, SC | 18 | 19 |  |  |
| Warner Robins, GA | 15 | 25 |  |  |

- **Texas:** MRP's ranking is almost identical to Lennar's communities in Houston, Dallas–Fort Worth and San Antonio. MRP's homes reflect where Lennar builds, not a worse-than-typical slice.
- **Arkansas:** MRP's homes in Little Rock and NW Arkansas are far more outlying than Lennar's communities there. Many came through Millrose's Rausch Coleman land.
- **Invitation Homes and AMH** mostly own older homes in established suburbs (41st and 33rd percentile), so MRP's homes face more nearby new construction.

## What the measures mean

- **Density:** people per square mile of land in the property's zip code (Census ZCTA).
- **Percentile in metro:** the share of the metro's residents who live in *less* dense zip codes than the property's.
  - 10 = more outlying than where 90% of the metro lives; 90 = denser than where 90% live.
  - It is weighted by people, not by zip code, so large, nearly empty rural zip codes don't distort the ranking.
  - Formula: `percentile = 100 × (population of the metro's zip codes with lower density) ÷ (population of all the metro's zip codes)`.
- **% in least dense quarter:** the share of properties whose percentile is below 25.

## Check our work in Excel (copy and paste, about 5 minutes)

The three files in this folder are tab-separated text. When you paste them into Excel, columns split automatically, and every formula (any cell starting with `=`) becomes a live Excel formula. Nothing needs to be downloaded.

1. Open a **new, blank Excel workbook**.
2. Rename the first sheet **`zips`**, then add two more sheets named **`homes`** and **`summary`**. The names must match exactly, because the formulas refer to them.
3. On GitHub, open [`1_zips.tsv`](1_zips.tsv) and click **Raw** (top right of the file).
4. Press **Ctrl+A** (select all), then **Ctrl+C** (copy).
5. In Excel, click cell **A1** on the **`zips`** sheet and press **Ctrl+V**.
6. Repeat steps 3–5 for [`2_homes.tsv`](2_homes.tsv) into the **`homes`** sheet, then [`3_summary.tsv`](3_summary.tsv) into the **`summary`** sheet.
7. Wait a few seconds for Excel to finish calculating. The bottom bar shows "Calculating" while it works.
8. **Check:** in the `homes` sheet, columns **K** and **L** should all show **0**, and in `summary`, column **K** should show **0** (blank where a portfolio has no properties in that metro). A 0 means Excel's formula gives exactly the same number as our analysis.
9. **Results:** scroll down the `summary` sheet. **Table 1** (from row 55) and **Table 2** (from row 61) rebuild the tables shown at the top of this section, calculated live from the pasted data.

If Excel turns pasted zip codes into numbers (for example `08001` into `8001`), that's fine: it happens on every sheet, so the lookups still match.

**Requirements:** Excel 2010 or later (Excel 365 recommended). The summary medians use `AGGREGATE`, which LibreOffice and Google Sheets don't support with this kind of input. Everything else works there too.

## What each sheet does

| Sheet | Columns | Formula |
|---|---|---|
| `zips` | zip, metro, population, land area, **density** | `=IF(D2>0,ROUND(C2/D2,6),"")`: population ÷ land area, rounded to 6 decimals so comparisons are exact |
| `homes` | portfolio, property, city, state, zip, **metro**, **density**, **percentile**, our results, checks | metro and density: `INDEX/MATCH` lookups on the `zips` sheet. Percentile: `=100*SUMIFS(population, metro, this metro, density, "<"&this density) / SUMIFS(population, metro, this metro, density, ">0")` |
| `summary` | portfolio, metro, count, median density, median percentile, % in least dense quarter, our results, check | count and %: `SUMPRODUCT` over the `homes` sheet. Medians: `AGGREGATE(17,6, values/condition, 2)`, the median of the rows that match the portfolio (and metro) |

## Sources (retrieved 2026-10-07)

- **Population:** US Census Bureau, American Community Survey 2019–2023 5-year estimates, table B01003 (total population) by ZCTA ([bulk file](https://www2.census.gov/programs-surveys/acs/summary_file/2023/table-based-SF/data/5YRData/acsdt5y2023-b01003.dat)).
- **Land area:** US Census Bureau, 2024 Gazetteer file for ZCTAs, `ALAND_SQMI` ([download](https://www2.census.gov/geo/docs/maps-data/data/gazetteer/2024_Gazetteer/2024_Gaz_zcta_national.zip)).
- **Metro for each zip code:** the `Metro` column of Zillow's zip-code home value file ([zillow.com/research/data](https://www.zillow.com/research/data/)), the same mapping used in the [Zillow analysis](../zillow/README.md).
- **MRP Liberty:** the homes in [`mrp_liberty_homes.csv`](../mrp_liberty_homes.csv) that have a zip code.
- **Invitation Homes:** every rental listing in Invitation Homes' public sitemap ([invitationhomes.com/property/sitemap.xml](https://www.invitationhomes.com/property/sitemap.xml)); the zip code is part of each listing's web address.
- **AMH:** the listings shown on each market search page linked from AMH's public sitemap ([amh.com/sitemap.xml](https://www.amh.com/sitemap.xml)).
- **Lennar:** the zip code on each community page in Lennar's public sitemap ([lennar.com sitemap](https://www.lennar.com/api/images/sitemapfe.xml)). Communities that redirect to a market page (closed out) are excluded.

All three sites' `robots.txt` rules allow these pages.

## Caveats

- **INVH and AMH** figures cover homes currently or recently listed for rent, a sample of their portfolios (about 85,000 and 60,000 homes respectively). They should reflect where those companies own homes, but aren't a full list.
- **Lennar** counts each active community once, regardless of its number of homes.
- **Census population lags 2–5 years.** Fast-growing new-build zip codes, typical of MRP and Lennar, look less dense than they are today.

[← Back to the main page](../README.md)
