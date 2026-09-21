# Batch 26 Predeclaration ADDENDUM: validation window capped at 2026-08-30

Original predeclaration: predeclarations/BATCH26-2026-09-21-validation-funding-carry.md (committed before any data fetch or execution). This addendum is committed before any validation-window data fetch or execution and narrows only the window end; every other term stands unchanged.

Reason:
1. The Binance public data archive (data.binance.vision) publishes funding-rate history only as monthly files. Monthly funding files exist through 2026-08; there is no daily fundingRate tree in the archive, and premiumIndexKlines do not carry funding rates (verified 2026-09-21 by S3 prefix listing and direct file inspection). September 2026 funding rates therefore cannot be sourced from any public archive today. fapi.binance.com is geo-blocked (HTTP 451) from this workspace.
2. Binance.US spot hourly data for 2026-08-31 is incomplete (BTC: 15 of 24 hourly records), so the last fully complete spot day in the archive is 2026-08-30.

Amended term:
- Validation window: 2026-01-01T00:00:00Z through 2026-08-30T23:59:59Z (was 2026-09-20). Gate 1 (data integrity: every complete UTC day in the window present, funding present on every day) is unchanged and now applies to this capped window.

Everything else - strategy rule, data sources, fee/funding handling, gates (Sharpe >= 1.0, PSR >= 0.95, MDD >= -25%, no rounding), twin-run byte-identity, publish protocol - is exactly as predeclared. This addendum was written and committed without looking at any 2026 result.
