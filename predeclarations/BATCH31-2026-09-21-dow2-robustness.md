# Batch 31 predeclaration: robustness of the batch-30 dow2-btcusdt pass

Locked before any batch-31 execution on 2026-09-21 (Asia/Jerusalem). Batch 30 produced exactly one exploration pass in a fixed 21-attempt grid: dow2-btcusdt (Wednesday-only long, BTC). Per lab rule, an exploration pass earns predeclared robustness follow-ups, not validation. This batch is that robustness check. Data: the same batch-19 Binance.US hourly files (SHA-256 re-recorded, already re-verified byte-identical against the published batch-19 checksums in batch 30). No new data is fetched. This earns at most one validation attempt; the 2026+ window stays closed regardless of outcome.

## Fixed design

Identical engine and mechanics to batch 30 (position 1 iff UTC weekday = Wednesday; day-t return = position x close-to-close; cost per position change as stated per attempt; gates on the daily series: Sharpe >= 1.0 with sqrt(365), positive arithmetic annualized return, MDD no worse than -25%, PSR >= 0.95, >= 500 observed days, <= 2 position changes/day, byte-exact twin rerun). The only change is the span and the cost stress:

- Attempt A (decisive): dow2-btcusdt over the FULL dataset span 2022-06-01..2025-12-31 (1309 days), 5bp per change.
- Attempt B (cost stress): dow2-btcusdt, full span, 10bp per change.
- Attempt C (cross-symbol): dow2-ethusdt, full span, 5bp.
- Attempt D (cross-symbol): dow2-solusdt, full span, 5bp.

## Decision rule (fixed a priori)

The package stays alive only if attempt A passes every gate on the full span. B, C, D are supporting evidence reported in full; they cannot rescue a failed A, and their own failures do not by themselves kill a passed A (they inform the validation design). If A passes, the package earns exactly one predeclared validation attempt on the 2026+ window. If A fails, the calendar family is dead and that concludes it. No rounding up of near-misses.

## Rules

Report files only under reports/dt-batch31-2026-09-21/ with SHA-256 checksums, twin-run verification, and fresh-clone verification.
