---
name: datapack-builder
description: 从多种来源构建专业金融服务 data pack，包括 CIM、offering memorandum、SEC filings、web search 或 MCP server。提取、标准化并统一财务数据，输出适合投资委员会审阅的 Excel workbook，具备一致结构、规范格式和可追溯假设。适用于并购尽调、私募股权分析、投资委员会材料，以及在组合公司之间统一财务汇报。不适用于简单财务计算，或处理已经完成的数据包。
---

# Financial Data Pack Builder

为私募股权、投资银行和资产管理构建专业且标准化的 financial data pack。将来自 CIM、offering memorandum、SEC filings、web search 或 MCP server 的财务数据，整理成适合投资委员会审阅的 Excel workbook。

**Important:** 在整个流程中，所有 Excel 文件创建和操作都使用 xlsx skill。

## CRITICAL SUCCESS FACTORS

每个 data pack 都必须达到以下标准。任何一点失败，都会让交付物失去可用性。

### 1. 数据准确性，零容忍错误
- 每个数字都要追溯到源文件，并标注页码
- 所有计算都必须用公式，不允许硬编码
- 交叉检查小计与总计，确保内部一致
- 验证资产负债表恒等式，Assets = Liabilities + Equity
- 确认现金流表与资产负债表变动勾稽一致

### 2. ESSENTIAL RULES

**RULE 1: 财务数据，金额类，使用带 $ 的货币格式**
触发词：Revenue、Sales、Income、EBITDA、Profit、Loss、Cost、Expense、Cash、Debt、Assets、Liabilities、Equity、Capex
格式：百万单位用 `$#,##0.0`，千位单位用 `$#,##0`
负数：使用 `$(123.0)`，不要写 `-$123`

**RULE 2: 运营数据，计数量，使用数字格式，不要 $**
触发词：Units、Stores、Locations、Employees、Customers、Square Feet、Properties、Headcount
格式：`#,##0`
负数：使用 `(123)`，并与表内其他项目保持一致

**RULE 3: 百分比，费率和比率，使用百分比格式**
触发词：Margin、Growth、Rate、Percentage、Yield、Return、Utilization、Occupancy
格式：`0.0%`
展示：写 `15.0%`，不要写 `0.15`

**RULE 4: 年份，使用文本格式，避免自动插入逗号**
格式：Text 或自定义格式，防止出现 `2,024`
展示：`2020, 2021, 2022, 2023A, 2024E`

**RULE 5: 如果上下文混合，每个指标使用自己的正确格式**
示例：
```
Segment Analysis, 2022, 2023, 2024
Retail Revenue, $50.0, $55.0, $60.0
  Stores, 100, 110, 120
  Revenue per Store, $0.5, $0.5, $0.5
```
Revenue 和 per-store 指标使用 `$`，Store 数量使用纯数字格式。

**RULE 6: 所有计算都必须使用公式，绝不硬编码计算结果**
所有小计、总计、比率和衍生指标都必须由公式生成，这样才能确保准确并支持动态更新。

### 3. 专业呈现标准

**Formatting Standards:**

**Color Scheme - Two Layers:**

**Layer 1: Font Colors，xlsx skill 强制要求**
- **Blue text (RGB: 0,0,255)**：所有硬编码输入，历史数据、假设，不用于普通正文
- **Black text (RGB: 0,0,0)**：所有公式与计算结果
- **Green text (RGB: 0,128,0)**：跨工作表链接

**Layer 2: Fill Colors，可选，用于增强展示**
- 填充色是可选的，只在用户要求或确实有助于呈现时使用
- 如果用户要求颜色或专业格式，可使用以下标准：
  - **Section headers**：深蓝底，RGB: 68,114,196，白字
  - **Sub-headers/column headers**：浅蓝底，RGB: 217,225,242，黑字
  - **Input cells**：浅绿 / 米色底，RGB: 226,239,218，蓝字
  - **Calculated cells**：白底黑字
