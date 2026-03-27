# 任务 2：财务建模 - 详细工作流

本文档提供执行 initiating-coverage skill 中 Task 2（Financial Modeling）的逐步说明。

## 任务概览

**Purpose**：提取历史财务数据，并建立包含预测和情景的综合 Excel 财务模型。

**Prerequisites**：⚠️ 开始前验证
- **Required**：可以访问公司财务数据
  - 对上市公司：从 SEC EDGAR 获取最新 10-K 和近期 10-Q
  - 对私有公司：来自可获取来源的财务报表或估算
  - 或：由用户提供预先提取好的历史财务数据
- **Optional**：Company research（Task 1），用于业务背景理解

**Output**：Excel Financial Model（.xlsx），包含 6 个核心 tabs：
1. Revenue Model
2. Income Statement
3. Cash Flow Statement
4. Balance Sheet
5. Scenarios
6. DCF Inputs

---

## 输入验证

**开始前检查：**

**Option A: 直接提取财务数据（最常见）**
- [ ] 是否可以访问 10-K filings（上市公司）？
- [ ] 或可以访问财务报表（私有公司）？
- [ ] 是否准备好创建 Excel 文件用于历史数据提取？

**Option B: 用户已提供预提取财务数据**
- [ ] 是否提供了历史财务数据文件？`.xlsx` 或其他格式
- [ ] 是否包含 3-5 年 income statement、cash flow、balance sheet？
- [ ] 数据是否干净且可直接使用？

**Optional Context：**
- [ ] 是否已完成 Task 1 的公司研究，用于业务理解？

**IF VERIFICATION FAILS**：停止，并先获取财务报表访问权限，10-K 或同等级资料。

---

## 模型结构与格式

### 颜色编码（行业标准）
- **Blue text**：硬编码输入，用户可修改
- **Black text**：公式与计算
- **Green text**：其他工作表链接
- **Red text**：错误或警示，应被消除

### 格式标准
- 专业边框与底纹
- 清晰的区块标题
- 支持折叠的 grouped rows
- 关键输入 / 输出使用 named ranges
- 公式中不要硬编码数字，除非是 12 个月这类常数
- 明确单位，$ thousands、$ millions 等

### 公式最佳实践
- 所有数字都应从假设出发流转
- 修改一个假设 → 整个模型联动更新
- 不要有 circular references
- 对关键单元格使用 named ranges
- 公式保持简单、可审计
- 对复杂计算添加注释

---

## 分步建模工作流

### 第 1 步：提取历史财务数据

**如果历史财务数据已经提取好，可跳到第 2 步。**

**针对上市公司：**

1. **下载 10-K Filing**
   - 进入 SEC EDGAR：`https://www.sec.gov/edgar/searchedgar/companysearch.html`
   - 搜索公司名称或 ticker
   - 下载最新 10-K（年报）
   - 找到 Item 8: Financial Statements and Supplementary Data

2. **创建 Historical Financials Excel 文件**
   - 文件名：`[Company]_Historical_Financials_[Date].xlsx`
   - 该文件将作为后续模型基础

3. **提取 Income Statement（3-5 年）**
   - 创建 Sheet 1："Historical Income Statement"
   - 提取全部 line items：
     - Revenue，总收入及如有披露则按分部
     - Cost of revenue / COGS
     - Gross profit
     - Operating expenses，拆出 R&D、Sales & Marketing、G&A
     - EBITDA，如未披露则自行计算：EBIT + D&A
     - EBIT / Operating income
     - Interest expense / income
     - Other income / expense
     - Pre-tax income
     - Income tax 和 tax rate
     - Net income
     - EPS，basic 和 diluted
     - Shares outstanding，basic 和 diluted

4. **提取 Cash Flow Statement（3-5 年）**
   - 创建 Sheet 2："Historical Cash Flow"
   - 提取全部 line items：
     - Operating activities，从 net income 起
     - Depreciation & amortization
     - Stock-based compensation
     - Changes in working capital，receivables、inventory、payables
     - Cash from operations
     - Investing activities，CapEx、acquisitions
     - Financing activities，debt issuance / repayment、equity、dividends
     - Net change in cash
     - Beginning and ending cash

5. **提取 Balance Sheet（3-5 年）**
   - 创建 Sheet 3："Historical Balance Sheet"
   - 提取全部 line items：
     - Current assets，cash、receivables、inventory、other
     - Non-current assets，PP&E、intangibles、goodwill
     - Total assets
     - Current liabilities，payables、accrued expenses、current debt
     - Non-current liabilities，long-term debt、deferred taxes
     - Total liabilities
     - Shareholders' equity，common stock、retained earnings
     - Total liabilities + equity

