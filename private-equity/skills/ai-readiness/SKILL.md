# 组合公司 AI 就绪度

description: 扫描整个组合，识别最具杠杆效应的 AI 机会，并排序 operating-partner 时间最该投向哪里。读取多家组合公司的季度更新和财务数据，识别各自的快速落地点，并汇总成一份统一的优先级行动清单。适用于季度组合回顾、年度规划，或决定哪些公司应优先获得 AI 投入。触发词包括 "AI readiness"、"AI opportunity scan"、"where should we deploy AI"、"AI across the portfolio"、"AI quick wins" 或 "which portcos are ready for AI"。

## Workflow

### Step 1: 连接组合数据

先询问用户组合材料放在哪里。不要自行假设，给出选项：

- **MCP servers**，数据室、SharePoint、Google Drive，或已连接的 portfolio-ops 数据库
- **Local files**，磁盘上的文件夹路径，里面包含季度 deck、财务数据、board packs
- **File uploads**，直接把 PDF、PowerPoint 或 Excel 拖进对话

连接后，读取整个组合，或其子集的季度更新、董事会材料和财务数据。对每家公司提取：行业、收入、各职能 headcount、提到的 tech stack，以及是否已有 AI / automation initiative 在推进。

如果用户只提供单家公司，也照样做扫描，只是跳过跨组合排序。

如果材料里不明显，前面就要问清：
- 各公司剩余持有期，AI payback 在距离退出只剩 12 个月时意义会小很多
- 是否已有某家 portco 实施过有效方案，可供复制

### Step 2: 单家公司扫描

对每家公司，回答 3 个 gate 问题。3 个都为 yes 才是 **Go**。任一为 no 则标记 **Wait**，并说明解除阻碍所需条件。

1. **数据是否可用？** 能否在不先做 6 个月数据项目的前提下，为该 use case 提供干净输入，如客户清单、发票流、合同库。
2. **是否有 owner？** 管理团队里是否有人真正负责推动，而不是只有 sponsor 口头 "support"。
3. **能否在 30 天内 pilot？** 一支团队、一个工作流、现成工具。如果答案以 "first we'd need to..." 开头，就不是 quick win。

然后识别最重要的 2-3 个 leverage point。重点看成本结构和运营中的这些模式：

**Back Office，通常最容易 pilot**
- 发票处理、AP / AR 匹配、费用分类
- 合同摘要，vendor agreements、leases、customer MSAs
- 月结流程，reconciliation、flux commentary、lender reporting 初稿

**Revenue / Front Office**
- RFP 和 proposal 初稿，如果收入以项目制为主，这通常杠杆很大
- 销售电话摘要和 CRM hygiene
- 客户支持工单分流和首轮回复草拟
- 配置型 / 复杂产品的报价

**Operations，取决于行业**
- SOP 和质量文档生成
- 排班和调度，field services、logistics
- 代码生成和代码审查，software portcos

对每个 leverage point，用一句话说明：替代什么工作、每周节省多少 FTE-hours，按 30-50% 假设，不要按 100%，以及是买现成工具还是需要轻量开发。

### Step 3: 跨组合排序

把每家公司识别出的 leverage point 全部堆成一张总表。按以下标准排序：

1. **Dollar impact**，年化 EBITDA 贡献，成本节省 + 收入提升，扣除工具成本后
2. **Speed to value**，从开始到首次可量化结果的月数
3. **Probability**，考虑数据质量、变更管理风险、管理团队能力后的折扣概率

如果分数接近，优先考虑剩余持有期少于 18 个月的机会，这类机会要么现在做，要么干脆不做。

输出总表：

| Rank | Company | Opportunity | Est. EBITDA ($) | Months to Value | Gate | First Step |
|---|---|---|---|---|---|---|
| 1 | | | | | Go | |
| 2 | | | | | Go | |
| 3 | | | | | Wait， [blocker] | |

### Step 4: 找出可复制打法

在组合里最有杠杆的动作，通常是把一个成功打法复制到多家公司。重点扫描：

- **同一行业、同一职能**，例如两家 healthcare services portcos 都有人工作 prior-auth，一个实施，两家落地
- **同一工具、不同公司**，如果一家 portco 已经跑通了 invoice-processing，就标出所有 AP volume 超过 $Xm 的其他 portcos，作为快速跟进者
- **共享供应商议价能力**，三家 portco 采购同一工具，就是一个议价机会

列出每个 replay，说明 lead company，谁先验证，以及 follower companies，谁复制。

### Step 5: 输出

为 operating partner 准备一页式组合回顾材料：

1. **Top 5 across the portfolio**，来自 Step 3 的排序表，附 owner 和 30 天内的 first step
2. **Replays**，2-3 个能同时覆盖多家公司的 playbook
3. **Go / Wait by company**，每家公司一行，Wait 要写清解除阻碍条件
4. **What we're NOT doing**，纸面上看起来不错，但未通过 gate 的机会，避免 operating partner 每个季度反复讨论
5. **Aggregate EBITDA contribution**，组合层面的 AI 总机会，拆分为 Year 1 quick wins 和 Years 2-3 scale 机会

## Important Notes

- **按美元排序，不按兴奋度排序。** 对一家 $40m revenue 公司来说，一个每年节省 $400k 的 AP automation，几乎总比一个炫目的面向客户 chatbot 更值钱。
- **真正的约束几乎总是数据，不是模型。** 如果一家公司连干净的客户清单都拿不出来，AI 不是第一项目，先做数据清理。要把这点说清楚。
- **优先现成工具。** 自研方案对工程能力不强的公司来说通常慢、贵且脆弱。优先推荐可以买来就部署的工具。
- **Owner 才是真正的 gate。** 一个没有内部 owner 的 quick win，90 天内大概率会死掉。如果管理团队里没人愿意负责，不管金额多大，都应标成 Wait。
- **持有期决定紧迫度。** 距离退出还有 3 年的公司，可以做基础数据项目。12 个月内要退出的公司，需要能体现在 CIM 所看 LTM EBITDA 里的项目，否则就跳过。
- **失败 pilot 本身就是信号。** 如果管理层已经试过某件事但没成功，要先搞清为什么，再决定是否再次提议。
