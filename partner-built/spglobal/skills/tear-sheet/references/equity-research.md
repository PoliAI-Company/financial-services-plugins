# 股票研究 Tear Sheet

## 用途
面向买方或卖方分析师，对某项投资进行评估时使用的高密度快照。重点放在估值、前瞻预期、财务轨迹和分析师一致预期上。所有内容都应服务于支持或挑战一条投资逻辑。

**默认页数：** 1 页。股票研究 tearsheet 传统上就是单页，高密度本身就是目的。如果用户明确要求更大篇幅，可以扩展到 2 页。

## 查询计划

从这些查询开始。如果结果不完整，就拆分成更窄的后续查询。

**查询 1，公司画像与市场数据：**
"[Company] company overview sector industry market capitalization enterprise value stock price 52-week high low shares outstanding beta"
→ Header、Business Description
→ **立即写入** `/tmp/tear-sheet/company-profile.txt`

**查询 2，历史财务：**
"[Company] annual income statement revenue gross profit EBITDA net income EPS free cash flow total debt cash and equivalents last 4 fiscal years"
→ Financial Summary，抓 4 年、展示 3 年，最早一年仅用于计算同比
→ **立即写入** 原始数值到 `/tmp/tear-sheet/financials.csv`

**查询 2b，分部数据，如有：**
"[Company] revenue by segment business unit last 2 fiscal years"
→ Revenue & Segment Breakdown，需要 2 年才能算同比。如果拿不到分部数据，就整节跳过，不要留空表。
→ **立即写入** `/tmp/tear-sheet/segments.csv`，如果无分部数据则跳过

**查询 3，估值与一致预期：**
"[Company] P/E EV/EBITDA EV/Revenue valuation multiples consensus revenue EPS estimates analyst recommendations price target"
→ Valuation Snapshot、Consensus Estimates
→ **立即写入** 倍数到 `/tmp/tear-sheet/valuation.csv`
→ **立即写入** 预期数据到 `/tmp/tear-sheet/consensus.csv`

**查询 4，财报电话会：**
"[Company] most recent earnings call key takeaways guidance"
→ Earnings Highlights
→ **立即写入** `/tmp/tear-sheet/earnings.txt`

**查询 5，股价表现：**
"[Company] stock price return 1 month 3 month 6 month 1 year YTD performance"
→ Stock Performance，不需要中间文件，数据直接进入文档

**查询 6，若用户提供了 comps：**
"[Comp company] market cap EV/Revenue EV/EBITDA revenue growth"，对每个 comp 重复
→ 为 Valuation Snapshot 提供 peer 背景
→ **立即写入** `/tmp/tear-sheet/peer-comps.csv`

## 章节

按优先级排序。如果必须压缩到 1 页，就从最下方开始裁剪。

### 1. 公司页眉
采用紧凑键值块，并按全局样式配置用双栏无边框表格呈现。

左栏：Ticker，exchange，sector / industry，HQ
右栏：Stock price、52-week range、market cap、EV、shares outstanding、beta

### 2. 业务描述
用 2 到 3 句紧凑文字。**要按分析师受众重写，不要直接粘贴 CIQ company summary。** CIQ 摘要只是输入，输出必须简洁、围绕投资逻辑。

对于覆盖广泛、大家都认识的大公司，可以默认读者已了解基本业务。开头应先讲 *正在发生变化的部分*，比如战略转向、资产组合重塑、新增长引擎，而不是写成 Wikipedia 式概述。对知名公司来说，不要浪费一句去解释 “provides financial data to institutions”，而应写类似 “Reshaping its portfolio toward higher-margin data and analytics businesses...” 这种更贴近投资逻辑的表述。

对于不那么知名的公司，可以先用一句简要介绍其业务，再转向与投资逻辑有关的动态。

### 3. 估值快照
这是股票 tearsheet 的核心。

| Metric | Trailing | Forward (NTM) |
|---|---|---|
| P/E | | |
| EV/EBITDA | | |
| EV/Revenue | | |
| P/FCF | | |
| Dividend Yield | | |

**只要工具能返回，就必须展示 forward multiples。** 如果存在前瞻倍数，却只展示 trailing 倍数，就是明显缺项，因为分析师是按 forward earnings 来估值的。如果拿不到前瞻倍数，就只展示 trailing，并标注 “Fwd estimates N/A.”

如果用户提供了 comps，就为每个 comp 增加列，或者在 comps 达到 3 家以上时增加 “Peer Median” 列。如果用户没给，但工具返回了 peer 数据，也应展示 “Peer Median”。如果两者都没有，就只展示公司自身倍数。

### 4. 一致预期
展示市场，也就是 the Street，对公司的预期，这是这一类 tearsheet 的核心差异化之一。

