# 投资组合再平衡

description: 分析投资组合配置偏移，并生成跨账户的再平衡交易建议。会考虑税务影响、交易成本和 wash sale 规则。触发词包括 "rebalance"、"portfolio drift"、"allocation check"、"rebalancing trades" 或 "my portfolio is out of balance"。

## Workflow

### Step 1: 当前状态

对每个账户记录：
- 账户类型，taxable、IRA、Roth、401k
- 持仓及当前市值
- 成本基础，针对 taxable 账户
- 各持仓未实现盈亏

### Step 2: 偏移分析

将当前配置与 IPS 目标对比：

| Asset Class | Target % | Current % | Drift | $ Over/Under |
|------------|----------|-----------|-------|-------------|
| US Large Cap Equity | | | | |
| US Small/Mid Cap | | | | |
| International Developed | | | | |
| Emerging Markets | | | | |
| Investment Grade Bonds | | | | |
| High Yield / Credit | | | | |
| TIPS / Inflation Protected | | | | |
| Alternatives | | | | |
| Cash | | | | |

标记超出再平衡带宽的资产，通常为 ±3-5%。

### Step 3: 交易建议

生成将配置拉回目标的交易：

**Tax-Aware Rebalancing Rules：**
- 优先在 tax-advantaged 账户中再平衡，IRA、Roth，因为没有税务后果
- 在 taxable 账户中，尽量避免卖出存在大量短期收益的持仓
- 如有可能，在再平衡时同步 harvest losses
- 注意所有账户之间的 wash sale 规则，30 天窗口
- 可以优先把新增资金投向低配资产，而不是直接交易

**Trade List：**

| Account | Action | Security | Shares/$ | Reason | Tax Impact |
|---------|--------|----------|----------|--------|-----------|
| | Buy/Sell | | | Rebalance / TLH | ST gain / LT gain / Loss |

### Step 4: 资产位置审查

优化不同资产放在哪类账户：
- **Tax-deferred (IRA/401k)**：债券、REITs、高换手基金，税拖累最大
- **Roth**：预期增长最高的资产，享受免税增长
- **Taxable**：税务效率高的股票资产，index funds、ETFs、munis，以及适合 tax-loss harvesting 的持仓

### Step 5: 执行

- 各账户的总交易量
- 预计交易成本
- 预计税务影响，已实现盈亏
- 对配置偏移的净改善效果

### Step 6: 输出

- 偏移分析表
- 建议交易清单，Excel
- 税务影响汇总
- 再平衡前后配置对比

## Important Notes

- 不要为了再平衡而再平衡，带宽内的小幅偏移通常没问题
- 对 taxable 账户来说，税务成本可能高于再平衡收益，要计算 breakeven
- 交易前应考虑待发生现金流，缴款、提款、RMDs
- 检查是否存在客户特定限制，ESG、集中持股、lockup
- 为每笔交易记录理由，便于合规留档
- Wash sale 规则跨账户生效，必须在整个家庭层面协同交易
