# Lab synthesis: FINAL - the map after 32 batches (2026-09-21)

Status document, not an experiment. Compiled from the per-batch reports in this repository. Gates throughout: annualized Sharpe >= 1.0, positive arithmetic annualized return, max drawdown no worse than -25%, PSR >= 0.95, >= 500 observed days (restated for validation as: every complete UTC day of the window present), <= 2 qualifying position events/day, byte-exact independent rerun. Exploration window 2024-2025 (crypto batches), 2018-2025 (non-crypto daily); validation window 2026+ opened exactly twice.

## Scoreboard

- 181 predeclared exploration attempts (batches 1-16, 18-23, 27-30, 32) plus 10 robustness attempts (batches 24-25 same-package re-runs; batch 31 robustness of the batch-30 pass).
- 3 exploration passes: batch 16 `donchian55-maker10bp-vol35-pt50-btcusdt`, the batch-24 funding-carry package, batch 30 `dow2-btcusdt`.
- 2 validation attempts on untouched 2026+ data: batch 17 killed the Donchian package (Sharpe 0.049); batch 26 killed funding carry (zero entries - the 2026 funding regime never printed above the 0.0001 baseline). Batch 30's pass never reached validation: batch 31 killed it at robustness (full-span Sharpe 0.826, PSR 0.9437 - a 2024-2025 window artifact).
- 0 surviving packages. Nothing in this repository is a live-trading basis.

## Dead families (falsified, with the batch that closed them)

| Family | Batches | Conclusion |
|---|---|---|
| Long-term reversal (equities, monthly) | 1-3 | No surviving signal after lookahead bugfix; 0/614 cost-aware passes at 15m horizon. |
| Intraday (15m) reversion | 3-5 | No systematic edge in any family tested. |
| Low-turnover / regime-gated reversion | 4-5 | 0/12. |
| Daily/4h trend (SMA50, golden cross) | 6-8 | Positive after costs, drawdown binds. |
| Trailing stop | 7 | 0/6, drawdown structural. |
| Vol-scaled sizing alone | 8, 14-15 | Moves drawdown inside gate; PSR caps near 0.94. Knob exhausted. |
| Cross-asset relative-strength rotation | 9, 11 | 0/12. |
| Donchian breakout (+ maker entry) | 12-13 | Sharpe 0.988 max; window-and-asset-specific luck per batch 18. |
| Profit-taking / time-exit rules | 16 | pt50 passed exploration once; validation killed it. |
| Slow time-series momentum (26w/52w) | 19 | BTC ~0.96 Sharpe, PSR ~0.91; alts fail. |
| TSMOM basket (diversification) | 20 | Dilutes the strong leg. |
| Long-short TSMOM (free shorts) | 21 | Short side adds nothing. |
| Multi-timeframe confluence | 22 | Sharpe 1.105, MDD -20.83% pass; PSR 0.9449 misses by 0.0051. |
| Funding-crowding regime filter | 23 | Gate removes good days; all metrics worse. |
| Funding/basis carry (market-neutral) | 24-26 | Passed exploration and trade-price robustness on 2024-2025; batch-26 validation on 2026: funding regime vanished (no print above 0.0001 baseline all year), zero entries, package killed. Structural returns exist but are regime-bound and low-yield. |
| Hourly time-series momentum | 27 | 0/9. k=24h strongly negative after costs; k=72/168h positive but far below every gate. |
| Non-crypto daily TSMOM | 28 | 0/16 on 8 FRED series (equity indexes, FX, WTI, broad dollar). Sharpe gate binds: best 0.771 (tsmom126-nasdaqcom). |
| Hourly crypto reversion | 29 | 0/12. Turnover-catastrophic at 1-8h lookbacks; best 24h attempt Sharpe 0.612. Sign-flipping a loser does not mirror it (costs, long-flat constraint). |
| Calendar day-of-week seasonality | 30-31 | 1/21 exploration pass (Wednesday BTC); batch-31 full-span robustness killed it (window artifact). |
| Cross-asset lead-lag (hourly) | 32 | 0/12. Turnover-catastrophic (5.8-12.7 changes/day at 5bp); Sharpe -0.86 to -6.08. The last price-based structure on the map. |

## What the map says

Price-based trading is falsified in BOTH directions (momentum and reversion) at the 15m, hourly, 4h, daily, and weekly horizons on BTC/ETH/SOL, and daily TSMOM is falsified on 8 major non-crypto series. Structural carry exists but is regime-bound and died at validation. Calendar seasonality produced exactly the multiple-comparison mirage it was expected to and died at robustness. Three exploration passes in 169 attempts, none surviving its first honest re-test: the gates demand a distribution, not a return stream, and the market does not owe anyone a simple one.

## Status: EXPLORATION COMPLETE

The map is exhausted. See reports/FINAL-CONCLUSION.md for the closing statement: 181 exploration + 10 robustness attempts, 3 passes all killed by their own predeclared re-tests, 0 surviving packages, nothing live-tradable. The lab reopens only on a genuinely new data class (options/vol surface, order book, on-chain), a new structural family with an explicit economic mechanism, or a specific owner request - all under the same protocol.
