# Analysis audit over the 921 corrected batch-3 runs (2026-09-20)

Scope: post-hoc analysis of the 921 corrected-engine attempts (r1/r2) and 3 validations already committed and archived. No new experiments were run. Full per-attempt data and parameter-level detail are in the private archive; this report is deliberately non-reconstructive.

## Headline findings (all grounded in the committed results)

1. **No tested family has a systematic gross edge at the 15m horizon.** At 0 cost, class median annualized Sharpes sit between -0.56 and +0.19 across all 12 families - statistically indistinguishable from noise.
2. **Costs are the dominant killer.** Class medians move from ~0 (0bp) to -1.2 (5bp/side) to -2.3 (10bp/side). Zero of 614 attempts at nonzero cost passed exploration. These intraday strategies churn too much for taker fees: the single validation survivor changes position 14.6 times/day, i.e. ~73bp/day of cost drag at 5bp/side - its 5bp and 10bp siblings failed exploration for exactly this reason.
3. **The survivor is not a statistically validated edge.** Under a null of zero true Sharpe, the Sharpe gate alone would pass ~24 of 307 zero-cost trials by chance; we observed 3 (all gates combined). The best configuration (an RSI-extreme reversion variant on SOLUSDT, 0bp) passes exploration AND untouched-2026+ validation (Sharpe 1.93) and was positive in 10 of 11 calendar quarters, but it cannot carry real-world taker costs at its turnover. It is a research lead, not a tradeable strategy.
4. **Multiple-testing verdict:** with 307 zero-cost trials and a best Sharpe of 2.27, deflated-Sharpe intuition says the family maximum is within luck. Nothing in batch-3 should be traded as-is.
5. **Grounded regularities worth exploiting in future designs:** slower trend variants degraded less than fast ones (slowest moving-average pair median -0.05 vs fastest -4.67 across all cost levels); longer holds hurt less in the sweep family; the only families with positive zero-cost medians are the two extreme-reversion families (RSI-extreme +0.18, session-VWAP reversion +0.19), concentrated on SOL/ETH pairs.

## Directions for the next predeclared batch (proposals, not started)

- D1: low-turnover reversion: the RSI/VWAP reversion families with wider bands and longer holds, targeting under 2 position changes/day so 5bp costs are survivable.
- D2: higher-timeframe signals (hourly/daily aggregation) for trend families - 15m churn is fatal under realistic costs.
- D3: maker/limit-entry execution modeling instead of taker costs, to fairly evaluate high-turnover reversion.
- D4: volatility-regime gating: restrict reversion to range-bound regimes where its zero-cost median was positive.
- D5: deprioritize orb/sweep/mom/fade at 15m - negative medians even at zero cost.

## Method note

Aggregates computed from the committed params/results of all 921 attempts (private archive bundle SHA-256 294aa68ad2d2ae52d642b9996f577db73e3c863adf19ebe1b635d25f641d64c1 verified byte-identical before analysis). Turnover measured from the committed survivor configuration's position series. Null-model expectation assumes independent daily returns (sd of annualized Sharpe over 730 days = sqrt(365/730)).
