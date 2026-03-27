# 首次覆盖报告质量控制清单

在交付首次覆盖报告之前，确认以下所有项目均已完成。

## 关键最低标准，报告必须满足

**如果出现以下任一情况，严禁交付：**
- ❌ DOCX 报告少于 30 页 → **INCOMPLETE**
- ❌ 嵌入图表少于 25 张 → **INCOMPLETE**
- ❌ 综合表格少于 12 张 → **INCOMPLETE**
- ❌ 字数少于 10,000 → **INCOMPLETE**
- ❌ 没有 XLS 财务模型 → **MISSING DELIVERABLE**
- ❌ 图表只是文字描述，而不是真实 PNG/JPG 文件 → **MAJOR FAILURE**

## 交付物清单

- [ ] 已创建 DOCX 报告文件
- [ ] 已创建 XLS 财务模型文件
- [ ] 两个文件均按规范命名：`[Company]_Initiation_Report_[Date].docx` 和 `[Company]_Financial_Model_[Date].xlsx`

## DOCX 报告，长度与内容

**长度验证：**
- [ ] 报告为 30-50 页，统计最终文档页数
- [ ] 字数为 10,000-15,000 词
- [ ] 若少于 30 页：停止，并补充内容

**视觉元素：**
- [ ] 已嵌入 25-35 张图表，统计数量：_____ 张
- [ ] 所有图表都是真实的 PNG/JPG 图片文件，而不是文字描述
- [ ] 已包含 12-20 张综合表格，统计数量：_____ 张
- [ ] 图表和表格贯穿全文，而不是集中堆在最后

**图表要求：**
- [ ] Revenue by product 图：Stacked Area 格式 ✓
- [ ] Revenue by geography 图：Stacked Bar 格式 ✓
- [ ] DCF sensitivity：双色维度 Heat Map，含颜色编码 ✓
- [ ] Valuation football field：水平条形图 ✓
- [ ] 其他所有图表都是真实图片文件 ✓

**表格要求：**
- [ ] 完整 Income Statement，40-50 行，含 5 年历史与 5 年预测
- [ ] 完整 Cash Flow Statement，30-40 行
- [ ] 完整 Balance Sheet，35-45 行
- [ ] Revenue by product 表，20-30 行
- [ ] Revenue by geography 表，15-20 行
- [ ] Revenue by channel 表，10-15 行
- [ ] Comparable companies 表，含 statistical summary，max/75th/median/25th/min
- [ ] DCF calculation 表，30-40 行
- [ ] WACC calculation 表，8-10 行
- [ ] 两张 sensitivity tables
- [ ] 2-3 张额外的财务 / 竞争表

## DOCX 报告，结构

**第 1 页要求：**
- [ ] 存在 "INITIATING COVERAGE" 标题，而不是 "Company Update"
- [ ] 标题聚焦投资论点，而不是事件驱动型标题，如 "Strong Q4 Results"
- [ ] 评级框包含 rating、price、target price、52-week range、market cap、EV
- [ ] 使用 ■ 字符与粗体标题，写出 3-4 条段落长度的 bullet
- [ ] 含 Financial & valuation metrics table，含 2-3 年历史和 2 年预测
- [ ] 表格使用 "A" 表示 actuals，"E" 表示 estimates
- [ ] 所有视觉元素都有 source lines

**内容章节：**
- [ ] Table of Contents，第 2 页
- [ ] Investment Thesis & Risks，3-5 页
- [ ] Company Overview，6-12 页，包含：
  - [ ] 公司描述
  - [ ] 历史与里程碑
  - [ ] 管理层简介，每位高管 300-400 词，共 3-4 位
  - [ ] 产品 / 服务细节
  - [ ] 竞争格局
- [ ] Financial Analysis & Projections，10-15 页
- [ ] Valuation Analysis，8-12 页
- [ ] Assumptions section，2,000-3,000 词，记录所有预测假设
- [ ] Scenario Analysis，1,500-2,000 词，包含 Bull/Base/Bear 参数
- [ ] Appendices，含 Data Sources & References 页面

## DOCX 报告，格式

**Figure 和 Table 格式：**
- [ ] 每个 figure 上方都有标题："Figure X - [Company] [Descriptive Title]"
- [ ] 每个 figure 下方都有来源行："Source: [Specific sources with dates]"
- [ ] Figure 编号连续，Figure 1、2、3... 中间无跳号
- [ ] 每个 table 都有带底纹的表头行
- [ ] 每个 table 底部都有来源行
- [ ] 所有年份都使用 "A" 表示 actual，"E" 表示 estimate

**专业格式：**
- [ ] 全文使用一致字体，Calibri、Arial 或类似字体
- [ ] 页眉页脚与页码完整
- [ ] 版面紧凑，60-80% 页面覆盖率，尽量减少留白
- [ ] 每一页都同时包含文字和视觉元素，图表或表格
- [ ] 使用专业商业报告模板

## 引用与来源 ⭐⭐⭐ CRITICAL

**来源标注：**
- [ ] 每个 figure 都有具体来源，含文档名称和日期
- [ ] 每个 table 都有具体来源，含文档引用
- [ ] 文中关键统计数据带脚注和来源
- [ ] 不是泛泛写 "Company data"，必须具体

**超链接：** ⭐⭐⭐ MANDATORY
- [ ] 所有 URL 都是可点击超链接，而不是纯文本
- [ ] SEC filings 超链接到 EDGAR viewer
- [ ] Earnings transcripts 超链接到来源页面，Seeking Alpha 或公司 IR
- [ ] Press releases 超链接到公司 IR 页面
- [ ] Presentations 超链接到 PDF URL
- [ ] Industry reports 若公开可获取，也带超链接
- [ ] 订阅数据，Bloomberg、FactSet，注明 "subscription required"
- [ ] 文中不显示原始 URL，只显示格式化超链接
- [ ] 抽测 3-5 个超链接，确保可正常打开，Ctrl+Click