6. **计算历史指标**
   - 创建 Sheet 4："Historical Metrics"
   - 从三张报表计算：
     - Revenue growth %（YoY）
     - Gross margin %
     - EBITDA margin %
     - Operating margin %
     - Net margin %
     - Free cash flow（CFO - CapEx）
     - FCF margin %
     - ROIC（近似：NOPAT / Invested Capital）
     - Debt/Equity ratio
     - Current ratio（Current Assets / Current Liabilities）

7. **记录来源与说明**
   - 创建 Sheet 5："Notes"
   - 记录：
     - 10-K filing date 和 fiscal year end
     - 任何一次性项目或调整
     - Non-GAAP 与 GAAP 差异
     - 分部拆分，如按产品 / 地区披露收入
     - 数据质量说明与局限性

**针对私有公司：**

1. **收集可获得数据**
   - 财务报表，如有
   - 含收入数据的 press releases
   - 融资公告
   - 行业估算或可比公司数据

2. **创建简化版历史文件**
   - 估算收入，如可获得
   - 估算利润率，如需借助可比公司
   - 关键比率和指标
   - 记录全部假设和来源

**Verification：**
- [ ] 已提取 3 张财务报表，3-5 年
- [ ] 报表间数字勾稽正确，net income 一致
- [ ] 关键指标计算正确
- [ ] Excel 文件已保存且可打开
- [ ] 数据来源已记录，10-K 日期、页码等

**投射模型基础现已完成。进入第 2 步。**
   - Capital expenditures
   - Working capital items
   - Debt and interest expense
   - Share count（basic 和 diluted）

3. **整理历史数据供录入**
   - 准备 3-5 年 actuals
   - 将其直接录入 Income Statement、Cash Flow Statement、Balance Sheet tabs
   - 历史年份放在前列，预测年份在后

4. **计算历史趋势**
   - Revenue CAGR
   - Margin progression
   - OpEx leverage
   - Working capital patterns
   - CapEx 占收入比例
   - 这些趋势将用于支持预测假设

**Note**：假设将直接记录在各个 tab 的蓝色输入单元格中，而不是单独放在一个 tab。

### 第 2 步：建立 Revenue Model

**CRITICAL：这是模型中最重要、也最细致的部分。**

#### A. Revenue by Product / Category（20-30 行）

创建详细表：
```
                        2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
Product Category A
  Sub-product A1        XX      XX      XX      XX      XX      XX      XX      XX      XX
  Sub-product A2        XX      XX      XX      XX      XX      XX      XX      XX      XX
  Sub-product A3        XX      XX      XX      XX      XX      XX      XX      XX      XX
  Category A Total      XX      XX      XX      XX      XX      XX      XX      XX      XX
  % of Total Rev        X%      X%      X%      X%      X%      X%      X%      X%      X%
  YoY Growth %          -       X%      X%      X%      X%      X%      X%      X%      X%

Product Category B
  [Similar structure]

[Continue for all product categories]

Services Revenue        XX      XX      XX      XX      XX      XX      XX      XX      XX
Other Revenue           XX      XX      XX      XX      XX      XX      XX      XX      XX

TOTAL REVENUE           XX      XX      XX      XX      XX      XX      XX      XX      XX
Total Revenue Growth %  -       X%      X%      X%      X%      X%      X%      X%      X%
```

**关键要求：**
- 展示每个 category 的绝对收入（$M）
- 计算每个 category 占总收入比例
- 展示每个 category 的 YoY 增长率
- 必须做到 granular sub-categories，而不仅是 3-5 个大类
- 展示业务 mix shift
- 所有预测都要联动到 Assumptions tab

#### B. Revenue by Geography（15-20 行）

