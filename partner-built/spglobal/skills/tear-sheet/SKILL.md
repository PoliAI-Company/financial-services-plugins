---
name: tear-sheet
description: "通过 Kensho LLM-ready API MCP server 使用 S&P Capital IQ 数据生成专业公司 tear sheet。当用户要求 tear sheet、公司一页纸、公司画像、事实表、公司快照或公司概览文档时使用，尤其是提到具体公司名称或 ticker 时。用户要求 equity research 摘要、并购公司画像、企业发展收购标的画像、销售/BD 会前准备材料，或任何简明的单公司财务摘要时也应触发。此 skill 支持四类受众：equity research、investment banking/M&A、corporate development 和 sales/business development。如果用户没有指定受众，需要询问。既适用于上市公司，也适用于私有公司。"
---

# 金融 Tear Sheet 生成器

通过 S&P Global MCP 工具，也就是 Kensho LLM-ready API，从 S&P Capital IQ 拉取实时数据，并将其格式化为面向特定受众的专业公司 tear sheet Word 文档。

## 样式配置

以下为合理默认值。若要适配你们机构品牌，可修改本节，常见改动包括颜色方案、字体和免责声明文本。

**Colors：**
- Primary，也就是页眉横幅背景和章节标题文字：`#1F3864`
- Accent，也就是招牌章节高亮：`#2E75B6`
- Table header row fill：`#D6E4F0`
- Table alternating row fill：`#F2F2F2`
- Table borders：`#CCCCCC`
- Header banner text：`#FFFFFF`

**Typography，docx-js 中使用 half-points：**
- Font family：Arial
- Company name：18pt 粗体，size 36
- Section headers：11pt 粗体，size 22，Primary 色
- Body text：9pt，size 18
- Table text：8.5pt，size 17
- Footer/disclaimer：7pt 斜体，size 14
- 各模板专用覆盖项写在各 reference 文件的 Formatting Notes 中

**Company Header Banner：**
- 页眉是横跨整页宽度的深蓝色横幅，背景为 `#1F3864`，公司名称为白色。
- **横幅下方的键值对必须用双栏无边框表格铺满整页宽度。** 左栏放公司识别信息，右栏放财务识别信息。每个单元格中的每条字段都应使用粗体 label 加常规 weight value，且处于同一行。不要把所有字段都挤在左侧单列，这样既浪费横向空间，也不专业。
- 具体实现方式、列宽和字段分配，请按英文原文执行。

**Section Headers：**
- 每个章节标题下方都需要一条细横线，颜色 `#CCCCCC`，厚度 0.5pt，用于清晰分隔章节。
- **这条线应作为标题段落本身的 bottom border 实现。** 不要插入额外段落去画线，否则会造成多余留白。
- 具体 docx-js 实现保持与英文原文一致。

**Bullet Formatting：**
- 全部 tearsheet 统一使用单一 bullet 字符 `•`
- 综合或分析型 bullet，比如 Earnings Highlights、Strategic Fit、Integration Considerations、Conversation Starters，应使用缩进块样式
- 关系信息中的信息型 bullet 使用标准正文缩进
- **不要对 bullet 区块加左边框强调**，因为 docx-js 渲染不稳定

**Tables，仅用于金融数据：**
- 表头使用 `#D6E4F0`
- 主体行用白色和 `#F2F2F2` 交替
- 边框颜色 `#CCCCCC`
- 数字列右对齐
- 始终使用 `ShadingType.CLEAR`

**Layout：**
- US Letter 纵向页面，四边边距均为 0.75"

**Number formatting：**
- 货币默认 USD。若公司收入大于 $50B，使用 billions，并保留 1 位小数，否则使用 millions。单位写在列表头，不要写在单元格里。
- **表格单元格只写带逗号的纯数字，不带 `$` 符号。**
- 财年必须使用真实年度标签
- 负数使用括号
- 百分比保留 1 位小数

**Footer，是真正的文档页脚，不是正文内联文本：**
页脚必须在每页底部重复出现，居中，两行，7pt 斜体，颜色 `#666666`。文案在同一公司不同 tearsheet 之间必须保持一致，不得随受众变化。

## 组件函数

**必须使用这些精确函数来创建文档元素，不要自己手写 docx-js 样式代码。** 把这些函数复制到生成的 Node 脚本中并直接调用。下面的代码块保持原样：

