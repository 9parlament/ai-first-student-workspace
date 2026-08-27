---
id: e2e-layers
domain: testing
tags: [structure, testbase, pages]
---
# Слои тестового модуля

**id:** `e2e-layers`

Корень: `tests/java/tests-java-gradle-junit5-allure3-selenide/src/test/java/`.

| Пакет | Назначение |
|-------|------------|
| `config/` | env profiles, typed keys |
| `api/` | `ApiTestBase`, HTTP-клиенты |
| `pages/` | Page Objects, локаторы, `@Step` |
| `helpers/` | `User` / `UserBuilder` / `DataFaker` — throwaway, не сид (чанк `testdata-user`) |
| `tests/e2e/` | браузерные сценарии, `TestBase` |
| `tests/api/` | HTTP-сценарии, `ApiTestBase` |
| `tests/manual/` | exploratory stubs |
| `tests/infra/` | helpers (config / HAR / CSS; не слой пирамиды) |
| `allure/` | attachments |
| `annotations/` | `@Layer`, `@Manual` |

## Do

Новый сценарий: сначала PO (или API-клиент) → потом класс теста. URL только из config.

## Don't

- `Configuration.browser` в каждом `@Test`.
- CSS/xpath в классе `*Tests`.
