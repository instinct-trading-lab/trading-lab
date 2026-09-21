# Batch 6 predeclaration: higher-timeframe trend

Locked before any batch-6 data execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before the batch-6 dataset is fetched or any batch-6 code is run.

## Question

The batch-3 audit found slow trend variants degraded least under costs (slowest moving-average pair median -0.05 vs fastest -4.67), and direction D2 proposed moving trend families off the fatal 15m churn. Batch 5 closed out the reversion direction. Batch 6 asks: do slow trend signals on aggregated higher-timeframe bars retain an edge after 5bp/side costs?

## Fixed design

- Public market data: Binance.US hourly candles for BTCUSDT, ETHUSDT and SOLUSDT, aggregated to higher timeframes.
- Exploration window: 2024-01-01 through 2025-12-31 UTC.
- Untouched validation window: 2026-01-01 onward. It will be opened only for exploration survivors, and any validation pass remains a research result, not authorization to trade.
- Six exploration attempts: two trend families on each of the three symbols.
- Cost: 5bp per position change. No zero-cost sibling is part of this batch.
- Accounting: signals computed only from closed aggregated bars; a position decided at bar t applies to the return of bar t+1 (next-bar accounting); equity compounds per bar; daily returns are compounded from bar-level strategy returns. Long/flat only (no shorting, no leverage).

## Signal definitions (fixed, no tuning after this commit)

- daily-sma50: aggregate hourly bars to UTC daily bars. Long when the daily close is strictly above the 50-day simple moving average of daily closes, flat otherwise.
- h4-golden: aggregate hourly bars to aligned 4-hour UTC bars (00, 04, 08, 12, 16, 20). Long when the 50-bar SMA of 4h closes is strictly above the 200-bar SMA of 4h closes, flat otherwise.

Both families are deliberately plain, widely published trend definitions; nothing is fitted to the exploration data.

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
