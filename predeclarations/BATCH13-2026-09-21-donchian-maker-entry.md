# Batch 13 predeclaration: Donchian breakout with fill-aware maker entry

Locked before batch-13 execution on 2026-09-21 (Asia/Jerusalem). Commit remotely before parsing data. The 2026+ validation window remains closed.

## Rationale and design

Batch 12's BTC 55-day Donchian cleared drawdown (-23.22%) but narrowly missed Sharpe (0.980); batch 10 showed fill-aware passive entry improved risk-adjusted results on daily trend. Batch 13 tests that execution synthesis without changing the signal.

Public Binance.US hourly BTCUSDT, ETHUSDT and SOLUSDT candles are aggregated to complete UTC daily OHLC bars. Exploration: 2024-01-01 through 2025-12-31, with prior warm-up only. Six attempts: 55-day Donchian entry / 27-day exit on each symbol, using passive-entry offsets of 5bp or 10bp below the signal-day close.

After close t, when flat and close_t is strictly above the maximum high of the preceding 55 complete days excluding t, place a one-day post-only buy limit at close_t*(1-offset). It fills during t+1 only if low_(t+1) <= limit; if filled, earn close_(t+1)/limit-1 that day. If unfilled, cancel after t+1 close; place a fresh order only if t+1 itself remains a valid breakout. Once long, exit at close t when close_t is strictly below the minimum low of the preceding 27 complete days excluding t; the return through that close is earned.

Maker entry fee: 0bp. Taker exit fee: 5bp. No rebates, leverage, shorts or credit before fill. Missing/incomplete days break continuity; no forward fill.

## Gates

At least 500 days; annualized Sharpe >=1.0 using sqrt(365) and sample standard deviation; positive arithmetic annualized return; max drawdown >=-25%; PSR versus zero >=0.95 using the prior estimator; <=2 entries plus exits/day; exact independent second-process match. Report all attempts and checksums. A failure does not open validation.