**Reference Page：**
- [ ] 报告末尾有 "Data Sources & References" 页面
- [ ] 列出报告中使用的所有来源
- [ ] 来源按类别组织，SEC Filings、Earnings Transcripts 等
- [ ] 每个来源都注明日期
- [ ] 每个来源都带可点击超链接，如适用

## XLS 财务模型，结构

**文件结构：**
- [ ] Excel 工作簿含 15+ tabs
- [ ] Tabs 包括：Executive Summary、Assumptions、Historical Financials、Revenue Model、Operating Expenses、Income Statement、Balance Sheet、Cash Flow、Supporting Schedules、DCF Valuation、Comps Analysis、Precedent Transactions、Scenarios、Sensitivity Analysis、Charts

**格式：**
- [ ] 蓝色文字用于硬编码输入
- [ ] 黑色文字用于公式
- [ ] 绿色文字用于其他表链接
- [ ] 专业格式，带边框和底纹
- [ ] 清晰的区块标题和标签

**模型功能：**
- [ ] 数字可完整流转，修改假设后整个模型自动更新
- [ ] DCF 与假设和预测联动
- [ ] 无循环引用或错误
- [ ] 重要单元格 / 区域均已命名
- [ ] Sensitivity tables 可动态运作

## XLS 财务模型，内容

**预测：**
- [ ] 3-5 年历史数据
- [ ] 5 年前瞻预测，FY+1 到 FY+5
- [ ] Revenue 按产品、地区、渠道拆分
- [ ] 完整 P&L，40-50 行
- [ ] 完整 cash flow，30-40 行
- [ ] 完整 balance sheet，35-45 行

**估值：**
- [ ] 完整 DCF 模型，展示所有计算步骤
- [ ] WACC calculation，列出全部组成部分
- [ ] Terminal value calculation
- [ ] Comparable companies analysis，5-10 家公司
- [ ] Precedent transactions analysis，5-10 笔交易
- [ ] Scenario analysis，Bull/Base/Bear
- [ ] 两张 sensitivity tables

## 跨文件一致性

**CRITICAL**：DOCX 与 XLS 之间的数字必须**完全一致**。

- [ ] Revenue 数字在两个文件中一致
- [ ] EPS 数字在两个文件中一致
- [ ] Margin 百分比在两个文件中一致
- [ ] 估值数字在两个文件中一致
- [ ] Price target 在两个文件中一致
- [ ] 所有预测年份在两个文件中一致

**验证方法**：在 DOCX 报告与 XLS 模型之间抽查 10-15 个关键数字。

## 内容质量

**Investment Thesis：**
- [ ] 有 3-5 个清晰的 thesis pillars
- [ ] 每个 pillar 都有具体数据和量化支撑
- [ ] 每个 pillar 都量化了财务影响
- [ ] 明确列出催化剂及时间线

**分析深度：**
- [ ] 商业模式分析充分
- [ ] 竞争格局分析详尽
- [ ] 已分析 3-5 年财务趋势
- [ ] 已识别并量化 8-12 个风险
- [ ] 已分析管理团队，每位高管 300-400 词

**假设：**
- [ ] 有 2,000-3,000 词记录全部假设
- [ ] 收入增长假设按品类 / 地区拆解
- [ ] 利润率假设配套桥接分析说明驱动因素
- [ ] 营运资本假设完整
- [ ] CapEx 假设完整
- [ ] 每个假设都有具体量化

**情景：**
- [ ] 有 1,500-2,000 词的情景分析
- [ ] Bull case 含具体参数和催化剂
- [ ] Base case 含详细逻辑
- [ ] Bear case 含具体触发因素
- [ ] 为每个情景给出概率判断

## 写作质量

**风格：**
- [ ] 先给数字，例如 "Revenue grew 15% to $1.2B"，而不是 "Strong revenue"
- [ ] 使用 "vs." 而不是 "versus"
- [ ] 表达直接、简洁
- [ ] 全文维持机构级专业语气
- [ ] 无口语化表达

**准确性：**
- [ ] ticker symbol 无拼写错误
- [ ] company name 无拼写错误
- [ ] 所有日期准确
- [ ] 所有计算已核验
- [ ] 图表与文字描述一致
- [ ] 所有数字格式正确，$、% 和千分位逗号

## 交付前最终检查

快速完成这轮最终检查：

1. **交付物**：DOCX 和 XLS 文件都已创建 ✓
2. **长度**：DOCX 为 30-50 页 ✓
3. **图表**：已嵌入 25-35 张真实 PNG/JPG 文件 ✓
4. **表格**：已包含 12-20 张综合表格 ✓
5. **字数**：10,000-15,000 词 ✓
6. **超链接**：抽测 3-5 个超链接，全部可用 ✓
7. **交叉核对**：抽查 10 个数字，DOCX 与 XLS 一致 ✓
8. **Page 1**：存在 "INITIATING COVERAGE" 标题 ✓

如果任何一项失败，**不要交付**，先返回修正。

## 实际计数验证

**交付前填写实际数量：**

DOCX Report:
- Page count: _____ pages，必须为 30-50
- Chart count: _____ charts，必须为 25-35
- Table count: _____ tables，必须为 12-20
- Word count: _____ words，必须为 10,000-15,000

XLS Model:
- Tab count: _____ tabs，建议为 15+
- Model years: _____ historical + _____ projected

如果任何数量低于最低要求，停止交付，并在交付前补足内容。
