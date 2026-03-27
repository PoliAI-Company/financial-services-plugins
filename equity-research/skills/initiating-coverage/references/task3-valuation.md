# 任务 3：估值分析 - 详细工作流

本文档提供执行 initiating-coverage skill 中 Task 3（Valuation Analysis）的逐步说明。

## 任务概览

**目的**：使用 DCF、comparables 和 precedent transactions 进行综合估值。

**前置条件**：⚠️ 开始前验证
- **必需**：Task 2 的财务模型
  - 预测 income statements
  - 预测 cash flows
  - Revenue 和 EBITDA forecasts
  - DCF inputs，unlevered FCF

**⚠️ 关键要求：在 TASK 2 完成前，不得开始本任务**

本任务依赖 Task 2 的财务模型。没有模型就开始会导致工作不完整。

**如果 TASK 2 尚未完成**：立即停止，并告知用户必须先完成 Task 2（Financial Modeling）。不要尝试继续，也不要创建占位式估值。

**输出**：估值分析（4-6 页 + Excel 标签页）
- DCF analysis，含 sensitivity tables
- Comparable companies analysis
- Precedent transactions，如适用
- Valuation football field
- Price target 和 recommendation

---

## 输入验证

**开始前检查：**
- [ ] Task 2 完成了吗？财务模型存在
- [ ] 模型文件路径 / 位置已知？
- [ ] 可以从模型中访问 projected financials？

**模型中必须具备：**
- [ ] 5 年 projected FCF
- [ ] Revenue projections
- [ ] EBITDA projections
- [ ] Terminal year metrics
- [ ] Balance sheet data，debt、cash、shares

**IF VERIFICATION FAILS**：停止，并先完成 Task 2（Financial Modeling）。

---

## 详细方法参考

如需深入了解估值方法、公式和理论，请参见：
**[valuation-methodologies.md](valuation-methodologies.md)**

本工作流文件聚焦执行步骤。方法论文件涵盖：
- DCF 理论与公式
- WACC 计算细节
- Terminal value 方法
- Comparable companies 理论
- Precedent transactions 理论

---

## 分步估值工作流

### 第 1 步：从财务模型中提取数据

**从 Task 2 的财务模型中提取：**

1. **Projected Financials（5 年）**
   - 按年份 Revenue（2025E-2029E）
   - EBITDA 按年
   - EBIT 按年
   - Tax rate
   - D&A 按年
   - CapEx 按年
   - Change in NWC 按年

2. **Unlevered Free Cash Flow**
   ```
   从财务模型的 DCF Inputs tab 提取：

                   2025E   2026E   2027E   2028E   2029E
   EBIT            $XXX    $XXX    $XXX    $XXX    $XXX
   × (1 - Tax Rate)
   = NOPAT         $XXX    $XXX    $XXX    $XXX    $XXX
   + D&A           $XXX    $XXX    $XXX    $XXX    $XXX
   - CapEx         ($XX)   ($XX)   ($XX)   ($XX)   ($XX)
   - Chg in NWC    ($XX)   ($XX)   ($XX)   ($XX)   ($XX)
   = Unlevered FCF $XXX    $XXX    $XXX    $XXX    $XXX
   ```

3. **Balance Sheet Data（当前）**
   - Total debt
   - Cash & equivalents
   - Net debt，Debt - Cash
   - Diluted shares outstanding

4. **Scenario Data**
   - Bull case revenue CAGR 和 terminal margin
   - Base case revenue CAGR 和 terminal margin
   - Bear case revenue CAGR 和 terminal margin

### 第 2 步：建立 DCF Analysis

#### A. 计算 WACC

**1. 确定 Risk-Free Rate**
   - 使用 10-year Treasury yield，查当前利率
   - 例如 late 2024 的 4.0-4.5%

**2. 确定 Cost of Equity（CAPM）**
   ```
   Cost of Equity = Risk-Free Rate + Beta × Equity Risk Premium

   Inputs:
   - Risk-Free Rate: [Current 10-year Treasury, e.g., 4.2%]
   - Beta: [Company beta from Bloomberg/FactSet or peer average]
   - Equity Risk Premium: 5-6% (historical average)

   Example:
   Cost of Equity = 4.2% + 1.3 × 5.5% = 11.35%
   ```