创建详细表：
```
                        2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
North America
  United States         XX      XX      XX      XX      XX      XX      XX      XX      XX
  Canada                XX      XX      XX      XX      XX      XX      XX      XX      XX
  Mexico                XX      XX      XX      XX      XX      XX      XX      XX      XX
  NA Total              XX      XX      XX      XX      XX      XX      XX      XX      XX
  % of Total            X%      X%      X%      X%      X%      X%      X%      X%      X%
  YoY Growth %          -       X%      X%      X%      X%      X%      X%      X%      X%

Europe
  UK                    XX      XX      XX      XX      XX      XX      XX      XX      XX
  Germany               XX      XX      XX      XX      XX      XX      XX      XX      XX
  France                XX      XX      XX      XX      XX      XX      XX      XX      XX
  Other Europe          XX      XX      XX      XX      XX      XX      XX      XX      XX
  Europe Total          XX      XX      XX      XX      XX      XX      XX      XX      XX
  % of Total            X%      X%      X%      X%      X%      X%      X%      X%      X%
  YoY Growth %          -       X%      X%      X%      X%      X%      X%      X%      X%

Asia-Pacific
  [Similar structure]

Rest of World
  [Similar structure]

TOTAL REVENUE           XX      XX      XX      XX      XX      XX      XX      XX      XX
```

**Verification：**
- 按产品拆分总收入 = 按地区拆分总收入 = Total revenue
- 所有百分比加总为 100%
- 增长率计算正确

#### C. Revenue by Channel（如适用）

```
                        2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
Direct Sales            XX      XX      XX      XX      XX      XX      XX      XX      XX
E-commerce/Online       XX      XX      XX      XX      XX      XX      XX      XX      XX
Wholesale/Partner       XX      XX      XX      XX      XX      XX      XX      XX      XX
Retail Stores
  Company-owned stores  XX      XX      XX      XX      XX      XX      XX      XX      XX
  Store count           XX      XX      XX      XX      XX      XX      XX      XX      XX
  Sales per store       XX      XX      XX      XX      XX      XX      XX      XX      XX
Other Channels          XX      XX      XX      XX      XX      XX      XX      XX      XX

TOTAL REVENUE           XX      XX      XX      XX      XX      XX      XX      XX      XX
```

### 第 3 步：建立 Operating Expenses 模型

#### A. Cost of Revenue
1. **拆分 COGS 组成部分**
   - 产品成本，材料、制造
   - Shipping 和 logistics
   - Service delivery costs
   - 其他直接成本

2. **与收入联动**
   - 计算 COGS 占收入比例
   - 按年份建模 gross margin
   - 联动到 Assumptions tab

#### B. R&D Expenses
```
Research & Development  2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
R&D Headcount           XX      XX      XX      XX      XX      XX      XX      XX      XX
R&D Comp per head       XX      XX      XX      XX      XX      XX      XX      XX      XX
R&D Personnel Costs     XX      XX      XX      XX      XX      XX      XX      XX      XX
R&D Other Costs         XX      XX      XX      XX      XX      XX      XX      XX      XX
Total R&D               XX      XX      XX      XX      XX      XX      XX      XX      XX
% of Revenue            X%      X%      X%      X%      X%      X%      X%      X%      X%
```

#### C. Sales & Marketing Expenses
```
Sales & Marketing       2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
S&M Headcount           XX      XX      XX      XX      XX      XX      XX      XX      XX
S&M Comp per head       XX      XX      XX      XX      XX      XX      XX      XX      XX
S&M Personnel Costs     XX      XX      XX      XX      XX      XX      XX      XX      XX
Marketing Spend         XX      XX      XX      XX      XX      XX      XX      XX      XX
S&M Other Costs         XX      XX      XX      XX      XX      XX      XX      XX      XX
Total S&M               XX      XX      XX      XX      XX      XX      XX      XX      XX
% of Revenue            X%      X%      X%      X%      X%      X%      X%      X%      X%
```

#### D. General & Administrative
```
G&A                     2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
G&A Headcount           XX      XX      XX      XX      XX      XX      XX      XX      XX
G&A Comp per head       XX      XX      XX      XX      XX      XX      XX      XX      XX
G&A Personnel Costs     XX      XX      XX      XX      XX      XX      XX      XX      XX
G&A Other Costs         XX      XX      XX      XX      XX      XX      XX      XX      XX
Total G&A               XX      XX      XX      XX      XX      XX      XX      XX      XX
% of Revenue            X%      X%      X%      X%      X%      X%      X%      X%      X%
```

#### E. Depreciation & Amortization
- 联动到 CapEx schedule
- 根据 Assumptions 中的折旧率建模
- 计算年度 D&A

### 第 4 步：建立 Income Statement

**创建完整 P&L，40-50 个 line items：**

