# hipostoffice.com — 已上线 Worker 官网与中国大陆下载验收

更新：2026-10-24。**旧的 Cloudflare Pages 创建步骤已不再需要。** 用户现在已经把 `hipostoffice.com` 绑定到 Cloudflare Worker `naiwa-v62-updates` 的 Production 环境。

## 当前真实状态

| 项目 | 实际结果 |
| --- | --- |
| 域名注册与 Cloudflare 管理 | 已完成 |
| Worker Production 绑定 hipostoffice.com | 已由用户控制台截图确认 |
| 正式官网 https://hipostoffice.com/ | 用户已确认看见奶蛙邮局下载页 |
| 云端校验：HTTPS 首页 | PASS（不是人工浏览截图） |
| 云端校验：官网下载 Windows EXE | 完整下载、大小+SHA-256 PASS |
| 云端校验：官网下载 Mac DMG | 完整下载、大小+SHA-256 PASS |
| 中国大陆电信/联通/移动节点 | 未验收；不可承诺各地均能访问或测速 |
| 已安装 Beta.4 的 Tauri 自动更新 | GitHub URL 渠道；与首页下载网络不同 |

### 已完成的真实外部下载验收

[GitHub Actions 工作流 40106737016](https://github.com/justinleo624/naiwa-v62-updates/actions/runs/40106737016) — **SUCCESS**。

执行环境是 **GitHub 托管的海外云端运行器，不是中国大陆网络**。

此任务直接通过官方 HTTPS 域名访问页面、下载两个真实安装包，再对下载文件进行 SHA-256 校验：

- `https://hipostoffice.com/` — 验证奶蛙邮局、Beta.4 和两项下载安装链接
- `https://hipostoffice.com/downloads/naiwa-windows-x86_64.exe`
  - 4,758,108 字节；SHA-256 `b03a675183e5fe5082cb2b5919d9dfdd07138671c4b73341cca4c9dbeb431776`
- `https://hipostoffice.com/downloads/naiwa-darwin-aarch64.dmg`
  - 7,152,123 字节；SHA-256 `bca734dd39c7ef94b97c96f896e4b43c7b6b0987eac4cb5c29267cb1f188541e`
- 回归验收工作流：`.github/workflows/verify-hipostoffice-live.yml`。可以手动执行，不修改站点、版本或用户数据库。

官网的静态构建/下载资源仍存放在公开仓库 `site/`，经过 SHA-256 签核之后 Cloudflare Worker 发布给 `hipostoffice.com`。

## 中国大陆真实线路验收（尚未完成）

使用 [ITDOG 网站测速](https://www.itdog.cn/http/)：

1. 在输入框测试 `https://hipostoffice.com/`，请求方法选择 GET，勾选 **中国电信、中国联通、中国移动**，执行网站测速。
2. 查看三运营商在多个省份是否能完成 DNS 解析、TLS 握手、返回 **HTTP 200**，以及平均耗时/失败率。如果失败率高则不标记国内 GO。
3. 再对 `https://hipostoffice.com/downloads/naiwa-windows-x86_64.exe` 测 HTTP 请求及响应状态。多节点网页测速可能会读取/下载全部文件且占用带宽，短时间内只需少量代表节点；不必对每个节点下载所有文件。
4. 在实际中国大陆家庭宽带和手机热点各完整下载安装一次（例如校园网 + 中国移动/电信），计算完整文件 SHA-256。在线测试器检测到 200 **不等于** 下载几 MB 内容不会中断。
5. 对 Beta.4 应用内签名自动更新使用的两条 GitHub 地址也进行独立检查：
   - `https://raw.githubusercontent.com/justinleo624/naiwa-v62-updates/main/beta/latest.json`
   - `https://github.com/justinleo624/naiwa-v62-updates/releases/download/v0.6.2-beta.4/naiwa-windows-x86_64.exe`
   
   如果更新源在大陆线路上无法访问，未来 Beta.5 的 **签名编译前**应规划官网托管更新清单和更新归档（Mac `.app.tar.gz` + Windows `.exe` 及对应 `.sig`），使新版本的内置 updater URL 指向自有域名；仅修改官网首页不会改变已经发布客户端内部的更新服务器。

**不要把 GitHub 美国运行器的成功误称为中国大陆网络验收。** Cloudflare 普通全球网络不等于中国境内网络，具体实际可用性取决于运营商、省份、DNS 和跨境路由。若失败率明显偏高，应增加网络可用的境外/香港或合规大陆镜像方案，再发布给大范围中国大陆用户。

## 后续 Beta.5

Beta.5 在私有应用仓库 PR #36 开发，尚未正式发布；官网暂时只展示已验签的 Beta.4。Beta.5 在 Mac/Windows 两平台正式签名并发布之前，不得让首页下载按钮指向虚假的新版文件。届时先在 `site/downloads/` 中用哈希固定新安装包并完成外部 HTTPS 下载验证，最后更新页面的显示版本和双平台下载资源。
