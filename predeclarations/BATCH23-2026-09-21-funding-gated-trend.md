# Batch 23 predeclaration: funding-gated slow trend (non-price regime signal)

Locked before any batch-23 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any funding-rate data is fetched or any batch-23 code is run. The 2026+ validation window remains closed.

## Question and mechanism

Ten price-only families are mapped; PSR binds near 0.94-0.95. Batch 23 adds the first non-price signal: perpetual-swap funding as a crowding gauge. The mechanism: funding is paid every 8 hours between perp longs and shorts; a persistently high positive rate means crowded longs paying to stay long, a regime prone to long-side flushes. The hypothesis is NOT that funding predicts direction, but that filtering out crowded-long regimes removes part of the left tail that binds PSR on the batch-19 slow-trend package.

## Cross-venue construction (explicit)

Funding history comes from Binance.com USD-M perpetual public data; price bars remain Binance.US spot hourly. The venues differ; funding is used only as a regime gauge (a slow moving average of a rate), never as a tradable price, and all timestamps are aligned to UTC days. This construction is predeclared here so it cannot be retrofitted.

## Fixed design

- Price data: the batch-19 dataset (Binance.US hourly BTCUSDT, ETHUSDT, SOLUSDT, 2022-06-01 through 2025-12-31); SHA-256 recorded. Funding data: Binance.com public funding-rate history for the same symbols, 2023-09-01 through 2025-12-31, fetched fresh after this commit; SHA-256 recorded per symbol.
- Funding aggregation: for UTC day t, the daily funding mean is the average of all funding records with fundingTime inside t. A trailing 7-day funding mean f_t uses days t-6 through t. If fewer than 15 funding records exist in those 7 days (about 21 expected), the funding gate fails (flat). No forward fill.
- Signal: long at close t only when BOTH (a) close_t is strictly greater than close_(t-364) (the batch-19 52-week momentum rule), AND (b) f_t <= 0.0005 (0.05% per 8 hours). The threshold is fixed a priori at five times the standard 0.01% baseline funding interval; it is not scanned.
- Execution, sizing, and costs: identical to batch 19 - weight w_t = min(1, 0.35 / vol_t) when long, 0 when flat; decided at close t, applied to the t to t+1 close-to-close return; 5bp x |w_t - w_(t-1)| charged on the day the change applies; initial entry charged. Long-only, no leverage.
- Exploration window: 2024-01-01 through 2025-12-31 UTC; earlier data is warm-up only. Three attempts: one per symbol.

## Gates

Identical to batches 14-22: >= 500 observed days; annualized Sharpe >= 1.0 (sqrt(365), sample standard deviation); positive arithmetic annualized return; max drawdown no worse than -25%; PSR >= 0.95 (same estimator); <= 2.0 qualifying position-change days per day; byte-exact independent rerun.

Every attempt, pass or fail, will be reported with dataset and report SHA-256 checksums. A failure does not open validation; a pass earns exactly one predeclared validation attempt. If funding data cannot be fetched or joined honestly, this batch reports the blockage instead of forcing a result.
