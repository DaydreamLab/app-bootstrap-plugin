---
name: app-bootstrap-logs-status
description: Shows ECS service/task and ALB target health via MCP logs_status. Use when the user types /app-bootstrap-logs-status or asks if the service is healthy.
disable-model-invocation: true
---

# logs_status

Call MCP tool `logs_status` on server `app-bootstrap` with `repo` from git origin, `env` default `dev`. See [reference.md](../app-bootstrap/reference.md).
