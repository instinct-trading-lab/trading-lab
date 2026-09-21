# Batch 25: funding carry with perp trade prices (robustness check)

Predeclaration committed before any trade-price fetch or execution as `57caa5e`. The identical batch-24 construction with perp TRADE-price klines instead of mark price. Independent output matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Entries/Exits | Verdict |
|---|---:|---:|---:|---:|---:|---|
| fundcarry-btcusdt | 1.30% | 1.654 | -0.50% | 0.9896 | 1/1 | PASS |
| fundcarry-ethusdt | 1.45% | 2.023 | -0.29% | 0.9995 | 1/1 | PASS |
| fundcarry-solusdt | 2.15% | 1.342 | -0.63% | 0.9826 | 1/1 | PASS |

## Verdict

**3/3 passed.** The batch-24 pass is robust: tradable perp prices change Sharpe by only 0.05-0.09 in either direction (BTCUSDT 1.654 vs 1.704; ETHUSDT 2.023 vs 2.079; SOLUSDT 1.342 vs 1.430). The mark-price smoothing concern is resolved - the Binance.US spot / Binance.com perp basis is extremely tight at daily granularity. Per the batch-24/25 predeclarations, the package has earned exactly one predeclared validation attempt on the 2026+ window. Caveats carried from batch 24: single round-trip per symbol; +1.3-2.2% annualized is a low-yield structural trade, not a high-return signal. Not a live strategy.
