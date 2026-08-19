---
id: ci-github-actions
domain: config
adr: 002
tags: [ci, github-actions]
related: [ci-gradle-args, cfg-stands, test-pyramid]
---
# GitHub Actions takeaway

**id:** `ci-github-actions`

Глаголы — skills `qa-review-ci` · `qa-create-ci` · `qa-fix-ci` · `qa-run-ci` · `qa-stop-ci`. Этот чанк — факты YAML. Не путать с `qa-run-stand` (Gradle на app).

`-Denv=` в jobs — как в `ci-gradle-args` (живой takeaway часто `multistack_ci`).

## Jobs (пирамида)

```
unit-tests → integration-tests
параллельно: tests-harness · component-tests · api-tests · e2e-tests · ui-mock-tests
deploy (если vars.DEPLOY_HOST) → api-tests-prod → e2e-tests-prod
deploy-stage (если vars.STAGE_HOST) → api-tests-stage → e2e-tests-stage
publish-allure-report (всегда собирает артефакты; Pages — soft)
```

PR без DNS всё равно гоняет unit → e2e на **compose раннера** (`-Denv=ci`). Deploy skip, если host-переменные пустые.

## Vars / secrets (когда поднимаете свой стенд)

| Ключ | Роль |
|------|------|
| `DEPLOY_HOST` / `DEPLOY_USER` / `DEPLOY_APP_DIR` | SSH prod compose |
| `DEPLOY_COMPOSE_PROJECT` | `--project-name` если на хосте уже есть другой compose (матрица) |
| `DEPLOY_COMPOSE_ENV_FILE` | remap портов (`BACKEND_JAVA_PORT`, `CI_GATEWAY_PORT`) |
| `STAGE_HOST` / `STAGE_USER` / `STAGE_APP_DIR` | SSH stage |
| `STAGE_COMPOSE_PROJECT` / `STAGE_COMPOSE_ENV_FILE` | stage twin |
| `secrets.DEPLOY_SSH_KEY` | ключ |
| `secrets.SELENOID_REMOTE_URL` | хаб с кредами — prod/stage e2e |

В этом файле **нет** TestOps / Telegram / Sonar — это школьный контур позже, не копировать из матрицы.

## CLI (run / stop)

```bash
gh workflow list
gh run list --limit 5
gh workflow run CI
gh run rerun <run-id> --failed
gh run cancel <run-id>
```

## Don't

- Копировать matrix `ci.yml` поверх takeaway.
- Хардкодить `ALLURE_TOKEN` / пароль хаба в YAML.
- Ждать зелёный `deploy`, если DNS ещё не поднят — смотрите jobs compose.
