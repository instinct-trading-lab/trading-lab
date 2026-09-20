# Batch 4 predeclaration: low-turnover reversion

Locked before execution on 2026-09-20 (Asia/Jerusalem).

## Question

Can the two only batch-3 families with positive zero-cost medians retain an edge after 5bp/side taker costs when redesigned to trade less than twice per day?

## Fixed design

- Public market data: Binance.US hourly candles for BTCUSDT, ETHUSDT and SOLUSDT.
- Exploration window: 2024-01-01 through 2025-12-31 UTC.
- Untouched validation window: 2026-01-01 onward. It will be opened only for exploration survivors.
- Six exploration attempts: one RSI-extreme reversion design and one rolling-VWAP reversion design on each of the three symbols.
- Cost: 5bp per position change. No zero-cost sibling is part of this batch.
- Accounting: signals computed only from closed bars; positions enter on the next bar; daily returns compounded from hourly strategy returns.
- Implementation details and reconstructive parameters remain private under the repository's reports-only boundary.

## Gates

An exploration attempt passes only if all are true:

1. at least 500 observed trading days;
2. annualized Sharpe >= 1.0;
3. positive arithmetic annualized return;
4. maximum drawdown no worse than -25%;
5. probabilistic Sharpe ratio versus zero >= 0.95;
6. average position changes <= 2.0 per day;
7. independent rerun matches the committed statistics exactly.

Every attempt, pass or fail, will be reported. Validation uses the same performance gates on the untouched 2026+ window. A validation pass is still a research result, not authorization to trade.
