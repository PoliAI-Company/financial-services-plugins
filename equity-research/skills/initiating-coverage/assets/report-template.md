# 股票研究首次覆盖报告模板

本模板提供创建综合股票研究首次覆盖报告的结构。在构建最终报告文档时，请以此作为指南。

**NOTE：** 实际报告**必须**使用 DOCX skill 创建。不要生成 markdown 内容。

**关键要求：**
1. 在创建 Word 文档**之前**，先使用 Python（matplotlib/plotly）生成 20-30+ 张图表图片
2. **Use DOCX skill**：创建具有正确样式、页眉页脚和格式的专业报告
3. **嵌入真实图表图片**：将生成的 PNG/JPG 图表文件插入到 Word 文档中的合适位置
4. **NO MARKDOWN**：不要生成 markdown 内容。使用 DOCX skill 创建 `.docx` 文件。

**关键排版指导：**
- **MAXIMUM DENSITY**：每一页都应尽可能装载更多信息。文字、图表和表格要交错排布。
- **NO ORPHANED SECTIONS**：不要让章节标题单独占一页，也不要让单张图表独占一页。
- **20-30+ ACTUAL CHART IMAGES**：先把图表生成成图片文件，再通过 DOCX skill 将其嵌入正文。

---

## PAGE 1: INVESTMENT UPDATE（最重要的一页）

**CRITICAL**：第 1 页不是传统 executive summary，而是一页 **Investment Update**，采用专业股票研究机构常用的特定机构化格式。

**重要结构说明：**
- 这是 "Investment Update" 或 "Company Update" 页面，不是 "Executive Summary"
- 左上角使用 rating box
- 突出展示股价表现图（Figure 1）
- 包含 3-4 条使用 ■ 的详细 bullet points
- 每条 bullet 由 **粗体主题标题** + 3-5 句话解释组成
- 页面底部有 financial and valuation metrics table
- 所有图表都必须有 figure 编号（Figure 1、Figure 2 等）和 source line

### 布局结构

**左上角 - RATING BOX：**
```
Rating:             [OUTPERFORM / NEUTRAL / UNDERWEIGHT / etc.]
Price ([Date]):     $[XX.XX]
Target Price:       $[XX.XX]
52-Week Range:      $[XX.XX] - $[XX.XX]
Market Cap:         $[XX.X]B
Enterprise Value:   $[XX.X]B
```

**左上角 - RESEARCH ANALYSTS：**
```
[Name], [Credentials (Ph.D., CFA, M.D., etc.)]
[Email] | [Phone]

[Name 2], [Credentials]
[Email] | [Phone]
```

**右上角 - STOCK PRICE PERFORMANCE：**
```
Figure 1 - [Company Name] Stock Price Performance
[Line chart showing stock price over 12-24 months with benchmark comparison]
Source: Company data, [Firm Name] estimates.
```

**主体内容 - 灰色标题栏：**
```
[OUTPERFORM / NEUTRAL / etc.] RECOMMENDATION / COMPANY UPDATE
```

**主体内容 - 详细 bullets（3-4 条）：**

使用 ■ 字符，每条 bullet 采用以下格式：
```
■ **[Bold Topic Header capturing main point].** 正文解释部分用 3-5 句话展开，包含具体数字、对比和分析。尽可能用数字开头并进行量化。使用 "vs." 而不是 "versus"。内容要具体、明确。

■ **[Second Topic Header].** [3-5 句详细解释...]

■ **[Third Topic Header].** [3-5 句详细解释...]

■ **[Fourth Topic Header - Optional].** [3-5 句详细解释...]
```

**EXAMPLE BULLET FORMAT：**
```
■ **Vertical SaaS leadership and regulatory moat should enable $50bn+ TAM by 2030.**
Deep domain expertise in healthcare IT, strong customer retention (95%+ net revenue retention),
and cross-sell capabilities have driven Acme Health's market expansion. With the healthcare IT
market expected to reach $50bn+ by 2030, Acme Health is well-positioned to capture share given
its regulatory moat and high switching costs. Management has indicated that 70% of current
revenue comes from enterprise hospital systems, suggesting strong product-market fit.
```

