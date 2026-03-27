# 任务 4：图表生成 - 详细工作流

本文档提供执行 initiating-coverage skill 中 Task 4（Chart Generation）的逐步说明。

## 任务概览

**目的**：为报告生成 25-35 张专业财务图表。

**前置条件**：⚠️ 开始前验证
- **必需**：Task 1 的公司研究
  - 公司历史、里程碑（用于 timeline charts）
  - 管理团队、组织结构（用于 org charts）
  - 产品组合（用于 product charts）
  - 客户细分（用于 customer charts）
  - 竞争格局（用于 competitive positioning charts）
  - TAM analysis（用于 market size charts）
- **必需**：Task 2 的财务模型
  - Revenue by product / geography 数据
  - Margin trends
  - Scenario comparison data
- **必需**：Task 3 的估值分析
  - DCF sensitivity table
  - Comparable companies data
  - Valuation ranges
- **必需**：外部市场数据
  - 历史股价数据（Yahoo Finance、Bloomberg）
  - 历史估值倍数（chart 34 可选）

**⚠️ CRITICAL: DO NOT START THIS TASK UNLESS TASKS 1, 2, AND 3 ARE COMPLETE**

本任务依赖前三项任务的产出。若缺少这些输入，将无法生成完整图表。

**如果 TASKS 1、2、3 中任一项未完成**：立即停止，并告知用户需要先完成哪些任务。具体要求：
- Task 1：公司研究文档（支持 9 张图）
- Task 2：包含全部 6 个标签页的财务模型（支持 8 张图）
- Task 3：已将估值标签页加入模型（支持 6 张图）
- 外部数据访问（支持 2 张图）

不要创建占位图表，也不要因缺数据而跳过任何图表。

**输出**：25-35 个专业图表文件（PNG/JPG，300 DPI）

---

## 输入验证

**开始前 - 检查全部前置条件：**

### Task 1 验证（Company Research）
- [ ] Task 1 complete?（公司研究文档存在）
- [ ] 已记录 company history and milestones?（charts 05, 06）
- [ ] 已描述 management team and org structure?（chart 07）
- [ ] 已整理 product portfolio?（chart 08）
- [ ] 已分析 customer segmentation?（chart 09）
- [ ] 已绘制 competitive landscape?（charts 16, 17, 18）
- [ ] 已完成 TAM sizing?（chart 15）

### Task 2 验证（Financial Model）
- [ ] Task 2 complete?（财务模型 Excel 文件存在）
- [ ] Revenue by product breakdown 可用？（chart 03 ⭐）
- [ ] Revenue by geography breakdown 可用？（chart 04 ⭐）
- [ ] Historical + projected financials 完整？（charts 02, 10, 11, 12）
- [ ] Scenario analysis（Bull/Base/Bear）完整？（chart 14）
- [ ] Operating metrics 可用？（chart 13）

### Task 3 验证（Valuation）
- [ ] Task 3 complete?（模型中已加入 valuation tabs）
- [ ] DCF sensitivity matrix 存在？（chart 28 ⭐）
- [ ] DCF calculation details 可用？（chart 29）
- [ ] Comparable companies data 已收集？（charts 30, 31）
- [ ] 已计算 valuation ranges？（chart 32 ⭐）

### 外部数据验证
- [ ] 可以访问历史股价数据？（chart 01）
- [ ] 可以访问历史估值数据？（chart 34，可选）

**IF ANY VERIFICATION FAILS：**
- 缺少 Task 1 → 先完成 Task 1（Company Research）
- 缺少 Task 2 → 先完成 Task 2（Financial Modeling）
- 缺少 Task 3 → 先完成 Task 3（Valuation Analysis）
- 缺少外部数据 → 先从 Yahoo Finance、Bloomberg 或类似来源获取

---

## 图表要求：25 张必做 + 10 张可选

**IMPORTANT**：Task 5（Report Assembly）会将**所有已创建的图表**嵌入最终报告。报告要求高视觉密度，平均每 200-300 词一张图，因此必须覆盖充分。

### 4 张必做图表（不可省略）⭐

以下 4 张图是必须存在的关键可视化：

1. **chart_03**：Revenue by Product/Segment - Stacked Area Chart ⭐
2. **chart_04**：Revenue by Geography - Stacked Bar Chart ⭐
3. **chart_28**：DCF Sensitivity Analysis - 2-Way Heatmap ⭐
4. **chart_32**：Valuation Football Field - Horizontal Bar Chart ⭐

### 25 张必做图表（完整集合）

