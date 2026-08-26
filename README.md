# AriaNg Workers

这是一个用于 Cloudflare Workers Static Assets 的 AriaNg 前端部署仓库。

本仓库只托管 Web 前端，不包含 aria2 下载服务。部署完成后，需要在其他服务器、NAS 或 Docker 容器中运行 aria2，并在页面设置中填写 aria2 的 RPC 地址。

## Cloudflare Workers 部署

本仓库已经包含 `wrangler.toml`，并配置了 `dist/` 作为静态资源目录。

通过 Cloudflare 的 Git 集成部署时使用以下配置：

```text
构建命令：npm run build
部署命令：npx wrangler deploy
根目录：/
```

也可以在本地部署：

```bash
npm ci
npm run build
npx wrangler login
npx wrangler deploy
```

构建结果会生成在 `dist/`，该目录已被 Git 忽略，不需要提交到仓库。

## aria2 RPC 配置

AriaNg 运行在浏览器中，因此浏览器必须能够访问 aria2 RPC 服务。例如：

```text
HTTP： http://aria2.example.com/jsonrpc
HTTPS： https://aria2.example.com/jsonrpc
WebSocket： ws://aria2.example.com/jsonrpc
安全 WebSocket： wss://aria2.example.com/jsonrpc
```

如果前端页面使用 HTTPS，RPC 通常也必须使用 HTTPS 或 WSS，否则浏览器会阻止混合内容连接。

建议为 aria2 配置 `rpc-secret`，并通过 Nginx、Cloudflare Tunnel 或其他安全方式暴露 RPC，避免直接公开 aria2 端口。

## 上游同步

本仓库基于 [mayswind/AriaNg](https://github.com/mayswind/AriaNg)。GitHub Actions 会定期检查上游 `master` 分支，只有检测到新提交时才会执行同步。

也可以在 GitHub 的 **Actions → Sync upstream AriaNg** 页面手动运行。若上游更新与本仓库的 Workers 配置产生冲突，工作流会停止，等待手动解决。

## 目录说明

| 路径 | 用途 |
| --- | --- |
| `src/` | AriaNg 前端源代码 |
| `dist/` | 构建输出，不提交到 Git |
| `wrangler.toml` | Cloudflare Workers 配置 |
| `.github/workflows/` | 上游同步工作流 |

## 许可与归属

AriaNg 原项目由 [mayswind](https://github.com/mayswind) 开发，原项目使用 MIT License。本仓库的修改部分同样遵循 MIT License，具体以 [LICENSE](LICENSE) 文件为准。
