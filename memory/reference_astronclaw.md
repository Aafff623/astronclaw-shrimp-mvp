---
name: astronclaw-reference
description: AstronClaw 平台 / 赛事关键链接 + Schema 校准注意 + 沙箱合规要点
metadata:
  type: reference
---

讯飞 AstronClaw 平台与赛事相关的外部参考清单。

## 关键链接

| 用途 | URL |
|------|-----|
| 比赛官网 | https://challenge.xfyun.cn |
| 讯飞开发者社区 | https://developer.xfyun.cn/ |
| 讯飞官网 | https://www.xfyun.cn/ |
| 本项目仓库 | https://github.com/Aafff623/astronclaw-shrimp-mvp |

## 平台核心能力（参赛卖点）

- **端云一体** —— Agent 既能云端调度，也能边缘执行
- **零代码 / 低代码 Skill** —— YAML / JSON 声明式，无需 Docker / Node
- **沙箱隔离** —— 国家信息安全三级认证
- **多模态** —— 语音 / 视觉 / RPA 执行原生支持
- **一键部署** —— 1 分钟上线，浏览器直接访问
- **SkillHub** —— 公开 Skill 仓库，社区评价基础设施

## ⚠️ Schema 校准注意

`skills/weekly-digest.yaml` 中的 schema 字段（如 `trigger.type` / `steps[].type` / `output_format`）
**以 AstronClaw v1 草案为参考**，正式部署前需对照官方 SDK / SkillHub 模板文档校准：

- 字段名可能不同（如 `cron` vs `schedule`）
- LLM 模型 ID 以平台实际可用为准（`spark-x1` 仅占位）
- `multimodal.image_generate` 接口名待官方确认
- 沙箱网络白名单字段格式以平台规则为准

**How to apply**：部署遇到 Schema 错误时，先查官方 SDK 文档，再校准 YAML 字段名，最后重新发布。
不要凭空猜字段名。

## 沙箱合规要点

- 不允许任意 HTTP 出站，必须显式声明 `security.network_allowlist`
- 不允许本地文件读写 / 系统 API 调用
- Skill 内容必须积极健康（不涉及政治敏感 / 暴力 / 低俗）
- API Key / Webhook URL 通过平台环境变量管理，不能写死在 YAML

## 关联

- [[project_skill_direction]]：基于平台能力反推 Skill 方向
- [[project_agent_five_factors]]：平台能力对应五要素的映射
