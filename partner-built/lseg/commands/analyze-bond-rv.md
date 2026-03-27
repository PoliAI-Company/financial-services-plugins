---
description: 结合收益率曲线、信用利差和情景压力测试分析债券相对价值
argument-hint: "<ISIN, RIC, or CUSIP> [vs benchmark]"
---

# 分析债券相对价值

> 这个命令使用 LSEG 债券定价、收益率曲线、信用曲线和情景分析工具。可用工具见 [CONNECTORS.md](../CONNECTORS.md)。

通过结合定价分析、收益率曲线背景、信用利差拆解和利率冲击情景，对一只或多只债券进行相对价值分析。

利差框架和贵贱判断的领域知识见 **bond-relative-value** skill。

## 工作流

### 1. 收集债券标识符

向用户询问：
- 债券标识符，必填，可使用 ISIN、RIC 或 CUSIP
- 可选的基准债券，用于比较
- 估值日期，可选，默认今天

### 2. 为债券定价

使用标识符调用 `bond_price`。

提取 clean/dirty price、yield、duration、convexity、DV01 和 currency。

如果提供了基准债券，也为其定价。

### 3. 获取无风险收益率曲线

为债券货币调用 `interest_rate_curve`，先 list 再 calculate。

在债券到期点插值，计算 G-spread。

### 4. 获取信用利差曲线

调用 `credit_curve`，先按 country 或 issuerType 搜索，再 calculate。

计算 residual spread，也就是债券 G-spread 减去对应到期期限上的信用曲线利差。正 residual 表示偏便宜，负 residual 表示偏贵。

### 5. 运行情景分析

使用平行利率冲击调用 `yieldbook_scenario`，包括 -100bp、-50bp、0bp、+50bp、+100bp。

提取各情景下的价格变化和 P&L。

### 6. 综合报告

展示债券摘要表、利差拆解，包括 G-spread、信用利差和 residual、情景 P&L 表，以及贵贱判断。

如果提供了基准债券，加入并排比较。

## 输出格式

先给出贵贱判断及其支撑证据，然后展示利差拆解和情景表。
