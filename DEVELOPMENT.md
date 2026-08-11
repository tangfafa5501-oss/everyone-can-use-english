# 开发环境与启动说明

## 必需环境

- Git
- Node.js 22 或更高的受支持 LTS 版本
- 仓库固定的 Yarn 4.6.0；不要混用 npm、pnpm 或 Bun 更新依赖
- 至少数 GB 可用磁盘空间，用于依赖、Electron 打包结果和可选语音模型

仓库已经提交 `.yarn/releases/yarn-4.6.0.cjs`。启用 Corepack 后，根目录的 `packageManager` 配置会选择正确的 Yarn：

```bash
corepack enable
yarn --version
yarn install --immutable
```

预期 Yarn 版本为 `4.6.0`。`--immutable` 可避免安装过程意外修改锁文件。Node.js 20 已停止官方安全维护，因此不再作为推荐开发环境。

## 平台注意事项

### Windows

- 推荐 Node.js 22 x64、Git for Windows 和 PowerShell。
- 必须通过 Yarn 运行仓库脚本；Yarn 的可移植脚本环境会处理项目中使用的类 Unix 环境变量语法。
- 如果 PowerShell 执行策略阻止 `npm.ps1` 或 `yarn.ps1`，请使用 `npm.cmd`、`yarn.cmd`；无需为了运行本项目而放宽系统执行策略。
- 如果 `sqlite3` 等原生模块没有可用的预编译包，需要安装 Python 3 和 Visual Studio Build Tools 的“使用 C++ 的桌面开发”组件。

### macOS

- 打包目标包含 Intel 和 Apple Silicon。
- 原生依赖构建可能需要 Xcode Command Line Tools。
- CI 在 macOS 13 上额外安装 SDL2；本地遇到相关链接错误时可执行 `brew install sdl2`。
- 签名和公证只在正式发布时需要 Apple Developer 凭据。

### Linux

- Electron 图形测试需要可用的显示服务；CI 使用 `xvfb-run`。
- 制作 deb 包需要 Electron Forge 对应的系统打包工具。

## 常用命令

```bash
# VitePress 内容站
yarn docs:dev
yarn docs:build

# Nuxt 门户
yarn portal:dev
yarn portal:generate

# Enjoy 桌面端（线上 API）
yarn enjoy:start

# Enjoy 桌面端（本地 API :3000）
yarn enjoy:dev

# 桌面端质量检查
yarn enjoy:lint
yarn enjoy:test:main
yarn enjoy:test:renderer
yarn enjoy:package
```

## 桌面端环境变量

| 变量 | 用途 | 是否必需 |
| --- | --- | --- |
| `WEB_API_URL` | 覆盖 HTTP API 地址 | 否 |
| `WS_URL` | 覆盖 WebSocket 地址 | 否 |
| `SETTINGS_PATH` | 隔离设置目录，常用于测试 | 否 |
| `LIBRARY_PATH` | 覆盖媒体库和数据库目录 | 否 |
| `HTTP_PROXY` / `HTTPS_PROXY` | 词典下载代理 | 否 |
| `PACKAGE_OS_ARCH` | 交叉打包时覆盖目标架构 | 否 |
| `NODE_OPTIONS` | 打包时调整 Node 内存等参数 | 否 |

项目没有自动加载根目录 `.env` 文件；请在启动进程或 CI 中显式设置变量。不要创建或提交包含真实密钥的配置文件。

## 后端边界

本仓库没有 `enjoy.bot` 对应的业务后端源码，也没有本地后端容器编排。`yarn enjoy:dev` 假定以下服务已经在本机运行：

- HTTP API：`http://localhost:3000`
- WebSocket：`ws://localhost:3000`

没有后端时可用 `yarn enjoy:start` 连接公开线上服务，但开发测试应避免修改真实线上数据。长期维护建议根据 `enjoy/src/api/client.ts` 建立 Mock API，或者取得兼容后端及其数据模型、鉴权和 WebSocket 协议文档。

## 本地数据与大文件

- SQLite 数据库和媒体默认位于 `EnjoyLibrary`。
- 测试通过 `SETTINGS_PATH` 和 `LIBRARY_PATH` 使用隔离目录。
- Whisper 模型可能在首次使用相关功能时下载。
- `enjoy/out/`、`.vite/`、测试报告和临时目录已被 Git 忽略。

开发数据库模型时必须同时提供迁移，不要直接修改用户现有 SQLite 文件。

## 发布与部署环境

以下变量只供项目维护者发布使用：

| 范围 | 变量或 GitHub Secret |
| --- | --- |
| GitHub Release | `GITHUB_TOKEN` / `PUBLISH_TOKEN` |
| macOS 签名 | `MACOS_CERTIFICATE_APPLICATION_BASE64`、`MACOS_CERTIFICATE_PASSWORD` |
| macOS 公证 | `APPLE_ID`、`APPLE_APP_PASSWORD`、`APPLE_TEAM_ID` |
| S3 兼容存储 | `S3_ACCESS_KEY_ID`、`S3_SECRET_ACCESS_KEY`、`S3_ENDPOINT` |
| Cloudflare | `CF_BASEONE_API_TOKEN`、`CF_BASEONE_ACCOUNT_ID` |
| 阿里云 OSS | `GLOBAL_OSS_ACCESS_KEY_SECRET` 以及工作流引用的 OSS 地址变量/密钥 |

普通本地开发不需要以上任何发布凭据。

## 建议的验证顺序

1. `yarn install --immutable`
2. 修改内容站时运行 `yarn docs:build`
3. 修改门户时运行 `yarn portal:generate`
4. 修改桌面端时运行 `yarn enjoy:lint`
5. 根据影响范围运行主进程或渲染进程 E2E
6. 涉及原生模块、安装器或发布配置时运行 `yarn enjoy:package` 或 `yarn enjoy:make`

## 仅提交代码到 GitHub

将源码推送到 GitHub 只需要 Git 和 GitHub 登录，不需要 Cloudflare、阿里云、Docker、Wrangler、应用签名证书或对象存储密钥。Node 和 Yarn 用于验证项目，不是执行 `git push` 的必要条件。

Windows 上推荐使用 Git Credential Manager 完成 HTTPS 登录。首次推送如果出现浏览器授权提示，登录拥有目标仓库写入权限的 GitHub 账号即可；不要把 Personal Access Token 写入仓库文件或远程 URL。
