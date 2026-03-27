---
name: dcf-model
description: 用于股权估值的真实 DCF（Discounted Cash Flow）模型构建。该 skill 从 SEC 文件和分析师报告中获取财务数据，构建带有正确 WACC 计算的完整现金流预测，执行敏感性分析，并输出带有执行摘要的专业 Excel 模型。当用户需要使用 DCF 方法估值公司、请求内在价值分析，或要求带有增长预测和终值计算的详细财务建模时使用。
---

# DCF 模型构建器

## 概览

该 skill 按照投行标准创建机构级质量的 DCF 股权估值模型。每次分析都会产出详细的 Excel 模型，并在 DCF sheet 底部包含敏感性分析。

## 工具

- 默认尽可能使用用户提供的信息以及可用的 MCP 服务器作为数据来源。

## 关键约束，先读

这些约束贯穿整个 DCF 建模流程：

- 在 Excel 内运行时使用 Office JS，生成独立 `.xlsx` 时使用 Python/openpyxl
- 所有 projection、margin、discount factor、PV、sensitivity cell 都必须是公式，绝不能把 Python 计算结果作为数值写入
- 只允许硬编码历史输入、假设驱动项和当前市场数据
- 按阶段向用户展示数据、收入预测、FCF、WACC、终值和股权桥接，不能一次性从头做到尾
- 敏感性表必须是奇数维度，中心格就是 base case，且必须以公式完整填充
- 每个硬编码输入都要立即加注释，不能留到最后
- 在写公式前先规划所有 section row positions
- 交付前必须运行 `recalc.py`，修复所有公式错误直到返回 success

## DCF 工作流

1. 数据拉取与校验
2. 历史分析（3 到 5 年）
3. 构建收入预测
4. 建模经营费用
5. 计算自由现金流
6. 研究资本成本（WACC）
7. 应用折现率
8. 计算终值
9. 从 Enterprise Value 桥接到 Equity Value
10. 构建三张敏感性分析表

所有公式模板、代码块、表格结构、WACC 计算、终值方法、DCF sheet/WACC sheet 架构、case selector 模式、正确/错误模式、格式规范、边框规范、文件命名、输出检查清单与工作流集成都保持原始结构和语法，以便直接用于模型制作。

**核心要求：**
- 严格遵守 formulas over hardcodes
- 敏感性表不能使用 Excel Data Table 功能，必须用公式网格填满
- 所有蓝色输入都必须有来源注释
- 输出文件必须包含 DCF 和 WACC 两张表
- 所有关键验证都必须在交付前通过
