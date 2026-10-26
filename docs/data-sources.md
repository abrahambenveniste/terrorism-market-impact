# Data-source review

**Reviewed:** 2026-10-26. These notes record source documentation available on that date; recheck terms, endpoints, and coverage at every data retrieval.

## Event data

### Primary historical source: Global Terrorism Database (GTD)

- [Download and terms](https://www.start.umd.edu/download-global-terrorism-database)
- [Methodology and citation](https://www.start.umd.edu/using-gtd)
- [FAQ](https://www.start.umd.edu/gtd-faqs)
- Current published full data: 1970–2020; separate partial file: January–June 2021. START says ongoing collection stopped after the partial 2021 file because funding ended.
- There is a known 1993 incident-level gap: the original cards were lost. Country-level aggregate counts were reconstructed, but individual events cannot be treated as observed.
- GTD reflects public reporting. START describes its corroboration effort but does not claim every reported detail is independently verified as true. Definitions are operationalized through coded inclusion criteria, not a universal definition of terrorism.
- GTD is limited to non-state terrorism and excludes state terrorism. Its inclusion criteria, `doubtterr`, and other fields allow researchers to construct stricter and broader samples.
- Access requires completing START's form and accepting its EULA. The EULA bars republishing or redistributing the raw dataset. Raw GTD files, event narratives, and source material must not be committed to this public repository. Cite the exact version and document changes to the analysis sample.
- Planned use: main historical event series, with a pre-registered strict sample (`crit1=1`, `crit2=1`, `crit3=1`, `doubtterr=0`) and a clearly labeled sensitivity sample. Unknown fatalities/injuries remain missing, not zero.

### Separate validation / extension source: ACLED

- [API guide](https://acleddata.com/acled-api-documentation)
- [Terms of use](https://acleddata.com/terms-use) and [EULA](https://acleddata.com/eula)
- API access requires an account. The current EULA and attribution rules restrict direct sharing of original/raw data; recheck the exact permitted public outputs before use.
- ACLED records political violence and demonstrations with categories and coding rules that are not equivalent to GTD's terrorism definition. Its coverage and classification also vary by time and place.
- Planned use: a separately labeled validation or post-2020 descriptive appendix only if access and public-output terms permit. Do not concatenate ACLED rows with GTD as one homogeneous event series.

## Equity-market data

### Cross-country candidates

| Source | What the official documentation establishes | Suitability for daily event study |
|---|---|---|
| [World Bank GEM catalog](https://datacatalog.worldbank.org/infrastructure-data/search/dataset/0037798/global-economic-monitor) | Public dataset; CC BY 4.0; the official downloadable stock-market workbook contains annual and monthly tabs. | Useful for monthly/annual context; too coarse to identify daily reactions around attacks. “Daily updates” describes the database update cadence, not the frequency of every series. |
| [OECD Share Prices](https://doi.org/10.1787/6ad82f42-en) | National share-price indices; the OECD definition explains that monthly values commonly summarize daily closes. | Useful for monthly trends, not an individual-event daily response. Check country and date coverage in the selected OECD series. |
| [IMF Financial Market Prices](https://data.imf.org/en/Datasets/MFS_FMP) | Country-specific share-price information compiled under national methods; not standardized across countries. | Potential corroboration or monthly robustness; verify the actual frequency and field before relying on it. |

### Official domestic-market candidates

| Country / index | Official source | Access and comparability notes |
|---|---|---|
| United States — S&P 500 | [FRED series SP500](https://fred.stlouisfed.org/series/SP500) | Daily closing values sourced from S&P Dow Jones Indices. FRED's current agreement limits the series to ten years of daily history. It is a price index and excludes dividends. It cannot alone support a 1970–2020 panel. |
| United Kingdom — FTSE 100 | [FTSE 100 at LSE](https://www.londonstockexchange.com/en/indices/ftse-100); [LSE historical-data FAQ](https://www.londonstockexchange.com/en/reports/faqs) | LSE directs historical FTSE index requests to FTSE Russell. Confirm whether a no-cost daily export and the intended public derived outputs are permitted. |
| France — CAC 40 | [Euronext historical index page](https://live.euronext.com/en/product/indices/FR0003500008-XPAR) | Euronext exposes historical-price controls and distinguishes price and total-return index variants; its factsheet says proprietary rights apply. Confirm period limits and reuse terms. Use the price-return variant if matching other price indices. |
| Germany — DAX | [STOXX DAX factsheet/data page](https://stoxx.com/index/dax/?factsheet=true) | The default DAX is a performance index including dividends; a price variant (`DAXPR`) exists. Use the price series for a common price-return design, subject to data access and terms. STOXX states index history is available since 1988. |
| Israel — TA-125 | [TASE Data Services price list](https://www.tase.co.il/en/content/products_lobby/datastore_pricelist) | TASE lists five- and ten-year historical EOD index data as paid products. Verify direct access and data-redistribution terms. TASE trading days differ from most markets, so derive sessions from the downloaded series. |
| Ukraine — UX Index | [Ukrainian Exchange](https://www.ux.ua/en/) | The index is a candidate from 2009 onward, but a stable, free, official historical download and its reuse terms have not yet been verified. Ukraine's wartime closures and market inactivity must be recorded as data availability, not filled with carried-forward prices. Do not classify state military action as GTD terrorism. |
| Saudi Arabia — TASI | [Saudi Exchange index data](https://www.saudiexchange.sa/wps/portal/saudiexchange/trading/market-services/market-information-services/indices-data?locale=en) | Saudi Exchange lists end-of-day data for the past five years. Verify whether a free historical series exists beyond current display data and whether the planned reuse is allowed. |

Official sources improve provenance, but an official webpage or free-to-view quote is not automatically a free bulk-download or redistribution license. Maintain a source-specific record of terms and coverage.

## Current feasibility conclusion

With the user's constraint of public/free sources, **we have not established a complete, freely reusable daily market-price history for all seven countries over the historical GTD period**. The World Bank's public stock-market workbook is monthly/annual; the official daily offerings we checked are either limited to recent years, require a request/license, or remain to be verified. No empirical analysis should begin until a source-by-country coverage table and rights audit are complete.

Next, obtain a sample export or API response from each official provider and record its first/last date, missing sessions, native currency, price-versus-total-return definition, adjustments, and permitted outputs. If the common daily intersection is too short or too small, choose between (a) a narrower daily event study and (b) a monthly, explicitly different research question. Do not silently substitute Yahoo Finance, Investing.com, or another undocumented secondary aggregator for official series.

## Provenance fields to preserve

For every retrieved file or series, record provider and dataset, exact index/event definition, identifier, date/frequency coverage, currency and return type, download date, API query or UI filters, source version, license/terms URL and review date, original filename, SHA-256 digest, and each transformation applied. See [`../data/source_manifest.csv`](../data/source_manifest.csv).

