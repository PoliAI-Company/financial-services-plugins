---
description: 结合国债和通胀覆盖层分析掉期曲线，识别曲线交易机会
argument-hint: "<currency e.g. EUR> [index e.g. ESTR]"
---

# 分析掉期曲线

> 这个命令使用 LSEG 掉期定价、利率曲线和通胀曲线工具。可用工具见 [CONNECTORS.md](../CONNECTORS.md)。

构建并分析利率掉期曲线，叠加国债收益率和通胀盈亏平衡，并识别曲线交易机会。

曲线分析和交易构建的领域知识见 **swap-curve-strategy** skill。

## 工作流

### 1. 收集输入

向用户询问：
- 货币，必填，例如 EUR、USD、GBP、CHF、JPY
- 参考利率指数，可选，例如 ESTR、SOFR、SONIA、TONA
- 估值日期，可选，默认今天

### 2. 发现掉期模板

用目标货币和可选指数，以 list 模式调用 `ir_swap`。

提取可用模板引用、指数细节和市场惯例。

### 3. 构建掉期曲线

对标准期限 2Y、5Y、7Y、10Y、20Y、30Y，以 price 模式调用 `ir_swap`。

提取各期限的平价掉期利率和 DV01。

### 4. 叠加国债曲线

为同一货币调用 `interest_rate_curve`，先 list 再 calculate。

计算每一期限的掉期利差，也就是掉期利率减去国债收益率。

### 5. 拆解实际利率

为该货币调用 `inflation_curve`，先 search 再 calculate。

计算实际掉期利率，也就是名义掉期利率减去通胀盈亏平衡。

### 6. 综合曲线策略观点

计算曲线指标，包括 2s10s slope、5s30s slope 和 2s5s10s butterfly。

根据当前水平与历史常态的比较，识别 steepener、flattener、butterfly 或 swap spread 交易机会。

展示掉期曲线表，带国债覆盖层、曲线指标、实际利率拆解，以及带 DV01 中性比例的交易建议。

## 输出格式

先给出曲线形态摘要和关键指标，比如 2s10s 和 butterfly。然后再提供详细表格和交易建议部分。
