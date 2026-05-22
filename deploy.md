# AstronClaw 一键部署教程

> 本文档说明如何把本仓库的 Skill 部署到 **科大讯飞 AstronClaw 平台**。
> 全程预计 1 ~ 5 分钟，无需 Docker / Node / Python 环境。

---

## 一、前置准备

### 1. 账号
- 注册 [讯飞开放平台账号](https://www.xfyun.cn/)
- 开通 AstronClaw 平台访问权限（部分功能需实名认证）

### 2. 环境变量
- 复制 `.env.example` 为 `.env`
- 填入 `ASTRONCLAW_API_KEY`、`ASTRONCLAW_APP_ID` 等

---

## 二、部署步骤

### 步骤 1：登录 AstronClaw 控制台
访问 https://www.xfyun.cn/ → 进入 **AstronClaw Agent 平台**。

### 步骤 2：创建新 Skill
- 点击「新建 Skill」
- 名称：`astronclaw-shrimp-mvp`
- 描述：与本仓库 README 一致

### 步骤 3：导入 Skill 配置
- 进入 Skill 编辑器
- 点击「从文件导入」
- 上传 `skills/` 目录下的 `.yaml` / `.json` 文件

### 步骤 4：配置环境变量
在 Skill 设置页面，将 `.env` 中的变量逐项填入「环境变量」面板。

### 步骤 5：测试运行
- 点击「沙箱测试」
- 验证核心流程跑通后再发布

### 步骤 6：发布到 SkillHub
- 点击「发布」→ 选择「公开发布到 SkillHub」
- 完善描述、截图、使用说明
- 这是评审重要依据，**务必勾选公开**

### 步骤 7：获取访问链接
- 发布后会生成访问 URL 和二维码
- 将链接填回 README.md 的「一键部署」章节

---

## 三、常见问题

### Q1：部署失败提示「沙箱权限不足」
A：检查 Skill 中是否调用了未授权的本地文件/系统 API；AstronClaw 沙箱仅允许 HTTP / 平台内置 API。

### Q2：环境变量没生效
A：环境变量修改后需要重新发布 Skill；浏览器缓存可强制刷新。

### Q3：推送到飞书/企业微信失败
A：检查 Webhook URL 是否完整、IP 是否在白名单（部分企业内网需配置）。

---

## 四、参考资源

- [讯飞开发者社区 - AstronClaw 专区](https://developer.xfyun.cn/)
- [比赛官网](https://challenge.xfyun.cn)
- 项目主页：[README.md](./README.md)
