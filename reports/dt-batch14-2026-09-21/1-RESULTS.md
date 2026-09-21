# Batch 14: volatility-targeted Donchian breakout with maker entry

Predeclaration committed before execution as `3ec3389`. Validation stayed closed. Six attempts applied 20-day volatility-targeted sizing (50% and 35% annualized targets) to the batch-13 Donchian55 signal with 10bp fill-aware maker entry and 5bp exit/resize taker costs. Independent output matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| donchian55-maker10bp-vol35-btcusdt | 27.65% | 1.065 | -17.95% | 0.9394 | FAIL |
| donchian55-maker10bp-vol35-ethusdt | 18.93% | 0.763 | -27.46% | 0.8618 | FAIL |
| donchian55-maker10bp-vol35-solusdt | -14.67% | -0.659 | -42.82% | 0.1755 | FAIL |
| donchian55-maker10bp-vol50-btcusdt | 30.39% | 1.000 | -22.08% | 0.9259 | FAIL |
| donchian55-maker10bp-vol50-ethusdt | 23.43% | 0.706 | -34.69% | 0.8425 | FAIL |
| donchian55-maker10bp-vol50-solusdt | -20.86% | -0.657 | -55.89% | 0.1764 | FAIL |

## Verdict

**0/6 passed.** Closest was `donchian55-maker10bp-vol35-btcusdt`: 27.65% annualized, Sharpe 1.065, MDD -17.95%, PSR 0.9394 - PSR missed the 0.95 gate by 0.0106 while Sharpe, return and drawdown all cleared. Vol targeting improved every metric on BTCUSDT versus batch 13 (Sharpe 0.988 -> 1.065, MDD -23.10% -> -17.95%) but PSR remains the binding gate. ETHUSDT and SOLUSDT stayed far from the gates. Validation remains closed. Not a live strategy.
