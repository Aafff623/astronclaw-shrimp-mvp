# GUIDE.md

> 项目通用规范与工作索引 —— 无论用 Claude Code、Kiro 还是其他 AI 编程工具接入本项目，均以此文件为准。

## 项目概述

讯飞 **AstronClaw 养虾挑战赛**参赛 MVP 仓库。核心交付：

1. 一个真实部署在 AstronClaw 平台的 Agent Skill（`weekly-digest`）
2. 发布到官方 **SkillHub** 接受社区评价
3. 演示视频 + 完整文档 + 干净 git log 时间线

## 仓库结构

```
astronclaw-shrimp-mvp/
├── README.md                     # 项目首页（评审第一眼）
├── GUIDE.md                      # 本文件（公共规范）
├── CLAUDE.md                     # Claude Code 入口
├── steering.md                   # Kiro 入口
├── deploy.md                     # AstronClaw 一键部署教程
├── .env.example / .gitignore / LICENSE
├── assets/                       # Banner 等视觉资源
├── screenshots/                  # 演示 GIF 与截图
├── skills/                       # AstronClaw Skill 配置（上传到平台用）
│   └── weekly-digest.yaml
├── docs/
│   ├── 技术报告.md
│   ├── 演示视频.md
│   ├── design-thinking.md        # 设计思想总结
│   └── 效果截图/
├── memory/                       # 项目协作记忆（决策 / 判断 / 偏好）
│   ├── MEMORY.md                 # 索引
│   └── *.md                      # 各 memory 文件
├── .claude/skills/               # Claude Code 工作流 skill
└── .kiro/skills/                 # Kiro 工作流 skill（与 .claude/skills 镜像）
```

## 工作索引规范

### Skill 配置开发
- 每个 Skill 一个 YAML / JSON 文件，文件名 kebab-case
- 顶部注释包含：版本号 + Schema 校准提示
- 必须显式声明 `security.network_allowlist`（沙箱合规）
- 必须有 `on_failure` 兜底告警
- 失败重试用指数退避

### Git 提交
- 遵循 [`.claude/skills/git-commit-guide/SKILL.md`](./.claude/skills/git-commit-guide/SKILL.md) 规范
- 格式：`<type>(<scope>): <subject>`
- 参赛高频类型：`skill` / `deploy` / `demo` / `docs` / `polish` / `chore`
- 一次提交只做一件事；不合并多语义
- 不在 commit message 中暴露密钥 / Webhook URL

### 索引联动维护
- 改动后遵循 [`.claude/skills/cascade-maintain/SKILL.md`](./.claude/skills/cascade-maintain/SKILL.md) 检查下游
- 关键链路：
  - **Skill 配置变更** → README / deploy.md / .env.example / 技术报告
  - **三层规范变更** → `GUIDE.md` ↔ `CLAUDE.md` ↔ `steering.md` 对齐
  - **Skill 双套变更** → `.claude/skills/` ↔ `.kiro/skills/` 同步
  - **设计判断产生** → 沉淀到 `memory/`

### 文档维护
- README 结构按 `readme-polish` 规范，**评审第一眼**
- 技术报告完整反映 Skill 设计、难点、技术栈
- 演示视频外链统一放 `docs/演示视频.md`
- 重要设计判断必须进 `memory/`，不止在 git log

### 多 Agent 协作
- Claude Code 读 [`CLAUDE.md`](./CLAUDE.md) 入口
- Kiro 读 [`steering.md`](./steering.md) 入口
- 两入口"核心目标 / 阶段 / 决策 / 方向"必须**一致**；差异仅在「行为约定」节
- `.claude/skills/<name>/SKILL.md` 与 `.kiro/skills/<name>/SKILL.md` 内容**字节级一致**

## 内容风格

- 中文为主，技术术语保留英文：AstronClaw / Skill / SkillHub / Agent / RPA / Webhook
- 先讲「为什么」，再讲「怎么做」；不写空话
- 表格 / Mermaid 图优先（信息密度高于文字段落）
- 统一色板：紫 `#6C3CE1` · 蓝 `#3B82F6` · 黄 `#F59E0B` · 绿 `#10B981` · 红 `#EF4444`

## Hackathon 提交阶段

- 部署到 AstronClaw 必须留下可访问 URL（不能写死占位）
- 发布到 SkillHub 必须公开
- 演示视频 30 ~ 90 秒，覆盖：触发 → 抓取 → 真实推送
- README 部署链接 + 技术报告 + 演示视频缺一不可

## 禁止事项

- 不在 commit / README / 公开文档中暴露 API Key / Webhook URL / 私钥
- 不把 `.env` 加入版本控制（`.gitignore` 已配置）
- 不修改 `.claude/skills/` 而不同步 `.kiro/skills/`
- 不在完成用户任务后直接 push，需用户 review 授权
- 不发布违反内容合规的 Skill（政治敏感 / 暴力 / 低俗）
- 不尝试沙箱越权（本地文件读写 / 敏感系统 API）
- 不在 commit 历史中重写已 push 到公开仓库的提交（参赛痕迹对评审可见）
