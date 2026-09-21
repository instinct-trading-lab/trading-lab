# Batch 28: non-crypto daily time-series momentum (exploration)

Predeclaration committed before any full-history fetch or execution (raw-file SHA-256 `85ec593e1b17e9b90fc60e488bf26560b6afb0be58871d2555694bb29a839290`). 8 FRED public series (3 equity indexes, 3 FX pairs, WTI crude, broad dollar) x 2 lookbacks (126/252 published days) = 16 fixed attempts, long-flat, 10bp per position change, Sharpe annualized with sqrt(252) as predeclared. Window 2018-01-01..2025-12-31 per each series' own calendar (~2,000 days per attempt). No 2026+ row read by the engine. Independent second-process rerun matched byte for byte. Buy-and-hold sanity checks reproduced known window returns (SP500 +153.9%, NASDAQCOM +231.7%, DCOILWTICO -5.2%).

| Attempt | Annualized return | Sharpe | Max drawdown | PSR | Position events | Verdict |
|---|---:|---:|---:|---:|---:|---|
| tsmom126-dcoilwtico | 3.30% | 0.126 | -52.48% | 0.6388 | 79 (0.040/day) | FAIL |
| tsmom126-dexjpus | 0.97% | 0.141 | -18.30% | 0.6539 | 64 (0.032/day) | FAIL |
| tsmom126-dexuseu | -0.67% | -0.144 | -14.79% | 0.3427 | 68 (0.034/day) | FAIL |
| tsmom126-dexusuk | -2.23% | -0.405 | -22.52% | 0.1266 | 87 (0.044/day) | FAIL |
| tsmom126-djia | 2.96% | 0.253 | -30.55% | 0.7616 | 62 (0.031/day) | FAIL |
| tsmom126-dtwexbgs | -0.17% | -0.042 | -10.20% | 0.4534 | 82 (0.041/day) | FAIL |
| tsmom126-nasdaqcom | 12.88% | 0.771 | -23.05% | 0.9837 | 36 (0.018/day) | FAIL |
| tsmom126-sp500 | 6.75% | 0.535 | -20.78% | 0.9320 | 66 (0.033/day) | FAIL |
| tsmom252-dcoilwtico | 1.85% | 0.076 | -51.62% | 0.5848 | 39 (0.020/day) | FAIL |
| tsmom252-dexjpus | 2.06% | 0.275 | -14.66% | 0.7791 | 82 (0.041/day) | FAIL |
| tsmom252-dexuseu | -1.23% | -0.268 | -19.73% | 0.2254 | 52 (0.026/day) | FAIL |
| tsmom252-dexusuk | -0.57% | -0.103 | -16.04% | 0.3856 | 78 (0.039/day) | FAIL |
| tsmom252-djia | 3.18% | 0.242 | -27.17% | 0.7503 | 34 (0.017/day) | FAIL |
| tsmom252-dtwexbgs | 0.08% | 0.019 | -11.48% | 0.5210 | 38 (0.019/day) | FAIL |
| tsmom252-nasdaqcom | 9.17% | 0.484 | -42.80% | 0.9093 | 34 (0.017/day) | FAIL |
| tsmom252-sp500 | 9.27% | 0.640 | -22.10% | 0.9613 | 22 (0.011/day) | FAIL |

## Verdict

**0/16 passed.** The binding gate flips here: with ~2,000 daily observations, PSR is easy (two attempts clear 0.95) but annualized Sharpe never reaches 1.0 - the best are tsmom126-nasdaqcom (Sharpe 0.771, PSR 0.9837, MDD -23.1%) and tsmom252-sp500 (Sharpe 0.640, PSR 0.9613, MDD -22.1%), both clear misses on Sharpe with drawdowns near the gate. FX and the broad dollar are flat to negative; WTI is flat with -52% drawdowns. Classic 6/12-month long-flat momentum after 10bp costs does not produce a gate-passing return distribution on major non-crypto daily series, matching the crypto result at the same horizon. 132 exploration attempts to date; the two remaining open directions narrow to hourly-scale crypto reversion (cost-doubtful a priori) and structured/cross-asset constructions not yet falsified.