必须创建以下 25 张图，每张在 Task 5 中都有明确用途：

**Investment Summary Section（1 张）：**
- chart_01: Stock Price Performance（12-24 months）

**Financial Performance Section（6 张）：**
- chart_02: Revenue Growth Trajectory
- chart_03: Revenue by Product - Stacked Area ⭐ MANDATORY
- chart_04: Revenue by Geography - Stacked Bar ⭐ MANDATORY
- chart_10: Gross Margin Evolution
- chart_11: EBITDA Margin Progression
- chart_12: Free Cash Flow Trend

**Company 101 Section（7 张）：**
- chart_05: Company Overview/Timeline
- chart_06: Key Milestones Timeline
- chart_07: Organizational Structure
- chart_08: Product Portfolio Overview
- chart_09: Customer Segmentation
- chart_15: Market Size Evolution (TAM)
- chart_16: Competitive Positioning Matrix

**Competitive & Market Section（2 张）：**
- chart_17: Market Share Breakdown
- chart_18: Competitive Benchmarking

**Scenario Analysis Section（2 张）：**
- chart_13: Operating Metrics Dashboard
- chart_14: Scenario Comparison (Bull/Base/Bear)

**Valuation Section（7 张）：**
- chart_28: DCF Sensitivity Heatmap ⭐ MANDATORY
- chart_29: DCF Valuation Waterfall
- chart_30: Trading Comps Scatter Plot
- chart_31: Peer Multiples Comparison
- chart_32: Valuation Football Field ⭐ MANDATORY
- chart_33: Price Target Scenarios
- chart_34: Historical Valuation Multiples

**合计：25 张必做图表**

### 10 张可选图表（用于达到 30-35 张）

为了提高视觉密度和叙事能力，可额外增加：

- chart_19: Customer Acquisition Trends
- chart_20: Unit Economics Evolution
- chart_21: Product Roadmap Timeline
- chart_22: Geographic Expansion Map
- chart_23: R&D Investment Trends
- chart_24: Sales & Marketing Efficiency
- chart_25: Working Capital Trends
- chart_26: Debt Maturity Schedule
- chart_27: Ownership Structure
- chart_35: Analyst Price Target Distribution

**总范围：25-35 张图（25 张必做 + 0-10 张可选）**

---

## 必做图表的数据来源映射

### 来自 Task 1（Company Research）- 9 张图
- chart_05: Company Overview → Task 1: Company Overview section
- chart_06: Key Milestones → Task 1: Company History section
- chart_07: Org Structure → Task 1: Management Team section
- chart_08: Product Portfolio → Task 1: Products & Services section
- chart_09: Customer Segmentation → Task 1: Customers & Go-to-Market section
- chart_15: Market Size Evolution → Task 1: Market Opportunity（TAM）section
- chart_16: Competitive Positioning → Task 1: Competitive Landscape section
- chart_17: Market Share → Task 1: Competitive Landscape section
- chart_18: Competitive Benchmarking → Task 1: Competitive Landscape section

### 来自 Task 2（Financial Model）- 8 张图
- chart_02: Revenue Growth → Income Statement tab（Revenue row）
- chart_03: Revenue by Product ⭐ → Revenue Model tab（Product breakdown）
- chart_04: Revenue by Geography ⭐ → Revenue Model tab（Geography breakdown）
- chart_10: Gross Margin → Income Statement tab（Gross Profit / Revenue）
- chart_11: EBITDA Margin → Income Statement tab（EBITDA / Revenue）
- chart_12: Free Cash Flow → Cash Flow Statement tab（CFO - CapEx）
- chart_13: Operating Metrics → Multiple tabs（Income Statement, Cash Flow）
- chart_14: Scenario Comparison → Scenarios tab（Bull/Base/Bear）

### 来自 Task 3（Valuation）- 6 张图
- chart_28: DCF Sensitivity ⭐ → Sensitivity Analysis tab
- chart_29: DCF Waterfall → DCF tab（Enterprise Value components）
- chart_30: Trading Comps Scatter → Comparable Companies tab
- chart_31: Peer Multiples → Comparable Companies tab
- chart_32: Valuation Football Field ⭐ → Valuation Summary tab
- chart_33: Price Target Scenarios → Valuation Summary tab（或由 scenarios 计算）

### 来自外部来源 - 2 张图
- chart_01: Stock Price Performance → Yahoo Finance、Bloomberg、Alpha Vantage
- chart_34: Historical Valuation Multiples → Yahoo Finance、Bloomberg（历史 P/E、EV/EBITDA）

