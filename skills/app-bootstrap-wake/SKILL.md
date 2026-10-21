---
name: app-bootstrap-wake
description: Wakes shared-dev compute or isolate EC2. For isolate, check hold_history first and always pass until; active hold rejects omitted/earlier until (equal OK)—shorten via clear_hold then wake. Use when the user types /app-bootstrap-wake or the app is 502 because it is scheduled off.
disable-model-invocation: true
---

# wake

Call MCP tool `wake` on server `app-bootstrap` with `repo` from git origin.

## Shared-dev

- Optional `keep_warm=true` to skip nightly stop.
- Do **not** pass `until` (isolate-only).

## Isolate

1. Call `hold_history` first to see current hold state / deadline.
2. Always pass `until` (Asia/Taipei; max 14 days; date-only means that day 22:00).
3. If a hold is still active (not expired):
   - Omitting `until`, or `until` **earlier** than the current deadline → rejected (error includes the current Asia/Taipei ISO 8601 deadline); no hold write, no start.
   - `until` **equal to** the current deadline → allowed (reaffirm + start).
   - `until` **later** → allowed (extend).
4. To **shorten** a deadline: `clear_hold` first, then `wake(until=…)`.
5. `keep_warm` does not apply to isolate and does not bypass the checks above.

See [reference.md](../app-bootstrap/reference.md).
