# 奶蛙邮局 V6.2 Beta 签名自动更新通道

**当前公开最新版：`0.6.2-beta.4`**。

- [Beta.4 Windows / macOS 正式内测下载页](https://github.com/justinleo624/naiwa-v62-updates/releases/tag/v0.6.2-beta.4)
- [在线更新清单 `beta/latest.json`](https://raw.githubusercontent.com/justinleo624/naiwa-v62-updates/main/beta/latest.json)
- 清单支持平台：`darwin-aarch64`、`windows-x86_64`。Intel Mac 暂不提供。
- 用户首次安装后自动连接 `https://naiwa-v62-beta3-api.onrender.com`，不需要手动选择服务器。
- Beta.3 历史安装包仍保留。原 Beta.3 与 Beta.4 使用相同 Tauri updater 签名密钥；已安装且启用更新渠道的 Beta.3 可以查询 Beta.4 更新。
- 2026-10-24 [GitHub Actions 40101059953](https://github.com/justinleo624/naiwa-v62-updates/actions/runs/40101059953) SUCCESS：五个文件实际 SHA-256 均与本机独立报告一致；签名绑定 Beta.4，签名者 key ID 与 Beta.3 一致；发布版本包、检查公网下载后，最后更新签名清单。
- 不同版本的真实客户端自动安装/重启仍待实机测试。
- 后续 Beta.5 等版本必须保留此相同公钥和相应受保护私钥，先发布并验签对应 Mac+Windows 归档，再将 `beta/latest.json` 前移。不得回退版本或发布未签名包。

**严格保密**：此仓库不包含任何 Tauri 私钥、Render 内测口令、数据库、个人恢复码或私有应用源码。更新签名与 macOS Developer ID 公证、Windows Authenticode 是不同的机制。
