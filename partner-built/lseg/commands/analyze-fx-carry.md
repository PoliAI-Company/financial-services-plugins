---
description: 结合即期、远期、波动率曲面和历史背景评估外汇套息交易机会
argument-hint: "<currency pair e.g. USDJPY> [tenor e.g. 3M]"
---

# 分析外汇套息交易

> 这个命令使用 LSEG 外汇定价、远期曲线、波动率曲面和历史数据工具。可用工具见 [CONNECTORS.md](../CONNECTORS.md)。

通过结合即期汇率、远期点、carry 期限结构、波动率风险和历史价格背景，评估某个货币对的套息交易机会。

套息框架和风险指标的领域知识见 **fx-carry-trade** skill。

## 工作流

### 1. 收集输入

向用户询问：
- 货币对，必填，例如 USDJPY、EURUSD、AUDUSD
- 目标期限，可选，默认 3M
- 估值日期，可选，默认今天

### 2. 获取即期汇率

对货币对调用 `fx_spot_price`。

提取中间价、买价、卖价和 bid-ask spread。

### 3. 为目标期限远期定价

对货币对和目标期限调用 `fx_forward_price`。

提取 forward rate 和 forward points，并计算年化 carry。

### 4. 映射完整 carry 曲线

对货币对调用 `fx_forward_curve`，先 list 再 calculate。

展示各期限，从隔夜到 1Y 的 carry 画像，包括 forward points、annualized carry 和 cumulative carry，并识别 sweet-spot tenor。

### 5. 评估波动率风险

对货币对调用 `fx_vol_surface`。

提取目标期限上的 ATM vol、25-delta risk reversal 和 25-delta butterfly。

计算 carry-to-vol ratio，也就是年化 carry 除以 ATM 隐含波动率。

### 6. 历史现货背景

使用货币对的 RIC 调用 `tscc_historical_pricing_summaries`，参数为 `interval: "P1D"` 和 `tenor: "1Y"`。

评估 52 周区间、当前所处位置和趋势方向。

### 7. 综合报告

展示 carry-to-vol ratio 和总体判断、即期与远期定价、carry 期限结构表、波动率曲面快照和历史背景。

## 输出格式

先给出 carry-to-vol ratio 及总体判断，也就是 attractive、moderate 或 unattractive。然后用表格给出详细支撑数据。
