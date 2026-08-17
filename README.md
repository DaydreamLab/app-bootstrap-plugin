# App 控制台 MCP 工具 — Cursor plugin

公開安裝用 repo。連到已佈署的 App 控制台 MCP（`https://app-bootstrap.daydream-lab.com/mcp`），附 skills 與 rules。

平台本體（private）[`DaydreamLab/app-bootstrap`](https://github.com/DaydreamLab/app-bootstrap) 以 **git submodule** 掛在 `cursor-plugin/`。本 repo 是 plugin 原始檔。

## 安裝

1. Cursor 側邊欄開 **Customize**
2. **Add Marketplace** → **Import from Github**
3. 貼：`https://github.com/DaydreamLab/app-bootstrap-plugin`
4. 安裝 plugin **app-bootstrap**

MCP 已寫死 `https://app-bootstrap.daydream-lab.com/mcp`，不用再填 URL。第一次連線走 GitHub OAuth。不要在 Cursor 使用者 `mcp.json` 再加同一條，也不要把 token 寫進 plugin。

本機 Compose 除錯才用 `http://127.0.0.1:8080/mcp`（另加使用者 MCP，不要改這個公開 plugin）。

## 使用

在**應用 repo**（有 Dockerfile）開 chat：

| 項目 | 說明 |
|---|---|
| `repo` | git origin 的 `owner/name` |
| `env` | `dev`（預設）或 `prod` |
| 授權 | 對該 repo 要有 write / maintain / admin |

常用：`project_status`、`bootstrap`、`wake`、`set_env` / `list_env`、`attach_domain`、`logs_*`、`destroy`。

- 共用 ALB：`bootstrap` 的 `hostname` 可省略，之後 `attach_domain`；有填則跨 dev／prod 不可撞名
- 推 `main` → dev；tag `vMAJOR.MINOR.PATCH` → prod
- shared-dev 平日 09:00 開、每天 22:00 關（Asia/Taipei）；502 時先 `wake`

## 開發（與平台 repo 同步）

在平台 repo 裡改 `cursor-plugin/`（本 repo 的 checkout），提交並推到 **本 repo `main`**，再回平台 repo 更新 submodule 指標：

```bash
cd cursor-plugin
git checkout main
# 改檔後
git add -A && git commit -m "Explain the change." && git push origin main
cd ..
git add cursor-plugin
git commit -m "Point cursor-plugin submodule at the latest plugin."
```
