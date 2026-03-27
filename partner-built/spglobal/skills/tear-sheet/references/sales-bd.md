# 销售 / 商务拓展 Tear Sheet

## 用途
这是一份为销售或 BD 团队准备客户会面的 briefing 文档。重点在于理解潜在客户的业务、管理层公开优先事项，以及找出能把你的产品或服务与其需求连接起来的切入点。财务部分被简化为规模和趋势层面。

这是最强调叙事感的一类 tearsheet，它更像 briefing memo，而不是数据表。

**默认页数：** 1 到 2 页。没有严格惯例，优先保证可读性，而不是一味压缩。

## 查询计划

从这些查询开始。如果结果不完整，再继续追问。

**查询 1，公司画像与财务：**
"[Company] business description overview products services headquarters employees sector industry revenue gross margin last 2 fiscal years"
→ Header、Company Overview、Financial Snapshot
→ **立即写入** `/tmp/tear-sheet/company-profile.txt`
→ **立即写入** 原始财务数据到 `/tmp/tear-sheet/financials.csv`

**查询 2，战略与财报电话会：**
"[Company] most recent earnings call strategic priorities CEO commentary guidance key initiatives"
→ Strategic Priorities
→ **立即写入** `/tmp/tear-sheet/earnings.txt`

**查询 3，关系与新闻：**
"[Company] key customers suppliers partners competitors business relationships recent acquisitions partnerships announcements"
→ Key Relationships、Recent News
→ **立即写入** `/tmp/tear-sheet/relationships.txt`

通常三次查询就足够。对知名公司来说，这些结果通常很丰富。对规模较小或私有公司来说，查询 2 和 3 可能比较 sparse，这没问题。定性部分仍然有价值，因为 Claude 会把拿到的信息综合成有用的 framing。

## 章节

按优先级排列。如果空间受限，就从底部开始裁剪。

### 1. 公司页眉
做得更精简，只保留识别信息，不放估值指标。

| Field | Notes |
|---|---|
| Company name | 大号粗体 |
| Ticker & Exchange | 上市公司显示，私有公司省略 |
| HQ | City, State/Country |
| Industry / Sector | |
| Employees | |
| Annual Revenue (latest) | 四舍五入到最近的 $B 或 $M |
| Market Cap | 上市公司展示，私有公司省略 |
| FY Revenue Guidance | 若财报数据有返回，例如 “6–8% organic growth” |
| FY EPS or EPS Guidance | 上市公司，从 `earnings.txt` 中提取 |
| Key Financial Metric | Adj. EPS、EBITDA margin 或类似指标，只保留一个 headline 数字 |

前瞻指引和 EPS 数据来自查询 2，也就是 earnings，要从 `earnings.txt` 中取，而不只是 `company-profile.txt`。

页眉是一条横向信息带，不需要 enterprise value，也不需要 beta，因为这个受众不关心这些。

### 2. 公司概览
这是最重要的部分。销售在会前读完这一节后，应当对潜在客户有扎实理解。

**不要直接粘贴 CIQ 公司摘要。** 它读起来像 SEC 文件，会让非金融受众失去兴趣。请用 3 到 5 句话的平实语言重写：
- 公司做什么，不用投资术语，比如说 “sells”，不要说 “monetizes”；说 “yearly revenue”，不要说 “top-line CAGR”
- 客户是谁
- 公司如何赚钱
- 主要在哪些地区运营
- 什么地方让它与众不同

要写成自然段。每句话都应让非金融背景的人也能读懂。

### 3. 战略重点与管理层评论
管理层现在最关注什么。如果你知道 CEO 在说什么，就更容易把你的 pitch 对准对方重点。

**这不是财报电话会摘要。** 不要直接复用 equity research tearsheet 里的 bullet。应提炼 3 到 5 个 *战略主题*，带主题标签和支撑数据：

- **AI/Data Monetization:** 管理层正积极投资 AI 能力，在 FY2024 向 R&D 投入 $X，并推出三个新的 AI 产品。
- **Margin Expansion:** CEO 提到运营效率是优先事项之一，目标是通过自动化实现 200bps 的营业利润率提升。
- **International Growth:** 正在 EMEA 开设新办公室；欧洲收入占比已从 18% 提升到 25%。

每个 bullet 都要回答一个问题：这家公司现在最关心什么，有什么证据支持。销售看到这些后，应当能立刻想到产品连接点。

如果没有财报电话会数据，这在私有公司中很常见，就改为 “Recent Developments”，使用工具返回的新闻或公告内容。

### 4. 财务快照
做简化处理。只保留一个紧凑表格，聚焦规模、方向和一个盈利信号。销售只需要知道三件事，这家公司多大、是否在增长、是否健康。

