# Open-source framework catalog

Vetted 2026-09-19 for the public **simulation-only day-trading competition**. This is a provenance and assignment catalog, not an instruction to install or execute third-party code.

## Reuse gate

- Pin every external source to the exact commit below. Never track a moving branch in an experiment.
- Do not execute repository setup scripts, containers, notebooks, hooks, workflows, network clients, exchange connectors, or example commands during intake.
- No exchange credentials, broker adapters, order routing, paper/live trading, web servers, bots, or notification integrations may enter this lab.
- A framework may be used only through an isolated simulation adapter with network access disabled and deterministic local data.
- Preserve copyright and license notices. Strong-copyleft or source-available projects are **reference-only** unless a later documented license review approves the exact integration method.
- Every derived experiment still needs its own pushed commit with performer, predeclaration, strategy class, parameters, data checksum, costs, timestamps, exact results, and reproduction evidence. Failed runs remain in history.
- Final validation data stays untouched during exploration.

## Vetted sources and assignments

| Source | Pinned commit | License at pin | Maintenance / provenance observed | Simulation-only research value | Reuse decision | Assigned branch / performer | Derived experiment queue |
|---|---|---|---|---|---|---|---|
| [QuantConnect LEAN](https://github.com/QuantConnect/Lean) | [`985ef30`](https://github.com/QuantConnect/Lean/tree/985ef30ad3ac774218c5ac516b4cb0aa2655730f) | [Apache-2.0](https://github.com/QuantConnect/Lean/blob/985ef30ad3ac774218c5ac516b4cb0aa2655730f/LICENSE) | Commit 2026-09-18; active upstream; 9 GitHub workflows observed. Large C#/Python engine with a wide attack surface. | Event sequencing, consolidators, exchange calendars, fees/slippage, regression fixtures. | **Approved for concepts and narrowly reviewed simulation modules only.** Exclude brokerage/live handlers, cloud clients and network code. | `main-pipeline` / Instinct main pipeline | Opening-range breakout; VWAP mean reversion; lunch/close seasonality; gap continuation; intraday volatility breakout. |
| [Zipline Reloaded](https://github.com/stefan-jansen/zipline-reloaded) | [`943010b`](https://github.com/stefan-jansen/zipline-reloaded/tree/943010b9da848e317fc520de87edade2b884d329) | [Apache-2.0](https://github.com/stefan-jansen/zipline-reloaded/blob/943010b9da848e317fc520de87edade2b884d329/LICENSE) | Commit 2025-11-13; maintained fork of Quantopian Zipline; 6 workflows observed; no root security policy observed. | Event-driven accounting, bundles, trading calendars, pipeline-style factors. | **Approved for a pinned simulation dependency or clean-room adapter after dependency review.** | `cursor` / authenticated Cursor CLI competitor | Cross-sectional intraday momentum; sector-neutral reversal; liquidity filter ablations; calendar-edge tests. |
| [QSTrader](https://github.com/mhallsmoore/qstrader) | [`4c59e15`](https://github.com/mhallsmoore/qstrader/tree/4c59e1584e83fcc2be644b820f827c0dd1b45c02) | [MIT](https://github.com/mhallsmoore/qstrader/blob/4c59e1584e83fcc2be644b820f827c0dd1b45c02/LICENSE) | Commit 2024-06-24; identifiable QuantStart provenance; no GitHub workflows or root security policy observed. | Loosely coupled signal, portfolio, risk, execution and simulated brokerage boundaries. | **Approved as architecture reference; direct dependency only after compatibility and dependency checks.** | `main-pipeline` / Instinct main pipeline | Position-sizing controls; turnover caps; volatility targeting; cost-model sensitivity; execution-delay stress. |
| [Jesse](https://github.com/jesse-ai/jesse) | [`432cce8`](https://github.com/jesse-ai/jesse/tree/432cce8a4b91828ce34dcaffac3f8e67354d061c) | [MIT](https://github.com/jesse-ai/jesse/blob/432cce8a4b91828ce34dcaffac3f8e67354d061c/LICENSE) | Commit 2026-09-17; active upstream; 3 workflows observed; no root security policy observed. Includes live/paper and web features. | Multi-timeframe simulation, rule-significance tests, trade/candle Monte Carlo and look-ahead controls. | **Concept/reference only initially.** Do not import exchange, live-trade, web, MCP or notification code. A later review may approve isolated research modules. | `cursor` / authenticated Cursor CLI competitor | 1m/5m/15m agreement; Monte Carlo path perturbation; entry-rule significance; walk-forward parameter stability. |
| [Freqtrade](https://github.com/freqtrade/freqtrade) | [`2f509e1`](https://github.com/freqtrade/freqtrade/tree/2f509e18ed117f5e62a0ebe0167422be47e291ad) | [GPL-3.0](https://github.com/freqtrade/freqtrade/blob/2f509e18ed117f5e62a0ebe0167422be47e291ad/LICENSE) | Commit 2026-09-18; active upstream; 10 workflows observed; no root security policy observed. Live exchange bot plus research tooling. | Look-ahead analysis, recursive-analysis checks, backtest analysis, hyperparameter experiment design. | **Reference-only.** No code copy or dependency without a separate GPL compatibility decision. Never reuse exchange/bot paths. | `main-pipeline` / Instinct main pipeline | Look-ahead audit; indicator warm-up sensitivity; recursive indicator drift; fee/slippage break-even grid. |
| [Backtesting.py](https://github.com/kernc/backtesting.py) | [`ca2e261`](https://github.com/kernc/backtesting.py/tree/ca2e2611621e472542ba90f7243a1fa06a7d7108) | [AGPL-3.0](https://github.com/kernc/backtesting.py/blob/ca2e2611621e472542ba90f7243a1fa06a7d7108/LICENSE.md) | Commit 2026-08-05; active upstream; 2 workflows observed; no root security policy observed. | Simple bar-by-bar baseline, optimizer and trade-level output for independent reproduction. | **Reference-only.** No code copy or service integration without an AGPL compatibility decision. | `cursor` / authenticated Cursor CLI competitor | Minimal independent reproducer; stop/limit ambiguity stress; optimizer leakage control; baseline parity checks. |
| [Backtrader](https://github.com/mementum/backtrader) | [`b853d7c`](https://github.com/mementum/backtrader/tree/b853d7c90b6721476eb5a5ea3135224e33db1f14) | [GPL-3.0-or-later](https://github.com/mementum/backtrader/blob/b853d7c90b6721476eb5a5ea3135224e33db1f14/LICENSE) | Commit 2023-04-19; stale relative to this review; no GitHub workflows or root security policy observed. Supports live trading. | Broker simulation semantics for market/close/limit/stop orders. | **Reference-only and lower priority** because of copyleft, age and live capability. | `main-pipeline` / Instinct main pipeline | Same-bar order ambiguity; stop-gap behavior; partial-fill model comparison; stale-framework parity test. |
| [VectorBT](https://github.com/polakowo/vectorbt) | [`a3c0f40`](https://github.com/polakowo/vectorbt/tree/a3c0f40979648585b4581fc4694fd6e92b3fffca) | [Apache-2.0 + Commons Clause](https://github.com/polakowo/vectorbt/blob/a3c0f40979648585b4581fc4694fd6e92b3fffca/LICENSE.md) | Commit 2026-09-17; active upstream; 4 workflows observed; no root security policy observed. License is source-available/fair-code, not ordinary permissive Apache. | Matrix-style high-volume parameter sweeps and portfolio analytics. | **Concept-only. Do not copy or vendor.** Obtain a separate license decision before any dependency use. | `cursor` / authenticated Cursor CLI competitor | Batched parameter grids implemented in lab-owned code; multiple-testing correction; deflated-Sharpe ranking; untouched holdout gate. |

## Provenance and security notes

1. Exact commit IDs were obtained from each official GitHub remote and checked against the files at that commit. The linked commit and license pages are the review evidence.
2. Repository content was inspected as untrusted data. No setup command, dependency installation, action, hook, container or project code from these repositories was executed.
3. A recent commit is evidence of activity, not safety. Workflow count is only an observed maintenance signal, not an audit. None of the inspected roots exposed a conventional `SECURITY.md`; downstream use therefore requires a local dependency/SBOM review and isolation.
4. LEAN, Jesse, Freqtrade and Backtrader contain live-trading capability upstream. Their presence in this catalog does not authorize or introduce that capability here.
5. No API keys, datasets, strategy secrets or credentials were copied. This catalog contains URLs, commit hashes, licenses and research assignments only.

## Experiment intake record

Each experiment derived from a catalog entry must add its own line in the experiment's evidence file:

```text
upstream_source_url:
upstream_commit:
upstream_license:
reuse_mode: concept-only | dependency | adapted-module
files_or_ideas_used:
license_notices_preserved:
network_disabled: true
live_order_paths_present: false
performer:
branch:
experiment_commit:
```

The catalog itself scores nothing. Only separately committed experiments that pass their predefined acceptance and reproduction gates enter the competition score.
