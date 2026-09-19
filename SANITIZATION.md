# Sanitization record (2026-09-19)

Policy (owner directive): the public repository exposes reports only - no source code, executable research code, raw datasets, credentials, or reconstructive strategy implementation, in current files or in Git history.

Actions taken:
1. Full private archive created BEFORE any removal: complete git bundle of all 3 branches and 1,698 commits (every experiment, all code, all raw data, all evidence). Stored privately outside GitHub; bundle SHA-256 294aa68ad2d2ae52d642b9996f577db73e3c863adf19ebe1b635d25f641d64c1.
2. main-pipeline history rewritten (force-push) to a reports-only tree: 1,675 per-run report JSONs with original commit SHA+timestamp provenance, scoreboard, errata, methodology (non-reconstructive), dataset checksums. Head: 8e8eae2a83b58773e52d6ea9e6fd94f7f2c377b5.
3. Verification then showed GitHub still served ALL removed content unauthenticated via dangling objects (old commit URLs, raw file URLs, codeload zips all HTTP 200). A force-push cannot purge that.
4. The repository was therefore DELETED and RECREATED empty, and only sanitized branches were pushed back. The historical import on main/cursor also contained code and a raw dataset zip; those branches were rebuilt reports-only as well (cursor: sanitized import; main: sanitized import + framework catalog docs).
5. Post-recreation unauthenticated verification: repo page, old commit URLs, raw code URLs, raw dataset URLs, and archive zips of prior heads all return 404.

Truthful counts are unchanged: 1,698 historical commits (preserved privately), 921 corrected attempts + 3 validations (batch-3), 686 preserved invalid attempts (ERRATA E1), 65 batch-1 validations. Cursor branch belongs to a separate worker; its future work is unaffected - the branch was restored with report-level content identical to its prior public state minus code/data.

Verification addendum: at first post-recreation check, exactly two raw.githubusercontent.com URLs (lab/dt_runner2.py and datasets_dt/BTCUSDT_15m.csv at the prior head 41b667e) still returned 200 from CDN edge cache because they had been fetched minutes before deletion; every never-before-requested old path returned 404 immediately. The cached pair is expected to expire with CDN TTL and is re-checked after each sanitization-related run. No forks/stars/watchers existed, so no external GitHub copies were made.

Final verification (2026-09-19 14:05 IDT): the two CDN edge-cached URLs (lab/dt_runner2.py and datasets_dt/BTCUSDT_15m.csv at prior head 41b667e) now return 404. No unauthenticated path to removed code or raw datasets remains: branches, tags (none existed), old commit URLs, raw file URLs, API blob/commit access, and downloadable archives all verified purged.
