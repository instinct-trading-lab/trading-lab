# Batch 6: higher-timeframe trend, exploration result

Predeclaration: `predeclarations/BATCH6-2026-09-21-higher-timeframe-trend.md`, committed before any data execution as remote commit `0d9a13e` on 2026-09-21.

Six new exploration attempts were run on public Binance.US hourly candles aggregated per the predeclaration (UTC daily bars; aligned 4h bars), exploration window 2024-01-01 through 2025-12-31, 5bp charged per position change, next-bar accounting, long/flat. Each attempt was rerun in a second independent process with an exact statistics match. Dataset checksums are recorded in each attempt JSON; report-file checksums are in `2-SHA256SUMS.txt`.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Changes/day | Verdict |
|---|---:|---:|---:|---:|---:|---|
| daily-sma50 / BTCUSDT | 38.69% | 1.119 | -25.89% | 0.946 | 0.067 | FAIL |
| daily-sma50 / ETHUSDT | 54.15% | 1.178 | -36.69% | 0.959 | 0.048 | FAIL |
| daily-sma50 / SOLUSDT | 24.73% | 0.425 | -51.34% | 0.727 | 0.053 | FAIL |
| h4-golden / BTCUSDT | 29.01% | 0.830 | -35.73% | 0.883 | 0.040 | FAIL |
| h4-golden / ETHUSDT | 46.32% | 1.000 | -44.15% | 0.930 | 0.029 | FAIL |
| h4-golden / SOLUSDT | 44.04% | 0.788 | -37.24% | 0.869 | 0.032 | FAIL |

## Verdict

**0/6 passed exploration.** This is the first batch in the lab where every attempt made money after costs - slow trend on aggregated bars is a categorically different profile from intraday reversion - but no attempt clears all gates. The binding constraint is drawdown: gate 4 (-25%) kills all six, with max drawdowns of -26% to -51%. Turnover is trivially low (0.03-0.07 changes/day), so costs are no longer the bottleneck.

daily-sma50 on ETHUSDT is the strongest package so far: Sharpe 1.18, PSR 0.959 (passes the PSR gate), +54.2% annualized, but a -36.7% drawdown. It is a research lead, not a pass.

## What this implies for the next batch (proposal, not started)

The grounded follow-up is drawdown control on this exact family, not new signals: a predeclared volatility-scaled position sizing or a predeclared trailing exit on daily-sma50/h4-golden, same symbols, windows, costs and gates. The untouched 2026+ validation window remains closed.

This is new experimental work. It provides no basis for live trading.
