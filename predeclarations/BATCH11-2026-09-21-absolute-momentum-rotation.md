# Batch 11 predeclaration: absolute-momentum-gated cross-asset rotation

Locked before batch-11 execution on 2026-09-21 (Asia/Jerusalem). Commit remotely before parsing data. The 2026+ window remains closed.

## Design

Daily BTCUSDT, ETHUSDT and SOLUSDT complete UTC closes from Binance.US; exploration 2024-01-01 through 2025-12-31, prior data for warm-up only. Six attempts use 7, 14 or 30 calendar-day trailing return and top-1 or top-2 selection. At close t, rank assets by trailing return. At t+1 assign equal weights only to selected assets whose score is strictly positive; the unused weight stays cash at zero return. If none is positive, hold cash. Ties break alphabetically. Decisions at t apply to t-to-t+1 returns. Long/cash, no leverage.

Cost is 5bp per unit of absolute portfolio-weight change, including moves to or from cash and initial entry. No forward filling; use dates with valid closes and lookbacks for all assets.

## Gates

At least 500 days; annualized Sharpe >=1.0 using sqrt(365) and sample standard deviation; positive arithmetic annualized return; max drawdown >=-25%; PSR versus zero >=0.95 under the prior estimator; <=2 weight-changing rebalances/day; exact independent second-process match. Report every attempt and checksums. Validation stays closed unless an attempt passes every gate.
