# Batch 29: hourly-scale crypto reversion (exploration)

Predeclaration committed before any execution (raw-file SHA-256 `bee6ad1ea168f8b7e39541c0d476955db1b8792e96270208eca17b5d02446672`). Direct test of the implication left by batch 27 (24h hourly momentum was strongly negative after costs). Long-flat reversion, k in {1,4,8,24}h x BTC/ETH/SOL = 12 fixed attempts, 5bp per position change, gates on the compounded daily series. Independent second-process rerun matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Position events | Verdict |
|---|---:|---:|---:|---:|---:|---|
| hrrev1-btcusdt | -163.47% | -5.420 | -96.70% | 0.0000 | 9256 (12.66/day) | FAIL |
| hrrev1-ethusdt | -192.62% | -4.186 | -98.32% | 0.0000 | 9216 (12.61/day) | FAIL |
| hrrev1-solusdt | -134.07% | -2.221 | -95.35% | 0.0014 | 9130 (12.49/day) | FAIL |
| hrrev4-btcusdt | -80.85% | -2.643 | -82.88% | 0.0001 | 4408 (6.03/day) | FAIL |
| hrrev4-ethusdt | -101.90% | -2.169 | -90.75% | 0.0008 | 4359 (5.96/day) | FAIL |
| hrrev4-solusdt | -52.95% | -0.924 | -82.01% | 0.0936 | 4208 (5.76/day) | FAIL |
| hrrev8-btcusdt | -70.68% | -2.347 | -79.08% | 0.0002 | 3059 (4.18/day) | FAIL |
| hrrev8-ethusdt | -80.15% | -1.709 | -84.87% | 0.0056 | 2986 (4.08/day) | FAIL |
| hrrev8-solusdt | -33.18% | -0.595 | -73.61% | 0.1976 | 2937 (4.02/day) | FAIL |
| hrrev24-btcusdt | -7.29% | -0.237 | -36.84% | 0.3680 | 1737 (2.38/day) | FAIL |
| hrrev24-ethusdt | 28.97% | 0.612 | -42.86% | 0.8037 | 1713 (2.34/day) | FAIL |
| hrrev24-solusdt | 15.61% | 0.276 | -42.86% | 0.6512 | 1628 (2.23/day) | FAIL |

## Verdict

**0/12 passed.** At 1h/4h/8h lookbacks, turnover (4.0-12.7 position changes per day) makes reversion catastrophic after 5bp costs - Sharpe -0.6 to -5.4, drawdowns to -98%, and the <= 2 events/day gate binds exactly as predeclared. At 24h the best attempt (hrrev24-ethusdt: Sharpe 0.612, PSR 0.8037, +29.0% annualized) still misses every statistical gate and breaches the events/day gate (2.34/day). Note the asymmetry with batch 27: flipping the sign of a losing strategy does not produce its mirror image, because costs and the long-flat constraint are not symmetric. Crypto price-based trading is now falsified in BOTH directions (momentum and reversion) at the 15m, hourly, 4h, daily, and weekly horizons on this universe, and daily TSMOM is additionally falsified on 8 major non-crypto series (batch 28). 148 exploration attempts to date.
