---
description: 从 PowerPoint 模板文件创建可复用的 PPT 模板 skill
argument-hint: "[.pptx 或 .potx 文件路径]"
allowed-tools: ["Read", "Write", "Bash", "Glob"]
---

# PPT 模板创建命令

根据用户提供的 PowerPoint 模板创建一个自包含的 PPT 模板 skill。

## 说明

1. **如果未提供模板文件，则索取模板文件**：
   - "Please provide the path to your PowerPoint template file (.pptx or .potx)"
   - 模板应包含你想使用的幻灯片版式和品牌元素

2. **加载 ppt-template-creator skill**：
   - 使用 `skill: "ppt-template-creator"` 工具加载完整 skill 说明
   - 按照该 skill 中的工作流分析模板并生成新的 skill

3. **收集额外信息**：
   - 公司名或模板名（用于命名 skill）
   - 主要使用场景（融资路演材料、董事会材料、客户演示等）

4. **执行 skill 工作流**：
   - 分析模板结构（版式、占位符、尺寸）
   - 生成带有 assets/ 和 SKILL.md 的 skill 目录
   - 创建示例演示文稿进行验证
   - 打包 skill

5. **将打包好的 skill 交付给用户**
