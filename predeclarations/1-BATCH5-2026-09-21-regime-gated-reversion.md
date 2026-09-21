# Batch 5 predeclaration: volatility/trend-regime-gated reversion

Locked before any data execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before the dataset for this batch is fetched or any batch-5 code is run.

## Question

Batch 3 showed the only families with positive zero-cost medians were the two extreme-reversion families, and proposed direction D4: restrict reversion to range-bound regimes. Batch 4 showed that simply slowing reversion down does not create a cost-bearing edge. Batch 5 asks: does gating the same reversion idea on a fixed, predeclared range/trend regime filter produce an edge that survives 5bp/side costs?

## Fixed design

- Public market data: Binance.US hourly candles for BTCUSDT, ETHUSDT and SOLUSDT.
- Exploration window: 2024-01-01 through 2025-12-31 UTC.
- Untouched validation window: 2026-01-01 onward. It will be opened only for exploration survivors, and any validation pass remains a research result, not authorization to trade.
- Six exploration attempts: two signal families on each of the three symbols.
- Cost: 5bp per position change. No zero-cost sibling is part of this batch.
- Accounting: signals computed only from closed bars; position decided at bar t applies to the return of bar t+1 (next-bar accounting); equity compounds hourly; daily returns are compounded from hourly strategy returns. Long/flat only (spot-realistic; no shorting, no leverage).

## Regime filter (fixed, no tuning after this commit)

At bar t, using only bars up to and including t:

- RANGE regime when abs(ln(close_t / close_{t-168})) <= 0.10 (trailing 7-day absolute log move at most 10%).
- TREND regime otherwise.
- Entries are allowed only while in RANGE. An open position is exited on the next bar if the regime flips to TREND.

## Signal definitions (fixed)

- rsi2-gated: RSI with period 2 on hourly closes. Enter long when in RANGE and RSI <= 10. Exit when RSI >= 60, or after 120 hours in position, or on regime flip.
- vwaprev-gated: rolling 168-hour VWAP over typical price (high+low+close)/3, volume-weighted. Enter long when in RANGE and close < VWAP * 0.97. Exit when close >= VWAP, or after 168 hours in position, or on regime flip.

Implementation details and reconstructive parameters beyond this file remain private under the repository's reports-only boundary.

## Gates

An exploration attempt passes only if all are true:

1. at least 500 observed trading days;
2. annualized Sharpe >= 1.0;
3. positive arithmetic annualized return;
4. maximum drawdown no worse than -25%;
5. probabilistic Sharpe ratio versus zero >= 0.95;
6. average position changes <= 2.0 per day;
7. independent rerun matches the committed statistics exactly.

Every attempt, pass or fail, will be reported. Dataset SHA-256 checksums are recorded per attempt.
