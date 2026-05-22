---
name: cascade-maintain
description: |
  链式维护：当一个源文件变更后，自动检测并更新所有下游关联文件。用户说"帮我维护一下"、"cascade 一下"、"同步一下"时触发。适用于 astronclaw-shrimp-mvp 项目中任何可能导致多文件联动变更的场景。
---

# Cascade Maintain Skill — AstronClaw Shrimp MVP

改了一个文件，链式更新所有下游关联文件。用户不需要记住影响范围，只需要说"帮我维护一下"。

## 触发场景

- 用户说"帮我维护一下"
- 用户说"cascade 一下"
- 用户说"同步一下"
- 用户说"看看有没有要更新的"
- 每次 Skill 配置变更后自动触发
- 每次部署 URL / SkillHub 链接变更后自动触发

## 工作流程

### Step 1：检测变更源

用 `git diff` 和 `git status` 扫描当前状态，根据结果进入不同模式：

**模式 A：被动追踪**（git status 有变更）

识别变更属于哪个源头：

| 变更文件模式 | 归属变更源 |
|-------------|-----------|
| `skills/*.yaml` 或 `skills/*.json` | Skill 配置变更 |
| `.env.example` | 环境变量结构变更 |
| `deploy.md` | 部署流程变更 |
| `docs/技术报告.md` | 技术架构变更 |
| `screenshots/*` 或 `docs/效果截图/*` | 演示资料更新 |
| `docs/演示视频.md` | 视频链接更新 |
| `README.md` | 结构 / 首屏调整 |

只检查对应链路的下游文件。

**模式 B：主动巡检**（git status 干净）

遍历所有 4 条链路，逐一检查一致性。重点检查：
- README 部署链接 / 部署二维码 是否与最新部署一致
- README 视频链接 是否与 `docs/演示视频.md` 一致
- README 仓库结构树 是否与实际目录一致
- `.env.example` 列表是否覆盖了 Skill 中引用的所有变量

### Step 2：按链路逐一检查

根据识别到的变更源，按对应链路检查每个下游文件：

---

#### 链路 A：Skill 配置变更

```
变更源: skills/*.yaml 或 skills/*.json
↓
1. README.md                       → "核心功能"列表是否增删
                                      + 一键部署链接是否需要重发布
2. deploy.md                       → 部署步骤是否需要新增 Skill 上传环节
3. .env.example                    → 新 Skill 引用的环境变量是否已声明
4. docs/技术报告.md                 → 技术栈表 / 关键代码片段 / Skill 设计章节
                                      是否反映新 Skill
5. SkillHub 上的 Skill              → 提醒用户重新发布 / 升级版本号
```

检查项：
- [ ] README 「核心功能」清单是否覆盖了所有 Skill 提供的能力？
- [ ] README 「一键部署链接」对应的 Skill 是否仍然有效？
- [ ] `deploy.md` 中是否提到了所有 Skill 的部署顺序？
- [ ] `.env.example` 是否声明了 Skill 引用的所有环境变量（未声明会导致部署失败）？
- [ ] `docs/技术报告.md` 的 Skill 配置示例是否与 `skills/` 实际内容同步？

---

#### 链路 B：部署 URL / SkillHub 链接变更

```
变更源: deploy.md / README 部署链接 / 新的 SkillHub 发布
↓
1. README.md                       → 「🚀 一键部署」章节链接 + 二维码图片
2. docs/技术报告.md                 → 文末「参考资料」/ 「项目链接」
3. docs/演示视频.md                 → 录制建议中的 GitHub 仓库地址（若有）
4. screenshots/deploy_qrcode.png   → 二维码是否需要重新生成
```

检查项：
- [ ] README 部署链接是否可访问？（不要写死过期 URL）
- [ ] 二维码图片是否对应最新 URL？
- [ ] 技术报告参考资料是否更新？

---

#### 链路 C：演示资料更新

```
变更源: screenshots/*.png|gif / docs/演示视频.md / 新增演示视频
↓
1. README.md                       → 「演示视频」表格 + 顶部 GIF 引用
2. docs/演示视频.md                 → 视频链接表格 + GIF 路径
3. docs/效果截图/                   → 截图缩略图与 README 引用是否对应
```

检查项：
- [ ] README 引用的 `screenshots/demo.gif` 是否真实存在？
- [ ] `docs/演示视频.md` 与 README 「演示视频」表格内容是否一致？
- [ ] 截图分辨率是否达标（建议 1920×1080 起步）？

---

#### 链路 D：技术架构 / 参赛信息变更

```
变更源: docs/技术报告.md / 参赛作者 / 提交日期
↓
1. README.md                       → 「技术亮点」列表 + 「参赛信息」表格
2. LICENSE                         → 版权年份 / 署名
3. docs/技术报告.md                 → 文档头部 + 最后更新日期
4. .claude/skills/*/SKILL.md       → 触发条件是否仍贴合实际工作流
```

检查项：
- [ ] README 技术亮点是否仍然准确（不要写"已实现"但实际未完成的项）？
- [ ] LICENSE 年份是否为当前年份？
- [ ] 技术报告文末日期是否更新？
- [ ] Skill 描述是否与项目实际使用方式一致？

---

### Step 3：执行更新

对每个需要更新的文件：
1. 先读取当前内容
2. 执行 Edit（级联更新通常不需要用户确认，除非涉及结构性变更）

### Step 4：提交

按 [[git-commit-guide]] 规范分组 commit：
- Skill 改动 → `skill(<name>): ...`
- 部署相关 → `deploy: ...`
- 文档/截图 → `docs: ...` 或 `demo: ...`
- 多文件联动同步 → `chore(cascade): 同步 N 处下游文件 — readme + deploy + env`

等待用户确认后再 push。

## 约束

- **不要假设** —— 检测不到变更源时，问用户而不是猜
- **不要过度更新** —— 只动链路上的文件，不顺手改无关内容
- **真实链接优先** —— 不允许写死占位 URL；部署链接必须可访问
- **环境变量必须对齐** —— Skill 引用什么变量，`.env.example` 就必须声明什么
- **截图 / GIF 必须存在** —— README 引用的图片路径必须真实存在，否则评委看到的是破图
- **参赛信息真实** —— 作者名、日期不可为占位符（提交前必须填实）

## 与其他 skill 的关系

- 完成 cascade 后请用 [[git-commit-guide]] 生成分组 commit
- 大幅 README 改动建议先用 `readme-polish` skill 打磨，再 cascade 同步下游
