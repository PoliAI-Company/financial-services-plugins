---
description: 结合定价、参考数据、现金流和情景分析复核固定收益组合
argument-hint: "<ISIN1,ISIN2,...> [scenario e.g. +100bp]"
---

# 复核固定收益组合

> 这个命令使用 LSEG 债券定价、YieldBook 分析和收益率曲线工具。可用工具见 [CONNECTORS.md](../CONNECTORS.md)。

通过为全部持仓定价、补充参考数据、投影现金流并在利率情景下进行压力测试，生成一份汇总后的固定收益组合风险与收益报告。

组合分析和情景分析的领域知识见 **fixed-income-portfolio** skill。

## 工作流

### 1. 收集组合持仓

向用户询问：
- 债券标识符，必填，逗号分隔的 ISIN、CUSIP 或 RIC
- 持仓规模或权重，可选，如果未提供则假设等权
- 要测试的特定情景，可选，例如 `+100bp`，默认使用标准情景网格
- 估值日期，可选，默认今天

### 2. 为全部债券定价

使用全部标识符调用 `bond_price`。

提取每只债券的 clean/dirty price、yield、duration、convexity、DV01 和 currency。

聚合组合层面指标，包括加权收益率、加权久期、总 DV01 和总市值。

### 3. 补充参考数据

为每只债券调用 `yieldbook_bond_reference`。

提取 security type、sector、ratings、coupon type、call features、issuer 和 country。

构建按行业、评级、到期桶和货币划分的组合结构拆解。

### 4. 投影现金流

为每只债券调用 `yieldbook_cashflow`。

将结果聚合成季度现金流瀑布，并标记到期集中的时间段。

### 5. 运行情景分析

使用利率冲击调用 `yieldbook_scenario`，包括 -200bp、-100bp、-50bp、0bp、+50bp、+100bp、+200bp。

识别哪些债券对上行和下行风险贡献最大。

### 6. 曲线背景

为组合主要货币调用 `interest_rate_curve`。

计算每只债券相对曲线的利差，并评估当前曲线环境。

### 7. 综合报告

呈现组合摘要指标、结构拆解、现金流瀑布、带风险贡献者的情景 P&L 表，以及曲线暴露。

## 输出格式

先展示组合摘要指标，然后分章节展开结构、现金流和风险分析。
