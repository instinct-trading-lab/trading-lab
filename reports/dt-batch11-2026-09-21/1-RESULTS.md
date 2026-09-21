# Batch 11: absolute-momentum-gated cross-asset rotation, exploration result

Predeclaration committed before execution as remote commit `b0e05c2`. The 2026+ validation window stayed closed.

Six variants ranked BTC, ETH and SOL on 7, 14 or 30-day relative strength and selected the top one or two, but held the corresponding weight in cash whenever a selected asset's own trailing return was not positive. Costs were 5bp per unit of absolute weight change. A separate process reproduced the complete output byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Rebalances/day | Verdict |
|---|---:|---:|---:|---:|---:|---|
| rs14-top1 | 29.68% | 0.529 | -47.04% | 0.773 | 0.210 | FAIL |
| rs14-top2 | 30.81% | 0.678 | -31.68% | 0.832 | 0.277 | FAIL |
| rs30-top1 | 35.65% | 0.625 | -40.05% | 0.814 | 0.149 | FAIL |
| rs30-top2 | 33.81% | 0.751 | -38.13% | 0.857 | 0.170 | FAIL |
| rs7-top1 | 16.69% | 0.286 | -63.67% | 0.657 | 0.284 | FAIL |
| rs7-top2 | 18.73% | 0.427 | -42.17% | 0.728 | 0.370 | FAIL |

## Verdict

**0/6 passed.** Best Sharpe was `rs30-top2`: 33.8% arithmetic annualized return, Sharpe 0.751, max drawdown -38.1%, PSR 0.857. The cash gate improved drawdown for some variants versus batch 9, but none reached either the Sharpe or drawdown gate. Validation remains closed. This is not a live strategy.
