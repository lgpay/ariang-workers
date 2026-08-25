# Cloudflare Workers deployment

This repository includes a `wrangler.toml` for deploying AriaNg as a Cloudflare Workers Static Assets application.

## Cloudflare Git integration

Use these settings when connecting the repository to Cloudflare Workers:

- Build command: `npm run build`
- Deploy command: `npx wrangler deploy`
- Root directory: `/`

The build output is generated in `dist/`, which is configured as the Workers static asset directory.

AriaNg is only the web frontend. An aria2 instance with a reachable HTTPS JSON-RPC endpoint or WSS endpoint is still required.