```javascript
const docx = require("docx");
const {
  Document, Paragraph, TextRun, Table, TableRow, TableCell,
  WidthType, AlignmentType, BorderStyle, ShadingType,
  Header, Footer, PageNumber, HeadingLevel, TableLayoutType,
  convertInchesToTwip
} = docx;

// ── Color constants ──
const COLORS = {
  PRIMARY: "1F3864",
  ACCENT: "2E75B6",
  TABLE_HEADER_FILL: "D6E4F0",
  TABLE_ALT_ROW: "F2F2F2",
  TABLE_BORDER: "CCCCCC",
  HEADER_TEXT: "FFFFFF",
  FOOTER_TEXT: "666666",
};

const FONT = "Arial";

// ── 1. createHeaderBanner ──
// Returns an array of docx elements: [banner paragraph, key-value table]
function createHeaderBanner(companyName, leftFields, rightFields) {
  // leftFields / rightFields: arrays of { label: string, value: string }
  const banner = new Paragraph({
    children: [
      new TextRun({
        text: companyName,
        bold: true,
        size: 36, // 18pt
        color: COLORS.HEADER_TEXT,
        font: FONT,
      }),
    ],
    shading: { type: ShadingType.CLEAR, color: "auto", fill: COLORS.PRIMARY },
    spacing: { after: 0 },
    alignment: AlignmentType.LEFT,
  });

  function buildCellParagraphs(fields) {
    return fields.map(
      (f) =>
        new Paragraph({
          children: [
            new TextRun({ text: f.label + "  ", bold: true, size: 18, font: FONT }),
            new TextRun({ text: f.value, size: 18, font: FONT }),
          ],
          spacing: { after: 40 },
        })
    );
  }

  const noBorder = { style: BorderStyle.NONE, size: 0, color: "FFFFFF" };
  const noBorders = { top: noBorder, bottom: noBorder, left: noBorder, right: noBorder };
  const noShading = { type: ShadingType.CLEAR, color: "auto", fill: "FFFFFF" };

  const kvTable = new Table({
    rows: [
      new TableRow({
        children: [
          new TableCell({
            children: buildCellParagraphs(leftFields),
            width: { size: 50, type: WidthType.PERCENTAGE },
            borders: noBorders,
            shading: noShading,
          }),
          new TableCell({
            children: buildCellParagraphs(rightFields),
            width: { size: 50, type: WidthType.PERCENTAGE },
            borders: noBorders,
            shading: noShading,
          }),
        ],
      }),
    ],
    width: { size: 100, type: WidthType.PERCENTAGE },
  });

  return [banner, kvTable];
}

// ── 2. createSectionHeader ──
// Returns a single Paragraph with bottom border rule
function createSectionHeader(text) {
  return new Paragraph({
    children: [
      new TextRun({
        text: text,
        bold: true,
        size: 22, // 11pt
        color: COLORS.PRIMARY,
        font: FONT,
      }),
    ],
    spacing: { before: 240, after: 0 }, // 12pt before, 0pt after
    border: {
      bottom: { style: BorderStyle.SINGLE, size: 1, color: COLORS.TABLE_BORDER },
    },
  });
}

// ── 3. createTable ──
// headers: string[], rows: string[][], options: { accentHeader?, fontSize? }
function createTable(headers, rows, options = {}) {
  const fontSize = options.fontSize || 17; // 8.5pt default
  const headerFill = options.accentHeader ? COLORS.ACCENT : COLORS.TABLE_HEADER_FILL;
  const headerTextColor = options.accentHeader ? COLORS.HEADER_TEXT : "000000";

  const cellBorders = {
    top: { style: BorderStyle.SINGLE, size: 1, color: COLORS.TABLE_BORDER },
    bottom: { style: BorderStyle.SINGLE, size: 1, color: COLORS.TABLE_BORDER },
    left: { style: BorderStyle.SINGLE, size: 1, color: COLORS.TABLE_BORDER },
    right: { style: BorderStyle.SINGLE, size: 1, color: COLORS.TABLE_BORDER },
  };

  const cellMargins = { top: 40, bottom: 40, left: 80, right: 80 };

  function isNumeric(val) {
    if (typeof val !== "string") return false;
    const cleaned = val.replace(/[,$%()]/g, "").trim();
    return cleaned !== "" && !isNaN(cleaned);
  }

  // Header row
  const headerRow = new TableRow({
    children: headers.map(
      (h) =>
        new TableCell({
          children: [
            new Paragraph({
              children: [
                new TextRun({
                  text: h,
                  bold: true,
                  size: fontSize,
                  color: headerTextColor,
                  font: FONT,
                }),
              ],
            }),
          ],
          shading: { type: ShadingType.CLEAR, color: "auto", fill: headerFill },
          borders: cellBorders,
          margins: cellMargins,
        })
    ),
  });

  // Data rows with alternating shading
  const dataRows = rows.map((row, rowIdx) => {
    const fill = rowIdx % 2 === 1 ? COLORS.TABLE_ALT_ROW : "FFFFFF";
    return new TableRow({
      children: row.map((cell, colIdx) => {
        const align = colIdx > 0 && isNumeric(cell)
          ? AlignmentType.RIGHT
          : AlignmentType.LEFT;
        return new TableCell({
          children: [
            new Paragraph({
              children: [
                new TextRun({ text: cell, size: fontSize, font: FONT }),
              ],
              alignment: align,
            }),
          ],
          shading: { type: ShadingType.CLEAR, color: "auto", fill: fill },
          borders: cellBorders,
          margins: cellMargins,
        });
      }),
    });
  });

  return new Table({
    rows: [headerRow, ...dataRows],
    width: { size: 100, type: WidthType.PERCENTAGE },
  });
}

// ── 4. createBulletList ──
// items: string[], style: "synthesis" | "informational"
function createBulletList(items, style = "synthesis") {
  const indent =
    style === "synthesis"
      ? { left: 360, hanging: 180 }   // 360 DXA left, hanging indent for bullet
      : { left: 180 };                 // 180 DXA, no hanging

  return items.map(
    (item) =>
      new Paragraph({
        children: [
          new TextRun({ text: "•  ", font: FONT, size: 18 }),
          new TextRun({ text: item, font: FONT, size: 18 }),
        ],
        indent: indent,
        spacing: { after: 60 },
      })
  );
}

// ── 5. createFooter ──
// date: string (e.g., "February 23, 2026")
function createFooter(date) {
  return new Footer({
    children: [
      new Paragraph({
        children: [
          new TextRun({
            text: `Data: S&P Capital IQ via Kensho | Analysis: AI-generated | ${date}`,
            italics: true,
            size: 14, // 7pt
            color: COLORS.FOOTER_TEXT,
            font: FONT,
          }),
        ],
        alignment: AlignmentType.CENTER,
      }),
      new Paragraph({
        children: [
          new TextRun({
            text: "For informational purposes only. Not investment advice.",
            italics: true,
            size: 14,
            color: COLORS.FOOTER_TEXT,
            font: FONT,
          }),
        ],
        alignment: AlignmentType.CENTER,
      }),
    ],
  });
}
```

