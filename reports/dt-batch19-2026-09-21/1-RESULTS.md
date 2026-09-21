# Batch 19: slow time-series momentum (new family)

Predeclaration committed before any data fetch or execution as `6ab08b8`. Six attempts tested literature-anchored 26-week and 52-week time-series momentum lookbacks with 35% volatility-target sizing, 2024-2025 exploration only. Independent output matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| tsmom182d-vol35-btcusdt | 32.24% | 0.934 | -24.53% | 0.9088 | FAIL |
| tsmom182d-vol35-ethusdt | -18.66% | -0.587 | -63.76% | 0.2045 | FAIL |
| tsmom182d-vol35-solusdt | -1.02% | -0.032 | -37.46% | 0.4822 | FAIL |
| tsmom364d-vol35-btcusdt | 34.50% | 0.962 | -24.90% | 0.9149 | FAIL |
| tsmom364d-vol35-ethusdt | 8.47% | 0.248 | -36.31% | 0.6377 | FAIL |
| tsmom364d-vol35-solusdt | 10.76% | 0.300 | -31.42% | 0.6643 | FAIL |

## Verdict

**0/6 passed.** BTCUSDT again carries the family (52-week: +34.50%, Sharpe 0.962, MDD -24.90%, PSR 0.9149 - misses Sharpe by 0.038, drawdown by 0.10pp, PSR by 0.035) and again it is not enough; ETHUSDT and SOLUSDT fail at both lookbacks. The pattern across batches 6-19 is consistent: long-only BTC trend/momentum sits near Sharpe 0.9-1.0 in 2024-2025, close to BTC beta itself, and no execution or sizing variant has separated from it. Validation remains closed. Not a live strategy.
