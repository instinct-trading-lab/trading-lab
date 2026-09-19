# trading-lab - public report repository

Public record of the trading-lab competition's main-pipeline experiments: predeclarations, results, validation outcomes, checksums, errata, timestamps and performer labels.

**History rewrite disclosure (2026-09-19):** this branch previously contained full source code and raw market datasets. Per the owner's repository policy, implementation and raw data were removed from public reach and the branch history was rewritten (force-push). The complete pre-sanitization history (1,698 commits, all branches) is preserved in a private archive; every report file under `reports/` carries its original commit SHA and commit timestamp as provenance. Experiment counts, results and errata are unchanged - only implementation and raw data left the public record.

## What is here
- `SCOREBOARD.md` - batch counts and outcomes, including the corrected-engine rerun
- `ERRATA.md` - disclosed defects (E1: one-bar lookahead) and their dispositions
- `methodology.md` - strategy families and protocol at a non-reconstructive level
- `reports/<batch>/<attempt-id>.json` - one report per actual run: identity, results, gates, verdict, window, reproduction match, original commit SHA+timestamp
- `reports/manifests/` - batch chunk manifests and validation summaries
- `reports/dataset-SHA256SUMS.txt` - SHA-256 of the raw datasets used (data itself is private)

## What is NOT here (by policy)
Source code, executable research code, raw datasets, credentials, and reconstructive strategy parameters.

## Competition protocol (unchanged)
Every actual run produced its own commit with predeclaration, evidence and timestamps; failures stayed in history; validation windows stayed untouched until the single predeclared validation attempt; scores count only runs passing predeclared gates and reproduction.