- 如果用户指定品牌色，则以用户要求为准

**如果使用填充色，两层逻辑如何协同：**
- 输入单元格：蓝字 + 浅绿底，表示用户输入数据
- 公式单元格：黑字 + 白底，表示计算结果
- 工作表链接：绿字 + 白底，表示来自其他标签页的引用

**字体颜色告诉你“它是什么”。填充色告诉你“它在哪里”，如果使用填充色的话。**

**IMPORTANT:** xlsx skill 要求的字体颜色是强制项。填充色是可选项，默认白底或不填充，除非用户明确要求增强格式或颜色。

**Always apply:**
- 标题加粗，左对齐
- 数字右对齐
- 子项目使用 2 空格缩进
- 小计上方单下划线
- 最终总计下方双下划线
- 冻结表头行 / 列
- 边框尽量少，只在结构需要时使用
- 统一字体，通常为 Calibri 或 Arial 11pt

**Never include:**
- 每个单元格四周都加边框
- 混用多种字体或字号
- 除非用户明确要求，否则不要加图表
- 不要过度装饰或过度格式化

## Structural Consistency
除非用户明确要求，否则采用标准 8 标签页结构：
1. Executive Summary
2. Historical Financials (Income Statement)
3. Balance Sheet
4. Cash Flow Statement
5. Operating Metrics
6. Property/Segment Performance，适用时
7. Market Analysis
8. Investment Highlights

### Tab 1: Executive Summary
用途：为时间有限的高管提供一页概览

内容：
- 公司概况，2 到 3 句描述商业模式
- 关键投资亮点，3 到 5 条 bullet
- 财务快照表，最近 3 年及预测期的 Revenue、EBITDA、Growth
- 如果适用，加入交易概览
- 突出展示核心指标

格式：简洁、标题加粗、少装饰，重点数字突出

### Tab 2: Historical Financials (Income Statement)
用途：完整展示损益历史

内容：
- 按分部 / 产品线拆分的收入
- 销售成本 / 收入成本
- 毛利与毛利率
- 详细运营费用，S&M、R&D、G&A
- EBITDA 与 Adjusted EBITDA
- 线下项目，D&A、利息、税项
- 净利润

格式：
- 年份作为列，文本格式，例如 2020、2021、2022
- 统一使用 `$ millions` 或 `$ thousands`，并在顶部明确单位
- 所有财务数据使用 accounting format
- 小计上方单下划线，净利润下方双下划线
- 所有数字右对齐

### Tab 3: Balance Sheet
用途：展示期末财务状况

内容：
- 流动资产，cash、AR、inventory、prepaid、other
- 长期资产，PP&E、intangibles、goodwill、other
- 流动负债，AP、accrued expenses、current portion of debt、other
- 长期负债，long-term debt、deferred taxes、other
- 股东权益，common stock、retained earnings、other

格式：
- 验证公式 `Assets = Liabilities + Equity`
- 日期标签保持一致
- 包含 working capital 计算
- 主要小计上方单下划线，最终总计使用双下划线

### Tab 4: Cash Flow Statement
用途：分析现金创造与使用

内容：
- Operating cash flow，优先间接法
- Investing cash flow，capex、acquisitions、asset sales
- Financing cash flow，debt issuance/repayment、equity、dividends
- 净现金变动
- 期初和期末现金余额

格式：
- 尽可能与利润表和资产负债表联动
- 展示从净利润到经营现金流的勾稽
- 清晰标识现金流出和现金来源

### Tab 5: Operating Metrics
用途：非财务 KPI 与运营数据

内容，取决于行业：
- 销量、客户数、网点数
- 生产率指标，人均收入、单店收入、单件收入
- 产能利用率
- 市占率
- 客户留存 / churn
- 行业特定 KPI

**CRITICAL FORMAT NOTE:**
运营指标不要加 `$`。这些是数量，不是金额。

