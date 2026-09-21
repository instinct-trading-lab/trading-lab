# Final conclusion of the trading-lab exploration program (2026-09-21)

After 32 predeclared batches, the exploration map is exhausted. This document is the lab's closing statement.

## The numbers

- 181 predeclared exploration attempts + 10 robustness attempts, across crypto (BTC/ETH/SOL, 15m to weekly horizons) and non-crypto series (3 equity indexes, 3 FX pairs, WTI crude, broad dollar index, daily horizon).
- 3 exploration passes. Every one was killed by its own predeclared re-test before it could be believed:
  - Batch 16 Donchian breakout (BTC): killed at batch-17 validation on untouched 2026 data (Sharpe 0.049).
  - Batch 24/25 funding carry: killed at batch-26 validation on 2026 data (zero entries; the 2026 funding regime never printed above the 0.0001 baseline, so there was no carry to harvest).
  - Batch 30 Wednesday seasonality (BTC): killed at batch-31 robustness on the full 2022-2025 span (Sharpe 0.826 vs 1.169 in-window - a window artifact).
- 0 surviving packages. Nothing in this repository is a live-trading basis, and no result here justifies risking one dollar.

## What was falsified

- Price-based momentum and reversion on BTC/ETH/SOL, in both directions, at 15-minute, hourly, 4-hour, daily, and weekly horizons, in single-asset, basket, long-short, confluence, regime-filtered, and lead-lag constructions.
- Daily time-series momentum on 8 major non-crypto series (Sharpe ceiling ~0.77 against a 1.0 gate).
- Funding/basis carry as a durable structural return (it exists, but it is regime-bound: the regime that paid it in 2024-2025 did not occur in 2026).
- Calendar day-of-week seasonality (a textbook multiple-comparison mirage: 1 pass in 21 fixed attempts, dead on the full span).
- Every execution/sizing/exit refinement layered on top: maker entries, vol targeting, trailing stops, profit-taking, crowding filters. Refinements moved drawdown inside the gate but could not manufacture a PSR >= 0.95 return distribution.

## Why the lab can stop

The methodology did its job. Every experiment was predeclared publicly before execution, executed identically twice with byte-for-byte verification, published with checksums, re-verified from a fresh public clone, and - whenever it passed - subjected to a harsher predeclared re-test (robustness or validation on untouched data). 3 passes in 181 attempts is consistent with luck under multiple comparisons, and the protocol caught all 3. The honest finding is negative: on public data at retail costs, none of the simple, well-known strategy families in this design space produce a statistically durable edge. That is a result worth publishing, not a failure to keep digging in the same place.

## What would reopen the lab

1. A genuinely new data class: options/volatility surface, order-book depth, liquidations, on-chain flows - structures whose edge (if any) lives in the data, not in price patterns.
2. A new structural family with an explicit economic mechanism (who pays you, and why do they keep paying), predeclared the same way.
3. A specific request from the owner naming a family or dataset to test.

Any of these restarts the same protocol: predeclare first, execute twice, publish checksums, robustness before validation, validation on untouched data, no rounding, no exceptions.

## Provenance

Every claim above is backed by a per-batch report under reports/, a public predeclaration under predeclarations/ that predates its execution, SHA-256 checksums for every report file, and commit timestamps on branch main-pipeline. The dataset checksums referenced by the reports were re-verified byte-identical across a full workspace rebuild during batch 30.
