# Batch 5: regime-gated reversion, exploration result

Predeclaration: `predeclarations/BATCH5-2026-09-21-regime-gated-reversion.md`, committed before any data execution as remote commits `7b7fa12` (upload) and `d5c35ed` (filename correction) on 2026-09-21.

Six new exploration attempts were run on public Binance.US hourly candles, 2024-01-01 through 2025-12-31, with 5bp charged per position change and next-bar accounting. Each attempt was rerun in a second independent process with an exact statistics match. Dataset checksums are recorded in each attempt JSON; report-file checksums are in `2-SHA256SUMS.txt`.

Design summary (full fixed spec in the predeclaration): the two batch-3 reversion families (RSI(2) extreme, rolling-168h VWAP), long/flat, active only while the trailing 7-day absolute log move is at most 10% (RANGE regime), exited on regime flip.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Changes/day | Verdict |
|---|---:|---:|---:|---:|---:|---|
| rsi2-gated / BTCUSDT | -20.37% | -1.030 | -41.52% | 0.066 | 2.078 | FAIL |
| rsi2-gated / ETHUSDT | -18.55% | -0.704 | -48.70% | 0.153 | 1.799 | FAIL |
| rsi2-gated / SOLUSDT | -21.09% | -0.734 | -51.07% | 0.143 | 1.674 | FAIL |
| vwaprev-gated / BTCUSDT | 5.82% | 0.262 | -18.36% | 0.644 | 0.248 | FAIL |
| vwaprev-gated / ETHUSDT | -24.08% | -0.787 | -47.67% | 0.128 | 0.358 | FAIL |
| vwaprev-gated / SOLUSDT | -38.64% | -1.049 | -69.44% | 0.069 | 0.591 | FAIL |

## Verdict

**0/6 passed exploration.** Regime gating did not rescue the reversion edge: five of six attempts lost money outright at 5bp/side, and the only positive return (VWAP reversion on BTCUSDT, 5.82% annualized) carries a Sharpe of 0.26 and PSR 0.64, far below the gates. The untouched 2026+ validation window was not opened.

Combined with batch 4, both reversion families have now failed exploration under realistic taker costs in their fast (batch 3), slowed (batch 4) and regime-gated (batch 5) forms. The reversion direction at the hourly horizon should be considered exhausted; remaining grounded directions from the batch-3 audit are higher-timeframe trend (D2) and maker-entry execution modeling (D3).

This is new experimental work and a negative result. It provides no basis for live trading.
