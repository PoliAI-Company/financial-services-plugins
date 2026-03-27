# Thesis Tracker

description: 维护并更新组合持仓和观察名单的投资论点。随着时间跟踪关键数据点、催化剂和论点里程碑。适用于用新信息更新论点、复盘持仓逻辑，或检查论点是否仍然成立。在用户提到 "update thesis for [company]"、"is my thesis still intact"、"thesis check"、"add data point to [company]" 或 "review my positions" 时触发。

## 工作流

### 第 1 步：定义或载入论点

如果是在创建新论点：
- **Company**：公司名称和 ticker
- **Position**：Long 或 Short
- **Thesis statement**：1-2 句话的核心论点，例如 "Long ACME，随着业务结构向软件迁移，定价权与经营杠杆将推动利润率扩张"
- **Key pillars**：3-5 个支撑论据
- **Key risks**：3-5 个会使论点失效的风险
- **Catalysts**：即将到来的、可验证或证伪该论点的事件，例如业绩、产品发布、监管决定
- **Target price / valuation**：若论点兑现，这只股票值多少钱
- **Stop-loss trigger**：什么情况会让你退出

如果是更新已有论点，询问用户新的数据点或进展。

### 第 2 步：更新日志

对每一个新的数据点或进展，记录：

- **Date**：事件发生时间
- **Data point**：发生了什么变化，业绩超预期、管理层离职、竞争对手动作等
- **Thesis impact**：这会强化、削弱还是中性影响某一论点支柱？
- **Action**：No change / Increase position / Trim / Exit
- **Updated conviction**：High / Medium / Low

### 第 3 步：论点评分卡

维护一份持续更新的评分卡：

| Pillar | Original Expectation | Current Status | Trend |
|--------|---------------------|----------------|-------|
| Revenue growth >20% | On track | Q3 was 22% | Stable |
| Margin expansion | Behind | Margins flat YoY | Concerning |
| New product launch | Pending | Delayed to Q2 | Watch |

### 第 4 步：催化剂日历

跟踪即将发生的催化剂：

| Date | Event | Expected Impact | Notes |
|------|-------|-----------------|-------|
| | | | |

### 第 5 步：输出

输出适用于以下场景的论点总结：
- 晨会讨论
- 组合复盘
- 风险委员会汇报

格式为简洁的 markdown 或 Word 文档，包含评分卡、近期更新和当前信心水平。

## 重要说明

- 一个论点必须是可证伪的，如果没有任何事情能否定它，那它就不是论点
- 对反面证据的跟踪应与支持性证据同样严格
- 即使没有重大变化，也至少按季度复盘一次论点
- 如果用户管理多个持仓，可以提出做一次完整的组合论点复盘
- 以结构化格式保存论点数据，便于跨会话引用
