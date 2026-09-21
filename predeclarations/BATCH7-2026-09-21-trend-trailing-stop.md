# Batch 7 predeclaration: higher-timeframe trend with predeclared trailing stop

Locked before any batch-7 data execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any batch-7 code is run. Batch 7 reuses the batch-6 dataset (checksums in reports/dt-batch6-2026-09-21 attempt JSONs); no new data is fetched.

## Question

Batch 6 was the first all-positive batch after costs, and the binding gate was drawdown (-26% to -51% vs the -25% gate). Batch 7 asks: does a single predeclared trailing-stop overlay on the exact batch-6 families bring maximum drawdown inside the gate while preserving Sharpe >= 1.0 and PSR >= 0.95?

## Fixed design

Everything identical to batch 6 (data, symbols, windows, 5bp per position change, next-bar accounting, long/flat, aggregation) except the exit logic below. Six exploration attempts: two families on each of the three symbols.

## Signal definitions (fixed, no tuning after this commit)

- daily-sma50-ts: batch-6 daily-sma50 entry rule (long when daily close > 50-day SMA). While in position, track the highest daily close since entry; exit when the daily close < 0.85 x that highest close (15% trailing stop), in addition to the base exit. After a trailing-stop exit, re-entry is allowed only on a fresh base-signal transition (base signal must first turn off, then on again).
- h4-golden-ts: batch-6 h4-golden entry rule (long when 4h SMA50 > 4h SMA200), with the identical 15% trailing-close stop measured on 4h closes, and the same fresh-transition re-entry rule.

## Gates

Identical to batch 6: at least 500 observed trading days; annualized Sharpe >= 1.0; positive arithmetic annualized return; maximum drawdown no worse than -25%; PSR versus zero >= 0.95; average position changes <= 2.0 per day; independent rerun matches the committed statistics exactly.

Every attempt, pass or fail, will be reported. Dataset SHA-256 checksums are recorded per attempt.
