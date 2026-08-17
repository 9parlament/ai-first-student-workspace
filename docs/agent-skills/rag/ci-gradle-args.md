---
id: ci-gradle-args
domain: config
adr: 002
tags: [gradle, tags, env]
---
# Gradle-команды takeaway

**id:** `ci-gradle-args`

Модуль: `tests-java-gradle-junit5-allure3-selenide/`. Один task `test`. Срез = `-DincludeTags` + `-Denv`.

## Стенды

| `-Denv=` | Что это | App |
|----------|---------|-----|
| `multistack_ci` | pipeline ≈ локальный compose / CI | UI [http://localhost:9821/](http://localhost:9821/) · API [http://localhost:8800/](http://localhost:8800/) |
| `multistack_stage` | stage takeaway | [https://stage.ai-first.autotests.ai/](https://stage.ai-first.autotests.ai/) + `remoteUrl` хаба |
| `multistack_prod` | prod takeaway (не матрица `/stack/…`) | [https://ai-first.autotests.ai/](https://ai-first.autotests.ai/) + `remoteUrl` хаба |

Перед `multistack_ci`: `docker compose up -d --build` в корне takeaway. Health: `curl -sf http://localhost:8800/api/health`.

## Команды

```bash
cd tests-java-gradle-junit5-allure3-selenide

# e2e (учебный «smoke» в этом стеке — тег e2e, не @Tag("smoke"))
./gradlew test -Denv=multistack_ci -DincludeTags=e2e -DexcludeTags=screenshot,mock

# один класс / метод (-Dtest= → filter; класс или Class#method; повтор не UP-TO-DATE)
./gradlew test -Denv=multistack_ci -DincludeTags=e2e -Dtest=HomeTests
./gradlew test -Denv=multistack_ci -DincludeTags=e2e \
  -Dtest=LoginTests#shouldShowErrorWhenPasswordIsWrong

# api без браузера
./gradlew test -Denv=multistack_ci -DincludeTags=api

# manual (шаги в коде, не браузер)
./gradlew test -Denv=multistack_ci -DincludeTags=manual

# «прод»-стенд (нужен remoteUrl с кредами — в git их нет)
./gradlew test -Denv=multistack_prod -DincludeTags=e2e -DexcludeTags=screenshot,mock
```

Allure results: `build/allure-results`. Отчёт: `npx allure serve build/allure-results` (после `npm ci` в модуле тестов).

## Don't

- `./gradlew test` без `-DincludeTags` на задаче «smoke / e2e».
- Выдумывать task `testE2e` — в takeaway его нет.
- Хардкодить URL в тесте — только `-Denv` / properties.
