# PowerPoint XML 参考

本文件汇总了以程序化方式编辑 PowerPoint 时可用的 XML 模式。直接处理 OOXML 格式时，可以参考这些模式。

**Note:** 示例中的颜色值，例如 `E67E22`、`D35400`，只是占位符。实际使用时应替换为模板的品牌色。

---

## ⚠️ 何时使用本参考

**以下场景请使用 python-pptx：**
- 创建新表格，python-pptx 会自动处理单元格结构和 relationships
- 添加文本框
- 插入图片
- 大多数 shape 创建
- 任何 python-pptx 已提供 API 的操作

**只有在以下场景才直接编辑 XML：**
- 修改 python-pptx API 没有暴露的既有元素属性
- 在通过 python-pptx 创建表格后，再对单元格格式做精细调整
- 微调 python-pptx API 尚不支持的特定 shape 属性

**NEVER use direct XML for:**
- 从零创建表格，relationship 管理容易出错，并且很可能损坏文件
- 初始 shape 创建，容易引发 shape ID 冲突
- 任何本可通过 python-pptx 完成的工作

本文件中的 XML 模式用于**参考和定向修改**，不是让你整块构建新元素。

---

## XML 编辑风险

如果不谨慎，直接编辑 XML 会损坏 PowerPoint 文件：
- PowerPoint XML 存在多层依赖，relationship files、content types 等
- 无效 XML 或缺失 relationship 会破坏整个文件
- 每页中的 shape ID 都必须唯一

**Always work on a backup copy**，绝不要直接编辑原始文件。

---

