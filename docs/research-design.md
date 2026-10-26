# Proposed research design

**Status:** pre-analysis plan draft. No data have been merged and no results have been calculated. Finalize this protocol after verifying a lawful, usable daily index panel.

## 1. Research questions

1. What is the short-run domestic equity-market response to recorded terrorist attacks?
2. Does the **magnitude** of that response become smaller or larger over calendar time?
3. Does any trend persist after accounting for attack severity/type, country, local market volatility, and the composition of observed events?

Report direction and magnitude separately. A mean signed return can move toward zero because responses are becoming smaller, because negative and positive responses cancel, or because event composition changes. The primary trend outcome should therefore be the absolute cumulative standardized abnormal return; signed CAR and volatility are secondary outcomes.

## 2. Event population and unit of analysis

- Countries: Israel, UK, France, Germany, Ukraine, USA, and Saudi Arabia (ISO3: ISR, GBR, FRA, DEU, UKR, USA, SAU).
- Primary historical event source: one dated GTD release. Main sample: the event occurred within the country whose index is studied and satisfies all three GTD inclusion criteria with `doubtterr=0`. Keep a sensitivity sample using a documented alternative rule.
- Do not infer terrorism from a news headline or from casualties alone. Preserve GTD's incident identifier and uncertainty fields.
- Treat an event as domestic by location, not perpetrator nationality. Add separate flags for capital-city events, suicide attacks, attack type, and log fatalities/injuries only where the values are known and the codebook supports that interpretation.
- GTD's 1993 incident-level gap is missing coverage, not zero attacks. Exclude 1993 from event-level rate comparisons and disclose it in all historical plots. GTD's partial 2021 file is not a complete year. No homogeneous GTD trend extends past 2020.
- Define the primary unit as one market-event pair. For multiple qualifying events in one country on the same date, retain event-level records but cluster inference by country-date and run an aggregate country-date sensitivity analysis. Flag overlapping event windows.

## 3. Market sample and alignment

- Use one broad domestic equity index per country, in local currency, and choose the same type of return (prefer price-return indices for the primary price-response design). Do not mix a dividend-inclusive performance index such as the headline DAX with price-only indices.
- Daily observation: official index closing level and date. Build trading sessions from the observed series; do not generate weekend or holiday prices.
- Main return: `r[t] = 100 * (ln(close[t]) - ln(close[t-1]))`. Retain source levels, currency, index identifier, and missing/suspended-session flags.
- GTD provides an event date but not a consistently reliable event time. Main `t=0` is the first observed local market session on or after the reported event date. Sensitivities: first session strictly after the event date and windows shifted by one session. This makes the timing assumption visible but cannot remove within-day misclassification.
- Mark exchanges closed or suspended at/after an attack. A closure is potentially part of the market response, not a zero return. Report such cases and analyze available pre-closure/post-reopening returns separately.
- The primary sample is the intersection of observed daily market coverage and complete event-source coverage, not a pre-imposed 1970–2020 claim for all markets. Report country-specific start/end dates and event counts before estimating effects.

## 4. Primary event study

For each market, estimate a market model in an estimation window ending well before the event, provisionally sessions `[-250, -31]`:

`r[c,t] = alpha[c,e] + beta[c,e] * r[benchmark,t] + error[c,t]`

The benchmark should be one consistently sourced broad global or regional equity index, not the domestic index itself. If a lawful daily benchmark cannot be obtained for all countries, disclose a local-mean-adjusted alternative and its weaker control for global shocks. Freeze the estimation-window and benchmark rule before inspecting event results.

Then calculate abnormal returns `AR = observed return - predicted return` and cumulative abnormal returns. Pre-specify `CAR[0,+1]` as the main window, `CAR[0,+5]` as a recovery/persistence window, and `CAR[-1,+1]` as a timing sensitivity. Avoid interpreting many overlapping window tests as independent evidence.

Standardize CAR using pre-event residual volatility estimated outside the event window. Report:

- signed CAR in percent (direction and economic size);
- absolute standardized CAR (primary measure of response magnitude);
- event-window realized volatility relative to a pre-event baseline (secondary outcome).

## 5. Testing whether impact changes over time

Primary model: regress absolute standardized CAR on event year (continuous linear trend), country fixed effects, log fatalities and injuries where known, attack-type indicators, and pre-event market volatility. Use robust inference that accounts for repeated events, same-date cross-country clustering, and overlapping event windows; compare event-date-clustered errors with a country/block bootstrap. Show country-specific slopes and pooled results. Use pre-specified decade groups as a descriptive robustness check, not as a search for the most favorable split.

Secondary models use signed CAR and volatility response. Address sparse events and heavy-tailed CARs with robust/quantile or permutation-based inference as appropriate. Adjust for multiple testing across secondary outcomes and event windows. Publish counts and uncertainty intervals even when estimates are not statistically significant.

This is a within-event association design. Market-model residuals do not remove every contemporaneous political, military, macroeconomic, or global shock. Avoid causal language unless a later design identifies a credible counterfactual.

## 6. Bias checks and sensitivity analyses

- Alternative GTD inclusion rules and explicit treatment of `doubtterr` cases.
- Exclude events with unknown date precision or uncertain country coding; compare event-level and country-date aggregates.
- Severity alternatives: fatalities, injuries, any casualty, suicide attack, attack type, capital-city indicator; never recode unknown as zero.
- Alternative event-day alignment and windows, especially where the market is closed on the reported date.
- Exclude events with overlapping estimation/event windows; then include them with country-date aggregation.
- Market benchmark alternatives, price versus total-return series if available, and raw-return versus volatility-standardized effects.
- Matched non-event trading sessions or date-block permutations to test whether observed CARs are unusual relative to the same market's ordinary volatility regime.
- Leave-one-country-out and leave-one-major-event-out analyses.
- Document market closures, suspensions, index methodology changes, currency/inflation episodes, and coverage breaks.

## 7. Interpretation limits

- Terrorism has no universal definition. GTD is an operational, non-state event dataset; it is not a complete record of all political violence or every attack that a government or news outlet labels terrorism.
- Reporting and coding intensity vary over time and geography. Apparent attenuation could reflect changing event selection, missing reports, or market-data coverage.
- Index composition, market depth, market opening hours, trading days, and index methodologies differ across countries and decades.
- Daily event dates without attack timestamps blur event-day versus next-session response. Daily closes cannot identify intraday effects.
- Ukraine's wartime disruption and exchange closures are structurally different from ordinary terrorism shocks. State military violence is outside the GTD main definition and must not be relabeled as terrorism.
- A short-run index reaction is not a measure of human harm, long-run economic damage, or investment advice.

## 8. Reporting checklist

Before any findings are published, include (1) exact source versions and licenses, (2) country/date coverage and missingness, (3) the event inclusion code, (4) full transformation and analysis code, (5) environment lock file and commands, (6) counts by country/year, (7) primary outcomes and uncertainty intervals, (8) all stated sensitivities, and (9) a no-causal-claim explanation where appropriate.

