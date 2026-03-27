---
name: fsi-strip-profile
description: |
  为 pitch book、交易材料和客户演示创建专业的投资银行 strip profile，公司简介。生成 1 到 4 页高信息密度幻灯片，包含象限布局、图表和表格。
---

## Workflow

### 1. 明确需求
- **Ask the user**: 是单页，还是多页，3 到 4 页？
- **Ask the user**: 是否有需要重点强调的领域或主题？
- **Only after user confirms**，再进入研究阶段

### 2. 研究与规划
**Data Sources:**
- **Primary**: 公司申报文件，BamSEC、SEC EDGAR，"Item 1. Business"、MD&A，投资者演示、公司官网
- **Market data**: Bloomberg、FactSet、CapIQ，价格、股数、market cap、net debt、EV、ownership
- **Estimates**: FactSet/CapIQ 一致预期中的 NTM revenue、EBITDA、EPS
- **News**: 过去 90 天的新闻稿、M&A 活动、业绩指引变更

**Required Metrics:**
- **Financials**: Revenue、EBITDA、margins，% 、EPS、FCF，覆盖 ±3 年
- **Valuation**: Market Cap、EV、EV/Revenue、EV/EBITDA、P/E multiples
- **Growth**: YoY growth rates，%
- **Ownership**: 前 5 大股东及持股比例
- **Segments**: 产品结构和 / 或地理结构，占比拆分

**Normalization:**
- 所有金额统一为同一种货币
- 缩放标准一致，全文统一使用 $mm 或 $bn，不要混用

**Before Building:**
- 在对话中输出提纲，每个项目 4 到 5 条 bullet，使用真实数字，不留占位符
- 输出风格选择，字体、颜色，hex codes，以及每组数据使用的图表类型
- 获取用户确认："Does this outline and visual strategy align with your vision?"

### 3. 按页创建
**CRITICAL: You MUST create ONE slide at a time and get user approval before proceeding to the next slide.**

**For EACH slide:**
1. 仅用 PptxGenJS 创建这一页
2. **MANDATORY: Convert to image for review** - You MUST convert slides to images so you can visually verify them:
   ```bash
   soffice --headless --convert-to pdf presentation.pptx
   pdftoppm -jpeg -r 150 -f 1 -l 1 presentation.pdf slide
   ```
3. **MANDATORY VISUAL REVIEW**: You MUST carefully examine the rendered slide image before proceeding:
   - **Text overlap check**: 逐项检查所有文本元素，标签、bullet、标题是否互相碰撞？
   - **Text cutoff check**: 是否有任何文本在边界处被截断？所有单词是否完整可见？
   - **Chart boundary check**: 图表是否都在容器内？所有坐标轴标签是否完整可见？
   - **Quadrant integrity**: 某一象限中的内容是否溢出到相邻象限？
4. **If ANY overlap or cutoff is detected**: 按以下顺序立即修复：
   - **First**: 减小字号，下调 1 到 2pt
   - **Second**: 缩短文本，缩写或移除次要信息
   - **Third**: 调整元素位置或容器尺寸
   - **Re-render and verify again**，在所有文本完全适配前不得继续
5. 向用户展示幻灯片图片和下载链接
6. **STOP and wait for explicit user approval**，在用户明确确认前不要继续下一页

**YOU MUST CHECK FOR THESE SPECIFIC ISSUES ON EVERY PAGE:**
- 表格行与下方文字碰撞
- 图表 x 轴标签在底部被截断
- 过长 bullet 换行后进入相邻内容区
- 象限内容溢出到相邻象限
- 标题与下方内容重叠
- 图例文字与图表元素重叠
- 页脚 / 来源文字与正文内容碰撞

---

## Slide Format Requirements

### 信息密度至关重要

**首要目标是最大化信息密度。** 忙碌的高管应能在 30 秒内理解完整公司故事。尽量填满每个象限。

**每个象限的目标：**
- **Company Overview**: 至少 6 到 8 个 bullets，HQ、成立时间、员工、CEO/CFO、market cap、ticker、行业、关键数据
- **Business & Positioning**: 6 到 8 个 bullets，收入驱动、产品、市场份额、竞争壁垒、客户数、地理构成
- **Key Financials**: 8 到 10 行表格，或图表 + 4 到 5 个关键指标，Revenue、EBITDA、margins、EPS、FCF、growth rates、valuation multiples
- **第四象限**: 5 到 7 个 bullets，ownership、recent M&A、developments、catalysts

**提高信息密度的方法：**
- 合并相关事实："HQ: Austin, TX; Founded: 2003; 140K employees"
- 始终加入数字：写 "$50B revenue"，不要写 "large revenue"
- 加入上下文："EBITDA margin: 25% (vs. 18% industry avg)"
- 写清 YoY 变化："Revenue: $125M (+28% YoY)"
- 使用百分比："Enterprise: 62% of revenue"