**底部区域 - 财务与估值指标表：**
```
                            [Year-3]A   [Year-2]A   [Year-1]A   [Year]E    [Year+1]E
Revenue ($M)                [X]         [X]         [X]         [X]        [X]
Revenue Growth (%)          X.X%        X.X%        X.X%        X.X%       X.X%
Gross Margin (%)           X.X%        X.X%        X.X%        X.X%       X.X%
EBITDA ($M)                [X]         [X]         [X]         [X]        [X]
EBITDA Margin (%)          X.X%        X.X%        X.X%        X.X%       X.X%
EPS ($)                    X.XX        X.XX        X.XX        X.XX       X.XX
P/E (x)                    XX.Xx       XX.Xx       XX.Xx       XX.Xx      XX.Xx
EV/Revenue (x)             X.Xx        X.Xx        X.Xx        X.Xx       X.Xx
EV/EBITDA (x)              XX.Xx       XX.Xx       XX.Xx       XX.Xx      XX.Xx

Note: Use "A" suffix for actual/historical years, "E" suffix for estimated/projected years
Source: Company data, [Firm Name] estimates.
```

---

## FIGURE 编号与格式标准

**CRITICAL**：所有图、图表和表格都必须遵循专业股票研究中的严格编号规范。

### Figure 编号格式

**每个图表 / 表格都必须包含：**
1. **连续编号**：Figure 1、Figure 2、Figure 3 等，整篇报告连续编号
2. **描述性标题**："Figure X - [Company] [Specific Metric] [Type of Chart/Analysis]"
3. **来源行**（始终位于底部）："Source: Company data, [Firm Name] estimates."

**示例：**
- Figure 1 - [Company] Stock Price Performance
- Figure 2 - [Company] Historical and Projected Revenue Mix by Product
- Figure 3 - [Company] Revenue by Geographic Region
- Figure 4 - [Product Name] Revenue and Price per Patient per Year
- Figure 5 - [Company] Gross Margin Evolution
- Figure 6 - DCF Sensitivity Analysis ($/share)
- Figure 7 - Valuation Football Field

### Caption 格式

```
Figure X - [Descriptive Title]
[Chart/Table/Graph content]
Source: Company data, [Firm Name] estimates.
```

对于包含多个数据来源的表格：
```
Figure X - [Descriptive Title]
[Table content]
Source: Company filings, FactSet, [Firm Name] estimates.
```

### 放置指导

- Figures 必须按在报告中的出现顺序编号
- 第一张图（Figure 1）通常是第 1 页上的股价图或收入增长图
- 每个 figure 的 caption 必须直接放在图形下方
- source line 应使用更小字号、斜体，并放在 figure 最底部

---

## PAGE 2: 目录

```
Executive Summary....................................................1
Investment Thesis & Risks..........................................3
Company Overview.......................................................6
  Business Description & History................................6
  Management & Ownership..........................................8
  Products & Technology...........................................9
  Customers & Go-to-Market......................................11
Growth Outlook & Drivers...........................................13
Financial Analysis & Performance.................................16
  Historical Performance........................................16
  Financial Projections.........................................19
Industry Overview & Competitive Landscape.....................21
  Market Size & TAM..............................................21
  Competitive Analysis..........................................23
  Industry Trends................................................25
Valuation Analysis..................................................27
Appendices & Disclosures...........................................31
```

---

## PAGES 3-5: INVESTMENT THESIS & RISKS

**布局原则**：在本部分中穿插文字和 2-3 张图表。每页都应同时有文字和图形。不要出现纯文字页或纯图表页。

### Investment Thesis

**[Thesis Pillar 1]: [Title - e.g., "Large and Growing TAM"]**

[用关键统计数字开头的首句]

[第 1 段：市场机会量化]
- 当前市场规模
- 增长驱动因素
- 公司的定位

[第 2 段：公司为何能获得份额]
- 竞争优势
- Go-to-market strategy
- 早期 traction / 证明点

[第 3 段：财务影响]
- 收入机会
- 利润率轮廓
- 时间线

**[EMBED CHART: TAM Growth Chart]** - 用 stacked area chart 展示市场规模演进及公司的机会空间

**[Thesis Pillar 2]: [Title - e.g., "Differentiated Technology/Product"]**