**3. 确定 Cost of Debt**
   ```
   Cost of Debt = Current borrowing rate or implied yield on bonds

   For private companies:
   Cost of Debt = Risk-Free Rate + Credit Spread (based on rating)

   Example:
   Cost of Debt (pre-tax) = 6.5%
   Cost of Debt (after-tax) = 6.5% × (1 - 25% tax rate) = 4.875%
   ```

**4. 确定 Capital Structure**
   ```
   使用 market values，而不是 book values：

   Market Value of Equity (E) = Share Price × Shares Outstanding
   Market Value of Debt (D) = Total Debt (如果债券不交易则可用账面值)
   Total Value (V) = E + D

   Weight of Equity = E / V
   Weight of Debt = D / V

   Example:
   E = $5,000M (90.9%)
   D = $500M (9.1%)
   V = $5,500M (100%)
   ```

**5. 计算 WACC**
   ```
   WACC = (E/V × Cost of Equity) + (D/V × Cost of Debt × (1 - Tax Rate))

   Example:
   WACC = (90.9% × 11.35%) + (9.1% × 6.5% × (1 - 25%))
   WACC = 10.32% + 0.44% = 10.76%

   Round to: 10.8% for base case
   ```

#### B. 计算 Terminal Value

**Method 1: Perpetuity Growth（优先）**
```
Terminal Value = FCF(2029) × (1 + g) / (WACC - g)

Where:
- FCF(2029) = Final year unlevered FCF from model
- g = Perpetual growth rate (typically 2.0-3.0%)
  - Should not exceed long-term GDP growth
  - Use 2.5% as base case

示例：
FCF(2029) = $500M
g = 2.5%
WACC = 10.8%

Terminal Value = $500M × (1.025) / (0.108 - 0.025)
Terminal Value = $512.5M / 0.083 = $6,175M
```

**Method 2: Exit Multiple（替代法）**
```
Terminal Value = EBITDA(2029) × Exit Multiple

Where:
- Exit Multiple = Current peer trading median (e.g., 12-15x EBITDA)

示例：
EBITDA(2029) = $800M
Exit Multiple = 13x

Terminal Value = $800M × 13x = $10,400M
```

**可选择其中一种方法，或取两者平均。**

#### C. 将现金流折现到现值

```
PV of Projected FCF = Σ [FCFt / (1 + WACC)^t] for t = 1 to 5

示例：
Year    FCF      Discount    PV of FCF
        ($M)     Factor      ($M)
2025    $250     1/(1.108)^1 = 0.9026    $226
2026    $320     1/(1.108)^2 = 0.8147    $261
2027    $390     1/(1.108)^3 = 0.7353    $287
2028    $450     1/(1.108)^4 = 0.6636    $299
2029    $500     1/(1.108)^5 = 0.5988    $299
                              Total PV:  $1,372M

PV of Terminal Value = Terminal Value / (1 + WACC)^5
PV of Terminal Value = $6,175M / (1.108)^5 = $6,175M × 0.5988 = $3,697M

Enterprise Value = $1,372M + $3,697M = $5,069M
```

#### D. 计算 Equity Value 与 Price Per Share

```
Enterprise Value                 $5,069M
- Net Debt (Debt - Cash)         ($450M)
+ Non-operating Assets           $0M
- Minority Interest              $0M
- Preferred Stock                $0M
= Equity Value                   $4,619M

Diluted Shares Outstanding       100M

Price Per Share = $4,619M / 100M = $46.19

Current Stock Price: $42.00
Implied Upside: 10.0%
```

#### E. DCF Sensitivity Analysis **CRITICAL**

**Table 1: WACC vs. Terminal Growth Rate**

