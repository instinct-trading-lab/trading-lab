# Batch 21: long-short time-series momentum (short-side falsification)

Predeclaration committed before execution as `4c0ec55`. Six attempts gave the batch-19 momentum signal a symmetric short side with deliberately free shorts (no borrow or funding), 2024-2025 exploration only. Independent output matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| lstmom182d-vol35-btcusdt | 31.27% | 0.854 | -28.08% | 0.8879 | FAIL |
| lstmom182d-vol35-ethusdt | -58.80% | -1.454 | -84.79% | 0.0187 | FAIL |
| lstmom182d-vol35-solusdt | -20.23% | -0.524 | -63.26% | 0.2291 | FAIL |
| lstmom364d-vol35-btcusdt | 35.89% | 0.980 | -26.25% | 0.9187 | FAIL |
| lstmom364d-vol35-ethusdt | -4.43% | -0.109 | -55.68% | 0.4386 | FAIL |
| lstmom364d-vol35-solusdt | 3.47% | 0.090 | -47.36% | 0.5506 | FAIL |

## Verdict

**0/6 passed, direction falsified.** Even with free shorts, long-short does not clear the gates anywhere: BTCUSDT 52-week lands at Sharpe 0.980 / PSR 0.9187 (no better than long-only), and the short side is catastrophic on ETHUSDT (26-week: -58.80% annualized, MDD -84.79%). The short side of this signal adds nothing, so no funding-cost follow-up is warranted. Validation remains closed. Not a live strategy.
