---
description: 使用品牌化 PPT 模板创建单页公司 strip profile
argument-hint: "[company name or ticker]"
---

# 单页 Strip Profile Command

为 pitch book 和交易材料创建专业的单页公司 strip profile。

## 工作流

### 第 1 步：收集公司信息

如果提供了公司名称或股票代码，就直接使用。否则请询问：
- "What company would you like to profile?"

### 第 2 步：检查可用的 PPT 模板技能

**首先，检查 skills 目录中是否已有 ppt-template skills**：

```bash
ls skills/ | grep -E "ppt-template|brand-guidelines"
```

如果存在模板 skill，例如 `techcorp-ppt-template`、`gs-brand-guidelines`：
1. 向用户列出可用模板
2. 询问要使用哪个模板，或者是否希望采用简洁专业格式
3. 使用 `skill: "[template-name]"` 加载所选模板 skill

如果没有模板 skill，请询问：
- "Do you have a branded PowerPoint template file to use? If so, provide the path. Otherwise I'll use a clean professional format."

如果提供了模板文件：
1. 分析模板结构，理解版式布局
2. 为单页内容使用合适的版式

### 第 3 步：加载 Strip Profile 技能

使用 `skill: "strip-profile"` 执行 profile 创建：

1. **明确需求**：
   - 确认采用单页格式
   - 询问是否有需要重点强调的领域

2. **研究公司数据**：
   - 公司概况，HQ、成立时间、员工数、管理层
   - 业务描述与市场定位
   - 关键财务数据，Revenue、EBITDA、利润率、增长
   - 估值指标，Market Cap、EV、multiples
   - 最新动态与新闻
   - 前几大股东，适用于上市公司

3. **创建 strip profile**：
   - 使用 4:3 比例，10" x 7.5"
   - 4 象限布局：
     - 左上：Company Overview，项目符号
     - 右上：Business & Positioning，项目符号
     - 左下：Key Financials，表格
     - 右下：股价图 + Shareholders，或 Recent News
   - 应用公司品牌色
   - 在分节标题中加入强调色条

### 第 4 步：视觉审阅

创建完幻灯片后：
1. 转为图片进行审阅
2. 检查是否有文字重叠或被截断
3. 确认所有数据都已填充，没有占位符
4. 向用户展示预览以供确认

### 第 5 步：交付输出

提供：
1. **PowerPoint file**，`.pptx`，即单页文件
2. **Image preview**，便于快速审阅
3. 所含关键数据点的**摘要**

## One-Pager Layout Reference

```
┌─────────────────────────────────────────────────────────────────┐
│ Company Name (TICKER)                                    [Logo] │
├────────────────────────────┬────────────────────────────────────┤
│ COMPANY OVERVIEW           │ BUSINESS & POSITIONING             │
│ • HQ, Founded, Employees   │ • Core business description        │
│ • CEO, CFO                 │ • Key products/services            │
│ • Market cap, industry     │ • Competitive positioning          │
│ • Key stats                │ • Growth drivers                   │
├────────────────────────────┼────────────────────────────────────┤
│ KEY FINANCIALS             │ STOCK PERFORMANCE / OWNERSHIP      │
│ ┌──────────────────────┐   │ [1Y Stock Chart]                   │
│ │ Metric │ FY24 │ FY25E│   │                                    │
│ │ Rev    │ $XXB │ $XXB │   │ Top Shareholders:                  │
│ │ EBITDA │ $XXB │ $XXB │   │ • Vanguard: X.X%                   │
│ │ Margin │ XX%  │ XX%  │   │ • BlackRock: X.X%                  │
│ │ EV/EBITDA │ XXx │ XXx │   │ • State Street: X.X%              │
│ └──────────────────────┘   │                                    │
└────────────────────────────┴────────────────────────────────────┘
Source: Company filings, FactSet
```

## Quality Checklist

交付前：
- [ ] 所有 4 个象限都填充了真实数据
- [ ] 没有残留占位文字
- [ ] 已应用公司品牌色
- [ ] 所有分节标题均有强调色条
- [ ] 财务表格格式正确
- [ ] 底部已标注来源
- [ ] 没有文字溢出或被截断
- [ ] 达到投资银行质量标准，GS/MS/JPM standard
