# HTML 报告模板参考

把这个模板作为单公司财报前瞻 HTML 报告的基础。根据 Phases 1 到 5 收集到的研究结果，自定义其中的数据、图表和叙事内容。

## HTML 结构

报告是一个单文件、自包含 HTML，具备以下特征：
- 内嵌 CSS，不依赖外部样式表
- 通过 CDN 加载 Chart.js 以支持交互图表
- 通过 `@media print` 提供打印友好样式
- 在屏幕和打印场景下都可用
- 目标长度为 4 到 5 个打印页

## 完整模板

下面的代码块保持原样，保留模板语法、可见文本和结构：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Earnings Preview — [COMPANY] ([TICKER]) — [DATE]</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.7/dist/chart.umd.min.js" integrity="sha384-vsrfeLOOY6KuIYKDlmVH5UiBmgIdB1oEf7p01YgWHuqmOHfZr374+odEv96n9tNC" crossorigin="anonymous"></script>
  <script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-annotation@3.1.0/dist/chartjs-plugin-annotation.min.js" integrity="sha384-3N9GHhCtN3CQef6tNfqgZlv7sQLYIkcChN+uaTZ7xVdzKYp/SjBNPxa92+hM7EAY" crossorigin="anonymous"></script>
  <style>
    /* ── Reset & Base ── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { font-size: 15px; }
    body {
      font-family: 'Arial Narrow', Arial, sans-serif;
      color: #1a1a2e;
      background: #fff;
      line-height: 1.6;
    }
...
</html>
```

## Chart.js 实现说明

### Figure 2，Revenue & EPS Chart
- **类型：** 组合图，bar 加 line
- **柱状图：** 左轴显示季度收入
- **折线图：** 右轴显示稀释 EPS
- **标签：** 季度标识，例如 `Q1 FY24`
- 使用 8 个季度数据

### Figure 3，Margin Trend Chart
- **类型：** 双折线图
- **线条：** Gross margin 百分比 和 operating margin 百分比
- **Y 轴：** 百分比，保留 1 位小数

### Figure 3，Revenue Growth Chart
- **类型：** 条形图，并根据正负进行条件着色
- **绿色柱：** 正增长季度
- **红色柱：** 负增长季度
- **重要：** 只包含那些可以计算同比的季度，也就是当前季度和去年同期都存在于 `financials.csv` 中的季度。拿到 8 个季度原始数据后，通常只能得到 4 个同比柱，而不是 8 个。

### Figure 4，Business Segment Revenue
- 使用 HTML 表格，而不是图表
- 列为 Segment、Latest Q Rev、% of Total、y/y Change
- y/y Change 单元格使用 `pos` 和 `neg` 类控制颜色

### Figure 5，带财报日期标注的股价图
- **类型：** 带 annotation plugin 的折线图
- **数据：** 1 年日频收盘价
- **标注：** 在每个财报日期处画虚线
- **标签：** 季度名称加上财报后 1 日股价变动
- **颜色：** 正反应为绿，负反应为红
- **关键：** 在创建图表前必须先注册 annotation plugin

### Figure 7，竞争对手指数化表现图
- **类型：** 多折线图，全部 rebased 到 100
- **目标公司：** 使用实线且线宽更粗
- **竞争对手：** 使用更细的虚线

### Figure 8，LTM P/E Comparison Chart
- **类型：** 横向条形图
- **目标公司：** 用海军蓝高亮
- **竞争对手：** 用浅蓝色
- **排序：** 按 P/E 从高到低

### Figure 8，Competitor Comparison Table
- 使用 HTML 表格
- 目标公司行使用 `highlight-row`

## 格式约定

### 数字
- Revenue，若以 $B 展示保留 1 位小数，若以 $M 展示则不保留小数
- EPS 保留 2 位小数
- Margin 保留 1 位小数并加 `%`
- Growth rate 保留 1 位小数并带正负号
- Market cap 若以 $B 展示保留 1 位小数
- Stock price 保留 2 位小数
- P/E 保留 1 位小数并加 `x`

### 颜色编码
- 正值使用 `class="pos"`
- 负值使用 `class="neg"`
- 中性值使用 `class="neutral"`
- 目标公司行使用 `class="highlight-row"`

### 图表编号
- 所有 figure 依次编号
- Figures 1 到 8 放在第 3 到 5 页
- 每张图和表下方都要写来源行，比如 `Source: S&P Capital IQ`

### 超链接事实
- 报告正文中的每一个事实，无论是数字还是定性陈述，都必须包裹在 `<a href="#ref-N" class="data-ref">` 中
- `ref-N` 必须与附录中的某一行对应
- 这适用于叙事文字、bullet、表格单元格和 blockquote 中的事实
- 图表坐标轴标签和 tooltip 不需要超链接

### 附录
- **必须以** `<div class="ai-disclaimer">Analysis is AI-generated — please confirm all outputs</div>` **开头**
- 附录位于报告最后，在所有图表之后
- 固定 4 列：Ref #、Fact、Value、Source & Derivation
- 正文中的每一个数字都必须有可点击链接跳转到附录对应行
- 每一行都必须包含详细 source 与 derivation，而不是泛泛写 `S&P Capital IQ`
- 计算值必须展示完整公式，并让公式中所有数字都链接回各自的附录条目
- Kensho 结果必须带可点击原始 URL

### 样式规则
- **不要使用 emoji**
- 全文统一使用 Arial Narrow
- 管理层引文要以 `<blockquote>` 形式嵌入 executive thesis 中，不要单独设节标题
- 保持所有文字紧凑，目标 4 到 5 页，附录额外计算
