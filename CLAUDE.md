# Financial Services 插件

这是一个面向金融服务专业人士的 Claude Cowork 插件市场。每个子目录都是一个独立插件。

## 仓库结构

```
├── investment-banking/  # 投资银行效率插件
```

## 插件结构

每个插件都遵循以下布局：
```
plugin-name/
├── .claude-plugin/plugin.json   # 插件清单（名称、描述、版本）
├── commands/                    # 斜杠命令（.md 文件）
├── skills/                      # 面向特定任务的知识文件
├── hooks/                       # 事件驱动自动化
├── mcp/                         # MCP 服务器集成
└── .claude/                     # 用户设置（*.local.md）
```

## 关键文件

- `marketplace.json`: 插件市场清单，注册所有插件及其源路径
- `plugin.json`: 插件元数据，包含名称、描述、版本和组件发现设置
- `commands/*.md`: 以 `/plugin:command-name` 调用的斜杠命令
- `skills/*/SKILL.md`: 面向特定任务的详细知识与工作流
- `*.local.md`: 用户专属配置（已被 git 忽略）
- `mcp-categories.json`: 在各插件之间共享的标准 MCP 分类定义

## 开发工作流

1. 直接编辑 markdown 文件，修改会立即生效
2. 使用 `/plugin:command-name` 语法测试命令
3. 当触发条件匹配时，技能会自动被调用
