---
name: initiating-coverage
description: 通过 5 任务工作流创建机构级股票研究首次覆盖报告。任务必须逐个执行，并验证前置条件——(1) 公司研究，(2) 财务建模，(3) 估值分析，(4) 图表生成，(5) 最终报告组装。每个任务都会产出指定交付物（markdown 文档、Excel 模型、图表或 DOCX 报告）。任务 3-5 依赖于前序任务。
---

# 首次覆盖

通过结构化的 5 任务工作流创建机构级股票研究首次覆盖报告。每个任务都必须单独执行，并在开始前验证输入。

## 概览

本技能用于生成首次覆盖综合报告，遵循机构研究标准（JPMorgan、Goldman Sachs、Morgan Stanley 风格）。任务逐个执行，每一步在继续前都要验证前置条件。

**默认字体**：除非用户另有指定，所有文档统一使用 Times New Roman。

---

## ⚠️ 关键规则：一次只做一个任务

**本技能仅支持单任务模式。**

### 如果用户请求完整流水线

当用户提出如下请求时：
- "Create a coverage initiation report for [Company]"
- "Write an initiation report for [Company]"
- "Do the entire equity research process for [Company]"
- "Complete all 5 tasks for [Company]"
- 任何暗示要运行多个任务或整个工作流的请求

**标准回复：**

1. **询问要执行哪个具体任务：**
   ```
   我可以帮你为 [Company] 制作一份股票研究首次覆盖报告。
   这个流程包含 5 个需要分别完成的独立任务：

   1. 公司研究 - 研究业务、管理层和行业
   2. 财务建模 - 建立预测模型
   3. 估值分析 - 完成 DCF 和可比公司分析
   4. 图表生成 - 创建 25-35 张图表
   5. 报告组装 - 汇编最终报告

   你想从哪个任务开始？
   ```

2. **当用户明确要求一次完成所有任务时：**
   ```
   我理解你希望一次完成完整的首次覆盖报告流程。
   目前，这个技能一次只支持执行一个任务，这样每个阶段都能做更好的质量控制和复核。

   我们正在完善更顺畅的端到端工作流，让这个过程进一步自动化；但目前仍需要把每个任务分开完成。

   你想先从任务 1（公司研究）开始吗？
   ```

3. **不要自动假设从哪个任务开始**，始终要求用户确认。

4. **不要自动串行执行多个任务**，完成一个任务、交付输出后，等待用户明确请求下一个任务。

### 任务执行规则

- ✅ 每次用户请求只执行**一个**任务
- ✅ 开始任务前始终验证前置条件
- ✅ 交付该任务输出并确认完成
- ✅ 等待用户明确请求下一个任务
- ❌ 不要自动串联多个任务
- ❌ 不要假设用户想继续下一个任务
- ❌ 在未验证所需输入存在之前，不要执行 Tasks 3-5

### ⚠️ 交付物政策：禁止走捷径

**只交付指定输出。不要额外创建文档。**

每个任务都定义了精确交付物。不要创建：
- ❌ "Completion summaries"
- ❌ "Executive summaries"
- ❌ "Quick reference guides"
- ❌ "Next steps documents"
- ❌ "Task completion reports"
- ❌ 任何其他看似“有帮助”但未明确要求的文档

**原因**：这些额外内容会浪费上下文，而且不符合专业工作流。

**应交付的内容**：
- ✅ Task 1：研究文档（.md）——**仅此一项**
- ✅ Task 2：财务模型（.xlsx）——**仅此一项**
- ✅ Task 3：估值分析（.md）+ 在 Task 2 文件中新增 Excel 标签页——**仅此这些**
- ✅ Task 4：图表压缩包（.zip）——**仅此一项**
- ✅ Task 5：最终报告（.docx）——**仅此一项**

**如果某交付物未列在上面，就不要创建。**

---

## 任务选择

选择要执行的任务：

