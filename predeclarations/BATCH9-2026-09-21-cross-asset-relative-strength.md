# Batch 9 predeclaration: daily cross-asset relative-strength rotation

Locked before any batch-9 data execution on 2026-09-21 (Asia/Jerusalem). This file must be committed to the remote repository before batch-9 data is fetched or inspected. The 2026+ validation window remains closed.

## Question

Batches 6-8 found a promising but non-passing absolute-trend family. Batch 9 changes the economic family rather than tuning that lead: can cross-sectional relative strength among BTC, ETH and SOL produce a cost-aware portfolio that clears the lab gates in the 2024-2025 exploration window?

## Fixed design

- Public market data: Binance.US hourly BTCUSDT, ETHUSDT and SOLUSDT candles, aggregated to UTC daily closes.
- Exploration window: 2024-01-01 through 2025-12-31 UTC. Sufficient prior data may be fetched only to warm up lookbacks.
- Untouched validation window: 2026-01-01 onward. It stays closed unless an exploration attempt clears every gate.
- Six portfolio-level attempts: trailing-close relative-strength lookbacks of 7, 14 and 30 calendar days, each selecting either the strongest one asset (`top1`) or strongest two assets (`top2`).
- At each UTC daily close t, score each asset by `close_t / close_(t-lookback) - 1`. At t+1 hold equal weights across the selected asset(s). No cash filter: the strategy is always fully invested after warm-up. Ties break alphabetically by symbol.
- Cost: 5bp per unit of absolute portfolio-weight change, charged on the day the new weights apply. A full switch from one asset to another therefore costs 10bp. Initial entry is charged.
- Accounting: decisions use only closed daily bars; weights chosen at t apply to close-to-close returns from t to t+1. Long-only, no leverage. Daily portfolio returns compound.
- Missing-data rule: evaluate only dates for which all three assets have a close and a valid lookback close. No forward filling.

## Gates

An exploration attempt passes only if all are true:

1. at least 500 observed portfolio days;
2. annualized Sharpe >= 1.0, using sqrt(365) and sample standard deviation of daily net returns;
3. positive arithmetic annualized return;
4. maximum drawdown no worse than -25%;
5. probabilistic Sharpe ratio versus zero >= 0.95, using the same Bailey-Lopez de Prado skew/kurtosis estimator used in batches 4-8;
6. average portfolio rebalances with any weight change <= 2.0 per day;
7. an independent second-process rerun matches all committed statistics exactly.

Every attempt, pass or fail, will be reported. Dataset and report SHA-256 checksums will be recorded. A passing exploration attempt may open one predeclared validation attempt later; this predeclaration itself does not open validation.
