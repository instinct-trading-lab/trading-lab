# Batch 32: cross-asset lead-lag (exploration - the last price-based structure)

Predeclaration committed before any execution (raw-file SHA-256 `2b5a8ecc27c418d41c4a0598d7d07d6d8a70536149d17b66356b8f8d2961dae0`). All six directed leader->follower pairs x lookbacks {1,4}h = 12 fixed attempts, long-flat in the follower, 5bp per change, gates on the compounded daily series. Independent second-process rerun matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Events | Verdict |
|---|---:|---:|---:|---:|---:|---|
| ll1-btcusdt-ethusdt | -205.65% | -4.350 | -98.77% | 0.0000 | 12.67/day | FAIL |
| ll1-btcusdt-solusdt | -243.20% | -4.157 | -99.50% | 0.0000 | 12.67/day | FAIL |
| ll1-ethusdt-btcusdt | -195.89% | -6.078 | -98.29% | 0.0000 | 12.62/day | FAIL |
| ll1-ethusdt-solusdt | -230.13% | -3.989 | -99.44% | 0.0000 | 12.62/day | FAIL |
| ll1-solusdt-btcusdt | -187.48% | -5.508 | -98.17% | 0.0000 | 12.50/day | FAIL |
| ll1-solusdt-ethusdt | -192.66% | -4.016 | -98.45% | 0.0000 | 12.50/day | FAIL |
| ll4-btcusdt-ethusdt | -63.20% | -1.299 | -80.60% | 0.0413 | 6.03/day | FAIL |
| ll4-btcusdt-solusdt | -126.55% | -2.161 | -94.73% | 0.0015 | 6.03/day | FAIL |
| ll4-ethusdt-btcusdt | -68.65% | -2.066 | -79.44% | 0.0025 | 5.97/day | FAIL |
| ll4-ethusdt-solusdt | -101.98% | -1.772 | -92.49% | 0.0072 | 5.97/day | FAIL |
| ll4-solusdt-btcusdt | -42.98% | -1.268 | -68.50% | 0.0410 | 5.77/day | FAIL |
| ll4-solusdt-ethusdt | -40.90% | -0.857 | -68.77% | 0.1230 | 5.77/day | FAIL |

## Verdict

**0/12 passed, and none was close.** Following another asset's hourly move trades 5.8-12.7 times per day, and at 5bp per change that turnover is fatal: every attempt is deeply negative (Sharpe -0.86 to -6.08, drawdowns to -99.5%). Whatever lead-lag information exists between these assets at the hourly scale is worth far less than its transaction costs at retail taker pricing. This closes the lab's exploration map: price-based trading is now falsified in both directions at every tested horizon, across single assets, crosses, rotations, confluences, regime filters, calendar effects, and lead-lag pairs. 181 exploration attempts + 10 robustness attempts, 2 validation attempts, 0 surviving packages. The lab's final conclusion follows as reports/FINAL-CONCLUSION.md.
