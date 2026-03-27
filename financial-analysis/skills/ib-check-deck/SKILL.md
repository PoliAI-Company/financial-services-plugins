---
name: ib-check-deck
description: 投资银行演示材料质量检查器。审阅 pitch deck 或面向客户的演示文稿，检查：(1) 跨页数字一致性，(2) 数据与叙事是否对齐，(3) 是否符合 IB 标准的语言润色，(4) 视觉与格式质检。当用户要求 review、check、QC、proof 或在发送前做最终检查时使用，包括“check my numbers”“reconcile figures across slides”“is this client-ready”“what am I missing before I send this out”等。
---

# IB Deck 检查器

从四个维度对演示文稿做全面 QC。读完整份 deck，然后报告发现。

## 环境检查

该 skill 同时适用于 PowerPoint 插件和聊天环境。开始前先识别环境：

- **Add-in** — 从实时打开的 deck 中读取。
- **Chat** — 从上传的 `.pptx` 文件中读取。

这是只读和报告流程，不做编辑，因此两种环境下工作流相同。

## 工作流

### 读取 deck

提取每一页的文本，并记录每一行来自哪一页。每一条发现都需要页级归因，例如："$500M appears on slides 3 and 8, but slide 15 shows $485M"。30 页的 deck 太长，不适合只靠工作记忆处理。把提取出来的文本写入文件，让数字检查脚本进行处理。

脚本需要带有页标记的 markdown 风格输入。格式如下：

```
## Slide 1
[slide 1 text content]

## Slide 2
[slide 2 text content]
```

### 1. 数字一致性

对提取结果运行脚本：

```bash
python scripts/extract_numbers.py /tmp/deck_content.md --check
```

该脚本会归一化单位（$500M vs $500MM vs $500,000,000 → 同一个数字）、对数值分类（revenue、EBITDA、multiples、margins），并在同一指标类别在不同幻灯片出现冲突值时发出提示。这一部分最有可能抓到人工第五遍审阅时仍遗漏的问题。

除脚本标记内容外，还要验证：
- 计算是否正确（总和是否加总、百分比是否相加、增长率是否与端点一致）
- 单位风格是否一致，整份 deck 应统一使用 $M 或 $MM
- 时间口径是否一致，FY、LTM、季度需明确标注

### 2. 数据与叙事是否对齐

把论点与支撑它的数据对应起来。这类错误往往很隐蔽，有人改了第 7 页的图，却忘了第 4 页的叙述。

- 趋势表述（"declining margins"）是否与图表方向一致？
- 市场地位表述（"#1 player"）是否有 revenue 和 share 数据支持？
- 合理性，例如 "#1 in a $100B market" 却只有 $200M revenue，那只是 0.2% 份额，不会是 #1

### 3. 语言润色

IB deck 有固定语域。扫描任何破坏这种语域的表述：口语化用词（"pretty good"、"a lot of"）、缩写、感叹号、没有数字支撑的模糊量词，以及对同一概念使用不同术语。

参考 `references/ib-terminology.md` 获取替换模式。

### 4. 视觉与格式 QC

对每一页执行标准视觉验证。重点关注：缺失的图表来源、缺失的坐标轴标签、字体排版不一致、数字格式漂移（同一 deck 中出现 1,000 和 1K）、日期格式漂移、脚注和免责声明缺失。

视觉验证能发现文本提取无法发现的重叠、溢出和对比度问题。不要跳过。没有来源标注的图表，在文本 dump 中看起来与带有完整来源的图表没区别。

## 输出

使用 `references/report-format.md` 中的结构。按严重级别分类：

- **Critical** — 数字不一致、事实错误、数据与叙事冲突。这些会阻止面向客户交付。
- **Important** — 语言、缺失来源、术语漂移。应修复。
- **Minor** — 字号、间距、日期格式。属于润色层面。

优先列出 critical。如果没有，也要明确写出来，例如："no number inconsistencies found" 本身就是一条发现，而不是“没有内容可写”。
