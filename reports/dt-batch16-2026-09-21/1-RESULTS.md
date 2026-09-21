# Batch 16: exit-rule variants on the vol-targeted Donchian maker stack

Predeclaration committed before execution as `e7cf34b`. Validation stayed closed. Six attempts tested partial profit-taking (bank half at +50% over fill, once per entry; the banked half stays in cash and the remainder is vol-managed without regrowing past its post-sale weight) and a 60-day time-exit on the batch-14 stack at the 35% volatility target. Independent output matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| donchian55-maker10bp-vol35-pt50-btcusdt | 29.46% | 1.260 | -17.95% | 0.9697 | PASS |
| donchian55-maker10bp-vol35-pt50-ethusdt | 24.01% | 1.049 | -21.26% | 0.9341 | FAIL |
| donchian55-maker10bp-vol35-pt50-solusdt | -10.70% | -0.500 | -37.87% | 0.2401 | FAIL |
| donchian55-maker10bp-vol35-time60-btcusdt | 24.04% | 0.975 | -15.69% | 0.9228 | FAIL |
| donchian55-maker10bp-vol35-time60-ethusdt | 25.12% | 1.084 | -25.84% | 0.9404 | FAIL |
| donchian55-maker10bp-vol35-time60-solusdt | -7.81% | -0.361 | -42.82% | 0.3048 | FAIL |

## Verdict

**1/6 passed exploration.** `donchian55-maker10bp-vol35-pt50-btcusdt` cleared every gate: +29.46% annualized, Sharpe 1.260, MDD -17.95%, PSR 0.9697, 731 days, 0.014 position events/day. This is the lab's first exploration pass. Per protocol it earns exactly one predeclared validation attempt on the untouched 2026+ window; validation will be predeclared separately before any 2026+ data is fetched. The time-exit variant did not pass anywhere. ETHUSDT improved but failed PSR; SOLUSDT stayed far away. This remains research, not a live strategy.
