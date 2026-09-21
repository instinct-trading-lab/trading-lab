# Batch 19 predeclaration: slow time-series momentum (new family)

Locked before any batch-19 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any batch-19 data is fetched or code is run. The 2026+ validation window remains closed.

## Question and mechanism

Three families are dead: 15-minute reversion (batches 3-5), rotation (9, 11), and daily Donchian trend (12-18: window-and-asset-specific luck, validation kill). Batch 19 tests a different, externally anchored family: slow time-series momentum. The mechanism is the published cross-asset anomaly that an asset whose trailing 6-12 month return is positive tends to keep rising (Moskowitz, Ooi and Pedersen, "Time Series Momentum", 2012). The lookbacks are fixed at 26 and 52 weeks by that literature, not scanned on our data, and the monthly-scale signal cannot churn the way the dead families did.

## Fixed design

- Data: public Binance.US hourly BTCUSDT, ETHUSDT and SOLUSDT candles, 2022-06-01 through 2025-12-31, fetched fresh after this commit; SHA-256 recorded per attempt. Aggregation to complete UTC daily OHLC bars; a day requires all 24 hourly records. No forward fill.
- Exploration window: 2024-01-01 through 2025-12-31 UTC; earlier data is warm-up only. Validation (2026-01-01 onward) stays closed.
- Signal: at UTC daily close t, long when close_t is strictly greater than close_(t-L), flat otherwise; L in {182, 364} days.
- Execution and sizing: the weight decided at close t applies to the close-to-close return from t to t+1. Weight w_t = min(1, 0.35 / vol_t) when long, 0 when flat, where vol_t is the annualized standard deviation of daily log returns over the trailing 20 complete days ending at t (x sqrt(365)). Cost: 5bp x |w_t - w_(t-1)|, charged on the day the new weight applies; the initial entry is charged. Long-only, no leverage.
- Six attempts: two lookbacks on each of BTCUSDT, ETHUSDT, SOLUSDT.

## Gates

1. at least 500 observed trading days;
2. annualized Sharpe >= 1.0 using sqrt(365) and the sample standard deviation of daily net returns;
3. positive arithmetic annualized return;
4. maximum drawdown no worse than -25%;
5. PSR versus zero >= 0.95 using the same Bailey-Lopez de Prado skew/kurtosis estimator as batches 4-18;
6. average days per observed day on which the position crosses zero or changes by at least 0.25 of full exposure <= 2.0;
7. an independent second-process rerun matches all committed statistics exactly.

Every attempt, pass or fail, will be reported with dataset and report SHA-256 checksums. A failure does not open validation; a pass earns exactly one predeclared validation attempt.
