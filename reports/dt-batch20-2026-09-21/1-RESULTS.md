# Batch 20: time-series momentum portfolio (diversification test)

Predeclaration committed before execution as `11033dd`. Two attempts averaged the three batch-19 momentum legs into an equal-weight basket, 2024-2025 exploration only. Independent output matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Verdict |
|---|---:|---:|---:|---:|---|
| tsmom182d-vol35-basket3 | 4.19% | 0.147 | -33.47% | 0.5824 | FAIL |
| tsmom364d-vol35-basket3 | 17.91% | 0.574 | -25.51% | 0.7918 | FAIL |

## Verdict

**0/2 passed.** Diversification did not rescue the family: the basket dilutes the strong BTCUSDT leg with the weak ETHUSDT and SOLUSDT legs (52-week basket Sharpe 0.574 versus 0.962 for BTCUSDT alone). Diversification only helps when the legs carry comparable positive expectancy; here they do not. Validation remains closed. Not a live strategy.
