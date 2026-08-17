---
name: app-bootstrap
description: App 控制台 MCP 工具：為應用 GitHub repo 做 AWS 堆疊（status、bootstrap、env、domain、logs、cost、destroy）。當使用者要佈署或拆除當前應用 repo 時使用。不要對 app-bootstrap 本專案呼叫 MCP。
---

# App 控制台 MCP 工具

Use MCP server **app-bootstrap** for **other application repos**. Call tools; do not invent AWS CLI. This git repo is the App 控制台 MCP 工具 itself.

If git origin is `*/app-bootstrap` (the App 控制台 MCP 工具 platform repo), stop: MCP refuses it. Point the operator at that private repo's `scripts/platform-stack.sh` and related docs.

For application repos, see [README.md](../../README.md) and [reference.md](reference.md).

1. Resolve `repo` as `owner/name` from git origin.
2. Prefer `project_status` before mutate.
3. Tool names, args, and confirms: [reference.md](reference.md)

Before `bootstrap`, ask **env** (`dev`|`prod`). **hostname is optional** on shared ALB (omit and call `attach_domain` later; unique across both ALBs when set). Unclear compute → shared Fargate (`static_ip=false`). `static_ip=true` only for fixed IP. `keep_warm` only shared-dev overnight.

If MCP is missing, tell the user to install the **app-bootstrap** plugin from `https://github.com/DaydreamLab/app-bootstrap-plugin` (MCP URL is built in: `https://app-bootstrap.daydream-lab.com/mcp`).
