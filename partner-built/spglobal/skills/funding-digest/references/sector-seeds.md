# 行业种子公司参考

当用户只给出行业而没有指定公司时，使用这些种子列表来启动公司覆盖范围构建。这些只是起点，后续一定要通过 `get_competitors_from_identifiers` 扩展，并用 `get_info_from_identifiers` 做校验。

> **下面所有种子都已经用 S&P Global 的标识符体系做过验证。** 如果某个种子解析失败，请先尝试括号中列出的别名，再决定是否丢弃。

## Technology / Software

### AI / Machine Learning
Seeds: OpenAI, Anthropic, Databricks, Scale AI, Cohere, Hugging Face, Mistral AI, xAI, Perplexity AI, Runway ML (alias: "Runway AI, Inc."), Together AI (alias: "Together Computer, Inc."), Character.ai (alias: "Character Technologies, Inc."), Groq, Stability AI, Aleph Alpha, Magic AI

⚠️ **排除项，不要作为种子使用：**
- *Inflection AI*，核心团队已被 Microsoft 吸收，时间是 2024 年 3 月。历史融资轮仍存在，但不会再有新活动。
- *Adept AI*，大部分团队在 2024 年被 Amazon 吸收，同上。
- *DeepMind*，Alphabet 的子公司，没有独立融资轮。

### Cybersecurity
Seeds: CrowdStrike, Palo Alto Networks, Wiz, Snyk, SentinelOne, Abnormal Security, Netskope

### Cloud Infrastructure / DevTools
Seeds: Snowflake, HashiCorp, Datadog, Confluent, Vercel, Supabase, PlanetScale

### Fintech
Seeds: Stripe, Plaid, Brex, Ramp, Mercury, Affirm, Marqeta, Navan

### Vertical SaaS
Seeds: ServiceTitan, Toast, Procore, Veeva Systems, Blend Labs

## Healthcare / Life Sciences

### Biotech / Pharma
Seeds: Moderna, BioNTech, Recursion Pharmaceuticals, Tempus AI, Insitro, AbCellera

### Digital Health
Seeds: Teladoc, Hims & Hers, Ro, Noom, Color Health

⚠️ **排除项，不要作为种子使用：**
- *Cerebral*，仍在运营，但监管问题很多。只有当用户明确要求时再纳入。

### Medical Devices
Seeds: Intuitive Surgical, Butterfly Network, Outset Medical

⚠️ **排除项，不要作为种子使用：**
- *Shockwave Medical*，已于 2024 年 5 月被 Johnson & Johnson 收购。现在是子公司，没有独立融资轮。

## Energy / Climate

### Climate Tech
Seeds: Redwood Materials, Form Energy, Commonwealth Fusion, Sila Nanotechnologies, Climeworks

### Clean Energy
Seeds: Enphase Energy, First Solar, Rivian, QuantumScape, Sunnova

## Consumer

### E-Commerce / Marketplace
Seeds: Shopify, Faire, Whatnot, Fanatics

⚠️ **排除项，不要作为种子使用：**
- *Temu (PDD Holdings)*，PDD Holdings 是大型上市集团，其融资活动通过公开资本市场体现，而不是风险投资轮。

### Consumer Social / Media
Seeds: Discord, Reddit, Substack

⚠️ **排除项，不要作为种子使用：**
- *BeReal*，已于 2024 年 6 月被 Voodoo 收购，现为子公司。
- *Lemon8*，品牌名 “Lemon8” 在 S&P Global 中会解析到一家荷兰小公司 Lemon8 B.V.，**不是** ByteDance 的社交应用。ByteDance 旗下应用属于子公司，没有独立融资轮。不要使用。

## Industrials / Logistics

### Logistics / Supply Chain
Seeds: Flexport, Samsara, Project44, FourKites

⚠️ **排除项，不要作为种子使用：**
- *Convoy*，已于 2023 年 10 月停止运营。标识符仍可解析，也能看到历史融资轮，但不会再有新活动。

### Robotics / Automation
Seeds: Figure AI, Agility Robotics, Locus Robotics, Symbotic, Covariant

### Space / Aerospace
Seeds: SpaceX, Relativity Space, Rocket Lab, Planet Labs, Astra

## 标识符别名参考

一些知名品牌名称与 S&P Global 中的法定实体名称并不一致。如果品牌名在 `get_info_from_identifiers` 中返回空结果，请尝试下列别名：

| Brand Name | S&P Global Legal Name | company_id |
|---|---|---|
| Together AI | Together Computer, Inc. | C_1860042219 |
| Character.ai | Character Technologies, Inc. | C_1829047235 |
| Runway ML | Runway AI, Inc. | C_633706980 |
| Adept AI | Adept AI Labs Inc. | C_1780739313 |
| xAI | X.AI LLC | C_1863863313 |

> **提示：** 当品牌名失败时，先用法定名称再次尝试 `get_info_from_identifiers`。如果仍然失败，则该公司可能尚未被索引。最后再尝试直接使用 `company_id` 作为标识符。

## 说明

- 这些列表偏向美国公司。若需要做地域过滤，比如欧洲或亚洲，competitor expansion 这一步就尤其重要。
- 对于这里没有列出的细分行业，可以向用户索要 2 到 3 家示例公司作为种子。
- 始终验证种子是否仍然活跃且相关，因为公司会转型、并购或关闭。
- **刷新频率：** 这些种子应按季度复核，尤其是 AI 行业变化非常快，因为收购和新进入者很多。
- 被标记为子公司或已收购的种子，在 `get_info_from_identifiers` 中依然能解析，状态为 `Operating Subsidiary`，但会返回零融资轮。做 funding 查询时应直接跳过。
