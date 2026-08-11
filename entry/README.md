# 1000h Entry Worker

该 Cloudflare Worker 是 `1000h.org` 的流量入口：

- `/`、`/portal-assets/*`、`/portal-static/*` 转发到 `1000h-portal`；
- 其他路径转发到 `1000h-vtp`（VitePress 内容站）。

两个 Service Binding 在 `wrangler.toml` 中分别命名为 `portal` 和 `vtp`。

## 本地检查

`entry` 没有运行时 npm 依赖，也没有加入根 Yarn workspace。安装 Wrangler 后可在本目录执行：

```bash
npx wrangler dev
```

本地运行仍需要可访问的 Cloudflare Worker 服务绑定。若只是修改路由逻辑，建议为 `handleRequest` 增加单元测试并使用模拟的 `env.portal.fetch` 与 `env.vtp.fetch`，不要直接依赖生产服务。

正式部署需要 GitHub Actions 中配置的 `CF_BASEONE_API_TOKEN` 和 `CF_BASEONE_ACCOUNT_ID`。