**如果某个象限显得稀疏，就继续补充：**
- 分部拆分及占比
- 地域收入拆分
- 客户集中度，top 10 = X%
- 近期合同中标及金额
- Guidance 与 consensus 对比
- Insider ownership

**Line spacing - use single textbox per section:**
```python
def add_section(slide, x, y, w, header_text, bullets, header_size=10, bullet_size=8):
    """Header + bullets in single textbox with natural spacing"""
    tb = slide.shapes.add_textbox(x, y, w, Inches(len(bullets) * 0.18 + 0.3))
    tf = tb.text_frame
    tf.word_wrap = True

    # Header paragraph
    p = tf.paragraphs[0]
    p.text = header_text
    p.font.bold = True
    p.font.size = Pt(header_size)
    p.font.color.rgb = RGBColor(0, 51, 102)
    p.space_after = Pt(6)  # Small gap after header

    # Bullet paragraphs
    for bullet in bullets:
        p = tf.add_paragraph()
        p.text = bullet
        p.font.size = Pt(bullet_size)
        p.space_after = Pt(3)
    return tb
```

**Key spacing principles:**
- 标题和 bullets 放在同一个 textbox 中，不要拆分成两个
- 标题后使用 `space_after = Pt(6)`，bullet 之间使用 `Pt(3)`
- 不要硬编码空隙，让段落间距自然处理
- 如果内容溢出，先降 1pt 字号，而不是先删内容

---

- **3-4 dense slides**，使用象限、列、表格、图表
- **Bullets for ALL body text**，不要写段落。**每个 section 只用一个 textbox 放下全部 bullets**，不要为每一条 bullet 单独建 textbox。使用 PptxGenJS bullet formatting：
  ```javascript
  // CORRECT: Single textbox with bullet list - each array item becomes a bullet
  // Position in top-left quadrant (Company Overview) - after header with accent bar
  slide.addText(
    [
      { text: 'Headquarters: Austin, Texas; Founded 2003', options: { bullet: { indent: 10 }, breakLine: true } },
      { text: 'Employees: 140,000+ globally across 6 continents', options: { bullet: { indent: 10 }, breakLine: true } },
      { text: 'CEO: Elon Musk; CFO: Vaibhav Taneja', options: { bullet: { indent: 10 }, breakLine: true } },
      { text: 'Market Cap: $850B (#6 globally by market cap)', options: { bullet: { indent: 10 }, breakLine: true } },
      { text: 'Segments: Automotive (85%), Energy (10%), Services (5%)', options: { bullet: { indent: 10 } } }
    ],
    { x: 0.45, y: 0.95, w: 4.5, h: 2.6, fontSize: 11, fontFace: 'Arial', valign: 'top', paraSpaceAfter: 6 }
  );

  // WRONG: Multiple separate textboxes for each bullet - causes alignment issues
  // slide.addText('Headquarters: Austin', { x: 0.5, y: 1.0, bullet: true });
  ```

  **Bullet formatting tips:**
  - `bullet: { indent: 10 }`，控制 bullet 缩进，数值越小越紧凑
  - `paraSpaceAfter: 6`，每段之后的间距，单位 point
  - 每条 bullet 尽量塞入多个相关事实，例如 "HQ: Austin; Founded: 2003"
  - 用具体数字和百分比提高信息密度
- 标题使用 **Title case**，不要用 ALL CAPS，并左对齐
- **Consistent fonts**，包括表格在内的所有元素都要统一
- **Company's brand colors**，你必须先通过 web search 研究真实品牌色，不能猜测或自行假设
- **Follow brand guidelines if provided**

### Visual Reference
参考 `examples/Nike_Strip_Profile_Example.pptx` 获取布局灵感。颜色需根据每家公司品牌进行调整。

---

## First Page Layout

必须通过忙碌高管的 "30-second comprehension test"。

### Slide Setup (CRITICAL)
**Use 4:3 aspect ratio**，标准投行 pitch book 格式：
```javascript
const pptx = new pptxgen();
pptx.layout = 'LAYOUT_4x3';  // 10" wide × 7.5" tall - MUST USE THIS
```

### Slide Coordinate System
PptxGenJS 使用英寸。4:3 幻灯片尺寸为 **10" wide × 7.5" tall**。
- **x**: 距左边缘的水平位置，0 到 10
- **y**: 距顶部的垂直位置，0 到 7.5
- **Content must stay within bounds**，四周保留 0.3" 边距

