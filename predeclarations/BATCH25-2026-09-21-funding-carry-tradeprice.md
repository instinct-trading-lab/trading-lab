# Batch 25 predeclaration: funding carry with perp trade prices (robustness check)

Locked before any batch-25 execution on 2026-09-21 (Asia/Jerusalem). This file is committed to the remote repository before any perp trade-price data is fetched or any batch-25 code is run. The 2026+ validation window remains closed.

## Question

Batch 24's funding-carry construction passed all gates on all three symbols, but its perp leg used mark-price klines - a smoothed index composite that can understate hedge noise and inflate Sharpe/PSR. Batch 25 reruns the identical construction with perp TRADE-price klines (regular USD-M futures klines, last traded price). If the pass survives the noisier tradable price, the batch-24 result is robust; if it collapses, the mark-price smoothing was the result.

## Fixed design

Identical to batch 24 in every rule, threshold, cost, convention, and gate, with exactly one change: the perp leg's daily close is built from Binance.com USD-M futures TRADE-price hourly klines (public data archive, 2023-12-01 through 2025-12-31, fetched fresh after this commit, SHA-256 recorded) instead of markPriceKlines. Spot prices, funding data, the capital convention, the entry/exit rules, the window, the three attempts (BTCUSDT, ETHUSDT, SOLUSDT), and all seven gates are unchanged from batch 24.

Every attempt, pass or fail, will be reported with dataset and report SHA-256 checksums. A failure does not open validation. A pass, together with batch 24's, earns exactly one predeclared validation attempt.
