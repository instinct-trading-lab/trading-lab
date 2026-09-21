# Batch 18 predeclaration: Donchian window ladder on the vol-targeted maker-entry stack

Locked before any batch-18 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any batch-18 code is run. The 2026+ validation window was opened only for batch 17 and is closed again for exploration: batch 18 uses only the 2024-2025 exploration window.

## Question

The batch-16 pt50 exploration pass died in batch-17 validation, which says the specific parameter combination was likely lucky rather than real. Before inventing new rules, batch 18 tests the robustness of the family's central choice: the 55-day entry / 27-day exit window pair. If the family has real structure, neighbouring window pairs on the same stack should show coherent results; if only 55/27 ever looked good, the family itself is suspect.

## Fixed design

- Data, aggregation, exploration window (2024-01-01 through 2025-12-31 UTC), warm-up, and dataset: identical to batches 13-16. SHA-256 recorded per attempt. No new data is fetched.
- Stack: identical to batch 14 at the 35% volatility target (10bp post-only maker entry at 0bp, 5bp exit and resize taker costs, 20-day realized-vol weight w*_t = min(1, 0.35 / vol_t)). No profit-taking or time-exit rules.
- Window pairs (entry, exit): (35, 17), (90, 45), (120, 60). Exit windows are half the entry window, rounded down, matching the 55/27 ratio.
- Nine attempts: three window pairs on each of BTCUSDT, ETHUSDT, SOLUSDT.

## Gates

Identical to batches 14-16:

1. at least 500 observed trading days;
2. annualized Sharpe >= 1.0 using sqrt(365) and the sample standard deviation of daily net returns;
3. positive arithmetic annualized return;
4. maximum drawdown no worse than -25%;
5. PSR versus zero >= 0.95 using the same Bailey-Lopez de Prado skew/kurtosis estimator as batches 4-16;
6. average days per observed day on which the position crosses zero or changes by at least 0.25 of full exposure <= 2.0;
7. an independent second-process rerun matches all committed statistics exactly.

Every attempt, pass or fail, will be reported with dataset and report SHA-256 checksums. A failure does not open validation; a pass earns one predeclared validation attempt.