```
INCOME STATEMENT        2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E

REVENUE
[Link to Revenue Model tab]
Total Revenue           XX      XX      XX      XX      XX      XX      XX      XX      XX
  YoY Growth %          -       X%      X%      X%      X%      X%      X%      X%      X%

COST OF REVENUE
[Link to COGS breakdown]
Total COGS              XX      XX      XX      XX      XX      XX      XX      XX      XX

GROSS PROFIT            XX      XX      XX      XX      XX      XX      XX      XX      XX
  Gross Margin %        X%      X%      X%      X%      X%      X%      X%      X%      X%

OPERATING EXPENSES
Total R&D               XX      XX      XX      XX      XX      XX      XX      XX      XX
  % of Revenue          X%      X%      X%      X%      X%      X%      X%      X%      X%
Total S&M               XX      XX      XX      XX      XX      XX      XX      XX      XX
  % of Revenue          X%      X%      X%      X%      X%      X%      X%      X%      X%
Total G&A               XX      XX      XX      XX      XX      XX      XX      XX      XX
  % of Revenue          X%      X%      X%      X%      X%      X%      X%      X%      X%
Depreciation & Amort.   XX      XX      XX      XX      XX      XX      XX      XX      XX

Total Operating Exp.    XX      XX      XX      XX      XX      XX      XX      XX      XX
  % of Revenue          X%      X%      X%      X%      X%      X%      X%      X%      X%

EBITDA                  XX      XX      XX      XX      XX      XX      XX      XX      XX
  EBITDA Margin %       X%      X%      X%      X%      X%      X%      X%      X%      X%

EBIT                    XX      XX      XX      XX      XX      XX      XX      XX      XX
  EBIT Margin %         X%      X%      X%      X%      X%      X%      X%      X%      X%

Interest expense        (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
Interest income         XX      XX      XX      XX      XX      XX      XX      XX      XX
Other income/(expense)  XX      XX      XX      XX      XX      XX      XX      XX      XX

Pre-tax income          XX      XX      XX      XX      XX      XX      XX      XX      XX

Income tax              (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
  Tax rate %            X%      X%      X%      X%      X%      X%      X%      X%      X%

NET INCOME              XX      XX      XX      XX      XX      XX      XX      XX      XX
  Net Margin %          X%      X%      X%      X%      X%      X%      X%      X%      X%

SHARES OUTSTANDING
Basic shares (M)        XX      XX      XX      XX      XX      XX      XX      XX      XX
Diluted shares (M)      XX      XX      XX      XX      XX      XX      XX      XX      XX

EARNINGS PER SHARE
Basic EPS               $X.XX   $X.XX   $X.XX   $X.XX   $X.XX   $X.XX   $X.XX   $X.XX   $X.XX
Diluted EPS             $X.XX   $X.XX   $X.XX   $X.XX   $X.XX   $X.XX   $X.XX   $X.XX   $X.XX
```

### 第 5 步：建立 Cash Flow Statement

```
CASH FLOW STATEMENT     2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E

OPERATING ACTIVITIES
Net Income              XX      XX      XX      XX      XX      XX      XX      XX      XX
Adjustments:
  Depreciation & Amort. XX      XX      XX      XX      XX      XX      XX      XX      XX
  Stock-based comp      XX      XX      XX      XX      XX      XX      XX      XX      XX
  Other non-cash        XX      XX      XX      XX      XX      XX      XX      XX      XX

Changes in WC:
  Accounts Receivable   (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
  Inventory             (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
  Accounts Payable      XX      XX      XX      XX      XX      XX      XX      XX      XX
  Other working capital (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)

Cash from Operations    XX      XX      XX      XX      XX      XX      XX      XX      XX

INVESTING ACTIVITIES
Capital Expenditures    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
Acquisitions            (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
Other investing         XX      XX      XX      XX      XX      XX      XX      XX      XX

Cash from Investing     (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)

FREE CASH FLOW          XX      XX      XX      XX      XX      XX      XX      XX      XX
  FCF Margin %          X%      X%      X%      X%      X%      X%      X%      X%      X%

FINANCING ACTIVITIES
Debt issuance           XX      XX      XX      XX      XX      XX      XX      XX      XX
Debt repayment          (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
Equity issuance         XX      XX      XX      XX      XX      XX      XX      XX      XX
Dividends paid          (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
Other financing         XX      XX      XX      XX      XX      XX      XX      XX      XX

Cash from Financing     XX      XX      XX      XX      XX      XX      XX      XX      XX

NET CHANGE IN CASH      XX      XX      XX      XX      XX      XX      XX      XX      XX

Beginning Cash          XX      XX      XX      XX      XX      XX      XX      XX      XX
Ending Cash             XX      XX      XX      XX      XX      XX      XX      XX      XX
```

