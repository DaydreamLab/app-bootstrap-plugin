---
name: app-bootstrap-wake
description: Wakes a shared-dev ECS service and shared Postgres/MariaDB/Redis until 22:00 Asia/Taipei (or keep_warm). Use when the user types /app-bootstrap-wake or the app is 502 because it is scheduled off.
disable-model-invocation: true
---

# wake

Call MCP tool `wake` on server `app-bootstrap` with `repo` from git origin. Optional `keep_warm=true` to skip nightly stop. See [reference.md](../app-bootstrap/reference.md).
