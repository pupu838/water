# 农业水利 × 遥感｜100 篇论文研究导航

## 长期公开网址：GitHub Pages（待首次启用）

本仓库新增独立的 [GitHub Pages 自动发布工作流](.github/workflows/github-pages.yml)，无需域名购买或额外的部署密钥，网页仍然使用本仓库 `main/index.html`。每次更新 `index.html` 将自动重新发布；EdgeOne Makers 的旧网站不会因此被删除。

**首次启用必须由仓库管理员在 [Settings → Pages](https://github.com/pupu838/water/settings/pages) 完成一次设置**：

1. 在 Build and deployment 下将 **Source** 设为 **GitHub Actions**。
2. 在 [发布工作流](https://github.com/pupu838/water/actions/workflows/github-pages.yml) 重新运行此前失败的任务，或手动运行工作流。
3. 只有部署显示成功后，正式使用 `https://pupu838.github.io/water/`。

说明：此方案不再依赖 EdgeOne 三小时预览链接，但并不保证 `github.io` 在中国大陆每条网络上都能始终正常访问；需通过实际网络测试。若未来必须确保中国大陆长期稳定使用，仍应考虑已合规的自定义域名与境内托管方案。

## 当前线上部署：腾讯云 EdgeOne Makers

本仓库 `main/index.html` 是农业水利与遥感 100 篇论文网页的**唯一源码入口**。

- 腾讯云 Makers 项目：`agri-water-remote-sensing-library`
- 项目 ID：`makers-n3bdnbdo1ez0`
- 自动发布工作流：[`pupu838/chatgpt-share-text-extractor` → `deploy-agri-water-edgeone.yml`](https://github.com/pupu838/chatgpt-share-text-extractor/blob/master/.github/workflows/deploy-agri-water-edgeone.yml)
- 复用旧仓库已有的 `EDGEONE_API_TOKEN` GitHub Secret；凭证没有复制到本仓库。
- 工作流每 15 分钟读取本仓库 `main` 分支，仅当 Git SHA 尚未发布时才向独立 Makers 项目部署。
- 已验证首次 EdgeOne 正式发布成功，且云端 HTTP 访问返回 200、存在农业水利相关页面内容。
- EdgeOne 默认域名在中国大陆可能要求带有 3 小时有效期的预览签名 URL。请从 [项目控制台](https://console.cloud.tencent.com/edgeone/pages/project/makers-n3bdnbdo1ez0) 获取最新访问入口；需要长久可靠地在中国大陆公开访问时，应考虑符合当地要求的自定义域名。
- CloudBase 环境已由用户于 2026-10-15 确认销毁；历史部署说明仅为存档，不再作为有效发布渠道。

以后修改网站时，编辑本仓库根目录 `index.html` 即可；不需要同步修改旧提取器的网页代码。自动发布可能有定时轮询与平台队列延迟，并非立即生效。

---


纯静态文献导航页（HTML + CSS + JavaScript），包含 50 篇博士论文与 50 篇期刊论文。

## 功能和注意事项

入口为 `index.html`。支持关键词搜索、按研究方向筛选、收藏和阅读笔记。收藏与笔记保存在本设备浏览器的 localStorage 中，不会自动跨设备同步。

文献数据来自此前整理的 100 篇论文表。少量论文已提供核实过的原文入口，其余以检索入口为主；用于正式论文引用前，请再核实题名、作者、发表年份和 DOI。

## 历史方案：腾讯云 CloudBase 静态网站托管（环境已销毁）

推荐从 [腾讯云开发控制台](https://console.cloud.tencent.com/tcb) 直接导入本仓库：

1. 登录腾讯云，在云开发中创建/选择环境并开通静态网站托管。
2. 选择「静态网站托管」→「新建部署」→「Git 仓库」→「公开仓库」。
3. 仓库地址填写 `https://github.com/pupu838/water.git`，分支选择 `main`。
4. 选择纯静态 HTML 项目（无需安装依赖或构建命令），入口为根目录的 `index.html`，部署路径为 `/`；若界面要求构建产物目录，尝试填写 `.`。
5. 控制台部署成功后会给出实际的公网访问域名。不要根据环境 ID 自行猜测。

腾讯云使用要求和费用，以控制台显示为准。

官方文档：https://docs.cloudbase.net/hosting/web-hosting

## 历史方案：CloudBase GitHub Actions（环境已销毁）

已部署的网站不需要重新创建。自动化工作流 `.github/workflows/cloudbase.yml` 使用现有的 CloudBase 环境和原部署日志中的云端路径 `/agri-water-remote-sensing`，以保留现有路径和域名绑定。

部署源文件为仓库根目录的 `index.html`：工作流运行时自动复制到 `dist/index.html` 并通过 CloudBase CLI 上传。仓库里同时保留 `dist/index.html`，兼容之前在 CloudBase 控制台使用的 `./dist` 部署配置。

### 首次授权（仅一次）

1. 为自动发布创建权限尽量小的腾讯云 CAM 子用户 API 密钥，或者使用已有的专用部署密钥。
2. 前往 [本仓库 Actions Secrets 设置](https://github.com/pupu838/water/settings/secrets/actions)，分别创建三个 Repository secrets：
   - `TCB_SECRET_ID`：腾讯云部署密钥 SecretId
   - `TCB_SECRET_KEY`：腾讯云部署密钥 SecretKey
   - `TCB_ENV_ID`：原网站所属 **环境 ID**（不是环境名称）
3. 前往 [Actions 工作流](https://github.com/pupu838/water/actions/workflows/cloudbase.yml)，选择 `Deploy to Tencent CloudBase`，点击 `Run workflow` 手动运行首次部署；确认成功后，后续对 `main` 分支的 `index.html` 更新将自动发布。

安全说明：不要把腾讯云密钥写入代码、Issue 或聊天内容；如果密钥意外泄露应立即停用并轮换。新建 SecretKey 时请妥善保存，腾讯云后续无法再次显示它。

官方指南：https://docs.cloudbase.net/hosting/cli-devops