## 目录
- [表格实现](#表格实现)
- [箭头形状](#箭头形状)
- [文本框](#文本框)
- [带填充的形状](#带填充的形状)
- [图片插入](#图片插入)
- [连接线](#连接线)
- [单位换算](#单位换算)

---

## 表格实现

### CRITICAL: 验证表格是真正的 Table Object

创建任何表格后，你都**必须**验证它是真正的 table object，而不是带分隔符的文本。

**Programmatic verification (python-pptx):**
```python
for shape in slide.shapes:
    if shape.has_table:
        print(f"✓ Found table: {len(shape.table.rows)} rows, {len(shape.table.columns)} columns")
```

**Visual verification (in exported image):**
- 无论内容长短，列都能严格对齐
- 单元格边框一致
- 选中表格时，应作为一个整体被选中

**Failure indicators，你创建的是文本，不是表格：**
- 值之间能看到 `|` 字符
- 内容长度变化时，列会错位
- 使用了 tab 字符 `\t` 来制造间距
- 用多个文本框拼成看似表格的版式

基于文本的“伪表格”无法被接收方正常编辑，字体变化后会错位，也会明显显得不专业。在 pitch deck 中，没有任何可以接受的场景去使用 pipe/tab 分隔的表格文本。

---

### Basic Table Structure

```xml
<a:tbl>
  <a:tblPr firstRow="1" bandRow="1">
    <a:tableStyleId>{5C22544A-7EE6-4342-B048-85BDC9FD1C3A}</a:tableStyleId>
  </a:tblPr>
  <a:tblGrid>
    <a:gridCol w="2000000"/>  <!-- Source column - width in EMUs -->
    <a:gridCol w="1200000"/>  <!-- 2024 Size column -->
    <a:gridCol w="1200000"/>  <!-- CAGR column -->
    <a:gridCol w="1200000"/>  <!-- 2030 Projection column -->
  </a:tblGrid>
  <!-- Row definitions follow -->
</a:tbl>
```

### Table Row with Cells

```xml
<a:tr h="370840">  <!-- Row height in EMUs -->
  <a:tc>
    <a:txBody>
      <a:bodyPr/>
      <a:lstStyle/>
      <a:p>
        <a:pPr algn="l"/>  <!-- Left alignment for text columns -->
        <a:r>
          <a:rPr lang="en-US" sz="1000" b="0"/>
          <a:t>Grand View Research</a:t>
        </a:r>
      </a:p>
    </a:txBody>
    <a:tcPr/>
  </a:tc>
  <a:tc>
    <a:txBody>
      <a:bodyPr/>
      <a:lstStyle/>
      <a:p>
        <a:pPr algn="ctr"/>  <!-- Center alignment for numeric columns -->
        <a:r>
          <a:rPr lang="en-US" sz="1000"/>
          <a:t>22.1</a:t>
        </a:r>
      </a:p>
    </a:txBody>
    <a:tcPr/>
  </a:tc>
  <!-- Additional cells... -->
</a:tr>
```

### Header Row Styling

```xml
<a:tr h="370840">
  <a:tc>
    <a:txBody>
      <a:bodyPr/>
      <a:lstStyle/>
      <a:p>
        <a:pPr algn="l"/>
        <a:r>
          <a:rPr lang="en-US" sz="1000" b="1">  <!-- Bold for headers -->
            <a:solidFill>
              <a:srgbClr val="FFFFFF"/>  <!-- White text -->
            </a:solidFill>
          </a:rPr>
          <a:t>Source</a:t>
        </a:r>
      </a:p>
    </a:txBody>
    <a:tcPr>
      <a:solidFill>
        <a:srgbClr val="E67E22"/>  <!-- Orange background -->
      </a:solidFill>
    </a:tcPr>
  </a:tc>
  <!-- Additional header cells... -->
</a:tr>
```

---

## 箭头形状

### Right Arrow Shape

```xml
<p:sp>
  <p:nvSpPr>
    <p:cNvPr id="10" name="Arrow Right"/>
    <p:cNvSpPr/>
    <p:nvPr/>
  </p:nvSpPr>
  <p:spPr>
    <a:xfrm>
      <a:off x="3000000" y="2500000"/>  <!-- Position in EMUs -->
      <a:ext cx="500000" cy="300000"/>   <!-- Size in EMUs -->
    </a:xfrm>
    <a:prstGeom prst="rightArrow">
      <a:avLst/>
    </a:prstGeom>
    <a:solidFill>
      <a:srgbClr val="E67E22"/>  <!-- Arrow fill color -->
    </a:solidFill>
    <a:ln>
      <a:noFill/>  <!-- No outline -->
    </a:ln>
  </p:spPr>
</p:sp>
```

### Down Arrow Shape

```xml
<p:sp>
  <p:nvSpPr>
    <p:cNvPr id="11" name="Arrow Down"/>
    <p:cNvSpPr/>
    <p:nvPr/>
  </p:nvSpPr>
  <p:spPr>
    <a:xfrm>
      <a:off x="2500000" y="3000000"/>
      <a:ext cx="300000" cy="500000"/>
    </a:xfrm>
    <a:prstGeom prst="downArrow">
      <a:avLst/>
    </a:prstGeom>
    <a:solidFill>
      <a:srgbClr val="E67E22"/>
    </a:solidFill>
  </p:spPr>
</p:sp>
```

### Chevron Shape

```xml
<p:sp>
  <p:nvSpPr>
    <p:cNvPr id="12" name="Chevron"/>
    <p:cNvSpPr/>
    <p:nvPr/>
  </p:nvSpPr>
  <p:spPr>
    <a:xfrm>
      <a:off x="3000000" y="2500000"/>
      <a:ext cx="400000" cy="600000"/>
    </a:xfrm>
    <a:prstGeom prst="chevron">
      <a:avLst/>
    </a:prstGeom>
    <a:solidFill>
      <a:srgbClr val="E67E22"/>
    </a:solidFill>
  </p:spPr>
</p:sp>
```

---

## 文本框

### Basic Text Box

```xml
<p:sp>
  <p:nvSpPr>
    <p:cNvPr id="5" name="TextBox 4"/>
    <p:cNvSpPr txBox="1"/>
    <p:nvPr/>
  </p:nvSpPr>
  <p:spPr>
    <a:xfrm>
      <a:off x="500000" y="1500000"/>
      <a:ext cx="4000000" cy="500000"/>
    </a:xfrm>
    <a:prstGeom prst="rect">
      <a:avLst/>
    </a:prstGeom>
    <a:noFill/>
  </p:spPr>
  <p:txBody>
    <a:bodyPr wrap="square" rtlCol="0">
      <a:spAutoFit/>
    </a:bodyPr>
    <a:lstStyle/>
    <a:p>
      <a:r>
        <a:rPr lang="en-US" sz="1400" dirty="0"/>
        <a:t>Text content here</a:t>
      </a:r>
    </a:p>
  </p:txBody>
</p:sp>
```

### Text Box with Bullet Points

```xml
<p:txBody>
  <a:bodyPr wrap="square">
    <a:spAutoFit/>
  </a:bodyPr>
  <a:lstStyle/>
  <a:p>
    <a:pPr marL="342900" indent="-342900">
      <a:buFont typeface="Wingdings" panose="05000000000000000000" pitchFamily="2" charset="2"/>
      <a:buChar char="&#252;"/>  <!-- Checkmark character -->
    </a:pPr>
    <a:r>
      <a:rPr lang="en-US" sz="1400" dirty="0"/>
      <a:t>First bullet point</a:t>
    </a:r>
  </a:p>
  <a:p>
    <a:pPr marL="342900" indent="-342900">
      <a:buFont typeface="Wingdings" panose="05000000000000000000" pitchFamily="2" charset="2"/>
      <a:buChar char="&#252;"/>
    </a:pPr>
    <a:r>
      <a:rPr lang="en-US" sz="1400" dirty="0"/>
      <a:t>Second bullet point</a:t>
    </a:r>
  </a:p>
</p:txBody>
```

### Text with White Color (for dark backgrounds)

```xml
<a:r>
  <a:rPr lang="en-US" sz="1000" b="1" i="1" dirty="0">
    <a:solidFill>
      <a:srgbClr val="FFFFFF"/>  <!-- White text -->
    </a:solidFill>
  </a:rPr>
  <a:t>White text on colored background</a:t>
</a:r>
```

---

## 带填充的形状

### Rectangle with Solid Fill

```xml
<p:sp>
  <p:nvSpPr>
    <p:cNvPr id="20" name="Rectangle 19"/>
    <p:cNvSpPr/>
    <p:nvPr/>
  </p:nvSpPr>
  <p:spPr>
    <a:xfrm>
      <a:off x="500000" y="2500000"/>
      <a:ext cx="1000000" cy="2000000"/>
    </a:xfrm>
    <a:prstGeom prst="rect">
      <a:avLst/>
    </a:prstGeom>
    <a:solidFill>
      <a:srgbClr val="E67E22"/>  <!-- Orange fill -->
    </a:solidFill>
    <a:ln w="12700">  <!-- Border width -->
      <a:solidFill>
        <a:srgbClr val="D35400"/>  <!-- Darker border -->
      </a:solidFill>
    </a:ln>
  </p:spPr>
  <p:txBody>
    <a:bodyPr rtlCol="0" anchor="ctr"/>  <!-- Vertically centered text -->
    <a:lstStyle/>
    <a:p>
      <a:pPr algn="ctr"/>  <!-- Horizontally centered -->
      <a:r>
        <a:rPr lang="en-US" sz="1600" b="1">
          <a:solidFill>
            <a:srgbClr val="FFFFFF"/>
          </a:solidFill>
        </a:rPr>
        <a:t>Label Text</a:t>
      </a:r>
    </a:p>
  </p:txBody>
</p:sp>
```

---

## 图片插入

### Adding Image to Slide

```xml
<p:pic>
  <p:nvPicPr>
    <p:cNvPr id="99" name="Company Logo"/>
    <p:cNvPicPr>
      <a:picLocks noChangeAspect="1"/>
    </p:cNvPicPr>
    <p:nvPr/>
  </p:nvPicPr>
  <p:blipFill>
    <a:blip r:embed="rIdLogo"/>  <!-- Reference to relationship ID -->
    <a:stretch>
      <a:fillRect/>
    </a:stretch>
  </p:blipFill>
  <p:spPr>
    <a:xfrm>
      <a:off x="10800000" y="200000"/>  <!-- Top-right position -->
      <a:ext cx="800000" cy="600000"/>   <!-- Logo dimensions -->
    </a:xfrm>
    <a:prstGeom prst="rect">
      <a:avLst/>
    </a:prstGeom>
  </p:spPr>
</p:pic>
```

### Adding Image Relationship

在 `ppt/slides/_rels/slideN.xml.rels` 中：

```xml
<Relationship Id="rIdLogo" 
  Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/image" 
  Target="../media/logo.png"/>
```

---

## 连接线

### Straight Connector

```xml
<p:cxnSp>
  <p:nvCxnSpPr>
    <p:cNvPr id="15" name="Straight Connector 14"/>
    <p:cNvCxnSpPr>
      <a:cxnSpLocks/>
    </p:cNvCxnSpPr>
    <p:nvPr/>
  </p:nvCxnSpPr>
  <p:spPr>
    <a:xfrm>
      <a:off x="500000" y="2500000"/>
      <a:ext cx="5000000" cy="0"/>  <!-- Horizontal line -->
    </a:xfrm>
    <a:prstGeom prst="line">
      <a:avLst/>
    </a:prstGeom>
    <a:ln w="12700">
      <a:solidFill>
        <a:srgbClr val="E67E22"/>
      </a:solidFill>
    </a:ln>
  </p:spPr>
</p:cxnSp>
```

### Dashed Line

```xml
<p:spPr>
  <a:xfrm>
    <a:off x="500000" y="4500000"/>
    <a:ext cx="5000000" cy="0"/>
  </a:xfrm>
  <a:prstGeom prst="line">
    <a:avLst/>
  </a:prstGeom>
  <a:ln w="12700">
    <a:solidFill>
      <a:srgbClr val="E67E22"/>
    </a:solidFill>
    <a:prstDash val="dash"/>  <!-- Dashed style -->
  </a:ln>
</p:spPr>
```

---

## 单位换算

| Unit | EMUs per unit |
|------|---------------|
| 1 inch | 914400 |
| 1 cm | 360000 |
| 1 point | 12700 |
| 1 pixel (96 DPI) | 9525 |

### Common Slide Dimensions (16:9)

- Width: 12192000 EMUs (13.333 inches)
- Height: 6858000 EMUs (7.5 inches)

### Typical Element Positions

| Element | X Position | Y Position |
|---------|------------|------------|
| Logo (top-right) | 10800000 | 200000 |
| Title | 342583 | 286603 |
| Subtitle | 402591 | 1767390 |
| Footer | 342583 | 6435334 |
