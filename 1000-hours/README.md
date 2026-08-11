# 1000 Hours with Attention Paid

This is the repo of [1000h.org](https://1000h.org).

By paying your attention into 1000 hours, you can master anything you need.

## 本地开发

请从仓库根目录运行：

```bash
yarn install --immutable
yarn docs:dev
```

构建和预览：

```bash
yarn docs:build
yarn docs:preview
```

站点使用 VitePress。正文是本目录下的 Markdown 文件，导航和主题配置位于 `.vitepress/`。提交内容修改前至少运行一次 `yarn docs:build`，以发现无效页面、Markdown 插件或静态资源问题。

Cloudflare 部署配置位于 `wrangler.toml`，GitHub Actions 使用仓库密钥完成正式部署；普通内容贡献不需要 Cloudflare 账号。
