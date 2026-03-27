# 内容映射参考

本文件说明如何把源数据映射到 pitch deck 模板的不同区域。该流程与具体模板无关，这些原则适用于任何模板设计。

## 目录

- [模板分析流程](#模板分析流程)
- [内容映射工作流](#内容映射工作流)
- [常见 Slide 类型及数据要求](#常见-slide-类型及数据要求)
- [映射校验清单](#映射校验清单)
- [处理数据与模板不匹配](#处理数据与模板不匹配)
- [按模板做定制适配](#按模板做定制适配)

---

## 模板分析流程

在填充任何模板之前，先分析其结构：

### 第 1 步：识别所有内容区域

逐页检查并识别：
- **Title/header placeholders**，标题放置位置
- **Subtitle/definition areas**，副标题或定义区
- **Content boxes**，主要内容区域，可能带标签侧栏
- **Table placeholders**，专门留给表格的数据区
- **Chart/visual areas**，图表、示意图或图片区域
- **Metric callout boxes**，用于突出关键数字的框
- **Footnote/source bars**，页面底部的来源与说明区
- **Logo placeholder**，通常在右上角

### 第 2 步：记录模板惯例

每个模板都有自己的风格。重点观察：
- **Color scheme**，标题、背景、强调色分别用什么颜色
- **Font choices**，已有文字使用了什么字体和字号
- **Box styling**，内容框是否带侧栏、边框或底色
- **Bullet styles**，模板默认用什么 bullet 符号
- **Alignment patterns**，平行区域如何对齐

### 第 3 步：区分指导区域与输出区域

模板中经常带有说明信息：
- **Instruction boxes**，彩色指导框，通常黄底白字
- **Placeholder text**，方括号中的提示文字
- **Example content**，用于展示预期格式的示例内容

**关键区别：** Instruction boxes 告诉你要做什么，最终输出中应被删除或重设格式。Output areas 才是你真正放内容的地方。

---

## 内容映射工作流

### 第 1 步：盘点源数据

列出所有可用数据：
- 市场规模数字及区间
- 增长率，CAGR、YoY
- 公司名称及描述
- 分部定义
- 财务指标
- 来源引用及日期
- Footnote 内容

### 第 2 步：将数据匹配到模板区域

对每个模板区域，明确：

| 模板区域 | 必需数据 | 来源位置 |
|----------|----------|----------|
| [区域名称] | [所需数据] | [查找位置] |

### 第 3 步：识别缺口

映射完成后，记录：
- **Missing data**，模板需要但源数据没有
- **Extra data**，源数据有但模板没有位置容纳
- **Format mismatches**，数据存在，但格式不对

### 第 4 步：在填充前先解决缺口

- Missing data：标记给用户，或继续寻找额外来源
- Extra data：确认是否应排除，或模板是否需要调整
- Format mismatches：先把数据转成模板所需格式

---

## 常见 Slide 类型及数据要求

以下是常见 slide 类型的典型数据要求。实际模板可能不同，始终以模板真实结构为准。

### Market Definition Slides

**Typical content areas:**
- 纳入范围的 segments，附示例 / 关键玩家
- 排除范围的 segments，附示例
- 市场定义文字
- Scope rationale / justification

**Data mapping considerations:**
- 源数据应明确区分 included 与 excluded segments
- Key players 应被正确映射到各自 segment
- 定义文本应与源文件的方法口径一致

**Data typically needed:**
- 需要纳入的 market segments 列表，附 key player 示例
- 需要排除的 market segments 列表，附示例
- 市场定义文本
- Scope rationale 或 justification

**Formatting principle:** 平行区域，included vs. excluded，应采用匹配的格式。

**Verification questions:**
- 每个 segment 是否都用了正确符号，✓ 表示 included，× 表示 excluded？
- 关键玩家是否被放到了正确的 segment 中？
- 定义是否与源文件的方法论一致？

### Market Sizing / TAM Slides

**Typical content areas:**
- 当前市场规模，附年份
- 增长率，CAGR 与时间段
- 未来 projection，附目标年份
- 按来源拆分的数据表
- Consensus / summary figures
- Key takeaways 或 insight

**Data typically needed:**
- 基准年市场规模数字
- 增长率，含时间区间
- 目标年份 projection 数字
- 每个数据点的来源引用

**Example column headers:** `Source | [Base Year] Size | CAGR | [Target Year] Projection`

**Formatting principle:** 如果展示多个来源，应加入 consensus / summary 行。

**Data mapping considerations:**
- 不同来源可能给出不同估计值，每个来源应映射为表中一行
- Consensus figures 需要由各来源数据计算得出
- Projection 应能用 CAGR 公式手动验证

**Verification questions:**
- 所有来源数字是否都与原始文件一致？
- Consensus 是否正确计算，而不是直接复制单一来源？
- 所有 projection 年份是否一致？
- 手动校验时，CAGR projection 是否成立？

### Competitive Landscape Slides

**Typical content areas:**
- 以 competitor 为列的 comparison table
- Feature / capability 行
- 财务指标行，revenue、growth、market share
- 关键观察或 positioning notes

**Data typically needed:**
- 需要比较的 competitor 名单
- 每家的 feature 或 capability
- 财务指标，若可得
- 财务数据对应的时间区间

**Formatting principle:** Subject company 应被视觉上区分出来，例如粗体、不同底色、边框，或放在最右一列。

**Data mapping considerations:**
- 确保源数据中的所有 competitor 都被纳入
- Feature 比较必须使用一致标准
- 财务数据必须来自可比时间段

**Verification questions:**
- 源数据中的 competitor 是否都已出现？
- Subject company 是否有明显视觉区分？
- 财务数字是否来自同一时期？
- ✓ / × 的使用是否一致且准确？

### Financial Summary Slides

**Typical content areas:**
- 关键指标 callout
- 历史财务表，actuals
- 预测财务表，estimates
- 增长率与利润率
- 可选趋势图

**Data typically needed:**
- 最近几年的 historical financials，actuals
- 未来几年的 projected financials，estimates
- 核心指标，Revenue、Growth %、Margins、EBITDA

**Example column headers:** `Metric | FY[Year-2] | FY[Year-1] | FY[Year]A | FY[Year+1]E | FY[Year+2]E`

**Formatting principle:** 历史数据，A，与预测数据，E，必须清晰区分。

**Data mapping considerations:**
- 历史期和预测期必须区分清楚
- 指标定义要与来源一致，Revenue vs. Net Revenue，EBITDA vs. Adjusted EBITDA
- 增长率计算方法保持一致

**Verification questions:**
- 历史期与预测期是否明确标注？
- 计算出的增长率是否与来源一致，或与手工计算一致？
- 指标定义是否与源文件一致？

### Transaction Comparables Slides

**Typical content areas:**
- 交易表，Date、Target、Acquirer、Deal Value
- 估值 multiples，EV/Revenue、EV/EBITDA
- Summary statistics，mean、median、high、low
- 对 subject company 的 implied valuation

**Data typically needed:**
- 交易详情：Date、Target、Acquirer、Deal Value
- Valuation multiples：EV/Revenue、EV/EBITDA
- Subject company 的相关指标，用于 implied valuation

**Formatting principle:** 必须提供 multiple 的 summary statistics，Mean、Median、High、Low。

**Data mapping considerations:**
- Multiple 应由交易数据计算，而不只是照抄
- Summary statistics 需要对所有交易做统计
- Implied valuation 需要将 multiple 应用于 subject company 指标

**Verification questions:**
- 相关交易是否都已纳入？
- Multiple 是否按 `EV ÷ Metric` 正确计算？
- Summary statistics 是否覆盖表中所有交易？
- Implied valuation 是否明确标注为 illustrative？

---

## 映射校验清单

进入格式阶段前，请先验证映射完整性：

### Data Completeness
- [ ] 每个模板 placeholder 都已匹配到源数据
- [ ] 所有来源引用都已记录，供 footnotes 使用
- [ ] 没有方括号 placeholder 未被映射

### Data Accuracy
- [ ] 数字与原始来源逐项一致
- [ ] 年份与时间区间记录正确
- [ ] 公司名称拼写正确
- [ ] 计算值，consensus、projection、multiple，已验证

### Logical Consistency
- [ ] Included 与 excluded segments 逻辑一致
- [ ] 历史数据在时间上先于预测数据
- [ ] 对比数据来自一致时间区间
- [ ] 总计与小计计算正确

### Source Attribution
- [ ] 每个数据点都能追溯到来源
- [ ] 已记录来源名称与发布日期年份
- [ ] 特殊说明的 footnote 编号已分配

---

## 处理数据与模板不匹配

### 模板要求的数据多于现有数据

**Options:**
1. 明确标记缺口，交由用户审阅
2. 将该区域标记为 "Data not available"，并说明原因
3. 如适合，可继续寻找额外来源
4. 如果数据本身不存在，建议调整模板

**Do not:** 不要捏造数据，也不要做没有依据的估计。

### 源数据多于模板可容纳的内容

**Options:**
1. 选取最相关、最新的数据点
2. 在合适时进行汇总或聚合
3. 在脚注中补充说明还有更多可用数据
4. 如果这些数据非常关键，可建议扩展模板

### 数据格式与模板格式不匹配

**Common transformations:**
- 单一数字 → 区间，用来源中的 min-max
- 详细拆分 → 汇总类别
- 年度数字 → CAGR，用两端点计算
- 绝对值 → 百分比，计算占比
- 多个来源 → Consensus，应用既定方法

### 模板术语与源数据术语不同

**Resolution process:**
1. 识别模板用词与源数据用词
2. 确认两者指向同一概念
3. 输出中使用模板术语
4. 如有必要，通过脚注补充说明

---

## 按模板做定制适配

请记住，这份参考描述的是常见模式，不是硬性要求。始终遵循以下原则：

1. **Follow the template**，如果模板使用不同的 section 名称，就以模板为准
2. **Match template style**，使用模板的字体、颜色和 bullet 风格
3. **Preserve template structure**，除非确有必要，不要重排页面结构
4. **Respect template spacing**，内容必须装进指定区域，不能溢出

目标是按模板原本设计把内容填进去，而不是重新设计模板。
