# Model Update

description: 用新数据更新财务模型，包括季度业绩、管理层指引、宏观变化或修订后的假设。调整预测、重新计算估值，并标记重大变化。适用于业绩发布后、指引更新后，或需要刷新核心假设时。在用户提到 "update model"、"plug earnings"、"refresh estimates"、"update numbers for [company]"、"new guidance" 或 "revise estimates" 时触发。

## 工作流

### 第 1 步：识别变化内容

确定更新触发因素：
- **Earnings release**：录入新的季度实际值
- **Guidance change**：公司更新了前瞻指引
- **Estimate revision**：分析师基于新信息调整假设
- **Macro update**：利率、汇率、大宗商品价格发生变化
- **Event-driven**：并购、重组、新产品、管理层变动

### 第 2 步：录入新数据

#### 业绩发布后
用公司披露的实际值更新模型：

| Line Item | Prior Estimate | Actual | Delta | Notes |
|-----------|---------------|--------|-------|-------|
| Revenue | | | | |
| Gross Margin | | | | |
| Operating Expenses | | | | |
| EBITDA | | | | |
| EPS | | | | |
| [Key metric 1] | | | | |
| [Key metric 2] | | | | |

**Segment Detail**（如适用）：
- 更新各业务分部的收入和利润率
- 记录任何分部结构变化

**资产负债表 / 现金流更新**：
- 现金与债务余额
- 股本数量，回购、稀释
- 资本开支实际值对比原预测
- 营运资本变化

### 第 3 步：修订前瞻预测

基于新数据，调整前瞻预测：

| | Old FY Est | New FY Est | Change | Old Next FY | New Next FY | Change |
|---|-----------|-----------|--------|------------|------------|--------|
| Revenue | | | | | | |
| EBITDA | | | | | | |
| EPS | | | | | | |

**关键假设变化：**
- 你在调整哪些假设，为什么？
- 收入增长率：old → new，原因
- 利润率假设：old → new，原因
- 是否新增项目，例如重组费用、一次性收益等

### 第 4 步：估值影响

基于更新后的预测重新计算估值：

| Valuation Method | Prior | Updated | Change |
|-----------------|-------|---------|--------|
| DCF fair value | | | |
| P/E (NTM EPS × target multiple) | | | |
| EV/EBITDA (NTM EBITDA × target multiple) | | | |
| **Price Target** | | | |

### 第 5 步：总结与行动

**预测变动总结：**
- 用一段话说明变了什么、为什么变、这对股价意味着什么
- 这是改变投资论点的事件，还是噪音？

**评级 / 目标价：**
- 维持评级还是调整评级？
- 新目标价，如果有变化，要说明方法论
- 相对当前股价的上行或下行空间

### 第 6 步：输出

- 更新后的 Excel 模型，如果用户提供了现有模型
- 预测变动总结，markdown 或 Word
- 更新后的目标价推导

## 重要说明

- 在往前推演之前，务必先将你的预测与公司披露数据完全对齐
- 标注任何一次性项目，并说明你的预测基于 GAAP 还是调整后口径
- 跟踪你的预测修订历史，这能展示你的分析演进
- 如果该季度噪音较大，要在预测调整中区分信号与噪音
- 更新后检查一致预期，你修订后的预测与 sell-side 主流预期相比如何？
- 股本数量很重要，股权激励、可转债或回购带来的稀释会实质影响 EPS
