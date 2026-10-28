# VPS Administration Log

This file records important inspections, decisions, changes, and follow-up items for this VPS. Add a dated entry for each meaningful administration action.

## Server identity

- Hostname: `vps.lumidotstudios.com`
- OS: Ubuntu 26.04.1 LTS
- Architecture: x86-64
- Resources at initial inspection: 2 CPUs, 3.8 GiB RAM, 96 GiB root disk

## 2026-10-28 — Initial server inventory

### Observed

- Uptime was approximately 4 days, 18 hours.
- Root filesystem was 2% used; no swap was configured.
- Only externally listening service was OpenSSH on TCP port 22.
- Active baseline services included SSH, chrony, systemd-resolved, cloud-init, and unattended upgrades.
- No containers were present.
- No application servers or common runtimes were detected beyond Python 3.14:
  - No Nginx, Apache, Caddy, PHP, Node.js, Java, Go, Docker, Podman, MySQL, PostgreSQL, Redis, or MongoDB.
- No Snap applications were installed.
- No deployed application directories were found under `/var/www`, `/opt`, or `/srv`.
- `/home/ubuntu/vps-admin` contained no tracked project files and was not a Git repository.

### Security observations

- SSH permits root login (`PermitRootLogin yes`).
- SSH permits password authentication (`PasswordAuthentication yes`).
- SSH X11 forwarding is enabled.
- No active UFW firewall configuration was reported.

### Decisions / follow-up

- Treat the VPS as a clean baseline host rather than an existing application server.
- Before deploying an application, harden SSH, configure a firewall, and decide whether swap is needed.
- Record all future infrastructure changes, package installations, deployments, incidents, and rollback decisions in this file.

## Change log

| Date | Change | Reason / outcome |
|---|---|---|
| 2026-10-28 | Created this administration log | Establish a durable record for VPS decisions and operational activity |
| 2026-10-28 | Installed Docker Engine and Compose | Container runtime for future applications; Docker socket remains restricted from `ubuntu` |
| 2026-10-28 | Deployed n8n at `https://workflows.lumidotstudios.com` | n8n + PostgreSQL + Caddy with persistent volumes and automatic HTTPS |
| 2026-10-28 | Enabled persistent 4 GiB swap | Added memory headroom; configured swappiness to 10 |
| 2026-10-28 | Deployed Paperclip at `https://team.lumidotstudios.com` | Official Docker image, authenticated mode, persistent data, and Caddy HTTPS; Paperclip is private behind the Docker network |

