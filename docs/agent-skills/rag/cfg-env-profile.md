---
id: cfg-env-profile
domain: config
adr: 002
tags: [env, properties]
---
# Выбор стенда

**id:** `cfg-env-profile`

`-Denv=multistack_ci` → `src/test/resources/config/multistack_ci.properties`.

Файлы в takeaway: `default.properties` (флаги) + `multistack_ci` / `multistack_mock` / `multistack_prod` (куда стучимся).

Ось **pipeline / stage / prod** — чанк `cfg-stands`. Тест не содержит URL стенда.

## Do

- Всегда передавать `-Denv=`.
- URL только в properties / `-DbaseUrl`, не в тесте.

## Don't

- Файл `local.properties` / `ci.properties` без stand-имени.
- Хардкод `http://localhost:9821` в `LoginTests`.
