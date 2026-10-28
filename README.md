# VPS Administration

This repository contains safe, human-maintained documentation and administration scripts for `vps.lumidotstudios.com`.

## Scope

- Keep operational decisions and maintenance history in `VPS_ADMIN_LOG.md`.
- Keep application source code in separate GitHub repositories.
- Never commit passwords, tokens, private keys, `.env` files, certificates, database dumps, or other sensitive data.

## Synchronization

From the VPS:

```bash
cd /home/ubuntu/vps-admin
git pull --ff-only
git add .
git commit -m "Describe the change"
git push
```

Changes made on GitHub can be brought to the VPS with `git pull --ff-only`. Changes made on the VPS should be committed and pushed after review.

## Change records

Add a dated section to `VPS_ADMIN_LOG.md` for meaningful inspections, decisions, installations, deployments, security changes, incidents, and rollbacks.
