---
name: earnings-preview-single
description: 生成一份简洁的 4 到 5 页单公司股票研究财报前瞻。它会分析最新财报电话会纪要、竞争格局、估值和近期新闻，输出专业 HTML 报告。
---

# 单公司财报前瞻

生成一份简洁、专业的单公司股票研究财报前瞻。输出是一个自包含的 HTML 文件，打印后目标为 4 到 5 页。报告应当数字密集、叙事紧凑、直切重点。

**数据来源，零例外：** 唯一允许的数据源是 **Kensho Grounding MCP**，也就是 `search`，以及 **S&P Global MCP**，也就是 `kfinance`。绝不允许使用其他工具、数据源或任何形式的网页访问。若 Kensho Grounding 没有结果，就重写查询或在报告中注明 “data not available”。**绝不能回退到 web search。** 报告中的每一条信息都必须能追溯到 `kfinance` MCP 函数调用或 Kensho `search` 调用之一。

**关键规则：** 在开始写报告任何内容之前，你必须先完成全部研究和数据收集，也就是 Phases 1 到 5。

**中间文件规则：** 所有来自 MCP 工具调用的原始数据，都必须在每次调用返回后 **立即** 写入 `/tmp/earnings-preview/` 下的文件，然后才能继续下一次调用。不要只保存在记忆里。在 Phase 1 开始时先运行 `mkdir -p /tmp/earnings-preview`。**在生成 HTML 报告前，也就是 Phase 7 前，你必须把所有中间文件重新读回上下文。文件，而不是你的记忆，才是每个数字、引文和来源 URL 的唯一事实来源。**

**财政季度规则：** 绝不能根据日历日期去猜财报季度。很多公司的财政年度并不等于自然年。季度和财政年度必须严格以 `get_next_earnings_from_identifiers` 或 `get_earnings_from_identifiers` 返回的 call name 为准。

**长度规则：** 报告必须简洁，目标 4 到 5 个打印页。不要写长篇段落。尽量用简洁 bullet。每句话都必须有价值。

**逐字引文规则：** 当你使用 `<blockquote>` 引用管理层讲话时，文本必须与原始 transcript **逐字一致**。绝不能转述、拼接或润色。如果找不到原句，就不能当作直接引语。

**计算完整性规则：** 对任何多步计算，都要显式写出每个步骤并验证中间结果。只要附录中的加总与组件不一致，整份报告就是错的。

**比率命名规则：** 所有估值比率必须明确标注为 **LTM** 或 **NTM**。不要用 trailing 或 forward。LTM 基于最近 4 个已报告季度之和，NTM 基于未来 4 个季度的一致预期 EPS 之和。

**超链接规则，严格执行：** 报告中的每一个事实，无论是数字还是定性表述，都必须被 `<a href="#ref-N" class="data-ref">` 包裹，并指向附录中的对应条目。**这不是可选项。**

---

## Phase 1，公司画像与初始化

1. 从 `$ARGUMENTS` 解析单个公司 ticker
2. 运行 `mkdir -p /tmp/earnings-preview`
3. 调用 `get_latest()` 建立当前报告期背景
4. 调用 `get_info_from_identifiers`，记录市值和行业
5. 调用 `get_company_summary_from_identifiers`，记录业务描述
6. 调用 `get_next_earnings_from_identifiers`，记录下次财报日期和财政季度名称

并**立即写入** `/tmp/earnings-preview/company-info.txt`

---

## Phase 2，财报电话会分析，必须在写作前完成

1. 调用 `get_latest_earnings_from_identifiers` 获取最近完成的财报电话会 `key_dev_id`
2. 调用 `get_transcript_from_key_dev_id`
3. **立刻写入** `/tmp/earnings-preview/transcript-extracts.txt`，包括 transcript source、call date、fiscal quarter、verbatim quotes、guidance、key drivers、headwinds & risks、analyst Q&A themes 以及 next quarter themes

---

## Phase 3，竞争对手分析

1. 调用 `get_competitors_from_identifiers`，参数 `competitor_source="all"`
2. 选择 **最相关的 5 到 7 家上市竞争对手**
3. 对目标公司和所有竞争对手分别抓取：
   - `get_prices_from_identifiers`，最近 12 个月日频价格
   - `get_financial_line_item_from_identifiers`，提取 `diluted_eps`，季度、8 个周期
   - `get_capitalization_from_identifiers`，获取最新 market cap
   - `get_consensus_estimates_from_identifiers`，季度、前瞻 4 个周期，用于计算 NTM EPS

每次工具调用返回后，都要立刻把原始数据追加写入相应中间文件，比如 `prices.csv`、`peer-eps.csv`、`peer-market-caps.csv`、`consensus-eps.csv`。

**这个阶段不要计算 P/E 或收益率。** 先把原始数据落盘，计算在 Phase 6 完成。

