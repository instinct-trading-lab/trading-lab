# Batch 28 predeclaration: non-crypto daily time-series momentum (exploration)

Locked before any batch-28 full-history data fetch or execution on 2026-09-21 (Asia/Jerusalem). Open direction #1 in LAB-SYNTHESIS.md: non-crypto universes at the daily horizon. Crypto price-based momentum/reversion is falsified at 15m, hourly, 4h, daily, and weekly horizons; this batch tests whether daily TSMOM exists in equity-index, FX, and commodity price series from a public macro source.

## Source and universe (fixed a priori)

Source: FRED (Federal Reserve Bank of St. Louis) public CSV downloads (fred.stlouisfed.org/graph/fredgraph.csv). Series: SP500, NASDAQCOM, DJIA (equity indexes); DEXUSEU, DEXJPUS, DEXUSUK (FX); DCOILWTICO (WTI crude); DTWEXBGS (broad dollar index). 8 series. Each series trades on its own publication calendar; rows with missing values ('.') are dropped. Any series whose history does not fully cover the warm-up plus window is reported as untestable, not as a pass or fail.

Disclosure: before this predeclaration, connectivity probes fetched the full history of SP500 and DEXUSEU (tails spot-checked, no analysis) and date-bounded 2019-Q1 samples of the other six series. No 2026-or-later value of any series was used in designing this batch; no return, signal, or gate computation was run on any of it. The full-history fetch for all 8 series happens only after this commit.

## Fixed design

- Signal (per attempt): at day-t close, trailing k-day close-to-close return r_k(t) = C(t)/C(t-k) - 1. Position for the next published day: long 1 unit if r_k(t) > 0, else flat. Long-flat only; no shorts, no leverage. For FX series, "long" means long the series as quoted.
- Lookbacks: k in {126, 252} published days (~6 and ~12 months). Fixed a priori.
- Attempts: 8 series x 2 lookbacks = 16 attempts, named tsmom{k}-{series lowercase}.
- Costs: 10bp per position change (0-to-1 or 1-to-0), charged to the day of the change.
- Window: 2018-01-01 through 2025-12-31 per each series' own calendar. Warm-up data from each series' full history (FRED SP500 begins 2016-09-19, giving >= 252 published days of warm-up before 2018). No 2026-or-later row is read by the engine: it slices strictly <= 2025-12-31. The 2026+ validation window stays closed.

## Gates (unchanged)

Evaluated on the daily return series: annualized Sharpe >= 1.0 (sqrt(252), sample standard deviation - non-crypto daily uses the 252 trading-day convention, stated a priori); positive arithmetic annualized return; max drawdown no worse than -25%; PSR >= 0.95 (same skew/kurtosis estimator); >= 500 observed days; <= 2 position changes per day; byte-exact independent second-process rerun. No rounding up of near-misses. An attempt passes only if every gate holds.

## Rules

This is exploration. A pass earns robustness follow-ups, not validation; a pass plus its robustness batch earns exactly one predeclared validation attempt on 2026+ data. Report files only (no raw data, no strategy code) under reports/dt-batch28-2026-09-21/ with SHA-256 checksums, twin-run verification, and fresh-clone verification.