**在生成脚本中的使用方式：**
1. 把上述所有函数和常量复制到生成的 Node.js 脚本中
2. 使用 `createHeaderBanner(...)`，不要手写 banner 和 header table
3. 每个 section title 都调用 `createSectionHeader(...)`
4. 所有表格都调用 `createTable(...)`
5. 综合型 bullet 使用 `createBulletList(items, "synthesis")`
6. 信息型关系条目使用 `createBulletList(items, "informational")`
7. 将 `createFooter(date)` 传给 Document 构造函数中的 `footers.default`

这些函数用来消除黑底表格、标题下方多余横线段落、有边框的 header key-value 表、不一致的 bullet 样式以及遗漏页脚等问题。

## 工作流

### Step 1，识别输入

继续前先收集最多四项：
1. **Company**，公司名称或 ticker
2. **Audience**，四种之一，Equity Research、IB / M&A、Corp Dev、Sales / BD
3. **Comparable companies**，可选
4. **Page length preference**，可选

如果用户没有指定 audience，就提问。

### Step 2，读取受众专属参考文件

从本 skill 目录中读取对应 reference 文件：
- Equity Research → `references/equity-research.md`
- IB / M&A → `references/ib-ma.md`
- Corp Dev → `references/corp-dev.md`
- Sales / BD → `references/sales-bd.md`

每个 reference 都定义了章节、查询计划、格式指导和默认页数。

### Step 3，通过 S&P Global MCP 拉取数据

**首先：** 创建中间文件目录：
```bash
mkdir -p /tmp/tear-sheet/
```

使用 **S&P Global** MCP 工具，也就是 Kensho LLM-ready API。各 reference 文件中的查询计划说明了每个章节需要什么数据，并指出在每步之后要写入哪些中间文件。

**每完成一个查询步骤，都要立刻把数据写入 reference 文件指定的中间文件。** 不要拖到最后再写，因为长对话中只有写盘的数据才能稳定保留。

**查询策略：**
- 始终拉取 4 个财年的财务数据，即便只展示 3 年，因为最早一年需要用于计算最早展示年份的同比
- 按 reference 文件中的计划执行，但如果结果不完整，可以使用更合适的工具或更窄查询继续补齐
- 如果目标数据经过有针对性的重试仍然拿不到，就继续，并标记为 `N/A` 或 `Not disclosed`
- 绝不能捏造数据

