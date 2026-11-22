# IC-MEMO — the open investment-committee memo format

**Every claim carries an evidence tag. Abstention is a first-class verdict.
Guardrails constrain, they never decide.** An IC-MEMO is the durable record
of a multi-role investment debate — analyst facts, bull/bear challenge,
risk guardrails, portfolio-manager verdict — designed to be **written by
committees (human or agent), read by future committees, and settled by
ledgers**.

- 📐 Spec v0.2 (extracted from production use, not invented):
  [spec/SPEC.md](spec/SPEC.md) · spec site: <https://vicfei.github.io/ic-memo/>
- 📄 Real examples (from the reference writer): [examples/](examples/) —
  NVDA PASS (abstention with full reasoning), sh600519 OVERWEIGHT
  (the first directed call), DEMO with guest personas (synthetic, marked)
- ✍️ Reference writer: [vicfei/dsh-TradingAgents](https://github.com/vicfei/dsh-TradingAgents)
  (the multi-agent committee that produces these in production)
- 🖋 Renderers: single-file HTML (adopted from the writer's
  `render_html.py`) · `dsh-ui` inline card (renders inside DeepSeek Harness
  replies via [dsh-uigen](https://github.com/vicfei/dsh-uigen)) — both planned

English | [简体中文](README.zh-CN.md)

## Why an open format

Investment-committee outputs today are chat logs — unauditable,
uncomparable, and silent on abstention. IC-MEMO makes the debate a
**document with a contract**: tag-integrity rules (no orphan numbers),
a closed verdict vocabulary (`BUY/OVERWEIGHT/HOLD/UNDERWEIGHT/SELL` +
`PASS` + `REVIEW` sentinel), mandatory guardrail citations in every
verdict, a cost footer, and a not-investment-advice disclosure on every
memo. Ledgers settle `(ticker, as_of, decision)` entries against
point-in-time windows; outcomes re-enter future memos only as `[T#]`
citations — the committee learns its own scorecard without polluting
point-in-time discipline.

## Status

Founded 2026-11-22 (S5.2 of the writer's roadmap). Spec v0.2 + examples
shipped; validator + Python SDK + renderers are the next milestones
(tracked in issues).

Not affiliated with any upstream. MIT. **Nothing here is investment
advice.**
