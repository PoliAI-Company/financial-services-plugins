# SEC 文件数据提取参考

**何时使用：** 仅当模型模板明确要求从 SEC 文件（10-K、10-Q）中提取数据时参考此文件。对于直接提供数据或使用其他数据源的模板，不需要此参考。

---

## 从 SEC 文件（10-K / 10-Q）中提取数据

当用上市公司数据填充模型模板时，应直接从 SEC 文件中提取财务数据。

### 第 1 步：定位文件

1. 使用 SEC EDGAR：`https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK=[TICKER]&type=10-K`
2. 对于季度数据，使用 `type=10-Q`

### 第 2 步：识别申报货币

在提取数据前，先识别报告货币：
- 查看封面或页眉中的报告货币
- 查看报表标题（例如 "in thousands of U.S. dollars"）
- 查看附注 1（Summary of Significant Accounting Policies）

**常见货币标识**

| 标识 | 货币 |
|-----------|----------|
| $, USD | 美元 |
| €, EUR | 欧元 |
| £, GBP | 英镑 |
| ¥, JPY | 日元 |
| ¥, CNY, RMB | 人民币 |
| CHF | 瑞士法郎 |
| CAD, C$ | 加元 |

将模型货币设置为与文件一致，并在 Assumptions 标签页中记录。

### 第 3 步：导航到财务报表

在 10-K 或 10-Q 中，定位：
- **Item 8**（10-K）或 **Item 1**（10-Q）：财务报表
- 需要提取的关键部分：
  - Consolidated Statements of Operations（利润表）
  - Consolidated Balance Sheets
  - Consolidated Statements of Cash Flows
  - Notes to Financial Statements（用于明细表）

### 第 4 步：数据提取映射

**利润表（来自 Consolidated Statements of Operations）**

| Filing 行项目 | Model 行项目 |
|------------------|-----------------|
| Net revenues / Net sales | Revenue |
| Cost of goods sold | COGS |
| Selling, general and administrative | SG&A |
| Depreciation and amortization | D&A |
| Interest expense, net | Interest Expense |
| Income tax expense | Taxes |
| Net income | Net Income |

**资产负债表（来自 Consolidated Balance Sheets）**

| Filing 行项目 | Model 行项目 |
|------------------|-----------------|
| Cash and cash equivalents | Cash |
| Accounts receivable, net | AR |
| Inventories | Inventory |
| Property, plant and equipment, net | PP&E (Net) |
| Total assets | Total Assets |
| Accounts payable | AP |
| Short-term debt / Current portion of LT debt | Current Debt |
| Long-term debt | LT Debt |
| Retained earnings | Retained Earnings |
| Total stockholders' equity | Total Equity |

**现金流量表（来自 Consolidated Statements of Cash Flows）**

| Filing 行项目 | Model 行项目 |
|------------------|-----------------|
| Net income | Net Income |
| Depreciation and amortization | D&A |
| Changes in accounts receivable | ΔAR |
| Changes in inventories | ΔInventory |
| Changes in accounts payable | ΔAP |
| Capital expenditures | CapEx |
| Proceeds from issuance of common stock | Equity Issuance |
| Proceeds from / Repayments of debt | Debt activity |
| Dividends paid | Dividends |

### 第 5 步：从附注中提取支持细节

针对各类明细表，从财务报表附注中提取：
- **Note: Debt** → 到期结构、利率、契约条款
- **Note: Property, Plant & Equipment** → PP&E 原值、累计折旧、使用年限
- **Note: Revenue** → 分部拆分、地理拆分
- **Note: Leases** → 经营租赁与融资租赁义务

### 第 6 步：历史数据要求

至少提取 3 年历史数据：
- 10-K 提供 3 年利润表/现金流量表，2 年资产负债表
- 第 3 年资产负债表需从上一年的 10-K 提取
- 如需季度颗粒度，可使用 10-Q 补充

### 数据提取检查清单

- 识别报告货币和单位规模（千、百万）
- 提取 3 年历史利润表
- 提取 3 年历史现金流量表
- 提取 3 年历史资产负债表
- 验证 IS Net Income = CF 起始 Net Income（每年）
- 验证 BS Cash = CF Ending Cash（每年）
- 从附注中提取债务到期表
- 提取 D&A 明细或使用年限假设
- 标注任何一次性或非经常性项目，以便标准化处理

### 处理常见申报差异

| 差异情况 | 处理方式 |
|-----------|---------------|
| D&A 包含在 COGS/SG&A 中 | 从现金流量表中提取 D&A |
| `Other` 项目金额重大 | 查看附注获取拆分 |
| 重述 | 使用重述后的数字，并在 assumptions 中标注 |
| 财年 ≠ 自然年 | 按财年结束日标注（例如 FYE Jan 2025） |
| 非美元报告货币 | 调整模型货币以匹配文件 |
