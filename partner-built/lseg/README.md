# LSEG 金融分析插件

使用 LSEG 金融数据与分析能力，对债券定价、分析收益率曲线、评估外汇套息交易、为期权估值，并构建宏观仪表板。

## 这个插件做什么

这个插件将 LSEG 的金融分析 MCP 工具封装为 8 个高层工作流，把多个工具调用串联成常见的金融分析任务。你不必逐个调用底层工具，每条命令都会把 4 到 5 个工具编排成一套连贯分析。

## 命令

| 命令 | 说明 |
|---------|-------------|
| `/analyze-bond-rv` | 通过利差拆解和情景压力测试分析债券相对价值 |
| `/analyze-fx-carry` | 结合即期、远期、波动率曲面和历史背景评估外汇套息机会 |
| `/research-equity` | 生成包含一致预期、基本面和价格表现的股票研究快照 |
| `/analyze-swap-curve` | 结合国债和通胀覆盖层分析掉期曲线，挖掘曲线交易思路 |
| `/analyze-option-vol` | 结合波动率曲面、Greeks 以及隐含波动率和已实现波动率对比分析期权波动率 |
| `/review-fi-portfolio` | 结合定价、现金流和情景分析复核固定收益组合 |
| `/macro-rates` | 使用经济指标、收益率曲线和掉期利差构建宏观与利率仪表板 |
| `/analyze-bond-basis` | 结合 CTD 识别和隐含回购利率分析债券期货基差 |

## Skills

每条命令都由对应 skill 提供深度领域知识支持：

| Skill | 领域知识 |
|-------|-----------------|
| `bond-relative-value` | 利差框架、G-spread/Z-spread/OAS、贵贱分析 |
| `fx-carry-trade` | 套息机制、carry-to-vol 比率、G10 与新兴市场套息动态 |
| `equity-research` | IBES 一致预期解读、基本面分析、估值指标 |
| `swap-curve-strategy` | 掉期曲线构建、曲线交易、实际利率分析 |
| `option-vol-analysis` | 波动率曲面解读、SABR 模型、Greeks、隐含波动率与已实现波动率 |
| `fixed-income-portfolio` | 组合分析、关键利率久期、现金流分析、情景测试 |
| `macro-rates-monitor` | 宏观指标、收益率曲线形态、实际利率、金融条件 |
| `bond-futures-basis` | CTD 机制、基差计算、隐含回购、交割期权 |

## 集成

这个插件连接到 **LFA MCP Server**，该服务提供对以下领域的 LSEG 金融数据与分析能力访问：

- **Bond Pricing**，债券和债券期货估值
- **FX Pricing**，即期和远期汇率
- **Curves**，利率、信用、通胀和外汇远期曲线
- **Swaps**，利率掉期定价
- **Options**，带完整 Greeks 的期权估值
- **Volatility**，外汇和股票隐含波动率曲面
- **Quantitative Analytics**，分析师预期、公司基本面、股票价格、宏观数据
- **Time Series**，历史定价汇总
- **YieldBook**，固定收益参考数据、现金流、情景与风险分析

完整工具参考见 [CONNECTORS.md](CONNECTORS.md)。

## 安装

```
claude plugins add LSEG
```

## 要求

- 具备可用凭证并可访问 LSEG MCP Server
- 拥有相关产品的数据授权
