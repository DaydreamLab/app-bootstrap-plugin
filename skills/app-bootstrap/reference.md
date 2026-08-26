# App 控制台 MCP 工具

Server name: `app-bootstrap`。`repo` 從**本機** `git remote` → `owner/name`（遠端不即時查 GitHub collaborator）。預設 `env=dev`。空 `region` 用平台預設（`ap-east-2`）。

若 origin 是 `DaydreamLab/app-bootstrap`（**平台本體／App 控制台 MCP 工具**），**不要呼叫 MCP**。那是 private 平台 repo，用它的 script 發佈，不用本 plugin。

使用者說明見 [README.md](../../README.md)。

Slash（非 MCP）：空專案先 `/app-bootstrap-init`（本機寫文件／Dockerfile／workflows），再 `bootstrap`。

| Tool | When | Args |
|---|---|---|
| `project_status` | Status, URLs, ECS, latest deploy | `repo`, `env?`, `region?` |
| `bootstrap` | First-time **dev or prod** for an **app** repo. Shared-dev = ECS on t4g.medium+Caddy+EIP（`hostname` optional, unique across envs when set; otherwise `attach_domain` later with A record to shared EIP）。`isolate=true`（alias `static_ip`）= dedicated EC2+EIP+Caddy with Redis plus MySQL or Postgres on that host（`isolate_db=mysql|postgres`，default mysql）。`database`：shared-dev 共用 Postgres（預設）或 MariaDB（`db_engine=mysql`）；**isolate-dev 同機 DB＋Redis**；**prod 為 RDS**。`storage=true`：私有 S3＋CloudFront。`keep_warm` 僅 shared-dev。 | `repo`, `env?`, `hostname?`, `region?`, `database?`, `storage?`, `isolate?`, `static_ip?`, `isolate_db?`, `db_engine?`, `instance_type?`, `keep_warm?`, `db_instance_class?` |
| `wake` | Start shared-**dev** compute + Postgres + MariaDB + Redis (or isolate EC2) until next 22:00 Taipei | `repo`, `region?`, `keep_warm?` |
| `attach_domain` | Set hostname after DNS matches (shared-dev: A to EIP + Caddy; prod: ALB host-header) | `repo`, `hostname`, `region?`, `env?` |
| `set_env` | One Secrets Manager key; confirm to roll ECS | `repo`, `key`, `value`, `env?`, `region?`, `confirm_token?` |
| `logs_status` / `logs_deploys` / `logs_errors` | Health / Actions / CW | … |
| `cost_estimate` | Budget alerts | `repo`, `region?` |
| `destroy` | Tear down this app **env** (not shared pools) | `repo`, `env?`, … (prod: `DESTROY owner/name`) |

Auth: Cursor OAuth to the MCP URL. Issued tokens are accepted from local identity files（no live GitHub `/user` per request）. No static Bearer in mcp.json.

Deploy（應用）：`main` → Environment `dev`；tag `vMAJOR.MINOR.PATCH` → Environment `prod`。  
本專案自己：`main` → apply `app-bootstrap-prod` 再 ECR／ECS。
