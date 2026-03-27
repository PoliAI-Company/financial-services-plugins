---
name: ppt-template-creator
description: 从用户提供的 PowerPoint 模板中创建自包含的 PPT 模板 SKILL，而不是创建演示文稿本身。仅在用户想把模板做成可复用 skill 时使用。如果用户要直接创建实际演示文稿，请使用 pptx skill。
---

# PPT 模板创建器

**此 skill 创建的是 SKILL，而不是演示文稿。** 当用户想把自己的 PowerPoint 模板转成可反复用于生成演示文稿的 skill 时使用。如果用户只是想创建演示文稿，请改用 `pptx` skill。

生成的 skill 包含：
- `assets/template.pptx` - 模板文件
- `SKILL.md` - 完整说明，不需要再引用这个 meta skill

**关于通用的 skill 构建最佳实践**，请参考 `skill-creator` skill。这个 skill 只聚焦 PPT 相关模式。

## 工作流

1. **用户提供模板**（.pptx 或 .potx）
2. **分析模板**，提取版式、占位符和尺寸
3. **初始化 skill**，使用 `skill-creator` skill 搭建 skill 结构
4. **添加模板**，把 .pptx 复制到 `assets/template.pptx`
5. **编写 SKILL.md**，按下方模板填写 PPT 特定细节
6. **创建示例**，生成示例演示文稿用于验证
7. **打包**，使用 `skill-creator` skill 打包为 `.skill` 文件

## 第 2 步：分析模板

**关键：提取精确的占位符位置**。这会决定内容区边界。

```python
from pptx import Presentation

prs = Presentation(template_path)
print(f"Dimensions: {prs.slide_width/914400:.2f}\" x {prs.slide_height/914400:.2f}\"")
print(f"Layouts: {len(prs.slide_layouts)}")

for idx, layout in enumerate(prs.slide_layouts):
    print(f"\n[{idx}] {layout.name}:")
    for ph in layout.placeholders:
        try:
            ph_idx = ph.placeholder_format.idx
            ph_type = ph.placeholder_format.type
            # IMPORTANT: Extract exact positions in inches
            left = ph.left / 914400
            top = ph.top / 914400
            width = ph.width / 914400
            height = ph.height / 914400
            print(f"    idx={ph_idx}, type={ph_type}")
            print(f"        x={left:.2f}\", y={top:.2f}\", w={width:.2f}\", h={height:.2f}\"")
        except:
            pass
```

**需要记录的关键尺寸：**
- **标题位置**：标题占位符在什么位置？
- **副标题/描述**：副标题行在哪里？
- **页脚占位符**：页脚或来源通常放哪里？
- **内容区**：副标题和页脚之间的区域就是内容区

### 找到真实内容区起始位置

**关键：** 内容区不一定在副标题占位符结束后立刻开始。很多模板会在副标题与正文区之间保留边框、分割线或留白。

**最佳方法：** 查看 Layout 2 或类似的内容版式，找到带有 OBJECT 占位符的版式，这个占位符的 `y` 位置就是内容实际起点。

```python
# Find the OBJECT placeholder to determine true content start
for idx, layout in enumerate(prs.slide_layouts):
    for ph in layout.placeholders:
        try:
            if ph.placeholder_format.type == 7:  # OBJECT type
                top = ph.top / 914400
                print(f"Layout [{idx}] {layout.name}: OBJECT starts at y={top:.2f}\"")
                # This y value is where your content should start!
        except:
            pass
```

**例如：** 模板可能出现：
- 副标题结束于 y=1.38"
- 但 OBJECT 占位符从 y=1.90" 开始
- 中间 0.52" 的空隙保留给边框或分割线，**不要在那里放内容**

应使用 OBJECT 占位符的 `y` 值作为内容起始位置，而不是副标题的结束位置。

## 第 5 步：编写 SKILL.md

生成的 skill 应具有以下结构：
```
[company]-ppt-template/
├── SKILL.md
└── assets/
    └── template.pptx
```

### 生成的 SKILL.md 模板

生成的 SKILL.md 必须**自包含**，把所有说明直接写进去。使用下面这个模板，并把方括号中的值替换为你的分析结果：

````markdown
---
name: [company]-ppt-template
description: [Company] PowerPoint template for creating presentations. Use when creating [Company]-branded pitch decks, board materials, or client presentations.
---

# [Company] PPT Template

Template: `assets/template.pptx` ([WIDTH]" x [HEIGHT]", [N] layouts)

## Creating Presentations

