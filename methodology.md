# Methodology (non-reconstructive)

Data: public 15-minute candles (Binance.US; Coinbase Exchange as second venue), crypto USDT/USD pairs, from 2024-01-01. Exploration window ends 2025-12-31; validation window 2026-01-01 onward, untouched during exploration scoring. Dataset SHA-256 in reports/dataset-SHA256SUMS.txt.

Strategy families tested (economic intuition only; exact implementations and parameters are private):
- orb: opening-range breakout
- fade / rsi2 / vwaprev: short-horizon mean reversion (bar extremes, RSI extremes, session-VWAP deviation)
- pdbreak / nr7 / volspike: range/volatility breakout (prior-day levels, narrow-range days, volume-confirmed breaks)
- mom / emax: trend continuation (trailing-return sign, moving-average cross)
- gapfade: day-boundary gap reversion
- sweep: prior-day extreme sweep failure (liquidity-grab reversal)
- dow: weekday seasonality with predeclared walk-forward selection

Protocol: one commit per actual run, pass or fail; costs charged per position change at 0/5/10bp per side; gates predeclared (min days, Sharpe floor, drawdown floor, positive mean, PSR >= 0.95 multiple-testing screen); reproduction = independent data re-parse with identical accounting must match committed results exactly. Engine defect E1 (one-bar lookahead) was caught, disclosed in ERRATA.md, and both grids were rerun under corrected accounting; the invalid originals remain listed in the private archive.
