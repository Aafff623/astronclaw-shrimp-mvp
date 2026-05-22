# 设计思想总结

> 本文件沉淀 `astronclaw-shrimp-mvp` 项目从无到有过程中的**所有设计判断**，
> 让未来的协作者（包括未来的我 / Claude Code / Kiro）能在 10 分钟内 get 每个决策的"为什么"。
>
> 这不是结果罗列，是**思考过程的还原**。

---

## 0. 项目定位

讯飞 AstronClaw 养虾挑战赛参赛 MVP。核心命题：

> **怎么做一个不像 Demo 的 MVP？**

评审一天看 50 个项目，凭什么记住你？答案不是"功能多"，是「**有体系思考 + 真的能跑 + 视觉有记忆点**」。

本项目所有设计判断都围绕这一命题展开。

---

## 1. Skill 方向选择 — 反向推荐 weekly-digest

### 1.1 用户原始候选（5 个）

```
论文助手 · 待办 Agent · 简历优化 · 微信自动回复 · 解题虾
```

### 1.2 我的判断：5 个都不够好

| 候选 | 致命问题 |
|------|----------|
| 论文助手 | 烂大街，AI Demo 默认选项 |
| 待办 Agent | 不需要 AstronClaw 也能做，**反证平台没必要** |
| 简历优化 | 纯对话，零执行能力 |
| 微信自动回复 | 场景模糊 + 合规风险 |
| 解题虾 | 多模态加分但仍是问答 |

**共同问题**：都没有用满 AstronClaw 的「端云一体 + RPA + 沙箱」核心卖点。

### 1.3 反向推荐：weekly-digest

5 步流水线：`fetch → rank → cover → render → push`

| 步骤 | 用了什么平台能力 |
|------|------------------|
| fetch | 沙箱网络白名单 + 并发抓取 |
| rank | LLM + JSON Schema 输出 |
| cover | 多模态图像生成（端云一体） |
| render | 模板渲染 |
| push | 多渠道 RPA（飞书 / 企微 / Notion） |

**全部用上**。这才是 AstronClaw 的舞台。

### 1.4 方法论

下次设计 Agent Skill 时，先问 4 个问题：

1. 是否**必须用**到平台核心能力？
2. 是否有**真实执行**动作？
3. 是否能**60 秒演示闭环**？
4. 是否**架构可复用**？

四个 yes 以上才值得做 MVP。

完整记录见 [`memory/project_skill_direction.md`](../memory/project_skill_direction.md)。

---

## 2. Agent 五要素方法论

### 2.1 五要素

```
Agentic Systems · Tool Use · Memory · Deployment · Observability
```

这是国际 Agent 设计圈通用语言（**banner 副标题正是这五个词**）。

| 要素 | 检验问题 |
|------|----------|
| Agentic Systems | 能否无人值守跑完闭环？ |
| Tool Use | 是否调用多种外部工具？ |
| Memory | 是否有持久化状态？ |
| Deployment | 是否真实部署可访问？ |
| Observability | 失败是否有告警 / 追溯？ |

### 2.2 weekly-digest 的五要素映射

每个要素都有具体落地证据（不是空话），详见 [`memory/project_agent_five_factors.md`](../memory/project_agent_five_factors.md)。

### 2.3 价值

五要素方法论的真正价值不是"打分"，是**强制完整性**：
- 任一要素缺失 → 设计漏洞 → 必然在某个评审维度被扣分
- 五要素齐全 → Agent 设计圈一眼能识别"内行"

---

## 3. Banner 视觉决策

### 3.1 两个方向

| 方向 | 风格 | 优势 | 风险 |
|------|------|------|------|
| A 极简抽象 | 紫蓝渐变 + 几何 + claw 隐含轮廓 | 保守安全 | 评审记不住 |
| **B 科技养虾感** ✅ | 半抽象机械虾 + 神经网络线 | **有记忆点**，IP 强 | 做不好像小学生作业 |

### 3.2 选 B 的理由

评审一天 50 个项目。**能记住的从来不是"看起来对的"，是"长得不一样的"**。
赛事 IP（养虾）是免费的视觉资产，完全避开是浪费。
但卡通虾掉档次 —— 半抽象机械虾是中间地带。

### 3.3 生成路径

- 首选：**GPT-Image-2**（用户自己生成，质量稳定可控）
- 备选：Replicate Flux Schnell（本次余额不足未用）
- 兜底：手工 SVG（紧急保仓库不破图）

### 3.4 意外收获

用户用 GPT-Image-2 生成的版本，副标题正是 `Agentic Systems · Tool Use · Memory · Deployment · Observability`。
这五个词后来反向驱动了 README Highlights 章节的重组（见下节）。

完整记录见 [`memory/feedback_banner_decision.md`](../memory/feedback_banner_decision.md)。

---

## 4. README polish — 视觉-语义双闭环

### 4.1 核心原则

```
Banner 主视觉 + 副标题（五要素）
       ↓
Highlights 章节按副标题五要素分行
       ↓
每行映射到 Skill 实际实现细节
```