| 任务 | 名称 | 前置条件 | 输出 |
|------|------|----------|------|
| **1** | 公司研究 | 公司名称 / ticker | 6-8K 字文档 |
| **2** | 财务建模 | 可访问 10-K 或财务数据 | Excel 模型（6 个标签页） |
| **3** | 估值分析 | 财务模型（Task 2） | 估值 + 目标价 |
| **4** | 图表生成 | Tasks 1、2、3 + 外部数据 | 25-35 张 PNG/JPG 图表 |
| **5** | 报告组装 | 所有前序任务（1-4） | 30-50 页 DOCX 报告 |

---

## 如何使用本 Skill

### 用户请求模式与响应

**模式 1：用户指定具体任务**
```
User: "Use initiating-coverage, Task 1 for Tesla"
Response: ✅ 立即执行 Task 1
```

**模式 2：用户说“initiation report”或“full pipeline”**
```
User: "Create a coverage initiation report for Tesla"
Response: ❌ 不要自动开始任何任务
         ✅ 询问从哪个任务开始（见上方模板）
```

**模式 3：用户想做“all tasks”或“entire workflow”**
```
User: "I want to complete all 5 tasks for Tesla"
Response: ❌ 不要串联执行任务
         ✅ 解释一次只支持一个任务（见上方模板）
         ✅ 问用户是否要从 Task 1 开始
```

### 正确使用示例

**执行单个任务：**
```
"Use initiating-coverage skill, Task 1 for Tesla"
"Do Task 2 of initiating-coverage for Tesla"
"Run Task 3 for Tesla using the initiating-coverage skill"
```

**完成完整报告（需要 5 次独立请求）：**
```
Request 1: "Do Task 1 for Tesla" → 完成 → 交付输出
Request 2: "Do Task 2 for Tesla" → 完成 → 交付输出
Request 3: "Do Task 3 for Tesla" → 完成 → 交付输出
Request 4: "Do Task 4 for Tesla" → 完成 → 交付输出
Request 5: "Do Task 5 for Tesla" → 完成 → 交付输出
```

### 任务执行顺序

要完成一份完整的 initiation report，必须按以下顺序，在独立用户请求中执行：

```
Request 1: Task 1 - Company Research（独立）
           ↓ [用户审阅输出并请求下一个任务]
Request 2: Task 2 - Financial Modeling（独立）
           ↓ [用户审阅输出并请求下一个任务]
Request 3: Task 3 - Valuation Analysis（依赖 Task 2 输出）
           ↓ [用户审阅输出并请求下一个任务]
Request 4: Task 4 - Chart Generation（依赖 Tasks 2 & 3 输出）
           ↓ [用户审阅输出并请求下一个任务]
Request 5: Task 5 - Report Assembly（依赖所有前序任务输出）
```

**说明**：Tasks 1 和 2 可以以任意顺序进行。Tasks 3-5 有严格依赖关系，继续前必须验证输入。

---

## Task 1: Company Research

**目的**：研究公司的业务、管理层、竞争地位、行业和风险。

**前置条件**：✅ 无（完全独立）
- 公司名称或 ticker symbol

**流程**：
1. 验证已提供公司名称 / ticker
2. 加载 references/task1-company-research.md 中的详细说明
3. 执行定性研究工作流
4. 交付研究文档

**输出**：公司研究文档（6,000-8,000 词）
- 公司概览与历史
- 管理层简介（300-400 词 × 3-4 位高管）
- 产品与服务分析
- 行业概览
- 竞争分析（5-10 个竞争对手）
- TAM 测算
- 风险评估（8-12 项风险）

**文件名**：`[Company]_Research_Document_[Date].md`

**⚠️ 只交付这一份文件。不要交付完成总结，不要额外生成文档。**

