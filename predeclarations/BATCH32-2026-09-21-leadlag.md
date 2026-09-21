# Batch 32 predeclaration: cross-asset lead-lag (exploration)

Locked before any batch-32 execution on 2026-09-21 (Asia/Jerusalem). The last untested price-based structure on the lab map: whether one crypto asset's hourly move predicts another's next hour. Data: the already-published batch-19 Binance.US hourly spot files (SHA-256 re-recorded; re-verified byte-identical against the published batch-19 checksums). No new data is fetched.

## Fixed design

- Universe: BTCUSDT, ETHUSDT, SOLUSDT spot, Binance.US hourly bars, exploration window 2024-01-01 through 2025-12-31 UTC (731 days).
- Signal (per attempt): at hour-t UTC close, the LEADER's trailing k-hour return r_k(t) = C_leader(t)/C_leader(t-k) - 1. Position in the FOLLOWER for hour t+1: long 1 unit if r_k(t) > 0, else flat. Long-flat only.
- Pairs (leader -> follower): BTC->ETH, BTC->SOL, ETH->BTC, SOL->BTC, ETH->SOL, SOL->ETH. All six directed pairs, so leadership in either direction is tested symmetrically.
- Lookbacks: k in {1, 4} hours. Fixed a priori.
- Attempts: 6 pairs x 2 lookbacks = 12, named ll{k}-{leader}-{follower} (e.g. ll1-btcusdt-ethusdt).
- Costs: 5bp taker per position change in the follower, charged to the hour of the change.
- Aggregation: hourly position returns compound into daily returns; gates evaluated on the daily series exactly as in batches 6-31 (annualized Sharpe sqrt(365), sample standard deviation; PSR with the same skew/kurtosis estimator).

## Gates (unchanged)

Annualized Sharpe >= 1.0; positive arithmetic annualized return; max drawdown no worse than -25%; PSR >= 0.95; >= 500 observed days; <= 2 position changes per day; byte-exact independent second-process rerun. No rounding up of near-misses.

## Rules

This is exploration. Any pass earns robustness follow-ups, not validation; the 2026+ window stays closed. If this batch produces no pass, the lab's exploration map is exhausted and the lab moves to its final conclusion report. Report files only under reports/dt-batch32-2026-09-21/ with SHA-256 checksums, twin-run verification, and fresh-clone verification.
