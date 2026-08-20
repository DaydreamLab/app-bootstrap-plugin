---
name: app-bootstrap-init
description: Scaffold app-bootstrap docs, minimal Dockerfile, and CI/deploy workflows into an empty application repo. Use when the user types /app-bootstrap-init.
disable-model-invocation: true
---

# init

If this git repo is `app-bootstrap` (platform), stop. Do not scaffold here.

Otherwise copy files from this skill's `templates/` into the workspace root. Replace `{{PROJECT_NAME}}` with the repo short name. **Do not overwrite** existing paths.

Writes: `README.md`, `docs/*`, `Dockerfile`, `.env.example`, `.github/workflows/ci.yml`, `app-deploy.yml`, `app-deploy-prod.yml`.

Deploy YAMLs mirror platform `templates/github/` (keep in sync there first). GitHub Environment vars still need MCP `bootstrap` after push.

Next: implement real runtime, then MCP `bootstrap`.
