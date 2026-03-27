# Deal Tracker

description: 跟踪多个在执行交易的里程碑、截止日期、行动事项和状态更新。维护交易管线视图，并提示即将到来的截止日期及逾期事项。适用于管理交易项目、跟踪流程里程碑，或准备每周交易审阅。触发词包括 "deal tracker"、"deal status"、"where are we on"、"process update"、"deal pipeline" 和 "weekly deal review"。

## Workflow

### Step 1: 交易设置

针对每笔交易，记录：
- **Deal name / code name**: Project [Name]
- **Client**: 卖方或买方名称
- **Deal type**: Sell-side、buy-side、financing、restructuring
- **Role**: Lead advisor、co-advisor、fairness opinion
- **Deal size**: 预期 enterprise value
- **Stage**: Pre-mandate → Engaged → Marketing → IOI → Diligence → Final bids → Signing → Close
- **Team**: 分配的 MD、VP、Associate、Analyst
- **Key dates**: Engagement date、CIM distribution、IOI deadline、management meetings、final bid deadline、target close

### Step 2: 里程碑跟踪

按交易跟踪关键里程碑：

| Milestone | Target Date | Actual Date | Status | Notes |
|-----------|------------|-------------|--------|-------|
| Engagement letter signed | | | | |
| CIM / teaser drafted | | | | |
| Buyer list approved | | | | |
| Teaser distributed | | | | |
| NDA execution | | | | |
| CIM distributed | | | | |
| IOI deadline | | | | |
| IOIs received / reviewed | | | | |
| Shortlist selected | | | | |
| Management meetings | | | | |
| Data room opened | | | | |
| Final bid deadline | | | | |
| Bids received / reviewed | | | | |
| Exclusivity granted | | | | |
| Confirmatory diligence | | | | |
| Purchase agreement signed | | | | |
| Regulatory approval | | | | |
| Close | | | | |

Status: On Track / At Risk / Delayed / Complete

### Step 3: 行动事项

维护一份覆盖所有交易的行动事项滚动清单：

| Action | Deal | Owner | Due Date | Priority | Status |
|--------|------|-------|----------|----------|--------|
| | | | | P0/P1/P2 | Open/Done/Blocked |

### Step 4: 每周交易审阅

为每周团队会议生成摘要：

**对每个活跃交易：**
1. 一行状态更新
2. 本周关键进展
3. 接下来 2 周的重要里程碑
4. 阻碍或风险
5. 下周行动事项

**Pipeline 摘要：**
- 各阶段活跃交易总数
- 风险交易，里程碑延误或流程停滞
- 管线中的新委托 / pitch
- 本季度预期 closing

### Step 5: 输出

- Excel workbook，包含：
  - Pipeline overview，所有交易，每行一笔
  - 每笔交易的 milestone tracker 标签页
  - Action item master list
  - Weekly review summary
- 可选：用于邮件或 Slack 分发的 Markdown 摘要

## Important Notes

- 至少每周更新一次 tracker，过期的 tracker 比没有 tracker 更糟
- 对里程碑开始滑落的交易及时预警，越早发现越能避免意外
- 没有 owner 和 due date 的行动事项通常不会完成，所以一定要具体
- Pipeline 视图应显示交易阶段、规模和成交概率，这对收入预测很有帮助
- 保留买方 / 投资人反馈记录，反馈中的模式有助于调整策略
- 已关闭或终止的交易应单独归档，保持活跃视图干净
