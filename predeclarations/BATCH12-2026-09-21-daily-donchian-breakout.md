# Batch 12 predeclaration: daily Donchian breakout

Locked before batch-12 execution on 2026-09-21 (Asia/Jerusalem). Commit remotely before parsing data. The 2026+ validation window remains closed.

## Design

Public Binance.US hourly candles for BTCUSDT, ETHUSDT and SOLUSDT, aggregated to complete UTC daily bars. Exploration is 2024-01-01 through 2025-12-31; prior data is warm-up only. Six attempts: 20-day and 55-day Donchian breakout on each symbol.

At close t, enter long for t+1 when close_t is strictly above the maximum high of the preceding N complete days, excluding t. Once long, exit for t+1 when close_t is strictly below the minimum low of the preceding floor(N/2) complete days, excluding t. Otherwise retain state. Position decided at t earns the t-to-t+1 close return. Long/flat, no leverage. Cost is 5bp per position change, charged when the new position applies. Missing/incomplete days break continuity; no forward fill.

## Gates

At least 500 days; annualized Sharpe >=1.0 using sqrt(365) and sample standard deviation; positive arithmetic annualized return; max drawdown >=-25%; PSR versus zero >=0.95 using the prior estimator; <=2 position changes/day; exact independent second-process match. Report every attempt and checksums. No failed exploration opens validation.
