# 格式标准参考

| 元素 | 格式 |
|---------|--------|
| 硬编码输入 | 蓝色字体 |
| 公式 | 黑色字体 |
| 指向其他工作表的链接 | 绿色字体 |
| 检查单元格 | 出错时红色，平衡时绿色 |
| 负值 | 使用括号，不使用负号 |
| 货币 | 大额数字不保留小数，每股数据保留 2 位小数 |
| 百分比 | 保留 1 位小数 |
| 标题 | 加粗，底部边框 |
| 单位行 | 在标题下方加入单位行（$ millions、%、等） |

## 视觉分隔指引

- 在历史列和预测列之间使用细竖边框
- 在分部总计之后使用粗底边框（例如 Total Assets）
- 小计使用单底边框
- 总计使用双底边框

## 总计和小计行格式

所有总计和小计行的数值都必须使用**加粗字体**，以便将汇总数字与单独项目清晰区分开来。

### 利润表（P&L）标签页
| 行 | 格式 |
|-----|------------|
| Gross Revenue | Bold |
| Total Cost of Revenue | Bold |
| Gross Profit | Bold |
| Total SG&A | Bold |
| EBITDA | Bold |
| EBIT | Bold |
| EBT | Bold |
| Net Profit After Tax | Bold |

### 资产负债表标签页
| 行 | 格式 |
|-----|------------|
| Total Current Assets | Bold |
| Total Non-Current Assets | Bold |
| Total Other Assets | Bold |
| Total Assets | Bold |
| Total Current Liabilities | Bold |
| Total Non-Current Liabilities | Bold |
| Total Equity | Bold |
| Total Liabilities and Equity | Bold |

### 现金流量表标签页
| 行 | 格式 |
|-----|------------|
| Cash Generated from Operations Before Working Capital Changes | Bold |
| Total Working Capital Changes | Bold |
| Net Cash Generated from Operations | Bold |
| Net Cash Flow from Investing Activities | Bold |
| Net Cash Flow from Financing Activities | Bold |
| Closing Cash Balance | Bold |

**注意：** 此清单并不穷尽。凡是代表总计、小计或汇总计算的行，都应在整个模型中应用加粗格式。

## 资产负债表检查行格式

资产负债表检查行（位于 Total Liabilities and Equity 下方）应使用条件数字格式，在数值不为零时显示为红色。当资产负债表正确平衡时（检查值 = 0），这些值显示为黑色或标准格式。

| 检查值 | 字体颜色 |
|-------------|------------|
| = 0（平衡） | Black（标准） |
| ≠ 0（错误） | Red |

**实现方式：** 应用自定义数字格式 `[Red][<>0]0.00;[Red][<>0](0.00);0.00`，或使用 Excel 条件格式规则 "Cell Value ≠ 0" → Red font。

## 利润率行格式

| 元素 | 格式 |
|---------|--------|
| Margin % 行 | 缩进、斜体、1 位小数 |
| 正向趋势 | 无特殊格式（或轻微绿色） |
| 负向趋势 | 标记以供审阅（浅黄色） |
| 低于同行平均 | 可考虑高亮以便讨论 |

## 信贷指标格式

| 元素 | 格式 |
|---------|--------|
| 杠杆倍数 | 1 位小数并带 `x` 后缀（例如 2.5x） |
| 百分比 | 1 位小数并带 `%` 后缀 |
| 净负债为负 | 使用括号，表示净现金头寸 |
| 分部标题 | 加粗，`CREDIT METRICS` |
| 分隔线 | 信贷指标分部上方使用细边框 |

## 信贷指标阈值颜色

| 指标 | Green | Yellow | Red |
|--------|-------|--------|-----|
| Total Debt / EBITDA | < 2.5x | 2.5x-4.0x | > 4.0x |
| Net Debt / EBITDA | < 2.0x | 2.0x-3.5x | > 3.5x |
| Interest Coverage | > 4.0x | 2.5x-4.0x | < 2.5x |
| Debt / Total Cap | < 40% | 40%-60% | > 60% |
| Current Ratio | > 1.5x | 1.0x-1.5x | < 1.0x |
| Quick Ratio | > 1.0x | 0.75x-1.0x | < 0.75x |

## Checks 标签页的条件格式

- 单元格包含通过标记 → 绿色填充
- 单元格包含失败标记 → 红色填充
- 单元格包含警告 → 黄色填充
- 差异单元格 = 0 → 浅绿色填充
- 差异单元格 ≠ 0 → 浅红色填充

## 利润率合理性标记

- Gross Margin < 0% → ERROR：检查 COGS
- Gross Margin > 80% → WARNING：核实 revenue/COGS
- EBITDA Margin < 0% → FLAG：经营亏损
- EBITDA Margin > 50% → WARNING：异常偏高
- Net Margin < 0% → FLAG：净亏损（在增长阶段可能可以接受）
- Net Margin > Gross Margin → ERROR：公式有问题
