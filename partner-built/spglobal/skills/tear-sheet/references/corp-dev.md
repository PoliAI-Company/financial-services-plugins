# Corporate Development Tear Sheet

## 用途
这是一份面向内部 Corp Dev 团队的标的评估画像，用于判断潜在收购对象。它不同于 IB / M&A 画像，后者更像为 pitch 讲述战略故事，而这里是一份强调战略匹配度的分析文档。重点在于目标公司的产品、客户、技术和运营与收购方之间是重叠、互补还是冲突。Corp Dev 受众已经了解自己公司，他们想知道的是，这个标的是否值得买，以及整合会是什么样。

**默认页数：** 1 到 2 页。Corp Dev 团队能接受更高密度的文档，如果内容扎实，第二页不会被视为问题。

## 查询计划

从这些查询开始。如果结果不完整，就拆开继续追问。

**查询 1，标的画像：**
"[Company] business description products services technology platform headquarters founded employees sector industry"
→ Header、Business & Product Overview
→ **立即写入** `/tmp/tear-sheet/company-profile.txt`

**查询 2，财务：**
"[Company] annual income statement revenue gross profit EBITDA operating income net income capex free cash flow R&D expense total debt cash and equivalents last 4 fiscal years"
→ Financial Summary，抓 4 年、展示 3 年，最早一年只用于同比计算。对 Corp Dev 来说，R&D 特别重要，因为它体现标的在 IP 上的投入
→ **立即写入** 原始数值到 `/tmp/tear-sheet/financials.csv`

**查询 3，分部与客户：**
"[Company] revenue by segment business unit last 2 fiscal years key customers end markets customer concentration"
→ Revenue Mix，需要 2 年才能算同比，Customer Analysis
→ **立即写入** 分部数据到 `/tmp/tear-sheet/segments.csv`，无数据则跳过

**查询 4，关系与竞争格局：**
"[Company] key customers suppliers partners competitors business relationships technology vendors"
→ Strategic Fit Analysis、Ecosystem Map
→ **立即写入** `/tmp/tear-sheet/relationships.txt`

**查询 5，估值与 peers：**
如果用户提供了具体 comps：
"[Comp company] enterprise value EV/Revenue EV/EBITDA revenue growth EBITDA margin"
否则：
使用 competitors 工具找 3 到 5 家上市 peers，并拉取各自 EV/Revenue，NTM，EV/EBITDA，NTM，收入增速和 EBITDA 利润率。
另外查询："[Company] enterprise value market capitalization valuation multiples"
→ Valuation Context
→ **立即写入** 公司倍数到 `/tmp/tear-sheet/valuation.csv`
→ **立即写入** peer 数据到 `/tmp/tear-sheet/peer-comps.csv`

**查询 6，所有权，如数据允许：**
"[Company] ownership structure investors institutional ownership insider ownership"
→ Ownership snapshot，不需要单独中间文件，可以并入 company-profile.txt

## 章节

按优先级排列。明确裁剪顺序见下方 “Page Budget & Cut Order”。

### 1. 公司页眉
和 IB / M&A 类似，但增加一行 “Strategic Relevance” 标语。

| Field | Notes |
|---|---|
| Company name | 大号粗体 |
| Ticker & Exchange | 上市公司显示，私有公司省略 |
| HQ Location | |
| Founded / Employees | |
| Enterprise Value | 上市公司写市值，私有公司写最近估值 |
| Ownership | Public / PE-backed / Founder-led / etc. |
| **Strategic Relevance** | 一句话说明为什么这个标的对收购方有吸引力，需基于数据综合 |

“Strategic Relevance” 是 Corp Dev 独有的一行。必须用中性分析视角写，而不是目标公司的市场宣传话术。要说明收购方 *能得到什么*，而不是目标公司 *是什么*。

### 2. 业务与产品概览
**不要直接粘贴 CIQ 公司摘要。** 应用 4 到 6 句话重写成一段，且强调产品和技术，因为这个受众关心的是收购，而不是投资：
- 核心产品和服务，以及它们解决什么问题
- 技术或平台架构的高层描述
- 关键差异化和竞争护城河
- 客户是谁，以及他们为什么购买
- 当前战略方向

