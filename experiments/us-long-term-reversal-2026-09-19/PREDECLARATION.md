# Predeclaration: US equity long-term reversal

Created before this run accesses its dataset.

## Thesis
A zero-investment US equity portfolio long stocks with weak returns over the prior multi-year formation period and short prior long-term winners earns a positive net premium as extrapolative mispricing mean-reverts. This cross-sectional long-term reversal experiment is economically distinct from one-month reversal, 12-to-2 momentum, aggregate market timing, value, size, profitability and all FX runs.

## Dataset
Kenneth R. French Data Library monthly Long-Term Reversal Factor (LT Rev), first available month through latest complete month. Select the return column by detecting the sole non-date numeric column under the monthly section, record source member and archive checksum. Fixed source URL in SOURCE.txt.

## Simulation and cost boundary
Use the published monthly LT Rev return without fitted parameters. Subtract 0.15% every month as an assumed all-in implementation drag. It is not measured from security holdings. Evaluate full sample, pre-2000 and fixed January-2000-forward subsample. Annual arithmetic return = mean x 12; annual volatility = sample SD x sqrt(12); zero-financing Sharpe; compounded net CAGR and maximum drawdown.

## Rejection gates
Reject unless all pass net of assumed cost: full Sharpe >= 0.50; January-2000-forward Sharpe >= 0.40; positive monthly net mean both before 2000 and from 2000; full maximum drawdown no worse than -60%. No changes after source access.