格式：
- 明确单位，customers、employees、stores、square feet 等
- 整数加千分位，例如 `1,250`，不要写 `$1,250`
- 比率用百分比格式，例如 `95.0%`
- 数字右对齐

### Tab 6: Property/Segment Performance (if applicable)
用途：按业务单元、物业或分部提供细分表现

内容：
- 各分部收入和盈利能力
- 按地点 / 产品的关键指标
- 分部特定 KPI
- 对比表现分析

格式：Revenue/EBITDA 与财务标签页一致，运营指标用纯数字格式

### Tab 7: Market Analysis
用途：提供行业背景和竞争定位

内容：
- 市场规模与增长趋势
- 竞争格局概览
- 市占率分析
- 行业基准与同业比较
- 如相关，加入监管环境

格式：叙述文本与表格结合，市场数据需注明来源

### Tab 8: Investment Highlights
用途：以叙述形式总结核心投资逻辑

内容：
- 对竞争优势的详细说明
- 增长机会与战略举措
- 风险因素及应对措施
- 管理层评估与历史表现
- 投资逻辑总结

格式：标题清晰、bullet 明确、段落简洁

## STEP-BY-STEP WORKFLOW

### Phase 1: 文档处理与数据提取

**Step 1.1: 分析源数据**
- 获取源材料，上传文件、公开申报 web search，或 MCP server 数据
- 审阅数据结构并识别关键部分
- 定位财务报表，通常为 3 到 5 年历史数据
- 识别管理层预测，如果有
- 记录财政年度结算日期
- 立刻标出任何数据质量问题

**Step 1.2: 提取财务报表**
- 提取历史利润表数据
- 提取资产负债表快照，年末或季末
- 提取现金流量表
- 如果有管理层预测，也一并提取
- 为可追溯性记录所有页码引用

**Step 1.3: 提取运营指标**
- 识别行业相关的非财务 KPI
- 提取 unit economics
- 提取客户 / 网点 / 产能数据
- 记录增长指标与趋势

**Step 1.4: 提取市场与行业数据**
- 竞争定位信息
- 市场规模与增速
- 行业 benchmark 数据
- 同业比较信息

**Step 1.5: 记录关键背景**
- 交易结构与逻辑
- 管理团队背景
- 源材料中的投资亮点
- 风险因素与注意事项
- 数据缺口或不一致之处

### Phase 2: 数据标准化与统一

**Step 2.1: 统一会计呈现**
- 确保所有年份的 line item 名称一致
- 标准化收入确认口径
- 识别并记录一次性费用
- 如有需要，建立 "Adjusted EBITDA" 调节表
- 记录任何会计政策变化

**Step 2.2: 应用格式判定逻辑**
对每个数据点，根据完整上下文判断格式：
- 读取标签页名称、表格标题、列标题和行标题
- 应用上面的 essential rules
- 如果不确定，回看原始源文件
- 默认采用更简洁的格式，少即是多

**Step 2.3: 识别标准化调整**
常见调整包括：
- Restructuring charges，若确属一次性，可加回
- Stock-based compensation，可按行业惯例加回
- Acquisition-related costs，加回并注明金额
- Legal settlements 或 litigation costs，评估是否会重复发生
- Asset sales 或 impairments，从经营结果中剔除
- Related party adjustments，调整至市场化水平
注意：来源引用方式因数据来源而异，文档用页码，网页用 URL，MCP 数据用 server reference

**Step 2.4: 创建 adjustment schedule**
对每项标准化调整：
- 说明调整内容与原因
- 标明来源，文档页码、URL 或数据源引用
- 按年份量化金额影响
- 评估重复发生风险
- 展示从 reported figures 到 adjusted figures 的计算过程

**Step 2.5: 验证数据完整性**
- 用公式确认所有小计求和正确
- 验证资产负债表平衡
- 检查现金流是否与资产负债表变动勾稽
- 跨标签页对比数字一致性
- 对任何差异进行标记并进一步调查

