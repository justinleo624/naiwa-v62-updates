# 奶蛙邮局 V6.2 Beta 签名自动更新通道

**当前公开自动更新版本：`0.6.2-beta.8`（2026-11-07）**，适用于 Windows x64 和 macOS Apple Silicon（ARM64），暂不提供 Mac Intel 版本。

- [Beta.8 Windows / Mac 正式签名预发布安装包](https://github.com/justinleo624/naiwa-v62-updates/releases/tag/v0.6.2-beta.8)
- [当前公开自动更新清单 `beta/latest.json`](https://raw.githubusercontent.com/justinleo624/naiwa-v62-updates/main/beta/latest.json)
- [Beta.8 真实重启后收信验收 Issue #62](https://github.com/justinleo624/naiwa-desktop-v6/issues/62)

## 旧版用户如何收到升级

已经安装并正在运行的 Beta.6 客户端，会在启动后自动检查新的签名版本，也可以手动打开「设置 → 桌面更新」检查更新。当提示 Beta.8 可安装时，**用户需要点击「安装更新」**；目前不进行无提示强制静默安装。

**如果电脑刚重启而原 Beta.6 没有自动启动，请先手动打开一次奶蛙。** 原 Beta.6 无法在自身未运行时检测更新。成功安装 Beta.8 并登录后，到「设置 → 通用与更新」启用「开机登录后自动待命」，之后才会在用户登录系统时尝试自动隐藏启动并在托盘收信。该功能遵循用户明确开启/关闭的偏好，退出应用后不会在关机期间表演。

## Beta.8 更新安全性

- [GitHub Actions #42347930268](https://github.com/justinleo624/naiwa-desktop-v6/actions/runs/42347930268)：Windows x64 / Mac ARM64 的原生编译、Rust 测试和 Node/API 回归通过。
- [GitHub Actions #42348664051](https://github.com/justinleo624/naiwa-desktop-v6/actions/runs/42348664051)：Node/API/UI **178/178**、Beta.7/Beta.8 专项 **14/14** 通过。
- [GitHub Actions #42348916612](https://github.com/justinleo624/naiwa-desktop-v6/actions/runs/42348916612)：两平台原有更新密钥的签名候选包构建通过。
- [GitHub Actions #42349510691](https://github.com/justinleo624/naiwa-desktop-v6/actions/runs/42349510691)：独立 Minisign 验签、篡改拒绝和旧 Beta.6 密钥连续性验证通过。
- 2026-11-07 [更新 PR #1](https://github.com/justinleo624/naiwa-v62-updates/pull/1) 合并后，客户端公开更新清单从 Beta.6 切换为 Beta.8；旧签名包和历史 Release 不变，未修改 Render 数据。
- Beta.8 真实 Windows 和 Mac 上「重启 → 自动隐藏启动 → 自动收到好友来信并且只签收一次」的端到端验收尚未完成，**不能把自动升级成功视为开机收信已通过**。

## 历史

Beta.3、Beta.4、Beta.5、Beta.6 原有签名 Release 仍保留；本次 Beta.8 继续使用与 Beta.6 相同的 Tauri 更新签名公钥。系统会验证签名与版本，禁止不受控的版本回退。Tauri 更新签名不同于 macOS Developer ID 公证和 Windows Authenticode。

**保密要求**：本仓库不包含任何 Tauri 私钥、Render 内测口令、数据库、个人恢复码或私有应用源码。
