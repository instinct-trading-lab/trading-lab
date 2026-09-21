# Batch 26 predeclaration: validation of the funding-carry package on the untouched 2026+ window

Locked before any batch-26 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any 2026-or-later funding, perp, or new spot data is fetched, parsed, or inspected by batch-26 code. The batch-24/25 passes earn exactly one validation attempt; this is it.

## Fixed design

- Package under test: the batch-24/25 funding-carry construction exactly as predeclared there, with the batch-25 trade-price perp leg: enter long spot + short perp (equal notional, 5bp taker per leg) at UTC close t when the trailing 7-day funding mean is strictly above 0.0005; exit both legs at close t when it falls to or below 0.0001; while held, daily return = spot close-to-close return - perp trade-price close-to-close return + the day's recorded funding sum; one unit of capital per unit of notional per leg.
- Data, fetched fresh after this commit from the same public sources (Binance.US spot hourly; Binance.com archive perp trade-price hourly and funding history): coverage 2025-12-01 (warm-up) through 2026-09-20 UTC (the latest complete UTC day at commit time). SHA-256 recorded per file. The batch-17 BTCUSDT spot file (SHA-256 9b790c5ff230a4886a86874228411374b141c1f63de1ce43fa7bc6a114194494, covering 2025-08-01 onward) may be reused for BTCUSDT warm-up; its checksum will be re-recorded.
- Validation window: 2026-01-01 through 2026-09-20 UTC. Three attempts: BTCUSDT, ETHUSDT, SOLUSDT. No variants, no tuning.

## Gates for validation

The 500-day exploration gate is restated as: every complete UTC day in the validation window must be present. All other gates are unchanged: annualized Sharpe >= 1.0 (sqrt(365), sample standard deviation); positive arithmetic annualized return; max drawdown no worse than -25%; PSR >= 0.95 (same estimator); <= 2.0 event days per day; byte-exact independent rerun. A symbol passes only if all gates hold for that symbol; the package passes only if at least the BTCUSDT attempt passes (the venue's deepest market) - stated a priori so the outcome cannot be cherry-picked.

The outcome, pass or fail, will be reported with dataset and report SHA-256 checksums. A validation failure kills the package. A validation pass makes the package a candidate for hostile review in a demo environment; it does not by itself authorize live trading.
