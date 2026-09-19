# Branch competition: main-pipeline vs cursor

Set up 2026-09-19 at Bar's instruction.

- `main-pipeline`: experiments run by the main trading pipeline.
- `cursor`: experiments run by the Cursor CLI agent.

Both branches follow the same evidence rules as `main`: one commit per real
attempted run, with predeclaration, source data or checksum, code, exact results,
reproduction evidence and timestamps. No empty commits.

The score is the count of experiments that pass their predefined acceptance and
reproduction gates - not commit count, not run count. Rejections are committed
and stay visible on both branches.