[采用类似结构，3 段说明机会、竞争定位和财务影响]

**[EMBED CHART: Competitive Positioning Matrix]** - 2×2 图，展示公司与竞争对手在关键维度上的位置

**[Thesis Pillar 3]: [Title - e.g., "Strong Execution and Management"]**

[类似结构]

**[如有需要，再加 2-3 个 pillars]**

**[EMBED CHART: Margin Expansion Pathway]** - 瀑布图或折线图，展示利润率改善路径

### Investment Risks

**Company-Specific Risks**

**[Risk 1]: [Title - e.g., "Customer Concentration"]**
[风险描述，尽可能量化影响，并说明缓释因素。2-3 句话。]

**[Risk 2]: [Title - e.g., "Execution Risk on Product Roadmap"]**
[描述，2-3 句话。]

**[Risk 3-5]: [Additional company-specific risks]**
[继续，合计 3-5 个公司特有风险]

**Industry/Market Risks**

**[Risk 1]: [Title - e.g., "Regulatory Uncertainty"]**
[描述，2-3 句话。]

**[Risk 2]: [Title - e.g., "Intense Competition"]**
[描述，2-3 句话。]

**[Risk 3-4]: [Additional industry/market risks]**
[继续，合计 2-4 个行业 / 市场风险]

---

## PAGES 8-19: COMPANY 101

### 公司描述（1 页）

**Overview**
[3-4 段说明：
- 公司是做什么的，用通俗语言
- 它如何赚钱
- 谁是它的客户
- 业务覆盖哪些地区
- 规模指标]

**Business Model Diagram/Visual**
[插入展示公司如何创造价值的可视化图]

### Company History（2-3 页）

**The Early Days: [Founding Story Title]**

[介绍创立背景：谁、何时、为什么、在哪里]

**Timeline of Key Milestones**

```
[Year]: [Founding event, initial funding]
[Year]: [Product launch, key milestone]
[Year]: [Major partnership, funding round]
[Year]: [Geographic expansion, new product]
[Year]: [Recent achievement]
```

**[Major Turning Point or Pivot]**
[如适用，描述任何重大战略转型]

**[Company Name] Today: [Current State Title]**
[描述公司当前地位、近期进展和当前战略的若干段落]

### Management & Ownership（2 页）

**Key Executives**

对于每位高管：
```
[Name] - [Title]
[Bio paragraph including:
- Current role and responsibilities
- Prior experience and track record
- Key accomplishments at company
- Education/credentials]
```

**Corporate Structure & Governance**
- 实体类型，C-Corp、PBC 等
- 董事会构成
- 特殊治理安排
- [如适用，加入治理结构图]

**Ownership Structure** [如有披露]
- 主要股东及持股比例
- 战略投资者
- 员工持股
- 内部人持股趋势

### Core Technology/Products（2-3 页）

**Technology Overview**
[描述核心技术 / 平台]

**Product Portfolio**

针对每项主要产品：
```
[Product Name]

描述：
[What it does, key features]

Target Customers:
[Who uses it, use cases]

Pricing Model:
[How it's priced, typical contract values]

Competitive Positioning:
[How it compares to alternatives]

Traction:
[Customers, revenue, growth metrics]
```

**Product Roadmap**
[未来待推出的产品 / 功能]

### Customers & Distribution（2-3 页）

**Customer Base**
- Total customers: [number]
- Customer segments（Enterprise、Mid-Market、SMB）
- 地域分布
- 客户案例 / 证言

**Go-to-Market Strategy**
- 销售渠道，直销、合作伙伴等
- 销售周期与 CAC
- 关键分发合作伙伴
- 营销策略

**Customer Economics**
- LTV/CAC ratio
- Net retention rate
- Churn rates
- Expansion rates

---

## PAGES 20-22: GROWTH OUTLOOK

### Growth Framework Overview

**短期增长驱动（1-2 年）**
1. [Driver 1]
2. [Driver 2]
3. [Driver 3]

**中期增长驱动（3-5 年）**
1. [Driver 1]
2. [Driver 2]

### Detailed Growth Driver Analysis

**[Growth Driver 1]: [Title]**

*Current State:*
[基线指标、当前表现]

*Opportunity:*
[市场规模、公司定位、增长潜力]

