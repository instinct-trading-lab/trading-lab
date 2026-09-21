# Batch 8: volatility-scaled higher-timeframe trend, exploration result

Predeclaration: `predeclarations/BATCH8-2026-09-21-vol-scaled-trend.md`, committed before execution as remote commit `524109c` on 2026-09-21 (11:23:55 IDT; code ran 11:24 IDT).

Six exploration attempts: the batch-6 trend families with predeclared volatility-targeted fractional exposure (target 50% annualized, trailing 20-bar realized vol, exposure = min(1, 0.50/vol)), 5bp per unit of exposure traded, next-bar accounting, long-only. Same batch-6 dataset (checksums match batch-6 attempt JSONs). Each attempt was rerun in a second independent process with an exact statistics match.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Changes/day | Verdict |
|---|---:|---:|---:|---:|---:|---|
| daily-sma50-vol / BTCUSDT | 36.29% | 1.136 | -24.14% | 0.9496 | 0.067 | FAIL |
| daily-sma50-vol / ETHUSDT | 44.57% | 1.188 | -34.26% | 0.963 | 0.052 | FAIL |
| daily-sma50-vol / SOLUSDT | 18.13% | 0.453 | -40.43% | 0.740 | 0.053 | FAIL |
| h4-golden-vol / BTCUSDT | 25.14% | 0.762 | -33.00% | 0.861 | 0.049 | FAIL |
| h4-golden-vol / ETHUSDT | 27.40% | 0.738 | -38.65% | 0.857 | 0.044 | FAIL |
| h4-golden-vol / SOLUSDT | 25.77% | 0.656 | -29.26% | 0.825 | 0.044 | FAIL |

## Verdict

**0/6 passed exploration.** Volatility scaling is the first drawdown control that moved the binding gate: BTCUSDT daily-sma50 came inside the drawdown gate (-24.14% vs -25%) with Sharpe 1.136 and +36.3% annualized, and failed only the PSR gate at 0.94957 versus 0.95 - a miss of 0.0004. Per the predeclared gates this is a FAIL, and the untouched 2026+ validation window stays closed. The gates are the gates: no rounding, no exception, and this report does not open validation.

Reading across batches 6-8: the daily-sma50 family on BTC/ETH is consistently the strongest package (Sharpe 1.1-1.2 after costs across all three sizing/exit variants), and drawdown, not cost or turnover, is the only binding constraint. Whether that profile survives the untouched 2026+ regime is exactly what validation is for, and validation requires a full exploration pass first.

This is new experimental work. It provides no basis for live trading.
