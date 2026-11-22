# IC-MEMO —— 开放的投资委员会备忘录格式

**每条主张带证据标签。弃权是一等判决。护栏只约束、不裁决。** IC-MEMO
是多角色投研辩论的持久记录——分析师事实、多空交锋、风控护栏、组合经理
裁决——为**委员会写（人或 agent）、未来委员会读、台账结算**而设计。

- 📐 规范 v0.2（从生产使用中提取，非凭空发明）：
  [spec/SPEC.md](spec/SPEC.md)（英文）· 规范站：<https://vicfei.github.io/ic-memo/>
- 📄 真实示例（来自参考写方）：[examples/](examples/) —— NVDA PASS（带完整
  推理的弃权）、sh600519 OVERWEIGHT（首条定向判决）、DEMO 客座人格
  （合成数据，显著标记）
- ✍️ 参考写方：[vicfei/dsh-TradingAgents](https://github.com/vicfei/dsh-TradingAgents)
  （生产环境中产出这些 memo 的多智能体议院）
- 🖋 渲染器：单文件 HTML（采纳写方 render_html.py）· dsh-ui 内联卡（经
  [dsh-uigen](https://github.com/vicfei/dsh-uigen) 在 DeepSeek Harness
  回复内渲染）——均在计划中

[English](README.md) | 简体中文

## 为什么做开放格式

今天的投委会产出是聊天记录——不可审计、不可比较、对弃权沉默。IC-MEMO
把辩论变成**带契约的文档**：标签完整性规则（数字不得孤立出现）、封闭
判决词表（BUY/OVERWEIGHT/HOLD/UNDERWEIGHT/SELL + PASS + REVIEW 哨兵）、
每条裁决必须引用护栏、成本脚注、每份 memo 带非投资建议披露。台账按时点
纪律结算 (ticker, as_of, decision)；结果只以 [T#] 引用回到未来 memo——
议院学习自己的战绩而不污染时点纪律。

## 状态

2026-11-22 立项（写方路线图 S5.2）。规范 v0.2 + 示例已交付；校验器 +
Python SDK + 渲染器为下一里程碑（issue 跟踪）。

与任何上游无关。MIT。**此处任何内容均不构成投资建议。**