创建双变量敏感性表：
```
Price Per Share ($)     Terminal Growth Rate
WACC        1.5%    2.0%    2.5%    3.0%    3.5%
9.0%        $52     $55     $59     $63     $68
9.5%        $48     $51     $54     $58     $62
10.0%       $45     $48     $51     $54     $57
10.5%       $42     $45     $47     $50     $53
11.0%       $40     $42     $44     $47     $50
11.5%       $38     $40     $42     $44     $47
12.0%       $36     $38     $40     $42     $44

Base Case: WACC = 10.8%, g = 2.5% → $46
Format as heatmap: Green (high values) → Yellow → Red (low values)
```

**Table 2: Revenue CAGR vs. Terminal EBITDA Margin**
```
Price Per Share ($)     Terminal EBITDA Margin (2029E)
Revenue CAGR    28%     30%     32%     34%     36%
15%             $38     $42     $46     $50     $54
20%             $42     $46     $51     $56     $61
25%             $46     $51     $56     $62     $68
30%             $51     $56     $62     $68     $75
35%             $56     $62     $68     $75     $83

Base Case: Rev CAGR = 25%, EBITDA Margin = 32% → $56
```

### 第 3 步：Comparable Companies Analysis

#### A. 选择 Comparable Companies

**选择标准：**
- 同行业 / 同板块，这是首要要求
- 相似商业模式
- 可比规模，market cap、revenue
- 相似增长轮廓
- 相似地域分布

**识别 5-10 家 peers：**
1. [Peer 1] - 直接竞争对手
2. [Peer 2] - 直接竞争对手
3. [Peer 3] - 邻近玩家
4. [Peer 4] - 相似商业模式
5. [Peer 5] - 区域竞争者
6. [再补 3-5 家]

**记录每个 peer 的选择逻辑。**

#### B. 收集 Peer Financial Data

**对每个 comparable，收集：**
- 当前股价
- Shares outstanding（diluted）
- Market capitalization
- Total debt 和 cash，用于 EV 计算
- Enterprise value
- LTM（Last Twelve Months）财务数据：
  - Revenue
  - EBITDA
  - EBIT
  - Net Income
- NTM（Next Twelve Months）一致预期
- Revenue growth rate
- EBITDA margin

**数据来源：**
- FactSet、CapitalIQ、Bloomberg，优先
- Company 10-Ks / 10-Qs，用于 actuals
- 若缺少专业工具，可用 Yahoo Finance、Seeking Alpha 获取 consensus estimates

#### C. 计算估值倍数

**对每个 peer，计算：**
```
EV/Revenue (LTM) = Enterprise Value / LTM Revenue
EV/Revenue (NTM) = Enterprise Value / NTM Revenue (est.)
EV/EBITDA (LTM) = Enterprise Value / LTM EBITDA
EV/EBITDA (NTM) = Enterprise Value / NTM EBITDA (est.)
P/E (NTM) = Market Cap / NTM Net Income (est.)
```

#### D. 创建 Comparable Companies Table（MANDATORY FORMAT）

```
COMPARABLE COMPANIES ANALYSIS

Company      Ticker  Mkt Cap  EV/Rev  EV/Rev  EV/EBITDA  EV/EBITDA  P/E   Rev     EBITDA
                     ($B)     LTM     NTM     LTM        NTM        NTM   Growth  Margin
Peer A       PRA     45.2     3.5x    3.2x    15.2x      13.8x      25x   18%     23%
Peer B       PRB     32.8     3.2x    2.9x    14.1x      12.5x      22x   15%     23%
Peer C       PRC     28.5     2.8x    2.6x    12.8x      11.2x      20x   12%     22%
Peer D       PRD     52.1     4.1x    3.7x    17.5x      15.2x      29x   22%     23%
Peer E       PRE     38.9     3.6x    3.3x    15.8x      14.1x      25x   17%     23%
Peer F       PRF     41.2     3.7x    3.4x    16.1x      13.9x      26x   19%     23%
Peer G       PRG     35.5     3.3x    3.0x    14.5x      12.8x      23x   16%     22%

[Target]     TRGT    38.0     3.4x    3.1x    14.8x      13.0x      24x   17%     23%

STATISTICAL SUMMARY
Maximum              52.1     4.1x    3.7x    17.5x      15.2x      29x   22%     23%
75th Percentile      45.2     3.7x    3.4x    16.1x      14.1x      26x   19%     23%
Median               38.9     3.5x    3.2x    15.2x      13.8x      25x   17%     23%
25th Percentile      32.8     3.2x    2.9x    14.1x      12.5x      22x   15%     22%
Minimum              28.5     2.8x    2.6x    12.8x      11.2x      20x   12%     22%

Note: Market data as of [Date]. LTM = Last Twelve Months. NTM = Next Twelve Months.
Source: FactSet, company filings, [Analyst] estimates.
```

