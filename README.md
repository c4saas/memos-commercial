# Memos — Customer Deployment

This repo holds only the customer-facing `docker-compose.yml` + `.env.example`.
It pulls a pinned, pre-built image from GHCR — source lives in
[c4saas/melvin-memos](https://github.com/c4saas/melvin-memos).

## Install

```bash
git clone https://github.com/c4saas/memos-commercial.git /opt/memos
cd /opt/memos
cp .env.example .env          # fill in secrets + branding
docker login ghcr.io          # (first time only; pull token)
docker compose pull
docker compose up -d
```

Open the URL from `.env` → sign in with `MEMOS_DEFAULT_EMAIL` /
`MEMOS_DEMO_PASSWORD`. Change the password immediately.

## Update

The version is pinned on this line in `docker-compose.yml`:

```yaml
image: ghcr.io/c4saas/melvin-memos:0.1.0
```

When we ship a new release:

```bash
cd /opt/memos
git pull                      # the CI auto-bumps the version here
docker compose pull
docker compose up -d
```

(If you prefer to track latest, change the tag to `:latest` and just run
`docker compose pull && docker compose up -d` whenever you want the newest.)

## Whitelabel (reseller partners)

See the `BRAND_*` variables in `.env.example` — name, colors, logo URL,
support email, and `BRAND_HIDE_POWERED_BY=1` for license-tier partners.

## Support

Questions → set `BRAND_SUPPORT_EMAIL` and point your users there.
Internal issues → https://github.com/c4saas/melvin-memos/issues
