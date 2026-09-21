# Batch 21 predeclaration: long-short time-series momentum (short-side falsification)

Locked before any batch-21 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any batch-21 code is run. The 2026+ validation window remains closed.

## Question and mechanism

Every lab batch so far is long-only, and the consistent failure mode is the left tail: PSR and drawdown bind while long-only structures ride full crypto downtrends. Batch 21 asks the symmetric question: does the short side of the batch-19 momentum signal add anything at all? This is a falsification test with deliberately free shorts: no borrow or funding cost is modeled. If long-short fails even with free shorts, the direction is dead. If it passes, a follow-up batch must add realistic funding costs before any validation.

## Fixed design

- Data and aggregation: the batch-19 dataset (Binance.US hourly BTCUSDT, ETHUSDT, SOLUSDT, 2022-06-01 through 2025-12-31); SHA-256 recorded per attempt. No new data is fetched.
- Exploration window: 2024-01-01 through 2025-12-31 UTC; earlier data is warm-up only. Validation stays closed.
- Signal: at UTC daily close t, sign = +1 when close_t is strictly greater than close_(t-L), -1 when strictly less, 0 when equal; L in {182, 364}.
- Execution and sizing: weight w_t = sign x min(1, 0.35 / vol_t), decided at close t, applied to the close-to-close return from t to t+1; vol_t is the 20-day annualized realized volatility. Cost: 5bp x |w_t - w_(t-1)|, charged on the day the change applies; initial entry charged. No borrow, funding, or short-rebate is modeled (see Question).
- Six attempts: two lookbacks on each of BTCUSDT, ETHUSDT, SOLUSDT.

## Gates

Identical to batches 14-20: >= 500 observed days; annualized Sharpe >= 1.0 (sqrt(365), sample standard deviation); positive arithmetic annualized return; max drawdown no worse than -25%; PSR >= 0.95 (same estimator); <= 2.0 qualifying position-change days per day; byte-exact independent rerun.

Every attempt, pass or fail, will be reported with dataset and report SHA-256 checksums. A pass here does NOT earn validation directly; it earns one follow-up exploration batch with funding costs modeled, which is the batch that can earn validation.
