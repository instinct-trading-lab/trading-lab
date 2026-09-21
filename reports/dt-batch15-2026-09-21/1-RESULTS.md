# Batch 15: volatility-target ladder on the Donchian maker-entry stack

Predeclaration committed before execution as `4ca04fc`. Validation stayed closed. Twelve attempts swept the annualized volatility target across 45%, 40%, 30% and 25% on the batch-14 stack. Independent output matched byte for byte. Batch-14 rungs (50%, 35%) are shown in the batch-14 report.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| donchian55-maker10bp-vol25-btcusdt | 19.48% | 1.000 | -13.51% | 0.9259 | FAIL |
| donchian55-maker10bp-vol25-ethusdt | 13.29% | 0.743 | -20.80% | 0.8550 | FAIL |
| donchian55-maker10bp-vol25-solusdt | -10.48% | -0.659 | -32.43% | 0.1755 | FAIL |
| donchian55-maker10bp-vol30-btcusdt | 23.81% | 1.035 | -16.07% | 0.9335 | FAIL |
| donchian55-maker10bp-vol30-ethusdt | 16.18% | 0.755 | -24.37% | 0.8592 | FAIL |
| donchian55-maker10bp-vol30-solusdt | -12.57% | -0.659 | -37.80% | 0.1755 | FAIL |
| donchian55-maker10bp-vol40-btcusdt | 29.51% | 1.058 | -19.35% | 0.9378 | FAIL |
| donchian55-maker10bp-vol40-ethusdt | 21.48% | 0.772 | -30.35% | 0.8642 | FAIL |
| donchian55-maker10bp-vol40-solusdt | -16.76% | -0.659 | -47.51% | 0.1755 | FAIL |
| donchian55-maker10bp-vol45-btcusdt | 30.02% | 1.024 | -20.72% | 0.9310 | FAIL |
| donchian55-maker10bp-vol45-ethusdt | 22.25% | 0.728 | -32.94% | 0.8497 | FAIL |
| donchian55-maker10bp-vol45-solusdt | -18.86% | -0.659 | -51.90% | 0.1755 | FAIL |

## Verdict

**0/12 passed.** PSR on BTCUSDT is concave in the volatility target with its peak near 35%: 0.9259 (25%), 0.9335 (30%), 0.9378 (40%), 0.9310 (45%), against 0.9394 at 35% and 0.9259 at 50% in batch 14. No rung reaches 0.95. Sizing alone cannot clear the PSR gate on this stack; the knob is exhausted. ETHUSDT and SOLUSDT stayed far from the gates at every target. Validation remains closed. Not a live strategy.
