---
name: ai-prd
description: Write a product requirements document (PRD) for an AI or LLM-powered feature — covering the problem, users, scope, and user stories like a normal PRD, plus the AI-specific parts most PRDs miss — why AI at all, model and architecture options (prompting / RAG / fine-tuning / agent), an evaluation plan with offline test sets and online metrics, failure modes and hallucination mitigations, human-in-the-loop checkpoints, data privacy and compliance, cost and latency budgets, and a staged rollout with go/no-go criteria. Use this skill whenever the user wants to write, draft, review, or improve a PRD, spec, requirements doc, or product proposal for anything involving AI, LLMs, chatbots, copilots, agents, RAG, AI assistants, or "adding AI" to an existing product — even if they just say "帮我写个 AI 功能的需求文档", "我想做一个 AI 助手，写个 PRD", "review my AI feature spec", or hand over a backlog from the user-story-backlog skill and ask for a PRD.
---

# AI 产品需求文档（AI PRD）

写一份**开发能做、测试能测、上线能判断成败**的 AI 产品需求文档。

普通 PRD 回答"做什么"和"做成什么样"。AI 产品还必须回答几个普通 PRD 不会问的问题：

- **为什么要用 AI？** 很多需求用规则或普通功能就能解决，而且更便宜、更可靠
- **"做好"怎么定义？** AI 的输出是概率性的，同一个问题每次答案可能不同，所以验收不能只靠"点一下看看"，需要评测集和指标
- **出错了怎么办？** AI 一定会出错。PRD 要事先写清楚哪些错误不能接受、怎么发现、怎么兜底
- **人在哪里介入？** 哪些动作 AI 可以自己做，哪些必须由人确认
- **数据能不能这样用？** 用户数据发给谁、存在哪、会不会被用于训练

这个 skill 的核心立场：**一个 AI 功能是否成功，要在开发前就写清楚判断标准。** 没有评测计划的 AI PRD，等于没有验收标准。

## 工作流程

### 第 1 步：收集输入，确认缺口

| 输入 | 处理方式 |
|---|---|
| 产品想法、会议记录 | 提取问题、用户和目标；关键信息缺失时先提问 |
| user-story-backlog 的输出 | 直接沿用其中的用户角色、故事和验收标准，作为 PRD 的需求部分；待确认问题合并到 PRD 的"开放问题" |
| usability-synthesis 的输出 | 作为"问题与证据"部分的依据 |
| 已有 PRD 草稿 | 进入**评审模式**：按 `references/ai-prd-checklist.md` 逐项检查，输出缺失项和修改建议，而不是重写整份文档 |

如果以下信息缺失，先向用户提问（最多 5 个问题）；用户希望直接开始时，按最合理的假设写，并在文档开头列出假设：

- 目标用户和使用场景
- 要解决的具体问题，以及现在用户是怎么解决的
- 数据从哪里来，是否涉及个人信息或敏感数据
- 有没有部署方式、预算或时间上的约束

### 第 2 步：先回答"为什么要用 AI"

在写任何 AI 相关内容之前，先做这个判断：

- 这个问题用**规则、搜索、模板或普通功能**能解决吗？如果能，AI 带来的额外价值是什么？
- 用户能接受 AI 偶尔出错吗？出错的代价有多大？
- 有没有足够的数据或知识来源，支撑 AI 做好这件事？

如果结论是"不需要 AI"或"只有一部分需要 AI"，如实写出来。**指出不该用 AI 的地方，是 AI 产品经理最有价值的判断之一。**

### 第 3 步：写需求部分

和普通 PRD 一样：背景与问题、目标用户、目标与成功指标、范围（做什么 / 不做什么）、用户故事与验收标准、用户流程。

**成功指标**分两层写：

- **业务指标**：这个功能最终要改变什么（如客服工单量下降、任务完成时间缩短）
- **AI 质量指标**：AI 本身做得好不好（如回答准确率、拒答准确率），具体见第 5 步

### 第 4 步：写 AI 方案部分

阅读 `references/ai-design-guide.md`，按其中的内容完成：

1. **AI 能力定义**：AI 具体负责哪一步，输入是什么、输出是什么、输出给谁用
2. **技术方案选择**：提示词工程 / RAG / 微调 / Agent，列出候选方案和选择理由。写到 PM 需要的深度即可：说清楚"为什么选它"和"代价是什么"，具体实现留给技术方案文档
3. **模型选择考虑**：效果、成本、延迟、部署方式（API / 私有化）、数据合规，不指定具体模型版本时写明"需技术评估"

### 第 5 步：写评测计划

这是 AI PRD 最重要的部分。按 `references/ai-design-guide.md` 中的评测章节完成：

- **离线评测**：评测集怎么构建（来源、规模、覆盖哪些类型的问题，必须包含难例和"应该拒答"的问题）、用什么指标、上线门槛是多少
- **在线评测**：上线后看哪些指标、怎么收集用户反馈
- **上线门槛（Go / No-Go）**：每个关键指标写明具体阈值。阈值需要和团队一起确认，PRD 中可以写"建议值"，但不能留空

### 第 6 步：写风险与兜底

- **失败模式**：列出这个功能**最可能**怎么出错，以及**最不能接受**怎么出错。每种失败写明严重程度、发现方式和兜底方案
- **人工介入节点**：哪些动作 AI 可以直接执行，哪些需要用户确认，哪些必须转人工。按 `references/ai-design-guide.md` 中的分级方法判断
- **数据与合规**：涉及哪些数据，是否包含个人信息或敏感信息，数据是否出境、是否用于训练，需要哪些用户授权。只写到"需要满足什么要求"，不给出法律意见，注明"需法务 / 合规确认"

### 第 7 步：写上线计划和开放问题

- **分阶段上线**：内测 → 小流量灰度 → 全量，每个阶段写明进入下一阶段的条件
- **成本与性能预算**：单次调用成本、响应时间的上限
- **开放问题**：所有未确定的事项，写明负责人或建议确认对象

### 第 8 步：自查

用 `references/ai-prd-checklist.md` 检查一遍，补上遗漏的部分。

## 输出格式

按 `templates/ai-prd-template.md` 的结构输出。可以根据功能的规模删减：

- **小功能**（如在已有产品里加一个 AI 摘要按钮）：保留所有 AI 相关章节，需求部分可以简写
- **AI 原生产品**：完整输出所有章节

但以下四个部分**任何规模都不能删**：为什么要用 AI、评测计划、失败模式与兜底、数据与合规。它们是 AI PRD 和普通 PRD 的本质区别。

用用户使用的语言写作。用户要求导出为文档时，按其要求的格式输出。

## 示例

完整的输入和输出示例见 `examples/` 目录。
