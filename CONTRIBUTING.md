# 参与贡献

感谢参与维护。开始前请阅读 [开发环境说明](./DEVELOPMENT.md) 和 [项目架构](./ARCHITECTURE.md)。

## 修改范围

- 内容修改：更新 `1000-hours/`、`book/` 或 `new-edition-drafts/`，并检查页面内链接和静态资源。
- 桌面端修改：更新 `enjoy/`，区分本地能力与远程 Enjoy API 依赖。
- 门户修改：更新 `1000h-portal/`。
- 域名路由修改：更新 `entry/`，并说明两个 Cloudflare Service Binding 的影响。

## 基本要求

1. 使用 Node.js 22+ 和仓库固定的 Yarn 4.6.0。
2. 使用 `yarn install --immutable` 安装依赖，不提交其他包管理器的锁文件。
3. 不提交账号、API Key、签名证书、云存储密钥或生产数据库。
4. 数据模型变化必须附带数据库迁移。
5. 新增远程 API 调用时说明失败、离线和未登录行为。
6. 尽量为缺陷修复增加对应测试。

## 提交前检查

根据修改范围运行：

```bash
yarn docs:build
yarn portal:generate
yarn enjoy:lint
yarn enjoy:test:main
yarn enjoy:test:renderer
```

桌面端测试和打包成本较高，不要求每次文档修改都运行；但桌面端逻辑或原生依赖修改至少应运行相关测试。

## 提交到 GitHub

本仓库约定：

- `origin` 指向个人维护仓库，用于日常推送；
- `upstream` 指向 `ZuodaoTech/everyone-can-use-english`，只用于同步原项目；
- 不要将安装包、构建目录、测试报告、数据库或本地媒体库提交到 Git。

建议从新分支提交维护工作：

```bash
git switch -c codex/maintenance-docs
git status
git add <需要提交的文件>
git diff --cached
git commit -m "docs: complete development documentation"
git push -u origin codex/maintenance-docs
```

推送后在 GitHub 上创建 Pull Request，再合并到个人仓库的 `main`。如果选择直接维护 `main`，也应在提交前仔细检查暂存文件，避免把本地安装包等大文件带入提交。

## 许可证

根仓库当前提供 GPL-3.0 许可证，但个别子项目的 `package.json` 仍有不同的许可证字段。复用、再发布或接受较大外部贡献前，维护者应先明确并统一各子目录的授权口径。
