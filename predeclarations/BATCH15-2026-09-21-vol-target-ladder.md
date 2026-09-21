# Batch 15 predeclaration: volatility-target ladder on the Donchian maker-entry stack

Locked before any batch-15 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any batch-15 code is run. The 2026+ validation window remains closed.

## Question

Batch 14 showed volatility targeting monotonically improved the BTCUSDT Donchian55-maker package as the target fell from 50% to 35%: Sharpe 1.000 -> 1.065, PSR 0.9259 -> 0.9394, drawdown -22.08% -> -17.95%. PSR versus zero is now the only binding gate (miss 0.0106 at 35%). Batch 15 asks whether the trend continues across a finer target ladder - 45%, 40%, 30%, 25% annualized - and whether any rung clears every gate.

## Fixed design

- Data, aggregation, exploration window, warm-up, and the closed 2026+ validation window: identical to batches 13-14. The batch 9-13 dataset is reused; SHA-256 recorded per attempt. No new data is fetched.
- Signal, execution, sizing rule, and cost model: identical to batch 14 (55-day Donchian entry, 27-day exit, 10bp post-only maker entry at 0bp, 5bp exit and resize taker costs, 20-day realized-vol target weight w*_t = min(1, TARGET / vol_t), resize charged on the deciding day's return).
- Twelve attempts: TARGET in {45%, 40%, 30%, 25%} on each of BTCUSDT, ETHUSDT, SOLUSDT.

## Gates

Identical to batch 14:

1. at least 500 observed trading days;
2. annualized Sharpe >= 1.0 using sqrt(365) and the sample standard deviation of daily net returns;
3. positive arithmetic annualized return;
4. maximum drawdown no worse than -25%;
5. PSR versus zero >= 0.95 using the same Bailey-Lopez de Prado skew/kurtosis estimator as batches 4-14;
6. average days per observed day on which the position crosses zero or changes by at least 0.25 of full exposure <= 2.0;
7. an independent second-process rerun matches all committed statistics exactly.

Every attempt, pass or fail, will be reported with dataset and report SHA-256 checksums. A failure does not open validation.
