# Batch 16 predeclaration: exit-rule variants on the vol-targeted Donchian maker stack

Locked before any batch-16 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any batch-16 code is run. The 2026+ validation window remains closed.

## Question

Batches 14-15 exhausted position sizing: PSR on the BTCUSDT package peaks near a 35% volatility target at 0.9394, below the 0.95 gate, while Sharpe, return and drawdown all pass. PSR is set by the shape of the daily return distribution, not by exposure size. Batch 16 asks whether predeclared exit rules that reshape that distribution - partial profit-taking or a maximum holding time - lift PSR over the gate without breaking the others.

## Fixed design

- Data, aggregation, exploration window, warm-up, and the closed 2026+ validation window: identical to batches 13-15. The batch 9-13 dataset is reused; SHA-256 recorded per attempt. No new data is fetched.
- Base stack: identical to batch 14 at the 35% volatility target (55-day Donchian entry, 27-day exit, 10bp post-only maker entry at 0bp, 5bp exit and resize taker costs, 20-day realized-vol weight w*_t = min(1, 0.35 / vol_t)).
- Variant A (partial profit-taking): once per entry, when the close first reaches at least +50% above the fill price, sell half the current weight at that close (5bp taker on the sold weight, charged that day). The remainder follows the base rules.
- Variant B (time-exit): when a position has been held for 60 complete trading days since the fill day, exit the full weight at that close (5bp taker), independent of the 27-day exit.
- Six attempts: variants A and B on each of BTCUSDT, ETHUSDT, SOLUSDT.

## Gates

Identical to batches 14-15:

1. at least 500 observed trading days;
2. annualized Sharpe >= 1.0 using sqrt(365) and the sample standard deviation of daily net returns;
3. positive arithmetic annualized return;
4. maximum drawdown no worse than -25%;
5. PSR versus zero >= 0.95 using the same Bailey-Lopez de Prado skew/kurtosis estimator as batches 4-15;
6. average days per observed day on which the position crosses zero or changes by at least 0.25 of full exposure <= 2.0;
7. an independent second-process rerun matches all committed statistics exactly.

Every attempt, pass or fail, will be reported with dataset and report SHA-256 checksums. A failure does not open validation.
