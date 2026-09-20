# Independent verification of the public batch-3 reports (2026-09-20)

Scope: read-only recomputation from the 924 JSON reports currently committed under `reports/dt-batch3-2026-09-19/`. This is an analysis artifact, not a new experiment. It does not inspect private strategy parameters, alter a predeclaration, or consume an attempt.

## Integrity and completeness

- Public files checked: **924** = **921 exploration attempts + 3 validation attempts**.
- Exploration grid is balanced by cost: **307 at 0bp, 307 at 5bp/side, 307 at 10bp/side**.
- Every one of the 924 reports records `reproduction_match: true`.
- SHA-256 of the lexicographically path-sorted `sha256sum` manifest for the 924 report files: `e57e890a0fae257bdfdb77776d48bde44f2860b03c14b09b42ed38bb2ae7c962`.

The manifest digest above is independently reproducible from this checkout with:

```sh
sha256sum reports/dt-batch3-2026-09-19/*.json | LC_ALL=C sort -k2 | sha256sum
```

## Recomputed exploration result

| Cost | Attempts | PASS | Median annualized Sharpe | Positive-Sharpe attempts |
|---:|---:|---:|---:|---:|
| 0bp | 307 | 3 | -0.089932 | 123 |
| 5bp/side | 307 | 0 | -1.177309 | 31 |
| 10bp/side | 307 | 0 | -2.269452 | 15 |

This independently confirms the batch-3 audit's load-bearing result: **0/614 nonzero-cost attempts passed**. A positive gross-looking result alone was not enough to clear the predeclared gates, and realistic taker costs shifted the median sharply negative.

## Zero-cost family medians

| Family | Attempts at 0bp | Median annualized Sharpe |
|---|---:|---:|
| dow | 11 | -0.279148 |
| emax | 44 | -0.049568 |
| fade | 18 | -0.028248 |
| gapfade | 44 | 0.000000 |
| mom | 18 | -0.315301 |
| nr7 | 3 | -0.275941 |
| orb | 27 | -0.390484 |
| pdbreak | 9 | -0.226677 |
| rsi2 | 12 | 0.180477 |
| sweep | 33 | -0.557881 |
| volspike | 44 | -0.109656 |
| vwaprev | 44 | 0.194469 |

Only `rsi2` and `vwaprev` have positive zero-cost family medians, both below 0.20. No tested family therefore shows a systematic 15-minute gross edge in the public results.

## Validation readback

The three untouched-window validation reports are:

- `vr10200`, rsi2 / SOLUSDT / 0bp: **PASS**, Sharpe 1.931498, PSR 0.951636.
- `vr10201`, rsi2 / SOLUSDT / 0bp: **FAIL**, Sharpe 1.177413, PSR 0.849938.
- `vr20840`, emax / ETHUSD_CB / 0bp: **FAIL**, Sharpe -0.042873, PSR 0.485547.

The sole validation survivor is a zero-cost research lead. Its existence does not overturn the 0/614 result after nonzero costs and is not evidence of a tradeable strategy.

## Decision boundary

Batch 4 has not been started. The five directions in `AUDIT-2026-09-20-batch3-analysis.md` remain proposals only and require an explicit predeclaration decision before any new competition attempt.
