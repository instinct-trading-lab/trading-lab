# Batch 7: trailing-stop trend, exploration result

Predeclaration: `predeclarations/BATCH7-2026-09-21-trend-trailing-stop.md`, committed before execution as remote commit `b582a66` on 2026-09-21, timestamped before any batch-7 code ran.

Six exploration attempts, identical design to batch 6 plus one predeclared overlay: exit when the close falls below 85% of the highest close since entry (15% trailing stop), re-entry only on a fresh base-signal transition. Same batch-6 dataset (checksums match batch-6 attempt JSONs), same windows, 5bp per position change, next-bar accounting, long/flat. Each attempt was rerun in a second independent process with an exact statistics match.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Changes/day | Verdict |
|---|---:|---:|---:|---:|---:|---|
| daily-sma50-ts / BTCUSDT | 36.51% | 1.122 | -28.08% | 0.947 | 0.067 | FAIL |
| daily-sma50-ts / ETHUSDT | 51.86% | 1.163 | -38.78% | 0.958 | 0.048 | FAIL |
| daily-sma50-ts / SOLUSDT | 48.69% | 0.935 | -38.42% | 0.910 | 0.052 | FAIL |
| h4-golden-ts / BTCUSDT | 26.15% | 0.795 | -38.45% | 0.872 | 0.040 | FAIL |
| h4-golden-ts / ETHUSDT | 48.20% | 1.088 | -41.61% | 0.948 | 0.029 | FAIL |
| h4-golden-ts / SOLUSDT | 25.55% | 0.665 | -40.54% | 0.830 | 0.030 | FAIL |

## Verdict

**0/6 passed exploration.** The 15% trailing stop did not fix the binding gate. Comparing like-for-like with batch 6: BTC daily drawdown barely moved (-25.9% to -28.1%), ETH daily got worse (-36.7% to -38.8%), and Sharpe was roughly unchanged. The drawdown in these families does not come from single runaway trends that a trailing stop can cut; it comes from repeated whipsaw losses through volatile regimes, which the stop crystallizes rather than prevents.

The drawdown problem in the higher-timeframe trend family is therefore structural to position timing, not exit latency. Remaining grounded drawdown-control variant: volatility-scaled position sizing (exposure inversely proportional to realized volatility), which changes the cost and turnover accounting and needs its own predeclaration. The untouched 2026+ validation window remains closed.

This is new experimental work and a negative result. It provides no basis for live trading.
