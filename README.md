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
| user-story-backlog | 把需求整理成用户故事、验收标准、优先级和里程碑 | 🚧 开发中 |
| ai-prd | 生成 AI 产品 PRD，包含评测指标、幻觉对策和人工确认节点 | 🚧 开发中 |

## 设计原则

- **结论可追溯**：每个结论都能对应到原始观察或数据，不凭空生成
- **小样本诚实**：数字始终带分子和分母（如 3/6），不夸大确定性
- **可验证**：迭代建议和需求都附带可检验的验收标准，而不是"优化体验"

## 安装

### Claude Code

把 skill 文件夹复制到个人 skills 目录：

```bash
git clone https://github.com/isabellae1/ai-pm-skills.git
cp -r ai-pm-skills/skills/usability-synthesis ~/.claude/skills/
```

### Claude.ai

把 `skills/usability-synthesis` 文件夹压缩成 zip，在 Claude.ai 设置中的 Skills 区域上传。

## 使用示例

安装后直接用自然语言提问即可，例如：

> 这是我们 6 个用户的可用性测试记录，帮我整理一下，看看哪些问题最该先改。

## License

[MIT](LICENSE)
