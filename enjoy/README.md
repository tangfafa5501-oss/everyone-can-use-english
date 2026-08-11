# Enjoy 桌面端

Enjoy 是基于 Electron、React、TypeScript、Vite 和 SQLite 的桌面应用，支持 Windows、macOS 和 Linux。

## 开始之前

请先阅读仓库根目录的 [开发环境说明](../DEVELOPMENT.md)。所有命令均建议从仓库根目录运行，并使用仓库固定的 Yarn 版本。

## 启动

使用线上 Enjoy API 启动：

```bash
yarn install --immutable
yarn enjoy:start
```

连接本地 API（默认 `http://localhost:3000`）：

```bash
yarn enjoy:dev
```

本地后端源码不包含在本仓库中。如果没有兼容后端，请使用 `yarn enjoy:start`，或只开发不依赖账号、同步和托管 AI 的本地功能。

首次启动会校验内置词典。语音模型会按功能需要另行下载，因此需要网络和足够的磁盘空间。

## 检查与构建

```bash
yarn enjoy:lint
yarn enjoy:test:main
yarn enjoy:test:renderer
yarn enjoy:package
yarn enjoy:make
```

`package` 生成未封装的应用目录，`make` 生成当前操作系统对应的安装包。完整 E2E 测试包含语音识别和原生模块，耗时明显长于普通前端测试。

## 运行时配置

桌面端从进程环境读取以下可选变量：

| 变量 | 用途 | 默认值 |
| --- | --- | --- |
| `WEB_API_URL` | HTTP API 地址 | `https://enjoy.bot` |
| `WS_URL` | WebSocket 地址 | `wss://enjoy.bot` |
| `SETTINGS_PATH` | 设置文件目录 | Electron 用户数据目录 |
| `LIBRARY_PATH` | 媒体库和数据库目录 | 系统文档目录下的 `EnjoyLibrary` |
| `HTTP_PROXY` / `HTTPS_PROXY` | 下载词典时使用的代理 | 未设置 |

发布签名、GitHub Release 和对象存储所需的变量只用于维护者发布流程，详见 [开发环境说明](../DEVELOPMENT.md#发布与部署环境)。不要提交真实密钥。
