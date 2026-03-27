---
description: 构建包含交易倍数的可比公司分析
argument-hint: "[公司名称或股票代码]"
---

# 可比公司分析命令

构建机构级的可比公司分析，包括经营指标、估值倍数和统计基准对比。

## 工作流

### 第 1 步：收集公司信息

如果提供了公司名称或股票代码，则直接使用。否则请询问：
- "What company would you like to analyze?"

### 第 2 步：加载 Comps Analysis Skill

使用 `skill: "comps-analysis"` 构建分析：

1. **明确分析目的**：
   - "What's the key question?"（估值、效率、增长比较）
   - "Who is the audience?"（IC、董事会、快速参考）
   - "Do you have a preferred format or template?"

2. **识别同行组**（4 到 6 家可比公司）：
   - 相似的商业模式
   - 相似的规模或市值区间
   - 相同的行业或板块
   - 地域可比性

3. **收集数据**（如果可用，优先使用 MCP 数据源）：
   - 经营指标：Revenue、Growth、Gross Margin、EBITDA、EBITDA Margin
   - 估值：Market Cap、Enterprise Value、EV/Revenue、EV/EBITDA、P/E
   - 基于行业补充其他指标（例如 SaaS 的 Rule of 40）

4. **构建分析**：
   - Operating Statistics 部分，包含公司数据和统计值（Max、75th、Median、25th、Min）
   - Valuation Multiples 部分，使用相同的统计汇总
   - Notes & Methodology 文档说明

### 第 3 步：创建 Excel 输出

生成包含以下内容的 Excel 文件：
- 标题区块（分析标题、公司、日期、单位）
- Operating Statistics & Financial Metrics 部分
- Valuation Multiples 部分
- 每项指标的统计汇总
- 记录来源与方法论的 Notes 部分

### 第 4 步：交付输出

提供：
1. **Excel 文件**（.xlsx），即 comps 分析
2. **摘要**，重点说明：
   - 同行组选取逻辑
   - 关键洞察（谁处于估值溢价或折价）
   - 供参考的中位数倍数

## 输出格式参考

```
┌─────────────────────────────────────────────────────────────────┐
│ [SECTOR] - COMPARABLE COMPANY ANALYSIS                          │
│ [Company 1] • [Company 2] • [Company 3] • [Company 4]          │
│ As of [Date] | All figures in USD Millions                      │
├─────────────────────────────────────────────────────────────────┤
│ OPERATING STATISTICS & FINANCIAL METRICS                        │
├──────────┬─────────┬─────────┬──────────┬─────────┬────────────┤
│ Company  │ Revenue │ Growth  │ Gross    │ EBITDA  │ EBITDA     │
│          │ (LTM)   │ (YoY)   │ Margin   │ (LTM)   │ Margin     │
├──────────┼─────────┼─────────┼──────────┼─────────┼────────────┤
│ [Data rows for each company]                                    │
│                                                                 │
│ Maximum  │ =MAX    │ =MAX    │ =MAX     │ =MAX    │ =MAX       │
│ 75th %   │ =QUART  │ =QUART  │ =QUART   │ =QUART  │ =QUART     │
│ Median   │ =MEDIAN │ =MEDIAN │ =MEDIAN  │ =MEDIAN │ =MEDIAN    │
│ 25th %   │ =QUART  │ =QUART  │ =QUART   │ =QUART  │ =QUART     │
│ Minimum  │ =MIN    │ =MIN    │ =MIN     │ =MIN    │ =MIN       │
├─────────────────────────────────────────────────────────────────┤
│ VALUATION MULTIPLES                                             │
├──────────┬──────────┬──────────┬──────────┬───────────┬────────┤
│ Company  │ Mkt Cap  │ EV       │ EV/Rev   │ EV/EBITDA │ P/E    │
├──────────┼──────────┼──────────┼──────────┼───────────┼────────┤
│ [Data rows + statistics]                                        │
└─────────────────────────────────────────────────────────────────┘
```

## 行业特定指标

| 行业 | 补充指标 |
|----------|-------------------|
| Software/SaaS | ARR, Net Dollar Retention, Rule of 40 |
| Retail | Same-store sales, Inventory Turns |
| Financials | ROE, ROA, Efficiency Ratio |
| Manufacturing | Asset Turnover, CapEx/Revenue |
| Healthcare | R&D/Revenue, Pipeline Value |

## 质量检查清单

交付前：
- [ ] 4 到 6 家真正可比的公司
- [ ] 时间口径一致（全部为 LTM 或全部为 FY）
- [ ] 所有公式均引用单元格，不使用硬编码值
- [ ] 所有硬编码输入均附有来源注释
- [ ] 统计项包含 Max、75th、Median、25th、Min
- [ ] Notes 部分记录来源和方法论
- [ ] 蓝色 = 输入，黑色 = 公式
- [ ] 合理性检查通过（利润率合逻辑，倍数合理）
