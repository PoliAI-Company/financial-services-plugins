---
name: funding-digest
description: 生成一页精致的 PowerPoint 幻灯片，总结用户关注行业或公司中近期融资轮次和重要资本市场活动的关键结论。当用户要求 deal flow 摘要、每周回顾、融资 digest、交易 roundup 或资本市场 briefing 时使用。触发语包括：'deal flow digest'、'weekly funding recap'、'deal roundup'、'transaction summary this week'、'what happened in [sector] this week'、'capital markets update'，以及任何要求把近期融资活动整理成 briefing 幻灯片的请求。输出为专业单页 PPTX，包含关键结论、估值数据和 Capital IQ 交易链接。
---

**AI 免责声明，强制要求：**
你必须在 PowerPoint 页脚中包含以下免责声明文本。这不是可选项，缺少它就表示报告不完整：

> **"Analysis is AI-generated — please confirm all outputs"**

**页脚**，在生成幻灯片底部，以醒目的黄色横幅展示：`Analysis is AI-generated — please confirm all outputs`

---

# 每周 Deal Flow Digest

生成一页 **分析师级别的 PowerPoint 幻灯片**，总结用户所关注行业或公司中近期融资轮次的关键结论，并使用 S&P Global Capital IQ 数据。每笔交易都应链接回它在 Capital IQ 中的资料页，方便快速下钻。

## 适用场景

当用户提出以下类型需求时触发：
- “Give me a deal flow digest for this week”
- “Weekly funding recap for [sector]”
- “What deals closed in [sector/companies] recently?”
- “Transaction roundup” 或 “deal roundup”
- “Capital markets update for my coverage universe”
- “Summarize recent funding activity”
- 任何关于 deal、raises 或 rounds 的周期性 briefing 请求

## 嵌套 Skills

这个 skill 会生成单页 PPTX briefing：
- 在生成 PowerPoint 之前，先阅读 `/mnt/skills/public/pptx/SKILL.md`，以及其子参考 `pptxgenjs.md`

## 实体解析与工具稳健性

S&P Global 的标识符系统会把公司名称解析到法定实体。大多数情况下效果不错，但也有一些已知失败模式，会导致返回空结果。**在整个工作流中都应执行下面这些规则，避免静默数据缺失。**

### Rule 0，在查询融资前预校验所有标识符

**在** 调用任何融资工具之前，先把每个标识符跑一遍 `get_info_from_identifiers`。它成本最低，也最可靠。检查两件事：

1. **是否成功解析？** 如果某个标识符返回空结果或错误，说明该名字在 S&P Global 中不存在。尝试 `references/sector-seeds.md` 里的别名、法定实体名称，或者直接使用 `company_id`。
2. **`status` 字段是什么？**
   - `Operating`，可以安全查询融资轮
   - `Operating Subsidiary`，公司存在，但已被母公司持有，会返回 **零融资轮**。可以在 digest 中将其作为背景说明，比如 “acquired by [Parent]”，但不要对其做融资查询
   - 其他状态，比如 closed、inactive，表示公司已不再运营，可能有历史数据，但不会有新活动

**这一步单独的预校验能避免大部分空结果问题。** 把候选公司批量送入单次 `get_info_from_identifiers` 调用，然后先做分流。

### Rule 1，遇到空结果时绝不能直接相信

如果 `get_rounds_of_funding_from_identifiers` 对某家公司返回空结果，而你原本预期它应该有数据：
1. **尝试法定实体名称或 company_id。** 品牌名通常能用，但不是绝对。已知别名映射见 `references/sector-seeds.md`。典型模式是 “[Brand] AI” 对应 “[Legal Name], Inc.”。
2. **确认公司确实存在于 S&P 中。** 如果你跳过了 Rule 0，现在就调用 `get_info_from_identifiers(identifiers=["Company"])`。若它也返回空，说明该公司可能太早期，尚未被索引。

### Rule 2，子公司没有独立融资轮

那些是大公司事业部或全资子公司的公司，比如 DeepMind、GitHub、BeReal，会返回 **零融资轮**。它们的资本事件记录在母公司层面。

**识别方式：** `get_info_from_identifiers` 返回中的 `status` 会是 `Operating Subsidiary`。`references/sector-seeds.md` 也会用 ⚠️ 标记这些情况。对它们直接跳过融资查询。

### Rule 3，优先使用 `get_rounds_of_funding_from_identifiers`，而不是 `get_funding_summary_from_identifiers`

summary 工具更快，但可靠性更差。即便详细轮次存在，它也可能报错或返回不完整结果。应始终把详细轮次工具作为主数据源。summary 工具只能用于快速查看总融资额或轮次数，并且当结果偏低时，必须再用 detailed rounds 工具核对。

