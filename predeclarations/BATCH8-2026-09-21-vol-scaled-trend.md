# Batch 8 predeclaration: volatility-scaled higher-timeframe trend

Locked before any batch-8 data execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any batch-8 code is run. Batch 8 reuses the batch-6 dataset (checksums in reports/dt-batch6-2026-09-21 attempt JSONs); no new data is fetched.

## Question

Batches 6-7 showed the higher-timeframe trend families are positive after costs but fail the -25% drawdown gate, and that a trailing stop does not bind the drawdown. Batch 8 asks the remaining grounded variant: does volatility-scaled position sizing bring drawdown inside the gate while keeping Sharpe >= 1.0 and PSR >= 0.95?

## Fixed design

Same data, symbols, windows, aggregation, next-bar accounting and long-only base signals as batch 6 (daily-sma50 and h4-golden), with position sizing replacing the binary position:

- vol_t = annualized standard deviation of log bar returns over the trailing 20 bars of the same timeframe (daily: x sqrt(365); 4h: x sqrt(2190)).
- exposure_t = min(1, 0.50 / vol_t) when the base trend signal is on, 0 when it is off. Target annualized volatility is fixed at 50%.
- Position decided at bar t applies to bar t+1 (next-bar accounting, unchanged).
- Cost: 5bp x |position_t - position_{t-1}|, charged at the bar where the change applies. This is the same 5bp-per-unit-traded taker model, generalized from binary to fractional exposure; it is predeclared here because batch 6/7 counted changes, not size.
- Daily returns compound from bar-level strategy returns. Equity compounds per bar.

## Gates

Identical thresholds to batches 4-7, with gate 6 defined for fractional exposure as: the average number of bars per day on which the position crosses zero OR changes by at least 0.25 of full exposure must be <= 2.0. Gates: at least 500 observed trading days; annualized Sharpe >= 1.0; positive arithmetic annualized return; maximum drawdown no worse than -25%; PSR versus zero >= 0.95; the turnover gate as just defined; independent rerun matches the committed statistics exactly.

Every attempt, pass or fail, will be reported. Dataset SHA-256 checksums are recorded per attempt.
