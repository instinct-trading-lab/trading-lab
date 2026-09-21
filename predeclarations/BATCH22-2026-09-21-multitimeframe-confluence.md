# Batch 22 predeclaration: multi-timeframe trend confluence

Locked before any batch-22 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any batch-22 code is run. The 2026+ validation window remains closed.

## Question and mechanism

Batch 6's daily-sma50 trend and batch 19's 52-week momentum each reached Sharpe ~0.96 on BTCUSDT alone but failed PSR/drawdown. Both are the same trade at different speeds; their losing days are partly independent whipsaws. The reasoned mechanism for combining them: requiring agreement between a medium (50-day) and slow (52-week) trend filter should remove trades taken against the dominant slow regime, shrinking the left tail that binds PSR, without scanning new parameters - both components are already predeclared winners of their own batches.

## Fixed design

- Data and aggregation: the batch-19 dataset (Binance.US hourly BTCUSDT, ETHUSDT, SOLUSDT, 2022-06-01 through 2025-12-31); SHA-256 recorded per attempt. No new data is fetched.
- Exploration window: 2024-01-01 through 2025-12-31 UTC; earlier data is warm-up only. Validation stays closed.
- Signal: long at close t only when BOTH (a) close_t is strictly above the 50-day simple moving average of closes ending at t, AND (b) close_t is strictly above close_(t-364). Otherwise flat.
- Execution and sizing: identical to batch 19 - weight w_t = min(1, 0.35 / vol_t) when long, 0 when flat; decided at close t, applied to the t to t+1 close-to-close return; 5bp x |w_t - w_(t-1)| charged on the day the change applies; initial entry charged. Long-only, no leverage.
- Three attempts: one on each of BTCUSDT, ETHUSDT, SOLUSDT.

## Gates

Identical to batches 14-21: >= 500 observed days; annualized Sharpe >= 1.0 (sqrt(365), sample standard deviation); positive arithmetic annualized return; max drawdown no worse than -25%; PSR >= 0.95 (same estimator); <= 2.0 qualifying position-change days per day; byte-exact independent rerun.

Every attempt, pass or fail, will be reported with dataset and report SHA-256 checksums. A failure does not open validation; a pass earns exactly one predeclared validation attempt.
