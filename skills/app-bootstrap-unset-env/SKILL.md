---
name: app-bootstrap-unset-env
description: Removes one cloud env key via MCP unset_env and rolls ECS after confirm. Use when the user types /app-bootstrap-unset-env or asks to delete a secret key.
disable-model-invocation: true
---

# unset_env

Call MCP tool `unset_env` on server `app-bootstrap`.

- `repo`, `key`
- `env` default `dev`
- Follow `confirm_token` before rolling

See [reference.md](../app-bootstrap/reference.md).