### First Page Positioning (in inches)
```
┌─────────────────────────────────────────────────────────────────┐
│ y=0.2  Title: Company Name (Ticker)                             │
├────────────────────────────┬────────────────────────────────────┤
│ y=0.6  Company Overview    │ y=0.6  Business & Positioning      │
│ x=0.3, w=4.7               │ x=5.0, w=4.7                       │
│ h=3.0                      │ h=3.0                              │
├────────────────────────────┼────────────────────────────────────┤
│ y=3.7  Key Financials      │ y=3.7  Stock/Recent Developments   │
│ x=0.3, w=4.7               │ x=5.0, w=4.7                       │
│ h=3.5                      │ h=3.5                              │
└────────────────────────────┴────────────────────────────────────┘
                                                            y=7.5
```

### Title Section (y=0.2)
**Company Name (Ticker)**，示例：`Tesla, Inc. (TSLA)`
```javascript
slide.addText('Tesla, Inc. (TSLA)', { x: 0.3, y: 0.2, w: 9.4, h: 0.35, fontSize: 18, bold: true });
```

### 4-Quadrant Layout (y=0.6 to y=7.2)

| Quadrant | Position | Content |
|----------|----------|---------|
| **1** | x=0.3, y=0.6, w=4.7, h=3.0 | **Company Overview**：HQ、成立时间、关键数据、业务摘要，4 到 5 条 bullets |
| **2** | x=5.0, y=0.6, w=4.7, h=3.0 | **Business & Positioning**：收入驱动、产品 / 服务、竞争地位、增长驱动，4 到 5 条 bullets |
| **3** | x=0.3, y=3.7, w=4.7, h=3.5 | **Key Financials**：Revenue、EBITDA、margins、EPS、FCF + Valuation，Mkt Cap、EV、multiples，**table OR chart, not both** |
| **4** | x=5.0, y=3.7, w=4.7, h=3.5 | **上市公司**：1Y 股价图 + top shareholders。**私有公司**：Recent developments 或 Ownership/M&A history |

### Font Sizes - USE THESE EXACT VALUES
| Element | Size | Notes |
|---------|------|-------|
| Slide title | 24pt | Bold, company brand color |
| Quadrant headers | 14pt | Bold, with accent bar |
| Body/bullet text | 11pt | Regular weight |
| Table text | 10pt | Dense tables 可用 9pt |
| Chart labels | 9pt | 标签尽量简短 |
| Source/footer | 8pt | 底部 |

**CRITICAL: If text overflows, REDUCE font size by 1pt and re-render.**

### Visual Accents (REQUIRED)
每个象限标题左侧都必须有颜色强调条：
```javascript
// Add accent bar for quadrant header
slide.addShape(pptx.shapes.RECTANGLE, {
  x: 0.3, y: 0.6, w: 0.08, h: 0.25,
  fill: { color: 'E31937' }  // Use company brand color
});
slide.addText('Company Overview', {
  x: 0.45, y: 0.6, w: 4.5, h: 0.3, fontSize: 14, bold: true, fontFace: 'Arial'
});
```

**Visual elements to include:**
- 所有分节标题旁都要有强调色条，使用品牌色
- 上下象限之间加入细水平分隔线
- 如果有公司 logo，将其放在右上角
- 表格使用浅灰色 `#CCCCCC` 的细网格线

### First Page Formatting
- **Font: Arial**，除非用户或品牌指南另有要求
- **Quadrant titles** 使用 Title Case，不要 ALL CAPS，例如 "Company Overview"
- **Bullets**：在开头加粗关键术语，例如 "**Market Position:** Leading global manufacturer..."
- 仅使用白底，不加色块、填充或阴影
- 分节标题用粗体，并遵循品牌指南样式
- 所有象限大小与对齐一致

---

## Subsequent Pages: Free-Form Layouts

- 可使用 40/60 或 50/50 的双栏、整页图表，或侧边栏布局
- 每页都是对首页内容的展开
- 保持一致的字体排版和配色体系
- 建议顺序：Products/Market → Financial Analysis → Leadership

---

## Charts (Multi-Slide Profiles)

**For multi-slide profiles**：加入 2 到 3 个真实的 PptxGenJS 图表。不要用 placeholder div 或静态图片。

**For single-slide profiles**：财务部分优先用表格，更省空间。只有在图表替代表格时才加入图表，不要两者同时出现。

| Data Type | Chart Type |
|-----------|------------|
| Revenue trends | Line or column, multi-year |
| Geographic breakdown | Horizontal bar |
| Product mix | Pie with percentages |
| Financial comparison | Column |
| Stock price, 1Y daily | Line |

### Chart Code Examples

