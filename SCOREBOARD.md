# Day-trading batch scoreboard (main-pipeline)

Performer: Instinct trading-lab agent (main-pipeline branch owner)
Batch: experiments/dt-batch-2026-09-19 | Spec: lab/dt_spec.json | Data: datasets_dt/ (SHA256SUMS.txt, Binance.US 15m, from 2024-01-01)

## Counts
- Predeclared attempts (exploration, <=2025-12-31): 261 (dt000..dt260), one pushed commit each
- Exploration PASS (predeclared gates in lab/dt_spec.json): 65
- Validation attempts on UNTOUCHED 2026+ data: 65 (v-series, one commit each, pass or fail)
- Validation PASS: 64 | Validation FAIL: 1 (v058/dt058)

## Gates (predeclared before any run)
Exploration: min 180 trading days, Sharpe >= 1.0, max drawdown >= -25%, positive total return, net of 0/5/10bp per-side costs.
Validation: same thresholds recomputed on data never touched during exploration scoring.

## Honest caveats
- 2024-2026 was a strongly trending crypto tape; long-side breakout classes (orb, pdbreak) inflate absolute Sharpes. 64/65 validation survival means the gates discriminate weakly in a bull market, not that all 64 are economically distinct edges.
- No multiple-testing correction applied yet (batch-2 predeclaration adds a PSR>=0.95 screen and deflated-SR reporting).
- Reproduction evidence = independent re-parse of the CSV plus the same strategy code, re-derived results must match committed results exactly (method disclosed in lab/dt_spec.json).
- Strategy classes so far: orb, fade, pdbreak, mom, rsi2, nr7 x BTCUSDT/ETHUSDT/SOLUSDT x 3 cost levels. More economically distinct classes to come.


---

# CORRECTED batch dt-batch3-2026-09-19 (engine daily_net_v2, ERRATA E1)

The batch-1/batch-2 numbers above are INVALID as scored (one-bar lookahead, see ERRATA.md). Corrected rerun:

- Attempts: 921/921 executed and committed (r1-series = batch-1 grid, r2-series = batch-2 grid), one commit each, failures preserved
- Reproduction mismatches: 0
- Exploration survivors (gates + PSR>=0.95): 3 - emax ETHUSD_CB 0bp (Sharpe 2.27), rsi2 SOLUSDT 0bp x2 (Sharpe 1.64, 1.79). NO survivor at any nonzero cost.
- Untouched 2026+ validations: 1 PASS / 3 - rsi2 SOLUSDT (5,95) h=2 0bp Sharpe 1.93. FAIL: rsi2 (10,90) h=2 (1.18, PSR screen), emax ETHUSD_CB (-0.04).
- Net: exactly ONE configuration survives end-to-end, at 0 cost only. Its 5bp and 10bp siblings failed exploration, so it is not yet evidence of a tradeable edge after costs.
