# Batch 13: Donchian breakout with fill-aware maker entry

Predeclaration committed before execution as `b602f68`. Validation stayed closed. Six 55-day Donchian variants used 5bp/10bp fill-aware passive entries and paid 5bp on exit. Independent output matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| donchian55-maker10bp-btcusdt | 32.48% | 0.988 | -23.10% | 0.922 | FAIL |
| donchian55-maker10bp-ethusdt | 30.01% | 0.692 | -35.39% | 0.839 | FAIL |
| donchian55-maker10bp-solusdt | -24.30% | -0.532 | -70.79% | 0.227 | FAIL |
| donchian55-maker5bp-btcusdt | 32.38% | 0.985 | -23.14% | 0.922 | FAIL |
| donchian55-maker5bp-ethusdt | 29.89% | 0.690 | -35.45% | 0.838 | FAIL |
| donchian55-maker5bp-solusdt | -24.45% | -0.535 | -70.87% | 0.225 | FAIL |

## Verdict

**0/6 passed.** Closest was `donchian55-maker10bp-btcusdt`: 32.5% annualized, Sharpe 0.988, MDD -23.1%, PSR 0.922. Maker execution improved the BTC result slightly but did not push Sharpe or PSR over their gates. Validation remains closed. Not a live strategy.
