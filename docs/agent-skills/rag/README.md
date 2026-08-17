# RAG для курса AI-first QA (диета)

Retrieval-единицы **для учебного репо студента**. Не копия всего `docs/rag/` monorepo (~96 чанков) — Ollama 7b это не удержит.

**SSOT паттернов в monorepo:** `docs/rag/` (преподаватель).  
**Студенту:** эти файлы кладём в `docs/agent-skills/rag/` учебного проекта. Skill пишет: «прочитай `docs/agent-skills/rag/po-fluent.md`».

Якоря кода — **takeaway** `java_spring-typescript_react-java_selenide` (клон [autotests-ai/java_spring-typescript_react-java_selenide](https://github.com/autotests-ai/java_spring-typescript_react-java_selenide)). Ethalon в monorepo — тот же код в другой раскладке папок.

## Как читать

Один чанк = один `id`. Агент читает **2–4 файла**, не всю папку.

| id | Файл | Когда |
|----|------|--------|
| `test-pyramid` | [test-pyramid.md](test-pyramid.md) | какой ярус, не путать slice |
| `test-layers` | [test-layers.md](test-layers.md) | `@Layer` → Gradle `-DincludeTags` |
| `e2e-layers` | [e2e-layers.md](e2e-layers.md) | config / TestBase / pages / tests |
| `po-fluent` | [po-fluent.md](po-fluent.md) | цепочка PO, `return this` |
| `po-locators` | [po-locators.md](po-locators.md) | селекторы только в PO |
| `po-step` | [po-step.md](po-step.md) | `@Step` на методах страницы |
| `test-negative` | [test-negative.md](test-negative.md) | negative login |
| `test-taxonomy` | [test-taxonomy.md](test-taxonomy.md) | Epic / Feature / Tag |
| `allure-attach` | [allure-attach.md](allure-attach.md) | screenshot / results |
| `allure-reporting-requirements` | [allure-reporting-requirements.md](allure-reporting-requirements.md) | steps по `@Layer` |
| `cfg-env-profile` | [cfg-env-profile.md](cfg-env-profile.md) | `-Denv=` |
| `cfg-stands` | [cfg-stands.md](cfg-stands.md) | pipeline / stage / prod при написании теста |
| `cfg-base-url` | [cfg-base-url.md](cfg-base-url.md) | `baseUrl` / `apiBaseUrl` |
| `ci-gradle-args` | [ci-gradle-args.md](ci-gradle-args.md) | эталонные Gradle-команды |
| `remote-selenoid` | [remote-selenoid.md](remote-selenoid.md) | браузер на хабе |
| `test-api-layer` | [test-api-layer.md](test-api-layer.md) | Rest Assured, не Selenide |
| `base-lifecycle` | [base-lifecycle.md](base-lifecycle.md) | `TestBase` setup/teardown |

Модуль 1: явный путь к файлу. Модуль 2: зачем не класть все чанки в один промпт.