### Phase 3: 构建 Excel Workbook

**CRITICAL: 所有 Excel 操作都必须使用 xlsx skill。开始前先阅读 xlsx skill 文档。**

**Step 3.1: 创建标准化标签页结构**
创建以下标签页：
- Executive Summary
- Historical Financials
- Balance Sheet
- Cash Flow
- Operating Metrics
- Property Performance，适用时
- Market Analysis
- Investment Highlights

**Step 3.2: 用正确格式构建每个标签页**
系统性应用格式规则：
- Headers：加粗、左对齐、11pt
- Financial data：百万单位使用 `$#,##0.0`
- Operational data：`#,##0`，不加 `$`
- Percentages：`0.0%`
- Years：文本格式，避免逗号
- Negatives：会计格式，使用括号
- Underlines：小计单下划线，总计双下划线

**Step 3.3: 用公式写入所有计算**
- 所有小计和总计必须是公式
- 资产负债表与利润表之间建立必要链接
- 现金流同时与利润表和资产负债表联动
- 建立跨标签页验证引用
- 不允许硬编码任何计算值

<correct_patterns>

### 行引用跟踪，直接复用这个模式

**写数据时先记录行号，再在公式中引用：**

```python
# ✅ CORRECT - Track row numbers as you write
revenue_row = row
write_data_row(ws, row, "Revenue", revenue_values)
row += 1

ebitda_row = row
write_data_row(ws, row, "EBITDA", ebitda_values)
row += 1

# Use stored row numbers in formulas
margin_row = row
for col in year_columns:
    cell = ws.cell(row=margin_row, column=col)
    cell.value = f"={get_column_letter(col)}{ebitda_row}/{get_column_letter(col)}{revenue_row}"
```

**复杂模型可以使用字典：**

```python
row_refs = {
    'revenue': 5,
    'cogs': 6,
    'gross_profit': 7,
    'ebitda': 12
}

# Later in formulas
margin_formula = f"=B{row_refs['ebitda']}/B{row_refs['revenue']}"
```

</correct_patterns>

<common_mistakes>

### WRONG: 硬编码行偏移

**不要使用相对偏移，这会在表结构变化时失效：**

```python
# ❌ WRONG - Fragile offset-based references
formula = f"=B{row-15}/B{row-19}"  # What is row-15? What is row-19?

# ❌ WRONG - Magic numbers
formula = f"=B{current_row-10}*C{current_row-20}"
```

**为什么这种方式会失败：**
- 增减行后会静默出错
- 读代码时几乎无法验证正确性
- 最终交付的 Excel 会变得很难排错

</common_mistakes>

**Step 3.4: 应用专业展示格式**
- 每个数据标签页冻结首行和首列
- 设置合适列宽，通常 12 到 15 个字符
- 所有数字右对齐
- 所有文本和标题左对齐
- 按会计标准加入单 / 双下划线
- 保持外观简洁、克制

### Phase 4: 场景构建，若包含预测

**Management Case:**
按源材料原样展示管理层预测：
- 提取所有管理层假设
- 记录增长率、利润率改善、资本需求
- 标出关键驱动与敏感项
- 对任何 "hockey stick" 型拐点保持怀疑并标记
- 明确标为 "Management Case"

**Base Case (Risk-Adjusted):**
基于公司特定风险，对管理层预测做保守调整：
- 结合执行风险和历史预测准确性，对收入增速打折
- 结合行业 benchmark 和经营杠杆，适度下调利润率扩张假设
- 若增长依赖 capex，则提高 capex 假设
- 若营运资本需求被低估，则进行补充
- 若适用，根据整合复杂度推迟协同效应兑现
- 记录全部调整、原因和支持分析

**Downside Case，LBO 分析中可选但推荐：**
基于行业周期性和公司脆弱点做压力测试：
- 模拟收入下滑，体现衰退风险或竞争压力
- 假设利润率承压，量减固定成本摊薄、价格压力
- 测试 covenant compliance 和 liquidity
- 评估 downside protection
- 记录正在测试的关键风险

