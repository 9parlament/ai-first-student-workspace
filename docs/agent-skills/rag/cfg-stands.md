---
id: cfg-stands
domain: config
adr: 002
tags: [env, pipeline, stage, prod]
related: [cfg-env-profile, cfg-base-url, remote-selenoid, ci-gradle-args]
---
# Pipeline / stage / prod — при разработке теста

**id:** `cfg-stands`

Автотест пишется **один раз** под несколько стендов. Стенд = `-Denv=` + `config/*.properties`, не ветка `if (prod)` в `LoginTests`.

## Слова курса → takeaway

| Слово | Смысл | В takeaway сейчас |
|-------|--------|-------------------|
| **pipeline** (CI) | эфемерный стенд в GitHub Actions / Jenkins, тот же код что локальный compose | `-Denv=multistack_ci` |
| **stage** | предпрод: прод-подобный URL + Selenoid; данные можно портить осторожно | `-Denv=multistack_stage` — [https://stage.ai-first.autotests.ai/](https://stage.ai-first.autotests.ai/) |
| **prod** | боевой / витринный деплой этого стека (не матрица `/stack/…`) | `-Denv=multistack_prod` — [https://ai-first.autotests.ai/](https://ai-first.autotests.ai/) + `remoteUrl` хаба (креды не в git) |
| mock | UI без живого backend | `-Denv=multistack_mock` (slice, не ярус пирамиды) |

Локальный `docker compose` на занятии ≈ pipeline-профиль (`multistack_ci`). Это не «третий прод».

## Что решить, пока пишешь тест (не после)

1. **URL и хаб** — только properties / `-DbaseUrl` / `-DremoteUrl`. Запрет: `localhost`, `autotests.ai`, пароль хаба в Java.
2. **Данные** — сиды вроде `user1` / `password1` должны существовать на **каждом** стенде, где тест поедет. Уникальный email на prod — фабрика + teardown или не гонять этот кейс на prod.
3. **Разрушение** — delete/drop/admin на prod **нельзя**, пока нет явного OK и отдельного `@Tag`. Pipeline/stage — можно, если стенд пересоздаётся.
4. **Какой срез куда** — pipeline: api + e2e slice. Prod: узкий smoke (тот же `@Tag("e2e")`, не новый класс «ProdLoginTests»). Stage: как prod, плюс то, что нельзя на бою.
5. **Браузер** — ci локально Chrome; stage/prod обычно Selenoid (`remote-selenoid`). Тест не знает, local это или remote.

## Do

- Новый тест: проговорить «поедет на pipeline / stage / prod?» и записать в ответ skill.
- Нет DNS/стенда → не выдумывать другой host в Java; URL только из properties.
- Jenkins `{login}-app-tests` = pipeline: те же `-Denv` и tags, что в job.

## Don't

- `if (env.contains("prod"))` в тесте.
- Отдельный репозиторий «тесты для прода».
- Гонять prod-профиль без рабочего `remoteUrl`.
- Считать «зелёный на localhost» достаточным для merge.
