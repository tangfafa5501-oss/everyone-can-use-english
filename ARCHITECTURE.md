# 项目架构

## 仓库组成

```text
everyone-can-use-english
├─ enjoy/          Electron 桌面应用
├─ 1000-hours/     VitePress 内容站（1000h-vtp）
├─ 1000h-portal/   Nuxt 静态门户（1000h-portal）
├─ entry/          1000h.org 的 Cloudflare Worker 路由入口
├─ book/           《人人都能用英语》原始书稿
└─ new-edition-drafts/ 新版内容草稿及配套媒体
```

根目录通过 Yarn workspaces 管理 `enjoy`、`1000-hours` 和 `1000h-portal`。`entry` 是独立的 Cloudflare Worker，不属于 workspace。

## 请求和部署关系

```text
浏览器 -> 1000h-entry
             ├─ 根路径和 portal 静态资源 -> 1000h-portal
             └─ 其他内容路径             -> 1000h-vtp

Enjoy 桌面端 -> enjoy.bot HTTP API / WebSocket
             -> 本地 SQLite、媒体库、FFmpeg、语音识别组件
             -> 第三方或用户配置的 AI、TTS、STT 服务
```

## Enjoy 桌面端

- `src/main.ts`：Electron 主进程入口。
- `src/preload.ts`：受控地向渲染进程暴露 IPC 能力。
- `src/main/`：窗口、设置、本地数据库、媒体和系统服务。
- `src/main/db/models/`：Sequelize 数据模型。
- `src/main/db/migrations/`：SQLite 迁移。
- `src/main/db/handlers/`：通过 IPC 使用的数据操作。
- `src/renderer/`：React 页面、组件、上下文和状态逻辑。
- `src/api/`：远程 Enjoy API 客户端。
- `e2e/`：打包应用上的 Playwright 测试。
- `lib/`：按平台提供的 Whisper、YouTube 下载等二进制组件。

桌面端同时包含“完全本地”和“依赖云端”两类能力。媒体播放、SQLite 数据、部分离线转写等可以在本仓库内开发；登录、同步、社区、余额和 Enjoy 托管 AI 依赖未开源的远程后端。

## 原仓库分支说明

官方原仓库的 `next` 分支包含未合并的配置管理、数据库 Handler 重构和目录分层调整。它与 `main` 已经分叉，不应直接整体合并。若继续桌面端架构升级，应按功能拆分迁移并为每批迁移补测试。
