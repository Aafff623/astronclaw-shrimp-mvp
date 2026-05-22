---
name: readme-polish-strategy
description: README polish 的视觉-语义双闭环原则：banner 副标题 ↔ 章节结构 ↔ Skill 实现三层对齐
metadata:
  type: feedback
---

README polish 的核心原则：**视觉与语义形成双闭环**。

## 三层闭环

```
Banner 主视觉 + 副标题 (Agentic / Tool Use / Memory / Deployment / Observability)
       ↓
Highlights 章节按副标题五要素分行组织
       ↓
每行映射到 Skill 实际实现细节（不是空话）
```

评审视线路径：banner → 副标题 → Highlights → Skills 章节 → weekly-digest.yaml，
**叙事一气贯通，五要素反复出现，强化记忆**。

## 实际操作

### Before（平铺式 bullet）
```markdown
- 🦞 基于讯飞 AstronClaw —— 端云一体 AI Agent 平台
- ⚡ 零代码/低代码 Skill —— YAML/JSON 声明式
- 🛡️ 沙箱隔离运行 —— 国家信息安全三级认证
...（共 6 条平台能力罗列）
```
**问题**：讲的都是平台能力，没说"我们怎么用"，评审看了一眼就忘。

### After（五要素表格）
```markdown
| 维度 | weekly-digest 的实现 |
|------|----------------------|
| 🦞 Agentic Systems | 5 步流水线全自动...           |
| 🛠️ Tool Use        | 4 类外部 API 并发调用...      |
| 🧠 Memory          | Notion 数据库写入 + 复利优化  |
| 🚀 Deployment      | AstronClaw + SkillHub 一键... |
| 📊 Observability   | 重试 + 日志 + 告警...         |
```
**改进**：每行都有"我们的实现"，五要素与 banner 副标题对齐，评审能立刻 get 体系思考。

## How to apply

下次 polish README 时检查：

1. **Banner 文字是否被用作章节锚点？** —— 副标题里的关键词必须在正文中出现
2. **Highlights 是否回答"我们怎么用平台"？** —— 不是罗列平台能力
3. **每行 Highlight 是否能链到 Skills 章节？** —— 抽象 → 具体的层层下钻
4. **是否有信息密度高的展示形式？** —— 表格 / Mermaid 优先于段落

## 关联

- [[feedback_banner_decision]]：banner 副标题是 polish 的语义锚点
- [[project_agent_five_factors]]：五要素方法论
- [[user_participant_profile]]：用户认可表格 / Mermaid 高密度展示
