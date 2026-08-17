---
id: test-pyramid
domain: testing
adr: 005
tags: [pyramid, layer, slice]
---
# Пирамида (takeaway)

**id:** `test-pyramid`

`@Layer` — ярус пирамиды. **CI slice** (screenshot / mock) — не ярус: тот же `@Layer("e2e")` + другой `@Tag`.

## Ярусы в этом проекте

| `@Layer` | Где код | Зачем |
|----------|---------|--------|
| unit | `backend-java-spring/src/test` | логика без HTTP/браузера |
| api | `tests/…/tests/api/` | HTTP, Rest Assured, `ApiTestBase` |
| e2e | `tests/…/tests/e2e/` | браузер, Page Object, `TestBase` |
| manual | `tests/…/tests/manual/` | `@Manual` + `Allure.step`, не WebDriver |
| harness | `tests/…/tests/testinfra/` | config/HAR/CSS — инфраструктура тестов |

Frontend RTL (Vitest) живёт во `frontend-typescript-react/` — это не Selenide `@Tag("component")`.

## Slice ≠ слой

| Slice | Как отбираем | Не делать |
|-------|----------------|-----------|
| screenshot | `@Tag("screenshot")` + env mock/prod | новый `@Layer("screenshot")` |
| mock | `@Tag("mock")` + `-Denv=multistack_mock` | путать с api-слоем |

«100% пирамида» = каждый **сценарий на своём ярусе** в правильной пропорции, не 100% line coverage.

## Don't

- Закрывать api-контракт только e2e.
- Писать e2e там, где хватает `AuthApiTests`.
