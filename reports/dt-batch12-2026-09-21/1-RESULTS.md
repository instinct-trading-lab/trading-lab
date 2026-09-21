# Batch 12: daily Donchian breakout, exploration result

Predeclaration committed before execution as remote commit `a67b67a`. Validation stayed closed. Six 20/55-day variants used next-day accounting and 5bp per position change; a second process matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| donchian20-btcusdt | 25.36% | 0.818 | -29.10% | 0.879 | FAIL |
| donchian20-ethusdt | -2.17% | -0.055 | -47.15% | 0.469 | FAIL |
| donchian20-solusdt | 4.31% | 0.098 | -40.59% | 0.555 | FAIL |
| donchian55-btcusdt | 32.22% | 0.980 | -23.22% | 0.920 | FAIL |
| donchian55-ethusdt | 29.67% | 0.685 | -35.57% | 0.836 | FAIL |
| donchian55-solusdt | -17.62% | -0.379 | -71.01% | 0.297 | FAIL |

## Verdict

**0/6 passed.** Closest was `donchian55-btcusdt`: 32.2% annualized, Sharpe 0.980, MDD -23.2%, PSR 0.920. It passed drawdown but missed Sharpe and PSR. Validation remains closed. Not a live strategy.
