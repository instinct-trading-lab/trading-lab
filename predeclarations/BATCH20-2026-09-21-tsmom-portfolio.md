# Batch 20 predeclaration: time-series momentum portfolio (diversification test)

Locked before any batch-20 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any batch-20 code is run. The 2026+ validation window remains closed.

## Question and mechanism

Batch 19 found each single-asset slow-momentum leg just under the gates on BTCUSDT and failing elsewhere. The reasoned next step is diversification, not another parameter: momentum signals across imperfectly correlated assets diversify idiosyncratic noise, so an equal-weight basket can clear Sharpe/PSR gates even when no leg does alone. Unlike batch 9's rotation (concentrated bets on the strongest asset), the basket holds every leg independently long-or-flat at one-third weight.

## Fixed design

- Data and aggregation: the batch-19 dataset (Binance.US hourly BTCUSDT, ETHUSDT, SOLUSDT, 2022-06-01 through 2025-12-31); SHA-256 recorded per attempt. No new data is fetched.
- Exploration window: 2024-01-01 through 2025-12-31 UTC; earlier data is warm-up only. Validation stays closed.
- Each leg: identical to batch 19 - long when close_t is strictly greater than close_(t-L), flat otherwise; leg weight w_leg,t = min(1, 0.35 / vol_leg,t); 5bp per unit of leg-weight change, charged on the day the change applies; initial entry charged.
- Portfolio: daily return is the simple average of the three leg daily net returns (one-third capital per leg, no rebalancing beyond each leg's own rule).
- Two attempts: L = 182 and L = 364.

## Gates

Identical to batches 14-19, computed on portfolio daily net returns: >= 500 observed days; annualized Sharpe >= 1.0; positive arithmetic annualized return; max drawdown no worse than -25%; PSR >= 0.95 (same estimator); <= 2.0 qualifying position-change days per day averaged across legs; byte-exact independent rerun.

Every attempt, pass or fail, will be reported with dataset and report SHA-256 checksums. A failure does not open validation; a pass earns exactly one predeclared validation attempt.