**场景文档要求：**
建立 assumptions schedule，展示：
- 各场景关键假设，收入增速、利润率、capex 占比
- 每项调整的原因
- 关键变量的敏感性分析
- 若可得，历史预测准确性
- 与行业 benchmark 的对比

### Phase 5: 质量控制与验证

**Step 5.1: 数据准确性检查**
验证：
- 每个数字都能回溯到来源，抽样检查并标注 documents/URLs/servers
- 所有计算都是公式，不是硬编码
- 小计和总计计算正确
- 年份显示没有逗号，`2024` 而不是 `2,024`
- 没有公式错误，`#REF!`、`#VALUE!`、`#DIV/0!`、`#N/A`

**Step 5.2: 格式一致性检查**
确认：
- 财务数据带 `$`
- 运营数据不带 `$`
- 百分比以 `%` 展示，`15.0%` 而不是 `0.15`
- 财务负数使用括号
- 标题加粗并左对齐
- 数字右对齐
- 年份使用文本格式

**Step 5.3: 结构与完整性检查**
确认：
- 所有必需标签页都存在，顺序正确
- Executive summary 简洁，一页内可读完
- 所有关键指标都已充分覆盖
- 从摘要到细节的逻辑流动清晰
- 每个标签页的颗粒度合适
- 没有缺失数据或未完成部分

**Step 5.4: 专业呈现检查**
审阅：
- 边框最少，只用于结构
- 缩进一致，子项目 2 空格
- 会计下划线使用正确，单线与双线
- 整体外观简洁专业
- 列宽合适，不要过宽或过窄

**Step 5.5: 文档与假设检查**
确保：
- 所有标准化调整都已记录并说明原因
- 已包含来源引用，文档页码、URL 或数据源 reference
- 假设陈述清晰且合理
- Executive summary 准确、有力度
- 文件名包含公司名与日期

### Phase 6: 最终交付

**Step 6.1: 创建 executive summary**
写出简洁、有冲击力的摘要，包括：
- 公司概况，商业模式、产品 / 服务、地域，2 到 3 句
- 核心财务指标，Revenue、EBITDA、Growth rates，表格形式
- 投资亮点，3 到 5 条核心优势或机会
- 重要风险或注意事项，简要说明
- 如果适用，加入交易背景

**Step 6.2: 最终文件准备**
- 使用规范命名保存工作簿：`CompanyName_DataPack_YYYY-MM-DD.xlsx`

## NORMALIZATION PATTERNS

### Common Adjustments to EBITDA

**1. Restructuring charges**
- 只有确属一次性时才加回，facility closure、一次性裁员
- 如果公司年年重组，就不要加回
- 记录具体性质以及为何认为不会重复发生
- 例如：`2023 restructuring: $3.0M facility closure, documented in source materials, one-time event`

**2. Stock-based compensation**
- 私募股权分析中通常会加回
- 作为非现金经营费用处理
- 所有期间处理口径保持一致
- 如果异常偏高，或含一次性授予，需要特别说明

**3. Acquisition-related costs**
- 加回 transaction fees 与 integration costs
- 按类型记录具体金额
- 不要把持续性的 integration 投资也加回
- 每项调整都注明来源

**4. Legal settlements and litigation**
- 只有真正孤立事件才加回
- 评估重复发生风险，是一次性和解还是长期诉讼模式
- 记录和解事项性质
- 评估其是否属于正常经营的一部分

**5. Asset sales or impairments**
- 将资产出售损益从经营 EBITDA 中剔除
- 如果减值确属一次性，也可剔除
- 记录出售 / 减值的是哪些资产以及原因
- 如果这些资产曾贡献经营收入，也要同步调整收入口径

