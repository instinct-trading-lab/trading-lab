# Batch 17 predeclaration: validation of the batch-16 passing package on the untouched 2026+ window

Locked before any batch-17 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any 2026-or-later market data is fetched, parsed, or inspected by any batch-17 code. Batch 16's passing exploration attempt earns exactly one validation attempt; this is it.

## Fixed design

- Package under test: `donchian55-maker10bp-vol35-pt50-btcusdt` exactly as predeclared in batches 13, 14 and 16: 55-day Donchian entry, 27-day exit, 10bp post-only maker entry at 0bp, 5bp exit and resize taker costs, 20-day realized-vol weight w*_t = min(1, 0.35 / vol_t), and partial profit-taking: once per entry, when the close first reaches at least +50% above the fill price, half the current weight is banked to cash at that close (5bp taker on the sold weight); the banked half stays in cash for the rest of that entry and the remainder is vol-managed without regrowing past its post-sale weight.
- Data: public Binance.US hourly BTCUSDT candles, fetched fresh after this commit. Aggregation to complete UTC daily OHLC bars; a day requires all 24 hourly records. No forward fill.
- Validation window: 2026-01-01 through 2026-09-20 UTC (the latest complete UTC day at commit time). Prior data from 2025-08-01 is warm-up only.
- One attempt. No variants, no tuning, no reruns with changed parameters.

## Gates for validation

The exploration window-count gate (500 days) cannot apply to a 263-day window; it is restated as: every complete UTC day in the validation window must be present. All other gates are unchanged:

1. every complete UTC day 2026-01-01 through 2026-09-20 present;
2. annualized Sharpe >= 1.0 using sqrt(365) and the sample standard deviation of daily net returns;
3. positive arithmetic annualized return;
4. maximum drawdown no worse than -25%;
5. PSR versus zero >= 0.95 using the same Bailey-Lopez de Prado skew/kurtosis estimator as batches 4-16;
6. average days per observed day on which the position crosses zero or changes by at least 0.25 of full exposure <= 2.0;
7. an independent second-process rerun matches all committed statistics exactly.

The outcome, pass or fail, will be reported with dataset and report SHA-256 checksums. A validation failure kills the package. A validation pass makes the package a candidate for hostile review in a demo environment; it does not by itself authorize live trading.
