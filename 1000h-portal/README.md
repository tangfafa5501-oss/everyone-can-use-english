# 1000h Portal

`1000h-portal` 是 1000h.org 根路径使用的 Nuxt 门户页。它生成静态文件，再由 Cloudflare Worker 或阿里云 OSS 提供服务。

## 本地开发

先在仓库根目录安装依赖：

```bash
yarn install --immutable
yarn portal:dev
```

默认开发地址为 `http://localhost:3000`。

## 构建与预览

```bash
yarn portal:generate
yarn portal:preview
```

生成结果位于 `.output/public`。页面修改主要位于 `pages/`、`components/`、`layouts/` 和 `styles/`。

正式部署配置见 `wrangler.toml` 和仓库的 `.github/workflows/deploy-1000h-portal*.yml`。本地开发不需要 Cloudflare 或阿里云凭据。