**⚠️ 不要走捷径：**
- ✅ 完整写出 6,000-8,000 词，不要摘要
- ✅ 对全部 3-4 位高管完成 300-400 词简介
- ✅ 对全部 5-10 个竞争对手做充分分析
- ✅ 覆盖 4 大类中的 8-12 项风险
- ❌ 不要为了省时间而缩写章节
- ❌ 不要跳过任何必需章节

**继续前验证**：本任务无额外要求。

---

## Task 2: Financial Modeling

**目的**：提取历史财务数据，并建立包含预测和情景的综合 Excel 财务模型。

**前置条件**：⚠️ 开始前验证
- **必需**：可访问公司的财务数据
  - 对上市公司：SEC EDGAR 上最新的 10-K
  - 对私有公司：财务报表或可获得的估算数据
  - 或者：用户已提供预先提取好的历史财务数据
- **可选**：Task 1 的公司研究，提供业务背景

**输入验证**：
```
BEFORE STARTING - Select approach:

Option A: Extract financials (most common)
- [ ] Have access to 10-K or financial statements?
- [ ] Ready to extract 3-5 years of data?

Option B: User provided pre-extracted financials
- [ ] Historical financials file received?
- [ ] Contains income statement, cash flow, balance sheet (3-5 years)?

可选：
- [ ] Company research (Task 1) complete for context?
```

**流程**：
1. 验证是否可获取财务数据
2. 加载 references/task2-financial-modeling.md 中的详细说明
3. **步骤 1**：如有需要，提取历史财务数据
4. **步骤 2+**：建立包含 6 个核心 tabs 的预测模型
5. 交付 Excel 模型

**输出**：Excel 财务模型（.xlsx）
- 6 个核心 tabs：
  1. **Revenue Model** - 按产品拆分（20-30 行）+ 按地区拆分（15-20 行）
  2. **Income Statement** - 完整 P&L，40-50 行项目，历史（3-5 年）+ 预测（5 年）
  3. **Cash Flow Statement** - 经营 / 投资 / 融资活动，历史 + 预测
  4. **Balance Sheet** - Assets / Liabilities / Equity，历史 + 预测
  5. **Scenarios** - Bull/Base/Bear 对比表
  6. **DCF Inputs** - 为 Task 3 估值准备输入

**文件名**：`[Company]_Financial_Model_[Date].xlsx`

**⚠️ 只交付这一份文件。不要交付完成总结，不要额外生成文档。**

**⚠️ 不要走捷径：**
- ✅ 如需提取财务数据，完整提取 3 张财务报表的所有项目（3-5 年）
- ✅ 完整建立 6 个预测 tabs，细节齐全
- ✅ 建立详细收入模型，含 20-30 行产品拆分和 15-20 行地区拆分
- ✅ 建立完整 income statement，40-50 行项目，不要缩写
- ✅ 包含完整 cash flow statement 和 balance sheet 的所有项目
- ✅ 完成全部三种情景，Bull/Base/Bear，且参数不同
- ❌ 不要创建简化版
- ❌ 不要跳过 6 个核心 tabs 中的任何一个
- ❌ 如需历史财务数据提取，不要省略

**继续到 Task 3 前的验证**：
- [ ] 历史财务数据已提取，或已提供
- [ ] Excel 文件已创建且可打开
- [ ] 模型包含全部 6 个核心 tabs
- [ ] 已纳入 3-5 年历史数据
- [ ] 已完成 5 年前瞻预测
- [ ] 已完成 Bull/Base/Bear 情景

---

## Task 3: Valuation Analysis

**目的**：使用 DCF、comps 和 precedent transactions 进行综合估值。

**前置条件**：⚠️ 开始前验证
- **必需**：Task 2 的财务模型
  - 预测 income statements
  - 预测 cash flows
  - Revenue 和 EBITDA forecasts
  - DCF inputs，unlevered FCF

**⚠️ 关键要求：在 Task 2 完成前，不得开始本任务**

本任务依赖 Task 2 的财务模型。没有模型就开始，会导致输出不完整。