**IMPORTANT**：创建全部 25 张必做图，必须同时具备 Tasks 1、2、3 和外部数据。

---

## 分步图表生成工作流

### 第 1 步：设置环境

**安装需要的库：**
```bash
pip install matplotlib seaborn pandas numpy plotly
```

**创建 Python 脚本头部：**
```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np
from matplotlib.patches import Rectangle
import warnings
warnings.filterwarnings('ignore')

# Set global style
plt.style.use('seaborn-v0_8-darkgrid')
sns.set_palette("husl")

# Global settings
DPI = 300
FIGURE_WIDTH = 10
FIGURE_HEIGHT = 6
TITLE_FONT_SIZE = 14
AXIS_FONT_SIZE = 12
LABEL_FONT_SIZE = 10
```

### 第 2 步：从模型和估值中提取数据

#### A. 提取 Revenue Data
```python
# Revenue by Product (from Task 2 model)
years = [2020, 2021, 2022, 2023, 2024, 2025, 2026, 2027, 2028, 2029]

# Extract from Excel or define manually from model
product_a = [100, 120, 145, 175, 210, 252, 302, 363, 435, 522]
product_b = [80, 95, 115, 138, 165, 198, 238, 285, 342, 411]
product_c = [50, 62, 78, 98, 122, 153, 191, 239, 299, 374]
product_d = [30, 38, 48, 61, 77, 97, 122, 153, 191, 239]

# Revenue by Geography
north_america = [150, 180, 220, 265, 320, 384, 461, 553, 664, 797]
europe = [80, 95, 115, 140, 170, 204, 245, 294, 353, 423]
asia_pacific = [40, 50, 63, 80, 101, 127, 159, 199, 249, 311]
rest_of_world = [20, 25, 32, 40, 51, 64, 80, 100, 125, 156]
```

#### B. 提取 Margin Data
```python
# Margin evolution
gross_margin = [58.0, 59.2, 60.5, 61.8, 63.0, 64.5, 66.0, 67.0, 67.5, 68.0]
ebitda_margin = [12.0, 15.5, 18.8, 22.0, 25.0, 28.0, 30.5, 32.0, 33.0, 34.0]
fcf_margin = [8.0, 11.0, 14.5, 18.0, 21.0, 24.0, 26.5, 28.0, 29.0, 30.0]
```

#### C. 提取 DCF Sensitivity Data
```python
# DCF Sensitivity (from Task 3 valuation)
wacc_values = [7.0, 8.0, 9.0, 10.0, 11.0, 12.0]
terminal_growth = [1.5, 2.0, 2.5, 3.0, 3.5]

# Price per share matrix (rows = WACC, columns = terminal growth)
dcf_sensitivity = np.array([
    [66, 71, 76, 82, 89],
    [58, 62, 67, 72, 78],
    [52, 55, 59, 63, 68],
    [47, 50, 53, 56, 60],
    [42, 45, 48, 51, 54],
    [39, 41, 44, 46, 49]
])
```

#### D. 提取 Valuation Ranges
```python
# Valuation Football Field (from Task 3)
valuation_methods = ['DCF Analysis', 'Trading Comps\n(NTM)', 'Precedent\nTransactions']
valuation_low = [48, 45, 52]
valuation_high = [62, 57, 66]
current_price = 50
target_price = 55
```

### 第 3 步：创建 Mandatory Charts

#### Chart 1: Revenue by Product - Stacked Area ⭐ MANDATORY
```python
def create_revenue_by_product_chart():
    """Create revenue by product stacked area chart"""

    fig, ax = plt.subplots(figsize=(10, 6))

    # Create stacked area chart
    ax.stackplot(years, product_a, product_b, product_c, product_d,
                 labels=['Product A', 'Product B', 'Product C', 'Product D'],
                 colors=['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728'],
                 alpha=0.8)

    # Formatting
    ax.set_xlabel('Year', fontsize=12, fontweight='bold')
    ax.set_ylabel('Revenue ($M)', fontsize=12, fontweight='bold')
    ax.set_title('Figure 3 - Revenue by Product/Segment (2020-2029E)',
                 fontsize=14, fontweight='bold', pad=20)

    # Legend
    ax.legend(loc='upper left', frameon=False, fontsize=10)

    # Grid
    ax.grid(axis='y', alpha=0.3, linestyle='--')
    ax.set_axisbelow(True)

    # Remove top and right spines
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)

    # Add vertical line to separate historical from projected
    ax.axvline(x=2024, color='gray', linestyle='--', linewidth=1, alpha=0.5)
    ax.text(2024.2, ax.get_ylim()[1]*0.95, 'Projected →',
            fontsize=9, color='gray', ha='left')

    # Source line
    fig.text(0.12, 0.02, 'Source: Company data, [Firm] estimates',
             fontsize=9, style='italic', color='gray')

    # Save
    plt.tight_layout()
    plt.savefig('chart_03_revenue_by_product_stacked_area.png',
                dpi=300, bbox_inches='tight', facecolor='white')
    plt.close()
    print("✓ Created: chart_03_revenue_by_product_stacked_area.png")

create_revenue_by_product_chart()
```

