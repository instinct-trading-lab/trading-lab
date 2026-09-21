# Batch 17: validation of the batch-16 passing package on the untouched 2026+ window

Predeclaration committed before any 2026+ data was fetched as `40dd2ad` (14:21:53 IDT; data fetch 14:22 IDT). One attempt, no variants, no tuning. Dataset SHA-256 recorded below. Independent output matched byte for byte.

Missing data: 2026-08-31 has only 15 of 24 hourly records on Binance.US and was excluded under the standing missing-data rule (no forward fill). 262 complete validation days were evaluated; every complete UTC day 2026-01-01 through 2026-09-20 is present.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Days | Verdict |
|---|---:|---:|---:|---:|---:|---|
| validation-donchian55-maker10bp-vol35-pt50-btcusdt | 0.94% | 0.049 | -15.04% | 0.5165 | 262 | FAIL |

## Verdict

**VALIDATION FAILED.** On the untouched 2026-01-01 through 2026-09-20 window the package returned 0.94% annualized with Sharpe 0.049 and PSR 0.5165 (3 entries, 2 exits). Per the predeclaration, this failure kills the batch-16 pt50-BTC package: the exploration pass did not replicate out of sample. The lab's exploration record stands at 1 pass in 78 predeclared attempts, and its validation record at 0 of 1. Nothing is anywhere near live trading; the search continues with new exploration batches.