**数据可得性说明：** 不同公司的一致预期覆盖深度差异很大。工具返回什么就展示什么，包括分析师数量、目标价、Buy/Hold/Sell 分布，但绝不要编造或估算任何一致预期。对于覆盖较薄的公司，这一节可能只包含收入和 EPS 预期，这依然有价值。

| Metric | FY[year] Est. | FY[year+1] Est. |
|---|---|---|
| Revenue | | |
| EPS (normalized) | | |
| EBITDA | | |

尽量使用 normalized 或 adjusted EPS。GAAP EPS 可能会被一次性项目扭曲，对前瞻判断价值更低。

主表下方，如果工具提供数据，应加入一个紧凑的一致预期区块：

| Analyst Consensus | |
|---|---|
| Mean Price Target | $XXX |
| # of Estimates | XX |
| Buy / Hold / Sell | XX / XX / XX |

如果拿不到目标价或评级分布，就直接省略这个区块，不要留空行。不要捏造这些数字。

如果完全没有一致预期数据，就整节跳过，并写 “Consensus estimates not available.” 不要估算。

### 5. 财务摘要，3 年
使用真实财政年度标签，做成一张高密度表。

| Metric ($M) | FY20XX | FY20XX | FY20XX |
|---|---|---|---|
| Revenue | | | |
| Revenue Growth % | | | |
| Gross Margin % | | | |
| EBITDA | | | |
| EBITDA Margin % | | | |
| Net Income | | | |
| EPS (Diluted) | | | |
| Free Cash Flow | | | |
| Net Debt | | | |

像增长率和利润率这样的衍生指标，应从原始数据计算，而不是单独再查。

**资本结构** 需要作为独立紧凑子表放在 Financial Summary 下方：
不要把这些行直接拼到 3 年财务摘要表里，否则前几年的空单元格会像缺失数据。应该用单独的 2 列子表，只展示最新财年。

| Metric | FY[latest] |
|---|---|
| Total Debt | $XXM |
| Cash & Equivalents | $XXM |
| Net Debt | $XXM |

这和 Corp Dev 及 IB/M&A tearsheet 中的资本结构格式一致。保持紧凑，不要在主表和子表之间额外留空。

### 6. 收入与分部拆解
如果工具提供了分部数据，就加入一张紧凑分部收入表。这对股票研究来说非常关键，因为分析师需要看到哪些业务线在驱动增长。

| Segment | Revenue ($M) | % of Total | YoY Growth |
|---|---|---|---|
| [Segment A] | | | |
| [Segment B] | | | |

对单页版本，要保持紧凑，只放表，不写定性段落。如果拿不到分部数据，就整节跳过，不要放空表或占位表。

### 7. 最近财报要点
需要写明季度和日期，比如 “Q3 FY2025 — October 2025”。用 3 到 4 个 bullet，且要带 **投资视角**，这个受众关注的是分部层面的细节，而不是抽象战略主题。

**如果管理层给出指引，第一条必须先写指引。** 用粗体前缀 `Guidance:`。这对分析师来说是最具操作性的前瞻信息，绝不能埋在后面。

**Beat/miss 背景，如数据允许：** 如果对该报告期能拿到一致预期，就应把 headline result 写成 beat 或 miss，比如 “Revenue of $X beat/missed consensus of $Y by Z%.” 如果拿不到对应期的一致预期，就只写绝对结果和增长率，不要臆造对比。

之后再写：
- 分部表现，哪些业务线加速或放缓
- 利润率轨迹，管理层对成本结构或盈利趋势的评论

应归因给管理层，比如 “Management highlighted...” 或 “CFO noted...”，而不是直接下判断。读起来应像 earnings recap，而不是新闻稿摘要。

### 8. 关键经营指标
如果有行业相关 KPI，就放 2 到 3 个，比如 subscriber count、same-store sales、NIM 等。如果没有行业专属指标，就用已经拿到的财务数据计算 ROE 和 ROIC。此节可选，空间紧张时优先删。

### 9. 股价表现，优先裁掉
列出各时间区间收益率。对这个受众来说分析价值相对较低，应当优先删掉。

| Period | Return |
|---|---|
| 1 Month | |
| 3 Month | |
| YTD | |
| 1 Year | |

## 格式说明
- **这是密度最高的一类 tearsheet。** 视觉上应明显比其他模板更紧。
- Financial Summary 表使用 8pt 文字，也就是 size 16，行高 240 DXA，是所有模板里最紧凑的。
- Valuation Snapshot 和 Consensus Estimates 使用 8.5pt，视觉中心要落在这里，因为分析师会先扫这两部分。
- 正文用 8.5pt，也就是 size 17，比全局默认的 9pt 更小。单页里每半个点都很重要。
- 章节间距尽量压缩。章节标题前 6pt，而不是全局 12pt，规则线后 2pt。
- 对任何显著拐点指标，比如增长转正、利润率扩张或压缩，可以加粗。
- 始终优先信息密度，而不是留白。
