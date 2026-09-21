# Batch 27 predeclaration: hourly-horizon time-series momentum (exploration)

Locked before any batch-27 execution on 2026-09-21 (Asia/Jerusalem). Open direction #3 in LAB-SYNTHESIS.md: hourly crypto families are untested at scale (15-minute reversion is falsified; daily/4h trend is falsified; the hourly horizon is open). This batch tests hourly time-series momentum only - no reversion, no other family, no tuning after execution.

## Fixed design

- Universe: BTCUSDT, ETHUSDT, SOLUSDT spot, Binance.US hourly bars, exploration window 2024-01-01 through 2025-12-31 UTC (731 days). Data: the already-published batch-19 dataset files (SHA-256 re-recorded in the attempt files).
- Signal (per attempt): at hour-t UTC close, compute the trailing k-hour close-to-close return r_k(t) = C(t)/C(t-k) - 1. Position for hour t+1: long 1 unit if r_k(t) > 0, else flat (0). Long-flat only; no shorts, no leverage.
- Lookbacks: k in {24, 72, 168} hours (1 day, 3 days, 7 days). Fixed a priori.
- Attempts: 3 lookbacks x 3 symbols = 9 attempts, named hrmom{k}-{symbol}.
- Costs: 5bp taker per position change (0-to-1 or 1-to-0), charged to the hour of the change.
- Aggregation: hourly position returns compound into daily returns; all gates are evaluated on the daily series exactly as in batches 6-25 (annualized Sharpe with sqrt(365), sample standard deviation; PSR with the same skew/kurtosis estimator).

## Gates (unchanged)

Annualized Sharpe >= 1.0; positive arithmetic annualized return; max drawdown no worse than -25%; PSR >= 0.95; >= 500 observed days; <= 2 qualifying position events per day (an event = a position change); byte-exact independent second-process rerun. No rounding up of near-misses. An attempt passes only if every gate holds.

## Rules

This is exploration. Any pass earns robustness follow-ups, not validation: the 2026+ window stays closed. A pass from this batch plus its robustness batch earns exactly one predeclared validation attempt, as with batch 24/25. All report files (no raw data, no strategy code) are published under reports/dt-batch27-2026-09-21/ with SHA-256 checksums, twin-run verification, and fresh-clone verification.
