# Batch 4: low-turnover reversion, exploration result

Predeclaration: `predeclarations/BATCH4-2026-09-20-low-turnover-reversion.md`, committed before data execution as remote commit `5b81d4d`.

Six new exploration attempts were run on public Binance.US hourly candles, 2024-01-01 through 2025-12-31, with 5bp charged per position change and next-bar accounting. Each was independently rerun with an exact statistics match. Dataset checksums are recorded in each attempt JSON.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Changes/day | Verdict |
|---|---:|---:|---:|---:|---:|---|
| rsi2 / BTCUSDT | -1.97% | -0.496 | -5.24% | 0.173 | 0.003 | FAIL |
| rsi2 / ETHUSDT | 5.43% | 0.385 | -21.07% | 0.714 | 0.019 | FAIL |
| rsi2 / SOLUSDT | 0.26% | 0.132 | -1.39% | 0.578 | 0.003 | FAIL |
| vwaprev / BTCUSDT | 0.29% | 0.014 | -33.14% | 0.508 | 0.123 | FAIL |
| vwaprev / ETHUSDT | -44.93% | -1.105 | -73.60% | 0.055 | 0.148 | FAIL |
| vwaprev / SOLUSDT | -14.26% | -0.371 | -56.38% | 0.298 | 0.131 | FAIL |

## Verdict

**0/6 passed exploration.** The redesign met the turnover target in all six attempts, but reducing churn did not create a reliable cost-bearing edge. The strongest return, RSI-extreme reversion on ETHUSDT, remained far below the Sharpe and PSR gates. The untouched 2026+ validation window was therefore not opened.

This is new experimental work and a negative result. It does not change the earlier batch-3 conclusion, and it provides no basis for live trading.
