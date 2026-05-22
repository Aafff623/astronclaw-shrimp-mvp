# steering.md

> Kiro 接入本项目时的方向与决策指引。项目级通用规范见 [`GUIDE.md`](./GUIDE.md)。
> 与 [`CLAUDE.md`](./CLAUDE.md)（Claude Code 入口）主体对称，差异仅在最后的「行为约定」节。

## 核心目标

1. **真实跑通 `weekly-digest` Skill** —— AstronClaw 沙箱执行成功，飞书 / 企微 / Notion 收到真实周报
2. **发布到官方 SkillHub** —— 公开可访问，接受社区收藏与评价
3. **完整提交参赛包** —— 部署链接 + 演示视频 + GitHub 仓库

## 当前阶段

- [x] 仓库骨架就位（README / docs / skills / LICENSE / Banner）
- [x] git-commit-guide + cascade-maintain skill 设计完成
- [x] `weekly-digest.yaml` 配置落地（5 步流水线，248 行）
- [x] 多 Agent 三层规范架构（GUIDE + CLAUDE + steering）
- [x] `memory/` 系统初始化
- [ ] AstronClaw 平台真实部署（Schema 待校准）
- [ ] SkillHub 公开发布
- [ ] 演示视频 30-90 秒录制
- [ ] 提交参赛包

## 决策记录

| 日期 | 决策 | 原因 |
|------|------|------|
| 2026-05-22 | 仓库初始化 + 三层规范 + 双套 Skill | 评审看的是工程素养，不是临时凑的 demo |
| 2026-05-22 | 选 `weekly-digest` 方向，放弃论文助手等 5 个候选 | 唯一能用满 AstronClaw 五要素的方向 |
| 2026-05-22 | Banner 走方向 B（科技养虾感），用 GPT-Image-2 | 评审一天看 50 个项目，记忆点 > 安全感 |
| 2026-05-22 | README polish 按 Banner 副标题五要素重组 | 视觉-语义双闭环 |
| 2026-05-22 | 沉淀设计思想到 `docs/design-thinking.md` | 让设计判断可被复用、可被未来 Agent 协作者继承 |

设计思想完整总结见 [`docs/design-thinking.md`](./docs/design-thinking.md)。

## 优先级原则

1. **真实部署 > 设计完美** —— Skill 在 AstronClaw 上跑通 > README 多打磨一段
2. **演示视频 > 功能堆砌** —— 30 秒展示真实闭环 > 10 个功能列表
3. **SkillHub 公开 > 闭门 demo** —— 不发布到 SkillHub 等于没参赛
4. **设计判断沉淀 > 一次性产出** —— 重要决策必须进 `memory/`，不止在 git log

## Kiro 行为约定

1. **不要假设** —— Schema / 字段不确定时先问，不凭空补全
2. **最小改动** —— 只改用户要求的部分，不顺手重构无关代码
3. **先理解再动手** —— 阅读相关文件和上下文后再给方案
4. **保持风格一致** —— 匹配项目现有的 Markdown 格式 / 命名 / 色板
5. **不要自动 commit & push** —— commit 后等用户 review 并明确授权
6. **遵循 cascade-maintain** —— 改一个文件，主动检查下游联动；不止动用户指的那一个
7. **沉淀到 memory** —— 重要决策与判断写入 `memory/`，不止在 commit message
8. **保持双套对称** —— 改 `.kiro/skills/` 时同步 `.claude/skills/`；改 `steering.md` 时同步 `CLAUDE.md`
