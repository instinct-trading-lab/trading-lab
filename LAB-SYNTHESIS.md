# Lab synthesis: the map after 27 batches (2026-09-21)

Status document, not an experiment. Compiled from the per-batch reports in this repository. Gates throughout: annualized Sharpe >= 1.0, positive arithmetic annualized return, max drawdown no worse than -25%, PSR >= 0.95, >= 500 observed days (restated for validation as: every complete UTC day of the window present), <= 2 qualifying position events/day, byte-exact independent rerun. Exploration window 2024-2025 (crypto batches); validation window 2026+ opened exactly twice.

## Scoreboard

- 116 predeclared exploration attempts (batches 1-16, 18-23, 27) plus 6 robustness attempts (batches 24-25, same package re-run on tradable prices).
- 2 exploration passes: batch 16 `donchian55-maker10bp-vol35-pt50-btcusdt` (Sharpe 1.260, PSR 0.9697, MDD -17.95%) and the batch-24 funding-carry package (mark price, confirmed on trade price in batch 25).
- 2 validation attempts on untouched 2026+ data: batch 17 killed the Donchian package (+0.94%, Sharpe 0.049, PSR 0.5165); batch 26 killed the funding-carry package (zero entries - 2026 funding never exceeded the 0.0001 baseline print, max trailing 7-day mean ~0.0001 vs the 0.0005 entry threshold).

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
| Funding/basis carry (market-neutral) | 24-26 | Passed exploration (batch 24) and trade-price robustness (batch 25) on 2024-2025; batch-26 validation on 2026 data: the funding regime vanished (no print above 0.0001 baseline all year), zero entries, package killed. Structural returns exist but are regime-bound and low-yield. |
| Hourly time-series momentum | 27 | 0/9. k=24h strongly negative after costs; k=72/168h positive but far below every gate (best Sharpe 0.446, PSR 0.7401). |

## What the map says

Every long-only or symmetric price-based structure on 2024-2025 BTC/ETH/SOL converges to the same place: Sharpe 0.9-1.1 on BTC (close to BTC beta itself), far less on ETH/SOL, with PSR bounded around 0.91-0.95. The gates demand a distribution, not a return stream, and no execution, sizing, exit-rule, lookback, confluence, regime-filter, or horizon variant produced one that replicated out of sample. Both in-sample PSR crossings (daily Donchian, funding carry) died on 2026 data - one to regime change in price behavior, one to regime change in funding. Crypto price-based momentum/reversion is now falsified at the 15m, hourly, 4h, daily, and weekly horizons on this universe.

## Open directions (not yet falsified)

1. Non-crypto universes (equities, FX, rates, commodities) at daily horizon.
2. Hourly-scale crypto reversion (the k=24h momentum loss in batch 27 implies it; turnover of ~2.3 position changes/day at 5bp makes profitability doubtful a priori, but the family itself is untested).

Nothing in this repository is a live-trading basis. Every claim above is backed by a per-batch report, checksums, and a public predeclaration that predates execution.