*Timeline & Milestones:*
- 近期（1-2 年）：[预期进展]
- 中期（3-5 年）：[预期进展]

*Risks & Challenges:*
[可能阻止该机会兑现的因素]

**[对每个主要增长驱动重复此结构]**

### Financial Projections

**Revenue Build-up**
[展示收入如何从当前水平增长到预测水平的可视化]

**Scenario Analysis**
[展示 Bear/Base/Bull 情景预测的表格或图]

---

## PAGES 21-24: FINANCIAL ANALYSIS & PERFORMANCE

**布局原则**：这一部分必须非常密集，穿插 5-7 张图表和财务表格。每页都应有多个元素，表格 + 1-2 张图。

### Historical Financial Analysis

**Income Statement Highlights（3-5 年历史）**
```
                    2021    2022    2023    2024    LTM
Revenue ($M)        [X]     [X]     [X]     [X]     [X]
  Growth %          -       X%      X%      X%      X%
Gross Profit ($M)   [X]     [X]     [X]     [X]     [X]
  Margin %          X%      X%      X%      X%      X%
EBITDA ($M)         [X]     [X]     [X]     [X]     [X]
  Margin %          X%      X%      X%      X%      X%
Net Income ($M)     [X]     [X]     [X]     [X]     [X]
  Margin %          X%      X%      X%      X%      X%
FCF ($M)            [X]     [X]     [X]     [X]     [X]
```

**[CHART 1: Revenue Growth Trajectory]**
折线图，展示历史收入并标注关键里程碑，图中可直接标注增长率。

**[CHART 2: REVENUE BY PRODUCT/SEGMENT]** ⭐ 关键图表
Stacked area chart，展示按产品线或业务分部拆分的收入结构随时间变化。该图用于展示业务 mix shift，以及哪些产品在驱动增长。
```
Example segments:
- Product A Revenue
- Product B Revenue
- Product C Revenue
- Services Revenue
```

**[CHART 3: REVENUE BY GEOGRAPHY]** ⭐ 关键图表
Stacked bar chart，展示按 geographic region 拆分的收入变化。
```
Example regions:
- North America
- Europe
- Asia-Pacific
- Rest of World
```

### Financial Performance Analysis

**[CHART 4: Gross Margin Evolution]**
折线图，并标注毛利率变化驱动，规模、定价、mix 等。

**[CHART 5: Operating Margin Progression]**
瀑布图展示从 gross margin 到 operating margin 的路径，或直接用折线图展示 EBITDA margin 趋势。

**[CHART 6: Free Cash Flow Generation]**
柱状 + 折线组合图，柱状表示 FCF，折线表示 FCF margin %。

**[CHART 7: Key Operating Metrics Dashboard]**
多面板图，展示 3-4 个关键指标：
- Customer count 或用户增长
- ARPU（Average Revenue Per User）或 ACV（Annual Contract Value）
- Customer cohort retention 或 net revenue retention
- LTV/CAC 或 magic number，或其他单位经济指标

### Forward Projections（3-5 年）

**Projected Financial Model**
```
                    2025E   2026E   2027E   2028E   2029E
Revenue ($M)        [X]     [X]     [X]     [X]     [X]
  Growth %          X%      X%      X%      X%      X%
Gross Profit ($M)   [X]     [X]     [X]     [X]     [X]
  Margin %          X%      X%      X%      X%      X%
EBITDA ($M)         [X]     [X]     [X]     [X]     [X]
  Margin %          X%      X%      X%      X%      X%
FCF ($M)            [X]     [X]     [X]     [X]     [X]
  FCF Margin %      X%      X%      X%      X%      X%
```

**Key Assumptions**
- 收入增长驱动与假设
- 利润率变化假设
- CapEx 占收入比例
- Working capital 假设

**Charts：**
- 展示收入驱动的 Revenue bridge
- 展示利润率改善路径的 Margin waterfall
- Free cash flow trajectory

### Fundraising & Valuation [针对私有公司]

**Fundraising History**
```
Round    Date      Amount    Valuation    Lead Investor(s)
Seed     [Date]    $XM       $XM          [Investor]
Series A [Date]    $XM       $XM          [Investor]
Series B [Date]    $XM       $XM          [Investor]
[etc.]
```

