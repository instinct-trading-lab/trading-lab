# Batch 29 predeclaration: hourly-scale crypto reversion (exploration)

Locked before any batch-29 execution on 2026-09-21 (Asia/Jerusalem). This is the last unfalsified crypto price-based family. Batch 27 showed hourly momentum at the 24h lookback is strongly NEGATIVE after costs on all three symbols, which implies hourly-scale reversion; this batch tests that implication directly, with fixed design and realistic costs. Data: the already-published batch-19 Binance.US hourly spot files (SHA-256 re-recorded); no new data is fetched.

## Fixed design

- Universe: BTCUSDT, ETHUSDT, SOLUSDT spot, Binance.US hourly bars, exploration window 2024-01-01 through 2025-12-31 UTC (731 days).
- Signal (per attempt): at hour-t UTC close, trailing k-hour return r_k(t) = C(t)/C(t-k) - 1. Position for hour t+1: long 1 unit if r_k(t) < 0, else flat. Reversion, long-flat only (no shorts: Binance.US spot cannot short; mixing in the perp leg would confound the family with basis, which batch 24-26 already covered).
- Lookbacks: k in {1, 4, 8, 24} hours. Fixed a priori.
- Attempts: 4 lookbacks x 3 symbols = 12 attempts, named hrrev{k}-{symbol}.
- Costs: 5bp taker per position change, charged to the hour of the change.
- Aggregation: hourly position returns compound into daily returns; gates evaluated on the daily series exactly as in batches 6-28 (annualized Sharpe sqrt(365), sample standard deviation; PSR with the same skew/kurtosis estimator).

## Gates (unchanged)

Annualized Sharpe >= 1.0; positive arithmetic annualized return; max drawdown no worse than -25%; PSR >= 0.95; >= 500 observed days; <= 2 position changes per day; byte-exact independent second-process rerun. No rounding up of near-misses. The <= 2 events/day gate is expected to bind hard at short lookbacks - that is the honest turnover test, not a technicality.

## Rules

This is exploration. Any pass earns robustness follow-ups, not validation; the 2026+ window stays closed. Report files only under reports/dt-batch29-2026-09-21/ with SHA-256 checksums, twin-run verification, and fresh-clone verification.
