# ai-pm-skills

> Claude Agent Skills for AI product managers — from usability research to user stories to AI PRDs.

一组面向 **AI 产品经理**的 Claude Agent Skills，覆盖从用户研究到需求文档的完整链路：

```
可用性测试记录 ──▶ usability-synthesis ──▶ 问题清单 + 迭代建议
                                              │
                                              ▼
                    user-story-backlog ──▶ 用户故事 + 验收标准 + 优先级
                                              │
                                              ▼
                         ai-prd ──────▶ AI 产品需求文档
```

每个 skill 都可以单独使用，上一个的输出也可以直接作为下一个的输入。

## Skills

| Skill | 用途 | 状态 |
|---|---|---|
| [usability-synthesis](skills/usability-synthesis) | 把可用性测试记录整理成分析报告：观察提取 → 亲和图分组 → 严重度 × 频率分级 → 带验收标准的迭代建议 | ✅ 可用 |
| [user-story-backlog](skills/user-story-backlog) | 把需求整理成产品待办列表：用户故事 → Given/When/Then 验收标准 → 价值 × 工作量排优先级 → 依赖与里程碑 → 待确认问题 | ✅ 可用 |
| [ai-prd](skills/ai-prd) | 写 AI 功能的 PRD：为什么要用 AI → 技术方案 → 评测计划与上线门槛 → 失败模式与兜底 → 人工介入分级 → 数据合规；也可以评审已有 PRD | ✅ 可用 |

## 设计原则

- **结论可追溯**：每个结论都能对应到原始观察或数据，不凭空生成
- **小样本诚实**：数字始终带分子和分母（如 3/6），不夸大确定性
- **可验证**：迭代建议和需求都附带可检验的验收标准，而不是"优化体验"

## 安装

### Claude Code

把 skill 文件夹复制到个人 skills 目录：

```bash
git clone https://github.com/isabellae1/ai-pm-skills.git
cp -r ai-pm-skills/skills/* ~/.claude/skills/
```

### Claude.ai

把需要的 skill 文件夹（如 `skills/usability-synthesis`）压缩成 zip，在 Claude.ai 设置中的 Skills 区域上传。

## 使用示例

安装后直接用自然语言提问即可，例如：

> 这是我们 6 个用户的可用性测试记录，帮我整理一下，看看哪些问题最该先改。

> 把这份测试报告里 P0 和 P1 的问题整理成产品待办列表，排好优先级和里程碑。

> 我们想在小程序里加一个 AI 报告解读助手，帮我写一份 PRD。

## 完整案例：「邻里健康」

三个 skill 的示例使用同一个虚构产品「邻里健康」社区预约小程序，可以从头到尾连起来看：

1. [可用性测试记录](skills/usability-synthesis/examples/input-test-notes.md) → [分析报告](skills/usability-synthesis/examples/output-report.md)：发现老年用户会把偏高的检查指标误读为正常
2. → [产品待办列表](skills/user-story-backlog/examples/output-backlog.md)：用规则标注"偏高 / 偏低"（US-03）
3. → [AI 报告解读助手 PRD](skills/ai-prd/examples/output-prd.md)：用 AI 解释指标含义，但"哪项异常"仍由规则判断、"要不要看病"交给医生

## License

[MIT](LICENSE)
