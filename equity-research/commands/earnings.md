---
description: 分析季度业绩并创建业绩更新报告
argument-hint: "[company name or ticker] [quarter, e.g. Q3 2024]"
---

# Earnings Analysis Command

创建一份专业的股票研究业绩更新报告，用于分析季度业绩结果。

## 工作流

### 第 1 步：收集信息

解析输入内容，提取：
- 公司名称或 ticker
- 季度，例如 Q3 2024、Q2 FY25

如果未提供，则询问：
- "你想分析哪家公司的业绩？"
- "是哪个季度？例如 Q3 2024"

### 第 2 步：验证时效性

**CRITICAL**：在继续之前，确认你拿到的是最新数据：
1. 搜索 "[Company] latest earnings results [current year]"
2. 确认业绩发布时间在最近 3 个月内
3. 确认 transcript 日期与发布日期一致

如果数据已经陈旧，告知用户并继续搜索最新材料。

### 第 3 步：加载 Earnings Analysis Skill

使用 `skill: "earnings-analysis"` 创建报告：

1. **数据收集**，搜索最新材料：
   - Earnings release，新闻稿
   - SEC EDGAR 上的 10-Q filing
   - Earnings call transcript
   - Investor presentation / supplemental materials
   - Consensus estimates，Bloomberg/FactSet

2. **Beat/Miss Analysis**：
   - 收入相对一致预期，超预期或低于预期，$X 或 X%
   - EPS 相对一致预期，超预期或低于预期，$X 或 X%
   - 关键分部表现相对预期
   - 解释结果偏离预期的原因

3. **Key Metrics Analysis**：
   - 按分部 / 地区拆分收入
   - 利润率趋势，毛利、营业、净利
   - 指引，上调 / 维持 / 下调
   - 更新前瞻预测

4. **Generate Charts**（8-12 张）：
   - 季度收入进展
   - 季度 EPS 进展
   - 利润率趋势
   - 分部收入
   - Beat/miss 总结
   - 预测修订
   - 估值图表

5. **Create Report**（8-12 页）：
   - 第 1 页：摘要，包含评级和目标价
   - 第 2-3 页：详细结果分析
   - 第 4-5 页：关键指标与指引
   - 第 6-7 页：更新后的投资论点
   - 第 8-10 页：估值与预测
   - Sources section，带可点击超链接

### 第 4 步：交付输出

提供：
1. **DOCX 报告**，8-12 页的业绩更新
2. **摘要**，重点说明：
   - 关键指标的 beat/miss
   - 指引变化
   - 论点影响，正面 / 负面 / 中性

## 报告结构参考

```
PAGE 1: EARNINGS SUMMARY
┌─────────────────────────────────────────────────────────────────┐
│ [Company] Q3 2024 Earnings Update                               │
│ Rating: BUY | Price Target: $XXX (from $XXX)                    │
├─────────────────────────────────────────────────────────────────┤
│ KEY TAKEAWAYS                                                   │
│ • Revenue beat by X% on strong [segment] performance            │
│ • EPS beat by $X.XX driven by margin expansion                  │
│ • FY guidance raised to $X.XX-$X.XX (from $X.XX-$X.XX)         │
│ • Thesis intact; maintain BUY rating                            │
├─────────────────────────────────────────────────────────────────┤
│ RESULTS SNAPSHOT                                                │
│ ┌─────────────┬──────────┬──────────┬──────────┐               │
│ │ Metric      │ Actual   │ Consensus│ Beat/Miss│               │
│ │ Revenue     │ $X.XXB   │ $X.XXB   │ +X.X%    │               │
│ │ EPS         │ $X.XX    │ $X.XX    │ +$X.XX   │               │
│ │ Gross Margin│ XX.X%    │ XX.X%    │ +XXbps   │               │
│ └─────────────┴──────────┴──────────┴──────────┘               │
└─────────────────────────────────────────────────────────────────┘

PAGES 2-3: DETAILED RESULTS
- 按分部进行分析
- 地域拆分
- 解释 beat/miss 的核心驱动

PAGES 4-5: METRICS & GUIDANCE
- 利润率分析
- 全年指引对比
- 更新后的季度预测

PAGES 6-7: THESIS UPDATE
- 发生了什么变化
- 风险与催化剂
- 投资建议

PAGES 8-10: VALUATION
- 如果变化显著，则更新 DCF/comps
- 目标价的论证
- 情景分析

SOURCES SECTION (with clickable hyperlinks):
- Earnings Release: [hyperlink]
- Form 10-Q: [EDGAR hyperlink]
- Earnings Call Transcript: [hyperlink]
- Consensus estimates: Bloomberg as of [date]
```

## Quality Checklist

交付前确认：
- [ ] 业绩数据来自最新季度，而不是陈旧数据
- [ ] beat/miss 用具体数字量化
- [ ] 所有图表都已嵌入，总计 8-12 张
- [ ] Sources section 带可点击超链接
- [ ] 每个 figure/table 都有来源引用
- [ ] 指引变化已清晰记录
- [ ] 评级和目标价在开头明确给出
- [ ] 8-12 页，3,000-5,000 词