**Valuation Evolution Chart**
[展示估值随时间演进的可视化]

**Current Valuation Metrics**
- 最新估值：$XXbn
- 隐含估值倍数：XX.Xx
- 与上市可比公司的比较

---

## PAGES 26-31: INDUSTRY OVERVIEW

### Industry Definition & Market Size

**Industry Overview**
[2-3 段说明：
- 行业定义与边界
- 当前市场规模
- 历史增长率
- 关键趋势与驱动因素]

**Market Size Chart**
[展示市场规模从历史到预测增长的可视化]

### Competitive Landscape

**Competitive Positioning Matrix**
[2x2 图，展示公司与竞争对手在关键维度上的定位]

**Competitive Comparison Table**
```
Metric              [Company]  Comp A   Comp B   Comp C   Comp D
Revenue ($B)        [X]        [X]      [X]      [X]      [X]
Growth %            X%         X%       X%       X%       X%
Market Share        X%         X%       X%       X%       X%
Gross Margin        X%         X%       X%       X%       X%
Key Differentiator  [X]        [X]      [X]      [X]      [X]
```

**Competitive Analysis Narrative**
[2-3 段分析：
- 竞争优势与劣势
- 市场定位
- 份额增减
- 护城河]

### Total Addressable Market

**TAM Calculation**
```
Current TAM (2025):              $XXbn
Projected TAM (2030):            $XXbn
CAGR:                            XX%

Segmentation:
- [Segment A]:                   $XXbn
- [Segment B]:                   $XXbn
- [Segment C]:                   $XXbn
```

**TAM Growth Chart**
[按细分市场展示 TAM 扩张的可视化]

**Company's Market Opportunity**
```
Total TAM (2030):                $XXbn
Serviceable TAM:                 $XXbn
Company's Realistic Share:       XX%
Implied Revenue Potential:       $XXbn
```

### Industry Dynamics

**Porter's Five Forces Analysis**
- Threat of new entrants: [High/Medium/Low] - [Explanation]
- Bargaining power of suppliers: [High/Medium/Low] - [Explanation]
- Bargaining power of buyers: [High/Medium/Low] - [Explanation]
- Threat of substitutes: [High/Medium/Low] - [Explanation]
- Industry rivalry: [High/Medium/Low] - [Explanation]

**Key Industry Trends**
1. [Trend 1]: [Description and impact]
2. [Trend 2]: [Description and impact]
3. [Trend 3]: [Description and impact]

---

## PAGES 32-34: VALUATION ANALYSIS

### Valuation Methodology Summary

```
Valuation Method            Weight    Implied Value    Weighted Value
DCF Analysis                50%       $XX - $YY        $ZZ
Trading Comparables         30%       $XX - $YY        $ZZ
Precedent Transactions      20%       $XX - $YY        $ZZ
                           ────       ─────────────    ─────────
Weighted Average Price Target         $AA - $BB        $CC
```

### DCF Analysis

**Key Assumptions**
```
Revenue Growth (2025-2029):         XX% CAGR
Terminal Growth Rate:               X.X%
WACC:                               X.X%
Terminal Year EBITDA Margin:        XX%
```

**Figure X - DCF Sensitivity Analysis ($/share)**

关键格式：DCF sensitivity 必须以带颜色编码的 2-way heat map table 展示。

```
                        Terminal Growth Rate
WACC        2.0%      2.5%      3.0%      3.5%      4.0%
8.0%        $52       $55       $58       $62       $66
9.0%        $48       $51       $54       $57       $61
10.0%       $45       $47       $50       $53       $56
11.0%       $42       $44       $47       $49       $52
12.0%       $39       $41       $44       $46       $49

Color coding: Green (higher values) → Yellow (mid) → Red (lower values)
Source: [Firm Name] estimates.
```

**Scenario Analysis**
```
Scenario      Enterprise Value    Equity Value    Price/Share
Bear Case     $XXbn              $XXbn           $XX
Base Case     $XXbn              $XXbn           $XX
Bull Case     $XXbn              $XXbn           $XX
```

### Trading Comparables

**Figure X - Comparable Companies Analysis**

关键格式：comp 表必须包含双部分结构和 statistical summary。

