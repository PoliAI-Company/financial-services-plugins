# 回报分析

description: 为 PE 交易评估快速构建 IRR/MOIC 敏感性分析表。围绕进入倍数、杠杆、退出倍数、增长和持有期情景建模回报。适用于快速评估一笔交易、对关键假设做压力测试，或准备 IC 回报展示页。触发词包括 "returns analysis"、"IRR sensitivity"、"MOIC table"、"what's the return at"、"model the returns" 或 "back of the envelope"。

## 工作流

### 第 1 步：收集交易输入

向用户询问，或从先前分析中提取：

**进入时：**
- 进入 EBITDA（LTM 或 NTM）
- 进入倍数（EV / EBITDA）
- 企业价值
- 交割时净债务
- 股权支票金额
- 交易费用与支出

**融资：**
- 高级债务（x EBITDA、利率、摊销）
- 次级债务 / 夹层融资（如有）
- 进入时总杠杆（x EBITDA）
- 股权出资

**经营假设：**
- 收入增长率（年化）
- EBITDA 利润率变化路径
- Capex 占收入百分比
- 营运资金变动
- 债务偿还进度

**退出时：**
- 持有期（年）
- 退出倍数（EV / EBITDA）
- 退出 EBITDA（根据增长假设计算）

### 第 2 步：基准情景回报

计算：

| 指标 | 数值 |
|--------|-------|
| 进入 EV | |
| 投入股权 | |
| 退出 EBITDA | |
| 退出 EV | |
| 退出时净债务 | |
| 退出股权价值 | |
| **MOIC** | |
| **IRR** | |
| 现金回报倍数 | |

展示回报瀑布分解：
- EBITDA 增长贡献
- 倍数扩张 / 收缩贡献
- 债务偿还贡献
- 费用 / 支出拖累

### 第 3 步：敏感性分析表

构建双变量敏感性矩阵：

**进入倍数 vs. 退出倍数**
| | Exit 6x | Exit 7x | Exit 8x | Exit 9x | Exit 10x |
|---|---------|---------|---------|---------|----------|
| Entry 7x | | | | | |
| Entry 8x | | | | | |
| Entry 9x | | | | | |
| Entry 10x | | | | | |

**EBITDA 增长 vs. 退出倍数**（固定进入倍数）

**杠杆 vs. 退出倍数**（固定进入倍数和增长）

**持有期 vs. 退出倍数**

每个单元格同时显示 IRR 和 MOIC，格式为 IRR / MOIC。

### 第 4 步：情景分析

构建 3 个情景：

| | Bull | Base | Bear |
|---|------|------|------|
| Revenue CAGR | | | |
| Exit EBITDA margin | | | |
| Exit multiple | | | |
| Exit EBITDA | | | |
| MOIC | | | |
| IRR | | | |

### 第 5 步：输出

- Excel 工作簿，包含：
  - 假设页
  - 回报计算页
  - 敏感性分析表（带条件着色格式）
  - 情景汇总页
- 一页式回报摘要，可直接用于 IC deck

## 关键公式

- **MOIC** = 退出股权价值 / 投入股权
- **IRR** = 求解 r：投入股权 × (1 + r)^n = 退出股权价值（如有中间现金流，需调整）
- **回报归因**：
  - 增长： (Exit EBITDA - Entry EBITDA) × Exit Multiple / Equity
  - 倍数： (Exit Multiple - Entry Multiple) × Entry EBITDA / Equity
  - 杠杆：持有期内债务偿还额 / Equity

## 重要说明

- 如适用，始终同时展示扣费前和扣费后、扣 carry 前和扣 carry 后的回报
- 管理层跟投和共同投资会改变股权支票金额，如相关请务必确认
- 股息再融资或中期分配会显著影响 IRR，如有计划必须纳入
- 不要忘记交易成本，通常为 EV 的 2-4%，它们会降低 Day 1 股权价值
- 税务因素，如 asset deal vs. stock deal、338(h)(10) election，可能会显著影响税后回报