**用户提供 comps：** 如果用户给了 comps，就显式查询每一家；如果没给，则用工具返回的 peer 数据，或使用 competitors 工具识别同行。

**用户自然提供的额外上下文：** 如果用户提到收购方是谁、他们卖什么，或潜在买家是谁，应直接把这些信息用于相关综合章节，不要额外追问。

**私有公司处理：**
CIQ 也覆盖私有公司，但数据会更稀疏。为私有公司生成时：
- 跳过 stock price、52-week range、beta、stock performance、consensus estimates、trading comps
- 强化 business overview、relationships、ownership structure 以及可得财务数据
- 在页眉显著标注 “Private Company”

### Step 3b，计算衍生指标

当全部数据收集完成并写入中间文件后，再统一计算所有衍生指标。这个步骤只做计算，不新增 MCP 查询。

**把所有中间文件重新读回上下文**，然后计算：
- 利润率，比如 Gross Margin、EBITDA Margin、FCF Margin、Operating Margin
- 增长率，比如收入同比、分部收入同比、EPS 同比
- 效率指标，比如 FCF Conversion、R&D as % of Revenue、Capex as % of Revenue
- 资本结构指标，比如 Net Debt 和 Net Debt / EBITDA
- 分部占比，即各分部收入占 consolidated total revenue 的比例

同时执行算术校验：
- 利润率必须能由原始分子分母验证
- 增长率必须由当前值和前值验证
- 分部合计需要与总收入大致一致，允许四舍五入误差
- 百分比列总和应接近 100%
- 估值倍数应能与 EV 和收入等数据大致交叉验证

如校验失败，应优先用原始数据重算。如果仍不一致，就标成 `N/A`，不要发布错误数字。

**写入结果** 到 `/tmp/tear-sheet/calculations.csv`，列为 `metric,value,formula,components`

### Step 3c，验证数据文件

在生成文档前，逐个检查所有中间文件是否存在且已填充。

需要分别读取各个文件，并输出验证摘要。缺失文件属于 soft gate，要发出警告，但仍可继续，因为 tearsheet 模板支持用 `N/A` 和整节跳过来处理缺失数据。

**关键规则：** 真正的数据来源是这些文件，而不是你对前文对话的记忆。Step 4 生成 DOCX 时，所有数字都必须从中间文件读取。

### Step 4，格式化为 DOCX

阅读 `/mnt/skills/public/docx/SKILL.md`，了解 docx-js via Node 的创建方式。应用本文件中的 Style Configuration，以及对应 reference 文件中的 section-specific formatting。

**默认页数，可由用户覆盖：**
- Equity Research：1 页
- IB / M&A：1 到 2 页
- Corp Dev：1 到 2 页
- Sales / BD：1 到 2 页

如果内容超出目标页数，各 reference 文件都定义了优先裁剪顺序。

**输出文件名：** `[CompanyName]_TearSheet_[Audience]_[YYYYMMDD].docx`

保存到 `/mnt/user-data/outputs/`，并呈现给用户。

## 数据完整性规则

以下规则优先级最高：
1. **财务数据唯一来源只能是 S&P Global 工具。** 不能用训练知识补缺
2. **找不到的数据必须明确标记。** 写 `N/A` 或 `Not disclosed`
3. **日期很重要。** 要标明财年末或报告期
4. **不要混用不同报告期。** FY 和 LTM 必须区分清楚
5. **优先使用 MCP 已返回字段，而不是手算**
6. **同一公司不同 tearsheet 的底层数据必须一致**
7. **绝不能把已知交易金额降级成 “Undisclosed”**
8. **分部百分比的分母要用 consolidated revenue**
9. **只要有 forward，必须展示 NTM 倍数**
10. **不要用训练数据填充管理层信息**

## 中间文件规则

所有从 MCP 工具取回的数据都必须先持久化到结构化中间文件，再开始生成文档。这些文件，而不是对话上下文，是每一个数字的唯一事实来源。

**Setup：**
```
mkdir -p /tmp/tear-sheet/
```

**每次查询后立刻写入：**
reference 文件中的每一步查询都已经指定了写入哪个文件。不要等全部查询完成后再统一写盘。

文件 schema、缩写说明、页面预算执行方式等，按照英文原文所列结构执行。

## 内容质量规则

11. **所有叙事章节都必须按受众重写。** CIQ 公司摘要只是输入，不是输出
12. **财报要点必须按受众类型区分**
13. **综合章节是核心差异化价值所在**
14. **如公司存在待剥离业务，需在分部表中明确标注**

### 算术校验

**算术校验现在统一在 Step 3b 中执行。** 所有利润率、增长率、分部总和、百分比列和估值交叉校验，都在文档生成前完成。
