# Terrorism and Domestic Stock-Market Responses

An open, evidence-first study of how terrorist attacks are associated with short-run reactions in domestic equity markets, and whether those reactions change over time.

**Status: research protocol and data-source feasibility review. No results have been calculated.**

## Research question

Across Israel, the United Kingdom, France, Germany, Ukraine, the United States, and Saudi Arabia, do domestic stock markets show smaller or larger abnormal price responses to terrorist attacks over time?

The intended primary outcome is the magnitude of a market's abnormal return around an attack, adjusted for its ordinary volatility. Signed returns and short-run volatility changes will be reported separately. “Impact” here means a short-run market-price response; it does not mean the attack caused later national economic outcomes.

## What the initial evidence says about data feasibility

- The [Global Terrorism Database (GTD)](https://www.start.umd.edu/download-global-terrorism-database) is the best starting point for a consistent historical event definition. Its current full file covers 1970–2020, has a known 1993 data gap, and may not be republished. A separate partial file covers January–June 2021.
- The [World Bank Global Economic Monitor (GEM)](https://datacatalog.worldbank.org/infrastructure-data/search/dataset/0037798/global-economic-monitor) is public and CC BY 4.0. Its downloadable “Stock Markets” workbook has annual and monthly sheets, not daily prices, so it cannot identify trading-day reactions to individual attacks.
- Official daily index history is fragmented across providers. Some sites expose recent values, while long historical exports or redistribution rights may require a license. **We have not yet found a complete, openly licensed, daily panel spanning all seven markets and decades.**
- [ACLED](https://acleddata.com/acled-api-documentation) is frequently updated and offers an API, but its event taxonomy differs from GTD and its terms restrict raw-data sharing. It will not be silently spliced into the historical GTD series.

For now, this repository records the evidence, source limitations, and a pre-analysis design. It will not publish fabricated or provisional findings. See [the source review](docs/data-sources.md) and [research design](docs/research-design.md).

## Countries and benchmark candidates

| Country | ISO3 | Candidate domestic benchmark |
|---|---:|---|
| Israel | ISR | TA-125 (price index) |
| United Kingdom | GBR | FTSE 100 (price index) |
| France | FRA | CAC 40 (price index) |
| Germany | DEU | DAX price index (DAXPR, not the dividend-inclusive DAX performance index) |
| Ukraine | UKR | Ukrainian Equities / UX Index |
| United States | USA | S&P 500 (price index) |
| Saudi Arabia | SAU | Tadawul All Share Index (TASI) |

These are candidates, not confirmed data inputs. Each selected series must pass a coverage, frequency, definition, timestamp, and reuse-rights audit before analysis. The full source register is in [`data/source_manifest.csv`](data/source_manifest.csv).

## Proposed method

1. Define domestic attacks by the country where the event occurred, using a pre-registered GTD inclusion rule.
2. Compute close-to-close local-currency returns from one consistently defined price-index series per market.
3. Estimate expected returns with a market model and calculate abnormal returns and cumulative abnormal returns (CARs) in short trading-session windows.
4. Compare both signed CAR and absolute volatility-standardized CAR across years, controlling for event severity, attack type, country, and background market volatility.
5. Account for overlapping events, simultaneous global shocks, cross-country event-date clustering, missing data, and exchanges that are closed or suspended.
6. Publish source versions, retrieval dates, transformation choices, code, and derived outputs. Raw files will only be included when the source terms explicitly permit redistribution.

The full protocol and sensitivity analyses are in [research-design.md](docs/research-design.md). An event study supports statements about market reactions around recorded events; by itself it does not establish a causal effect.

## Reproducibility and data policy

This repository is public. **No licensed raw event or market data are included.** Obtain each source directly, read its current terms, and record the exact version and SHA-256 digest in the source manifest. Keep local-only copies under `data/raw/`; that folder is ignored by Git. Put only permitted, documented derived outputs in `data/processed/` or `data/derived/`.

The code environment and analysis pipeline will be pinned and documented when the feasible daily-market source set is confirmed. The project currently has no declared code license; public visibility does not itself grant permission to reuse code or data.

## Planned repository map

- `docs/data-sources.md` — event and market source review, access constraints, and current feasibility decision.
- `docs/research-design.md` — definitions, estimands, event-study plan, trend model, robustness checks, and limitations.
- `docs/data-dictionary.md` — normalized event and market-data fields.
- `docs/tooling.md` — tools used for the feasibility review and the planned analysis environment.
- `docs/decisions.md` — choices made and questions still open.
- `data/source_manifest.csv` — per-series provenance, coverage, frequency, license, and checksum register.
- `data/raw/README.md` — rules for source files kept locally.
- `data/processed/README.md`, `data/derived/README.md` — rules for derived outputs.

## Reference methods

- MacKinlay, A. C. (1997). [Event Studies in Economics and Finance](https://doi.org/10.1257/jel.35.1.13). *Journal of Economic Literature*, 35(1), 13–39.
- Kolari, J. W., & Pynnönen, S. (2010). [Event Study Testing with Cross-sectional Correlation of Abnormal Returns](https://doi.org/10.1093/rfs/hhq072). *The Review of Financial Studies*, 23(11), 3996–4025.

## Next research decision

The daily market-data audit is the gating step. If no defensible free daily series covers the requested countries and period, the study will either narrow its country/time coverage or change to a monthly question; it will not use an undocumented price aggregator as if it were official data. See [open decisions](docs/decisions.md).