#### Chart 2: Revenue by Geography - Stacked Bar ⭐ MANDATORY
```python
def create_revenue_by_geography_chart():
    """Create revenue by geography stacked bar chart"""

    years_labels = ['2020', '2021', '2022', '2023', '2024',
                    '2025E', '2026E', '2027E', '2028E', '2029E']

    fig, ax = plt.subplots(figsize=(10, 6))

    # Create stacked bar chart
    width = 0.6
    x = np.arange(len(years_labels))

    p1 = ax.bar(x, north_america, width, label='North America', color='#1f77b4')
    p2 = ax.bar(x, europe, width, bottom=north_america,
                label='Europe', color='#ff7f0e')
    p3 = ax.bar(x, asia_pacific, width,
                bottom=np.array(north_america) + np.array(europe),
                label='Asia-Pacific', color='#2ca02c')
    p4 = ax.bar(x, rest_of_world, width,
                bottom=np.array(north_america) + np.array(europe) + np.array(asia_pacific),
                label='Rest of World', color='#d62728')

    # Formatting
    ax.set_xlabel('Year', fontsize=12, fontweight='bold')
    ax.set_ylabel('Revenue ($M)', fontsize=12, fontweight='bold')
    ax.set_title('Figure 4 - Revenue by Geography (2020-2029E)',
                 fontsize=14, fontweight='bold', pad=20)
    ax.set_xticks(x)
    ax.set_xticklabels(years_labels, rotation=45, ha='right')

    # Legend
    ax.legend(loc='upper left', frameon=False, fontsize=10)

    # Grid
    ax.grid(axis='y', alpha=0.3, linestyle='--')
    ax.set_axisbelow(True)

    # Remove top and right spines
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)

    # Source line
    fig.text(0.12, 0.02, 'Source: Company data, [Firm] estimates',
             fontsize=9, style='italic', color='gray')

    # Save
    plt.tight_layout()
    plt.savefig('chart_04_revenue_by_geography_stacked_bar.png',
                dpi=300, bbox_inches='tight', facecolor='white')
    plt.close()
    print("✓ Created: chart_04_revenue_by_geography_stacked_bar.png")

create_revenue_by_geography_chart()
```

#### Chart 3: DCF Sensitivity - Heatmap ⭐ MANDATORY
```python
def create_dcf_sensitivity_heatmap():
    """Create DCF sensitivity analysis heatmap"""

    # Create DataFrame
    df = pd.DataFrame(dcf_sensitivity,
                      index=[f'{w}%' for w in wacc_values],
                      columns=[f'{g}%' for g in terminal_growth])

    fig, ax = plt.subplots(figsize=(8, 6))

    # Create heatmap
    sns.heatmap(df, annot=True, fmt='d', cmap='RdYlGn',
                cbar_kws={'label': 'Price per Share ($)'},
                linewidths=0.5, linecolor='white',
                ax=ax, vmin=35, vmax=95)

    # Formatting
    ax.set_xlabel('Terminal Growth Rate', fontsize=12, fontweight='bold')
    ax.set_ylabel('WACC', fontsize=12, fontweight='bold')
    ax.set_title('Figure 28 - DCF Sensitivity Analysis ($/share)',
                 fontsize=14, fontweight='bold', pad=20)

    # Rotate y-axis labels
    plt.yticks(rotation=0)

    # Source line
    fig.text(0.12, 0.02, 'Source: [Firm] estimates',
             fontsize=9, style='italic', color='gray')

    # Save
    plt.tight_layout()
    plt.savefig('chart_28_dcf_sensitivity_heatmap.png',
                dpi=300, bbox_inches='tight', facecolor='white')
    plt.close()
    print("✓ Created: chart_28_dcf_sensitivity_heatmap.png")

create_dcf_sensitivity_heatmap()
```

