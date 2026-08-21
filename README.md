# ai-first-student-workspace

Учебный workspace курса **AI-first QA**: takeaway Java/Spring + React + Selenide, плюс rules / skills / RAG.

Домашка одним запросом: [HOMEWORK.md](HOMEWORK.md) — сначала **Fork**, потом clone своего форка.

```bash
# Fork на GitHub, затем:
git clone https://github.com/<your-login>/ai-first-student-workspace.git
cd ai-first-student-workspace
docker compose up -d --build
```

| Role | Folder |
|------|--------|
| Backend | `backend-java-spring/` |
| Frontend | `frontend-typescript-react/` (`vendor/` — запечённый design-system runtime) |
| Tests | `tests-java-gradle-junit5-allure3-selenide/` |

```bash
curl -sf http://localhost:8800/api/health
# UI same-origin (SPA + /api): http://localhost:9821/
# UI container only:          http://localhost:9811/
```

| Method | Path | Что |
|--------|------|-----|
| GET | `/api/health` | liveness |
| GET | `/api/openapi.yaml` | контракт (байты `_contract/openapi.yaml`) |
| GET | `/api/docs` | Swagger UI на ту yaml |

```bash
curl -sf http://localhost:8800/api/openapi.yaml >/dev/null
# Swagger UI: http://localhost:8800/api/docs
# same-origin: http://localhost:9821/api/docs
```

Tests (gateway already up):

```bash
cd tests-java-gradle-junit5-allure3-selenide
./gradlew test -Denv=ci -DincludeTags=e2e -DexcludeTags=screenshot,mock
```

CI: `.github/workflows/ci.yml` (same orchestrator as the clone; stack knobs in `env:`).  
Prod stand: [https://ai-first.autotests.ai/](https://ai-first.autotests.ai/) (`-Denv=prod`).  
Stage: [https://stage.ai-first.autotests.ai/](https://stage.ai-first.autotests.ai/) (`-Denv=stage`).

Maintainers: refresh from the hub ethalon in the zero-design-system monorepo:

```bash
./generators/render/render.sh --preset singlestack
```