### 第 6 步：建立 Balance Sheet

创建完整 balance sheet，35-45 个 line items：

```
BALANCE SHEET           2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E

ASSETS
Current Assets:
  Cash & Equivalents    XX      XX      XX      XX      XX      XX      XX      XX      XX
  Accounts Receivable   XX      XX      XX      XX      XX      XX      XX      XX      XX
  Inventory             XX      XX      XX      XX      XX      XX      XX      XX      XX
  Prepaid expenses      XX      XX      XX      XX      XX      XX      XX      XX      XX
  Other current assets  XX      XX      XX      XX      XX      XX      XX      XX      XX
Total Current Assets    XX      XX      XX      XX      XX      XX      XX      XX      XX

Non-Current Assets:
  PP&E, gross           XX      XX      XX      XX      XX      XX      XX      XX      XX
  Accumulated Depr.     (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
  PP&E, net             XX      XX      XX      XX      XX      XX      XX      XX      XX
  Intangible assets     XX      XX      XX      XX      XX      XX      XX      XX      XX
  Goodwill              XX      XX      XX      XX      XX      XX      XX      XX      XX
  Other non-current     XX      XX      XX      XX      XX      XX      XX      XX      XX
Total Non-Current       XX      XX      XX      XX      XX      XX      XX      XX      XX

TOTAL ASSETS            XX      XX      XX      XX      XX      XX      XX      XX      XX

LIABILITIES
Current Liabilities:
  Accounts Payable      XX      XX      XX      XX      XX      XX      XX      XX      XX
  Accrued expenses      XX      XX      XX      XX      XX      XX      XX      XX      XX
  Deferred revenue      XX      XX      XX      XX      XX      XX      XX      XX      XX
  Current debt          XX      XX      XX      XX      XX      XX      XX      XX      XX
  Other current liab.   XX      XX      XX      XX      XX      XX      XX      XX      XX
Total Current Liab.     XX      XX      XX      XX      XX      XX      XX      XX      XX

Non-Current Liabilities:
  Long-term debt        XX      XX      XX      XX      XX      XX      XX      XX      XX
  Deferred taxes        XX      XX      XX      XX      XX      XX      XX      XX      XX
  Other non-current     XX      XX      XX      XX      XX      XX      XX      XX      XX
Total Non-Current Liab. XX      XX      XX      XX      XX      XX      XX      XX      XX

TOTAL LIABILITIES       XX      XX      XX      XX      XX      XX      XX      XX      XX

EQUITY
  Common stock          XX      XX      XX      XX      XX      XX      XX      XX      XX
  Additional paid-in    XX      XX      XX      XX      XX      XX      XX      XX      XX
  Retained earnings     XX      XX      XX      XX      XX      XX      XX      XX      XX
  Treasury stock        (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
  Other equity          XX      XX      XX      XX      XX      XX      XX      XX      XX
TOTAL EQUITY            XX      XX      XX      XX      XX      XX      XX      XX      XX

TOTAL LIAB + EQUITY     XX      XX      XX      XX      XX      XX      XX      XX      XX

BALANCE CHECK           OK      OK      OK      OK      OK      OK      OK      OK      OK
```

**Balance Check Formula：**
- 对每一年，Total Assets 必须等于 Total Liabilities + Equity
- 任何不平衡都要用红色标示

### 第 7 步：建立 DCF Inputs Tab

为估值（Task 3）准备输入：

```
DCF INPUTS              2025E   2026E   2027E   2028E   2029E

EBIT                    XX      XX      XX      XX      XX
Tax Rate                X%      X%      X%      X%      X%
NOPAT                   XX      XX      XX      XX      XX

Add: D&A                XX      XX      XX      XX      XX
Less: CapEx             (XX)    (XX)    (XX)    (XX)    (XX)
Less: Chg in NWC        (XX)    (XX)    (XX)    (XX)    (XX)

UNLEVERED FCF           XX      XX      XX      XX      XX

Terminal Year Metrics:
  2029E Revenue         $X,XXX
  2029E EBITDA          $XXX
  2029E EBIT            $XXX
  2029E Unlevered FCF   $XXX
```

### 第 8 步：建立 Scenarios Tab

创建三种情景及其差异化假设：

#### Scenario Assumptions Table
```
Assumption                      Bull        Base        Bear
Revenue CAGR (2025-2029)        XX%         XX%         XX%
Gross Margin 2029E              XX%         XX%         XX%
EBITDA Margin 2029E             XX%         XX%         XX%
CapEx as % of Revenue           X%          X%          X%
[Add other key assumptions]
```

