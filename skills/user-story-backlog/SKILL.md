---
name: user-story-backlog
description: Turn raw requirements — client meeting notes, feature requests, a PRD draft, stakeholder wishlists, or a usability findings report — into a structured product backlog of user stories with Given/When/Then acceptance criteria, value × effort prioritization, dependencies, milestones, and a list of open questions. Use this skill whenever the user wants to write user stories, build or groom a backlog, break an epic down, plan sprints or milestones, prepare tickets for Jira/Linear/Trello, or asks things like "帮我拆一下需求", "写用户故事", "整理成产品待办列表", "这些需求怎么排优先级", even if they don't say "user story". Also use it right after the usability-synthesis skill to turn its P0/P1 recommendations into backlog items.
---

# 需求拆解与产品待办列表（User Story Backlog）

把零散的需求，整理成**开发能直接领走、测试能直接验收**的产品待办列表：谁需要什么、为什么、做到什么程度算完成、先做哪个。

这个 skill 的核心立场有两条：

1. **需求来源要可追溯，不凭空补需求。** 原始材料里没说清楚的地方，列为"待确认问题"，而不是自己脑补一个答案写进故事里。PM 写错的需求比没写的需求代价更大，因为开发会照着做。
2. **先排依赖，再排价值。** 价值最高的功能，如果依赖的底层还没打好，硬做只会反复返工。

## 工作流程

### 第 1 步：识别输入类型

| 输入类型 | 处理方式 |
|---|---|
| 会议记录、客户原话、需求清单 | 从中提取需求，原话可作为来源引用 |
| 已有 PRD 或需求文档 | 按文档结构拆解，保留原有编号便于对照 |
| usability-synthesis 报告 | 每条 P0/P1 迭代建议转为一个故事；报告里的验收标准直接沿用为验收标准；"需求层面的问题"转为待确认问题 |
| 一句话想法（"做个记账 App"） | 信息太少，先列出 3–5 个关键问题请用户回答；如果用户希望直接开始，按最常见的理解拆解，并在报告开头写明假设 |

### 第 2 步：识别用户角色

列出所有会和产品打交道的角色，包括容易漏掉的：管理员、客服、未登录用户、第三方系统。每个角色写一句话描述**他想达成什么**，而不只是职位名称。

### 第 3 步：拆分 Epic 和用户故事

- **Epic**：一个完整的用户目标，通常需要多个故事才能实现
- **用户故事**：按以下格式写：

  > 作为 **[角色]**，我希望 **[能力]**，以便 **[价值]**。

  "以便"这一句不能省，它是排优先级和判断范围的依据。写不出"以便"的故事，往往说明这个需求还没想清楚，应该进入待确认问题。

- 用 `references/story-quality.md` 中的 **INVEST** 标准检查每个故事，开始拆分前先阅读它。太大的故事继续拆，最常用的拆法写在该文件里。
- **技术性工作**（如协议升级、数据迁移、搭建基础设施）不强行写成用户故事，标为 **Enabler（支撑项）**，写清楚它支撑哪些故事。

### 第 4 步：写验收标准

每个故事写 2–5 条验收标准，用 **Given / When / Then** 格式：

> **Given** [前置条件]，**When** [用户操作]，**Then** [可观察的结果]。

- 至少包含一条**正常路径**和一条**异常或边界情况**（如网络断开、输入为空、无权限）
- 结果必须**可观察、可验证**，避免"体验流畅""界面友好"这类无法测试的描述
- 涉及 AI 功能时，补充对 AI 输出的约束，例如"证据不足时拒答""高风险操作需用户确认"

### 第 5 步：估算与排优先级

- **工作量**：用 S / M / L 相对估算，不给具体天数。在报告中注明"需与开发团队确认"，因为 PM 单方面的估算只能作为参考。
- **用户价值**：高 / 中 / 低，依据是"以便"那一句，以及有多少用户会受益
- **优先级**：用 MoSCoW 分类（Must / Should / Could / Won't this time），参考下表：

| 价值 \ 工作量 | S | M | L |
|---|---|---|---|
| 高 | Must | Must | Should（考虑拆小） |
| 中 | Should | Should | Could |
| 低 | Could | Won't this time | Won't this time |

表格只是起点。如果某个故事是其他 Must 故事的前置依赖，它自动升为 Must；合规、安全相关的故事不因工作量大而降级。调整时写明理由。

### 第 6 步：梳理依赖并划分里程碑

1. 标出故事之间、故事和 Enabler 之间的依赖关系
2. **先按依赖排序**：被依赖的放前面
3. **再按优先级排序**：同一层级内，Must 优先
4. 划分为 2–4 个里程碑，每个里程碑写一句**交付目标**（这一阶段结束后，用户能做到什么）

第一个里程碑应该是一个**能独立演示的最小可用版本**，而不只是"把底层搭好"。如果底层工作量很大，就在第一个里程碑里同时纳入一条最核心的用户路径，让它能被看见、被验证。

### 第 7 步：整理待确认问题

把材料中矛盾、模糊、缺失的地方集中列出，每条写明：问题是什么、影响哪些故事、建议问谁。这一部分和故事本身同样重要。

## 输出结构

```markdown
# [产品名] 产品待办列表

## 概要
- 输入来源：
- 规模：N 个 Epic，M 个用户故事，K 个 Enabler
- 假设说明：（如有）

## 用户角色
| 角色 | 想达成什么 |

## 产品待办列表
| 编号 | Epic | 用户故事 | 价值 | 工作量 | 优先级 | 依赖 | 里程碑 |

## 故事详情
### [编号] 故事标题
- 用户故事：作为……我希望……以便……
- 来源：（引用原始材料的位置或原话）
- 验收标准：
  - Given … When … Then …
- 备注：（优先级调整理由、拆分说明等）

## Enabler（支撑项）
| 编号 | 内容 | 支撑的故事 | 工作量 |

## 里程碑
| 里程碑 | 交付目标 | 包含 |

## 待确认问题
| 编号 | 问题 | 影响的故事 | 建议确认对象 |
```

用用户使用的语言写作。如果用户需要导入 Jira、Linear 等工具，额外输出一份 CSV，列为：`Summary, Description, Acceptance Criteria, Priority, Epic Link, Labels`。

## 示例

完整的输入和输出示例见 `examples/` 目录。
