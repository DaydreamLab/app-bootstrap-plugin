---
name: app-bootstrap-bootstrap
description: Creates the opinionated AWS app stack in dev or prod via MCP bootstrap. Use when the user types /app-bootstrap-bootstrap or asks to first-time provision the current repo.
disable-model-invocation: true
---

# bootstrap

If this git repo is `app-bootstrap` (App 控制台 MCP 工具), do not call MCP. Use `scripts/platform-stack.sh apply`. Shared pools: `scripts/shared-dev-stack.sh apply`, `scripts/shared-prod-stack.sh apply`.

Otherwise call MCP tool `bootstrap` on server `app-bootstrap`. Repo must contain a Dockerfile.

Ask **`env`**: `dev` (default) or `prod`.

**Default** (`isolate=false`): join the shared Fargate+ALB pool for that env. **`hostname` is optional** (unique across **both** shared ALBs when set). Omit it and call `attach_domain` later. Missing pool → tell operator to apply the matching shared-*-stack.sh.

- `database=true`: on **shared-dev** → shared Postgres EC2; on **prod** (or any isolate box) → dedicated RDS. Optional `db_instance_class` (default `db.t4g.micro`).
- `storage=true`: private S3 + CloudFront (OAC); overwrites `AWS_BUCKET` / `AWS_DEFAULT_REGION` / `AWS_URL`. Seed with `aws s3 sync` manually. Re-bootstrap with `storage=false` destroys the bucket and CDN.
- `keep_warm=true`: only for shared-**dev**.
- `isolate=true` (alias `static_ip`): EC2+EIP+Caddy; does not join shared ALB.
- Do not invent shared_db (not implemented yet).

See [reference.md](../app-bootstrap/reference.md).
