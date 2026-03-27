# Merger Model

description: 为并购交易构建增厚/摊薄分析。建模 pro forma EPS 影响、协同效应敏感性及 purchase price allocation。适用于评估潜在收购、为 pitch 准备 merger consequences analysis，或就交易条款提供建议。触发词包括 "merger model"、"accretion dilution"、"M&A model"、"pro forma EPS"、"merger consequences" 和 "deal impact analysis"。

## 工作流

### 第 1 步：收集输入

**Acquirer:**
- 公司名称、当前股价、流通股数
- LTM 和 NTM EPS，GAAP 与 adjusted
- P/E multiple
- 税前债务成本、税率
- 资产负债表现金、现有债务

**Target:**
- 公司名称、当前股价、流通股数，若为上市公司
- LTM 和 NTM EPS 或净利润
- Enterprise value 或 equity value

**Deal Terms:**
- 每股出价，或相对当前股价的溢价
- 对价结构，现金占比与股票占比
- 为现金部分融资而新增的债务
- 预期协同效应，收入和成本，以及释放节奏
- 交易费用与融资费用
- 预期交割日期

### 第 2 步：Purchase Price Analysis

| Item | Value |
|------|-------|
| Offer price per share | |
| Premium to current | |
| Equity value | |
| Plus: net debt assumed | |
| Enterprise value | |
| EV / EBITDA implied | |
| P/E implied | |

### 第 3 步：Sources & Uses

| Sources | $ | Uses | $ |
|---------|---|------|---|
| New debt | | Equity purchase price | |
| Cash on hand | | Refinance target debt | |
| New equity issued | | Transaction fees | |
| | | Financing fees | |
| **Total** | | **Total** | |

### 第 4 步：Pro Forma EPS，Accretion / Dilution

按年度计算，Year 1 到 3：

| | Standalone | Pro Forma | Accretion/(Dilution) |
|---|-----------|-----------|---------------------|
| Acquirer net income | | | |
| Target net income | | | |
| Synergies (after tax) | | | |
| Foregone interest on cash (after tax) | | | |
| New debt interest (after tax) | | | |
| Intangible amortization (after tax) | | | |
| Pro forma net income | | | |
| Pro forma shares | | | |
| **Pro forma EPS** | | | |
| **Accretion / (Dilution) %** | | | |

### 第 5 步：敏感性分析

**Accretion/Dilution vs. Synergies and Offer Premium:**

| | $0M syn | $25M syn | $50M syn | $75M syn | $100M syn |
|---|---------|----------|----------|----------|-----------|
| 15% premium | | | | | |
| 20% premium | | | | | |
| 25% premium | | | | | |
| 30% premium | | | | | |

**Accretion/Dilution vs. Cash/Stock Mix:**

| | 100% cash | 75/25 | 50/50 | 25/75 | 100% stock |
|---|-----------|-------|-------|-------|------------|
| Year 1 | | | | | |
| Year 2 | | | | | |

### 第 6 步：盈亏平衡协同效应

计算该交易在 Year 1 实现 EPS 中性的最低协同效应水平。

### 第 7 步：输出

- Excel workbook，包含：
  - Assumptions 标签页
  - Sources & uses
  - Pro forma income statement
  - Accretion/dilution summary
  - Sensitivity tables
  - Breakeven analysis
- 用于 pitch book 的单页 merger consequences summary

## Important Notes

- 在相关场景下，始终同时展示 GAAP 与 adjusted，cash，EPS
- 股票对价交易中，使用收购方当前股价计算 exchange ratio，并说明新发股份带来的摊薄
- 要纳入 purchase price allocation，goodwill 与 intangible amortization 会影响 GAAP EPS
- 协同效应释放节奏很关键，Year 1 往往只能实现 run-rate synergy 的 25% 到 50%
- 不要漏掉动用现金带来的利息收入损失，以及新增债务的利息费用
- 协同效应和利息调整所用税率应与收购方边际税率一致
