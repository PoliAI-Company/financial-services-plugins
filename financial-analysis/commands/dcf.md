---
description: 构建使用 comps 终值倍数校验的 DCF 估值模型
argument-hint: "[公司名称或股票代码]"
---

# DCF 估值命令

构建机构级质量的 DCF 模型，并使用可比公司分析为估值区间提供参考。

## 工作流

### 第 1 步：收集公司信息

如果提供了公司名称或股票代码，则直接使用。否则请询问：
- "What company would you like to value?"

### 第 2 步：执行可比公司分析

**首先加载 comps-analysis skill** 来构建交易 comps：

使用 `skill: "comps-analysis"` 来：
1. 识别 4 到 6 家可比上市公司
2. 拉取经营指标（Revenue、EBITDA、利润率、增长）
3. 拉取估值倍数（EV/Revenue、EV/EBITDA、P/E）
4. 计算统计汇总（中位数、25th/75th 分位）

**需要从 comps 中记录的关键输出：**
- 中位数 EV/EBITDA 倍数 → 用于终值退出倍数
- 中位数 EV/Revenue 倍数 → 用于对 DCF 输出做合理性校验
- 同行增长率 → 用于收入预测基准
- 同行利润率 → 用于利润率假设基准

### 第 3 步：构建 DCF 模型

**加载 dcf-model skill** 来搭建估值模型：

使用 `skill: "dcf-model"` 来：
1. 收集历史财务数据和市场数据
2. 构建收入预测（Bear/Base/Bull）
3. 建模经营费用和 FCF
4. 使用 CAPM 计算 WACC
5. 折现现金流并计算终值
6. 桥接到股权价值和隐含股价

**使用 comps 为 DCF 假设提供依据：**

| Comps 输出 | DCF 输入 |
|--------------|-----------|
| Peer median EV/EBITDA | Terminal exit multiple range |
| Peer 25th-75th EV/EBITDA | Sensitivity analysis range |
| Peer median growth rate | Benchmark for revenue assumptions |
| Peer median EBITDA margin | Target margin in terminal year |
| Peer median P/E | Cross-check implied P/E from DCF |

### 第 4 步：交叉校验估值

DCF 完成后，验证：
1. **DCF 隐含 EV/EBITDA** 与同行中位数相比
   - 如果 DCF 隐含 25x，而同行交易于 12x，需要调查原因
2. **DCF 隐含 P/E** 与同行中位数相比
3. **终值占 EV 的比例**（应为 50% 到 70%）
4. **估值中隐含的增长** 与同行增长率相比

### 第 5 步：交付输出

提供：
1. **Comps 分析表格**（.xlsx），含同行交易倍数
2. **DCF 模型**（.xlsx），包含：
   - Bear/Base/Bull 场景
   - 敏感性表（WACC 对 Terminal Growth 等）
   - 含隐含上涨或下跌空间的估值摘要
3. **摘要**，说明：
   - 关键估值驱动因素
   - comps 如何为分析提供依据
   - 需要关注的风险和敏感项

## 示例输出摘要

```
VALUATION SUMMARY: [Company] ([Ticker])

Comparable Companies Analysis:
- Peer Group: [List of 4-6 comps]
- Median EV/EBITDA: 12.5x (range: 10.2x - 15.8x)
- Median EV/Revenue: 3.2x (range: 2.1x - 4.5x)

DCF Valuation (Base Case):
- Implied Share Price: $XX.XX
- Current Price: $YY.YY
- Implied Upside: +XX%

Valuation Cross-Check:
- DCF Implied EV/EBITDA: 13.2x (vs peer median 12.5x)
- DCF Implied P/E: 22.4x (vs peer median 20.1x)
- Terminal Value: 62% of EV (within normal range)

Key Assumptions:
- Revenue CAGR: X% (vs peer median X%)
- Terminal EBITDA Margin: X% (vs peer median X%)
- WACC: X.X%
- Terminal Growth: X.X%
```
