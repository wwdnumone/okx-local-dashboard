# GitHub 发布指南

本指南将当前项目作为开源代码仓库发布。项目已整理好，发布时不需要修改运行代码。

## 1. 确定仓库信息

推荐仓库名：

```text
okx-local-dashboard
```

推荐 GitHub Description（可直接复制）：

```text
单文件 HTML 的 OKX 只读交易数据台，支持成交、订单、持仓和资产查询，多类型合并、本地凭证配置及 CSV/JSON 导出。无需安装或后端。
```

可选英文简介：

```text
A single-file, read-only OKX dashboard for trades, orders, positions and balances, with local credential settings and CSV/JSON export. No installation or backend required.
```

推荐 Topics：

```text
okx
okx-api
trading-dashboard
html
javascript
local-first
read-only
csv-export
```

项目已附 MIT 许可证，版权行写为 `2026 OKX Local Dashboard contributors`。MIT 允许他人使用、修改、再分发和商业使用，但要求保留版权及许可证。接受这一授权方式即可保留；如需换成自己的版权署名，请在首次公开前修改 LICENSE 的版权行。

## 2. 网页上传，不用安装 Git

### 创建仓库

1. 注册或登录 [GitHub](https://github.com/)。
2. 打开 [新建仓库](https://github.com/new)。
3. Repository name 填 `okx-local-dashboard`。
4. Description 粘贴上面的中文或英文简介。
5. Visibility 选 **Public**。
6. 不另外初始化 README、`.gitignore` 或 License；项目包中已有这些文件。
7. 点击 **Create repository**。

### 上传文件

1. 解压项目 ZIP。
2. 进入解压后的 `okx-local-dashboard` 文件夹。
3. 在空仓库页面点击 **uploading an existing file**；非空仓库通常使用 **Add file → Upload files**。
4. 上传这个文件夹的**内部文件和子目录**，不要只上传 ZIP，也不要在仓库里再套一层同名文件夹。
5. 确认仓库根目录将包含 `index.html`、`README.md`、`LICENSE` 等，`docs` 和 `tests` 目录保持原结构。
6. Commit message 可以填写 `Initial release: OKX Local Dashboard`。
7. 点击 **Commit changes**。

`.gitignore` 是隐藏文件。macOS Finder 可按 `Command + Shift + .` 显示隐藏文件；Windows 可打开“显示隐藏的项目”。也可以随后通过 **Add file → Create new file** 创建 `.gitignore` 并粘贴项目包中对应内容。

上传完成后，首页应直接显示 README，而不是只看到一个压缩包或需要再进入一层目录。

### 设置仓库简介

在仓库首页右侧 **About** 区域点击设置图标：

- 填写 Description。
- 添加需要的 Topics。
- 没有独立在线演示时，Website 可留空。

本项目支持下载后本地打开，不需要启用 GitHub Pages。仅公开代码与提供在线网页是两项不同的操作；如将来部署 Pages，需单独验证跨域策略和网站来源下的凭证存储行为。

## 3. 发布 v1.0.0 下载版本

GitHub 仓库可以直接下载源码；Release 方便用户一眼找到可运行文件。

1. 在仓库页面进入 **Releases**，点击 **Create a new release** 或 **Draft a new release**。
2. 创建标签 `v1.0.0`，目标分支选 `main`（或仓库实际默认分支）。
3. 标题填写 `v1.0.0 · 首个公开版本`。
4. 发布说明可使用下文模板。
5. 将仓库中的 `index.html` 作为附件上传。它不含真实凭证，可单独下载运行。
6. 如果已经决定正式公开该版本，点击 **Publish release**；尚需检查时先保存为草稿。

GitHub 会自动提供源码 ZIP / tar.gz；不必手动重复上传源码包。

### 发布说明模板

```markdown
首个公开版本：通过本地单文件 HTML 查询 OKX 个人交易数据。

功能：
- 查询成交明细、历史订单、当前委托、持仓和交易账户资产。
- 支持所有产品类型合并展示、独立分页及继续加载。
- 在网页中配置 API 凭证，可选保存在当前浏览器。
- 支持 CSV / JSON 导出、演示模式、侧栏折叠和返回顶部。

使用方法：
下载附件 index.html，用现代浏览器打开；先点击“查看演示”预览，再填写只读 API Key、Secret Key 和 Passphrase。

说明：
- 记住凭证使用当前浏览器 localStorage，未加密，适合个人可信设备。
- 实际接口读取受地区、账户权限、网络和 CORS 策略影响。
- 逻辑测试使用模拟接口，不代表所有地区的真实账户环境均已验证。
```

## 4. 确认上传的是项目文件

本项目包的 `index.html` 默认凭证为空。你在浏览器中“记住”的凭证存储在浏览器内，不会自动写入这个 HTML 文件。

不要额外放入填写过真实凭证的配置、账户导出 CSV / JSON、浏览器网络日志或真实账户截图。需要展示界面时使用“查看演示”截图。

`.gitignore` 仅是辅助规则，不能保证阻止网页上传或所有敏感文件。若误将真实密钥公开，请先在 OKX 撤销该 Key；只删掉最新文件不能移除 Git 历史中的秘密。

## 5. 可选：使用 Git 命令行上传

如果更习惯命令行，可用这一方式代替网页上传。先按前文创建一个**空仓库**，并确保本机已安装 Git、完成 GitHub 的 HTTPS 凭证或 SSH 登录配置。

在本地项目根目录打开终端，执行：

```bash
git init
git branch -M main
git add index.html README.md LICENSE .gitignore config.example.txt CHANGELOG.md docs tests
git commit -m "Initial release: OKX Local Dashboard"
git remote add origin https://github.com/YOUR_USERNAME/okx-local-dashboard.git
git push -u origin main
```

将 `YOUR_USERNAME` 替换为你的真实 GitHub 用户名；若仓库名不同，也要对应替换。GitHub 不支持使用账户密码完成 Git HTTPS 推送，请使用 GitHub 支持的凭证管理器、个人访问令牌或 SSH；不要将令牌写入仓库文件或 remote URL。

如果这是已有 Git 仓库或已经配置过 origin，不要重复初始化或盲目替换远程地址，应先检查现有状态。

## 6. 以后更新版本

网页方式：通过 **Add file → Upload files** 上传更新后的同名文件，写清更新说明并提交。需要改文档时，可打开文件后点击编辑按钮。

命令行方式：

```bash
git add index.html README.md docs CHANGELOG.md tests
git commit -m "Describe the change"
git push
```

将示例提交说明改为实际修改内容。发布新版本时更新 `CHANGELOG.md`，并创建新的标签和 Release，例如 `v1.0.1`；不要覆盖旧版本的记录。

运行逻辑测试需要 Node.js 18 或更新版本：

```bash
node tests/dashboard.test.cjs
```

测试不会向 OKX 发起真实请求。若变更了接口逻辑，还需使用自己的只读 Key 验证对应账户场景，并如实记录实际验证范围。