### Rule 4，谨慎分批并持续校验

当处理大公司池，也就是 50 家以上时，每批控制在 15 到 20 家。每跑完一批，都要检查哪些公司返回空结果，并在进入下一批之前，对这些公司执行 Rule 1 的 fallback 逻辑。

### Rule 5，`role` 参数至关重要

- `company_raising_funds`，表示 “X 融到了哪些轮次”，站在融资公司视角
- `company_investing_in_round_of_funding`，表示 “投资方 Y 投了哪些轮次”，站在投资方视角

如果用错角色，结果通常会静默返回空。做 deal flow digest 时，几乎总是应该用 `company_raising_funds`。只有在专门分析投资机构组合活动时，才使用 investor 角色。

### Rule 6，标识符解析大小写不敏感，但拼写敏感

S&P Global 对大小写处理宽松，比如 `openai` 和 `OpenAI` 都可以，但对拼写和标点非常严格。比如 `Character AI` 可能失败，而 `Character.ai` 成功。拿不准时，优先用 `company_id`，比如 `C_1829047235`，它一定能解析。

## 工作流

### Step 1，确定覆盖范围与时间区间

先确定 digest 要覆盖什么。有两种常见场景：

**回访用户，已有 watchlist：**
如果用户之前已经定义过要跟踪的行业或公司，就直接使用那份列表。可从对话历史里查找先前 watchlist。

**新用户：**
需要询问：

| Parameter | Default | Notes |
|-----------|---------|-------|
| **Sectors** | *(at least one)* | 例如 “AI, Fintech, Biotech” |
| **Specific companies** | Optional | 可作为行业级覆盖的补充 |
| **Time period** | Last 7 days | 比如 “This week”、"last 2 weeks"、"this month" |

根据时间区间精确计算 `start_date` 和 `end_date`。

### Step 2，构建公司池

对每个行业，用经过校验的 bootstrap 流程来建立公司池：

1. 从领域知识中选择 **seed companies**，见 `references/sector-seeds.md`
   - 特别留意种子文件中的 ⚠️ 警告和别名说明，有些知名公司是子公司、已被收购，或只能用特定法定名称解析
   - 对于已知别名不匹配的公司，种子文件里还提供了 `company_id`，在品牌名失败时可直接使用

2. **立刻预校验所有种子**，执行 Rule 0：
   ```
   get_info_from_identifiers(identifiers=[all_seeds_for_this_sector])
   ```
   把结果分成两类：
   - ✅ **Resolved & Operating**，也就是 `status = "Operating"`，可以继续做 competitor expansion
   - ❌ **Unresolved or Subsidiary**，需要尝试别名或法定名称；子公司只保留背景说明，但不做融资查询

3. **用 competitors 扩展范围**，只对 ✅ 解析成功的种子执行：
   ```
   get_competitors_from_identifiers(identifiers=[resolved_seeds], competitor_source="all")
   ```

4. **校验扩展后的公司池：**
   ```
   get_info_from_identifiers(identifiers=[new_competitors])
   ```
   同样按上述逻辑分流，再根据 `simple_industry` 过滤出与目标行业一致的公司，并剔除无法解析或属于子公司的名字。

如果用户直接给了具体公司，也要先做同样的预校验。即便是非常知名的品牌名，也不要跳过这一步。

公司池要控制在可管理规模，理想情况下每个行业保留 15 到 40 家 **已解析且处于 Operating 状态** 的公司。多行业 digest 总量可能到 50 到 100 家以上。

### Step 3，抓取融资轮次

对公司池中的所有公司执行：

```
get_rounds_of_funding_from_identifiers(
    identifiers=[batch],
    role="company_raising_funds",
    start_date="YYYY-MM-DD",
    end_date="YYYY-MM-DD"
)
```

公司池较大时，请按 15 到 20 家一批处理。

**每处理完一批，都要找出返回空结果的公司。** 对于那些你预期本应有活动的公司：
1. 用法定实体名称或替代标识符重试
2. 只有在所有 fallback 都失败后，才把它记为 “no data”

把成功结果中的所有 `transaction_id` 收集起来，再用以下工具补充详细融资轮信息：

```
get_rounds_of_funding_info_from_transaction_ids(
    transaction_ids=[all_funding_ids]
)
```

尽量一次性提交全部 transaction IDs，或至少分成少量批次，而不是逐笔调用。