同时应遵守日期一致性规则和 P/E 计算规则，尤其是 comparative stock returns 必须使用所有 ticker 共同重叠的起始日期，LTM P/E 也必须基于各公司各自最近 4 个已报告季度。

---

## Phase 4，新闻、预期与行业情报，使用 Kensho Grounding

必须对每个类别都运行 `search`，不能跳过：
- earnings estimates & analyst sentiment
- analyst ratings / price target / upgrades / downgrades
- risks / bear case
- recent news，最近 60 天重大新闻，**强制要求**
- sector outlook / trends

**关键点：** 必须记录 Kensho `search` 结果中的 **source URL**。每次 search 返回后，立刻把结果追加到 `/tmp/earnings-preview/kensho-findings.txt`。

---

## Phase 5，财务数据收集

抓取最近 8 个季度的财务数据，包括 revenue、gross_profit、operating_income、ebitda、net_income、diluted_eps，并在每次调用后立即写入 `/tmp/earnings-preview/financials.csv`。

分部数据通过 `get_segments_from_identifiers` 获取，写入 `segments.csv`。注意做同比时需要前一年同季度数据，如果没有，就必须写 “y/y not available”，不能估算。

历史财报日期通过 `get_earnings_from_identifiers` 获取，并写入 `earnings-dates.csv`。

---

## Phase 6，验证与计算，强制，不得跳过

在生成报告前，把所有中间文件读回，并基于干净数据执行计算。这个阶段的目标是确保所有数字来自文件，而不是来自对话记忆。

1. 读取所有中间文件
2. 计算衍生指标，比如 gross margin、operating margin、revenue y/y、EPS y/y、segment y/y、LTM P/E、NTM P/E、stock returns
3. 做交叉校验，确认同比、return 基准日期、LTM EPS 和 verbatim quotes 都正确
4. 将所有衍生结果写入 `/tmp/earnings-preview/calculations.csv`

这个文件会成为报告中所有数字的唯一事实来源。

---

## Phase 7，生成 HTML 报告

**停止。** 在写任何 HTML 之前，必须逐个把所有中间文件重新读入。不能合并成单次 bash 调用，也不能跳过任何一个文件。

读完后，必须向用户打印数据文件验证摘要，并明确说明所有中间文件已成功加载，接下来将使用这些文件作为唯一事实来源。

完整 HTML 模板、CSS 和 Chart.js 配置见 [report-template.md](report-template.md)。

**强制要求：图表必须使用模板中的 helper functions。** 不要手写自定义 inline Chart.js 代码。每张图都应放在自己的 `<script>` 标签内，并包裹在 try-catch 中，防止单图报错拖垮整页。

### 报告结构，目标 4 到 5 页

报告分为两半：
- **叙事部分**，第 1 到 2 页
- **图表部分**，第 3 到 5 页

### AI 免责声明，强制，必须出现 3 次

以下文本必须出现在报告中：

> **"Analysis is AI-generated — please confirm all outputs"**

它必须出现在：
1. Header banner 前的黄色横幅
2. Footer 中的黄色横幅
3. Appendix 开头的黄色横幅

### 页面说明

**PAGE 1：封面与投资逻辑**
- AI disclaimer banner
- Header，Company name、Ticker、Industry、Report date
- Title，带季度和主题副标题
- Executive thesis，最多 2 到 3 个短段加 bullet points
- 管理层关键引文应自然融入叙事中，不要单独设 “Key Management Quotes” 标题

**PAGE 2：预期、主题与新闻**
- Consensus Estimates Table，且 y/y 变化的颜色编码必须严格按正负号机械执行
- Key Metrics Beyond Headline EPS
- Themes to Watch
- Recent News & Developments

**PAGES 3 到 5：Figures**
- Figure 1 到 Figure 8，图表与表格按模板规定输出

**APPENDIX：数据来源与计算，强制，不可省略**
- 附录必须以 AI disclaimer banner 开头
- 每一个在正文中出现的事实，都必须在附录中有对应条目
- 附录表固定 4 列：Ref #、Fact、Value、Source & Derivation
- 原始 S&P 数据必须标明具体 MCP 函数调用
- 计算值必须展示完整公式，并让所有组件成为可点击链接
- Transcript claim 必须带 verbatim excerpt 和 transcript 元数据
- Kensho 结果必须带可点击 source URL 和 search query

---

## Phase 8，输出

1. 将完整 HTML 文件写到当前工作目录，命名为 `earnings-preview-[TICKER]-YYYY-MM-DD.html`
2. 使用 `open` 打开文件
3. 告诉用户文件已创建，并总结关键发现

---

## 写作指南

- **不要使用 emoji**
- **保持简洁**，目标 4 到 5 页
- **用具体数字表达**
- **必须表达明确观点**，这是财报前瞻，不是流水账
- **管理层引文要嵌入叙事，不要单独设标题**
- **语气要专业、分析性强、数据驱动**
- **图表必须基于真实 MCP 数据**
- **估值必须放在同业背景中解读**
- **每一个事实都必须超链接到附录**
