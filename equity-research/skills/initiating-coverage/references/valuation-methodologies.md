# 股票研究估值方法论

本参考文档系统说明股票研究中使用的三类主要估值方法：Discounted Cash Flow (DCF)、Trading Comparables 和 Precedent Transactions。

## 目录

1. [Discounted Cash Flow (DCF) Analysis](#discounted-cash-flow-dcf-analysis)
2. [Trading Comparables Analysis](#trading-comparables-analysis)
3. [Precedent Transactions Analysis](#precedent-transactions-analysis)
4. [Valuation Reconciliation](#valuation-reconciliation)

---

## Discounted Cash Flow (DCF) Analysis

### 概览

DCF 分析基于公司未来预测现金流的现值来估值。由于它建立在企业基本面价值创造之上，因此通常被视为理论上最扎实的估值方法。

### 分步 DCF 流程

#### 1. 历史财务分析
- 收集 3-5 年历史财务数据
- 计算历史 FCF = EBIT(1-Tax Rate) + D&A - CapEx - Change in NWC
- 分析历史增长率与利润率
- 识别趋势与周期性

#### 2. 搭建收入预测（5-10 年）
**方法：**
- **Top-down**：从市场规模（TAM）→ 市场份额 → 收入
- **Bottom-up**：销量 × 单价
- **Hybrid**：组合多个驱动因素

**关键考虑：**
- 管理层指引与历史增长
- 行业增长率与市场趋势
- 竞争格局与市场份额演变
- 产品管线与新市场机会
- 宏观经济因素

#### 3. 预测营业费用
- **COGS**：按收入百分比建模（分析历史利润率）
- **SG&A**：通常半固定；按收入百分比建模，并考虑规模效应
- **R&D**：对 tech/pharma 很关键；按收入百分比建模
- **D&A**：基于 CapEx 假设推导

**Calculate EBIT** = Revenue - COGS - Operating Expenses

#### 4. 计算 Unlevered Free Cash Flow
```
EBIT
× (1 - Tax Rate)
= NOPAT (Net Operating Profit After Tax)
+ Depreciation & Amortization
- Capital Expenditures
- Increase in Net Working Capital
= Unlevered Free Cash Flow (UFCF)
```

**CapEx Assumptions：**
- Maintenance CapEx：维持当前经营所需的资本开支，通常为收入的 2-4%
- Growth CapEx：扩张所需的资本开支
- 参考行业基准和公司指引

**Net Working Capital：**
- NWC = (Accounts Receivable + Inventory) - Accounts Payable
- 可按收入百分比或按天数建模，DSO、DIO、DPO
- NWC 增加表示现金流出

#### 5. 确定 Terminal Value

**Method A: Perpetuity Growth Method**
```
Terminal Value = FCF(final year) × (1 + g) / (WACC - g)
```
- g = 永续增长率，通常 2-3%，不能超过 GDP 长期增速
- 适用于公司已进入稳定成熟增长阶段

**Method B: Exit Multiple Method**
```
Terminal Value = EBITDA(final year) × Exit Multiple
```
- Exit multiple 通常参考当前 trading comps
- 对周期性业务更适用

#### 6. 计算 Weighted Average Cost of Capital (WACC)

```
WACC = (E/V × Cost of Equity) + (D/V × Cost of Debt × (1 - Tax Rate))
```

**Cost of Equity（用 CAPM 计算）：**
```
Cost of Equity = Risk-Free Rate + Beta × Equity Risk Premium
```
- Risk-Free Rate：10-year Treasury yield
- Beta：股价收益率相对市场的回归 beta，或使用可比公司 beta
- Equity Risk Premium：历史平均约 5-6%

**Cost of Debt：**
```
Cost of Debt = Risk-Free Rate + Credit Spread
```
- 使用公司当前借款利率，或债券隐含收益率
- 如无在外债券，则根据信用评级调整

**Capital Structure：**
- E/V = 股权市场价值 / 总价值
- D/V = 债务市场价值 / 总价值
- 使用目标资本结构，而不是当前结构，若差异较大时尤其如此

#### 7. 将现金流折现到现值

```
PV = Σ [FCFt / (1 + WACC)^t] + [Terminal Value / (1 + WACC)^n]
```

#### 8. 计算 Enterprise Value 与 Equity Value

```
Enterprise Value = PV of Projected FCF + PV of Terminal Value
Less: Net Debt (Total Debt - Cash)
Plus: Non-operating Assets
Less: Minority Interest
Less: Preferred Stock
= Equity Value

Price Per Share = Equity Value / Diluted Shares Outstanding
```

### DCF Sensitivity Analysis

始终要对关键变量进行 sensitivity analysis：

1. **Two-way sensitivity table**：WACC vs. Terminal Growth Rate
2. **Revenue growth scenarios**：Base / Bull / Bear cases
3. **Margin assumptions**：经营杠杆情景
4. **Terminal multiple sensitivity**：若使用 exit multiple method

**示例敏感性表：**
```
           Terminal Growth Rate
WACC      2.0%    2.5%    3.0%
8.0%      $45     $48     $52
9.0%      $40     $43     $46
10.0%     $36     $39     $41
```

### 常见 DCF 错误，务必避免

1. **Double-counting growth**：在没有相应投资，CapEx、NWC 的情况下，假设高增长
2. **Unrealistic terminal growth**：终值增长率不应超过长期 GDP 增速
3. **Ignoring cyclicality**：对周期性业务要用归一化盈利
4. **Wrong cash flow definition**：应使用 unlevered FCF，而不是 net income
5. **Inconsistent assumptions**：折现率必须与现金流口径匹配，unlevered FCF 对应 WACC

---

## Trading Comparables Analysis

### 概览

Trading comps 基于公开市场上类似公司的估值水平来为目标公司估值。它反映当前市场情绪和相对估值水平。

### 分步 Comps 流程

#### 1. 选择可比公司

**选择标准：**
- 同一行业 / 板块，这是首要标准
- 相似的商业模式和收入来源
- 可比的规模，market cap、revenue
- 相似的增长轮廓和利润率
- 相似的终端市场与地区分布

**典型样本池：**
- 从 8-15 家公司开始
- 剔除存在特殊情形的公司
- 最终保留 5-10 家

#### 2. 收集财务信息

**所需数据：**
- 当前股价和流通股数量
- 最新财年财务报表
- 下一年，NTM，一致预期
- 历史增长率

**计算市场指标：**
- Market Cap = Share Price × Shares Outstanding
- Enterprise Value = Market Cap + Debt + Minority Interest + Preferred - Cash
- Net Debt = Total Debt - Cash & Equivalents

#### 3. 计算估值倍数

**Enterprise Value Multiples：**
- **EV/Revenue**：适用于早期 / 高增长公司
- **EV/EBITDA**：最常用；适用于资本密集型业务
- **EV/EBIT**：当 D&A 差异较大时更有用

**Equity Value Multiples：**
- **P/E (Price/Earnings)**：应用最广
- **P/B (Price/Book)**：适用于金融机构
- **P/S (Price/Sales)**：适用于尚未盈利的公司

**计算口径：**
- Last Twelve Months (LTM)，历史口径
- Next Twelve Months (NTM)，前瞻口径，通常优先采用

#### 4. 分析并选择倍数

**建立 Comparable Company Table：**

| Company | Market Cap | EV/Revenue | EV/EBITDA | EV/EBIT | P/E (NTM) | Revenue Growth | EBITDA Margin |
|---------|-----------|------------|-----------|---------|-----------|----------------|---------------|
| Comp A  | $10B      | 3.5x       | 12.0x     | 18.0x   | 22.0x     | 15%            | 28%           |
| Comp B  | $8B       | 3.0x       | 10.5x     | 16.0x   | 19.0x     | 12%            | 27%           |
| ...     | ...       | ...        | ...       | ...     | ...       | ...            | ...           |
| Median  | -         | **3.2x**   | **11.0x** | **17.0x** | **20.5x** | 13%            | 27.5%         |

**调整：**
- 剔除离群值，通常是超过 2 个标准差的值
- 考虑使用 median 而不是 mean，避免被离群值扭曲
- 如果部分 comps 更接近目标，可对倍数赋予更高权重
- 根据增长、利润率、风险差异进行调整

#### 5. 将倍数应用于目标公司

**示例计算：**
```
Target Company NTM EBITDA = $500M
Selected EV/EBITDA Multiple = 11.0x
Implied Enterprise Value = $500M × 11.0x = $5,500M

Less: Net Debt = $1,000M
Equity Value = $4,500M

Shares Outstanding = 100M
Implied Price Per Share = $45.00
```

#### 6. 选择合适的倍数

**根据以下情况选择：**
- **EV/Revenue**：高增长、亏损公司，例如 tech、pre-profit biotech
- **EV/EBITDA**：最常见，用于资本密集型行业，如制造、通信
- **P/E**：适用于盈利稳定、资本结构稳定的公司，如消费、零售
- **Sector-specific**：银行看 P/B，油气看 EV/Production，媒体看 EV/Subscriber

### Premium / Discount Analysis

可以基于以下因素施加溢价或折价：
- **Growth premium**：增长越高，倍数越高
- **Profitability**：利润率越高，倍数越高
- **Size**：大公司通常享受溢价，流动性因素
- **Market position**：市场领导者通常有溢价
- **Geographic**：发达市场 vs. 新兴市场

---

## Precedent Transactions Analysis

### 概览

Precedent transactions 基于并购交易中为类似公司支付的价格进行估值。它反映控制权溢价和战略价值。

### 分步流程

#### 1. 识别相关交易

**选择标准：**
- 同一或相似行业
- 相近规模，通常为目标公司的 0.5x 到 2x
- 相似业务特征
- 较近时间内的交易，最好是过去 3-5 年
- 已公告且已完成的交易，避免撤销交易

**典型样本池：**
- 至少 5-10 笔交易
- 重点参考近期交易，对较新交易赋予更高权重

#### 2. 收集交易细节

**所需信息：**
- 交易日期，公告日与完成日
- 收购价格和交易结构，现金、股票或混合
- 目标公司在交易时点的财务数据
- 战略逻辑与协同效应
- 支付的控制权溢价

**来源：**
- SEC filings，S-4、8-K、proxy statements
- Press releases 和 investor presentations
- 并购数据库，CapIQ、FactSet、Bloomberg

#### 3. 计算交易倍数

**采用与 trading comps 相同的倍数，但基于交易价值：**

```
Transaction Value = Equity Purchase Price + Assumed Debt - Cash Acquired

EV/Revenue (LTM) = Transaction Value / Target's LTM Revenue
EV/EBITDA (LTM) = Transaction Value / Target's LTM EBITDA
EV/EBIT (LTM) = Transaction Value / Target's LTM EBIT
```

**计算控制权溢价：**
```
Control Premium = (Offer Price - Unaffected Price) / Unaffected Price
```
- Unaffected Price = 公告前 1-2 天目标公司的股价
- Typical range：20-40%

#### 4. 分析 precedent transactions

**建立 Precedent Transactions Table：**

| Date | Target | Acquirer | Deal Value | EV/Revenue | EV/EBITDA | Premium | Rationale |
|------|--------|----------|------------|------------|-----------|---------|-----------|
| Q1'24 | CompX | BuyerA | $5.0B | 4.0x | 14.0x | 35% | Market consolidation |
| Q3'23 | CompY | BuyerB | $3.5B | 3.5x | 12.5x | 28% | Strategic fit |
| Median | - | - | - | **3.8x** | **13.0x** | **31%** | - |

#### 5. 应用于目标公司

**重要考虑：**
- Precedent multiples 通常高于 trading comps，因为包含控制权溢价
- 需要根据交易逻辑差异进行调整
- 考虑交易时的市场环境与当前市场环境是否不同
- 对近期交易赋予更高权重

**示例计算：**
```
Target Company LTM EBITDA = $450M
Selected EV/EBITDA Multiple = 13.0x (precedent)
vs Trading Comps Multiple = 11.0x

Implied EV (Precedent) = $450M × 13.0x = $5,850M
Implied EV (Trading) = $450M × 11.0x = $4,950M

Implied Control Premium = $5,850M / $4,950M - 1 = 18%
```

### 对交易倍数的调整

**可考虑基于以下因素进行调整：**
- **Market conditions**：牛市 vs. 熊市，并购活跃程度
- **Deal structure**：战略买家 vs. 财务买家
- **Synergies**：高协同交易往往对应更高溢价
- **Competitive dynamics**：单一买家 vs. 多方竞购
- **Time value**：越老的交易相关性越弱

---

## Valuation Reconciliation

### 建立 Valuation Bridge

将三种方法放在统一框架中呈现：

**示例估值汇总：**

| Method | Enterprise Value | Equity Value | Price/Share | Weight | Implied Value |
|--------|------------------|--------------|-------------|--------|---------------|
| DCF Analysis | $5,200M | $4,200M | $42.00 | 50% | $21.00 |
| Trading Comps | $5,500M | $4,500M | $45.00 | 30% | $13.50 |
| Precedent Trans. | $5,850M | $4,850M | $48.50 | 20% | $9.70 |
| **Weighted Avg** | - | - | **$44.20** | - | **$44.20** |

### 各方法权重

**Typical Weighting：**
- **DCF**：40-60%，体现基本面价值，但依赖预测准确性
- **Trading Comps**：25-40%，反映当前市场情绪
- **Precedent Trans.**：15-25%，除非 M&A 可能性较高，否则权重较低

**根据以下因素调整权重：**
- **Confidence in forecasts**：对预测越有信心，DCF 权重越高
- **Market conditions**：牛 / 熊市会影响 comps 的可靠性
- **M&A likelihood**：若公司可能成为收购目标或行业在整合，则权重更高
- **Company maturity**：成熟公司更偏重 comps；成长公司更偏重 DCF

### 估值区间

始终给出估值区间，而不是单点估值：

**方法：**
- **Base Case**：最可能出现的情景
- **Bull Case**：乐观假设，收入增长、利润率更强
- **Bear Case**：保守假设

**示例：**
```
Bear Case: $38 - $40
Base Case: $42 - $46
Bull Case: $48 - $52

Recommendation: BUY with target price of $45 (midpoint of base case)
```

### Sanity Checks

**从以下维度交叉验证估值：**
1. **Historical multiples**：当前估值是否与历史区间相符？
2. **Peer comparison**：相对 peers 的溢价 / 折价是否合理？
3. **Implied growth**：市场当前价格隐含了怎样的增长预期？
4. **Implied returns**：从当前价格到目标价的 IRR 是多少？
5. **Market cap analysis**：对应的总市值是否合理？

---

## 结论

同时使用这三种估值方法，可以形成更稳健的公允价值判断框架：

- **DCF** 提供基于基本面的内在价值
- **Trading Comps** 反映当前市场估值
- **Precedent Transactions** 反映并购价值与控制权溢价

关键在于理解驱动各方法的假设，并提出一个经过充分论证的估值区间，覆盖多种情景和方法论。