**6. Related party adjustments**
- 将高于市场水平的关联方费用，租金、管理费等，调整到市场水平
- 提供市场化依据
- 剔除通过公司报销的个人费用
- 记录市场水平对比逻辑

### Conservative vs Aggressive Normalization

**Management Case:**
- 包含管理层提出的全部调整
- 接受公司对 "non-recurring" 的定义
- EBITDA 调整更激进
- 用于理解管理层视角

**Base Case，Recommended for investment decisions:**
- 只纳入明确的一次性项目
- 对反复出现的 "one-time" 费用提高审查标准
- 排除缺乏支撑的推测性调整
- 更保守，也更容易向投资委员会解释

## INDUSTRY-SPECIFIC ADAPTATIONS

### Technology/SaaS
需要抓取的关键指标：
- ARR 与 MRR
- 分 cohort 客户数
- CAC 与 LTV
- Churn rate，gross 和 net
- Net revenue retention
- Rule of 40，Growth % + EBITDA Margin %
- Magic number，销售效率

格式说明：ARR 是货币，客户数是纯数字，比率使用 `%`

### Manufacturing/Industrial
需要抓取的关键指标：
- 产能与产能利用率
- 各产品线产量
- Inventory turns
- 各产品线毛利率
- Order backlog

格式说明：产量和产能是数字，利用率是 `%`，收入和成本是货币

### Real Estate/Hospitality
需要抓取的关键指标：
- 物业 / 房间 / 面积
- Occupancy rates
- ADR，使用货币格式
- RevPAR，使用货币格式
- NOI，使用货币格式
- Cap rates
- FF&E reserve

格式说明：房间数和面积是数字，occupancy 是 `%`，ADR/RevPAR 是货币

### Healthcare/Services
需要抓取的关键指标：
- Locations / facilities
- Providers / employees
- Patients / visits，量化指标
- Revenue per visit，货币格式
- Payor mix
- Same-store growth

格式说明：Locations 和 visits 是数字，revenue per visit 是货币，比率使用 `%`

## FINAL DELIVERY CHECKLIST

交付 data pack 之前，完成以下检查：

**Structure:**
- 所有必需标签页都存在，且顺序合理
- 每个标签页都有清晰标题
- Executive summary 简洁，一页内可读完

**Data Accuracy:**
- 所有数字都能追溯到来源，documents、URLs 或 data servers
- 关键数字已有来源引用，页码、URL 等
- 所有计算都用公式，没有硬编码计算值
- 小计和总计已验证
- 资产负债表平衡，Assets = Liabilities + Equity
- 没有 `#REF!`、`#VALUE!` 或 `#DIV/0!` 错误

**Formatting - Years and Numbers:**
- 年份显示正确：`2020, 2021, 2022`，不带逗号
- 财务数据带 `$`：`$50.0, $125.5`
- 运营指标不带 `$`：`100 stores, 250 employees`
- 百分比格式正确：`15.0%, 25.5%`
- 负数用括号：`$(15.0)`，不是 `-$15.0`

**Formatting - Professional Standards:**
- 标题加粗并左对齐
- 数字右对齐
- 缩进一致，子项目 2 空格
- 小计上方单下划线
- 最终总计下方双下划线
- 表头已冻结
- 全文件字体一致
- 边框尽量少，只用于结构
- 整体外观整洁专业

**Content Completeness:**
- 财务报表完整，IS、BS、CF
- 运营指标提取充分
- 标准化调整已记录
- 假设表述清晰
- Executive summary 清晰、简洁、有力度
- Investment highlights 有说服力
- Market analysis 提供了背景信息

**Documentation:**
- 所有标准化调整都有解释
- 每个数据单元格都带来源说明、注释和链接，文档页码、URL 或数据源引用
- 假设有依据说明
- 已记录数据限制
- 文件名符合命名规则：`CompanyName_DataPack_YYYY-MM-DD.xlsx`

**Final Output:**
- 文件已保存到 outputs，命名规范正确
- 所有质量检查都已通过
