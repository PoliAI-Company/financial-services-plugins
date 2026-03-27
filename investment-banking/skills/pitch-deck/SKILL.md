---
name: pitch-deck
description: "使用源文件中的数据填充投资银行 pitch deck 模板。适用场景包括，用户提供需要填充的 PowerPoint 模板，用户有 Excel/CSV 等源数据需要写入幻灯片，用户提到填充或完善现有 pitch deck 模板，或用户需要把数据迁移到既有版式中。不适用于从零开始创建演示文稿。"
---

# 填充 Investment Banking Pitch Deck 模板

## Reference Files

**开始任务时先读完所有 reference files，再开始任何工作。** 这些文件包含关键模式和反模式，会直接影响你的处理方法。不要等到遇到问题时才回头看。

| File | 用途 |
|------|------|
| [`formatting-standards.md`](reference/formatting-standards.md) | 文本、bullet、表格、图表、对齐 |
| [`slide-templates.md`](reference/slide-templates.md) | 常见 slide 类型的内容映射指导 |
| [`xml-reference.md`](reference/xml-reference.md) | PowerPoint XML 模式，涵盖表格、形状、箭头 |
| [`calculation-standards.md`](reference/calculation-standards.md) | 财务公式校验标准，CAGR、consensus |

---

## Workflow Decision Tree

**这是什么类型的任务？**

```
┌─ Populating empty template with source data?
│  └─→ Follow "Template Population Workflow" below
│
├─ Editing existing populated slides?
│  └─→ Extract current content, modify, revalidate
│
└─ Fixing formatting issues on existing slides?
   └─→ See "Common Failures" table, apply targeted fixes
```

---

## ⚠️ Critical Rendering Limitation

**LibreOffice 用于验证，但不能准确渲染 PowerPoint 文件。** 它会破坏字体、渐变、形状位置、文字换行以及部分表格格式。

**这意味着什么：** 即使某页在 LibreOffice 中看起来通过了视觉验证，在 Microsoft PowerPoint 中仍可能有问题。验证循环能发现结构性问题，例如缺失内容、损坏表格、残留 placeholder formatting，但**无法**发现字体替换、细微对齐偏移或渐变错误。

**Required action:** 交付时必须始终附上这段说明：
> "This file was validated using LibreOffice. Please review in Microsoft PowerPoint before distribution, as rendering differences may exist."

---

## Template Population Workflow

复制并跟踪进度：

```
Pitch Deck Progress:
- [ ] Phase 1: Extract and validate source data
- [ ] Phase 2: Map content to template sections
- [ ] Phase 3: Populate slides with proper formatting
- [ ] Phase 4: Validate → Fix → Repeat until clean
- [ ] Phase 5: Final verification
```

### Phase 1: Data Extraction
1. **Create backup**，在任何修改前先备份原始模板，复制为 `[filename]_backup.pptx`。直接 XML 编辑或意外错误都可能损坏文件。
2. 识别全部源材料，Excel、CSV、PDF 报告、Word 文档、数据库、web sources
3. 从每个来源中提取相关数据点
4. 将所有数字与原始来源核对
5. 统一单位和货币，转换为模板中使用的主单位 / 主币种
6. 记录所有需要校验的计算项，参见 [`calculation-standards.md`](reference/calculation-standards.md)

