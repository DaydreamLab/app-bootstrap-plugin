# {{PROJECT_NAME}} — CI/CD

本文件描述 **app-bootstrap** 部署、版本規則與 PR 合約檢查。

## 相關文件

- [`README.md`](../README.md) — 本機啟動入口
- [`docs/SPEC.md`](SPEC.md) — 產品規格
- [`docs/ROADMAP.md`](ROADMAP.md) — 開發進度

## 總覽

| 觸發 | 執行內容 |
| --- | --- |
| **Pull Request** | [`.github/workflows/ci.yml`](../.github/workflows/ci.yml)：`docker build` + `GET /health` |
| **Push 至 `main`** | [`.github/workflows/app-deploy.yml`](../.github/workflows/app-deploy.yml)：`docker build .` 推映像，更新 ECS（`dev`） |
| **Tag `vMAJOR.MINOR.PATCH`** | [`.github/workflows/app-deploy-prod.yml`](../.github/workflows/app-deploy-prod.yml) → `prod` |

## 版本規則

| 規則 | 說明 |
| --- | --- |
| Dev | 推 **`main`**（或 `master`）→ GitHub Environment **`dev`** |
| Prod | 僅 semver tag **`vMAJOR.MINOR.PATCH`**（如 `v1.2.3`）→ Environment **`prod`** |
| Tag filter | `app-deploy-prod.yml`：`v[0-9]+.[0-9]+.[0-9]+` |
| 非 semver tag | 不觸發 prod deploy |

映像合約在根目錄 [Dockerfile](../Dockerfile)。migrate／seed 若需要，放在映像 entrypoint，**不要**寫進 deploy workflow。

## 應用合約（app-bootstrap）

| 項目 | 要求 |
| --- | --- |
| Dockerfile | repo **根目錄**（`docker build .`） |
| Listen | `PORT`（平台注入 `8080`） |
| Health | `GET /health` → 200（**不碰 DB**） |
| Logs | stdout／stderr |
| Secrets | 勿把 `.env` 推進 git；`.env.example` 的 key 會在 Secrets Manager 建空值 |

dev／prod 的 DB、Mail 等由 **App 控制台**（app-bootstrap MCP）管理。部署 workflow 只推映像；機密注入由平台堆疊負責。GitHub Environment variables（`AWS_ROLE_ARN`、`ECR_REPOSITORY`、`ECS_*` 等）在 MCP `bootstrap` 後寫入；若遠端已有 workflow 檔，bootstrap **不會覆寫**。

## PR 測試（ci.yml）

1. Checkout
2. `docker build`
3. 起容器（`PORT=8080`）並 `curl /health`

依技術棧可再加單元測試步驟。

## Deploy workflows 同步

`app-deploy.yml`／`app-deploy-prod.yml` 語意應對齊平台 [`DaydreamLab/app-bootstrap`](https://github.com/DaydreamLab/app-bootstrap) 的 `templates/github/`。改平台模板後，再同步到 app-bootstrap-plugin 的 init 範本。
