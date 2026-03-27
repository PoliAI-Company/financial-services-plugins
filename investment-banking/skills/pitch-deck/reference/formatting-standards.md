# 格式标准参考

本参考文件汇总了创建 pitch deck 时常见的 PowerPoint 格式原则。这些是通用最佳实践，应根据实际使用的模板进行调整。

---

## Table of Contents

1. [视觉层级与版式](#视觉层级与版式)
2. [文本格式](#文本格式)
3. [表格创建](#表格创建)
4. [图表和图片处理](#图表和图片处理)
5. [数据可视化](#数据可视化)
6. [字体一致性](#字体一致性)
7. [模板适配](#模板适配)

---

## 视觉层级与版式

### 框体和分区布局

幻灯片布局会因内容和模板设计而不同。常见元素包括：
- 含标题和副标题的页眉区域
- 带标签侧栏的内容框
- 用于结构化数据的表格
- 用于可视化数据的图表
- 位于页脚的 footnote 区

具体布局应以实际模板为准。常见内容类型及典型结构包括：
- **Market definition slides**：标签框 + bullet 内容 + commentary 区
- **TAM/sizing slides**：核心指标 callout + 数据表 + 关键结论
- **Competitive analysis**：对比表或矩阵
- **Financial summaries**：图表 + 支撑数据表

### 对齐原则

**上下平行区域的垂直对齐：**

上下堆叠的框在以下方面应保持一致：
- 左边距位置
- Bullet 缩进
- 文本起始位置
- 框宽

左右相邻的框在以下方面应保持一致：
- 顶部位置
- 高度，若内容允许
- 内边距

---

## 文本格式

### Bullet Point Structure

不要堆砌未经整理的文本。应把内容拆成便于快速浏览的 bullet。

**Illustrative Correct Structure:**
```
✓  Consumer mobile and web language learning apps
   (Duolingo, Babbel, Memrise, Busuu)
✓  B2B enterprise language training platforms
   (goFLUENT, Speexx, Learnship)
✓  Online tutoring marketplaces
   (italki, Preply, Cambly)
```

**Illustrative Incorrect Structure (Text Dump):**
```
Consumer mobile/web apps (Duolingo, Babbel, Memrise, Busuu)
B2B enterprise platforms (Speexx, Rosetta Stone Enterprise)
Online tutoring marketplaces (Preply, italki, Cambly)
```

### Bullet Symbol Guidelines

| Context | Symbol | Usage |
|---------|--------|-------|
| Included/Positive | ✓ (checkmark) | 范围内项目、已存在特性 |
| Excluded/Negative | × (cross) | 范围外项目、缺失特性 |
| Neutral list | • (bullet) | 普通列举或说明 |
| Numbered sequence | 1. 2. 3. | 流程步骤、排名 |
| Sub-bullets | ‣ or – | 主 bullet 下的次级信息 |

应根据模板现有风格来选择符号。

### Bullet Consistency

同一框 / 同一区域内的 bullet 必须格式一致：
- 符号一致，除非有意区分
- 主 bullet 缩进一致
- Bullet 大小一致
- Bullet 与正文之间间距一致
- 同层级 bullet 正文字号一致

### Font Size Guidelines

以下是常见区间，应根据模板要求调整：

| Element | Typical Size (pt) | Style |
|---------|-------------------|-------|
| Slide Title | 40-48 | Bold |
| Subtitle/Definition | 18-22 | Bold |
| Section Headers | 14-16 | Regular |
| Body Text/Bullets | 12-14 | Regular |
| Table Headers | 10-12 | Bold |
| Table Body | 9-11 | Regular |
| Footnotes | 8-9 | Italic |

### Text Density Guidelines

- 每个内容框**最多 6 到 7 个 bullets**，根据空间可略调
- 每条 bullet **最多 2 行**
- **括号示例**可放在同一行，或下一行缩进显示
- **避免孤行词**，不要让单个词单独换到下一行

---

## 表格创建

### CRITICAL: 使用真正的 Table Objects

**表格必须是 table object，绝不能是用 tab 间隔的文本。**

带 tab 的文本永远无法稳定对齐，看起来也不专业。始终要创建真正的表格对象。

### 表格结构规范

1. **列对齐**：
   - 文本列左对齐，header 和正文都左对齐
   - 数值列居中或右对齐
   - Header 的对齐方式要与该列正文一致

2. **Header row**：
   - 粗体
   - 带底色，使用模板品牌色
   - 文字颜色必须具备足够对比度
   - 对齐方式与正文列一致

3. **Alternating rows**，可选：
   - 交替浅底色有助于阅读

4. **Summary/Total row**：
   - 粗体
   - 上方加粗分隔线
   - 使用不同底色区分

5. **Table width**：
   - 填满指定区域宽度
   - 不要让表格漂在大片空白中

### XML 实现模式见 [`xml-reference.md`](xml-reference.md#table-implementation)

---

## 图表和图片处理

### 从 Excel 粘贴图表

从 Excel 粘贴图表时：

1. **只粘贴图表本体**，不要连源数据表一起带进来
2. **放大到填满指定区域**，图表不能像缩略图一样缩在角落
3. **保持纵横比**，不要拉伸变形
4. **检查可读性**，坐标轴、图例、数据标签都必须清晰可读

### 从 Excel 粘贴表格

从 Excel 粘贴表格时：

1. **只粘贴格式化后的表格**，排除源数据与计算过程
2. **放大到填满指定区域**
3. **检查列宽**，确保文字没有被截断
4. **检查格式是否保留**，颜色、边框、字体可能需要手动微调

### Size Guidelines

**最低尺寸原则：**
- 图表应占据其指定区域的大部分空间
- 表格应完全填满指定区域宽度
- 图片大小应与上下文匹配，绝不能像缩略图

**缩得太小的典型迹象，应避免：**
- 图表只占可用空间的一小部分
- 标签无法阅读
- 视觉元素周围留下大片空白
- 看起来像一个小缩略图

### Proper Sizing Workflow

1. 先识别目标区域的尺寸
2. 粘贴图表 / 表格
3. 立即调整大小以填满目标区域
4. 检查所有文字是否仍然清晰可读
5. 必要时调整内部元素，图例位置、坐标轴标签等

---

## 数据可视化

### 核心指标展示

展示核心指标时，例如 TAM、CAGR、projections，应尽量体现它们之间的关系，而不是静态罗列：

- **Visual flow indicators**：用箭头、chevron、connector 等 shape 展示推进关系
- **Size hierarchy**：主要指标字体更大，标签更小
- **Spatial arrangement**：用空间布局体现逻辑关系

### Arrow and Flow Indicators

如果使用箭头或流向指示：
- 使用 PowerPoint shape objects，不要用文本字符
- 最终演示中不要出现 `→`、`⟹` 这类文本箭头
- 用 PowerPoint 的 shape 工具，或用 XML shape 元素创建箭头

**XML 实现见 [`xml-reference.md`](xml-reference.md#arrow-shapes)**

---

## 字体一致性

### Cross-Box Font Consistency

所有处于同一层级的文本框都应使用完全一致的字号。

**需要一致的同层级框包括：**

| Box Type | Should Match With |
|----------|-------------------|
| "Segments Included" content | "Segments Excluded" content |
| "Definition" content | "Scope Rationale" content |
| Left column bullets | Right column bullets |
| All label boxes | Each other |
| All section headers | Each other |

### Verification Process

1. 识别所有同层级文本框
2. 检查每个框的字号
3. 如有差异，统一调整
4. 如果都能容纳内容，优先采用较大字号，否则统一采用较小字号

**Exception**：Sub-bullets 或次级说明可以比主 bullet 小，但必须在所有同类框中保持一致。

---

## 模板适配

这些标准应根据实际模板进行适配：

1. **Colors**：使用模板品牌色，而不是机械套用固定颜色
2. **Fonts**：使用模板指定字体
3. **Spacing**：遵循模板现有的间距规则
4. **Layout**：遵循模板原有版式结构

无论模板如何变化，以下原则始终不变：
- 文本必须与背景形成足够对比
- 表格必须是真正的 table object
- 内容应合理填满可用空间
- 平行元素之间的格式应保持一致
- 图表 / 图片尺寸必须合适