**如果 TASK 2 尚未完成**：立即停止，并告知用户必须先完成 Task 2（Financial Modeling）。不要尝试继续，也不要做占位式估值。

**输入验证**：
```
BEFORE STARTING:
- [ ] Task 2 complete? (Financial model exists)
- [ ] Model file path/location known?
- [ ] Can access projected financials from model?

模型中必需内容：
- [ ] Projected FCF (5 years)
- [ ] Revenue projections
- [ ] EBITDA projections
- [ ] Terminal year metrics
```

**流程**：
1. 验证财务模型可访问
2. 加载 references/task3-valuation.md 中的详细说明
3. 执行估值工作流
4. 交付估值分析

**输出**：估值分析（4-6 页 + Excel 标签页）
- DCF analysis，含 sensitivity tables
- Comparable companies（5-10 家 peers，含 statistical summary）
- Precedent transactions，如适用
- Valuation football field
- **Price target**：$XX.XX
- **Recommendation**：BUY/HOLD/SELL
- **Upside**：XX%
- Key catalysts（3-5）

**文件**：
- `[Company]_Valuation_Analysis_[Date].md`（书面估值分析文档）
- 在 `[Company]_Financial_Model_[Date].xlsx`（Task 2 文件）中新增 Excel tabs
  - DCF tab，含 calculations
  - Sensitivity analysis tab
  - Comparable companies tab
  - Valuation summary tab

**⚠️ 仅交付：1 个 markdown 文件 + 向现有 Excel 中增加 4 个 tabs。不要交付完成总结，不要额外生成文档。**

**⚠️ 不要走捷径：**
- ✅ 完成完整 DCF 分析和 sensitivity matrix
- ✅ 完整分析全部 5-10 家 comparable companies
- ✅ comps 表中包含 statistical summary，max/75th/median/25th/min
- ✅ 创建完整 sensitivity analysis tab，含多个 WACC 与 terminal growth 情景
- ✅ 写满 4-6 页估值分析，不要缩写
- ✅ 基于具体方法研究并论证 price target
- ❌ 不要跳过 comparable company analysis
- ❌ 不要做没有 sensitivity 的简化 DCF

**继续到 Task 4 前的验证**：
- [ ] Price target 已确定
- [ ] 估值至少使用两种方法，最低要求 DCF + Comps
- [ ] DCF sensitivity table 已完成
- [ ] Comparable companies table 含 statistical summary

---

## Task 4: Chart Generation

**目的**：为报告生成 25-35 张专业财务图表。

**前置条件**：⚠️ 开始前验证
- **必需**：Task 1 的公司研究
  - 公司历史和里程碑，用于 timeline charts
  - 管理层和组织结构，用于 org charts
  - 产品组合，用于 product charts
  - 客户细分，用于 customer charts
  - 竞争格局，用于 competitive charts
  - TAM 分析，用于 market size charts
- **必需**：Task 2 的财务模型（已加上 Task 3 的估值 tabs）
  - 按产品 / 地区拆分收入数据，来自 Task 2 tabs
  - 利润率趋势，来自 Task 2 tabs
  - 情景对比数据，来自 Task 2 tabs
  - DCF sensitivity table，来自同一 Excel 中的 Task 3 tab
  - Comparable companies data，来自同一 Excel 中的 Task 3 tab
  - 估值区间，来自同一 Excel 中的 Task 3 tab
- **必需**：外部市场数据
  - 历史股价数据，Yahoo Finance、Bloomberg 等
  - 历史估值倍数，用于历史趋势图

**⚠️ CRITICAL: DO NOT START THIS TASK UNLESS TASKS 1, 2, AND 3 ARE COMPLETE**

本任务依赖前三个任务的输出。缺少任意一个都会导致图表不完整。

