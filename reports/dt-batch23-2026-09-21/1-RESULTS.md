# Batch 23: funding-gated slow trend (non-price regime signal)

Predeclaration committed before any funding fetch or execution as `c34f95e`. Three attempts gated the batch-19 52-week trend with a 7-day funding crowding filter (flat when trailing mean funding exceeds 5x the 0.01% baseline), 2024-2025 exploration only. Cross-venue construction (Binance.com perp funding as gauge, Binance.US spot prices) predeclared. Independent output matched byte for byte. Funding fetch: Binance public data archive, 2559 records per symbol, no gaps.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| fundgate-tsmom364-vol35-btcusdt | 32.68% | 0.912 | -25.21% | 0.9032 | FAIL |
| fundgate-tsmom364-vol35-ethusdt | 4.45% | 0.132 | -36.31% | 0.5740 | FAIL |
| fundgate-tsmom364-vol35-solusdt | -0.25% | -0.007 | -31.42% | 0.4960 | FAIL |

## Verdict

**0/3 passed, hypothesis falsified as designed.** The crowding filter did not remove the left tail; it removed good days too. On BTCUSDT every metric moved the wrong way versus ungated batch 19 (Sharpe 0.962 -> 0.912, MDD -24.90% -> -25.21%, PSR 0.9149 -> 0.9032). Extreme funding in 2024-2025 marked strong trends more often than imminent flushes. Validation remains closed. Not a live strategy.
