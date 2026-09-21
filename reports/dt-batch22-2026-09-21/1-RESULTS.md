# Batch 22: multi-timeframe trend confluence

Predeclaration committed before execution as `9504978`. Three attempts required agreement between the 50-day SMA and the 52-week momentum filter, 2024-2025 exploration only. Independent output matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| mtf-sma50-tsmom364-vol35-btcusdt | 29.91% | 1.105 | -20.83% | 0.9449 | FAIL |
| mtf-sma50-tsmom364-vol35-ethusdt | 15.14% | 0.637 | -27.71% | 0.8184 | FAIL |
| mtf-sma50-tsmom364-vol35-solusdt | 4.88% | 0.177 | -30.43% | 0.5991 | FAIL |

## Verdict

**0/3 passed.** Confluence improved the BTCUSDT package again (+29.91%, Sharpe 1.105, MDD -20.83% - all pass) but PSR 0.9449 still misses 0.95, by 0.0051. PSR is the asymptote this vein keeps hitting: every structure lands between 0.91 and 0.97 and only the batch-16 outlier ever crossed, which validation then killed. ETHUSDT and SOLUSDT fail. Validation remains closed. Not a live strategy.
