# V6.2 Beta 签名自动更新通道

**当前已发布：`0.6.2-beta.3`。**

- 公开安装包：[V6.2 Beta.3 Release](https://github.com/justinleo624/naiwa-v62-updates/releases/tag/v0.6.2-beta.3)
- 更新检查清单：[`beta/latest.json`](https://raw.githubusercontent.com/justinleo624/naiwa-v62-updates/main/beta/latest.json)
- 支持清单平台：`darwin-aarch64` 和 `windows-x86_64`。
- 二进制签名由 Owner 持有的 Tauri 更新私钥产生；本仓库仅公开签名和可验证的更新包，不含私钥。
- 当前清单与 Beta.3 安装包同版本。只有以后发布更高版本且清单更新之后，客户端才应提示升级。
- 同版本安装和静态 manifest 可用 **不等于** 已经过真实的两个不同版本之间自动升级；后者仍需完成测试。
- 将来升级时应继续沿用原始公钥与对应私钥；只在对应两平台签名资产和可公开访问的下载 URL 均 verified 后更新清单。
- 不应把 Render 的 Beta 内测访问口令、用户密钥、聊天数据或任何签名私钥放入此目录。

Render 当前独立 Beta API：`https://naiwa-v62-beta3-api.onrender.com`。历史 Railway 账号和好友不会自动迁移。首次安装后请在客户端高级连接设置里改为 Render 地址并重新注册。
