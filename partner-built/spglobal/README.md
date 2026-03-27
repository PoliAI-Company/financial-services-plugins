# S&P Global 插件

这个插件通过一组预构建 skills，把 S&P Global 的金融数据和分析能力直接带入你的 AI 工作流。它面向希望基于权威 S&P Global 数据开展 AI 辅助研究、分析和文档生成的金融专业人士。

这些 skills 建立在开放标准，也就是 MCP 之上，并设计为可跨 AI 平台和代理框架工作。虽然该插件遵循 Claude Cowork 标准，但所有 skills 以及底层数据层本身都与平台无关。如果你想在别的环境中使用这些 skills，完全可以。

我们知道每家机构都有自己的需求。这些 skills 只是帮你更快做出成品的起点。我们鼓励你根据自己公司的流程、模板和数据需求，对提示词、输出和工作流进行调整。

本插件中的 skills 按现状提供。生成的输出和数据不保证完全正确。**务必对 LLM 生成的结果进行人工校验。**

## 包含的 Skills

### Tearsheets
**需要**：订阅 [S&P Global LLM-ready API](https://www.marketplace.spglobal.com/en/solutions/kensho-llm-ready-api-%28a156fe9f-5564-4f60-a624-95d8645dc98f%29)

将 S&P Capital IQ 的实时数据填充到格式化的 1 到 2 页公司 tearsheet Word 文档中。支持四种受众类型，每种都针对不同使用场景优化：
* Equity Research，面向买方和卖方分析师的投资逻辑快照
* Investment Banking / M&A，交易语境下的公司画像
* Corporate Development，面向内部战略团队的并购标的画像
* Sales / Business Development，面向商业团队的客户会前准备材料

**示例提示词**：`Generate a business development tearsheet for Palantir.`

### Industry Transaction Summaries
**需要**：订阅 [S&P Global LLM-ready API](https://www.marketplace.spglobal.com/en/solutions/kensho-llm-ready-api-%28a156fe9f-5564-4f60-a624-95d8645dc98f%29)

基于 S&P Capital IQ 交易数据，总结某个行业或特定公司的近期并购和交易活动。适合做市场图谱、pitch 准备和竞争情报。

**示例提示词**：`Summarize recent transactions in the data infrastructure space`

### Earnings Previews
**需要**：订阅 [S&P Global LLM-ready API](https://www.marketplace.spglobal.com/en/solutions/kensho-llm-ready-api-%28a156fe9f-5564-4f60-a624-95d8645dc98f%29)

为即将发布的财报生成结构化预览，包括一致预期、近期指引、分析师情绪和关键关注点，全部基于 S&P Capital IQ 数据。

**示例提示词**：`Give me an earnings preview for Salesforce.`

## 如何使用
插件和 skills 需要能够访问 S&P Global 数据，支持方式包括订阅 [Capital IQ Pro](https://www.spglobal.com/market-intelligence/en/solutions/products/sp-capital-iq-pro) 或 [S&P Global LLM-ready API](https://www.marketplace.spglobal.com/en/solutions/kensho-llm-ready-api-%28a156fe9f-5564-4f60-a624-95d8645dc98f%29)。

LLM-ready API 可以通过其 MCP 服务器轻松集成到 Claude 或其他应用中。按 [这些步骤](docs.kensho.com/llmreadyapi/mcp/third-party/claude) 完成设置。

### 在 Cowork 中使用
你需要付费 Claude 计划，比如 Pro、Max、Team 或 Enterprise，以及适用于 macOS 或 Windows 的 Claude Desktop 应用。

1. 打开 Claude Desktop，进入 **Cowork** 标签
1. 点击 **Customize with Plugins**
1. 在 Browse Plugins 中选择 **Personal**
1. 点击 **plus sign “+”** 添加插件
1. 按提示使用你的 S&P Global 凭证完成认证

安装完成后，相关 skill 会自动激活，你只需要用自然语言描述需求。你也可以在聊天中输入 `/` 来查看可用命令，并显式调用特定 skill。

如果你想让插件更贴合你所在机构的工作流、模板或术语，可以在查看已安装插件时点击 **Customize**。我们鼓励这样做，默认配置只是起点，不是唯一做法。

### 在 Claude Desktop 中使用单独 skill
如果不安装完整插件，而是在 Claude Desktop 中单独安装 skill：

1. 打开 **Settings**
1. 进入 **Capabilities → Skills**
1. 点击 **Add**
1. 上传本仓库中的 skill 文件

上传后，这些 skills 会立刻在你的 Claude Desktop 会话中可用。你可以按需安装一个，也可以安装多个。

### 在 Claude Code 中使用单独 skill

按照 [Claude Code documentation](https://code.claude.com/docs/en/discover-plugins#add-from-github) 中的说明操作。

### 其他平台
这个仓库中的 skills 都是 Markdown 文件。任何支持自定义指令、系统提示词或知识文件上传的 AI 平台都可以使用它们。不同平台的接入方式可能不同，但原则相同，也就是把 skill 内容加载进去，让模型将其作为持续上下文。

**ChatGPT**：可以把 skill 内容粘贴到 Custom Instructions，也就是 Settings → Customize ChatGPT；上传到 Project 中作为知识文件；或者加入 Custom GPT 的配置中。自定义指令会全局生效，Project 级文件则只在特定工作流范围内提供上下文。

**Microsoft Copilot**：可根据你的 Copilot 配置，也就是 M365 Copilot、Copilot Studio 等，把 skill 内容粘贴到自定义提示词或系统指令中。通过 Copilot Studio 进行的企业部署还支持直接上传知识源。

**其他平台**：如果你的平台支持系统提示词或持久化指令层，就把 skill Markdown 粘贴进去。如果支持基于文件的知识检索，就上传 skill 文件。这些 skills 是纯 Markdown，不需要特殊格式或额外工具。

## 接下来会有什么
我们正在持续构建更多覆盖金融工作流的 skills 和插件。非常欢迎你告诉我们，哪些能力对你最有价值。若有一般问题、反馈或合作意向，请联系 [commercial@kensho.com](mailto:commercial@kensho.com)，或在本仓库中提交 issue。

# License

根据 Apache 2.0 License 授权。除非适用法律要求或书面约定，否则依据该许可分发的软件按 “AS IS” 基础提供，不附带任何明示或默示的担保或条件。许可证中的具体语言将约束相应权限和限制。

Copyright 2026-present Kensho Technologies, LLC. 当前日期以仓库最近一次提交的时间戳为准。
