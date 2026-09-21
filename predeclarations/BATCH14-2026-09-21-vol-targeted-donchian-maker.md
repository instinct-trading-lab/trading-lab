# Batch 14 predeclaration: volatility-targeted Donchian breakout with maker entry

Locked before any batch-14 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any batch-14 code is run. The 2026+ validation window remains closed.

## Question

Batch 13's 55-day Donchian breakout with 10bp fill-aware maker entry on BTCUSDT ended one gate away: Sharpe 0.988 versus 1.0 and PSR 0.922 versus 0.95, with drawdown already inside the gate (-23.10%). Batch 8 showed volatility-targeted fractional sizing is the one lever so far that improved a trend family's Sharpe and drawdown together (daily-sma50 BTCUSDT: Sharpe 1.136, drawdown -24.14%). Batch 14 asks whether that sizing, applied to the batch-13 signal and execution stack without changing the signal, clears every gate.

## Fixed design

- Data: the batch 9-13 dataset (public Binance.US hourly BTCUSDT, ETHUSDT, SOLUSDT candles, 2023-11-01 through 2025-12-31, SHA-256 recorded per attempt). No new data is fetched.
- Aggregation: complete UTC daily OHLC bars; a day requires all 24 hourly records. No forward fill.
- Exploration window: 2024-01-01 through 2025-12-31 UTC; earlier data is warm-up only. Validation (2026-01-01 onward) stays closed.
- Signal and execution, identical to batch 13: after close t, when flat and close_t is strictly above the maximum high of the preceding 55 complete days excluding t, place a one-day post-only buy limit at close_t x (1 - 10bp). It fills during t+1 only if low_(t+1) <= limit; a fill earns close_(t+1)/limit - 1 per unit that day. An unfilled order is cancelled after t+1 close; a fresh order is placed only if t+1 itself remains a valid breakout. Once long, exit at close t when close_t is strictly below the minimum low of the preceding 27 complete days excluding t; the return through that close is earned.
- Sizing (new, replacing the binary position): vol_t is the annualized standard deviation of daily log close-to-close returns over the trailing 20 complete days ending at t (x sqrt(365)). Target weight w*_t = min(1, TARGET / vol_t). A maker fill at signal close t establishes weight w*_t. While held, the weight decided at each close d for day d+1 is w_d = min(1, TARGET / vol_d).
- Costs: entry fill fee 0bp (maker). Exit fee 5bp x weight, charged on the exit day's return. Resizing decided at close d costs 5bp x |w_d - w_(d-1)|, charged on day d's return. Long-only, no leverage, no shorts, no credit before fill.
- Six attempts: TARGET in {50%, 35%} on each of BTCUSDT, ETHUSDT, SOLUSDT.

## Gates

An attempt passes only if all are true:

1. at least 500 observed trading days;
2. annualized Sharpe >= 1.0 using sqrt(365) and the sample standard deviation of daily net returns;
3. positive arithmetic annualized return;
4. maximum drawdown no worse than -25%;
5. PSR versus zero >= 0.95 using the same Bailey-Lopez de Prado skew/kurtosis estimator as batches 4-13;
6. average days per observed day on which the position crosses zero or changes by at least 0.25 of full exposure <= 2.0;
7. an independent second-process rerun matches all committed statistics exactly.

Every attempt, pass or fail, will be reported with dataset and report SHA-256 checksums. A failure does not open validation.