**Horizontal Bar (fits in bottom-right quadrant for 4:3 slide):**
```javascript
slide.addChart(pptx.charts.BAR, [{
  name: 'FY2024 Revenue by Region',
  labels: ['North America', 'EMEA', 'China', 'APLA'],
  values: [21.4, 13.6, 7.6, 6.7]
}], {
  x: 5.0, y: 4.1, w: 4.5, h: 3.0,  // Fits in bottom-right quadrant (4:3)
  barDir: 'bar', chartColors: ['FF6B35'], showValue: true,
  dataLabelFontSize: 10, catAxisLabelFontSize: 10, valAxisLabelFontSize: 10,
  dataLabelFormatCode: '$#,##0.0B',
  title: 'Revenue by Geography', titleFontSize: 12, titleBold: true
});
```

**Pie Chart (fits in bottom-right quadrant for 4:3 slide):**
```javascript
slide.addChart(pptx.charts.PIE, [{
  name: 'Product Mix',
  labels: ['Footwear', 'Apparel', 'Equipment'],
  values: [68, 29, 3]
}], {
  x: 5.0, y: 4.1, w: 4.5, h: 3.0,  // Fits in bottom-right quadrant (4:3)
  showPercent: true, showLegend: true, legendPos: 'r',
  dataLabelFontSize: 10, legendFontSize: 10,
  chartColors: ['FF6B35', '2C2C2C', '4A4A4A'],
  title: 'Revenue Mix FY24', titleFontSize: 12, titleBold: true
});
```

**Line Chart (full width for subsequent slides):**
```javascript
slide.addChart(pptx.charts.LINE, [{
  name: 'Revenue ($B)',
  labels: ['FY21', 'FY22', 'FY23', 'FY24', 'FY25E'],
  values: [44.5, 46.7, 48.5, 51.4, 54.2]
}], {
  x: 0.3, y: 1.2, w: 9.4, h: 5.5,  // Full width for 4:3 slide
  chartColors: ['FF6B35'], showValue: true, lineSmooth: true,
  dataLabelFontSize: 11, catAxisLabelFontSize: 11, valAxisLabelFontSize: 11,
  title: 'Revenue Trend & Forecast', titleFontSize: 14, titleBold: true
});
```

---

## Financial Data Formatting

**Always use native PptxGenJS tables or charts, NEVER plain text prose or HTML tables.**

使用 `slide.addTable()` 处理财务数据，适合 4:3 幻灯片左下象限：
```javascript
// Add header with accent bar first
slide.addShape(pptx.shapes.RECTANGLE, {
  x: 0.3, y: 3.7, w: 0.08, h: 0.25, fill: { color: 'E31937' }
});
slide.addText('Key Financials & Valuation', {
  x: 0.45, y: 3.7, w: 4.5, h: 0.3, fontSize: 14, bold: true, fontFace: 'Arial'
});

// Financial data table
slide.addTable([
  [{ text: 'Metric', options: { bold: true, fill: '003366', color: 'FFFFFF' } },
   { text: 'FY24', options: { bold: true, fill: '003366', color: 'FFFFFF' } },
   { text: 'FY25E', options: { bold: true, fill: '003366', color: 'FFFFFF' } }],
  ['Revenue', '$51.4B', '$54.2B'],
  ['YoY Growth', '+6.0%', '+5.5%'],
  ['EBITDA', '$8.9B', '$9.5B'],
  ['EBITDA Margin', '17.3%', '17.5%'],
  ['EPS', '$3.42', '$3.75'],
  ['Market Cap', '$185B', '—'],
  ['EV/EBITDA', '12.5x', '11.7x']
], {
  x: 0.45, y: 4.1, w: 4.3, h: 3.0,  // Below header in bottom-left quadrant
  fontFace: 'Arial', fontSize: 10,
  border: { pt: 0.5, color: 'CCCCCC' },
  valign: 'middle',
  colW: [1.8, 1.25, 1.25]  // Column widths
});
```

❌ **Incorrect:** 使用纯文本，如 `Note: FY2024 revenue growth +1.0%, Net Income $5.1B...`
❌ **Incorrect:** 使用无法正确转入 PowerPoint 的 HTML tables

对于 projections，用结构化表格展示 Bear/Base/Bull 场景。

---

## Quality Checklist

### First Page
- [ ] 标题区包含公司名、ticker、industry
- [ ] 标题下方严格为 4 个等大象限
- [ ] 正文全部为 bullets，不写段落，每条最多 1 行
- [ ] 财务内容使用表格或图表，不要同时使用两者

### All Slides
- [ ] 没有文字溢出或截断
- [ ] 全文保持一致的字体和颜色
- [ ] 图表渲染正确
- [ ] 没有 placeholder text，全部使用真实数据
- [ ] 单位缩放一致，统一使用 $mm 或 $bn，不混用
- [ ] 已标注来源
- [ ] 达到投资银行质量标准，GS/MS/JPM standard

**Note:** 创建 PowerPoint 文件时请参考 **PPTX skill**。
