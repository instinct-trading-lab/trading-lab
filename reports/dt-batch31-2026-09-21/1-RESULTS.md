# Batch 31: robustness of the batch-30 dow2-btcusdt pass

Predeclaration committed before any execution (raw-file SHA-256 `4664aca139f115bd077d9d5be6bbed6ffb3f0a7823944263b66ad3261269d866`). Identical engine to batch 30, full dataset span 2022-06-01..2025-12-31 (1308 trading days after dropping the first day, which has no prior close). Independent second-process rerun matched byte for byte.

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Days | Verdict |
|---|---:|---:|---:|---:|---:|---|
| A-dow2-btcusdt-fullspan-5bp | 17.59% | 0.826 | -21.99% | 0.9437 | 1308 | FAIL |
| B-dow2-btcusdt-fullspan-10bp | 12.37% | 0.581 | -24.27% | 0.8672 | 1308 | FAIL |
| C-dow2-ethusdt-fullspan-5bp | 24.51% | 0.831 | -28.94% | 0.9467 | 1308 | FAIL |
| D-dow2-solusdt-fullspan-5bp | 17.77% | 0.411 | -64.90% | 0.7721 | 1308 | FAIL |

## Verdict

**Decisive attempt A FAILS: the package is dead, and with it the calendar family.** On the full 3.5-year span, Wednesday-only BTC earns Sharpe 0.826 / PSR 0.9437 - both below gate - versus Sharpe 1.169 / PSR 0.9655 on the 2024-2025 exploration window. The batch-30 pass was a window artifact, exactly the failure mode the robustness step exists to catch. Supporting attempts confirm: doubling costs drops Sharpe to 0.581; ETH misses the drawdown gate (-28.9%); SOL is far below all gates (Sharpe 0.411). Per the predeclared decision rule this family is closed with no validation attempt earned. 169 exploration + 6 robustness attempts to date; 2 validation attempts; 0 surviving packages.