**IF ANY OF TASKS 1, 2, OR 3 ARE NOT COMPLETE**：立即停止，并告知用户需要先完成哪些任务。具体要求如下：
- Task 1：公司研究文档，用于 9 张图
- Task 2：包含全部 6 个 tabs 的财务模型，用于 8 张图
- Task 3：已加入模型中的 valuation tabs，用于 6 张图
- 外部数据访问，用于 2 张图

不要尝试创建占位图表，也不要因缺数据而跳过图表。

**输入验证**：
```
BEFORE STARTING:
- [ ] Task 1 complete? (Company research exists)
- [ ] Task 2 complete? (Financial model exists)
- [ ] Task 3 complete? (Valuation analysis exists)
- [ ] Can access external market data sources?

Task 1 必需内容：
- [ ] Company history and milestones (for charts 05, 06)
- [ ] Management team structure (for chart 07)
- [ ] Product portfolio details (for chart 08)
- [ ] Customer segmentation data (for chart 09)
- [ ] Competitive landscape analysis (for charts 16, 17, 18)
- [ ] TAM sizing and market data (for chart 15)

Task 2 必需内容：
- [ ] Revenue by product (historical + projected) - for chart 03 ⭐
- [ ] Revenue by geography (historical + projected) - for chart 04 ⭐
- [ ] Income statement with margins (for charts 02, 10, 11)
- [ ] Cash flow statement (for chart 12)
- [ ] Scenario comparison data (for chart 14)

Task 3 必需内容：
- [ ] DCF sensitivity matrix - for chart 28 ⭐
- [ ] DCF components (for chart 29)
- [ ] Comparable companies data (for charts 30, 31)
- [ ] Valuation ranges - for chart 32 ⭐

外部来源必需内容：
- [ ] Historical stock price data (for chart 01)
- [ ] Historical valuation multiples (for chart 34)
```

**流程**：
1. 验证模型与估值输出可访问
2. 加载 references/task4-chart-generation.md 中的详细说明
3. 执行图表生成工作流
4. 将全部图表打包为 zip 文件
5. 交付 zip 文件

**输出**：25-35 张专业图表文件（PNG/JPG，300 DPI），打包为 zip

**4 张必需图表**（必须存在）⭐：
- chart_03：Revenue by product（stacked area）
- chart_04：Revenue by geography（stacked bar）
- chart_28：DCF sensitivity（2-way heatmap）
- chart_32：Valuation football field（horizontal bars）

**25 张必需图表**（指定清单）：
- Investment Summary：chart_01
- Financial Performance：charts 02, 03⭐, 04⭐, 10, 11, 12, 14
- Company 101：charts 05, 06, 07, 08, 09, 15, 16
- Competitive/Market：charts 17, 18
- Scenario Analysis：chart 13
- Valuation：charts 28⭐, 29, 30, 31, 32⭐, 33, 34

**10 张可选图表**（使总数达到 26-35）：
- charts 19-27, 35，客户获取、单位经济模型、产品路线图等

**IMPORTANT**：Task 5 会嵌入创建出的**全部**图表（25-35 张），以达到视觉密度要求，每 200-300 词一张图。

**文件命名**：`chart_01_description.png`、`chart_02_description.png` 等

**交付物**：`[Company]_Charts_[Date].zip`，包含所有 25-35 个图表文件 + chart_index.txt

**⚠️ 只交付这一份 ZIP 文件。不要交付完成总结，不要单独输出图表清单，不要额外生成文档。**

**⚠️ 不要走捷径：**
- ✅ 至少创建全部 25 张 required charts
- ✅ 包含全部 4 张 mandatory charts
- ✅ 可选再加 1-10 张图，达到 26-35 张，提高视觉密度
- ✅ 生成 300 DPI 的专业级图表，而不是低清占位图
- ✅ 每张图都要独立、格式良好
- ✅ 将全部图表和 chart index 打包进 zip 文件
- ❌ 不要只做 10-15 张图，最低要求是 25
- ❌ 不要跳过 4 张 mandatory charts 中的任何一张
- ❌ 不要使用低质量 / 占位图片

