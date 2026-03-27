# 投资银行 / 并购 Tear Sheet

## 用途
用于交易背景下的公司画像，可服务于潜在标的、收购方或 pitchbook 收录。重点关注战略定位、分部细节、业务关系和并购活动。估值以交易倍数为框架，而不是投资逻辑。

**默认页数：** 1 到 2 页。IB 公司画像经常会延伸到第二页，尤其是在分部数据和并购数据丰富时。

## 查询计划

先从这些查询开始。如果结果不完整，就拆分并继续追问。

**查询 1，画像与识别信息：**
"[Company] business description headquarters founded employees sector industry ownership structure major shareholders"
→ Header、Business Overview
→ **立即写入** `/tmp/tear-sheet/company-profile.txt`

**查询 2，分部与财务：**
"[Company] revenue by segment business unit last 2 fiscal years AND annual income statement revenue gross profit EBITDA operating income net income capex free cash flow total debt cash and equivalents last 4 fiscal years"
→ Segment Breakdown，需要 2 年数据来计算同比，Financial Summary，抓取 4 年、展示 3 年，最早一年只用于计算同比
→ **立即写入** 原始财务数据到 `/tmp/tear-sheet/financials.csv`
→ **立即写入** 分部数据到 `/tmp/tear-sheet/segments.csv`，如果没有分部数据则跳过

**查询 3，估值与可比公司：**
如果用户提供了具体可比公司，则对每家查询：
"[Comp company] enterprise value EV/Revenue EV/EBITDA revenue growth EBITDA margin"
否则：
使用 competitors 工具识别 3 到 5 家上市可比公司，再拉取各自的 EV/Revenue，NTM，EV/EBITDA，NTM，收入增速百分比和 EBITDA 利润率百分比。
另外查询："[Company] enterprise value market capitalization EV/Revenue EV/EBITDA valuation multiples"
→ Header，EV/market cap，Trading Comps
→ **立即写入** 公司倍数到 `/tmp/tear-sheet/valuation.csv`
→ **立即写入** 可比公司数据到 `/tmp/tear-sheet/peer-comps.csv`

**查询 4，并购活动：**
"[Company] acquisitions divestitures completed transactions last 5 years deal value"
→ 公司自身交易
→ **立即写入** `/tmp/tear-sheet/ma-activity.csv`

**查询 5，可比交易，如数据允许：**
使用查询 1 结果中的具体行业，比如 “cloud observability software M&A transactions”，而不是 “technology M&A”。如果用户指定了 comps，也可以尝试："[comp company] acquisition deal multiples."
→ Comparable Transactions
→ **追加写入** 可比交易到 `/tmp/tear-sheet/ma-activity.csv`，增加 `type=precedent` 用于区分公司自身交易

**查询 6，关系与所有权：**
"[Company] key customers suppliers partners business relationships institutional ownership insider ownership"
→ Business Relationships、Ownership，如数据允许
→ **立即写入** `/tmp/tear-sheet/relationships.txt`

## 章节

按优先级排列。明确的裁剪指导见下方 “Page Budget & Cut Order”。

### 1. 公司页眉
采用键值块，呈现和交易相关的标识信息。

| Field | Notes |
|---|---|
| Company name | 大号粗体 |
| Ticker & Exchange | 上市公司显示，私有公司省略 |
| HQ Location | City, State/Country |
| Founded | 年份 |
| Employees | 大致员工数 |
| Market Cap / Valuation | 上市公司写市值，私有公司写最近已知估值 |
| Enterprise Value | |
| Ownership | Public / PE-backed，写 sponsor 名称 / Family / Other |

对私有公司，要显著标注 “Private Company”，并省略 ticker 和 exchange。

### 2. 业务概览
**这是一段 pitchbook 风格文字，不是 CIQ 摘要。** 不要直接粘贴数据工具中的公司描述。请用 4 到 6 句话重写，采用 pitchbook 风格：
- 描述收入模式，比如 recurring 还是 transactional，subscription 还是 license
- 说明客户基础的规模，比如 “serves 80% of Fortune 500 banks”
- 明确竞争护城河，比如 “proprietary dataset of X” 或 “only provider with Y”
- 框定对买方或卖方真正重要的增长驱动

语气应当自信、具体。银行家读完这一段后，应能立刻理解公司的战略定位。

### 3. 收入与分部拆解
按业务单元或产品线拆分收入。

| Segment | Revenue ($M) | % of Total | YoY Growth |
|---|---|---|---|
| [Segment A] | | | |
| [Segment B] | | | |
| **Total** | | **100%** | |

**如果没有分部数据：** 用 2 到 3 句话定性描述收入结构，比如 “Revenue is primarily derived from subscription licenses (~70%) and professional services (~30%).” 空表会让文档看起来像坏掉了，定性描述仍然能传达有用信息。

### 4. 财务摘要，3 年加 LTM
使用真实财政年度作为列表头。**如果有 LTM 数据，就在最新财政年度右侧加一列 LTM。** 标注方式为 “LTM [quarter end date]”，例如 “LTM Q3 2025”。银行家做估值交叉验证时会依赖 LTM，仅看财年可能滞后 6 个月以上。

| Metric ($M) | FY20XX | FY20XX | FY20XX | LTM [date] |
|---|---|---|---|---|
| Revenue | | | | |
| Revenue Growth % | | | | |
| Gross Profit | | | | |
| Gross Margin % | | | | |
| EBITDA | | | | |
| EBITDA Margin % | | | | |
| Operating Income | | | | |
| Net Income | | | | |
| Capex | | | | |
| Free Cash Flow | | | | |
| FCF Margin % | | | | |

在并购语境中，利润率和 FCF 转化率与绝对规模同样重要，因为买方在评估效率和现金创造能力。

