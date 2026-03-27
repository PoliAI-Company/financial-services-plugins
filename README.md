# Claude for Financial Services 插件

这些插件可将 Claude 变成金融服务领域的专业助手，覆盖投资银行、股票研究、私募股权和财富管理。为 [Claude Cowork](https://claude.com/product/cowork) 打造，也兼容 [Claude Code](https://claude.com/product/claude-code)。

## 为什么使用插件

Cowork 让你设定目标，由 Claude 交付完整且专业的成果。插件让你更进一步，你可以告诉 Claude 你的机构如何做分析、应从哪些数据源取数、如何处理关键工作流，以及要开放哪些斜杠命令，这样你的团队就能得到更优且更一致的结果。

每个插件都为特定的金融服务工作流打包了技能、连接器、斜杠命令和子代理。开箱即用时，它们就为 Claude 在该岗位上的协作能力提供了强有力的起点。真正的价值来自你按公司实际情况进行定制，你的模型、模板和流程，都可以融入其中，让 Claude 像是专为你的团队打造的一样工作。

## 什么是 Claude for Financial Services？

Claude for Financial Services 是基于 Claude for Enterprise 构建的一套完整解决方案，具备面向金融分析的专门能力。它将 Claude 连接到金融从业者日常使用的数据源和工具，免去在多个浏览器标签页之间来回切换的麻烦，并通过改进来源核验来降低人工收集数据带来的错误风险。

## 端到端工作流

这些插件不只是零散工具的集合，它们支持覆盖研究、分析、建模和产出创建的完整工作流：

- **研究到报告**：从 MCP 提供方拉取实时数据，分析财报结果，并生成可直接发布的股票研究报告，全部在同一个会话中完成
- **电子表格分析**：构建可比公司分析、DCF 模型和 LBO 模型，输出为功能完整的 Excel 工作簿，包含实时公式、敏感性分析表和行业标准格式
- **金融建模**：基于 SEC 文件填充三表模型，结合同行数据交叉核对假设，并对情景进行压力测试，同时内置蓝色、黑色、绿色的配色规范
- **交易材料**：起草 CIM、teaser 和 process letter，然后基于你公司品牌化的 PowerPoint 模板生成 pitch deck 幻灯片和 strip profile
- **从组合到汇报**：筛选机会、执行尽调清单、编写 IC memo，并追踪投资组合 KPI，从数据顺畅走到最终交付物

每条工作流都会把上游数据源（通过 MCP）连接到下游产出（Excel、PowerPoint、Word），让你从提出问题直接走到成品交付，无需反复切换上下文。

## 插件市场

先从 **financial analysis** 开始，这是核心插件，提供共享建模工具和全部 MCP 数据连接器。然后再按工作流需要添加各个职能专用插件，以增强 Claude 的能力。

| 插件 | 类型 | 作用方式 | 连接器 |
|--------|------|-------------|------------|
| **[financial analysis](./financial-analysis)** | 核心插件（先安装） | 构建 comps、DCF 模型、LBO 模型和三表财务模型。检查演示材料质量并创建可复用的 PPT 模板。提供共享基础能力和全部数据连接器。 | Daloopa, Morningstar, S&P Global, FactSet, Moody's, MT Newswires, Aiera, LSEG, PitchBook, Chronograph, Egnyte |
| **[investment banking](./investment-banking)** | 附加插件 | 起草 CIM、teaser 和 process letter。构建买方名单、运行并购模型、创建 strip profile，并按里程碑追踪进行中的交易。 | — |
| **[equity research](./equity-research)** | 附加插件 | 撰写财报更新和首次覆盖报告。维护投资逻辑，追踪催化剂，起草晨报，并筛选新想法。 | — |
| **[private equity](./private-equity)** | 附加插件 | 挖掘和筛选交易，执行尽调清单，分析单位经济模型和回报，撰写 IC memo，并监控被投公司的 KPI。 | — |
| **[wealth management](./wealth-management)** | 附加插件 | 为客户会议做准备，制定财务规划，再平衡投资组合，生成客户报告，并识别税损收割机会。 | — |

**41 个技能，38 个命令，11 个 MCP 集成**

你可以直接在 Cowork 中安装这些插件，也可以在 GitHub 上浏览完整集合，或者自己构建插件。

### 合作伙伴构建的插件

这些插件由我们的数据合作伙伴构建和维护，可将他们的金融数据与分析能力直接带入 Claude 工作流。

| 插件 | 合作伙伴 | 作用方式 |
|--------|---------|-------------|
| **[LSEG](./partner-built/lseg)** | [LSEG](https://www.lseg.com/) | 使用 LSEG 的金融数据和分析能力，对债券定价、分析收益率曲线、评估外汇套息交易、进行期权估值，并构建宏观仪表板。包含 8 个命令，覆盖固定收益、外汇、股票和宏观分析。 |
| **[S&P Global](./partner-built/spglobal)** | [S&P Global](https://www.spglobal.com/) | 基于 S&P Capital IQ 数据生成公司 tearsheet、财报前瞻和融资摘要。支持多种受众类型，包括股票研究、投资银行/并购、企业发展和销售团队。 |

## 快速开始

### Cowork

在 [claude.com/plugins](https://claude.com/plugins/) 安装插件。

### Claude Code

```bash
# 添加市场源
claude plugin marketplace add anthropics/financial-services-plugins

# 先安装核心插件（必需）
claude plugin install financial-analysis@financial-services-plugins

# 然后按需添加职能专用插件
claude plugin install investment-banking@financial-services-plugins
claude plugin install equity-research@financial-services-plugins
claude plugin install private-equity@financial-services-plugins
claude plugin install wealth-management@financial-services-plugins
```

安装完成后，插件会自动激活。相关技能会在适用时自动触发，斜杠命令也会在你的会话中可用：

```bash
/comps [company]                # 可比公司分析
/dcf [company]                  # DCF 估值模型
/earnings [company] [quarter]   # 财报后更新报告
/one-pager [company]            # 单页公司简介
/ic-memo [project name]         # 投资委员会备忘录
/source [criteria]              # 交易挖掘
/client-review [client]         # 客户会议准备
```

## 插件如何工作

每个插件都遵循相同的结构：

```
plugin-name/
├── .claude-plugin/plugin.json   # 清单文件
├── .mcp.json                    # 工具连接
├── commands/                    # 你显式调用的斜杠命令
└── skills/                      # Claude 自动调用的领域知识
```

- **技能** 编码了 Claude 交付专业级金融工作所需的领域专长、最佳实践和分步工作流。相关时，Claude 会自动调用它们。
- **命令** 是你主动触发的显式操作，例如 `/comps`、`/earnings`、`/ic-memo`。
- **连接器** 通过 [MCP servers](https://modelcontextprotocol.io/) 将 Claude 连接到你的工作流所依赖的外部数据源，包括金融数据终端、研究平台、文档管理系统等。

每个组件都基于文件实现，使用 markdown 和 JSON，无需代码、基础设施或构建步骤。

## MCP 集成

所有连接器都集中在 **financial analysis** 核心插件中，并由所有附加插件共享。

| 提供方 | URL |
|----------|-----|
| [Daloopa](https://www.daloopa.com/) | `https://mcp.daloopa.com/server/mcp` |
| [Morningstar](https://www.morningstar.com/) | `https://mcp.morningstar.com/mcp` |
| [S&P Global](https://www.spglobal.com/) | `https://kfinance.kensho.com/integrations/mcp` |
| [FactSet](https://www.factset.com/) | `https://mcp.factset.com/mcp` |
| [Moody's](https://www.moodys.com/) | `https://api.moodys.com/genai-ready-data/m1/mcp` |
| [MT Newswires](https://www.mtnewswires.com/) | `https://vast-mcp.blueskyapi.com/mtnewswires` |
| [Aiera](https://www.aiera.com/) | `https://mcp-pub.aiera.com` |
| [LSEG](https://www.lseg.com/) | `https://api.analytics.lseg.com/lfa/mcp` |
| [PitchBook](https://pitchbook.com/) | `https://premium.mcp.pitchbook.com/mcp` |
| [Chronograph](https://www.chronograph.pe/) | `https://ai.chronograph.pe/mcp` |
| [Egnyte](https://www.egnyte.com/) | `https://mcp-server.egnyte.com/mcp` |

> 使用 MCP 可能需要相应提供方的订阅或 API key。

## 如何把它们变成你的版本

这些插件只是起点。按照你公司实际的工作方式来定制之后，它们会有更高的价值：

- **替换连接器**：编辑 `.mcp.json`，指向你具体使用的数据提供方和内部工具。
- **加入公司语境**：把你的术语、交易流程和格式标准写入技能文件，让 Claude 理解你的业务环境。
- **带入你的模板**：使用 `/ppt-template` 教会 Claude 你公司品牌化的 PowerPoint 布局，让每份演示材料都符合你的风格指南。
- **调整工作流**：修改技能说明，使之匹配你团队真实的分析方式，而不是教科书里的标准流程。
- **构建新插件**：按照上述结构，为我们尚未覆盖的工作流创建插件。

随着团队不断构建和共享插件，Claude 会逐渐成为跨职能专家。你定义的语境会被嵌入到每一次相关交互中，让管理者把更少时间花在流程执行上，把更多时间放在流程优化上。

## 贡献

插件本质上就是 markdown 文件。Fork 这个仓库，完成修改后提交 PR。若要新增技能或插件，请包含：

- 一个 `SKILL.md`，清楚写明触发条件和工作流步骤
- 如果需要由用户调用，在 `commands/` 中提供对应命令
- 如果新增了能力，更新插件清单文件

## 许可证

[Apache License 2.0](./LICENSE)

## 免责声明

这些插件用于辅助金融工作流，但不构成金融或投资建议。请始终由合格的金融专业人士核验相关结论。任何 AI 生成的分析，在被用于金融或投资决策之前，都应由金融专业人士审阅。
