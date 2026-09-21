# Batch 27: hourly-horizon time-series momentum (exploration)

Predeclaration committed before any execution (raw-file SHA-256 `52459d7929624667f21e39a0b365d6ec72eeadbd2057a4c9eaf9a453092acb84`). Hourly TSMOM, long-flat, 3 lookbacks x 3 symbols = 9 fixed attempts, 5bp taker per position change, gates on the compounded daily series. Independent second-process rerun matched byte for byte. Window data gap-free (31,433 hourly bars per symbol, 2022-06-01..2025-12-31).

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Position events | Verdict |
|---|---:|---:|---:|---:|---:|---|
| hrmom24-btcusdt | -31.86% | -0.886 | -64.70% | 0.1124 | 1737 (2.38/day) | FAIL |
| hrmom24-ethusdt | -76.68% | -1.476 | -85.80% | 0.0249 | 1713 (2.34/day) | FAIL |
| hrmom24-solusdt | -51.70% | -0.863 | -82.88% | 0.1179 | 1626 (2.22/day) | FAIL |
| hrmom72-btcusdt | 10.96% | 0.304 | -50.91% | 0.6676 | 934 (1.28/day) | FAIL |
| hrmom72-ethusdt | 13.64% | 0.271 | -57.46% | 0.6510 | 951 (1.30/day) | FAIL |
| hrmom72-solusdt | 0.82% | 0.014 | -70.63% | 0.5077 | 872 (1.19/day) | FAIL |
| hrmom168-btcusdt | 10.89% | 0.324 | -32.21% | 0.6778 | 618 (0.85/day) | FAIL |
| hrmom168-ethusdt | 21.11% | 0.446 | -45.00% | 0.7401 | 610 (0.83/day) | FAIL |
| hrmom168-solusdt | 15.02% | 0.262 | -46.06% | 0.6450 | 619 (0.85/day) | FAIL |

## Verdict

**0/9 passed.** The hourly horizon shows no harvestable momentum: the 24h lookback is strongly NEGATIVE after costs (Sharpe -0.86 to -1.48, i.e. hourly-scale reversion dominates at that horizon, and its turnover of ~2.3 events/day makes the flip side untradeable at 5bp), and the 72h/168h lookbacks are positive but far below every gate (best Sharpe 0.446, best PSR 0.7401, drawdowns to -45%). Combined with the falsified daily/4h trend families and the falsified 15-minute reversion family, crypto price-based momentum/reversion is now closed at the 15m, hourly, 4h, daily, and weekly horizons on this universe. Open directions remaining: non-crypto universes at daily horizon. 116 exploration attempts to date, 1 exploration pass (killed at validation), 2 validation attempts (both killed their packages).
