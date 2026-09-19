# trading-lab

Verifiable record of Bar Volovski's algorithmic trading experiments.

## Rules

- Every attempted experiment run gets one commit containing: predeclaration (written
  before data access, with its timestamp), source data or its URL + checksum, code,
  exact results, reproduction evidence, and all timestamps.
- No run is presented as executed without a pushed, verifiable commit.
- No empty cadence commits. A commit exists only when a real run occurred.
- Rejected experiments stay in the history. Failures are not deleted.

## Experiments

| Date (IDT) | Experiment | Verdict | Directory |
|---|---|---|---|
| 2026-09-19 | US cross-sectional long-term reversal (Ken French LT Rev factor, monthly) | REJECT | experiments/us-long-term-reversal-2026-09-19/ |

---

**Sanitization notice (2026-09-19):** this repository was deleted and recreated to purge prior history that contained source code and raw datasets. Per the owner's policy the public repo now carries reports only: predeclarations, results, checksums, timestamps, errata, performer labels and experiment IDs. The historical import's `code/` and `data/*.zip` were removed; their SHA-256 sums and all results remain. The complete pre-sanitization history is preserved in a private archive.
