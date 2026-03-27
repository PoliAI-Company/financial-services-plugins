# 投资银行插件

面向股票研究、估值分析、演示文稿和交易材料的投资银行效率工具。

## 功能

- **交易材料** - CIM、teaser、process letter 和 buyer list
- **演示材料** - Strip profile、使用品牌模板的 pitch deck
- **交易支持** - Merger model、deal tracking 和 data pack

## 安装

```bash
claude --plugin-dir /path/to/investment-banking
```

或者复制到你项目的 `.claude-plugin/` 目录中。

## Commands

| Command | 说明 |
|---------|------|
| `/one-pager [company]` | 用于 pitch book 的单页 strip profile |
| `/cim [company]` | 起草 Confidential Information Memorandum |
| `/teaser [company]` | 匿名单页公司 teaser |
| `/buyer-list [company]` | 战略与财务买方名单 |
| `/merger-model [deal]` | 增厚/摊薄并购分析 |
| `/process-letter [deal]` | 出价指引与流程往来函件 |
| `/deal-tracker` | 跟踪在执行交易、关键里程碑和行动事项 |

## Skills

### 交易材料
| Skill | 说明 |
|-------|------|
| **cim-builder** | 起草 Confidential Information Memorandum |
| **teaser** | 匿名单页公司 teaser |
| **process-letter** | 出价指引与流程往来函件 |
| **buyer-list** | 战略与财务买方名单 |
| **datapack-builder** | 基于 CIM 和申报文件构建 data pack |

### 演示材料
| Skill | 说明 |
|-------|------|
| **strip-profile** | 用于 pitch book 的高信息密度公司简介 |
| **pitch-deck** | 用数据填充 pitch deck 模板 |

### 交易支持
| Skill | 说明 |
|-------|------|
| **merger-model** | 增厚/摊薄并购分析 |
| **deal-tracker** | 跟踪在执行交易、关键里程碑和行动事项 |

## 示例工作流

### 单页 Strip Profile
```
/one-pager Target

# Generates:
# - Single-slide company profile using PPT template
# - 4 quadrants: Overview, Business, Financials, Ownership
# - Respects template margins and branding
```

### CIM 起草
```
/cim Target

# Generates:
# - Full CIM document with executive summary, business overview,
#   financial analysis, and market positioning
```

### Merger Model
```
/merger-model Acquirer acquiring Target

# Generates:
# - Accretion/dilution analysis
# - Sources and uses, pro forma financials
# - Sensitivity on purchase price and synergies
```
