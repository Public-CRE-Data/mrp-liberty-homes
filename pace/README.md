# Pace of MRP Liberty's purchases: buying appears to have paused since Oct 5

Based on county deed records, MRP Liberty LLC (Millrose Properties' home-buying subsidiary) appears to have bought Lennar homes in **two bursts around Lennar's quarter-ends** and then stopped. A re-check on **Oct 19, 2026** of about 190 counties we can search found **no Lennar-to-MRP Liberty deed recorded after Oct 5**, although most county records were current to Oct 12–19.

## Homes deeded to MRP Liberty, by week

| Week starting | Homes |
|---|---|
| Aug 24 | 132 |
| **Aug 31** (Lennar's fiscal Q3 ends Aug 31) | **682** |
| Sep 7 | 154 |
| Sep 14 | 13 |
| Sep 21 | 4 |
| Sep 28 (around Sep 30) | 37 |
| Oct 5 | 16 (the last Lennar deeds on Oct 5, plus a 6-home build-to-rent closing on Oct 7) |
| **Oct 12** | **0** |
| **Oct 19** | **0** |

- 1,038 of the 1,107 homes have a date: the recording date, or where the index doesn't show one, the deed or sale date from the assessor. The other 68 are known only as owned by MRP Liberty, with no date. One deed was recorded in May.
- **About 93% were dated in the three weeks around the Aug 31 quarter-end.** A smaller burst came around Sep 30.

## Why we believe this is a pause, not slow record-keeping

County records lag. An empty week can simply mean the county hasn't caught up. So for each county we recorded **how current its records are**, and compared that with the latest MRP Liberty deed:

| Examples (full list in [`3_county_checks.tsv`](3_county_checks.tsv)) | Records current through | Latest MRP Liberty deed | MRP homes |
|---|---|---|---|
| Collin, TX (clerk deed index) | Oct 19 | Oct 1 | 50 |
| Harris, TX (clerk deed index) | Oct 16 | Oct 2 | 37 |
| Travis, TX (clerk index, temporary) | Oct 19 | Sep 3 | 5 |
| Williamson, TX (clerk deed index) | Oct 14 | Sep 11 | 26 |
| Marion, FL (clerk deed index, verified) | Oct 18 | Oct 1 | 44 |
| Wake, NC (register of deeds) | Oct 16 | Sep 25 | 31 |
| Horry, SC (register of deeds, released) | Oct 12 | Sep 25 | 27 |
| Sebastian, AR (assessor, filed dates) | Oct 14 | Oct 5 | 7 |

- **In about 35 counties whose records run to Oct 14–19, the latest MRP Liberty deed is Oct 5 or earlier.** These include Millrose's largest markets in Texas, Florida, the Carolinas and Arizona, plus Minnesota's state sale filings.
- In the same counties, **Lennar kept recording sales to individual buyers** during those weeks, which suggests records were flowing.
- **Owner records match the deeds.** County owner lists show the same MRP Liberty homes as a week earlier, and no MRP Liberty homes have been resold.
- Millrose's land-bank entities (MRP H… LLCs, Millrose Properties [state] LLCs) kept recording land deals with several builders through mid-October. **The pause appears to be in finished-home purchases, not the land business.**

**Limits:**
- Many county sources are tax or map layers, which lag deed books by days to weeks. The cleanest evidence is the clerk and register-of-deeds indexes above.
- Counties we can't search (logins, CAPTCHAs, disclaimer gates) could still hold later deeds.
- What looks like a pause could also be a quarter-end buying pattern. **The next test is Lennar's Nov 30 fiscal year-end:** if purchases resume around then, quarter-end timing would be the more likely explanation; if not, a sustained pause would be.

## Files

| File (paste into sheet) | What it is |
|---|---|
| [`1_deeds.tsv`](1_deeds.tsv) → `deeds` | All 1,107 homes: state, county, address, deed date and its basis |
| [`2_weekly.tsv`](2_weekly.tsv) → `weekly` | Homes per week (live `COUNTIFS` formulas) with a check column |
| [`3_county_checks.tsv`](3_county_checks.tsv) → `counties` | 37 counties: the source searched, how current its records are, MRP Liberty homes, latest deed date, and days with no MRP deed before the records end (formulas) |

## Check our work in Excel

The files are tab-separated text: columns split automatically when pasted, and every cell starting with `=` becomes a live formula. Needs Excel 2010 or later.

1. Open a **new, blank Excel workbook** and create 3 sheets named exactly **`deeds`**, **`weekly`**, **`counties`**.
2. For each file: open it on GitHub, click **Raw**, press **Ctrl+A** then **Ctrl+C**, click cell **A1** on the matching sheet and press **Ctrl+V**. Paste `1_deeds.tsv` first.
3. **Check:** every cell in the **check** column on `weekly` should be **0**.

If the "records current through" column shows numbers instead of dates, format it as a date. The county list was compiled on Oct 19, 2026, from public clerk, recorder, assessor and state sale-filing sources.

[← Back to the main page](../README.md)