评审视线路径：**banner → 副标题 → Highlights → Skills 章节 → weekly-digest.yaml**，
五要素反复出现，叙事一气贯通。

### 4.2 改造前后对比

Before：6 条平铺式 bullet（讲平台能力）
After：5 行表格（**五要素 × weekly-digest 实现**）

After 版本的优势：
- 信息密度高（5 秒可扫完）
- 每行有"具体实现"，不是空话
- 与 banner 形成视觉-语义闭环

完整记录见 [`memory/feedback_readme_polish.md`](../memory/feedback_readme_polish.md)。

---

## 5. 工作流 Skill 设计

### 5.1 git-commit-guide

参赛专属 type 体系（不同于学习项目）：

| 阶段 | type | 用途 |
|------|------|------|
| 核心 | `skill` / `deploy` / `demo` / `docs` | Skill / 部署 / 演示 / 文档 |
| 进阶 | `feat` / `fix` / `refactor` / `polish` | 功能 / 修复 / 重构 / 打磨 |
| 杂项 | `chore` / `init` | 仓库维护 / 初始化 |

### 5.2 cascade-maintain

参赛专属 4 条联动链路（不同于学习项目的 6 条）：

| 链路 | 源 → 下游 |
|------|-----------|
| A. Skill 配置变更 | `skills/*.yaml` → README / deploy.md / .env.example / 技术报告 |
| B. 部署 URL 变更 | deploy.md → README / 技术报告 / 二维码 |
| C. 演示资料更新 | screenshots/ → README / 演示视频.md |
| D. 技术架构变更 | 技术报告 → README / LICENSE 年份 / Skill 触发条件 |

新增链路（本轮加入）：

| 链路 | 说明 |
|------|------|
| E. 三层规范变更 | `GUIDE.md` ↔ `CLAUDE.md` ↔ `steering.md` 对齐 |
| F. Skill 双套同步 | `.claude/skills/` ↔ `.kiro/skills/` 字节级一致 |
| G. 设计判断产生 | 沉淀到 `memory/` + 更新 `MEMORY.md` 索引 |

---

## 6. 多 Agent 协作架构

### 6.1 三层规范

```
GUIDE.md         （公共规范，所有 agent 都读）
   ↓
CLAUDE.md   ←→   steering.md
（Claude Code）  （Kiro）
```

CLAUDE.md 与 steering.md **主体对称**，差异仅在最后的"行为约定"节（工具名）。
公共内容（仓库结构 / Git 规则 / 内容风格 / 禁止事项）放 GUIDE.md，避免重复。

### 6.2 双套 Skill

```
.claude/skills/<name>/SKILL.md   ←  byte-level 一致  →   .kiro/skills/<name>/SKILL.md
```

任何 Skill 改动必须同步两边，否则两个 Agent 看到不一致的工作流规范，会产生混乱。
Copy-Item / `cascade-maintain` 链路 F 保证一致性。

### 6.3 Memory 索引

```
memory/
├── MEMORY.md                    # 索引（每条一行）
└── <type>_<topic>.md            # frontmatter (name / description / type)
```

类型：user / feedback / project / reference

Memory 的核心价值：**让重要决策不只活在 git commit message 里**，
未来的协作者（包括未来的我）能直接读到设计判断的"为什么"。

---

## 7. 经验沉淀 — 这个项目教会我的事

### 7.1 反向推荐比顺从有用

用户给了 5 个候选 → 我直接说"5 个都不够好" → 推荐第 6 个 → 用户采纳。
**有立场的协作 > 平均主义罗列**。前提是论据扎实。

### 7.2 视觉资料是免费的语义锚点

Banner 不只是装饰。副标题文字会被反复在 README / 演示视频 / SkillHub 介绍中复用。
设计 banner 时就要想：**这几个词后续能不能成为章节标题、章节锚点、演示开场白？**

### 7.3 三层规范是给未来自己写的备忘

`GUIDE.md` / `CLAUDE.md` / `steering.md` 三层架构看似冗余，实际是给"未来不记得当时为什么这么做"的自己写的备忘。
配合 `memory/` 系统，决策可被复用、可被继承、可被审计。

### 7.4 git log 是参赛迭代的时间线

按 `git-commit-guide` 分组 commit 后，git log 自然呈现「init → skill → cascade → polish」的迭代节奏。
**评审看 git log 时看到的是工程素养**，不是临时凑的 demo。

---

## 8. 未来 polish 方向

- [ ] AstronClaw 平台 Schema 真实校准（部署一次就知道哪些字段名错了）
- [ ] `weekly-digest` Memory 层升级（用户反馈循环 → 排序权重）
- [ ] 录制 30 秒演示视频时，开场就报五要素（强化体系叙事）
- [ ] SkillHub 发布后回填 README 部署链接，更新 Roadmap v1.0

---

_最后更新：2026-05-22 · 与 git log 时间线对齐_