#### Chart 4: Valuation Football Field ⭐ MANDATORY
```python
def create_valuation_football_field():
    """Create valuation football field chart"""

    fig, ax = plt.subplots(figsize=(10, 5))

    # Create horizontal bars
    y_positions = np.arange(len(valuation_methods))
    colors = ['#1f77b4', '#ff7f0e', '#2ca02c']

    for i, (method, low, high, color) in enumerate(
            zip(valuation_methods, valuation_low, valuation_high, colors)):
        ax.barh(i, high - low, left=low, height=0.6,
                color=color, alpha=0.7, label=method)

        # Add value labels at ends
        ax.text(low - 1, i, f'${low}', va='center', ha='right', fontsize=10)
        ax.text(high + 1, i, f'${high}', va='center', ha='left', fontsize=10)

    # Add current price line
    ax.axvline(x=current_price, color='red', linestyle='--', linewidth=2,
               label=f'Current: ${current_price}', alpha=0.7)

    # Add target price line
    ax.axvline(x=target_price, color='black', linestyle='-', linewidth=2,
               label=f'Target: ${target_price}')

    # Formatting
    ax.set_yticks(y_positions)
    ax.set_yticklabels(valuation_methods, fontsize=11)
    ax.set_xlabel('Price Per Share ($)', fontsize=12, fontweight='bold')
    ax.set_title('Figure 32 - Valuation Football Field',
                 fontsize=14, fontweight='bold', pad=20)

    # Set x-axis limits
    ax.set_xlim(40, 70)

    # Remove spines
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    ax.spines['left'].set_visible(False)

    # Grid
    ax.grid(axis='x', alpha=0.3, linestyle='--')
    ax.set_axisbelow(True)

    # Legend
    ax.legend(loc='upper right', frameon=False, fontsize=9)

    # Source line
    fig.text(0.12, 0.02, 'Source: [Firm] estimates',
             fontsize=9, style='italic', color='gray')

    # Save
    plt.tight_layout()
    plt.savefig('chart_32_valuation_football_field.png',
                dpi=300, bbox_inches='tight', facecolor='white')
    plt.close()
    print("✓ Created: chart_32_valuation_football_field.png")

create_valuation_football_field()
```

### 第 4 步：创建其余必做图表（Charts 1-34）

必须完成 25 张 required charts 中的其余图表，每张在 Task 5 中都有明确用途。

#### Investment Summary（1 张）
```python
# chart_01: Stock Price Performance (12-24 months)
# - Line chart showing stock price over time vs. market index
# - Used on Page 1 of final report
```

#### Financial Performance（除 chart_03 和 chart_04 外，还需 5 张）
```python
# chart_02: Revenue Growth Trajectory
# chart_10: Gross Margin Evolution
# chart_11: EBITDA Margin Progression
# chart_12: Free Cash Flow Trend
# chart_14: Scenario Comparison (Bull/Base/Bear)
```

#### Company 101 Section（7 张）
```python
# chart_05: Company Overview/Timeline
# chart_06: Key Milestones Timeline
# chart_07: Organizational Structure
# chart_08: Product Portfolio Overview
# chart_09: Customer Segmentation
# chart_15: Market Size Evolution (TAM)
# chart_16: Competitive Positioning Matrix
```

#### Competitive & Market（2 张）
```python
# chart_17: Market Share Breakdown
# chart_18: Competitive Benchmarking
```

#### Scenario Analysis（1 张）
```python
# chart_13: Operating Metrics Dashboard
```

#### Valuation Section（除 chart_28 和 chart_32 外，还需 6 张）
```python
# chart_29: DCF Valuation Waterfall
# chart_30: Trading Comps Scatter Plot
# chart_31: Peer Multiples Comparison
# chart_33: Price Target Scenarios
# chart_34: Historical Valuation Multiples
```

**所有图表统一要求：**
- 300 DPI resolution
- Professional color scheme
- 清晰的 labels、legends 和 titles
- Figure 编号，例如 "Figure 5 - Company Timeline"
- 底部 source citations

### 第 4B 步：创建 Optional Charts（总数达到 26-35）

**可选**：额外增加 1-10 张图，提升视觉密度：

```python
# chart_19: Customer Acquisition Trends
# chart_20: Unit Economics Evolution
# chart_21: Product Roadmap Timeline
# chart_22: Geographic Expansion Map
# chart_23: R&D Investment Trends
# chart_24: Sales & Marketing Efficiency
# chart_25: Working Capital Trends
# chart_26: Debt Maturity Schedule
# chart_27: Ownership Structure
# chart_35: Analyst Price Target Distribution
```

这些 optional charts 有助于提升视觉叙事，并帮助达到 Task 5 所要求的 "每 200-300 词一张图" 的密度目标。