### Phase 2: Content Mapping
1. **Open and visually review the template**，先理解结构、风格和现有内容，再开始改动
2. 分析模板结构，识别所有 placeholder 区域和内容框
3. 将源数据映射到对应模板区域，参见 [`slide-templates.md`](reference/slide-templates.md)
4. 识别 placeholder guidance boxes，通常是任务创建者加入的彩色提示框
5. 记录数据缺口或不匹配，处理方法见 [`slide-templates.md`](reference/slide-templates.md#handling-data-template-mismatches)

### Phase 3: Template Population
1. **Remove or reformat placeholder boxes**，彩色说明框告诉你要做什么，不是最终格式。删除它们，并在原位创建符合模板风格的正式内容。参见 [Critical Anti-Patterns](#critical-anti-patterns-never-do-these)
2. 先把每个部分的内容填进去，优先解决内容完整性
3. **Then apply formatting**，使其匹配模板风格，参见 [`formatting-standards.md`](reference/formatting-standards.md)
4. 表格必须用真正的 table object，**绝不能**用 pipe 或 tab 分隔文本，参见 [`xml-reference.md`](reference/xml-reference.md#table-implementation)
5. 箭头 / 形状必须使用 PowerPoint 对象，参见 [`xml-reference.md`](reference/xml-reference.md#arrow-shapes)
6. 如果任务文件中提供了公司 logo，就插入；如果没有，提示用户：`[LOGO NOT PROVIDED - please supply company logo]`

### Phase 4: Validate → Fix → Repeat

**这是一个反馈循环。重复执行，直到所有检查通过，或者达到升级条件。**

```bash
# Convert to images for visual validation
soffice --headless --convert-to pdf presentation.pptx
pdftoppm -jpeg -r 150 presentation.pdf slide
```

**Validation checklist，逐页检查导出的图片：**
- [ ] 文字与背景对比度是否足够，清晰可读？
- [ ] 表格是否为真实对象，列对齐正确，不是 pipe/tab 文本？
- [ ] 图表 / 表格是否填满指定区域？
- [ ] 同一区域内的 bullet formatting 是否一致？
- [ ] 同层级盒子的字号是否一致？
- [ ] 是否有内容超出页面边界？
- [ ] **No placeholder formatting retained**，不能保留大块彩色说明框并把数据直接塞进去
- [ ] **No text-based "tables"**，不能用 `|` 或 tab 制造假列
- [ ] **Cross-slide consistency**，相同指标在不同页上必须完全一致

**Fix cycle protocol:**

| Cycle | Action |
|-------|--------|
| 1 | 修复全部已识别问题，然后重新验证 |
| 2 | 修复剩余问题，然后重新验证 |
| 3 | 如果问题仍然存在，记录未解决问题并升级给用户 |

**After 3 cycles, if issues remain:**
1. 列出每个未解决问题，写明 slide number 和描述
2. 说明已经尝试过什么
3. 交付文件，并明确附上免责声明："The following issues could not be resolved automatically: [list]. Manual review required."

**Do not** 无限循环。有些问题，例如字体渲染、复杂形状对齐，可能确实需要在 PowerPoint 中手工处理。

### Phase 5: Final Verification

交付前，完整走一遍 [Final Quality Checklist](#final-quality-checklist)。

---

## Quick Reference Tables

### Bullet Symbols

| Context | Symbol | Usage |
|---------|--------|-------|
| Included/Positive | ✓ | 范围内项目、已具备特性 |
| Excluded/Negative | × | 范围外项目、不具备特性 |
| Neutral list | • | 普通列举或说明 |
| Numbered sequence | 1. 2. 3. | 步骤、流程、排名 |
| Sub-bullets | – | 主 bullet 下的次级信息 |

### Slide Hierarchy Levels (Typical)

以下是常见区间，应根据模板要求调整：

| Level | Examples | Typical Size | Style |
|-------|----------|--------------|-------|
| Title | Slide title | 40-48pt | Bold |
| Subtitle | Market definition, slide descriptor | 18-22pt | Bold |
| Section Header | "Key Projections", "Commentary" | 14-16pt | Regular |
| Block Label | "Segments Included", "Definition" sidebar | 12-14pt | Regular |
| Block Content | Bullet points, body text | 11-14pt | Regular |
| Table Header | Column headers | 10-12pt | Bold |
| Table Body | Cell content | 9-11pt | Regular |
| Footnotes | Sources, notes | 8-9pt | Italic |

### Font Consistency Matching

处于**同一层级**的文本框必须使用完全一致的字号：

| Same Level | Must Match With |
|------------|-----------------|
| "Segments Included" | "Segments Excluded" |
| "Definition" | "Scope Rationale" |
| Left column bullets | Right column bullets |
| All block labels | Each other |
| All section headers | Each other |

### Rounding for Presentation

以下是**常见惯例**，应根据数值量级和模板风格调整：

| Value Type | Typical Rounding | Example |
|------------|------------------|---------|
| Large market sizes ($10bn+) | 取整到最近 $1bn | 18.5 → $19bn |
| Smaller market sizes (<$10bn) | 取整到最近 $0.5bn 或 $0.1bn | 2.3 → $2.5bn |
| Size ranges | 匹配源数据精度 | 14.9-22.1 → $15-22bn |
| CAGR | 整数 % 或 0.5% | 16.4% → 16% 或 16.5% |
| Market share | 取整到最近 5% 或与源数据一致 | 21.4% → 20% |
| Multiples | 保留 1 位小数 | 9.69 → 9.7x |

**Principle:** 四舍五入不应实质改变数字含义。数值较小时，应使用更细的精度。

### Text Density Rules

- 每个内容框最多 6 到 7 个 bullets
- 每条 bullet 最多 2 行
- 括号内示例可放同行，或另起一行缩进
- 避免孤行词，不能只剩一个单词换到下一行

### Alignment Principles

**上下垂直堆叠的框**必须在以下方面保持一致：
- 左边距位置、bullet 缩进、文本起始位置、框宽

**左右并排的框**必须在以下方面保持一致：
- 顶部位置、高度，若内容允许，以及内部 padding

### Multi-Slide Consistency

当同一组数据出现在多个 slide 时：
- 数值、格式和术语必须完全一致
- 若某页更新了指标，其他所有出现位置都必须同步更新
- 在验证阶段要交叉核对，及时发现不一致

---

## MUST Requirements

以下要求无论模板怎样，都不可妥协：

| Requirement | Details |
|-------------|---------|
| **Text Readability** | 所有文本都必须与背景形成足够对比。浅色字适用于深蓝、深绿、黑色背景，深色字适用于白色、浅灰、浅黄背景。 |
| **Actual Table Objects** | 表格数据必须使用真正的 table object，而不是 tab 分隔文本。参见 [`xml-reference.md`](reference/xml-reference.md#table-implementation)。 |
| **Proper Chart/Table Sizing** | 粘贴的视觉元素必须填满指定区域。参见 [`formatting-standards.md`](reference/formatting-standards.md#chart-and-image-handling)。 |
| **Consistent Formatting** | 同一区域内 bullet 的符号、字号、缩进必须一致。同层级盒子字号必须一致。 |
| **Content Boundaries** | 所有内容必须在 slide 边界内。Footnote box 宽度，16:9 约 32.5cm，4:3 约 24cm。 |
| **No Placeholder Formatting** | 删除彩色说明框。正文区域应根据模板使用浅底深字。 |

---

## Critical Anti-Patterns: NEVER DO THESE

这些错误通常来自于把 placeholder formatting 误当作最终输出格式。能否识别这些模式很关键。

### Anti-Pattern 1: 把真实数据直接填进 Placeholder Boxes

**What happens:** 模板里有彩色说明框，黄色、橙色等，内含指导文字。模型把指导文字替换成真实数据，但保留了原来的彩色框。

**Why it's wrong:** 彩色框本身就是 placeholder。它告诉你应该放什么内容，不代表最终格式。最终输出应使用不同样式，通常是浅底深字，或正式样式的 shape。

**Recognition test:** 如果你交付的页面里仍有大块彩色矩形，里面塞着真实数据，那你复制的是 placeholder 样式，而不是在做替换。

**Critical distinction，placeholders 分两类：**

| Type | How to identify | What to do |
|------|-----------------|------------|
| **Instruction boxes** | 颜色很亮，黄色、橙色，内含 "Insert X here" 之类指导文字，浅色字配彩色背景 | 删除整个 shape，然后用正式格式重建内容 |
| **Layout placeholders** | 属于 slide master / layout 的一部分，颜色中性，与模板主题一致，显示 "Click to add text" | 保留 shape，只替换文字内容 |

如果不确定，就检查同一模板的空白页里这个 shape 是否还存在。Layout placeholder 会保留，instruction box 只是普通图形。

### Anti-Pattern 2: 文本伪表格

**What happens:** 用 `|`、tab 或空格拼出看起来像表格的内容，而不是真正的 table object。

**Why it's wrong:** 这根本不是表格。列永远无法稳定对齐，格式也无法统一，而且看起来非常业余。

**Recognition test:** 如果你在输入 `|` 字符，或者依赖空格和 tab 来造列，那你做的是文本，不是表格。

**MUST verify:** 创建任何表格后，必须验证它是真正的 table object。验证方法见 [`xml-reference.md`](reference/xml-reference.md#critical-verify-tables-are-actual-table-objects)。

### Anti-Pattern 3: 继承 Placeholder 的对比度样式

**What happens:** Placeholder 用浅色字配彩色背景，例如白字黄底。模型填入真实数据后保留这种配色，导致内容难以阅读。

**Why it's wrong:** Placeholder 的颜色本来就是为了提醒“这里要替换”。正式页面中的正文，通常应使用浅底深字。

**Recognition test:** 如果正文区域仍然是亮色背景上放白字或浅色字，而且不是标题区，你就是继承了 placeholder formatting。

**Correct approach:** 应使用正式格式，通常正文用深色文字，`#000000` 或 `#333333`，配白色或浅色背景。标题和强调区域可以用品牌色。

### Summary: Placeholder vs. Production

| Element | Placeholder (Input) | Production (Output) |
|---------|---------------------|---------------------|
| Instruction boxes | 彩色背景，指导文字 | 删除或重设格式 |
| Data areas | `[Insert data here]` 文本 | 真实数据，清晰排版 |
| Tables | 描述表格应包含什么 | 真实 table object，含行列结构 |
| Body text | 彩底浅字 | 浅底深字 |

**Placeholder 告诉你该做什么，不告诉你最终该怎么排。**

---

## Common Failures

更详细的说明见上方 [Critical Anti-Patterns](#critical-anti-patterns-never-do-these)。

| Failure | Solution | Reference |
|---------|----------|-----------|
| Unstructured text dumps | 拆成 bullets，✓、×、• | [`formatting-standards.md`](reference/formatting-standards.md#bullet-point-structure) |
| Pipe/tab-separated "tables" | 创建真实 table objects，带分隔符的文本不算表格 | [`xml-reference.md`](reference/xml-reference.md#table-implementation) |
| Poor text/background contrast | 检查每个文字元素 | — |
| Tiny pasted charts | 放大到填满区域，只粘贴 chart 本身 | [`formatting-standards.md`](reference/formatting-standards.md#proper-sizing-workflow) |
| Source data pasted with charts | 复制前只选 chart object | — |
| Data dumped into placeholder boxes | 删除彩色说明框，用正式格式重建内容 | [Anti-Patterns](#critical-anti-patterns-never-do-these) |
| Inconsistent bullets | 先定义一种样式，再整页统一应用 | [`formatting-standards.md`](reference/formatting-standards.md#bullet-consistency) |
| Inconsistent fonts across boxes | 同层级统一字号 | [`formatting-standards.md`](reference/formatting-standards.md#font-consistency) |
| Content overflow | 明确设置框宽，footnotes: 16:9 用 32.5cm，4:3 用 24cm | — |
| Missing logo | 使用任务文件中的 logo，没有就提示用户 | — |
| Remaining `[brackets]` | 搜索并替换所有 placeholder | — |
| Text arrows (→, ⟹) | 改用 PowerPoint shape objects | [`xml-reference.md`](reference/xml-reference.md#arrow-shapes) |

---

## Error Handling

**If PDF/image conversion fails:**
1. 检查 LibreOffice 是否安装，`which soffice`
2. 尝试备用命令，`libreoffice --headless --convert-to pdf presentation.pptx`
3. 如果仍失败，就在 PowerPoint/LibreOffice 中手动打开并导出

**If source data has inconsistencies or conflicts:**
1. **Priority order**: 优先使用任务文件中明确给出的数据
2. 如果使用外部数据，web search 或外部文档，要明确告知用户
3. 显式记录所有差异
4. 用脚注说明采用该数据源的原因

**If calculations don't match source projections:**
1. 展示你的计算方法
2. 说明差异及可能原因，基准年份不同、方法不同等
3. 如果差异显著，就同时展示两组数值
4. 标记给用户决策

---

## Table Structure Guidelines

创建表格时，必须使用真实 table object：

**Column Alignment:**
- 文本列：左对齐，header 和正文都左对齐
- 数值列：右对齐或居中，header 与正文保持一致

**Header Row:**
- 粗体
- 着色背景，使用模板品牌色
- 白字或高对比文本颜色

**Consensus/Total Row:**
- 粗体
- 上方加分隔线
- 用不同底色区分

**Width:** 完全填满指定区域宽度。

XML 实现方式参见 [`xml-reference.md`](reference/xml-reference.md#table-implementation)。

---

## Footnote Format

**Format:**
```
Sources: [Source 1] (Year), [Source 2] (Year).
Notes: (1) [First note]; (2) [Second note].
```

**Example:**
```
Sources: Grand View Research (2024), Mordor Intelligence (2024), Markets and Markets (2023).
Notes: (1) Excludes hardware revenue; (2) Includes both B2B and B2C segments.
```

正文中的所有上标数字，¹、²、³，都必须在 Notes 中有对应条目。

---

## Logo Placement

- 使用任务材料中提供的 logo 文件
- 如果未提供，提示用户：`[LOGO NOT PROVIDED - please supply company logo]`
- 位置通常在右上角，尺寸在全 deck 中保持一致，且不能压到正文内容

---

## Data Requirements by Slide Type

不同 slide 类型的详细数据要求、格式原则和示例列标题，见 [`slide-templates.md`](reference/slide-templates.md#common-slide-types-and-data-requirements)。

常见类型包括：Market Definition、Market Sizing/TAM、Competitive Landscape、Financial Summary、Transaction Comparables。

---

## Final Quality Checklist

交付填充后的模板前，请验证：

### Data Accuracy
- [ ] 所有数字与原始源文件一致
- [ ] 所有计算值均已按公式验证，见 [`calculation-standards.md`](reference/calculation-standards.md)
- [ ] 年份和时间区间正确
- [ ] 公司 / 可比公司名称拼写正确
- [ ] 相同数字在所有出现的 slide 上都完全一致

### Content Mapping
- [ ] 每个模板区域都填入了合适的数据
- [ ] 没有残留 `[bracket]` placeholder text
- [ ] 所有来源引用都已写入脚注
- [ ] 所有脚注编号，¹²³，都在 Notes 中有对应项

### Formatting
- [ ] 所有文本与背景对比充分，清晰可读
- [ ] 表格是真实 table objects，不是 pipe/tab 文本
- [ ] 图表 / 表格填满指定区域，不是缩略图
- [ ] 每个 section 内的 bullet formatting 一致
- [ ] 同层级盒子的字号一致
- [ ] 没有内容超出 slide 边界
- [ ] 没有保留 placeholder boxes 并把数据塞进去
- [ ] 最终输出中没有彩色 instruction boxes

### Template Compliance
- [ ] Placeholder instruction boxes 已删除或重设格式
- [ ] 格式匹配模板风格，颜色、字体
- [ ] Logo 已放置且位置正确
- [ ] 正文采用正式呈现格式，主内容区为浅底深字

### Final Step
- [ ] 建议用户在分发前用 Microsoft PowerPoint 再做一次最终检查，LibreOffice 可能存在渲染差异
