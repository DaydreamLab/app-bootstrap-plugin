---
name: app-bootstrap-project-status
description: Shows bootstrap status, URLs, ECS/ALB health, and latest GitHub deploy via MCP project_status. Use when the user types /app-bootstrap-project-status or asks if the repo is up.
disable-model-invocation: true
---

# project_status

Call MCP tool `project_status` on server `app-bootstrap`.

- `repo`: `owner/name` from git origin
- `env`: default `dev`
- `region`: omit unless the user named one

Summarize bootstrapped, alb_dns, hostname, ECS/ALB, latest deploys. See [reference.md](../app-bootstrap/reference.md).
