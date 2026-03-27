# 投后组合监控

description: 跟踪并分析组合公司相对于计划的表现。读取月度 / 季度财务包，Excel、PDF，提取 KPI，标记相对预算的偏差，并生成汇总仪表盘。适用于审阅组合公司财报、准备董事会材料，或监控 covenant 合规。触发词包括 "review portfolio company"、"monthly financials"、"how is [company] performing"、"covenant check" 或 "portfolio update"。

## Workflow

### Step 1: 读取财务包

- 接收用户提供的组合公司财务包，Excel 工作簿、PDF 或 CSV
- 提取关键财务指标：Revenue、EBITDA、现金余额、未偿债务、capex、营运资金
- 识别报告期间，并与上期及预算 / 计划进行比较

### Step 2: KPI 提取与偏差分析

需要跟踪的关键指标，可根据公司所在行业调整：

**财务 KPI：**
- Revenue vs. budget，金额和百分比
- EBITDA 和 EBITDA margin vs. budget
- 现金余额和净债务
- 杠杆率，Net Debt / LTM EBITDA
- 利息覆盖倍数
- Capex vs. budget
- 自由现金流

**运营 KPI**，向用户确认或从数据中推断：
- 客户数 / 单客户收入
- 员工人数 / 人均收入
- Backlog / pipeline
- Churn / retention rates

### Step 3: 标记并汇总

- **Green**：与计划差异在 5% 以内
- **Yellow**：低于计划 5-15%，需要讨论
- **Red**：低于计划超过 15%，或存在 covenant breach 风险，需要立刻关注

输出简洁摘要：
1. 一段执行摘要，"Company X is tracking [ahead/behind/on] plan..."
2. KPI 表，展示 actual、budget 和 prior period
3. 红 / 黄标事项及背景
4. Covenant compliance 状态，如适用
5. 给管理层的问题清单

### Step 4: 趋势分析

如果提供了多个期间：
- 绘制关键指标的时间趋势图，revenue、EBITDA、cash
- 识别趋势是在加速、放缓还是稳定
- 与 underwriting case 对比

## Important Notes

- 如果未提供预算 / 计划，始终先索取，用于做比较
- 不要主观假设行业特定 KPI，先问清楚这家公司真正看重什么
- 如果 covenant 水平未知，向用户索取信贷协议条款
- 输出应达到 board-ready 水准，简洁、客观、不啰嗦
