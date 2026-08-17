# App 控制台 MCP 工具 — Cursor plugin

公開安裝用 repo。連到已佈署的 App 控制台 MCP（`https://app-bootstrap.daydream-lab.com/mcp`），附 skills 與 rules。

平台本體（private）在 [`DaydreamLab/app-bootstrap`](https://github.com/DaydreamLab/app-bootstrap)。不要對那個 repo 呼叫 MCP。

## 安裝

1. Cursor 側邊欄開 **Customize**
2. **Add Marketplace** → **Import from Github**
3. 貼：`https://github.com/DaydreamLab/app-bootstrap-plugin`
4. 安裝 plugin **app-bootstrap**
5. `MCP_URL` 用預設 `https://app-bootstrap.daydream-lab.com/mcp`（本機 Compose 可改 `http://127.0.0.1:8080/mcp`）

第一次連線走 GitHub OAuth。不要在 `mcp.json` 再加同一條 URL，也不要把 token 寫進 plugin。

## 使用

在**應用 repo**（有 Dockerfile）開 chat：

| 項目 | 說明 |
|---|---|
| `repo` | git origin 的 `owner/name` |
| `env` | `dev`（預設）或 `prod` |
| 授權 | 對該 repo 要有 write / maintain / admin |

常用：`project_status`、`bootstrap`、`wake`、`set_env` / `list_env`、`attach_domain`、`logs_*`、`destroy`。

- 共用 ALB：`bootstrap` 必填 `hostname`，跨 dev／prod 不可撞名
- 推 `main` → dev；tag `vMAJOR.MINOR.PATCH` → prod
- shared-dev 平日 09:00 開、每天 22:00 關（Asia/Taipei）；502 時先 `wake`

## 開發

plugin 原始檔在平台 repo 的 `cursor-plugin/`。改完再同步到本 repo。
