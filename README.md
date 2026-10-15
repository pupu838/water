# 农业水利 × 遥感｜100 篇论文研究导航

纯静态文献导航页（HTML + CSS + JavaScript），包含 50 篇博士论文与 50 篇期刊论文。

## 功能和注意事项

入口为 `index.html`。支持关键词搜索、按研究方向筛选、收藏和阅读笔记。收藏与笔记保存在本设备浏览器的 localStorage 中，不会自动跨设备同步。

文献数据来自此前整理的 100 篇论文表。少量论文已提供核实过的原文入口，其余以检索入口为主；用于正式论文引用前，请再核实题名、作者、发表年份和 DOI。

## 腾讯云 CloudBase 静态网站托管

推荐从 [腾讯云开发控制台](https://console.cloud.tencent.com/tcb) 直接导入本仓库：

1. 登录腾讯云，在云开发中创建/选择环境并开通静态网站托管。
2. 选择「静态网站托管」→「新建部署」→「Git 仓库」→「公开仓库」。
3. 仓库地址填写 `https://github.com/pupu838/water.git`，分支选择 `main`。
4. 选择纯静态 HTML 项目（无需安装依赖或构建命令），入口为根目录的 `index.html`，部署路径为 `/`；若界面要求构建产物目录，尝试填写 `.`。
5. 控制台部署成功后会给出实际的公网访问域名。不要根据环境 ID 自行猜测。

腾讯云使用要求和费用，以控制台显示为准。

官方文档：https://docs.cloudbase.net/hosting/web-hosting

## GitHub Actions 自动发布到腾讯云（可选）

仓库提供 `.github/workflows/cloudbase.yml`。默认不部署，直到启用。

1. 在 GitHub 仓库 Settings → Secrets and variables → Actions → Secrets 中，配置 `TCB_SECRET_ID`、`TCB_SECRET_KEY` 和 `TCB_ENV_ID`。
2. 在相同页面 Variables 中增加 `TCB_ENABLED=true`。
3. 在 Actions 中手动运行「Deploy to Tencent CloudBase」，以后更新 `index.html` 会自动重新部署。

**不要将腾讯云 SecretKey 放进代码或聊天消息。** 推荐为部署创建最小权限凭据。

官方文档：https://docs.cloudbase.net/hosting/cli-devops