### 第 5 步：创建 Chart Index

创建一个文本文件，列出全部图表：

```python
def create_chart_index():
    """Create index of all charts"""

    # 25 REQUIRED CHARTS
    required_charts = [
        "chart_01_stock_price_performance.png - Stock Price Performance (12-24M)",
        "chart_02_revenue_growth_trajectory.png - Revenue Growth Trajectory",
        "chart_03_revenue_by_product_stacked_area.png - Revenue by Product [MANDATORY]",
        "chart_04_revenue_by_geography_stacked_bar.png - Revenue by Geography [MANDATORY]",
        "chart_05_company_overview.png - Company Overview/Timeline",
        "chart_06_key_milestones_timeline.png - Key Milestones Timeline",
        "chart_07_organizational_structure.png - Organizational Structure",
        "chart_08_product_portfolio.png - Product Portfolio Overview",
        "chart_09_customer_segmentation.png - Customer Segmentation",
        "chart_10_gross_margin_evolution.png - Gross Margin Evolution",
        "chart_11_ebitda_margin_progression.png - EBITDA Margin Progression",
        "chart_12_free_cash_flow_trend.png - Free Cash Flow Trend",
        "chart_13_operating_metrics_dashboard.png - Operating Metrics Dashboard",
        "chart_14_scenario_comparison.png - Scenario Comparison (Bull/Base/Bear)",
        "chart_15_market_size_evolution.png - Market Size Evolution (TAM)",
        "chart_16_competitive_positioning.png - Competitive Positioning Matrix",
        "chart_17_market_share.png - Market Share Breakdown",
        "chart_18_competitive_benchmarking.png - Competitive Benchmarking",
        "chart_28_dcf_sensitivity_heatmap.png - DCF Sensitivity Heatmap [MANDATORY]",
        "chart_29_dcf_waterfall.png - DCF Valuation Waterfall",
        "chart_30_trading_comps_scatter.png - Trading Comps Scatter Plot",
        "chart_31_peer_multiples_comparison.png - Peer Multiples Comparison",
        "chart_32_valuation_football_field.png - Valuation Football Field [MANDATORY]",
        "chart_33_price_target_scenarios.png - Price Target Scenarios",
        "chart_34_historical_valuation_multiples.png - Historical Valuation Multiples",
    ]

    # 10 OPTIONAL CHARTS (for 26-35 range)
    optional_charts = [
        "chart_19_customer_acquisition_trends.png - Customer Acquisition Trends [OPTIONAL]",
        "chart_20_unit_economics_evolution.png - Unit Economics Evolution [OPTIONAL]",
        "chart_21_product_roadmap_timeline.png - Product Roadmap Timeline [OPTIONAL]",
        "chart_22_geographic_expansion_map.png - Geographic Expansion Map [OPTIONAL]",
        "chart_23_rd_investment_trends.png - R&D Investment Trends [OPTIONAL]",
        "chart_24_sales_marketing_efficiency.png - Sales & Marketing Efficiency [OPTIONAL]",
        "chart_25_working_capital_trends.png - Working Capital Trends [OPTIONAL]",
        "chart_26_debt_maturity_schedule.png - Debt Maturity Schedule [OPTIONAL]",
        "chart_27_ownership_structure.png - Ownership Structure [OPTIONAL]",
        "chart_35_analyst_price_targets.png - Analyst Price Target Distribution [OPTIONAL]",
    ]

    with open('chart_index.txt', 'w') as f:
        f.write("CHART INDEX FOR [COMPANY] EQUITY RESEARCH REPORT\n")
        f.write("=" * 60 + "\n\n")

        f.write("4 MANDATORY CHARTS (Must be present):\n")
        f.write("- chart_03: Revenue by Product (Stacked Area) ⭐\n")
        f.write("- chart_04: Revenue by Geography (Stacked Bar) ⭐\n")
        f.write("- chart_28: DCF Sensitivity (Heatmap) ⭐\n")
        f.write("- chart_32: Valuation Football Field ⭐\n\n")

        f.write("25 REQUIRED CHARTS:\n")
        for chart in required_charts:
            f.write(f"  {chart}\n")

        f.write("\n10 OPTIONAL CHARTS (for 26-35 total):\n")
        for chart in optional_charts:
            f.write(f"  {chart}\n")

        f.write("\n" + "=" * 60 + "\n")
        f.write("NOTE: Task 5 will embed ALL charts created (25-35) throughout\n")
        f.write("the report for visual density (1 chart every 200-300 words).\n")

    print("✓ Created: chart_index.txt")

create_chart_index()
```

