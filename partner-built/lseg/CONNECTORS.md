# 连接器

该插件连接到 **LFA MCP Server**，它提供来自 LSEG 的金融分析工具。所有工具都由一个 MCP 服务器统一提供，不需要额外连接器。

## 命令如何引用工具

这个插件中的命令使用工具的精确名称来引用 MCP 工具，例如 `bond_price`、`interest_rate_curve`。为方便理解，这些工具按类别组织如下：

## 工具分类

| 类别 | 占位符 | 工具 | 说明 |
|------|--------|------|------|
| 债券定价 | `~~bond-pricing` | `bond_price`, `bond_future_price` | 为债券和债券期货定价，并返回完整分析指标 |
| 外汇定价 | `~~fx-pricing` | `fx_spot_price`, `fx_forward_price` | 外汇即期和远期定价 |
| 利率曲线 | `~~ir-curves` | `interest_rate_curve`, `inflation_curve` | 国债收益率曲线和通胀盈亏平衡曲线 |
| 信用曲线 | `~~credit-curves` | `credit_curve` | 按发行人类型划分的信用利差曲线 |
| 外汇曲线 | `~~fx-curves` | `fx_forward_curve` | 外汇远期点曲线 |
| 期权 | `~~options` | `option_value`, `option_template_list` | 带 Greeks 的期权估值 |
| 掉期 | `~~swaps` | `ir_swap` | 利率掉期定价 |
| 波动率曲面 | `~~volatility` | `fx_vol_surface`, `equity_vol_surface` | 外汇和股票隐含波动率曲面 |
| 量化分析 | `~~qa` | `qa_ibes_consensus`, `qa_company_fundamentals`, `qa_historical_equity_price`, `qa_macroeconomic` | 分析师预期、基本面、价格和宏观数据 |
| 时间序列 | `~~time-series` | `tscc_historical_pricing_summaries` | 历史定价汇总，支持日内和跨日 |
| 固定收益分析 | `~~yieldbook` | `yieldbook_bond_reference`, `yieldbook_cashflow`, `yieldbook_scenario`, `fixed_income_risk_analytics` | 债券参考数据、现金流、情景分析、OAS/久期 |

## 完整工具参考

### Bond Domain
- **`bond_price`**，计算债券价格、估值与分析指标。支持 ISIN、RIC、CUSIP 或 AssetId。返回收益率、久期、凸性、DV01、应计利息。支持通过价格或收益率覆盖进行 what-if 情景分析。
- **`bond_future_price`**，计算债券期货价格和分析指标。返回公允价值、最便宜可交割券识别结果、交割篮子、转换因子和合约 DV01。

### FX Domain
- **`fx_spot_price`**，针对 ISO 货币对的外汇即期定价。返回中间价、买价和卖价。
- **`fx_forward_price`**，按特定期限或日期进行外汇远期定价。返回远期点、远期汇率和 carry。

### Curves Domain
- **`interest_rate_curve`**，国债收益率曲线。两阶段流程，先列出可用曲线，再计算曲线点。返回平价利率、零息利率、贴现因子和远期利率。
- **`credit_curve`**，信用利差曲线。可按国家和发行人类型搜索，例如 Corporate、Sovereign、Agency 等，然后计算利差期限结构。
- **`inflation_curve`**，通胀盈亏平衡曲线。可按国家或货币搜索，然后计算盈亏平衡通胀率和实际收益率。
- **`fx_forward_curve`**，外汇远期点曲线。先列出曲线，再计算标准期限上的远期点。

### Swaps Domain
- **`ir_swap`**，利率掉期定价。两阶段流程，先按货币或指数列模板，再按期限定价。返回平价利率、DV01 和 NPV。

### Options Domain
- **`option_value`**，期权估值，支持香草、障碍、二元和亚洲期权。返回权利金、完整 Greeks 和风险指标。
- **`option_template_list`**，列出可用于定价的期权模板。

### Volatility Domain
- **`fx_vol_surface`**，使用 SABR 模型生成外汇波动率曲面。返回各期限和 Delta 执行价上的波动率曲面。
- **`equity_vol_surface`**，股票隐含波动率曲面。支持通过 RIC 处理股票和指数，通过 RICROOT 处理期货。

### Quantitative Analytics Domain
- **`qa_ibes_consensus`**，IBES 分析师一致预期，覆盖 EPS、收入、EBITDA、DPS。提供前瞻预期、分析师数量、离散度及高低区间。
- **`qa_company_fundamentals`**，公司已披露财务数据，包括利润表和资产负债表指标。提供历史财政年度数据。
- **`qa_historical_equity_price`**，历史股票价格，带 OHLCV、总回报和 beta。
- **`qa_macroeconomic`**，宏观经济指标数据库。可按助记符或描述搜索，获取最新值或时间序列。

### Time Series Domain
- **`tscc_historical_pricing_summaries`**，任意 RIC 的历史定价汇总。支持跨日频率，比如日、周、月，也支持日内频率，比如 1 分钟到 1 小时。

### Fixed Income Analytics (YieldBook) Domain
- **`yieldbook_bond_reference`**，债券参考数据，包括证券类型、行业、评级、票息、到期日、发行人。
- **`yieldbook_cashflow`**，债券现金流预测，包括未来票息和本金支付安排。
- **`yieldbook_scenario`**，债券情景分析，输出平行利率冲击下的价格和收益率。
- **`fixed_income_risk_analytics`**，债券风险分析，包括 OAS、有效久期、关键利率久期和凸性。