#### Scenario Output Table
```
Metric                          Bull        Base        Bear
2029E Revenue ($M)              $X,XXX      $X,XXX      $X,XXX
2029E EBITDA ($M)               $XXX        $XXX        $XXX
2029E EBITDA Margin             XX%         XX%         XX%
2029E Net Income ($M)           $XXX        $XXX        $XXX
2029E EPS                       $X.XX       $X.XX       $X.XX
2029E FCF ($M)                  $XXX        $XXX        $XXX
2029E FCF Margin                XX%         XX%         XX%

Cumulative FCF 2025-2029 ($M)   $XXX        $XXX        $XXX
```

**记录情景逻辑：**
- Bull case：[描述乐观但可实现的假设]
- Base case：[描述最可能发生的情景]
- Bear case：[描述下行风险与触发因素]

### 第 9 步：质量检查

**验证模型完整性：**
1. [ ] 检查公式，抽样测试关键计算
2. [ ] 修改假设，确认模型联动更新正确
3. [ ] 测试情景切换
4. [ ] 验证颜色编码，blue/black/green
5. [ ] 检查所有年份的 balance sheet 是否平衡
6. [ ] 验证无 circular references，Excel 会提示
7. [ ] 检查预测中是否出现硬编码数字
8. [ ] 验证所有跨表链接是否正常
9. [ ] 测试 revenue totals 在各 tabs 中是否一致
10. [ ] 审查格式和展示质量

---

## 质量标准

### 模型完整性
- 所有公式在不同工作表之间正确联动
- 预测部分不出现硬编码数字，除 Assumptions tab 外
- 无 circular references
- 所有年份 balance sheet 平衡
- 情景切换运作正确

### 完整性
- 6 个核心 tabs 完整存在：Revenue Model、Income Statement、Cash Flow Statement、Balance Sheet、Scenarios、DCF Inputs
- Income Statement 含 40-50 个 line items
- Revenue Model 中按产品拆分 20-30 行
- Revenue Model 中按地区拆分 15-20 行
- 完整 cash flow 和 balance sheet，含所有项目
- Bull/Base/Bear 情景完整

### 专业格式
- 一致的颜色编码，blue/black/green
- 清晰标题与标签
- 合理边框与底纹
- 关键单元格使用 named ranges
- grouped rows 支持折叠
- 单位清晰，$ thousands vs. $ millions

### 文档记录
- 假设附带逻辑说明，蓝色输入格及注释
- 数据来源记录在单元格注释或 tabs 内 notes section
- 对复杂计算加注释解释
- 方法论描述清楚

---

## 文件命名规范

财务模型命名为：
`[Company]_Financial_Model_[Date].xlsx`

示例：`Tesla_Financial_Model_2024-10-27.xlsx`

---

## 成功标准

一个成功的财务模型应当：
1. 拥有全部 6 个核心 tabs
2. 完全动态化，修改假设即可联动更新
3. 预测中不存在硬编码数字
4. 包含详细收入拆分，按产品 20-30 行，按地区 15-20 行
5. Income Statement 含 40-50 个 line items
6. 包含 Bull/Base/Bear 情景
7. 格式专业，颜色编码规范
8. 勾稽正确，balance sheet 与 cash flow 平衡
9. 可审计、易追踪
10. 能为估值分析提供正确 FCF 输入

---

## 常见模型类型 - 特殊考虑

### High-Growth Tech / SaaS
- 重点看 ARR growth 和 net retention
- 按产品线和地区建模
- R&D 与 S&M 投入较高
- 盈利路径时间线
- Unit economics，LTV/CAC

### E-commerce / Retail
- 按产品类别和渠道拆分收入
- 店铺数量与同店增长，如适用
- 库存周转与营运资本
- 履约成本
- Customer acquisition

### Manufacturing / Industrial
- 产能利用率
- 原材料成本与定价
- Gross margin bridge，量 / 价 / mix / 成本
- 重 CapEx 模型
- Working capital cycles

---

## 下一步

完成 Task 2 后，财务模型将用于：
- **Task 3 (Valuation)**：提供 DCF inputs 和预测财务数据
- **Task 4 (Charts)**：提供收入趋势、利润率图和情景对比图的数据
- **Task 5 (Report Assembly)**：为报告表格和定量分析提供财务数据
