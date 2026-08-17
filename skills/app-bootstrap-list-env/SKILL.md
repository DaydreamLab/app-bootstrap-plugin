---
name: app-bootstrap-list-env
description: Lists cloud env key names (not values) via MCP list_env. Use when the user types /app-bootstrap-list-env or asks which secrets exist.
disable-model-invocation: true
---

# list_env

Call MCP tool `list_env` on server `app-bootstrap`. Report keys only.

- `repo`: `owner/name` from git origin
- `env` default `dev`

See [reference.md](../app-bootstrap/reference.md).
