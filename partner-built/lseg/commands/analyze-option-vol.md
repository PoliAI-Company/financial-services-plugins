---
description: 结合波动率曲面、Greeks 和隐含波动率与已实现波动率对比分析期权波动率
argument-hint: "<underlying e.g. .SPX or EURUSD> [strike] [expiry]"
---

# 分析期权波动率

> 这个命令使用 LSEG 波动率曲面、期权定价和历史数据工具。可用工具见 [CONNECTORS.md](../CONNECTORS.md)。

通过生成标的的波动率曲面、为期权定价并返回完整 Greeks、再比较隐含波动率和已实现波动率，分析当前波动率环境。

波动率曲面解读和 Greeks 分析的领域知识见 **option-vol-analysis** skill。

## 工作流

### 1. 收集输入

向用户询问：
- 标的资产，必填：
  - 股票或指数使用 RIC 格式，例如 `VOD.L@RIC`、`.SPX@RIC`
  - 期货使用 RICROOT 格式，例如 `ES@RICROOT`、`CL@RICROOT`
  - 外汇使用 ISO 货币对，例如 `EURUSD`、`USDJPY`
- 执行价，可选，默认 ATM
- 到期日或期限，可选，默认 3M
- 看涨或看跌，可选，默认两者都看

先判断这是股票/指数还是外汇，以选择正确的波动率曲面工具。

### 2. 生成波动率曲面

**对于股票、指数和期货：** 调用 `equity_vol_surface`。

**对于外汇：** 调用 `fx_vol_surface`。

提取各期限 ATM 波动率、25-delta risk reversal 和 25-delta butterfly。

### 3. 发现期权模板

为标的调用 `option_template_list`，识别可用类型、到期日和执行价。

### 4. 为期权定价

使用标的、执行价和到期日调用 `option_value`。

提取权利金、delta、gamma、vega、theta 和隐含波动率。

### 5. 计算已实现波动率

调用 `tscc_historical_pricing_summaries`，参数使用 `interval: "P1D"` 和 `tenor: "1Y"`。

计算 20 日、60 日和 90 日 close-to-close 已实现波动率，并与对应期限的隐含波动率比较。

### 6. 综合报告

展示波动率曲面摘要表、Greeks 表、隐含波动率与已实现波动率对比、波动率区间判断以及策略建议。

## 输出格式

先给出最关键的波动率判断，也就是隐含波动率相对已实现波动率偏贵还是偏便宜。然后再展示曲面摘要、期权定价和详细对比。