**Part 1: Individual Company Data**
```
Company         Ticker   Market   EV/Rev   EV/Rev   EV/EBITDA  EV/EBITDA  Rev     EBITDA
                         Cap($B)  2024E    2025E    2024E      2025E      Growth  Margin
Peer A          PERA     XX.X     X.Xx     X.Xx     XX.X       XX.X       XX%     XX%
Peer B          PERB     XX.X     X.Xx     X.Xx     XX.X       XX.X       XX%     XX%
Peer C          PERC     XX.X     X.Xx     X.Xx     XX.X       XX.X       XX%     XX%
Peer D          PERD     XX.X     X.Xx     X.Xx     XX.X       XX.X       XX%     XX%
[Company]       COMP     XX.X     X.Xx     X.Xx     XX.X       XX.X       XX%     XX%
```

**Part 2: Statistical Summary**
```
Max                      XX.X     X.Xx     X.Xx     XX.X       XX.X       XX%     XX%
75th Percentile          XX.X     X.Xx     X.Xx     XX.X       XX.X       XX%     XX%
Median                   XX.X     X.Xx     X.Xx     XX.X       XX.X       XX%     XX%
25th Percentile          XX.X     X.Xx     X.Xx     XX.X       XX.X       XX%     XX%
Min                      XX.X     X.Xx     X.Xx     XX.X       XX.X       XX%     XX%

Source: FactSet, company filings, [Firm Name] estimates.
```

**Implied Valuation**
[说明将 peer multiples 应用于公司指标的计算过程]

### Precedent Transactions [如适用]

**Figure X - Precedent Transaction Analysis**
```
Date        Target       Acquirer      Deal      EV/Rev   EV/EBITDA  Premium
                                      Value($B)
[MM/YYYY]   [Company A]  [Buyer A]    X.X       X.Xx     XX.X       XX%
[MM/YYYY]   [Company B]  [Buyer B]    X.X       X.Xx     XX.X       XX%
[MM/YYYY]   [Company C]  [Buyer C]    X.X       X.Xx     XX.X       XX%
────────────────────────────────────────────────────────────────────
Median                                          X.Xx     XX.X       XX%

Source: Capital IQ, company filings, [Firm Name] estimates.
```

**Control Premium Analysis**
[讨论该行业中的典型溢价水平]

### Valuation Summary

**Figure X - Valuation Football Field**

关键格式：football field 必须是水平条形图，展示全部估值方法。

```
Valuation Method                Low End ────── Range ────── High End

DCF Analysis                    $42 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ $58

Trading Comps (NTM)             $45 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ $55

Precedent Trans.                $48 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ $60
                                                      ↑
                                            Current Price: $50
────────────────────────────────────────────────────────────────
Valuation Range:                $42                        $60

Color coding: Each method should have distinct color bar
Add vertical line showing current stock price
Source: [Firm Name] estimates.
```

**Price Target & Recommendation**
```
Current Price:              $XX.XX ([Date])
Price Target:               $YY.YY
Upside/Downside:            ZZ%

Recommendation:             BUY / HOLD / SELL
Time Horizon:               12 months

Catalysts:
• [Near-term catalyst with timeframe]
• [Medium-term catalyst with timeframe]
• [Long-term catalyst with timeframe]
```

---

## PAGES 35+: APPENDICES & DISCLOSURES

### Appendix A: Detailed Financial Model
[引用 Excel 模型]

### Appendix B: Management Bios
[如正文未放下，可加入更完整的简介]

### Appendix C: Product Detail
[如需要，可加入额外产品信息]

### Appendix D: Industry Data Sources
[列出行业分析所用来源]

### Required Disclosures
- Analyst certification
- Important disclosures
- Company-specific disclosures
- Legal entity disclosures
- Other regulatory disclosures

---

## 应包含的图形与图表

**目标：全篇穿插 20-30+ 张图表**

**核心原则**：图表应嵌入各个正文部分，而不是集中放在单独页面。除目录外，每页至少应有一张图或一张表。

### Page 1 - Executive Summary（3 张图）
1. Revenue/ARR growth trajectory，折线图，历史 + 预测
2. Key metrics dashboard，多面板图
3. Market positioning 或 margin progression

