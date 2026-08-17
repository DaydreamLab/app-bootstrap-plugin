---
name: app-bootstrap-set-env
description: Sets one cloud env key in Secrets Manager via MCP set_env and rolls ECS after confirm. Use when the user types /app-bootstrap-set-env or asks to set a runtime secret.
disable-model-invocation: true
---

# set_env

Call MCP tool `set_env` on server `app-bootstrap`. Never echo `value` back in chat.

- `repo`, `key`, `value` (from the user)
- `env` default `dev`
- Follow `confirm_token` if the tool asks before rolling

See [reference.md](../app-bootstrap/reference.md).