**每个融资轮必须提取以下字段，这对幻灯片至关重要：**
- `transaction_id`，用于生成 Capital IQ deal link
- **Announcement date**，融资轮对外公布的日期
- **Close date**，融资轮正式完成的日期
- Amount raised
- **Pre-money valuation**，如有披露
- **Post-money valuation**，如有披露
- Lead investors
- Round type，比如 Series A、B、C
- Security terms
- Advisors
- Pricing trend，也就是 up-round、down-round 或 flat

> **日期是必填项。** 最终幻灯片中的交易表必须始终展示 announcement date 和 close date。若只有一个日期可用，就展示该日期，另一个写 `—`。

### Step 4，为重要交易补充公司背景

对参与重大交易的公司，比如大额融资轮、估值剧烈变化的公司，抓取简要公司描述：

```
get_company_summary_from_identifiers(identifiers=[notable_companies])
```

这样可以为叙事增加背景，比如 “The company, an AI infrastructure startup founded in 2021...”

### Step 5，识别亮点与趋势

在设计幻灯片前，先分析数据，找出真正的故事线：

**应标记为 “Notable” 的情况：**
- 融资轮 ≥ $100M
- Down rounds
- 新晋独角兽，post-money valuation 首次跨过 $1B
- 估值显著跳升，post-money 至少是上一轮已知估值的 2 倍
- Repeat raisers，也就是同一公司 6 个月内再次融资
- 异常庞大的投资人 syndicate

**需要识别的趋势：**
- 本周期总投放资本，相比常态是否偏高，如有历史数据
- 哪些子行业最热，按轮次数和融资额判断
- 轮次阶段分布，是早期还是后期主导
- 最活跃的投资人
- 地理集中度
- 估值趋势，也就是 pre-money valuations 正在收缩还是扩张

**选择 3 到 5 条 Key Takeaways：**
把最重要的信号提炼成 3 到 5 条简洁、硬朗、数据支撑充分的结论句。它们是整页幻灯片的中心。

### Step 6，生成公司 Logo

对于出现在 key takeaways 或 notable deals 中的公司，使用本地两层方案生成 logo。**不要使用 Clearbit**，它已弃用且经常失败。外部 logo CDN 往往需要 API key 或受网络限制阻断，因此使用本地方案。

#### Tier 1，`simple-icons` npm 包

`simple-icons` 打包了数千个高质量 SVG 品牌图标，可完全离线工作。需要配合 `sharp` 完成 SVG 到 PNG 的转换：

```bash
npm install simple-icons sharp
```

**查找策略：**

```javascript
const si = require('simple-icons');
const sharp = require('sharp');

// Find an icon by exact title match (case-insensitive)
function findSimpleIcon(companyName) {
    // Try exact match first
    for (const [key, val] of Object.entries(si)) {
        if (!key.startsWith('si') || !val || !val.title) continue;
        if (val.title.toLowerCase() === companyName.toLowerCase()) return val;
    }
    // Try without common suffixes (AI, Inc., Corp.)
    const stripped = companyName.replace(/\s*(AI|Inc\.?|Corp\.?|Ltd\.?)$/i, '').trim();
    if (stripped !== companyName) {
        for (const [key, val] of Object.entries(si)) {
            if (!key.startsWith('si') || !val || !val.title) continue;
            if (val.title.toLowerCase() === stripped.toLowerCase()) return val;
        }
    }
    return null;
}

// Convert SVG to PNG with the brand's official color
async function simpleIconToPng(icon, outputPath) {
    const coloredSvg = icon.svg.replace('<svg', `<svg fill="#${icon.hex}"`);
    await sharp(Buffer.from(coloredSvg))
        .resize(128, 128, { fit: 'contain', background: { r: 255, g: 255, b: 255, alpha: 0 } })
        .png()
        .toFile(outputPath);
}
```

**覆盖率：** 对典型 deal flow 公司，约能覆盖 43%，对大型科技品牌表现较好，对垂直细分或超早期公司较弱。

#### Tier 2，基于首字母的 `sharp` 回退方案

对于 `simple-icons` 找不到的公司，生成一个干净的首字母 logo：

```javascript
async function generateInitialLogo(companyName, outputPath) {
    const initial = companyName.charAt(0).toUpperCase();
    const svg = `
    <svg width="128" height="128" xmlns="http://www.w3.org/2000/svg">
        <circle cx="64" cy="64" r="64" fill="#BDBDBD"/>
        <text x="64" y="64" font-family="Arial, Helvetica, sans-serif"
              font-size="56" font-weight="bold" fill="#FFFFFF"
              text-anchor="middle" dominant-baseline="central">${initial}</text>
    </svg>`;
    await sharp(Buffer.from(svg)).png().toFile(outputPath);
}
```

#### 完整流程

