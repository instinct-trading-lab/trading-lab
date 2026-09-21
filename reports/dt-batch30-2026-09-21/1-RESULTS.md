# Batch 30: crypto day-of-week seasonality (exploration)

Predeclaration committed before any execution (raw-file SHA-256 `46b69b7ff1ea1d0a5e11a4cbf0b6800036561572028d256e5e6c666b59e23fb7`). 7 weekdays x 3 symbols = 21 fixed attempts, long only on weekday w (entered at prior UTC close, exited at day close), 5bp per position change, gates on the 731-day daily series. Workspace was rebuilt before this batch; the batch-19 dataset was re-downloaded from Binance.US and matched the published batch-19 SHA-256 values byte-for-byte before execution. Independent second-process rerun matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| dow0-btcusdt (mon) | 17.47% | 0.791 | -17.66% | 0.8736 | FAIL |
| dow0-ethusdt (mon) | 11.20% | 0.353 | -34.44% | 0.6920 | FAIL |
| dow0-solusdt (mon) | -9.12% | -0.249 | -57.15% | 0.3603 | FAIL |
| dow1-btcusdt (tue) | -14.75% | -0.789 | -39.29% | 0.1287 | FAIL |
| dow1-ethusdt (tue) | -30.34% | -1.170 | -60.10% | 0.0484 | FAIL |
| dow1-solusdt (tue) | -18.86% | -0.640 | -52.80% | 0.1831 | FAIL |
| dow2-btcusdt (wed) | 24.14% | 1.169 | -21.99% | 0.9655 | PASS |
| dow2-ethusdt (wed) | 35.10% | 1.202 | -25.79% | 0.9699 | FAIL |
| dow2-solusdt (wed) | 34.56% | 1.058 | -22.65% | 0.9429 | FAIL |
| dow3-btcusdt (thu) | -12.89% | -0.727 | -31.21% | 0.1652 | FAIL |
| dow3-ethusdt (thu) | -20.29% | -0.688 | -41.66% | 0.1860 | FAIL |
| dow3-solusdt (thu) | -12.88% | -0.392 | -45.81% | 0.2923 | FAIL |
| dow4-btcusdt (fri) | -4.30% | -0.230 | -27.59% | 0.3724 | FAIL |
| dow4-ethusdt (fri) | -7.84% | -0.311 | -27.62% | 0.3308 | FAIL |
| dow4-solusdt (fri) | -7.20% | -0.227 | -32.69% | 0.3735 | FAIL |
| dow5-btcusdt (sat) | -3.72% | -0.448 | -10.03% | 0.2518 | FAIL |
| dow5-ethusdt (sat) | 9.56% | 0.564 | -12.60% | 0.7908 | FAIL |
| dow5-solusdt (sat) | 9.07% | 0.363 | -14.69% | 0.7022 | FAIL |
| dow6-btcusdt (sun) | 5.22% | 0.327 | -24.61% | 0.6801 | FAIL |
| dow6-ethusdt (sun) | 3.42% | 0.146 | -46.31% | 0.5818 | FAIL |
| dow6-solusdt (sun) | 13.09% | 0.407 | -35.32% | 0.7265 | FAIL |

## Verdict

**1/21 passed: dow2-btcusdt (Wednesday, BTC only)** - Sharpe 1.169, PSR 0.9655, MDD -22.0%, +24.1% annualized on ~104 traded days/year, 0.29 position events/day. The two sibling attempts fail narrowly and instructively: dow2-ethusdt breaches the drawdown gate by 0.79pp (-25.79% vs -25%) and dow2-solusdt misses PSR (0.9429). Multiple-comparison discipline applies with full force: with 21 fixed attempts, one borderline pass is consistent with luck, and this lab's own history (batch 16's exploration pass died at validation) says exactly what this earns: a predeclared ROBUSTNESS batch (full-span 2022-2025 data, cost doubling, cross-symbol), not validation. The 2026+ window stays closed. Every other weekday-symbol cell is a clean fail, most of them deeply negative (Tuesday is the mirror image: all three symbols strongly negative).