要站在收购方视角来写。读者真正想问的是，我们现有的东西和它怎么拼在一起。

### 3. 收入结构与客户画像
分成两个子部分：

**a）分部收入，如有：**

| Segment | Revenue ($M) | % of Total | YoY Growth |
|---|---|---|---|

**b）客户分析：**
在分部表下方，或者在拿不到分部数据时替代表格，用一段定性文字覆盖以下内容：
- 客户集中度，前 5 大客户是否占收入 30% 以上，这对并购风险非常关键
- 客户类型，是 enterprise、SMB 还是 consumer
- 合同结构，是 subscription、transactional 还是 license，如能得知
- 地域结构

客户集中度是这里最重要的信号。如果工具返回了任何关于大客户或收入集中的信息，就要突出展示。如果数据稀疏，也要基于业务描述和关系信息写出能推断出的部分。控制在 2 到 3 句话。

### 4. 战略匹配分析
**这是 Corp Dev tearsheet 的招牌章节。** 必须出现，不能省略，也不要过度压缩。它使用 S&P Capital IQ 的 Business Relationships 数据，去映射重叠与互补关系。

分成三个桶。**每个桶都必须是 2 到 3 句分析性推理，而不是公司名称列表。** 只列名字没有意义，必须解释这种重叠或互补对收购意味着什么。

**Customer Overlap：** 目标公司的客户是否也会购买收购方产品，或者是否属于收购方所在行业。共享客户意味着更容易 cross-sell，但也可能带来渠道冲突。应点名这些共享关系，并解释其含义。

**Technology / Product Complement：** 目标公司是否填补了收购方产品组合中的空白。它们的技术栈长什么样。它们使用哪些技术供应商。如果它们已经在使用收购方技术，这就是强烈的整合信号。

**Competitive Displacement：** 目标公司本身是不是竞争对手，或者收购后是否等于把竞争对手从市场上移除。要写出关键竞争对手，并说明收购后竞争格局将如何变化。

这一节需要做真正的综合，把关系数据和业务概览连接起来。如果用户告诉你收购方是谁，就针对这个收购方定制。如果没有，也要保持泛化但仍然具备分析性。

**长度纪律：** 每个桶 2 到 3 句话是硬约束，不是建议。每个 bullet 应先给洞见，再用一个具体数据点支撑。实际输出很容易膨胀到 5 到 7 句，这是撑到第三页的主要原因。如果你写超过 3 句，多余内容应移到 Integration Considerations。

### 5. 财务摘要，3 年
和 IB / M&A 类似，但更强调 R&D 和资本效率。

| Metric ($M) | FY20XX | FY20XX | FY20XX |
|---|---|---|---|
| Revenue | | | |
| Revenue Growth % | | | |
| Gross Margin % | | | |
| EBITDA | | | |
| EBITDA Margin % | | | |
| R&D Expense | | | |
| R&D as % of Revenue | | | |
| Capex | | | |
| Free Cash Flow | | | |
| FCF Conversion (FCF/EBITDA) | | | |

R&D 强度反映价值更多来自 IP 还是服务。FCF 转化率反映整合复杂度，高 Capex 业务更难整合。如果 R&D 费用没有单独披露，应写 “Not separately disclosed”，而不是 “N/A”，因为这一点本身就很有信息量。

**资本结构**，作为财务摘要下方的紧凑子表：

| Metric | Value |
|---|---|
| Total Debt | $XXM |
| Cash & Equivalents | $XXM |
| Net Debt | $XXM |
| Net Debt / EBITDA | X.Xx |

需要再加一句收购视角解释，例如净债务和 EBITDA 杠杆对投资级收购方是否可控，以及在 LBO 情景下会如何放大杠杆。

### 6. 估值背景
**对上市公司来说，这一节是必需的。** Corp Dev 团队需要市场背景来框定潜在出价。如果工具返回了估值倍数，这一节就必须出现。不要因为页数问题删掉它，应先删 Ownership Snapshot。

这不是正式估值模型，Corp Dev 团队会自己做 DCF。这里提供的是市场背景。

**a）交易倍数，如上市：**

**Peer 背景不是可选项，而是必要项。** 如果用户给了 comps，就逐个成列展示。如果没有，就用 competitors 工具找 3 到 5 家上市 peers，并拉取它们的 EV/Revenue，NTM，EV/EBITDA，NTM，收入增速和 EBITDA 利润率。

