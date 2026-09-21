# Batch 10: fill-aware maker-entry execution model, exploration result

Predeclaration: `predeclarations/BATCH10-2026-09-21-maker-entry-model.md`, committed before execution as remote commit `9808e88`. The 2026+ validation window was not opened.

Six attempts applied conservative one-day passive entries 5bp or 10bp below the preceding signal-day close to daily-sma50 on BTC, ETH and SOL. An order filled only when the following complete UTC day's low touched its limit; unfilled orders were canceled and recomputed after the next close. Maker entry fee was 0bp and taker exit fee 5bp. Each attempt was rerun in a separate process with byte-identical output.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Events/day | Verdict |
|---|---:|---:|---:|---:|---:|---|
| dailysma50-maker10bp-btcusdt | 39.90% | 1.152 | -25.34% | 0.951 | 0.068 | FAIL |
| dailysma50-maker10bp-ethusdt | 55.49% | 1.205 | -36.13% | 0.963 | 0.049 | FAIL |
| dailysma50-maker10bp-solusdt | 22.50% | 0.388 | -50.91% | 0.709 | 0.055 | FAIL |
| dailysma50-maker5bp-btcusdt | 39.27% | 1.134 | -25.52% | 0.949 | 0.068 | FAIL |
| dailysma50-maker5bp-ethusdt | 55.03% | 1.196 | -36.32% | 0.962 | 0.049 | FAIL |
| dailysma50-maker5bp-solusdt | 22.00% | 0.379 | -51.06% | 0.705 | 0.055 | FAIL |

## Verdict

**0/6 passed exploration.** The best risk-adjusted attempt was `dailysma50-maker10bp-ethusdt`: 55.5% arithmetic annualized return, Sharpe 1.205, max drawdown -36.13%, and PSR 0.963. BTC at 10bp passed Sharpe and PSR but missed the drawdown gate by 0.34 percentage points (-25.34% versus -25%). ETH passed Sharpe and PSR but missed drawdown by more than 11 points. SOL failed Sharpe, PSR and drawdown.

The maker-entry execution hypothesis improved the BTC package over plain taker execution but did not clear the locked gate. No rounding or exception is applied, and validation stays closed. This is not a live strategy.
