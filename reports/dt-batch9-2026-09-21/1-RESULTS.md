# Batch 9: daily cross-asset relative-strength rotation, exploration result

Predeclaration: `predeclarations/BATCH9-2026-09-21-cross-asset-relative-strength.md`, committed before data execution as remote commit `9d76489` on 2026-09-21. The 2026+ validation window was not opened.

Six portfolio-level attempts were run on BTCUSDT, ETHUSDT and SOLUSDT: trailing relative strength over 7, 14 and 30 calendar days, selecting the strongest one or two assets daily. The selected weights apply to the next close-to-close return. Costs are 5bp per unit of absolute weight change, including initial entry. Each attempt was rerun in a separate process and the complete output matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Rebalances/day | Verdict |
|---|---:|---:|---:|---:|---:|---|
| rs14-top1 | 38.36% | 0.591 | -55.20% | 0.799 | 0.173 | FAIL |
| rs14-top2 | 36.28% | 0.587 | -54.03% | 0.797 | 0.204 | FAIL |
| rs30-top1 | 31.32% | 0.474 | -53.61% | 0.750 | 0.121 | FAIL |
| rs30-top2 | 37.30% | 0.618 | -48.24% | 0.809 | 0.092 | FAIL |
| rs7-top1 | 31.74% | 0.473 | -51.90% | 0.748 | 0.247 | FAIL |
| rs7-top2 | 47.59% | 0.776 | -46.18% | 0.865 | 0.230 | FAIL |

## Verdict

**0/6 passed exploration.** Every variant made money after costs, but all failed both the Sharpe and drawdown gates. The strongest risk-adjusted attempt was `rs7-top2`: 47.6% arithmetic annualized return, Sharpe 0.776, maximum drawdown -46.2%, and PSR 0.865. The family did not earn access to the untouched 2026+ validation window.

Cross-asset rotation reduced neither risk nor drawdown enough relative to the batch-8 BTC daily-sma50 volatility-scaled lead. This closes this plain always-invested relative-strength design under the current gates; it is not a strategy and provides no basis for live trading.