**资本结构**，作为财务摘要下方的紧凑子表：

| Metric | Value |
|---|---|
| Total Debt | $XXM |
| Cash & Equivalents | $XXM |
| Net Debt | $XXM |
| Net Debt / EBITDA | X.Xx |
| S&P Credit Rating | XX，如有 |

从已抓取的资产负债表数据中提取。这是银行家公司画像中的标准组成部分。总债务、杠杆率和信用评级可以让买方迅速理解融资结构。如果没有信用评级，就删掉那一行。

### 5. 交易可比
公司倍数 **和经营指标** 要一起展示，银行家不会只看倍数。

**只要工具能返回，就必须展示前瞻倍数。** 如果有 forward 数据，却只展示 trailing 倍数，就是明显缺项，因为银行家按 forward earnings 给交易定价。

**应有 peer 列。** 如果用户给了 comps，每家公司都要单独成列。如果没有，就用 competitors 工具找 3 到 5 家上市同行，并拉取它们的倍数和经营指标。如果只有公司自身倍数，没有 peer 背景，那么对任何投行业务场景来说都不完整。

| Metric | [Company] | [Comp 1] | [Comp 2] | [Comp 3] | Peer Median |
|---|---|---|---|---|---|
| EV/Revenue (NTM) | | | | | |
| EV/EBITDA (NTM) | | | | | |
| Revenue Growth % | | | | | |
| EBITDA Margin % | | | | | |

如果尝试 peer 查询之后仍然只能拿到公司自身倍数，就展示这些数据，并在表下列出所选 peer 名称。

私有公司跳过本节。

### 6. 并购活动
分为两部分。**本节应展示交易金额。** 银行家会注意到缺失。

**硬规则：** 如果并购工具返回了交易金额，就必须在输出中出现。绝不能把已知金额降级写成 “Undisclosed”。只有工具确实没有返回时，才能写 “Undisclosed”。

**a）公司自身交易：**

**表格必须有专门的 Deal Value 列。** 不要把金额混进 Notes 或 Rationale 列。银行家扫描时就是在找数字，独立列更有用。

| Date | Target / Divested | Deal Value ($M) | Type | Rationale |
|---|---|---|---|---|
| | | | Acquisition / Divestiture | |

如果没有：写 “No disclosed transactions in the last 5 years.”

**b）行业可比交易，如数据允许：**
使用前面识别出的具体行业，比如 “cloud infrastructure software M&A”，而不是 “technology M&A”。如果用户给了 comps，也要查这些具体公司的交易。

| Date | Target | Acquirer | EV ($M) | EV/Rev | EV/EBITDA |
|---|---|---|---|---|---|

如果工具拿不到，就写 “Comparable transaction data not available from data source.” 不要臆造先例交易倍数。

### 7. 关键业务关系
使用 S&P Capital IQ relationship data，按类型分组：

**Customers：** 前 3 到 5 个命名客户
**Suppliers：** 关键供应商和技术提供方
**Partners：** 战略联盟、分销和合资
**Competitors：** 关键竞争对手名称

每一项都应包含关系类型和括号中的描述，说明关系性质，比如 “AWS — cloud infrastructure (primary hosting provider)”。只有名字而没有上下文没有价值。这个部分要留出足够空间，因为战略价值很高，很多竞品 tearsheet 都没有这一块。

### 8. 所有权快照，如数据允许，若工具无结果则省略
如果工具返回机构持股、内部人持股比例或前十大股东，可加入紧凑区块：

Top institutional holders，如有，列出前 3 到 5 名及持股比例。
Insider ownership，写汇总比例。

对于 PE-backed 公司，要写 sponsor 名称、收购年份和持股比例。所有权结构会直接影响交易复杂度。一个高度分散持股的上市公司、一个创始人控制的公司以及一个 PE 支持公司，交易路径完全不同。

如果工具没有返回所有权数据，就整节省略，不要放占位符。

**不要加入管理团队表。** S&P Global 工具不会返回高管数据，见 Data Integrity Rule 10。用训练数据补管理层名字一定会过时。

## 页数预算与裁剪顺序

**目标：最多 2 页。** IB 画像可以充分用满两页，但不能溢出到第三页。如果内容超过 2 页，按以下顺序裁剪，而且每一项都要先完整裁掉，再动下一项：

1. Ownership Snapshot，整节省略
2. Comparable Sector Transactions，保留公司自身并购，删掉先例交易
3. Business Relationships，压缩为前 3 个竞争对手，加上 suppliers、partners、customers 各前 2 个，并把描述压成括号短语
4. Capital Structure，把 Net Debt/EBITDA 合并进 Financial Summary 作为单独一行
5. Trading Comparables，把 peer 数量降到 3 家

永远不要裁掉：Business Overview、Revenue & Segment Breakdown、Financial Summary 核心表，以及公司自身交易部分的 M&A Activity。

## 格式说明
- Business Overview 和 Segment Breakdown 要占最大视觉权重。
- **M&A Activity 是招牌章节：** M&A 表头要用 Accent 色，也就是 `#2E75B6` 填充，白色粗体文字。这是唯一一个表头颜色不同于标准 `#D6E4F0` 的表，应该让人一眼注意到。
- **Business Relationships 在空间允许时要保留呼吸感。** 每组关系之间留 6pt，完整保留每条描述。但如果要冲到第三页，就按上面的裁剪顺序压缩。这个部分价值高，但也最容易压缩。
- 对私有公司来说，页眉、业务概览、财务和关系是核心，其他章节可能相对稀疏。
- **两页纪律：** 渲染前要先心里估算页数。如果 Business Relationships 加上 M&A Activity 会超过整整一页，就应开始按裁剪顺序删减。
