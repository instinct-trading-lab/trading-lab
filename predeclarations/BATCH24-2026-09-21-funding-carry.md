# Batch 24 predeclaration: funding carry (market-neutral, funding-transfer returns)

Locked before any batch-24 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any perpetual mark-price data is fetched or any batch-24 code is run. The 2026+ validation window remains closed.

## Question and mechanism

Every directional family is dead; batch 23 showed extreme funding marks strong trends, not flushes. Batch 24 tests the construction that does not predict price at all: when funding is persistently high, crowded perp longs pay shorts every 8 hours, and a delta-neutral position (long spot, short perp, equal notional) collects that transfer with only basis noise. Returns come from the funding mechanism itself.

## Cross-venue construction and conventions (explicit)

- Spot prices: Binance.US hourly BTCUSDT/ETHUSDT/SOLUSDT (batch-19 dataset). Perp mark prices and funding: Binance.com USD-M perpetual public data archive. The venues differ, so the hedge carries cross-venue basis noise in addition to same-venue basis risk; this is an approximation of the same-venue carry trade and is predeclared as such.
- Capital convention: one unit of capital supports one unit of notional on each leg (spot holding cross-collateralizes the short perp). Returns are computed per unit of capital so defined. No leverage beyond this.
- Funding convention: while held, the short perp collects the recorded funding rate at each 8h timestamp on notional (positive rate = short receives).

## Fixed design

- Data: batch-19 spot dataset (SHA-256 recorded); Binance.com public markPriceKlines hourly and fundingRate monthly archives for the same symbols, 2023-12-01 through 2025-12-31, fetched fresh after this commit (SHA-256 recorded). Aggregation: complete UTC daily bars, 24 hourly records required. No forward fill.
- Entry: at UTC close t, when flat, if the trailing 7-day funding mean f_t (as defined in batch 23) is strictly greater than 0.0005 (5x the 0.01% baseline), enter at close t: long spot + short perp, equal notional, 5bp taker on each leg (10bp total on capital).
- Exit: at UTC close t, when held, if f_t <= 0.0001 (the baseline), exit both legs at close t (another 10bp on capital). The normalization rule is fixed a priori.
- Daily held return: (spot close-to-close return) - (perp mark close-to-close return) + (sum of the day's recorded funding rates).
- Exploration window: 2024-01-01 through 2025-12-31 UTC; earlier data is warm-up only. Three attempts: one per symbol. Position-events gate interpretation: an event day is a day on which the combined position changes state (enter or exit); the two legs of one state change count as one event.

## Gates

Identical thresholds to batches 14-23: >= 500 observed days; annualized Sharpe >= 1.0 (sqrt(365), sample standard deviation); positive arithmetic annualized return; max drawdown no worse than -25%; PSR >= 0.95 (same estimator); <= 2.0 event days per day; byte-exact independent rerun.

Every attempt, pass or fail, will be reported with dataset and report SHA-256 checksums. A failure does not open validation; a pass earns exactly one predeclared validation attempt. If the construction cannot be modeled honestly from public data, the batch reports the blockage instead.