| Metric | FY[prior year] | FY[latest] | YoY Change |
|---|---|---|---|
| Revenue | | | +X% |
| Gross Margin % | | | +X.Xpp |
| Employees | | | |

最多三行。不要放 EBITDA、EV 倍数、资产负债表或净利润。对销售受众来说，Gross margin 是比 EBITDA 或净利润更合适的单一盈利指标，它更直观，也能体现业务健康度，而不要求读者具备金融专业背景。如果需要更深财务信息，可以另行请求 equity research 版本。

对私有公司来说，这张表可能只有收入和员工数两个点，这也足够体现规模和成长性。

### 5. 关键关系与生态
帮助销售理解潜在客户所处的世界，并找出切入角度。

用四组标签化列表呈现，每组 3 到 5 个名称，每项一行描述：

**Customers：** 他们卖给谁，帮助理解 go-to-market 和重叠目标客户。
示例：`JPMorgan Chase — customer (enterprise analytics platform deployment)`

**Vendors / Technology：** 他们买什么，用于识别替代或集成机会。
示例：`AWS — vendor (primary cloud infrastructure); Snowflake — vendor (data warehouse)`

**Partners：** 他们和谁合作，可用于寻找 co-sell 角度或共同关系。
示例：`Deloitte — partner (implementation for enterprise clients)`

**Competitors：** 他们和谁竞争，用于明确定位背景。
示例：`Bloomberg — competitor (financial data terminal)`

每一项都需要一个括号描述，告诉销售这段关系意味着什么，而不只是对方是谁。

如果没有关系数据，就写 “Relationship data not available”，然后继续。

### 6. 近期新闻与进展
写 3 到 5 个 bullet，每条一句话，最新的放前面。如有日期则加上。**第一条必须是最新财报。** 对销售会前准备来说，这通常是最重要的近期事件，也为后续所有信息定下背景。之后再放并购、产品发布、管理层变动和重大客户赢单。

**本节末尾应加入即将发生的催化剂，使用 “Coming Up:” 标签。** 例如即将发布财报、待完成剥离、产品发布、投资者日或监管节点。这些是销售外联最自然的切入窗口，也是最常见的触达理由。可从财报电话会评论和并购数据中提取，比如 pending transaction。

### 7. Conversation Starters，优先裁掉
基于以上数据综合出 2 到 3 条建议谈资。**每条 starter 都必须引用第三节中的具体战略重点。** 泛泛问题没有价值。请写成问题句。

**每条 starter 都要打上建议面向的 persona 标签**，例如 CTO、CFO、CDO、Head of Data、VP Engineering、Head of Procurement。与 CTO 的开场和与 CFO 的开场绝不会相同。如果用户已经说明要见谁，就只生成对应 persona 的 starter。

示例：
- *(CTO/CDO)* `You mentioned [specific AI initiative from Section 3] on your last earnings call — how is that impacting your [relevant need]?`
- *(CFO/COO)* `With your [margin expansion target from Section 3], are you evaluating tools that could accelerate that timeline?`
- *(VP Strategy/Corp Dev)* `I noticed [Company] recently acquired [target] — does that change your approach to [capability]?`

如果用户已经说明自己卖什么产品或服务，就把这些问题和该产品连接起来。如果没有，就保持和潜在客户战略主题相关，但不要硬绑定具体解决方案。

**校验测试：** 在最终确定每条 conversation starter 之前，确认其中至少包含一个来自 tearsheet 的具体数字、日期、产品名称或 initiative 名称。那种可以套用到任何同行公司的问题，不是好问题。比如 “How are you thinking about AI?” 太泛。像 “Your CEO mentioned $1B in AI investment since 2018 and 20% adoption of the iLEVEL auto-ingestion feature — how is that changing your analysts' workflows?” 这种才体现准备充分。

这部分是 Claude 的综合输出，而不是工具原始数据。要明确标注。

## 格式说明
- **这应该是最温和、最易读的一类 tearsheet。** 内容仍然严谨，但整体风格应更像 briefing memo，而不是数据终端。
- 正文使用完整 9pt，也就是 size 18，不要压缩。可读性优先于密度。
- 正文段落行距用 1.15x，比默认略松。这个模板里，留白是特性，不是浪费。
- Company Overview 和 Strategic Priorities 应占到页面约 40 到 50% 的空间。
- Financial Snapshot 视觉上要紧凑，重要性次于前两节，保持小巧干净。
- Key Relationships 可以考虑双栏布局，也就是左栏 Customers 加 Vendors，右栏 Partners 加 Competitors，以节省纵向空间，同时保留描述。
- Conversation Starters 使用缩进块样式 bullet。这是文档的最终价值点，视觉上应该突出。
