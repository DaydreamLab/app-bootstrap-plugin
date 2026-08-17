---
name: app-bootstrap-destroy
description: Destroys this repo's AWS stack via MCP destroy. Dev needs two confirms; prod needs phrase DESTROY owner/name. Use when the user types /app-bootstrap-destroy or explicitly asks to tear down.
disable-model-invocation: true
---

# destroy

Call MCP tool `destroy` on server `app-bootstrap` only if the user clearly asked to destroy.

- `repo` from git origin; `env` default `dev`
- Follow `confirm_token`. Prod also `confirm_phrase`: `DESTROY owner/name`
- Current repo only. Does **not** destroy shared VPC/ALB/Postgres.

See [reference.md](../app-bootstrap/reference.md).
