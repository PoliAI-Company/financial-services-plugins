---
name: skill-creator
description: 用于创建高质量 skill 的指南。当用户想创建新 skill，或更新现有 skill，以扩展 Claude 的专用知识、工作流或工具集成能力时使用。
license: Complete terms in LICENSE.txt
---

# Skill Creator

这个 skill 提供关于如何创建高质量 skill 的指导。

## 关于 Skills

Skills 是模块化、自包含的软件包，通过提供专门知识、工作流和工具来扩展 Claude 的能力。你可以把它们理解为面向特定领域或任务的“上手指南”。它们会把 Claude 从通用型代理转变为带有程序性知识的专用代理，而这些知识不可能由任何模型完全内化。

### Skills 提供什么

1. Specialized workflows - 针对特定领域的多步骤流程
2. Tool integrations - 处理特定文件格式或 API 的说明
3. Domain expertise - 公司特定知识、schema、业务逻辑
4. Bundled resources - 用于复杂和重复任务的脚本、参考资料和资源

## 核心原则

### 简洁最重要

上下文窗口是公共资源。Skills 要与 Claude 需要的其他内容共享上下文窗口，包括 system prompt、对话历史、其他 skills 的元数据，以及实际的用户请求。

**默认假设：Claude 已经很聪明。** 只添加 Claude 原本没有的上下文。对每一段信息都要质疑：“Claude 真的需要这段解释吗？”以及“这段话是否值得它占用的 token 成本？”

尽量用简明示例代替冗长解释。

### 设定合适的自由度

根据任务的脆弱性和变化程度，匹配说明的具体程度：

**高自由度（文本说明）**：当多种方法都有效、决策依赖上下文，或需要启发式判断时使用。

**中等自由度（带参数的伪代码或脚本）**：当存在推荐模式、允许一定变化，或行为受配置影响时使用。

**低自由度（具体脚本、参数较少）**：当操作脆弱且容易出错、一致性至关重要，或必须严格按特定顺序执行时使用。

把 Claude 想成在探索一条路径：两侧是悬崖的窄桥需要明确护栏，开放原野则允许多条路线。

### Skill 的结构

每个 skill 都由一个必需的 SKILL.md 文件和可选的打包资源组成：

```
skill-name/
├── SKILL.md (required)
│   ├── YAML frontmatter metadata (required)
│   │   ├── name: (required)
│   │   └── description: (required)
│   └── Markdown instructions (required)
└── Bundled Resources (optional)
    ├── scripts/          - Executable code (Python/Bash/etc.)
    ├── references/       - Documentation intended to be loaded into context as needed
    └── assets/           - Files used in output (templates, icons, fonts, etc.)
```

#### SKILL.md（必需）

每个 SKILL.md 包括：

- **Frontmatter**（YAML）：包含 `name` 和 `description` 字段。这两个字段是 Claude 判断何时触发该 skill 的唯一依据，因此必须清晰、完整地描述这个 skill 是什么，以及何时应该使用。
- **Body**（Markdown）：使用该 skill 的说明和指引。只有在 skill 触发之后才会被加载。

#### Bundled Resources（可选）

##### Scripts (`scripts/`)

用于需要确定性可靠性或会被反复重写任务的可执行代码（Python/Bash 等）。

- **何时加入**：当相同代码会被反复重写，或需要确定性可靠性时
- **示例**：`scripts/rotate_pdf.py` 用于 PDF 旋转任务
- **好处**：更省 token、更稳定，而且可能无需读入上下文就能执行
- **注意**：脚本在打补丁或适配环境时，Claude 仍然可能需要读取

##### References (`references/`)

作为参考资料的文档，应在需要时加载到上下文中，帮助 Claude 完成任务与思考。

- **何时加入**：当 Claude 在工作过程中需要参考文档时
- **示例**：`references/finance.md`、`references/mnda.md`、`references/policies.md`、`references/api_docs.md`
- **用途**：数据库 schema、API 文档、领域知识、公司政策、详细工作流指南
- **好处**：保持 SKILL.md 精简，只有在需要时才加载
- **最佳实践**：如果文件较大（>10k words），在 SKILL.md 中包含 grep 搜索模式
- **避免重复**：信息应当只存在于 SKILL.md 或 references 文件之一，不要两边都放。除非是真正核心的内容，否则详细资料更适合放入 references，这样既保持 SKILL.md 精简，也让信息可发现。