**CRITICAL**：statistical summary，max/75th/median/25th/min，**是强制项**。

#### E. 将倍数应用到目标公司

**选择主要倍数**，成熟公司通常使用 EV/EBITDA：

```
Target Company NTM EBITDA = $550M (from financial model)

Apply Median Peer Multiple:
Peer Median EV/EBITDA (NTM) = 13.8x
Implied EV = $550M × 13.8x = $7,590M

Apply 25th Percentile (Conservative):
25th Percentile EV/EBITDA (NTM) = 12.5x
Implied EV = $550M × 12.5x = $6,875M

Apply 75th Percentile (Optimistic):
75th Percentile EV/EBITDA (NTM) = 14.1x
Implied EV = $550M × 14.1x = $7,755M

Valuation Range (Comps): $6,875M - $7,755M
Midpoint: $7,315M

Convert to Equity Value:
Implied EV (Median)        $7,590M
- Net Debt                 ($450M)
= Implied Equity Value     $7,140M

Shares Outstanding         100M
Implied Price/Share        $71.40
```

**论证溢价 / 折价：**
- 目标公司增长 17%，与 peer median 17% 相同 → In-line
- 目标 EBITDA margin 为 23%，与 peer median 23% 相同 → In-line
- 目标 market position → [据此论证 premium/discount]
- **Conclusion**：使用 median multiple，不做调整

### 第 4 步：Precedent Transactions（可选）

**Note**：仅当 M&A 对该板块 / 公司具有现实意义时适用。

#### A. 识别相关交易

**搜索 5-10 笔 M&A 交易：**
- 同一行业，过去 3-5 年内
- 相似规模，目标公司的 0.5x 到 2x
- 已公告且已完成的交易

**示例：**
```
PRECEDENT TRANSACTIONS ANALYSIS

Date     Target        Acquirer      Deal     EV/Rev  EV/EBITDA  Premium  Rationale
                                    Value($B)  LTM     LTM
Q1 2024  Comp A       Strategic      $5.2B    4.2x    16.5x      35%      Consolidation
Q3 2023  Comp B       PE Firm        $3.8B    3.8x    14.2x      28%      Platform
Q4 2023  Comp C       Strategic      $4.5B    4.0x    15.8x      32%      Geographic
Q2 2023  Comp D       Strategic      $6.1B    4.5x    17.2x      38%      Strategic fit
Q1 2023  Comp E       PE Firm        $3.2B    3.5x    13.5x      25%      Carve-out

Median                                        4.0x    15.8x      32%

Source: CapitalIQ, company filings, press releases.
```

#### B. 应用于目标公司

```
Target Company LTM EBITDA = $500M
Precedent Median EV/EBITDA (LTM) = 15.8x

Implied EV (Precedent) = $500M × 15.8x = $7,900M

Note: Precedent multiples typically 10-20% higher than trading comps
due to control premium and synergies.
```

### 第 5 步：Valuation Reconciliation

#### A. 创建 Valuation Summary Table

```
VALUATION SUMMARY

Method                  Low     Base    High    Weight  Weighted Value
DCF Analysis            $42     $46     $51     50%     $23.00
Trading Comps (NTM)     $64     $71     $78     40%     $28.40
Precedent Trans.        $70     $79     $88     10%     $7.90
                                                        -------
Weighted Average Target                         100%    $59.30

Rounded Price Target: $59.00

Current Price (as of [Date]):    $42.00
Upside to Target:                40% ($59.00 / $42.00 - 1)
```

