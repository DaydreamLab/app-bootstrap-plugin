# {{PROJECT_NAME}}

以 **Docker** 運行的應用（請改寫為實際技術棧）。雲端走 **app-bootstrap**（`PORT=8080`、`GET /health`）。

## Requirements

- [Docker](https://docs.docker.com/get-docker/)

## Installation

```bash
cp .env.example .env
docker build -t {{PROJECT_NAME}} .
docker run --rm -p 8080:8080 --env-file .env {{PROJECT_NAME}}
```

## Directory structure

```
docs/                   專案文件（見下方 Documentation）。
.github/workflows/      CI 與 app-bootstrap deploy。
Dockerfile              平台映像合約（聽 PORT、GET /health）。
.env.example            環境變數樣板（勿提交 .env）。
```

依技術棧補上 `src/`、測試目錄等；細節見 [Documentation](#documentation)。

## 本機開發

```bash
docker build -t {{PROJECT_NAME}} .
docker run --rm -p 8080:8080 -e PORT=8080 {{PROJECT_NAME}}
curl -s http://127.0.0.1:8080/health
```

## Testing

```bash
# 依技術棧替換；CI 預設以 docker build + /health 驗證合約
docker build -t {{PROJECT_NAME}}:test .
```

## CI/CD

- **Pull Request** → `ci.yml`：`docker build` + `/health`
- **Push `main`** → `app-deploy.yml`：推映像、更新 ECS（dev）
- **Tag `vMAJOR.MINOR.PATCH`** → `app-deploy-prod.yml`：prod 部署

版本規則、workflow、app-bootstrap 合約見 [`docs/CI_CD.md`](docs/CI_CD.md)。Deploy 用的 GitHub Environment variables 由 MCP `bootstrap` 寫入。

## Documentation

各文件開頭均有 **相關文件** 交叉連結；README 為入口。

- [`docs/CI_CD.md`](docs/CI_CD.md) — CI／部署／版本規則／合約
- [`docs/SPEC.md`](docs/SPEC.md) — 產品規格（請填）
- [`docs/ROADMAP.md`](docs/ROADMAP.md) — 開發進度（請填）
