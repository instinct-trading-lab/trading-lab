# Batch 18: Donchian window ladder on the vol-targeted maker-entry stack

Predeclaration committed before execution as `911d4e6`. Nine attempts tested (35,17), (90,45) and (120,60) window pairs on the batch-14 stack at the 35% volatility target, 2024-2025 exploration only. Independent output matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| donchian120x60-maker10bp-vol35-btcusdt | 3.99% | 0.171 | -21.46% | 0.5960 | FAIL |
| donchian120x60-maker10bp-vol35-ethusdt | -7.91% | -0.299 | -36.72% | 0.3367 | FAIL |
| donchian120x60-maker10bp-vol35-solusdt | 4.27% | 0.140 | -24.86% | 0.5786 | FAIL |
| donchian35x17-maker10bp-vol35-btcusdt | 17.48% | 0.678 | -26.46% | 0.8348 | FAIL |
| donchian35x17-maker10bp-vol35-ethusdt | 28.31% | 1.210 | -27.15% | 0.9614 | FAIL |
| donchian35x17-maker10bp-vol35-solusdt | -1.54% | -0.066 | -32.83% | 0.4628 | FAIL |
| donchian90x45-maker10bp-vol35-btcusdt | 21.71% | 0.915 | -16.52% | 0.9088 | FAIL |
| donchian90x45-maker10bp-vol35-ethusdt | 16.63% | 0.725 | -27.80% | 0.8493 | FAIL |
| donchian90x45-maker10bp-vol35-solusdt | -2.82% | -0.115 | -27.39% | 0.4356 | FAIL |

## Verdict

**0/9 passed.** The ladder shows no coherent structure: each asset's best window is different (ETHUSDT 35/17: Sharpe 1.210, PSR 0.9614, but MDD -27.15% fails; BTCUSDT 55/27 was the batch-14 peak; 120/60 is dead everywhere). A robust trend family would not need a different lucky window per asset. Combined with the batch-17 validation failure, this says the Donchian-maker family's apparent edge is window-and-asset-specific luck, not structure. The family joins reversion and rotation on the dead list unless a future predeclaration gives a reasoned mechanism for window choice. Validation remains closed. Not a live strategy.