### 第 6 步：质量检查

**运行验证：**

```python
import os

def verify_charts():
    """Verify all charts were created successfully"""

    mandatory_charts = [
        'chart_03_revenue_by_product_stacked_area.png',
        'chart_04_revenue_by_geography_stacked_bar.png',
        'chart_28_dcf_sensitivity_heatmap.png',
        'chart_32_valuation_football_field.png'
    ]

    print("\n" + "="*60)
    print("CHART GENERATION VERIFICATION")
    print("="*60)

    # Check mandatory charts
    print("\n1. MANDATORY CHARTS:")
    all_mandatory_present = True
    for chart in mandatory_charts:
        if os.path.exists(chart):
            size = os.path.getsize(chart) / 1024  # KB
            print(f"   ✓ {chart} ({size:.1f} KB)")
        else:
            print(f"   ✗ MISSING: {chart}")
            all_mandatory_present = False

    # Count total charts
    chart_files = [f for f in os.listdir('.') if f.startswith('chart_') and f.endswith('.png')]
    print(f"\n2. TOTAL CHARTS: {len(chart_files)}")
    print(f"   Target: 25-35 charts")
    print(f"   Status: {'✓ PASS' if 25 <= len(chart_files) <= 35 else '⚠ WARNING'}")

    # Check file sizes (should be > 50KB for 300 DPI)
    print("\n3. FILE SIZE CHECK:")
    small_files = []
    for chart in chart_files[:5]:  # Sample first 5
        size = os.path.getsize(chart) / 1024
        if size < 50:
            small_files.append(chart)
        print(f"   {chart}: {size:.1f} KB")

    if small_files:
        print(f"   ⚠ WARNING: {len(small_files)} files may be low resolution")
    else:
        print(f"   ✓ All sampled files have adequate size")

    # Final verdict
    print("\n" + "="*60)
    if all_mandatory_present and 25 <= len(chart_files) <= 35:
        print("✓ VERIFICATION PASSED - Ready for Task 5")
    else:
        print("✗ VERIFICATION FAILED - Review missing charts")
    print("="*60 + "\n")

verify_charts()
```

---

## 质量标准

### Visual Quality
- [ ] 高分辨率（至少 300 DPI）
- [ ] 专业配色方案，全套图风格一致
- [ ] 文字清晰可读（字号不小于 9pt）
- [ ] 比例恰当，无拉伸变形
- [ ] 无明显像素化或图像瑕疵

### Data Accuracy
- [ ] 数据与源文件一致（financial model 和 valuation）
- [ ] 单位和标签正确，$ millions、百分比等
- [ ] 坐标范围和比例合适
- [ ] 不同图表的时间周期一致
- [ ] 计算已核验

### Formatting Quality
- [ ] 所有图表风格一致
- [ ] Figure 编号正确且连续
- [ ] 标题和说明清晰
- [ ] 每张图都有 source citation
- [ ] 外观专业

### Completeness
- [ ] 4 张 mandatory charts 均已创建
- [ ] 总图表数为 25-35 张
- [ ] 文件命名规范，chart_01、chart_02 等
- [ ] Chart index 已创建
- [ ] 可直接嵌入 Word

---

## 图表类型参考

### 各图表类型适用场景

**Line Charts**：时间序列趋势，revenue、margins、stock price

**Stacked Area**：Revenue by product ⭐、market size composition

**Stacked Bar**：Revenue by geography ⭐、quarterly breakdowns

**Heatmap**：DCF sensitivity ⭐、correlation matrices

**Horizontal Bar**：Valuation football field ⭐、peer rankings

**Waterfall**：Revenue bridges、margin analysis、DCF build-up

**Scatter/Bubble**：Growth vs. valuation、competitive positioning

**2×2 Matrix**：Competitive positioning、product portfolio

---

## 文件命名规范

**始终使用以下格式：**
```
chart_[NUMBER]_[DESCRIPTION].png

示例：
chart_01_stock_price_performance.png
chart_03_revenue_by_product_stacked_area.png
chart_28_dcf_sensitivity_heatmap.png
```

**按报告中的位置顺序编号**，而不是按创建顺序。

---

## 常见图表生成问题

### Issue 1: 分辨率低
**Problem**：图表看起来有明显像素感
**Solution**：确保 `plt.savefig()` 中设置 `dpi=300`

### Issue 2: 文字被截断
**Problem**：标签或标题在边缘被截断
**Solution**：在 `plt.savefig()` 中使用 `bbox_inches='tight'`

