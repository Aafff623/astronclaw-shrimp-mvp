---
name: agent-five-factors
description: Agent 设计五要素（Agentic Systems / Tool Use / Memory / Deployment / Observability）与 Skill 设计的映射方法
metadata:
  type: project
---

Agent 设计圈通用的**五要素方法论**，用于评估和设计任何 Agent Skill 的完整性。

## 五要素定义

| # | 要素 | 中文 | 检验问题 |
|---|------|------|----------|
| 1 | **Agentic Systems** | 闭环执行 | Skill 是否能从触发到产出无人值守跑完？ |
| 2 | **Tool Use** | 多工具协作 | 是否调用多种外部 API / RPA / 数据源？ |
| 3 | **Memory** | 长期记忆 | 是否有状态写入持久层（数据库 / 文件 / 知识库）？ |
| 4 | **Deployment** | 部署可达 | 是否真实部署在云端，有可访问的入口？ |
| 5 | **Observability** | 可观测性 | 失败是否有告警？步骤是否可追溯？ |

## weekly-digest 的映射

| 要素 | 实现 |
|------|------|
| Agentic Systems | 5 步流水线全自动：定时触发 → 多源抓取 → AI 排序 → 多模态产出 → 多渠道分发 |
| Tool Use | arXiv API + GitHub Search API + 飞书/企微 Webhook + Notion API（4 类外部工具） |
| Memory | 周报写入 Notion 数据库 → 下一期排序权重的输入（复利式优化） |
| Deployment | AstronClaw 原生 cron + SkillHub 一键发布，沙箱隔离 |
| Observability | 指数退避重试 3 次 + 步骤级日志 + 失败时飞书自动告警 |

## How to apply

### 设计 Skill 时
用五要素做完整性 checklist。**任一缺失都是设计漏洞**：
- 缺 Memory → Agent 没有状态，每次都从零开始（不够智能）
- 缺 Observability → 失败无感知（生产不可用）
- 缺 Tool Use → 跟普通 LLM 调用没区别（平台没必要）
- 缺 Agentic Systems → 不是 Agent，是 prompt（评审会扣分）
- 缺 Deployment → 闭门 Demo（不算参赛作品）

### 文档输出时
README Highlights 章节按五要素组织，**banner 副标题 ↔ Highlights ↔ Skill 实现**形成三层闭环，
评审一眼能 get 项目的体系思考。

### 评估其他 Agent Skill 时
用五要素打分（每项 0-2 分，满分 10），低于 7 分基本不值得做 MVP。

## 来源

五要素短语来自用户的 GPT-Image-2 banner 副标题 `Agentic Systems · Tool Use · Memory · Deployment · Observability`，
是国际 Agent 设计圈通用语言。

## 关联

- [[project_skill_direction]]：用五要素筛选 weekly-digest 而非 5 个通用候选
- [[feedback_banner_decision]]：banner 副标题即五要素来源
- [[feedback_readme_polish]]：Highlights 章节按五要素重组的视觉-语义闭环
