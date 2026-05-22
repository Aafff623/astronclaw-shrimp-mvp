---
name: git-commit-guide
description: |
  Git 提交规范化指引（astronclaw-shrimp-mvp 参赛版）。当用户说"提交一下"、"commit"、"帮我写 commit"时，按此规范生成 commit message。
  覆盖参赛 MVP 全部 type 定义、scope 规则、subject 风格和 body 格式。
---

# Git Commit Guide Skill — AstronClaw Shrimp MVP

参赛项目 git 提交统一规范。Agent 生成 commit message 时必须遵循，用户也可手动参考。

## Commit 格式

```
<type>(<scope>): <subject>

<body（可选）>
```

- `type`：提交类型（见下方）
- `scope`：可选，影响范围（模块名 / 文件类型 / Skill 名）
- `subject`：简短描述，中英文均可，不超过 72 字
- `body`：可选，补充信息（部署链接、Skill ID、关联活动等）

## Type 类型

### 核心（贯穿全程）

| type | 用途 | 频率 |
|------|------|------|
| `skill` | AstronClaw Skill 配置变更（YAML / JSON 增删改） | 高频 |
| `deploy` | 部署相关：部署链接、环境变量、SkillHub 发布 | 中频 |
| `demo` | 演示资料：视频链接、GIF、截图、二维码 | 中频 |
| `docs` | README / 技术报告 / deploy.md / 其他文档 | 高频 |

### 进阶（迭代 / 打磨）

| type | 用途 | 频率 |
|------|------|------|
| `feat` | MVP 新功能（Agent 能力、集成渠道、交互入口） | 开发期高频 |
| `fix` | Bug 修复 / Skill 调用失败 / 推送异常 | 按需 |
| `refactor` | 重构：Skill 拆分、流程重组、目录调整 | 按需 |
| `polish` | 打磨：README 美化、格式规范化、视觉调整 | 提交前 |

### 杂项

| type | 用途 | 频率 |
|------|------|------|
| `chore` | 仓库结构、配置、`.gitignore`、依赖维护 | 按需 |
| `init` | 项目 / 目录 / 模块初始化 | 仅一次 |

## Scope 规则

- **Skill 名**：直接写 Skill 名或缩写，如 `skill(daily-summary)`、`skill(news-push)`
- **模块名**：如 `readme`、`deploy`、`technical-report`、`screenshots`
- **文件类型**：如 `env`、`gitignore`、`license`
- **可省略**：当 subject 已经足够清晰时，scope 可以不写

## Subject 风格

- 不超过 **72 字**（git log 默认换行宽度）
- 中英文混排，技术术语保留英文（AstronClaw、Skill、SkillHub、Webhook 等）
- 用 `—`（em dash）连接主信息和补充信息
- 信息结构：**做了什么 + 结果/规模**

## Body 格式

### 部署相关：附部署链接

```
deploy(skillhub): 发布 daily-summary Skill 到 SkillHub

Skill URL: https://...
Skill ID: shrimp-mvp-001
Status: 已公开
```

### Skill 迭代：附 Skill 名与版本

```
refactor(skill): 拆分 news-push Skill 为抓取 + 推送两个独立 Skill

- shrimp-fetch v0.2.0
- shrimp-push v0.1.0
```

### Agent 协助完成：附署名

```
docs(readme): 用 readme-polish 规范化打磨首屏

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>
```

## 实际示例

```bash
# 项目初始化
init: project structure for AstronClaw Shrimp MVP

# Skill 配置（高频）
skill(daily-summary): 新增每日论文抓取 Skill 配置
skill(news-push): 调整推送频率 cron 表达式 — 每天改为每 6 小时
feat(skill): 接入飞书机器人 Webhook 推送

# 部署
deploy: 首次部署到 AstronClaw 沙箱 — 测试链路通过
deploy(skillhub): 发布 daily-summary Skill 到官方 SkillHub
deploy(env): 补充 ASTRONCLAW_API_KEY 占位到 .env.example

# 演示资料
demo: 录制 90 秒演示视频并上传 Bilibili
demo(screenshots): 补充部署流程 4 张截图
demo(gif): 替换 demo.gif 为优化版（200KB → 80KB）

# 文档
docs(readme): 用户微调 — 标题、描述、章节命名优化
docs(report): 补充技术架构图与难点章节
polish(readme): 规范化打磨 — readme-polish skill 沉淀

# 修复
fix(skill): 修复 Webhook 推送内容编码错误
fix(deploy): 修正 .env.example 中 endpoint 拼写

# 重构
refactor(skill): 拆分推送逻辑为独立 Skill — 复用性提升

# 杂项
chore(gitignore): 补充 *.zip / build/ 忽略规则
```

## 规则

1. **一次提交只做一件事** — 不要把 Skill 改动和文档调整混在一起
2. **不要合并多天的内容** — git log 是参赛迭代的时间线
3. **Skill 配置变更必须用 `skill` 类型** — 评审会看 SkillHub 与 git 历史的对应关系
4. **部署相关变更必须用 `deploy` 类型** — 方便定位"何时改部署"
5. **Co-Authored-By**：Agent 协助完成的 commit 附带 `Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>`
6. **不要自动 push** — commit 后等用户确认再 push（参赛仓库公开，每次 push 都对评委可见）
7. **不要在 commit message 中暴露 API Key / Webhook URL** — 这些只能进 `.env`

## 与 cascade-maintain 的关系

当本 skill 提示 commit 前，建议先调用 [[cascade-maintain]] 确保下游文件一致后再提交，
避免 "Skill 改了但 README 部署链接没更新" 类问题。
