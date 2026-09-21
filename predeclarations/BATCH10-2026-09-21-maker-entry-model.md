# Batch 10 predeclaration: fill-aware maker-entry execution model

Locked before any batch-10 execution on 2026-09-21 (Asia/Jerusalem). This file must be committed to the remote repository before batch-10 data is parsed or inspected. The 2026+ validation window remains closed.

## Question

Batch 8 brought BTC daily-sma50 inside the drawdown gate but missed PSR by 0.0004. Batch 10 tests a different execution hypothesis, not another signal: can conservative passive entries improve the daily-sma50 family after realistic unfilled-order handling?

## Fixed design

- Public Binance.US hourly candles for BTCUSDT, ETHUSDT and SOLUSDT, aggregated to complete UTC daily OHLC bars.
- Exploration: 2024-01-01 through 2025-12-31 UTC, with prior bars only for SMA warm-up. Validation from 2026-01-01 onward stays closed.
- Six attempts: daily-sma50 on each symbol with passive-entry offsets of 5bp and 10bp below the signal-day close.
- Signal: after UTC day t closes, desired state is long when close_t is strictly above the trailing 50-day SMA including t, otherwise flat.
- Entry: when flat and the signal at t is long, place a post-only buy limit at close_t * (1-offset). During day t+1 it fills only if low_(t+1) <= limit. If filled, entry price is the limit and the position earns close_(t+1)/limit-1 for that day. If unfilled, remain flat; after t+1 closes, cancel and recompute a new one-day order from close_(t+1) if its signal remains long.
- Exit: when long and the signal at t is flat, exit at close_t. The t close-to-close return is earned before that exit. No return after exit until a later maker fill.
- Costs: maker entry fee 0bp; taker exit fee 5bp deducted on exit. This isolates maker-entry execution while retaining conservative paid exits. No rebates. Initial entry has no extra fee.
- Accounting: one position maximum, long/flat, no leverage. Signals use closed bars only. No credit for a bar before an entry fills. Missing or incomplete UTC days are excluded and break continuity; no forward filling.

## Gates

Same portfolio gates as batches 6-9: at least 500 observed exploration days; annualized Sharpe >= 1.0 using sqrt(365) and sample standard deviation; positive arithmetic annualized return; max drawdown no worse than -25%; PSR versus zero >= 0.95 using the same estimator; average entries plus exits <= 2.0 per day; second-process rerun matches exactly.

Every attempt will be reported with dataset and report SHA-256 checksums. No exploration failure opens validation.