#### B. 确定权重逻辑

**Typical Weighting：**
- DCF：40-60%，当 forecasts 较可靠时权重更高
- Trading Comps：25-40%，反映市场情绪
- Precedent Trans：10-25%，除非 M&A 可能性高，否则权重较低

**在该示例中：**
- DCF 50%：对预测有较高信心
- Comps 40%：peer set 充足
- Precedent 10%：短期内 M&A 可能性不高

#### C. 创建 Valuation Football Field Chart

```
VALUATION FOOTBALL FIELD

Method                  Low ◄────────── Range ──────────► High

DCF Analysis            $42 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ $51

Trading Comps (NTM)     $64 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ $78

Precedent Trans.        $70 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ $88
                                          ↑
                                    Current: $42
─────────────────────────────────────────────────────────
Valuation Range         $42                          $88
Price Target: $59 (weighted average)

Color code:
- DCF: Blue
- Trading Comps: Green
- Precedent Trans: Orange
- Vertical line at current price: Red dashed
- Vertical line at target: Black solid
```

#### D. 按情景划分估值

```
VALUATION BY SCENARIO

Scenario    Probability  Revenue  EBITDA    DCF      Comps    Weighted
                        CAGR     Margin    Value    Multiple  Avg
Bear Case   20%         18%      28%       $38      11.5x     $42
Base Case   60%         25%      32%       $46      13.8x     $59
Bull Case   20%         32%      36%       $58      16.0x     $82

Expected Value (probability-weighted): $59
```

### 第 6 步：最终 Price Target 与 Recommendation

```
═══════════════════════════════════════════════════════════
INVESTMENT RECOMMENDATION
═══════════════════════════════════════════════════════════

Current Price:          $42.00 (as of [Date])
Price Target:           $59.00 (12-month)
Upside/(Downside):      +40.5%

Rating:                 BUY / OUTPERFORM

Valuation Methodology:  Based on weighted average of DCF (50%),
                       trading comparables (40%), and precedent
                       transactions (10%).

Time Horizon:          12 months

───────────────────────────────────────────────────────────
KEY INVESTMENT CATALYSTS
───────────────────────────────────────────────────────────

1. New Product Launch (Q2 2025)
   - Expected to drive 15-20% revenue acceleration
   - Already seeing strong pre-orders

2. Margin Expansion (FY2025-2026)
   - Operating leverage from scale
   - Path to 35% EBITDA margin (from current 28%)

3. Market Share Gains (Ongoing)
   - Taking share from legacy competitors
   - Net Promoter Score improvement

4. International Expansion (H2 2025)
   - Entry into European markets
   - Potential $200M incremental revenue opportunity

5. Potential M&A Target (12-18 months)
   - Strategic fit for larger players
   - Precedent transactions suggest 30-40% premium

───────────────────────────────────────────────────────────
KEY RISKS TO PRICE TARGET
───────────────────────────────────────────────────────────

Downside Risks:
1. Competitive Pressure (High probability, -15% impact)
   - New entrant launched competing product
   - Could pressure pricing and market share

2. Execution Risk (Medium probability, -10% impact)
   - New product launch delays or underperformance
   - Management turnover

3. Macro Slowdown (Medium probability, -20% impact)
   - Economic recession would impact customer spending
   - Operating leverage would reverse

4. Regulatory Risk (Low probability, -25% impact)
   - Potential new regulations in key market
   - Would increase compliance costs

Upside Risks:
1. M&A Bid (Low probability, +35% impact)
   - Strategic acquirer pays control premium

2. Beat-and-Raise (Medium probability, +10% impact)
   - Consistent outperformance vs. estimates

═══════════════════════════════════════════════════════════
```

---

## 质量标准

### DCF Quality Checks
- [ ] WACC 计算正确，组成部分有记录
- [ ] Terminal value 合理，低于 total enterprise value 的 70%
- [ ] Sensitivity analysis 覆盖现实区间，WACC ±200-300bps，terminal growth ±100bps
- [ ] Unlevered FCF 从 EBIT 正确计算
- [ ] Enterprise 到 equity value 的桥接正确
- [ ] 使用 diluted shares，而不是 basic shares

