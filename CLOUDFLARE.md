# Cloudflare — docs.almasix.com

This repository is the Starlight site for **docs.almasix.com**, served as
Worker static assets (same pattern as [almasix.com](https://almasix.com)).

## Wrangler

[`wrangler.jsonc`](./wrangler.jsonc) serves `./dist`. There is no Worker `main` script.

## CI vs deploy

GitHub Actions ([`.github/workflows/docs.yml`](./.github/workflows/docs.yml)) **builds only**.

**Deploy** is Cloudflare **Workers Builds** (no API tokens in GitHub):

| Setting | Value |
|---------|--------|
| Root directory | `/` |
| Build command | `npm ci && npm run build` |
| Deploy command | `npx wrangler deploy` |
| Project name | `almasix-docs` |
| Node | `24` (or `22`) |

## Cutover from GitHub Pages (on almasix)

1. Connect Workers Builds to **`almasix-dev/almasix-docs`** with the settings above.
2. Custom domains → add **`docs.almasix.com`**.
3. Wait until **Active** + cert issued.
4. Remove grey-cloud `docs` CNAME → `almasix-dev.github.io` if still present.
5. Disable GitHub Pages on `almasix-dev/almasix`.
6. Verify: `curl -I https://docs.almasix.com/`

## Local

```bash
npm ci
npm run build
npx wrangler deploy   # needs Cloudflare auth (local only)
```

## Package docs

Conduit, Inertia, and Permission keep their own `website/` docs hosts. See the hub
[`CLOUDFLARE.md`](https://github.com/almasix-dev/almasix-website/blob/main/CLOUDFLARE.md).
