# 奶蛙邮局 V6.2 Beta.3 — 下载与签名更新

**小范围受邀内测已发布。** 这里只存放可公开下载的安装包、更新归档及其签名；私有应用源码、用户数据库和更新签名私钥不在这里。

## 下载安装

**[打开 V6.2 Beta.3 发布页面](https://github.com/justinleo624/naiwa-v62-updates/releases/tag/v0.6.2-beta.3)**

| 设备 | 安装文件 |
| --- | --- |
| Windows 10/11 x64 | [naiwa-windows-x86_64.exe](https://github.com/justinleo624/naiwa-v62-updates/releases/download/v0.6.2-beta.3/naiwa-windows-x86_64.exe) |
| Mac Apple Silicon (M1/M2/M3/M4/更新型号) | [naiwa-darwin-aarch64.dmg](https://github.com/justinleo624/naiwa-v62-updates/releases/download/v0.6.2-beta.3/naiwa-darwin-aarch64.dmg) |

暂不提供经过正式验收的 Intel Mac 安装包。当前 Windows 安装包尚无独立 Authenticode 开发者签名，Mac 使用 ad-hoc 签名且尚未 Apple 公证；系统可能要求手动确认安装。仅从上述 GitHub 官方仓库页面下载，不要关闭系统全部安全保护。

## 安装后连接全新 Render 邮局

这批冻结的 Beta.3 安装包**原先以 Railway Beta 为默认地址**。由于后端已迁到 Render，而且不迁移历史账号，首次使用需要切换一次服务器：

1. 打开“奶蛙邮局 Beta”（不要误开 V6.1 稳定版）。
2. 登录页展开 **高级连接设置**，将服务器 URL 改为 **`https://naiwa-v62-beta3-api.onrender.com`**，点击 **测试连接并重试**。
3. 由组织者通过私人渠道提供 **Render Beta 内测口令**，然后创建新账号并单独保存一次性恢复码。请不要将口令写在公开 GitHub 评论中。
4. 两位朋友都使用同一个 Render URL，随后相互邀请、加好友和发送消息。旧 Railway 账号/密钥不能用于 Render。

目前 Render 只开放封闭口令内测；邮箱、手机号、微信登录尚未开放。

## 应用内自动更新

这批 Beta.3 是带 Tauri 签名更新能力的候选安装包：使用相同 Beta 更新公钥构建的后续安装包，可以通过应用内 **检查更新 → 下载 → 验签 → 安装** 流程升级。

公开静态更新源：[`beta/latest.json`](https://raw.githubusercontent.com/justinleo624/naiwa-v62-updates/main/beta/latest.json)。

当前清单版本是 **0.6.2-beta.3**，与首次安装版本相同，所以 Beta.3 用户现在“检查更新”应显示已是最新版。**完整跨版本实际升级仍待后续更高 Beta 版本进行真实双机验证**，不能把签名文件通过测试当成已经完成自动升级实测。

更新包由 Tauri 自身签名验证；它不同于 macOS 开发者身份签名或 Windows 安装包的操作系统信任签名。所有后续更新必须继续使用与已发布 Beta.3 相同的 Tauri 更新签名密钥。

## 发布验证与安全说明

2026-10-24 GitHub Actions [真实验收与发布记录](https://github.com/justinleo624/naiwa-v62-updates/actions/runs/40091395545) 成功：从草稿 Release 下载五个历史签名候选文件，逐一核对 SHA-256（全部 PASS），核对真实 `.sig` 内容，公开该不可覆盖的 Beta.3 预发布版本、检查公开下载地址，最后发布两平台更新清单。此前 Mac/Windows 本机 Codex 曾报告相同公钥验签及篡改拒绝 PASS；此处未重复对二进制进行独立公钥验签，也尚未进行 Render 真实双机 GUI 联调。

该应用为邀请制小规模测试产品，不要发送敏感私信或在未取得许可的情况下大规模分发受版权保护的角色素材。旧 Railway Beta 后端与历史数据保持原样。

## 更新发布维护

公开仓库中的 [受控 Beta.3 发布工作流](https://github.com/justinleo624/naiwa-v62-updates/actions/workflows/publish-verified-beta3.yml) 只处理已锁定哈希的 Beta.3 文件，不会构建私有源码或自动发布任意新版本。发布 Beta.4 时需要由维护者使用同一私钥生成并验证新的安装包和签名，再更新版本化 Release 及 `beta/latest.json`，且绝不回退到旧版清单。
