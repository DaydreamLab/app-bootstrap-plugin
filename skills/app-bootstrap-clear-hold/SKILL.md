---
name: app-bootstrap-clear-hold
description: Clears an isolate-dev wake hold via MCP clear_hold (SSM only; does not stop EC2). Two-step confirm_token. Use before wake(until=…) when shortening a hold, or when the user types /app-bootstrap-clear-hold.
disable-model-invocation: true
---

# clear_hold

Call MCP tool `clear_hold` on server `app-bootstrap` for **isolate** dev only.

- Args: `repo` (from git origin), optional `region`, optional `confirm_token`
- Clears the SSM wake hold only — **does not** stop the EC2; there is **no** `stop` parameter
- Two-step confirm:
  1. First call (no token) → returns `hold_until` and `confirm_token` (no write)
  2. Second call with `confirm_token` → clears the hold; audit event `clear` visible in `hold_history`
- No active hold / expired / unreadable → `ok=true`, `cleared=false`, plus `hold_state`; **no** token issued and **no** write
- After clear, the next 22:00 Asia/Taipei stop may shut the box down; call `wake(until=…)` if it should stay up

See [reference.md](../app-bootstrap/reference.md).
