---
id: test-api-layer
domain: testing
adr: 009
tags: [api, rest-assured]
related: [test-negative, test-layers, cfg-stands, testdata-user]
---
# API слой

**id:** `test-api-layer`

Канон: `api/ApiTestBase.java`, `api/AuthApiClient.java`, `tests/api/AuthApiTests.java`.  
`@Layer("api")` + `@Tag("api")`. Браузера нет.

Wrong password на HTTP: `AuthApiTests#loginWithInvalidPassword` — 401 + `schemas/error.json` + `"Wrong login or password"`.  
Почему это не новый e2e-клик — ADR `009-login-401-is-api`.

```bash
./gradlew test -Denv=ci -DincludeTags=api
```

## Do

- Новый endpoint → класс в `tests/api/`, assert через Rest Assured.
- Схема: `src/test/resources/schemas/`.

## Don't

- `@Layer("api")` + `TestBase` / Selenide.
- Проверять JSON-контракт логина только кликами в UI.
- Логин сида через `UserBuilder` — литералы `"user1"` / `"password1"` (чанк `testdata-user`).
