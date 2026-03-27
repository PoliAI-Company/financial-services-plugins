# 税损收割

description: 在 taxable 账户中识别 tax-loss harvesting 机会。找出存在未实现亏损的持仓，建议替代证券，并跟踪 wash sale 窗口。触发词包括 "tax-loss harvesting"、"TLH"、"harvest losses"、"tax losses"、"unrealized losses" 或 "year-end tax planning"。

## Workflow

### Step 1: 识别候选项

扫描 taxable 账户中存在未实现亏损的持仓：

| Security | Asset Class | Cost Basis | Current Value | Unrealized Loss | Holding Period | % Loss |
|----------|-----------|-----------|---------------|-----------------|---------------|--------|
| | | | | | ST / LT | |

**优先级规则：**
1. 绝对亏损金额最大，税务收益最大
2. 优先短期亏损，可抵消按普通所得税税率征税的短期收益
3. 跌幅百分比最大的持仓，短期内反弹概率可能更低

### Step 2: 盈亏预算

计算客户当前税务情况：

| Category | Amount |
|----------|--------|
| Realized short-term gains YTD | |
| Realized long-term gains YTD | |
| Realized losses YTD | |
| Net gain/(loss) position | |
| Carryforward losses from prior years | |
| **Target harvesting amount** | |

**税务节省估算：**
- 短期亏损 × 边际普通所得税率
- 长期亏损 × 资本利得税率
- 最多可用 $3,000 净亏损抵扣普通收入
- 超出部分结转以后年度

### Step 3: 替代证券

对每个可收割候选，建议一个替代品，要求：
- 保持相近市场暴露，同一资产类别、行业、地域
- 不是 "substantially identical"，避免触发 wash sale
- 风险 / 回报特征相近

| Sell | Replace With | Reason | Tracking Error Risk |
|------|-------------|--------|-------------------|
| SPDR S&P 500 (SPY) | iShares Core S&P 500 (IVV) | 同类指数暴露，不同基金公司 | Minimal |
| Vanguard Total Intl (VXUS) | iShares MSCI ACWI ex-US (ACWX) | 暴露相近，指数不同 | Low |
| Individual stock ABC | Sector ETF (XLK) | 更广泛暴露，无 wash sale 风险 | Moderate |

### Step 4: Wash Sale 检查

执行前，确认不存在 wash sale：

- 检查家庭层面所有账户，taxable、IRA、Roth、配偶账户
- 向前看 30 天，过去 30 天是否买入了实质相同证券
- 向后看 30 天，未来 30 天内禁止回补同一证券
- 检查 dividend reinvestment plans，DRIPs，它们也可能触发 wash sale
- 为每笔交易记录 wash sale 窗口

| Security Sold | Wash Sale Window Start | Window End | DRIP Active? | Risk |
|--------------|----------------------|-----------|-------------|------|
| | | | | |

### Step 5: 执行计划

| Trade # | Account | Action | Security | Shares | Est. Proceeds | Est. Loss | Replacement | Notes |
|---------|---------|--------|----------|--------|--------------|-----------|-------------|-------|
| | | Sell | | | | | | |
| | | Buy | | | | | | |

**Summary：**
- 预计收割总亏损：$
- 预计节税：$，按边际税率 % 估算
- 对组合的净影响很小，替代证券维持原有市场暴露
- Wash sale window 管理：[dates]

### Step 6: 收割后跟踪

30+ 天后，可选：
- 换回原始证券，如有需要
- 持续持有替代证券，如无必要换回
- 更新成本基础记录
- 为税务申报留存记录

### Step 7: 输出

- 收割机会清单，Excel
- 交易执行表
- Wash sale 跟踪日历
- 税务节省估算摘要
- 替代证券选择理由

## Important Notes

- Wash sale 规则很严格，违规会导致亏损不得抵扣，并且要调整成本基础
- Substantially identical 指的是同一证券，不是同一资产类别，跟踪不同指数的 ETF 通常问题不大
- 始终在家庭所有账户层面统筹，包括退休账户
- 也要考虑长期成本基础被下调的代价，收割会重置成本基础，未来可能产生更多收益税
- 年底是收割高峰，但全年都可能出现机会
- 12 月 mutual fund capital gains distributions 可能会提高收割紧迫度
- 为税务申报和合规完整记录所有动作
- 不是所有亏损都值得收割，交易成本和 tracking error 都是真实成本
