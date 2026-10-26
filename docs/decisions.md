# Research decisions and open questions

## Decisions so far

- Repository audience: public and reproducible.
- Markets requested: Israel, UK, France, Germany, Ukraine, USA, Saudi Arabia.
- Market-data constraint: public/free only (user preference, 2026-10-26).
- Historical event-source candidate: GTD with a strict, documented sample; GTD's 1993 gap and partial 2021 file will be explicit.
- No raw data redistribution unless the source license expressly permits it.
- No results will be reported until source coverage, permissions, and transformations are auditable.
- The candidate primary outcome is absolute volatility-standardized abnormal return around an event; signed return and volatility are separate outcomes.
- No code license has been selected yet.

## Questions for the next design pass

1. Should the main event universe include only attacks physically inside each country, or also attacks abroad that directly target that country's nationals or institutions? The proposed default is events inside the country.
2. Should the headline conclusion focus on one trading session, or short-run effects over several days? The proposed default is `CAR[0,+1]` with a `CAR[0,+5]` persistence check.
3. Are you comfortable defining “impact over time” as the trend in the standardized **magnitude** of abnormal returns, with direction reported separately? This avoids positive and negative events cancelling.
4. What is the preferred public code license (if any)? Data source terms will remain separate and may be more restrictive.

## Gating issue

Find and audit free, officially sourced, daily price-index history with public-output rights. If the seven-country multi-decade panel is unavailable, make the coverage tradeoff explicit and decide whether to narrow countries/years or use monthly data with a different research question.