##### Assets (`assets/`)

不打算加载进上下文，而是供 Claude 在最终输出中使用的文件。

- **何时加入**：当 skill 需要在最终输出中使用某些文件时
- **示例**：`assets/logo.png`、`assets/slides.pptx`、`assets/frontend-template/`、`assets/font.ttf`
- **用途**：模板、图像、图标、样板代码、字体、需要复制或修改的示例文档
- **好处**：把输出资源与文档分开，Claude 可以使用这些文件而不用把它们读入上下文

#### 不要在 Skill 中加入什么

skill 只应包含直接支持其功能的必要文件。不要创建额外的文档或辅助文件，包括：

- README.md
- INSTALLATION_GUIDE.md
- QUICK_REFERENCE.md
- CHANGELOG.md
- 等等

skill 应只包含 AI 代理完成手头工作所需的信息。不应包含关于 skill 创建过程、安装测试流程、面向用户的文档等辅助背景，否则只会增加混乱和噪音。

## Progressive Disclosure 设计原则

Skills 使用三级加载机制，以高效管理上下文：

1. **Metadata（name + description）** - 总是在上下文中
2. **SKILL.md body** - skill 触发时加载
3. **Bundled resources** - Claude 需要时加载

保持 SKILL.md 正文只包含关键内容，并尽量低于 500 行，以减少上下文膨胀。当内容接近这个限制时，将内容拆分到其他文件，并且必须在 SKILL.md 中明确引用这些文件并说明何时读取。

## Skill 创建流程

Skill 创建包括以下步骤：

1. 通过具体示例理解 skill
2. 规划可复用的 skill 内容（scripts、references、assets）
3. 初始化 skill（运行 init_skill.py）
4. 编辑 skill（实现资源并编写 SKILL.md）
5. 打包 skill（运行 package_skill.py）
6. 根据真实使用情况迭代

按顺序执行这些步骤，只有在有明确理由时才跳过。

### 第 1 步：通过具体示例理解 Skill

只有在 skill 的使用模式已经非常清楚时才跳过。即便是在改造现有 skill 时，这一步也依然有价值。

为了创建高质量 skill，先要清楚它在现实中的具体使用方式。这种理解可以来自用户直接给出的例子，也可以来自你生成并经用户确认的例子。

### 第 2 步：规划可复用的 Skill 内容

把具体示例转化为高质量 skill 时，要分析每个示例：

1. 如果从零开始执行这个示例，需要做什么
2. 反复执行这些工作流时，哪些脚本、参考资料和资源会有帮助

### 第 3 步：初始化 Skill

此时就该真正创建 skill 了。

如果是从零开始创建新 skill，始终运行 `init_skill.py`，它会自动生成带模板的 skill 目录，更高效也更可靠。

用法：

```bash
scripts/init_skill.py <skill-name> --path <output-directory>
```

### 第 4 步：编辑 Skill

编辑新建或已有 skill 时，要记住它是给另一个 Claude 实例使用的。放入那些对另一个 Claude 有帮助且不明显的信息，例如程序性知识、领域细节或可复用资源。

有帮助的参考：

- **多步骤流程**：见 references/workflows.md
- **特定输出格式或质量标准**：见 references/output-patterns.md

### 第 5 步：打包 Skill

开发完成后，必须把 skill 打包为可分发的 `.skill` 文件。打包流程会先自动验证：

```bash
scripts/package_skill.py <path/to/skill-folder>
```

可选输出目录：

```bash
scripts/package_skill.py <path/to/skill-folder> ./dist
```

### 第 6 步：迭代

测试 skill 后，用户可能会提出改进请求。这通常发生在他们刚刚使用过 skill、对表现细节印象最清楚的时候。

**迭代工作流：**

1. 在真实任务中使用 skill
2. 发现卡点或低效之处
3. 识别 SKILL.md 或打包资源需要如何更新
4. 实施修改并再次测试