| Metric | [Company] | [Peer 1] | [Peer 2] | [Peer 3] | Peer Median |
|---|---|---|---|---|---|
| EV/Revenue (NTM) | | | | | |
| EV/EBITDA (NTM) | | | | | |
| Revenue Growth % | | | | | |
| EBITDA Margin % | | | | | |

孤立地展示公司倍数对 Corp Dev 来说没有意义，他们需要相对 peer set 的位置，才能判断标的是便宜还是昂贵。

如果工具拿不到 peer 倍数，就展示公司自身倍数，并在表下列出所选 peers 名称供参考。

**b）先例交易，如数据允许：**
如果并购工具返回了目标同行或同子行业的近期交易，应展示：

| Date | Target | Acquirer | EV ($M) | EV/Rev | EV/EBITDA |
|---|---|---|---|---|---|

并写一句框定性说明，比如 “Recent transactions in [sub-sector] have valued targets at X–Yx revenue.”

如果工具拿不到先例交易数据，就写 “Precedent transaction data not available from data source”，不要默默省略，更不要编造倍数。

私有公司跳过 trading multiples，但如果有先例交易，仍然值得展示。

### 7. 所有权快照，如数据允许，若工具无结果则省略
如果工具返回了所有权数据，就加入一个紧凑区块，写 founder/family control 百分比、PE sponsor 细节和机构持股集中度。所有权结构会直接影响交易复杂度，也关系到整合考量。

**不要加入管理团队表。** S&P Global 工具不会返回高管数据，见 Data Integrity Rule 10。用训练数据补管理层一定会过时。

### 8. 整合考量
**必须出现，不要裁掉。** 这是 Corp Dev tearsheet 的分析性收束部分。基于上文所有内容综合成 3 到 4 个有实质内容的 bullet：
- **Key risks：** 客户集中、关键人物依赖、技术债信号
- **Integration complexity：** 地域分布，多国更难，员工数量、产品数量
- **Synergy signals：** 共享客户、互补产品、重叠技术供应商
- **Open questions：** Corp Dev 团队在出价前还需要尽调什么，且必须是具体、可执行的尽调事项，而不是泛泛战略问题

要明确标注这部分是分析观察，而不是数据源中的既成事实。

## 页数预算与裁剪顺序

**目标：2 页。** Corp Dev 画像可以充分用满两页，但除非用户明确要求更长格式，否则不能溢出到第三页。如果超过 2 页，按以下顺序裁剪，每一项都先完整裁掉再动下一项：

1. Ownership Snapshot，整节省略
2. Revenue Mix 下的 Customer Analysis prose，压缩到最多 2 句
3. Valuation Context 的解释性段落，保留 peer comp 表，删掉表下方解读
4. Precedent Transactions，保留 “not available” 说明，如空间极其紧张再删
5. Capital Structure 的解释句，保留表，删掉表下文字
6. Strategic Fit Analysis，把每个 bullet 压缩到最多 2 到 3 句，但不能删掉整节

永远不要裁掉：Business & Product Overview、Financial Summary 核心表，以及 Integration Considerations。

## 格式说明
- **Strategic Fit Analysis 是页面焦点。** 应给予更明显的样式：
  - 提升到 9.5pt，也就是 size 19，比标准正文略大，让这一节看起来最重要。
  - 使用全局样式配置中的缩进块 bullet。
  - 不要使用左边框强调，docx-js 渲染不稳定。
- Financial Summary 应明显突出 R&D 和 FCF conversion。
- 对上市公司来说，带 peer comps 的 Valuation Context 是必需项，不要先于 Ownership Snapshot 删除。
- 对私有标的来说，画像会更依赖定性章节，比如 Business Overview、Strategic Fit 和 Relationships，这很正常，而且依然很有价值。
- 语气应分析性、评估性，而不是宣传性。这不是 pitch，而是 assessment。
- **两页纪律：** 在渲染前先估算页数。Strategic Fit 的 3 个长 bullet 加上 Integration Considerations 的 4 个 bullet，单独就可能占满一页。如果如此，应先压缩 Strategic Fit，而不是牺牲其他核心内容。
