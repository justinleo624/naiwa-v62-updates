# 奶蛙邮局 V6.2 Beta.4 — 下载与自动更新

**当前推荐：V6.2 Beta.4。** Windows 和 macOS Apple Silicon 版本已公开，可以发给受邀朋友下载安装。软件默认连接 Render，无需设置服务器地址。

## 下载 Beta.4

**[查看最新版发布页面](https://github.com/justinleo624/naiwa-v62-updates/releases/tag/v0.6.2-beta.4)**

| 平台 | 下载安装 |
| --- | --- |
| Windows 10/11 x64 | [下载 Windows 安装包 (.exe)](https://github.com/justinleo624/naiwa-v62-updates/releases/download/v0.6.2-beta.4/naiwa-windows-x86_64.exe) |
| Mac Apple Silicon（M 系列） | [下载 Mac 安装包 (.dmg)](https://github.com/justinleo624/naiwa-v62-updates/releases/download/v0.6.2-beta.4/naiwa-darwin-aarch64.dmg) |

目前不提供经过发行验收的 Intel Mac 包。仅从以上官方 GitHub Release 下载。

### 朋友们如何开始使用

1. 下载安装 Beta.4 并打开 **奶蛙邮局 Beta**。
2. 软件自动连接 `https://naiwa-v62-beta3-api.onrender.com`，**无需填写或切换服务器地址**；普通界面已隐藏服务器修改入口，网络异常时仍有重新连接功能。
3. 通过组织者私下提供的内测口令创建新账号，或使用已有 Render 用户发来的邀请加入好友。
4. 互相添加好友、发送每日短句；务必保存注册时显示的一次性账号恢复码。

**注意：** Render 是全新的 Beta 邮局。Railway 历史账号、好友和消息没有迁移；旧 Beta.3 用户首次升级到 Beta.4 后，需要在 Render 上重新注册。请勿在 GitHub、截图或公开聊天里发布内测口令。

当前 Render 服务的邮箱、阿里云短信、微信登录尚未开启；客户端会自动隐藏未开放的认证入口。

### 应用内自动更新

Beta.4 带有 Tauri v2 的数字签名自动更新。后续版本发布后，软件可以自动检查新版本，并在用户确认后下载、验签、安装。静态版本检查源：

**[beta/latest.json](https://raw.githubusercontent.com/justinleo624/naiwa-v62-updates/main/beta/latest.json)**

已发布的更新清单版本是 **0.6.2-beta.4**，支持 `darwin-aarch64` 和 `windows-x86_64`。现有 Beta.3 若已启用此更新渠道，可检测到 Beta.4；更新签名密钥与 Beta.3 保持一致。不同版本之间的真实设备自动安装/重启验收还需后续完成，不能把签名验证等同于全面的实机升级测试。

### 发布验证

2026-10-24 [发布工作流 40101059953](https://github.com/justinleo624/naiwa-v62-updates/actions/runs/40101059953) **SUCCESS**：核对两台电脑报告中的同一源码 SHA `97d7feb07a716da7510dbf95c1e6dc0fdcc5018f`，再从 GitHub 草稿下载五个文件逐一校验 SHA-256，检查 Beta.4 更新签名版本与 Beta.3 公钥 ID 一致；公开 Release，检查两个平台的更新包下载，最后才将 `beta/latest.json` 升至 Beta.4。两台本地 Codex 独立验签 PASS 记录在私有源码仓库 PR #35。

Mac 安装包目前是 ad-hoc 签名，尚未取得 Apple Developer ID 公证；Windows 安装包尚无 Authenticode 开发者签名。系统可能提示未验证开发者。**Tauri 更新包签名不等于操作系统开发者签名。** 建议仅限少量熟悉的朋友受邀内测，遇到异常反馈给发布者，勿禁用所有系统安全防护。

旧版 [Beta.3 Release](https://github.com/justinleo624/naiwa-v62-updates/releases/tag/v0.6.2-beta.3) 保留用于历史版本回退/验收，不作为新用户推荐安装包。

本仓库仅发布客户端二进制、更新归档和签名。应用私有源码、数据库、Tauri 私钥、账户凭证均未公开。
