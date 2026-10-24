# hipostoffice.com — Cloudflare Pages 绑定与中国大陆访问验收

## 已完成（实际操作证据）

- 官网页面目录：`site/`（静态 `index.html` + `style.css` + `favicon.svg` + 安全响应头）。
- Windows / macOS 安装按钮使用 **本站同源静态文件**：
  - `/downloads/naiwa-windows-x86_64.exe`，大小 4,758,108 字节，SHA-256 `b03a675183e5fe5082cb2b5919d9dfdd07138671c4b73341cca4c9dbeb431776`
  - `/downloads/naiwa-darwin-aarch64.dmg`，大小 7,152,123 字节，SHA-256 `bca734dd39c7ef94b97c96f896e4b43c7b6b0987eac4cb5c29267cb1f188541e`
- GitHub Actions 已真实从正式 Beta.4 Release 下载两个完整安装包并校验 SHA-256，再提交到公开仓库 `site/downloads`。之后 Cloudflare Pages 的下载链接无需实时跳转 GitHub。
- Render 网页演示站：`https://hipostoffice-download-preview.onrender.com`（部署 Live）。
- Cloudflare Registrar 域名已购买：`hipostoffice.com`。尚需 Owner 在 Cloudflare Dashboard **创建 Pages 项目并绑定自有域名**。无 Cloudflare 插件的 Chat 模式无法自行点 Dashboard 进行写入；DNS 的已读页面之前显示没有根域名 A/CNAME 网站记录。

## Owner 一次性的 Cloudflare 页面操作（无需 Codex）

1. 打开 https://dash.cloudflare.com/dc68be889fd6e119d6a6095f20cac687/workers-and-pages ，点击 **Create application / Pages / Connect to Git**（2026 的导航名称可能略变）。
2. 选择 GitHub `justinleo624/naiwa-v62-updates`。这是一份公开的**纯二进制和静态网页仓库**，绝非私有应用源码。
3. 创建 Pages 项目，建议名称 `hipostoffice-web`，Production branch = `main`。
4. 构建设置：**Framework = None**；**Root directory = `/`（默认）**；**Build command = 留空**（静态无需编译）；**Build output directory = `site`**。
5. 首次 Deploy，确认 Pages 自动给出的 `https://hipostoffice-web.pages.dev` 实际可显示首页与 `/downloads/` 安装包。若 Pages 新版 UI 要求 Build command，填 `echo static`。
6. 打开 Pages 项目的 **Custom domains → Set up a domain**，填写 `hipostoffice.com`。因为此域名由同一个 Cloudflare 账号管理，Cloudflare 通常会自动创建根域名 CNAME 和证书，必须等状态 Active / TLS Issued。选择绑定 www 子域名可选，但不要删除或修改邮件 `mail.hipostoffice.com` 的 SPF / DKIM 等 DNS 记录。
7. 设置 HTTPS（Always Use HTTPS）。核对 `https://hipostoffice.com/`、`https://hipostoffice.com/style.css`、`https://hipostoffice.com/downloads/naiwa-windows-x86_64.exe`、`https://hipostoffice.com/downloads/naiwa-darwin-aarch64.dmg`。
8. 国内验收：用中国电信、联通、移动至少各一条真实线路打开首页，点击下载并对实际下载字节计算 SHA-256；记录成功率、速度、地区、运营商。**不要只用国外节点测速代替国内访问**。若大陆移动/电信访问失败，Cloudflare 免费全球网络不保证稳定，考虑香港/海外镜像或在取得 ICP 备案后选择合规大陆 CDN。

## 绝不混淆

- 域名 Registrar/Cloudflare DNS 并不会自动给根域名提供网站托管。
- Pages 自定义域名的 CNAME 应经由 Pages → Custom domains 添加，而不是手工随意添加指向 pages.dev 的 CNAME。
- 网站静态下载 CDN 是给首次安装用户的；Tauri 自动更新仍走 `https://raw.githubusercontent.com/justinleo624/naiwa-v62-updates/main/beta/latest.json`，要真正保证大陆用户以后能自动升级，还需要测试该 **更新清单和 Release URL** 的国内访问能力，必要时在下一轮已签名构建中一起迁移更新源（不能只改旧版客户端网页）。
- 单文件 25 MiB 以内才可直接放入 Pages；当前两安装包均约 5–7 MB，符合限额。以后大包考虑 Cloudflare R2 / 对象存储。
- 当前官网固定发布 Beta.4。只有 Beta.5 双平台签名包、公开 Release 均完成，且本站镜像 SHA 校验成功，才前移网站的版本显示与安装链接；禁止指向尚未生成的 Beta.5 包。
