---
description: 结合 CTD 识别、隐含回购利率和基差交易判断分析债券期货基差
argument-hint: "<bond future RIC e.g. FGBLc1>"
---

# 分析债券期货基差

> 这个命令使用 LSEG 债券期货定价、债券定价、收益率曲线和历史数据工具。可用工具见 [CONNECTORS.md](../CONNECTORS.md)。

通过为期货定价、识别最便宜可交割债券、计算 gross 和 net basis，并评估基差交易机会，分析债券期货基差。

基差机制和交易策略的领域知识见 **bond-futures-basis** skill。

## 工作流

### 1. 收集输入

向用户询问：
- 债券期货 RIC，必填，例如 FGBLc1，也就是 Euro Bund，TYc1，也就是 US 10Y Note，FFIc1，也就是 UK Gilt
- 市场数据日期，可选，默认今天

### 2. 为债券期货定价

对期货 RIC 调用 `bond_future_price`。

提取公允价格、CTD 债券标识符、带转换因子的交割篮子、合约 DV01 和交割日期。

### 3. 为 CTD 债券定价

对第二步中的 CTD 标识符调用 `bond_price`。

提取 clean/dirty price、yield、duration、DV01、accrued interest 和 coupon。

计算 gross basis、invoice price、carry 和 net basis。

### 4. 计算隐含回购利率

为期货对应货币调用 `interest_rate_curve`，先 list 再 calculate，并使用短端利率作为回购代理。

计算 implied repo rate，并将其与市场回购利率比较。

### 5. 跟踪历史基差

对期货和 CTD 债券同时调用 `tscc_historical_pricing_summaries`，参数使用 `tenor: "3M"` 和 `interval: "P1D"`。

评估基差趋势、波动率和历史区间。

### 6. 主权信用背景

对相关主权调用 `credit_curve`，例如 Bund 用 `DE`，Treasury 用 `US`。

### 7. 综合报告

展示期货摘要表、CTD 债券分析、基差计算表，包括 gross 和 net basis、implied repo 对 market repo 的比较、历史背景，以及交易建议，也就是 long basis、short basis 或 neutral。

## 输出格式

先给出基差交易判断，也就是 long、short 或 neutral，并说明 implied repo 的比较结果。然后再展示详细分析表。