**继续到 Task 5 前的验证**：
- [ ] 已创建至少 25 个图表文件
- [ ] 4 张 mandatory charts 全部存在
- [ ] 所有图表均可打开且显示正常
- [ ] 图表均保存为 300 DPI
- [ ] 已创建列出全部文件与类别的 chart index
- [ ] 所有图表均已打包入 zip 文件
- [ ] 文件命名符合规范：chart_##_description.png

---

## Task 5: Report Assembly

**目的**：撰写并组装最终的综合 DOCX 报告。

**前置条件**：⚠️ 开始前验证
- **必需**：Task 1 的公司研究
  - 全部 6-8K 字内容
  - 管理层简介
  - 竞争分析
  - 风险评估
- **必需**：Task 2 的财务模型
  - Excel 工作簿
  - 全部预测与情景
- **必需**：Task 3 的估值分析
  - 目标价和评级
  - DCF、comps、precedent transactions
  - 全部估值数据
- **必需**：Task 4 的图表文件
  - 含 25-35 张 PNG/JPG 图的 zip 文件
  - zip 中包含 chart index

**⚠️ CRITICAL: DO NOT START THIS TASK UNLESS ALL TASKS 1-4 ARE COMPLETE**

这是最终组装任务，没有前面所有成果就无法完成。

**IF ANY OF TASKS 1, 2, 3, OR 4 ARE NOT COMPLETE**：立即停止，并告知用户需先完成哪些任务。具体要求如下：
- Task 1：公司研究文档（6-8K 字）
- Task 2：含全部 6 个 tabs 的财务模型
- Task 3：含 price target 与 recommendation 的估值分析
- Task 4：包含 25-35 张图的图表 zip 文件

不要尝试用 placeholder content、替代缺失章节，或组装不完整的报告。报告必须使用全部输入，并达到可直接发布的标准。

**输入验证**：
```
BEFORE STARTING - ALL TASKS MUST BE COMPLETE:

Task 1 验证：
- [ ] Company research document exists? (6-8K words)
- [ ] Management bios complete? (300-400 words × 3-4 execs)
- [ ] Competitive analysis complete? (5-10 competitors)
- [ ] Risk assessment complete? (8-12 risks)

Task 2 验证：
- [ ] Financial model exists and can be opened?
- [ ] Model has projections (5 years)?
- [ ] Scenarios exist (Bull/Base/Bear)?

Task 3 验证：
- [ ] Valuation analysis complete?
- [ ] Price target determined?
- [ ] Recommendation set? (BUY/HOLD/SELL)
- [ ] DCF and comps complete?

Task 4 验证：
- [ ] Chart zip file exists?
- [ ] Can extract/access all 25-35 chart files from zip?
- [ ] All 4 mandatory charts present?
  - [ ] Revenue by product (stacked area)
  - [ ] Revenue by geography (stacked bar)
  - [ ] DCF sensitivity (heatmap)
  - [ ] Valuation football field
- [ ] Chart files accessible and can be opened?

IF ANY VERIFICATION FAILS: Stop and complete missing task first.
```

**流程**：
1. **CRITICAL**：开始前验证全部前置条件
2. 加载 references/task5-report-assembly.md 中的详细说明
3. 使用 Claude 内建 skills 执行报告组装：
   - **Use DOCX skill** 创建并操作 Word 文档
   - **Use XLSX skill** 读取 Task 2/3 的 Excel 数据
   - **Use Read tool** 读取 Task 1 和 Task 3 的 markdown 文件
   - 读取 Task 1 `.md` → 转换为 Word 格式 → 在正文中插入图表
   - 读取 Task 2 `.xlsx` → 抽取表格 → 撰写定量分析
   - 读取 Task 3 `.md` + Excel tabs → 复制 / 调整估值分析
   - 使用 DOCX skill 在全文中插入 Task 4 的 `.png` 图表文件
   - 创建高文字密度、每 200-300 词插入图表的报告
