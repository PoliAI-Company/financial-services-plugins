---
description: 生成包含一致预期、基本面和价格表现的完整股票研究快照
argument-hint: "<ticker e.g. AAPL> [period e.g. FY2024-FY2026]"
---

# 股票研究

> 这个命令使用 LSEG 定量分析、历史定价和宏观经济数据工具。可用工具见 [CONNECTORS.md](../CONNECTORS.md)。

生成一份完整的股票研究快照，整合分析师一致预期、历史财务数据、价格表现和宏观背景。

基本面分析和预期解读的领域知识见 **equity-research** skill。

## 工作流

### 1. 收集输入

向用户询问：
- 股票代码，必填，使用 IBES ticker 格式，例如 AAPL、MSFT、VOD
- 关注的前瞻期间，可选，默认未来 2 个财政年度
- 是否有特定关注点，例如 earnings、revenue、dividends

### 2. 获取一致预期

使用 ticker 调用 `qa_ibes_consensus`，获取 FY1 和 FY2 预期。
- 指标包括 EPS、Revenue、EBITDA、DPS
- 周期类型使用 `A`，也就是年度

提取中位数或均值预期、分析师数量、高低区间和离散度。

### 3. 拉取历史基本面

调用 `qa_company_fundamentals` 获取过去 3 到 5 个财政年度数据。

提取收入增长、利润率趋势、杠杆和盈利轨迹。

### 4. 评估价格表现

调用 `qa_historical_equity_price` 获取 1 年历史。

计算年初至今回报、1 年回报、52 周区间和 beta。

### 5. 近期价格行为细节

调用 `tscc_historical_pricing_summaries`，参数使用 `interval: "P1D"` 和 `tenor: "3M"`。

提取日度 OHLCV、成交量趋势和近期动量。

### 6. 宏观背景

在公司主要市场上调用 `qa_macroeconomic` 获取 GDP、CPI 和政策利率。

总结宏观环境对该行业是顺风还是逆风。

### 7. 综合报告

展示一致预期表、历史财务摘要、估值指标，比如 forward P/E，也就是价格除以一致 EPS，价格表现、宏观背景，以及投资逻辑摘要。

## 输出格式

以结构化研究笔记形式展示。先给出 1 到 2 句话的投资逻辑摘要，然后用表格和分区展开支撑内容。
