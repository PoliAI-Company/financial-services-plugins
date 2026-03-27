# 单位经济分析

description: 分析 PE 目标公司的单位经济，包括 ARR cohort、LTV/CAC、净留存、回本期、收入质量和利润率 waterfall。对软件 / SaaS、经常性收入和订阅业务尤其重要。适用于评估收入质量、构建 cohort 分析，或评估客户经济模型。触发词包括 "unit economics"、"cohort analysis"、"ARR analysis"、"LTV CAC"、"net retention"、"revenue quality" 或 "customer economics"。

## 工作流

### 第 1 步：识别业务模式

先判断收入模式，以便调整分析框架：
- **SaaS / Subscription**：ARR、净留存、cohort
- **Recurring services**：合同价值、续约率、upsell
- **Transaction / usage-based**：单笔交易收入、交易量趋势、take rate
- **Hybrid**：按收入来源拆分

### 第 2 步：核心指标

#### ARR / 收入质量
- **ARR bridge**：期初 ARR → New → Expansion → Contraction → Churn → 期末 ARR
- **ARR by cohort**：分 vintage 分析，每个年度 cohort 的留存和增长表现如何
- **Revenue concentration**：前 10 / 20 / 50 大客户占总收入百分比
- **Revenue by type**：经常性收入 vs. 非经常性收入 vs. 专业服务收入
- **Contract structure**：ACV 分布、多年期合同占比、自动续约占比

#### 客户经济
- **CAC (Customer Acquisition Cost)**：总 S&M 支出 / 新获客数量
- **LTV (Lifetime Value)**： (ARPU × Gross Margin) / Churn Rate
- **LTV:CAC ratio**：健康业务通常目标 >3x
- **CAC payback period**：回收获客成本所需月数
- **Blended vs. segmented**：按客户细分拆解，如 enterprise、SMB、mid-market

#### 留存与扩张
- **Gross retention**：期初 ARR 的留存比例，不含扩张
- **Net retention (NDR)**：含扩张后期初 ARR 的留存比例
- **Logo churn**：流失客户数占比
- **Dollar churn**：流失收入占比，通常与 logo churn 不同
- **Expansion rate**：upsell + cross-sell 占期初 ARR 百分比

#### Cohort Analysis
构建 cohort 矩阵，展示：

| Cohort | Year 0 | Year 1 | Year 2 | Year 3 | Year 4 |
|--------|--------|--------|--------|--------|--------|
| 2020 | $1.0M | $1.1M | $1.2M | $1.1M | |
| 2021 | $1.5M | $1.7M | $1.8M | | |
| 2022 | $2.0M | $2.3M | | | |
| 2023 | $3.0M | | | | |

同时展示绝对金额视图和索引视图，Year 0 = 100%。

#### Margin Waterfall
- Revenue → Gross Profit → Contribution Margin → EBITDA
- 全成本口径的单位经济，获取、服务和留住一个客户的成本分别是多少
- 分收入来源的毛利率，subscription、services、other

### 第 3 步：对标分析

将单位经济与相关 benchmark 比较：
- **SaaS Rule of 40**：增长率 + EBITDA margin > 40%
- **SaaS Magic Number**：Net new ARR / 上一期 S&M 支出 > 0.75x
- **NDR benchmarks**：最佳水平 >120%，良好 >110%，低于 100% 需警惕
- **LTV:CAC**：最佳水平 >5x，良好 >3x，低于 2x 需警惕
- **Gross retention**：最佳水平 >95%，良好 >90%，低于 85% 需警惕
- **CAC payback**：最佳水平 <12 个月，良好 <18 个月，高于 24 个月需警惕

### 第 4 步：收入质量评分

综合形成收入质量评估：

| 因素 | Score (1-5) | 备注 |
|--------|-------------|-------|
| Recurring % | | |
| Net retention | | |
| Customer concentration | | |
| Cohort stability | | |
| Growth durability | | |
| Margin profile | | |
| **Overall** | | |

### 第 5 步：输出

- Excel 工作簿，包含 ARR bridge、cohort matrix、单位经济仪表盘
- 汇总页，展示关键指标和 benchmark
- 红旗事项，以及需要进一步尽调的领域

## Important Notes

- 如有可能，始终争取获得客户级原始数据，汇总指标很容易掩盖问题
- NDR 高于 100% 可能掩盖高 gross churn，只要 expansion 足够强就会被覆盖，所以二者都要展示
- Cohort analysis 是衡量收入质量最关键的视角，应尽量推动获取这部分数据
- 区分 contracted ARR 和实际确认收入
- 对于 usage-based 模式，应关注消费趋势和扩张模式，而不是机械套用传统 ARR 指标
- Professional services 收入应单独评估，它不属于经常性收入，而且利润率通常更低
