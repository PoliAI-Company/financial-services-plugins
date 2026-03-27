---
name: 3-statement-model
description: 完成、补齐并填充三大报表财务模型模板（利润表、资产负债表、现金流量表）。当用户要求填写模型模板、补全现有模型框架、用数据填充财务模型、补完部分已填的 IS/BS/CF 框架，或在现有模板结构中连接三张财务报表时使用。触发词包括要求 fill in、complete 或 populate 三大报表模型模板的请求。
---

# 三大报表财务模型模板补全

在利润表、资产负债表和现金流量表之间建立正确勾稽，完成并填充集成财务模型模板。

## 关键原则

- Excel 内运行时使用 Office JS，独立 `.xlsx` 时使用 Python/openpyxl
- 派生单元格一律写公式，不写硬编码结果
- 只有历史实际数和 Assumptions 标签页的驱动假设可以是硬编码数字
- 必须分步向用户展示：模板映射、historicals、IS projections、BS、CF，逐步确认，不能一次性全部完成再展示
- 默认格式使用蓝灰配色，字体颜色用于区分输入、公式和跨表链接

## 模型结构与模板识别

在填充前，需要先识别：
- 各标签页的命名与作用
- 行结构和列结构
- Actuals 与 Estimates 的分隔方式
- named ranges
- projection period 的口径

## 可选分析模块

- Margin Analysis：只有在用户要求或模板明确需要时才加入
- Credit Metrics：只有在用户要求或模板明确需要时才加入
- Scenario Analysis：使用 Base / Upside / Downside 切换
- SEC Filings Data Extraction：如需从 10-K / 10-Q 提取数据，参见 `references/sec-filings.md`

## 模板补全流程

1. 分析模板结构
2. 在不破坏公式的前提下填写数据
3. 验证公式完整性
4. 按工作表做质量检查
5. 做跨报表完整性检查
6. 进行最终复核

## 模型验证与审计

关键检查包括：
- Balance Sheet Balance
- Cash Tie-Out
- Net Income Link
- Retained Earnings
- Equity Financing
- NOL Schedule
- Scenario Hierarchy
- Formula Integrity

所有详细检查表、sign convention、circular reference handling、master check 和 quick debug workflow 保持原始结构与公式说明，供直接套用。