```javascript
async function fetchLogo(companyName, outputDir) {
    const fileName = companyName.toLowerCase().replace(/[\s.]+/g, '-') + '.png';
    const outPath = path.join(outputDir, fileName);

    // Tier 1: Try simple-icons
    const icon = findSimpleIcon(companyName);
    if (icon) {
        await simpleIconToPng(icon, outPath);
        return { path: outPath, source: 'simple-icons' };
    }

    // Tier 2: Generate initial-based fallback
    await generateInitialLogo(companyName, outPath);
    return { path: outPath, source: 'initial-fallback' };
}
```

**Logo 使用规范：**
- 所有 logo 保存到 `/home/claude/logos/[company-name].png`
- 统一输出 128×128、透明底 PNG
- 幻灯片上展示高度控制在 0.35" 到 0.5"，它们只是视觉辅助，不是视觉中心
- 回退 logo 用灰色圆形背景，也就是 `BDBDBD`，白字，保持单色体系
- 不要随意混搭 logo 风格。如果大部分公司能解析出品牌图标，少量回退 logo 也应尽量自然融合

### Step 7，生成单页 PPTX

在创建幻灯片前，先阅读 `/mnt/skills/public/pptx/SKILL.md` 和 `/mnt/skills/public/pptx/pptxgenjs.md`。

使用 `pptxgenjs` 创建 **单页** PowerPoint。页面要信息密集但干净，感觉更像高层金融简报，而不是文字墙。

#### 幻灯片布局

下面的结构图保持不变：

```
┌─────────────────────────────────────────────────────────────┐
│  DEAL FLOW DIGEST                                           │
│  [Period] · [Sectors]                           [Date]      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐       │
│  │  $X.XB  │  │  N      │  │  $X.XB  │  │  $X.XB  │       │
│  │ Raised  │  │ Rounds  │  │ Avg Pre │  │ Largest │       │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘       │
│                                                             │
│  KEY TAKEAWAYS                                              │
│  ─────────────────────────────────────────────────          │
│  [Logo] Takeaway 1 text goes here...                        │
│  [Logo] Takeaway 2 text goes here...                        │
│  [Logo] Takeaway 3 text goes here...                        │
│  [Logo] Takeaway 4 text goes here...                        │
│                                                             │
│  TOP DEALS                                                  │
│  ┌──────────────────────────────────────────────────────────┐│
│  │Company│Type │Announced│Closed│Amount│Pre-$│Post-$│Lead│🔗││
│  │───────│─────│─────────│──────│──────│─────│──────│────│──││
│  │ ...   │ ... │  ...    │ ...  │ ...  │ ... │ ...  │... │🔗││
│  └──────────────────────────────────────────────────────────┘│
│                                                             │
│  [Footer: Deal Flow Digest · Sources: S&P Global Capital IQ]│
│  [Footer: AI Disclaimer]                                    │
└─────────────────────────────────────────────────────────────┘
```

#### 设计规范

**色彩哲学：** 极简，以黑白灰为主。只有在颜色本身能表达意义时才使用颜色，比如下轮融资用红色提示，亮眼正面指标用绿色提示，或公司 logo 本身。不要为了装饰而使用颜色。

其余配色、字体、Stat Cards、Key Takeaways、Top Deals Table、Deal Link Implementation、Table Centering、Footer、General color rules、Code Structure、QA 流程、结果呈现、错误处理和示例提示词等内容，按英文原文中的结构和约束执行。代码块与模板语法保持不变。

## 错误处理

### 实体解析失败
- 已知公司却返回空结果时，先看 `get_info_from_identifiers`，再尝试种子文件中的别名或直接使用 `company_id`
- 子公司，比如 DeepMind、GitHub、Instagram、WhatsApp、YouTube、BeReal，不应被当作 “no activity”，而应标注为已被收购或子公司
- 已停业公司不会再有新活动
- `get_funding_summary_from_identifiers` 出错或返回 0 时，应回退到 `get_rounds_of_funding_from_identifiers`
- 若 investor 视角查询结果为空，要检查是否把 `role` 参数写错

### 数据质量问题
- 若某行业在时间区间内没有融资活动，应明确写在幻灯片上，因为 “没有交易” 本身也是信息
- 若大多数交易没有 pre-money 或 post-money 估值，应在页脚说明数据限制，并将相应统计卡替换为其他指标
- 若 logo 获取失败，应使用首字母回退方案，保持视觉一致
- 若 notable deals 超过 6 笔，只展示前 6 笔，并加脚注说明有更多交易未展示
- 多行业大覆盖面场景下，应坚持批处理 API 调用
- 若交易 ID 不能生成有效 Capital IQ 链接，就省略该行链接单元格，不要放坏链