### Comparables Quality Checks
- [ ] 已选出 5-10 家 comparable companies
- [ ] Peer 选择具备可辩护性，并记录原因
- [ ] 包含 statistical summary，max/75th/median/25th/min，强制项
- [ ] Multiple 选择合适，成熟公司用 EV/EBITDA，高增长公司用 EV/Revenue
- [ ] Premium / discount 有具体论证
- [ ] 数据来源与日期记录完整

### 整体估值质量检查
- [ ] 至少使用 2 种估值方法，最低 DCF + Comps
- [ ] 权重说明充分且合理
- [ ] 提供 low / base / high 估值区间，而非单点值
- [ ] 已进行 Bull/Base/Bear 情景分析
- [ ] 已做 sanity checks
- [ ] 所有关键假设都有逻辑说明

---

## Sanity Checks

**始终执行以下校验：**

1. **Historical Multiple Check**
   - 隐含倍数是否与公司历史交易区间一致？
   - 若不一致，解释原因

2. **Peer Comparison**
   - 相对 peers 的溢价 / 折价是否由基本面支撑？
   - 检查增长、利润率、市场地位

3. **Implied Growth Check**
   - 当前股价隐含了什么增长预期？
   - 该预期是否与公司轨迹相符？

4. **Market Cap Reasonableness**
   - 结合公司规模与 peers，总市值是否合理？
   - 是否会导致公司在行业中显得过大 / 过小？

5. **Terminal Value Check**
   - Terminal value 是否低于 total enterprise value 的 60-70%？
   - 若高于 70%，说明显性预测期可能太短

6. **WACC Reasonableness**
   - WACC 是否位于典型公司 8-14% 区间？
   - Tech / high-growth：10-14%
   - Mature / stable：7-10%

7. **Implied Returns Check**
   - 从当前股价到目标价，12 个月 IRR 是多少？
   - 是否与 recommendation rating 相匹配？

---

## 输出文件

创建以下交付物：

### 1. Valuation Analysis Document
**File**：`[Company]_Valuation_Analysis_[Date].md`（书面分析）

**内容**（4-6 页）：
- 含目标价的 executive summary
- DCF analysis（1 页），含 sensitivity table
- Comparable companies analysis（1 页），含 statistical summary
- Precedent transactions（0.5 页），如适用
- Valuation summary 和 football field（0.5 页）
- Investment recommendation（1 页）
- Key catalysts and risks（1 页）

### 2. Excel Valuation Tabs
**添加到 Task 2 的财务模型文件中：** `[Company]_Financial_Model_[Date].xlsx`

**IMPORTANT**：不要单独创建 Excel 文件。应直接向 Task 2 的现有财务模型中增加下列 tabs，以便所有定量数据集中在同一文件内。

**需要新增的 tabs：**
- DCF tab，完整计算
- Sensitivity analysis tab
- Comps tab，含 peer data
- Precedent transactions tab，如适用
- Valuation summary tab

---

## 成功标准

成功的估值分析应当：
1. 至少使用两种方法，最低为 DCF + Comps
2. 包含完整的 DCF 双变量 sensitivity analysis
3. comps 中包含 statistical summary，max/75th/median/25th/min
4. 给出 low / base / high 估值区间，而不是单点值
5. 所有关键假设均有清晰逻辑说明
6. 完成 sanity checks
7. 得出可辩护的 price target
8. 提供明确的 buy / hold / sell recommendation
9. 识别 3-5 个 key catalysts
10. 识别 3-5 个 key risks
11. 具备可审计性与透明度

---

## 下一步

完成 Task 3 后，估值分析将用于：
- **Task 4 (Charts)**：生成 DCF sensitivity heatmaps、valuation football field 和 scenario comparison charts
- **Task 5 (Report Assembly)**：将估值分析整合进最终报告

目标价与评级是最终股票研究报告中投资建议的核心基础。