```python
from pptx import Presentation

prs = Presentation("path/to/skill/assets/template.pptx")

# DELETE all existing slides first
while len(prs.slides) > 0:
    rId = prs.slides._sldIdLst[0].rId
    prs.part.drop_rel(rId)
    del prs.slides._sldIdLst[0]

# Add slides from layouts
slide = prs.slides.add_slide(prs.slide_layouts[LAYOUT_IDX])
```

## Key Layouts

| Index | Name | Use For |
|-------|------|---------|
| [0] | [Layout Name] | [Cover/title slide] |
| [N] | [Layout Name] | [Content with bullets] |
| [N] | [Layout Name] | [Two-column layout] |

## Placeholder Mapping

**CRITICAL: Include exact positions (x, y coordinates) for each placeholder.**

### Layout [N]: [Name]
| idx | Type | Position | Use |
|-----|------|----------|-----|
| [idx] | TITLE (1) | y=[Y]" | Slide title |
| [idx] | BODY (2) | y=[Y]" | Subtitle/description |
| [idx] | BODY (2) | y=[Y]" | Footer |
| [idx] | BODY (2) | y=[Y]" | Source/notes |

### Content Area Boundaries

**Document the safe content area for custom shapes/tables/charts:**

```
Content Area (for Layout [N]):
- Left margin: [X]" (content starts here)
- Top: [Y]" (below subtitle placeholder)
- Width: [W]"
- Height: [H]" (ends before footer)

For 4-quadrant layouts:
- Left column: x=[X]", width=[W]"
- Right column: x=[X]", width=[W]"
- Top row: y=[Y]", height=[H]"
- Bottom row: y=[Y]", height=[H]"
```

**Why this matters:** Custom content (textboxes, tables, charts) must stay within these boundaries to avoid overlapping with template placeholders like titles, footers, and source lines.

## Filling Content

**Do NOT add manual bullet characters** - slide master handles formatting.

```python
# Fill title
for shape in slide.shapes:
    if hasattr(shape, 'placeholder_format'):
        if shape.placeholder_format.type == 1:  # TITLE
            shape.text = "Slide Title"

# Fill content with hierarchy (level 0 = header, level 1 = bullet)
for shape in slide.shapes:
    if hasattr(shape, 'placeholder_format'):
        idx = shape.placeholder_format.idx
        if idx == [CONTENT_IDX]:
            tf = shape.text_frame
            for para in tf.paragraphs:
                para.clear()

            content = [
                ("Section Header", 0),
                ("First bullet point", 1),
                ("Second bullet point", 1),
            ]

            tf.paragraphs[0].text = content[0][0]
            tf.paragraphs[0].level = content[0][1]
            for text, level in content[1:]:
                p = tf.add_paragraph()
                p.text = text
                p.level = level
```

## Example: Cover Slide

```python
slide = prs.slides.add_slide(prs.slide_layouts[[COVER_IDX]])
for shape in slide.shapes:
    if hasattr(shape, 'placeholder_format'):
        idx = shape.placeholder_format.idx
        if idx == [TITLE_IDX]:
            shape.text = "Company Name"
        elif idx == [SUBTITLE_IDX]:
            shape.text = "Presentation Title | Date"
```

## Example: Content Slide

```python
slide = prs.slides.add_slide(prs.slide_layouts[[CONTENT_IDX]])
for shape in slide.shapes:
    if hasattr(shape, 'placeholder_format'):
        ph_type = shape.placeholder_format.type
        idx = shape.placeholder_format.idx
        if ph_type == 1:
            shape.text = "Executive Summary"
        elif idx == [BODY_IDX]:
            tf = shape.text_frame
            for para in tf.paragraphs:
                para.clear()
            content = [
                ("Key Findings", 0),
                ("Revenue grew 40% YoY to $50M", 1),
                ("Expanded to 3 new markets", 1),
                ("Recommendation", 0),
                ("Proceed with strategic initiative", 1),
            ]
            tf.paragraphs[0].text = content[0][0]
            tf.paragraphs[0].level = content[0][1]
            for text, level in content[1:]:
                p = tf.add_paragraph()
                p.text = text
                p.level = level
```
````

## 第 6 步：创建示例输出

生成一个示例演示文稿来验证 skill 是否正常工作。将其与 skill 一起保存，作为参考。

## 面向生成 skill 的 PPT 专属规则

1. **模板放在 assets/** 中，始终打包 `.pptx` 文件
2. **SKILL.md 自包含**，所有说明都直接嵌入，不依赖外部引用
3. **不要手动添加项目符号**，使用 `paragraph.level` 表示层级
4. **先删除所有幻灯片**，再开始新增
5. **按 idx 记录占位符**，placeholder idx 是模板特有的
