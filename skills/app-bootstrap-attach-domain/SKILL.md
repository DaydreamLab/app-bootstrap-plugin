---
name: app-bootstrap-attach-domain
description: After DNS is in place, attach HTTPS via MCP attach_domain (ACM on ALB, or Caddy/Let’s Encrypt on EC2+EIP). Use when the user types /app-bootstrap-attach-domain or has already pointed DNS.
disable-model-invocation: true
---

# attach_domain

Call MCP tool `attach_domain` on server `app-bootstrap`. Do not change registrar DNS.

- `repo`: `owner/name`
- `hostname`: the name the user provided

If `project_status` shows an EIP (`static_ip`), the human must create an **A record** to that EIP first. The tool fails immediately if DNS does not resolve to the EIP; do not wait/poll — tell them to retry later. TLS is Caddy + Let’s Encrypt (HTTP-01), not ACM.

If there is an ALB, they must CNAME to `alb_dns` first; then ACM.

See [reference.md](../app-bootstrap/reference.md).
