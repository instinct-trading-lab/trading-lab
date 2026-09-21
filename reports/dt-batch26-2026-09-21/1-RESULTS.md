# Batch 26: VALIDATION of the funding-carry package on the untouched 2026+ window

Predeclaration committed before any 2026 data fetch or execution as `ce3d0b6`; window-cap addendum (to 2026-08-30, because September funding is not yet published in any public archive and 2026-08-31 spot is incomplete on Binance.US) committed before any 2026 data fetch or execution as `9e2d0b6`. This is the single validation attempt earned by the batch-24/25 exploration passes, run with the batch-25 trade-price construction, unchanged. Independent second-process rerun matched byte for byte.

Validation window: 2026-01-01 through 2026-08-30 UTC (242 days), per the addendum.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Entries/Exits | Verdict |
|---|---:|---:|---:|---:|---:|---|
| fundcarry-btcusdt | 0.00% | undefined (0 trades) | 0.00% | undefined (0 trades) | 0/0 | FAIL |
| fundcarry-ethusdt | 0.00% | undefined (0 trades) | 0.00% | undefined (0 trades) | 0/0 | FAIL |
| fundcarry-solusdt | 0.00% | undefined (0 trades) | 0.00% | undefined (0 trades) | 0/0 | FAIL |

## Gate 1 (data integrity): PASS

Every complete UTC day of the validation window is present for all three symbols: 242/242 days with 24/24 hourly records for both Binance.US spot and Binance.com perp trade klines, and at least one funding record on every window day (729 funding records per symbol, 3 per day, 2026-01-01..2026-08-31). The only incomplete day found in the fetched span is 2026-08-31 (15/24 hourly records, all symbols) - outside the amended window.

## Why the strategy never entered

The entry rule requires the trailing 7-day mean funding rate strictly above 0.0005 per 8h. In the entire fetched 2026 funding history (2026-01-01..2026-08-31) not a single funding print exceeded 0.0005 on any of the three symbols; the observed maximum print was exactly 0.0001 (the baseline rate), and the maximum trailing 7-day mean was ~0.00009-0.0001. Funding was pinned at or below baseline - and frequently negative - throughout the window. The construction correctly stayed flat; there was simply no carry to harvest in 2026. Data sanity check: 729 records/symbol, per-day coverage complete, values in the expected [-0.0007, 0.0001] range - the zero-entry outcome is a property of the market, not of parsing.

## Verdict

**0/3 passed. The funding-carry package is KILLED**, exactly as the predeclaration requires ("a validation failure kills the package"). The batch-24/25 exploration passes do not generalize to 2026: the funding regime that made the trade pay in 2024-2025 (sustained prints above 5bp/8h) did not occur in the 2026 validation window. Sharpe and PSR are undefined (zero trades, zero variance) and are recorded as null, not rounded or imputed. The funding-carry family is closed. 108 exploration attempts + 2 validation attempts to date; the lab moves to the next predeclared exploration batch.
