# Batch 24: funding carry (market-neutral, funding-transfer returns)

Predeclaration committed before any perp-data fetch or execution as its predeclaration commit on `main-pipeline` (14:11 IDT sequence: predec commit, then mark-price fetch). Three attempts held long spot + short perp (equal notional) whenever the 7-day funding mean exceeded 5x baseline, collecting recorded 8h funding, 2024-2025 exploration only. Independent output matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Entries/Exits | Verdict |
|---|---:|---:|---:|---:|---:|---|
| fundcarry-btcusdt | 1.29% | 1.704 | -0.47% | 0.9916 | 1/1 | PASS |
| fundcarry-ethusdt | 1.44% | 2.079 | -0.28% | 0.9997 | 1/1 | PASS |
| fundcarry-solusdt | 2.13% | 1.430 | -0.62% | 0.9872 | 1/1 | PASS |

## Verdict

**3/3 passed the predeclared exploration gates.** Each symbol traded exactly once (one entry, one exit): the position collected 3.0-4.5% total funding with sub-1% drawdown while held, and sat in cash otherwise.

## Methodology caveat (why validation stays closed)

The perp leg uses MARK price klines, which are a smoothed index composite, not tradable prices. Smoothing can understate hedge noise and inflate Sharpe/PSR. Before any validation, batch 25 will rerun this exact construction with perp TRADE-price klines as a predeclared robustness check. The pass is real per the predeclared spec; it is not yet a robust pass. Also note each attempt is a single round-trip - fragile evidence by construction. Not a live strategy.
