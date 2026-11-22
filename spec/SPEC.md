# IC-MEMO — the open investment-committee memo format

> **Spec v0.2** — extracted from production use (dsh-TradingAgents, 2026-11-16 → 11-22, dozens of live memos incl. the portfolio variant). An IC-MEMO is the durable, evidence-tagged record of a multi-role investment debate that ends in a disciplined verdict. It is designed to be **written by committees (human or agent), read by future committees, and settled by ledgers**.
>
> Reference implementation: [vicfei/dsh-TradingAgents](https://github.com/vicfei/dsh-TradingAgents) (writer) · this repo (spec, validators, renderers). Stability: v0.2 fields never renamed, only added.

## 1. Document shape

Markdown for humans with **one machine block**: a fenced `yaml` header immediately after the H1.

```markdown
# IC-MEMO · <TICKER> · <YYYY-MM-DD>

```yaml
ticker: <string>
as_of: <YYYY-MM-DD>
committee: <string>          # e.g. tradingagents/v1
decision: <verdict>          # see §3
confidence: <int 0-100>
size_hint: <string>          # free-form, references [G#]
invalidation: [<string>, …]  # conditions that force re-review, each cites tags
```

## 1 · 分析师纪要 …       # section names are conventional, not mandated
## 2 · 多空辩论 …
## 3 · 风控护栏 …
## 4 · 组合经理裁决 …
---
*<cost footer>*
```

**Mandatory sections** (headings are free-form but the ROLES are fixed):
analyst brief (facts), bull/bear debate (challenges + responses), risk
guardrails, PM verdict. A memo missing any role's output is invalid.

## 2. Evidence tags — the load-bearing rule

- `[A#]` analyst facts · `[B#]` bull claims · `[R#]` bear rebuttals ·
  `[G#]` guardrails · `[T#]` track-record lessons (re-injected history).
- **Every factual claim carries a tag; every tag is defined exactly once**
  in the section that owns it; claims cite tags — `…[A2][G3]`.
- Numbers are **only allowed inside tagged claims** — no orphan figures.
  A claim with no evidence citation is a spec violation, not a style issue.
- Optional `[X#-TICKER]` suffix in portfolio memos namespaces facts per name.

## 3. Verdict vocabulary (closed set, normalizable)

| verdict | meaning |
|---|---|
| `BUY` / `OVERWEIGHT` / `HOLD` / `UNDERWEIGHT` / `SELL` | directed calls (settleable) |
| `PASS` | **first-class abstention** — evidence insufficient or guardrails unresolved; never settles, never counts as a directional miss |
| `REVIEW` | sentinel — out-of-vocabulary/missing decision, machine-normalized; banners the memo, never silently treated as PASS/HOLD |

`confidence: 0-100` accompanies every verdict. A PASS with reasoning is a
complete, valuable memo — abstention is a decision.

## 4. Guardrails vs decisions (the auditability spine)

Guardrails (`[G#]`) **constrain** the PM; they never decide. The verdict
section must cite the guardrails that bound it; overruling one must be
explicit and reasoned. A PM verdict with zero [G#] citations is invalid.

## 5. Portfolio variant

Same shape; the header carries `tickers: [...]`, `decision: DEPLOY | HOLD |
PASS | REVIEW`, `weights: {<ticker>: <pct>}`, `cash_pct: <pct>` —
**weights + cash must sum to 100**; a wrong total is flagged on the memo,
never silently rescaled. Allocation debate cites `[A#-TICKER]`;
guardrails include single-name cap, concentration limits, a
stated-plainly correlation caveat when no correlation data is in evidence.

## 6. Footer & disclosures (mandatory)

- Cost footer: elapsed, model, temperature, data source(s) — reproducibility.
- **Not-investment-advice footer on every memo. No exceptions.**
- Synthetic/demo memos must be conspicuously marked (`ticker: DEMO` or an
  explicit synthetic banner); synthetic memos never enter real ledgers.

## 7. Ledger interop (settlement contract)

An IC-MEMO is born settleable: `(ticker, as_of, decision, confidence)` is
the ledger entry; point-in-time discipline belongs to the ledger (entry at
first close strictly after `as_of`; never score the live bar; unresolved
windows stay pending). The memo itself never contains outcome data —
outcomes live in the ledger and re-enter future memos only as `[T#]`
citations.

## 8. Conformance

A conformant tool: parses the yaml header, checks the closed verdict
vocabulary (normalizing casing; rejecting out-of-vocabulary to REVIEW),
validates tag uniqueness and citation integrity (cited tags exist), and
renders without loss (single-file HTML; `dsh-ui` inline card). The
reference validator/renderers live in this repo; dsh-TradingAgents is the
reference writer.
