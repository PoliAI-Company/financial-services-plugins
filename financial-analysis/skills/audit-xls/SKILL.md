---
name: audit-xls
description: 审计电子表格中的公式准确性、错误和常见问题。可将范围限定为选定区域、单个工作表或整个模型，包括资产负债表平衡、现金勾稽和逻辑合理性等财务模型完整性检查。当用户提出“audit this sheet”“check my formulas”“find formula errors”“QA this spreadsheet”“sanity check this”“debug model”“model check”“model won't balance”“something's off in my model”“model review”等请求时使用。
---

# 审计电子表格

审计公式和数据的准确性与错误。范围决定深度，从选区的快速公式检查，到完整财务模型的完整性审计。

## 第 1 步：确定范围

如果用户已经给出范围，则直接使用。否则**询问他们**：

> What scope do you want me to audit?
> - **selection** — just the currently selected range
> - **sheet** — the current active sheet only
> - **model** — the whole workbook, including financial-model integrity checks (BS balance, cash tie-out, roll-forwards, logic sanity)

**model** 范围最深入，适用于 DCF、LBO、三大报表、并购、comps 或任何在发送给客户或 IC 前需要检查的集成财务模型。

---

## 第 2 步：公式层检查（所有范围）

无论范围如何，都执行以下检查：

| 检查项 | 关注点 |
|---|---|
| 公式错误 | `#REF!`, `#VALUE!`, `#N/A`, `#DIV/0!`, `#NAME?` |
| 公式中的硬编码 | `=A1*1.05` 中的 `1.05` 应该是单元格引用 |
| 公式不一致 | 某个公式打破其所在行或列的相邻模式 |
| 范围偏移一行 | `SUM` / `AVERAGE` 漏掉首行或末行 |
| 被粘贴覆盖的公式 | 看起来像公式逻辑，但实际上是硬编码值 |
| 循环引用 | 有意或无意 |
| 跨表链接损坏 | 引用了被移动或删除的单元格 |
| 单位或尺度不匹配 | 千与百万混用，百分比以整数形式存储 |
| 隐藏行/标签页 | 可能包含覆盖值或陈旧计算 |

---

## 第 3 步：模型完整性检查（仅 model 范围）

如果范围是 **model**，识别模型类型（DCF / LBO / 3-statement / merger / comps / custom），并执行相应完整性检查。

### 3a. 结构审查

| 检查项 | 关注点 |
|---|---|
| 输入/公式分离 | 输入是否与计算清晰分开？ |
| 颜色约定 | Blue=input、black=formula、green=link 或模型所用约定，是否一致？ |
| 标签页流程 | 顺序是否合理（Assumptions → IS → BS → CF → Valuation）？ |
| 日期标题 | 所有标签页是否一致？ |
| 单位 | 是否一致（thousands vs millions vs actuals）？ |

### 3b. 资产负债表

| 检查项 | 测试 |
|---|---|
| BS 平衡 | Total Assets = Total Liabilities + Equity（每个期间） |
| RE 滚动 | Prior RE + Net Income − Dividends = Current RE |
| Goodwill/intangibles | 是否由并购假设流转而来（如适用） |

如果 BS 不平，**按期间量化差额并追踪问题断点**。在修复前，其他内容都不重要。

### 3c. 现金流量表

| 检查项 | 测试 |
|---|---|
| 现金勾稽 | CF Ending Cash = BS Cash（每个期间） |
| 现金流求和 | CFO + CFI + CFF = Δ Cash |
| D&A 一致 | CF 上的 D&A = IS 上的 D&A |
| CapEx 一致 | CF 上的 CapEx 与 BS 上的 PP&E rollforward 一致 |
| 营运资本变动 | 符号与 BS 变动方向一致（ΔAR、ΔAP、ΔInventory） |

### 3d. 利润表

| 检查项 | 测试 |
|---|---|
| 收入构建 | 与分部或产品明细一致 |
| 税项 | Tax expense = Pre-tax income × tax rate（允许递延税调整） |
| 股本数量 | 与稀释明细表一致（期权、可转债、回购） |

### 3e. 循环引用

- Interest → debt balance → cash → interest 是 LBO/3-statement 中常见的有意循环
- 若为有意：验证迭代开关存在且能正常工作
- 若为无意：追踪循环路径并说明如何打断

### 3f. 逻辑与合理性

| 检查项 | 何时标记 |
|---|---|
| 增长率 | 收入增长 >100% 且没有解释 |
| 利润率 | 超出行业常规范围 |
| 终值占比过高 | TV > ~75% 的 DCF EV（黄色警示） |
| 曲棍球杆式预测 | 远期年度预测出现不现实的跃升 |
| 复合增长过度 | EBITDA 到第 10 年膨胀到荒谬水平 |
| 极端情况 | 在 0% 或负增长、负 EBITDA、杠杆为负时模型崩溃 |

### 3g. 不同模型类型的特定 bug

**DCF：**
- 折现率用在错误期间（mid-year vs end-of-year）
- 终值未折现回现值
- WACC 使用账面值而非市值
- FCF 包含利息费用（应为 unlevered）
- 税盾重复计算

**LBO：**
- 债务偿还与 cash sweep 机制不匹配
- PIK 利息未计入本金
- 管理层 rollover 未反映在回报中
- 退出倍数用错 EBITDA（LTM vs NTM）
- 费用未从 Day 1 equity 中扣除

**Merger：**
- 增厚/摊薄使用了错误股本数（交易前 vs 交易后）
- 协同效应未逐步体现
- Purchase price allocation 不平
- 现金利息损失未计入
- 交易费用未进入 sources & uses

**3-statement：**
- 营运资本变动符号错误
- 折旧与 PP&E schedule 不一致
- 债务到期表与本金偿还不一致
- 分红超过净利润且没有解释

---

## 第 4 步：输出报告

输出发现表：

| # | Sheet | Cell/Range | Severity | Category | Issue | Suggested Fix |
|---|---|---|---|---|---|---|

**严重级别：**
- **Critical** — 输出错误（BS 不平、公式损坏、现金不勾稽）
- **Warning** — 风险较高（硬编码、公式不一致、极端情况失效）
- **Info** — 风格或最佳实践问题（颜色编码、布局、命名）

对于 **model** 范围，在前面加一行摘要：

> Model type: [DCF/LBO/3-stmt/...] — Overall: [Clean / Minor Issues / Major Issues] — [N] critical, [N] warnings, [N] info

**未经用户要求不要改动任何内容**，先报告，待用户要求时再修复。

---

## 备注

- **先看 BS 平衡**。如果它不平，下游全部结果都值得怀疑
- **硬编码覆盖是最常见的隐性 bug 来源**，要积极搜索
- **符号约定错误**（现金流出正负号搞反）非常常见
- 如果模型使用 VBA 宏，请注明任何无法仅通过公式审计的宏驱动计算
