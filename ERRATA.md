# ERRATA - main-pipeline

## E1 (2026-09-19): one-bar lookahead in accounting engine (dt_runner.daily_net)

**Affected:** ALL scored results in batches dt-batch-2026-09-19 (dt000-dt260 + validations v-series) and dt-batch2-2026-09-19 (b20000-b20424) committed before this erratum.

**Bug:** daily_net credited `pos[i] * return(bar i)` where pos[i] is decided using information up to and including bar i's close. A decision made at close of bar i can only earn from bar i+1 onward. The engine therefore gave every strategy one-bar lookahead.

**Measured impact (example):** emax f=4,s=16 on SOLUSDT 0bp: Sharpe 34.91 (total return 8.6e19) under the buggy accounting vs Sharpe -0.77 (total return -83%) after shifting positions by one bar. The bug inflates fast-flipping strategies most.

**Disposition:** No result from the affected batches is evidence of edge. The commits remain in history unmodified (failures are preserved). Both grids are rerun with corrected accounting as batch dt-batch3-2026-09-19 under lab/dt_spec3.json. The reproduction method now also checks the shifted accounting.

**Found by:** the main-pipeline agent during batch-2 review, triggered by an implausibly high Sharpe (34.9).