### Pages 3-5 - Investment Thesis & Risks（3 张图）
4. TAM growth and opportunity，stacked area chart
5. Competitive positioning matrix，2×2 气泡图
6. Margin expansion pathway，瀑布图或折线图

### Pages 6-17 - Company 101（6-8 张图）
7. Business model diagram，流程图
8. Company timeline，水平时间轴
9. Funding history，柱状图 + valuation 折线
10. Organization chart
11. Product portfolio matrix
12. Customer segmentation，饼图或 tree map
13. Geographic revenue breakdown
14. Customer cohort retention

### Pages 18-20 - Growth Outlook（4 张图）
15. Revenue bridge showing drivers，瀑布图
16. Market share evolution，折线图
17. Product roadmap，时间轴
18. Geographic expansion，带时间线的地图

### Pages 21-24 - Financials（7 张图）⭐ CRITICAL SECTION
19. Revenue growth trajectory，带注释折线图
20. **Revenue by product/segment**，stacked area ⭐ 必须有
21. **Revenue by geography**，stacked bar ⭐ 必须有
22. Gross margin evolution，折线图
23. Operating margin progression，瀑布图或折线图
24. Free cash flow trajectory，柱状 + 折线组合图
25. Key operating metrics dashboard，多面板图
26. Scenario comparison，分组柱状图：Bear/Base/Bull

### Pages 25-30 - Industry Overview（6 张图）
27. Market size evolution，带 CAGR 的面积图
28. Competitive landscape map，2×2
29. Market share 饼图
30. Market share evolution over time，折线图
31. TAM segmentation
32. Industry trend charts

### Pages 31-34 - Valuation（5 张图）
33. DCF sensitivity analysis，heat map
34. DCF waterfall，PV of cash flows → equity value
35. Trading comps scatter plot，growth vs. multiple
36. Peer valuation multiples，分组柱状图
37. Valuation football field，区间图
38. Price target scenarios，带上行 / 下行空间的柱状图

**图表风格指南：**
- **统一配色方案**，全篇使用 3-5 个品牌色
- **专业字体**，Arial、Calibri 或类似字体
- **所有图表都要有清晰标签和图例**
- **图表底部要有来源说明**
- **高信息密度**，高效利用图表空间
- **多样化图表类型**，增强视觉表现
- **添加注释**，突出关键洞察
- **嵌入正文**，不要让图表独立占页
- **适当在表格中使用 sparklines**

---

## 使用本模板的说明

1. **第 1 页最关键：** 第 1 页 executive summary 必须包含全部关键信息，fast facts、financial snapshot、3 张图、估值总结、投资论点和风险。这是最重要的一页。

2. **最大密度：** 专业股票研究报告的信息密度非常高。每页都应尽量塞满，文字、图表和表格要交错出现，目标是 60-80% 页面覆盖率，尽量减少留白。

3. **不要出现孤立页面：** 不要让章节标题单独占页，也不要让一张图 / 一张表独占一页。所有元素要组合在一起。例如，不要让 "Financial Snapshot" 单独出现在第 6 页，要把它与周边内容整合。

4. **20-30+ 张图表：** 全文加入大量图形，重点包括：
   - **Revenue by product/segment**（stacked area chart）
   - **Revenue by geography**（stacked bar chart）
   - **Financial performance trends**（多张图）
   - 图表要嵌入正文，而不是单独集中放置

5. **Use DOC Skill：** 本提纲应通过 DOC skill 转换成专业 Word 文档，包含正确格式、样式、页眉页脚和页码。

6. **Intersplice Content：** 正文段落之间要嵌入图表。每页应有 2-4 个不同元素，表格、图表、文本块。

7. **保持一致格式：** 标题、正文、表格和图表应使用一致的样式。先选定一个配色方案，并在全文坚持使用。

8. **References：** 为所有数据点添加引用和来源。

9. **Proofread：** 始终校对准确性，尤其是财务数据和计算。

10. **Executive Summary 最后写：** 虽然它出现在第 1 页，但应在完成全部分析后最后撰写。

11. **Balance：** 客观呈现积极面与负面因素。

12. **Specific > Generic：** 使用具体数据和案例，而不是泛泛而谈。