4. 保存并交付最终 DOCX 报告

**关键原则**：
- 使用 Claude 的 DOCX 与 XLSX skills，而不是 Python 库
- 使用真实文件操作，读 `.md` / `.xlsx` / `.png`，写 `.docx`
- 优秀的股票研究报告应是**高文字密度 + 丰富说明性图片**，页面覆盖率 60-80%，平均每页至少一张图

**🔥 CRITICAL：这个任务必须全力以赴**

**这是最终交付物。不要走捷径。**

- ✅ 使用完整 token 预算，这是前面所有工作的汇总
- ✅ 每个章节都完整写出，不要总结，不要缩写
- ✅ 满足全部最低标准，30+ 页、10,000+ 字、25+ 图、12+ 表
- ✅ Projection assumptions 要写透，2,000-3,000 词，按产品逐项展开
- ✅ Scenario analysis 要写透，1,500-2,000 词，明确 Bull/Base/Bear 参数
- ✅ 插入 Task 4 的全部图表，不只是挑几张，而是全部 25-35 张
- ✅ 建立 Task 2/3 中的全部表格，提取每张财务表，不要省略
- ✅ 直接使用 Task 1 内容，复制完整 Company 101 章节，6-8K 字
- ✅ 只接受专业级质量，必须与 JPMorgan / Goldman Sachs 研究难以区分

**NEVER：**
- ❌ "This section would include..." —— 直接写出完整章节
- ❌ "Charts would be inserted here..." —— 直接插入真实图表
- ❌ "See financial model for details..." —— 直接抽取并写出细节
- ❌ 因篇幅而跳过章节 —— 每个章节都必须完整
- ❌ 为节省 token 而缩写 —— 需要多少 token 就用多少

**这是一份可直接发布的机构级研究成果，不能省力、不能省 token、不能省细节。**

**输出**：Comprehensive Equity Research Report（.docx）

**规格要求**：
- **Length**：30-50 页，最低 30 页
- **Word count**：10,000-15,000，最低 10,000 词
- **Charts**：25-35 张嵌入图片
- **Tables**：12-20 张综合表格
- **Format**：专业 DOCX，带可点击超链接

**报告结构**：
- 第 1 页：Investment Summary，INITIATING COVERAGE 格式
- 第 2-5 页：Investment thesis & risks
- 第 6-17 页：Company 101
- 第 18-30 页：Financial analysis & projections
- 第 31-40 页：Valuation analysis
- 第 41-50 页：Appendices

**文件名**：`[Company]_Initiation_Report_[Date].docx`

**⚠️ 只交付这 1 个 DOCX 文件。不要额外生成 executive summaries、highlights 文档或其他文件。**

**最终验证**：
- [ ] 报告页数为 30-50 页
- [ ] 字数为 10,000-15,000
- [ ] 嵌入了 25-35 张图
- [ ] 包含 12-20 张表
- [ ] 所有引用都是可点击超链接
- [ ] 所有数字与财务模型完全一致

---

## 输入验证协议

### 为什么输入验证很重要

每个任务都有严格前置条件。缺失输入就直接运行会：
- 浪费时间，产出不完整
- 导致质量低下
- 带来返工

**开始任何任务前，始终先验证输入。**

### 按任务划分的验证清单

**Task 1**：✅ 无需验证（独立）

**Task 2**：检查是否可获取历史财务数据

**Task 3**：检查财务模型是否存在且可访问

**Task 4**：检查模型（Task 2）和估值（Task 3）是否都已存在

**Task 5**：检查所有前序任务是否已完成（1、2、3、4）

### 如果验证失败怎么办

```
IF prerequisites are missing:
1. Stop the current task
2. Identify which prerequisite task(s) need to be completed
3. Execute the missing task(s) first
4. Return to current task once prerequisites are met
```