### Issue 3: 配色不专业
**Problem**：颜色看起来不够专业
**Solution**：使用现成的调色板，如 Tableau10，或自定义 corporate colors

### Issue 4: 标签重叠
**Problem**：坐标轴标签互相重叠
**Solution**：旋转标签，例如 `rotation=45`，或减小字号

### Issue 5: 白边过多
**Problem**：图表四周留白太多
**Solution**：保存前使用 `plt.tight_layout()`

---

## 成功标准

成功的 chart package 应满足：
1. **包含全部 4 张 mandatory charts** ⭐
2. **至少创建 25 张 required charts**
3. **可选增加 1-10 张图，达到 26-35 张**
4. 全部图表风格一致且专业
5. 分辨率达到 300 DPI，可供印刷
6. 每张图都有清晰标签、图例和标题
7. 每张图都有 figure number 和 source citation
8. 可直接嵌入 Word
9. 覆盖全部关键财务指标和分析主题
10. 能与文字分析形成互补的视觉叙事
11. 数据准确且可回溯到 source data
12. 全部图表打包入 zip，并附 chart index

**Remember**：Task 5 会把全部已创建图表嵌入最终报告，用于提高视觉密度。

---

## 输出文件

完成 Task 4 后，交付物包括：

**25 个 REQUIRED Chart Files（至少）：**
1. chart_01_stock_price_performance.png
2. chart_02_revenue_growth_trajectory.png
3. chart_03_revenue_by_product_stacked_area.png ⭐ MANDATORY
4. chart_04_revenue_by_geography_stacked_bar.png ⭐ MANDATORY
5. chart_05_company_overview.png
6. chart_06_key_milestones_timeline.png
7. chart_07_organizational_structure.png
8. chart_08_product_portfolio.png
9. chart_09_customer_segmentation.png
10. chart_10_gross_margin_evolution.png
11. chart_11_ebitda_margin_progression.png
12. chart_12_free_cash_flow_trend.png
13. chart_13_operating_metrics_dashboard.png
14. chart_14_scenario_comparison.png
15. chart_15_market_size_evolution.png
16. chart_16_competitive_positioning.png
17. chart_17_market_share.png
18. chart_18_competitive_benchmarking.png
19-27. *为 optional charts 预留*
28. chart_28_dcf_sensitivity_heatmap.png ⭐ MANDATORY
29. chart_29_dcf_waterfall.png
30. chart_30_trading_comps_scatter.png
31. chart_31_peer_multiples_comparison.png
32. chart_32_valuation_football_field.png ⭐ MANDATORY
33. chart_33_price_target_scenarios.png
34. chart_34_historical_valuation_multiples.png
35. *为 optional chart 预留*

**10 个 OPTIONAL Chart Files（用于达到 26-35 总数）：**
- chart_19 through chart_27, chart_35（如创建）

**Chart Index（1 个文本文件）：**
- chart_index.txt（列出全部图表、描述和分类）

**所有图表文件必须：**
- 300 DPI 分辨率（印刷质量）
- 宽度 6-10 英寸（适合嵌入 Word）
- 白色背景（专业外观）
- PNG 格式（无损）
- 可立即嵌入 Word

**最后一步：打包全部图表**

创建 zip 文件，包含全部图表和 chart index：

```
[Company]_Charts_[Date].zip
├── chart_01_stock_price_performance.png
├── chart_02_revenue_growth_trajectory.png
├── chart_03_revenue_by_product_stacked_area.png ⭐
├── chart_04_revenue_by_geography_stacked_bar.png ⭐
├── chart_05_company_overview.png
├── ... (all 25-35 chart files)
├── chart_28_dcf_sensitivity_heatmap.png ⭐
├── chart_32_valuation_football_field.png ⭐
├── chart_34_historical_valuation_multiples.png
└── chart_index.txt
```

**示例**：`Tesla_Charts_2024-10-28.zip`

**为什么这很重要**：Task 5 会把全部图表嵌入最终报告。报告要求高视觉密度，因此每张图都有实际用途，要么服务于特定分析部分，要么用于视觉叙事与页面填充。
- 验证全部 25-35 张图都已存在
- 为 Task 5（Report Assembly）准备图表

---

## 下一步

完成 Task 4 后，zip 文件将被用于：
- **Task 5 (Report Assembly)**：解压图表，并将全部图表嵌入最终 DOCX 报告的合适位置

其中 4 张 mandatory charts 对报告中的估值和财务分析部分尤其关键。
