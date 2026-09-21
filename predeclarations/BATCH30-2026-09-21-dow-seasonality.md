# Batch 30 predeclaration: crypto day-of-week seasonality (exploration)

Locked before any batch-30 execution on 2026-09-21 (Asia/Jerusalem). Calendar-anomaly family, untested so far. Data: the already-published batch-19 Binance.US hourly spot files (SHA-256 re-recorded); no new data is fetched beyond re-downloading the identical public dataset after a workspace rebuild (checksums must match the published batch-19 values, verified before execution). Multiple-comparison discipline: the full grid below is fixed a priori, every attempt is reported, and no subset selection happens after execution.

## Fixed design

- Universe: BTCUSDT, ETHUSDT, SOLUSDT spot, Binance.US hourly bars aggregated to UTC daily closes, exploration window 2024-01-01 through 2025-12-31 UTC (731 days).
- Signal (per attempt): attempt (symbol, w) holds 1 unit long on every UTC day whose weekday equals w (0=Monday ... 6=Sunday), flat on all other days. Mechanically: position for day t is 1 iff weekday(t)=w; day-t return = position x (C(t)/C(t-1) - 1); entry is at the prior day's UTC close, exit at day t's UTC close.
- Attempts: 7 weekdays x 3 symbols = 21 attempts, named dow{w}-{symbol}.
- Costs: 5bp taker per position change (each weekly round trip = one entry + one exit = 10bp total), charged to the day the change occurs.
- Gates evaluated on the 731-day daily series exactly as in batches 6-29 (annualized Sharpe sqrt(365), sample standard deviation; PSR with the same skew/kurtosis estimator).

## Gates (unchanged)

Annualized Sharpe >= 1.0; positive arithmetic annualized return; max drawdown no worse than -25%; PSR >= 0.95; >= 500 observed days; <= 2 position changes per day (each attempt changes position at most twice per week, so this gate is structural, not binding); byte-exact independent second-process rerun. No rounding up of near-misses.

## Rules

This is exploration. Any pass earns robustness follow-ups, not validation; the 2026+ window stays closed. Report files only under reports/dt-batch30-2026-09-21/ with SHA-256 checksums, twin-run verification, and fresh-clone verification.