### 输入验证示例对话

```
User: "Use initiating-coverage, Task 5 for Tesla"

Claude: "Starting Task 5: Report Assembly for Tesla

VERIFICATION - Checking prerequisites:
- Task 1 (Company research)... ❌ NOT FOUND
- Task 2 (Financial model)... ❌ NOT FOUND
- Task 3 (Valuation)... ❌ NOT FOUND
- Task 4 (Charts)... ❌ NOT FOUND

⚠️ VERIFICATION FAILED

Task 5 requires ALL previous tasks to be complete.

To proceed:
1. Complete Task 1: Company Research
2. Complete Task 2: Financial Modeling
3. Complete Task 3: Valuation Analysis
4. Complete Task 4: Chart Generation
5. Then return to Task 5

Would you like to start with Task 1 first?"
```

---

## 任务参考文件

每个任务的详细说明被拆分到独立参考文件中，以保持本 skill 精简：

- **references/task1-company-research.md** - 公司研究工作流
- **references/task2-financial-modeling.md** - 财务建模工作流
- **references/task3-valuation.md** - 估值方法
  - 另见：references/valuation-methodologies.md，获取 DCF / comps 深入说明
- **references/task4-chart-generation.md** - 图表生成工作流
- **references/task5-report-assembly.md** - 报告撰写工作流
  - 另见：assets/report-template.md，获取报告结构
  - 另见：assets/quality-checklist.md，获取质检清单

**何时加载参考文件**：只加载当前具体任务对应的参考文件。这些文件都很大，不要一次加载多个。在开始某个任务时，读取对应参考文件获取逐步说明。

---

## 质量标准

所有输出都要达到头部投行机构标准，参考 JPMorgan、Goldman Sachs、Morgan Stanley：

- **Comprehensive**：满足全部最低要求
- **Detailed**：给出具体数据和示例，而不是空泛表述
- **Quantified**：以数字和指标开头
- **Cited**：所有来源带可点击超链接
- **Professional**：采用机构级格式
- **Accurate**：所有数字已验证并交叉检查

---

## 重要说明

### 任务独立性

- **Task 1** 可随时运行，无依赖
- **Task 2** 可随时运行，只需历史财务数据
- **Tasks 1 & 2** 可以并行
- **Task 3** 依赖 Task 2
- **Task 4** 依赖 Tasks 2 & 3
- **Task 5** 依赖 Tasks 1、2、3、4

### 会话管理

**同一会话中**：输出会自动对后续任务可用

**不同会话中**：显式引用前序任务输出
```
"Use Task 3 with the model from yesterday at [path]"
"Use Task 5 with the research document at [path]"
```

### 文件组织

工作流期间建议的目录结构：
```
ProjectFolder/
├── Task1_Research/
│   └── [Company]_Research_Document.md
├── Task2_Model/
│   └── [Company]_Financial_Model.xlsx
├── Task3_Valuation/
│   └── [Company]_Valuation_Analysis.pdf
├── Task4_Charts/
│   ├── chart_01.png
│   └── ... (25-35 files)
└── Task5_Report/
    └── [Company]_Initiation_Report.docx
```

### 不支持端到端自动执行

本 skill **不支持**自动按顺序一次性跑完全部任务。每个任务都必须显式请求并验证。

**原因**：这样可以确保：
- 每一步都有质量控制
- 能在继续前审阅输出
- 能灵活暂停 / 继续工作流
- 能清晰验证前置条件

---

## Success Criteria

一个成功的 initiation report 工作流应当：
1. 按顺序完成全部 5 个任务
2. 通过所有输入验证
3. 满足全部质量标准
4. 产出所有必需交付物
5. 各交付物间数字交叉一致
6. 最终报告达到可直接发布标准

**输出质量**：机构级，JPMorgan / Goldman / Morgan Stanley 水准
**使用场景**：对某家公司进行首次综合覆盖
