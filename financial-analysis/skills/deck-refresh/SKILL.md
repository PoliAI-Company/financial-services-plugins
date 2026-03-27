---
name: deck-refresh
description: 用新数字更新演示文稿，包括季度滚动更新、业绩更新、comps 刷新和市场数据重置。当用户提出“update the deck with Q4 numbers”“refresh the comps”“roll this forward”“swap in the new earnings”“change all the $485M to $512M”等请求，或任何在不重建整份 deck 的前提下替换现有 deck 中数字的需求时使用。
---

# Deck 刷新

更新 deck 中的数字。deck 本身就是格式的唯一真源，你只改数值。

## 环境检查

该 skill 同时适用于 PowerPoint 插件和聊天环境。开始前先识别所处环境，因为编辑机制不同，但目标一致：

- **Add-in** — deck 已实时打开，直接编辑文字 run、表格单元格和图表数据。
- **Chat** — deck 是用户上传的文件；用新数值重生成受影响的幻灯片，并把结果写回文件。

无论哪种方式，都要做到最小改动，保留现有格式。

这是一个四阶段流程，第三阶段是审批关口。在用户看到计划之前，不要编辑。

## 第 1 阶段：获取数据

使用 `ask_user_question` 了解新数字将如何提供：

- **Pasted mapping** — 用户直接输入或粘贴类似 "revenue $485M → $512M, EBITDA $120M → $135M." 这种最清晰。
- **Uploaded Excel** — 有旧值/新值两列，或用户希望你提取的最新输出表。读取后，在信任数据前确认每一列的含义。
- **Just the new values** — 例如 "Q4 revenue was $512M, margins were 22%." 由你判断每个值替换什么。可以做，但在改动前必须确认映射。把 `$512M` 错映射到 revenue，而用户实际指的是 gross profit，是一种静默灾难。

还要询问**衍生数字**：如果 revenue 变了，用户是否希望同步重算增长率和占比，还是保持不变？很多 deck 某处写着 "+15% YoY"，现在可能已过时。是否修改这种值是用户该做的判断，不是你替他们决定。

## 第 2 阶段：通读并找全

读完整份 deck。对每个旧值，找出它出现的所有位置，包括那些表面看起来不一样的形式：

| 变体 | 示例 |
|---|---|
| Scale | `$485M`, `$0.485B`, `$485,000,000` |
| Precision | `$485M`, `$485.0M`, `~$485M` |
| Unit style | `$485M`, `$485MM`, `$485 million`, `485M` |
| Embedded | "revenue grew to $485M", "a $485M business", axis labels |

一份 deck 如果在第 3 页写 `$485M`，第 8 页图表坐标轴写 `485`，第 15 页脚注写 `$485.0 million`，那就是同一个数字的三个实例。简单查找替换会漏掉其中两个。你不能漏。

**数字容易藏身的位置：**
- 文本框
- 表格单元格
- 图表数据标签和坐标轴标签
- 图表源数据，也就是驱动柱状图或折线图的数值，不只是标签
- 脚注、来源行、小字说明
- 如果用户关心的话，还包括演讲者备注

建立一份清单：对每个旧值，记录它出现的所有位置、具体文本形式，以及将要变成什么。这份清单就是计划。

## 第 3 阶段：展示计划并获得批准

**这会对别人花了时间打磨的 deck 进行破坏性操作。** 在编辑任何内容前，先展示完整变更清单，并让它足够易读：

```
$485M → $512M (Revenue)
  Slide 3  — Title box: "Revenue grew to $485M"
  Slide 8  — Chart axis label: "485"
  Slide 15 — Footnote: "$485.0 million in FY24 revenue"

$120M → $135M (Adj. EBITDA)
  Slide 3  — Table cell
  Slide 11 — Body text: "$120M of Adj. EBITDA"

FLAGGED — possibly derived, not in your mapping:
  Slide 3  — "+15% YoY" (growth rate — stale if base year didn't change?)
  Slide 7  — "12% market share" (was this computed from $485M / market size?)
```

标记部分很重要。你不是在机械执行查找替换，而是在发现用户深夜容易忽略的二阶影响。如果映射是 `$485M → $512M`，而第 3 页旁边还有 `+15% YoY`，那个增长率现在大概率也错了。要标出来，不要默默修，也不要默默放过。

使用 `ask_user_question` 获取审批：按展示内容继续执行、继续但跳过标记项，或者先让他们修订映射。

## 第 4 阶段：执行、保留、汇报

针对每一项变更，只做实现目标所需的最小编辑。具体方式取决于环境：

- **Add-in** — 直接在实时 deck 中编辑具体的 run、单元格或图表 series。
- **Chat** — 用新数值重生成受影响的幻灯片，同时精确保留其他元素，然后写回文件。

无论哪种方式，标准都一样：

- **形状中的文本** — 改值，不改字体、字号、颜色和加粗状态。如果 `$485M` 在一句话里是 14pt 海军蓝粗体，那么 `$512M` 也必须是同样格式。
- **表格单元格** — 改单元格，不动表格其他部分。
- **图表数据** — 更新底层 series 值，让柱子或折线真正变化。只改标签不改数据，会得到一张说谎的图。

不要重设任何你没必要碰的格式。deck 现有风格默认就是正确的。你是外科医生，不是装修队。

完成后，报告实际结果：

```
Updated 11 values across 8 slides.

Changed:
  [the list from Phase 3, now past-tense]

Still flagged — did NOT change:
  Slide 3 — "+15% YoY" (derived; confirm separately)
  Slide 7 — "12% market share"
```

对每一页被编辑过的幻灯片执行标准视觉验证。某个数字可能从 `$485M` 变成 `$1,205M`，长度增加后就会溢出文本框，或者把表格列宽挤坏。要在用户发现前先发现。

## 你不做什么

- **不重建整页** — 如果某页叙事已经不适配新数字，例如写着 "margins compressed"，但现在利润率上升了，那么标记它，不要重写。
- **未获要求不重算** — 衍生数字是否修改由用户决定。第 1 阶段的问题就是为此设置的。
- **不改格式** — 如果 deck 使用 `$MM` 而用户映射写的是 `$M`，以 deck 风格为准，而不是映射风格。变的是数值，不是样式。
