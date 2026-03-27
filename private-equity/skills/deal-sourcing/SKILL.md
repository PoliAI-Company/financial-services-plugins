# 交易 sourcing

description: PE 交易 sourcing 工作流，发现目标公司、检查 CRM 中是否已有关系，并起草个性化创始人外联邮件。适用于寻找新交易、在某个行业中筛选公司，或联系创始人。触发词包括 "find companies"、"source deals"、"draft founder email"、"check if we've seen this company" 或 "outreach to founder"。

## 工作流

本技能遵循 3 步 sourcing 流程：

### 第 1 步：发现公司

根据用户标准调研并识别潜在目标公司：

- **行业 / 赛道聚焦**：询问用户关注的领域，例如 "B2B SaaS in healthcare"、"industrial services in the Southeast"
- **交易参数**：收入区间、EBITDA 区间、增长特征、地域、所有权类型，创始人持有、PE 支持、企业 carve-out
- **信息来源**：使用 web search 查找符合标准的公司，查看行业报告、会议参会名单、行业媒体和竞争格局
- **输出**：形成候选名单，包含公司名称、简介、估算收入 / 规模、所在地、创始人 / CEO 姓名、官网，以及为什么符合 thesis

### 第 2 步：CRM 检查

在外联前，先检查公司或创始人是否已经存在于机构 CRM 中：

- 在用户邮箱（Gmail）中搜索是否与该公司或创始人有过往来
- 在 Slack 中搜索内部是否提到过该目标，或是否有过往讨论
- 询问用户："Have you or your team had any prior contact with [Company]?"
- 标记任何已有关系、以前 pass 过的情况或已知背景
- **输出**：对每家公司标注为 "New"（无过往接触）、"Existing"（发现过往往来，附简述）或 "Previously Passed"（如有明确证据显示之前 pass 过）

### 第 3 步：起草创始人外联

为创始人 / CEO 起草个性化冷启动邮件：

- **语气**：专业但友好，不要过于正式，创始人更愿意回复真诚、简洁的外联
- **结构**：
  1. 简短介绍，你是谁，你所在的机构是谁，如未知，先向用户确认机构介绍
  2. 为什么这家公司引起你的关注，要引用具体点，如产品、市场地位、增长表现
  3. 你在寻找什么，是合作关系，不只是交易
  4. 柔和的邀约，"Would you be open to a brief conversation?"
- **个性化**：引用公司的具体产品、近期新闻或市场定位，不要使用泛模板
- **长度**：最多 4-6 句话，创始人通常很忙
- **语气匹配**：如果用户以前发过类似外联邮件，先研究其语气和风格。可以在 Gmail 的 sent 邮件里搜索 "reaching out"、"introduction"、"partnership" 等关键词寻找样例

### 邮件草稿指引

- 主题行要短且具体，引用公司或行业，不要写成 "Investment Opportunity"
- 首次接触不要带附件
- 要有清晰但低压的 CTA
- 如可用，直接在 Gmail 中起草，否则输出为文本供用户复制

## 示例互动

**User**: "Find me founder-owned industrial services companies in Texas doing $10-50M revenue"

**Assistant**:
1. 在网上搜索符合条件的 Texas industrial services 公司
2. 展示包含关键细节的 5-8 家公司 shortlist
3. 对每家公司检查 Gmail / Slack 中是否有过往联系
4. 为标记为 "New" 的公司起草个性化外联邮件
5. 在发送前展示草稿供用户审阅

## Important Notes

- 起草邮件前，始终先把 shortlist 给用户确认
- 未经用户明确批准，绝不发送邮件
- 如果用户的机构介绍或投资标准不明确，起草前先确认
- 质量优先于数量，5 个研究扎实的目标，胜过 20 个泛泛的名单
